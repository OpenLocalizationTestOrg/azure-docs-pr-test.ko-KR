---
title: "Azure 앱 서비스의 aaaConvert WordPress tooMultisite"
description: "Tootake 기존 WordPress 웹 앱이 Azure의 hello 갤러리를 통해 만들어진 하 고 tooWordPress 멀티 사이트를 변환 하는 방법을 알아봅니다"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 1153f0a8043de875f081704cd0a124776758878c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-wordpress-toomultisite-in-azure-app-service"></a><span data-ttu-id="f61c0-103">Azure 앱 서비스에서 WordPress tooMultisite 변환</span><span class="sxs-lookup"><span data-stu-id="f61c0-103">Convert WordPress tooMultisite in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="f61c0-104">개요</span><span class="sxs-lookup"><span data-stu-id="f61c0-104">Overview</span></span>
<span data-ttu-id="f61c0-105">*[Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span><span class="sxs-lookup"><span data-stu-id="f61c0-105">*By [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span></span>

<span data-ttu-id="f61c0-106">이 자습서에서는 tootake WordPress는 기존 웹 응용 프로그램 만드는 방법은 Azure 및 WordPress 멀티 사이트에 설치 하는 변환에서 hello 갤러리를 통해 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-106">In this tutorial, you will learn how tootake an existing WordPress web app created through hello gallery in Azure and convert it into a WordPress Multisite install.</span></span> <span data-ttu-id="f61c0-107">또한 어떻게 tooassign hello의 사용자 지정 도메인 tooeach 하위 사이트 귀하의 설치에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-107">Additionally, you will learn how tooassign a custom domain tooeach of hello subsites within your install.</span></span>

<span data-ttu-id="f61c0-108">여기서는 WordPress가 이미 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-108">It is assumed that you have an existing installation of WordPress.</span></span> <span data-ttu-id="f61c0-109">이렇게 하지 않으면 하는 경우에 제공 된 hello 지침은 따르십시오 [Azure의 hello 갤러리에서 WordPress 웹 사이트를 만들][website-from-gallery]합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-109">If you do not, please follow hello guidance provided in [Create a WordPress web site from hello gallery in Azure][website-from-gallery].</span></span>

<span data-ttu-id="f61c0-110">기존 WordPress 변환 단일 사이트 설치 tooMultisite 일반적으로 매우 간단 하 고 hello에서 바로 hello 초기 단계 중 상당수 [A 네트워크 만들기] [ wordpress-codex-create-a-network] hello 페이지[WordPress Codex](http://codex.wordpress.org)합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-110">Converting an existing WordPress single site install tooMultisite is generally fairly simple, and many of hello initial steps here come straight from hello [Create A Network][wordpress-codex-create-a-network] page on hello [WordPress Codex](http://codex.wordpress.org).</span></span>

<span data-ttu-id="f61c0-111">이제 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-111">Let's get started.</span></span>

## <a name="allow-multisite"></a><span data-ttu-id="f61c0-112">멀티 사이트 허용</span><span class="sxs-lookup"><span data-stu-id="f61c0-112">Allow Multisite</span></span>
<span data-ttu-id="f61c0-113">먼저 hello 통해 멀티 사이트 tooenable `wp-config.php` hello로 파일 **WP\_허용\_멀티 사이트** 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-113">You first need tooenable Multisite through hello `wp-config.php` file with hello **WP\_ALLOW\_MULTISITE** constant.</span></span> <span data-ttu-id="f61c0-114">없는 두 가지 방법 tooedit 웹 응용 프로그램 파일: hello FTP 및 Git 통해 hello를 통해 먼저가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-114">There are two methods tooedit your web app files: hello first is through FTP, and hello second through Git.</span></span> <span data-ttu-id="f61c0-115">방법을 잘 모를 경우 toosetup toohello 자습서 다음을 참조 하십시오 이러한 방법 중 하나:</span><span class="sxs-lookup"><span data-stu-id="f61c0-115">If you are unfamiliar with how toosetup either of these methods, please refer toohello following tutorials:</span></span>

* <span data-ttu-id="f61c0-116">[MySQL 및 FTP를 사용하는 PHP 웹 사이트][website-w-mysql-and-ftp-ftp-setup]</span><span class="sxs-lookup"><span data-stu-id="f61c0-116">[PHP web site with MySQL and FTP][website-w-mysql-and-ftp-ftp-setup]</span></span>
* <span data-ttu-id="f61c0-117">[MySQL 및 Git를 사용하는 PHP 웹 사이트][website-w-mysql-and-git-git-setup]</span><span class="sxs-lookup"><span data-stu-id="f61c0-117">[PHP web site with MySQL and Git][website-w-mysql-and-git-git-setup]</span></span>

<span data-ttu-id="f61c0-118">열기 hello `wp-config.php` 선택한 hello 편집기로 파일을 hello 위에 hello 다음과 같은 추가 `/* That's all, stop editing! Happy blogging. */` 선입니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-118">Open hello `wp-config.php` file with hello editor of your choosing and add hello following above hello `/* That's all, stop editing! Happy blogging. */` line.</span></span>

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

<span data-ttu-id="f61c0-119">있는지 toosave hello 파일 이어야 하 고 뒤로 toohello 서버 업로드!</span><span class="sxs-lookup"><span data-stu-id="f61c0-119">Be sure toosave hello file and upload it back toohello server!</span></span>

## <a name="network-setup"></a><span data-ttu-id="f61c0-120">네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="f61c0-120">Network Setup</span></span>
<span data-ttu-id="f61c0-121">Toohello 로그인 *wp 관리자* 웹 응용 프로그램의 영역 hello 아래에 새 항목을 참조 해야 **도구** 이라는 메뉴가 **네트워크 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-121">Log in toohello *wp-admin* area of your web app and you should see a new item under hello **Tools** menu called **Network Setup**.</span></span> <span data-ttu-id="f61c0-122">클릭 **네트워크 설정** 고 네트워크의 hello 세부 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-122">Click **Network Setup** and fill in hello details of your network.</span></span>

![네트워크 설정 화면][wordpress-network-setup]

<span data-ttu-id="f61c0-124">이 자습서에서는 hello *하위 디렉터리* 항상 작동 해야 하 고 hello 자습서의 뒷부분에 나오는 각 하위 사이트에 대 한 사용자 지정 도메인을 설정 합니다 것 때문에 스키마를 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-124">This tutorial uses hello *Sub-directories* site schema because it should always work, and we will be setting up custom domains for each subsite later in hello tutorial.</span></span> <span data-ttu-id="f61c0-125">그러나 hello 통해 도메인을 매핑하는 경우 하위 도메인을 설치 하는 가능한 toosetup 있어야 [Azure 포털](https://portal.azure.com) 및 와일드 카드 DNS를 올바르게 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-125">However, it should be possible toosetup a subdomain install if you map a domain through hello [Azure Portal](https://portal.azure.com) and setup wildcard DNS properly.</span></span>

<span data-ttu-id="f61c0-126">하위 도메인 vs 대 한 자세한 내용은 하위 디렉터리 설정을 참조 hello [멀티 사이트 네트워크 유형의] [ wordpress-codex-types-of-networks] hello WordPress Codex 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-126">For more information on sub-domain vs sub-directory setups see hello [Types of multisite network][wordpress-codex-types-of-networks] article on hello WordPress Codex.</span></span>

## <a name="enable-hello-network"></a><span data-ttu-id="f61c0-127">Hello 네트워크를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f61c0-127">Enable hello Network</span></span>
<span data-ttu-id="f61c0-128">hello 네트워크 hello 데이터베이스에서 이제 구성 하지만 한 나머지 단계 tooenable hello 네트워크 기능.</span><span class="sxs-lookup"><span data-stu-id="f61c0-128">hello network is now configured in hello database, but there is one remaining step tooenable hello network functionality.</span></span> <span data-ttu-id="f61c0-129">Hello 마무리 `wp-config.php` 설정을 확인 하 고 `web.config` 제대로 각 사이트를 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-129">Finalize hello `wp-config.php` settings and ensure `web.config` properly routes each site.</span></span>

<span data-ttu-id="f61c0-130">Hello를 클릭 한 후 **설치** hello 단추 *네트워크 설정* 페이지에서 WordPress는 tooupdate hello 시도 `wp-config.php` 및 `web.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-130">After clicking hello **Install** button on hello *Network Setup* page, WordPress will attempt tooupdate hello `wp-config.php` and `web.config` files.</span></span> <span data-ttu-id="f61c0-131">그러나 항상 확인 해야 hello 파일 tooensure hello 업데이트 성공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-131">However, you should always check hello files tooensure hello updates were successful.</span></span> <span data-ttu-id="f61c0-132">그렇지 않은 경우이 화면 hello 필요한 업데이트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-132">If not, this screen will present you with hello necessary updates.</span></span> <span data-ttu-id="f61c0-133">편집 하 고 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-133">Edit and save hello files.</span></span>

<span data-ttu-id="f61c0-134">작업을 수행 하면 아웃 toolog 및 로그 필요 합니다. 이러한 업데이트 hello wp 관리 대시보드 스풀링됩니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-134">After making these updates you will need toolog out and log back into hello wp-admin dashboard.</span></span>

<span data-ttu-id="f61c0-135">있어야는 추가 메뉴 레이블이 지정 된 hello admin 모음의 **내 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-135">There should now be an additional menu on hello admin bar labeled **My Sites**.</span></span> <span data-ttu-id="f61c0-136">이 메뉴 있습니다 toocontrol hello 통해 새로운 네트워크 **네트워크 관리자** 대시보드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-136">This menu allows you toocontrol your new network through hello **Network Admin** dashboard.</span></span>

## <a name="adding-custom-domains"></a><span data-ttu-id="f61c0-137">사용자 지정 도메인 추가</span><span class="sxs-lookup"><span data-stu-id="f61c0-137">Adding custom domains</span></span>
<span data-ttu-id="f61c0-138">hello [WordPress MU 도메인 매핑] [ wordpress-plugin-wordpress-mu-domain-mapping] 플러그 인을 사용 하면 쉽게 tooadd 사용자 지정 도메인 tooany 사이트 네트워크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-138">hello [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] plugin makes it a breeze tooadd custom domains tooany site in your network.</span></span> <span data-ttu-id="f61c0-139">플러그 인 toooperate hello에 대 한 적절 하 게 해야 toodo hello 포털 뿐만 아니라 도메인 등록자에서 몇 가지 추가 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-139">In order for hello plugin toooperate properly, you need toodo some additional setup on hello Portal, and also at your domain registrar.</span></span>

## <a name="enable-domain-mapping-toohello-web-app"></a><span data-ttu-id="f61c0-140">도메인 매핑 toohello 웹 응용 프로그램을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="f61c0-140">Enable domain mapping toohello web app</span></span>
<span data-ttu-id="f61c0-141">hello **무료** [앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 계획 모드에서는 사용자 지정 도메인 tooWeb 앱을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-141">hello **Free** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan mode does not support adding custom domains tooWeb Apps.</span></span> <span data-ttu-id="f61c0-142">해야 tooswitch 너무**Shared** 또는 **표준** 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-142">You will need tooswitch too**Shared** or **Standard** mode.</span></span> <span data-ttu-id="f61c0-143">toodo이:</span><span class="sxs-lookup"><span data-stu-id="f61c0-143">toodo this:</span></span>

* <span data-ttu-id="f61c0-144">Azure 포털 toohello를 로그인 하 고 웹 응용 프로그램을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-144">Log in toohello Azure Portal and locate your web app.</span></span> 
* <span data-ttu-id="f61c0-145">Hello 클릭 **수직** 탭에서 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-145">Click on hello **Scale up** tab in **Settings**.</span></span>
* <span data-ttu-id="f61c0-146">**일반**에서 *공유* 또는 *표준*을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-146">Under **General**, select either *SHARED* or *STANDARD*</span></span>
* <span data-ttu-id="f61c0-147">페이지 맨 아래에 있는 **저장**</span><span class="sxs-lookup"><span data-stu-id="f61c0-147">Click **Save**</span></span>

<span data-ttu-id="f61c0-148">Tooverify hello 변경 하 라는 메시지가 나타날 수 고 웹 앱 수 이제 사용량에 따라 비용 하 고도 설정한 다른 구성이 hello를 승인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-148">You may receive a message asking you tooverify hello change and acknowledge your web app may now incur a cost, depending upon usage and hello other configuration you set.</span></span>

<span data-ttu-id="f61c0-149">몇 초 정도 tooprocess hello 새 설정을 걸리는 이제는 사용자 도메인을 좋은 시간 toostart 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-149">It takes a few seconds tooprocess hello new settings, so now is a good time toostart setting up your domain.</span></span>

## <a name="verify-your-domain"></a><span data-ttu-id="f61c0-150">도메인 확인</span><span class="sxs-lookup"><span data-stu-id="f61c0-150">Verify your domain</span></span>
<span data-ttu-id="f61c0-151">Azure 웹 앱을 허용 하는 사용자 도메인 toohello 사이트 toomap 전에 먼저 hello 권한 부여 toomap hello 도메인 있는지 tooverify를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-151">Before Azure Web Apps will allow you toomap a domain toohello site, you first need tooverify that you have hello authorization toomap hello domain.</span></span> <span data-ttu-id="f61c0-152">toodo 따라서 새 CNAME 레코드 tooyour DNS 항목을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-152">toodo so, you must add a new CNAME record tooyour DNS entry.</span></span>

* <span data-ttu-id="f61c0-153">Tooyour 도메인의 DNS 관리자 로그인</span><span class="sxs-lookup"><span data-stu-id="f61c0-153">Log in tooyour domain's DNS manager</span></span>
* <span data-ttu-id="f61c0-154">새로운 CNAME *awverify*</span><span class="sxs-lookup"><span data-stu-id="f61c0-154">Create a new CNAME *awverify*</span></span>
* <span data-ttu-id="f61c0-155">지점 *awverify* 너무*awverify. YOUR_DOMAIN.azurewebsites.net*</span><span class="sxs-lookup"><span data-stu-id="f61c0-155">Point *awverify* too*awverify.YOUR_DOMAIN.azurewebsites.net*</span></span>

<span data-ttu-id="f61c0-156">단계를 수행 하는 hello 즉시 작동 하지 않을 경우 커피를 확인 한 다음 다시 시도 하 고 다시 시도 하십시오 이동 하는 하므로 하세요 전체 발효 DNS 변경 내용 toogo hello에 대 한 다소 시간이 걸릴 수 있습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-156">It may take some time for hello DNS changes toogo into full effect, so if hello following steps do not work immediately, go make a cup of coffee, then come back and try again.</span></span>

## <a name="add-hello-domain-toohello-web-app"></a><span data-ttu-id="f61c0-157">Hello 도메인 toohello 웹 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="f61c0-157">Add hello domain toohello web app</span></span>
<span data-ttu-id="f61c0-158">Hello Azure 포털을 통해 반환 tooyour 웹 응용 프로그램 클릭 **설정**, 클릭 하 고 **사용자 지정 도메인 및 SSL**합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-158">Return tooyour web app through hello Azure Portal, click **Settings**, and then click **Custom domains and SSL**.</span></span>

<span data-ttu-id="f61c0-159">Hello 때 *SSL 설정* 는 표시 나타납니다 hello 필드 tooassign tooyour 웹 응용 프로그램을 복원할 모든 hello 도메인을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-159">When hello *SSL settings* are displayed, you will see hello fields where you will input all hello domains which you wish tooassign tooyour web app.</span></span> <span data-ttu-id="f61c0-160">도메인은 여기에 나열 되지 hello 도메인 DNS가 설치 하는 방법에 관계 없이 WordPress, 내부 매핑에 사용할 수 있는 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-160">If a domain is not listed here, it will not be available for mapping inside WordPress, regardless of how hello domain DNS is setup.</span></span>

![사용자 지정 도메인 관리 대화 상자][wordpress-manage-domains]

<span data-ttu-id="f61c0-162">Hello 텍스트 상자에 도메인을 입력 한 후 Azure hello 이전에 만든 CNAME 레코드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-162">After typing your domain into hello text box, Azure will verify hello CNAME record you created previously.</span></span> <span data-ttu-id="f61c0-163">Hello DNS에 완전히 전파 되지, 빨간색 표시기가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-163">If hello DNS has not fully propagated, a red indicator will show.</span></span> <span data-ttu-id="f61c0-164">성공한 경우에는 녹색 확인 표시가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-164">If it was successful, you will see a green checkmark.</span></span> 

<span data-ttu-id="f61c0-165">Hello hello hello 대화 상자 맨 아래에 나열 된 IP 주소를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-165">Take note of hello IP Address listed at hello bottom of hello dialog.</span></span> <span data-ttu-id="f61c0-166">도메인에 대 한이 toosetup hello 레코드가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-166">You will need this toosetup hello A record for your domain.</span></span>

## <a name="setup-hello-domain-a-record"></a><span data-ttu-id="f61c0-167">Hello 도메인 A 레코드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-167">Setup hello domain A record</span></span>
<span data-ttu-id="f61c0-168">Hello 다른 단계가 성공 했는지, 하는 경우 이제 hello DNS A 레코드를 통해 도메인 tooyour Azure 웹 앱을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-168">If hello other steps were successful, you may now assign hello domain tooyour Azure web app through a DNS A record.</span></span> 

<span data-ttu-id="f61c0-169">그러나 것이 중요 한 toonote 여기는 Azure 웹 앱에 동의 CNAME 및 A 레코드를 모두 있습니다 *해야* A 레코드 tooenable 적절 한 도메인 매핑을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-169">It is important toonote here that Azure web apps accept both CNAME and A records, however you *must* use an A record tooenable proper domain mapping.</span></span> <span data-ttu-id="f61c0-170">CNAME 전달할 수 없습니다 tooanother CNAME을 드립니다 YOUR_DOMAIN.azurewebsites.net를 사용 하 여 Azure에서 만든 작업은입니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-170">A CNAME cannot be forwarded tooanother CNAME, which is what Azure created for you with YOUR_DOMAIN.azurewebsites.net.</span></span>

<span data-ttu-id="f61c0-171">Hello 이전 단계에서 hello IP 주소를 사용 하 여 tooyour DNS 관리자와 설치 hello 레코드 toopoint toothat IP 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-171">Using hello IP address from hello previous step, return tooyour DNS manager and setup hello A record toopoint toothat IP.</span></span>

## <a name="install-and-setup-hello-plugin"></a><span data-ttu-id="f61c0-172">Hello 플러그 인을 설치 및 설정</span><span class="sxs-lookup"><span data-stu-id="f61c0-172">Install and setup hello plugin</span></span>
<span data-ttu-id="f61c0-173">WordPress 멀티 사이트가 현재 없는 기본 제공 메서드 toomap 사용자 지정 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-173">WordPress Multisite currently does not have a built-in method toomap custom domains.</span></span> <span data-ttu-id="f61c0-174">그러나 호출 플러그 인은 [WordPress MU 도메인 매핑] [ wordpress-plugin-wordpress-mu-domain-mapping] 드립니다 hello 기능을 추가 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-174">However, there is a plugin called [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] that adds hello functionality for you.</span></span> <span data-ttu-id="f61c0-175">사이트의 네트워크 관리 부분 toohello에에서 로그인 하 고 hello 설치 **WordPress MU 도메인 매핑** 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-175">Log in toohello Network Admin portion of your site and install hello **WordPress MU Domain Mapping** plugin.</span></span>

<span data-ttu-id="f61c0-176">설치 및 활성화 hello 플러그 인을 방문 후 **설정** > **도메인 매핑** tooconfigure hello 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-176">After installing and activating hello plugin, visit **Settings** > **Domain Mapping** tooconfigure hello plugin.</span></span> <span data-ttu-id="f61c0-177">Hello 첫 번째 텍스트 상자에 *서버 IP 주소*, 입력된 hello toosetup 사용 된 IP 주소 hello hello 도메인에 대 한 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-177">In hello first textbox, *Server IP Address*, input hello IP Address you used toosetup hello A record for hello domain.</span></span> <span data-ttu-id="f61c0-178">필요한 설정을 *도메인 옵션* 원하는 (hello 기본값 만족 하는 종종)를 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-178">Set any *Domain Options* you desire (hello defaults are often fine) and click **Save**.</span></span>

## <a name="map-hello-domain"></a><span data-ttu-id="f61c0-179">Hello 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="f61c0-179">Map hello domain</span></span>
<span data-ttu-id="f61c0-180">Hello 방문 **대시보드** toomap hello 도메인을 원하는 hello 사이트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-180">Visit hello **Dashboard** for hello site you wish toomap hello domain to.</span></span> <span data-ttu-id="f61c0-181">클릭 **도구** > **도메인 매핑** 및 형식 hello 새 도메인을 클릭 하 고 hello 텍스트 상자에 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-181">Click on **Tools** > **Domain Mapping** and type hello new domain into hello textbox and click **Add**.</span></span>

<span data-ttu-id="f61c0-182">기본적으로 hello 새 도메인에 자동으로 생성 된 사이트 도메인 toohello 다시 작성된 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-182">By default, hello new domain will be rewritten toohello autogenerated site domain.</span></span> <span data-ttu-id="f61c0-183">모든 트래픽을 전송 toohello 새 도메인 toohave을 원하는 경우 확인 hello *이 블로그에 대 한 주 도메인* 저장 하기 전에 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-183">If you want toohave all traffic sent toohello new domain, check hello *Primary domain for this blog* box before saving.</span></span> <span data-ttu-id="f61c0-184">도메인 tooa 사이트의 무제한 추가할 수 있지만 하나만 주 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-184">You can add an unlimited number of domains tooa site, but  only one can be primary.</span></span>

## <a name="do-it-again"></a><span data-ttu-id="f61c0-185">다시 실행</span><span class="sxs-lookup"><span data-stu-id="f61c0-185">Do it again</span></span>
<span data-ttu-id="f61c0-186">Azure 웹 앱을 사용 하면 tooadd tooa 웹 응용 프로그램 도메인 개수는 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-186">Azure Web Apps allow you tooadd an unlimited number of domains tooa web app.</span></span> <span data-ttu-id="f61c0-187">tooadd tooexecute hello 해야 하는 다른 도메인 **도메인 확인** 및 **hello 도메인 A 레코드를 설정** 각 도메인에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="f61c0-187">tooadd another domain you will need tooexecute hello **Verify your domain** and **Setup hello domain A record** sections for each domain.</span></span>    

> [!NOTE]
> <span data-ttu-id="f61c0-188">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-188">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f61c0-189">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f61c0-189">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="f61c0-190">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="f61c0-190">What's changed</span></span>
* <span data-ttu-id="f61c0-191">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f61c0-191">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


