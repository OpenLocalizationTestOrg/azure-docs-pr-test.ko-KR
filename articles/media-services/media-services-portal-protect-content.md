---
title: "Azure Portal을 사용하여 콘텐츠 보호 정책 구성 | Microsoft 문서"
description: "이 문서에서는 Azure Portal을 사용하여 콘텐츠 보호 정책을 구성하는 방법에 대해 설명합니다. 또한 자산에서 동적 암호화를 사용하도록 설정하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 67b3fa9936daebeafb7e87fe3a7b0c7e0105b3b3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-content-protection-policies-using-the-azure-portal"></a><span data-ttu-id="24bfd-104">Azure Portal을 사용하여 콘텐츠 보호 정책 구성</span><span class="sxs-lookup"><span data-stu-id="24bfd-104">Configuring content protection policies using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="24bfd-105">이 자습서를 완료하려면 Azure 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="24bfd-106">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24bfd-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="24bfd-107">개요</span><span class="sxs-lookup"><span data-stu-id="24bfd-107">Overview</span></span>
<span data-ttu-id="24bfd-108">Microsoft AMS(Azure Media Services)를 사용하면 사용자 컴퓨터에서 저장, 처리 및 배달에 이르는 과정 내내 미디어를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-108">Microsoft Azure Media Services (AMS) enables you to secure your media from the time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="24bfd-109">Media Services를 사용하면 AES(Advanced Encryption Standard, 128비트 암호화 키 사용) 및 PlayReady 및/또는 Widevine DRM을 사용하는 CENC(일반 암호화) 및 Apple FairPlay로 동적 암호화된 콘텐츠를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-109">Media Services allows you to deliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="24bfd-110">AMS는 DRM 라이선스 및 AES 암호화되지 않은 키를 인증된 클라이언트에 배달하는 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-110">AMS provides a service for delivering DRM licenses and AES clear keys to authorized clients.</span></span> <span data-ttu-id="24bfd-111">Azure Portal을 사용하면 모든 암호화 형식에 대해 **키/라이선스 권한 부여 정책** 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-111">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="24bfd-112">이 문서에서는 Azure Portal을 사용하여 콘텐츠 보호 정책을 구성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-112">This article demonstrates how to configure content protection policies with the Azure portal.</span></span> <span data-ttu-id="24bfd-113">또한 자산에 동적 암호화를 적용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-113">The article also shows how to apply dynamic encryption to your assets.</span></span>


> [!NOTE]
> <span data-ttu-id="24bfd-114">보호 정책을 Azure 클래식 포털을 사용하여 만든 경우 [Azure Portal](https://portal.azure.com/)에 나타나지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-114">If you used the Azure classic portal to create protection policies, the policies may not appear in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="24bfd-115">그러나 모든 이전 정책은 여전히 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-115">However, all the old polices still exist.</span></span> <span data-ttu-id="24bfd-116">해당 정책을 Azure Media Services .NET SDK 또는 [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) 도구를 사용하여 검사할 수 있습니다(정책을 보려면 자산을 마우스 오른쪽 단추로 클릭 -> 정보를 표시(F4) -> 콘텐츠 키 탭 클릭 -> 키 클릭).</span><span class="sxs-lookup"><span data-stu-id="24bfd-116">You can examine them using the Azure Media Services .NET SDK or the [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (to see the policies, right-click on the asset -> Display information (F4)->click on Content keys tab-> click on the key).</span></span> 
> 
> <span data-ttu-id="24bfd-117">새 정책을 사용하여 자산을 암호화하려는 경우 Azure Portal을 사용하여 구성하고, 저장을 클릭한 다음, 동적 암호화를 다시 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-117">If you want to encrypt your asset using new policies, configure them with the Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="24bfd-118">콘텐츠 보호 구성 시작</span><span class="sxs-lookup"><span data-stu-id="24bfd-118">Start configuring content protection</span></span>
<span data-ttu-id="24bfd-119">포털을 사용하여 AMS 계정 전역에 콘텐츠 보호 구성을 시작하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-119">To use the portal to start configuring content protection, global to your AMS account, do the following:</span></span>

1. <span data-ttu-id="24bfd-120">[Azure Portal](https://portal.azure.com/)에서 Azure Media Services 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="24bfd-121">**설정** > **Content Protection**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-121">Select **Settings** > **Content protection**.</span></span>

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="24bfd-123">키/라이선스 권한 부여 정책</span><span class="sxs-lookup"><span data-stu-id="24bfd-123">Key/license authorization policy</span></span>
<span data-ttu-id="24bfd-124">AMS는 키 또는 라이선스를 요청하는 사용자를 인증하는 여러 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="24bfd-125">콘텐츠 키 권한 부여 정책은 사용자가 구성해야 하며 이 키/라이선스를 클라이언트에 배달하기 위해서는 해당 클라이언트를 충족시켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-125">The content key authorization policy must be configured by you and met by your client in order for the key/license to be delived to the client.</span></span> <span data-ttu-id="24bfd-126">콘텐츠 키 권한 부여 정책에는 **열기** 또는 **토큰** 제한과 같은 하나 이상의 권한 부여 제한이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-126">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="24bfd-127">Azure Portal을 사용하면 모든 암호화 형식에 대해 **키/라이선스 권한 부여 정책** 을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-127">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="24bfd-128">열기</span><span class="sxs-lookup"><span data-stu-id="24bfd-128">Open</span></span>
<span data-ttu-id="24bfd-129">열기 제한은 시스템이 키를 요청하는 사람에게 키를 제공하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-129">Open restriction means that the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="24bfd-130">이 제한은 테스트 목적으로 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="24bfd-131">토큰</span><span class="sxs-lookup"><span data-stu-id="24bfd-131">Token</span></span>
<span data-ttu-id="24bfd-132">토큰 제한 정책은 보안 토큰 서비스(STS)에 의해 발급된 토큰이 수반되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-132">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="24bfd-133">미디어 서비스 지원 토큰에는 간단한 웹 토큰(SWT) 형식 및 JSON 웹 토큰(JWT) 형식의 토큰을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-133">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="24bfd-134">미디어 서비스는 보안 토큰 서비스를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="24bfd-135">사용자 지정 STS를 만들거나 Microsoft Azure ACS를 활용하여 토큰을 발급할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-135">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="24bfd-136">지정된 키로 서명된 토큰을 만들고 토큰 제한 구성에서 지정한 클레임을 발급하려면 반드시 STS를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-136">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration.</span></span> <span data-ttu-id="24bfd-137">토큰이 유효하고 해당 토큰의 클레임이 키(또는 라이선스)에 대해 구성된 클레임과 일치하는 경우 미디어 서비스 키 배달 서비스는 요청된 키(또는 라이선스)를 클라이언트에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-137">The Media Services key delivery service will return the requested key (or license) to the client if the token is valid and the claims in the token match those configured for the key (or license).</span></span>

<span data-ttu-id="24bfd-138">토큰 제한 정책을 구성하는 경우 기본 확인 키, 발급자 및 대상 매개 변수를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-138">When configuring the token restricted policy, you must specify the primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="24bfd-139">기본 확인 키는 토큰이 서명된 키를 포함하며 발급자는 토큰을 발행하는 보안 토큰 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-139">The primary verification key contains the key that the token was signed with, issuer is the secure token service that issues the token.</span></span> <span data-ttu-id="24bfd-140">청중(범위) 라고도 함)은 토큰의 의도 또는 토큰이 접근을 인증하는 대상 리소스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-140">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="24bfd-141">미디어 서비스 키 배달 서비스는 이러한 토큰의 값이 템플릿 파일에 있는 값과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-141">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span>

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="24bfd-143">PlayReady 권한 템플릿</span><span class="sxs-lookup"><span data-stu-id="24bfd-143">PlayReady rights template</span></span>
<span data-ttu-id="24bfd-144">PlayReady 권한 템플릿에 대한 자세한 내용은 [Media Services PlayReady 라이선스 템플릿 개요](media-services-playready-license-template-overview.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="24bfd-144">For detailed information about the PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="24bfd-145">영구적</span><span class="sxs-lookup"><span data-stu-id="24bfd-145">Non persistent</span></span>
<span data-ttu-id="24bfd-146">라이선스를 비영구적으로 구성하는 경우 플레이어가 라이선스를 사용하는 동안에는 메모리에 보관만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-146">If you configure license as non-persistent, it is only held in memory while the player is using the license.</span></span>  

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="24bfd-148">영구적</span><span class="sxs-lookup"><span data-stu-id="24bfd-148">Persistent</span></span>
<span data-ttu-id="24bfd-149">라이선스를 영구적으로 구성하는 경우 클라이언트의 영구 저장소에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-149">If you configure the license  as persistent, it is saved in persistent storage on the client.</span></span>

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="24bfd-151">Widevine 권한 템플릿</span><span class="sxs-lookup"><span data-stu-id="24bfd-151">Widevine rights template</span></span>
<span data-ttu-id="24bfd-152">Widevine 권한 템플릿에 대한 자세한 내용은 [Widevine 라이선스 템플릿 개요](media-services-widevine-license-template-overview.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="24bfd-152">For detailed information about the Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="24bfd-153">기본</span><span class="sxs-lookup"><span data-stu-id="24bfd-153">Basic</span></span>
<span data-ttu-id="24bfd-154">**기본**을 선택하면 템플릿이 모든 기본값으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-154">When you select **Basic**, the template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="24bfd-155">고급</span><span class="sxs-lookup"><span data-stu-id="24bfd-155">Advanced</span></span>
<span data-ttu-id="24bfd-156">Widevine 구성의 고급 옵션에 대한 자세한 내용은 [이](media-services-widevine-license-template-overview.md) 토픽을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="24bfd-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="24bfd-158">FairPlay 구성</span><span class="sxs-lookup"><span data-stu-id="24bfd-158">FairPlay configuration</span></span>
<span data-ttu-id="24bfd-159">FairPlay 암호화를 사용하려면 FairPlay 구성 옵션을 통해 응용 프로그램 인증서 및 ASK(Application Secret Key, 응용 프로그램 비밀 키)를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-159">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option.</span></span> <span data-ttu-id="24bfd-160">FairPlay 구성 및 요구 사항에 대한 자세한 내용은 [이](media-services-protect-hls-with-fairplay.md) 문서를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="24bfd-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-to-your-asset"></a><span data-ttu-id="24bfd-162">동적 암호화를 자산에 적용</span><span class="sxs-lookup"><span data-stu-id="24bfd-162">Apply dynamic encryption to your asset</span></span>
<span data-ttu-id="24bfd-163">동적 암호화를 활용하려면 소스 파일을 적응 비트 전송률 MP4 파일 집합으로 인코딩해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-163">To take advantage of dynamic encryption, you need to encode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-to-encrypt"></a><span data-ttu-id="24bfd-164">암호화하려는 자산을 선택</span><span class="sxs-lookup"><span data-stu-id="24bfd-164">Select an asset that you want to encrypt</span></span>
<span data-ttu-id="24bfd-165">모든 자산을 보려면 **설정** > **자산**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-165">To see all your assets, select **Settings** > **Assets**.</span></span>

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="24bfd-167">AES 또는 DRM으로 암호화</span><span class="sxs-lookup"><span data-stu-id="24bfd-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="24bfd-168">자산에서 **암호화**를 누르면 **AES** 또는 **DRM**의 두 가지 선택 사항이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="24bfd-169">AES</span><span class="sxs-lookup"><span data-stu-id="24bfd-169">AES</span></span>
<span data-ttu-id="24bfd-170">부드러운 스트리밍, HLS 및 MPEG-DASH의 모든 스트리밍 프로토콜에서 AES 암호화되지 않은 키 암호화를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="24bfd-172">DRM</span><span class="sxs-lookup"><span data-stu-id="24bfd-172">DRM</span></span>
<span data-ttu-id="24bfd-173">DRM 탭을 선택하면 콘텐츠 보호 정책(현재 구성되어 있어야 함) + 스트리밍 프로토콜 집합의 다른 선택 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-173">When you select the DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="24bfd-174">**MPEG-DASH를 사용하는 PlayReady 및 Widevine** - PlayReady 및 Widevine DRM의 MPEG-DASH 스트림을 동적으로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="24bfd-175">**MPEG-DASH를 사용하는 PlayReady 및 Widevine + HLS를 사용하는 FairPlay** - PlayReady 및 Widevine DRM의 MPEG-DASH 스트림을 동적으로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="24bfd-176">또한 FairPlay의 HLS 스트림도 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="24bfd-177">**부드러운 스트리밍, HLS 및 MPEG-DASH만 사용하는 PlayReady** - PlayReady DRM의 부드러운 스트리밍, HLS, MPEG-DASH 스트림을 동적으로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="24bfd-178">**MPEG-DASH만 사용하는 Widevine** - Widevine DRM의 MPEG-DASH를 동적으로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="24bfd-179">**HLS만 사용하는 FairPlay** - FairPlay의 HLS 스트림을 동적으로 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="24bfd-180">FairPlay 암호화를 사용하려면 Content Protection 설정 블레이드의 FairPlay 구성 옵션을 통해 응용 프로그램 인증서 및 ASK(Application Secret Key, 응용 프로그램 비밀 키)를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-180">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option of the Content Protection settings blade.</span></span>

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="24bfd-182">암호화를 선택한 후 **적용**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-182">Once you make the encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="24bfd-183">Safari에서 AES 암호화 HLS를 재생하려는 경우 [이 블로그](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24bfd-183">If you are planning to play an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="24bfd-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="24bfd-184">Next steps</span></span>
<span data-ttu-id="24bfd-185">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="24bfd-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="24bfd-186">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="24bfd-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

