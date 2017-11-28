---
title: "aaaConfiguring 콘텐츠 보호 정책을 사용 하 여 hello Azure 포털 | Microsoft Docs"
description: "이 문서에서는 방법을 toouse hello Azure 포털 tooconfigure 콘텐츠 보호 정책 보여줍니다. hello 표시 방법을 문서도 tooenable 자산에 대 한 동적 암호화."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a><span data-ttu-id="697b0-104">Hello Azure 포털을 사용 하 여 콘텐츠 보호 정책 구성</span><span class="sxs-lookup"><span data-stu-id="697b0-104">Configuring content protection policies using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="697b0-105">toocomplete이이 자습서에서는 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="697b0-106">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="697b0-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="697b0-107">개요</span><span class="sxs-lookup"><span data-stu-id="697b0-107">Overview</span></span>
<span data-ttu-id="697b0-108">Microsoft Azure 미디어 서비스 AMS ()를 사용 하면 toosecure 하면 미디어를 저장, 처리 및 배달을 통해 컴퓨터를 벗어나 hello 시간.</span><span class="sxs-lookup"><span data-stu-id="697b0-108">Microsoft Azure Media Services (AMS) enables you toosecure your media from hello time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="697b0-109">미디어 서비스에서는 toodeliver 내용을 동적으로 AES로 암호화 된 고급 암호화 표준 () (128 비트 암호화 키 사용), PlayReady 및/또는 Widevine DRM 및 Apple FairPlay를 사용 하 여 일반 암호화 (CENC).</span><span class="sxs-lookup"><span data-stu-id="697b0-109">Media Services allows you toodeliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="697b0-110">AMS DRM 라이선스 배달용 서비스를 제공 하 고 AES 키 tooauthorized 클라이언트를 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-110">AMS provides a service for delivering DRM licenses and AES clear keys tooauthorized clients.</span></span> <span data-ttu-id="697b0-111">hello Azure 포털을 통해 있습니다 하나 toocreate **권한 부여 정책 키/라이선스** 모든 유형의 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-111">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="697b0-112">이 문서에서는 tooconfigure hello Azure 포털을 사용 하 여 보호 정책을 콘텐츠 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-112">This article demonstrates how tooconfigure content protection policies with hello Azure portal.</span></span> <span data-ttu-id="697b0-113">hello 표시 방법을 문서도 tooapply 동적 암호화 tooyour 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-113">hello article also shows how tooapply dynamic encryption tooyour assets.</span></span>


> [!NOTE]
> <span data-ttu-id="697b0-114">Hello 정책 hello Azure 클래식 포털 toocreate 보호 정책을 사용 하는 경우 hello에 나타나지 않을 수 있습니다 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-114">If you used hello Azure classic portal toocreate protection policies, hello policies may not appear in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="697b0-115">그러나 오래 된 모든 hello 정책을 여전히 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-115">However, all hello old polices still exist.</span></span> <span data-ttu-id="697b0-116">검사할 수 있습니다 Azure 미디어 서비스.NET SDK 또는 hello hello를 사용 하 여 [미디어 서비스 탐색기 Azure](https://github.com/Azure/Azure-Media-Services-Explorer/releases) 도구 (toosee hello 정책 hello 자산에 대해 마우스 오른쪽 단추로 클릭-> 디스플레이 탭 콘텐츠 키에 대해-> (F4) 정보 키를 누르거나 hello).</span><span class="sxs-lookup"><span data-stu-id="697b0-116">You can examine them using hello Azure Media Services .NET SDK or hello [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (toosee hello policies, right-click on hello asset -> Display information (F4)->click on Content keys tab-> click on hello key).</span></span> 
> 
> <span data-ttu-id="697b0-117">새 정책을 사용 하 여 자산 tooencrypt 하려는 경우 Azure 포털 hello로 구성 저장을 클릭 한 동적 암호화를 다시 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-117">If you want tooencrypt your asset using new policies, configure them with hello Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="697b0-118">콘텐츠 보호 구성 시작</span><span class="sxs-lookup"><span data-stu-id="697b0-118">Start configuring content protection</span></span>
<span data-ttu-id="697b0-119">콘텐츠 보호, 글로벌 tooyour AMS 계정 구성 toouse hello 포털 toostart 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-119">toouse hello portal toostart configuring content protection, global tooyour AMS account, do hello following:</span></span>

1. <span data-ttu-id="697b0-120">Hello에 [Azure 포털](https://portal.azure.com/)를 Azure 미디어 서비스 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="697b0-121">**설정** > **Content Protection**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-121">Select **Settings** > **Content protection**.</span></span>

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="697b0-123">키/라이선스 권한 부여 정책</span><span class="sxs-lookup"><span data-stu-id="697b0-123">Key/license authorization policy</span></span>
<span data-ttu-id="697b0-124">AMS는 키 또는 라이선스를 요청하는 사용자를 인증하는 여러 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="697b0-125">hello 콘텐츠 키 인증 정책은 구성 하 고 클라이언트 hello 키/라이선스 toobe delived toohello 클라이언트 하려면에서 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-125">hello content key authorization policy must be configured by you and met by your client in order for hello key/license toobe delived toohello client.</span></span> <span data-ttu-id="697b0-126">hello 콘텐츠 키 인증 정책이 있을 수 하나 이상의 권한 부여 제한을: **열고** 또는 **토큰** 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-126">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="697b0-127">hello Azure 포털을 통해 있습니다 하나 toocreate **권한 부여 정책 키/라이선스** 모든 유형의 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-127">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="697b0-128">열기</span><span class="sxs-lookup"><span data-stu-id="697b0-128">Open</span></span>
<span data-ttu-id="697b0-129">개방형 제한 의미 hello 시스템 키를 요청 하는 hello 키 tooanyone를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-129">Open restriction means that hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="697b0-130">이 제한은 테스트 목적으로 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="697b0-131">위임</span><span class="sxs-lookup"><span data-stu-id="697b0-131">Token</span></span>
<span data-ttu-id="697b0-132">보안 토큰 서비스 (STS)에서 발급 한 토큰 hello 토큰 제한 정책은 함께 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-132">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="697b0-133">미디어 서비스는 hello 단순 웹 토큰 (SWT) 형식 및 JSON 웹 토큰 (JWT) 형식 토큰을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-133">Media Services supports tokens in hello Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="697b0-134">미디어 서비스는 보안 토큰 서비스를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="697b0-135">사용자 지정 STS를 만들거나 Microsoft Azure ACS tooissue 토큰을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-135">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="697b0-136">hello STS 구성된 toocreate 지정 hello로 토큰에 서명 해야 합니다. 키 클레임을 발급 hello 토큰 제한 구성에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-136">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration.</span></span> <span data-ttu-id="697b0-137">hello 미디어 서비스 키 배달 서비스는 hello 요청한 키 (또는 라이선스) toohello 클라이언트 hello 토큰이 유효한 경우 및 hello 반환 hello 토큰 일치 항목에 구성 된 hello 키 (또는 라이선스)에 대 한 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-137">hello Media Services key delivery service will return hello requested key (or license) toohello client if hello token is valid and hello claims in hello token match those configured for hello key (or license).</span></span>

<span data-ttu-id="697b0-138">토큰 제한 정책 hello를 구성할 때 hello 기본 확인 키, 발급자 및 대상 매개 변수를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-138">When configuring hello token restricted policy, you must specify hello primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="697b0-139">hello hello 기본 확인 키가 포함 되어 hello 토큰이 서명, 발급자 hello 보안 토큰 서비스 hello 토큰을 발급 하는 키입니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-139">hello primary verification key contains hello key that hello token was signed with, issuer is hello secure token service that issues hello token.</span></span> <span data-ttu-id="697b0-140">hello 리소스 hello 토큰에 대 한 액세스 권한을 부여 또는 hello audience (범위 라고도 함) hello 토큰의 hello 의도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-140">hello audience (sometimes called scope) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="697b0-141">hello 미디어 서비스 키 배달 서비스는 hello 토큰의 이러한 값 hello 템플릿에서 hello 값과 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-141">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span>

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="697b0-143">PlayReady 권한 템플릿</span><span class="sxs-lookup"><span data-stu-id="697b0-143">PlayReady rights template</span></span>
<span data-ttu-id="697b0-144">Hello PlayReady 권한 서식 파일에 대 한 자세한 내용은 참조 하십시오. [미디어 서비스 PlayReady 라이선스 템플릿 개요](media-services-playready-license-template-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-144">For detailed information about hello PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="697b0-145">영구적</span><span class="sxs-lookup"><span data-stu-id="697b0-145">Non persistent</span></span>
<span data-ttu-id="697b0-146">비 영구적인로 라이선스를 구성 하는 경우 hello 플레이어 hello 라이선스를 사용 하는 동안 메모리에 보관만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-146">If you configure license as non-persistent, it is only held in memory while hello player is using hello license.</span></span>  

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="697b0-148">영구적</span><span class="sxs-lookup"><span data-stu-id="697b0-148">Persistent</span></span>
<span data-ttu-id="697b0-149">영구적으로 hello 라이선스를 구성 하는 경우 영구 저장소에 클라이언트 hello에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-149">If you configure hello license  as persistent, it is saved in persistent storage on hello client.</span></span>

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="697b0-151">Widevine 권한 템플릿</span><span class="sxs-lookup"><span data-stu-id="697b0-151">Widevine rights template</span></span>
<span data-ttu-id="697b0-152">Widevine 권한 템플릿 hello에 대 한 자세한 내용은 참조 하십시오. [Widevine 라이선스 템플릿 개요](media-services-widevine-license-template-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-152">For detailed information about hello Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="697b0-153">Basic</span><span class="sxs-lookup"><span data-stu-id="697b0-153">Basic</span></span>
<span data-ttu-id="697b0-154">선택 하는 경우 **기본**, 모든 값이 기본값 된 hello 서식 파일 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-154">When you select **Basic**, hello template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="697b0-155">고급</span><span class="sxs-lookup"><span data-stu-id="697b0-155">Advanced</span></span>
<span data-ttu-id="697b0-156">Widevine 구성의 고급 옵션에 대한 자세한 내용은 [이](media-services-widevine-license-template-overview.md) 토픽을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="697b0-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="697b0-158">FairPlay 구성</span><span class="sxs-lookup"><span data-stu-id="697b0-158">FairPlay configuration</span></span>
<span data-ttu-id="697b0-159">tooenable FairPlay 암호화 hello FairPlay 구성 옵션을 통해 tooprovide hello 앱 인증서 및 응용 프로그램 암호 키 (ASK) 필요.</span><span class="sxs-lookup"><span data-stu-id="697b0-159">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option.</span></span> <span data-ttu-id="697b0-160">FairPlay 구성 및 요구 사항에 대한 자세한 내용은 [이](media-services-protect-hls-with-fairplay.md) 문서를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="697b0-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a><span data-ttu-id="697b0-162">동적 암호화 tooyour 자산 적용</span><span class="sxs-lookup"><span data-stu-id="697b0-162">Apply dynamic encryption tooyour asset</span></span>
<span data-ttu-id="697b0-163">tootake 이점은 동적 암호화 해야 tooencode 소스 파일의 적응 비트 전송률 MP4 파일 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-163">tootake advantage of dynamic encryption, you need tooencode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-tooencrypt"></a><span data-ttu-id="697b0-164">자산 tooencrypt 않겠다고 선택</span><span class="sxs-lookup"><span data-stu-id="697b0-164">Select an asset that you want tooencrypt</span></span>
<span data-ttu-id="697b0-165">모든 자산을 선택 하는 toosee **설정** > **자산**합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-165">toosee all your assets, select **Settings** > **Assets**.</span></span>

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="697b0-167">AES 또는 DRM으로 암호화</span><span class="sxs-lookup"><span data-stu-id="697b0-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="697b0-168">자산에서 **암호화**를 누르면 **AES** 또는 **DRM**의 두 가지 선택 사항이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="697b0-169">AES</span><span class="sxs-lookup"><span data-stu-id="697b0-169">AES</span></span>
<span data-ttu-id="697b0-170">부드러운 스트리밍, HLS 및 MPEG-DASH의 모든 스트리밍 프로토콜에서 AES 암호화되지 않은 키 암호화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="697b0-172">DRM</span><span class="sxs-lookup"><span data-stu-id="697b0-172">DRM</span></span>
<span data-ttu-id="697b0-173">Hello DRM 탭을 선택 하면 콘텐츠 보호 정책의 다른 옵션과 함께 제공 됩니다 (있음 구성한 경우 이제) + 스트리밍 프로토콜의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-173">When you select hello DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="697b0-174">**MPEG-DASH를 사용하는 PlayReady 및 Widevine** - PlayReady 및 Widevine DRM의 MPEG-DASH 스트림을 동적으로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="697b0-175">**MPEG-DASH를 사용하는 PlayReady 및 Widevine + HLS를 사용하는 FairPlay** - PlayReady 및 Widevine DRM의 MPEG-DASH 스트림을 동적으로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="697b0-176">또한 FairPlay의 HLS 스트림도 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="697b0-177">**부드러운 스트리밍, HLS 및 MPEG-DASH만 사용하는 PlayReady** - PlayReady DRM의 부드러운 스트리밍, HLS, MPEG-DASH 스트림을 동적으로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="697b0-178">**MPEG-DASH만 사용하는 Widevine** - Widevine DRM의 MPEG-DASH를 동적으로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="697b0-179">**HLS만 사용하는 FairPlay** - FairPlay의 HLS 스트림을 동적으로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="697b0-180">tooenable FairPlay 암호화 hello hello 콘텐츠 보호 설정 블레이드의 FairPlay 구성 옵션을 통해 tooprovide hello 앱 인증서 및 응용 프로그램 암호 키 (ASK) 필요.</span><span class="sxs-lookup"><span data-stu-id="697b0-180">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option of hello Content Protection settings blade.</span></span>

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="697b0-182">Hello 암호화 선택 하면 키를 눌러 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-182">Once you make hello encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="697b0-183">AES 암호화 safari에서는 HLS tooplay 계획인 경우, 참조 [이 블로그](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/)합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-183">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="697b0-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="697b0-184">Next steps</span></span>
<span data-ttu-id="697b0-185">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="697b0-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="697b0-186">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="697b0-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

