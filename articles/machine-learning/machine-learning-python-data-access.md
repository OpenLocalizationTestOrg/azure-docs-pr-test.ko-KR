---
title: "Machine Learning Python 클라이언트 라이브러리를 사용하여 데이터 집합에 액세스 | Microsoft Docs"
description: "Python 클라이언트 라이브러리를 설치하고 사용하여 로컬 Python 환경에서 안전하게 Azure 기계 학습 데이터에 액세스하고 관리합니다."
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
ms.openlocfilehash: e3ae712e0f8d386f637520fbbff4b348bc86f32d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="access-datasets-with-python-using-the-azure-machine-learning-python-client-library"></a><span data-ttu-id="8d2ee-103">Azure 기계 학습 Python 클라이언트 라이브러리를 사용하여 Python으로 데이터 집합에 액세스</span><span class="sxs-lookup"><span data-stu-id="8d2ee-103">Access datasets with Python using the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="8d2ee-104">Microsoft Azure 기계 학습 Python 클라이언트 라이브러리 미리보기를 사용하면 로컬 Python 환경에서 Azure 기계 학습 데이터 집합으로 안전하게 액세스 할 수 있고, 작업 영역에 데이터 집합을 생성하여 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-104">The preview of Microsoft Azure Machine Learning Python client library can enable secure access to your Azure Machine Learning datasets from a local Python environment and enables the creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="8d2ee-105">이 항목에서는 다음 수행 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="8d2ee-106">기계 학습 Python 클라이언트 라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="8d2ee-106">install the Machine Learning Python client library</span></span> 
* <span data-ttu-id="8d2ee-107">로컬 Python 환경에서 Azure 기계 학습 데이터 집합에 액세스하는 권한을 얻는 방법에 대한 지침을 비롯하여 데이터 집합에 액세스 및 업로드</span><span class="sxs-lookup"><span data-stu-id="8d2ee-107">access and upload datasets, including instructions on how to get authorization to access Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="8d2ee-108">실험에서 중간 데이터 집합에 액세스</span><span class="sxs-lookup"><span data-stu-id="8d2ee-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="8d2ee-109">Python 클라이언트 라이브러리를 사용하여 데이터 집합 열거, 메타 데이터에 액세스, 데이터 집합의 내용 읽기, 새 데이터 집합 만들기 및 기존 데이터 집합 업데이트</span><span class="sxs-lookup"><span data-stu-id="8d2ee-109">use the Python client library to enumerate datasets, access metadata, read the contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="8d2ee-110"><a name="prerequisites"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="8d2ee-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="8d2ee-111">Python 클라이언트 라이브러리는 다음과 같은 환경에서 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-111">The Python client library has been tested under the following environments:</span></span>

* <span data-ttu-id="8d2ee-112">Windows, Mac 및 Linux</span><span class="sxs-lookup"><span data-stu-id="8d2ee-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="8d2ee-113">Python 2.7, 3.3 및 3.4</span><span class="sxs-lookup"><span data-stu-id="8d2ee-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="8d2ee-114">다음 패키지에 대한 종속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-114">It has a dependency on the following packages:</span></span>

* <span data-ttu-id="8d2ee-115">requests</span><span class="sxs-lookup"><span data-stu-id="8d2ee-115">requests</span></span>
* <span data-ttu-id="8d2ee-116">python-dateutil</span><span class="sxs-lookup"><span data-stu-id="8d2ee-116">python-dateutil</span></span>
* <span data-ttu-id="8d2ee-117">pandas</span><span class="sxs-lookup"><span data-stu-id="8d2ee-117">pandas</span></span>

<span data-ttu-id="8d2ee-118">Python, IPython 및 설치된 것으로 위에 나열된 세 가지 패키지와 함께 제공되는 [Anaconda](http://continuum.io/downloads#all) 또는 [Canopy](https://store.enthought.com/downloads/) 등의 Python 배포판을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and the three packages listed above installed.</span></span> <span data-ttu-id="8d2ee-119">IPython은 반드시 필요하지는 않지만 데이터를 대화식으로 조작하고 시각화는 데 훌륭한 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="8d2ee-120"><a name="installation"></a>Azure 기계 학습 Python 클라이언트 라이브러리를 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="8d2ee-120"><a name="installation"></a>How to install the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="8d2ee-121">이 항목에 설명된 작업을 완료하려면 Azure Machine Learning Python 클라이언트 라이브러리도 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-121">The Azure Machine Learning Python client library must also be installed to complete the tasks outlined in this topic.</span></span> <span data-ttu-id="8d2ee-122">[Python 패키지 인덱스](https://pypi.python.org/pypi/azureml)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-122">It is available from the [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="8d2ee-123">Python 환경에 설치하려면 로컬 Python 환경에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-123">To install it in your Python environment, run the following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="8d2ee-124">또는 [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python)의 원본에서 다운로드하고 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-124">Alternatively, you can download and install from the sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="8d2ee-125">컴퓨터에 git가 설치된 경우 pip를 사용하여 git 리포지토리에서 직접 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-125">If you have git installed on your machine, you can use pip to install directly from the git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="8d2ee-126"><a name="datasetAccess"></a>스튜디오 코드 조각을 사용하여 데이터 집합에 액세스</span><span class="sxs-lookup"><span data-stu-id="8d2ee-126"><a name="datasetAccess"></a>Use Studio Code snippets to access datasets</span></span>
<span data-ttu-id="8d2ee-127">Python 클라이언트 라이브러리를 사용하면 실행된 기존 데이터 집합에 프로그래밍 방식으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-127">The Python client library gives you programmatic access to your existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="8d2ee-128">스튜디오 웹 인터페이스에서 필요한 모든 정보를 포함하는 코드 조간을 생성하여 로컬 컴퓨터에 Pandas DataFrame 개체로 데이터 집합을 다운로드하고 역직렬화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-128">From the Studio web interface, you can generate code snippets that include all the necessary information to download and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="8d2ee-129"><a name="security"></a>데이터 액세스를 위한 보안</span><span class="sxs-lookup"><span data-stu-id="8d2ee-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="8d2ee-130">스튜디오에서 Python 클라이언트 라이브러리와 함께 사용하도록 제공하는 코드 조각에는 작업 영역 ID와 권한 부여 토큰이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-130">The code snippets provided by Studio for use with the Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="8d2ee-131">이러한 코드 조각은 작업 영역에 대한 전체 액세스 권한을 제공하고 암호와 같이 보호되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-131">These provide full access to your workspace and must be protected, like a password.</span></span>

<span data-ttu-id="8d2ee-132">보안상의 이유로 코드 조각은 이전에 역할이 작업 영역의 **소유자** 로 설정된 사용자만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-132">For security reasons, the code snippet functionality is only available to users that have their role set as **Owner** for the workspace.</span></span> <span data-ttu-id="8d2ee-133">사용자의 역할은 Azure Machine Learning 스튜디오의 **설정**에서 **사용자** 페이지에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-133">Your role is displayed in Azure Machine Learning Studio on the **USERS** page under **Settings**.</span></span>

![보안][security]

<span data-ttu-id="8d2ee-135">역할이 **소유자**로 설정되지 않은 경우 소유자로 다시 초대되도록 요청하거나 작업 영역의 소유자에게 코드 조각을 제공하도록 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-135">If your role is not set as **Owner**, you can either request to be reinvited as an owner, or ask the owner of the workspace to provide you with the code snippet.</span></span>

<span data-ttu-id="8d2ee-136">권한 부여 토큰을 가져오기 위해 다음 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-136">To obtain the authorization token, you can do one of the following:</span></span>

* <span data-ttu-id="8d2ee-137">소유자에서 토큰을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-137">Ask for a token from an owner.</span></span> <span data-ttu-id="8d2ee-138">소유자가 스튜디오의 작업 영역에 있는 설정 페이지에서 권한 부여 토큰에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-138">Owners can access their authorization tokens from the Settings page of their workspace in Studio.</span></span> <span data-ttu-id="8d2ee-139">왼쪽 창에서 **설정**을 선택하고 **권한 부여 토큰**을 클릭하여 기본 및 보조 토큰을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-139">Select **Settings** from the left pane and click **AUTHORIZATION TOKENS** to see the primary and secondary tokens.</span></span>  <span data-ttu-id="8d2ee-140">기본 또는 보조 권한 부여 토큰을 코드 조각에서 사용할 수 있지만, 소유자가 보조 권한 부여 토크만 공유하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-140">Although either the primary or the secondary authorization tokens can be used in the code snippet, it is recommended that owners only share the secondary authorization tokens.</span></span>

![권한 부여 토큰](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="8d2ee-142">소유자의 역할로 승격하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-142">Ask to be promoted to role of owner.</span></span>  <span data-ttu-id="8d2ee-143">그러려면 작업 영역의 현재 소유자가 먼저 작업 영역에서 사용자를 제거한 다음 소유자로 다시 초대해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-143">To do this, a current owner of the workspace needs to first remove you from the workspace then re-invite you to it as an owner.</span></span>

<span data-ttu-id="8d2ee-144">개발자가 작업 영역 ID와 권한 부여 토큰을 얻고 나면 역할에 상관 없이 코드 조각을 사용하여 작업 영역에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-144">Once developers have obtained the workspace id and authorization token, they are able to access the workspace using the code snippet regardless of their role.</span></span>

<span data-ttu-id="8d2ee-145">권한 부여 토큰은 **설정**의 **권한 부여 토큰** 페이지에서 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-145">Authorization tokens are managed on the **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="8d2ee-146">토큰을 다시 생성할 수 있지만 이 절차를 수행하면 이전 토큰에 대한 액세스 권한이 취소됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-146">You can regenerate them, but this procedure revokes access to the previous token.</span></span>

### <span data-ttu-id="8d2ee-147"><a name="accessingDatasets"></a>로컬 Python 응용 프로그램에서 데이터 집합에 액세스</span><span class="sxs-lookup"><span data-stu-id="8d2ee-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="8d2ee-148">Machine Learning Studio의 왼쪽에 있는 탐색 모음에서 **데이터 집합** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-148">In Machine Learning Studio, click **DATASETS** in the navigation bar on the left.</span></span>
2. <span data-ttu-id="8d2ee-149">액세스하려는 데이터 집합을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-149">Select the dataset you would like to access.</span></span> <span data-ttu-id="8d2ee-150">**내 데이터 집합** 목록 또는 **샘플** 목록에서 데이터 집합을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-150">You can select any of the datasets from the **MY DATASETS** list or from the **SAMPLES** list.</span></span>
3. <span data-ttu-id="8d2ee-151">아래 쪽 도구 모음에서 **데이터 액세스 코드 생성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-151">From the bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="8d2ee-152">데이터가 Python 클라이언트 라이브러리와 호환되지 않는 형식이면 이 단추는 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-152">If the data is in a format incompatible with the Python client library, this button is disabled.</span></span>
   
    ![데이터 집합][datasets]
4. <span data-ttu-id="8d2ee-154">표시되는 창에서 코드 조각을 선택하여 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-154">Select the code snippet from the window that appears and copy it to your clipboard.</span></span>
   
    ![액세스 코드][dataset-access-code]
5. <span data-ttu-id="8d2ee-156">코드를 로컬 Python 응용 프로그램의 Notebook에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-156">Paste the code into the notebook of your local Python application.</span></span>
   
    ![노트북][ipython-dataset]

## <span data-ttu-id="8d2ee-158"><a name="accessingIntermediateDatasets"></a>기계 학습 실험에서 중간 데이터 집합에 액세스</span><span class="sxs-lookup"><span data-stu-id="8d2ee-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="8d2ee-159">기계 학습 스튜디오에서 실험을 실행하고 나면 모듈의 출력 노드에서 중간 데이터 집합에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-159">After an experiment is run in the Machine Learning Studio, it is possible to access the intermediate datasets from the output nodes of modules.</span></span> <span data-ttu-id="8d2ee-160">중간 데이터 집합은 모델 도구가 실행될 때 중간 단계를 위해 생성되고 사용된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="8d2ee-161">데이터 형식이 Python 클라이언트 라이브러리와 호환되는 한 중간 데이터 집합에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-161">Intermediate datasets can be accessed as long as the data format is compatible with the Python client library.</span></span>

<span data-ttu-id="8d2ee-162">지원되는 형식은 다음과 같습니다(해당 상수는 `azureml.DataTypeIds` 클래스에 있음).</span><span class="sxs-lookup"><span data-stu-id="8d2ee-162">The following formats are supported (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="8d2ee-163">일반 텍스트</span><span class="sxs-lookup"><span data-stu-id="8d2ee-163">PlainText</span></span>
* <span data-ttu-id="8d2ee-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="8d2ee-164">GenericCSV</span></span>
* <span data-ttu-id="8d2ee-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="8d2ee-165">GenericTSV</span></span>
* <span data-ttu-id="8d2ee-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="8d2ee-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="8d2ee-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="8d2ee-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="8d2ee-168">모듈 출력 노드 위에 포인터를 두면 형식을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-168">You can determine the format by hovering over a module output node.</span></span> <span data-ttu-id="8d2ee-169">도구 설명에 노드 이름과 함께 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-169">It is displayed along with the node name, in a tooltip.</span></span>

<span data-ttu-id="8d2ee-170">[분할][split] 모듈과 같은 일부 모듈은 Python 클라이언트 라이브러리에서 지원하지 않는 `Dataset`라는 형식으로 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-170">Some of the modules, such as the [Split][split] module, output to a format named `Dataset`, which is not supported by the Python client library.</span></span>

![데이터 집합 형식][dataset-format]

<span data-ttu-id="8d2ee-172">[CSV로 변환][convert-to-csv]과 같은 변환 모듈을 사용하여 출력을 지원되는 형식으로 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-172">You need to use a conversion module, such as [Convert to CSV][convert-to-csv], to get an output into a supported format.</span></span>

![GenericCSV 형식][csv-format]

<span data-ttu-id="8d2ee-174">다음 단계에서는 실험을 만들고 실행하며 중간 데이터 집합에 액세스하는 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-174">The following steps show an example that creates an experiment, runs it and accesses the intermediate dataset.</span></span>

1. <span data-ttu-id="8d2ee-175">새로운 실험 만들기</span><span class="sxs-lookup"><span data-stu-id="8d2ee-175">Create a new experiment.</span></span>
2. <span data-ttu-id="8d2ee-176">**성인 인구 조사 소득 이진 분류 데이터 집합** 모듈을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="8d2ee-177">[분할][split] 모듈을 삽입하고 입력을 데이터 집합 모듈 출력에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-177">Insert a [Split][split] module, and connect its input to the dataset module output.</span></span>
4. <span data-ttu-id="8d2ee-178">[CSV로 변환][convert-to-csv] 모듈을 삽입하고 입력을 [분할][split] 모듈 출력 중 하나에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-178">Insert a [Convert to CSV][convert-to-csv] module and connect its input to one of the [Split][split] module outputs.</span></span>
5. <span data-ttu-id="8d2ee-179">실험을 저장하고, 실행하며, 실행이 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-179">Save the experiment, run it, and wait for it to finish running.</span></span>
6. <span data-ttu-id="8d2ee-180">[CSV로 변환][convert-to-csv] 모듈에서 출력 노드를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-180">Click the output node on the [Convert to CSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="8d2ee-181">상황에 맞는 메뉴가 표시되면 **데이터 액세스 코드 생성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-181">When the context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![상황에 맞는 메뉴][experiment]
8. <span data-ttu-id="8d2ee-183">표시되는 창에서 코드 조각을 선택하여 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-183">Select the code snippet and copy it to your clipboard from the window that appears.</span></span>
   
    ![액세스 코드][intermediate-dataset-access-code]
9. <span data-ttu-id="8d2ee-185">노트북에 코드를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-185">Paste the code in your notebook.</span></span>
   
    ![노트북][ipython-intermediate-dataset]
10. <span data-ttu-id="8d2ee-187">Matplotlib를 사용하여 데이터를 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-187">You can visualize the data using matplotlib.</span></span> <span data-ttu-id="8d2ee-188">그러면 나이 열에 대한 히스토그램에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-188">This displays in a histogram for the age column:</span></span>
    
    ![히스토그램][ipython-histogram]

## <span data-ttu-id="8d2ee-190"><a name="clientApis"></a>기계 학습 Python 클라이언트 라이브러리를 사용하여 데이터 집합에 액세스, 읽기, 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="8d2ee-190"><a name="clientApis"></a>Use the Machine Learning Python client library to access, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="8d2ee-191">작업 영역</span><span class="sxs-lookup"><span data-stu-id="8d2ee-191">Workspace</span></span>
<span data-ttu-id="8d2ee-192">작업 영역은 Python 클라이언트 라이브러리의 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-192">The workspace is the entry point for the Python client library.</span></span> <span data-ttu-id="8d2ee-193">`Workspace` 클래스에 인스턴스를 생성할 작업 영역 ID와 권한 부여 토큰을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-193">Provide the `Workspace` class with your workspace id and authorization token to create an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="8d2ee-194">데이터 집합 열거</span><span class="sxs-lookup"><span data-stu-id="8d2ee-194">Enumerate datasets</span></span>
<span data-ttu-id="8d2ee-195">지정된 작업 영역에 모든 데이터 집합 열거:</span><span class="sxs-lookup"><span data-stu-id="8d2ee-195">To enumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="8d2ee-196">사용자 생성 데이터 집합만 열거:</span><span class="sxs-lookup"><span data-stu-id="8d2ee-196">To enumerate just the user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="8d2ee-197">예제 데이터 집합만 열거:</span><span class="sxs-lookup"><span data-stu-id="8d2ee-197">To enumerate just the example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="8d2ee-198">데이터 집합 이름(대/소문자 구분)으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="8d2ee-199">또는 인덱스별로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="8d2ee-200">Metadata</span><span class="sxs-lookup"><span data-stu-id="8d2ee-200">Metadata</span></span>
<span data-ttu-id="8d2ee-201">데이터 집합에는 콘텐츠 외에도 메타 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-201">Datasets have metadata, in addition to content.</span></span> <span data-ttu-id="8d2ee-202">(중간 데이터 집합은 이 규칙의 예외로서, 메타 데이터가 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="8d2ee-202">(Intermediate datasets are an exception to this rule and do not have any metadata.)</span></span>

<span data-ttu-id="8d2ee-203">일부 메타 데이터 값은 사용자가 생성 시 할당:</span><span class="sxs-lookup"><span data-stu-id="8d2ee-203">Some metadata values are assigned by the user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="8d2ee-204">다른 메타 데이터 값은 Azure 기계 학습에서 할당:</span><span class="sxs-lookup"><span data-stu-id="8d2ee-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="8d2ee-205">사용 가능한 메타 데이터에 대한 자세한 내용은 `SourceDataset` 클래스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-205">See the `SourceDataset` class for more on the available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="8d2ee-206">콘텐츠 읽기</span><span class="sxs-lookup"><span data-stu-id="8d2ee-206">Read contents</span></span>
<span data-ttu-id="8d2ee-207">기계 학습 스튜디오에서 제공한 코드 조각은 자동으로 다운로드하여 Pandas DataFrame 개체에 데이터 집합을 역직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-207">The code snippets provided by Machine Learning Studio automatically download and deserialize the dataset to a Pandas DataFrame object.</span></span> <span data-ttu-id="8d2ee-208">이 작업은 `to_dataframe` 메서드를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-208">This is done with the `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="8d2ee-209">원시 데이터를 다운로드하고 직접 역직렬화를 수행하려는 경우 옵션으로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-209">If you prefer to download the raw data, and perform the deserialization yourself, that is an option.</span></span> <span data-ttu-id="8d2ee-210">현재로서는 Python 클라이언트 라이브러리에서 역직렬화할 수 없는 ‘ARFF’와 같은 형식의 경우에만 선택 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-210">At the moment, this is the only option for formats such as 'ARFF', which the Python client library cannot deserialize.</span></span>

<span data-ttu-id="8d2ee-211">텍스트로 콘텐츠 읽기:</span><span class="sxs-lookup"><span data-stu-id="8d2ee-211">To read the contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="8d2ee-212">이진을 콘텐츠 읽기:</span><span class="sxs-lookup"><span data-stu-id="8d2ee-212">To read the contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="8d2ee-213">콘텐츠에 스트림만 열 수도 있음:</span><span class="sxs-lookup"><span data-stu-id="8d2ee-213">You can also just open a stream to the contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="8d2ee-214">새 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="8d2ee-214">Create a new dataset</span></span>
<span data-ttu-id="8d2ee-215">Python 클라이언트 라이브러리를 사용하면 Python 프로그램에서 데이터 집합을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-215">The Python client library allows you to upload datasets from your Python program.</span></span> <span data-ttu-id="8d2ee-216">이러한 데이터 집합은 작업 영역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="8d2ee-217">Pandas DataFrame에 데이터가 있는 경우 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-217">If you have your data in a Pandas DataFrame, use the following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="8d2ee-218">데이터가 이미 직렬화된 경우 다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="8d2ee-219">Python 클라이언트 라이브러리에서 Pandas DataFrame을 다음 형식으로 직렬화할 수 있습니다(해당 상수는 `azureml.DataTypeIds` 클래스에 있음).</span><span class="sxs-lookup"><span data-stu-id="8d2ee-219">The Python client library is able to serialize a Pandas DataFrame to the following formats (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="8d2ee-220">일반 텍스트</span><span class="sxs-lookup"><span data-stu-id="8d2ee-220">PlainText</span></span>
* <span data-ttu-id="8d2ee-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="8d2ee-221">GenericCSV</span></span>
* <span data-ttu-id="8d2ee-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="8d2ee-222">GenericTSV</span></span>
* <span data-ttu-id="8d2ee-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="8d2ee-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="8d2ee-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="8d2ee-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="8d2ee-225">기존 데이터 집합 업데이트</span><span class="sxs-lookup"><span data-stu-id="8d2ee-225">Update an existing dataset</span></span>
<span data-ttu-id="8d2ee-226">기존 데이터 집합과 일치하는 이름으로 새 데이터 집합을 업로드하려고 하면 충돌 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-226">If you try to upload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="8d2ee-227">기존 데이터 집합을 업데이트하려면 먼저 기존 데이터 집합에 대한 참조를 얻어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-227">To update an existing dataset, you first need to get a reference to the existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="8d2ee-228">그러면 `update_from_dataframe` 을 사용하여 Azure에서 데이터 집합의 콘텐츠를 직렬화하고 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-228">Then use `update_from_dataframe` to serialize and replace the contents of the dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="8d2ee-229">데이터를 다른 형식으로 직렬화하려면 선택적 `data_type_id` 매개 변수의 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-229">If you want to serialize the data to a different format, specify a value for the optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="8d2ee-230">`description` 매개 변수의 값을 지정하여 선택적으로 새 설명을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-230">You can optionally set a new description by specifying a value for the `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up to feb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to feb 2015'

<span data-ttu-id="8d2ee-231">`name` 매개 변수의 값을 지정하여 선택적으로 새로운 이름을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-231">You can optionally set a new name by specifying a value for the `name` parameter.</span></span> <span data-ttu-id="8d2ee-232">지금부터 새 이름만 사용하여 데이터 집합을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-232">From now on, you'll retrieve the dataset using the new name only.</span></span> <span data-ttu-id="8d2ee-233">다음 코드에서는 데이터, 이름 및 설명을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-233">The following code updates the data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up to feb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up to feb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="8d2ee-234">`data_type_id`, `name` 및 `description` 매개 변수는 선택 사항이고 기본적으로 이전 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-234">The `data_type_id`, `name` and `description` parameters are optional and default to their previous value.</span></span> <span data-ttu-id="8d2ee-235">`dataframe` 매개 변수는 항상 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-235">The `dataframe` parameter is always required.</span></span>

<span data-ttu-id="8d2ee-236">데이터가 이미 직렬화된 경우 `update_from_dataframe` 대신 `update_from_raw_data`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="8d2ee-237">`dataframe` 대신 `raw_data`만 전달하면, 비슷하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="8d2ee-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

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

