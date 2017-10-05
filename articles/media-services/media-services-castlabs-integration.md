---
title: "castLabs를 사용하여 Azure Media Services에 Widevine 라이선스 제공 | Microsoft 문서"
description: "이 문서에서는 Azure 미디어 서비스(AMS)를 사용하여 PlayReady와 Widevine DRM이 모두 있는 AMS에서 동적으로 암호화된 스트림을 전달하는 방법을 설명합니다. PlayReady 라이선스는 미디어 서비스 PlayReady 라이선스 서버에서 제공되며 Widevine 라이선스는 castLabs 라이선스 서버에서 제공됩니다."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 5b69e804809f834e81221fb2787a997a52dbe286
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="using-castlabs-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="390cd-104">castLabs를 사용하여 Azure 미디어 서비스에 Widevine 라이선스 제공</span><span class="sxs-lookup"><span data-stu-id="390cd-104">Using castLabs to deliver Widevine licenses to Azure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="390cd-105">Axinom</span><span class="sxs-lookup"><span data-stu-id="390cd-105">Axinom</span></span>](media-services-axinom-integration.md)
> * [<span data-ttu-id="390cd-106">castLabs</span><span class="sxs-lookup"><span data-stu-id="390cd-106">castLabs</span></span>](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="390cd-107">개요</span><span class="sxs-lookup"><span data-stu-id="390cd-107">Overview</span></span>
<span data-ttu-id="390cd-108">이 문서에서는 Azure 미디어 서비스(AMS)를 사용하여 PlayReady와 Widevine DRM이 모두 있는 AMS에서 동적으로 암호화된 스트림을 전달하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-108">This article describes how you can use Azure Media Services (AMS) to deliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="390cd-109">PlayReady 라이선스는 미디어 서비스 PlayReady 라이선스 서버에서 제공되며 Widevine 라이선스는 **castLabs** 라이선스 서버에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-109">The PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="390cd-110">CENC(PlayReady 및/또는 Widevine)에 의해 보호되는 스트리밍 콘텐츠를 재생하려면 [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-110">To playback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="390cd-111">자세한 내용은 [AMP 문서](http://amp.azure.net/libs/amp/latest/docs/) 를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="390cd-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="390cd-112">다음 다이어그램은 고도의 Azure 미디어 서비스 및 castLabs 통합 아키텍처를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-112">The following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![통합](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="390cd-114">일반적인 시스템 설정</span><span class="sxs-lookup"><span data-stu-id="390cd-114">Typical system set up</span></span>
* <span data-ttu-id="390cd-115">미디어 콘텐츠는 AMS에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="390cd-116">콘텐츠 키의 키 ID는 castLabs 및 AMS에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="390cd-117">castLabs 및 AMS에는 모두 내장된 토큰 인증이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="390cd-118">다음 섹션에서는 인증 토큰에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-118">The following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="390cd-119">클라이언트가 비디오 스트리밍을 요청하면 콘텐츠는 **일반 암호화** (CENC)를 통해 동적으로 암호화되며 AMS는 부드러운 스트리밍 및 DASH로 동적으로 패키징됩니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-119">When a client requests to stream the video, the content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS to Smooth Streaming and DASH.</span></span> <span data-ttu-id="390cd-120">HLS 스트리밍 프로토콜에 대한 PlayReady M2TS 기본 스트림 암호화를 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="390cd-121">PlayReady 라이선스는 AMS 라이선스 서버에서 검색되고 Widevine 라이선스는 castLabs 라이선스 서버에서 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="390cd-122">Media Player는 클라이언트 플랫폼 기능에 따라 가져올 라이선스를 자동으로 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-122">Media Player automatically decides which license to fetch based on the client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="390cd-123">라이선스를 가져오기 위한 인증 토큰 생성</span><span class="sxs-lookup"><span data-stu-id="390cd-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="390cd-124">castLabs 및 AMS는 둘 다 라이선스를 인증하는 데 사용되는 JWT(JSON 웹 토큰) 토큰 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-124">Both castLabs and AMS support JWT (JSON Web Token) token format used to authorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="390cd-125">AMS의 JWT 토큰</span><span class="sxs-lookup"><span data-stu-id="390cd-125">JWT token in AMS</span></span>
<span data-ttu-id="390cd-126">다음 표에서는 AMS의 JWT 토큰을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-126">The following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="390cd-127">발급자</span><span class="sxs-lookup"><span data-stu-id="390cd-127">Issuer</span></span> | <span data-ttu-id="390cd-128">선택한 STS(보안 토큰 서비스)의 발급자 문자열</span><span class="sxs-lookup"><span data-stu-id="390cd-128">Issuer string from the chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="390cd-129">대상</span><span class="sxs-lookup"><span data-stu-id="390cd-129">Audience</span></span> |<span data-ttu-id="390cd-130">사용된 STS의 대상 문자열</span><span class="sxs-lookup"><span data-stu-id="390cd-130">Audience string from the used STS</span></span> |
| <span data-ttu-id="390cd-131">클레임</span><span class="sxs-lookup"><span data-stu-id="390cd-131">Claims</span></span> |<span data-ttu-id="390cd-132">클레임 집합</span><span class="sxs-lookup"><span data-stu-id="390cd-132">A set of claims</span></span> |
| <span data-ttu-id="390cd-133">NotBefore</span><span class="sxs-lookup"><span data-stu-id="390cd-133">NotBefore</span></span> |<span data-ttu-id="390cd-134">토큰의 시작 유효성</span><span class="sxs-lookup"><span data-stu-id="390cd-134">Start validity of the token</span></span> |
| <span data-ttu-id="390cd-135">만료</span><span class="sxs-lookup"><span data-stu-id="390cd-135">Expires</span></span> |<span data-ttu-id="390cd-136">토큰의 종료 유효성</span><span class="sxs-lookup"><span data-stu-id="390cd-136">End validity of the token</span></span> |
| <span data-ttu-id="390cd-137">SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="390cd-137">SigningCredentials</span></span> |<span data-ttu-id="390cd-138">PlayReady 라이선스 서버, castLabs 라이선스 서버 및 STS 간에 공유되는 키로, 대칭 또는 비대칭 키일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-138">The key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="390cd-139">castLabs의 JWT 토큰</span><span class="sxs-lookup"><span data-stu-id="390cd-139">JWT token in castLabs</span></span>
<span data-ttu-id="390cd-140">다음 표에서는 castLabs의 JWT 토큰을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-140">The following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="390cd-141">이름</span><span class="sxs-lookup"><span data-stu-id="390cd-141">Name</span></span> | <span data-ttu-id="390cd-142">설명</span><span class="sxs-lookup"><span data-stu-id="390cd-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="390cd-143">optData</span><span class="sxs-lookup"><span data-stu-id="390cd-143">optData</span></span> |<span data-ttu-id="390cd-144">사용자에 대한 정보가 포함된 JSON 문자열.</span><span class="sxs-lookup"><span data-stu-id="390cd-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="390cd-145">crt</span><span class="sxs-lookup"><span data-stu-id="390cd-145">crt</span></span> |<span data-ttu-id="390cd-146">자산, 해당 자산의 라이선스 정보 및 재생 권한에 대한 정보가 포함된 JSON 문자열.</span><span class="sxs-lookup"><span data-stu-id="390cd-146">A JSON string containing information about the asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="390cd-147">iat</span><span class="sxs-lookup"><span data-stu-id="390cd-147">iat</span></span> |<span data-ttu-id="390cd-148">Epoch의 현재 날짜/시간.</span><span class="sxs-lookup"><span data-stu-id="390cd-148">The current datetime in epoch.</span></span> |
| <span data-ttu-id="390cd-149">jti</span><span class="sxs-lookup"><span data-stu-id="390cd-149">jti</span></span> |<span data-ttu-id="390cd-150">이 토큰에 대한 고유 식별자(모든 토큰은 castLabs 시스템에서 한 번만 사용할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="390cd-150">A unique identifier about this token (every token can only be used once in the castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="390cd-151">샘플 솔루션 설정</span><span class="sxs-lookup"><span data-stu-id="390cd-151">Sample solution set up</span></span>
<span data-ttu-id="390cd-152">[샘플 솔루션](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) 은 다음 두 프로젝트로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-152">The [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="390cd-153">PlayReady 및 Widevine에 대해 이미 수집된 자산에 DRM 제한을 설정하는 데 사용할 수 있는 콘솔 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="390cd-153">A console app that can be used to set DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="390cd-154">토큰을 배포하는 웹 응용 프로그램. STS의 간소화된 버전으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="390cd-155">콘솔 응용 프로그램을 사용하려면</span><span class="sxs-lookup"><span data-stu-id="390cd-155">To use the console application:</span></span>

1. <span data-ttu-id="390cd-156">app.config를 변경하여 AMS 자격 증명, castLabs 자격 증명, STS 구성 및 공유 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-156">Change the app.config to setup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="390cd-157">AMS에 자산을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="390cd-158">업로드된 자산에서 UUID를 가져오고 Program.cs 파일의 32행을 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-158">Get the UUID from the uploaded Asset, and change Line 32 in the Program.cs file:</span></span>
   
      <span data-ttu-id="390cd-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="390cd-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="390cd-160">castLabs 시스템에서 AssetId를 사용하여 자산의 이름을 지정합니다(Program.cs 파일의 44행).</span><span class="sxs-lookup"><span data-stu-id="390cd-160">Use an AssetId for naming the asset in the castLabs system (Line 44 in the Program.cs file).</span></span>
   
   <span data-ttu-id="390cd-161">**castLabs**에 대해 AssetId를 설정해야 하며, 고유한 영숫자 문자열로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-161">You must set AssetId for **castLabs**; it needs to be a unique alphanumeric string.</span></span>
5. <span data-ttu-id="390cd-162">프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-162">Run the program.</span></span>

<span data-ttu-id="390cd-163">웹 응용 프로그램(STS)을 사용하려면</span><span class="sxs-lookup"><span data-stu-id="390cd-163">To use the Web Application (STS):</span></span>

1. <span data-ttu-id="390cd-164">web.config를 변경하여 castlabs 판매자 ID, STS 구성 및 공유 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-164">Change the web.config to setup castlabs merchant ID, the STS configuration and the shared key.</span></span>
2. <span data-ttu-id="390cd-165">Azure 웹 사이트에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-165">Deploy to Azure Websites.</span></span>
3. <span data-ttu-id="390cd-166">웹 사이트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-166">Navigate to the website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="390cd-167">비디오 재생</span><span class="sxs-lookup"><span data-stu-id="390cd-167">Playing back a video</span></span>
<span data-ttu-id="390cd-168">일반 암호화(PlayReady 및/또는 Widevine)를 사용하여 암호화된 비디오를 재생할 때는 [Azure 미디어 플레이어](http://amsplayer.azurewebsites.net/azuremediaplayer.html)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-168">To playback a video encrypted with common encryption (PlayReady and/or Widevine), you can use the [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="390cd-169">콘솔 앱을 실행하는 경우 콘텐츠 키 ID와 매니페스트 URL이 화면에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-169">When running the console app, the Content Key ID and the Manifest URL are echoed.</span></span>

1. <span data-ttu-id="390cd-170">새 탭을 열고 STS를 시작합니다(http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid]).</span><span class="sxs-lookup"><span data-stu-id="390cd-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="390cd-171">[Azure 미디어 플레이어](http://amsplayer.azurewebsites.net/azuremediaplayer.html)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-171">Go to [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="390cd-172">스트리밍 URL에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-172">Paste in the streaming URL.</span></span>
4. <span data-ttu-id="390cd-173">**고급 옵션** 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-173">Click the **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="390cd-174">**보호** 드롭다운에서 PlayReady 및/또는 Widevine를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-174">In the **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="390cd-175">STS에서 가져온 토큰을 토큰 텍스트 상자에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-175">Paste the token that you got from your STS in the Token textbox.</span></span> 
   
   <span data-ttu-id="390cd-176">castLab 라이선스 서버는 토큰 앞에 "Bearer =" 접두사가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-176">The castLab license server does not need the “Bearer=” prefix in front of the token.</span></span> <span data-ttu-id="390cd-177">따라서 토큰을 제출하기 전에 제거하세요.</span><span class="sxs-lookup"><span data-stu-id="390cd-177">So please remove that before submitting the token.</span></span>
7. <span data-ttu-id="390cd-178">플레이어를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-178">Update the player.</span></span>
8. <span data-ttu-id="390cd-179">비디오가 재생됩니다.</span><span class="sxs-lookup"><span data-stu-id="390cd-179">The video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="390cd-180">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="390cd-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="390cd-181">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="390cd-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

