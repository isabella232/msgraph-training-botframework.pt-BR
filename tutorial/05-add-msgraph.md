---
ms.openlocfilehash: ced0e75c32d26aed43afa61d498f2f0c438bf2d0
ms.sourcegitcommit: e0d9b18d2d4cbeb4a48890f3420a47e6a90abc53
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "49347743"
---
<!-- markdownlint-disable MD002 MD041 -->

Nesta seção, você usará o SDK do Microsoft Graph para obter o usuário conectado.

## <a name="create-a-graph-service"></a>Criar um serviço de gráfico

Comece implementando um serviço que o bot pode usar para obter um **GraphServiceClient** do SDK do Microsoft Graph e, em seguida, disponibilizar esse serviço para o bot por meio da injeção de dependência.

1. Crie um novo diretório na raiz do projeto chamado **Graph**. Crie um novo arquivo no diretório **./Graph** chamado **IGraphClientService.cs** e adicione o código a seguir.

    :::code language="csharp" source="../demo/GraphCalendarBot/Graph/IGraphClientService.cs" id="IGraphClientServiceSnippet":::

1. Crie um novo arquivo no diretório **./Graph** chamado **GraphClientService.cs** e adicione o código a seguir.

    :::code language="csharp" source="../demo/GraphCalendarBot/Graph/GraphClientService.cs" id="GraphClientServiceSnippet":::

1. Abra **./Startup.cs** e adicione o código a seguir ao final da `ConfigureServices` função.

    :::code language="csharp" source="../demo/GraphCalendarBot/Startup.cs" id="AddGraphServiceSnippet":::

1. Abra **./dialogs/MainDialog.cs**. Adicione as seguintes `using` instruções à parte superior do arquivo.

    ```csharp
    using System;
    using System.IO;
    using CalendarBot.Graph;
    using AdaptiveCards;
    using Microsoft.Graph;
    ```

1. Adicione a propriedade a seguir à classe **MainDialog** .

    ```csharp
    private readonly IGraphClientService _graphClientService;
    ```

1. Localize o construtor da classe **MainDialog** e atualize sua assinatura para obter um parâmetro **IGraphServiceClient** .

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/MainDialog.cs" id="ConstructorSignatureSnippet" highlight="4":::

1. Adicione o código a seguir ao construtor.

    ```csharp
    _graphClientService = graphClientService;
    ```

## <a name="get-the-logged-on-user"></a>Obter o usuário conectado

Nesta seção, você usará o Microsoft Graph para obter o nome, o endereço de email e a foto do usuário. Em seguida, você criará um cartão adaptável para mostrar as informações.

1. Crie um novo arquivo na raiz do projeto chamado **CardHelper.cs**. Adicione o código a seguir a esse arquivo.

    ```csharp
    using AdaptiveCards;
    using Microsoft.Graph;
    using System;
    using System.IO;

    namespace CalendarBot
    {
        public class CardHelper
        {
            public static AdaptiveCard GetUserCard(User user, Stream photo)
            {
              // Create an Adaptive Card to display the user
                // See https://adaptivecards.io/designer/ for possibilities
                var userCard = new AdaptiveCard("1.2");

                var columns = new AdaptiveColumnSet();
                userCard.Body.Add(columns);

                var userPhotoColumn = new AdaptiveColumn { Width = AdaptiveColumnWidth.Auto };
                columns.Columns.Add(userPhotoColumn);

                userPhotoColumn.Items.Add(new AdaptiveImage {
                    Style = AdaptiveImageStyle.Person,
                    Size = AdaptiveImageSize.Small,
                    Url = GetDataUriFromPhoto(photo)
                });

                var userInfoColumn = new AdaptiveColumn {Width = AdaptiveColumnWidth.Stretch };
                columns.Columns.Add(userInfoColumn);

                userInfoColumn.Items.Add(new AdaptiveTextBlock {
                    Weight = AdaptiveTextWeight.Bolder,
                    Wrap = true,
                    Text = user.DisplayName
                });

                userInfoColumn.Items.Add(new AdaptiveTextBlock {
                    Spacing = AdaptiveSpacing.None,
                    IsSubtle = true,
                    Wrap = true,
                    Text = user.Mail ?? user.UserPrincipalName
                });

                return userCard;
            }

            private static Uri GetDataUriFromPhoto(Stream photo)
            {
                // Copy to a MemoryStream to get access to bytes
                var photoStream = new MemoryStream();
                photo.CopyTo(photoStream);

                var photoBytes = photoStream.ToArray();

                return new Uri($"data:image/png;base64,{Convert.ToBase64String(photoBytes)}");
            }
        }
    }
    ```

    Este código usa o pacote NuGet do **AdaptiveCard** para criar um cartão adaptável para exibir o usuário.

1. Adicione a função a seguir à classe **MainDialog** .

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/MainDialog.cs" id="DisplayLoggedInUserSnippet":::

    Considere o que esse código faz.

    - Ele usa o **graphClient** para [obter o usuário conectado](https://docs.microsoft.com/graph/api/user-get?view=graph-rest-1.0).
        - Ele usa o `Select` método para limitar quais campos são retornados.
    - Ele usa o **graphClient** para [obter a foto do usuário](https://docs.microsoft.com/graph/api/profilephoto-get?view=graph-rest-1.0), solicitando o tamanho mínimo suportado de pixels de 48x48.
    - Ele usa a classe **CardHelper** para construir um cartão adaptável e envia o cartão como um anexo.

1. Substitua o código dentro do `else if (command.StartsWith("show me"))` bloco em `ProcessStepAsync` com o seguinte.

    :::code language="csharp" source="../demo/GraphCalendarBot/Dialogs/MainDialog.cs" id="ShowMeSnippet" highlight="3":::

1. Salve todas as suas alterações e reinicie o bot.

1. Use o emulador da estrutura de bot para se conectar ao bot e fazer logon. Selecione o botão **Mostrar mim** para exibir o usuário conectado.

    ![Uma captura de tela do cartão adaptável mostrando o usuário](images/user-card.png)
