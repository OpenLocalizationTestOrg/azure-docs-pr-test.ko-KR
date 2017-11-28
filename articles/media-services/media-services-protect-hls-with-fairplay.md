---
title: "Apple FairPlay-Azure 또는 Microsoft PlayReady로 HLS 콘텐츠를 aaaProtect | Microsoft Docs"
description: "이 항목 한 개요를 제공 하 고 Azure 미디어 서비스 toodynamically toouse Apple FairPlay 사용 하 여 HTTP 라이브 스트리밍 (HLS) 콘텐츠를 암호화 하는 방법을 보여 줍니다. 또한 toouse hello 미디어 서비스 배달 서비스 toodeliver FairPlay 라이선스 tooclients를 라이선스 하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="2f244-104">Microsoft PlayReady 또는 Apple FairPlay로 HLS 콘텐츠 보호</span><span class="sxs-lookup"><span data-stu-id="2f244-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="2f244-105">Azure 미디어 서비스 사용 하면 toodynamically hello 다음 형식을 사용 하 여 HTTP 라이브 스트리밍 (HLS) 콘텐츠를 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-105">Azure Media Services enables you toodynamically encrypt your HTTP Live Streaming (HLS) content by using hello following formats:</span></span>  

* <span data-ttu-id="2f244-106">**AES-128 비트 봉투 암호화되지 않은 키**</span><span class="sxs-lookup"><span data-stu-id="2f244-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="2f244-107">hello 전체 청크 암호화 되어 hello를 사용 하 여 **S-128 CBC** 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-107">hello entire chunk is encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="2f244-108">hello 스트림의 hello 암호 해독 되는 iOS 및 OS X 플레이어 고유 하 게 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-108">hello decryption of hello stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="2f244-109">자세한 내용은 [AES-128 동적 암호화 및 키 배달 서비스 사용](media-services-protect-with-aes128.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f244-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="2f244-110">**Apple FairPlay**</span><span class="sxs-lookup"><span data-stu-id="2f244-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="2f244-111">hello 개별 비디오 및 오디오 샘플 hello를 사용 하 여 암호화 된 **S-128 CBC** 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-111">hello individual video and audio samples are encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="2f244-112">**FairPlay 스트리밍** (FPS)는 iOS와 Apple TV 네이티브 지원과 hello 장치 운영 체제에 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-112">**FairPlay Streaming** (FPS) is integrated into hello device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="2f244-113">OS X에서 safari hello 암호화 미디어 확장 (EME) 인터페이스 지원을 사용 하 여 FPS를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-113">Safari on OS X enables FPS by using hello Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="2f244-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="2f244-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="2f244-115">hello 다음 그림에 나와 hello **HLS + FairPlay 또는 PlayReady 동적 암호화** 워크플로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-115">hello following image shows hello **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![동적 암호화 워크플로 다이어그램](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="2f244-117">이 항목에서는 미디어 서비스 toodynamically toouse Apple FairPlay로 HLS 콘텐츠를 암호화 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-117">This topic demonstrates how toouse Media Services toodynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="2f244-118">또한 toouse hello 미디어 서비스 배달 서비스 toodeliver FairPlay 라이선스 tooclients를 라이선스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-118">It also shows how toouse hello Media Services license delivery service toodeliver FairPlay licenses tooclients.</span></span>

> [!NOTE]
> <span data-ttu-id="2f244-119">또한 원하는 tooencrypt HLS PlayReady로 콘텐츠 toocreate 공통 콘텐츠 키를 해야 자산에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-119">If you also want tooencrypt your HLS content with PlayReady, you need toocreate a common content key and associate it with your asset.</span></span> <span data-ttu-id="2f244-120">에 설명 된 대로 tooconfigure hello 콘텐츠 키 권한 부여 정책 등을 또한 해야 [PlayReady를 사용 하 여 동적 일반 암호화](media-services-protect-with-drm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-120">You also need tooconfigure hello content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="2f244-121">요구 사항 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="2f244-121">Requirements and considerations</span></span>

<span data-ttu-id="2f244-122">암호화 된 HLS 미디어 서비스 toodeliver FairPlay, 및 toodeliver FairPlay 라이선스와 함께 사용 하는 경우 hello 다음 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-122">hello following are required when using Media Services toodeliver HLS encrypted with FairPlay, and toodeliver FairPlay licenses:</span></span>

  * <span data-ttu-id="2f244-123">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="2f244-123">An Azure account.</span></span> <span data-ttu-id="2f244-124">자세한 내용은 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f244-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="2f244-125">Media Services 계정.</span><span class="sxs-lookup"><span data-stu-id="2f244-125">A Media Services account.</span></span> <span data-ttu-id="2f244-126">하나의 toocreate 참조 [hello Azure 포털을 사용 하 여 Azure 미디어 서비스 계정 만들기](media-services-portal-create-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-126">toocreate one, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="2f244-127">[Apple Development Program](https://developer.apple.com/)에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="2f244-128">Apple에서는 hello 콘텐츠 소유자 tooobtain hello 요구 [배포 패키지](https://developer.apple.com/contact/fps/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-128">Apple requires hello content owner tooobtain hello [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="2f244-129">미디어 서비스 키 보안 모듈 (KSM)를 이미 구현 하기 hello 최종 FPS 패키지를 요청 하 고 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting hello final FPS package.</span></span> <span data-ttu-id="2f244-130">최종 FPS toogenerate 인증 패키징하고 가져올 hello의 지침을 응용 프로그램 암호 키 (ASK) hello는 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-130">There are instructions in hello final FPS package toogenerate certification and obtain hello Application Secret Key (ASK).</span></span> <span data-ttu-id="2f244-131">FairPlay ASK tooconfigure를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-131">You use ASK tooconfigure FairPlay.</span></span>
  * <span data-ttu-id="2f244-132">Azure 미디어 서비스 .NET SDK 버전 **3.6.0** 이상.</span><span class="sxs-lookup"><span data-stu-id="2f244-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="2f244-133">미디어 서비스 키 배달 측 작업을 수행 하는 hello는 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-133">hello following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="2f244-134">**응용 프로그램 인증서 (AC)**: hello 개인 키가 포함 된.pfx 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-134">**App Cert (AC)**: This is a .pfx file that contains hello private key.</span></span> <span data-ttu-id="2f244-135">이 파일을 만들고 암호로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="2f244-136">키 배달 정책을 구성 하면 Base64 형식으로 해당 암호 및 hello.pfx 파일을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-136">When you configure a key delivery policy, you must provide that password and hello .pfx file in Base64 format.</span></span>

      <span data-ttu-id="2f244-137">단계를 수행 하는 hello FairPlay에 대 한 toogenerate.pfx 인증서 파일 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-137">hello following steps describe how toogenerate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="2f244-138">https://slproweb.com/products/Win32OpenSSL.html에서 OpenSSL을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="2f244-139">Hello FairPlay 인증서와 다른 파일을 Apple에 의해 전달 있는 toohello 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-139">Go toohello folder where hello FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="2f244-140">Hello hello 명령줄에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-140">Run hello following command from hello command line.</span></span> <span data-ttu-id="2f244-141">이 hello.cer 파일 tooa.pem 파일을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-141">This converts hello .cer file tooa .pem file.</span></span>

        <span data-ttu-id="2f244-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span><span class="sxs-lookup"><span data-stu-id="2f244-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="2f244-143">Hello hello 명령줄에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-143">Run hello following command from hello command line.</span></span> <span data-ttu-id="2f244-144">이 hello 개인 키가 있는 hello.pem 파일 tooa.pfx 파일을 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-144">This converts hello .pem file tooa .pfx file with hello private key.</span></span> <span data-ttu-id="2f244-145">그런 다음 hello.pfx 파일에 대 한 hello 암호 OpenSSL에 요청 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-145">hello password for hello .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="2f244-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="2f244-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="2f244-147">**응용 프로그램 인증서 암호가**: hello.pfx 파일을 만들기 위한 hello 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-147">**App Cert password**: hello password for creating hello .pfx file.</span></span>
  * <span data-ttu-id="2f244-148">**응용 프로그램 인증서 암호 ID**: hello 암호를 다른 미디어 서비스 키를 업로드 하는 비슷한 toohow 업로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-148">**App Cert password ID**: You must upload hello password, similar toohow they upload other Media Services keys.</span></span> <span data-ttu-id="2f244-149">사용 하 여 hello **ContentKeyType.FairPlayPfxPassword** enum 값 tooget hello 미디어 서비스 id입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-149">Use hello **ContentKeyType.FairPlayPfxPassword** enum value tooget hello Media Services ID.</span></span> <span data-ttu-id="2f244-150">이것은 필요한 toouse 내 hello 키 배달 정책 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-150">This is what they need toouse inside hello key delivery policy option.</span></span>
  * <span data-ttu-id="2f244-151">**iv**: 16바이트의 임의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="2f244-152">일치 해야 hello 자산 배달 정책에 iv hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-152">It must match hello iv in hello asset delivery policy.</span></span> <span data-ttu-id="2f244-153">생성할 hello iv를 두 위치에 저장 합니다: hello 자산 배달 정책 및 hello 키 배달 정책 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-153">You generate hello iv, and put it in both places: hello asset delivery policy and hello key delivery policy option.</span></span>
  * <span data-ttu-id="2f244-154">**요청**: hello Apple 개발자 포털을 사용 하 여 hello 인증을 생성 하면이 키를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-154">**ASK**: This key is received when you generate hello certification by using hello Apple Developer portal.</span></span> <span data-ttu-id="2f244-155">각 개발 팀에 고유한 ASK가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="2f244-156">Hello ASK의 복사본을 저장 하 고 안전한 장소에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-156">Save a copy of hello ASK, and store it in a safe place.</span></span> <span data-ttu-id="2f244-157">FairPlayAsk tooMedia 서비스로 tooconfigure ASK 나중에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-157">You will need tooconfigure ASK as FairPlayAsk tooMedia Services later.</span></span>
  * <span data-ttu-id="2f244-158">**ASK ID**: 이 ID는 Media Services에 ASK를 업로드할 때 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="2f244-159">ASK hello를 사용 하 여 업로드 해야 **ContentKeyType.FairPlayAsk** 열거형 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-159">You must upload ASK by using hello **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="2f244-160">Hello 결과로 hello 미디어 서비스 ID가 반환 하 고 hello 키 배달 정책 옵션을 설정할 때 용도입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-160">As hello result, hello Media Services ID is returned, and this is what should be used when setting hello key delivery policy option.</span></span>

<span data-ttu-id="2f244-161">hello 다음과 같은 상황이 발생 하는 설정 해야 hello FPS 클라이언트 측:</span><span class="sxs-lookup"><span data-stu-id="2f244-161">hello following things must be set by hello FPS client side:</span></span>

  * <span data-ttu-id="2f244-162">**응용 프로그램 인증서 (AC)**: 일부 페이로드는 hello 운영 체제 tooencrypt 사용 하 여 hello 공개 키를 포함 하는.cer/.der 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-162">**App Cert (AC)**: This is a .cer/.der file that contains hello public key, which hello operating system uses tooencrypt some payload.</span></span> <span data-ttu-id="2f244-163">미디어 서비스는 hello 플레이어에 필요 하기 때문에 항목에 대 한 tooknow가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-163">Media Services needs tooknow about it because it is required by hello player.</span></span> <span data-ttu-id="2f244-164">hello 키 배달 서비스 hello 해당 개인 키를 사용 하 여 해독 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-164">hello key delivery service decrypts it using hello corresponding private key.</span></span>

<span data-ttu-id="2f244-165">tooplay는 FairPlay 암호화 스트림을 다시, 실제 ASK 첫 번째를 가져오고 실제 인증서를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-165">tooplay back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="2f244-166">이 프로세스에서는 다음 세 가지 요소를 모두 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="2f244-167">.der 파일</span><span class="sxs-lookup"><span data-stu-id="2f244-167">.der file</span></span>
  * <span data-ttu-id="2f244-168">.pfx 파일</span><span class="sxs-lookup"><span data-stu-id="2f244-168">.pfx file</span></span>
  * <span data-ttu-id="2f244-169">hello.pfx에 대 한 암호</span><span class="sxs-lookup"><span data-stu-id="2f244-169">password for hello .pfx</span></span>

<span data-ttu-id="2f244-170">hello 다음 클라이언트는 지원로 HLS **S-128 CBC** 암호화: OS X, Apple TV iOS Safari 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-170">hello following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="2f244-171">FairPlay 동적 암호화 및 라이선스 배달 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="2f244-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="2f244-172">hello 다음은 hello 미디어 서비스 라이선스 배달 서비스를 사용 하 여 및 동적 암호화를 사용 하 여 FairPlay로 자산을 보호 하기 위한 일반적인 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-172">hello following are general steps for protecting your assets with FairPlay by using hello Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="2f244-173">자산을 만들고 hello 자산에 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-173">Create an asset, and upload files into hello asset.</span></span>
2. <span data-ttu-id="2f244-174">Hello 파일 toohello 적응 비트 전송률 MP4 세트를 포함 하는 hello 자산을으로 인코딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="2f244-174">Encode hello asset that contains hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="2f244-175">콘텐츠 키를 만들고 hello 인코딩된 자산에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-175">Create a content key, and associate it with hello encoded asset.</span></span>  
4. <span data-ttu-id="2f244-176">Hello 콘텐츠 키 권한 부여 정책을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-176">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="2f244-177">Hello 다음을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-177">Specify hello following:</span></span>

   * <span data-ttu-id="2f244-178">hello에 (이 경우 FairPlay) 배달 방법.</span><span class="sxs-lookup"><span data-stu-id="2f244-178">hello delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="2f244-179">FairPlay 정책 옵션 구성 -</span><span class="sxs-lookup"><span data-stu-id="2f244-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="2f244-180">방법에 대 한 자세한 내용은 tooconfigure FairPlay, 참조 hello **ConfigureFairPlayPolicyOptions()** hello 샘플 아래 메서드.</span><span class="sxs-lookup"><span data-stu-id="2f244-180">For details on how tooconfigure FairPlay, see hello **ConfigureFairPlayPolicyOptions()** method in hello sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="2f244-181">일반적으로 원할 tooconfigure FairPlay 정책 옵션을 한 번만 인증은 ASK 서로 집합 하나만 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-181">Usually, you would want tooconfigure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="2f244-182">제한(열기 또는 토큰).</span><span class="sxs-lookup"><span data-stu-id="2f244-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="2f244-183">Hello 키 toohello 클라이언트 배달 방법을 정의 하는 정보 특정 toohello 키 배달 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-183">Information specific toohello key delivery type that defines how hello key is delivered toohello client.</span></span>
5. <span data-ttu-id="2f244-184">Hello 자산 배달 정책을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-184">Configure hello asset delivery policy.</span></span> <span data-ttu-id="2f244-185">hello 배달 정책 구성에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-185">hello delivery policy configuration includes:</span></span>

   * <span data-ttu-id="2f244-186">hello 배달 프로토콜 (HLS)입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-186">hello delivery protocol (HLS).</span></span>
   * <span data-ttu-id="2f244-187">동적 암호화 (일반 CBC 암호화)의 hello 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-187">hello type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="2f244-188">hello 라이선스 취득 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-188">hello license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="2f244-189">FairPlay와 다른 디지털 Rights Management (DRM) 시스템을 사용 하 여 암호화 하는 스트림을 toodeliver 원하는 tooconfigure 별도 배달 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-189">If you want toodeliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have tooconfigure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="2f244-190">HTTP (대시)와 CENC (Common Encryption) (PlayReady + Widevine) 및 PlayReady로 부드러운 스트리밍 적응 스트리밍 동적 하나 IAssetDeliveryPolicy tooconfigure</span><span class="sxs-lookup"><span data-stu-id="2f244-190">One IAssetDeliveryPolicy tooconfigure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="2f244-191">다른 IAssetDeliveryPolicy tooconfigure FairPlay HLS에 대 한</span><span class="sxs-lookup"><span data-stu-id="2f244-191">Another IAssetDeliveryPolicy tooconfigure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="2f244-192">OnDemand 로케이터 tooget 스트리밍 URL을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-192">Create an OnDemand locator tooget a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="2f244-193">플레이어 앱별 FairPlay 키 배달 사용</span><span class="sxs-lookup"><span data-stu-id="2f244-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="2f244-194">Hello iOS SDK를 사용 하 여 플레이어 응용 프로그램을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-194">You can develop player apps by using hello iOS SDK.</span></span> <span data-ttu-id="2f244-195">toobe 수 tooplay FairPlay 콘텐츠 tooimplement hello 라이선스 교환 프로토콜을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-195">toobe able tooplay FairPlay content, you have tooimplement hello license exchange protocol.</span></span> <span data-ttu-id="2f244-196">Apple에서는 이 프로토콜을 지정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="2f244-197">가 tooeach 앱 toosend 키 배달 요청 하는 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-197">It is up tooeach app how toosend key delivery requests.</span></span> <span data-ttu-id="2f244-198">hello 미디어 서비스 FairPlay 키 배달 서비스는 hello SPC toocome hello 다음 양식에서에서 www-form-url 인코딩된 post 메시지로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-198">hello Media Services FairPlay key delivery service expects hello SPC toocome as a www-form-url encoded post message, in hello following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="2f244-199">Azure Media Player hello 초기 FairPlay 재생을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-199">Azure Media Player doesn’t support FairPlay playback out of hello box.</span></span> <span data-ttu-id="2f244-200">MAC OS X에서 tooget FairPlay 재생 hello Apple 개발자 계정에서에서 hello 샘플 플레이어를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-200">tooget FairPlay playback on MAC OS X, obtain hello sample player from hello Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="2f244-201">스트리밍 URL</span><span class="sxs-lookup"><span data-stu-id="2f244-201">Streaming URLs</span></span>
<span data-ttu-id="2f244-202">Hello 스트리밍 URL에에서는 암호화 태그를 사용 해야 둘 이상의 DRM으로 자산 암호화 된 경우: (형식 ='m3u8-aapl' 암호화 'xxx' =) 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in hello streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="2f244-203">hello 고려 사항에 따라 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-203">hello following considerations apply:</span></span>

* <span data-ttu-id="2f244-204">1개 이하의 암호화 형식만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="2f244-205">hello 암호화 유형 toobe 한 암호화가 적용 된 toohello 자산만 hello URL에 지정 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-205">hello encryption type doesn't have toobe specified in hello URL if only one encryption was applied toohello asset.</span></span>
* <span data-ttu-id="2f244-206">hello 암호화 유형은 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-206">hello encryption type is case insensitive.</span></span>
* <span data-ttu-id="2f244-207">hello 다음 암호화 종류를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-207">hello following encryption types can be specified:</span></span>  
  * <span data-ttu-id="2f244-208">**cenc**: 일반 암호화(PlayReady 또는 Widevine)</span><span class="sxs-lookup"><span data-stu-id="2f244-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="2f244-209">**cbcs-aapl**: FairPlay</span><span class="sxs-lookup"><span data-stu-id="2f244-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="2f244-210">**cbc**: AES 봉투 암호화</span><span class="sxs-lookup"><span data-stu-id="2f244-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="2f244-211">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="2f244-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="2f244-212">개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-212">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="2f244-213">추가 요소를 너무 다음 hello**appSettings** app.config 파일에 정의 된:</span><span class="sxs-lookup"><span data-stu-id="2f244-213">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="2f244-214">예제</span><span class="sxs-lookup"><span data-stu-id="2f244-214">Example</span></span>

<span data-ttu-id="2f244-215">다음 예제는 hello hello 기능 toouse 미디어 서비스 toodeliver FairPlay로 암호화 된 콘텐츠를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-215">hello following sample demonstrates hello ability toouse Media Services toodeliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="2f244-216">이 기능은 for.NET 버전 3.6.0 hello Azure Media Services SDK에서에서 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-216">This functionality was introduced in hello Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="2f244-217">이 섹션에 표시 된 hello 코드도 Program.cs 파일의 hello 코드를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-217">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="2f244-218">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="2f244-219">Hello를 사용 해야 항상 사용 하는 경우 동일한 정책 ID hello 동일 일 / 액세스 하는 로케이터가 있는 원위치에서 의도 한 tooremain 오랜 시간 동안 (비-업로드 정책)는에 대 한 예를 들어 정책을 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="2f244-219">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="2f244-220">자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2f244-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="2f244-221">확인 되었는지 tooupdate 변수 toopoint toofolders 입력된 파일이 있는 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="2f244-221">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }


        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Open",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                        Requirements = null
                    }
                    };


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Token Authorization Policy",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                        Requirements = tokenTemplateString,
                    }
                    };

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();
            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
            assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="2f244-222">다음 단계: 미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="2f244-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2f244-223">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="2f244-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
