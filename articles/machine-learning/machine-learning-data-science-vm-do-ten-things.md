---
title: "데이터 과학 가상 컴퓨터에서 수행할 수 있는 10가지 작업 | Microsoft 문서"
description: "데이터 과학 가상 컴퓨터에서 다양한 데이터 탐색 및 모델링 작업을 수행합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 145dfe3e-2bd2-478f-9b6e-99d97d789c62
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;weig;bradsev
ms.openlocfilehash: 45af1cd3a05b483429d2307659f1882ef28921f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="ten-things-you-can-do-on-the-data-science-virtual-machine"></a><span data-ttu-id="4406b-103">데이터 과학 가상 컴퓨터로 할 수 있는 10가지 일</span><span class="sxs-lookup"><span data-stu-id="4406b-103">Ten things you can do on the Data science Virtual Machine</span></span>
<span data-ttu-id="4406b-104">Microsoft DSVM(데이터 과학 가상 컴퓨터)은 다양한 데이터 탐색 및 모델링 작업을 수행할 수 있는 강력한 데이터 과학 개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-104">The Microsoft Data Science Virtual Machine (DSVM) is a powerful data science development environment that enables you to perform various data exploration and modeling tasks.</span></span> <span data-ttu-id="4406b-105">이 환경에는 온-프레미스, 클라우드 또는 하이브리드 배포에 대한 간편하고 신속하게 분석을 시작할 수 있는 여러 대중적인 분석 도구가 기본적으로 내장되고 번들로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-105">The environment comes already built and bundled with several popular data analytics tools that make it easy to get started quickly with your analysis for On-premises, Cloud or hybrid deployments.</span></span> <span data-ttu-id="4406b-106">DSVM은 여러 Azure 서비스와 긴밀하게 연동하며 Azure의 Azure SQL Data Warehouse, Azure Data Lake, Azure Storage 또는 Azure Cosmos DB에 저장된 데이터를 읽고 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-106">The DSVM works closely with many Azure services and is able to read and process data that is already stored on Azure, in Azure SQL Data Warehouse, Azure Data Lake, Azure Storage, or in Azure Cosmos DB.</span></span> <span data-ttu-id="4406b-107">또한 Azure 기계 학습 및 Azure Data Factory와 같은 기타 분석 도구를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-107">It can also leverage other analytics tools such as Azure Machine Learning and Azure Data Factory.</span></span>

<span data-ttu-id="4406b-108">이 문서에서는 DSVM을 사용하여 다양한 데이터 과학 작업을 수행하고 다른 Azure 서비스와 상호 작용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-108">In this article we walk you through how to use your DSVM to perform various data science tasks and interact with other Azure services.</span></span> <span data-ttu-id="4406b-109">다음은 DSVM에서 수행할 수 있는 작업 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-109">Here are some of the things you can do on the DSVM:</span></span>

1. <span data-ttu-id="4406b-110">Microsoft R 서버, Python을 사용하여 DSVM에서 로컬로 데이터 탐색 및 모델 개발</span><span class="sxs-lookup"><span data-stu-id="4406b-110">Explore data and develop models locally on the DSVM using Microsoft R Server, Python</span></span>
2. <span data-ttu-id="4406b-111">Jupyter Notebook에서 Python 2, Python 3 그리고 확장성 및 성능 위주로 설계된 R의 엔터프라이즈급 버전인 Microsoft R을 사용하여 브라우저에서 데이터 실험</span><span class="sxs-lookup"><span data-stu-id="4406b-111">Use a Jupyter notebook to experiment with your data on a browser using Python 2, Python 3, Microsoft R an enterprise ready version of R designed for scalability and performance</span></span>
3. <span data-ttu-id="4406b-112">클라이언트 응용 프로그램이 간단한 웹 서비스 인터페이스를 사용하여 모델에 액세스할 수 있도록 Azure 기계 학습에서 R 및 Python을 사용하여 구축된 모델 운영</span><span class="sxs-lookup"><span data-stu-id="4406b-112">Operationalize models built using R and Python on Azure Machine Learning so client applications can access your models using a simple web services interface</span></span>
4. <span data-ttu-id="4406b-113">Azure Portal 또는 Powershell을 사용하여 Azure 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="4406b-113">Administer your Azure resources using  Azure portal or Powershell</span></span>
5. <span data-ttu-id="4406b-114">Azure File Storage를 DSVM에 탑재 가능한 드라이브로 만들어 저장소 공간을 확장하고 전체 팀에서 대규모 데이터 집합/코드 공유</span><span class="sxs-lookup"><span data-stu-id="4406b-114">Extend your storage space and share large-scale datasets / code across your whole team by creating an Azure File storage as a mountable drive on your DSVM</span></span>
6. <span data-ttu-id="4406b-115">GitHub를 사용하여 팀과 코드를 공유하고 사전 설치된 Git 클라이언트(Git Bash Git GUI)를 사용하여 리포지토리에 액세스</span><span class="sxs-lookup"><span data-stu-id="4406b-115">Share code with your team using GitHub and access your repository using the pre-installed Git clients - Git Bash, Git GUI.</span></span>
7. <span data-ttu-id="4406b-116">Azure Blob Storage, Azure Data Lake, Azure HDInsight(Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse, 데이터베이스 등의 다양한 Azure 데이터 및 분석 서비스에 액세스</span><span class="sxs-lookup"><span data-stu-id="4406b-116">Access various Azure data and analytics services like Azure blob storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse & databases</span></span>
8. <span data-ttu-id="4406b-117">DSVM에 사전 설치된 Power BI Desktop을 사용하여 보고서 및 대시보드를 구축하여 클라우드에 배포</span><span class="sxs-lookup"><span data-stu-id="4406b-117">Build reports and dashboard using the Power BI Desktop pre-installed on the DSVM and deploy them on the cloud</span></span>
9. <span data-ttu-id="4406b-118">프로젝트 요구 사항에 맞게 DSVM을 동적으로 확장</span><span class="sxs-lookup"><span data-stu-id="4406b-118">Dynamically scale your DSVM to meet your project needs</span></span>
10. <span data-ttu-id="4406b-119">가상 컴퓨터에 추가 도구 설치</span><span class="sxs-lookup"><span data-stu-id="4406b-119">Install additional tools on your virtual machine</span></span>   

> [!NOTE]
> <span data-ttu-id="4406b-120">이 문서에 나열된 추가 데이터 저장소 및 분석 서비스의 대부분에 대해서는 추가 사용 요금이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-120">Additional usage charges apply for many of the additional data storage and analytics services listed in this article.</span></span> <span data-ttu-id="4406b-121">자세한 내용은 [Azure 가격 책정](https://azure.microsoft.com/pricing/) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4406b-121">Please refer to the [Azure Pricing](https://azure.microsoft.com/pricing/) page for details.</span></span>
> 
> 

<span data-ttu-id="4406b-122">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="4406b-122">**Prerequisites**</span></span>

* <span data-ttu-id="4406b-123">Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-123">You need an Azure subscription.</span></span> <span data-ttu-id="4406b-124">[여기](https://azure.microsoft.com/free/)서 평가판에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-124">You can sign up for a free trial [here](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="4406b-125">Azure 포털에서 데이터 과학 가상 컴퓨터를 프로비전하는 방법에 대한 지침은 [가상 컴퓨터 만들기](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-125">Instructions for provisioning a Data Science Virtual Machine on the Azure portal are available at [Creating a virtual machine](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span></span>

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a><span data-ttu-id="4406b-126">1. Microsoft R 서버 또는 Python을 사용하여 데이터 탐색 및 모델 개발</span><span class="sxs-lookup"><span data-stu-id="4406b-126">1. Explore data and develop models using Microsoft R Server or Python</span></span>
<span data-ttu-id="4406b-127">R 및 Python 같은 언어를 사용하여 DSVM에서 바로 데이터를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-127">You can use languages like R and Python to do your data analytics right on the DSVM.</span></span>

<span data-ttu-id="4406b-128">R의 경우 시작 메뉴 또는 바탕 화면에서 찾을 수 있는 "Revolution R Enterprise 8.0"이라는 IDE를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-128">For R, you can use an IDE called "Revolution R Enterprise 8.0" that can be found on the start menu or the desktop.</span></span> <span data-ttu-id="4406b-129">Microsoft는 병렬로 청크된 분석을 수행하여 확장 가능한 분석을 지원하고 허용된 메모리 크기를 초과하는 데이터를 분석할 수 있도록 오픈 소스/CRAN-R 기반의 추가 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-129">Microsoft has provided additional libraries on top of the Open source/CRAN-R to enable scalable analytics and the ability to analyze data larger than the memory size allowed by doing parallel chunked analysis.</span></span> <span data-ttu-id="4406b-130">[RStudio](https://www.rstudio.com/products/rstudio-desktop/)와 같은 선택으로 R IDE를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-130">You can also install an R IDE of your choice like [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span></span>

<span data-ttu-id="4406b-131">Python의 경우 PTVS(Python Tools for Visual Studio) 확장 기능이 사전 설치된 Visual Studio Community Edition 같은 IDE를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-131">For Python, you can use an IDE like Visual Studio Community Edition which has the Python Tools for Visual Studio (PTVS) extension pre-installed.</span></span> <span data-ttu-id="4406b-132">기본적으로 기본 Python 2.7만(SciKit, Pandas 같은 분석 라이브러리 없이) PTVS에 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-132">By default, only a basic Python 2.7 is configured on PTVS (without any analytics library like SciKit, Pandas).</span></span> <span data-ttu-id="4406b-133">Anaconda Python 2.7 및 3.5를 사용하려면 다음 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-133">In order to enable Anaconda Python 2.7 and 3.5, you need to do the following:</span></span>

* <span data-ttu-id="4406b-134">**도구** -> **Python 도구** -> **Python 환경**으로 이동한 다음 Visual Studio 2015 Community Edition에서 "**+ 사용자 지정**"을 클릭하여 각 버전에 대해 사용자 지정 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-134">Create custom environments for each version by navigating to **Tools** -> **Python Tools** -> **Python Environments** and then clicking "**+ Custom**" in the Visual Studio 2015 Community Edition</span></span>
* <span data-ttu-id="4406b-135">설명을 입력하고 Anaconda Python 2.7에는 환경 접두사 *c:\anaconda*를, Anaconda Python 3.5에는 환경 접두사 *c:\anaconda\envs\py35*를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-135">Give a description and set the environment prefix paths as *c:\anaconda* for Anaconda Python 2.7 OR *c:\anaconda\envs\py35* for Anaconda Python 3.5</span></span>
* <span data-ttu-id="4406b-136">**자동 감지**를 클릭한 다음 **적용**을 클릭하여 환경을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-136">Click **Auto Detect** and then **Apply** to save the environment.</span></span>

<span data-ttu-id="4406b-137">Visual Studio에서 사용자 지정 환경 설정이 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-137">Here is what the custom environment setup looks like in Visual Studio.</span></span>

![PTVS 설치](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

<span data-ttu-id="4406b-139">Python 환경을 만드는 방법에 대한 자세한 내용은 [PTVS 설명서](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4406b-139">See the [PTVS documentation](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) for additional details on how to create Python Environments.</span></span>

<span data-ttu-id="4406b-140">이제 새 Python 프로젝트를 만들 수 있도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-140">Now you are set up to create a new Python project.</span></span> <span data-ttu-id="4406b-141">**파일** -> **새로 만들기** -> **프로젝트** -> **Python**으로 이동하고 작성하는 Python 응용 프로그램의 종류를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-141">Navigate to **File** -> **New** -> **Project** -> **Python** and select the type of Python application you are building.</span></span> <span data-ttu-id="4406b-142">현재 프로젝트에 대한 Python 환경을 원하는 버전(Anaconda 2.7 또는 3.5)으로 설정할 수 있습니다. **Python 환경**을 마우스 오른쪽 단추로 클릭하고 **Python 환경 추가/제거**를 선택한 다음 프로젝트와 연결할 원하는 환경을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-142">You can set the Python environment for the current project to the desired version (Anaconda 2.7 or 3.5): right-click the **Python environment**, select **Add/Remove Python Environments**, and then select the desired environment to associate with the project.</span></span> <span data-ttu-id="4406b-143">제품 [설명서](https://github.com/Microsoft/PTVS/wiki) 페이지에서 PTVS 작업에 대한 자세한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-143">You can find more information about working with PTVS on the product [documentation](https://github.com/Microsoft/PTVS/wiki) page.</span></span>

## <a name="2-using-a-jupyter-notebook-to-explore-and-model-your-data-with-python-or-r"></a><span data-ttu-id="4406b-144">2. Jupyter Notebook에서 Python 또는 R을 사용하여 데이터 탐색 및 모델링</span><span class="sxs-lookup"><span data-stu-id="4406b-144">2. Using a Jupyter Notebook to explore and model your data with Python or R</span></span>
<span data-ttu-id="4406b-145">Jupyter Notebook은 데이터 탐색 및 모델링을 위한 브라우저 기반 "IDE"를 제공하는 강력한 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-145">The Jupyter Notebook is a powerful environment that provides a browser-based "IDE" for data exploration and modeling.</span></span> <span data-ttu-id="4406b-146">Jupyter Notebook에서 Python 2, Python 3 또는 R(오픈 소스 및 Microsoft R 서버 모두)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-146">You can use Python 2, Python 3 or R (both Open Source and the Microsoft R Server) in a Jupyter Notebook.</span></span>

<span data-ttu-id="4406b-147">Jupyter Notebook을 실행하려면 **Jupyter Notebook**이라는 시작 메뉴 아이콘/바탕 화면 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-147">To launch the Jupyter Notebook click on the start menu icon / desktop icon titled **Jupyter Notebook**.</span></span> <span data-ttu-id="4406b-148">DSVM에서 "https://localhost:9999/"를 탐색하여 Jupiter Notebook에 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-148">On the DSVM you can also browse to "https://localhost:9999/" to access the Jupiter Notebook.</span></span> <span data-ttu-id="4406b-149">암호를 요청하는 경우 [Microsoft 데이터 과학 가상 컴퓨터 프로비전](machine-learning-data-science-provision-vm.md) 항목의 ***Jupyter Notebook 서버에 강력한 암호를 만드는 방법*** 섹션에서 제공하는 지침을 사용하여 Jupyter Notebook 액세스를 위한 강력한 암호를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-149">If it prompts you for a password, use instructions provided in the ***How to create a strong password on the Jupyter notebook server*** section of the [Provision the Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md) topic to create a strong password to access the Jupyter notebook.</span></span> 

<span data-ttu-id="4406b-150">Notebook을 열면 DSVM에 사전 패키지된 예제 Notebook 몇 개가 포함된 디렉터리가 보일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-150">Once you have opened the notebook, you should see a directory that contains a few example notebooks that are pre-packaged into the DSVM.</span></span> <span data-ttu-id="4406b-151">이제 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-151">Now you can:</span></span>

* <span data-ttu-id="4406b-152">Notebook을 클릭하면 코드가 보입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-152">click on the notebook to see the code.</span></span>
* <span data-ttu-id="4406b-153">**SHIFT-ENTER**를 눌러 각 셀 실행</span><span class="sxs-lookup"><span data-stu-id="4406b-153">execute each cell by pressing **SHIFT-ENTER**.</span></span>
* <span data-ttu-id="4406b-154">**셀** -> **실행**을 클릭하여 전체 Notebook을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-154">run the entire notebook by clicking on **Cell** -> **Run**</span></span>
* <span data-ttu-id="4406b-155">Jupyter 아이콘(왼쪽 상단 모서리)을 클릭하고 오른쪽에 있는 **새로 만들기** 단추를 클릭한 다음 Notebook 언어(커널이라고도 함)를 선택하여 새 Notebook을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-155">create a new notebook by clicking on the Jupyter Icon (left top corner) and then clicking **New** button on the right and then choosing the notebook language (also known as kernels).</span></span>   

> [!NOTE]
> <span data-ttu-id="4406b-156">현재 Python 2.7, Python 3.5 및 R이 지원됩니다. R 커널은 오픈 소스 R과 엔터프라이즈급 확장 가능 Microsoft R 서버 양쪽에서 프로그래밍을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-156">Currently we support Python 2.7, Python 3.5 and R. The R kernel supports programming in both Open source R as well as the enterprise scalable Microsoft R Server.</span></span>   
> 
> 

<span data-ttu-id="4406b-157">Notebook에 액세스한 다음에는 데이터를 탐색하고, 모델을 구축하고, 선택한 라이브러리로 모델을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-157">Once you are in the notebook you can explore your data, build the model, test the model using your choice of libraries.</span></span>

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a><span data-ttu-id="4406b-158">3. R 또는 Python을 사용하여 모델을 구축하고 Azure 기계 학습을 사용하여 운영</span><span class="sxs-lookup"><span data-stu-id="4406b-158">3. Build models using R or Python and Operationalize them using Azure Machine Learning</span></span>
<span data-ttu-id="4406b-159">모델을 구축하고 유효성을 검사한 후에는 일반적으로 프로덕션 환경에 모델을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-159">Once you have built and validated your model the next step is usually to deploy it into production.</span></span> <span data-ttu-id="4406b-160">이렇게 하면 클라이언트 응용 프로그램에서 실시간으로 또는 배치 모드 기준으로 예측 모델을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-160">This allows your client applications to invoke the model predictions on a real time or on a batch mode basis.</span></span> <span data-ttu-id="4406b-161">Azure 기계 학습은 R 또는 Python에서 구축된 모델을 운영하는 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-161">Azure Machine Learning provides a mechanism to operationalize a model built in either R or Python.</span></span>

<span data-ttu-id="4406b-162">Azure 기계 학습에서 모델을 운영하면 클라이언트가 입력 매개 변수를 전달하고 그에 대한 출력으로 모델로부터 예측을 수신하는 REST 호출을 만들 수 있도록 웹 서비스가 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-162">When you operationalize your model in Azure Machine Learning, a web service is exposed that allows clients to make REST calls that pass in input parameters and receive predictions from the model as outputs.</span></span>   

> [!NOTE]
> <span data-ttu-id="4406b-163">아직 Azure Machine Learning에 등록하지 않은 경우 [Azure Machine Learning Studio](https://studio.azureml.net/) 홈페이지에서 "시작"을 클릭하여 무료 작업 영역 또는 표준 작업 영역을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-163">If you have not yet signed up for Azure Machine Learning, you can obtain a free workspace or a standard workspace by visiting the [Azure Machine Learning Studio](https://studio.azureml.net/) home page and clicking on "Get Started".</span></span>   
> 
> 

### <a name="build-and-operationalize-python-models"></a><span data-ttu-id="4406b-164">Python 모델 구축 및 운영</span><span class="sxs-lookup"><span data-stu-id="4406b-164">Build and Operationalize Python models</span></span>
<span data-ttu-id="4406b-165">SciKit-학습 라이브러리를 사용하여 간단한 모델을 작성하는 Python Jupyter Notebook에서 개발된 코드의 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-165">Here is a snippet of code developed in a Python Jupyter Notebook that builds a simple model using the SciKit-learn library.</span></span>

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

<span data-ttu-id="4406b-166">Azure 기계 학습에 python 모델을 배포하는 데 사용되는 메서드는 함수로 모델의 예측을 래핑하고 Azure 기계 학습 작업 영역 ID, API 키 및 입력을 표시하고 매개 변수를 반환하는 사전 설치된 Azure 기계 학습 python 라이브러리에서 제공하는 특성으로 데코레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-166">The method used to deploy your python models to Azure Machine Learning wraps the prediction of the model into a function and decorates it with attributes provided by the pre-installed Azure Machine Learning python library that denote your Azure Machine Learning workspace ID, API Key, and the input and return parameters.</span></span>  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

<span data-ttu-id="4406b-167">이제 클라이언트에서 웹 서비스에 대한 호출을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-167">A client can now make calls to the web service.</span></span> <span data-ttu-id="4406b-168">REST API 요청을 작성하는 간편한 래퍼가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-168">There are convenience wrappers that construct the REST API requests.</span></span> <span data-ttu-id="4406b-169">다음은 웹 서비스를 사용하는 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-169">Here is a sample code to consume the web service.</span></span>

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> <span data-ttu-id="4406b-170">Azure 기계 학습 라이브러리는 현재 Python 2.7에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-170">The Azure Machine Learning library is only supported on Python 2.7 currently.</span></span>   
> 
> 

### <a name="build-and-operationalize-r-models"></a><span data-ttu-id="4406b-171">R 모델 구축 및 운영</span><span class="sxs-lookup"><span data-stu-id="4406b-171">Build and Operationalize R models</span></span>
<span data-ttu-id="4406b-172">구축된 R 모델을 Python에서 사용한 방법과 비슷한 방법으로 데이터 과학 가상 컴퓨터 또는 Azure 기계 학습의 다른 위치에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-172">You can deploy R models built on the Data Science Virtual Machine or elsewhere onto Azure Machine Learning in a manner that is similar to how it is done for Python.</span></span> <span data-ttu-id="4406b-173">단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-173">Her are the steps:</span></span>

* <span data-ttu-id="4406b-174">다음 코드 예제와 같이 작업 영역 ID 및 인증 토큰을 제공하는 settings.json 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-174">create a settings.json file to provide your workspace ID and auth token as shown in the following code sample.</span></span>
* <span data-ttu-id="4406b-175">모델의 예측 함수에 대한 래퍼를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-175">write a wrapper for the model's predict function.</span></span>
* <span data-ttu-id="4406b-176">Azure 기계 학습 라이브러리에서 ```publishWebService``` 를 호출하여 함수 래퍼에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-176">call ```publishWebService``` in the Azure Machine Learning library to pass in the function wrapper.</span></span>  

<span data-ttu-id="4406b-177">Azure Machine Learning에서 모델을 설정, 작성, 게시하고 웹 서비스로 사용하는 데 활용할 수 있는 절차와 코드 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-177">Here is the procedure and code snippets that can be used to set up, build, publish, and consume a model as a web service in Azure Machine Learning.</span></span>

#### <a name="setup"></a><span data-ttu-id="4406b-178">설정</span><span class="sxs-lookup"><span data-stu-id="4406b-178">Setup</span></span>
1. <span data-ttu-id="4406b-179">Revolution R Enterprise 8.0 IDE 또는 R IDE에 ```install.packages("AzureML")``` 를 입력하여 Machine Learning R 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-179">Install the Machine Learning R package by typing ```install.packages("AzureML")``` in Revolution R Enterprise 8.0 IDE or your R IDE.</span></span>
2. <span data-ttu-id="4406b-180">[여기](https://cran.r-project.org/bin/windows/Rtools/)에서 RTools를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-180">Download RTools from [here](https://cran.r-project.org/bin/windows/Rtools/).</span></span> <span data-ttu-id="4406b-181">Machine Learning으로 R 패키지를 운영하기 위해 경로(및 명명된 zip.exe)에 zip 유틸리티가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-181">You need the zip utility in the path (and named zip.exe) to operationalize your R package into Machine Learning.</span></span>
3. <span data-ttu-id="4406b-182">홈 디렉터리 아래의 ```.azureml```이라는 디렉터리 아래에서 settings.json 파일을 만들고 Azure Machine Learning 작업 영역에서 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-182">Create a settings.json file under a directory called ```.azureml``` under your home directory and enter the parameters from your Azure Machine Learning workspace:</span></span>

<span data-ttu-id="4406b-183">settings.json 파일 구조:</span><span class="sxs-lookup"><span data-stu-id="4406b-183">settings.json File structure:</span></span>

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a><span data-ttu-id="4406b-184">R에서 모델을 구축하고 Azure Machine Learning에 게시</span><span class="sxs-lookup"><span data-stu-id="4406b-184">Build a model in R and publish it in Azure Machine Learning</span></span>
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function to publish based on the model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-the-model-deployed-in-azure-machine-learning"></a><span data-ttu-id="4406b-185">Azure Machine Learning에 배포된 모델 사용</span><span class="sxs-lookup"><span data-stu-id="4406b-185">Consume the model deployed in Azure Machine Learning</span></span>
<span data-ttu-id="4406b-186">클라이언트 응용 프로그램의 모델을 사용하기 위해 Azure 기계 학습 라이브러리를 사용하여 끝점을 확인하는 `services` API 호출을 통해 게시된 웹 서비스를 이름으로 조회합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-186">To consume the model from a client application, we use the Azure Machine Learning library to look up the published web service by name using the `services` API call to determine the endpoint.</span></span> <span data-ttu-id="4406b-187">그런 다음 `consume` 함수를 호출하여 예측할 데이터 프레임을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-187">Then you just call the `consume` function and pass in the data frame to be predicted.</span></span>
<span data-ttu-id="4406b-188">다음 코드는 모델을 Azure 기계 학습 웹 서비스로 게시하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-188">The following code is used to consume the model published as an Azure Machine Learning web service.</span></span>

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use the last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

<span data-ttu-id="4406b-189">Azure 기계 학습 R 라이브러리에 대한 자세한 정보는 [여기](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-189">More information about the Azure Machine Learning R library can be found [here](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span></span>

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a><span data-ttu-id="4406b-190">4. Azure 포털 또는 Powershell을 사용하여 Azure 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="4406b-190">4. Administer your Azure resources using Azure portal or Powershell</span></span>
<span data-ttu-id="4406b-191">DSVM을 사용하면 가상 컴퓨터에서 로컬로 분석 솔루션을 구축할 수 있을 뿐만 아니라 Microsoft의 Azure 클라우드 서비스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-191">The DSVM not only allows you to build your analytics solution locally on the virtual machine, but also allows you to access services on Microsoft's Azure cloud.</span></span> <span data-ttu-id="4406b-192">Azure는 DSVM에서 관리 및 액세스할 수 있는 여러 가지 계산, 저장소, 데이터 분석 서비스 및 기타 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-192">Azure provides several compute, storage, data analytics services and other services that you can administer and access from your DSVM.</span></span>

<span data-ttu-id="4406b-193">Azure 구독 및 클라우드 리소스를 관리하려는 경우 브라우저에서 [Azure 포털](https://portal.azure.com)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="4406b-193">To administer your Azure subscription and cloud resources you can use your browser and point to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4406b-194">Azure Powershell을 사용하여 스크립트를 통해 Azure 구독 및 리소스를 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-194">You can also use Azure Powershell to administer your Azure subscription and resources via a script.</span></span>
<span data-ttu-id="4406b-195">바탕 화면의 바로 가기 또는 시작 메뉴의 "Microsoft Azure Powershell"을 사용하여 Azure Powershell을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-195">You can run Azure Powershell from a shortcut on the desktop or from the start menu titled "Microsoft Azure Powershell".</span></span> <span data-ttu-id="4406b-196">Windows Powershell 스크립트를 사용하여 Azure 구독 및 리소스를 관리하는 방법에 대한 자세한 내용은 [Microsoft Azure Powershell 설명서](../powershell-azure-resource-manager.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4406b-196">Refer to [Microsoft Azure Powershell documentation](../powershell-azure-resource-manager.md) for more information on how you can administer your Azure subscription and resources using Windows Powershell scripts.</span></span>

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a><span data-ttu-id="4406b-197">5. 공유 파일 시스템으로 저장소 공간 확장</span><span class="sxs-lookup"><span data-stu-id="4406b-197">5. Extend your storage space with a shared file system</span></span>
<span data-ttu-id="4406b-198">데이터 과학자는 팀 내에서 대용량 데이터 집합, 코드 또는 기타 리소스를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-198">Data scientists can share large datasets, code or other resources within the team.</span></span> <span data-ttu-id="4406b-199">DSVM 자체에는 약 70GB의 사용 가능한 공간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-199">The DSVM itself has about 70GB of space available.</span></span> <span data-ttu-id="4406b-200">저장소를 확장하려면 Azure 파일 서비스를 사용하여 DSVM에 파일을 마운트하거나 REST API를 통해 액세스하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-200">To extend your storage, you can use the Azure File Service and either mount it on the DSVM or access it via a REST API.</span></span>   

> [!NOTE]
> <span data-ttu-id="4406b-201">Azure 파일 서비스 공유의 최대 공간은 5TB이고 개별 파일 크기 제한은 1TB입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-201">The maximum space of the Azure File Service share is 5TB and individual file size limit is 1TB.</span></span>   
> 
> 

<span data-ttu-id="4406b-202">Azure Powershell을 사용하여 Azure 파일 서비스 공유를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-202">You can use Azure Powershell to create an Azure File Service share.</span></span> <span data-ttu-id="4406b-203">다음은 Azure PowerShell에서 실행하여 Azure 파일 서비스 공유를 만들 수 있는 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-203">Here is the script to run under Azure PowerShell to create an Azure File service share.</span></span>

    # Authenticate to Azure.
    Login-AzureRmAccount
    # Select your subscription
    Get-AzureRmSubscription –SubscriptionName "<your subscription name>" | Select-AzureRmSubscription
    # Create a new resource group.
    New-AzureRmResourceGroup -Name <dsvmdatarg>
    # Create a new storage account. You can reuse existing storage account if you wish.
    New-AzureRmStorageAccount -Name <mydatadisk> -ResourceGroupName <dsvmdatarg> -Location "<Azure Data Center Name For eg. South Central US>" -Type "Standard_LRS"
    # Set your current working storage account
    Set-AzureRmCurrentStorageAccount –ResourceGroupName "<dsvmdatarg>" –StorageAccountName <mydatadisk>

    # Create a Azure File Service Share
    $s = New-AzureStorageShare <<teamsharename>>
    # Create a directory under the FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List the share to confirm that everything worked
    Get-AzureStorageFile -Share $s


<span data-ttu-id="4406b-204">Azure 파일 공유를 만들었으니 이제 Azure의 모든 가상 컴퓨터에 파일을 마운트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-204">Now that you have created an Azure file share, you can mount it in any virtual machine in Azure.</span></span> <span data-ttu-id="4406b-205">대기 시간을 줄이고 데이터 전송 요금이 부과되지 않도록 VM과 저장소 계정을 동일한 Azure 데이터 센터에 둘 것을 강력하게 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-205">It is highly recommended that the VM is in same Azure data center as the storage account to avoid latency and data transfer charges.</span></span> <span data-ttu-id="4406b-206">다음은 Azure Powershell에서 실행할 수 있는 드라이브를 DSVM에 마운트하는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-206">Here are the commands to mount the drive on the DSVM that you can run on Azure Powershell.</span></span>

    # Get storage key of the storage account that has the Azure file share from Azure portal. Store it securely on the VM to avoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount the Azure file share as Z: drive on the VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


<span data-ttu-id="4406b-207">이제 VM의 일반적인 드라이브처럼 이 드라이브에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-207">Now you can access this drive as you would any normal drive on the VM.</span></span>

## <a name="6-share-code-with-your-team-using-github"></a><span data-ttu-id="4406b-208">6. GitHub를 사용하여 팀과 코드 공유</span><span class="sxs-lookup"><span data-stu-id="4406b-208">6. Share code with your team using GitHub</span></span>
<span data-ttu-id="4406b-209">GitHub는 개발자 커뮤니티에서 공유하는 다양한 기술을 사용하는 여러 도구를 위한 수많은 샘플 코드 및 소스를 찾을 수 있는 코드 리포지토리입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-209">GitHub is a code repository where you can find a lot of sample code and sources for different tools using various technologies shared by the developer community.</span></span> <span data-ttu-id="4406b-210">Github는 코드 파일 버전을 추적하고 저장하는 기술로 Git를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-210">It uses Git as the technology to track and store versions of the code files.</span></span> <span data-ttu-id="4406b-211">GitHub는 팀의 공유 코드 및 문서를 저장하는 고유의 리포지토리를 만들고, 버전 제어를 구현하고, 코드를 보고 의견을 제시하는 액세스 권한을 제어할 수 있는 플랫폼이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-211">GitHub is also a platform where you can create your own repository to store your team's shared code and documentation, implement version control and also control who have access to view and contribute code.</span></span> <span data-ttu-id="4406b-212">Git 사용에 대한 자세한 내용을 보려면 [GitHub 도움말 페이지](https://help.github.com/)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="4406b-212">Please visit the [GitHub help pages](https://help.github.com/) for more information on using Git.</span></span> <span data-ttu-id="4406b-213">팀과 협력하고, 커뮤니티에서 개발한 코드를 사용하고, 다시 커뮤니티에 코드에 대한 의견을 제시하는 방법 중 하나로 GitHub를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-213">You can use GitHub as one of the ways to collaborate with your team, use code developed by the community and contribute code back to the community.</span></span>

<span data-ttu-id="4406b-214">DSVM은 GitHub 리포지토리에 액세스할 수 있는 클라이언트 도구가 이미 GUI와 명령줄에 내장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-214">The DSVM already comes loaded with client tools on both command-line as well GUI to access GitHub repository.</span></span> <span data-ttu-id="4406b-215">Git 및 GitHub를 사용하는 명령줄 도구는 Git Bash입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-215">The command-line tool to work with Git and GitHub is called Git Bash.</span></span> <span data-ttu-id="4406b-216">DSVM에 설치된 Visual Studio에는 Git 확장 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-216">Visual Studio installed on the DSVM has the Git extensions.</span></span> <span data-ttu-id="4406b-217">시작 메뉴 및 바탕 화면에서 이러한 도구의 시작 아이콘을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-217">You can find start-up icons for these tools on the start menu and the desktop.</span></span>

<span data-ttu-id="4406b-218">GitHub 리포지토리에서 코드를 다운로드하려면 ```git clone``` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-218">To download code from a GitHub repository you use the ```git clone``` command.</span></span> <span data-ttu-id="4406b-219">예를 들어 Microsoft가 현재 디렉터리에 게시한 데이터 과학 리포지토리를 다운로드하려면 ```git-bash```에 액세스한 후 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-219">For example to download data science repository published by Microsoft into the current directory you can run the following command once you are in ```git-bash```.</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="4406b-220">Visual Studio에서 동일한 복제 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-220">In Visual Studio, you can do the same clone operation.</span></span> <span data-ttu-id="4406b-221">아래 스크린샷은 Visual Studio에서 Git 및 GitHub 도구에 액세스하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-221">The  following screen-shot shows how to access Git and GitHub tools in Visual Studio.</span></span>

![Visual Studio의 Git](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

<span data-ttu-id="4406b-223">github.com에서 제공하는 여러 리소스를 통해 Git를 사용하여 GitHub 리포지토리를 작업하는 방법에 대한 자세한 내용을 찾을 수 있습니다. [참고 자료](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) 를 보시면 많은 도움이 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-223">You can find more information on using Git to work with your GitHub repository from several resources available on github.com. The [cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) is a useful reference.</span></span>

## <a name="7-access-various-azure-data-and-analytics-services"></a><span data-ttu-id="4406b-224">7. 다양한 Azure 데이터 및 분석 서비스에 액세스</span><span class="sxs-lookup"><span data-stu-id="4406b-224">7. Access various Azure data and analytics services</span></span>
### <a name="azure-blob"></a><span data-ttu-id="4406b-225">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="4406b-225">Azure Blob</span></span>
<span data-ttu-id="4406b-226">Azure Blob은 크고 작은 데이터를 위한 경제적이면서 안정적인 클라우드 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-226">Azure blob is a reliable, economical cloud storage for data big and small.</span></span> <span data-ttu-id="4406b-227">Azure Blob으로 데이터를 이동하고 Azure Blob에 저장된 데이터에 액세스하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-227">Let us look at how you can move data to Azure Blob and access data stored in an Azure Blob.</span></span>

<span data-ttu-id="4406b-228">**필수 요소**</span><span class="sxs-lookup"><span data-stu-id="4406b-228">**Prerequisite**</span></span>

* <span data-ttu-id="4406b-229">**[Azure 포털](https://portal.azure.com)에서 고유한 Azure Blob 저장소 계정을 만듭니다.**</span><span class="sxs-lookup"><span data-stu-id="4406b-229">**Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).**</span></span>

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="4406b-231">사전 설치된 명령줄 AzCopy 도구를 ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```에서 찾을 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-231">Confirm that the pre-installed command-line AzCopy tool is found at ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span></span> <span data-ttu-id="4406b-232">이 도구를 실행할 때 전체 명령 경로 입력하지 않아도 PATH 환경 변수에 azcopy.exe를 포함하는 디렉터리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-232">You can add the directory containing the azcopy.exe to your PATH environment variable to avoid typing the full command path when running this tool.</span></span> <span data-ttu-id="4406b-233">AzCopy 도구에 대한 자세한 내용은 [AzCopy 설명서](../storage/common/storage-use-azcopy.md)</span><span class="sxs-lookup"><span data-stu-id="4406b-233">For more info on AzCopy tool please refer to [AzCopy documentation](../storage/common/storage-use-azcopy.md)</span></span>
* <span data-ttu-id="4406b-234">Azure 저장소 탐색기 도구를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-234">Start the Azure Storage Explorer tool.</span></span> <span data-ttu-id="4406b-235">이 도구는 [Microsoft Azure 저장소 탐색기](http://storageexplorer.com/)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-235">It can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

<span data-ttu-id="4406b-237">**VM에서 Azure Blob로 데이터 이동: AzCopy**</span><span class="sxs-lookup"><span data-stu-id="4406b-237">**Move data from VM to Azure Blob: AzCopy**</span></span>

<span data-ttu-id="4406b-238">로컬 파일과 Blob Storage 간에 데이터를 이동하려면 명령줄 또는 PowerShell에서 AzCopy를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-238">To move data between your local files and blob storage, you can use AzCopy in command-line or PowerShell:</span></span>

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

<span data-ttu-id="4406b-239">파일이 저장되는 경로를 **C:\myfolder**로, Blob Store 계정 이름을 **mystorageaccount**로, 컨테이너 이름을 **mycontainer**로, Blob Store 액세스 키를 **저장소 계정 키**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-239">Replace **C:\myfolder** to the path where your file is stored, **mystorageaccount** to your blob storage account name, **mycontainer** to the container name, **storage account key** to your blob storage access key.</span></span> <span data-ttu-id="4406b-240">저장소 계정 자격 증명은 [Azure 포털](https://portal.azure.com)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-240">You can find your storage account credentials in [Azure portal](https://portal.azure.com).</span></span>

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

<span data-ttu-id="4406b-242">PowerShell 또는 명령 프롬프트에서 AzCopy 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-242">Run AzCopy command in PowerShell or from a command prompt.</span></span> <span data-ttu-id="4406b-243">다음은 AzCopy 명령을 사용하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-243">Here is some example usage of AzCopy command:</span></span>

    # Copy *.sql from local machine to a Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container to Local machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



<span data-ttu-id="4406b-244">Azure 명령을 실행하여 AzCopy Blob을 복사하면 잠시 후 Azure 저장소 탐색기에 해당 파일이 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-244">Once you run your AzCopy command to copy to an Azure blob you see your file shows up in Azure Storage Explorer shortly.</span></span>

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

<span data-ttu-id="4406b-246">**VM에서 Azure Blob로 데이터 이동: Azure 저장소 탐색기**</span><span class="sxs-lookup"><span data-stu-id="4406b-246">**Move data from VM to Azure Blob: Azure Storage Explorer**</span></span>

<span data-ttu-id="4406b-247">Azure 저장소 탐색기를 사용하여 VM의 로컬 파일에서 데이터를 업로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-247">You can also upload data from the local file in your VM using Azure Storage Explorer:</span></span>

* <span data-ttu-id="4406b-248">컨테이너에 데이터를 업로드하려면 대상 컨테이너를 선택하고 **업로드** 단추를 클릭합니다.![저장소 탐색기에서 업로드](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="4406b-248">To upload data to a container, select the target container and click the **Upload** button.![Upload in Storage Explorer](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span></span>
* <span data-ttu-id="4406b-249">**파일** 상자 오른쪽의 **...**을 클릭하고 파일 시스템에서 업로드할 파일을 하나 이상 선택한 후에 **업로드**를 클릭하여 파일 업로드를 시작합니다.![Blob에 파일 업로드](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="4406b-249">Click on the **...** to the right of the **Files** box, select one or multiple files to upload from the file system and click **Upload** to begin uploading the files.![Upload files to blob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span></span>

<span data-ttu-id="4406b-250">**Azure Blob에서 데이터 읽기: Machine Learning 판독기 모듈**</span><span class="sxs-lookup"><span data-stu-id="4406b-250">**Read data from Azure Blob: Machine Learning reader module**</span></span>

<span data-ttu-id="4406b-251">Azure Machine Learning Studio에서 **데이터 가져오기 모듈** 을 사용하여 Blob에서 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-251">In Azure Machine Learning Studio you can use an **Import Data module** to read data from your blob.</span></span>

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

<span data-ttu-id="4406b-253">**Azure Blob에서 데이터 읽기: Python ODBC**</span><span class="sxs-lookup"><span data-stu-id="4406b-253">**Read data from Azure Blob: Python ODBC**</span></span>

<span data-ttu-id="4406b-254">**BlobService** 라이브러리를 사용하여 Jupyter Notebook 또는 Python 프로그램의 Blob에서 직접 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-254">You can use **BlobService** library to read data directly from blob in a Jupyter Notebook or Python program.</span></span>

<span data-ttu-id="4406b-255">먼저 필요한 패키지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-255">First, import required packages:</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random

<span data-ttu-id="4406b-256">그런 다음 Azure Blob 계정 자격 증명을 연결하고 Blob에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-256">Then plug in your Azure Blob account credentials and read data from Blob:</span></span>

    CONTAINERNAME = 'xxx'
    STORAGEACCOUNTNAME = 'xxxx'
    STORAGEACCOUNTKEY = 'xxxxxxxxxxxxxxxx'
    BLOBNAME = 'nyctaxidataset/nyctaxitrip/trip_data_1.csv'
    localfilename = 'trip_data_1.csv'
    LOCALDIRECTORY = os.getcwd()
    LOCALFILE =  os.path.join(LOCALDIRECTORY, localfilename)

    #download from blob
    t1 = time.time()
    blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
    blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILE)
    t2 = time.time()
    print(("It takes %s seconds to download "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'the size of the data is: %d rows and  %d columns' % df1.shape

<span data-ttu-id="4406b-257">데이터 프레임으로 데이터를 읽어 들입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-257">The data is read in as a data frame:</span></span>

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a><span data-ttu-id="4406b-259">Azure 데이터 레이크</span><span class="sxs-lookup"><span data-stu-id="4406b-259">Azure Data Lake</span></span>
<span data-ttu-id="4406b-260">빅 데이터 분석 작업용의 초대형 리포지토리인 Azure Data Lake Storage는 HDFS(Hadoop 분산 파일 시스템)와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-260">Azure Data Lake Storage is a hyper-scale repository for big data analytics workloads and compatible with Hadoop Distributed File System (HDFS).</span></span> <span data-ttu-id="4406b-261">또한 Hadoop 에코시스템 및 Azure Data Lake Analytics에서 모두 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-261">It works with both the Hadoop ecosystem and the Azure Data Lake Analytics.</span></span> <span data-ttu-id="4406b-262">Azure Data Lake 저장소에 데이터를 이동하고 Azure Data Lake 분석을 사용하여 분석을 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-262">We show how you can move data into the Azure Data Lake Store and run analytics using Azure Data Lake Analytics.</span></span>

<span data-ttu-id="4406b-263">**필수 요소**</span><span class="sxs-lookup"><span data-stu-id="4406b-263">**Prerequisite**</span></span>

* <span data-ttu-id="4406b-264">[Azure 포털](https://portal.azure.com)에서 Azure Data Lake Analytics를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-264">Create your Azure Data Lake Analytics in [Azure portal](https://portal.azure.com).</span></span>

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* <span data-ttu-id="4406b-266">이 [링크](https://www.microsoft.com/download/details.aspx?id=49504)에서 찾을 수 있는 **Visual Studio**의 **Azure Data Lake 도구**는 이미 가상 컴퓨터의 Visual Studio Community Edition에 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-266">The  **Azure Data Lake Tools** in **Visual Studio** found at this  [link](https://www.microsoft.com/download/details.aspx?id=49504) is already installed on the Visual Studio Community Edition which is on the virtual machine.</span></span> <span data-ttu-id="4406b-267">Visual Studio를 시작하고 Azure 구독에 로그인하면 Visual Studio의 왼쪽 패널에 Azure Data Lake Analytics 계정 및 저장소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-267">After starting Visual Studio and logging in your Azure subscription, you should see your Azure Data Analytics account and storage in the left panel of Visual Studio.</span></span>

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

<span data-ttu-id="4406b-269">**VM에서 Data Lake로 데이터 이동: Azure Data Lake 탐색기**</span><span class="sxs-lookup"><span data-stu-id="4406b-269">**Move data from VM to Data Lake: Azure Data Lake Explorer**</span></span>

<span data-ttu-id="4406b-270">**Azure Data Lake Explorer** 를 사용하여 가상 컴퓨터의 로컬 파일에서 Data Lake Storage로 데이터를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-270">You can use **Azure Data Lake Explorer** to upload data from the local files in your Virtual Machine to Data Lake storage.</span></span>

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

<span data-ttu-id="4406b-272">[ADF(Azure Data Factory)](https://azure.microsoft.com/services/data-factory/)를 사용하여 Azure Data Lake로 또는 Azure Data Lake에서 데이터를 이동하는 데이터 파이프라인을 구축할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-272">You can also build a data pipeline to productionize your data movement to or from Azure Data Lake using the [Azure Data Factory(ADF)](https://azure.microsoft.com/services/data-factory/).</span></span> <span data-ttu-id="4406b-273">데이터 파이프라인을 구축하는 단계를 안내하는 이 [문서](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4406b-273">We refer you to this [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) to guide you through the steps to build the data pipelines.</span></span>

<span data-ttu-id="4406b-274">**Azure Blob에서 Data Lake로 데이터 읽기: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="4406b-274">**Read data from Azure Blob to Data Lake: U-SQL**</span></span>

<span data-ttu-id="4406b-275">데이터가 Azure Blob 저장소에 상주하는 경우 U SQL 쿼리를 사용하여 Azure 저장소 Blob에서 직접 데이터를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-275">If your data resides in Azure Blob storage, you can directly read data from Azure storage blob in U-SQL query.</span></span> <span data-ttu-id="4406b-276">U-SQL 쿼리를 작성하기 전에 Blob 저장소 계정이 Azure Data Lake에 연결되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-276">Before composing your U-SQL query, make sure your blob storage account is linked to your Azure Data Lake.</span></span> <span data-ttu-id="4406b-277">**Azure Portal**로 이동하여 Azure Data Lake Analytics 대시보드를 찾은 다음 **데이터 원본 추가**를 클릭하고 저장소 유형을 **Azure Storage**로 선택한 후에 Azure Storage 계정 이름 및 키를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-277">Go to **Azure portal**, find your Azure Data Lake Analytics dashboard, click **Add Data Source**, select storage type to **Azure Storage** and plug in your Azure Storage Account Name and Key.</span></span> <span data-ttu-id="4406b-278">그러면 저장소 계정에 저장된 데이터를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-278">Then you are able to reference the data stored in the storage account.</span></span>

![저장소 계정 및 키 입력](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

<span data-ttu-id="4406b-280">Visual Studio에서 Blob 저장소의 데이터를 읽고, 데이터를 조작하고, 기능을 엔지니어링하고, Azure Data Lake 또는 Azure Blob 저장소에 결과 데이터를 출력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-280">In Visual Studio, you can read data from blob storage, do some data manipulation, feature engineering, and output the resulting data to either Azure Data Lake or Azure Blob Storage.</span></span> <span data-ttu-id="4406b-281">Blob Storage의 데이터를 참조할 때는 **wasb://**를 사용하고, Azure Data Lake의 데이터를 참조할 때는 **swbhdfs://**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-281">When you reference the data in blob storage, use **wasb://**; when you reference the data in Azure Data Lake, use **swbhdfs://**</span></span>

![데이터 프레임](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

<span data-ttu-id="4406b-283">Visual Studio에서 다음 U-SQL 쿼리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-283">You may use the following U-SQL queries in Visual Studio:</span></span>

    @a =
        EXTRACT medallion string,
                hack_license string,
                vendor_id string,
                rate_code string,
                store_and_fwd_flag string,
                pickup_datetime string,
                dropoff_datetime string,
                passenger_count int,
                trip_time_in_secs double,
                trip_distance double,
                pickup_longitude string,
                pickup_latitude string,
                dropoff_longitude string,
                dropoff_latitude string

        FROM "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Input Data File Name>"
        USING Extractors.Csv();

    @b =
        SELECT vendor_id,
        COUNT(medallion) AS cnt_medallion,
        SUM(passenger_count) AS cnt_passenger,
        AVG(trip_distance) AS avg_trip_dist,
        MIN(trip_distance) AS min_trip_dist,
        MAX(trip_distance) AS max_trip_dist,
        AVG(trip_time_in_secs) AS avg_trip_time
        FROM @a
        GROUP BY vendor_id;

    OUTPUT @b   
    TO "swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    TO "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



<span data-ttu-id="4406b-284">서버에 쿼리가 제출되면 작업 상태를 표시하는 다이어그램이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-284">After your query is submitted to the server, a diagram showing the status of your job is displayed.</span></span>

![작업 상태 다이어그램](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

<span data-ttu-id="4406b-286">**Data Lake의 데이터 쿼리: U SQL**</span><span class="sxs-lookup"><span data-stu-id="4406b-286">**Query data in Data Lake: U-SQL**</span></span>

<span data-ttu-id="4406b-287">Azure Data Lake에 데이터 집합이 수집되면 [U-SQL 언어](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md)를 사용하여 데이터를 쿼리하고 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-287">After the dataset is ingested into Azure Data Lake, you can use [U-SQL language](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) to query and explore the data.</span></span> <span data-ttu-id="4406b-288">U-SQL 언어는 T-SQL과 비슷하지만 C#의 일부 기능이 결합되어 사용자가 사용자 지정 모듈, 사용자 정의 함수 등을 작성할 수 있습니다. 이전 단계의 스크립트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-288">U-SQL language is similar to T-SQL, but combines some features from C# so that users can write customized modules, user-defined functions, and etc. You can use the scripts in the previous step.</span></span>

<span data-ttu-id="4406b-289">서버에 쿼리가 제출되면 잠시 후 **Azure Data Lake 탐색기**에서 tripdata_summary.CSV 파일이 표시되며, 이 파일을 마우스 오른쪽 단추로 클릭하여 데이터를 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-289">After the query is submitted to server, tripdata_summary.CSV can be found shortly in **Azure Data Lake Explorer**, you may preview the data by right-click the file.</span></span>

![Azure Data Lake Explorer의 파일](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

<span data-ttu-id="4406b-291">파일 정보를 보려면:</span><span class="sxs-lookup"><span data-stu-id="4406b-291">To see the file information:</span></span>

![파일 요약](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a><span data-ttu-id="4406b-293">HDInsight Hadoop 클러스터</span><span class="sxs-lookup"><span data-stu-id="4406b-293">HDInsight Hadoop Clusters</span></span>
<span data-ttu-id="4406b-294">Azure HDInsight는 클라우드에서 관리되는 Apache Hadoop, Spark, HBase 및 Storm 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-294">Azure HDInsight is a managed Apache Hadoop, Spark, HBase, and Storm service on the cloud.</span></span> <span data-ttu-id="4406b-295">데이터 과학 가상 컴퓨터에서 Azure HDInsight 클러스터를 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-295">You can work easily with Azure HDInsight clusters from the data science virtual machine.</span></span>

<span data-ttu-id="4406b-296">**필수 요소**</span><span class="sxs-lookup"><span data-stu-id="4406b-296">**Prerequisite**</span></span>

* <span data-ttu-id="4406b-297">[Azure 포털](https://portal.azure.com)에서 고유한 Azure Blob 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-297">Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4406b-298">이 저장소 계정은 HDInsight 클러스터에 대한 데이터를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-298">This storage account is used to store data for HDInsight clusters.</span></span>

![Azure Blob Storage 계정 만들기](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="4406b-300">[Azure 포털](machine-learning-data-science-customize-hadoop-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="4406b-300">Customize Azure HDInsight Hadoop Clusters from [Azure portal](machine-learning-data-science-customize-hadoop-cluster.md)</span></span>
  
  * <span data-ttu-id="4406b-301">HDInsight 클러스터를 만들 때 만든 저장소 계정을 HDInsight 클러스터와 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-301">You must link the storage account created with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="4406b-302">이 저장소 계정은 클러스터 내에서 처리할 수 있는 데이터에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-302">This storage account is used for accessing data that can be processed within the cluster.</span></span>

![HDInsight 클러스터로 만든 저장소 계정에 연결](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* <span data-ttu-id="4406b-304">클러스터의 헤드 노드에 대한 **원격 액세스**를 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-304">You must enable **Remote Access** to the head node of the cluster after it is created.</span></span> <span data-ttu-id="4406b-305">여기에서 지정한 원격 액세스 자격 증명(클러스터에 대해 지정한 자격 증명과 다름)을 기억해야 합니다. 후속 절차에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-305">Remember the remote access credentials you specify here (different from those specified for the cluster at its creation): you need them in the subsequent procedure.</span></span>

![원격 액세스 사용](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* <span data-ttu-id="4406b-307">Azure Machine Learning 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-307">Create an Azure Machine Learning workspace.</span></span> <span data-ttu-id="4406b-308">Machine Learning 실험이 이 Machine Learning 작업 영역에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-308">Your Machine Learning Experiments are stored in this Machine Learning workspace.</span></span> <span data-ttu-id="4406b-309">아래 스크린샷에 표시된 것과 같이 포털에서 강조 표시된 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-309">Select the highlighted options in Portal as shown in the following screenshot:</span></span>

![Azure 기계 학습 작업 영역 만들기](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* <span data-ttu-id="4406b-311">그런 다음 작업 영역에 대한 매개 변수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-311">Then enter the parameters for your workspace</span></span>

![Machine Learning 작업 영역 매개 변수 입력](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* <span data-ttu-id="4406b-313">IPython Notebook을 사용하여 데이터를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-313">Upload data using IPython Notebook.</span></span> <span data-ttu-id="4406b-314">먼저 필요한 패키지를 가져오고 자격 증명에 연결하고 저장소 계정에 db를 만든 다음 HDI 클러스터에 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-314">First import required packages, plug in credentials, create a db in your storage account, then load data to HDI clusters.</span></span>

        #Import required Packages
        import pyodbc
        import time as time
        import json
        import os
        import urllib
        import urllib2
        import warnings
        import re
        import pandas as pd
        import matplotlib.pyplot as plt
        from azure.storage.blob import BlobService
        warnings.filterwarnings("ignore", category=UserWarning, module='urllib2')


        #Create the connection to Hive using ODBC
        SERVER_NAME='xxx.azurehdinsight.net'
        DATABASE_NAME='nyctaxidb'
        USERID='xxx'
        PASSWORD='xxxx'
        DB_DRIVER='Microsoft Hive ODBC Driver'
        driver = 'DRIVER={' + DB_DRIVER + '}'
        server = 'Host=' + SERVER_NAME + ';Port=443'
        database = 'Schema=' + DATABASE_NAME
        hiveserv = 'HiveServerType=2'
        auth = 'AuthMech=6'
        uid = 'UID=' + USERID
        pwd = 'PWD=' + PASSWORD
        CONNECTION_STRING = ';'.join([driver,server,database,hiveserv,auth,uid,pwd])
        connection = pyodbc.connect(CONNECTION_STRING, autocommit=True)
        cursor=connection.cursor()


        #Create Hive database and tables
        queryString = "create database if not exists nyctaxidb;"
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.trip
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            rate_code string,
                            store_and_fwd_flag string,
                            pickup_datetime string,
                            dropoff_datetime string,
                            passenger_count int,
                            trip_time_in_secs double,
                            trip_distance double,
                            pickup_longitude double,
                            pickup_latitude double,
                            dropoff_longitude double,
                            dropoff_latitude double)  
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.fare
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            pickup_datetime string,
                            payment_type string,
                            fare_amount double,
                            surcharge double,
                            mta_tax double,
                            tip_amount double,
                            tolls_amount double,
                            total_amount double)
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)


        #Upload data from blob storage to HDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* <span data-ttu-id="4406b-315">또는 이 [연습](machine-learning-data-science-process-hive-walkthrough.md)에 따라 NYC Taxi 데이터를 HDI 클러스터에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-315">Alternately,  you can follow this [walkthrough](machine-learning-data-science-process-hive-walkthrough.md) to upload NYC Taxi data to HDI cluster.</span></span> <span data-ttu-id="4406b-316">주요 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-316">Major steps include:</span></span>
  
  * <span data-ttu-id="4406b-317">AzCopy: 압축된 CSV를 공용 Blob에서 로컬 폴더로 다운로드</span><span class="sxs-lookup"><span data-stu-id="4406b-317">AzCopy: download zipped CSV's from public blob to your local folder</span></span>
  * <span data-ttu-id="4406b-318">AzCopy: 압축을 푼 CSV를 로컬 폴더에서 HDI 클러스터로 업로드</span><span class="sxs-lookup"><span data-stu-id="4406b-318">AzCopy: upload unzipped CSV's from local folder to HDI cluster</span></span>
  * <span data-ttu-id="4406b-319">Hadoop 클러스터의 헤드 노드에 로그인하여 예비 데이터 분석 준비</span><span class="sxs-lookup"><span data-stu-id="4406b-319">Log into the head node of Hadoop cluster and prepare for exploratory data analysis</span></span>

<span data-ttu-id="4406b-320">데이터가 HDI 클러스터에 로드되면 Azure 저장소를 탐색기에서 데이터를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-320">After the data is loaded to HDI cluster, you can check your data in Azure Storage Explorer.</span></span> <span data-ttu-id="4406b-321">그리고 HDI 클러스터에서 만든 데이터베이스 nyctaxidb가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-321">And you have a database nyctaxidb created in HDI cluster.</span></span>

<span data-ttu-id="4406b-322">**데이터 탐색: Python에서 Hive 쿼리**</span><span class="sxs-lookup"><span data-stu-id="4406b-322">**Data exploration: Hive Queries in Python**</span></span>

<span data-ttu-id="4406b-323">데이터가 Hadoop 클러스터에 있기 때문에 pyodbc 패키지를 사용하여 Hadoop 클러스터에 연결한 후 Hive를 사용하여 데이터베이스를 쿼리하여 데이터 탐색 및 기능 엔지니어링을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-323">Since the data is in Hadoop cluster, you can use the pyodbc package to connect to Hadoop Clusters and query database using Hive to do exploration and feature engineering.</span></span> <span data-ttu-id="4406b-324">필수 조건 단계에서 만든 기존 테이블을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-324">You can view the existing tables we created in the prerequisite step.</span></span>

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![기존 테이블 보기](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

<span data-ttu-id="4406b-326">각 월의 레코드 수와 trip 테이블에서 팁을 받은 여정과 팁을 받지 않은 여정의 빈도를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-326">Let's look at the number of records in each month and the frequencies of tipped or not in the trip table:</span></span>

    queryString = """
        select month, count(*) from nyctaxidb.trip group by month;
        """
    results = pd.read_sql(queryString,connection)

    %matplotlib inline

    results.columns = ['month', 'trip_count']
    df = results.copy()
    df.index = df['month']
    df['trip_count'].plot(kind='bar')


![월별 레코드 수에 대한 도표](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Number_Records_by_Month_v3.PNG)

    queryString = """
        SELECT tipped, COUNT(*) AS tip_freq
        FROM
        (
            SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
            FROM nyctaxidb.fare
        )tc
        GROUP BY tipped;
        """
    results = pd.read_sql(queryString,connection)

    results.columns = ['tipped', 'trip_count']
    df = results.copy()
    df.index = df['tipped']
    df['trip_count'].plot(kind='bar')


![팁 빈도 도표](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Frequency_tip_or_not_v3.PNG)

<span data-ttu-id="4406b-329">또한 승차 위치와 하차 위치 사이의 거리를 계산한 다음 주행 거리와 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-329">We can also compute the distance between pickup location and dropoff location and then compare it to the trip distance.</span></span>

    queryString = """
                    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
                        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
                        *radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
                        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
                        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
                        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*
                        pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance
                        from nyctaxidb.trip
                        where month=1
                            and pickup_longitude between -90 and -30
                            and pickup_latitude between 30 and 90
                            and dropoff_longitude between -90 and -30
                            and dropoff_latitude between 30 and 90;
                """
    results = pd.read_sql(queryString,connection)
    results.head(5)


![승차 및 하차 테이블](./media/machine-learning-data-science-vm-do-ten-things/Exploration_compute_pickup_dropoff_distance_v2.PNG)

    results.columns = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude',
                       'dropoff_latitude', 'trip_distance', 'trip_time_in_secs', 'direct_distance']
    df = results.loc[results['trip_distance']<=100] #remove outliers
    df = df.loc[df['direct_distance']<=100] #remove outliers
    plt.scatter(df['direct_distance'], df['trip_distance'])


![주행 거리에 대한 승차/하차 거리 도표](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

<span data-ttu-id="4406b-332">이제 모델링을 위한 다운샘플링(1%) 데이터 집합을 준비하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-332">Now let's prepare a down-sampled (1%) set of data for modeling.</span></span> <span data-ttu-id="4406b-333">Machine Learning 판독기 모듈에서 이 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-333">We can use this data in Machine Learning reader module.</span></span>

        queryString = """
        create  table if not exists nyctaxi_downsampled_dataset_testNEW (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\\n'
        stored as textfile;
        """
        cursor.execute(queryString)

        --- now insert contents of the join into the preceding internal table

        queryString = """
        insert overwrite table nyctaxi_downsampled_dataset_testNEW
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class
        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance,
        rand() as sample_key

        from trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01
        """
        cursor.execute(queryString)

<span data-ttu-id="4406b-334">잠시 후 Hadoop 클러스터에 데이터가 로드된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-334">After a while, you can see the data has been loaded in Hadoop clusters:</span></span>

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![데이터 테이블](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

<span data-ttu-id="4406b-336">**Machine Learning을 사용하여 HDI에서 데이터 읽기: 판독기 모듈**</span><span class="sxs-lookup"><span data-stu-id="4406b-336">**Read data from HDI using Machine Learning: reader module**</span></span>

<span data-ttu-id="4406b-337">Machine Learning Studio의 **판독기** 모듈을 사용하여 Hadoop 클러스터의 데이터베이스에 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-337">You may also use the **reader** module in Machine Learning Studio to access the database in Hadoop cluster.</span></span> <span data-ttu-id="4406b-338">HDI 클러스터의 자격 증명과 Azure Storage 계정을 연결하여 HDI 클러스터의 데이터베이스를 사용한 기계 학습 모델 빌드를 가능하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-338">Plug in the credentials of your HDI clusters and Azure Storage Account to enable build ing machine learning models using database in HDI clusters.</span></span>

![판독기 모듈 속성](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

<span data-ttu-id="4406b-340">그러면 채점된 데이터 집합을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-340">The scored dataset can then be viewed:</span></span>

![채점된 데이터 집합 보기](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a><span data-ttu-id="4406b-342">Azure SQL 데이터 웨어하우스 및 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="4406b-342">Azure SQL Data Warehouse & databases</span></span>
<span data-ttu-id="4406b-343">Azure SQL 데이터 웨어하우스는 엔터프라이즈급 SQL Server 환경의 서비스로 탄력적인 데이터 웨어하우스입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-343">Azure SQL Data Warehouse is an elastic data warehouse as a service with enterprise-class SQL Server experience.</span></span>

<span data-ttu-id="4406b-344">이 [문서](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md)에 제공된 지침에 따라 Azure SQL Data Warehouse를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-344">You can provision your Azure SQL Data Warehouse by following the instructions provided in this [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span></span> <span data-ttu-id="4406b-345">Azure SQL Data Warehouse를 프로비전하면 이 [연습](machine-learning-data-science-process-sqldw-walkthrough.md) 을 사용하여 SQL Data Warehouse 내의 데이터를 사용해 데이터 업로드, 탐색 및 모델링을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-345">Once you provision your Azure SQL Data Warehouse, you can use this [walkthrough](machine-learning-data-science-process-sqldw-walkthrough.md) to do data upload, exploration and modeling using data within the SQL Data Warehouse.</span></span>

#### <a name="azure-cosmos-db"></a><span data-ttu-id="4406b-346">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4406b-346">Azure Cosmos DB</span></span>
<span data-ttu-id="4406b-347">Azure Cosmos DB는 클라우드의 NoSQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-347">Azure Cosmos DB is a NoSQL database in the cloud.</span></span> <span data-ttu-id="4406b-348">JSON과 같은 문서를 작업할 수 있으며 문서를 저장 및 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-348">It allows you to work with documents like JSON and allows you to store and query the documents.</span></span>

<span data-ttu-id="4406b-349">DSVM에서 Azure Cosmos DB에 액세스하려면 다음과 같은 필수 조건 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-349">You need to do the following per-requisites steps to access Azure Cosmos DB from the DSVM.</span></span>

1. <span data-ttu-id="4406b-350">DocumentDB Python SDK를 설치합니다(명령 프롬프트에서 ```pip install pydocumentdb``` 실행).</span><span class="sxs-lookup"><span data-stu-id="4406b-350">Install DocumentDB Python SDK (Run ```pip install pydocumentdb``` from command prompt)</span></span>
2. <span data-ttu-id="4406b-351">[Azure Portal](https://portal.azure.com)에서 Azure Cosmos DB 계정과 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-351">Create an Azure Cosmos DB account and a database from [Azure portal](https://portal.azure.com)</span></span>
3. <span data-ttu-id="4406b-352">[여기](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d)서 "Azure Cosmos DB 마이그레이션 도구"를 다운로드하여 원하는 디렉터리에 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-352">Download "Azure Cosmos DB Migration Tool" from [here](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) and extract to a directory of your choice</span></span>
4. <span data-ttu-id="4406b-353">마이그레이션 도구(Cosmos DB 마이그레이션 도구를 설치한 디렉터리 dtui.exe)에 다음 명령 매개 변수를 사용하여 [공용 Blob](https://cahandson.blob.core.windows.net/samples/volcano.json)에 저장된 JSON 데이터(화산 데이터)를 Cosmos DB로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-353">Import JSON data (volcano data) stored on a [public blob](https://cahandson.blob.core.windows.net/samples/volcano.json) into Cosmos DB with following command parameters to the migration tool (dtui.exe from the directory where you installed the Cosmos DB Migration Tool).</span></span> <span data-ttu-id="4406b-354">아래의 원본 및 대상 위치를 다음 매개 변수와 함께 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-354">Enter the source and target location with these parameters:</span></span>
   
    <span data-ttu-id="4406b-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span><span class="sxs-lookup"><span data-stu-id="4406b-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span></span>

<span data-ttu-id="4406b-356">데이터를 가져온 후에는 Jupyter로 이동하여 *DocumentDBSample*이라는 제목의 Notebook을 열 수 있습니다. 이 Notebook에는 DocumentDB에 액세스하여 몇 가지 기본 쿼리를 수행할 수 있는 Python 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-356">Once you import the data, you can go to Jupyter and open the notebook titled *DocumentDBSample* which contains python code to access DocumentDB and do some basic querying.</span></span> <span data-ttu-id="4406b-357">서비스 [설명서 페이지](https://docs.microsoft.com/azure/cosmos-db/)를 방문하여 Cosmos DB에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-357">You can learn more about Cosmos DB by visiting the service [documentation page](https://docs.microsoft.com/azure/cosmos-db/).</span></span>

## <a name="8-build-reports-and-dashboard-using-the-power-bi-desktop"></a><span data-ttu-id="4406b-358">8. Power BI Desktop을 사용하여 보고서 및 대시보드 작성</span><span class="sxs-lookup"><span data-stu-id="4406b-358">8. Build reports and dashboard using the Power BI Desktop</span></span>
<span data-ttu-id="4406b-359">위의 Cosmos DB 예제에서 확인한 Volcano JSON 파일을 Power BI에서 시각화하여 데이터를 시각적으로 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-359">Let us visualize the Volcano JSON file that we saw in the preceding Cosmos DB example in Power BI to gain visual insights into the data.</span></span> <span data-ttu-id="4406b-360">자세한 단계는 [Power BI 문서](../cosmos-db/powerbi-visualize.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-360">Detailed steps are available in the [Power BI article](../cosmos-db/powerbi-visualize.md).</span></span> <span data-ttu-id="4406b-361">대략적인 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-361">Here are the high-level steps:</span></span>

1. <span data-ttu-id="4406b-362">Power BI Desktop을 열고 "Get Data"를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-362">Open Power BI Desktop and do "Get Data".</span></span> <span data-ttu-id="4406b-363">URL을 https://cahandson.blob.core.windows.net/samples/volcano.json으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-363">Specify the URL as: https://cahandson.blob.core.windows.net/samples/volcano.json</span></span>
2. <span data-ttu-id="4406b-364">목록으로 가져온 JSON 레코드가 보일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-364">You should see the JSON records imported as a list</span></span>
3. <span data-ttu-id="4406b-365">Power BI가 동일한 항목을 작업할 수 있도록 목록을 테이블로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-365">Convert the list to a table so Power BI can work with the same</span></span>
4. <span data-ttu-id="4406b-366">확장 아이콘(열 오른쪽에 "왼쪽 화살표와 오른쪽 화살표" 아이콘이 있는 아이콘)을 클릭하여 열을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-366">Expand the columns by clicking on the expand icon (the one with the "left arrow and a right arrow" icon on the right of the column)</span></span>
5. <span data-ttu-id="4406b-367">위치가 "레코드" 필드인 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-367">Notice that location is a "Record" field.</span></span> <span data-ttu-id="4406b-368">레코드를 확장하고 좌표만 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-368">Expand the record and select only the coordinates.</span></span> <span data-ttu-id="4406b-369">좌표는 목록 열입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-369">Coordinate is a list column</span></span>
6. <span data-ttu-id="4406b-370">목록 좌표 열을 쉼표로 구분된 LatLong 열로 변환하는 새 열을 추가하고 ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```수식을 사용하여 좌표 목록 필드의 두 요소를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-370">Add a new column to convert the list coordinate column into a comma separate LatLong column concatenating the two elements in the coordinate list field using the formula ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span></span>
7. <span data-ttu-id="4406b-371">마지막으로 ```Elevation``` 열을 10진수로 변환하고 **닫기** 및 **적용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-371">Finally convert the ```Elevation``` column to Decimal and select the **Close** and **Apply**.</span></span>

<span data-ttu-id="4406b-372">위의 단계를 수행하는 대신, 위의 단계를 스크립팅하는 다음 코드를 Power BI 고급 편집기에 붙여넣어서 데이터 변환을 쿼리 언어로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-372">Instead of preceding steps, you can paste the following code that scripts out the steps used in the Advanced Editor in Power BI that allows you to write the data transformations in a query language.</span></span>

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted to Table" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted to Table", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



<span data-ttu-id="4406b-373">이제 Power BI 데이터 모델에 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-373">You now have the data in your Power BI data model.</span></span> <span data-ttu-id="4406b-374">Power BI Desktop이 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-374">Your Power BI desktop should appear as follows:</span></span>

![Power BI 데스크톱](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

<span data-ttu-id="4406b-376">데이터 모델을 사용하여 보고서를 작성하고 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-376">You can start building reports and visualizations using the data model.</span></span> <span data-ttu-id="4406b-377">이 [Power BI 문서](../cosmos-db/powerbi-visualize.md#build-the-reports) 의 단계에 따라 보고서를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-377">You can follow the steps in this [Power BI article](../cosmos-db/powerbi-visualize.md#build-the-reports) to build a report.</span></span> <span data-ttu-id="4406b-378">최종 결과는 다음과 같이 표시되는 보고서입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-378">The end result is a report that looks like the following.</span></span>

![Power BI 데스크톱 보고서 보기 - Power BI 커넥터](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-to-meet-your-project-needs"></a><span data-ttu-id="4406b-380">9. 프로젝트 요구 사항에 맞게 DSVM을 동적으로 확장</span><span class="sxs-lookup"><span data-stu-id="4406b-380">9. Dynamically scale your DSVM to meet your project needs</span></span>
<span data-ttu-id="4406b-381">프로젝트 요구 사항에 맞게 DSVM을 확장 및 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-381">You can scale up and down the DSVM to meet your project needs.</span></span> <span data-ttu-id="4406b-382">저녁이나 주말에 VM이 필요 없으면 [Azure 포털](https://portal.azure.com)에서 VM을 종료하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-382">If you don't need to use the VM in the evening or weekends, you can just shut down the VM from the [Azure portal](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="4406b-383">VM의 운영 체제만 종료하면 계산 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-383">You incur compute charges if you use just the Operating system shutdown button on the VM.</span></span>  
> 
> 

<span data-ttu-id="4406b-384">대규모 분석을 처리하고 더 많은 CPU, 메모리 및/또는 디스크 용량이 필요한 경우 CPU 코어, 메모리 용량 및 디스크 유형(반도체 드라이브 포함)을 기준으로 계산 성능과 예산 조건에 맞는 VM 크기를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-384">If you need to handle some large-scale analysis and need more CPU and/or memory and/or disk capacity you can find a large choice of VM sizes in terms of CPU cores, memory capacity and disk types (including Solid state drives) that meet your compute and budgetary needs.</span></span> <span data-ttu-id="4406b-385">시간당 계산 가격을 비롯한 전체 VM 목록은 [Azure 가상 컴퓨터 가격 책정](https://azure.microsoft.com/pricing/details/virtual-machines/) 페이지에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-385">The full list of VMs along with their hourly compute pricing is available on the [Azure Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/) page.</span></span>

<span data-ttu-id="4406b-386">마찬가지로, 필요한 VM 처리 용량이 감소할 경우(예: 주요 워크로드를 Hadoop 또는 Spark 클러스터로 이동) [Azure 포털](https://portal.azure.com) 에서 VM 인스턴스 설정으로 이동하여 클러스터 규모를 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-386">Similarly, if your need for VM processing capacity reduces (for example: you moved a major workload to a Hadoop or a Spark cluster), you can scale down the cluster from the [Azure portal](https://portal.azure.com) and going to the settings of your VM instance.</span></span> <span data-ttu-id="4406b-387">다음은 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-387">Here is a screenshot.</span></span>

![VM 인스턴스 설정](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a><span data-ttu-id="4406b-389">10. 가상 컴퓨터에 추가 도구 설치</span><span class="sxs-lookup"><span data-stu-id="4406b-389">10. Install additional tools on your virtual machine</span></span>
<span data-ttu-id="4406b-390">Microsoft에서는 다양한 일반 데이터 분석 요구 사항을 해결할 수 있으며 환경을 하나씩 설치 및 구성하는 대신 한꺼번에 처리하여 시간을 절약하고 사용하는 리소스에 대한 요금을 지불하여 비용을 절감하는 다양한 도구를 패키지로 제공해 드리고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-390">We have packaged several tools that we believe are able to address many of the common data analytics needs and that should save you time by avoiding having to install and configure your environments one by one and save you money by paying only for resources that you use.</span></span>

<span data-ttu-id="4406b-391">사용자는 이 문서에서 프로파일링한 다른 Azure 데이터 및 분석 서비스를 활용하여 분석 환경을 강화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-391">You can leverage other Azure data and analytics services profiled in this article to enhance your analytics environment.</span></span> <span data-ttu-id="4406b-392">하지만 경우에 따라 독점적 타사 도구를 비롯한 추가 도구가 필요할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-392">We understand that in some cases your needs may require additional tools, including some proprietary third-party tools.</span></span> <span data-ttu-id="4406b-393">사용자에게는 가상 컴퓨터에 필요한 새 도구를 설치할 수 있는 모든 관리 액세스 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-393">You have full administrative access on the virtual machine to install new tools you need.</span></span> <span data-ttu-id="4406b-394">또한 사전 설치되지 않은 추가 패키지를 Python 및 R에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-394">You can also install additional packages in Python and R that are not pre-installed.</span></span> <span data-ttu-id="4406b-395">Python의 경우 ```conda``` 또는 ```pip```를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-395">For Python you can use either ```conda``` or ```pip```.</span></span> <span data-ttu-id="4406b-396">R의 경우 R 콘솔에서 ```install.packages()```를 사용하거나 IDE를 사용한 다음 "**패키지** -> **패키지 설치...**"를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-396">For R you can use the ```install.packages()``` in the R console or use the IDE and choose "**Packages** -> **Install Packages...**".</span></span>

## <a name="summary"></a><span data-ttu-id="4406b-397">요약</span><span class="sxs-lookup"><span data-stu-id="4406b-397">Summary</span></span>
<span data-ttu-id="4406b-398">이는 Microsoft 데이터 과학 가상 컴퓨터에서 할 수 있는 여러 가지 일 중의 극히 일부에 불과합니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-398">These are just some of the things you can do on the Microsoft Data Science Virtual Machine.</span></span> <span data-ttu-id="4406b-399">그 외에도 다양한 방법으로 효과적인 분석 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4406b-399">There are many more things you can do to make it an effective analytics environment.</span></span>

