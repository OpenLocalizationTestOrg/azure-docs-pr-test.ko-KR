---
title: "aaaHow toomonitor 클라우드 서비스 | Microsoft Docs"
description: "Toomonitor hello Azure 클래식 포털을 사용 하 여 서비스를 클라우드 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: ee98c56e0b98b85d75a5c1d796800069c4f06d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-cloud-services"></a><span data-ttu-id="2a430-103">TooMonitor 클라우드 서비스 하는 방법</span><span class="sxs-lookup"><span data-stu-id="2a430-103">How tooMonitor Cloud Services</span></span>
[!INCLUDE [disclaimer](../../includes/disclaimer.md)]

<span data-ttu-id="2a430-104">모니터링할 수 있습니다 `key` hello Azure 클래식 포털에서에서 클라우드 서비스에 대 한 성능 메트릭을 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-104">You can monitor `key` performance metrics for your cloud services in hello Azure classic portal.</span></span> <span data-ttu-id="2a430-105">표시 되는 모니터링 하는 hello를 사용자 지정할 수 있습니다 및 toominimal 모니터링의 수준과 각 서비스 역할에 대 한 자세한 정보 표시 hello를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-105">You can set hello level of monitoring toominimal and verbose for each service role, and can customize hello monitoring displays.</span></span> <span data-ttu-id="2a430-106">자세한 정보 표시 모니터링 데이터 hello 포털 외부에 액세스할 수 있는 저장소 계정에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-106">Verbose monitoring data is stored in a storage account, which you can access outside hello portal.</span></span> 

<span data-ttu-id="2a430-107">Hello Azure 클래식 포털에서에서 모니터링 디스플레이 매우 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-107">Monitoring displays in hello Azure classic portal are highly configurable.</span></span> <span data-ttu-id="2a430-108">Hello 메트릭을 선택할 수 있습니다 toomonitor hello hello 메트릭 목록에서 원하는 **모니터** 페이지에서 선택할 수도 있습니다는 메트릭 tooplot 메트릭 차트 hello에 있는 **모니터** 페이지 및 hello 대시보드에.</span><span class="sxs-lookup"><span data-stu-id="2a430-108">You can choose hello metrics you want toomonitor in hello metrics list on hello **Monitor** page, and you can choose which metrics tooplot in metrics charts on hello **Monitor** page and hello dashboard.</span></span> 

## <a name="concepts"></a><span data-ttu-id="2a430-109">개념</span><span class="sxs-lookup"><span data-stu-id="2a430-109">Concepts</span></span>
<span data-ttu-id="2a430-110">기본적으로 최소 모니터링 hello 역할 인스턴스 (가상 컴퓨터)에 대 한 hello 호스트 운영 체제에서 수집 된 성능 카운터를 사용 하 여 새 클라우드 서비스에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-110">By default, minimal monitoring is provided for a new cloud service using performance counters gathered from hello host operating system for hello roles instances (virtual machines).</span></span> <span data-ttu-id="2a430-111">hello 최소 메트릭은 제한 tooCPU 비율, 데이터, 데이터 출력, 디스크 읽기 처리량 및 디스크 쓰기 처리량입니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-111">hello minimal metrics are limited tooCPU Percentage, Data In, Data Out, Disk Read Throughput, and Disk Write Throughput.</span></span> <span data-ttu-id="2a430-112">자세한 정보 표시 모니터링을 구성 하 여 hello 가상 컴퓨터 (역할 인스턴스) 내에서 성능 데이터를 기반으로 추적을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-112">By configuring verbose monitoring, you can receive additional metrics based on performance data within hello virtual machines (role instances).</span></span> <span data-ttu-id="2a430-113">자세한 정보 표시 메트릭을 hello 응용 프로그램 작업 중 발생 하는 문제를 보다 자세하게 분석을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-113">hello verbose metrics enable closer analysis of issues that occur during application operations.</span></span>

<span data-ttu-id="2a430-114">기본적으로 역할 인스턴스에서 성능 카운터 데이터 샘플링 하 고 hello 역할 인스턴스에서 3 분 간격으로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-114">By default performance counter data from role instances is sampled and transferred from hello role instance at 3-minute intervals.</span></span> <span data-ttu-id="2a430-115">자세한 정보 표시 모니터링을 사용 하도록 설정 하면 hello 원시 성능 카운터 데이터는 1 시간 및 12 시간 동안 5 분 간격으로 각 역할에 대 한 역할 인스턴스 및 각 역할 인스턴스에 대 한 집계 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-115">When you enable verbose monitoring, hello raw performance counter data is aggregated for each role instance and across role instances for each role at intervals of 5 minutes, 1 hour, and 12 hours.</span></span> <span data-ttu-id="2a430-116">hello 집계 된 데이터는 제거 10 일 후.</span><span class="sxs-lookup"><span data-stu-id="2a430-116">hello aggregated data is purged after 10 days.</span></span>

<span data-ttu-id="2a430-117">집계 hello 자세한 정보 표시 모니터링을 사용 하면 저장소 계정의 테이블에 모니터링 데이터가 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-117">After you enable verbose monitoring, hello aggregated monitoring data is stored in tables in your storage account.</span></span> <span data-ttu-id="2a430-118">tooenable 자세한 정보 표시 하는 역할에 대 한 모니터링을 toohello 저장소 계정을 연결 하는 진단 연결 문자열을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-118">tooenable verbose monitoring for a role, you must configure a diagnostics connection string that links toohello storage account.</span></span> <span data-ttu-id="2a430-119">역할에 따라 다른 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-119">You can use different storage accounts for different roles.</span></span>

<span data-ttu-id="2a430-120">저장소 비용 toodata 저장소, 데이터 전송 및 저장소 트랜잭션 관련 된 자세한 정보 표시 모니터링 증가 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-120">Enabling verbose monitoring increases your storage costs related toodata storage, data transfer, and storage transactions.</span></span> <span data-ttu-id="2a430-121">최소 모니터링에는 저장소 계정이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-121">Minimal monitoring does not require a storage account.</span></span> <span data-ttu-id="2a430-122">hello tooverbose 수준 모니터링을 설정 하는 경우에 hello 데이터 hello 최소 모니터링 수준에 노출 되는 hello 메트릭에 대 한 저장소 계정에 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-122">hello data for hello metrics that are exposed at hello minimal monitoring level are not stored in your storage account, even if you set hello monitoring level tooverbose.</span></span>

## <a name="how-to-configure-monitoring-for-cloud-services"></a><span data-ttu-id="2a430-123">방법: Cloud Services에 대한 모니터링 구성</span><span class="sxs-lookup"><span data-stu-id="2a430-123">How to: Configure monitoring for cloud services</span></span>
<span data-ttu-id="2a430-124">다음 프로시저 tooconfigure hello Azure 클래식 포털에서에서 모니터링 최소 또는 자세한 정보는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-124">Use hello following procedures tooconfigure verbose or minimal monitoring in hello Azure classic portal.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="2a430-125">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="2a430-125">Before you begin</span></span>
* <span data-ttu-id="2a430-126">만들기는 *클래식* 저장소 계정 toostore hello 데이터를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-126">Create a *classic* storage account toostore hello monitoring data.</span></span> <span data-ttu-id="2a430-127">역할에 따라 다른 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-127">You can use different storage accounts for different roles.</span></span> <span data-ttu-id="2a430-128">자세한 내용은 참조 [어떻게 toocreate 저장소 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-128">For more information, see [How toocreate a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="2a430-129">클라우드 서비스 역할에 대해 Azure 진단을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-129">Enable Azure Diagnostics for your cloud service roles.</span></span> <span data-ttu-id="2a430-130">[Cloud Services에 대한 진단 구성](cloud-services-dotnet-diagnostics.md)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="2a430-130">See [Configuring Diagnostics for Cloud Services](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="2a430-131">Hello 진단 연결 문자열 hello 역할 구성에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-131">Ensure that hello diagnostics connection string is present in hello Role configuration.</span></span> <span data-ttu-id="2a430-132">Azure 진단을 사용 하도록 설정 하 고 진단 연결 문자열 hello 역할 구성에 포함 될 때까지 자세한 정보 표시 모니터링 켤 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-132">You cannot turn on verbose monitoring until you enable Azure Diagnostics and include a diagnostics connection string in hello Role configuration.</span></span>   

> [!NOTE]
> <span data-ttu-id="2a430-133">Azure SDK 2.5를 대상으로 하는 프로젝트 자동으로에 포함 하지 않은 hello 진단 연결 문자열 hello 프로젝트 템플릿을 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-133">Projects targeting Azure SDK 2.5 did not automatically include hello diagnostics connection string in hello project template.</span></span> <span data-ttu-id="2a430-134">이러한 프로젝트에 대해 toomanually 해야 hello 진단 연결 문자열 toohello 역할 구성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-134">For these projects, you need toomanually add hello diagnostics connection string toohello Role configuration.</span></span>
> 
> 

<span data-ttu-id="2a430-135">**toomanually 진단 연결 문자열 tooRole 구성 추가**</span><span class="sxs-lookup"><span data-stu-id="2a430-135">**toomanually add diagnostics connection string tooRole configuration**</span></span>

1. <span data-ttu-id="2a430-136">Visual Studio에서 열기 hello 클라우드 서비스 프로젝트</span><span class="sxs-lookup"><span data-stu-id="2a430-136">Open hello Cloud Service project in Visual Studio</span></span>
2. <span data-ttu-id="2a430-137">Hello에 두 번 클릭 **역할** tooopen 역할 디자이너 hello 선택한 hello **설정을** 탭</span><span class="sxs-lookup"><span data-stu-id="2a430-137">Double-click on hello **Role** tooopen hello Role designer and select hello **Settings** tab</span></span>
3. <span data-ttu-id="2a430-138">**Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**이라는 설정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-138">Look for a setting named **Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**.</span></span> 
4. <span data-ttu-id="2a430-139">이 설정이 없으면 클릭 hello **설정 추가** 단추 tooadd 것 toohello 구성과 변경 hello hello 새 설정이 너무에 대 한 형식을**ConnectionString**</span><span class="sxs-lookup"><span data-stu-id="2a430-139">If this setting is not present, click on hello **Add Setting** button tooadd it toohello configuration and change hello type for hello new setting too**ConnectionString**</span></span>
5. <span data-ttu-id="2a430-140">Hello를 클릭 하 여 연결 문자열 hello에 대 한 hello 값을 설정 **...**  단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-140">Set hello value for connection string hello by clicking on hello **...** button.</span></span> <span data-ttu-id="2a430-141">그러면 열립니다 tooselect을 수 있는 대화 상자를 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="2a430-141">This will open up a dialog allowing you tooselect a storage account.</span></span>
   
    ![Visual Studio 설정](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioDiagnosticsConnectionString.png)

### <a name="toochange-hello-monitoring-level-tooverbose-or-minimal"></a><span data-ttu-id="2a430-143">모니터링 수준 tooverbose toochange hello / 최소</span><span class="sxs-lookup"><span data-stu-id="2a430-143">toochange hello monitoring level tooverbose or minimal</span></span>
1. <span data-ttu-id="2a430-144">Hello에 [Azure 클래식 포털](https://manage.windowsazure.com/)개방형 hello **구성** hello 클라우드 서비스 배포에 대 한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-144">In hello [Azure classic portal](https://manage.windowsazure.com/), open hello **Configure** page for hello cloud service deployment.</span></span>
2. <span data-ttu-id="2a430-145">**수준**에서 **자세히** 또는 **최소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-145">In **Level**, click **Verbose** or **Minimal**.</span></span> 
3. <span data-ttu-id="2a430-146">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-146">Click **Save**.</span></span>

<span data-ttu-id="2a430-147">자세한 정보 표시 모니터링을 설정 하면 후 hello 시간이 내의 hello Azure 클래식 포털에서에서 데이터를 모니터링 하는 hello 보기를 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-147">After you turn on verbose monitoring, you should start seeing hello monitoring data in hello Azure classic portal within hello hour.</span></span>

<span data-ttu-id="2a430-148">hello 원시 성능 카운터 데이터 및 모니터링 데이터를 집계 된 hello 역할에 대 한 배포 ID hello로 정규화 된 테이블의 hello 저장소 계정에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-148">hello raw performance counter data and aggregated monitoring data are stored in hello storage account in tables qualified by hello deployment ID for hello roles.</span></span> 

## <a name="how-to-receive-alerts-for-cloud-service-metrics"></a><span data-ttu-id="2a430-149">방법: 클라우드 서비스 메트릭에 대한 경고 받기</span><span class="sxs-lookup"><span data-stu-id="2a430-149">How to: Receive alerts for cloud service metrics</span></span>
<span data-ttu-id="2a430-150">클라우드 서비스 모니터링 메트릭을 기반으로 경고를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-150">You can receive alerts based on your cloud service monitoring metrics.</span></span> <span data-ttu-id="2a430-151">Hello에 **관리 서비스** 페이지 hello Azure 클래식 포털을 만들 수 있습니다 규칙 tootrigger 경고 hello 메트릭을 선택 하면 사용자가 지정한 값에 도달 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="2a430-151">On hello **Management Services** page of hello Azure classic portal, you can create a rule tootrigger an alert when hello metric you choose reaches a value that you specify.</span></span> <span data-ttu-id="2a430-152">또한 hello 경고가 트리거될 때 전송 toohave 전자 메일을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-152">You can also choose toohave email sent when hello alert is triggered.</span></span> <span data-ttu-id="2a430-153">자세한 내용은 [방법: Azure에서 경고 알림 받기 및 경고 규칙 관리](http://go.microsoft.com/fwlink/?LinkId=309356)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a430-153">For more information, see [How to: Receive Alert Notifications and Manage Alert Rules in Azure](http://go.microsoft.com/fwlink/?LinkId=309356).</span></span>

## <a name="how-to-add-metrics-toohello-metrics-table"></a><span data-ttu-id="2a430-154">방법: 메트릭 toohello 메트릭 테이블 추가</span><span class="sxs-lookup"><span data-stu-id="2a430-154">How to: Add metrics toohello metrics table</span></span>
1. <span data-ttu-id="2a430-155">Hello에 [Azure 클래식 포털](http://manage.windowsazure.com/)개방형 hello **모니터** hello 클라우드 서비스에 대 한 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-155">In hello [Azure classic portal](http://manage.windowsazure.com/), open hello **Monitor** page for hello cloud service.</span></span>
   
    <span data-ttu-id="2a430-156">기본적으로 hello 메트릭 테이블 hello 사용 가능한 메트릭의 하위 집합을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-156">By default, hello metrics table displays a subset of hello available metrics.</span></span> <span data-ttu-id="2a430-157">hello 그림 hello 역할 수준에서 집계 데이터와 함께 기본 hello 제한 toohello Memory\Available MBytes 성능 카운터는 클라우드 서비스에 대 한 자세한 정보 표시 메트릭을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-157">hello illustration shows hello default verbose metrics for a cloud service, which is limited toohello Memory\Available MBytes performance counter, with data aggregated at hello role level.</span></span> <span data-ttu-id="2a430-158">사용 하 여 **메트릭 추가** tooselect 추가 집계 및에 대 한 역할 수준 메트릭 toomonitor hello Azure 클래식 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-158">Use **Add Metrics** tooselect additional aggregate and role-level metrics toomonitor in hello Azure classic portal.</span></span>
   
    ![자세한 표시](./media/cloud-services-how-to-monitor/CloudServices_DefaultVerboseDisplay.png)
2. <span data-ttu-id="2a430-160">tooadd 메트릭 toohello 메트릭 테이블:</span><span class="sxs-lookup"><span data-stu-id="2a430-160">tooadd metrics toohello metrics table:</span></span>
   
   1. <span data-ttu-id="2a430-161">클릭 **메트릭 추가** tooopen **메트릭 선택**, 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-161">Click **Add Metrics** tooopen **Choose Metrics**, shown below.</span></span>
      
       <span data-ttu-id="2a430-162">첫 번째 사용 가능한 메트릭을 hello에는 사용할 수 있는 확장 된 tooshow 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-162">hello first available metric is expanded tooshow options that are available.</span></span> <span data-ttu-id="2a430-163">Hello 위쪽 옵션 각 메트릭에 대 한 모든 역할에 대해 집계 모니터링 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-163">For each metric, hello top option displays aggregated monitoring data for all roles.</span></span> <span data-ttu-id="2a430-164">또한 toodisplay 데이터에 대 한 개별 역할을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-164">In addition, you can choose individual roles toodisplay data for.</span></span>
      
       ![메트릭 추가](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics.png)
   2. <span data-ttu-id="2a430-166">tooselect 메트릭 toodisplay</span><span class="sxs-lookup"><span data-stu-id="2a430-166">tooselect metrics toodisplay</span></span>
      
      * <span data-ttu-id="2a430-167">모니터링 옵션 hello 메트릭 tooexpand hello 하 여 hello 아래쪽 화살표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-167">Click hello down arrow by hello metric tooexpand hello monitoring options.</span></span>
      * <span data-ttu-id="2a430-168">각각에 대 한 확인란을 선택 hello toodisplay 원하는 옵션을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-168">Select hello check box for each monitoring option you want toodisplay.</span></span>
        
        <span data-ttu-id="2a430-169">Hello 메트릭 표에 too50 메트릭을를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-169">You can display up too50 metrics in hello metrics table.</span></span>
        
        > [!TIP]
        > <span data-ttu-id="2a430-170">자세한 정보 표시 모니터링 hello 메트릭 목록 메트릭 수십 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-170">In verbose monitoring, hello metrics list can contain dozens of metrics.</span></span> <span data-ttu-id="2a430-171">scrollbar toodisplay hello hello 대화 상자의 오른쪽 위로 가져갑니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-171">toodisplay a scrollbar, hover over hello right side of hello dialog box.</span></span> <span data-ttu-id="2a430-172">toofilter hello 목록 hello 검색 아이콘을 클릭 하 고 아래와 같이 hello 검색 상자에 텍스트를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-172">toofilter hello list, click hello search icon, and enter text in hello search box, as shown below.</span></span>
        > 
        > 
        
        ![메트릭 검색 추가](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics_Search.png)
3. <span data-ttu-id="2a430-174">메트릭 선택을 마치면 확인(확인 표시)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-174">After you finish selecting metrics, click OK (checkmark).</span></span>
   
    <span data-ttu-id="2a430-175">hello 선택한 메트릭을 추가 하 toohello 메트릭 테이블에서 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-175">hello selected metrics are added toohello metrics table, as shown below.</span></span>
   
    ![모니터 메트릭](./media/cloud-services-how-to-monitor/CloudServices_Monitor_UpdatedMetrics.png)
4. <span data-ttu-id="2a430-177">toodelete hello 메트릭 테이블에서 메트릭을 클릭 hello 메트릭 tooselect, 클릭 **메트릭을 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-177">toodelete a metric from hello metrics table, click hello metric tooselect it, and then click **Delete Metric**.</span></span> <span data-ttu-id="2a430-178">메트릭을 선택한 경우에만 **메트릭 삭제** 이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-178">(You only see **Delete Metric** when you have a metric selected.)</span></span>

### <a name="tooadd-custom-metrics-toohello-metrics-table"></a><span data-ttu-id="2a430-179">tooadd 사용자 지정 메트릭 toohello 메트릭 테이블</span><span class="sxs-lookup"><span data-stu-id="2a430-179">tooadd custom metrics toohello metrics table</span></span>
<span data-ttu-id="2a430-180">hello **Verbose** hello 포털에서 모니터링할 수 있는 기본 메트릭 목록을 제공 수준을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-180">hello **Verbose** monitoring level provides a list of default metrics that you can monitor on hello portal.</span></span> <span data-ttu-id="2a430-181">또한 toothese 모든 사용자 지정 메트릭 또는 hello 포털을 통해 응용 프로그램에서 정의 하는 성능 카운터를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-181">In addition toothese you can monitor any custom metrics or performance counters defined by your application through hello portal.</span></span>

<span data-ttu-id="2a430-182">hello 다음 단계에서는 가정를 설정한 **Verbose** 모니터링 수준 및 응용 프로그램 toocollect 및 전송 사용자 지정 성능 카운터의 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-182">hello following steps assume that you have turned on **Verbose** monitoring level and have configured your application toocollect and transfer custom performance counters.</span></span> 

<span data-ttu-id="2a430-183">toodisplay hello 사용자 지정 성능 카운터에 hello wad 컨트롤 컨테이너에서 hello 구성 tooupdate 필요한 포털:</span><span class="sxs-lookup"><span data-stu-id="2a430-183">toodisplay hello custom performance counters in hello portal you need tooupdate hello configuration in wad-control-container:</span></span>

1. <span data-ttu-id="2a430-184">진단 저장소 계정에서 hello wad 컨트롤 컨테이너 blob을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-184">Open hello wad-control-container blob in your diagnostics storage account.</span></span> <span data-ttu-id="2a430-185">Visual Studio 또는 기타 저장소 탐색기 toodo 사용할 수 있습니다이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-185">You can use Visual Studio or any other storage explorer toodo this.</span></span>
   
    ![Visual Studio 서버 Explorer](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioBlobExplorer.png)
2. <span data-ttu-id="2a430-187">Hello 패턴을 사용 하 여 hello blob 경로 탐색 **DeploymentId/RoleName/RoleInstance** 역할 인스턴스에 대 한 toofind hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-187">Navigate hello blob path using hello pattern **DeploymentId/RoleName/RoleInstance** toofind hello configuration for your role instance.</span></span> 
   
    ![Visual Studio 저장소 Explorer](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioStorage.png)
3. <span data-ttu-id="2a430-189">역할 인스턴스에 대 한 hello 구성 파일을 다운로드 하 고 업데이트 tooinclude 모든 사용자 지정 성능 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-189">Download hello configuration file for your role instance and update it tooinclude any custom performance counters.</span></span> <span data-ttu-id="2a430-190">예를 들어 toomonitor *Disk Write Bytes/sec* hello에 대 한 *C 드라이브* hello 다음에서 추가 **PerformanceCounters\Subscriptions** 노드</span><span class="sxs-lookup"><span data-stu-id="2a430-190">For example toomonitor *Disk Write Bytes/sec* for hello *C drive* add hello following under **PerformanceCounters\Subscriptions** node</span></span>
   
    ```xml
    <PerformanceCounterConfiguration>
    <CounterSpecifier>\LogicalDisk(C:)\Disk Write Bytes/sec</CounterSpecifier>
    <SampleRateInSeconds>180</SampleRateInSeconds>
    </PerformanceCounterConfiguration>
    ```
4. <span data-ttu-id="2a430-191">Hello 변경 내용 및 업로드 hello 구성 파일 백 toohello 저장 hello blob에서 기존 파일을 hello 동일한 위치 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-191">Save hello changes and upload hello configuration file back toohello same location overwriting hello existing file in hello blob.</span></span>
5. <span data-ttu-id="2a430-192">Azure 클래식 포털 구성 hello에 tooVerbose 모드를 설정/해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-192">Toggle tooVerbose mode in hello Azure classic portal configuration.</span></span> <span data-ttu-id="2a430-193">자세한 정보 표시 모드에 이미 있던 경우 tootoggle toominimal 및 뒤로 tooverbose를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-193">If you were in Verbose mode already you will have tootoggle toominimal and back tooverbose.</span></span>
6. <span data-ttu-id="2a430-194">사용자 지정 성능 카운터를 hello 이제 hello에 사용할 수 **메트릭 추가** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="2a430-194">hello custom performance counter will now be available in hello **Add Metrics** dialog box.</span></span> 

## <a name="how-to-customize-hello-metrics-chart"></a><span data-ttu-id="2a430-195">방법: hello 메트릭 차트를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="2a430-195">How to: Customize hello metrics chart</span></span>
1. <span data-ttu-id="2a430-196">Hello 메트릭 표에 hello 메트릭 차트에 메트릭 tooplot too6 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-196">In hello metrics table, select up too6 metrics tooplot on hello metrics chart.</span></span> <span data-ttu-id="2a430-197">메트릭을 tooselect 왼쪽된 면에 hello 확인란을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-197">tooselect a metric, click hello check box on its left side.</span></span> <span data-ttu-id="2a430-198">tooremove hello 메트릭 차트에서 메트릭을 hello 메트릭 테이블에서 해당 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-198">tooremove a metric from hello metrics chart, clear its check box in hello metrics table.</span></span>
   
    <span data-ttu-id="2a430-199">메트릭 hello 메트릭 테이블을 선택 하면 hello 메트릭은 toohello 메트릭 차트를 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-199">As you select metrics in hello metrics table, hello metrics are added toohello metrics chart.</span></span> <span data-ttu-id="2a430-200">좁은 디스플레이에 **자세한 n** 드롭 다운 목록 hello 디스플레이 맞지 않는 메트릭 헤더를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-200">On a narrow display, an **n more** drop-down list contains metric headers that won't fit hello display.</span></span>
2. <span data-ttu-id="2a430-201">tooswitch 상대 값 (각 메트릭에 대해만 최종 값)과 절대 값 (Y 축 표시), 표시 간의 상대 또는 절대 hello 차트의 hello 위쪽을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-201">tooswitch between displaying relative values (final value only for each metric) and absolute values (Y axis displayed), select Relative or Absolute at hello top of hello chart.</span></span>
   
    ![상대 또는 절대](./media/cloud-services-how-to-monitor/CloudServices_Monitor_RelativeAbsolute.png)
3. <span data-ttu-id="2a430-203">toochange hello 시간 범위 hello 메트릭 차트 hello 차트의 위쪽 hello에 1 시간, 24 시간 또는 7 일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-203">toochange hello time range hello metrics chart displays, select 1 hour, 24 hours, or 7 days at hello top of hello chart.</span></span>
   
    ![모니터 표시 기간](./media/cloud-services-how-to-monitor/CloudServices_Monitor_DisplayPeriod.png)
   
    <span data-ttu-id="2a430-205">Hello 대시보드 메트릭 차트에 그리기 메트릭에 대 한 hello 메서드 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-205">On hello dashboard metrics chart, hello method for plotting metrics is different.</span></span> <span data-ttu-id="2a430-206">표준 메트릭 집합을 사용할 수는 및 메트릭을 추가 하거나 hello 메트릭 헤더를 선택 하 여 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-206">A standard set of metrics is available, and metrics are added or removed by selecting hello metric header.</span></span>

### <a name="toocustomize-hello-metrics-chart-on-hello-dashboard"></a><span data-ttu-id="2a430-207">hello 대시보드에서 toocustomize hello 메트릭 차트</span><span class="sxs-lookup"><span data-stu-id="2a430-207">toocustomize hello metrics chart on hello dashboard</span></span>
1. <span data-ttu-id="2a430-208">Hello 클라우드 서비스에 대 한 hello 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-208">Open hello dashboard for hello cloud service.</span></span>
2. <span data-ttu-id="2a430-209">추가 하거나 hello 차트에서 메트릭을 제거:</span><span class="sxs-lookup"><span data-stu-id="2a430-209">Add or remove metrics from hello chart:</span></span>
   
   * <span data-ttu-id="2a430-210">tooplot hello 차트 헤더에서 hello 메트릭에 대 한 새 메트릭, 선택 hello 확인란 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-210">tooplot a new metric, select hello check box for hello metric in hello chart headers.</span></span> <span data-ttu-id="2a430-211">좁은 표시 되는 아래쪽 화살표에서 hello 클릭  ***n* ?? 메트릭** tooplot 메트릭 hello 차트 머리글 영역을 표시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-211">On a narrow display, click hello down arrow by ***n*??metrics** tooplot a metric hello chart header area can't display.</span></span>
   * <span data-ttu-id="2a430-212">해당 헤더에 의해 확인란 선택을 취소 hello hello 차트에 메트릭 toodelete 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-212">toodelete a metric that is plotted on hello chart, clear hello check box by its header.</span></span>
   
3. <span data-ttu-id="2a430-213">**상대** 및 **절대** 표시를 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-213">Switch between **Relative** and **Absolute** displays.</span></span>
4. <span data-ttu-id="2a430-214">1 시간, 24 시간 또는 7 일간의 데이터 toodisplay 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-214">Choose 1 hour, 24 hours, or 7 days of data toodisplay.</span></span>

## <a name="how-to-access-verbose-monitoring-data-outside-hello-azure-classic-portal"></a><span data-ttu-id="2a430-215">방법: hello Azure 클래식 포털 외부 자세한 정보 표시 모니터링 데이터에 액세스</span><span class="sxs-lookup"><span data-stu-id="2a430-215">How to: Access verbose monitoring data outside hello Azure classic portal</span></span>
<span data-ttu-id="2a430-216">자세한 정보 표시 모니터링 데이터는 각 역할에 대해 지정 하는 hello 저장소 계정에서 테이블에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-216">Verbose monitoring data is stored in tables in hello storage accounts that you specify for each role.</span></span> <span data-ttu-id="2a430-217">각 클라우드 서비스 배포에 대 한 hello 역할에 대 한 6 개의 테이블이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-217">For each cloud service deployment, six tables are created for hello role.</span></span> <span data-ttu-id="2a430-218">각각(5분, 1시간 및 12시간)에 대해 두 개의 테이블이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-218">Two tables are created for each (5 minutes, 1 hour, and 12 hours).</span></span> <span data-ttu-id="2a430-219">역할 수준 집계; 저장 이러한 테이블 중 하나 역할 인스턴스에 대 한 다른 테이블 저장소 집계 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2a430-219">One of these tables stores role-level aggregations; hello other table stores aggregations for role instances.</span></span> 

<span data-ttu-id="2a430-220">hello 테이블 이름에는 형식에 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="2a430-220">hello table names have hello following format:</span></span>

```
WAD*deploymentID*PT*aggregation_interval*[R|RI]Table
```

<span data-ttu-id="2a430-221">설명:</span><span class="sxs-lookup"><span data-stu-id="2a430-221">where:</span></span>

* <span data-ttu-id="2a430-222">*deploymentID* 는 hello toohello 클라우드 서비스 배포에 할당 된 GUID</span><span class="sxs-lookup"><span data-stu-id="2a430-222">*deploymentID* is hello GUID assigned toohello cloud service deployment</span></span>
* <span data-ttu-id="2a430-223">*aggregation_interval* = 5M, 1H 또는 12H</span><span class="sxs-lookup"><span data-stu-id="2a430-223">*aggregation_interval* = 5M, 1H, or 12H</span></span>
* <span data-ttu-id="2a430-224">역할 수준 집계 = R</span><span class="sxs-lookup"><span data-stu-id="2a430-224">role-level aggregations = R</span></span>
* <span data-ttu-id="2a430-225">역할 인스턴스에 대한 집계 = RI</span><span class="sxs-lookup"><span data-stu-id="2a430-225">aggregations for role instances = RI</span></span>

<span data-ttu-id="2a430-226">예를 들어 hello 다음 테이블은 저장 1 시간 간격으로 집계 하는 자세한 정보 표시 모니터링 데이터:</span><span class="sxs-lookup"><span data-stu-id="2a430-226">For example, hello following tables would store verbose monitoring data aggregated at 1-hour intervals:</span></span>

```
WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRTable (hourly aggregations for hello role)

WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRITable (hourly aggregations for role instances)
```
