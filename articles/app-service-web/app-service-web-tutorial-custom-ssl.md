---
title: "Azure Web Apps에 기존 사용자 지정 SSL 인증서 바인딩 | Microsoft 문서"
description: "Azure App Service의 웹앱, 모바일 앱 백 엔드 또는 API 앱에 사용자 지정 SSL 인증서를 바인딩하는 방법을 알아봅니다."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 15c31ae5451a31dff2df08047ee43e75edacc127
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-to-azure-web-apps"></a><span data-ttu-id="7de11-103">Azure Web Apps에 기존 사용자 지정 SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="7de11-103">Bind an existing custom SSL certificate to Azure Web Apps</span></span>

<span data-ttu-id="7de11-104">Azure Web Apps는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="7de11-105">이 자습서에서는 신뢰할 수 있는 인증 기관에서 구매한 사용자 지정 SSL 인증서를 [Azure Web Apps](app-service-web-overview.md)에 바인딩하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-105">This tutorial shows you how to bind a custom SSL certificate that you purchased from a trusted certificate authority to [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="7de11-106">완료하면 사용자 지정 DNS 도메인의 HTTPS 끝점에서 웹앱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-106">When you're finished, you'll be able to access your web app at the HTTPS endpoint of your custom DNS domain.</span></span>

![사용자 지정 SSL 인증서가 포함된 웹앱](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="7de11-108">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7de11-109">앱의 가격 책정 계층 업그레이드</span><span class="sxs-lookup"><span data-stu-id="7de11-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="7de11-110">App Service에 사용자 지정 SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="7de11-110">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="7de11-111">앱에 대해 HTTPS 적용</span><span class="sxs-lookup"><span data-stu-id="7de11-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="7de11-112">스크립트로 SSL 인증서 바인딩 자동화</span><span class="sxs-lookup"><span data-stu-id="7de11-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="7de11-113">사용자 지정 SSL 인증서가 필요한 경우 Azure Portal에서 직접 SSL 인증서를 구매하고 웹앱에 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-113">If you need to get a custom SSL certificate, you can get one in the Azure portal directly and bind it to your web app.</span></span> <span data-ttu-id="7de11-114">[App Service 인증서 자습서](web-sites-purchase-ssl-web-site.md)를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="7de11-114">Follow the [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7de11-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7de11-115">Prerequisites</span></span>

<span data-ttu-id="7de11-116">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-116">To complete this tutorial:</span></span>

- [<span data-ttu-id="7de11-117">App Service 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="7de11-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="7de11-118">웹앱에 사용자 지정 DNS 이름 매핑</span><span class="sxs-lookup"><span data-stu-id="7de11-118">Map a custom DNS name to your web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="7de11-119">신뢰할 수 있는 인증 기관에서 SSL 인증서 구매</span><span class="sxs-lookup"><span data-stu-id="7de11-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="7de11-120">SSL 인증서에 대한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="7de11-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="7de11-121">App Service에서 인증서를 사용하려면 인증서가 다음 요구 사항을 모두 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-121">To use a certificate in App Service, the certificate must meet all the following requirements:</span></span>

* <span data-ttu-id="7de11-122">신뢰할 수 있는 인증 기관에서 서명됨</span><span class="sxs-lookup"><span data-stu-id="7de11-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="7de11-123">암호로 보호된 PFX 파일로 내보냄</span><span class="sxs-lookup"><span data-stu-id="7de11-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="7de11-124">길이가 2048비트 이상인 개인 키를 포함함</span><span class="sxs-lookup"><span data-stu-id="7de11-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="7de11-125">인증서 체인의 모든 중간 인증서를 포함함</span><span class="sxs-lookup"><span data-stu-id="7de11-125">Contains all intermediate certificates in the certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="7de11-126">**ECC(타원 곡선 암호화) 인증서**는 App Service에서 사용할 수 있지만 이 문서에서는 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="7de11-127">ECC 인증서를 만드는 정확한 단계에서 인증 기관을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="7de11-127">Work with your certificate authority on the exact steps to create ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="7de11-128">웹앱 준비</span><span class="sxs-lookup"><span data-stu-id="7de11-128">Prepare your web app</span></span>

<span data-ttu-id="7de11-129">사용자 지정 SSL 인증서를 웹앱에 바인딩하려면 [App Service 가격](https://azure.microsoft.com/pricing/details/app-service/)이 **기본**, **표준** 또는 **프리미엄** 계층에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-129">To bind a custom SSL certificate to your web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in the **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="7de11-130">이 단계에서는 웹앱이 지원되는 가격 책정 계층에 있음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-130">In this step, you make sure that your web app is in the supported pricing tier.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="7de11-131">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="7de11-131">Log in to Azure</span></span>

<span data-ttu-id="7de11-132">[Azure 포털](https://portal.azure.com)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-132">Open the [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-to-your-web-app"></a><span data-ttu-id="7de11-133">웹앱으로 이동</span><span class="sxs-lookup"><span data-stu-id="7de11-133">Navigate to your web app</span></span>

<span data-ttu-id="7de11-134">왼쪽 메뉴에서 **App Services**를 클릭한 다음 웹앱의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-134">From the left menu, click **App Services**, and then click the name of your web app.</span></span>

![웹앱 선택](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="7de11-136">웹앱의 관리 페이지에 연결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-136">You have landed in the management page of your web app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="7de11-137">가격 책정 계층 확인</span><span class="sxs-lookup"><span data-stu-id="7de11-137">Check the pricing tier</span></span>

<span data-ttu-id="7de11-138">웹앱 페이지의 왼쪽 탐색 영역에서 **설정** 섹션으로 스크롤하고 **강화(App Service 계획)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-138">In the left-hand navigation of your web app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![강화 메뉴](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="7de11-140">웹앱이 **무료** 또는 **공유** 계층에 있지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-140">Check to make sure that your web app is not in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="7de11-141">웹앱의 현재 계층이 진한 파란색 상자로 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![가격 책정 계층 확인](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="7de11-143">사용자 지정 SSL은 **무료** 또는 **공유** 계층에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-143">Custom SSL is not supported in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="7de11-144">강화해야 하는 경우 다음 섹션의 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-144">If you need to scale up, follow the steps in the next section.</span></span> <span data-ttu-id="7de11-145">그렇지 않은 경우 **가격 책정 계층 선택** 페이지를 닫고 [SSL 인증서 업로드 및 바인딩](#upload)으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-145">Otherwise, close the **Choose your pricing tier** page and skip to [Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="7de11-146">App Service 계획 강화</span><span class="sxs-lookup"><span data-stu-id="7de11-146">Scale up your App Service plan</span></span>

<span data-ttu-id="7de11-147">**기본**, **표준** 또는 **프리미엄** 계층 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-147">Select one of the **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="7de11-148">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-148">Click **Select**.</span></span>

![가격 책정 계층 선택](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="7de11-150">다음 알림이 표시되면 강화 작업이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-150">When you see the following notification, the scale operation is complete.</span></span>

![강화 알림](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="7de11-152">SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="7de11-152">Bind your SSL certificate</span></span>

<span data-ttu-id="7de11-153">SSL 인증서를 웹앱에 업로드할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-153">You are ready to upload your SSL certificate to your web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="7de11-154">중간 인증서 병합</span><span class="sxs-lookup"><span data-stu-id="7de11-154">Merge intermediate certificates</span></span>

<span data-ttu-id="7de11-155">인증 기관에서 여러 인증서를 인증서 체인에 제공하면 인증서를 순서대로 병합해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-155">If your certificate authority gives you multiple certificates in the certificate chain, you need to merge the certificates in order.</span></span> 

<span data-ttu-id="7de11-156">이렇게 하려면 받은 각 인증서를 텍스트 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-156">To do this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="7de11-157">_mergedcertificate.crt_라는 병합된 인증서의 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-157">Create a file for the merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="7de11-158">텍스트 편집기에서 각 인증서의 내용을 이 파일에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-158">In a text editor, copy the content of each certificate into this file.</span></span> <span data-ttu-id="7de11-159">인증서의 순서는 다음 템플릿과 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-159">The order of your certificates should look like the following template:</span></span>

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-to-pfx"></a><span data-ttu-id="7de11-160">PFX로 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="7de11-160">Export certificate to PFX</span></span>

<span data-ttu-id="7de11-161">인증서 요청 생성에 사용된 개인 키로 병합된 SSL 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-161">Export your merged SSL certificate with the private key that your certificate request was generated with.</span></span>

<span data-ttu-id="7de11-162">OpenSSL을 사용하여 인증서 요청을 생성한 경우 개인 키 파일을 만든 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="7de11-163">인증서를 PFX로 내보내려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-163">To export your certificate to PFX, run the following command.</span></span> <span data-ttu-id="7de11-164">_&lt;private-key-file>_ 및 _&lt;merged-certificate-file>_ 자리 표시자를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-164">Replace the placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="7de11-165">메시지가 표시되면 내보내기 암호를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-165">When prompted, define an export password.</span></span> <span data-ttu-id="7de11-166">나중에 SSL 인증서를 App Service에 업로드할 때 이 암호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-166">You'll use this password when uploading your SSL certificate to App Service later.</span></span>

<span data-ttu-id="7de11-167">IIS 또는 _Certreq.exe_를 사용하여 인증서 요청을 생성한 경우 인증서를 로컬 컴퓨터에 설치한 다음 [해당 인증서를 PFX로 내보냅니다](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="7de11-167">If you used IIS or _Certreq.exe_ to generate your certificate request, install the certificate to your local machine, and then [export the certificate to PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="7de11-168">SSL 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="7de11-168">Upload your SSL certificate</span></span>

<span data-ttu-id="7de11-169">SSL 인증서를 업로드하려면 웹앱의 왼쪽 탐색 영역에서 **SSL 인증서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-169">To upload your SSL certificate, click **SSL certificates** in the left navigation of your web app.</span></span>

<span data-ttu-id="7de11-170">**인증서 업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="7de11-171">**PFX 인증서 파일**에서 PFX 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="7de11-172">**인증서 암호**에서 PFX 파일을 내보낼 때 만든 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-172">In **Certificate password**, type the password that you created when you exported the PFX file.</span></span>

<span data-ttu-id="7de11-173">**업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-173">Click **Upload**.</span></span>

![인증서 업로드](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="7de11-175">App Service에서 인증서 업로드가 완료되면 **SSL 인증서** 페이지에 업로드된 인증서가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-175">When App Service finishes uploading your certificate, it appears in the **SSL certificates** page.</span></span>

![업로드된 인증서](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="7de11-177">SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="7de11-177">Bind your SSL certificate</span></span>

<span data-ttu-id="7de11-178">**SSL 바인딩** 섹션에서 **바인딩 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-178">In the **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="7de11-179">**SSL 바인딩 추가** 페이지에서 드롭다운을 사용하여 보호할 도메인 이름과 사용할 인증서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-179">In the **Add SSL Binding** page, use the dropdowns to select the domain name to secure, and the certificate to use.</span></span>

> [!NOTE]
> <span data-ttu-id="7de11-180">인증서를 업로드했지만 **Hostname** 드롭다운에서 해당 도메인 이름이 표시되지 않으면 브라우저 페이지를 새로 고쳐 봅니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-180">If you have uploaded your certificate but don't see the domain name(s) in the **Hostname** dropdown, try refreshing the browser page.</span></span>
>
>

<span data-ttu-id="7de11-181">**SSL 유형**에서 **[SNI(서버 이름 표시)](http://en.wikipedia.org/wiki/Server_Name_Indication)** 또는 IP 기반 SSL을 사용할지 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-181">In **SSL Type**, select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="7de11-182">**SNI 기반 SSL** - 여러 개의 SNI 기반 SSL 바인딩을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="7de11-183">이 옵션을 사용하면 여러 SSL 인증서로 같은 IP 주소의 여러 도메인을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-183">This option allows multiple SSL certificates to secure multiple domains on the same IP address.</span></span> <span data-ttu-id="7de11-184">대부분의 최신 브라우저(Internet Explorer, Chrome, Firefox 및 Opera 포함)는 SNI를 지원합니다. [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)(서버 이름 표시)에서 더 포괄적인 브라우저 지원 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="7de11-185">**IP 기반 SSL** - IP 기반 SSL 바인딩 하나만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="7de11-186">이 옵션을 사용하면 전용 공용 IP 주소를 보호하는 데 하나의 SSL 인증서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-186">This option allows only one SSL certificate to secure a dedicated public IP address.</span></span> <span data-ttu-id="7de11-187">여러 도메인을 보호하려면 동일한 SSL 인증서를 사용하여 모두 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-187">To secure multiple domains, you must secure them all using the same SSL certificate.</span></span> <span data-ttu-id="7de11-188">이 옵션은 SSL 바인딩의 일반적인 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-188">This is the traditional option for SSL binding.</span></span>

<span data-ttu-id="7de11-189">**바인딩 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-189">Click **Add Binding**.</span></span>

![SSL 인증서 바인딩](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="7de11-191">App Service에서 인증서 업로드가 완료되면 **SSL 바인딩** 섹션에 업로드된 인증서가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-191">When App Service finishes uploading your certificate, it appears in the **SSL bindings** sections.</span></span>

![웹앱에 바인딩된 인증서](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="7de11-193">IP SSL에 대한 A 레코드 다시 매핑</span><span class="sxs-lookup"><span data-stu-id="7de11-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="7de11-194">웹앱에서 IP 기반 SSL을 사용하지 않을 경우 [사용자 지정 도메인에 대한 HTTPS 테스트](#test)로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-194">If you don't use IP-based SSL in your web app, skip to [Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="7de11-195">기본적으로 웹앱에서는 공유 공용 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="7de11-196">IP 기반 SSL을 사용하여 인증서를 바인딩하면 App Service에서 웹앱에 대한 새로운 전용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="7de11-197">A 레코드를 웹앱에 매핑한 경우 이 새로운 전용 IP 주소로 도메인 레지스트리를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-197">If you have mapped an A record to your web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="7de11-198">웹앱의 **사용자 지정 도메인** 페이지가 새로운 전용 IP 주소로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-198">Your web app's **Custom domain** page is updated with the new, dedicated IP address.</span></span> <span data-ttu-id="7de11-199">[이 IP 주소를 복사](app-service-web-tutorial-custom-domain.md#info)하고 이 새로운 IP 주소에 [A 레코드를 다시 매핑](app-service-web-tutorial-custom-domain.md#map-an-a-record)합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap the A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) to this new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="7de11-200">HTTPS 테스트</span><span class="sxs-lookup"><span data-stu-id="7de11-200">Test HTTPS</span></span>

<span data-ttu-id="7de11-201">이제 HTTPS가 사용자 지정 도메인에 작동하는지 확인하는 작업만 남았습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-201">All that's left to do now is to make sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="7de11-202">다양한 브라우저에서 `https://<your.custom.domain>`으로 이동하여 웹앱을 처리하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-202">In various browsers, browse to `https://<your.custom.domain>` to see that it serves up your web app.</span></span>

![Azure 앱에 대한 포털 탐색](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="7de11-204">웹앱에서 인증서 유효성 검사 오류가 발생한 경우 자체 서명된 인증서를 사용하고 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="7de11-205">그렇지 않으면 인증서를 PFX 파일로 내보낼 때 중간 인증서를 생략했을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-205">If that's not the case, you may have left out intermediate certificates when you export your certificate to the PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="7de11-206">HTTPS 적용</span><span class="sxs-lookup"><span data-stu-id="7de11-206">Enforce HTTPS</span></span>

<span data-ttu-id="7de11-207">App Service에서는 HTTPS를 적용하지 *않으므로* 방문자는 HTTP를 사용하여 웹앱에 계속 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="7de11-208">웹앱에 HTTPS를 적용하려면 웹앱의 _web.config_ 파일에 다시 쓰기 규칙을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-208">To enforce HTTPS for your web app, define a rewrite rule in the _web.config_ file for your web app.</span></span> <span data-ttu-id="7de11-209">웹앱의 언어 프레임워크에 관계없이 App Service에서는 이 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-209">App Service uses this file, regardless of the language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="7de11-210">언어별 요청 리디렉션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="7de11-211">ASP.NET MVC는 _web.config_의 다시 쓰기 규칙 대신 [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-211">ASP.NET MVC can use the [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of the rewrite rule in _web.config_.</span></span>

<span data-ttu-id="7de11-212">.NET 개발자는 이 파일에 친숙해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="7de11-213">이 파일은 솔루션의 루트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-213">It is in the root of your solution.</span></span>

<span data-ttu-id="7de11-214">또는 PHP, Node.js, Python 또는 Java로 개발할 경우 사용자 대신 App Service에서 이 파일을 생성했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="7de11-215">[FTP/S를 사용하여 앱에 Azure App Service에 배포](app-service-deploy-ftp.md)의 지침에 따라 웹앱의 FTP 끝점에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-215">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="7de11-216">이 파일은 _/home/site/wwwroot_에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="7de11-217">이 파일이 없으면 다음 XML을 사용하여 이 폴더에 _web.config_ 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-217">If not, create a _web.config_ file in this folder with the following XML:</span></span>

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

<span data-ttu-id="7de11-218">기존 _web.config_ 파일의 경우 `<rule>` 요소 전체를 _web.config_의 `configuration/system.webServer/rewrite/rules` 요소에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-218">For an existing _web.config_ file, copy the entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="7de11-219">_web.config_에 다른 `<rule>` 요소가 있으면 복사한 `<rule>` 요소를 다른 `<rule>` 요소 앞에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-219">If there are other `<rule>` elements in your _web.config_, place the copied `<rule>` element before the other `<rule>` elements.</span></span>

<span data-ttu-id="7de11-220">이 규칙에서는 사용자가 웹앱에 대해 HTTP 요청을 수행할 때마다 HTTPS 프로토콜에 HTTP 301(영구 리디렉션)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-220">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="7de11-221">예를 들어 `http://contoso.com`에서 `https://contoso.com`으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-221">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

<span data-ttu-id="7de11-222">IIS URL 다시 쓰기 모듈에 대한 자세한 내용은 [URL 다시 쓰기](http://www.iis.net/downloads/microsoft/url-rewrite) (영문) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7de11-222">For more information on the IIS URL Rewrite module, see the [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="7de11-223">Linux의 Web Apps에 HTTPS 적용</span><span class="sxs-lookup"><span data-stu-id="7de11-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="7de11-224">Linux의 App Service에서는 HTTPS를 적용하지 *않으므로* 누구든지 여전히 HTTP를 사용하여 웹앱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="7de11-225">웹앱에 HTTPS를 적용하려면 웹앱의 _.htaccess_ 파일에 다시 쓰기 규칙을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-225">To enforce HTTPS for your web app, define a rewrite rule in the _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="7de11-226">[FTP/S를 사용하여 앱에 Azure App Service에 배포](app-service-deploy-ftp.md)의 지침에 따라 웹앱의 FTP 끝점에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-226">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="7de11-227">_/home/site/wwwroot_에서 다음 코드를 사용하여 _.htaccess_ 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-227">In _/home/site/wwwroot_, create an _.htaccess_ file with the following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="7de11-228">이 규칙에서는 사용자가 웹앱에 대해 HTTP 요청을 수행할 때마다 HTTPS 프로토콜에 HTTP 301(영구 리디렉션)을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-228">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="7de11-229">예를 들어 `http://contoso.com`에서 `https://contoso.com`으로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-229">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="7de11-230">스크립트를 사용하여 자동화</span><span class="sxs-lookup"><span data-stu-id="7de11-230">Automate with scripts</span></span>

<span data-ttu-id="7de11-231">[Azure CLI](/cli/azure/install-azure-cli) 또는 [Azure PowerShell](/powershell/azure/overview)을 통해 스크립트를 사용하여 웹앱에 대한 SSL 바인딩을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-231">You can automate SSL bindings for your web app with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="7de11-232">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7de11-232">Azure CLI</span></span>

<span data-ttu-id="7de11-233">다음 명령은 내보낸 PFX 파일을 업로드하고 지문을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-233">The following command uploads an exported PFX file and gets the thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="7de11-234">다음 명령은 이전 명령의 지문을 사용하여 SNI 기반 SSL 바인딩을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-234">The following command adds an SNI-based SSL binding, using the thumbprint from the previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="7de11-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7de11-235">Azure PowerShell</span></span>

<span data-ttu-id="7de11-236">다음 명령은 내보낸 PFX 파일을 업로드하고 SNI 기반 SSL 바인딩을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-236">The following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="7de11-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7de11-237">Next steps</span></span>

<span data-ttu-id="7de11-238">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7de11-239">앱의 가격 책정 계층 업그레이드</span><span class="sxs-lookup"><span data-stu-id="7de11-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="7de11-240">App Service에 사용자 지정 SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="7de11-240">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="7de11-241">앱에 대해 HTTPS 적용</span><span class="sxs-lookup"><span data-stu-id="7de11-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="7de11-242">스크립트로 SSL 인증서 바인딩 자동화</span><span class="sxs-lookup"><span data-stu-id="7de11-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="7de11-243">다음 자습서로 이동하여 Azure Content Delivery Network를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="7de11-243">Advance to the next tutorial to learn how to use Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7de11-244">Azure App Service에 CDN(Content Delivery Network) 추가</span><span class="sxs-lookup"><span data-stu-id="7de11-244">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
