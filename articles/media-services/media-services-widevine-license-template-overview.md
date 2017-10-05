---
title: "Widevine 라이선스 템플릿 개요 | Microsoft Docs"
description: "이 토픽에서는 Widevine 라이선스를 구성하는 데 사용되는 Widevine 라이선스 템플릿의 개요를 제공합니다."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0e6f1f05-7ed6-4ed6-82a0-0cc2182b075a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 667ff16dc7608dab2a5b8b1fd7df715da4620ca1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="widevine-license-template-overview"></a><span data-ttu-id="1fcb0-103">Widevine 라이선스 템플릿 개요</span><span class="sxs-lookup"><span data-stu-id="1fcb0-103">Widevine license template overview</span></span>
## <a name="overview"></a><span data-ttu-id="1fcb0-104">개요</span><span class="sxs-lookup"><span data-stu-id="1fcb0-104">Overview</span></span>
<span data-ttu-id="1fcb0-105">이제 Azure 미디어 서비스를 사용하면 Widevine 라이선스를 요청하고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-105">Azure Media Services now enables you to configure and request Widevine licenses.</span></span> <span data-ttu-id="1fcb0-106">최종 사용자 플레이어가 Widevine으로 보호된 콘텐츠를 재생하려고 하면 라이선스 배달 서비스로 요청을 보내 라이선스를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-106">When the end user player tries to play your Widevine protected content, a request is sent to the license delivery service to obtain a license.</span></span> <span data-ttu-id="1fcb0-107">라이선스 서비스에서 요청을 승인하면 클라이언트로 전송하여 지정된 콘텐츠의 암호를 해독하고 재생하는 데 사용할 수 있는 라이선스가 발급됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-107">If the license service approves the request, it issues the license which is sent to the client and can be used to decrypt and play the specified content.</span></span>

<span data-ttu-id="1fcb0-108">Widevine 라이선스 요청 형식은 JSON 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-108">Widevine license request is formatted as a JSON message.</span></span>  

>[!NOTE]
> <span data-ttu-id="1fcb0-109">"{}"로 값이 없는 빈 메시지를 만들도록 선택할 수 있으며 모든 기본값이 포함된 라이선스 템플릿이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-109">You can choose to create an empty message with no values just "{}" and a license template will be created with all defaults.</span></span> <span data-ttu-id="1fcb0-110">기본값은 대부분의 경우 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-110">The default works for most cases.</span></span> <span data-ttu-id="1fcb0-111">예를 들어 MS 기반 라이선스 배달 시나리오에서도 항상 기본값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-111">For example, for MS based license delivery scenarios that should always be default.</span></span> <span data-ttu-id="1fcb0-112">"provider" 및 "content_id" 값을 설정해야 하는 경우 공급자가 Google의 Widevine 자격 증명과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-112">If you do need to set the "provider" and "content_id" values, a provider must match Google's Widevine credentials.</span></span>

    {  
       “payload”:“<license challenge>”,
       “content_id”: “<content id>” 
       “provider”: ”<provider>”
       “allowed_track_types”:“<types>”,
       “content_key_specs”:[  
          {  
             “track_type”:“<track type 1>”
          },
          {  
             “track_type”:“<track type 2>”
          },
          …
       ],
       “policy_overrides”:{  
          “can_play”:<can play>,
          “can persist”:<can persist>,
          “can_renew”:<can renew>,
          “rental_duration_seconds”:<rental duration>,
          “playback_duration_seconds”:<playback duration>,
          “license_duration_seconds”:<license duration>,
          “renewal_recovery_duration_seconds”:<renewal recovery duration>,
          “renewal_server_url”:”<renewal server url>”,
          “renewal_delay_seconds”:<renewal delay>,
          “renewal_retry_interval_seconds”:<renewal retry interval>,
          “renew_with_usage”:<renew with usage>
       }
    }

## <a name="json-message"></a><span data-ttu-id="1fcb0-113">JSON 메시지</span><span class="sxs-lookup"><span data-stu-id="1fcb0-113">JSON message</span></span>
| <span data-ttu-id="1fcb0-114">이름</span><span class="sxs-lookup"><span data-stu-id="1fcb0-114">Name</span></span> | <span data-ttu-id="1fcb0-115">값</span><span class="sxs-lookup"><span data-stu-id="1fcb0-115">Value</span></span> | <span data-ttu-id="1fcb0-116">설명</span><span class="sxs-lookup"><span data-stu-id="1fcb0-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1fcb0-117">payload</span><span class="sxs-lookup"><span data-stu-id="1fcb0-117">payload</span></span> |<span data-ttu-id="1fcb0-118">Base64 인코딩된 문자열</span><span class="sxs-lookup"><span data-stu-id="1fcb0-118">Base64 encoded string</span></span> |<span data-ttu-id="1fcb0-119">클라이언트에서 보낸 라이선스 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-119">The license request sent by a client.</span></span> |
| <span data-ttu-id="1fcb0-120">content_id</span><span class="sxs-lookup"><span data-stu-id="1fcb0-120">content_id</span></span> |<span data-ttu-id="1fcb0-121">Base64 인코딩된 문자열</span><span class="sxs-lookup"><span data-stu-id="1fcb0-121">Base64 encoded string</span></span> |<span data-ttu-id="1fcb0-122">각 content_key_specs.track_type에 대한 KeyId 및 콘텐츠 키를 파생시키는 데 사용되는 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-122">Identifier used to derive KeyId(s) and Content Key(s) for each content_key_specs.track_type.</span></span> |
| <span data-ttu-id="1fcb0-123">provider</span><span class="sxs-lookup"><span data-stu-id="1fcb0-123">provider</span></span> |<span data-ttu-id="1fcb0-124">string</span><span class="sxs-lookup"><span data-stu-id="1fcb0-124">string</span></span> |<span data-ttu-id="1fcb0-125">콘텐츠 키 및 정책을 조회하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-125">Used to look up content keys and policies.</span></span> <span data-ttu-id="1fcb0-126">MS 키 배달이 Widevine 라이선스 배달에 사용되는 경우 이 매개 변수는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-126">If MS key delivery is used for Widevine license delivery, this parameter is ignored.</span></span> |
| <span data-ttu-id="1fcb0-127">policy_name</span><span class="sxs-lookup"><span data-stu-id="1fcb0-127">policy_name</span></span> |<span data-ttu-id="1fcb0-128">string</span><span class="sxs-lookup"><span data-stu-id="1fcb0-128">string</span></span> |<span data-ttu-id="1fcb0-129">이전에 등록된 정책의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-129">Name of a previously registered policy.</span></span> <span data-ttu-id="1fcb0-130">옵션</span><span class="sxs-lookup"><span data-stu-id="1fcb0-130">Optional</span></span> |
| <span data-ttu-id="1fcb0-131">allowed_track_types</span><span class="sxs-lookup"><span data-stu-id="1fcb0-131">allowed_track_types</span></span> |<span data-ttu-id="1fcb0-132">enum</span><span class="sxs-lookup"><span data-stu-id="1fcb0-132">enum</span></span> |<span data-ttu-id="1fcb0-133">SD_ONLY 또는 SD_HD.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-133">SD_ONLY or SD_HD.</span></span> <span data-ttu-id="1fcb0-134">라이선스에 포함할 콘텐츠 키를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-134">Controls which content keys should be included in a license</span></span> |
| <span data-ttu-id="1fcb0-135">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="1fcb0-135">content_key_specs</span></span> |<span data-ttu-id="1fcb0-136">JSON 구조 배열. 아래 **콘텐츠 키 사양** 참조</span><span class="sxs-lookup"><span data-stu-id="1fcb0-136">array of JSON structures, see **Content Key Specs** below</span></span> |<span data-ttu-id="1fcb0-137">반환할 콘텐츠 키에 대한 보다 세분화된 제어.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-137">A finer grained control on what content keys to return.</span></span> <span data-ttu-id="1fcb0-138">자세한 내용은 아래 콘텐츠 키 사양을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-138">See Content Key Spec below for details.</span></span>  <span data-ttu-id="1fcb0-139">Allowed_track_types 및 content_key_specs 중 하나만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-139">Only one of allowed_track_types and content_key_specs can be specified.</span></span> |
| <span data-ttu-id="1fcb0-140">use_policy_overrides_exclusively</span><span class="sxs-lookup"><span data-stu-id="1fcb0-140">use_policy_overrides_exclusively</span></span> |<span data-ttu-id="1fcb0-141">boolean.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-141">boolean.</span></span> <span data-ttu-id="1fcb0-142">true 또는 false</span><span class="sxs-lookup"><span data-stu-id="1fcb0-142">true or false</span></span> |<span data-ttu-id="1fcb0-143">policy_overrides로 지정된 정책 특성을 사용하고 이전에 저장된 모든 정책은 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-143">Use policy attributes specified by policy_overrides and omit all previously stored policy.</span></span> |
| <span data-ttu-id="1fcb0-144">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="1fcb0-144">policy_overrides</span></span> |<span data-ttu-id="1fcb0-145">JSON 구조. 아래 **정책 재정의** 참조</span><span class="sxs-lookup"><span data-stu-id="1fcb0-145">JSON structure, see **Policy Overrides** below</span></span> |<span data-ttu-id="1fcb0-146">이 라이선스에 대한 정책 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-146">Policy settings for this license.</span></span>  <span data-ttu-id="1fcb0-147">이 자산에 미리 정의된 정책이 있는 경우 이러한 지정된 값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-147">In the event this asset has a pre-defined policy, these specified values will be used.</span></span> |
| <span data-ttu-id="1fcb0-148">session_init</span><span class="sxs-lookup"><span data-stu-id="1fcb0-148">session_init</span></span> |<span data-ttu-id="1fcb0-149">JSON 구조. 아래 **세션 초기화** 참조</span><span class="sxs-lookup"><span data-stu-id="1fcb0-149">JSON structure, see **Session Initialization** below</span></span> |<span data-ttu-id="1fcb0-150">라이선스에 전달되는 선택적 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-150">Optional data passed to license.</span></span> |
| <span data-ttu-id="1fcb0-151">parse_only</span><span class="sxs-lookup"><span data-stu-id="1fcb0-151">parse_only</span></span> |<span data-ttu-id="1fcb0-152">boolean.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-152">boolean.</span></span> <span data-ttu-id="1fcb0-153">true 또는 false</span><span class="sxs-lookup"><span data-stu-id="1fcb0-153">true or false</span></span> |<span data-ttu-id="1fcb0-154">라이선스 요청이 구문 분석되지만 라이선스는 발급되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-154">The license request is parsed but no license is issued.</span></span> <span data-ttu-id="1fcb0-155">그러나 라이선스 요청을 구성하는 값은 응답에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-155">However, values form the license request are returned in the response.</span></span> |

## <a name="content-key-specs"></a><span data-ttu-id="1fcb0-156">콘텐츠 키 사양</span><span class="sxs-lookup"><span data-stu-id="1fcb0-156">Content Key Specs</span></span>
<span data-ttu-id="1fcb0-157">기존 정책이 있는 경우 콘텐츠 키 사양에 값을 지정할 필요가 없습니다.  이 콘텐츠와 연결된 기존 정책이 HDCP 및 CGMS와 같은 출력 보호를 확인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-157">If a pre-existing policy exist, there is no need to specify any of the values in the Content Key Spec.  The pre-existing policy associated with this content will be used to determine the output protection such as HDCP and CGMS.</span></span>  <span data-ttu-id="1fcb0-158">기존 정책이 Widevine 라이선스 서버에 등록되지 않은 경우 콘텐츠 공급자는 값을 라이선스 요청에 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-158">If a pre-existing policy is not registered with the Widevine License Server, the content provider can inject the values into the license request.</span></span>   

<span data-ttu-id="1fcb0-159">use_policy_overrides_exclusively 옵션에 관계없이 모든 트랙에 대해 각 content_key_specs를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-159">Each content_key_specs must be specified for all tracks, regardless of the option use_policy_overrides_exclusively.</span></span> 

| <span data-ttu-id="1fcb0-160">이름</span><span class="sxs-lookup"><span data-stu-id="1fcb0-160">Name</span></span> | <span data-ttu-id="1fcb0-161">값</span><span class="sxs-lookup"><span data-stu-id="1fcb0-161">Value</span></span> | <span data-ttu-id="1fcb0-162">설명</span><span class="sxs-lookup"><span data-stu-id="1fcb0-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1fcb0-163">content_key_specs.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-163">content_key_specs.</span></span> <span data-ttu-id="1fcb0-164">track_type</span><span class="sxs-lookup"><span data-stu-id="1fcb0-164">track_type</span></span> |<span data-ttu-id="1fcb0-165">string</span><span class="sxs-lookup"><span data-stu-id="1fcb0-165">string</span></span> |<span data-ttu-id="1fcb0-166">트랙 유형 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-166">A track type name.</span></span> <span data-ttu-id="1fcb0-167">라이선스 요청에 Content_key_specs를 지정한 경우 모든 트랙 유형을 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-167">If content_key_specs is specified in the license request, make sure to specify all track types explicitly.</span></span> <span data-ttu-id="1fcb0-168">이렇게 하지 않으면 이전 10초 재생에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-168">Failure to do so will result in failure to playback past 10 seconds.</span></span> |
| <span data-ttu-id="1fcb0-169">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="1fcb0-169">content_key_specs</span></span>  <br/> <span data-ttu-id="1fcb0-170">security_level</span><span class="sxs-lookup"><span data-stu-id="1fcb0-170">security_level</span></span> |<span data-ttu-id="1fcb0-171">uint32</span><span class="sxs-lookup"><span data-stu-id="1fcb0-171">uint32</span></span> |<span data-ttu-id="1fcb0-172">재생에 대한 클라이언트 견고성 요구 사항을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-172">Defines client robustness requirements for playback.</span></span> <br/> <span data-ttu-id="1fcb0-173">1 - 소프트웨어 기반 화이트 박스 암호화가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-173">1 - Software-based whitebox crypto is required.</span></span> <br/> <span data-ttu-id="1fcb0-174">2 - 소프트웨어 암호화 및 난독 처리된 디코더가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-174">2 - Software crypto and an obfuscated decoder is required.</span></span> <br/> <span data-ttu-id="1fcb0-175">3 - 하드웨어 기반의 신뢰할 수 있는 실행 환경에서 키 자료 및 암호화 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-175">3 - The key material and crypto operations must be performed within a hardware backed trusted execution environment.</span></span> <br/> <span data-ttu-id="1fcb0-176">4 - 하드웨어 기반의 신뢰할 수 있는 실행 환경에서 콘텐츠의 암호화 및 디코딩을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-176">4 - The crypto and decoding of content must be performed within a hardware backed trusted execution environment.</span></span>  <br/> <span data-ttu-id="1fcb0-177">5 - 하드웨어 기반의 신뢰할 수 있는 실행 환경에서 미디어의 암호화, 디코딩 및 모든 처리(압축 및 압축 해제)를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-177">5 - The crypto, decoding and all handling of the media (compressed and uncompressed) must be handled within a hardware backed trusted execution environment.</span></span> |
| <span data-ttu-id="1fcb0-178">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="1fcb0-178">content_key_specs</span></span> <br/> <span data-ttu-id="1fcb0-179">required_output_protection.hdc</span><span class="sxs-lookup"><span data-stu-id="1fcb0-179">required_output_protection.hdc</span></span> |<span data-ttu-id="1fcb0-180">string - HDCP_NONE, HDCP_V1, HDCP_V2 중 하나</span><span class="sxs-lookup"><span data-stu-id="1fcb0-180">string - one of: HDCP_NONE, HDCP_V1, HDCP_V2</span></span> |<span data-ttu-id="1fcb0-181">HDCP가 필요한지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-181">Indicates whether HDCP is require</span></span> |
| <span data-ttu-id="1fcb0-182">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="1fcb0-182">content_key_specs</span></span> <br/><span data-ttu-id="1fcb0-183">key</span><span class="sxs-lookup"><span data-stu-id="1fcb0-183">key</span></span> |<span data-ttu-id="1fcb0-184">Base64 </span><span class="sxs-lookup"><span data-stu-id="1fcb0-184">Base64</span></span> <br/><span data-ttu-id="1fcb0-185">인코딩된 문자열</span><span class="sxs-lookup"><span data-stu-id="1fcb0-185">encoded string</span></span> |<span data-ttu-id="1fcb0-186">이 트랙에 사용할 콘텐츠 키입니다. 지정된 경우 track_type 또는 key_id가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-186">Content key to use for this track. If specified, the track_type or key_id is required.</span></span>  <span data-ttu-id="1fcb0-187">이 옵션을 사용하면 Widevine 라이선스 서버에서 키를 생성하거나 조회하도록 하지 않고, 콘텐츠 공급자가 이 트랙에 대한 콘텐츠 키를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-187">This option allows the content provider to inject the content key for this track instead of letting Widevine license server generate or lookup a key.</span></span> |
| <span data-ttu-id="1fcb0-188">content_key_specs.key_id</span><span class="sxs-lookup"><span data-stu-id="1fcb0-188">content_key_specs.key_id</span></span> |<span data-ttu-id="1fcb0-189">Base64 인코딩된 문자열 binary, 16바이트</span><span class="sxs-lookup"><span data-stu-id="1fcb0-189">Base64 encoded string  binary, 16 bytes</span></span> |<span data-ttu-id="1fcb0-190">키의 고유 식별자.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-190">Unique identifier for the key.</span></span> |

## <a name="policy-overrides"></a><span data-ttu-id="1fcb0-191">정책 재정의</span><span class="sxs-lookup"><span data-stu-id="1fcb0-191">Policy Overrides</span></span>
| <span data-ttu-id="1fcb0-192">이름</span><span class="sxs-lookup"><span data-stu-id="1fcb0-192">Name</span></span> | <span data-ttu-id="1fcb0-193">값</span><span class="sxs-lookup"><span data-stu-id="1fcb0-193">Value</span></span> | <span data-ttu-id="1fcb0-194">설명</span><span class="sxs-lookup"><span data-stu-id="1fcb0-194">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1fcb0-195">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-195">policy_overrides.</span></span> <span data-ttu-id="1fcb0-196">can_play</span><span class="sxs-lookup"><span data-stu-id="1fcb0-196">can_play</span></span> |<span data-ttu-id="1fcb0-197">boolean.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-197">boolean.</span></span> <span data-ttu-id="1fcb0-198">true 또는 false</span><span class="sxs-lookup"><span data-stu-id="1fcb0-198">true or false</span></span> |<span data-ttu-id="1fcb0-199">콘텐츠의 재생이 허용됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-199">Indicates that playback of the content is allowed.</span></span> <span data-ttu-id="1fcb0-200">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-200">Default is false.</span></span> |
| <span data-ttu-id="1fcb0-201">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-201">policy_overrides.</span></span> <span data-ttu-id="1fcb0-202">can_persist</span><span class="sxs-lookup"><span data-stu-id="1fcb0-202">can_persist</span></span> |<span data-ttu-id="1fcb0-203">boolean.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-203">boolean.</span></span> <span data-ttu-id="1fcb0-204">true 또는 false</span><span class="sxs-lookup"><span data-stu-id="1fcb0-204">true or false</span></span> |<span data-ttu-id="1fcb0-205">라이선스를 오프라인 용도로 비휘발성 저장소에 유지할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-205">Indicates that the license may be persisted to non-volatile storage for offline use.</span></span> <span data-ttu-id="1fcb0-206">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-206">Default is false.</span></span> |
| <span data-ttu-id="1fcb0-207">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-207">policy_overrides.</span></span> <span data-ttu-id="1fcb0-208">can_renew</span><span class="sxs-lookup"><span data-stu-id="1fcb0-208">can_renew</span></span> |<span data-ttu-id="1fcb0-209">boolean. true 또는 false</span><span class="sxs-lookup"><span data-stu-id="1fcb0-209">boolean true or false</span></span> |<span data-ttu-id="1fcb0-210">이 라이선스의 갱신이 허용됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-210">Indicates that renewal of this license is allowed.</span></span> <span data-ttu-id="1fcb0-211">true이면 라이선스의 기간을 하트비트로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-211">If true, the duration of the license can be extended by heartbeat.</span></span> <span data-ttu-id="1fcb0-212">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-212">Default is false.</span></span> |
| <span data-ttu-id="1fcb0-213">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-213">policy_overrides.</span></span> <span data-ttu-id="1fcb0-214">license_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="1fcb0-214">license_duration_seconds</span></span> |<span data-ttu-id="1fcb0-215">int64</span><span class="sxs-lookup"><span data-stu-id="1fcb0-215">int64</span></span> |<span data-ttu-id="1fcb0-216">이 특정 라이선스에 대한 기간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-216">Indicates the time window for this specific license.</span></span> <span data-ttu-id="1fcb0-217">값 0은 기간에 제한이 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-217">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="1fcb0-218">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-218">Default is 0.</span></span> |
| <span data-ttu-id="1fcb0-219">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-219">policy_overrides.</span></span> <span data-ttu-id="1fcb0-220">rental_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="1fcb0-220">rental_duration_seconds</span></span> |<span data-ttu-id="1fcb0-221">int64</span><span class="sxs-lookup"><span data-stu-id="1fcb0-221">int64</span></span> |<span data-ttu-id="1fcb0-222">재생이 허용되는 동안 기간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-222">Indicates the time window while playback is permitted.</span></span> <span data-ttu-id="1fcb0-223">값 0은 기간에 제한이 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-223">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="1fcb0-224">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-224">Default is 0.</span></span> |
| <span data-ttu-id="1fcb0-225">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-225">policy_overrides.</span></span> <span data-ttu-id="1fcb0-226">playback_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="1fcb0-226">playback_duration_seconds</span></span> |<span data-ttu-id="1fcb0-227">int64</span><span class="sxs-lookup"><span data-stu-id="1fcb0-227">int64</span></span> |<span data-ttu-id="1fcb0-228">라이선스 기간 내에서 재생이 시작된 후 표시 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-228">The viewing window of time once playback starts within the license duration.</span></span> <span data-ttu-id="1fcb0-229">값 0은 기간에 제한이 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-229">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="1fcb0-230">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-230">Default is 0.</span></span> |
| <span data-ttu-id="1fcb0-231">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-231">policy_overrides.</span></span> <span data-ttu-id="1fcb0-232">renewal_server_url</span><span class="sxs-lookup"><span data-stu-id="1fcb0-232">renewal_server_url</span></span> |<span data-ttu-id="1fcb0-233">string</span><span class="sxs-lookup"><span data-stu-id="1fcb0-233">string</span></span> |<span data-ttu-id="1fcb0-234">이 라이선스에 대한 모든 하트비트(갱신) 요청은 지정된 URL로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-234">All heartbeat (renewal) requests for this license shall be directed to the specified URL.</span></span> <span data-ttu-id="1fcb0-235">이 필드는 can_renew가 true인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-235">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="1fcb0-236">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-236">policy_overrides.</span></span> <span data-ttu-id="1fcb0-237">renewal_delay_seconds</span><span class="sxs-lookup"><span data-stu-id="1fcb0-237">renewal_delay_seconds</span></span> |<span data-ttu-id="1fcb0-238">int64</span><span class="sxs-lookup"><span data-stu-id="1fcb0-238">int64</span></span> |<span data-ttu-id="1fcb0-239">license_start_time 이후, 처음으로 갱신을 시도할 때까지 시간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-239">How many seconds after license_start_time, before renewal is first attempted.</span></span> <span data-ttu-id="1fcb0-240">이 필드는 can_renew가 true인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-240">This field is only used if can_renew is true.</span></span> <span data-ttu-id="1fcb0-241">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-241">Default is 0</span></span> |
| <span data-ttu-id="1fcb0-242">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-242">policy_overrides.</span></span> <span data-ttu-id="1fcb0-243">renewal_retry_interval_seconds</span><span class="sxs-lookup"><span data-stu-id="1fcb0-243">renewal_retry_interval_seconds</span></span> |<span data-ttu-id="1fcb0-244">int64</span><span class="sxs-lookup"><span data-stu-id="1fcb0-244">int64</span></span> |<span data-ttu-id="1fcb0-245">실패 시 후속 라이선스 갱신 요청 간 지연 시간(초)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-245">Specifies the delay in seconds between subsequent license renewal requests, in case of failure.</span></span> <span data-ttu-id="1fcb0-246">이 필드는 can_renew가 true인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-246">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="1fcb0-247">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-247">policy_overrides.</span></span> <span data-ttu-id="1fcb0-248">renewal_recovery_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="1fcb0-248">renewal_recovery_duration_seconds</span></span> |<span data-ttu-id="1fcb0-249">int64</span><span class="sxs-lookup"><span data-stu-id="1fcb0-249">int64</span></span> |<span data-ttu-id="1fcb0-250">갱신을 시도하는 동안 재생을 진행하도록 허용되었으나 라이선스 서버와 백 엔드 문제로 인해 재생이 실패한 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-250">The window of time, in which playback is allowed to continue while renewal is attempted, yet unsuccessful due to backend problems with the license server.</span></span> <span data-ttu-id="1fcb0-251">값 0은 기간에 제한이 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-251">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="1fcb0-252">이 필드는 can_renew가 true인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-252">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="1fcb0-253">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-253">policy_overrides.</span></span> <span data-ttu-id="1fcb0-254">renew_with_usage</span><span class="sxs-lookup"><span data-stu-id="1fcb0-254">renew_with_usage</span></span> |<span data-ttu-id="1fcb0-255">boolean. true 또는 false</span><span class="sxs-lookup"><span data-stu-id="1fcb0-255">boolean true or false</span></span> |<span data-ttu-id="1fcb0-256">사용이 시작된 경우 갱신을 위해 라이선스가 전송되어야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-256">Indicates that the license shall be sent for renewal when usage is started.</span></span> <span data-ttu-id="1fcb0-257">이 필드는 can_renew가 true인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-257">This field is only used if can_renew is true.</span></span> |

## <a name="session-initialization"></a><span data-ttu-id="1fcb0-258">세션 초기화</span><span class="sxs-lookup"><span data-stu-id="1fcb0-258">Session Initialization</span></span>
| <span data-ttu-id="1fcb0-259">이름</span><span class="sxs-lookup"><span data-stu-id="1fcb0-259">Name</span></span> | <span data-ttu-id="1fcb0-260">값</span><span class="sxs-lookup"><span data-stu-id="1fcb0-260">Value</span></span> | <span data-ttu-id="1fcb0-261">설명</span><span class="sxs-lookup"><span data-stu-id="1fcb0-261">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1fcb0-262">provider_session_token</span><span class="sxs-lookup"><span data-stu-id="1fcb0-262">provider_session_token</span></span> |<span data-ttu-id="1fcb0-263">Base64 인코딩된 문자열</span><span class="sxs-lookup"><span data-stu-id="1fcb0-263">Base64 encoded string</span></span> |<span data-ttu-id="1fcb0-264">이 세션 토큰은 라이선스에 다시 전달되고 후속 갱신에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-264">This session token is passed back in the license and will exist in subsequent renewals.</span></span>  <span data-ttu-id="1fcb0-265">세션 토큰은 세션 이후에는 유지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-265">The session token will not persist beyond sessions.</span></span> |
| <span data-ttu-id="1fcb0-266">provider_client_token</span><span class="sxs-lookup"><span data-stu-id="1fcb0-266">provider_client_token</span></span> |<span data-ttu-id="1fcb0-267">Base64 인코딩된 문자열</span><span class="sxs-lookup"><span data-stu-id="1fcb0-267">Base64 encoded string</span></span> |<span data-ttu-id="1fcb0-268">라이선스 응답으로 다시 보낼 클라이언트 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-268">Client token to send back in the license response.</span></span>  <span data-ttu-id="1fcb0-269">클라이언트 요청에 클라이언트 토큰이 포함된 경우 이 값은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-269">If the license request contains a client token, this value is ignored.</span></span> <span data-ttu-id="1fcb0-270">클라이언트 토큰은 라이선스 세션 이후에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-270">The client token will persist beyond license sessions.</span></span> |
| <span data-ttu-id="1fcb0-271">override_provider_client_token</span><span class="sxs-lookup"><span data-stu-id="1fcb0-271">override_provider_client_token</span></span> |<span data-ttu-id="1fcb0-272">boolean.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-272">boolean.</span></span> <span data-ttu-id="1fcb0-273">true 또는 false</span><span class="sxs-lookup"><span data-stu-id="1fcb0-273">true or false</span></span> |<span data-ttu-id="1fcb0-274">false이고 라이선스 요청에 클라이언트 토큰이 포함된 경우 이 구조에 클라이언트 토큰이 지정된 경우에도 요청의 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-274">If false and the license request contains a client token, use the token from the request even if a client token was specified in this structure.</span></span>  <span data-ttu-id="1fcb0-275">true이면 항상 이 구조에 지정된 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-275">If true, always use the token specified in this structure.</span></span> |

## <a name="configure-your-widevine-licenses-using-net-types"></a><span data-ttu-id="1fcb0-276">.NET 형식을 사용하여 Widevine 라이선스 구성</span><span class="sxs-lookup"><span data-stu-id="1fcb0-276">Configure your Widevine licenses using .NET types</span></span>
<span data-ttu-id="1fcb0-277">미디어 서비스는 Widevine 라이선스를 구성할 수 있는 .NET API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-277">Media Services provides .NET APIs that let you configure your Widevine licenses.</span></span> 

### <a name="classes-as-defined-in-the-media-services-net-sdk"></a><span data-ttu-id="1fcb0-278">미디어 서비스 .NET SDK에 정의된 클래스</span><span class="sxs-lookup"><span data-stu-id="1fcb0-278">Classes as defined in the Media Services .NET SDK</span></span>
<span data-ttu-id="1fcb0-279">이러한 형식에 대한 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-279">The following are the definitions of these types.</span></span>

    public class WidevineMessage
    {
        public WidevineMessage();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public AllowedTrackTypes? allowed_track_types { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public ContentKeySpecs[] content_key_specs { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public object policy_overrides { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum AllowedTrackTypes
    {
        SD_ONLY = 0,
        SD_HD = 1
    }
    public class ContentKeySpecs
    {
        public ContentKeySpecs();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string key_id { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public RequiredOutputProtection required_output_protection { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public int? security_level { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string track_type { get; set; }
    }

    public class RequiredOutputProtection
    {
        public RequiredOutputProtection();

        public Hdcp hdcp { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum Hdcp
    {
        HDCP_NONE = 0,
        HDCP_V1 = 1,
        HDCP_V2 = 2
    }

### <a name="example"></a><span data-ttu-id="1fcb0-280">예</span><span class="sxs-lookup"><span data-stu-id="1fcb0-280">Example</span></span>
<span data-ttu-id="1fcb0-281">다음 예제는 .NET API를 사용하여 간단한 Widevine 라이선스를 구성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1fcb0-281">The following example shows how to use .NET APIs to configure  a simple Widevine license.</span></span>

    private static string ConfigureWidevineLicenseTemplate()
    {
        var template = new WidevineMessage
        {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                new ContentKeySpecs
                {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                }
            },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
        };

        string configuration = JsonConvert.SerializeObject(template);
        return configuration;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="1fcb0-282">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="1fcb0-282">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1fcb0-283">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="1fcb0-283">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="1fcb0-284">참고 항목</span><span class="sxs-lookup"><span data-stu-id="1fcb0-284">See also</span></span>
[<span data-ttu-id="1fcb0-285">PlayReady 및/또는 Widevine 동적 일반 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="1fcb0-285">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

