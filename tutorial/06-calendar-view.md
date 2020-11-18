---
ms.openlocfilehash: 65fd8e133174c6ac7bbbbc00487cabc72ebe561d
ms.sourcegitcommit: e0d9b18d2d4cbeb4a48890f3420a47e6a90abc53
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "49347745"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="ecf1d-101">Nesta seção, você usará o SDK do Microsoft Graph para obter os três próximos eventos no calendário do usuário da semana atual.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-101">In this section you'll use the Microsoft Graph SDK to get the next 3 upcoming events on the user's calendar for the current week.</span></span>

## <a name="get-a-calendar-view"></a><span data-ttu-id="ecf1d-102">Obter um modo de exibição de calendário</span><span class="sxs-lookup"><span data-stu-id="ecf1d-102">Get a calendar view</span></span>

<span data-ttu-id="ecf1d-103">Um modo de exibição de calendário é uma lista de eventos no calendário de um usuário que está entre dois valores de data/hora.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-103">A calendar view is a list of events on a user's calendar that fall between two date/time values.</span></span> <span data-ttu-id="ecf1d-104">A vantagem de usar um modo de exibição de calendário é que ele inclui qualquer ocorrência de reuniões recorrentes.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-104">The advantage of using a calendar view is that it includes any occurrences of recurring meetings.</span></span>

1. <span data-ttu-id="ecf1d-105">Abra **./CardHelper.cs** e adicione a função a seguir à classe **CardHelper** .</span><span class="sxs-lookup"><span data-stu-id="ecf1d-105">Open **./CardHelper.cs** and add the following function to the **CardHelper** class.</span></span>

    :::code language="csharp" source="../demo/GraphCalendarBot/CardHelper.cs" id="GetEventCardSnippet":::

    <span data-ttu-id="ecf1d-106">Este código cria um cartão adaptável para renderizar um evento de calendário.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-106">This code builds an Adaptive Card to render a calendar event.</span></span>

1. <span data-ttu-id="ecf1d-107">Abra **./dialogs/MainDialog.cs** e adicione a função a seguir à classe **MainDialog** .</span><span class="sxs-lookup"><span data-stu-id="ecf1d-107">Open **./Dialogs/MainDialog.cs** and add the following function to the **MainDialog** class.</span></span>

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/MainDialog.cs" id="DisplayCalendarViewSnippet":::

    <span data-ttu-id="ecf1d-108">Considere o que esse código faz.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-108">Consider what this code does.</span></span>

    - <span data-ttu-id="ecf1d-109">Ele obtém o **MailboxSettings** do usuário para determinar o fuso horário preferencial do usuário e os formatos de data/hora.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-109">It gets the user's **MailboxSettings** to determine the user's preferred time zone and date/time formats.</span></span>
    - <span data-ttu-id="ecf1d-110">Ele define os valores **StartDateTime** e **EndDateTime** como agora e o final da semana, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-110">It sets the **startDateTime** and **endDateTime** values to now and the end of the week, respectively.</span></span> <span data-ttu-id="ecf1d-111">Isso define a janela de tempo que o modo de exibição de calendário usa.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-111">This defines the window of time that the calendar view uses.</span></span>
    - <span data-ttu-id="ecf1d-112">Ele chama `graphClient.Me.CalendarView` os seguintes detalhes.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-112">It calls `graphClient.Me.CalendarView` with the following details.</span></span>
        - <span data-ttu-id="ecf1d-113">Ele define o `Prefer: outlook.timezone` cabeçalho para o fuso horário preferencial do usuário, fazendo com que as horas de início e de término dos eventos estejam no fuso horário do usuário.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-113">It sets the `Prefer: outlook.timezone` header to the user's preferred time zone, causing the start and end times for the events to be in the user's timezone.</span></span>
        - <span data-ttu-id="ecf1d-114">Ele usa o `Top(3)` método para limitar os resultados apenas aos três primeiros eventos.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-114">It uses the `Top(3)` method to limit the results to only the first 3 events.</span></span>
        - <span data-ttu-id="ecf1d-115">Ele usa `Select` para limitar os campos retornados apenas aos campos usados pelo bot.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-115">It uses `Select` to limit the fields returned to just those fields used by the bot.</span></span>
        - <span data-ttu-id="ecf1d-116">Ele usa `OrderBy` para classificar os eventos por hora de início.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-116">It uses `OrderBy` to sort the events by start time.</span></span>
    - <span data-ttu-id="ecf1d-117">Ele adiciona um cartão adaptável para cada evento à mensagem de resposta.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-117">It adds an Adaptive Card for each event to the reply message.</span></span>

1. <span data-ttu-id="ecf1d-118">Substitua o código dentro do `else if (command.StartsWith("show calendar"))` bloco em `ProcessStepAsync` com o seguinte.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-118">Replace the code inside the `else if (command.StartsWith("show calendar"))` block in `ProcessStepAsync` with the following.</span></span>

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/MainDialog.cs" id="ShowCalendarSnippet" highlight="3":::

1. <span data-ttu-id="ecf1d-119">Salve todas as suas alterações e reinicie o bot.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-119">Save all of your changes and restart the bot.</span></span>

1. <span data-ttu-id="ecf1d-120">Use o emulador da estrutura de bot para se conectar ao bot e fazer logon.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-120">Use the Bot Framework Emulator to connect to the bot and log in.</span></span> <span data-ttu-id="ecf1d-121">Selecione o botão **Mostrar calendário** para exibir o modo de exibição calendário.</span><span class="sxs-lookup"><span data-stu-id="ecf1d-121">Select the **Show calendar** button to display the calendar view.</span></span>

    ![Uma captura de tela do cartão adaptável mostrando os três próximos eventos](images/calendar-view.png)
