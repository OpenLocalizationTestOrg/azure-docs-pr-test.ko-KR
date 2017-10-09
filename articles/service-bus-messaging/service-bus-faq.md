---
title: "서비스 버스 질문과 대답 (FAQ) aaaAzure | Microsoft Docs"
description: "Azure Service Bus에 대한 일부 자주 묻는 질문을 답변합니다."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: cc75786d-3448-4f79-9fec-eef56c0027ba
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 71fe9eac46647a3e4026dbcaf2196984dd4b6a44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-faq"></a>Service Bus FAQ
이 문서는 Microsoft Azure Service Bus에 대한 일부 자주 묻는 질문을 답변합니다. Hello를 방문할 수도 [Azure 지원 Faq](http://go.microsoft.com/fwlink/?LinkID=185083) 일반적인 Azure 가격 책정 및 지원 정보입니다.

## <a name="general-questions-about-azure-service-bus"></a>Azure Service Bus에 대한 일반적인 질문
### <a name="what-is-azure-service-bus"></a>Azure Service Bus란?
[Azure 서비스 버스](service-bus-messaging-overview.md) 는 분리 된 시스템 간에 toosend 데이터 수 있는 비동기 메시징 클라우드 플랫폼입니다. Microsoft는 하면 필요 하지 않고 toohost 순서 toouse의 고유한 하드웨어 중 하나 이므로 서비스로이 기능을 제공 하기.

### <a name="what-is-a-service-bus-namespace"></a>Service Bus 네임스페이스란?
[네임스페이스](service-bus-create-namespace-portal.md)는 응용 프로그램 내에서 Service Bus 리소스의 주소를 지정하기 위한 범위 컨테이너를 제공합니다. 하나를 만들면 필요한 toouse 서비스 버스 이며 hello 중 하나로 시작의 첫 번째 단계 설정 됩니다.

### <a name="what-is-an-azure-service-bus-queue"></a>Azure Service Bus 큐란?
[Service Bus 큐](service-bus-queues-topics-subscriptions.md)는 메시지가 저장되는 엔터티입니다. 큐는 여러 응용 프로그램이 나 서로 toocommunicate 해야 하는 분산된 응용 프로그램의 여러 부분이 있는 경우에 특히 유용 합니다. hello 큐는 비슷한 tooa 배포 센터 여러 제품 (메시지)를 수신 하 고 해당 위치에서 전송 합니다.

### <a name="what-are-azure-service-bus-topics-and-subscriptions"></a>Azure Service Bus 토픽 및 구독이란?
토픽은 큐로 시각화할 수 있고 여러 구독을 사용하는 경우 더 풍부한 메시징 모델이 되며 기본적으로는 일대다 통신 도구입니다. 이 게시/등록 모델 (또는 *pub/sub*)을 여러 구독 toohave 포함 하는 메시지 tooa 항목 여러 응용 프로그램에서 받은 메시지를 보내는 응용 프로그램을 사용 하도록 설정 합니다.

### <a name="what-is-a-partitioned-entity"></a>분할된 엔터티란?
일반적인 큐 또는 항목은 단일 메시지 broker에서 처리되며 하나의 메시징 저장소에 저장됩니다. [분할된 큐 또는 토픽](service-bus-partitioning.md)은 여러 메시지 broker에 의해 처리되고 여러 메시징 저장소에 저장됩니다. 이 즉, 분할 된 큐 또는 항목의 전체 처리량을 hello 더 이상 단일 메시지 브로커 또는 메시징 저장소의 hello 성능을 제한 됩니다. 또한 메시징 스토어가 일시적으로 중단된 경우에도 분할된 큐 또는 항목을 계속 렌더링할 수 없습니다.

분할 엔터티를 사용하는 경우 순서는 보장할 수 없습니다. 파티션을 사용할 수 없다는 hello 이벤트에서 수 여전히 보내고 다른 파티션에 hello에서 메시지를 수신 합니다.

## <a name="best-practices"></a>모범 사례
### <a name="what-are-some-azure-service-bus-best-practices"></a>일부 Azure Service Bus 모범 사례는 무엇인가요?
* [서비스 버스를 사용 하 여 성능 향상에 대 한 유용한] [ Best practices for performance improvements using Service Bus] -이 문서에서는 메시지를 교환할 때 toooptimize 성능 방법을 설명 합니다.

### <a name="what-should-i-know-before-creating-entities"></a>엔터티를 만들기 전에 무엇을 알아야 하나요?
다음과 같은 큐와 항목의 속성 hello는 변경할 수 없습니다. 새 대체 엔터티를 만들지 않고 엔터티를 프로비전하는 경우 다음 항목을 수정할 수 없다는 점을 고려해야 합니다.

* 크기
* 분할
* 세션
* 중복 검색
* Express 엔터티

## <a name="pricing"></a>가격
이 섹션 hello 서비스 버스 가격 구조에 대 한 몇 가지 자주 묻는 질문에 답변 합니다.

hello [서비스 버스 가격 및 요금 청구](service-bus-pricing-billing.md) 참조, 문서 설명 하 고 서비스 버스 가격 옵션에 대 한 정보에 대 한 서비스 버스의 hello 과금 단위 [서비스 버스 가격 정보](https://azure.microsoft.com/pricing/details/service-bus/)합니다.

Hello를 방문할 수도 [Azure 지원 Faq](http://go.microsoft.com/fwlink/?LinkID=185083) 일반 Azure 가격 정보에 대 한 합니다. 

### <a name="how-do-you-charge-for-service-bus"></a>Service Bus 요금을 어떻게 청구하나요?
Service Bus 가격 책정에 대한 전체 내용은 [Service Bus 가격 책정 세부 정보][Pricing overview]를 참조하세요. 또한 toohello 가격 설명이 없는 한, 응용 프로그램 프로 비전 되는 hello 데이터 센터 외부의 수신을 위해 연결 된 데이터 전송에 대 한 요금이 청구 됩니다.

### <a name="what-usage-of-service-bus-is-subject-toodata-transfer-what-is-not"></a>서비스 버스의 어떤 사용은 주체 toodata 전송? 어떤 경우에 대상이 아닌가요?
지정된 Azure 지역 내에서 데이터 전송은 비용뿐만 아니라 인바운드 데이터 전송 없이 제공됩니다. 해당 지역 외부의 데이터 전송 속도가 찾을 수 있는 제목 tooegress 요금 [여기](https://azure.microsoft.com/pricing/details/bandwidth/)합니다.

### <a name="does-service-bus-charge-for-storage"></a>Service Bus는 저장소에 대한 요금을 청구하나요?
아니요, Service Bus는 저장소에 대한 요금을 청구하지 않습니다. 그러나 한 할당량 제한 hello 최대 데이터 양을 큐/항목당 지속 될 수 있습니다. Hello 다음 FAQ를 참조 하십시오.

## <a name="quotas"></a>할당량

서비스 버스 제한 및 할당량 목록, 참조 hello [서비스 버스 할당량 개요][Quotas overview]합니다.

### <a name="does-service-bus-have-any-usage-quotas"></a>Service Bus는 사용 할당량이 있나요?
기본적으로 모든 클라우드 서비스의 경우 Microsoft는 모든 고객의 구독에 대해 계산되는 월별 사용 할당량을 집계합니다. 이러한 제한 보다 사용자의 필요가 많을 수도 있다는 것을 이해하기 때문에 사용자의 요구를 이해하고 이러한 제한을 적절하게 조정할 수 있도록 언제든지 서비스에 문의하세요. 서비스 버스에 대 한 hello 집계 사용 할당량은 매달 5 십억 메시지입니다.

Hello 오른쪽 toodisable를 지정된 된 달에 사용 할당량을 초과한 고객 계정, 보유 하지만 전자 메일 알림을 제공 하 고 작업을 수행 하기 전에 여러 시도 toocontact 고객을 확인 합니다. 이러한 할당량을 초과 하는 고객 hello 할당량을 초과 하는 요금에 대 한 지불 해야 합니다.

Azure에서 다른 서비스와 마찬가지로 서비스 버스 리소스의 공정한 사용 인지 특정 할당량 tooensure의 집합을 적용 합니다. Hello에서 이러한 할당량에 대 한 자세한 정보를 찾을 수 있습니다 [서비스 버스 할당량 개요][Quotas overview]합니다.

## <a name="troubleshooting"></a>문제 해결
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-service-bus-apis-and-their-suggested-actions"></a>일부 Azure 서비스 버스 Api 및 해당 권장된 동작에서 생성 된 hello 예외 무엇입니까?
가능한 Service Bus 예외의 목록은 [예외 개요][Exceptions overview]를 참조하세요.

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature"></a>공유 액세스 서명이란 무엇이고 어떤 언어가 서명 생성을 지원하나요?
공유 액세스 서명은 SHA – 256 보안 해시 또는 URI에 따른 인증 메커니즘입니다. 방법에 대 한 내용은 toogenerate 노드, PHP, Java 및 C의 고유한 서명을\#, hello 참조 [공유 액세스 서명] [ Shared Access Signatures] 문서.

## <a name="subscription-and-namespace-management"></a>구독 및 네임스페이스 관리
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>네임 스페이스 tooanother Azure 구독을 마이그레이션하는 방법

Hello 중 하나를 사용 하 여 하나의 Azure 구독 tooanother에서 네임 스페이스를 이동할 수 있습니다 [Azure 포털](https://portal.azure.com) 또는 PowerShell 명령입니다. Tooexecute hello 작업 순서에서에서 hello 네임 스페이스 이미 여야 활성화 합니다. hello 명령을 실행 하는 hello 사용자는 모두 hello 소스의 관리자 여야 하 고 대상 구독 해야 합니다.

#### <a name="portal"></a>포털

Azure 포털 toomigrate 서비스 버스 네임 스페이스 tooanother 구독 toouse hello hello 지시에 따라 [여기](../azure-resource-manager/resource-group-move-resources.md#use-portal)합니다. 

#### <a name="powershell"></a>PowerShell

hello 다음의 PowerShell 명령 순서는 네임 스페이스에서에서 이동 하나의 Azure 구독 tooanother 합니다. tooexecute이이 작업을 hello 네임 스페이스 이미 활성 상태 여야 하 고 hello PowerShell 명령을 실행 하는 hello 사용자 두 hello 원본 및 대상 구독에서 관리자 여야 합니다.

```powershell
# Create a new resource group in target subscription
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move namespace from source subscription tootarget subscription
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="next-steps"></a>다음 단계
서비스 버스에 대 한 자세한 toolearn hello 다음 항목을 참조 하십시오.

* [Azure Service Bus 프리미엄 소개(블로그 게시물)](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Azure Service Bus 프리미엄 소개(Channel9)](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [Service Bus 개요](service-bus-messaging-overview.md)
* [Azure Service Bus 아키텍처 개요](service-bus-fundamentals-hybrid-solutions.md)
* [Service Bus 큐 시작](service-bus-dotnet-get-started-with-queues.md)

[Best practices for performance improvements using Service Bus]: service-bus-performance-improvements.md
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Quotas overview]: service-bus-quotas.md
[Exceptions overview]: service-bus-messaging-exceptions.md
[Shared Access Signatures]: service-bus-sas.md
