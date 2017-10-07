---
title: "Azure에서 개발자를 위한 aaaGet 시작 가이드 | Microsoft Docs"
description: "이 항목에서는 tooget hello Microsoft Azure 플랫폼을 사용 하 여 해당 개발 환경에 대 한 시작을 보고 하는 개발자를 위한 중요 한 정보를 제공 합니다."
services: 
cloud: 
documentationcenter: 
author: ggailey777
manager: erikre
ms.assetid: 
ms.service: na
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: glenga
ms.openlocfilehash: 72dc2678db7738923d4bc7783e297fea6fcded83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-guide-for-azure-developers"></a>Azure 개발자를 위한 시작 가이드

## <a name="what-is-azure"></a>Azure란? 

Azure는 기존 응용 프로그램을 호스팅할 hello 새 응용 프로그램의 개발을 간소화 하 고도 온-프레미스 응용 프로그램을 향상 시킬 수 있는 완전 한 클라우드 플랫폼입니다. Toodevelop 해야 하는 hello 클라우드 서비스를 통합 하는 azure, 테스트, 배포 및 응용 프로그램을 관리-클라우드의 hello 효율성을 이용 하면서 컴퓨팅입니다.

Azure에서 응용 프로그램을 호스트하면 작은 응용 프로그램부터 시작하여 고객의 요구가 증가함에 따라 응용 프로그램을 쉽게 확장할 수 있습니다. 또한 azure도 서로 다른 지역 간 장애 조치를 포함 하 여 고가용성 응용 프로그램에 대 한 필요한 hello 안정성을 제공 합니다. hello [Azure 포털](https://portal.azure.com) 모든 Azure 서비스를 쉽게 관리할 수 있습니다. 또한 서비스 관련 API 및 템플릿을 사용하여 서비스를 프로그래밍 방식으로 관리할 수 있습니다.

**이 독자**:이 가이드는 소개 toohello 응용 프로그램 개발자를 위한 Azure 플랫폼입니다. Toostart 기존 응용 프로그램 tooAzure Azure 또는 마이그레이션에 새 응용 프로그램을 구축 해야 하는 방향과 지침을 제공 합니다.

## <a name="where-do-i-start"></a>시작 단계

Azure에서 제공 하는 모든 hello 서비스와 서비스 필요한 toosupport 솔루션 아키텍처 까다로운 작업 toofigure 수 있습니다. 이 섹션 밝은 hello Azure 서비스 개발자가 일반적으로 사용 합니다. 목록이 모든 Azure 서비스에 대 한 참조 hello [Azure 문서](../../index.md)합니다.

방법을 결정 해야 먼저 toohost Azure에서 응용 프로그램입니다. 해야 하나요 toomanage 전체 인프라를 가상 컴퓨터로 (VM). Azure에서 제공 하는 hello 플랫폼 관리 기능을 사용할 수 있습니까? 이전에 서버가 없는 프레임 워크 toohost 코드 실행만 필요 한가요?

응용 프로그램에 Azure에서 몇 가지 옵션을 제공하는 클라우드 저장소가 필요합니다. Azure의 엔터프라이즈 인증을 활용할 수 있습니다. 또한 클라우드 기반 개발 및 모니터링을 위한 도구가 있으며 대부분의 호스팅 서비스는 DevOps 통합을 제공합니다.

이제 응용 프로그램에 대 한 조사 하는 것이 좋습니다 hello 특정 서비스의 일부에 대해 살펴보겠습니다.

### <a name="application-hosting"></a>응용 프로그램 호스팅

Azure는 hello 인프라 세부 정보에 대 한 tooworry 없는 있도록 여러 클라우드 기반 계산 제공 toorun 응용 프로그램을 제공 합니다. 응용 프로그램 사용량의 증가에 따라 리소스를 쉽게 확장할 수 있습니다.

Azure는 필요한 응용 프로그램 개발 및 호스팅 요구 사항을 지원하는 서비스를 제공합니다. 인프라-as a service (IaaS)를 제공 하는 azure 응용 프로그램 호스팅에 대 한 제어를 전체 toogive 합니다. Azure의 플랫폼으로-서비스 (PaaS) 제품 hello 완벽 하 게 관리 하는 데 필요한 서비스 toopower 앱을 제공 합니다. 없는 Azure의 서버 호스팅에 적용 코드를 작성은 toodo 하기만 합니다.

![Azure 응용 프로그램 호스팅 옵션](./media/azure-developer-guide/azure-developer-hosting-options.png)


#### <a name="azure-app-service"></a>Azure 앱 서비스 

웹 기반 프로젝트를 사용 하 여 가장 빠른 경로 toopublish hello 하려는 경우 Azure 앱 서비스는 것이 좋습니다. 응용 프로그램 서비스를 통해 쉽게 tooextend 사용자 앱 toosupport 모바일 클라이언트를 구성 하 고 쉽게 REST Api를 게시 합니다. 이 플랫폼은 소셜 공급자, 트래픽 기반 자동 크기 조정, 프로덕션 환경에서 테스트, 연속 배포 및 컨테이너 기반 배포를 사용하여 인증을 제공합니다.

앱 서비스에서 앱을 만들 때 유형만 hello 중 하나를 선택 합니다.

- [Web Apps](../../app-service-web/app-service-web-overview.md): .NET, Java, PHP, Node.js 및 Python으로 작성된 웹 응용 프로그램 및 웹 사이트를 호스트할 수 있습니다.

- [모바일 앱](../../app-service-mobile/app-service-mobile-value-prop.md): 모바일 장치에서 웹 앱 확장 toosupport 액세스 합니다. 소셜 공급자 및 Azure AD(Azure Active Directory)에서 인증을 활성화하고 백 엔드 저장소를 제공하고 푸시 알림을 위해 [Azure Notification Hubs](../../notification-hubs/notification-hubs-push-notification-overview.md)와 통합할 수 있습니다.

- [API 앱](../../app-service-api/app-service-api-apps-why-best-platform.md): 더 많은 클라이언트가 쉽게 사용할 수 있도록 사용자 Api Swagger 메타 데이터를 사용 하는 hello 클라우드에 안전 하 게 노출할 수 있습니다.

모든 응용 프로그램 세 가지 형식은 공유 하기 때문에 응용 프로그램 서비스 런타임 hello, 웹 사이트를 호스팅하, 모바일 클라이언트를 지원 및 모두에서 azure에서 Api를 노출 hello 같은 프로젝트 또는 솔루션입니다. 앱 서비스에 대해 자세히 toolearn 참조 [응용 프로그램 서비스 작동 방식](../../app-service/app-service-how-works-readme.md)합니다.

App Service는 DevOps를 염두에 두고 설계되었습니다. GitHub Webhook, Jenkins, Visual Studio Team Services, TeamCity 등을 포함하여 게시 및 연속 통합 배포를 위한 다양한 도구를 지원합니다.

Hello를 사용 하 여 프로그램 기존 응용 프로그램 tooApp 서비스를 마이그레이션할 수 있습니다 [온라인 마이그레이션 도구](https://www.migratetoazure.net/)합니다.

>**때 toouse**: 기존 웹 응용 프로그램 tooAzure 마이그레이션하는 경우 사용 하 여 앱 서비스 및 웹 응용 프로그램에 대 한 완전히 관리 되는 호스팅 플랫폼 중지 해야 합니다. 모바일 클라이언트 toosupport 필요 하거나 앱과 함께 REST Api를 노출 하는 경우에 응용 프로그램 서비스를 사용할 수 있습니다.

>**시작 하려면**: 응용 프로그램 서비스 사용 하면 쉽게 toocreate 및 첫 번째 배포 [웹 앱](../../app-service-web/web-sites-dotnet-get-started.md), [모바일 앱](../../app-service-mobile/app-service-mobile-ios-get-started.md), 또는 [API 앱](../../app-service-api/app-service-api-dotnet-get-started.md)합니다.

>**지금 사용해 보기**: 응용 프로그램 서비스를 사용 하면 Azure 계정에 대해 toosign 필요 없이 단기간 용 앱 tootry hello 플랫폼 프로 비전 합니다. Hello 플랫폼을 시도 하 고 [Azure 앱 서비스 앱 만들기](https://tryappservice.azure.com/)합니다.

#### <a name="azure-virtual-machines"></a>Azure 가상 컴퓨터

인프라-as a service (IaaS) 공급 업체 Azure에 배포할 수 있습니다 tooor 마이그레이션할 Windows 또는 Linux Vm의 경우 응용 프로그램 tooeither 프로그램. Azure 가상 네트워크와 함께 Azure 가상 컴퓨터의 Windows 또는 Linux Vm tooAzure hello 배포를 지원합니다. Vm에서 hello 컴퓨터의 hello 구성 완전히 제어를 해야 합니다. VM을 사용하는 경우 사용자가 모든 서버 소프트웨어 설치, 구성, 유지 관리 및 운영 체제 패치를 담당합니다.

Vm이 있는 제어 hello 수준으로 인해 PaaS 모델에 적합 하지 않은 Azure에서 다양 한 서버 워크 로드를 실행할 수 있습니다. 이러한 워크로드에는 데이터베이스 서버, Windows Server Active Directory 및 Microsoft SharePoint가 포함됩니다. 자세한 내용은 중 하나에 대 한 hello 가상 컴퓨터 설명서를 참조 하십시오. [Linux](/azure/virtual-machines/linux/) 또는 [Windows](/azure/virtual-machines/windows/)합니다.

>**때 toouse**: 프로그램 응용 프로그램 인프라 또는 toomigrate 온-프레미스 응용 프로그램 작업 부하 tooAzure toomake 변경 하지 않고도 제어할 수 전체 하려는 경우 가상 컴퓨터를 사용 합니다.

>**시작 하려면**: 만들기는 [Linux VM](../../virtual-machines/virtual-machines-linux-quick-create-portal.md) 또는 [Windows VM](../../virtual-machines/virtual-machines-windows-hero-tutorial.md) hello Azure 포털에서에서 합니다.

#### <a name="azure-functions-serverless"></a>Azure Functions(서버를 사용하지 않음)

대신 아웃 빌드 및 전체 응용 프로그램이 나 hello 인프라 toorun 코드 관리에 대 한 걱정의 합니다. 경우에 어떻게 있습니다 수만 사용자 코드를 작성 한 실행 응답 tooevents 또는 일정에 따라?  [Azure 기능](../../azure-functions/functions-overview.md) 은 "않는" a-스타일 바로 작성할 수 있습니다 hello 필요한 코드를 제공 합니다. Functions를 사용하면 코드 실행이 HTTP 요청, Webhook, 클라우드 서비스 이벤트 또는 일정에 따라 트리거됩니다. C\#, F\#, Node.js, Python 또는 PHP와 같은 원하는 개발 언어로 코드를 작성할 수 있습니다. 사용량 기반 요금 청구 된 코드를 실행 하 고 필요에 따라 Azure 조정 하는 hello 시간에 대해서만 지불 합니다.

>**때 toouse**: 웹 기반 이벤트에 의해 또는 일정에 따라 다른 Azure 서비스에 의해 트리거되는 코드가 있는 경우에 Azure 함수를 사용 합니다. 전체 호스팅된 프로젝트 또는 하려는 경우 toopay 코드를 실행 하는 hello 시간에 대 한 오버 헤드 hello 필요 하지 않는 경우에 함수를 사용할 수 있습니다. toolearn 더 참조 [Azure 함수 개요](../../azure-functions/functions-overview.md)합니다.

>**시작 하려면**: 너무 hello 함수 빠른 시작 자습서에 따라[첫 번째 사용자 함수를 만들어](../../azure-functions/functions-create-first-azure-function.md) hello 포털에서 합니다.

>**지금 사용해 보기**: Azure 함수에는 Azure 계정으로 가입할 toosign 필요 없이 코드를 실행할 수 있습니다. 지금 사용하여 [첫 번째 Azure Function을 만듭니다](https://tryappservice.azure.com/).

#### <a name="azure-service-fabric"></a>Azure Service Fabric

Azure 서비스 패브릭은 쉽게 toobuild 수행 하는 분산된 시스템 플랫폼 패키지, 배포 하 고, 확장성 및 안정성이 뛰어난 microservices를 관리 합니다. 또한 배포된 응용 프로그램의 프로비전, 배포, 모니터링, 업그레이드/패치 및 삭제를 위한 포괄적인 응용 프로그램 관리 기능을 제공합니다. 에 컴퓨터의 공유 풀에서 실행 되는 앱을 시작 작은 toohundreds 또는 수천 필요에 따라 컴퓨터의 크기를 조정 합니다.

Service Fabric은 OWIN(Open Web Interface for .NET) 및 ASP.NET Core를 사용하여 WebAPI를 지원합니다. Service Fabric은 .NET Core 및 Java 모두에서 Linux에 대한 서비스를 구축하는 SDK를 제공합니다. 서비스 패브릭에 대해 자세히 toolearn 참조 hello [서비스 패브릭 학습 경로](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)합니다.

>**때 toouse:** 서비스 패브릭 응용 프로그램을 만들거나 기존 응용 프로그램 toouse 마이크로 서비스 아키텍처를 다시 작성 하는 경우이 좋은 대안입니다. 서비스 패브릭을 사용 하 여 더 많은에 대 한 제어 나 hello 기본 인프라에 대 한 직접 액세스 해야 하는 경우.

>**시작하기:** [첫 번째 Azure Service Fabric 응용 프로그램을 만듭니다](../../service-fabric/service-fabric-create-your-first-application-in-visual-studio.md).

### <a name="enhance-your-applications-with-azure-services"></a>Azure 서비스를 사용하여 응용 프로그램 개선

또한 tooapplication 호스팅, Azure hello 기능, 개발 및 hello 클라우드 및 온-프레미스 둘 다에서 응용 프로그램의 유지 관리를 향상 시킬 수 있는 서비스 제공을 제공 합니다.

#### <a name="hosted-storage-and-data-access"></a>호스트된 저장소 및 데이터 액세스

대부분의 응용 프로그램 해야 Azure에 응용 프로그램 toohost를 결정 하는 방법의 하므로 관계 없이 데이터를 저장, hello 저장소 및 데이터 서비스를 다음 중 하나 이상을 것이 좋습니다.

-   **Azure SQL 데이터베이스**: hello 클라우드에서 관계형 테이블 형식 데이터를 저장 하기 위한 Microsoft SQL Server 엔진 hello Azure 기반 버전입니다. SQL Database는 예측 가능한 성능, 가동 중지 시간이 없는 확장성, 무중단 업무 방식, 데이터 보호 기능을 제공합니다.

    >**때 toouse**: TSQL 쿼리에 대 한 응용 프로그램 데이터 저장소 참조 무결성, 트랜잭션 지원 및 지원에 필요한 경우.

    >**시작 하려면**: [hello Azure 포털을 사용 하 여 분 후에 SQL 데이터베이스를 만들](../../sql-database/sql-database-get-started.md)합니다.

-   **Azure Storage**: Blob, 큐, 파일 및 다른 종류의 비관계형 데이터에 대한 항상 사용 가능한 지속형 저장소를 제공합니다. 저장소 Vm에 대 한 hello 저장소 기반을 제공합니다.

    >**때 toouse**: blob, 공유, 파일 또는 (큐) 메시지를 응용 프로그램 키-값 쌍 (테이블)와 같은 비관계형 데이터를 저장 하는 경우.

    >**시작하기**: 저장소 유형([Blob](../../storage/blobs/storage-dotnet-how-to-use-blobs.md), [테이블](../../cosmos-db/table-storage-how-to-use-dotnet.md), [큐](../../storage/queues/storage-dotnet-how-to-use-queues.md) 또는 [파일](../../storage/files/storage-dotnet-how-to-use-files.md)) 중 하나를 선택합니다.

-   **Azure DocumentDB**: 완벽하게 관리되고 확장 가능한 NoSQL 데이터베이스 서비스로, 개체 데이터에 대해 SQL 쿼리 기능을 수행합니다. 기존 MongoDB 드라이버를 사용하여 DocumentDB에 액세스할 수 있습니다.
    >**때 toouse:** 응용 프로그램에서 JSON 문서에 대해 toobe 수 tooexecute SQL 쿼리 필요한 또는 MongoDB를 사용 하는 경우.

    >**시작하기**: [DocumentDB C# 콘솔 응용 프로그램을 빌드합니다](../../documentdb/documentdb-get-started.md). MongoDB 개발자인 경우 [MongoDB에 대한 DocumentDB 프로토콜 지원](../../documentdb/documentdb-protocol-mongodb.md)을 참조하세요.

사용할 수 있습니다 [Azure Data Factory](../../data-factory/data-factory-introduction.md) toomove 기존 온-프레미스 데이터 tooAzure 합니다. 준비 toomove 데이터 toohello 클라우드 하지 않은 경우 [하이브리드 연결](../../biztalk-services/integration-hybrid-connection-overview.md) 연결할 BizTalk 서비스 사용 하면 응용 프로그램 서비스 호스트 앱 tooon 온-프레미스 리소스입니다. 또한 온-프레미스 응용 프로그램에서 tooAzure 데이터 및 저장소 서비스에 연결할 수 있습니다.

#### <a name="docker-support"></a>Docker 지원

OS 가상화의 형태인 Docker 컨테이너를 사용하면 더 효율적이고 예측 가능한 방식으로 응용 프로그램을 배포할 수 있습니다. 컨테이너 화 된 응용 프로그램 개발 및 테스트 시스템에서 방식으로 동일한 프로덕션 hello에서 작동 합니다. 표준 Docker 도구를 사용하여 컨테이너를 관리할 수 있습니다. 기존 기술 및 toodeploy 인기 있는 오픈 소스 도구를 사용 하 고 Azure에서 컨테이너 기반 응용 프로그램을 관리할 수 있습니다.

Azure에서는 여러 가지 방법으로 응용 프로그램에서 toouse 컨테이너를 제공 합니다.

-   **Azure Docker VM 확장**: VM Docker 도구 tooact는 Docker 호스트를 구성할 수 있습니다.

    >**때 toouse**: vm에서 응용 프로그램에 대 한 toogenerate 일관 된 컨테이너 배포 하려는 경우 또는 toouse 하려는 경우 [Docker Compose](https://docs.docker.com/compose/overview/)합니다.

    >**시작 하려면**: [hello Docker VM 확장을 사용 하 여 Azure에서 Docker 환경을 만들](../../virtual-machines/virtual-machines-linux-dockerextension.md)합니다.

-   **Azure 컨테이너 서비스**: toorun 컨테이너 화 가능한 응용 프로그램을 미리 구성 된 만들기, 구성 및 클러스터 된 가상 컴퓨터를 관리할 수 있습니다. 컨테이너 서비스에 대해 자세히 toolearn 참조 [Azure 컨테이너 서비스 소개](../../container-service/container-service-intro.md)합니다.

    >**때 toouse**: toobuild 즉시 사용, 확장 가능한 환경 추가 일정 예약 및 관리 도구를 제공 하는 docker는 Docker Swarm 클러스터를 배포 하는 경우 필요 합니다.

    >**시작하기**: [Container Service 클러스터를 배포합니다](../../container-service/dcos-swarm/container-service-deployment.md).

-   **Docker Machine**: docker-machine 명령을 사용하여 가상 호스트에서 Docker 엔진을 설치 및 관리할 수 있습니다.

    >**때 toouse**: 단일 Docker 호스트를 만들어 tooquickly 프로토타입 응용 프로그램 중지 해야 합니다.

-   **App Service용 사용자 지정 Docker 이미지**: Linux에서 웹앱을 배포할 때 컨테이너 레지스트리 또는 고객 컨테이너에서 Docker 컨테이너를 사용할 수 있습니다.

    >**때 toouse**: Linux tooa Docker 이미지에서 웹 앱을 배포 하는 경우.

    >**시작하기**: [Linux에서 App Service에 대한 사용자 지정 Docker 이미지를 사용합니다](../../app-service-web/app-service-linux-using-custom-docker-image.md).

### <a name="authentication"></a>인증

중요 한 toonot 프로그램 응용 프로그램 뿐만 아니라 무단 tooprevent tooyour 리소스에 액세스를 사용 하는 사용자를 알고 있습니다. Azure 앱 클라이언트를 여러 가지 방법으로 tooauthenticate 제공합니다.

-   **Azure Active Directory (Azure AD)**: hello Microsoft 다중 테 넌 트, 클라우드 기반 id 및 액세스 관리 서비스입니다. Azure AD와 통합 하 여 단일 로그인 (SSO) tooyour 응용 프로그램에 추가할 수 있습니다. 디렉터리 속성 직접 hello Azure AD Graph API 또는 hello Microsoft Graph API를 사용 하 여 액세스할 수 있습니다. 네이티브 HTTP/REST 끝점을 사용 하 여 hello oauth 2.0 권한 부여 프레임 워크 및 Open ID 연결에 대 한 Azure AD 지원을 통합할 수 있으며 다중 플랫폼 Azure AD 인증 라이브러리 hello 수 있습니다.

    >**때 toouse**: tooprovide SSO 환경, 그래프 기반 데이터 작업을 이동 하거나 도메인 기반 사용자를 인증 합니다.

    >**시작 하려면**: toolearn hello을 더 참조 [Azure Active Directory 개발자 가이드](../../active-directory/active-directory-developers-guide.md)합니다.

-   **앱 서비스 인증**: 소셜 id 공급자와 함께 Azure AD에 대 한 기본 제공 인증 지원 용량도 toohost 앱 서비스 앱을 선택 하면-Facebook, Google, Microsoft 및 Twitter를 포함 합니다.

    >**때 toouse**: Azure AD를 사용 하 여 앱 서비스 앱에 tooenable 인증 하려는 경우 소셜 id 공급자 또는 둘 다 합니다.

    >**시작 하려면**: toolearn 앱 서비스에서 인증에 대 한 참조 [인증 및 Azure 앱 서비스의 권한 부여](../../app-service/app-service-authentication-overview.md)합니다.

Azure의 보안 모범 사례에 대해 자세히 toolearn 참조 [Azure 보안에 대 한 유용한 정보 및 패턴](../../security/security-best-practices-and-patterns.md)합니다.

### <a name="monitoring"></a>모니터링

Toobe 수 toomonitor 성능 필요한 응용 프로그램을 만들고 Azure에서 실행할을 고객 응용 프로그램을 사용 하는 방법을 확인 한 문제에 대해 보고 합니다. Azure는 몇 가지 모니터링 옵션을 제공합니다.

-   **Visual Studio Application Insights**: 라이브 웹 응용 프로그램을 Visual Studio toomonitor와 통합 하는 확장 가능한 분석 Azure 호스팅 서비스입니다. 사용 하면 Azure에서 호스팅되는 여부를 toocontinuously 해야 하는 hello 데이터 hello 성능 및 응용 프로그램의 가용성을 개선 합니다.

    >**시작 하려면**: 따라 hello [Application Insights 자습서](../../application-insights/app-insights-overview.md)합니다.

-   **Azure 모니터**: toovisualize, 쿼리, 경로, 보관 및 hello 메트릭 및 Azure 인프라와 리소스에서 생성 되는 로그에서 작동 하는 데 도움이 되는 서비스입니다. 모니터는 hello Azure 포털에서에서 참조 하 고 Azure 리소스를 모니터링 하기 위한 단일 소스는 hello 데이터 뷰를 제공 합니다.
 
    >**시작하기**: [Azure Monitor를 시작합니다](../../monitoring-and-diagnostics/monitoring-get-started.md).

### <a name="devops-integration"></a>DevOps 통합

Vm을 프로 비전 또는 연속 통합을 사용 하 여 웹 앱을 게시, Azure는 대부분의 hello 인기 있는 DevOps 도구와 통합 됩니다. Jenkins, GitHub, Puppet, Chef, TeamCity, Ansible, VSTS, 등과 같은 도구에 대 한 지원을 통해 hello 도구는 이미 있고 최대화 기존 환경을 사용 하 여 작업할 수 있습니다.

>**지금 사용해 보기:** [hello DevOps 통합 중 몇 가지 사용을](https://azure.microsoft.com/try/devops/)합니다.

>**시작 하려면**: toosee DevOps 옵션, 앱 서비스 앱에 대 한 참조 [연속 배포 tooAzure 앱 서비스](../../app-service-web/app-service-continuous-deployment.md)합니다.


## <a name="azure-regions"></a>Azure 지역

Azure는 hello 전 세계 여러 지역에서 일반적으로 사용할 수 있는 전역 클라우드 플랫폼입니다. 서비스, 응용 프로그램 또는 Azure에서 VM 프로 비전 할 때 응용 프로그램이 실행 되는 특정 데이터 센터를 나타내는 영역 tooselect 요청 또는 데이터가 저장 되어 있습니다. Hello에 게시 된 toospecific 위치에 해당 하는 이러한 영역 [Azure 지역](https://azure.microsoft.com/regions/) 페이지.

### <a name="choose-hello-best-region-for-your-application-and-data"></a>응용 프로그램 및 데이터에 대 한 hello 최상의 영역 선택

Azure를 사용 하 여 hello 이점 중 하나입니다 hello 전 세계 toovarious 데이터 센터 응용 프로그램을 배포할 수 있습니다. hello 지역을 선택 하는 응용 프로그램의 hello 성능에 영향을 줄 수 있습니다. 예를 들어, 더 나은 toochoose 영역의 네트워크 요청에 고객 tooreduce 대기 시간이 더 가깝기 때문 toomost을를입니다. 수도 있습니다 tooselect 일부 국가에서 응용 프로그램을 배포 하기 위한 지역 toomeet hello 법적 요구 합니다. 항상 이므로 모범 사례 toostore 응용 프로그램 데이터 동일한 데이터 센터 hello 또는 데이터 센터에 가까운 같이 가능한 toohello 데이터 센터와 응용 프로그램을 호스팅하는 합니다.

### <a name="multi-region-apps"></a>다중 지역 앱

발생 가능성 이것이 불가능 한 오프 라인으로 전체 데이터 센터 toogo에 대 한 인터넷 오류나 자연 재해와 같은 이벤트 때문입니다. 모범 사례 toohost 중요 한 비즈니스 응용 프로그램 둘 이상의 데이터 센터 tooprovide 최대 사용 가능한 경우 여러 지역을 사용하면 로컬 사용자에게 대기 시간을 줄여주고 응용 프로그램을 업데이트할 때 유연성에 대한 추가 기회를 제공할 수 있습니다.

가상 컴퓨터 및 응용 프로그램 서비스와 같은 일부 서비스를 사용 하 여 [Azure 트래픽 관리자](../../traffic-manager/traffic-manager-overview.md) tooenable 다중 영역 지원 영역 toosupport 고가용성 엔터프라이즈 응용 프로그램 간 장애 조치를 사용 합니다. 예를 들어 [Azure 참조 아키텍처: 고가용성을 요구하는 웹 응용 프로그램](../../guidance/guidance-web-apps-multi-region.md)을 참조하세요.

>**때 toouse**: 장애 조치 및 복제를 활용 하는 엔터프라이즈 및 가용성이 높은 응용 프로그램을 보유 하는 경우.

## <a name="how-do-i-manage-my-applications-and-projects"></a>응용 프로그램 및 프로젝트 관리 방법

Azure toocreate 있습니다에 대 한 다양 한 경험을 제공 하 고 Azure 리소스, 응용 프로그램 및 프로젝트 관리-프로그래밍 방식과 hello [Azure 포털](https://portal.azure.com/)합니다.

### <a name="command-line-interfaces-and-powershell"></a>명령줄 인터페이스 및 PowerShell

Azure 제공 두 가지 방법으로 toomanage 응용 프로그램 및 서비스 hello 명령줄에서 Bash, 터미널, hello 명령 프롬프트 또는 원하는 명령줄 도구를 사용 하 여 합니다. 일반적으로 hello hello Azure 포털에서와 같이 명령줄에서 hello 동일 작업을 수행할 수 있습니다-만들기 등 가상 컴퓨터, 가상 네트워크, 웹 앱 및 기타 서비스를 구성 합니다.

-   [Azure 명령줄 인터페이스 (CLI)](../../xplat-cli-install.md): tooan Azure 구독을 연결 하 고 hello 명령줄에서 Azure 리소스에 대 한 다양 한 태스크를 프로그래밍할 수 있습니다.

-   [Azure PowerShell](../../powershell-install-configure.md): toomanage Azure를 사용 하면 cmdlet이 포함 된 모듈의 집합을 제공 하 여 Windows PowerShell을 사용 하는 리소스입니다.

### <a name="azure-portal"></a>Azure portal

Azure 포털 hello 있습니다 수 toocreate를 사용 하 여, 관리 및 Azure 리소스 및 서비스 제거 웹 기반 응용 프로그램입니다. hello Azure 포털에 위치한 <https://portal.azure.com>합니다. Azure 리소스를 관리 하는 액세스 toosubscription 설정 및 청구 정보에 대 한 도구, 사용자 지정 가능한 대시보드를 포함 됩니다. 자세한 내용은 참조 hello [Azure 포털 개요](../../azure-portal-overview.md)합니다.

### <a name="rest-apis"></a>REST API

Azure의 hello Azure 포털 UI 지원 하는 REST Api 집합을 기반으로 합니다. 대부분의 이러한 REST Api는도 지원 되는 toolet 프로그래밍 방식으로 프로 비전 하 고 모든 인터넷 사용 장치에서 Azure 리소스와 응용 프로그램을 관리 합니다. Hello 전체 집합이 REST API 설명서를 참조 hello [Azure REST SDK 참조](https://docs.microsoft.com/rest/api/)합니다.

### <a name="apis"></a>API

또한 Api tooREST 여러 Azure 서비스 수 있는 응용 프로그램에서 다음 개발 플랫폼 hello에 대 한 Sdk를 포함 하 여 플랫폼 특정 Azure Sdk를 사용 하 여 리소스를 프로그래밍 방식으로 관리:

-   [.NET](https://go.microsoft.com/fwlink/?linkid=834925)
-   [Node.JS](http://azure.github.io/azure-sdk-for-node/)
-   [Java](https://docs.microsoft.com/java/api/)
-   [PHP](https://github.com/Azure/azure-sdk-for-php/blob/master/README.md)
-   [Python](http://azure-sdk-for-python.readthedocs.io/en/latest/)
-   [Ruby](https://github.com/Azure/azure-sdk-for-ruby/blob/master/README.md)

와 같은 서비스 [모바일 앱](../../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md) 및 [Azure 미디어 서비스](../../media-services/media-services-dotnet-how-to-use.md) 클라이언트 쪽 Sdk toolet 제공 웹 및 모바일 클라이언트 응용 프로그램에서 서비스에 액세스할 수 있습니다.

### <a name="azure-resource-manager"></a>Azure 리소스 관리자 
    
가능성이 높은 Azure에서 응용 프로그램 실행의 작업이 여러 Azure 서비스와의 뒤에 오며 hello 동일한 수명 주기가 모든 하며이 논리 단위로 간주 될 수 있습니다. 예를 들어 웹앱은 Web Apps, SQL Database, Storage, Azure Redis Cache 및 Azure Content Delivery Network 서비스를 사용할 수 있습니다. [Azure 리소스 관리자](../../azure-resource-manager/resource-group-overview.md) hello 리소스 그룹으로 응용 프로그램에서 사용할 수 있습니다. 배포 지정, 업데이트 또는 단일, 통합 작업에서 모든 hello 리소스를 삭제 합니다.

또한 toologically 그룹화 하 고 관리 관련 리소스, Azure 리소스 관리자는 hello 배포 및 관련된 리소스의 구성을 사용자 지정할 수 있는 배포 기능을 포함 합니다. 예를 들어 Resource Manager를 사용하면 여러 가상 컴퓨터, 부하 분산 장치 및 Azure SQL Database를 단일 단위로 구성하는 응용 프로그램을 배포 및 구성할 수 있습니다.

JSON 형식 문서인 Azure Resource Manager 템플릿을 사용하여 이러한 배포를 개발합니다. 템플릿을 사용하면 스크립트 대신 선언적 템플릿을 통해 배포를 정의하고 응용 프로그램을 관리할 수 있습니다. 템플릿은 테스트, 스테이징 및 프로덕션과 같은 여러 환경에 사용할 수 있습니다. 예를 들어 템플릿을 사용 하 여 한 번의 클릭으로 서비스를 Azure의 hello 리포지토리 tooa 집합에 hello 코드를 배포 하는 단추 tooa GitHub 리포지토리를 추가할 수 있습니다.

>**때 toouse**: Azure CLI 및 Azure PowerShell, REST Api를 사용 하 여 프로그래밍 방식으로 관리할 수 있는 앱에 대 한 템플릿 기반 배포 하려는 경우 사용 하 여 리소스 관리자 템플릿을 hello 합니다.

>**시작 하려면**: 템플릿을 사용 하 여 시작 tooget 참조 [제작 Azure 리소스 관리자 템플릿을](../../resource-group-authoring-templates.md)합니다.

## <a name="understanding-accounts-subscriptions-and-billing"></a>계정, 구독 및 청구 이해

개발자 म toodive hello 코드에 바로 및 같은 tooget 실행 응용 프로그램을 만드는 것으로 최대한 빠르게 시작을 시도 합니다. Tooencourage 확실히 원하는 toostart 최대한 쉽게 Azure에서 작동 합니다. toohelp 쉽게 쉽게, Azure 서비스는 [무료 평가판](https://azure.microsoft.com/free/)합니다. 일부 서비스도에 "실행 방법 무료로" 기능을 같은 [Azure 앱 서비스](https://tryappservice.azure.com/), 계정을 만들 너무도 필요 하지 않은입니다. 재미로 코딩 및 배포 하 여 응용 프로그램 tooAzure toodive 그대로 것도 중요 한 tootake 일부 시간 toounderstand Azure 사용자 계정, 구독 및 청구의 관점에서 작동 하는 방법입니다.

### <a name="what-is-an-azure-account"></a>Azure 계정이란?

toobe 수 toocreate 또는 Azure 구독 작업에는 Azure 계정이 있어야 합니다. Azure 계정은 Azure AD 또는 회사나 학교 조직과 같은 디렉터리의 단순한 ID로, Azure AD에서 신뢰할 수 있는 것입니다. 소속 조직 toosuch, 하는 경우 Azure AD에서 신뢰 하는 Microsoft 계정을 사용 하 여 항상 구독을 만들 수 있습니다. Azure AD와 온-프레미스 Windows Server Active Directory 통합에 대 한 더 toolearn 참조 [Azure Active Directory와 온-프레미스 id 통합](../../active-directory/active-directory-aadconnect.md)합니다.

모든 Azure 구독은 Azure AD 인스턴스와 트러스트 관계가 있습니다. 즉, 트러스트 하 여 해당 디렉터리 tooauthenticate 사용자, 서비스 및 장치입니다. 여러 구독 hello 신뢰할 수 있는 동일한 디렉터리만 구독 디렉터리를 하나만 신뢰 합니다. toolearn 더 참조 [Azure 구독과 Azure Active Directory와 연결 된](../../active-directory/active-directory-how-subscriptions-associated-directory.md)합니다.

또한 toodefining 개별 Azure 계정을 id로 호출 또한 *사용자*를 정의할 수도 있습니다 *그룹* Azure AD에서 합니다. 역할 기반 액세스 제어 (RBAC)를 사용 하 여 구독에 좋은 방법 toomanage 액세스 tooresources은 사용자 그룹을 만드는 합니다. toocreate 그룹 참조 toolearn [Azure Active Directory 미리 보기에서 그룹 만들기](../../active-directory/active-directory-groups-create-azure-portal.md)합니다. 또한 [PowerShell을 사용](../../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md)하여 그룹을 만들고 관리할 수 있습니다.

### <a name="manage-your-subscriptions"></a>구독 관리

구독은 연결 된 Azure 계정 tooan 있는 Azure 서비스의 논리 단위입니다. 각 연결된 계정에는 구독에서의 역할이 있습니다. Azure 서비스에 대한 청구는 구독 단위로 이루어집니다. 목록이 형식으로 사용할 수 있는 구독 서비스 hello에 대 한 참조 [Microsoft Azure 제안 세부 정보](https://azure.microsoft.com/support/legal/offer-details/)합니다.

#### <a name="administrator-roles"></a>관리자 역할

Azure 구독에는 언제든지 할당할 수 있는 여러 계정 관리자 역할이 있습니다.

-   **계정 관리자**:이 역할 hello 구독에 대 한 모든 권한을 가집니다 및 청구에 대 한 책임이 있는 hello 계정입니다.

-   **서비스 관리자**: hello 구독이이 역할의 모든 hello 서비스에 대 한 제어 합니다. 이 hello 기본적으로 계정 관리자 hello으로 동일한 계정입니다.

-   **공동 관리자**:이 역할에 모든 서비스 관리자 hello로 액세스할 동일 hello 점을 제외 하 고 hello 구독 tooan Azure 디렉터리의 hello 연결을 변경할 수 없습니다.

관리자 역할에 대 한 자세한 정보는 toolearn 참조 [어떻게 tooadd 또는 변경 Azure 관리자 역할](../../billing/billing-add-change-azure-subscription-administrator.md#add-an-admin-for-a-subscription)합니다.

#### <a name="resource-groups"></a>리소스 그룹

새로운 Azure 서비스를 프로비전할 때 지정된 구독에서 수행할 수 있습니다. 리소스 그룹의 hello 컨텍스트에서 리소스 라고도 하는 개별 Azure 서비스에 생성 됩니다. 리소스 그룹 toodeploy 더 쉽게 확인 하 고 응용 프로그램의 리소스를 관리 합니다. 리소스 그룹에는 하나의 단위로 toowork와 원하는 응용 프로그램에 대 한 hello 리소스를 모두 포함 되어야 합니다. 리소스 그룹 및 심지어 toodifferent 구독 간에 리소스를 이동할 수 있습니다. 리소스를 이동 하는 방법에 대 한 toolearn 참조 [리소스 toonew 리소스 그룹이 나 구독 이동](../../resource-group-move-resources.md)합니다.

hello Azure 리소스 탐색기는 구독에서 이미 만든 hello 리소스를 시각화에 유용한 도구입니다. toolearn 더 참조 [tooview Azure 리소스 탐색기를 사용 하 여 리소스를 수정 하 고](../../resource-manager-resource-explorer.md)합니다.

#### <a name="grant-access-tooresources"></a>권한 부여 액세스 tooresources

TooAzure 리소스 액세스를 허용 하는 경우 항상 이므로 hello로 사용자 최소 권한의 필요한 tooperform 지정된 된 작업을 제공 하는 것이 좋습니다.

-   **역할 기반 액세스 제어 (RBAC)**: Azure에 권한을 부여할 수 있습니다는 지정 된 범위에서 toouser 계정 (사용자): 구독, 리소스 그룹 또는 개별 리소스입니다. RBAC를 사용 하 여 리소스 그룹으로 리소스 집합을 배포 하 고 사용 권한 tooa 특정 사용자 또는 그룹 권한을 부여 수 있습니다. 또한 toohello 대상 리소스 그룹에 속하는 액세스 tooonly hello 리소스를 제한할 수 있습니다. 가상 컴퓨터 또는 가상 네트워크와 같은 액세스 tooa 단일 리소스를 부여할 수도 있습니다. 역할 toohello 사용자, 그룹 또는 서비스 사용자를 할당할 toogrant 액세스 있습니다. 미리 정의된 많은 역할이 있으며 자체 사용자 지정 역할을 정의할 수도 있습니다.

    >**때 toouse**: 사용자 및 그룹에 대 한 세분화 된 액세스 관리 중지 해야 합니다.

    >**시작 하려면**: toolearn 더 참조 [hello Azure 포털에에서 대 한 액세스 관리 시작](../../active-directory/role-based-access-control-what-is.md)합니다.

-   **서비스 보안 주체 개체**: 또한 tooproviding toouser 사용자 및 그룹에 액세스 권한을 부여할 수 있습니다 hello 동일한 액세스 tooa 서비스 보안 주체입니다.

    > **때 toouse**: 하는 프로그래밍 방식으로 Azure 리소스 관리 하거나 때 응용 프로그램에 대 한 액세스 권한을 부여 합니다. 자세한 내용은 [Azure Active Directory 응용 프로그램 및 서비스 주체 만들기](../../resource-group-create-service-principal-portal.md)를 참조하세요.

#### <a name="tags"></a>태그들

Azure 리소스 관리자를 사용 하면 사용자 지정 태그 tooindividual 리소스를 할당할 수 있습니다. 태그는 키-값 쌍, 대금 청구 또는 모니터링에 대 한 tooorganize 리소스를 필요할 때 유용할 수 있습니다. 태그 여러 리소스 그룹에 걸쳐 방식으로 tootrack 리소스를 제공합니다. Hello Azure 리소스 관리자 템플릿 또는 프로그래밍 방식으로 hello REST API, hello Azure CLI 또는 PowerShell을 사용 하 여 hello 포털에서 태그를 할당할 수 있습니다. Tooeach 리소스 여러 태그를 할당할 수 있습니다. toolearn 더 참조 [를 사용 하 여 Azure 리소스를 tooorganize 태그](../../resource-group-using-tags.md)합니다.

### <a name="billing"></a>결제

온-프레미스에서 toocloud 호스팅 서비스의 컴퓨팅 hello 이동, 추적 및 서비스 사용과 관련 된 비용을 예측은 중요 한 문제입니다. 중요 한 toobe 수 tooestimate는 새 리소스는 매월 toorun 비용입니다. 현재 지출 한 hello에 따라 지정된 된 월에 대 한 hello 청구 표시 되는 모양을 toobe 수 tooproject을 해야 합니다.

#### <a name="get-resource-usage-data"></a>리소스 사용 현황 데이터 가져오기

Azure는 액세스 tooresource 소비와 Azure 구독에 대 한 메타 데이터 정보를 제공 하는 청구 REST Api 집합을 제공 합니다. 예측 하 고 Azure 비용을 관리 하는 기능 toobetter hello 이러한 청구 Api 제공 합니다. 시간별 증가에 따른 지출을 추적 및 분석하고, 지출 경고를 만들고, 현재 사용 추세를 기반으로 향후 청구를 예측할 수 있습니다.

>**시작 하려면**: hello 청구 Api 사용에 대 한 더 toolearn 참조 [Azure 청구 사용량 및 RateCard Api 개요](../../billing-usage-rate-card-overview.md)합니다.

#### <a name="predict-future-costs"></a>향후 비용 예측

Azure의 미리 tooestimate 비용 재미가 있지만 [가격 계산기](https://azure.microsoft.com/pricing/calculator/) 리소스 배포 된 hello 비용을 예측할 때는 사용할 수 있습니다. Hello 포털 및 hello REST Api 청구 tooestimate 이후 비용, 현재 사용량에 따라 hello 결제 블레이드를 사용할 수 있습니다.

>**시작하기**: 참조 [Azure 청구 사용량 및 RateCard API 개요](../../billing-usage-rate-card-overview.md)를 참조하세요.

#### <a name="set-up-billing-alerts"></a>청구 경고 설정

응용 프로그램 또는 Azure에서 솔루션을 배포한 후에 hello 경고에 정의 된 지출 한 hello 접근 하는 경우 전자 메일을 보내 경고를 만들 수 있습니다.

>**시작 하려면**: toolearn 더 참조 [청구 Microsoft Azure 구독에 대 한 경고를 설정](../../billing-set-up-alerts.md)합니다.
