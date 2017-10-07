---
title: "기계 학습을 사용 하 여 고객 변동 aaaAnalyzing | Microsoft Docs"
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
ms.openlocfilehash: 070e6a2ebe4f2fe439a42ffe1a3fa9d6d3788d62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-customer-churn-by-using-azure-machine-learning"></a><span data-ttu-id="99d74-103">Azure 기계 학습을 사용하여 고객 이탈 분석</span><span class="sxs-lookup"><span data-stu-id="99d74-103">Analyzing Customer Churn by using Azure Machine Learning</span></span>
## <a name="overview"></a><span data-ttu-id="99d74-104">개요</span><span class="sxs-lookup"><span data-stu-id="99d74-104">Overview</span></span>
<span data-ttu-id="99d74-105">이 문서에서는 Azure Machine Learning을 사용하여 빌드된 고객 이탈 분석 프로젝트의 참조 구현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-105">This article presents a reference implementation of a customer churn analysis project that is built by using Azure Machine Learning.</span></span> <span data-ttu-id="99d74-106">이 문서에서는 전체적는 산업 고객 변동 hello 문제를 해결 하는 데 관련 된 일반 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-106">In this article, we discuss associated generic models for holistically solving hello problem of industrial customer churn.</span></span> <span data-ttu-id="99d74-107">또한 기계 학습을 사용 하 여 작성 된 모델을의 hello 정확도 측정 및 평가 이후 개발 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-107">We also measure hello accuracy of models that are built by using Machine Learning, and we assess directions for further development.</span></span>  

### <a name="acknowledgements"></a><span data-ttu-id="99d74-108">감사의 말</span><span class="sxs-lookup"><span data-stu-id="99d74-108">Acknowledgements</span></span>
<span data-ttu-id="99d74-109">이 실험은 Microsoft의 수석 데이터 과학자인 Serge Berger와 이전 Microsoft Azure 기계 학습 제품 관리자인 Roger Barga가 개발하고 테스트했습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-109">This experiment was developed and tested by Serge Berger, Principal Data Scientist at Microsoft, and Roger Barga, formerly Product Manager for Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="99d74-110">hello Azure 설명서 팀 감사 히 전문 지식을 바탕으로 인해 및에이 문서를 공유 해 주셔서 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-110">hello Azure documentation team gratefully acknowledges their expertise and thanks them for sharing this white paper.</span></span>

> [!NOTE]
> <span data-ttu-id="99d74-111">이 실험에 사용 되는 hello 데이터에 공개적으로 사용할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="99d74-111">hello data used for this experiment is not publicly available.</span></span> <span data-ttu-id="99d74-112">변동 분석에 대 한 toobuild 기계 학습 모델 하는 방법의 예제를 보려면: [소매 변동 모델 템플릿](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1) 에 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com/)</span><span class="sxs-lookup"><span data-stu-id="99d74-112">For an example of how toobuild a machine learning model for churn analysis, see: [Retail churn model template](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1) in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)</span></span>
> 
> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-problem-of-customer-churn"></a><span data-ttu-id="99d74-113">고객 변동 hello 문제</span><span class="sxs-lookup"><span data-stu-id="99d74-113">hello problem of customer churn</span></span>
<span data-ttu-id="99d74-114">모든 enterprise 섹터 및 hello 소비자 시장에서 기업에는 변동와 toodeal이 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-114">Businesses in hello consumer market and in all enterprise sectors have toodeal with churn.</span></span> <span data-ttu-id="99d74-115">때때로 이탈이 지나치고 정책 의사 결정에 영향을 미칠 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-115">Sometimes churn is excessive and influences policy decisions.</span></span> <span data-ttu-id="99d74-116">hello 전통적인 솔루션 toopredict 높은 경향은 churners 이며 캠페인, 마케팅 호텔 서비스를 통해 또는 특수 dispensations 적용 하 여 해당 요구를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-116">hello traditional solution is toopredict high-propensity churners and address their needs via a concierge service, marketing campaigns, or by applying special dispensations.</span></span> <span data-ttu-id="99d74-117">이러한 접근 방식은 업계 tooindustry 뿐 한 업계 (예를 들어 telecommunications) 내에서 특정 소비자 클러스터 tooanother 에서도 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-117">These approaches can vary from industry tooindustry and even from a particular consumer cluster tooanother within one industry (for example, telecommunications).</span></span>

<span data-ttu-id="99d74-118">hello 공통적으로 적용 기업 필요로 이러한 특별 한 고객 유지 노력 toominimize 한다는입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-118">hello common factor is that businesses need toominimize these special customer retention efforts.</span></span> <span data-ttu-id="99d74-119">따라서 자연 방법론 변동 hello 확률 모든 고객 tooscore 되 고 hello 상위 n 개 항목을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-119">Thus, a natural methodology would be tooscore every customer with hello probability of churn and address hello top N ones.</span></span> <span data-ttu-id="99d74-120">hello 우수 고객 이윤이 가장 높은 것; hello 될 수 있습니다. 예를 들어 더 복잡 한 시나리오는 수익 함수 특수 분배 후보 hello 선택 하는 동안 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-120">hello top customers might be hello most profitable ones; for example, in more sophisticated scenarios, a profit function is employed during hello selection of candidates for special dispensation.</span></span> <span data-ttu-id="99d74-121">그러나 이러한 고려 사항은 변동 처리 하기 위한 hello 전체적인 전략의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-121">However, these considerations are only a part of hello holistic strategy for dealing with churn.</span></span> <span data-ttu-id="99d74-122">기업에는 또한 계정 위험 (및 관련 된 위험 허용 범위)에 tootake 사항이 hello 수준과 hello 개입 및 적당히 고객 조각화의 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-122">Businesses also have tootake into account risk (and associated risk tolerance), hello level and cost of hello intervention, and plausible customer segmentation.</span></span>  

## <a name="industry-outlook-and-approaches"></a><span data-ttu-id="99d74-123">업계 전망 및 접근법</span><span class="sxs-lookup"><span data-stu-id="99d74-123">Industry outlook and approaches</span></span>
<span data-ttu-id="99d74-124">정교한 이탈 처리는 성숙한 산업의 표시입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-124">Sophisticated handling of churn is a sign of a mature industry.</span></span> <span data-ttu-id="99d74-125">hello 전형적인 예로 hello telecommunications 업계 구독자가 공급자 tooanother에서 알려진된 toofrequently 스위치.</span><span class="sxs-lookup"><span data-stu-id="99d74-125">hello classic example is hello telecommunications industry where subscribers are known toofrequently switch from one provider tooanother.</span></span> <span data-ttu-id="99d74-126">이 자발적인 이탈이 주된 관심사입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-126">This voluntary churn is a prime concern.</span></span> <span data-ttu-id="99d74-127">또한 공급자 누적 많은 기술 자료에 대 한 *드라이버 변동*되는 hello 요소 드라이브 고객 tooswitch 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-127">Moreover, providers have accumulated significant knowledge about *churn drivers*, which are hello factors that drive customers tooswitch.</span></span>

<span data-ttu-id="99d74-128">예를 들어, 핸드셋 장치 원하는 hello 휴대폰 비즈니스의 변동의 잘 알려진 드라이버.</span><span class="sxs-lookup"><span data-stu-id="99d74-128">For instance, handset or device choice is a well-known driver of churn in hello mobile phone business.</span></span> <span data-ttu-id="99d74-129">결과적으로, 인기 있는 정책에는 새 구독자 및 전체 가격 tooexisting 업그레이드에 대 한 고객 청구에 대 한 송수화기의 toosubsidize hello 가격입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-129">As a result, a popular policy is toosubsidize hello price of a handset for new subscribers and charging a full price tooexisting customers for an upgrade.</span></span> <span data-ttu-id="99d74-130">지금까지이 정책을 차례로 화면에 표시 공급자 toorefine 고 전략이 새 할인 하나의 공급자 tooanother tooget에서 도약 toocustomers가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-130">Historically, this policy has led toocustomers hopping from one provider tooanother tooget a new discount, which in turn, has prompted providers toorefine their strategies.</span></span>

<span data-ttu-id="99d74-131">송수화기 제품의 높은 변동성은 현재 송수화기 모델을 기반으로 한 이탈 모델이 잘못되었음을 빠르게 입증하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-131">High volatility in handset offerings is a factor that very quickly invalidates models of churn that are based on current handset models.</span></span> <span data-ttu-id="99d74-132">또한 휴대폰만 통신 장치가 아닌; 값은 시간 문 (고려 hello iPhone)도 되며 이러한 소셜 예측자 일반 통신 데이터 집합의 외부 hello 범위.</span><span class="sxs-lookup"><span data-stu-id="99d74-132">Additionally, mobile phones are not only telecommunication devices; they are also fashion statements (consider hello iPhone), and these social predictors are outside hello scope of regular telecommunications data sets.</span></span>

<span data-ttu-id="99d74-133">hello 모델링 됩니다 변동에 대 한 알려진된 이유를 제거 하 여 사운드 정책 시도해 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-133">hello net result for modeling is that you cannot devise a sound policy simply by eliminating known reasons for churn.</span></span> <span data-ttu-id="99d74-134">실제로 의사 결정 트리와 같이 범주형 변수를 수량화하는 대표적인 모델을 비롯하여 연속 모델링 전략은 **필수**입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-134">In fact, a continuous modeling strategy, including classic models that quantify categorical variables (such as decision trees), is **mandatory**.</span></span>

<span data-ttu-id="99d74-135">조직에서는 큰 데이터 집합을 사용 하 여 고객에 게에, 효과적인 방법 toohello 문제로 (특히, 빅 데이터에 따라 변동 검색)의 빅 데이터 분석을 수행 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-135">Using big data sets on their customers, organizations are performing big data analytics (in particular, churn detection based on big data) as an effective approach toohello problem.</span></span> <span data-ttu-id="99d74-136">hello ETL 섹션에 맞춰져 있으며 권장 사항에에서는 변동 hello 빅 데이터 접근 방식 toohello 문제에 대 한 자세한을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-136">You can find more about hello big data approach toohello problem of churn in hello Recommendations on ETL section.</span></span>  

## <a name="methodology-toomodel-customer-churn"></a><span data-ttu-id="99d74-137">방법론 toomodel 고객 변동</span><span class="sxs-lookup"><span data-stu-id="99d74-137">Methodology toomodel customer churn</span></span>
<span data-ttu-id="99d74-138">일반적인 문제 해결 프로세스 toosolve 고객 변동은 그림 1-3에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-138">A common problem-solving process toosolve customer churn is depicted in Figures 1-3:</span></span>  

1. <span data-ttu-id="99d74-139">위험 모델 tooconsider을 사용 하면 작업 위험 및 확률에 미치는 영향입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-139">A risk model allows you tooconsider how actions affect probability and risk.</span></span>
2. <span data-ttu-id="99d74-140">개입 모델 tooconsider을 사용 하면 hello 수준의 개입 hello 확률 청크 및 hello 양이 고객 수명 가치 (CLV)의 영향을 줄 수는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-140">An intervention model allows you tooconsider how hello level of intervention could affect hello probability of churn and hello amount of customer lifetime value (CLV).</span></span>
3. <span data-ttu-id="99d74-141">이 분석은 에스컬레이션된 tooa 사전 마케팅 캠페인을 고객 세그먼트 toodeliver hello 최적의 제공 대상 tooa 정 성적 분석 인계 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-141">This analysis lends itself tooa qualitative analysis that is escalated tooa proactive marketing campaign that targets customer segments toodeliver hello optimal offer.</span></span>  

![][1]

<span data-ttu-id="99d74-142">이 과정 이라면 방법은 hello 가장 좋은 방법은 tootreat 변동을 있지만 복잡성 함께 제공: hello 모델 간의 다중 모델 아키타 및 추적 종속성 toodevelop 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-142">This forward looking approach is hello best way tootreat churn, but it comes with complexity: we have toodevelop a multi-model archetype and trace dependencies between hello models.</span></span> <span data-ttu-id="99d74-143">hello 다음 다이어그램에에서 표시 된 대로 모델 간에 hello 상호 작용을 캡슐화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-143">hello interaction among models can be encapsulated as shown in hello following diagram:</span></span>  

![][2]

<span data-ttu-id="99d74-144">*그림 4: 통합 다중 모델 원형*</span><span class="sxs-lookup"><span data-stu-id="99d74-144">*Figure 4: Unified multi-model archetype*</span></span>  

<span data-ttu-id="99d74-145">Hello 모델 간의 상호 작용에는 키 toodeliver 전체적인 접근 방식 toocustomer 보존 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-145">Interaction between hello models is key if we are toodeliver a holistic approach toocustomer retention.</span></span> <span data-ttu-id="99d74-146">각 모델; 시간에 따라 반드시 저하 따라서 hello 아키텍처는 암시적 루프 (유사한 toohello 아키타 hello CRISP-DM 데이터 마이닝 표준에 따라 설정 [***3***]).</span><span class="sxs-lookup"><span data-stu-id="99d74-146">Each model necessarily degrades over time; therefore, hello architecture is an implicit loop (similar toohello archetype set by hello CRISP-DM data mining standard, [***3***]).</span></span>  

<span data-ttu-id="99d74-147">hello 마케팅-위험-의사 결정 분할/분해의 전체 주기는 여전히 적용 가능한 toomany 비즈니스 문제는 일반화 된 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-147">hello overall cycle of risk-decision-marketing segmentation/decomposition is still a generalized structure, which is applicable toomany business problems.</span></span> <span data-ttu-id="99d74-148">변동을 분석 문제의이 그룹의 강력한 담당자 단순히 않으므로 간단한 예측 솔루션을 허용 하지 않는 복잡 한 비즈니스 문제의 모든 hello 특성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-148">Churn analysis is simply a strong representative of this group of problems because it exhibits all hello traits of a complex business problem that does not allow a simplified predictive solution.</span></span> <span data-ttu-id="99d74-149">hello 소셜 hello 최신 접근 방식 toochurn의 측면 특히 hello 접근 방식에서 강조 표시 되지 않습니다 되지만 모델에서와 같이 hello 소셜 측면 hello 모델링 아키타에 캡슐화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-149">hello social aspects of hello modern approach toochurn are not particularly highlighted in hello approach, but hello social aspects are encapsulated in hello modeling archetype, as they would be in any model.</span></span>  

<span data-ttu-id="99d74-150">여기서 또 다른 흥미로운 요소는 빅데이터 분석입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-150">An interesting addition here is big data analytics.</span></span> <span data-ttu-id="99d74-151">오늘날의 통신 및 소매 비즈니스 고객에 게에 대 한 철저 한 데이터를 수집 하 고 해당 hello 필요한 연결 다중 모델은 일반적인 추세를 제공 추세와 같은 새로운 될 것에 대 한 hello 사물 인터넷 쉽게 수 것으로 예상 하 고 유비쿼터스 된 장치에 여러 계층에서 비즈니스 tooemploy 스마트 솔루션을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-151">Today's telecommunication and retail businesses collect exhaustive data about their customers, and we can easily foresee that hello need for multi-model connectivity will become a common trend, given emerging trends such as hello Internet of Things and ubiquitous devices, which allow business tooemploy smart solutions at multiple layers.</span></span>  

 

## <a name="implementing-hello-modeling-archetype-in-machine-learning-studio"></a><span data-ttu-id="99d74-152">기계 학습 스튜디오에서 아키타 모델링 hello 구현</span><span class="sxs-lookup"><span data-stu-id="99d74-152">Implementing hello modeling archetype in Machine Learning Studio</span></span>
<span data-ttu-id="99d74-153">방금 설명한 hello 문제가 들어 이란 hello 가장 좋은 방법은 tooimplement 통합된 모델링 및 점수 매기기 방법</span><span class="sxs-lookup"><span data-stu-id="99d74-153">Given hello problem just described, what is hello best way tooimplement an integrated modeling and scoring approach?</span></span> <span data-ttu-id="99d74-154">이 섹션에서는 Azure 기계 학습 스튜디오를 사용하여 이 작업을 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-154">In this section, we will demonstrate how we accomplished this by using Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="99d74-155">hello 다중 모델 방법은 필수인 변동에 대 한 전역 아키타를 디자인 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-155">hello multi-model approach is a must when designing a global archetype for churn.</span></span> <span data-ttu-id="99d74-156">Hello 방식의 (예측) 부분 점수 매기기에 hello 다중 모델 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-156">Even hello scoring (predictive) part of hello approach should be multi-model.</span></span>  

<span data-ttu-id="99d74-157">hello 다음 그림에 hello 프로토타입 기계 학습 스튜디오 toopredict 변동의 점수 매기기 알고리즘 4 개를 사용 하는 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-157">hello following diagram shows hello prototype we created, which employs four scoring algorithms in Machine Learning Studio toopredict churn.</span></span> <span data-ttu-id="99d74-158">hello 다중 모델 접근 방식을 사용 하는 앙상블 분류자 tooincrease 정확도 toocreate 뿐만 아니라 tooprotect 과잉 맞춤이 및 tooimprove 규범적인 기능 선택에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-158">hello reason for using a multi-model approach is not only toocreate an ensemble classifier tooincrease accuracy, but also tooprotect against over-fitting and tooimprove prescriptive feature selection.</span></span>  

![][3]

<span data-ttu-id="99d74-159">*그림 5: 일탈 모델링 접근법의 프로토타입*</span><span class="sxs-lookup"><span data-stu-id="99d74-159">*Figure 5: Prototype of a churn modeling approach*</span></span>  

<span data-ttu-id="99d74-160">hello 다음 섹션에서는 기계 학습 스튜디오를 사용 하 여 구현한 모델 점수 매기기 hello 프로토타입에 대 한 자세한 정보.</span><span class="sxs-lookup"><span data-stu-id="99d74-160">hello following sections provide more details about hello prototype scoring model that we implemented by using Machine Learning Studio.</span></span>  

### <a name="data-selection-and-preparation"></a><span data-ttu-id="99d74-161">데이터 선택 및 준비</span><span class="sxs-lookup"><span data-stu-id="99d74-161">Data selection and preparation</span></span>
<span data-ttu-id="99d74-162">hello 데이터 toobuild hello 모델을 사용 하 고 hello 난독 처리 하는 데이터 tooprotect 고객 개인 정보 점수 고객 CRM 세로 솔루션에서 얻을 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-162">hello data used toobuild hello models and score customers was obtained from a CRM vertical solution, with hello data obfuscated tooprotect customer privacy.</span></span> <span data-ttu-id="99d74-163">hello 데이터 포함 hello 미국의 8, 000 구독에 대 한 정보 되 고 결합 하 여 세 개의 소스: 데이터 (구독 메타 데이터), 활동 데이터 (hello 시스템 사용) 및 고객 지원 데이터를 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-163">hello data contains information about 8,000 subscriptions in hello U.S., and it combines three sources: provisioning data (subscription metadata), activity data (usage of hello system), and customer support data.</span></span> <span data-ttu-id="99d74-164">hello 데이터에는 모든 비즈니스 관련 hello 고객;에 대 한 정보 예를 들어 충성도 메타 데이터 / 신용 점수는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-164">hello data does not include any business related information about hello customers; for example, it does not include loyalty metadata or credit scores.</span></span>  

<span data-ttu-id="99d74-165">간단히 말해 데이터 준비가 이미 다른 곳에서 완료되었다고 가정하므로 ETL 및 데이터 정리 프로세스는 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-165">For simplicity, ETL and data cleansing processes are out of scope because we assume that data preparation has already been done elsewhere.</span></span>   

<span data-ttu-id="99d74-166">모델링에 대해 기능 선택을 기반으로 한 예측자를 hello 임의 포리스트 모듈을 사용 하는 hello 프로세스에 포함 된 hello 집합의 점수 매기기 예비 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-166">Feature selection for modeling is based on preliminary significance scoring of hello set of predictors, included in hello process that uses hello random forest module.</span></span> <span data-ttu-id="99d74-167">기계 학습 스튜디오에서 hello 구현에 대 한 hello 평균값, 중앙값, 및 대표 기능에 대 한 범위를 계산 했습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-167">For hello implementation in Machine Learning Studio, we calculated hello mean, median, and ranges for representative features.</span></span> <span data-ttu-id="99d74-168">예를 들어, 사용자 활동에 대 한 최소 및 최대 값과 같은 hello 질적 데이터에 대 한 집계를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-168">For example, we added aggregates for hello qualitative data, such as minimum and maximum values for user activity.</span></span>    

<span data-ttu-id="99d74-169">또한 가장 최근 6 개월 hello에 대 한 임시 정보를 캡처 했습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-169">We also captured temporal information for hello most recent six months.</span></span> <span data-ttu-id="99d74-170">1 년 동안 데이터를 분석 했습니다 하 고는 통계적으로 중요 한 추세 인 경우에 변동에 hello 영향이 크게 감소 6 개월 후를 설정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-170">We analyzed data for one year and we established that even if there were statistically significant trends, hello effect on churn is greatly diminished after six months.</span></span>  

<span data-ttu-id="99d74-171">hello 가장 중요 한 점은 해당 hello 전체 포함 하는 프로세스 ETL, 기능 선택 하 고 모델링 기계 학습 스튜디오에서는 Microsoft Azure에서 데이터 원본을 사용 하 여 구현 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-171">hello most important point is that hello entire process, including ETL, feature selection, and modeling was implemented in Machine Learning Studio, using data sources in Microsoft Azure.</span></span>   

<span data-ttu-id="99d74-172">hello 다음 다이어그램에서는 사용 된 hello 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-172">hello following diagrams illustrate hello data that was used.</span></span>  

![][4]

<span data-ttu-id="99d74-173">*그림 6: 데이터 원본 발췌(난독 처리됨)*</span><span class="sxs-lookup"><span data-stu-id="99d74-173">*Figure 6: Excerpt of data source (obfuscated)*</span></span>  

![][5]

<span data-ttu-id="99d74-174">*그림 7: 데이터 원본에서 추출된 기능*</span><span class="sxs-lookup"><span data-stu-id="99d74-174">*Figure 7: Features extracted from data source*</span></span>
 

> <span data-ttu-id="99d74-175">Note는이 데이터는 전용 포트 이며 따라서 hello 모델 및 데이터를 공유할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-175">Note that this data is private and therefore hello model and data cannot be shared.</span></span>
> <span data-ttu-id="99d74-176">그러나 공개적으로 사용할 수 있는 데이터를 사용 하 여 비슷한 모델을이 샘플 실험을 hello 참조 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com/): [Telco 고객 변동](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383)합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-176">However, for a similar model using publicly available data, see this sample experiment in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/): [Telco Customer Churn](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383).</span></span>
> 
> <span data-ttu-id="99d74-177">Cortana 인텔리전스 Suite를 사용 하 여 변동을 분석 모델을 구현 하는 방법에 대 한 자세한 toolearn, 것도 좋습니다 [이 비디오](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html) 수석 프로그램 관리자 Wee Hyong Tok 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-177">toolearn more about how you can implement a churn analysis model using Cortana Intelligence Suite, we also recommend [this video](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html) by Senior Program Manager Wee Hyong Tok.</span></span> 
> 
> 

### <a name="algorithms-used-in-hello-prototype"></a><span data-ttu-id="99d74-178">Hello 프로토타입에 사용 되는 알고리즘</span><span class="sxs-lookup"><span data-stu-id="99d74-178">Algorithms used in hello prototype</span></span>
<span data-ttu-id="99d74-179">다음 4 개의 기계 학습 알고리즘 hello 사용 toobuild hello 프로토타입 (사용자 지정):</span><span class="sxs-lookup"><span data-stu-id="99d74-179">We used hello following four machine learning algorithms toobuild hello prototype (no customization):</span></span>  

1. <span data-ttu-id="99d74-180">LR(로지스틱 회귀)</span><span class="sxs-lookup"><span data-stu-id="99d74-180">Logistic regression (LR)</span></span>
2. <span data-ttu-id="99d74-181">BT(향상된 의사 결정 트리)</span><span class="sxs-lookup"><span data-stu-id="99d74-181">Boosted decision tree (BT)</span></span>
3. <span data-ttu-id="99d74-182">AP(Averaged Perceptron)</span><span class="sxs-lookup"><span data-stu-id="99d74-182">Averaged perceptron (AP)</span></span>
4. <span data-ttu-id="99d74-183">SVM(Support Vector Machine)</span><span class="sxs-lookup"><span data-stu-id="99d74-183">Support vector machine (SVM)</span></span>  

<span data-ttu-id="99d74-184">hello 다음 다이어그램에서는 일부는 hello 모델 생성 된 hello 순서를 나타내는 hello 실험 디자인 화면에서를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-184">hello following diagram illustrates a portion of hello experiment design surface, which indicates hello sequence in which hello models were created:</span></span>  

![][6]  

<span data-ttu-id="99d74-185">*그림 8: 기계 학습 스튜디오에서 모델 만들기*</span><span class="sxs-lookup"><span data-stu-id="99d74-185">*Figure 8: Creating models in Machine Learning Studio*</span></span>  

### <a name="scoring-methods"></a><span data-ttu-id="99d74-186">점수 매기기 방법</span><span class="sxs-lookup"><span data-stu-id="99d74-186">Scoring methods</span></span>
<span data-ttu-id="99d74-187">레이블이 지정 된 학습 데이터 집합을 사용 하 여 4 hello 모델 점수가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-187">We scored hello four models by using a labeled training dataset.</span></span>  

<span data-ttu-id="99d74-188">또한 hello SAS Enterprise 마이너 12의 데스크톱 버전을 사용 하 여 작성 된 데이터 집합 tooa 비교 가능한 모델 점수 매기기 hello을 제출 했습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-188">We also submitted hello scoring dataset tooa comparable model built by using hello desktop edition of SAS Enterprise Miner 12.</span></span> <span data-ttu-id="99d74-189">Hello SAS 모델 및 모든 4 개의 기계 학습 스튜디오 모델의 hello 정확도 측정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-189">We measured hello accuracy of hello SAS model and all four Machine Learning Studio models.</span></span>  

## <a name="results"></a><span data-ttu-id="99d74-190">결과</span><span class="sxs-lookup"><span data-stu-id="99d74-190">Results</span></span>
<span data-ttu-id="99d74-191">이 섹션에서는 데이터 집합 점수 매기기 hello를 기반으로 hello 모델의 정확도 hello에 대 한 우리의 연구 결과 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-191">In this section, we present our findings about hello accuracy of hello models, based on hello scoring dataset.</span></span>  

### <a name="accuracy-and-precision-of-scoring"></a><span data-ttu-id="99d74-192">점수 매기기의 정확도 및 정밀도</span><span class="sxs-lookup"><span data-stu-id="99d74-192">Accuracy and precision of scoring</span></span>
<span data-ttu-id="99d74-193">일반적으로 Azure 기계 학습에서 hello 구현이 SAS 뒤의 약 10-15% (곡선 아래의 영역 또는 AUC) 정확도 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-193">Generally, hello implementation in Azure Machine Learning is behind SAS in accuracy by about 10-15% (Area Under Curve or AUC).</span></span>  

<span data-ttu-id="99d74-194">그러나 변동의 hello 가장 중요 한 메트릭을 hello 오 분류 속도: 즉, 상위 n 개 churners hello 분류자에서 예측으로 hello의 있는 실제로 수행한 **하지** , 변경 및 특별 한 처리를 아직 받지? hello 다음 다이어그램에서는 모든 hello 모델에 대 한이 오 분류 비율을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-194">However, hello most important metric in churn is hello misclassification rate: that is, of hello top N churners as predicted by hello classifier, which of them actually did **not** churn, and yet received special treatment? hello following diagram compares this misclassification rate for all hello models:</span></span>  

![][7]

<span data-ttu-id="99d74-195">*그림 9: Passau 프로토타입 AUC(Area Under Curve)*</span><span class="sxs-lookup"><span data-stu-id="99d74-195">*Figure 9: Passau prototype area under curve*</span></span>

### <a name="using-auc-toocompare-results"></a><span data-ttu-id="99d74-196">AUC toocompare 결과 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="99d74-196">Using AUC toocompare results</span></span>
<span data-ttu-id="99d74-197">영역에서 곡선 (AUC)은 전역 측정 한 값을 나타내는 메트릭입니다 *separability* 양수 및 음수 모집단에 대 한 점수의 hello 배포판 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-197">Area Under Curve (AUC) is a metric that represents a global measure of *separability* between hello distributions of scores for positive and negative populations.</span></span> <span data-ttu-id="99d74-198">비슷한 toohello 기존 수신기 연산자 특성 (ROC) 그래프에서 하지만 중요 한 차이점 해당 hello AUC 메트릭이 않습니다 toochoose 임계값 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-198">It is similar toohello traditional Receiver Operator Characteristic (ROC) graph, but one important difference is that hello AUC metric does not require you toochoose a threshold value.</span></span> <span data-ttu-id="99d74-199">대신, 통해 hello 결과 요약 하기 **모든** 가능한 선택 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-199">Instead, it summarizes hello results over **all** possible choices.</span></span> <span data-ttu-id="99d74-200">반면, hello 기존의 ROC 그래프 hello 세로 축 및 hello false 양의 속도 hello 가로 축에에 hello 양의 속도 표시 하 고 hello 분류 임계값 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-200">In contrast, hello traditional ROC graph shows hello positive rate on hello vertical axis and hello false positive rate on hello horizontal axis, and hello classification threshold varies.</span></span>   

<span data-ttu-id="99d74-201">일반적으로 AUC는 모델 toobe AUC 값을 사용 하 여 비교할 수 있기 때문에 서로 다른 알고리즘 (또는 다른 시스템)에 대 한 주요 측정값으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-201">AUC is generally used as a measure of worth for different algorithms (or different systems) because it allows models toobe compared by means of their AUC values.</span></span> <span data-ttu-id="99d74-202">이는 기상학 및 생물공학과 같은 산업에서 일반적인 접근법입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-202">This is a popular approach in industries such as meteorology and biosciences.</span></span> <span data-ttu-id="99d74-203">따라서 AUC는 분류자 성능을 평가하는 데 널리 사용되는 대표적인 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-203">Thus, AUC represents a popular tool for assessing classifier performance.</span></span>  

### <a name="comparing-misclassification-rates"></a><span data-ttu-id="99d74-204">오분류 비율 비교</span><span class="sxs-lookup"><span data-stu-id="99d74-204">Comparing misclassification rates</span></span>
<span data-ttu-id="99d74-205">약 8, 000 구독 hello CRM 데이터를 사용 하 여 hello 오 분류 속도 hello 데이터 집합을 비교 했습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-205">We compared hello misclassification rates on hello dataset in question by using hello CRM data of approximately 8,000 subscriptions.</span></span>  

* <span data-ttu-id="99d74-206">hello SAS 오 분류 속도 10-15%입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-206">hello SAS misclassification rate was 10-15%.</span></span>
* <span data-ttu-id="99d74-207">hello 기계 학습 스튜디오 오 분류 속도 상위 200-300 churners hello에 대 한 15-20%입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-207">hello Machine Learning Studio misclassification rate was 15-20% for hello top 200-300 churners.</span></span>  

<span data-ttu-id="99d74-208">Hello telecommunications 업계에서 있는 고객 호텔 서비스 또는 다른 특별 한 처리를 제공 하 여 가장 높은 위험 toochurn hello만 중요 한 tooaddress입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-208">In hello telecommunications industry, it is important tooaddress only those customers who have hello highest risk toochurn by offering them a concierge service or other special treatment.</span></span> <span data-ttu-id="99d74-209">이러한 측면에서는 hello 기계 학습 스튜디오 구현 hello SAS 모델 수준의 맞춤형는 결과를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-209">In that respect, hello Machine Learning Studio implementation achieves results on par with hello SAS model.</span></span>  

<span data-ttu-id="99d74-210">Hello 하 여 동일한 토큰을 정확도 전체 자릿수 보다 더 중요 한 잠재적인 churners 잘못 분류에 주로 관심이 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-210">By hello same token, accuracy is more important than precision because we are mostly interested in correctly classifying potential churners.</span></span>  

<span data-ttu-id="99d74-211">Wikipedia에서 다이어그램을 다음 hello 역동적인, 이해 하기 쉬운 그래픽에서 hello 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-211">hello following diagram from Wikipedia depicts hello relationship in a lively, easy-to-understand graphic:</span></span>  

![][8]

<span data-ttu-id="99d74-212">*그림 10: 정확도와 정밀도 간의 균형 유지*</span><span class="sxs-lookup"><span data-stu-id="99d74-212">*Figure 10: Tradeoff between accuracy and precision*</span></span>

### <a name="accuracy-and-precision-results-for-boosted-decision-tree-model"></a><span data-ttu-id="99d74-213">향상된 의사 결정 트리 모델의 정확도 및 정밀도 결과</span><span class="sxs-lookup"><span data-stu-id="99d74-213">Accuracy and precision results for boosted decision tree model</span></span>
<span data-ttu-id="99d74-214">다음 차트 표시 hello 원시 hello toobe hello hello 4 개의 모델 간에 가장 정확 하 게 발생 하는 hello 승격 된 의사 결정 트리 모델에 대 한 hello 기계 학습 프로토타입을 사용 하 여 점수 매기기에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-214">hello following chart displays hello raw results from scoring using hello Machine Learning prototype for hello boosted decision tree model, which happens toobe hello most accurate among hello four models:</span></span>  

![][9]

<span data-ttu-id="99d74-215">*그림 11: 향상된 의사 결정 트리 모델 특성*</span><span class="sxs-lookup"><span data-stu-id="99d74-215">*Figure 11: Boosted decision tree model characteristics*</span></span>

## <a name="performance-comparison"></a><span data-ttu-id="99d74-216">성능 비교</span><span class="sxs-lookup"><span data-stu-id="99d74-216">Performance comparison</span></span>
<span data-ttu-id="99d74-217">데이터 hello 기계 학습 스튜디오 모델과 비교 가능한 SAS Enterprise 마이너 12.1 hello 데스크톱 버전을 사용 하 여 만든 모델을 사용 하 여을 획득 된 hello 속도 비교 했습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-217">We compared hello speed at which data was scored using hello Machine Learning Studio models and a comparable model created by using hello desktop edition of SAS Enterprise Miner 12.1.</span></span>  

<span data-ttu-id="99d74-218">다음 표에 hello hello 알고리즘의 hello 성능을 요약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-218">hello following table summarizes hello performance of hello algorithms:</span></span>  

<span data-ttu-id="99d74-219">*표 1. Hello 알고리즘의 일반적인 성능 (정확도)*</span><span class="sxs-lookup"><span data-stu-id="99d74-219">*Table 1. General performance (accuracy) of hello algorithms*</span></span>

| <span data-ttu-id="99d74-220">LR</span><span class="sxs-lookup"><span data-stu-id="99d74-220">LR</span></span> | <span data-ttu-id="99d74-221">BT</span><span class="sxs-lookup"><span data-stu-id="99d74-221">BT</span></span> | <span data-ttu-id="99d74-222">AP</span><span class="sxs-lookup"><span data-stu-id="99d74-222">AP</span></span> | <span data-ttu-id="99d74-223">SVM</span><span class="sxs-lookup"><span data-stu-id="99d74-223">SVM</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="99d74-224">평균 모델</span><span class="sxs-lookup"><span data-stu-id="99d74-224">Average Model</span></span> |<span data-ttu-id="99d74-225">hello 최상의 모델</span><span class="sxs-lookup"><span data-stu-id="99d74-225">hello Best Model</span></span> |<span data-ttu-id="99d74-226">성능 미만</span><span class="sxs-lookup"><span data-stu-id="99d74-226">Underperforming</span></span> |<span data-ttu-id="99d74-227">평균 모델</span><span class="sxs-lookup"><span data-stu-id="99d74-227">Average Model</span></span> |

<span data-ttu-id="99d74-228">par 크게 달라 실적이 우수 했습니다 SAS를 실행 하지만 정확도의 속도 대 한 15 25%가 기계 학습 스튜디오에서 호스트 되는 hello 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-228">hello models hosted in Machine Learning Studio outperformed SAS by 15-25% for speed of execution, but accuracy was largely on par.</span></span>  

## <a name="discussion-and-recommendations"></a><span data-ttu-id="99d74-229">설명 및 권장 사항</span><span class="sxs-lookup"><span data-stu-id="99d74-229">Discussion and recommendations</span></span>
<span data-ttu-id="99d74-230">Hello telecommunications 업계의 몇 가지 사례 tooanalyze 늘어났습니다 변동를 포함 하 여:</span><span class="sxs-lookup"><span data-stu-id="99d74-230">In hello telecommunications industry, several practices have emerged tooanalyze churn, including:</span></span>  

* <span data-ttu-id="99d74-231">네 가지 기본 범주에 대한 메트릭을 도출합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-231">Derive metrics for four fundamental categories:</span></span>
  * <span data-ttu-id="99d74-232">**엔터티(예: 구독)**.</span><span class="sxs-lookup"><span data-stu-id="99d74-232">**Entity (for example, a subscription)**.</span></span> <span data-ttu-id="99d74-233">Hello 구독 및/또는 변동의 hello 주제는 고객에 대 한 기본 정보를 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-233">Provision basic information about hello subscription and/or customer that is hello subject of churn.</span></span>
  * <span data-ttu-id="99d74-234">**활동**.</span><span class="sxs-lookup"><span data-stu-id="99d74-234">**Activity**.</span></span> <span data-ttu-id="99d74-235">예를 들어 hello 수가 로그인 관련된 toohello 엔터티에 있는 모든 가능한 사용 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-235">Obtain all possible usage information that is related toohello entity, for example, hello number of logins.</span></span>
  * <span data-ttu-id="99d74-236">**고객 지원**.</span><span class="sxs-lookup"><span data-stu-id="99d74-236">**Customer support**.</span></span> <span data-ttu-id="99d74-237">Hello 구독 있어 문제점 또는 고객와의 상호 작용을 지원 하는지 여부를 고객 지원 로그 tooindicate에서 정보를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-237">Harvest information from customer support logs tooindicate whether hello subscription had issues or interactions with customer support.</span></span>
  * <span data-ttu-id="99d74-238">**경쟁 및 비즈니스 데이터**.</span><span class="sxs-lookup"><span data-stu-id="99d74-238">**Competitive and business data**.</span></span> <span data-ttu-id="99d74-239">Hello 고객에 대 한 가능한 모든 정보 (예를 들어 가능 사용 불가능 하거나 하드 tootrack).</span><span class="sxs-lookup"><span data-stu-id="99d74-239">Obtain any information possible about hello customer (for example, can be unavailable or hard tootrack).</span></span>
* <span data-ttu-id="99d74-240">중요도 toodrive 기능 선택을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-240">Use importance toodrive feature selection.</span></span> <span data-ttu-id="99d74-241">이 hello 승격 된 의사 결정 트리 모델은 항상 성공할 가능성이 접근 방식을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-241">This implies that hello boosted decision tree model is always a promising approach.</span></span>  

<span data-ttu-id="99d74-242">hello 사용 하 여 이러한 네 가지 범주의 hello 감 하는 만드는 간단한 *결정적* 범주별 적절 한 요소에 구성 하는 인덱스에 따라 접근 방식을 tooidentify 고객 변동에 대 한 위험에는 충분 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-242">hello use of these four categories creates hello illusion that a simple *deterministic* approach, based on indexes formed on reasonable factors per category, should suffice tooidentify customers at risk for churn.</span></span> <span data-ttu-id="99d74-243">불행히도 이 생각은 타당한 것처럼 보이지만 잘못된 이해입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-243">Unfortunately, although this notion seems plausible, it is a false understanding.</span></span> <span data-ttu-id="99d74-244">hello 이유는 변동은 임시 효과 toochurn hello 요인은 일반적으로 임시 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-244">hello reason is that churn is a temporal effect and hello factors contributing toochurn are usually in transient states.</span></span> <span data-ttu-id="99d74-245">고객 tooconsider 두면 오늘 하면 다를 수 있습니다 내일 고 확실히 됩니다 다른 6 개월 지금부터 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-245">What leads a customer tooconsider leaving today might be different tomorrow, and it certainly will be different six months from now.</span></span> <span data-ttu-id="99d74-246">따라서 *확률적* 모델이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-246">Therefore, a *probabilistic* model is a necessity.</span></span>  

<span data-ttu-id="99d74-247">일반적으로 비즈니스 인텔리전스 지향 접근 방식 tooanalytics이 선호 하는 비즈니스에 중요 한 관찰이 종종 간과 되, 이기 때문에 대부분는 판매 쉽고 간단 하 게 자동화 입 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-247">This important observation is often overlooked in business, which generally prefers a business intelligence-oriented approach tooanalytics, mostly because it is an easier sell and admits straightforward automation.</span></span>  

<span data-ttu-id="99d74-248">그러나 기계 학습 스튜디오를 사용 하 여 셀프 서비스 분석에 대 한 hello 약속 부문 또는 부서, 그레이드할 정보의 hello 네 가지 범주는 하다는 것 변동에 대 한 기계 학습에 중요 한 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-248">However, hello promise of self-service analytics by using Machine Learning Studio is that hello four categories of information, graded by division or department, become a valuable source for machine learning about churn.</span></span>  

<span data-ttu-id="99d74-249">Azure 기계 학습에 방문 하 고 다른 흥미로운 기능은 hello 기능 tooadd 이미 사용할 수 있는 미리 정의 된 모듈의 사용자 지정 모듈 toohello 저장소 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-249">Another exciting capability coming in Azure Machine Learning is hello ability tooadd a custom module toohello repository of predefined modules that are already available.</span></span> <span data-ttu-id="99d74-250">이 기능을 기본적으로, 기회 tooselect 라이브러리 만들고 수직적 시장에 사용할 템플릿을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-250">This capability, essentially, creates an opportunity tooselect libraries and create templates for vertical markets.</span></span> <span data-ttu-id="99d74-251">Azure 기계 학습의 hello 마켓플레이스를 구별 하는 중요 한 요소인 것합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-251">It is an important differentiator of Azure Machine Learning in hello market place.</span></span>  

<span data-ttu-id="99d74-252">이 항목을 hello 이후, 특히 관련 toobig 데이터 분석 toocontinue 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-252">We hope toocontinue this topic in hello future, especially related toobig data analytics.</span></span>
  

## <a name="conclusion"></a><span data-ttu-id="99d74-253">결론</span><span class="sxs-lookup"><span data-stu-id="99d74-253">Conclusion</span></span>
<span data-ttu-id="99d74-254">이 문서에서는 일반 프레임 워크를 사용 하 여 고객 변동의 합리적 tootackling hello 일반적인 문제를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-254">This paper describes a sensible approach tootackling hello common problem of customer churn by using a generic framework.</span></span> <span data-ttu-id="99d74-255">점수 매기기 모델의 프로토타입을 고려하고 Azure 기계 학습을 사용하여 해당 프로토타입을 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-255">We considered a prototype for scoring models and implemented it by using Azure Machine Learning.</span></span> <span data-ttu-id="99d74-256">마지막으로, 큰지에 toocomparable 알고리즘에 따라 SAS 사용 하 여 hello 프로토타입 솔루션의 성능과 hello 정확도 평가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-256">Finally, we assessed hello accuracy and performance of hello prototype solution with regard toocomparable algorithms in SAS.</span></span>  

<span data-ttu-id="99d74-257">**자세한 내용은 다음을 참조하세요.**</span><span class="sxs-lookup"><span data-stu-id="99d74-257">**For more information:**</span></span>  

<span data-ttu-id="99d74-258">이 문서가 도움이 되었나요?</span><span class="sxs-lookup"><span data-stu-id="99d74-258">Did this paper help you?</span></span> <span data-ttu-id="99d74-259">사용자 의견을 보내주세요.</span><span class="sxs-lookup"><span data-stu-id="99d74-259">Please give us your feedback.</span></span> <span data-ttu-id="99d74-260">값 1 (나쁨) too5 (점 높음) 중 하나를 알려,이 문서를 평가해 주시기 및 이유 지정 했을 수 이러한 등급?</span><span class="sxs-lookup"><span data-stu-id="99d74-260">Tell us on a scale of 1 (poor) too5 (excellent), how would you rate this paper and why have you given it this rating?</span></span> <span data-ttu-id="99d74-261">예:</span><span class="sxs-lookup"><span data-stu-id="99d74-261">For example:</span></span>  

* <span data-ttu-id="99d74-262">점수를 주 시겠습니까 기한 toohaving 좋은 예, 뛰어난 스크린 샷, 명료한 또는 다른 이유로 높은?</span><span class="sxs-lookup"><span data-stu-id="99d74-262">Are you rating it high due toohaving good examples, excellent screen shots, clear writing, or another reason?</span></span>
* <span data-ttu-id="99d74-263">점수를 주 시겠습니까 기한 toopoor 예제, 유사 항목 스크린 샷 또는 명확 하지 않은 쓰기 낮은?</span><span class="sxs-lookup"><span data-stu-id="99d74-263">Are you rating it low due toopoor examples, fuzzy screen shots, or unclear writing?</span></span>  

<span data-ttu-id="99d74-264">이 피드백 hello 배포 하는 백서의 품질을 개선 하는 데는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-264">This feedback will help us improve hello quality of white papers we release.</span></span>   

<span data-ttu-id="99d74-265">[사용자 의견 보내기](mailto:sqlfback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="99d74-265">[Send feedback](mailto:sqlfback@microsoft.com).</span></span>
 

## <a name="references"></a><span data-ttu-id="99d74-266">참조</span><span class="sxs-lookup"><span data-stu-id="99d74-266">References</span></span>
<span data-ttu-id="99d74-267">[1] 예측 분석: McKnight, 정보 관리 년 7 월/년 8 월 2011 년 p.18-20 W. hello 예측을 초과 합니다.</span><span class="sxs-lookup"><span data-stu-id="99d74-267">[1] Predictive Analytics: Beyond hello Predictions, W. McKnight, Information Management, July/August 2011, p.18-20.</span></span>  

<span data-ttu-id="99d74-268">[2] Wikipedia 문서: [Accuracy and precision](http://en.wikipedia.org/wiki/Accuracy_and_precision)</span><span class="sxs-lookup"><span data-stu-id="99d74-268">[2] Wikipedia article: [Accuracy and precision](http://en.wikipedia.org/wiki/Accuracy_and_precision)</span></span>

<span data-ttu-id="99d74-269">[3] [CRISP-DM 1.0: Step-by-Step Data Mining Guide](http://www.the-modeling-agency.com/crisp-dm.pdf)</span><span class="sxs-lookup"><span data-stu-id="99d74-269">[3] [CRISP-DM 1.0: Step-by-Step Data Mining Guide](http://www.the-modeling-agency.com/crisp-dm.pdf)</span></span>   

<span data-ttu-id="99d74-270">[4] [Big Data Marketing: Engage Your Customers More Effectively and Drive Value](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn)</span><span class="sxs-lookup"><span data-stu-id="99d74-270">[4] [Big Data Marketing: Engage Your Customers More Effectively and Drive Value](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn)</span></span>

<span data-ttu-id="99d74-271">[5] [Cortana Intelligence 갤러리](http://gallery.cortanaintelligence.com/)의 [Telco 이탈 모델 템플릿](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5)</span><span class="sxs-lookup"><span data-stu-id="99d74-271">[5] [Telco churn model template](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5) in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)</span></span> 
 

## <a name="appendix"></a><span data-ttu-id="99d74-272">부록</span><span class="sxs-lookup"><span data-stu-id="99d74-272">Appendix</span></span>
![][10]

<span data-ttu-id="99d74-273">*그림 12: 이탈 프로토타입에 대한 프레젠테이션 스냅숏*</span><span class="sxs-lookup"><span data-stu-id="99d74-273">*Figure 12: Snapshot of a presentation on churn prototype*</span></span>

[1]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-1.png
[2]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-2.png
[3]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-3.png
[4]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-4.png
[5]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-5.png
[6]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-6.png
[7]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-7.png
[8]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-8.png
[9]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-9.png
[10]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-10.png
