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
# <a name="widevine-license-template-overview"></a>Widevine 라이선스 템플릿 개요
## <a name="overview"></a>개요
이제 azure 미디어 서비스는 tooconfigure 및 요청 Widevine 라이선스에서는 합니다. Widevine 보호 된 콘텐츠를 요청 hello 최종 사용자 플레이어 시도 tooplay 경우 보낸된 toohello 라이선스 배달 서비스 tooobtain 라이선스가 있습니다. Hello 라이선스 서비스 hello 요청을 승인 하는 경우 보낸된 toohello 클라이언트 중인 hello 라이선스를 발급 하 고 수 수 사용된 toodecrypt 앤 플레이 hello 지정 된 콘텐츠입니다.

Widevine 라이선스 요청 형식은 JSON 메시지입니다.  

>[!NOTE]
> Toocreate 없는 값만 "{}"와 빈 메시지를 선택할 수 있습니다 및 라이선스 템플릿을 모든 기본값을 사용 하 여 만들어야 합니다. hello 기본 대부분의 경우에 적합합니다. 예를 들어 MS 기반 라이선스 배달 시나리오에서도 항상 기본값을 사용할 수 있습니다. Tooset hello "provider" 및 "content_id" 값이 필요 않으면, 공급자 Google의 Widevine 자격 증명과 일치 해야 합니다.

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

## <a name="json-message"></a>JSON 메시지
| 이름 | 값 | 설명 |
| --- | --- | --- |
| payload |Base64 인코딩된 문자열 |클라이언트에서 보낸 hello 라이선스 요청 합니다. |
| content_id |Base64 인코딩된 문자열 |각 content_key_specs.track_type에 tooderive KeyId(s) 및 콘텐츠 키를 사용 하는 식별자. |
| provider |string |콘텐츠 키 및 정책을를 사용 하는 toolook 합니다. MS 키 배달이 Widevine 라이선스 배달에 사용되는 경우 이 매개 변수는 무시됩니다. |
| policy_name |string |이전에 등록된 정책의 이름입니다. 옵션 |
| allowed_track_types |enum |SD_ONLY 또는 SD_HD. 라이선스에 포함할 콘텐츠 키를 제어합니다. |
| content_key_specs |JSON 구조 배열. 아래 **콘텐츠 키 사양** 참조 |보다 세밀 하 게 세분화 된 컨트롤에 콘텐츠 키 tooreturn 합니다. 자세한 내용은 아래 콘텐츠 키 사양을 참조하세요.  Allowed_track_types 및 content_key_specs 중 하나만 지정할 수 있습니다. |
| use_policy_overrides_exclusively |boolean. true 또는 false |policy_overrides로 지정된 정책 특성을 사용하고 이전에 저장된 모든 정책은 생략합니다. |
| policy_overrides |JSON 구조. 아래 **정책 재정의** 참조 |이 라이선스에 대한 정책 설정입니다.  이 자산에는 미리 정의 된 정책이 hello 이벤트에서, 이러한 지정 된 값이 사용 됩니다. |
| session_init |JSON 구조. 아래 **세션 초기화** 참조 |선택적 데이터 toolicense를 전달 합니다. |
| parse_only |boolean. true 또는 false |hello 라이선스 요청은 구문 분석 되지만 라이선스가 발급 됩니다. 그러나 값 양식 hello 라이선스 요청 hello 응답에 반환 됩니다. |

## <a name="content-key-specs"></a>콘텐츠 키 사양
기존 정책 없을 경우 hello 콘텐츠 키 사양에서에서 값을 hello의 필요성 toospecify 없습니다.  이 콘텐츠와 연결 된 hello 기존 정책을 HDCP CGMS 등 사용된 toodetermine hello 출력 보호 됩니다.  기존 정책 Widevine 라이선스 서버 hello로 등록 되어 있지 않으면, hello 콘텐츠 공급자 hello 라이선스 요청에 hello 값을 삽입할 수 있습니다.   

각 content_key_specs hello 옵션 use_policy_overrides_exclusively에 관계 없이 모든 트랙에 대해 지정 되어야 합니다. 

| 이름 | 값 | 설명 |
| --- | --- | --- |
| content_key_specs. track_type |string |트랙 유형 이름입니다. Content_key_specs hello 라이선스 요청에 지정 된 경우 확인 되었는지 toospecify 추적 모든 형식을 명시적으로 합니다. 오류 toodo 하므로 될 오류 tooplayback 지난 10 초 수 있습니다. |
| content_key_specs  <br/> security_level |uint32 |재생에 대한 클라이언트 견고성 요구 사항을 정의합니다. <br/> 1 - 소프트웨어 기반 화이트 박스 암호화가 필요합니다. <br/> 2 - 소프트웨어 암호화 및 난독 처리된 디코더가 필요합니다. <br/> 3-hello 키 재료 및 암호화 작업은 하드웨어 백업 된 신뢰할 수 있는 실행 환경 내에서 수행 되어야 합니다. <br/> 4-암호화 및 콘텐츠의 디코딩 hello 하드웨어 백업 된 신뢰할 수 있는 실행 환경 내에서 수행 되어야 합니다.  <br/> 5-hello 암호화, 디코딩 및 모두 처리 hello 미디어 (압축 및 압축 되지 않은)의 하드웨어 백업 된 신뢰할 수 있는 실행 환경 내에서 처리 되어야 합니다. |
| content_key_specs <br/> required_output_protection.hdc |string - HDCP_NONE, HDCP_V1, HDCP_V2 중 하나 |HDCP가 필요한지 여부를 나타냅니다. |
| content_key_specs <br/>key |Base64  <br/>인코딩된 문자열 |이 트랙에 대 한 콘텐츠 키 toouse 합니다. 지정 하지 않거나 track_type hello key_id가 필요 합니다.  이 옵션을 사용 하면 hello 콘텐츠 공급자 tooinject hello Widevine 라이선스 서버는 키 조회 또는 생성 하도록 하는 대신이 트랙에 대 한 콘텐츠 키입니다. |
| content_key_specs.key_id |Base64 인코딩된 문자열 binary, 16바이트 |Hello 키에 대 한 고유 식별자입니다. |

## <a name="policy-overrides"></a>정책 재정의
| 이름 | 값 | 설명 |
| --- | --- | --- |
| policy_overrides. can_play |boolean. true 또는 false |해당 재생이 나타냅니다 hello의 콘텐츠를 사용할 수 있습니다. 기본값은 false입니다. |
| policy_overrides. can_persist |boolean. true 또는 false |Hello 라이센스 지속형된 toonon 비휘발성 저장소를 오프 라인 수를 나타냅니다. 기본값은 false입니다. |
| policy_overrides. can_renew |boolean. true 또는 false |이 라이선스의 갱신이 허용됨을 나타냅니다. True 인 경우, 하트 비트 하 여 hello 라이선스 기간의 hello를 확장할 수 있습니다. 기본값은 false입니다. |
| policy_overrides. license_duration_seconds |int64 |이 특정 라이선스에 대 한 hello 기간을 나타냅니다. 값이 0 no 제한 toohello 기간 임을 나타냅니다. 기본값은 0입니다. |
| policy_overrides. rental_duration_seconds |int64 |재생은 허용 하는 동안 hello 기간을 나타냅니다. 값이 0 no 제한 toohello 기간 임을 나타냅니다. 기본값은 0입니다. |
| policy_overrides. playback_duration_seconds |int64 |hello 재생 hello 라이선스 기간 내에서 시작 되 면 시간 창을 표시 합니다. 값이 0 no 제한 toohello 기간 임을 나타냅니다. 기본값은 0입니다. |
| policy_overrides. renewal_server_url |string |이 라이선스에 대 한 모든 하트 비트 (갱신) 요청은 toohello 지정한 URL 전송할 합니다. 이 필드는 can_renew가 true인 경우에만 사용할 수 있습니다. |
| policy_overrides. renewal_delay_seconds |int64 |license_start_time 이후, 처음으로 갱신을 시도할 때까지 시간(초)입니다. 이 필드는 can_renew가 true인 경우에만 사용할 수 있습니다. 기본값은 0입니다. |
| policy_overrides. renewal_retry_interval_seconds |int64 |Hello 지연 실패 시 후속 라이선스 갱신 요청 간격 (초) 단위로 지정 합니다. 이 필드는 can_renew가 true인 경우에만 사용할 수 있습니다. |
| policy_overrides. renewal_recovery_duration_seconds |int64 |시간,는 재생 toocontinue 갱신 하는 동안 hello 창이 시도 된 됩니다 아직 toobackend 문제 hello 라이선스 서버를 인해 실패 합니다. 값이 0 no 제한 toohello 기간 임을 나타냅니다. 이 필드는 can_renew가 true인 경우에만 사용할 수 있습니다. |
| policy_overrides. renew_with_usage |boolean. true 또는 false |사용 현황이 시작 될 때 갱신에 대 한 해당 hello 라이선스를 보낼 수는 나타냅니다. 이 필드는 can_renew가 true인 경우에만 사용할 수 있습니다. |

## <a name="session-initialization"></a>세션 초기화
| 이름 | 값 | 설명 |
| --- | --- | --- |
| provider_session_token |Base64 인코딩된 문자열 |이 세션 토큰 hello 라이선스에 다시 전달 하 고 후속 갱신에 존재 합니다.  hello 세션 토큰 세션 이상 유지 되지 않습니다. |
| provider_client_token |Base64 인코딩된 문자열 |클라이언트 hello 라이선스 응답에서 토큰 toosend 합니다.  클라이언트 토큰을 포함 하는 hello 라이선스 요청을 하는 경우이 값은 무시 됩니다. 클라이언트 토큰 hello 라이선스 세션 유지 됩니다. |
| override_provider_client_token |boolean. true 또는 false |클라이언트 토큰을 포함 하는 false이 고 hello 라이선스 요청을 하는 경우이 구조에는 클라이언트 토큰을 지정 하는 경우에 hello 요청에서 hello 토큰을 사용 합니다.  True 인 경우, 항상이 구조에 지정 된 hello 토큰을 사용 합니다. |

## <a name="configure-your-widevine-licenses-using-net-types"></a>.NET 형식을 사용하여 Widevine 라이선스 구성
미디어 서비스는 Widevine 라이선스를 구성할 수 있는 .NET API를 제공합니다. 

### <a name="classes-as-defined-in-hello-media-services-net-sdk"></a>Hello 미디어 서비스.NET SDK에에서 정의 된 대로 클래스
hello 다음은 이러한 유형의 hello 정의 합니다.

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

### <a name="example"></a>예제
hello 방법을 예제와 다음 toouse.NET Api tooconfigure 간단한 Widevine 라이선스입니다.

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


## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>참고 항목
[PlayReady 및/또는 Widevine 동적 일반 암호화 사용](media-services-protect-with-drm.md)

