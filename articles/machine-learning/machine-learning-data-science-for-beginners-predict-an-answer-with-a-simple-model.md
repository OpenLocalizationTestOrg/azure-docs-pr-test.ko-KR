---
title: "간단한 회귀 모델-Azure 기계 학습에 대 한 답변 aaaPredict | Microsoft Docs"
description: "어떻게 toocreate 간단한 회귀 비디오 4 초보자를 위한 데이터 과학에서 가격 toopredict를 모델링 합니다. 대상 데이터와 함께 선형 회귀가 포함됩니다."
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
ms.openlocfilehash: d4270c2237c33b7e898b78a08b292bc9d62e49ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="predict-an-answer-with-a-simple-model"></a><span data-ttu-id="b4f16-105">단순 모델을 사용하여 답변 예측</span><span class="sxs-lookup"><span data-stu-id="b4f16-105">Predict an answer with a simple model</span></span>
## <a name="video-4-data-science-for-beginners-series"></a><span data-ttu-id="b4f16-106">비디오 4: 초급자를 위한 데이터 과학 시리즈</span><span class="sxs-lookup"><span data-stu-id="b4f16-106">Video 4: Data Science for Beginners series</span></span>
<span data-ttu-id="b4f16-107">간단한 회귀 모델 toopredict toocreate 비디오 4 초보자를 위한 데이터 과학에 다이아몬드의 가격 hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-107">Learn how toocreate a simple regression model toopredict hello price of a diamond in Data Science for Beginners video 4.</span></span> <span data-ttu-id="b4f16-108">대상 데이터를 사용하여 회귀 모델을 그려볼 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-108">We'll draw a regression model with target data.</span></span>

<span data-ttu-id="b4f16-109">hello 시리즈를 최대한 활용 tooget hello 모두 보기</span><span class="sxs-lookup"><span data-stu-id="b4f16-109">tooget hello most out of hello series, watch them all.</span></span> <span data-ttu-id="b4f16-110">[비디오 이동 toohello 목록](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="b4f16-110">[Go toohello list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-predict-an-answer-with-a-simple-model/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="b4f16-111">이 시리즈의 다른 비디오</span><span class="sxs-lookup"><span data-stu-id="b4f16-111">Other videos in this series</span></span>
<span data-ttu-id="b4f16-112">*초보자를 위한 데이터 과학* 는 5 개의 짧은 비디오의 간략 한 소개 toodata 과학 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-112">*Data Science for Beginners* is a quick introduction toodata science in five short videos.</span></span>

* <span data-ttu-id="b4f16-113">비디오 1: [hello 5 데이터 과학 답변의 질문](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 분 14 초)*</span><span class="sxs-lookup"><span data-stu-id="b4f16-113">Video 1: [hello 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="b4f16-114">비디오 2: [데이터 과학에 사용할 수 있게 데이터가 준비되었나요?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="b4f16-114">Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="b4f16-115">*(4분 56초)*</span><span class="sxs-lookup"><span data-stu-id="b4f16-115">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="b4f16-116">비디오 3: [데이터로 대답할 수 있는 질문하기](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4분 17초)*</span><span class="sxs-lookup"><span data-stu-id="b4f16-116">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="b4f16-117">비디오 4: 단순 모델을 사용하여 답변 예측</span><span class="sxs-lookup"><span data-stu-id="b4f16-117">Video 4: Predict an answer with a simple model</span></span>
* <span data-ttu-id="b4f16-118">비디오 5: [타인의 작업 toodo 데이터 과학 복사](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 분 18 초)*</span><span class="sxs-lookup"><span data-stu-id="b4f16-118">Video 5: [Copy other people's work toodo data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-predict-an-answer-with-a-simple-model"></a><span data-ttu-id="b4f16-119">비디오 내용: 단순 모델을 사용하여 답변 예측</span><span class="sxs-lookup"><span data-stu-id="b4f16-119">Transcript: Predict an answer with a simple model</span></span>
<span data-ttu-id="b4f16-120">Toohello hello "데이터 과학에 대 한 초보자를 위한" 시리즈의에서 네 번째 동영상을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-120">Welcome toohello fourth video in hello "Data Science for Beginners" series.</span></span> <span data-ttu-id="b4f16-121">여기서는 간단한 모델을 빌드하고 예측을 진행할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-121">In this one, we'll build a simple model and make a prediction.</span></span>

<span data-ttu-id="b4f16-122">*모델* 은 데이터에 대한 간소화된 이야기입니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-122">A *model* is a simplified story about our data.</span></span> <span data-ttu-id="b4f16-123">무슨 의미인지 보여드리겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-123">I'll show you what I mean.</span></span>

## <a name="collect-relevant-accurate-connected-enough-data"></a><span data-ttu-id="b4f16-124">관련성 있고, 정확하고, 연결된 충분한 데이터 수집</span><span class="sxs-lookup"><span data-stu-id="b4f16-124">Collect relevant, accurate, connected, enough data</span></span>
<span data-ttu-id="b4f16-125">다이아몬드의 tooshop을 한다고 가정 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-125">Say I want tooshop for a diamond.</span></span> <span data-ttu-id="b4f16-126">에 속한 1.35 캐럿 다이아몬드에 대 한 설정 사용 하 여 toomy 할머니 링 있고 tooget 가격은 어느 정도 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-126">I have a ring that belonged toomy grandmother with a setting for a 1.35 carat diamond, and I want tooget an idea of how much it will cost.</span></span> <span data-ttu-id="b4f16-127">Hello 보석 저장소로 메모장 및 펜 걸릴 및 내가 모든 hello 대/소문자 및 carats 어느 정도 입니까은 hello 다이아몬드의 hello 가격 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-127">I take a notepad and pen into hello jewelry store, and I write down hello price of all of hello diamonds in hello case and how much they weigh in carats.</span></span> <span data-ttu-id="b4f16-128">Hello 첫 번째 다이아몬드-1.01 carats 및 $7,366로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-128">Starting with hello first diamond - it's 1.01 carats and $7,366.</span></span>

<span data-ttu-id="b4f16-129">이제 하 고이 작업을 수행 모든 hello에 대 한 hello 저장소에서 다른 다이아몬드입니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-129">Now I go through and do this for all hello other diamonds in hello store.</span></span>

![다이아몬드 데이터 열](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/diamond-data.png)

<span data-ttu-id="b4f16-131">목록에는 두 개의 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-131">Notice that our list has two columns.</span></span> <span data-ttu-id="b4f16-132">각 열은 캐럿 무게와 가격의 두 가지 다른 특성을 포함하며 각 행은 1개의 다이아몬드를 나타내는 단일 데이터 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-132">Each column has a different attribute - weight in carats and price - and each row is a single data point that represents a single diamond.</span></span>

<span data-ttu-id="b4f16-133">실제로 여기에 작은 데이터 집합인 표를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-133">We've actually created a small data set here - a table.</span></span> <span data-ttu-id="b4f16-134">이 표가 우리의 품질 기준을 충족한다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-134">Notice that it meets our criteria for quality:</span></span>

* <span data-ttu-id="b4f16-135">hello 데이터는 **관련** -가중치는 확실 하 게 관련된 tooprice</span><span class="sxs-lookup"><span data-stu-id="b4f16-135">hello data is **relevant** - weight is definitely related tooprice</span></span>
* <span data-ttu-id="b4f16-136">있기 **정확한** -म म 적어 hello 가격을 다시 확인</span><span class="sxs-lookup"><span data-stu-id="b4f16-136">It's **accurate** - we double-checked hello prices that we write down</span></span>
* <span data-ttu-id="b4f16-137">**연결되어 있음** - 이러한 열에는 공백이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-137">It's **connected** - there are no blank spaces in either of these columns</span></span>
* <span data-ttu-id="b4f16-138">볼 수 있겠지만, 및가 **충분 한** 데이터 tooanswer 우리의 질문</span><span class="sxs-lookup"><span data-stu-id="b4f16-138">And, as we'll see, it's **enough** data tooanswer our question</span></span>

## <a name="ask-a-sharp-question"></a><span data-ttu-id="b4f16-139">정확하게 질문하기</span><span class="sxs-lookup"><span data-stu-id="b4f16-139">Ask a sharp question</span></span>
<span data-ttu-id="b4f16-140">이제 날카로운 방식으로 우리의 질문을 야기 합니다 했습니다: "는 비용 비용 toobuy 1.35 캐럿 다이아몬드?"</span><span class="sxs-lookup"><span data-stu-id="b4f16-140">Now we'll pose our question in a sharp way: "How much will it cost toobuy a 1.35 carat diamond?"</span></span>

<span data-ttu-id="b4f16-141">이 목록은 없는 1.35 캐럿 다이아몬드, toouse hello 나머지 우리의 데이터 tooget 응답 toohello 질문 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-141">Our list doesn't have a 1.35 carat diamond in it, so we'll have toouse hello rest of our data tooget an answer toohello question.</span></span>

## <a name="plot-hello-existing-data"></a><span data-ttu-id="b4f16-142">Hello 기존 데이터 표시</span><span class="sxs-lookup"><span data-stu-id="b4f16-142">Plot hello existing data</span></span>
<span data-ttu-id="b4f16-143">hello 먼저 하겠습니다 점은 긋습니다 번호, 축, toochart hello 가중치를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-143">hello first thing we'll do is draw a horizontal number line, called an axis, toochart hello weights.</span></span> <span data-ttu-id="b4f16-144">hello 범위의 hello 가중치 0 too2 이므로 범위 및 각 절반 캐럿에 대 한 틱 put을 검사 하는 줄을 내릴 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-144">hello range of hello weights is 0 too2, so we'll draw a line that covers that range and put ticks for each half carat.</span></span>

<span data-ttu-id="b4f16-145">그런 다음 세로 축 toorecord hello 가격을 그릴 알아보고 toohello 가중치 가로 축 연결 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-145">Next we'll draw a vertical axis toorecord hello price and connect it toohello horizontal weight axis.</span></span> <span data-ttu-id="b4f16-146">단위는 달러가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-146">This will be in units of dollars.</span></span> <span data-ttu-id="b4f16-147">이제 좌표축이 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-147">Now we have a set of coordinate axes.</span></span>

![무게 및 가격 축](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/weight-and-price-axes.png)

<span data-ttu-id="b4f16-149">현재 진행 중인 tootake이이 데이터 이제로 설정 된 *산 점도*합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-149">We're going tootake this data now and turn it into a *scatter plot*.</span></span> <span data-ttu-id="b4f16-150">이것이 좋은 방법 toovisualize 숫자 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-150">This is a great way toovisualize numerical data sets.</span></span>

<span data-ttu-id="b4f16-151">첫 번째 데이터 요소 hello에 대 한 1.01 carats에서 세로 선을 파악 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-151">For hello first data point, we eyeball a vertical line at 1.01 carats.</span></span> <span data-ttu-id="b4f16-152">그런 다음 $7,366에 해당하는 수평선을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-152">Then, we eyeball a horizontal line at $7,366.</span></span> <span data-ttu-id="b4f16-153">만나는 위치에 점을 그립니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-153">Where they meet, we draw a dot.</span></span> <span data-ttu-id="b4f16-154">이것은 첫 번째 다이아몬드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-154">This represents our first diamond.</span></span>

<span data-ttu-id="b4f16-155">이제이 목록에 각 다이아몬드를 통해 이동 하 고 동일한 작업을 hello 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-155">Now we go through each diamond on this list and do hello same thing.</span></span> <span data-ttu-id="b4f16-156">다 끝나면 각 다이아몬드에 하나씩 여러 개의 점이 그려집니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-156">When we're through, this is what we get: a bunch of dots, one for each diamond.</span></span>

![산점도](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/scatter-plot.png)

## <a name="draw-hello-model-through-hello-data-points"></a><span data-ttu-id="b4f16-158">Hello 데이터 요소를 통해 그리기 hello 모델</span><span class="sxs-lookup"><span data-stu-id="b4f16-158">Draw hello model through hello data points</span></span>
<span data-ttu-id="b4f16-159">이제 hello 점과 squint 보면 hello 컬렉션 fat, 유사 항목 줄 같이 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-159">Now if you look at hello dots and squint, hello collection looks like a fat, fuzzy line.</span></span> <span data-ttu-id="b4f16-160">마커를 사용해서 그 사이로 직선을 그릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-160">We can take our marker and draw a straight line through it.</span></span>

<span data-ttu-id="b4f16-161">선을 그려서 *모델*을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-161">By drawing a line, we created a *model*.</span></span> <span data-ttu-id="b4f16-162">Hello 현실 세계 차지 하 고 그 단순한 만화 버전으로 생각 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-162">Think of this as taking hello real world and making a simplistic cartoon version of it.</span></span> <span data-ttu-id="b4f16-163">이제 hello 만화 잘못 되었습니다.-hello 줄 모든 hello 데이터 요소를 통해 이동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-163">Now hello cartoon is wrong - hello line doesn't go through all hello data points.</span></span> <span data-ttu-id="b4f16-164">하지만 유용한 단순화 기법입니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-164">But, it's a useful simplification.</span></span>

![선형 회귀 선](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/linear-regression-line.png)

<span data-ttu-id="b4f16-166">hello 점으로 거치지 않습니다 정확 하 게 hello 줄 hello 팩트는 정상입니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-166">hello fact that all hello dots don't go exactly through hello line is OK.</span></span> <span data-ttu-id="b4f16-167">데이터 과학자 hello-된 모델을 hello 선-임을 한다는 것으로이 설명 하 고 각 점의 대 한 일부 *노이즈* 또는 *분산* 연관 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-167">Data scientists explain this by saying that there's hello model - that's hello line - and then each dot has some *noise* or *variance* associated with it.</span></span> <span data-ttu-id="b4f16-168">완벽 한 관계를 원본으로 사용 하는 hello 않으며 노이즈와 불확실 한 정보를 추가 하는 hello 해보겠습니다, 실제 세계 않으면입니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-168">There's hello underlying perfect relationship, and then there's hello gritty, real world that adds noise and uncertainty.</span></span>

<span data-ttu-id="b4f16-169">Tooanswer hello 질문 त ु म 때문에 *얼마나 됩니까?* 라고는 *회귀*합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-169">Because we're trying tooanswer hello question *How much?* this is called a *regression*.</span></span> <span data-ttu-id="b4f16-170">또한 직선을 사용하므로 *선형 회귀*에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-170">And because we're using a straight line, it's a *linear regression*.</span></span>

## <a name="use-hello-model-toofind-hello-answer"></a><span data-ttu-id="b4f16-171">Hello 모델 toofind hello 답변을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b4f16-171">Use hello model toofind hello answer</span></span>
<span data-ttu-id="b4f16-172">이제 우리에게는 모델이 있고 “1.35 캐럿의 다이아몬드 가격은 얼마나 될까요?”라는 질문을 해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-172">Now we have a model and we ask it our question: How much will a 1.35 carat diamond cost?</span></span>

<span data-ttu-id="b4f16-173">tooanswer 우리의 질문 1.35 carats 파악 하 고 세로 선을 그립니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-173">tooanswer our question, we eyeball 1.35 carats and draw a vertical line.</span></span> <span data-ttu-id="b4f16-174">Hello 모델 선과 교차, 여기서 가로줄 toohello 달러 축을 파악 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-174">Where it crosses hello model line, we eyeball a horizontal line toohello dollar axis.</span></span> <span data-ttu-id="b4f16-175">정확히 10,000에 닿네요.</span><span class="sxs-lookup"><span data-stu-id="b4f16-175">It hits right at 10,000.</span></span> <span data-ttu-id="b4f16-176">와우 그렇다면 이게 정답입니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-176">Boom!</span></span> <span data-ttu-id="b4f16-177">Hello 대답은: 1.35 캐럿 다이아몬드 약 10, 000 달러 비용이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-177">That's hello answer: A 1.35 carat diamond costs about $10,000.</span></span>

![Hello 모델에 hello 답변 찾기](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/find-the-answer.png)

## <a name="create-a-confidence-interval"></a><span data-ttu-id="b4f16-179">신뢰 구간 만들기</span><span class="sxs-lookup"><span data-stu-id="b4f16-179">Create a confidence interval</span></span>
<span data-ttu-id="b4f16-180">것이 자연 toowonder 어떻게이 예측은 정확 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-180">It's natural toowonder how precise this prediction is.</span></span> <span data-ttu-id="b4f16-181">Hello 1.35 캐럿 다이아몬드 너무 매우 가까운 됩니다 유용 tooknow가 $ 10, 000, 또는 위 또는 아래로 많은 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-181">It's useful tooknow whether hello 1.35 carat diamond will be very close too$10,000, or a lot higher or lower.</span></span> <span data-ttu-id="b4f16-182">toofigure이 out, 봉투 (envelope)의 hello 점 대부분을 포함 하는 hello 회귀선 주위를 그릴 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-182">toofigure this out, let's draw an envelope around hello regression line that includes most of hello dots.</span></span> <span data-ttu-id="b4f16-183">이 봉투 (envelope이) 라고 우리의 *신뢰 구간*: We're 때문에이 봉투 속하는 가격 확신 상당히 지난 hello에서 그 중 대부분 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-183">This envelope is called our *confidence interval*: We're pretty confident that prices fall within this envelope, because in hello past most of them have.</span></span> <span data-ttu-id="b4f16-184">해당 봉투의 hello 위아래 hello hello 1.35 캐럿 줄이 교차 하는 곳에서 두 개 가로 줄 내릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-184">We can draw two more horizontal lines from where hello 1.35 carat line crosses hello top and hello bottom of that envelope.</span></span>

![예측](./media/machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model/confidence-interval.png)

<span data-ttu-id="b4f16-186">이제 우리 수 예를 신뢰 구간 우리의: 수 말할 자신 있게 1.35 캐럿 다이아몬드의 hello 가격 약 $10000-하지만 $8000 낮은 것 이며 함을 $ 12, 000으로 높을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-186">Now we can say something about our confidence interval:  We can say confidently that hello price of a 1.35 carat diamond is about $10,000 - but it might be as low as $8,000 and it might be as high as $12,000.</span></span>

## <a name="were-done-with-no-math-or-computers"></a><span data-ttu-id="b4f16-187">수학이나 컴퓨터 없이도 해냈습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-187">We're done, with no math or computers</span></span>
<span data-ttu-id="b4f16-188">어떤 데이터 과학자 toodo, 지급에 수행한 및 그리기 만으로 했던:</span><span class="sxs-lookup"><span data-stu-id="b4f16-188">We did what data scientists get paid toodo, and we did it just by drawing:</span></span>

* <span data-ttu-id="b4f16-189">데이터로 답변할 수 있는 질문을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-189">We asked a question that we could answer with data</span></span>
* <span data-ttu-id="b4f16-190">*선형 회귀*를 사용하여 *모델*을 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-190">We built a *model* using *linear regression*</span></span>
* <span data-ttu-id="b4f16-191">*신뢰 구간*을 토대로 *예측*을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-191">We made a *prediction*, complete with a *confidence interval*</span></span>

<span data-ttu-id="b4f16-192">Toodo 수학 또는 컴퓨터를 사용 하지 않았습니다 고 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-192">And we didn't use math or computers toodo it.</span></span>

<span data-ttu-id="b4f16-193">우리에게 더 많은 정보가 있었다면, 예를 들어</span><span class="sxs-lookup"><span data-stu-id="b4f16-193">Now if we'd had more information, like...</span></span>

* <span data-ttu-id="b4f16-194">hello는 hello 다이아몬드의 잘라내기</span><span class="sxs-lookup"><span data-stu-id="b4f16-194">hello cut of hello diamond</span></span>
* <span data-ttu-id="b4f16-195">색상 변경 (얼마나 비슷한지를 hello 다이아몬드는 toobeing 흰색)</span><span class="sxs-lookup"><span data-stu-id="b4f16-195">color variations (how close hello diamond is toobeing white)</span></span>
* <span data-ttu-id="b4f16-196">hello 수가 hello 다이아몬드에 포함</span><span class="sxs-lookup"><span data-stu-id="b4f16-196">hello number of inclusions in hello diamond</span></span>

<span data-ttu-id="b4f16-197">그러면 더 많은 열이 형성될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-197">...then we would have had more columns.</span></span> <span data-ttu-id="b4f16-198">이 경우에는 수학이 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-198">In that case, math becomes helpful.</span></span> <span data-ttu-id="b4f16-199">을 두 개 이상의 열이 있는 경우 용지에 하드 toodraw 점입니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-199">If you have more than two columns, it's hard toodraw dots on paper.</span></span> <span data-ttu-id="b4f16-200">hello 수학을 사용 하면 해당 줄 또는 해당 평면 tooyour 데이터를 매우 잘 맞습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-200">hello math lets you fit that line or that plane tooyour data very nicely.</span></span>

<span data-ttu-id="b4f16-201">또한 다이아몬드 몇 개가 아니라 2,000개 또는 2백만 개가 있다면 컴퓨터로 훨씬 더 빠르게 이러한 작업을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-201">Also, if instead of just a handful of diamonds, we had two thousand or two million, then you can do that work much faster with a computer.</span></span>

<span data-ttu-id="b4f16-202">오늘 toodo 선형 회귀 되 고, 설정 하는 방법 데이터를 사용 하 여 예측에 대 한 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-202">Today, we've talked about how toodo linear regression, and we made a prediction using data.</span></span>

<span data-ttu-id="b4f16-203">Hello 아웃 있는지 toocheck "데이터 과학에 대 한 초보자를 위한"에서 Microsoft Azure 기계 학습에서 비디오를 다른 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4f16-203">Be sure toocheck out hello other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4f16-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4f16-204">Next steps</span></span>
* [<span data-ttu-id="b4f16-205">Machine Learning Studio로 첫 번째 데이터 과학 실험 시도</span><span class="sxs-lookup"><span data-stu-id="b4f16-205">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="b4f16-206">가져오기 소개 tooMachine Microsoft Azure에서 학습</span><span class="sxs-lookup"><span data-stu-id="b4f16-206">Get an introduction tooMachine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
