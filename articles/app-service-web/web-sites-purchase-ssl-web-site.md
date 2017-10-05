---
title: "Azure App Service 앱에 SSL 인증서 추가 | Microsoft Docs"
description: "Azure App Service 앱에 SSL 인증서를 추가하는 방법을 알아봅니다."
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: 191dd7240ad15b4936a72bc27a2d0162350f3afb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="85e14-103">Azure 앱 서비스에 대한 SSL 인증서 구입 및 구성</span><span class="sxs-lookup"><span data-stu-id="85e14-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="85e14-104">이 자습서에서는 **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**에 대한 SSL 인증서를 구매하여 [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)에 안전하게 저장하고 사용자 지정 도메인과 연결하여 Web App의 보안을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-to-azure"></a><span data-ttu-id="85e14-105">1단계 - Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="85e14-105">Step 1 - Log in to Azure</span></span>

<span data-ttu-id="85e14-106">Azure Portal http://portal.azure.com 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-106">Log in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="85e14-107">2단계 - SSL 인증서 주문하기</span><span class="sxs-lookup"><span data-stu-id="85e14-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="85e14-108">**Azure Portal**에서 새로운 [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL)를 만들어 SSL 인증서를 주문할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In the **Azure portal**.</span></span>

![인증서 만들기](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="85e14-110">SSL 인증서에 친숙한 **이름** 및 **도메인 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-110">Enter a friendly **Name** for your SSL certificate and enter the **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="85e14-111">구매 프로세스의 가장 중요한 부분 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-111">This is one of the most critical parts of the purchase process.</span></span> <span data-ttu-id="85e14-112">이 인증서로 보호하려면 올바른 호스트 이름(사용자 지정 도메인)을 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-112">Make sure to enter correct host name (custom domain) that you want to protect with this certificate.</span></span> <span data-ttu-id="85e14-113">**마세요** .</span><span class="sxs-lookup"><span data-stu-id="85e14-113">**DO NOT** append the Host name with WWW.</span></span> 
>

<span data-ttu-id="85e14-114">**구독**, **리소스 그룹** 및 **인증서 SKU**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="85e14-115">App Service Certificate는 동일한 구독 내의 다른 App Services에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-115">App Service Certificates can only be used by other App Services within the same subscription.</span></span>  
>

## <a name="step-3---store-the-certificate-in-azure-key-vault"></a><span data-ttu-id="85e14-116">3단계 - Azure Key Vault에 인증서 저장</span><span class="sxs-lookup"><span data-stu-id="85e14-116">Step 3 - Store the certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="85e14-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)는 클라우드 응용 프로그램 및 서비스에서 사용되는 암호화 키 및 비밀을 보호하는데 도움이 되는 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="85e14-118">SSL 인증서 구입을 완료했으면 [App Service Certificate](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) 리소스 블레이드를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-118">Once the SSL Certificate purchase is complete, you need to open [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![KV에 저장할 준비 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="85e14-120">이 인증서를 사용하려면 몇 가지 추가 단계를 완료해야 하므로 인증서 상태가 **"발급 보류 중"**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need to complete before you can start using this certificate.</span></span>

<span data-ttu-id="85e14-121">인증서 속성 블레이드 내에서 **인증서 구성**을 클릭하고 **1단계: 저장**을 클릭하여 이 인증서를 Azure Key Vault에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** to store this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="85e14-122">**Key Vault 상태** 블레이드에서 **Key Vault 리포지토리**를 클릭하여 이 인증서를 저장할 기존 Key Vault를 선택하거나 **새 Key Vault 만들기**로 동일한 구독 및 리소스 그룹 내에 새 Key Vault를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-122">From **Key Vault Status** Blade, click **Key Vault Repository** to choose an existing Key Vault to store this certificate **OR Create New Key Vault** to create new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="85e14-123">Azure Key Vault의 경우 이 인증서를 저장하는 데 약간의 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="85e14-124">자세한 내용은 **[Azure Key Vault 가격 책정 정보](https://azure.microsoft.com/pricing/details/key-vault/)**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85e14-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="85e14-125">이 인증서를 저장할 Key Vault 리포지토리를 선택하면 **저장** 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-125">Once you have selected the Key Vault Repository to store this certificate in, the **Store** option should show success.</span></span>

![KV의 저장 성공 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-the-domain-ownership"></a><span data-ttu-id="85e14-127">4단계 - 도메인 소유권 확인</span><span class="sxs-lookup"><span data-stu-id="85e14-127">Step 4 - Verify the Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="85e14-128">App Service Certificate에서는 도메인 확인 방법으로 도메인 확인, 메일 확인 및 수동 확인을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="85e14-129">자세한 내용은 [고급 섹션](#advanced)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85e14-129">These are explained in more details in the [Advanced section](#advanced).</span></span>

<span data-ttu-id="85e14-130">3단계에서 사용한 것과 동일한 **인증서 구성** 블레이드에서 **2단계: 확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-130">From the same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="85e14-131">**도메인 확인** 가장 간편한 프로세스이지만 **[Azure App Service에서 사용자 지정 도메인을 구입](custom-dns-web-site-buydomains-web-app.md)**한 **경우에만** 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-131">**Domain Verification** This is the most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="85e14-132">**확인** 단추를 클릭하고 이 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-132">Click on **Verify** button to complete this step.</span></span>

![도메인 확인 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="85e14-134">**확인**을 클릭한 후 **확인** 옵션이 성공할 때까지 **새로 고침** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-134">After clicking **Verify**, use the **Refresh** button until the **Verify** option should show success.</span></span>

![KV의 확인 성공 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-to-app-service-app"></a><span data-ttu-id="85e14-136">5단계: App Service 앱에 인증서 할당</span><span class="sxs-lookup"><span data-stu-id="85e14-136">Step 5 - Assign Certificate to App Service App</span></span>

> [!NOTE]
> <span data-ttu-id="85e14-137">이 섹션의 단계를 수행하기 전에 사용자 지정 도메인 이름을 앱과 연결한 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-137">Before performing the steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="85e14-138">자세한 내용은 **[웹앱에 대한 사용자 지정 도메인 이름 구성](app-service-web-tutorial-custom-domain.md)**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85e14-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="85e14-139">**[Azure Portal](https://portal.azure.com/)**에서 페이지 왼쪽의 **App Service** 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-139">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="85e14-140">이 인증서를 할당하려는 앱의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-140">Click the name of your app to which you want to assign this certificate.</span></span>

<span data-ttu-id="85e14-141">**설정**에서 **SSL 인증서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-141">In the **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="85e14-142">**App Service Certificate 가져오기**를 클릭하고 방금 구입한 인증서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-142">Click **Import App Service Certificate** and select the certificate that you just purchased.</span></span>

![인증서 가져오기 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="85e14-144">**ssl 바인딩** 섹션에서 **바인딩 추가**를 클릭하고 드롭다운을 사용하여 SSL로 보안을 설정할 도메인 이름과 사용할 인증서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-144">In the **ssl bindings** section Click on **Add bindings**, and use the dropdowns to select the domain name to secure with SSL, and the certificate to use.</span></span> <span data-ttu-id="85e14-145">**[SNI(서버 이름 표시)](http://en.wikipedia.org/wiki/Server_Name_Indication)**를 사용할지 또는 IP 기반 SSL을 사용할지 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-145">You may also select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![SSL 바인딩 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="85e14-147">**바인딩 추가** 를 클릭하여 변경 내용을 저장하고 SSL을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-147">Click **Add Binding** to save the changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="85e14-148">**IP 기반 SSL**을 선택했으며 사용자 지정 도메인이 A 레코드를 사용하여 구성된 경우 다음과 같은 추가 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps.</span></span> <span data-ttu-id="85e14-149">자세한 내용은 [고급 섹션](#Advanced)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85e14-149">These are explained in more details in the [Advanced section](#Advanced).</span></span>

<span data-ttu-id="85e14-150">이 시점에서 `HTTP://` 대신 `HTTPS://`를 사용하여 앱에 방문하여 인증서가 올바르게 구성되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-150">At this point, you should be able to visit your app using `HTTPS://` instead of `HTTP://` to verify that the certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="85e14-151">6단계 - 관리 작업</span><span class="sxs-lookup"><span data-stu-id="85e14-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="85e14-152">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="85e14-152">Azure CLI</span></span>

<span data-ttu-id="85e14-153">[!code-azurecli[기본](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "웹앱에 사용자 지정 SSL 인증서 바인딩")]</span><span class="sxs-lookup"><span data-stu-id="85e14-153">[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span> 

### <a name="powershell"></a><span data-ttu-id="85e14-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="85e14-154">PowerShell</span></span>

<span data-ttu-id="85e14-155">[!code-powershell[기본](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "웹앱에 사용자 지정 SSL 인증서 바인딩")]</span><span class="sxs-lookup"><span data-stu-id="85e14-155">[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]</span></span>

## <a name="advanced"></a><span data-ttu-id="85e14-156">고급</span><span class="sxs-lookup"><span data-stu-id="85e14-156">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="85e14-157">도메인 소유권 확인</span><span class="sxs-lookup"><span data-stu-id="85e14-157">Verifying Domain Ownership</span></span>

<span data-ttu-id="85e14-158">App Service Certificate에서는 도메인 확인 방법으로 메일 확인 및 수동 확인도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-158">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="85e14-159">메일 확인</span><span class="sxs-lookup"><span data-stu-id="85e14-159">Mail Verification</span></span>

<span data-ttu-id="85e14-160">확인 전자 메일이 이 사용자 지정 도메인과 연결된 전자 메일 주소로 이미 전송되었습니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-160">Verification email has already been sent to the Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="85e14-161">메일 확인 단계를 완료하려면 메일을 열고 확인 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-161">To complete the Email verification step, open the email and click the verification link.</span></span>

![메일 확인 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="85e14-163">확인 전자 메일을 다시 전송해야 하는 경우 **전자 메일 다시 보내기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-163">If you need to resend the verification email, click the **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="85e14-164">수동 확인</span><span class="sxs-lookup"><span data-stu-id="85e14-164">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85e14-165">HTML 웹 페이지 확인(표준 인증서 SKU로만 작동)</span><span class="sxs-lookup"><span data-stu-id="85e14-165">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="85e14-166">**"starfield.html"**이라는 HTML 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="85e14-166">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="85e14-167">이 파일의 내용은 도메인 확인 토큰의 이름과 정확히 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-167">Content of this file should be the exact name of the Domain Verification Token.</span></span> <span data-ttu-id="85e14-168">(토큰은 도메인 확인 상태 블레이드에서 복사할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="85e14-168">(You can copy the token from the Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="85e14-169">이 파일을 도메인을 호스팅하는 웹 서버의 루트에서 업로드합니다. `/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="85e14-169">Upload this file at the root of the web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="85e14-170">확인이 끝났으면 **새로 고침**을 클릭하여 인증서 상태를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-170">Click **Refresh** to update the certificate status after verification is completed.</span></span> <span data-ttu-id="85e14-171">확인을 완료하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-171">It might take few minutes for verification to complete.</span></span>

> [!TIP]
> <span data-ttu-id="85e14-172">`curl -G http://<domain>/.well-known/pki-validation/starfield.html`을 사용하는 터미널에서 응답에 `<verification-token>`이 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-172">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` the response should contain the `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="85e14-173">DNS TXT 레코드 확인</span><span class="sxs-lookup"><span data-stu-id="85e14-173">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="85e14-174">DNS 관리자를 사용하여 `@` 하위 도메인에 값이 도메인 확인 토큰과 같은 TXT 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-174">Using your DNS manager, Create a TXT record on the `@` subdomain with value equal to the Domain Verification Token.</span></span>
1. <span data-ttu-id="85e14-175">확인이 끝났으면 **“새로 고침”**을 클릭하여 인증서 상태를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-175">Click **“Refresh”** to update the Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="85e14-176">`@.<domain>`에서 `<verification-token>` 값을 가진 TXT 레코드를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-176">You need to create a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-to-app-service-app"></a><span data-ttu-id="85e14-177">App Service 앱에 인증서 할당</span><span class="sxs-lookup"><span data-stu-id="85e14-177">Assign Certificate to App Service App</span></span>

<span data-ttu-id="85e14-178">**IP 기반 SSL** 을 선택했으며 사용자 지정 도메인이 A 레코드를 사용하여 구성된 경우 다음과 같은 추가 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-178">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps:</span></span>

<span data-ttu-id="85e14-179">IP 기반 SSL 바인딩을 구성하면 앱에 전용 IP 주소가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-179">After you have configured an IP based SSL binding, a dedicated IP address is assigned to your app.</span></span> <span data-ttu-id="85e14-180">**호스트 이름** 섹션.바로 위에 있는 앱 설정 아래 **사용자 지정 도메인** 페이지에서 이 IP 주소를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-180">You can find this IP address on the **Custom domain** page under settings of your app, right above the **Hostnames** section.</span></span> <span data-ttu-id="85e14-181">**외부 IP 주소**로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-181">It is listed as **External IP Address**</span></span>

![IP SSL 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="85e14-183">이 IP 주소는 이전에 도메인에 대한 A 레코드를 구성하는 데 사용된 가상 IP 주소와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-183">Note that this IP address is different than the virtual IP address used previously to configure the A record for your domain.</span></span> <span data-ttu-id="85e14-184">SNI 기반 SSL을 사용하도록 구성되었거나 SSL을 사용하도록 구성되지 않은 경우에는 이 항목에 대한 주소가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-184">If you are configured to use SNI based SSL, or are not configured to use SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="85e14-185">도메인 이름 등록 기관에서 제공한 도구를 사용하여 이전 단계의 IP 주소를 가리키도록 사용자 지정 도메인 이름에 대한 A 레코드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-185">Using the tools provided by your domain name registrar, modify the A record for your custom domain name to point to the IP address from the previous step.</span></span>

## <a name="rekey-and-sync-the-certificate"></a><span data-ttu-id="85e14-186">인증서 키 다시 생성 및 동기화</span><span class="sxs-lookup"><span data-stu-id="85e14-186">Rekey and Sync the Certificate</span></span>

<span data-ttu-id="85e14-187">인증서의 키를 다시 생성하려면 **인증서 속성** 블레이드에서 **키 다시 생성 및 동기화** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-187">If you ever need to Rekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="85e14-188">프로세스를 시작하려면 **키 다시 생성** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-188">Click **Rekey** Button to initiate the process.</span></span> <span data-ttu-id="85e14-189">이 프로세스는 완료하는 데 1-10분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-189">This process can take 1-10 minutes to complete.</span></span>

![SSL 키 다시 생성 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="85e14-191">인증서 키를 다시 생성하면 인증서가 인증 기관에서 발급한 새 인증서로 롤링됩니다.</span><span class="sxs-lookup"><span data-stu-id="85e14-191">Rekeying your certificate rolls the certificate with a new certificate issued from the certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85e14-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="85e14-192">Next Steps</span></span>

* [<span data-ttu-id="85e14-193">Content Delivery Network 추가</span><span class="sxs-lookup"><span data-stu-id="85e14-193">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)