---
title: "Azure Site Recovery를 사용 하 여 다중 계층 SharePoint 응용 프로그램 aaaReplicate | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooreplicate Azure 사이트 복구 기능을 사용 하 여 다중 계층 SharePoint 응용 프로그램입니다."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sutalasi
ms.openlocfilehash: d856034ac2a3c95b0c1f0cf85e62c4e7a5a3210f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-sharepoint-application-for-disaster-recovery-using-azure-site-recovery"></a>Azure Site Recovery를 사용하여 재해 복구를 위해 다중 계층 SharePoint 응용 프로그램 복제 | Microsoft Docs

이 문서에 자세히 설명 방법을 사용 하 여 SharePoint 응용 프로그램 tooprotect [Azure Site Recovery](site-recovery-overview.md)합니다.


## <a name="overview"></a>개요

Microsoft SharePoint는 그룹 또는 부서가 정보를 구성, 공동 작업 및 공유하도록 도울 수 있는 강력한 응용 프로그램입니다. SharePoint는 인트라넷 포털, 문서 및 파일 관리, 공동 작업, 소셜 네트워크, 엑스트라넷, 웹 사이트, 엔터프라이즈 검색 및 비즈니스 인텔리전스를 제공합니다. 또한 시스템 통합, 프로세스 통합 및 워크플로 자동화 기능도 갖추고 있습니다. 일반적으로 조직 계층 1 응용 프로그램 중요 한 toodowntime 및 데이터 손실으로 간주합니다.

오늘날, Microsoft SharePoint는 기본적으로 재해 복구 기능을 제공하지 않습니다. Hello 형식 및 소수 자릿수가 재해에 관계 없이 복구 hello 팜을 복구할 수 있는 대기 데이터 센터의 hello 사용을 해야 합니다. 대기 중인 데이터 센터는 hello 기본 데이터 센터에서 hello 가동 중단에서 충분 한 로컬 시스템 및 백업을 복구할 수 없습니다 시나리오에 필요 합니다.

좋은 재해 복구 솔루션 SharePoint와 같은 복잡 한 응용 프로그램 아키텍처 hello 주위 복구 계획의 모델링을 허용 해야 합니다. 또한 hello 기능 사용자 지정 tooadd 단계 toohandle 응용 프로그램 간의 매핑을 다양 한 계층 따라서 재해의 hello 이벤트에서 더 낮은 RTO에 한 번 클릭으로 장애 조치를 제공 있어야 합니다.

이 문서에 자세히 설명 방법을 사용 하 여 SharePoint 응용 프로그램 tooprotect [Azure Site Recovery](site-recovery-overview.md)합니다. 이 문서에서는 복제 하는 3 계층 SharePoint 응용 프로그램 tooAzure, 재해 복구 훈련과 수행 하는 방법은 및 장애 조치 hello 응용 프로그램 tooAzure 하는 방법에 대 한 모범 사례를 설명 합니다.

다중 계층 응용 프로그램 tooAzure 복구에 대 한 비디오 아래 hello를 볼 수 있습니다.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/Disaster-Recovery-of-load-balanced-multi-tier-applications-using-Azure-Site-Recovery/player]


## <a name="prerequisites"></a>필수 조건

시작 하기 전에 hello 다음 알고 있어야 합니다.

1. [가상 컴퓨터 tooAzure 복제](site-recovery-vmware-to-azure.md)
2. 어떻게 너무[복구 네트워크 디자인](site-recovery-network-design.md)
3. [테스트 장애 조치 tooAzure 수행](site-recovery-test-failover-to-azure.md)
4. [장애 조치 tooAzure 수행](site-recovery-failover.md)
5. 어떻게 너무[도메인 컨트롤러 복제](site-recovery-active-directory.md)
6. 어떻게 너무[SQL Server 복제](site-recovery-sql.md)

## <a name="sharepoint-architecture"></a>SharePoint 아키텍처

계층 토폴로지 및 서버 역할 tooimplement 특정 목표 및 목적을 충족 하는 팜 디자인을 사용 하 여 하나 이상의 서버에 SharePoint은 배포할 수 있습니다. 수 많은 동시 사용자 및 콘텐츠 항목을 지원하는 일반적인 큰 규모의 많은 처리량을 요구하는 SharePoint 서버 팜은 확장성 전략의 일부로 서비스 그룹화를 사용합니다. 이러한 서비스를 함께 그룹화 하 고 hello 서버 그룹으로 다음 확장 전용된 서버에 서비스를 실행 하는 것이 방법은 수 있습니다. hello 다음 토폴로지를 보여 줍니다 hello 서비스 및 서버 3 계층 SharePoint 서버 팜에 대 한 그룹화 합니다. 에 대 한 자세한 지침은 다른 SharePoint 토폴로지 tooSharePoint 설명서와 제품 라인 아키텍처를 참조 하십시오. SharePoint 2013 배포에 대한 자세한 내용은 [이 문서](https://technet.microsoft.com/en-us/library/cc303422.aspx)에서 확인할 수 있습니다.



![배포 패턴 1](./media/site-recovery-sharepoint/sharepointarch.png)


## <a name="site-recovery-support"></a>Site Recovery 지원

이 문서를 작성하기 위해 Windows Server 2012 R2 Enterprise가 있는 VMware 가상 컴퓨터가 사용되었습니다. SharePoint 2013 Enterprise Edition 및 SQL server 2014 Enterprise Edition이 사용되었습니다. 사이트 복구 복제 응용 프로그램을 알 수 없는 그대로 hello 권장 사항을 여기에 제공 된 예상된 toohold에도 다음과 같은 시나리오에 대 한 합니다.

### <a name="source-and-target"></a>원본 및 대상

**시나리오** | **tooa 보조 사이트** | **tooAzure**
--- | --- | ---
**Hyper-V** | 예 | 예
**VMware** | 예 | 예
**물리적 서버** | 예 | 예

### <a name="sharepoint-versions"></a>SharePoint 버전
SharePoint server 버전에 따라 hello 사용할 수 있습니다.

* SharePoint Server 2013 Standard
* SharePoint Server 2013 Enterprise
* SharePoint Server 2016 Standard
* SharePoint Server 2016 Enterprise

### <a name="things-tookeep-in-mind"></a>유의 사항 tookeep

공유 디스크 기반 클러스터 응용 프로그램에서 모든 계층으로 사용 하는 경우는 금지 됩니다 수 toouse 사이트 복구 복제 tooreplicate 해당 가상 컴퓨터 수입니다. Hello 응용 프로그램에서 제공 하는 기본 복제를 사용 하 고 사용 하 여 한 [복구 계획](site-recovery-create-recovery-plans.md) toofailover 모든 계층입니다.

## <a name="replicating-virtual-machines"></a>가상 컴퓨터 복제

에 따라 [이 지침은](site-recovery-vmware-to-azure.md) toostart hello 가상 컴퓨터 tooAzure를 복제 합니다.

* Hello 복제가 완료 되 면 각 계층의 tooeach 가상 컴퓨터를 이동 하 고 동일한 가용성 집합 선택 되었는지 확인 ' 복제 된 항목 > 설정 > 속성 > 계산 및 네트워크 '. 예를 들어 웹 계층에 vm 3 개 있는 경우에 모든 hello 3 개의 Vm은 동일한 Azure의 가용성 집합의 toobe 일부 구성 확인 합니다.

    ![가용성 집합 설정](./media/site-recovery-sharepoint/select-av-set.png)

* Active Directory 및 DNS를 보호에 대 한 지침을 참조 너무[보호 Active Directory 및 DNS](site-recovery-active-directory.md) 문서.

* SQL server에서 실행 하는 데이터베이스 계층을 보호 하는 지침에 대 한 참조 너무[SQL Server 보호](site-recovery-active-directory.md) 문서.

## <a name="networking-configuration"></a>네트워킹 구성

### <a name="network-properties"></a>네트워크 속성

* Hello 응용 프로그램 및 웹 계층 Vm에 대 한 hello Vm 장애 조치 후 연결 된 toohello 적합 한 DR 네트워크 얻을 수 있도록 Azure 포털에서 네트워크 설정을 구성 합니다.

    ![네트워크 선택](./media/site-recovery-sharepoint/select-network.png)


* 고정 IP를 사용 하는 경우 다음 hello에 가상 컴퓨터 tootake hello 원하는 hello IP 지정 **대상 IP** 필드

    ![고정 IP 설정](./media/site-recovery-sharepoint/set-static-ip.png)

### <a name="dns-and-traffic-routing"></a>DNS 및 트래픽 라우팅

인터넷 연결 사이트에 대 한 ['Priority' 형식에 대 한 트래픽 관리자 프로필을 만들](../traffic-manager/traffic-manager-create-profile.md) hello Azure 구독에에서 있습니다. 선택한 다음 방식으로 수행 하는 hello에서 DNS 및 트래픽 관리자 프로필을 구성 합니다.


| **Where** | **원본** | **대상**|
| --- | --- | --- |
| 공용 DNS | SharePoint 사이트에 대한 공용 DNS <br/><br/> 예: sharepoint.contoso.com | 트래픽 관리자 <br/><br/> contososharepoint.trafficmanager.net |
| 온-프레미스 DNS | sharepointonprem.contoso.com | Hello 온-프레미스 팜에서 공용 IP |


Hello 트래픽 관리자 프로필에서에서 [hello 기본 및 복구 끝점을 만들](../traffic-manager/traffic-manager-configure-priority-routing-method.md)합니다. 온-프레미스 끝점 및 Azure 끝점에 대 한 공용 IP에 대 한 외부 끝점 hello를 사용 합니다. Hello 우선 순위가 더 높은 tooon 온-프레미스 끝점을 설정 되어 있는지 확인 합니다.

트래픽 관리자 tooautomatically 되려면에서 hello SharePoint 웹 계층의 특정 포트 (예: 800)에서 테스트 페이지 호스트 가용성 사후 장애 조치를 검색 합니다. 이는 SharePoint 사이트 중에서 익명 인증을 사용하도록 설정할 수 없을 경우에 해결 방법입니다.

[Hello 트래픽 관리자 프로필을 구성](../traffic-manager/traffic-manager-configure-priority-routing-method.md) 설정 아래 hello로 합니다.

* 라우팅 방법 - ‘우선 순위’
* DNS 시간 toolive (TTL)-' 30 초'
* 끝점 모니터 설정 - 익명 인증을 사용하도록 설정할 수 있는 경우 특정 웹 사이트 끝점을 지정할 수 있습니다. 또는 특정 포트(예: 800)에서 테스트 페이지를 사용할 수 있습니다.

## <a name="creating-a-recovery-plan"></a>복구 계획 만들기

복구 계획을 나열 하는 응용 프로그램 일관성을 유지 하는 다중 계층 응용 프로그램, 따라서의 다양 한 계층의 hello 장애 조치 수 있습니다. 다중 계층 웹 응용 프로그램에 대 한 복구 계획을 만드는 동안 hello 아래 단계를 따릅니다. [복구 계획 만들기에 대한 자세한 정보](site-recovery-runbook-automation.md#customize-the-recovery-plan)

### <a name="adding-virtual-machines-toofailover-groups"></a>가상 컴퓨터 toofailover 그룹 추가

1. 추가 hello 응용 프로그램 및 웹 계층 Vm에서 복구 계획을 만듭니다.
2. '사용자 지정' toogroup hello Vm 클릭 합니다. 기본적으로 모든 VM은 ‘그룹 1’에 속합니다.

    ![RP 사용자 지정](./media/site-recovery-sharepoint/rp-groups.png)

3. 다른 그룹 (그룹 2)를 만들고 hello 웹 계층 Vm hello 새 그룹으로 이동 합니다. 앱 계층 VM은 ‘그룹 1’의 일부여야 하며, 웹 계층 VM은 ‘그룹 2’의 일부여야 합니다. 이 응용 프로그램 계층 Vm 부팅 웹 계층 Vm 먼저 옵니다 hello tooensure입니다.


### <a name="adding-scripts-toohello-recovery-plan"></a>Toohello 복구 계획 스크립트 추가

Hello 'tooAzure 배포' 아래 단추를 클릭 하 고 자동화 계정으로 가장 많이 사용 하는 hello Azure 사이트 복구 스크립트를 배포할 수 있습니다. 게시 된 모든 스크립트를 사용 하는 경우에 hello hello 스크립트에 대 한 지침을 따라를 확인 합니다.

[![TooAzure 배포](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

1. 이전 스크립트 too'Group 1' toofailover SQL 가용성 그룹을 추가 합니다. Hello 예제 스크립트에 게시 하는 hello ' ASR SQL FailoverAG' 스크립트를 사용 합니다. Hello 스크립트에 hello 지침에 따라를 하는 데 필요한 hello 변경할 hello 스크립트에 적절 하 게 확인 합니다.

    ![Add-AG-Script-Step-1](./media/site-recovery-sharepoint/add-ag-script-step1.png)

    ![Add-AG-Script-Step-2](./media/site-recovery-sharepoint/add-ag-script-step2.png)

2. 웹 계층 (그룹 2)의 가상 컴퓨터를 통해 실패 hello에 부하 분산 장치는 post 작업 스크립트 tooattach를 추가 합니다. Hello 예제 스크립트에 게시 하는 hello ' ASR AddSingleLoadBalancer' 스크립트를 사용 합니다. Hello 스크립트에 hello 지침에 따라를 하는 데 필요한 hello 변경할 hello 스크립트에 적절 하 게 확인 합니다.

    ![Add-LB-Script-Step-1](./media/site-recovery-sharepoint/add-lb-script-step1.png)

    ![Add-LB-Script-Step-2](./media/site-recovery-sharepoint/add-lb-script-step2.png)

3. Azure에서 수동 단계 tooupdate hello DNS 레코드 toopoint toohello 새 팜에 추가 합니다.

    * 인터넷 연결 사이트의 경우 사후 장애 조치에 DNS 업데이트가 필요하지 않습니다. Hello '네트워킹 지침' 섹션 tooconfigure 트래픽 관리자에서에서 설명 하는 hello 단계를 따릅니다. Hello 이전 섹션에 설명 된 대로 hello 트래픽 관리자 프로필 설정 되어, 경우 스크립트 tooopen 더미 포트 (hello 예제에서는 800) hello Azure VM에 추가 합니다.

    * 내부 웹 사이트에 대 한 수동 단계 tooupdate hello DNS 레코드 toopoint toohello 새 웹 계층 VM의 부하 분산 장치 IP를 추가 합니다.

4. 백업에서 수동 단계 toorestore 검색 응용 프로그램을 추가 하거나 새 검색 서비스를 시작 합니다.

5. 검색 서비스 응용 프로그램을 백업에서 복원하는 것은 아래 단계를 수행합니다.

    * 이 메서드 hello 재해가 발생 하기 전에 hello 검색 서비스 응용 프로그램의 백업을 수행한 hello DR 사이트에서 해당 hello 백업을 사용할 수 없는 되었다고 가정 합니다.
    * (예를 들어, 하루에 한 번씩) hello 백업을 예약 하 고 hello DR 사이트에서 복사 프로시저 tooplace hello 백업을 사용 하 여 쉽게 달성할 수 있습니다. 복사 절차에는 AzCopy(Azure 복사)와 같은 스크립트를 사용한 프로그램 또는 DFSR(분산 파일 서비스 복제)를 설정하는 것이 포함될 수 있습니다.
    * 이제 해당 hello 팜이 실행 하는 SharePoint 중앙 관리에서 '백업 및 복원' hello 찾아서 복원을 선택 합니다. hello 복원 질의 지정한 hello 백업 위치 (tooupdate hello 값을 할 수 있습니다). Toorestore 원하는 hello 검색 서비스 응용 프로그램 백업을 선택 합니다.
    * 검색이 복원됩니다. 복원 hello 있음을 명심 toofind hello에서는 하드 드라이브 문자 할당 toothose 서버 동일한 토폴로지 (동일한 서버 수)와 동일 합니다. 자세한 내용은 [‘SharePoint 2013의 검색 서비스 응용 프로그램 복원’](https://technet.microsoft.com/library/ee748654.aspx) 문서를 참조하세요.


6. 새로운 검색 서비스 응용 프로그램으로 시작은 다음 단계를 수행합니다.

    * 이 메서드는 hello "검색 관리" 데이터베이스의 백업을 hello DR 사이트에서 사용할 수 있는지를 가정 합니다.
    * Hello 다른 검색 서비스 응용 프로그램 데이터베이스는 복제 되지 이후 toobe 다시 생성 해야 합니다. 따라서 toodo tooCentral 관리 이동 하 게 되 고 hello 검색 서비스 응용 프로그램을 삭제 합니다. 모든 서버에 있는 호스트 hello 검색 인덱스 hello 인덱스 파일을 삭제 합니다.
    * Hello 검색 서비스 응용 프로그램 및이 다시 만듭니다 hello 데이터베이스를 다시 만듭니다. Toohave 좋습니다 준비 스크립트를 다시 만듭니다.이 서비스 응용 프로그램 가능한 tooperform 아니므로 hello GUI 통해 모든 작업. 예를 들어 hello 인덱스 드라이브 위치를 설정 하 고 hello 검색 토폴로지 구성만 가능 SharePoint PowerShell cmdlet을 사용 하 여 됩니다. 복원 SPEnterpriseSearchServiceApplication hello Windows PowerShell cmdlet를 사용 하 고 hello 로그 전달 및 복제 한 검색 관리 데이터베이스, Search_Service__DB 지정 키를 누릅니다. 이 cmdlet는 hello 구성 검색, 스키마, 관리 되는 속성, 규칙 및 소스를 제공 하 고 hello 기본 집합이 다른 구성 요소를 만듭니다.
    * Hello 검색 서비스 응용 프로그램은 다시 만들어지지 되 면 각 콘텐츠 원본 toorestore hello 검색 서비스에 대 한 전체 탐색을 시작 해야 합니다. 검색 권장 사항 등 hello 온-프레미스 팜에서 일부 분석 정보가 손실 됩니다.

7. 모든 hello 단계가 완료 되 면 hello 복구 계획을 저장 하 고 hello 최종 복구 계획은 다음과 같습니다.

    ![저장된 RP](./media/site-recovery-sharepoint/saved-rp.png)

## <a name="doing-a-test-failover"></a>테스트 장애 조치 수행
에 따라 [이 지침은](site-recovery-test-failover-to-azure.md) toodo 테스트 장애 조치 합니다.

1.  TooAzure 포털 이동한 다음 복구 서비스 자격 증명 모음을 선택 합니다.
2.  SharePoint 응용 프로그램에 대해 생성 하는 hello 복구 계획을 클릭 합니다.
3.  '테스트 장애 조치'를 클릭합니다.
4.  복구 지점 및 Azure 가상 네트워크 toostart hello 테스트 장애 조치 프로세스를 선택 합니다.
5.  Hello 보조 환경의 되 면 사용자 유효성 검사를 수행할 수 있습니다.
6.  Hello 유효성 검사가 완료 되 면 '정리 테스트 장애 조치' hello 복구 계획에서 클릭할 수 있는 및 hello 테스트 장애 조치 환경이 정리 됩니다.

AD에 대 한 테스트 장애 조치를 수행 하는 작업에 대 한 지침에 대 한 DNS, 너무 참조 및[테스트 AD에 대 한 장애 조치 고려 사항 및 DNS](site-recovery-active-directory.md#test-failover-considerations) 문서.

가용성 그룹에 항상 SQL에 대 한 테스트 장애 조치 작업에 대 한 지침을 참조 너무[SQL Server Always On에 대 한 장애 조치를 수행 하 테스트](site-recovery-sql.md#steps-to-do-a-test-failover) 문서.

## <a name="doing-a-failover"></a>장애 조치 수행
장애 조치(Failover)를 수행할 때 [이 지침](site-recovery-failover.md)을 따릅니다.

1.  TooAzure 포털 이동한 다음 복구 서비스 자격 증명 모음을 선택 합니다.
2.  SharePoint 응용 프로그램에 대해 생성 하는 hello 복구 계획을 클릭 합니다.
3.  '장애 조치'를 클릭합니다.
4.  복구 지점 toostart hello 장애 조치 프로세스를 선택 합니다.

## <a name="next-steps"></a>다음 단계
Site Recovery를 사용하여 [다른 응용 프로그램을 복제](site-recovery-workload.md)하는 것에 대해 자세히 알아볼 수 있습니다.
