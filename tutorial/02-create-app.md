---
ms.openlocfilehash: 12a6c18b52e2bc9aba5ad69c8bb9ab8091c11a64
ms.sourcegitcommit: e0d9b18d2d4cbeb4a48890f3420a47e6a90abc53
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "49347733"
---
<!-- markdownlint-disable MD002 MD041 -->

Nesta seção, você criará um projeto de estrutura de bot.

1. Abra a interface de linha de comando (CLI) em um diretório onde você deseja criar o projeto. Execute o seguinte comando para criar um novo projeto usando o modelo **Microsoft. bot. Framework. CSharp. EchoBot** .

    ```dotnetcli
    dotnet new echobot -n GraphCalendarBot
    ```

    > [!NOTE]
    > Se você receber um `No templates matched the input template name: echobot.` erro, instale o modelo com o comando a seguir e execute novamente o comando anterior.
    >
    > ```dotnetcli
    > dotnet new -i Microsoft.Bot.Framework.CSharp.EchoBot
    > ```

1. Renomeie a classe **EchoBot** padrão como **CalendarBot**. Abra **./bots/EchoBot.cs** e substitua todas as instâncias do `EchoBot` com `CalendarBot` . Renomeie o arquivo para **CalendarBot.cs**.

1. Substitua todas as instâncias de `EchoBot` com `CalendarBot` nos arquivos **. cs** restantes.

1. Na sua CLI, altere o diretório atual para o diretório **GraphCalendarBot** e execute o comando a seguir para confirmar se o projeto é criado.

    ```dotnetcli
    dotnet build
    ```

## <a name="add-nuget-packages"></a>Adicionar pacotes NuGet

Antes de prosseguir, instale alguns pacotes NuGet adicionais que serão usados posteriormente.

- [AdaptiveCards](https://www.nuget.org/packages/AdaptiveCards/) para permitir que o bot envie cartões adaptáveis em respostas.
- [Microsoft. bot. Builder. dialogs](https://www.nuget.org/packages/Microsoft.Bot.Builder.Dialogs/) para adicionar o suporte de caixa de diálogo ao bot.
- [Microsoft. Recognizers. Text. datatypes. Timex](https://www.nuget.org/packages/Microsoft.Recognizers.Text.DataTypes.TimexExpression/) para converter as expressões de Timex retornadas de prompts de bot em objetos **DateTime** .
- [Microsoft. Graph](https://www.nuget.org/packages/Microsoft.Graph/) para fazer chamadas para o Microsoft Graph.

1. Execute os seguintes comandos em sua CLI para instalar as dependências.

    ```Shell
    dotnet add package AdaptiveCards --version 2.2.0
    dotnet add package Microsoft.Bot.Builder.Dialogs --version 4.10.3
    dotnet add package Microsoft.Bot.Builder.Integration.AspNet.Core --version 4.10.3
    dotnet add package Microsoft.Recognizers.Text.DataTypes.TimexExpression --version 1.4.1
    dotnet add package Microsoft.Graph --version 3.18.0
    ```

## <a name="test-the-bot"></a>Testar o bot

Antes de adicionar qualquer código, teste o bot para verificar se ele funciona corretamente e se o emulador da estrutura de bot está configurado para testá-lo.

1. Inicie o bot executando o seguinte comando.

    ```dotnetcli
    dotnet run
    ```

    > [!TIP]
    > Embora você possa usar qualquer editor de texto para editar os arquivos de origem no projeto, é recomendável usar o [Visual Studio Code](https://code.visualstudio.com/). O Visual Studio Code oferece suporte à depuração, IntelliSense e muito mais. Se estiver usando o Visual Studio Code, você pode iniciar o bot usando o menu **executar**  ->  **inicialização de depuração** .

1. Confirme se o bot está sendo executado abrindo seu navegador e acessando `http://localhost:3978` . Você verá um **bot pronto!** Mensagem.

1. Abra o emulador da estrutura do bot. Escolha o menu **arquivo** e, em seguida, **abra bot**.

1. Insira `http://localhost:3978/api/messages` na **URL do bot** e, em seguida, selecione **conectar**.

1. O bot responde com `Hello and welcome!` na janela de bate-papo. Envie uma mensagem para o bot e confirme que ela a ecoa de volta.

    ![Uma captura de tela do emulador de estrutura de bot conectado ao bot](images/test-emulator.png)
