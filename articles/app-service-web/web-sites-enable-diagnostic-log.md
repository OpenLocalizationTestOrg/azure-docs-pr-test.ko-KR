---
title: "Azure 앱 서비스에서 웹앱에 대한 진단 로깅 설정"
description: "진단 로그를 사용하도록 설정하는 방법, 응용 프로그램에 계측을 추가하는 방법 및 Azure에서 기록된 정보에 액세스하는 방법에 대해 알아봅니다."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: c9da27b2-47d4-4c33-a3cb-1819955ee43b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2016
ms.author: cephalin
ms.openlocfilehash: 7b125aeb9c0ee1dcbb199da98b0ce079820ea85c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-diagnostics-logging-for-web-apps-in-azure-app-service"></a><span data-ttu-id="7ec31-103">Azure 앱 서비스에서 웹앱에 대한 진단 로깅 설정</span><span class="sxs-lookup"><span data-stu-id="7ec31-103">Enable diagnostics logging for web apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="7ec31-104">개요</span><span class="sxs-lookup"><span data-stu-id="7ec31-104">Overview</span></span>
<span data-ttu-id="7ec31-105">Azure는 [앱 서비스 웹앱](http://go.microsoft.com/fwlink/?LinkId=529714)을 디버그하는 데 도움이 되는 기본 제공 진단을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-105">Azure provides built-in diagnostics to assist with debugging an [App Service web app](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="7ec31-106">이 문서에서는 진단 로그를 사용하도록 설정하는 방법, 응용 프로그램에 계측을 추가하는 방법 및 Azure에서 기록된 정보에 액세스하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-106">In this article you'll learn how to enable diagnostic logging and add instrumentation to your application, as well as how to access the information logged by Azure.</span></span>

<span data-ttu-id="7ec31-107">이 문서에서는 진단 로그와 같이 작업하기 위해 [Azure 포털](https://portal.azure.com), Azure PowerShell, 그리고 Azure CLI(Azure Command-Line Interface, Azure 명령줄 인터페이스)가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-107">This article uses the [Azure Portal](https://portal.azure.com), Azure PowerShell, and the Azure Command-Line Interface (Azure CLI) to work with diagnostic logs.</span></span> <span data-ttu-id="7ec31-108">Visual Studio를 사용하여 진단 로그로 작업하는 방법에 대한 자세한 내용은 [Visual Studio에서 Azure 문제 해결](web-sites-dotnet-troubleshoot-visual-studio.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ec31-108">For information on working with diagnostic logs using Visual Studio, see [Troubleshooting Azure in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="7ec31-109"><a name="whatisdiag"></a>웹 서버 진단 및 응용 프로그램 진단</span><span class="sxs-lookup"><span data-stu-id="7ec31-109"><a name="whatisdiag"></a>Web server diagnostics and application diagnostics</span></span>
<span data-ttu-id="7ec31-110">앱 서비스 웹앱은 웹 서버와 웹 응용 프로그램 모두의 정보를 로깅할 수 있도록 진단 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-110">App Service web apps provide diagnostic functionality for logging information from both the web server and the web application.</span></span> <span data-ttu-id="7ec31-111">이는 논리적으로 **웹 서버 진단** 및 **응용 프로그램 진단**으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-111">These are logically separated into **web server diagnostics** and **application diagnostics**.</span></span>

### <a name="web-server-diagnostics"></a><span data-ttu-id="7ec31-112">웹 서버 진단</span><span class="sxs-lookup"><span data-stu-id="7ec31-112">Web server diagnostics</span></span>
<span data-ttu-id="7ec31-113">다음과 같은 종류의 로그를 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-113">You can enable or disable the following kinds of logs:</span></span>

* <span data-ttu-id="7ec31-114">**자세한 오류 로깅** - 오류를 나타내는 HTTP 상태 코드(상태 코드 400 이상)의 자세한 오류 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-114">**Detailed Error Logging** - Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span> <span data-ttu-id="7ec31-115">여기에는 서버에서 오류 코드를 반환한 이유를 확인하는 데 도움이 되는 정보가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-115">This may contain information that can help determine why the server returned the error code.</span></span>
* <span data-ttu-id="7ec31-116">**실패한 요청 추적** - 요청을 처리하는 데 사용된 IIS 구성 요소 추적 및 각 구성 요소에 소요된 시간을 포함하여 실패한 요청에 대해 자세한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-116">**Failed Request Tracing** - Detailed information on failed requests, including a trace of the IIS components used to process the request and the time taken in each component.</span></span> <span data-ttu-id="7ec31-117">이는 사이트 성능을 개선하거나 반환된 특정 HTTP 오류를 유발한 항목을 격리하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-117">This can be useful if you are attempting to increase site performance or isolate what is causing a specific HTTP error to be returned.</span></span>
* <span data-ttu-id="7ec31-118">**웹 서버 로깅** - [W3C 확장 로그 파일 형식](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)을 사용하는 HTTP 트랜잭션에 대한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-118">**Web Server Logging** - Information about HTTP transactions using the [W3C extended log file format](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span> <span data-ttu-id="7ec31-119">이는 처리된 요청 수, 특정 IP 주소에서 들어온 요청 수 등의 전체 사이트 메트릭을 확인하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-119">This is useful when determining overall site metrics such as the number of requests handled or how many requests are from a specific IP address.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="7ec31-120">응용 프로그램 진단</span><span class="sxs-lookup"><span data-stu-id="7ec31-120">Application diagnostics</span></span>
<span data-ttu-id="7ec31-121">응용 프로그램 진단을 통해 웹 응용 프로그램에서 생성된 정보를 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-121">Application diagnostics allows you to capture information produced by a web application.</span></span> <span data-ttu-id="7ec31-122">ASP.NET 응용 프로그램은 [System.Diagnostics.Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx) 클래스를 사용하여 응용 프로그램 진단 로그에 정보를 로깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-122">ASP.NET applications can use the [System.Diagnostics.Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx) class to log information to the application diagnostics log.</span></span> <span data-ttu-id="7ec31-123">예:</span><span class="sxs-lookup"><span data-stu-id="7ec31-123">For example:</span></span>

    System.Diagnostics.Trace.TraceError("If you're seeing this, something bad happened");

<span data-ttu-id="7ec31-124">런타임에 문제 해결을 위해 이러한 로그를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-124">At runtime you can retrieve these logs to help with troubleshooting.</span></span> <span data-ttu-id="7ec31-125">자세한 내용은 [Visual Studio에서 Azure 웹앱 문제 해결](web-sites-dotnet-troubleshoot-visual-studio.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ec31-125">For more information, see [Troubleshooting Azure web apps in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

<span data-ttu-id="7ec31-126">웹앱에 콘텐츠를 게시하는 경우 앱 서비스 웹앱은 배포 정보도 로깅합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-126">App Service web apps also log deployment information when you publish content to a web app.</span></span> <span data-ttu-id="7ec31-127">이는 자동으로 수행되며 배포 로깅에 대한 구성 설정은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-127">This happens automatically and there are no configuration settings for deployment logging.</span></span> <span data-ttu-id="7ec31-128">배포 로깅을 사용하면 배포가 실패한 이유를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-128">Deployment logging allows you to determine why a deployment failed.</span></span> <span data-ttu-id="7ec31-129">예를 들어 사용자 지정 배포 스크립트를 사용하는 경우 스크립트가 실패한 이유를 확인하는 데 배포 로깅을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-129">For example, if you are using a custom deployment script, you might use deployment logging to determine why the script is failing.</span></span>

## <span data-ttu-id="7ec31-130"><a name="enablediag"></a>진단을 사용하도록 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="7ec31-130"><a name="enablediag"></a>How to enable diagnostics</span></span>
<span data-ttu-id="7ec31-131">[Azure Portal](https://portal.azure.com)에서 진단을 사용하려면, 웹앱의 블레이드에서 **설정>진단 로그**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-131">To enable diagnostics in the [Azure Portal](https://portal.azure.com), go to the blade for your web app and click **Settings > Diagnostics logs**.</span></span>

<!-- todo:cleanup dogfood addresses in screenshot -->
![로그 부분](./media/web-sites-enable-diagnostic-log/logspart.png)

<span data-ttu-id="7ec31-133">**응용 프로그램 진단**을 사용하도록 설정하는 경우 **수준**도 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-133">When you enable **application diagnostics** you also choose the **Level**.</span></span> <span data-ttu-id="7ec31-134">이 설정을 사용하면 캡처된 정보를 **정보**, **경고** 또는 **오류** 정보로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-134">This setting allows you to filter the information captured to **informational**, **warning** or **error** information.</span></span> <span data-ttu-id="7ec31-135">이를 **세부 정보 표시** 로 설정하면 응용 프로그램에서 생성된 모든 정보가 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-135">Setting this to **verbose** will log all information produced by the application.</span></span>

> [!NOTE]
> <span data-ttu-id="7ec31-136">web.config 파일을 변경하는 것과 달리, 응용 프로그램 진단을 사용하도록 설정하거나 진단 로그 수준을 변경하면 응용 프로그램이 실행되는 앱 도메인이 재순환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-136">Unlike changing the web.config file, enabling Application diagnostics or changing diagnostic log levels does not recycle the app domain that the application runs within.</span></span>
>
>

<span data-ttu-id="7ec31-137">[클래식 포털](https://manage.windowsazure.com) 웹앱 **구성** 탭에서 **웹 서버 로깅**에 대한 **저장소** 또는 **파일 시스템**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-137">In the [classic portal](https://manage.windowsazure.com) Web app **Configure** tab, you can select **storage** or **file system** for **web server logging**.</span></span> <span data-ttu-id="7ec31-138">**저장소** 를 선택하면 저장소 계정을 선택하고 로그를 기록할 Blob 컨테이너를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-138">Selecting **storage** allows you to select a storage account, and then a blob container that the logs will be written to.</span></span> <span data-ttu-id="7ec31-139">**사이트 진단** 에 대한 기타 모든 로그는 파일 시스템에만 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-139">All other logs for **site diagnostics** are written to the file system only.</span></span>

<span data-ttu-id="7ec31-140">[클래식 포털](https://manage.windowsazure.com) 웹앱 구성 탭은 또한 응용 프로그램 진단에 대한 추가 **구성** 이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-140">The [classic portal](https://manage.windowsazure.com) Web app **Configure** tab also has additional settings for application diagnostics:</span></span>

* <span data-ttu-id="7ec31-141">**파일 시스템** - 웹 앱 파일 시스템에 응용 프로그램 진단 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-141">**File system** - stores the application diagnostics information to the web app file system.</span></span> <span data-ttu-id="7ec31-142">이러한 파일은 FTP로 액세스하거나, Azure PowerShell 또는 Azure 명령줄 인터페이스(Azure CLI)를 사용하여 Zip 보관 파일로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-142">These files can be accessed by FTP, or downloaded as a Zip archive by using the Azure PowerShell or Azure Command-Line Interface (Azure CLI).</span></span>
* <span data-ttu-id="7ec31-143">**테이블 저장소** - 지정된 Azure 저장소 계정 및 테이블 이름에 응용 프로그램 진단 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-143">**Table storage** - stores the application diagnostics information in the specified Azure Storage Account and table name.</span></span>
* <span data-ttu-id="7ec31-144">**Blob 저장소** - 지정된 Azure 저장소 계정 및 Blob 컨테이너에 응용 프로그램 진단 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-144">**Blob storage** - stores the application diagnostics information in the specified Azure Storage Account and blob container.</span></span>
* <span data-ttu-id="7ec31-145">**보존 기간** - 기본적으로 로그는 **Blob Storage**에서 자동으로 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-145">**Retention period** - by default, logs are not automatically deleted from **blob storage**.</span></span> <span data-ttu-id="7ec31-146">자동으로 로그를 삭제하려면 **set retention** 을 선택하고 로그를 보관할 기간(일)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-146">Select **set retention** and enter the number of days to keep logs if you wish to automatically delete logs.</span></span>

> [!NOTE]
> <span data-ttu-id="7ec31-147">[저장소 계정의 선택키를 다시 생성](../storage/common/storage-create-storage-account.md)하는 경우 해당 로깅 구성을 다시 설정하여 업데이트한 키를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-147">If you [regenerate your storage account's access keys](../storage/common/storage-create-storage-account.md), you must reset the respective logging configuration to use the updated keys.</span></span> <span data-ttu-id="7ec31-148">다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-148">To do this:</span></span>
>
> 1. <span data-ttu-id="7ec31-149">**구성** 탭에서 해당 로깅 기능을 **끄기**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-149">In the **Configure** tab, set the respective logging feature to **Off**.</span></span> <span data-ttu-id="7ec31-150">설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-150">Save your setting.</span></span>
> 2. <span data-ttu-id="7ec31-151">저장소 계정 Blob 또는 테이블에 로깅을 다시 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-151">Enable logging to the storage account blob or table again.</span></span> <span data-ttu-id="7ec31-152">설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-152">Save your setting.</span></span>
>
>

<span data-ttu-id="7ec31-153">파일 시스템, 테이블 저장소 또는 Blob 저장소를 원하는 방식으로 결합하여 동시에 사용하도록 설정할 수 있으며 로그 수준은 개별적으로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-153">Any combination of file system, table storage, or blob storage can be enabled at the same time, and have individual log level configurations.</span></span> <span data-ttu-id="7ec31-154">예를 들어 장기적인 로깅 솔루션으로 Blob 저장소에 오류 및 경고를 기록하면서 파일 시스템 로깅은 세부 정보 표시 수준으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-154">For example, you may wish to log errors and warnings to blob storage as a long-term logging solution, while enabling file system logging with a level of verbose.</span></span>

<span data-ttu-id="7ec31-155">세 저장소 위치 모두는 로깅된 이벤트에 대해 동일한 기본 정보를 제공하는 반면 **Table Storage** 및 **Blob Storage**는 **파일 시스템**에 기록하는 것보다 인스턴스 ID, 스레드 ID 및 좀 더 세부적인 타임스탬프(눈금 형식) 등 추가 정보를 로깅합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-155">While all three storage locations provide the same basic information for logged events, **table storage** and **blob storage** log additional information such as the instance ID, thread ID, and a more granular timestamp (tick format) than logging to **file system**.</span></span>

> [!NOTE]
> <span data-ttu-id="7ec31-156">**Table Storage** 또는 **Blob Storage**에 저장된 정보는 이러한 저장소 시스템에서 바로 작업할 수 있는 저장소 클라이언트 또는 응용 프로그램을 사용해서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-156">Information stored in **table storage** or **blob  storage** can only be accessed using a storage client or an application that can directly work with these storage systems.</span></span> <span data-ttu-id="7ec31-157">예를 들어 Visual Studio 2013에는 테이블 또는 Blob 저장소를 탐색하는 데 사용할 수 있는 저장소 탐색기를 포함하고 있으며, HDInsight는 Blob 저장소에 저장된 데이터에 액세스하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-157">For example, Visual Studio 2013 contains a Storage Explorer that can be used to explore table or blob storage, and HDInsight can access data stored in blob storage.</span></span> <span data-ttu-id="7ec31-158">또한 [Azure SDK](/downloads/#)중 하나를 사용하여 Azure 저장소에 액세스하는 응용 프로그램을 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-158">You can also write an application that accesses Azure Storage by using one of the [Azure SDKs](/downloads/#).</span></span>
>
> [!NOTE]
> <span data-ttu-id="7ec31-159">Azure PowerShell에서 **Set-AzureWebsite** cmdlet을 사용해서도 진단을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-159">Diagnostics can also be enabled from Azure PowerShell using the **Set-AzureWebsite** cmdlet.</span></span> <span data-ttu-id="7ec31-160">Azure PowerShell을 설치하지 않았거나 Azure 구독을 사용하도록 이를 구성하지 않은 경우 [Azure PowerShell을 사용하는 방법](/develop/nodejs/how-to-guides/powershell-cmdlets/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ec31-160">If you have not installed Azure PowerShell, or have not configured it to use your Azure Subscription, see [How to Use Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).</span></span>
>
>

## <span data-ttu-id="7ec31-161"><a name="download"></a> 방법: 로그 다운로드</span><span class="sxs-lookup"><span data-stu-id="7ec31-161"><a name="download"></a> How to: Download logs</span></span>
<span data-ttu-id="7ec31-162">웹 앱 파일 시스템에 저장된 진단 정보는 FTP를 사용하여 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-162">Diagnostic information stored to the web app file system can be accessed directly using FTP.</span></span> <span data-ttu-id="7ec31-163">또한 Azure PowerShell 또는 Azure 명령줄 인터페이스를 사용하여 Zip 보관 파일로 다운로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-163">It can also be downloaded as a Zip archive using Azure PowerShell or the Azure Command-Line Interface.</span></span>

<span data-ttu-id="7ec31-164">로그가 저장되는 디렉터리 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-164">The directory structure that the logs are stored in is as follows:</span></span>

* <span data-ttu-id="7ec31-165">**응용 프로그램 로그** - /LogFiles/Application/입니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-165">**Application logs** - /LogFiles/Application/.</span></span> <span data-ttu-id="7ec31-166">이 폴더에는 응용 프로그램 로깅으로 생성된 정보가 포함된 하나 이상의 텍스트 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-166">This folder contains one or more text files containing information produced by application logging.</span></span>
* <span data-ttu-id="7ec31-167">**실패한 요청 추적** - /LogFiles/W3SVC#########/입니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-167">**Failed Request Traces** - /LogFiles/W3SVC#########/.</span></span> <span data-ttu-id="7ec31-168">이 폴더에는 하나의 XSL 파일 및 하나 이상의 XML 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-168">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="7ec31-169">XSL 파일은 XML 파일을 Internet Explorer에서 볼 때 XML 파일의 내용에 서식을 지정하고 필터링하는 기능을 제공하므로 XSL 파일은 XML 파일과 동일한 디렉터리에 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-169">Ensure that you download the XSL file into the same directory as the XML file(s) because the XSL file provides functionality for formatting and filtering the contents of the XML file(s) when viewed in Internet Explorer.</span></span>
* <span data-ttu-id="7ec31-170">**Detailed Error Logs** - /LogFiles/DetailedErrors/입니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-170">**Detailed Error Logs** - /LogFiles/DetailedErrors/.</span></span> <span data-ttu-id="7ec31-171">이 폴더에는 발생한 HTTP 오류에 대해 방대한 정보를 제공하는 하나 이상의 .htm 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-171">This folder contains one or more .htm files that provide extensive information for any HTTP errors that have occurred.</span></span>
* <span data-ttu-id="7ec31-172">**웹 서버 로그** - /LogFiles/http/RawLogs입니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-172">**Web Server Logs** - /LogFiles/http/RawLogs.</span></span> <span data-ttu-id="7ec31-173">이 폴더에는 [W3C 확장 로그 파일 형식](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)을 사용하여 서식이 지정된 하나 이상의 텍스트 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-173">This folder contains one or more text files formatted using the [W3C extended log file format](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
* <span data-ttu-id="7ec31-174">**Deployment logs** - /LogFiles/Git입니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-174">**Deployment logs** - /LogFiles/Git.</span></span> <span data-ttu-id="7ec31-175">이 폴더에는 Azure 웹 앱에서 사용된 내부 배포 프로세스에서 생성된 로그와 Git 배포용 로그가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-175">This folder contains logs generated by the internal deployment processes used by Azure web apps, as well as logs for Git deployments.</span></span>

### <a name="ftp"></a><span data-ttu-id="7ec31-176">FTP</span><span class="sxs-lookup"><span data-stu-id="7ec31-176">FTP</span></span>
<span data-ttu-id="7ec31-177">FTP를 사용하여 진단 정보에 액세스하려면, **클래식 포털** 에서 웹앱의 [대시보드](https://manage.windowsazure.com)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-177">To access diagnostic information using FTP, visit the **Dashboard** of your web app in the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="7ec31-178">**간략 상태** 섹션에서 **FTP 진단 로그** 링크를 사용하여 FTP를 통해 로그 파일에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-178">In the **quick glance** section, use the **FTP Diagnostic Logs** link to access the log files using FTP.</span></span> <span data-ttu-id="7ec31-179">**Deployment/FTP User** 항목은 FTP 사이트에 액세스하는 데 사용해야 하는 사용자 이름을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-179">The **Deployment/FTP User** entry lists the user name that should be used to access the FTP site.</span></span>

> [!NOTE]
> <span data-ttu-id="7ec31-180">**배포/FTP 사용자** 항목이 설정되지 않은 경우 또는 이 사용자의 암호를 잊은 경우 **대시보드**의 **간략 상태** 섹션에서 **배포 자격 증명 다시 설정** 링크를 사용하여 새 사용자 및 암호를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-180">If the **Deployment/FTP User** entry is not set, or you have forgotten the password for this user, you can create a new user and password by using the **Reset deployment credentials** link in the **quick glance** section of the **Dashboard**.</span></span>
>
>

### <a name="download-with-azure-powershell"></a><span data-ttu-id="7ec31-181">Azure PowerShell로 다운로드</span><span class="sxs-lookup"><span data-stu-id="7ec31-181">Download with Azure PowerShell</span></span>
<span data-ttu-id="7ec31-182">로그 파일을 다운로드하려면 새 인스턴스의 Azure PowerShell을 시작하고 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-182">To download the log files, start a new instance of Azure PowerShell and use the following command:</span></span>

    Save-AzureWebSiteLog -Name webappname

<span data-ttu-id="7ec31-183">이 명령을 실행하면 **-Name** 매개 변수로 지정된 웹앱이 로그가 현재 디렉터리의 **logs.zip**이라는 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-183">This will save the logs for the web app specified by the **-Name** parameter to a file named **logs.zip** in the current directory.</span></span>

> [!NOTE]
> <span data-ttu-id="7ec31-184">Azure PowerShell을 설치하지 않았거나 Azure 구독을 사용하도록 이를 구성하지 않은 경우 [Azure PowerShell을 사용하는 방법](/develop/nodejs/how-to-guides/powershell-cmdlets/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ec31-184">If you have not installed Azure PowerShell, or have not configured it to use your Azure Subscription, see [How to Use Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).</span></span>
>
>

### <a name="download-with-azure-command-line-interface"></a><span data-ttu-id="7ec31-185">Azure 명령줄 인터페이스로 다운로드</span><span class="sxs-lookup"><span data-stu-id="7ec31-185">Download with Azure Command-Line Interface</span></span>
<span data-ttu-id="7ec31-186">Azure 명령줄 인터페이스를 사용하여 로그 파일을 다운로드하려면 새 명령 프롬프트, PowerShell, Bash 또는 터미널 세션을 열고 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-186">To download the log files using the Azure Command Line Interface, open a new command prompt, PowerShell, Bash, or Terminal session and enter the following command:</span></span>

    azure site log download webappname

<span data-ttu-id="7ec31-187">이 명령을 실행하면 'webappname'이라는 웹 앱의 로그가 현재 디렉터리의 **diagnostics.zip** 이라는 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-187">This will save the logs for the web app named 'webappname' to a file named **diagnostics.zip** in the current directory.</span></span>

> [!NOTE]
> <span data-ttu-id="7ec31-188">Azure CLI(Azure Command-Line Interface)를 설치하지 않았거나 Azure 구독을 사용하도록 Azure CLI를 구성하지 않은 경우 [Azure CLI 사용 방법](../cli-install-nodejs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ec31-188">If you have not installed the Azure Command-Line Interface (Azure CLI), or have not configured it to use your Azure Subscription, see [How to Use Azure CLI](../cli-install-nodejs.md).</span></span>
>
>

## <a name="how-to-view-logs-in-application-insights"></a><span data-ttu-id="7ec31-189">방법: Application Insights에서 로그 보기</span><span class="sxs-lookup"><span data-stu-id="7ec31-189">How to: View logs in Application Insights</span></span>
<span data-ttu-id="7ec31-190">Visual Studio Application Insights는 로그 필터링과 검색을 위한 도구 및 요청과 다른 이벤트와 로그를 연결하기 위한 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-190">Visual Studio Application Insights provides tools for filtering and searching logs, and for correlating the logs with requests and other events.</span></span>

1. <span data-ttu-id="7ec31-191">Visual Studio의 프로젝트에 Application Insights SDK 추가</span><span class="sxs-lookup"><span data-stu-id="7ec31-191">Add the Application Insights SDK to your project in Visual Studio.</span></span>
   * <span data-ttu-id="7ec31-192">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 Application Insights 추가를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-192">In Solution Explorer, right click your project and choose Add Application Insights.</span></span> <span data-ttu-id="7ec31-193">Application Insights 리소스 만들기를 포함 하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-193">You'll be guided through steps that include creating an Application Insights resource.</span></span> [<span data-ttu-id="7ec31-194">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="7ec31-194">Learn more</span></span>](../application-insights/app-insights-asp-net.md)
2. <span data-ttu-id="7ec31-195">추적 수신기 패키지를 프로젝트에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-195">Add the Trace Listener package to your project.</span></span>
   * <span data-ttu-id="7ec31-196">프로젝트를 마우스 오른쪽 단추로 클릭하고 NuGet 패키지 관리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-196">Right click your project and choose Manage NuGet Packages.</span></span> <span data-ttu-id="7ec31-197">자동으로 로그를 삭제하려면 `Microsoft.ApplicationInsights.TraceListener` [자세히 알아보기](../application-insights/app-insights-asp-net-trace-logs.md)</span><span class="sxs-lookup"><span data-stu-id="7ec31-197">Select `Microsoft.ApplicationInsights.TraceListener` [Learn more](../application-insights/app-insights-asp-net-trace-logs.md)</span></span>
3. <span data-ttu-id="7ec31-198">프로젝트를 업로드하고 실행하여 로그 데이터를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-198">Upload your project and run it to generate log data.</span></span>
4. <span data-ttu-id="7ec31-199">[Azure Portal](https://portal.azure.com/)에서 새 Application Insights 리소스를 찾아서 **검색**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-199">In the [Azure Portal](https://portal.azure.com/), browse to your new Application Insights resource, and open **Search**.</span></span> <span data-ttu-id="7ec31-200">요청, 사용법 및 다른 원격 분석와 함께 로그 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-200">You'll see your log data, along with request, usage and other telemetry.</span></span> <span data-ttu-id="7ec31-201">일부 원격 분석에 몇 분 정도 걸릴 수 있습니다. 새로 고침을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-201">Some telemetry might take a few minutes to arrive: click Refresh.</span></span> [<span data-ttu-id="7ec31-202">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="7ec31-202">Learn more</span></span>](../application-insights/app-insights-diagnostic-search.md)

[<span data-ttu-id="7ec31-203">Application Insights로 추적되는 성능에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="7ec31-203">Learn more about performance tracking with Application Insights</span></span>](../application-insights/app-insights-azure-web-apps.md)

## <span data-ttu-id="7ec31-204"><a name="streamlogs"></a> 방법: 스트림 로그</span><span class="sxs-lookup"><span data-stu-id="7ec31-204"><a name="streamlogs"></a> How to: Stream logs</span></span>
<span data-ttu-id="7ec31-205">응용 프로그램을 개발하는 동안 거의 실시간의 로깅 정보를 보는 것이 종종 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-205">While developing an application, it is often useful to see logging information in near-real time.</span></span> <span data-ttu-id="7ec31-206">이는 Azure PowerShell 또는 Azure 명령줄 인터페이스 중 하나를 사용하여 개발 환경에 로깅 정보를 스트리밍하도록 하면 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-206">This can be accomplished by streaming logging information to your development environment using either Azure PowerShell or the Azure Command-Line Interface.</span></span>

> [!NOTE]
> <span data-ttu-id="7ec31-207">일부 유형의 로깅 버퍼는 로그 파일에 기록하고 이로 인해 스크림에서 이벤트가 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-207">Some types of logging buffer write to the log file, which can result in out of order events in the stream.</span></span> <span data-ttu-id="7ec31-208">예를 들어 사용자가 페이지를 방문할 때 발생한 응용 프로그램 로그 항목이 페이지 요청에 대한 해당 HTTP 로그 항목보다 먼저 스트림에 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-208">For example, an application log entry that occurs when a user visits a page may be displayed in the stream before the corresponding HTTP log entry for the page request.</span></span>
>
> [!NOTE]
> <span data-ttu-id="7ec31-209">로그 스트리밍은 **D:\\home\\LogFiles\\** 폴더에 저장된 모든 텍스트 파일에 기록된 정보를 스트리밍할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-209">Log streaming will also stream information written to any text file stored in the **D:\\home\\LogFiles\\** folder.</span></span>
>
>

### <a name="streaming-with-azure-powershell"></a><span data-ttu-id="7ec31-210">Azure PowerShell로 스트리밍</span><span class="sxs-lookup"><span data-stu-id="7ec31-210">Streaming with Azure PowerShell</span></span>
<span data-ttu-id="7ec31-211">로깅 정보를 스트리밍하려면 Azure PowerShell의 새 인스턴스를 시작하고 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-211">To stream logging information, start a new instance of Azure PowerShell and use the following command:</span></span>

    Get-AzureWebSiteLog -Name webappname -Tail

<span data-ttu-id="7ec31-212">이 명령을 실행하면 **-Name** 매개 변수로 지정된 웹 앱에 연결되고 로그 이벤트가 웹 앱에 발생하면 PowerShell 창으로 정보가 스트리밍되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-212">This will connect to the web app specified by the **-Name** parameter and begin streaming information to the PowerShell window as log events occur on the web app.</span></span> <span data-ttu-id="7ec31-213">/LogFiles 디렉터리(d:/home/logfiles)에 저장된 .txt, .log 또는 .htm으로 끝나는 파일에 기록된 정보는 로컬 콘솔로 스트리밍됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-213">Any information written to files ending in .txt, .log, or .htm that are stored in the /LogFiles directory (d:/home/logfiles) will be streamed to the local console.</span></span>

<span data-ttu-id="7ec31-214">오류와 같은 특정 이벤트를 필터링하려면 **-Message** 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-214">To filter specific events, such as errors, use the **-Message** parameter.</span></span> <span data-ttu-id="7ec31-215">예:</span><span class="sxs-lookup"><span data-stu-id="7ec31-215">For example:</span></span>

    Get-AzureWebSiteLog -Name webappname -Tail -Message Error

<span data-ttu-id="7ec31-216">HTTP와 같은 특정 로그 유형을 필터링하려면 **-Path** 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-216">To filter specific log types, such as HTTP, use the **-Path** parameter.</span></span> <span data-ttu-id="7ec31-217">예:</span><span class="sxs-lookup"><span data-stu-id="7ec31-217">For example:</span></span>

    Get-AzureWebSiteLog -Name webappname -Tail -Path http

<span data-ttu-id="7ec31-218">사용 가능한 경로 목록을 보려면 -ListPath 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-218">To see a list of available paths, use the -ListPath parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="7ec31-219">Azure PowerShell을 설치하지 않았거나 Azure 구독을 사용하도록 이를 구성하지 않은 경우 [Azure PowerShell을 사용하는 방법](/develop/nodejs/how-to-guides/powershell-cmdlets/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ec31-219">If you have not installed Azure PowerShell, or have not configured it to use your Azure Subscription, see [How to Use Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).</span></span>
>
>

### <a name="streaming-with-azure-command-line-interface"></a><span data-ttu-id="7ec31-220">Azure 명령줄 인터페이스로 스트리밍</span><span class="sxs-lookup"><span data-stu-id="7ec31-220">Streaming with Azure Command-Line Interface</span></span>
<span data-ttu-id="7ec31-221">로깅 정보를 스트리밍하려면 새 명령 프롬프트, PowerShell, Bash 또는 터미널 세션을 열고 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-221">To stream logging information, open a new command prompt, PowerShell, Bash, or Terminal session and enter the following command:</span></span>

    azure site log tail webappname

<span data-ttu-id="7ec31-222">이 명령을 실행하면 'webappname'이라는 웹 앱에 연결되고 로그 이벤트가 웹 앱에서 발생하면 창으로 정보가 스트리밍되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-222">This will connect to the web app named 'webappname' and begin streaming information to the window as log events occur on the web app.</span></span> <span data-ttu-id="7ec31-223">/LogFiles 디렉터리(d:/home/logfiles)에 저장된 .txt, .log 또는 .htm으로 끝나는 파일에 기록된 정보는 로컬 콘솔로 스트리밍됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-223">Any information written to files ending in .txt, .log, or .htm that are stored in the /LogFiles directory (d:/home/logfiles) will be streamed to the local console.</span></span>

<span data-ttu-id="7ec31-224">오류와 같은 특정 이벤트를 필터링하려면 **--Filter** 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-224">To filter specific events, such as errors, use the **--Filter** parameter.</span></span> <span data-ttu-id="7ec31-225">예:</span><span class="sxs-lookup"><span data-stu-id="7ec31-225">For example:</span></span>

    azure site log tail webappname --filter Error

<span data-ttu-id="7ec31-226">HTTP와 같은 특정 로그 유형을 필터링하려면 **-Path** 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-226">To filter specific log types, such as HTTP, use the **--Path** parameter.</span></span> <span data-ttu-id="7ec31-227">예:</span><span class="sxs-lookup"><span data-stu-id="7ec31-227">For example:</span></span>

    azure site log tail webappname --path http

> [!NOTE]
> <span data-ttu-id="7ec31-228">Azure Command-Line Interface를 설치하지 않았거나 Azure 구독을 사용하도록 Azure CLI를 구성하지 않은 경우 [Azure Command-Line Interface 사용 방법](../cli-install-nodejs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ec31-228">If you have not installed the Azure Command-Line Interface, or have not configured it to use your Azure Subscription, see [How to Use Azure Command-Line Interface](../cli-install-nodejs.md).</span></span>
>
>

## <span data-ttu-id="7ec31-229"><a name="understandlogs"></a> 방법: 진단 로그 이해</span><span class="sxs-lookup"><span data-stu-id="7ec31-229"><a name="understandlogs"></a> How to: Understand diagnostics logs</span></span>
### <a name="application-diagnostics-logs"></a><span data-ttu-id="7ec31-230">응용 프로그램 진단 로그</span><span class="sxs-lookup"><span data-stu-id="7ec31-230">Application diagnostics logs</span></span>
<span data-ttu-id="7ec31-231">응용 프로그램 진단은 로그가 파일 시스템, 테이블 저장소 또는 Blob 저장소 중 어디에 저장되는지에 따라 .NET 응용 프로그램 관련 형식으로 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-231">Application diagnostics stores information in a specific format for .NET applications, depending on whether you store logs to the file system, table storage, or blob storage.</span></span> <span data-ttu-id="7ec31-232">이벤트가 발생한 날짜 및 시간, 이벤트가 생성된 프로세스 ID, 이벤트 유형(정보, 경고, 오류), 이벤트 메시지 등 저장된 데이터의 기본 집합은 모든 세 저장소 유형 전체에서 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-232">The base set of data stored is the same across all three storage types - the date and time the event occurred, the process ID that produced the event, the event type (information, warning, error,) and the event message.</span></span>

<span data-ttu-id="7ec31-233">**파일 시스템**</span><span class="sxs-lookup"><span data-stu-id="7ec31-233">**File system**</span></span>

<span data-ttu-id="7ec31-234">파일 시스템에 로깅되거나 스트리밍을 통해 수신된 각 줄은 다음 형식과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-234">Each line logged to the file system or received using streaming will be in the following format:</span></span>

    {Date}  PID[{process id}] {event type/level} {message}

<span data-ttu-id="7ec31-235">예를 들어 오류 이벤트는 다음과 비슷하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-235">For example, an error event would appear similar to the following:</span></span>

    2014-01-30T16:36:59  PID[3096] Error       Fatal error on the page!

<span data-ttu-id="7ec31-236">파일 시스템에 로깅하면 사용 가능한 세 가지 방법의 가장 기본적인 정보, 즉 시간, 프로세스 ID, 이벤트 수준 및 메시지만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-236">Logging to the file system provides the most basic information of the three available methods, providing only the time, process id, event level, and message.</span></span>

<span data-ttu-id="7ec31-237">**Table Storage**</span><span class="sxs-lookup"><span data-stu-id="7ec31-237">**Table storage**</span></span>

<span data-ttu-id="7ec31-238">테이블 저장소에 로깅하면 추가 속성을 사용하여 테이블에 저장된 데이터와 이벤트에 대한 좀 더 세부적인 정보를 쉽게 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-238">When logging to table storage, additional properties are used to facilitate searching the data stored in the table as well as more granular information on the event.</span></span> <span data-ttu-id="7ec31-239">다음 속성(열)이 테이블에 저장된 각 엔터티(행)에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-239">The following properties (columns) are used for each entity (row) stored in the table.</span></span>

| <span data-ttu-id="7ec31-240">속성 이름</span><span class="sxs-lookup"><span data-stu-id="7ec31-240">Property name</span></span> | <span data-ttu-id="7ec31-241">값/형식</span><span class="sxs-lookup"><span data-stu-id="7ec31-241">Value/format</span></span> |
| --- | --- |
| <span data-ttu-id="7ec31-242">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="7ec31-242">PartitionKey</span></span> |<span data-ttu-id="7ec31-243">yyyyMMddHH 형식의 이벤트 날짜/시간</span><span class="sxs-lookup"><span data-stu-id="7ec31-243">Date/time of the event in yyyyMMddHH format</span></span> |
| <span data-ttu-id="7ec31-244">RowKey</span><span class="sxs-lookup"><span data-stu-id="7ec31-244">RowKey</span></span> |<span data-ttu-id="7ec31-245">이 엔터티를 고유하게 식별하는 GUID 값</span><span class="sxs-lookup"><span data-stu-id="7ec31-245">A GUID value that uniquely identifies this entity</span></span> |
| <span data-ttu-id="7ec31-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="7ec31-246">Timestamp</span></span> |<span data-ttu-id="7ec31-247">이벤트가 발생한 날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="7ec31-247">The date and time that the event occurred</span></span> |
| <span data-ttu-id="7ec31-248">EventTickCount</span><span class="sxs-lookup"><span data-stu-id="7ec31-248">EventTickCount</span></span> |<span data-ttu-id="7ec31-249">이벤트가 발생한 날짜 및 시간(눈금 형식, 더 높은 정밀도)</span><span class="sxs-lookup"><span data-stu-id="7ec31-249">The date and time that the event occurred, in Tick format (greater precision)</span></span> |
| <span data-ttu-id="7ec31-250">ApplicationName</span><span class="sxs-lookup"><span data-stu-id="7ec31-250">ApplicationName</span></span> |<span data-ttu-id="7ec31-251">웹 앱 이름</span><span class="sxs-lookup"><span data-stu-id="7ec31-251">The web app name</span></span> |
| <span data-ttu-id="7ec31-252">수준</span><span class="sxs-lookup"><span data-stu-id="7ec31-252">Level</span></span> |<span data-ttu-id="7ec31-253">이벤트 수준(예: 오류, 경고, 정보)</span><span class="sxs-lookup"><span data-stu-id="7ec31-253">Event level (e.g. error, warning, information)</span></span> |
| <span data-ttu-id="7ec31-254">EventId</span><span class="sxs-lookup"><span data-stu-id="7ec31-254">EventId</span></span> |<span data-ttu-id="7ec31-255">이 이벤트의 이벤트 ID</span><span class="sxs-lookup"><span data-stu-id="7ec31-255">The event ID of this event</span></span><p><p><span data-ttu-id="7ec31-256">지정하지 않을 경우 0으로 기본 설정됨</span><span class="sxs-lookup"><span data-stu-id="7ec31-256">Defaults to 0 if none specified</span></span> |
| <span data-ttu-id="7ec31-257">InstanceId</span><span class="sxs-lookup"><span data-stu-id="7ec31-257">InstanceId</span></span> |<span data-ttu-id="7ec31-258">이벤트가 발생한 웹앱의 인스턴스</span><span class="sxs-lookup"><span data-stu-id="7ec31-258">Instance of the web app that the even occurred on</span></span> |
| <span data-ttu-id="7ec31-259">Pid</span><span class="sxs-lookup"><span data-stu-id="7ec31-259">Pid</span></span> |<span data-ttu-id="7ec31-260">프로세스 ID</span><span class="sxs-lookup"><span data-stu-id="7ec31-260">Process ID</span></span> |
| <span data-ttu-id="7ec31-261">Tid</span><span class="sxs-lookup"><span data-stu-id="7ec31-261">Tid</span></span> |<span data-ttu-id="7ec31-262">이벤트가 생성된 스레드의 스레드 ID</span><span class="sxs-lookup"><span data-stu-id="7ec31-262">The thread ID of the thread that produced the event</span></span> |
| <span data-ttu-id="7ec31-263">Message</span><span class="sxs-lookup"><span data-stu-id="7ec31-263">Message</span></span> |<span data-ttu-id="7ec31-264">이벤트 세부 정보 메시지</span><span class="sxs-lookup"><span data-stu-id="7ec31-264">Event detail message</span></span> |

<span data-ttu-id="7ec31-265">**Blob 저장소**</span><span class="sxs-lookup"><span data-stu-id="7ec31-265">**Blob storage**</span></span>

<span data-ttu-id="7ec31-266">Blob 저장소에 로깅하는 경우 데이터는 쉼표로 구분된 값(CSV) 형식으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-266">When logging to blob storage, data is stored in comma-separated values (CSV) format.</span></span> <span data-ttu-id="7ec31-267">테이블 저장소와 마찬가지로 이벤트에 대해 좀 더 세부적인 정보를 제공하기 위해 추가 필드가 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-267">Similar to table storage, additional fields are logged to provide more granular information about the event.</span></span> <span data-ttu-id="7ec31-268">CSV에서 다음 속성이 각 행에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-268">The following properties are used for each row in the CSV:</span></span>

| <span data-ttu-id="7ec31-269">속성 이름</span><span class="sxs-lookup"><span data-stu-id="7ec31-269">Property name</span></span> | <span data-ttu-id="7ec31-270">값/형식</span><span class="sxs-lookup"><span data-stu-id="7ec31-270">Value/format</span></span> |
| --- | --- |
| <span data-ttu-id="7ec31-271">Date</span><span class="sxs-lookup"><span data-stu-id="7ec31-271">Date</span></span> |<span data-ttu-id="7ec31-272">이벤트가 발생한 날짜 및 시간</span><span class="sxs-lookup"><span data-stu-id="7ec31-272">The date and time that the event occurred</span></span> |
| <span data-ttu-id="7ec31-273">수준</span><span class="sxs-lookup"><span data-stu-id="7ec31-273">Level</span></span> |<span data-ttu-id="7ec31-274">이벤트 수준(예: 오류, 경고, 정보)</span><span class="sxs-lookup"><span data-stu-id="7ec31-274">Event level (e.g. error, warning, information)</span></span> |
| <span data-ttu-id="7ec31-275">ApplicationName</span><span class="sxs-lookup"><span data-stu-id="7ec31-275">ApplicationName</span></span> |<span data-ttu-id="7ec31-276">웹 앱 이름</span><span class="sxs-lookup"><span data-stu-id="7ec31-276">The web app name</span></span> |
| <span data-ttu-id="7ec31-277">InstanceId</span><span class="sxs-lookup"><span data-stu-id="7ec31-277">InstanceId</span></span> |<span data-ttu-id="7ec31-278">이벤트가 발생한 웹앱의 인스턴스</span><span class="sxs-lookup"><span data-stu-id="7ec31-278">Instance of the web app that the event occurred on</span></span> |
| <span data-ttu-id="7ec31-279">EventTickCount</span><span class="sxs-lookup"><span data-stu-id="7ec31-279">EventTickCount</span></span> |<span data-ttu-id="7ec31-280">이벤트가 발생한 날짜 및 시간(눈금 형식, 더 높은 정밀도)</span><span class="sxs-lookup"><span data-stu-id="7ec31-280">The date and time that the event occurred, in Tick format (greater precision)</span></span> |
| <span data-ttu-id="7ec31-281">EventId</span><span class="sxs-lookup"><span data-stu-id="7ec31-281">EventId</span></span> |<span data-ttu-id="7ec31-282">이 이벤트의 이벤트 ID</span><span class="sxs-lookup"><span data-stu-id="7ec31-282">The event ID of this event</span></span><p><p><span data-ttu-id="7ec31-283">지정하지 않을 경우 0으로 기본 설정됨</span><span class="sxs-lookup"><span data-stu-id="7ec31-283">Defaults to 0 if none specified</span></span> |
| <span data-ttu-id="7ec31-284">Pid</span><span class="sxs-lookup"><span data-stu-id="7ec31-284">Pid</span></span> |<span data-ttu-id="7ec31-285">프로세스 ID</span><span class="sxs-lookup"><span data-stu-id="7ec31-285">Process ID</span></span> |
| <span data-ttu-id="7ec31-286">Tid</span><span class="sxs-lookup"><span data-stu-id="7ec31-286">Tid</span></span> |<span data-ttu-id="7ec31-287">이벤트가 생성된 스레드의 스레드 ID</span><span class="sxs-lookup"><span data-stu-id="7ec31-287">The thread ID of the thread that produced the event</span></span> |
| <span data-ttu-id="7ec31-288">Message</span><span class="sxs-lookup"><span data-stu-id="7ec31-288">Message</span></span> |<span data-ttu-id="7ec31-289">이벤트 세부 정보 메시지</span><span class="sxs-lookup"><span data-stu-id="7ec31-289">Event detail message</span></span> |

<span data-ttu-id="7ec31-290">Blob에 저장된 데이터는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-290">The data stored in a blob would look similar to the following:</span></span>

    date,level,applicationName,instanceId,eventTickCount,eventId,pid,tid,message
    2014-01-30T16:36:52,Error,mywebapp,6ee38a,635266966128818593,0,3096,9,An error occurred

> [!NOTE]
> <span data-ttu-id="7ec31-291">로그의 첫 번째 줄에는 이 예에 나타난 대로 열 헤더가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-291">The first line of the log will contain the column headers as represented in this example.</span></span>
>
>

### <a name="failed-request-traces"></a><span data-ttu-id="7ec31-292">실패한 요청 추적</span><span class="sxs-lookup"><span data-stu-id="7ec31-292">Failed request traces</span></span>
<span data-ttu-id="7ec31-293">실패한 요청 추적은 **fr######.xml**이라는 XML 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-293">Failed request traces are stored in XML files named **fr######.xml**.</span></span> <span data-ttu-id="7ec31-294">로깅된 정보를 더 쉽게 볼 수 있도록 **freb.xsl**이라는 XSL 스타일시트가 XML 파일과 동일한 디렉터리에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-294">To make it easier to view the logged information, an XSL stylesheet named **freb.xsl** is provided in the same directory as the XML files.</span></span> <span data-ttu-id="7ec31-295">Internet Explorer에서 XML 파일 중 하나를 열면 XSL 스타일시트를 사용하여 추적 정보에 서식이 지정되어 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-295">Opening one of the XML files in Internet Explorer will use the XSL stylesheet to provide a formatted display of the trace information.</span></span> <span data-ttu-id="7ec31-296">이는 다음과 비슷하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-296">This will appear similar to the following:</span></span>

![브라우저에 표시된 실패한 요청](./media/web-sites-enable-diagnostic-log/tws-failedrequestinbrowser.png)

### <a name="detailed-error-logs"></a><span data-ttu-id="7ec31-298">Detailed Error Logs</span><span class="sxs-lookup"><span data-stu-id="7ec31-298">Detailed error logs</span></span>
<span data-ttu-id="7ec31-299">자세한 오류 로그는 발생한 HTTP 오류에 대해 좀 더 자세한 정보를 제공하는 HTML 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-299">Detailed error logs are HTML documents that provide more detailed information on HTTP errors that have occurred.</span></span> <span data-ttu-id="7ec31-300">이들은 단순한 HTML 문서이므로 웹 브라우저를 사용하여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-300">Since they are simply HTML documents, they can be viewed using a web browser.</span></span>

### <a name="web-server-logs"></a><span data-ttu-id="7ec31-301">웹 서버 로그</span><span class="sxs-lookup"><span data-stu-id="7ec31-301">Web server logs</span></span>
<span data-ttu-id="7ec31-302">웹 서버 로그는 [W3C 확장 로그 파일 형식](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)을 사용하여 서식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-302">The web server logs are formatted using the [W3C extended log file format](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span> <span data-ttu-id="7ec31-303">이 정보는 텍스트 편집기를 사용하여 읽거나 [Log Parser](http://go.microsoft.com/fwlink/?LinkId=246619)와 같은 유틸리티를 사용하여 구문 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-303">This information can be read using a text editor or parsed using utilities such as [Log Parser](http://go.microsoft.com/fwlink/?LinkId=246619).</span></span>

> [!NOTE]
> <span data-ttu-id="7ec31-304">Azure Web Apps에서 생성된 로그는 **s-computername**, **s-ip** 또는 **cs-version** 필드를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-304">The logs produced by Azure web apps do not support the **s-computername**, **s-ip**, or **cs-version** fields.</span></span>
>
>

## <span data-ttu-id="7ec31-305"><a name="nextsteps"></a> 다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ec31-305"><a name="nextsteps"></a> Next steps</span></span>
* [<span data-ttu-id="7ec31-306">웹앱을 모니터링하는 방법</span><span class="sxs-lookup"><span data-stu-id="7ec31-306">How to Monitor Web Apps</span></span>](http://docs.microsoft.com/en-us/azure/app-service-web/web-sites-monitor)
* [<span data-ttu-id="7ec31-307">Visual Studio에서 Azure 웹앱 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7ec31-307">Troubleshooting Azure web apps in Visual Studio</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)
* [<span data-ttu-id="7ec31-308">HDInsight에서 웹앱 로그 분석</span><span class="sxs-lookup"><span data-stu-id="7ec31-308">Analyze web app Logs in HDInsight</span></span>](http://gallery.technet.microsoft.com/scriptcenter/Analyses-Windows-Azure-web-0b27d413)

> [!NOTE]
> <span data-ttu-id="7ec31-309">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-309">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7ec31-310">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ec31-310">No credit cards required; no commitments.</span></span>
>
>

## <a name="whats-changed"></a><span data-ttu-id="7ec31-311">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="7ec31-311">What's changed</span></span>
* <span data-ttu-id="7ec31-312">웹 사이트에서 앱 서비스로의 변경에 대한 지침은 [Azure 앱 서비스와 이 서비스가 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="7ec31-312">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
* <span data-ttu-id="7ec31-313">이전 포털에서 새 포털로의 변경에 대한 지침은 [Azure 포털 탐색에 대한 참조](http://go.microsoft.com/fwlink/?LinkId=529715)</span><span class="sxs-lookup"><span data-stu-id="7ec31-313">For a guide to the change of the old portal to the new portal see: [Reference for navigating the Azure portal](http://go.microsoft.com/fwlink/?LinkId=529715)</span></span>
