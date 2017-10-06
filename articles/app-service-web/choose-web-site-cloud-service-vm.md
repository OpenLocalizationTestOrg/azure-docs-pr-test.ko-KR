---
title: "앱 서비스, 가상 컴퓨터, 서비스 패브릭 및 클라우드 서비스 비교 aaaAzure | Microsoft Docs"
description: "자세한 내용은 방법 Azure 앱 서비스, 가상 컴퓨터, 서비스 패브릭 및 호스팅에 대 한 클라우드 서비스 간에 toochoose 웹 응용 프로그램입니다."
services: app-service\web, virtual-machines, cloud-services
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 7d346a23-532a-42a9-98a8-23b7286d32a8
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 07/07/2016
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 7577332ed049df66178c7b2cd5c440a7f93a7865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-virtual-machines-service-fabric-and-cloud-services-comparison"></a>Azure App Service, 가상 컴퓨터, Service Fabric 및 Cloud Services 비교
## <a name="overview"></a>개요
Azure에서는 여러 가지 방법을 toohost 웹 사이트: [Azure 앱 서비스][Azure App Service], [가상 컴퓨터][Virtual Machines], [서비스 패브릭 ] [ Service Fabric], 및 [클라우드 서비스][Cloud Services]합니다. 이 문서를 사용 하 여 hello 옵션을 이해 하 고 웹 응용 프로그램에 대 한 hello 올바른 선택을 확인 수 있습니다.

Azure 앱 서비스는 hello 대부분의 웹 응용 프로그램에 적합 합니다. 배포 및 관리 hello 플랫폼에 통합 되어, 사이트 신속 하 게 toohandle 트래픽 부하를 확장할 수 있고 hello 기본 제공 부하 분산 및 트래픽 관리자는 고가용성을 제공 합니다. 앱 서비스 tooAzure 사이트 기존 이동할 수 있습니다으로 쉽게는 [온라인 마이그레이션 도구](https://www.migratetoazure.net/)hello 웹 응용 프로그램 갤러리에서에서 오픈 소스 응용 프로그램을 사용 하 여, 또는 hello 프레임 워크 및 사용자가 원하는 도구를 사용 하 여 새 사이트를 만듭니다. hello [WebJobs] [ WebJobs] 쉽게 tooadd 백그라운드 작업 처리 tooyour 앱 서비스 웹 앱 기능을 사용 합니다.

새 응용 프로그램을 만들거나 기존 응용 프로그램을 다시 작성 하는 경우 서비스 패브릭이 좋은 대안 toouse 마이크로 서비스 아키텍처. 에 컴퓨터의 공유 풀에서 실행 되는 앱 수 작은 항목부터 시작 하 고 toomassive 눈금으로 수백 또는 수천 대 컴퓨터 필요에 따라 증가 합니다. 상태 저장 서비스 쉽게 tooconsistently 확인 및 응용 프로그램 상태가 안정적으로 저장 하 고 서비스 패브릭 자동으로 관리 서비스 분할 배율 및 가용성 드립니다.  Service Fabric은 OWIN(Open Web Interface for .NET) 및 ASP.NET Core를 사용하여 WebAPI를 지원합니다.  또한 비교 tooApp 서비스 패브릭 서비스를 제어할 수를 늘리거나 hello 기본 인프라에 대 한 직접 액세스를 제공합니다. 서버로 원격으로 연결하거나 서버 시작 작업을 구성할 수 있습니다. 클라우드 서비스는 비슷한 tooService 일정 정도의 제어 및 사용 편리성을에서 패브릭 하지만 이제 레거시 서비스 및 서비스 패브릭 새로운 개발에 대 한 것이 좋습니다.

앱 서비스 또는 서비스 패브릭에서 toorun 상당한 수정 해야 하는 기존 응용 프로그램의 경우 toohello 클라우드 마이그레이션 순서 toosimplify에 가상 컴퓨터를 선택할 수 있습니다. 그러나 올바르게 구성 안전 하 게 유지 하 고 Vm을 유지 관리에 훨씬 더 많은 시간이 필요 하며 IT 전문 지식을 비교 tooAzure 앱 서비스 및 서비스 패브릭. Azure 가상 컴퓨터를 고려 하는 경우 계정 hello 지속적인 유지 관리가 필요한 노력 toopatch 고려 있는지 확인 업데이트 하 고, VM 환경을 관리 합니다. Azure 가상 컴퓨터는 IaaS(Infrastructure-as-a-Service)이지만 App Service 및 Service Fabric은 PaaS(Platform-as-a-Service)입니다. 

## <a name="features"></a>기능 비교
앱 서비스의 hello 기능을 비교 하는 다음 표에 hello, 클라우드 서비스, 가상 컴퓨터 및 서비스 패브릭 toohelp hello 최선의 선택 하 게 합니다. 각 옵션에 대 한 SLA hello에 대 한 현재 정보를 참조 하십시오. [Azure 서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)합니다.

| 기능 | App Service(웹앱) | Cloud Services(웹 역할) | 가상 컴퓨터 | Service Fabric | 참고 사항 |
| --- | --- | --- | --- | --- | --- |
| 빠른 배포 |X | | |X |응용 프로그램 또는 응용 프로그램 업데이트 tooa 클라우드 서비스를 배포 하거나 VM을 만드는 몇 분 정도 걸립니다; 이상 응용 프로그램 tooa 웹 응용 프로그램 배포 초가 걸립니다. |
| 재배포 하지 않고 toolarger 컴퓨터를 크기 조정 |X | | |X | |
| 웹 서버 인스턴스가 콘텐츠 및 tooredeploy 했거나 크기를 조정 다시 구성 하지 않는 것을 의미 하는 구성을 공유 합니다. |X | | |X | |
| 여러 배포 환경(프로덕션 및 스테이징) |X |X | |X |서비스 패브릭 toohave을 사용 하면 응용 프로그램 또는 사용자 응용 프로그램-side-by-side의 toodeploy 서로 다른 버전에 대 한 여러 환경입니다. |
| 자동 OS 업데이트 관리 |X |X | | |자동 OS 업데이트는 향후 Service Fabric 릴리스에서 제공될 예정입니다. |
| 원활한 플랫폼 전환(32비트와 64비트 간을 쉽게 이동) |X |X | | | |
| GIT, FTP를 사용하여 코드 배포 |X | |X | | |
| 웹 배포를 사용하여 코드 배포 |X | |X | |클라우드 서비스는 hello를 사용 하 여 웹 배포 toodeploy 업데이트 tooindividual 역할 인스턴스를 지원 합니다. 그러나는 역할의 초기 배포를 위해 사용할 수 없습니다 및 웹 배포를 사용 하 여 업데이트 하기 위해 받은 toodeploy 별도로 tooeach 역할 인스턴스가 있습니다. 프로덕션 환경에 대 한 클라우드 서비스 SLA hello에 대 한 순서 tooqualify 여러 인스턴스가 필요 합니다. |
| WebMatrix 지원 |X | |X | | |
| 서비스 버스, 저장소, SQL 데이터베이스와 같은 액세스 tooservices |X |X |X |X | |
| 다중 계층 아키텍처의 웹 또는 웹 서비스 계층 호스트 |X |X |X |X | |
| 다중 계층 아키텍처의 중간 계층 호스트 |X |X |X |X |앱 서비스 웹 앱 수 쉽게 REST API 중간 계층을 호스트 하 고 hello [WebJobs](http://go.microsoft.com/fwlink/?linkid=390226) 기능 백그라운드 처리 작업을 호스트할 수 있습니다. Hello 계층에 대 한 전용된 웹 사이트 tooachieve 독립 확장성에서 WebJobs을 실행할 수 있습니다. hello 미리 보기 [API 앱](../app-service-api/app-service-api-apps-why-best-platform.md) 기능은 REST 서비스를 호스팅하기 위한 더 많은 기능을 제공 합니다. |
| 통합된 MySQL-as-a-Service 지원 |X |X |X | |클라우드 서비스는 hello Azure 포털 워크플로의 일부로 하지 않지만 ClearDB의 제품을 MySQL-as a service를 통합할 수 있습니다. |
| ASP.NET, 클래식 ASP, Node.js, PHP, Python 지원 |X |X |X |X |서비스 패브릭 사용 하 여 웹 프런트 엔드 hello 만들기를 지원 [ASP.NET 5](../service-fabric/service-fabric-add-a-web-frontend.md) 로 응용 프로그램 (Node.js, Java 등)를 배포할 수 있습니다는 [게스트 실행 파일](../service-fabric/service-fabric-deploy-existing-app.md)합니다. |
| 재배포 하지 않고 toomultiple 인스턴스 확장 |X |X |X |X |가상 컴퓨터를 toomultiple 인스턴스 늘릴 수 있지만 hello 서비스에서 실행 중인 toohandle이 확장 작성 해야 합니다. Tooconfigure 부하 분산 장치 tooroute 요청 hello 컴퓨터에 있고 만드는 선호도 그룹 tooprevent toomaintenance 또는 하드웨어 오류 인해 모든 인스턴스의 동시 다시 시작 합니다. |
| SSL 지원 |X |X |X |X |App Service 웹앱의 경우 사용자 지정 도메인 이름에 대한 SSL은 기본 및 표준 모드에서만 지원됩니다. 웹앱에 SSL을 사용하는 방법에 대한 자세한 내용은 [Azure 웹 사이트에 대한 SSL 인증서 구성](app-service-web-tutorial-custom-ssl.md)을 참조하세요. |
| Visual Studio 통합 |X |X |X |X | |
| 원격 디버깅 |X |X |X | | |
| TFS를 사용하여 코드 배포 |X |X |X |X | |
| [Azure Virtual Network](/azure/virtual-network/)를 사용한 네트워크 격리 |X |X |X |X |[Azure 웹 사이트 Virtual Network 통합](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/)도 참조하세요. |
| [Azure Traffic Manager](/azure/traffic-manager/) 지원 |X |X |X |X | |
| 통합된 끝점 모니터링 |X |X |X | | |
| 원격 데스크톱 액세스 tooservers | |X |X |X | |
| 사용자 지정 MSI 설치 | |X |X |X |서비스 패브릭 toohost 모든 실행 파일 이름으로 파일을 사용 하면 한 [게스트 실행 파일](../service-fabric/service-fabric-deploy-existing-app.md) hello Vm에서 모든 앱을 설치할 수 있습니다. |
| 시작 작업을 toodefine/실행 하는 기능 | |X |X |X | |
| TooETW 이벤트를 수신할 수 있습니다. | |X |X |X | |

## <a name="scenarios"></a>시나리오 및 권장 사항
Toowhich Azure 웹 호스팅 옵션 각각에 대해 가장 적합 한 수 있으므로 권장 사항이 포함 된 몇 가지 일반적인 응용 프로그램 시나리오 다음과 같습니다.

* [백그라운드 처리 및 온-프레미스 자산와 통합 하는 데이터베이스 백 엔드 toorun 비즈니스 응용 프로그램과 웹 프런트 엔드가 필요 합니다.](#onprem)
* [글로벌 서비스 및 올바른 크기를 조정 하는 회사 내 웹 사이트에 도달 하는 신뢰할 수 있는 방법은 toohost이 필요 합니다.](#corp)
* [IIS6 응용 프로그램을 Windows Server 2003에서 실행 중인 경우](#iis6)
* [중소기업 소유자 저는 및 저렴 한 비용으로 toohost 내 사이트 필요한 하지만 향후 성장에 주의 합니다.](#smallbusiness)
* [웹 또는 그래픽 디자이너 저는 하 고 원하는 toodesign 내 고객에 대 한 웹 사이트를 구축 합니다.](#designer)
* [다중 계층 응용 프로그램 웹 프런트 엔드 toohello 클라우드를 마이그레이션하는 중입니다.](#multitier)
* [내 응용 프로그램이 고도로 사용자 지정 된 Windows 또는 Linux 환경과 I toomove 것 toohello 클라우드입니다.](#custom)
* [내 사이트에는 오픈 소스 소프트웨어를 사용 하 고 toohost 원하는 Azure에서.](#oss)
* [Tooconnect toohello 회사 네트워크 하는 기간 업무 응용 프로그램을 있습니다.](#lob)
* [모바일 클라이언트에 대 한 REST API 또는 웹 서비스 toohost을 하겠습니다.](#mobile)

### <a id="onprem"></a>백그라운드 처리 및 온-프레미스 자산와 통합 하는 데이터베이스 백 엔드 toorun 비즈니스 응용 프로그램과 웹 프런트 엔드가 필요 합니다.
Azure App Service는 복잡한 비즈니스 응용 프로그램에 적합한 솔루션입니다. 하면 부하 분산 된 플랫폼에서 자동으로 확장 하 고 Active Directory로 보호 되 tooyour 온-프레미스 리소스에 연결할 수 있는 앱을 개발 합니다. 세계 최고 수준의 포털 및 Api를 통해 쉽게 해당 앱을 관리 하며 toogain 어떻게 고객이 사용 하 고 해당 응용 프로그램 통찰력 도구로 파악할 수 있습니다. hello [Webjobs] [ Webjobs] 작업 하이브리드 연결 및 VNET 기능 하는 동안 프로그램 웹 계층의 일부로 쉽게 쉽게 tooconnect 백 tooon 온-프레미스 리소스 및 기능을 사용 하면 백그라운드 프로세스를 실행할 수 있습니다. Azure App Service는 웹앱에 대해 9의 SLA를 제공하며 다음 작업을 수행할 수 있게 해줍니다.

* 자동 복구 및 패치되는 클라우드 플랫폼에서 응용 프로그램을 안정적으로 실행할 수 있습니다.
* 전 세계 데이터 센터 네트워크로 자동 확장할 수 있습니다.
* 재해 복구를 위한 백업 및 복원을 수행할 수 있습니다.
* ISO, SOC2 및 PCI 호환성을 제공할 수 있습니다.
* Active Directory와 통합할 수 있습니다.

### <a id="corp"></a>글로벌 서비스 및 올바른 크기를 조정 하는 회사 내 웹 사이트에 도달 하는 신뢰할 수 있는 방법은 toohost이 필요 합니다.
Azure App Service는 회사 웹 사이트를 호스트하는 데 적합한 솔루션입니다. 웹 앱 tooscale 신속 하 게 값과 데이터 센터의 전역 네트워크를 통해 toomeet 요구 하는 쉽게 있습니다. Azure 웹 사이트는 로컬 연결, 내결함성 및 지능형 트래픽 관리 기능을 제공합니다. 매우 효율적인 관리 도구를 제공 하는 플랫폼 모두에 있도록 toogain 통찰력 사이트 상태 및 사이트 트래픽 쉽고 신속 하 게 합니다. Azure App Service는 웹앱에 대해 9의 SLA를 제공하며 다음 작업을 수행할 수 있게 해줍니다.

* 자동 복구 및 패치되는 클라우드 플랫폼에서 웹 사이트를 안정적으로 실행할 수 있습니다.
* 전 세계 데이터 센터 네트워크로 자동 확장할 수 있습니다.
* 재해 복구를 위한 백업 및 복원을 수행할 수 있습니다.
* 통합된 도구로 로그 및 트래픽을 관리할 수 있습니다.
* ISO, SOC2 및 PCI 호환성을 제공할 수 있습니다.
* Active Directory와 통합할 수 있습니다.

### <a id="iis6"></a> IIS6 응용 프로그램을 Windows Server 2003에서 실행 중인 경우
Azure 앱 서비스를 통해 쉽게 tooavoid hello 이전 IIS6 응용 프로그램 마이그레이션과 관련 된 인프라 비용입니다. Microsoft가 만든 [쉽게 toouse 마이그레이션 도구와 자세한 마이그레이션 지침](https://www.movemetowebsites.net/) toocheck 호환성을 사용 하 고 toobe 수행 해야 하는 모든 변경 내용을 다룹니다. 일반 CMS 도구, Visual Studio 및 TFS와 통합 하면 쉽게 toodeploy IIS6 응용 프로그램 toohello 클라우드 직접 있습니다. 배포 된 후 hello Azure 포털 제공 사용할 수 있는 강력한 관리 도구가 tooscale toomanage 비용 다운 및 필요에 따라 toomeet 요청 드릴업 합니다. Hello 마이그레이션 도구와 함께 다음 작업을 수행할 수 있습니다.

* 신속 하 고 쉽게 레거시 Windows Server 2003 웹 응용 프로그램 toohello 클라우드를 마이그레이션하십시오.
* Tooleave 옵트인 하 여 연결 된 SQL 데이터베이스 온-프레미스 toocreate 혼성 응용 프로그램.
* 레거시 응용 프로그램과 함께 SQL Database를 자동으로 이동할 수 있습니다.

### <a id="smallbusiness"></a>중소기업 소유자 저는 및 저렴 한 비용으로 toohost 내 사이트 필요한 하지만 향후 성장에 주의 합니다.
Azure App Service는 처음에 무료로 사용한 후 필요할 때 기능을 추가할 수 있으므로 이 시나리오에 적합한 솔루션입니다. 각 무료 웹 앱에는 Azure에서 제공 하는 도메인 (*your_company*. azurewebsites.net), hello 플랫폼 쉽게 tooget 하는 응용 프로그램 갤러리 뿐만 아니라 통합된 배포 및 관리 도구를 포함 하 고 시작 합니다. 다른 여러 서비스 및 향상 된 사용자 요구를 충족 하는 hello 사이트 tooevolve 허용 하는 확장 옵션이 있습니다. Azure App Service를 통해 다음 작업을 수행할 수 있습니다.

* 무료 계층 hello로 시작 하며 필요에 따라 다음 확장 합니다.
* WordPress와 같은 인기 있는 웹 응용 프로그램을 설정 하는 hello 응용 프로그램 갤러리 tooquickly를 사용 합니다.
* 필요에 따라 추가 Azure 서비스 및 기능 tooyour 응용 프로그램을 추가 합니다.
* HTTPS를 사용하여 웹앱 보안을 유지할 수 있습니다.

### <a id="designer"></a>웹 또는 그래픽 디자이너 저는 하 고 원하는 toodesign 내 고객에 대 한 웹 사이트를 구축
웹 개발자와 디자이너의 경우 다양한 프레임워크 및 도구와 쉽게 통합되고, Git 및 FTP용 배포 지원을 포함하며, Visual Studio 및 SQL Database와 같은 도구 및 서비스와 긴밀하게 통합되는 Azure App Service가 적합합니다. App Service를 통해 다음 작업을 수행할 수 있습니다.

* [자동화된 작업][scripting](영문)을 위해 명령줄 도구를 사용할 수 있습니다.
* [.Net][dotnet], [PHP][PHP], [Node.js][nodejs] 및 [Python][Python] 등의 인기 있는 언어로 작업할 수 있습니다.
* Toovery 고용량 업그레이드에 대 한 세 개의 서로 다른 크기 조정 수준을 선택 합니다.
* 와 같은 다른 Azure 서비스와 통합 [SQL 데이터베이스][sqldatabase], [서비스 버스] [ servicebus] 및 [저장소] [ Storage], 또는 파트너의 hello 제공 [Azure Store][azurestore], MySQL 및 MongoDB와 같은 합니다.
* Visual Studio, Git, WebMatrix, WebDeploy, TFS, FTP 등의 도구와 통합할 수 있습니다.

### <a id="multitier"></a>다중 계층 응용 프로그램 웹 프런트 엔드 toohello 클라우드를 마이그레이션하는 중입니다.
Tooa 데이터베이스를 연결 하는 웹 서버 같은 다중 계층 응용 프로그램을 실행 하는 경우 Azure 앱 서비스는 Azure SQL 데이터베이스와의 긴밀 한 통합을 제공 하는 좋은 방법입니다. 및 백 엔드 프로세스를 실행 하기 위한 hello Webjob 기능을 사용할 수 있습니다.

더 hello 서버 환경 같은 hello 기능 tooremote 서버에 대 한 제어 필요 하거나 서버 시작 작업을 구성 하는 경우에 하나 이상의 프로그램 계층에 대 한 서비스 패브릭을 선택 합니다.

가상 컴퓨터에 선택 사용자 계층의 하나 이상의 toouse 하려는 경우 고유한 컴퓨터 이미지 하거나 서버 소프트웨어 또는 서비스 패브릭에서 구성할 수 없는 서비스를 실행 합니다.

### <a id="custom"></a>내 응용 프로그램이 고도로 사용자 지정 된 Windows 또는 Linux 환경과 I toomove 것 toohello 클라우드입니다.
응용 프로그램에 필요한 복잡 한 설치 또는 소프트웨어 및 hello 운영 체제의 구성, 가상 컴퓨터 hello 가장 적합 한 솔루션을 때문일 수 있습니다. 가상 컴퓨터를 통해 다음을 수행할 수 있습니다.

* 예: Windows 또는 Linux 운영 체제, 가상 컴퓨터 갤러리 toostart hello를 사용 하 고 응용 프로그램 요구 사항에 대 한 사용자 지정 합니다.
* 만들고 Azure에서 가상 컴퓨터에는 기존 온-프레미스 서버 toorun의 사용자 지정 이미지를 업로드 합니다.

### <a id="oss"></a>내 사이트에는 오픈 소스 소프트웨어를 사용 하 고 toohost 원하는 Azure에서
오픈 소스 framework 응용 프로그램 서비스, hello 언어에서 사용할 수 응용 프로그램에 필요한 프레임 워크 있습니다에 대 한 자동으로 구성 된 경우. App Service를 통해 다음 작업을 수행할 수 있습니다.

* [.NET][dotnet], [PHP][PHP], [Node.js][nodejs] 및 [Python][Python] 등의 여러 인기 있는 오픈 소스 언어를 사용할 수 있습니다.
* WordPress, Drupal, Umbraco, DNN 및 다른 여러 타사 웹 응용 프로그램을 설정할 수 있습니다.
* 기존 응용 프로그램을 마이그레이션하거나 hello 응용 프로그램 갤러리에서에서 새 항목을 만듭니다.

앱 서비스에서 오픈 소스 프레임 워크에 지원 되지 않는 경우 실행할 수 있습니다 hello 중 하나에서 다른 Azure 웹 호스팅 옵션입니다. 가상 컴퓨터를 사용 하면 소프트웨어 설치 및 구성 hello Windows 될 수 있는 hello 컴퓨터 이미지에 또는 Linux 기반 합니다.

### <a id="lob"></a>Tooconnect toohello 회사 네트워크를 필요로 하는 기간 업무 응용 프로그램이
Toocreate 기간 업무 응용 프로그램을 사용 하도록 하려는 경우 웹 사이트에 직접 액세스 tooservices 또는 hello 회사 네트워크의 데이터에 필요할 수 있습니다. 이 응용 프로그램 서비스, 서비스 패브릭 및 hello를 사용 하 여 가상 컴퓨터에서 수행 가능한 [Azure 가상 네트워크 서비스](/azure/virtual-network/)합니다. 앱 서비스에서 hello를 사용할 수 있습니다 [VNET 통합 기능](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/), 회사 네트워크에서 듯 Azure 응용 프로그램 toorun 수 있습니다.

### <a id="mobile"></a>원하는 toohost 모바일 클라이언트에 대 한 REST API 또는 웹 서비스
HTTP 기반 웹 서비스를 사용 하면 다양 한 클라이언트, 모바일 클라이언트 toosupport 있습니다. ASP.NET Web API와 같은 프레임 워크 통합 Visual Studio toomake와 보다 쉽게 toocreate 및 REST 서비스를 사용 합니다.  이러한 서비스는 웹 끝점에서 노출, 가능한 toouse 이므로 모든 웹 Azure toosupport에 호스팅 과정이이 시나리오입니다. 그러나 REST API를 호스트하는 데 적합한 옵션은 App Service입니다. App Service를 통해 다음 작업을 수행할 수 있습니다.

* 신속 하 게 만들는 [모바일 앱](../app-service-mobile/app-service-mobile-value-prop.md) 또는 [API 앱](../app-service-api/app-service-api-apps-why-best-platform.md) toohost hello HTTP 웹 서비스에 Azure의 전 세계적으로 분산된 데이터 센터 중 하나입니다.
* 기존 서비스를 마이그레이션하거나 새 서비스를 만들 수 있습니다.
* 단일 인스턴스를 가진 가용성에 대 한 SLA를 달성 하거나 toomultiple 전용 컴퓨터를 확장 합니다.
* 사용 하 여 hello 사이트 tooprovide REST Api tooany HTTP 클라이언트, 모바일 클라이언트를 게시 합니다.

> [!NOTE]
> Tooget 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동<a href="https://trywebsites.azurewebsites.net/">https://trywebsites.azurewebsites.net</a>만들 수 있는 즉시 수명이 짧은 스타터 앱 Azure 앱 서비스에서 무료로, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

## <a id="nextsteps"></a> 다음 단계
Hello 3 웹 호스팅 옵션에 대 한 자세한 내용은 참조 [Azure 소개](../fundamentals-introduction-to-azure.md)합니다.

응용 프로그램에 대 한 hello 선택 옵션으로 시작 tooget hello 다음 리소스를 참조:

* [Azure App Service](/azure/app-service/)
* [Azure Cloud Services](/azure/cloud-services/)
* [Azure 가상 컴퓨터](/azure/virtual-machines/)
* [Service Fabric](/azure/service-fabric/)

<!-- URL List -->

[Azure App Service]: /azure/app-service/
[Cloud Services]: /azure/cloud-services/
[Virtual Machines]: /azure/virtual-machines/
[Service Fabric]: /azure/service-fabric/
[ClearDB]: http://www.cleardb.com/
[WebJobs]: http://go.microsoft.com/fwlink/?linkid=390226&clcid=0x409
[Configuring an SSL certificate for an Azure Website]: app-service-web-tutorial-custom-ssl.md
[azurestore]: https://azuremarketplace.microsoft.com/en-us/marketplace/apps
[scripting]: https://azure.microsoft.com/documentation/scripts/?services=web-sites
[dotnet]: https://azure.microsoft.com/develop/net/
[nodejs]: https://azure.microsoft.com/develop/nodejs/
[PHP]: https://azure.microsoft.com/develop/php/
[Python]: https://azure.microsoft.com/develop/python/
[servicebus]: /azure/service-bus/
[sqldatabase]: /azure/sql-database/
[Storage]: /azure/storage/

<!-- IMG List -->

[ChoicesDiagram]: ./media/choose-web-site-cloud-service-vm/Websites_CloudServices_VMs_3.png
