---
title: "부하 분산 장치에 대 한 리소스 관리자 지원 aaaAzure | Microsoft Docs"
description: "Azure Resource Manager와 함께 부하 분산 장치용 PowerShell을 사용합니다. 부하 분산 장치에 템플릿을 사용합니다."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a>Azure Load Balancer에 대한 Azure Resource Manager 지원 사용

Azure 리소스 관리자는 Azure에서 서비스에 대 한 hello 기본 설정된 관리 프레임 워크. 이제 Azure Resource Manager 기반 API 및 도구를 사용하여 Azure Load Balancer를 관리할 수 있습니다.

## <a name="concepts"></a>개념

리소스 관리자와 Azure 부하 분산 장치 hello를 다음 자식 리소스가 포함 되어 있습니다.

* 프런트 엔드 IP 구성 - 부하 분산 장치는 VIP(가상 IP)라고도 하는 프런트 엔드 IP 주소를 하나 이상 포함할 수 있습니다. 이러한 IP 주소는 hello 트래픽에 대 한 수신으로 사용 됩니다.
* 백 엔드 주소 풀 – 이들은 hello 가상 컴퓨터 네트워크 인터페이스 카드 (NIC) toowhich 부하 배포와 연결 된 IP 주소입니다.
* 부하 분산 규칙 – 규칙 속성에 지정 된 프런트 엔드 IP 매핑합니다 조합 포트 및 포트 조합 tooa 백 엔드 IP 주소 집합입니다. 부하 분산 장치 하나에 여러 부하 분산 규칙이 포함될 수 있습니다. 각 규칙은 VM과 연결된 백 엔드 IP와 포트 및 프런트 엔드 IP와 포트의 조합입니다.
* 프로브 – 프로브 VM 인스턴스 hello 상태 있습니다 tookeep 추적을 사용 합니다. 상태 검색이 실패 하면 hello VM 인스턴스 수행 될 순환 순서에서 자동으로 합니다.
* 인바운드 NAT 규칙 – NAT 규칙 정의 인바운드 트래픽을 hello 프런트 엔드 IP를 통해 흐르는 hello 및 분산된 toohello 다시 IP를 종료 합니다.

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a>빠른 시작 템플릿

Azure 리소스 관리자를 사용 하면 tooprovision 선언적 템플릿을 사용 하 여 응용 프로그램입니다. 단일 템플릿에서 여러 서비스를 해당 종속성과 함께 배포할 수 있습니다. Hello를 사용 하 여 동일한 템플릿 toorepeatedly hello 응용 프로그램 수명 주기의 다른 단계 동안 응용 프로그램을 배포 합니다.

템플릿은 가상 컴퓨터, 가상 네트워크, 가용성 집합, NIC(네트워크 인터페이스), 저장소 계정, 부하 분산 장치, 네트워크 보안 그룹 및 공용 IP에 대한 정의를 포함할 수 있습니다. 템플릿을 사용하면 복잡한 응용 프로그램에 필요한 모든 항목을 만들 수 있습니다. 버전 제어 및 공동 작업에 대 한 콘텐츠 관리 시스템에 hello 템플릿 파일을 확인할 수 있습니다.

[템플릿에 대한 자세한 정보](../azure-resource-manager/resource-manager-template-walkthrough.md)

[네트워크 리소스에 대한 자세한 정보](../virtual-network/resource-groups-networking.md)

Azure Load Balancer를 사용하는 빠른 시작 템플릿은 커뮤니티 생성 템플릿 집합을 호스트하는 [GitHub 리포지토리](https://github.com/Azure/azure-quickstart-templates) 에서 찾을 수 있습니다.

템플릿의 예:

* [부하 분산 장치의 2개 VM 및 부하 분산 규칙](http://go.microsoft.com/fwlink/?LinkId=544799)
* [내부 부하 분산 장치를 포함하는 VNET의 2개 VM 및 부하 분산 장치 규칙](http://go.microsoft.com/fwlink/?LinkId=544800)
* [부하 분산 장치에 2 개의 Vm hello LB에서 NAT 규칙을 구성 하 고](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a>PowerShell 또는 CLI를 사용하여 Azure 부하 분산 장치 설정

Azure Resource Manager cmdlet, 명령줄 도구 및 REST API 시작

* [Azure 네트워킹 Cmdlet](https://msdn.microsoft.com/library/azure/mt163510.aspx) 사용된 toocreate 부하 분산 될 수 있습니다.
* [어떻게 toocreate Azure 리소스 관리자를 사용 하 여 부하 분산 장치](load-balancer-get-started-ilb-arm-ps.md)
* [Hello Azure CLI를 사용 하 여 Azure 리소스 관리](../xplat-cli-azure-resource-manager.md)
* [부하 분산 장치 REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a>다음 단계

[인터넷 연결 부하 분산 장치를 시작](load-balancer-get-started-internet-arm-ps.md)하고 특정 부하 분산 장치 네트워크 트래픽 동작에 대한 [배포 모드](load-balancer-distribution-mode.md) 유형을 구성할 수도 있습니다.

자세한 내용은 방법 toomanage [부하 분산 장치에 대 한 TCP 시간 제한 설정을 유휴](load-balancer-tcp-idle-timeout.md)합니다. 이 응용 프로그램에 필요한 tookeep 연결 활성 서버 부하 분산 장치 뒤에 대 한 경우에 중요 합니다.
