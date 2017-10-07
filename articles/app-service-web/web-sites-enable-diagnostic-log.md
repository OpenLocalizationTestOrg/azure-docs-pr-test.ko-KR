---
title: "Azure 앱 서비스에서 웹 앱에 대 한 진단 로깅을 aaaEnable"
description: "자세한 방법을 tooenable 진단 로깅 tooaccess hello Azure에 의해 기록 된 정보는 방법에 계측 tooyour 응용 프로그램을 추가 합니다."
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
ms.openlocfilehash: 4b2903ff31cc93180552cf51196c33505ffbaf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-logging-for-web-apps-in-azure-app-service"></a><span data-ttu-id="ed3fc-103">Azure 앱 서비스에서 웹앱에 대한 진단 로깅 설정</span><span class="sxs-lookup"><span data-stu-id="ed3fc-103">Enable diagnostics logging for web apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="ed3fc-104">개요</span><span class="sxs-lookup"><span data-stu-id="ed3fc-104">Overview</span></span>
<span data-ttu-id="ed3fc-105">Azure에서 기본 제공 진단 tooassist 디버깅이 설정 된 상태로 제공는 [앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-105">Azure provides built-in diagnostics tooassist with debugging an [App Service web app](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="ed3fc-106">이 문서에서는 알아봅니다 어떻게 tooenable 진단 로깅 tooaccess hello Azure에 의해 기록 된 정보는 방법에 계측 tooyour 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-106">In this article you'll learn how tooenable diagnostic logging and add instrumentation tooyour application, as well as how tooaccess hello information logged by Azure.</span></span>

<span data-ttu-id="ed3fc-107">이 문서에서는 hello [Azure 포털](https://portal.azure.com), Azure PowerShell 및 진단 로그와 hello Azure CLI (명령줄 인터페이스 Azure) toowork 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-107">This article uses hello [Azure Portal](https://portal.azure.com), Azure PowerShell, and hello Azure Command-Line Interface (Azure CLI) toowork with diagnostic logs.</span></span> <span data-ttu-id="ed3fc-108">Visual Studio를 사용하여 진단 로그로 작업하는 방법에 대한 자세한 내용은 [Visual Studio에서 Azure 문제 해결](web-sites-dotnet-troubleshoot-visual-studio.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-108">For information on working with diagnostic logs using Visual Studio, see [Troubleshooting Azure in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="ed3fc-109"><a name="whatisdiag"></a>웹 서버 진단 및 응용 프로그램 진단</span><span class="sxs-lookup"><span data-stu-id="ed3fc-109"><a name="whatisdiag"></a>Web server diagnostics and application diagnostics</span></span>
<span data-ttu-id="ed3fc-110">앱 서비스 웹 앱 hello 웹 서버와 hello 웹 응용 프로그램에서 로깅 정보에 대 한 진단 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-110">App Service web apps provide diagnostic functionality for logging information from both hello web server and hello web application.</span></span> <span data-ttu-id="ed3fc-111">이는 논리적으로 **웹 서버 진단** 및 **응용 프로그램 진단**으로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-111">These are logically separated into **web server diagnostics** and **application diagnostics**.</span></span>

### <a name="web-server-diagnostics"></a><span data-ttu-id="ed3fc-112">웹 서버 진단</span><span class="sxs-lookup"><span data-stu-id="ed3fc-112">Web server diagnostics</span></span>
<span data-ttu-id="ed3fc-113">다음 종류의 로그 hello를 사용 하지 않도록 설정 하거나 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-113">You can enable or disable hello following kinds of logs:</span></span>

* <span data-ttu-id="ed3fc-114">**자세한 오류 로깅** - 오류를 나타내는 HTTP 상태 코드(상태 코드 400 이상)의 자세한 오류 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-114">**Detailed Error Logging** - Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span> <span data-ttu-id="ed3fc-115">이 hello 서버 hello 오류 코드를 반환 하는 이유를 확인 하는 데 유용한 정보를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-115">This may contain information that can help determine why hello server returned hello error code.</span></span>
* <span data-ttu-id="ed3fc-116">**요청을 추적 하지 못했습니다.** -hello IIS 구성 요소 사용 tooprocess hello 요청 및 각 구성 요소에서 수행 되는 hello 시간 추적을 포함 하 여 실패 한 요청을 대 한 상세 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-116">**Failed Request Tracing** - Detailed information on failed requests, including a trace of hello IIS components used tooprocess hello request and hello time taken in each component.</span></span> <span data-ttu-id="ed3fc-117">반환 된 HTTP 오류 toobe를 특정 원인을 격리 tooincrease 사이트 성능을 하려고 하는 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-117">This can be useful if you are attempting tooincrease site performance or isolate what is causing a specific HTTP error toobe returned.</span></span>
* <span data-ttu-id="ed3fc-118">**웹 서버 로깅** -hello를 사용 하 여 HTTP 트랜잭션에 대 한 정보 [W3C 확장된 로그 파일 형식](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-118">**Web Server Logging** - Information about HTTP transactions using hello [W3C extended log file format](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span> <span data-ttu-id="ed3fc-119">특정 IP 주소에서 처리 하는 요청의 hello 번호와 같은 전반적인 사이트 메트릭 또는 요청 수를 결정할 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-119">This is useful when determining overall site metrics such as hello number of requests handled or how many requests are from a specific IP address.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="ed3fc-120">응용 프로그램 진단</span><span class="sxs-lookup"><span data-stu-id="ed3fc-120">Application diagnostics</span></span>
<span data-ttu-id="ed3fc-121">응용 프로그램 진단 toocapture 정보를 웹 응용 프로그램에서 만든 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-121">Application diagnostics allows you toocapture information produced by a web application.</span></span> <span data-ttu-id="ed3fc-122">ASP.NET 응용 프로그램에서는 hello [System.Diagnostics.Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx) 클래스 toolog 정보 toohello 응용 프로그램 진단 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-122">ASP.NET applications can use hello [System.Diagnostics.Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx) class toolog information toohello application diagnostics log.</span></span> <span data-ttu-id="ed3fc-123">예:</span><span class="sxs-lookup"><span data-stu-id="ed3fc-123">For example:</span></span>

    System.Diagnostics.Trace.TraceError("If you're seeing this, something bad happened");

<span data-ttu-id="ed3fc-124">런타임 시 이러한 로그 toohelp 문제 해결을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-124">At runtime you can retrieve these logs toohelp with troubleshooting.</span></span> <span data-ttu-id="ed3fc-125">자세한 내용은 [Visual Studio에서 Azure 웹앱 문제 해결](web-sites-dotnet-troubleshoot-visual-studio.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-125">For more information, see [Troubleshooting Azure web apps in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

<span data-ttu-id="ed3fc-126">앱 서비스 웹 앱도 tooa 콘텐츠 웹 응용 프로그램을 게시할 때 배포 정보를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-126">App Service web apps also log deployment information when you publish content tooa web app.</span></span> <span data-ttu-id="ed3fc-127">이는 자동으로 수행되며 배포 로깅에 대한 구성 설정은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-127">This happens automatically and there are no configuration settings for deployment logging.</span></span> <span data-ttu-id="ed3fc-128">배포 로깅을 통해 배포에 실패 한 이유 toodetermine 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-128">Deployment logging allows you toodetermine why a deployment failed.</span></span> <span data-ttu-id="ed3fc-129">예를 들어 사용자 지정 배포 스크립트를 사용 하는 경우 배포 로깅 toodetermine hello 스크립트가 실패 이유를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-129">For example, if you are using a custom deployment script, you might use deployment logging toodetermine why hello script is failing.</span></span>

## <span data-ttu-id="ed3fc-130"><a name="enablediag"></a>어떻게 tooenable 진단</span><span class="sxs-lookup"><span data-stu-id="ed3fc-130"><a name="enablediag"></a>How tooenable diagnostics</span></span>
<span data-ttu-id="ed3fc-131">hello에서 tooenable 진단 [Azure 포털](https://portal.azure.com)웹 앱에 대 한 toohello 블레이드로 이동 하 고 클릭 **설정 > 진단 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-131">tooenable diagnostics in hello [Azure Portal](https://portal.azure.com), go toohello blade for your web app and click **Settings > Diagnostics logs**.</span></span>

<!-- todo:cleanup dogfood addresses in screenshot -->
![로그 부분](./media/web-sites-enable-diagnostic-log/logspart.png)

<span data-ttu-id="ed3fc-133">사용 하면 **응용 프로그램 진단** hello 선택할 수도 **수준**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-133">When you enable **application diagnostics** you also choose hello **Level**.</span></span> <span data-ttu-id="ed3fc-134">이 설정을 통해 toofilter hello 정보를 너무 캡처**정보**, **경고** 또는 **오류** 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-134">This setting allows you toofilter hello information captured too**informational**, **warning** or **error** information.</span></span> <span data-ttu-id="ed3fc-135">이 너무 설정**verbose** hello 응용 프로그램에서 생성 된 모든 정보를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-135">Setting this too**verbose** will log all information produced by hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="ed3fc-136">Hello web.config를 변경 하는 달리 파일을 응용 프로그램 진단을 사용 하도록 설정 하거나 진단 로그 수준을 변경 hello 응용 프로그램 내에서 실행 되는 hello 응용 프로그램 도메인을 재활용 하지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-136">Unlike changing hello web.config file, enabling Application diagnostics or changing diagnostic log levels does not recycle hello app domain that hello application runs within.</span></span>
>
>

<span data-ttu-id="ed3fc-137">Hello에 [클래식 포털](https://manage.windowsazure.com) 웹 앱 **구성** 탭을 선택할 수 있습니다 **저장소** 또는 **파일 시스템** 에 대 한 **웹 서버 로깅**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-137">In hello [classic portal](https://manage.windowsazure.com) Web app **Configure** tab, you can select **storage** or **file system** for **web server logging**.</span></span> <span data-ttu-id="ed3fc-138">선택 하면 **저장소** tooselect 저장소 계정 및 hello 로그에 쓸 blob 컨테이너에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-138">Selecting **storage** allows you tooselect a storage account, and then a blob container that hello logs will be written to.</span></span> <span data-ttu-id="ed3fc-139">에 대 한 다른 모든 로그 **사이트 진단** toohello 파일 시스템에만 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-139">All other logs for **site diagnostics** are written toohello file system only.</span></span>

<span data-ttu-id="ed3fc-140">hello [클래식 포털](https://manage.windowsazure.com) 웹 앱 **구성** 는 응용 프로그램 진단 위한 추가 설정도 탭:</span><span class="sxs-lookup"><span data-stu-id="ed3fc-140">hello [classic portal](https://manage.windowsazure.com) Web app **Configure** tab also has additional settings for application diagnostics:</span></span>

* <span data-ttu-id="ed3fc-141">**파일 시스템** -저장소 hello 응용 프로그램 진단 정보 toohello 웹 응용 프로그램 파일 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-141">**File system** - stores hello application diagnostics information toohello web app file system.</span></span> <span data-ttu-id="ed3fc-142">이러한 파일을 액세스 하 여 FTP 또는 hello Azure PowerShell 또는 Azure 명령줄 인터페이스 (Azure CLI)를 사용 하 여를 Zip 보관 파일로 다운로드 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-142">These files can be accessed by FTP, or downloaded as a Zip archive by using hello Azure PowerShell or Azure Command-Line Interface (Azure CLI).</span></span>
* <span data-ttu-id="ed3fc-143">**테이블 저장소** -저장소 hello hello 지정 된 Azure 저장소 계정 및 테이블 이름에 응용 프로그램 진단 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-143">**Table storage** - stores hello application diagnostics information in hello specified Azure Storage Account and table name.</span></span>
* <span data-ttu-id="ed3fc-144">**Blob 저장소** -저장소 hello hello 지정 된 Azure 저장소 계정과 blob 컨테이너에 응용 프로그램 진단 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-144">**Blob storage** - stores hello application diagnostics information in hello specified Azure Storage Account and blob container.</span></span>
* <span data-ttu-id="ed3fc-145">**보존 기간** - 기본적으로 로그는 **Blob Storage**에서 자동으로 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-145">**Retention period** - by default, logs are not automatically deleted from **blob storage**.</span></span> <span data-ttu-id="ed3fc-146">선택 **보존 설정** hello tookeep 로그 tooautomatically를 원하는 경우 로그를 삭제 하는 일 수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-146">Select **set retention** and enter hello number of days tookeep logs if you wish tooautomatically delete logs.</span></span>

> [!NOTE]
> <span data-ttu-id="ed3fc-147">경우 있습니다 [저장소 계정의 액세스 키 다시 생성](../storage/common/storage-create-storage-account.md), hello 각 로깅 구성 toouse 업데이트 hello 키를 다시 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-147">If you [regenerate your storage account's access keys](../storage/common/storage-create-storage-account.md), you must reset hello respective logging configuration toouse hello updated keys.</span></span> <span data-ttu-id="ed3fc-148">toodo이:</span><span class="sxs-lookup"><span data-stu-id="ed3fc-148">toodo this:</span></span>
>
> 1. <span data-ttu-id="ed3fc-149">Hello에 **구성** 탭 너무 hello 각 로깅 기능을 설정 합니다**오프**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-149">In hello **Configure** tab, set hello respective logging feature too**Off**.</span></span> <span data-ttu-id="ed3fc-150">설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-150">Save your setting.</span></span>
> 2. <span data-ttu-id="ed3fc-151">로깅 toohello 저장소 계정 blob 또는 테이블을 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-151">Enable logging toohello storage account blob or table again.</span></span> <span data-ttu-id="ed3fc-152">설정을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-152">Save your setting.</span></span>
>
>

<span data-ttu-id="ed3fc-153">파일 시스템, 테이블 저장소 또는 blob 저장소의 조합이 시간, 동일 하며 개별 로그 수준 구성을 포함 하는 hello에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-153">Any combination of file system, table storage, or blob storage can be enabled at hello same time, and have individual log level configurations.</span></span> <span data-ttu-id="ed3fc-154">예를 들어 수도 있습니다 toolog 오류 및 경고 tooblob 저장소 장기 로깅 솔루션으로 자세한 정보 표시 수준으로 파일 시스템 로깅이 활성화 하는 동안.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-154">For example, you may wish toolog errors and warnings tooblob storage as a long-term logging solution, while enabling file system logging with a level of verbose.</span></span>

<span data-ttu-id="ed3fc-155">Hello를 제공 하는 모든 세 저장소 위치 기록 된 이벤트에 대 한 기본 정보를 동일한 **테이블 저장소** 및 **blob 저장소** hello 인스턴스 ID, 스레드 ID 및 더 같은 추가 정보를 기록 합니다. 너무 로깅 보다 세분화 된 타임 스탬프 (눈금 형식)**파일 시스템**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-155">While all three storage locations provide hello same basic information for logged events, **table storage** and **blob storage** log additional information such as hello instance ID, thread ID, and a more granular timestamp (tick format) than logging too**file system**.</span></span>

> [!NOTE]
> <span data-ttu-id="ed3fc-156">**Table Storage** 또는 **Blob Storage**에 저장된 정보는 이러한 저장소 시스템에서 바로 작업할 수 있는 저장소 클라이언트 또는 응용 프로그램을 사용해서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-156">Information stored in **table storage** or **blob  storage** can only be accessed using a storage client or an application that can directly work with these storage systems.</span></span> <span data-ttu-id="ed3fc-157">예를 들어 Visual Studio 2013 사용된 tooexplore 테이블 또는 blob 저장소 일 수 있는 저장소 탐색기 있어서 HDInsight blob 저장소에 저장 된 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-157">For example, Visual Studio 2013 contains a Storage Explorer that can be used tooexplore table or blob storage, and HDInsight can access data stored in blob storage.</span></span> <span data-ttu-id="ed3fc-158">Hello 중 하나를 사용 하 여 Azure 저장소에 액세스 하는 응용 프로그램을 작성할 수도 있습니다 [Azure Sdk](/downloads/#)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-158">You can also write an application that accesses Azure Storage by using one of hello [Azure SDKs](/downloads/#).</span></span>
>
> [!NOTE]
> <span data-ttu-id="ed3fc-159">Hello를 사용 하 여 Azure PowerShell에서 진단을 설정할 수도 있습니다 **집합 AzureWebsite** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-159">Diagnostics can also be enabled from Azure PowerShell using hello **Set-AzureWebsite** cmdlet.</span></span> <span data-ttu-id="ed3fc-160">Azure PowerShell을 설치 하지 않은 경우 또는 구성 하지 toouse Azure 구독을 참조 [어떻게 tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-160">If you have not installed Azure PowerShell, or have not configured it toouse your Azure Subscription, see [How tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).</span></span>
>
>

## <span data-ttu-id="ed3fc-161"><a name="download"></a> 방법: 로그 다운로드</span><span class="sxs-lookup"><span data-stu-id="ed3fc-161"><a name="download"></a> How to: Download logs</span></span>
<span data-ttu-id="ed3fc-162">저장 된 진단 정보 toohello 웹 응용 프로그램 파일 시스템은 FTP를 사용 하 여 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-162">Diagnostic information stored toohello web app file system can be accessed directly using FTP.</span></span> <span data-ttu-id="ed3fc-163">Azure PowerShell 또는 hello Azure 명령줄 인터페이스를 사용 하는 Zip 보관 파일로 다운로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-163">It can also be downloaded as a Zip archive using Azure PowerShell or hello Azure Command-Line Interface.</span></span>

<span data-ttu-id="ed3fc-164">hello 로그에 저장 된 hello 디렉터리 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-164">hello directory structure that hello logs are stored in is as follows:</span></span>

* <span data-ttu-id="ed3fc-165">**응용 프로그램 로그** - /LogFiles/Application/입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-165">**Application logs** - /LogFiles/Application/.</span></span> <span data-ttu-id="ed3fc-166">이 폴더에는 응용 프로그램 로깅으로 생성된 정보가 포함된 하나 이상의 텍스트 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-166">This folder contains one or more text files containing information produced by application logging.</span></span>
* <span data-ttu-id="ed3fc-167">**실패한 요청 추적** - /LogFiles/W3SVC#########/입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-167">**Failed Request Traces** - /LogFiles/W3SVC#########/.</span></span> <span data-ttu-id="ed3fc-168">이 폴더에는 하나의 XSL 파일 및 하나 이상의 XML 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-168">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="ed3fc-169">Internet Explorer에서 볼 때 hello XSL 파일 hello XML의 hello 내용을 필터링 하 고 서식 지정 기능을 제공 하기 때문에 XML 파일 hello와 동일한 디렉터리에서 파일 hello에 hello XSL 파일을 다운로드 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-169">Ensure that you download hello XSL file into hello same directory as hello XML file(s) because hello XSL file provides functionality for formatting and filtering hello contents of hello XML file(s) when viewed in Internet Explorer.</span></span>
* <span data-ttu-id="ed3fc-170">**Detailed Error Logs** - /LogFiles/DetailedErrors/입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-170">**Detailed Error Logs** - /LogFiles/DetailedErrors/.</span></span> <span data-ttu-id="ed3fc-171">이 폴더에는 발생한 HTTP 오류에 대해 방대한 정보를 제공하는 하나 이상의 .htm 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-171">This folder contains one or more .htm files that provide extensive information for any HTTP errors that have occurred.</span></span>
* <span data-ttu-id="ed3fc-172">**웹 서버 로그** - /LogFiles/http/RawLogs입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-172">**Web Server Logs** - /LogFiles/http/RawLogs.</span></span> <span data-ttu-id="ed3fc-173">이 폴더에 hello를 사용 하 여 포맷 하는 하나 이상의 텍스트 파일이 [W3C 확장된 로그 파일 형식](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-173">This folder contains one or more text files formatted using hello [W3C extended log file format](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
* <span data-ttu-id="ed3fc-174">**Deployment logs** - /LogFiles/Git입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-174">**Deployment logs** - /LogFiles/Git.</span></span> <span data-ttu-id="ed3fc-175">이 폴더 포함 Azure 웹 앱에서 사용 하는 hello 내부 배포 프로세스에 의해 생성 된 로그도 Git 배포에 대 한 기록.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-175">This folder contains logs generated by hello internal deployment processes used by Azure web apps, as well as logs for Git deployments.</span></span>

### <a name="ftp"></a><span data-ttu-id="ed3fc-176">FTP</span><span class="sxs-lookup"><span data-stu-id="ed3fc-176">FTP</span></span>
<span data-ttu-id="ed3fc-177">FTP, 방문 hello를 사용 하 여 tooaccess 진단 정보 **대시보드** hello에서 웹 응용 프로그램의 [클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-177">tooaccess diagnostic information using FTP, visit hello **Dashboard** of your web app in hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="ed3fc-178">Hello에 **눈에 보는** 섹션에서 hello를 사용 하 여 **FTP 진단 로그** tooaccess hello 로그 파일이 FTP를 사용 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-178">In hello **quick glance** section, use hello **FTP Diagnostic Logs** link tooaccess hello log files using FTP.</span></span> <span data-ttu-id="ed3fc-179">hello **배포/FTP 사용자** 항목에 사용 되는 tooaccess hello FTP 사이트 되어야 하는 hello 사용자 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-179">hello **Deployment/FTP User** entry lists hello user name that should be used tooaccess hello FTP site.</span></span>

> [!NOTE]
> <span data-ttu-id="ed3fc-180">경우 hello **배포/FTP 사용자** 항목을 설정 하지 않으면 또는이 사용자에 대 한 hello 암호를 잊어버린, hello를 사용 하 여 새 사용자와 암호를 만들 수 있습니다 **배포 자격 증명 재설정** hello에대한링크**눈에 보는** hello 섹션 **대시보드**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-180">If hello **Deployment/FTP User** entry is not set, or you have forgotten hello password for this user, you can create a new user and password by using hello **Reset deployment credentials** link in hello **quick glance** section of hello **Dashboard**.</span></span>
>
>

### <a name="download-with-azure-powershell"></a><span data-ttu-id="ed3fc-181">Azure PowerShell로 다운로드</span><span class="sxs-lookup"><span data-stu-id="ed3fc-181">Download with Azure PowerShell</span></span>
<span data-ttu-id="ed3fc-182">toodownload hello 로그 파일을 Azure PowerShell의 새 인스턴스를 시작한 다음 명령을 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ed3fc-182">toodownload hello log files, start a new instance of Azure PowerShell and use hello following command:</span></span>

    Save-AzureWebSiteLog -Name webappname

<span data-ttu-id="ed3fc-183">그러면 hello로 지정 된 hello 웹 앱에 대 한 hello 로그에 저장 됩니다 **-이름** 명명 된 매개 변수 tooa 파일 **logs.zip** hello 현재 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-183">This will save hello logs for hello web app specified by hello **-Name** parameter tooa file named **logs.zip** in hello current directory.</span></span>

> [!NOTE]
> <span data-ttu-id="ed3fc-184">Azure PowerShell을 설치 하지 않은 경우 또는 구성 하지 toouse Azure 구독을 참조 [어떻게 tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-184">If you have not installed Azure PowerShell, or have not configured it toouse your Azure Subscription, see [How tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).</span></span>
>
>

### <a name="download-with-azure-command-line-interface"></a><span data-ttu-id="ed3fc-185">Azure 명령줄 인터페이스로 다운로드</span><span class="sxs-lookup"><span data-stu-id="ed3fc-185">Download with Azure Command-Line Interface</span></span>
<span data-ttu-id="ed3fc-186">hello Azure 명령줄 인터페이스를 사용 하 여 toodownload hello 로그 파일을 새 명령 프롬프트, PowerShell, Bash, 또는 터미널 세션 열고 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-186">toodownload hello log files using hello Azure Command Line Interface, open a new command prompt, PowerShell, Bash, or Terminal session and enter hello following command:</span></span>

    azure site log download webappname

<span data-ttu-id="ed3fc-187">그러면 라는 'webappname' tooa 파일 라는 hello 웹 앱에 대 한 hello 로그에 저장 됩니다 **diagnostics.zip** hello 현재 디렉터리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-187">This will save hello logs for hello web app named 'webappname' tooa file named **diagnostics.zip** in hello current directory.</span></span>

> [!NOTE]
> <span data-ttu-id="ed3fc-188">Azure 명령줄 인터페이스 (Azure CLI) hello 또는 구성 하지 않은 것 toouse 설치 하지 않은 경우 Azure 구독을 참조 [어떻게 tooUse Azure CLI](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-188">If you have not installed hello Azure Command-Line Interface (Azure CLI), or have not configured it toouse your Azure Subscription, see [How tooUse Azure CLI](../cli-install-nodejs.md).</span></span>
>
>

## <a name="how-to-view-logs-in-application-insights"></a><span data-ttu-id="ed3fc-189">방법: Application Insights에서 로그 보기</span><span class="sxs-lookup"><span data-stu-id="ed3fc-189">How to: View logs in Application Insights</span></span>
<span data-ttu-id="ed3fc-190">Visual Studio Application Insights는 필터링 및 로그 검색에 대 한 요청 및 기타 이벤트와 hello 로그의 상관 관계 도구를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-190">Visual Studio Application Insights provides tools for filtering and searching logs, and for correlating hello logs with requests and other events.</span></span>

1. <span data-ttu-id="ed3fc-191">Visual Studio에서 hello Application Insights SDK tooyour 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-191">Add hello Application Insights SDK tooyour project in Visual Studio.</span></span>
   * <span data-ttu-id="ed3fc-192">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 Application Insights 추가를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-192">In Solution Explorer, right click your project and choose Add Application Insights.</span></span> <span data-ttu-id="ed3fc-193">Application Insights 리소스 만들기를 포함 하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-193">You'll be guided through steps that include creating an Application Insights resource.</span></span> [<span data-ttu-id="ed3fc-194">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="ed3fc-194">Learn more</span></span>](../application-insights/app-insights-asp-net.md)
2. <span data-ttu-id="ed3fc-195">Hello 추적 수신기 패키지 tooyour 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-195">Add hello Trace Listener package tooyour project.</span></span>
   * <span data-ttu-id="ed3fc-196">프로젝트를 마우스 오른쪽 단추로 클릭하고 NuGet 패키지 관리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-196">Right click your project and choose Manage NuGet Packages.</span></span> <span data-ttu-id="ed3fc-197">자동으로 로그를 삭제하려면 `Microsoft.ApplicationInsights.TraceListener` [자세히 알아보기](../application-insights/app-insights-asp-net-trace-logs.md)</span><span class="sxs-lookup"><span data-stu-id="ed3fc-197">Select `Microsoft.ApplicationInsights.TraceListener` [Learn more](../application-insights/app-insights-asp-net-trace-logs.md)</span></span>
3. <span data-ttu-id="ed3fc-198">프로젝트를 업로드 하 고 toogenerate 로그 데이터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-198">Upload your project and run it toogenerate log data.</span></span>
4. <span data-ttu-id="ed3fc-199">Hello에 [Azure 포털](https://portal.azure.com/)tooyour 새 Application Insights 리소스를 찾아 열 **검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-199">In hello [Azure Portal](https://portal.azure.com/), browse tooyour new Application Insights resource, and open **Search**.</span></span> <span data-ttu-id="ed3fc-200">요청, 사용법 및 다른 원격 분석와 함께 로그 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-200">You'll see your log data, along with request, usage and other telemetry.</span></span> <span data-ttu-id="ed3fc-201">일부 원격 분석에는 몇 분 tooarrive 걸릴 수 있습니다: 새로 고침을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-201">Some telemetry might take a few minutes tooarrive: click Refresh.</span></span> [<span data-ttu-id="ed3fc-202">자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="ed3fc-202">Learn more</span></span>](../application-insights/app-insights-diagnostic-search.md)

[<span data-ttu-id="ed3fc-203">Application Insights로 추적되는 성능에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="ed3fc-203">Learn more about performance tracking with Application Insights</span></span>](../application-insights/app-insights-azure-web-apps.md)

## <span data-ttu-id="ed3fc-204"><a name="streamlogs"></a> 방법: 스트림 로그</span><span class="sxs-lookup"><span data-stu-id="ed3fc-204"><a name="streamlogs"></a> How to: Stream logs</span></span>
<span data-ttu-id="ed3fc-205">응용 프로그램을 개발 하는 동안 것이 거의 실시간에 유용한 toosee 로깅 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-205">While developing an application, it is often useful toosee logging information in near-real time.</span></span> <span data-ttu-id="ed3fc-206">Azure PowerShell 또는 hello Azure 명령줄 인터페이스를 사용 하 여 로깅 정보 tooyour 개발 환경을 스트리밍 함으로써이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-206">This can be accomplished by streaming logging information tooyour development environment using either Azure PowerShell or hello Azure Command-Line Interface.</span></span>

> [!NOTE]
> <span data-ttu-id="ed3fc-207">일부 유형의 로깅 버퍼 쓰기 toohello 로그 파일을 hello 스트림에 순서가 틀린 이벤트 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-207">Some types of logging buffer write toohello log file, which can result in out of order events in hello stream.</span></span> <span data-ttu-id="ed3fc-208">예를 들어 사용자가 페이지를 방문 하는 경우에 발생 하는 응용 프로그램 로그 항목이 hello 스트림 hello 페이지 요청에 대 한 hello 해당 HTTP 로그 항목 앞에 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-208">For example, an application log entry that occurs when a user visits a page may be displayed in hello stream before hello corresponding HTTP log entry for hello page request.</span></span>
>
> [!NOTE]
> <span data-ttu-id="ed3fc-209">스트리밍 로그 hello에 저장 된 tooany 텍스트 파일에 기록 된 정보 또한 스트리밍되지 **d:\\홈\\LogFiles\\**  폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-209">Log streaming will also stream information written tooany text file stored in hello **D:\\home\\LogFiles\\** folder.</span></span>
>
>

### <a name="streaming-with-azure-powershell"></a><span data-ttu-id="ed3fc-210">Azure PowerShell로 스트리밍</span><span class="sxs-lookup"><span data-stu-id="ed3fc-210">Streaming with Azure PowerShell</span></span>
<span data-ttu-id="ed3fc-211">toostream 로깅 정보는 Azure PowerShell의 새 인스턴스를 시작 하 고 다음 명령을 hello를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="ed3fc-211">toostream logging information, start a new instance of Azure PowerShell and use hello following command:</span></span>

    Get-AzureWebSiteLog -Name webappname -Tail

<span data-ttu-id="ed3fc-212">그러면 hello로 지정 된 toohello 웹 앱에 연결 됩니다 **-이름** 매개 변수 및 이벤트 로그 수행 되 면 hello 웹 응용 프로그램에서 스트리밍되 기 정보 toohello PowerShell 창을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-212">This will connect toohello web app specified by hello **-Name** parameter and begin streaming information toohello PowerShell window as log events occur on hello web app.</span></span> <span data-ttu-id="ed3fc-213">Hello /LogFiles 디렉터리 (d: / 홈/로그 파일)에 저장 되어 있는.txt,.log, 또는.htm toofiles 작성 된 모든 정보 toohello 로컬 콘솔이 스트리밍됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-213">Any information written toofiles ending in .txt, .log, or .htm that are stored in hello /LogFiles directory (d:/home/logfiles) will be streamed toohello local console.</span></span>

<span data-ttu-id="ed3fc-214">hello를 사용 하는 오류와 같은 특정 이벤트를 toofilter **-메시지** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-214">toofilter specific events, such as errors, use hello **-Message** parameter.</span></span> <span data-ttu-id="ed3fc-215">예:</span><span class="sxs-lookup"><span data-stu-id="ed3fc-215">For example:</span></span>

    Get-AzureWebSiteLog -Name webappname -Tail -Message Error

<span data-ttu-id="ed3fc-216">HTTP와 같이 toofilter 특정 로그 유형을 사용 하 여 hello **-경로** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-216">toofilter specific log types, such as HTTP, use hello **-Path** parameter.</span></span> <span data-ttu-id="ed3fc-217">예:</span><span class="sxs-lookup"><span data-stu-id="ed3fc-217">For example:</span></span>

    Get-AzureWebSiteLog -Name webappname -Tail -Path http

<span data-ttu-id="ed3fc-218">사용 가능한 경로 사용 하 여 hello-ListPath 매개 변수 목록이 toosee 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-218">toosee a list of available paths, use hello -ListPath parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="ed3fc-219">Azure PowerShell을 설치 하지 않은 경우 또는 구성 하지 toouse Azure 구독을 참조 [어떻게 tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-219">If you have not installed Azure PowerShell, or have not configured it toouse your Azure Subscription, see [How tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/).</span></span>
>
>

### <a name="streaming-with-azure-command-line-interface"></a><span data-ttu-id="ed3fc-220">Azure 명령줄 인터페이스로 스트리밍</span><span class="sxs-lookup"><span data-stu-id="ed3fc-220">Streaming with Azure Command-Line Interface</span></span>
<span data-ttu-id="ed3fc-221">toostream 로깅 정보는 새 명령 프롬프트, PowerShell, Bash, 또는 터미널 세션 열고 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-221">toostream logging information, open a new command prompt, PowerShell, Bash, or Terminal session and enter hello following command:</span></span>

    azure site log tail webappname

<span data-ttu-id="ed3fc-222">'Webappname' 라는 toohello 웹 앱에 연결 되 고 이벤트 로그 수행 되 면 hello 웹 응용 프로그램에서 정보 toohello 창 스트리밍을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-222">This will connect toohello web app named 'webappname' and begin streaming information toohello window as log events occur on hello web app.</span></span> <span data-ttu-id="ed3fc-223">Hello /LogFiles 디렉터리 (d: / 홈/로그 파일)에 저장 되어 있는.txt,.log, 또는.htm toofiles 작성 된 모든 정보 toohello 로컬 콘솔이 스트리밍됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-223">Any information written toofiles ending in .txt, .log, or .htm that are stored in hello /LogFiles directory (d:/home/logfiles) will be streamed toohello local console.</span></span>

<span data-ttu-id="ed3fc-224">hello를 사용 하는 오류와 같은 특정 이벤트를 toofilter **-필터** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-224">toofilter specific events, such as errors, use hello **--Filter** parameter.</span></span> <span data-ttu-id="ed3fc-225">예:</span><span class="sxs-lookup"><span data-stu-id="ed3fc-225">For example:</span></span>

    azure site log tail webappname --filter Error

<span data-ttu-id="ed3fc-226">HTTP와 같이 toofilter 특정 로그 유형을 사용 하 여 hello **-경로** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-226">toofilter specific log types, such as HTTP, use hello **--Path** parameter.</span></span> <span data-ttu-id="ed3fc-227">예:</span><span class="sxs-lookup"><span data-stu-id="ed3fc-227">For example:</span></span>

    azure site log tail webappname --path http

> [!NOTE]
> <span data-ttu-id="ed3fc-228">Azure 명령줄 인터페이스 hello 또는 구성 하지 않은 것 toouse 설치 하지 않은 경우 Azure 구독을 참조 [어떻게 tooUse Azure 명령줄 인터페이스](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-228">If you have not installed hello Azure Command-Line Interface, or have not configured it toouse your Azure Subscription, see [How tooUse Azure Command-Line Interface](../cli-install-nodejs.md).</span></span>
>
>

## <span data-ttu-id="ed3fc-229"><a name="understandlogs"></a> 방법: 진단 로그 이해</span><span class="sxs-lookup"><span data-stu-id="ed3fc-229"><a name="understandlogs"></a> How to: Understand diagnostics logs</span></span>
### <a name="application-diagnostics-logs"></a><span data-ttu-id="ed3fc-230">응용 프로그램 진단 로그</span><span class="sxs-lookup"><span data-stu-id="ed3fc-230">Application diagnostics logs</span></span>
<span data-ttu-id="ed3fc-231">응용 프로그램 진단 로그 toohello 파일 시스템, 테이블 저장소에 저장 또는 blob 저장소에 따라.NET 응용 프로그램에 대 한 특정 형식 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-231">Application diagnostics stores information in a specific format for .NET applications, depending on whether you store logs toohello file system, table storage, or blob storage.</span></span> <span data-ttu-id="ed3fc-232">저장 된 데이터의 기본 집합 hello 3 개의 저장소 유형을 모두에서 동일 hello hello 날짜 및 시간 hello 이벤트가 발생 한 hello 이벤트, (정보, 경고, 오류,) hello 이벤트 유형 및 hello 이벤트 메시지를 생성 하는 hello 프로세스 ID는.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-232">hello base set of data stored is hello same across all three storage types - hello date and time hello event occurred, hello process ID that produced hello event, hello event type (information, warning, error,) and hello event message.</span></span>

<span data-ttu-id="ed3fc-233">**파일 시스템**</span><span class="sxs-lookup"><span data-stu-id="ed3fc-233">**File system**</span></span>

<span data-ttu-id="ed3fc-234">형식에 따라 hello 각 줄 로깅된 toohello 파일 시스템 또는 스트리밍 사용 하 여 수신 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-234">Each line logged toohello file system or received using streaming will be in hello following format:</span></span>

    {Date}  PID[{process id}] {event type/level} {message}

<span data-ttu-id="ed3fc-235">예를 들어 오류 이벤트와 비슷한 toohello 다음 표시:</span><span class="sxs-lookup"><span data-stu-id="ed3fc-235">For example, an error event would appear similar toohello following:</span></span>

    2014-01-30T16:36:59  PID[3096] Error       Fatal error on hello page!

<span data-ttu-id="ed3fc-236">Toohello 파일 시스템 로깅 정보를 제공 hello 가장 기본적인 hello 세 사용할 수 있는 방법 중 hello 시간, 프로세스 id, 이벤트 수준 및 메시지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-236">Logging toohello file system provides hello most basic information of hello three available methods, providing only hello time, process id, event level, and message.</span></span>

<span data-ttu-id="ed3fc-237">**Table Storage**</span><span class="sxs-lookup"><span data-stu-id="ed3fc-237">**Table storage**</span></span>

<span data-ttu-id="ed3fc-238">Tootable 저장소를 로그인 할 때 추가 속성을 사용 하는 toofacilitate hello 이벤트에 보다 자세한 정보를 비롯 하 여 hello 테이블에 저장 된 hello 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-238">When logging tootable storage, additional properties are used toofacilitate searching hello data stored in hello table as well as more granular information on hello event.</span></span> <span data-ttu-id="ed3fc-239">hello 다음 속성 (열)에 사용 됩니다 hello 테이블에 저장 된 각 엔터티 (행).</span><span class="sxs-lookup"><span data-stu-id="ed3fc-239">hello following properties (columns) are used for each entity (row) stored in hello table.</span></span>

| <span data-ttu-id="ed3fc-240">속성 이름</span><span class="sxs-lookup"><span data-stu-id="ed3fc-240">Property name</span></span> | <span data-ttu-id="ed3fc-241">값/형식</span><span class="sxs-lookup"><span data-stu-id="ed3fc-241">Value/format</span></span> |
| --- | --- |
| <span data-ttu-id="ed3fc-242">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="ed3fc-242">PartitionKey</span></span> |<span data-ttu-id="ed3fc-243">YyyyMMddHH 형식에서 hello 이벤트의 날짜/시간</span><span class="sxs-lookup"><span data-stu-id="ed3fc-243">Date/time of hello event in yyyyMMddHH format</span></span> |
| <span data-ttu-id="ed3fc-244">RowKey</span><span class="sxs-lookup"><span data-stu-id="ed3fc-244">RowKey</span></span> |<span data-ttu-id="ed3fc-245">이 엔터티를 고유하게 식별하는 GUID 값</span><span class="sxs-lookup"><span data-stu-id="ed3fc-245">A GUID value that uniquely identifies this entity</span></span> |
| <span data-ttu-id="ed3fc-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="ed3fc-246">Timestamp</span></span> |<span data-ttu-id="ed3fc-247">hello 날짜와 시간을 hello 이벤트 발생</span><span class="sxs-lookup"><span data-stu-id="ed3fc-247">hello date and time that hello event occurred</span></span> |
| <span data-ttu-id="ed3fc-248">EventTickCount</span><span class="sxs-lookup"><span data-stu-id="ed3fc-248">EventTickCount</span></span> |<span data-ttu-id="ed3fc-249">hello 날짜와 시간을 hello 이벤트 발생 눈금 형식 (큰 전체 자릿수)</span><span class="sxs-lookup"><span data-stu-id="ed3fc-249">hello date and time that hello event occurred, in Tick format (greater precision)</span></span> |
| <span data-ttu-id="ed3fc-250">ApplicationName</span><span class="sxs-lookup"><span data-stu-id="ed3fc-250">ApplicationName</span></span> |<span data-ttu-id="ed3fc-251">hello 웹 응용 프로그램 이름</span><span class="sxs-lookup"><span data-stu-id="ed3fc-251">hello web app name</span></span> |
| <span data-ttu-id="ed3fc-252">Level</span><span class="sxs-lookup"><span data-stu-id="ed3fc-252">Level</span></span> |<span data-ttu-id="ed3fc-253">이벤트 수준(예: 오류, 경고, 정보)</span><span class="sxs-lookup"><span data-stu-id="ed3fc-253">Event level (e.g. error, warning, information)</span></span> |
| <span data-ttu-id="ed3fc-254">EventId</span><span class="sxs-lookup"><span data-stu-id="ed3fc-254">EventId</span></span> |<span data-ttu-id="ed3fc-255">이 이벤트의 hello 이벤트 ID</span><span class="sxs-lookup"><span data-stu-id="ed3fc-255">hello event ID of this event</span></span><p><p><span data-ttu-id="ed3fc-256">지정 하지 않을 경우 too0 기본값</span><span class="sxs-lookup"><span data-stu-id="ed3fc-256">Defaults too0 if none specified</span></span> |
| <span data-ttu-id="ed3fc-257">InstanceId</span><span class="sxs-lookup"><span data-stu-id="ed3fc-257">InstanceId</span></span> |<span data-ttu-id="ed3fc-258">발생 한도 hello hello 웹 앱의 인스턴스</span><span class="sxs-lookup"><span data-stu-id="ed3fc-258">Instance of hello web app that hello even occurred on</span></span> |
| <span data-ttu-id="ed3fc-259">Pid</span><span class="sxs-lookup"><span data-stu-id="ed3fc-259">Pid</span></span> |<span data-ttu-id="ed3fc-260">프로세스 ID</span><span class="sxs-lookup"><span data-stu-id="ed3fc-260">Process ID</span></span> |
| <span data-ttu-id="ed3fc-261">Tid</span><span class="sxs-lookup"><span data-stu-id="ed3fc-261">Tid</span></span> |<span data-ttu-id="ed3fc-262">hello 이벤트를 생성 하는 hello 스레드의 hello 스레드 ID</span><span class="sxs-lookup"><span data-stu-id="ed3fc-262">hello thread ID of hello thread that produced hello event</span></span> |
| <span data-ttu-id="ed3fc-263">Message</span><span class="sxs-lookup"><span data-stu-id="ed3fc-263">Message</span></span> |<span data-ttu-id="ed3fc-264">이벤트 세부 정보 메시지</span><span class="sxs-lookup"><span data-stu-id="ed3fc-264">Event detail message</span></span> |

<span data-ttu-id="ed3fc-265">**Blob 저장소**</span><span class="sxs-lookup"><span data-stu-id="ed3fc-265">**Blob storage**</span></span>

<span data-ttu-id="ed3fc-266">Tooblob 저장소를 로그인 할 때 데이터는 쉼표로 구분 된 값 (CSV) 형식으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-266">When logging tooblob storage, data is stored in comma-separated values (CSV) format.</span></span> <span data-ttu-id="ed3fc-267">비슷한 tootable 저장소 추가 필드는 기록 된 tooprovide hello 이벤트에 대 한 보다 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-267">Similar tootable storage, additional fields are logged tooprovide more granular information about hello event.</span></span> <span data-ttu-id="ed3fc-268">hello 다음 속성을 사용 hello CSV의에서 각 행에 대해:</span><span class="sxs-lookup"><span data-stu-id="ed3fc-268">hello following properties are used for each row in hello CSV:</span></span>

| <span data-ttu-id="ed3fc-269">속성 이름</span><span class="sxs-lookup"><span data-stu-id="ed3fc-269">Property name</span></span> | <span data-ttu-id="ed3fc-270">값/형식</span><span class="sxs-lookup"><span data-stu-id="ed3fc-270">Value/format</span></span> |
| --- | --- |
| <span data-ttu-id="ed3fc-271">Date</span><span class="sxs-lookup"><span data-stu-id="ed3fc-271">Date</span></span> |<span data-ttu-id="ed3fc-272">hello 날짜와 시간을 hello 이벤트 발생</span><span class="sxs-lookup"><span data-stu-id="ed3fc-272">hello date and time that hello event occurred</span></span> |
| <span data-ttu-id="ed3fc-273">Level</span><span class="sxs-lookup"><span data-stu-id="ed3fc-273">Level</span></span> |<span data-ttu-id="ed3fc-274">이벤트 수준(예: 오류, 경고, 정보)</span><span class="sxs-lookup"><span data-stu-id="ed3fc-274">Event level (e.g. error, warning, information)</span></span> |
| <span data-ttu-id="ed3fc-275">ApplicationName</span><span class="sxs-lookup"><span data-stu-id="ed3fc-275">ApplicationName</span></span> |<span data-ttu-id="ed3fc-276">hello 웹 응용 프로그램 이름</span><span class="sxs-lookup"><span data-stu-id="ed3fc-276">hello web app name</span></span> |
| <span data-ttu-id="ed3fc-277">InstanceId</span><span class="sxs-lookup"><span data-stu-id="ed3fc-277">InstanceId</span></span> |<span data-ttu-id="ed3fc-278">발생 한 이벤트 hello hello 웹 앱의 인스턴스</span><span class="sxs-lookup"><span data-stu-id="ed3fc-278">Instance of hello web app that hello event occurred on</span></span> |
| <span data-ttu-id="ed3fc-279">EventTickCount</span><span class="sxs-lookup"><span data-stu-id="ed3fc-279">EventTickCount</span></span> |<span data-ttu-id="ed3fc-280">hello 날짜와 시간을 hello 이벤트 발생 눈금 형식 (큰 전체 자릿수)</span><span class="sxs-lookup"><span data-stu-id="ed3fc-280">hello date and time that hello event occurred, in Tick format (greater precision)</span></span> |
| <span data-ttu-id="ed3fc-281">EventId</span><span class="sxs-lookup"><span data-stu-id="ed3fc-281">EventId</span></span> |<span data-ttu-id="ed3fc-282">이 이벤트의 hello 이벤트 ID</span><span class="sxs-lookup"><span data-stu-id="ed3fc-282">hello event ID of this event</span></span><p><p><span data-ttu-id="ed3fc-283">지정 하지 않을 경우 too0 기본값</span><span class="sxs-lookup"><span data-stu-id="ed3fc-283">Defaults too0 if none specified</span></span> |
| <span data-ttu-id="ed3fc-284">Pid</span><span class="sxs-lookup"><span data-stu-id="ed3fc-284">Pid</span></span> |<span data-ttu-id="ed3fc-285">프로세스 ID</span><span class="sxs-lookup"><span data-stu-id="ed3fc-285">Process ID</span></span> |
| <span data-ttu-id="ed3fc-286">Tid</span><span class="sxs-lookup"><span data-stu-id="ed3fc-286">Tid</span></span> |<span data-ttu-id="ed3fc-287">hello 이벤트를 생성 하는 hello 스레드의 hello 스레드 ID</span><span class="sxs-lookup"><span data-stu-id="ed3fc-287">hello thread ID of hello thread that produced hello event</span></span> |
| <span data-ttu-id="ed3fc-288">Message</span><span class="sxs-lookup"><span data-stu-id="ed3fc-288">Message</span></span> |<span data-ttu-id="ed3fc-289">이벤트 세부 정보 메시지</span><span class="sxs-lookup"><span data-stu-id="ed3fc-289">Event detail message</span></span> |

<span data-ttu-id="ed3fc-290">blob에 저장 된 hello 데이터 toohello 다음과 비슷한 형태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-290">hello data stored in a blob would look similar toohello following:</span></span>

    date,level,applicationName,instanceId,eventTickCount,eventId,pid,tid,message
    2014-01-30T16:36:52,Error,mywebapp,6ee38a,635266966128818593,0,3096,9,An error occurred

> [!NOTE]
> <span data-ttu-id="ed3fc-291">이 예제에 표시 된 대로 hello 로그의 첫 번째 줄 hello hello 열 머리글을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-291">hello first line of hello log will contain hello column headers as represented in this example.</span></span>
>
>

### <a name="failed-request-traces"></a><span data-ttu-id="ed3fc-292">실패한 요청 추적</span><span class="sxs-lookup"><span data-stu-id="ed3fc-292">Failed request traces</span></span>
<span data-ttu-id="ed3fc-293">실패한 요청 추적은 **fr######.xml**이라는 XML 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-293">Failed request traces are stored in XML files named **fr######.xml**.</span></span> <span data-ttu-id="ed3fc-294">toomake 것 보다 쉽게 tooview hello 기록 정보, 명명 된 XSL 스타일 시트 **freb.xsl** 에 제공 된 hello 동일 hello XML 파일 처럼 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-294">toomake it easier tooview hello logged information, an XSL stylesheet named **freb.xsl** is provided in hello same directory as hello XML files.</span></span> <span data-ttu-id="ed3fc-295">Internet Explorer에서 hello XML 파일 중 하나를 열면 hello XSL 스타일 시트 tooprovide hello 추적 정보의 형식이 지정 된 표시를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-295">Opening one of hello XML files in Internet Explorer will use hello XSL stylesheet tooprovide a formatted display of hello trace information.</span></span> <span data-ttu-id="ed3fc-296">비슷한 toohello 다음에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-296">This will appear similar toohello following:</span></span>

![실패 한 요청 hello 브라우저에 표시](./media/web-sites-enable-diagnostic-log/tws-failedrequestinbrowser.png)

### <a name="detailed-error-logs"></a><span data-ttu-id="ed3fc-298">Detailed Error Logs</span><span class="sxs-lookup"><span data-stu-id="ed3fc-298">Detailed error logs</span></span>
<span data-ttu-id="ed3fc-299">자세한 오류 로그는 발생한 HTTP 오류에 대해 좀 더 자세한 정보를 제공하는 HTML 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-299">Detailed error logs are HTML documents that provide more detailed information on HTTP errors that have occurred.</span></span> <span data-ttu-id="ed3fc-300">이들은 단순한 HTML 문서이므로 웹 브라우저를 사용하여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-300">Since they are simply HTML documents, they can be viewed using a web browser.</span></span>

### <a name="web-server-logs"></a><span data-ttu-id="ed3fc-301">웹 서버 로그</span><span class="sxs-lookup"><span data-stu-id="ed3fc-301">Web server logs</span></span>
<span data-ttu-id="ed3fc-302">hello 웹 서버 로그는 서식이 지정 hello를 사용 하 여 [W3C 확장된 로그 파일 형식](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-302">hello web server logs are formatted using hello [W3C extended log file format](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span> <span data-ttu-id="ed3fc-303">이 정보는 텍스트 편집기를 사용하여 읽거나 [Log Parser](http://go.microsoft.com/fwlink/?LinkId=246619)와 같은 유틸리티를 사용하여 구문 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-303">This information can be read using a text editor or parsed using utilities such as [Log Parser](http://go.microsoft.com/fwlink/?LinkId=246619).</span></span>

> [!NOTE]
> <span data-ttu-id="ed3fc-304">hello Azure 웹 앱에서 생성 된 로그를 지원 하지 않습니다 hello **s-computername**, **s ip**, 또는 **cs 버전** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-304">hello logs produced by Azure web apps do not support hello **s-computername**, **s-ip**, or **cs-version** fields.</span></span>
>
>

## <span data-ttu-id="ed3fc-305"><a name="nextsteps"></a> 다음 단계</span><span class="sxs-lookup"><span data-stu-id="ed3fc-305"><a name="nextsteps"></a> Next steps</span></span>
* [<span data-ttu-id="ed3fc-306">어떻게 tooMonitor 웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="ed3fc-306">How tooMonitor Web Apps</span></span>](http://docs.microsoft.com/en-us/azure/app-service-web/web-sites-monitor)
* [<span data-ttu-id="ed3fc-307">Visual Studio에서 Azure 웹앱 문제 해결</span><span class="sxs-lookup"><span data-stu-id="ed3fc-307">Troubleshooting Azure web apps in Visual Studio</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)
* [<span data-ttu-id="ed3fc-308">HDInsight에서 웹앱 로그 분석</span><span class="sxs-lookup"><span data-stu-id="ed3fc-308">Analyze web app Logs in HDInsight</span></span>](http://gallery.technet.microsoft.com/scriptcenter/Analyses-Windows-Azure-web-0b27d413)

> [!NOTE]
> <span data-ttu-id="ed3fc-309">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-309">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ed3fc-310">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed3fc-310">No credit cards required; no commitments.</span></span>
>
>

## <a name="whats-changed"></a><span data-ttu-id="ed3fc-311">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="ed3fc-311">What's changed</span></span>
* <span data-ttu-id="ed3fc-312">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="ed3fc-312">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
* <span data-ttu-id="ed3fc-313">가이드 toohello hello 이전 포털 toohello 새 포털의 변경 참조: [탐색에 대 한 참조 hello Azure 포털](http://go.microsoft.com/fwlink/?LinkId=529715)</span><span class="sxs-lookup"><span data-stu-id="ed3fc-313">For a guide toohello change of hello old portal toohello new portal see: [Reference for navigating hello Azure portal](http://go.microsoft.com/fwlink/?LinkId=529715)</span></span>
