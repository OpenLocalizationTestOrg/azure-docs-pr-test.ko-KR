---
title: "Microsoft PlayReady 또는 Apple FairPlay로 HLS 콘텐츠 보호 - Azure | Microsoft Docs"
description: "이 항목에서는 Azure 미디어 서비스를 사용하여 Apple FairPlay에서 HLS(HTTP 라이브 스트리밍) 콘텐츠를 동적으로 암호화하는 방법과 개요를 설명합니다. 또한 미디어 서비스 라이선스 배달 서비스를 사용하여 클라이언트에 FairPlay 라이선스를 제공하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 895d6307b1cef74e195cc2ffd8dbef4196e97b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="d1fb2-104">Microsoft PlayReady 또는 Apple FairPlay로 HLS 콘텐츠 보호</span><span class="sxs-lookup"><span data-stu-id="d1fb2-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="d1fb2-105">Azure Media Services를 사용하면 다음 형식을 사용하여 HLS(HTTP 라이브 스트리밍) 콘텐츠를 동적으로 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-105">Azure Media Services enables you to dynamically encrypt your HTTP Live Streaming (HLS) content by using the following formats:</span></span>  

* <span data-ttu-id="d1fb2-106">**AES-128 비트 봉투 암호화되지 않은 키**</span><span class="sxs-lookup"><span data-stu-id="d1fb2-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="d1fb2-107">전체 청크는 **AES-128 CBC** 모드를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-107">The entire chunk is encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="d1fb2-108">스트림의 암호 해독은 iOS 및 OS X 플레이어에서 고유하게 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-108">The decryption of the stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="d1fb2-109">자세한 내용은 [AES-128 동적 암호화 및 키 배달 서비스 사용](media-services-protect-with-aes128.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="d1fb2-110">**Apple FairPlay**</span><span class="sxs-lookup"><span data-stu-id="d1fb2-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="d1fb2-111">개별 비디오 및 오디오 샘플은 **AES-128 CBC** 모드를 사용하여 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-111">The individual video and audio samples are encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="d1fb2-112">**FairPlay 스트리밍** (FPS)은 장치 운영 체제에 통합되며, iOS 및 Apple TV에서 고유하게 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-112">**FairPlay Streaming** (FPS) is integrated into the device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="d1fb2-113">OS X의 Safari는 EME(Encrypted Media Extensions) 인터페이스 지원을 사용하여 FPS를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-113">Safari on OS X enables FPS by using the Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="d1fb2-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="d1fb2-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="d1fb2-115">다음 이미지에서는 **HLS + FairPlay 또는 PlayReady 동적 암호화** 워크플로를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-115">The following image shows the **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![동적 암호화 워크플로 다이어그램](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="d1fb2-117">이 항목에서는 Media Services를 사용하여 Apple FairPlay에서 HLS 컨텐트를 동적으로 암호화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-117">This topic demonstrates how to use Media Services to dynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="d1fb2-118">또한 미디어 서비스 라이선스 배달 서비스를 사용하여 클라이언트에 FairPlay 라이선스를 제공하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-118">It also shows how to use the Media Services license delivery service to deliver FairPlay licenses to clients.</span></span>

> [!NOTE]
> <span data-ttu-id="d1fb2-119">PlayReady로 HLS 콘텐츠를 암호화하려면 공통 콘텐츠 키를 만들고 자산에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-119">If you also want to encrypt your HLS content with PlayReady, you need to create a common content key and associate it with your asset.</span></span> <span data-ttu-id="d1fb2-120">[PlayReady 동적 일반 암호화 사용](media-services-protect-with-drm.md)에서 설명한 대로 콘텐츠 키의 권한 부여 정책을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-120">You also need to configure the content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="d1fb2-121">요구 사항 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="d1fb2-121">Requirements and considerations</span></span>

<span data-ttu-id="d1fb2-122">Media Services를 사용하여 FairPlay로 암호화된 HLS를 배달하고 FairPlay 라이선스를 배달할 때 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-122">The following are required when using Media Services to deliver HLS encrypted with FairPlay, and to deliver FairPlay licenses:</span></span>

  * <span data-ttu-id="d1fb2-123">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-123">An Azure account.</span></span> <span data-ttu-id="d1fb2-124">자세한 내용은 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="d1fb2-125">미디어 서비스 계정.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-125">A Media Services account.</span></span> <span data-ttu-id="d1fb2-126">계정을 만들려면 [Azure Portal을 사용하여 Azure Media Services 계정 만들기](media-services-portal-create-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-126">To create one, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="d1fb2-127">[Apple Development Program](https://developer.apple.com/)에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="d1fb2-128">Apple에서는 [배포 패키지](https://developer.apple.com/contact/fps/)를 얻으려면 콘텐츠 소유자를 요구합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-128">Apple requires the content owner to obtain the [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="d1fb2-129">이미 Media Services로 KSM(키 보안 모듈)을 구현했고 최종 FPS 패키지를 요청하고 있음을 명시합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting the final FPS package.</span></span> <span data-ttu-id="d1fb2-130">최종 FPS 패키지에는 인증을 생성하고 ASK(응용 프로그램 비밀 키)를 얻기 위한 지침이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-130">There are instructions in the final FPS package to generate certification and obtain the Application Secret Key (ASK).</span></span> <span data-ttu-id="d1fb2-131">ASK를 사용하여 FairPlay를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-131">You use ASK to configure FairPlay.</span></span>
  * <span data-ttu-id="d1fb2-132">Azure 미디어 서비스 .NET SDK 버전 **3.6.0** 이상.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="d1fb2-133">Media Services 키 배달 쪽에서 다음 항목을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-133">The following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="d1fb2-134">**AC(앱 인증서)**: 개인 키가 포함된 .pfx 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-134">**App Cert (AC)**: This is a .pfx file that contains the private key.</span></span> <span data-ttu-id="d1fb2-135">이 파일을 만들고 암호로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="d1fb2-136">키 배달 정책을 구성할 때 해당 암호와 Base64 형식의 .pfx 파일을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-136">When you configure a key delivery policy, you must provide that password and the .pfx file in Base64 format.</span></span>

      <span data-ttu-id="d1fb2-137">다음 단계에서는 FairPlay에 대한 .pfx 인증서 파일을 생성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-137">The following steps describe how to generate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="d1fb2-138">https://slproweb.com/products/Win32OpenSSL.html에서 OpenSSL을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="d1fb2-139">FairPlay 인증서 및 Apple에서 전달하는 다른 파일이 있는 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-139">Go to the folder where the FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="d1fb2-140">명령줄에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-140">Run the following command from the command line.</span></span> <span data-ttu-id="d1fb2-141">이렇게 하면 .cer 파일이 .pem 파일로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-141">This converts the .cer file to a .pem file.</span></span>

        <span data-ttu-id="d1fb2-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span><span class="sxs-lookup"><span data-stu-id="d1fb2-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="d1fb2-143">명령줄에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-143">Run the following command from the command line.</span></span> <span data-ttu-id="d1fb2-144">이렇게 하면 .pem 파일이 개인 키가 있는 .pfx 파일로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-144">This converts the .pem file to a .pfx file with the private key.</span></span> <span data-ttu-id="d1fb2-145">OpenSSL에서 .pfx 파일에 대한 암호를 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-145">The password for the .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="d1fb2-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="d1fb2-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="d1fb2-147">**앱 인증서 암호**: .pfx 파일을 만들기 위한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-147">**App Cert password**: The password for creating the .pfx file.</span></span>
  * <span data-ttu-id="d1fb2-148">**앱 인증서 암호 ID**: 다른 Media Services 키를 업로드하는 방법과 비슷하게 암호를 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-148">**App Cert password ID**: You must upload the password, similar to how they upload other Media Services keys.</span></span> <span data-ttu-id="d1fb2-149">**ContentKeyType.FairPlayPfxPassword** 열거형 값을 사용하여 Media Services ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-149">Use the **ContentKeyType.FairPlayPfxPassword** enum value to get the Media Services ID.</span></span> <span data-ttu-id="d1fb2-150">이 ID는 키 배달 정책 옵션 내에서 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-150">This is what they need to use inside the key delivery policy option.</span></span>
  * <span data-ttu-id="d1fb2-151">**iv**: 16바이트의 임의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="d1fb2-152">자산 배달 정책의 iv와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-152">It must match the iv in the asset delivery policy.</span></span> <span data-ttu-id="d1fb2-153">iv를 생성하여 두 위치, 즉 자산 배달 정책과 키 배달 정책 옵션에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-153">You generate the iv, and put it in both places: the asset delivery policy and the key delivery policy option.</span></span>
  * <span data-ttu-id="d1fb2-154">**ASK**: 이 키는 Apple 개발자 포털을 사용하여 인증을 생성할 때 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-154">**ASK**: This key is received when you generate the certification by using the Apple Developer portal.</span></span> <span data-ttu-id="d1fb2-155">각 개발 팀에 고유한 ASK가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="d1fb2-156">ASK 복사본을 저장하고 안전한 장소에 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-156">Save a copy of the ASK, and store it in a safe place.</span></span> <span data-ttu-id="d1fb2-157">나중에 Media Services에 ASK를 FairPlayAsk로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-157">You will need to configure ASK as FairPlayAsk to Media Services later.</span></span>
  * <span data-ttu-id="d1fb2-158">**ASK ID**: 이 ID는 Media Services에 ASK를 업로드할 때 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="d1fb2-159">**ContentKeyType.FairPlayAsk** 열거형 값을 사용하여 ASK를 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-159">You must upload ASK by using the **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="d1fb2-160">결과적으로 Media Services ID가 반환되고, 이 ID는 키 배달 정책 옵션을 설정할 때 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-160">As the result, the Media Services ID is returned, and this is what should be used when setting the key delivery policy option.</span></span>

<span data-ttu-id="d1fb2-161">FPS 클라이언트 쪽에서 다음을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-161">The following things must be set by the FPS client side:</span></span>

  * <span data-ttu-id="d1fb2-162">**AC(앱 인증서)**: 운영 체제에서 일부 페이로드를 암호화하는 데 사용하는 공개 키가 포함된 .cer/.der 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-162">**App Cert (AC)**: This is a .cer/.der file that contains the public key, which the operating system uses to encrypt some payload.</span></span> <span data-ttu-id="d1fb2-163">플레이어에 필요하기 때문에 Media Services에서 이에 대해 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-163">Media Services needs to know about it because it is required by the player.</span></span> <span data-ttu-id="d1fb2-164">키 배달 서비스는 해당 개인 키를 사용하여 암호를 해독합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-164">The key delivery service decrypts it using the corresponding private key.</span></span>

<span data-ttu-id="d1fb2-165">FairPlay 암호화된 스트림을 재생하려면 먼저 실제 ASK를 받은 다음 실제 인증서를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-165">To play back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="d1fb2-166">이 프로세스에서는 다음 세 가지 요소를 모두 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="d1fb2-167">.der 파일</span><span class="sxs-lookup"><span data-stu-id="d1fb2-167">.der file</span></span>
  * <span data-ttu-id="d1fb2-168">.pfx 파일</span><span class="sxs-lookup"><span data-stu-id="d1fb2-168">.pfx file</span></span>
  * <span data-ttu-id="d1fb2-169">.pfx에 대한 암호</span><span class="sxs-lookup"><span data-stu-id="d1fb2-169">password for the .pfx</span></span>

<span data-ttu-id="d1fb2-170">OS X, Apple TV, iOS의 Safari 클라이언트는 **AES-128 CBC** 암호화로 HLS를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-170">The following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="d1fb2-171">FairPlay 동적 암호화 및 라이선스 배달 서비스 구성</span><span class="sxs-lookup"><span data-stu-id="d1fb2-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="d1fb2-172">다음은 Media Services 라이선스 배달 서비스를 사용하고 동적 암호화도 사용하여 FairPlay로 자산을 보호하는 일반적인 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-172">The following are general steps for protecting your assets with FairPlay by using the Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="d1fb2-173">자산을 만들고 이 자산에 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-173">Create an asset, and upload files into the asset.</span></span>
2. <span data-ttu-id="d1fb2-174">파일이 포함된 자산을 적응 비트 전송률 MP4 집합으로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-174">Encode the asset that contains the file to the adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="d1fb2-175">콘텐츠 키를 만들고 인코딩된 자산과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-175">Create a content key, and associate it with the encoded asset.</span></span>  
4. <span data-ttu-id="d1fb2-176">콘텐츠 키의 권한 부여 정책을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-176">Configure the content key’s authorization policy.</span></span> <span data-ttu-id="d1fb2-177">다음을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-177">Specify the following:</span></span>

   * <span data-ttu-id="d1fb2-178">배달 방법(이 경우 FairPlay)</span><span class="sxs-lookup"><span data-stu-id="d1fb2-178">The delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="d1fb2-179">FairPlay 정책 옵션 구성 -</span><span class="sxs-lookup"><span data-stu-id="d1fb2-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="d1fb2-180">FairPlay를 구성하는 방법에 대한 자세한 내용은 아래 샘플의 **ConfigureFairPlayPolicyOptions()** 메서드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-180">For details on how to configure FairPlay, see the **ConfigureFairPlayPolicyOptions()** method in the sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="d1fb2-181">일반적으로 인증과 ASK 집합 하나만 있기 때문에 FairPlay 정책 옵션은 한 번만 구성하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-181">Usually, you would want to configure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="d1fb2-182">제한(열기 또는 토큰).</span><span class="sxs-lookup"><span data-stu-id="d1fb2-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="d1fb2-183">키를 클라이언트에 배달하는 방법을 정의하는 키 배달 유형과 관련된 정보</span><span class="sxs-lookup"><span data-stu-id="d1fb2-183">Information specific to the key delivery type that defines how the key is delivered to the client.</span></span>
5. <span data-ttu-id="d1fb2-184">자산 배달 정책을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-184">Configure the asset delivery policy.</span></span> <span data-ttu-id="d1fb2-185">배달 정책 구성에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-185">The delivery policy configuration includes:</span></span>

   * <span data-ttu-id="d1fb2-186">배달 프로토콜(HLS)</span><span class="sxs-lookup"><span data-stu-id="d1fb2-186">The delivery protocol (HLS).</span></span>
   * <span data-ttu-id="d1fb2-187">동적 암호화 형식(일반 CBC 암호화)</span><span class="sxs-lookup"><span data-stu-id="d1fb2-187">The type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="d1fb2-188">라이선스 획득 URL</span><span class="sxs-lookup"><span data-stu-id="d1fb2-188">The license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="d1fb2-189">FairPlay와 다른 DRM(디지털 권한 관리) 시스템으로 암호화되는 스트림을 배달하려면 다음과 같은 별도의 배달 정책을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-189">If you want to deliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have to configure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="d1fb2-190">일반 암호화 (CENC) (PlayReady + Widevine)를 사용하여 DASH(Dynamic Adaptive Streaming over HTTP)를 구성하고, PlayReady를 사용하여 부드러운 스트리밍을 구성하는 하나의 IAssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="d1fb2-190">One IAssetDeliveryPolicy to configure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="d1fb2-191">HLS에 대한 FairPlay를 구성하기 위한 또 다른 IAssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="d1fb2-191">Another IAssetDeliveryPolicy to configure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="d1fb2-192">스트리밍 URL을 얻기 위해 주문형 로케이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-192">Create an OnDemand locator to get a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="d1fb2-193">플레이어 앱별 FairPlay 키 배달 사용</span><span class="sxs-lookup"><span data-stu-id="d1fb2-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="d1fb2-194">iOS SDK를 사용하여 플레이어 앱을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-194">You can develop player apps by using the iOS SDK.</span></span> <span data-ttu-id="d1fb2-195">FairPlay 콘텐츠를 재생하려면 라이선스 교환 프로토콜을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-195">To be able to play FairPlay content, you have to implement the license exchange protocol.</span></span> <span data-ttu-id="d1fb2-196">Apple에서는 이 프로토콜을 지정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="d1fb2-197">키 배달 요청을 전송하는 방법은 앱마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-197">It is up to each app how to send key delivery requests.</span></span> <span data-ttu-id="d1fb2-198">Media Services FairPlay 키 배달 서비스에서는 SPC가 다음 형식의 www-form-url 인코딩된 게시 메시지로 도착해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-198">The Media Services FairPlay key delivery service expects the SPC to come as a www-form-url encoded post message, in the following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="d1fb2-199">Azure 미디어 플레이어는 기본적으로 FairPlay 재생을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-199">Azure Media Player doesn’t support FairPlay playback out of the box.</span></span> <span data-ttu-id="d1fb2-200">Mac OS X에서 FairPlay를 재생하려면 Apple 개발자 계정에서 샘플 플레이어를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-200">To get FairPlay playback on MAC OS X, obtain the sample player from the Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="d1fb2-201">스트리밍 URL</span><span class="sxs-lookup"><span data-stu-id="d1fb2-201">Streaming URLs</span></span>
<span data-ttu-id="d1fb2-202">자산이 하나 이상의 DRM으로 암호화되어 있는 경우 스트리밍 URL에서 암호화 태그를 사용해야 합니다(형식='m3u8-aapl', 암호화='xxx').</span><span class="sxs-lookup"><span data-stu-id="d1fb2-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in the streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="d1fb2-203">고려 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-203">The following considerations apply:</span></span>

* <span data-ttu-id="d1fb2-204">1개 이하의 암호화 형식만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="d1fb2-205">하나의 암호화만 자산에 적용되었으면 URL에 암호화 형식을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-205">The encryption type doesn't have to be specified in the URL if only one encryption was applied to the asset.</span></span>
* <span data-ttu-id="d1fb2-206">암호화 형식은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-206">The encryption type is case insensitive.</span></span>
* <span data-ttu-id="d1fb2-207">다음과 같은 암호화 형식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-207">The following encryption types can be specified:</span></span>  
  * <span data-ttu-id="d1fb2-208">**cenc**: 일반 암호화(PlayReady 또는 Widevine)</span><span class="sxs-lookup"><span data-stu-id="d1fb2-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="d1fb2-209">**cbcs-aapl**: FairPlay</span><span class="sxs-lookup"><span data-stu-id="d1fb2-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="d1fb2-210">**cbc**: AES 봉투 암호화</span><span class="sxs-lookup"><span data-stu-id="d1fb2-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d1fb2-211">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="d1fb2-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="d1fb2-212">개발 환경을 설정하고 [.NET을 사용한 Media Services 환경](media-services-dotnet-how-to-use.md)에 설명된 대로 연결 정보를 사용하여 app.config 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-212">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="d1fb2-213">다음 요소를 app.config 파일에 정의된 **appSettings**에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-213">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="d1fb2-214">예제</span><span class="sxs-lookup"><span data-stu-id="d1fb2-214">Example</span></span>

<span data-ttu-id="d1fb2-215">다음 샘플에서는 Media Services를 사용하여 FairPlay로 암호화된 콘텐츠를 배달하는 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-215">The following sample demonstrates the ability to use Media Services to deliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="d1fb2-216">이 기능은 .NET 버전 3.6.0용 Azure Media Services SDK에서 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-216">This functionality was introduced in the Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="d1fb2-217">Program.cs 파일에 있는 코드를 이 섹션에 나와 있는 코드로 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-217">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="d1fb2-218">다른 AMS 정책(예: 로케이터 정책 또는 ContentKeyAuthorizationPolicy의 경우)은 1,000,000개의 정책으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="d1fb2-219">항상 같은 날짜/액세스 권한을 사용하는 경우(예: 비 업로드 정책처럼 오랫동안 배치되는 로케이터에 대한 정책) 동일한 정책 ID를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-219">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="d1fb2-220">자세한 내용은 [이 항목](media-services-dotnet-manage-entities.md#limit-access-policies) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="d1fb2-221">입력 파일이 있는 폴더를 가리키도록 변수를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1fb2-221">Make sure to update variables to point to folders where your input files are located.</span></span>

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
        // Read values from the App.config file.
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
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on the the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
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

            // Associate the key with the asset.
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

            // Associate the content key authorization policy with the content key.
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

            // Associate the content key authorization policy with the content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with the cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound to a real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key to generate the response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating the .pfx file.
            string pfxPassword = "<customer password for creating the .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key to generate the response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match the iv in the asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify the .pfx file created by the customer.
            var appCert = new X509Certificate2("path to the .pfx file created by the customer", pfxPassword, X509KeyStorageFlags.Exportable);

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

            // Get the FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // The reason the below code replaces "https://" with "skd://" is because
            // in the IOS player sample code which you obtained in Apple developer account,
            // the player only recognizes a Key URL that starts with skd://.
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

            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets the streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator to the streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL to the manifest file.
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


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="d1fb2-222">다음 단계: 미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="d1fb2-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d1fb2-223">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="d1fb2-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
