---
title: "웹 응용 프로그램에서 Azure 마켓플레이스 hello aaaCreate | Microsoft Docs"
description: "방법을 사용 하 여 hello Azure Marketplace에서에서 새 WordPress 웹 앱 toocreate hello Azure 포털에 알아봅니다."
services: app-service\web
documentationcenter: 
author: sunbuild
manager: erikre
editor: 
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sunbuild
ms.custom: mvc
ms.openlocfilehash: 5ad1ca2f3f7831d857c3e9b02738b6b34acf3649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-from-hello-azure-marketplace"></a>Hello Azure Marketplace에서에서 웹 앱 만들기
<!-- Note: This article replaces web-sites-php-web-site-gallery.md -->

[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

hello Azure 마켓플레이스는 다양 한 범위의 예: WordPress 및 Umbraco CMS 오픈 소스 소프트웨어 커뮤니티에서 개발한 인기 있는 웹 앱을 제공 합니다. 이 자습서에 설명 어떻게 toocreate WordPress 응용 프로그램에서 Azure 마켓플레이스에 적용 됩니다.
Azure Web App 및 MySQL 데이터베이스를 만듭니다. 

![WordPress 웹앱 대시보드 예제](./media/app-service-web-create-web-app-from-marketplace/wpdashboard2.png)

## <a name="before-you-begin"></a>시작하기 전에 

Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.

## <a name="deploy-from-azure-marketplace"></a>Azure Marketplace에서 배포
Azure 마켓플레이스의 toodeploy WordPress 아래 hello 단계를 수행 합니다.

### <a name="sign-in-tooazure"></a>TooAzure에 로그인
Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.

### <a name="deploy-wordpress-template"></a>WordPress 템플릿 배포
Azure 마켓플레이스 hello 설치 hello 리소스를 설정 하기 위한 템플릿을 제공 [WordPress](https://portal.azure.com/#create/WordPress.WordPress) 템플릿 tooget 시작 합니다.
   
Hello 다음 입력 정보 toodeploy hello WordPress 앱 및 관련 리소스입니다.

  ![WordPress 만들기 흐름](./media/app-service-web-create-web-app-from-marketplace/wordpress-portal-create.png)


| 필드         | 제안 값           | 설명  |
| ------------- |-------------------------|-------------|
| 앱 이름      | mywordpressapp          | **웹앱 이름**으로 고유한 앱 이름을 입력합니다. 이 이름은 앱에 대 한 기본 DNS 이름 hello의 일부로 사용 됩니다 `<app_name>.azurewebsites.net`되므로 원래 toobe 고유 Azure에서 모든 앱에서 합니다. Tooyour 사용자 노출 먼저 사용자 지정 도메인 이름을 tooyour 응용 프로그램을 나중에 매핑할 수 있습니다. |
| 구독  | Pay-As-You-Go             | **구독**을 선택합니다. 다중 구독인 경우 hello 적절 한 구독을 선택 합니다. |
| 리소스 그룹| mywordpressappgroup                 |    **리소스 그룹**을 입력합니다. 리소스 그룹은 웹앱 및 데이터베이스 같은 Azure 리소스가 배포되고 관리되는 논리적 컨테이너입니다. 리소스 그룹을 만들거나 기존 리소스 그룹을 사용할 수 있습니다. |
| 앱 서비스 계획 | myappplan          | 앱 서비스 계획을 사용 하는 실제 리소스 toohost의 hello 컬렉션 응용을 프로그램을 나타냅니다. 선택 hello **위치** 및 hello **가격 책정 계층**합니다. 가격 책정에 대한 자세한 내용은 [App Service 가격 책정 계층](https://azure.microsoft.com/pricing/details/app-service/)을 참조하세요. |
| 데이터베이스      | mywordpressapp          | MySQL 용 hello 적절 한 데이터베이스 공급자를 선택 합니다. 웹앱은 **ClearDB**, **MySQL용 Azure 데이터베이스** 및 **MySQL 앱 내**를 지원합니다. 자세한 내용은 아래의 [데이터베이스 구성](#database-config) 섹션을 참조하세요. |
| Application Insights | 설정 또는 해제          | 선택 사항입니다. [Application Insights](https://azure.microsoft.com/en-us/services/application-insights/)는 **설정**을 클릭하면 웹앱에 대한 모니터링 서비스를 제공합니다.|

<a name="database-config"></a>

### <a name="database-configuration"></a>데이터베이스 구성
MySQL 데이터베이스 공급자의 선택에 따라 hello 단계를 수행 합니다.  웹 앱과 MySQL 데이터베이스 hello에 있을 것이 좋습니다. 동일한 위치입니다.

#### <a name="cleardb"></a>ClearDB 
[ClearDB](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)는 Azure의 완전히 통합된 MySQL 서비스를 위한 타사 솔루션입니다. 에 순서 toouse ClearDB 데이터베이스를 해야 하는 신용 카드 tooyour tooassociate [Azure 계정](http://account.windowsazure.com/subscriptions)합니다. 기존 데이터베이스 toochoose 목록을 볼 하거나 클릭 수 ClearDB 데이터베이스 공급자를 선택한 경우 **새로 만들기** 단추 toocreate 데이터베이스입니다.

![ClearDB 만들기](./media/app-service-web-create-web-app-from-marketplace/mysqldbcreate.png)

#### <a name="azure-database-for-mysql-preview"></a>MySQL용 Azure 데이터베이스(미리 보기)
[MySQL에 대 한 azure 데이터베이스](https://azure.microsoft.com/en-us/services/mysql) hello 클라우드에서 가장 신뢰할 고객이 응용 프로그램 개발 및 분과 hello에서 크기 조정에 toostand MySQL 데이터베이스를 사용 하면 배포에 대 한 관리 되는 데이터베이스 서비스를 제공 합니다. 가격 책정 모델에서 inclusive, 높은 가용성, 보안 및 복구 – 기본 제공 되 고 비용 없이 같은 원하는 모든 hello 기능 얻게 추가 비용입니다. 클릭 **가격 책정 계층** toochoose 다른 [가격 책정 계층](https://azure.microsoft.com/pricing/details/mysql)합니다. toouse 기존의 데이터베이스 또는 MySQL 서버를 기존 서버가 있는 hello에 있는 기존 리소스 그룹을 사용 합니다. 

![Hello 웹 응용 프로그램에 대 한 hello 데이터베이스 설정 구성](./media/app-service-web-create-web-app-from-marketplace/wordpress-azure-database.PNG)

> [!NOTE]
>  MySQL용 Azure 데이터베이스(미리 보기) 및 Linux의 웹앱(미리 보기)을 모든 하위 지역에서 사용할 수 있는 것은 아닙니다. 에 대 한 자세한 toolearn [MySQL (미리 보기)에 대 한 Azure 데이터베이스](https://docs.microsoft.com/en-us/azure/mysql) 및 [Linux에서 웹 앱](./app-service-linux-intro.md) 제한 사항입니다. 

#### <a name="mysql-in-app"></a>MySQL 인앱
[앱에서 MySQL](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app) hello 플랫폼에 MySql을 고유 하 게 실행할 수 있도록 하는 응용 프로그램 서비스의 기능입니다. hello 핵심 기능 hello 릴리스의 hello 기능 지원:

- MySQL 서버 hello 나란히 hello 사이트를 호스팅하는 웹 서버가 동일한 인스턴스를 실행 합니다. 이렇게 하면 응용 프로그램 성능이 향상됩니다.
- 저장소가 MySQL 및 웹앱 파일 간에 공유됩니다. 무료 및 공유 계획이 적중할 수 할당량 한도 hello 사이트를 사용 하 여 작업에 따라 hello 있습니다 때 참고를 수행 합니다. 무료 및 공유 계획에 대한 [할당량 제한](https://azure.microsoft.com/en-us/pricing/details/app-service/plans/)을 확인하세요.
- MySQL에 대해 느린 쿼리 로깅 및 일반 로깅을 설정할 수 있습니다. Note hello 사이트 성능에 영향을 줄 수이 고 항상 사용 하지 않습니다. hello 로깅 기능을 사용 하면 모든 응용 프로그램 문제를 조사 합니다. 

자세한 내용은 이 [문서](https://blogs.msdn.microsoft.com/appserviceteam/2016/08/18/announcing-mysql-in-app-preview-for-web-apps/ )를 확인하세요.

![MySQL 인 앱 관리](./media/app-service-web-create-web-app-from-marketplace/mysqlinappmanage.PNG)

Hello hello WordPress 응용 프로그램 배포 되는 동안 hello 포털 페이지 위쪽에 hello 종 모양 아이콘을 클릭 하 여 hello 진행률을 볼 수 있습니다.    
![진행률 표시기](./media/app-service-web-create-web-app-from-marketplace/deploy-success.png)

## <a name="manage-your-new-azure-web-app"></a>새로운 Azure 웹앱 관리

Azure 포털 tootake hello 웹 응용 프로그램에 방금 만든를 살펴보면 toohello를 이동 합니다.

toodo이 너무 로그인[https://portal.azure.com](https://portal.azure.com)합니다.

Hello 왼쪽된 메뉴에서 클릭 **응용 프로그램 서비스**, Azure 웹 앱의 hello 이름을 클릭 합니다.

![포털 탐색 tooAzure 웹 응용 프로그램](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-list.png)


웹앱의 _블레이드_(가로로 열리는 포털 페이지)로 이동했습니다.

기본적으로 웹 앱 블레이드 표시 hello **개요** 페이지. 이 페이지에서는 앱이 어떻게 작동하고 있는지를 보여 줍니다. 여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다. hello hello 블레이드의 왼쪽에 hello 탭 hello 서로 다른 구성 페이지를 열 수를 보여 줍니다.

![Azure Portal의 App Service 블레이드](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-detail.png)

Hello 블레이드에서 이러한 탭 hello tooyour 웹 응용 프로그램을 추가할 수는 많은 유용한 기능을 보여 줍니다. hello 목록 다음 몇 가지 hello 가능성을 제공 합니다.

* 사용자 지정 DNS 이름 매핑
* 사용자 지정 SSL 인증서 바인딩
* 지속적 배포 구성
* 수평 및 수직 확장
* 사용자 인증 추가

Hello 5 분 WordPress 설치 마법사 toohave WordPress 응용 프로그램 시작 및 실행을 완료 합니다. 체크 아웃 [Wordpress 설명서](https://codex.WordPress.org/) toodevelop 웹 앱입니다.

![Wordpress 설치 마법사](./media/app-service-web-create-web-app-from-marketplace/wplanguage.png)

## <a name="configuring-your-app"></a>앱 구성 
WordPress 앱을 프로덕션에서 사용할 수 있도록 준비하기 위해 관리와 관련된 몇 가지 단계를 수행해야 합니다. 이러한 단계 tooconfigure 따르고 WordPress 응용 프로그램 관리:

| toodo이 중... | 사용 기능... |
| --- | --- |
| **대규모 파일 업로드 또는 저장** |[Blob Storage 사용을 위한 WordPress 플러그 인](https://wordpress.org/plugins/windows-azure-storage/)|
| **메일 보내기** |구매 [SendGrid](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SendGrid.SendGrid?tab=Overview) hello를 사용 하 여 서비스를 전자 메일로 보내기 [SendGrid를 사용 하기 위한 WordPress 플러그 인](https://wordpress.org/plugins/sendgrid-email-delivery-simplified/) tooconfigure 것|
| **사용자 지정 도메인 이름** |[Azure 앱 서비스에서 사용자 지정 도메인 이름 구성](app-service-web-tutorial-custom-domain.md) |
| **HTTPS** |[Azure App Service에서 웹앱에 대한 HTTPS를 사용하도록 설정](app-service-web-tutorial-custom-ssl.md) |
| **사전 프로덕션 유효성 검사** |[Azure App Service에서 웹앱에 대한 스테이징 및 개발 환경 설정](web-sites-staged-publishing.md)|
| **모니터링 및 문제 해결** |[Azure App Service에서 웹앱에 대한 진단 로깅 설정](web-sites-enable-diagnostic-log.md) 및 [Azure App Service에서 웹앱 모니터링](app-service-web-tutorial-monitoring.md) |
| **사이트 배포** |[Azure App Service에서 웹앱 배포](app-service-deploy-local-git.md) |


## <a name="secure-your-app"></a>앱 보안 
WordPress 앱을 프로덕션에서 사용할 수 있도록 준비하기 위해 관리와 관련된 몇 가지 단계를 수행해야 합니다. 이러한 단계 tooconfigure 따르고 WordPress 응용 프로그램 관리:

| toodo이 중... | 사용 기능... |
| --- | --- |
| **강력한 사용자 이름 및 암호**|  암호를 자주 변경합니다. *admin* 또는 *wordpress* 등과 같이 일반적으로 사용되는 사용자 이름은 사용하지 마세요. 모든 WordPress 사용자 toouse 고유한 사용자 이름과 강력한 암호를 적용 합니다. |
| **최신 상태로 유지** | WordPress 핵심, 테마, toodate 플러그 인을 유지 합니다. Hello 최신 PHP 런타임에 Azure 앱 서비스에서 사용할 수 있는 사용 |
| **WordPress 보안 키 업데이트** | 업데이트 [WordPress 보안 키](https://codex.wordpress.org/Editing_wp-config.php#Security_Keys) tooimprove 암호화 쿠키에 저장|

## <a name="improve-performance"></a>성능 향상
Hello 클라우드의 성능이 주로 캐싱 및 확장을 통해 이루어집니다. 그러나 hello 메모리, 대역폭 및 웹 응용 프로그램 호스트의 다른 특성 고려할 수 있습니다.

| toodo이 중... | 사용 기능... |
| --- | --- |
| **앱 서비스 인스턴스 기능 이해** |[App Service 계층의 기능을 비롯한 가격 책정 세부 정보](https://azure.microsoft.com/en-us/pricing/details/app-service/)|
| **리소스 캐시** |사용 하 여 [Azure Redis cache](https://azure.microsoft.com/en-us/services/cache/), 또는 중 하나 hello 캐싱 제공 되는 다른 hello [Azure 저장소](https://azuremarketplace.microsoft.com) |
| **응용 프로그램 확장** |Tooscale 해야 [Azure 앱 서비스의 웹 앱 hello](web-sites-scale.md) 및/또는 MySQL 데이터베이스 사용 합니다. MySQL 인 앱은 확장을 지원하지 않으므로 ClearDB 또는 MySQL용 Azure 데이터베이스(미리 보기)를 선택합니다. [MySQL (미리 보기)에 대 한 Azure 데이터베이스의 크기를 조정](https://azure.microsoft.com/en-us/pricing/details/mysql/) 사용 하는 경우 또는 [ClearDB 높은 가용성 라우팅](http://w2.cleardb.net/faqs/) tooscale 데이터베이스를 |

## <a name="availability-and-disaster-recovery"></a>가용성 및 재해 복구
고가용성 재해 복구 toomaintain 비즈니스 연속성의 hello 측면을 포함합니다. Hello 클라우드에서 오류 및 재해를 계획 하려면 toorecognize hello 오류 신속 하 게 합니다. 이러한 솔루션은 고가용성을 위한 전략을 구현하는 데 도움이 됩니다.

| toodo이 중... | 사용 기능... |
| --- | --- |
| **사이트 부하 분산** 또는 **사이트 지리적으로 분산** |[Azure Traffic Manager로 트래픽 라우팅](https://azure.microsoft.com/en-us/services/traffic-manager/) |
| **백업 및 복원** |[Azure App Service에서 웹앱 백업](web-sites-backup.md) 및 [Azure App Service에서 웹앱 복원](web-sites-restore.md) |

## <a name="next-steps"></a>다음 단계
다양 한 기능에 대 한 자세한 내용은 [앱 서비스 toodevelop와 소수 자릿수](/app-service-web/)합니다.
