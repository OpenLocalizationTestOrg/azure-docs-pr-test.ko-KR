---
title: "클라우드 서비스를 모니터링하는 방법 | Microsoft Docs"
description: "Azure 클래식 포털을 사용하여 Cloud Services를 모니터링하는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: 5c48d2fb-b8ea-420f-80df-7aebe2b66b1b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2015
ms.author: adegeo
ms.openlocfilehash: c369b22cf068a473343b006eb1b06fdd350d31db
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-monitor-cloud-services"></a><span data-ttu-id="93097-103">Cloud Services를 모니터링하는 방법</span><span class="sxs-lookup"><span data-stu-id="93097-103">How to Monitor Cloud Services</span></span>
[!INCLUDE [disclaimer](../../includes/disclaimer.md)]

<span data-ttu-id="93097-104">Azure 클래식 포털에서 Cloud Services의 `key` 성능 메트릭을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-104">You can monitor `key` performance metrics for your cloud services in the Azure classic portal.</span></span> <span data-ttu-id="93097-105">각 서비스 역할에 대해 모니터링 수준을 최소 및 자세히로 설정하고 모니터링 표시를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-105">You can set the level of monitoring to minimal and verbose for each service role, and can customize the monitoring displays.</span></span> <span data-ttu-id="93097-106">자세한 모니터링 데이터는 저장소 계정에 저장되며, 포털 외부에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-106">Verbose monitoring data is stored in a storage account, which you can access outside the portal.</span></span> 

<span data-ttu-id="93097-107">Azure 클래식 포털의 모니터링 표시는 매우 다양하게 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-107">Monitoring displays in the Azure classic portal are highly configurable.</span></span> <span data-ttu-id="93097-108">**모니터** 페이지의 메트릭 목록에서 모니터링할 메트릭을 선택하고 **모니터** 페이지 및 대시보드에서 메트릭 차트에 넣을 메트릭을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-108">You can choose the metrics you want to monitor in the metrics list on the **Monitor** page, and you can choose which metrics to plot in metrics charts on the **Monitor** page and the dashboard.</span></span> 

## <a name="concepts"></a><span data-ttu-id="93097-109">개념</span><span class="sxs-lookup"><span data-stu-id="93097-109">Concepts</span></span>
<span data-ttu-id="93097-110">기본적으로 최소 모니터링은 역할 인스턴스(가상 컴퓨터)에 대해 호스트 운영 체제에서 수집된 성능 카운터를 사용하여 새 클라우드 서비스에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="93097-110">By default, minimal monitoring is provided for a new cloud service using performance counters gathered from the host operating system for the roles instances (virtual machines).</span></span> <span data-ttu-id="93097-111">최소 메트릭은 CPU 비율, 데이터 입력, 데이터 출력, 디스크 읽기 처리량 및 디스크 쓰기 처리량으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="93097-111">The minimal metrics are limited to CPU Percentage, Data In, Data Out, Disk Read Throughput, and Disk Write Throughput.</span></span> <span data-ttu-id="93097-112">자세한 모니터링을 구성하면 가상 컴퓨터(역할 인스턴스) 내의 성능 데이터를 기반으로 추가 메트릭을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-112">By configuring verbose monitoring, you can receive additional metrics based on performance data within the virtual machines (role instances).</span></span> <span data-ttu-id="93097-113">자세한 정보 표시 메트릭을 사용하면 응용 프로그램 작동 중 발생하는 문제를 보다 자세히 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-113">The verbose metrics enable closer analysis of issues that occur during application operations.</span></span>

<span data-ttu-id="93097-114">기본적으로 역할 인스턴스의 성능 카운터 데이터는 역할 인스턴스에서 3분 간격으로 샘플링되고 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="93097-114">By default performance counter data from role instances is sampled and transferred from the role instance at 3-minute intervals.</span></span> <span data-ttu-id="93097-115">자세한 모니터링을 사용하는 경우 원시 성능 카운터 데이터가 각 역할 인스턴스 및 각 역할의 전체 역할 인스턴스에 대해 5분, 1시간 및 12시간 간격으로 집계됩니다.</span><span class="sxs-lookup"><span data-stu-id="93097-115">When you enable verbose monitoring, the raw performance counter data is aggregated for each role instance and across role instances for each role at intervals of 5 minutes, 1 hour, and 12 hours.</span></span> <span data-ttu-id="93097-116">집계된 데이터는 10일 후에 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="93097-116">The aggregated data is purged after 10 days.</span></span>

<span data-ttu-id="93097-117">자세한 모니터링을 사용하면 집계된 모니터링 데이터가 저장소 계정에 테이블로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="93097-117">After you enable verbose monitoring, the aggregated monitoring data is stored in tables in your storage account.</span></span> <span data-ttu-id="93097-118">역할에 자세한 모니터링을 사용하려면 저장소 계정에 연결되는 진단 연결 문자열을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-118">To enable verbose monitoring for a role, you must configure a diagnostics connection string that links to the storage account.</span></span> <span data-ttu-id="93097-119">역할에 따라 다른 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-119">You can use different storage accounts for different roles.</span></span>

<span data-ttu-id="93097-120">자세한 모니터링을 사용하면 데이터 저장소, 데이터 전송 및 저장소 트랜잭션과 관련된 저장소 비용이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-120">Enabling verbose monitoring increases your storage costs related to data storage, data transfer, and storage transactions.</span></span> <span data-ttu-id="93097-121">최소 모니터링에는 저장소 계정이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-121">Minimal monitoring does not require a storage account.</span></span> <span data-ttu-id="93097-122">최소 모니터링 수준에서 노출되는 메트릭에 대한 데이터는 모니터링 수준을 자세히로 설정하는 경우에도 저장소 계정에 저장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-122">The data for the metrics that are exposed at the minimal monitoring level are not stored in your storage account, even if you set the monitoring level to verbose.</span></span>

## <a name="how-to-configure-monitoring-for-cloud-services"></a><span data-ttu-id="93097-123">방법: Cloud Services에 대한 모니터링 구성</span><span class="sxs-lookup"><span data-stu-id="93097-123">How to: Configure monitoring for cloud services</span></span>
<span data-ttu-id="93097-124">다음 절차를 사용하여 Azure 클래식 포털에서 자세한 모니터링 또는 최소 모니터링을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-124">Use the following procedures to configure verbose or minimal monitoring in the Azure classic portal.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="93097-125">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="93097-125">Before you begin</span></span>
* <span data-ttu-id="93097-126">모니터링 데이터를 저장할 *클래식* 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="93097-126">Create a *classic* storage account to store the monitoring data.</span></span> <span data-ttu-id="93097-127">역할에 따라 다른 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-127">You can use different storage accounts for different roles.</span></span> <span data-ttu-id="93097-128">자세한 내용은 [저장소 계정을 만드는 방법](../storage/common/storage-create-storage-account.md#create-a-storage-account)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93097-128">For more information, see [How to create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="93097-129">클라우드 서비스 역할에 대해 Azure 진단을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-129">Enable Azure Diagnostics for your cloud service roles.</span></span> <span data-ttu-id="93097-130">[Cloud Services에 대한 진단 구성](cloud-services-dotnet-diagnostics.md)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="93097-130">See [Configuring Diagnostics for Cloud Services](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="93097-131">역할 구성에서 진단 연결 문자열이 있는지 확인하십시오.</span><span class="sxs-lookup"><span data-stu-id="93097-131">Ensure that the diagnostics connection string is present in the Role configuration.</span></span> <span data-ttu-id="93097-132">Azure 진단을 사용하도록 설정하고 역할 구성에 진단 연결 문자열을 포함할 때까지 자세한 정보 표시를 켤 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-132">You cannot turn on verbose monitoring until you enable Azure Diagnostics and include a diagnostics connection string in the Role configuration.</span></span>   

> [!NOTE]
> <span data-ttu-id="93097-133">Azure SDK 2.5 대상 프로젝트는 프로젝트 템플릿에 진단 연결 문자열을 자동으로 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-133">Projects targeting Azure SDK 2.5 did not automatically include the diagnostics connection string in the project template.</span></span> <span data-ttu-id="93097-134">이러한 프로젝트에 대해서는 역할 구성에 진단 연결 문자열을 수동으로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-134">For these projects, you need to manually add the diagnostics connection string to the Role configuration.</span></span>
> 
> 

<span data-ttu-id="93097-135">**역할 구성에 수동으로 진단 연결 문자열을 추가하려면**</span><span class="sxs-lookup"><span data-stu-id="93097-135">**To manually add diagnostics connection string to Role configuration**</span></span>

1. <span data-ttu-id="93097-136">Visual Studio에서 클라우드 서비스 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93097-136">Open the Cloud Service project in Visual Studio</span></span>
2. <span data-ttu-id="93097-137">**역할**을 두 번 클릭하여 역할 디자이너를 열고 **설정** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-137">Double-click on the **Role** to open the Role designer and select the **Settings** tab</span></span>
3. <span data-ttu-id="93097-138">**Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**이라는 설정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-138">Look for a setting named **Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**.</span></span> 
4. <span data-ttu-id="93097-139">이 설정이 없다면 **설정 추가** 단추를 클릭하여 구성에 추가한 다음 새로운 설정의 유형을 **ConnectionString**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-139">If this setting is not present, click on the **Add Setting** button to add it to the configuration and change the type for the new setting to **ConnectionString**</span></span>
5. <span data-ttu-id="93097-140">**...** 단추를 클릭하여 연결 문자열에 대한 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-140">Set the value for connection string the by clicking on the **...** button.</span></span> <span data-ttu-id="93097-141">그러면 저장소 계정을 선택할 수 있는 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="93097-141">This will open up a dialog allowing you to select a storage account.</span></span>
   
    ![Visual Studio 설정](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioDiagnosticsConnectionString.png)

### <a name="to-change-the-monitoring-level-to-verbose-or-minimal"></a><span data-ttu-id="93097-143">모니터링 수준을 자세히 또는 최소로 변경하려면</span><span class="sxs-lookup"><span data-stu-id="93097-143">To change the monitoring level to verbose or minimal</span></span>
1. <span data-ttu-id="93097-144">[Azure 클래식 포털](https://manage.windowsazure.com/)에서 클라우드 서비스 배포를 위한 **구성** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93097-144">In the [Azure classic portal](https://manage.windowsazure.com/), open the **Configure** page for the cloud service deployment.</span></span>
2. <span data-ttu-id="93097-145">**수준**에서 **자세히** 또는 **최소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-145">In **Level**, click **Verbose** or **Minimal**.</span></span> 
3. <span data-ttu-id="93097-146">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-146">Click **Save**.</span></span>

<span data-ttu-id="93097-147">자세한 모니터링을 켜면 해당 시간 내에 Azure 클래식 포털에 모니터링 데이터가 표시되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-147">After you turn on verbose monitoring, you should start seeing the monitoring data in the Azure classic portal within the hour.</span></span>

<span data-ttu-id="93097-148">원시 성능 카운터 데이터 및 집계된 모니터링 데이터는 역할에 대한 배포 ID로 한정되는 테이블로 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="93097-148">The raw performance counter data and aggregated monitoring data are stored in the storage account in tables qualified by the deployment ID for the roles.</span></span> 

## <a name="how-to-receive-alerts-for-cloud-service-metrics"></a><span data-ttu-id="93097-149">방법: 클라우드 서비스 메트릭에 대한 경고 받기</span><span class="sxs-lookup"><span data-stu-id="93097-149">How to: Receive alerts for cloud service metrics</span></span>
<span data-ttu-id="93097-150">클라우드 서비스 모니터링 메트릭을 기반으로 경고를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-150">You can receive alerts based on your cloud service monitoring metrics.</span></span> <span data-ttu-id="93097-151">Azure 클래식 포털의 **관리 서비스** 페이지에서 선택한 메트릭이 지정한 값에 도달하는 경우 경고를 트리거하는 규칙을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-151">On the **Management Services** page of the Azure classic portal, you can create a rule to trigger an alert when the metric you choose reaches a value that you specify.</span></span> <span data-ttu-id="93097-152">또한 경고가 트리거되면 메일을 보내도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-152">You can also choose to have email sent when the alert is triggered.</span></span> <span data-ttu-id="93097-153">자세한 내용은 [방법: Azure에서 경고 알림 받기 및 경고 규칙 관리](http://go.microsoft.com/fwlink/?LinkId=309356)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93097-153">For more information, see [How to: Receive Alert Notifications and Manage Alert Rules in Azure](http://go.microsoft.com/fwlink/?LinkId=309356).</span></span>

## <a name="how-to-add-metrics-to-the-metrics-table"></a><span data-ttu-id="93097-154">방법: 메트릭 테이블에 메트릭 추가</span><span class="sxs-lookup"><span data-stu-id="93097-154">How to: Add metrics to the metrics table</span></span>
1. <span data-ttu-id="93097-155">[Azure 클래식 포털](http://manage.windowsazure.com/)에서 클라우드 서비스에 대한 **모니터** 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93097-155">In the [Azure classic portal](http://manage.windowsazure.com/), open the **Monitor** page for the cloud service.</span></span>
   
    <span data-ttu-id="93097-156">기본적으로 메트릭 테이블에는 사용 가능한 메트릭의 하위 집합이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="93097-156">By default, the metrics table displays a subset of the available metrics.</span></span> <span data-ttu-id="93097-157">다음 그림에서는 역할 수준에서 집계된 데이터를 사용하여 Memory\Available MBytes 성능 카운터로 제한되는 클라우드 서비스에 대한 기본적인 자세한 정보 표시 메트릭을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93097-157">The illustration shows the default verbose metrics for a cloud service, which is limited to the Memory\Available MBytes performance counter, with data aggregated at the role level.</span></span> <span data-ttu-id="93097-158">**메트릭 추가** 를 사용하여 Azure 클래식 포털에서 모니터링할 추가 집계 및 역할 수준 메트릭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-158">Use **Add Metrics** to select additional aggregate and role-level metrics to monitor in the Azure classic portal.</span></span>
   
    ![자세한 표시](./media/cloud-services-how-to-monitor/CloudServices_DefaultVerboseDisplay.png)
2. <span data-ttu-id="93097-160">메트릭 테이블에 메트릭을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="93097-160">To add metrics to the metrics table:</span></span>
   
   1. <span data-ttu-id="93097-161">아래와 같이 **메트릭 추가**를 클릭하여 **메트릭 선택**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93097-161">Click **Add Metrics** to open **Choose Metrics**, shown below.</span></span>
      
       <span data-ttu-id="93097-162">사용 가능한 첫 번째 메트릭이 확장되어 사용 가능한 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="93097-162">The first available metric is expanded to show options that are available.</span></span> <span data-ttu-id="93097-163">각 메트릭에 대한 맨 위 옵션에는 모든 역할에 대해 집계된 모니터링 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="93097-163">For each metric, the top option displays aggregated monitoring data for all roles.</span></span> <span data-ttu-id="93097-164">또한 데이터를 표시할 개별 역할을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-164">In addition, you can choose individual roles to display data for.</span></span>
      
       ![메트릭 추가](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics.png)
   2. <span data-ttu-id="93097-166">표시할 메트릭을 선택하려면</span><span class="sxs-lookup"><span data-stu-id="93097-166">To select metrics to display</span></span>
      
      * <span data-ttu-id="93097-167">메트릭 옆에 있는 아래쪽 화살표를 클릭하여 모니터링 옵션을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-167">Click the down arrow by the metric to expand the monitoring options.</span></span>
      * <span data-ttu-id="93097-168">표시할 각 모니터링 옵션에 대한 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-168">Select the check box for each monitoring option you want to display.</span></span>
        
        <span data-ttu-id="93097-169">메트릭 테이블에 최대 50개의 메트릭을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-169">You can display up to 50 metrics in the metrics table.</span></span>
        
        > [!TIP]
        > <span data-ttu-id="93097-170">자세한 모니터링에서 메트릭 목록에는 수십 개의 메트릭이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-170">In verbose monitoring, the metrics list can contain dozens of metrics.</span></span> <span data-ttu-id="93097-171">스크롤 막대를 표시하려면 대화 상자의 오른쪽을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="93097-171">To display a scrollbar, hover over the right side of the dialog box.</span></span> <span data-ttu-id="93097-172">목록을 필터링하려면 아래와 같이 검색 아이콘을 클릭하고 검색 상자에 텍스트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-172">To filter the list, click the search icon, and enter text in the search box, as shown below.</span></span>
        > 
        > 
        
        ![메트릭 검색 추가](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics_Search.png)
3. <span data-ttu-id="93097-174">메트릭 선택을 마치면 확인(확인 표시)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-174">After you finish selecting metrics, click OK (checkmark).</span></span>
   
    <span data-ttu-id="93097-175">아래와 같이 선택한 메트릭이 메트릭 테이블에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="93097-175">The selected metrics are added to the metrics table, as shown below.</span></span>
   
    ![모니터 메트릭](./media/cloud-services-how-to-monitor/CloudServices_Monitor_UpdatedMetrics.png)
4. <span data-ttu-id="93097-177">메트릭 테이블에서 메트릭을 삭제하려면 메트릭을 클릭하여 선택한 다음 **메트릭 삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-177">To delete a metric from the metrics table, click the metric to select it, and then click **Delete Metric**.</span></span> <span data-ttu-id="93097-178">메트릭을 선택한 경우에만 **메트릭 삭제** 이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="93097-178">(You only see **Delete Metric** when you have a metric selected.)</span></span>

### <a name="to-add-custom-metrics-to-the-metrics-table"></a><span data-ttu-id="93097-179">메트릭 테이블에 사용자 지정 메트릭을 추가하려면</span><span class="sxs-lookup"><span data-stu-id="93097-179">To add custom metrics to the metrics table</span></span>
<span data-ttu-id="93097-180">**자세한 정보 표시** 모니터링 수준은 포털에서 모니터링할 수 있는 기본 메트릭 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-180">The **Verbose** monitoring level provides a list of default metrics that you can monitor on the portal.</span></span> <span data-ttu-id="93097-181">이외에도 포털을 통해 응용 프로그램에 의해 정의되는 모든 사용자 지정 또는 성능 카운터를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-181">In addition to these you can monitor any custom metrics or performance counters defined by your application through the portal.</span></span>

<span data-ttu-id="93097-182">다음 단계는 **자세한 정보 표시** 모니터링 수준을 켜고 사용자 지정 성능 카운터를 수집 및 전송하도록 응용 프로그램을 구성했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-182">The following steps assume that you have turned on **Verbose** monitoring level and have configured your application to collect and transfer custom performance counters.</span></span> 

<span data-ttu-id="93097-183">포털에서 사용자 지정 성능 카운터를 표시하려면 wad-control-container에서 구성을 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-183">To display the custom performance counters in the portal you need to update the configuration in wad-control-container:</span></span>

1. <span data-ttu-id="93097-184">진단 저장소 계정의 wad-control-container blob을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93097-184">Open the wad-control-container blob in your diagnostics storage account.</span></span> <span data-ttu-id="93097-185">Visual Studio 또는 다른 저장소 Explorer를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-185">You can use Visual Studio or any other storage explorer to do this.</span></span>
   
    ![Visual Studio 서버 Explorer](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioBlobExplorer.png)
2. <span data-ttu-id="93097-187">패턴 **DeploymentId/RoleName/RoleInstance**을 사용하여 blob 경로로 이동하여 역할 인스턴스에 대한 구성을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-187">Navigate the blob path using the pattern **DeploymentId/RoleName/RoleInstance** to find the configuration for your role instance.</span></span> 
   
    ![Visual Studio 저장소 Explorer](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioStorage.png)
3. <span data-ttu-id="93097-189">역할 인스턴스에 대한 구성 파일을 다운로드 하고 모든 사용자 지정 성능 카운터를 포함하도록 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-189">Download the configuration file for your role instance and update it to include any custom performance counters.</span></span> <span data-ttu-id="93097-190">예를 들어 *C 드라이브*에 대해 *Disk Write Bytes/sec*를 모니터링하려면 **PerformanceCounters\Subscriptions** 노드 아래에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-190">For example to monitor *Disk Write Bytes/sec* for the *C drive* add the following under **PerformanceCounters\Subscriptions** node</span></span>
   
    ```xml
    <PerformanceCounterConfiguration>
    <CounterSpecifier>\LogicalDisk(C:)\Disk Write Bytes/sec</CounterSpecifier>
    <SampleRateInSeconds>180</SampleRateInSeconds>
    </PerformanceCounterConfiguration>
    ```
4. <span data-ttu-id="93097-191">변경 내용을 저장하고 구성 파일을 동일한 위치에 업로드하여 blob 내 기존 파일을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="93097-191">Save the changes and upload the configuration file back to the same location overwriting the existing file in the blob.</span></span>
5. <span data-ttu-id="93097-192">Azure 클래식 포털 구성에서 자세한 정보 표시 모드를 설정/해제합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-192">Toggle to Verbose mode in the Azure classic portal configuration.</span></span> <span data-ttu-id="93097-193">이미 자세한 정보 표시 모드인 경우에는 최소로 전환한 다음 자세한 정보 표시로 돌아가야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-193">If you were in Verbose mode already you will have to toggle to minimal and back to verbose.</span></span>
6. <span data-ttu-id="93097-194">그러면 사용자 지정 성능 카운터가 **메트릭 추가** 대화 상자에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="93097-194">The custom performance counter will now be available in the **Add Metrics** dialog box.</span></span> 

## <a name="how-to-customize-the-metrics-chart"></a><span data-ttu-id="93097-195">방법: 메트릭 차트 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="93097-195">How to: Customize the metrics chart</span></span>
1. <span data-ttu-id="93097-196">메트릭 테이블에서 메트릭 차트에 넣을 메트릭을 최대 6개까지 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-196">In the metrics table, select up to 6 metrics to plot on the metrics chart.</span></span> <span data-ttu-id="93097-197">메트릭을 선택하려면 왼쪽에 있는 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-197">To select a metric, click the check box on its left side.</span></span> <span data-ttu-id="93097-198">메트릭 차트에서 메트릭을 제거하려면 메트릭 테이블에서 해당 확인란을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-198">To remove a metric from the metrics chart, clear its check box in the metrics table.</span></span>
   
    <span data-ttu-id="93097-199">메트릭 테이블에서 메트릭을 선택하면 메트릭이 메트릭 차트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="93097-199">As you select metrics in the metrics table, the metrics are added to the metrics chart.</span></span> <span data-ttu-id="93097-200">좁은 화면에서는 화면에 맞지 않는 메트릭 헤더가 **n more** 드롭다운 목록에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="93097-200">On a narrow display, an **n more** drop-down list contains metric headers that won't fit the display.</span></span>
2. <span data-ttu-id="93097-201">상대 값(각 메트릭에 대한 최종 값만)과 절대 값(Y축에 표시됨) 표시를 전환하려면 차트 맨 위에서 상대 또는 절대를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-201">To switch between displaying relative values (final value only for each metric) and absolute values (Y axis displayed), select Relative or Absolute at the top of the chart.</span></span>
   
    ![상대 또는 절대](./media/cloud-services-how-to-monitor/CloudServices_Monitor_RelativeAbsolute.png)
3. <span data-ttu-id="93097-203">메트릭 차트가 표시되는 시간 범위를 변경하려면 차트 맨 위에서 1시간, 24시간 또는 7일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-203">To change the time range the metrics chart displays, select 1 hour, 24 hours, or 7 days at the top of the chart.</span></span>
   
    ![모니터 표시 기간](./media/cloud-services-how-to-monitor/CloudServices_Monitor_DisplayPeriod.png)
   
    <span data-ttu-id="93097-205">대시보드 메트릭 차트에서 메트릭을 넣는 방법은 다양합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-205">On the dashboard metrics chart, the method for plotting metrics is different.</span></span> <span data-ttu-id="93097-206">표준 메트릭 집합을 사용할 수 있으며, 메트릭 헤더를 선택하여 메트릭을 추가하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-206">A standard set of metrics is available, and metrics are added or removed by selecting the metric header.</span></span>

### <a name="to-customize-the-metrics-chart-on-the-dashboard"></a><span data-ttu-id="93097-207">대시보드에서 메트릭 차트를 사용자 지정하려면</span><span class="sxs-lookup"><span data-stu-id="93097-207">To customize the metrics chart on the dashboard</span></span>
1. <span data-ttu-id="93097-208">클라우드 서비스에 대한 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93097-208">Open the dashboard for the cloud service.</span></span>
2. <span data-ttu-id="93097-209">차트에서 메트릭을 추가하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-209">Add or remove metrics from the chart:</span></span>
   
   * <span data-ttu-id="93097-210">새 메트릭을 넣으려면 차트 헤더에서 메트릭에 대한 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-210">To plot a new metric, select the check box for the metric in the chart headers.</span></span> <span data-ttu-id="93097-211">좁은 화면에서는 ***n*??메트릭** 옆에 있는 아래쪽 화살표를 클릭하여 차트 헤더 영역에 표시할 수 없는 메트릭을 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-211">On a narrow display, click the down arrow by ***n*??metrics** to plot a metric the chart header area can't display.</span></span>
   * <span data-ttu-id="93097-212">차트에 그려진 메트릭을 삭제하려면 헤더 옆에 있는 확인란을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-212">To delete a metric that is plotted on the chart, clear the check box by its header.</span></span>
   
3. <span data-ttu-id="93097-213">**상대** 및 **절대** 표시를 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-213">Switch between **Relative** and **Absolute** displays.</span></span>
4. <span data-ttu-id="93097-214">1시간, 24시간 또는 7일의 데이터를 선택하여 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="93097-214">Choose 1 hour, 24 hours, or 7 days of data to display.</span></span>

## <a name="how-to-access-verbose-monitoring-data-outside-the-azure-classic-portal"></a><span data-ttu-id="93097-215">방법: Azure 클래식 포털 외부에서 자세한 모니터링 데이터 액세스</span><span class="sxs-lookup"><span data-stu-id="93097-215">How to: Access verbose monitoring data outside the Azure classic portal</span></span>
<span data-ttu-id="93097-216">자세한 모니터링 데이터는 각 영역에 대해 지정한 저장소 계정에 테이블로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="93097-216">Verbose monitoring data is stored in tables in the storage accounts that you specify for each role.</span></span> <span data-ttu-id="93097-217">각 클라우드 서비스 배포에서 역할에 대해 6개의 테이블이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="93097-217">For each cloud service deployment, six tables are created for the role.</span></span> <span data-ttu-id="93097-218">각각(5분, 1시간 및 12시간)에 대해 두 개의 테이블이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="93097-218">Two tables are created for each (5 minutes, 1 hour, and 12 hours).</span></span> <span data-ttu-id="93097-219">이러한 테이블 중 하나에는 역할 수준 집계가 저장되고, 다른 테이블에는 역할 인스턴스에 대한 집계가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="93097-219">One of these tables stores role-level aggregations; the other table stores aggregations for role instances.</span></span> 

<span data-ttu-id="93097-220">테이블 이름의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93097-220">The table names have the following format:</span></span>

```
WAD*deploymentID*PT*aggregation_interval*[R|RI]Table
```

<span data-ttu-id="93097-221">위치:</span><span class="sxs-lookup"><span data-stu-id="93097-221">where:</span></span>

* <span data-ttu-id="93097-222">*deploymentID*는 클라우드 서비스 배포에 할당된 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="93097-222">*deploymentID* is the GUID assigned to the cloud service deployment</span></span>
* <span data-ttu-id="93097-223">*aggregation_interval* = 5M, 1H 또는 12H</span><span class="sxs-lookup"><span data-stu-id="93097-223">*aggregation_interval* = 5M, 1H, or 12H</span></span>
* <span data-ttu-id="93097-224">역할 수준 집계 = R</span><span class="sxs-lookup"><span data-stu-id="93097-224">role-level aggregations = R</span></span>
* <span data-ttu-id="93097-225">역할 인스턴스에 대한 집계 = RI</span><span class="sxs-lookup"><span data-stu-id="93097-225">aggregations for role instances = RI</span></span>

<span data-ttu-id="93097-226">예를 들어 다음 테이블에는 1시간 간격으로 집계된 자세한 모니터링 데이터가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="93097-226">For example, the following tables would store verbose monitoring data aggregated at 1-hour intervals:</span></span>

```
WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRTable (hourly aggregations for the role)

WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRITable (hourly aggregations for role instances)
```
