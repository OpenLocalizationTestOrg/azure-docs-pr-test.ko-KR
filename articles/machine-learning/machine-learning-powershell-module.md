---
title: "Machine Learning용 PowerShell 모듈 | Microsoft Docs"
description: "Azure 기계 학습용 PowerShell 모듈은 공개 미리 보기 모드로 사용할 수 있습니다. PowerShell을 사용하여 작업 영역, 실험, 웹 서비스 등을 만들고 관리합니다."
keywords: "실험, 선형 회귀, 기계 학습 알고리즘, 기계 학습 자습서, 예측 모델링 기술, 데이터 과학 실험"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: a9001cc2-3aa0-47e1-b175-1f76408ba1d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: garye;haining
ms.openlocfilehash: 6ea4b887428891f41ed1a4bad26148763cefabe8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="powershell-module-for-microsoft-azure-machine-learning"></a><span data-ttu-id="7ba33-105">Microsoft Azure 기계 학습용 PowerShell 모듈</span><span class="sxs-lookup"><span data-stu-id="7ba33-105">PowerShell module for Microsoft Azure Machine Learning</span></span>
<span data-ttu-id="7ba33-106">Azure Machine Learning용 PowerShell 모듈은 Windows PowerShell을 사용하여 작업 영역, 실험, 데이터 집합, 기존 웹 서비스 등을 관리할 수 있는 강력한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-106">The PowerShell module for Azure Machine Learning is a powerful tool that allows you to use Windows PowerShell to manage workspaces, experiments, datasets, Classic web services, and more.</span></span>

<span data-ttu-id="7ba33-107">[https://aka.ms/amlps](https://aka.ms/amlps)에서 설명서를 보고 전체 소스 코드와 함께 모듈을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-107">You can view the documentation and download the module, along with the full source code, at [https://aka.ms/amlps](https://aka.ms/amlps).</span></span> 

> [!NOTE]
> <span data-ttu-id="7ba33-108">Azure 기계 학습 PowerShell 모듈은 현재 미리 보기 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-108">The Azure Machine Learning PowerShell module is currently in preview mode.</span></span> <span data-ttu-id="7ba33-109">모듈은 이 미리 보기 기간 중에 계속 개선되고 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-109">The module will continue to be improved and expanded during this preview period.</span></span> <span data-ttu-id="7ba33-110">뉴스 및 정보는 [Cortana Intelligence 및 기계 학습 블로그](https://blogs.technet.microsoft.com/machinelearning/)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="7ba33-110">Keep an eye on the [Cortana Intelligence and Machine Learning Blog](https://blogs.technet.microsoft.com/machinelearning/) for news and information.</span></span>

## <a name="what-is-the-machine-learning-powershell-module"></a><span data-ttu-id="7ba33-111">기계 학습 PowerShell 모듈이란?</span><span class="sxs-lookup"><span data-stu-id="7ba33-111">What is the Machine Learning PowerShell module?</span></span>
<span data-ttu-id="7ba33-112">Machine Learning PowerShell 모듈은 Windows PowerShell에서 Azure Machine Learning 작업 영역, 실험, 데이터 집합, 기존 웹 서비스 및 기존 웹 서비스 끝점을 완벽하게 관리할 수 있는 .NET 기반 DLL 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-112">The Machine Learning PowerShell module is a .NET-based DLL module that allows you to fully manage Azure Machine Learning workspaces, experiments, datasets, Classic web services, and Classic web service endpoints from Windows PowerShell.</span></span> 

<span data-ttu-id="7ba33-113">모듈과 함께 명확하게 구분된 [C# API 계층](https://github.com/hning86/azuremlps/blob/master/code/AzureMLSDK.cs)을 포함하는 전체 소스 코드를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-113">Along with the module, you can download the full source code which includes a cleanly separated [C# API layer](https://github.com/hning86/azuremlps/blob/master/code/AzureMLSDK.cs).</span></span> <span data-ttu-id="7ba33-114">고유한 .NET 프로젝트에서 이 DLL을 참조하고 .NET 코드를 통해 Azure Machine Learning을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-114">You can reference this DLL from your own .NET project and manage Azure Machine Learning through .NET code.</span></span> <span data-ttu-id="7ba33-115">또한 DLL은 자주 사용하는 클라이언트에서 직접 활용할 수 있는 기본 REST API에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-115">In addition, the DLL depends on underlying REST APIs that you can use directly from your favorite client.</span></span>

## <a name="what-can-i-do-with-the-powershell-module"></a><span data-ttu-id="7ba33-116">PowerShell 모듈을 사용해서 무엇을 할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="7ba33-116">What can I do with the PowerShell module?</span></span>
<span data-ttu-id="7ba33-117">다음은 이 PowerShell 모듈로 수행할 수 있는 일부 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-117">Here are some of the tasks you can perform with this PowerShell module.</span></span> <span data-ttu-id="7ba33-118">다음을 포함한 여러 기능은 [전체 설명서](https://aka.ms/amlps) 를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-118">Check out the [full documentation](https://aka.ms/amlps) for these and many more functions.</span></span>

* <span data-ttu-id="7ba33-119">관리 인증서를 사용한 새 작업 영역 프로비전([New-AmlWorkspace](https://github.com/hning86/azuremlps#new-amlworkspace))</span><span class="sxs-lookup"><span data-stu-id="7ba33-119">Provision a new workspace using a management certificate ([New-AmlWorkspace](https://github.com/hning86/azuremlps#new-amlworkspace))</span></span>
* <span data-ttu-id="7ba33-120">실험 그래프를 나타내는 JSON 파일을 내보내기 및 가져오기([Export-AmlExperimentGraph](https://github.com/hning86/azuremlps#export-amlexperimentgraph) 및 [Import-AmlExperimentGraph](https://github.com/hning86/azuremlps#import-amlexperimentgraph))</span><span class="sxs-lookup"><span data-stu-id="7ba33-120">Export and import a JSON file representing an experiment graph ([Export-AmlExperimentGraph](https://github.com/hning86/azuremlps#export-amlexperimentgraph) and [Import-AmlExperimentGraph](https://github.com/hning86/azuremlps#import-amlexperimentgraph))</span></span>
* <span data-ttu-id="7ba33-121">실험 실행([Start-AmlExperiment](https://github.com/hning86/azuremlps#start-amlexperiment))</span><span class="sxs-lookup"><span data-stu-id="7ba33-121">Run an experiment ([Start-AmlExperiment](https://github.com/hning86/azuremlps#start-amlexperiment))</span></span>
* <span data-ttu-id="7ba33-122">예측 실험에서 웹 서비스 만들기([New-AmlWebService](https://github.com/hning86/azuremlps#new-amlwebservice))</span><span class="sxs-lookup"><span data-stu-id="7ba33-122">Create a web service out of a predictive experiment ([New-AmlWebService](https://github.com/hning86/azuremlps#new-amlwebservice))</span></span>
* <span data-ttu-id="7ba33-123">게시된 웹 서비스에 끝점 만들기([Add-AmlWebServiceEndpoint](https://github.com/hning86/azuremlps#add-amlwebserviceendpoint))</span><span class="sxs-lookup"><span data-stu-id="7ba33-123">Create an endpoint on a published web service ([Add-AmlWebServiceEndpoint](https://github.com/hning86/azuremlps#add-amlwebserviceendpoint))</span></span>
* <span data-ttu-id="7ba33-124">RRS 또는 BES 웹 서비스 끝점 호출([Invoke-AmlWebServiceRRSEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) 및 [Invoke-AmlWebServicBESEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint))</span><span class="sxs-lookup"><span data-stu-id="7ba33-124">Invoke an RRS and/or BES web service endpoint ([Invoke-AmlWebServiceRRSEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) and [Invoke-AmlWebServicBESEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint))</span></span>

<span data-ttu-id="7ba33-125">기존 실험을 실행하기 위해 PowerShell을 사용하는 간단한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-125">Here's a quick example of using PowerShell to run an existing experiment:</span></span>

        #Find the first Experiment named “xyz”
        $exp = (Get-AmlExperiment | where Description -eq ‘xyz’)[0]
        #Run the Experiment
        Start-AmlExperiment -ExperimentId $exp.ExperimentId 

<span data-ttu-id="7ba33-126">일반적으로 요청된 작업을 자동화하도록 PowerShell 모듈을 사용하는 방법에 대한 자세한 사용 사례는 [PowerShell을 사용하여 한 실험에서 여러 Machine Learning 모델 및 웹 서비스 끝점 만들기](machine-learning-create-models-and-endpoints-with-powershell.md)문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ba33-126">For a more in-depth use case, see this article on using the PowerShell module to automate a commonly-requested task: [Create many Machine Learning models and web service endpoints from one experiment using PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).</span></span>

## <a name="how-do-i-get-started"></a><span data-ttu-id="7ba33-127">어떻게 시작하나요?</span><span class="sxs-lookup"><span data-stu-id="7ba33-127">How do I get started?</span></span>
<span data-ttu-id="7ba33-128">Machine Learning PowerShell을 시작하려면 GitHub에서 [릴리스 패키지](https://github.com/hning86/azuremlps/releases)를 다운로드하고 [설치에 대한 지침](https://github.com/hning86/azuremlps/blob/master/README.md)을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-128">To get started with Machine Learning PowerShell, download the [release package](https://github.com/hning86/azuremlps/releases) from GitHub and follow the [instructions for installation](https://github.com/hning86/azuremlps/blob/master/README.md).</span></span> <span data-ttu-id="7ba33-129">지침은 다운로드/압축 해제된 DLL의 차단을 해제한 다음 PowerShell 환경으로 가져오는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-129">The instructions explain how to unblock the downloaded/unzipped DLL and then import it into your PowerShell environment.</span></span> <span data-ttu-id="7ba33-130">대부분의 cmdlet에는 작업 영역 ID, 작업 영역 권한 부여 토큰 및 작업 영역이 위치한 Azure 지역을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-130">Most of the cmdlets require that you supply the workspace ID, the workspace authorization token, and the Azure region that the workspace is in.</span></span> <span data-ttu-id="7ba33-131">값을 제공하는 가장 간단한 방법은 기본 config.json 파일을 통하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-131">The simplest way to provide the values is through a default config.json file.</span></span> <span data-ttu-id="7ba33-132">지침은 또한 이 파일을 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-132">The instructions also explain how to configure this file.</span></span> 

<span data-ttu-id="7ba33-133">원하는 경우 Visual Studio를 사용하여 git 트리 복제하고 코드를 수정하여 로컬에 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-133">And if you want, you can clone the git tree, modify the code, and compile it locally using Visual Studio.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ba33-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ba33-134">Next steps</span></span>
<span data-ttu-id="7ba33-135">PowerShell 모듈에 대한한 전체 설명서를 [https://aka.ms/amlps](https://aka.ms/amlps)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ba33-135">You can find the full documentation for the PowerShell module at [https://aka.ms/amlps](https://aka.ms/amlps).</span></span> 

<span data-ttu-id="7ba33-136">실제 시나리오에서 모듈을 사용하는 방법의 확장된 예제는 자세한 사용 사례인 [PowerShell을 사용하여 한 실험에서 여러 기계 학습 모델 및 웹 서비스 끝점을 만들기](machine-learning-create-models-and-endpoints-with-powershell.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="7ba33-136">For an extended example of how to use the module in a real-world scenario, check out the in-depth use case, [Create many Machine Learning models and web service endpoints from one experiment using PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).</span></span>
