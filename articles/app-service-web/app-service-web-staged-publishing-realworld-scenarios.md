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
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="459ed-103">웹 앱에서 DevOps 환경을 효과적으로 사용하기</span><span class="sxs-lookup"><span data-stu-id="459ed-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="459ed-104">이 문서에서는 어떻게 tooset 및 개발, 스테이징, QA (품질 보증), 프로덕션 등의 다양 한 환경에서 응용 프로그램의 여러 버전을 하는 경우 웹 응용 프로그램 배포를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-104">This article shows you how tooset up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="459ed-105">각 버전의 응용 프로그램 배포 프로세스의 hello 특정 목적을 위해 개발 환경으로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-105">Each version of your application can be considered as a development environment for hello specific purpose of your deployment process.</span></span> <span data-ttu-id="459ed-106">예를 들어 개발자는 hello 변경 tooproduction를 강제 하기 전에 hello QA 환경 tootest hello 품질 hello 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-106">For example, developers can use hello QA environment tootest hello quality of hello application before they push hello changes tooproduction.</span></span>
<span data-ttu-id="459ed-107">여러 개발 환경을 challenge tootrack 코드 필요 하기 때문에 (계산, 웹 응용 프로그램, 데이터베이스, 캐시, 등) 리소스를 관리 하 고 코드 환경에서 배포 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-107">Multiple development environments can be a challenge because you need tootrack code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="459ed-108">비프로덕션 환경(스테이지, 개발, QA) 설정</span><span class="sxs-lookup"><span data-stu-id="459ed-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="459ed-109">프로덕션 웹 앱 및 실행 되 면 hello 다음 단계는 비-프로덕션 환경 toocreate입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-109">After a production web app is up and running, hello next step is toocreate a non-production environment.</span></span> <span data-ttu-id="459ed-110">toouse 배포 슬롯 hello Standard 또는 Premium Azure 앱 서비스 계획 모드에서 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-110">toouse deployment slots, make sure that you are running in hello Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="459ed-111">배포 슬롯은 자체 호스트 이름을 갖춘 라이브 웹앱입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="459ed-112">웹 응용 프로그램 콘텐츠 및 구성 요소는 hello 프로덕션 슬롯을 포함 하 여 두 배포 슬롯 간에 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-112">Web app content and configuration elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="459ed-113">내 응용 프로그램 tooa 배포 슬롯을 배포 하면 혜택을 따라 hello 가져오기:</span><span class="sxs-lookup"><span data-stu-id="459ed-113">When you deploy your application tooa deployment slot, you get hello following benefits:</span></span>

- <span data-ttu-id="459ed-114">Hello 앱 hello 프로덕션 슬롯으로 교환 하기 전에 스테이징 배포 슬롯의 변경 내용을 tooa 웹 앱을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-114">You can validate changes tooa web app in a staging deployment slot before you swap hello app with hello production slot.</span></span>
- <span data-ttu-id="459ed-115">웹 앱 tooa 슬롯을 먼저 배포 하 고 프로덕션 환경으로 교체 하는 경우 hello 슬롯의 모든 인스턴스 전에 프로덕션으로 교환 하 준비 됩니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-115">When you deploy a web app tooa slot first and swap it into production, all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="459ed-116">이 프로세스는 웹앱을 배포할 때 가동 중지가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="459ed-117">hello 트래픽 리디렉션이 원활 하 게, 고 tooswap 작업 인해 요청 없음이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-117">hello traffic redirection is seamless, and no requests are dropped due tooswap operations.</span></span> <span data-ttu-id="459ed-118">tooautomate이 전체 워크플로 구성 [자동 교환](web-sites-staged-publishing.md#configure-auto-swap) 사전 교환 유효성 검사가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-118">tooautomate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="459ed-119">교환, 후 이전에 준비 된 hello 웹 응용 프로그램에는 이제 hello 슬롯 hello 이전 프로덕션 웹 앱을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-119">After a swap, hello slot that has hello previously staged web app now has hello previous production web app.</span></span> <span data-ttu-id="459ed-120">Hello 프로덕션 슬롯으로 교환 된 hello 변경 하면 예상과 다른 경우에 hello을 수행할 수 있습니다 동일한 교환 즉시 tooget 프로그램 "마지막으로 성공한" 웹 응용 프로그램 백 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-120">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good" web app back.</span></span>

<span data-ttu-id="459ed-121">스테이징 배포 슬롯을 tooset 참조 [스테이징 환경에서 Azure 앱 서비스 웹 앱에 대 한 설정](web-sites-staged-publishing.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-121">tooset up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="459ed-122">모든 환경에는 고유한 리소스 집합이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="459ed-123">예를 들어 웹앱에서 데이터베이스를 사용하는 경우 프로덕션 웹앱과 스테이징 웹앱은 서로 다른 데이터베이스를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="459ed-124">개발 환경을 준비 데이터베이스, 저장소, 또는 캐시 tooset 등 준비 개발 환경 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-124">Add staging development environment resources such as database, storage, or cache tooset your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="459ed-125">여러 개발 환경을 사용하는 예</span><span class="sxs-lookup"><span data-stu-id="459ed-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="459ed-126">모든 프로젝트는 최소한 두 가지 환경(개발 및 생산)에서 소스 코드 관리를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="459ed-127">콘텐츠 관리 시스템 (CMSs), 응용 프로그램 프레임 워크를 사용 하는 경우 hello 응용 프로그램 사용자 지정 하지 않고이 시나리오를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-127">If you use content management systems (CMSs), application frameworks, etc., hello application might not support this scenario without customization.</span></span> <span data-ttu-id="459ed-128">이러한 상황 hello 다음 섹션에에서 설명 된 hello 인기 있는 프레임 워크의 일부에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-128">This eventuality is true for some of hello popular frameworks that are discussed in hello following sections.</span></span> <span data-ttu-id="459ed-129">다양 한 질문으로 작업할 때 CMS/프레임 워크와 같은 toomind를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-129">Lots of questions come toomind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="459ed-130">어떻게 수행 하면 분해 hello 콘텐츠를 다른 환경으로?</span><span class="sxs-lookup"><span data-stu-id="459ed-130">How do you break hello content out into different environments?</span></span>
- <span data-ttu-id="459ed-131">프레임워크 버전 업데이트에 영향을 주지 않고 변경할 수 있는 파일은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="459ed-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="459ed-132">환경별 구성은 어떻게 관리합니까?</span><span class="sxs-lookup"><span data-stu-id="459ed-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="459ed-133">모듈, 플러그 인 및 hello 핵심 프레임 워크에 대 한 업데이트 된 버전은 어떻게 관리 해야 할까요?</span><span class="sxs-lookup"><span data-stu-id="459ed-133">How do you manage version updates for modules, plugins, and hello core framework?</span></span>

<span data-ttu-id="459ed-134">프로젝트에 대 한 여러 환경을를 여러 방법으로 tooset 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-134">There are many ways tooset up multiple environments for your project.</span></span> <span data-ttu-id="459ed-135">hello 다음 예제에서는 각 각각의 응용 프로그램에 대 한 한 가지 방법은</span><span class="sxs-lookup"><span data-stu-id="459ed-135">hello following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="459ed-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="459ed-136">WordPress</span></span>
<span data-ttu-id="459ed-137">이 섹션에서는 사용 하 여 배포 워크플로를 tooset WordPress에 대 한 슬롯 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-137">In this section, you will learn how tooset up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="459ed-138">대부분의 CMS 솔루션처럼 WordPress도 여러 개발 환경을 지원하려면 사용자 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="459ed-139">Azure 앱 서비스의 hello 웹 응용 프로그램 기능을 코드 외부에서 쉽게 toostore 구성 설정을 구성 하는 몇 가지 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-139">hello Web Apps feature of Azure App Service has a few features that make it easy toostore configuration settings outside your code.</span></span>

1. <span data-ttu-id="459ed-140">스테이징 슬롯을 만들기 전에 설정 응용 프로그램 코드 toosupport 여러 환경.</span><span class="sxs-lookup"><span data-stu-id="459ed-140">Before you create a staging slot, set up your application code toosupport multiple environments.</span></span> <span data-ttu-id="459ed-141">toosupport 여러 환경 tooedit 해야 WordPress, `wp-config.php` 로컬 개발에 웹 앱 및 코드 hello 파일 시작 부분의 hello 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-141">toosupport multiple environments in WordPress, you need tooedit `wp-config.php` on your local development web app and add hello following code at hello beginning of hello file.</span></span> <span data-ttu-id="459ed-142">이 프로세스를 응용 프로그램 toopick hello 올바른 구성 hello 선택한 환경에 따라 사용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-142">This process will enable your application toopick hello correct configuration based on hello selected environment.</span></span>

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

2. <span data-ttu-id="459ed-143">호출 하는 웹 응용 프로그램 루트 아래에 폴더 `config`, hello 추가 `wp-config.azure.php` 및 `wp-config.local.php` 파일을 각각 Azure 환경 및 로컬 환경을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-143">Create a folder under web app root called `config`, and add hello `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="459ed-144">hello 다음 복사 `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="459ed-144">Copy hello following in `wp-config.local.php`:</span></span>

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

    <span data-ttu-id="459ed-145">Hello 이전 코드와 같이 hello 보안 키를 설정 해킹에서 tooprevent 웹 앱을 도움말, 고유 값을 사용 하므로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-145">Setting hello security keys as illustrated in hello previous code can help tooprevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="459ed-146">Toogenerate hello 문자열 hello 코드에서 언급 한 보안 키를 해야 하는 경우 다음을 할 수 있습니다 [이동 toohello 자동 생성기](https://api.wordpress.org/secret-key/1.1/salt) toocreate 새로운 키/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-146">If you need toogenerate hello string for security keys mentioned in hello code, you can [go toohello automatic generator](https://api.wordpress.org/secret-key/1.1/salt) toocreate new key/value pairs.</span></span>

4. <span data-ttu-id="459ed-147">복사 hello 다음 코드에서는 `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="459ed-147">Copy hello following code in `wp-config.azure.php`:</span></span>

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

#### <a name="use-relative-paths"></a><span data-ttu-id="459ed-148">상대 경로 사용</span><span class="sxs-lookup"><span data-stu-id="459ed-148">Use relative paths</span></span>
<span data-ttu-id="459ed-149">Hello WordPress 응용 프로그램에서 한 마지막 작업 tooconfigure 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-149">One last thing tooconfigure in hello WordPress app is relative paths.</span></span> <span data-ttu-id="459ed-150">WordPress는 hello 데이터베이스 URL 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-150">WordPress stores URL information in hello database.</span></span> <span data-ttu-id="459ed-151">이 저장소 tooanother 하나의 환경에서에서 콘텐츠를 이동 더 어려워집니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-151">This storage makes moving content from one environment tooanother more difficult.</span></span> <span data-ttu-id="459ed-152">로컬 toostage 또는 스테이지 tooproduction 환경에서 이동 될 때마다 tooupdate hello 데이터베이스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-152">You need tooupdate hello database every time you move from local toostage or stage tooproduction environments.</span></span> <span data-ttu-id="459ed-153">하나의 환경 tooanother를 사용 하 여 hello에서 배포 될 때마다 데이터베이스 배포에 발생할 수 있는 문제의 tooreduce hello 위험 [관련 루트 플러그 인 연결](https://wordpress.org/plugins/root-relative-urls/)는 hello WordPress 관리자를 사용 하 여 설치할 수 있습니다 대시보드입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-153">tooreduce hello risk of issues that can be caused with deploying a database every time you deploy from one environment tooanother, use hello [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using hello WordPress administrator dashboard.</span></span>

<span data-ttu-id="459ed-154">다음 항목 tooyour hello 추가 `wp-config.php` hello 대기 시키기 전에 파일 `That's all, stop editing!` 메모:</span><span class="sxs-lookup"><span data-stu-id="459ed-154">Add hello following entries tooyour `wp-config.php` file before hello `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="459ed-155">Hello 플러그 인 hello 통해 활성화 `Plugins` WordPress 관리자 대시보드에 대 한 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-155">Activate hello plugin through hello `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="459ed-156">WordPress 앱에 대한 고정 링크 설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="hello-final-wp-configphp-file"></a><span data-ttu-id="459ed-157">최종 hello `wp-config.php` 파일</span><span class="sxs-lookup"><span data-stu-id="459ed-157">hello final `wp-config.php` file</span></span>
<span data-ttu-id="459ed-158">WordPress 코어 업데이트는 `wp-config.php`, `wp-config.azure.php` 및 `wp-config.local.php` 파일에 영향을 주지 없습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="459ed-159">다음은 최종 버전의 hello `wp-config.php` 파일:</span><span class="sxs-lookup"><span data-stu-id="459ed-159">Here's a final version of hello `wp-config.php` file:</span></span>

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

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="459ed-160">스테이징 환경 설정</span><span class="sxs-lookup"><span data-stu-id="459ed-160">Set up a staging environment</span></span>
1. <span data-ttu-id="459ed-161">Azure 구독에서 실행 중인 WordPress 웹 앱이 이미 있는 경우 toohello 로그인 [Azure 포털](http://portal.azure.com), tooyour WordPress 웹 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-161">If you already have a WordPress web app running on your Azure subscription, sign in toohello [Azure portal](http://portal.azure.com), and then go tooyour WordPress web app.</span></span> <span data-ttu-id="459ed-162">WordPress 웹 응용 프로그램에 없을 경우 hello Azure Marketplace에서에서 하나를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-162">If you don't have a WordPress web app, you can create one from hello Azure Marketplace.</span></span> <span data-ttu-id="459ed-163">toolearn 더 참조 [Azure 앱 서비스에서 WordPress 웹 앱을 만들](web-sites-php-web-site-gallery.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-163">toolearn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="459ed-164">클릭 **설정** > **배포 슬롯** > **추가** toocreate hello 이름의 배포 슬롯을 *단계*.</span><span class="sxs-lookup"><span data-stu-id="459ed-164">Click **Settings** > **Deployment slots** > **Add** toocreate a deployment slot with hello name *stage*.</span></span> <span data-ttu-id="459ed-165">배포 슬롯은 다른 웹 응용 프로그램 공유 hello 이전에 만든 hello 기본 웹 응용 프로그램으로 동일한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-165">A deployment slot is another web application that shares hello same resources as hello primary web app that you created previously.</span></span>

    ![스테이지 배포 슬롯 만들기](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="459ed-167">예를 들어 다른 MySQL 데이터베이스를 추가 `wordpress-stage-db`, tooyour 리소스 그룹 `wordpressapp-group`합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-167">Add another MySQL database, say `wordpress-stage-db`, tooyour resource group, `wordpressapp-group`.</span></span>

    ![MySQL 데이터베이스 tooresource 그룹 추가](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="459ed-169">스테이지 배포 슬롯 toopoint toohello 새 데이터베이스에 대 한 hello 연결 문자열 업데이트 `wordpress-stage-db`합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-169">Update hello connection strings for your stage deployment slot toopoint toohello new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="459ed-170">프로덕션 웹 앱 `wordpressprodapp`, 웹 앱을 준비 하 고 `wordpressprodapp-stage`, 지점 toodifferent 데이터베이스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point toodifferent databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="459ed-171">환경 관련 앱 설정 구성</span><span class="sxs-lookup"><span data-stu-id="459ed-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="459ed-172">개발자 hello 구성 정보, 호출의 일부분으로 Azure에서 키/값 문자열 쌍에 저장할 수 있습니다 **앱 설정**, 웹 앱과 연결 된입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-172">Developers can store key/value string pairs in Azure as part of hello configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="459ed-173">런타임 시 웹 응용 프로그램은 자동으로 이러한 값을 검색 하 고 웹 응용 프로그램에서 실행 중인 toocode 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-173">At runtime, web apps automatically retrieve these values and make them available toocode that's running in your web app.</span></span> <span data-ttu-id="459ed-174">보안 측면에서 암호가 포함된 데이터베이스 연결 문자열과 같은 중요한 정보는 `wp-config.php`와 같은 파일에 일반 텍스트로 표시되지 않기 때문에 긍정적인 부수 효과가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="459ed-175">단락 뒤 hello에 설명 된이 프로세스는 파일 변경 내용 및 hello WordPress 응용 프로그램에 대 한 데이터베이스 변경 내용을 모두 포함 하기 때문에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-175">This process, which is explained in hello following paragraphs, is useful because it includes both file changes and database changes for hello WordPress app:</span></span>

* <span data-ttu-id="459ed-176">WordPress 버전 업그레이드</span><span class="sxs-lookup"><span data-stu-id="459ed-176">WordPress version upgrade</span></span>
* <span data-ttu-id="459ed-177">플러그 인 새로 추가, 편집 또는 업그레이드</span><span class="sxs-lookup"><span data-stu-id="459ed-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="459ed-178">테마 새로 추가, 편집 또는 업그레이드</span><span class="sxs-lookup"><span data-stu-id="459ed-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="459ed-179">다음에 대한 앱 설정 구성</span><span class="sxs-lookup"><span data-stu-id="459ed-179">Configure app settings for:</span></span>

* <span data-ttu-id="459ed-180">데이터베이스 정보</span><span class="sxs-lookup"><span data-stu-id="459ed-180">Database information</span></span>
* <span data-ttu-id="459ed-181">WordPress 로깅 설정/해제</span><span class="sxs-lookup"><span data-stu-id="459ed-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="459ed-182">WordPress 보안 설정</span><span class="sxs-lookup"><span data-stu-id="459ed-182">WordPress security settings</span></span>

![Wordpress 웹앱에 대한 앱 설정](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="459ed-184">Hello 다음 프로덕션 웹 앱 및 단계 슬롯에 대 한 응용 프로그램 설정을 추가 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-184">Make sure that you add hello following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="459ed-185">Hello 프로덕션 웹 앱 및 웹 응용 프로그램을 스테이징 서로 다른 데이터베이스를 사용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-185">Note that hello production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="459ed-186">지우기 hello **슬롯 설정을** WP_ENV 제외한 모든 hello 설정 매개 변수에 대 한 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-186">Clear hello **Slot Setting** checkbox for all hello settings parameters except WP_ENV.</span></span> <span data-ttu-id="459ed-187">이 프로세스 됩니다 웹 앱, 파일 내용 및 데이터베이스에 대 한 hello 구성을 교체 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-187">This process will swap hello configuration for your web app, file content, and database.</span></span> <span data-ttu-id="459ed-188">경우 **슬롯 설정을** 은 됩니다 hello 웹 앱의 앱 설정 및 연결 문자열 구성 옵션을 선택 *하지* 수행 하는 경우 환경에 걸쳐 이동는 **교체** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-188">If **Slot Setting** is checked, hello web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="459ed-189">데이터베이스 변경 내용이 있더라도 프로덕션 웹앱은 손상되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="459ed-190">WebMatrix 또는 사용자가 선택한, FTP, Git, 또는 PhpMyAdmin 같은 도구를 사용 하 여 hello 로컬 개발 환경 웹 응용 프로그램 toohello 단계 웹 앱 및 데이터베이스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-190">Deploy hello local development environment web app toohello stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![WordPress 웹앱에 Web Matrix 게시 대화 상자](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="459ed-192">스테이징 웹앱을 찾아 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-192">Browse and test your staging web app.</span></span> <span data-ttu-id="459ed-193">여기서 hello 웹 응용 프로그램의 hello 테마는 toobe 업데이트 시나리오를 고려 하면 웹 앱을 준비 하는 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-193">Considering a scenario where hello theme of hello web app is toobe updated, here is hello staging web app.</span></span>

    ![슬롯 교환 전에 스테이징 웹앱 찾아보기](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="459ed-195">상태가 양호해 클릭 hello **교체** 콘텐츠 toohello 프로덕션 환경에 스테이징 웹 응용 프로그램 toomove 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-195">If all looks good, click hello **Swap** button on your staging web app toomove your content toohello production environment.</span></span> <span data-ttu-id="459ed-196">이 경우 중 환경에 걸쳐 hello web app 및 hello 데이터베이스 교체 모든 **스왑** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-196">In this case, you swap hello web app and hello database across environments during every **Swap** operation.</span></span>

    ![WordPress에 대한 변경 내용 미리 보기 교환](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="459ed-198">시나리오 tooonly 푸시 파일 (어떤 데이터베이스 업데이트)를 필요한 경우를 확인 한 다음 **슬롯 설정을** 데이터베이스와 관련 된 모든 hello에 대 한 *앱 설정* 및 *연결 문자열 설정을*hello에 **웹 앱 설정을** hello hello를 수행 하기 전에 Azure 포털 내에서 블레이드 **교체**합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-198">If your scenario needs tooonly push files (no database updates), then check **Slot Setting** for all hello database-related *app settings* and *connection strings settings* in hello **Web App Settings** blade within hello Azure portal before doing hello **Swap**.</span></span> <span data-ttu-id="459ed-199">이 경우 **교환**을 수행할 때 DB_NAME, DB_HOST, DB_PASSWORD, DB_USER 및 기본 연결 문자열 설정이 변경 내용 미리 보기에 표시되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="459ed-200">Hello을 완료 하는 경우 지금은 **교체** 작업, WordPress 웹 응용 프로그램은 hello 있는 hello 업데이트 파일에만 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-200">At this time, when you complete hello **Swap** operation, hello WordPress web app will have hello updates files only.</span></span>
    >
    >

    <span data-ttu-id="459ed-201">이렇게 하면 하기 전에 **교체**, hello 프로덕션 WordPress 웹 앱 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-201">Before doing a **Swap**, here is hello production WordPress web app.</span></span>
    <span data-ttu-id="459ed-202">![슬롯 교환 전 프로덕션 웹앱](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="459ed-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="459ed-203">Hello 후 **교체** 프로덕션 웹 앱에서 작업을 hello 테마 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-203">After hello **Swap** operation, hello theme has been updated on your production web app.</span></span>

    ![슬롯 교환 후 프로덕션 웹앱](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="459ed-205">Tooroll 다시 필요할 때 toohello 프로덕션 웹 이동할 수 있습니다 **앱 설정**, hello를 클릭 하 고 **교체** tooswap hello 웹 응용 프로그램 및 데이터베이스를 프로덕션 toostaging 슬롯 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-205">When you need tooroll back, you can go toohello production web **App Settings**, and click hello **Swap** button tooswap hello web app and database from production toostaging slot.</span></span> <span data-ttu-id="459ed-206">데이터베이스 변경 내용에 포함 된 경우는 **교체** 작업, 다음 hello tooyour 스테이징 웹 앱을 배포한 다음에 스테이징 웹 앱에 대 한 toodeploy hello 데이터베이스 변경 내용을 toohello 현재 데이터베이스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-206">Remember that if database changes are included with a **Swap** operation, then hello next time you deploy tooyour staging web app, you need toodeploy hello database changes toohello current database for your staging web app.</span></span> <span data-ttu-id="459ed-207">hello 현재 데이터베이스 hello 이전 프로덕션 데이터베이스 또는 hello 단계 데이터베이스 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-207">hello current database might be hello previous production database or hello stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="459ed-208">요약</span><span class="sxs-lookup"><span data-stu-id="459ed-208">Summary</span></span>
<span data-ttu-id="459ed-209">다음은 데이터베이스가 있는 모든 응용 프로그램에 일반화된 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="459ed-210">로컬 환경에 hello 응용 프로그램을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-210">Install hello application on your local environment.</span></span>
2. <span data-ttu-id="459ed-211">환경별 구성(로컬 및 Azure Web Apps) 포함</span><span class="sxs-lookup"><span data-stu-id="459ed-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="459ed-212">Web Apps의 스테이징 환경 및 프로덕션 환경 설정</span><span class="sxs-lookup"><span data-stu-id="459ed-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="459ed-213">Azure에서 이미 실행 하는 프로덕션 응용 프로그램의 경우 프로덕션 콘텐츠 (파일/코드 및 데이터베이스) toolocal 및 준비 환경을 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-213">If you have a production application already running on Azure, sync your production content (files/code and database) toolocal and staging environments.</span></span>
5. <span data-ttu-id="459ed-214">로컬 환경에서 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="459ed-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="459ed-215">유지 관리 또는 잠긴된 모드에서 프로덕션 웹 앱 하 고 프로덕션 toostaging 및 개발 환경에서 데이터베이스 콘텐츠를 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-215">Place your production web app under maintenance or locked mode, and sync database content from production toostaging and dev environments.</span></span>
7. <span data-ttu-id="459ed-216">Toohello 준비 환경 및 테스트를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-216">Deploy toohello staging environment and test.</span></span>
8. <span data-ttu-id="459ed-217">Tooproduction 환경을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-217">Deploy tooproduction environment.</span></span>
9. <span data-ttu-id="459ed-218">4-6단계 반복</span><span class="sxs-lookup"><span data-stu-id="459ed-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="459ed-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="459ed-219">Umbraco</span></span>
<span data-ttu-id="459ed-220">이 섹션에서는 hello Umbraco CMS 다중 DevOps 환경에서 사용자 지정 모듈 toodeploy를 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-220">In this section, you will learn how hello Umbraco CMS uses a custom module toodeploy across multiple DevOps environments.</span></span> <span data-ttu-id="459ed-221">이 예에서는 여러 개발 환경을 다른 접근 방식을 toomanaging를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-221">This example provides a different approach toomanaging multiple development environments.</span></span>

<span data-ttu-id="459ed-222">[Umbraco CMS](http://umbraco.com/)는 많은 개발자가 사용하는 인기 있는 .NET CMS 솔루션이며,</span><span class="sxs-lookup"><span data-stu-id="459ed-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="459ed-223">Hello 제공 [Courier2](http://umbraco.com/products/more-add-ons/courier-2) 개발 toostaging tooproduction 환경에서 모듈 toodeploy 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-223">It provides hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module toodeploy from development toostaging tooproduction environments.</span></span> <span data-ttu-id="459ed-224">Visual Studio 또는 WebMatrix를 사용하여 Umbraco CMS 웹앱용 로컬 개발 환경을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="459ed-225">Visual Studio를 사용하여 Umbraco 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="459ed-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="459ed-226">WebMatrix를 사용하여 Umbraco 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="459ed-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="459ed-227">항상 잊지 말고 수행 tooremove hello `install` 응용 프로그램 아래에 폴더 toostage 또는 프로덕션 웹 앱 업로드 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-227">Always remember tooremove hello `install` folder under your application, and never upload it toostage or production web apps.</span></span> <span data-ttu-id="459ed-228">이 자습서에서는 WebMatrix를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="459ed-229">스테이징 환경 설정</span><span class="sxs-lookup"><span data-stu-id="459ed-229">Set up a staging environment</span></span>
1. <span data-ttu-id="459ed-230">Hello Umbraco CMS 웹 앱이 이미 있는 것으로 가정 하 고 실행 Umbraco CMS 웹 앱에 대 한 앞서 언급 했 듯이 배포 슬롯을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-230">Create a deployment slot as mentioned previously for hello Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="459ed-231">이렇게 하지 않으면 hello Marketplace에서에서 하나를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-231">If you do not, you can create one from hello Marketplace.</span></span>
2. <span data-ttu-id="459ed-232">사용자 단계 배포 슬롯 toopoint toohello 새에 대 한 hello 연결 문자열을 업데이트 **umbraco-단계-db** 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-232">Update hello connection string for your stage deployment slot toopoint toohello new **umbraco-stage-db** database.</span></span> <span data-ttu-id="459ed-233">프로덕션 웹 앱 (umbraositecms-1)과 스테이징 웹 응용 프로그램 (umbracositecms 1 단계) *해야* 지점 toodifferent 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="459ed-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point toodifferent databases.</span></span>

    ![새 스테이징 데이터베이스를 통해 스테이징 웹앱의 연결 문자열 업데이트](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="459ed-235">클릭 **제작 가져오기 설정** hello 배포 슬롯에 대 한 **단계**합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-235">Click **Get Publish settings** for hello deployment slot **stage**.</span></span> <span data-ttu-id="459ed-236">이 프로세스는 모든 hello 필요한 정보를 Visual Studio 또는 WebMatrix toopublish hello 로컬 개발 웹 앱 toohello Azure 웹 앱에서 응용 프로그램을 저장 하 여 게시 설정 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-236">This process will download a publish settings file that stores all hello information that Visual Studio or WebMatrix requires toopublish your application from hello local development web app toohello Azure web app.</span></span>

    ![Get 게시의 웹 앱을 준비 하는 hello 설정](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="459ed-238">WebMatrix 또는 Visual Studio에서 로컬 개발 웹앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="459ed-239">이 자습서에서는 WebMatrix를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="459ed-240">먼저 tooimport hello 스테이징 웹 앱에 대 한 설정 파일을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-240">First, you need tooimport hello publish settings file for your staging web app.</span></span>

    ![Web Matrix를 사용하여 Umbraco 게시 설정 가져오기](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="459ed-242">Hello 대화 상자의 변경 내용을 검토 하 고 로컬 웹 앱 tooyour Azure 웹 앱을 배포할 *umbracositecms 1 단계*합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-242">Review changes in hello dialog box, and deploy your local web app tooyour Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="459ed-243">Hello에 파일을 생략 됩니다 tooyour 스테이징 웹 앱을 직접 파일을 배포 하면 `~/app_data/TEMP/` 폴더 hello 단계 웹 앱이 첫 번째 때 이러한 파일은 다시 생성 됩니다 때문에 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-243">When you deploy files directly tooyour staging web app, you will omit files in hello `~/app_data/TEMP/` folder because these files will be regenerated when hello stage web app is first started.</span></span> <span data-ttu-id="459ed-244">또한 hello를 생략 해야 `~/app_data/umbraco.config` 파일에도 다시 생성 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-244">You should also omit hello `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Web Matrix에서 게시 설정 검토](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="459ed-246">Hello Umbraco 로컬 웹 앱 toohello 스테이징 웹 응용 프로그램을 성공적으로 게시 한 후 tooyour 스테이징 웹 앱을 찾아 문제를 해결 하는 몇 가지 테스트 toorule를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-246">After you successfully publish hello Umbraco local web app toohello staging web app, browse tooyour staging web app, and run a few tests toorule out any issues.</span></span>

#### <a name="set-up-hello-courier2-deployment-module"></a><span data-ttu-id="459ed-247">Hello Courier2 배포 모듈 설정</span><span class="sxs-lookup"><span data-stu-id="459ed-247">Set up hello Courier2 deployment module</span></span>
<span data-ttu-id="459ed-248">Hello로 [Courier2](http://umbraco.com/products/more-add-ons/courier-2) 모듈 toopush 콘텐츠, 스타일 시트 및 스테이징 웹 응용 프로그램 tooa 프로덕션 웹 앱의 모듈을 개발 하면 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-248">With hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click toopush content, style sheets, and development modules from a staging web app tooa production web app.</span></span> <span data-ttu-id="459ed-249">이 프로세스는 hello를 깰 위험을 프로덕션 웹 앱 업데이트를 배포 하는 경우를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-249">This process reduces hello risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="459ed-250">Hello에 대 한 Courier2에 대 한 라이선스를 구입 `*.azurewebsites.net` 도메인 및 사용자 지정 도메인 (예: http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="459ed-250">Purchase a license for Courier2 for hello `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="459ed-251">현재 위치 hello 라이선스 다운로드 hello 라이선스를 구입한 후 (합니다. 파일-사용권 계약) hello에 `bin` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-251">After you purchase hello license, place hello downloaded license (.LIC file) in hello `bin` folder.</span></span>

![라이선스 파일을 bin 폴더에 넣기](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="459ed-253">[Hello Courier2 패키지 다운로드](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/)합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-253">[Download hello Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="459ed-254">예를 들어 http://umbracocms-site-stage.azurewebsites.net/umbraco tooyour 단계 웹 앱에서 로그인 hello 클릭 **개발자** 메뉴를 차례로 클릭 **패키지** > **설치 로컬 패키지**합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-254">Sign in tooyour stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click hello **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Umbraco 패키지 설치 관리자](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="459ed-256">Hello 설치 관리자를 사용 하 여 hello Courier2 패키지를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-256">Upload hello Courier2 package by using hello installer.</span></span>

    ![Courier 모듈에 대한 패키지 업로드](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="459ed-258">hello에서 tooupdate hello courier.config 파일이 필요 tooconfigure hello 패키지 **Config** 웹 응용 프로그램의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-258">tooconfigure hello package, you need tooupdate hello courier.config file under hello **Config** folder of your web app.</span></span>

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

4. <span data-ttu-id="459ed-259">`<repositories>`, hello 프로덕션 사이트 URL 및 사용자 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-259">Under `<repositories>`, enter hello production site URL and user information.</span></span>
    <span data-ttu-id="459ed-260">Hello 기본 Umbraco 멤버 자격 공급자를 사용 하는 경우 다음 hello 관리 사용자에 대 한 hello ID에서에서 추가 hello &lt;사용자&gt; 섹션.</span><span class="sxs-lookup"><span data-stu-id="459ed-260">If you are using hello default Umbraco membership provider, then add hello ID for hello Administration user in hello &lt;user&gt; section.</span></span>
    <span data-ttu-id="459ed-261">사용자 지정 Umbraco 멤버 자격 공급자를 사용 하는 경우 사용 하 여 `<login>`,`<password>` hello Courier2 모듈 tooconnect toohello 프로덕션 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in hello Courier2 module tooconnect toohello production site.</span></span>
    <span data-ttu-id="459ed-262">자세한 내용은 [hello Courier2 모듈에 대 한 hello 설명서를 검토](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation)합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-262">For more details, [review hello documentation for hello Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="459ed-263">마찬가지로, 프로덕션 사이트에 hello Courier2 모듈을 설치 하 고 여기 표시 된 대로 해당 courier.config 파일 toopoint toohello 단계 웹 응용 프로그램을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-263">Similarly, install hello Courier2 module on your production site, and configure it toopoint toohello stage web app in its respective courier.config file as shown here.</span></span>

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

6. <span data-ttu-id="459ed-264">Hello 클릭 **Courier2** hello Umbraco CMS 웹 응용 프로그램 대시보드에에서 탭을 클릭 한 다음 **위치**합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-264">Click hello **Courier2** tab in hello Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="459ed-265">설명한 것 처럼 hello 리포지토리 이름이 표시 되어야 `courier.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-265">You should see hello repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="459ed-266">프로덕션 웹앱 및 스테이징 웹앱 모두에서 이 프로세스를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-266">Do this process on both your production and staging web apps.</span></span>

    ![대상 웹앱 리포지토리 보기](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="459ed-268">hello 준비 사이트 toohello 프로덕션 사이트의에서 콘텐츠를 toodeploy 너무 이동**콘텐츠**, 기존 페이지를 선택 하거나 새 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-268">toodeploy content from hello staging site toohello production site, go too**Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="459ed-269">기존 페이지 hello 페이지의 제목 hello 여기서는 웹 응용 프로그램에서 선택 하겠습니다. **시작-새**, 클릭 하 고 **저장 및 게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-269">I will select an existing page from my web app where hello title of hello page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![페이지 제목 변경 및 게시](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="459ed-271">마우스 오른쪽 단추로 클릭 hello 페이지 tooview 모든 hello 옵션을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-271">Right-click hello modified page tooview all hello options.</span></span> <span data-ttu-id="459ed-272">클릭 **Courier** tooopen hello **배포** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="459ed-272">Click **Courier** tooopen hello **Deployment** dialog box.</span></span> <span data-ttu-id="459ed-273">클릭 **배포** tooinitiate 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-273">Click **Deploy** tooinitiate deployment.</span></span>

    ![Courier 모듈 배포 대화 상자](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="459ed-275">Hello 변경 내용을 검토 한 다음 클릭 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-275">Review hello changes, and then click **Continue**.</span></span>

    ![Courier 모듈 배포 대화 상자 변경 내용 검토](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="459ed-277">hello 배포 로그 hello 배포가 성공적으로 수행 하는 경우 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-277">hello deployment log shows if hello deployment was successful.</span></span>

     ![Courier 모듈에서 배포 로그 보기](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="459ed-279">Hello 변경 내용이 반영 하는 경우 프로덕션 웹 앱 toosee 사용자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-279">Browse your production web app toosee if hello changes are reflected.</span></span>

     ![프로덕션 웹앱 찾아보기](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="459ed-281">Courier, 검토 toouse 설명서 hello 하는 방법에 대 한 자세한 toolearn 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-281">toolearn more about how toouse Courier, review hello documentation.</span></span>

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a><span data-ttu-id="459ed-282">Tooupgrade는 Umbraco CMS 버전 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="459ed-282">How tooupgrade hello Umbraco CMS version</span></span>
<span data-ttu-id="459ed-283">Courier이 Umbraco CMS tooanother의 한 버전에서 업그레이드 하는 도움말 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-283">Courier will not help you upgrade from one version of Umbraco CMS tooanother.</span></span> <span data-ttu-id="459ed-284">Umbraco CMS 버전을 업그레이드할 때 사용자 지정 모듈 또는 모듈에서 파트너와의 비 호환성을 확인 하 고 Umbraco 핵심 라이브러리 hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and hello Umbraco Core libraries.</span></span> <span data-ttu-id="459ed-285">모범 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-285">Here are best practices:</span></span>

* <span data-ttu-id="459ed-286">업그레이드하기 전에 항상 웹앱과 데이터베이스를 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="459ed-287">Azure에서 웹 앱에 hello 백업 기능을 사용 하 여 웹 사이트에 대 한 자동 백업을 설정 하 고 hello 복원 기능을 사용 하 여 필요한 경우 사이트를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-287">On web apps in Azure, you can set up automatic backups for your websites by using hello backup feature and restore your site if needed by using hello restore feature.</span></span> <span data-ttu-id="459ed-288">자세한 내용은 참조 하십시오. [어떻게 tooback 웹 앱을](web-sites-backup.md) 및 [어떻게 toorestore 웹 앱](web-sites-restore.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-288">For more details, see [How tooback up your web app](web-sites-backup.md) and [How toorestore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="459ed-289">파트너 로부터 패키지를 업그레이드 하는 hello 버전과 호환 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-289">Check if packages from partners are compatible with hello version you're upgrading to.</span></span> <span data-ttu-id="459ed-290">Hello 패키지에 다운로드 페이지, hello 프로젝트 호환성 Umbraco CMS 버전을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-290">On hello package's download page, review hello project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="459ed-291">방법에 대 한 자세한 내용은 tooupgrade 웹 앱을 로컬로 [hello 일반적인 업그레이드 지침 참조](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general)합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-291">For more details about how tooupgrade your web app locally, [see hello general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="459ed-292">로컬 개발 사이트를 업그레이드 한 후 웹 앱을 준비 하는 hello 변경 toohello를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-292">After your local development site is upgraded, publish hello changes toohello staging web app.</span></span> <span data-ttu-id="459ed-293">응용 프로그램을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-293">Test your application.</span></span> <span data-ttu-id="459ed-294">상태가 양호해 hello를 사용 하 여 **교체** 단추 tooswap 준비 사이트 toohello 프로덕션 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-294">If all looks good, use hello **Swap** button tooswap your staging site toohello production web app.</span></span> <span data-ttu-id="459ed-295">Hello를 사용 하는 경우 **교체** 작업을 웹 앱의 구성에 영향을 받을 hello 변경을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-295">When you use hello **Swap** operation, you can view hello changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="459ed-296">이 **교체** hello 웹 응용 프로그램 및 데이터베이스 작업을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-296">This **Swap** operation swaps hello web apps and databases.</span></span> <span data-ttu-id="459ed-297">Hello 후 **교체**, hello 프로덕션 웹 앱 됩니다 지점 toohello umbraco-단계-db 데이터베이스 및 웹 응용 프로그램 준비 됩니다 지점 tooumbraco prod db 데이터베이스 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-297">After hello **Swap**, hello production web app will point toohello umbraco-stage-db database, and hello staging web app will point tooumbraco-prod-db database.</span></span>

![Umbraco CMS 배포를 위한 교환 미리보기](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="459ed-299">교환 하는 hello 웹 앱과 hello 데이터베이스 둘 다의 장점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-299">Here are advantages of swapping both hello web app and hello database:</span></span>

* <span data-ttu-id="459ed-300">롤백할 수 있습니다 다른 웹 응용 프로그램의 이전 버전 toohello **교체** 응용 프로그램에 문제가 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="459ed-300">You can roll back toohello previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="459ed-301">업그레이드 하는 toodeploy 파일 및 웹 응용 프로그램 toohello 프로덕션 웹 앱을 준비 하는 hello에서 데이터베이스 및 데이터베이스 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-301">For an upgrade, you need toodeploy files and databases from hello staging web app toohello production web app and database.</span></span> <span data-ttu-id="459ed-302">파일과 데이터베이스를 배포할 때 많은 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="459ed-303">Hello를 사용 하 여 **교체** 기능, 슬롯의 업그레이드 하는 동안 가동 중지 시간 감소를 변경 내용을 배포할 때 발생할 수 있는 오류의 hello 위험을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-303">By using hello **Swap** feature of slots, we can reduce downtime during an upgrade and reduce hello risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="459ed-304">작업을 수행할 수 **A / B 테스트** hello를 사용 하 여 [프로덕션 환경에서 테스트](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-304">You can do **A/B testing** by using hello [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="459ed-305">이 예제를 작성할 수 있는 사용자 지정 모듈 비슷한 tooUmbraco Courier 모듈 toomanage 배포 환경에 걸쳐 hello 플랫폼의 융통성 hello를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="459ed-305">This example shows you hello flexibility of hello platform where you can build custom modules similar tooUmbraco Courier module toomanage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="459ed-306">참조</span><span class="sxs-lookup"><span data-stu-id="459ed-306">References</span></span>
[<span data-ttu-id="459ed-307">Azure 앱 서비스를 사용하여 Agile 소프트웨어 개발</span><span class="sxs-lookup"><span data-stu-id="459ed-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="459ed-308">Azure 앱 서비스에서 웹 앱에 대한 스테이징 환경 설정</span><span class="sxs-lookup"><span data-stu-id="459ed-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="459ed-309">Tooblock 웹 toonon 프로덕션 배포 슬롯을 액세스 하는 방법</span><span class="sxs-lookup"><span data-stu-id="459ed-309">How tooblock web access toonon-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
