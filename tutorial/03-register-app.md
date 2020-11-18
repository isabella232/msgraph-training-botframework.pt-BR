---
ms.openlocfilehash: 9a320225c7e7e76506d73909a311fa019b1f74f3
ms.sourcegitcommit: e0d9b18d2d4cbeb4a48890f3420a47e6a90abc53
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2020
ms.locfileid: "49347723"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="06d14-101">Neste exercício, você criará um novo registro de canais de bot e um registro de aplicativo Web do Azure AD usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="06d14-101">In this exercise, you will create a new Bot Channels registration and an Azure AD web application registration using the Azure Portal.</span></span>

## <a name="create-a-bot-channels-registration"></a><span data-ttu-id="06d14-102">Criar um registro de canais de bot</span><span class="sxs-lookup"><span data-stu-id="06d14-102">Create a Bot Channels registration</span></span>

1. <span data-ttu-id="06d14-103">Abra um navegador e navegue até o [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="06d14-103">Open a browser and navigate to the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="06d14-104">Faça logon usando a conta associada à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="06d14-104">Login using the account associated with your Azure subscription.</span></span>

1. <span data-ttu-id="06d14-105">Selecione o menu superior esquerdo e, em seguida, selecione **criar um recurso**.</span><span class="sxs-lookup"><span data-stu-id="06d14-105">Select the upper-left menu, then select **Create a resource**.</span></span>

    ![Uma captura de tela do menu do portal do Azure](images/create-resource.png)

1. <span data-ttu-id="06d14-107">Na **nova** página, procure `Bot Channel` e selecione o **registro de canais de bot**.</span><span class="sxs-lookup"><span data-stu-id="06d14-107">On the **New** page, search for `Bot Channel` and select **Bot Channels Registration**.</span></span>

1. <span data-ttu-id="06d14-108">Na página **registro de canais de bot** , selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="06d14-108">On the **Bot Channels Registration** page, select **Create**.</span></span>

1. <span data-ttu-id="06d14-109">Preencha os campos obrigatórios e deixe **ponto de extremidade de mensagem** em branco.</span><span class="sxs-lookup"><span data-stu-id="06d14-109">Fill in the required fields, and leave **Messaging endpoint** blank.</span></span> <span data-ttu-id="06d14-110">O campo **identificador de bot** deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="06d14-110">The **Bot handle** field must be unique.</span></span> <span data-ttu-id="06d14-111">Certifique-se de revisar as diferentes camadas de preços e selecionar o que faz sentido para o seu cenário.</span><span class="sxs-lookup"><span data-stu-id="06d14-111">Be sure to review the different pricing tiers and select what makes sense for your scenario.</span></span> <span data-ttu-id="06d14-112">Se este é apenas um exercício de aprendizagem, talvez você queira selecionar a opção gratuito.</span><span class="sxs-lookup"><span data-stu-id="06d14-112">If this is just a learning exercise, you may want to select the free option.</span></span>

1. <span data-ttu-id="06d14-113">Selecione a **ID e a senha do aplicativo Microsoft e**, em seguida, selecione **criar novo**.</span><span class="sxs-lookup"><span data-stu-id="06d14-113">Select the **Microsoft App ID and password**, then select **Create New**.</span></span>

1. <span data-ttu-id="06d14-114">Selecione **criar ID de aplicativo no portal de registro de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="06d14-114">Select **Create App ID in the App Registration Portal**.</span></span> <span data-ttu-id="06d14-115">Isso abrirá uma nova janela ou guia na folha de **registros de aplicativos** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="06d14-115">This will open a new window or tab to the **App registrations** blade in the Azure Portal.</span></span>

1. <span data-ttu-id="06d14-116">Na folha **registros de aplicativos** , selecione **novo registro**.</span><span class="sxs-lookup"><span data-stu-id="06d14-116">In the **App registrations** blade, select **New registration**.</span></span>

1. <span data-ttu-id="06d14-117">Defina os valores da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="06d14-117">Set the values as follows.</span></span>

    - <span data-ttu-id="06d14-118">Defina **Nome** para `Graph Calendar Bot`.</span><span class="sxs-lookup"><span data-stu-id="06d14-118">Set **Name** to `Graph Calendar Bot`.</span></span>
    - <span data-ttu-id="06d14-119">Defina **Tipos de conta com suporte** para **Contas em qualquer diretório organizacional e contas pessoais da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="06d14-119">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="06d14-120">Deixe o **URI de Redirecionamento** vazio.</span><span class="sxs-lookup"><span data-stu-id="06d14-120">Leave **Redirect URI** empty.</span></span>

    ![Uma captura de tela da página registrar um aplicativo](./images/aad-register-an-app.png)

1. <span data-ttu-id="06d14-122">Selecione **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="06d14-122">Select **Register**.</span></span> <span data-ttu-id="06d14-123">Na página **bot Calendar do gráfico** , copie o valor da **ID do aplicativo (cliente)** e salve-o, você precisará deles nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="06d14-123">On the **Graph Calendar Bot** page, copy the value of the **Application (client) ID** and save it, you will need it in the following steps.</span></span>

    ![Uma captura de tela da ID do aplicativo do novo registro de aplicativo](./images/aad-application-id.png)

1. <span data-ttu-id="06d14-125">Selecione **Certificados e segredos** sob **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="06d14-125">Select **Certificates & secrets** under **Manage**.</span></span> <span data-ttu-id="06d14-126">Selecione o botão **Novo segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="06d14-126">Select the **New client secret** button.</span></span> <span data-ttu-id="06d14-127">Insira um valor em **Descrição** e selecione uma das opções para **expirar** e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="06d14-127">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

1. <span data-ttu-id="06d14-128">Copie o valor secreto do cliente antes de sair desta página.</span><span class="sxs-lookup"><span data-stu-id="06d14-128">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="06d14-129">Você precisará dela nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="06d14-129">You will need it in the following steps.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="06d14-130">Este segredo do cliente nunca é mostrado novamente, portanto, copie-o agora.</span><span class="sxs-lookup"><span data-stu-id="06d14-130">This client secret is never shown again, so make sure you copy it now.</span></span> <span data-ttu-id="06d14-131">Você precisará inserir esse valor em vários lugares para mantê-lo seguro.</span><span class="sxs-lookup"><span data-stu-id="06d14-131">You will need to enter this value in multiple places so keep it safe.</span></span>

1. <span data-ttu-id="06d14-132">Retorne à janela de registro do canal de bot no navegador e cole a ID do aplicativo no campo **ID do aplicativo da Microsoft** .</span><span class="sxs-lookup"><span data-stu-id="06d14-132">Return to the Bot Channel Registration window in your browser, and paste the application ID into the **Microsoft App ID** field.</span></span> <span data-ttu-id="06d14-133">Cole o segredo do cliente no campo **senha** .</span><span class="sxs-lookup"><span data-stu-id="06d14-133">Paste your client secret into the **Password** field.</span></span> <span data-ttu-id="06d14-134">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="06d14-134">Select **OK**.</span></span>

1. <span data-ttu-id="06d14-135">Na página **registro de canais de bots** , selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="06d14-135">On the **Bots Channels Registration** page, select **Create**.</span></span>

1. <span data-ttu-id="06d14-136">Aguarde até que o registro de canais de bot seja criado.</span><span class="sxs-lookup"><span data-stu-id="06d14-136">Wait for the Bot Channels registration to be created.</span></span> <span data-ttu-id="06d14-137">Depois de criado, retorne à Home Page no portal do Azure e selecione **serviços de bot**.</span><span class="sxs-lookup"><span data-stu-id="06d14-137">Once created, return to the Home page in the Azure Portal, then select **Bot Services**.</span></span> <span data-ttu-id="06d14-138">Selecione seu novo registro de canal de bots para exibir suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="06d14-138">Select your new Bots Channel registration to view its properties.</span></span>

## <a name="create-a-web-app-registration"></a><span data-ttu-id="06d14-139">Criar um registro de aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="06d14-139">Create a web app registration</span></span>

1. <span data-ttu-id="06d14-140">Retorne à seção **registros de aplicativos** do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="06d14-140">Return to the **App registrations** section of the Azure Portal.</span></span>

1. <span data-ttu-id="06d14-141">Selecione **Novo registro**.</span><span class="sxs-lookup"><span data-stu-id="06d14-141">Select **New registration**.</span></span> <span data-ttu-id="06d14-142">Na página **Registrar um aplicativo**, defina os valores da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="06d14-142">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="06d14-143">Defina **Nome** para `Graph Calendar Bot Auth`.</span><span class="sxs-lookup"><span data-stu-id="06d14-143">Set **Name** to `Graph Calendar Bot Auth`.</span></span>
    - <span data-ttu-id="06d14-144">Defina **Tipos de conta com suporte** para **Contas em qualquer diretório organizacional e contas pessoais da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="06d14-144">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="06d14-145">Em **URI de Redirecionamento**, defina o primeiro menu suspenso para `Web` e defina o valor como `https://token.botframework.com/.auth/web/redirect`.</span><span class="sxs-lookup"><span data-stu-id="06d14-145">Under **Redirect URI**, set the first drop-down to `Web` and set the value to `https://token.botframework.com/.auth/web/redirect`.</span></span>

1. <span data-ttu-id="06d14-146">Selecione **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="06d14-146">Select **Register**.</span></span> <span data-ttu-id="06d14-147">Na página **autenticação de bot de calendário do gráfico** , copie o valor da **ID do aplicativo (cliente)** e salve-o, você precisará deles nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="06d14-147">On the **Graph Calendar Bot Auth** page, copy the value of the **Application (client) ID** and save it, you will need it in the following steps.</span></span>

1. <span data-ttu-id="06d14-148">Selecione **Certificados e segredos** sob **Gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="06d14-148">Select **Certificates & secrets** under **Manage**.</span></span> <span data-ttu-id="06d14-149">Selecione o botão **Novo segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="06d14-149">Select the **New client secret** button.</span></span> <span data-ttu-id="06d14-150">Insira um valor em **Descrição** e selecione uma das opções para **expirar** e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="06d14-150">Enter a value in **Description** and select one of the options for **Expires** and select **Add**.</span></span>

1. <span data-ttu-id="06d14-151">Copie o valor secreto do cliente antes de sair desta página.</span><span class="sxs-lookup"><span data-stu-id="06d14-151">Copy the client secret value before you leave this page.</span></span> <span data-ttu-id="06d14-152">Você precisará dela nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="06d14-152">You will need it in the following steps.</span></span>

1. <span data-ttu-id="06d14-153">Selecione **permissões de API** e, em seguida, selecione **Adicionar uma permissão**.</span><span class="sxs-lookup"><span data-stu-id="06d14-153">Select **API permissions**, then select **Add a permission**.</span></span>

1. <span data-ttu-id="06d14-154">Selecione **Microsoft Graph** e, em seguida, selecione **permissões delegadas**.</span><span class="sxs-lookup"><span data-stu-id="06d14-154">Select **Microsoft Graph**, then select **Delegated permissions**.</span></span>

1. <span data-ttu-id="06d14-155">Selecione as permissões a seguir e, em seguida, selecione **adicionar permissões**.</span><span class="sxs-lookup"><span data-stu-id="06d14-155">Select the following permissions, then select **Add permissions**.</span></span>

    - <span data-ttu-id="06d14-156">**openid**</span><span class="sxs-lookup"><span data-stu-id="06d14-156">**openid**</span></span>
    - <span data-ttu-id="06d14-157">**perfil**</span><span class="sxs-lookup"><span data-stu-id="06d14-157">**profile**</span></span>
    - <span data-ttu-id="06d14-158">**Calendars.ReadWrite**</span><span class="sxs-lookup"><span data-stu-id="06d14-158">**Calendars.ReadWrite**</span></span>
    - <span data-ttu-id="06d14-159">**MailboxSettings.Read**</span><span class="sxs-lookup"><span data-stu-id="06d14-159">**MailboxSettings.Read**</span></span>

    ![Captura de tela das permissões configuradas](images/configured-permissions.png)

### <a name="about-permissions"></a><span data-ttu-id="06d14-161">Sobre permissões</span><span class="sxs-lookup"><span data-stu-id="06d14-161">About permissions</span></span>

<span data-ttu-id="06d14-162">Considere o que cada um desses escopos de permissão permite que o bot faça e o que o bot utilizará para eles.</span><span class="sxs-lookup"><span data-stu-id="06d14-162">Consider what each of those permission scopes allows the bot to do, and what the bot will use them for.</span></span>

- <span data-ttu-id="06d14-163">**OpenID** e **Profile**: permite ao bot assinar usuários e obter informações básicas do Azure AD no token de identidade.</span><span class="sxs-lookup"><span data-stu-id="06d14-163">**openid** and **profile**: allows the bot to sign users in and get basic information from Azure AD in the identity token.</span></span>
- <span data-ttu-id="06d14-164">**Calendars. ReadWrite**: permite que o bot Leia o calendário do usuário e adicione novos eventos ao calendário do usuário.</span><span class="sxs-lookup"><span data-stu-id="06d14-164">**Calendars.ReadWrite**: allows the bot to read the user's calendar and to add new events to the user's calendar.</span></span>
- <span data-ttu-id="06d14-165">**MailboxSettings. Read**: permite que o bot Leia as configurações da caixa de correio do usuário.</span><span class="sxs-lookup"><span data-stu-id="06d14-165">**MailboxSettings.Read**: allows the bot to read the user's mailbox settings.</span></span> <span data-ttu-id="06d14-166">O bot usará isso para obter o fuso horário selecionado do usuário.</span><span class="sxs-lookup"><span data-stu-id="06d14-166">The bot will use this to get the user's selected time zone.</span></span>
- <span data-ttu-id="06d14-167">**User. Read**: permite ao bot obter o perfil do usuário do Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="06d14-167">**User.Read**: allows the bot to get the user's profile from Microsoft Graph.</span></span> <span data-ttu-id="06d14-168">O bot usará isso para obter o nome do usuário.</span><span class="sxs-lookup"><span data-stu-id="06d14-168">The bot will use this to get the user's name.</span></span>

## <a name="add-oauth-connection-to-the-bot"></a><span data-ttu-id="06d14-169">Adicionar conexão OAuth ao bot</span><span class="sxs-lookup"><span data-stu-id="06d14-169">Add OAuth connection to the bot</span></span>

1. <span data-ttu-id="06d14-170">Navegue até a página de registro dos canais de bot do bot no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="06d14-170">Navigate to your bot's Bot Channels Registration page on the Azure Portal.</span></span> <span data-ttu-id="06d14-171">Selecione **configurações** em **Gerenciamento de bot**.</span><span class="sxs-lookup"><span data-stu-id="06d14-171">Select **Settings** under **Bot Management**.</span></span>

1. <span data-ttu-id="06d14-172">Em **configurações de conexão OAuth** próximo à parte inferior da página, selecione **Adicionar configuração**.</span><span class="sxs-lookup"><span data-stu-id="06d14-172">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>

1. <span data-ttu-id="06d14-173">Preencha o formulário da seguinte maneira e selecione **salvar**.</span><span class="sxs-lookup"><span data-stu-id="06d14-173">Fill in the form as follows, then select **Save**.</span></span>

    - <span data-ttu-id="06d14-174">**Nome**: `GraphBotAuth`</span><span class="sxs-lookup"><span data-stu-id="06d14-174">**Name**: `GraphBotAuth`</span></span>
    - <span data-ttu-id="06d14-175">**Provedor**: **Azure Active Directory v2**</span><span class="sxs-lookup"><span data-stu-id="06d14-175">**Provider**: **Azure Active Directory v2**</span></span>
    - <span data-ttu-id="06d14-176">**ID do cliente**: a ID do aplicativo do seu registro de **autenticação do bot de calendário do gráfico** .</span><span class="sxs-lookup"><span data-stu-id="06d14-176">**Client id**: The application ID of your **Graph Calendar Bot Auth** registration.</span></span>
    - <span data-ttu-id="06d14-177">**Segredo do cliente**: o segredo do cliente do registro de **autenticação do bot de calendário do gráfico** .</span><span class="sxs-lookup"><span data-stu-id="06d14-177">**Client secret**: The client secret of your **Graph Calendar Bot Auth** registration.</span></span>
    - <span data-ttu-id="06d14-178">**URL do token do Exchange**: deixar em branco</span><span class="sxs-lookup"><span data-stu-id="06d14-178">**Token Exchange URL**: Leave blank</span></span>
    - <span data-ttu-id="06d14-179">**ID do locatário**: `common`</span><span class="sxs-lookup"><span data-stu-id="06d14-179">**Tenant ID**: `common`</span></span>
    - <span data-ttu-id="06d14-180">**Escopos**: `openid profile Calendars.ReadWrite MailboxSettings.Read User.Read`</span><span class="sxs-lookup"><span data-stu-id="06d14-180">**Scopes**: `openid profile Calendars.ReadWrite MailboxSettings.Read User.Read`</span></span>

1. <span data-ttu-id="06d14-181">Selecione a entrada **GraphBotAuth** em **configurações de conexão OAuth**.</span><span class="sxs-lookup"><span data-stu-id="06d14-181">Select the **GraphBotAuth** entry under **OAuth Connection Settings**.</span></span>

1. <span data-ttu-id="06d14-182">Selecione **testar conexão**.</span><span class="sxs-lookup"><span data-stu-id="06d14-182">Select **Test Connection**.</span></span> <span data-ttu-id="06d14-183">Isso abre uma nova janela ou guia do navegador para iniciar o fluxo do OAuth.</span><span class="sxs-lookup"><span data-stu-id="06d14-183">This opens a new browser window or tab to start the OAuth flow.</span></span>

1. <span data-ttu-id="06d14-184">Se necessário, entre.</span><span class="sxs-lookup"><span data-stu-id="06d14-184">If necessary, sign in.</span></span> <span data-ttu-id="06d14-185">Revise a lista de permissões solicitadas e selecione **aceitar**.</span><span class="sxs-lookup"><span data-stu-id="06d14-185">Review the list of requested permissions, then select **Accept**.</span></span>

1. <span data-ttu-id="06d14-186">Você verá uma mensagem de **teste de conexão com êxito em ' GraphBotAuth '** .</span><span class="sxs-lookup"><span data-stu-id="06d14-186">You should see a **Test Connection to 'GraphBotAuth' Succeeded** message.</span></span>

> [!TIP]
> <span data-ttu-id="06d14-187">Você pode selecionar o botão **copiar token** nesta página e colar o token em [https://jwt.ms](https://jwt.ms) para ver as declarações dentro do token.</span><span class="sxs-lookup"><span data-stu-id="06d14-187">You can select the **Copy Token** button on this page, and paste the token into [https://jwt.ms](https://jwt.ms) to see the claims inside the token.</span></span> <span data-ttu-id="06d14-188">Isso é útil na solução de problemas de erros de autenticação.</span><span class="sxs-lookup"><span data-stu-id="06d14-188">This is useful when troubleshooting authentication errors.</span></span>
