---
title: "aaaHow toodebug Azure 앱 서비스에 Node.js 웹 응용 프로그램"
description: "어떻게 toodebug는 Node.js 웹 Azure 앱 서비스의 앱에 알아봅니다."
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="816eb-103">어떻게 toodebug는 Node.js 웹 응용 프로그램을 Azure 앱 서비스</span><span class="sxs-lookup"><span data-stu-id="816eb-103">How toodebug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="816eb-104">Azure에서 호스팅되는 Node.js 응용 프로그램 디버깅에 기본 제공 진단 tooassist 제공 [Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-104">Azure provides built-in diagnostics tooassist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="816eb-105">이 문서에서는 살펴보겠습니다 어떻게 stdout 및 stderr, hello 브라우저에 오류 정보를 표시 및 어떻게 toodownload 뷰와 로그 파일의 tooenable 로깅을 합니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-105">In this article, you will learn how tooenable logging of stdout and stderr, display error information in hello browser, and how toodownload and view log files.</span></span>

<span data-ttu-id="816eb-106">Azure에서 호스트되는 Node.js 응용 프로그램에 대한 진단은 [IISNode]에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="816eb-107">진단 정보 수집에 대 한 가장 일반적인 설정을 hello 설명, 수 있으며 IISNode 작업에 대 한 전체 참조는 제공 수 않습니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-107">While this article discusses hello most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="816eb-108">IISNode 사용한 작업에 대 한 자세한 내용은 참조 hello [IISNode Readme] GitHub에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-108">For more information on working with IISNode, see hello [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="816eb-109">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="816eb-109">Enable logging</span></span>
<span data-ttu-id="816eb-110">기본적으로, 앱 서비스 웹 앱은 배포에 대한 진단 정보만 캡처합니다(예: Git를 사용하여 웹 앱을 배포하는 경우).</span><span class="sxs-lookup"><span data-stu-id="816eb-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="816eb-111">이 정보는 **package.json**에 참조된 모듈을 설치하거나 사용자 지정 배포 스크립트를 사용하는 경우에 실패가 발생하는 등 배포하는 동안 문제가 발생할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="816eb-112">tooenable hello stdout 및 stderr 스트림의 로깅, 만들어야는 **IISNode.yml** Node.js 응용 프로그램의 hello 루트에 있는 파일 및 hello 다음 추가:</span><span class="sxs-lookup"><span data-stu-id="816eb-112">tooenable hello logging of stdout and stderr streams, you must create an **IISNode.yml** file at hello root of your Node.js application and add hello following:</span></span>

    loggingEnabled: true

<span data-ttu-id="816eb-113">이 Node.js 응용 프로그램에서 stdout 및 stderr의 hello 로깅을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-113">This enables hello logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="816eb-114">hello **IISNode.yml** 친숙 한 오류 또는 개발자 오류가 반환될지 toohello 브라우저 오류가 발생 하는지 여부를 파일에 사용 되는 toocontrol 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-114">hello **IISNode.yml** file can also be used toocontrol whether friendly errors or developer errors are returned toohello browser when a failure occurs.</span></span> <span data-ttu-id="816eb-115">tooenable 개발자 오류 추가 줄 toohello 다음 hello **IISNode.yml** 파일:</span><span class="sxs-lookup"><span data-stu-id="816eb-115">tooenable developer errors, add hello following line toohello **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="816eb-116">이 옵션을 사용 하도록 설정, IISNode hello 마지막 64k "내부 서버 오류가 발생 했습니다."와 같은 친숙 한 오류 대신 toostderr 전달 되는 정보를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-116">Once this option is enabled, IISNode will return hello last 64K of information sent toostderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="816eb-117">Tooend 사용자가 전송 되는 개발 오류 개발 하는 동안 문제를 진단할 때 devErrorsEnabled 기능은 유용 하지만 프로덕션 환경에서 사용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent tooend users.</span></span>
> 
> 

<span data-ttu-id="816eb-118">경우 hello **IISNode.yml** 파일 응용 프로그램 내에서 이미 존재 하지 않으면, 업데이트 하는 hello 응용 프로그램을 게시 한 후 웹 앱을 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-118">If hello **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing hello updated application.</span></span> <span data-ttu-id="816eb-119">이전에 게시했던 기존 **IISNode.yml** 파일에서 설정만 변경하는 경우에는 다시 시작하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="816eb-120">웹 앱 hello Azure 명령줄 도구 또는 Azure PowerShell Cmdlet, 기본값을 사용 하 여 만들어진 경우 **IISNode.yml** 파일이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-120">If your web app was created using hello Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="816eb-121">toorestart hello 웹 응용 프로그램에서 hello의 웹 앱 선택 hello [Azure 포털](https://portal.azure.com), 클릭 하 고 **다시 시작** 단추:</span><span class="sxs-lookup"><span data-stu-id="816eb-121">toorestart hello web app, select hello web app in hello [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![다시 시작 단추][restart-button]

<span data-ttu-id="816eb-123">Hello Azure Command-Line Tools 개발 환경에서 설치 된 경우에 hello 명령 toorestart hello 웹 앱에 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-123">If hello Azure Command-Line Tools are installed in your development environment, you can use hello following command toorestart hello web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="816eb-124">LoggingEnabled 및 devErrorsEnabled 진단 정보 캡처를 위한 가장 일반적으로 사용 하는 hello IISNode.yml 구성 옵션을 사용 하는 다양 한 호스팅 환경에 대 한 옵션 tooconfigure IISNode.yml 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-124">While loggingEnabled and devErrorsEnabled are hello most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used tooconfigure a variety of options for your hosting environment.</span></span> <span data-ttu-id="816eb-125">Hello 구성 옵션의 전체 목록을 보려면 hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-125">For a full list of hello configuration options, see hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="816eb-126">로그 액세스</span><span class="sxs-lookup"><span data-stu-id="816eb-126">Accessing logs</span></span>
<span data-ttu-id="816eb-127">진단 로그는 세 가지 방법으로;에서 액세스할 수 있습니다. Hello FTP 파일 전송 프로토콜 ()를 다운로드 하는 Zip 보관 파일을 사용 하 여 또는 라이브 업데이트 hello 로그 (비상)의 스트림입니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-127">Diagnostic logs can be accessed in three ways; Using hello File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of hello log (also known as a tail).</span></span> <span data-ttu-id="816eb-128">Hello 로그 파일의 hello Zip 보관 파일을 다운로드 하거나 hello 라이브 스트림 보기 hello Azure Command-Line Tools 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-128">Downloading hello Zip archive of hello log files or viewing hello live stream require hello Azure Command-Line Tools.</span></span> <span data-ttu-id="816eb-129">이러한 hello 다음 명령을 사용 하 여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-129">These can be installed by using hello following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="816eb-130">설치 되 면 hello 'azure' 명령을 사용 하 여 hello 도구를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-130">Once installed, hello tools can be accessed using hello 'azure' command.</span></span> <span data-ttu-id="816eb-131">명령줄 도구를 hello 해야 구성된 toouse Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="816eb-131">hello command-line tools must first be configured toouse your Azure subscription.</span></span> <span data-ttu-id="816eb-132">어떻게 tooaccomplish이 작업에 대 한 내용은 hello 참조 **toodownload 및 가져오기 게시 설정에 어떻게** hello의 섹션 [어떻게 tooUse hello Azure Command-Line Tools](../xplat-cli-connect.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="816eb-132">For information on how tooaccomplish this task, see hello **How toodownload and import publish settings** section of hello [How tooUse hello Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="816eb-133">FTP</span><span class="sxs-lookup"><span data-stu-id="816eb-133">FTP</span></span>
<span data-ttu-id="816eb-134">FTP 통해 tooaccess hello 진단 정보 방문 hello [Azure 포털](https://portal.azure.com), 웹 앱을 선택한 다음 선택 hello **대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-134">tooaccess hello diagnostic information through FTP, visit hello [Azure Portal](https://portal.azure.com), select your web app, and then select hello **DASHBOARD**.</span></span> <span data-ttu-id="816eb-135">Hello에 **빠른 링크** 섹션 hello **FTP 진단 로그** 및 **FTPS 진단 로그** hello FTP 프로토콜을 사용 하 여 액세스 toohello 로그 링크를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-135">In hello **quick links** section, hello **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access toohello logs using hello FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="816eb-136">하지 이전에 구성한 경우 사용자 이름 및 암호 FTP 나 개발을 위한, 그렇게 할 수 있습니다 hello에서 **퀵 스타트** 관리 페이지를 선택 하 여 **배포 자격 증명 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-136">If you have not previously configured user name and password for FTP or deployment, you can do so from hello **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="816eb-137">hello hello 대시보드에서 반환 된 FTP URL은 hello에 대 한 **LogFiles** hello 다음 하위 디렉터리를 포함 하는 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="816eb-137">hello FTP URL returned in hello dashboard is for hello **LogFiles** directory, which will contain hello following sub-directories:</span></span>

* <span data-ttu-id="816eb-138">[배포 방법](web-sites-deploy.md) -이름이 같은 생성 되 고 정보를 포함 하는 hello의 디렉터리 관련 toodeployments Git와 같은 배포 방법을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="816eb-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
* <span data-ttu-id="816eb-139">nodejs - 응용 프로그램의 모든 인스턴스에서 캡처된 stdout 및 stderr 정보(loggingEnabled가 True인 경우)</span><span class="sxs-lookup"><span data-stu-id="816eb-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="816eb-140">Zip 보관 파일</span><span class="sxs-lookup"><span data-stu-id="816eb-140">Zip archive</span></span>
<span data-ttu-id="816eb-141">toodownload hello Azure 명령줄 도구에서 다음 명령을 사용 하 여 hello hello 진단 로그의 Zip 보관:</span><span class="sxs-lookup"><span data-stu-id="816eb-141">toodownload a Zip archive of hello diagnostic logs, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="816eb-142">다운로드 됩니다는 **diagnostics.zip** hello 현재 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-142">This will download a **diagnostics.zip** in hello current directory.</span></span> <span data-ttu-id="816eb-143">이 보관 디렉터리 구조를 다음 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-143">This archive contains hello following directory structure:</span></span>

* <span data-ttu-id="816eb-144">deployments - 응용 프로그램의 배포에 대한 정보 로그</span><span class="sxs-lookup"><span data-stu-id="816eb-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="816eb-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="816eb-145">LogFiles</span></span>
  
  * <span data-ttu-id="816eb-146">[배포 방법](web-sites-deploy.md) -이름이 같은 생성 되 고 정보를 포함 하는 hello의 디렉터리 관련 toodeployments Git와 같은 배포 방법을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="816eb-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
  * <span data-ttu-id="816eb-147">nodejs - 응용 프로그램의 모든 인스턴스에서 캡처된 stdout 및 stderr 정보(loggingEnabled가 True인 경우)</span><span class="sxs-lookup"><span data-stu-id="816eb-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="816eb-148">라이브 스트림(비상 로그)</span><span class="sxs-lookup"><span data-stu-id="816eb-148">Live stream (tail)</span></span>
<span data-ttu-id="816eb-149">진단 로그 정보를 hello Azure 명령줄 도구에서 다음 명령을 사용 하 여 hello 라이브 스트림 tooview:</span><span class="sxs-lookup"><span data-stu-id="816eb-149">tooview a live stream of diagnostic log information, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="816eb-150">서버 hello에 나타나는 순서 대로 업데이트 되는 이벤트 로그의 스트림을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-150">This will return a stream of log events that are updated as they occur on hello server.</span></span> <span data-ttu-id="816eb-151">이 스트림은 배포 정보와 stdout 및 stderr 정보를 반환합니다(loggingEnabled가 True인 경우).</span><span class="sxs-lookup"><span data-stu-id="816eb-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="816eb-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="816eb-152">Next Steps</span></span>
<span data-ttu-id="816eb-153">이 방법에 대해 배웠습니다 문서 Azure에 대 한 진단 정보 tooenable 및 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-153">In this article you learned how tooenable and access diagnostics information for Azure.</span></span> <span data-ttu-id="816eb-154">이 정보에 유용 하지만 사용 하는 모듈 또는 해당 hello 버전 앱 서비스 웹 앱에서 사용 하는 Node.js의 tooa 문제가 원인일 응용 프로그램에 발생 하는 이해 문제 차이가 있는 hello 배포에 사용 된 것 보다 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-154">While this information is useful in understanding problems that occur with your application, it may point tooa problem with a module you are using or that hello version of Node.js used by App Service Web Apps is different than hello one used in your deployment environment.</span></span>

<span data-ttu-id="816eb-155">Azure에서 모듈 작업에 대한 자세한 내용은 [Azure 응용 프로그램에 Node.js 모듈 사용](../nodejs-use-node-modules-azure-apps.md)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="816eb-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="816eb-156">Node.js 버전의 응용 프로그램 지정에 대한 자세한 내용은 [Azure 응용 프로그램에서 Node.js 버전 지정]을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="816eb-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="816eb-157">자세한 내용은 참고 항목 hello [Node.js 개발자 센터](/develop/nodejs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-157">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="816eb-158">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="816eb-158">What's changed</span></span>
* <span data-ttu-id="816eb-159">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="816eb-159">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="816eb-160">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-160">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="816eb-161">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="816eb-161">No credit cards required; no commitments.</span></span>
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[Azure 응용 프로그램에서 Node.js 버전 지정]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

