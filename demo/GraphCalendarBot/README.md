---
ms.openlocfilehash: c0fd9a9f5529f202c125d7f1e7c6b50fa9dc630d
ms.sourcegitcommit: e0d9b18d2d4cbeb4a48890f3420a47e6a90abc53
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "49347736"
---
# <a name="graphcalendarbot"></a><span data-ttu-id="574ea-101">GraphCalendarBot</span><span class="sxs-lookup"><span data-stu-id="574ea-101">GraphCalendarBot</span></span>

<span data-ttu-id="574ea-102">Amostra de bot de eco v4 da estrutura de bot.</span><span class="sxs-lookup"><span data-stu-id="574ea-102">Bot Framework v4 echo bot sample.</span></span>

<span data-ttu-id="574ea-103">Este bot foi criado usando a [estrutura de bot](https://dev.botframework.com), ele mostra como criar um bot simples que aceita entrada do usuário e o ecoa de volta.</span><span class="sxs-lookup"><span data-stu-id="574ea-103">This bot has been created using [Bot Framework](https://dev.botframework.com), it shows how to create a simple bot that accepts input from the user and echoes it back.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="574ea-104">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="574ea-104">Prerequisites</span></span>

- <span data-ttu-id="574ea-105">[.NET Core SDK](https://dotnet.microsoft.com/download) versão 3,1</span><span class="sxs-lookup"><span data-stu-id="574ea-105">[.NET Core SDK](https://dotnet.microsoft.com/download) version 3.1</span></span>

  ```bash
  # determine dotnet version
  dotnet --version
  ```

## <a name="to-try-this-sample"></a><span data-ttu-id="574ea-106">Para testar este exemplo</span><span class="sxs-lookup"><span data-stu-id="574ea-106">To try this sample</span></span>

- <span data-ttu-id="574ea-107">Em um terminal, navegue até `GraphCalendarBot`</span><span class="sxs-lookup"><span data-stu-id="574ea-107">In a terminal, navigate to `GraphCalendarBot`</span></span>

    ```bash
    # change into project folder
    cd GraphCalendarBot
    ```

- <span data-ttu-id="574ea-108">Execute o bot a partir de um terminal ou do Visual Studio, escolha A opção A ou B.</span><span class="sxs-lookup"><span data-stu-id="574ea-108">Run the bot from a terminal or from Visual Studio, choose option A or B.</span></span>

  <span data-ttu-id="574ea-109">A) de um terminal</span><span class="sxs-lookup"><span data-stu-id="574ea-109">A) From a terminal</span></span>

  ```bash
  # run the bot
  dotnet run
  ```

  <span data-ttu-id="574ea-110">B) ou do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="574ea-110">B) Or from Visual Studio</span></span>

  - <span data-ttu-id="574ea-111">Iniciar o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="574ea-111">Launch Visual Studio</span></span>
  - <span data-ttu-id="574ea-112">Arquivo > Open-> Project/Solution</span><span class="sxs-lookup"><span data-stu-id="574ea-112">File -> Open -> Project/Solution</span></span>
  - <span data-ttu-id="574ea-113">Navegar até a `GraphCalendarBot` pasta</span><span class="sxs-lookup"><span data-stu-id="574ea-113">Navigate to `GraphCalendarBot` folder</span></span>
  - <span data-ttu-id="574ea-114">Selecionar `GraphCalendarBot.csproj` arquivo</span><span class="sxs-lookup"><span data-stu-id="574ea-114">Select `GraphCalendarBot.csproj` file</span></span>
  - <span data-ttu-id="574ea-115">Pressione `F5` para executar o projeto</span><span class="sxs-lookup"><span data-stu-id="574ea-115">Press `F5` to run the project</span></span>

## <a name="testing-the-bot-using-bot-framework-emulator"></a><span data-ttu-id="574ea-116">Testando o bot usando o emulador da estrutura de bot</span><span class="sxs-lookup"><span data-stu-id="574ea-116">Testing the bot using Bot Framework Emulator</span></span>

<span data-ttu-id="574ea-117">O [emulador de estrutura de bot](https://github.com/microsoft/botframework-emulator) é um aplicativo de área de trabalho que permite aos desenvolvedores de bot testar e depurar seus bots no localhost ou executar remotamente por meio de um túnel.</span><span class="sxs-lookup"><span data-stu-id="574ea-117">[Bot Framework Emulator](https://github.com/microsoft/botframework-emulator) is a desktop application that allows bot developers to test and debug their bots on localhost or running remotely through a tunnel.</span></span>

- <span data-ttu-id="574ea-118">Instale o emulador de estrutura de bot versão 4.9.0 ou superior [a partir daqui](https://github.com/Microsoft/BotFramework-Emulator/releases)</span><span class="sxs-lookup"><span data-stu-id="574ea-118">Install the Bot Framework Emulator version 4.9.0 or greater from [here](https://github.com/Microsoft/BotFramework-Emulator/releases)</span></span>

### <a name="connect-to-the-bot-using-bot-framework-emulator"></a><span data-ttu-id="574ea-119">Conectar-se ao bot usando o emulador da estrutura de bot</span><span class="sxs-lookup"><span data-stu-id="574ea-119">Connect to the bot using Bot Framework Emulator</span></span>

- <span data-ttu-id="574ea-120">Iniciar emulador de estrutura de bot</span><span class="sxs-lookup"><span data-stu-id="574ea-120">Launch Bot Framework Emulator</span></span>
- <span data-ttu-id="574ea-121">> bot de arquivo aberto</span><span class="sxs-lookup"><span data-stu-id="574ea-121">File -> Open Bot</span></span>
- <span data-ttu-id="574ea-122">Insira uma URL de bot de `http://localhost:3978/api/messages`</span><span class="sxs-lookup"><span data-stu-id="574ea-122">Enter a Bot URL of `http://localhost:3978/api/messages`</span></span>

## <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="574ea-123">Implantar o bot no Azure</span><span class="sxs-lookup"><span data-stu-id="574ea-123">Deploy the bot to Azure</span></span>

<span data-ttu-id="574ea-124">Para saber mais sobre como implantar um bot no Azure, confira [implantar o bot no Azure](https://aka.ms/azuredeployment) para obter uma lista completa de instruções de implantação.</span><span class="sxs-lookup"><span data-stu-id="574ea-124">To learn more about deploying a bot to Azure, see [Deploy your bot to Azure](https://aka.ms/azuredeployment) for a complete list of deployment instructions.</span></span>

## <a name="further-reading"></a><span data-ttu-id="574ea-125">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="574ea-125">Further reading</span></span>

- [<span data-ttu-id="574ea-126">Documentação da estrutura do bot</span><span class="sxs-lookup"><span data-stu-id="574ea-126">Bot Framework Documentation</span></span>](https://docs.botframework.com)
- [<span data-ttu-id="574ea-127">Noções básicas de bot</span><span class="sxs-lookup"><span data-stu-id="574ea-127">Bot Basics</span></span>](https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0)
- [<span data-ttu-id="574ea-128">Processamento de atividades</span><span class="sxs-lookup"><span data-stu-id="574ea-128">Activity processing</span></span>](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-concept-activity-processing?view=azure-bot-service-4.0)
- [<span data-ttu-id="574ea-129">Introdução ao serviço do Azure bot</span><span class="sxs-lookup"><span data-stu-id="574ea-129">Azure Bot Service Introduction</span></span>](https://docs.microsoft.com/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0)
- [<span data-ttu-id="574ea-130">Documentação do serviço do Azure bot</span><span class="sxs-lookup"><span data-stu-id="574ea-130">Azure Bot Service Documentation</span></span>](https://docs.microsoft.com/azure/bot-service/?view=azure-bot-service-4.0)
- [<span data-ttu-id="574ea-131">Ferramentas da CLI do .NET Core</span><span class="sxs-lookup"><span data-stu-id="574ea-131">.NET Core CLI tools</span></span>](https://docs.microsoft.com/en-us/dotnet/core/tools/?tabs=netcore2x)
- [<span data-ttu-id="574ea-132">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="574ea-132">Azure CLI</span></span>](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
- [<span data-ttu-id="574ea-133">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="574ea-133">Azure Portal</span></span>](https://portal.azure.com)
- [<span data-ttu-id="574ea-134">Compreensão do idioma usando LUIS</span><span class="sxs-lookup"><span data-stu-id="574ea-134">Language Understanding using LUIS</span></span>](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/)
- [<span data-ttu-id="574ea-135">Serviço de conector de bot e canais</span><span class="sxs-lookup"><span data-stu-id="574ea-135">Channels and Bot Connector Service</span></span>](https://docs.microsoft.com/en-us/azure/bot-service/bot-concepts?view=azure-bot-service-4.0)

<span data-ttu-id="574ea-136">Gerado usando `dotnet new echobot` v 4.10.2</span><span class="sxs-lookup"><span data-stu-id="574ea-136">Generated using `dotnet new echobot` v4.10.2</span></span>
