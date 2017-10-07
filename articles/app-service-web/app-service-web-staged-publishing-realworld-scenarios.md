---
title: "웹 앱에 대 한 효과적으로 aaaUse DevOps 환경 | Microsoft Docs"
description: "응용 프로그램에 대 한 여러 개발 환경을 관리 하 고 toouse 배포 tooset를 슬롯 하는 방법에 대해 알아봅니다"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 16a594dc-61f5-4984-b5ca-9d5abc39fb1e
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 61a552e735a4ad9769b661d7c988744074ba2962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a>웹 앱에서 DevOps 환경을 효과적으로 사용하기
이 문서에서는 어떻게 tooset 및 개발, 스테이징, QA (품질 보증), 프로덕션 등의 다양 한 환경에서 응용 프로그램의 여러 버전을 하는 경우 웹 응용 프로그램 배포를 관리 합니다. 각 버전의 응용 프로그램 배포 프로세스의 hello 특정 목적을 위해 개발 환경으로 간주할 수 있습니다. 예를 들어 개발자는 hello 변경 tooproduction를 강제 하기 전에 hello QA 환경 tootest hello 품질 hello 응용 프로그램을 사용할 수 있습니다.
여러 개발 환경을 challenge tootrack 코드 필요 하기 때문에 (계산, 웹 응용 프로그램, 데이터베이스, 캐시, 등) 리소스를 관리 하 고 코드 환경에서 배포 될 수 있습니다.

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a>비프로덕션 환경(스테이지, 개발, QA) 설정
프로덕션 웹 앱 및 실행 되 면 hello 다음 단계는 비-프로덕션 환경 toocreate입니다. toouse 배포 슬롯 hello Standard 또는 Premium Azure 앱 서비스 계획 모드에서 실행 되 고 있는지 확인 합니다. 배포 슬롯은 자체 호스트 이름을 갖춘 라이브 웹앱입니다. 웹 응용 프로그램 콘텐츠 및 구성 요소는 hello 프로덕션 슬롯을 포함 하 여 두 배포 슬롯 간에 교환할 수 있습니다. 내 응용 프로그램 tooa 배포 슬롯을 배포 하면 혜택을 따라 hello 가져오기:

- Hello 앱 hello 프로덕션 슬롯으로 교환 하기 전에 스테이징 배포 슬롯의 변경 내용을 tooa 웹 앱을 확인할 수 있습니다.
- 웹 앱 tooa 슬롯을 먼저 배포 하 고 프로덕션 환경으로 교체 하는 경우 hello 슬롯의 모든 인스턴스 전에 프로덕션으로 교환 하 준비 됩니다. 이 프로세스는 웹앱을 배포할 때 가동 중지가 발생하지 않습니다. hello 트래픽 리디렉션이 원활 하 게, 고 tooswap 작업 인해 요청 없음이 삭제 됩니다. tooautomate이 전체 워크플로 구성 [자동 교환](web-sites-staged-publishing.md#configure-auto-swap) 사전 교환 유효성 검사가 필요 하지 않습니다.
- 교환, 후 이전에 준비 된 hello 웹 응용 프로그램에는 이제 hello 슬롯 hello 이전 프로덕션 웹 앱을 있습니다. Hello 프로덕션 슬롯으로 교환 된 hello 변경 하면 예상과 다른 경우에 hello을 수행할 수 있습니다 동일한 교환 즉시 tooget 프로그램 "마지막으로 성공한" 웹 응용 프로그램 백 합니다.

스테이징 배포 슬롯을 tooset 참조 [스테이징 환경에서 Azure 앱 서비스 웹 앱에 대 한 설정](web-sites-staged-publishing.md)합니다. 모든 환경에는 고유한 리소스 집합이 있어야 합니다. 예를 들어 웹앱에서 데이터베이스를 사용하는 경우 프로덕션 웹앱과 스테이징 웹앱은 서로 다른 데이터베이스를 사용해야 합니다. 개발 환경을 준비 데이터베이스, 저장소, 또는 캐시 tooset 등 준비 개발 환경 리소스를 추가 합니다.

## <a name="examples-of-using-multiple-development-environments"></a>여러 개발 환경을 사용하는 예
모든 프로젝트는 최소한 두 가지 환경(개발 및 생산)에서 소스 코드 관리를 수행해야 합니다. 콘텐츠 관리 시스템 (CMSs), 응용 프로그램 프레임 워크를 사용 하는 경우 hello 응용 프로그램 사용자 지정 하지 않고이 시나리오를 지원 하지 않습니다. 이러한 상황 hello 다음 섹션에에서 설명 된 hello 인기 있는 프레임 워크의 일부에 적용 됩니다. 다양 한 질문으로 작업할 때 CMS/프레임 워크와 같은 toomind를 가져옵니다.

- 어떻게 수행 하면 분해 hello 콘텐츠를 다른 환경으로?
- 프레임워크 버전 업데이트에 영향을 주지 않고 변경할 수 있는 파일은 무엇입니까?
- 환경별 구성은 어떻게 관리합니까?
- 모듈, 플러그 인 및 hello 핵심 프레임 워크에 대 한 업데이트 된 버전은 어떻게 관리 해야 할까요?

프로젝트에 대 한 여러 환경을를 여러 방법으로 tooset 가지가 있습니다. hello 다음 예제에서는 각 각각의 응용 프로그램에 대 한 한 가지 방법은

### <a name="wordpress"></a>WordPress
이 섹션에서는 사용 하 여 배포 워크플로를 tooset WordPress에 대 한 슬롯 하는 방법을 배웁니다. 대부분의 CMS 솔루션처럼 WordPress도 여러 개발 환경을 지원하려면 사용자 지정해야 합니다. Azure 앱 서비스의 hello 웹 응용 프로그램 기능을 코드 외부에서 쉽게 toostore 구성 설정을 구성 하는 몇 가지 기능이 있습니다.

1. 스테이징 슬롯을 만들기 전에 설정 응용 프로그램 코드 toosupport 여러 환경. toosupport 여러 환경 tooedit 해야 WordPress, `wp-config.php` 로컬 개발에 웹 앱 및 코드 hello 파일 시작 부분의 hello 다음 hello를 추가 합니다. 이 프로세스를 응용 프로그램 toopick hello 올바른 구성 hello 선택한 환경에 따라 사용 하 고 있습니다.

    ```
    // Support multiple environments
    // set hello config file based on current environment
    if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) {
    // local development
     $config_file = 'config/wp-config.local.php';
    }
    elseif ((strpos(getenv('WP_ENV'),'stage') !== false) || (strpos(getenv('WP_ENV'),'prod' )!== false ))
    //single file for all azure development environments
     $config_file = 'config/wp-config.azure.php';
    }
    $path = dirname(__FILE__). '/';
    if (file_exists($path. $config_file)) {
    // include hello config file if it exists, otherwise WP is going toofail
    require_once $path. $config_file;
    ```

2. 호출 하는 웹 응용 프로그램 루트 아래에 폴더 `config`, hello 추가 `wp-config.azure.php` 및 `wp-config.local.php` 파일을 각각 Azure 환경 및 로컬 환경을 나타냅니다.

3. hello 다음 복사 `wp-config.local.php`:

    ```
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this tootrue tooenable hello display of notices during development.
     * It is strongly recommended that plugin and theme developers use WP_DEBUG
     * in their development environments.
     */
    define('WP_DEBUG', true);

    //Security key settings
    define('AUTH_KEY', 'put your unique phrase here');
    define('SECURE_AUTH_KEY','put your unique phrase here');
    define('LOGGED_IN_KEY','put your unique phrase here');
    define('NONCE_KEY', 'put your unique phrase here');
    define('AUTH_SALT', 'put your unique phrase here');
    define('SECURE_AUTH_SALT', 'put your unique phrase here');
    define('LOGGED_IN_SALT', 'put your unique phrase here');
    define('NONCE_SALT', 'put your unique phrase here');

    /**
     * WordPress Database Table prefix.
     *
     * You can have multiple installations in one database if you give each a unique
     * prefix. Only numbers, letters, and underscores please!
     */
    $table_prefix = 'wp_';
    ```

    Hello 이전 코드와 같이 hello 보안 키를 설정 해킹에서 tooprevent 웹 앱을 도움말, 고유 값을 사용 하므로 수 있습니다. Toogenerate hello 문자열 hello 코드에서 언급 한 보안 키를 해야 하는 경우 다음을 할 수 있습니다 [이동 toohello 자동 생성기](https://api.wordpress.org/secret-key/1.1/salt) toocreate 새로운 키/값 쌍입니다.

4. 복사 hello 다음 코드에서는 `wp-config.azure.php`:

    ```    
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', getenv('DB_NAME'));

    /** MySQL database username */
    define('DB_USER', getenv('DB_USER'));

    /** MySQL database password */
    define('DB_PASSWORD', getenv('DB_PASSWORD'));

    /** MySQL hostname */
    define('DB_HOST', getenv('DB_HOST'));

    /**
    * For developers: WordPress debugging mode.
    *
    * Change this tootrue tooenable hello display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging tooinvestigate issues without displaying tooend user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on hello page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need toogenerate hello string for security keys mentioned above, you can go hello automatic generator toocreate new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
    define('AUTH_KEY',getenv('DB_AUTH_KEY'));
    define('SECURE_AUTH_KEY', getenv('DB_SECURE_AUTH_KEY'));
    define('LOGGED_IN_KEY', getenv('DB_LOGGED_IN_KEY'));
    define('NONCE_KEY', getenv('DB_NONCE_KEY'));
    define('AUTH_SALT', getenv('DB_AUTH_SALT'));
    define('SECURE_AUTH_SALT', getenv('DB_SECURE_AUTH_SALT'));
    define('LOGGED_IN_SALT',  getenv('DB_LOGGED_IN_SALT'));
    define('NONCE_SALT',  getenv('DB_NONCE_SALT'));

    /**
    * WordPress Database Table prefix.
    *
    * You can have multiple installations in one database if you give each a unique
    * prefix. Only numbers, letters, and underscores please!
    */
    $table_prefix = getenv('DB_PREFIX');
    ```

#### <a name="use-relative-paths"></a>상대 경로 사용
Hello WordPress 응용 프로그램에서 한 마지막 작업 tooconfigure 상대 경로입니다. WordPress는 hello 데이터베이스 URL 정보를 저장합니다. 이 저장소 tooanother 하나의 환경에서에서 콘텐츠를 이동 더 어려워집니다. 로컬 toostage 또는 스테이지 tooproduction 환경에서 이동 될 때마다 tooupdate hello 데이터베이스가 필요 합니다. 하나의 환경 tooanother를 사용 하 여 hello에서 배포 될 때마다 데이터베이스 배포에 발생할 수 있는 문제의 tooreduce hello 위험 [관련 루트 플러그 인 연결](https://wordpress.org/plugins/root-relative-urls/)는 hello WordPress 관리자를 사용 하 여 설치할 수 있습니다 대시보드입니다.

다음 항목 tooyour hello 추가 `wp-config.php` hello 대기 시키기 전에 파일 `That's all, stop editing!` 메모:

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

Hello 플러그 인 hello 통해 활성화 `Plugins` WordPress 관리자 대시보드에 대 한 메뉴입니다. WordPress 앱에 대한 고정 링크 설정을 저장합니다.

#### <a name="hello-final-wp-configphp-file"></a>최종 hello `wp-config.php` 파일
WordPress 코어 업데이트는 `wp-config.php`, `wp-config.azure.php` 및 `wp-config.local.php` 파일에 영향을 주지 없습니다. 다음은 최종 버전의 hello `wp-config.php` 파일:

```
<?php
/**
 * hello base configurations of hello WordPress.
 *
 * This file has hello following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get hello MySQL settings from your web host.
 *
 * This file is used by hello wp-config.php creation script during the
 * installation. You don't have toouse hello web web app, you can just copy this file
 * too"wp-config.php" and fill in hello values.
 *
 * @package WordPress
 */

// Support multiple environments
// set hello config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include hello config file if it exists, otherwise WP is going toofail
  require_once $path. $config_file;
}

/** Database Charset toouse in creating database tables. */
define('DB_CHARSET', 'utf8');

/** hello Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path toohello WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a>스테이징 환경 설정
1. Azure 구독에서 실행 중인 WordPress 웹 앱이 이미 있는 경우 toohello 로그인 [Azure 포털](http://portal.azure.com), tooyour WordPress 웹 응용 프로그램을 이동 합니다. WordPress 웹 응용 프로그램에 없을 경우 hello Azure Marketplace에서에서 하나를 만들 수 있습니다. toolearn 더 참조 [Azure 앱 서비스에서 WordPress 웹 앱을 만들](web-sites-php-web-site-gallery.md)합니다.
클릭 **설정** > **배포 슬롯** > **추가** toocreate hello 이름의 배포 슬롯을 *단계*. 배포 슬롯은 다른 웹 응용 프로그램 공유 hello 이전에 만든 hello 기본 웹 응용 프로그램으로 동일한 리소스입니다.

    ![스테이지 배포 슬롯 만들기](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. 예를 들어 다른 MySQL 데이터베이스를 추가 `wordpress-stage-db`, tooyour 리소스 그룹 `wordpressapp-group`합니다.

    ![MySQL 데이터베이스 tooresource 그룹 추가](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. 스테이지 배포 슬롯 toopoint toohello 새 데이터베이스에 대 한 hello 연결 문자열 업데이트 `wordpress-stage-db`합니다. 프로덕션 웹 앱 `wordpressprodapp`, 웹 앱을 준비 하 고 `wordpressprodapp-stage`, 지점 toodifferent 데이터베이스 해야 합니다.

#### <a name="configure-environment-specific-app-settings"></a>환경 관련 앱 설정 구성
개발자 hello 구성 정보, 호출의 일부분으로 Azure에서 키/값 문자열 쌍에 저장할 수 있습니다 **앱 설정**, 웹 앱과 연결 된입니다. 런타임 시 웹 응용 프로그램은 자동으로 이러한 값을 검색 하 고 웹 응용 프로그램에서 실행 중인 toocode 사용할 수 있도록 합니다. 보안 측면에서 암호가 포함된 데이터베이스 연결 문자열과 같은 중요한 정보는 `wp-config.php`와 같은 파일에 일반 텍스트로 표시되지 않기 때문에 긍정적인 부수 효과가 있습니다.

단락 뒤 hello에 설명 된이 프로세스는 파일 변경 내용 및 hello WordPress 응용 프로그램에 대 한 데이터베이스 변경 내용을 모두 포함 하기 때문에 유용 합니다.

* WordPress 버전 업그레이드
* 플러그 인 새로 추가, 편집 또는 업그레이드
* 테마 새로 추가, 편집 또는 업그레이드

다음에 대한 앱 설정 구성

* 데이터베이스 정보
* WordPress 로깅 설정/해제
* WordPress 보안 설정

![Wordpress 웹앱에 대한 앱 설정](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

Hello 다음 프로덕션 웹 앱 및 단계 슬롯에 대 한 응용 프로그램 설정을 추가 하 고 있는지 확인 합니다. Hello 프로덕션 웹 앱 및 웹 응용 프로그램을 스테이징 서로 다른 데이터베이스를 사용 하는지 확인 합니다.

1. 지우기 hello **슬롯 설정을** WP_ENV 제외한 모든 hello 설정 매개 변수에 대 한 확인란을 선택 합니다. 이 프로세스 됩니다 웹 앱, 파일 내용 및 데이터베이스에 대 한 hello 구성을 교체 합니다. 경우 **슬롯 설정을** 은 됩니다 hello 웹 앱의 앱 설정 및 연결 문자열 구성 옵션을 선택 *하지* 수행 하는 경우 환경에 걸쳐 이동는 **교체** 작업 합니다. 데이터베이스 변경 내용이 있더라도 프로덕션 웹앱은 손상되지 않습니다.

2. WebMatrix 또는 사용자가 선택한, FTP, Git, 또는 PhpMyAdmin 같은 도구를 사용 하 여 hello 로컬 개발 환경 웹 응용 프로그램 toohello 단계 웹 앱 및 데이터베이스를 배포 합니다.

    ![WordPress 웹앱에 Web Matrix 게시 대화 상자](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. 스테이징 웹앱을 찾아 테스트합니다. 여기서 hello 웹 응용 프로그램의 hello 테마는 toobe 업데이트 시나리오를 고려 하면 웹 앱을 준비 하는 hello 다음과 같습니다.

    ![슬롯 교환 전에 스테이징 웹앱 찾아보기](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. 상태가 양호해 클릭 hello **교체** 콘텐츠 toohello 프로덕션 환경에 스테이징 웹 응용 프로그램 toomove 단추입니다. 이 경우 중 환경에 걸쳐 hello web app 및 hello 데이터베이스 교체 모든 **스왑** 작업 합니다.

    ![WordPress에 대한 변경 내용 미리 보기 교환](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > 시나리오 tooonly 푸시 파일 (어떤 데이터베이스 업데이트)를 필요한 경우를 확인 한 다음 **슬롯 설정을** 데이터베이스와 관련 된 모든 hello에 대 한 *앱 설정* 및 *연결 문자열 설정을*hello에 **웹 앱 설정을** hello hello를 수행 하기 전에 Azure 포털 내에서 블레이드 **교체**합니다. 이 경우 **교환**을 수행할 때 DB_NAME, DB_HOST, DB_PASSWORD, DB_USER 및 기본 연결 문자열 설정이 변경 내용 미리 보기에 표시되지 않아야 합니다. Hello을 완료 하는 경우 지금은 **교체** 작업, WordPress 웹 응용 프로그램은 hello 있는 hello 업데이트 파일에만 해당 합니다.
    >
    >

    이렇게 하면 하기 전에 **교체**, hello 프로덕션 WordPress 웹 앱 다음과 같습니다.
    ![슬롯 교환 전 프로덕션 웹앱](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)

    Hello 후 **교체** 프로덕션 웹 앱에서 작업을 hello 테마 업데이트 되었습니다.

    ![슬롯 교환 후 프로덕션 웹앱](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. Tooroll 다시 필요할 때 toohello 프로덕션 웹 이동할 수 있습니다 **앱 설정**, hello를 클릭 하 고 **교체** tooswap hello 웹 응용 프로그램 및 데이터베이스를 프로덕션 toostaging 슬롯 단추입니다. 데이터베이스 변경 내용에 포함 된 경우는 **교체** 작업, 다음 hello tooyour 스테이징 웹 앱을 배포한 다음에 스테이징 웹 앱에 대 한 toodeploy hello 데이터베이스 변경 내용을 toohello 현재 데이터베이스가 필요 합니다. hello 현재 데이터베이스 hello 이전 프로덕션 데이터베이스 또는 hello 단계 데이터베이스 일 수 있습니다.

#### <a name="summary"></a>요약
다음은 데이터베이스가 있는 모든 응용 프로그램에 일반화된 프로세스입니다.

1. 로컬 환경에 hello 응용 프로그램을 설치 합니다.
2. 환경별 구성(로컬 및 Azure Web Apps) 포함
3. Web Apps의 스테이징 환경 및 프로덕션 환경 설정
4. Azure에서 이미 실행 하는 프로덕션 응용 프로그램의 경우 프로덕션 콘텐츠 (파일/코드 및 데이터베이스) toolocal 및 준비 환경을 동기화 합니다.
5. 로컬 환경에서 응용 프로그램 개발
6. 유지 관리 또는 잠긴된 모드에서 프로덕션 웹 앱 하 고 프로덕션 toostaging 및 개발 환경에서 데이터베이스 콘텐츠를 동기화 합니다.
7. Toohello 준비 환경 및 테스트를 배포 합니다.
8. Tooproduction 환경을 배포 합니다.
9. 4-6단계 반복

### <a name="umbraco"></a>Umbraco
이 섹션에서는 hello Umbraco CMS 다중 DevOps 환경에서 사용자 지정 모듈 toodeploy를 사용 하는 방법을 배웁니다. 이 예에서는 여러 개발 환경을 다른 접근 방식을 toomanaging를 제공합니다.

[Umbraco CMS](http://umbraco.com/)는 많은 개발자가 사용하는 인기 있는 .NET CMS 솔루션이며, Hello 제공 [Courier2](http://umbraco.com/products/more-add-ons/courier-2) 개발 toostaging tooproduction 환경에서 모듈 toodeploy 합니다. Visual Studio 또는 WebMatrix를 사용하여 Umbraco CMS 웹앱용 로컬 개발 환경을 쉽게 만들 수 있습니다.

- [Visual Studio를 사용하여 Umbraco 웹앱 만들기](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [WebMatrix를 사용하여 Umbraco 웹앱 만들기](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

항상 잊지 말고 수행 tooremove hello `install` 응용 프로그램 아래에 폴더 toostage 또는 프로덕션 웹 앱 업로드 되지 않습니다. 이 자습서에서는 WebMatrix를 사용합니다.

#### <a name="set-up-a-staging-environment"></a>스테이징 환경 설정
1. Hello Umbraco CMS 웹 앱이 이미 있는 것으로 가정 하 고 실행 Umbraco CMS 웹 앱에 대 한 앞서 언급 했 듯이 배포 슬롯을 만듭니다. 이렇게 하지 않으면 hello Marketplace에서에서 하나를 만들 수 있습니다.
2. 사용자 단계 배포 슬롯 toopoint toohello 새에 대 한 hello 연결 문자열을 업데이트 **umbraco-단계-db** 데이터베이스입니다. 프로덕션 웹 앱 (umbraositecms-1)과 스테이징 웹 응용 프로그램 (umbracositecms 1 단계) *해야* 지점 toodifferent 데이터베이스.

    ![새 스테이징 데이터베이스를 통해 스테이징 웹앱의 연결 문자열 업데이트](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. 클릭 **제작 가져오기 설정** hello 배포 슬롯에 대 한 **단계**합니다. 이 프로세스는 모든 hello 필요한 정보를 Visual Studio 또는 WebMatrix toopublish hello 로컬 개발 웹 앱 toohello Azure 웹 앱에서 응용 프로그램을 저장 하 여 게시 설정 파일을 다운로드 합니다.

    ![Get 게시의 웹 앱을 준비 하는 hello 설정](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. WebMatrix 또는 Visual Studio에서 로컬 개발 웹앱을 엽니다. 이 자습서에서는 WebMatrix를 사용합니다. 먼저 tooimport hello 스테이징 웹 앱에 대 한 설정 파일을 게시 합니다.

    ![Web Matrix를 사용하여 Umbraco 게시 설정 가져오기](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. Hello 대화 상자의 변경 내용을 검토 하 고 로컬 웹 앱 tooyour Azure 웹 앱을 배포할 *umbracositecms 1 단계*합니다. Hello에 파일을 생략 됩니다 tooyour 스테이징 웹 앱을 직접 파일을 배포 하면 `~/app_data/TEMP/` 폴더 hello 단계 웹 앱이 첫 번째 때 이러한 파일은 다시 생성 됩니다 때문에 시작 합니다. 또한 hello를 생략 해야 `~/app_data/umbraco.config` 파일에도 다시 생성 되지 것입니다.

    ![Web Matrix에서 게시 설정 검토](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. Hello Umbraco 로컬 웹 앱 toohello 스테이징 웹 응용 프로그램을 성공적으로 게시 한 후 tooyour 스테이징 웹 앱을 찾아 문제를 해결 하는 몇 가지 테스트 toorule를 실행 합니다.

#### <a name="set-up-hello-courier2-deployment-module"></a>Hello Courier2 배포 모듈 설정
Hello로 [Courier2](http://umbraco.com/products/more-add-ons/courier-2) 모듈 toopush 콘텐츠, 스타일 시트 및 스테이징 웹 응용 프로그램 tooa 프로덕션 웹 앱의 모듈을 개발 하면 단추로 클릭 합니다. 이 프로세스는 hello를 깰 위험을 프로덕션 웹 앱 업데이트를 배포 하는 경우를 줄입니다.
Hello에 대 한 Courier2에 대 한 라이선스를 구입 `*.azurewebsites.net` 도메인 및 사용자 지정 도메인 (예: http://abc.com). 현재 위치 hello 라이선스 다운로드 hello 라이선스를 구입한 후 (합니다. 파일-사용권 계약) hello에 `bin` 폴더입니다.

![라이선스 파일을 bin 폴더에 넣기](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. [Hello Courier2 패키지 다운로드](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/)합니다. 예를 들어 http://umbracocms-site-stage.azurewebsites.net/umbraco tooyour 단계 웹 앱에서 로그인 hello 클릭 **개발자** 메뉴를 차례로 클릭 **패키지** > **설치 로컬 패키지**합니다.

    ![Umbraco 패키지 설치 관리자](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. Hello 설치 관리자를 사용 하 여 hello Courier2 패키지를 업로드 합니다.

    ![Courier 모듈에 대한 패키지 업로드](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. hello에서 tooupdate hello courier.config 파일이 필요 tooconfigure hello 패키지 **Config** 웹 응용 프로그램의 폴더입니다.

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. `<repositories>`, hello 프로덕션 사이트 URL 및 사용자 정보를 입력 합니다.
    Hello 기본 Umbraco 멤버 자격 공급자를 사용 하는 경우 다음 hello 관리 사용자에 대 한 hello ID에서에서 추가 hello &lt;사용자&gt; 섹션.
    사용자 지정 Umbraco 멤버 자격 공급자를 사용 하는 경우 사용 하 여 `<login>`,`<password>` hello Courier2 모듈 tooconnect toohello 프로덕션 사이트에 있습니다.
    자세한 내용은 [hello Courier2 모듈에 대 한 hello 설명서를 검토](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation)합니다.

5. 마찬가지로, 프로덕션 사이트에 hello Courier2 모듈을 설치 하 고 여기 표시 된 대로 해당 courier.config 파일 toopoint toohello 단계 웹 응용 프로그램을 구성 합니다.

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. Hello 클릭 **Courier2** hello Umbraco CMS 웹 응용 프로그램 대시보드에에서 탭을 클릭 한 다음 **위치**합니다. 설명한 것 처럼 hello 리포지토리 이름이 표시 되어야 `courier.config`합니다. 프로덕션 웹앱 및 스테이징 웹앱 모두에서 이 프로세스를 수행합니다.

    ![대상 웹앱 리포지토리 보기](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. hello 준비 사이트 toohello 프로덕션 사이트의에서 콘텐츠를 toodeploy 너무 이동**콘텐츠**, 기존 페이지를 선택 하거나 새 페이지를 만듭니다. 기존 페이지 hello 페이지의 제목 hello 여기서는 웹 응용 프로그램에서 선택 하겠습니다. **시작-새**, 클릭 하 고 **저장 및 게시**합니다.

    ![페이지 제목 변경 및 게시](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. 마우스 오른쪽 단추로 클릭 hello 페이지 tooview 모든 hello 옵션을 수정합니다. 클릭 **Courier** tooopen hello **배포** 대화 상자. 클릭 **배포** tooinitiate 배포 합니다.

    ![Courier 모듈 배포 대화 상자](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. Hello 변경 내용을 검토 한 다음 클릭 **계속**합니다.

    ![Courier 모듈 배포 대화 상자 변경 내용 검토](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    hello 배포 로그 hello 배포가 성공적으로 수행 하는 경우 표시 됩니다.

     ![Courier 모듈에서 배포 로그 보기](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. Hello 변경 내용이 반영 하는 경우 프로덕션 웹 앱 toosee 사용자를 찾습니다.

     ![프로덕션 웹앱 찾아보기](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

Courier, 검토 toouse 설명서 hello 하는 방법에 대 한 자세한 toolearn 합니다.

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a>Tooupgrade는 Umbraco CMS 버전 hello 하는 방법
Courier이 Umbraco CMS tooanother의 한 버전에서 업그레이드 하는 도움말 되지 않습니다. Umbraco CMS 버전을 업그레이드할 때 사용자 지정 모듈 또는 모듈에서 파트너와의 비 호환성을 확인 하 고 Umbraco 핵심 라이브러리 hello 해야 합니다. 모범 사례는 다음과 같습니다.

* 업그레이드하기 전에 항상 웹앱과 데이터베이스를 백업합니다. Azure에서 웹 앱에 hello 백업 기능을 사용 하 여 웹 사이트에 대 한 자동 백업을 설정 하 고 hello 복원 기능을 사용 하 여 필요한 경우 사이트를 복원할 수 있습니다. 자세한 내용은 참조 하십시오. [어떻게 tooback 웹 앱을](web-sites-backup.md) 및 [어떻게 toorestore 웹 앱](web-sites-restore.md)합니다.
* 파트너 로부터 패키지를 업그레이드 하는 hello 버전과 호환 되는지 확인 합니다. Hello 패키지에 다운로드 페이지, hello 프로젝트 호환성 Umbraco CMS 버전을 검토 합니다.

방법에 대 한 자세한 내용은 tooupgrade 웹 앱을 로컬로 [hello 일반적인 업그레이드 지침 참조](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general)합니다.

로컬 개발 사이트를 업그레이드 한 후 웹 앱을 준비 하는 hello 변경 toohello를 게시 합니다. 응용 프로그램을 테스트합니다. 상태가 양호해 hello를 사용 하 여 **교체** 단추 tooswap 준비 사이트 toohello 프로덕션 웹 앱입니다. Hello를 사용 하는 경우 **교체** 작업을 웹 앱의 구성에 영향을 받을 hello 변경을 볼 수 있습니다. 이 **교체** hello 웹 응용 프로그램 및 데이터베이스 작업을 바꿉니다. Hello 후 **교체**, hello 프로덕션 웹 앱 됩니다 지점 toohello umbraco-단계-db 데이터베이스 및 웹 응용 프로그램 준비 됩니다 지점 tooumbraco prod db 데이터베이스 hello 합니다.

![Umbraco CMS 배포를 위한 교환 미리보기](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

교환 하는 hello 웹 앱과 hello 데이터베이스 둘 다의 장점은 다음과 같습니다.

* 롤백할 수 있습니다 다른 웹 응용 프로그램의 이전 버전 toohello **교체** 응용 프로그램에 문제가 있는 경우.
* 업그레이드 하는 toodeploy 파일 및 웹 응용 프로그램 toohello 프로덕션 웹 앱을 준비 하는 hello에서 데이터베이스 및 데이터베이스 필요 합니다. 파일과 데이터베이스를 배포할 때 많은 문제가 발생할 수 있습니다. Hello를 사용 하 여 **교체** 기능, 슬롯의 업그레이드 하는 동안 가동 중지 시간 감소를 변경 내용을 배포할 때 발생할 수 있는 오류의 hello 위험을 줄일 수 있습니다.
* 작업을 수행할 수 **A / B 테스트** hello를 사용 하 여 [프로덕션 환경에서 테스트](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) 기능입니다.

이 예제를 작성할 수 있는 사용자 지정 모듈 비슷한 tooUmbraco Courier 모듈 toomanage 배포 환경에 걸쳐 hello 플랫폼의 융통성 hello를 표시 합니다.

## <a name="references"></a>참조
[Azure 앱 서비스를 사용하여 Agile 소프트웨어 개발](app-service-agile-software-development.md)

[Azure 앱 서비스에서 웹 앱에 대한 스테이징 환경 설정](web-sites-staged-publishing.md)

[Tooblock 웹 toonon 프로덕션 배포 슬롯을 액세스 하는 방법](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
