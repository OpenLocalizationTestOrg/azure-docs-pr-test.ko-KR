---
title: "Azure 기계 학습에서 사용자 지정 R 모듈 aaaAuthor | Microsoft Docs"
description: "Azure 기계 학습에서 사용자 지정 R 모듈을 작성하기 위한 빠른 시작입니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="ec377-103">Azure 기계 학습에서 사용자 지정 R 모듈 작성</span><span class="sxs-lookup"><span data-stu-id="ec377-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="ec377-104">이 항목에서는 설명 방법을 tooauthor 및 Azure 기계 학습에서 사용자 지정 R 모듈을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-104">This topic describes how tooauthor and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="ec377-105">사용자 지정 R 모듈 정의 및 파일을 사용 하는 toodefine 설명으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-105">It explains what custom R modules are and what files are used toodefine them.</span></span> <span data-ttu-id="ec377-106">방법을 tooconstruct hello 모듈을 정의 하는 파일 및 tooregister 기계 학습 작업 영역에서 배포에 대 한 모듈 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-106">It illustrates how tooconstruct hello files that define a module and how tooregister hello module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="ec377-107">hello 요소와 사용자 지정 모듈 hello의 hello 정의에 사용 되는 특성은 다음 보다 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-107">hello elements and attributes used in hello definition of hello custom module are then described in more detail.</span></span> <span data-ttu-id="ec377-108">어떻게 toouse 보조 기능 및 파일 여러 출력도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-108">How toouse auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="ec377-109">사용자 지정 R 모듈이란?</span><span class="sxs-lookup"><span data-stu-id="ec377-109">What is a custom R module?</span></span>
<span data-ttu-id="ec377-110">A **사용자 지정 모듈** 일 수 있는 사용자 정의 모듈 업로드 tooyour 작업 영역을 이며 Azure 기계 학습 실험의 일부로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-110">A **custom module** is a user-defined module that can be uploaded tooyour workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="ec377-111">사용자 지정 R 모듈은 사용자 정의 R 함수를 실행하는 **사용자 지정 모듈** 입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="ec377-112">**R** 은 통계학자 및 데이터 과학자가 알고리즘을 구현하는 데 널리 사용되는 통계 컴퓨팅 및 그래픽용 프로그래밍 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="ec377-113">현재 R 이후 릴리스를 위한 예약 된 다른 언어에 대 한 사용자 지정 모듈을 검색 하지만 지원에서 지원 되는 hello만 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-113">Currently, R is hello only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="ec377-114">사용자 지정 모듈을 **고급 상태** Azure 기계 학습에서 hello 의미 있는 다른 모듈 처럼 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-114">Custom modules have **first-class status** in Azure Machine Learning in hello sense that they can be used just like any other module.</span></span> <span data-ttu-id="ec377-115">다른 모듈과 함께 실행하거나, 게시된 실험이나 시각화에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="ec377-116">사용 되는 입력 및 출력 포트 toobe hello, 모델링 매개 변수 및 기타 다양 한 런타임 동작을 hello hello 모듈에 의해 구현 되는 hello 알고리즘을 제어할 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-116">You have control over hello algorithm implemented by hello module, hello input and output ports toobe used, hello modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="ec377-117">또한 사용자 지정 모듈을 포함 하는 실험 쉽게 공유할 hello Cortana 인텔리전스 갤러리에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-117">An experiment that contains custom modules can also be published into hello Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="ec377-118">사용자 지정 R 모듈의 파일</span><span class="sxs-lookup"><span data-stu-id="ec377-118">Files in a custom R module</span></span>
<span data-ttu-id="ec377-119">사용자 지정 R 모듈은 최소한 다음 두 개의 파일을 포함하는 .zip 파일로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="ec377-120">A **소스 파일** hello 모듈에 의해 노출 되는 hello R 함수를 구현 하는</span><span class="sxs-lookup"><span data-stu-id="ec377-120">A **source file** that implements hello R function exposed by hello module</span></span>
* <span data-ttu-id="ec377-121">**XML 정의 파일** hello 사용자 지정 모듈 인터페이스를 설명 하는</span><span class="sxs-lookup"><span data-stu-id="ec377-121">An **XML definition file** that describes hello custom module interface</span></span>

<span data-ttu-id="ec377-122">추가 보조 파일 hello 사용자 지정 모듈에서 액세스할 수 있는 기능을 제공 하는 hello.zip 파일에 포함 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-122">Additional auxiliary files can also be included in hello .zip file that provides functionality that can be accessed from hello custom module.</span></span> <span data-ttu-id="ec377-123">이 옵션은 hello에서 설명한 **인수** hello 참조 섹션의 일부로 **hello XML 정의 파일에서 요소** 다음 hello 퀵 스타트 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-123">This option is discussed in hello **Arguments** part of hello reference section **Elements in hello XML definition file** following hello quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="ec377-124">빠른 시작 예: 사용자 지정 R 모듈 정의, 패키지 및 등록</span><span class="sxs-lookup"><span data-stu-id="ec377-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="ec377-125">Tooconstruct 사용자 지정 R 모듈에 필요한 파일을 hello 하는 방법을 보여 주는이 예제, zip 파일을 변환한 다음 기계 학습 작업 영역에 레지스터 hello 모듈 패키지에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-125">This example illustrates how tooconstruct hello files required by a custom R module, package them into a zip file, and then register hello module in your Machine Learning workspace.</span></span> <span data-ttu-id="ec377-126">hello 예제 zip 패키지 및 예제 파일에서 다운로드할 수 있습니다 [다운로드 CustomAddRows.zip 파일](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-126">hello example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="hello-source-file"></a><span data-ttu-id="ec377-127">hello 소스 파일</span><span class="sxs-lookup"><span data-stu-id="ec377-127">hello source file</span></span>
<span data-ttu-id="ec377-128">hello 예제를 고려해 보세요는 **행을 추가 하는 사용자 지정** hello의 표준 구현 hello를 수정 하는 모듈 **행 추가** 모듈이 두 데이터 집합 (데이터 프레임)에서 tooconcatenate 행 (관찰)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-128">Consider hello example of a **Custom Add Rows** module that modifies hello standard implementation of hello **Add Rows** module used tooconcatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="ec377-129">표준 hello **행 추가** hello를 사용 하 여 첫 번째 입력된 데이터 집합을 hello의 hello 두 번째 입력된 데이터 집합 toohello 끝의 hello 행을 추가 하는 모듈 `rbind` 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-129">hello standard **Add Rows** module appends hello rows of hello second input dataset toohello end of hello first input dataset using hello `rbind` algorithm.</span></span> <span data-ttu-id="ec377-130">사용자 지정 하는 hello `CustomAddRows` 함수 마찬가지로 두 개의 데이터 집합을 사용할 수 있지만 추가 입력으로 부울 전환 매개 변수를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-130">hello customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="ec377-131">Hello 스왑 매개 변수가 너무 설정 된 경우**FALSE**, 것 처럼 표준 구현을 hello 반환 hello 동일한 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-131">If hello swap parameter is set too**FALSE**, it returns hello same data set as hello standard implementation.</span></span> <span data-ttu-id="ec377-132">Hello 스왑 매개 변수가 있지만 **TRUE**, hello 함수 대신 hello 두 번째 데이터 집합의 첫 번째 입력된 데이터 집합 toohello 끝의 행을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-132">But if hello swap parameter is **TRUE**, hello function appends rows of first input dataset toohello end of hello second dataset instead.</span></span> <span data-ttu-id="ec377-133">R hello hello 구현이 포함 된 hello CustomAddRows.R 파일 `CustomAddRows` 함수 hello에 의해 노출 **행을 추가 하는 사용자 지정** 모듈에 R 코드를 다음 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-133">hello CustomAddRows.R file that contains hello implementation of hello R `CustomAddRows` function exposed by hello **Custom Add Rows** module has hello following R code.</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="hello-xml-definition-file"></a><span data-ttu-id="ec377-134">hello XML 정의 파일</span><span class="sxs-lookup"><span data-stu-id="ec377-134">hello XML definition file</span></span>
<span data-ttu-id="ec377-135">tooexpose이 `CustomAddRows` 함수를 Azure 기계 학습 모듈로 XML 정의 파일 만들어야 toospecify 어떻게 hello **행을 추가 하는 사용자 지정** 모듈의 디자인과 작동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-135">tooexpose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created toospecify how hello **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="ec377-136">값의 hello hello 중요 toonote는 **id** hello의 특성 **입력** 및 **Arg** hello XML 파일의 요소는 hello R의 hello 함수 매개 변수 이름은 일치 해야 합니다 정확 하 게 hello CustomAddRows.R 파일에 코드: (*dataset1*, *dataset2*, 및 *스왑* hello 예제에서).</span><span class="sxs-lookup"><span data-stu-id="ec377-136">It is critical toonote that hello value of hello **id** attributes of hello **Input** and **Arg** elements in hello XML file must match hello function parameter names of hello R code in hello CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in hello example).</span></span> <span data-ttu-id="ec377-137">마찬가지로, hello의 값을 hello **entryPoint** hello 특성 **언어** 요소 hello R 스크립트의 hello 함수 hello 이름을 정확히 일치 해야 합니다: (*CustomAddRows* hello 예제).</span><span class="sxs-lookup"><span data-stu-id="ec377-137">Similarly, hello value of hello **entryPoint** attribute of hello **Language** element must match hello name of hello function in hello R script EXACTLY: (*CustomAddRows* in hello example).</span></span> 

<span data-ttu-id="ec377-138">반면, hello **id** hello에 대 한 특성 **출력** 요소 hello R 스크립트에서 tooany 변수 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-138">In contrast, hello **id** attribute for hello **Output** element does not correspond tooany variables in hello R script.</span></span> <span data-ttu-id="ec377-139">둘 이상의 출력에 필요한 경우 목록을 hello R 함수에서와 함께 반환 결과 배치 *hello에 동일한 순서* 으로 **출력** 요소 hello XML 파일에도 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-139">When more than one output is required, simply return a list from hello R function with results placed *in hello same order* as **Outputs** elements are declared in hello XML file.</span></span>

### <a name="package-and-register-hello-module"></a><span data-ttu-id="ec377-140">패키지 및 레지스터 hello 모듈</span><span class="sxs-lookup"><span data-stu-id="ec377-140">Package and register hello module</span></span>
<span data-ttu-id="ec377-141">이러한 두 개의 파일을 저장 *CustomAddRows.R* 및 *CustomAddRows.xml* 다음 zip hello 두 개의 파일이 함께에 및를 *CustomAddRows.zip* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip hello two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="ec377-142">기계 학습 작업 영역을 이동 tooyour hello 기계 학습 스튜디오 작업 영역에서 클릭 hello tooregister **+ 새로 만들기** hello 아래쪽에 단추 선택한 **모듈에서 ZIP 패키지->** tooupload 새 hello **행을 추가 하는 사용자 지정** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-142">tooregister them in your Machine Learning workspace, go tooyour workspace in hello Machine Learning Studio, click hello **+NEW** button on hello bottom and choose **MODULE -> FROM ZIP PACKAGE** tooupload hello new **Custom Add Rows** module.</span></span>

![Zip 업로드](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="ec377-144">hello **행을 추가 하는 사용자 지정** 모듈은 기계 학습 실험에서 액세스 하는 준비 toobe 이제 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-144">hello **Custom Add Rows** module is now ready toobe accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-hello-xml-definition-file"></a><span data-ttu-id="ec377-145">Hello XML 정의 파일의 요소</span><span class="sxs-lookup"><span data-stu-id="ec377-145">Elements in hello XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="ec377-146">Module 요소</span><span class="sxs-lookup"><span data-stu-id="ec377-146">Module elements</span></span>
<span data-ttu-id="ec377-147">hello **모듈** 요소는 사용 되는 toodefine hello XML 파일에 사용자 지정 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-147">hello **Module** element is used toodefine a custom module in hello XML file.</span></span> <span data-ttu-id="ec377-148">여러 **module** 요소를 사용하여 여러 모듈을 하나의 XML 파일에 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="ec377-149">작업 영역의 각 모듈은 이름이 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="ec377-150">기존 사용자 지정 모듈 이름이 hello로 사용자 지정 모듈을 등록 하 고 새 hello hello 기존 모듈 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-150">Register a custom module with hello same name as an existing custom module and it replaces hello existing module with hello new one.</span></span> <span data-ttu-id="ec377-151">그러나 사용자 지정 모듈 수 기존 Azure 기계 학습 모듈 이름이 hello로 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-151">Custom modules can, however, be registered with hello same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="ec377-152">따라서에 나타나면 hello **사용자 지정** hello 모듈 색상표의 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-152">If so, they appear in hello **Custom** category of hello module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


<span data-ttu-id="ec377-153">Hello 내 **모듈** 요소를 두 개의 추가 선택적 요소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-153">Within hello **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="ec377-154">**소유자** hello 모듈에 포함 된 요소</span><span class="sxs-lookup"><span data-stu-id="ec377-154">an **Owner** element that is embedded into hello module</span></span>  
* <span data-ttu-id="ec377-155">**설명** 위로 hello 컴퓨터 학습 UI의에서 hello 모듈 및 hello 모듈에 대 한 빠른 도움말 표시 되는 텍스트가 포함 된 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-155">a **Description** element that contains text that is displayed in quick help for hello module and when you hover over hello module in hello Machine Learning UI.</span></span>

<span data-ttu-id="ec377-156">Hello 모듈 요소에 문자 제한에 대 한 규칙:</span><span class="sxs-lookup"><span data-stu-id="ec377-156">Rules for characters limits in hello Module elements:</span></span>

* <span data-ttu-id="ec377-157">값의 hello hello **이름** hello에 대 한 특성 **모듈** 요소는 64 자를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-157">hello value of hello **name** attribute in hello **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="ec377-158">hello 내용의 hello **설명** 요소 길이가 128 자를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-158">hello content of hello **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="ec377-159">hello 내용의 hello **소유자** 요소는 32 자를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-159">hello content of hello **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="ec377-160">Nondeterministic.* * 기본적으로, 모든 모듈 것으로 간주 됩니다 toobe 결정적 또는 모듈의 결과 결정적 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered toobe deterministic.</span></span> <span data-ttu-id="ec377-161">즉, 입력된 매개 변수 및 데이터는 변경 되지 않는 집합이 들어 hello 모듈 반환 해야 hello eacRAND 또는 실행 functionh 시 발생 하는 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-161">That is, given an unchanging set of input parameters and data, hello module should return hello same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="ec377-162">이 문제를 Azure 기계 학습 스튜디오를만 다시 실행 하는 경우 매개 변수 결정적인 함수로 표시 된 모듈 또는 hello 입력된 데이터가 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or hello input data has changed.</span></span> <span data-ttu-id="ec377-163">훨씬 더 빠른 실행의 실험 제공 hello 캐시 된 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-163">Returning hello cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="ec377-164">RAND 또는 hello 현재 날짜 또는 시간을 반환 하는 함수 같은 비결 정적 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-164">There are functions that are nondeterministic, such as RAND or a function that returns hello current date or time.</span></span> <span data-ttu-id="ec377-165">모듈 비결 정적 함수를 사용 하는 경우 해당 hello 모듈은 결정적이 설정 hello 선택적으로 지정할 수 있습니다 **isDeterministic** 너무 특성**FALSE**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-165">If your module uses a nondeterministic function, you can specify that hello module is non-deterministic by setting hello optional **isDeterministic** attribute too**FALSE**.</span></span> <span data-ttu-id="ec377-166">이렇게 하면 해당 hello 모듈을 다시 실행 hello 실험을 실행할 때마다 hello 모듈 입력 및 매개 변수가 변경 되지 않은 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-166">This insures that hello module is rerun whenever hello experiment is run, even if hello module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="ec377-167">언어 정의</span><span class="sxs-lookup"><span data-stu-id="ec377-167">Language Definition</span></span>
<span data-ttu-id="ec377-168">hello **언어** XML 정의 파일에 요소가 사용 되는 toospecify hello 사용자 지정 모듈 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-168">hello **Language** element in your XML definition file is used toospecify hello custom module language.</span></span> <span data-ttu-id="ec377-169">현재 R이 hello 언어 에서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-169">Currently, R is hello only supported language.</span></span> <span data-ttu-id="ec377-170">값의 hello hello **sourceFile** 특성에는 hello 모듈이 실행 되 면 hello 함수 toocall를 포함 하는 hello R 파일의 hello 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-170">hello value of hello **sourceFile** attribute must be hello name of hello R file that contains hello function toocall when hello module is run.</span></span> <span data-ttu-id="ec377-171">이 파일에는 hello zip 패키지의 일부 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-171">This file must be part of hello zip package.</span></span> <span data-ttu-id="ec377-172">값의 hello hello **entryPoint** 특성은 호출 하는 hello 함수 hello 이름이 며 hello 소스 파일에 정의 된 유효한 함수 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-172">hello value of hello **entryPoint** attribute is hello name of hello function being called and must match a valid function defined with in hello source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="ec377-173">포트</span><span class="sxs-lookup"><span data-stu-id="ec377-173">Ports</span></span>
<span data-ttu-id="ec377-174">hello 사용자 지정 모듈에 대 한 입력 및 출력 포트에에서 지정 된 hello의 자식 요소 **포트** hello XML 정의 파일의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-174">hello input and output ports for a custom module are specified in child elements of hello **Ports** section of hello XML definition file.</span></span> <span data-ttu-id="ec377-175">이러한 요소 들의 hello 순서 hello 레이아웃 숙련 된 (사용자 경험) 사용자가을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-175">hello order of these elements determines hello layout experienced (UX) by users.</span></span> <span data-ttu-id="ec377-176">첫 번째 자식 hello **입력** 또는 **출력** hello에 나열 된 **포트** hello XML 파일의 요소는 hello hello 컴퓨터 학습 사용자 환경에서에서 가장 왼쪽 입력된 포트</span><span class="sxs-lookup"><span data-stu-id="ec377-176">hello first child **input** or **output** listed in hello **Ports** element of hello XML file becomes hello left-most input port in hello Machine Learning UX.</span></span>
<span data-ttu-id="ec377-177">각 입력 및 출력 포트는 선택적 있을 수 **설명** hello 텍스트 위로 마우스 커서 hello hello 포트 hello 컴퓨터 학습 UI에에서 표시 된 것을 지정 하는 자식 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-177">Each input and output port may have an optional **Description** child element that specifies hello text shown when you hover hello mouse cursor over hello port in hello Machine Learning UI.</span></span>

<span data-ttu-id="ec377-178">**포트 규칙**:</span><span class="sxs-lookup"><span data-stu-id="ec377-178">**Ports Rules**:</span></span>

* <span data-ttu-id="ec377-179">**입력 및 출력 포트** 의 최대 개수는 각각 8개입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="ec377-180">Input 요소</span><span class="sxs-lookup"><span data-stu-id="ec377-180">Input elements</span></span>
<span data-ttu-id="ec377-181">입력된 포트를 사용 하면 toopass 데이터 tooyour R 함수 및 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-181">Input ports allow you toopass data tooyour R function and workspace.</span></span> <span data-ttu-id="ec377-182">hello **데이터 형식** 입력된 포트는 다음과 같은 지원 되는:</span><span class="sxs-lookup"><span data-stu-id="ec377-182">hello **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="ec377-183">**DataTable:** 이 형식이 data.frame tooyour R 함수에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-183">**DataTable:** This type is passed tooyour R function as a data.frame.</span></span> <span data-ttu-id="ec377-184">기계 학습에서 지원 되는 모든 형식 (예: CSV 파일 또는 ARFF 파일)와 호환 되는 사실, **DataTable** 자동으로 변환 된 tooa data.frame 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted tooa data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="ec377-185">hello **id** 각각와 연관 된 특성 **DataTable** 입력된 포트 고유 값이 있어야 하 고 해당 명명 된 R 함수에 매개 변수이 값이 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-185">hello **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="ec377-186">선택적 **DataTable** 실험에서 입력으로 전달 되지 않는 포트 hello 값에는 **NULL** hello 입력에 연결 되어 있지 않으면 전달 된 toohello R 함수 및 선택적 zip 포트는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-186">Optional **DataTable** ports that are not passed as input in an experiment have hello value **NULL** passed toohello R function and optional zip ports are ignored if hello input is not connected.</span></span> <span data-ttu-id="ec377-187">hello **isOptional** 특성은 모두 hello에 대 한 선택적 **DataTable** 및 **Zip** 형식과 *false* 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-187">hello **isOptional** attribute is optional for both hello **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="ec377-188">**Zip:** 사용자 지정 모듈에서는 zip 파일을 입력으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="ec377-189">이 입력 되 고 함수 hello R 작업 디렉터리에 압축을 풀합니다</span><span class="sxs-lookup"><span data-stu-id="ec377-189">This input is unpacked into hello R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

<span data-ttu-id="ec377-190">사용자 지정 R 모듈 Zip 포트에 대 한 hello id가 없는 toomatch hello R 함수의 모든 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-190">For custom R modules, hello id for a Zip port does not have toomatch any parameters of hello R function.</span></span> <span data-ttu-id="ec377-191">Hello zip 파일은 자동으로 추출 된 toohello R 작업 디렉터리 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-191">This is because hello zip file is automatically extracted toohello R working directory.</span></span>

<span data-ttu-id="ec377-192">**입력 규칙:**</span><span class="sxs-lookup"><span data-stu-id="ec377-192">**Input Rules:**</span></span>

* <span data-ttu-id="ec377-193">값의 hello hello **id** hello 특성 **입력** 요소 유효한 R 변수 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-193">hello value of hello **id** attribute of hello **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="ec377-194">값의 hello hello **id** hello의 특성 **입력** 요소 64 자 보다 길면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-194">hello value of hello **id** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="ec377-195">hello 값 hello **이름** hello의 특성 **입력** 요소 64 자 보다 길면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-195">hello value of hello **name** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="ec377-196">hello 내용의 hello **설명** 요소 128 자를 초과할 수 없습니다</span><span class="sxs-lookup"><span data-stu-id="ec377-196">hello content of hello **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="ec377-197">값의 hello hello **형식** hello 특성 **입력** 요소 여야 합니다. *Zip* 또는 *DataTable*합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-197">hello value of hello **type** attribute of hello **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="ec377-198">값의 hello hello **isOptional** hello 특성 **입력** 요소가 필요 하지 않습니다 (이며 *false* 지정 되지 않은 경우 기본적으로); 있지만 지정 된 경우 이어야합니다*true* 또는 *false*합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-198">hello value of hello **isOptional** attribute of hello **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="ec377-199">Output 요소</span><span class="sxs-lookup"><span data-stu-id="ec377-199">Output elements</span></span>
<span data-ttu-id="ec377-200">**표준 출력 포트:** 출력 포트는 매핑된 toohello 후속 모듈에 의해 사용할 수 있는 R 함수를 사용 하 여 반환 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-200">**Standard output ports:** Output ports are mapped toohello return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="ec377-201">*DataTable* hello 표준 출력 포트 유형을 현재 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-201">*DataTable* is hello only standard output port type supported currently.</span></span> <span data-ttu-id="ec377-202">향후 *Learners* 및 *Transforms*이 지원될 예정입니다. *DataTable* 출력은 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="ec377-203">사용자 지정 R 모듈에서 출력에 대 한 값의 hello hello **id** 특성에는 어디에도 toocorrespond hello R 스크립트에 없지만 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-203">For outputs in custom R modules, hello value of hello **id** attribute does not have toocorrespond with anything in hello R script, but it must be unique.</span></span> <span data-ttu-id="ec377-204">단일 모듈 출력에 대 한 hello hello R 함수의 반환 값 이어야 합니다는 *data.frame*합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-204">For a single module output, hello return value from hello R function must be a *data.frame*.</span></span> <span data-ttu-id="ec377-205">지원 되는 데이터 형식의 개체가 둘 이상 toooutput 순서, hello 적절 한 출력 포트 toobe hello XML 정의 파일에 지정 하며, hello 개체 필요 toobe는 목록으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-205">In order toooutput more than one object of a supported data type, hello appropriate output ports need toobe specified in hello XML definition file and hello objects need toobe returned as a list.</span></span> <span data-ttu-id="ec377-206">hello 출력 개체에서 반환 된 목록 hello에 hello 개체 사항이 hello 순서를 반영 하는 왼쪽된 tooright toooutput 포트 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-206">hello output objects are assigned toooutput ports from left tooright, reflecting hello order in which hello objects are placed in hello returned list.</span></span>

<span data-ttu-id="ec377-207">예를 들어, toomodify hello **행을 추가 하는 사용자 지정** 모듈 toooutput hello 원래 두 개의 데이터 집합 *dataset1* 및 *dataset2*, 또한 toohello 새 조인 데이터 집합, *데이터 집합*, (는 순서에 따라 왼쪽된 tooright에서으로: *데이터 집합*, *dataset1*, *dataset2*), 다음 hello 정의 다음과 같이 hello CustomAddRows.xml 파일에서 포트를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-207">For example, if you want toomodify hello **Custom Add Rows** module toooutput hello original two datasets, *dataset1* and *dataset2*, in addition toohello new joined dataset, *dataset*, (in an order, from left tooright, as: *dataset*, *dataset1*, *dataset2*), then define hello output ports in hello CustomAddRows.xml file as follows:</span></span>

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


<span data-ttu-id="ec377-208">및에서 'CustomAddRows.R' hello 올바른 순서로 hello 목록 개체의 목록에 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-208">And return hello list of objects in a list in hello correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="ec377-209">**시각화 출력:** 형식의 출력 포트를 지정할 수도 있습니다 *시각화*, R hello 그래픽 장치 및 콘솔 출력에서 hello 출력을 표시 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays hello output from hello R graphics device and console output.</span></span> <span data-ttu-id="ec377-210">이 포트 hello R 함수 출력의 일부가 아니며 hello 순서 다른 hello 방해 하지 않습니다 포트 유형을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-210">This port is not part of hello R function output and does not interfere with hello order of hello other output port types.</span></span> <span data-ttu-id="ec377-211">tooadd는 시각화 포트 toohello 사용자 지정 모듈 추가 **출력** 의 값을 가진 요소가 *시각화* 에 대 한 해당 **형식** 특성:</span><span class="sxs-lookup"><span data-stu-id="ec377-211">tooadd a visualization port toohello custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

<span data-ttu-id="ec377-212">**출력 규칙:**</span><span class="sxs-lookup"><span data-stu-id="ec377-212">**Output Rules:**</span></span>

* <span data-ttu-id="ec377-213">값의 hello hello **id** hello 특성 **출력** 요소 유효한 R 변수 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-213">hello value of hello **id** attribute of hello **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="ec377-214">값의 hello hello **id** hello 특성 **출력** 요소 32 자 보다 길 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-214">hello value of hello **id** attribute of hello **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="ec377-215">hello 값 hello **이름** hello의 특성 **출력** 요소 64 자 보다 길면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-215">hello value of hello **name** attribute of hello **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="ec377-216">값의 hello hello **형식** hello 특성 **출력** 요소 여야 합니다. *시각화*합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-216">hello value of hello **type** attribute of hello **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="ec377-217">인수</span><span class="sxs-lookup"><span data-stu-id="ec377-217">Arguments</span></span>
<span data-ttu-id="ec377-218">추가 데이터는 hello에 정의 된 모듈 매개 변수를 통해 toohello R 함수 전달 될 수 있습니다 **인수** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-218">Additional data can be passed toohello R function via module parameters which are defined in hello **Arguments** element.</span></span> <span data-ttu-id="ec377-219">이러한 매개 변수는 hello 모듈을 선택한 경우 hello 컴퓨터 학습 UI의 hello 오른쪽에 있는 속성 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-219">These parameters appear in hello rightmost properties pane of hello Machine Learning UI when hello module is selected.</span></span> <span data-ttu-id="ec377-220">인수는 지원 되는 hello 형식 중 하나일 수 있습니다 또는 필요할 때 사용자 지정 열거를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-220">Arguments can be any of hello supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="ec377-221">비슷한 toohello **포트** 요소 **인수** 요소는 선택적 점이 **설명** hello 마우스를 가리킬 때 표시할 hello 텍스트를 지정 하는 요소 통해 hello 매개 변수 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-221">Similar toohello **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies hello text that appears when you hover hello mouse over hello parameter name.</span></span>
<span data-ttu-id="ec377-222">DefaultValue, minValue 및 maxValue 같은 모듈에 대 한 선택적 속성 tooa 특성으로 tooany 인수를 추가할 수 있습니다 **속성** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added tooany argument as attributes tooa **Properties** element.</span></span> <span data-ttu-id="ec377-223">Hello에 대 한 올바른 속성 **속성** 요소 hello 인수 형식에 따라 다르며 hello 다음 섹션의 인수 형식과 지원 되는 hello와 함께 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-223">Valid properties for hello **Properties** element depend on hello argument type and are described with hello supported argument types in hello next section.</span></span> <span data-ttu-id="ec377-224">Hello로 인수 **isOptional** 속성이 너무 설정**"true"** hello 사용자 tooenter 값이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-224">Arguments with hello **isOptional** property set too**"true"** do not require hello user tooenter a value.</span></span> <span data-ttu-id="ec377-225">값 toohello 인수를 제공 하지 않으면 다음 hello 인수 toohello 진입점 함수를 전달 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-225">If a value is not provided toohello argument, then hello argument is not passed toohello entry point function.</span></span> <span data-ttu-id="ec377-226">예: hello 함수에 의해 명시적으로 처리 하는 선택적 필요 toobe 하의 hello 진입점 함수 인수는 hello 항목 지점 함수 정의의 기본 값은 NULL 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-226">Arguments of hello entry point function that are optional need toobe explicitly handled by hello function, e.g. assigned a default value of NULL in hello entry point function definition.</span></span> <span data-ttu-id="ec377-227">선택적 인수에서 강제 적용만 hello 사용자가 값이 제공 하는 경우 즉, min 또는 max를 다른 인수 제약 조건, hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-227">An optional argument will only enforce hello other argument constraints, i.e. min or max, if a value is provided by hello user.</span></span>
<span data-ttu-id="ec377-228">이 입력 및 출력와 마찬가지로 연결 된 고유 id 값이 있다고 각 hello 매개 변수에 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-228">As with inputs and outputs, it is critical that each of hello parameters have unique id values associated with them.</span></span> <span data-ttu-id="ec377-229">이 빠른 시작 hello id/매개 변수를 연결 하는 예 였습니다 *스왑*합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-229">In our quick start example hello associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="ec377-230">Arg 요소</span><span class="sxs-lookup"><span data-stu-id="ec377-230">Arg element</span></span>
<span data-ttu-id="ec377-231">모듈 매개 변수는 hello를 사용 하 여 정의 된 **Arg** hello의 자식 요소 **인수** hello XML 정의 파일의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-231">A module parameter is defined using hello **Arg** child element of hello **Arguments** section of hello XML definition file.</span></span> <span data-ttu-id="ec377-232">Hello에 hello 자식 요소와 마찬가지로 **포트** 섹션에서 hello의 매개 변수 순서 hello **인수** hello 사용자 환경에서에서 발생 하는 hello 레이아웃을 정의 하는 섹션</span><span class="sxs-lookup"><span data-stu-id="ec377-232">As with hello child elements in hello **Ports** section, hello ordering of parameters in hello **Arguments** section defines hello layout encountered in hello UX.</span></span> <span data-ttu-id="ec377-233">hello에 매개 변수가 나타나는 위에서 아래로 동일한 순서에 정의 된 hello에 UI hello hello XML 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-233">hello parameters appear from top down in hello UI in hello same order in which they are defined in hello XML file.</span></span> <span data-ttu-id="ec377-234">매개 변수에 대 한 기계 학습에서 지원 되는 hello 형식 여기에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-234">hello types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="ec377-235">**int** – 정수(32비트) 형식 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="ec377-236">*선택적 속성*: **min**, **max**, **default** 및 **isOptional**</span><span class="sxs-lookup"><span data-stu-id="ec377-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="ec377-237">**double** – 실수(Double) 형식 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="ec377-238">*선택적 속성*: **min**, **max**, **default** 및 **isOptional**</span><span class="sxs-lookup"><span data-stu-id="ec377-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="ec377-239">**bool** – UX에서 확인란으로 표시되는 부울 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="ec377-240">*선택적 속성*: **default** - 설정하지 않은 경우 false</span><span class="sxs-lookup"><span data-stu-id="ec377-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="ec377-241">**string**: 표준 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="ec377-242">*선택적 속성*: **default** 및 **isOptional**</span><span class="sxs-lookup"><span data-stu-id="ec377-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="ec377-243">**ColumnPicker**: 열 선택 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="ec377-244">이 형식은 hello UX에서에서 열 선택으로 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-244">This type renders in hello UX as a column chooser.</span></span> <span data-ttu-id="ec377-245">hello **속성** 요소는 있는 열을 선택 하면 hello 대상 포트 유형 이어야 합니다 hello 포트의 사용 되는 여기서 toospecify hello id *DataTable*합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-245">hello **Property** element is used here toospecify hello id of hello port from which columns are selected, where hello target port type must be *DataTable*.</span></span> <span data-ttu-id="ec377-246">hello 열 선택의 hello 결과 선택 hello 열 이름이 들어 있는 문자열 목록으로 toohello R 함수를 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-246">hello result of hello column selection is passed toohello R function as a list of strings containing hello selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="ec377-247">*필수 속성*: **portId** -일치 하는 항목 형식과 Input 요소의 id hello *DataTable*합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-247">*Required Properties*: **portId** - matches hello id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="ec377-248">*선택적 속성*:</span><span class="sxs-lookup"><span data-stu-id="ec377-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="ec377-249">**allowedTypes** -hello 열 필터 형식에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-249">**allowedTypes** - Filters hello column types from which you can pick.</span></span> <span data-ttu-id="ec377-250">유효한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="ec377-251">숫자</span><span class="sxs-lookup"><span data-stu-id="ec377-251">Numeric</span></span>
    * <span data-ttu-id="ec377-252">Boolean</span><span class="sxs-lookup"><span data-stu-id="ec377-252">Boolean</span></span>
    * <span data-ttu-id="ec377-253">범주</span><span class="sxs-lookup"><span data-stu-id="ec377-253">Categorical</span></span>
    * <span data-ttu-id="ec377-254">string</span><span class="sxs-lookup"><span data-stu-id="ec377-254">String</span></span>
    * <span data-ttu-id="ec377-255">레이블</span><span class="sxs-lookup"><span data-stu-id="ec377-255">Label</span></span>
    * <span data-ttu-id="ec377-256">기능</span><span class="sxs-lookup"><span data-stu-id="ec377-256">Feature</span></span>
    * <span data-ttu-id="ec377-257">Score</span><span class="sxs-lookup"><span data-stu-id="ec377-257">Score</span></span>
    * <span data-ttu-id="ec377-258">모두</span><span class="sxs-lookup"><span data-stu-id="ec377-258">All</span></span>
  * <span data-ttu-id="ec377-259">**기본** -hello 열 선택에 대 한 올바른 기본 선택 항목 포함:</span><span class="sxs-lookup"><span data-stu-id="ec377-259">**default** - Valid default selections for hello column picker include:</span></span> 
    
    * <span data-ttu-id="ec377-260">없음</span><span class="sxs-lookup"><span data-stu-id="ec377-260">None</span></span>
    * <span data-ttu-id="ec377-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="ec377-261">NumericFeature</span></span>
    * <span data-ttu-id="ec377-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="ec377-262">NumericLabel</span></span>
    * <span data-ttu-id="ec377-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="ec377-263">NumericScore</span></span>
    * <span data-ttu-id="ec377-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="ec377-264">NumericAll</span></span>
    * <span data-ttu-id="ec377-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="ec377-265">BooleanFeature</span></span>
    * <span data-ttu-id="ec377-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="ec377-266">BooleanLabel</span></span>
    * <span data-ttu-id="ec377-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="ec377-267">BooleanScore</span></span>
    * <span data-ttu-id="ec377-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="ec377-268">BooleanAll</span></span>
    * <span data-ttu-id="ec377-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="ec377-269">CategoricalFeature</span></span>
    * <span data-ttu-id="ec377-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="ec377-270">CategoricalLabel</span></span>
    * <span data-ttu-id="ec377-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="ec377-271">CategoricalScore</span></span>
    * <span data-ttu-id="ec377-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="ec377-272">CategoricalAll</span></span>
    * <span data-ttu-id="ec377-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="ec377-273">StringFeature</span></span>
    * <span data-ttu-id="ec377-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="ec377-274">StringLabel</span></span>
    * <span data-ttu-id="ec377-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="ec377-275">StringScore</span></span>
    * <span data-ttu-id="ec377-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="ec377-276">StringAll</span></span>
    * <span data-ttu-id="ec377-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="ec377-277">AllLabel</span></span>
    * <span data-ttu-id="ec377-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="ec377-278">AllFeature</span></span>
    * <span data-ttu-id="ec377-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="ec377-279">AllScore</span></span>
    * <span data-ttu-id="ec377-280">모두</span><span class="sxs-lookup"><span data-stu-id="ec377-280">All</span></span>

<span data-ttu-id="ec377-281">**DropDown**: 사용자가 지정한 열거형(드롭다운) 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="ec377-282">hello 드롭다운 항목 hello 내에서 지정 **속성** 사용 하 여 요소는 **항목** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-282">hello dropdown items are specified within hello **Properties** element using an **Item** element.</span></span> <span data-ttu-id="ec377-283">hello **id** 각 **항목** 고유 해야 하 고 유효한 R 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-283">hello **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="ec377-284">값의 hello hello **이름** 의 **항목** 볼 수 있는 hello 텍스트와 toohello R 함수를 전달 된 값과 hello로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-284">hello value of hello **name** of an **Item** serves as both hello text that you see and hello value that is passed toohello R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="ec377-285">*선택적 속성*:</span><span class="sxs-lookup"><span data-stu-id="ec377-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="ec377-286">**기본** -hello hello 중 하나에서 id 값을 가진 일치 해야 hello 기본 속성의 값 **항목** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-286">**default** - hello value for hello default property must correspond with an id value from one of hello **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="ec377-287">보조 파일</span><span class="sxs-lookup"><span data-stu-id="ec377-287">Auxiliary Files</span></span>
<span data-ttu-id="ec377-288">사용자 지정 모듈 ZIP 파일에 배치 된 모든 파일이 실행 시간 동안 진행 중인 toobe 사용 하기 위해 사용할 수 있는 경우</span><span class="sxs-lookup"><span data-stu-id="ec377-288">Any file that is placed in your custom module ZIP file is going toobe available for use during execution time.</span></span> <span data-ttu-id="ec377-289">모든 디렉터리 구조는 있는 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="ec377-290">이 파일 소싱 works hello 동일한 로컬 및 Azure 기계 학습 실행에서 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-290">This means that file sourcing works hello same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="ec377-291">모든 파일은 추출 된 too'src' 모든 경로가 있어야 하므로 디렉터리 ' src /' 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-291">Notice that all files are extracted too‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="ec377-292">예를 들어 RemoveDupNARows.R 파일에서 수행 하는 R 함수를 이미 작성 하 고 tooremove NAs 있는 hello 데이터 집합에서 모든 행을 CustomAddRows에 출력 하기 전에 모든 중복 행을 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-292">For example, say you want tooremove any rows with NAs from hello dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="ec377-293">Hello 보조 파일 RemoveDupNARows.R hello CustomAddRows 함수에서에서 소스 수 있습니다.:</span><span class="sxs-lookup"><span data-stu-id="ec377-293">You can source hello auxiliary file RemoveDupNARows.R in hello CustomAddRows function:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

<span data-ttu-id="ec377-294">그런 다음 ‘CustomAddRows.R’, ‘CustomAddRows.xml’ 및 ‘RemoveDupNARows.R’이 포함된 zip 파일을 사용자 지정 R 모듈로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="ec377-295">실행 환경</span><span class="sxs-lookup"><span data-stu-id="ec377-295">Execution Environment</span></span>
<span data-ttu-id="ec377-296">hello 실행 환경을 사용 하 여 hello R 스크립트에 대 한 hello와 같은 버전의 R hello **R 스크립트 실행** 모듈 있습니다 사용할 hello 동일 하 고 기본 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-296">hello execution environment for hello R script uses hello same version of R as hello **Execute R Script** module and can use hello same default packages.</span></span> <span data-ttu-id="ec377-297">Hello 사용자 지정 모듈 zip 패키지에 포함 하 여 추가 R 패키지 tooyour 사용자 지정 모듈을 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-297">You can also add additional R packages tooyour custom module by including them in hello custom module zip package.</span></span> <span data-ttu-id="ec377-298">사용자 고유의 R 환경과 마찬가지로 R 스크립트에서 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="ec377-299">**Hello 실행 환경 제한인** 포함:</span><span class="sxs-lookup"><span data-stu-id="ec377-299">**Limitations of hello execution environment** include:</span></span>

* <span data-ttu-id="ec377-300">비영구 파일 시스템: hello 사용자 지정 모듈 실행 될 때 기록 된 파일이 hello 여러 번 실행 간에 유지 되지 같은 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="ec377-300">Non-persistent file system: Files written when hello custom module is run are not persisted across multiple runs of hello same module.</span></span>
* <span data-ttu-id="ec377-301">네트워크 액세스 불가</span><span class="sxs-lookup"><span data-stu-id="ec377-301">No network access</span></span>

