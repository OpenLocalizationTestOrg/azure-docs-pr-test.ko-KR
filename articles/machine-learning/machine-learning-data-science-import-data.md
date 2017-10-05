---
title: "Machine Learning 스튜디오로 데이터 가져오기 | Microsoft Docs"
description: "다양한 데이터 원본에서 Azure 기계 학습 스튜디오로 데이터를 가져오는 방법 지원되는 데이터 형식에 대해 알아봅니다."
keywords: "데이터 가져오기, 데이터 형식, 데이터 유형, 데이터 원본, 학습 데이터"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: b92b480e62f4ce4f4836dc5d0f6afbe80c6b664a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="5ae2e-105">다양한 데이터 원본에서 Azure 기계 학습 스튜디오로 학습 데이터를 가져오기</span><span class="sxs-lookup"><span data-stu-id="5ae2e-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="5ae2e-106">다음을 수행하면 기계 학습 스튜디오에 사용자 고유의 데이터를 사용하여 예측 분석 솔루션을 개발 및 학습할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-106">To use your own data in Machine Learning Studio to develop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="5ae2e-107">미리 하드 드라이브의 **로컬 파일** 에서 데이터를 업로드하여 사용자의 작업 영역에 데이터 집합 모듈을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-107">upload data from a **local file** ahead of time from your hard drive to create a dataset module in your workspace</span></span>
* <span data-ttu-id="5ae2e-108">[데이터 가져오기][import-data] 모듈을 사용하여 실험을 실행하는 동안 여러 **온라인 데이터 원본** 중 하나에서 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-108">access data from one of several **online data sources** while your experiment is running using the [Import Data][import-data] module</span></span> 
* <span data-ttu-id="5ae2e-109">**데이터 집합**으로 저장된 또 다른 Azure 기계 학습 실험에서 나온 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="5ae2e-110">온-프레미스 **SQL Server 데이터베이스**에서 데이터 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="5ae2e-111">이러한 각 옵션을 아래 메뉴의 항목 중 하나에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-111">Each of these options is described in one of the topics on the menu below.</span></span> <span data-ttu-id="5ae2e-112">이 항목에서는 기계 학습 스튜디오에서 사용하기 위해 이러한 여러 데이터 원본에서 데이터를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-112">These topics show you how to import data from these various data sources to use in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="5ae2e-113">기계 학습 스튜디오에는 학습 데이터로 사용할 수 있는 샘플 데이터 집합이 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="5ae2e-114">이에 대한 자세한 내용은 ( [Azure 기계 학습 스튜디오의 샘플 데이터 집합 사용](machine-learning-use-sample-datasets.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-114">For information on these, see [Use the sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="5ae2e-115">또한 이 소개 항목에서는 기계 학습 스튜디오에 사용할 준비가 완료된 데이터를 가져오는 방법을 보여 주고 지원되는 데이터 형식과 데이터 유형을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-115">This introductory topic also discusses how to get data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="5ae2e-116">Azure 기계 학습 스튜디오에서 사용할 준비가 완료된 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="5ae2e-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="5ae2e-117">기계 학습 스튜디오는 데이터베이스에서 구분되었거나 구조화된 데이터인 텍스트 데이터 등의 직사각형 또는 테이블 형식 데이터에 대해 작업하도록 설계되어 있습니다. 단, 경우에 따라 직사각형이 아닌 데이터도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-117">Machine Learning Studio is designed to work with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="5ae2e-118">데이터가 비교적 정리되어 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="5ae2e-119">즉, 실험에 데이터를 업로드하기 전에 따옴표가 없는 문자열 등의 문제를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-119">That is, you'll want to take care of issues such as unquoted strings before you upload the data into your experiment.</span></span>

<span data-ttu-id="5ae2e-120">그러나 기계 학습 스튜디오에는 실험에서 데이터를 조작할 수 있는 모듈도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="5ae2e-121">사용할 기계 학습 알고리즘에 따라 누락된 값 및 스파스 데이터와 같은 데이터 구조 문제 해결 방법을 결정해야 하며, 이때 도움을 줄 수 있는 모듈이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-121">Depending on the machine learning algorithms you'll be using, you may need to decide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="5ae2e-122">모듈 팔레트의 **데이터 변환** 섹션에서 이러한 함수를 수행하는 모듈을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-122">Look in the **Data Transformation** section of the module palette for modules that perform these functions.</span></span>

<span data-ttu-id="5ae2e-123">실험을 수행하는 동안 언제든지 출력 포트를 클릭하여 모듈에서 생성한 데이터를 보거나 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-123">At any point in your experiment you can view or download the data that's produced by a module by clicking the output port.</span></span> <span data-ttu-id="5ae2e-124">모듈에 따라 서로 다른 다운로드 옵션을 사용할 수 있습니다. 또는 기계 학습 스튜디오의 웹 브라우저에서 데이터를 시각화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-124">Depending on the module, there may be different download options available, or you may be able to visualize the data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="5ae2e-125">지원되는 데이터 형식 및 데이터 유형</span><span class="sxs-lookup"><span data-stu-id="5ae2e-125">Data formats and data types supported</span></span>
<span data-ttu-id="5ae2e-126">데이터를 가져오는 데 사용하는 메커니즘과 데이터의 출처에 따라 실험에 여러 데이터 형식을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-126">You can import a number of data types into your experiment, depending on what mechanism you use to import data and where it's coming from:</span></span>

* <span data-ttu-id="5ae2e-127">일반 텍스트(.txt)</span><span class="sxs-lookup"><span data-stu-id="5ae2e-127">Plain text (.txt)</span></span>
* <span data-ttu-id="5ae2e-128">헤더가 있거나(.csv) 없는(.nh.csv) 쉼표로 구분된 값(CSV)</span><span class="sxs-lookup"><span data-stu-id="5ae2e-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="5ae2e-129">헤더가 있거나(.tsv) 없는(.nh.tsv) 탭으로 구분된 값(TSV)</span><span class="sxs-lookup"><span data-stu-id="5ae2e-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="5ae2e-130">Excel 파일</span><span class="sxs-lookup"><span data-stu-id="5ae2e-130">Excel file</span></span>
* <span data-ttu-id="5ae2e-131">Azure 테이블</span><span class="sxs-lookup"><span data-stu-id="5ae2e-131">Azure table</span></span>
* <span data-ttu-id="5ae2e-132">Hive 테이블</span><span class="sxs-lookup"><span data-stu-id="5ae2e-132">Hive table</span></span>
* <span data-ttu-id="5ae2e-133">SQL 데이터베이스 테이블</span><span class="sxs-lookup"><span data-stu-id="5ae2e-133">SQL database table</span></span>
* <span data-ttu-id="5ae2e-134">OData 값</span><span class="sxs-lookup"><span data-stu-id="5ae2e-134">OData values</span></span>
* <span data-ttu-id="5ae2e-135">SVMLight 데이터(.svmlight)(형식 정보는 [SVMLight 정의](http://svmlight.joachims.org/) 참조)</span><span class="sxs-lookup"><span data-stu-id="5ae2e-135">SVMLight data (.svmlight) (see the [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="5ae2e-136">특성 관계 파일 형식(ARFF) 데이터(.arff)(형식 정보는 [ARFF 정의](http://weka.wikispaces.com/ARFF) 참조)</span><span class="sxs-lookup"><span data-stu-id="5ae2e-136">Attribute Relation File Format (ARFF) data (.arff) (see the [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="5ae2e-137">Zip 파일(.zip)</span><span class="sxs-lookup"><span data-stu-id="5ae2e-137">Zip file (.zip)</span></span>
* <span data-ttu-id="5ae2e-138">R 개체 또는 작업 영역 파일(. RData)</span><span class="sxs-lookup"><span data-stu-id="5ae2e-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="5ae2e-139">메타 데이터를 포함하는 ARFF와 같은 형식으로 데이터를 가져오는 경우, 기계 학습 스튜디오에서는 이 메타 데이터를 사용하여 각 열의 머리글과 데이터 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata to define the heading and data type of each column.</span></span>

<span data-ttu-id="5ae2e-140">이 메타 데이터를 포함하지 않는 TSV 또는 CSV 형식과 같은 데이터를 가져오는 경우, 기계 학습에서는 데이터를 샘플링하여 각 열의 데이터 형식을 유추합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers the data type for each column by sampling the data.</span></span> <span data-ttu-id="5ae2e-141">데이터에 열 머리글이 없는 경우 기계 학습 스튜디오에서 기본 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-141">If the data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="5ae2e-142">[메타데이터 편집][edit-metadata]을 사용하여 열의 머리글과 데이터 유형을 명시적으로 지정하거나 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-142">You can explicitly specify or change the headings and data types for columns using the [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="5ae2e-143">기계 학습 스튜디오에서 인식하는 **데이터 유형** 은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-143">The following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="5ae2e-144">String</span><span class="sxs-lookup"><span data-stu-id="5ae2e-144">String</span></span>
* <span data-ttu-id="5ae2e-145">Integer</span><span class="sxs-lookup"><span data-stu-id="5ae2e-145">Integer</span></span>
* <span data-ttu-id="5ae2e-146">double</span><span class="sxs-lookup"><span data-stu-id="5ae2e-146">Double</span></span>
* <span data-ttu-id="5ae2e-147">Boolean</span><span class="sxs-lookup"><span data-stu-id="5ae2e-147">Boolean</span></span>
* <span data-ttu-id="5ae2e-148">DateTime</span><span class="sxs-lookup"><span data-stu-id="5ae2e-148">DateTime</span></span>
* <span data-ttu-id="5ae2e-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="5ae2e-149">TimeSpan</span></span>

<span data-ttu-id="5ae2e-150">Machine Learning 스튜디오에서는 ***데이터 테이블***이라는 내부 데이터 형식을 사용하여 모듈 간에 데이터를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-150">Machine Learning Studio uses an internal data type called ***Data Table*** to pass data between modules.</span></span> <span data-ttu-id="5ae2e-151">[데이터 집합으로 변환][convert-to-dataset] 모듈을 사용하여 명시적으로 데이터를 데이터 테이블 형식으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-151">You can explicitly convert your data into Data Table format using the [Convert to Dataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="5ae2e-152">데이터 테이블 이외의 형식을 허용하는 모든 모듈에서는 다음 모듈에 데이터를 전달하기 전에 데이터를 데이터 테이블로 자동 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-152">Any module that accepts formats other than Data Table will convert the data to Data Table silently before passing it to the next module.</span></span>

<span data-ttu-id="5ae2e-153">필요한 경우 다른 변환 모듈을 사용하여 데이터 테이블 형식을 다시 CSV, TSV, ARFF 또는 SVMLight 형식으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="5ae2e-154">모듈 팔레트의 **데이터 형식 변환** 섹션에서 이러한 함수를 수행하는 모듈을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5ae2e-154">Look in the **Data Format Conversions** section of the module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
