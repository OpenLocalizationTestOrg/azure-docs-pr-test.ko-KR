---
title: "Azure에서 앱 강화 | Microsoft Docs"
description: "Azure 앱 서비스에서 앱을 강화하여 용량 및 기능을 추가하는 방법을 알아봅니다."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 75ddbacbd4dd14597b786d26f0730477f6c85811
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-up-an-app-in-azure"></a><span data-ttu-id="0db59-103">Azure에서 앱 강화</span><span class="sxs-lookup"><span data-stu-id="0db59-103">Scale up an app in Azure</span></span>
<span data-ttu-id="0db59-104">이 문서에서는 Azure 앱 서비스에서 앱의 크기를 조정하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-104">This article shows you how to scale your app in Azure App Service.</span></span> <span data-ttu-id="0db59-105">크기를 조정하는 두 개의 워크플로(강화, 규모 확장)가 있으며 이 문서에서는 강화 워크플로를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-105">There are two workflows for scaling, scale up and scale out, and this article explains the scale up workflow.</span></span>

* <span data-ttu-id="0db59-106">[강화](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): 더 많은 CPU, 메모리, 디스크 공간 및 추가 기능(전용 가상 컴퓨터(VM), 사용자 지정 도메인 및 인증서, 스테이징 슬롯, 자동 크기 조정 등)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-106">[Scale up](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Get more CPU, memory, disk space, and extra features like dedicated virtual machines (VMs), custom domains and certificates, staging slots, autoscaling, and more.</span></span> <span data-ttu-id="0db59-107">앱이 속한 앱 서비스 계획의 가격 책정 계층을 변경하여 강화합니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-107">You scale up by changing the pricing tier of the App Service plan that your app belongs to.</span></span>
* <span data-ttu-id="0db59-108">[규모 확장](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): 앱을 실행하는 VM 인스턴스 수가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-108">[Scale out](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): Increase the number of VM instances that run your app.</span></span>
  <span data-ttu-id="0db59-109">가격 책정 계층에 따라 최대 20개의 인스턴스로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-109">You can scale out to as many as 20 instances, depending on your pricing tier.</span></span> <span data-ttu-id="0db59-110">[프리미엄](../app-service/app-service-app-service-environments-readme.md) 계층에서 **앱 서비스 환경** 은 규모 확장 개수가 인스턴스 50개로 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-110">[App Service Environments](../app-service/app-service-app-service-environments-readme.md) in **Premium** tier will further increase your scale-out count to 50 instances.</span></span> <span data-ttu-id="0db59-111">규모 확장에 대한 자세한 내용은 [수동 또는 자동으로 인스턴스 개수 조정](../monitoring-and-diagnostics/insights-how-to-scale.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0db59-111">For more information about scaling out, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md).</span></span> <span data-ttu-id="0db59-112">자동 크기 조정을 사용하는 방법을 찾아볼 수 있으며 이는 미리 정의된 규칙 및 일정에 따라 자동으로 인스턴스 개수를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-112">There you will find out how to use autoscaling, which is to scale instance count automatically based on predefined rules and schedules.</span></span>

<span data-ttu-id="0db59-113">크기 조정 설정을 적용하는 데 몇 초밖에 걸리지 않으며 [앱 서비스 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)의 모든 앱에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-113">The scale settings take only seconds to apply and affect all apps in your [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
<span data-ttu-id="0db59-114">코드를 변경하거나 응용 프로그램을 다시 배포할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-114">They do not require you to change your code or redeploy your application.</span></span>

<span data-ttu-id="0db59-115">개별 앱 서비스 계획의 가격 책정 및 기능에 대한 자세한 내용은 [앱 서비스 가격 정보](https://azure.microsoft.com/pricing/details/web-sites/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0db59-115">For information about the pricing and features of individual App Service plans, see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>  

> [!NOTE]
> <span data-ttu-id="0db59-116">**무료** 계층에서 앱 서비스 계획을 전환하기 전에 먼저 Azure 구독에 대한 [지출 한도](https://azure.microsoft.com/pricing/spending-limits/) 를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-116">Before you switch an App Service plan from the **Free** tier, you must first remove the [spending limits](https://azure.microsoft.com/pricing/spending-limits/) in place for your Azure subscription.</span></span> <span data-ttu-id="0db59-117">Microsoft Azure App Service 구독 옵션을 보거나 변경하려면 [Microsoft Azure 구독][azuresubscriptions]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0db59-117">To view or change options for your Microsoft Azure App Service subscription, see [Microsoft Azure Subscriptions][azuresubscriptions].</span></span>
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a><span data-ttu-id="0db59-118">가격 책정 계층 강화</span><span class="sxs-lookup"><span data-stu-id="0db59-118">Scale up your pricing tier</span></span>
1. <span data-ttu-id="0db59-119">브라우저에서 [Azure Portal][portal]을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-119">In your browser, open the [Azure portal][portal].</span></span>
2. <span data-ttu-id="0db59-120">앱 블레이드에서 **모든 설정**을 클릭한 다음 **강화**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-120">In your app's blade, click **All settings**, and then click **Scale Up**.</span></span>
   
    ![Azure 앱을 강화하기 위해 이동합니다.][ChooseWHP]
3. <span data-ttu-id="0db59-122">사용자 계층을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-122">Choose your tier, and then click **Select**.</span></span>
   
    <span data-ttu-id="0db59-123">작업이 완료되면 **알림** 탭에 **성공**이 녹색으로 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-123">The **Notifications** tab will flash a green **SUCCESS** after the operation is complete.</span></span>

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a><span data-ttu-id="0db59-124">규모 관련 리소스</span><span class="sxs-lookup"><span data-stu-id="0db59-124">Scale related resources</span></span>
<span data-ttu-id="0db59-125">앱이 Azure SQL 데이터베이스 또는 Azure 저장소와 같은 다른 서비스에 종속된 경우 요구에 따라 해당 리소스를 강화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-125">If your app depends on other services, such as Azure SQL Database or Azure Storage, you can also scale up those resources based on your needs.</span></span> <span data-ttu-id="0db59-126">이러한 리소스는 앱 서비스 계획을 사용하여 크기가 조정되지 않고 개별적으로 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-126">These resources are not scaled with the App Service plan and must be scaled separately.</span></span>

1. <span data-ttu-id="0db59-127">**필수 항목**에서 **리소스 그룹** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-127">In **Essentials**, click the **Resource group** link.</span></span>
   
    ![Azure 앱의 관련 리소스를 강화합니다.](./media/web-sites-scale/RGEssentialsLink.png)
2. <span data-ttu-id="0db59-129">**리소스 그룹** 블레이드의 **요약** 파트에서 크기를 조정하려는 리소스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-129">In the **Summary** part of the **Resource group** blade, click a resource that you want to scale.</span></span> <span data-ttu-id="0db59-130">다음 스크린샷은 SQL 데이터베이스 리소스 및 Azure Storage 리소스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-130">The following screenshot shows a SQL Database resource and an Azure Storage resource.</span></span>
   
    ![리소스 그룹 블레이드로 이동하여 Azure 앱을 강화합니다.](./media/web-sites-scale/ResourceGroup.png)
3. <span data-ttu-id="0db59-132">SQL Database 리소스의 경우 **설정** > **가격 책정 계층**을 클릭하여 가격 책정 계층을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-132">For a SQL Database resource, click **Settings** > **Pricing tier** to scale the pricing tier.</span></span>
   
    ![Azure 앱에 대한 SQL 데이터베이스 백 엔드를 강화합니다.](./media/web-sites-scale/ScaleDatabase.png)
   
    <span data-ttu-id="0db59-134">또한 SQL 데이터베이스 인스턴스에 [지역에서 복제](../sql-database/sql-database-geo-replication-overview.md) 를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-134">You can also turn on [geo-replication](../sql-database/sql-database-geo-replication-overview.md) for your SQL Database instance.</span></span>
   
    <span data-ttu-id="0db59-135">Azure Storage 리소스의 경우 **설정** > **구성**을 클릭하여 저장소 옵션을 강화합니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-135">For an Azure Storage resource, click **Settings** > **Configuration** to scale up your storage options.</span></span>
   
    ![Azure 앱에서 사용하는 Azure 저장소 계정을 강화합니다](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a><span data-ttu-id="0db59-137">개발자 기능에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="0db59-137">Learn about developer features</span></span>
<span data-ttu-id="0db59-138">가격 책정 계층에 따라 다음과 같은 개발자 지향 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-138">Depending on the pricing tier, the following developer-oriented features are available:</span></span>

### <a name="bitness"></a><span data-ttu-id="0db59-139">비트 수</span><span class="sxs-lookup"><span data-stu-id="0db59-139">Bitness</span></span>
* <span data-ttu-id="0db59-140">**기본**, **표준** 및 **프리미엄** 계층은 64비트 및 32비트 응용 프로그램을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-140">The **Basic**, **Standard**, and **Premium** tiers support 64-bit and 32-bit applications.</span></span>
* <span data-ttu-id="0db59-141">**무료** 및 **공유** 계획 계층은 32비트 응용 프로그램만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-141">The **Free** and **Shared** plan tiers support 32-bit applications only.</span></span>

### <a name="debugger-support"></a><span data-ttu-id="0db59-142">디버거 지원</span><span class="sxs-lookup"><span data-stu-id="0db59-142">Debugger support</span></span>
* <span data-ttu-id="0db59-143">디버거 지원은 App Service 계획당 1건의 연결에서 **무료**, **공유** 및 **기본** 모드에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-143">Debugger support is available for the **Free**, **Shared**, and **Basic** modes at one connection per App Service plan.</span></span>
* <span data-ttu-id="0db59-144">디버거 지원은 App Service 계획당 5건의 동시 연결에서 **표준** 및 **프리미엄** 모드에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-144">Debugger support is available for the **Standard** and **Premium** modes at five concurrent connections per App Service plan.</span></span>

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a><span data-ttu-id="0db59-145">다른 기능에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="0db59-145">Learn about other features</span></span>
* <span data-ttu-id="0db59-146">개발자를 비롯하여 모든 사용자에게 유용한 가격 및 기능을 포함하여 앱 서비스 계획의 나머지 모든 기능에 대한 자세한 내용은 [앱 서비스 가격 정보](https://azure.microsoft.com/pricing/details/web-sites/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0db59-146">For detailed information about all of the remaining features in the App Service plans, including pricing and features of interest to all users (including developers), see [App Service Pricing Details](https://azure.microsoft.com/pricing/details/web-sites/).</span></span>

> [!NOTE]
> <span data-ttu-id="0db59-147">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 평가](https://azure.microsoft.com/try/app-service/)로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-147">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/) where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="0db59-148">신용 카드는 필요하지 않으며 약정은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0db59-148">No credit cards are required and there are no commitments.</span></span>
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a><span data-ttu-id="0db59-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0db59-149">Next steps</span></span>
* <span data-ttu-id="0db59-150">Azure에 등록하려면 [Microsoft Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0db59-150">To get started with Azure, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="0db59-151">가격 책정, 지원 및 SLA에 대한 자세한 내용은 다음 링크를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="0db59-151">For information about pricing, support, and SLA, visit the following links.</span></span>
  
    [<span data-ttu-id="0db59-152">데이터 전송 가격 정보</span><span class="sxs-lookup"><span data-stu-id="0db59-152">Data Transfers Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [<span data-ttu-id="0db59-153">Microsoft Azure 지원 계획</span><span class="sxs-lookup"><span data-stu-id="0db59-153">Microsoft Azure Support Plans</span></span>](https://azure.microsoft.com/support/plans/)
  
    [<span data-ttu-id="0db59-154">서비스 수준 계약</span><span class="sxs-lookup"><span data-stu-id="0db59-154">Service Level Agreements</span></span>](https://azure.microsoft.com/support/legal/sla/)
  
    [<span data-ttu-id="0db59-155">SQL 데이터베이스 가격 정보</span><span class="sxs-lookup"><span data-stu-id="0db59-155">SQL Database Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/sql-database/)
  
    <span data-ttu-id="0db59-156">[Microsoft Azure를 위한 가상 컴퓨터 및 클라우드 서비스 크기][vmsizes]</span><span class="sxs-lookup"><span data-stu-id="0db59-156">[Virtual Machine and Cloud Service Sizes for Microsoft Azure][vmsizes]</span></span>
  
    [<span data-ttu-id="0db59-157">앱 서비스 가격 정보</span><span class="sxs-lookup"><span data-stu-id="0db59-157">App Service Pricing Details</span></span>](https://azure.microsoft.com/pricing/details/app-service/)
  
    [<span data-ttu-id="0db59-158">앱 서비스 가격 정보 - SSL 연결</span><span class="sxs-lookup"><span data-stu-id="0db59-158">App Service Pricing Details - SSL Connections</span></span>](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* <span data-ttu-id="0db59-159">확장성 있고 복원력이 뛰어난 아키텍처 빌드를 포함하여 Azure 앱 서비스 모범 사례에 대한 자세한 내용은 [모범 사례: Azure 앱 서비스 웹앱](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0db59-159">For information about Azure App Service best practices, including building a scalable and resilient architecture, see [Best Practices: Azure App Service Web Apps](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).</span></span>
* <span data-ttu-id="0db59-160">앱 서비스 앱 크기 조정에 대한 비디오는 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0db59-160">For videos about scaling App Service apps, see the following resources:</span></span>
  
  * [<span data-ttu-id="0db59-161">Azure 웹 사이트 크기를 조정하는 방법 - 스테판 스차코우(Stefan Schackow)</span><span class="sxs-lookup"><span data-stu-id="0db59-161">When to Scale Azure Websites - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [<span data-ttu-id="0db59-162">Azure 웹 사이트, CPU 또는 예약 리소스 크기 자동 조정 - 스테판 스차코우(Stefan Schackow)</span><span class="sxs-lookup"><span data-stu-id="0db59-162">Auto Scaling Azure Websites, CPU or Scheduled - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [<span data-ttu-id="0db59-163">Azure 웹 사이트 크기 조정 방법 - 스테판 스차코우(Stefan Schackow)</span><span class="sxs-lookup"><span data-stu-id="0db59-163">How Azure Websites Scale - with Stefan Schackow</span></span>](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
