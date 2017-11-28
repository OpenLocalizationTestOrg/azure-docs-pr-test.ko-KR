---
title: "aaaAzure 릴레이 하이브리드 연결 프로토콜 가이드 | Microsoft Docs"
description: "Azure 릴레이 하이브리드 연결 프로토콜 가이드입니다."
services: service-bus-relay
documentationcenter: na
author: clemensv
manager: timlt
editor: 
ms.assetid: 149f980c-3702-4805-8069-5321275bc3e8
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 2d145d919d606ae4722b063e1baf39fb845a600a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# Azure 릴레이 하이브리드 연결 프로토콜
Azure 릴레이 hello Azure 서비스 버스 플랫폼의 주요 기능 독특하고 hello 중 하나입니다. 새 hello *하이브리드 연결* 릴레이의 기능은 HTTP 및 Websocket 기반 보안, 오픈 프로토콜 발전 합니다. 교체 되는 hello 전자의 경우 동일 하 게 명명 된 *BizTalk 서비스* 된 소유 프로토콜 기반 기능입니다. Azure 앱 서비스에 하이브리드 연결의 hello 통합으로 toofunction 계속-됩니다.

하이브리드 연결을 사용하면 네트워크에 연결된 두 응용 프로그램 간의 양방향 이진 스트림 통신이 가능해지며, 이 통신 중에 양 당사자 중 하나 또는 둘 다가 NAT 또는 방화벽 뒤에 있을 수 있습니다. 이 문서에서는 수신기 및 보낸 사람 역할 및 수신기에서 새 연결을 수락 하는 방법에 대 한 클라이언트 연결에 대 한 hello 하이브리드 연결 릴레이와 hello 클라이언트의 상호 작용을 설명 합니다.

## 상호 작용 모델
두 당사자 hello Azure 클라우드를 파티를 검색 하 고 연결 toofrom 자신의 네트워크의 관점 모두에서 rendezvous 지점을 제공 하 여 연결 하는 hello 하이브리드 연결 릴레이 합니다. Rendezvous 그때 hello, Api 및 hello Azure 포털에서에서이 예제와 기타 문서에 "하이브리드 연결" 라고 합니다. hello 서비스 끝점은 하이브리드 연결 참조 tooas hello "서비스" hello이이 문서의 나머지 부분에 대 한 합니다. hello 상호 작용 모델에 다른 네트워킹 많은 Api가 설정한 hello 명명법 leans 합니다.

먼저 준비 toohandle 들어오는 연결을 나타내며 이후에 도착 했을 때 허용 하는 수신기가 있습니다. 다른 쪽 hello를 hello 수신기를 양방향 통신 경로 설정에 허용 되는 연결 toobe 예상 쪽으로 연결 하는 연결 중인 클라이언트.
"연결", "Listen" 및 "동의" 동일 hello는 대부분에서 찾을 용어 소켓 Api입니다.

모든 릴레이 통신 모델 수신기"hello"도 "클라이언트"에서 colloquial 사용 되 고 다른 용어 오버 로드를 발생 시킬 수 있는 서비스 끝점에 대 한 아웃 바운드 연결을 만드는 어느 쪽을 있습니다. 따라서 하이브리드 연결에 사용 하는 hello 정확한 용어는 다음과 같습니다.

연결의 양쪽 모두에 hello 프로그램 클라이언트 toohello 서비스 이므로 "클라이언트" 라고 합니다. hello 대기 하 고 연결 "수신기"는 또는 허용 하는 클라이언트 있다고 toobe hello "수신기 역할." hello 서비스를 통해 수신기에 대 한 새 연결을 시작 하는 hello 클라이언트 hello "sender" 라고 아니거나 "보낸 사람 역할입니다."

### 수신기 상호 작용
hello 수신기에 4 개의 상호 hello 서비스입니다. 통신에 대 한 세부 정보를 모두 hello 참조 섹션에이 문서의 뒷부분에 설명 되어 있습니다.

#### 수신 대기
tooindicate 준비 toohello 서비스 수신기는 준비 tooaccept 연결 하는 아웃 바운드 WebSocket 연결을 만듭니다. 연결 핸드셰이크가 hello hello 릴레이 네임 스페이스 및 이름을 지정 하는 hello "Listen" 항목을 마우스 오른쪽 단추로 제공 하는 보안 토큰에 구성 된 하이브리드 연결의 hello 이름을 전달 합니다.
WebSocket hello hello 서비스에서 수락 되 면 hello 등록 완료 되 고 hello 설정 웹 WebSocket 모든 후속 상호 작용 사용을 위한 "컨트롤 채널" hello로 활성 상태로 유지 됩니다. hello 서비스 too25 동시 수신기에서 하이브리드 연결을 허용합니다. 두 개 이상의 활성 수신기가 있는 경우 들어오는 연결은 임의의 순서로 균형 조정되지만, 공평하게 배포되지 않을 수 있습니다.

#### 수락
보낸 사람이 hello 서비스에 대 한 새 연결을 열면 hello 서비스를 선택 하 고 hello hello 하이브리드 연결에 활성 수신기 중 하나를 알립니다. 이 알림은 수신기 hello hello WebSocket 끝점의 hello URL을 포함 하는 toofor hello 연결 수락을 연결 해야 하는 JSON 메시지와 hello open 컨트롤 채널을 통해 toohello 수신기를 전송 됩니다.

hello URL 수 및 추가 작업 없이 hello 수신기에서 바로 사용할 수 있어야 합니다.
hello 인코딩 정보는만 hello 보낸 사람으로의 시간 동안에 기본적으로 짧은 기간 동안 유효한은 hello 연결 설정 toobe에 종단 간, 하지만 tooa 최대 30 초를 기꺼이 toowait입니다. hello URL만 하나의 성공적으로 연결 시도 대해 사용할 수 있습니다. 빨리 hello rendezvous URL 설정 되 면이 WebSocket의 모든 작업을 더 이상와 연결에서 릴레이 되는 WebSocket hello 및 개입 또는 hello 서비스에 의해 해석 없이 toohello 보낸 사람입니다.

#### 갱신
hello 보안 토큰을 사용 하는 tooregister hello 수신기 이어야 하며 유지 컨트롤 채널 hello 수신기가 활성 상태인 동안 만료 될 수 있습니다. 토큰 만료 hello 지속적인 연결에는 영향을 주지 않지만 hello 컨트롤 채널 toobe 삭제 또는 만료 hello 순간 직후 hello 서비스에 의해 발생 합니다. hello "갱신" 작업이 hello 컨트롤 채널 유지 관리할 수 있습니다를 장기간 있도록 수신기 hello JSON 메시지를 hello 컨트롤 채널 연관 된 tooreplace hello 토큰을 보낼 수 있습니다.

#### Ping
Hello 컨트롤 채널 hello 방식에 매개 자, 오랜 시간 동안 유휴 상태 유지 되 면 같은 부하 분산 장치 Nat 삭제할 수 있습니다 hello TCP 연결. hello "ping" 작업을 방지 하 되 해당 hello 연결 hello 네트워크 경로에 모든 사용자를 게 미리 알리는 hello 채널에서 적은 양의 데이터를 전송 하 여 toobe 활성화 하 고 hello 수신기에 대 한 "라이브" 테스트도도 사용 합니다. Hello ping이 실패 하면 hello 컨트롤 채널을 사용할 수 없는으로 간주 하 고 hello 수신기에 다시 연결 해야 합니다.

### 발신자 상호작용
hello 보낸 사람 hello 서비스와 단일 상호 작용은만: 연결 합니다.

#### 연결
작업을 "연결" 하는 hello hello 서비스를 제공 하 hello 이름 (필요에 따라 하지만 기본적으로 필요한 경우) 및 hello 하이브리드 연결의 WebSocket hello 쿼리 문자열에 "Send" 권한을 부여 하는 보안 토큰을 엽니다. hello 서비스 다음 방식으로 앞에서 설명한 hello에 hello 수신기와 상호 작용 하 고 hello 수신기가이 WebSocket와 결합 되는 랑 데 부 연결을 만듭니다. Hello WebSocket을 수락한 후 연결 된 수신기와 함께 해당 WebSocket에서 더 이상 모든 상호 작용 됩니다.

### 상호 작용 요약
이 상호 작용 모델의 hello 결과 해당 hello 보낸 클라이언트는 연결 된 tooa 수신기 이며 추가 preambles 없거나 준비 해야 하는 "정리" WebSocket와 핸드셰이크에서 해제 되는입니다. 이 모델의 WebSocket 클라이언트 계층으로 올바르게 생성 된 URL을 제공 하 여 거의 모든 기존 WebSocket 클라이언트 구현 tooreadily 활용 hello 서비스 하이브리드 연결을 통해.

수신기 hello WebSocket accept 상호 작용을 통해 가져오는 hello 랑 데 부 연결 정리 되며 tooany 기존 WebSocket 서버 구현을 "동의"를 구분 하는 일부 최소한의 추가 추상화 된 전달 될 수 있습니다. 프레임 워크의 로컬 네트워크 수신기 및 원격 하이브리드 연결에 대 한 작업 "동의" 작업 합니다.

## 프로토콜 참조

이 섹션의 앞에서 설명한 hello 프로토콜 상호 작용 hello 세부 정보를 설명 합니다.

모든 WebSocket 연결은 일반적으로 일부 WebSocket 프레임워크 또는 API에서 추상화되는 HTTPS 1.1의 업그레이드로 포트 443에서 설정됩니다. 여기의 설명은 특정 프레임워크를 제안하지 않고 중립적으로 구현하는 방법을 설명합니다.

### 수신기 프로토콜
hello 수신기 프로토콜 두 개의 연결 제스처 및 세 가지 메시지 작업으로 구성 됩니다.

#### 수신기 컨트롤 채널 연결
hello 컨트롤 채널을 열에 대 한 WebSocket 연결을 만들기:

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...[&sb-hc-id=...]&sb-hc-token=...
```

hello `namespace-address` 은 호스트 hello hello 폼의 일반적으로 하이브리드 연결을 하는 hello Azure 릴레이 네임 스페이스의 정규화 된 도메인 이름 hello `{myname}.servicebus.windows.net`합니다.

hello 쿼리 문자열 매개 변수 옵션은 다음과 같습니다.

| 매개 변수 | 필수 | 설명 |
| --- | --- | --- |
| `sb-hc-action` |예 |Hello 수신기 역할 hello에 대 한 매개 변수 여야 **sb hc가 동작 = 수신** |
| `{path}` |예 |hello의 hello URL로 인코딩된 네임 스페이스 경로에 하이브리드 연결 tooregister이이 수신기 미리 구성 합니다. 이 식은 고정 추가 toohello `$hc/` 경로 부분입니다. |
| `sb-hc-token` |예\* |hello 수신기를 제공 해야 유효 하 고 URL로 인코딩된 서비스 버스 공유 액세스 토큰을 hello 네임 스페이스 또는 hello를 제공 하는 하이브리드 연결에 대 한 **수신** 오른쪽입니다. |
| `sb-hc-id` |아니요 |이 클라이언트 제공 옵션 ID를 사용하면 종단 간 진단 추적을 수행할 수 있습니다. |

WebSocket 연결이 hello toohello 하이브리드 연결 경로 등록 되었을, 또는 잘못 되었거나 누락 된 토큰 또는 일부 다른 오류로 인해 실패 하면 hello 오류 피드백 hello 일반 HTTP 1.1 상태 피드백 모델을 사용 하 여 제공 됩니다. 상태 설명에는 다음과 같이 Azure 지원 담당자에게 전달될 수 있는 오류 추적 ID를 포함됩니다.

| 코드 | 오류 | 설명 |
| --- | --- | --- |
| 404 |찾을 수 없음 |hello 하이브리드 연결 경로가 유효 하지 않거나 hello 기본 URL의 형식이 잘못 되었습니다. |
| 401 |권한 없음 |hello 보안 토큰이 누락 또는 잘못 되었거나 잘못 되었습니다. |
| 403 |사용할 수 없음 |hello 보안 토큰이이 동작에 대 한이 경로 대해 올바르지 않습니다. |
| 500 |내부 오류 |Hello 서비스에서 발생 했습니다. |

WebSocket 연결 hello 의도적으로 종료 되 hello 서비스에서 적절 한 WebSocket 프로토콜 오류 코드는 추적을 포함 하는 자세한 오류 메시지와 함께 사용 하 여 통신 하는 그 과정에 대 한 hello 이유를 처음 설정한 후 ID입니다. hello 서비스 오류 조건이 발생 없이 컨트롤 채널 아래로 종료 되지 않습니다. 정상적인 종료는 클라이언트를 제어합니다.

| WS 상태 | 설명 |
| --- | --- |
| 1001 |hello 하이브리드 연결 경로 삭제 되거나 사용 하지 않도록 설정 되어 있습니다. |
| 1008 |hello 보안 토큰이 만료 되었습니다, 그리고 따라서 hello 권한 부여 정책 위반 됩니다. |
| 1011 |Hello 서비스에서 발생 했습니다. |

### 핸드셰이크 수락
hello "동의" 알림이 이전에 설정한 컨트롤 채널을 통해 hello 서비스 toohello 수신기에서 WebSocket 텍스트 프레임에서 JSON 메시지를로 전송 됩니다. 회신 toothis 메시지가 되지 않습니다.

hello 메시지에 "동의" 라는 hello이 이번에 다음과 같은 속성을 정의 하는 JSON 개체가 포함 되어 있습니다.

* **주소** – hello WebSocket toothe 서비스 tooaccept 들어오는 연결을 설정 하는 데 사용 되는 URL 문자열 toobe hello 합니다.
* **id** – hello이 연결에 대 한 고유 식별자입니다. Hello 보낸 클라이언트에서 hello ID가 제공 하는 경우 hello 보낸 사람에 게 제공 된 값이 고 그렇지 않으면 시스템 생성 값입니다.
* **connectHeaders** – 되었던 모든 HTTP 헤더 hello Sec WebSocket 프로토콜 및 확장-WebSocket Sec-머리글을 포함 하는 hello 보낸 사람이 toohello 릴레이 끝점을 제공 합니다.

#### 수락 메시지

```json
{                                                           
    "accept" : {
        "address" : "wss://168.61.148.205:443/$hc/{path}?..."    
        "id" : "4cb542c3-047a-4d40-a19f-bdc66441e736",  
        "connectHeaders" : {                                         
            "Host" : "...",                                                
            "Sec-WebSocket-Protocol" : "...",                              
            "Sec-WebSocket-Extensions" : "..."                             
        }                                                            
     }                                                         
}
```

hello 주소 URL hello에서 JSON 메시지를 사용 hello 수신기에서 설정할 수 제공 hello WebSocket을 승인 또는 거부 hello 보낸 소켓에 대 한 합니다.

#### Hello 소켓을 수락합니다.
tooaccept, hello 수신기는 WebSocket 연결 toohello 제공 된 주소를 설정합니다.

Hello "동의" 메시지 수행은 `Sec-WebSocket-Protocol` 헤더로, 해당 프로토콜을 지 원하는 경우에 해당 hello 수신기 hello WebSocket 허용 것으로 예상 합니다. 또한 hello WebSocket 설정으로 hello 헤더를 설정 합니다.

hello에 마찬가지 toohello `Sec-WebSocket-Extensions` 헤더입니다. 필요한 hello의 hello 헤더 toohello 서버 쪽 회신을 설정할지 hello 프레임 워크 확장을 지 원하는 경우 `Sec-WebSocket-Extensions` hello 확장에 대 한 핸드셰이크입니다.

hello URL로 사용 해야-hello를 설정 하는 데는 소켓을 허용 하지만 다음 매개 변수를 포함 합니다.

| 매개 변수 | 필수 | 설명 |
| --- | --- | --- |
| `sb-hc-action` |예 |소켓을 적용 하기 위한 hello 매개 변수 여야 합니다.`sb-hc-action=accept` |
| `{path}` |예 |(다음 단락 뒤에 hello 참조) |
| `sb-hc-id` |아니요 |**ID**에 대한 앞의 설명을 참조하세요. |

`{path}`미리 구성 어떤 tooregister에 하이브리드 연결이이 수신기의 hello hello URL로 인코딩된 네임 스페이스 경로입니다. 이 식은 고정 추가 toothe `$hc/` 경로 부분입니다. 

hello `path` 식은 접미사와 분리 하면 슬래시 후 hello 등록 된 이름 뒤에 오는 쿼리 문자열 식으로 확장 될 수 있습니다. 따라서 가능한 tooinclude HTTP 헤더 없으면 hello 보낸 클라이언트 toopass 디스패치 인수 toohello 수용할 수 있는 활성 수신기를 수 있습니다. hello expectation은 해당 hello 수신기 hello 고정된 경로 부분 및 경로에서 등록 된 이름을 hello 프레임 워크 구문 분석 하 고 만듭니다 hello 나머지 가능 접두사로 쿼리 문자열 인수 없이 `sb-`, 사용 가능한 toohello 응용 프로그램에 대 한 결정 tooaccept hello 연결 여부입니다.

자세한 내용은 "보낸 사람 프로토콜" 섹션을 따라 hello를 참조 하세요.

오류가 없으면 hello 서비스는 다음과 같이 회신할 수 있습니다.

| 코드 | 오류 | 설명 |
| --- | --- | --- |
| 403 |사용할 수 없음 |hello URL이 올바르지 않습니다. |
| 500 |내부 오류 |Hello 서비스에서 발생 했습니다. |

Hello 연결이 설정 된 후 hello 서버 종료 hello WebSocket hello 보낸 WebSocket 종료, 상태를 다음 hello로:

| WS 상태 | 설명 |
| --- | --- |
| 1001 |hello 보낸 클라이언트 hello 연결을 종료합니다. |
| 1001 |hello 하이브리드 연결 경로 삭제 되거나 사용 하지 않도록 설정 되어 있습니다. |
| 1008 |hello 보안 토큰이 만료 되었습니다, 그리고 따라서 hello 권한 부여 정책 위반 됩니다. |
| 1011 |Hello 서비스에서 발생 했습니다. |

#### 거부 된 hello 소켓
검사 "허용" hello 메시지 비슷한 핸드셰이크는 필요 하므로 hello 상태 코드와 hello 거부 이유 흐를 수 통신 상태 설명을 다시 toohello 보낸 후 hello 소켓을 거부 합니다.

hello 프로토콜 디자인 선택 여기는 (즉, 정의 된 오류 상태에 디자인 된 tooend) WebSocket 핸드셰이크 toouse 되므로 수신기 클라이언트 구현 WebSocket 클라이언트에서 toorely를 계속할 수 있으며 추가 사용, HTTP 클라이언트 운영 체제 미 설치 필요가 없습니다.

tooreject hello 소켓, 클라이언트 hello hello "허용" 메시지에서 hello 주소 URI를 사용 하 고 두 쿼리 문자열 매개 변수 tooit를 다음과 같이 추가 합니다.

| 매개 변수 | 필수 | 설명 |
| --- | --- | --- |
| statusCode |예 |숫자 HTTP 상태 코드 |
| statusDescription |예 |Hello 거부에 대 한 사람이 읽을 수 있는 이유입니다. |

결과 URI는 다음 hello tooestablish WebSocket 연결을 사용 합니다.

올바르게 완료한 경우 이 핸드셰이크는 WebSocket이 설정되지 않았기 때문에 HTTP 오류 코드 410과 함께 의도적으로 실패합니다. 문제가 발생 하는 경우 코드를 다음 hello hello 오류 설명:

| 코드 | 오류 | 설명 |
| --- | --- | --- |
| 403 |사용할 수 없음 |hello URL이 올바르지 않습니다. |
| 500 |내부 오류 |Hello 서비스에서 발생 했습니다. |

### 수신기 토큰 갱신
Hello 수신기 토큰이 tooexpire에 대 한 경우 설정 된 hello 컨트롤 채널을 통해 프레임 메시지 toohello 서비스 텍스트를 전송 하 여 바꿀 수 것입니다. 호출 하는 JSON 개체를 포함 하는 메시지 `renewToken`,이 이번에 속성을 다음 hello를 정의 하는:

* **토큰** – 네임 스페이스 또는 hello를 제공 하는 하이브리드 연결에 대 한 유효 하 고 URL로 인코딩된 서비스 버스 공유 액세스 토큰 **수신** 오른쪽입니다.

#### renewToken 메시지

```json
{                                                                                                                                                                        
    "renewToken" : {                                                                                                                                                      
        "token" : "SharedAccessSignature sr=http%3a%2f%2fcontoso.servicebus.windows.net%2fhyco%2f&amp;sig=XXXXXXXXXX%3d&amp;se=1471633754&amp;skn=SasKeyName"  
    }                                                                                                                                                                     
}
```

Hello 토큰 유효성 검사에 실패 하면 액세스가 거부 되었습니다 하 고 hello 클라우드 서비스 오류가 발생 하 여 hello 컨트롤 채널 WebSocket을 닫습니다. 그렇지 않으면 회신이 없습니다.

| WS 상태 | 설명 |
| --- | --- |
| 1008 |hello 보안 토큰이 만료 되었습니다, 그리고 따라서 hello 권한 부여 정책 위반 됩니다. |

## 발신자 프로토콜
hello 보낸 사람 프로토콜 방법은 사실상 동일 toohello 수신기 설정 됩니다.
hello ´ ֲ hello 종단에 대 한 최대 투명도 WebSocket입니다. hello 주소 toois hello와 다른 hello 수신기 하지만 hello "action"의 경우와 동일 하 고 토큰을 연결 하는 다른 권한이 필요 합니다.

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...&sb-hc-id=...&sbc-hc-token=...
```

hello *네임 스페이스 주소* 은 호스트 hello hello 폼의 일반적으로 하이브리드 연결을 하는 hello Azure 릴레이 네임 스페이스의 정규화 된 도메인 이름 hello `{myname}.servicebus.windows.net`합니다.

hello 요청 임의의 HTTP 헤더를 포함 하 여 응용 프로그램 정의 포함할 수 있습니다. 모든 헤더 흐름 toohello 수신기를 제공 하 고 hello에서 확인할 수 있습니다 `connectHeader` 개체의 hello **수락** 제어 메시지입니다.

hello 쿼리 문자열 매개 변수 옵션은 다음과 같습니다.

| 매개 변수 | Required? | 설명 |
| --- | --- | --- |
| `sb-hc-action` |예 |Hello 보낸 사람 역할에 대 한 hello 매개 변수 여야 `action=connect`합니다. |
| `{path}` |예 |(다음 단락 뒤에 hello 참조) |
| `sb-hc-token` |예\* |hello 수신기를 제공 해야 유효 하 고 URL로 인코딩된 서비스 버스 공유 액세스 토큰을 hello 네임 스페이스 또는 hello를 제공 하는 하이브리드 연결에 대 한 **보낼** 오른쪽입니다. |
| `sb-hc-id` |아니요 |사용 가능한 toohello 수신기 hello 백업을 만든 없고 종단 간 진단 추적을 사용할 수는 선택적 ID 핸드셰이크를 수락 합니다. |

hello `{path}` hello의 URL로 인코딩된 네임 스페이스 경로 hello이이 수신기는 tooregister에 하이브리드 연결 미리 구성 됩니다. hello `path` 식 접미사는 쿼리 문자열 식 toocommunicate 추가와 확장 될 수 있습니다. 하이브리드 연결 hello hello 경로 아래에서 등록 되 면 `hyco`, hello `path` 식일 수 있습니다 `hyco/suffix?param=value&...` hello 쿼리 문자열 매개 변수를 여기에 정의 된 옵니다. 그러면 전체 식은 다음과 같을 수 있습니다.

```
wss://{namespace-address}/$hc/hyco/suffix?param=value&sb-hc-action=...[&sb-hc-id=...&]sbc-hc-token=...
```

hello `path` 식 hello 주소 hello "허용" 제어 메시지에 포함 된 URI에에서 toohello 수신기를 통해 전달 됩니다.

WebSocket 연결이 hello 등록 되지 toohello 하이브리드 연결 경로에 잘못 되었거나 누락 된 토큰 또는 일부 다른 오류로 인해 실패할 hello 일반 HTTP 1.1 상태 피드백 모델을 사용 하 여 hello 오류 피드백 제공 됩니다. 상태 설명에는 다음과 같이 Azure 지원 담당자에게 전달될 수 있는 오류 추적 ID를 포함됩니다.

| 코드 | 오류 | 설명 |
| --- | --- | --- |
| 404 |찾을 수 없음 |hello 하이브리드 연결 경로가 유효 하지 않거나 hello 기본 URL의 형식이 잘못 되었습니다. |
| 401 |권한 없음 |hello 보안 토큰이 누락 또는 잘못 되었거나 잘못 되었습니다. |
| 403 |사용할 수 없음 |보안 토큰 hello 하 고이 작업에 대 한이 경로 대해 올바르지 않습니다. |
| 500 |내부 오류 |Hello 서비스에서 발생 했습니다. |

처음으로 설정 된 후 hello 서비스에 의해 hello WebSocket 연결이 종료 되 의도적으로, 이렇게 하면 hello 이유 있으므로 통신 하는 적절 한 WebSocket 프로토콜 오류 코드가 포함 된 자세한 오류 메시지와 함께 사용 하는 추적 id입니다.

| WS 상태 | 설명 |
| --- | --- |
| 1000 |hello 수신기 hello 소켓을 종료합니다. |
| 1001 |hello 하이브리드 연결 경로 삭제 되거나 사용 하지 않도록 설정 되어 있습니다. |
| 1008 |hello 보안 토큰이 만료 되었습니다, 그리고 따라서 hello 권한 부여 정책 위반 됩니다. |
| 1011 |Hello 서비스에서 발생 했습니다. |

## 다음 단계
* [릴레이 FAQ](relay-faq.md)
* [네임스페이스 만들기](relay-create-namespace-portal.md)
* [.NET 시작](relay-hybrid-connections-dotnet-get-started.md)
* [노드 시작](relay-hybrid-connections-node-get-started.md)

