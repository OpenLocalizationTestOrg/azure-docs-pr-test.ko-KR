---
title: "Visual Studio 프로젝트 템플릿을 사용하여 Batch 솔루션을 구축하기 시작 - Azure | Microsoft Docs"
description: "Visual Studio 프로젝트 템플릿을 통해 Azure Batch에서 계산 집약적인 워크로드를 어떻게 구현하고 실행할 수 있는지 알아봅니다."
services: batch
documentationcenter: .net
author: fayora
manager: timlt
editor: 
ms.assetid: 5e041ae2-25af-4882-a79e-3aa63c4bfb20
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: da77ce827c65deb18d9d84ce5cf768d89788e205
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-visual-studio-project-templates-to-jump-start-batch-solutions"></a><span data-ttu-id="7ea37-103">Visual Studio 프로젝트 템플릿을 사용하여 Batch 솔루션 빠르게 시작</span><span class="sxs-lookup"><span data-stu-id="7ea37-103">Use Visual Studio project templates to jump-start Batch solutions</span></span>

<span data-ttu-id="7ea37-104">배치용 **작업 관리자** 및 **태스크 프로세서 Visual Studio 템플릿**은 최소한의 노력으로 배치에서 계산 집약적 워크로드를 구현 및 실행하는 데 도움이 되는 코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-104">The **Job Manager** and **Task Processor Visual Studio templates** for Batch provide code to help you to implement and run your compute-intensive workloads on Batch with the least amount of effort.</span></span> <span data-ttu-id="7ea37-105">이 문서에서는 이러한 템플릿을 설명하고 템플릿을 사용하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-105">This document describes these templates and provides guidance for how to use them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ea37-106">이 문서에서는 이러한 두 템플릿에 해당하는 정보만 다루며 사용자가 Batch 서비스 및 이와 관련된 주요 개념(풀, 계산 노드, 작업 및 태스크, 작업 관리자 태스크, 환경 변수 및 기타 관련 정보)에 익숙하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-106">This article discusses only information applicable to these two templates, and assumes that you are familiar with the Batch service and key concepts related to it: pools, compute nodes, jobs and tasks, job manager tasks, environment variables, and other relevant information.</span></span> <span data-ttu-id="7ea37-107">보다 자세한 내용은 [Azure 배치의 기본 사항](batch-technical-overview.md), [개발자를 위한 배치 기능 개요](batch-api-basics.md) 및 [.NET용 Azure 배치 라이브러리 시작](batch-dotnet-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ea37-107">You can find more information in [Basics of Azure Batch](batch-technical-overview.md), [Batch feature overview for developers](batch-api-basics.md), and [Get started with the Azure Batch library for .NET](batch-dotnet-get-started.md).</span></span>
> 
> 

## <a name="high-level-overview"></a><span data-ttu-id="7ea37-108">대략적인 개요</span><span class="sxs-lookup"><span data-stu-id="7ea37-108">High-level overview</span></span>
<span data-ttu-id="7ea37-109">작업 관리자 및 태스크 프로세서 템플릿은 다음 두 가지 유용한 구성 요소를 만드는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-109">The Job Manager and Task Processor templates can be used to create two useful components:</span></span>

* <span data-ttu-id="7ea37-110">작업을 독립적으로 병렬 실행 가능한 여러 태스크로 나눌 수 있는 작업 분할자를 구현하는 작업 관리자 태스크.</span><span class="sxs-lookup"><span data-stu-id="7ea37-110">A job manager task that implements a job splitter that can break a job down into multiple tasks that can run independently, in parallel.</span></span>
* <span data-ttu-id="7ea37-111">응용 프로그램 명령줄에 대한 전처리 및 후처리를 수행하는 데 사용할 수 있는 태스크 프로세서.</span><span class="sxs-lookup"><span data-stu-id="7ea37-111">A task processor that can be used to perform pre-processing and post-processing around an application command line.</span></span>

<span data-ttu-id="7ea37-112">예를 들어 동영상 렌더링 시나리오에서 경우 작업 분할자는 하나의 동영상 작업을 수백 또는 수천 개의 태스크로 전환하여 개별 프레임을 별도로 처리하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-112">For example, in a movie rendering scenario, the job splitter would turn a single movie job into hundreds or thousands of separate tasks that would process individual frames separately.</span></span> <span data-ttu-id="7ea37-113">마찬가지로, 태스크 프로세서는 각 프레임을 렌더링하는 데 필요한 렌더링 응용 프로그램과 모든 종속 프로세스를 호출하고 추가 작업(예: 렌더링된 프레임을 저장소 위치에 복사)을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-113">Correspondingly, the task processor would invoke the rendering application and all dependent processes that are needed to render each frame, as well as perform any additional actions (for example, copying the rendered frame to a storage location).</span></span>

> [!NOTE]
> <span data-ttu-id="7ea37-114">작업 관리자 및 태스크 프로세서 템플릿은 서로 독립적이므로 기본 설정에서 계산 작업의 요구 사항에 따라 둘 다 또는 둘 중 하나만 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-114">The Job Manager and Task Processor templates are independent of each other, so you can choose to use both, or only one of them, depending on the requirements of your compute job and on your preferences.</span></span>
> 
> 

<span data-ttu-id="7ea37-115">아래 다이어그램에 표시된 것처럼 이러한 템플릿을 사용하는 계산 작업은 세 가지 단계를 거칩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-115">As shown in the diagram below, a compute job that uses these templates will go through three stages:</span></span>

1. <span data-ttu-id="7ea37-116">클라이언트 코드(예: 응용 프로그램, 웹 서비스 등)가 작업을 Azure의 Batch 서비스에 제출합니다. 이때 작업 관리자가 프로그래밍하는 작업 관리자 태스크로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-116">The client code (e.g., application, web service, etc.) submits a job to the Batch service on Azure, specifying as its job manager task the job manager program.</span></span>
2. <span data-ttu-id="7ea37-117">Batch 서비스는 계산 노드에서 작업 관리자 태스크를 실행하고 작업 분할자는 작업 분할자 코드에 있는 매개 변수 및 사양에 따라 필요한 만큼의 계산 노드에서 지정된 수의 태스크 프로세서 태스크를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-117">The Batch service runs the job manager task on a compute node and the job splitter launches the specified number of task processor tasks, on as many compute nodes as required, based on the parameters and specifications in the job splitter code.</span></span>
3. <span data-ttu-id="7ea37-118">태스크 프로세서 태스크는 입력 데이터를 처리하고 출력 데이터를 생성하기 위해 독립적으로 병렬 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-118">The task processor tasks run independently, in parallel, to process the input data and generate the output data.</span></span>

![클라이언트 코드가 배치 서비스와 상호 작용하는 방법을 보여 주는 다이어그램][diagram01]

## <a name="prerequisites"></a><span data-ttu-id="7ea37-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="7ea37-120">Prerequisites</span></span>
<span data-ttu-id="7ea37-121">Batch 템플릿을 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-121">To use the Batch templates, you will need the following:</span></span>

* <span data-ttu-id="7ea37-122">Visual Studio 2015가 설치된 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="7ea37-122">A computer with Visual Studio 2015 installed.</span></span> <span data-ttu-id="7ea37-123">일괄 처리 템플릿은 현재 Visual Studio 2015에 대해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-123">Batch templates are currently only supported for Visual Studio 2015.</span></span>
* <span data-ttu-id="7ea37-124">[Visual Studio 갤러리][vs_gallery]에서 Visual Studio 확장으로 제공되는 Batch 템플릿.</span><span class="sxs-lookup"><span data-stu-id="7ea37-124">The Batch templates, which are available from the [Visual Studio Gallery][vs_gallery] as Visual Studio extensions.</span></span> <span data-ttu-id="7ea37-125">템플릿을 얻는 방법은 두 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-125">There are two ways to get the templates:</span></span>
  
  * <span data-ttu-id="7ea37-126">Visual Studio에서 **확장 및 업데이트** 대화 상자를 사용하여 템플릿을 설치합니다(자세한 내용은 [Visual Studio 확장 찾기 및 사용][vs_find_use_ext] 참조).</span><span class="sxs-lookup"><span data-stu-id="7ea37-126">Install the templates using the **Extensions and Updates** dialog box in Visual Studio (for more information, see [Finding and Using Visual Studio Extensions][vs_find_use_ext]).</span></span> <span data-ttu-id="7ea37-127">**확장 및 업데이트** 대화 상자에서 다음 두 확장을 검색하여 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-127">In the **Extensions and Updates** dialog box, search and download the following two extensions:</span></span>
    
    * <span data-ttu-id="7ea37-128">Azure 배치 작업 관리자(작업 분할자 포함)</span><span class="sxs-lookup"><span data-stu-id="7ea37-128">Azure Batch Job Manager with Job Splitter</span></span>
    * <span data-ttu-id="7ea37-129">Azure 배치 태스크 프로세서</span><span class="sxs-lookup"><span data-stu-id="7ea37-129">Azure Batch Task Processor</span></span>
  * <span data-ttu-id="7ea37-130">Visual Studio의 온라인 갤러리에서 템플릿을 다운로드합니다. [Microsoft Azure Batch 프로젝트 템플릿][vs_gallery_templates]</span><span class="sxs-lookup"><span data-stu-id="7ea37-130">Download the templates from the online gallery for Visual Studio: [Microsoft Azure Batch Project Templates][vs_gallery_templates]</span></span>
* <span data-ttu-id="7ea37-131">[응용 프로그램 패키지](batch-application-packages.md) 기능을 사용하여 작업 관리자 및 태스크 프로세서를 Batch 계산 노드에 배포할 계획인 경우 저장소 계정을 배치 계정에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-131">If you plan to use the [Application Packages](batch-application-packages.md) feature to deploy the job manager and task processor to the Batch compute nodes, you need to link a storage account to your Batch account.</span></span>

## <a name="preparation"></a><span data-ttu-id="7ea37-132">준비</span><span class="sxs-lookup"><span data-stu-id="7ea37-132">Preparation</span></span>
<span data-ttu-id="7ea37-133">작업 관리자 및 태스크 프로세서 프로그램 간에 코드를 쉽게 공유할 수 있으므로 작업 관리자 및 태스크 프로세서를 포함할 수 있는 솔루션을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-133">We recommend creating a solution that can contain your job manager as well as your task processor, because this can make it easier to share code between your job manager and task processor programs.</span></span> <span data-ttu-id="7ea37-134">이 솔루션을 만들려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="7ea37-134">To create this solution, follow these steps:</span></span>

1. <span data-ttu-id="7ea37-135">Visual Studio를 열고 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-135">Open Visual Studio and select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="7ea37-136">**템플릿** 아래에서 **기타 프로젝트 형식**을 확장하고 **Visual Studio 솔루션**을 클릭한 후 **빈 솔루션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-136">Under **Templates**, expand **Other Project Types**, click **Visual Studio Solutions**, and then select **Blank Solution**.</span></span>
3. <span data-ttu-id="7ea37-137">응용 프로그램 및 이 솔루션의 용도를 설명하는 이름을 입력합니다(예: "LitwareBatchTaskPrograms").</span><span class="sxs-lookup"><span data-stu-id="7ea37-137">Type a name that describes your application and the purpose of this solution (e.g., "LitwareBatchTaskPrograms").</span></span>
4. <span data-ttu-id="7ea37-138">새 솔루션을 만들려면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-138">To create the new solution, click **OK**.</span></span>

## <a name="job-manager-template"></a><span data-ttu-id="7ea37-139">작업 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="7ea37-139">Job Manager template</span></span>
<span data-ttu-id="7ea37-140">작업 관리자 템플릿을 통해 다음 작업을 수행할 수 있는 작업 관리자 태스크를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-140">The Job Manager template helps you to implement a job manager task that can perform the following actions:</span></span>

* <span data-ttu-id="7ea37-141">작업을 여러 태스크로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-141">Split a job into multiple tasks.</span></span>
* <span data-ttu-id="7ea37-142">배치에서 실행하려면 이러한 태스크를 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-142">Submit those tasks to run on Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="7ea37-143">작업 관리자 태스크에 대한 자세한 내용은 [개발자를 위한 배치 기능 개요](batch-api-basics.md#job-manager-task)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ea37-143">For more information about job manager tasks, see [Batch feature overview for developers](batch-api-basics.md#job-manager-task).</span></span>
> 
> 

### <a name="create-a-job-manager-using-the-template"></a><span data-ttu-id="7ea37-144">템플릿을 사용하여 작업 관리자 만들기</span><span class="sxs-lookup"><span data-stu-id="7ea37-144">Create a Job Manager using the template</span></span>
<span data-ttu-id="7ea37-145">이전에 만든 솔루션에 작업 관리자를 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-145">To add a job manager to the solution that you created earlier, follow these steps:</span></span>

1. <span data-ttu-id="7ea37-146">Visual Studio에서 기존 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-146">Open your existing solution in Visual Studio.</span></span>
2. <span data-ttu-id="7ea37-147">솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **추가** > **새 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-147">In Solution Explorer, right-click the solution, click **Add** > **New Project**.</span></span>
3. <span data-ttu-id="7ea37-148">**Visual C#** 아래에서 **클라우드**를 클릭한 후 **Azure 배치 작업 관리자 및 작업 분할자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-148">Under **Visual C#**, click **Cloud**, and then click **Azure Batch Job Manager with Job Splitter**.</span></span>
4. <span data-ttu-id="7ea37-149">응용 프로그램을 설명하고 이 프로젝트를 작업 관리자로 식별하는 이름을 입력합니다(예: "LitwareJobManager").</span><span class="sxs-lookup"><span data-stu-id="7ea37-149">Type a name that describes your application and identifies this project as the job manager (e.g. "LitwareJobManager").</span></span>
5. <span data-ttu-id="7ea37-150">프로젝트를 만들려면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-150">To create the project, click **OK**.</span></span>
6. <span data-ttu-id="7ea37-151">마지막으로, 프로젝트를 빌드하여 Visual Studio에서 모든 참조된 NuGet 패키지를 로드하고 수정을 시작하기 전에 해당 프로젝트가 유효한지 확인하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-151">Finally, build the project to force Visual Studio to load all referenced NuGet packages and to verify that the project is valid before you start modifying it.</span></span>

### <a name="job-manager-template-files-and-their-purpose"></a><span data-ttu-id="7ea37-152">작업 관리자 템플릿 파일 및 그 용도</span><span class="sxs-lookup"><span data-stu-id="7ea37-152">Job Manager template files and their purpose</span></span>
<span data-ttu-id="7ea37-153">작업 관리자 템플릿을 사용하여 프로젝트를 만들면 세 가지 코드 파일 그룹이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-153">When you create a project using the Job Manager template, it generates three groups of code files:</span></span>

* <span data-ttu-id="7ea37-154">메인 프로그램 파일(Program.cs).</span><span class="sxs-lookup"><span data-stu-id="7ea37-154">The main program file (Program.cs).</span></span> <span data-ttu-id="7ea37-155">여기에는 프로그램 진입점과 최상위 예외 처리가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-155">This contains the program entry point and top-level exception handling.</span></span> <span data-ttu-id="7ea37-156">일반적으로 이 값을 수정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-156">You shouldn't normally need to modify this.</span></span>
* <span data-ttu-id="7ea37-157">프레임워크 디렉터리.</span><span class="sxs-lookup"><span data-stu-id="7ea37-157">The Framework directory.</span></span> <span data-ttu-id="7ea37-158">여기에는 매개 변수 압축 해제, 배치 작업에 태스크 추가 등 작업 관리자 프로그램이 수행했던 '상용구' 작업을 담당하는 파일이 포함됩니다. 일반적으로 이러한 파일을 수정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-158">This contains the files responsible for the 'boilerplate' work done by the job manager program – unpacking parameters, adding tasks to the Batch job, etc. You shouldn't normally need to modify these files.</span></span>
* <span data-ttu-id="7ea37-159">작업 분할자 파일(JobSplitter.cs).</span><span class="sxs-lookup"><span data-stu-id="7ea37-159">The job splitter file (JobSplitter.cs).</span></span> <span data-ttu-id="7ea37-160">작업을 태스크로 분할하기 위해 응용 프로그램 관련 논리를 배치할 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-160">This is where you will put your application-specific logic for splitting a job into tasks.</span></span>

<span data-ttu-id="7ea37-161">물론 작업 분할 논리의 복잡성에 따라 작업 분할자 코드를 지원하는 데 필요하다면 파일을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-161">Of course you can add additional files as required to support your job splitter code, depending on the complexity of the job splitting logic.</span></span>

<span data-ttu-id="7ea37-162">템플릿에서는 .csproj 파일, app.config, packages.config 등과 같은 표준 .NET 프로젝트 파일도 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-162">The template also generates standard .NET project files such as a .csproj file, app.config, packages.config, etc.</span></span>

<span data-ttu-id="7ea37-163">이 섹션의 나머지에서는 다양한 파일 및 해당 코드 구조를 설명하고 각 클래스에서 어떤 작업을 수행하는지 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-163">The rest of this section describes the different files and their code structure, and explains what each class does.</span></span>

![작업 관리자 템플릿 솔루션을 보여 주는 Visual Studio 솔루션 탐색기][solution_explorer01]

<span data-ttu-id="7ea37-165">**프레임워크 파일**</span><span class="sxs-lookup"><span data-stu-id="7ea37-165">**Framework files**</span></span>

* <span data-ttu-id="7ea37-166">`Configuration.cs`: 배치 계정 정보, 연결된 저장소 계정 자격 증명, 작업 및 태스크 정보 및 작업 매개 변수와 같은 작업 구성 데이터의 로드를 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-166">`Configuration.cs`: Encapsulates the loading of job configuration data such as Batch account details, linked storage account credentials, job and task information, and job parameters.</span></span> <span data-ttu-id="7ea37-167">또한 Configuration.EnvironmentVariable 클래스를 통해 배치 정의된 환경 변수(배치 설명서에서 태스크에 대한 환경 설정 참조)에 대한 액세스도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-167">It also provides access to Batch-defined environment variables (see Environment settings for tasks, in the Batch documentation) via the Configuration.EnvironmentVariable class.</span></span>
* <span data-ttu-id="7ea37-168">`IConfiguration.cs`: 모조 또는 모의 구성 개체를 사용하여 작업 분할자의 단위 태스크를 수행할 수 있도록 구성 클래스의 구현을 추상화합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-168">`IConfiguration.cs`: Abstracts the implementation of the Configuration class, so that you can unit test your job splitter using a fake or mock configuration object.</span></span>
* <span data-ttu-id="7ea37-169">`JobManager.cs`: 작업 관리자 프로그램의 구성 요소를 오케스트레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-169">`JobManager.cs`: Orchestrates the components of the job manager program.</span></span> <span data-ttu-id="7ea37-170">작업 분할자의 초기화, 작업 분할자 호출 및 작업 분할자에서 태스크 제출자로 반환되는 태스크 디스패치를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-170">It is responsible for the initializing the job splitter, invoking the job splitter, and dispatching the tasks returned by the job splitter to the task submitter.</span></span>
* <span data-ttu-id="7ea37-171">`JobManagerException.cs`: 작업 관리자를 종료해야 하는 오류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-171">`JobManagerException.cs`: Represents an error that requires the job manager to terminate.</span></span> <span data-ttu-id="7ea37-172">JobManagerException은 종료의 일부분으로 특정 진단 정보를 제공할 수 있는 '예상된' 오류를 래핑하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-172">JobManagerException is used to wrap 'expected' errors where specific diagnostic information can be provided as part of termination.</span></span>
* <span data-ttu-id="7ea37-173">`TaskSubmitter.cs`:이 클래스는 작업 분할자가 반환한 태스크를 배치 작업에 추가하는 것을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-173">`TaskSubmitter.cs`: This class is responsible to adding tasks returned by the job splitter to the Batch job.</span></span> <span data-ttu-id="7ea37-174">JobManager 클래스는 태스크 시퀀스를 배치로 효율적으로 집계하여 작업에 시기 적절하게 추가한 후 각 배치에 대한 백그라운드 스레드에서 TaskSubmitter.SubmitTasks를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-174">The JobManager class aggregates the sequence of tasks into batches for efficient but timely addition to the job, then calls TaskSubmitter.SubmitTasks on a background thread for each batch.</span></span>

<span data-ttu-id="7ea37-175">**작업 분할자**</span><span class="sxs-lookup"><span data-stu-id="7ea37-175">**Job Splitter**</span></span>

<span data-ttu-id="7ea37-176">`JobSplitter.cs`: 이 클래스는 작업을 태스크로 분할하기 위한 응용 프로그램 관련 논리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-176">`JobSplitter.cs`: This class contains application-specific logic for splitting the job into tasks.</span></span> <span data-ttu-id="7ea37-177">프레임워크는 태스크 시퀀스를 가져오기 위해 JobSplitter.Split 메서드를 호출하며 메서드가 시퀀스를 반환하면 이를 작업에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-177">The framework invokes the JobSplitter.Split method to obtain a sequence of tasks, which it adds to the job as the method returns them.</span></span> <span data-ttu-id="7ea37-178">작업의 논리를 삽입할 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-178">This is the class where you will inject the logic of your job.</span></span> <span data-ttu-id="7ea37-179">작업을 파티션할 태스크를 나타내는 CloudTask 인스턴스 시퀀스를 반환할 Split 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-179">Implement the Split method to return a sequence of CloudTask instances representing the tasks into which you want to partition the job.</span></span>

<span data-ttu-id="7ea37-180">**표준 .NET 명령줄 프로젝트 파일**</span><span class="sxs-lookup"><span data-stu-id="7ea37-180">**Standard .NET command line project files**</span></span>

* <span data-ttu-id="7ea37-181">`App.config`: 표준 .NET 응용 프로그램 구성 파일</span><span class="sxs-lookup"><span data-stu-id="7ea37-181">`App.config`: Standard .NET application configuration file.</span></span>
* <span data-ttu-id="7ea37-182">`Packages.config`: 표준 NuGet 패키지 종속성 파일</span><span class="sxs-lookup"><span data-stu-id="7ea37-182">`Packages.config`: Standard NuGet package dependency file.</span></span>
* <span data-ttu-id="7ea37-183">`Program.cs`: 프로그램 진입점과 최상위 예외 처리가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-183">`Program.cs`: Contains the program entry point and top-level exception handling.</span></span>

### <a name="implementing-the-job-splitter"></a><span data-ttu-id="7ea37-184">작업 분할자 구현</span><span class="sxs-lookup"><span data-stu-id="7ea37-184">Implementing the job splitter</span></span>
<span data-ttu-id="7ea37-185">작업 관리자 템플릿 프로젝트를 열면 프로젝트에 기본적으로 JobSplitter.cs 파일이 열려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-185">When you open the Job Manager template project, the project will have the JobSplitter.cs file open by default.</span></span> <span data-ttu-id="7ea37-186">아래 표시된 Split() 메서드를 사용하여 워크로드에서 태스크에 대한 분할 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-186">You can implement the split logic for the tasks in your workload by using the Split() method show below:</span></span>

```csharp
/// <summary>
/// Gets the tasks into which to split the job. This is where you inject
/// your application-specific logic for decomposing the job into tasks.
///
/// The job manager framework invokes the Split method for you; you need
/// only to implement it, not to call it yourself. Typically, your
/// implementation should return tasks lazily, for example using a C#
/// iterator and the "yield return" statement; this allows tasks to be added
/// and to start running while splitting is still in progress.
/// </summary>
/// <returns>The tasks to be added to the job. Tasks are added automatically
/// by the job manager framework as they are returned by this method.</returns>
public IEnumerable<CloudTask> Split()
{
    // Your code for the split logic goes here.
    int startFrame = Convert.ToInt32(_parameters["StartFrame"]);
    int endFrame = Convert.ToInt32(_parameters["EndFrame"]);

    for (int i = startFrame; i <= endFrame; i++)
    {
        yield return new CloudTask("myTask" + i, "cmd /c dir");
    }
}
```

> [!NOTE]
> <span data-ttu-id="7ea37-187">`Split()` 메서드에서 주석이 지정된 섹션은 작업을 서로 다른 태스크로 분리하는 논리를 추가하여 수정하려는 작업 관리자 템플릿 코드의 유일한 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-187">The annotated section in the `Split()` method is the only section of the Job Manager template code that is intended for you to modify by adding the logic to split your jobs into different tasks.</span></span> <span data-ttu-id="7ea37-188">템플릿의 다른 섹션을 수정하려는 경우 Batch가 작동하는 방식을 파악하고 몇 가지 [Batch 코드 샘플][github_samples]을 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="7ea37-188">If you want to modify a different section of the template, please ensure you are familiarized with how Batch works, and try out a few of the [Batch code samples][github_samples].</span></span>
> 
> 

<span data-ttu-id="7ea37-189">Split() 구현에서는 다음에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-189">Your Split() implementation has access to:</span></span>

* <span data-ttu-id="7ea37-190">`_parameters` 필드를 통해 작업 매개 변수에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-190">The job parameters, via the `_parameters` field.</span></span>
* <span data-ttu-id="7ea37-191">`_job` 필드를 통해 작업을 나타내는 CloudJob 개체에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-191">The CloudJob object representing the job, via the `_job` field.</span></span>
* <span data-ttu-id="7ea37-192">`_jobManagerTask` 필드를 통해 작업 관리자 태스크를 나타내는 CloudTask 개체에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-192">The CloudTask object representing the job manager task, via the `_jobManagerTask` field.</span></span>

<span data-ttu-id="7ea37-193">`Split()` 구현에서는 태스크를 작업에 직접 추가하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-193">Your `Split()` implementation does not need to add tasks to the job directly.</span></span> <span data-ttu-id="7ea37-194">대신, 코드가 CloudTask 개체의 시퀀스를 반환하고 이러한 개체는 작업 분할자를 호출하는 프레임워크 클래스에 의해 작업에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-194">Instead, your code should return a sequence of CloudTask objects, and these will be added to the job automatically by the framework classes that invoke the job splitter.</span></span> <span data-ttu-id="7ea37-195">일반적으로 C#의 반복기(`yield return`) 기능을 사용하여 모든 태스크가 계산될 때까지 기다리지 않고 가능한 빨리 실행을 시작할 수 있도록 작업 분할자를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-195">It's common to use C#'s iterator (`yield return`) feature to implement job splitters as this allows the tasks to start running as soon as possible rather than waiting for all tasks to be calculated.</span></span>

<span data-ttu-id="7ea37-196">**작업 분할자 실패**</span><span class="sxs-lookup"><span data-stu-id="7ea37-196">**Job splitter failure**</span></span>

<span data-ttu-id="7ea37-197">작업 분할자에 오류가 발생하는 경우 다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-197">If your job splitter encounters an error, it should either:</span></span>

* <span data-ttu-id="7ea37-198">C# `yield break` 문을 사용하여 시퀀스를 종료합니다. 이 경우 작업 관리자가 성공으로 처리됩니다. 또는</span><span class="sxs-lookup"><span data-stu-id="7ea37-198">Terminate the sequence using the C# `yield break` statement, in which case the job manager will be treated as successful; or</span></span>
* <span data-ttu-id="7ea37-199">예외를 Throw합니다. 이 경우 작업 관리자는 실패로 처리되며 클라이언트가 구성된 방식에 따라 재시도될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-199">Throw an exception, in which case the job manager will be treated as failed and may be retried depending on how the client has configured it).</span></span>

<span data-ttu-id="7ea37-200">두 경우 모두, 작업 분할자에 의해 이미 반환되어 배치 작업에 추가된 모든 태스크를 실행할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-200">In both cases, any tasks already returned by the job splitter and added to the Batch job will be eligible to run.</span></span> <span data-ttu-id="7ea37-201">이러한 경우가 발생하지 않도록 하려면 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-201">If you don't want this to happen, then you could:</span></span>

* <span data-ttu-id="7ea37-202">작업 분할자에서 반환하기 전에 작업 종료</span><span class="sxs-lookup"><span data-stu-id="7ea37-202">Terminate the job before returning from the job splitter</span></span>
* <span data-ttu-id="7ea37-203">반환하기 전에 전체 태스크 컬렉션 작성(즉, C# 반복기를 사용하여 작업 분할자를 구현하는 대신 `ICollection<CloudTask>` 하나에 `IList<CloudTask>` instead of implementing your job splitter using a C# iterat하나에)</span><span class="sxs-lookup"><span data-stu-id="7ea37-203">Formulate the entire task collection before returning it (that is, return an `ICollection<CloudTask>` or `IList<CloudTask>` instead of implementing your job splitter using a C# iterator)</span></span>
* <span data-ttu-id="7ea37-204">태스크 종속성을 사용하여 모든 태스크가 작업 관리자의 성공적인 완료에 종속되도록 함</span><span class="sxs-lookup"><span data-stu-id="7ea37-204">Use task dependencies to make all tasks depend on the successful completion of the job manager</span></span>

<span data-ttu-id="7ea37-205">**작업 관리자 재시도**</span><span class="sxs-lookup"><span data-stu-id="7ea37-205">**Job manager retries**</span></span>

<span data-ttu-id="7ea37-206">작업 관리자가 실패하는 경우 클라이언트 재시도 설정에 따라 배치 서비스에 의해 재시도될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-206">If the job manager fails, it may be retried by the Batch service depending on the client retry settings.</span></span> <span data-ttu-id="7ea37-207">일반적으로 이 방법은 프레임워크가 태스크를 작업에 추가할 경우 이미 존재하는 모든 태스크를 무시하므로 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-207">In general, this is safe, because when the framework adds tasks to the job, it ignores any tasks that already exist.</span></span> <span data-ttu-id="7ea37-208">그러나 태스크 계산 비용이 많이 드는 경우 작업에 이미 추가했던 태스크를 다시 계산하는 비용이 발생하는 것을 원하지 않을 수 있으며 반대로, 다시 실행한다고 해도 동일한 태스크 ID가 생성된다는 보장이 없는 경우 '중복 무시' 동작이 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-208">However, if calculating tasks is expensive, you may not wish to incur the cost of recalculating tasks that have already been added to the job; conversely, if the re-run is not guaranteed to generate the same task IDs then the 'ignore duplicates' behavior will not kick in.</span></span> <span data-ttu-id="7ea37-209">이러한 경우 예를 들어 태스크가 생성되기 시작하기 전에 CloudJob.ListTasks를 수행하여 이미 수행되었고 반복되지 않는 작업을 검색하도록 작업 분할자를 설계해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-209">In these cases you should design your job splitter to detect the work that has already been done and not repeat it, for example by performing a CloudJob.ListTasks before starting to yield tasks.</span></span>

### <a name="exit-codes-and-exceptions-in-the-job-manager-template"></a><span data-ttu-id="7ea37-210">작업 관리자 템플릿에서 종료 코드 및 예외</span><span class="sxs-lookup"><span data-stu-id="7ea37-210">Exit codes and exceptions in the Job Manager template</span></span>
<span data-ttu-id="7ea37-211">종료 코드 및 예외는 프로그램 실행 결과를 확인하는 메커니즘을 제공하며 프로그램의 실행 시 발생하는 문제를 식별하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-211">Exit codes and exceptions provide a mechanism to determine the outcome of running a program, and they can help to identify any problems with the execution of the program.</span></span> <span data-ttu-id="7ea37-212">작업 관리자 템플릿은 이 섹션에 설명된 종료 코드 및 예외를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-212">The Job Manager template implements the exit codes and exceptions described in this section.</span></span>

<span data-ttu-id="7ea37-213">작업 관리자 템플릿으로 구현된 작업 관리자 태스크는 세 가지 가능한 종료 코드를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-213">A job manager task that is implemented with the Job Manager template can return three possible exit codes:</span></span>

| <span data-ttu-id="7ea37-214">코드</span><span class="sxs-lookup"><span data-stu-id="7ea37-214">Code</span></span> | <span data-ttu-id="7ea37-215">설명</span><span class="sxs-lookup"><span data-stu-id="7ea37-215">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7ea37-216">0</span><span class="sxs-lookup"><span data-stu-id="7ea37-216">0</span></span> |<span data-ttu-id="7ea37-217">작업 관리자가 성공적으로 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-217">The job manager completed successfully.</span></span> <span data-ttu-id="7ea37-218">작업 분할자 코드가 완료될 때까지 실행되고 모든 태스크가 작업에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-218">Your job splitter code ran to completion, and all tasks were added to the job.</span></span> |
| <span data-ttu-id="7ea37-219">1</span><span class="sxs-lookup"><span data-stu-id="7ea37-219">1</span></span> |<span data-ttu-id="7ea37-220">작업 관리자 태스크가 프로그램의 '예상된' 부분에서 예외로 인해 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-220">The job manager task failed with an exception in an 'expected' part of the program.</span></span> <span data-ttu-id="7ea37-221">예외는 진단 정보 및 가능한 경우, 오류를 해결하기 위한 제안과 함께 JobManagerException으로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-221">The exception was translated to a JobManagerException with diagnostic information and, where possible, suggestions for resolving the failure.</span></span> |
| <span data-ttu-id="7ea37-222">2</span><span class="sxs-lookup"><span data-stu-id="7ea37-222">2</span></span> |<span data-ttu-id="7ea37-223">작업 관리자 태스크가 '예기치 않은' 예외로 인해 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-223">The job manager task failed with an 'unexpected' exception.</span></span> <span data-ttu-id="7ea37-224">예외는 표준 출력에 기록되었지만 작업 관리자가 추가 진단 또는 재구성 정보를 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-224">The exception was logged to standard output, but the job manager was unable to add any additional diagnostic or remediation information.</span></span> |

<span data-ttu-id="7ea37-225">작업 관리자 태스크가 실패하는 경우 일부 태스크는 오류가 발생하기 전에 서비스에 추가되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-225">In the case of job manager task failure, some tasks may still have been added to the service before the error occurred.</span></span> <span data-ttu-id="7ea37-226">이러한 태스크는 정상적으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-226">These tasks will run as normal.</span></span> <span data-ttu-id="7ea37-227">이 코드 경로에 대한 설명은 위의 "작업 분할자 오류"를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ea37-227">See "Job Splitter Failure" above for discussion of this code path.</span></span>

<span data-ttu-id="7ea37-228">예외에서 반환된 모든 정보는 stdout.txt 및 stderr.txt 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-228">All the information returned by exceptions is written into stdout.txt and stderr.txt files.</span></span> <span data-ttu-id="7ea37-229">자세한 내용은 [오류 처리](batch-api-basics.md#error-handling)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ea37-229">For more information, see [Error Handling](batch-api-basics.md#error-handling).</span></span>

### <a name="client-considerations"></a><span data-ttu-id="7ea37-230">클라이언트 고려 사항</span><span class="sxs-lookup"><span data-stu-id="7ea37-230">Client considerations</span></span>
<span data-ttu-id="7ea37-231">이 섹션에서는 이 템플릿을 기반으로 작업 관리자를 호출할 때 일부 클라이언트 구현 요구 사항에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-231">This section describes some client implementation requirements when invoking a job manager based on this template.</span></span> <span data-ttu-id="7ea37-232">매개 변수 및 환경 설정 전달에 대한 자세한 내용은 [클라이언트 코드에서 매개 변수 및 환경 변수를 전달하는 방법](#pass-environment-settings) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ea37-232">See [How to pass parameters and environment variables from the client code](#pass-environment-settings) for details on passing parameters and environment settings.</span></span>

<span data-ttu-id="7ea37-233">**필수 자격 증명**</span><span class="sxs-lookup"><span data-stu-id="7ea37-233">**Mandatory credentials**</span></span>

<span data-ttu-id="7ea37-234">Azure 배치 작업에 태스크를 추가하려면 작업 관리자 태스크에 Azure 배치 계정 URL과 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-234">In order to add tasks to the Azure Batch job, the job manager task requires your Azure Batch account URL and key.</span></span> <span data-ttu-id="7ea37-235">YOUR_BATCH_URL 및 YOUR_BATCH_KEY라는 환경 변수에 이를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-235">You must pass these in environment variables named YOUR_BATCH_URL and YOUR_BATCH_KEY.</span></span> <span data-ttu-id="7ea37-236">작업 관리자 태스크 환경 설정에서 이러한 내용을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-236">You can set these in the Job Manager task environment settings.</span></span> <span data-ttu-id="7ea37-237">예를 들어 C# 클라이언트에서 다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-237">For example, in a C# client:</span></span>

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    new EnvironmentSetting("YOUR_BATCH_URL", "https://account.region.batch.azure.com"),
    new EnvironmentSetting("YOUR_BATCH_KEY", "{your_base64_encoded_account_key}"),
};
```
<span data-ttu-id="7ea37-238">**Storage 자격 증명**</span><span class="sxs-lookup"><span data-stu-id="7ea37-238">**Storage credentials**</span></span>

<span data-ttu-id="7ea37-239">일반적으로 (a) 대부분의 작업 관리자는 연결된 저장소 계정에 명시적으로 액세스할 필요가 없으므로 클라이언트는 작업 관리자 태스크에 연결된 저장소 계정을 제공하지 않아도 되며 (b) 대체로 연결된 저장소 계정이 작업에 대한 일반 환경 설정으로 모든 태스크에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-239">Typically, the client does not need to provide the linked storage account credentials to the job manager task because (a) most job managers do not need to explicitly access the linked storage account and (b) the linked storage account is often provided to all tasks as a common environment setting for the job.</span></span> <span data-ttu-id="7ea37-240">일반 환경 설정을 통해 연결된 저장소 계정을 제공하지 않는 경우 작업 관리자는 연결된 저장소에 액세스해야 하며 다음과 같이 연결된 저장소 자격 증명을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-240">If you are not providing the linked storage account via the common environment settings, and the job manager requires access to linked storage, then you should supply the linked storage credentials as follows:</span></span>

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    /* other environment settings */
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

<span data-ttu-id="7ea37-241">**작업 관리자 태스크 설정**</span><span class="sxs-lookup"><span data-stu-id="7ea37-241">**Job manager task settings**</span></span>

<span data-ttu-id="7ea37-242">클라이언트는 작업 관리자 *killJobOnCompletion* 플래그를 **false**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-242">The client should set the job manager *killJobOnCompletion* flag to **false**.</span></span>

<span data-ttu-id="7ea37-243">클라이언트가 *runExclusive* 를 **false**로 설정하는 것이 일반적으로 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-243">It is usually safe for the client to set *runExclusive* to **false**.</span></span>

<span data-ttu-id="7ea37-244">클라이언트는 *resourceFiles* 또는 *applicationPackageReferences* 컬렉션을 사용하여 작업 관리자 실행 파일(및 필요한 DLL)이 계산 노드에 배포되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-244">The client should use the *resourceFiles* or *applicationPackageReferences* collection to have the job manager executable (and its required DLLs) deployed to the compute node.</span></span>

<span data-ttu-id="7ea37-245">기본적으로 작업 관리자는 실패한 경우 재시도되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-245">By default, the job manager will not be retried if it fails.</span></span> <span data-ttu-id="7ea37-246">사용자의 작업 논리자 논리에 따라 클라이언트가 *constraints*/*maxTaskRetryCount*를 통해 재시도를 활성화하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-246">Depending on your job manager logic, the client may want to enable retries via *constraints*/*maxTaskRetryCount*.</span></span>

<span data-ttu-id="7ea37-247">**작업 설정**</span><span class="sxs-lookup"><span data-stu-id="7ea37-247">**Job settings**</span></span>

<span data-ttu-id="7ea37-248">작업 분할자가 종속성과 함께 태스크를 내보내는 경우 클라이언트는 작업의 usesTaskDependencies를 true로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-248">If the job splitter emits tasks with dependencies, the client must set the job's usesTaskDependencies to true.</span></span>

<span data-ttu-id="7ea37-249">작업 분할자 모델에서는 클라이언트가 작업 분할자가 생성한 것 이상으로 작업에 태스크를 추가하려는 것은 정상적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-249">In the job splitter model, it is unusual for clients to wish to add tasks to jobs over and above what the job splitter creates.</span></span> <span data-ttu-id="7ea37-250">따라서 클라이언트는 일반적으로 작업의 *onAllTasksComplete* 를 **terminatejob**으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-250">The client should therefore normally set the job's *onAllTasksComplete* to **terminatejob**.</span></span>

## <a name="task-processor-template"></a><span data-ttu-id="7ea37-251">태스크 프로세서 템플릿</span><span class="sxs-lookup"><span data-stu-id="7ea37-251">Task Processor template</span></span>
<span data-ttu-id="7ea37-252">태스크 프로세서 템플릿을 통해 다음 작업을 수행할 수 있는 태스크 프로세서를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-252">A Task Processor template helps you to implement a task processor that can perform the following actions:</span></span>

* <span data-ttu-id="7ea37-253">각 배치 태스크를 실행하는 데 필요한 정보를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-253">Set up the information required by each Batch task to run.</span></span>
* <span data-ttu-id="7ea37-254">각 배치 태스크에 필요한 모든 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-254">Run all actions required by each Batch task.</span></span>
* <span data-ttu-id="7ea37-255">태스크 출력을 영구 저장소에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-255">Save task outputs to persistent storage.</span></span>

<span data-ttu-id="7ea37-256">배치에서 태스크를 실행하는 데 태스크 프로세서가 반드시 필요하지는 않지만 태스크 프로세서를 사용할 경우 주요 장점은 한 위치에서 모든 태스크 실행 작업을 구현하는 래퍼를 제공한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-256">Although a task processor is not required to run tasks on Batch, the key advantage of using a task processor is that it provides a wrapper to implement all task execution actions in one location.</span></span> <span data-ttu-id="7ea37-257">예를 들어 각 태스크의 컨텍스트에서 여러 응용 프로그램을 실행해야 하는 경우 또는 각 태스크를 완료한 후 데이터를 영구 저장소에 복사해야 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-257">For example, if you need to run several applications in the context of each task, or if you need to copy data to persistent storage after completing each task.</span></span>

<span data-ttu-id="7ea37-258">태스크 프로세서가 수행하는 작업은 단순 또는 복잡할 수 있으며 워크로드의 필요에 따라 많거나 적을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-258">The actions performed by the task processor can be as simple or complex, and as many or as few, as required by your workload.</span></span> <span data-ttu-id="7ea37-259">또한 모든 태스크 작업을 하나의 태스크 프로세서로 구현하여 응용 프로그램 또는 워크로드 요구 사항의 변경에 따라 작업을 쉽게 업데이트 또는 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-259">Additionally, by implementing all task actions into one task processor, you can readily update or add actions based on changes to applications or workload requirements.</span></span> <span data-ttu-id="7ea37-260">그러나 예를 들어 간단한 명령줄에서 신속하게 시작할 수 있는 작업을 실행하는 경우처럼 일부 경우에는 태스크 프로세서가 불필요한 복잡성을 추가할 수 있으므로 사용자 구현에 대해 최적의 솔루션이 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-260">However, in some cases a task processor might not be the optimal solution for your implementation as it can add unnecessary complexity, for example when running jobs that can be quickly started from a simple command line.</span></span>

### <a name="create-a-task-processor-using-the-template"></a><span data-ttu-id="7ea37-261">템플릿을 사용하여 태스크 프로세서 만들기</span><span class="sxs-lookup"><span data-stu-id="7ea37-261">Create a Task Processor using the template</span></span>
<span data-ttu-id="7ea37-262">이전에 만든 솔루션에 태스크 프로세서를 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-262">To add a task processor to the solution that you created earlier, follow these steps:</span></span>

1. <span data-ttu-id="7ea37-263">Visual Studio에서 기존 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-263">Open your existing solution in Visual Studio.</span></span>
2. <span data-ttu-id="7ea37-264">솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 후 **새 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-264">In Solution Explorer, right-click the solution, click **Add**, and then click **New Project**.</span></span>
3. <span data-ttu-id="7ea37-265">**Visual C#** 아래에서 **클라우드**를 클릭한 후 **Azure 배치 태스크 프로세서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-265">Under **Visual C#**, click **Cloud**, and then click **Azure Batch Task Processor**.</span></span>
4. <span data-ttu-id="7ea37-266">응용 프로그램을 설명하고 이 프로젝트를 태스크 프로세서로 식별하는 이름을 입력합니다(예: "LitwareTaskProcessor").</span><span class="sxs-lookup"><span data-stu-id="7ea37-266">Type a name that describes your application and identifies this project as the task processor (e.g. "LitwareTaskProcessor").</span></span>
5. <span data-ttu-id="7ea37-267">프로젝트를 만들려면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-267">To create the project, click **OK**.</span></span>
6. <span data-ttu-id="7ea37-268">마지막으로, 프로젝트를 빌드하여 Visual Studio에서 모든 참조된 NuGet 패키지를 로드하고 수정을 시작하기 전에 해당 프로젝트가 유효한지 확인하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-268">Finally, build the project to force Visual Studio to load all referenced NuGet packages and to verify that the project is valid before you start modifying it.</span></span>

### <a name="task-processor-template-files-and-their-purpose"></a><span data-ttu-id="7ea37-269">태스크 프로세서 템플릿 파일 및 그 용도</span><span class="sxs-lookup"><span data-stu-id="7ea37-269">Task Processor template files and their purpose</span></span>
<span data-ttu-id="7ea37-270">태스크 프로세서 템플릿을 사용하여 프로젝트를 만들면 세 가지 코드 파일 그룹이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-270">When you create a project using the task processor template, it generates three groups of code files:</span></span>

* <span data-ttu-id="7ea37-271">메인 프로그램 파일(Program.cs).</span><span class="sxs-lookup"><span data-stu-id="7ea37-271">The main program file (Program.cs).</span></span> <span data-ttu-id="7ea37-272">여기에는 프로그램 진입점과 최상위 예외 처리가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-272">This contains the program entry point and top-level exception handling.</span></span> <span data-ttu-id="7ea37-273">일반적으로 이 값을 수정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-273">You shouldn't normally need to modify this.</span></span>
* <span data-ttu-id="7ea37-274">프레임워크 디렉터리.</span><span class="sxs-lookup"><span data-stu-id="7ea37-274">The Framework directory.</span></span> <span data-ttu-id="7ea37-275">여기에는 매개 변수 압축 해제, 배치 작업에 태스크 추가 등 작업 관리자 프로그램이 수행했던 '상용구' 작업을 담당하는 파일이 포함됩니다. 일반적으로 이러한 파일을 수정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-275">This contains the files responsible for the 'boilerplate' work done by the job manager program – unpacking parameters, adding tasks to the Batch job, etc. You shouldn't normally need to modify these files.</span></span>
* <span data-ttu-id="7ea37-276">태스크 프로세서 파일(TaskProcessor.cs).</span><span class="sxs-lookup"><span data-stu-id="7ea37-276">The task processor file (TaskProcessor.cs).</span></span> <span data-ttu-id="7ea37-277">태스크를 실행(일반적으로 기존 실행 파일을 호출)하기 위해 응용 프로그램 관련 논리를 배치할 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-277">This is where you will put your application-specific logic for executing a task (typically by calling out to an existing executable).</span></span> <span data-ttu-id="7ea37-278">전처리 및 후처리 코드(예: 추가 데이터 다운로드 또는 결과 파일 업로드 등)도 여기에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-278">Pre- and post-processing code, such as downloading additional data or uploading result files, also goes here.</span></span>

<span data-ttu-id="7ea37-279">물론 작업 분할 논리의 복잡성에 따라 태스크 프로세서 코드를 지원하는 데 필요하다면 파일을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-279">Of course you can add additional files as required to support your task processor code, depending on the complexity of the job splitting logic.</span></span>

<span data-ttu-id="7ea37-280">템플릿에서는 .csproj 파일, app.config, packages.config 등과 같은 표준 .NET 프로젝트 파일도 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-280">The template also generates standard .NET project files such as a .csproj file, app.config, packages.config, etc.</span></span>

<span data-ttu-id="7ea37-281">이 섹션의 나머지에서는 다양한 파일 및 해당 코드 구조를 설명하고 각 클래스에서 어떤 작업을 수행하는지 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-281">The rest of this section describes the different files and their code structure, and explains what each class does.</span></span>

![태스크 프로세서 템플릿 솔루션을 보여 주는 Visual Studio 솔루션 탐색기][solution_explorer02]

<span data-ttu-id="7ea37-283">**프레임워크 파일**</span><span class="sxs-lookup"><span data-stu-id="7ea37-283">**Framework files**</span></span>

* <span data-ttu-id="7ea37-284">`Configuration.cs`: 배치 계정 정보, 연결된 저장소 계정 자격 증명, 작업 및 태스크 정보 및 작업 매개 변수와 같은 작업 구성 데이터의 로드를 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-284">`Configuration.cs`: Encapsulates the loading of job configuration data such as Batch account details, linked storage account credentials, job and task information, and job parameters.</span></span> <span data-ttu-id="7ea37-285">또한 Configuration.EnvironmentVariable 클래스를 통해 배치 정의된 환경 변수(배치 설명서에서 태스크에 대한 환경 설정 참조)에 대한 액세스도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-285">It also provides access to Batch-defined environment variables (see Environment settings for tasks, in the Batch documentation) via the Configuration.EnvironmentVariable class.</span></span>
* <span data-ttu-id="7ea37-286">`IConfiguration.cs`: 모조 또는 모의 구성 개체를 사용하여 작업 분할자의 단위 태스크를 수행할 수 있도록 구성 클래스의 구현을 추상화합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-286">`IConfiguration.cs`: Abstracts the implementation of the Configuration class, so that you can unit test your job splitter using a fake or mock configuration object.</span></span>
* <span data-ttu-id="7ea37-287">`TaskProcessorException.cs`: 작업 관리자를 종료해야 하는 오류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-287">`TaskProcessorException.cs`: Represents an error that requires the job manager to terminate.</span></span> <span data-ttu-id="7ea37-288">TaskProcessorException은 종료의 일부분으로 특정 진단 정보를 제공할 수 있는 '예상된' 오류를 래핑하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-288">TaskProcessorException is used to wrap 'expected' errors where specific diagnostic information can be provided as part of termination.</span></span>

<span data-ttu-id="7ea37-289">**태스크 프로세서**</span><span class="sxs-lookup"><span data-stu-id="7ea37-289">**Task Processor**</span></span>

* <span data-ttu-id="7ea37-290">`TaskProcessor.cs`: 태스크를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-290">`TaskProcessor.cs`: Runs the task.</span></span> <span data-ttu-id="7ea37-291">프레임워크는 TaskProcessor.Run 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-291">The framework invokes the TaskProcessor.Run method.</span></span> <span data-ttu-id="7ea37-292">태스크의 응용 프로그램 관련 논리를 삽입할 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-292">This is the class where you will inject the application-specific logic of your task.</span></span> <span data-ttu-id="7ea37-293">다음을 수행하는 Run 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-293">Implement the Run method to:</span></span>
  * <span data-ttu-id="7ea37-294">태스크 매개 변수 구문 분석 및 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="7ea37-294">Parse and validate any task parameters</span></span>
  * <span data-ttu-id="7ea37-295">호출하려는 모든 외부 프로그램에 대한 명령줄 작성</span><span class="sxs-lookup"><span data-stu-id="7ea37-295">Compose the command line for any external program you want to invoke</span></span>
  * <span data-ttu-id="7ea37-296">디버깅 용도로 필요할 수 있는 모든 진단 정보 기록</span><span class="sxs-lookup"><span data-stu-id="7ea37-296">Log any diagnostic information you may require for debugging purposes</span></span>
  * <span data-ttu-id="7ea37-297">해당 명령줄을 사용하는 프로세스 시작</span><span class="sxs-lookup"><span data-stu-id="7ea37-297">Start a process using that command line</span></span>
  * <span data-ttu-id="7ea37-298">프로세스가 종료될 때까지 대기</span><span class="sxs-lookup"><span data-stu-id="7ea37-298">Wait for the process to exit</span></span>
  * <span data-ttu-id="7ea37-299">성공 또는 실패를 확인하기 위해 프로세스의 종료 코드 캡처</span><span class="sxs-lookup"><span data-stu-id="7ea37-299">Capture the exit code of the process to determine if it succeeded or failed</span></span>
  * <span data-ttu-id="7ea37-300">영구 저장소에 보관하려는 모든 출력 파일 저장</span><span class="sxs-lookup"><span data-stu-id="7ea37-300">Save any output files you want to keep to persistent storage</span></span>

<span data-ttu-id="7ea37-301">**표준 .NET 명령줄 프로젝트 파일**</span><span class="sxs-lookup"><span data-stu-id="7ea37-301">**Standard .NET command line project files**</span></span>

* <span data-ttu-id="7ea37-302">`App.config`: 표준 .NET 응용 프로그램 구성 파일</span><span class="sxs-lookup"><span data-stu-id="7ea37-302">`App.config`: Standard .NET application configuration file.</span></span>
* <span data-ttu-id="7ea37-303">`Packages.config`: 표준 NuGet 패키지 종속성 파일</span><span class="sxs-lookup"><span data-stu-id="7ea37-303">`Packages.config`: Standard NuGet package dependency file.</span></span>
* <span data-ttu-id="7ea37-304">`Program.cs`: 프로그램 진입점과 최상위 예외 처리가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-304">`Program.cs`: Contains the program entry point and top-level exception handling.</span></span>

## <a name="implementing-the-task-processor"></a><span data-ttu-id="7ea37-305">태스크 프로세서 구현</span><span class="sxs-lookup"><span data-stu-id="7ea37-305">Implementing the task processor</span></span>
<span data-ttu-id="7ea37-306">태스크 프로세서 템플릿 프로젝트를 열면 프로젝트에 기본적으로 TaskProcessor.cs 파일이 열려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-306">When you open the Task Processor template project, the project will have the TaskProcessor.cs file open by default.</span></span> <span data-ttu-id="7ea37-307">아래 표시된 Run() 메서드를 사용하여 워크로드에서 태스크에 대한 실행 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-307">You can implement the run logic for the tasks in your workload by using the Run() method shown below:</span></span>

```csharp
/// <summary>
/// Runs the task processing logic. This is where you inject
/// your application-specific logic for decomposing the job into tasks.
///
/// The task processor framework invokes the Run method for you; you need
/// only to implement it, not to call it yourself. Typically, your
/// implementation will execute an external program (from resource files or
/// an application package), check the exit code of that program and
/// save output files to persistent storage.
/// </summary>
public async Task<int> Run()

{
    try
    {
        //Your code for the task processor goes here.
        var command = $"compare {_parameters["Frame1"]} {_parameters["Frame2"]} compare.gif";
        using (var process = Process.Start($"cmd /c {command}"))
        {
            process.WaitForExit();
            var taskOutputStorage = new TaskOutputStorage(
            _configuration.StorageAccount,
            _configuration.JobId,
            _configuration.TaskId
            );
            await taskOutputStorage.SaveAsync(
            TaskOutputKind.TaskOutput,
            @"..\stdout.txt",
            @"stdout.txt"
            );
            return process.ExitCode;
        }
    }
    catch (Exception ex)
    {
        throw new TaskProcessorException(
        $"{ex.GetType().Name} exception in run task processor: {ex.Message}",
        ex
        );
    }
}
```
> [!NOTE]
> <span data-ttu-id="7ea37-308">Run() 메서드에서 주석이 지정된 섹션은 워크로드에 태스크에 대한 실행 논리를 추가하여 수정하려는 태스크 프로세서 템플릿 코드의 유일한 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-308">The annotated section in the Run() method is the only section of the Task Processor template code that is intended for you to modify by adding the run logic for the tasks in your workload.</span></span> <span data-ttu-id="7ea37-309">템플릿의 다른 섹션을 수정하려는 경우 배치 설명서를 검토하고 몇 가지 배치 코드 샘플을 사용해 본 후 배치가 작동하는 방식을 직접 파악해 보세요.</span><span class="sxs-lookup"><span data-stu-id="7ea37-309">If you want to modify a different section of the template, please first familiarize yourself with how Batch works by reviewing the Batch documentation and trying out a few of the Batch code samples.</span></span>
> 
> 

<span data-ttu-id="7ea37-310">Run() 메서드는 명령줄을 실행하고 하나 이상의 프로세스를 시작하며 모든 프로세스가 완료될 때까지 기다리고 결과를 저장하며 마지막으로는 종료 코드와 함께 반환하는 일을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-310">The Run() method is responsible for launching the command line, starting one or more processes, waiting for all process to complete, saving the results, and finally returning with an exit code.</span></span> <span data-ttu-id="7ea37-311">Run() 메서드에서 태스크에 대한 처리 논리를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-311">The Run() method is where you implement the processing logic for your tasks.</span></span> <span data-ttu-id="7ea37-312">태스크 프로세서 프레임워크가 사용자 대신 Run() 메서드를 호출하므로 사용자가 직접 호출하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-312">The task processor framework invokes the Run() method for you; you do not need to call it yourself.</span></span>

<span data-ttu-id="7ea37-313">Run() 구현에서는 다음에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-313">Your Run() implementation has access to:</span></span>

* <span data-ttu-id="7ea37-314">`_parameters` 필드를 통해 태스크 매개 변수에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-314">The task parameters, via the `_parameters` field.</span></span>
* <span data-ttu-id="7ea37-315">`_jobId`과 `_taskId` 필드를 통해 작업 및 태스크 ID에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-315">The job and task ids, via the `_jobId` and `_taskId` fields.</span></span>
* <span data-ttu-id="7ea37-316">`_configuration` 필드를 통해 태스크 구성에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-316">The task configuration, via the `_configuration` field.</span></span>

<span data-ttu-id="7ea37-317">**태스크 실패**</span><span class="sxs-lookup"><span data-stu-id="7ea37-317">**Task failure**</span></span>

<span data-ttu-id="7ea37-318">오류가 발생한 경우 예외를 throw하여 Run() 메서드를 종료할 수 있지만 이렇게 하면 최상위 예외 처리기가 태스크 종료 코드 제어 하에 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-318">In case of failure, you can exit the Run() method by throwing an exception, but this leaves the top level exception handler in control of the task exit code.</span></span> <span data-ttu-id="7ea37-319">예를 들어 진단 목적을 위해 다양한 오류 유형을 구분할 수 있도록 종료 코드를 제어해야 하는 경우 또는 일부 오류 모드에서 특정 작업만 종료해야 하므로 0이 아닌 종료 코드를 반환하여 Run() 메서드를 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-319">If you need to control the exit code so that you can distinguish different types of failure, for example for diagnostic purposes or because some failure modes should terminate the job and others should not, then you should exit the Run() method by returning a non-zero exit code.</span></span> <span data-ttu-id="7ea37-320">이것이 태스크 종료 코드가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-320">This becomes the task exit code.</span></span>

### <a name="exit-codes-and-exceptions-in-the-task-processor-template"></a><span data-ttu-id="7ea37-321">태스크 프로세서 템플릿에서 종료 코드 및 예외</span><span class="sxs-lookup"><span data-stu-id="7ea37-321">Exit codes and exceptions in the Task Processor template</span></span>
<span data-ttu-id="7ea37-322">종료 코드 및 예외는 프로그램 실행 결과를 확인하는 메커니즘을 제공하며 프로그램의 실행 시 발생하는 문제를 식별하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-322">Exit codes and exceptions provide a mechanism to determine the outcome of running a program, and they can help identify any problems with the execution of the program.</span></span> <span data-ttu-id="7ea37-323">태스크 프로세서 템플릿은 이 섹션에 설명된 종료 코드 및 예외를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-323">The Task Processor template implements the exit codes and exceptions described in this section.</span></span>

<span data-ttu-id="7ea37-324">태스크 프로세서 템플릿으로 구현된 태스크 프로세서 태스크는 세 가지 가능한 종료 코드를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-324">A task processor task that is implemented with the Task Processor template can return three possible exit codes:</span></span>

| <span data-ttu-id="7ea37-325">코드</span><span class="sxs-lookup"><span data-stu-id="7ea37-325">Code</span></span> | <span data-ttu-id="7ea37-326">설명</span><span class="sxs-lookup"><span data-stu-id="7ea37-326">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7ea37-327">[Process.ExitCode][process_exitcode]</span><span class="sxs-lookup"><span data-stu-id="7ea37-327">[Process.ExitCode][process_exitcode]</span></span> |<span data-ttu-id="7ea37-328">태스크 프로세서가 완료될 때까지 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-328">The task processor ran to completion.</span></span> <span data-ttu-id="7ea37-329">사용자가 호출한 프로그램이 성공했음을 의미하는 것은 아니며 태스크 프로세서가 이를 성공적으로 호출했고 예외 없이 후처리를 수행했음만 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-329">Note that this does not imply that the program you invoked was successful – only that the task processor invoked it successfully and performed any post-processing without exceptions.</span></span> <span data-ttu-id="7ea37-330">종료 코드의 의미는 호출한 프로그램에 따라 다르며 일반적으로 종료 코드 0은 프로그램이 성공했음을 의미하고 그 외의 종료 코드는 프로그램이 실패했음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-330">The meaning of the exit code depends on the invoked program – typically exit code 0 means the program succeeded and any other exit code means the program failed.</span></span> |
| <span data-ttu-id="7ea37-331">1</span><span class="sxs-lookup"><span data-stu-id="7ea37-331">1</span></span> |<span data-ttu-id="7ea37-332">태스크 프로세서가 프로그램의 '예상된' 부분에서 예외로 인해 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-332">The task processor failed with an exception in an 'expected' part of the program.</span></span> <span data-ttu-id="7ea37-333">예외는 진단 정보 및 가능한 경우, 오류를 해결하기 위한 제안과 함께 `TaskProcessorException` 으로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-333">The exception was translated to a `TaskProcessorException` with diagnostic information and, where possible, suggestions for resolving the failure.</span></span> |
| <span data-ttu-id="7ea37-334">2</span><span class="sxs-lookup"><span data-stu-id="7ea37-334">2</span></span> |<span data-ttu-id="7ea37-335">태스크 프로세서가 '예기치 않은' 예외로 인해 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-335">The task processor failed with an 'unexpected' exception.</span></span> <span data-ttu-id="7ea37-336">예외는 표준 출력에 기록되었지만 태스크 프로세서가 추가 진단 또는 재구성 정보를 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-336">The exception was logged to standard output, but the task processor was unable to add any additional diagnostic or remediation information.</span></span> |

> [!NOTE]
> <span data-ttu-id="7ea37-337">호출한 프로그램에서 특정 오류 모드를 나타내기 위해 종료 코드 1 및 2를 사용하는 경우 태스크 프로세서 오류에 대해 종료 코드 1 및 2를 사용하는 것이 모호합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-337">If the program you invoke uses exit codes 1 and 2 to indicate specific failure modes, then using exit codes 1 and 2 for task processor errors is ambiguous.</span></span> <span data-ttu-id="7ea37-338">Program.cs 파일에서 예외 사례를 편집하여 이러한 태스크 프로세서 오류 코드를 고유한 종료 코드로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-338">You can change these task processor error codes to distinctive exit codes by editing the exception cases in the Program.cs file.</span></span>
> 
> 

<span data-ttu-id="7ea37-339">예외에서 반환된 모든 정보는 stdout.txt 및 stderr.txt 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-339">All the information returned by exceptions is written into stdout.txt and stderr.txt files.</span></span> <span data-ttu-id="7ea37-340">자세한 내용은 배치 설명서의 오류 처리를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ea37-340">For more information, see Error Handling, in the Batch documentation.</span></span>

### <a name="client-considerations"></a><span data-ttu-id="7ea37-341">클라이언트 고려 사항</span><span class="sxs-lookup"><span data-stu-id="7ea37-341">Client considerations</span></span>
<span data-ttu-id="7ea37-342">**Storage 자격 증명**</span><span class="sxs-lookup"><span data-stu-id="7ea37-342">**Storage credentials**</span></span>

<span data-ttu-id="7ea37-343">태스크 프로세서에서 출력을 유지하기 위해 Azure Blob 저장소를 사용하는 경우(예를 들어 파일 규약 도우미 라이브러리를 사용하는 경우) 클라우드 저장소 계정 자격 증명 *또는* 공유 액세스 서명(SAS)을 포함하는 Blob 컨테이너 URL 중 *하나에* 액세스해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-343">If your task processor uses Azure blob storage to persist outputs, for example using the file conventions helper library, then it needs access to *either* the cloud storage account credentials *or* a blob container URL that includes a shared access signature (SAS).</span></span> <span data-ttu-id="7ea37-344">템플릿에는 일반적인 환경 변수를 통해 자격 증명을 제공하기 위한 지원이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-344">The template includes support for providing credentials via common environment variables.</span></span> <span data-ttu-id="7ea37-345">클라이언트는 다음과 같이 저장소 자격 증명을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-345">Your client can pass the storage credentials as follows:</span></span>

```csharp
job.CommonEnvironmentSettings = new [] {
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

<span data-ttu-id="7ea37-346">그러면 저장소 계정을 `_configuration.StorageAccount` 속성을 통해 TaskProcessor 클래스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-346">The storage account is then available in the TaskProcessor class via the `_configuration.StorageAccount` property.</span></span>

<span data-ttu-id="7ea37-347">SAS와 함께 컨테이너 URL을 사용하는 것을 선호하는 경우 작업의 일반적인 환경 설정을 통해 이를 전달할 수도 있지만 현재 태스크 프로세서 템플릿은 이에 대한 기본 제공 지원을 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-347">If you prefer to use a container URL with SAS, you can also pass this via an job common environment setting, but the task processor template does not currently include built-in support for this.</span></span>

<span data-ttu-id="7ea37-348">**Storage 설정**</span><span class="sxs-lookup"><span data-stu-id="7ea37-348">**Storage setup**</span></span>

<span data-ttu-id="7ea37-349">클라이언트 또는 작업 관리자 태스크는 태스크를 작업에 추가하기 전에 태스크에 필요한 모든 컨테이너를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-349">It is recommended that the client or job manager task create any containers required by tasks before adding the tasks to the job.</span></span> <span data-ttu-id="7ea37-350">SAS와 함께 컨테이너 URL을 사용하는 경우 이러한 URL에는 컨테이너를 생성할 권한이 없으므로 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-350">This is mandatory if you use a container URL with SAS, as such a URL does not include permission to create the container.</span></span> <span data-ttu-id="7ea37-351">컨테이너에서 CloudBlobContainer.CreateIfNotExistsAsync를 호출해야 하는 모든 태스크를 저장하므로 저장소 계정 자격 증명을 전달하는 경우에도 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-351">It is recommended even if you pass storage account credentials, as it saves every task having to call CloudBlobContainer.CreateIfNotExistsAsync on the container.</span></span>

## <a name="pass-parameters-and-environment-variables"></a><span data-ttu-id="7ea37-352">매개 변수 및 환경 변수 전달</span><span class="sxs-lookup"><span data-stu-id="7ea37-352">Pass parameters and environment variables</span></span>
### <a name="pass-environment-settings"></a><span data-ttu-id="7ea37-353">환경 설정 전달</span><span class="sxs-lookup"><span data-stu-id="7ea37-353">Pass environment settings</span></span>
<span data-ttu-id="7ea37-354">클라이언트는 환경 설정 형태로 작업 관리자 태스크에 정보를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-354">A client can pass information to the job manager task in the form of environment settings.</span></span> <span data-ttu-id="7ea37-355">그러면 계산 작업의 일부로 실행할 태스크 프로세서 태스크를 생성할 때 작업 관리자 태스크가 이 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-355">This information can then be used by the job manager task when generating the task processor tasks that will run as part of the compute job.</span></span> <span data-ttu-id="7ea37-356">환경 설정으로 전달할 수 있는 정보의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-356">Examples of the information that you can pass as environment settings are:</span></span>

* <span data-ttu-id="7ea37-357">Storage 계정 이름 및 계정 키</span><span class="sxs-lookup"><span data-stu-id="7ea37-357">Storage account name and account keys</span></span>
* <span data-ttu-id="7ea37-358">배치 계정 URL</span><span class="sxs-lookup"><span data-stu-id="7ea37-358">Batch account URL</span></span>
* <span data-ttu-id="7ea37-359">배치 계정 키</span><span class="sxs-lookup"><span data-stu-id="7ea37-359">Batch account key</span></span>

<span data-ttu-id="7ea37-360">배치 서비스에는 [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask]에서 `EnvironmentSettings` 속성을 사용하여 환경 설정을 작업 관리자 태스크로 전달하는 간단한 메커니즘이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-360">The Batch service has a simple mechanism to pass environment settings to a job manager task by using the `EnvironmentSettings` property in [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask].</span></span>

<span data-ttu-id="7ea37-361">예를 들어 배치 계정에 대한 `BatchClient` 인스턴스를 가져오려면 클라이언트 코드에서 배치 계정에 대한 URL 및 공유 키 자격 증명을 환경 변수로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-361">For example, to get the `BatchClient` instance for a Batch account, you can pass as environment variables from the client code the URL and shared key credentials for the Batch account.</span></span> <span data-ttu-id="7ea37-362">마찬가지로 배치 계정에 연결되는 저장소 계정에 액세스하려면 저장소 계정 이름 및 저장소 계정 키를 환경 변수로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-362">Likewise, to access the storage account that is linked to the Batch account, you can pass the storage account name and the storage account key as environment variables.</span></span>

### <a name="pass-parameters-to-the-job-manager-template"></a><span data-ttu-id="7ea37-363">매개 변수를 작업 관리자 템플릿으로 전달</span><span class="sxs-lookup"><span data-stu-id="7ea37-363">Pass parameters to the Job Manager template</span></span>
<span data-ttu-id="7ea37-364">대부분의 경우 작업 분할 프로세스를 제어하거나 작업에 대한 태스크를 구성하기 위해 작업당 매개 변수를 작업 관리자 태스크로 전달하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-364">In many cases, it's useful to pass per-job parameters to the job manager task, either to control the job splitting process or to configure the tasks for the job.</span></span> <span data-ttu-id="7ea37-365">작업 관리자 태스크에 대한 리소스 파일로 parameters.json이라는 JSON 파일을 업로드하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-365">You can do this by uploading a JSON file named parameters.json as a resource file for the job manager task.</span></span> <span data-ttu-id="7ea37-366">그러면 매개 변수를 작업 관리자 템플릿의 `JobSplitter._parameters` 필드에서 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-366">The parameters can then become available in the `JobSplitter._parameters` field in the Job Manager template.</span></span>

> [!NOTE]
> <span data-ttu-id="7ea37-367">기본 제공 매개 변수 처리기는 문자열-문자열 사전만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-367">The built-in parameter handler supports only string-to-string dictionaries.</span></span> <span data-ttu-id="7ea37-368">복잡한 JSON 값을 매개 변수 값으로 전달하려는 경우 이러한 값을 문자열로 전달하고 작업 분할자에서 구문 분석하거나 프레임워크의 `Configuration.GetJobParameters` 메서드를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-368">If you want to pass complex JSON values as parameter values, you will need to pass these as strings and parse them in the job splitter, or modify the framework's `Configuration.GetJobParameters` method.</span></span>
> 
> 

### <a name="pass-parameters-to-the-task-processor-template"></a><span data-ttu-id="7ea37-369">매개 변수를 태스크 프로세서 템플릿으로 전달</span><span class="sxs-lookup"><span data-stu-id="7ea37-369">Pass parameters to the Task Processor template</span></span>
<span data-ttu-id="7ea37-370">매개 변수를 태스크 프로세서 템플릿을 사용하여 구현된 개별 태스크로 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-370">You can also pass parameters to individual tasks implemented using the Task Processor template.</span></span> <span data-ttu-id="7ea37-371">작업 관리자 템플릿처럼 태스크 프로세서 템플릿은</span><span class="sxs-lookup"><span data-stu-id="7ea37-371">Just as with the job manager template, the task processor template looks for a resource file named</span></span>

<span data-ttu-id="7ea37-372">parameters.json이라는 리소스 파일을 찾고 있는 경우 이를 매개 변수 사전으로 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-372">parameters.json, and if found it loads it as the parameters dictionary.</span></span> <span data-ttu-id="7ea37-373">매개 변수를 태스크 프로세서 태스크로 전달하는 방법에 대한 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-373">There are a couple of options for how to pass parameters to the task processor tasks:</span></span>

* <span data-ttu-id="7ea37-374">작업 매개 변수 JSON을 재사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-374">Reuse the job parameters JSON.</span></span> <span data-ttu-id="7ea37-375">유일한 매개 변수가 작업 수준 매개 변수(예를 들어 렌더링 높이 및 너비)인 경우 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-375">This works well if the only parameters are job-wide ones (for example, a render height and width).</span></span> <span data-ttu-id="7ea37-376">이렇게 하려면 작업 분할자에서 CloudTask를 만들 때 parameters.json 리소스 파일 개체에 대한 참조를 작업 관리자 태스크의 ResourceFiles(`JobSplitter._jobManagerTask.ResourceFiles`)에서 CloudTask의 ResourceFiles 컬렉션으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-376">To do this, when creating a CloudTask in the job splitter, add a reference to the parameters.json resource file object from the job manager task's ResourceFiles (`JobSplitter._jobManagerTask.ResourceFiles`) to the CloudTask's ResourceFiles collection.</span></span>
* <span data-ttu-id="7ea37-377">태스크 관련 parameters.json 문서를 작업 분할자 실행의 일부로 생성 및 업로드하고 태스크 리소스 파일 컬렉션에서 해당 Blob를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-377">Generate and upload a task-specific parameters.json document as part of job splitter execution, and reference that blob in the task's resource files collection.</span></span> <span data-ttu-id="7ea37-378">다양한 태스크에 서로 다른 매개 변수가 있는 경우 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-378">This is necessary if different tasks have different parameters.</span></span> <span data-ttu-id="7ea37-379">프레임 인덱스가 태스크에 매개 변수로 전달되는 3D 렌더링 시나리오를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-379">An example might be a 3D rendering scenario where the frame index is passed to the task as a parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="7ea37-380">기본 제공 매개 변수 처리기는 문자열-문자열 사전만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-380">The built-in parameter handler supports only string-to-string dictionaries.</span></span> <span data-ttu-id="7ea37-381">복잡한 JSON 값을 매개 변수 값으로 전달하려는 경우 이러한 값을 문자열로 전달하고 태스크 프로세서에서 구문 분석하거나 프레임워크의 `Configuration.GetTaskParameters` 메서드를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-381">If you want to pass complex JSON values as parameter values, you will need to pass these as strings and parse them in the task processor, or modify the framework's `Configuration.GetTaskParameters` method.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7ea37-382">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7ea37-382">Next steps</span></span>
### <a name="persist-job-and-task-output-to-azure-storage"></a><span data-ttu-id="7ea37-383">작업 유지 및 Azure Storage에 태스크 출력</span><span class="sxs-lookup"><span data-stu-id="7ea37-383">Persist job and task output to Azure Storage</span></span>
<span data-ttu-id="7ea37-384">Batch 솔루션 개발 시 다른 유용한 도구는 [Azure Batch 파일 규칙][nuget_package]입니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-384">Another helpful tool in Batch solution development is [Azure Batch File Conventions][nuget_package].</span></span> <span data-ttu-id="7ea37-385">배치 .NET 응용 프로그램에서 .NET 클래스 라이브러리(현재 미리 보기 상태)를 사용하면 Azure Storage 간에 태스크 출력을 쉽게 저장하고 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-385">Use this .NET class library (currently in preview) in your Batch .NET applications to easily store and retrieve task outputs to and from Azure Storage.</span></span> <span data-ttu-id="7ea37-386">[Azure 배치 작업 및 태스크 출력 보관](batch-task-output.md) 에는 라이브러리 및 사용법에 대한 자세한 내용이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-386">[Persist Azure Batch job and task output](batch-task-output.md) contains a full discussion of the library and its usage.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="7ea37-387">배치 포럼</span><span class="sxs-lookup"><span data-stu-id="7ea37-387">Batch Forum</span></span>
<span data-ttu-id="7ea37-388">MSDN의 [Azure Batch 포럼][forum]은 Batch를 설명하고 서비스에 대한 질문을 하는 데 많은 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-388">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="7ea37-389">유용한 "고정" 게시물을 참조하고 Batch 솔루션을 빌드하는 동안 질문이 생기면 즉시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="7ea37-389">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[net_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobmanagertask.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[process_exitcode]: https://msdn.microsoft.com/library/system.diagnostics.process.exitcode.aspx
[vs_gallery]: https://visualstudiogallery.msdn.microsoft.com/
[vs_gallery_templates]: https://go.microsoft.com/fwlink/?linkid=820714
[vs_find_use_ext]: https://msdn.microsoft.com/library/dd293638.aspx

[diagram01]: ./media/batch-visual-studio-templates/diagram01.png
[solution_explorer01]: ./media/batch-visual-studio-templates/solution_explorer01.png
[solution_explorer02]: ./media/batch-visual-studio-templates/solution_explorer02.png
