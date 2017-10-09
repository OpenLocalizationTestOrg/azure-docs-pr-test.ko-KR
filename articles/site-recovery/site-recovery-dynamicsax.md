---
title: "Azure Site Recovery를 사용 하 여 다중 계층 Dynamics AX 배포 aaaReplicate | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooreplicate 하 고 Azure Site Recovery를 사용 하 여 Dynamics AX 보호"
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
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a>Azure Site Recovery를 사용하여 다중 계층 Dynamics AX 응용 프로그램 복제

## <a name="overview"></a>개요


Microsoft Dynamics AX 위치에서 기업 toostandardized 프로세스 간에 hello 가장 인기 있는 ERP 솔루션 중 하나는, 리소스 및 규정 준수를 단순화 관리 합니다. 매우 중요 한 toobe 있는지는 hello 응용 프로그램은 중요 한 tooan 조직 비즈니스 고려 하는 모든 재해 응용 프로그램 실행 중에 있어야 최소 시간입니다.

오늘날, Microsoft Dynamics AX는 기본적으로 재해 복구 기능을 제공하지 않습니다. Microsoft Dynamics AX로 응용 프로그램 개체 서버, Active Directory (AD) SQL 데이터베이스 서버, SharePoint 서버와 같은 많은 서버 구성 요소, 이러한 각 구성이 요소에 대 한 보고 서버 등 toomanage hello 재해 복구는 수동으로 뿐만 아니라 들지만 오류가 발생할 수도 있습니다.

이 문서에서는 [Azure Site Recovery](site-recovery-overview.md)를 사용하여 Dynamics AX 응용 프로그램을 위한 재해 복구 솔루션을 만드는 방법에 대해 자세히 설명합니다. 한 번 클릭 복구 계획, 지원되는 구성 및 필수 구성 요소를 사용하는 계획된/계획되지 않은/테스트 장애 조치(Failover)에도 적용됩니다.
Azure Site Recovery 기반 재해 복구 솔루션은 Microsoft Dynamics AX에 의해 완벽하게 테스트, 인증 및 권장됩니다.



## <a name="prerequisites"></a>필수 조건

Azure Site Recovery를 사용 하 여 Dynamics AX 응용 프로그램에 대 한 재해 복구를 구현 하려면 다음 필수 구성 요소를 완료 하는 hello 합니다.

•   온-프레미스 Dynamics AX 배포 설치

•   Microsoft Azure 구독에 Azure Site Recovery Services 자격 증명 모음 생성

• 경우 Azure는 복구 사이트로 hello Azure 가상 컴퓨터 준비 평가 도구에서 실행 tooensure Vm은 Azure Vm 및 Azure 사이트 복구 서비스와 호환 되는


## <a name="site-recovery-support"></a>Site Recovery 지원

이 문서를 만드는 목적은 hello, VMware 가상 컴퓨터와 Windows Server 2012 R2 Enterprise에서 Dynamics AX 2012R3 사용 되었습니다. 사이트 복구 복제 응용 프로그램을 알 수 없는 그대로 hello 권장 사항을 여기에 제공 된 예상된 toohold도 다음과 같은 시나리오에 있습니다.

### <a name="source-and-target"></a>원본 및 대상

**시나리오** | **tooa 보조 사이트** | **tooAzure**
--- | --- | ---
**Hyper-V** | 예 | 예
**VMware** | 예 | 예
**물리적 서버** | 예 | 예

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a>Azure Site Recovery를 사용하여 Dynamics AX 응용 프로그램의 DR 사용
### <a name="protect-your-dynamics-ax-application"></a>Dynamics AX 응용 프로그램 보호
Hello Dynamics AX 요구 toobe의 각 구성 요소를 보호 된 tooenable hello 완전 한 응용 프로그램 복제 및 복구 합니다. 이 섹션에서는 다음을 설명합니다.

**1. Active Directory의 보호**

**2. SQL 계층의 보호**

**3. 앱 및 웹 계층의 보호**

**4. 네트워킹 구성**

**5. 복구 계획**

### <a name="1-setup-ad-and-dns-replication"></a>1. AD 및 DNS 복제 설정

Active Directory 응용 프로그램 toofunction Dynamics AX에 대 한 hello DR 사이트에 필요 합니다. Hello 복잡 한 hello 고객의 온-프레미스 환경에 따라 권장된 선택 사항이 두 가지가 있습니다.

**옵션 1**

Hello 고객에 게 적은 수의 응용 프로그램 및 그의 전체에 대 한 단일 도메인 컨트롤러가 온-프레미스 사이트 않으며 됩니다 수 장애 조치 hello 전체 사이트 함께 ASR 복제 tooreplicate hello DC 컴퓨터 toosecondary 사이트 (사용 하는 것이 좋습니다. 에 해당 사이트 tooSite와 사이트 tooAzure).

**옵션 2**

Hello 고객 응용 프로그램의 많은 수 및 Active Directory 포리스트 실행 되는 장애 조치 응용 프로그램은 거의 한 번에 경우 hello DR 사이트에서 추가 도메인 컨트롤러 설정 것이 좋습니다 (보조 사이트 또는 Azure).

너무를 참조 하십시오[DR 사이트에서 사용할 수 있는 도메인 컨트롤러를 만드는 부록 가이드](site-recovery-active-directory.md)합니다. 이 문서의 나머지 부분에서는 DR 사이트에서 DC를 사용할 수 있다고 가정합니다.

### <a name="2-setup-sql-server-replication"></a>2. SQL Server 복제 설정
Hello 권장를 보호 하기 위한 옵션에 대 한 자세한 기술 지침에 대 한 toocompanion 가이드를 참조 하십시오 [SQL 계층](site-recovery-sql.md)합니다.

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a>3. Dynamics AX 클라이언트 및 AOS VM에 대한 보호를 사용 하도록 설정
Hello Vm에 배포 되어 있는지 여부에 따라 관련 Azure Site Recovery 구성 수행 [Hyper-v](site-recovery-hyper-v-site-to-azure.md) 또는 [VMware](site-recovery-vmware-to-azure.md)합니다.

> [!TIP]
> 권장된 크래시 일치 빈도 tooconfigure 15 분입니다.
>

스냅숏 아래 hello 'VMware 사이트 tooAzure' 보호 시나리오에서 Dynamics 구성 요소는 vm hello 보호 상태를 보여 줍니다.
![보호된 항목](./media/site-recovery-dynamics-ax/protecteditems.png)

### <a name="4-configure-networking"></a>4. 네트워킹 구성
VM 계산 및 네트워크 설정 구성

Hello AX 클라이언트와 AOS Vm에 대 한 hello VM 네트워크 장애 조치 후 연결 된 toohello 적합 한 DR 네트워크 얻을 수 있도록 Azure 사이트 복구에서 네트워크 설정을 구성 합니다. 이러한 계층에 대 한 hello DR 네트워크는 라우팅 가능 toohello SQL 계층을 확인 합니다.

선택할 수 있습니다 hello 스냅숏 아래에 나와 있는 것 처럼 hello에 hello VM 복제 항목 tooconfigure hello 네트워크 설정 합니다.

* AOS에 대 한 서버 hello 올바른 가용성 집합을 선택합니다.

* 고정 IP를 사용 하는 다음 hello에 가상 컴퓨터 tootake hello 원하는 hello IP를 지정 하는 경우 **대상 IP** 필드 ![네트워크 설정](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)



### <a name="5-creating-a-recovery-plan"></a>5. 복구 계획 만들기

Azure Site Recovery tooautomate hello 장애 조치 프로세스에서 복구 계획을 만들 수 있습니다. Hello 복구 계획의 앱 계층 및 웹 계층을 추가 합니다. 응용 프로그램 계층 전에 프런트 엔드 종료 하는 hello 하므로 서로 다른 그룹에 정렬 합니다.

1)  구독에 hello Azure Site Recovery 자격 증명 모음을 선택 하 고 ' 복구 계획 ' 타일을 클릭 합니다.

2)  ‘+ 복구 계획’을 클릭하고 이름을 지정합니다.

3)  Hello 'Source' 및 'Target'를 선택 합니다. hello 대상 Azure 또는 보조 사이트가 될 수 있습니다. Hello 배포 모델을 지정 해야 Azure를 선택 하는 경우

![복구 계획 만들기](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  Hello AOS 및 클라이언트 Vm toohello 복구 계획을 선택 하 고 ✓를 클릭 합니다.
![복구 계획 만들기](./media/site-recovery-dynamics-ax/selectvms.png)


![복구 계획](./media/site-recovery-dynamics-ax/recoveryplan.png)

아래에 설명 된 대로 여러 단계를 추가 하 여 Dynamics AX 응용 프로그램에 대 한 hello 복구 계획을 사용자 지정할 수 있습니다. 스냅숏 위에 hello hello 단계를 모두 추가한 후 hello 전체 복구 계획을 보여 줍니다.

*단계:*

*1. SQL Server 장애 조치(failover) 단계*

너무 참조[' SQL Server DR 솔루션 '](site-recovery-sql.md) 복구 단계 특정 tooSQL 서버에 대 한 자세한 내용은 부록 가이드입니다.

*2. 장애 조치 그룹 1: hello AOS Vm 장애 조치합니다*

선택 된 hello 복구 지점 PIT 가능한 toohello 데이터베이스로 가깝게 하지만 계속 하지 인지 확인 합니다.

*3. 스크립트: 추가 부하 분산 장치 (만 E-A)* 부하 분산 장치 tooit tooadd 상황 AOS VM 그룹 뒤 (Azure 자동화)를 통해 스크립트를 추가 합니다. 이 작업 스크립트 toodo를 사용할 수 있습니다. 문서 참조 [tooadd DR 다중 계층 응용 프로그램에 대 한 분산 장치를 로드 하는 방법](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)

*4. 장애 조치 그룹 2: hello AX 클라이언트 Vm 장애 조치할 합니다.*
Hello 웹 계층 Vm hello 복구 계획의 일환으로 장애 조치할 합니다.


### <a name="doing-a-test-failover"></a>테스트 장애 조치 수행

DR 솔루션 too'AD 참조 ' 및 특정 tooAD 고려 사항 및 테스트 장애 조치 중 각각의 SQL server에 대 한 'SQL Server DR 솔루션 부록 가이드입니다.

1.  TooAzure 포털 이동 하 고 사이트 복구 자격 증명 모음을 선택 합니다.
2.  Dynamics AX에 대해 생성 하는 hello 복구 계획을 클릭 합니다.
3.  ‘테스트 장애 조치(Failover)’를 클릭합니다.
4.  Hello 가상 네트워크 toostart hello 테스트 장애 조치 프로세스를 선택 합니다.
5.  Hello 보조 환경의 되 면 사용자 유효성 검사를 수행할 수 있습니다.
6.  Hello 유효성 검사가 완료 되 면 유효성 검사 완료를 선택할 수 있습니다 및 hello 테스트 장애 조치 환경을 정리 합니다.

에 따라 [이 지침은](site-recovery-test-failover-to-azure.md) toodo 테스트 장애 조치 합니다.

### <a name="doing-a-failover"></a>장애 조치 수행

1.  TooAzure 포털 이동 하 고 사이트 복구 자격 증명 모음을 선택 합니다.
2.  Dynamics AX에 대해 생성 하는 hello 복구 계획을 클릭 합니다.
3.  ‘장애 조치(Failover)’를 클릭하고 ‘장애 조치(Failover)’를 선택합니다.
4.  Hello 대상 네트워크를 선택 하 고 ✓ toostart hello 장애 조치 프로세스를 클릭 합니다.

장애 조치를 수행할 때 [이 지침](site-recovery-failover.md)을 따릅니다.

### <a name="perform-a-failback"></a>장애 복구 수행

Too'SQL 서버 DR 솔루션 참조 ' 장애 복구 하는 동안 특정 tooSQL 서버 고려 사항에 대 한 부록 가이드입니다.

1.  TooAzure 포털 이동 하 고 사이트 복구 자격 증명 모음을 선택 합니다.
2.  Dynamics AX에 대해 생성 하는 hello 복구 계획을 클릭 합니다.
3.  ‘장애 조치(Failover)’를 클릭하고 장애 조치(Failover)를 선택합니다.
4.  ‘방향 변경’을 클릭합니다.
5.  Hello 적절 한 옵션-VM 만들기 옵션와 데이터 동기화 선택
6.  ✓ toostart hello Failback' 프로세스를 클릭 합니다.


장애 복구를 수행할 때 [이 지침](site-recovery-failback-azure-to-vmware.md)을 따릅니다.

##<a name="summary"></a>요약
Azure Site Recovery를 사용하여 Dynamics AX 응용 프로그램에 대한 완전히 자동화된 재해 복구 계획을 만들 수 있습니다. 어디에서 나 몇 초 이내 hello 장애 조치를 시작할 수 있습니다에 이벤트를 더 이상의 hello 및 hello 응용 프로그램 실행를 가져오고 (분)에서입니다.

## <a name="next-steps"></a>다음 단계
읽기 [어떤 작업 부하를 보호할 수 있습니까?](site-recovery-workload.md) toolearn Azure Site Recovery와 엔터프라이즈 작업을 보호 하는 방법에 대 한 자세한 합니다.
