---
ms.openlocfilehash: dc5816eb653053d63bfe3bf48413b3557583d109
ms.sourcegitcommit: e0d9b18d2d4cbeb4a48890f3420a47e6a90abc53
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "49347720"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="b2432-101">Nesta seção, você usará o SDK do Microsoft Graph para adicionar um evento ao calendário do usuário.</span><span class="sxs-lookup"><span data-stu-id="b2432-101">In this section you'll use the Microsoft Graph SDK to add an event to the user's calendar.</span></span>

## <a name="implement-a-dialog"></a><span data-ttu-id="b2432-102">Implementar uma caixa de diálogo</span><span class="sxs-lookup"><span data-stu-id="b2432-102">Implement a dialog</span></span>

<span data-ttu-id="b2432-103">Comece criando uma nova caixa de diálogo personalizada para solicitar ao usuário os valores necessários para adicionar um evento ao seu calendário.</span><span class="sxs-lookup"><span data-stu-id="b2432-103">Start by creating a new custom dialog to prompt the user for the values needed to add an event to their calendar.</span></span> <span data-ttu-id="b2432-104">Esta caixa de diálogo usará um **WaterfallDialog** para realizar as seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="b2432-104">This dialog will use a **WaterfallDialog** to do the following steps.</span></span>

- <span data-ttu-id="b2432-105">Solicitar um assunto</span><span class="sxs-lookup"><span data-stu-id="b2432-105">Prompt for a subject</span></span>
- <span data-ttu-id="b2432-106">Pergunte se o usuário deseja convidar pessoas</span><span class="sxs-lookup"><span data-stu-id="b2432-106">Ask if the user wants to invite people</span></span>
- <span data-ttu-id="b2432-107">Solicitar participantes (se o usuário disse sim para a etapa anterior)</span><span class="sxs-lookup"><span data-stu-id="b2432-107">Prompt for attendees (if user said yes to previous step)</span></span>
- <span data-ttu-id="b2432-108">Solicitar uma data e hora de início</span><span class="sxs-lookup"><span data-stu-id="b2432-108">Prompt for a start date and time</span></span>
- <span data-ttu-id="b2432-109">Solicitar data e hora de término</span><span class="sxs-lookup"><span data-stu-id="b2432-109">Prompt for an end date and time</span></span>
- <span data-ttu-id="b2432-110">Exibir todos os valores coletados e solicitar que o usuário confirme</span><span class="sxs-lookup"><span data-stu-id="b2432-110">Display all of the collected values and ask user to confirm</span></span>
- <span data-ttu-id="b2432-111">Se o usuário confirmar, obter o token de acesso de **OAuthPrompt**</span><span class="sxs-lookup"><span data-stu-id="b2432-111">If user confirms, get access token from **OAuthPrompt**</span></span>
- <span data-ttu-id="b2432-112">Criar o evento</span><span class="sxs-lookup"><span data-stu-id="b2432-112">Create the event</span></span>

1. <span data-ttu-id="b2432-113">Crie um novo arquivo no diretório **./dialogs** chamado **NewEventDialog.cs** e adicione o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="b2432-113">Create a new file in the **./Dialogs** directory named **NewEventDialog.cs** and add the following code.</span></span>

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

    <span data-ttu-id="b2432-114">Este é o Shell de uma nova caixa de diálogo que solicitará ao usuário os valores necessários para adicionar um evento ao seu calendário.</span><span class="sxs-lookup"><span data-stu-id="b2432-114">This is the shell of a new dialog that will prompt the user for the values needed to add an event to their calendar.</span></span>

1. <span data-ttu-id="b2432-115">Adicione a função a seguir à classe **NewEventDialog** para solicitar ao usuário um assunto.</span><span class="sxs-lookup"><span data-stu-id="b2432-115">Add the following function to the **NewEventDialog** class to prompt the user for a subject.</span></span>

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="PromptForSubjectSnippet":::

1. <span data-ttu-id="b2432-116">Adicione a função a seguir à classe **NewEventDialog** para armazenar o assunto que o usuário deu na etapa anterior e solicitar se deseja adicionar participantes.</span><span class="sxs-lookup"><span data-stu-id="b2432-116">Add the following function to the **NewEventDialog** class to store the subject the user gave in the previous step, and to ask if they want to add attendees.</span></span>

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="PromptForAddAttendeesSnippet":::

1. <span data-ttu-id="b2432-117">Adicione a função a seguir à classe **NewEventDialog** para verificar a resposta do usuário da etapa anterior e solicitar ao usuário uma lista de participantes, se necessário.</span><span class="sxs-lookup"><span data-stu-id="b2432-117">Add the following function to the **NewEventDialog** class to check the user's response from the previous step and prompt the user for a list of attendees if needed.</span></span>

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="PromptForAttendeesSnippet":::

1. <span data-ttu-id="b2432-118">Adicione a função a seguir à classe **NewEventDialog** para armazenar a lista de participantes da etapa anterior (se presente) e solicitar ao usuário uma data e hora de início.</span><span class="sxs-lookup"><span data-stu-id="b2432-118">Add the following function to the **NewEventDialog** class to store the list of attendees from the previous step (if present) and prompt the user for a start date and time.</span></span>

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="PromptForStartSnippet":::

1. <span data-ttu-id="b2432-119">Adicione a função a seguir à classe **NewEventDialog** para armazenar o valor inicial da etapa anterior e solicitar ao usuário uma data e hora de término.</span><span class="sxs-lookup"><span data-stu-id="b2432-119">Add the following function to the **NewEventDialog** class to store the start value from the previous step and prompt the user for an end date and time.</span></span>

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="PromptForEndSnippet":::

1. <span data-ttu-id="b2432-120">Adicione a função a seguir à classe **NewEventDialog** para armazenar o valor final da etapa anterior e solicitar que o usuário confirme todas as entradas.</span><span class="sxs-lookup"><span data-stu-id="b2432-120">Add the following function to the **NewEventDialog** class to store the end value from the previous step and ask the user to confirm all of the inputs.</span></span>

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="ConfirmNewEventSnippet":::

1. <span data-ttu-id="b2432-121">Adicione a função a seguir à classe **NewEventDialog** para verificar a resposta do usuário da etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="b2432-121">Add the following function to the **NewEventDialog** class to check the user's response from the previous step.</span></span> <span data-ttu-id="b2432-122">Se o usuário confirmar as entradas, use a classe **OAuthPrompt** para obter um token de acesso.</span><span class="sxs-lookup"><span data-stu-id="b2432-122">If the user confirms the inputs, use the **OAuthPrompt** class to get an access token.</span></span> <span data-ttu-id="b2432-123">Caso contrário, Finalize a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b2432-123">Otherwise, end the dialog.</span></span>

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="GetTokenSnippet":::

1. <span data-ttu-id="b2432-124">Adicione a função a seguir à classe **NewEventDialog** para usar o SDK do Microsoft Graph para criar o novo evento.</span><span class="sxs-lookup"><span data-stu-id="b2432-124">Add the following function to the **NewEventDialog** class to use the Microsoft Graph SDK to create the new event.</span></span>

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="AddEventSnippet":::

    <span data-ttu-id="b2432-125">Considere o que esse código faz.</span><span class="sxs-lookup"><span data-stu-id="b2432-125">Consider what this code does.</span></span>

    - <span data-ttu-id="b2432-126">Ele obtém o **MailboxSettings** do usuário para determinar o fuso horário preferencial do usuário.</span><span class="sxs-lookup"><span data-stu-id="b2432-126">It gets the user's **MailboxSettings** to determine the user's preferred time zone.</span></span>
    - <span data-ttu-id="b2432-127">Ele cria um objeto **Event** usando os valores fornecidos pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="b2432-127">It creates an **Event** object using the values provided by the user.</span></span> <span data-ttu-id="b2432-128">Observe que as propriedades **Start** e **end** são definidas com o fuso horário do usuário.</span><span class="sxs-lookup"><span data-stu-id="b2432-128">Note that the **Start** and **End** properties are set with the user's time zone.</span></span>
    - <span data-ttu-id="b2432-129">Ele cria o evento no calendário do usuário.</span><span class="sxs-lookup"><span data-stu-id="b2432-129">It creates the event on the user's calendar.</span></span>

## <a name="add-validation"></a><span data-ttu-id="b2432-130">Adicionar validação</span><span class="sxs-lookup"><span data-stu-id="b2432-130">Add validation</span></span>

<span data-ttu-id="b2432-131">Agora, adicione a validação à entrada do usuário para evitar erros durante a criação do evento com o Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="b2432-131">Now add validation to the user's input to avoid errors when creating the event with Microsoft Graph.</span></span> <span data-ttu-id="b2432-132">Queremos garantir que:</span><span class="sxs-lookup"><span data-stu-id="b2432-132">We want to make sure that:</span></span>

- <span data-ttu-id="b2432-133">Se o usuário fornece uma lista de participantes, deve ser uma lista delimitada por ponto e vírgula de endereços de email válidos.</span><span class="sxs-lookup"><span data-stu-id="b2432-133">If the user gives an attendee list, it should be a semicolon-delimited list of valid email addresses.</span></span>
- <span data-ttu-id="b2432-134">A data/hora de início deve ser uma data e hora válidas.</span><span class="sxs-lookup"><span data-stu-id="b2432-134">The start date/time should be a valid date and time.</span></span>
- <span data-ttu-id="b2432-135">A data/hora de término deve ser uma data e hora válida e deve ser depois do início.</span><span class="sxs-lookup"><span data-stu-id="b2432-135">The end date/time should be a valid date and time, and should be later than the start.</span></span>

1. <span data-ttu-id="b2432-136">Adicione a função a seguir à classe **NewEventDialog** para validar a entrada do usuário para os participantes.</span><span class="sxs-lookup"><span data-stu-id="b2432-136">Add the following function to the **NewEventDialog** class to validate the user's entry for attendees.</span></span>

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="AttendeesValidatorSnippet":::

1. <span data-ttu-id="b2432-137">Adicione as seguintes funções à classe **NewEventDialog** para validar a entrada do usuário para data e hora de início.</span><span class="sxs-lookup"><span data-stu-id="b2432-137">Add the following functions to the **NewEventDialog** class to validate the user's entry for start date and time.</span></span>

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="StartValidatorSnippet":::

1. <span data-ttu-id="b2432-138">Adicione a função a seguir à classe **NewEventDialog** para validar a entrada do usuário para data e hora de término.</span><span class="sxs-lookup"><span data-stu-id="b2432-138">Add the following function to the **NewEventDialog** class to validate the user's entry for end date and time.</span></span>

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="EndValidatorSnippet":::

## <a name="add-steps-to-waterfalldialog"></a><span data-ttu-id="b2432-139">Adicionar etapas a WaterfallDialog</span><span class="sxs-lookup"><span data-stu-id="b2432-139">Add steps to WaterfallDialog</span></span>

<span data-ttu-id="b2432-140">Agora que você tem todas as "etapas" para a caixa de diálogo, a última etapa é adicioná-las a um **WaterfallDialog** no construtor e, em seguida, adicionar **NewEventDialog** ao **MainDialog**.</span><span class="sxs-lookup"><span data-stu-id="b2432-140">Now that you have all of the "steps" for the dialog, the last step is to add them to a **WaterfallDialog** in the constructor, then add the **NewEventDialog** to the **MainDialog**.</span></span>

1. <span data-ttu-id="b2432-141">Localize o construtor **NewEventDialog** e adicione o código a seguir a ele.</span><span class="sxs-lookup"><span data-stu-id="b2432-141">Locate the **NewEventDialog** constructor and add the following code to it.</span></span>

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/NewEventDialog.cs" id="ConstructorSnippet":::

    <span data-ttu-id="b2432-142">Isso adiciona todas as caixas de diálogo que são usadas e adiciona todas as funções que você implementou como etapas no **WaterfallDialog**.</span><span class="sxs-lookup"><span data-stu-id="b2432-142">This adds all of the dialogs that are used, and adds all of the functions you implemented as steps in the **WaterfallDialog**.</span></span>

1. <span data-ttu-id="b2432-143">Abra **./dialogs/MainDialog.cs** e adicione a seguinte linha ao construtor.</span><span class="sxs-lookup"><span data-stu-id="b2432-143">Open **./Dialogs/MainDialog.cs** and add the following line to the constructor.</span></span>

    ```csharp
    AddDialog(new NewEventDialog(configuration, graphClientService));
    ```

1. <span data-ttu-id="b2432-144">Substitua o código dentro do `else if (command.StartsWith("add event"))` bloco em `ProcessStepAsync` com o seguinte.</span><span class="sxs-lookup"><span data-stu-id="b2432-144">Replace the code inside the `else if (command.StartsWith("add event"))` block in `ProcessStepAsync` with the following.</span></span>

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/MainDialog.cs" id="AddEventSnippet" highlight="3":::

1. <span data-ttu-id="b2432-145">Salve todas as suas alterações e reinicie o bot.</span><span class="sxs-lookup"><span data-stu-id="b2432-145">Save all of your changes and restart the bot.</span></span>

1. <span data-ttu-id="b2432-146">Use o emulador da estrutura de bot para se conectar ao bot e fazer logon.</span><span class="sxs-lookup"><span data-stu-id="b2432-146">Use the Bot Framework Emulator to connect to the bot and log in.</span></span> <span data-ttu-id="b2432-147">Selecione o botão **Adicionar evento** .</span><span class="sxs-lookup"><span data-stu-id="b2432-147">Select the **Add event** button.</span></span>

1. <span data-ttu-id="b2432-148">Responda aos prompts para criar um novo evento.</span><span class="sxs-lookup"><span data-stu-id="b2432-148">Respond to the prompts to create a new event.</span></span> <span data-ttu-id="b2432-149">Observe que, quando solicitado para os valores inicial e final, você pode usar frases como "hoje em 3PM" ou "agora".</span><span class="sxs-lookup"><span data-stu-id="b2432-149">Note that when prompted for start and end values, you can use phrases like "today at 3PM", or "now".</span></span>

    ![Uma captura de tela da caixa de diálogo Adicionar evento no emulador da estrutura do bot](images/add-event.png)
