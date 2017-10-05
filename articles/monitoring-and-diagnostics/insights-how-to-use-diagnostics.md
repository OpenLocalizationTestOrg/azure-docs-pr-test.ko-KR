---
title: "Microsoft Azure에서 모니터링 및 진단 사용 | Microsoft 문서"
description: "Azure에서 리소스에 대한 진단을 설정하는 방법에 대해 알아봅니다."
author: rboucher
manager: carolz
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: af1947a9-c211-4aa1-8924-880a86240be4
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: b82bb1ab419831e803689edb2a2a7fe256dde5a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-monitoring-and-diagnostics"></a><span data-ttu-id="daa4c-103">모니터링 및 진단 사용</span><span class="sxs-lookup"><span data-stu-id="daa4c-103">Enable monitoring and diagnostics</span></span>
<span data-ttu-id="daa4c-104">[Azure 포털](https://portal.azure.com)에서 리소스에 대한 다양하고 빈번한 모니터링 및 진단 데이터를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-104">In the [Azure Portal](https://portal.azure.com), you can configure rich, frequent, monitoring and diagnostics data about your resources.</span></span> <span data-ttu-id="daa4c-105">[REST API](https://msdn.microsoft.com/library/azure/dn931932.aspx) 또는 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)를 사용하여 프로그래밍 방식으로 진단을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-105">You can also use the [REST API](https://msdn.microsoft.com/library/azure/dn931932.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) to configure diagnostics programmatically.</span></span>

<span data-ttu-id="daa4c-106">Azure의 진단, 모니터링 및 메트릭 데이터는 선택한 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-106">Diagnostics, monitoring and metric data in Azure is saved into a Storage account of your choice.</span></span> <span data-ttu-id="daa4c-107">따라서 저장소 탐색기부터 Power BI 및 타사 도구에 이르기까지 원하는 도구를 사용하여 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-107">This allows you to use whatever tooling you want to read the data, from a storage explorer, to Power BI to third-party tooling.</span></span>

## <a name="when-you-create-a-resource"></a><span data-ttu-id="daa4c-108">리소스를 만드는 경우</span><span class="sxs-lookup"><span data-stu-id="daa4c-108">When you create a resource</span></span>
<span data-ttu-id="daa4c-109">[Azure 포털](https://portal.azure.com)에서 리소스를 처음 만드는 경우 대부분의 서비스를 통해 진단을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-109">Most services allow you to enable diagnostics when you first create them in the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="daa4c-110">**새로 만들기** 로 이동한 다음 관심 있는 리소스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-110">Go to **New** and choose the resource you are interested in.</span></span>
2. <span data-ttu-id="daa4c-111">**선택적 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-111">Select **Optional configuration**.</span></span>
    <span data-ttu-id="daa4c-112">![진단 블레이드](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)</span><span class="sxs-lookup"><span data-stu-id="daa4c-112">![Diagnostics blade](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)</span></span>
3. <span data-ttu-id="daa4c-113">**진단**을 선택하고 **On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-113">Select **Diagnostics**, and click **On**.</span></span> <span data-ttu-id="daa4c-114">진단을 저장할 저장소 계정을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-114">You will need to choose the Storage account that you want diagnostics to be saved to.</span></span> <span data-ttu-id="daa4c-115">저장소 계정에 진단을 보내는 경우 저장소 및 트랜잭션에 대해 표준 데이터 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-115">You’ll be charged normal data rates for storage and transactions when you send diagnostics to a storage account.</span></span>
4. <span data-ttu-id="daa4c-116">**확인** 을 클릭하여 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-116">Click **OK** and create the resource.</span></span>

## <a name="change-settings-for-an-existing-resource"></a><span data-ttu-id="daa4c-117">기존 리소스에 대한 설정 변경</span><span class="sxs-lookup"><span data-stu-id="daa4c-117">Change settings for an existing resource</span></span>
<span data-ttu-id="daa4c-118">리소스를 이미 만들었으며 진단 설정을 변경하려는 경우(예: 데이터 컬렉션 수준 변경), Azure 포털에서 바로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-118">If you have already created a resource and you want to change the diagnostics settings (to change the level of data collection, for example), you can do that right in the Azure Portal.</span></span>

1. <span data-ttu-id="daa4c-119">리소스로 이동한 다음 **설정** 명령을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-119">Go to the resource and click the **Settings** command.</span></span>
2. <span data-ttu-id="daa4c-120">**진단**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-120">Select **Diagnostics**.</span></span>
3. <span data-ttu-id="daa4c-121">**진단** 블레이드에는 해당 리소스에 대한 가능한 진단 및 모니터링 컬렉션 데이터가 모두 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-121">The **Diagnostics** blade has all of the possible diagnostics and monitoring collection data for that resource.</span></span> <span data-ttu-id="daa4c-122">일부 리소스의 경우 데이터에 대한 **보존** 정책을 선택하여 저장소 계정에서 정리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-122">For some resources you can also choose a **Retention** policy for the data, to clean it up from your storage account.</span></span>
    <span data-ttu-id="daa4c-123">![저장소 진단](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)</span><span class="sxs-lookup"><span data-stu-id="daa4c-123">![Storage diagnostics](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)</span></span>
4. <span data-ttu-id="daa4c-124">설정을 선택한 후 **저장** 명령을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-124">Once you've chosen your settings, click the **Save** command.</span></span> <span data-ttu-id="daa4c-125">처음 사용하도록 설정하는 경우 모니터링 데이터가 표시되는 데 시간이 걸릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-125">It may take a little while for monitoring data to show up if you are enabling it for the first time.</span></span>

### <a name="categories-of-data-collection-for-virtual-machines"></a><span data-ttu-id="daa4c-126">가상 컴퓨터에 대한 데이터 컬렉션 범주</span><span class="sxs-lookup"><span data-stu-id="daa4c-126">Categories of data collection for virtual machines</span></span>
<span data-ttu-id="daa4c-127">가상 컴퓨터의 경우 모든 메트릭과 로그가 1분 간격으로 기록되므로 컴퓨터에 대한 최신 정보를 항상 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-127">For virtual machines all metrics and logs will be recorded at one-minute intervals, so you can always have the most up-to-date information about your machine.</span></span>

* <span data-ttu-id="daa4c-128">**기본 메트릭** : 프로세서, 메모리 등 가상 컴퓨터에 대한 상태 메트릭입니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-128">**Basic metrics** : Health metrics about your virtual machine such as processor and memory</span></span>
* <span data-ttu-id="daa4c-129">**네트워크 및 웹 메트릭** : 네트워크 연결 및 웹 서비스에 대한 메트릭입니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-129">**Network and web metrics** : Metrics about your network connections and web services</span></span>
* <span data-ttu-id="daa4c-130">**.NET 메트릭** : 가상 컴퓨터에서 실행되는 .NET 및 ASP.NET 응용 프로그램에 대한 메트릭입니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-130">**.NET metrics** : Metrics about the .NET and ASP.NET applications running on your virtual machine</span></span>
* <span data-ttu-id="daa4c-131">**SQL 메트릭** : Microsoft SQL Service를 실행하는 경우 해당 성능 메트릭입니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-131">**SQL metrics** : If you are running Microsoft SQL Service, its performance metrics</span></span>
* <span data-ttu-id="daa4c-132">**Windows 이벤트 응용 프로그램 로그** : 응용 프로그램 채널로 전송되는 Windows 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-132">**Windows event application logs** : Windows events that are sent to the application channel</span></span>
* <span data-ttu-id="daa4c-133">**Windows 이벤트 시스템 로그** : 시스템 채널로 전송되는 Windows 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-133">**Windows event system logs** : Windows events that are sent to the system channel.</span></span> <span data-ttu-id="daa4c-134">[Microsoft 맬웨어 방지 프로그램](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409)의 모든 이벤트도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-134">This also includes all events from [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).</span></span>
* <span data-ttu-id="daa4c-135">**Windows 이벤트 보안 로그** : 보안 채널로 전송되는 Windows 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-135">**Windows event security logs** : Windows events that are sent to the security channel</span></span>
* <span data-ttu-id="daa4c-136">**진단 인프라 로그** : 진단 수집 인프라에 대한 로깅입니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-136">**Diagnostics infrastructure logs** : Logging about the diagnostics collection infrastructure</span></span>
* <span data-ttu-id="daa4c-137">**IIS 로그** : IIS 서버에 대한 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-137">**IIS logs** : Logs about your IIS server</span></span>

<span data-ttu-id="daa4c-138">현재 특정 Linux 배포는 지원되지 않으며, 가상 컴퓨터에 게스트 에이전트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-138">Note that at this time certain distributions of Linux are not supported, and, the Guest Agent must be installed on the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="daa4c-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="daa4c-139">Next steps</span></span>
* <span data-ttu-id="daa4c-140">[경고 알림을 수신](insights-receive-alert-notifications.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-140">[Receive alert notifications](insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="daa4c-141">[서비스 메트릭을 모니터링](insights-how-to-customize-monitoring.md) 하여 서비스를 사용 가능하며 응답할 수 있는 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-141">[Monitor service metrics](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
* <span data-ttu-id="daa4c-142">[인스턴스 개수를 자동으로 조정](insights-how-to-scale.md) 하여 수요를 기준으로 서비스 크기가 조정되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-142">[Scale instance count automatically](insights-how-to-scale.md) to make sure your service scale based on demand.</span></span>
* <span data-ttu-id="daa4c-143">[응용 프로그램 성능을 모니터링](../application-insights/app-insights-azure-web-apps.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-143">[Monitor application performance](../application-insights/app-insights-azure-web-apps.md) if you want to understand exactly how your code is performing in the cloud.</span></span>
* <span data-ttu-id="daa4c-144">[이벤트 및 활동 로그를 보고](insights-debugging-with-events.md) 서비스에서 발생한 모든 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-144">[View events and activity log](insights-debugging-with-events.md) to learn everything that has happened in your service.</span></span>
* <span data-ttu-id="daa4c-145">[서비스 상태를 추적](insights-service-health.md) 하여 Azure에서 성능 저하 또는 서비스 중단이 발생한 시기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="daa4c-145">[Track service health](insights-service-health.md) to find out when Azure has experienced performance degradation or service interruptions.</span></span>

