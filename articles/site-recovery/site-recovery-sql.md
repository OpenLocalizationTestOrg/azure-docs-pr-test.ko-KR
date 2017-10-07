---
title: "SQL Server 및 Azure 사이트 복구와 aaaReplicate 응용 프로그램 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooreplicate Azure Site Recovery를 사용 하 여 SQL Server 재해 기능에 대 한 SQL Server."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 99755f2cd2f7e924071f1e230ac4a0bda88f0a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-sql-server-using-sql-server-disaster-recovery-and-azure-site-recovery"></a>SQL Server 재해 복구 및 Azure Site Recovery를 사용하여 SQL Server 보호

이 문서에서는 tooprotect hello SQL Server의 SQL Server의 비즈니스 연속성 및 재해 복구 (BCDR) 기술을 함께 사용 하 여 응용 프로그램의 끝을 백업 하는 방법을 설명 하 고 [Azure Site Recovery](site-recovery-overview.md)합니다.

시작하기 전에 장애 조치(failover) 클러스터링, Always On 가용성 그룹, 데이터베이스 미러링 및 로그 전달을 비롯한 SQL Server 재해 복구 기능을 알고 있어야 합니다.


## <a name="sql-server-deployments"></a>SQL Server 배포

다양 한 작업을 기반으로 SQL Server를 사용 하 고 SharePoint, Dynamics, 및 SAP, tooimplement 데이터 서비스와 같은 앱과 통합 될 수 있습니다.  SQL Server는 다양한 방법으로 배포될 수 있습니다.

* **독립 실행형 SQL Server**: SQL Server 및 모든 데이터베이스는 단일 컴퓨터(물리적 또는 가상)에서 호스트됩니다. 가상화된 경우 호스트 클러스터링은 고가용성을 위해 사용됩니다. 게스트 수준의 고가용성은 구현되지 않습니다.
* **SQL Server 장애 조치(Failover) 클러스터링 인스턴스(Always On FCI)**: 공유된 디스크와 함께 인스턴스화된 SQL Server를 실행하는 노드가 2개 이상 Windows 장애 조치 클러스터에 구성됩니다. 노드가 다운 되는 경우 hello 클러스터 tooanother 인스턴스를 통해 SQL Server를 실패할 수 있습니다. 이 설치 프로그램은 일반적으로 사용 되는 tooimplement 고가용성 기본 사이트에 있습니다. 이 배포는 오류 또는 중단이 hello 공유 저장소 계층에서에 대해 보호 하지 않습니다. 공유 디스크는 iSCSI, 파이버 채널 또는 공유 vhdx를 사용하여 구현할 수 있습니다.
* **SQL Always ON 가용성 그룹**: 동기 복제 및 자동 장애 조치(failover)를 사용하여 가용성 그룹에서 구성된 SQL Server 데이터베이스로 공유되지 않은 클러스터에서 2개 이상의 노드를 설정합니다.

 이 문서는 hello tooa 원격 사이트 데이터베이스를 복구 하기 위한 네이티브 SQL 재해 복구 기술에 따라 활용 하 여:

* SQL Always On 가용성 그룹, SQL Server 2012 또는 2014 Enterprise edition에 대 한 재해 복구를 위한 tooprovide 합니다.
* SQL Server Standard 버전(모든 버전) 또는 SQL Server 2008 R2에 대한 높은 보안 모드에서 SQL 데이터베이스 미러링.

## <a name="site-recovery-support"></a>Site Recovery 지원

### <a name="supported-scenarios"></a>지원되는 시나리오
사이트 복구는 hello 표에 요약 된 대로 SQL Server를 보호할 수 있습니다.

**시나리오** | **tooa 보조 사이트** | **tooAzure**
--- | --- | ---
**Hyper-V** | 예 | 예
**VMware** | 예 | 예
**물리적 서버** | 예 | 예

### <a name="supported-sql-server-versions"></a>지원되는 SQL Server 버전
이러한 SQL Server 버전 지원 hello 시나리오에 대 한 지원 됩니다.

* SQL Server 2016 Enterprise 및 Standard
* SQL Server 2014 Enterprise 및 Standard
* SQL Server 2012 Enterprise 및 Standard
* SQL Server 2008 R2 Enterprise 및 Standard

### <a name="supported-sql-server-integration"></a>지원되는 SQL Server 통합

사이트 복구 tooprovide 재해 복구 솔루션 hello 표에 요약 되어 네이티브 SQL Server BCDR 기술과 함께 통합할 수 있습니다.

**기능** | **세부 정보** | **SQL Server** |
--- | --- | ---
**Always On 가용성 그룹** | SQL Server의 여러 독립 실행형 인스턴스는 여러 노드가 있는 장애 조치 클러스터에서 실행됩니다.<br/><br/>SQL Server 인스턴스에서 복사(미러링)할 수 있는 장애 조치 그룹으로 데이터베이스를 그룹화하여 공유 저장소가 필요하지 않습니다.<br/><br/>기본 사이트 및 하나 이상의 보조 사이트 간에 재해 복구를 제공합니다. 동기 복제 및 자동 장애 조치를 사용하여 가용성 그룹에서 구성된 SQL Server 데이터베이스로 공유되지 않은 클러스터에서 두 노드를 설정할 수 있습니다. | SQL Server 2014 및 2012 Enterprise 버전
**장애 조치(failover) 클러스터링(Always On FCI)** | SQL Server는 온-프레미스 SQL Server 작업의 고가용성을 위해 Windows 장애 조치(failover) 클러스터링을 활용합니다.<br/><br/>공유 디스크를 사용하는 SQL Server 서버의 인스턴스를 실행하는 노드는 장애 조치 클러스터에서 구성됩니다. 인스턴스가 다운 된 경우 hello 클러스터 장애 하나 toodifferent 조치 합니다.<br/><br/>hello 클러스터 실패 또는 공유 저장소에서 작동 중단 으로부터 보호 하지 않습니다. hello 공유 디스크는 iSCSI, 파이버 채널을 구현할 수 있습니다 또는 공유 vhdx를 이용 합니다. | SQL Server Enterprise 버전<br/><br/>SQL Server Standard edition (제한 된 tootwo 노드만 해당)
**데이터베이스 미러링(높은 보안 모드)** | 단일 데이터베이스 tooa 단일 보조 복사본을 보호합니다. 높은 보안(동기) 및 고성능(비동기) 복제 모드에서 모두 사용할 수 있습니다. 장애 조치 클러스터가 필요하지 않습니다. | SQL Server 2008 R2<br/><br/>SQL Server Enterprise 모든 버전
**독립 실행형 SQL Server** | hello SQL Server 및 데이터베이스는 단일 서버 (실제 또는 가상)에 호스트 됩니다. 호스트 클러스터링 hello 서버가 가상 경우 고가용성을 위해 사용 됩니다. 게스트 수준의 고가용성은 없습니다. | Enterprise 또는 Standard 에디션

## <a name="deployment-recommendations"></a>배포 권장 사항

이 표에서는 Site Recovery와 SQL Server BCDR 기술을 통합하기 위한 권장 사항을 요약합니다.

| **버전** | **에디션** | **배포웹사이트를** | **온-프레미스 tooon 온-프레미스** | **온-프레미스 tooAzure** |
| --- | --- | --- | --- | --- |
| SQL Server 2014 또는 2012 |Enterprise |장애 조치 클러스터 인스턴스 |Always On 가용성 그룹 |Always On 가용성 그룹 |
|| Enterprise |고가용성을 위한 Always On 가용성 그룹 |Always On 가용성 그룹 |Always On 가용성 그룹 | |
|| Standard |장애 조치 클러스터 인스턴스(FCI) |로컬 미러를 사용하는 Site Recovery 복제 |로컬 미러를 사용하는 Site Recovery 복제 | |
|| Enterprise 또는 Standard |독립 실행형 |Site Recovery 복제 |Site Recovery 복제 | |
| SQL Server 2008 R2 또는 2008 |Enterprise 또는 Standard |장애 조치 클러스터 인스턴스(FCI) |로컬 미러를 사용하는 Site Recovery 복제 |로컬 미러를 사용하는 Site Recovery 복제 |
|| Enterprise 또는 Standard |독립 실행형 |Site Recovery 복제 |Site Recovery 복제 | |
| SQL Server(모든 버전) |Enterprise 또는 Standard |장애 조치 클러스터 인스턴스 - DTC 응용 프로그램 |Site Recovery 복제 |지원되지 않음 |

## <a name="deployment-prerequisites"></a>배포 필수 조건

* 지원되는 SQL Server 버전을 실행하는 온-프레미스 SQL Server 배포입니다. 일반적으로 SQL Server에 대한 Active Directory도 필요합니다.
* hello 요구 사항에 대 한 hello toodeploy 시나리오입니다. 에 대 한 지원 요구 사항에 대 한 자세한 [복제 tooAzure](site-recovery-support-matrix-to-azure.md) 및 [온-프레미스](site-recovery-support-matrix.md), 및 [배포 필수 구성 요소](site-recovery-prereq.md)합니다.
* azure에서 실행된 hello 복구를 tooset [Azure 가상 컴퓨터 준비 평가](http://www.microsoft.com/download/details.aspx?id=40898) toomake 있는지 Azure Site Recovery와 호환 되는 SQL Server 가상 컴퓨터에 도구입니다.

## <a name="set-up-active-directory"></a>Active Directory 설정

Active Directory에 대 한 SQL Server toorun hello 보조 복구 사이트에 제대로 설정.

* **소규모 기업은**-응용 프로그램 및 hello 온-프레미스 사이트에 대 한 단일 도메인 컨트롤러는 적은 수 toofail hello 전체 사이트를 통해 하려는 경우 권장 사이트 복구 복제 tooreplicate hello 도메인 컨트롤러를 사용 하 여 toohello 보조 데이터 센터 또는 tooAzure 합니다.
* **중간 toolarge 엔터프라이즈**-Active Directory 포리스트, 응용 프로그램의 많은 경우 응용 프로그램 또는 워크 로드를 하나씩 toofail 또는 hello 보조 데이터 센터에 추가 도메인 컨트롤러를 설정한 것이 좋습니다 Azure입니다. Always On 가용성 그룹 toorecover tooa 원격 사이트를 사용 하는 경우에 hello 보조 사이트에서 또는 Azure에서 toouse hello 복구할 SQL Server 인스턴스에 대 한 다른 추가 도메인 컨트롤러를 설정 하는 것이 좋습니다.

이 문서의 지침 hello hello 보조 위치에는 도메인 컨트롤러를 사용할 수 있는지를 가정 합니다. Site Recovery를 사용한 Active Directory 보호에 대해 [자세히 알아보세요](site-recovery-active-directory.md).


## <a name="integrate-with-sql-server-always-on-for-replication-tooazure"></a>복제 tooAzure에 대 한 SQL Server Always On와 통합

여기에 사용자의 할 toodo:

1. Azure Automation 계정에 스크립트를 가져옵니다. Hello 스크립트 toofailover SQL 가용성 그룹이 포함 되어이에서 [리소스 관리자 가상 컴퓨터가](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAG.ps1) 및 [클래식 가상 컴퓨터](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAGClassic.ps1)합니다.

    [![TooAzure 배포](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)


1. ASR-SQL-FailoverAG hello hello 복구 계획의 첫 번째 그룹의 이전 동작으로 추가 합니다.

1. Hello hello 가용성 그룹의 hello 스크립트 toocreate 자동화 변수 tooprovide hello 이름에서에서 사용할 수 있는 지침을 따릅니다.

### <a name="steps-toodo-a-test-failover"></a>단계 toodo 테스트 장애 조치

SQL Always On은 테스트 장애 조치(failover)를 고유하게 지원하지 않습니다. 따라서 hello 다음을 사용 하는 것이 좋습니다.

1. 설정 [Azure 백업](../backup/backup-azure-vms.md) Azure의 hello 가용성 그룹 복제본을 호스팅하는 hello 가상 컴퓨터에 있습니다.

1. Hello 복구 계획의 테스트 장애 조치를 트리거하기 전에 hello 이전 단계에서 발생 하는 hello 백업 으로부터 hello 가상 컴퓨터를 복구 합니다.

    ![Azure Backup에서 복원 ](./media/site-recovery-sql/restore-from-backup.png)

1. [강제 쿼럼](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum#PowerShellProcedure) hello 가상 컴퓨터 백업에서 복원 합니다.

1. Hello 수신기 tooan ip hello 테스트 장애 조치 네트워크에서 사용할 수 있는 IP를 업데이트 합니다.

    ![수신기 IP 업데이트](./media/site-recovery-sql/update-listener-ip.png)

1. 수신기를 온라인 상태로 만듭니다.

    ![수신기를 온라인 상태로 만들기](./media/site-recovery-sql/bring-listener-online.png)

1. 프런트 엔드 IP 풀 해당 tooeach 가용성 그룹 수신기에서 생성 한 IP 및 hello 백 엔드 풀에 추가 된 hello SQL 가상 컴퓨터 부하 분산 장치를 만듭니다.

     ![부하 분산 장치 만들기 - 프런트 엔드 IP 풀 ](./media/site-recovery-sql/create-load-balancer1.png)

    ![부하 분산 장치 만들기 - 백 엔드 풀 ](./media/site-recovery-sql/create-load-balancer2.png)

1. Hello 복구 계획의 테스트 장애 조치를 수행 합니다.

### <a name="steps-toodo-a-failover"></a>단계 toodo 장애 조치

테스트 장애 조치를 수행 하 여 hello 스크립트 hello 복구 계획 및 유효성이 검사 된 hello 복구 계획에 추가 했으면, hello 복구 계획의 장애 조치를 수행할 수 있습니다.


## <a name="integrate-with-sql-server-always-on-for-replication-tooa-secondary-on-premises-site"></a>복제 tooa 보조 온-프레미스 사이트에 대 한 SQL Server Always On와 통합

Hello SQL Server 고가용성 (또는 FCI)에 대 한 가용성 그룹을 사용 하는, 경우에 hello 복구 사이트에서 가용성 그룹을 사용 하는 것이 좋습니다. Note이 적용 분산된 트랜잭션을 사용 하지 않는 tooapps 됩니다.

1. [데이터베이스를 구성](https://msdn.microsoft.com/library/hh213078.aspx) 합니다.
1. Hello 보조 사이트의 가상 네트워크를 만듭니다.
1. Hello 가상 네트워크와 hello 기본 사이트 간에 사이트 간 VPN 연결을 설정 합니다.
1. Hello 복구 사이트에서 가상 컴퓨터를 만들고에 SQL Server를 설치 합니다.
1. Hello 기존 Always On 가용성 그룹 toohello 확장 새 SQL Server VM입니다. 이 SQL Server 인스턴스를 비동기 복제 복사본으로 구성합니다.
1. 가용성 그룹 수신기를 만들거나 hello 기존 수신기 tooinclude hello 비동기 복제 가상 컴퓨터를 업데이트 합니다.
1. Hello 수신기를 사용 하 여 해당 hello 응용 프로그램이 팜에 설정 되어 있는지 확인 합니다. 데이터베이스 서버 이름 hello를 사용 하 여를 설치 인 경우 업데이트 toouse hello 수신기 tooreconfigure 필요 하지 hello 장애 조치 후 것입니다.

분산된 트랜잭션을 사용하는 응용 프로그램의 경우 [VMware/물리적 서버 사이트 간 복제](site-recovery-vmware-to-vmware.md)로 Site Recovery를 배포하는 것이 좋습니다.

### <a name="recovery-plan-considerations"></a>복구 계획 고려 사항
1. Hello 기본 및 보조 사이트에서이 샘플 스크립트 toohello VMM 라이브러리를 추가 합니다.

        Param(
        [string]$SQLAvailabilityGroupPath
        )
        import-module sqlps
        Switch-SqlAvailabilityGroup -Path $SQLAvailabilityGroupPath -AllowDataLoss -force

1. Hello 응용 프로그램에 대 한 복구 계획을 만들 때 사전 작업 tooGroup 1 스크립팅된 단계를 추가 하, 가용성 그룹에 대해 hello 스크립트 toofail를 호출 합니다.

## <a name="protect-a-standalone-sql-server"></a>독립 실행형 SQL Server 보호

이 시나리오에서는 사이트 복구 복제 tooprotect hello SQL Server 컴퓨터를 사용 하는 것이 좋습니다. SQL Server VM 또는 물리적 서버 인지 하 고 원하는 tooreplicate tooAzure 또는 보조 온-프레미스 사이트 hello 정확한 단계가 달라 집니다. [Site Recovery 시나리오](site-recovery-overview.md)에 대해 자세히 알아봅니다.

## <a name="protect-a-sql-server-cluster-standard-editionwindows-server-2008-r2"></a>SQL Server 클러스터 보호(표준 에디션/Windows Server 2008 R2)

SQL Server Standard edition 또는 SQL Server 2008 r 2를 실행 하는 클러스터에 대 한 사이트 복구 복제 tooprotect SQL Server를 사용 하는 것이 좋습니다.

### <a name="on-premises-tooon-premises"></a>온-프레미스 tooon 온-프레미스

* Hello 응용 프로그램에서 분산된 트랜잭션을 사용 하는 경우 배포는 것이 좋습니다 [SAN 복제를 사용 하 여 사이트 복구](site-recovery-vmm-san.md) Hyper-v 환경에 대 한 또는 [/물리적 서버 tooVMware](site-recovery-vmware-to-vmware.md) VMware 환경에 대 한 합니다.
* 비-DTC 응용 프로그램에 대 한 접근 방식 toorecover hello 클러스터 위에 hello를 로컬 우선 DB 미러를 활용 하 여 독립 실행형 서버로 사용 합니다.

### <a name="on-premises-tooazure"></a>온-프레미스 tooAzure

사이트 복구에서 게스트를 제공 하지 않으면 tooAzure를 복제 하는 경우 클러스터 지원. 또한 SQL Server는 Standard 에디션에 대해 저비용 재해 복구 솔루션을 제공하지 않습니다. 이 시나리오에서는 hello 온-프레미스 SQL Server 클러스터 tooa 독립 실행형 SQL Server를 보호 하 고 Azure에서 복구는 것이 좋습니다.

1. Hello 온-프레미스 사이트에서 추가 독립 실행형 SQL Server 인스턴스를 구성 합니다.
1. Hello 데이터베이스에 대 한 hello 인스턴스 tooserve 미러 서버로 구성 tooprotect 원하는 합니다. 높은 보안 모드에서 미러링을 구성합니다.
1. Hello 온-프레미스 사이트에서 사이트 복구에 대 한 구성 ([Hyper-v](site-recovery-hyper-v-site-to-azure.md) 또는 [Vm/물리적 서버)](site-recovery-vmware-to-azure-classic.md)합니다.
1. 사이트 복구 복제 tooreplicate hello 새 SQL Server 인스턴스 tooAzure를 사용 합니다. 우선 미러 복사본 이므로, 사이트 복구 복제를 사용 하 여 복제 된 tooAzure 수는 있지만 hello 주 클러스터와 동기화 됩니다.


![표준 클러스터](./media/site-recovery-sql/standalone-cluster-local.png)

### <a name="failback-considerations"></a>장애 복구 고려 사항

SQL Server Standard 클러스터에 대 한 계획 되지 않은 장애 조치 후 장애 복구에는 SQL server 백업 및 복원 hello 미러 인스턴스 toohello 원래 클러스터에서 hello 미러의 재설정이 발생 된 필요합니다.

## <a name="next-steps"></a>다음 단계
Site Recovery 아키텍처에 대해 [자세히 알아봅니다](site-recovery-components.md).
