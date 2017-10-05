---
title: "Machine Learning을 사용하여 고객 이탈 분석 | Microsoft Docs"
description: "고객 이탈을 분석하고 채점하는 통합 모델 개발에 대한 사례 연구"
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: 1333ffe2-59b8-4f40-9be7-3bf1173fc38d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 84916fc86fd731b3544a0d389325d9a1d14e1a39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="analyzing-customer-churn-by-using-azure-machine-learning"></a><span data-ttu-id="5d499-103">Azure 기계 학습을 사용하여 고객 이탈 분석</span><span class="sxs-lookup"><span data-stu-id="5d499-103">Analyzing Customer Churn by using Azure Machine Learning</span></span>
## <a name="overview"></a><span data-ttu-id="5d499-104">개요</span><span class="sxs-lookup"><span data-stu-id="5d499-104">Overview</span></span>
<span data-ttu-id="5d499-105">이 문서에서는 Azure Machine Learning을 사용하여 빌드된 고객 이탈 분석 프로젝트의 참조 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-105">This article presents a reference implementation of a customer churn analysis project that is built by using Azure Machine Learning.</span></span> <span data-ttu-id="5d499-106">이 문서에서는 산업 고객 이탈 문제를 전체적으로 해결하기 위한 관련된 일반 모델을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-106">In this article, we discuss associated generic models for holistically solving the problem of industrial customer churn.</span></span> <span data-ttu-id="5d499-107">또한 기계 학습을 사용하여 빌드된 모델의 정확도를 측정하고 향후 배포를 위한 방향을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-107">We also measure the accuracy of models that are built by using Machine Learning, and we assess directions for further development.</span></span>  

### <a name="acknowledgements"></a><span data-ttu-id="5d499-108">감사의 말</span><span class="sxs-lookup"><span data-stu-id="5d499-108">Acknowledgements</span></span>
<span data-ttu-id="5d499-109">이 실험은 Microsoft의 수석 데이터 과학자인 Serge Berger와 이전 Microsoft Azure 기계 학습 제품 관리자인 Roger Barga가 개발하고 테스트했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-109">This experiment was developed and tested by Serge Berger, Principal Data Scientist at Microsoft, and Roger Barga, formerly Product Manager for Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="5d499-110">Azure 설명서 팀은 담당자들의 전문 지식을 인정하고 이 백서를 공유한 것에 대해 감사해하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-110">The Azure documentation team gratefully acknowledges their expertise and thanks them for sharing this white paper.</span></span>

> [!NOTE]
> <span data-ttu-id="5d499-111">이 실험에 사용된 데이터는 공개적으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-111">The data used for this experiment is not publicly available.</span></span> <span data-ttu-id="5d499-112">이탈 분석을 위한 Machine Learning 모델을 작성하는 방법의 예제를 보려면 [Cortana Intelligence 갤러리](http://gallery.cortanaintelligence.com/)의 [소매 이탈 모델 템플릿](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d499-112">For an example of how to build a machine learning model for churn analysis, see: [Retail churn model template](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1) in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)</span></span>
> 
> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="the-problem-of-customer-churn"></a><span data-ttu-id="5d499-113">고객 이탈 문제</span><span class="sxs-lookup"><span data-stu-id="5d499-113">The problem of customer churn</span></span>
<span data-ttu-id="5d499-114">고객 시장과 모든 기업 부문의 비즈니스에서는 이탈을 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-114">Businesses in the consumer market and in all enterprise sectors have to deal with churn.</span></span> <span data-ttu-id="5d499-115">때때로 이탈이 지나치고 정책 의사 결정에 영향을 미칠 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-115">Sometimes churn is excessive and influences policy decisions.</span></span> <span data-ttu-id="5d499-116">기존 솔루션에서는 이탈 가능성이 큰 고객을 예측하고 안내자 서비스, 마케팅 캠페인 또는 특별 관리 적용을 통해 해당 고객의 요구를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-116">The traditional solution is to predict high-propensity churners and address their needs via a concierge service, marketing campaigns, or by applying special dispensations.</span></span> <span data-ttu-id="5d499-117">이러한 접근법은 업계에 따라, 또한 한 업계(예: 통신) 내의 특정 고객 집단에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-117">These approaches can vary from industry to industry and even from a particular consumer cluster to another within one industry (for example, telecommunications).</span></span>

<span data-ttu-id="5d499-118">공통적인 요인은 비즈니스에서 이러한 특별 고객 유지 노력을 최소화해야 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-118">The common factor is that businesses need to minimize these special customer retention efforts.</span></span> <span data-ttu-id="5d499-119">따라서 모든 고객에 대해 이탈 가능성을 점수로 매겨 상위 N명에 초점을 맞추는 것이 자연스러운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-119">Thus, a natural methodology would be to score every customer with the probability of churn and address the top N ones.</span></span> <span data-ttu-id="5d499-120">상위 고객은 이탈 가능성이 가장 큰 고객일 수 있습니다. 예를 들어 더 정교한 시나리오에서는 특별 관리 후보를 선택하는 동안 이윤 함수를 채택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-120">The top customers might be the most profitable ones; for example, in more sophisticated scenarios, a profit function is employed during the selection of candidates for special dispensation.</span></span> <span data-ttu-id="5d499-121">하지만 이러한 고려 사항은 이탈을 처리하기 위한 전체적인 전략의 일부일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-121">However, these considerations are only a part of the holistic strategy for dealing with churn.</span></span> <span data-ttu-id="5d499-122">비즈니스에서는 위험(및 관련 위험 허용 범위), 개입 수준 및 비용, 타당한 고객 구분도 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-122">Businesses also have to take into account risk (and associated risk tolerance), the level and cost of the intervention, and plausible customer segmentation.</span></span>  

## <a name="industry-outlook-and-approaches"></a><span data-ttu-id="5d499-123">업계 전망 및 접근법</span><span class="sxs-lookup"><span data-stu-id="5d499-123">Industry outlook and approaches</span></span>
<span data-ttu-id="5d499-124">정교한 이탈 처리는 성숙한 산업의 표시입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-124">Sophisticated handling of churn is a sign of a mature industry.</span></span> <span data-ttu-id="5d499-125">대표적인 예로는 가입자가 공급자를 빈번히 전환하는 것으로 알려진 통신 업계를 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-125">The classic example is the telecommunications industry where subscribers are known to frequently switch from one provider to another.</span></span> <span data-ttu-id="5d499-126">이 자발적인 이탈이 주된 관심사입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-126">This voluntary churn is a prime concern.</span></span> <span data-ttu-id="5d499-127">또한 공급자는 고객 전환을 유도하는 요인인 *이탈 동인*에 대한 상당한 정보를 축적했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-127">Moreover, providers have accumulated significant knowledge about *churn drivers*, which are the factors that drive customers to switch.</span></span>

<span data-ttu-id="5d499-128">예를 들어 송수화기나 장치 선택은 휴대폰 비즈니스에서 잘 알려진 이탈 동인입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-128">For instance, handset or device choice is a well-known driver of churn in the mobile phone business.</span></span> <span data-ttu-id="5d499-129">따라서 업그레이드 시 기존 고객에게 전체 가격을 청구하면서 신규 가입자를 위해 송수화기 보조금을 지급하는 정책이 널리 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-129">As a result, a popular policy is to subsidize the price of a handset for new subscribers and charging a full price to existing customers for an upgrade.</span></span> <span data-ttu-id="5d499-130">역사적으로 이 정책은 고객이 공급자를 변경할 때 새로운 할인을 얻을 것이라고 기대하게 하고, 결국 이에 따라 공급자는 전략을 다듬어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-130">Historically, this policy has led to customers hopping from one provider to another to get a new discount, which in turn, has prompted providers to refine their strategies.</span></span>

<span data-ttu-id="5d499-131">송수화기 제품의 높은 변동성은 현재 송수화기 모델을 기반으로 한 이탈 모델이 잘못되었음을 빠르게 입증하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-131">High volatility in handset offerings is a factor that very quickly invalidates models of churn that are based on current handset models.</span></span> <span data-ttu-id="5d499-132">또한 휴대폰은 통신 장치일 뿐만 아니라 패션이며(예: iPhone) 이러한 사회적 예측 변수는 일반적인 통신 데이터 집합 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-132">Additionally, mobile phones are not only telecommunication devices; they are also fashion statements (consider the iPhone), and these social predictors are outside the scope of regular telecommunications data sets.</span></span>

<span data-ttu-id="5d499-133">모델링의 최종적인 결론은 이탈에 대한 알려진 이유를 제거함으로써 타당한 정책을 고안할 수 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-133">The net result for modeling is that you cannot devise a sound policy simply by eliminating known reasons for churn.</span></span> <span data-ttu-id="5d499-134">실제로 의사 결정 트리와 같이 범주형 변수를 수량화하는 대표적인 모델을 비롯하여 연속 모델링 전략은 **필수**입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-134">In fact, a continuous modeling strategy, including classic models that quantify categorical variables (such as decision trees), is **mandatory**.</span></span>

<span data-ttu-id="5d499-135">조직에서는 고객에 대한 빅데이터 집합을 사용하여 효과적인 문제 접근법으로 빅데이터 분석, 특히 빅데이터를 기반으로 한 이탈 감지를 수행하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-135">Using big data sets on their customers, organizations are performing big data analytics (in particular, churn detection based on big data) as an effective approach to the problem.</span></span> <span data-ttu-id="5d499-136">ETL 권장 사항 섹션에서 이탈 문제에 대한 빅데이터 접근법을 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-136">You can find more about the big data approach to the problem of churn in the Recommendations on ETL section.</span></span>  

## <a name="methodology-to-model-customer-churn"></a><span data-ttu-id="5d499-137">고객 이탈 모델링 방법</span><span class="sxs-lookup"><span data-stu-id="5d499-137">Methodology to model customer churn</span></span>
<span data-ttu-id="5d499-138">그림 1~3에서는 고객 이탈을 해결하기 위한 일반적인 문제 해결 프로세스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-138">A common problem-solving process to solve customer churn is depicted in Figures 1-3:</span></span>  

1. <span data-ttu-id="5d499-139">위험 모델에서는 작업이 가능성과 위험에 어떤 영향을 미치는지를 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-139">A risk model allows you to consider how actions affect probability and risk.</span></span>
2. <span data-ttu-id="5d499-140">개입 모델에서는 개입 수준이 이탈 가능성과 CLV(Customer Lifetime Value) 크기에 어떤 영향을 미치는지를 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-140">An intervention model allows you to consider how the level of intervention could affect the probability of churn and the amount of customer lifetime value (CLV).</span></span>
3. <span data-ttu-id="5d499-141">이 분석은 최적의 제품을 제공하기 위한 고객층을 대상으로 하는 사전 마케팅 캠페인으로 확대되는 정성 분석에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-141">This analysis lends itself to a qualitative analysis that is escalated to a proactive marketing campaign that targets customer segments to deliver the optimal offer.</span></span>  

![][1]

<span data-ttu-id="5d499-142">이러한 미래 예측 접근법은 이탈을 처리하는 가장 좋은 방법이지만 복잡성 문제가 있습니다. 따라서 다중 모델 원형을 개발하고 모델 간의 종속성을 추적해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-142">This forward looking approach is the best way to treat churn, but it comes with complexity: we have to develop a multi-model archetype and trace dependencies between the models.</span></span> <span data-ttu-id="5d499-143">모델 간의 조작은 다음 다이어그램과 같이 캡슐화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-143">The interaction among models can be encapsulated as shown in the following diagram:</span></span>  

![][2]

<span data-ttu-id="5d499-144">*그림 4: 통합 다중 모델 원형*</span><span class="sxs-lookup"><span data-stu-id="5d499-144">*Figure 4: Unified multi-model archetype*</span></span>  

<span data-ttu-id="5d499-145">고객 유지에 대한 전체적 접근법을 제공하려면 모델 간의 상호 작용이 핵심 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-145">Interaction between the models is key if we are to deliver a holistic approach to customer retention.</span></span> <span data-ttu-id="5d499-146">각 모델은 시간에 지나면서 가치가 저하되므로 아키텍처는 암시적 루프입니다(CRISP-DM 데이터 마이닝 표준, [***3***]에 의해 설정된 원형과 비슷함).</span><span class="sxs-lookup"><span data-stu-id="5d499-146">Each model necessarily degrades over time; therefore, the architecture is an implicit loop (similar to the archetype set by the CRISP-DM data mining standard, [***3***]).</span></span>  

<span data-ttu-id="5d499-147">위험 의사 결정 마케팅 구분/해체의 전체 주기는 대부분 비즈니스 문제에 적용할 수 있는 범용화된 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-147">The overall cycle of risk-decision-marketing segmentation/decomposition is still a generalized structure, which is applicable to many business problems.</span></span> <span data-ttu-id="5d499-148">이탈 분석은 간소화된 예측 솔루션을 허용하지 않는 복잡한 비즈니스 문제의 모든 특성을 보이므로 이 문제 그룹의 강력한 대표 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-148">Churn analysis is simply a strong representative of this group of problems because it exhibits all the traits of a complex business problem that does not allow a simplified predictive solution.</span></span> <span data-ttu-id="5d499-149">이탈에 대한 현대적 접근법의 사회적 측면은 접근법에서 특별히 강조되지 않지만 사회적 측면은 모든 모델에서와 같이 모델링 원형에서 캡슐화됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-149">The social aspects of the modern approach to churn are not particularly highlighted in the approach, but the social aspects are encapsulated in the modeling archetype, as they would be in any model.</span></span>  

<span data-ttu-id="5d499-150">여기서 또 다른 흥미로운 요소는 빅데이터 분석입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-150">An interesting addition here is big data analytics.</span></span> <span data-ttu-id="5d499-151">오늘날 통신 및 소매 비즈니스에서는 고객에 대한 방대한 데이터를 수집하며, 사물 인터넷(Internet of Things) 및 유비쿼터스 장치와 같이 새롭게 떠오르는 추세를 고려해 볼 때 비즈니스가 여러 계층에서 스마트 솔루션을 채택할 수 있도록 하는 다중 모델 연결에 대한 필요가 일반적인 추세가 될 것임을 쉽게 예측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-151">Today's telecommunication and retail businesses collect exhaustive data about their customers, and we can easily foresee that the need for multi-model connectivity will become a common trend, given emerging trends such as the Internet of Things and ubiquitous devices, which allow business to employ smart solutions at multiple layers.</span></span>  

 

## <a name="implementing-the-modeling-archetype-in-machine-learning-studio"></a><span data-ttu-id="5d499-152">기계 학습 스튜디오에서 모델링 원형 구현</span><span class="sxs-lookup"><span data-stu-id="5d499-152">Implementing the modeling archetype in Machine Learning Studio</span></span>
<span data-ttu-id="5d499-153">방금 설명한 문제에 대해 통합 모델링 및 점수 매기기 접근법을 구현하는 가장 좋은 방법은 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="5d499-153">Given the problem just described, what is the best way to implement an integrated modeling and scoring approach?</span></span> <span data-ttu-id="5d499-154">이 섹션에서는 Azure 기계 학습 스튜디오를 사용하여 이 작업을 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-154">In this section, we will demonstrate how we accomplished this by using Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="5d499-155">다중 모델 접근법은 이탈에 대한 전역적인 원형을 디자인할 때 필수 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-155">The multi-model approach is a must when designing a global archetype for churn.</span></span> <span data-ttu-id="5d499-156">접근법의 점수 매기기(예측) 부분도 다중 모델이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-156">Even the scoring (predictive) part of the approach should be multi-model.</span></span>  

<span data-ttu-id="5d499-157">다음 다이어그램에서는 Microsoft에서 만든, 이탈을 예측하는 데 기계 학습 스튜디오의 네 가지 점수 매기기 알고리즘을 사용하는 프로토타입을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-157">The following diagram shows the prototype we created, which employs four scoring algorithms in Machine Learning Studio to predict churn.</span></span> <span data-ttu-id="5d499-158">다중 모델 접근법은 전체 분류자를 만들어 정확도를 높일 뿐만 아니라 과잉 맞춤을 방지하고 예측 기능 선택을 개선하기 위해 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-158">The reason for using a multi-model approach is not only to create an ensemble classifier to increase accuracy, but also to protect against over-fitting and to improve prescriptive feature selection.</span></span>  

![][3]

<span data-ttu-id="5d499-159">*그림 5: 일탈 모델링 접근법의 프로토타입*</span><span class="sxs-lookup"><span data-stu-id="5d499-159">*Figure 5: Prototype of a churn modeling approach*</span></span>  

<span data-ttu-id="5d499-160">다음 섹션에서는 기계 학습 스튜디오를 사용하여 구현한 프로토타입 점수 매기기 모델에 대한 자세한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-160">The following sections provide more details about the prototype scoring model that we implemented by using Machine Learning Studio.</span></span>  

### <a name="data-selection-and-preparation"></a><span data-ttu-id="5d499-161">데이터 선택 및 준비</span><span class="sxs-lookup"><span data-stu-id="5d499-161">Data selection and preparation</span></span>
<span data-ttu-id="5d499-162">모델을 빌드하고 고객 점수를 매기는 데 사용되는 데이터는 CRM Vertical 솔루션에서 얻고 고객 개인 정보를 보호하도록 데이터가 난독 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-162">The data used to build the models and score customers was obtained from a CRM vertical solution, with the data obfuscated to protect customer privacy.</span></span> <span data-ttu-id="5d499-163">이 데이터에는 미국의 구독 회원 8,000명에 대한 정보가 포함되어 있으며, 세 가지 소스 데이터, 즉 프로비저닝 데이터(구독 메타데이터), 활동 데이터(시스템 사용) 및 고객 지원 데이터가 통합되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-163">The data contains information about 8,000 subscriptions in the U.S., and it combines three sources: provisioning data (subscription metadata), activity data (usage of the system), and customer support data.</span></span> <span data-ttu-id="5d499-164">로열티 메타데이터 또는 신용 점수와 같은 고객에 대한 비즈니스 관련 정보는 데이터에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-164">The data does not include any business related information about the customers; for example, it does not include loyalty metadata or credit scores.</span></span>  

<span data-ttu-id="5d499-165">간단히 말해 데이터 준비가 이미 다른 곳에서 완료되었다고 가정하므로 ETL 및 데이터 정리 프로세스는 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-165">For simplicity, ETL and data cleansing processes are out of scope because we assume that data preparation has already been done elsewhere.</span></span>   

<span data-ttu-id="5d499-166">모델링에 대한 기능 선택은 임의 포리스트 모듈을 사용하는 프로세스에 포함된 예측 변수 집합에 대한 사전 중요도 점수 매기기를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-166">Feature selection for modeling is based on preliminary significance scoring of the set of predictors, included in the process that uses the random forest module.</span></span> <span data-ttu-id="5d499-167">기계 학습 스튜디오에서 구현하기 위해 대표적인 기능에 대한 평균, 중앙값 및 범위를 계산했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-167">For the implementation in Machine Learning Studio, we calculated the mean, median, and ranges for representative features.</span></span> <span data-ttu-id="5d499-168">예를 들어 사용자 활동에 대한 최소값 및 최대값 같은 정성 데이터에 대한 집계를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-168">For example, we added aggregates for the qualitative data, such as minimum and maximum values for user activity.</span></span>    

<span data-ttu-id="5d499-169">또한 최근 6개월 동안의 임시 정보를 캡처했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-169">We also captured temporal information for the most recent six months.</span></span> <span data-ttu-id="5d499-170">1년 동안의 데이터를 분석하고 통계상 중요한 추세라도 6개월 후에는 이탈에 대한 영향이 크게 감소하도록 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-170">We analyzed data for one year and we established that even if there were statistically significant trends, the effect on churn is greatly diminished after six months.</span></span>  

<span data-ttu-id="5d499-171">가장 중요한 사항은 ETL, 기능 선택, 모델링을 비롯한 전체 프로세스가 Microsoft Azure에서 데이터 원본을 사용하여 기계 학습 스튜디오에서 구현되었다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-171">The most important point is that the entire process, including ETL, feature selection, and modeling was implemented in Machine Learning Studio, using data sources in Microsoft Azure.</span></span>   

<span data-ttu-id="5d499-172">다음 다이어그램에서는 사용된 데이터를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-172">The following diagrams illustrate the data that was used.</span></span>  

![][4]

<span data-ttu-id="5d499-173">*그림 6: 데이터 원본 발췌(난독 처리됨)*</span><span class="sxs-lookup"><span data-stu-id="5d499-173">*Figure 6: Excerpt of data source (obfuscated)*</span></span>  

![][5]

<span data-ttu-id="5d499-174">*그림 7: 데이터 원본에서 추출된 기능*</span><span class="sxs-lookup"><span data-stu-id="5d499-174">*Figure 7: Features extracted from data source*</span></span>
 

> <span data-ttu-id="5d499-175">이 데이터는 비공개 데이터이므로 모델 및 데이터를 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-175">Note that this data is private and therefore the model and data cannot be shared.</span></span>
> <span data-ttu-id="5d499-176">그러나 공개적으로 사용할 수 있는 데이터를 사용하는 유사한 모델의 경우 [Cortana Intelligence 갤러리](http://gallery.cortanaintelligence.com/): [Telco 고객 이탈](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383)의 이 샘플 실험을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d499-176">However, for a similar model using publicly available data, see this sample experiment in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/): [Telco Customer Churn](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383).</span></span>
> 
> <span data-ttu-id="5d499-177">Cortana Intelligence 제품군을 사용하여 변동 분석을 구현하는 방법에 대한 자세한 내용을 알아보려면 선임 프로그램 관리자인 Wee Hyong Tok의 [이 비디오](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html) 를 시청하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-177">To learn more about how you can implement a churn analysis model using Cortana Intelligence Suite, we also recommend [this video](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html) by Senior Program Manager Wee Hyong Tok.</span></span> 
> 
> 

### <a name="algorithms-used-in-the-prototype"></a><span data-ttu-id="5d499-178">프로토타입에 사용된 알고리즘</span><span class="sxs-lookup"><span data-stu-id="5d499-178">Algorithms used in the prototype</span></span>
<span data-ttu-id="5d499-179">프로토타입(사용자 지정 아님)을 빌드하는 데 사용한 네 가지 기계 학습 알고리즘은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-179">We used the following four machine learning algorithms to build the prototype (no customization):</span></span>  

1. <span data-ttu-id="5d499-180">LR(로지스틱 회귀)</span><span class="sxs-lookup"><span data-stu-id="5d499-180">Logistic regression (LR)</span></span>
2. <span data-ttu-id="5d499-181">BT(향상된 의사 결정 트리)</span><span class="sxs-lookup"><span data-stu-id="5d499-181">Boosted decision tree (BT)</span></span>
3. <span data-ttu-id="5d499-182">AP(Averaged Perceptron)</span><span class="sxs-lookup"><span data-stu-id="5d499-182">Averaged perceptron (AP)</span></span>
4. <span data-ttu-id="5d499-183">SVM(Support Vector Machine)</span><span class="sxs-lookup"><span data-stu-id="5d499-183">Support vector machine (SVM)</span></span>  

<span data-ttu-id="5d499-184">다음 다이어그램에서는 모델이 생성된 시퀀스를 나타내는 실험 디자인 화면의 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-184">The following diagram illustrates a portion of the experiment design surface, which indicates the sequence in which the models were created:</span></span>  

![][6]  

<span data-ttu-id="5d499-185">*그림 8: 기계 학습 스튜디오에서 모델 만들기*</span><span class="sxs-lookup"><span data-stu-id="5d499-185">*Figure 8: Creating models in Machine Learning Studio*</span></span>  

### <a name="scoring-methods"></a><span data-ttu-id="5d499-186">점수 매기기 방법</span><span class="sxs-lookup"><span data-stu-id="5d499-186">Scoring methods</span></span>
<span data-ttu-id="5d499-187">레이블이 지정된 학습 데이터 집합을 사용하여 네 가지 모델의 점수를 매겼습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-187">We scored the four models by using a labeled training dataset.</span></span>  

<span data-ttu-id="5d499-188">또한 데스크톱 버전의 SAS Enterprise Miner 12를 사용하여 빌드한 비교 가능한 모델에 점수 매기기 데이터 집합을 제출했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-188">We also submitted the scoring dataset to a comparable model built by using the desktop edition of SAS Enterprise Miner 12.</span></span> <span data-ttu-id="5d499-189">SAS 모델과 네 가지 기계 학습 스튜디오 모델 모두의 정확도를 측정했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-189">We measured the accuracy of the SAS model and all four Machine Learning Studio models.</span></span>  

## <a name="results"></a><span data-ttu-id="5d499-190">결과</span><span class="sxs-lookup"><span data-stu-id="5d499-190">Results</span></span>
<span data-ttu-id="5d499-191">이 섹션에서는 점수 데이터 집합에 따라 모델 정확도에 대한 결과를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-191">In this section, we present our findings about the accuracy of the models, based on the scoring dataset.</span></span>  

### <a name="accuracy-and-precision-of-scoring"></a><span data-ttu-id="5d499-192">점수 매기기의 정확도 및 정밀도</span><span class="sxs-lookup"><span data-stu-id="5d499-192">Accuracy and precision of scoring</span></span>
<span data-ttu-id="5d499-193">일반적으로 Azure 기계 학습의 구현은 정확도가 SAS보다 10~15%(AUC(Area Under Curve)) 정도 낮습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-193">Generally, the implementation in Azure Machine Learning is behind SAS in accuracy by about 10-15% (Area Under Curve or AUC).</span></span>  

<span data-ttu-id="5d499-194">그러나 이탈의 가장 중요한 메트릭은 오분류 비율입니다. 즉, 분류자를 통해 예측된 상위 N명의 이탈자 가운데 실제로 이탈하지 **않았지만** 특별 대우를 받은 비율(%)입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-194">However, the most important metric in churn is the misclassification rate: that is, of the top N churners as predicted by the classifier, which of them actually did **not** churn, and yet received special treatment?</span></span> <span data-ttu-id="5d499-195">다음 다이어그램에서는 모든 모델에 대한 이 오분류 비율을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-195">The following diagram compares this misclassification rate for all the models:</span></span>  

![][7]

<span data-ttu-id="5d499-196">*그림 9: Passau 프로토타입 AUC(Area Under Curve)*</span><span class="sxs-lookup"><span data-stu-id="5d499-196">*Figure 9: Passau prototype area under curve*</span></span>

### <a name="using-auc-to-compare-results"></a><span data-ttu-id="5d499-197">AUC를 사용하여 결과 비교</span><span class="sxs-lookup"><span data-stu-id="5d499-197">Using AUC to compare results</span></span>
<span data-ttu-id="5d499-198">AUC(Area Under Curve)는 긍정적 및 부정적 모집단에 대한 점수 분포 간에 *분리성* 의 전역 측정값을 나타내는 메트릭입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-198">Area Under Curve (AUC) is a metric that represents a global measure of *separability* between the distributions of scores for positive and negative populations.</span></span> <span data-ttu-id="5d499-199">이는 기존 ROC(Receiver Operator Characteristic) 그래프와 비슷하지만 한 가지 중요한 차이는 AUC 메트릭은 임계값을 선택할 필요가 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-199">It is similar to the traditional Receiver Operator Characteristic (ROC) graph, but one important difference is that the AUC metric does not require you to choose a threshold value.</span></span> <span data-ttu-id="5d499-200">대신에 AUC 메트릭은 **모든** 가능한 선택 항목에 대한 결과를 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-200">Instead, it summarizes the results over **all** possible choices.</span></span> <span data-ttu-id="5d499-201">이와 달리 기존 ROC 그래프는 세로축의 긍정적 비율, 가로축의 긍정적 오류 비율 및 분류 임계값을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-201">In contrast, the traditional ROC graph shows the positive rate on the vertical axis and the false positive rate on the horizontal axis, and the classification threshold varies.</span></span>   

<span data-ttu-id="5d499-202">AUC 값을 통해 모델을 비교할 수 있으므로 일반적으로 AUC는 다양한 알고리즘(또는 다양한 시스템)에 대한 가치의 측정값으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-202">AUC is generally used as a measure of worth for different algorithms (or different systems) because it allows models to be compared by means of their AUC values.</span></span> <span data-ttu-id="5d499-203">이는 기상학 및 생물공학과 같은 산업에서 일반적인 접근법입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-203">This is a popular approach in industries such as meteorology and biosciences.</span></span> <span data-ttu-id="5d499-204">따라서 AUC는 분류자 성능을 평가하는 데 널리 사용되는 대표적인 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-204">Thus, AUC represents a popular tool for assessing classifier performance.</span></span>  

### <a name="comparing-misclassification-rates"></a><span data-ttu-id="5d499-205">오분류 비율 비교</span><span class="sxs-lookup"><span data-stu-id="5d499-205">Comparing misclassification rates</span></span>
<span data-ttu-id="5d499-206">8,000여 개 구독에 대한 CRM 데이터를 사용하여 해당 데이터 집합에 대한 오분류 비율을 비교했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-206">We compared the misclassification rates on the dataset in question by using the CRM data of approximately 8,000 subscriptions.</span></span>  

* <span data-ttu-id="5d499-207">SAS 오분류 비율은 10~15%였습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-207">The SAS misclassification rate was 10-15%.</span></span>
* <span data-ttu-id="5d499-208">기계 학습 스튜디오 오분류 비율은 상위 200~300명의 이탈자에 대해 15~20%였습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-208">The Machine Learning Studio misclassification rate was 15-20% for the top 200-300 churners.</span></span>  

<span data-ttu-id="5d499-209">통신 업계에서는 안내자 서비스나 기타 특별 대우를 제공하여 이탈 위험이 가장 큰 고객에게만 초점을 맞춰야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-209">In the telecommunications industry, it is important to address only those customers who have the highest risk to churn by offering them a concierge service or other special treatment.</span></span> <span data-ttu-id="5d499-210">그 점에 있어서 기계 학습 스튜디오 구현은 SAS 모델과 같은 결과를 달성합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-210">In that respect, the Machine Learning Studio implementation achieves results on par with the SAS model.</span></span>  

<span data-ttu-id="5d499-211">주요 관심사는 잠재 이탈자를 제대로 분류하는 것이었기 때문에 같은 이유로 정확도가 정밀도보다 더 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-211">By the same token, accuracy is more important than precision because we are mostly interested in correctly classifying potential churners.</span></span>  

<span data-ttu-id="5d499-212">Wikipedia의 다음 다이어그램에서는 효과적이고 이해하기 쉬운 그래픽을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-212">The following diagram from Wikipedia depicts the relationship in a lively, easy-to-understand graphic:</span></span>  

![][8]

<span data-ttu-id="5d499-213">*그림 10: 정확도와 정밀도 간의 균형 유지*</span><span class="sxs-lookup"><span data-stu-id="5d499-213">*Figure 10: Tradeoff between accuracy and precision*</span></span>

### <a name="accuracy-and-precision-results-for-boosted-decision-tree-model"></a><span data-ttu-id="5d499-214">향상된 의사 결정 트리 모델의 정확도 및 정밀도 결과</span><span class="sxs-lookup"><span data-stu-id="5d499-214">Accuracy and precision results for boosted decision tree model</span></span>
<span data-ttu-id="5d499-215">다음 차트에는 네 가지 모델 가운데 가장 정확할 수 있는 향상된 의사 결정 트리 모델에 대해 기계 학습 프로토타입을 사용한 점수 매기기의 원시 결과가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-215">The following chart displays the raw results from scoring using the Machine Learning prototype for the boosted decision tree model, which happens to be the most accurate among the four models:</span></span>  

![][9]

<span data-ttu-id="5d499-216">*그림 11: 향상된 의사 결정 트리 모델 특성*</span><span class="sxs-lookup"><span data-stu-id="5d499-216">*Figure 11: Boosted decision tree model characteristics*</span></span>

## <a name="performance-comparison"></a><span data-ttu-id="5d499-217">성능 비교</span><span class="sxs-lookup"><span data-stu-id="5d499-217">Performance comparison</span></span>
<span data-ttu-id="5d499-218">기계 학습 스튜디오 모델과 SAS Enterprise Miner 12.1 Desktop Edition을 사용하여 생성된 비슷한 모델을 사용하여 데이터 점수를 매긴 속도를 비교했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-218">We compared the speed at which data was scored using the Machine Learning Studio models and a comparable model created by using the desktop edition of SAS Enterprise Miner 12.1.</span></span>  

<span data-ttu-id="5d499-219">다음 표에서는 알고리즘의 성능을 간략히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-219">The following table summarizes the performance of the algorithms:</span></span>  

<span data-ttu-id="5d499-220">*표 1. 알고리즘의 일반 성능(정확도)*</span><span class="sxs-lookup"><span data-stu-id="5d499-220">*Table 1. General performance (accuracy) of the algorithms*</span></span>

| <span data-ttu-id="5d499-221">LR</span><span class="sxs-lookup"><span data-stu-id="5d499-221">LR</span></span> | <span data-ttu-id="5d499-222">BT</span><span class="sxs-lookup"><span data-stu-id="5d499-222">BT</span></span> | <span data-ttu-id="5d499-223">AP</span><span class="sxs-lookup"><span data-stu-id="5d499-223">AP</span></span> | <span data-ttu-id="5d499-224">SVM</span><span class="sxs-lookup"><span data-stu-id="5d499-224">SVM</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5d499-225">평균 모델</span><span class="sxs-lookup"><span data-stu-id="5d499-225">Average Model</span></span> |<span data-ttu-id="5d499-226">최적 모델</span><span class="sxs-lookup"><span data-stu-id="5d499-226">The Best Model</span></span> |<span data-ttu-id="5d499-227">성능 미만</span><span class="sxs-lookup"><span data-stu-id="5d499-227">Underperforming</span></span> |<span data-ttu-id="5d499-228">평균 모델</span><span class="sxs-lookup"><span data-stu-id="5d499-228">Average Model</span></span> |

<span data-ttu-id="5d499-229">기계 학습 스튜디오에서 호스트된 모델은 실행 속도 성능이 SAS보다 15~25% 높았지만 정확도는 대체로 같았습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-229">The models hosted in Machine Learning Studio outperformed SAS by 15-25% for speed of execution, but accuracy was largely on par.</span></span>  

## <a name="discussion-and-recommendations"></a><span data-ttu-id="5d499-230">설명 및 권장 사항</span><span class="sxs-lookup"><span data-stu-id="5d499-230">Discussion and recommendations</span></span>
<span data-ttu-id="5d499-231">통신 업계에는 다음과 같이 이탈을 분석하기 위한 여러 가지 사례가 나타났습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-231">In the telecommunications industry, several practices have emerged to analyze churn, including:</span></span>  

* <span data-ttu-id="5d499-232">네 가지 기본 범주에 대한 메트릭을 도출합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-232">Derive metrics for four fundamental categories:</span></span>
  * <span data-ttu-id="5d499-233">**엔터티(예: 구독)**.</span><span class="sxs-lookup"><span data-stu-id="5d499-233">**Entity (for example, a subscription)**.</span></span> <span data-ttu-id="5d499-234">이탈할 가능성이 있는 구독 및/또는 고객에 대한 기본 정보를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-234">Provision basic information about the subscription and/or customer that is the subject of churn.</span></span>
  * <span data-ttu-id="5d499-235">**활동**.</span><span class="sxs-lookup"><span data-stu-id="5d499-235">**Activity**.</span></span> <span data-ttu-id="5d499-236">엔터티와 관련된 가능한 모든 사용 정보(예: 로그인 횟수)를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-236">Obtain all possible usage information that is related to the entity, for example, the number of logins.</span></span>
  * <span data-ttu-id="5d499-237">**고객 지원**.</span><span class="sxs-lookup"><span data-stu-id="5d499-237">**Customer support**.</span></span> <span data-ttu-id="5d499-238">구독에 고객 지원에 대한 조작 또는 문제가 있는지를 나타내기 위해 고객 지원 로그에서 정보를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-238">Harvest information from customer support logs to indicate whether the subscription had issues or interactions with customer support.</span></span>
  * <span data-ttu-id="5d499-239">**경쟁 및 비즈니스 데이터**.</span><span class="sxs-lookup"><span data-stu-id="5d499-239">**Competitive and business data**.</span></span> <span data-ttu-id="5d499-240">고객에 대해 가능한 모든 정보를 얻습니다(예: 사용할 수 없거나 추적하기 어려운 정보).</span><span class="sxs-lookup"><span data-stu-id="5d499-240">Obtain any information possible about the customer (for example, can be unavailable or hard to track).</span></span>
* <span data-ttu-id="5d499-241">기능 선택의 기준으로는 중요도를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-241">Use importance to drive feature selection.</span></span> <span data-ttu-id="5d499-242">이는 향상된 의사 결정 트리 모델이 항상 유망한 접근법임을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-242">This implies that the boosted decision tree model is always a promising approach.</span></span>  

<span data-ttu-id="5d499-243">이러한 네 가지 범주 사용은 이탈 위험이 있는 고객을 식별하는 데 있어 범주별로 타당한 요소에 대해 형성된 인덱스를 기반으로 하는 단순 *결정적* 접근법만으로 충분하다는 착각을 일으킵니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-243">The use of these four categories creates the illusion that a simple *deterministic* approach, based on indexes formed on reasonable factors per category, should suffice to identify customers at risk for churn.</span></span> <span data-ttu-id="5d499-244">불행히도 이 생각은 타당한 것처럼 보이지만 잘못된 이해입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-244">Unfortunately, although this notion seems plausible, it is a false understanding.</span></span> <span data-ttu-id="5d499-245">이탈은 일시적 영향이고 일반적으로 이탈을 가져오는 요인은 과도 상태이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-245">The reason is that churn is a temporal effect and the factors contributing to churn are usually in transient states.</span></span> <span data-ttu-id="5d499-246">오늘 고객이 이탈을 고려하게 하는 요인은 내일은 달라질 수 있고 지금부터 6개월 후에는 확실히 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-246">What leads a customer to consider leaving today might be different tomorrow, and it certainly will be different six months from now.</span></span> <span data-ttu-id="5d499-247">따라서 *확률적* 모델이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-247">Therefore, a *probabilistic* model is a necessity.</span></span>  

<span data-ttu-id="5d499-248">비즈니스 인텔리전스 지향 접근법이 주로 판매가 더 쉽고 직관적인 자동화를 허용하기 때문에 분석보다 이 접근법을 선호하는 비즈니스에서는 이 중요한 관찰 결과가 종종 간과됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-248">This important observation is often overlooked in business, which generally prefers a business intelligence-oriented approach to analytics, mostly because it is an easier sell and admits straightforward automation.</span></span>  

<span data-ttu-id="5d499-249">하지만 기계 학습 스튜디오를 사용한 셀프 서비스 분석에서 기대되는 것은 사업부나 부서별로 등급이 지정된 네 가지 정보 범주가 이탈에 대한 기계 학습의 중요한 출처가 된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-249">However, the promise of self-service analytics by using Machine Learning Studio is that the four categories of information, graded by division or department, become a valuable source for machine learning about churn.</span></span>  

<span data-ttu-id="5d499-250">Azure 기계 학습에서 제공되는 또 다른 흥미로운 기능은 이미 사용할 수 있는 미리 정의된 모듈의 리포지토리에 사용자 지정 모듈을 추가하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-250">Another exciting capability coming in Azure Machine Learning is the ability to add a custom module to the repository of predefined modules that are already available.</span></span> <span data-ttu-id="5d499-251">이 기능은 기본적으로 라이브러리를 선택하고 수직적 시장에 대한 템플릿을 만들 기회를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-251">This capability, essentially, creates an opportunity to select libraries and create templates for vertical markets.</span></span> <span data-ttu-id="5d499-252">이는 마켓플레이스에서 Azure 기계 학습의 중요한 차별화 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-252">It is an important differentiator of Azure Machine Learning in the market place.</span></span>  

<span data-ttu-id="5d499-253">특히 빅데이터 분석과 관련된 이 토픽은 나중에 설명할 기회가 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-253">We hope to continue this topic in the future, especially related to big data analytics.</span></span>
  

## <a name="conclusion"></a><span data-ttu-id="5d499-254">결론</span><span class="sxs-lookup"><span data-stu-id="5d499-254">Conclusion</span></span>
<span data-ttu-id="5d499-255">이 문서에서는 일반 프레임워크를 사용하여 일반적인 문제인 고객 이탈을 방지하기 위한 합리적인 접근법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-255">This paper describes a sensible approach to tackling the common problem of customer churn by using a generic framework.</span></span> <span data-ttu-id="5d499-256">점수 매기기 모델의 프로토타입을 고려하고 Azure 기계 학습을 사용하여 해당 프로토타입을 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-256">We considered a prototype for scoring models and implemented it by using Azure Machine Learning.</span></span> <span data-ttu-id="5d499-257">마지막으로 SAS의 비슷한 알고리즘과 비교하여 프로토타입 솔루션의 정확도와 성능을 평가했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-257">Finally, we assessed the accuracy and performance of the prototype solution with regard to comparable algorithms in SAS.</span></span>  

<span data-ttu-id="5d499-258">**자세한 내용은 다음을 참조하세요.**</span><span class="sxs-lookup"><span data-stu-id="5d499-258">**For more information:**</span></span>  

<span data-ttu-id="5d499-259">이 문서가 도움이 되었나요?</span><span class="sxs-lookup"><span data-stu-id="5d499-259">Did this paper help you?</span></span> <span data-ttu-id="5d499-260">사용자 의견을 보내주세요.</span><span class="sxs-lookup"><span data-stu-id="5d499-260">Please give us your feedback.</span></span> <span data-ttu-id="5d499-261">이 문서에 대한 평가를 1(기준 미달)-5(매우 우수) 등급으로 지정하고 이 등급을 지정한 이유를 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="5d499-261">Tell us on a scale of 1 (poor) to 5 (excellent), how would you rate this paper and why have you given it this rating?</span></span> <span data-ttu-id="5d499-262">예:</span><span class="sxs-lookup"><span data-stu-id="5d499-262">For example:</span></span>  

* <span data-ttu-id="5d499-263">좋은 예제, 우수한 스크린샷, 분명한 설명 또는 다른 이유 때문에 높음 등급을 지정하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="5d499-263">Are you rating it high due to having good examples, excellent screen shots, clear writing, or another reason?</span></span>
* <span data-ttu-id="5d499-264">기준 미달 예제, 애매한 스크린샷 또는 모호한 설명 때문에 낮음 등급을 지정하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="5d499-264">Are you rating it low due to poor examples, fuzzy screen shots, or unclear writing?</span></span>  

<span data-ttu-id="5d499-265">이 사용자 의견은 릴리스되는 백서의 품질을 향상하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d499-265">This feedback will help us improve the quality of white papers we release.</span></span>   

<span data-ttu-id="5d499-266">[사용자 의견 보내기](mailto:sqlfback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="5d499-266">[Send feedback](mailto:sqlfback@microsoft.com).</span></span>
 

## <a name="references"></a><span data-ttu-id="5d499-267">참조</span><span class="sxs-lookup"><span data-stu-id="5d499-267">References</span></span>
<span data-ttu-id="5d499-268">[1] Predictive Analytics: Beyond the Predictions, W. McKnight, Information Management, July/August 2011, p.18-20.</span><span class="sxs-lookup"><span data-stu-id="5d499-268">[1] Predictive Analytics: Beyond the Predictions, W. McKnight, Information Management, July/August 2011, p.18-20.</span></span>  

<span data-ttu-id="5d499-269">[2] Wikipedia 문서: [Accuracy and precision](http://en.wikipedia.org/wiki/Accuracy_and_precision)</span><span class="sxs-lookup"><span data-stu-id="5d499-269">[2] Wikipedia article: [Accuracy and precision](http://en.wikipedia.org/wiki/Accuracy_and_precision)</span></span>

<span data-ttu-id="5d499-270">[3] [CRISP-DM 1.0: Step-by-Step Data Mining Guide](http://www.the-modeling-agency.com/crisp-dm.pdf)</span><span class="sxs-lookup"><span data-stu-id="5d499-270">[3] [CRISP-DM 1.0: Step-by-Step Data Mining Guide](http://www.the-modeling-agency.com/crisp-dm.pdf)</span></span>   

<span data-ttu-id="5d499-271">[4] [Big Data Marketing: Engage Your Customers More Effectively and Drive Value](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn)</span><span class="sxs-lookup"><span data-stu-id="5d499-271">[4] [Big Data Marketing: Engage Your Customers More Effectively and Drive Value](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn)</span></span>

<span data-ttu-id="5d499-272">[5] [Cortana Intelligence 갤러리](http://gallery.cortanaintelligence.com/)의 [Telco 이탈 모델 템플릿](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5)</span><span class="sxs-lookup"><span data-stu-id="5d499-272">[5] [Telco churn model template](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5) in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)</span></span> 
 

## <a name="appendix"></a><span data-ttu-id="5d499-273">부록</span><span class="sxs-lookup"><span data-stu-id="5d499-273">Appendix</span></span>
![][10]

<span data-ttu-id="5d499-274">*그림 12: 이탈 프로토타입에 대한 프레젠테이션 스냅숏*</span><span class="sxs-lookup"><span data-stu-id="5d499-274">*Figure 12: Snapshot of a presentation on churn prototype*</span></span>

<span data-ttu-id="5d499-275">[1]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-1.png</span><span class="sxs-lookup"><span data-stu-id="5d499-275">[1]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-1.png</span></span>
<span data-ttu-id="5d499-276">[2]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-2.png</span><span class="sxs-lookup"><span data-stu-id="5d499-276">[2]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-2.png</span></span>
[3]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-3.png
[4]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-4.png
[5]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-5.png
[6]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-6.png
[7]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-7.png
[8]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-8.png
[9]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-9.png
[10]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-10.png
