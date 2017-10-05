---
title: "Azure Machine Learning에서 사용자 지정 R 모듈 작성 | Microsoft Docs"
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
ms.openlocfilehash: 964ddb551a475243891abce8a2b835e65569a4ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="1e5c1-103">Azure 기계 학습에서 사용자 지정 R 모듈 작성</span><span class="sxs-lookup"><span data-stu-id="1e5c1-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="1e5c1-104">이 항목에서는 Azure 기계 학습에서 사용자 지정 R 모듈을 작성하여 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-104">This topic describes how to author and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="1e5c1-105">사용자 지정 R 모듈의 정의와 이를 정의하는 데 사용되는 파일을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-105">It explains what custom R modules are and what files are used to define them.</span></span> <span data-ttu-id="1e5c1-106">또한 이러한 파일을 생성하여 기계 학습 작업 영역에서 모듈을 정의하는 파일을 구조화하고 배포용 모듈을 등록하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-106">It illustrates how to construct the files that define a module and how to register the module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="1e5c1-107">그런 다음 사용자 지정 모듈의 정의에 사용되는 요소 및 특성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-107">The elements and attributes used in the definition of the custom module are then described in more detail.</span></span> <span data-ttu-id="1e5c1-108">보조 기능과 파일 및 여러 출력을 사용하는 방법도 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-108">How to use auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="1e5c1-109">사용자 지정 R 모듈이란?</span><span class="sxs-lookup"><span data-stu-id="1e5c1-109">What is a custom R module?</span></span>
<span data-ttu-id="1e5c1-110">**사용자 지정 모듈** 은 사용자의 작업 영역에 업로드하고 Azure 기계 학습 실험의 일부로 실행할 수 있는 사용자 정의 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-110">A **custom module** is a user-defined module that can be uploaded to your workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="1e5c1-111">사용자 지정 R 모듈은 사용자 정의 R 함수를 실행하는 **사용자 지정 모듈** 입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="1e5c1-112">**R** 은 통계학자 및 데이터 과학자가 알고리즘을 구현하는 데 널리 사용되는 통계 컴퓨팅 및 그래픽용 프로그래밍 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="1e5c1-113">현재, R은 사용자 지정 모듈에서 지원되는 유일한 언어이지만 향후 릴리스에서는 추가 언어에 대한 지원이 예정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-113">Currently, R is the only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="1e5c1-114">사용자 지정 모듈은 다른 모든 모듈처럼 사용할 수 있다는 점에서 Azure 기계 학습에서 **첫 번째 클래스** 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-114">Custom modules have **first-class status** in Azure Machine Learning in the sense that they can be used just like any other module.</span></span> <span data-ttu-id="1e5c1-115">다른 모듈과 함께 실행하거나, 게시된 실험이나 시각화에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="1e5c1-116">사용자는 모듈에 의해 구현되는 알고리즘, 사용할 입력 및 출력 포트, 모델링 매개 변수 및 기타 여러 런타임 동작을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-116">You have control over the algorithm implemented by the module, the input and output ports to be used, the modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="1e5c1-117">사용자 지정 모듈을 포함한 실험은 손쉬운 공유를 위해 Cortana 인텔리전스 갤러리에 게시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-117">An experiment that contains custom modules can also be published into the Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="1e5c1-118">사용자 지정 R 모듈의 파일</span><span class="sxs-lookup"><span data-stu-id="1e5c1-118">Files in a custom R module</span></span>
<span data-ttu-id="1e5c1-119">사용자 지정 R 모듈은 최소한 다음 두 개의 파일을 포함하는 .zip 파일로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="1e5c1-120">모듈에 의해 노출되는 R 함수를 구현하는 **소스 파일**</span><span class="sxs-lookup"><span data-stu-id="1e5c1-120">A **source file** that implements the R function exposed by the module</span></span>
* <span data-ttu-id="1e5c1-121">사용자 지정 모듈 인터페이스를 설명하는 **XML 정의 파일**</span><span class="sxs-lookup"><span data-stu-id="1e5c1-121">An **XML definition file** that describes the custom module interface</span></span>

<span data-ttu-id="1e5c1-122">사용자 지정 모듈에서 액세스할 수 있는 기능을 제공하는 추가 보조 파일을 .zip 파일에 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-122">Additional auxiliary files can also be included in the .zip file that provides functionality that can be accessed from the custom module.</span></span> <span data-ttu-id="1e5c1-123">이 옵션은 빠른 시작 예제에 이어지는 참조 섹션 **XML 정의 파일의 요소**의 **인수** 부분에서 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-123">This option is discussed in the **Arguments** part of the reference section **Elements in the XML definition file** following the quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="1e5c1-124">빠른 시작 예: 사용자 지정 R 모듈 정의, 패키지 및 등록</span><span class="sxs-lookup"><span data-stu-id="1e5c1-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="1e5c1-125">이 예제에서는 사용자 지정 R 모듈에 필요한 파일을 생성하고 이를 zip 파일에 패키지한 다음 기계 학습 작업 영역에 모듈을 등록하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-125">This example illustrates how to construct the files required by a custom R module, package them into a zip file, and then register the module in your Machine Learning workspace.</span></span> <span data-ttu-id="1e5c1-126">예제 zip 패키지 및 샘플 파일은 [CustomAddRows.zip 파일 다운로드](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-126">The example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="the-source-file"></a><span data-ttu-id="1e5c1-127">원본 파일</span><span class="sxs-lookup"><span data-stu-id="1e5c1-127">The source file</span></span>
<span data-ttu-id="1e5c1-128">두 데이터 집합(데이터 프레임)의 행(관찰)을 연결하는 데 사용되는 **행 추가** 모듈의 표준 구현을 수정하는 **사용자 지정 행 추가** 모듈의 예제를 고려해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-128">Consider the example of a **Custom Add Rows** module that modifies the standard implementation of the **Add Rows** module used to concatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="1e5c1-129">표준 **행 추가** 모듈은 `rbind` 알고리즘을 사용하여 두 번째 입력 데이터 집합의 행을 첫 번째 입력 데이터 집합의 끝에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-129">The standard **Add Rows** module appends the rows of the second input dataset to the end of the first input dataset using the `rbind` algorithm.</span></span> <span data-ttu-id="1e5c1-130">사용자 지정 `CustomAddRows` 함수는 두 데이터 집합을 허용할 뿐만 아니라 부울 스왑 매개 변수도 추가 입력으로 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-130">The customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="1e5c1-131">스왑 매개 변수가 **FALSE**로 설정된 경우 표준 구현과 동일한 데이터 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-131">If the swap parameter is set to **FALSE**, it returns the same data set as the standard implementation.</span></span> <span data-ttu-id="1e5c1-132">그러나 스왑 매개 변수가 **TRUE**인 경우에는 함수는 대신 첫 번째 입력 데이터 집합의 행을 두 번째 데이터 집합의 끝에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-132">But if the swap parameter is **TRUE**, the function appends rows of first input dataset to the end of the second dataset instead.</span></span> <span data-ttu-id="1e5c1-133">**사용자 지정 행 추가** 모듈에 의해 노출되는 R `CustomAddRows` 함수의 구현을 포함하는 CustomAddRows.R 파일은 다음 R 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-133">The CustomAddRows.R file that contains the implementation of the R `CustomAddRows` function exposed by the **Custom Add Rows** module has the following R code.</span></span>

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

### <a name="the-xml-definition-file"></a><span data-ttu-id="1e5c1-134">XML 정의 파일</span><span class="sxs-lookup"><span data-stu-id="1e5c1-134">The XML definition file</span></span>
<span data-ttu-id="1e5c1-135">이 `CustomAddRows` 함수를 Azure 기계 학습 모듈로 노출하려면 XML 정의 파일을 만들어 **사용자 지정 행 추가** 모듈의 표시 및 동작 방식을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-135">To expose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created to specify how the **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset to another. Dataset 2 is concatenated to Dataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify the base language, script file and R function to use for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: The values of the id attributes in the Input and Arg elements must match the parameter names in the R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>The combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="1e5c1-136">XML 파일의 **Input** 및 **Arg** 요소에 대한 **id** 특성 값은 CustomAddRows.R 파일에 있는 R 코드의 함수 매개 변수 이름(이 예제의 경우 *dataset1*, *dataset2* 및 *swap*)과 정확히 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-136">It is critical to note that the value of the **id** attributes of the **Input** and **Arg** elements in the XML file must match the function parameter names of the R code in the CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in the example).</span></span> <span data-ttu-id="1e5c1-137">마찬가지로, **Language** 요소의 **entryPoint** 특성 값은 R 스크립트의 함수 이름(이 예제의 경우 *CustomAddRows*)과 정확히 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-137">Similarly, the value of the **entryPoint** attribute of the **Language** element must match the name of the function in the R script EXACTLY: (*CustomAddRows* in the example).</span></span> 

<span data-ttu-id="1e5c1-138">반면, **Output** 요소의 **id** 특성은 R 스크립트의 변수에 해당하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-138">In contrast, the **id** attribute for the **Output** element does not correspond to any variables in the R script.</span></span> <span data-ttu-id="1e5c1-139">둘 이상의 출력이 필요한 경우 XML 파일에 선언된 *Output* 요소와 **동일한 순서로** 결과가 배치된 목록이 R 함수에서 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-139">When more than one output is required, simply return a list from the R function with results placed *in the same order* as **Outputs** elements are declared in the XML file.</span></span>

### <a name="package-and-register-the-module"></a><span data-ttu-id="1e5c1-140">모듈 패키지 및 등록</span><span class="sxs-lookup"><span data-stu-id="1e5c1-140">Package and register the module</span></span>
<span data-ttu-id="1e5c1-141">이 두 파일을 *CustomAddRows.R*과 *CustomAddRows.xml*로 저장한 다음 두 파일을 *CustomAddRows.zip* 파일로 함께 압축합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip the two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="1e5c1-142">이 파일을 Machine Learning 작업 영역에 등록하려면 Machine Learning 스튜디오의 작업 영역으로 이동한 후 아래쪽에서 **+새로 만들기** 단추를 클릭하고 **모듈 -> Zip 패키지**를 선택하여 새 **사용자 지정 행 추가** 모듈을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-142">To register them in your Machine Learning workspace, go to your workspace in the Machine Learning Studio, click the **+NEW** button on the bottom and choose **MODULE -> FROM ZIP PACKAGE** to upload the new **Custom Add Rows** module.</span></span>

![Zip 업로드](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="1e5c1-144">이제 기계 학습 실험에서 **사용자 지정 행 추가** 모듈에 액세스할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-144">The **Custom Add Rows** module is now ready to be accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-the-xml-definition-file"></a><span data-ttu-id="1e5c1-145">인수</span><span class="sxs-lookup"><span data-stu-id="1e5c1-145">Elements in the XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="1e5c1-146">Module 요소</span><span class="sxs-lookup"><span data-stu-id="1e5c1-146">Module elements</span></span>
<span data-ttu-id="1e5c1-147">**Module** 요소는 XML 파일에서 사용자 지정 모듈을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-147">The **Module** element is used to define a custom module in the XML file.</span></span> <span data-ttu-id="1e5c1-148">여러 **module** 요소를 사용하여 여러 모듈을 하나의 XML 파일에 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="1e5c1-149">작업 영역의 각 모듈은 이름이 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="1e5c1-150">기존 사용자 지정 모듈과 동일한 이름으로 사용자 지정 모듈을 등록하면 기존 모듈이 새 모듈로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-150">Register a custom module with the same name as an existing custom module and it replaces the existing module with the new one.</span></span> <span data-ttu-id="1e5c1-151">그러나 사용자 지정 모듈을 기존 Azure 기계 학습 모듈과 동일한 이름으로 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-151">Custom modules can, however, be registered with the same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="1e5c1-152">이 경우 모듈 팔레트의 **사용자 지정** 범주에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-152">If so, they appear in the **Custom** category of the module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset to another...</Description>/> 


<span data-ttu-id="1e5c1-153">**Module** 요소 내에서 두 개의 추가 선택적 요소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-153">Within the **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="1e5c1-154">모듈에 포함된 **Owner** 요소</span><span class="sxs-lookup"><span data-stu-id="1e5c1-154">an **Owner** element that is embedded into the module</span></span>  
* <span data-ttu-id="1e5c1-155">모듈에 대한 빠른 도움말 및 기계 학습 UI에서 모듈 위에 마우스 커서를 놓으면 표시되는 텍스트를 포함하는 **Description** 요소.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-155">a **Description** element that contains text that is displayed in quick help for the module and when you hover over the module in the Machine Learning UI.</span></span>

<span data-ttu-id="1e5c1-156">Module 요소의 문자 제한에 대한 규칙:</span><span class="sxs-lookup"><span data-stu-id="1e5c1-156">Rules for characters limits in the Module elements:</span></span>

* <span data-ttu-id="1e5c1-157">**Module** 요소의 **name** 특성 값은 64자를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-157">The value of the **name** attribute in the **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="1e5c1-158">**Description** 요소의 내용은 128자를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-158">The content of the **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="1e5c1-159">**Owner** 요소의 내용은 32자를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-159">The content of the **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="1e5c1-160">모듈의 결과는 결정적이거나 비결정적일 수 있습니다.** 기본적으로 모든 모듈은 결정적인 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered to be deterministic.</span></span> <span data-ttu-id="1e5c1-161">즉, 변경되지 않는 입력 매개 변수 및 데이터 집합이 주어진 경우 모듈은 실행될 때마다 같은 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-161">That is, given an unchanging set of input parameters and data, the module should return the same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="1e5c1-162">이 동작에 따라 Azure 기계 학습 스튜디오는 매개 변수 또는 입력 데이터가 변경된 경우에만 결정적으로 표시된 모듈을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or the input data has changed.</span></span> <span data-ttu-id="1e5c1-163">캐시된 결과 반환은 훨씬 더 빠른 실험의 실행도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-163">Returning the cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="1e5c1-164">현재 날짜 또는 시간을 반환하는 RAND 또는 함수와 같은 비결정적인 함수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-164">There are functions that are nondeterministic, such as RAND or a function that returns the current date or time.</span></span> <span data-ttu-id="1e5c1-165">모듈이 비결정적 함수를 사용하는 경우 옵션 **isDeterministic** 특성을 **FALSE**로 설정하여 모듈을 비결정적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-165">If your module uses a nondeterministic function, you can specify that the module is non-deterministic by setting the optional **isDeterministic** attribute to **FALSE**.</span></span> <span data-ttu-id="1e5c1-166">이는 모듈이 모듈 입력 및 매개 변수가 변경되지 않은 경우에도 실험이 실행될 때마다 다시 실행되는 것을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-166">This insures that the module is rerun whenever the experiment is run, even if the module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="1e5c1-167">언어 정의</span><span class="sxs-lookup"><span data-stu-id="1e5c1-167">Language Definition</span></span>
<span data-ttu-id="1e5c1-168">XML 정의 파일의 **Language** 요소는 사용자 지정 모듈 언어를 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-168">The **Language** element in your XML definition file is used to specify the custom module language.</span></span> <span data-ttu-id="1e5c1-169">현재 지원되는 언어는 R뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-169">Currently, R is the only supported language.</span></span> <span data-ttu-id="1e5c1-170">**sourceFile** 특성 값은 모듈을 실행할 때 호출할 함수가 포함된 R 파일의 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-170">The value of the **sourceFile** attribute must be the name of the R file that contains the function to call when the module is run.</span></span> <span data-ttu-id="1e5c1-171">이 파일은 zip 패키지의 일부여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-171">This file must be part of the zip package.</span></span> <span data-ttu-id="1e5c1-172">**entryPoint** 특성 값은 호출되는 함수의 이름이며, 소스 파일에 정의된 유효한 함수와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-172">The value of the **entryPoint** attribute is the name of the function being called and must match a valid function defined with in the source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="1e5c1-173">포트</span><span class="sxs-lookup"><span data-stu-id="1e5c1-173">Ports</span></span>
<span data-ttu-id="1e5c1-174">사용자 지정 모듈의 입력 및 출력 포트는 XML 정의 파일의 **Ports** 섹션의 자식 요소에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-174">The input and output ports for a custom module are specified in child elements of the **Ports** section of the XML definition file.</span></span> <span data-ttu-id="1e5c1-175">이러한 요소의 순서에 따라 사용자의 레이아웃(UX)이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-175">The order of these elements determines the layout experienced (UX) by users.</span></span> <span data-ttu-id="1e5c1-176">XML 파일의 **Ports** 요소에 나열된 첫 번째 자식 **input** 또는 **output**은 Machine Learning UX의 맨 왼쪽 입력 포트가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-176">The first child **input** or **output** listed in the **Ports** element of the XML file becomes the left-most input port in the Machine Learning UX.</span></span>
<span data-ttu-id="1e5c1-177">각 입력 및 출력 포트에는 사용자가 기계 학습 UI에서 포트 위에 마우스 커서를 놓으면 표시되는 텍스트를 지정하는 선택적 **Description** 자식 요소가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-177">Each input and output port may have an optional **Description** child element that specifies the text shown when you hover the mouse cursor over the port in the Machine Learning UI.</span></span>

<span data-ttu-id="1e5c1-178">**포트 규칙**:</span><span class="sxs-lookup"><span data-stu-id="1e5c1-178">**Ports Rules**:</span></span>

* <span data-ttu-id="1e5c1-179">**입력 및 출력 포트** 의 최대 개수는 각각 8개입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="1e5c1-180">Input 요소</span><span class="sxs-lookup"><span data-stu-id="1e5c1-180">Input elements</span></span>
<span data-ttu-id="1e5c1-181">입력 포트를 통해 사용자는 R 함수 및 작업 영역으로 데이터를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-181">Input ports allow you to pass data to your R function and workspace.</span></span> <span data-ttu-id="1e5c1-182">입력 포트에 지원되는 **데이터 형식** 은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-182">The **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="1e5c1-183">**DataTable:** 이 형식은 data.frame으로 R 함수에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-183">**DataTable:** This type is passed to your R function as a data.frame.</span></span> <span data-ttu-id="1e5c1-184">실제로 기계 학습에서 지원되고 **DataTable** 과 호환되는 모든 형식(예: CSV 파일 또는 ARFF 파일)은 자동으로 data.frame으로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted to a data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="1e5c1-185">각 **DataTable** 입력 포트와 연결된 **id** 특성에는 고유 값이 있어야 하며, 이러한 값은 R 함수의 해당 명명된 매개 변수와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-185">The **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="1e5c1-186">실험에서 입력으로 전달되지 않는 선택적 **DataTable** 포트에는 R 함수로 전달되는 **NULL** 값이 있으며, 선택적 zip 포트는 입력이 연결되지 않은 경우 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-186">Optional **DataTable** ports that are not passed as input in an experiment have the value **NULL** passed to the R function and optional zip ports are ignored if the input is not connected.</span></span> <span data-ttu-id="1e5c1-187">**isOptional** 특성은 **DataTable** 및 **Zip** 형식에 둘 다에 대해 선택 사항이며, 기본적으로 *false*입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-187">The **isOptional** attribute is optional for both the **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="1e5c1-188">**Zip:** 사용자 지정 모듈에서는 zip 파일을 입력으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="1e5c1-189">이 입력은 함수의 R 작업 디렉터리에 압축이 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-189">This input is unpacked into the R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files to be extracted to the R working directory.</Description>
           </Input>

<span data-ttu-id="1e5c1-190">사용자 지정 R 모듈의 경우 Zip 포트에 대한 ID는 R 함수의 매개 변수와 일치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-190">For custom R modules, the id for a Zip port does not have to match any parameters of the R function.</span></span> <span data-ttu-id="1e5c1-191">zip 파일은 R 작업 디렉터리에 자동으로 추출되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-191">This is because the zip file is automatically extracted to the R working directory.</span></span>

<span data-ttu-id="1e5c1-192">**입력 규칙:**</span><span class="sxs-lookup"><span data-stu-id="1e5c1-192">**Input Rules:**</span></span>

* <span data-ttu-id="1e5c1-193">**Input** 요소의 **id** 특성 값은 유효한 R 변수 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-193">The value of the **id** attribute of the **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="1e5c1-194">**Input** 요소의 **id** 특성 값은 64자 이내여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-194">The value of the **id** attribute of the **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="1e5c1-195">**Input** 요소의 **name** 특성 값은 64자 이내여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-195">The value of the **name** attribute of the **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="1e5c1-196">**Description** 요소의 내용은 128자 이내여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-196">The content of the **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="1e5c1-197">**Input** 요소의 **type** 특성 값은 *Zip* 또는 *DataTable*이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-197">The value of the **type** attribute of the **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="1e5c1-198">**Input** 요소의 **isOptional** 특성 값은 필수가 아니지만(지정하지 않을 경우 기본적으로 *false*) 지정한 경우 *true* 또는 *false*여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-198">The value of the **isOptional** attribute of the **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="1e5c1-199">Output 요소</span><span class="sxs-lookup"><span data-stu-id="1e5c1-199">Output elements</span></span>
<span data-ttu-id="1e5c1-200">**표준 출력 포트:** 출력 포트는 R 함수의 반환 값에 매핑되어 후속 모듈에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-200">**Standard output ports:** Output ports are mapped to the return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="1e5c1-201">*DataTable* 은 현재 지원되는 유일한 표준 출력 포트 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-201">*DataTable* is the only standard output port type supported currently.</span></span> <span data-ttu-id="1e5c1-202">향후 *Learners* 및 *Transforms*이 지원될 예정입니다. *DataTable* 출력은 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="1e5c1-203">사용자 지정 R 모듈의 출력은 **id** 특성 값이 R 스크립트의 항목에 해당할 필요는 없지만 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-203">For outputs in custom R modules, the value of the **id** attribute does not have to correspond with anything in the R script, but it must be unique.</span></span> <span data-ttu-id="1e5c1-204">단일 모듈 출력의 경우 R 함수의 반환 값은 *data.frame*이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-204">For a single module output, the return value from the R function must be a *data.frame*.</span></span> <span data-ttu-id="1e5c1-205">지원되는 데이터 형식의 개체를 두 개 이상 출력하려면 XML 정의 파일에 해당 출력 포트를 지정하고 개체를 목록으로 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-205">In order to output more than one object of a supported data type, the appropriate output ports need to be specified in the XML definition file and the objects need to be returned as a list.</span></span> <span data-ttu-id="1e5c1-206">출력 개체는 반환되는 목록에서 개체가 배치된 순서를 나타내도록 왼쪽으로 오른쪽으로 출력 포트에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-206">The output objects are assigned to output ports from left to right, reflecting the order in which the objects are placed in the returned list.</span></span>

<span data-ttu-id="1e5c1-207">예를 들어 **사용자 지정 행 추가** 모듈을 새로 조인된 *dataset*과 함께 원래 두 데이터 집합 *dataset1* 및 *dataset2*를 출력(왼쪽부터 순서대로 *dataset*, *dataset1*, *dataset2*)하도록 수정하려면 CustomAddRows.xml 파일에서 다음과 같이 출력 포트를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-207">For example, if you want to modify the **Custom Add Rows** module to output the original two datasets, *dataset1* and *dataset2*, in addition to the new joined dataset, *dataset*, (in an order, from left to right, as: *dataset*, *dataset1*, *dataset2*), then define the output ports in the CustomAddRows.xml file as follows:</span></span>

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


<span data-ttu-id="1e5c1-208">그런 다음 ‘CustomAddRows.R’에서 올바른 순서로 목록에 있는 개체 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-208">And return the list of objects in a list in the correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="1e5c1-209">**시각화 출력:** R 그래픽 장치의 출력 및 콘솔 출력을 표시하는 *Visualization*형식의 출력 포트를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays the output from the R graphics device and console output.</span></span> <span data-ttu-id="1e5c1-210">이 포트는 R 함수 출력의 일부가 아니며 다른 출력 포트 형식의 순서와 간섭되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-210">This port is not part of the R function output and does not interfere with the order of the other output port types.</span></span> <span data-ttu-id="1e5c1-211">사용자 지정 모듈에 시각화 포트를 추가하려면 해당 **type** 특성 값이 *Visualization*인 **Output** 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-211">To add a visualization port to the custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View the R console graphics device output.</Description>
    </Output>

<span data-ttu-id="1e5c1-212">**출력 규칙:**</span><span class="sxs-lookup"><span data-stu-id="1e5c1-212">**Output Rules:**</span></span>

* <span data-ttu-id="1e5c1-213">**Output** 요소의 **id** 특성 값은 유효한 R 변수 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-213">The value of the **id** attribute of the **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="1e5c1-214">**Output** 요소의 **id** 특성 값은 32자 이내여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-214">The value of the **id** attribute of the **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="1e5c1-215">**Output** 요소의 **name** 특성 값은 64자 이내여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-215">The value of the **name** attribute of the **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="1e5c1-216">**Output** 요소의 **type** 특성 값은 *Visualization*이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-216">The value of the **type** attribute of the **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="1e5c1-217">인수</span><span class="sxs-lookup"><span data-stu-id="1e5c1-217">Arguments</span></span>
<span data-ttu-id="1e5c1-218">**Arguments** 요소에 정의된 모듈 매개 변수를 통해 R 함수에 추가 데이터를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-218">Additional data can be passed to the R function via module parameters which are defined in the **Arguments** element.</span></span> <span data-ttu-id="1e5c1-219">이러한 매개 변수는 모듈을 선택한 경우 기계 학습 UI의 맨 오른쪽 속성 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-219">These parameters appear in the rightmost properties pane of the Machine Learning UI when the module is selected.</span></span> <span data-ttu-id="1e5c1-220">인수는 지원되는 형식 중 하나이거나, 필요한 경우 사용자 지정 열거형을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-220">Arguments can be any of the supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="1e5c1-221">**Ports** 요소와 마찬가지로, **Arguments** 요소에는 매개 변수 이름 위에 마우스를 놓으면 표시되는 텍스트를 지정하는 선택적 **Description** 요소가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-221">Similar to the **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies the text that appears when you hover the mouse over the parameter name.</span></span>
<span data-ttu-id="1e5c1-222">defaultValue, minValue 및 maxValue와 같은 모듈의 선택적 속성을 **Properties** 요소의 특성으로 인수에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added to any argument as attributes to a **Properties** element.</span></span> <span data-ttu-id="1e5c1-223">**Properties** 요소의 유효한 속성은 인수 형식에 따라 다르며, 아래 섹션의 지원되는 인수 형식에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-223">Valid properties for the **Properties** element depend on the argument type and are described with the supported argument types in the next section.</span></span> <span data-ttu-id="1e5c1-224">**"true"**로 설정된 **isOptional** 속성을 가진 인수는 사용자가 값을 입력하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-224">Arguments with the **isOptional** property set to **"true"** do not require the user to enter a value.</span></span> <span data-ttu-id="1e5c1-225">인수에 값을 입력하지 않으면 진입점 함수에 전달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-225">If a value is not provided to the argument, then the argument is not passed to the entry point function.</span></span> <span data-ttu-id="1e5c1-226">예: 선택적인 진입점 함수의 인수는 함수에 의해 명시적으로 처리되어야 합니다(예: 진입점 함수 정에서 할당된 NULL의 기본값).</span><span class="sxs-lookup"><span data-stu-id="1e5c1-226">Arguments of the entry point function that are optional need to be explicitly handled by the function, e.g. assigned a default value of NULL in the entry point function definition.</span></span> <span data-ttu-id="1e5c1-227">선택적 인수는 사용자가 값을 제공하는 경우 다른 인수 제약 조건(즉, min 또는 max)을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-227">An optional argument will only enforce the other argument constraints, i.e. min or max, if a value is provided by the user.</span></span>
<span data-ttu-id="1e5c1-228">입력 및 출력과 마찬가지로 각 매개 변수에는 고유한 ID 값이 연결되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-228">As with inputs and outputs, it is critical that each of the parameters have unique id values associated with them.</span></span> <span data-ttu-id="1e5c1-229">이 빠른 시작 예제에서 연결된 ID/매개 변수는 *swap*입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-229">In our quick start example the associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="1e5c1-230">Arg 요소</span><span class="sxs-lookup"><span data-stu-id="1e5c1-230">Arg element</span></span>
<span data-ttu-id="1e5c1-231">모듈 매개 변수는 XML 정의 파일에서 **Arguments** 섹션의 **Arg** 자식 요소를 사용하여 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-231">A module parameter is defined using the **Arg** child element of the **Arguments** section of the XML definition file.</span></span> <span data-ttu-id="1e5c1-232">**Ports** 섹션의 하위 요소와 마찬가지로 **Arguments** 섹션의 매개 변수 순서는 UX 레이아웃을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-232">As with the child elements in the **Ports** section, the ordering of parameters in the **Arguments** section defines the layout encountered in the UX.</span></span> <span data-ttu-id="1e5c1-233">매개 변수는 XML 파일에 정의된 순서대로 위에서 아래로 UI에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-233">The parameters appear from top down in the UI in the same order in which they are defined in the XML file.</span></span> <span data-ttu-id="1e5c1-234">기계 학습에서 지원하는 매개 변수 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-234">The types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="1e5c1-235">**int** – 정수(32비트) 형식 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="1e5c1-236">*선택적 속성*: **min**, **max**, **default** 및 **isOptional**</span><span class="sxs-lookup"><span data-stu-id="1e5c1-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="1e5c1-237">**double** – 실수(Double) 형식 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="1e5c1-238">*선택적 속성*: **min**, **max**, **default** 및 **isOptional**</span><span class="sxs-lookup"><span data-stu-id="1e5c1-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="1e5c1-239">**bool** – UX에서 확인란으로 표시되는 부울 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="1e5c1-240">*선택적 속성*: **default** - 설정하지 않은 경우 false</span><span class="sxs-lookup"><span data-stu-id="1e5c1-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="1e5c1-241">**string**: 표준 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="1e5c1-242">*선택적 속성*: **default** 및 **isOptional**</span><span class="sxs-lookup"><span data-stu-id="1e5c1-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="1e5c1-243">**ColumnPicker**: 열 선택 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="1e5c1-244">이 형식은 UX에서 열 선택기로 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-244">This type renders in the UX as a column chooser.</span></span> <span data-ttu-id="1e5c1-245">여기에서 **Property** 요소는 열을 선택할 포트의 ID를 지정하는 데 사용되며, 대상 포트 형식은 *DataTable*이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-245">The **Property** element is used here to specify the id of the port from which columns are selected, where the target port type must be *DataTable*.</span></span> <span data-ttu-id="1e5c1-246">열 선택의 결과는 선택한 열 이름이 포함된 문자열 목록으로 R 함수에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-246">The result of the column selection is passed to the R function as a list of strings containing the selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="1e5c1-247">*필수 속성*: **portId** - 형식이 *DataTable*인 Input 요소의 ID와 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-247">*Required Properties*: **portId** - matches the id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="1e5c1-248">*선택적 속성*:</span><span class="sxs-lookup"><span data-stu-id="1e5c1-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="1e5c1-249">**allowedTypes** - 선택할 수 있는 열 형식을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-249">**allowedTypes** - Filters the column types from which you can pick.</span></span> <span data-ttu-id="1e5c1-250">유효한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="1e5c1-251">숫자</span><span class="sxs-lookup"><span data-stu-id="1e5c1-251">Numeric</span></span>
    * <span data-ttu-id="1e5c1-252">Boolean</span><span class="sxs-lookup"><span data-stu-id="1e5c1-252">Boolean</span></span>
    * <span data-ttu-id="1e5c1-253">범주</span><span class="sxs-lookup"><span data-stu-id="1e5c1-253">Categorical</span></span>
    * <span data-ttu-id="1e5c1-254">string</span><span class="sxs-lookup"><span data-stu-id="1e5c1-254">String</span></span>
    * <span data-ttu-id="1e5c1-255">레이블</span><span class="sxs-lookup"><span data-stu-id="1e5c1-255">Label</span></span>
    * <span data-ttu-id="1e5c1-256">기능</span><span class="sxs-lookup"><span data-stu-id="1e5c1-256">Feature</span></span>
    * <span data-ttu-id="1e5c1-257">Score</span><span class="sxs-lookup"><span data-stu-id="1e5c1-257">Score</span></span>
    * <span data-ttu-id="1e5c1-258">모두</span><span class="sxs-lookup"><span data-stu-id="1e5c1-258">All</span></span>
  * <span data-ttu-id="1e5c1-259">**default** -열 선택의 유효한 기본 선택 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-259">**default** - Valid default selections for the column picker include:</span></span> 
    
    * <span data-ttu-id="1e5c1-260">없음</span><span class="sxs-lookup"><span data-stu-id="1e5c1-260">None</span></span>
    * <span data-ttu-id="1e5c1-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="1e5c1-261">NumericFeature</span></span>
    * <span data-ttu-id="1e5c1-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="1e5c1-262">NumericLabel</span></span>
    * <span data-ttu-id="1e5c1-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="1e5c1-263">NumericScore</span></span>
    * <span data-ttu-id="1e5c1-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="1e5c1-264">NumericAll</span></span>
    * <span data-ttu-id="1e5c1-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="1e5c1-265">BooleanFeature</span></span>
    * <span data-ttu-id="1e5c1-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="1e5c1-266">BooleanLabel</span></span>
    * <span data-ttu-id="1e5c1-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="1e5c1-267">BooleanScore</span></span>
    * <span data-ttu-id="1e5c1-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="1e5c1-268">BooleanAll</span></span>
    * <span data-ttu-id="1e5c1-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="1e5c1-269">CategoricalFeature</span></span>
    * <span data-ttu-id="1e5c1-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="1e5c1-270">CategoricalLabel</span></span>
    * <span data-ttu-id="1e5c1-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="1e5c1-271">CategoricalScore</span></span>
    * <span data-ttu-id="1e5c1-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="1e5c1-272">CategoricalAll</span></span>
    * <span data-ttu-id="1e5c1-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="1e5c1-273">StringFeature</span></span>
    * <span data-ttu-id="1e5c1-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="1e5c1-274">StringLabel</span></span>
    * <span data-ttu-id="1e5c1-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="1e5c1-275">StringScore</span></span>
    * <span data-ttu-id="1e5c1-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="1e5c1-276">StringAll</span></span>
    * <span data-ttu-id="1e5c1-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="1e5c1-277">AllLabel</span></span>
    * <span data-ttu-id="1e5c1-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="1e5c1-278">AllFeature</span></span>
    * <span data-ttu-id="1e5c1-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="1e5c1-279">AllScore</span></span>
    * <span data-ttu-id="1e5c1-280">모두</span><span class="sxs-lookup"><span data-stu-id="1e5c1-280">All</span></span>

<span data-ttu-id="1e5c1-281">**DropDown**: 사용자가 지정한 열거형(드롭다운) 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="1e5c1-282">드롭다운 항목은 **Item** 요소를 사용하여 **Properties** 요소 내에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-282">The dropdown items are specified within the **Properties** element using an **Item** element.</span></span> <span data-ttu-id="1e5c1-283">각 **Item**에 대한 **id**는 고유하고 유효한 R 변수여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-283">The **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="1e5c1-284">**Item**의 **name** 값은 표시되는 텍스트와 R 함수에 전달되는 값으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-284">The value of the **name** of an **Item** serves as both the text that you see and the value that is passed to the R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="1e5c1-285">*선택적 속성*:</span><span class="sxs-lookup"><span data-stu-id="1e5c1-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="1e5c1-286">**default** - 기본 속성 값은 **Item** 요소 중 하나의 id 값에 해당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-286">**default** - The value for the default property must correspond with an id value from one of the **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="1e5c1-287">보조 파일</span><span class="sxs-lookup"><span data-stu-id="1e5c1-287">Auxiliary Files</span></span>
<span data-ttu-id="1e5c1-288">사용자 지정 모듈 ZIP 파일에 있는 모든 파일은 실행 시간 동안 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-288">Any file that is placed in your custom module ZIP file is going to be available for use during execution time.</span></span> <span data-ttu-id="1e5c1-289">모든 디렉터리 구조는 있는 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="1e5c1-290">따라서 파일 소싱이 로컬과 Azure 기계 학습 실행에서 동일하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-290">This means that file sourcing works the same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="1e5c1-291">모든 파일은 'src' 디렉터리로 추출되므로 모든 경로에 'src/' 접두사가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-291">Notice that all files are extracted to ‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="1e5c1-292">예를 들어 데이터 집합을 CustomAddRows에 출력하기 전에 NA가 있는 모든 행과 모든 중복 행을 데이터 집합에서 제거하려는 경우 RemoveDupNARows.R 파일에서 이 작업을 수행하는 R 함수를 이미 작성했다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-292">For example, say you want to remove any rows with NAs from the dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="1e5c1-293">CustomAddRows 함수에서 보조 파일 RemoveDupNARows.R을 소싱할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-293">You can source the auxiliary file RemoveDupNARows.R in the CustomAddRows function:</span></span>

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

<span data-ttu-id="1e5c1-294">그런 다음 ‘CustomAddRows.R’, ‘CustomAddRows.xml’ 및 ‘RemoveDupNARows.R’이 포함된 zip 파일을 사용자 지정 R 모듈로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="1e5c1-295">실행 환경</span><span class="sxs-lookup"><span data-stu-id="1e5c1-295">Execution Environment</span></span>
<span data-ttu-id="1e5c1-296">R 스크립트의 실행 환경에서는 **R 스크립트 실행** 모듈과 동일한 버전의 R을 사용하며, 동일한 기본 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-296">The execution environment for the R script uses the same version of R as the **Execute R Script** module and can use the same default packages.</span></span> <span data-ttu-id="1e5c1-297">사용자 지정 모듈 zip 패키지에 포함하여 사용자 지정 모듈에 추가 R 패키지를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-297">You can also add additional R packages to your custom module by including them in the custom module zip package.</span></span> <span data-ttu-id="1e5c1-298">사용자 고유의 R 환경과 마찬가지로 R 스크립트에서 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="1e5c1-299">**실행 환경에 대한 제한 사항** 은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-299">**Limitations of the execution environment** include:</span></span>

* <span data-ttu-id="1e5c1-300">비영구 파일 시스템: 사용자 지정 모듈을 실행할 때 작성한 파일은 동일한 모듈의 여러 실행에서 유지되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e5c1-300">Non-persistent file system: Files written when the custom module is run are not persisted across multiple runs of the same module.</span></span>
* <span data-ttu-id="1e5c1-301">네트워크 액세스 불가</span><span class="sxs-lookup"><span data-stu-id="1e5c1-301">No network access</span></span>

