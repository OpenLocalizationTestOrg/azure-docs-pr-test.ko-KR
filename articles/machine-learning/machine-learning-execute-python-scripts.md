---
title: "학습 스크립트 aaaExecute Python 컴퓨터 | Microsoft Docs"
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
ms.openlocfilehash: 8d23aaa972a46cb1a07ea0f18cc1e24933fe3e6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="execute-python-machine-learning-scripts-in-azure-machine-learning-studio"></a><span data-ttu-id="375b5-104">Azure 기계 학습 스튜디오에서 Python 기계 학습 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="375b5-104">Execute Python machine learning scripts in Azure Machine Learning Studio</span></span>

<span data-ttu-id="375b5-105">이 항목에서는 hello 현재 Azure 기계 학습에서 Python 스크립트 지원 기본 hello 디자인 원칙을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-105">This topic describes hello design principles underlying hello current support for Python scripts in Azure Machine Learning.</span></span> <span data-ttu-id="375b5-106">제공 하는 hello 주 기능도 요약 되어 포함 하 여:</span><span class="sxs-lookup"><span data-stu-id="375b5-106">hello main capabilities provided are also outlined, including:</span></span>

- <span data-ttu-id="375b5-107">기본 사용 시나리오 실행</span><span class="sxs-lookup"><span data-stu-id="375b5-107">execute basic usage scenarios</span></span>
- <span data-ttu-id="375b5-108">웹 서비스에서 실험 점수 매기기</span><span class="sxs-lookup"><span data-stu-id="375b5-108">score an experiment in a web service</span></span>
- <span data-ttu-id="375b5-109">기존 코드 가져오기 지원</span><span class="sxs-lookup"><span data-stu-id="375b5-109">support for importing existing code</span></span>
- <span data-ttu-id="375b5-110">시각화 내보내기</span><span class="sxs-lookup"><span data-stu-id="375b5-110">export visualizations</span></span>
- <span data-ttu-id="375b5-111">감독 모드 기능 선택 수행</span><span class="sxs-lookup"><span data-stu-id="375b5-111">perform supervised feature selection</span></span>
- <span data-ttu-id="375b5-112">일부 제한 사항 파악</span><span class="sxs-lookup"><span data-stu-id="375b5-112">understand some limitations</span></span>

<span data-ttu-id="375b5-113">[Python](https://www.python.org/) 는 대부분 데이터 과학자의 hello 도구 상자에 필수적인 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-113">[Python](https://www.python.org/) is an indispensable tool in hello tool chest of many data scientists.</span></span> <span data-ttu-id="375b5-114">여기에는:</span><span class="sxs-lookup"><span data-stu-id="375b5-114">It has:</span></span>

* <span data-ttu-id="375b5-115">세련되고 간결한 구문,</span><span class="sxs-lookup"><span data-stu-id="375b5-115">an elegant and concise syntax,</span></span> 
* <span data-ttu-id="375b5-116">플랫폼 간 지원,</span><span class="sxs-lookup"><span data-stu-id="375b5-116">cross-platform support,</span></span> 
* <span data-ttu-id="375b5-117">방대한 양의 강력한 라이브러리 컬렉션 및</span><span class="sxs-lookup"><span data-stu-id="375b5-117">a vast collection of powerful libraries, and</span></span> 
* <span data-ttu-id="375b5-118">완성도 있는 개발 도구가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-118">mature development tools.</span></span> 

<span data-ttu-id="375b5-119">Python은 기계 학습 모델링에서 일반적으로 사용되는 워크플로의 다음과 같은 모든 단계에서 사용되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-119">Python is being used in all phases of a workflow typically used in machine learning modeling:</span></span>

- <span data-ttu-id="375b5-120">데이터 수집 및 처리</span><span class="sxs-lookup"><span data-stu-id="375b5-120">data ingest and processing</span></span> 
- <span data-ttu-id="375b5-121">기능 생성</span><span class="sxs-lookup"><span data-stu-id="375b5-121">feature construction</span></span>
- <span data-ttu-id="375b5-122">모델 학습</span><span class="sxs-lookup"><span data-stu-id="375b5-122">model training</span></span> 
- <span data-ttu-id="375b5-123">모델 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="375b5-123">model validation</span></span>
- <span data-ttu-id="375b5-124">hello 모델 배포</span><span class="sxs-lookup"><span data-stu-id="375b5-124">deployment of hello models</span></span>

<span data-ttu-id="375b5-125">Azure Machine Learning Studio에서는 기계 학습 실험의 다양한 부분에 Python 스크립트를 포함할 수 있으며, 해당 스크립트를 Microsoft Azure의 웹 서비스로 원활하게 게시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-125">Azure Machine Learning Studio supports embedding Python scripts into various parts of a machine learning experiment and also seamlessly publishing them as web services on Microsoft Azure.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


## <a name="design-principles-of-python-scripts-in-machine-learning"></a><span data-ttu-id="375b5-126">기계 학습에서 Python 스크립트의 디자인 원칙</span><span class="sxs-lookup"><span data-stu-id="375b5-126">Design principles of Python scripts in Machine Learning</span></span>

<span data-ttu-id="375b5-127">Azure 기계 학습 스튜디오의 기본 인터페이스 tooPython hello는 hello를 통해 [Python 스크립트 실행] [ execute-python-script] 그림 1에 표시 된 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-127">hello primary interface tooPython in Azure Machine Learning Studio is via hello [Execute Python Script][execute-python-script] module shown in Figure 1.</span></span>

![image1](./media/machine-learning-execute-python-scripts/execute-machine-learning-python-scripts-module.png)

![image2](./media/machine-learning-execute-python-scripts/embedded-machine-learning-python-script.png)

<span data-ttu-id="375b5-130">그림 1.</span><span class="sxs-lookup"><span data-stu-id="375b5-130">Figure 1.</span></span> <span data-ttu-id="375b5-131">hello **Python 스크립트 실행** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-131">hello **Execute Python Script** module.</span></span>

<span data-ttu-id="375b5-132">hello [Python 스크립트 실행] [ execute-python-script] Azure 기계 학습 스튜디오의 모듈 toothree 입력을 허용 하 고 생성 tootwo 출력 (hello 다음 섹션에서에서 설명)를 해당 R 아날로그 같은 hello [ R 스크립트 실행] [ execute-r-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-132">hello [Execute Python Script][execute-python-script] module in Azure ML Studio accepts up toothree inputs and produces up tootwo outputs (discussed in hello following section), like its R analogue, hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="375b5-133">hello 실행할 Python 코드 toobe에 입력 된 특수 이라고 명명 된 매개 변수 상자 hello 진입점 함수를 호출 `azureml_main`합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-133">hello Python code toobe executed is entered into hello parameter box as a specially named entry-point function called `azureml_main`.</span></span> <span data-ttu-id="375b5-134">다음은 원칙 tooimplement이이 모듈을 사용 하는 hello 주요 디자인이입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-134">Here are hello key design principles used tooimplement this module:</span></span>

1. <span data-ttu-id="375b5-135">*Python 사용자에게 자연스러워야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="375b5-135">*Must be idiomatic for Python users.*</span></span> <span data-ttu-id="375b5-136">대부분의 Python 사용자는 코드를 모듈 내의 함수로 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-136">Most Python users factor their code as functions inside modules.</span></span> <span data-ttu-id="375b5-137">따라서 최상위 모듈에 실행 가능 문을 많이 포함하는 경우는 거의 없습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-137">So putting a lot of executable statements in a top-level module is relatively rare.</span></span> <span data-ttu-id="375b5-138">결과적으로, hello 스크립트 상자도 특별 하 게 명명 된 Python 함수 변수로 사용 것과 반대로 toojust 문의 시퀀스를 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-138">As a result, hello script box also takes a specially named Python function as opposed toojust a sequence of statements.</span></span> <span data-ttu-id="375b5-139">hello hello 함수에서 제공 하는 개체 유형이 표준 Python 라이브러리와 같은 [팬더](http://pandas.pydata.org/) 데이터 프레임 및 [NumPy](http://www.numpy.org/) 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-139">hello objects exposed in hello function are standard Python library types such as [Pandas](http://pandas.pydata.org/) data frames and [NumPy](http://www.numpy.org/) arrays.</span></span>
2. <span data-ttu-id="375b5-140">*로컬 및 클라우드 실행 간의 충실도가 높아야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="375b5-140">*Must have high-fidelity between local and cloud executions.*</span></span> <span data-ttu-id="375b5-141">hello 사용 되는 백 엔드 tooexecute hello Python 코드 기반 [Anaconda](https://store.continuum.io/cshop/anaconda/), 광범위 하 게 플랫폼 간 과학 Python 배포를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-141">hello backend used tooexecute hello Python code is based on [Anaconda](https://store.continuum.io/cshop/anaconda/), a widely used cross-platform scientific Python distribution.</span></span> <span data-ttu-id="375b5-142">가장 일반적인 Python 패키지 hello 닫기 too200 함께 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-142">It comes with close too200 of hello most common Python packages.</span></span> <span data-ttu-id="375b5-143">따라서 데이터 과학자는 자신의 로컬 Azure Machine Learning 호환 Anaconda 환경에서 코드를 디버그하고 한정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-143">Therefore, data scientists can debug and qualify their code on their local Azure Machine Learning-compatible Anaconda environment.</span></span> <span data-ttu-id="375b5-144">그런 다음 기존 개발 환경와 같은 사용 [IPython](http://ipython.org/) 노트북 또는 [Python Tools for Visual Studio](http://aka.ms/ptvs), toorun Azure ML 실험의 일환으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-144">Then use an existing development environment, such as [IPython](http://ipython.org/) notebook or [Python Tools for Visual Studio](http://aka.ms/ptvs), toorun it as part of an Azure ML experiment.</span></span> <span data-ttu-id="375b5-145">hello `azureml_main` 바닐라 Python 함수 등 진입점은 * * * SDK가 설치 되어 hello 또는 Azure ML 관련 코드 없이 작성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-145">hello `azureml_main` entry point is a vanilla Python function and so ****can be authored without Azure ML-specific code or hello SDK installed.</span></span>
3. <span data-ttu-id="375b5-146">*다른 Azure 기계 학습 모듈로 원활하게 구성할 수 있어야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="375b5-146">*Must be seamlessly composable with other Azure Machine Learning modules.*</span></span> <span data-ttu-id="375b5-147">hello [Python 스크립트 실행] [ execute-python-script] 모듈에서는 입력 및 출력,으로 표준 Azure 기계 학습 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-147">hello [Execute Python Script][execute-python-script] module accepts, as inputs and outputs, standard Azure Machine Learning datasets.</span></span> <span data-ttu-id="375b5-148">투명 하 고 효율적으로 hello 기본 프레임 워크는 hello Azure ML 및 Python 런타임은 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-148">hello underlying framework transparently and efficiently bridges hello Azure ML and Python runtimes.</span></span> <span data-ttu-id="375b5-149">따라서 Python을 기존 Azure ML 워크플로(R 및 SQLite를 호출하는 워크플로 포함)와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-149">So Python can be used in conjunction with existing Azure ML workflows, including those that call into R and SQLite.</span></span> <span data-ttu-id="375b5-150">이를 통해 데이터 과학자는 다음과 같은 워크플로를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-150">A  result, data scientist could compose workflows that:</span></span>
   * <span data-ttu-id="375b5-151">데이터 전처리 및 정리에 Python 및 Pandas를 사용하는 워크플로</span><span class="sxs-lookup"><span data-stu-id="375b5-151">use Python and Pandas for data pre-processing and cleaning</span></span>
   * <span data-ttu-id="375b5-152">피드 hello 데이터 tooa SQL 변환, 여러 데이터 집합 tooform 기능 조인</span><span class="sxs-lookup"><span data-stu-id="375b5-152">feed hello data tooa SQL transformation, joining multiple datasets tooform features</span></span>
   * <span data-ttu-id="375b5-153">hello 알고리즘을 사용 하 여 Azure 기계 학습에서 모델을 학습 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-153">train models using hello algorithms in Azure Machine Learning</span></span> 
   * <span data-ttu-id="375b5-154">평가 하 고 오른쪽을 사용 하 여 hello 결과 한 후 처리</span><span class="sxs-lookup"><span data-stu-id="375b5-154">evaluate and post-process hello results using R.</span></span>


## <a name="basic-usage-scenarios-in-ml-for-python-scripts"></a><span data-ttu-id="375b5-155">ML의 Python 스크립트 기본 사용 시나리오</span><span class="sxs-lookup"><span data-stu-id="375b5-155">Basic usage scenarios in ML for Python scripts</span></span>

<span data-ttu-id="375b5-156">이 섹션에서는 설문 조사 hello의 기본 용도 hello에 [Python 스크립트 실행] [ execute-python-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-156">In this section, we survey some of hello basic uses of hello [Execute Python Script][execute-python-script] module.</span></span> <span data-ttu-id="375b5-157">입력 toohello Python 모듈 팬더 데이터 프레임으로 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-157">Inputs toohello Python module are exposed as Pandas data frames.</span></span> <span data-ttu-id="375b5-158">hello 함수 반환 해야 합니다는 Python 안에 패키징된 단일 팬더 데이터 프레임 [시퀀스](https://docs.python.org/2/c-api/sequence.html) 튜플, 목록 또는 배열 NumPy 등입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-158">hello function must return a single Pandas data frame packaged inside of a Python [sequence](https://docs.python.org/2/c-api/sequence.html) such as a tuple, list, or NumPy array.</span></span> <span data-ttu-id="375b5-159">이 시퀀스의 첫 번째 요소 hello는 hello hello 모듈의 첫 번째 출력 포트에 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-159">hello first element of this sequence is then returned in hello first output port of hello module.</span></span> <span data-ttu-id="375b5-160">이 스키마는 그림 2에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-160">This scheme is shown in Figure 2.</span></span>

![image3](./media/machine-learning-execute-python-scripts/map-of-python-script-inputs-outputs.png)

<span data-ttu-id="375b5-162">그림 2.</span><span class="sxs-lookup"><span data-stu-id="375b5-162">Figure 2.</span></span> <span data-ttu-id="375b5-163">매핑 포트 tooparameters 입력과 toooutput 포트 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-163">Mapping of input ports tooparameters and return value toooutput port.</span></span>

<span data-ttu-id="375b5-164">더 자세한 hello 입력된 포트의 hello 매핑된 tooparameters를 얻는 방법의 의미 체계 `azureml_main` 함수 표 1에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-164">More detailed semantics of how hello input ports get mapped tooparameters of hello `azureml_main` function are shown in Table 1:</span></span>

![image1T](./media/machine-learning-execute-python-scripts/python-script-inputs-mapped-to-parameters.png)

<span data-ttu-id="375b5-166">표 1.</span><span class="sxs-lookup"><span data-stu-id="375b5-166">Table 1.</span></span> <span data-ttu-id="375b5-167">입력된 포트 toofunction 매개 변수 매핑이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-167">Mapping of input ports toofunction parameters.</span></span>

<span data-ttu-id="375b5-168">hello 매핑 입력된 포트 사이의 함수 매개 변수는 위치:</span><span class="sxs-lookup"><span data-stu-id="375b5-168">hello mapping between input ports and function parameters is positional:</span></span>

- <span data-ttu-id="375b5-169">hello 첫 번째 연결 된 입력된 포트는 매핑된 toohello hello 함수의 첫 번째 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-169">hello first connected input port is mapped toohello first parameter of hello function.</span></span> 
- <span data-ttu-id="375b5-170">hello (연결) 하는 경우 두 번째 입력은 매핑된 toohello hello 함수의 두 번째 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-170">hello second input (if connected) is mapped toohello second parameter of hello function.</span></span>

<span data-ttu-id="375b5-171">참조 *데이터 분석에 대 한 Python* (2012 O'Reilly) 여 서 McKinney 효과적이 고 효율적으로 사용 되는 toomanipulate 데이터 수 있습니다 어떻게 및 Python 팬더에 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-171">See *Python for Data Analysis* (O'Reilly, 2012) by W. McKinney for more information on Python Pandas and on how it can be used toomanipulate data effectively and efficiently.</span></span> 


## <a name="translation-of-input-and-output-types"></a><span data-ttu-id="375b5-172">입력 및 출력 유형 변환</span><span class="sxs-lookup"><span data-stu-id="375b5-172">Translation of input and output types</span></span> 
<span data-ttu-id="375b5-173">Azure 기계 학습에서 입력된 데이터 집합은 팬더에서 변환 된 toodata 프레임입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-173">Input datasets in Azure ML are converted toodata frames in Pandas.</span></span> <span data-ttu-id="375b5-174">출력 데이터 프레임 백 tooAzure 기계 학습 데이터 집합을 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-174">Output data frames are converted back tooAzure ML datasets.</span></span> <span data-ttu-id="375b5-175">변환을 수행 하는 hello 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-175">hello following conversions are performed:</span></span>

1. <span data-ttu-id="375b5-176">문자열 및 숫자 열으로 변환 됩니다-이 데이터 집합에서 누락 된 값은 변환 된 too'NA' 팬더의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-176">String and numeric columns are converted as-is and missing values in a dataset are converted too‘NA’ values in Pandas.</span></span> <span data-ttu-id="375b5-177">hello 동일한 변환이 발생 하는 방식으로 다시 hello에 (팬더에 NA 값은 Azure ML에서 변환 된 toomissing 값).</span><span class="sxs-lookup"><span data-stu-id="375b5-177">hello same conversion happens on hello way back (NA values in Pandas are converted toomissing values in Azure ML).</span></span>
2. <span data-ttu-id="375b5-178">Pandas의 인덱스 벡터는 Azure ML에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-178">Index vectors in Pandas are not supported in Azure ML.</span></span> <span data-ttu-id="375b5-179">모든 입력된 데이터 프레임 hello Python 함수에는 항상 0 toohello 행 수-1에서에서 64 비트 숫자 인덱스를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-179">All input data frames in hello Python function always have a 64-bit numerical index from 0 toohello number of rows minus 1.</span></span> 
3. <span data-ttu-id="375b5-180">Azure ML 데이터 집합에는 중복된 열 이름과 문자열이 아닌 열 이름이 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-180">Azure ML datasets cannot have duplicate column names and column names that are not strings.</span></span> <span data-ttu-id="375b5-181">출력 데이터 프레임에 숫자가 아닌 열이 포함 된 경우 프레임 워크 호출 hello `str` hello 열 이름에서.</span><span class="sxs-lookup"><span data-stu-id="375b5-181">If an output data frame contains non-numeric columns, hello framework calls `str` on hello column names.</span></span> <span data-ttu-id="375b5-182">마찬가지로, 자동으로 바뀐된 tooinsure는 모든 중복 열 이름을 hello 이름이 고유한 지 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-182">Likewise, any duplicate column names are automatically mangled tooinsure hello names are unique.</span></span> <span data-ttu-id="375b5-183">hello 접미사 (2) toohello 첫 번째 중복, (3) toohello 두 번째 중복 및에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-183">hello suffix (2) is added toohello first duplicate, (3) toohello second duplicate, and so on.</span></span>


## <a name="operationalizing-python-scripts"></a><span data-ttu-id="375b5-184">Python 스크립트 운영 가능화</span><span class="sxs-lookup"><span data-stu-id="375b5-184">Operationalizing Python scripts</span></span>

<span data-ttu-id="375b5-185">점수 매기기 실험에서 모든 [Python 스크립트 실행][execute-python-script] 모듈은 웹 서비스로 게시될 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-185">Any [Execute Python Script][execute-python-script] modules used in a scoring experiment are called when published as a web service.</span></span> <span data-ttu-id="375b5-186">예를 들어 그림 3은 hello 코드 tooevaluate 단일 Python 식을 포함 하는 점수 매기기 실험을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-186">For example, Figure 3 shows a scoring experiment that contains hello code tooevaluate a single Python expression.</span></span> 

![image4](./media/machine-learning-execute-python-scripts/figure3a.png)

![image5](./media/machine-learning-execute-python-scripts/python-script-with-python-pandas.png)

<span data-ttu-id="375b5-189">그림 3.</span><span class="sxs-lookup"><span data-stu-id="375b5-189">Figure 3.</span></span> <span data-ttu-id="375b5-190">Python 식을 평가하기 위한 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-190">Web service for evaluating a Python expression.</span></span>

<span data-ttu-id="375b5-191">이 실험에서 작성된 웹 서비스는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-191">A web service created from this experiment:</span></span>

- <span data-ttu-id="375b5-192">Python 식(문자열)을 입력으로 사용</span><span class="sxs-lookup"><span data-stu-id="375b5-192">takes as input a Python expression (as a string)</span></span>
- <span data-ttu-id="375b5-193">toohello Python 인터프리터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-193">sends it toohello Python interpreter</span></span> 
- <span data-ttu-id="375b5-194">hello 식과 hello 평가 결과 모두 포함 하는 테이블을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-194">returns a table containing both hello expression and hello evaluated result.</span></span>


## <a name="importing-existing-python-script-modules"></a><span data-ttu-id="375b5-195">기존 Python 스크립트 모듈 가져오기</span><span class="sxs-lookup"><span data-stu-id="375b5-195">Importing existing Python script modules</span></span>

<span data-ttu-id="375b5-196">대부분 데이터 과학자에 대 한 일반적인 사용 사례 tooincorporate Azure 기계 학습 실험에 기존 Python 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-196">A common use-case for many data scientists is tooincorporate existing Python scripts into Azure ML experiments.</span></span> <span data-ttu-id="375b5-197">모든 코드를 연결 하 고 단일 스크립트 상자에 붙여넣을 수 않아도 hello [Python 스크립트 실행] [ execute-python-script] 모듈 hello 세 번째 입력 포트 Python 모듈을 포함 하는 zip 파일을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-197">Instead of requiring that all code be concatenated and pasted into a single script box, hello [Execute Python Script][execute-python-script] module accepts a zip file that contains Python modules at hello third input port.</span></span> <span data-ttu-id="375b5-198">런타임 시 hello 실행 프레임 워크에 의해 hello 파일 압축을 푼 및 hello 내용이 hello Python 인터프리터의 toohello 라이브러리 경로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-198">hello file is unzipped by hello execution framework at runtime and hello contents are added toohello library path of hello Python interpreter.</span></span> <span data-ttu-id="375b5-199">hello `azureml_main` 진입점 함수 이러한 모듈을 직접 가져올 다음 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-199">hello `azureml_main` entry point function can then import these modules directly.</span></span>

<span data-ttu-id="375b5-200">예를 들어 hello 파일을 Hello.py 간단한 "Hello, World" 함수를 포함 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-200">As an example, consider hello file Hello.py containing a simple “Hello, World” function.</span></span>

![image6](./media/machine-learning-execute-python-scripts/figure4.png)

<span data-ttu-id="375b5-202">그림 4.</span><span class="sxs-lookup"><span data-stu-id="375b5-202">Figure 4.</span></span> <span data-ttu-id="375b5-203">Hello.py 파일의 사용자 정의 함수</span><span class="sxs-lookup"><span data-stu-id="375b5-203">User-defined function in Hello.py file.</span></span>

<span data-ttu-id="375b5-204">다음으로 Hello.py을 포함하는 Hello.zip이라는 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-204">Next, we create a file Hello.zip that contains Hello.py:</span></span>

![image7](./media/machine-learning-execute-python-scripts/figure5.png)

<span data-ttu-id="375b5-206">그림 5.</span><span class="sxs-lookup"><span data-stu-id="375b5-206">Figure 5.</span></span> <span data-ttu-id="375b5-207">사용자 정의 Python 코드가 포함된 Zip 파일.</span><span class="sxs-lookup"><span data-stu-id="375b5-207">Zip file containing user-defined Python code.</span></span>

<span data-ttu-id="375b5-208">Azure 기계 학습 스튜디오에 데이터 집합으로 hello zip 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-208">Upload hello zip file as a dataset into Azure Machine Learning Studio.</span></span> <span data-ttu-id="375b5-209">그런 다음 만들고 toohello hello의 세 번째 입력된 포트를 연결 하 여 hello Hello.zip 파일에 hello Python 코드를 사용 하는 실험을 실행할 **Python 스크립트 실행** 이 그림에 표시 된 것과 같이 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-209">Then create and run an experiment that uses hello Python code in hello Hello.zip file by attaching it toohello third input port of hello **Execute Python Script** module, as shown in this figure.</span></span>

![image8](./media/machine-learning-execute-python-scripts/figure6a.png)

![image9](./media/machine-learning-execute-python-scripts/figure6b.png)

<span data-ttu-id="375b5-212">그림 6.</span><span class="sxs-lookup"><span data-stu-id="375b5-212">Figure 6.</span></span> <span data-ttu-id="375b5-213">zip 파일로 업로드된 사용자 정의 Python 코드를 사용하는 샘플 실험.</span><span class="sxs-lookup"><span data-stu-id="375b5-213">Sample experiment with user-defined Python code uploaded as a zip file.</span></span>

<span data-ttu-id="375b5-214">해당 hello zip 파일을 패키지에 포함 된 되었습니다 hello 모듈 출력에 표시 하 고 해당 hello 함수 `print_hello` 를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-214">hello module output shows that hello zip file has been unpackaged and that hello function `print_hello` has been run.</span></span>
<span data-ttu-id="375b5-215"> 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)</span><span class="sxs-lookup"><span data-stu-id="375b5-215"> 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)</span></span>

<span data-ttu-id="375b5-216">그림 7.</span><span class="sxs-lookup"><span data-stu-id="375b5-216">Figure 7.</span></span> <span data-ttu-id="375b5-217">사용자 정의 함수가 사용 hello 내 [Python 스크립트 실행] [ execute-python-script] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-217">User-defined function in use inside hello [Execute Python Script][execute-python-script] module.</span></span>


## <a name="working-with-visualizations"></a><span data-ttu-id="375b5-218">시각화 작업</span><span class="sxs-lookup"><span data-stu-id="375b5-218">Working with visualizations</span></span>

<span data-ttu-id="375b5-219">Hello에서 시각화할 수 MatplotLib를 사용 하 여 hello 브라우저에 생성 된 플롯을 반환할 수 [Python 스크립트 실행][execute-python-script]합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-219">Plots created using MatplotLib that can be visualized on hello browser can be returned by hello [Execute Python Script][execute-python-script].</span></span> <span data-ttu-id="375b5-220">하지만 hello 점도 없는 자동으로 리디렉션된 tooimages 오른쪽을 사용 하는 것 처럼 Hello 사용자 명시적으로 파일 저장 해야 모든 점도 tooPNG 있더라도 하므로 toobe 백 tooAzure 기계 학습을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-220">But hello plots are not automatically redirected tooimages as they are when using R. So hello user must explicitly save any plots tooPNG files if they are toobe returned back tooAzure Machine Learning.</span></span> 

<span data-ttu-id="375b5-221">MatplotLib에서 toogenerate 이미지 hello 절차를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-221">toogenerate images from MatplotLib, you must complete hello following procedure:</span></span>

* <span data-ttu-id="375b5-222">hello 백 엔드 전환 너무 "AGG" hello에서 기본 하 기반 렌더러</span><span class="sxs-lookup"><span data-stu-id="375b5-222">switch hello backend too“AGG” from hello default Qt-based renderer</span></span> 
* <span data-ttu-id="375b5-223">새 그림 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="375b5-223">create a new figure object</span></span> 
* <span data-ttu-id="375b5-224">hello 축 및 것에 모든 표와 예측치를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-224">get hello axis and generate all plots into it</span></span> 
* <span data-ttu-id="375b5-225">hello 그림 tooa PNG 파일 저장</span><span class="sxs-lookup"><span data-stu-id="375b5-225">save hello figure tooa PNG file</span></span> 

<span data-ttu-id="375b5-226">그림 8 hello scatter_matrix 함수를 사용 하 여 팬더에는 산 점도 행렬을 만드는 다음 hello이이 과정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-226">This process is illustrated in hello following Figure 8 that creates a scatter plot matrix using hello scatter_matrix function in Pandas.</span></span>

![image1v](./media/machine-learning-execute-python-scripts/figure-v1-8.png)

<span data-ttu-id="375b5-228">그림 8.</span><span class="sxs-lookup"><span data-stu-id="375b5-228">Figure 8.</span></span> <span data-ttu-id="375b5-229">MatplotLib 그림 tooimages toosave 코드.</span><span class="sxs-lookup"><span data-stu-id="375b5-229">Code toosave MatplotLib figures tooimages.</span></span>

<span data-ttu-id="375b5-230">그림 9 tooreturn 점도 hello 두 번째 출력 포트를 통해 이전에 표시 된 hello 스크립트를 사용 하는 실험을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-230">Figure 9 shows an experiment that uses hello script shown previously tooreturn plots via hello second output port.</span></span>

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9a.png) 

![image2v](./media/machine-learning-execute-python-scripts/figure-v2-9b.png) 

<span data-ttu-id="375b5-233">그림 9.</span><span class="sxs-lookup"><span data-stu-id="375b5-233">Figure 9.</span></span> <span data-ttu-id="375b5-234">Python 코드에서 생성된 그림 시각화.</span><span class="sxs-lookup"><span data-stu-id="375b5-234">Visualizing plots generated from Python code.</span></span>

<span data-ttu-id="375b5-235">가능한 tooreturn 여러 그림 서로 다른 이미지를 저장 하 여, 모든 이미지를 Azure 기계 학습 런타임 선택 hello 사용 되며 시각화에 대 한이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-235">It is possible tooreturn multiple figures by saving them into different images, hello Azure Machine Learning runtime picks up all images and concatenates them for visualization.</span></span>


## <a name="advanced-examples"></a><span data-ttu-id="375b5-236">고급 예제</span><span class="sxs-lookup"><span data-stu-id="375b5-236">Advanced examples</span></span>

<span data-ttu-id="375b5-237">Azure 기계 학습에 설치 된 hello Anaconda 환경을 NumPy, SciPy, 및 Scikits-설명 등의 일반적인 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-237">hello Anaconda environment installed in Azure Machine Learning contains common packages such as NumPy, SciPy, and Scikits-Learn.</span></span> <span data-ttu-id="375b5-238">이러한 패키지는 기계 학습 파이프라인의 여러 데이터 처리 작업에 효율적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-238">These packages can be effectively used for various data processing tasks in a machine learning pipeline.</span></span> <span data-ttu-id="375b5-239">예를 들어 hello 다음 실험 및 스크립트 설명 Scikits 배우기 toocompute 기능 중요도 점수에 앙상블 학습자의 데이터 집합에 대 한 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-239">As an example, hello following experiment and script illustrate hello use of ensemble learners in Scikits-Learn toocompute feature importance scores for a dataset.</span></span> <span data-ttu-id="375b5-240">hello 점수는 다른 ML 모델 공급 하기 전에 사용 되는 tooperform 감독 기능 선택 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-240">hello scores can be used tooperform supervised feature selection before being fed into another ML model.</span></span>

<span data-ttu-id="375b5-241">Hello Python 사용 되는 함수 toocompute hello 중요도 점수와 hello 점수를 기준으로 순서 hello 기능 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-241">Here is hello Python function used toocompute hello importance scores and order hello features based on hello scores:</span></span>

![image11](./media/machine-learning-execute-python-scripts/figure8.png)

<span data-ttu-id="375b5-243">그림 10.</span><span class="sxs-lookup"><span data-stu-id="375b5-243">Figure 10.</span></span> <span data-ttu-id="375b5-244">기능 점수 여 toorank 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-244">Function toorank features by scores.</span></span>
<span data-ttu-id="375b5-245"> hello 다음 실험 다음을 계산 하 고 Azure 기계 학습에서 hello "Pima 인도양 식이 조절" 데이터 집합의 기능 hello 중요도 점수를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-245">  hello following experiment then computes and returns hello importance scores of features in hello “Pima Indian Diabetes” dataset in Azure Machine Learning:</span></span>

<span data-ttu-id="375b5-246">![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)</span><span class="sxs-lookup"><span data-stu-id="375b5-246">![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)</span></span>    

<span data-ttu-id="375b5-247">그림 11.</span><span class="sxs-lookup"><span data-stu-id="375b5-247">Figure 11.</span></span> <span data-ttu-id="375b5-248">Hello Pima 인도양 식이 조절 데이터 집합의 실험 toorank 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-248">Experiment toorank features in hello Pima Indian Diabetes dataset.</span></span>

## <a name="limitations"></a><span data-ttu-id="375b5-249">제한 사항</span><span class="sxs-lookup"><span data-stu-id="375b5-249">Limitations</span></span>
<span data-ttu-id="375b5-250">hello [Python 스크립트 실행] [ execute-python-script] 현재 다음과 같은 제한을 hello에:</span><span class="sxs-lookup"><span data-stu-id="375b5-250">hello [Execute Python Script][execute-python-script] currently has hello following limitations:</span></span>

1. <span data-ttu-id="375b5-251">*샌드박스 실행.*</span><span class="sxs-lookup"><span data-stu-id="375b5-251">*Sandboxed execution.*</span></span> <span data-ttu-id="375b5-252">hello Python 런타임의 현재 보안으로 보호 하 고 결과적으로,을 영구적으로 액세스 toohello 네트워크나 toohello 로컬 파일 시스템을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-252">hello Python runtime is currently sandboxed and, as a result, does not allow access toohello network or toohello local file system in a persistent manner.</span></span> <span data-ttu-id="375b5-253">로컬에 저장 하는 모든 파일 격리 되며 hello 모듈 완료 되 면 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-253">All files saved locally are isolated and deleted once hello module finishes.</span></span> <span data-ttu-id="375b5-254">hello Python 코드에서 실행 하는 hello 컴퓨터에서 대부분의 디렉터리에 액세스할 수 없습니다, 그리고 현재 디렉터리와 하위 디렉터리 hello hello 예외 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-254">hello Python code cannot access most directories on hello machine it runs on, hello exception being hello current directory and its subdirectories.</span></span>
2. <span data-ttu-id="375b5-255">*정교한 개발 및 디버깅 지원이 부족합니다.*</span><span class="sxs-lookup"><span data-stu-id="375b5-255">*Lack of sophisticated development and debugging support.*</span></span> <span data-ttu-id="375b5-256">현재 hello Python 모듈은 intellisense 및 디버깅 같은 IDE 기능을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-256">hello Python module currently does not support IDE features such as intellisense and debugging.</span></span> <span data-ttu-id="375b5-257">또한 런타임 시 hello 모듈이 실패할 경우 hello 전체 Python 스택 추적 ´ ù.</span><span class="sxs-lookup"><span data-stu-id="375b5-257">Also, if hello module fails at runtime, hello full Python stack trace is available.</span></span> <span data-ttu-id="375b5-258">하지만 hello 모듈에 대 한 hello 출력 로그에서 볼 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-258">But it must be viewed in hello output log for hello module.</span></span> <span data-ttu-id="375b5-259">개발 및 IPython 등의 환경에서 Python 스크립트를 디버그할 하 hello 모듈에 hello 코드를 가져온 다음 현재 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-259">We currently recommend that you develop and debug Python scripts in an environment such as IPython and then import hello code into hello module.</span></span>
3. <span data-ttu-id="375b5-260">*단일 데이터 프레임 출력.*</span><span class="sxs-lookup"><span data-stu-id="375b5-260">*Single data frame output.*</span></span> <span data-ttu-id="375b5-261">hello Python 되는 허용 된 tooreturn 단일 데이터 프레임을 출력으로.</span><span class="sxs-lookup"><span data-stu-id="375b5-261">hello Python entry point is only permitted tooreturn a single data frame as output.</span></span> <span data-ttu-id="375b5-262">현재는 가능 tooreturn 임의의 Python 학습 된 모델에는 직접 toohello Azure 기계 학습 런타임 다시와 같은 개체는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-262">It is not currently possible tooreturn arbitrary Python objects such as trained models directly back toohello Azure Machine Learning runtime.</span></span> <span data-ttu-id="375b5-263">와 같은 [R 스크립트 실행][execute-r-script], hello가 같은 제한 사항이 것은 바이트에 toopickle 개체 배열 및 다음 데이터 프레임 내에서 반환 하는 대부분의 경우에 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-263">Like [Execute R Script][execute-r-script], which has hello same limitation, it is possible in many cases toopickle objects into a byte array and then return that inside of a data frame.</span></span>
4. <span data-ttu-id="375b5-264">*Python 설치 불가능 toocustomize*합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-264">*Inability toocustomize Python installation*.</span></span> <span data-ttu-id="375b5-265">현재 hello 방법은 tooadd 사용자 지정 Python 모듈에만 앞에서 설명한 hello zip 파일 메커니즘을 통해.</span><span class="sxs-lookup"><span data-stu-id="375b5-265">Currently, hello only way tooadd custom Python modules is via hello zip file mechanism described earlier.</span></span> <span data-ttu-id="375b5-266">이 방법은 작은 모듈의 경우 가능하지만, 모듈이 크거나(특히 네이티브 DLL이 있는 모듈) 모듈 수가 많은 경우 번거로울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-266">While this is feasible for small modules, it is cumbersome for large modules (especially those with native DLLs) or a large number of modules.</span></span> 

## <a name="conclusions"></a><span data-ttu-id="375b5-267">결론</span><span class="sxs-lookup"><span data-stu-id="375b5-267">Conclusions</span></span>
<span data-ttu-id="375b5-268">hello [Python 스크립트 실행] [ execute-python-script] 모듈을 사용 하면 데이터 과학자 tooincorporate 기존 Python 코드를 Azure 기계 학습 및 tooseamlessly 학습 워크플로에 클라우드에서 호스팅하는 컴퓨터 웹 서비스의 일부분으로 운영 화 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-268">hello [Execute Python Script][execute-python-script] module allows a data scientist tooincorporate existing Python code into cloud-hosted machine learning workflows in Azure Machine Learning and tooseamlessly operationalize them as part of a web service.</span></span> <span data-ttu-id="375b5-269">Azure 기계 학습의 다른 모듈와 hello Python 스크립트 모듈 자연스럽 게 상호 운용 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-269">hello Python script module interoperates naturally with other modules in Azure Machine Learning.</span></span> <span data-ttu-id="375b5-270">데이터 탐색 toopre 처리 및 기능 추출 / tooevaluation 작업의 범위 및 hello 결과의 사후 처리에 대 한 hello 모듈을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-270">hello module can be used for a range of tasks from data exploration toopre-processing and feature extraction, and then tooevaluation and post-processing of hello results.</span></span> <span data-ttu-id="375b5-271">실행을 위해 사용 되는 hello 백 엔드 런타임 Anaconda, 충분 한 테스트를 널리 사용 되는 Python 배포를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-271">hello backend runtime used for execution is based on Anaconda, a well-tested and widely used Python distribution.</span></span> <span data-ttu-id="375b5-272">이 백 엔드 쉽게 있습니다 tooon 보드 기존 코드 자산에 대 한 hello 클라우드로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-272">This backend makes it simple for you tooon-board existing code assets into hello cloud.</span></span>

<span data-ttu-id="375b5-273">추가 기능 toohello tooprovide 것으로 예상 [Python 스크립트 실행] [ execute-python-script] 기능 tootrain hello 및 Python에서 모델을 운용와 같은 모듈 및 tooadd hello에 대 한 지원 향상 개발 및 Azure 기계 학습 스튜디오에서 코드를 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-273">We expect tooprovide additional functionality toohello [Execute Python Script][execute-python-script] module such as hello ability tootrain and operationalize models in Python and tooadd better support for hello development and debugging code in Azure Machine Learning Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="375b5-274">다음 단계</span><span class="sxs-lookup"><span data-stu-id="375b5-274">Next steps</span></span>
<span data-ttu-id="375b5-275">자세한 내용은 참조 hello [Python 개발자 센터](https://azure.microsoft.com/develop/python/)합니다.</span><span class="sxs-lookup"><span data-stu-id="375b5-275">For more information, see hello [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span>

<!-- Module References -->
[execute-python-script]: https://msdn.microsoft.com/library/azure/cdb56f95-7f4c-404d-bde7-5bb972e6f232/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
