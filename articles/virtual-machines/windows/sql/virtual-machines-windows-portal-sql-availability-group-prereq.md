---
title: "aaaSQL 서버 가용성 그룹-Azure 가상 컴퓨터-필수 조건 | Microsoft Docs"
description: "이 자습서에서는 Azure Vm에서 SQL Server Always On 가용성을 만들기 위한 tooconfigure hello 선행 조건을 그룹화 하는 방법을 보여 줍니다."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: c492db4c-3faa-4645-849f-5a1a663be55a
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: eed0729ead25c7793bb17a04cd7fd996c7dc8c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="complete-hello-prerequisites-for-creating-always-on-availability-groups-on-azure-virtual-machines"></a>Azure 가상 컴퓨터에서 Always On 가용성 그룹을 만들기 위한 사전 요구 사항을 hello 완료

이 자습서에서는 어떻게 toocomplete hello를 만들기 위한 필수 구성 요소는 [Azure 가상 컴퓨터 (Vm)에서 SQL Server Always On 가용성 그룹](virtual-machines-windows-portal-sql-availability-group-tutorial.md)합니다. Hello 필수 구성 요소를 마친 경우 단일 리소스 그룹에 도메인 컨트롤러, 두 SQL Server Vm 및 미러링 모니터 서버 있는 합니다.

**예상 시간**: toocomplete hello 필수 구성 요소는 몇 시간이 걸릴 수 있습니다. 이 시간의 대부분은 가상 컴퓨터를 만드는 데 소요됩니다.

hello 다음 다이어그램에서는 hello 자습서에서 작성 합니다.

![가용성 그룹](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="review-availability-group-documentation"></a>가용성 그룹 설명서 검토

이 자습서는 사용자가 SQL Server Always On 가용성 그룹을 기본적으로 이해하고 있다고 가정합니다. 이 기술에 익숙하지 않은 경우 [Always On 가용성 그룹 개요(SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx)를 참조하세요.


## <a name="create-an-azure-account"></a>Azure 계정 만들기
Azure 계정이 필요합니다. [무료 Azure 계정을 열거나](/pricing/free-trial/?WT.mc_id=A261C142F) 또는 [Visual Studio 구독자 혜택을 활성화](/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있습니다.

## <a name="create-a-resource-group"></a>리소스 그룹 만들기
1. Toohello 로그인 [Azure 포털](http://portal.azure.com)합니다.
2. 클릭  **+**  toocreate hello 포털에서 새 개체입니다.

   ![새 개체](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-portalplus.png)

3. 형식 **리소스 그룹** hello에 **마켓플레이스** 검색 창.

   ![리소스 그룹](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroupsymbol.png)
4. **리소스 그룹**을 클릭합니다.
5. **만들기**를 클릭합니다.
6. Hello에 **리소스 그룹** 블레이드 아래 **리소스 그룹 이름은**를 hello 리소스 그룹에 대 한 이름을 입력 합니다. 예를 들어 **sql-ha-rg**를 입력합니다.
7. 여러 Azure 구독이 있는 경우 hello 구독 hello toocreate hello 가용성 그룹에 원하는 Azure 구독 인지 확인 합니다.
8. 위치를 선택합니다. hello 위치는 hello toocreate hello 가용성 그룹을 원하는 Azure 지역입니다. 이 자습서에서는 여기 toobuild 하나는 Azure 위치에 있는 모든 리소스입니다.
9. 확인 **Pin toodashboard** 을 선택 합니다. 이 선택적 설정은 Azure 포털 대시보드에서 hello에 hello 리소스 그룹에 대 한 바로 가기를 둡니다.

   ![리소스 그룹](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroup.png)

10. 클릭 **만들기** toocreate hello 리소스 그룹입니다.

Azure hello 리소스 그룹 및 핀 바로 가기 toohello 리소스 그룹을 만듭니다 포털 hello 합니다.

## <a name="create-hello-network-and-subnets"></a>Hello 네트워크 및 서브넷 만들기
hello 다음 단계는 toocreate hello 네트워크 및 hello Azure 리소스 그룹의 서브넷입니다.

hello 솔루션 두 서브넷으로 하나의 가상 네트워크를 사용합니다. hello [가상 네트워크 개요](../../../virtual-network/virtual-networks-overview.md) azure에서 네트워크에 대 한 자세한 정보를 제공 합니다.

toocreate hello 가상 네트워크:

1. Hello 리소스 그룹에 Azure 포털에서에서 클릭 **+ 추가**합니다. Azure 열립니다 hello **모든** 블레이드입니다.

   ![새 항목](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/02-newiteminrg.png)
2. **가상 네트워크**를 검색합니다.

     ![가상 네트워크 검색](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/04-findvirtualnetwork.png)
3. **가상 네트워크**를 클릭합니다.
4. Hello에 **가상 네트워크** 블레이드에서 hello 클릭 **리소스 관리자** 배포 모델 및 클릭 **만들기**합니다.

    hello 아래 표에 나와 hello 가상 네트워크에 대 한 hello 설정.

   | **필드** | 값 |
   | --- | --- |
   | **Name** |autoHAVNET |
   | **주소 공간** |10.33.0.0/24 |
   | **서브넷 이름** |관리자 |
   | **서브넷 주소 범위** |10.33.0.0/29 |
   | **구독** |Hello 구독 toouse를 추가할지 여부를 지정 합니다. 하나의 구독만 있는 경우 **구독**은 비어 있습니다. |
   | **리소스 그룹** |선택 **기존 항목 사용** hello 리소스 그룹의 hello 이름을 선택 합니다. |
   | **위치**: |Hello Azure 위치를 지정 합니다. |

   주소 공간 및 서브넷 주소 범위는 hello 테이블에서 다를 수 있습니다. 구독에 따라 hello 포털 사용 가능한 주소 공간 및 해당 서브넷 주소 범위를 제안합니다. 사용할 수 있는 주소 공간이 충분하지 않으면 다른 구독을 사용하세요.

   hello 예제를 사용 하 여 hello 서브넷 이름 **Admin**합니다. Hello 도메인 컨트롤러에 대 한이 서브넷은입니다.

5. **만들기**를 클릭합니다.

   ![Hello 가상 네트워크 구성](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/06-configurevirtualnetwork.png)

Azure 포털 대시보드에서 toohello를 반환 하 고 hello 새 네트워크를 만들 때 사용자에 게 알려줍니다.

### <a name="create-a-second-subnet"></a>두 번째 서브넷 만들기
hello 새 가상 네트워크에 서브넷이 둘을 라는 **Admin**. hello 도메인 컨트롤러는이 서브넷을 사용 합니다. SQL Server Vm hello 라는 두 번째 서브넷을 사용 하 여 **SQL**합니다. tooconfigure이이 서브넷:

1. 대시보드를에서 만든 hello 리소스 그룹 클릭 **SQL-HA-RG**합니다. Hello 네트워크 hello 리소스 그룹에서 찾을 **리소스**합니다.

    경우 **SQL-HA-RG** 표시 되지 않으면 클릭 하 여 찾을 **리소스 그룹** 및 hello 리소스 그룹 이름으로 필터링 합니다.
2. 클릭 **autoHAVNET** hello 리소스 목록에 있습니다. Azure는 hello 네트워크 구성 블레이드를 엽니다.
3. Hello에 **autoHAVNET** 가상 네트워크 블레이드 아래 **설정** , 클릭 **서브넷**합니다.

    이미 만든 참고 hello 서브넷입니다.

   ![Hello 가상 네트워크 구성](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/07-addsubnet.png)
5. 두 번째 서브넷을 만듭니다. **+ 서브넷**을 클릭합니다.
6. Hello에 **서브넷 추가** 블레이드를 입력 하 여 hello 서브넷 구성 **sqlsubnet** 아래 **이름**합니다. 유효한 **주소 범위**가 자동으로 지정됩니다. 이 주소 범위에 최소 10개의 주소가 있는지 확인합니다. 프로덕션 환경에서는 더 많은 주소가 필요할 수 있습니다.
7. **확인**을 클릭합니다.

    ![Hello 가상 네트워크 구성](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/08-configuresubnet.png)

다음 표에 hello hello 네트워크 구성 설정을 요약 되어 있습니다.

| **필드** | 값 |
| --- | --- |
| **Name** |**autoHAVNET** |
| **주소 공간** |구독에서 사용 가능한 주소 공간 hello에이 값에 따라 다릅니다. 일반적인 값은 10.0.0.0/16입니다. |
| **서브넷 이름** |**admin** |
| **서브넷 주소 범위** |이 값이 구독에 hello 사용 가능한 주소 범위에 따라 달라 집니다. 일반적인 값은 10.0.0.0/24입니다. |
| **서브넷 이름** |**sqlsubnet** |
| **서브넷 주소 범위** |이 값이 구독에 hello 사용 가능한 주소 범위에 따라 달라 집니다. 일반적인 값은 10.0.1.0/24입니다. |
| **구독** |Hello 구독 toouse를 추가할지 여부를 지정 합니다. |
| **리소스 그룹** |**SQL-HA-RG** |
| **위치**: |지정 hello hello 리소스 그룹에 대해 선택한 동일한 위치입니다. |

## <a name="create-availability-sets"></a>가용성 집합 만들기

가상 컴퓨터를 만들기 전에 가용성 집합을 toocreate 해야 합니다. 가용성 집합 계획 되거나 계획 되지 않은 유지 관리 이벤트에 대 한 hello 가동 중지 시간을 줄입니다. Azure 가용성 집합은 Azure에서 물리적 장애 도메인 및 업데이트 도메인에 배치하는 리소스의 논리적 그룹입니다. 오류 도메인 전원 및 네트워크 리소스를 별도 hello 가용성 집합의 hello 멤버에서는 합니다. hello 가용성 집합의 멤버 되지 당해 hello에 대 한 유지 관리를 위해 동일한 업데이트 도메인 확인 시간입니다. 자세한 내용은 참조 [관리 가상 컴퓨터의 가용성을 hello](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

두 개의 가용성 집합이 필요합니다. 하나는 hello 도메인 컨트롤러에 대 한입니다. 두 번째 hello hello SQL Server Vm입니다.

가용성 설정 toohello 리소스 그룹을 이동 하 고 클릭 toocreate **추가**합니다. 입력 하 여 hello 결과 필터링 **가용성 집합**합니다. 클릭 **가용성 집합** 에 결과 얻으려면 hello 및 클릭 **만들기**합니다.

다음 표에 hello toohello 매개 변수에 따라 두 개의 가용성 집합을 구성 합니다.

| **필드** | 도메인 컨트롤러 가용성 집합 | SQL Server 가용성 집합 |
| --- | --- | --- |
| **Name** |adavailabilityset |sqlavailabilityset |
| **리소스 그룹** |SQL-HA-RG |SQL-HA-RG |
| **장애 도메인** |3 |3 |
| **업데이트 도메인** |5 |3 |

Hello 가용성 집합을 만든 후 hello Azure 포털에서에서 toohello 리소스 그룹을 반환 합니다.

## <a name="create-domain-controllers"></a>도메인 컨트롤러 만들기
Hello 네트워크, 서브넷, 가용성 집합 및 인터넷 연결 부하 분산을 만든 후 hello 도메인 컨트롤러에 대 한 준비 toocreate hello 가상 컴퓨터를 수 있습니다.

### <a name="create-virtual-machines-for-hello-domain-controllers"></a>Hello에 대 한 가상 컴퓨터를 도메인 컨트롤러 만들기
toocreate hello 도메인 컨트롤러를 구성 하 고, toohello 반환 **SQL-HA-RG** 리소스 그룹입니다.

1. **추가**를 클릭합니다. hello **모든** 블레이드를 엽니다.
2. **Windows Server 2016 Datacenter**를 입력합니다.
3. **Windows Server 2016 Datacenter**를 클릭합니다. Hello에 **Windows Server 2016 Datacenter** 블레이드에서 해당 hello 배포 모델은 확인 **리소스 관리자**, 클릭 하 고 **만들기**합니다. Azure 열립니다 hello **가상 컴퓨터를 만들** 블레이드입니다.

Hello 앞 단계 toocreate 두 가상 컴퓨터를 반복 합니다. Hello 두 가상 컴퓨터 이름을 지정 합니다.

* ad-primary-dc
* ad-secondary-dc

  > [!NOTE]
  > hello **ad 보조 dc** 가상 컴퓨터는 선택 사항이 Active Directory 도메인 서비스에 대 한 고가용성 tooprovide 합니다.
  >
  >

hello 다음 표에서 이러한 두 컴퓨터에 대 한 hello 설정:

| **필드** | 값 |
| --- | --- |
| **Name** |최초 도메인 컨트롤러 *ad-primary-dc*</br>두 번째 도메인 컨트롤러 *ad-secondary-dc* |
| **VM 디스크 유형** |SSD |
| **사용자 이름** |DomainAdmin |
| **암호** |Contoso!0000 |
| **구독** |*사용자의 구독* |
| **리소스 그룹** |SQL-HA-RG |
| **위치**: |*사용자의 위치* |
| **크기** |DS1_V2 |
| **저장소** | **관리되는 디스크 사용** - **Yes** |
| **가상 네트워크** |autoHAVNET |
| **서브넷** |관리자 |
| **공용 IP 주소** |*이름이 같은 VM hello* |
| **네트워크 보안 그룹** |*이름이 같은 VM hello* |
| **가용성 집합** |adavailabilityset </br>**장애 도메인**:2</br>**업데이트 도메인**: 2|
| **진단** |사용 |
| **진단 저장소 계정** |*자동으로 생성됨* |

   >[!IMPORTANT]
   >VM을 만들 때 가용성 집합에 VM을 배치할 수 있습니다. VM을 만든 후에 설정할 hello 가용성을 변경할 수 없습니다. 참조 [관리 가상 컴퓨터의 가용성을 hello](../manage-availability.md)합니다.

Azure는 hello 가상 컴퓨터를 만듭니다.

Hello 가상 컴퓨터를 만든 후에 hello 도메인 컨트롤러를 구성 합니다.

### <a name="configure-hello-domain-controller"></a>Hello 도메인 컨트롤러 구성
Hello에서 다음 단계는 hello 구성 **ad-주-dc** corp.contoso.com에 대 한 도메인 컨트롤러로 컴퓨터.

1. Hello 포털을 열고 hello **SQL-HA-RG** 리소스 그룹을 선택 하는 hello **ad-주-dc** 컴퓨터입니다. Hello에 **ad-주-dc** 블레이드에서 클릭 **연결** tooopen는 RDP 파일에서 원격 데스크톱 액세스 합니다.

    ![Tooa 가상 컴퓨터에 연결](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/20-connectrdp.png)
2. 구성된 관리자 계정(**\DomainAdmin**) 및 암호(**Contoso!0000**)로 로그인합니다.
3. 기본적으로 hello **서버 관리자** 대시보드가 표시 되어야 합니다.
4. Hello 클릭 **역할 및 기능 추가** hello 대시보드에서 링크 합니다.

    ![서버 관리자 - 역할 추가](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
5. 선택 **다음** toohello에 도달할 때까지 **서버 역할** 섹션.
6. 선택 hello **Active Directory 도메인 서비스** 및 **DNS 서버** 역할입니다. 메시지가 표시되면 이러한 역할에 필요한 기능을 더 추가합니다.

   > [!NOTE]
   > 정적 IP 주소가 없다는 경고가 표시됩니다. 클릭 하 여 hello 구성, 테스트 하려는 경우 **계속**합니다. 프로덕션 시나리오에 대 한 IP 주소 toostatic hello hello Azure 포털에서에서 설정 또는 [hello 도메인 컨트롤러 컴퓨터의 PowerShell tooset hello 고정 IP 주소를 사용 하 여](../../../virtual-network/virtual-networks-reserved-private-ip.md)합니다.
   >
   >

    ![역할 추가 대화 상자](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/23-addroles.png)
7. 클릭 **다음** hello에 도달할 때까지 **확인** 섹션. 선택 hello **필요한 경우 자동으로 hello 대상 서버 다시 시작** 확인란 합니다.
8. **Install**을 클릭합니다.
9. Hello 기능 설치, 반환 toohello 완료 된 후 **서버 관리자** 대시보드 합니다.
10. 새 선택 hello **AD DS** hello 왼쪽 창에서 옵션입니다.
11. Hello 클릭 **자세한** hello 노란색 경고 표시줄에 링크 합니다.

    ![Hello DNS 서버 VM에 AD DS 대화 상자](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/24-addsmore.png)
12. Hello에 **동작** hello 열 **모든 서버에 대 한 작업 세부 정보** 대화 상자에서 클릭 **이 서버 tooa 도메인 컨트롤러의 수준을 올린**합니다.
13. Hello에 **Active Directory 도메인 서비스 구성 마법사**를 다음 값에는 hello를 사용 하 여:

    | **Page** | 설정 |
    | --- | --- |
    | **배포 구성** |**새 포리스트 추가**<br/> **루트 도메인 이름** = corp.contoso.com |
    | **도메인 컨트롤러 옵션** |**암호** = Contoso!0000<br/>**암호 확인** = Contoso!0000 |
14. 클릭 **다음** 통해 toogo hello hello 마법사의 다른 페이지. Hello에 **필수 구성 요소 확인** 페이지, hello 메시지의 뒤에 표시 되는지 확인: **모든 필수 구성 요소 검사를 통과 했습니다**합니다. 모든 적용 가능한 경고 메시지를 검토할 수 있지만 가능한 toocontinue hello 설치.
15. **Install**을 클릭합니다. hello **ad-주-dc** 가상 컴퓨터가 자동으로 다시 시작 합니다.

### <a name="note-hello-ip-address-of-hello-primary-domain-controller"></a>Note hello 주 도메인 컨트롤러의 hello IP 주소

DNS에 대 한 hello 주 도메인 컨트롤러를 사용 합니다. Note hello 주 도메인 컨트롤러 IP 주소입니다.

Hello Azure 포털을 통해 한 가지 방법은 tooget hello 주 도메인 컨트롤러 IP 주소가입니다.

1. Azure 포털 hello hello 리소스 그룹을 엽니다.

2. Hello 주 도메인 컨트롤러를 클릭 합니다.

3. Hello 주 도메인 컨트롤러 블레이드에서 클릭 **네트워크 인터페이스**합니다.

![네트워크 인터페이스](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/25-primarydcip.png)

이 서버에 대 한 hello 개인 IP 주소를 note 합니다.

### <a name="configure-hello-virtual-network-dns"></a>Hello 가상 네트워크 DNS 구성
Hello 첫 번째 도메인 컨트롤러를 만들고 hello 첫 번째 서버에서 DNS를 활성화 한 후이 서버를 구성 hello 가상 네트워크 toouse이 DNS에 대 한 합니다.

1. Hello Azure 포털에서에서 hello 가상 네트워크를 클릭 합니다.

2. **설정**에서 **DNS 서버**를 클릭합니다.

3. 클릭 **사용자 지정**, hello hello 주 도메인 컨트롤러의 개인 IP 주소를 입력 합니다.

4. **Save**를 클릭합니다.

### <a name="configure-hello-second-domain-controller"></a>Hello 두 번째 도메인 컨트롤러를 구성 합니다.
Hello 주 도메인 컨트롤러를 다시 부팅 후 hello 두 번째 도메인 컨트롤러를 구성할 수 있습니다. 이 선택적 단계는 가용성을 높이기 위한 것입니다. 이러한 단계 tooconfigure hello 두 번째 도메인 컨트롤러를 수행 합니다.

1. Hello 포털을 열고 hello **SQL-HA-RG** 리소스 그룹을 선택 하는 hello **ad 보조 dc** 컴퓨터입니다. Hello에 **ad 보조 dc** 블레이드에서 클릭 **연결** tooopen는 RDP 파일에서 원격 데스크톱 액세스 합니다.
2. 구성 된 관리자 계정을 사용 하 여 toohello VM에에서 로그인 (**BUILTIN\DomainAdmin**) 및 암호 (**Contoso! 0000**).
3. 변경 hello hello 도메인 컨트롤러의 DNS 서버 주소 toohello 주소를 기본 설정입니다.
4. **네트워크 및 공유 센터**를 hello 네트워크 인터페이스를 클릭 합니다.
   ![네트워크 인터페이스](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/26-networkinterface.png)

5. **속성**을 클릭합니다.
6. **인터넷 프로토콜 버전 4(TCP/IPv4)**를 선택하고 **속성**을 클릭합니다.
7. 선택 **다음 DNS 서버 주소를 사용 하 여 hello** hello 주 도메인 컨트롤러의 hello 주소를 지정 하 고 **기본 설정 DNS 서버**합니다.
8. 클릭 **확인**, 차례로 **닫기** toocommit hello 변경 합니다. 현재 위치는 VM 수 toojoin hello 너무**corp.contoso.com**합니다.

   >[!IMPORTANT]
   >Hello DNS 설정을 변경한 후 hello 연결 tooyour 원격 데스크톱을 손실 된 경우 toohello Azure 포털 및 다시 시작 hello 가상 컴퓨터를 이동 합니다.

9. Hello 원격 데스크톱 toohello 보조 도메인 컨트롤러에서 열고 **서버 관리자 대시보드**합니다.
10. Hello 클릭 **역할 및 기능 추가** hello 대시보드에서 링크 합니다.

    ![서버 관리자 - 역할 추가](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
11. 선택 **다음** toohello에 도달할 때까지 **서버 역할** 섹션.
12. 선택 hello **Active Directory 도메인 서비스** 및 **DNS 서버** 역할입니다. 메시지가 표시되면 이러한 역할에 필요한 기능을 더 추가합니다.
13. Hello 기능 설치, 반환 toohello 완료 된 후 **서버 관리자** 대시보드 합니다.
14. 새 선택 hello **AD DS** hello 왼쪽 창에서 옵션입니다.
15. Hello 클릭 **자세한** hello 노란색 경고 표시줄에 링크 합니다.
16. Hello에 **동작** hello 열 **모든 서버에 대 한 작업 세부 정보** 대화 상자에서 클릭 **이 서버 tooa 도메인 컨트롤러의 수준을 올린**합니다.
17. 아래 **배포 구성**선택, **도메인 컨트롤러 tooan 기존 도메인을 추가**합니다.
   ![배포 구성](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/28-deploymentconfig.png)
18. **선택**을 클릭합니다.
19. Hello 관리자 계정을 사용 하 여 연결 (**CORP. CONTOSO.COM\domainadmin**) 및 암호 (**Contoso! 0000**).
20. **hello 포리스트에서 도메인을 선택**, 해당 도메인을 클릭 하 고 클릭 **확인**합니다.
21. **도메인 컨트롤러 옵션**hello 기본값을 사용 하 고 DSRM 암호를 설정 합니다.

   >[!NOTE]
   >hello **DNS 옵션** 페이지 수 있어도 경고이 DNS 서버에 대 한 위임을 만들 수 없습니다. 비-프로덕션 환경에서 이 경고를 무시할 수 있습니다.
22. 클릭 **다음** hello 대화 hello에 도달할 때까지 **필수 구성 요소** 확인 합니다. **설치**를 클릭합니다.

Hello 서버 hello 구성 변경을 완료 되 면 hello 서버를 다시 시작 합니다.

### <a name="add-hello-private-ip-address-toohello-second-domain-controller-toohello-vpn-dns-server"></a>Hello 개인 IP 주소가 toohello 두 번째 도메인 컨트롤러 toohello VPN DNS 서버를 추가 합니다.

Azure 포털에서 가상 네트워크 hello hello 보조 도메인 컨트롤러의 hello DNS 서버 tooinclude hello IP 주소를 변경 합니다. 따라서 hello DNS 서비스 중복성을 수 있습니다.

### <a name=DomainAccounts></a>Hello 도메인 계정 구성

Hello 다음 단계에서 hello Active Directory 계정을 구성합니다. hello 아래 표에 나와 hello 계정.

| |설치 계정<br/> |sqlserver-0 <br/>SQL Server 및 SQL 에이전트 서비스 계정 |sqlserver-1<br/>SQL Server 및 SQL 에이전트 서비스 계정
| --- | --- | --- | ---
|**이름** |Install |SQLSvc1 | SQLSvc2
|**사용자 SamAccountName** |Install |SQLSvc1 | SQLSvc2

다음 단계 toocreate hello 각 계정을 사용 합니다.

1. Toohello 로그인 **ad-주-dc** 컴퓨터입니다.
2. **서버 관리자**에서 **도구**를 선택한 후 **Active Directory 관리 센터**를 클릭합니다.   
3. 선택 **corp (로컬)** hello 왼쪽된 창에서.
4. Hello 오른쪽에 **작업** 창 선택 **새로**, 클릭 하 고 **사용자**합니다.
   ![Active Directory 관리 센터](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/29-addcnewuser.png)

   >[!TIP]
   >각 계정에 대해 복잡한 암호를 설정합니다.<br/> 비-프로덕션 환경에 대 한 집합 hello 사용자 계정 toonever 만료 됩니다.

5. 클릭 **확인** toocreate hello 사용자입니다.
6. Hello 각 hello 세 가지 계정에 대해 이전 단계를 반복 합니다.

### <a name="grant-hello-required-permissions-toohello-installation-account"></a>사용 권한이 필요한 hello toohello 설치 계정
1. Hello에 **Active Directory 관리 센터**선택, **corp (로컬)** hello 왼쪽된 창에서. 그런 다음 오른쪽 hello **작업** 창에서 클릭 **속성**합니다.

    ![CORP 사용자 속성](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/31-addcproperties.png)
2. 선택 **확장**, hello를 클릭 한 다음 **고급** hello 단추 **보안** 탭 합니다.
3. Hello에 **회사의 고급 보안 설정** 대화 상자를 클릭 하 여 **추가**합니다.
4. **보안 주체 선택**을 클릭하고, **CORP\Install**을 검색하고 나서, **확인**을 클릭합니다.
5. 선택 hello **모든 속성 읽기** 확인란 합니다.

6. 선택 hello **컴퓨터 개체 만들기** 확인란 합니다.

     ![Corp 사용자 권한](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/33-addpermissions.png)
7. **확인**을 클릭한 후 **확인**을 한 번 더 클릭합니다. 닫기 hello **corp** 속성 창.

Active Directory와 hello 사용자 개체의 구성을 완료 했으므로 두 SQL Server Vm 및 미러링 모니터 서버 VM 만듭니다. 그런 다음 모든 세 toohello 도메인에 가입 합니다.

## <a name="create-sql-server-vms"></a>SQL Server VM 만들기

3개의 가상 컴퓨터를 추가로 만듭니다. hello 솔루션에는 SQL Server 인스턴스에서 두 개의 가상 컴퓨터가 필요합니다. 세 번째 가상 컴퓨터는 미러링 모니터 서버로 작동됩니다. Windows Server 2016에서는 [미러링 모니터 서버](http://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness)를 사용할 수 있지만, 이전 운영 체제와의 일관성을 위해 이 문서에서는 미러링 모니터 서버로 가상 컴퓨터를 사용합니다.  

계속 진행 하기 전에 hello를 deisign 의사 결정을 따르는 것이 좋습니다.

* **저장소 - Azure Managed Disks**

   Hello 가상 컴퓨터 저장소에 대 한 Azure 관리 되는 디스크를 사용 합니다. SQL Server 가상 컴퓨터에 대해 Managed Disks가 권장됩니다. Hello 백그라운드 핸들 저장소 디스크를 관리합니다. 또한 관리 되는 디스크와 가상 컴퓨터에에서 있는 경우 hello 동일한 가용성 집합에 Azure hello 저장소 리소스 tooprovide 적절 한 중복 배포 합니다. 자세한 내용은 [Azure Managed Disks 개요](../managed-disks-overview.md)를 참조하세요. 가용성 집합의 Managed Disks에 대한 구체적인 내용을 보려면 [가용성 집합에서 VM에 Managed Disks 사용](../manage-availability.md#use-managed-disks-for-vms-in-an-availability-set)을 참조하세요.

* **네트워크 - 프로덕션 환경의 개인 IP 주소**

   이 자습서에서는 hello 가상 컴퓨터에 대 한 공용 IP 주소를 사용 합니다. 이렇게 하면 원격 연결을 통해 가상 컴퓨터 toohello hello 인터넷 직접-쉽게 구성 단계입니다. 프로덕션 환경에서는 순서 tooreduce hello 보안 취약성을 hello SQL Server 인스턴스의 VM 리소스의 개인 IP 주소만을 좋습니다.

### <a name="create-and-configure-hello-sql-server-vms"></a>만들기 및 구성 hello SQL Server Vm
다음으로 추가 클러스터 노드의 VM 1개와 SQL Server VM 2개를 포함하는 VM을 3개 만듭니다. 각 toocreate hello Vm의 toohello 돌아가서 **SQL-HA-RG** 리소스 그룹에서 클릭 **추가**, hello 적절 한 갤러리 항목에 대 한 검색, 클릭 **가상 컴퓨터**, 한 다음 클릭 **갤러리에서**합니다. Hello 정보를 사용 하 여 hello Vm을 만들 테이블 toohelp 다음 hello에:


| Page | VM1 | VM2 | VM3 |
| --- | --- | --- | --- |
| Hello 적절 한 갤러리 항목 선택 |**Windows Server 2016 Datacenter** |**Windows Server 2016의 SQL Server 2016 SP1 Enterprise** |**Windows Server 2016의 SQL Server 2016 SP1 Enterprise** |
| 가상 컴퓨터 구성 **기본 사항** |**이름** = cluster-fsw<br/>**사용자 이름** = DomainAdmin<br/>**암호** = Contoso!0000<br/>**구독** = 사용자 구독<br/>**리소스 그룹** = SQL-HA-RG<br/>**위치** = 해당 Azure 위치 |**이름** = sqlserver-0<br/>**사용자 이름** = DomainAdmin<br/>**암호** = Contoso!0000<br/>**구독** = 사용자 구독<br/>**리소스 그룹** = SQL-HA-RG<br/>**위치** = 해당 Azure 위치 |**이름** = sqlserver-1<br/>**사용자 이름** = DomainAdmin<br/>**암호** = Contoso!0000<br/>**구독** = 사용자 구독<br/>**리소스 그룹** = SQL-HA-RG<br/>**위치** = 해당 Azure 위치 |
| 가상 컴퓨터 구성 **크기** |**크기** = DS1\_V2(1 코어, 3.5GB) |**크기** = DS2\_V2(2 코어, 7GB)</br>hello 크기 (프리미엄 디스크 지원 SSD 저장소를 지원 해야 합니다 합니다. )) |**크기** = DS2\_V2(2 코어, 7GB) |
| 가상 컴퓨터 구성 **설정** |**저장소**: Managed Disks 사용<br/>**가상 네트워크** = autoHAVNET<br/>**서브넷** = sqlsubnet(10.1.1.0/24)<br/>**공용 IP 주소**: 자동으로 생성됩니다.<br/>**네트워크 보안 그룹** = 없음<br/>**진단 모니터링** = 사용<br/>**진단 Storage 계정** = 자동으로 생성된 Storage계정 사용<br/>**가용성 집합** = sqlAvailabilitySet<br/> |**저장소**: Managed Disks 사용<br/>**가상 네트워크** = autoHAVNET<br/>**서브넷** = sqlsubnet(10.1.1.0/24)<br/>**공용 IP 주소**: 자동으로 생성됩니다.<br/>**네트워크 보안 그룹** = 없음<br/>**진단 모니터링** = 사용<br/>**진단 Storage 계정** = 자동으로 생성된 Storage계정 사용<br/>**가용성 집합** = sqlAvailabilitySet<br/> |**저장소**: Managed Disks 사용<br/>**가상 네트워크** = autoHAVNET<br/>**서브넷** = sqlsubnet(10.1.1.0/24)<br/>**공용 IP 주소**: 자동으로 생성됩니다.<br/>**네트워크 보안 그룹** = 없음<br/>**진단 모니터링** = 사용<br/>**진단 Storage 계정** = 자동으로 생성된 Storage계정 사용<br/>**가용성 집합** = sqlAvailabilitySet<br/> |
| 가상 컴퓨터 구성 **SQL Server 설정** |해당 없음 |**SQL 연결** = 개인(가상 네트워크 내)<br/>**포트** = 1433<br/>**SQL 인증** = 사용 안 함<br/>**Storage 구성** = 일반<br/>**자동화된 패치** = 일요일 2시<br/>**자동화된 백업** = 사용 안 함</br>**Azure 주요 자격 증명 모음 통합** = 사용 안 함 |**SQL 연결** = 개인(가상 네트워크 내)<br/>**포트** = 1433<br/>**SQL 인증** = 사용 안 함<br/>**Storage 구성** = 일반<br/>**자동화된 패치** = 일요일 2시<br/>**자동화된 백업** = 사용 안 함</br>**Azure 주요 자격 증명 모음 통합** = 사용 안 함 |

<br/>

> [!NOTE]
> 여기서 제안 하는 hello 컴퓨터 크기는 Azure Vm에서 가용성 그룹을 테스트 하기 위한 것입니다. 프로덕션 작업에 최상의 성능을 얻으려면 hello hello 및 권장 사항은 SQL Server 컴퓨터 크기 구성을 참조 하십시오. [Azure 가상 컴퓨터에서 SQL Server에 대 한 성능 모범 사례](virtual-machines-windows-sql-performance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
>
>

Toojoin hello 세 Vm이 완전히 프로 비전 한 후 해야 해당 toohello **corp.contoso.com** CORP\Install 관리자 권한 toohello 컴퓨터 도메인 및 부여 합니다.

### <a name="joinDomain"></a>Hello 서버 toohello 도메인에 가입

이제 수 toojoin hello Vm 너무 넌**corp.contoso.com**합니다. Hello hello SQL Server Vm 및 hello 파일 모두에 대해 다음을 수행 미러링 모니터 서버를 공유 합니다.

1. Toohello 가상 컴퓨터를 원격으로 연결 **BUILTIN\DomainAdmin**합니다.
2. **서버 관리자**에서 **로컬 서버**를 클릭합니다.
3. Hello 클릭 **작업 그룹** 링크 합니다.
4. Hello에 **컴퓨터 이름** 섹션에서 클릭 **변경**합니다.
5. 선택 hello **도메인** 확인란과 형식 **corp.contoso.com** hello 텍스트 상자에 있습니다. **확인**을 클릭합니다.
6. Hello에 **Windows 보안** 팝업 대화 상자 hello 기본 도메인 관리자 계정에 대 한 hello 자격 증명 지정 (**CORP\DomainAdmin**) 및 hello 암호 (**Contoso! 0000**).
7. Hello "시작 toohello corp.contoso.com 도메인" 메시지가 나타나면 클릭 **확인**합니다.
8. 클릭 **닫기**, 클릭 하 고 **지금 다시 시작** hello 팝업 대화 상자에서.

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-cluster-vm"></a>각 클러스터 VM에서 관리자 권한으로 hello Corp\Install 사용자 추가

Hello 도메인의 구성원으로 각 가상 컴퓨터를 다시 시작한 후 추가 **CORP\Install** hello 로컬 관리자 그룹의 구성원으로 합니다.

1. Hello VM을 다시 시작 될 때까지 기다린 후에 주 도메인 컨트롤러 toosign hello에서 다시 hello RDP 파일을 너무 시작**sqlserver-0** hello를 사용 하 여 **CORP\DomainAdmin** 계정.
   >[!TIP]
   >Hello 도메인 관리자 계정으로 로그인 하 고 있는지 확인 합니다. Hello 이전 단계에서 hello에 기본 제공 관리자 계정을 사용 했습니다. Hello 서버 이면 hello 도메인 했으므로 hello 도메인 계정을 사용 합니다. RDP 세션에서 *도메인*\\*사용자 이름*을 지정합니다.

2. **서버 관리자**에서 **도구**를 선택하고 **컴퓨터 관리**를 클릭합니다.
3. Hello에 **컴퓨터 관리** 창 확장 **로컬 사용자 및 그룹**를 선택한 후 **그룹**합니다.
4. Hello를 두 번 클릭 **관리자** 그룹입니다.
5. Hello에 **Administrators 속성** 대화 상자에서 hello 클릭 **추가** 단추입니다.
6. Hello 사용자 입력 **CORP\Install**, 클릭 하 고 **확인**합니다.
7. 클릭 **확인** tooclose hello **관리자 속성** 대화 상자.
8. hello 이전 단계를 반복 **sqlserver-1** 및 **클러스터 fsw**합니다.

### <a name="setServiceAccount"></a>Hello SQL Server 서비스 계정 설정

각 SQL Server VM에서 hello SQL Server 서비스 계정을 설정 합니다. Hello 계정을 만든 경우 사용 하면 [hello 도메인 계정을 구성](#DomainAccounts)합니다.

1. **SQL Server 구성 관리자**를 엽니다.
2. Hello SQL Server 서비스를 마우스 오른쪽 단추로 누른 **속성**합니다.
3. Hello 계정 및 암호를 설정 합니다.
4. 다른 SQL Server VM hello에서 이러한 단계를 반복 합니다.  

SQL Server 가용성 그룹에 대 한 각 SQL Server VM을 도메인 계정으로 toorun을 필요합니다.

### <a name="create-a-sign-in-on-each-sql-server-vm-for-hello-installation-account"></a>Hello 설치 계정에 대 한 각 SQL Server VM에는 로그인 만들기

Hello 설치 계정 (CORP\install) tooconfigure hello 가용성 그룹을 사용 합니다. 이 계정에 있어야 toobe hello 소속 **sysadmin** 각 SQL Server VM에서 고정된 서버 역할입니다. hello 다음 단계는 로그인 기능을 만드는 hello 설치 계정:

1. Hello를 사용 하 여 toohello 서버 hello 프로토콜 RDP (원격 데스크톱)를 통해 연결  *\<MachineName\>\DomainAdmin* 계정.

1. SQL Server Management Studio를 열고 toohello SQL Server의 로컬 인스턴스에 연결 합니다.

1. **개체 탐색기**에서 **보안**을 클릭합니다.

1. 마우스 오른쪽 단추로 **로그인**을 클릭합니다. **새 로그인**을 클릭합니다.

1. **로그인 - 신규**에서 **검색**을 클릭합니다.

1. **위치**를 클릭합니다.

1. Hello 도메인 관리자 네트워크 자격 증명을 입력 합니다.

1. Hello 설치 계정을 사용 합니다.

1. Hello의 멤버인 로그인 toobe hello 설정 **sysadmin** 고정된 서버 역할입니다.

1. **확인**을 클릭합니다.

Hello 앞에 다른 SQL Server VM hello에서 단계를 반복 합니다.

## <a name="add-failover-clustering-features-tooboth-sql-server-vms"></a>장애 조치 클러스터링 기능 tooboth SQL Server Vm 추가

tooadd 장애 조치 클러스터링 기능을 모두 SQL Server Vm에 따라 hello지 않습니다.

1. Hello를 사용 하 여 hello 프로토콜 RDP (원격 데스크톱)를 통해 toohello SQL Server 가상 컴퓨터를 연결 *CORP\install* 계정. **서버 관리자 대시보드**를 엽니다.
2. Hello 클릭 **역할 및 기능 추가** hello 대시보드에서 링크 합니다.

    ![서버 관리자 - 역할 추가](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
3. 선택 **다음** toohello에 도달할 때까지 **서버 기능** 섹션.
4. **기능**에서 **장애 조치 클러스터링**을 선택합니다.
5. 필요한 추가 기능을 추가합니다.
6. 클릭 **설치** tooadd hello 기능입니다.

다른 SQL Server VM hello에서 hello 단계를 반복 합니다.

## <a name="a-nameendpoint-firewall-configure-hello-firewall-on-each-sql-server-vm"></a><a name="endpoint-firewall">각 SQL Server VM에서 hello 방화벽을 구성 합니다.

hello 솔루션 hello를 toobe hello 방화벽에서 열어야 하는 TCP 포트를 다음 사항이 필요 합니다.

- **SQL Server VM**:<br/>
   SQL Server의 기본 인스턴스의 경우 포트 1433입니다.
- **Azure Load Balancer 프로브:**<br/>
   사용 가능한 모든 포트입니다. 예제는 59999를 자주 사용합니다.
- **데이터베이스 미러링 끝점:** <br/>
   사용 가능한 모든 포트입니다. 예제는 5022를 자주 사용합니다.

hello 방화벽 포트 요구 toobe 두 SQL Server Vm에서 열려 있습니다.

hello 포트를 열 hello 메서드 hello 방화벽을 사용 하면에 따라 달라 집니다. hello 다음 섹션에서는 tooopen hello Windows 방화벽에서 포트 하는 방법을 설명 합니다. 각 SQL Server Vm에 필요한 hello 포트를 엽니다.

### <a name="open-a-tcp-port-in-hello-firewall"></a>Hello 방화벽에서 TCP 포트 열기

1. 첫 번째 SQL Server hello **시작** 화면을 시작 하며, **고급 보안이 포함 된 Windows 방화벽**합니다.
2. Hello 왼쪽된 창에서 선택 **인바운드 규칙**합니다. Hello 오른쪽 창에서 클릭 **새 규칙**합니다.
3. **규칙 유형**에 **포트**를 선택합니다.
4. Hello 포트에 대 한 지정 **TCP** 및 포트 번호를 적절 한 형식 hello 합니다. 다음 예제는 hello를 참조 하십시오.

   ![SQL 방화벽](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/35-tcpports.png)

5. **다음**을 누릅니다.
6. Hello에 **동작** 페이지에서 유지 **hello 연결 허용** 을 선택한 다음 클릭 **다음**합니다.
7. Hello에 **프로필** 페이지 hello 기본 설정을 적용 하 고 클릭 **다음**합니다.
8. Hello에 **이름** 페이지 규칙 이름을 지정 합니다 (같은 **Azure LB 프로브**) hello에 **이름** 텍스트 상자 및 클릭 한 다음 **완료**합니다.

두 번째 SQL Server VM hello 하는에 이러한 단계를 반복 합니다.

## <a name="next-steps"></a>다음 단계

* [Azure Virtual Machines에서 SQL Server Always On 가용성 그룹 만들기](virtual-machines-windows-portal-sql-availability-group-tutorial.md)
