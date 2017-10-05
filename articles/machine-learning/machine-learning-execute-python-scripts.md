---
title: "Python Machine Learning 스크립트 실행 | Microsoft Docs"
description: "Azure 기계 학습에서 Python 스크립트를 지원하는 데 기본이 되는 디자인 원칙 및 기본 사용 시나리오, 기능 및 제한 사항을 간략히 설명합니다."
keywords: "python 기계 학습, pandas, python pandas, python 스크립트, python 스크립트 실행"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ee9eb764-0d3e-4104-a797-19fc29345d39
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bradsev
ms.openlocfilehash: e8d6377bc939e6711a96e521b5f574fc8d060929
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="execute-python-machine-learning-scripts-in-azure-machine-learning-studio"></a><span data-ttu-id="77e2e-104">Azure 기계 학습 스튜디오에서 Python 기계 학습 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="77e2e-104">Execute Python machine learning scripts in Azure Machine Learning Studio</span></span>

<span data-ttu-id="77e2e-105">이 항목에서는 Azure Machine Learning에서 현재 Python 스크립트를 지원하는 데 기본이 되는 디자인 원칙을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-105">This topic describes the design principles underlying the current support for Python scripts in Azure Machine Learning.</span></span> <span data-ttu-id="77e2e-106">다음을 비롯하여 제공되는 기본 기능도 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-106">The main capabilities provided are also outlined, including:</span></span>

- <span data-ttu-id="77e2e-107">기본 사용 시나리오 실행</span><span class="sxs-lookup"><span data-stu-id="77e2e-107">execute basic usage scenarios</span></span>
- <span data-ttu-id="77e2e-108">웹 서비스에서 실험 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="77e2e-108">score an experiment in a web service</span></span>
- <span data-ttu-id="77e2e-109">기존 코드 가져오기 지원</span><span class="sxs-lookup"><span data-stu-id="77e2e-109">support for importing existing code</span></span>
- <span data-ttu-id="77e2e-110">시각화 내보내기</span><span class="sxs-lookup"><span data-stu-id="77e2e-110">export visualizations</span></span>
- <span data-ttu-id="77e2e-111">감독 모드 기능 선택 수행</span><span class="sxs-lookup"><span data-stu-id="77e2e-111">perform supervised feature selection</span></span>
- <span data-ttu-id="77e2e-112">일부 제한 사항 파악</span><span class="sxs-lookup"><span data-stu-id="77e2e-112">understand some limitations</span></span>

<span data-ttu-id="77e2e-113">[Python](https://www.python.org/) 은 여러 데이터 과학자들의 도구 상자에 필수적인 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-113">[Python](https://www.python.org/) is an indispensable tool in the tool chest of many data scientists.</span></span> <span data-ttu-id="77e2e-114">여기에는:</span><span class="sxs-lookup"><span data-stu-id="77e2e-114">It has:</span></span>

* <span data-ttu-id="77e2e-115">세련되고 간결한 구문,</span><span class="sxs-lookup"><span data-stu-id="77e2e-115">an elegant and concise syntax,</span></span> 
* <span data-ttu-id="77e2e-116">플랫폼 간 지원,</span><span class="sxs-lookup"><span data-stu-id="77e2e-116">cross-platform support,</span></span> 
* <span data-ttu-id="77e2e-117">방대한 양의 강력한 라이브러리 컬렉션 및</span><span class="sxs-lookup"><span data-stu-id="77e2e-117">a vast collection of powerful libraries, and</span></span> 
* <span data-ttu-id="77e2e-118">완성도 있는 개발 도구가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-118">mature development tools.</span></span> 

<span data-ttu-id="77e2e-119">Python은 기계 학습 모델링에서 일반적으로 사용되는 워크플로의 다음과 같은 모든 단계에서 사용되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-119">Python is being used in all phases of a workflow typically used in machine learning modeling:</span></span>

- <span data-ttu-id="77e2e-120">데이터 수집 및 처리</span><span class="sxs-lookup"><span data-stu-id="77e2e-120">data ingest and processing</span></span> 
- <span data-ttu-id="77e2e-121">기능 생성</span><span class="sxs-lookup"><span data-stu-id="77e2e-121">feature construction</span></span>
- <span data-ttu-id="77e2e-122">모델 학습</span><span class="sxs-lookup"><span data-stu-id="77e2e-122">model training</span></span> 
- <span data-ttu-id="77e2e-123">모델 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="77e2e-123">model validation</span></span>
- <span data-ttu-id="77e2e-124">모델 배포</span><span class="sxs-lookup"><span data-stu-id="77e2e-124">deployment of the models</span></span>

<span data-ttu-id="77e2e-125">Azure Machine Learning Studio에서는 기계 학습 실험의 다양한 부분에 Python 스크립트를 포함할 수 있으며, 해당 스크립트를 Microsoft Azure의 웹 서비스로 원활하게 게시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-125">Azure Machine Learning Studio supports embedding Python scripts into various parts of a machine learning experiment and also seamlessly publishing them as web services on Microsoft Azure.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


## <a name="design-principles-of-python-scripts-in-machine-learning"></a><span data-ttu-id="77e2e-126">기계 학습에서 Python 스크립트의 디자인 원칙</span><span class="sxs-lookup"><span data-stu-id="77e2e-126">Design principles of Python scripts in Machine Learning</span></span>

<span data-ttu-id="77e2e-127">Azure 기계 학습 스튜디오에서 Python의 기본 인터페이스는 그림 1에 표시된 [Python 스크립트 실행][execute-python-script] 모듈을 통해 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-127">The primary interface to Python in Azure Machine Learning Studio is via the [Execute Python Script][execute-python-script] module shown in Figure 1.</span></span>

![image1](./media/machine-learning-execute-python-scripts/execute-machine-learning-python-scripts-module.png)

![image2](./media/machine-learning-execute-python-scripts/embedded-machine-learning-python-script.png)

<span data-ttu-id="77e2e-130">그림 1.</span><span class="sxs-lookup"><span data-stu-id="77e2e-130">Figure 1.</span></span> <span data-ttu-id="77e2e-131">**Python 스크립트 실행** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-131">The **Execute Python Script** module.</span></span>

<span data-ttu-id="77e2e-132">Azure ML Studio의 [Python 스크립트 실행][execute-python-script] 모듈에서는 R의 동일 모듈인 [R 스크립트 실행][execute-r-script] 모듈과 마찬가지로 최대 세 개의 입력을 허용하고 최대 두 개의 출력을 생성합니다(다음 섹션에서 설명함).</span><span class="sxs-lookup"><span data-stu-id="77e2e-132">The [Execute Python Script][execute-python-script] module in Azure ML Studio accepts up to three inputs and produces up to two outputs (discussed in the following section), like its R analogue, the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="77e2e-133">실행할 Python 코드는 `azureml_main`이라는 특별하게 명명된 진입점 함수로 매개 변수 상자에 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-133">The Python code to be executed is entered into the parameter box as a specially named entry-point function called `azureml_main`.</span></span> <span data-ttu-id="77e2e-134">다음은 이 모듈을 구현하는 데 사용하는 핵심 디자인 원칙입니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-134">Here are the key design principles used to implement this module:</span></span>

1. <span data-ttu-id="77e2e-135">*Python 사용자에게 자연스러워야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="77e2e-135">*Must be idiomatic for Python users.*</span></span> <span data-ttu-id="77e2e-136">대부분의 Python 사용자는 코드를 모듈 내의 함수로 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-136">Most Python users factor their code as functions inside modules.</span></span> <span data-ttu-id="77e2e-137">따라서 최상위 모듈에 실행 가능 문을 많이 포함하는 경우는 거의 없습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-137">So putting a lot of executable statements in a top-level module is relatively rare.</span></span> <span data-ttu-id="77e2e-138">따라서 스크립트 상자도 일련의 문장이 아니라 특별하게 명명된 Python 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-138">As a result, the script box also takes a specially named Python function as opposed to just a sequence of statements.</span></span> <span data-ttu-id="77e2e-139">함수에 노출된 개체는 [Pandas](http://pandas.pydata.org/) 데이터 프레임 및 [NumPy](http://www.numpy.org/) 배열과 같은 표준 Python 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-139">The objects exposed in the function are standard Python library types such as [Pandas](http://pandas.pydata.org/) data frames and [NumPy](http://www.numpy.org/) arrays.</span></span>
2. <span data-ttu-id="77e2e-140">*로컬 및 클라우드 실행 간의 충실도가 높아야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="77e2e-140">*Must have high-fidelity between local and cloud executions.*</span></span> <span data-ttu-id="77e2e-141">Python 코드를 실행하는 데 사용하는 백 엔드는 널리 사용되는 플랫폼 간 과학 Python 배포인 [Anaconda](https://store.continuum.io/cshop/anaconda/)를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-141">The backend used to execute the Python code is based on [Anaconda](https://store.continuum.io/cshop/anaconda/), a widely used cross-platform scientific Python distribution.</span></span> <span data-ttu-id="77e2e-142">가장 일반적인 Python 패키지가 거의 200개 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-142">It comes with close to 200 of the most common Python packages.</span></span> <span data-ttu-id="77e2e-143">따라서 데이터 과학자는 자신의 로컬 Azure Machine Learning 호환 Anaconda 환경에서 코드를 디버그하고 한정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-143">Therefore, data scientists can debug and qualify their code on their local Azure Machine Learning-compatible Anaconda environment.</span></span> <span data-ttu-id="77e2e-144">그런 후에 [IPython](http://ipython.org/) Notebook 또는 [Visual Studio용 Python 도구](http://aka.ms/ptvs)와 같은 기존 개발 환경을 사용하여 코드를 Azure ML 실험의 일부분으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-144">Then use an existing development environment, such as [IPython](http://ipython.org/) notebook or [Python Tools for Visual Studio](http://aka.ms/ptvs), to run it as part of an Azure ML experiment.</span></span> <span data-ttu-id="77e2e-145">`azureml_main` 진입점은 바닐라 Python 함수이며 Azure ML 관련 코드 또는 SDK가 설치되어 있지 않아도 ****작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-145">The `azureml_main` entry point is a vanilla Python function and so ****can be authored without Azure ML-specific code or the SDK installed.</span></span>
3. <span data-ttu-id="77e2e-146">*다른 Azure 기계 학습 모듈로 원활하게 구성할 수 있어야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="77e2e-146">*Must be seamlessly composable with other Azure Machine Learning modules.*</span></span> <span data-ttu-id="77e2e-147">[Python 스크립트 실행][execute-python-script] 모듈이 입력 및 출력으로 표준 Azure 기계 학습 데이터 집합을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-147">The [Execute Python Script][execute-python-script] module accepts, as inputs and outputs, standard Azure Machine Learning datasets.</span></span> <span data-ttu-id="77e2e-148">기본 프레임워크는 Azure ML 및 Python 런타임을 효율적이며 투명한 방식으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-148">The underlying framework transparently and efficiently bridges the Azure ML and Python runtimes.</span></span> <span data-ttu-id="77e2e-149">따라서 Python을 기존 Azure ML 워크플로(R 및 SQLite를 호출하는 워크플로 포함)와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-149">So Python can be used in conjunction with existing Azure ML workflows, including those that call into R and SQLite.</span></span> <span data-ttu-id="77e2e-150">이를 통해 데이터 과학자는 다음과 같은 워크플로를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-150">A  result, data scientist could compose workflows that:</span></span>
   * <span data-ttu-id="77e2e-151">데이터 전처리 및 정리에 Python 및 Pandas를 사용하는 워크플로</span><span class="sxs-lookup"><span data-stu-id="77e2e-151">use Python and Pandas for data pre-processing and cleaning</span></span>
   * <span data-ttu-id="77e2e-152">SQL 변환으로 데이터를 공급해 여러 데이터 집합을 연결하여 기능을 생성하는 워크플로</span><span class="sxs-lookup"><span data-stu-id="77e2e-152">feed the data to a SQL transformation, joining multiple datasets to form features</span></span>
   * <span data-ttu-id="77e2e-153">Azure 기계 학습의 알고리즘을 사용하여 모델 학습을 수행하는 워크플로</span><span class="sxs-lookup"><span data-stu-id="77e2e-153">train models using the algorithms in Azure Machine Learning</span></span> 
   * <span data-ttu-id="77e2e-154">R을 사용하여 결과 평가 및 사후 처리.</span><span class="sxs-lookup"><span data-stu-id="77e2e-154">evaluate and post-process the results using R.</span></span>


## <a name="basic-usage-scenarios-in-ml-for-python-scripts"></a><span data-ttu-id="77e2e-155">ML의 Python 스크립트 기본 사용 시나리오</span><span class="sxs-lookup"><span data-stu-id="77e2e-155">Basic usage scenarios in ML for Python scripts</span></span>

<span data-ttu-id="77e2e-156">이 섹션에서는 [Python 스크립트 실행][execute-python-script] 모듈의 몇 가지 기본 사용에 대해 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-156">In this section, we survey some of the basic uses of the [Execute Python Script][execute-python-script] module.</span></span> <span data-ttu-id="77e2e-157">Python 모듈에 입력하는 내용은 Pandas 데이터 프레임으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-157">Inputs to the Python module are exposed as Pandas data frames.</span></span> <span data-ttu-id="77e2e-158">이 함수는 튜플, 목록 또는 Numpy 배열과 같이 Python [시퀀스](https://docs.python.org/2/c-api/sequence.html) 내부에 패키지된 단일 Pandas 데이터 프레임을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-158">The function must return a single Pandas data frame packaged inside of a Python [sequence](https://docs.python.org/2/c-api/sequence.html) such as a tuple, list, or NumPy array.</span></span> <span data-ttu-id="77e2e-159">그러면 이 시퀀스의 첫 번째 요소가 모듈의 첫 번째 출력 포트에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-159">The first element of this sequence is then returned in the first output port of the module.</span></span> <span data-ttu-id="77e2e-160">이 스키마는 그림 2에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-160">This scheme is shown in Figure 2.</span></span>

![image3](./media/machine-learning-execute-python-scripts/map-of-python-script-inputs-outputs.png)

<span data-ttu-id="77e2e-162">그림 2.</span><span class="sxs-lookup"><span data-stu-id="77e2e-162">Figure 2.</span></span> <span data-ttu-id="77e2e-163">입력 포트를 매개 변수에 매핑 및 출력 포트에 값 반환.</span><span class="sxs-lookup"><span data-stu-id="77e2e-163">Mapping of input ports to parameters and return value to output port.</span></span>

<span data-ttu-id="77e2e-164">입력 포트가 `azureml_main` 함수에 매핑되는 방법에 대한 자세한 의미 체계는 표 1에 표시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-164">More detailed semantics of how the input ports get mapped to parameters of the `azureml_main` function are shown in Table 1:</span></span>

![image1T](./media/machine-learning-execute-python-scripts/python-script-inputs-mapped-to-parameters.png)

<span data-ttu-id="77e2e-166">표 1.</span><span class="sxs-lookup"><span data-stu-id="77e2e-166">Table 1.</span></span> <span data-ttu-id="77e2e-167">입력 포트를 함수 매개 변수에 매핑.</span><span class="sxs-lookup"><span data-stu-id="77e2e-167">Mapping of input ports to function parameters.</span></span>

<span data-ttu-id="77e2e-168">입력 포트와 함수 매개 변수 간의 매핑은 위치와 관련됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-168">The mapping between input ports and function parameters is positional:</span></span>

- <span data-ttu-id="77e2e-169">첫 번째로 연결된 입력 포트는 함수의 첫 번째 매개 변수에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-169">The first connected input port is mapped to the first parameter of the function.</span></span> 
- <span data-ttu-id="77e2e-170">두 번째 입력(연결된 경우)은 함수의 두 번째 매개 변수에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-170">The second input (if connected) is mapped to the second parameter of the function.</span></span>

<span data-ttu-id="77e2e-171">Python Pandas에 대한 자세한 내용 및 Python Pandas를 사용하여 효율적으로 데이터를 조작하는 방법은 W. McKinney의 저서 *Python for Data Analysis*(O'Reilly, 2012)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-171">See *Python for Data Analysis* (O'Reilly, 2012) by W. McKinney for more information on Python Pandas and on how it can be used to manipulate data effectively and efficiently.</span></span> 


## <a name="translation-of-input-and-output-types"></a><span data-ttu-id="77e2e-172">입력 및 출력 유형 변환</span><span class="sxs-lookup"><span data-stu-id="77e2e-172">Translation of input and output types</span></span> 
<span data-ttu-id="77e2e-173">Azure ML의 입력 데이터 집합은 Pandas에서 데이터 프레임으로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-173">Input datasets in Azure ML are converted to data frames in Pandas.</span></span> <span data-ttu-id="77e2e-174">출력 데이터 프레임은 Azure ML 데이터 집합으로 다시 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-174">Output data frames are converted back to Azure ML datasets.</span></span> <span data-ttu-id="77e2e-175">다음과 같은 변환이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-175">The following conversions are performed:</span></span>

1. <span data-ttu-id="77e2e-176">문자열과 숫자 열은 현상태 그대로 변환되고, 데이터 집합의 누락된 값은 Pandas에서 ‘NA’ 값으로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-176">String and numeric columns are converted as-is and missing values in a dataset are converted to ‘NA’ values in Pandas.</span></span> <span data-ttu-id="77e2e-177">그 반대의 경우에도 마찬가지로 변환됩니다(Pandas의 NA 값은 Azure ML의 누락된 값으로 변환됨).</span><span class="sxs-lookup"><span data-stu-id="77e2e-177">The same conversion happens on the way back (NA values in Pandas are converted to missing values in Azure ML).</span></span>
2. <span data-ttu-id="77e2e-178">Pandas의 인덱스 벡터는 Azure ML에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-178">Index vectors in Pandas are not supported in Azure ML.</span></span> <span data-ttu-id="77e2e-179">Python 함수의 모든 입력 데이터 프레임에는 항상 0부터 시작하여 행 수에서 1을 뺀 인덱스까지 64비트의 숫자 인덱스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-179">All input data frames in the Python function always have a 64-bit numerical index from 0 to the number of rows minus 1.</span></span> 
3. <span data-ttu-id="77e2e-180">Azure ML 데이터 집합에는 중복된 열 이름과 문자열이 아닌 열 이름이 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-180">Azure ML datasets cannot have duplicate column names and column names that are not strings.</span></span> <span data-ttu-id="77e2e-181">출력 데이터 프레임에 숫자가 아닌 열이 포함된 경우 프레임워크를 통해 해당 열에서 `str` 을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-181">If an output data frame contains non-numeric columns, the framework calls `str` on the column names.</span></span> <span data-ttu-id="77e2e-182">마찬가지로 중복된 모든 열 이름은 손상된 것으로 자동 처리하여 이름을 고유하게 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-182">Likewise, any duplicate column names are automatically mangled to insure the names are unique.</span></span> <span data-ttu-id="77e2e-183">접미사(2)는 첫 번째 중복 항목에 추가되고 (3)은 두 번째 중복 항목에 추가되는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-183">The suffix (2) is added to the first duplicate, (3) to the second duplicate, and so on.</span></span>


## <a name="operationalizing-python-scripts"></a><span data-ttu-id="77e2e-184">Python 스크립트 운영 가능화</span><span class="sxs-lookup"><span data-stu-id="77e2e-184">Operationalizing Python scripts</span></span>

<span data-ttu-id="77e2e-185">점수 매기기 실험에서 모든 [Python 스크립트 실행][execute-python-script] 모듈은 웹 서비스로 게시될 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-185">Any [Execute Python Script][execute-python-script] modules used in a scoring experiment are called when published as a web service.</span></span> <span data-ttu-id="77e2e-186">예를 들어 그림 3에서는 단일 Python 식을 평가하는 코드가 포함된 점수 매기기 실험을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-186">For example, Figure 3 shows a scoring experiment that contains the code to evaluate a single Python expression.</span></span> 

![image4](./media/machine-learning-execute-python-scripts/figure3a.png)

![image5](./media/machine-learning-execute-python-scripts/python-script-with-python-pandas.png)

<span data-ttu-id="77e2e-189">그림 3.</span><span class="sxs-lookup"><span data-stu-id="77e2e-189">Figure 3.</span></span> <span data-ttu-id="77e2e-190">Python 식을 평가하기 위한 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-190">Web service for evaluating a Python expression.</span></span>

<span data-ttu-id="77e2e-191">이 실험에서 작성된 웹 서비스는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-191">A web service created from this experiment:</span></span>

- <span data-ttu-id="77e2e-192">Python 식(문자열)을 입력으로 사용</span><span class="sxs-lookup"><span data-stu-id="77e2e-192">takes as input a Python expression (as a string)</span></span>
- <span data-ttu-id="77e2e-193">Python 인터프리터로 식 전송</span><span class="sxs-lookup"><span data-stu-id="77e2e-193">sends it to the Python interpreter</span></span> 
- <span data-ttu-id="77e2e-194">식과 계산된 결과가 모두 포함된 테이블 반환</span><span class="sxs-lookup"><span data-stu-id="77e2e-194">returns a table containing both the expression and the evaluated result.</span></span>


## <a name="importing-existing-python-script-modules"></a><span data-ttu-id="77e2e-195">기존 Python 스크립트 모듈 가져오기</span><span class="sxs-lookup"><span data-stu-id="77e2e-195">Importing existing Python script modules</span></span>

<span data-ttu-id="77e2e-196">대부분의 데이터 과학자들이 일반적으로 사용하는 사례는 기존 Python 스크립트를 Azure ML 실험으로 통합하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-196">A common use-case for many data scientists is to incorporate existing Python scripts into Azure ML experiments.</span></span> <span data-ttu-id="77e2e-197">모든 코드를 연결하여 단일 스크립트 상자에 붙여넣는 대신 [Python 스크립트 실행][execute-python-script] 모듈에서는 세 번째 입력 포트에서 Python 모듈을 포함하는 zip 파일을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-197">Instead of requiring that all code be concatenated and pasted into a single script box, the [Execute Python Script][execute-python-script] module accepts a zip file that contains Python modules at the third input port.</span></span> <span data-ttu-id="77e2e-198">이 파일은 런타임에 입력 프레임워크에서 압축이 풀리며, 파일의 내용은 Python 인터프리터의 라이브러리 경로에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-198">The file is unzipped by the execution framework at runtime and the contents are added to the library path of the Python interpreter.</span></span> <span data-ttu-id="77e2e-199">그러면 `azureml_main` 진입점 함수가 이러한 모듈을 직접 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-199">The `azureml_main` entry point function can then import these modules directly.</span></span>

<span data-ttu-id="77e2e-200">예를 들어, 간단한 “Hello, World” 함수를 포함하는 Hello.py라는 파일을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-200">As an example, consider the file Hello.py containing a simple “Hello, World” function.</span></span>

![image6](./media/machine-learning-execute-python-scripts/figure4.png)

<span data-ttu-id="77e2e-202">그림 4.</span><span class="sxs-lookup"><span data-stu-id="77e2e-202">Figure 4.</span></span> <span data-ttu-id="77e2e-203">Hello.py 파일의 사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="77e2e-203">User-defined function in Hello.py file.</span></span>

<span data-ttu-id="77e2e-204">다음으로 Hello.py을 포함하는 Hello.zip이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-204">Next, we create a file Hello.zip that contains Hello.py:</span></span>

![image7](./media/machine-learning-execute-python-scripts/figure5.png)

<span data-ttu-id="77e2e-206">그림 5.</span><span class="sxs-lookup"><span data-stu-id="77e2e-206">Figure 5.</span></span> <span data-ttu-id="77e2e-207">사용자 정의 Python 코드가 포함된 Zip 파일.</span><span class="sxs-lookup"><span data-stu-id="77e2e-207">Zip file containing user-defined Python code.</span></span>

<span data-ttu-id="77e2e-208">zip 파일을 데이터 집합으로 Azure Machine Learning Studio에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-208">Upload the zip file as a dataset into Azure Machine Learning Studio.</span></span> <span data-ttu-id="77e2e-209">그런 다음 이 그림에 표시된 대로 **Python 스크립트 실행** 모듈의 세 번째 입력 포트에 Hello.zip 파일을 연결하여 해당 파일에서 Python 코드를 사용하는 실험을 만들어서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-209">Then create and run an experiment that uses the Python code in the Hello.zip file by attaching it to the third input port of the **Execute Python Script** module, as shown in this figure.</span></span>

![image8](./media/machine-learning-execute-python-scripts/figure6a.png)

![image9](./media/machine-learning-execute-python-scripts/figure6b.png)

<span data-ttu-id="77e2e-212">그림 6.</span><span class="sxs-lookup"><span data-stu-id="77e2e-212">Figure 6.</span></span> <span data-ttu-id="77e2e-213">zip 파일로 업로드된 사용자 정의 Python 코드를 사용하는 샘플 실험.</span><span class="sxs-lookup"><span data-stu-id="77e2e-213">Sample experiment with user-defined Python code uploaded as a zip file.</span></span>

<span data-ttu-id="77e2e-214">모듈 출력에는 zip 파일의 패키지가 해제되었으며 `print_hello` 함수가 실행되었음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-214">The module output shows that the zip file has been unpackaged and that the function `print_hello` has been run.</span></span>
<span data-ttu-id="77e2e-215"> 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)</span><span class="sxs-lookup"><span data-stu-id="77e2e-215"> 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)</span></span>

<span data-ttu-id="77e2e-216">그림 7.</span><span class="sxs-lookup"><span data-stu-id="77e2e-216">Figure 7.</span></span> <span data-ttu-id="77e2e-217">[Python 스크립트 실행][execute-python-script] 모듈에서 사용 중인 사용자 정의 함수.</span><span class="sxs-lookup"><span data-stu-id="77e2e-217">User-defined function in use inside the [Execute Python Script][execute-python-script] module.</span></span>


## <a name="working-with-visualizations"></a><span data-ttu-id="77e2e-218">시각화 작업</span><span class="sxs-lookup"><span data-stu-id="77e2e-218">Working with visualizations</span></span>

<span data-ttu-id="77e2e-219">브라우저에서 시각화할 수 있는 MatplotLib를 사용하여 만든 그림은 [Python 스크립트 실행][execute-python-script]을 통해 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-219">Plots created using MatplotLib that can be visualized on the browser can be returned by the [Execute Python Script][execute-python-script].</span></span> <span data-ttu-id="77e2e-220">그러나 R을 사용할 때 그림은 현상태 그대로 이미지로 자동 리디렉션되므로, Azure 기계 학습으로 다시 반환하려는 경우 명시적으로 모든 그림을 PNG 파일로 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-220">But the plots are not automatically redirected to images as they are when using R. So the user must explicitly save any plots to PNG files if they are to be returned back to Azure Machine Learning.</span></span> 

<span data-ttu-id="77e2e-221">MatplotLib에서 이미지를 생성하려면 다음 절차를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-221">To generate images from MatplotLib, you must complete the following procedure:</span></span>

* <span data-ttu-id="77e2e-222">기본 Qt 기반 렌더러에서 “AGG”로 백 엔드 전환</span><span class="sxs-lookup"><span data-stu-id="77e2e-222">switch the backend to “AGG” from the default Qt-based renderer</span></span> 
* <span data-ttu-id="77e2e-223">새 그림 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="77e2e-223">create a new figure object</span></span> 
* <span data-ttu-id="77e2e-224">축을 가져오고 축에 모든 그림을 생성</span><span class="sxs-lookup"><span data-stu-id="77e2e-224">get the axis and generate all plots into it</span></span> 
* <span data-ttu-id="77e2e-225">PNG 파일에 그림 저장</span><span class="sxs-lookup"><span data-stu-id="77e2e-225">save the figure to a PNG file</span></span> 

<span data-ttu-id="77e2e-226">Pandas에서 scatter_matrix 함수를 사용하여 산점도 행렬을 생성하는 이 프로세스는 다음 그림 8에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-226">This process is illustrated in the following Figure 8 that creates a scatter plot matrix using the scatter_matrix function in Pandas.</span></span>

![image1v](./media/machine-learning-execute-python-scripts/figure-v1-8.png)

<span data-ttu-id="77e2e-228">그림 8.</span><span class="sxs-lookup"><span data-stu-id="77e2e-228">Figure 8.</span></span> <span data-ttu-id="77e2e-229">MatplotLib 그림을 이미지에 저장하기 위한 코드</span><span class="sxs-lookup"><span data-stu-id="77e2e-229">Code to save MatplotLib figures to images.</span></span>

<span data-ttu-id="77e2e-230">그림 9에서는 이전에 표시된 스크립트를 사용하여 두 번째 출력 포트를 통해 그림을 반환하는 실험을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-230">Figure 9 shows an experiment that uses the script shown previously to return plots via the second output port.</span></span>

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9a.png) 

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9b.png) 

<span data-ttu-id="77e2e-233">그림 9.</span><span class="sxs-lookup"><span data-stu-id="77e2e-233">Figure 9.</span></span> <span data-ttu-id="77e2e-234">Python 코드에서 생성된 그림 시각화.</span><span class="sxs-lookup"><span data-stu-id="77e2e-234">Visualizing plots generated from Python code.</span></span>

<span data-ttu-id="77e2e-235">여러 수치를 서로 다른 이미지에 저장하여 반환하고, Azure Machine Learning 런타임 시 모든 이미지를 선택한 다음, 시각화를 위해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-235">It is possible to return multiple figures by saving them into different images, the Azure Machine Learning runtime picks up all images and concatenates them for visualization.</span></span>


## <a name="advanced-examples"></a><span data-ttu-id="77e2e-236">고급 예제</span><span class="sxs-lookup"><span data-stu-id="77e2e-236">Advanced examples</span></span>

<span data-ttu-id="77e2e-237">Azure Machine Learning에서 설치되는 Anaconda 환경에는 NumPy, SciPy, Scikits-Learn 등의 일반 패키지가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-237">The Anaconda environment installed in Azure Machine Learning contains common packages such as NumPy, SciPy, and Scikits-Learn.</span></span> <span data-ttu-id="77e2e-238">이러한 패키지는 기계 학습 파이프라인의 여러 데이터 처리 작업에 효율적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-238">These packages can be effectively used for various data processing tasks in a machine learning pipeline.</span></span> <span data-ttu-id="77e2e-239">예를 들어 다음 실험과 스크립트에서는 데이터 집합의 기능 중요도 점수를 계산하기 위한 Scikits-Learn의 앙상블 학습자 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-239">As an example, the following experiment and script illustrate the use of ensemble learners in Scikits-Learn to compute feature importance scores for a dataset.</span></span> <span data-ttu-id="77e2e-240">점수는 다른 ML 모델에 공급하기 전에 감독 모드 기능 선택을 수행하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-240">The scores can be used to perform supervised feature selection before being fed into another ML model.</span></span>

<span data-ttu-id="77e2e-241">중요도 점수를 계산한 다음 이 점수에 따라 기능의 순서를 지정하는 데 사용되는 Python 함수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-241">Here is the Python function used to compute the importance scores and order the features based on the scores:</span></span>

![image11](./media/machine-learning-execute-python-scripts/figure8.png)

<span data-ttu-id="77e2e-243">그림 10.</span><span class="sxs-lookup"><span data-stu-id="77e2e-243">Figure 10.</span></span> <span data-ttu-id="77e2e-244">점수별로 기능의 순위를 지정하는 기능.</span><span class="sxs-lookup"><span data-stu-id="77e2e-244">Function to rank features by scores.</span></span>
<span data-ttu-id="77e2e-245">  다음 실험에서는 Azure Machine Learning의 “Pima Indian Diabetes” 데이터 집합에 있는 기능의 중요도 점수를 계산하여 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-245">  The following experiment then computes and returns the importance scores of features in the “Pima Indian Diabetes” dataset in Azure Machine Learning:</span></span>

<span data-ttu-id="77e2e-246">![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)</span><span class="sxs-lookup"><span data-stu-id="77e2e-246">![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)</span></span>    

<span data-ttu-id="77e2e-247">그림 11.</span><span class="sxs-lookup"><span data-stu-id="77e2e-247">Figure 11.</span></span> <span data-ttu-id="77e2e-248">Pima Indian Diabetes 데이터 집합에서 기능의 순위를 지정하는 실험.</span><span class="sxs-lookup"><span data-stu-id="77e2e-248">Experiment to rank features in the Pima Indian Diabetes dataset.</span></span>

## <a name="limitations"></a><span data-ttu-id="77e2e-249">제한 사항</span><span class="sxs-lookup"><span data-stu-id="77e2e-249">Limitations</span></span>
<span data-ttu-id="77e2e-250">[Python 스크립트 실행][execute-python-script]에는 현재 다음과 같은 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-250">The [Execute Python Script][execute-python-script] currently has the following limitations:</span></span>

1. <span data-ttu-id="77e2e-251">*샌드박스 실행.*</span><span class="sxs-lookup"><span data-stu-id="77e2e-251">*Sandboxed execution.*</span></span> <span data-ttu-id="77e2e-252">현재 Python 런타임은 샌드박스로 작동하므로, 지속적인 방식으로 네트워크나 로컬 파일 시스템에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-252">The Python runtime is currently sandboxed and, as a result, does not allow access to the network or to the local file system in a persistent manner.</span></span> <span data-ttu-id="77e2e-253">모듈이 완료되면 로컬에 저장된 모든 파일이 격리되어 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-253">All files saved locally are isolated and deleted once the module finishes.</span></span> <span data-ttu-id="77e2e-254">Python 코드는 현재 디렉터리와 하위 디렉터리를 제외하고, 코드가 실행되는 컴퓨터에 있는 대부분의 디렉터리에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-254">The Python code cannot access most directories on the machine it runs on, the exception being the current directory and its subdirectories.</span></span>
2. <span data-ttu-id="77e2e-255">*정교한 개발 및 디버깅 지원이 부족합니다.*</span><span class="sxs-lookup"><span data-stu-id="77e2e-255">*Lack of sophisticated development and debugging support.*</span></span> <span data-ttu-id="77e2e-256">현재 Python 모듈에서는 Intellisense와 디버깅 같은 IDE 기능을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-256">The Python module currently does not support IDE features such as intellisense and debugging.</span></span> <span data-ttu-id="77e2e-257">또한 모듈이 런타임에서 실패하는 경우 전체 Python 스택 추적을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-257">Also, if the module fails at runtime, the full Python stack trace is available.</span></span> <span data-ttu-id="77e2e-258">그러나 스택 추적은 모듈의 출력 로그에서 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-258">But it must be viewed in the output log for the module.</span></span> <span data-ttu-id="77e2e-259">현재로서는 IPython과 같은 환경에서 Python 스크립트를 개발하고 디버그한 다음 모듈에 코드를 가져오는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-259">We currently recommend that you develop and debug Python scripts in an environment such as IPython and then import the code into the module.</span></span>
3. <span data-ttu-id="77e2e-260">*단일 데이터 프레임 출력.*</span><span class="sxs-lookup"><span data-stu-id="77e2e-260">*Single data frame output.*</span></span> <span data-ttu-id="77e2e-261">Python 진입점은 단일 데이터 프레임을 출력으로 반환할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-261">The Python entry point is only permitted to return a single data frame as output.</span></span> <span data-ttu-id="77e2e-262">현재로서는 학습된 모델과 같은 임의의 Python 개체를 Azure 기계 학습 런타임에 직접 반환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-262">It is not currently possible to return arbitrary Python objects such as trained models directly back to the Azure Machine Learning runtime.</span></span> <span data-ttu-id="77e2e-263">동일한 제한 사항이 있는 [R 스크립트 실행][execute-r-script]과 마찬가지로, 대부분의 경우 개체를 바이트 배열로 만든 다음 데이터 프레임 내부에서 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-263">Like [Execute R Script][execute-r-script], which has the same limitation, it is possible in many cases to pickle objects into a byte array and then return that inside of a data frame.</span></span>
4. <span data-ttu-id="77e2e-264">*Python 설치를 사용자 지정할 수 없음*.</span><span class="sxs-lookup"><span data-stu-id="77e2e-264">*Inability to customize Python installation*.</span></span> <span data-ttu-id="77e2e-265">현재 사용자 지정 Python 모듈을 추가하는 유일한 방법은 이전에 설명한 zip 파일 메커니즘을 통한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-265">Currently, the only way to add custom Python modules is via the zip file mechanism described earlier.</span></span> <span data-ttu-id="77e2e-266">이 방법은 작은 모듈의 경우 가능하지만, 모듈이 크거나(특히 네이티브 DLL이 있는 모듈) 모듈 수가 많은 경우 번거로울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-266">While this is feasible for small modules, it is cumbersome for large modules (especially those with native DLLs) or a large number of modules.</span></span> 

## <a name="conclusions"></a><span data-ttu-id="77e2e-267">결론</span><span class="sxs-lookup"><span data-stu-id="77e2e-267">Conclusions</span></span>
<span data-ttu-id="77e2e-268">데이터 과학자가 [Python 스크립트 실행][execute-python-script] 모듈을 사용하여 Azure 기계 학습의 클라우드 호스팅 기계 학습 워크플로에 기존 Python 코드를 통합하고 웹 서비스의 일부로 원활하게 운영할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-268">The [Execute Python Script][execute-python-script] module allows a data scientist to incorporate existing Python code into cloud-hosted machine learning workflows in Azure Machine Learning and to seamlessly operationalize them as part of a web service.</span></span> <span data-ttu-id="77e2e-269">Python 스크립트 모듈은 Azure Machine Learning의 다른 모듈과 자연스럽게 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-269">The Python script module interoperates naturally with other modules in Azure Machine Learning.</span></span> <span data-ttu-id="77e2e-270">이 모듈은 데이터 탐색, 전처리, 기능 추출에서 결과 평가 및 후처리에 이르기까지 폭넓은 작업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-270">The module can be used for a range of tasks from data exploration to pre-processing and feature extraction, and then to evaluation and post-processing of the results.</span></span> <span data-ttu-id="77e2e-271">실행에 사용되는 백 엔드 런타임은 충분히 테스트되어 널리 사용되는 Python 배포인 Anaconda를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-271">The backend runtime used for execution is based on Anaconda, a well-tested and widely used Python distribution.</span></span> <span data-ttu-id="77e2e-272">이 백 엔드를 사용하면 기존 코드 자산을 클라우드에 간편하게 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-272">This backend makes it simple for you to on-board existing code assets into the cloud.</span></span>

<span data-ttu-id="77e2e-273">[Python 스크립트 실행][execute-python-script] 모듈에 추가 기능(예: Python의 모듈을 학습하고 운영화하는 기능 및 Azure Machine Learning Studio에서의 코드 개발 및 디버깅 지원 향상)을 제공할 것으로 기대합니다.</span><span class="sxs-lookup"><span data-stu-id="77e2e-273">We expect to provide additional functionality to the [Execute Python Script][execute-python-script] module such as the ability to train and operationalize models in Python and to add better support for the development and debugging code in Azure Machine Learning Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77e2e-274">다음 단계</span><span class="sxs-lookup"><span data-stu-id="77e2e-274">Next steps</span></span>
<span data-ttu-id="77e2e-275">자세한 내용은 [Python 개발자 센터](https://azure.microsoft.com/develop/python/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77e2e-275">For more information, see the [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span>

<!-- Module References -->
[execute-python-script]: https://msdn.microsoft.com/library/azure/cdb56f95-7f4c-404d-bde7-5bb972e6f232/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
