---
title: "aaaAzure 릴레이 Faq | Microsoft Docs"
description: "Azure 릴레이 대 한 질문과 대답 toosome를 가져옵니다."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 886d2c7f-838f-4938-bd23-466662fb1c8e
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: ab14431e27df43287940e7d12ea37e4093638d21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-faqs"></a>Azure Relay FAQ

이 문서에서는 [Azure Relay](https://azure.microsoft.com/services/service-bus/)에 대해 자주 묻는 일부 질문에 답변합니다. 또한 일반적인 Azure 가격 책정 및 지원 정보는 [Azure 지원 FAQ](http://go.microsoft.com/fwlink/?LinkID=185083)를 참조하세요.

## <a name="general-questions"></a>일반적인 질문
### <a name="what-is-azure-relay"></a>Azure 릴레이란?
hello [Azure 릴레이 서비스](relay-what-is-it.md) 하이브리드 응용 프로그램을 용이 하 게 수 있도록 하 여 더 안전 하 게 회사의 엔터프라이즈 네트워크 toohello 공용 클라우드 내에 있는 서비스를 노출 합니다. 방화벽 연결을 열지 않고 및 개입 수준이 변경 tooa 회사 네트워크 인프라를 요구 하지 않고 hello 서비스를 노출할 수 있습니다.

### <a name="what-is-a-relay-namespace"></a>릴레이 네임스페이스란?
A [네임 스페이스](relay-create-namespace-portal.md) 은 범위 지정 컨테이너 응용 프로그램 내에서 tooaddress 릴레이 리소스를 사용할 수 있습니다. 네임 스페이스 toouse 릴레이 만들어야 합니다. 이 자습서에서 hello 첫 번째 단계 중 하나입니다.

### <a name="what-happened-tooservice-bus-relay-service"></a>어떤 발생 했습니다 tooService 서비스 버스 릴레이?
이전에 명명 된 서비스 버스 릴레이 서비스는 hello는 WCF 릴레이 이제 라고 합니다. 계속할 수 있습니다 toouse이이 서비스가 정상적으로. hello 하이브리드 연결 기능은 Azure BizTalk 서비스에서 transplanted 된 되는 서비스의 업데이트 된 버전이 있습니다. WCF 릴레이 및 하이브리드 연결 계속 toobe 지원 합니다.

## <a name="pricing"></a>가격
몇 가지 질문과 대답에 대 한이 섹션 답변 hello 가격 구조 릴레이 합니다. 또한 일반적인 Azure 가격 책정 정보는 [Azure 지원 FAQ](http://go.microsoft.com/fwlink/?LinkID=185083)를 참조하면 됩니다. Relay 가격 책정에 대한 전체 내용은 [Service Bus 가격 책정 세부 정보][Pricing overview]를 참조하세요.

### <a name="how-do-you-charge-for-hybrid-connections-and-wcf-relay"></a>하이브리드 연결 및 WCF 릴레이의 요금은 어떻게 청구되나요?
릴레이 가격에 대 한 자세한 내용은 참조 hello [하이브리드 연결 및 WCF 릴레이] [ Pricing overview] hello 서비스 버스 가격 책정 세부 정보 페이지에는 테이블입니다. 또한 toohello 가격 참고 사항으로 페이지에서 응용 프로그램 프로 비전 되는 hello 데이터 센터 외부의 수신을 위해 연결 된 데이터 전송에 대 한 요금이 청구 됩니다.

### <a name="how-am-i-billed-for-hybrid-connections"></a>하이브리드 연결의 요금은 어떻게 청구되나요?
하이브리드 연결에 대한 세 가지 예제 청구 시나리오는 다음과 같습니다.

*   시나리오 1:
    *   하이브리드 연결 관리자를 설치 하 고 지속적으로 hello 전체 월에 대 한 실행 hello 인스턴스와 같은 단일 수신기를 해야 합니다.
    *   Hello 달간 hello 연결을 통해 3GB의 데이터를 보냅니다. 
    *   총 청구 금액은 $5입니다.
*   시나리오 2:
    *   하이브리드 연결 관리자를 설치 하 고 지속적으로 hello 전체 월에 대 한 실행 hello 인스턴스와 같은 단일 수신기를 해야 합니다.
    *   Hello 달간 hello 연결을 통해 10GB의 데이터를 보냅니다.
    *   총 청구 금액은 $7.50입니다. Hello 연결에 대 한 $5 이며 첫 5GB +에 대 한 $2.50 hello 추가 5GB의 데이터입니다.
*   시나리오 3:
    *   두 인스턴스 A와 B의 hello 하이브리드 연결 관리자를 설치 하 고 1 개월 내내 hello에 대 한 지속적으로 실행 해야 합니다.
    *   A hello (월) 동안 연결을 통해 3GB의 데이터를 보냅니다.
    *   B hello (월) 동안 연결을 통해 6GB의 데이터를 보냅니다.
    *   총 청구 금액은 $10.50입니다. $ A 연결에 대 한 5 + $ B 연결에 대 한 5 + $0.50 (용 hello 연결 B에 여섯 번째 기가바이트)입니다.

참고 hello 가격 hello 예제에서 사용 되는 hello 하이브리드 연결의 미리 보기 기간 중에 적용할 수 있습니다. 가격은 하이브리드 연결의 일반 공급 시 주체 toochange 합니다.

### <a name="how-are-hours-calculated-for-relay"></a>Relay의 경우 시간은 어떻게 계산되나요?

WCF Relay는 표준 계층 네임스페이스에서만 사용할 수 있습니다. 그렇지 않은 경우 릴레이의 가격 책정 및 [연결 할당량](../service-bus-messaging/service-bus-quotas.md)은 변경되지 않습니다. 즉, 릴레이 toobe hello 작업이 아닌 메시지 수를 기준으로 요금이 청구 계속와 릴레이 시간. 자세한 내용은 참조 hello ["하이브리드 연결 및 WCF 릴레이"](https://azure.microsoft.com/pricing/details/service-bus/) hello 가격 책정 세부 정보 페이지에는 테이블입니다.

### <a name="what-if-i-have-more-than-one-listener-connected-tooa-specific-relay"></a>둘 이상의 수신기 연결 된 tooa 특정 릴레이 경우 어떻게 합니까?
경우에 따라 단일 릴레이에 연결된 수신기가 여러 개 있을 수 있습니다. 릴레이 하나 이상의 릴레이 리스너가 연결된 tooit 때 열려으로 간주 됩니다. 추가 릴레이 시간에 수신기 tooan 오픈 릴레이 결과 추가 합니다. 번호 hello 릴레이의 보낸 사람 (호출 하는 클라이언트 또는 송신 메시지 toorelays) 연결 된 tooa 릴레이 영향을 주지 않습니다는 릴레이 시간 hello 계산 합니다.

### <a name="how-is-hello-messages-meter-calculated-for-wcf-relays"></a>WCF 릴레이 대 한 hello 메시지 미터를 계산 하는 방법
(**TooWCF 릴레이 적용 됩니다. 하이브리드 연결에서 메시지의 비용은 없습니다.**)

일반적으로 청구 가능 메시지 릴레이 사용 하 여 계산에 대 한 hello 동일에 사용 되는 메서드 이전에 설명한 엔터티 (큐, 토픽 및 구독)를 조정 합니다. 하지만 몇 가지 주목할 차이점이 있습니다.

보내는 메시지 tooa 서비스 버스 릴레이 "full을 통해" hello 메시지를 받는 toohello 릴레이 수신기 전송 처리 됩니다. 송신 작업 toohello 서비스 버스 릴레이 뒤에 배달 toohello 릴레이 수신기로 처리 되지 않습니다. 요청-응답 스타일 서비스 호출 (의 too64 KB를) 두 개의 청구 가능 메시지가 릴레이 수신기 결과 대해: hello 요청 및 응답 hello에 대 한 하나의 청구 가능 메시지에 대 한 하나의 청구 가능 메시지 (hello 응답은 64KB도 가정 하거나 작은). 이 클라이언트와 서비스 간의 큐 toomediate를 사용 하는 방식과 다릅니다. 클라이언트와 서비스 간의 큐 toomediate를 사용 하는 경우 hello 동일한 요청-회신 패턴을 사용 하려면 hello 큐 toohello 서비스에서 큐에서 제거/배달 이어서 요청 보내기 toohello 대기열을 합니다. 다음 응답 보내기 tooanother 큐와 큐에서 제거/배달 큐 toohello 클라이언트에서. 같은 크기로 too64 KB) (위쪽 전체에서 가정 하는 hello를 사용 하 여 hello 청구 가능 메시지 4에서 큐 패턴 결과 조정 합니다. 두 번 hello 수가 메시지 tooimplement hello 릴레이 사용 하 여 수행 하는 같은 패턴에 대 한 요금이 청구 됩니다. 물론,는 이점을 toousing 큐 tooachieve이이 패턴을 내구성 및 부하 평준화 합니다. 다음과 같은이 이점을 hello 추가 비용을 발생 될 수 있습니다.

Hello를 사용 하 여 열린 릴레이 **netTCPRelay** WCF 바인딩을 hello 시스템을 통과 하는 데이터 스트림의 아니라 개별 메시지가 아니라 메시지를 처리 합니다. 이 바인딩을 사용 하면 hello 발신자와 리스너 하기만 보내고 받은 hello 개별 메시지의 hello 프레임에 대 한 가시성 됩니다. Hello를 사용 하는 릴레이 대 한 **netTCPRelay** 바인딩, 모든 데이터는 청구 가능 메시지 계산에 대 한 스트림을로 처리 됩니다. 이 경우 서비스 버스 hello 총 5 분 단위로 개별 릴레이 통해 보내거나 받은 데이터의 양을 계산 합니다. 그런 다음 해당 기간 동안 64 KB toodetermine hello 해당 릴레이 대 한 청구 가능 메시지 수로 해당 총 데이터 양이 분할 합니다.

## <a name="quotas"></a>할당량
| 할당량 이름 | 범위 | 유형 | 초과 시 동작 | 값 |
| --- | --- | --- | --- | --- |
| 릴레이의 동시 수신기 |엔터티 |정적 |추가 연결에 대 한 후속 요청이 거부 되 고 hello 호출 코드에서 예외가 수신 됩니다. |25 |
| 동시 릴레이 수신기 |시스템 수준 |정적 |추가 연결에 대 한 후속 요청이 거부 되 고 hello 호출 코드에서 예외가 수신 됩니다. |2, 000 |
| 서비스 네임스페이스의 모든 릴레이 끝점당 동시 릴레이 연결 |시스템 수준 |공용 |- |5, 000 |
| 서비스 네임스페이스당 릴레이 끝점 |시스템 수준 |공용 |- |10000 |
| [NetOnewayRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.netonewayrelaybinding.aspx) and [NetEventRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.neteventrelaybinding.aspx) 릴레이의 메시지 크기 |시스템 수준 |정적 |이러한 할당량을 초과 하는 들어오는 메시지는 거부 하 고 hello 호출 코드에서 예외가 수신 됩니다. |64KB |
| [HttpRelayTransportBindingElement](https://msdn.microsoft.com/library/microsoft.servicebus.httprelaytransportbindingelement.aspx) 및 [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) 릴레이의 메시지 크기 |시스템 수준 |공용 |- |무제한 |

### <a name="does-relay-have-any-usage-quotas"></a>릴레이에는 사용 할당량이 있습니까?
기본적으로 모든 클라우드 서비스의 경우 Microsoft는 모든 고객의 구독에 대해 계산되는 월별 사용 할당량을 집계합니다. 이번에는 요구가 이러한 제한을 초과할 수 있다는 점을 이해합니다. 이러한 한도를 적절하게 조정할 수 있도록 고객 서비스에 언제든지 문의해 주세요. 서비스 버스에 대 한 hello 집계 사용 할당량은 다음과 같습니다.

* 50억 개의 메시지
* 2백만 릴레이 시간

Hello 오른쪽 toodisable 계정을 월간 사용 할당량을 초과 하는 예약 되어있습니다, 하지만 전자 메일 알림을 제공 하 고 작업을 수행 하기 전에 여러 시도 toocontact hello 고객으로 만듭니다. 이러한 할당량을 초과하는 고객은 초과하는 요금을 지불해야 합니다.

### <a name="naming-restrictions"></a>명명 제한
릴레이 네임스페이스 이름은 6~50자여야 합니다.

## <a name="subscription-and-namespace-management"></a>구독 및 네임스페이스 관리
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>네임 스페이스 tooanother Azure 구독을 마이그레이션하는 방법

중 하나 사용 하 여 hello 수 하나의 Azure 구독 tooanother 구독에서 네임 스페이스 toomove [Azure 포털](https://portal.azure.com) 하거나 PowerShell 명령을 사용 합니다. 네임 스페이스 tooanother 구독 toomove hello 네임 스페이스 이미 활성 상태 여야 합니다. hello 명령을 실행 하는 hello 사용자 hello 원본 및 대상 구독 모두에 관리자가 사용자 여야 합니다.

#### <a name="azure-portal"></a>Azure portal

toouse hello 하나의 구독만 tooanother 구독에서 Azure 포털 toomigrate Azure 릴레이 네임 스페이스 참조 [리소스 tooa 새 리소스 그룹이 나 구독 이동](../azure-resource-manager/resource-group-move-resources.md#use-portal)합니다. 

#### <a name="powershell"></a>PowerShell

toouse PowerShell toomove 다음 명령 시퀀스를 사용 하 여 hello tooanother 구독 한 Azure 구독에서에서 네임 스페이스입니다. tooexecute이이 작업을 hello 네임 스페이스 이미 활성 상태 여야 하 고 hello PowerShell 명령을 실행 하는 hello 사용자 hello 원본 및 대상 구독 모두에 관리자 사용자 여야 합니다.

```powershell
# Create a new resource group in hello target subscription.
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move hello namespace from hello source subscription toohello target subscription.
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="troubleshooting"></a>문제 해결
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-relay-apis-and-suggested-actions-you-can-take"></a>정의 hello 예외 중 일부 Azure 릴레이 Api에 의해 생성 된 및 권장 조치를 수행할 수 있는 방법
일반적인 예외 및 수행할 수 있는 권장 조치에 대한 설명은 [릴레이 예외][Relay exceptions]를 참조하세요.

### <a name="what-is-a-shared-access-signature-and-which-languages-can-i-use-toogenerate-a-signature"></a>공유 액세스 서명을 란 무엇이 고 있는 언어를 사용할 수 있습니까 toogenerate 서명?
공유 액세스 서명(SAS)은 SHA-256 보안 해시 또는 URI에 따른 인증 메커니즘입니다. Toogenerate 노드, PHP, Java, C 및 C#에서 사용자 고유의 서명을 확인 하려면 어떻게 해야 하는 방법에 대 한 내용은 [공유 액세스 서명 사용 하 여 서비스 버스 인증][Shared Access Signatures]합니다.

### <a name="is-it-possible-toowhitelist-relay-endpoints"></a>가능한 toowhitelist 릴레이 끝점 입니까?
예. hello 릴레이 클라이언트 연결을 toohello Azure 릴레이 서비스를 정규화 된 도메인 이름을 사용 하 여 만듭니다. 고객은 DNS 허용 목록을 지원하는 방화벽에 `*.servicebus.windows.net`에 대한 항목을 추가할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* [네임스페이스 만들기](relay-create-namespace-portal.md)
* [.NET 시작](relay-hybrid-connections-dotnet-get-started.md)
* [노드 시작](relay-hybrid-connections-node-get-started.md)

[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Relay exceptions]: relay-exceptions.md
[Shared access signatures]: ../service-bus-messaging/service-bus-sas.md