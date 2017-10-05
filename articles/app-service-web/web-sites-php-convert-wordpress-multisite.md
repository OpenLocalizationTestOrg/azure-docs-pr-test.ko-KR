---
title: "Azure 앱 서비스에서 멀티사이트로 WordPress 변환"
description: "Azure의 갤러리를 통해 만든 기존 WordPress 웹앱을 가져와 WordPress 다중 사이트로 변환하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 4a15fb5e97d2ca57e5883c07651c372c54021c92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="convert-wordpress-to-multisite-in-azure-app-service"></a><span data-ttu-id="20c18-103">Azure 앱 서비스에서 멀티사이트로 WordPress 변환</span><span class="sxs-lookup"><span data-stu-id="20c18-103">Convert WordPress to Multisite in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="20c18-104">개요</span><span class="sxs-lookup"><span data-stu-id="20c18-104">Overview</span></span>
<span data-ttu-id="20c18-105">*[Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span><span class="sxs-lookup"><span data-stu-id="20c18-105">*By [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span></span>

<span data-ttu-id="20c18-106">이 자습서에서는 Azure의 갤러리를 통해 만든 기존 WordPress 웹앱을 가져와서 WordPress 멀티 사이트 설치로 변환하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-106">In this tutorial, you will learn how to take an existing WordPress web app created through the gallery in Azure and convert it into a WordPress Multisite install.</span></span> <span data-ttu-id="20c18-107">또한 설치 내에 있는 각 하위 사이트에 사용자 지정 도메인을 할당하는 방법도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-107">Additionally, you will learn how to assign a custom domain to each of the subsites within your install.</span></span>

<span data-ttu-id="20c18-108">여기서는 WordPress가 이미 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-108">It is assumed that you have an existing installation of WordPress.</span></span> <span data-ttu-id="20c18-109">그렇지 않은 경우 [Azure의 갤러리에서 WordPress 웹 사이트 만들기][website-from-gallery]의 지침을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="20c18-109">If you do not, please follow the guidance provided in [Create a WordPress web site from the gallery in Azure][website-from-gallery].</span></span>

<span data-ttu-id="20c18-110">기존 WordPress 단일 사이트 설치를 멀티 사이트로 변환하는 작업은 일반적으로 매우 간단하며 여기서는 초기의 많은 단계를 [WordPress Codex](http://codex.wordpress.org)(영문)의 [네트워크 만들기][wordpress-codex-create-a-network] 페이지에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-110">Converting an existing WordPress single site install to Multisite is generally fairly simple, and many of the initial steps here come straight from the [Create A Network][wordpress-codex-create-a-network] page on the [WordPress Codex](http://codex.wordpress.org).</span></span>

<span data-ttu-id="20c18-111">이제 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-111">Let's get started.</span></span>

## <a name="allow-multisite"></a><span data-ttu-id="20c18-112">멀티 사이트 허용</span><span class="sxs-lookup"><span data-stu-id="20c18-112">Allow Multisite</span></span>
<span data-ttu-id="20c18-113">먼저 `wp-config.php` 파일에서 **WP\_ALLOW\_MULTISITE** 상수를 사용하여 다중 사이트를 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-113">You first need to enable Multisite through the `wp-config.php` file with the **WP\_ALLOW\_MULTISITE** constant.</span></span> <span data-ttu-id="20c18-114">웹 앱 파일은 두 가지 방법으로 편집할 수 있습니다. 첫 번째는 FTP를 통하는 것이고 두 번째는 Git를 통하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-114">There are two methods to edit your web app files: the first is through FTP, and the second through Git.</span></span> <span data-ttu-id="20c18-115">이러한 방법을 설정하는 데 익숙지 않다면 다음 자습서를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="20c18-115">If you are unfamiliar with how to setup either of these methods, please refer to the following tutorials:</span></span>

* <span data-ttu-id="20c18-116">[MySQL 및 FTP를 사용하는 PHP 웹 사이트][website-w-mysql-and-ftp-ftp-setup]</span><span class="sxs-lookup"><span data-stu-id="20c18-116">[PHP web site with MySQL and FTP][website-w-mysql-and-ftp-ftp-setup]</span></span>
* <span data-ttu-id="20c18-117">[MySQL 및 Git를 사용하는 PHP 웹 사이트][website-w-mysql-and-git-git-setup]</span><span class="sxs-lookup"><span data-stu-id="20c18-117">[PHP web site with MySQL and Git][website-w-mysql-and-git-git-setup]</span></span>

<span data-ttu-id="20c18-118">선택한 편집기를 사용하여 `wp-config.php` 파일을 열고 `/* That's all, stop editing! Happy blogging. */` 줄 위에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-118">Open the `wp-config.php` file with the editor of your choosing and add the following above the `/* That's all, stop editing! Happy blogging. */` line.</span></span>

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

<span data-ttu-id="20c18-119">파일을 저장하고 다시 서버에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-119">Be sure to save the file and upload it back to the server!</span></span>

## <a name="network-setup"></a><span data-ttu-id="20c18-120">네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="20c18-120">Network Setup</span></span>
<span data-ttu-id="20c18-121">웹앱의 *wp-admin*에 로그인하면 **도구** 메뉴 아래에 **네트워크 설정**이라는 새 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-121">Log in to the *wp-admin* area of your web app and you should see a new item under the **Tools** menu called **Network Setup**.</span></span> <span data-ttu-id="20c18-122">**네트워크 설정**을 클릭하고 네트워크의 세부 정보를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-122">Click **Network Setup** and fill in the details of your network.</span></span>

![네트워크 설정 화면][wordpress-network-setup]

<span data-ttu-id="20c18-124">이 자습서에서는 *Sub-directories* 사이트 스키마가 항상 적절히 작동하므로 이 스키마를 사용하며 이 자습서의 뒷부분에서 각 하위 사이트에 대한 사용자 지정 도메인을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-124">This tutorial uses the *Sub-directories* site schema because it should always work, and we will be setting up custom domains for each subsite later in the tutorial.</span></span> <span data-ttu-id="20c18-125">그러나 [Azure 포털](https://portal.azure.com)을 통해 도메인을 매핑하고 와일드카드 DNS를 제대로 설정한 경우 하위 도메인 설치를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-125">However, it should be possible to setup a subdomain install if you map a domain through the [Azure Portal](https://portal.azure.com) and setup wildcard DNS properly.</span></span>

<span data-ttu-id="20c18-126">하위 도메인과 하위 디렉터리 설정에 대한 자세한 내용은 WordPress Codex의 [멀티 사이트 네트워크 유형][wordpress-codex-types-of-networks] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20c18-126">For more information on sub-domain vs sub-directory setups see the [Types of multisite network][wordpress-codex-types-of-networks] article on the WordPress Codex.</span></span>

## <a name="enable-the-network"></a><span data-ttu-id="20c18-127">네트워크 사용</span><span class="sxs-lookup"><span data-stu-id="20c18-127">Enable the Network</span></span>
<span data-ttu-id="20c18-128">이제 네트워크가 데이터베이스에 구성되어 있지만 네트워크 기능을 사용하도록 설정하는 단계가 하나 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-128">The network is now configured in the database, but there is one remaining step to enable the network functionality.</span></span> <span data-ttu-id="20c18-129">`wp-config.php` 설정을 완료하고 `web.config`에서 각 사이트를 적절히 라우팅하는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="20c18-129">Finalize the `wp-config.php` settings and ensure `web.config` properly routes each site.</span></span>

<span data-ttu-id="20c18-130">*네트워크 설정* 페이지에서 **설치** 단추를 클릭하면 WordPress에서 `wp-config.php` 및 `web.config` 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-130">After clicking the **Install** button on the *Network Setup* page, WordPress will attempt to update the `wp-config.php` and `web.config` files.</span></span> <span data-ttu-id="20c18-131">그러나 항상 파일을 검토하여 업데이트가 성공했는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-131">However, you should always check the files to ensure the updates were successful.</span></span> <span data-ttu-id="20c18-132">업데이트에 성공하지 못한 경우 이 화면은 필수 업데이트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-132">If not, this screen will present you with the necessary updates.</span></span> <span data-ttu-id="20c18-133">파일을 편집하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-133">Edit and save the files.</span></span>

<span data-ttu-id="20c18-134">업데이트한 후 wp-admin 대시보드에서 로그아웃했다가 다시 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-134">After making these updates you will need to log out and log back into the wp-admin dashboard.</span></span>

<span data-ttu-id="20c18-135">이제 관리 표시줄에 **내 사이트**라는 레이블의 추가 메뉴가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-135">There should now be an additional menu on the admin bar labeled **My Sites**.</span></span> <span data-ttu-id="20c18-136">이 메뉴를 사용하여 **네트워크 관리** 대시보드를 통해 새 네트워크를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-136">This menu allows you to control your new network through the **Network Admin** dashboard.</span></span>

## <a name="adding-custom-domains"></a><span data-ttu-id="20c18-137">사용자 지정 도메인 추가</span><span class="sxs-lookup"><span data-stu-id="20c18-137">Adding custom domains</span></span>
<span data-ttu-id="20c18-138">[WordPress MU 도메인 매핑][wordpress-plugin-wordpress-mu-domain-mapping] 플러그 인을 사용하면 네트워크에 있는 임의의 사이트에 사용자 지정 도메인을 쉽게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-138">The [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] plugin makes it a breeze to add custom domains to any site in your network.</span></span> <span data-ttu-id="20c18-139">플러그 인의 정상적인 작동을 위해서는 포털과 도메인 등록 기관에서 추가 설정을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-139">In order for the plugin to operate properly, you need to do some additional setup on the Portal, and also at your domain registrar.</span></span>

## <a name="enable-domain-mapping-to-the-web-app"></a><span data-ttu-id="20c18-140">웹 앱에 대한 도메인 매핑 사용</span><span class="sxs-lookup"><span data-stu-id="20c18-140">Enable domain mapping to the web app</span></span>
<span data-ttu-id="20c18-141">**무료** [앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 계획 모드에서는 웹앱에 사용자 지정 도메인을 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-141">The **Free** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan mode does not support adding custom domains to Web Apps.</span></span> <span data-ttu-id="20c18-142">**공유** 또는 **표준** 모드로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-142">You will need to switch to **Shared** or **Standard** mode.</span></span> <span data-ttu-id="20c18-143">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-143">To do this:</span></span>

* <span data-ttu-id="20c18-144">Azure 포털에 로그인하여 웹 앱을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-144">Log in to the Azure Portal and locate your web app.</span></span> 
* <span data-ttu-id="20c18-145">**설정**의 **규모 확장** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-145">Click on the **Scale up** tab in **Settings**.</span></span>
* <span data-ttu-id="20c18-146">**일반**에서 *공유* 또는 *표준*을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-146">Under **General**, select either *SHARED* or *STANDARD*</span></span>
* <span data-ttu-id="20c18-147">페이지 맨 아래에 있는 **저장**</span><span class="sxs-lookup"><span data-stu-id="20c18-147">Click **Save**</span></span>

<span data-ttu-id="20c18-148">변경을 확인하고 사용량 및 기타 설정된 구성에 따라 웹앱에 비용이 청구될 수 있음을 알리는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-148">You may receive a message asking you to verify the change and acknowledge your web app may now incur a cost, depending upon usage and the other configuration you set.</span></span>

<span data-ttu-id="20c18-149">새 설정을 처리하는 데 몇 초 정도 걸리며, 이제 도메인을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-149">It takes a few seconds to process the new settings, so now is a good time to start setting up your domain.</span></span>

## <a name="verify-your-domain"></a><span data-ttu-id="20c18-150">도메인 확인</span><span class="sxs-lookup"><span data-stu-id="20c18-150">Verify your domain</span></span>
<span data-ttu-id="20c18-151">Azure 웹 앱에서 사이트에 도메인을 매핑하려면 먼저 도메인에 매핑할 수 있는 권한이 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-151">Before Azure Web Apps will allow you to map a domain to the site, you first need to verify that you have the authorization to map the domain.</span></span> <span data-ttu-id="20c18-152">이를 위해서는 DNS 항목에 새 CNAME 레코드를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-152">To do so, you must add a new CNAME record to your DNS entry.</span></span>

* <span data-ttu-id="20c18-153">도메인의 DNS 관리자에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-153">Log in to your domain's DNS manager</span></span>
* <span data-ttu-id="20c18-154">새로운 CNAME *awverify*</span><span class="sxs-lookup"><span data-stu-id="20c18-154">Create a new CNAME *awverify*</span></span>
* <span data-ttu-id="20c18-155">*awverify*로 *awverify.YOUR_DOMAIN.azurewebsites.net*을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-155">Point *awverify* to *awverify.YOUR_DOMAIN.azurewebsites.net*</span></span>

<span data-ttu-id="20c18-156">DNS 변경 내용이 완전히 적용되는 데 어느 정도 시간이 걸릴 수 있으므로, 다음 단계가 즉시 진행되지 않으면 잠시 쉬었다가 나중에 다시 시도해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="20c18-156">It may take some time for the DNS changes to go into full effect, so if the following steps do not work immediately, go make a cup of coffee, then come back and try again.</span></span>

## <a name="add-the-domain-to-the-web-app"></a><span data-ttu-id="20c18-157">웹 앱에 도메인 추가</span><span class="sxs-lookup"><span data-stu-id="20c18-157">Add the domain to the web app</span></span>
<span data-ttu-id="20c18-158">Azure 포털을 통해 웹앱에 반환하고 **설정**, **사용자 지정 도메인 및 SSL**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-158">Return to your web app through the Azure Portal, click **Settings**, and then click **Custom domains and SSL**.</span></span>

<span data-ttu-id="20c18-159">*SSL 설정* 이 표시되면 웹앱에 할당하려는 모든 도메인을 입력할 필드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-159">When the *SSL settings* are displayed, you will see the fields where you will input all the domains which you wish to assign to your web app.</span></span> <span data-ttu-id="20c18-160">여기에 나열되지 않는 도메인은 도메인 DNS 설정 방법과 상관없이 WordPress에서 매핑에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-160">If a domain is not listed here, it will not be available for mapping inside WordPress, regardless of how the domain DNS is setup.</span></span>

![사용자 지정 도메인 관리 대화 상자][wordpress-manage-domains]

<span data-ttu-id="20c18-162">텍스트 상자에 도메인을 입력한 후 Azure에서 앞서 만든 CNAME 레코드를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-162">After typing your domain into the text box, Azure will verify the CNAME record you created previously.</span></span> <span data-ttu-id="20c18-163">DNS가 완전히 전파되지 않으면 빨간색 표시기가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-163">If the DNS has not fully propagated, a red indicator will show.</span></span> <span data-ttu-id="20c18-164">성공한 경우에는 녹색 확인 표시가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-164">If it was successful, you will see a green checkmark.</span></span> 

<span data-ttu-id="20c18-165">대화 상자 아래쪽에 나열되는 IP 주소를 기록하십시오.</span><span class="sxs-lookup"><span data-stu-id="20c18-165">Take note of the IP Address listed at the bottom of the dialog.</span></span> <span data-ttu-id="20c18-166">도메인에 대한 A 레코드를 설정하는 데 이 주소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-166">You will need this to setup the A record for your domain.</span></span>

## <a name="setup-the-domain-a-record"></a><span data-ttu-id="20c18-167">도메인 A 레코드 설정</span><span class="sxs-lookup"><span data-stu-id="20c18-167">Setup the domain A record</span></span>
<span data-ttu-id="20c18-168">다른 단계가 완료되었다면 이제 DNS A 레코드를 통해 Azure 웹 앱에 도메인을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-168">If the other steps were successful, you may now assign the domain to your Azure web app through a DNS A record.</span></span> 

<span data-ttu-id="20c18-169">Azure 웹앱에서 CNAME과 A 레코드를 모두 허용하지만 적절한 도메인 매핑을 사용하려면 *반드시* A 레코드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-169">It is important to note here that Azure web apps accept both CNAME and A records, however you *must* use an A record to enable proper domain mapping.</span></span> <span data-ttu-id="20c18-170">CNAME은 YOUR_DOMAIN.azurewebsites.net을 사용하여 자동으로 만들어지는 다른 CNAME으로 전달할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-170">A CNAME cannot be forwarded to another CNAME, which is what Azure created for you with YOUR_DOMAIN.azurewebsites.net.</span></span>

<span data-ttu-id="20c18-171">이전 단계의 IP 주소를 사용하여 DNS 관리자로 돌아와서 해당 IP를 가리키도록 A 레코드를 설정하십시오.</span><span class="sxs-lookup"><span data-stu-id="20c18-171">Using the IP address from the previous step, return to your DNS manager and setup the A record to point to that IP.</span></span>

## <a name="install-and-setup-the-plugin"></a><span data-ttu-id="20c18-172">플러그 인 설치 및 설정</span><span class="sxs-lookup"><span data-stu-id="20c18-172">Install and setup the plugin</span></span>
<span data-ttu-id="20c18-173">WordPress 멀티 사이트에는 사용자 지정 도메인에 매핑하는 기본 제공 방법이 현재 없습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-173">WordPress Multisite currently does not have a built-in method to map custom domains.</span></span> <span data-ttu-id="20c18-174">그러나 매핑 기능을 추가해 주는 [WordPress MU 도메인 매핑][wordpress-plugin-wordpress-mu-domain-mapping](영문)이라는 플러그 인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-174">However, there is a plugin called [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] that adds the functionality for you.</span></span> <span data-ttu-id="20c18-175">사이트의 네트워크 관리 부분에 로그인하여 **WordPress MU 도메인 매핑** 플러그 인을 설치하십시오.</span><span class="sxs-lookup"><span data-stu-id="20c18-175">Log in to the Network Admin portion of your site and install the **WordPress MU Domain Mapping** plugin.</span></span>

<span data-ttu-id="20c18-176">플러그 인을 설치하고 활성화한 후 **규모 확장** > **도메인 매핑** 으로 이동하여 플러그 인을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-176">After installing and activating the plugin, visit **Settings** > **Domain Mapping** to configure the plugin.</span></span> <span data-ttu-id="20c18-177">첫 번째 텍스트 상자인 *서버 IP 주소*에서, 도메인의 A 레코드를 설정하는 데 사용한 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-177">In the first textbox, *Server IP Address*, input the IP Address you used to setup the A record for the domain.</span></span> <span data-ttu-id="20c18-178">원하는 임의의 *도메인 옵션*을 설정하고(대개 기본값을 그대로 사용하는 것이 좋음) **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-178">Set any *Domain Options* you desire (the defaults are often fine) and click **Save**.</span></span>

## <a name="map-the-domain"></a><span data-ttu-id="20c18-179">도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="20c18-179">Map the domain</span></span>
<span data-ttu-id="20c18-180">도메인을 매핑할 사이트의 **대시보드** 로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-180">Visit the **Dashboard** for the site you wish to map the domain to.</span></span> <span data-ttu-id="20c18-181">**도구** > **도메인 매핑**을 클릭하고 텍스트 상자에 새 도메인을 입력한 후 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-181">Click on **Tools** > **Domain Mapping** and type the new domain into the textbox and click **Add**.</span></span>

<span data-ttu-id="20c18-182">기본적으로 새 도메인은 자동 생성된 사이트 도메인에 다시 쓰입니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-182">By default, the new domain will be rewritten to the autogenerated site domain.</span></span> <span data-ttu-id="20c18-183">모든 트래픽을 새 도메인으로 보내려면 저장하기 전에 *Primary domain for this blog* 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-183">If you want to have all traffic sent to the new domain, check the *Primary domain for this blog* box before saving.</span></span> <span data-ttu-id="20c18-184">사이트에 도메인을 무제한으로 추가할 수 있지만 한 도메인만 주 도메인이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-184">You can add an unlimited number of domains to a site, but  only one can be primary.</span></span>

## <a name="do-it-again"></a><span data-ttu-id="20c18-185">다시 실행</span><span class="sxs-lookup"><span data-stu-id="20c18-185">Do it again</span></span>
<span data-ttu-id="20c18-186">Azure 웹 앱에서는 웹 앱에 도메인을 무제한으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-186">Azure Web Apps allow you to add an unlimited number of domains to a web app.</span></span> <span data-ttu-id="20c18-187">다른 도메인을 추가하려면 각 도메인에 대해 **도메인 확인** 및 **도메인 A 레코드 설정** 섹션을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-187">To add another domain you will need to execute the **Verify your domain** and **Setup the domain A record** sections for each domain.</span></span>    

> [!NOTE]
> <span data-ttu-id="20c18-188">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-188">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="20c18-189">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="20c18-189">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="20c18-190">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="20c18-190">What's changed</span></span>
* <span data-ttu-id="20c18-191">웹 사이트에서 앱 서비스로의 변경에 대한 지침은 [Azure App Service와 이 서비스가 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="20c18-191">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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


