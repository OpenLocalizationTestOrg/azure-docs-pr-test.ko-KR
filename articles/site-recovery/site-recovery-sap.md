---
title: "Azure Site Recovery를 사용 하 여 다중 계층 SAP NetWeaver 응용 프로그램 배포 aaaProtect | Microsoft Docs"
description: "이 문서에서 설명 하는 방법을 tooprotect SAP NetWeaver 응용 프로그램 배포를 Azure Site Recovery를 사용 하 여"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: manayar
ms.openlocfilehash: 34651c7b14d23a44005372f4f923c401e0224231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-a-multi-tier-sap-netweaver-application-deployment-using-azure-site-recovery"></a>Azure Site Recovery를 사용하여 다중 SAP NetWeaver 응용 프로그램 배포 보호 

대부분의 중대형 SAP 배포에는 어떤 형태의 재해 복구 솔루션이 있습니다.  강력 하 고 테스트 가능한 재해 복구 솔루션의 hello 중요도 많은 핵심 비즈니스 프로세스는 SAP 같은 tooapplications 이동 증가 했습니다.  Azure Site Recovery 테스트와 통합 된 SAP 응용 프로그램 및 hello 기능에는 높이고 총 소유 비용 (TCO) 경쟁 솔루션 보다 대부분 온-프레미스 재해 복구 솔루션을 초과.
Azure Site Recovery를 통해 다음을 수행할 수 있습니다.
* TooAzure 구성 요소를 복제 하 여 온-프레미스를 실행 하는 SAP NetWeaver 및 비-NetWeaver 프로덕션 응용 프로그램의 보호를 사용 하도록 설정 합니다.
* 구성 요소 tooanother Azure 데이터 센터에 복제 하 여 Azure에서 실행 하는 SAP NetWeaver 및 비-NetWeaver 프로덕션 응용 프로그램의 보호를 사용 하도록 설정 합니다.
* SAP 배포 tooAzure toomigrate Site Recovery를 사용 하 여 클라우드 마이그레이션을 간소화 합니다.
* SAP 응용 프로그램 테스팅을 위해 온디맨드로 프로덕션 클론을 만들어 SAP 프로젝트 업그레이드, 테스트 및 프로토타입 생성을 단순화합니다.

이 문서에서 설명 하는 방법을 tooprotect SAP NetWeaver 응용 프로그램 배포를 사용 하 여 [Azure Site Recovery](site-recovery-overview.md)합니다. 이 문서에서는 hello tooanother hello 지원 시나리오 및 구성의 경우, Azure Site Recovery를 사용 하 여 Azure 데이터 센터에 복제 하 여 Azure에서 3 계층 SAP NetWeaver 배포를 보호 하기 위한 모범 사례를 설명 하 고 어떻게 tooperform 장애 조치가 모두 테스트 장애 조치 (재해 복구 훈련) 및 실제 장애 조치 합니다.


## <a name="prerequisites"></a>필수 조건
시작 하기 전에 hello 다음 알고 있어야 합니다.

1. [가상 컴퓨터 tooAzure 복제](azure-to-azure-walkthrough-enable-replication.md)
2. 어떻게 너무[복구 네트워크 디자인](site-recovery-azure-to-azure-networking-guidance.md)
3. [테스트 장애 조치 tooAzure 수행](azure-to-azure-walkthrough-test-failover.md)
4. [장애 조치 tooAzure 수행](site-recovery-failover.md)
5. 어떻게 너무[도메인 컨트롤러 복제](site-recovery-active-directory.md)
6. 어떻게 너무[SQL Server 복제](site-recovery-sql.md)

## <a name="supported-scenarios"></a>지원되는 시나리오
Azure Site Recovery와 hello 다음 시나리오에 대 한 재해 복구 솔루션을 구현할 수 있습니다.
* 설계 tooanother Azure 데이터 센터 (Azure-Azure DR)를 복제 하는 하나의 Azure 데이터 센터에서 실행 되는 SAP 시스템 [여기](https://aka.ms/asr-a2a-architecture)합니다.
* VMWare (또는 물리적) 서버에서 실행 되는 SAP 시스템 온-프레미스 복제 tooa DR 사이트는 Azure 데이터 센터에서 (VMware-Azure DR)으로 설계 된 몇 가지 추가 구성 요소를 필요 [여기](https://aka.ms/asr-v2a-architecture)합니다.
* Hyper-v에서 실행 되는 SAP 시스템 온-프레미스 복제 tooa DR 사이트 설계 된 대로 몇 가지 추가 구성 요소에 필요한 Azure 데이터 센터 (Azure에 하이퍼 V DR)에서 [여기](https://aka.ms/asr-h2a-architecture)합니다.

이 문서에서는 hello 첫 번째 사례 Azure-Azure DR-toodemonstrate Azure 사이트 복구의 SAP 재해 복구 기능을 사용 합니다. Azure 사이트 복구 복제 응용 프로그램을 알 수 없는 그대로 설명 하는 hello 프로세스도 다른 시나리오에 대 한 예상된 toohold입니다.

### <a name="required-foundation-services"></a>필요한 기반 서비스
이 설명서 시나리오 모두 된 foundation 서비스 배포를 수행 하는 hello를 사용 하 여 배포:
* ExpressRoute 또는 사이트 간 가상 사설망(VPN)
* Azure에서 하나 이상의 Active Directory 도메인 컨트롤러와 DNS 서버 실행됨

위의 hello 인프라에 설정 된 이전 toodeploying Azure Site Recovery는 것이 좋습니다.


## <a name="typical-sap-application-deployment"></a>일반 SAP 응용 프로그램 배포
일반적으로 대형 SAP 고객 6 too20 개별 SAP 응용 프로그램 간에 배포합니다.  이러한 응용 프로그램의 대부분 hello SAP NetWeaver ABAP 또는 Java 엔진을 기반으로 합니다.  이러한 핵심 NetWeaver 응용 프로그램을 지원하는 것은 더 적은 규모의 많은 특정 비 NetWeaver SAP 독립 실행형 엔진이며 보통은 비 SAP 응용 프로그램입니다.  

것이 중요 한 tooinventory 모든 hello SAP 응용 프로그램에서 가로 모드와 toodetermine hello 배포 모드 (2 계층 또는 3 계층), 버전, 패치, 실행, 크기, 변동 속도 및 디스크 지 속성 요구 합니다.

![배포 패턴](./media/site-recovery-sap/sap-typical-deployment.png)

SQL Server AlwaysOn, Oracle DataGuard 또는 시스템 복제 HANA 같은 hello 기본 DBMS 도구를 통해 hello SAP 데이터베이스 지 속성 계층을 보호 해야 합니다. hello 클라이언트 계층은 또한 Azure Site Recovery에 의해 보호 되지 않은 DNS 전파 지연, 보안 및 원격 액세스 toohello DR 데이터 센터 같은이 계층에 영향을 주는 중요 한 tooconsider 항목입니다.

Azure Site Recovery는 hello 권장 (A) SCS를 포함 하 여 hello 응용 프로그램 계층에 대 한 솔루션입니다. 다른 응용 프로그램 비 NetWeaver SAP 응용 프로그램 및 기타 응용 프로그램 hello의 일부를 형성와 같은 전반적인는 SAP 배포 환경도 Azure 사이트 복구 보호 되어야 합니다.

## <a name="replicate-virtual-machines"></a>가상 컴퓨터 복제
에 따라 [이 지침은](azure-to-azure-walkthrough-enable-replication.md) 모든 복제 toostart hello SAP 응용 프로그램 가상 컴퓨터 toohello Azure DR 데이터 센터입니다.

고정 IP를 사용 하는 경우에 계산 및 네트워크 설정의 hello 네트워크 인터페이스 카드 섹션에서 가상 컴퓨터 tootake hello 원하는 hello IP를 지정할 수 있습니다.

![대상 IP](./media/site-recovery-sap/sap-static-ip.png)


## <a name="creating-a-recovery-plan"></a>복구 계획 만들기
복구 계획을 나열 하는 응용 프로그램 일관성을 유지 하는 다중 계층 응용 프로그램, 따라서의 다양 한 계층의 hello 장애 조치 수 있습니다. Hello 단계 설명에 따라 [여기](site-recovery-create-recovery-plans.md) 다중 계층 웹 응용 프로그램에 대 한 복구 계획을 만들 때.

### <a name="adding-scripts-toohello-recovery-plan"></a>Toohello 복구 계획 스크립트 추가
해야 toodo hello Azure 가상 컴퓨터 사후 장애 조치/테스트 장애 조치에 대 한 일부 작업에 대 한 응용 프로그램 toofunction 올바르게 합니다. 예: 업데이트 DNS 항목에 설명 된 대로 hello 복구 계획에서 해당 스크립트를 추가 하 여 바인딩 및 연결을 변경 hello post 장애 조치 작업을 자동화할 수 있습니다 [이 여기서](site-recovery-create-recovery-plans.md#add-scripts)합니다.

### <a name="dns-update"></a>DNS 업데이트
Hello DNS 동적 DNS 업데이트를 다음 가상 컴퓨터에 대 한 일반적으로 구성 된 경우는 시작 되 면 hello 새 ip hello DNS를 업데이트 합니다. Tooadd 명시적 단계 tooupdate DNS hello로 새 hello 가상 컴퓨터의 Ip 다음 추가이 [DNS에 IP tooupdate 스크립트](https://aka.ms/asr-dns-update) 복구 계획 그룹에 대 한 게시 작업으로 합니다.  

## <a name="example-azure-to-azure-deployment"></a>Azure-Azure 배포 예제
Hello Azure Site Recovery Azure-Azure DR 시나리오 아래의 hello 다이어그램에 표시 됩니다.
* 기본 데이터 센터 (Azure 남-동 아시아) 싱가포르 중인 hello 및 hello DR 데이터 센터 홍콩 (Azure 동아시아)입니다.  이 시나리오에서는 싱가포르에서 동기 모드로 SQL Server AlwaysOn을 실행하는 두 VM을 통해 로컬 고가용성을 제공합니다.
* 파일 공유 ASCS hello hello SAP 단일 실패 지점 위한 tooprovide HA 사용된 될 수 있습니다. 파일 공유 ASCS에는 클러스터 공유 디스크가 필요하지 않으며 SIOS 같은 응용 프로그램이 필요하지 않습니다.
* Hello DBMS 계층에 대 한 DR 보호는 비동기 복제를 사용 하 여 수행 됩니다.
* 따라서 hello DR SQL Server 솔루션에서 로컬 고가용성,이 경우 "대칭 DR" – toodescribe 프로덕션의 정확한 복제본에 있는 DR 솔루션을 사용 하는 용어 보여 줍니다. 대칭 DR hello 사용 hello 데이터베이스 계층에 대 한 필수 이며 많은 고객 활용 하 여 클라우드 배포 toobuild 로컬 높은 가용성 노드의 hello 유연성 신속 하 게 DR 이벤트가 발생 한 후 합니다.
* hello 다이어그램에서는 SAP NetWeaver ASCS hello 및 Azure 사이트 복구에서 복제 되는 응용 프로그램 서버 계층에 설명 합니다.

![복제 시나리오](./media/site-recovery-sap/sap-replication-scenario.png)

## <a name="doing-a-test-failover"></a>테스트 장애 조치 수행
에 따라 [이 지침은](azure-to-azure-walkthrough-test-failover.md) toodo 테스트 장애 조치 합니다.

1.  TooAzure 포털 이동한 다음 복구 서비스 자격 증명 모음을 선택 합니다.
2.  SAP 응용 프로그램 (s)에 대해 생성 하는 hello 복구 계획을 클릭 합니다.
3.  '테스트 장애 조치'를 클릭합니다.
4.  복구 지점 및 Azure 가상 네트워크 toostart hello 테스트 장애 조치 프로세스를 선택 합니다.
5.  Hello 보조 환경의 되 면 사용자 유효성 검사를 수행할 수 있습니다.
6.  Hello 유효성 검사가 완료 되 면 클릭 '테스트 장애 조치 정리' 및 tooclean hello 장애 조치 환경입니다.

## <a name="doing-a-failover"></a>장애 조치 수행
장애 조치를 수행할 때 [이 지침](site-recovery-failover.md)을 따릅니다.

1.  TooAzure 포털 이동한 다음 복구 서비스 자격 증명 모음을 선택 합니다.
2.  SAP 응용 프로그램에 대해 생성 하는 hello 복구 계획을 클릭 합니다.
3.  '장애 조치'를 클릭합니다.
4.  복구 지점 toostart hello 장애 조치 프로세스를 선택 합니다.

## <a name="next-steps"></a>다음 단계
[이 백서](http://aka.ms/asr-sap)에서는 Azure Site Recovery를 사용한 SAP NetWeaver 배포에서의 재해 복구 솔루션 구축에 대해 자세히 알아봅니다. hello 백서도 서로 다른 SAP 아키텍처에 대 한 권장 사항에 설명, Azure에서 SAP에 대 한 지원 되는 응용 프로그램 및 VM 유형을 나열 하 고 재해 복구 솔루션에 대 한 가능한 테스트 계획에 설명 합니다.

Site Recovery를 사용하여 [다른 워크로드를 복제](site-recovery-workload.md)하는 것에 대해 알아봅니다.
