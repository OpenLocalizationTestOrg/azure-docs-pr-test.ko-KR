---
title: "다른 Azure 서비스와 Azure DNS aaaUsing | Microsoft Docs"
description: "Azure DNS tooresolve toouse 다른 Azure 서비스에 대 한 이름 지정 방법을 이해"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure dns
ms.assetid: e9b5eb94-7984-4640-9930-564bb9e82b78
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 09/21/2016
ms.author: gwallace
ms.openlocfilehash: 791f93d6aff2c638c08518e9f1e8ab89ac8de3f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-dns-works-with-other-azure-services"></a>다른 Azure 서비스와 함께 Azure DNS가 작동하는 방법

Azure DNS는 호스팅된 DNS 관리 및 이름 확인 서비스입니다. 이렇게 하면 다른 응용 프로그램과 서비스를 Azure에 배포 했나요 있습니다 toocreate 공용 DNS 이름을 hello에 대 한 합니다. 사용자 지정 도메인에서 Azure 서비스에 대 한 이름을 만드는 작업은을 서비스에 대 한 hello 올바른 형식의 레코드를 추가 합니다.

* 동적으로 할당 된 IP 주소를 만들어야 합니다 DNS CNAME 레코드를 Azure에서 만들어진 지도 toohello DNS 이름을 서비스에 대 한 합니다. DNS 표준 hello 영역 루트에 대 한 CNAME 레코드를 사용 하 여 하지 못하게 합니다.
* 정적으로 할당 된 IP 주소에 대 한 모든 이름을 사용 하 여 DNS A 레코드를 만들 수 포함 하는 *naked 도메인* hello 영역 루트에서 이름입니다.

hello 다음 테이블 윤곽선 hello 지원 레코드 종류를 여러 Azure 서비스에 사용할 수 있습니다. 이 테이블에서 볼 수 있듯이 Azure DNS는 인터넷 연결 네트워크 리소스에 대한 DNS 레코드만을 지원합니다. Azure DNS는 내부, 개인 주소의 이름 확인에 사용할 수 없습니다.

| Azure 서비스 | 네트워크 인터페이스 | 설명 |
| --- | --- | --- |
| Application Gateway |[프런트 엔드 공용 IP](dns-custom-domain.md#public-ip-address) |DNS A 또는 CNAME 레코드를 만들 수 있습니다. |
| 부하 분산 장치 |[프런트 엔드 공용 IP](dns-custom-domain.md#public-ip-address)  |DNS A 또는 CNAME 레코드를 만들 수 있습니다. 부하 분산 장치는 동적으로 할당된 IPv6 공용 IP 주소를 가질 수 있습니다. 따라서 IPv6 주소에 대한 CNAME 레코드를 만들어야 합니다. |
| Traffic Manager |공용 이름 |트래픽 관리자 프로필 tooyour 할당 toohello trafficmanager.net 이름을 매핑하는 CNAME을만 만들 수 있습니다. 자세한 내용은 [Traffic Manager 작동 방식](../traffic-manager/traffic-manager-overview.md#traffic-manager-example)을 참조하세요. |
| 클라우드 서비스 |[공용 IP](dns-custom-domain.md#public-ip-address) |정적으로 할당된 IP 주소의 경우 DNS A 레코드를 만들 수 있습니다. 동적으로 할당 된 IP 주소에 대 한 toohello 매핑하는 CNAME 레코드 만들어야 *cloudapp.net* 이름입니다. 이 규칙에는 클라우드 서비스로 배포 되어 있으므로 hello 클래식 포털에서 만든 tooVMs 적용 됩니다. 자세한 내용은 [Cloud Services에서 사용자 지정 도메인 이름 구성](../cloud-services/cloud-services-custom-domain-name-portal.md)을 참조하세요. |
| App Service | [외부 IP](dns-custom-domain.md#app-service-web-apps) |외부 IP 주소의 경우 DNS A 레코드를 만들 수 있습니다. 그렇지 않으면 toohello azurewebsites.net 이름을 매핑하는 CNAME 레코드를 만들어야 합니다. 자세한 내용은 참조 [매핑 사용자 지정 도메인 이름을 tooan Azure 응용 프로그램](../app-service-web/web-sites-custom-domain-name.md) |
| 리소스 관리자 VM |[공용 IP](dns-custom-domain.md#public-ip-address) |리소스 관리자 VM은 공용 IP 주소를 가질 수 있습니다. 공용 IP 주소가 있는 VM은 부하 분산 장치 뒤에 올 수도 있습니다. 공용 주소 hello에 대 한 DNS A 또는 CNAME 레코드를 만들 수 있습니다. 이 사용자 지정 이름을 hello 부하 분산 장치에서 사용 되는 toobypass hello VIP를 수 있습니다. |
| 클래식 VM |[공용 IP](dns-custom-domain.md#public-ip-address) |PowerShell 또는 CLI를 사용하여 만든 클래식 VM은 동적 또는 정적(예약된) 가상 주소로 구성될 수 있습니다. DNS CNAME 또는 A 레코드를 각각 만들 수 있습니다. |
