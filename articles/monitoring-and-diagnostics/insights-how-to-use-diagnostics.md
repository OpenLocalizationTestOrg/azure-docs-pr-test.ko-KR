---
title: "aaaEnable 모니터링 및 Microsoft Azure에서 진단 | Microsoft Docs"
description: "자세한 방법을 tooset Azure에서 리소스에 대 한 진단 구성 합니다."
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
ms.openlocfilehash: 865d010c5846fff6d871e20eca2bc4ac35028354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-monitoring-and-diagnostics"></a><span data-ttu-id="50f14-103">모니터링 및 진단 사용</span><span class="sxs-lookup"><span data-stu-id="50f14-103">Enable monitoring and diagnostics</span></span>
<span data-ttu-id="50f14-104">Hello에 [Azure 포털](https://portal.azure.com), 리소스에 대 한 풍부한 자주, 모니터링 및 진단 데이터를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-104">In hello [Azure Portal](https://portal.azure.com), you can configure rich, frequent, monitoring and diagnostics data about your resources.</span></span> <span data-ttu-id="50f14-105">Hello를 사용할 수도 있습니다 [REST API](https://msdn.microsoft.com/library/azure/dn931932.aspx) 또는 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooconfigure 진단 프로그래밍 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-105">You can also use hello [REST API](https://msdn.microsoft.com/library/azure/dn931932.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooconfigure diagnostics programmatically.</span></span>

<span data-ttu-id="50f14-106">Azure의 진단, 모니터링 및 메트릭 데이터는 선택한 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-106">Diagnostics, monitoring and metric data in Azure is saved into a Storage account of your choice.</span></span> <span data-ttu-id="50f14-107">이렇게 하면 toouse 있습니다 어떤 tooling tooread hello 데이터 저장소 탐색기에서 원하는 tooPower BI toothird 타사 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-107">This allows you toouse whatever tooling you want tooread hello data, from a storage explorer, tooPower BI toothird-party tooling.</span></span>

## <a name="when-you-create-a-resource"></a><span data-ttu-id="50f14-108">리소스를 만드는 경우</span><span class="sxs-lookup"><span data-stu-id="50f14-108">When you create a resource</span></span>
<span data-ttu-id="50f14-109">대부분 서비스를 사용 하면 tooenable 진단 hello에 처음 만들 때 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-109">Most services allow you tooenable diagnostics when you first create them in hello [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="50f14-110">너무 이동**새로** 에 관심이 있는 hello 리소스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-110">Go too**New** and choose hello resource you are interested in.</span></span>
2. <span data-ttu-id="50f14-111">**선택적 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-111">Select **Optional configuration**.</span></span>
    <span data-ttu-id="50f14-112">![진단 블레이드](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)</span><span class="sxs-lookup"><span data-stu-id="50f14-112">![Diagnostics blade](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)</span></span>
3. <span data-ttu-id="50f14-113">**진단**을 선택하고 **On**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-113">Select **Diagnostics**, and click **On**.</span></span> <span data-ttu-id="50f14-114">Toochoose hello 저장소 계정의 진단 toobe에 저장 되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-114">You will need toochoose hello Storage account that you want diagnostics toobe saved to.</span></span> <span data-ttu-id="50f14-115">있습니다 진단 tooa 저장소 계정을 보낼 때 저장소 및 트랜잭션에 대해 일반 데이터 요금이 청구 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-115">You’ll be charged normal data rates for storage and transactions when you send diagnostics tooa storage account.</span></span>
4. <span data-ttu-id="50f14-116">클릭 **확인** hello 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-116">Click **OK** and create hello resource.</span></span>

## <a name="change-settings-for-an-existing-resource"></a><span data-ttu-id="50f14-117">기존 리소스에 대한 설정 변경</span><span class="sxs-lookup"><span data-stu-id="50f14-117">Change settings for an existing resource</span></span>
<span data-ttu-id="50f14-118">리소스를 이미 만든 경우 toochange hello 진단 설정 (예: 데이터 컬렉션의 toochange hello 수준) hello Azure 포털에서에서 해당 바로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-118">If you have already created a resource and you want toochange hello diagnostics settings (toochange hello level of data collection, for example), you can do that right in hello Azure Portal.</span></span>

1. <span data-ttu-id="50f14-119">Toohello 리소스를 이동 하 고 hello 클릭 **설정을** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-119">Go toohello resource and click hello **Settings** command.</span></span>
2. <span data-ttu-id="50f14-120">**진단**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-120">Select **Diagnostics**.</span></span>
3. <span data-ttu-id="50f14-121">hello **진단** 블레이드는 모든 hello 가지 진단 및 해당 리소스에 대 한 컬렉션 데이터를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-121">hello **Diagnostics** blade has all of hello possible diagnostics and monitoring collection data for that resource.</span></span> <span data-ttu-id="50f14-122">일부 리소스에 대 한 선택할 수도 있습니다는 **보존** 정책 tooclean hello 데이터용 저장소 계정에서이 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-122">For some resources you can also choose a **Retention** policy for hello data, tooclean it up from your storage account.</span></span>
    <span data-ttu-id="50f14-123">![저장소 진단](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)</span><span class="sxs-lookup"><span data-stu-id="50f14-123">![Storage diagnostics](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)</span></span>
4. <span data-ttu-id="50f14-124">설정을 선택 하면 클릭 hello **저장** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-124">Once you've chosen your settings, click hello **Save** command.</span></span> <span data-ttu-id="50f14-125">설정 하는 경우 그 hello에 대 한 처음으로 데이터 tooshow를 모니터링에 대 한 약간 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-125">It may take a little while for monitoring data tooshow up if you are enabling it for hello first time.</span></span>

### <a name="categories-of-data-collection-for-virtual-machines"></a><span data-ttu-id="50f14-126">가상 컴퓨터에 대한 데이터 컬렉션 범주</span><span class="sxs-lookup"><span data-stu-id="50f14-126">Categories of data collection for virtual machines</span></span>
<span data-ttu-id="50f14-127">가상 컴퓨터에 대 한 모든 메트릭 및 로그를 기록할지 1 분 간격으로 수 있도록 항상 hello 최신 정보를 대부분 컴퓨터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-127">For virtual machines all metrics and logs will be recorded at one-minute intervals, so you can always have hello most up-to-date information about your machine.</span></span>

* <span data-ttu-id="50f14-128">**기본 메트릭** : 프로세서, 메모리 등 가상 컴퓨터에 대한 상태 메트릭입니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-128">**Basic metrics** : Health metrics about your virtual machine such as processor and memory</span></span>
* <span data-ttu-id="50f14-129">**네트워크 및 웹 메트릭** : 네트워크 연결 및 웹 서비스에 대한 메트릭입니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-129">**Network and web metrics** : Metrics about your network connections and web services</span></span>
* <span data-ttu-id="50f14-130">**.NET 메트릭** : hello.NET 및 ASP.NET 응용 프로그램에 가상 컴퓨터에서 실행 되는 메트릭</span><span class="sxs-lookup"><span data-stu-id="50f14-130">**.NET metrics** : Metrics about hello .NET and ASP.NET applications running on your virtual machine</span></span>
* <span data-ttu-id="50f14-131">**SQL 메트릭** : Microsoft SQL Service를 실행하는 경우 해당 성능 메트릭입니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-131">**SQL metrics** : If you are running Microsoft SQL Service, its performance metrics</span></span>
* <span data-ttu-id="50f14-132">**Windows 이벤트 응용 프로그램 로그** : toohello 응용 프로그램 채널 전송 되는 Windows 이벤트</span><span class="sxs-lookup"><span data-stu-id="50f14-132">**Windows event application logs** : Windows events that are sent toohello application channel</span></span>
* <span data-ttu-id="50f14-133">**Windows 이벤트 시스템 로그** : toohello 시스템 채널 전송 되는 Windows 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-133">**Windows event system logs** : Windows events that are sent toohello system channel.</span></span> <span data-ttu-id="50f14-134">[Microsoft 맬웨어 방지 프로그램](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409)의 모든 이벤트도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-134">This also includes all events from [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).</span></span>
* <span data-ttu-id="50f14-135">**Windows 이벤트 보안 로그** : toohello 보안 채널을 전송 하는 Windows 이벤트</span><span class="sxs-lookup"><span data-stu-id="50f14-135">**Windows event security logs** : Windows events that are sent toohello security channel</span></span>
* <span data-ttu-id="50f14-136">**진단 인프라 로그** : hello 진단 컬렉션 인프라에 대 한 로깅</span><span class="sxs-lookup"><span data-stu-id="50f14-136">**Diagnostics infrastructure logs** : Logging about hello diagnostics collection infrastructure</span></span>
* <span data-ttu-id="50f14-137">**IIS 로그** : IIS 서버에 대한 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-137">**IIS logs** : Logs about your IIS server</span></span>

<span data-ttu-id="50f14-138">Note이 이번에 특정 배포판의 Linux가 지원 되지 않으며, 하, hello 게스트 에이전트 hello 가상 컴퓨터에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-138">Note that at this time certain distributions of Linux are not supported, and, hello Guest Agent must be installed on hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50f14-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="50f14-139">Next steps</span></span>
* <span data-ttu-id="50f14-140">작업 이벤트가 발생하거나 메트릭이 임계값을 초과할 때마다 [경고 알림을 수신](insights-receive-alert-notifications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-140">[Receive alert notifications](insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="50f14-141">[서비스 메트릭스를 모니터링](insights-how-to-customize-monitoring.md) toomake 서비스를 사용 가능 하 고 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-141">[Monitor service metrics](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
* <span data-ttu-id="50f14-142">[인스턴스 수를 자동으로 크기 조정](insights-how-to-scale.md) toomake 있는지 요구에 따라 서비스 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-142">[Scale instance count automatically](insights-how-to-scale.md) toomake sure your service scale based on demand.</span></span>
* <span data-ttu-id="50f14-143">[응용 프로그램 성능 모니터링](../application-insights/app-insights-azure-web-apps.md) toounderstand 하려면 정확 하 게 코드 작업 수행 방식을 hello 클라우드에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-143">[Monitor application performance](../application-insights/app-insights-azure-web-apps.md) if you want toounderstand exactly how your code is performing in hello cloud.</span></span>
* <span data-ttu-id="50f14-144">[이벤트 및 활동 로그 보기](insights-debugging-with-events.md) toolearn 모든 서비스에 발생 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-144">[View events and activity log](insights-debugging-with-events.md) toolearn everything that has happened in your service.</span></span>
* <span data-ttu-id="50f14-145">[서비스 상태를 추적할](insights-service-health.md) toofind Azure에 성능 저하 또는 서비스 중단을 발생 하는 경우 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="50f14-145">[Track service health](insights-service-health.md) toofind out when Azure has experienced performance degradation or service interruptions.</span></span>

