---
title: "sql에 항상 aaaConfigure 부하 분산 장치 | Microsoft Docs"
description: "부하 분산 장치 toowork에 항상 SQL 및 tooleverage powershell toocreate hello SQL 구현에 대 한 분산 장치를 로드 하는 방법 구성"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a>SQL Always On에 대해 부하 분산 장치 구성

이제 ILB에서 SQL Server AlwaysOn 가용성 그룹을 실행할 수 있습니다. 가용성 그룹은 고가용성 및 재해 복구를 위한 SQL Server의 주력 솔루션입니다. 가용성 그룹 수신기 hello 하면 클라이언트 응용 프로그램 tooseamlessly toohello hello hello 구성의 hello 복제본 수에 관계 없이 주 복제본을 연결 합니다.

hello 수신기 (DNS) 이름은 매핑된 tooa 부하 분산 된 IP 주소 이며 Azure의 부하 분산 장치 hello 들어오는 트래픽을 tooonly hello 주 서버에 지시 hello 복제 세트에 없습니다.

SQL Server AlwaysOn(수신기) 끝점에 대해 ILB 지원을 사용할 수 있습니다. 이제 hello 수신기의 hello 액세스 가능성을 제어할 하 고 가상 네트워크 (VNet)에 특정 서브넷에서 hello 부하 분산 된 IP 주소를 선택할 수 있습니다.

ILB를 hello 수신기에서 사용 하 여 SQL server 끝점 hello (예: Server tcp:ListenerName, 1433 = 데이터베이스 DatabaseName =)만 액세스할 수 있는:

* 서비스 및 Vm에서 hello 동일한 가상 네트워크
* 연결된 온-프레미스 네트워크의 서비스 및 VM
* 상호 연결된 VNet의 서비스 및 VM

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

그림 1 - 인터넷 연결 부하 분산 장치로 구성된 SQL AlwaysOn

## <a name="add-internal-load-balancer-toohello-service"></a>내부 부하 분산 장치 toohello 서비스 추가

1. 다음 예제는 hello, 우리 ' 서브넷-1' 이라는 서브넷을 포함 하는 가상 네트워크 구성:

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. 각 VM에서 ILB에 대한 부하 분산 끝점 추가

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    2 VM의 호출된 "sqlsvc1" 및 "sqlsvc2" 실행 되 고 있는 위의 hello 예제에서 서비스 "Sqlsvc" hello 클라우드에서 합니다. Hello ILB를 만든 후 `DirectServerReturn` 스위치를 추가 하면 분산 된 끝점 toohello ILB tooallow SQL tooconfigure hello에 대 한 수신기 hello 가용성 그룹을 로드 합니다.

SQL AlwaysOn에 대한 자세한 내용은 [Azure에서 AlwaysOn 가용성 그룹에 대한 내부 부하 분산 장치 구성](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md)을 참조하세요.

## <a name="see-also"></a>참고 항목
[인터넷 연결 부하 분산 장치 구성 시작](load-balancer-get-started-internet-arm-ps.md)

[내부 부하 분산 장치 구성 시작](load-balancer-get-started-ilb-arm-ps.md)

[부하 분산 장치 배포 모드 구성](load-balancer-distribution-mode.md)

[부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성](load-balancer-tcp-idle-timeout.md)
