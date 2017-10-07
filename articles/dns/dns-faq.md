---
title: aaaAzure DNS FAQ | Microsoft Docs
description: "Azure DNS에 대한 질문과 대답"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: jonatul
ms.openlocfilehash: 55006e9d8b311f1e94678eb9d35ce3448b936488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-faq"></a>Azure DNS FAQ

## <a name="about-azure-dns"></a>Azure DNS 정보

### <a name="what-is-azure-dns"></a>Azure DNS란?

Domain Name System hello 또는 DNS는 변환 합니다 (또는 해결) 웹 사이트 또는 서비스 이름을 지정 tooits IP 주소입니다. Azure DNS는 DNS 도메인에 대한 호스팅 서비스로, Microsoft Azure 인프라를 사용하여 이름 확인을 제공합니다. Azure에서 도메인을 호스트 하 여 DNS를 관리할 수 있습니다 레코드를 사용 하 여 다른 Azure 서비스와 동일한 자격 증명, Api, 도구 및 대금 청구 hello 합니다.

Azure DNS의 DNS 도메인은 DNS 이름 서버의 Azure 글로벌 네트워크에 호스팅됩니다. 각 DNS 쿼리에 사용 가능한 가장 가까운 DNS 서버 hello에 응답할 수 있도록 애니캐스트 네트워킹을 사용 합니다. 이렇게 하면 도메인에 대해 빠른 성능과 고가용성이 제공됩니다.

hello Azure DNS 서비스는 Azure 리소스 관리자에 기반 합니다. 이 경우 역할 기반 액세스 제어, 감사 로그 및 리소스 잠금과 같은 리소스 관리자 기능의 이점을 누릴 수 있습니다. 도메인 및 레코드 hello Azure 포털, Azure PowerShell cmdlet 통해 관리할 수 있으며, 플랫폼 간 Azure CLI hello 합니다. 자동 DNS 관리를 요구 하는 응용 프로그램은 REST API와 Sdk hello 통해 hello 서비스와 통합할 수 있습니다.

### <a name="how-much-does-azure-dns-cost"></a>Azure DNS 비용은 얼마입니까?

hello Azure DNS 청구 모델 hello 수가 Azure DNS 및 DNS 쿼리를 받게 hello 수에서 호스트 되는 DNS 영역을 기반으로 합니다. 할인은 사용량에 따라 제공됩니다.

자세한 내용은 참조 hello [가격 책정 페이지 Azure DNS](https://azure.microsoft.com/pricing/details/dns/)합니다.

### <a name="what-is-hello-sla-for-azure-dns"></a>Azure DNS에 대 한 hello SLA 란?

유효한 DNS 요청 받음을 응답 하나 이상의 Azure DNS 이름 서버에서 이상 hello 시간의 99.99% 하 게 됩니다.

자세한 내용은 참조 hello [Azure DNS SLA 페이지](https://azure.microsoft.com/support/legal/sla/dns)합니다.

### <a name="what-is-a-dns-zone-is-it-hello-same-as-a-dns-domain"></a>'DNS 영역'이란 무엇인가요? 동일한 DNS 도메인으로 hello 것은? 

도메인 예를 들어 만든 'contoso.com' hello 도메인 이름 시스템에는 고유 이름입니다.

DNS 영역에는 특정 도메인에 대 한 사용 되는 toohost hello DNS 레코드입니다. 예를 들어 contoso.com' hello 도메인' 예: (메일 서버)에 대 한 ' mail.contoso.com' 및 'www.contoso.com' (웹 사이트)에 대 한 여러 DNS 레코드를 포함할 수 있습니다. 이러한 hello DNS 영역 'contoso.com'에서 호스트 됩니다.

도메인 이름이 *이름만*인 반면, DNS 영역은 도메인 이름에 대 한 hello DNS 레코드를 포함 하는 데이터 리소스입니다. Azure DNS toohost DNS 영역을 허용 하 고 Azure에서 도메인에 대 한 hello DNS 레코드를 관리 합니다. DNS 이름 서버 hello 인터넷에서에서 tooanswer DNS 쿼리도 제공합니다.

### <a name="do-i-need-toopurchase-a-dns-domain-name-toouse-azure-dns"></a>DNS 도메인 이름 toouse Azure DNS toopurchase 필요 합니까? 

그럴 필요는 없습니다.

Toopurchase 도메인 toohost Azure DNS에 DNS 영역을 사용할 필요가 없습니다. Hello 도메인 이름을 소유 하지 않고 언제 든 지 DNS 영역을 만들 수 있습니다. 이 영역에 대 한 DNS 쿼리 하는 경우 이러한 보내지는지 toohello Azure DNS 이름 서버 toohello 영역 할당을 해결만 됩니다.

Hello 글로벌 DNS 계층-이 사용 하면 DNS에서 아무 곳 이나의 쿼리 hello world toofind DNS 영역 및 DNS 레코드를 응답에 toolink DNS 영역이 복원할 toopurchase hello 도메인 이름이 필요 합니다.

## <a name="azure-dns-features"></a>Azure DNS 기능

### <a name="does-azure-dns-support-dns-based-traffic-routing-or-endpoint-failover"></a>Azure DNS는 DNS 기반 트래픽 라우팅 또는 끝점 장애 조치(failover)를 지원하나요?

DNS 기반 트래픽 라우팅 및 끝점 장애 조치(failover)는 Azure Traffic Manager에 의해 제공됩니다. 이것은 Azure DNS와 함께 사용할 수 있는 별도 Azure 서비스입니다. 자세한 내용은 참조 hello [트래픽 관리자 개요](../traffic-manager/traffic-manager-overview.md)합니다.

Azure DNS가 지정된 된 DNS 레코드에 대 한 각 DNS 쿼리에 hello를 항상 받는 'static' DNS 도메인 호스팅만 지원 같은 DNS 응답 합니다.

### <a name="does-azure-dns-support-domain-name-registration"></a>Azure DNS는 도메인 이름 등록을 지원하나요?

아니요. Azure DNS는 현재 도메인 이름 구입을 지원하지 않습니다. Toopurchase 도메인을 원하는 경우 제 3 자 도메인 이름 등록 기관 toouse를 해야 합니다. hello 등록 기관에는 일반적으로 작은 연간 요금 요금. hello 도메인의 DNS 레코드 관리용 Azure DNS에서 호스팅할 수 있습니다. 참조 [도메인 tooAzure DNS 위임](dns-domain-delegation.md) 대 한 자세한 내용은 합니다.

이 기능은 백로그에서 추적하는 기능입니다. 피드백 사이트도 사용할 수 있습니다[이 기능에 대 한 사용자를 지 원하는 등록](https://feedback.azure.com/forums/217313-networking/suggestions/4996615-azure-should-be-its-own-domain-registrar)합니다.

### <a name="does-azure-dns-support-private-domains"></a>Azure DNS에서는 '개인' 도메인을 지원하나요?

아니요. Azure DNS는 현재 인터넷 연결 도메인만 지원합니다.

이 기능은 백로그에서 추적하는 기능입니다. 피드백 사이트도 사용할 수 있습니다[이 기능에 대 한 사용자를 지 원하는 등록](https://feedback.azure.com/forums/217313-networking/suggestions/10737696-enable-split-dns-for-providing-both-public-and-int)합니다.

Azure의 내부 DNS 옵션에 대한 자세한 내용은 [VM 및 역할 인스턴스에 대한 이름 확인](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)을 참조하세요.

### <a name="does-azure-dns-support-dnssec"></a>Azure DNS에서는 DNSSEC를 지원하나요?

아니요. Azure DNS는 현재 DNSSEC를 지원하지 않습니다.

이 기능은 백로그에서 추적하는 기능입니다. 피드백 사이트도 사용할 수 있습니다[이 기능에 대 한 사용자를 지 원하는 등록](https://feedback.azure.com/forums/217313-networking/suggestions/13284393-azure-dns-needs-dnssec-support)합니다.

### <a name="does-azure-dns-support-zone-transfers-axfrixfr"></a>Azure DNS에서는 영역 전송(AXFR/IXFR)을 지원하나요?

아니요. Azure DNS는 현재 영역 전송을 지원하지 않습니다. DNS 영역 수 [hello Azure CLI를 사용 하 여 Azure DNS로 가져온](dns-import-export.md)합니다. DNS 레코드 hello를 통해 관리할 수 있습니다 [Azure DNS 관리 포털](dns-operations-recordsets-portal.md), 우리의 [REST API](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [PowerShell cmdlet](dns-operations-recordsets.md), 또는 [ CLI 도구](dns-operations-recordsets-cli.md)합니다.

이 기능은 백로그에서 추적하는 기능입니다. 피드백 사이트도 사용할 수 있습니다[이 기능에 대 한 사용자를 지 원하는 등록](https://feedback.azure.com/forums/217313-networking/suggestions/12925503-extend-azure-dns-to-support-zone-transfers-so-it-c)합니다.

### <a name="does-azure-dns-support-url-redirects"></a>Azure DNS에서는 URL 리디렉션을 지원하나요?

아니요. URL 리디렉션 서비스는 DNS 서비스에 실제로 없는-hello DNS 수준 대신 hello HTTP 수준에서 작동 합니다. 일부 URL의 DNS 공급자 toobundle 서비스를 전반적인 제공의 일환으로 리디렉션합니다. 현재 이 기능은 Azure DNS에서 지원되지 않습니다.

이 기능은 백로그에서 추적됩니다. 피드백 사이트도 사용할 수 있습니다[이 기능에 대 한 사용자를 지 원하는 등록](https://feedback.azure.com/forums/217313-networking/suggestions/10109736-provide-a-301-permanent-redirect-service-for-ape)합니다.

## <a name="using-azure-dns"></a>Azure DNS 사용

### <a name="can-i-co-host-a-domain-using-azure-dns-and-another-dns-provider"></a>Azure DNS 및 다른 DNS 공급자를 사용하여 도메인을 공동 호스트할 수 있나요?

예. Azure DNS에서는 다른 DNS 서비스와의 도메인 공동 호스팅을 지원합니다.

toodo 따라서 hello 도메인 (어떤 공급자 DNS를 수신 하는 컨트롤 hello 도메인에 대 한 쿼리)에 대 한 toomodify hello NS 레코드를 해야 하는 두 공급자의 toopoint toohello 이름 서버입니다. 이러한 NS 레코드 toobe 3 위치 수정 필요: Azure DNS에서 다른 공급자를 hello 및 hello 부모 영역 (도메인 이름 등록 기관 hello 통해 일반적으로 구성 됨). DNS 위임에 대한 자세한 내용은 [DNS 도메인 위임](dns-domain-delegation.md)을 참조하세요.

또한 tooensure hello 도메인에 대 한 hello DNS 레코드는 모두 DNS 공급자 간의 동기화 해야 합니다. Azure DNS는 현재 DNS 영역 전송을 지원하지 않습니다. Hello 중 하나를 사용 하 여 toosynchronize DNS 레코드를 필요한 [Azure DNS 관리 포털](dns-operations-recordsets-portal.md), 우리의 [REST API](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [PowerShell cmdlet](dns-operations-recordsets.md) 또는 [CLI 도구](dns-operations-recordsets-cli.md)합니다.

### <a name="do-i-have-toodelegate-my-domain-tooall-4-azure-dns-name-servers"></a>용량은 toodelegate 내 도메인 tooall 4 Azure DNS 이름 서버

예. Azure DNS 오류 격리 및 향상 된 복원 력 tooeach DNS 영역 이름은 4 대의 서버를 할당합니다. 에 대 한 tooqualify hello Azure DNS SLA toodelegate tooall 4 도메인 이름 서버를 해야 합니다.

### <a name="what-are-hello-usage-limits-for-azure-dns"></a>Azure DNS에 대 한 hello 사용 제한 사항은 무엇입니까?

기본 제한 값을 다음 hello Azure DNS를 사용 하는 경우에 적용 됩니다.

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

### <a name="can-i-move-an-azure-dns-zone-between-resource-groups-or-between-subscriptions"></a>리소스 그룹 또는 구독 간에 Azure DNS 영역을 이동할 수 있나요?

예. 리소스 그룹 또는 구독 간에 DNS 영역을 이동할 수 있습니다.

DNS 영역을 이동할 때 DNS 쿼리는 아무런 영향도 받지 않습니다. hello 이름 서버 toohello 영역 할당 유지 hello를 동일 하 고 DNS 쿼리 전체에서 정상적으로 처리 됩니다.

자세한 내용 및 방법에 대 한 toomove DNS 영역 참조 [리소스 tooa 새 리소스 그룹이 나 구독 이동](../azure-resource-manager/resource-group-move-resources.md)합니다.

### <a name="how-long-does-it-take-for-dns-changes-tootake-effect"></a>가 소요 DNS 변경 내용 tootake 효과 대 한?

새 DNS 영역 및 DNS 레코드 일반적으로 내에 반영 되도록 hello Azure DNS 이름 서버에 신속 하 게 몇 초입니다.

Tooexisting DNS 레코드 변경 내용 약간 더 길 걸릴 수 있지만 60 초 이내 hello Azure DNS 이름 서버에 여전히 반영 해야 합니다. 이 경우 DNS (DNS 클라이언트 및 DNS 재귀 확인자)에서 Azure DNS 외부에서 캐싱도 DNS 변경 toobe 효과적인에 걸린 hello 시간을 달라질 수 있습니다. 각 레코드 집합의 hello Time To Live (TTL) 속성을 사용 하 여이 캐시 기간을 제어할 수 있습니다.

### <a name="how-can-i-protect-my-dns-zones-against-accidental-deletion"></a>실수로 삭제되지 않도록 내 DNS 영역을 보호하려면 어떻게 해야 하나요?

Azure DNS는 Azure 리소스 관리자를 사용 하 여 관리 되 고 하면 도움이 hello Azure 리소스 관리자는 제어 기능에 액세스를 제공 합니다. 역할 기반 액세스 제어에 사용 되는 toocontrol 읽기 또는 쓰기 액세스 tooDNS 영역 및 레코드 집합 수 있는 사용자 수 있습니다. 리소스 잠금을 DNS 영역 및 레코드 집합의 적용 된 tooprevent 실수로 수정 또는 삭제 될 수 있습니다.

자세한 내용은 [DNS 영역 및 레코드 보호](dns-protect-zones-recordsets.md)를 참조하세요.

### <a name="how-do-i-set-up-spf-records-in-azure-dns"></a>Azure DNS에서 SPF 레코드를 설정하려면 어떻게 해야 하나요?

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="how-do-i-set-up-an-international-domain-name-idn-in-azure-dns"></a>Azure DNS에서 IDN(국제 도메인 이름)을 설정하려면 어떻게 해야 하나요?

IDN(국제 도메인 이름)은 '[punycode](https://en.wikipedia.org/wiki/Punycode)'로 각 DNS 이름을 인코딩하여 사용할 수 있습니다. DNS 쿼리는 이러한 punycode로 인코딩된 이름을 사용하여 수행됩니다.

레코드 집합 이름 toopunycode 또는 첫 번째 변환 하는 동안 hello 영역 이름으로 Azure DNS에 국제 Idn (도메인 이름)을 구성할 수 있습니다. Azure DNS는 현재 punycode로/부터의 기본 제공 변환을 지원하지 않습니다.

## <a name="next-steps"></a>다음 단계

[Azure DNS에 대해 자세히 알아보기](dns-overview.md)
<br>
[DNS 영역 및 레코드에 대해 자세히 알아보기](dns-zones-records.md)
<br>
[Azure DNS 시작](dns-getstarted-portal.md)

