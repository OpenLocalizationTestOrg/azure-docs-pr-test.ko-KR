---
title: "웹 앱 aaaOpen 소스 기술을 Azure에 대 한 Faq | Microsoft Docs"
description: "Azure 앱 서비스의 웹 응용 프로그램 기능 hello의에서 오픈 소스 기술에 대 한 질문과 대답 toofrequently를 가져옵니다."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="d3c07-103">Azure Web Apps에 대한 오픈 소스 기술 FAQ</span><span class="sxs-lookup"><span data-stu-id="d3c07-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="d3c07-104">이 문서는 오픈 소스 기술을 hello에 대 한 문제에 대 한 질문과 대답 (Faq) 답변 toofrequently 되어 [Azure 앱 서비스의 웹 응용 프로그램 기능](https://azure.microsoft.com/services/app-service/web/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-104">This article has answers toofrequently asked questions (FAQs) about issues with open-source technologies for hello [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a><span data-ttu-id="d3c07-105">내 ClearDB 데이터베이스가 다운되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-105">My ClearDB database is down.</span></span> <span data-ttu-id="d3c07-106">이 문제를 해결하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="d3c07-106">How do I resolve this?</span></span>

<span data-ttu-id="d3c07-107">데이터베이스 관련 문제에 대해서는 [ClearDB 지원](https://www.cleardb.com/developers/help/support)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="d3c07-107">For database-related issues, contact [ClearDB support](https://www.cleardb.com/developers/help/support).</span></span> 

<span data-ttu-id="d3c07-108">ClearDB에 대 한 대답 toocommon 질문에 대 한 참조 [ClearDB Faq](https://docs.microsoft.com/azure/store-cleardb-faq/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-108">For answers toocommon questions about ClearDB, see [ClearDB FAQs](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a><span data-ttu-id="d3c07-109">ClearDB 데이터베이스 hello 포털에 나열 되지 않은 이유는?</span><span class="sxs-lookup"><span data-stu-id="d3c07-109">Why isn't my ClearDB database listed in hello portal?</span></span>

<span data-ttu-id="d3c07-110">Hello에 ClearDB 데이터베이스를 만들 경우 [Azure 포털](http://portal.azure.com/), hello 데이터베이스 hello에 표시 되지 않으면 [Azure 클래식 포털](http://manage.windowsazure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-110">If you create a ClearDB database in hello [Azure portal](http://portal.azure.com/), hello database doesn't appear in hello [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="d3c07-111">이 문제를 해결할 toowork, 데이터베이스 toohello 웹 앱을 수동으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-111">toowork around this, you can manually link your database toohello web app.</span></span>

<span data-ttu-id="d3c07-112">마찬가지로, hello에 ClearDB 데이터베이스를 만들 경우 [Azure 클래식 포털](http://manage.windowsazure.com/), 데이터베이스 hello에 표시 되지 않습니다 [Azure 포털](http://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-112">Similarly, if you create a ClearDB database in hello [Azure classic portal](http://manage.windowsazure.com/),  you won't see your database in hello [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="d3c07-113">이 경우 해결 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-113">In this case, no workaround is available.</span></span> 

<span data-ttu-id="d3c07-114">자세한 내용은 [Azure App Service를 사용하는 ClearDB MySQLl 데이터베이스에 대한 FAQ](https://docs.microsoft.com/azure/store-cleardb-faq/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3c07-114">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a><span data-ttu-id="d3c07-115">구독 마이그레이션 중에 내 ClearDB 데이터베이스가 마이그레이션되지 않은 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="d3c07-115">Why wasn't my ClearDB database migrated during my subscription migration?</span></span>

<span data-ttu-id="d3c07-116">구독 간에 리소스 마이그레이션을 수행할 때 일부 제한 사항 이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-116">When you perform resource migration across subscriptions, some limitations apply.</span></span> <span data-ttu-id="d3c07-117">ClearDB MySQL 데이터베이스는 타사 서비스이므로 Azure 구독 마이그레이션 중에 마이그레이션되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-117">A ClearDB MySQL database is a third-party service and is not migrated during an Azure subscription migration.</span></span>

<span data-ttu-id="d3c07-118">Azure 리소스를 마이그레이션하기 전에 hello 마이그레이션의 MySQL 데이터베이스를 관리 하지 ClearDB MySQL 데이터베이스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-118">If you don't manage hello migration of your MySQL database before you migrate your Azure resources, your ClearDB MySQL database might be unavailable.</span></span> <span data-ttu-id="d3c07-119">tooavoid이이 먼저 수동으로 ClearDB 데이터베이스를 마이그레이션하고 다음 hello 웹 앱에 대 한 Azure 구독을 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-119">tooavoid this, first, manually migrate your ClearDB database, and then migrate hello Azure subscription for your web app.</span></span>

<span data-ttu-id="d3c07-120">자세한 내용은 [Azure App Service를 사용하는 ClearDB MySQLl 데이터베이스에 대한 FAQ](https://docs.microsoft.com/azure/store-cleardb-faq/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3c07-120">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a><span data-ttu-id="d3c07-121">PHP tootroubleshoot PHP 문제를 로깅에 하려면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="d3c07-121">How do I turn on PHP logging tootroubleshoot PHP issues?</span></span>

<span data-ttu-id="d3c07-122">PHP 로깅을 tooturn:</span><span class="sxs-lookup"><span data-stu-id="d3c07-122">tooturn on PHP logging:</span></span>

1. <span data-ttu-id="d3c07-123">Tooyour 로그인 [Kudu 웹 사이트](https://*yourwebsitename*.scm.azurewebsites.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-123">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="d3c07-124">Hello 상단 메뉴에서 선택 **디버그 콘솔** > **CMD**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-124">In hello top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="d3c07-125">선택 hello **사이트** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-125">Select hello **Site** folder.</span></span>
4. <span data-ttu-id="d3c07-126">선택 hello **wwwroot** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-126">Select hello **wwwroot** folder.</span></span>
5. <span data-ttu-id="d3c07-127">선택 hello  **+**  아이콘을 선택한 후 **새 파일**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-127">Select hello **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="d3c07-128">Hello 파일 이름을 너무 설정**. user.ini**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-128">Set hello file name too**.user.ini**.</span></span>
7. <span data-ttu-id="d3c07-129">다음 너무 hello 연필 아이콘을 선택한**. user.ini**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-129">Select hello pencil icon next too**.user.ini**.</span></span>
8. <span data-ttu-id="d3c07-130">Hello 파일에서이 코드를 추가 합니다.`log_errors=on`</span><span class="sxs-lookup"><span data-stu-id="d3c07-130">In hello file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="d3c07-131">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-131">Select **Save**.</span></span>
10. <span data-ttu-id="d3c07-132">다음 너무 hello 연필 아이콘을 선택한**wp config.php**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-132">Select hello pencil icon next too**wp-config.php**.</span></span>
11. <span data-ttu-id="d3c07-133">Hello 텍스트 toohello 코드 다음 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-133">Change hello text toohello following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="d3c07-134">Hello hello 웹 응용 프로그램 메뉴에 Azure 포털에서에서 웹 앱을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-134">In hello Azure portal, in hello web app menu, restart your web app.</span></span>

<span data-ttu-id="d3c07-135">자세한 내용은 [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/)(WordPress 오류 로그 사용)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3c07-135">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="d3c07-136">App Service에 호스트된 앱에서 Python 응용 프로그램 오류를 기록하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="d3c07-136">How do I log Python application errors in apps that are hosted in App Service?</span></span>

<span data-ttu-id="d3c07-137">toocapture Python 응용 프로그램 오류:</span><span class="sxs-lookup"><span data-stu-id="d3c07-137">toocapture Python application errors:</span></span>

1. <span data-ttu-id="d3c07-138">Hello 웹 앱에서 Azure 포털에서에서 선택 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-138">In hello Azure portal, in your web app, select **Settings**.</span></span>
2. <span data-ttu-id="d3c07-139">Hello에 **설정** 탭에서 **응용 프로그램 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-139">On hello **Settings** tab, select **Application settings**.</span></span>
3. <span data-ttu-id="d3c07-140">아래 **앱 설정**를 키/값 쌍을 다음 hello 입력:</span><span class="sxs-lookup"><span data-stu-id="d3c07-140">Under **App settings**, enter hello following key/value pair:</span></span>
    * <span data-ttu-id="d3c07-141">키: WSGI_LOG</span><span class="sxs-lookup"><span data-stu-id="d3c07-141">Key : WSGI_LOG</span></span>
    * <span data-ttu-id="d3c07-142">값: D:\home\site\wwwroot\logs.txt(선택한 파일 이름 입력)</span><span class="sxs-lookup"><span data-stu-id="d3c07-142">Value : D:\home\site\wwwroot\logs.txt (enter your choice of file name)</span></span>

<span data-ttu-id="d3c07-143">이제 hello wwwroot 폴더에 hello logs.txt 파일에 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-143">You should now see errors in hello logs.txt file in hello wwwroot folder.</span></span>

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="d3c07-144">Hello 버전의 hello 앱 서비스에서 호스팅되는 Node.js 응용 프로그램을 변경 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="d3c07-144">How do I change hello version of hello Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="d3c07-145">toochange hello 버전의 hello Node.js 응용 프로그램에서는 hello 다음 옵션 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-145">toochange hello version of hello Node.js application, you can use one of hello following options:</span></span>

*   <span data-ttu-id="d3c07-146">Hello Azure 포털에서에서 사용 하 여 **앱 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-146">In hello Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="d3c07-147">Azure 포털 hello tooyour 웹 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-147">In hello Azure portal, go tooyour web app.</span></span>
    2. <span data-ttu-id="d3c07-148">Hello에 **설정** 블레이드를 **응용 프로그램 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-148">On hello **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="d3c07-149">**앱 설정**WEBSITE_NODE_DEFAULT_VERSION hello 키로 포함할 수 있으며 hello 버전의 Node.js 원하는 hello 값으로, 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-149">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as hello key, and hello version of Node.js you want as hello value.</span></span>
    4. <span data-ttu-id="d3c07-150">Tooyour 이동 [Kudu 콘솔](https://*yourwebsitename*.scm.azurewebsites.net)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-150">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="d3c07-151">toocheck은 Node.js 버전 hello, hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-151">toocheck hello Node.js version, enter hello following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="d3c07-152">Hello iisnode.yml 파일을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-152">Modify hello iisnode.yml file.</span></span> <span data-ttu-id="d3c07-153">Hello iisnode.yml 파일에 있는 hello Node.js 버전 변경만 hello 런타임 환경을 설정 해당 iisnode 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-153">Changing hello Node.js version in hello iisnode.yml file only sets hello runtime environment that iisnode uses.</span></span> <span data-ttu-id="d3c07-154">Kudu cmd 등과 여전히 hello Node.js 버전 사용에서 설정 된 **앱 설정** hello Azure 포털의에서.</span><span class="sxs-lookup"><span data-stu-id="d3c07-154">Your Kudu cmd and others still use hello Node.js version that is set in **App settings** in hello Azure portal.</span></span>

    <span data-ttu-id="d3c07-155">tooset hello iisnode.yml 응용 프로그램 루트 폴더에 있는 iisnode.yml 파일을 수동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-155">tooset hello iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="d3c07-156">Hello 파일에서 다음 줄 hello를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-156">In hello file, include hello following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="d3c07-157">소스 제어 배포가 동안 package.json을 사용 하 여 hello iisnode.yml 파일을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-157">Set hello iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="d3c07-158">hello Azure 소스 제어 배포 과정 단계를 수행 하는 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-158">hello Azure source control deployment process involves hello following steps:</span></span>
    1. <span data-ttu-id="d3c07-159">콘텐츠 toohello Azure 웹 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-159">Moves content toohello Azure web app.</span></span>
    2. <span data-ttu-id="d3c07-160">절이 없는 경우 (deploy.cmd,.deployment 파일) hello 웹 응용 프로그램 루트 폴더에는 기본 배포 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-160">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in hello web app root folder.</span></span>
    3. <span data-ttu-id="d3c07-161">해당 파일을 만듭니다 iisnode.yml hello package.json 파일에 있는 hello Node.js 버전을 언급 하는 경우 배포 스크립트를 실행 > 엔진`"engines": {"node": "5.9.1","npm": "3.7.3"}`</span><span class="sxs-lookup"><span data-stu-id="d3c07-161">Runs a deployment script in which it creates an iisnode.yml file if you mention hello Node.js version in hello package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="d3c07-162">hello iisnode.yml 파일에 다음 코드 줄을 hello:</span><span class="sxs-lookup"><span data-stu-id="d3c07-162">hello iisnode.yml file has hello following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="d3c07-163">앱 서비스에서 호스팅되는 내 WordPress 앱에서 "데이터베이스 연결 설정 오류" hello 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-163">I see hello message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="d3c07-164">이 문제를 어떻게 해결해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="d3c07-164">How do I troubleshoot this?</span></span>

<span data-ttu-id="d3c07-165">에 대 한 전체 hello 단계가 자세히 Azure WordPress 응용 프로그램, tooenable php_errors.log 및 디버그 로그에이 오류가 표시 되 면 [WordPress 사용 오류 로그](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-165">If you see this error in your Azure WordPress app, tooenable php_errors.log and debug.log, complete hello steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="d3c07-166">Hello 로그 설정 되 면 hello 오류를 재현 한 다음 hello 로그 toosee 연결에서 실행 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="d3c07-166">When hello logs are enabled, reproduce hello error, and then check hello logs toosee if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="d3c07-167">디버그 로그 또는 php_errors.log 파일에이 오류를 참조 하는 경우 앱이 hello 연결 수를 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-167">If you see this error in your debug.log or php_errors.log files, your app is exceeding hello number of connections.</span></span> <span data-ttu-id="d3c07-168">ClearDB를 호스팅하는 경우 hello에서 사용할 수 있는 연결 수를 확인 하면 [서비스 계획](https://www.cleardb.com/pricing.view)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-168">If you’re hosting on ClearDB, verify hello number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="d3c07-169">App Service에 호스트된 Node.js 앱을 디버그하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="d3c07-169">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="d3c07-170">Tooyour 이동 [Kudu 콘솔](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-170">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="d3c07-171">이동 tooyour 응용 프로그램 로그 폴더 (D:\home\LogFiles\Application)입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-171">Go tooyour application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="d3c07-172">Hello logging_errors.txt 파일에서 콘텐츠를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-172">In hello logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="d3c07-173">App Service 웹앱 또는 API 앱에서 기본 Python 모듈을 설치하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="d3c07-173">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="d3c07-174">일부 패키지는 Azure에서 pip를 사용하여 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-174">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="d3c07-175">hello 패키지 hello Python 패키지 인덱스에 사용할 수 없습니다 또는 컴파일러 해야 할 수 있습니다 (컴파일러에서 사용할 수 없으면 앱 서비스의 hello 웹 응용 프로그램을 실행 중인 hello 컴퓨터).</span><span class="sxs-lookup"><span data-stu-id="d3c07-175">hello package might not be available on hello Python Package Index, or a compiler might be required (a compiler is not available on hello computer that is running hello web app in App Service).</span></span> <span data-ttu-id="d3c07-176">App Service Web Apps 및 API Apps에서 기본 모듈을 설치하는 방법에 대한 자세한 내용은 [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/)(App Service에서 Python 모듈 설치)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3c07-176">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a><span data-ttu-id="d3c07-177">Python의 Git 및 hello 새 버전을 사용 하 여 Django 앱 tooApp 서비스를 어떻게 배포 합니까?</span><span class="sxs-lookup"><span data-stu-id="d3c07-177">How do I deploy a Django app tooApp Service by using Git and hello new version of Python?</span></span>

<span data-ttu-id="d3c07-178">Django 설치에 대 한 정보를 참조 하십시오. [Django 앱 tooApp 서비스 배포](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-178">For information about installing Django, see [Deploying a Django app tooApp Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-hello-tomcat-log-files-located"></a><span data-ttu-id="d3c07-179">에 있는 hello Tomcat 로그 파일은 어디에 있습니까?</span><span class="sxs-lookup"><span data-stu-id="d3c07-179">Where are hello Tomcat log files located?</span></span>

<span data-ttu-id="d3c07-180">Azure Marketplace 및 사용자 지정 배포의 경우:</span><span class="sxs-lookup"><span data-stu-id="d3c07-180">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="d3c07-181">폴더 위치: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span><span class="sxs-lookup"><span data-stu-id="d3c07-181">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="d3c07-182">관심 파일:</span><span class="sxs-lookup"><span data-stu-id="d3c07-182">Files of interest:</span></span>
    * <span data-ttu-id="d3c07-183">catalina.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d3c07-183">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="d3c07-184">host-manager.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d3c07-184">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="d3c07-185">localhost.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d3c07-185">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="d3c07-186">manager.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d3c07-186">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="d3c07-187">site_access_log.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d3c07-187">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="d3c07-188">포털 **앱 설정** 배포의 경우:</span><span class="sxs-lookup"><span data-stu-id="d3c07-188">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="d3c07-189">폴더 위치: D:\home\LogFiles</span><span class="sxs-lookup"><span data-stu-id="d3c07-189">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="d3c07-190">관심 파일:</span><span class="sxs-lookup"><span data-stu-id="d3c07-190">Files of interest:</span></span>
    * <span data-ttu-id="d3c07-191">catalina.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d3c07-191">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="d3c07-192">host-manager.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d3c07-192">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="d3c07-193">localhost.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d3c07-193">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="d3c07-194">manager.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d3c07-194">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="d3c07-195">site_access_log.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d3c07-195">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="d3c07-196">JDBC 드라이버 연결 오류를 해결하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="d3c07-196">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="d3c07-197">Hello Tomcat 로그에 메시지의 뒤에 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-197">You might see hello following message in your Tomcat logs:</span></span>

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="d3c07-198">tooresolve hello 오류:</span><span class="sxs-lookup"><span data-stu-id="d3c07-198">tooresolve hello error:</span></span>

1. <span data-ttu-id="d3c07-199">응용 프로그램/lib 폴더에서 hello sqljdbc*.jar 파일을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-199">Remove hello sqljdbc*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="d3c07-200">Hello 사용자 지정 Tomcat 또는 Azure 마켓플레이스 Tomcat 웹 서버를 사용 하는 경우이.jar 파일 toohello Tomcat lib 폴더를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-200">If you are using hello custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file toohello Tomcat lib folder.</span></span>
3. <span data-ttu-id="d3c07-201">Java를 사용 하는 경우 hello Azure 포털 (선택 **Java 1.8** > **Tomcat 서버**), 병렬 tooyour 앱 있는 hello 폴더에 hello sqljdbc.* jar 파일 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-201">If you are enabling Java from hello Azure portal (select **Java 1.8** > **Tomcat server**), copy hello sqljdbc.* jar file in hello folder that's parallel tooyour app.</span></span> <span data-ttu-id="d3c07-202">Hello 다음 클래스 경로 설정 toohello web.config 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-202">Then, add hello following classpath setting toohello web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a><span data-ttu-id="d3c07-203">Toocopy 실시간 로그 파일을 하려고 할 때 오류가 나타나는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="d3c07-203">Why do I see errors when I attempt toocopy live log files?</span></span>

<span data-ttu-id="d3c07-204">Java 응용 프로그램 (예: Tomcat)에 대 한 toocopy 실시간 로그 파일을 시도 하면이 FTP 오류가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-204">If you try toocopy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

<span data-ttu-id="d3c07-205">hello 오류 메시지가 hello FTP 클라이언트에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-205">hello error message might vary, depending on hello FTP client.</span></span>

<span data-ttu-id="d3c07-206">모든 Java 앱에는 이 잠금 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-206">All Java apps have this locking issue.</span></span> <span data-ttu-id="d3c07-207">Kudu만 지원 hello 응용 프로그램을 실행 하는 동안이 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-207">Only Kudu supports downloading this file while hello app is running.</span></span>

<span data-ttu-id="d3c07-208">중지 hello 앱 toothese 파일이 FTP 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-208">Stopping hello app allows FTP access toothese files.</span></span>

<span data-ttu-id="d3c07-209">다른 해결 방법은 toowrite 일정으로 실행 하 고 이러한 파일 tooa 다른 디렉터리를 복사 하는 웹 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-209">Another workaround is toowrite a WebJob that runs on a schedule and copies these files tooa different directory.</span></span> <span data-ttu-id="d3c07-210">샘플 프로젝트에 대 한 참조 hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="d3c07-210">For a sample project, see hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-hello-log-files-for-jetty"></a><span data-ttu-id="d3c07-211">Jetty에 대 한 로그 파일 hello를 어디서 찾을 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="d3c07-211">Where do I find hello log files for Jetty?</span></span>

<span data-ttu-id="d3c07-212">Marketplace와 사용자 지정 배포에 대 한 hello 로그 파일은 hello D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-212">For Marketplace and custom deployments, hello log file is in hello D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="d3c07-213">참고 hello 폴더 위치를 사용 하는 jetty hello 버전에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-213">Note that hello folder location depends on hello version of Jetty you are using.</span></span> <span data-ttu-id="d3c07-214">예를 들어 hello 경로가 제공 Jetty 9.1.2에 대 한 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-214">For example, hello path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="d3c07-215">jetty_*YYYY_MM_DD*.stderrout.log를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-215">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="d3c07-216">포털 응용 프로그램 설정 배포에 대 한 hello 로그 파일이 D:\home\LogFiles입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-216">For portal App Setting deployments, hello log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="d3c07-217">jetty_*YYYY_MM_DD*.stderrout.log 찾기</span><span class="sxs-lookup"><span data-stu-id="d3c07-217">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="d3c07-218">내 Azure 웹앱에서 메일을 보낼 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d3c07-218">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="d3c07-219">App Service에는 기본 제공 메일 기능이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-219">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="d3c07-220">앱에서 메일을 보낼 수 있는 다른 좋은 방법은 이 [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure)(스택 오버플로 토론)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3c07-220">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a><span data-ttu-id="d3c07-221">내 WordPress 사이트 tooanother URL를 리디렉션하도록 하는 이유</span><span class="sxs-lookup"><span data-stu-id="d3c07-221">Why does my WordPress site redirect tooanother URL?</span></span>

<span data-ttu-id="d3c07-222">TooAzure 최근에 마이그레이션한 경우 WordPress toohello 이전 도메인 URL을 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-222">If you have recently migrated tooAzure, WordPress might redirect toohello old domain URL.</span></span> <span data-ttu-id="d3c07-223">이 설정 hello MySQL 데이터베이스에 의해 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-223">This is caused by a setting in hello MySQL database.</span></span>

<span data-ttu-id="d3c07-224">WordPress 버디 + hello 데이터베이스에서 직접 tooupdate hello 리디렉션 URL을 사용할 수 있는 Azure 사이트 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-224">WordPress Buddy+ is an Azure Site Extension that you can use tooupdate hello redirection URL directly in hello database.</span></span> <span data-ttu-id="d3c07-225">WordPress Buddy+ 사용에 대한 자세한 내용은 [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)(WordPress Buddy+를 사용한 WordPress 도구 및 MySQL 마이그레이션)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3c07-225">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="d3c07-226">SQL 쿼리 또는 PHPMyAdmin 사용 하 여 toomanually 업데이트 hello 리디렉션 URL을 선호 하는 경우 참조 또는 [WordPress: toowrong URL 리디렉션](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-226">Alternatively, if you prefer toomanually update hello redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting toowrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="d3c07-227">내 WordPress 로그인 암호를 어떻게 변경할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="d3c07-227">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="d3c07-228">WordPress 로그인 암호를 잊어버린 경우에 WordPress 버디 + tooupdate을 사용할 수 있습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-228">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ tooupdate it.</span></span> <span data-ttu-id="d3c07-229">암호, WordPress Azure 버디 + 사이트 확장을 설치 hello 및 다음 전체 hello 단계에 설명 된 tooreset [WordPress 도구 및 MySQL 마이그레이션 WordPress 버디 + 준수](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-229">tooreset your password, install hello WordPress Buddy+ Azure Site Extension, and then complete hello steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a><span data-ttu-id="d3c07-230">TooWordPress 로그인 할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-230">I can't sign in tooWordPress.</span></span> <span data-ttu-id="d3c07-231">이 문제를 해결하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="d3c07-231">How do I resolve this?</span></span>

<span data-ttu-id="d3c07-232">최근에 플러그 인을 설치한 후 WordPress에서 잠긴 것을 알았다면 잘못된 플러그 인이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-232">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="d3c07-233">WordPress Buddy+는 WordPress에서 플러그 인을 사용하지 않도록 설정할 수 있는 Azure 사이트 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-233">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="d3c07-234">자세한 내용은 [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)(WordPress Buddy+를 사용한 WordPress 도구 및 MySQL 마이그레이션)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3c07-234">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="d3c07-235">내 WordPress 데이터베이스를 마이그레이션하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="d3c07-235">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="d3c07-236">마이그레이션 hello MySQL 데이터베이스는 연결 된 tooyour WordPress 웹 사이트에 대 한 여러 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-236">You have multiple options for migrating hello MySQL database that's connected tooyour WordPress website:</span></span>

* <span data-ttu-id="d3c07-237">개발자: 사용 하 여 hello [명령 프롬프트 또는 PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span><span class="sxs-lookup"><span data-stu-id="d3c07-237">Developers: Use hello [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="d3c07-238">비 개발자: [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) 사용</span><span class="sxs-lookup"><span data-stu-id="d3c07-238">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="d3c07-239">WordPress의 보안을 강화하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="d3c07-239">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="d3c07-240">WordPress에 대 한 보안 모범 사례에 대 한 toolearn 참조 [Azure에서 WordPress 보안에 대 한 유용한](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-240">toolearn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="d3c07-241">Toouse PHPMyAdmin, 려을 hello 메시지 "액세스가 거부 되었습니다." 표시</span><span class="sxs-lookup"><span data-stu-id="d3c07-241">I am trying toouse PHPMyAdmin, and I see hello message “Access denied.”</span></span> <span data-ttu-id="d3c07-242">이 문제를 해결하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="d3c07-242">How do I resolve this?</span></span>

<span data-ttu-id="d3c07-243">이 앱 서비스 인스턴스에서 아직 실행 되지 않고 hello MySQL 앱에서 기능 하는 경우이 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-243">You might experience this issue if hello MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="d3c07-244">tooresolve 문제, try tooaccess 웹 사이트를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-244">tooresolve hello issue, try tooaccess your website.</span></span> <span data-ttu-id="d3c07-245">이 앱에서 MySQL hello 프로세스를 비롯 한 hello 필요한 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-245">This starts hello required processes, including hello MySQL in-app process.</span></span> <span data-ttu-id="d3c07-246">프로세스 탐색기에서 앱에서 실행 중인 MySQL 해당 mysqld.exe 확인는 tooverify hello 프로세스에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-246">tooverify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in hello processes.</span></span>

<span data-ttu-id="d3c07-247">앱에서 MySQL 실행 되 고 있는지 확인 한 후 toouse PHPMyAdmin 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="d3c07-247">After you ensure that MySQL in-app is running, try toouse PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="d3c07-248">Tooimport 시도 하거나 PHPMyadmin를 사용 하 여 앱에서 MySQL 데이터베이스를 내보낼 때 HTTP 403 오류가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-248">I get an HTTP 403 error when I try tooimport or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="d3c07-249">이 문제를 해결하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="d3c07-249">How do I resolve this?</span></span>

<span data-ttu-id="d3c07-250">이전 버전의 Chrome을 사용하고 있으면 알려진 버그가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-250">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="d3c07-251">최신 버전의 Chrome 업그레이드 tooa tooresolve hello 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3c07-251">tooresolve hello issue, upgrade tooa newer version of Chrome.</span></span> <span data-ttu-id="d3c07-252">또한 Internet Explorer 또는 hello 문제가 발생 하지 않으면 가장자리와 같은 다른 브라우저를 사용해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="d3c07-252">Also try using a different browser, like Internet Explorer or Edge, where hello issue does not occur.</span></span>
