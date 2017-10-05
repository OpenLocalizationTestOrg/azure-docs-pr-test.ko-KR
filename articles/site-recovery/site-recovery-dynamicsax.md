---
title: "Azure Site Recovery를 사용하여 다중 계층 Dynamics AX 배포 복제 | Microsoft Docs"
description: "이 문서는 Azure Site Recovery를 사용하여 Dynamics AX를 복제 및 보호하는 방법에 대해 설명합니다."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: 03127c8f4841b67436c4819628319705af0b2cd5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a>Azure Site Recovery를 사용하여 다중 계층 Dynamics AX 응용 프로그램 복제

## <a name="overview"></a>개요


Microsoft Dynamics AX는 위치 간 프로세스, 리소스 관리 및 규정 준수 간소화를 표준화하는 기업들에게 가장 인기 있는 ERP 솔루션 중 하나입니다. 조직에게 응용 프로그램은 비즈니스에 중요한 요소입니다. 이러한 점을 고려할 때, 모든 재해가 발생할 경우 응용 프로그램이 최소 시간 내에 실행되어야 함은 매우 중요합니다.

오늘날, Microsoft Dynamics AX는 기본적으로 재해 복구 기능을 제공하지 않습니다. Microsoft Dynamics AX는 응용 프로그램 개체 서버, AD(Active Directory), SQL Database 서버, SharePoint Server, 보고 서버 등과 같은 많은 서버 구성 요소로 구성되어 있습니다. 이러한 각 구성의 재해 복구를 수동으로 관리하는 것은 비용이 많이 들 뿐만 아니라 오류가 발생하기 쉽습니다.

이 문서에서는 [Azure Site Recovery](site-recovery-overview.md)를 사용하여 Dynamics AX 응용 프로그램을 위한 재해 복구 솔루션을 만드는 방법에 대해 자세히 설명합니다. 한 번 클릭 복구 계획, 지원되는 구성 및 필수 구성 요소를 사용하는 계획된/계획되지 않은/테스트 장애 조치(Failover)에도 적용됩니다.
Azure Site Recovery 기반 재해 복구 솔루션은 Microsoft Dynamics AX에 의해 완벽하게 테스트, 인증 및 권장됩니다.



## <a name="prerequisites"></a>필수 조건

Azure Site Recovery를 사용하여 Dynamics AX 응용 프로그램을 위한 재해 복구를 구현하려면 다음과 같은 필수 조건을 완료해야 합니다.

•   온-프레미스 Dynamics AX 배포 설치

•   Microsoft Azure 구독에 Azure Site Recovery Services 자격 증명 모음 생성

•   Azure가 복구 사이트인 경우 VM에서 Azure Virtual Machine 준비 평가 도구를 실행하여 Azure VM 및 Azure Site Recovery Services와 호환되는지 확인


## <a name="site-recovery-support"></a>Site Recovery 지원

이 문서를 작성하기 위해 Windows Server 2012 R2 Enterprise에서 Dynamics AX 2012 R3가 있는 VMware 가상 컴퓨터가 사용되었습니다. Site Recovery 복제는 응용 프로그램을 제한하지 않으므로 여기서 제시하는 권장 사항은 다음 시나리오에서도 유지됩니다.

### <a name="source-and-target"></a>원본 및 대상

**시나리오** | **보조 사이트로** | **Azure로**
--- | --- | ---
**Hyper-V** | 예 | 예
**VMware** | 예 | 예
**물리적 서버** | 예 | 예

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a>Azure Site Recovery를 사용하여 Dynamics AX 응용 프로그램의 DR 사용
### <a name="protect-your-dynamics-ax-application"></a>Dynamics AX 응용 프로그램 보호
완전한 응용 프로그램 복제 및 복구를 위해서는 Dynamics AX의 각 구성 요소를 보호해야 합니다. 이 섹션에서는 다음을 설명합니다.

**1. Active Directory의 보호**

**2. SQL 계층의 보호**

**3. 앱 및 웹 계층의 보호**

**4. 네트워킹 구성**

**5. 복구 계획**

### <a name="1-setup-ad-and-dns-replication"></a>1. AD 및 DNS 복제 설정

Active Directory는 Dynamics AX 응용 프로그램 작동을 위한 DR 사이트에 필요합니다. 고객의 온-프레미스 환경의 복잡도에 따라 권장되는 두 가지 옵션이 있습니다.

**옵션 1**

고객이 적은 수의 응용 프로그램과 전체 온-프레미스 사이트에 대한 단일 도메인 컨트롤러를 보유하고 있고 전체 사이트를 장애 조치(failover)하려는 경우 ASR 복제를 사용하여 DC 컴퓨터를 보조 사이트로 복제하는 것이 좋습니다(사이트 간 및 사이트-Azure에 적용 가능).

**옵션 2**

고객이 많은 수의 응용 프로그램을 보유하고 있고 Active Directory 포리스트를 실행 중이며 한 번에 소수의 응용 프로그램을 장애 조치(failover)하려는 경우 DR 사이트(보조 사이트 또는 Azure)에 추가 도메인 컨트롤러를 설정하는 것이 좋습니다.

[DR 사이트에서 사용할 수 있는 도메인 컨트롤러 만들기에 관한 부록 가이드](site-recovery-active-directory.md)를 참조하세요. 이 문서의 나머지 부분에서는 DR 사이트에서 DC를 사용할 수 있다고 가정합니다.

### <a name="2-setup-sql-server-replication"></a>2. SQL Server 복제 설정
[SQL 계층](site-recovery-sql.md) 보호를 위해 권장되는 옵션에 대한 자세한 기술 지침은 부록 가이드를 참조하세요.

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a>3. Dynamics AX 클라이언트 및 AOS VM에 대한 보호를 사용 하도록 설정
VM이 [Hyper-V](site-recovery-hyper-v-site-to-azure.md) 또는 [VMware](site-recovery-vmware-to-azure.md)에 배포되었는지 여부에 따라 관련 Azure Site Recovery 구성을 수행합니다.

> [!TIP]
> 권장되는 충돌 일관성 빈도는 15분입니다.
>

스냅숏 아래에는 ‘VMware 사이트에서 Azure로’ 보호 시나리오에서 Dynamics 구성 요소 VM의 보호 상태가 나와 있습니다.
![보호된 항목](./media/site-recovery-dynamics-ax/protecteditems.png)

### <a name="4-configure-networking"></a>4. 네트워킹 구성
VM 계산 및 네트워크 설정 구성

AX 클라이언트 및 AOS VM의 경우 Azure Site Recovery에서 네트워크 설정을 구성하여 장애 조치(failover) 후에 VM 네트워크가 올바른 DR 네트워크에 연결되도록 합니다. 이러한 계층에 대한 DR 네트워크가 SQL 계층으로 라우팅할 수 있는지 확인합니다.

아래 스냅숏에 나온 것처럼 복제 항목에서 VM을 선택하여 네트워크 설정을 구성할 수 있습니다.

* AOS 서버의 경우 올바른 가용성 집합을 선택합니다.

* 고정 IP를 사용하는 경우 **대상 IP** 필드에 가상 컴퓨터에서 사용할 IP를 지정합니다![네트워크 설정](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png).



### <a name="5-creating-a-recovery-plan"></a>5. 복구 계획 만들기

Azure Site Recovery에서 복구 계획을 만들어 장애 조치(failover) 프로세스를 자동화할 수 있습니다. 복구 계획의 앱 계층 및 웹 계층을 추가합니다. 앱 계층 이전에 프런트 엔드가 종료되도록 다른 그룹으로 순서를 정합니다.

1)  구독에서 Azure Site Recovery 자격 증명 모음을 선택하고 ‘복구 계획’ 타일을 클릭합니다.

2)  ‘+ 복구 계획’을 클릭하고 이름을 지정합니다.

3)  ‘원본’ 및 ‘대상’을 선택합니다. 대상은 Azure 또는 보조 사이트일 수 있습니다. Azure를 선택하는 경우 배포 모델을 지정해야 합니다.

![복구 계획 만들기](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  복구 계획에 AOS 및 클라이언트 VM을 선택하고 ✓를 클릭합니다.
![복구 계획 만들기](./media/site-recovery-dynamics-ax/selectvms.png)


![복구 계획](./media/site-recovery-dynamics-ax/recoveryplan.png)

아래 설명된 대로 여러 단계를 추가하여 Dynamics AX 응용 프로그램에 대한 복구 계획을 사용자 지정할 수 있습니다. 위의 스냅숏은 단계를 모두 추가한 후 전체 복구 계획을 보여 줍니다.

*단계:*

*1. SQL Server 장애 조치(failover) 단계*

SQL 서버와 관련된 복구 단계에 대한 자세한 내용은 [‘SQL Server DR 솔루션’](site-recovery-sql.md) 부록 가이드를 참조하세요.

*2. 장애 조치(Failover) 그룹 1: AOS VM 장애 조치(Failover)*

선택한 복구 지점이 데이터베이스 PIT에 가능한 한 가까우면서도 선행되지 않는지 확인합니다.

*3. 스크립트: 부하 분산 장치 추가(E-A만 해당)* AOS VM 그룹이 나온 뒤 스크립트를 추가(Azure Automation을 통해)하여 부하 분산 장치를 추가합니다. 스크립트를 사용하여 이 작업을 수행할 수 있습니다. [다중 계층 응용 프로그램 DR에 대한 부하 분산 장치를 추가하는 방법](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/) 문서를 참조하세요.

*4. 장애 조치(Failover) 그룹 2: AX 클라이언트 VM 장애 조치(Failover)*
복구 계획의 일부로 웹 계층 VM을 장애 조치합니다.


### <a name="doing-a-test-failover"></a>테스트 장애 조치 수행

테스트 장애 조치(Failover)를 수행하는 동안 AD 및 SQL 서버에 각각 관련된 고려 사항에 대해서는 ‘AD DR 솔루션’ 및 ‘SQL Server DR 솔루션’ 부록 가이드를 참조하세요.

1.  Azure Portal로 이동하여 Site Recovery 자격 증명 모음을 선택합니다.
2.  Dynamics AX에 대해 만든 복구 계획을 클릭합니다.
3.  ‘테스트 장애 조치(Failover)’를 클릭합니다.
4.  가상 네트워크를 선택하여 테스트 장애 조치(failover) 프로세스를 시작합니다.
5.  보조 환경이 가동 중이면 유효성 검사를 수행할 수 있습니다.
6.  유효성 검사가 완료되면 '유효성 검사 완료'를 선택할 수 있으며 테스트 장애 조치 환경이 정리됩니다.

[이 지침](site-recovery-test-failover-to-azure.md)에 따라 테스트 장애 조치를 수행합니다.

### <a name="doing-a-failover"></a>장애 조치 수행

1.  Azure Portal로 이동하여 Site Recovery 자격 증명 모음을 선택합니다.
2.  Dynamics AX에 대해 만든 복구 계획을 클릭합니다.
3.  ‘장애 조치(Failover)’를 클릭하고 ‘장애 조치(Failover)’를 선택합니다.
4.  대상 네트워크를 선택하고 ✓를 클릭하여 장애 조치(Failover) 프로세스를 시작합니다.

장애 조치를 수행할 때 [이 지침](site-recovery-failover.md)을 따릅니다.

### <a name="perform-a-failback"></a>장애 복구 수행

장애 복구 동안 SQL 서버와 관련된 고려 사항은 ‘SQL Server DR 솔루션’ 부록 가이드를 참조하세요.

1.  Azure Portal로 이동하여 Site Recovery 자격 증명 모음을 선택합니다.
2.  Dynamics AX에 대해 만든 복구 계획을 클릭합니다.
3.  ‘장애 조치(Failover)’를 클릭하고 장애 조치(Failover)를 선택합니다.
4.  ‘방향 변경’을 클릭합니다.
5.  데이터 동기화 및 VM 만들기 옵션 중 적절한 옵션을 선택합니다.
6.  ✓를 클릭하여 ‘장애 복구’ 프로세스를 시작합니다.


장애 복구를 수행할 때 [이 지침](site-recovery-failback-azure-to-vmware.md)을 따릅니다.

##<a name="summary"></a>요약
Azure Site Recovery를 사용하여 Dynamics AX 응용 프로그램에 대한 완전히 자동화된 재해 복구 계획을 만들 수 있습니다. 중단이 발생할 경우 어디서나 몇 초 이내에 장애 조치(failover)를 시작하고 몇 분 만에 응용 프로그램을 가동할 수 있습니다.

## <a name="next-steps"></a>다음 단계
Azure Site Recovery로 엔터프라이즈 워크로드를 보호하는 방법에 대해 자세히 알아보려면 [어떤 워크로드를 보호할 수 있습니까?](site-recovery-workload.md) 를 읽어보세요.
