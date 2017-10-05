---
title: "Azure Storage에서 진단 데이터 저장 및 보기 | Microsoft Docs"
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
ms.openlocfilehash: 374cc179e13c00e439415e3df16e0c6d5ccba5e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="e1f1b-103">Azure 저장소에서 진단 데이터 저장 및 보기</span><span class="sxs-lookup"><span data-stu-id="e1f1b-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="e1f1b-104">진단 데이터를 Microsoft Azure 저장소 에뮬레이터 또는 Azure 저장소에 전송하지 않는 한 진단 데이터는 영구적으로 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-104">Diagnostic data is not permanently stored unless you transfer it to the Microsoft Azure storage emulator or to Azure storage.</span></span> <span data-ttu-id="e1f1b-105">저장소에서 사용할 수 있는 여러 도구 중 하나로 한 번 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="e1f1b-106">저장소 계정 지정</span><span class="sxs-lookup"><span data-stu-id="e1f1b-106">Specify a storage account</span></span>
<span data-ttu-id="e1f1b-107">ServiceConfiguration.cscfg 파일에서 사용하려는 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-107">You specify the storage account that you want to use in the ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="e1f1b-108">계정 정보는 구성 설정에서 연결 문자열로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-108">The account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="e1f1b-109">다음 예제에서는 Visual Studio에서 새 클라우드 서비스 프로젝트에 대해 생성된 기본 연결 문자열을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-109">The following example shows the default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="e1f1b-110">이 연결 문자열을 변경하여 Azure 저장소 계정에 대한 계정 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-110">You can change this connection string to provide account information for an Azure storage account.</span></span>

<span data-ttu-id="e1f1b-111">수집되는 진단 데이터의 형식에 따라 Azure 진단은 Blob 서비스 또는 테이블 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-111">Depending on the type of diagnostic data that is being collected, Azure Diagnostics uses either the Blob service or the Table service.</span></span> <span data-ttu-id="e1f1b-112">다음 표에서 유지되는 데이터 원본 및 해당 형식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-112">The following table shows the data sources that are persisted and their format.</span></span>

| <span data-ttu-id="e1f1b-113">데이터 원본</span><span class="sxs-lookup"><span data-stu-id="e1f1b-113">Data source</span></span> | <span data-ttu-id="e1f1b-114">저장소 형식</span><span class="sxs-lookup"><span data-stu-id="e1f1b-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="e1f1b-115">Azure 로그</span><span class="sxs-lookup"><span data-stu-id="e1f1b-115">Azure logs</span></span> |<span data-ttu-id="e1f1b-116">테이블</span><span class="sxs-lookup"><span data-stu-id="e1f1b-116">Table</span></span> |
| <span data-ttu-id="e1f1b-117">IIS 7.0 로그</span><span class="sxs-lookup"><span data-stu-id="e1f1b-117">IIS 7.0 logs</span></span> |<span data-ttu-id="e1f1b-118">Blob</span><span class="sxs-lookup"><span data-stu-id="e1f1b-118">Blob</span></span> |
| <span data-ttu-id="e1f1b-119">Azure 진단 인프라 로그</span><span class="sxs-lookup"><span data-stu-id="e1f1b-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="e1f1b-120">테이블</span><span class="sxs-lookup"><span data-stu-id="e1f1b-120">Table</span></span> |
| <span data-ttu-id="e1f1b-121">실패한 요청 추적 로그</span><span class="sxs-lookup"><span data-stu-id="e1f1b-121">Failed Request Trace logs</span></span> |<span data-ttu-id="e1f1b-122">Blob</span><span class="sxs-lookup"><span data-stu-id="e1f1b-122">Blob</span></span> |
| <span data-ttu-id="e1f1b-123">Windows 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="e1f1b-123">Windows Event logs</span></span> |<span data-ttu-id="e1f1b-124">테이블</span><span class="sxs-lookup"><span data-stu-id="e1f1b-124">Table</span></span> |
| <span data-ttu-id="e1f1b-125">성능 카운터</span><span class="sxs-lookup"><span data-stu-id="e1f1b-125">Performance counters</span></span> |<span data-ttu-id="e1f1b-126">테이블</span><span class="sxs-lookup"><span data-stu-id="e1f1b-126">Table</span></span> |
| <span data-ttu-id="e1f1b-127">크래시 덤프</span><span class="sxs-lookup"><span data-stu-id="e1f1b-127">Crash dumps</span></span> |<span data-ttu-id="e1f1b-128">Blob</span><span class="sxs-lookup"><span data-stu-id="e1f1b-128">Blob</span></span> |
| <span data-ttu-id="e1f1b-129">사용자 지정 오류 로그</span><span class="sxs-lookup"><span data-stu-id="e1f1b-129">Custom error logs</span></span> |<span data-ttu-id="e1f1b-130">Blob</span><span class="sxs-lookup"><span data-stu-id="e1f1b-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="e1f1b-131">진단 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="e1f1b-131">Transfer diagnostic data</span></span>
<span data-ttu-id="e1f1b-132">SDK 2.5 이상의 경우 구성 파일을 통해 진단 데이터 전송 요청이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-132">For SDK 2.5 and later, the request to transfer diagnostic data can occur through the configuration file.</span></span> <span data-ttu-id="e1f1b-133">구성에서 지정된 예약된 간격으로 진단 데이터를 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-133">You can transfer diagnostic data at scheduled intervals as specified in the configuration.</span></span>

<span data-ttu-id="e1f1b-134">SDK 2.4 및 이전 버전의 경우 프로그래밍 방식으로 구성 파일을 통해 진단 데이터 전송을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-134">For SDK 2.4 and previous you can request to transfer the diagnostic data through the configuration file as well as programmatically.</span></span> <span data-ttu-id="e1f1b-135">프로그래밍 방식을 사용하면 주문형 전송을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-135">The programmatic approach also allows you to do on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1f1b-136">Azure 저장소 계정에 진단 데이터를 전송하는 경우 진단 데이터를 사용하는 저장소 리소스에 대한 비용이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-136">When you transfer diagnostic data to an Azure storage account, you incur costs for the storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="e1f1b-137">진단 데이터 저장</span><span class="sxs-lookup"><span data-stu-id="e1f1b-137">Store diagnostic data</span></span>
<span data-ttu-id="e1f1b-138">로그 데이터는 다음과 같은 이름의 Blob 또는 테이블 저장소에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-138">Log data is stored in either Blob or Table storage with the following names:</span></span>

<span data-ttu-id="e1f1b-139">**테이블**</span><span class="sxs-lookup"><span data-stu-id="e1f1b-139">**Tables**</span></span>

* <span data-ttu-id="e1f1b-140">**WadLogsTable** - 추적 수신기를 사용하여 코드에서 작성된 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-140">**WadLogsTable** - Logs written in code using the trace listener.</span></span>
* <span data-ttu-id="e1f1b-141">**WADDiagnosticInfrastructureLogsTable** - 진단 모니터 및 구성 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="e1f1b-142">**WADDirectoriesTable** – 진단 모니터를 모니터링하는 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-142">**WADDirectoriesTable** – Directories that the diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="e1f1b-143">IIS 로그, IIS 실패한 요청 로그 및 사용자 지정 디렉터리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="e1f1b-144">Blob 로그 파일의 위치는 Container 필드에 지정되고 Blob의 이름은 RelativePath 필드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-144">The location of the blob log file is specified in the Container field and the name of the blob is in the RelativePath field.</span></span>  <span data-ttu-id="e1f1b-145">AbsolutePath 필드는 Azure 가상 컴퓨터에 존재했던 파일의 이름과 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-145">The AbsolutePath field indicates the location and name of the file as it existed on the Azure virtual machine.</span></span>
* <span data-ttu-id="e1f1b-146">**WADPerformanceCountersTable** – 성능 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="e1f1b-147">**WADWindowsEventLogsTable** – Windows 이벤트 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="e1f1b-148">**Blob**</span><span class="sxs-lookup"><span data-stu-id="e1f1b-148">**Blobs**</span></span>

* <span data-ttu-id="e1f1b-149">**wad-control-container** – (SDK 2.4 및 이전 버전의 경우만) Azure 진단을 제어하는 XML 구성 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains the XML configuration files that controls the Azure diagnostics .</span></span>
* <span data-ttu-id="e1f1b-150">**wad-iis-failedreqlogfiles** – IIS 실패한 요청 로그에서 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="e1f1b-151">**wad-iis-logfiles** – IIS 로그에 관한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="e1f1b-152">**"custom"** – 진단 모니터에 의해 모니터링되는 구성 디렉터리에 기반한 사용자 지정 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-152">**"custom"** – A custom container based on configuring directories that are monitored by the diagnostic monitor.</span></span>  <span data-ttu-id="e1f1b-153">이 Blob 컨테이너의 이름은 WADDirectoriesTable에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-153">The name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-to-view-diagnostic-data"></a><span data-ttu-id="e1f1b-154">진단 데이터를 볼 도구</span><span class="sxs-lookup"><span data-stu-id="e1f1b-154">Tools to view diagnostic data</span></span>
<span data-ttu-id="e1f1b-155">여러 도구를 사용하여 저장소로 전송된 후 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-155">Several tools are available to view the data after it is transferred to storage.</span></span> <span data-ttu-id="e1f1b-156">예:</span><span class="sxs-lookup"><span data-stu-id="e1f1b-156">For example:</span></span>

* <span data-ttu-id="e1f1b-157">Visual Studio의 서버 탐색기 - Microsoft Visual Studio용 Azure 도구를 설치한 경우 서버 탐색기에서 Azure 저장소 노드를 사용하여 Azure 저장소 계정에서 읽기 전용 Blob 및 테이블 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-157">Server Explorer in Visual Studio - If you have installed the Azure Tools for Microsoft Visual Studio, you can use the Azure Storage node in Server Explorer to view read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="e1f1b-158">로컬 저장소 에뮬레이터 계정 및 Azure용으로 만든 저장소 계정에서 데이터를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="e1f1b-159">자세한 내용은 [서버 탐색기로 저장소 리소스 탐색 및 관리](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="e1f1b-160">[Microsoft Azure Storage 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md) 는 Windows, OSX 및 Linux에서 Azure Storage 데이터로 손쉽게 작업할 수 있도록 해주는 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you to easily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="e1f1b-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) 에는 Azure에서 실행되는 응용 프로그램으로 수집된 진단 데이터를 보고 다운로드하고 관리할 수 있는 Azure 진단 관리자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1f1b-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you to view, download and manage the diagnostics data collected by the applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1f1b-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e1f1b-162">Next Steps</span></span>
[<span data-ttu-id="e1f1b-163">Azure 진단으로 클라우드 서비스 응용 프로그램의 흐름 추적</span><span class="sxs-lookup"><span data-stu-id="e1f1b-163">Trace the flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

