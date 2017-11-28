---
title: "기계 학습의 R 언어에 대 한 aaaQuickstart 자습서 | Microsoft Docs"
description: "이 R 신속 하 게 hello R 언어를 사용 하 여 Azure 기계 학습 스튜디오 toocreate 예측 솔루션으로 시작 하는 자습서 tooget 프로그래밍을 사용 합니다."
keywords: "빠른 시작, r 언어, r 프로그래밍 언어, r 프로그래밍 자습서"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="eaa57-104">Azure 기계 학습에 대 한 hello R 프로그래밍 언어에 대 한 빠른 시작 자습서</span><span class="sxs-lookup"><span data-stu-id="eaa57-104">Quickstart tutorial for hello R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="eaa57-105">소개</span><span class="sxs-lookup"><span data-stu-id="eaa57-105">Introduction</span></span>
<span data-ttu-id="eaa57-106">이 빠른 시작 자습서를 사용 하면 신속 하 게 hello R 프로그래밍 언어를 사용 하 여 Azure 기계 학습 확장을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using hello R programming language.</span></span> <span data-ttu-id="eaa57-107">이 R 자습서 toocreate 프로그래밍, 테스트 하 고 Azure 기계 학습에서 R 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-107">Follow this R programming tutorial toocreate, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="eaa57-108">자습서를 통해 작업 하는 동안 Azure 기계 학습에서 hello R 언어를 사용 하 여 완벽 한 예측 솔루션을 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-108">As you work through tutorial, you will create a complete forecasting solution by using hello R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="eaa57-109">Microsoft Azure 기계 학습에는 강력한 기계 학습 및 데이터 조작 모듈이 많이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="eaa57-110">hello 강력한 R 언어에 특별히 만들어진 분석의 hello 공통 언어 라고 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-110">hello powerful R language has been described as hello lingua franca of analytics.</span></span> <span data-ttu-id="eaa57-111">다행히 오른쪽을 사용 하 여 Azure 기계 학습에서 분석 및 데이터 조작을 확장할 수 있습니다. 이 조합은 제공 hello 확장성 및 Azure 기계 학습의 배포의 용이성 hello 유연성 및 심층 분석은 R입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides hello scalability and ease of deployment of Azure Machine Learning with hello flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a><span data-ttu-id="eaa57-112">예측 및 hello 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="eaa57-112">Forecasting and hello dataset</span></span>
<span data-ttu-id="eaa57-113">예측은 널리 활용되고 매우 유용한 분석 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="eaa57-114">공통 최적의 재고 수준, toopredicting macroeconomic 변수 결정 계절 관련 항목에 대 한 판매 예측에서 범위를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, toopredicting macroeconomic variables.</span></span> <span data-ttu-id="eaa57-115">일반적으로 예측은 시계열 모델을 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="eaa57-116">시계열 데이터는 hello 값 시간 인덱스를 포함할 수 있는 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-116">Time series data is data in which hello values have a time index.</span></span> <span data-ttu-id="eaa57-117">예를 들어 매월 또는 1 분 마다 hello 시간 인덱스 보통, 수 또는 비 정기적인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-117">hello time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="eaa57-118">시계열 모델은 시계열 데이터를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-118">A time series model is based on time series data.</span></span> <span data-ttu-id="eaa57-119">hello R 프로그래밍 언어는 유연성 있는 프레임 워크 및 시계열 데이터에 대 한 광범위 한 분석을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-119">hello R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="eaa57-120">이 빠른 시작 가이드에서는 캘리포니아 유제품 생산 및 가격 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="eaa57-121">이 데이터는 여러 유제품 hello 생산 및 우유 fat, 벤치 마크 물품의 hello 가격에 월별 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-121">This data includes monthly information on hello production of several dairy products and hello price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="eaa57-122">hello 데이터는 R 스크립트와 함께이 문서에서 사용 가능 [여기에서 다운로드][download]합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-122">hello data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="eaa57-123">이 데이터를 원래 http://future.aae.wisc.edu/tab/production.html에 hello 위스콘신 대학에서에서 사용할 수 있는 정보에서 합성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-123">This data was originally synthesized from information available from hello University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="eaa57-124">조직</span><span class="sxs-lookup"><span data-stu-id="eaa57-124">Organization</span></span>
<span data-ttu-id="eaa57-125">Toocreate, 테스트 하 고 hello Azure 기계 학습 환경에서 분석 및 데이터 조작 R 코드를 실행 하는 방법을 배울 때 여러 단계가 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-125">We will progress through several steps as you learn how toocreate, test and execute analytics and data manipulation R code in hello Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="eaa57-126">먼저 hello R 언어를 사용 하 여 hello Azure 기계 학습 스튜디오 환경에서의 hello 기본 사항을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-126">First we will explore hello basics of using hello R language in hello Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="eaa57-127">그런 다음 진행 하는 과정 toodiscussing hello Azure 기계 학습 환경에서 데이터, R 코드 그래픽과 대 한 I/O의 다양 한 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-127">Then we progress toodiscussing various aspects of I/O for data, R code and graphics in hello Azure Machine Learning environment.</span></span>
* <span data-ttu-id="eaa57-128">그런 다음 데이터 정리 및 변환에 대 한 코드를 만들어 예측 솔루션의 hello 첫 번째 부분을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-128">We will then construct hello first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="eaa57-129">준비 된 데이터와이 데이터 집합에 있는 hello 변수의 여러 간의 hello 상관 관계에 대 한 분석을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-129">With our data prepared we will perform an analysis of hello correlations between several of hello variables in our dataset.</span></span>
* <span data-ttu-id="eaa57-130">마지막으로 우유 생산의 계절성 시계열 예측 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="eaa57-131"><a id="mlstudio"></a>기계 학습 스튜디오에서 R 언어와 상호 작용</span><span class="sxs-lookup"><span data-stu-id="eaa57-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="eaa57-132">이 섹션에서는 R hello hello 기계 학습 스튜디오 환경에서 프로그래밍 언어와의 상호 작용의 몇 가지 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-132">This section takes you through some basics of interacting with hello R programming language in hello Machine Learning Studio environment.</span></span> <span data-ttu-id="eaa57-133">hello R 언어에는 강력한 도구 toocreate 사용자 지정 분석 및 데이터 조작 모듈 hello Azure 기계 학습 환경 내에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-133">hello R language provides a powerful tool toocreate customized analytics and data manipulation modules within hello Azure Machine Learning environment.</span></span>

<span data-ttu-id="eaa57-134">작은 규모의 RStudio toodevelop, 테스트 및 디버그 R 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-134">I will use RStudio toodevelop, test and debug R code on a small scale.</span></span> <span data-ttu-id="eaa57-135">이 코드는 다음 잘라내기 및 붙여넣기에는 [R 스크립트 실행] [ execute-r-script] 준비 toorun 기계 학습 스튜디오의에서 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready toorun.</span></span>  

### <a name="hello-execute-r-script-module"></a><span data-ttu-id="eaa57-136">hello R 스크립트 실행 모듈</span><span class="sxs-lookup"><span data-stu-id="eaa57-136">hello Execute R Script module</span></span>
<span data-ttu-id="eaa57-137">기계 학습 스튜디오에서 R 스크립트는 hello 내에서 실행 됩니다 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-137">Within Machine Learning Studio, R scripts are run within hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="eaa57-138">Hello의 예로 [R 스크립트 실행] [ execute-r-script] 기계 학습 스튜디오의 모듈 그림 1에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-138">An example of hello [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![R 프로그래밍 언어: 기계 학습 스튜디오에서 선택한 hello R 스크립트 실행 모듈][1]

<span data-ttu-id="eaa57-140">*그림 1입니다. hello 기계 학습 스튜디오 환경 선택 hello R 스크립트 실행 모듈을 표시 합니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-140">*Figure 1. hello Machine Learning Studio environment showing hello Execute R Script module selected.*</span></span>

<span data-ttu-id="eaa57-141">Hello hello를 사용 하기 위한 hello 기계 학습 스튜디오 환경의 주요 부분 중 일부에 대해 살펴보겠습니다 tooFigure 1 참조, [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-141">Referring tooFigure 1, let's look at some of hello key parts of hello Machine Learning Studio environment for working with hello [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="eaa57-142">hello 실험에서 모듈 hello hello 가운데 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-142">hello modules in hello experiment are shown in hello center pane.</span></span>
* <span data-ttu-id="eaa57-143">hello hello 오른쪽 창 위쪽 부분 창 tooview를 포함 하 고 R 스크립트를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-143">hello upper part of hello right pane contains a window tooview and edit your R scripts.</span></span>  
* <span data-ttu-id="eaa57-144">hello의 일부 속성을 표시 하는 창 오른쪽의 아래쪽 hello [R 스크립트 실행][execute-r-script]합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-144">hello lower part of right pane shows some properties of hello [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="eaa57-145">이 창의 hello 적절 한 지점을 클릭 하 여 hello 오류 및 출력 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-145">You can view hello error and output logs by clicking on hello appropriate spots of this pane.</span></span>

<span data-ttu-id="eaa57-146">여기, 물론,에서 설명할 hello [R 스크립트 실행] [ execute-r-script] hello이이 문서의 나머지 부분에 더 자세히 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-146">We will, of course, be discussing hello [Execute R Script][execute-r-script] in greater detail in hello rest of this document.</span></span>

<span data-ttu-id="eaa57-147">복잡한 R 함수를 사용할 경우에는 RStudio에서 편집, 테스트 및 디버그하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="eaa57-148">모든 소프트웨어 개발에서와 마찬가지로 코드를 점차적으로 확장하고 간단한 작은 테스트 사례에서 테스트하세요.</span><span class="sxs-lookup"><span data-stu-id="eaa57-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="eaa57-149">함수 hello의 hello R 스크립트 창에 붙여 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-149">Then cut and paste your functions into hello R script window of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="eaa57-150">이 방법을 사용 하면 tooharness 모두 hello RStudio 통합된 개발 환경 (IDE) 및 Azure 기계 학습의 hello.</span><span class="sxs-lookup"><span data-stu-id="eaa57-150">This approach allows you tooharness both hello RStudio integrated development environment (IDE) and hello power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="eaa57-151">R 코드 실행</span><span class="sxs-lookup"><span data-stu-id="eaa57-151">Execute R code</span></span>
<span data-ttu-id="eaa57-152">Hello의 모든 R 코드 [R 스크립트 실행] [ execute-r-script] hello를 클릭 하 여 hello 실험을 실행할 때 모듈을 실행할 **실행** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-152">Any R code in hello [Execute R Script][execute-r-script] module will execute when you run hello experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="eaa57-153">Hello에 확인 표시가 나타나면 실행이 완료 되었을 때 [R 스크립트 실행] [ execute-r-script] 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-153">When execution has completed, a check mark will appear on hello [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="eaa57-154">Azure 기계 학습용 방어 R 코딩</span><span class="sxs-lookup"><span data-stu-id="eaa57-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="eaa57-155">Azure 기계 학습을 사용하여 웹 서비스용 R 코드를 개발하는 경우 코드가 예기치 않은 데이터 입력 및 예외를 처리할 방법을 확실히 계획해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="eaa57-156">toomaintain 명확성을 I 포함 하지 않고 거의 hello 방식으로 검사 또는 대부분의 표시 된 hello 코드 예제에서 예외 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-156">toomaintain clarity, I have not included much in hello way of checking or exception handling in most of hello code examples shown.</span></span> <span data-ttu-id="eaa57-157">하지만 계속 진행하면서 R의 예외 처리 기능을 사용하는 몇 가지 함수 예를 제공하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="eaa57-158">Hello에 나열 된 Wickham로 hello 책의 해당 섹션을 읽어 권장 R 예외 처리는 보다 완전 하 게 처리 해야 할 경우 [부록 B-추가 정보](#appendixb)합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-158">If you need a more complete treatment of R exception handling, I recommend you read hello applicable sections of hello book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="eaa57-159">기계 학습 스튜디오에서 R 디버깅 및 테스트</span><span class="sxs-lookup"><span data-stu-id="eaa57-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="eaa57-160">tooreiterate, 필자 권장 테스트 및 소규모 RStudio에 대 한 R 코드를 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-160">tooreiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="eaa57-161">그러나 hello에 대 한 R 코드 문제 아래로 tootrack 할 경우가 있습니다. [R 스크립트 실행] [ execute-r-script] 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-161">However, there are cases where you will need tootrack down R code problems in hello [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="eaa57-162">또한 것이 좋습니다 toocheck에서 결과 기계 학습 스튜디오 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-162">In addition, it is good practice toocheck your results in Machine Learning Studio.</span></span>

<span data-ttu-id="eaa57-163">Hello 실행 하 고 hello Azure 기계 학습 플랫폼에서 R 코드의 출력은 주로 output.log 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-163">Output from hello execution of your R code and on hello Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="eaa57-164">일부 추가 정보는 error.log에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="eaa57-165">기계 학습 스튜디오에서 R 코드를 실행 하는 동안 오류가 발생, 작업의 첫 번째 과정 error.log에서 toolook 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be toolook at error.log.</span></span> <span data-ttu-id="eaa57-166">이 파일에 유용한 오류 메시지 toohelp 이해 하 고 오류를 해결 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-166">This file can contain useful error messages toohelp you understand and correct your error.</span></span> <span data-ttu-id="eaa57-167">tooview error.log를 클릭 **오류 로그 보기** hello에 **속성 창** hello에 대 한 [R 스크립트 실행] [ execute-r-script] hello 오류를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-167">tooview error.log, click on **View error log** on hello **properties pane** for hello [Execute R Script][execute-r-script] containing hello error.</span></span>

<span data-ttu-id="eaa57-168">예를 들어, 필자는 정의 되지 않은 변수 y에 R 코드에서 다음 hello는 [R 스크립트 실행] [ execute-r-script] 모듈:</span><span class="sxs-lookup"><span data-stu-id="eaa57-168">For example, I ran hello following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="eaa57-169">이 코드는 오류 조건이 발생 tooexecute를 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-169">This code fails tooexecute, resulting in an error condition.</span></span> <span data-ttu-id="eaa57-170">클릭 하면 **오류 로그 보기** hello에 **속성 창** 생성 hello 그림 2에 표시 된 것으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-170">Clicking on **View error log** on hello **properties pane** produces hello display shown in Figure 2.</span></span>

  ![오류 메시지 팝업][2]

<span data-ttu-id="eaa57-172">*그림 2. 오류 메시지 팝업*</span><span class="sxs-lookup"><span data-stu-id="eaa57-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="eaa57-173">Toolook output.log toosee hello R 오류 메시지에 필요한 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-173">It looks like we need toolook in output.log toosee hello R error message.</span></span> <span data-ttu-id="eaa57-174">Hello 클릭 [R 스크립트 실행] [ execute-r-script] hello를 클릭 하 고 **output.log 볼** hello에 대 한 항목 **속성 창** toohello 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-174">Click on hello [Execute R Script][execute-r-script] and then click on hello **View output.log** item on hello **properties pane** toohello right.</span></span> <span data-ttu-id="eaa57-175">새 브라우저 창이 열리고 hello 다음 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-175">A new browser window opens, and I see hello following.</span></span>

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="eaa57-176">이 오류 메시지가 없는 예기치 않은 문제를 포함 하 고 명확 하 게 hello 문제를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-176">This error message contains no surprises and clearly identifies hello problem.</span></span>

<span data-ttu-id="eaa57-177">R에서 모든 개체의 tooinspect hello 값, 이러한 값 toohello output.log 파일로 인쇄할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-177">tooinspect hello value of any object in R, you can print these values toohello output.log file.</span></span> <span data-ttu-id="eaa57-178">값은 기본적으로 개체를 검사 하는 것에 대 한 hello 규칙 대화형 R 세션에서와 같이 동일한 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-178">hello rules for examining object values are essentially hello same as in an interactive R session.</span></span> <span data-ttu-id="eaa57-179">예를 들어 한 줄에 변수 이름을 입력 하는 경우 hello 개체의 hello 값 인쇄 toohello output.log 파일 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-179">For example, if you type a variable name on a line, hello value of hello object will be printed toohello output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="eaa57-180">기계 학습 스튜디오의 패키지</span><span class="sxs-lookup"><span data-stu-id="eaa57-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="eaa57-181">Azure 기계 학습은 350개가 넘는 사전 설치된 R 언어 패키지를 함께 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="eaa57-182">Hello 코드 hello에 다음을 사용할 수 있습니다 [R 스크립트 실행] [ execute-r-script] 모듈 tooretrieve hello 목록이 미리 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-182">You can use hello following code in hello [Execute R Script][execute-r-script] module tooretrieve a list of hello preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="eaa57-183">이 코드의 마지막 줄 hello hello 순간에 모르는 경우 계속 읽어 보십시오.</span><span class="sxs-lookup"><span data-stu-id="eaa57-183">If you don't understand hello last line of this code at hello moment, read on.</span></span> <span data-ttu-id="eaa57-184">Hello이이 문서의 나머지 부분에서 광범위 하 게 hello Azure 기계 학습 환경에서 R을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-184">In hello rest of this document we will extensively discuss using R in hello Azure Machine Learning environment.</span></span>

### <a name="introduction-toorstudio"></a><span data-ttu-id="eaa57-185">소개 tooRStudio</span><span class="sxs-lookup"><span data-stu-id="eaa57-185">Introduction tooRStudio</span></span>
<span data-ttu-id="eaa57-186">RStudio는 r 널리 사용 되는 IDE 편집, 테스트 및 디버깅이 퀵 스타트 가이드에 사용 된 hello R 코드의 일부에 대 한 RStudio를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of hello R code used in this quick start guide.</span></span> <span data-ttu-id="eaa57-187">R 코드를 테스트 및 준비 되 면 단순히 잘라내어 hello RStudio 편집기에서 기계 학습 스튜디오로 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-187">Once R code is tested and ready, you simply cut and paste from hello RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="eaa57-188">데스크톱 컴퓨터에 설치 된 R hello 프로그래밍 언어가 없는 경우 이렇게 하면 지금 것을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-188">If you do not have hello R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="eaa57-189">오픈 소스 R 언어의 무료 다운로드 hello 포괄적인 R 보관 네트워크 (CRAN)에서 사용할 수 있는에서 [http://www.r-project.org/](http://www.r-project.org/)합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-189">Free downloads of open source R language are available at hello Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="eaa57-190">Windows, Mac OS, Linux/UNIX용 다운로드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="eaa57-191">주변 미러를 선택 하 고 hello 다운로드 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-191">Choose a nearby mirror and follow hello download directions.</span></span> <span data-ttu-id="eaa57-192">또한 CRAN에는 유용한 분석 및 데이터 조작 패키지가 풍부하게 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="eaa57-193">새 tooRStudio 인 경우에 다운로드 하 고 hello 데스크톱 버전을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-193">If you are new tooRStudio, you should download and install hello desktop version.</span></span> <span data-ttu-id="eaa57-194">Http://www.rstudio.com/products/RStudio/에 Windows, Mac OS 및 Linux/UNIX 용 RStudio를 다운로드 하는 hello를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-194">You can find hello RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="eaa57-195">RStudio tooinstall 데스크톱 컴퓨터에서 제공 하는 hello 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-195">Follow hello directions provided tooinstall RStudio on your desktop machine.</span></span>  

<span data-ttu-id="eaa57-196">자습서 소개 tooRStudio https://support.rstudio.com/hc/sections/200107586-Using-RStudio에서 ´ ù입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-196">A tutorial introduction tooRStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="eaa57-197">[부록 A][appendixa]에 RStudio 사용에 대한 추가 정보가 일부 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="eaa57-198"><a id="scriptmodule"></a>Hello R 스크립트 실행 모듈 내부 및 외부 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="eaa57-198"><a id="scriptmodule"></a>Get data in and out of hello Execute R Script module</span></span>
<span data-ttu-id="eaa57-199">이 섹션에서는 다음과 같은 작용이 hello 안팎으로 데이터를 가져오는 방법을 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-199">In this section we will discuss how you get data into and out of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="eaa57-200">Toohandle 다양 한 데이터 형식을 읽는 방법 및 hello 외부로 검토할 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-200">We will review how toohandle various data types read into and out of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="eaa57-201">이전에 다운로드 한 hello zip 파일에이 섹션에 대 한 hello 전체 코드가입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-201">hello complete code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="eaa57-202">기계 학습 스튜디오에서 데이터 로드 및 확인</span><span class="sxs-lookup"><span data-stu-id="eaa57-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="eaa57-203"><a id="loading"></a>Hello 데이터 집합 로드</span><span class="sxs-lookup"><span data-stu-id="eaa57-203"><a id="loading"></a>Load hello dataset</span></span>
<span data-ttu-id="eaa57-204">Hello를 로드 하 여 먼저 **csdairydata.csv** Azure 기계 학습 스튜디오로 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-204">We will start by loading hello **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="eaa57-205">Azure 기계 학습 스튜디오 환경을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="eaa57-206">클릭 **+ 새로 만들기** hello에서 화면 및 선택의 왼쪽 하단 **Dataset**합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-206">Click on **+ NEW** at hello lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="eaa57-207">선택 **로컬 파일에서**, 차례로 **찾아보기** tooselect hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-207">Select **From Local File**, and then **Browse** tooselect hello file.</span></span>
* <span data-ttu-id="eaa57-208">선택 했는지 확인 **일반 CSV 파일 (.csv) 헤더로** hello 데이터 집합에 대 한 hello 종류로 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-208">Make sure you have selected **Generic CSV file with header (.csv)** as hello type for hello dataset.</span></span>
* <span data-ttu-id="eaa57-209">Hello 확인 표시를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-209">Click hello check mark.</span></span>
* <span data-ttu-id="eaa57-210">Hello를 클릭 하 여 hello 새 데이터 집합을 표시 해야 hello 데이터 집합을 업로드 후 **데이터 집합** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-210">After hello dataset has been uploaded, you should see hello new dataset by clicking on hello **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="eaa57-211">실험 만들기</span><span class="sxs-lookup"><span data-stu-id="eaa57-211">Create an experiment</span></span>
<span data-ttu-id="eaa57-212">기계 학습 스튜디오에서 일부 데이터를 만들었으므로 이제 해당 toocreate 실험 toodo hello 분석 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-212">Now that we have some data in Machine Learning Studio, we need toocreate an experiment toodo hello analysis.</span></span>  

* <span data-ttu-id="eaa57-213">클릭 **+ 새로 만들기** hello에서 왼쪽 아래로 하 고 선택 **실험**, 다음 **빈 실험**합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-213">Click on **+ NEW** at hello lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="eaa57-214">실험을 선택 하면 이름을 지정 하 고 hello 수정 수 **실험에 생성 중...**  hello hello 페이지 위쪽에는 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-214">You can name your experiment by selecting, and modifying, hello **Experiment created on ...** title at hello top of hello page.</span></span> <span data-ttu-id="eaa57-215">예를 들어 너무 변경**CA 유제품 분석**합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-215">For example, changing it too**CA Dairy Analysis**.</span></span>
* <span data-ttu-id="eaa57-216">Hello hello 실험 페이지의 왼쪽의 확장 **저장 된 데이터 집합**, 차례로 **내 데이터 집합**합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-216">On hello left of hello experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="eaa57-217">Hello 표시 되어야 **cadairydata.csv** 이전에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-217">You should see hello **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="eaa57-218">끌어서 놓기 hello **csdairydata.csv dataset** hello 실험에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-218">Drag and drop hello **csdairydata.csv dataset** onto hello experiment.</span></span>
* <span data-ttu-id="eaa57-219">Hello에 **검색 항목을 실험** hello 맨 hello 왼쪽된 창에서 형식 상자 [R 스크립트 실행][execute-r-script]합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-219">In hello **Search experiment items** box on hello top of hello left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="eaa57-220">Hello 검색 목록에 표시 하는 hello 모듈을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-220">You will see hello module appear in hello search list.</span></span>
* <span data-ttu-id="eaa57-221">끌어서 놓기 hello [R 스크립트 실행] [ execute-r-script] 프로그램 팔레트에 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-221">Drag and drop hello [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="eaa57-222">Hello hello 출력에 연결 **csdairydata.csv dataset** toohello 맨 왼쪽 입력 (**Dataset1**)의 hello [R 스크립트 실행][execute-r-script]합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-222">Connect hello output of hello **csdairydata.csv dataset** toohello leftmost input (**Dataset1**) of hello [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="eaa57-223">**저장 tooclick를 잊지 마십시오!**</span><span class="sxs-lookup"><span data-stu-id="eaa57-223">**Don't forget tooclick on 'Save'!**</span></span>  

<span data-ttu-id="eaa57-224">이때 실험이 그림 3과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-224">At this point your experiment should look something like Figure 3.</span></span>

![데이터 집합 및 R 스크립트 실행 모듈을 시험해 hello CA 유제품 분석][3]

<span data-ttu-id="eaa57-226">*그림 3입니다. hello CA 유제품 분석 데이터 집합 및 R 스크립트 실행 모듈으로 시험 합니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-226">*Figure 3. hello CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-hello-data"></a><span data-ttu-id="eaa57-227">Hello 데이터 확인</span><span class="sxs-lookup"><span data-stu-id="eaa57-227">Check on hello data</span></span>
<span data-ttu-id="eaa57-228">우리의 실험으로 로드 하는 hello 데이터를 살펴봅시다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-228">Let's have a look at hello data we have loaded into our experiment.</span></span> <span data-ttu-id="eaa57-229">Hello 실험에서 hello의 hello 출력에서 클릭 **cadairydata.csv dataset** 선택 **시각화**합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-229">In hello experiment, click on hello output of hello **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="eaa57-230">그림 4와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-230">You should see something like Figure 4.</span></span>  

![Hello cadairydata.csv 데이터 집합의 요약][4]

<span data-ttu-id="eaa57-232">*그림 4. Hello cadairydata.csv 데이터 집합의 요약입니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-232">*Figure 4. Summary of hello cadairydata.csv dataset.*</span></span>

<span data-ttu-id="eaa57-233">여기에서 많은 유용한 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="eaa57-234">았습니다 해당 데이터 집합의 첫 번째 여러 행을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-234">We can see hello first several rows of that dataset.</span></span> <span data-ttu-id="eaa57-235">열을 선택 하는 경우 hello 통계 섹션 hello 열에 대 한 자세한 정보를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-235">If we select a column, hello Statistics section shows more information about hello column.</span></span> <span data-ttu-id="eaa57-236">예를 들어 hello 기능 유형 행이 보여줍니다 Azure 기계 학습 스튜디오 할당 toohello 열 데이터 형식.</span><span class="sxs-lookup"><span data-stu-id="eaa57-236">For example, hello Feature Type row shows us what data types Azure Machine Learning Studio assigned toohello column.</span></span> <span data-ttu-id="eaa57-237">심각한 작업 toodo 시작 하기 전에 좋은 온전성 검사는 다음과 같이 신속 하 게 확인할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-237">Having a quick look like this is a good sanity check before we start toodo any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="eaa57-238">첫 번째 R 스크립트</span><span class="sxs-lookup"><span data-stu-id="eaa57-238">First R script</span></span>
<span data-ttu-id="eaa57-239">Azure 기계 학습 스튜디오에서 간단한 첫 번째 R 스크립트 tooexperiment와를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-239">Let's create a simple first R script tooexperiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="eaa57-240">만든를 있으며 hello 따라 RStudio에서 스크립트를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-240">I have created and tested hello following script in RStudio.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="eaa57-241">이제 tootransfer 스크립트 tooAzure 기계 학습 스튜디오가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-241">Now I need tootransfer this script tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="eaa57-242">간단히 잘라내고 붙여넣을 수 있지만</span><span class="sxs-lookup"><span data-stu-id="eaa57-242">I could simply cut and paste.</span></span> <span data-ttu-id="eaa57-243">이 경우에서는 R 스크립트를 zip 파일을 통해 전송하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-toohello-execute-r-script-module"></a><span data-ttu-id="eaa57-244">데이터 입력된 toohello R 스크립트 실행 모듈</span><span class="sxs-lookup"><span data-stu-id="eaa57-244">Data input toohello Execute R Script module</span></span>
<span data-ttu-id="eaa57-245">Hello 입력 toohello에서 살펴봅시다 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-245">Let's have a look at hello inputs toohello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="eaa57-246">이 예제에서는 hello 캘리포니아 dairy 데이터 읽습니다 hello에 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-246">In this example we will read hello California dairy data into hello [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="eaa57-247">Hello에 대 한 입력이 세 가지 가능한 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-247">There are three possible inputs for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="eaa57-248">응용 프로그램에 따라 이러한 입력을 하나만 사용하거나 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="eaa57-249">또한 전혀 없는 입력을 사용 하는 완벽 하 게 합리적인 toouse R 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-249">It is also perfectly reasonable toouse an R script that takes no input at all.</span></span>  

<span data-ttu-id="eaa57-250">Tooright 왼쪽된에서 이동 하는 이러한 입력을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-250">Let's look at each of these inputs, going from left tooright.</span></span> <span data-ttu-id="eaa57-251">Hello 입력 위에 커서를 놓으면 도구 설명 hello를 검토 하 여 각 hello 입력의 hello 이름을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-251">You can see hello names of each of hello inputs by placing your cursor over hello input and reading hello tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="eaa57-252">스크립트 번들</span><span class="sxs-lookup"><span data-stu-id="eaa57-252">Script Bundle</span></span>
<span data-ttu-id="eaa57-253">hello 스크립트 번들 입력 하면에 zip 파일의 toopass hello 내용을 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-253">hello Script Bundle input allows you toopass hello contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="eaa57-254">Hello hello zip 파일의 명령을 tooread hello 내용을 R 코드를 다음 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-254">You can use one of hello following commands tooread hello contents of hello zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="eaa57-255">Azure 기계 학습 hello src 있는 것 처럼 hello zip에서 파일을 처리 / 디렉터리 tooprefix 파일에이 디렉터리 이름의 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-255">Azure Machine Learning treats files in hello zip as if they are in hello src/ directory, so you need tooprefix your file names with this directory name.</span></span> <span data-ttu-id="eaa57-256">예를 들어 경우 hello zip 파일이 hello `yourfile.R` 및 `yourData.rdata` hello zip hello 루트에 있는 사용자는 이러한 문제를 해결으로 `src/yourfile.R` 및 `src/yourData.rdata` 사용 하는 경우 `source` 및 `load`합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-256">For example, if hello zip contains hello files `yourfile.R` and `yourData.rdata` in hello root of hello zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="eaa57-257">로드 데이터 집합에서 이미 설명한 [hello 데이터 집합 로드](#loading)합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-257">We already discussed loading datasets in [Loading hello dataset](#loading).</span></span> <span data-ttu-id="eaa57-258">만든 hello 이전 섹션에 표시 된 hello R 스크립트를 테스트 한 후 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-258">Once you have created and tested hello R script shown in hello previous section, do hello following:</span></span>

1. <span data-ttu-id="eaa57-259">Hello R 스크립트를 저장 한 합니다. R 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-259">Save hello R script into a .R file.</span></span> <span data-ttu-id="eaa57-260">이 스크립트 파일을 "simpleplot.R"이라고 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="eaa57-261">Hello 내용을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-261">Here's hello contents.</span></span>
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="eaa57-262">Zip 파일을 만들고 스크립트를 이 zip 파일에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="eaa57-263">Windows에서는 hello 파일을 마우스 오른쪽 단추로 클릭 및 선택 수 **보내기**, 차례로 **압축 폴더**합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-263">On Windows, you can right-click on hello file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="eaa57-264">이렇게 하면 hello "simpleplot 포함 된 zip 파일을 새로 만들어집니다. R"파일입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-264">This will create a new zip file containing hello "simpleplot.R" file.</span></span>
3. <span data-ttu-id="eaa57-265">추가 파일 toohello **데이터 집합** hello 형식으로 지정 되는 기계 학습 스튜디오에서 **zip**합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-265">Add your file toohello **datasets** in Machine Learning Studio, specifying hello type as **zip**.</span></span> <span data-ttu-id="eaa57-266">이제 데이터 집합에서 hello zip 파일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-266">You should now see hello zip file in your datasets.</span></span>
4. <span data-ttu-id="eaa57-267">끌어서 놓기 hello zip 파일에서 **데이터 집합** hello에 **기계 학습 스튜디오 캔버스**합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-267">Drag and drop hello zip file from **datasets** onto hello **ML Studio canvas**.</span></span>
5. <span data-ttu-id="eaa57-268">Hello hello 출력에 연결 **데이터 zip** 아이콘 toohello **스크립트 번들** hello의 입력 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-268">Connect hello output of hello **zip data** icon toohello **Script Bundle** input of hello [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="eaa57-269">형식 hello `source()` 함수 hello에 대 한 hello 코드 창에 zip 파일 이름으로 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-269">Type hello `source()` function with your zip file name into hello code window for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="eaa57-270">제 경우 `source("src/simpleplot.R")`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="eaa57-271">반드시 **저장**을 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="eaa57-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="eaa57-272">다음이 단계 완료 되 면 hello [R 스크립트 실행] [ execute-r-script] hello 실험 실행 될 때 모듈 hello zip 파일의 hello R 스크립트 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-272">Once these steps are complete, hello [Execute R Script][execute-r-script] module will execute hello R script in hello zip file when hello experiment is run.</span></span> <span data-ttu-id="eaa57-273">이때 실험이 그림 5와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-273">At this point your experiment should look something like Figure 5.</span></span>

![압축된 R 스크립트를 사용한 실험][6]

<span data-ttu-id="eaa57-275">*그림 5. 압축된 R 스크립트를 사용한 실험*</span><span class="sxs-lookup"><span data-stu-id="eaa57-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="eaa57-276">Dataset1</span><span class="sxs-lookup"><span data-stu-id="eaa57-276">Dataset1</span></span>
<span data-ttu-id="eaa57-277">Dataset1 hello 입력을 사용 하 여 데이터 tooyour R 코드의 사각형 테이블을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-277">You can pass a rectangular table of data tooyour R code by using hello Dataset1 input.</span></span> <span data-ttu-id="eaa57-278">이 간단한 스크립트 hello에 `maml.mapInputPort(1)` 함수 포트 1에서에서 hello 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-278">In our simple script hello `maml.mapInputPort(1)` function reads hello data from port 1.</span></span> <span data-ttu-id="eaa57-279">이 데이터 tooa 코드에서 변수 이름 데이터 프레임 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-279">This data is then assigned tooa dataframe variable name in your code.</span></span> <span data-ttu-id="eaa57-280">간단한 스크립트 코드의 첫 번째 줄 hello hello 할당을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-280">In our simple script hello first line of code performs hello assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="eaa57-281">Hello를 클릭 하 여 실험을 실행 **실행** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-281">Execute your experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="eaa57-282">Hello 실행이 끝날 때 클릭 hello [R 스크립트 실행] [ execute-r-script] 모듈과 클릭 **출력 로그 보기** hello 속성 창에서.</span><span class="sxs-lookup"><span data-stu-id="eaa57-282">When hello execution finishes, click on hello [Execute R Script][execute-r-script] module and then click **View output log** on hello properties pane.</span></span> <span data-ttu-id="eaa57-283">새 페이지를 보여주는 hello output.log 파일의 내용을 hello 브라우저에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-283">A new page should appear in your browser showing hello contents of hello output.log file.</span></span> <span data-ttu-id="eaa57-284">스크롤할 때 표시 되어야 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-284">When you scroll down you should see something like hello following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="eaa57-285">멀리 hello 아래로 페이지는 hello 다음과 유사할는 hello 열에 대 한 더 자세한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-285">Farther down hello page is more detailed information on hello columns, which will look something like hello following.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

<span data-ttu-id="eaa57-286">이러한 결과 228 관측값과 hello 데이터 프레임에서 9 열이 있는 예상 대로 대부분 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-286">These results are mostly as expected, with 228 observations and 9 columns in hello dataframe.</span></span> <span data-ttu-id="eaa57-287">Hello 열 이름, hello R 데이터 형식 및 각 열의 예제를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-287">We can see hello column names, hello R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="eaa57-288">이 동일한 인쇄 출력은 hello hello의 R 장치 출력에서에서 편리 하 게 사용할 수 있는 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-288">This same printed output is conveniently available from hello R Device output of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="eaa57-289">다음과 같은 작용이 hello의 hello 출력 [R 스크립트 실행] [ execute-r-script] hello 다음 섹션에는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-289">We will discuss hello outputs of hello [Execute R Script][execute-r-script] module in hello next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="eaa57-290">Dataset2</span><span class="sxs-lookup"><span data-stu-id="eaa57-290">Dataset2</span></span>
<span data-ttu-id="eaa57-291">hello hello Dataset2 입력의 동작은 Dataset1의 동일한 toothat입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-291">hello behavior of hello Dataset2 input is identical toothat of Dataset1.</span></span> <span data-ttu-id="eaa57-292">이 입력을 사용하여 두 번째 사각형의 데이터 테이블을 R 코드에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="eaa57-293">함수 hello `maml.mapInputPort(2)`, hello 인수 2는 사용 되는 toopass이이 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-293">hello function `maml.mapInputPort(2)`, with hello argument 2, is used toopass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="eaa57-294">R 스크립트 실행 출력</span><span class="sxs-lookup"><span data-stu-id="eaa57-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="eaa57-295">데이터 프레임 출력</span><span class="sxs-lookup"><span data-stu-id="eaa57-295">Output a dataframe</span></span>
<span data-ttu-id="eaa57-296">Hello를 사용 하 여 hello 결과 Dataset1 포트를 통해 사각형 테이블로 R 데이터 프레임의 hello 내용을 출력할 수 `maml.mapOutputPort()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-296">You can output hello contents of an R dataframe as a rectangular table through hello Result Dataset1 port by using hello `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="eaa57-297">간단한 R 스크립트에서이 다음 줄 hello 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-297">In our simple R script this is performed by hello following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="eaa57-298">실행 중인 hello 실험 한 후 hello 결과 Dataset1 출력 포트를 클릭 하 고 클릭 한 다음 **시각화**합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-298">After running hello experiment, click on hello Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="eaa57-299">그림 6과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-299">You should see something like Figure 6.</span></span>

![hello 캘리포니아 dairy 데이터의 hello 출력의 hello 시각화][7]

<span data-ttu-id="eaa57-301">*그림 6입니다. hello 캘리포니아 dairy 데이터의 hello 출력의 hello 시각화 합니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-301">*Figure 6. hello visualization of hello output of hello California dairy data.*</span></span>

<span data-ttu-id="eaa57-302">이 출력이 똑같습니다 동일한 toohello 입력이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-302">This output looks identical toohello input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="eaa57-303">R 장치 출력</span><span class="sxs-lookup"><span data-stu-id="eaa57-303">R Device output</span></span>
<span data-ttu-id="eaa57-304">hello의 장치 출력 hello [R 스크립트 실행] [ execute-r-script] 모듈 메시지와 그래픽 출력을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-304">hello Device output of hello [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="eaa57-305">R에서 메시지를 모두 표준 출력과 표준 오류 toohello R 장치 출력 포트로 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-305">Both standard output and standard error messages from R are sent toohello R Device output port.</span></span>  

<span data-ttu-id="eaa57-306">R 장치 출력으로 hello 포트를 선택한 다음 클릭 tooview hello **시각화**합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-306">tooview hello R Device output, click on hello port and then on **Visualize**.</span></span> <span data-ttu-id="eaa57-307">Hello 표준 출력과 표준 오류 그림 7에 hello R 스크립트에서 보면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-307">We see hello standard output and standard error from hello R script in Figure 7.</span></span>

![표준 출력과 표준 오류 hello R 장치 포트에서][8]

<span data-ttu-id="eaa57-309">*그림 7. 표준 출력과 표준 오류 hello R 장치 포트에서*</span><span class="sxs-lookup"><span data-stu-id="eaa57-309">*Figure 7. Standard output and standard error from hello R Device port.*</span></span>

<span data-ttu-id="eaa57-310">म 아래로 그림 8에 R 스크립트에서 hello 그래픽 출력 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-310">Scrolling down we see hello graphics output from our R script in Figure 8.</span></span>  

![R 장치 포트 hello 그래픽 출력][9]

<span data-ttu-id="eaa57-312">*그림 8. R 장치 포트 hello에서 출력 하는 그래픽입니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-312">*Figure 8. Graphics output from hello R Device port.*</span></span>  

## <span data-ttu-id="eaa57-313"><a id="filtering"></a>데이터 필터링 및 변환</span><span class="sxs-lookup"><span data-stu-id="eaa57-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="eaa57-314">이 섹션에서는 기본 데이터 필터링 및 변환 작업 hello 캘리포니아 dairy 데이터에 몇 가지를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-314">In this section we will perform some basic data filtering and transformation operations on hello California dairy data.</span></span> <span data-ttu-id="eaa57-315">이 섹션의 hello 끝으로 데이터 분석 모델을 작성 하는 데 적합 한 형식에 있는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-315">By hello end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="eaa57-316">더욱 구체적으로 설명하자면 이 섹션에서 여러 일반적인 데이터 정리 및 변환 작업(형식 변환, 데이터 프레임 필터링, 새 계산 열 추가, 값 변환)을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="eaa57-317">이 배경은 실제 문제에서 발생 하는 여러 변형이 hello로 처리 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-317">This background should help you deal with hello many variations encountered in real-world problems.</span></span>

<span data-ttu-id="eaa57-318">이 섹션에 대 한 hello 전체 R 코드는 이전에 다운로드 한 hello zip 파일에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-318">hello complete R code for this section is available in hello zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="eaa57-319">형식 변환</span><span class="sxs-lookup"><span data-stu-id="eaa57-319">Type transformations</span></span>
<span data-ttu-id="eaa57-320">Hello 캘리포니아 dairy 데이터 hello hello R 코드를 읽을 수 했으므로 [R 스크립트 실행] [ execute-r-script] 모듈 hello hello 열에는 데이터에는 의도 한 hello 유형 및 형식을 tooensure 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-320">Now that we can read hello California dairy data into hello R code in hello [Execute R Script][execute-r-script] module, we need tooensure that hello data in hello columns has hello intended type and format.</span></span>  

<span data-ttu-id="eaa57-321">R은는 동적으로 형식화 된 언어는 데이터 형식에서 필요에 따라 하나의 tooanother 강제 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-321">R is a dynamically typed language, which means that data types are coerced from one tooanother as required.</span></span> <span data-ttu-id="eaa57-322">hello 원자성 데이터 형식을 R에서 숫자, 논리 및 문자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-322">hello atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="eaa57-323">hello 요소 형식은 사용 되는 toocompactly 범주 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-323">hello factor type is used toocompactly store categorical data.</span></span> <span data-ttu-id="eaa57-324">hello 참조에서 데이터 형식에 대 한 자세한 정보를 제공 수 [부록 B-추가 읽기](#appendixb)합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-324">You can find much more information on data types in hello references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="eaa57-325">테이블 형식 데이터를 외부 소스에서 R로 읽을 때 항상 hello 열에서 형식으로 인해 발생 하는 것이 좋습니다 toocheck hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-325">When tabular data is read into R from an external source, it is always a good idea toocheck hello resulting types in hello columns.</span></span> <span data-ttu-id="eaa57-326">문자 형식의 열을 원하더라도 많은 경우 이 열은 요소로 표시되거나 그 반대로 요소가 문자 형식으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="eaa57-327">그 밖의 경우 구상 중인 열은 부동 소수점 숫자가 아닌 문자 데이터, 즉 1.23이 아닌 '1.23'으로 나타내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="eaa57-328">다행히 매핑이 불가능으로 쉽게 tooconvert 하나 형식 tooanother, 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-328">Fortunately, it is easy tooconvert one type tooanother, as long as mapping is possible.</span></span> <span data-ttu-id="eaa57-329">예를 들어 '네바다' 숫자 값으로 변환할 수는 없지만 tooa 요소 (범주 변수)를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it tooa factor (categorical variable).</span></span> <span data-ttu-id="eaa57-330">또 다른 예로 숫자 1을 문자 '1'이나 요소로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="eaa57-331">이러한 변환에 대 한 hello 구문은 간단: `as.datatype()`합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-331">hello syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="eaa57-332">이러한 형식 변환 함수 hello 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-332">These type conversion functions include hello following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="eaa57-333">Hello 데이터 종류 hello 입력의 열에서는 hello 이전 섹션에서 확인: 숫자, 'Month' 형식 문자는 hello 열을 제외한 형식의 모든 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-333">Looking at hello data types of hello columns we input in hello previous section: all columns are of type numeric, except for hello column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="eaa57-334">이 tooa 요소를 변환 하 고 테스트 결과 hello 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-334">Let's convert this tooa factor and test hello results.</span></span>  

<span data-ttu-id="eaa57-335">Hello scatterplot 행렬을 만들고 hello 'Month' 열 tooa 요소를 변환 하는 줄을 추가 하는 hello 줄을 삭제 했습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-335">I have deleted hello line that created hello scatterplot matrix and added a line converting hello 'Month' column tooa factor.</span></span> <span data-ttu-id="eaa57-336">내 실험에서 필자는 방금 잘라내기 및 붙여넣기 hello R 코드의 hello hello 코드 창에 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-336">In my experiment I will just cut and paste hello R code into hello code window of hello [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="eaa57-337">도 hello zip 파일을 업데이트 하 고 tooAzure 기계 학습 스튜디오에 업로드할 수 마이그레이션하지만이 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-337">You could also update hello zip file and upload it tooAzure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="eaa57-338">이 코드를 실행 하 고 R 스크립트 hello에 대 한 hello 출력 로그를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-338">Let's execute this code and look at hello output log for hello R script.</span></span> <span data-ttu-id="eaa57-339">hello hello 로그에서 관련 데이터는 그림 9에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-339">hello relevant data from hello log is shown in Figure 9.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="eaa57-340">*그림 9. 계수 변수로 hello 데이터 프레임의 요약입니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-340">*Figure 9. Summary of hello dataframe with a factor variable.*</span></span>

<span data-ttu-id="eaa57-341">월에 대 한 hello 유형 이어야 이제 '**14 개 수준 w / 비율**'.</span><span class="sxs-lookup"><span data-stu-id="eaa57-341">hello type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="eaa57-342">이것이 문제가 hello 연도에 12 개월만 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-342">This is a problem since there are only 12 months in hello year.</span></span> <span data-ttu-id="eaa57-343">형식 hello toosee을 확인할 수 있습니다에 **시각화** hello 결과 데이터 집합의 포트는 '**범주별**'.</span><span class="sxs-lookup"><span data-stu-id="eaa57-343">You can also check toosee that hello type in **Visualize** of hello Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="eaa57-344">hello 문제는 해당 hello 'Month' 열 체계적으로 코딩 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-344">hello problem is that hello 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="eaa57-345">어떤 경우에는 April라고 하고 또 어떤 경우에는 Apr로 줄여서 표시하기도 합니다. Hello 문자열 too3 문자 트리밍 하 여이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming hello string too3 characters.</span></span> <span data-ttu-id="eaa57-346">이제 코드 줄 hello hello 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-346">hello line of code now looks like hello following:</span></span>

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="eaa57-347">Hello 실험을 다시 실행 하 고 hello 출력 로그를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-347">Rerun hello experiment and view hello output log.</span></span> <span data-ttu-id="eaa57-348">hello 예상 결과 그림 10에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-348">hello expected results are shown in Figure 10.</span></span>  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="eaa57-349">*그림 10. 올바른 요소 수준 수가 hello 데이터 프레임의 요약입니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-349">*Figure 10. Summary of hello dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="eaa57-350">변수는 hello 원하는 12 개의 수준이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-350">Our factor variable now has hello desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="eaa57-351">기본 데이터 프레임 필터링</span><span class="sxs-lookup"><span data-stu-id="eaa57-351">Basic data frame filtering</span></span>
<span data-ttu-id="eaa57-352">R 데이터 프레임은 강력한 필터링 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="eaa57-353">행이나 열에 논리 필터를 사용하여 데이터 집합을 하위 집합으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="eaa57-354">대부분의 경우 복잡한 필터 조건을 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="eaa57-355">참조 하는 hello [부록 B-추가 읽기](#appendixb) 데이터 프레임을 필터링 하는 광범위 한 예제가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-355">hello references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="eaa57-356">이 데이터 집합에서 수행해야 하는 필터링이 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="eaa57-357">Hello cadairydata 데이터 프레임의 hello 열을 보면 두 개의 불필요 한 열 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-357">If you look at hello columns in hello cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="eaa57-358">hello 첫 번째 열에는 방금 매우 유용 하지 않는 행 번호를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-358">hello first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="eaa57-359">hello 두 번째 열에서 Year.Month, 중복 된 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-359">hello second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="eaa57-360">쉽게 hello 다음 R 코드를 사용 하 여 이러한 열을 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-360">We can easily exclude these columns by using hello following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="eaa57-361">이 섹션에서는 방금 드리도록 하겠습니다 이제 있습니다 hello hello에 추가 하 고 I 하는 추가 코드 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-361">From now on in this section, I will just show you hello additional code I am adding in hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="eaa57-362">각 새 줄에 추가 합니다. **전에** hello `str()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-362">I will add each new line **before** hello `str()` function.</span></span> <span data-ttu-id="eaa57-363">사용이 함수 tooverify 결과 Azure 기계 학습 스튜디오에서.</span><span class="sxs-lookup"><span data-stu-id="eaa57-363">I use this function tooverify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="eaa57-364">Hello 줄 toomy R 코드 hello에 다음을 추가 하려면 [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-364">I add hello following line toomy R code in hello [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="eaa57-365">실험에서이 코드를 실행 하 고 출력 로그 hello hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-365">Run this code in your experiment and check hello result from hello output log.</span></span> <span data-ttu-id="eaa57-366">이러한 결과는 그림 11에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-366">These results are shown in Figure 11.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="eaa57-367">*그림 11. 제거 하는 두 개의 열이 있는 hello 데이터 프레임의 요약입니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-367">*Figure 11. Summary of hello dataframe with two columns removed.*</span></span>

<span data-ttu-id="eaa57-368">기쁘게도</span><span class="sxs-lookup"><span data-stu-id="eaa57-368">Good news!</span></span> <span data-ttu-id="eaa57-369">Hello 예상 결과가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-369">We get hello expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="eaa57-370">새 열 추가</span><span class="sxs-lookup"><span data-stu-id="eaa57-370">Add a new column</span></span>
<span data-ttu-id="eaa57-371">시계열 모델의 toocreate 편리한 toohave hello 시계열 hello 시작 된 이후 개월 hello 포함 하는 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-371">toocreate time series models it will be convenient toohave a column containing hello months since hello start of hello time series.</span></span> <span data-ttu-id="eaa57-372">'Month.Count'라는 열을 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="eaa57-373">첫 번째 간단한 함수를 만듭니다 hello 코드를 구성 하는 toohelp `num.month()`합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-373">toohelp organize hello code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="eaa57-374">다음 함수 toocreate hello 데이터 프레임에서 새 열이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-374">We will then apply this function toocreate a new column in hello dataframe.</span></span> <span data-ttu-id="eaa57-375">hello 새 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-375">hello new code is as follows.</span></span>

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="eaa57-376">이제 업데이트 hello 실험을 실행 하 고 hello 결과물 로그 tooview hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-376">Now run hello updated experiment and use hello output log tooview hello results.</span></span> <span data-ttu-id="eaa57-377">이러한 결과는 그림 12에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-377">These results are shown in Figure 12.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="eaa57-378">*그림 12. Hello 추가 열이 있는 hello 데이터 프레임의 요약입니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-378">*Figure 12. Summary of hello dataframe with hello additional column.*</span></span>

<span data-ttu-id="eaa57-379">모두 제대로 작동하는 것 같으며</span><span class="sxs-lookup"><span data-stu-id="eaa57-379">It looks like everything is working.</span></span> <span data-ttu-id="eaa57-380">Hello hello 예상 값을 가진 새 열이 데이터 프레임에 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-380">We have hello new column with hello expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="eaa57-381">값 변환</span><span class="sxs-lookup"><span data-stu-id="eaa57-381">Value transformations</span></span>
<span data-ttu-id="eaa57-382">이 섹션의 hello 값이 데이터 프레임의 hello 열 중 일부에 대해 몇 가지 간단한 변환을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-382">In this section we will perform some simple transformations on hello values in some of hello columns of our dataframe.</span></span> <span data-ttu-id="eaa57-383">hello R 언어에는 거의 임의의 값 변환을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-383">hello R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="eaa57-384">참조 하는 hello [부록 B-추가 정보](#appendixb) 광범위 한 예가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-384">hello references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="eaa57-385">Hello 값이 데이터 프레임의 hello 요약에서 보면 표시 되어야 뭔가 이상 여기 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-385">If you look at hello values in hello summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="eaa57-386">캘리포니아에서 아이스크림이 우유보다 더 많이 생산되나요?</span><span class="sxs-lookup"><span data-stu-id="eaa57-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="eaa57-387">아니요, 물론,이 인해 이해,이 팩트로 sad 수 하지 미국 toosome 아이스크림 입력.</span><span class="sxs-lookup"><span data-stu-id="eaa57-387">No, of course not, as this makes no sense, sad as this fact may be toosome of us ice cream lovers.</span></span> <span data-ttu-id="eaa57-388">hello 단위 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-388">hello units are different.</span></span> <span data-ttu-id="eaa57-389">hello 가격 파운드, 우유 1m 단위로 1,000 단위로 미국 파운드, 아이스크림은 US 갤런, 이며 별장 cheese 1, 000 미국 파운드 단위에서 우리는 단위에서입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-389">hello price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="eaa57-390">아이스크림 정도와 갤런 당 약 6.5 파운드 라고 가정할 경우을 활용해 서 쉽게 이들 값이 1, 000 파운드의 단위를 같은 모두에 맞게 곱하기 tooconvert hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do hello multiplication tooconvert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="eaa57-391">이 예측 모델의 경우 이 데이터의 추세 및 계절성 조정을 위해 승법 모형을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="eaa57-392">로그 변환을 toouse이이 과정을 단순화 하는 선형 모델을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-392">A log transformation allows us toouse a linear model, simplifying this process.</span></span> <span data-ttu-id="eaa57-393">Hello 동일 함수 hello 승수 적용 되는 위치에 hello 로그 변환을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-393">We can apply hello log transformation in hello same function where hello multiplier is applied.</span></span>

<span data-ttu-id="eaa57-394">새 함수를 정의 하려면 코드 다음 hello에서 `log.transform()`, hello 숫자 값이 포함 된 toohello 행을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-394">In hello following code, I define a new function, `log.transform()`, and apply it toohello rows containing hello numerical values.</span></span> <span data-ttu-id="eaa57-395">hello R `Map()` 함수는 사용 되는 tooapply hello `log.transform()` 함수 toohello hello 데이터 프레임의 열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-395">hello R `Map()` function is used tooapply hello `log.transform()` function toohello selected columns of hello dataframe.</span></span> <span data-ttu-id="eaa57-396">`Map()`너무 유사`apply()` 둘 이상의 인수 toohello 함수 목록이 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-396">`Map()` is similar too`apply()` but allows for more than one list of arguments toohello function.</span></span> <span data-ttu-id="eaa57-397">승수 목록이 두 번째 인수 toohello hello를 제공 하는 참고 `log.transform()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-397">Note that a list of multipliers supplies hello second argument toohello `log.transform()` function.</span></span> <span data-ttu-id="eaa57-398">hello `na.omit()` 함수는 약간의 정리 tooensure 없으므로 누락 또는에 정의 되지 않은 값 hello 데이터 프레임으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-398">hello `na.omit()` function is used as a bit of cleanup tooensure we do not have missing or undefined values in hello dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="eaa57-399">Hello에는 비트 상황이 발생 하지는 `log.transform()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-399">There is quite a bit happening in hello `log.transform()` function.</span></span> <span data-ttu-id="eaa57-400">이 코드의 대부분을 hello 인수도 잠재적인 문제에 대 한 확인 되었거나 여전히 hello 계산 하는 동안 발생할 수 있는 예외를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-400">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="eaa57-401">이 코드의 몇 줄만 실제로 계산 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-401">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="eaa57-402">hello 방어 프로그래밍의 hello 목표는 처리를 계속할 수 없는 단일 함수의 tooprevent hello 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-402">hello goal of hello defensive programming is tooprevent hello failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="eaa57-403">장기 실행 분석의 갑작스런 실패는 사용자에게 상당한 불만을 초래할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="eaa57-404">이 경우 기본 반환 값을 선택 해야 하는 제한 tooavoid 손상 toodownstream 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-404">tooavoid this situation, default return values must be chosen that will limit damage toodownstream processing.</span></span> <span data-ttu-id="eaa57-405">메시지 무언가 떨어졌습니다. 잘못 생성 된 tooalert 사용자 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-405">A message is also produced tooalert users that something has gone wrong.</span></span>

<span data-ttu-id="eaa57-406">R에서 사용 되는 toodefensive 프로그래밍 없는 경우이 모든 코드는 약간 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-406">If you are not used toodefensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="eaa57-407">필자는 안내 hello 주요 단계:</span><span class="sxs-lookup"><span data-stu-id="eaa57-407">I will walk you through hello major steps:</span></span>

1. <span data-ttu-id="eaa57-408">네 개 메시지의 벡터가 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-408">A vector of four messages is defined.</span></span> <span data-ttu-id="eaa57-409">이러한 메시지는이 코드에서 발생할 수 있는 hello 가능한 오류와 예외 중 일부에 대 한 사용 되는 toocommunicate 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-409">These messages are used toocommunicate information about some of hello possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="eaa57-410">각각의 경우에 대해 NA 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-410">I return a value of NA for each case.</span></span> <span data-ttu-id="eaa57-411">부작용이 더 적을 수 있는 다른 가능성이 많습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="eaa57-412">예를 들어 0의 벡터 또는 원래 입력된 벡터 hello 반환할 수 I.</span><span class="sxs-lookup"><span data-stu-id="eaa57-412">I could return a vector of zeroes, or hello original input vector, for example.</span></span>
3. <span data-ttu-id="eaa57-413">검사는 hello 인수 toohello 함수에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-413">Checks are run on hello arguments toohello function.</span></span> <span data-ttu-id="eaa57-414">각각의 경우에서 오류가 감지 되 면 기본값을 반환 되 고 메시지 hello에 의해 생성 되 `warning()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-414">In each case, if an error is detected, a default value is returned and a message is produced by hello `warning()` function.</span></span> <span data-ttu-id="eaa57-415">사용 하 고 `warning()` 대신 `stop()` hello 후자를 정확히 무엇 려 실행 종료 처럼 tooavoid 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-415">I am using `warning()` rather than `stop()` as hello latter will terminate execution, exactly what I am trying tooavoid.</span></span> <span data-ttu-id="eaa57-416">이 코드의 경우 함수 접근 방법으로 작성하면 복잡하고 난해해 보이므로 프로시저 방식으로 작성하였습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="eaa57-417">hello 로그 계산에 래핑됩니다.이 `tryCatch()` 를 예외 갑자기 중지 tooprocessing 발생 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-417">hello log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt tooprocessing.</span></span> <span data-ttu-id="eaa57-418">`tryCatch()`가 없으면 R 함수에 의해 발생한 대부분의 오류는 중지 작업을 수행하는 중지 신호가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="eaa57-419">실험에서이 R 코드를 실행 하 고 hello 살펴보면 hello output.log 파일에 출력을 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-419">Execute this R code in your experiment and have a look at hello printed output in hello output.log file.</span></span> <span data-ttu-id="eaa57-420">그림 13에 표시 된 것 처럼 이제 hello hello 열 4 개 로그의 hello 변형 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-420">You will now see hello transformed values of hello four columns in hello log, as shown in Figure 13.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="eaa57-421">*그림 13. Hello 요약 hello 데이터 프레임의 값을 변환 되지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-421">*Figure 13. Summary of hello transformed values in hello dataframe.*</span></span>

<span data-ttu-id="eaa57-422">변환 된 hello 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-422">We see hello values have been transformed.</span></span> <span data-ttu-id="eaa57-423">이제 우유 생산이 다른 모든 유제품 생산을 훨씬 초과합니다. 현재 로그 눈금으로 보고 있다는 사실을 상기하세요.</span><span class="sxs-lookup"><span data-stu-id="eaa57-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="eaa57-424">이 시점에서 데이터가 정리되며 모델링할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="eaa57-425">Hello 시각화 hello 결과 데이터 집합의 출력에 대 한 요약을 보면 우리의 [R 스크립트 실행] [ execute-r-script] 모듈을 나타납니다 hello 'Month' 열이 '범주' 12 고유 값으로 다시 싶었기와 마찬가지로, .</span><span class="sxs-lookup"><span data-stu-id="eaa57-425">Looking at hello visualization summary for hello Result Dataset output of our [Execute R Script][execute-r-script] module, you will see hello 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="eaa57-426"><a id="timeseries"></a>시계열 개체 및 상관관계 분석</span><span class="sxs-lookup"><span data-stu-id="eaa57-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="eaa57-427">이 섹션에서는 몇 가지 기본 R 시간 시계열 개체를 탐색 하 고 hello 변수 중 일부는 간의 hello 상관 관계를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-427">In this section we will explore a few basic R time series objects and analyze hello correlations between some of hello variables.</span></span> <span data-ttu-id="eaa57-428">목표는 데이터 프레임 hello 쌍으로 된 상관 관계 정보를 포함 하에서 여러 시퀀스 번호 보다 낮은 toooutput는 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-428">Our goal is toooutput a dataframe containing hello pairwise correlation information at several lags.</span></span>

<span data-ttu-id="eaa57-429">이 섹션에 대 한 hello 전체 R 코드는 이전에 다운로드 한 hello zip 파일에입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-429">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="eaa57-430">R의 시계열 개체</span><span class="sxs-lookup"><span data-stu-id="eaa57-430">Time series objects in R</span></span>
<span data-ttu-id="eaa57-431">이미 언급했듯이 시계열은 시간으로 인덱싱된 일련의 데이터 값입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="eaa57-432">R 시간 시계열 개체는 사용 되는 toocreate 고 hello 시간 인덱스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-432">R time series objects are used toocreate and manage hello time index.</span></span> <span data-ttu-id="eaa57-433">여러 가지 이점을 toousing 시간 계열 개체가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-433">There are several advantages toousing time series objects.</span></span> <span data-ttu-id="eaa57-434">시간 series 개체 해소 hello에서 많은 세부 사항을 hello 개체에 캡슐화 하는 hello 시간 시계열 인덱스 값을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-434">Time series objects free you from hello many details of managing hello time series index values that are encapsulated in hello object.</span></span> <span data-ttu-id="eaa57-435">또한 시간 series 개체 메서드 수 있도록 toouse hello 많은 시간 시계열 플롯을 모델링 등 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-435">In addition, time series objects allow you toouse hello many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="eaa57-436">hello POSIXct 시간 시계열 클래스는 일반적으로 사용 및는 비교적 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-436">hello POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="eaa57-437">이 시간 시계열 클래스에서 hello hello epoch, 1970 년 1 월 1 일 시작 시간을 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-437">This time series class measures time from hello start of hello epoch, January 1, 1970.</span></span> <span data-ttu-id="eaa57-438">이 예제에서는 POSIXct 시계열 개체를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="eaa57-439">널리 사용되는 다른 R 시계열 개체 클래스에는 확장 가능한 시계열인 zoo와 xts가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="eaa57-440">시계열 개체 예</span><span class="sxs-lookup"><span data-stu-id="eaa57-440">Time series object example</span></span>
<span data-ttu-id="eaa57-441">예제로 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-441">Let's get started with our example.</span></span> <span data-ttu-id="eaa57-442">**새** [R 스크립트 실행][execute-r-script] 모듈을 실험에 끌어다 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="eaa57-443">Hello 기존 hello 결과 Dataset1 출력 포트에 연결 [R 스크립트 실행] [ execute-r-script] 모듈 toohello Dataset1 입력 포트의 새 hello [R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-443">Connect hello Result Dataset1 output port of hello existing [Execute R Script][execute-r-script] module toohello Dataset1 input port of hello new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="eaa57-444">첫 번째 예제를 보려면 hello 했던 것 처럼 것으로 hello 예제에서 몇 가지 사항 볼 수 있는 것을 통해 진행률만 hello 증분 각 단계에서 R 코드의 줄 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-444">As I did for hello first examples, as we progress through hello example, at some points I will show only hello incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-hello-dataframe"></a><span data-ttu-id="eaa57-445">읽기 hello 데이터 프레임</span><span class="sxs-lookup"><span data-stu-id="eaa57-445">Reading hello dataframe</span></span>
<span data-ttu-id="eaa57-446">첫 번째 단계로, 보겠습니다 데이터 프레임이 읽고 얻을 수 있는 예상 hello 결과 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-446">As a first step, let's read in a dataframe and make sure we get hello expected results.</span></span> <span data-ttu-id="eaa57-447">hello 다음 코드 수행할지 hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-447">hello following code should do hello job.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

<span data-ttu-id="eaa57-448">이제 hello 실험을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-448">Now, run hello experiment.</span></span> <span data-ttu-id="eaa57-449">hello 새 R 스크립트 실행 도형의 hello 로그 그림 14과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-449">hello log of hello new Execute R Script shape should look like Figure 14.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

<span data-ttu-id="eaa57-450">*(그림 14). Hello R 스크립트 실행 모듈의 hello 데이터 프레임의 요약입니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-450">*Figure 14. Summary of hello dataframe in hello Execute R Script module.*</span></span>

<span data-ttu-id="eaa57-451">이 데이터를 예상 하는 hello 형식 및 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-451">This data is of hello expected types and format.</span></span> <span data-ttu-id="eaa57-452">Note hello 'Month' 열은 형식 인수 및 hello 수준 수를 예상 했습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-452">Note that hello 'Month' column is of type factor and has hello expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="eaa57-453">시계열 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="eaa57-453">Creating a time series object</span></span>
<span data-ttu-id="eaa57-454">Tooadd 시간 시계열 개체 tooour 데이터 프레임이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-454">We need tooadd a time series object tooour dataframe.</span></span> <span data-ttu-id="eaa57-455">POSIXct 클래스의 새 열을 추가 하는 hello 다음 hello 현재 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-455">Replace hello current code with hello following, which adds a new column of class POSIXct.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

<span data-ttu-id="eaa57-456">이제 hello 로그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-456">Now, check hello log.</span></span> <span data-ttu-id="eaa57-457">그림 15와 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-457">It should look like Figure 15.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="eaa57-458">*그림 15. 요약 시간 시계열 개체와 데이터 hello 프레임입니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-458">*Figure 15. Summary of hello dataframe with a time series object.*</span></span>

<span data-ttu-id="eaa57-459">해당 hello 새 열이 실제로 클래스 POSIXct hello 요약에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-459">We can see from hello summary that hello new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-hello-data"></a><span data-ttu-id="eaa57-460">탐색 하 고 hello 데이터 변환</span><span class="sxs-lookup"><span data-stu-id="eaa57-460">Exploring and transforming hello data</span></span>
<span data-ttu-id="eaa57-461">이 데이터 집합에 hello 변수 중 일부를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-461">Let's explore some of hello variables in this dataset.</span></span> <span data-ttu-id="eaa57-462">Scatterplot 행렬은 좋은 방법 tooproduce를 빠르게 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-462">A scatterplot matrix is a good way tooproduce a quick look.</span></span> <span data-ttu-id="eaa57-463">Hello 교체 중인 I `str()` hello 다음 줄으로 hello 이전 R 코드의 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-463">I am replacing hello `str()` function in hello previous R code with hello following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="eaa57-464">이 코드를 실행하고 결과를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="eaa57-464">Run this code and see what happens.</span></span> <span data-ttu-id="eaa57-465">R 장치 포트 hello에 생성 된 hello 점도 그림 16과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-465">hello plot produced at hello R Device port should look like Figure 16.</span></span>

![선택한 변수의 산점도 행렬][17]

<span data-ttu-id="eaa57-467">*그림 16. 선택한 변수의 산점도 행렬*</span><span class="sxs-lookup"><span data-stu-id="eaa57-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="eaa57-468">이러한 변수 간의 hello 관계에 있는 일부 odd-looking 구조는.</span><span class="sxs-lookup"><span data-stu-id="eaa57-468">There is some odd-looking structure in hello relationships between these variables.</span></span> <span data-ttu-id="eaa57-469">아마도이 म 하지 표준화 hello 변수 hello 팩트 및 추세 hello 데이터에서에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-469">Perhaps this arises from trends in hello data and from hello fact that we have not standardized hello variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="eaa57-470">상관관계 분석</span><span class="sxs-lookup"><span data-stu-id="eaa57-470">Correlation analysis</span></span>
<span data-ttu-id="eaa57-471">tooboth 필요 tooperform 상관 관계 분석 추세를 취소 하 고 hello 변수 표준화 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-471">tooperform correlation analysis we need tooboth de-trend and standardize hello variables.</span></span> <span data-ttu-id="eaa57-472">단순히 사용 하 여 hello R `scale()` 모두 센터 및 변수 크기를 조정 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-472">We could simply use hello R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="eaa57-473">이 함수가 더 빨리 실행될 수 있지만</span><span class="sxs-lookup"><span data-stu-id="eaa57-473">This function might well run faster.</span></span> <span data-ttu-id="eaa57-474">그러나 tooshow 원하는 하면 R에서 방어 프로그래밍의 예</span><span class="sxs-lookup"><span data-stu-id="eaa57-474">However, I want tooshow you an example of defensive programing in R.</span></span>

<span data-ttu-id="eaa57-475">hello `ts.detrend()` 아래 표시 된 함수는 이러한 작업을 모두 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-475">hello `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="eaa57-476">hello 다음 두 줄의 코드 hello 데이터 추세를 취소 하 고 hello 값을 표준화 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-476">hello following two lines of code de-trend hello data and then standardize hello values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="eaa57-477">Hello에는 비트 상황이 발생 하지는 `ts.detrend()` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-477">There is quite a bit happening in hello `ts.detrend()` function.</span></span> <span data-ttu-id="eaa57-478">이 코드의 대부분을 hello 인수도 잠재적인 문제에 대 한 확인 되었거나 여전히 hello 계산 하는 동안 발생할 수 있는 예외를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-478">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="eaa57-479">이 코드의 몇 줄만 실제로 계산 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-479">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="eaa57-480">방어적 프로그램의 예는 [값 변환](#valuetransformations)에서 이미 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="eaa57-481">두 계산 블록이 모두 `tryCatch()`로 래핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="eaa57-482">일부 오류는 감지 tooreturn hello 원래 입력된 벡터 및 다른 경우에 0으로 벡터를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-482">For some errors it makes sense tooreturn hello original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="eaa57-483">Hello 취소 추세 분석에 사용 되는 선형 회귀는 문제는 시간 시계열입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-483">Note that hello linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="eaa57-484">hello 예측자 변수 시간 시계열 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-484">hello predictor variable is a time series object.</span></span>  

<span data-ttu-id="eaa57-485">한 번 `ts.detrend()` 정의 우리의 데이터 프레임에 대 한 관심의 toohello 변수에 적용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-485">Once `ts.detrend()` is defined we apply it toohello variables of interest in our dataframe.</span></span> <span data-ttu-id="eaa57-486">Hello 결과 목록에서 만든 강제 변환 해야 우리 `lapply()` 를 사용 하 여 데이터 프레임 toodata `as.data.frame()`합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-486">We must coerce hello resulting list created by `lapply()` toodata dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="eaa57-487">방어 측면으로 인해 `ts.detrend()`, 오류 tooprocess hello 변수 중 하나가 되더라도 해결 hello 처리 다른 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-487">Because of defensive aspects of `ts.detrend()`, failure tooprocess one of hello variables will not prevent correct processing of hello others.</span></span>  

<span data-ttu-id="eaa57-488">코드의 마지막 줄 hello pairwise scatterplot를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-488">hello final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="eaa57-489">Hello R 코드를 실행 한 후 hello scatterplot의 hello 결과 17 그림에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-489">After running hello R code, hello results of hello scatterplot are shown in Figure 17.</span></span>

![비추세화되고 표준화된 시계열의 쌍별 산점도][18]

<span data-ttu-id="eaa57-491">*그림 17. 비추세화되고 표준화된 시계열의 쌍별 산점도*</span><span class="sxs-lookup"><span data-stu-id="eaa57-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="eaa57-492">이러한 결과 toothose 그림 16을 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-492">You can compare these results toothose shown in Figure 16.</span></span> <span data-ttu-id="eaa57-493">Hello로 추세 제거 하 고 표준화 변수 hello는 훨씬 덜 구조 이러한 변수 간의 hello 관계를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-493">With hello trend removed and hello variables standardized, we see a lot less structure in hello relationships between these variables.</span></span>

<span data-ttu-id="eaa57-494">hello 코드 toocompute hello 상관 관계 R ccf 개체로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-494">hello code toocompute hello correlations as R ccf objects is as follows.</span></span>

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="eaa57-495">그림 18 같이 hello 로그를 생성이 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-495">Running this code produces hello log shown in Figure 18.</span></span>

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

<span data-ttu-id="eaa57-496">*그림 18. Ccf 목록이 hello 쌍으로 된 상관 관계 분석에서 개체입니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-496">*Figure 18. List of ccf objects from hello pairwise correlation analysis.*</span></span>

<span data-ttu-id="eaa57-497">각 지연에 대해 상관관계 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="eaa57-498">이러한 상관 관계 값은 중요 한 충분히 큰 toobe입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-498">None of these correlation values is large enough toobe significant.</span></span> <span data-ttu-id="eaa57-499">따라서 각 변수를 독립적으로 모델링할 수 있다는 결론을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="eaa57-500">데이터 프레임 출력</span><span class="sxs-lookup"><span data-stu-id="eaa57-500">Output a dataframe</span></span>
<span data-ttu-id="eaa57-501">R ccf 개체 목록으로 hello 쌍으로 된 상관 관계 계산가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-501">We have computed hello pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="eaa57-502">이 hello 출력 포트 결과 데이터 집합의 데이터 프레임이 실제로 필요에 따라 약간의 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-502">This presents a bit of a problem as hello Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="eaa57-503">또한 hello ccf 개체는 자체 및 원하는 hello 값만 hello hello에 hello 상관 관계가 목록의 첫 번째 요소에 다양 한 시퀀스 번호 보다 낮은 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-503">Further, hello ccf object is itself a list and we want only hello values in hello first element of this list, hello correlations at hello various lags.</span></span>

<span data-ttu-id="eaa57-504">다음 코드 추출 hello 지연 값 목록을 사용 하는 ccf 개체의 hello 목록에서 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-504">hello following code extracts hello lag values from hello list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="eaa57-505">hello 첫 번째 코드 줄에는 약간 까다로울 이며 것을 이해 하는 데 일부 설명은 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-505">hello first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="eaa57-506">Hello 다음 했습니까 hello 빌드된 프로젝트에서 작업 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-506">Working from hello inside out we have hello following:</span></span>

1. <span data-ttu-id="eaa57-507">hello '**[[**'hello 인수와 함께 연산자'**1**'가 선택 되어 hello hello hello ccf 개체 목록의 첫 번째 요소에서 시퀀스 번호 보다 낮은 hello에 대 한 상관 관계의 벡터입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-507">hello '**[[**' operator with hello argument '**1**' selects hello vector of correlations at hello lags from hello first element of hello ccf object list.</span></span>
2. <span data-ttu-id="eaa57-508">hello `do.call()` 함수 hello 적용 `rbind()` hello 목록의 hello 요소를 마우스로 함수 반환 `lapply()`합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-508">hello `do.call()` function applies hello `rbind()` function over hello elements of hello list returns by `lapply()`.</span></span>
3. <span data-ttu-id="eaa57-509">hello `data.frame()` 함수에서 생성 하는 hello 결과 강제 변환 `do.call()` tooa 데이터 프레임입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-509">hello `data.frame()` function coerces hello result produced by `do.call()` tooa dataframe.</span></span>

<span data-ttu-id="eaa57-510">Hello 행 이름이 hello 데이터 프레임의 열에 있는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-510">Note that hello row names are in a column of hello dataframe.</span></span> <span data-ttu-id="eaa57-511">Hello에서 출력 될 때 hello 행 이름을 유지 이렇게 [R 스크립트 실행][execute-r-script]합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-511">Doing so preserves hello row names when they are output from hello [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="eaa57-512">그림 19 hello 출력 하는 hello 코드 실행을 생성 할 때 I **시각화** hello hello 결과 데이터 집합 포트에 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-512">Running hello code produces hello output shown in Figure 19 when I **Visualize** hello output at hello Result Dataset port.</span></span> <span data-ttu-id="eaa57-513">hello 행 이름은 의도 한 대로 hello 첫 번째 열에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-513">hello row names are in hello first column, as intended.</span></span>

![Hello 상관 관계 분석에서 출력 결과][20]

<span data-ttu-id="eaa57-515">*그림 19. Hello 상관 관계 분석에서 출력 된 결과입니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-515">*Figure 19. Results output from hello correlation analysis.*</span></span>

## <span data-ttu-id="eaa57-516"><a id="seasonalforecasting"></a>시계열 예: 계절별 예측</span><span class="sxs-lookup"><span data-stu-id="eaa57-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="eaa57-517">데이터 형식이 이제 분석에 적합 한 형식 및 hello 변수 간의 상관 없는 중요 한 관계는 있음을 확인 했습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between hello variables.</span></span> <span data-ttu-id="eaa57-518">이제 시계열 예측 모델을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="eaa57-519">이 모델을 사용 하 여 우리 예측 캘리포니아 우유 프로덕션 hello에 대 한 12 개월의 2013.</span><span class="sxs-lookup"><span data-stu-id="eaa57-519">Using this model we will forecast California milk production for hello 12 months of 2013.</span></span>

<span data-ttu-id="eaa57-520">예측 모델에는 두 가지 구성 요소, 즉 추세 구성 요소와 계절 구성 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="eaa57-521">hello 전체 예측은 hello 곱일이 두 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-521">hello complete forecast is hello product of these two components.</span></span> <span data-ttu-id="eaa57-522">이런 형식의 모델을 승법 모형이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="eaa57-523">hello는 대체 항목은 가산적 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-523">hello alternative is an additive model.</span></span> <span data-ttu-id="eaa57-524">이미 tractable이 분석을 낮추는 관심 있는 로그 변환 toohello 변수 적용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-524">We have already applied a log transformation toohello variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="eaa57-525">이 섹션에 대 한 hello 전체 R 코드는 이전에 다운로드 한 hello zip 파일에입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-525">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="creating-hello-dataframe-for-analysis"></a><span data-ttu-id="eaa57-526">Hello 데이터 프레임 분석을 위해 만들기</span><span class="sxs-lookup"><span data-stu-id="eaa57-526">Creating hello dataframe for analysis</span></span>
<span data-ttu-id="eaa57-527">추가 하 여 시작 된 **새** [R 스크립트 실행] [ execute-r-script] 모듈 tooyour 실험 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-527">Start by adding a **new** [Execute R Script][execute-r-script] module tooyour experiment.</span></span> <span data-ttu-id="eaa57-528">Hello 연결 **결과 데이터 집합** hello 기존 출력 [R 스크립트 실행] [ execute-r-script] 모듈 toohello **Dataset1** hello 새 모듈의 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-528">Connect hello **Result Dataset** output of hello existing [Execute R Script][execute-r-script] module toohello **Dataset1** input of hello new module.</span></span> <span data-ttu-id="eaa57-529">hello 결과 그림 20과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-529">hello result should look something like Figure 20.</span></span>

![hello 추가 hello 새 R 스크립트 실행 모듈을 시험해][21]

<span data-ttu-id="eaa57-531">*그림 20입니다. hello는 hello 새 R 스크립트 실행 모듈 추가 사용해 보십시오.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-531">*Figure 20. hello experiment with hello new Execute R Script module added.*</span></span>

<span data-ttu-id="eaa57-532">으로 hello 상관 관계 분석에서는 방금 완료 해야 tooadd POSIXct 시간 시계열 개체를 지정 된 열입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-532">As with hello correlation analysis we just completed, we need tooadd a column with a POSIXct time series object.</span></span> <span data-ttu-id="eaa57-533">hello 코드 다음에이 위해 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-533">hello following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="eaa57-534">이 코드를 실행 하 고 hello 로그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-534">Run this code and look at hello log.</span></span> <span data-ttu-id="eaa57-535">hello 결과 그림 21 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-535">hello result should look like Figure 21.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="eaa57-536">*그림 21. Hello 데이터 프레임의 요약입니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-536">*Figure 21. A summary of hello dataframe.*</span></span>

<span data-ttu-id="eaa57-537">이 결과와 toostart 준비 하는 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-537">With this result, we are ready toostart our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="eaa57-538">학습 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="eaa57-538">Create a training dataset</span></span>
<span data-ttu-id="eaa57-539">생성 된 hello 데이터 프레임으로 학습 데이터 집합 toocreate가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-539">With hello dataframe constructed we need toocreate a training dataset.</span></span> <span data-ttu-id="eaa57-540">이 데이터 모두 포함 되며 2013 hello 연도의 마지막 12 hello 점을 제외 하 고 hello 관찰의 변수인 우리의 테스트 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-540">This data will include all of hello observations except hello last 12, of hello year 2013, which is our test dataset.</span></span> <span data-ttu-id="eaa57-541">hello 다음 하위 집합 hello 데이터 프레임을 코드로 바꾸고 hello dairy 프로덕션 및 price 변수 플롯을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-541">hello following code subsets hello dataframe and creates plots of hello dairy production and price variables.</span></span> <span data-ttu-id="eaa57-542">Hello 차트가 프로덕션 및 price 변수 4 개 다음 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-542">I then create plots of hello four production and price variables.</span></span> <span data-ttu-id="eaa57-543">익명 함수 사용 되는 toodefine 점도 대 한 일부 보완 이며 hello hello 목록이 반복 다른 두 개의 인수를 `Map()`합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-543">An anonymous function is used toodefine some augments for plot, and then iterate over hello list of hello other two arguments with `Map()`.</span></span> <span data-ttu-id="eaa57-544">여기서는 For 루프가 잘 작동했겠지만</span><span class="sxs-lookup"><span data-stu-id="eaa57-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="eaa57-545">R은 함수 언어이므로 함수를 사용한 접근 방식을 보여 주고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="eaa57-546">그림 22와 hello R 장치 출력에서 일련의 시계열을 그리는 hello를 생성 hello 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-546">Running hello code produces hello series of time series plots from hello R Device output shown in Figure 22.</span></span> <span data-ttu-id="eaa57-547">날짜, 계열을 그릴 메서드 hello 시간의 훌륭한 장점 단위는 해당 hello 시간 축 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-547">Note that hello time axis is in units of dates, a nice benefit of hello time series plot method.</span></span>

![캘리포니아 유제품 생산 및 가격 데이터의 첫 번째 시계열 도표](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![캘리포니아 유제품 생산 및 가격 데이터의 두 번째 시계열 도표](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![캘리포니아 유제품 생산 및 가격 데이터의 세 번째 시계열 도표](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![캘리포니아 유제품 생산 및 가격 데이터의 네 번째 시계열 도표](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="eaa57-552">*그림 22. 캘리포니아 유제품 생산 및 가격 데이터의 시계열 도표*</span><span class="sxs-lookup"><span data-stu-id="eaa57-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="eaa57-553">추세 모델</span><span class="sxs-lookup"><span data-stu-id="eaa57-553">A trend model</span></span>
<span data-ttu-id="eaa57-554">시간 series 개체 및 hello 데이터에 살펴보고 필요를 만들었으면 tooconstruct hello 캘리포니아 우유 프로덕션 데이터에 대 한 추세 모델을 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-554">Having created a time series object and having had a look at hello data, let's start tooconstruct a trend model for hello California milk production data.</span></span> <span data-ttu-id="eaa57-555">시계열 회귀로 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-555">We can do this with a time series regression.</span></span> <span data-ttu-id="eaa57-556">그러나 되기 hello 그림에서는 모델링 해 볼 필요는 기울기가 고 절편 tooaccurately 이상 hello hello 학습 데이터의 추세를 관찰 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-556">However, it is clear from hello plot that we will need more than a slope and intercept tooaccurately model hello observed trend in hello training data.</span></span>

<span data-ttu-id="eaa57-557">Hello hello 데이터의 작은 규모를 매개 변수로 받아 I 됩니다 RStudio에 추세에 대 한 hello 모델을 작성 하 고 잘라내기 및 붙여넣기 hello 결과 모델 Azure 기계 학습에 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-557">Given hello small scale of hello data, I will build hello model for trend in RStudio and then cut and paste hello resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="eaa57-558">RStudio는 이러한 유형의 대화형 분석에 대화형 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="eaa57-559">첫 번째 시도 같이 I too3 힘을 다항식 회귀를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-559">As a first attempt, I will try a polynomial regression with powers up too3.</span></span> <span data-ttu-id="eaa57-560">이러한 종류의 모형을 과적합하게 하는 것은 매우 위험합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="eaa57-561">따라서 것이 가장 좋은 tooavoid 상위 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-561">Therefore, it is best tooavoid high order terms.</span></span> <span data-ttu-id="eaa57-562">hello `I()` hello 내용의 해석을 제한 하는 함수 ('있는 그대로' hello 내용을 해석) 하 고 회귀 수식에 toowrite 문자 그대로 해석 된 함수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-562">hello `I()` function inhibits interpretation of hello contents (interprets hello contents 'as is') and allows you toowrite a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="eaa57-563">Hello 다음을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-563">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

<span data-ttu-id="eaa57-564">P 값에서 (Pr (> | t |))는 hello 알 수 있습니다이 출력 제곱된 용어 상당한 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-564">From P values (Pr(>|t|)) in this output, we can see that hello squared term may not be significant.</span></span> <span data-ttu-id="eaa57-565">Hello를 사용 합니다 `update()` 삭제 hello 하 여이 모델 용어 제곱 toomodify 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-565">I will use hello `update()` function toomodify this model by dropping hello squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="eaa57-566">Hello 다음을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-566">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

<span data-ttu-id="eaa57-567">보기가 더 낫습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-567">This looks better.</span></span> <span data-ttu-id="eaa57-568">Hello 단어를 모두 의미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-568">All of hello terms are significant.</span></span> <span data-ttu-id="eaa57-569">그러나 hello 2e 16 값 기본 값 이며 너무 심각 하 게 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-569">However, hello 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="eaa57-570">온전성 테스트로 표시 된 hello 추세 곡선이 있는 hello 캘리포니아 dairy 프로덕션 데이터의 시간 시계열 그림을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-570">As a sanity test, let's make a time series plot of hello California dairy production data with hello trend curve shown.</span></span> <span data-ttu-id="eaa57-571">Hello 코드 hello Azure 기계 학습에서에서 다음을 추가 했지만 [R 스크립트 실행] [ execute-r-script] 모델 (하지 RStudio) toocreate 모델 hello 및 플롯을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-571">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) toocreate hello model and make a plot.</span></span> <span data-ttu-id="eaa57-572">그림 23에서 hello 결과가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-572">hello result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![추세 모델을 표시한 캘리포니아 우유 생산 데이터](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="eaa57-574">*그림 23. 추세 모델을 표시한 캘리포니아 우유 생산 데이터*</span><span class="sxs-lookup"><span data-stu-id="eaa57-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="eaa57-575">Hello 추세 모델 hello 데이터를 상당히 잘 맞는 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-575">It looks like hello trend model fits hello data fairly well.</span></span> <span data-ttu-id="eaa57-576">또한 찾을 과잉 맞춤이의 toobe 증거 하나는 홀수 hello 모델 곡선의 선분 흔듭니다 등입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-576">Further, there does not seem toobe evidence of over-fitting, such as odd wiggles in hello model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="eaa57-577">계절 모델</span><span class="sxs-lookup"><span data-stu-id="eaa57-577">Seasonal model</span></span>
<span data-ttu-id="eaa57-578">손 모양에 추세 모델에서는 toopush에 및 필요 hello 계절 관련 영향을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-578">With a trend model in hand, we need toopush on and include hello seasonal effects.</span></span> <span data-ttu-id="eaa57-579">Hello 연도의 달 hello hello 선형 모델 toocapture hello-월별 효과 더미 변수로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-579">We will use hello month of hello year as a dummy variable in hello linear model toocapture hello month-by-month effect.</span></span> <span data-ttu-id="eaa57-580">모델로 인수 변수를 사용할 때 hello 절편 하지 계산 해야 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-580">Note that when you introduce factor variables into a model, hello intercept must not be computed.</span></span> <span data-ttu-id="eaa57-581">이렇게 하지 않으면 hello 공식은 과다 하 게 지정 하 고 R 짧아집니다 면 hello 중 원하는 요인 있지만 hello 절편 용어 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-581">If you do not do this, hello formula is over-specified and R will drop one of hello desired factors but keep hello intercept term.</span></span>

<span data-ttu-id="eaa57-582">Hello 사용할 수 있으므로 만족 스러운 추세 모델 `update()` 함수 tooadd hello 새 조건 toohello 기존 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-582">Since we have a satisfactory trend model we can use hello `update()` function tooadd hello new terms toohello existing model.</span></span> <span data-ttu-id="eaa57-583">hello 업데이트 수식에서-1 hello hello 절편 용어를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-583">hello -1 in hello update formula drops hello intercept term.</span></span> <span data-ttu-id="eaa57-584">Hello 잠시 동안 RStudio를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-584">Continuing in RStudio for hello moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="eaa57-585">Hello 다음을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-585">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

<span data-ttu-id="eaa57-586">해당 hello 모델이 더 이상 절편 용어 고 12 월 중요 한 요소에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-586">We see that hello model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="eaa57-587">이것은 의도 했던 toosee 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-587">This is exactly what we wanted toosee.</span></span>

<span data-ttu-id="eaa57-588">Hello 계절별 모델 얼마나 잘 작동 하는 hello 캘리포니아 dairy 프로덕션 데이터 toosee의 다른 시간 시계열 그림을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-588">Let's make another time series plot of hello California dairy production data toosee how well hello seasonal model is working.</span></span> <span data-ttu-id="eaa57-589">Hello 코드 hello Azure 기계 학습에서에서 다음을 추가 했지만 [R 스크립트 실행] [ execute-r-script] toocreate 모델 hello 및 플롯을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-589">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] toocreate hello model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="eaa57-590">그림 24 같이 hello 그림을 생성 Azure 기계 학습에서이 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-590">Running this code in Azure Machine Learning produces hello plot shown in Figure 24.</span></span>

![계절의 영향이 포함된 캘리포니아 우유 생산 모델](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="eaa57-592">*그림 24. 계절의 영향이 포함된 캘리포니아 우유 생산 모델*</span><span class="sxs-lookup"><span data-stu-id="eaa57-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="eaa57-593">hello 적합된 한 toohello 데이터 그림 24에 표시 된 것은 아니라 높이면 서입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-593">hello fit toohello data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="eaa57-594">Hello 추세와 hello 계절 관련 영향 (월별 변형)을 모두 적절 한 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-594">Both hello trend and hello seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="eaa57-595">이 모델에 다른 검사 방법으로 hello 잉여를 살펴보면 죠.</span><span class="sxs-lookup"><span data-stu-id="eaa57-595">As another check on our model, let's have a look at hello residuals.</span></span> <span data-ttu-id="eaa57-596">hello 다음 코드에서는 두 당사의 모델에서 예측된 값 hello, 계산 hello 계절 관련 모델에 대 한 hello 잉여 하 고 표시 hello 학습 데이터에 대 한 이러한 잉여 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-596">hello following code computes hello predicted values from our two models, computes hello residuals for hello seasonal model, and then plots these residuals for hello training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="eaa57-597">그림 25에서 hello 잔여 그림 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-597">hello residual plot is shown in Figure 25.</span></span>

![잉여 hello 학습 데이터에 대 한 hello 계절 관련 모델의](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="eaa57-599">*그림 25. Hello 학습 데이터에 대 한 hello 계절 관련 모델의 나머지를 제공 합니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-599">*Figure 25. Residuals of hello seasonal model for hello training data.*</span></span>

<span data-ttu-id="eaa57-600">이 정도의 오차는 적절해 보입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-600">These residuals look reasonable.</span></span> <span data-ttu-id="eaa57-601">이 모델에 대 한 고려 되지 않습니다는 hello 2008 2009 경기의 hello 효과 제외 하 고 특정 없는 구조는 특히 잘 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-601">There is no particular structure, except hello effect of hello 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="eaa57-602">그림 25 같이 hello 점도 hello 잉여에 시간 종속적 패턴을 감지 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-602">hello plot shown in Figure 25 is useful for detecting any time-dependent patterns in hello residuals.</span></span> <span data-ttu-id="eaa57-603">안녕하세요 명시적 방법을 컴퓨팅 나머지 하 고 그리는 hello 사용의 hello 그림에서 시간 순서에 hello 잉여를 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-603">hello explicit approach of computing and plotting hello residuals I used places hello residuals in time order on hello plot.</span></span> <span data-ttu-id="eaa57-604">경우 hello에 다른 손 I에 점으로 표시 `milk.lm$residuals`, 시간 순서로 hello 점도 않았을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-604">If, on hello other hand, I had plotted `milk.lm$residuals`, hello plot would not have been in time order.</span></span>

<span data-ttu-id="eaa57-605">사용할 수도 있습니다 `plot.lm()` tooproduce 일련의 진단 점도 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-605">You can also use `plot.lm()` tooproduce a series of diagnostic plots.</span></span>

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="eaa57-606">이 코드는 그림 26에서 보여 주는 일련의 진단 도표를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![Hello 계절 관련 모델에 대 한 진단 점도 중 첫 번째](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Hello 계절 관련 모델에 대 한 진단 점도 중 두 번째](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Hello 계절 관련 모델에 대 한 진단 점도의 3](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Hello 계절 관련 모델에 대 한 진단 점도 중 네 번째](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="eaa57-611">*그림 26. Hello 계절 관련 모델에 대 한 진단 표시합니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-611">*Figure 26. Diagnostic plots for hello seasonal model.*</span></span>

<span data-ttu-id="eaa57-612">이러한 점도 이지만에서 식별 된 몇 가지 높은 영향력 지점이 toocause 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-612">There are a few highly influential points identified in these plots, but nothing toocause great concern.</span></span> <span data-ttu-id="eaa57-613">또한 확인할 수 있습니다 hello 보통 Q Q 그림에서는 hello 잉여 닫기 toonormally 배포 된 경우 선형 모델에 대 한 중요 한 가정을 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-613">Further, we can see from hello Normal Q-Q plot that hello residuals are close toonormally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="eaa57-614">예측 및 모델 평가</span><span class="sxs-lookup"><span data-stu-id="eaa57-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="eaa57-615">예에서 사용 하는 한 더 많은 작업 toodo toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-615">There is just one more thing toodo toocomplete our example.</span></span> <span data-ttu-id="eaa57-616">Hello 오류 hello 실제 데이터를 비교 하 여 측정 및 toocompute 예측 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-616">We need toocompute forecasts and measure hello error against hello actual data.</span></span> <span data-ttu-id="eaa57-617">이 예측 hello에 대 한 12 개월의 2013 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-617">Our forecast will be for hello 12 months of 2013.</span></span> <span data-ttu-id="eaa57-618">우리는 학습 데이터 집합에 속하지 않는이 예측된 toohello 실제 데이터에 대 한 측정 하는 오류를 계산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-618">We can compute an error measure for this forecast toohello actual data that is not part of our training dataset.</span></span> <span data-ttu-id="eaa57-619">또한 비교할 수 있습니다 성능 hello에 학습 데이터 toohello 18 세 테스트 데이터의 12 개월입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-619">Additionally, we can compare performance on hello 18 years of training data toohello 12 months of test data.</span></span>  

<span data-ttu-id="eaa57-620">사용 된 메트릭 개수가 시계열 모델의 toomeasure hello 성능.</span><span class="sxs-lookup"><span data-stu-id="eaa57-620">A number of metrics are used toomeasure hello performance of time series models.</span></span> <span data-ttu-id="eaa57-621">경우에 hello 제곱 평균 (RMS) 오류를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-621">In our case we will use hello root mean square (RMS) error.</span></span> <span data-ttu-id="eaa57-622">hello 다음 함수를 계산합니다. 두 계열 간의 hello RMS 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-622">hello following function computes hello RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="eaa57-623">Hello와 마찬가지로 `log.transform()` 함수에서 설명한 섹션 "변환 값" hello,이 함수에서 오류 검사 및 예외 복구 코드의 많습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-623">As with hello `log.transform()` function we discussed in hello "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="eaa57-624">hello 원칙은 데 사용 된 동일한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-624">hello principles employed are hello same.</span></span> <span data-ttu-id="eaa57-625">hello 작업에 래핑된 두 위치에서 `tryCatch()`합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-625">hello work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="eaa57-626">첫째, 시계열 hello 되므로 exponentiated, hello 값의 hello 로그 노력입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-626">First, hello time series are exponentiated, since we have been working with hello logs of hello values.</span></span> <span data-ttu-id="eaa57-627">둘째, hello 실제 RMS 오류 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-627">Second, hello actual RMS error is computed.</span></span>  

<span data-ttu-id="eaa57-628">함수 toomeasure hello RMS 오류로 equipped, 보겠습니다 빌드하고 hello RMS 오류를 포함 하는 데이터 프레임을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-628">Equipped with a function toomeasure hello RMS error, let's build and output a dataframe containing hello RMS errors.</span></span> <span data-ttu-id="eaa57-629">단독 hello 추세 모델에 대 한 사용 약관 계절 관련 요소로 hello 전체 모델 기능이 포함 될 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-629">We will include terms for hello trend model alone and hello complete model with seasonal factors.</span></span> <span data-ttu-id="eaa57-630">hello 다음 코드는 hello 작업에서는 생성 한 hello 두 선형 모델을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-630">hello following code does hello job by using hello two linear models we have constructed.</span></span>

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="eaa57-631">그림 27 hello 결과 데이터 집합 출력 포트에 표시 된 hello 출력을 생성이 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-631">Running this code produces hello output shown in Figure 27 at hello Result Dataset output port.</span></span>

![RMS에 대 한 오류 hello 모델 비교][26]

<span data-ttu-id="eaa57-633">*그림 27. Hello 모델에 대 한 RMS 오류 비교 합니다.*</span><span class="sxs-lookup"><span data-stu-id="eaa57-633">*Figure 27. Comparison of RMS errors for hello models.*</span></span>

<span data-ttu-id="eaa57-634">이 결과에서 추가 hello 계절 관련 요인 toohello 모델 줄어든다는 hello RMS 오류 크게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-634">From these results, we see that adding hello seasonal factors toohello model reduces hello RMS error significantly.</span></span> <span data-ttu-id="eaa57-635">너무 레지스터 hello 학습 데이터에 대 한 RMS hello 오류는 다소 보다 작은 hello에 대 한 예측 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-635">Not too surprisingly, hello RMS error for hello training data is a bit less than for hello forecast.</span></span>

## <span data-ttu-id="eaa57-636"><a id="appendixa"></a>부록 a: 가이드 tooRStudio</span><span class="sxs-lookup"><span data-stu-id="eaa57-636"><a id="appendixa"></a>APPENDIX A: Guide tooRStudio</span></span>
<span data-ttu-id="eaa57-637">이 부록에 제공 합니다 일부 링크 toohello hello RStudio 설명서 tooget 시작한의 주요 섹션 RStudio 매우 잘 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-637">RStudio is quite well documented, so in this appendix I will provide some links toohello key sections of hello RStudio documentation tooget you started.</span></span>

1. <span data-ttu-id="eaa57-638">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="eaa57-638">Creating projects</span></span>
   
   <span data-ttu-id="eaa57-639">R RStudio를 사용하여 R 코드를 프로젝트에서 구성하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="eaa57-640">프로젝트를 사용 하 여 hello 설명서 https://support.rstudio.com/hc/articles/200526207-Using-Projects에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-640">hello documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="eaa57-641">다음이 단계를 수행 하 고이 문서에서 hello R 코드 예제에 대 한 프로젝트를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-641">I recommend that you follow these directions and create a project for hello R code examples in this document.</span></span>  
2. <span data-ttu-id="eaa57-642">R 코드 편집 및 실행</span><span class="sxs-lookup"><span data-stu-id="eaa57-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="eaa57-643">RStudio는 R 코드의 편집 및 실행을 위해 통합 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="eaa57-644">설명서는 https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code(영문)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="eaa57-645">디버그</span><span class="sxs-lookup"><span data-stu-id="eaa57-645">Debugging</span></span>
   
   <span data-ttu-id="eaa57-646">RStudio에는 강력한 디버그 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="eaa57-647">이러한 기능에 대한 설명서는 https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio(영문)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="eaa57-648">hello 중단점 문제 해결 기능 https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-648">hello breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="eaa57-649"><a id="appendixb"></a>부록 B - 추가 정보</span><span class="sxs-lookup"><span data-stu-id="eaa57-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="eaa57-650">프로그래밍의 자습서에서는 hello 기초가이 R 항목에 대 할 toouse hello Azure 기계 학습 스튜디오를 사용 하는 R 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-650">This R programming tutorial covers hello basics of what you need toouse hello R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="eaa57-651">R에 익숙하지 않은 경우 CRAN에서 두 가지 소개 자료를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="eaa57-652">Emmanuel Paradis 여 초보자를 위한 R http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf에 좋은 위치 toostart입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-652">R for Beginners by Emmanuel Paradis is a good place toostart at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="eaa57-653">소개 tooR 여 W. n입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-653">An Introduction tooR by W. N.</span></span> <span data-ttu-id="eaa57-654">Venables et.</span><span class="sxs-lookup"><span data-stu-id="eaa57-654">Venables et.</span></span> <span data-ttu-id="eaa57-655">al.</span><span class="sxs-lookup"><span data-stu-id="eaa57-655">al.</span></span> <span data-ttu-id="eaa57-656">이 쓴 'An Introduction to R(R에 대한 소개)'에서 더 심도있게 다루고 있으며 http://cran.r-project.org/doc/manuals/R-intro.html(영문)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="eaa57-657">R을 시작하는 데 도움을 되는 서적이 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="eaa57-658">몇 가지 유용한 서적은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="eaa57-659">아트의 R 프로그래밍 hello: A 둘러보기의 통계 소프트웨어 디자인 Norman Matloff 여은 R에서는 뛰어난 소개 tooprogramming</span><span class="sxs-lookup"><span data-stu-id="eaa57-659">hello Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction tooprogramming in R.</span></span>  
* <span data-ttu-id="eaa57-660">Paul Teetor 하 여 R Cookbook 오른쪽은 문제 및 솔루션 접근 방식 toousing를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-660">R Cookbook by Paul Teetor provides a problem and solution approach toousing R.</span></span>  
* <span data-ttu-id="eaa57-661">'R in Action'(저자: Robert Kabacoff)(영문)도 유용한 입문서입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="eaa57-662">hello 도우미 빠른 R 웹 사이트는 http://www.statmethods.net/에 유용한 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-662">hello companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="eaa57-663">Patrick Burns 하 여 R 르노는 오른쪽 hello 책에서 프로그래밍할 때 발생할 수 있는 작업은 복잡할 및 어려운 항목의 수를 처리 하는 매우 유머 책 http://www.burns-stat.com/documents/books/the-r-inferno/에서 무료로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. hello book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="eaa57-664">R에서 고급 항목에 심층 분석 하려는 경우 살펴본 hello 책 Hadley Wickham 하 여 고급 R 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-664">If you want a deep dive into advanced topics in R, have a look at hello book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="eaa57-665">이 설명서의 온라인 버전 hello http://adv-r.had.co.nz/에서 무료로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-665">hello online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="eaa57-666">시계열 분석에 대 한 hello CRAN 작업 보기에서에서 R 시간 시계열 패키지의 카탈로그를 확인할 수 있습니다: http://cran.r-project.org/web/views/TimeSeries.html 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-666">A catalogue of R time series packages can be found in hello CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="eaa57-667">특정 시간 시계열 개체 패키지에 대 한 자세한 내용은 해당 패키지에 대 한 toohello 설명서를 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-667">For information on specific time series object packages, you should refer toohello documentation for that package.</span></span>

<span data-ttu-id="eaa57-668">hello 책 Paul Cowpertwait 및 Andrew Metcalfe에서 R로 소개 시계열 시계열 분석에 대 한 소개 toousing R을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-668">hello book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction toousing R for time series analysis.</span></span> <span data-ttu-id="eaa57-669">많은 이론서에서 R 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="eaa57-670">다음은 유용한 인터넷 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-670">Some great internet resources:</span></span>

* <span data-ttu-id="eaa57-671">DataCamp: DataCamp hello 편안 하 게 코딩 연습 및 비디오 단원 브라우저에서에서 R 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-671">DataCamp: DataCamp teaches R in hello comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="eaa57-672">Hello 최신 R 기술 및 패키지에 대 한 대화형 자습서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-672">There are interactive tutorials on hello latest R techniques and packages.</span></span> <span data-ttu-id="eaa57-673">Https://www.datacamp.com/courses/introduction-to-r에 hello 무료 대화형 R 자습서를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eaa57-673">Take hello free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="eaa57-674">Programiz에서 R을 시작하는 가이드 https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="eaa57-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="eaa57-675">클라크슨 대학교의 Kelly Black이 제공하는 빠른 R 자습서 http://www.cyclismo.org/tutorial/R/</span><span class="sxs-lookup"><span data-stu-id="eaa57-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="eaa57-676">60 개 이상의 R 리소스 http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span><span class="sxs-lookup"><span data-stu-id="eaa57-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
