---
ms.openlocfilehash: 12a6c18b52e2bc9aba5ad69c8bb9ab8091c11a64
ms.sourcegitcommit: e0d9b18d2d4cbeb4a48890f3420a47e6a90abc53
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "49347733"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="367c4-101">Nesta seção, você criará um projeto de estrutura de bot.</span><span class="sxs-lookup"><span data-stu-id="367c4-101">In this section you'll create a Bot Framework project.</span></span>

1. <span data-ttu-id="367c4-102">Abra a interface de linha de comando (CLI) em um diretório onde você deseja criar o projeto.</span><span class="sxs-lookup"><span data-stu-id="367c4-102">Open your command-line interface (CLI) in a directory where you want to create the project.</span></span> <span data-ttu-id="367c4-103">Execute o seguinte comando para criar um novo projeto usando o modelo **Microsoft. bot. Framework. CSharp. EchoBot** .</span><span class="sxs-lookup"><span data-stu-id="367c4-103">Run the following command to create new project using the **Microsoft.Bot.Framework.CSharp.EchoBot** template.</span></span>

    ```dotnetcli
    dotnet new echobot -n GraphCalendarBot
    ```

    > [!NOTE]
    > <span data-ttu-id="367c4-104">Se você receber um `No templates matched the input template name: echobot.` erro, instale o modelo com o comando a seguir e execute novamente o comando anterior.</span><span class="sxs-lookup"><span data-stu-id="367c4-104">If you receive an `No templates matched the input template name: echobot.` error, install the template with the following command and re-run the previous command.</span></span>
    >
    > ```dotnetcli
    > dotnet new -i Microsoft.Bot.Framework.CSharp.EchoBot
    > ```

1. <span data-ttu-id="367c4-105">Renomeie a classe **EchoBot** padrão como **CalendarBot**.</span><span class="sxs-lookup"><span data-stu-id="367c4-105">Rename the default **EchoBot** class to **CalendarBot**.</span></span> <span data-ttu-id="367c4-106">Abra **./bots/EchoBot.cs** e substitua todas as instâncias do `EchoBot` com `CalendarBot` .</span><span class="sxs-lookup"><span data-stu-id="367c4-106">Open **./Bots/EchoBot.cs** and replace all instances of `EchoBot` with `CalendarBot`.</span></span> <span data-ttu-id="367c4-107">Renomeie o arquivo para **CalendarBot.cs**.</span><span class="sxs-lookup"><span data-stu-id="367c4-107">Rename the file to **CalendarBot.cs**.</span></span>

1. <span data-ttu-id="367c4-108">Substitua todas as instâncias de `EchoBot` com `CalendarBot` nos arquivos **. cs** restantes.</span><span class="sxs-lookup"><span data-stu-id="367c4-108">Replace all instances of `EchoBot` with `CalendarBot` in the remaining **.cs** files.</span></span>

1. <span data-ttu-id="367c4-109">Na sua CLI, altere o diretório atual para o diretório **GraphCalendarBot** e execute o comando a seguir para confirmar se o projeto é criado.</span><span class="sxs-lookup"><span data-stu-id="367c4-109">In your CLI, change the current directory to the **GraphCalendarBot** directory and run the following command to confirm the project builds.</span></span>

    ```dotnetcli
    dotnet build
    ```

## <a name="add-nuget-packages"></a><span data-ttu-id="367c4-110">Adicionar pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="367c4-110">Add NuGet packages</span></span>

<span data-ttu-id="367c4-111">Antes de prosseguir, instale alguns pacotes NuGet adicionais que serão usados posteriormente.</span><span class="sxs-lookup"><span data-stu-id="367c4-111">Before moving on, install some additional NuGet packages that you will use later.</span></span>

- <span data-ttu-id="367c4-112">[AdaptiveCards](https://www.nuget.org/packages/AdaptiveCards/) para permitir que o bot envie cartões adaptáveis em respostas.</span><span class="sxs-lookup"><span data-stu-id="367c4-112">[AdaptiveCards](https://www.nuget.org/packages/AdaptiveCards/) to allow the bot to send Adaptive Cards in responses.</span></span>
- <span data-ttu-id="367c4-113">[Microsoft. bot. Builder. dialogs](https://www.nuget.org/packages/Microsoft.Bot.Builder.Dialogs/) para adicionar o suporte de caixa de diálogo ao bot.</span><span class="sxs-lookup"><span data-stu-id="367c4-113">[Microsoft.Bot.Builder.Dialogs](https://www.nuget.org/packages/Microsoft.Bot.Builder.Dialogs/) to add dialog support to the bot.</span></span>
- <span data-ttu-id="367c4-114">[Microsoft. Recognizers. Text. datatypes. Timex](https://www.nuget.org/packages/Microsoft.Recognizers.Text.DataTypes.TimexExpression/) para converter as expressões de Timex retornadas de prompts de bot em objetos **DateTime** .</span><span class="sxs-lookup"><span data-stu-id="367c4-114">[Microsoft.Recognizers.Text.DataTypes.TimexExpression](https://www.nuget.org/packages/Microsoft.Recognizers.Text.DataTypes.TimexExpression/) to convert the TIMEX expressions returned from bot prompts into **DateTime** objects.</span></span>
- <span data-ttu-id="367c4-115">[Microsoft. Graph](https://www.nuget.org/packages/Microsoft.Graph/) para fazer chamadas para o Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="367c4-115">[Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) for making calls to Microsoft Graph.</span></span>

1. <span data-ttu-id="367c4-116">Execute os seguintes comandos em sua CLI para instalar as dependências.</span><span class="sxs-lookup"><span data-stu-id="367c4-116">Run the following commands in your CLI to install the dependencies.</span></span>

    ```Shell
    dotnet add package AdaptiveCards --version 2.2.0
    dotnet add package Microsoft.Bot.Builder.Dialogs --version 4.10.3
    dotnet add package Microsoft.Bot.Builder.Integration.AspNet.Core --version 4.10.3
    dotnet add package Microsoft.Recognizers.Text.DataTypes.TimexExpression --version 1.4.1
    dotnet add package Microsoft.Graph --version 3.18.0
    ```

## <a name="test-the-bot"></a><span data-ttu-id="367c4-117">Testar o bot</span><span class="sxs-lookup"><span data-stu-id="367c4-117">Test the bot</span></span>

<span data-ttu-id="367c4-118">Antes de adicionar qualquer código, teste o bot para verificar se ele funciona corretamente e se o emulador da estrutura de bot está configurado para testá-lo.</span><span class="sxs-lookup"><span data-stu-id="367c4-118">Before adding any code, test the bot to make sure that it works correctly, and that the Bot Framework Emulator is configured to test it.</span></span>

1. <span data-ttu-id="367c4-119">Inicie o bot executando o seguinte comando.</span><span class="sxs-lookup"><span data-stu-id="367c4-119">Start the bot by running the following command.</span></span>

    ```dotnetcli
    dotnet run
    ```

    > [!TIP]
    > <span data-ttu-id="367c4-120">Embora você possa usar qualquer editor de texto para editar os arquivos de origem no projeto, é recomendável usar o [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="367c4-120">While you can use any text editor to edit the source files in the project, we recommend using [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="367c4-121">O Visual Studio Code oferece suporte à depuração, IntelliSense e muito mais.</span><span class="sxs-lookup"><span data-stu-id="367c4-121">Visual Studio Code offers debugging support, Intellisense, and more.</span></span> <span data-ttu-id="367c4-122">Se estiver usando o Visual Studio Code, você pode iniciar o bot usando o menu **executar**  ->  **inicialização de depuração** .</span><span class="sxs-lookup"><span data-stu-id="367c4-122">If using Visual Studio Code, you can start the bot using the **Run** -> **Start Debugging** menu.</span></span>

1. <span data-ttu-id="367c4-123">Confirme se o bot está sendo executado abrindo seu navegador e acessando `http://localhost:3978` .</span><span class="sxs-lookup"><span data-stu-id="367c4-123">Confirm the bot is running by opening your browser and going to `http://localhost:3978`.</span></span> <span data-ttu-id="367c4-124">Você verá um **bot pronto!**</span><span class="sxs-lookup"><span data-stu-id="367c4-124">You should see a **Your bot is ready!**</span></span> <span data-ttu-id="367c4-125">Mensagem.</span><span class="sxs-lookup"><span data-stu-id="367c4-125">message.</span></span>

1. <span data-ttu-id="367c4-126">Abra o emulador da estrutura do bot.</span><span class="sxs-lookup"><span data-stu-id="367c4-126">Open the Bot Framework Emulator.</span></span> <span data-ttu-id="367c4-127">Escolha o menu **arquivo** e, em seguida, **abra bot**.</span><span class="sxs-lookup"><span data-stu-id="367c4-127">Choose the **File** menu, then **Open Bot**.</span></span>

1. <span data-ttu-id="367c4-128">Insira `http://localhost:3978/api/messages` na **URL do bot** e, em seguida, selecione **conectar**.</span><span class="sxs-lookup"><span data-stu-id="367c4-128">Enter `http://localhost:3978/api/messages` in the **Bot URL**, then select **Connect**.</span></span>

1. <span data-ttu-id="367c4-129">O bot responde com `Hello and welcome!` na janela de bate-papo.</span><span class="sxs-lookup"><span data-stu-id="367c4-129">The bot responds with `Hello and welcome!` in the chat window.</span></span> <span data-ttu-id="367c4-130">Envie uma mensagem para o bot e confirme que ela a ecoa de volta.</span><span class="sxs-lookup"><span data-stu-id="367c4-130">Send a message to the bot and confirm it echoes it back.</span></span>

    ![Uma captura de tela do emulador de estrutura de bot conectado ao bot](images/test-emulator.png)
