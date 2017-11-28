---
title: "aaaBind 기존 사용자 지정 SSL 인증서 tooAzure 웹 응용 프로그램 | Microsoft Docs"
description: "사용자 지정 SSL 인증서 tooyour 웹 앱, 모바일 앱 백 엔드, 또는 Azure 앱 서비스에서 API 앱 tootoobind에 알아봅니다."
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
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a><span data-ttu-id="9ddc6-103">기존 사용자 지정 SSL 인증서 tooAzure 웹 응용 프로그램 바인딩</span><span class="sxs-lookup"><span data-stu-id="9ddc6-103">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>

<span data-ttu-id="9ddc6-104">Azure Web Apps는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="9ddc6-105">이 자습서에서는 어떻게 toobind 사용자 지정 SSL 인증서 너무 신뢰할 수 있는 인증 기관에서 구입한[Azure 웹 앱](app-service-web-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-105">This tutorial shows you how toobind a custom SSL certificate that you purchased from a trusted certificate authority too[Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="9ddc6-106">완료 되 면 수 수 tooaccess 웹 앱에서 사용자 지정 DNS 도메인의 hello HTTPS 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-106">When you're finished, you'll be able tooaccess your web app at hello HTTPS endpoint of your custom DNS domain.</span></span>

![사용자 지정 SSL 인증서가 포함된 웹앱](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="9ddc6-108">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9ddc6-109">앱의 가격 책정 계층 업그레이드</span><span class="sxs-lookup"><span data-stu-id="9ddc6-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="9ddc6-110">사용자 지정 SSL 인증서 tooApp 서비스 바인딩</span><span class="sxs-lookup"><span data-stu-id="9ddc6-110">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="9ddc6-111">앱에 대해 HTTPS 적용</span><span class="sxs-lookup"><span data-stu-id="9ddc6-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="9ddc6-112">스크립트로 SSL 인증서 바인딩 자동화</span><span class="sxs-lookup"><span data-stu-id="9ddc6-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="9ddc6-113">Tooget 사용자 지정 SSL 인증서가 필요한 경우 hello Azure 포털에서에서 직접 얻을 수 있으며 tooyour 웹 응용 프로그램을 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-113">If you need tooget a custom SSL certificate, you can get one in hello Azure portal directly and bind it tooyour web app.</span></span> <span data-ttu-id="9ddc6-114">Hello에 따라 [앱 서비스 인증서 자습서](web-sites-purchase-ssl-web-site.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-114">Follow hello [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ddc6-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9ddc6-115">Prerequisites</span></span>

<span data-ttu-id="9ddc6-116">toocomplete이이 자습서:</span><span class="sxs-lookup"><span data-stu-id="9ddc6-116">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="9ddc6-117">App Service 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="9ddc6-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="9ddc6-118">사용자 지정 DNS 이름 tooyour 웹 응용 프로그램 맵</span><span class="sxs-lookup"><span data-stu-id="9ddc6-118">Map a custom DNS name tooyour web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="9ddc6-119">신뢰할 수 있는 인증 기관에서 SSL 인증서 구매</span><span class="sxs-lookup"><span data-stu-id="9ddc6-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="9ddc6-120">SSL 인증서에 대한 요구 사항</span><span class="sxs-lookup"><span data-stu-id="9ddc6-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="9ddc6-121">앱 서비스에서 인증서 toouse hello 인증서 요구 사항을 준수 하는 모든 hello를 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-121">toouse a certificate in App Service, hello certificate must meet all hello following requirements:</span></span>

* <span data-ttu-id="9ddc6-122">신뢰할 수 있는 인증 기관에서 서명됨</span><span class="sxs-lookup"><span data-stu-id="9ddc6-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="9ddc6-123">암호로 보호된 PFX 파일로 내보냄</span><span class="sxs-lookup"><span data-stu-id="9ddc6-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="9ddc6-124">길이가 2048비트 이상인 개인 키를 포함함</span><span class="sxs-lookup"><span data-stu-id="9ddc6-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="9ddc6-125">Hello 인증서 체인에 모든 중간 인증서를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-125">Contains all intermediate certificates in hello certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="9ddc6-126">**ECC(타원 곡선 암호화) 인증서**는 App Service에서 사용할 수 있지만 이 문서에서는 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="9ddc6-127">인증 기관 hello 정확한 단계 toocreate ECC 인증서에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-127">Work with your certificate authority on hello exact steps toocreate ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="9ddc6-128">웹앱 준비</span><span class="sxs-lookup"><span data-stu-id="9ddc6-128">Prepare your web app</span></span>

<span data-ttu-id="9ddc6-129">toobind 사용자 지정 SSL 인증서 tooyour 웹 응용 프로그램 프로그램 [앱 서비스 계획](https://azure.microsoft.com/pricing/details/app-service/) hello에 있어야 **기본**, **표준**, 또는 **프리미엄** 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-129">toobind a custom SSL certificate tooyour web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in hello **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="9ddc6-130">이 단계에서는 있습니다 지원 되는지 확인을 웹 앱 hello에 가격 책정 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-130">In this step, you make sure that your web app is in hello supported pricing tier.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="9ddc6-131">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="9ddc6-131">Log in tooAzure</span></span>

<span data-ttu-id="9ddc6-132">열기 hello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-132">Open hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-tooyour-web-app"></a><span data-ttu-id="9ddc6-133">Tooyour 웹 응용 프로그램 이동</span><span class="sxs-lookup"><span data-stu-id="9ddc6-133">Navigate tooyour web app</span></span>

<span data-ttu-id="9ddc6-134">Hello 왼쪽된 메뉴에서 클릭 **응용 프로그램 서비스**, 웹 응용 프로그램의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-134">From hello left menu, click **App Services**, and then click hello name of your web app.</span></span>

![웹앱 선택](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="9ddc6-136">웹 응용 프로그램의 hello 관리 페이지에 연결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-136">You have landed in hello management page of your web app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="9ddc6-137">가격 책정 계층 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-137">Check hello pricing tier</span></span>

<span data-ttu-id="9ddc6-138">웹 응용 프로그램 페이지의 왼쪽 탐색 hello 스크롤하여 toohello **설정** 선택한 섹션 **(앱 서비스 계획) 수직**합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-138">In hello left-hand navigation of your web app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![강화 메뉴](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="9ddc6-140">Toomake 있는지 웹 앱 hello에 있지 않은지 확인 **무료** 또는 **Shared** 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-140">Check toomake sure that your web app is not in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="9ddc6-141">웹앱의 현재 계층이 진한 파란색 상자로 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![가격 책정 계층 확인](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="9ddc6-143">사용자 지정 SSL hello에서 지원 되지 않습니다 **무료** 또는 **Shared** 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-143">Custom SSL is not supported in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="9ddc6-144">tooscale 해야 할 경우 hello 다음 섹션의 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-144">If you need tooscale up, follow hello steps in hello next section.</span></span> <span data-ttu-id="9ddc6-145">Hello를 닫습니다 **가격 책정 계층 선택** 페이지 및 너무 건너뛸[업로드 하 고 SSL 인증서에 바인딩할](#upload)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-145">Otherwise, close hello **Choose your pricing tier** page and skip too[Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="9ddc6-146">App Service 계획 강화</span><span class="sxs-lookup"><span data-stu-id="9ddc6-146">Scale up your App Service plan</span></span>

<span data-ttu-id="9ddc6-147">Hello 중 하나를 선택 **기본**, **표준**, 또는 **프리미엄** 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-147">Select one of hello **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="9ddc6-148">**선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-148">Click **Select**.</span></span>

![가격 책정 계층 선택](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="9ddc6-150">Hello 알림을 다음 표시 되 면 hello 크기 조정 작업이 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-150">When you see hello following notification, hello scale operation is complete.</span></span>

![강화 알림](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="9ddc6-152">SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="9ddc6-152">Bind your SSL certificate</span></span>

<span data-ttu-id="9ddc6-153">사용자는 준비 tooupload SSL 인증서 tooyour 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-153">You are ready tooupload your SSL certificate tooyour web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="9ddc6-154">중간 인증서 병합</span><span class="sxs-lookup"><span data-stu-id="9ddc6-154">Merge intermediate certificates</span></span>

<span data-ttu-id="9ddc6-155">인증 기관에 인증서가 여러 개 hello 인증서 체인을 제공 하는 경우 순서 대로 toomerge hello 인증서가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-155">If your certificate authority gives you multiple certificates in hello certificate chain, you need toomerge hello certificates in order.</span></span> 

<span data-ttu-id="9ddc6-156">toodo 각 열기가 인증서를 텍스트 편집기에서 받은 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-156">toodo this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="9ddc6-157">라는 hello 병합 된 인증서에 대 한 파일을 만들 _mergedcertificate.crt_합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-157">Create a file for hello merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="9ddc6-158">텍스트 편집기에서이 파일에 각 인증서의 hello 콘텐츠를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-158">In a text editor, copy hello content of each certificate into this file.</span></span> <span data-ttu-id="9ddc6-159">인증서의 hello 순서는 서식 파일을 다음 hello 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-159">hello order of your certificates should look like hello following template:</span></span>

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

### <a name="export-certificate-toopfx"></a><span data-ttu-id="9ddc6-160">인증서 tooPFX 내보내기</span><span class="sxs-lookup"><span data-stu-id="9ddc6-160">Export certificate tooPFX</span></span>

<span data-ttu-id="9ddc6-161">병합 된 SSL 인증서를 사용 하 여 인증서 요청 생성 hello 개인 키로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-161">Export your merged SSL certificate with hello private key that your certificate request was generated with.</span></span>

<span data-ttu-id="9ddc6-162">OpenSSL을 사용하여 인증서 요청을 생성한 경우 개인 키 파일을 만든 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="9ddc6-163">tooexport hello 다음 명령을 실행 하 여 인증서 tooPFX 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-163">tooexport your certificate tooPFX, run hello following command.</span></span> <span data-ttu-id="9ddc6-164">Hello 자리 표시자를 대체  _&lt;개인 키 파일 >_ 및  _&lt;병합-인증서-파일 >_합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-164">Replace hello placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="9ddc6-165">메시지가 표시되면 내보내기 암호를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-165">When prompted, define an export password.</span></span> <span data-ttu-id="9ddc6-166">프로그램 SSL 인증서 tooApp 서비스 나중에 업로드할 때이 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-166">You'll use this password when uploading your SSL certificate tooApp Service later.</span></span>

<span data-ttu-id="9ddc6-167">IIS를 사용 하는 경우 또는 _Certreq.exe_ toogenerate 인증서 요청, 설치 hello 인증서 tooyour 로컬 컴퓨터 즉, 한 다음 [hello 인증서 tooPFX 내보내기](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-167">If you used IIS or _Certreq.exe_ toogenerate your certificate request, install hello certificate tooyour local machine, and then [export hello certificate tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="9ddc6-168">SSL 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="9ddc6-168">Upload your SSL certificate</span></span>

<span data-ttu-id="9ddc6-169">tooupload SSL 인증서를 클릭 하 여 **SSL 인증서** hello 왼쪽 탐색의 웹 앱에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-169">tooupload your SSL certificate, click **SSL certificates** in hello left navigation of your web app.</span></span>

<span data-ttu-id="9ddc6-170">**인증서 업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="9ddc6-171">**PFX 인증서 파일**에서 PFX 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="9ddc6-172">**인증서 암호**, hello PFX 파일을 내보낼 때 만든 hello 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-172">In **Certificate password**, type hello password that you created when you exported hello PFX file.</span></span>

<span data-ttu-id="9ddc6-173">**업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-173">Click **Upload**.</span></span>

![인증서 업로드](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="9ddc6-175">Hello에 표시 하는 앱 서비스 인증서를 업로드 완료 되 면 **SSL 인증서** 페이지.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-175">When App Service finishes uploading your certificate, it appears in hello **SSL certificates** page.</span></span>

![업로드된 인증서](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="9ddc6-177">SSL 인증서 바인딩</span><span class="sxs-lookup"><span data-stu-id="9ddc6-177">Bind your SSL certificate</span></span>

<span data-ttu-id="9ddc6-178">Hello에 **SSL 바인딩을** 섹션에서 클릭 **바인딩을 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-178">In hello **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="9ddc6-179">Hello에 **SSL 바인딩 추가** 페이지 hello 드롭다운 tooselect hello 도메인 이름 toosecure 및 인증서 toouse hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-179">In hello **Add SSL Binding** page, use hello dropdowns tooselect hello domain name toosecure, and hello certificate toouse.</span></span>

> [!NOTE]
> <span data-ttu-id="9ddc6-180">인증서를 업로드 한 해도 hello에 hello 도메인 이름에 표시 되지 않는 경우 **Hostname** 드롭다운에서 hello 브라우저 페이지를 새로 고 치세요.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-180">If you have uploaded your certificate but don't see hello domain name(s) in hello **Hostname** dropdown, try refreshing hello browser page.</span></span>
>
>

<span data-ttu-id="9ddc6-181">**SSL 유형**을 선택 하는지 여부를 toouse  **[SNI 서버 이름 표시 ()](http://en.wikipedia.org/wiki/Server_Name_Indication)**  또는 IP 기반 SSL 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-181">In **SSL Type**, select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="9ddc6-182">**SNI 기반 SSL** - 여러 개의 SNI 기반 SSL 바인딩을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="9ddc6-183">이 옵션을 사용 하면 여러 SSL 인증서 toosecure hello에 여러 도메인이 동일한 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-183">This option allows multiple SSL certificates toosecure multiple domains on hello same IP address.</span></span> <span data-ttu-id="9ddc6-184">대부분의 최신 브라우저(Internet Explorer, Chrome, Firefox 및 Opera 포함)는 SNI를 지원합니다. [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)(서버 이름 표시)에서 더 포괄적인 브라우저 지원 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="9ddc6-185">**IP 기반 SSL** - IP 기반 SSL 바인딩 하나만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="9ddc6-186">이 옵션을 사용 하면 하나의 SSL 인증서 toosecure 전용된 공용 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-186">This option allows only one SSL certificate toosecure a dedicated public IP address.</span></span> <span data-ttu-id="9ddc6-187">toosecure 여러 도메인에 보안을 설정 해야을 사용 하 여 모든 hello 같은 SSL 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-187">toosecure multiple domains, you must secure them all using hello same SSL certificate.</span></span> <span data-ttu-id="9ddc6-188">SSL 바인딩에 대 한 hello 기존의 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-188">This is hello traditional option for SSL binding.</span></span>

<span data-ttu-id="9ddc6-189">**바인딩 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-189">Click **Add Binding**.</span></span>

![SSL 인증서 바인딩](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="9ddc6-191">Hello에 표시 하는 앱 서비스 인증서를 업로드 완료 되 면 **SSL 바인딩을** 섹션.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-191">When App Service finishes uploading your certificate, it appears in hello **SSL bindings** sections.</span></span>

![바인딩된 tooweb 응용 프로그램 인증서](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="9ddc6-193">IP SSL에 대한 A 레코드 다시 매핑</span><span class="sxs-lookup"><span data-stu-id="9ddc6-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="9ddc6-194">웹 앱에서 IP 기반 SSL를 사용 하지 않는 경우 너무 건너뜁니다[사용자 지정 도메인에 대 한 테스트 HTTPS](#test)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-194">If you don't use IP-based SSL in your web app, skip too[Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="9ddc6-195">기본적으로 웹앱에서는 공유 공용 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="9ddc6-196">IP 기반 SSL을 사용하여 인증서를 바인딩하면 App Service에서 웹앱에 대한 새로운 전용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="9ddc6-197">A 레코드 tooyour 웹 응용 프로그램을 매핑한 경우이 새, 전용 IP 주소로 도메인 레지스트리를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-197">If you have mapped an A record tooyour web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="9ddc6-198">웹 앱의 **사용자 지정 도메인** 페이지 hello 새 전용된 IP 주소를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-198">Your web app's **Custom domain** page is updated with hello new, dedicated IP address.</span></span> <span data-ttu-id="9ddc6-199">[이 IP 주소를 복사](app-service-web-tutorial-custom-domain.md#info), 다음 [다시 매핑 hello 레코드](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis 새 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap hello A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="9ddc6-200">HTTPS 테스트</span><span class="sxs-lookup"><span data-stu-id="9ddc6-200">Test HTTPS</span></span>

<span data-ttu-id="9ddc6-201">이제 toodo 없어진을 사용자 지정 도메인에 대 한 HTTPS 작동 하는지 toomake 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-201">All that's left toodo now is toomake sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="9ddc6-202">다양 한 브라우저에서 찾은 너무`https://<your.custom.domain>` toosee 웹 앱을 처리 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-202">In various browsers, browse too`https://<your.custom.domain>` toosee that it serves up your web app.</span></span>

![포털 탐색 tooAzure 응용 프로그램](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="9ddc6-204">웹앱에서 인증서 유효성 검사 오류가 발생한 경우 자체 서명된 인증서를 사용하고 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="9ddc6-205">않은 hello 경우, 있습니다 수 생략 되었으므로 중간 인증서 toohello PFX 인증서 파일을 내보낼 때.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-205">If that's not hello case, you may have left out intermediate certificates when you export your certificate toohello PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="9ddc6-206">HTTPS 적용</span><span class="sxs-lookup"><span data-stu-id="9ddc6-206">Enforce HTTPS</span></span>

<span data-ttu-id="9ddc6-207">App Service에서는 HTTPS를 적용하지 *않으므로* 방문자는 HTTP를 사용하여 웹앱에 계속 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="9ddc6-208">hello에 다시 쓰기 규칙을 정의 하는 웹 앱에 대 한 HTTPS tooenforce _web.config_ 웹 앱에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-208">tooenforce HTTPS for your web app, define a rewrite rule in hello _web.config_ file for your web app.</span></span> <span data-ttu-id="9ddc6-209">앱 서비스 웹 앱의 hello 언어 프레임 워크에 관계 없이이 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-209">App Service uses this file, regardless of hello language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="9ddc6-210">언어별 요청 리디렉션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="9ddc6-211">ASP.NET MVC hello צ ְ ײ [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) hello 다시 쓰기 규칙에서 대신 필터 _web.config_합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-211">ASP.NET MVC can use hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of hello rewrite rule in _web.config_.</span></span>

<span data-ttu-id="9ddc6-212">.NET 개발자는 이 파일에 친숙해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="9ddc6-213">솔루션의 hello 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-213">It is in hello root of your solution.</span></span>

<span data-ttu-id="9ddc6-214">또는 PHP, Node.js, Python 또는 Java로 개발할 경우 사용자 대신 App Service에서 이 파일을 생성했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="9ddc6-215">Hello 지침에 따라 tooyour 웹 앱의 FTP 끝점 연결 [프로그램 응용 프로그램 tooAzure FTP/S를 사용 하 여 응용 프로그램 서비스를 배포할](app-service-deploy-ftp.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-215">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="9ddc6-216">이 파일은 _/home/site/wwwroot_에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="9ddc6-217">그렇지 않은 경우 만들기는 _web.config_ hello 다음과 같은 XML이이 폴더에서:</span><span class="sxs-lookup"><span data-stu-id="9ddc6-217">If not, create a _web.config_ file in this folder with hello following XML:</span></span>

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

<span data-ttu-id="9ddc6-218">기존 _web.config_ 파일, hello 전체 복사 `<rule>` 요소에 프로그램 _web.config_의 `configuration/system.webServer/rewrite/rules` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-218">For an existing _web.config_ file, copy hello entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="9ddc6-219">다른 경우 `<rule>` 요소에 프로그램 _web.config_, 복사 위치 hello `<rule>` hello 다른 하기 전에 요소 `<rule>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-219">If there are other `<rule>` elements in your _web.config_, place hello copied `<rule>` element before hello other `<rule>` elements.</span></span>

<span data-ttu-id="9ddc6-220">이 규칙 hello 사용자가 HTTP 요청 tooyour 웹 앱 때마다 301 (영구적 이동) toohello HTTPS 프로토콜을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-220">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="9ddc6-221">예를 들어에서 리디렉션합니다 `http://contoso.com` 너무`https://contoso.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-221">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

<span data-ttu-id="9ddc6-222">IIS URL 재작성 모듈 hello에 대 한 자세한 내용은 참조 hello [URL 재작성](http://www.iis.net/downloads/microsoft/url-rewrite) 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-222">For more information on hello IIS URL Rewrite module, see hello [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="9ddc6-223">Linux의 Web Apps에 HTTPS 적용</span><span class="sxs-lookup"><span data-stu-id="9ddc6-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="9ddc6-224">Linux의 App Service에서는 HTTPS를 적용하지 *않으므로* 누구든지 여전히 HTTP를 사용하여 웹앱에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="9ddc6-225">hello에 다시 쓰기 규칙을 정의 하는 웹 앱에 대 한 HTTPS tooenforce _.htaccess_ 웹 앱에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-225">tooenforce HTTPS for your web app, define a rewrite rule in hello _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="9ddc6-226">Hello 지침에 따라 tooyour 웹 앱의 FTP 끝점 연결 [프로그램 응용 프로그램 tooAzure FTP/S를 사용 하 여 응용 프로그램 서비스를 배포할](app-service-deploy-ftp.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-226">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="9ddc6-227">_/home/site/wwwroot_을 만듭니다는 _.htaccess_ 코드 다음 hello로 파일:</span><span class="sxs-lookup"><span data-stu-id="9ddc6-227">In _/home/site/wwwroot_, create an _.htaccess_ file with hello following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="9ddc6-228">이 규칙 hello 사용자가 HTTP 요청 tooyour 웹 앱 때마다 301 (영구적 이동) toohello HTTPS 프로토콜을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-228">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="9ddc6-229">예를 들어에서 리디렉션합니다 `http://contoso.com` 너무`https://contoso.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-229">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="9ddc6-230">스크립트를 사용하여 자동화</span><span class="sxs-lookup"><span data-stu-id="9ddc6-230">Automate with scripts</span></span>

<span data-ttu-id="9ddc6-231">Hello를 사용 하 여 스크립트를 사용 하 여 웹 앱에 대 한 SSL 바인딩의 자동화할 수 있습니다 [Azure CLI](/cli/azure/install-azure-cli) 또는 [Azure PowerShell](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-231">You can automate SSL bindings for your web app with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="9ddc6-232">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9ddc6-232">Azure CLI</span></span>

<span data-ttu-id="9ddc6-233">다음 명령을 hello는 내보낸된 PFX 파일을 업로드 하 고 hello 지문을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-233">hello following command uploads an exported PFX file and gets hello thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="9ddc6-234">hello 다음 명령을 한 SNI 기반 SSL 바인딩을 추가, hello 이전 명령에서 hello 지문을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-234">hello following command adds an SNI-based SSL binding, using hello thumbprint from hello previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="9ddc6-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ddc6-235">Azure PowerShell</span></span>

<span data-ttu-id="9ddc6-236">hello 다음 명령은 내보낸된 PFX 파일을 업로드 하 고 SNI 기반 SSL 바인딩을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-236">hello following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="9ddc6-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9ddc6-237">Next steps</span></span>

<span data-ttu-id="9ddc6-238">이 자습서에서 학습한 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9ddc6-239">앱의 가격 책정 계층 업그레이드</span><span class="sxs-lookup"><span data-stu-id="9ddc6-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="9ddc6-240">사용자 지정 SSL 인증서 tooApp 서비스 바인딩</span><span class="sxs-lookup"><span data-stu-id="9ddc6-240">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="9ddc6-241">앱에 대해 HTTPS 적용</span><span class="sxs-lookup"><span data-stu-id="9ddc6-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="9ddc6-242">스크립트로 SSL 인증서 바인딩 자동화</span><span class="sxs-lookup"><span data-stu-id="9ddc6-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="9ddc6-243">다음 자습서 toolearn toohello 어떻게 발전 toouse Azure 콘텐츠 배달 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="9ddc6-243">Advance toohello next tutorial toolearn how toouse Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9ddc6-244">추가 네트워크 CDN (콘텐츠 배달) tooan Azure 앱 서비스</span><span class="sxs-lookup"><span data-stu-id="9ddc6-244">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
