---
ms.openlocfilehash: c0fd9a9f5529f202c125d7f1e7c6b50fa9dc630d
ms.sourcegitcommit: e0d9b18d2d4cbeb4a48890f3420a47e6a90abc53
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "49347736"
---
# <a name="graphcalendarbot"></a>GraphCalendarBot

Amostra de bot de eco v4 da estrutura de bot.

Este bot foi criado usando a [estrutura de bot](https://dev.botframework.com), ele mostra como criar um bot simples que aceita entrada do usuário e o ecoa de volta.

## <a name="prerequisites"></a>Pré-requisitos

- [.NET Core SDK](https://dotnet.microsoft.com/download) versão 3,1

  ```bash
  # determine dotnet version
  dotnet --version
  ```

## <a name="to-try-this-sample"></a>Para testar este exemplo

- Em um terminal, navegue até `GraphCalendarBot`

    ```bash
    # change into project folder
    cd GraphCalendarBot
    ```

- Execute o bot a partir de um terminal ou do Visual Studio, escolha A opção A ou B.

  A) de um terminal

  ```bash
  # run the bot
  dotnet run
  ```

  B) ou do Visual Studio

  - Iniciar o Visual Studio
  - Arquivo > Open-> Project/Solution
  - Navegar até a `GraphCalendarBot` pasta
  - Selecionar `GraphCalendarBot.csproj` arquivo
  - Pressione `F5` para executar o projeto

## <a name="testing-the-bot-using-bot-framework-emulator"></a>Testando o bot usando o emulador da estrutura de bot

O [emulador de estrutura de bot](https://github.com/microsoft/botframework-emulator) é um aplicativo de área de trabalho que permite aos desenvolvedores de bot testar e depurar seus bots no localhost ou executar remotamente por meio de um túnel.

- Instale o emulador de estrutura de bot versão 4.9.0 ou superior [a partir daqui](https://github.com/Microsoft/BotFramework-Emulator/releases)

### <a name="connect-to-the-bot-using-bot-framework-emulator"></a>Conectar-se ao bot usando o emulador da estrutura de bot

- Iniciar emulador de estrutura de bot
- > bot de arquivo aberto
- Insira uma URL de bot de `http://localhost:3978/api/messages`

## <a name="deploy-the-bot-to-azure"></a>Implantar o bot no Azure

Para saber mais sobre como implantar um bot no Azure, confira [implantar o bot no Azure](https://aka.ms/azuredeployment) para obter uma lista completa de instruções de implantação.

## <a name="further-reading"></a>Leitura adicional

- [Documentação da estrutura do bot](https://docs.botframework.com)
- [Noções básicas de bot](https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0)
- [Processamento de atividades](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-concept-activity-processing?view=azure-bot-service-4.0)
- [Introdução ao serviço do Azure bot](https://docs.microsoft.com/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0)
- [Documentação do serviço do Azure bot](https://docs.microsoft.com/azure/bot-service/?view=azure-bot-service-4.0)
- [Ferramentas da CLI do .NET Core](https://docs.microsoft.com/en-us/dotnet/core/tools/?tabs=netcore2x)
- [CLI do Azure](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
- [Portal do Azure](https://portal.azure.com)
- [Compreensão do idioma usando LUIS](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/)
- [Serviço de conector de bot e canais](https://docs.microsoft.com/en-us/azure/bot-service/bot-concepts?view=azure-bot-service-4.0)

Gerado usando `dotnet new echobot` v 4.10.2
