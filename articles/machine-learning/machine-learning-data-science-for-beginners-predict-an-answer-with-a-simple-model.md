---
title: "단순 회귀 모델을 사용하여 답변 예측 - Azure Machine Learning | Microsoft Docs"
description: "초급자를 위한 데이터 과학 비디오 4에는 가격을 예측하는 단순 회귀 모델을 만드는 방법이 나옵니다. 대상 데이터와 함께 선형 회귀가 포함됩니다."
keywords: "모델 만들기,단순 모델,가격 예측,단순 회귀 모델"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: a28f1fab-e2d8-4663-aa7d-ca3530c8b525
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 24df1823af2610a5111118f47e4cadbcfcc0eff1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a><span data-ttu-id="68c70-105">단순 모델을 사용하여 답변 예측</span><span class="sxs-lookup"><span data-stu-id="68c70-105">Predict an answer with a simple model</span></span>
## <a name="video-4-data-science-for-beginners-series"></a><span data-ttu-id="68c70-106">비디오 4: 초급자를 위한 데이터 과학 시리즈</span><span class="sxs-lookup"><span data-stu-id="68c70-106">Video 4: Data Science for Beginners series</span></span>
<span data-ttu-id="68c70-107">초급자를 위한 데이터 과학 비디오 4에서는 다이아몬드의 가격을 예측하는 단순 회귀 모델을 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-107">Learn how to create a simple regression model to predict the price of a diamond in Data Science for Beginners video 4.</span></span> <span data-ttu-id="68c70-108">대상 데이터를 사용하여 회귀 모델을 그려볼 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-108">We'll draw a regression model with target data.</span></span>

<span data-ttu-id="68c70-109">시리즈를 최대한 활용하려면 모두 시청하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-109">To get the most out of the series, watch them all.</span></span> <span data-ttu-id="68c70-110">[비디오 목록으로 이동](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="68c70-110">[Go to the list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="68c70-111">이 시리즈의 다른 비디오</span><span class="sxs-lookup"><span data-stu-id="68c70-111">Other videos in this series</span></span>
<span data-ttu-id="68c70-112">*초급자를 위한 데이터 과학* 은 다섯 개의 짧은 비디오를 통해 데이터 과학을 간략히 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="68c70-113">비디오 1: [데이터 과학으로 답변할 수 있는 5가지 질문](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5분 14초)*</span><span class="sxs-lookup"><span data-stu-id="68c70-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="68c70-114">비디오 2: [데이터 과학에 사용할 수 있게 데이터가 준비되었나요?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="68c70-114">Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="68c70-115">*(4분 56초)*</span><span class="sxs-lookup"><span data-stu-id="68c70-115">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="68c70-116">비디오 3: [데이터로 대답할 수 있는 질문하기](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4분 17초)*</span><span class="sxs-lookup"><span data-stu-id="68c70-116">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="68c70-117">비디오 4: 단순 모델을 사용하여 답변 예측</span><span class="sxs-lookup"><span data-stu-id="68c70-117">Video 4: Predict an answer with a simple model</span></span>
* <span data-ttu-id="68c70-118">비디오 5: [데이터 과학을 수행하기 위해 다른 사람의 작품 복사](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3분 18초)*</span><span class="sxs-lookup"><span data-stu-id="68c70-118">Video 5: [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-predict-an-answer-with-a-simple-model"></a><span data-ttu-id="68c70-119">비디오 내용: 단순 모델을 사용하여 답변 예측</span><span class="sxs-lookup"><span data-stu-id="68c70-119">Transcript: Predict an answer with a simple model</span></span>
<span data-ttu-id="68c70-120">“초급자를 위한 데이터 과학” 시리즈 중 4번째 비디오를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-120">Welcome to the fourth video in the "Data Science for Beginners" series.</span></span> <span data-ttu-id="68c70-121">여기서는 간단한 모델을 빌드하고 예측을 진행할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-121">In this one, we'll build a simple model and make a prediction.</span></span>

<span data-ttu-id="68c70-122">*모델* 은 데이터에 대한 간소화된 이야기입니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-122">A *model* is a simplified story about our data.</span></span> <span data-ttu-id="68c70-123">무슨 의미인지 보여드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-123">I'll show you what I mean.</span></span>

## <a name="collect-relevant-accurate-connected-enough-data"></a><span data-ttu-id="68c70-124">관련성 있고, 정확하고, 연결된 충분한 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="68c70-124">Collect relevant, accurate, connected, enough data</span></span>
<span data-ttu-id="68c70-125">다이아몬드를 구입하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-125">Say I want to shop for a diamond.</span></span> <span data-ttu-id="68c70-126">할머니께 물려받은 1.35 캐럿 다이아몬드 반지의 가격이 얼마나 되는지 알고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-126">I have a ring that belonged to my grandmother with a setting for a 1.35 carat diamond, and I want to get an idea of how much it will cost.</span></span> <span data-ttu-id="68c70-127">노트와 펜을 들고 보석점에 가서 케이스에 들어 있는 모든 다이아몬드의 가격과 캐럿 무게를 적습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-127">I take a notepad and pen into the jewelry store, and I write down the price of all of the diamonds in the case and how much they weigh in carats.</span></span> <span data-ttu-id="68c70-128">첫 번째 다이아몬드는 1.01 캐럿에 $7,366입니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-128">Starting with the first diamond - it's 1.01 carats and $7,366.</span></span>

<span data-ttu-id="68c70-129">매장의 다른 모든 다이아몬드에 대해서도 같은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-129">Now I go through and do this for all the other diamonds in the store.</span></span>

![다이아몬드 데이터 열](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

<span data-ttu-id="68c70-131">목록에는 두 개의 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-131">Notice that our list has two columns.</span></span> <span data-ttu-id="68c70-132">각 열은 캐럿 무게와 가격의 두 가지 다른 특성을 포함하며 각 행은 1개의 다이아몬드를 나타내는 단일 데이터 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-132">Each column has a different attribute - weight in carats and price - and each row is a single data point that represents a single diamond.</span></span>

<span data-ttu-id="68c70-133">실제로 여기에 작은 데이터 집합인 표를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-133">We've actually created a small data set here - a table.</span></span> <span data-ttu-id="68c70-134">이 표가 우리의 품질 기준을 충족한다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-134">Notice that it meets our criteria for quality:</span></span>

* <span data-ttu-id="68c70-135">데이터가 **관련 있음** - 무게가 가격이 확실히 연관되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-135">The data is **relevant** - weight is definitely related to price</span></span>
* <span data-ttu-id="68c70-136">**정확함** - 적어놓은 가격을 한 번 더 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-136">It's **accurate** - we double-checked the prices that we write down</span></span>
* <span data-ttu-id="68c70-137">**연결되어 있음** - 이러한 열에는 공백이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-137">It's **connected** - there are no blank spaces in either of these columns</span></span>
* <span data-ttu-id="68c70-138">또한 여기서 확인된 것처럼 질문에 답변할 수 있는 **충분한** 데이터가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-138">And, as we'll see, it's **enough** data to answer our question</span></span>

## <a name="ask-a-sharp-question"></a><span data-ttu-id="68c70-139">정확하게 질문하기</span><span class="sxs-lookup"><span data-stu-id="68c70-139">Ask a sharp question</span></span>
<span data-ttu-id="68c70-140">이제 “1.35 캐럿의 다이아몬드를 구입하는 비용은 얼마나 될까요?”와 같이 더 상세하게 질문해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-140">Now we'll pose our question in a sharp way: "How much will it cost to buy a 1.35 carat diamond?"</span></span>

<span data-ttu-id="68c70-141">목록에는 1.35 캐럿 다이아몬드가 없으므로 나머지 데이터를 사용해서 질문에 대한 답변을 얻어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-141">Our list doesn't have a 1.35 carat diamond in it, so we'll have to use the rest of our data to get an answer to the question.</span></span>

## <a name="plot-the-existing-data"></a><span data-ttu-id="68c70-142">기존 데이터 도식화</span><span class="sxs-lookup"><span data-stu-id="68c70-142">Plot the existing data</span></span>
<span data-ttu-id="68c70-143">가장 먼저 수행할 작업은 축에 해당하는 수평선을 그려 무게를 차트로 나타내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-143">The first thing we'll do is draw a horizontal number line, called an axis, to chart the weights.</span></span> <span data-ttu-id="68c70-144">무게 범위는 0~2이므로 해당 범위를 포함하는 선을 그리고 1/2 캐럿 단위로 눈금을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-144">The range of the weights is 0 to 2, so we'll draw a line that covers that range and put ticks for each half carat.</span></span>

<span data-ttu-id="68c70-145">그런 다음 수직선을 그려 가격을 기록한 후 가로의 무게 축에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-145">Next we'll draw a vertical axis to record the price and connect it to the horizontal weight axis.</span></span> <span data-ttu-id="68c70-146">단위는 달러가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-146">This will be in units of dollars.</span></span> <span data-ttu-id="68c70-147">이제 좌표축이 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-147">Now we have a set of coordinate axes.</span></span>

![무게 및 가격 축](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

<span data-ttu-id="68c70-149">이제 이 데이터를 가져와서 *산점도*로 나타낼 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-149">We're going to take this data now and turn it into a *scatter plot*.</span></span> <span data-ttu-id="68c70-150">이 방법은 수치 데이터 집합을 시각화하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-150">This is a great way to visualize numerical data sets.</span></span>

<span data-ttu-id="68c70-151">첫 번째 데이터 요소의 경우 1.01 캐럿에 해당하는 수직선을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-151">For the first data point, we eyeball a vertical line at 1.01 carats.</span></span> <span data-ttu-id="68c70-152">그런 다음 $7,366에 해당하는 수평선을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-152">Then, we eyeball a horizontal line at $7,366.</span></span> <span data-ttu-id="68c70-153">만나는 위치에 점을 그립니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-153">Where they meet, we draw a dot.</span></span> <span data-ttu-id="68c70-154">이것은 첫 번째 다이아몬드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-154">This represents our first diamond.</span></span>

<span data-ttu-id="68c70-155">이제 이 목록의 모든 다이아몬드에 대해 동일한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-155">Now we go through each diamond on this list and do the same thing.</span></span> <span data-ttu-id="68c70-156">다 끝나면 각 다이아몬드에 하나씩 여러 개의 점이 그려집니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-156">When we're through, this is what we get: a bunch of dots, one for each diamond.</span></span>

![산점도](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-the-model-through-the-data-points"></a><span data-ttu-id="68c70-158">데이터 요소를 통해 모델 그리기</span><span class="sxs-lookup"><span data-stu-id="68c70-158">Draw the model through the data points</span></span>
<span data-ttu-id="68c70-159">이제 눈을 가늘게 뜨고 점들을 응시하면 두리뭉실한 선처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-159">Now if you look at the dots and squint, the collection looks like a fat, fuzzy line.</span></span> <span data-ttu-id="68c70-160">마커를 사용해서 그 사이로 직선을 그릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-160">We can take our marker and draw a straight line through it.</span></span>

<span data-ttu-id="68c70-161">선을 그려서 *모델*을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-161">By drawing a line, we created a *model*.</span></span> <span data-ttu-id="68c70-162">이러한 과정은 실제 세계에서 아주 간단한 만화 버전을 만드는 것으로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-162">Think of this as taking the real world and making a simplistic cartoon version of it.</span></span> <span data-ttu-id="68c70-163">그 만화는 잘못된 것입니다. 선이 모든 데이터 요소를 지나가지는 않으니까요.</span><span class="sxs-lookup"><span data-stu-id="68c70-163">Now the cartoon is wrong - the line doesn't go through all the data points.</span></span> <span data-ttu-id="68c70-164">하지만 유용한 단순화 기법입니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-164">But, it's a useful simplification.</span></span>

![선형 회귀 선](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

<span data-ttu-id="68c70-166">모든 점이 정확히 선을 지나가지 않아도 괜찮습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-166">The fact that all the dots don't go exactly through the line is OK.</span></span> <span data-ttu-id="68c70-167">데이터 과학자들은 이제 선에 해당하는 모델이 형성되었고 각 점에는 이와 연관된 *노이즈* 또는 *분산*이 있다고 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-167">Data scientists explain this by saying that there's the model - that's the line - and then each dot has some *noise* or *variance* associated with it.</span></span> <span data-ttu-id="68c70-168">기본적인 완벽한 관계가 있으며, 또한 노이즈와 불확실성이 적용되는 단호한 실제 세계가 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-168">There's the underlying perfect relationship, and then there's the gritty, real world that adds noise and uncertainty.</span></span>

<span data-ttu-id="68c70-169">여기서는 *가격은 얼마일까요?*라는 질문에 답변하려고 하기 때문에 이를 *회귀*라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-169">Because we're trying to answer the question *How much?* this is called a *regression*.</span></span> <span data-ttu-id="68c70-170">또한 직선을 사용하므로 *선형 회귀*에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-170">And because we're using a straight line, it's a *linear regression*.</span></span>

## <a name="use-the-model-to-find-the-answer"></a><span data-ttu-id="68c70-171">모델을 사용하여 해답 찾기</span><span class="sxs-lookup"><span data-stu-id="68c70-171">Use the model to find the answer</span></span>
<span data-ttu-id="68c70-172">이제 우리에게는 모델이 있고 “1.35 캐럿의 다이아몬드 가격은 얼마나 될까요?”라는 질문을 해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-172">Now we have a model and we ask it our question: How much will a 1.35 carat diamond cost?</span></span>

<span data-ttu-id="68c70-173">질문에 대한 답변을 얻기 위해 1.35 캐럿에서 수직선을 그립니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-173">To answer our question, we eyeball 1.35 carats and draw a vertical line.</span></span> <span data-ttu-id="68c70-174">모델 선을 지나는 위치에서 달러 축과 만나는 수평선을 그려 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-174">Where it crosses the model line, we eyeball a horizontal line to the dollar axis.</span></span> <span data-ttu-id="68c70-175">정확히 10,000에 닿네요.</span><span class="sxs-lookup"><span data-stu-id="68c70-175">It hits right at 10,000.</span></span> <span data-ttu-id="68c70-176">와우 그렇다면 이게 정답입니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-176">Boom!</span></span> <span data-ttu-id="68c70-177">1.35 캐럿 다이아몬드의 가격은 약 10,000달러입니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-177">That's the answer: A 1.35 carat diamond costs about $10,000.</span></span>

![모델에서 해답 찾기](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a><span data-ttu-id="68c70-179">신뢰 구간 만들기</span><span class="sxs-lookup"><span data-stu-id="68c70-179">Create a confidence interval</span></span>
<span data-ttu-id="68c70-180">이 예측이 얼마나 정확한지 궁금해하는 것은 당연하겠죠.</span><span class="sxs-lookup"><span data-stu-id="68c70-180">It's natural to wonder how precise this prediction is.</span></span> <span data-ttu-id="68c70-181">1.35 캐럿 다이아몬드 가격이 10,000에 아주 가까운지, 약간 더 높은지 또는 더 낮은지를 알면 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-181">It's useful to know whether the 1.35 carat diamond will be very close to $10,000, or a lot higher or lower.</span></span> <span data-ttu-id="68c70-182">이를 알아내기 위해 회귀 직선 주위에 대부분의 점들을 포함하는 범위를 그려보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-182">To figure this out, let's draw an envelope around the regression line that includes most of the dots.</span></span> <span data-ttu-id="68c70-183">이 범위를 *신뢰 구간*이라고 합니다. 앞서 확인한 것처럼 대부분의 가격이 이 범위에 속한다고 확신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-183">This envelope is called our *confidence interval*: We're pretty confident that prices fall within this envelope, because in the past most of them have.</span></span> <span data-ttu-id="68c70-184">1.35 캐럿 선이 해당 범위의 맨 위와 맨 아래에서 교차하는 수평선을 2개 더 그릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-184">We can draw two more horizontal lines from where the 1.35 carat line crosses the top and the bottom of that envelope.</span></span>

![예측](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

<span data-ttu-id="68c70-186">이제 이 신뢰 구간에 대해 이렇게 말할 수 있습니다. 1.35 캐럿 다이아몬드의 가격은 약 10,000달러이지만 최하 8,000달러에서 최고 12,000달러가 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-186">Now we can say something about our confidence interval:  We can say confidently that the price of a 1.35 carat diamond is about $10,000 - but it might be as low as $8,000 and it might be as high as $12,000.</span></span>

## <a name="were-done-with-no-math-or-computers"></a><span data-ttu-id="68c70-187">수학이나 컴퓨터 없이도 해냈습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-187">We're done, with no math or computers</span></span>
<span data-ttu-id="68c70-188">데이터 과학자들이 돈을 받고 하는 일을 우리가 해넀습니다. 그림만 그려서 말이죠.</span><span class="sxs-lookup"><span data-stu-id="68c70-188">We did what data scientists get paid to do, and we did it just by drawing:</span></span>

* <span data-ttu-id="68c70-189">데이터로 답변할 수 있는 질문을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-189">We asked a question that we could answer with data</span></span>
* <span data-ttu-id="68c70-190">*선형 회귀*를 사용하여 *모델*을 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-190">We built a *model* using *linear regression*</span></span>
* <span data-ttu-id="68c70-191">*신뢰 구간*을 토대로 *예측*을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-191">We made a *prediction*, complete with a *confidence interval*</span></span>

<span data-ttu-id="68c70-192">또한 수학이나 컴퓨터를 사용하지 않고 이 모든 것을 해냈습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-192">And we didn't use math or computers to do it.</span></span>

<span data-ttu-id="68c70-193">우리에게 더 많은 정보가 있었다면, 예를 들어</span><span class="sxs-lookup"><span data-stu-id="68c70-193">Now if we'd had more information, like...</span></span>

* <span data-ttu-id="68c70-194">다이아몬드 커트</span><span class="sxs-lookup"><span data-stu-id="68c70-194">the cut of the diamond</span></span>
* <span data-ttu-id="68c70-195">색상 변형(다이아몬드가 흰색에 가까운 정도)</span><span class="sxs-lookup"><span data-stu-id="68c70-195">color variations (how close the diamond is to being white)</span></span>
* <span data-ttu-id="68c70-196">다이아몬드의 함유물 수 같은 것 말입니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-196">the number of inclusions in the diamond</span></span>

<span data-ttu-id="68c70-197">그러면 더 많은 열이 형성될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-197">...then we would have had more columns.</span></span> <span data-ttu-id="68c70-198">이 경우에는 수학이 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-198">In that case, math becomes helpful.</span></span> <span data-ttu-id="68c70-199">열이 두 개보다 많은 경우 종이에 점을 그리기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-199">If you have more than two columns, it's hard to draw dots on paper.</span></span> <span data-ttu-id="68c70-200">수학을 사용하면 데이터에 좀 더 잘 맞는 선이나 평면을 그릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-200">The math lets you fit that line or that plane to your data very nicely.</span></span>

<span data-ttu-id="68c70-201">또한 다이아몬드 몇 개가 아니라 2,000개 또는 2백만 개가 있다면 컴퓨터로 훨씬 더 빠르게 이러한 작업을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-201">Also, if instead of just a handful of diamonds, we had two thousand or two million, then you can do that work much faster with a computer.</span></span>

<span data-ttu-id="68c70-202">오늘은 선형 회귀를 수행하는 방법을 논의했으며 데이터를 사용해서 예측을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="68c70-202">Today, we've talked about how to do linear regression, and we made a prediction using data.</span></span>

<span data-ttu-id="68c70-203">Microsoft Azure 기계 학습의 “초급자를 위한 데이터 과학”에 있는 다른 비디오도 확인해보세요.</span><span class="sxs-lookup"><span data-stu-id="68c70-203">Be sure to check out the other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68c70-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="68c70-204">Next steps</span></span>
* [<span data-ttu-id="68c70-205">Machine Learning Studio로 첫 번째 데이터 과학 실험 시도</span><span class="sxs-lookup"><span data-stu-id="68c70-205">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="68c70-206">Microsoft Azure의 기계 학습 소개 보기</span><span class="sxs-lookup"><span data-stu-id="68c70-206">Get an introduction to Machine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
