---
title: "aaaCreate 하 고 Azure에서 MySQL 데이터베이스 사용 tooa 연결"
description: "Toouse Azure 포털 toocreate MySQL 데이터베이스 hello 하 한 다음 Azure에서 PHP 웹 응용 프로그램에서 tooit를 연결 하는 방법에 대해 알아봅니다."
documentationcenter: php
services: app-service\web
author: cephalin
manager: erikre
editor: 
tags: mysql
ms.assetid: 55465a9a-7e65-4fd9-8a65-dd83ee41f3e5
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;cephalin
ms.openlocfilehash: 3abc02f8887432625666afd847e9dc0c0a4db2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a>만들고 Azure에서 MySQL 데이터베이스 사용 tooa 연결
이 자습서에서는 toocreate MySQL 데이터베이스 hello에 어떻게 [Azure 포털](https://portal.azure.com) (공급자가 [ClearDB](http://www.cleardb.com/)) 어떻게 tooconnect tooit에서 PHP 웹 응용 프로그램에서 실행 되 고 [Azure 앱 서비스](app-service/app-service-value-prop-what-is.md).

> [!NOTE]
> [마켓플레이스 앱 템플릿](app-service-web/app-service-web-create-web-app-from-marketplace.md)의 일부로 MySQL 데이터베이스를 만들 수도 있습니다.
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a>Azure 포털에서 MySQL 데이터베이스 만들기
toocreate hello Azure 포털에서에서 MySQL 데이터베이스는 다음 hello지 않습니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello 왼쪽된 메뉴에서 클릭 **새로** > **데이터 + 저장소** > **MySQL 데이터베이스**합니다.

    ![Azure에서 MySQL 데이터베이스 만들기 - 시작](./media/store-php-create-mysql-database/create-db-1-start.png)
3. 새 MySQL 데이터베이스 hello에 [블레이드](azure-portal-overview.md), 새 MySQL 데이터베이스를 다음과 같이 구성 (*블레이드*: 가로로 열리면 포털 페이지):

   * **데이터베이스 이름**: 고유하게 식별 가능한 이름을 입력합니다.
   * **구독**: hello 구독 toouse 선택
   * **데이터베이스 유형**: 선택 **Shared** 저렴 한 비용 또는 무료 계층에 대 한 또는 **전용** tooget 전용 리소스입니다.
   * **리소스 그룹**: hello MySQL 데이터베이스 tooan 기존 항목 추가 [리소스 그룹](azure-resource-manager/resource-group-overview.md) 또는 새에 배치 합니다. 같은 그룹 쉽게 관리할 수 있습니다 함께 hello의 리소스입니다.
   * **위치**: 위치 닫기 tooyou를 선택 합니다. Tooan 기존 리소스 그룹을 추가할 때 잠긴된 toohello 리소스 그룹 위치 것입니다.
   * **가격 책정 계층**: **가격 책정 계층**을 클릭한 후 가격 책정 옵션(**Mercury** 계층은 무료)을 선택한 후 **선택**을 클릭합니다.
   * **약관**: 클릭 **약관**hello 구매 세부 정보를 검토 하 고 클릭 **구매**합니다.
   * **Pin toodashboard**: tooaccess 하려는 경우 선택 hello 대시보드에서 직접 것입니다. 포털 탐색에 아직 익숙하지 않은 경우 특히 유용합니다.

     다음 스크린 샷 hello는 MySQL 데이터베이스를 구성 하는 방법의 예시입니다.  
     ![Azure에서 MySQL 데이터베이스 만들기 - 구성](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. 구성을 완료하면 **만들기**를 클릭합니다.

    ![Azure에서 MySQL 데이터베이스 만들기 - 만들기](./media/store-php-create-mysql-database/create-db-3-create.png)

    배포가 시작되었음을 알려주는 팝업 알림이 표시됩니다.

    ![Azure에서 MySQL 데이터베이스 만들기 - 진행 중](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    배포에 성공하면 다른 팝업을 받게 됩니다. hello 포털도 MySQL 데이터베이스 블레이드에서 자동으로 열립니다.

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a>Tooyour MySQL 데이터베이스를 연결 합니다.
toosee hello 연결 정보에 대 한 새 MySQL 데이터베이스를 클릭 하기만 **속성** 웹 앱의 블레이드에서 합니다.

![Azure에서 MySQL 데이터베이스 만들기- MySQL 데이터베이스 블레이드](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

이제 모든 웹앱에서 연결 정보를 사용할 수 있습니다. 간단한 PHP 응용 프로그램에서 toouse hello 연결 정보를 제공 하는 방법을 보여 주는 샘플 [여기](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql)합니다.

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a>Hello PHP get 시작된 자습서) (에서 Laravel 웹 앱에 연결
완료 된 hello 자습서 한다고 가정해 보세요 [만들기, 구성 및 PHP 웹 응용 프로그램 tooAzure 배포](app-service-web/app-service-web-php-get-started.md) 있고는 [Laravel](https://www.laravel.com/) Azure에서 실행 되는 웹 응용 프로그램입니다. 데이터베이스 기능 tooyour Laravel 응용 프로그램을 쉽게 추가할 수 있습니다. 아래 hello 단계를 수행 합니다.

> [!NOTE]
> hello 다음 단계에서는 가정 hello 자습서를 완료 했으면 [만들기, 구성 및 PHP 웹 응용 프로그램 tooAzure 배포](app-service-web/app-service-web-php-get-started.md)합니다.
>
>

1. 로컬 개발 환경 toopoint toohello MySQL 데이터베이스에서 hello Laravel 응용 프로그램을 구성 합니다. toodo이,이 오픈 `.env` Laravel 앱에서 루트 디렉터리 및 hello MySQL 데이터베이스 옵션을 구성 합니다.

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > Hello에 **속성** 블레이드에서 MySQL 데이터베이스의 이름을 hello 되거나 하나 hello 보이지 않을 hello에 **데이터베이스 이름** 필드입니다. 더 나은 toocheck hello 데이터베이스 매개 변수에서 hello **연결 문자열** 필드입니다.    
   >
   > ![Azure에서 MySQL 데이터베이스 만들기 - 진행 중](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. hello 액세스할 수 있는지 MySQL 이제 가장 빠른 방법은 tooverify은 toouse [Laravel의 기본 인증 스 캐 폴딩](https://laravel.com/docs/5.2/authentication#authentication-quickstart)합니다.
   Hello 명령줄 터미널 hello 명령을 Laravel 응용 프로그램의 루트 디렉터리에서 다음을 실행 합니다.

         php artisan migrate
         php artisan make:auth

    첫 번째 명령은 hello hello에 미리 정의 된 마이그레이션에 따라 Azure의 hello 테이블을 만듭니다 `database/migrations` 디렉터리 및 hello 두 번째 명령은 스 캐 폴드 hello 기본 뷰 및 사용자 등록 및 인증에 대 한 경로입니다.
3. 이제 hello 개발 서버를 실행 합니다.

        php artisan serve
4. Hello 브라우저에서 toohttp://localhost:8000 이동한 표시 된 대로 새 사용자를 등록 합니다.

    ![Azure에서 tooMySQL 데이터베이스 연결-사용자 등록](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    Hello UI 프롬프트 완료 hello 등록을 수행 합니다. 등록이 완료되면 로그인됩니다.

    ![Azure에서 tooMySQL 데이터베이스 연결-사용자 등록](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    이제 Azure의 hello MySQL 데이터베이스에 대 한 응용 프로그램 개발 하는 합니다.
5. 이제, 하기만 하면 tooreplicate 프로그램 `.env` 설정 tooyour Azure 웹 앱입니다. Hello 다음 Azure CLI 명령을 실행 합니다.

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. 다음으로 커밋하고 푸시합니다 tooAzure hello 로컬 변경 내용을 실행 하는 동안 이전에 만든 `php artisan make:auth`합니다.

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. Toohello Azure 웹 앱을 찾습니다.

        azure site browse
8. 앞에서 만든 hello 사용자 자격 증명을 사용 하 여 로그인 합니다.

    ![Azure에서 tooMySQL 데이터베이스 연결-tooAzure 웹 응용 프로그램 찾아보기](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    에 로그인 한 후 hello 친숙 한 사후 로그인 화면을 표시 되어야 합니다.

    ![Azure-로그인에서 tooMySQL 데이터베이스 연결](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    축하합니다. 이제 Azure의 PHP 웹앱으로 MySQL 데이터베이스에서 데이터에 액세스합니다.

## <a name="next-steps"></a>다음 단계
자세한 내용은 참조 hello [PHP 개발자 센터](/develop/php/)합니다.
