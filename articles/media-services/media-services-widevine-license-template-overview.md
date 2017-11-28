---
title: "aaaWidevine 라이선스 템플릿 개요 | Microsoft Docs"
description: "이 항목에서는 tooconfigure Widevine 라이선스 사용 되는 Widevine 라이선스 템플릿 개요를 제공 합니다."
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
ms.openlocfilehash: 67a6ae38cf3d3c21e1b7282aef15f79b21776414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="widevine-license-template-overview"></a><span data-ttu-id="61496-103">Widevine 라이선스 템플릿 개요</span><span class="sxs-lookup"><span data-stu-id="61496-103">Widevine license template overview</span></span>
## <a name="overview"></a><span data-ttu-id="61496-104">개요</span><span class="sxs-lookup"><span data-stu-id="61496-104">Overview</span></span>
<span data-ttu-id="61496-105">이제 azure 미디어 서비스는 tooconfigure 및 요청 Widevine 라이선스에서는 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-105">Azure Media Services now enables you tooconfigure and request Widevine licenses.</span></span> <span data-ttu-id="61496-106">Widevine 보호 된 콘텐츠를 요청 hello 최종 사용자 플레이어 시도 tooplay 경우 보낸된 toohello 라이선스 배달 서비스 tooobtain 라이선스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61496-106">When hello end user player tries tooplay your Widevine protected content, a request is sent toohello license delivery service tooobtain a license.</span></span> <span data-ttu-id="61496-107">Hello 라이선스 서비스 hello 요청을 승인 하는 경우 보낸된 toohello 클라이언트 중인 hello 라이선스를 발급 하 고 수 수 사용된 toodecrypt 앤 플레이 hello 지정 된 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="61496-107">If hello license service approves hello request, it issues hello license which is sent toohello client and can be used toodecrypt and play hello specified content.</span></span>

<span data-ttu-id="61496-108">Widevine 라이선스 요청 형식은 JSON 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="61496-108">Widevine license request is formatted as a JSON message.</span></span>  

>[!NOTE]
> <span data-ttu-id="61496-109">Toocreate 없는 값만 "{}"와 빈 메시지를 선택할 수 있습니다 및 라이선스 템플릿을 모든 기본값을 사용 하 여 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-109">You can choose toocreate an empty message with no values just "{}" and a license template will be created with all defaults.</span></span> <span data-ttu-id="61496-110">hello 기본 대부분의 경우에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-110">hello default works for most cases.</span></span> <span data-ttu-id="61496-111">예를 들어 MS 기반 라이선스 배달 시나리오에서도 항상 기본값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61496-111">For example, for MS based license delivery scenarios that should always be default.</span></span> <span data-ttu-id="61496-112">Tooset hello "provider" 및 "content_id" 값이 필요 않으면, 공급자 Google의 Widevine 자격 증명과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-112">If you do need tooset hello "provider" and "content_id" values, a provider must match Google's Widevine credentials.</span></span>

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

## <a name="json-message"></a><span data-ttu-id="61496-113">JSON 메시지</span><span class="sxs-lookup"><span data-stu-id="61496-113">JSON message</span></span>
| <span data-ttu-id="61496-114">이름</span><span class="sxs-lookup"><span data-stu-id="61496-114">Name</span></span> | <span data-ttu-id="61496-115">값</span><span class="sxs-lookup"><span data-stu-id="61496-115">Value</span></span> | <span data-ttu-id="61496-116">설명</span><span class="sxs-lookup"><span data-stu-id="61496-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="61496-117">payload</span><span class="sxs-lookup"><span data-stu-id="61496-117">payload</span></span> |<span data-ttu-id="61496-118">Base64 인코딩된 문자열</span><span class="sxs-lookup"><span data-stu-id="61496-118">Base64 encoded string</span></span> |<span data-ttu-id="61496-119">클라이언트에서 보낸 hello 라이선스 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-119">hello license request sent by a client.</span></span> |
| <span data-ttu-id="61496-120">content_id</span><span class="sxs-lookup"><span data-stu-id="61496-120">content_id</span></span> |<span data-ttu-id="61496-121">Base64 인코딩된 문자열</span><span class="sxs-lookup"><span data-stu-id="61496-121">Base64 encoded string</span></span> |<span data-ttu-id="61496-122">각 content_key_specs.track_type에 tooderive KeyId(s) 및 콘텐츠 키를 사용 하는 식별자.</span><span class="sxs-lookup"><span data-stu-id="61496-122">Identifier used tooderive KeyId(s) and Content Key(s) for each content_key_specs.track_type.</span></span> |
| <span data-ttu-id="61496-123">provider</span><span class="sxs-lookup"><span data-stu-id="61496-123">provider</span></span> |<span data-ttu-id="61496-124">string</span><span class="sxs-lookup"><span data-stu-id="61496-124">string</span></span> |<span data-ttu-id="61496-125">콘텐츠 키 및 정책을를 사용 하는 toolook 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-125">Used toolook up content keys and policies.</span></span> <span data-ttu-id="61496-126">MS 키 배달이 Widevine 라이선스 배달에 사용되는 경우 이 매개 변수는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="61496-126">If MS key delivery is used for Widevine license delivery, this parameter is ignored.</span></span> |
| <span data-ttu-id="61496-127">policy_name</span><span class="sxs-lookup"><span data-stu-id="61496-127">policy_name</span></span> |<span data-ttu-id="61496-128">string</span><span class="sxs-lookup"><span data-stu-id="61496-128">string</span></span> |<span data-ttu-id="61496-129">이전에 등록된 정책의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="61496-129">Name of a previously registered policy.</span></span> <span data-ttu-id="61496-130">옵션</span><span class="sxs-lookup"><span data-stu-id="61496-130">Optional</span></span> |
| <span data-ttu-id="61496-131">allowed_track_types</span><span class="sxs-lookup"><span data-stu-id="61496-131">allowed_track_types</span></span> |<span data-ttu-id="61496-132">enum</span><span class="sxs-lookup"><span data-stu-id="61496-132">enum</span></span> |<span data-ttu-id="61496-133">SD_ONLY 또는 SD_HD.</span><span class="sxs-lookup"><span data-stu-id="61496-133">SD_ONLY or SD_HD.</span></span> <span data-ttu-id="61496-134">라이선스에 포함할 콘텐츠 키를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-134">Controls which content keys should be included in a license</span></span> |
| <span data-ttu-id="61496-135">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="61496-135">content_key_specs</span></span> |<span data-ttu-id="61496-136">JSON 구조 배열. 아래 **콘텐츠 키 사양** 참조</span><span class="sxs-lookup"><span data-stu-id="61496-136">array of JSON structures, see **Content Key Specs** below</span></span> |<span data-ttu-id="61496-137">보다 세밀 하 게 세분화 된 컨트롤에 콘텐츠 키 tooreturn 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-137">A finer grained control on what content keys tooreturn.</span></span> <span data-ttu-id="61496-138">자세한 내용은 아래 콘텐츠 키 사양을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="61496-138">See Content Key Spec below for details.</span></span>  <span data-ttu-id="61496-139">Allowed_track_types 및 content_key_specs 중 하나만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61496-139">Only one of allowed_track_types and content_key_specs can be specified.</span></span> |
| <span data-ttu-id="61496-140">use_policy_overrides_exclusively</span><span class="sxs-lookup"><span data-stu-id="61496-140">use_policy_overrides_exclusively</span></span> |<span data-ttu-id="61496-141">boolean.</span><span class="sxs-lookup"><span data-stu-id="61496-141">boolean.</span></span> <span data-ttu-id="61496-142">true 또는 false</span><span class="sxs-lookup"><span data-stu-id="61496-142">true or false</span></span> |<span data-ttu-id="61496-143">policy_overrides로 지정된 정책 특성을 사용하고 이전에 저장된 모든 정책은 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-143">Use policy attributes specified by policy_overrides and omit all previously stored policy.</span></span> |
| <span data-ttu-id="61496-144">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="61496-144">policy_overrides</span></span> |<span data-ttu-id="61496-145">JSON 구조. 아래 **정책 재정의** 참조</span><span class="sxs-lookup"><span data-stu-id="61496-145">JSON structure, see **Policy Overrides** below</span></span> |<span data-ttu-id="61496-146">이 라이선스에 대한 정책 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="61496-146">Policy settings for this license.</span></span>  <span data-ttu-id="61496-147">이 자산에는 미리 정의 된 정책이 hello 이벤트에서, 이러한 지정 된 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61496-147">In hello event this asset has a pre-defined policy, these specified values will be used.</span></span> |
| <span data-ttu-id="61496-148">session_init</span><span class="sxs-lookup"><span data-stu-id="61496-148">session_init</span></span> |<span data-ttu-id="61496-149">JSON 구조. 아래 **세션 초기화** 참조</span><span class="sxs-lookup"><span data-stu-id="61496-149">JSON structure, see **Session Initialization** below</span></span> |<span data-ttu-id="61496-150">선택적 데이터 toolicense를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-150">Optional data passed toolicense.</span></span> |
| <span data-ttu-id="61496-151">parse_only</span><span class="sxs-lookup"><span data-stu-id="61496-151">parse_only</span></span> |<span data-ttu-id="61496-152">boolean.</span><span class="sxs-lookup"><span data-stu-id="61496-152">boolean.</span></span> <span data-ttu-id="61496-153">true 또는 false</span><span class="sxs-lookup"><span data-stu-id="61496-153">true or false</span></span> |<span data-ttu-id="61496-154">hello 라이선스 요청은 구문 분석 되지만 라이선스가 발급 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61496-154">hello license request is parsed but no license is issued.</span></span> <span data-ttu-id="61496-155">그러나 값 양식 hello 라이선스 요청 hello 응답에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61496-155">However, values form hello license request are returned in hello response.</span></span> |

## <a name="content-key-specs"></a><span data-ttu-id="61496-156">콘텐츠 키 사양</span><span class="sxs-lookup"><span data-stu-id="61496-156">Content Key Specs</span></span>
<span data-ttu-id="61496-157">기존 정책 없을 경우 hello 콘텐츠 키 사양에서에서 값을 hello의 필요성 toospecify 없습니다.  이 콘텐츠와 연결 된 hello 기존 정책을 HDCP CGMS 등 사용된 toodetermine hello 출력 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61496-157">If a pre-existing policy exist, there is no need toospecify any of hello values in hello Content Key Spec.  hello pre-existing policy associated with this content will be used toodetermine hello output protection such as HDCP and CGMS.</span></span>  <span data-ttu-id="61496-158">기존 정책 Widevine 라이선스 서버 hello로 등록 되어 있지 않으면, hello 콘텐츠 공급자 hello 라이선스 요청에 hello 값을 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61496-158">If a pre-existing policy is not registered with hello Widevine License Server, hello content provider can inject hello values into hello license request.</span></span>   

<span data-ttu-id="61496-159">각 content_key_specs hello 옵션 use_policy_overrides_exclusively에 관계 없이 모든 트랙에 대해 지정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-159">Each content_key_specs must be specified for all tracks, regardless of hello option use_policy_overrides_exclusively.</span></span> 

| <span data-ttu-id="61496-160">이름</span><span class="sxs-lookup"><span data-stu-id="61496-160">Name</span></span> | <span data-ttu-id="61496-161">값</span><span class="sxs-lookup"><span data-stu-id="61496-161">Value</span></span> | <span data-ttu-id="61496-162">설명</span><span class="sxs-lookup"><span data-stu-id="61496-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="61496-163">content_key_specs.</span><span class="sxs-lookup"><span data-stu-id="61496-163">content_key_specs.</span></span> <span data-ttu-id="61496-164">track_type</span><span class="sxs-lookup"><span data-stu-id="61496-164">track_type</span></span> |<span data-ttu-id="61496-165">string</span><span class="sxs-lookup"><span data-stu-id="61496-165">string</span></span> |<span data-ttu-id="61496-166">트랙 유형 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="61496-166">A track type name.</span></span> <span data-ttu-id="61496-167">Content_key_specs hello 라이선스 요청에 지정 된 경우 확인 되었는지 toospecify 추적 모든 형식을 명시적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-167">If content_key_specs is specified in hello license request, make sure toospecify all track types explicitly.</span></span> <span data-ttu-id="61496-168">오류 toodo 하므로 될 오류 tooplayback 지난 10 초 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61496-168">Failure toodo so will result in failure tooplayback past 10 seconds.</span></span> |
| <span data-ttu-id="61496-169">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="61496-169">content_key_specs</span></span>  <br/> <span data-ttu-id="61496-170">security_level</span><span class="sxs-lookup"><span data-stu-id="61496-170">security_level</span></span> |<span data-ttu-id="61496-171">uint32</span><span class="sxs-lookup"><span data-stu-id="61496-171">uint32</span></span> |<span data-ttu-id="61496-172">재생에 대한 클라이언트 견고성 요구 사항을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-172">Defines client robustness requirements for playback.</span></span> <br/> <span data-ttu-id="61496-173">1 - 소프트웨어 기반 화이트 박스 암호화가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-173">1 - Software-based whitebox crypto is required.</span></span> <br/> <span data-ttu-id="61496-174">2 - 소프트웨어 암호화 및 난독 처리된 디코더가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-174">2 - Software crypto and an obfuscated decoder is required.</span></span> <br/> <span data-ttu-id="61496-175">3-hello 키 재료 및 암호화 작업은 하드웨어 백업 된 신뢰할 수 있는 실행 환경 내에서 수행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-175">3 - hello key material and crypto operations must be performed within a hardware backed trusted execution environment.</span></span> <br/> <span data-ttu-id="61496-176">4-암호화 및 콘텐츠의 디코딩 hello 하드웨어 백업 된 신뢰할 수 있는 실행 환경 내에서 수행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-176">4 - hello crypto and decoding of content must be performed within a hardware backed trusted execution environment.</span></span>  <br/> <span data-ttu-id="61496-177">5-hello 암호화, 디코딩 및 모두 처리 hello 미디어 (압축 및 압축 되지 않은)의 하드웨어 백업 된 신뢰할 수 있는 실행 환경 내에서 처리 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-177">5 - hello crypto, decoding and all handling of hello media (compressed and uncompressed) must be handled within a hardware backed trusted execution environment.</span></span> |
| <span data-ttu-id="61496-178">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="61496-178">content_key_specs</span></span> <br/> <span data-ttu-id="61496-179">required_output_protection.hdc</span><span class="sxs-lookup"><span data-stu-id="61496-179">required_output_protection.hdc</span></span> |<span data-ttu-id="61496-180">string - HDCP_NONE, HDCP_V1, HDCP_V2 중 하나</span><span class="sxs-lookup"><span data-stu-id="61496-180">string - one of: HDCP_NONE, HDCP_V1, HDCP_V2</span></span> |<span data-ttu-id="61496-181">HDCP가 필요한지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="61496-181">Indicates whether HDCP is require</span></span> |
| <span data-ttu-id="61496-182">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="61496-182">content_key_specs</span></span> <br/><span data-ttu-id="61496-183">key</span><span class="sxs-lookup"><span data-stu-id="61496-183">key</span></span> |<span data-ttu-id="61496-184">Base64 </span><span class="sxs-lookup"><span data-stu-id="61496-184">Base64</span></span> <br/><span data-ttu-id="61496-185">인코딩된 문자열</span><span class="sxs-lookup"><span data-stu-id="61496-185">encoded string</span></span> |<span data-ttu-id="61496-186">이 트랙에 대 한 콘텐츠 키 toouse 합니다. 지정 하지 않거나 track_type hello key_id가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-186">Content key toouse for this track. If specified, hello track_type or key_id is required.</span></span>  <span data-ttu-id="61496-187">이 옵션을 사용 하면 hello 콘텐츠 공급자 tooinject hello Widevine 라이선스 서버는 키 조회 또는 생성 하도록 하는 대신이 트랙에 대 한 콘텐츠 키입니다.</span><span class="sxs-lookup"><span data-stu-id="61496-187">This option allows hello content provider tooinject hello content key for this track instead of letting Widevine license server generate or lookup a key.</span></span> |
| <span data-ttu-id="61496-188">content_key_specs.key_id</span><span class="sxs-lookup"><span data-stu-id="61496-188">content_key_specs.key_id</span></span> |<span data-ttu-id="61496-189">Base64 인코딩된 문자열 binary, 16바이트</span><span class="sxs-lookup"><span data-stu-id="61496-189">Base64 encoded string  binary, 16 bytes</span></span> |<span data-ttu-id="61496-190">Hello 키에 대 한 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="61496-190">Unique identifier for hello key.</span></span> |

## <a name="policy-overrides"></a><span data-ttu-id="61496-191">정책 재정의</span><span class="sxs-lookup"><span data-stu-id="61496-191">Policy Overrides</span></span>
| <span data-ttu-id="61496-192">이름</span><span class="sxs-lookup"><span data-stu-id="61496-192">Name</span></span> | <span data-ttu-id="61496-193">값</span><span class="sxs-lookup"><span data-stu-id="61496-193">Value</span></span> | <span data-ttu-id="61496-194">설명</span><span class="sxs-lookup"><span data-stu-id="61496-194">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="61496-195">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="61496-195">policy_overrides.</span></span> <span data-ttu-id="61496-196">can_play</span><span class="sxs-lookup"><span data-stu-id="61496-196">can_play</span></span> |<span data-ttu-id="61496-197">boolean.</span><span class="sxs-lookup"><span data-stu-id="61496-197">boolean.</span></span> <span data-ttu-id="61496-198">true 또는 false</span><span class="sxs-lookup"><span data-stu-id="61496-198">true or false</span></span> |<span data-ttu-id="61496-199">해당 재생이 나타냅니다 hello의 콘텐츠를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61496-199">Indicates that playback of hello content is allowed.</span></span> <span data-ttu-id="61496-200">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="61496-200">Default is false.</span></span> |
| <span data-ttu-id="61496-201">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="61496-201">policy_overrides.</span></span> <span data-ttu-id="61496-202">can_persist</span><span class="sxs-lookup"><span data-stu-id="61496-202">can_persist</span></span> |<span data-ttu-id="61496-203">boolean.</span><span class="sxs-lookup"><span data-stu-id="61496-203">boolean.</span></span> <span data-ttu-id="61496-204">true 또는 false</span><span class="sxs-lookup"><span data-stu-id="61496-204">true or false</span></span> |<span data-ttu-id="61496-205">Hello 라이센스 지속형된 toonon 비휘발성 저장소를 오프 라인 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="61496-205">Indicates that hello license may be persisted toonon-volatile storage for offline use.</span></span> <span data-ttu-id="61496-206">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="61496-206">Default is false.</span></span> |
| <span data-ttu-id="61496-207">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="61496-207">policy_overrides.</span></span> <span data-ttu-id="61496-208">can_renew</span><span class="sxs-lookup"><span data-stu-id="61496-208">can_renew</span></span> |<span data-ttu-id="61496-209">boolean. true 또는 false</span><span class="sxs-lookup"><span data-stu-id="61496-209">boolean true or false</span></span> |<span data-ttu-id="61496-210">이 라이선스의 갱신이 허용됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="61496-210">Indicates that renewal of this license is allowed.</span></span> <span data-ttu-id="61496-211">True 인 경우, 하트 비트 하 여 hello 라이선스 기간의 hello를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61496-211">If true, hello duration of hello license can be extended by heartbeat.</span></span> <span data-ttu-id="61496-212">기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="61496-212">Default is false.</span></span> |
| <span data-ttu-id="61496-213">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="61496-213">policy_overrides.</span></span> <span data-ttu-id="61496-214">license_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="61496-214">license_duration_seconds</span></span> |<span data-ttu-id="61496-215">int64</span><span class="sxs-lookup"><span data-stu-id="61496-215">int64</span></span> |<span data-ttu-id="61496-216">이 특정 라이선스에 대 한 hello 기간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="61496-216">Indicates hello time window for this specific license.</span></span> <span data-ttu-id="61496-217">값이 0 no 제한 toohello 기간 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="61496-217">A value of 0 indicates that there is no limit toohello duration.</span></span> <span data-ttu-id="61496-218">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="61496-218">Default is 0.</span></span> |
| <span data-ttu-id="61496-219">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="61496-219">policy_overrides.</span></span> <span data-ttu-id="61496-220">rental_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="61496-220">rental_duration_seconds</span></span> |<span data-ttu-id="61496-221">int64</span><span class="sxs-lookup"><span data-stu-id="61496-221">int64</span></span> |<span data-ttu-id="61496-222">재생은 허용 하는 동안 hello 기간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="61496-222">Indicates hello time window while playback is permitted.</span></span> <span data-ttu-id="61496-223">값이 0 no 제한 toohello 기간 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="61496-223">A value of 0 indicates that there is no limit toohello duration.</span></span> <span data-ttu-id="61496-224">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="61496-224">Default is 0.</span></span> |
| <span data-ttu-id="61496-225">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="61496-225">policy_overrides.</span></span> <span data-ttu-id="61496-226">playback_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="61496-226">playback_duration_seconds</span></span> |<span data-ttu-id="61496-227">int64</span><span class="sxs-lookup"><span data-stu-id="61496-227">int64</span></span> |<span data-ttu-id="61496-228">hello 재생 hello 라이선스 기간 내에서 시작 되 면 시간 창을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-228">hello viewing window of time once playback starts within hello license duration.</span></span> <span data-ttu-id="61496-229">값이 0 no 제한 toohello 기간 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="61496-229">A value of 0 indicates that there is no limit toohello duration.</span></span> <span data-ttu-id="61496-230">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="61496-230">Default is 0.</span></span> |
| <span data-ttu-id="61496-231">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="61496-231">policy_overrides.</span></span> <span data-ttu-id="61496-232">renewal_server_url</span><span class="sxs-lookup"><span data-stu-id="61496-232">renewal_server_url</span></span> |<span data-ttu-id="61496-233">string</span><span class="sxs-lookup"><span data-stu-id="61496-233">string</span></span> |<span data-ttu-id="61496-234">이 라이선스에 대 한 모든 하트 비트 (갱신) 요청은 toohello 지정한 URL 전송할 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-234">All heartbeat (renewal) requests for this license shall be directed toohello specified URL.</span></span> <span data-ttu-id="61496-235">이 필드는 can_renew가 true인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61496-235">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="61496-236">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="61496-236">policy_overrides.</span></span> <span data-ttu-id="61496-237">renewal_delay_seconds</span><span class="sxs-lookup"><span data-stu-id="61496-237">renewal_delay_seconds</span></span> |<span data-ttu-id="61496-238">int64</span><span class="sxs-lookup"><span data-stu-id="61496-238">int64</span></span> |<span data-ttu-id="61496-239">license_start_time 이후, 처음으로 갱신을 시도할 때까지 시간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="61496-239">How many seconds after license_start_time, before renewal is first attempted.</span></span> <span data-ttu-id="61496-240">이 필드는 can_renew가 true인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61496-240">This field is only used if can_renew is true.</span></span> <span data-ttu-id="61496-241">기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="61496-241">Default is 0</span></span> |
| <span data-ttu-id="61496-242">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="61496-242">policy_overrides.</span></span> <span data-ttu-id="61496-243">renewal_retry_interval_seconds</span><span class="sxs-lookup"><span data-stu-id="61496-243">renewal_retry_interval_seconds</span></span> |<span data-ttu-id="61496-244">int64</span><span class="sxs-lookup"><span data-stu-id="61496-244">int64</span></span> |<span data-ttu-id="61496-245">Hello 지연 실패 시 후속 라이선스 갱신 요청 간격 (초) 단위로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-245">Specifies hello delay in seconds between subsequent license renewal requests, in case of failure.</span></span> <span data-ttu-id="61496-246">이 필드는 can_renew가 true인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61496-246">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="61496-247">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="61496-247">policy_overrides.</span></span> <span data-ttu-id="61496-248">renewal_recovery_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="61496-248">renewal_recovery_duration_seconds</span></span> |<span data-ttu-id="61496-249">int64</span><span class="sxs-lookup"><span data-stu-id="61496-249">int64</span></span> |<span data-ttu-id="61496-250">시간,는 재생 toocontinue 갱신 하는 동안 hello 창이 시도 된 됩니다 아직 toobackend 문제 hello 라이선스 서버를 인해 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-250">hello window of time, in which playback is allowed toocontinue while renewal is attempted, yet unsuccessful due toobackend problems with hello license server.</span></span> <span data-ttu-id="61496-251">값이 0 no 제한 toohello 기간 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="61496-251">A value of 0 indicates that there is no limit toohello duration.</span></span> <span data-ttu-id="61496-252">이 필드는 can_renew가 true인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61496-252">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="61496-253">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="61496-253">policy_overrides.</span></span> <span data-ttu-id="61496-254">renew_with_usage</span><span class="sxs-lookup"><span data-stu-id="61496-254">renew_with_usage</span></span> |<span data-ttu-id="61496-255">boolean. true 또는 false</span><span class="sxs-lookup"><span data-stu-id="61496-255">boolean true or false</span></span> |<span data-ttu-id="61496-256">사용 현황이 시작 될 때 갱신에 대 한 해당 hello 라이선스를 보낼 수는 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="61496-256">Indicates that hello license shall be sent for renewal when usage is started.</span></span> <span data-ttu-id="61496-257">이 필드는 can_renew가 true인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61496-257">This field is only used if can_renew is true.</span></span> |

## <a name="session-initialization"></a><span data-ttu-id="61496-258">세션 초기화</span><span class="sxs-lookup"><span data-stu-id="61496-258">Session Initialization</span></span>
| <span data-ttu-id="61496-259">이름</span><span class="sxs-lookup"><span data-stu-id="61496-259">Name</span></span> | <span data-ttu-id="61496-260">값</span><span class="sxs-lookup"><span data-stu-id="61496-260">Value</span></span> | <span data-ttu-id="61496-261">설명</span><span class="sxs-lookup"><span data-stu-id="61496-261">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="61496-262">provider_session_token</span><span class="sxs-lookup"><span data-stu-id="61496-262">provider_session_token</span></span> |<span data-ttu-id="61496-263">Base64 인코딩된 문자열</span><span class="sxs-lookup"><span data-stu-id="61496-263">Base64 encoded string</span></span> |<span data-ttu-id="61496-264">이 세션 토큰 hello 라이선스에 다시 전달 하 고 후속 갱신에 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-264">This session token is passed back in hello license and will exist in subsequent renewals.</span></span>  <span data-ttu-id="61496-265">hello 세션 토큰 세션 이상 유지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="61496-265">hello session token will not persist beyond sessions.</span></span> |
| <span data-ttu-id="61496-266">provider_client_token</span><span class="sxs-lookup"><span data-stu-id="61496-266">provider_client_token</span></span> |<span data-ttu-id="61496-267">Base64 인코딩된 문자열</span><span class="sxs-lookup"><span data-stu-id="61496-267">Base64 encoded string</span></span> |<span data-ttu-id="61496-268">클라이언트 hello 라이선스 응답에서 토큰 toosend 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-268">Client token toosend back in hello license response.</span></span>  <span data-ttu-id="61496-269">클라이언트 토큰을 포함 하는 hello 라이선스 요청을 하는 경우이 값은 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61496-269">If hello license request contains a client token, this value is ignored.</span></span> <span data-ttu-id="61496-270">클라이언트 토큰 hello 라이선스 세션 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="61496-270">hello client token will persist beyond license sessions.</span></span> |
| <span data-ttu-id="61496-271">override_provider_client_token</span><span class="sxs-lookup"><span data-stu-id="61496-271">override_provider_client_token</span></span> |<span data-ttu-id="61496-272">boolean.</span><span class="sxs-lookup"><span data-stu-id="61496-272">boolean.</span></span> <span data-ttu-id="61496-273">true 또는 false</span><span class="sxs-lookup"><span data-stu-id="61496-273">true or false</span></span> |<span data-ttu-id="61496-274">클라이언트 토큰을 포함 하는 false이 고 hello 라이선스 요청을 하는 경우이 구조에는 클라이언트 토큰을 지정 하는 경우에 hello 요청에서 hello 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-274">If false and hello license request contains a client token, use hello token from hello request even if a client token was specified in this structure.</span></span>  <span data-ttu-id="61496-275">True 인 경우, 항상이 구조에 지정 된 hello 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-275">If true, always use hello token specified in this structure.</span></span> |

## <a name="configure-your-widevine-licenses-using-net-types"></a><span data-ttu-id="61496-276">.NET 형식을 사용하여 Widevine 라이선스 구성</span><span class="sxs-lookup"><span data-stu-id="61496-276">Configure your Widevine licenses using .NET types</span></span>
<span data-ttu-id="61496-277">미디어 서비스는 Widevine 라이선스를 구성할 수 있는 .NET API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-277">Media Services provides .NET APIs that let you configure your Widevine licenses.</span></span> 

### <a name="classes-as-defined-in-hello-media-services-net-sdk"></a><span data-ttu-id="61496-278">Hello 미디어 서비스.NET SDK에에서 정의 된 대로 클래스</span><span class="sxs-lookup"><span data-stu-id="61496-278">Classes as defined in hello Media Services .NET SDK</span></span>
<span data-ttu-id="61496-279">hello 다음은 이러한 유형의 hello 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="61496-279">hello following are hello definitions of these types.</span></span>

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

### <a name="example"></a><span data-ttu-id="61496-280">예제</span><span class="sxs-lookup"><span data-stu-id="61496-280">Example</span></span>
<span data-ttu-id="61496-281">hello 방법을 예제와 다음 toouse.NET Api tooconfigure 간단한 Widevine 라이선스입니다.</span><span class="sxs-lookup"><span data-stu-id="61496-281">hello following example shows how toouse .NET APIs tooconfigure  a simple Widevine license.</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="61496-282">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="61496-282">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="61496-283">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="61496-283">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="61496-284">참고 항목</span><span class="sxs-lookup"><span data-stu-id="61496-284">See also</span></span>
[<span data-ttu-id="61496-285">PlayReady 및/또는 Widevine 동적 일반 암호화 사용</span><span class="sxs-lookup"><span data-stu-id="61496-285">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

