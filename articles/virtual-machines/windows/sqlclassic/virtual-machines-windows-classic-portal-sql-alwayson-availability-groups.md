---
title: "aaaConfigure Always On 가용성 그룹 Azure 가상 컴퓨터 (클래식)에서 | Microsoft Docs"
description: "Azure Virtual Machines로 Always On 가용성 그룹을 만듭니다. 이 자습서는 주로 hello 사용자 인터페이스 및 도구 보다는 스크립트를 사용합니다."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 8d48a3d2-79f8-4ab0-9327-2f30ee0b2ff1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: f428ad994a55378c281c959f4696fdcaf50632b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-virtual-machines-classic"></a>Azure Virtual Machines의 Always On 가용성 그룹 구성(클래식)
> [!div class="op_single_selector"]
> * [클래식: UI](../classic/portal-sql-alwayson-availability-groups.md)
> * [클래식: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

시작하기 전에 이제 Azure Resource Manager 모델에서 이 작업을 완료할 수 있는지 확인하는 것이 좋습니다. 새 배포에는 Azure Resource Manager 모델을 사용하는 것이 좋습니다. [Azure Virtual Machines의 SQL Server Always On 가용성 그룹](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md)을 참조하세요.

> [!IMPORTANT] 
> 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. Azure는 두 개의 서로 다른 배포 모델 toocreate 및 리소스 사용: [리소스 관리자 및 기본](../../../azure-resource-manager/resource-manager-deployment-model.md)합니다. 이 문서에서는 toouse 클래식 배포 모델을 hello 하는 방법을 설명 합니다. 

toocomplete hello Azure 리소스 관리자 모델에서는이 작업 참조 [Azure 가상 컴퓨터에 SQL Server Always On 가용성 그룹](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md)합니다.

이 종단 간 자습서에서 사용 하 여 SQL Server 항상 Azure 가상 컴퓨터에서 실행 되 가용성 tooimplement 그룹화 하는 방법을 보여 줍니다.

Hello 자습서의 hello 끝 요소 다음 hello Azure에서 SQL Server Always On 솔루션 구성 됩니다.

* 여러 서브넷과 프런트 엔드 및 백 엔드 서브넷을 포함하는 가상 네트워크
* Active Directory(Azure AD) 도메인을 포함한 도메인 컨트롤러
* SQL Server를 실행 하 고 배포 된 toohello 백 엔드 서브넷 및 도메인에 가입된 toohello Azure AD는 두 개의 가상 컴퓨터
* Hello 노드 과반수 쿼럼 모델을 사용 하 여 3 개 노드 장애 조치 클러스터
* 가용성 데이터베이스의 두 개의 동기 커밋 복제본이 포함된 가용성 그룹

다음 그림 hello는 hello 솔루션의 그래픽 표현입니다.

![Azure에서 가용성 그룹에 대한 테스트 랩 아키텍처](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC791912.png)

이것은 가능한 구성 중 하나입니다. 예를 들어 hello 2 복제본 가용성 그룹에 대 한 가상 컴퓨터 수를 최소화할 수 있습니다. 이 구성은 hello 2 개 노드 클러스터에서 쿼럼 파일 공유 감시로 hello 도메인 컨트롤러를 사용 하 여 Azure에서 계산 시간에 저장 합니다. 이 메서드는 hello 설명 구성에서 씩 hello 가상 컴퓨터 수를 줄입니다.

이 자습서에서는 hello 다음을 가정합니다.

* Azure 계정이 있습니다.
* 이미 어떻게 toouse hello GUI hello 가상 컴퓨터 갤러리 tooprovision에서 SQL Server를 실행 하는 클래식 가상 컴퓨터를 알고 있습니다.
* Always On 가용성 그룹을 확실하게 이해하고 있습니다. 자세한 내용은 [Always On 가용성 그룹(SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx)을 참조하세요.

> [!NOTE]
> SharePoint와 Always On 가용성 그룹을 사용하는 것에 관심이 있는 경우 [Configure SQL Server 2012 Always On Availability Groups for SharePoint 2013](https://technet.microsoft.com/library/jj715261.aspx)(SharePoint 2013에 대해 SQL Server 2012 Always On 가용성 그룹 구성)을 참조하세요.
> 
> 

## <a name="create-hello-virtual-network-and-domain-controller-server"></a>Hello 가상 네트워크 및 도메인 컨트롤러 서버 만들기
새로운 Azure 평가판 계정으로 시작합니다. 계정을 설정한 후 hello hello Azure 클래식 포털의 홈 화면에 있어야 합니다.

1. Hello 클릭 **새로** hello hello 다음 스크린 샷에서 같이 hello 페이지 아래쪽의 hello 왼쪽된 모서리에 있는 단추입니다.
   
    ![Hello 포털에서 새로 만들기를 클릭 합니다.](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665511.gif)
2. 클릭 **네트워크 서비스** > **가상 네트워크** > **사용자 지정 만들기**hello 스크린 샷 뒤에 나타난 것 처럼 합니다.
   
    ![가상 네트워크 만들기](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665512.gif)
3. Hello에 **가상 네트워크 만들기** 대화 상자, hello 페이지를 단계별로 실행 하 고 다음 표에 hello의 hello 설정을 사용 하 여 새 가상 네트워크를 만듭니다. 
   
   | Page | 설정 |
   | --- | --- |
   | 가상 네트워크 세부 정보 |**이름 = ContosoNET**<br/>**지역 = 미국 서부** |
   | DNS 서버 및 VPN 연결 |없음 |
   | 가상 네트워크 주소 공간 |설정은 다음 스크린 샷 hello에 나와 있습니다. ![가상 네트워크 만들기](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784620.png) |
4. Hello 도메인 컨트롤러 (DC)으로 사용할 hello 가상 컴퓨터를 만듭니다. 클릭 **새로** > **계산** > **가상 컴퓨터** > **갤러리에서**에 나타난 것 처럼 다음 스크린 샷 번호입니다.
   
    ![가상 컴퓨터 만들기](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784621.png)
5. Hello에 **가상 컴퓨터 만들기** 대화 상자, hello 페이지를 단계별로 실행 하 고 다음 표에 hello의 hello 설정을 사용 하 여 새 가상 컴퓨터를 구성 합니다. 
   
   | Page | 설정 |
   | --- | --- |
   | Hello 가상 컴퓨터 운영 체제를 선택 합니다. |Windows Server 2012 R2 Datacenter |
   | 가상 컴퓨터 구성 |**버전 릴리스 날짜** = (latest)<br/>**가상 컴퓨터 이름** = ContosoDC<br/>**계층** = 표준<br/>**크기** = A2(2코어)<br/>**새 사용자 이름** = AzureAdmin<br/>**새 암호** = Contoso!000<br/>**확인** = Contoso!000 |
   | 가상 컴퓨터 구성 |**클라우드 서비스** = 새 클라우드 서비스 만들기<br/>**클라우드 서비스 DNS 이름** = 고유한 클라우드 서비스 이름<br/>**DNS 이름** = 고유 이름(예: ContosoDC123)<br/>**지역/선호도 그룹/가상 네트워크** = ContosoNET<br/>**가상 네트워크 서브넷** = Back(10.10.2.0/24)<br/> **계정** = 자동으로 생성된 Storage 계정 사용<br/>**가용성 집합** = (없음) |
   | 가상 컴퓨터 옵션 |기본값 사용 |

Hello 새 가상 컴퓨터를 구성한 후 hello 가상 컴퓨터 toobe이 프로 비전 될 때까지 기다립니다. 이 프로세스는 몇 가지 시간 toofinish를 걸립니다. Hello를 누르면 **가상 컴퓨터** 탭 hello Azure 클래식 포털에서 볼 수 있습니다에서 ContosoDC 순환 상태가 **시작 (프로 비전)** 너무**Stopped**, **시작**, **실행 중 (프로 비전)**, 마지막으로 **실행**합니다.

hello DC 서버가 이제 구축 했습니다. 다음으로,이 DC 서버에는 hello Active Directory 도메인을 구성 합니다.

## <a name="configure-hello-domain-controller"></a>Hello 도메인 컨트롤러 구성
다음 단계는 hello, corp.contoso.com에 대 한 도메인 컨트롤러로 hello ContosoDC 컴퓨터를 구성 합니다.

1. Hello 포털에서 선택 hello **ContosoDC** 컴퓨터입니다. Hello에 **대시보드** 탭을 클릭 **연결** tooopen 원격 데스크톱 액세스에 대 한 원격 데스크톱 (RDP) 파일입니다.
   
    ![TooVritual 컴퓨터 연결](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784622.png)
2. 구성된 관리자 계정(**\AzureAdmin**) 및 암호(**Contoso!000**)로 로그인합니다.
3. 기본적으로 hello **서버 관리자** 대시보드가 표시 되어야 합니다.
4. Hello 클릭 **역할 및 기능 추가** hello 대시보드에서 링크 합니다.
   
    ![서버 탐색기 역할 추가](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784623.png)
5. 클릭 **다음** toohello에 도달할 때까지 **서버 역할** 섹션.
6. 선택 hello **Active Directory 도메인 서비스** 및 **DNS 서버** 역할입니다. 메시지가 표시되면 이러한 역할에 필요한 기능을 추가합니다.
   
   > [!NOTE]
   > 고정 IP 주소가 없다는 유효성 검사 경고 페이지가 표시됩니다. Hello 구성을 테스트 하는 경우 클릭 **계속**합니다. 프로덕션 시나리오에 대 한 [hello 도메인 컨트롤러 컴퓨터의 PowerShell tooset hello 고정 IP 주소를 사용 하 여](../../../virtual-network/virtual-networks-reserved-private-ip.md)합니다.
   > 
   > 
   
    ![역할 추가 대화 상자](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784624.png)
7. 클릭 **다음** hello에 도달할 때까지 **확인** 섹션. 선택 hello **필요한 경우 자동으로 hello 대상 서버 다시 시작** 확인란 합니다.
8. **Install**을 클릭합니다.
9. Hello 기능이 설치 된 후 반환 toohello **서버 관리자** 대시보드 합니다.
10. 새 선택 hello **AD DS** hello 왼쪽된 창에서 옵션입니다.
11. Hello 클릭 **자세한** hello 노란색 경고 표시줄에 링크 합니다.
    
     ![DNS 서버 가상 컴퓨터의 AD DS 대화 상자](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784625.png)
12. Hello에 **동작** hello의 열 **모든 서버에 대 한 작업 세부 정보** 대화 상자를 클릭 **이 서버 tooa 도메인 컨트롤러의 수준을 올린**합니다.
13. Hello에 **Active Directory 도메인 서비스 구성 마법사**를 다음 값에는 hello를 사용 하 여:
    
    | Page | 설정 |
    | --- | --- |
    | 배포 구성 |**새 포리스트 추가** = 선택됨<br/>**루트 도메인 이름** = corp.contoso.com |
    | 도메인 컨트롤러 옵션 |**암호** = Contoso!000<br/>**암호 확인** = Contoso!000 |
14. 클릭 **다음** 통해 toogo hello hello 마법사의 다른 페이지. Hello에 **필수 구성 요소 확인** 페이지, hello 메시지의 뒤에 표시 되는지 확인: **모든 필수 구성 요소 검사를 통과 했습니다**합니다. 적용 가능한 모든 경고 메시지를 검토 해야 하지만 hello 설치 가능한 toocontinue는 note 합니다.
15. **Install**을 클릭합니다. hello **ContosoDC** 가상 컴퓨터 자동으로 재부팅 됩니다.

## <a name="configure-domain-accounts"></a>도메인 계정 구성
hello 다음 단계에는 나중에 사용할 hello Active Directory 계정을 구성합니다.

1. 다시 로그인 toohello **ContosoDC** 컴퓨터입니다.
2. **서버 관리자**에서 **도구** > **Active Directory 관리 센터**를 클릭합니다.
   
    ![Active Directory 관리 센터](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784626.png)
3. Hello에 **Active Directory 관리 센터**선택, **corp (로컬)** hello 왼쪽된 창에서.
4. Hello 오른쪽에 **작업** 창에서 클릭 **새로** > **사용자**합니다. 다음 설정을 사용 하 여 hello:
   
   | 설정 | 값 |
   | --- | --- |
   | **이름** |Install |
   | **사용자 SamAccountName** |Install |
   | **암호** |Contoso!000 |
   | **암호 확인** |Contoso!000 |
   | **기타 암호 옵션** |선택 |
   | **암호 사용 기간 제한 없음** |선택 |
5. 클릭 **확인** toocreate hello **설치** 사용자입니다. 이 계정에 사용 되는 tooconfigure hello 클러스터와 hello 가용성 그룹 장애 조치 됩니다.
6. 두 개의 추가 사용자를 만들고 **CORP\SQLSvc1** 및 **CORP\SQLSvc2**, hello로 동일한 단계입니다. 이러한 계정은 hello SQL Server 인스턴스에 대해 사용 됩니다. 다음으로, toogive 해야 **CORP\Install** hello 필요한 권한을 tooconfigure Windows 장애 조치 클러스터링 합니다.
7. Hello에 **Active Directory 관리 센터**, 클릭 **corp (로컬)** hello 왼쪽된 창에서. Hello에 **작업** 창에서 클릭 **속성**합니다.
   
    ![CORP 사용자 속성](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784627.png)
8. 선택 **확장**, hello를 클릭 한 다음 **고급** hello 단추 **보안** 탭 합니다.
9. Hello에 **회사의 고급 보안 설정** 대화 상자를 클릭 **추가**합니다.
10. **보안 주체 선택**을 클릭하고, **CORP\Install**을 검색하고 나서, **확인**을 클릭합니다.
11. 선택 hello **모든 속성 읽기** 및 **컴퓨터 개체 만들기** 사용 권한.
    
     ![Corp 사용자 권한](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784628.png)
12. **확인**을 클릭한 후 **확인**을 한 번 더 클릭합니다. 닫기 hello corp 속성 창입니다.

Active Directory와 hello 사용자 개체를 구성 했으므로 세 개의 SQL Server 가상 컴퓨터를 만들고 쿼리하고 toothis 도메인에 가입 합니다.

## <a name="create-hello-sql-server-virtual-machines"></a>Hello SQL Server 가상 컴퓨터 만들기
3개의 가상 컴퓨터를 만듭니다. 하나는 클러스터 노드에 사용되고 두 개는 SQL Server에 사용됩니다. toohello Azure 클래식 포털을 다시 클릭 합니다. 각 toocreate hello 가상 컴퓨터의 이동 **새로** > **계산** > **가상 컴퓨터**  >  **갤러리에서**합니다. 그런 다음 다음 hello 가상 컴퓨터를 만들 테이블 toohelp hello hello 템플릿을 사용 합니다.

| Page | VM1 | VM2 | VM3 |
| --- | --- | --- | --- |
| Hello 가상 컴퓨터 운영 체제를 선택 합니다. |**Windows Server 2012 R2 Datacenter** |**SQL Server 2014 RTM Enterprise** |**SQL Server 2014 RTM Enterprise** |
| 가상 컴퓨터 구성 |**버전 릴리스 날짜** = (latest)<br/>**가상 컴퓨터 이름** = ContosoWSFCNode<br/>**계층** = 표준<br/>**크기** = A2(2코어)<br/>**새 사용자 이름** = AzureAdmin<br/>**새 암호** = Contoso!000<br/>**확인** = Contoso!000 |**버전 릴리스 날짜** = (latest)<br/>**가상 컴퓨터 이름** = ContosoSQL1<br/>**계층** = 표준<br/>**크기** = A3(4코어)<br/>**새 사용자 이름** = AzureAdmin<br/>**새 암호** = Contoso!000<br/>**확인** = Contoso!000 |**버전 릴리스 날짜** = (latest)<br/>**가상 컴퓨터 이름** = ContosoSQL2<br/>**계층** = 표준<br/>**크기** = A3(4코어)<br/>**새 사용자 이름** = AzureAdmin<br/>**새 암호** = Contoso!000<br/>**확인** = Contoso!000 |
| 가상 컴퓨터 구성 |**클라우드 서비스** = 이전에 만든 고유한 클라우드 서비스 DNS 이름(예: ContosoDC123)<br/>**지역/선호도 그룹/가상 네트워크** = ContosoNET<br/>**가상 네트워크 서브넷** = Back(10.10.2.0/24)<br/> **계정** = 자동으로 생성된 Storage 계정 사용<br/>**가용성 집합** = 가용성 집합 만들기<br/>**가용성 집합 이름** = SQLHADR |**클라우드 서비스** = 이전에 만든 고유한 클라우드 서비스 DNS 이름(예: ContosoDC123)<br/>**지역/선호도 그룹/가상 네트워크** = ContosoNET<br/>**가상 네트워크 서브넷** = Back(10.10.2.0/24)<br/>**계정** = 자동으로 생성된 Storage 계정 사용<br/>**가용성 집합** = SQLHADR (구성할 수도 있습니다 hello 가용성 hello 컴퓨터를 만든 후에 설정 합니다. 3 개의 컴퓨터가 할당 해야 toohello SQLHADR 가용성 집합입니다.) |**클라우드 서비스** = 이전에 만든 고유한 클라우드 서비스 DNS 이름(예: ContosoDC123)<br/>**지역/선호도 그룹/가상 네트워크** = ContosoNET<br/>**가상 네트워크 서브넷** = Back(10.10.2.0/24)<br/>**계정** = 자동으로 생성된 Storage 계정 사용<br/>**가용성 집합** = SQLHADR (구성할 수도 있습니다 hello 가용성 hello 컴퓨터를 만든 후에 설정 합니다. 3 개의 컴퓨터가 할당 해야 toohello SQLHADR 가용성 집합입니다.) |
| 가상 컴퓨터 옵션 |기본값 사용 |기본값 사용 |기본값 사용 |

<br/>

> [!NOTE]
> 이전 구성 hello 기본 계층 컴퓨터 부하 분산 끝점을 지원 하지 않으므로 표준 계층 가상 컴퓨터를 제안 합니다. 부하 분산 끝점 필요 이상 toocreate 가용성 그룹 수신기입니다. 또한 여기에 제안 된 hello 컴퓨터 크기는 Azure 가상 컴퓨터의 가용성 그룹을 테스트 하기 위한 것입니다. 프로덕션 작업에 최상의 성능을 얻으려면 hello hello 및 권장 사항은 SQL Server 컴퓨터 크기 구성을 참조 하십시오. [Azure 가상 컴퓨터의 SQL Server에 대 한 성능 모범 사례](../sql/virtual-machines-windows-sql-performance.md)합니다.
> 
> 

Toojoin hello 3 개의 가상 컴퓨터가 완전히 프로 비전 한 후 해야 해당 toohello **corp.contoso.com** CORP\Install 관리자 권한 toohello 컴퓨터 도메인 및 부여 합니다. toodo이를 사용 하 여 hello hello 3 가상 컴퓨터의 각 단계를 수행 합니다.

1. 먼저, hello 기본 설정 DNS 서버 주소를 변경 합니다. Hello 목록의 hello 가상 컴퓨터를 선택 하 고 hello를 클릭 하 여 각 가상 컴퓨터의 RDP 파일 tooyour 로컬 디렉터리에 다운로드 **연결** 단추입니다. tooselect 가상 컴퓨터를 hello 스크린 샷 다음 그림과 같이 hello 첫 번째 행의 셀에 hello 하지만 아무 곳 이나 클릭 합니다.
   
    ![Hello RDP 파일 다운로드](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664953.jpg)
2. 열기 hello RDP 파일을 다운로드 및 구성 된 관리자 계정을 사용 하 여 toohello 가상 컴퓨터에 로그인 (**BUILTIN\AzureAdmin**) 및 암호 (**Contoso! 000**).
3. 에 로그인 한 후 표시 되어야 hello **서버 관리자** 대시보드 합니다. 클릭 **로컬 서버** hello 왼쪽된 창에서.
4. Hello 클릭 **DHCP를 사용 하도록 설정 하는 i p v 6에서 할당 된 IPv4 주소** 링크 합니다.
5. Hello에 **네트워크 연결** 대화 상자 hello 네트워크 아이콘을 클릭 합니다.
   
    ![Hello 가상 컴퓨터 기본 설정 DNS 서버 변경](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784629.png)
6. Hello 명령 모음에서 **이 연결의 hello 설정 변경**합니다. (창의 hello 크기에 따라 할 수 있습니다 tooclick hello 이중 오른쪽 화살표 toosee이이 명령).
7. **인터넷 프로토콜 버전 4(TCP/IPv4)**를 선택하고 **속성**을 클릭합니다.
8. 선택 **다음 DNS 서버 주소를 사용 하 여 hello** 지정 **10.10.2.4** 에 **기본 설정 DNS 서버**합니다.
9. hello **10.10.2.4** 주소는 Azure 가상 네트워크의 hello 10.10.2.0/24 서브넷의 할당 된 tooa 가상 컴퓨터는 hello 주소입니다. 가상 컴퓨터는 **ContosoDC**입니다. tooverify **ContosoDC**의 IP 주소를 사용 하 여 **nslookup contosodc** hello 스크린 샷 다음 그림과 같이 hello 명령 프롬프트 창에서.
   
    ![도메인 컨트롤러에 대 한 NSLOOKUP toofind IP 주소를 사용 합니다.](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664954.jpg)
10. 클릭 **확인** > **닫기** toocommit hello 변경 합니다. Hello 가상 컴퓨터를 너무 가입 이제 수**corp.contoso.com**합니다.
11. Hello에 다시 **로컬 서버** 창의 hello 클릭 **작업 그룹** 링크 합니다.
12. Hello에 **컴퓨터 이름** 섹션에서 클릭 **변경**합니다.
13. 선택 hello **도메인** 확인란, 형식 **corp.contoso.com** hello 텍스트 상자와 클릭 **확인**합니다.
14. Hello에 **Windows 보안** 대화 상자를 hello 기본 도메인 관리자 계정에 대 한 hello 자격 증명 지정 (**CORP\AzureAdmin**) 및 hello 암호 (**Contoso! 000**).
15. Hello "시작 toohello corp.contoso.com 도메인" 메시지가 나타나면 클릭 **확인**합니다.
16. 클릭 **닫기** > **지금 다시 시작** hello 대화 상자에서.

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-virtual-machine"></a>각 가상 컴퓨터에서 관리자 권한으로 hello Corp\Install 사용자 추가
1. Hello 가상 컴퓨터를 다시 시작 될 때까지 기다린 다음 열기 hello RDP 다시 toosign toohello 가상 컴퓨터에서 사용 하 여 파일 hello **BUILTIN\AzureAdmin** 계정.
2. **서버 관리자**에서 **도구** > **컴퓨터 관리**를 클릭합니다.
   
    ![컴퓨터 관리](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784630.png)
3. Hello에 **컴퓨터 관리** 대화 상자에서 **로컬 사용자 및 그룹**, 클릭 하 고 **그룹**합니다.
4. Hello를 두 번 클릭 **관리자** 그룹입니다.
5. Hello에 **Administrators 속성** 대화 상자를 클릭 hello **추가** 단추입니다.
6. Hello 사용자 입력 **CORP\Install**, 클릭 하 고 **확인**합니다. Hello를 사용 하 여 자격 증명에 대 한 대화 상자가 나타나면 **AzureAdmin** hello로 계정 **Contoso! 000** 암호입니다.
7. 클릭 **확인** tooclose hello **관리자 속성** 대화 상자.

### <a name="add-hello-failover-clustering-feature-tooeach-virtual-machine"></a>Hello 장애 조치 클러스터링 기능 tooeach 가상 컴퓨터 추가
1. Hello에 **서버 관리자** 대시보드를 클릭 하 여 **역할 및 기능 추가**합니다.
2. Hello에 **추가 역할 및 기능 마법사**, 클릭 **다음** toohello에 도달할 때까지 **기능** 페이지.
3. **장애 조치 클러스터링**을 선택합니다. 메시지가 표시되면 다른 종속 기능을 추가합니다.
   
    ![장애 조치 클러스터링 기능은 toovirtual 컴퓨터 추가](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784631.png)
4. 클릭 **다음**, 클릭 하 고 **설치** hello에 **확인** 페이지.
5. Hello 때 **장애 조치 클러스터링** 기능 설치가 완료 되 면 클릭 **닫기**합니다.
6. 로그 아웃 hello 가상 컴퓨터.
7. Hello 세 서버 모두에 대 한이 섹션의 단계를 반복: **ContosoWSFCNode**, **ContosoSQL1**, 및 **ContosoSQL2**합니다.

실행 되 고 SQL Server 가상 컴퓨터를 프로비저닝할 이제 hello 있지만 각각에 SQL Server에 대 한 hello 기본 옵션이 있습니다.

## <a name="create-hello-failover-cluster"></a>Hello 장애 조치 클러스터 만들기
이 섹션에서는 나중에 만드는 hello 가용성 그룹을 호스팅할 hello 장애 조치 클러스터를 만듭니다. 지금까지 hello tooeach hello 장애 조치 클러스터에 사용할 수 있는 세 hello 가상 컴퓨터의 다음 수행 해야 합니다.

* Azure의 hello 완벽 하 게 프로 비전 된 가상 컴퓨터
* Hello 가상 컴퓨터 toohello 도메인에 가입
* 추가 **CORP\Install** toohello 로컬 관리자 그룹
* 추가 된 hello 장애 조치 클러스터링 기능

이 모든 작업은 toohello 장애 조치 클러스터 연결 하기 전에 각 가상 컴퓨터에 필수 구성 요소입니다.

또한 hello Azure 가상 네트워크는 작동 하지 않는 hello에 동일한 방식으로 온-프레미스 네트워크입니다. Toocreate hello 클러스터 순서에 따라 hello에 필요 합니다.

1. 하나의 노드에 단일 노드 클러스터를 만듭니다(**ContosoSQL1**).
2. Hello 클러스터 IP 주소 tooan 수정 사용 되지 않는 IP 주소 (**10.10.2.101**).
3. Hello 클러스터 이름을 온라인 상태로 전환 합니다.
4. 추가 hello 다른 노드 (**ContosoSQL2** 및 **ContosoWSFCNode**).

완벽 하 게 hello 클러스터를 구성 하는 단계 toocomplete hello 작업을 수행 하는 hello를 사용 합니다.

1. 에 대 한 RDP 파일 열기 hello **ContosoSQL1**, hello 도메인 계정을 사용 하 여 로그인 **CORP\Install**합니다.
2. Hello에 **서버 관리자** 대시보드를 클릭 하 여 **도구** > **장애 조치 클러스터 관리자**합니다.
3. Hello 왼쪽된 창에서 마우스 오른쪽 단추로 클릭 **장애 조치 클러스터 관리자**, 클릭 하 고 **클러스터 만들기**hello 스크린 샷 뒤에 나타난 것 처럼 합니다.
   
    ![클러스터 만들기](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784632.png)
4. 클러스터 만들기 마법사를 hello를 hello 페이지를 단계별로 실행 하 고 다음 표에 hello의 hello 설정을 사용 하 여 1 노드 클러스터를 만듭니다.
   
   | Page | 설정 |
   | --- | --- |
   | 시작하기 전에 |기본값 사용 |
   | 서버 선택 |**서버 이름 입력**에 **ContosoSQL1**을 입력하고 **추가**를 클릭합니다. |
   | 유효성 검사 경고 |선택 **아니요.가이 클러스터에 대 한 Microsoft의 지원이 필요 하지 않으며 따라서 toorun hello 유효성 검사를 원하지 않는 I를 테스트 합니다. 다음을 클릭 하면 hello 클러스터 만들기를 계속**합니다. |
   | 클러스터 관리 hello에 대 한 액세스 지점 |**클러스터 이름**에 **Cluster1**을 입력합니다. |
   | 다음 |저장소 공간을 사용하지 않는 경우 기본값을 사용합니다. Hello 경고를 다음이 표를 참조 하십시오. |
   
   > [!WARNING]
   > 사용 중인 경우 [저장소 공간](https://technet.microsoft.com/library/hh831739), 여러 디스크를 저장소 풀으로 그룹화 하, hello를 지워야 **모든 적합 한 저장소 toohello 클러스터 추가** hello 확인란 **확인** 페이지. 이 옵션의 선택을 취소 하지 않으면 hello 프로세스를 클러스터링 하는 동안 hello 가상 디스크가 분리 됩니다. 결과적으로, 되었으므로 또한 나타나지 디스크 관리자 또는 탐색기 hello 저장소 공간 hello 클러스터에서 제거 되 고 PowerShell을 사용 하 여 다시 연결할 때까지 합니다.
   > 
   > 
5. Hello 왼쪽된 창에서 **장애 조치 클러스터 관리자**, 클릭 하 고 **Cluster1.corp.contoso.com**합니다.
6. Hello 가운데 창에서 toohello 아래로 스크롤하여 **클러스터 코어 리소스** 섹션을 확장 hello **이름: Clutser1** 세부 정보입니다. 두 hello 표시 되어야 **이름** 및 hello **IP 주소** hello의 리소스 **실패** 상태입니다. hello IP 주소 리소스 상태로 만들 수 없습니다 온라인 hello 클러스터 할당 된 hello hello 컴퓨터 자체와 같은 IP 주소는 중복 된 주소입니다.
7. 마우스 오른쪽 단추로 클릭 hello 실패 **IP 주소** 리소스 및 클릭 **속성**합니다.
   
    ![클러스터 속성](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784633.png)
8. 선택 **고정 IP 주소**, 지정 **10.10.2.101** hello에 **주소** 텍스트 상자 및 클릭 **확인**합니다.
9. Hello에 **클러스터 코어 리소스** 섹션에서 마우스 오른쪽 단추로 클릭 **이름: Cluster1**, 클릭 하 고 **온라인 상태로 만들기**합니다. 두 리소스가 모두 온라인 상태로 전환될 때까지 기다립니다. Hello 클러스터 이름 리소스가 온라인 상태가 되 면 새 Active Directory 컴퓨터 계정으로 hello DC 서버가 업데이트 됩니다. 이 Active Directory 계정을 사용 toorun hello 가용성 나중에 클러스터 된 서비스를 그룹화 합니다.
10. Hello 남은 toohello 클러스터 노드를 추가 합니다. Hello 브라우저 트리에서 마우스 오른쪽 단추로 **Cluster1.corp.contoso.com**, 클릭 하 고 **노드 추가**hello 스크린 샷 뒤에 나타난 것 처럼 합니다.
    
     ![Toohello 클러스터 노드 추가](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784634.png)
11. Hello에 **노드 추가 마법사**, 클릭 **다음** hello에 **서버 선택** 페이지에서 추가 **ContosoSQL2** 및 **ContosoWSFCNode**  toohello 목록에 hello 서버 이름을 입력 하 여 **서버 이름을 입력** 클릭 한 다음 **추가**합니다. 완료하면 **다음**을 클릭합니다.
12. Hello에 **유효성 검사 경고** 페이지 **아니요**프로덕션 시나리오에 hello 유효성 검사 테스트를 수행 해야 하지만, 합니다. 그런 후 **다음**을 클릭합니다.
13. Hello에 **확인** 페이지 **다음** tooadd hello 노드.
    
    > [!WARNING]
    > 사용 중인 경우 [저장소 공간](https://technet.microsoft.com/library/hh831739), 여러 디스크를 저장소 풀으로 그룹화 하, hello를 지워야 **모든 적합 한 저장소 toohello 클러스터 추가** 확인란 합니다. 이 옵션의 선택을 취소 하지 않으면 hello 프로세스를 클러스터링 하는 동안 hello 가상 디스크가 분리 됩니다. 결과적으로, 것도 표시 되지 디스크 관리자 또는 탐색기 hello 저장소 공간을 클러스터에서 제거 될 때까지 않으며 PowerShell을 사용 하 여 다시 연결 합니다.
    > 
    > 
14. Hello 노드 toohello 클러스터에 추가 된 후 클릭 **마침**합니다. 장애 조치 클러스터 관리자 이제 클러스터 노드 3 개 있으며 hello로 나열 표시 **노드** 컨테이너입니다.
15. Hello 원격 데스크톱 세션에서 로그인 합니다.

## <a name="prepare-hello-sql-server-instances-for-availability-groups"></a>가용성 그룹에 대 한 hello SQL Server 인스턴스 준비
이 섹션에서는 작업 둘 다에 따라 hello **ContosoSQL1** 및 **contosoSQL2**:

* 에 대 한 로그인을 추가 **NT AUTHORITY\System** 필요한 권한을 부여 toohello 기본 SQL Server 인스턴스를 설정 합니다.
* 추가 **CORP\Install** sysadmin 역할 toohello 기본 SQL Server 인스턴스로.
* SQL Server의 원격 액세스에 대 한 hello 방화벽을 엽니다.
* 가용성 그룹 기능에 항상 hello를 사용 하도록 설정 합니다.
* Hello SQL Server 서비스 계정에도 변경**CORP\SQLSvc1** 및 **CORP\SQLSvc2**각각.

이 작업은 순서와 관계없이 수행할 수 있습니다. 그럼에도 불구 하 고 단계를 수행 하는 hello 대로 진행 됩니다 순서로 합니다. 모두에 대 한 hello 단계에 따라 **ContosoSQL1** 및 **ContosoSQL2**:

1. Hello hello 가상 컴퓨터에 대 한 원격 데스크톱 세션에서 등록 하지 않은 않으면 지금 연결 합니다.
2. 열기 hello RDP 파일을 **ContosoSQL1** 및 **ContosoSQL2**로 로그인 **BUILTIN\AzureAdmin**합니다.
3. 추가 **NT AUTHORITY\System** toohello SQL Server 로그인 필요한 권한을 부여 합니다. **SQL Server Management Studio**를 엽니다.
4. 클릭 **연결** tooconnect toohello 기본 SQL Server 인스턴스.
5. **개체 탐색기**에서 **보안**을 확장한 다음 **로그인**을 확장합니다.
6. 마우스 오른쪽 단추로 클릭 hello **NT AUTHORITY\System** 로그인 및 클릭 **속성**합니다.
7. Hello에 **보안 개체** hello 로컬 서버에 대 한 페이지 **Grant** 에 대 한 다음, 권한을 hello 및 클릭 **확인**합니다.
   
   * 가용성 그룹 변경
   * SQL 연결
   * 서버 상태 보기
8. 추가 **CORP\Install** 로 **sysadmin** 역할 toohello 기본 SQL Server 인스턴스. **개체 탐색기**에서 **로그인**을 마우스 오른쪽 단추로 클릭하고 **새 로그인**을 클릭합니다.
9. **로그인 이름**에 **CORP\Install**을 입력합니다.
10. Hello에 **서버 역할** 페이지에서 **sysadmin**, 클릭 하 고 **확인**합니다. Hello 로그인을 만든 후 확장 하 여 확인할 수 있습니다 **로그인** 에 **개체 탐색기**합니다.
11. hello에 SQL Server에 대 한 방화벽 규칙 toocreate **시작** 화면, 열린 **고급 보안이 포함 된 Windows 방화벽**합니다.
12. Hello 왼쪽된 창에서 선택 **인바운드 규칙**합니다. Hello 오른쪽 창에서 클릭 **새 규칙**합니다.
13. Hello에 **규칙 유형** 페이지 **프로그램** > **다음**합니다.
14. Hello에 **프로그램** 페이지에서 **다음 프로그램 경로**, 형식 **%ProgramFiles%\Microsoft SQL Server\MSSQL12 합니다. MSSQLSERVER\MSSQL\Binn\sqlservr.exe** hello 텍스트 상자와 클릭 **다음**합니다. Hello SQL Server 디렉터리는 경우 이러한 지침을 따라 SQL Server 2012를 사용 하 여, **MSSQL11. MSSQLSERVER**합니다.
15. Hello에 **동작** 페이지에서 유지 **hello 연결 허용** 을 선택한 다음 클릭 **다음**합니다.
16. Hello에 **프로필** 페이지 hello 기본 설정을 적용 하 고 클릭 **다음**합니다.
17. Hello에 **이름** 페이지에서 같이 규칙 이름을 지정 **SQL Server (프로그램 규칙)**, hello에 **이름** 텍스트 상자의 클릭 **마침**합니다.
18. tooenable hello **Always On 가용성 그룹** hello에 기능을 **시작** 화면, 열린 **SQL Server 구성 관리자**합니다.
19. Hello 브라우저 트리에서 클릭 **SQL Server 서비스**를 마우스 오른쪽 단추로 클릭 hello **SQL Server (MSSQLSERVER)** 서비스를 마우스 클릭 **속성**합니다.
20. Hello 클릭 **Always On 고가용성** 탭에서 **Always On 가용성 그룹 사용**에 나타난 것 처럼 스크린 샷, 다음 hello 및 클릭 **적용**합니다. 클릭 **확인** hello 대화 상자와 hello를 닫지 마십시오 **속성** 아직 대화 상자. Hello 서비스 계정을 변경한 후에 hello SQL Server 서비스를 다시 시작 됩니다.
    
     ![Always On 가용성 그룹 사용](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665520.gif)
21. SQL Server 서비스 계정 toochange hello 클릭 hello **로그온** 탭에서 입력 **CORP\SQLSvc1** (에 대 한 **ContosoSQL1**) 또는 **CORP\SQLSvc2** ( 에 대 한 **ContosoSQL2**)에서 **계정 이름**를 입력 하 고 hello 암호를 확인 하 고 클릭 **확인**합니다.
22. Hello 대화 상자가 열리면 클릭 **예** toorestart hello SQL Server 서비스입니다. Hello SQL Server 서비스를 다시 시작 되 면 hello에서 수행한 변경 **속성** 대화 상자에 적용 됩니다.
23. 로그 아웃 hello 가상 컴퓨터.

## <a name="create-hello-availability-group"></a>Hello 가용성 그룹 만들기
준비 tooconfigure 가용성 그룹입니다. 다음은 수행할 사항을 간략히 설명합니다.

* **ContosoSQL1**에 새 데이터베이스(**MyDB1**)를 만듭니다.
* 전체 백업과 hello 데이터베이스의 트랜잭션 로그 백업을 모두를 수행 합니다.
* Hello 전체를 복원 하 고 로그 백업을 너무**ContosoSQL2** hello로 **NORECOVERY** 옵션입니다.
* Hello 가용성 그룹 만들기 (**AG1**) 읽기 가능한 보조 복제본, 동기 커밋 및 자동 장애 조치와 합니다.

### <a name="create-hello-mydb1-database-on-contososql1"></a>ContosoSQL1에 hello MyDB1 데이터베이스 만들기
1. 하는 경우 등록 하지 않은 이미 hello에 대 한 원격 데스크톱 세션에서 **ContosoSQL1** 및 **ContosoSQL2**, 지금 합니다.
2. 에 대 한 RDP 파일 열기 hello **ContosoSQL1**로 로그인 **CORP\Install**합니다.
3. **파일 탐색기**에서 **C:\\** 아래에 **backup**이라는 디렉터리를 만듭니다. 이 디렉터리 tooback 사용 및 데이터베이스를 복원 합니다.
4. Hello 새 디렉터리를 마우스 오른쪽 단추로 클릭, 너무 가리킨**공유할**, 클릭 하 고 **특정 사용자**hello 스크린 샷 뒤에 나타난 것 처럼 합니다.
   
    ![백업 폴더 만들기](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665521.gif)
5. 추가 **CORP\SQLSvc1**, 다음 hello 제공 **읽기/쓰기** 권한. 추가 **CORP\SQLSvc2**, 다음 hello 제공 **읽기** 권한에 표시 된 대로 스크린 샷, 다음 hello 및 클릭 **공유**합니다. Hello 파일 공유 프로세스가 완료 되 면 클릭 **수행**합니다.
   
    ![백업 폴더에 대한 권한 부여](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665522.gif)
6. hello에서 toocreate hello 데이터베이스 **시작** 메뉴를 열고 **SQL Server Management Studio**, 클릭 하 고 **연결** tooconnect toohello 기본 SQL Server 인스턴스.
7. **개체 탐색기**에서 **데이터베이스**를 마우스 오른쪽 단추로 클릭한 다음 **새 데이터베이스**를 클릭합니다.
8. **데이터베이스 이름**에 **MyDB1**을 입력하고 **확인**을 클릭합니다.

### <a name="make-a-full-backup-of-mydb1-and-restore-it-on-contososql2"></a>MyDB1의 전체 백업 수행 및 ContosoSQL2에 복원
1. hello의 전체 백업을 데이터베이스 toomake **개체 탐색기**, 확장 **데이터베이스**를 마우스 오른쪽 단추로 클릭 **MyDB1**, 너무 가리킨**작업**, 및 클릭 **백업**합니다.
2. Hello에 **소스** 섹션에서 유지 **백업 유형** 도**전체**합니다. Hello에 **대상** 섹션에서 클릭 **제거** hello 백업 파일에 대 한 tooremove hello 기본 파일 경로입니다.
3. Hello에 **대상** 섹션에서 클릭 **추가**합니다.
4. Hello에 **파일 이름** 텍스트 상자에서  **\\ContosoSQL1\backup\MyDB1.bak**, 클릭 **확인**, 클릭 하 고 **확인** 다시 hello 데이터베이스를 tooback 합니다. Hello 백업 작업이 완료 되 면 클릭 **확인** 다시 tooclose hello 대화 상자.
5. 트랜잭션 toomake hello 데이터베이스의 백업을 로그인 **개체 탐색기**, 확장 **데이터베이스**를 마우스 오른쪽 단추로 클릭 **MyDB1**, 너무 가리킨**작업**, 클릭 하 고 **백업**합니다.
6. **백업 유형**에서 **트랜잭션 로그**를 선택합니다. Hello 유지 **대상** 이전에 지정 된 경로 집합 toohello 파일을 누르고 **확인**합니다. Hello 백업 작업이 완료 되 면 클릭 **확인** 다시 합니다.
7. 전체 toorestore hello 및 트랜잭션 로그 백업을 **ContosoSQL2**개방형 hello RDP 파일에 대 한 **ContosoSQL2**로 로그인 **CORP\Install**합니다. Hello에 대 한 원격 데스크톱 세션을 두고 **ContosoSQL1** 엽니다.
8. Hello에서 **시작** 메뉴를 열고 **SQL Server Management Studio**, 클릭 하 고 **연결** tooconnect toohello 기본 SQL Server 인스턴스.
9. **개체 탐색기**에서 **데이터베이스**를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 복원**을 클릭합니다.
10. Hello에 **소스** 섹션에서 **장치**, hello 줄임표를 클릭 하 고 **...** 단추를 선택합니다.
11. **백업 장치 선택**에서 **추가**를 클릭합니다.
12. **백업 파일 위치**에서 **\\ContosoSQL1\backup**을 입력하고, **새로 고침**을 클릭하고, **MyDB1.bak**를 선택하고, **확인**을 클릭하고 나서, **확인**을 다시 클릭합니다. Hello 전체 백업 및 로그 백업 hello에 hello 이제 표시 **toorestore 사용할 백업 세트** 창.
13. Toohello 이동 **옵션** 페이지에서 **RESTORE WITH NORECOVERY** 에 **복구 상태**, 클릭 하 고 **확인** toorestore hello 데이터베이스입니다. Hello 후 복원 작업 완료, 클릭 **확인**합니다.

### <a name="create-hello-availability-group"></a>Hello 가용성 그룹 만들기
1. 이동에 대 한 원격 데스크톱 세션 toohello 다시 **ContosoSQL1**합니다. **개체 탐색기** SQL Server Management Studio에서 마우스 오른쪽 단추로 클릭 **Always On 고가용성**, 클릭 하 고 **새 가용성 그룹 마법사**hello에 나타난 것 처럼 다음 스크린 샷
   
    ![새 가용성 그룹 마법사 시작](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665523.gif)
2. Hello에 **소개** 페이지 **다음**합니다. Hello에 **가용성 그룹 이름 지정** 페이지에서 입력 **AG1** 에 **가용성 그룹 이름**, 클릭 **다음** 다시 합니다.
   
    ![새 가용성 그룹 마법사, 가용성 그룹 이름 지정](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665524.gif)
3. Hello에 **데이터베이스 선택** 페이지 **MyDB1**, 클릭 하 고 **다음**합니다. hello 의도 된 주 복제본에서 최소한 하나의 전체 백업을 수행 했으므로 hello 데이터베이스가 가용성 그룹에 대 한 hello 필수 구성 요소를 충족 합니다.
   
    ![새 가용성 그룹 마법사, 데이터베이스 선택](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665525.gif)
4. hello에 **복제본 지정** 페이지 **Add Replica**합니다.
   
    ![새 가용성 그룹 마법사, 복제본 지정](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665526.gif)
5. Hello에 **tooServer 연결** 대화 상자에서 **ContosoSQL2** 에 **서버 이름**, 클릭 하 고 **연결**합니다.
   
    ![새 가용성 그룹 마법사, Connect tooserver](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665527.gif)
6. Hello에 다시 **복제본 지정** 페이지, 이제 **ContosoSQL2** 에 나열 된 **사용 가능한 복제본**합니다. 다음 스크린 샷에서 hello와 같이 hello 복제본을 구성 합니다. 작업을 마쳤으면 **다음**을 클릭합니다.
   
    ![새 가용성 그룹 마법사, 복제본 지정(전체)](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665528.gif)
7. Hello에 **초기 데이터 동기화 선택** 페이지 **조인만**, 클릭 하 고 **다음**합니다. 이미 데이터 동기화 수동으로 수행한 hello 전체 및 트랜잭션 백업을에서 정의가 **ContosoSQL1** 에서 복원 하 고 **ContosoSQL2**합니다. Tooperform hello 하지 데이터베이스에 대 한 백업 및 복원 작업을 선택할 수 있으며 대신 선택 **전체** toolet hello 새 가용성 그룹 마법사는 사용자에 대 한 데이터 동기화를 수행 합니다. 그러나 일부 기업에서 사용하는 대형 데이터베이스의 경우에는 이 옵션을 사용하지 않는 것이 좋습니다.
   
    ![새 가용성 그룹 마법사, 초기 데이터 동기화 선택.](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665529.gif)
8. Hello에 **유효성 검사** 페이지 **다음**합니다. 이 페이지에는 비슷한 toohello 스크린 샷 다음 같아야 합니다. 가용성 그룹 수신기를 구성 하지 않았기 때문에는 hello 수신기 구성에 대 한 경고입니다. 이 자습서에서는 수신기를 구성하지 않으므로 이 경고를 무시해도 됩니다. 이 자습서, 참조를 완료 한 후 tooconfigure hello 수신기 [Azure에서 Always On 가용성 그룹에 대 한 ILB 수신기 구성](../classic/ps-sql-int-listener.md)합니다.
   
    ![새 가용성 그룹 마법사, 유효성 검사](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665530.gif)
9. Hello에 **요약** 페이지 **마침**, 고 hello 마법사 hello 새 가용성 그룹을 구성 하는 동안 기다립니다. Hello에 **진행률** 페이지에서 클릭할 수 있는 **자세한 내용을 보려면** tooview hello 진행 상황을 설명 합니다. Hello 마법사를 완료 한 후 검사할 hello **결과** 페이지 tooverify 있는 hello 가용성 그룹 성공적으로 만들어지면 hello 다음 스크린 샷에서 같이 클릭 한 다음 **닫기** tooexit hello 마법사입니다.
   
    ![새 가용성 그룹 마법사, 결과](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665531.gif)
10. **개체 탐색기**에서 **Always On 고가용성**을 확장하고 **가용성 그룹**을 확장합니다. 이제이 컨테이너에서 hello 새 가용성 그룹을 표시 됩니다. **AG1(기본)**을 마우스 오른쪽 단추로 클릭하고 **대시보드 표시**를 클릭합니다.
    
     ![가용성 그룹 대시보드 표시](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665532.gif)
11. 프로그램 **Always On 대시보드** 모양 비슷한 toohello 하나 hello에 스크린 샷을 수행 해야 합니다. Hello 복제본, hello 장애 조치 모드의 각 복제본 및 hello 동기화 상태를 볼 수 있습니다.
    
     ![가용성 그룹 대시보드](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665533.gif)
12. 너무 반환**서버 관리자**, 클릭 **도구**를 연 다음 **장애 조치 클러스터 관리자**합니다.
13. **Cluster1.corp.contoso.com**과 **서비스 및 응용 프로그램**을 차례로 확장합니다. 선택 **역할** 해당 hello 확인 **AG1** 가용성 그룹 역할이 생성 되었음. AG1 없는지 데이터베이스 클라이언트가 toohello 가용성 그룹에 연결할 수는 IP 주소는 수신기를 구성 하지 않은 때문에 note 합니다. 읽기 / 쓰기 작업에 대 한 toohello 주 노드 및 읽기 전용 쿼리에 대 한 hello 보조 노드에 직접 연결 합니다.
    
     ![장애 조치(Failover) 클러스터 관리자에서 AG](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665534.gif)

> [!WARNING]
> 가용성 그룹 장애 조치 클러스터 관리자 hello에서 hello 통해 toofail를 시도 하지 않습니다. 모든 장애 조치(failover) 작업은 SQL Server Management Studio의 **Always On 대시보드**에서 수행해야 합니다. 자세한 내용은 참조 [사용에 대 한 제한에는 가용성 그룹 장애 조치 클러스터 관리자 hello](https://msdn.microsoft.com/library/ff929171.aspx)합니다.
> 
> 

## <a name="next-steps"></a>다음 단계
이제 Azure에서 가용성 그룹을 만들어 SQL Server Always On을 성공적으로 구현했습니다. 이 가용성 그룹에 대 한 수신기 tooconfigure 참조 [Azure에서 Always On 가용성 그룹에 대 한 ILB 수신기 구성](../classic/ps-sql-int-listener.md)합니다.

Azure에서 SQL Server를 사용하는 방법에 대한 기타 정보는 [Azure 가상 컴퓨터의 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)를 참조하세요.

