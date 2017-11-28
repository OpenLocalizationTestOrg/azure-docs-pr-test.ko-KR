---
title: "aaaUsing castLabs toodeliver Widevine 라이선스 tooAzure 미디어 서비스 | Microsoft Docs"
description: "이 문서에서는 Azure 미디어 서비스 (AMS) toodeliver PlayReady와 Widevine DRMs AMS 하 여 동적으로 암호화 된 스트림을 사용 하는 방법을 설명 합니다. 미디어 서비스 PlayReady 라이선스 서버에서 가져온 hello PlayReady 라이선스 및 Widevine 라이선스 castLabs 라이선스 서버에 의해 전달 됩니다."
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
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="41aac-104">CastLabs toodeliver Widevine 라이선스 tooAzure 미디어 서비스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="41aac-104">Using castLabs toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="41aac-105">Axinom</span><span class="sxs-lookup"><span data-stu-id="41aac-105">Axinom</span></span>](media-services-axinom-integration.md)
> * [<span data-ttu-id="41aac-106">castLabs</span><span class="sxs-lookup"><span data-stu-id="41aac-106">castLabs</span></span>](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="41aac-107">개요</span><span class="sxs-lookup"><span data-stu-id="41aac-107">Overview</span></span>
<span data-ttu-id="41aac-108">이 문서에서는 Azure 미디어 서비스 (AMS) toodeliver PlayReady와 Widevine DRMs AMS 하 여 동적으로 암호화 된 스트림을 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-108">This article describes how you can use Azure Media Services (AMS) toodeliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="41aac-109">Widevine 라이선스에서 제공 하 고 hello PlayReady 라이선스 미디어 서비스 PlayReady 라이선스 서버에서 가져오는데 **castLabs** 라이선스 서버.</span><span class="sxs-lookup"><span data-stu-id="41aac-109">hello PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="41aac-110">보호 된 콘텐츠 스트리밍 tooplayback CENC (PlayReady 및/또는 Widevine), 여는 데 [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-110">tooplayback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="41aac-111">자세한 내용은 [AMP 문서](http://amp.azure.net/libs/amp/latest/docs/) 를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="41aac-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="41aac-112">다음 다이어그램 hello 높은 수준의 Azure 미디어 서비스 및 castLabs 통합 아키텍처를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-112">hello following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![통합](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="41aac-114">일반적인 시스템 설정</span><span class="sxs-lookup"><span data-stu-id="41aac-114">Typical system set up</span></span>
* <span data-ttu-id="41aac-115">미디어 콘텐츠는 AMS에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="41aac-116">콘텐츠 키의 키 ID는 castLabs 및 AMS에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="41aac-117">castLabs 및 AMS에는 모두 내장된 토큰 인증이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="41aac-118">다음 섹션 hello 인증 토큰에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-118">hello following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="41aac-119">Hello 콘텐츠가 동적으로 암호화 된 클라이언트 toostream hello 비디오를 요청 하면 **일반 암호화** (CENC) 및 스트리밍 및 DASH AMS tooSmooth 하 여 동적으로 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-119">When a client requests toostream hello video, hello content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS tooSmooth Streaming and DASH.</span></span> <span data-ttu-id="41aac-120">HLS 스트리밍 프로토콜에 대한 PlayReady M2TS 기본 스트림 암호화를 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="41aac-121">PlayReady 라이선스는 AMS 라이선스 서버에서 검색되고 Widevine 라이선스는 castLabs 라이선스 서버에서 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="41aac-122">미디어 플레이어는 어떤 라이선스 toofetch hello 클라이언트 플랫폼 기능에 따라 자동으로 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-122">Media Player automatically decides which license toofetch based on hello client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="41aac-123">라이선스를 가져오기 위한 인증 토큰 생성</span><span class="sxs-lookup"><span data-stu-id="41aac-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="41aac-124">CastLabs 및 AMS 둘 다 사용 하는 토큰 형식을 tooauthorize 라이선스 JWT (JSON 웹 토큰)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-124">Both castLabs and AMS support JWT (JSON Web Token) token format used tooauthorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="41aac-125">AMS의 JWT 토큰</span><span class="sxs-lookup"><span data-stu-id="41aac-125">JWT token in AMS</span></span>
<span data-ttu-id="41aac-126">다음 표에서 hello AMS에서 JWT 토큰을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-126">hello following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="41aac-127">발급자</span><span class="sxs-lookup"><span data-stu-id="41aac-127">Issuer</span></span> | <span data-ttu-id="41aac-128">발급자 문자열 hello에서 선택한 서비스 STS (보안 토큰)</span><span class="sxs-lookup"><span data-stu-id="41aac-128">Issuer string from hello chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="41aac-129">대상</span><span class="sxs-lookup"><span data-stu-id="41aac-129">Audience</span></span> |<span data-ttu-id="41aac-130">STS를 사용 하는 hello에서 대상 그룹 문자열</span><span class="sxs-lookup"><span data-stu-id="41aac-130">Audience string from hello used STS</span></span> |
| <span data-ttu-id="41aac-131">클레임</span><span class="sxs-lookup"><span data-stu-id="41aac-131">Claims</span></span> |<span data-ttu-id="41aac-132">클레임 집합</span><span class="sxs-lookup"><span data-stu-id="41aac-132">A set of claims</span></span> |
| <span data-ttu-id="41aac-133">NotBefore</span><span class="sxs-lookup"><span data-stu-id="41aac-133">NotBefore</span></span> |<span data-ttu-id="41aac-134">Hello 토큰의 유효성을 검사를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-134">Start validity of hello token</span></span> |
| <span data-ttu-id="41aac-135">만료</span><span class="sxs-lookup"><span data-stu-id="41aac-135">Expires</span></span> |<span data-ttu-id="41aac-136">Hello 토큰의 끝 유효성</span><span class="sxs-lookup"><span data-stu-id="41aac-136">End validity of hello token</span></span> |
| <span data-ttu-id="41aac-137">SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="41aac-137">SigningCredentials</span></span> |<span data-ttu-id="41aac-138">라이선스 서버 및 STS를 castLabs PlayReady 라이선스 서버 간에 공유 되는 hello 키 대칭 또는 비대칭 키 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-138">hello key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="41aac-139">castLabs의 JWT 토큰</span><span class="sxs-lookup"><span data-stu-id="41aac-139">JWT token in castLabs</span></span>
<span data-ttu-id="41aac-140">다음 표에서 hello castLabs에서 JWT 토큰을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-140">hello following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="41aac-141">이름</span><span class="sxs-lookup"><span data-stu-id="41aac-141">Name</span></span> | <span data-ttu-id="41aac-142">설명</span><span class="sxs-lookup"><span data-stu-id="41aac-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="41aac-143">optData</span><span class="sxs-lookup"><span data-stu-id="41aac-143">optData</span></span> |<span data-ttu-id="41aac-144">사용자에 대한 정보가 포함된 JSON 문자열.</span><span class="sxs-lookup"><span data-stu-id="41aac-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="41aac-145">crt</span><span class="sxs-lookup"><span data-stu-id="41aac-145">crt</span></span> |<span data-ttu-id="41aac-146">JSON 문자열 대 한 정보가 들어 hello 자산, 라이선스 정보 및 재생 권한을 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-146">A JSON string containing information about hello asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="41aac-147">iat</span><span class="sxs-lookup"><span data-stu-id="41aac-147">iat</span></span> |<span data-ttu-id="41aac-148">hello epoch의 현재 datetime입니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-148">hello current datetime in epoch.</span></span> |
| <span data-ttu-id="41aac-149">jti</span><span class="sxs-lookup"><span data-stu-id="41aac-149">jti</span></span> |<span data-ttu-id="41aac-150">(모든 토큰 수 번만 사용할 hello castLabs 시스템에서)이이 토큰에 대 한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-150">A unique identifier about this token (every token can only be used once in hello castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="41aac-151">샘플 솔루션 설정</span><span class="sxs-lookup"><span data-stu-id="41aac-151">Sample solution set up</span></span>
<span data-ttu-id="41aac-152">hello [샘플 솔루션](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) 두 개의 프로젝트로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-152">hello [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="41aac-153">PlayReady 및 Widevine 모두에 대해 이미 수집 된 자산에 사용 되는 tooset DRM 제한 될 수 있는 콘솔 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-153">A console app that can be used tooset DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="41aac-154">토큰을 배포하는 웹 응용 프로그램. STS의 간소화된 버전으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="41aac-155">toouse hello 콘솔 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="41aac-155">toouse hello console application:</span></span>

1. <span data-ttu-id="41aac-156">Hello app.config toosetup AMS 자격 증명, castLabs 자격 증명, STS 구성 및 공유 키를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-156">Change hello app.config toosetup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="41aac-157">AMS에 자산을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="41aac-158">Get hello UUID hello에서 자산을 업로드 하 고 hello Program.cs 파일의 선을 32를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-158">Get hello UUID from hello uploaded Asset, and change Line 32 in hello Program.cs file:</span></span>
   
      <span data-ttu-id="41aac-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="41aac-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="41aac-160">Hello castLabs 시스템 (hello Program.cs 파일의 선을 44) hello 자산에는 AssetId를 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="41aac-160">Use an AssetId for naming hello asset in hello castLabs system (Line 44 in hello Program.cs file).</span></span>
   
   <span data-ttu-id="41aac-161">에 대 한 AssetId 설정 해야 **castLabs**; toobe 고유한 영숫자 문자열 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-161">You must set AssetId for **castLabs**; it needs toobe a unique alphanumeric string.</span></span>
5. <span data-ttu-id="41aac-162">Hello 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-162">Run hello program.</span></span>

<span data-ttu-id="41aac-163">toouse hello 웹 응용 프로그램 (STS):</span><span class="sxs-lookup"><span data-stu-id="41aac-163">toouse hello Web Application (STS):</span></span>

1. <span data-ttu-id="41aac-164">변경 hello web.config toosetup castlabs merchant ID, STS 구성 hello 및 hello 공유 키.</span><span class="sxs-lookup"><span data-stu-id="41aac-164">Change hello web.config toosetup castlabs merchant ID, hello STS configuration and hello shared key.</span></span>
2. <span data-ttu-id="41aac-165">TooAzure 웹 사이트를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-165">Deploy tooAzure Websites.</span></span>
3. <span data-ttu-id="41aac-166">Toohello 웹 사이트를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-166">Navigate toohello website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="41aac-167">비디오 재생</span><span class="sxs-lookup"><span data-stu-id="41aac-167">Playing back a video</span></span>
<span data-ttu-id="41aac-168">hello를 사용할 수 있습니다, tooplayback (PlayReady 및/또는 Widevine) 일반 암호화를 사용 하 여 암호화 된 비디오 [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-168">tooplayback a video encrypted with common encryption (PlayReady and/or Widevine), you can use hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="41aac-169">Hello 콘솔 응용 프로그램을 실행할 때 hello 콘텐츠 키 ID 및 URL 매니페스트 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-169">When running hello console app, hello Content Key ID and hello Manifest URL are echoed.</span></span>

1. <span data-ttu-id="41aac-170">새 탭을 열고 STS를 시작합니다(http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid]).</span><span class="sxs-lookup"><span data-stu-id="41aac-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="41aac-171">너무 이동[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-171">Go too[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="41aac-172">스트리밍 URL hello에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-172">Paste in hello streaming URL.</span></span>
4. <span data-ttu-id="41aac-173">Hello 클릭 **고급 옵션** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-173">Click hello **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="41aac-174">Hello에 **보호** 드롭다운에서 PlayReady 및/또는 Widevine 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-174">In hello **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="41aac-175">Hello 토큰 텍스트 상자에 STS에서 가져온 hello 토큰을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-175">Paste hello token that you got from your STS in hello Token textbox.</span></span> 
   
   <span data-ttu-id="41aac-176">hello castLab 라이선스 서버는 hello 않아도 "전달자 =" hello 토큰 앞에 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-176">hello castLab license server does not need hello “Bearer=” prefix in front of hello token.</span></span> <span data-ttu-id="41aac-177">따라서 하는 hello 토큰을 제출 하기 전에 제거 하세요.</span><span class="sxs-lookup"><span data-stu-id="41aac-177">So please remove that before submitting hello token.</span></span>
7. <span data-ttu-id="41aac-178">Hello 플레이어를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-178">Update hello player.</span></span>
8. <span data-ttu-id="41aac-179">hello 비디오를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41aac-179">hello video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="41aac-180">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="41aac-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="41aac-181">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="41aac-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

