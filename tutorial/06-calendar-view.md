---
ms.openlocfilehash: 65fd8e133174c6ac7bbbbc00487cabc72ebe561d
ms.sourcegitcommit: e0d9b18d2d4cbeb4a48890f3420a47e6a90abc53
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "49347745"
---
<!-- markdownlint-disable MD002 MD041 -->

Nesta seção, você usará o SDK do Microsoft Graph para obter os três próximos eventos no calendário do usuário da semana atual.

## <a name="get-a-calendar-view"></a>Obter um modo de exibição de calendário

Um modo de exibição de calendário é uma lista de eventos no calendário de um usuário que está entre dois valores de data/hora. A vantagem de usar um modo de exibição de calendário é que ele inclui qualquer ocorrência de reuniões recorrentes.

1. Abra **./CardHelper.cs** e adicione a função a seguir à classe **CardHelper** .

    :::code language="csharp" source="../demo/GraphCalendarBot/CardHelper.cs" id="GetEventCardSnippet":::

    Este código cria um cartão adaptável para renderizar um evento de calendário.

1. Abra **./dialogs/MainDialog.cs** e adicione a função a seguir à classe **MainDialog** .

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/MainDialog.cs" id="DisplayCalendarViewSnippet":::

    Considere o que esse código faz.

    - Ele obtém o **MailboxSettings** do usuário para determinar o fuso horário preferencial do usuário e os formatos de data/hora.
    - Ele define os valores **StartDateTime** e **EndDateTime** como agora e o final da semana, respectivamente. Isso define a janela de tempo que o modo de exibição de calendário usa.
    - Ele chama `graphClient.Me.CalendarView` os seguintes detalhes.
        - Ele define o `Prefer: outlook.timezone` cabeçalho para o fuso horário preferencial do usuário, fazendo com que as horas de início e de término dos eventos estejam no fuso horário do usuário.
        - Ele usa o `Top(3)` método para limitar os resultados apenas aos três primeiros eventos.
        - Ele usa `Select` para limitar os campos retornados apenas aos campos usados pelo bot.
        - Ele usa `OrderBy` para classificar os eventos por hora de início.
    - Ele adiciona um cartão adaptável para cada evento à mensagem de resposta.

1. Substitua o código dentro do `else if (command.StartsWith("show calendar"))` bloco em `ProcessStepAsync` com o seguinte.

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/MainDialog.cs" id="ShowCalendarSnippet" highlight="3":::

1. Salve todas as suas alterações e reinicie o bot.

1. Use o emulador da estrutura de bot para se conectar ao bot e fazer logon. Selecione o botão **Mostrar calendário** para exibir o modo de exibição calendário.

    ![Uma captura de tela do cartão adaptável mostrando os três próximos eventos](images/calendar-view.png)
