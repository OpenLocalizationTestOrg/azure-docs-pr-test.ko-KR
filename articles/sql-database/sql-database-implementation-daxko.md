---
title: "SQL 데이터베이스 Azure 사례 연구-aaaAzure Daxko/CSI | Microsoft Docs"
description: "해당 고객 서비스 및 성능 개발 주기 및 tooenhance Daxko/CSI tooaccelerate SQL 데이터베이스를 사용 하는 방법에 대해 알아봅니다"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 00c8a713-f20c-4d6b-b8b7-0c1b9ba5f05b
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 3e3d58a1d9c3c919fc0e4cdb2765f680719c19d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="daxkocsi-used-azure-tooaccelerate-its-development-cycle-and-tooenhance-its-customer-services-and-performance"></a>Daxko/CSI 정의와 개발 주기 및 tooenhance Azure tooaccelerate 사용 되는 해당 고객 서비스 및 성능
![Daxko/CSI 로고](./media/sql-database-implementation-daxko/csidaxkologo25.png)

Daxko/CSI 소프트웨어 직면 과제: 적합성 및 오락 센터의 해당 고객 기반 급성장는 포괄적인 엔터프라이즈 소프트웨어 솔루션의 감사 toohello 성공 했지만 해당 증가에 따라 필요한 IT 인프라 hello와 동기화 고객 기반 hello 회사의 테스트 된 IT 직원입니다. hello 회사가 점점 증가 하는 데이터베이스 관리를 위한 특히 상승 작업 오버 헤드에 의해 제한 됩니다. 더 심한 경우 해당 작업 오버 헤드 hello 기업의 소프트웨어에 대 한 새로운 모바일 기능와 같은 새로운 이니셔티브 개발 리소스에 잘라내기 되었습니다.

TooDavid Molina에 따라, Daxko/CSI에서 감독의 제품 개발, toosimplify 데이터베이스 관리 필요 하다는 hello 플랫폼으로-서비스 (PaaS) 모델에 제공 된 Azure CSI 소프트웨어 확장성을 개선 및 리소스 toofocus에 확보 ops 대신 소프트웨어입니다. "Azure SQL 데이터베이스는 우리에게 아주 유용한 선택 옵션이었습니다. SQL Server, 장애 조치 클러스터 및 모든 hello를 유지 관리 하는 방법에 대 한 tooworry 다니지 않아도 다른 인프라 요구 했습니다 us에 적합 합니다. "

이후 tooAzure 마이그레이션, CSI 소프트웨어 필요한 두 개의 toomanage 운영 담당자는 600 고객 데이터베이스에 대해 합니다. hello 회사 toomove 고객 데이터베이스 크기에 따라와 필요한 Azure SQL 데이터베이스 탄력적 풀을 사용 합니다.

Molina 계속 되 면 "고객 즉시 변경 hello을 더 쉬워집니다. 탄력적 풀 이전에는 버스트 기간 동안 제한 시간 및 기타 문제가 가끔씩 발생했습니다. Azure 탄력적 풀과 수 필요에 따라 전환 하 고 hello 소프트웨어 문제 없이 사용 하 여. "

또한 고객에 대 한 tooimproving 성능, Azure 탄력적 풀 해제 CSI 소프트웨어 리소스를 새로운 서비스 및 기능, 운영 및 관리를 처리 하는 대신 개발에 toofocus. 이러한 IT 리소스는 CSI 소프트웨어 제공을 SpectrumNG, toohelp 해당 엔터프라이즈 소프트웨어를 개선 하는 데 도움을 준. gym 멤버 참여 직원 효율성을 개선 하 고 대화형 작업 및 실시간 알림을 대 한 직원 및 멤버 모바일 액세스 권한을 부여 합니다.

또한 azure CSI 소프트웨어를 가속화 하 고 자동화 옵션을 사용 하 여 hello 개발 및-QA (품질 보증) 주기를 개선 있었습니다. Hello 회사의 Azure 구현 빌드 관리자 구성 요소는 단추의 hello 클릭으로 패키징할 수 있습니다. "Hello 릴리스 주기의 일환으로, QA은 이제 수 toodeploy tooa 테스트 환경 우리의 프로덕션 스택 가깝게 모방가 Azure에서 Molina의 설명에 따라. Tooour 개발 환경 toovet 변경 즉시 빌드를 배포할 수 있습니다. 이전에는 테스트를 위한 이러한 공간이 없었으므로 이점은 큰 도움이 되었습니다."라고 Molina는 설명했습니다.

## <a name="offloading-toohello-cloud"></a>Toohello 클라우드 오프 로드
Toohello 클라우드를 이동 하기 전에 CSI 소프트웨어 Houston에서 로컬 데이터 센터에서 다중 테 넌 트 인프라 성공적으로 작성 해야 했습니다. 으로 hello 회사 확장 구매 프로비저닝과 hello 하드웨어를 유지 관리에서 늘어나는 작업 증가 처리 하 고 소프트웨어 필요 toosupport 고객 합니다. IT 직원 toohandle 운영에 새 리소스를 프로 비전 하 고 새 서비스 toocustomers 롤아웃하기 tooa 저하 시킨 다른 병목 상태가 되었습니다.

CSI Software에서는 이러한 오버헤드를 없애고 작업 자체가 아닌 코드에 집중할 수 있도록 하기 위한 클라우드 옵션을 알아보게 되었습니다. hello 회사 발견 hello 상위 클라우드 공급자의 많은 큰 IT 직원 toomanage hello IaaS 스택을 계속 해야 하는 인프라-as a service (IaaS) 솔루션만 제공 합니다. Hello 끝 CSI 소프트웨어 hello Azure PaaS 솔루션 요구 사항에 적합 한 최상의 hello 되었는지 확인 합니다. Molina의 설명에 "Azure 가져옵니다 hello 방식을 hello 하드웨어 및 시스템 소프트웨어는 IT 오버 헤드를 줄이는 동시 소프트웨어 제공을에 집중할 수 있습니다."

## <a name="making-hello-transition-tooazure"></a>Hello 전환 tooAzure 만들기
Azure는 PaaS 솔루션을 선택한 후 CSI 소프트웨어 백 엔드 인프라 및 데이터베이스 toohello 클라우드 마이그레이션 시작 했습니다. 이전 tooAzure SpectrumNG 고객 tooinstall hello 백 엔드에서 Windows Communication Foundation (WCF) 서비스와 통신 하는 클라이언트 응용 프로그램을 필요 합니다. TooMolina에 따라 "일부 고객이 자신의 데이터 센터에서 모든 항목을 호스트 하는 있지만 빌드 했습니다 hello 제품 toobe 다중 테 넌 트 아웃 합니다. म 호스트 휴스턴의 데이터 센터에 있는 모든 것 hello 데이터 저장소로 SQL Server를 사용 합니다.

"우리의 제품 제공도 포함 멤버 용 웹 포털 (ASP.net으로 작성)가 디자인 된 toobe 흰색 레이블 toomatch hello 고객의 웹 사이트 및 SOAP API toosupport hello 온라인 페이지 및 다른 공급 업체의 통합이 포함 됩니다."

hello 마이그레이션 toohello 클라우드 긴 하지 않는데 hello 아키텍처에 대 한 합니다. TooMolina에 따라, "hello 대부분의 hello 노력은 해결 config 파일 정보를 중앙 집중식된 연결 문자열 수정 읽는 및 패키징, 업로드, 및 우리의 릴리스 배포 hello 자동화 hello 방식을 수정 합니다."

toodevelop hello 자동화 기능을 작성할 Azure PowerShell을 사용 하는 CSI 소프트웨어 엔지니어 및 REST Api toocreate 패키지 하 고 tooa 매일 밤 릴리스에 대 한 스테이징 환경에 업로드 합니다.
hello 전체 전환 tooan Azure의 클라우드 기반 배포 오류가 발생 했습니다. 신속 하 고 원활 하 게 hello CSI 소프트웨어 IT 팀에 대 한 합니다. Molina의 설명에 "모두 했습니다 베타 환경 hello 클라우드에서 hello 프로젝트에 대 한 수행의 3 toofour 주 이내입니다. 정말 놀라운 성과였습니다.”라고 Molina는 설명했습니다.

CSI 소프트웨어 구성 및 테스트 환경 hello, 후 마이그레이션 시작 된 고객 합니다. CSI 소프트웨어 호스팅를 이미 사용 하 여 고객에 대 한 hello 전환 거의 원활 하 게 했습니다. 고객 온-프레미스 배포에서 마이그레이션에 대 한 hello 마이그레이션 toohello 클라우드 추가 약간의 시간이 걸립니다 했지만 주로 계속 고객과 CSI 소프트웨어에 대 한 간편한 합니다.

새 고객에 대 한 CSI 소프트웨어의 IT 직원이 사용 하 여 hello 프로세스 tooon 보드 다음 해당 tooAzure:

1. Azure PowerShell 스크립트는 hello 고객;에 대 한 새 데이터베이스를 사용 하는 toospin 모든 고객 시작 프리미엄 계층 tooensure에 hello 전환에 대 한 초기 처리량 충분 합니다.
2. 가능 하면 CSI 소프트웨어 hello Azure 마이그레이션 마법사가 SQL toomove 기존 데이터 tooan Azure SQL 데이터베이스 인스턴스를 사용 합니다.
3. 마지막으로, Microsoft SQL Server Integration Services (SSIS)는 사용 되는 tooreconcile hello 데이터 또는 tooperform 불일치도 모든 데이터 정리 작업에 필요 합니다.

현재, CSI Software 고객의 약 99%가 4개의 지역 데이터 센터(중북부, 중남부, 동부, 서부)에 있는 Azure에 호스트되고 있습니다. 각 고객의 지리적 지역에 데이터 센터를 포함 하면 대기 시간이 유지 tooa 최소.

## <a name="azure-elastic-pools-free-up-it-resources"></a>Azure 탄력적 풀로 IT 리소스 확보
Azure의 몇 가지 기능 CSI 소프트웨어 드린 shift 인프라 및 작업 포커스가 toobeing 기능 및 개발 초점을 맞춘 못하게 합니다. 아마도 가장 큰 장점은 hello 탄력적 풀에서 되었습니다.

CSI Software는 현재 고객에게 약 550개의 데이터베이스를 제공합니다. 탄력적 풀, 전에 어려운 toomanage 내의 많은 데이터베이스는 계층 구조입니다. Ops 관리자는 중요 한 IT 리소스 오버 헤드가 필요한 고객의 hello 버스트 요구에 따라 tooassign 성능 계층에 있습니다. 탄력적 풀을 사용하면서 관리자들은 테넌트에 프리미엄 또는 표준 풀을 적절히 할당한 다음 크기 및 필요에 따라 고객을 이동할 수 있습니다. 거의 즉시 더 쉬워집니다 hello 탄력적 풀의 hello 효과 고객 탄력적 풀, 하기 전에 고객 버스트 사용 기간 동안 시간 초과 및 기타 문제 들 이지만 탄력적 풀과 필요에 따라 고객에 게 활동 버스트 발생할 수 있습니다 하 고 toouse SpectrumNG 문제 없이 계속 할 수 있습니다.

## <a name="azure-active-geo-replication-accelerates-reporting"></a>Azure 활성 지역 복제로 보고 기능 가속화
일부 CSI Software 고객은 Azure 활성 지역 복제도 활용하고 있습니다. 활성 지리적 복제 toofour를 읽기 가능한 보조 데이터베이스를 구성할 수 hello에 같거나 다른 데이터 센터 지역입니다. CSI 소프트웨어에서는 두 가지 방법으로 활성 지리적 복제를 활용: hello 보조 데이터베이스는 데이터 센터 가동 중단 또는 hello 불가능 tooconnect toohello 주 데이터베이스의; hello 사례에서 사용할 수 있는 첫째, 및 둘째, hello 보조 데이터베이스는 읽을 수 있는 사용된 toooffload 작업 보고와 같은 읽기 전용 작업 될 수 있습니다. 일부 CSI 소프트웨어 고객 사용이 혜택 tooaccelerate 워크플로 보고 합니다.

## <a name="csi-software-application-logic-and-architecture"></a>CSI Software 응용 프로그램 논리 및 아키텍처
SpectrumNG에서는 웹 역할을 사용합니다. Hello 응용 프로그램을 다중 테 넌 트 때문에 WCF 서비스는 고객의 사용 되는 toohandle hello 초기 연결 요청입니다. Molina 상태를 "hello 요청 식별 한 다음에 게는 us 연결 문자열을 작성할 tootheir 데이터베이스 toodo 아웃 필요 무엇이 든 각 고객 toodo."

해당 서비스의 웹 계층의 hello 경우 CSI 소프트웨어 활용 Azure 자동 크기 조정, 날짜와 시간에 따라 합니다. 사용 가능한 리소스에는 업무 시간 동안 각 지역의 데이터 센터의 toohello 표준 시간대에 따라 자동으로 증가 tooaccommodate 더 높은 사용 합니다. 리소스 tooscale 때 고객의 요구 사항 우선 순위가 더 낮은 주말에 설정도 됩니다.

![Daxko/CSI 아키텍처](./media/sql-database-implementation-daxko/figure1.png)

그림 1. 클라우드 서비스 작업자 역할은 Azure SQL 데이터베이스에서 구조화된 데이터를 가져오고, 테이블 저장소에서 반구조화된 데이터를 가져옵니다. SpectrumNG 사용자는 클라우드 데이터 서비스 웹 역할을 통해 해당 데이터와 상호 작용합니다.

## <a name="using-web-apps-and-a-web-plan-tier-for-mobile-apps"></a>모바일 앱에 대해 웹앱 및 웹 계획 계층 사용
전체 모바일 플랫폼을 포함 하 여 새 initiatives tooenable CSI 소프트웨어에 대 한 리소스를 해제 하는 Azure SQL 데이터베이스를 사용 하 여 Azure 웹 앱에서 호스트 되는 사용자 지정 API에 따라. hello 플랫폼 gym 구성원 수 및 직원 toouse 모바일 장치 toocheck 일정 클래스, 예약 및 메시지를 수신 합니다.

hello 플랫폼 사용 하 여 서비스 지향 아키텍처 (SOA) tootake 단일 구성 — 판매 시점 관리 시스템 (POS),는 판매 시스템 등의-hello 즉석 tooanother 웹 플랜에서 이동한 후 스핀업 서비스 toosupport 해당 구성 요소에 있는 다른 모든 항목을 그대로 유지 하면서 hello 원래 웹 계획 합니다. 이 기능은 CSI Software에 놀라운 유연성을 제공하고, 비용 절감에도 도움을 줍니다.

## <a name="azure-lets-csi-software-developers-focus-on-apps-and-services"></a>Azure를 통해 CSI Software 개발자가 앱 및 서비스에 집중
Azure SQL 데이터베이스가 아닌 hello 신속 하 고 신뢰할 수 있는 서비스를 이용할 수 있는 boon tooSpectrumNG 고객 방금 CSI 소프트웨어에 대 한 큰 장점은 이기도 IT 직원 및 개발자가 있습니다. Hello 클라우드에서 ops tooAzure에 오프 로드 CSI 소프트웨어 리소스 및 인프라에 대 한 오버 헤드가 감소, 해당 개발 주기를 가속화할 및 더 이상 필요 없는 toomicromanage 데이터베이스 toooptimize 성능 해당 테 넌 트에 대 한 합니다.

## <a name="more-information"></a>자세한 정보
* Azure 탄력적 풀에 대해 자세히 toolearn 참조 [탄력적 풀](sql-database-elastic-pool.md)합니다.
* 데이터베이스 도구 및 탄력적인 크기 조정에 대해 자세히 toolearn 참조 [탄력적 데이터베이스 도구 및 탄력적인 크기 조정을](sql-database-elastic-scale-get-started.md)합니다.
* SQL Server 데이터베이스 마이그레이션에 대 한 더 toolearn 참조 참조 [SQL Server 데이터베이스 tooAzure 마이그레이션할](sql-database-cloud-migrate.md)합니다.
* 활성 지리적 복제에 대해 자세히 toolearn 참조 [활성 지리적 복제](sql-database-geo-replication-overview.md)합니다.
* 웹 역할 및 작업자 역할에 대해 자세히 toolearn 참조 [작업자 역할](../fundamentals-introduction-to-azure.md#compute)합니다.    
* Azure 서비스 버스에 대 한 자세한 toolearn 참조 [Azure 서비스 버스](https://azure.microsoft.com/services/service-bus/)합니다.
* 자동 크기 조정에 대 한 자세한 toolearn 참조 [클라우드 서비스 크기 조정](../cloud-services/cloud-services-how-to-scale.md)합니다.

