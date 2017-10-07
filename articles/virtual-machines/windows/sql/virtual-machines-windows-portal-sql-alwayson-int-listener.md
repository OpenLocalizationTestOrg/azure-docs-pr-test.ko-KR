---
title: "Azure 가상 컴퓨터에서 SQL Server 가용성 그룹 수신기를 aaaCreate | Microsoft Docs"
description: "Azure Virtual Machines에서 SQL Server에 대한 Always On 가용성 그룹용 수신기를 만드는 단계별 지침"
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: d1f291e9-9af2-41ba-9d29-9541e3adcfcf
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/01/2017
ms.author: mikeray
ms.openlocfilehash: c6a44dc5c7c18b572c2bf5772b4651b7210aacbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-load-balancer-for-an-always-on-availability-group-in-azure"></a>Azure에서 Always On 가용성 그룹에 대한 부하 분산 장치 구성
이 문서에 설명 방법을 toocreate 부하 분산 장치는 SQL Server Always On 가용성 그룹에에서 대 한 Azure 가상 컴퓨터를 Azure 리소스 관리자와 함께 실행 합니다. 가용성 그룹 hello SQL Server 인스턴스를 Azure 가상 컴퓨터의 경우 부하 분산 장치가 필요 합니다. hello 부하 분산 장치는 hello 가용성 그룹 수신기에 대 한 hello IP 주소를 저장합니다. 가용성 그룹이 여러 지역에 분산된 경우 각 지역에 부하 분산 장치가 있어야 합니다.

toocomplete toohave SQL Server 가용성 그룹 리소스 관리자를 사용 하 여 실행 하는 Azure 가상 컴퓨터에 배포 해야이 작업을 합니다. SQL Server 가상 컴퓨터 둘 다 toohello 속해야 합니다. 동일한 가용성 집합입니다. Hello를 사용할 수 있습니다 [Microsoft 템플릿](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically 리소스 관리자의 hello 가용성 그룹을 만듭니다. 이 템플릿은 내부 부하 분산 장치를 자동으로 만듭니다. 

원하는 경우 [수동으로 가용성 그룹을 구성](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)할 수 있습니다.

이 문서를 진행하려면 가용성 그룹이 이미 구성되어 있어야 합니다.  

관련 항목은 다음과 같습니다.

* [Azure VM의 Always On 가용성 그룹 구성(GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Azure 리소스 관리자 및 PowerShell을 사용하여 VNet-VNet 연결 구성](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

이 문서 전체를 검색 하 여 만들고 hello Azure 포털에서에서 부하 분산 장치를 구성 합니다. Hello 프로세스가 완료 되 면 hello 가용성 그룹 수신기에 대 한 hello 부하 분산 장치에서 hello 클러스터 toouse hello IP 주소를 구성 합니다.

## <a name="create-and-configure-hello-load-balancer-in-hello-azure-portal"></a>Hello Azure 포털에서에서 만들고 hello 부하 분산 장치
이 부분의 hello 작업 수행 hello 다음:

1. Hello Azure 포털에서에서 부하 분산 장치 hello 만들고 hello IP 주소를 구성 합니다.
2. Hello 백 엔드 풀을 구성 합니다.
3. Hello 프로브를 만듭니다. 
4. Hello 부하 분산 규칙을 설정 합니다.

> [!NOTE]
> 여러 리소스 그룹 및 지역 hello SQL Server 인스턴스의 경우 각 단계를 수행을 두 번 한 번만 각 리소스 그룹에 있습니다.
> 
> 

### <a name="step-1-create-hello-load-balancer-and-configure-hello-ip-address"></a>1 단계: hello 부하 분산 장치 만들기 및 hello IP 주소 구성
먼저 hello 부하 분산 장치를 만듭니다. 

1. Hello Azure 포털에서에서 hello SQL Server 가상 컴퓨터를 포함 하는 hello 리소스 그룹을 엽니다. 

2. Hello 리소스 그룹에서 클릭 **추가**합니다.

3. 검색할 **부하 분산 장치** 다음 hello 검색 결과 선택 하 고 **부하 분산 장치**에서 게시는 **Microsoft**합니다.

4. Hello에 **부하 분산 장치** 블레이드에서 클릭 **만들기**합니다.

5. Hello에 **부하 분산 장치 만들기** 대화 상자에서 다음과 같이 hello 부하 분산 장치를 구성 합니다.

   | 설정 | 값 |
   | --- | --- |
   | **Name** |Hello 부하 분산 장치를 나타내는 텍스트 이름입니다. 예를 들어 **sqlLB**입니다. |
   | **형식** |**내부**: 대부분의 구현 hello 내에서 응용 프로그램에서 내부 부하 분산 장치를 사용 하 여 동일한 가상 네트워크 tooconnect toohello 가용성 그룹입니다.  </br> **외부**: 공용 인터넷 연결을 통해 응용 프로그램 tooconnect toohello 가용성 그룹을 허용 합니다. |
   | **가상 네트워크** |Hello에 hello SQL Server 인스턴스로만 구성 되어 있는 가상 네트워크를 선택 합니다. |
   | **서브넷** |SQL Server 인스턴스가 hello hello 서브넷을 선택 합니다. |
   | **IP 주소 할당** |**정적** |
   | **개인 IP 주소** |Hello 서브넷에서 사용 가능한 IP 주소를 지정 합니다. Hello 클러스터에서 수신기를 만들 때이 IP 주소를 사용 합니다. 이 문서의 뒷부분에 나오는 PowerShell 스크립트에서 사용 하 여이 주소 hello에 대 한 `$ILBIP` 변수입니다. |
   | **구독** |구독이 여러 개인 경우 이 필드가 나타날 수 있습니다. 이 리소스와 tooassociate hello 구독을 선택 합니다. 일반적으로 동일한 구독 hello 가용성 그룹에 대 한 모든 hello 리소스 hello는 것입니다. |
   | **리소스 그룹** |SQL Server 인스턴스가 hello hello 리소스 그룹을 선택 합니다. |
   | **위치**: |Hello hello SQL Server 인스턴스는 Azure 위치를 선택 합니다. |

6. **만들기**를 클릭합니다. 

Azure는 hello 부하 분산 장치를 만듭니다. 부하 분산 장치 hello tooa 특정 네트워크, 서브넷, 리소스 그룹 및 위치에 속해 있습니다. Azure hello 작업을 완료 한 후에 Azure의 hello 부하 분산 장치 설정을 확인 합니다. 

### <a name="step-2-configure-hello-back-end-pool"></a>2 단계: hello 백 엔드 풀 구성
Azure 호출 hello 백 엔드 주소 풀 *백 엔드 풀*합니다. 이 경우 hello 백 엔드 풀은 가용성 그룹의 hello 두 SQL Server 인스턴스의 hello 주소입니다. 

1. 리소스 그룹을 만든 hello 부하 분산 장치를 클릭 합니다. 

2. **설정**에서 **백 엔드 풀**을 클릭합니다.

3. **백 엔드 풀**, 클릭 **추가** toocreate 백 엔드 주소 풀입니다. 

4. **백 엔드 풀 추가**아래 **이름**를 hello 백 엔드 풀의 이름을 입력 합니다.

5. **가상 컴퓨터**에서 **가상 컴퓨터 추가**를 클릭합니다. 

6. 아래 **가상 컴퓨터를 선택할**, 클릭 **가용성 집합 선택**, hello 가용성 집합 hello SQL Server 가상 컴퓨터에 속해 있는지를 지정 합니다.

7. Hello 가용성 집합을 선택한 후 클릭 **hello 가상 컴퓨터를 선택할**, 선택 hello hello 가용성 그룹의 hello SQL Server 인스턴스를 호스트 하 고 클릭 두 개의 가상 컴퓨터가 **선택**. 

8. 클릭 **확인** 용 tooclose hello 블레이드에 **가상 컴퓨터를 선택할**, 및 **백 엔드 풀 추가**합니다. 

Azure는 hello 백 엔드 주소 풀에 대 한 hello 설정을 업데이트합니다. 이제 가용성 집합에는 두 개의 SQL Server 인스턴스에 대한 풀이 있습니다.

### <a name="step-3-create-a-probe"></a>3단계: 프로브 만들기
hello 프로브 현재 소유 하 고 hello SQL Server 인스턴스는 가용성 그룹 수신기 hello Azure을 확인 하는 방법을 정의 합니다. Azure는 hello 프로브를 만들 때 정의 하는 포트에 hello IP 주소를 기반으로 하는 hello 서비스를 조사 합니다.

1. Hello에 부하 분산 장치 **설정** 블레이드에서 클릭 **상태 프로브**합니다. 

2. Hello에 **상태 프로브** 블레이드에서 클릭 **추가**합니다.

3. Hello에 hello 프로브를 구성 **추가 프로브** 블레이드입니다. 다음 사용 하 여 hello tooconfigure hello 프로브 값:

   | 설정 | 값 |
   | --- | --- |
   | **Name** |Hello 프로브를 나타내는 텍스트 이름입니다. 예를 들어 **SQLAlwaysOnEndPointProbe**입니다. |
   | **프로토콜** |**TCP** |
   | **포트** |사용 가능한 모든 포트를 사용할 수 있습니다. 예를 들어 *59999*입니다. |
   | **간격** |*5* |
   | **비정상 임계값** |*2* |

4.  **확인**을 클릭합니다. 

> [!NOTE]
> 지정한 hello 포트가 두 SQL Server 인스턴스의 hello 방화벽에서 열려 있는지 확인 합니다. 두 인스턴스의 hello 있습니다를 사용 하는 TCP 포트에 대 한 인바운드 규칙을 필요 합니다. 자세한 내용은 [방화벽 규칙 추가 또는 편집](http://technet.microsoft.com/library/cc753558.aspx)을 참조하세요. 
> 
> 

Azure는 hello 프로브 만들고 tootest는 SQL Server 인스턴스에 hello hello 가용성 그룹 수신기를 사용 합니다.

### <a name="step-4-set-hello-load-balancing-rules"></a>4 단계: hello 부하 분산 규칙 설정
hello 부하 분산 규칙 hello 부하 분산 장치에서 트래픽을 toohello SQL Server 인스턴스를 라우팅하 하는 방법 구성 합니다. 이 부하 분산 장치에 대 한 hello 두 SQL Server 인스턴스 중 하나에만 hello 가용성 그룹 수신기 리소스를 소유 하 고 한 번에 직접 서버 반환 사용 합니다.

1. Hello에 부하 분산 장치 **설정** 블레이드에서 클릭 **부하 분산 규칙**합니다. 

2. Hello에 **부하 분산 규칙** 블레이드에서 클릭 **추가**합니다.

3. Hello에 **추가 부하 분산 규칙** 블레이드에서 hello 부하 분산 규칙을 구성 합니다. 다음 설정을 사용 하 여 hello: 

   | 설정 | 값 |
   | --- | --- |
   | **Name** |Hello 부하 분산 규칙을 나타내는 텍스트 이름입니다. 예를 들어 **SQLAlwaysOnEndPointListener**입니다. |
   | **프로토콜** |**TCP** |
   | **포트** |*1433* |
   | **백 엔드 포트** |*1433*. 이 규칙은 **부동 IP(Direct Server Return)**를 사용하므로 이 값은 무시됩니다. |
   | **프로브** |이 부하 분산 장치에 대해 만든 hello 검색의 hello 이름을 사용 합니다. |
   | **세션 지속성** |**없음** |
   | **유휴 제한 시간(분)** |*4* |
   | **부동 IP(Direct Server Return)** |**사용** |

   > [!NOTE]
   > Hello 블레이드 tooview 아래로 tooscroll hello 설정을 모두 있을 수 있습니다.
   > 

4. **확인**을 클릭합니다. 
5. Azure는 hello 부하 분산 규칙을 구성 합니다. 이제 hello 부하 분산 장치는 hello hello 가용성 그룹 수신기를 호스팅하는 구성 된 tooroute 트래픽 toohello SQL Server 인스턴스입니다. 

이 시점에서 hello 리소스 그룹 tooboth SQL Server 컴퓨터를 연결 하는 부하 분산 장치를 있습니다. 또한 hello 부하 분산 장치 컴퓨터와 hello 가용성 그룹에 대 한 toorequests 응답할 수 있도록 hello SQL Server Always On 가용성 그룹 수신기에 대 한 IP 주소를 포함 합니다.

> [!NOTE]
> SQL Server 인스턴스가 별도 두 지역에 있는 경우 hello의 hello 단계 다른 지역을 반복 합니다. 각 지역마다 하나의 부하 분산 장치가 필요합니다. 
> 
> 

## <a name="configure-hello-cluster-toouse-hello-load-balancer-ip-address"></a>Hello 클러스터 toouse hello 부하 분산 장치 IP 주소 구성
hello 다음 단계는 hello 클러스터에서 tooconfigure hello 수신기 고 hello 수신기를 온라인 상태로 전환 합니다. 다음 hello지 않습니다. 

1. Hello 장애 조치 클러스터에 hello 가용성 그룹 수신기를 만듭니다. 

2. Hello 수신기를 온라인 상태로 전환 합니다.

### <a name="step-5-create-hello-availability-group-listener-on-hello-failover-cluster"></a>5 단계: hello 장애 조치 클러스터에 hello 가용성 그룹 수신기 만들기
이 단계에서는 수동으로 장애 조치 클러스터 관리자 및 SQL Server Management Studio에서 hello 가용성 그룹 수신기를 만듭니다.

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

### <a name="verify-hello-configuration-of-hello-listener"></a>Hello 수신기의 hello 구성 확인

Hello 클러스터 리소스 및 종속성 제대로 구성 되어 SQL Server Management Studio에서 수 tooview hello 수신기 있어야 합니다. tooset 수신기 포트 hello, 다음 hello지 않습니다.

1. SQL Server Management Studio를 시작 하 고 toohello 주 복제본을 연결 합니다.

2. 너무 이동**AlwaysOn 고가용성** > **가용성 그룹** > **가용성 그룹 수신기**합니다.  
    이제 장애 조치 클러스터 관리자에서 만든 hello 수신기 이름이 표시 됩니다. 

3. Hello 수신기 이름을 마우스 오른쪽 단추로 클릭 한 다음 **속성**합니다.

4. Hello에 **포트** 상자 이전 사용 $EndpointPort hello를 사용 하 여 hello 가용성 그룹 수신기에 대 한 hello 포트 번호를 지정 합니다 (1433 hello이 기본값 이었습니다)를 클릭 하 고 **확인**합니다.

이제 Resource Manager 모드에서 실행 중인 Azure 가상 컴퓨터에 가용성 그룹이 생겼습니다. 

## <a name="test-hello-connection-toohello-listener"></a>테스트 hello 연결 toohello 수신기
Hello 다음을 수행 하 여 hello 연결을 테스트 합니다.

1. RDP tooa SQL Server 인스턴스 hello에 있는 동일한 가상 네트워크 구성 요소, 않도록 지정 되었으나 자체 hello 복제 합니다. 이 서버는 hello 클러스터에서 다른 SQL Server 인스턴스에 hello 수 있습니다.

2. 사용 하 여 **sqlcmd** 유틸리티 tootest hello 연결 합니다. 예를 들어 다음 스크립트는 hello 설정는 **sqlcmd** hello 수신기 Windows 인증을 통해 연결 toohello 주 복제본:
   
        sqlcmd -S <listenerName> -E

hello SQLCMD 연결 hello 주 복제본을 호스팅하는 toohello SQL Server 인스턴스를 자동으로 연결 합니다. 

## <a name="create-an-ip-address-for-an-additional-availability-group"></a>추가 가용성 그룹의 IP 주소 만들기

각 가용성 그룹은 별도의 수신기를 사용합니다. 각 수신기는 자체 IP 주소가 있습니다. 사용 하 여 hello 동일 추가 수신기에 대 한 분산 toohold hello IP 주소를 로드 합니다. 가용성 그룹을 만든 후에 hello IP 주소 toohello 부하 분산 장치를 추가 하 고 hello 수신기를 구성 합니다.

hello Azure 포털에 대 한 IP 주소 tooa 부하 분산 tooadd 다음 hello지 않습니다.

1. Hello Azure 포털에서에서 hello 부하 분산 장치를 포함 하는 hello 리소스 그룹을 열고 hello 부하 분산 장치를 클릭 합니다. 

2. **설정**에서 **프런트 엔드 IP 풀**을 클릭한 후 **추가**를 클릭합니다. 

3. 아래 **프런트 엔드 IP 주소 추가**, hello 프런트 엔드에 대 한 이름을 지정 합니다. 

4. 해당 hello 확인 **가상 네트워크** 및 hello **서브넷** SQL Server 인스턴스 hello와 동일 하 게 hello 됩니다.

5. Hello 수신기에 대 한 hello IP 주소를 설정 합니다. 
   
   >[!TIP]
   >Hello IP 주소 toostatic 설정 하 고 hello 서브넷에 현재 사용 되지 않는 주소를 입력할 수 있습니다. 또는 hello IP 주소 toodynamic 설정 하 고 hello 새 프런트 엔드 IP 풀을 저장할 수 있습니다. 이렇게 하면 hello Azure 포털 사용 가능한 IP 주소 toohello 풀을 자동으로 할당 합니다. 그런 다음 hello 프런트 엔드 IP 풀을 다시 열고 하 고 hello 할당 toostatic 변경할 수 있습니다. 

6. Hello 수신기에 대 한 hello IP 주소를 저장 합니다. 

7. 다음 설정을 hello를 사용 하 여 상태 검색을 추가 합니다.

   |설정 |값
   |:-----|:----
   |**Name** |이름 tooidentify hello 프로브 합니다.
   |**프로토콜** |TCP
   |**포트** |사용하지 않는 TCP 포트를 모든 가상 컴퓨터에서 사용할 수 있어야 합니다. 다른 용도로는 사용할 수 없습니다. 두 수신기 hello צ ְ ײ 프로브 포트로 동일 합니다. 
   |**간격** |프로브 사이의 시간 크기 hello 시도합니다. Hello 기본 (5)를 사용 합니다.
   |**비정상 임계값** |여러 가상 컴퓨터를 하기 전에 중지 해야 함을 연속 임계값 hello 비정상으로 간주 됩니다.

8. 클릭 **확인** toosave hello 프로브 합니다. 

9. 부하 분산 규칙을 만듭니다. **부하 분산 규칙**을 클릭한 다음 **추가**를 클릭합니다.

10. Hello 새 부하 분산 규칙 hello 다음 설정을 사용 하 여 구성 합니다.

   |설정 |값
   |:-----|:----
   |**Name** |이름 tooidentify hello 부하 분산 규칙입니다. 
   |**프런트 엔드 IP 주소** |만든 hello IP 주소를 선택 합니다. 
   |**프로토콜** |TCP
   |**포트** |Hello SQL Server 인스턴스를 사용 하는 hello 포트를 사용 합니다. 변경하지 않을 경우 기본 인스턴스는 포트 1433을 사용합니다. 
   |**백 엔드 포트** |같은 값으로 사용 하 여 hello **포트**합니다.
   |**백 엔드 풀** |SQL Server 인스턴스에서 hello hello 가상 컴퓨터를 포함 하는 hello 풀입니다. 
   |**상태 프로브** |만든 hello 프로브를 선택 합니다.
   |**세션 지속성** |없음
   |**유휴 제한 시간(분)** |기본값(4)
   |**부동 IP(Direct Server Return)** | 사용

### <a name="configure-hello-availability-group-toouse-hello-new-ip-address"></a>Hello 가용성 그룹 toouse hello 새 IP 주소 구성

toofinish hello 첫 번째 가용성 그룹을 만든 때 수행한 단계를 반복 hello hello 클러스터를 구성 합니다. 즉, hello 구성 [toouse hello 새 IP 주소를 클러스터](#configure-the-cluster-to-use-the-load-balancer-ip-address)합니다. 

Hello 수신기에 대 한 IP 주소를 추가 하면 hello 다음을 수행 하 여 hello 추가 가용성 그룹을 구성 합니다. 

1. Hello 새 IP 주소에 대 한 hello 프로브 포트를 두 SQL Server 가상 컴퓨터에서 열려 있는지 확인 합니다. 

2. [클러스터 관리자에서 hello 클라이언트 액세스 지점 추가](#addcap)합니다.

3. [Hello 가용성 그룹에 대 한 hello IP 리소스 구성](#congroup)합니다.

   >[!IMPORTANT]
   >Hello IP 주소를 만들 때 toohello 부하 분산 장치를 추가한 hello IP 주소를 사용 합니다.  

4. [SQL Server 가용성 그룹 리소스가 hello hello 클라이언트 액세스 지점에 종속 되 게](#dependencyGroup)합니다.

5. [Hello 클라이언트 액세스 지점 hello IP 주소에 종속 리소스](#listname)합니다.
 
6. [PowerShell에서 hello 클러스터 매개 변수를 설정](#setparam)합니다.

Hello 가용성 그룹 toouse hello 새 IP 주소를 구성한 후에 hello 연결 toohello 수신기를 구성 합니다. 

## <a name="next-steps"></a>다음 단계

- [다른 지역의 Azure Virtual Machines에서 SQL Server Always On 가용성 그룹 구성](virtual-machines-windows-portal-sql-availability-group-dr.md)
