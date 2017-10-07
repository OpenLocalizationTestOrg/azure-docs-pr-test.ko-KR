---
title: "관리자 끝점 유형에 aaaTraffic | Microsoft Docs"
description: "이 문서에서는 Azure Traffic Manager와 함께 사용할 수 있는 다양한 유형의 끝점을 설명합니다."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 4e506986-f78d-41d1-becf-56c8516e4d21
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: kumud
ms.openlocfilehash: 787412ac6207f76791bf3ff753d1df2767b1a964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoints"></a>Traffic Manager 끝점
Microsoft Azure 트래픽 관리자 사용 하면 네트워크 트래픽이 어떤가요 toocontrol distributed tooapplication 배포 서로 다른 데이터 센터에서 실행 합니다. 각 응용 프로그램 배포를 Traffic Manager에서 '끝점'으로 구성합니다. 트래픽 관리자 DNS 요청을 받으면 hello DNS 응답에에서 사용 가능한 끝점 tooreturn를 선택 합니다. 트래픽 관리자 기반 hello 현재 끝점 상태 및 hello 트래픽 라우팅 방법 hello 선택 합니다. 자세한 내용은 [Traffic Manager 작동 방식](traffic-manager-how-traffic-manager-works.md)을 참조하세요.

Traffic Manager에서 지원되는 끝점에는 세 가지 종류가 있습니다.
* **Azure 끝점**은 Azure에서 호스팅되는 서비스에 사용됩니다.
* **외부 끝점**은 온-프레미스 또는 다른 호스팅 공급자 중 하나로 Azure 외부에서 호스팅되는 서비스에 사용됩니다.
* **끝점에 중첩 된** toocombine 사용 되는 트래픽 관리자 프로필 toocreate 보다 유연한 트래픽 라우팅을 구성표 toosupport hello 요구에 더 큰, 보다 복잡 한 배포 됩니다.

단일 Traffic Manager 프로필에서 서로 다른 유형의 끝점을 결합하는 방법에는 제한이 없습니다. 각 프로필은 모든 끝점 유형의 혼합을 포함할 수 있습니다.

다음 섹션 hello 자세히 각 끝점 유형에 대해 설명 합니다.

## <a name="azure-endpoints"></a>Azure 끝점

Azure 끝점은 Traffic Manager에서 Azure 기반 서비스에 사용됩니다. hello Azure 리소스 유형만 지원 됩니다.

* '클래식' IaaS VM 및 PaaS 클라우드 서비스.
* 웹앱
* PublicIPAddress 리소스 (직접 또는 Azure 부하 분산 장치를 통해 연결 된 tooVMs 일 수 있음). hello publicIpAddress toobe 트래픽 관리자 프로필에서 사용 되는 할당 된 DNS 이름이 있어야 합니다.

PublicIPAddress 리소스는 Azure Resource Manager 리소스입니다. Hello 클래식 배포 모델에는 존재 하지 않습니다. 따라서 Traffic Manager의 Azure Resource Manager 환경에서만 지원됩니다. hello 다른 끝점 유형이 지원 됩니다 리소스 관리자와 hello 클래식 배포 모델을 통해.

Azure 끝점을 사용하는 경우 Traffic Manager는 '클래식' IaaS VM, 클라우드 서비스 또는 웹앱이 중지되고 시작되는 시기를 감지합니다. 이 상태는 hello 끝점 상태에 반영 됩니다. 자세한 내용은 [Traffic Manager 끝점 모니터링](traffic-manager-monitoring.md#endpoint-and-profile-status)을 참조하세요. Hello 기본 서비스가 중지 되 면 트래픽 관리자 끝점 상태 확인 또는 toohello 끝점으로 트래픽 수행 하지 않습니다. Hello에 대 한 청구 이벤트가 발생 하지 트래픽 관리자 인스턴스를 중지 했습니다. Hello 서비스를 다시 시작을 다시 시작을 청구 하 고 hello 끝점 적격 tooreceive 트래픽입니다. 이 검색 tooPublicIpAddress 끝점 적용 되지 않습니다.

## <a name="external-endpoints"></a>외부 끝점

외부 끝점은 Azure 외부 서비스에 대해 사용됩니다. 예: 온-프레미스에서 호스팅되는 서비스 또는 다른 공급자로 호스팅되는 서비스. 외부 끝점 개별적으로 사용 하거나 hello Azure 끝점과 함께 결합할 수 같은 트래픽 관리자 프로필. 외부 끝점과 Azure 끝점을 결합하여 다양한 시나리오를 사용할 수 있습니다.

* 액티브-패시브 또는 액티브-액티브 장애 조치 모델 중 하나에서 기존 온-프레미스 응용 프로그램에 대 한 Azure tooprovide 증가 중복성을 사용 합니다.
* hello, 전 세계 사용자에 대 한 응용 프로그램 대기 시간 tooreduce는 기존 온-프레미스 응용 프로그램 tooadditional 지리적 위치에서 Azure 확장 합니다. 자세한 내용은 [Traffic Manager '성능' 트래픽 라우팅](traffic-manager-routing-methods.md#performance)을 참조하세요.
* 계속 해 서 또는 ' 버스트 클라우드 ' 솔루션 toomeet 수요에서 급증으로 기존 온-프레미스 응용 프로그램에 대 한 Azure tooprovide 추가 용량을 사용 합니다.

경우에 따라 것이 유용한 toouse 외부 끝점 tooreference Azure 서비스 (예제를 보려면 hello [FAQ](traffic-manager-faqs.md#traffic-manager-endpoints)). 이 경우 상태 검사 hello 외부 끝점을 평가 하지 hello Azure 끝점 요금이 청구 됩니다. 그러나 Azure 끝점과 달리 중지 하거나 서비스를 원본으로 사용 하는 hello를 삭제 하는 경우 상태 검사 대금 청구 사용 하지 않도록 설정 하거나 hello 트래픽 관리자에서 끝점을 삭제할 때까지 계속 합니다.

## <a name="nested-endpoints"></a>중첩 끝점

중첩 된 끝점에는 더 큰, 복잡 한 배포 hello 요구를 지원할와 여러 트래픽 관리자 프로필 toocreate 유연한 트래픽 라우팅을 계획을 결합 합니다. 중첩 끝점과 끝점 tooa 'parent' 프로필 'child' 프로필 추가 됩니다. 두 hello 자식 및 부모 프로필에는 다른 중첩 된 프로필을 포함 하 여 모든 종류의 다른 끝점과 포함할 수 있습니다. 자세한 내용은 [중첩 Traffic Manager 프로필](traffic-manager-nested-profiles.md)을 참조하세요.

## <a name="web-apps-as-endpoints"></a>끝점으로 웹앱

Traffic Manager에서 끝점으로 웹앱을 구성하는 경우 몇 가지 추가 고려 사항이 적용됩니다.

1. 웹 앱 이상 또는 hello '표준' SKU만은 트래픽 관리자와 함께 사용 하기에 적합 합니다. Tooadd 낮은 SKU 실패의 웹 응용 프로그램을 시도합니다. Hello 다운 그레이드 하는 기존 웹 응용 프로그램의 SKU는 트래픽을 toothat 웹 앱을 더 이상 보내는 트래픽 관리자에서 발생 합니다.
2. 끝점이 HTTP 요청을 받으면 사용 하 여 hello 'host' 헤더 hello 요청 toodetermine에는 웹 응용 프로그램 서비스 hello 요청 해야 합니다. hello 호스트 헤더 hello DNS 사용 되는 이름 tooinitiate hello 요청, 예를 들어 'contosoapp.azurewebsites.net'를 포함합니다. 웹 응용 프로그램 hello DNS 이름으로 다른 DNS 이름을 toouse hello 응용 프로그램에 대 한 사용자 지정 도메인 이름으로 등록 되어야 합니다. Azure 끝점으로 웹 앱 끝점을 추가할 때 hello 트래픽 관리자 프로필 DNS 이름은 hello 응용 프로그램에 대 한 자동으로 등록 됩니다. 이 등록은 hello 끝점 삭제 될 때 자동으로 제거 됩니다.
3. 각 Traffic Manager 프로필은 각 Azure 지역에서 최대 하나의 웹앱 끝점을 가질 수 있습니다. 이 제약 조건을 toowork 주위 외부 끝점으로 웹 응용 프로그램을 구성할 수 있습니다. 자세한 내용은 참조 hello [FAQ](traffic-manager-faqs.md#traffic-manager-endpoints)합니다.

## <a name="enabling-and-disabling-endpoints"></a>끝점 활성화 및 비활성화

트래픽 관리자에서 끝점을 해제 하면 유지 관리 모드에 있거나 재배포 중인 끝점에서 유용한 tootemporarily 제거 트래픽이 될 수 있습니다. Hello 끝점 다시 실행 되 면 다시 설정할 수 있습니다.

끝점 사용 될 수 있고 hello 트래픽 관리자 포털, PowerShell, CLI 또는 리소스 관리자와 hello 클래식 배포 모델 모두에서 사용할 수는 모두 REST API를 통해 사용할 수 없게 합니다.

> [!NOTE]
> Azure 끝점을 해제 하면 영향을 주지 toodo Azure에서 배포 상태입니다. Azure 서비스 (예: VM 또는 웹 응용 프로그램 실행 중이 고 수 tooreceive 트래픽을 트래픽 관리자에서 사용 하지 않도록 설정 하는 경우에 유지 됩니다. 트래픽은 toohello 서비스 인스턴스에서 hello 트래픽 관리자를 통해 프로필 DNS 이름 보다는 직접 해결할 수 있습니다. 자세한 내용은 [Traffic Manager 작동 방식](traffic-manager-how-traffic-manager-works.md)을 참조하세요.

각 끝점 tooreceive 트래픽의 hello 현재 eligibility hello 다음 요인에 따라 다릅니다.

* hello 프로필 상태 (사용/사용 안 함)
* hello 끝점 상태 (사용/사용 안 함)
* hello 결과 해당 끝점에 대 한 hello 상태 확인

자세한 내용은 [Traffic Manager 끝점 모니터링](traffic-manager-monitoring.md#endpoint-and-profile-status)을 참조하세요.

> [!NOTE]
> Hello DNS 수준에서 작동 하는 트래픽 관리자 이므로 tooinfluence 수 없습니다 기존 연결 tooany 끝점. 끝점에 사용할 수 없는 경우 트래픽 관리자는 새 연결 tooanother 사용할 수 있는 끝점을 전달 합니다. 그러나 hello 호스트 사용 하지 않도록 설정 하는 hello 또는 비정상 끝점 뒤에 있는 해당 세션은 종료 될 때까지 tooreceive 트래픽이 기존 연결을 통해 계속 될 수 있습니다. 응용 프로그램에서 기존 연결 hello 세션 기간 tooallow 트래픽 toodrain을 제한 해야 합니다.

프로필의 모든 끝점을 해제 하거나 hello 프로필 자체를 사용 하지 않도록 설정 하는 경우 트래픽 관리자는 'NXDOMAIN' 응답 tooa 새 DNS 쿼리를 보냅니다.


## <a name="next-steps"></a>다음 단계

* [Traffic Manager 작동 방식](traffic-manager-how-traffic-manager-works.md)에 대해 알아봅니다.
* Traffic Manager [끝점 모니터링 및 자동 장애 조치(failover)](traffic-manager-monitoring.md)에 대해 알아봅니다.
* Traffic Manager [트래픽 라우팅 방법](traffic-manager-routing-methods.md)에 대해 알아봅니다.
