---
title: "aaaStore 및 Azure 저장소에 진단 데이터 보기 | Microsoft Docs"
description: "Azure 저장소로 Azure 진단 데이터를 가져오고 보기"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="58233-103">Azure 저장소에서 진단 데이터 저장 및 보기</span><span class="sxs-lookup"><span data-stu-id="58233-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="58233-104">Toohello Microsoft Azure 저장소 에뮬레이터 또는 tooAzure 저장소 전송 하지 않는 한 진단 데이터는 영구적으로 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58233-104">Diagnostic data is not permanently stored unless you transfer it toohello Microsoft Azure storage emulator or tooAzure storage.</span></span> <span data-ttu-id="58233-105">저장소에서 사용할 수 있는 여러 도구 중 하나로 한 번 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58233-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="58233-106">저장소 계정 지정</span><span class="sxs-lookup"><span data-stu-id="58233-106">Specify a storage account</span></span>
<span data-ttu-id="58233-107">Toouse hello ServiceConfiguration.cscfg 파일에 지정 하는 hello 저장소 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="58233-107">You specify hello storage account that you want toouse in hello ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="58233-108">hello 계정 정보는 구성 설정에 대 한 연결 문자열로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58233-108">hello account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="58233-109">hello 다음 예제는 Visual Studio에서 새 클라우드 서비스 프로젝트에 대해 만든 hello 기본 연결 문자열.</span><span class="sxs-lookup"><span data-stu-id="58233-109">hello following example shows hello default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="58233-110">Azure 저장소 계정에 대 한이 연결 문자열 tooprovide 계정 정보를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58233-110">You can change this connection string tooprovide account information for an Azure storage account.</span></span>

<span data-ttu-id="58233-111">수집 되 고 진단 데이터의 hello 형식에 따라 Azure 진단 hello Blob 서비스 또는 hello 테이블 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="58233-111">Depending on hello type of diagnostic data that is being collected, Azure Diagnostics uses either hello Blob service or hello Table service.</span></span> <span data-ttu-id="58233-112">hello 다음 표에서 지속 hello 데이터 원본 및 해당 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="58233-112">hello following table shows hello data sources that are persisted and their format.</span></span>

| <span data-ttu-id="58233-113">데이터 원본</span><span class="sxs-lookup"><span data-stu-id="58233-113">Data source</span></span> | <span data-ttu-id="58233-114">저장소 형식</span><span class="sxs-lookup"><span data-stu-id="58233-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="58233-115">Azure 로그</span><span class="sxs-lookup"><span data-stu-id="58233-115">Azure logs</span></span> |<span data-ttu-id="58233-116">테이블</span><span class="sxs-lookup"><span data-stu-id="58233-116">Table</span></span> |
| <span data-ttu-id="58233-117">IIS 7.0 로그</span><span class="sxs-lookup"><span data-stu-id="58233-117">IIS 7.0 logs</span></span> |<span data-ttu-id="58233-118">Blob</span><span class="sxs-lookup"><span data-stu-id="58233-118">Blob</span></span> |
| <span data-ttu-id="58233-119">Azure 진단 인프라 로그</span><span class="sxs-lookup"><span data-stu-id="58233-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="58233-120">테이블</span><span class="sxs-lookup"><span data-stu-id="58233-120">Table</span></span> |
| <span data-ttu-id="58233-121">실패한 요청 추적 로그</span><span class="sxs-lookup"><span data-stu-id="58233-121">Failed Request Trace logs</span></span> |<span data-ttu-id="58233-122">Blob</span><span class="sxs-lookup"><span data-stu-id="58233-122">Blob</span></span> |
| <span data-ttu-id="58233-123">Windows 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="58233-123">Windows Event logs</span></span> |<span data-ttu-id="58233-124">테이블</span><span class="sxs-lookup"><span data-stu-id="58233-124">Table</span></span> |
| <span data-ttu-id="58233-125">성능 카운터</span><span class="sxs-lookup"><span data-stu-id="58233-125">Performance counters</span></span> |<span data-ttu-id="58233-126">테이블</span><span class="sxs-lookup"><span data-stu-id="58233-126">Table</span></span> |
| <span data-ttu-id="58233-127">크래시 덤프</span><span class="sxs-lookup"><span data-stu-id="58233-127">Crash dumps</span></span> |<span data-ttu-id="58233-128">Blob</span><span class="sxs-lookup"><span data-stu-id="58233-128">Blob</span></span> |
| <span data-ttu-id="58233-129">사용자 지정 오류 로그</span><span class="sxs-lookup"><span data-stu-id="58233-129">Custom error logs</span></span> |<span data-ttu-id="58233-130">Blob</span><span class="sxs-lookup"><span data-stu-id="58233-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="58233-131">진단 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="58233-131">Transfer diagnostic data</span></span>
<span data-ttu-id="58233-132">SDK 2.5 이상 버전에서는 hello 요청 tootransfer 진단 데이터는 hello 구성 파일을 통해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58233-132">For SDK 2.5 and later, hello request tootransfer diagnostic data can occur through hello configuration file.</span></span> <span data-ttu-id="58233-133">Hello 구성에 지정 된 예약 된 간격으로 진단 데이터를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58233-133">You can transfer diagnostic data at scheduled intervals as specified in hello configuration.</span></span>

<span data-ttu-id="58233-134">SDK 2.4 및 이전 프로그래밍 방식 tootransfer hello에 대 한 진단 데이터도 hello 구성 파일을 통해 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58233-134">For SDK 2.4 and previous you can request tootransfer hello diagnostic data through hello configuration file as well as programmatically.</span></span> <span data-ttu-id="58233-135">hello 프로그래밍 방식을 toodo 주문형 전송을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="58233-135">hello programmatic approach also allows you toodo on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58233-136">진단 데이터 tooan Azure 저장소 계정으로 전송할 경우 진단 데이터가 사용 하는 hello 저장소 리소스에 대 한 비용이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="58233-136">When you transfer diagnostic data tooan Azure storage account, you incur costs for hello storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="58233-137">진단 데이터 저장</span><span class="sxs-lookup"><span data-stu-id="58233-137">Store diagnostic data</span></span>
<span data-ttu-id="58233-138">로그 데이터는 이름 다음 hello로 Blob 또는 테이블 저장소에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58233-138">Log data is stored in either Blob or Table storage with hello following names:</span></span>

<span data-ttu-id="58233-139">**테이블**</span><span class="sxs-lookup"><span data-stu-id="58233-139">**Tables**</span></span>

* <span data-ttu-id="58233-140">**WadLogsTable** -hello 추적 수신기를 사용 하 여 코드를 작성 한 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="58233-140">**WadLogsTable** - Logs written in code using hello trace listener.</span></span>
* <span data-ttu-id="58233-141">**WADDiagnosticInfrastructureLogsTable** - 진단 모니터 및 구성 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="58233-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="58233-142">**WADDirectoriesTable** – 디렉터리 해당 hello 진단 모니터는 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="58233-142">**WADDirectoriesTable** – Directories that hello diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="58233-143">IIS 로그, IIS 실패한 요청 로그 및 사용자 지정 디렉터리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="58233-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="58233-144">hello blob 로그 파일의 위치 hello hello Container 필드에 지정 된 및 hello hello blob 이름이 hello RelativePath 필드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58233-144">hello location of hello blob log file is specified in hello Container field and hello name of hello blob is in hello RelativePath field.</span></span>  <span data-ttu-id="58233-145">hello AbsolutePath 필드 hello Azure 가상 컴퓨터에 hello 파일의 이름과 hello 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="58233-145">hello AbsolutePath field indicates hello location and name of hello file as it existed on hello Azure virtual machine.</span></span>
* <span data-ttu-id="58233-146">**WADPerformanceCountersTable** – 성능 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="58233-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="58233-147">**WADWindowsEventLogsTable** – Windows 이벤트 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="58233-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="58233-148">**Blob**</span><span class="sxs-lookup"><span data-stu-id="58233-148">**Blobs**</span></span>

* <span data-ttu-id="58233-149">**wad 컨트롤 컨테이너** – (SDK 2.4 및 이전) hello Azure 진단을 제어 하는 hello XML 구성 파일이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58233-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains hello XML configuration files that controls hello Azure diagnostics .</span></span>
* <span data-ttu-id="58233-150">**wad-iis-failedreqlogfiles** – IIS 실패한 요청 로그에서 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="58233-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="58233-151">**wad-iis-logfiles** – IIS 로그에 관한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="58233-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="58233-152">**"custom"** – hello 진단 모니터에 의해 모니터링 되는 디렉터리를 구성 하는 방법에 따라 사용자 지정 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="58233-152">**"custom"** – A custom container based on configuring directories that are monitored by hello diagnostic monitor.</span></span>  <span data-ttu-id="58233-153">이 blob 컨테이너의 hello 이름은 WADDirectoriesTable에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58233-153">hello name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-tooview-diagnostic-data"></a><span data-ttu-id="58233-154">도구 tooview 진단 데이터</span><span class="sxs-lookup"><span data-stu-id="58233-154">Tools tooview diagnostic data</span></span>
<span data-ttu-id="58233-155">여러 가지 도구는 전송된 toostorage 올바르게 설치 후 사용 가능한 tooview hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="58233-155">Several tools are available tooview hello data after it is transferred toostorage.</span></span> <span data-ttu-id="58233-156">예:</span><span class="sxs-lookup"><span data-stu-id="58233-156">For example:</span></span>

* <span data-ttu-id="58233-157">Visual Studio-서버 탐색기 hello Azure 도구 for Microsoft Visual Studio를 설치 하는 경우 사용할 수 있습니다 hello Azure 저장소 노드 서버 탐색기 tooview 읽기 전용 blob 및 테이블 데이터의 Azure 저장소 계정에서.</span><span class="sxs-lookup"><span data-stu-id="58233-157">Server Explorer in Visual Studio - If you have installed hello Azure Tools for Microsoft Visual Studio, you can use hello Azure Storage node in Server Explorer tooview read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="58233-158">로컬 저장소 에뮬레이터 계정 및 Azure용으로 만든 저장소 계정에서 데이터를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58233-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="58233-159">자세한 내용은 [서버 탐색기로 저장소 리소스 탐색 및 관리](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58233-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="58233-160">[Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md) 는 Windows, OSX 및 Linux에서 데이터를 Azure 저장소 사용 tooeasily 작업 수 있도록 하는 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="58233-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="58233-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) tooview, 수 있는 Azure 진단 관리자를 포함 합니다. 다운로드 하 고 Azure에서 실행 되는 hello 응용 프로그램에서 수집한 hello 진단 데이터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="58233-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you tooview, download and manage hello diagnostics data collected by hello applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58233-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="58233-162">Next Steps</span></span>
[<span data-ttu-id="58233-163">Azure 진단으로 클라우드 서비스 응용 프로그램에서 추적 hello 흐름</span><span class="sxs-lookup"><span data-stu-id="58233-163">Trace hello flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

