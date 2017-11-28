---
title: "기계 학습 Python 클라이언트 라이브러리와 함께 데이터 집합 aaaAccess | Microsoft Docs"
description: "설치 및 Python 클라이언트 라이브러리 tooaccess hello 사용 하 여 로컬 Python 환경에서 Azure 기계 학습 데이터를 안전 하 게 관리 합니다."
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a><span data-ttu-id="88256-103">Hello Azure 기계 학습 Python 클라이언트 라이브러리를 사용 하 여 Python으로 데이터 집합 액세스</span><span class="sxs-lookup"><span data-stu-id="88256-103">Access datasets with Python using hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="88256-104">Microsoft Azure 기계 학습 Python 클라이언트 라이브러리의 hello 미리 보기는 보안 액세스 tooyour 로컬 Python 환경에서 Azure 기계 학습 데이터 집합을 사용 하도록 설정할 수 하 고 작업 영역에서 데이터 집합의 hello 생성 및 관리를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-104">hello preview of Microsoft Azure Machine Learning Python client library can enable secure access tooyour Azure Machine Learning datasets from a local Python environment and enables hello creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="88256-105">이 항목에서는 다음 수행 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="88256-106">hello 기계 학습 Python 클라이언트 라이브러리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-106">install hello Machine Learning Python client library</span></span> 
* <span data-ttu-id="88256-107">액세스 방법에 대 한 지침을 포함 하 여 데이터 집합을 업로드 하 고 tooget 권한 부여 tooaccess 로컬 Python 환경에서 Azure 기계 학습 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="88256-107">access and upload datasets, including instructions on how tooget authorization tooaccess Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="88256-108">실험에서 중간 데이터 집합에 액세스</span><span class="sxs-lookup"><span data-stu-id="88256-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="88256-109">hello Python 클라이언트 라이브러리 tooenumerate 데이터 집합을 사용 하 여, 메타 데이터에 액세스, 데이터 집합의 hello 내용의 읽을, 새 데이터 집합을 만들 및 기존 데이터 집합 업데이트</span><span class="sxs-lookup"><span data-stu-id="88256-109">use hello Python client library tooenumerate datasets, access metadata, read hello contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="88256-110"><a name="prerequisites"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="88256-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="88256-111">hello Python 클라이언트 라이브러리 hello 다음 환경에서 테스트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-111">hello Python client library has been tested under hello following environments:</span></span>

* <span data-ttu-id="88256-112">Windows, Mac 및 Linux</span><span class="sxs-lookup"><span data-stu-id="88256-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="88256-113">Python 2.7, 3.3 및 3.4</span><span class="sxs-lookup"><span data-stu-id="88256-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="88256-114">Hello 다음 패키지에 종속 되어:</span><span class="sxs-lookup"><span data-stu-id="88256-114">It has a dependency on hello following packages:</span></span>

* <span data-ttu-id="88256-115">requests</span><span class="sxs-lookup"><span data-stu-id="88256-115">requests</span></span>
* <span data-ttu-id="88256-116">python-dateutil</span><span class="sxs-lookup"><span data-stu-id="88256-116">python-dateutil</span></span>
* <span data-ttu-id="88256-117">pandas</span><span class="sxs-lookup"><span data-stu-id="88256-117">pandas</span></span>

<span data-ttu-id="88256-118">와 같은 Python 배포를 사용 하는 것이 좋습니다 [Anaconda](http://continuum.io/downloads#all) 또는 [Canopy](https://store.enthought.com/downloads/), python, IPython 나오는 및 위에 나열 된 3 hello 패키지 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and hello three packages listed above installed.</span></span> <span data-ttu-id="88256-119">IPython은 반드시 필요하지는 않지만 데이터를 대화식으로 조작하고 시각화는 데 훌륭한 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="88256-120"><a name="installation"></a>어떻게 tooinstall hello Azure 기계 학습 Python 클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="88256-120"><a name="installation"></a>How tooinstall hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="88256-121">hello Azure 기계 학습 Python 클라이언트 라이브러리는이 항목에 설명 된 설치 된 toocomplete hello 작업 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-121">hello Azure Machine Learning Python client library must also be installed toocomplete hello tasks outlined in this topic.</span></span> <span data-ttu-id="88256-122">Hello에서 다운로드할 수 [Python 패키지 인덱스](https://pypi.python.org/pypi/azureml)합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-122">It is available from hello [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="88256-123">Python 환경에서 실행 tooinstall 다음 로컬 Python 환경에서 명령을 hello:</span><span class="sxs-lookup"><span data-stu-id="88256-123">tooinstall it in your Python environment, run hello following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="88256-124">다운로드 하 고 hello 원본에서의 설치 수 또는 [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python)합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-124">Alternatively, you can download and install from hello sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="88256-125">Git 컴퓨터에 설치 되어 있는 경우 pip tooinstall hello git 리포지토리에서 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-125">If you have git installed on your machine, you can use pip tooinstall directly from hello git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="88256-126"><a name="datasetAccess"></a>Studio 코드 조각 tooaccess 데이터 집합 사용</span><span class="sxs-lookup"><span data-stu-id="88256-126"><a name="datasetAccess"></a>Use Studio Code snippets tooaccess datasets</span></span>
<span data-ttu-id="88256-127">hello Python 클라이언트 라이브러리 실행 된 실험에서 프로그래밍 방식 액세스 tooyour 기존 데이터 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-127">hello Python client library gives you programmatic access tooyour existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="88256-128">Hello Studio 웹 인터페이스에서 모든 hello 필요한 정보 toodownload가 포함 된 데이터 집합 위치 컴퓨터에 팬더 데이터 프레임 개체로 deserialize 하는 코드 조각을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-128">From hello Studio web interface, you can generate code snippets that include all hello necessary information toodownload and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="88256-129"><a name="security"></a>데이터 액세스를 위한 보안</span><span class="sxs-lookup"><span data-stu-id="88256-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="88256-130">hello Python 클라이언트 라이브러리와 함께 사용 하 여 작업 영역 id 및 권한 부여 포함 Studio에서 제공 하는 코드 조각 hello 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-130">hello code snippets provided by Studio for use with hello Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="88256-131">이러한 모든 권한 tooyour 작업 영역을 제공 하 고는 암호와 같은 보호 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-131">These provide full access tooyour workspace and must be protected, like a password.</span></span>

<span data-ttu-id="88256-132">보안상의 이유로 hello 코드 조각 기능은만 해당 역할이으로 설정 되어 사용할 수 있는 toousers **소유자** hello 작업 영역에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-132">For security reasons, hello code snippet functionality is only available toousers that have their role set as **Owner** for hello workspace.</span></span> <span data-ttu-id="88256-133">Hello에 Azure 기계 학습 스튜디오에 사용자 역할이 표시 **사용자** 페이지 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-133">Your role is displayed in Azure Machine Learning Studio on hello **USERS** page under **Settings**.</span></span>

![보안][security]

<span data-ttu-id="88256-135">역할으로 설정 되어 있지 않으면 **소유자**는 소유자로 reinvited toobe 요청 하거나 작업 영역 tooprovide hello의 hello 소유자에 게 hello 코드 조각으로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-135">If your role is not set as **Owner**, you can either request toobe reinvited as an owner, or ask hello owner of hello workspace tooprovide you with hello code snippet.</span></span>

<span data-ttu-id="88256-136">tooobtain hello 권한 부여 토큰 hello 다음 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-136">tooobtain hello authorization token, you can do one of hello following:</span></span>

* <span data-ttu-id="88256-137">소유자에서 토큰을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-137">Ask for a token from an owner.</span></span> <span data-ttu-id="88256-138">소유자가 작업 영역 Studio에서의 hello 설정 페이지에서 해당 권한 부여 토큰을 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-138">Owners can access their authorization tokens from hello Settings page of their workspace in Studio.</span></span> <span data-ttu-id="88256-139">선택 **설정** hello 왼쪽 창에서 데이터 및 클릭에서에서 **권한 부여 토큰** toosee hello 기본 및 보조 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-139">Select **Settings** from hello left pane and click **AUTHORIZATION TOKENS** toosee hello primary and secondary tokens.</span></span>  <span data-ttu-id="88256-140">기본 hello 또는 hello 보조 권한 부여 토큰 사용할 수 있지만 hello 코드 조각에, 소유자만 hello 보조 권한 부여 토큰을 공유 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-140">Although either hello primary or hello secondary authorization tokens can be used in hello code snippet, it is recommended that owners only share hello secondary authorization tokens.</span></span>

![권한 부여 토큰](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="88256-142">승격 toobe toorole 소유자에 게 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-142">Ask toobe promoted toorole of owner.</span></span>  <span data-ttu-id="88256-143">toodo이 hello 작업 영역 요구 toofirst의 현재 소유자 hello 작업 영역에서 제거 하면 다음 다시 초대 하거나 소유자로 tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-143">toodo this, a current owner of hello workspace needs toofirst remove you from hello workspace then re-invite you tooit as an owner.</span></span>

<span data-ttu-id="88256-144">개발자가 얻은 hello 작업 영역 id 및 권한 부여 되 면 토큰을 서로 수 tooaccess hello 역할에 관계 없이 hello 코드 조각을 사용 하 여 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-144">Once developers have obtained hello workspace id and authorization token, they are able tooaccess hello workspace using hello code snippet regardless of their role.</span></span>

<span data-ttu-id="88256-145">Hello에 관리 되는 권한 부여 토큰 **권한 부여 토큰** 페이지 **설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-145">Authorization tokens are managed on hello **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="88256-146">다시 생성할 수 있지만이 절차 액세스 toohello 이전 토큰을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-146">You can regenerate them, but this procedure revokes access toohello previous token.</span></span>

### <span data-ttu-id="88256-147"><a name="accessingDatasets"></a>로컬 Python 응용 프로그램에서 데이터 집합에 액세스</span><span class="sxs-lookup"><span data-stu-id="88256-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="88256-148">기계 학습 스튜디오에서 클릭 **데이터 집합** hello hello 왼쪽 탐색 모음에서.</span><span class="sxs-lookup"><span data-stu-id="88256-148">In Machine Learning Studio, click **DATASETS** in hello navigation bar on hello left.</span></span>
2. <span data-ttu-id="88256-149">Tooaccess 원하는 hello 데이터 집합을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-149">Select hello dataset you would like tooaccess.</span></span> <span data-ttu-id="88256-150">Hello에서 hello 데이터 집합 중 하나를 선택할 수 있습니다 **내 데이터 집합** 목록 또는 hello **샘플** 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-150">You can select any of hello datasets from hello **MY DATASETS** list or from hello **SAMPLES** list.</span></span>
3. <span data-ttu-id="88256-151">Hello 아래쪽 도구 모음에서 클릭 **데이터 액세스 코드 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-151">From hello bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="88256-152">Hello 데이터가 hello Python 클라이언트 라이브러리와 호환 되지 않는 형식 이면이 단추가 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88256-152">If hello data is in a format incompatible with hello Python client library, this button is disabled.</span></span>
   
    ![데이터 집합][datasets]
4. <span data-ttu-id="88256-154">Hello 코드 조각 표시 되는 hello 창에서 선택한 tooyour 클립보드로 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-154">Select hello code snippet from hello window that appears and copy it tooyour clipboard.</span></span>
   
    ![액세스 코드][dataset-access-code]
5. <span data-ttu-id="88256-156">로컬 Python 응용 프로그램의 hello 노트북에 hello 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-156">Paste hello code into hello notebook of your local Python application.</span></span>
   
    ![노트북][ipython-dataset]

## <span data-ttu-id="88256-158"><a name="accessingIntermediateDatasets"></a>기계 학습 실험에서 중간 데이터 집합에 액세스</span><span class="sxs-lookup"><span data-stu-id="88256-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="88256-159">실험을 hello 기계 학습 스튜디오에서에서 실행 가능한 tooaccess hello 중간에서 데이터 집합 hello 출력 노드 모듈의 파일은입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-159">After an experiment is run in hello Machine Learning Studio, it is possible tooaccess hello intermediate datasets from hello output nodes of modules.</span></span> <span data-ttu-id="88256-160">중간 데이터 집합은 모델 도구가 실행될 때 중간 단계를 위해 생성되고 사용된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="88256-161">중간 데이터 집합이 hello 데이터 형식은 hello Python 클라이언트 라이브러리와 호환으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-161">Intermediate datasets can be accessed as long as hello data format is compatible with hello Python client library.</span></span>

<span data-ttu-id="88256-162">hello 다음과 같은 형식이 지원 됩니다 (hello에 이러한 상수는 `azureml.DataTypeIds` 클래스).</span><span class="sxs-lookup"><span data-stu-id="88256-162">hello following formats are supported (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="88256-163">일반 텍스트</span><span class="sxs-lookup"><span data-stu-id="88256-163">PlainText</span></span>
* <span data-ttu-id="88256-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="88256-164">GenericCSV</span></span>
* <span data-ttu-id="88256-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="88256-165">GenericTSV</span></span>
* <span data-ttu-id="88256-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="88256-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="88256-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="88256-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="88256-168">모듈 출력 노드 위로 이동 하 여 hello 형식을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-168">You can determine hello format by hovering over a module output node.</span></span> <span data-ttu-id="88256-169">도구 설명에 hello 노드 이름과 함께 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88256-169">It is displayed along with hello node name, in a tooltip.</span></span>

<span data-ttu-id="88256-170">Hello 같은 hello 모듈의 일부 [분할] [ split] 모듈, 명명 된 출력 tooa 형식 `Dataset`, hello Python 클라이언트 라이브러리에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-170">Some of hello modules, such as hello [Split][split] module, output tooa format named `Dataset`, which is not supported by hello Python client library.</span></span>

![데이터 집합 형식][dataset-format]

<span data-ttu-id="88256-172">같은 toouse 변환 모듈이 필요 [tooCSV 변환][convert-to-csv], tooget 지원 되는 형식으로 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-172">You need toouse a conversion module, such as [Convert tooCSV][convert-to-csv], tooget an output into a supported format.</span></span>

![GenericCSV 형식][csv-format]

<span data-ttu-id="88256-174">hello 다음 단계는 보여 주는 예제는 실험을 만들고 실행를 hello 중간 데이터 집합에 액세스 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-174">hello following steps show an example that creates an experiment, runs it and accesses hello intermediate dataset.</span></span>

1. <span data-ttu-id="88256-175">새로운 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="88256-175">Create a new experiment.</span></span>
2. <span data-ttu-id="88256-176">**성인 인구 조사 소득 이진 분류 데이터 집합** 모듈을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="88256-177">삽입 한 [분할] [ split] 모듈 toohello 입력된 데이터 집합 모듈 출력을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-177">Insert a [Split][split] module, and connect its input toohello dataset module output.</span></span>
4. <span data-ttu-id="88256-178">삽입 한 [tooCSV 변환] [ convert-to-csv] 모듈의 hello 해당 입력된 tooone 연결 [분할] [ split] 모듈의 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-178">Insert a [Convert tooCSV][convert-to-csv] module and connect its input tooone of hello [Split][split] module outputs.</span></span>
5. <span data-ttu-id="88256-179">Hello 실험을 저장 하 고 실행 될 때까지 기다렸다가 toofinish 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-179">Save hello experiment, run it, and wait for it toofinish running.</span></span>
6. <span data-ttu-id="88256-180">Hello에 hello 출력 노드를 클릭 [tooCSV 변환] [ convert-to-csv] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-180">Click hello output node on hello [Convert tooCSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="88256-181">Hello 상황에 맞는 메뉴에 표시 되 면 선택 **데이터 액세스 코드 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-181">When hello context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![상황에 맞는 메뉴][experiment]
8. <span data-ttu-id="88256-183">Hello 코드 조각 선택에서 나타나는 hello 창 tooyour 클립보드를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-183">Select hello code snippet and copy it tooyour clipboard from hello window that appears.</span></span>
   
    ![액세스 코드][intermediate-dataset-access-code]
9. <span data-ttu-id="88256-185">전자 필기장의 hello 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-185">Paste hello code in your notebook.</span></span>
   
    ![노트북][ipython-intermediate-dataset]
10. <span data-ttu-id="88256-187">Matplotlib를 사용 하 여 hello 데이터를 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-187">You can visualize hello data using matplotlib.</span></span> <span data-ttu-id="88256-188">그러면 hello 나가 열에 대 한 히스토그램에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88256-188">This displays in a histogram for hello age column:</span></span>
    
    ![히스토그램][ipython-histogram]

## <span data-ttu-id="88256-190"><a name="clientApis"></a>기계 학습 Python 클라이언트 라이브러리 tooaccess hello를 사용 하 여, 읽기, 작성 및 데이터 집합 관리</span><span class="sxs-lookup"><span data-stu-id="88256-190"><a name="clientApis"></a>Use hello Machine Learning Python client library tooaccess, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="88256-191">작업 영역</span><span class="sxs-lookup"><span data-stu-id="88256-191">Workspace</span></span>
<span data-ttu-id="88256-192">hello 작업 영역은 hello hello Python 클라이언트 라이브러리에 대 한 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-192">hello workspace is hello entry point for hello Python client library.</span></span> <span data-ttu-id="88256-193">Hello 제공 `Workspace` 클래스에 작업 영역 id 및 권한 부여 토큰 toocreate와 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="88256-193">Provide hello `Workspace` class with your workspace id and authorization token toocreate an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="88256-194">데이터 집합 열거</span><span class="sxs-lookup"><span data-stu-id="88256-194">Enumerate datasets</span></span>
<span data-ttu-id="88256-195">tooenumerate 지정된 된 작업 영역에서 모든 데이터 집합.</span><span class="sxs-lookup"><span data-stu-id="88256-195">tooenumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="88256-196">tooenumerate 정당한 hello 사용자가 만든 데이터 집합:</span><span class="sxs-lookup"><span data-stu-id="88256-196">tooenumerate just hello user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="88256-197">tooenumerate 정당한 hello 예제 데이터 집합:</span><span class="sxs-lookup"><span data-stu-id="88256-197">tooenumerate just hello example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="88256-198">데이터 집합 이름(대/소문자 구분)으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="88256-199">또는 인덱스별로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="88256-200">Metadata</span><span class="sxs-lookup"><span data-stu-id="88256-200">Metadata</span></span>
<span data-ttu-id="88256-201">메타 데이터를 추가 toocontent에 있어야 하는 데이터 집합.</span><span class="sxs-lookup"><span data-stu-id="88256-201">Datasets have metadata, in addition toocontent.</span></span> <span data-ttu-id="88256-202">(중간 데이터 집합 예외 toothis 규칙은 및 메타 데이터에는 필요가 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="88256-202">(Intermediate datasets are an exception toothis rule and do not have any metadata.)</span></span>

<span data-ttu-id="88256-203">일부 메타 데이터 값은 생성 시 hello 사용자가 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="88256-203">Some metadata values are assigned by hello user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="88256-204">다른 메타 데이터 값은 Azure 기계 학습에서 할당:</span><span class="sxs-lookup"><span data-stu-id="88256-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="88256-205">Hello 참조 `SourceDataset` 자세한 on hello 사용 가능한 메타 데이터에 대 한 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-205">See hello `SourceDataset` class for more on hello available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="88256-206">콘텐츠 읽기</span><span class="sxs-lookup"><span data-stu-id="88256-206">Read contents</span></span>
<span data-ttu-id="88256-207">자동으로 기계 학습 스튜디오에서 제공 하는 hello 코드 조각 다운로드 하 여 hello dataset tooa 팬더 데이터 프레임 개체를 역직렬화 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-207">hello code snippets provided by Machine Learning Studio automatically download and deserialize hello dataset tooa Pandas DataFrame object.</span></span> <span data-ttu-id="88256-208">Hello로 이렇게 `to_dataframe` 메서드:</span><span class="sxs-lookup"><span data-stu-id="88256-208">This is done with hello `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="88256-209">Toodownload hello 원시 데이터를 선호 하 고 직접 hello deserialization을 수행 하는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-209">If you prefer toodownload hello raw data, and perform hello deserialization yourself, that is an option.</span></span> <span data-ttu-id="88256-210">Hello 순간에 상위 hello Python 클라이언트 라이브러리를 역직렬화 할 수 없습니다 'ARFF' 등의 형식에 대 한 hello 유일한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-210">At hello moment, this is hello only option for formats such as 'ARFF', which hello Python client library cannot deserialize.</span></span>

<span data-ttu-id="88256-211">텍스트로 tooread hello 내용:</span><span class="sxs-lookup"><span data-stu-id="88256-211">tooread hello contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="88256-212">이진으로 tooread hello 내용:</span><span class="sxs-lookup"><span data-stu-id="88256-212">tooread hello contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="88256-213">클릭할 수도 스트림 toohello 내용을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-213">You can also just open a stream toohello contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="88256-214">새 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="88256-214">Create a new dataset</span></span>
<span data-ttu-id="88256-215">hello Python 클라이언트 라이브러리에서는 Python 프로그램에서 tooupload 데이터 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-215">hello Python client library allows you tooupload datasets from your Python program.</span></span> <span data-ttu-id="88256-216">이러한 데이터 집합은 작업 영역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="88256-217">데이터 팬더 데이터 프레임에 있으면 코드 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-217">If you have your data in a Pandas DataFrame, use hello following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="88256-218">데이터가 이미 직렬화된 경우 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="88256-219">hello Python 클라이언트 라이브러리는 팬더 데이터 프레임 toohello 다음 서식을 지정 하는 수 tooserialize (hello에 이러한 상수는 `azureml.DataTypeIds` 클래스).</span><span class="sxs-lookup"><span data-stu-id="88256-219">hello Python client library is able tooserialize a Pandas DataFrame toohello following formats (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="88256-220">일반 텍스트</span><span class="sxs-lookup"><span data-stu-id="88256-220">PlainText</span></span>
* <span data-ttu-id="88256-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="88256-221">GenericCSV</span></span>
* <span data-ttu-id="88256-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="88256-222">GenericTSV</span></span>
* <span data-ttu-id="88256-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="88256-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="88256-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="88256-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="88256-225">기존 데이터 집합 업데이트</span><span class="sxs-lookup"><span data-stu-id="88256-225">Update an existing dataset</span></span>
<span data-ttu-id="88256-226">기존 데이터 집합을 일치 하는 이름 가진 새 데이터 집합을 tooupload 하려고 하면 충돌 오류를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-226">If you try tooupload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="88256-227">기존 데이터 집합 tooupdate 먼저 tooget 참조 toohello 기존 데이터 집합.</span><span class="sxs-lookup"><span data-stu-id="88256-227">tooupdate an existing dataset, you first need tooget a reference toohello existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="88256-228">다음 사용 하 여 `update_from_dataframe` Azure의 hello 데이터 집합의 tooserialize 및 바꾸기 hello 내용을:</span><span class="sxs-lookup"><span data-stu-id="88256-228">Then use `update_from_dataframe` tooserialize and replace hello contents of hello dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="88256-229">Tooserialize hello 데이터 tooa 서로 다른 서식을 지정 하려는 경우 선택적 hello에 대 한 값을 지정 합니다. `data_type_id` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-229">If you want tooserialize hello data tooa different format, specify a value for hello optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="88256-230">Hello에 대 한 값을 지정 하 여 새 설명을 선택적으로 설정할 수 있습니다 `description` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-230">You can optionally set a new description by specifying a value for hello `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

<span data-ttu-id="88256-231">Hello에 대 한 값을 지정 하 여 새 이름을 지정할 수도 있습니다 `name` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-231">You can optionally set a new name by specifying a value for hello `name` parameter.</span></span> <span data-ttu-id="88256-232">이제 새 이름만 hello를 사용 하 여 hello 데이터 집합을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88256-232">From now on, you'll retrieve hello dataset using hello new name only.</span></span> <span data-ttu-id="88256-233">hello 코드 다음에 hello 데이터, 이름 및 설명을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-233">hello following code updates hello data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="88256-234">hello `data_type_id`, `name` 및 `description` 매개 변수는 선택 사항이 며 기본 tootheir 이전 값입니다.</span><span class="sxs-lookup"><span data-stu-id="88256-234">hello `data_type_id`, `name` and `description` parameters are optional and default tootheir previous value.</span></span> <span data-ttu-id="88256-235">hello `dataframe` 매개 변수는 항상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-235">hello `dataframe` parameter is always required.</span></span>

<span data-ttu-id="88256-236">데이터가 이미 직렬화된 경우 `update_from_dataframe` 대신 `update_from_raw_data`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="88256-237">`dataframe` 대신 `raw_data`만 전달하면, 비슷하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="88256-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

