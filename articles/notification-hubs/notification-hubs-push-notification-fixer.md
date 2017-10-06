---
title: "알림 허브-aaaAzure 진단 지침"
description: "Azure 알림 허브와 toodiagnose 공통 발급 하는 방법에 대 한 지침입니다."
services: notification-hubs
documentationcenter: Mobile
author: ysxu
manager: erikre
editor: 
ms.assetid: b5c89a2a-63b8-46d2-bbed-924f5a4cce61
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: NA
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: e374278f2bfdfad36ba091e8846059cd184c17ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs---diagnosis-guidelines"></a>Azure 알림 허브 - 진단 지침
## <a name="overview"></a>개요
Azure 알림 허브 고객의 도움을 주신 hello 가장 일반적인 질문 중 하나는 해당 응용 프로그램 백 엔드에서 보낸 알림의 표시 되지 않는 이유 아웃 toofigure hello 클라이언트 장치에 표시 되는 방식을 알림은 삭제 된 위치와 이유 및 방법 toofix이 있습니다. 이 문서에서 살펴보겠습니다 hello 알림을 삭제 되거나 끝나지 않는 이유는 다양 한 이유로 hello 장치에 있습니다. 또한 분석 하 고 hello 근본 원인을 알아낼 수 있는 방법을 통해 볼 수 있습니다. 

우선,는 중요 한 toounderstand 알림 toohello 장치 Azure 알림 허브를 푸시하는 방법
![][0]

Hello에서 일반적인 송신 알림 흐름 hello 메시지를 보내 **응용 프로그램 백 엔드** 너무**Azure 알림 허브 (NH)** 차례로 고려 하는 모든 hello 등록에 약간의 처리를 수행 하는 계정 hello 즉, 모든 hello 등록 tooreceive hello 푸시 알림이 필요로 하는 태그 및 태그 식 toodetermine "대상 으로" 구성 합니다. 이러한 등록은 지원되는 일부 또는 모든 플랫폼(iOS, Google, Windows, Windows Phone, Kindle 및 중국 Android용 Baidu)에 적용될 수 있습니다. NH 다음 푸시 알림을, 등록, 특정 toohello 장치 플랫폼의 여러 일괄 처리에서 분할 hello 대상, 설정 되 면 **푸시 알림 서비스 (PNS)** -Apple의 APNS, GCM Google 등에 대 한 예입니다. NH는 hello 알림 허브 구성 페이지에서 hello Azure 클래식 포털에서에서 설정 하는 hello 자격 증명을 기반으로 하는 각 PNS hello로 인증 합니다. hello PNS에는 다음 각 hello 알림을 toohello 전달 **클라이언트 장치**합니다. 이것은 hello 플랫폼 toodeliver 푸시 알림 방법 및 참고는 hello 알림 배달의 최종 레그 hello 플랫폼 PNS 및 hello 장치 간에 발생 하는 것이 좋습니다. 따라서 4가지 주요 구성 요소(*클라이언트*, *응용 프로그램 백 엔드*, *Azure Notification Hubs(NH)* 및 *푸시 알림 서비스(PNS)*)가 있으며 이러한 알림은 삭제될 수 있습니다. 이 아키텍처에 대한 자세한 내용은 [Notification Hubs 개요]에서 확인할 수 있습니다.

오류 toodeliver 알림을 테스트/준비 단계 또는 구성 문제를 나타낼 수 있는의 일부 또는 모두이 알림을 hello 프로덕션 환경에서 발생할 수 있습니다 hello 초기 하는 동안 발생할 수 있습니다 가져오기 끊길 깊은 일부 응용 프로그램을 나타내는 또는 메시징 패턴 문제입니다. Hello 섹션에서 아래 살펴보겠습니다 다양 한 삭제 알림 시나리오에서 일반적인 toohello 드문 종류 중 일부를 사용할 수 있습니다 명백한 및 일부 다른 많은 양의 하지 사이의 값입니다. 

## <a name="azure-notifications-hub-mis-configuration"></a>Azure 알림 허브의 잘못된 구성
Azure 알림 허브가 필요한 tooauthenticate 자체 hello 컨텍스트에서 hello 개발자 응용 프로그램 toobe 수 toosuccessfully 송신 알림 toohello의 각 PNS 합니다. 이 가능 hello 개발자 hello 각 플랫폼 (예: Google, 사과, Windows 등)와 개발자 계정을 만들고 다음 알림에서 hello 포털에서 구성할 toobe 필요한 자격 증명을 받게 응용 프로그램을 등록 하 여 허브 구성 섹션입니다. 경우 알림이 표시 되지 않습니다는 hello 올바른 자격 증명 hello hello 응용 프로그램과 일치 하는 알림 허브에에서 구성 된 tooensure 아래 만들어야 플랫폼 특정 개발자 계정으로, 첫 번째 단계를 통해 설정 됩니다. 있습니다.이 [시작 자습서] 단계별 방식으로이 프로세스를 보다 유용 toogo 합니다. 다음은 잘못된 구성의 몇가지 예입니다.

1. **일반**
   
    ) 동일 하면 알림 허브 이름 (입력 오류) 없이 hello는 있는지:
   
   * Hello 클라이언트에서 등록 하는 
   * Hello 백 엔드에서 알림을 보내는 위치  
   * Hello PNS 자격 증명을 구성한 및 
   * 에 구성 된 SAS 자격 증명에는 클라이언트와 hello 백 엔드를 hello 합니다. 
     
     b) hello 클라이언트와 응용 프로그램 백 엔드 hello에서 올바른 SAS 구성 문자열 hello를 사용 하 고 있는지 합니다. 으로 규칙을 사용 해야 hello **DefaultListenSharedAccessSignature** hello 클라이언트 및 **DefaultFullSharedAccessSignature** (주는 권한 toobe hello 응용 프로그램 백 엔드에 수 toosend 알림 toohello NH)
2. **Apple 푸시 알림 서비스(APNS) 구성**
   
    서로 다른 2개의 허브를 유지해야 하는데, 하나는 프로덕션에 다른 하나는 테스트 목적으로 유지해야 합니다. 즉, 샌드박스 환경 tooa 별도 허브 및 프로덕션 tooa 별도 허브에서 toouse 보아야 hello 인증서 toouse 보아야 hello 인증서를 업로드 하는 것을 의미 합니다. Tooupload 다양 한 유형의 인증서 toohello 마십시오으로 동일한 허브는 hello 줄 아래로 알림 오류가 발생할 수 있습니다. 여기서 다양 한 유형의 인증서 toohello 실수로 업로드 한 위치에서 직접 찾을 같은 허브 것이 좋습니다 toodelete hello 허브 및 새로 시작 합니다. 어떤 이유로 든 원하는 경우에 없는 hello에 다음 수 toodelete hello 허브 매우 이상, hello 허브에서 모든 hello 기존 등록을 삭제 해야 합니다. 
3. **메시징 GCM(Google Cloud) 구성** 
   
    a) 클라우드 프로젝트에서 "Android용 Google 클라우드 메시징"을 설정했는지 확인합니다. 
   
    ![][2]
   
    b)을 만들어야 합니다 "서버 키" 어떤 NH hello 자격 증명을 가져올 GCM과 tooauthenticate 사용 됩니다. 
   
    ![][3]
   
    c) hello 클라이언트 hello 대시보드에서 얻을 수 있는 완전히 숫자 엔터티는 "프로젝트 ID"를 구성 합니다.
   
    ![][1]

## <a name="application-issues"></a>응용 프로그램 문제
1) **태그/태그 식**

태그 또는 태그 식 toosegment 대상 그룹을 사용할 경우 있기 항상 hello 알림을 보낼 때 한지 대상이 송신 호출에서 지정 하는 hello 태그/태그 식을 기반으로 찾을 수 없습니다. 이 가장 좋습니다 tooreview는 사용자 등록 tooensure 태그가 있는 일치 알림을 전송 하 고 다음 해당 등록으로 hello 클라이언트 에서만에서 hello 알림을 확인 메일을 확인 합니다. 예: 태그 "정치" 말 NH 있는 프로그램 등록 작업을 완료 된 모든 태그와 알림 "스포츠" 보내는 경우이 전송 되지 않습니다 tooany 장치입니다. 복잡한 경우에는 "태그 A" 또는 "태그 B"로만 등록한 태그 식뿐만 아니라 "태그 A && 태그 B"를 대상으로 알림을 보내는 경우도 포함될 수 있습니다. Hello에 자체 팁 섹션 아래의 진단, 가지가 서로 hello 태그와 함께 사용자 등록을 검토할 수 있습니다. 

2) **템플릿 문제**

템플릿을 사용 하는 다음에 설명 된 hello 지침을 따르는 확인 [템플릿 지침]합니다. 

3) **잘못된 등록**

알림 허브가 올바르게 구성 된 hello 및 모든 태그/태그 식을 올바르게 hello 찾기 toowhich hello 알림을 toobe 전송 해야 하는 유효한 대상의 발생을 사용한 경우 NH를 발생 시킵니다 동시-각 일괄 처리에에서 여러 개의 처리 일괄 처리 등록 tooa 집합 메시지를 보냅니다. 

> [!NOTE]
> 병렬에서 처리 hello지 않습니다 것, 이후 hello 순서는 hello 알림을 배달할 수를 보장 하지는 않습니다 했습니다. 
> 
> 

이제 Azure 알림 허브는 "최대 한 번의" 메시지 전달 모델에 대해 최적화되었습니다. 즉,를 알림이 없는 두 번 이상 tooa 장치 배달 되는 중복 제거를 시도 했습니다. tooensure hello 등록 전체를 검사 하 고 하나의 메시지만 확인이 실제로 보내는 hello 메시지 toohello PNS 하기 전에 장치 식별자 당 전송 됩니다. 을 각 일괄 처리 toohello PNS에서 수락 하는 다시 전송 되 고 hello 등록 유효성 검사, 있기 hello PNS 해당 일괄 처리에서 하나 이상의 hello 등록 오류가 검색 오류 tooAzure NH 반환 하 고 있으므로 삭제 하는 처리를 중지합니다 완전히 일괄 처리입니다. TCP 스트림 프로토콜을 사용하는 APNS와 특히 유용합니다. 한 번 대부분에 대 한 최적화 된 것 이지만 배달 주소를 제거 하는이 경우의 hello 우리의 데이터베이스와 다음 해당 일괄 처리에서 hello 장치 hello 나머지 부분에 대 한 알림 배달을 다시 시도에서 오류가 있는 등록 합니다.

Hello Azure 알림 허브 REST Api를 사용 하 여 등록에 대 한 배달 실패 시도 hello에 대 한 오류 정보를 가져올 수 있습니다: [메시지 원격 분석: 알림 메시지 원격 분석 가져오기](https://msdn.microsoft.com/library/azure/mt608135.aspx) 및 [PNS 피드백](https://msdn.microsoft.com/library/azure/mt705560.aspx). Hello 참조 [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample) 예를 들어 코드입니다.

## <a name="pns-issues"></a>PNS 문제
hello 알림 메시지를 받은 후 해당 책임 toodeliver hello 알림 toohello 장치는 해당 PNS hello 합니다. Azure 알림 허브가 hello 그림을 추가 벗어나 hello 알림을 toobe toohello 장치 배달 될 경우는 제어 하지 않습니다. Hello 플랫폼 알림 서비스와 매우 강력한 되므로 알림은 hello PNS에서에서 tooreach hello 장치를 몇 초 후에 수행 합니다. 그러나 Hello PNS에서 조정 하는 경우 다음 Azure 알림 허브가 적용 된 지 수 백오프 전략 있고, hello PNS 30 분에 연결할 수 없는 유지 되는 정책에서 tooexpire 놓고 이러한 메시지를 영구적으로 삭제 합니다. 

PNS toodeliver 알림을 시도 하는 경우 hello 장치가 오프 라인이 hello 알림 시간 제한 된 기간에 대 한 hello PNS에서 저장 되 고 toohello 장치를 사용할 수 있을 때 배달 합니다. 특정 앱에 대한 최근 알림 하나만 저장됩니다. 각 새로운 알림이 hello 장치가 오프 라인 상태인 동안 여러 알림을 보내기 하면 hello 사전 통지 toobe 삭제 됩니다. Hello 최신 알림만 유지 합니다.이 동작은 APNS에서 알림을 통합 하 고 축소 (축소 키를 사용 하 여)는 GCM에서 참조 된 tooas 합니다. 오랜 시간 동안 hello 장치가 오프 라인 상태인 경우에 대 한 목록만 저장 하는 모든 알림이 삭제 됩니다. 소스 - [APNS 지침] & [GCM 지침]

Azure 알림 허브-와 결합 키 hello 제네릭을 사용 하 여 HTTP 헤더를 통해 전달할 수 있습니다 `SendNotification` API (예: –.NET SDK에 대 한 `SendNotificationAsync`) toohello은으로 전달 되는 HTTP 헤더를 사용 하 해당 PNS 합니다. 

## <a name="self-diagnose-tips"></a>자체 진단 팁
여기에 살펴보겠습니다 hello 다양 한 수단 toodiagnose 및 모든 알림 허브 문제 원인:

### <a name="verify-credentials"></a>자격 증명 확인
1. **PNS 개발자 포털**
   
    Hello 해당 PNS 개발자 포털 (APNS, GCM, WNS 등)을 사용 하 여 정보를 확인할 우리의 [시작 자습서]합니다.
2. **Azure 클래식 포털**
   
    구성 탭 tooreview toohello 이동한 다음 hello PNS 개발자 포털에서 가져온 설정과 hello 자격 증명과 일치 합니다. 
   
    ![][4]

### <a name="verify-registrations"></a>등록 확인
1. **Visual Studio**
   
    개발을 위한 Visual Studio를 사용 하는 경우 Azure tooMicrosoft 뷰와 연결할 고 "서버 탐색기" 알림 허브를 포함 한 Azure 서비스를 관리할 수 있습니다. 개발/테스트 환경에서 주로 유용합니다. 
   
    ![][9]
   
    보고 하 고 플랫폼, 네이티브 또는 템플릿 등록, 태그, PNS 식별자, 등록 id와 hello 만료 날짜에 대 한 분류 원활 하 게 되는 허브의 모든 hello 등록을 관리할 수 있습니다. 또한 hello 신속 하 게-tooedit는 태그를 원하는 경우에 예를 들어 유용 등록을 편집할 수 있습니다. 
   
    ![][8]
   
   > [!NOTE]
   > Visual Studio 기능 tooedit 등록은 등록의 수가 적은 개발/테스트 중에 사용 해야 합니다. 대량, 사용자 등록 고려 발생 필요 toofix 있을 경우 여기에서 설명 하는 hello 내보내기/가져오기 등록 기능을 사용 하 여 [내보내기/가져오기 등록](https://msdn.microsoft.com/library/dn790624.aspx)
   > 
   > 
2. **서비스 버스 탐색기**
   
    많은 고객이 ServiceBus 탐색기에 설명된 [ServiceBus 탐색기]를 사용하여 알림 허브를 보고 관리합니다 Code.microsoft.com - [ServiceBus 탐색기 코드]에서 사용할 수 있는 공개 소스 프로젝트입니다.

### <a name="verify-message-notifications"></a>알림 메시지 확인
1. **Azure 클래식 포털**
   
    실행 되 고 모든 서비스 백 엔드를 필요로 하지 않고 toohello "디버그" 탭 toosend 테스트 알림을 tooyour 클라이언트를 이동할 수 있습니다. 
   
    ![][7]
2. **Visual Studio**
   
    Hello comforts의 Visual Studio에서 테스트 알림을 보낼 수도 있습니다.
   
    ![][10]
   
    더 많은 on hello Visual Studio 알림 허브 Azure 탐색기 기능 여기-읽을 수 있습니다. 
   
   * [VS 서버 탐색기 개요]
   * [VS 서버 탐색기 블로그 게시물 - 1]
   * [VS 서버 탐색기 블로그 게시물 - 2]

### <a name="debug-failed-notifications-review-notification-outcome"></a>실패한 알림 디버그/알림 결과 검토
**EnableTestSend 속성**

알림 허브를 통해 알림을 보낼 때 처음 것 바로 가져옵니다 큐에서 대기 NH toodo 모든 대상 아웃 toofigure 처리에 대 한 코드를 다음 결국 NH 보냅니다 toohello PNS. 이 REST API 또는 hello 클라이언트 SDK 중 하나를 사용 하는 경우 hello hello 메시지를 송신 호출 유일한 수단의 반환이 성공적 이면 성공적으로 큐에 대기 되었습니다 알림 허브를 의미 합니다. NH는 결국 toosend hello 메시지 tooPNS 가져왔습니다 때 무슨 상황이 통찰력을 제공 하지는 않습니다. 알림이 하지 hello PNS에서 허용 하는 hello 최대값을 초과 하는 가능성이 있는지 NH toodeliver hello 메시지 tooPNS 시도 하면 오류가 발생 했습니다 예를 들어 hello 페이로드 크기는 hello 클라이언트 장치에 도착, 또는 hello 자격 증명 NH에 구성 된 경우 hello PNS 오류에 대 한 정보는 잘못 된 등 tooget, 라는 속성이 도입 되었습니다 [EnableTestSend 기능]합니다. 이 속성을 테스트 hello 포털 또는 Visual Studio 클라이언트에서 메시지 및 되므로 세부 toosee 가능 보낼 때 사용할 자동으로 정보를 디버깅 합니다. 가능한 경우 이제.NET SDK hello의 hello 예제를 수행 하는 Api를 통해이 사용할 수 있습니다 및 결국 추가 tooall 클라이언트 Sdk를 수 있습니다. toouse hello REST 호출으로이 간단 하 게 추가할 송신 호출의 hello 끝에 예를 들어 "test" 라는 쿼리 문자열 매개 변수 

    https://mynamespace.servicebus.windows.net/mynotificationhub/messages?api-version=2013-10&test

*예(.NET SDK)*

.NET SDK toosend 알림 기본 메시지를 사용 하는 가정 합니다.

    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName);
    var result = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(result.State);

`result.State`단순히 상태 `Enqueued` hello 실행 기능에 대 한 모든 한 정보 없이 hello 끝나기 전에 tooyour 푸시 발생 합니다. Hello를 사용 하 여 수 `EnableTestSend` hello를 초기화 하는 동안 부울 속성 `NotificationHubClient` hello 알림을 전송 하는 동안 발생 하는 hello PNS 오류에 대 한 자세한 상태를 가져올 수 있습니다. 여기에 hello 송신 호출 NH hello 알림 tooPNS toodetermine hello 결과가 전달한 후만 반환 하기 때문에 시간이 추가로 tooreturn을 걸립니다. 

    bool enableTestSend = true;
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName, enableTestSend);

    var outcome = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(outcome.State);

    foreach (RegistrationResult result in outcome.Results)
    {
        Console.WriteLine(result.ApplicationPlatform + "\n" + result.RegistrationId + "\n" + result.Outcome);
    }

*샘플 출력*

    DetailedStateAvailable
    windows
    7619785862101227384-7840974832647865618-3
    hello Token obtained from hello Token Provider is wrong

이 메시지는 hello 알림 허브에 잘못 된 자격 증명 구성 또는 hello 허브 및 hello에 hello 등록 문제가 권장 과정 toodelete이이 등록 되 고 hello 클라이언트 hello를 보내기 전에 다시 나타냅니다. 메시지. 

> [!NOTE]
> Hello를 사용 하 여가이 속성의 스로틀 과도 하 게 되 고 따라서만 사용 해야이 제한 된 집합이 등록 된 개발/테스트 환경에서 note 합니다. 디버그 알림을 too10 장치만 보냅니다. 처리 분당 디버그 보냅니다 toobe 10 개로 제한을 해야 합니다. 
> 
> 

### <a name="review-telemetry"></a>원격 분석 검토
1. **Azure 클래식 포털 사용**
   
    hello 포털을 통해 알림 허브의 모든 hello 작업의 간략 한 개요 tooget 있습니다. 
   
    a) hello "대시보드" 탭에서에서 플랫폼 마다 오류 뿐 아니라 hello 등록, 알림의 집계 보기를 볼 수 있습니다. 
   
    ![][5]
   
    hello "모니터 임계값" 탭 tootake NH toosend hello 알림 toohello PNS가 반환한 PNS 특정 오류에 특히에서 여러 다른 플랫폼 특정 메트릭을 추가할 수도 b). 
   
    ![][6]
   
    검토 hello로 시작 해야 c) **들어오는 메시지**, **등록 작업**, **알림 성공** tooper 플랫폼 탭 tooreview hello를 이동 합니다 PNS 특정 오류가 발생 했습니다. 
   
    d) 있는 경우 hello 알림 허브 잘못 구성 된 hello 인증 설정을 사용 하 여 다음 있습니다 PNS 인증 오류가 표시 됩니다. 상태 toocheck hello PNS 자격 증명입니다. 

2) **프로그래밍 방식 액세스**

자세한 내용은 다음 참조 

* [프로그래밍 방식 원격 분석 액세스]
* [API 샘플을 통한 원격 분석 액세스] 

> [!NOTE]
> **등록 내보내기/가져오기**, **API를 통한 원격 분석 액세스** 등의 여러 원격 분석 관련 기능은 표준 계층에서만 사용할 수 있습니다. Toouse 사용 하려는 경우 이러한 기능에 있는 경우 무료 또는 기본 계층 다음 있습니다 hello REST Api에서 직접 사용 하 여 hello SDK 및 HTTP 403 (금지 됨)를 사용 하는 동안 예외 메시지 toothis 영향을 받게 됩니다. Azure 클래식 포털을 통해 tooStandard 계층을 이동 했다고 있는지 확인 합니다.  
> 
> 

<!-- IMAGES -->
[0]: ./media/notification-hubs-diagnosing/Architecture.png
[1]: ./media/notification-hubs-diagnosing/GCMConfigure.png
[2]: ./media/notification-hubs-diagnosing/GCMEnable.png
[3]: ./media/notification-hubs-diagnosing/GCMServerKey.png
[4]: ./media/notification-hubs-diagnosing/PortalConfigure.png
[5]: ./media/notification-hubs-diagnosing/PortalDashboard.png
[6]: ./media/notification-hubs-diagnosing/PortalMonitoring.png
[7]: ./media/notification-hubs-diagnosing/PortalTestNotification.png
[8]: ./media/notification-hubs-diagnosing/VSRegistrations.png
[9]: ./media/notification-hubs-diagnosing/VSServerExplorer.png
[10]: ./media/notification-hubs-diagnosing/VSTestNotification.png

<!-- LINKS -->
[Notification Hubs 개요]: notification-hubs-push-notification-overview.md
[시작 자습서]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[템플릿 지침]: https://msdn.microsoft.com/library/dn530748.aspx 
[APNS 지침]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW4
[GCM 지침]: http://developer.android.com/google/gcm/adv.html
[Export/Import Registrations]: http://msdn.microsoft.com/library/dn790624.aspx
[ServiceBus 탐색기]: http://msdn.microsoft.com/library/dn530751.aspx
[ServiceBus 탐색기 코드]: https://code.msdn.microsoft.com/windowsazure/Service-Bus-Explorer-f2abca5a
[VS 서버 탐색기 개요]: http://msdn.microsoft.com/library/windows/apps/xaml/dn792122.aspx 
[VS 서버 탐색기 블로그 게시물 - 1]: http://azure.microsoft.com/blog/2014/04/09/deep-dive-visual-studio-2013-update-2-rc-and-azure-sdk-2-3/#NotificationHubs 
[VS 서버 탐색기 블로그 게시물 - 2]: http://azure.microsoft.com/blog/2014/08/04/announcing-release-of-visual-studio-2013-update-3-and-azure-sdk-2-4/ 
[EnableTestSend 기능]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx
[프로그래밍 방식 원격 분석 액세스]: http://msdn.microsoft.com/library/azure/dn458823.aspx
[API 샘플을 통한 원격 분석 액세스]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel

