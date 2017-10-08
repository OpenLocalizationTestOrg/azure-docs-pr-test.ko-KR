---
title: "Azure Notification Hubs: FAQ(질문과 대답) | Microsoft Docs"
description: "알림 허브에서 솔루션을 디자인/구현하는 방법과 관련한 FAQ"
services: notification-hubs
documentationcenter: mobile
author: ysxu
manager: erikre
keywords: "푸시 알림, 푸시 알림, iOS 푸시 알림, Android 푸시 알림, iOS 푸시, Android 푸시"
editor: 
ms.assetid: 7b385713-ef3b-4f01-8b1f-ffe3690bbd40
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 01/19/2017
ms.author: yuaxu
ms.openlocfilehash: a70efa7fc5954966847d5a173e9b10accf4b737e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="push-notifications-with-azure-notification-hubs-frequently-asked-questions"></a>Azure Notification Hubs로 푸시 알림: 질문과 대답
## <a name="general"></a>일반
### <a name="what-is-hello-resource-structure-of-notification-hubs"></a>알림 허브의 hello 리소스 구조는 무엇입니까?

Azure Notification Hubs에는 허브 및 네임스페이스라는 두 개의 리소스 수준이 있습니다. 허브는 하나의 응용 프로그램의 hello 플랫폼 간 푸시 정보를 저장할 수 있는 단일 밀어넣기 리소스입니다. 네임스페이스는 한 지역의 허브 컬렉션입니다.

권장되는 매핑은 하나의 네임스페이스를 하나의 앱과 일치시키는 것입니다. 네임스페이스 내에 프로덕션 앱과 작동하는 프로덕션 허브, 테스트 앱과 작동하는 테스트 허브 등이 있을 수 있습니다.

### <a name="what-is-hello-price-model-for-notification-hubs"></a>알림 허브에 대 한 hello 가격 모델은 무엇입니까?
hello 최신 가격 정보에서 확인할 수 있습니다 hello [알림 허브 가격] 페이지. 알림 허브는 hello 네임 스페이스 수준에서 요금이 청구 됩니다. (Hello 정의 네임 스페이스의 "알림 허브의 hello 리소스 구조는 무엇입니까?" 참조) 알림 허브는 3 계층을 제공 합니다.

* **체험**: 이 계층은 푸시 기능을 탐색하기 적절한 시작점입니다. 프로덕션 앱에는 권장되지 않습니다. 네임스페이스마다 매달 500개의 장치와 백만 개의 푸시를 Service Level Agreement(서비스 수준 약정) 보장 없이 받게 됩니다.
* **기본**:이 계층 (또는 표준 계층 hello) 작은 프로덕션 앱에 대 한 것이 좋습니다. 네임스페이스마다 매달 200,000개의 장치와 천만 개의 푸시를 기본으로 받게 됩니다. 할당량 증가 옵션이 포함됩니다.
* **표준**:이 계층 중간 toolarge 프로덕션 앱에 대 한 것이 좋습니다. 네임스페이스마다 매달 천만 개의 장치와 천만 개의 푸시를 기본으로 받게 됩니다. 할당량 증가 옵션 및 다양한 원격 분석 기능이 포함됩니다.

표준 계층 기능:
* **다양 한 원격 분석**: tootrack 알림 허브 당 메시지 원격 분석을 사용할 수 있습니다 디버깅에 대 한 요청 및 플랫폼 알림 시스템 피드백 푸시 하나입니다.
* **다중 테넌트**: 네임스페이스 수준에서 플랫폼 알림 시스템 자격 증명 작업을 수행할 수 있습니다. 이 옵션을 사용 하면 tooeasily hello 내에서 허브로 테 넌 트 분할 동일한 네임 스페이스입니다.
* **푸시 예약**: 언제 든 지 전송 알림을 toobe 예약할 수 있습니다.

### <a name="what-is-hello-notification-hubs-sla"></a>알림 허브 SLA hello 이란?
올바르게 구성 된 응용 프로그램 기본 및 표준 알림 허브 계층에 대 한 푸시 알림을 보낼 하거나 등록 관리 작업을 hello 시간의 99.9% 이상 수행할 수 있습니다. 이동 toohello hello SLA에 대 한 자세한 toolearn [알림 허브 SLA](https://azure.microsoft.com/support/legal/sla/notification-hubs/) 페이지.

> [!NOTE]
> 제 3 자 플랫폼 알림 시스템 (예: Apple APNS 및 Google FCM)에 종속 된 푸시 알림에 이러한 메시지의 배달 hello에 대 한 SLA 아닙니다. 알림 허브는 hello 일괄 처리 tooPlatform 알림 시스템 (보장 된 SLA)을 보낸 후 hello 플랫폼 알림 시스템 toodeliver hello의 hello 책임 푸시합니다 (SLA 보장) 됩니다.

### <a name="which-customers-are-using-notification-hubs"></a>어떤 고객이 알림 허브를 사용하나요?
많은 고객이 Notification Hubs를 사용합니다. 주목할 만한 고객은 여기에 나열되어 있습니다.

* 2014년 소치 동계 올림픽: 수 백 개의 관심 그룹에서 300만 대 이상의 장치를 사용하여 1억 5천만 개 이상의 알림을 2주 동안 디스패치했습니다. [사례 연구: 소치]
* Skanska: [사례 연구: Skanska]
* Seattle Times: [사례 연구: Seattle Times]
* Mural.ly: [사례 연구: Mural.ly]
* 7Digital: [사례 연구: 7Digital]
* Bing Apps: 수 천만 대의 장치에서 매일 3백만 건의 알림을 전송했습니다.

### <a name="how-do-i-upgrade-or-downgrade-my-hub-or-namespace-tooa-different-tier"></a>업그레이드 하거나 내 허브 또는 네임 스페이스 tooa 다른 계층을 다운 그레이드할 어떻게 해야 합니까?
Toohello 이동  **[Azure 포털]** > **알림 허브 네임 스페이스** 또는 **알림 허브**합니다. Hello 리소스 tooupdate을 너무 이동 선택**가격 책정 계층**합니다. 참고 hello 요구 사항:

* hello 가격 책정 계층 업데이트 적용 너무*모든* hello 네임 스페이스를 사용 하는 허브입니다.
* 장치 횟수를 다운 그레이드 하는 hello 계층 hello도 초과 하면 다운 그레이드 먼저 toodelete 장치 필요 합니다.


## <a name="design-and-development"></a>디자인 및 개발
### <a name="which-server-side-platforms-do-you-support"></a>어떤 서버 쪽 플랫폼을 지원하나요?
.NET, Java, Node.js, PHP 및 Python용 서버 SDK가 제공됩니다. Notification Hubs API는 REST 인터페이스를 기반으로 하므로 다양한 플랫폼을 사용하거나 추가 종속성을 원하지 않는 경우 REST API로 직접 작업할 수 있습니다. 자세한 내용은 toohello 이동 [알림 허브 REST Api] 페이지.

### <a name="which-client-platforms-do-you-support"></a>어떤 클라이언트 플랫폼이 지원되나요?
푸시 알림은 [iOS](notification-hubs-ios-apple-push-notification-apns-get-started.md), [Android](notification-hubs-android-push-notification-google-gcm-get-started.md), [Windows 유니버설](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md), [Windows Phone](notification-hubs-windows-mobile-push-notifications-mpns.md), [Kindle](notification-hubs-kindle-amazon-adm-push-notification.md), [Android China(Baidu 제공)](notification-hubs-baidu-china-android-notifications-get-started.md), Xamarin([iOS](xamarin-notification-hubs-ios-push-notification-apns-get-started.md) 및 [Android](xamarin-notification-hubs-push-notifications-android-gcm.md)), [Chrome Apps](notification-hubs-chrome-push-notifications-get-started.md) 및 [Safari](https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSafari)에 대해 지원됩니다. 자세한 내용은 toohello 이동 [알림 허브 시작 자습서] 페이지.

### <a name="do-you-support-text-message-email-or-web-notifications"></a>문자 메시지, 전자 메일, 웹 알림이 지원되나요?
알림 허브에는 기본적으로 디자인 된 toosend 알림 toomobile 앱입니다. 전자 메일 또는 문자 메시지 기능은 제공하지 않습니다. 그러나 이러한 기능을 제공 하는 타사 플랫폼과 통합 될 수 있습니다 toosend 네이티브 푸시 알림을 알림 허브를 사용 하 여 [모바일 앱]합니다.

또한 알림 허브는 hello 초기 브라우저에서 푸시 알림 배달 서비스를 제공 하지 않습니다. 고객 지원 hello 서버 측 플랫폼 기반으로 SignalR을 사용 하 여이 기능을 구현할 수 있습니다. Hello 크롬 샌드박스에서 toosend 알림 toobrowser 앱을 원하는 경우 참조 hello [크롬 앱 자습서]합니다.

### <a name="how-are-mobile-apps-and-azure-notification-hubs-related-and-when-do-i-use-them"></a>Mobile Apps와 Azure Notification Hubs는 어떻게 관련성이 있으며 이 두 항목은 각각 어떤 경우에 사용해야 하나요?
기존의 모바일 응용 프로그램을 다시 종료 하 고 tooadd만 hello 기능 toosend 푸시 알림을, Azure 알림 허브를 사용할 수 있습니다. 처음부터 모바일 앱 백 엔드를 tooset 하려는 경우에 hello Azure 앱 서비스 모바일 앱 기능을 사용 하는 것이 좋습니다. 모바일 앱 hello 모바일 앱 백 엔드에서 푸시 알림을 쉽게 보낼 수 있도록 자동으로 알림 허브를 제공 합니다. 모바일 앱에 대 한 가격 책정 hello 알림 허브에 대 한 기본 요금에 포함 됩니다. 푸시 포함 하는 hello를 초과 하는 경우에 지불 합니다. 에 대 한 자세한 내용은 비용, toohello 이동 [앱 서비스 가격 책정] 페이지.

### <a name="how-many-devices-can-i-support-if-i-send-push-notifications-via-notification-hubs"></a>알림 허브를 통해 푸시 알림을 보낼 경우 얼마나 많은 장치를 지원할 수 있나요?
Toohello 참조 [알림 허브 가격] hello 수가 지원 되는 장치에 대 한 자세한 내용은 합니다.

천만 개 이상의 등록된 장치에 대한 지원이 필요한 경우 직접 [문의](https://azure.microsoft.com/overview/contact-us/)하여 솔루션을 확장하도록 합니다.

### <a name="how-many-push-notifications-can-i-send-out"></a>보낼 수 있는 푸시 알림 수는 몇 개인가요?
Hello 선택한 계층에 따라 Azure 알림 허브를 자동으로 조정 hello 시스템을 통과 하는 알림의 hello 수에 따라 합니다.

> [!NOTE]
> hello 전반적인 사용 비용 늘릴 수 개의 푸시 알림 전달 하기 hello 수를 기반 합니다. Hello에 설명 된 hello 계층 제한의 인식 하 고 있는지 확인 [알림 허브 가격] 페이지.
> 
> 

고객이 알림 허브 toosend 수백만 개의 푸시 알림을 매일 사용 합니다. 없는 toodo 아무 것도 특별 한 tooscale hello Azure 알림 허브를 사용 하는 상태로, 푸시 알림의 도달 합니다.

### <a name="how-long-does-it-take-for-sent-push-notifications-tooreach-my-device"></a>시간에 대 한 take 보낸 푸시 알림을 tooreach 장치?
일반적인 사용 시나리오에서는 hello 들어오는 부하 일관이 고, Azure 알림 허브 이상 처리할 수 *1 백만 푸시 알림을 보내는 1 분*합니다. 이 속도 태그의 hello 수, hello 특성 hello 들어오는 보냅니다 및 기타 외부 요인에 따라 달라질 수 있습니다.

Hello 예상 배달 시간 동안 hello 서비스는 hello 대상 플랫폼 마다 계산 하 고 메시지 toohello 푸시 알림 서비스 (PNS) hello 등록 태그 또는 태그 식에 따라 라우팅합니다. hello hello PNS toosend 알림 toohello 장치의 합니다.

PNS hello 알림을 배달 하기 위한 모든 SLA를 보장 하지 않습니다. 그러나 대부분의 푸시 알림은 tooNotification 허브 보내지는 hello 시간부터 (일반적으로 10 분) 이내에 몇 분 안에 tootarget 장치를 배달 됩니다. 몇 가지 알림에 더 많은 시간이 소요될 수 있습니다.

> [!NOTE]
> Azure 알림 허브에 정책이 toodrop 장소에에서 모든 푸시 알림이 PNS toohello 30 분 내에 배달 되지 않습니다. 이 지연에 대 한 여러 가지 이유로 발생할 수 있습니다 하지만 hello PNS에서 응용 프로그램을 조정 하기 때문에 일반적으로 대부분 합니다.
> 
> 

### <a name="is-there-any-latency-guarantee"></a>대기 시간 보장이 있나요?
푸시 알림 (외부, 플랫폼별 PNS에서 배달)에서는 hello 이기 때문에 보장이 없습니다 대기 시간입니다. 일반적으로 몇 분 안에 hello 대부분의 푸시 알림 전달 해야 합니다.

### <a name="what-do-i-need-tooconsider-when-designing-a-solution-with-namespaces-and-notification-hubs"></a>무엇을 네임 스페이스 및 알림 허브와 솔루션을 설계할 때 tooconsider 필요 한가요?
#### <a name="mobile-appenvironment"></a>모바일 앱/환경
* 환경당 모바일 앱마다 알림 허브를 하나씩 사용합니다.
* 다중 테넌트 시나리오에서는 각 테넌트에 별도의 허브가 있어야 합니다.
* 되지 공유 hello 프로덕션 환경과 테스트 환경에 대 한 동일한 알림 허브입니다. 이 경우 알림을 보낼 때 문제를 일으킬 수 있습니다. (Apple에서는 각기 별도의 자격 증명을 사용하는 샌드박스 및 프로덕션 푸시 끝점을 제공합니다.)
* 기본적으로 hello Azure 포털을 통해 테스트 알림을 tooyour 등록 된 장치를 보낼 수도 있고 Visual Studio에서 Azure 통합된 구성 요소를 hello 수 있습니다. hello 임계값 hello 등록 풀에서 임의로 선택 된 too10 장치 설정 됩니다.

> [!NOTE]
> 허브 Apple 샌드박스 인증서 사용 하 여 원래 구성 했 고 다음 다시 구성 된 toouse Apple 프로덕션 인증서 인 경우 hello 원래 장치 토큰을 유효 하지 않습니다. 잘못 된 토큰에는 푸시 toofail을 발생 합니다. 프로덕션 환경과 테스트 환경을 분리하고 각기 환경에 서로 다른 허브를 사용합니다.
> 
> 

#### <a name="pns-credentials"></a>PNS 자격 증명
Apple, Google 등의 플랫폼 개발자 포털에 모바일 앱을 등록하면 앱 식별자 및 보안 토큰이 전송됩니다. hello 앱 백 엔드 제공 이러한 PNS 토큰 toohello 플랫폼의 푸시 알림을 toodevices 전송 될 수 있도록 합니다. 보안 토큰 hello 형태의 인증서 (예를 들어 Apple iOS 또는 Windows Phone) 또는 보안 키 (예: Google Android 또는 Windows) 될 수 있습니다. 이들은 알림 허브에서 구성해야 합니다. Hello 알림 허브 수준에서 구성은 일반적으로 수행 되지만 다중 테 넌 트 시나리오에서 hello 네임 스페이스 수준에서 수행할 수도 있습니다.

#### <a name="namespaces"></a>네임스페이스
네임스페이스를 배포 그룹화에 사용할 수 있습니다. 도 사용할 수 toorepresent 사용 되는 모든 알림 허브의 모든 테 넌 트에 대 한 다중 테 넌 트 시나리오에서 동일한 앱 hello 합니다.

#### <a name="geo-distribution"></a>지역 배포
지역 배포가 푸시 알림 시나리오에서 반드시 중요한 것은 아닙니다. 푸시 알림 toodevices 전달 하는 다양 한 PNSes (APNS, GCM 등) 고르게 분산 되지 않습니다.

전역적으로 사용 되는 응용 프로그램의 경우에 hello 전 세계 다양 한 Azure 지역에서 hello 알림 허브 서비스를 사용 하 여 다른 네임 스페이스에 허브를 만들 수 있습니다.

> [!NOTE]
> 관리 비용(특히, 등록에)이 늘어날 수 있으므로 이러한 배열은 권장하지 않습니다. 명시적인 수요가 있는 경우에만 수행해야 합니다.
> 
> 

### <a name="should-i-do-registrations-from-hello-app-back-end-or-directly-through-client-devices"></a>실행할 등록 hello 앱 백 엔드에서 또는 클라이언트를 통해 직접 장치 작업
Hello 앱 백 엔드에서 등록은 hello 등록을 만들기 전에 tooauthenticate 클라이언트가 있는 경우에 유용 합니다. 생성 또는 hello 앱 백 엔드 응용 프로그램 논리를 기반으로 수정 해야 하는 태그에 있는 경우에 유용 합니다. 자세한 내용은 toohello 이동 [백 엔드 등록 지침] 및 [백 엔드 등록 지침 2] 페이지입니다.

### <a name="what-is-hello-push-notification-delivery-security-model"></a>Hello 푸시 알림 배달 보안 모델은 무엇입니까?
Azure Notification Hubs에서는 [공유 액세스 서명](../storage/common/storage-dotnet-shared-access-signature-part-1.md) 기반 보안 모델을 사용합니다. Hello 루트 네임 스페이스 수준에서 또는 hello 세분화 된 알림 허브 수준에서 hello 공유 액세스 서명 토큰을 사용할 수 있습니다. 공유 액세스 서명 토큰 toosend 메시지 사용 권한 또는 toolisten 알림 사용 권한에 대 한 예를 들어 집합 toofollow 다양 한 권한 부여 규칙 사용 될 수 있습니다. 자세한 내용은 참조 hello [알림 허브 보안 모델] 문서.

### <a name="how-should-i-handle-sensitive-payload-in-push-notifications"></a>푸시 알림의 중요한 페이로드를 어떻게 처리해야 하나요?
모든 알림이 PNS hello 플랫폼으로 tootarget 장치 배달 됩니다. 처리 되 고 toohello 통과 tooAzure 알림 허브에는 알림이 전송 될 때 해당 PNS 합니다.

Hello 보낸 사람 toohello Azure 알림 허브 toohello PNS에서에서 모든 연결에 HTTPS를 사용 합니다.

> [!NOTE]
> Azure 알림 허브는 어떤 방식으로든에서 hello 페이로드 메시지를 기록 하지 않습니다.
> 
> 

toosend 중요 한 페이로드 푸시 Secure 패턴을 사용 하는 것이 좋습니다. hello 보낸 사람 없이 hello 페이로드 메시지 식별자 toohello 장치와 ping 알림을 제공합니다. Hello 장치에서 앱 hello hello 페이로드를 받으면 hello 앱 toofetch hello 메시지 정보 직접 보안 API를 호출 합니다. 에 어떻게 tooimplement이 패턴을 사용 하 여 지침을 이동 toohello [알림 허브 푸시 Secure 자습서] 페이지.

## <a name="operations"></a>작업
### <a name="what-support-is-provided-for-disaster-recovery"></a>재해 복구에는 어떤 지원이 제공되나요?
(Hello 알림 허브 이름, hello 연결 문자열 및 기타 중요 한 정보) 저희 쪽에서 재해 복구 검사 메타 데이터를 제공합니다. 등록 데이터는 hello 재해 복구 시나리오 트리거되면 *만 세그먼트* 손실 되는 hello 알림 허브 인프라의 합니다. 새 허브 후 복구에이 데이터 tooimplement 솔루션 toorepopulate이 필요 합니다.

1. 다른 데이터 센터에서 보조 알림 허브를 만듭니다. Hello 시작 tooshield부터 다시 만드는지에 권장에서 재해 복구 이벤트 관리 기능에 영향을 줄 수 있습니다. Hello 재해 복구 이벤트의 hello 번에 하나씩 만들 수 있습니다.

2. 기본 알림 허브에서 hello 등록 된 hello 보조 알림 허브를 채웁니다. 등록으로 제공 하는 대로 동기화 유지 하 고 두 허브에서 toomaintain 등록 시도 권장 하지 않는 우리 됩니다. 이 연습 hello PNS 측면에서 등록 tooexpire의 hello 내재 된 경향이 때문에 제대로 작동 하지 않습니다. 만료되거나 잘못된 등록에 대한 PNS 피드백이 수신되면 Notification Hubs에서는 해당 등록을 정리합니다.  

앱 백 엔드에 대해서는 두 가지 권장 사항이 있습니다.

* 끝에는 주어진 등록 집합을 유지 관리하는 앱 백 엔드를 사용하세요. 그런 다음 hello 보조 알림 허브에은 대량 삽입을 수행할 수 있습니다.

* 백업으로 hello 기본 알림 허브 등록의 일반 덤프 하는 앱 백 엔드를 사용 합니다. 그런 다음 hello 보조 알림 허브에은 대량 삽입을 수행할 수 있습니다.

> [!NOTE]
> Hello 표준 계층에서 사용할 수 있는 등록 내보내기/가져오기 기능 hello에 설명 되어 [등록 내보내기/가져오기] 문서.
> 
> 

없다면 백 엔드 hello 앱 대상 장치에서 시작 될 때, 새 등록을 수행 하며 hello 보조 알림 허브의 합니다. 결국 hello 보조 알림 허브에 등록 된 모든 hello 활성 장치 갖습니다.

앱이 열리지 않은 장치가 알림을 수신하지 않을 때 시간 간격이 있게 됩니다.

### <a name="is-there-audit-log-capability"></a>감사 로그 기능이 있나요?
모든 알림 허브 관리 작업 hello에 노출 된 toooperation 로그 이동 [Azure 클래식 포털]합니다.

## <a name="monitoring-and-troubleshooting"></a>모니터링 및 문제 해결
### <a name="what-troubleshooting-capabilities-are-available"></a>어떤 문제 해결 기능이 제공되나요?
Azure 알림 허브는 특히 삭제 된 알림 hello 가장 일반적인 시나리오에 대 한 문제 해결을 위한 몇 가지 기능을 제공 합니다. 자세한 내용은 참조 hello [알림 허브 문제 해결] 백서에 나와 있습니다.

### <a name="what-telemetry-features-are-available"></a>어떤 원격 분석 기능이 제공되나요?
Azure 알림 허브 사용 원격 분석 데이터 보기 hello에 [Azure 클래식 포털]합니다. Hello 메트릭에 대 한 세부 정보 hello에서 사용할 수 있는 [알림 허브 메트릭] 페이지.

> [!NOTE]
> 알림 성공 의미는 푸시 알림을 배달 toohello 단순히 외부 PNS Google의 GCM 또는 (예를 들어 APNS apple). hello hello PNS toodeliver hello 알림 tootarget 장치 합니다. 일반적으로 hello PNS 배달 메트릭 toothird 파티를 노출 하지 않습니다.  
> 
> 

프로그래밍 방식으로 (hello 표준 계층) hello 기능 tooexport hello 원격 분석 데이터도 제공 합니다. 자세한 내용은 참조 hello [알림 허브 메트릭 샘플]합니다.

[Azure 클래식 포털]: https://manage.windowsazure.com
[알림 허브 가격]: http://azure.microsoft.com/pricing/details/notification-hubs/
[Notification Hubs SLA]: http://azure.microsoft.com/support/legal/sla/
[사례 연구: 소치]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=7942
[사례 연구: Skanska]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5847
[사례 연구: Seattle Times]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=8354
[사례 연구: Mural.ly]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=11592
[사례 연구: 7Digital]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=3684
[알림 허브 REST Api]: https://msdn.microsoft.com/library/azure/dn530746.aspx
[알림 허브 시작 자습서]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[크롬 앱 자습서]: http://azure.microsoft.com/documentation/articles/notification-hubs-chrome-get-started/
[Mobile Services Pricing]: http://azure.microsoft.com/pricing/details/mobile-services/
[백 엔드 등록 지침]: https://msdn.microsoft.com/library/azure/dn743807.aspx
[백 엔드 등록 지침 2]: https://msdn.microsoft.com/library/azure/dn530747.aspx
[알림 허브 보안 모델]: https://msdn.microsoft.com/library/azure/dn495373.aspx
[알림 허브 푸시 Secure 자습서]: http://azure.microsoft.com/documentation/articles/notification-hubs-aspnet-backend-ios-secure-push/
[알림 허브 문제 해결]: http://azure.microsoft.com/documentation/articles/notification-hubs-diagnosing/
[알림 허브 메트릭]: https://msdn.microsoft.com/library/dn458822.aspx
[알림 허브 메트릭 샘플]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel
[등록 내보내기/가져오기]: https://msdn.microsoft.com/library/dn790624.aspx
[Azure 포털]: https://portal.azure.com
[complete samples]: https://github.com/Azure/azure-notificationhubs-samples
[모바일 앱]: https://azure.microsoft.com/services/app-service/mobile/
[앱 서비스 가격 책정]: https://azure.microsoft.com/pricing/details/app-service/
