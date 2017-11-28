---
title: "aaaAdd SSL 인증서 tooyour Azure 앱 서비스 앱 | Microsoft Docs"
description: "어떻게 tooadd SSL 인증서 tooyour 앱 서비스 앱에 알아봅니다."
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
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="d1ec5-103">Azure 앱 서비스에 대한 SSL 인증서 구입 및 구성</span><span class="sxs-lookup"><span data-stu-id="d1ec5-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="d1ec5-104">이 자습서에서는 **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**에 대한 SSL 인증서를 구매하여 [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)에 안전하게 저장하고 사용자 지정 도메인과 연결하여 Web App의 보안을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-tooazure"></a><span data-ttu-id="d1ec5-105">1 단계-tooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="d1ec5-105">Step 1 - Log in tooAzure</span></span>

<span data-ttu-id="d1ec5-106">Toohello http://portal.azure.com에서 Azure 포털 로그인</span><span class="sxs-lookup"><span data-stu-id="d1ec5-106">Log in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="d1ec5-107">2단계 - SSL 인증서 주문하기</span><span class="sxs-lookup"><span data-stu-id="d1ec5-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="d1ec5-108">새 SSL 인증서 주문을 입력 하기 [앱 서비스 인증서](https://portal.azure.com/#create/Microsoft.SSL) hello에 **Azure 포털**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In hello **Azure portal**.</span></span>

![인증서 만들기](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="d1ec5-110">친숙 한 입력 **이름** 및 SSL 인증서 및 hello 입력 **도메인 이름**</span><span class="sxs-lookup"><span data-stu-id="d1ec5-110">Enter a friendly **Name** for your SSL certificate and enter hello **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="d1ec5-111">Hello hello 구매 프로세스의 가장 중요 한 부분 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-111">This is one of hello most critical parts of hello purchase process.</span></span> <span data-ttu-id="d1ec5-112">호스트 이름 (사용자 지정 도메인)이이 인증서와 함께 tooprotect 원하는 해결 되었는지 tooenter를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-112">Make sure tooenter correct host name (custom domain) that you want tooprotect with this certificate.</span></span> <span data-ttu-id="d1ec5-113">**없는** WWW와 hello 호스트 이름을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-113">**DO NOT** append hello Host name with WWW.</span></span> 
>

<span data-ttu-id="d1ec5-114">**구독**, **리소스 그룹** 및 **인증서 SKU**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="d1ec5-115">앱 서비스 인증서 hello 내에서 다른 앱 서비스에서 사용할 수 있습니다만 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-115">App Service Certificates can only be used by other App Services within hello same subscription.</span></span>  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a><span data-ttu-id="d1ec5-116">3 단계-Azure 키 자격 증명 모음에 hello 인증서 저장</span><span class="sxs-lookup"><span data-stu-id="d1ec5-116">Step 3 - Store hello certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="d1ec5-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)는 클라우드 응용 프로그램 및 서비스에서 사용되는 암호화 키 및 비밀을 보호하는데 도움이 되는 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="d1ec5-118">Tooopen 필요한 SSL 인증서 구매 hello 완료 되 면 [앱 서비스 인증서](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) 리소스 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-118">Once hello SSL Certificate purchase is complete, you need tooopen [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![KV에 준비 toostore의 이미지를 삽입 합니다.](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="d1ec5-120">인증서 상태 임을 알게 될 **"보류 중인 발급"** 몇 가지 단계가 더 많으면 있어야만 toocomplete이이 인증서를 사용 하 여 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need toocomplete before you can start using this certificate.</span></span>

<span data-ttu-id="d1ec5-121">클릭 **인증서 구성** 내부를 클릭 하 고 인증서 속성 블레이드 **1 단계: 저장소** toostore Azure 키 자격 증명 모음에이 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** toostore this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="d1ec5-122">**키 자격 증명 모음의 상태** 블레이드에서 클릭 **키 자격 증명 모음 저장소** toochoose는 기존 키 자격 증명 모음 toostore이이 인증서 **또는 새 키 자격 증명 모음 만들기** toocreate 새 키 자격 증명 모음 동일한 구독 및 리소스 그룹의 내부 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-122">From **Key Vault Status** Blade, click **Key Vault Repository** toochoose an existing Key Vault toostore this certificate **OR Create New Key Vault** toocreate new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="d1ec5-123">Azure Key Vault의 경우 이 인증서를 저장하는 데 약간의 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="d1ec5-124">자세한 내용은 **[Azure Key Vault 가격 책정 정보](https://azure.microsoft.com/pricing/details/key-vault/)**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="d1ec5-125">키 자격 증명 모음 저장소 toostore hello에이 인증서 선택 하면 hello **저장소** 옵션 성공을 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-125">Once you have selected hello Key Vault Repository toostore this certificate in, hello **Store** option should show success.</span></span>

![KV의 저장 성공 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a><span data-ttu-id="d1ec5-127">4 단계-hello 도메인 소유권 확인</span><span class="sxs-lookup"><span data-stu-id="d1ec5-127">Step 4 - Verify hello Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="d1ec5-128">App Service Certificate에서는 도메인 확인 방법으로 도메인 확인, 메일 확인 및 수동 확인을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="d1ec5-129">Hello에 자세히 설명 되어 이러한 [고급 절](#advanced)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-129">These are explained in more details in hello [Advanced section](#advanced).</span></span>

<span data-ttu-id="d1ec5-130">동일한 hello **인증서 구성** 3 단계에서에서 사용 되는 블레이드, 클릭 **2 단계: 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-130">From hello same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="d1ec5-131">**도메인 확인** hello 가장 편리 하 게 프로세스 **경우에만** 있는  **[Azure 앱 서비스에서 사용자 지정 도메인을 구입 합니다.](custom-dns-web-site-buydomains-web-app.md)**</span><span class="sxs-lookup"><span data-stu-id="d1ec5-131">**Domain Verification** This is hello most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="d1ec5-132">클릭 **확인** toocomplete이이 단계를 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-132">Click on **Verify** button toocomplete this step.</span></span>

![도메인 확인 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="d1ec5-134">클릭 한 후 **확인**, hello를 사용 하 여 **새로 고침** hello 때까지 단추 **확인** 옵션 성공을 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-134">After clicking **Verify**, use hello **Refresh** button until hello **Verify** option should show success.</span></span>

![KV의 확인 성공 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a><span data-ttu-id="d1ec5-136">5 단계-인증서 tooApp 서비스 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="d1ec5-136">Step 5 - Assign Certificate tooApp Service App</span></span>

> [!NOTE]
> <span data-ttu-id="d1ec5-137">이 섹션의 hello 단계를 수행 하기 전에 먼저 연결 해야 사용자 지정 도메인 이름을 앱을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-137">Before performing hello steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="d1ec5-138">자세한 내용은 **[웹앱에 대한 사용자 지정 도메인 이름 구성](app-service-web-tutorial-custom-domain.md)**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="d1ec5-139">Hello에  **[Azure 포털](https://portal.azure.com/)**, hello 클릭 **앱 서비스** hello 창의 hello 왼쪽의 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-139">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="d1ec5-140">Hello 이름을 클릭 앱 toowhich의 원하는 tooassign이이 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-140">Click hello name of your app toowhich you want tooassign this certificate.</span></span>

<span data-ttu-id="d1ec5-141">Hello에 **설정**, 클릭 **SSL 인증서**합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-141">In hello **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="d1ec5-142">클릭 **앱 서비스 인증서 가져오기** 및 선택 hello 구입한 인증서를 방금 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-142">Click **Import App Service Certificate** and select hello certificate that you just purchased.</span></span>

![인증서 가져오기 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="d1ec5-144">Hello에 **ssl 바인딩을** 섹션에서 클릭 **바인딩을 추가할**, 인증서 toouse hello 및 hello 드롭다운 tooselect 도메인 이름 toosecure hello를 사용 하 여 SSL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-144">In hello **ssl bindings** section Click on **Add bindings**, and use hello dropdowns tooselect hello domain name toosecure with SSL, and hello certificate toouse.</span></span> <span data-ttu-id="d1ec5-145">선택할 수 있습니다 여부 toouse  **[SNI 서버 이름 표시 ()](http://en.wikipedia.org/wiki/Server_Name_Indication)**  IP 기반 SSL 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-145">You may also select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![SSL 바인딩 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="d1ec5-147">클릭 **바인딩 추가** toosave hello 변경 하 고 SSL을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-147">Click **Add Binding** toosave hello changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="d1ec5-148">선택한 경우 **IP 기반 SSL** 및 사용자 지정 도메인이 A 레코드를 사용 하 여 구성 된 추가 단계를 수행 하는 hello를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps.</span></span> <span data-ttu-id="d1ec5-149">Hello에 자세히 설명 되어 이러한 [고급 절](#Advanced)합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-149">These are explained in more details in hello [Advanced section](#Advanced).</span></span>

<span data-ttu-id="d1ec5-150">이 시점에서 있습니다 있어야 수 toovisit 사용 하 여 앱 `HTTPS://` 대신 `HTTP://` 인증서 hello tooverify가 올바르게 구성 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-150">At this point, you should be able toovisit your app using `HTTPS://` instead of `HTTP://` tooverify that hello certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="d1ec5-151">6단계 - 관리 작업</span><span class="sxs-lookup"><span data-stu-id="d1ec5-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="d1ec5-152">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d1ec5-152">Azure CLI</span></span>

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a><span data-ttu-id="d1ec5-153">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1ec5-153">PowerShell</span></span>

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a><span data-ttu-id="d1ec5-154">고급</span><span class="sxs-lookup"><span data-stu-id="d1ec5-154">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="d1ec5-155">도메인 소유권 확인</span><span class="sxs-lookup"><span data-stu-id="d1ec5-155">Verifying Domain Ownership</span></span>

<span data-ttu-id="d1ec5-156">App Service Certificate에서는 도메인 확인 방법으로 메일 확인 및 수동 확인도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-156">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="d1ec5-157">메일 확인</span><span class="sxs-lookup"><span data-stu-id="d1ec5-157">Mail Verification</span></span>

<span data-ttu-id="d1ec5-158">확인 전자 메일에 이미이 사용자 지정 도메인과 관련 된 전자 메일 주소 toohello를 전송 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-158">Verification email has already been sent toohello Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="d1ec5-159">toocomplete hello 전자 메일 확인 단계 hello 전자 메일을 열고 hello 확인 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-159">toocomplete hello Email verification step, open hello email and click hello verification link.</span></span>

![메일 확인 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="d1ec5-161">Tooresend hello 확인 전자 메일을 해야 하는 경우 클릭 hello **전자 메일 다시 보내기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-161">If you need tooresend hello verification email, click hello **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="d1ec5-162">수동 확인</span><span class="sxs-lookup"><span data-stu-id="d1ec5-162">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1ec5-163">HTML 웹 페이지 확인(표준 인증서 SKU로만 작동)</span><span class="sxs-lookup"><span data-stu-id="d1ec5-163">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="d1ec5-164">**"starfield.html"**이라는 HTML 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="d1ec5-164">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="d1ec5-165">콘텐츠이 파일의 이름 이어야 합니다 hello 정확한 hello 도메인 확인 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-165">Content of this file should be hello exact name of hello Domain Verification Token.</span></span> <span data-ttu-id="d1ec5-166">(도메인 확인 상태 블레이드 hello에서 hello 토큰 복사할 수)</span><span class="sxs-lookup"><span data-stu-id="d1ec5-166">(You can copy hello token from hello Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="d1ec5-167">도메인 호스팅 hello 웹 서버의 hello 루트에이 파일을 업로드`/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="d1ec5-167">Upload this file at hello root of hello web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="d1ec5-168">클릭 **새로 고침** tooupdate hello 인증서 상태 후 확인이 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-168">Click **Refresh** tooupdate hello certificate status after verification is completed.</span></span> <span data-ttu-id="d1ec5-169">확인 toocomplete 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-169">It might take few minutes for verification toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="d1ec5-170">사용 하 여 터미널 확인 `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello 응답 hello 있어야 `<verification-token>`합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-170">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello response should contain hello `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="d1ec5-171">DNS TXT 레코드 확인</span><span class="sxs-lookup"><span data-stu-id="d1ec5-171">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="d1ec5-172">Hello에 TXT 레코드를 만드는 DNS 관리자를 사용 하 여 `@` 하위 도메인 값 같은 toohello 도메인 확인 토큰을 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-172">Using your DNS manager, Create a TXT record on hello `@` subdomain with value equal toohello Domain Verification Token.</span></span>
1. <span data-ttu-id="d1ec5-173">클릭 **"새로 고침"** tooupdate hello 인증서 상태 후 확인이 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-173">Click **“Refresh”** tooupdate hello Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="d1ec5-174">TXT 레코드 toocreate가 필요한 `@.<domain>` 값을 가진 `<verification-token>`합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-174">You need toocreate a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-tooapp-service-app"></a><span data-ttu-id="d1ec5-175">인증서 tooApp 서비스 응용 프로그램 할당</span><span class="sxs-lookup"><span data-stu-id="d1ec5-175">Assign Certificate tooApp Service App</span></span>

<span data-ttu-id="d1ec5-176">선택한 경우 **IP 기반 SSL** 및 사용자 지정 도메인이 A 레코드를 사용 하 여 구성 된 추가 단계를 수행 하는 hello를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-176">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps:</span></span>

<span data-ttu-id="d1ec5-177">구성 하 고 나면 IP 기반 SSL 바인딩에, tooyour 앱 전용된 IP 주소를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-177">After you have configured an IP based SSL binding, a dedicated IP address is assigned tooyour app.</span></span> <span data-ttu-id="d1ec5-178">Hello에이 IP 주소를 찾을 수 있습니다 **사용자 지정 도메인** hello 오른쪽 위에서 응용 프로그램의 설정에서 페이지 **Hostnames** 섹션.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-178">You can find this IP address on hello **Custom domain** page under settings of your app, right above hello **Hostnames** section.</span></span> <span data-ttu-id="d1ec5-179">**외부 IP 주소**로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-179">It is listed as **External IP Address**</span></span>

![IP SSL 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="d1ec5-181">이 IP 주소는 hello 가상 IP 주소 사용 보다 이전에 tooconfigure hello A 레코드가 도메인에 대 한 다른 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-181">Note that this IP address is different than hello virtual IP address used previously tooconfigure hello A record for your domain.</span></span> <span data-ttu-id="d1ec5-182">구성 된 경우 toouse SNI 기반 SSL을 이나 없는 toouse SSL을 구성, 주소가 없습니다.이 항목에 대해 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-182">If you are configured toouse SNI based SSL, or are not configured toouse SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="d1ec5-183">도메인 이름 등록 기관에서 제공 하는 hello 도구를 사용 하 여 hello hello 이전 단계에서 사용자 지정 도메인 이름 toopoint toohello IP 주소에 대 한 레코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-183">Using hello tools provided by your domain name registrar, modify hello A record for your custom domain name toopoint toohello IP address from hello previous step.</span></span>

## <a name="rekey-and-sync-hello-certificate"></a><span data-ttu-id="d1ec5-184">키 다시 생성 하 고 hello 인증서를 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-184">Rekey and Sync hello Certificate</span></span>

<span data-ttu-id="d1ec5-185">필요한 경우 tooRekey 인증서를 선택 **키 다시 생성 하 고 동기화** 옵션에서 **인증서 속성** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-185">If you ever need tooRekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="d1ec5-186">클릭 **키 다시 생성** tooinitiate hello 프로세스 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-186">Click **Rekey** Button tooinitiate hello process.</span></span> <span data-ttu-id="d1ec5-187">1-10 분 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-187">This process can take 1-10 minutes toocomplete.</span></span>

![SSL 키 다시 생성 이미지 삽입](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="d1ec5-189">인증서 재입력 hello 인증서 hello 인증 기관에서 발급 한 새 인증서를 롤업 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1ec5-189">Rekeying your certificate rolls hello certificate with a new certificate issued from hello certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1ec5-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d1ec5-190">Next Steps</span></span>

* [<span data-ttu-id="d1ec5-191">Content Delivery Network 추가</span><span class="sxs-lookup"><span data-stu-id="d1ec5-191">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)