---
title: "Azure DNS의 aaaOverview | Microsoft Docs"
description: "Microsoft Azure의 DNS 호스팅 서비스 개요입니다. Microsoft Azure에 도메인을 호스트하세요."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a>Azure DNS 개요

Domain Name System hello 또는 DNS는 변환 합니다 (또는 해결) 웹 사이트 또는 서비스 이름을 지정 tooits IP 주소입니다. Azure DNS는 DNS 도메인에 대한 호스팅 서비스로, Microsoft Azure 인프라를 사용하여 이름 확인을 제공합니다. Azure에서 도메인을 호스트 하 여 DNS를 관리할 수 있습니다 레코드를 사용 하 여 다른 Azure 서비스와 동일한 자격 증명, Api, 도구 및 대금 청구 hello 합니다.

![DNS 개요](./media/dns-overview/scenario.png)

## <a name="features"></a>기능

* **안정성 및 성능** - Azure DNS의 DNS 도메인은 DNS 이름 서버의 Azure 글로벌 네트워크에 호스트됩니다. 각 DNS 쿼리에 사용 가능한 가장 가까운 DNS 서버 hello에 응답할 수 있도록 애니캐스트 네트워킹을 사용 합니다. 이렇게 하면 도메인에 대해 빠른 성능과 고가용성이 제공됩니다.

* **완벽 한 통합** -hello Azure DNS 서비스는 Azure 서비스에 대 한 DNS 레코드 사용된 toomanage 수 있으며 외부 리소스에 대 한 DNS tooprovide 사용된 될 수 있습니다. Azure DNS 프로토콜은 hello Azure 포털에에서 통합 하 고 사용 하 여 다른 Azure 서비스와 동일한 자격 증명, 청구 및 지원 계약 hello 합니다.

* **보안** -hello Azure DNS 서비스는 Azure 리소스 관리자에 기반 합니다. 이 경우 역할 기반 액세스 제어, 감사 로그 및 리소스 잠금과 같은 리소스 관리자 기능의 이점을 누릴 수 있습니다. 도메인 및 레코드 hello Azure 포털, Azure PowerShell cmdlet 통해 관리할 수 있으며, 플랫폼 간 Azure CLI hello 합니다. 자동 DNS 관리를 요구 하는 응용 프로그램은 REST API와 Sdk hello 통해 hello 서비스와 통합할 수 있습니다.

Azure DNS는 현재 도메인 이름 구입을 지원하지 않습니다. Toopurchase 도메인을 원하는 경우 제 3 자 도메인 이름 등록 기관 toouse를 해야 합니다. hello 등록 기관에는 일반적으로 작은 연간 요금 요금. hello 도메인의 DNS 레코드 관리용 Azure DNS에서 호스팅할 수 있습니다. 참조 [도메인 tooAzure DNS 위임](dns-domain-delegation.md) 대 한 자세한 내용은 합니다.

## <a name="pricing"></a>가격

DNS 요금 청구는 hello 수가 hello DNS 쿼리 수 및 Azure에서 호스팅되는 DNS 영역을 기반으로 합니다. 방문 가격에 대 한 자세한 toolearn [Azure DNS 가격](https://azure.microsoft.com/pricing/details/dns/)합니다.

## <a name="faq"></a>FAQ

Azure DNS에 대 한 자주 묻는 질문에 대 한 참조 hello [Azure DNS FAQ](dns-faq.md)합니다.

## <a name="next-steps"></a>다음 단계

[DNS 영역 및 레코드 개요](dns-zones-records.md)를 참조하여 DNS 영역 및 레코드에 대해 알아봅니다.

너무 방법에 대해 알아봅니다[DNS 영역을 만드는](./dns-getstarted-create-dnszone-portal.md) Azure DNS에 있습니다.

일부 hello에 대 한 자세한 내용은 다른 키 [네트워킹 기능](../networking/networking-overview.md) Azure의 합니다.

