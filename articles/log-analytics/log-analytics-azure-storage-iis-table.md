---
title: "Azure Log Analytics에서 이벤트에 대해 IIS와 Table Storage에 Blob Storage 사용 | Microsoft Docs"
description: "Log Analytics는 Table Storage에 진단을 쓰는 Azure 서비스 또는 Blob Storage에 기록된 IIS 로그에 대해 로그를 읽을 수 있습니다."
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
ms.openlocfilehash: 459ef90ca1d76bada6565bfefd7b4bd1086197d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="3f45c-103">Log Analytics에서 이벤트에 대해 IIS와 Azure Table Storage에 Azure Blob Storage 사용</span><span class="sxs-lookup"><span data-stu-id="3f45c-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="3f45c-104">Log Analytics는 Table Storage에 진단을 쓰는 다음 서비스에 대한 로그나 Blob Storage에 기록된 IIS 로그를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-104">Log Analytics can read the logs for the following services that write diagnostics to table storage or IIS logs written to blob storage:</span></span>

* <span data-ttu-id="3f45c-105">Service Fabric 클러스터(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="3f45c-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="3f45c-106">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3f45c-106">Virtual Machines</span></span>
* <span data-ttu-id="3f45c-107">웹/작업자 역할</span><span class="sxs-lookup"><span data-stu-id="3f45c-107">Web/Worker Roles</span></span>

<span data-ttu-id="3f45c-108">Log Analytics에서 이러한 리소스에 대한 데이터를 수집하려면 Azure 진단을 사용하도록 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="3f45c-109">진단이 사용하도록 설정되어 있으면 Azure Portal 또는 PowerShell을 사용하여 로그를 수집하도록 Log Analytics를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-109">Once diagnostics are enabled, you can use the Azure portal or PowerShell configure Log Analytics to collect the logs.</span></span>

<span data-ttu-id="3f45c-110">Azure 진단은 Azure에서 실행 중인 작업자 역할, 웹 역할 또는 가상 컴퓨터에서 진단 데이터를 수집하는 데 사용할 수 있는 Azure 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-110">Azure Diagnostics is an Azure extension that enables you to collect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="3f45c-111">데이터는 Azure Storage 계정에 저장되며 이후 Log Analytics를 통해 수집될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-111">The data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="3f45c-112">Log Analytics가 이러한 Azure Diagnostics 로그를 수집하려면 로그가 다음 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-112">For Log Analytics to collect these Azure Diagnostics logs, the logs must be in the following locations:</span></span>

| <span data-ttu-id="3f45c-113">로그 형식</span><span class="sxs-lookup"><span data-stu-id="3f45c-113">Log Type</span></span> | <span data-ttu-id="3f45c-114">리소스 종류</span><span class="sxs-lookup"><span data-stu-id="3f45c-114">Resource Type</span></span> | <span data-ttu-id="3f45c-115">위치</span><span class="sxs-lookup"><span data-stu-id="3f45c-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3f45c-116">IIS 로그</span><span class="sxs-lookup"><span data-stu-id="3f45c-116">IIS logs</span></span> |<span data-ttu-id="3f45c-117">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3f45c-117">Virtual Machines</span></span> <br> <span data-ttu-id="3f45c-118">웹 역할</span><span class="sxs-lookup"><span data-stu-id="3f45c-118">Web roles</span></span> <br> <span data-ttu-id="3f45c-119">작업자 역할</span><span class="sxs-lookup"><span data-stu-id="3f45c-119">Worker roles</span></span> |<span data-ttu-id="3f45c-120">wad-iis-logfiles(Blob Storage)</span><span class="sxs-lookup"><span data-stu-id="3f45c-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="3f45c-121">syslog</span><span class="sxs-lookup"><span data-stu-id="3f45c-121">Syslog</span></span> |<span data-ttu-id="3f45c-122">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3f45c-122">Virtual Machines</span></span> |<span data-ttu-id="3f45c-123">LinuxsyslogVer2v0(Table Storage)</span><span class="sxs-lookup"><span data-stu-id="3f45c-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="3f45c-124">Service Fabric 작업 이벤트</span><span class="sxs-lookup"><span data-stu-id="3f45c-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="3f45c-125">Service Fabric 노드</span><span class="sxs-lookup"><span data-stu-id="3f45c-125">Service Fabric nodes</span></span> |<span data-ttu-id="3f45c-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="3f45c-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="3f45c-127">Service Fabric Reliable Actor 이벤트</span><span class="sxs-lookup"><span data-stu-id="3f45c-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="3f45c-128">Service Fabric 노드</span><span class="sxs-lookup"><span data-stu-id="3f45c-128">Service Fabric nodes</span></span> |<span data-ttu-id="3f45c-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="3f45c-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="3f45c-130">Service Fabric Reliable Service 이벤트</span><span class="sxs-lookup"><span data-stu-id="3f45c-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="3f45c-131">Service Fabric 노드</span><span class="sxs-lookup"><span data-stu-id="3f45c-131">Service Fabric nodes</span></span> |<span data-ttu-id="3f45c-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="3f45c-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="3f45c-133">Windows 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="3f45c-133">Windows Event logs</span></span> |<span data-ttu-id="3f45c-134">Service Fabric 노드</span><span class="sxs-lookup"><span data-stu-id="3f45c-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="3f45c-135">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3f45c-135">Virtual Machines</span></span> <br> <span data-ttu-id="3f45c-136">웹 역할</span><span class="sxs-lookup"><span data-stu-id="3f45c-136">Web roles</span></span> <br> <span data-ttu-id="3f45c-137">작업자 역할</span><span class="sxs-lookup"><span data-stu-id="3f45c-137">Worker roles</span></span> |<span data-ttu-id="3f45c-138">WADWindowsEventLogsTable(Table Storage)</span><span class="sxs-lookup"><span data-stu-id="3f45c-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="3f45c-139">Windows ETW 로그</span><span class="sxs-lookup"><span data-stu-id="3f45c-139">Windows ETW logs</span></span> |<span data-ttu-id="3f45c-140">Service Fabric 노드</span><span class="sxs-lookup"><span data-stu-id="3f45c-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="3f45c-141">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3f45c-141">Virtual Machines</span></span> <br> <span data-ttu-id="3f45c-142">웹 역할</span><span class="sxs-lookup"><span data-stu-id="3f45c-142">Web roles</span></span> <br> <span data-ttu-id="3f45c-143">작업자 역할</span><span class="sxs-lookup"><span data-stu-id="3f45c-143">Worker roles</span></span> |<span data-ttu-id="3f45c-144">WADETWEventTable(Table Storage)</span><span class="sxs-lookup"><span data-stu-id="3f45c-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="3f45c-145">Azure 웹사이트에서 IIS 로그는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="3f45c-146">가상 컴퓨터의 경우 [Log Analytics 에이전트](log-analytics-azure-vm-extension.md)를 가상 컴퓨터에 설치하여 추가 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-146">For virtual machines, you have the option of installing the [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine to enable additional insights.</span></span> <span data-ttu-id="3f45c-147">IIS 로그 및 이벤트 로그를 분석할 수 있을 뿐만 아니라 구성 변경 추적, SQL 평가, 업데이트 평가 등 추가 분석을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-147">In addition to being able to analyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="3f45c-148">이벤트 로그 및 IIS 로그 컬렉션에 대한 Azure 진단을 가상 컴퓨터에서 사용</span><span class="sxs-lookup"><span data-stu-id="3f45c-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="3f45c-149">다음 절차를 사용하여 Microsoft Azure Portal에서 이벤트 로그 및 IIS 로그를 수집할 수 있도록 가상 컴퓨터에서 Azure 진단을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-149">Use the following procedure to enable Azure diagnostics in a virtual machine for Event Log and IIS log collection using the Microsoft Azure portal.</span></span>

### <a name="to-enable-azure-diagnostics-in-a-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="3f45c-150">Azure Portal을 통해 가상 컴퓨터에서 Azure 진단을 사용하도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="3f45c-150">To enable Azure diagnostics in a virtual machine with the Azure portal</span></span>
1. <span data-ttu-id="3f45c-151">가상 컴퓨터를 만들 때 VM 에이전트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-151">Install the VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="3f45c-152">가상 컴퓨터가 이미 있는 경우 VM 에이전트가 이미 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-152">If the virtual machine already exists, verify that the VM Agent is already installed.</span></span>

   * <span data-ttu-id="3f45c-153">Azure Portal에서 가상 컴퓨터로 이동하여 **옵션 구성**, **진단**을 차례로 선택한 다음 **상태**를 **설정**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-153">In the Azure portal, navigate to the virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** to **On**.</span></span>

     <span data-ttu-id="3f45c-154">완료되면 VM에서 Azure 진단 확장이 설치 및 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-154">Upon completion, the VM has the Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="3f45c-155">이 확장은 진단 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="3f45c-156">모니터링을 설정하고 기존 VM에 대한 이벤트 로깅을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="3f45c-157">VM 수준에서 진단을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-157">You can enable diagnostics at the VM level.</span></span> <span data-ttu-id="3f45c-158">진단을 사용하도록 설정한 다음 이벤트 로깅을 구성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-158">To enable diagnostics and then configure event logging, perform the following steps:</span></span>

   1. <span data-ttu-id="3f45c-159">VM을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-159">Select the VM.</span></span>
   2. <span data-ttu-id="3f45c-160">**모니터링**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="3f45c-161">**진단**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="3f45c-162">**상태**를 **켬**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-162">Set the **Status** to **ON**.</span></span>
   5. <span data-ttu-id="3f45c-163">수집하려는 각 진단 로그를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-163">Select each diagnostics log that you want to collect.</span></span>
   6. <span data-ttu-id="3f45c-164">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="3f45c-165">IIS 로그 및 이벤트 컬렉션에 대한 웹 역할에서 Azure 진단 사용</span><span class="sxs-lookup"><span data-stu-id="3f45c-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="3f45c-166">Azure 진단을 사용하도록 설정하는 일반적인 단계는 [클라우드 서비스에서 진단을 사용하도록 설정하는 방법](../cloud-services/cloud-services-dotnet-diagnostics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f45c-166">Refer to [How To Enable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="3f45c-167">아래 지침에서는 Log Analytics에서 사용하기 위해 이 정보를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-167">The instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="3f45c-168">Azure 진단을 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="3f45c-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="3f45c-169">IIS 로그는 기본적으로 scheduledTransferPeriod 전송 간격에 전송 하는 로그 데이터와 함께 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-169">IIS logs are stored by default, with log data transferred at the scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="3f45c-170">Windows 이벤트 로그는 기본적으로 전송되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="to-enable-diagnostics"></a><span data-ttu-id="3f45c-171">진단을 사용하도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="3f45c-171">To enable diagnostics</span></span>
<span data-ttu-id="3f45c-172">Windows 이벤트 로그를 사용하도록 설정하거나 scheduledTransferPeriod를 변경하려면 [4단계: 진단 구성 파일 만들기 및 확장 설치](../cloud-services/cloud-services-dotnet-diagnostics.md)에서처럼 XML 구성 파일(diagnostics.wadcfg)을 사용하여 Azure Diagnostics를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-172">To enable Windows Event Logs, or to change the scheduledTransferPeriod, configure Azure Diagnostics using the XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install the extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="3f45c-173">다음 예제 구성 파일은 응용 프로그램 및 시스템 로그에서 모든 이벤트 및 IIS 로그를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-173">The following example configuration file collects IIS Logs and all Events from the Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant to Web roles -->
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

<span data-ttu-id="3f45c-174">다음 예에서처럼 ConfigurationSettings이 저장소 계정을 지정하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-174">Ensure that your ConfigurationSettings specifies a storage account, as in the following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="3f45c-175">**AccountName** 및 **AccountKey** 값은 Azure Portal 저장소 계정 대시보드의 액세스 키 관리 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-175">The **AccountName** and **AccountKey** values are found in the Azure portal in the storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="3f45c-176">연결 문자열에 대한 프로토콜은 **https**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-176">The protocol for the connection string must be **https**.</span></span>

<span data-ttu-id="3f45c-177">업데이트된 진단 구성이 클라우드 서비스에 적용되고 Azure Storage에 진단을 기록한 후에는 Log Analytics를 구성할 준비가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-177">Once the updated diagnostic configuration is applied to your cloud service and it is writing diagnostics to Azure Storage, then you are ready to configure Log Analytics.</span></span>

## <a name="use-the-azure-portal-to-collect-logs-from-azure-storage"></a><span data-ttu-id="3f45c-178">Azure Portal을 사용하여 Azure Storage에서 로그 수집</span><span class="sxs-lookup"><span data-stu-id="3f45c-178">Use the Azure portal to collect logs from Azure Storage</span></span>
<span data-ttu-id="3f45c-179">Azure Portal을 사용하여 다음 Azure 서비스에 대한 로그를 수집하도록 Log Analytics를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-179">You can use the Azure portal to configure Log Analytics to collect the logs for the following Azure services:</span></span>

* <span data-ttu-id="3f45c-180">서비스 패브릭 클러스터</span><span class="sxs-lookup"><span data-stu-id="3f45c-180">Service Fabric clusters</span></span>
* <span data-ttu-id="3f45c-181">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="3f45c-181">Virtual Machines</span></span>
* <span data-ttu-id="3f45c-182">웹/작업자 역할</span><span class="sxs-lookup"><span data-stu-id="3f45c-182">Web/Worker Roles</span></span>

<span data-ttu-id="3f45c-183">Azure Portal에서 Log Analytics 작업 공간으로 이동하여 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-183">In the Azure portal, navigate to your Log Analytics workspace and perform the following tasks:</span></span>

1. <span data-ttu-id="3f45c-184">*저장소 계정 로그*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="3f45c-185">작업 *추가*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-185">Click the *Add* task</span></span>
3. <span data-ttu-id="3f45c-186">진단 로그를 포함하는 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-186">Select the Storage account that contains the diagnostics logs</span></span>
   * <span data-ttu-id="3f45c-187">이 계정은 클래식 저장소 계정 또는 Azure Resource Manager 저장소 계정일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="3f45c-188">로그를 수집할 대상 데이터 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-188">Select the Data Type you want to collect logs for</span></span>
   * <span data-ttu-id="3f45c-189">선택 항목은 IIS 로그, 이벤트, Syslog(Linux), ETW 로그 및 Service Fabric 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-189">The choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="3f45c-190">원본 값은 데이터 형식에 따라 자동으로 채워지며 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-190">The value for Source is automatically populated based on the data type and cannot be changed</span></span>
6. <span data-ttu-id="3f45c-191">확인을 클릭하여 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-191">Click OK to save the configuration</span></span>

<span data-ttu-id="3f45c-192">Log Analytics가 수집할 다른 저장소 계정과 데이터 형식에 대해 2-6단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics to collect.</span></span>

<span data-ttu-id="3f45c-193">약 30분 후에 Log Analytics의 저장소 계정에서 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-193">In approximately 30 minutes, you are able to see data from the storage account in Log Analytics.</span></span> <span data-ttu-id="3f45c-194">구성이 적용된 후에 저장소에 기록된 데이터만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-194">You will only see data that is written to storage after the configuration is applied.</span></span> <span data-ttu-id="3f45c-195">Log Analytics는 저장소 계정의 기존 데이터를 읽지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-195">Log Analytics does not read the pre-existing data from the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="3f45c-196">포털은 원본이 저장소 계정에 있는지 또는 새 데이터를 쓰는 중인지 확인하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-196">The portal does not validate that the Source exists in the storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="3f45c-197">PowerShell을 사용하여 이벤트 로그 및 IIS 로그 컬렉션에 대한 Azure 진단을 가상 컴퓨터에서 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="3f45c-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="3f45c-198">[Azure 진단을 인덱싱하도록 Log Analytics 구성](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) 단계를 사용하여 PowerShell을 통해 Table Storage에 기록된 Azure 진단을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-198">Use the steps in [Configuring Log Analytics to index Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) to use PowerShell to read from Azure diagnostics that are written to table storage.</span></span>

<span data-ttu-id="3f45c-199">Azure PowerShell을 사용하여 Azure 저장소에 기록된 이벤트를 보다 정확하게 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-199">Using Azure PowerShell you can more precisely specify the events that are written to Azure Storage.</span></span>
<span data-ttu-id="3f45c-200">자세한 내용은 [Azure 가상 컴퓨터에서 진단 사용](../virtual-machines-dotnet-diagnostics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f45c-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="3f45c-201">다음 PowerShell 스크립트를 사용하여 Azure 진단을 사용하도록 설정하고 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-201">You can enable and update Azure diagnostics using the following PowerShell script.</span></span>
<span data-ttu-id="3f45c-202">또한 사용자 지정 로깅 구성을 사용하여 이 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="3f45c-203">스크립트를 수정하여 저장소 계정, 서비스 이름 및 가상 컴퓨터 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-203">Modify the script to set the storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="3f45c-204">스크립트는 클래식 가상 컴퓨터에 대한 cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-204">The script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="3f45c-205">다음 스크립트 샘플을 검토하고 복사하며 필요에 따라 수정하고, 샘플을 PowerShell 스크립트 파일로 저장한 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-205">Review the following script sample, copy it, modify it as needed, save the sample as a PowerShell script file, and then run the script.</span></span>

```
    #Connect to Azure
    Add-AzureAccount

    # settings to change:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert to config format

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
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of the extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="3f45c-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3f45c-206">Next steps</span></span>
* <span data-ttu-id="3f45c-207">지원되는 Azure 서비스에 대해 [Azure 서비스에 대한 로그 및 메트릭 수집](log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="3f45c-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="3f45c-208">[솔루션을 사용하도록 설정](log-analytics-add-solutions.md) 하여 데이터에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-208">[Enable Solutions](log-analytics-add-solutions.md) to provide insight into the data.</span></span>
* <span data-ttu-id="3f45c-209">[검색 쿼리를 사용](log-analytics-log-searches.md) 하여 데이터를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="3f45c-209">[Use search queries](log-analytics-log-searches.md) to analyze the data.</span></span>
