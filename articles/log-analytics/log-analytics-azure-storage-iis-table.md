---
title: "Azure 로그 분석에서 이벤트에 대 한 IIS 및 테이블 저장소에 blob 저장소를 aaaUse | Microsoft Docs"
description: "로그 분석 tooblob 저장소를 작성 하는 IIS 로그 또는 진단 tootable 저장소를 작성 하는 Azure 서비스에 대 한 hello 로그를 읽을 수 있습니다."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="17a9b-103">Log Analytics에서 이벤트에 대해 IIS와 Azure Table Storage에 Azure Blob Storage 사용</span><span class="sxs-lookup"><span data-stu-id="17a9b-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="17a9b-104">로그 분석 저장소 또는 IIS 로그 서 면된 tooblob 저장소 tootable 진단 유틸리티를 작성 하는 서비스를 수행 하는 hello에 대 한 hello 로그를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-104">Log Analytics can read hello logs for hello following services that write diagnostics tootable storage or IIS logs written tooblob storage:</span></span>

* <span data-ttu-id="17a9b-105">Service Fabric 클러스터(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="17a9b-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="17a9b-106">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="17a9b-106">Virtual Machines</span></span>
* <span data-ttu-id="17a9b-107">웹/작업자 역할</span><span class="sxs-lookup"><span data-stu-id="17a9b-107">Web/Worker Roles</span></span>

<span data-ttu-id="17a9b-108">Log Analytics에서 이러한 리소스에 대한 데이터를 수집하려면 Azure 진단을 사용하도록 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="17a9b-109">진단 성화 hello Azure 포털을 사용할 수 있습니다 또는 PowerShell 로그 분석 toocollect hello 로그를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-109">Once diagnostics are enabled, you can use hello Azure portal or PowerShell configure Log Analytics toocollect hello logs.</span></span>

<span data-ttu-id="17a9b-110">Azure 진단은 Azure에서 실행 중인 가상 컴퓨터, 웹 역할 또는 작업자 역할에서 toocollect 진단 데이터를 수 있는 Azure 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-110">Azure Diagnostics is an Azure extension that enables you toocollect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="17a9b-111">hello 데이터는 Azure 저장소 계정에 저장 되 고 로그 분석에 의해 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-111">hello data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="17a9b-112">로그 분석 toocollect에 대 한 Azure 진단 로그 hello 로그에에서 있어야 hello 다음 위치:</span><span class="sxs-lookup"><span data-stu-id="17a9b-112">For Log Analytics toocollect these Azure Diagnostics logs, hello logs must be in hello following locations:</span></span>

| <span data-ttu-id="17a9b-113">로그 형식</span><span class="sxs-lookup"><span data-stu-id="17a9b-113">Log Type</span></span> | <span data-ttu-id="17a9b-114">리소스 종류</span><span class="sxs-lookup"><span data-stu-id="17a9b-114">Resource Type</span></span> | <span data-ttu-id="17a9b-115">위치</span><span class="sxs-lookup"><span data-stu-id="17a9b-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="17a9b-116">IIS 로그</span><span class="sxs-lookup"><span data-stu-id="17a9b-116">IIS logs</span></span> |<span data-ttu-id="17a9b-117">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="17a9b-117">Virtual Machines</span></span> <br> <span data-ttu-id="17a9b-118">웹 역할</span><span class="sxs-lookup"><span data-stu-id="17a9b-118">Web roles</span></span> <br> <span data-ttu-id="17a9b-119">작업자 역할</span><span class="sxs-lookup"><span data-stu-id="17a9b-119">Worker roles</span></span> |<span data-ttu-id="17a9b-120">wad-iis-logfiles(Blob Storage)</span><span class="sxs-lookup"><span data-stu-id="17a9b-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="17a9b-121">syslog</span><span class="sxs-lookup"><span data-stu-id="17a9b-121">Syslog</span></span> |<span data-ttu-id="17a9b-122">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="17a9b-122">Virtual Machines</span></span> |<span data-ttu-id="17a9b-123">LinuxsyslogVer2v0(Table Storage)</span><span class="sxs-lookup"><span data-stu-id="17a9b-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="17a9b-124">Service Fabric 작업 이벤트</span><span class="sxs-lookup"><span data-stu-id="17a9b-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="17a9b-125">Service Fabric 노드</span><span class="sxs-lookup"><span data-stu-id="17a9b-125">Service Fabric nodes</span></span> |<span data-ttu-id="17a9b-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="17a9b-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="17a9b-127">Service Fabric Reliable Actor 이벤트</span><span class="sxs-lookup"><span data-stu-id="17a9b-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="17a9b-128">Service Fabric 노드</span><span class="sxs-lookup"><span data-stu-id="17a9b-128">Service Fabric nodes</span></span> |<span data-ttu-id="17a9b-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="17a9b-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="17a9b-130">Service Fabric Reliable Service 이벤트</span><span class="sxs-lookup"><span data-stu-id="17a9b-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="17a9b-131">Service Fabric 노드</span><span class="sxs-lookup"><span data-stu-id="17a9b-131">Service Fabric nodes</span></span> |<span data-ttu-id="17a9b-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="17a9b-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="17a9b-133">Windows 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="17a9b-133">Windows Event logs</span></span> |<span data-ttu-id="17a9b-134">Service Fabric 노드</span><span class="sxs-lookup"><span data-stu-id="17a9b-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="17a9b-135">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="17a9b-135">Virtual Machines</span></span> <br> <span data-ttu-id="17a9b-136">웹 역할</span><span class="sxs-lookup"><span data-stu-id="17a9b-136">Web roles</span></span> <br> <span data-ttu-id="17a9b-137">작업자 역할</span><span class="sxs-lookup"><span data-stu-id="17a9b-137">Worker roles</span></span> |<span data-ttu-id="17a9b-138">WADWindowsEventLogsTable(Table Storage)</span><span class="sxs-lookup"><span data-stu-id="17a9b-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="17a9b-139">Windows ETW 로그</span><span class="sxs-lookup"><span data-stu-id="17a9b-139">Windows ETW logs</span></span> |<span data-ttu-id="17a9b-140">Service Fabric 노드</span><span class="sxs-lookup"><span data-stu-id="17a9b-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="17a9b-141">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="17a9b-141">Virtual Machines</span></span> <br> <span data-ttu-id="17a9b-142">웹 역할</span><span class="sxs-lookup"><span data-stu-id="17a9b-142">Web roles</span></span> <br> <span data-ttu-id="17a9b-143">작업자 역할</span><span class="sxs-lookup"><span data-stu-id="17a9b-143">Worker roles</span></span> |<span data-ttu-id="17a9b-144">WADETWEventTable(Table Storage)</span><span class="sxs-lookup"><span data-stu-id="17a9b-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="17a9b-145">Azure 웹사이트에서 IIS 로그는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="17a9b-146">가상 컴퓨터에 대 한 옵션이 있습니다 hello hello 설치 [로그 분석 에이전트](log-analytics-azure-vm-extension.md) 가상 컴퓨터 tooenable 추가로 insights를 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-146">For virtual machines, you have hello option of installing hello [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine tooenable additional insights.</span></span> <span data-ttu-id="17a9b-147">또한 toobeing 수 tooanalyze IIS 로그 및 이벤트 로그에 구성 변경 내용 추적, SQL 평가 및 업데이트 평가 포함 한 추가 분석을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-147">In addition toobeing able tooanalyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="17a9b-148">이벤트 로그 및 IIS 로그 컬렉션에 대한 Azure 진단을 가상 컴퓨터에서 사용</span><span class="sxs-lookup"><span data-stu-id="17a9b-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="17a9b-149">이벤트 로그와 IIS 로그 hello Microsoft Azure 포털을 사용 하 여 컬렉션에 대 한 프로시저 tooenable Azure 진단을 가상 컴퓨터에서 다음 사용 하 여 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-149">Use hello following procedure tooenable Azure diagnostics in a virtual machine for Event Log and IIS log collection using hello Microsoft Azure portal.</span></span>

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="17a9b-150">Azure 포털 hello로 가상 컴퓨터에서 Azure 진단 tooenable</span><span class="sxs-lookup"><span data-stu-id="17a9b-150">tooenable Azure diagnostics in a virtual machine with hello Azure portal</span></span>
1. <span data-ttu-id="17a9b-151">가상 컴퓨터를 만들 때 hello VM 에이전트를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-151">Install hello VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="17a9b-152">Hello 가상 컴퓨터가 이미 있는 경우 VM 에이전트가 이미 설치 되어 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-152">If hello virtual machine already exists, verify that hello VM Agent is already installed.</span></span>

   * <span data-ttu-id="17a9b-153">에 Azure 포털 hello, toohello 가상 컴퓨터를 이동, 선택 **옵션 구성**, 다음 **진단** 설정 **상태** 너무**에**.</span><span class="sxs-lookup"><span data-stu-id="17a9b-153">In hello Azure portal, navigate toohello virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** too**On**.</span></span>

     <span data-ttu-id="17a9b-154">완료 되 면 hello VM에 설치 되어 있고 실행 hello Azure 진단 확장을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-154">Upon completion, hello VM has hello Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="17a9b-155">이 확장은 진단 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="17a9b-156">모니터링을 설정하고 기존 VM에 대한 이벤트 로깅을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="17a9b-157">Hello VM 수준에서 진단을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-157">You can enable diagnostics at hello VM level.</span></span> <span data-ttu-id="17a9b-158">tooenable 진단 하 고 다음 이벤트 로깅을 구성 단계를 수행 하는 hello를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="17a9b-158">tooenable diagnostics and then configure event logging, perform hello following steps:</span></span>

   1. <span data-ttu-id="17a9b-159">Hello VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-159">Select hello VM.</span></span>
   2. <span data-ttu-id="17a9b-160">**모니터링**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="17a9b-161">**진단**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="17a9b-162">집합 hello **상태** 너무**ON**합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-162">Set hello **Status** too**ON**.</span></span>
   5. <span data-ttu-id="17a9b-163">Toocollect 하려는 각 진단 로그를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-163">Select each diagnostics log that you want toocollect.</span></span>
   6. <span data-ttu-id="17a9b-164">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="17a9b-165">IIS 로그 및 이벤트 컬렉션에 대한 웹 역할에서 Azure 진단 사용</span><span class="sxs-lookup"><span data-stu-id="17a9b-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="17a9b-166">너무 참조[어떻게 tooEnable 클라우드 서비스에서 진단](../cloud-services/cloud-services-dotnet-diagnostics.md) 에 대 한 일반 단계 Azure 진단을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-166">Refer too[How tooEnable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="17a9b-167">아래 hello 지침이이 정보를 사용 하 고 로그 분석에 사용할 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-167">hello instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="17a9b-168">Azure 진단을 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="17a9b-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="17a9b-169">IIS 로그는 기본적으로 hello scheduledTransferPeriod 전송 간격에 전송 하는 로그 데이터와 함께 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-169">IIS logs are stored by default, with log data transferred at hello scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="17a9b-170">Windows 이벤트 로그는 기본적으로 전송되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="tooenable-diagnostics"></a><span data-ttu-id="17a9b-171">tooenable 진단</span><span class="sxs-lookup"><span data-stu-id="17a9b-171">tooenable diagnostics</span></span>
<span data-ttu-id="17a9b-172">tooenable Windows 이벤트 로그 또는 toochange scheduledTransferPeriod hello, 같이 hello XML 구성 파일 (diagnostics.wadcfg)을 사용 하 여 Azure 진단 구성 [4 단계: 진단 구성 파일을 만들고 hello를 설치 합니다. 확장](../cloud-services/cloud-services-dotnet-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="17a9b-172">tooenable Windows Event Logs, or toochange hello scheduledTransferPeriod, configure Azure Diagnostics using hello XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install hello extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="17a9b-173">hello 다음 예제에서는 구성 파일에서 수집 IIS 로그 및 모든 hello 응용 프로그램에서에서 발생 한 이벤트와 시스템 로그.</span><span class="sxs-lookup"><span data-stu-id="17a9b-173">hello following example configuration file collects IIS Logs and all Events from hello Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

<span data-ttu-id="17a9b-174">ConfigurationSettings hello 다음 예제 처럼 저장소 계정을 지정 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-174">Ensure that your ConfigurationSettings specifies a storage account, as in hello following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="17a9b-175">hello **AccountName** 및 **AccountKey** 값은 hello 저장소 계정 대시보드의 액세스 키 관리 아래에서 Azure 포털 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-175">hello **AccountName** and **AccountKey** values are found in hello Azure portal in hello storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="17a9b-176">hello 연결 문자열에 대 한 hello 프로토콜 있어야 **https**합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-176">hello protocol for hello connection string must be **https**.</span></span>

<span data-ttu-id="17a9b-177">Hello 업데이트 된 진단 구성이 적용 되 고 나면 tooyour 클라우드 서비스 이므로 기록 진단 tooAzure 저장소, 준비 tooconfigure 로그 분석 중인 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-177">Once hello updated diagnostic configuration is applied tooyour cloud service and it is writing diagnostics tooAzure Storage, then you are ready tooconfigure Log Analytics.</span></span>

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a><span data-ttu-id="17a9b-178">Azure 저장소에서 Azure 포털 toocollect 로그 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="17a9b-178">Use hello Azure portal toocollect logs from Azure Storage</span></span>
<span data-ttu-id="17a9b-179">Azure 서비스를 수행 하는 hello에 대 한 hello Azure 포털 tooconfigure 로그 분석 toocollect hello 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-179">You can use hello Azure portal tooconfigure Log Analytics toocollect hello logs for hello following Azure services:</span></span>

* <span data-ttu-id="17a9b-180">서비스 패브릭 클러스터</span><span class="sxs-lookup"><span data-stu-id="17a9b-180">Service Fabric clusters</span></span>
* <span data-ttu-id="17a9b-181">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="17a9b-181">Virtual Machines</span></span>
* <span data-ttu-id="17a9b-182">웹/작업자 역할</span><span class="sxs-lookup"><span data-stu-id="17a9b-182">Web/Worker Roles</span></span>

<span data-ttu-id="17a9b-183">Hello Azure 포털에서에서 tooyour 로그 분석 작업 영역을 탐색 하 고 작업을 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-183">In hello Azure portal, navigate tooyour Log Analytics workspace and perform hello following tasks:</span></span>

1. <span data-ttu-id="17a9b-184">*저장소 계정 로그*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="17a9b-185">Hello 클릭 *추가* 작업</span><span class="sxs-lookup"><span data-stu-id="17a9b-185">Click hello *Add* task</span></span>
3. <span data-ttu-id="17a9b-186">Hello 진단 로그를 포함 하는 hello 저장소 계정을 선택합니다</span><span class="sxs-lookup"><span data-stu-id="17a9b-186">Select hello Storage account that contains hello diagnostics logs</span></span>
   * <span data-ttu-id="17a9b-187">이 계정은 클래식 저장소 계정 또는 Azure Resource Manager 저장소 계정일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="17a9b-188">Hello에 대 한 toocollect 로그를 원하는 데이터 형식을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-188">Select hello Data Type you want toocollect logs for</span></span>
   * <span data-ttu-id="17a9b-189">hello 선택 항목은 IIS 로그 이벤트입니다. Syslog (Linux); ETW 로그 서비스 패브릭 이벤트</span><span class="sxs-lookup"><span data-stu-id="17a9b-189">hello choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="17a9b-190">원본에 대 한 hello 값 자동으로 채워집니다 hello 데이터 입력 하 고 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-190">hello value for Source is automatically populated based on hello data type and cannot be changed</span></span>
6. <span data-ttu-id="17a9b-191">확인 toosave hello 구성을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-191">Click OK toosave hello configuration</span></span>

<span data-ttu-id="17a9b-192">로그 분석 toocollect 원하는 추가 저장소 계정 및 데이터 형식에 대해 2 ~ 6 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics toocollect.</span></span>

<span data-ttu-id="17a9b-193">약 30 분 수 toosee hello 저장소에서에서 계정의 데이터를 로그 분석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-193">In approximately 30 minutes, you are able toosee data from hello storage account in Log Analytics.</span></span> <span data-ttu-id="17a9b-194">또한 hello 구성이 적용 된 후 toostorage 작성 된 데이터에 대해서만 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-194">You will only see data that is written toostorage after hello configuration is applied.</span></span> <span data-ttu-id="17a9b-195">로그 분석 hello 저장소 계정에서 hello 기존의 데이터를 읽지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-195">Log Analytics does not read hello pre-existing data from hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="17a9b-196">새 데이터를 쓰고 또는 hello 포털 원본이 hello 저장소 계정에 해당 hello 유효성을 검사 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-196">hello portal does not validate that hello Source exists in hello storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="17a9b-197">PowerShell을 사용하여 이벤트 로그 및 IIS 로그 컬렉션에 대한 Azure 진단을 가상 컴퓨터에서 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="17a9b-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="17a9b-198">단계를 사용 하 여 hello [로그 분석 구성 tooindex Azure 진단](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) tootable 저장소 작성 된 Azure 진단의 toouse PowerShell tooread 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-198">Use hello steps in [Configuring Log Analytics tooindex Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread from Azure diagnostics that are written tootable storage.</span></span>

<span data-ttu-id="17a9b-199">Azure PowerShell을 사용 하 여 hello 기록 된 이벤트를 tooAzure 저장소를 보다 정확 하 게 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-199">Using Azure PowerShell you can more precisely specify hello events that are written tooAzure Storage.</span></span>
<span data-ttu-id="17a9b-200">자세한 내용은 [Azure 가상 컴퓨터에서 진단 사용](../virtual-machines-dotnet-diagnostics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="17a9b-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="17a9b-201">사용 하도록 설정 하 고 PowerShell 스크립트 뒤 hello를 사용 하 여 Azure 진단을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-201">You can enable and update Azure diagnostics using hello following PowerShell script.</span></span>
<span data-ttu-id="17a9b-202">또한 사용자 지정 로깅 구성을 사용하여 이 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="17a9b-203">Hello 스크립트 tooset hello 저장소 계정, 서비스 이름 및 가상 컴퓨터 이름을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-203">Modify hello script tooset hello storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="17a9b-204">hello 스크립트 클래식 가상 컴퓨터에 대 한 cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-204">hello script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="17a9b-205">다음 스크립트 샘플 hello 검토, 복사, 필요에 따라 수정, hello 샘플 PowerShell 스크립트 파일로 저장 고 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-205">Review hello following script sample, copy it, modify it as needed, save hello sample as a PowerShell script file, and then run hello script.</span></span>

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="17a9b-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="17a9b-206">Next steps</span></span>
* <span data-ttu-id="17a9b-207">지원되는 Azure 서비스에 대해 [Azure 서비스에 대한 로그 및 메트릭 수집](log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="17a9b-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="17a9b-208">[솔루션 사용](log-analytics-add-solutions.md) hello 데이터에 대 한 tooprovide 한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-208">[Enable Solutions](log-analytics-add-solutions.md) tooprovide insight into hello data.</span></span>
* <span data-ttu-id="17a9b-209">[검색 쿼리를 사용 하 여](log-analytics-log-searches.md) tooanalyze hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="17a9b-209">[Use search queries](log-analytics-log-searches.md) tooanalyze hello data.</span></span>
