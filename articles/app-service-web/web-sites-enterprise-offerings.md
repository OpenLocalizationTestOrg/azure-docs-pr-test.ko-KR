---
title: "aaaAzure 엔터프라이즈에 대 한 앱 서비스 웹 앱 제공"
description: "표시 방법을 업무상 toouse Azure 앱 서비스 웹 앱 toocreate 엔터프라이즈 웹 사이트 솔루션"
services: app-service\web
documentationcenter: 
author: apwestgarth
manager: erikre
editor: 
ms.assetid: cf9ac3b2-0493-4461-8b64-251d3a5cd5b5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: anwestg
ms.openlocfilehash: 5d551509219988160858ff35298d3c7275d1d071
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-apps-offerings-for-enterprise-whitepaper"></a>엔터프라이즈용 Azure 앱 서비스 웹 앱 오퍼링 백서
필요 tooreduce 비용 hello 및 IT 솔루션과 신속 하 게 진화에서 빠르게 배달 환경 개발자, IT 전문가 및 관리자에 대 한 새로운 문제를 만듭니다. 사용자가 자신의 업무 (LOB) 웹 응용 프로그램 toobe 신속 하 고 모든 장치에서 사용할 수 있는 응답을 찾고 점점 더 합니다. Hello에서 같은 시간 기업에 증가 하는 hello 생산성과 효율성 클라우드 및 모바일 서비스와의 통합에서 제공 되는 toocapitalize 시도, Active Directory를 사용 하 여 장치에서 single sign on 만큼 단순할 수 있습니다 데이터를 사용 하 여 office 365에서 toocollaboration 차례로 Salesforce hello 회사 구현에서 데이터를 가져와서 내부 LOB 응용 프로그램에서 찾아볼 수 있습니다. [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)는 웹 및 모바일 응용 프로그램, Web API 및 일반 웹 사이트를 개발, 테스트 및 실행하기 위한 엔터프라이즈급 클라우드 서비스입니다. 사용 되는 toorun 회사 웹 사이트, 인트라넷 사이트, 비즈니스 앱, 수 및 사례 규모 및 연속 통합 및 최신 DevOps에 대 한 지원과 함께 가용성을 위해 최적화 된 데이터 센터의 글로벌 네트워크에서 디지털 마케팅 캠페인 합니다.  

이 백서에서는 hello의 hello 기능 [웹 앱](/services/app-service/web/) 서비스 특히 LOB 웹 응용 프로그램 실행, 기존 웹 응용 프로그램 마이그레이션을 다루는 초점을 및 새 LOB의 배포 웹 hello에 대 한 응용 프로그램 플랫폼입니다.

## <a name="audience"></a>대상
IT 전문가, 설계자 및 온-프레미스를 현재 실행 중인 toomigrate toohello 클라우드 웹 작업을 찾는 관리자입니다. 웹 작업에는 두 비즈니스 tooEmployee 걸쳐 있을 수 있습니다 또는 비즈니스 tooPartners 웹 응용 프로그램입니다.

## <a name="introduction"></a>소개
앱 서비스 웹 앱은 어떤 toohost 외부 및 내부에 이상적인 플랫폼으로 대신 사용자에 게 작용할 비즈니스 가치를 제공 하기 위해 tooconcentrate 수 있도록 하는 비용 효율적인 확장성, 관리 되는 솔루션을 제공 하므로 웹 응용 프로그램 및 서비스 상당한 양의 시간과 비용을 소비 하는 보다 유지 관리 하 고 지 원하는 환경으로 구분 합니다. 웹 앱은 어떤 toodeploy hello 기능 toocontinue tooauthenticate Microsoft Azure Active Directory와 통합을 통해 온-프레미스 Active Directory에 대해 제공 하 여 엔터프라이즈 웹 응용 프로그램 지원의 쉽고 빠르게 유연한 플랫폼을 제공 합니다. 만드는 배포 응용 프로그램 및 인프라 하지에 toofocus 수 있는 관리 되는 플랫폼 모두에 hello 비즈니스 요구 사항-toogrow를 자동으로 조정 하는 동안 프로그램 내부 연속 통합 및 배포 방법, 사용 합니다.

## <a name="problem-definition"></a>문제 정의
hello IT 지형 변경 중임을 신속 하 게 해당 높은 자본 비용에 긴 리드 번 tooone toohandle 부하를 자동으로 확장 되는 서비스의 요청 시 사용을 사용 하 여 기존 서버에 호스트에서 벗어나는 합니다. IT 부서가 문제가 tooreduce hello 비용 및 인프라의 공간 않으며는 또한 민첩성을 증가 시키는 동시 CAPEX 감소에 중점을 둔 지출 유지 관리 합니다. Windows Server 2003과 같이 이전 인프라 플랫폼의 수명 hello 끝 앞에 잠재적인 방식으로 tooavoid 새 장기 자본 비용으로 IT 부서 tooreview 클라우드 마이그레이션 수입니다. Cio 지난 hello에서 다른 부서;에 대 한 구매 결정을 확인 합니다. 그러나 점점 더 CMOs 및 기타 비즈니스 단위 책임자 수행 하 고 그들의 예산 소요 된 방식에 더 활발 한 역할 되며 어떤 hello 투자 수익률 있습니다. 점점 더 많은 비즈니스 필요 자신의 인력 toobe 원격 작업, toosystems 걱정과 액세스 권한이 필요한 고객으로 더 많은 시간을 소비 직원과 자유 어느 때 보다 훨씬 더 많은 모바일.

비즈니스 요구 사항은 월별, 주별, 일별로 변경됩니다. 비즈니스는 타사나 내부에서 제공하는 다양한 새 기능으로 정기적으로 업데이트되는 서비스를 통해 즉각적이고 전 세계적인 확장을 모색하고 있습니다.  일부 경우에는 또한 원하는 hello 기능 tooisolate 응용 프로그램 기업과 하는 동안 tooresources에 액세스 하는 공용 클라우드 기능 사용 합니다. 사용자는 office 365와 같이 자신의 개인 생활에서 여러 서비스를 사용하는 데 더 높은 기대를 가집니다. Toohave 액세스 toosimilar toodate, 해당 작업 수명에 풍부한 서비스 기능을 기대 합니다. 이 요청으로 toocope IT 해야 봐 toohelp hello 비즈니스 tooenable이 선택을 통해 및 제 3 자와의 통합 서비스를 신중 하 게 총 저렴된 한 비용으로 신뢰할 수 있는 되기도 하는 동안 toohello 비즈니스 요구를 사용할 수 있는 플랫폼 선택 소유 합니다.

개발 팀 toodeliver 비즈니스 혜택을 찾고, 기준으로 새 기능을 제공 합니다. 기존 도구와 구현 방법-개발, 테스트에 통합 하는 비용 효율적이 고 신뢰할 수 있는 플랫폼에 대 한 원하는 놓습니다. 고 IT 부서와 함께 작업 배포, 관리 및 가동 중지 시간이 0의 hello 목표와 모든 경고를 자동화 합니다.

<a name="highlevel"></a>
## <a name="high-level-solution"></a>고급 솔루션
웹 플랫폼 및 프레임 워크 점점 더 되 고 toodevelop, 테스트 및 호스트 기간 업무 응용 프로그램을 사용 합니다.  비즈니스 응용 프로그램에서 사용 하는 내부 직원 비용 시스템 등의 일반적인 선으로 종종만 구성 된 웹 응용 프로그램 hello 응용 프로그램과 연결 된 백업 데이터베이스 toostore hello 데이터를 사용 합니다.

앱 서비스 웹 앱은 이러한 응용 프로그램을 호스트하기 적당한 옵션으로, 관리하고 패치 적용할 때 수동 작업과 가동 중지 시간이 거의 없는 확장성과 안정성이 뛰어난 인프라를 제공합니다. hello Microsoft Azure 플랫폼 제공 ClearDB 등 파트너 로부터 서비스 Microsoft Azure SQL 데이터베이스는 관리 되는 확장 가능한 관계형 데이터베이스-as a service, toopopular에서 웹 응용 프로그램에서 여러 데이터 저장소 옵션 toosupport 웹 응용 프로그램 호스트 MySQL 데이터베이스 사용 및 MongoDB 합니다.

또 다른 방법은 toomake 온-프레미스에 대 한 기존 투자를 활용 합니다. Hello 예제 시나리오에서 직원 비용 시스템에서 내부 인프라 내에서 toomaintain에 데이터 저장소를 판독기 수 있습니다. 이 IT 거 버 넌 스 요구 사항 (보고, 급여, 청구 등)의 내부 시스템 또는 toosatisfy와의 통합에 대 한 수 있습니다.  웹 앱에 다양을 한 프레미스 인프라에서 있습니다 tooconnect tooyour를 사용 하도록 설정 하는 방법 제공 합니다.

* [앱 서비스 환경](app-service-app-service-environment-intro.md) -앱 서비스 환경 (ASE)는 새로운 프리미엄 기능 toohello Microsoft Azure 앱 서비스 제품 추가 최근에 있습니다.  ASE는 격리 및 보안 네트워크 액세스를 제공하면서 Azure 앱 서비스 앱을 대규모로 안전하게 실행하는 완전히 격리된 전용 환경을 제공합니다.   
* [하이브리드 연결](../biztalk-services/integration-hybrid-connection-overview.md) – 하이브리드 연결에는 Microsoft Azure BizTalk 서비스의 기능 및 예를 들어 SQL Server, MySQL, 웹 Api 및 사용자 지정 웹 서비스 웹 앱 tooconnect tooon 프레미스 리소스를 안전 하 게 사용 합니다.
* [가상 네트워크 통합](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/) – Azure 가상 네트워크의 웹 응용 프로그램 통합 가능 tooconnect 웹 앱 tooan Azure 가상 네트워크에 있는 설정에는 사이트 간 VPN 통해 프레미스 인프라에 연결 된 tooyour 될 수 있습니다.

hello 다음 다이어그램 표시는 예에서는 상위 수준의 솔루션 프레미스 리소스에 대 한 연결 옵션을 사용 합니다.  hello 첫 번째 예제는 방법을 보여 줍니다 Azure 앱 서비스의 표준 기능을 사용 하 여 수행할 수 있습니다 hello 두 번째로이 수 있는 방법을 보여 줍니다 hello 프리미엄 앱 서비스 환경 기능을 사용 하 여 수행 합니다.

표준 앱 서비스 기능 사용: ![](./media/web-sites-enterprise-offerings/on-premise-connectivity-solutions.png "Using Standard App Service Features")

앱 서비스 환경 사용: ![](./media/web-sites-enterprise-offerings/on-premise-connectivity-solutions-ASE.png "Using an App Service Environment")

## <a name="business-benefits"></a>비즈니스 이점
앱 서비스 웹 앱을 훨씬 더 비용 효율적이 고 hello 비즈니스 요구 사항에 대 한 배달에 agile 함수 toobe 프로그램을 사용 하면 비즈니스 이점을 한 호스트를 제공 합니다.

### <a name="paas-model"></a>PaaS 모델
앱 서비스 웹 앱은 다양한 효율성 및 비용 절감 효과를 제공하는 PaaS(Platform as a Service) 모델을 기반으로 합니다.  더 이상 toospend 시간 Vm 관리, 운영 체제 및 프레임 워크를 패치 적용 해야 합니다. 웹 앱은 toofocus 웹 응용 프로그램 및 하지 Vm의 경우 팀 무료 tooprovide 추가 비즈니스 가치를 유지 관리에 사용할 수 있는 자동으로 패치 환경.

웹 앱의 기본 PaaS 모델 hello hello DevOps 방법론 toofulfill의 실제 사용자 목표를 수 있습니다. 사업적으로 즉, 완전 한 관리 및 hello 응용 프로그램 전체 수명 주기 전체에서 개발, 테스트, 릴리스, 모니터링 및 관리, 및 지원을 포함 한 통합.

Visual Studio Team Services, GitHub, TeamCity, Hudson 또는 BitBucket에서 개발 팀, 연속 통합 및 배포 워크플로 구성할 수 있으며에 대 한 자동화 된 빌드를 사용 하면 테스트 및 배포를 사용 하도록 설정 더 빠르게 릴리스 주기를 감소 하는 동안 기존 인프라에 해제에 관련 된 hello 마찰 합니다. 웹 앱에도 여러 테스트 및 릴리스 워크플로에 대 한 환경 준비 만들기 hello 지원, 더 이상 수행 tooreserve 또는 이러한 목적에 대 한 하드웨어 할당, 원하는 대로 사용자 고유의 프로 모션을 정의 하는 만큼 환경을 만들 수 없습니다. toorelease 워크플로입니다. 사업적으로 있습니다 수 toorelease tooa 테스트 슬롯 소스 제어에서 결정, 수행할 일련의 테스트 완료 되 면 tooa 단계 슬롯을 승격 및 마지막 스왑 tooproduction hello로 중단 시간 없이 추가 된 웹 응용 프로그램에서 호스트 되는 장점 웹 앱을 미리 로드 되어 및 핫 tooprovide hello 최상의 고객 경험 합니다.  Hello toodirect 앱 서비스 웹 앱의 기능을 프로덕션에서 테스트 트래픽 tooa 다른 슬롯의 섹션을 모든 트래픽을 toohello 새 배포를 전환 하거나 모든 트래픽이 되돌리기 전에 hello 변경 사항 검증 기업 하 수는 또한 toohello 이전 배포 합니다.

운영 팀 있음을 확신할 수 웹 응용 프로그램 모니터링 및 경고 기능에 기본 제공 hello로 웹 응용 프로그램에서 호스트를 사용 하 여 hello 최상의 가능한 위치 tooreact tooany 문제에서 되는지 합니다. 운영 팀에서 Microsoft Visual Studio Application Insights, New Relic 및 AppDynamics의 분석 및 모니터링 솔루션에 이미 투자한 경우에는 어떤가요? 이 웹 응용 프로그램 연속성 및 어떤 toomonitor에서 친숙 한 환경을 설정 하는 웹 앱에도 완전히 지원 됩니다.

마지막으로, 웹 응용 프로그램 제공 기능 tooautomatically 앱 및 직접 tooan Azure Blob 저장소 컨테이너 호스트 된 데이터베이스를 백업 합니다. 쉽게과 갖출 재해에서 어떤 toorecover, 복잡 한 프레미스 하드웨어 및 소프트웨어에 필요 hello 감소 하는 매우 비용 효율적인 메서드.

### <a name="ease-of-migration"></a>간편한 마이그레이션
하드웨어 및 운영 체제의 릴리스 주기가 빨라지면서 하드웨어 유지 보수 및 회전이 비즈니스의 주요 문제가 되고 있습니다. 2015의 지원 종료 toohello 생성 되는 Windows Server 2003 R2 서버를 많이 있을 수 있지만 비즈니스에 대 한 키 웹 응용 프로그램을 호스팅 여전히는? 앱 서비스 웹 앱은 해당 웹 응용 프로그램에 어떤 toohost 좋은 후보 및 있습니다 toorationalize hello 비즈니스 하드웨어 자산에 대 한 합니다. 웹 앱 액세스할 수 있도록 tooa 다양 한 관리 및 hello 서비스의 일부로 유지 관리 되는 하드웨어 사양 예산 인프라의 일부로 hello 필요 toofactor 교체 및 관리 비용을 제거 합니다.  마이그레이션은 복사본 처럼 간단 해질 수 및 위치 hello 웹 응용 프로그램 마이그레이션 길잡이 사용 하는 값을 추가 하면 기존 배포 tooWeb 앱 또는 더 복잡 한 마이그레이션 작업에 붙여 넣습니다. 마이그레이션된 웹 응용 프로그램 hello 광범위 한 추가 서비스 toohello 웹 응용 프로그램을 통합 하는 Azure 서비스를 이용할 수 있습니다. 예를 들어 Azure Active Directory toocontrol 액세스 tooyour 기반 응용 프로그램 사용자의 연결 toosecurity 그룹 추가 고려할 수 있습니다. 또 다른 예로 캐시 서비스 tooimprove 성능 추가 하 고 전반적인 더 나은 사용자 환경을 제공 하는 대기 시간을 줄일 수 있습니다.

### <a name="enterprise-class-hosting"></a>엔터프라이즈급 호스팅
Toobe 수 toohandle 입증 되었습니다 하는 신뢰할 수 있는 플랫폼 소형 내부 개발 및 테스트 워크 로드에서 크기가 조정 toohighly 트래픽 혼잡 웹 사이트에서 필요한 다양 한 비즈니스, 앱 서비스 웹 응용 프로그램에 안정적인 제공 합니다. 동일한의 hello 사용 하는 웹 앱을 사용 하 여 호스팅 플랫폼을 높은 값 웹 작업에 대 한 회사는 Microsoft에서 사용 하는 엔터프라이즈 클래스입니다. 보안 및 규정 준수 ISO (ISO/IEC 27001:2005); 등의 규정 요구 사항을으로 hello Azure 플랫폼에서 모든 서비스와 함께 웹 앱 작성 SOC1 및 SOC2 SSAE 16/ISAE 3402 증명, HIPAA BAA, PCI 및 Fedramp hello 매우 핵심 각 요소 및 기능에 대 한 자세한 내용은 참조 하십시오 [http://aka.ms/azurecompliance](/support/trust-center/compliance/)합니다.

Microsoft Azure 플랫폼에서는 역할 기반 권한 부여 컨트롤 엔터프라이즈 수준의 제어 tooresources 웹 응용 프로그램 내에서 사용 하도록 설정 합니다. RBAC 제공 기업 hello 전원 tooimplement 자신의 액세스 관리 정책을 hello Azure 환경에서에서 해당 자산을 모두에 대 한 사용자가 toogroups 할당을 다시 hello 필요한 사용 권한의 웹 같은 hello 자산에 대 한 toothose 그룹 할당 하 여 응용 프로그램입니다. Azure의 RBAC에 대한 자세한 내용은 [http://aka.ms/azurerbac](../active-directory/role-based-access-control-configure.md)를 참조하세요. 웹 앱을 활용하면 웹 응용 프로그램을 안전한 보안 환경에 배포하고 자산이 배포되는 영역을 완벽히 제어할 수 있습니다.

Azure 앱 서비스 환경 [http://aka.ms/aseintro](http://aka.ms/aseintro) 되는 새로운 프리미엄 서비스 계획 옵션 toomake 하려는 기업 고객 Azure 앱 서비스 사용 하며, 이러한 완벽 하 게 격리 되 고 전용 환경을 제공 합니다.  이 통해 사용할 수 있는 매우 높은 비율의 인바운드 및 아웃 바운드 네트워크 트래픽에 대 한 모든 권한을 갖는 하면서 엔터프라이즈 고객 toodeploy 응용 프로그램 및 ASEs 가상를 통해 응용 프로그램 toohave 고속 보안 연결 사용 네트워크 tooon 온-프레미스 리소스입니다.

앱 서비스 웹 앱은 hello 기능 tooconnect 백 tooyour 데이터 웨어하우스 나 SharePoint 환경에 같은 내부 리소스를 제공 하 여도 수 toomake 되어 온-프레미스 투자의 활용 합니다. 에 설명 된 대로 [높은 수준 솔루션](#high-level-solution) 정확해 tooestablish 연결 tooon 하이브리드 연결 및 가상 네트워크 연결을 사용 하 여 프레미스 인프라와 서비스입니다.

### <a name="global-scale"></a>글로벌 환경
앱 서비스 웹 앱 전역 및 확장 가능한 플랫폼은 웹 응용 프로그램 toogrow를 수 있도록 하 고, 최소한의 장기적인 계획으로 신속 하 게 toohello 증가 하는 비즈니스 요구를 조정 하 고, 비용입니다. 프레미스 인프라 시나리오에 일반적인 확장 및 증가 로컬에서 또는 지리적으로 많은 양의 관리, 계획 및 비용 tooprovision 필요한 인프라 및 관리 추가 합니다. 웹 응용 프로그램에서는 hello 기능 tooscale hello ebb 및 요구 사항의 흐름을 사용 하 여 웹 응용 프로그램을 제공합니다. 예를 들어 hello 비용에 따른 응용 프로그램을 사용 하 여 예를 들어, hello 달의 대부분 hello에 대 한 사용자에 게 hello 응용 프로그램의 밝은 사용자 하지만 hello 최종 기한에 도달한 입력 비용 전송 toobe 및 사용에 대 한 각 월 증가 하면 응용 프로그램에 웹 앱에는 hello 기능 tooautomatically 응용 프로그램에 대 한 더 많은 인프라를 프로 비전 없으며 다음 hello 사용 수그러들가 되 면 다시 것 확장할 수 정의한 백 toohello 초기 인프라.

웹 앱은 전 세계 24개 데이터 센터에서 전 세계에서 사용할 수 있으며, 그 수가 늘고 있습니다. 영역 및 위치를 가장 업데이트 hello 목록은 참조 [http://aka.ms/azlocations](http://aka.ms/azlocations)합니다. 웹 앱을 이용하면 기업이 전 세계 범위와 규모를 쉽게 얻을 수 있습니다. 새 영역을 보고 사용 하는 응용 프로그램 대시보드 및 웹 앱에서 호스트 추가 데이터 센터에 쉽게 배포할 수 있습니다 및 웹 앱 및 Azure 트래픽 관리자의 hello 조합 사용 하 여 훨씬 더 신속 하 게 로컬 사용자를 제공 하는 hello로 회사가 커짐에 따라 hello로 모든 추가 된 hello 아래 수 toocontract 되 고 확장 가능한 인프라의 장점 한 변화에 따른 hello 필요한 hello 개 지사를 확장 합니다.

## <a name="solution-details"></a>솔루션 세부 정보
응용 프로그램 마이그레이션 시나리오의 예를 살펴보겠습니다. 앱 서비스 웹 앱 기능 tootogether tooprovide 대형 솔루션 및 비즈니스 가치를 제공 하는 방법의 hello 세부 정보를 설명 합니다.

예제에서는이를 여기에서 설명할 비즈니스 응용 프로그램의 hello 줄은 비용 정산에 대 한 지출이 직원 toosubmit 수 있는 응용 프로그램을 보고 됩니다. hello 응용 프로그램에서 iis 6을 실행 하는 Windows Server 2003 R2 호스팅되고 hello 데이터베이스는 SQL Server 2005 데이터베이스입니다. 끝의 서비스에 대 한 Windows Server 2003 R2 및 SQL Server 2005 들어오는 hello로 이전 버전의 서버에 있는 작용 하며 선택 이유 hello [도구](http://aka.ms/websitesmigration) 및 [지침](http://aka.ms/websitesmigrationresources) tooautomatically를 Azure로 워크 로드를 마이그레이션합니다. 이 점을 염두에서이 예에서 사용 된 hello 패턴 tooa 와이드 확인 하는 마이그레이션 시나리오의 적용 됩니다.

### <a name="migrate-existing-application"></a>기존 응용 프로그램 마이그레이션
단계 1의 전체 hello 기간 업무 응용 프로그램 tooWeb 응용 프로그램을 이동 하기 위한 솔루션은 tooidentify hello 기존 응용 프로그램 자산 및 아키텍처입니다. 이 문서에서 hello 예제는 아래 hello 그림에 나와 있는 것 처럼 hello 데이터베이스는 별도 SQL Server에서 호스트와 단일 IIS 서버에서 호스팅되는 ASP.NET 웹 응용 프로그램입니다. 사용자 이름 및 암호 조합을 사용 하 여 직원 로그인 toohello 시스템 비용의 세부 정보를 입력 하 고 비용의 각 항목에 대 한 hello 데이터베이스로 확인, 스캔 한 복사본을 업로드 합니다.

![](./media/web-sites-enterprise-offerings/on-premise-app-example.png)

#### <a name="items-tooconsider"></a>항목 tooconsider
온-프레미스 환경에서 마이그레이션 응용 프로그램을 들 수 있습니다 tookeep, 웹 응용 프로그램의 몇 가지 제약 조건에 유의 합니다. 응용 프로그램 tooWeb 앱을 웹 마이그레이션할 때 인식 일부 주요 항목 toobe 같습니다 ([http://aka.ms/websitesmigrationresources](http://aka.ms/websitesmigrationresources)):

* 포트 바인딩 - 웹 앱은 HTTP 트래픽에는 포트 80, HTTPS 트래픽에는 포트 443만 지원합니다. 응용 프로그램이 다른 포트를 사용 하는 경우 HTTP에 포트 80 사용 하 고 포트 443을 HTTPS 트래픽에 대 한 후 한 번 마이그레이션된 hello 응용 프로그램 생성 됩니다. 이것은 종종 무해 한 문제에는 일반적으로 프레미스 배포 toomake 특히 개발 및 테스트 환경에서에서 도메인 이름의 순서 tooovercome hello 사용 중인 다른 포트를 사용 하는 대로
* 인증 - 웹 앱은 익명 인증을 기본 지원하고 응용 프로그램에서 지정한 경우 폼 인증도 지원합니다. 웹 앱만 hello 응용 프로그램이 Azure Active Directory 및 ad FS와 통합 되어 있을 때 Windows 인증을 제공할 수 있습니다. [여기](http://aka.ms/azurebizapp)
* GAC 어셈블리 기반-웹 응용 프로그램 어셈블리 toohello 전역 어셈블리 캐시 (GAC)의 hello 배포를 허용 하지 않습니다. 따라서 hello 응용 프로그램 마이그레이션 중인 경우 활용이 온-프레미스 기능을 hello 응용 프로그램의 이동 hello 어셈블리 toohello bin 폴더는 것이 좋습니다.
* IIS5 호환 모드-웹 응용 프로그램 IIS5 호환 모드를 지원 하지 않습니다 및 각 웹 응용 프로그램 인스턴스 및 모든 웹 응용 프로그램 hello 부모에서 인스턴스를 실행 하는 웹 응용 프로그램에서 단일 응용 프로그램 풀에서 작업자 프로세스를 같은 hello 그렇게 합니다.
* COM 라이브러리-웹 응용 프로그램을 사용 하 여 hello 플랫폼의 COM 구성 요소 hello 등록을 허용 하지 않습니다. 따라서 hello 응용 프로그램의 모든 COM 구성 요소를 사용 하는, 경우 이러한 해야 toobe 관리 코드로 다시 작성 하 고 hello 응용 프로그램과 함께 배포 합니다.
* ISAPI 필터 – 웹 앱에서 ISAPI 필터를 지원할 수 있습니다. Toobe hello 응용 프로그램의 일부분으로 배포 하 고 hello 웹 응용 프로그램의 web.config 파일에 등록 해야 합니다. 자세한 내용은 [http://aka.ms/azurewebsitesxdt](web-sites-transform-extend.md)을 참조하세요.

이러한 항목으로 간주 되 면 웹 응용 프로그램 클라우드 hello에 대 한 준비가 됩니다. 걱정 일부 항목을 완벽 하 게 충족 되지 않는 hello 마이그레이션 도구 최선의 노력 toomigration 지정 됩니다.

hello 마이그레이션 프로세스의 다음 단계를 hello은 toocreate 앱 서비스 웹 앱 및 Azure SQL 데이터베이스입니다. Tooselect 웹 응용 프로그램 요구 사항에 따라 사용할 수 있는 다양 한 CPU 코어 수와 RAM 금액을 사용 하 여 웹 응용 프로그램 인스턴스는 여러 크기 있습니다. 자세한 정보 및 가격은 [https://azure.microsoft.com/pricing/details/app-service/](https://azure.microsoft.com/pricing/details/app-service/)를 참조하세요. 마찬가지로, Microsoft Azure SQL 데이터베이스는 다양 한 서비스 계층에 비즈니스 요구의 tooall 하 고 성능 수준이 toofulfill 요구 사항입니다. 자세한 정보는 [https://azure.microsoft.com/pricing/details/sql-database/](https://azure.microsoft.com/pricing/details/sql-database/)를 참조하세요. 를 만든 후 hello 응용 프로그램은 FTP 또는 WebDeploy 통해 업로드 tooApp 서비스 웹 앱 하 고 hello 데이터베이스로 이동 합니다.

이 마이그레이션 hello 솔루션 Azure SQL 데이터베이스 있지만 실제로 hello만 데이터베이스가 아니라 Azure에서 지원 되는 사용 합니다. 회사의 MySQL, MongoDB, Azure Cosmos DB 및 hello를 구입할 수 있는 추가 기능을 통해 더 많은 사용 하 여 만들 수도 [Azure Store](/marketplace/partner-program/)합니다.

Azure SQL 데이터베이스는 여러 옵션을 만들 때 사용할 수 있는 tooimport에서 기존 데이터베이스 toousing hello에 대 한 스크립트를 생성 하는 온-프레미스 서버에서 기존 데이터베이스를은 [데이터 계층 응용 프로그램 내보내기 및 가져오기](http://aka.ms/dacpac) .

SQL Server Management Studio를 사용 하 여 toohello 데이터베이스 연결을 새 Azure SQL 데이터베이스를 만들어 hello 비용에 따른 응용 프로그램 데이터베이스를 만든 및 스크립트 toobuild를 실행 한 다음 데이터베이스 스키마를 hello hello 온-프레미스에서 데이터를 채웁니다. 데이터베이스입니다.

hello hello 마이그레이션의이 첫 번째 단계에서는 최종 단계 hello를 업데이트 해야 hello 응용 프로그램에 대 한 연결 문자열 toohello 데이터베이스입니다. Hello Azure 포털을 통해이 작업을 수행할 수 있습니다. 각 웹 앱에 대 한 응용 프로그램별 설정, 사용 중인 hello 응용 프로그램 tooconnect tooany 데이터베이스에서 사용 중인 모든 연결 문자열을 포함 하 여 수정할 수 있습니다.

### <a name="alternatives-toousing-azure-sql-database"></a>대안 toousing Azure SQL 데이터베이스
hello Azure 플랫폼 제안 다양 한 대안 toousing 웹 응용 프로그램 주 데이터베이스와 Azure SQL 데이터베이스, 즉,이 tooenable 다양 한 작업 데이터를 비즈니스 NoSQL 솔루션 또는 tooenable hello 플랫폼 toosuit 활용 합니다. 예를 들어 비즈니스 오프 사이트 또는 공용 클라우드 환경에서 저장 되지 않아야 하는 데이터를 보유할 수 있습니다 및 따라서 toomaintain hello 사용 하 여 자신의 온-프레미스 데이터베이스의 유사할 것입니다.

#### <a name="connectivity-tooon-premises-resources"></a>연결 tooOn 프레미스 리소스
앱 서비스 웹 앱은 기존 귀중 인프라의 재사용을 사용 하도록 설정 데이터베이스와 같은 tooon 프레미스 리소스에 연결 하기 위한 여러 옵션을 제공 합니다. 아래에 나열 된 hello 옵션은입니다.

* 따라서 hello 환경 toocommunicate 개인 끝점으로 사용 하도록 설정 내에 있는 hello 동일, 앱 서비스 환경 격리 되며 가상 네트워크의 서브넷 내에서 만든 가상 네트워크- [http://aka.ms/appserviceasenetworking](http://aka.ms/appserviceasenetworking)
* 웹 앱 가상 네트워크 통합 웹 응용 프로그램 간의 통합을 지원 하 고 수 있도록 하는 Azure 가상 네트워크를 사이트 간 VPN으로 tooyour 프레미스 네트워크에 연결 하는 경우 연결을 허용 하는 가상 네트워크에서 실행 중인 tooresources 액세스 내부 시스템에서 직접 tooyour 합니다.
* 하이브리드 연결은 Azure BizTalk 서비스의 기능 및 SQL Server, MySQL, HTTP 웹 Api 및 대부분의 사용자 지정 웹 서비스 등는 쉽게 tooconnect tooindividual 온-프레미스 리소스를 제공 합니다.

#### <a name="scale-and-resiliency"></a>크기 조정 및 복원력
업무 하므로 합병 또는 자연 유기적 증가 통해 해당 리소스가 증가 따라 너무 웹 응용 프로그램을 확장 해야 toomeet 이러한 새 요구 합니다. 실제로 오늘 일반적인 toosee는 더 높은 여러 위치에 배치 팀과 원격 직원의 되, 예를 들어 hello 미국, 유럽 및 아시아, 더 많은 지역에서 잦은 영업 직원으로 지사가 회사. 웹 앱을 사용 소수 자릿수를 편리 하 고 자동으로 hello 기능 toohandle 탄력적 변경 되었습니다.

앱 서비스 웹 앱에 웹 응용 프로그램 구성 toobe tooscale hello 두 벡터-시간 또는 CPU 사용 하 여 예약에 따라 Azure 포털을 통해 자동으로 허용 합니다. 큰 변경 우리의 비용 시스템 toomarketing 웹 사이트의 경우 트래픽 버스트 발생 하는 보고와 같은 웹 응용 프로그램에서 모든 비즈니스 응용 프로그램에 대 한 사용량에 대 한 비용 효율적인 매우 유연한 방식으로 toocater 제공 웹 응용 프로그램 자동 크기 조정 에 대 한 프로 모션의 짧은 기간입니다. 자세한 정보 및 웹 응용 프로그램을 사용 하 여 웹 응용 프로그램 크기 조정에 대 한 지침을 참조 하세요. [어떻게 tooScale 웹 사이트](web-sites-scale.md)합니다.

또한 웹 응용 프로그램의 크기 조정 유연성 toohello hello 여러 데이터 센터 및 지리적 지역에서 전체 플랫폼 수 있도록 비즈니스 연속성 솔루션 및 웹 응용 프로그램 및 해당 자산 hello 가능한 배포를 통해 복구 기능을 합니다.

## <a name="summary"></a>요약
앱 서비스 웹 앱은 비용 효율적이 고 응답성이 뛰어난 유연한 솔루션 toohello 동적 비즈니스 요구에 빠르게 발전 하 고 환경에 제공합니다. 웹 앱은 최신 DevOps 기능을 포함하고 수동 관리를 줄이는 관리되는 플랫폼을 활용하여 생산성과 효율성을 늘릴 뿐 아니라 크기 조정, 복원력, 보안 및 온-프레미스와의 통합 면에서 엔터프라이즈급 기능을 제공합니다.

## <a name="call-tooaction"></a>TooAction 호출
Hello Azure 앱 서비스 웹 앱 서비스에 대 한 자세한 내용은 방문 [http://aka.ms/enterprisewebsites](/services/websites/enterprise/) 자세한 내용은 기반 할 수 있습니다 하 고 서명 하는 위치에 지금 평가판에 대해 [https://azure.microsoft.com/ 가격 책정/무료 평가판 /](https://azure.microsoft.com/pricing/free-trial/) tooevaluate 서비스 hello 및 비즈니스에 대 한 hello 혜택을 검색 합니다.

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]
