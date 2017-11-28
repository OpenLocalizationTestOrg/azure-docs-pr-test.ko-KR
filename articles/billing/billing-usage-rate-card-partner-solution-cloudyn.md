---
title: "aaaMicrosoft Azure 사용량 및 RateCard Api를 사용 하도록 설정 Cloudyn tooProvide 고객에 대 한 ITFM | Microsoft Docs"
description: "Hello Azure 청구 Api가 제품에 통합 경험에 Microsoft Azure 청구 파트너 Cloudyn에서 고유한 관점을 제공 합니다.  Azure 서비스용 Cloudyn를 사용/시도하는 데 관심을 두는 Azure 및 Cloudyn 고객에게 특히 유용합니다."
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: f1397397-7e92-4c20-9862-ab6b93afefb7
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: e221ac8b8feebb725a1cc669c8143ab829621a8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-usage-and-ratecard-apis-enable-cloudyn-tooprovide-itfm-for-customers"></a><span data-ttu-id="e6957-104">Microsoft Azure 사용량 및 RateCard Api를 사용 하도록 설정 Cloudyn tooProvide ITFM 고객에 대 한</span><span class="sxs-lookup"><span data-stu-id="e6957-104">Microsoft Azure Usage and RateCard APIs Enable Cloudyn tooProvide ITFM for Customers</span></span>
<span data-ttu-id="e6957-105">Microsoft Azure 리소스 사용량 및 RateCard Api Cloudyn, Microsoft 개발 파트너 및 클라우드 관리 기능을 확인 하는 선도적인 기업 hello 새의 비공개 미리 보기를 위해 선택 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-105">Cloudyn, a Microsoft development partner and a leading provider of cloud management capabilities, was chosen for a private preview of hello new Microsoft Azure Resource Usage and RateCard APIs.</span></span>  <span data-ttu-id="e6957-106">hello 사용량 API는 구독에 대 한 액세스 tooestimated Azure 사용량 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-106">hello Usage API provides access tooestimated Azure consumption data for a subscription.</span></span> <span data-ttu-id="e6957-107">hello RateCard API 비 기업 계약 EA 고객에 대 한 모든 Azure 서비스의 전체 가격 책정 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-107">hello RateCard API provides complete pricing information of all Azure services, for non-Enterprise Agreement (EA) customers.</span></span> <span data-ttu-id="e6957-108">함께 통합되어 이러한 API는 Cloudyn에서 제공하는 것과 같이 IT 재무 관리(ITFM) 도구에 입력하기 위한 전체 정보 기초를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-108">Integrated together, these APIs provide a complete information basis for input into IT Financial Management (ITFM) tools such as those provided by Cloudyn.</span></span>

## <a name="introduction"></a><span data-ttu-id="e6957-109">소개</span><span class="sxs-lookup"><span data-stu-id="e6957-109">Introduction</span></span>
<span data-ttu-id="e6957-110">hello RateCard API에서에서 데이터를 사용 하 여 hello 사용량 API에서에서 데이터의 이른바 "multiplication" hello (사용 [장치] [$unit] price = 자세한 사용 현황 및 비용) 정보를 생성 hello 가장 세분화 하 고 정확한 신뢰할 수 있는 청구 사용할 수 있는 Azure에 대 한 현재 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-110">hello so-called “multiplication” of data from hello Usage API with data from hello RateCard API (usage [units] price[$unit] = Detailed Usage and Cost) creates hello most granular, accurate and reliable billing information available for Azure today.</span></span>

![ITFM 개요][1]

<span data-ttu-id="e6957-112">이러한 Api를 사용해 고객의 사용량 및 Cloudyn tooanalyze 고객 계정에 허용 tooperform를 간단 하 고 프로그래밍 방식으로 다양 한 ITFM 작업 고객에 대 한 비용에 주요 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-112">Consuming these APIs provides key information on customers’ usage and costs, allowing Cloudyn tooanalyze customer accounts in a simple, programmatic manner, and tooperform various ITFM tasks for its customers.</span></span>

## <a name="integrating-cloudyn-with-hello-ratecard-and-usage-apis"></a><span data-ttu-id="e6957-113">사용량 Api 및 RateCard hello로 Cloudyn 통합</span><span class="sxs-lookup"><span data-stu-id="e6957-113">Integrating Cloudyn with hello RateCard and Usage APIs</span></span>
<span data-ttu-id="e6957-114">hello RateCard API 지역 정보, 통화 및 로캘-OfferDurableID (종 량 제, 레거시 6 및 12 개월 약속을 사용 하는 제품 hello 고객 Azure의 hello 유형 지정 하는 것이 가장 중요 한 hello와 같은 여러 개의 입력된 매개 변수--필요 계획, MSDN 혜택, MPN 제공, 프로 모션 혜택 및 다른 사용자).</span><span class="sxs-lookup"><span data-stu-id="e6957-114">hello RateCard API requires several input parameters -- like region info, currency and locale -- but hello most important one is OfferDurableID, which specifies hello type of Azure offering hello customer is using (Pay-as-you-Go, legacy 6 and 12-month commitment plans, MSDN offers, MPN offers, promotional offers and others).</span></span> <span data-ttu-id="e6957-115">hello OfferDurableID 있습니다 hello [e 사용 내역 및 청구 포털](https://account.windowsazure.com/Subscriptions), 아래 hello "제공 ID" hello에 대 한 구독을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-115">hello OfferDurableID can be found in hello [Azure Usage and Billing portal](https://account.windowsazure.com/Subscriptions), under hello "Offer ID" for hello given subscription.</span></span>

<span data-ttu-id="e6957-116">에 대 한 등록 시 [Azure에 대 한 Cloudyn](https://www.cloudyn.com/microsoft-azure/) 서비스, 고객 Cloudyn toopull hello RateCard API를 통해 관련 된 가격 책정 정보 수 있는 OfferDurableID 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-116">Upon registration for [Cloudyn for Azure](https://www.cloudyn.com/microsoft-azure/) services, customers can add their OfferDurableID code, which allows Cloudyn toopull their relevant pricing information through hello RateCard API.</span></span>  <span data-ttu-id="e6957-117">Hello 행사의 서로 다른 형식에 대 한 정보를 찾을 수 있습니다 하나 hello [Microsoft Azure 제안 세부 정보](https://azure.microsoft.com/support/legal/offer-details/) 페이지.</span><span class="sxs-lookup"><span data-stu-id="e6957-117">Information on hello different types of offers can be found one hello [Microsoft Azure Offer Details](https://azure.microsoft.com/support/legal/offer-details/) page.</span></span>

![Cloudyn ITFM 엔진 개요][2]

<span data-ttu-id="e6957-119">Cloudyn 더하기 toohello Azure 성능 API, 분석, 시각화의 추가 계층 toocreate 경고에서 사용량 및 RateCard Api hello 둘 다 사용 하 여 비용 보고, 관리 및는 신뢰할 수 있는 Azure 고객을 제공 하는 실행 가능한 권장 사항 엔터프라이즈 클라우드 ITFM 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-119">Cloudyn uses both hello Usage and RateCard APIs, in addition toohello Azure Performance API, toocreate additional layers of visualization, analytics, alerting, reporting, cost management and actionable recommendations, providing Azure customers a reliable enterprise cloud ITFM tool.</span></span>

## <a name="cloudyn-itfm-use-cases-enabled-by-usage-and-ratecard-api-integration"></a><span data-ttu-id="e6957-120">사용 및 RateCard API 통합이 사용하도록 설정한 Cloudyn ITFM 사용 사례</span><span class="sxs-lookup"><span data-stu-id="e6957-120">Cloudyn ITFM use cases enabled by Usage and RateCard API integration</span></span>
<span data-ttu-id="e6957-121">사용 및 RateCard API가 사용하도록 설정한 일반적인 Cloudyn ITFM 사용 사례는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-121">Common Cloudyn ITFM use cases enabled by usage and RateCard APIs include:</span></span>

* <span data-ttu-id="e6957-122">**비용 분석** -클라우드 허용 tooany 차원 (공급자, 서비스, 계정, 지역 등)를 식별 합니다. 네이티브 세분화 toobe 비용이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-122">**Cost Analysis** - Allows cloud costs toobe broken down tooany native identifying dimension (provider, service, account, region etc.).</span></span> <span data-ttu-id="e6957-123">hello Azure 사용량 및 RateCard Api 확인이 쉬운 작업이 hello 사용 및 비용 데이터를 그룹화 하 고 Cloudyn으로 필터링 하 고 toohello 사용자 그래픽 또는 표 형태로 표시 되는 계정당의 가장 세분화 된 분석을 제공 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-123">hello Azure Usage and RateCard APIs make this an easy task, by providing hello most granular breakdown of usage and cost data per account, which is then grouped and filtered by Cloudyn and presented toohello user, in a graphic or tabular form.</span></span>

![비용 분석 원형 차트][3]

* <span data-ttu-id="e6957-125">**할당 360 비용** -활성화 재무 및 IT 관리자 toouncover hello 실제 비용 분석, 드라이버 및 클라우드 배포의 추세.</span><span class="sxs-lookup"><span data-stu-id="e6957-125">**Cost Allocation 360** - Enables finance and IT managers toouncover hello actual cost breakdown, drivers and trends of their cloud deployment.</span></span> <span data-ttu-id="e6957-126">더 이상 허용 관리자와 비즈니스 단위, 부서, 지역 등, tooeasily 연결 배포 비용 클라우드 비용에 대 한 최고의 정보를 제공 하 고 엔터프라이즈 환불 및 showbacks 촉진 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-126">It further allows managers tooeasily associate deployment expenses with business units, departments, regions, and more, providing unprecedented insights into cloud costs, and facilitating enterprise chargebacks and showbacks.</span></span> <span data-ttu-id="e6957-127">hello Azure 사용량 및 RateCard Api 메서드 및 태그 되지 않은 또는 untaggable 리소스를 할당 하기 위한 비즈니스 논리를 정의 하 여 hello Api를 보완 하는 입력된 tooCloudyn 비용 할당 엔진으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-127">hello Azure Usage and RateCard APIs serve as input tooCloudyn’s cost allocation engine, which complements hello APIs by defining methods and business logic for allocating untagged or untaggable resources.</span></span>

![비용 할당 360 차트][4]

* <span data-ttu-id="e6957-129">**비용 효율적으로 조정** -크기 제한을 초과 또는 과도 하 게 프로 비전 된 컴퓨터에서 hello 고객의 비용을 절감 활용도 낮은 가상 컴퓨터에 대 한 최적화 권장 사항을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-129">**Cost-Effective Sizing** - Provides right-sizing recommendations for underutilized virtual machines, thus reducing hello customer’s expenses on oversized or over-provisioned machines.</span></span> <span data-ttu-id="e6957-130">가상 컴퓨터 CPU 및 RAM 메트릭(성능 API을 통해), 실행 시간(사용 API을 통해) 및 비용(RateCard API를 통해)을 검사하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-130">It does so by examining virtual machine CPU and RAM metrics (via Performance API), hours of run-time (via Usage API) and cost (via RateCard API).</span></span> <span data-ttu-id="e6957-131">Cloudyn 그런 다음 활용도 낮은 CPU, RAM 리소스 (성능)에 따라 최적화 권장 사항을 제공 하 고 hello 실제 시간-사용률 (% 사용률)의 hello 하 여 hello Vm 간의 hello 가격 델타 (RateCard)를 곱하여 예상된 공간 절약을 계산 합니다. 미달 사용된 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-131">Cloudyn then provides right-sizing recommendations based on underutilized CPU or RAM resources (Performance), and calculates estimated savings by multiplying hello price delta (RateCard) between hello VMs by hello actual time-utilization (Usage) of hello underutilized machine.</span></span>

![비용 효율적인 크기 조정][5]

* <span data-ttu-id="e6957-133">**클라우드 포팅 권장 사항** -클라우드 포팅에서 재무 조언을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-133">**Cloud Porting Recommendations** - Provides financial advice on cloud porting.</span></span> <span data-ttu-id="e6957-134">이 사용자의 주요 클라우드 공급 업체에 배포 하는 클라우드 리소스의 현재 비용을 확인 하 고 Azure에서 해당 하는 배포의 toohello 비용을 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-134">It examines a user's current costs of cloud resources which are deployed on major cloud vendors, and compares it toohello cost of an equivalent deployment on Azure.</span></span> <span data-ttu-id="e6957-135">그런 다음 세분화 된 제공 당 리소스, 재정적 기반 권장 사항을 tooAzure 이식 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-135">It then provides granular, per-resource, financially-based porting recommendations tooAzure.</span></span> <span data-ttu-id="e6957-136">Azure (성능 메트릭 및 사용자 기본 설정에 따라)에서 필요한 hello 해당 배포를 파악 한 후 Cloudyn hello 해당 배포의 hello RateCard API tooevaluate hello 비용을 사용 하 여 Azure에서.</span><span class="sxs-lookup"><span data-stu-id="e6957-136">After assessing hello equivalent deployment required on Azure (based on performance metrics and user preferences), Cloudyn uses hello RateCard API tooevaluate hello cost of hello equivalent deployment on Azure.</span></span>
* <span data-ttu-id="e6957-137">**성능 보고서** -Azure의 성능 API에서 사용 하도록 설정, 이러한 보고서의 CPU와 RAM 사용 기능 배열을 toooptimization 권장 사항을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-137">**Performance Reports** - Enabled by Azure’s performance API, these reports provide an array of features from CPU and RAM utilization toooptimization recommendations.</span></span> <span data-ttu-id="e6957-138">아래는 평균 CPU 사용률로 인스턴스 분석 결과를 나타낸 인스턴스 사용률 보고서 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-138">Below is an instance utilization report example, presenting instance breakdown by average CPU utilization.</span></span>

![성능 보고서][6]

* <span data-ttu-id="e6957-140">**범주 관리자** -Cloudyn 순서 toounorganized 클라우드 리소스를 제공 하는 것의 강력한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-140">**Category manager** - A powerful feature in Cloudyn that brings order toounorganized cloud resources.</span></span> <span data-ttu-id="e6957-141">제공 hello 자유 toocreate 사용자가 자신의 고유한 범주 (태그) 효과적인 측정 하 고 보고 하는 업무 관례에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-141">It provides users hello freedom toocreate their own unique categories (tags) for effective measuring and reporting that is in line with business practices.</span></span> <span data-ttu-id="e6957-142">또한 사용자는 일치하지 않는 태그를 쉽게 규제및 분류하고(예: 입력 오류 및 기타 불일치) 정확한 비용 특성에 대한 태그되지 않은 리소스를 자동으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-142">Further, users can easily regulate and categorize inconsistent tagging (i.e. typos and other discrepancies) and automatically detect untagged resources for accurate cost attribution.</span></span>

![범주 관리자][7]

## <a name="video"></a><span data-ttu-id="e6957-144">비디오</span><span class="sxs-lookup"><span data-stu-id="e6957-144">Video</span></span>
<span data-ttu-id="e6957-145">다음은 Azure 고객 Cloudyn을 사용 하 여 Azure 및 Azure 청구 Api, Azure 사용량 데이터에서 toogain insights hello에 대 한는 방법을 보여 주는 짧은 비디오입니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-145">Here's a short video which shows how an Azure customer can use Cloudyn for Azure and hello Azure Billing APIs, toogain insights from their Azure consumption data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Cloudyn-Provides-Cloud-ITFM-Tools-Via-Microsoft-Azure-APIs/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e6957-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6957-146">Next Steps</span></span>
* <span data-ttu-id="e6957-147">무료 시작 [Azure에 대 한 Cloudyn](https://www.cloudyn.com/microsoft-azure/) 평가판 toosee를 가져오는 방법을 사용자 지정 보고 및 Microsoft Azure 클라우드 배포에 대 한 분석 투명도 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-147">Start a free [Cloudyn for Azure](https://www.cloudyn.com/microsoft-azure/) trial toosee how you can obtain cost transparency with customized reporting and analytics for your Microsoft Azure cloud deployment.</span></span>
* <span data-ttu-id="e6957-148">참조 [Microsoft Azure 리소스 소비량에 대 한 이해력](billing-usage-rate-card-overview.md) hello Azure 리소스 사용량 및 RateCard Api에 대 한 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-148">See [Gain insights into your Microsoft Azure resource consumption](billing-usage-rate-card-overview.md) for an overview of hello Azure Resource Usage and RateCard APIs.</span></span>
* <span data-ttu-id="e6957-149">체크 아웃 hello [Azure 청구 REST API 참조](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) 두 Api에 대 한 자세한 내용은 hello hello Azure 리소스 관리자에서 제공 된 Api 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-149">Check out hello [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) for more information on both APIs, which are part of hello set of APIs provided by hello Azure Resource Manager.</span></span>
* <span data-ttu-id="e6957-150">Hello 샘플 코드에 바로 toodive 하려는 경우에 Microsoft Azure 청구 API 코드 샘플 확인해 [Azure 코드 예제](https://azure.microsoft.com/documentation/samples/?term=billing)합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-150">If you would like toodive right into hello sample code, check out our Microsoft Azure Billing API Code Samples on [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?term=billing).</span></span>

## <a name="learn-more"></a><span data-ttu-id="e6957-151">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="e6957-151">Learn More</span></span>
* <span data-ttu-id="e6957-152">Microsoft Azure EA (기업 계약) 제공 서비스에 대해 자세히 toolearn를 방문 하십시오 [Azure Enterprise hello에 대 한 라이선스](https://azure.microsoft.com/pricing/enterprise-agreement/)</span><span class="sxs-lookup"><span data-stu-id="e6957-152">toolearn more about Microsoft Azure Enterprise Agreement (EA) offers, please visit [Licensing Azure for hello Enterprise](https://azure.microsoft.com/pricing/enterprise-agreement/)</span></span>
* <span data-ttu-id="e6957-153">Hello 참조 [Azure 리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md) hello Azure 리소스 관리자에 대 한 자세한 문서 toolearn 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-153">See hello [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md) article toolearn more about hello Azure Resource Manager.</span></span>
* <span data-ttu-id="e6957-154">클라우드 이해에 필요한 toohelp 지출 도구의 hello suite에 자세한 내용은 참조 하십시오 너무 Gartner 문서 [IT 재무 관리 (ITFM) 도구에 대 한 시장 가이드](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb)합니다.</span><span class="sxs-lookup"><span data-stu-id="e6957-154">For additional information on hello suite of tools necessary toohelp in gaining an understanding of cloud spend, please refer too Gartner article [Market Guide for IT Financial Management (ITFM) Tools](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).</span></span>

<!--Image references-->
[1]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Overview.png
[2]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Engine-Overview.png
[3]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Analysis-Pie-Chart.png
[4]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Allocation-360-Chart.png
[5]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Effective-Sizing.png
[6]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Performance-Reports.png
[7]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Category-Manager.png
