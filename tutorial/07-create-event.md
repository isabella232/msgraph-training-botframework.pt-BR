---
ms.openlocfilehash: dc5816eb653053d63bfe3bf48413b3557583d109
ms.sourcegitcommit: e0d9b18d2d4cbeb4a48890f3420a47e6a90abc53
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "49347720"
---
<!-- markdownlint-disable MD002 MD041 -->

Nesta seção, você usará o SDK do Microsoft Graph para adicionar um evento ao calendário do usuário.

## <a name="implement-a-dialog"></a>Implementar uma caixa de diálogo

Comece criando uma nova caixa de diálogo personalizada para solicitar ao usuário os valores necessários para adicionar um evento ao seu calendário. Esta caixa de diálogo usará um **WaterfallDialog** para realizar as seguintes etapas.

- Solicitar um assunto
- Pergunte se o usuário deseja convidar pessoas
- Solicitar participantes (se o usuário disse sim para a etapa anterior)
- Solicitar uma data e hora de início
- Solicitar data e hora de término
- Exibir todos os valores coletados e solicitar que o usuário confirme
- Se o usuário confirmar, obter o token de acesso de **OAuthPrompt**
- Criar o evento

1. Crie um novo arquivo no diretório **./dialogs** chamado **NewEventDialog.cs** e adicione o código a seguir.

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Bot.Builder;
    using Microsoft.Bot.Builder.Dialogs;
    using Microsoft.Bot.Schema;
    using Microsoft.Extensions.Configuration;
    using Microsoft.Extensions.Logging;
    using Microsoft.Graph;
    using CalendarBot.Graph;
    using Microsoft.Recognizers.Text.DataTypes.TimexExpression;
    using TimexTypes = Microsoft.Recognizers.Text.DataTypes.TimexExpression.Constants.TimexTypes;

    namespace CalendarBot.Dialogs
    {
        public class NewEventDialog : LogoutDialog
        {
            protected readonly ILogger _logger;
            private readonly IGraphClientService _graphClientService;

            public NewEventDialog(
                IConfiguration configuration,
                IGraphClientService graphClientService)
                : base(nameof(NewEventDialog), configuration["ConnectionName"])
            {

            }

            // Generate a DateTime from the list of
            // DateTimeResolutions provided by the DateTimePrompt
            private static DateTime GetDateTimeFromResolutions(IList<DateTimeResolution> resolutions)
            {
                var timex = new TimexProperty(resolutions[0].Timex);

                // Handle the "now" case
                if (timex.Now ?? false)
                {
                    return DateTime.Now;
                }

                // Otherwise generate a DateTime
                return TimexHelpers.DateFromTimex(timex);
            }
        }
    }
    ```

    Este é o Shell de uma nova caixa de diálogo que solicitará ao usuário os valores necessários para adicionar um evento ao seu calendário.

1. Adicione a função a seguir à classe **NewEventDialog** para solicitar ao usuário um assunto.

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="PromptForSubjectSnippet":::

1. Adicione a função a seguir à classe **NewEventDialog** para armazenar o assunto que o usuário deu na etapa anterior e solicitar se deseja adicionar participantes.

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="PromptForAddAttendeesSnippet":::

1. Adicione a função a seguir à classe **NewEventDialog** para verificar a resposta do usuário da etapa anterior e solicitar ao usuário uma lista de participantes, se necessário.

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="PromptForAttendeesSnippet":::

1. Adicione a função a seguir à classe **NewEventDialog** para armazenar a lista de participantes da etapa anterior (se presente) e solicitar ao usuário uma data e hora de início.

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="PromptForStartSnippet":::

1. Adicione a função a seguir à classe **NewEventDialog** para armazenar o valor inicial da etapa anterior e solicitar ao usuário uma data e hora de término.

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="PromptForEndSnippet":::

1. Adicione a função a seguir à classe **NewEventDialog** para armazenar o valor final da etapa anterior e solicitar que o usuário confirme todas as entradas.

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="ConfirmNewEventSnippet":::

1. Adicione a função a seguir à classe **NewEventDialog** para verificar a resposta do usuário da etapa anterior. Se o usuário confirmar as entradas, use a classe **OAuthPrompt** para obter um token de acesso. Caso contrário, Finalize a caixa de diálogo.

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="GetTokenSnippet":::

1. Adicione a função a seguir à classe **NewEventDialog** para usar o SDK do Microsoft Graph para criar o novo evento.

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="AddEventSnippet":::

    Considere o que esse código faz.

    - Ele obtém o **MailboxSettings** do usuário para determinar o fuso horário preferencial do usuário.
    - Ele cria um objeto **Event** usando os valores fornecidos pelo usuário. Observe que as propriedades **Start** e **end** são definidas com o fuso horário do usuário.
    - Ele cria o evento no calendário do usuário.

## <a name="add-validation"></a>Adicionar validação

Agora, adicione a validação à entrada do usuário para evitar erros durante a criação do evento com o Microsoft Graph. Queremos garantir que:

- Se o usuário fornece uma lista de participantes, deve ser uma lista delimitada por ponto e vírgula de endereços de email válidos.
- A data/hora de início deve ser uma data e hora válidas.
- A data/hora de término deve ser uma data e hora válida e deve ser depois do início.

1. Adicione a função a seguir à classe **NewEventDialog** para validar a entrada do usuário para os participantes.

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="AttendeesValidatorSnippet":::

1. Adicione as seguintes funções à classe **NewEventDialog** para validar a entrada do usuário para data e hora de início.

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="StartValidatorSnippet":::

1. Adicione a função a seguir à classe **NewEventDialog** para validar a entrada do usuário para data e hora de término.

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="EndValidatorSnippet":::

## <a name="add-steps-to-waterfalldialog"></a>Adicionar etapas a WaterfallDialog

Agora que você tem todas as "etapas" para a caixa de diálogo, a última etapa é adicioná-las a um **WaterfallDialog** no construtor e, em seguida, adicionar **NewEventDialog** ao **MainDialog**.

1. Localize o construtor **NewEventDialog** e adicione o código a seguir a ele.

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="ConstructorSnippet":::

    Isso adiciona todas as caixas de diálogo que são usadas e adiciona todas as funções que você implementou como etapas no **WaterfallDialog**.

1. Abra **./dialogs/MainDialog.cs** e adicione a seguinte linha ao construtor.

    ```csharp
    AddDialog(new NewEventDialog(configuration, graphClientService));
    ```

1. Substitua o código dentro do `else if (command.StartsWith("add event"))` bloco em `ProcessStepAsync` com o seguinte.

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/MainDialog.cs" id="AddEventSnippet" highlight="3":::

1. Salve todas as suas alterações e reinicie o bot.

1. Use o emulador da estrutura de bot para se conectar ao bot e fazer logon. Selecione o botão **Adicionar evento** .

1. Responda aos prompts para criar um novo evento. Observe que, quando solicitado para os valores inicial e final, você pode usar frases como "hoje em 3PM" ou "agora".

    ![Uma captura de tela da caixa de diálogo Adicionar evento no emulador da estrutura do bot](images/add-event.png)
