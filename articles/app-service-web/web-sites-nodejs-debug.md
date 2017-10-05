---
title: "Azure 앱 서비스에서 Node.js 웹 앱을 디버그하는 방법"
description: "Azure 앱 서비스에서 Node.js 웹 앱을 디버그하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 5e302a4c58a171d40e43a22c34c724e868019ec8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-debug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="f4a1e-103">Azure 앱 서비스에서 Node.js 웹 앱을 디버그하는 방법</span><span class="sxs-lookup"><span data-stu-id="f4a1e-103">How to debug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="f4a1e-104">Azure는 [Azure 웹 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 웹 앱에 호스트되는 Node.js 응용 프로그램을 디버그하는 데 도움이 되는 기본 제공 진단 로그를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-104">Azure provides built-in diagnostics to assist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="f4a1e-105">이 문서에서는 stdout 및 stderr의 로깅을 사용하고, 브라우저에서 오류 정보를 표시하고, 로그 파일을 다운로드하여 보는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-105">In this article, you will learn how to enable logging of stdout and stderr, display error information in the browser, and how to download and view log files.</span></span>

<span data-ttu-id="f4a1e-106">Azure에서 호스트되는 Node.js 응용 프로그램에 대한 진단은 [IISNode]에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="f4a1e-107">이 문서에서 진단 정보 수집에 대한 가장 일반적인 설정을 논의하긴 하지만 IISNode 작업을 모두 다루지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-107">While this article discusses the most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="f4a1e-108">IISNode 작업에 대한 자세한 내용은 GitHub의 [IISNode 추가 정보] (영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-108">For more information on working with IISNode, see the [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="f4a1e-109">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="f4a1e-109">Enable logging</span></span>
<span data-ttu-id="f4a1e-110">기본적으로, 앱 서비스 웹 앱은 배포에 대한 진단 정보만 캡처합니다(예: Git를 사용하여 웹 앱을 배포하는 경우).</span><span class="sxs-lookup"><span data-stu-id="f4a1e-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="f4a1e-111">이 정보는 **package.json**에 참조된 모듈을 설치하거나 사용자 지정 배포 스크립트를 사용하는 경우에 실패가 발생하는 등 배포하는 동안 문제가 발생할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="f4a1e-112">stdout 및 stderr 스트림에 대한 로깅을 사용하려면 Node.js 응용 프로그램의 루트에서 **IISNode.yml** 파일을 만들고 다음을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-112">To enable the logging of stdout and stderr streams, you must create an **IISNode.yml** file at the root of your Node.js application and add the following:</span></span>

    loggingEnabled: true

<span data-ttu-id="f4a1e-113">그러면 Node.js 응용 프로그램에서 stderr 및 stdout에 대한 로깅이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-113">This enables the logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="f4a1e-114">**IISNode.yml** 파일을 사용하여 실패가 발생할 때 브라우저로 친숙한 오류를 반환할지 아니면 개발자 오류를 반환할지 여부도 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-114">The **IISNode.yml** file can also be used to control whether friendly errors or developer errors are returned to the browser when a failure occurs.</span></span> <span data-ttu-id="f4a1e-115">개발자 오류를 사용하려면 **IISNode.yml** 파일에 다음 줄을 추가하십시오.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-115">To enable developer errors, add the following line to the **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="f4a1e-116">이 옵션을 사용하도록 설정하면 IISNode가 친숙한 오류(예: "내부 서버 오류가 발생했습니다.") 대신 stderr에 전송된 정보의 마지막 64K를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-116">Once this option is enabled, IISNode will return the last 64K of information sent to stderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="f4a1e-117">devErrorsEnabled가 개발 중 문제를 진단하는 데 유용하긴 하지만 프로덕션 환경에서 이 옵션을 사용하도록 설정하면 개발 오류가 최종 사용자에게 전달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent to end users.</span></span>
> 
> 

<span data-ttu-id="f4a1e-118">**IISNode.yml** 파일이 응용 프로그램에 아직 없는 경우, 업데이트된 응용 프로그램을 게시한 후 웹 앱을 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-118">If the **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing the updated application.</span></span> <span data-ttu-id="f4a1e-119">이전에 게시했던 기존 **IISNode.yml** 파일에서 설정만 변경하는 경우에는 다시 시작하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="f4a1e-120">Azure 명령줄 도구 또는 Azure PowerShell Cmdlet을 사용하여 웹 앱을 만든 경우 기본 **IISNode.yml** 파일이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-120">If your web app was created using the Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="f4a1e-121">웹앱을 다시 시작하려면 [Azure 포털](https://portal.azure.com)에서 웹앱을 선택한 다음 **다시 시작** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-121">To restart the web app, select the web app in the [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![다시 시작 단추][restart-button]

<span data-ttu-id="f4a1e-123">Azure 명령줄 도구가 개발 환경에 설치되어 있는 경우 다음 명령을 사용하여 웹 앱을 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-123">If the Azure Command-Line Tools are installed in your development environment, you can use the following command to restart the web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="f4a1e-124">loggingEnabled 및 devErrorsEnabled가 진단 정보를 캡처하기 위해 가장 일반적으로 사용되는 IISNode.yml 구성 옵션이긴 하지만 IISNode.yml을 사용하여 호스팅 환경을 위한 다양한 옵션을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-124">While loggingEnabled and devErrorsEnabled are the most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used to configure a variety of options for your hosting environment.</span></span> <span data-ttu-id="f4a1e-125">전체 구성 옵션 목록에 대해서는 [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml)(영문) 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-125">For a full list of the configuration options, see the [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="f4a1e-126">로그 액세스</span><span class="sxs-lookup"><span data-stu-id="f4a1e-126">Accessing logs</span></span>
<span data-ttu-id="f4a1e-127">진단 로그에는 세 가지 방법 즉, FTP(파일 전송 프로토콜) 사용이나 Zip 보관 파일 다운로드를 통해 또는 로그(또는 비상 로그)의 업데이트된 라이브 스트림으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-127">Diagnostic logs can be accessed in three ways; Using the File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of the log (also known as a tail).</span></span> <span data-ttu-id="f4a1e-128">로그 파일의 Zip 보관 파일을 다운로드하거나 라이브 스트림을 보려면 Azure 명령줄 도구가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-128">Downloading the Zip archive of the log files or viewing the live stream require the Azure Command-Line Tools.</span></span> <span data-ttu-id="f4a1e-129">다음 명령을 사용하여 명령줄 도구를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-129">These can be installed by using the following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="f4a1e-130">설치한 도구에는 'azure' 명령을 사용하여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-130">Once installed, the tools can be accessed using the 'azure' command.</span></span> <span data-ttu-id="f4a1e-131">먼저 Azure 구독을 사용하도록 명령줄 도구를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-131">The command-line tools must first be configured to use your Azure subscription.</span></span> <span data-ttu-id="f4a1e-132">이 작업을 수행하는 방법에 대한 자세한 내용은 **Azure 명령줄 도구 사용 방법** (영문) 문서의 [게시 설정을 다운로드하여 가져오는 방법](../xplat-cli-connect.md) 섹션을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-132">For information on how to accomplish this task, see the **How to download and import publish settings** section of the [How to Use The Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="f4a1e-133">FTP</span><span class="sxs-lookup"><span data-stu-id="f4a1e-133">FTP</span></span>
<span data-ttu-id="f4a1e-134">FTP를 통해 진단 정보에 액세스하려면 [Azure 포털](https://portal.azure.com)을 방문하고, 웹앱을 선택한 후 **대시보드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-134">To access the diagnostic information through FTP, visit the [Azure Portal](https://portal.azure.com), select your web app, and then select the **DASHBOARD**.</span></span> <span data-ttu-id="f4a1e-135">**빠른 연결** 섹션에서 **FTP 진단 로그** 및 **FTPS 진단 로그** 링크는 FTP 프로토콜을 사용하여 로그에 액세스할 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-135">In the **quick links** section, the **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access to the logs using the FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="f4a1e-136">FTP 또는 배포의 사용자 이름 및 암호를 아직 구성하지 않은 경우 **배포 자격 증명 설정**을 선택하여 **빠른 시작** 관리 페이지에서 사용자 이름 및 암호를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-136">If you have not previously configured user name and password for FTP or deployment, you can do so from the **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="f4a1e-137">대시보드에 반환된 FTP URL은 다음 하위 디렉터리를 포함하는 **LogFiles** 디렉터리에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-137">The FTP URL returned in the dashboard is for the **LogFiles** directory, which will contain the following sub-directories:</span></span>

* <span data-ttu-id="f4a1e-138">[배포 방법](web-sites-deploy.md) - Git와 같은 배포 방법을 사용하는 경우 동일한 이름의 디렉터리가 만들어지고 배포와 관련된 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
* <span data-ttu-id="f4a1e-139">nodejs - 응용 프로그램의 모든 인스턴스에서 캡처된 stdout 및 stderr 정보(loggingEnabled가 True인 경우)</span><span class="sxs-lookup"><span data-stu-id="f4a1e-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="f4a1e-140">Zip 보관 파일</span><span class="sxs-lookup"><span data-stu-id="f4a1e-140">Zip archive</span></span>
<span data-ttu-id="f4a1e-141">진단 로그의 Zip 보관 파일을 다운로드하려면 Azure 명령줄 도구에서 다음 명령을 사용하십시오.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-141">To download a Zip archive of the diagnostic logs, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="f4a1e-142">현재 디렉터리에 **diagnostics.zip** 이 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-142">This will download a **diagnostics.zip** in the current directory.</span></span> <span data-ttu-id="f4a1e-143">이 보관 파일은 다음 디렉터리 구조를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-143">This archive contains the following directory structure:</span></span>

* <span data-ttu-id="f4a1e-144">deployments - 응용 프로그램의 배포에 대한 정보 로그</span><span class="sxs-lookup"><span data-stu-id="f4a1e-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="f4a1e-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="f4a1e-145">LogFiles</span></span>
  
  * <span data-ttu-id="f4a1e-146">[배포 방법](web-sites-deploy.md) - Git와 같은 배포 방법을 사용하는 경우 동일한 이름의 디렉터리가 만들어지고 배포와 관련된 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
  * <span data-ttu-id="f4a1e-147">nodejs - 응용 프로그램의 모든 인스턴스에서 캡처된 stdout 및 stderr 정보(loggingEnabled가 True인 경우)</span><span class="sxs-lookup"><span data-stu-id="f4a1e-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="f4a1e-148">라이브 스트림(비상 로그)</span><span class="sxs-lookup"><span data-stu-id="f4a1e-148">Live stream (tail)</span></span>
<span data-ttu-id="f4a1e-149">진단 로그 정보의 라이브 스트림을 보려면 Azure 명령줄 도구에서 다음 명령을 사용하십시오.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-149">To view a live stream of diagnostic log information, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="f4a1e-150">서버에서 발생하는 업데이트된 로그 이벤트의 스트림이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-150">This will return a stream of log events that are updated as they occur on the server.</span></span> <span data-ttu-id="f4a1e-151">이 스트림은 배포 정보와 stdout 및 stderr 정보를 반환합니다(loggingEnabled가 True인 경우).</span><span class="sxs-lookup"><span data-stu-id="f4a1e-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="f4a1e-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4a1e-152">Next Steps</span></span>
<span data-ttu-id="f4a1e-153">이 문서에서는 Azure에 대한 진단 정보를 사용하고 액세스하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-153">In this article you learned how to enable and access diagnostics information for Azure.</span></span> <span data-ttu-id="f4a1e-154">이 정보는 응용 프로그램에서 발생하는 문제를 이해하는 데 유용하며, 사용 중인 모듈의 문제를 나타내거나 앱 서비스 웹 앱에 사용된 Node.js 버전이 배포 환경에 사용된 버전과 다르다는 점을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-154">While this information is useful in understanding problems that occur with your application, it may point to a problem with a module you are using or that the version of Node.js used by App Service Web Apps is different than the one used in your deployment environment.</span></span>

<span data-ttu-id="f4a1e-155">Azure에서 모듈 작업에 대한 자세한 내용은 [Azure 응용 프로그램에 Node.js 모듈 사용](../nodejs-use-node-modules-azure-apps.md)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="f4a1e-156">Node.js 버전의 응용 프로그램 지정에 대한 자세한 내용은 [Azure 응용 프로그램에서 Node.js 버전 지정]을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="f4a1e-157">자세한 내용은 [Node.js 개발자 센터](/develop/nodejs/)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-157">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="f4a1e-158">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="f4a1e-158">What's changed</span></span>
* <span data-ttu-id="f4a1e-159">웹 사이트에서 앱 서비스로의 변경에 대한 지침은 [Azure 앱 서비스와 이 서비스가 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f4a1e-159">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="f4a1e-160">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-160">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f4a1e-161">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4a1e-161">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="f4a1e-162">[IISNode]: https://github.com/tjanczuk/iisnode</span><span class="sxs-lookup"><span data-stu-id="f4a1e-162">[IISNode]: https://github.com/tjanczuk/iisnode</span></span>
<span data-ttu-id="f4a1e-163">[IISNode 추가 정보]: https://github.com/tjanczuk/iisnode#readme</span><span class="sxs-lookup"><span data-stu-id="f4a1e-163">[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme</span></span>
[How to Use The Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
<span data-ttu-id="f4a1e-164">[Azure 응용 프로그램에서 Node.js 버전 지정]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="f4a1e-164">[Specifying a Node.js version in an Azure application]: ../nodejs-specify-node-version-azure-apps.md</span></span>

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

