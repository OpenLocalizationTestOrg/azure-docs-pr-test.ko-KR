---
title: "aaaAbout Azure 앱 서비스에서 모바일 앱"
description: "앱 서비스 제공 모바일 앱 tooyour 엔터프라이즈 하는 hello 장점에 알아봅니다."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: 4e96cb9d-a632-4cf6-8219-0810d8ade3f9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: ab96af11c3df196acfb9ecec1339e7f6093c7066
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started"> </a>Azure App Service의 Mobile Apps 정보
Azure App Service는 완전히 관리되는 PaaS([platform as a service](https://azure.microsoft.com/overview/what-is-paas/))로써 전문 개발자를 위해 제공됩니다. hello 서비스 풍부한 기능 tooweb, 모바일, 및 통합 시나리오를 제공합니다. 

Azure 앱 서비스의 hello 모바일 앱 기능 엔터프라이즈 개발자 및 확장성이 높은 전체적으로 사용할 수 있는 시스템 통합 업체는 모바일 응용 프로그램 개발 플랫폼을 사용 합니다.

![Mobile Apps 기능에 대한 시각적 개요](./media/app-service-mobile-value-prop/overview.png)

## <a name="why-mobile-apps"></a>Mobile Apps 사용 이유
Hello 모바일 앱 기능을 사용 하 여 다음을 수행할 수 있습니다.

* **네이티브 앱 및 크로스 플랫폼 앱 빌드**: 빌드하는 앱이 네이티브 iOS, Android 및 Windows 앱인지 또는 크로스 플랫폼 Xamarin 앱이나 Cordova(PhoneGap) 앱인지에 관계없이 네이티브 SDK를 통해 App Service를 사용할 수 있습니다.
* **Tooyour 엔터프라이즈 시스템 연결**: hello 모바일 앱 기능을 사용 하면 분 후에 회사 로그인 추가 하 고 하거나 연결할 수 tooyour 엔터프라이즈 온-프레미스 클라우드 리소스입니다.
* **데이터 동기화를 사용 하 여 오프 라인 지원 앱을 빌드**: 오프 라인으로 작업 하는 응용 프로그램을 구축 하 여 모바일 직원 생산성을 높일을 확인 하 고 엔터프라이즈 데이터 소스를 사용 하 여 연결이 때 hello 백그라운드에서 모바일 앱 toosync 데이터를 사용 하거나 SaaS () Api 서비스로 소프트웨어입니다.
* **시간 (초)에서 알림을 toomillions 푸시**: 모든 장치에서 인스턴트 푸시 알림 사용 하는 고객 tootheir 요구에 맞게 설정 하 고 hello 시간이 오른쪽 때 전송에 참여 합니다.

## <a name="mobile-apps-features"></a>Mobile Apps 기능
hello 같은 기능에는 중요 한 toocloud 사용이 가능한 모바일 개발

* **인증 및 권한 부여**: 엔터프라이즈 인증을 위한 Azure Active Directory 및 Facebook, Google, Twitter, Microsoft 계정과 같은 소셜 공급자를 포함하여 점점 증가하는 ID 공급자 목록에서 선택합니다. Mobile Apps은 각 공급자에 대해 OAuth 2.0 서비스를 제공합니다. 공급자 관련 기능에 대 한 hello id 공급자에 대 한 hello SDK를 통합할 수 있습니다.

    [인증 기능]에 대해 자세히 알아보세요.

* **데이터 액세스**: 모바일 앱 tooAzure SQL 데이터베이스 또는 온-프레미스 SQL server 연결에 모바일에서 잘 작동 OData v3 데이터 소스를 제공 합니다. 이 서비스가 Entity Framework를 기반으로 할 수 있기 때문에 [Azure Table Storage], MongoDB, [Azure Cosmos DB] 및 SaaS API 공급자(예: Office 365 및 Salesforce.com)를 비롯한 다른 NoSQL 및 SQL 데이터 공급자와 쉽게 통합할 수 있습니다.

* **오프 라인 동기화**: 클라이언트인 Sdk 쉽게 쉽게 toobuild 강력 하 고 응답 모바일 응용 프로그램을 오프 라인에서 데이터 집합으로 작업 합니다. 충돌 해결 지원을 비롯 하 여 hello 백 엔드 데이터를 자동으로이 데이터 집합을 동기화 할 수 있습니다.

  [데이터 기능]에 대해 자세히 알아보세요.

* **푸시 알림**: 클라이언트인 Sdk 완벽 하 게 통합 Azure 알림 허브의 hello 등록 기능을 가진 사용자의 푸시 알림을 toomillions를 동시에 보낼 수 있도록 합니다.

  [푸시 알림 기능]에 대해 자세히 알아보세요.

* **클라이언트 SDK**: 네이티브 개발([iOS], [Android] 및 [Windows]), 플랫폼 간 개발([Xamarin.iOS 및 Xamarin.Android], [Xamarin.Forms]) 및 하이브리드 응용 프로그램 개발([Apache Cordova])을 포함하는 전체 집합의 클라이언트 SDK를 제공합니다. 각 클라이언트 SDK는 MIT 라이선스로 사용할 수 있으며 오픈 소스입니다.

## <a name="azure-app-service-features"></a>Azure App Service 기능
같은 플랫폼 기능 hello는 모바일 프로덕션 사이트에 대 한 유용 합니다.

* **자동 크기 조정**: 응용 프로그램 서비스와 있습니다 수 신속 하 게 수직 또는 수평 확장 toohandle 들어오는 고객 로드 합니다. 수동으로 hello 수와 Vm의 크기를 선택 하거나 모바일 앱 백 엔드 부하 또는 일정에 따라 자동 크기 조정 tooscale를 설정 합니다.

  [자동 크기 조정]에 대해 자세히 알아보세요.

* **스테이징 환경**: App Service는 여러 버전의 사이트를 실행할 수 있으므로 A/B 테스트, 대규모 DevOps 계획의 일부로 프로덕션에서 테스트 및 새로운 백 엔드의 현재 위치 스테이징을 수행할 수 있습니다.

  [스테이징 환경]에 대해 자세히 알아보세요.

* **연속 배포**: SCM 시스템의 tooa 분기에 푸시하여 백 엔드의 새 버전을 자동으로 배포할 수 있도록 앱 서비스 일반적인 공급 체인 관리 (SCM) 시스템에 통합할 수 있습니다.

  [배포 옵션]에 대해 자세히 알아보세요.

* **가상 네트워킹**: 응용 프로그램 서비스 가상 네트워크, Azure express 경로 또는 하이브리드 연결을 사용 하 여 tooon 온-프레미스 리소스를 연결할 수 있습니다.

  [하이브리드 연결], [가상 네트워크] 및 [ExpressRoute]에 대해 자세히 알아보세요.

* **격리 및 전용 환경**: 높은 확장성으로 Azure App Service 앱을 안전하게 실행하기 위해 완전히 격리된 전용 환경에서 App Service를 실행할 수 있습니다. 이 환경은 높은 확장성, 격리 또는 보안된 네트워크 액세스가 요구되는 응용 프로그램 워크로드에 이상적입니다.

  [App Service 환경]에 대해 자세히 알아보세요.

## <a name="next-steps"></a>다음 단계

tooget 완료 hello Azure 앱 서비스에서 모바일 앱 시작 [시작] 자습서입니다. 모바일 다시 종료 만들 hello 기본 사항 및 사용자가 선택한 클라이언트 hello 자습서에 설명 합니다. 인증 통합, 오프라인 동기화 및 푸시 알림에 대해서도 설명합니다. 완료할 수 있습니다 hello 자습서를 여러 번 한 번만 각 클라이언트 응용 프로그램에 대 한 합니다.

Mobile Apps에 대한 자세한 내용은 [학습 맵]을 검토하세요.
Azure 앱 서비스 플랫폼 hello에 대 한 자세한 내용은 참조 [Azure 앱 서비스]합니다.

<!-- URLs. -->
[Migrate your mobile service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[Azure 앱 서비스]: ../app-service/app-service-value-prop-what-is.md
[시작]: app-service-mobile-ios-get-started.md
[Azure Table Storage]:../cosmos-db/table-storage-how-to-use-dotnet.md
[Azure Cosmos DB]: ../cosmos-db/documentdb-get-started.md
[인증 기능]: ./app-service-mobile-auth.md
[데이터 기능]: ./app-service-mobile-offline-data-sync.md
[푸시 알림 기능]: ../notification-hubs/notification-hubs-push-notification-overview.md
[iOS]: ./app-service-mobile-ios-how-to-use-client-library.md
[Android]: ./app-service-mobile-android-how-to-use-client-library.md
[Windows]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.iOS 및 Xamarin.Android]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.Forms]: ./app-service-mobile-xamarin-forms-get-started.md
[Apache Cordova]: ./app-service-mobile-cordova-how-to-use-client-library.md
[자동 크기 조정]: ../app-service-web/web-sites-scale.md
[스테이징 환경]: ../app-service-web/web-sites-staged-publishing.md
[배포 옵션]: ../app-service-web/web-sites-deploy.md
[하이브리드 연결]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[가상 네트워크]: ../app-service-web/web-sites-integrate-with-vnet.md
[ExpressRoute]: ../app-service-web/app-service-app-service-environment-network-configuration-expressroute.md
[App Service 환경]: ../app-service-web/app-service-app-service-environment-intro.md
[학습 맵]: https://azure.microsoft.com/en-us/documentation/learning-paths/appservice-mobileapps/
