---
title: "Visual Studio 프로젝트 템플릿-Azure 사용 하 여 일괄 처리 솔루션을 구축 aaaStart | Microsoft Docs"
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
ms.openlocfilehash: a61c480ddc4dffd66c01220a137a3e852e39c338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-project-templates-toojump-start-batch-solutions"></a><span data-ttu-id="ed23a-103">Visual Studio 프로젝트 템플릿 toojump 시작 일괄 처리 솔루션을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ed23a-103">Use Visual Studio project templates toojump-start Batch solutions</span></span>

<span data-ttu-id="ed23a-104">hello **작업 관리자** 및 **작업 프로세서 Visual Studio 템플릿** 일괄 처리에 대 한 코드 toohelp 제공 하면 tooimplement 및 포함 된 일괄 처리에서 계산 집약적인 작업 hello 이상 실행 한 작업의 양을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-104">hello **Job Manager** and **Task Processor Visual Studio templates** for Batch provide code toohelp you tooimplement and run your compute-intensive workloads on Batch with hello least amount of effort.</span></span> <span data-ttu-id="ed23a-105">이 문서에서는 이러한 템플릿을 설명 하 고 방법에 대 한 지침을 제공 toouse 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-105">This document describes these templates and provides guidance for how toouse them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed23a-106">이 문서는 유일한 정보 적용 가능한 toothese 두 서식 파일에 설명 하 고 hello 일괄 처리 서비스 및 관련된 tooit 주요 개념에 익숙한 것으로 가정: 풀, 계산 노드, 작업 및 작업, 작업 관리자 태스크가, 환경 변수 및 기타 관련 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-106">This article discusses only information applicable toothese two templates, and assumes that you are familiar with hello Batch service and key concepts related tooit: pools, compute nodes, jobs and tasks, job manager tasks, environment variables, and other relevant information.</span></span> <span data-ttu-id="ed23a-107">자세한 정보를 찾을 수 [Azure 배치 기본 사항](batch-technical-overview.md), [개발자를 위한 일괄 처리 기능 개요](batch-api-basics.md), 및 [.NET 용 hello Azure 배치 라이브러리 시작](batch-dotnet-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-107">You can find more information in [Basics of Azure Batch](batch-technical-overview.md), [Batch feature overview for developers](batch-api-basics.md), and [Get started with hello Azure Batch library for .NET](batch-dotnet-get-started.md).</span></span>
> 
> 

## <a name="high-level-overview"></a><span data-ttu-id="ed23a-108">대략적인 개요</span><span class="sxs-lookup"><span data-stu-id="ed23a-108">High-level overview</span></span>
<span data-ttu-id="ed23a-109">hello 작업 관리자 태스크 프로세서 템플릿과 toocreate 사용 되는 두 개의 유용한 구성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-109">hello Job Manager and Task Processor templates can be used toocreate two useful components:</span></span>

* <span data-ttu-id="ed23a-110">작업을 독립적으로 병렬 실행 가능한 여러 태스크로 나눌 수 있는 작업 분할자를 구현하는 작업 관리자 태스크.</span><span class="sxs-lookup"><span data-stu-id="ed23a-110">A job manager task that implements a job splitter that can break a job down into multiple tasks that can run independently, in parallel.</span></span>
* <span data-ttu-id="ed23a-111">사용 되는 tooperform 전처리 및 후 처리 하는 응용 프로그램 명령줄 주위 수 있는 작업 프로세서입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-111">A task processor that can be used tooperform pre-processing and post-processing around an application command line.</span></span>

<span data-ttu-id="ed23a-112">예를 들어 영화 렌더링 시나리오에서는 hello 작업 분할은 단일 동영상 작업으로 바꿀 수백 또는 수천 개의 개별 프레임을 별도로 처리는 별도 작업.</span><span class="sxs-lookup"><span data-stu-id="ed23a-112">For example, in a movie rendering scenario, hello job splitter would turn a single movie job into hundreds or thousands of separate tasks that would process individual frames separately.</span></span> <span data-ttu-id="ed23a-113">마찬가지로 hello 작업 프로세서는 호출 응용 프로그램 및 모든 종속 된 프로세스에 필요한 toorender 각 프레임을 렌더링 하는 hello 뿐만 아니라 추가 작업 (예를 들어 복사 렌더링 hello 프레임 tooa 저장소 위치)을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-113">Correspondingly, hello task processor would invoke hello rendering application and all dependent processes that are needed toorender each frame, as well as perform any additional actions (for example, copying hello rendered frame tooa storage location).</span></span>

> [!NOTE]
> <span data-ttu-id="ed23a-114">hello 작업 관리자와 작업 프로세서 템플릿은 서로 독립적으로 가로 및 세로 또는 hello 요구 사항 계산 작업의 및 기본 설정에 따라 둘 중 하나만 toouse를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-114">hello Job Manager and Task Processor templates are independent of each other, so you can choose toouse both, or only one of them, depending on hello requirements of your compute job and on your preferences.</span></span>
> 
> 

<span data-ttu-id="ed23a-115">Hello 다이어그램 아래에 나와 있는 것 처럼 이러한 템플릿을 사용 하는 계산 작업 3 가지 단계를 거치게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-115">As shown in hello diagram below, a compute job that uses these templates will go through three stages:</span></span>

1. <span data-ttu-id="ed23a-116">hello 클라이언트 코드 (예: 응용 프로그램, 웹 서비스 등)은 작업 관리자 태스크 hello 작업 관리자 프로그램으로 지정 하는 Azure에서 일괄 처리 서비스는 작업 toohello를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-116">hello client code (e.g., application, web service, etc.) submits a job toohello Batch service on Azure, specifying as its job manager task hello job manager program.</span></span>
2. <span data-ttu-id="ed23a-117">hello 일괄 처리 서비스가 계산 노드에서 hello 작업 관리자 태스크를 실행 하 고 hello 작업 분할자를 실행 하는 hello 작업 프로세서 작업의 수에 따라 지정 많은 계산 노드를 필요에 따라 hello 매개 변수 및 hello 작업 분할자 코드의 사양에 따라 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-117">hello Batch service runs hello job manager task on a compute node and hello job splitter launches hello specified number of task processor tasks, on as many compute nodes as required, based on hello parameters and specifications in hello job splitter code.</span></span>
3. <span data-ttu-id="ed23a-118">hello 작업 프로세서 작업 독립적으로 실행, 병렬로 tooprocess hello 입력된 데이터 및 hello 출력 데이터를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-118">hello task processor tasks run independently, in parallel, tooprocess hello input data and generate hello output data.</span></span>

![클라이언트 코드 hello 일괄 처리 서비스와 상호 작용 하는 방법을 보여 주는 다이어그램][diagram01]

## <a name="prerequisites"></a><span data-ttu-id="ed23a-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ed23a-120">Prerequisites</span></span>
<span data-ttu-id="ed23a-121">toouse hello 일괄 처리 템플릿 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-121">toouse hello Batch templates, you will need hello following:</span></span>

* <span data-ttu-id="ed23a-122">Visual Studio 2015가 설치된 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="ed23a-122">A computer with Visual Studio 2015 installed.</span></span> <span data-ttu-id="ed23a-123">일괄 처리 템플릿은 현재 Visual Studio 2015에 대해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-123">Batch templates are currently only supported for Visual Studio 2015.</span></span>
* <span data-ttu-id="ed23a-124">hello에서 사용할 수 있는 hello 일괄 처리 템플릿 [Visual Studio 갤러리] [ vs_gallery] Visual Studio 확장으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-124">hello Batch templates, which are available from hello [Visual Studio Gallery][vs_gallery] as Visual Studio extensions.</span></span> <span data-ttu-id="ed23a-125">두 가지가 tooget hello 템플릿:</span><span class="sxs-lookup"><span data-stu-id="ed23a-125">There are two ways tooget hello templates:</span></span>
  
  * <span data-ttu-id="ed23a-126">Hello를 사용 하 여 hello 템플릿을 설치 **확장명 및 업데이트** Visual Studio에서 대화 상자 (자세한 내용은 참조 [찾기 및 사용 하 여 Visual Studio 확장명][vs_find_use_ext]).</span><span class="sxs-lookup"><span data-stu-id="ed23a-126">Install hello templates using hello **Extensions and Updates** dialog box in Visual Studio (for more information, see [Finding and Using Visual Studio Extensions][vs_find_use_ext]).</span></span> <span data-ttu-id="ed23a-127">Hello에 **확장명 및 업데이트** 대화 상자에서 다음 두 가지 확장 검색 및 다운로드 hello:</span><span class="sxs-lookup"><span data-stu-id="ed23a-127">In hello **Extensions and Updates** dialog box, search and download hello following two extensions:</span></span>
    
    * <span data-ttu-id="ed23a-128">Azure 배치 작업 관리자(작업 분할자 포함)</span><span class="sxs-lookup"><span data-stu-id="ed23a-128">Azure Batch Job Manager with Job Splitter</span></span>
    * <span data-ttu-id="ed23a-129">Azure 배치 태스크 프로세서</span><span class="sxs-lookup"><span data-stu-id="ed23a-129">Azure Batch Task Processor</span></span>
  * <span data-ttu-id="ed23a-130">Hello 온라인 갤러리에서 Visual Studio에 대 한 hello 서식 파일을 다운로드: [Microsoft Azure 일괄 처리 프로젝트 템플릿][vs_gallery_templates]</span><span class="sxs-lookup"><span data-stu-id="ed23a-130">Download hello templates from hello online gallery for Visual Studio: [Microsoft Azure Batch Project Templates][vs_gallery_templates]</span></span>
* <span data-ttu-id="ed23a-131">Toouse hello 하려는 경우 [응용 프로그램 패키지](batch-application-packages.md) 기능 toodeploy hello 작업 관리자 태스크 프로세서 toohello 일괄 처리는 계산 노드 toolink 저장소 계정 tooyour 일괄 처리 계정 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-131">If you plan toouse hello [Application Packages](batch-application-packages.md) feature toodeploy hello job manager and task processor toohello Batch compute nodes, you need toolink a storage account tooyour Batch account.</span></span>

## <a name="preparation"></a><span data-ttu-id="ed23a-132">준비</span><span class="sxs-lookup"><span data-stu-id="ed23a-132">Preparation</span></span>
<span data-ttu-id="ed23a-133">작업 관리자와 작업 프로세서 프로그램 간에 더 쉽게 tooshare 코드를 만들 수 있습니다이 때문에 작업 관리자 뿐만 아니라 해당 작업 프로세서를 포함할 수 있는 솔루션을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-133">We recommend creating a solution that can contain your job manager as well as your task processor, because this can make it easier tooshare code between your job manager and task processor programs.</span></span> <span data-ttu-id="ed23a-134">toocreate이이 솔루션에서는 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-134">toocreate this solution, follow these steps:</span></span>

1. <span data-ttu-id="ed23a-135">Visual Studio를 열고 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-135">Open Visual Studio and select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="ed23a-136">**템플릿** 아래에서 **기타 프로젝트 형식**을 확장하고 **Visual Studio 솔루션**을 클릭한 후 **빈 솔루션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-136">Under **Templates**, expand **Other Project Types**, click **Visual Studio Solutions**, and then select **Blank Solution**.</span></span>
3. <span data-ttu-id="ed23a-137">이 솔루션 (예: "LitwareBatchTaskPrograms")의 응용 프로그램 및 hello 용도 설명 하는 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-137">Type a name that describes your application and hello purpose of this solution (e.g., "LitwareBatchTaskPrograms").</span></span>
4. <span data-ttu-id="ed23a-138">toocreate hello 새 솔루션을 클릭 하 여 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-138">toocreate hello new solution, click **OK**.</span></span>

## <a name="job-manager-template"></a><span data-ttu-id="ed23a-139">작업 관리자 템플릿</span><span class="sxs-lookup"><span data-stu-id="ed23a-139">Job Manager template</span></span>
<span data-ttu-id="ed23a-140">hello 작업 관리자 템플릿을 tooimplement hello 다음 작업을 수행할 수 있는 작업 관리자 태스크를 사용 하면:</span><span class="sxs-lookup"><span data-stu-id="ed23a-140">hello Job Manager template helps you tooimplement a job manager task that can perform hello following actions:</span></span>

* <span data-ttu-id="ed23a-141">작업을 여러 태스크로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-141">Split a job into multiple tasks.</span></span>
* <span data-ttu-id="ed23a-142">이러한 작업 toorun 일괄 처리에 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-142">Submit those tasks toorun on Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="ed23a-143">작업 관리자 태스크에 대한 자세한 내용은 [개발자를 위한 배치 기능 개요](batch-api-basics.md#job-manager-task)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed23a-143">For more information about job manager tasks, see [Batch feature overview for developers](batch-api-basics.md#job-manager-task).</span></span>
> 
> 

### <a name="create-a-job-manager-using-hello-template"></a><span data-ttu-id="ed23a-144">Hello 템플릿을 사용 하 여 작업 관리자를 만듭니다</span><span class="sxs-lookup"><span data-stu-id="ed23a-144">Create a Job Manager using hello template</span></span>
<span data-ttu-id="ed23a-145">앞에서 만든 작업 관리자 toohello 솔루션 tooadd 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="ed23a-145">tooadd a job manager toohello solution that you created earlier, follow these steps:</span></span>

1. <span data-ttu-id="ed23a-146">Visual Studio에서 기존 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-146">Open your existing solution in Visual Studio.</span></span>
2. <span data-ttu-id="ed23a-147">솔루션 탐색기, 마우스 오른쪽 단추로 클릭 hello 솔루션에서에서 클릭 **추가** > **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-147">In Solution Explorer, right-click hello solution, click **Add** > **New Project**.</span></span>
3. <span data-ttu-id="ed23a-148">**Visual C#** 아래에서 **클라우드**를 클릭한 후 **Azure 배치 작업 관리자 및 작업 분할자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-148">Under **Visual C#**, click **Cloud**, and then click **Azure Batch Job Manager with Job Splitter**.</span></span>
4. <span data-ttu-id="ed23a-149">응용 프로그램을 설명 하 고 (예: hello 작업 관리자와이 프로젝트를 식별 하는 이름을 입력 합니다. "LitwareJobManager").</span><span class="sxs-lookup"><span data-stu-id="ed23a-149">Type a name that describes your application and identifies this project as hello job manager (e.g. "LitwareJobManager").</span></span>
5. <span data-ttu-id="ed23a-150">toocreate hello 프로젝트 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-150">toocreate hello project, click **OK**.</span></span>
6. <span data-ttu-id="ed23a-151">마지막으로 모든 빌드 hello 프로젝트 tooforce Visual Studio tooload NuGet 패키지를 참조 하 고 수정 하기 시작 하기 전에 프로젝트 hello tooverify 올바른지.</span><span class="sxs-lookup"><span data-stu-id="ed23a-151">Finally, build hello project tooforce Visual Studio tooload all referenced NuGet packages and tooverify that hello project is valid before you start modifying it.</span></span>

### <a name="job-manager-template-files-and-their-purpose"></a><span data-ttu-id="ed23a-152">작업 관리자 템플릿 파일 및 그 용도</span><span class="sxs-lookup"><span data-stu-id="ed23a-152">Job Manager template files and their purpose</span></span>
<span data-ttu-id="ed23a-153">Hello 작업 관리자 템플릿을 사용 하 여 프로젝트를 만들면 코드 파일의 세 그룹 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-153">When you create a project using hello Job Manager template, it generates three groups of code files:</span></span>

* <span data-ttu-id="ed23a-154">hello 주 프로그램 (Program.cs) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-154">hello main program file (Program.cs).</span></span> <span data-ttu-id="ed23a-155">Hello 프로그램 진입점 및 최상위 예외 처리 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-155">This contains hello program entry point and top-level exception handling.</span></span> <span data-ttu-id="ed23a-156">일반적으로 필요는 없습니다 toomodify이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-156">You shouldn't normally need toomodify this.</span></span>
* <span data-ttu-id="ed23a-157">hello 프레임 워크 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-157">hello Framework directory.</span></span> <span data-ttu-id="ed23a-158">이 매개 변수를 추가 작업 toohello 일괄 작업 등의 압축을 푼 hello 작업 관리자 프로그램 –에서 수행 하는 hello '상용구' 작업을 담당 하는 hello 파일을 포함 합니다. 일반적으로 필요는 없습니다 toomodify 이러한 파일.</span><span class="sxs-lookup"><span data-stu-id="ed23a-158">This contains hello files responsible for hello 'boilerplate' work done by hello job manager program – unpacking parameters, adding tasks toohello Batch job, etc. You shouldn't normally need toomodify these files.</span></span>
* <span data-ttu-id="ed23a-159">hello 작업 분할자 파일 (JobSplitter.cs)입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-159">hello job splitter file (JobSplitter.cs).</span></span> <span data-ttu-id="ed23a-160">작업을 태스크로 분할하기 위해 응용 프로그램 관련 논리를 배치할 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-160">This is where you will put your application-specific logic for splitting a job into tasks.</span></span>

<span data-ttu-id="ed23a-161">물론 작업 분할자 코드 논리를 분할 하는 hello 작업의 hello 복잡성에 따라 필요한 toosupport로 추가 파일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-161">Of course you can add additional files as required toosupport your job splitter code, depending on hello complexity of hello job splitting logic.</span></span>

<span data-ttu-id="ed23a-162">또한 hello 템플릿은.csproj 파일, app.config, packages.config 등과 같은 표준.NET 프로젝트 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-162">hello template also generates standard .NET project files such as a .csproj file, app.config, packages.config, etc.</span></span>

<span data-ttu-id="ed23a-163">이 섹션의 나머지 부분 hello hello 다른 파일 및 해당 코드 구조 및 각 클래스의 용도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-163">hello rest of this section describes hello different files and their code structure, and explains what each class does.</span></span>

![Hello 작업 관리자 템플릿 솔루션을 보여 주는 visual Studio 솔루션 탐색기][solution_explorer01]

<span data-ttu-id="ed23a-165">**프레임워크 파일**</span><span class="sxs-lookup"><span data-stu-id="ed23a-165">**Framework files**</span></span>

* <span data-ttu-id="ed23a-166">`Configuration.cs`: Hello 로드 일괄 처리 계정 세부 정보, 연결 된 저장소 계정 자격 증명, 작업 및 작업 정보 및 작업 매개 변수 같은 작업 구성 데이터를 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-166">`Configuration.cs`: Encapsulates hello loading of job configuration data such as Batch account details, linked storage account credentials, job and task information, and job parameters.</span></span> <span data-ttu-id="ed23a-167">액세스 hello Configuration.EnvironmentVariable 클래스를 통해 tooBatch 정의 환경 변수 (hello 일괄 처리 설명서에서 작업에 대 한 환경 설정을 참조)도 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-167">It also provides access tooBatch-defined environment variables (see Environment settings for tasks, in hello Batch documentation) via hello Configuration.EnvironmentVariable class.</span></span>
* <span data-ttu-id="ed23a-168">`IConfiguration.cs`: 요약이 hello hello 구성 클래스의 구현, 단위 테스트 가짜 또는 모의 구성 개체를 사용 하 여 작업 분할자 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-168">`IConfiguration.cs`: Abstracts hello implementation of hello Configuration class, so that you can unit test your job splitter using a fake or mock configuration object.</span></span>
* <span data-ttu-id="ed23a-169">`JobManager.cs`: 작업 관리자 프로그램 hello의 hello 구성 요소를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-169">`JobManager.cs`: Orchestrates hello components of hello job manager program.</span></span> <span data-ttu-id="ed23a-170">Hello 작업 분할자 호출 되는 hello 작업 분할을 초기화 하는 hello을 담당 하 고 hello 작업 분할자 toohello 작업 제출 자가 반환한 hello 작업 디스패치.</span><span class="sxs-lookup"><span data-stu-id="ed23a-170">It is responsible for hello initializing hello job splitter, invoking hello job splitter, and dispatching hello tasks returned by hello job splitter toohello task submitter.</span></span>
* <span data-ttu-id="ed23a-171">`JobManagerException.cs`: 작업 관리자 tooterminate hello를 필요로 하는 오류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-171">`JobManagerException.cs`: Represents an error that requires hello job manager tooterminate.</span></span> <span data-ttu-id="ed23a-172">JobManagerException 종료의 일부로 관련 진단 정보가 수 제공 하는 경우 사용 되는 toowrap '예상 된' 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-172">JobManagerException is used toowrap 'expected' errors where specific diagnostic information can be provided as part of termination.</span></span>
* <span data-ttu-id="ed23a-173">`TaskSubmitter.cs`:이 클래스는 hello 작업 분할자 toohello 일괄 작업에서 반환 하는 책임 tooadding 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-173">`TaskSubmitter.cs`: This class is responsible tooadding tasks returned by hello job splitter toohello Batch job.</span></span> <span data-ttu-id="ed23a-174">hello JobManager 클래스 hello 일련의 작업을 시기 적절 하지만 효율적인 추가 toohello 작업에 대 한 일괄 처리로 집계 한 다음 각 일괄 처리에 대 한 백그라운드 스레드에서 TaskSubmitter.SubmitTasks를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-174">hello JobManager class aggregates hello sequence of tasks into batches for efficient but timely addition toohello job, then calls TaskSubmitter.SubmitTasks on a background thread for each batch.</span></span>

<span data-ttu-id="ed23a-175">**작업 분할자**</span><span class="sxs-lookup"><span data-stu-id="ed23a-175">**Job Splitter**</span></span>

<span data-ttu-id="ed23a-176">`JobSplitter.cs`:이 클래스는 작업으로 hello 작업 분할에 대 한 응용 프로그램별 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-176">`JobSplitter.cs`: This class contains application-specific logic for splitting hello job into tasks.</span></span> <span data-ttu-id="ed23a-177">hello 프레임 워크 호출 시퀀스를 추가 하 여 작업을 hello JobSplitter.Split 메서드 tooobtain hello 메서드로 toohello 작업을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-177">hello framework invokes hello JobSplitter.Split method tooobtain a sequence of tasks, which it adds toohello job as hello method returns them.</span></span> <span data-ttu-id="ed23a-178">이 클래스는 hello 클래스 작업의 hello 논리를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-178">This is hello class where you will inject hello logic of your job.</span></span> <span data-ttu-id="ed23a-179">Hello 분할 메서드 tooreturn toopartition hello 작업 하려는 hello 작업을 나타내는 CloudTask 인스턴스의 시퀀스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-179">Implement hello Split method tooreturn a sequence of CloudTask instances representing hello tasks into which you want toopartition hello job.</span></span>

<span data-ttu-id="ed23a-180">**표준 .NET 명령줄 프로젝트 파일**</span><span class="sxs-lookup"><span data-stu-id="ed23a-180">**Standard .NET command line project files**</span></span>

* <span data-ttu-id="ed23a-181">`App.config`: 표준 .NET 응용 프로그램 구성 파일</span><span class="sxs-lookup"><span data-stu-id="ed23a-181">`App.config`: Standard .NET application configuration file.</span></span>
* <span data-ttu-id="ed23a-182">`Packages.config`: 표준 NuGet 패키지 종속성 파일</span><span class="sxs-lookup"><span data-stu-id="ed23a-182">`Packages.config`: Standard NuGet package dependency file.</span></span>
* <span data-ttu-id="ed23a-183">`Program.cs`: Hello 프로그램 진입점 및 최상위 예외 처리 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-183">`Program.cs`: Contains hello program entry point and top-level exception handling.</span></span>

### <a name="implementing-hello-job-splitter"></a><span data-ttu-id="ed23a-184">Hello 작업 분할을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-184">Implementing hello job splitter</span></span>
<span data-ttu-id="ed23a-185">Hello 작업 관리자 템플릿 프로젝트를 열면 hello 프로젝트 hello JobSplitter.cs 파일 기본적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-185">When you open hello Job Manager template project, hello project will have hello JobSplitter.cs file open by default.</span></span> <span data-ttu-id="ed23a-186">Hello hello split () 메서드 아래에 표시를 사용 하 여 분할 작업에 대 한 hello 작업에 대 한 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-186">You can implement hello split logic for hello tasks in your workload by using hello Split() method show below:</span></span>

```csharp
/// <summary>
/// Gets hello tasks into which toosplit hello job. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello job manager framework invokes hello Split method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation should return tasks lazily, for example using a C#
/// iterator and hello "yield return" statement; this allows tasks toobe added
/// and toostart running while splitting is still in progress.
/// </summary>
/// <returns>hello tasks toobe added toohello job. Tasks are added automatically
/// by hello job manager framework as they are returned by this method.</returns>
public IEnumerable<CloudTask> Split()
{
    // Your code for hello split logic goes here.
    int startFrame = Convert.ToInt32(_parameters["StartFrame"]);
    int endFrame = Convert.ToInt32(_parameters["EndFrame"]);

    for (int i = startFrame; i <= endFrame; i++)
    {
        yield return new CloudTask("myTask" + i, "cmd /c dir");
    }
}
```

> [!NOTE]
> <span data-ttu-id="ed23a-187">hello hello에 대 한 섹션을 주석 처리 `Split()` 메서드는 hello만 섹션 hello toomodify 하는 다른 작업으로 hello 논리 toosplit 작업을 추가 하 여 대상으로 하는 작업 관리자 템플릿 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-187">hello annotated section in hello `Split()` method is hello only section of hello Job Manager template code that is intended for you toomodify by adding hello logic toosplit your jobs into different tasks.</span></span> <span data-ttu-id="ed23a-188">Toomodify hello 서식 파일의 다른 섹션을 원하는 경우의 일괄 처리의 작동 방식으로 개체는 확인 하세요 hello 중 몇 가지 사용을 및 [코드 샘플을 일괄 처리][github_samples]합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-188">If you want toomodify a different section of hello template, please ensure you are familiarized with how Batch works, and try out a few of hello [Batch code samples][github_samples].</span></span>
> 
> 

<span data-ttu-id="ed23a-189">Split() 구현에서는 다음에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-189">Your Split() implementation has access to:</span></span>

* <span data-ttu-id="ed23a-190">hello 통해 작업 매개 변수를 hello `_parameters` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-190">hello job parameters, via hello `_parameters` field.</span></span>
* <span data-ttu-id="ed23a-191">hello CloudJob 개체 hello 통해 나타내는 hello 작업 `_job` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-191">hello CloudJob object representing hello job, via hello `_job` field.</span></span>
* <span data-ttu-id="ed23a-192">hello CloudTask 개체 hello 통해 나타내는 hello 작업 관리자 태스크가 `_jobManagerTask` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-192">hello CloudTask object representing hello job manager task, via hello `_jobManagerTask` field.</span></span>

<span data-ttu-id="ed23a-193">프로그램 `Split()` 구현 tooadd 작업 toohello 작업을 직접 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-193">Your `Split()` implementation does not need tooadd tasks toohello job directly.</span></span> <span data-ttu-id="ed23a-194">대신 코드 CloudTask 개체의 시퀀스를 반환 해야 하 고 이러한 추가할 toohello 작업이 자동으로 hello 작업 분할자를 호출 하는 hello 프레임 워크 클래스.</span><span class="sxs-lookup"><span data-stu-id="ed23a-194">Instead, your code should return a sequence of CloudTask objects, and these will be added toohello job automatically by hello framework classes that invoke hello job splitter.</span></span> <span data-ttu-id="ed23a-195">일반적인 C#의 toouse 반복기는 (`yield return`)으로 계산 된 모든 작업 toobe 대기 하는 것이 아니라이 통해 실행 가능한 한 빨리 hello 작업 toostart tooimplement 작업 분할자 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-195">It's common toouse C#'s iterator (`yield return`) feature tooimplement job splitters as this allows hello tasks toostart running as soon as possible rather than waiting for all tasks toobe calculated.</span></span>

<span data-ttu-id="ed23a-196">**작업 분할자 실패**</span><span class="sxs-lookup"><span data-stu-id="ed23a-196">**Job splitter failure**</span></span>

<span data-ttu-id="ed23a-197">작업 분할자에 오류가 발생하는 경우 다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-197">If your job splitter encounters an error, it should either:</span></span>

* <span data-ttu-id="ed23a-198">C# hello를 사용 하 여 hello 시퀀스 종료 `yield break` 는 case hello 작업 관리자 간주 되며 성공으로; 문 또는</span><span class="sxs-lookup"><span data-stu-id="ed23a-198">Terminate hello sequence using hello C# `yield break` statement, in which case hello job manager will be treated as successful; or</span></span>
* <span data-ttu-id="ed23a-199">case hello 작업 관리자 실패 한 것으로 처리 되 고 hello 클라이언트 구성에 방식에 따라 다시 시도할 수 예외가 throw).</span><span class="sxs-lookup"><span data-stu-id="ed23a-199">Throw an exception, in which case hello job manager will be treated as failed and may be retried depending on how hello client has configured it).</span></span>

<span data-ttu-id="ed23a-200">두 경우 모두 모든 작업은 이미 hello 작업 분할에서 반환 하 고 추가 된 toohello 일괄 작업에는 적격 toorun 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-200">In both cases, any tasks already returned by hello job splitter and added toohello Batch job will be eligible toorun.</span></span> <span data-ttu-id="ed23a-201">이 toohappen 사용 하지 않으려는 경우 다음 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-201">If you don't want this toohappen, then you could:</span></span>

* <span data-ttu-id="ed23a-202">Hello 작업 분할에서 반환 하기 전에 hello 작업 종료</span><span class="sxs-lookup"><span data-stu-id="ed23a-202">Terminate hello job before returning from hello job splitter</span></span>
* <span data-ttu-id="ed23a-203">반환 하기 전에 전체 작업 컬렉션 hello 공식화 (즉, 반환 된 `ICollection<CloudTask>` 또는 `IList<CloudTask>` C# 반복기를 사용 하 여 작업 분할을 구현 하는 대신)</span><span class="sxs-lookup"><span data-stu-id="ed23a-203">Formulate hello entire task collection before returning it (that is, return an `ICollection<CloudTask>` or `IList<CloudTask>` instead of implementing your job splitter using a C# iterator)</span></span>
* <span data-ttu-id="ed23a-204">작업 종속성 toomake hello 작업 관리자의 hello 성공적으로 완료에 종속 된 모든 작업을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="ed23a-204">Use task dependencies toomake all tasks depend on hello successful completion of hello job manager</span></span>

<span data-ttu-id="ed23a-205">**작업 관리자 재시도**</span><span class="sxs-lookup"><span data-stu-id="ed23a-205">**Job manager retries**</span></span>

<span data-ttu-id="ed23a-206">Hello 작업 관리자가 실패 하는 경우 hello 클라이언트 다시 시도 설정에 따라 hello 일괄 처리 서비스에서 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-206">If hello job manager fails, it may be retried by hello Batch service depending on hello client retry settings.</span></span> <span data-ttu-id="ed23a-207">일반적으로이 보안상 hello 프레임 워크 추가 작업 toohello 작업을 하는 경우 이미 존재 하는 모든 작업에서 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-207">In general, this is safe, because when hello framework adds tasks toohello job, it ignores any tasks that already exist.</span></span> <span data-ttu-id="ed23a-208">그러나 작업 계산 비용이 많이 드는 경우 하지 않을 toohello 작업, 이미 추가 된 작업을 다시 계산의 tooincur hello 비용 반대로, hello를 다시 실행 하는 경우는 보장된 되지 않음 toogenerate hello 동일한 작업 Id 다음 hello '중복을 무시 합니다.' 동작 작업을 시작 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-208">However, if calculating tasks is expensive, you may not wish tooincur hello cost of recalculating tasks that have already been added toohello job; conversely, if hello re-run is not guaranteed toogenerate hello same task IDs then hello 'ignore duplicates' behavior will not kick in.</span></span> <span data-ttu-id="ed23a-209">이러한 경우 작업 분할 toodetect hello는 작업에 이미 수행 되었습니다 및 반복 되지 것, 예를 들어 한 CloudJob.ListTasks tooyield 작업을 시작 하기 전에 수행 하 여 디자인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-209">In these cases you should design your job splitter toodetect hello work that has already been done and not repeat it, for example by performing a CloudJob.ListTasks before starting tooyield tasks.</span></span>

### <a name="exit-codes-and-exceptions-in-hello-job-manager-template"></a><span data-ttu-id="ed23a-210">종료 코드와 hello 작업 관리자 서식 파일의 예외</span><span class="sxs-lookup"><span data-stu-id="ed23a-210">Exit codes and exceptions in hello Job Manager template</span></span>
<span data-ttu-id="ed23a-211">종료 코드와 예외는 프로그램을 실행 하는의 메커니즘 toodetermine hello 결과 제공 하 고 tooidentify 문제 hello hello 프로그램 실행에 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-211">Exit codes and exceptions provide a mechanism toodetermine hello outcome of running a program, and they can help tooidentify any problems with hello execution of hello program.</span></span> <span data-ttu-id="ed23a-212">작업 관리자 템플릿 hello hello 종료 코드 및이 섹션에 설명 된 예외를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-212">hello Job Manager template implements hello exit codes and exceptions described in this section.</span></span>

<span data-ttu-id="ed23a-213">Hello 작업 관리자 템플릿을 사용 하 여 구현 되는 작업 관리자 태스크는 세 가지 가능한 종료 코드를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-213">A job manager task that is implemented with hello Job Manager template can return three possible exit codes:</span></span>

| <span data-ttu-id="ed23a-214">코드</span><span class="sxs-lookup"><span data-stu-id="ed23a-214">Code</span></span> | <span data-ttu-id="ed23a-215">설명</span><span class="sxs-lookup"><span data-stu-id="ed23a-215">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ed23a-216">0</span><span class="sxs-lookup"><span data-stu-id="ed23a-216">0</span></span> |<span data-ttu-id="ed23a-217">hello 작업 관리자가 성공적으로 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-217">hello job manager completed successfully.</span></span> <span data-ttu-id="ed23a-218">작업 분할 코드 toocompletion, 실행 되 고 모든 작업 toohello 작업이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-218">Your job splitter code ran toocompletion, and all tasks were added toohello job.</span></span> |
| <span data-ttu-id="ed23a-219">1</span><span class="sxs-lookup"><span data-stu-id="ed23a-219">1</span></span> |<span data-ttu-id="ed23a-220">'예상된' hello 프로그램 부분에 예외와 함께 hello 작업 관리자 태스크가 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-220">hello job manager task failed with an exception in an 'expected' part of hello program.</span></span> <span data-ttu-id="ed23a-221">hello 예외는 번역 된 tooa JobManagerException와 진단 정보 및 해결에 대 한 제안을 오류 hello 가능한 경우.</span><span class="sxs-lookup"><span data-stu-id="ed23a-221">hello exception was translated tooa JobManagerException with diagnostic information and, where possible, suggestions for resolving hello failure.</span></span> |
| <span data-ttu-id="ed23a-222">2</span><span class="sxs-lookup"><span data-stu-id="ed23a-222">2</span></span> |<span data-ttu-id="ed23a-223">작업 관리자 태스크가 hello '예기치 않은' 예외로 인해 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-223">hello job manager task failed with an 'unexpected' exception.</span></span> <span data-ttu-id="ed23a-224">hello 예외는 출력 기록된 toostandard 했지만 hello 작업 관리자 수 없습니다 tooadd 추가 진단 또는 업데이트 관리 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-224">hello exception was logged toostandard output, but hello job manager was unable tooadd any additional diagnostic or remediation information.</span></span> |

<span data-ttu-id="ed23a-225">Hello 작업 관리자 작업 실패의 경우에서 일부 작업 여전히 추가 된 toohello 서비스 전에 hello 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-225">In hello case of job manager task failure, some tasks may still have been added toohello service before hello error occurred.</span></span> <span data-ttu-id="ed23a-226">이러한 태스크는 정상적으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-226">These tasks will run as normal.</span></span> <span data-ttu-id="ed23a-227">이 코드 경로에 대한 설명은 위의 "작업 분할자 오류"를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed23a-227">See "Job Splitter Failure" above for discussion of this code path.</span></span>

<span data-ttu-id="ed23a-228">예외에서 반환 하는 모든 hello 정보 stderr.txt 및 stdout.txt 파일에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-228">All hello information returned by exceptions is written into stdout.txt and stderr.txt files.</span></span> <span data-ttu-id="ed23a-229">자세한 내용은 [오류 처리](batch-api-basics.md#error-handling)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed23a-229">For more information, see [Error Handling](batch-api-basics.md#error-handling).</span></span>

### <a name="client-considerations"></a><span data-ttu-id="ed23a-230">클라이언트 고려 사항</span><span class="sxs-lookup"><span data-stu-id="ed23a-230">Client considerations</span></span>
<span data-ttu-id="ed23a-231">이 섹션에서는 이 템플릿을 기반으로 작업 관리자를 호출할 때 일부 클라이언트 구현 요구 사항에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-231">This section describes some client implementation requirements when invoking a job manager based on this template.</span></span> <span data-ttu-id="ed23a-232">참조 [toopass 매개 변수 및 환경 변수를 hello 클라이언트 코드에 어떻게](#pass-environment-settings) 전달 매개 변수 및 환경 설정에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-232">See [How toopass parameters and environment variables from hello client code](#pass-environment-settings) for details on passing parameters and environment settings.</span></span>

<span data-ttu-id="ed23a-233">**필수 자격 증명**</span><span class="sxs-lookup"><span data-stu-id="ed23a-233">**Mandatory credentials**</span></span>

<span data-ttu-id="ed23a-234">순서 tooadd 작업 toohello Azure 일괄 처리 작업에서 작업 관리자 태스크가 hello Azure 배치 계정 URL과 키 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-234">In order tooadd tasks toohello Azure Batch job, hello job manager task requires your Azure Batch account URL and key.</span></span> <span data-ttu-id="ed23a-235">YOUR_BATCH_URL 및 YOUR_BATCH_KEY라는 환경 변수에 이를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-235">You must pass these in environment variables named YOUR_BATCH_URL and YOUR_BATCH_KEY.</span></span> <span data-ttu-id="ed23a-236">Hello 작업 관리자에서에서 이러한 작업 환경 설정을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-236">You can set these in hello Job Manager task environment settings.</span></span> <span data-ttu-id="ed23a-237">예를 들어 C# 클라이언트에서 다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-237">For example, in a C# client:</span></span>

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    new EnvironmentSetting("YOUR_BATCH_URL", "https://account.region.batch.azure.com"),
    new EnvironmentSetting("YOUR_BATCH_KEY", "{your_base64_encoded_account_key}"),
};
```
<span data-ttu-id="ed23a-238">**Storage 자격 증명**</span><span class="sxs-lookup"><span data-stu-id="ed23a-238">**Storage credentials**</span></span>

<span data-ttu-id="ed23a-239">일반적으로 hello 클라이언트 필요가 없는 tooprovide hello 연결 된 저장소 계정 자격 증명 toohello 작업 관리자 태스크는 (a) 대부분의 작업 관리자 tooexplicitly 액세스 hello 연결 된 저장소 계정이 필요 하지 않습니다 (b) hello 연결 된 저장소 계정을 제공 하기 때문에 hello 작업에 대 한 일반적인 환경 설정으로 tooall 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-239">Typically, hello client does not need tooprovide hello linked storage account credentials toohello job manager task because (a) most job managers do not need tooexplicitly access hello linked storage account and (b) hello linked storage account is often provided tooall tasks as a common environment setting for hello job.</span></span> <span data-ttu-id="ed23a-240">제공 하지 않으면 hello 연결 된 공통 환경 설정 hello 통해 저장소 계정 및 hello 작업 관리자 액세스 toolinked 저장소 필요 후 다음과 같이 hello 연결 된 저장소 자격 증명을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-240">If you are not providing hello linked storage account via hello common environment settings, and hello job manager requires access toolinked storage, then you should supply hello linked storage credentials as follows:</span></span>

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    /* other environment settings */
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

<span data-ttu-id="ed23a-241">**작업 관리자 태스크 설정**</span><span class="sxs-lookup"><span data-stu-id="ed23a-241">**Job manager task settings**</span></span>

<span data-ttu-id="ed23a-242">hello 클라이언트 hello 작업 관리자를 설정 해야 *killJobOnCompletion* 너무 플래그**false**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-242">hello client should set hello job manager *killJobOnCompletion* flag too**false**.</span></span>

<span data-ttu-id="ed23a-243">일반적으로 클라이언트 tooset hello에 대 한 *runExclusive* 너무**false**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-243">It is usually safe for hello client tooset *runExclusive* too**false**.</span></span>

<span data-ttu-id="ed23a-244">hello 클라이언트는 hello를 사용 하 여 *resourceFiles* 또는 *applicationPackageReferences* toohello 계산 노드를 배포한 컬렉션 toohave hello 작업 관리자 실행 (및 필요한 Dll)입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-244">hello client should use hello *resourceFiles* or *applicationPackageReferences* collection toohave hello job manager executable (and its required DLLs) deployed toohello compute node.</span></span>

<span data-ttu-id="ed23a-245">기본적으로 hello 작업 관리자 재시도 되지 않습니다 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-245">By default, hello job manager will not be retried if it fails.</span></span> <span data-ttu-id="ed23a-246">사용자 작업 관리자 논리에 따라 hello 클라이언트를 통해 tooenable 다시 시도 하는 경우가 *제약 조건을*/*maxTaskRetryCount*합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-246">Depending on your job manager logic, hello client may want tooenable retries via *constraints*/*maxTaskRetryCount*.</span></span>

<span data-ttu-id="ed23a-247">**작업 설정**</span><span class="sxs-lookup"><span data-stu-id="ed23a-247">**Job settings**</span></span>

<span data-ttu-id="ed23a-248">Hello 작업 분할 작업 종속성을 가진 이면 hello 클라이언트 hello 작업 usesTaskDependencies tootrue를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-248">If hello job splitter emits tasks with dependencies, hello client must set hello job's usesTaskDependencies tootrue.</span></span>

<span data-ttu-id="ed23a-249">Hello 작업 분할 모델에서는 어떤 hello 작업 분할자 만듭니다 외 toowish tooadd 작업 toojobs 클라이언트에 대 한 거의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-249">In hello job splitter model, it is unusual for clients toowish tooadd tasks toojobs over and above what hello job splitter creates.</span></span> <span data-ttu-id="ed23a-250">따라서 hello 클라이언트 hello 작업이 정상적으로 설정 해야 *onAllTasksComplete* 너무**terminatejob**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-250">hello client should therefore normally set hello job's *onAllTasksComplete* too**terminatejob**.</span></span>

## <a name="task-processor-template"></a><span data-ttu-id="ed23a-251">태스크 프로세서 템플릿</span><span class="sxs-lookup"><span data-stu-id="ed23a-251">Task Processor template</span></span>
<span data-ttu-id="ed23a-252">작업 프로세서 템플릿 tooimplement hello 다음 작업을 수행할 수 있는 작업 프로세서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-252">A Task Processor template helps you tooimplement a task processor that can perform hello following actions:</span></span>

* <span data-ttu-id="ed23a-253">각 일괄 처리 작업 toorun에서 필요한 hello 정보를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-253">Set up hello information required by each Batch task toorun.</span></span>
* <span data-ttu-id="ed23a-254">각 배치 태스크에 필요한 모든 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-254">Run all actions required by each Batch task.</span></span>
* <span data-ttu-id="ed23a-255">Toopersistent 저장소 작업 출력을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-255">Save task outputs toopersistent storage.</span></span>

<span data-ttu-id="ed23a-256">작업 프로세서 일괄 처리에 필요한 toorun 작업 하지는 않지만 제공 하는 래퍼 tooimplement 한 위치에서 작업 실행 작업을 모두를 hello 작업 프로세서 사용의 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-256">Although a task processor is not required toorun tasks on Batch, hello key advantage of using a task processor is that it provides a wrapper tooimplement all task execution actions in one location.</span></span> <span data-ttu-id="ed23a-257">예를 들어 각 작업의 hello 컨텍스트에 여러 응용 프로그램 toorun 필요한 경우 또는 필요한 경우 toocopy 데이터 toopersistent 저장소 완료 한 후 각각의 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-257">For example, if you need toorun several applications in hello context of each task, or if you need toocopy data toopersistent storage after completing each task.</span></span>

<span data-ttu-id="ed23a-258">hello 작업 프로세서에 의해 실행 hello 작업은 단순 또는 복합 및 많은 또는 워크 로드에 필요한 최소한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-258">hello actions performed by hello task processor can be as simple or complex, and as many or as few, as required by your workload.</span></span> <span data-ttu-id="ed23a-259">또한 작업 프로세서가 두 개에 모든 작업 동작을 구현 하 여 손쉽게 업데이트 하거나 추가할 수 있습니다 변경 tooapplications 또는 작업 부하 요구 사항에 따라 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-259">Additionally, by implementing all task actions into one task processor, you can readily update or add actions based on changes tooapplications or workload requirements.</span></span> <span data-ttu-id="ed23a-260">그러나 경우에 따라 임무 프로세서 아닐 수 있습니다 hello 최적의 솔루션 구현에 대 한 예를 들어 경우 간단한 명령줄에서 신속 하 게 시작할 수 있는 작업을 실행 하는 불필요 한 복잡성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-260">However, in some cases a task processor might not be hello optimal solution for your implementation as it can add unnecessary complexity, for example when running jobs that can be quickly started from a simple command line.</span></span>

### <a name="create-a-task-processor-using-hello-template"></a><span data-ttu-id="ed23a-261">Hello 템플릿을 사용 하 여 작업 프로세서 만들기</span><span class="sxs-lookup"><span data-stu-id="ed23a-261">Create a Task Processor using hello template</span></span>
<span data-ttu-id="ed23a-262">앞에서 만든 작업 프로세서 toohello 솔루션 tooadd 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="ed23a-262">tooadd a task processor toohello solution that you created earlier, follow these steps:</span></span>

1. <span data-ttu-id="ed23a-263">Visual Studio에서 기존 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-263">Open your existing solution in Visual Studio.</span></span>
2. <span data-ttu-id="ed23a-264">솔루션 탐색기, 마우스 오른쪽 단추로 클릭 hello 솔루션에서에서 클릭 **추가**, 클릭 하 고 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-264">In Solution Explorer, right-click hello solution, click **Add**, and then click **New Project**.</span></span>
3. <span data-ttu-id="ed23a-265">**Visual C#** 아래에서 **클라우드**를 클릭한 후 **Azure 배치 태스크 프로세서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-265">Under **Visual C#**, click **Cloud**, and then click **Azure Batch Task Processor**.</span></span>
4. <span data-ttu-id="ed23a-266">응용 프로그램을 설명 하 고 작업 프로세서 (예: hello으로이 프로젝트를 식별 하는 이름을 입력 합니다. "LitwareTaskProcessor").</span><span class="sxs-lookup"><span data-stu-id="ed23a-266">Type a name that describes your application and identifies this project as hello task processor (e.g. "LitwareTaskProcessor").</span></span>
5. <span data-ttu-id="ed23a-267">toocreate hello 프로젝트 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-267">toocreate hello project, click **OK**.</span></span>
6. <span data-ttu-id="ed23a-268">마지막으로 모든 빌드 hello 프로젝트 tooforce Visual Studio tooload NuGet 패키지를 참조 하 고 수정 하기 시작 하기 전에 프로젝트 hello tooverify 올바른지.</span><span class="sxs-lookup"><span data-stu-id="ed23a-268">Finally, build hello project tooforce Visual Studio tooload all referenced NuGet packages and tooverify that hello project is valid before you start modifying it.</span></span>

### <a name="task-processor-template-files-and-their-purpose"></a><span data-ttu-id="ed23a-269">태스크 프로세서 템플릿 파일 및 그 용도</span><span class="sxs-lookup"><span data-stu-id="ed23a-269">Task Processor template files and their purpose</span></span>
<span data-ttu-id="ed23a-270">Hello 작업 프로세서 템플릿을 사용 하 여 프로젝트를 만들면 코드 파일의 세 그룹 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-270">When you create a project using hello task processor template, it generates three groups of code files:</span></span>

* <span data-ttu-id="ed23a-271">hello 주 프로그램 (Program.cs) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-271">hello main program file (Program.cs).</span></span> <span data-ttu-id="ed23a-272">Hello 프로그램 진입점 및 최상위 예외 처리 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-272">This contains hello program entry point and top-level exception handling.</span></span> <span data-ttu-id="ed23a-273">일반적으로 필요는 없습니다 toomodify이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-273">You shouldn't normally need toomodify this.</span></span>
* <span data-ttu-id="ed23a-274">hello 프레임 워크 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-274">hello Framework directory.</span></span> <span data-ttu-id="ed23a-275">이 매개 변수를 추가 작업 toohello 일괄 작업 등의 압축을 푼 hello 작업 관리자 프로그램 –에서 수행 하는 hello '상용구' 작업을 담당 하는 hello 파일을 포함 합니다. 일반적으로 필요는 없습니다 toomodify 이러한 파일.</span><span class="sxs-lookup"><span data-stu-id="ed23a-275">This contains hello files responsible for hello 'boilerplate' work done by hello job manager program – unpacking parameters, adding tasks toohello Batch job, etc. You shouldn't normally need toomodify these files.</span></span>
* <span data-ttu-id="ed23a-276">hello 작업 프로세서 파일 (TaskProcessor.cs)입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-276">hello task processor file (TaskProcessor.cs).</span></span> <span data-ttu-id="ed23a-277">(일반적으로 호출 하 여 기존 실행 파일 tooan out) 작업을 실행 하기 위한 응용 프로그램별 논리를 입력할입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-277">This is where you will put your application-specific logic for executing a task (typically by calling out tooan existing executable).</span></span> <span data-ttu-id="ed23a-278">전처리 및 후처리 코드(예: 추가 데이터 다운로드 또는 결과 파일 업로드 등)도 여기에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-278">Pre- and post-processing code, such as downloading additional data or uploading result files, also goes here.</span></span>

<span data-ttu-id="ed23a-279">물론 작업 프로세서 코드 논리를 분할 하는 hello 작업의 hello 복잡성에 따라 필요한 toosupport로 추가 파일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-279">Of course you can add additional files as required toosupport your task processor code, depending on hello complexity of hello job splitting logic.</span></span>

<span data-ttu-id="ed23a-280">또한 hello 템플릿은.csproj 파일, app.config, packages.config 등과 같은 표준.NET 프로젝트 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-280">hello template also generates standard .NET project files such as a .csproj file, app.config, packages.config, etc.</span></span>

<span data-ttu-id="ed23a-281">이 섹션의 나머지 부분 hello hello 다른 파일 및 해당 코드 구조 및 각 클래스의 용도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-281">hello rest of this section describes hello different files and their code structure, and explains what each class does.</span></span>

![Hello 프로세서 작업 서식 파일 솔루션을 보여 주는 visual Studio 솔루션 탐색기][solution_explorer02]

<span data-ttu-id="ed23a-283">**프레임워크 파일**</span><span class="sxs-lookup"><span data-stu-id="ed23a-283">**Framework files**</span></span>

* <span data-ttu-id="ed23a-284">`Configuration.cs`: Hello 로드 일괄 처리 계정 세부 정보, 연결 된 저장소 계정 자격 증명, 작업 및 작업 정보 및 작업 매개 변수 같은 작업 구성 데이터를 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-284">`Configuration.cs`: Encapsulates hello loading of job configuration data such as Batch account details, linked storage account credentials, job and task information, and job parameters.</span></span> <span data-ttu-id="ed23a-285">액세스 hello Configuration.EnvironmentVariable 클래스를 통해 tooBatch 정의 환경 변수 (hello 일괄 처리 설명서에서 작업에 대 한 환경 설정을 참조)도 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-285">It also provides access tooBatch-defined environment variables (see Environment settings for tasks, in hello Batch documentation) via hello Configuration.EnvironmentVariable class.</span></span>
* <span data-ttu-id="ed23a-286">`IConfiguration.cs`: 요약이 hello hello 구성 클래스의 구현, 단위 테스트 가짜 또는 모의 구성 개체를 사용 하 여 작업 분할자 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-286">`IConfiguration.cs`: Abstracts hello implementation of hello Configuration class, so that you can unit test your job splitter using a fake or mock configuration object.</span></span>
* <span data-ttu-id="ed23a-287">`TaskProcessorException.cs`: 작업 관리자 tooterminate hello를 필요로 하는 오류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-287">`TaskProcessorException.cs`: Represents an error that requires hello job manager tooterminate.</span></span> <span data-ttu-id="ed23a-288">TaskProcessorException 종료의 일부로 관련 진단 정보가 수 제공 하는 경우 사용 되는 toowrap '예상 된' 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-288">TaskProcessorException is used toowrap 'expected' errors where specific diagnostic information can be provided as part of termination.</span></span>

<span data-ttu-id="ed23a-289">**태스크 프로세서**</span><span class="sxs-lookup"><span data-stu-id="ed23a-289">**Task Processor**</span></span>

* <span data-ttu-id="ed23a-290">`TaskProcessor.cs`: Hello 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-290">`TaskProcessor.cs`: Runs hello task.</span></span> <span data-ttu-id="ed23a-291">hello 프레임 워크 hello TaskProcessor.Run 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-291">hello framework invokes hello TaskProcessor.Run method.</span></span> <span data-ttu-id="ed23a-292">이 클래스는 hello 클래스 해당 작업의 hello 응용 프로그램별 논리를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-292">This is hello class where you will inject hello application-specific logic of your task.</span></span> <span data-ttu-id="ed23a-293">Hello 실행 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-293">Implement hello Run method to:</span></span>
  * <span data-ttu-id="ed23a-294">태스크 매개 변수 구문 분석 및 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="ed23a-294">Parse and validate any task parameters</span></span>
  * <span data-ttu-id="ed23a-295">Hello 명령줄 작성 tooinvoke 하려는 모든 외부 프로그램에 대 한</span><span class="sxs-lookup"><span data-stu-id="ed23a-295">Compose hello command line for any external program you want tooinvoke</span></span>
  * <span data-ttu-id="ed23a-296">디버깅 용도로 필요할 수 있는 모든 진단 정보 기록</span><span class="sxs-lookup"><span data-stu-id="ed23a-296">Log any diagnostic information you may require for debugging purposes</span></span>
  * <span data-ttu-id="ed23a-297">해당 명령줄을 사용하는 프로세스 시작</span><span class="sxs-lookup"><span data-stu-id="ed23a-297">Start a process using that command line</span></span>
  * <span data-ttu-id="ed23a-298">Hello 프로세스 tooexit 때까지 대기</span><span class="sxs-lookup"><span data-stu-id="ed23a-298">Wait for hello process tooexit</span></span>
  * <span data-ttu-id="ed23a-299">성공 또는 실패 하는 경우 hello 프로세스 toodetermine hello 종료 코드를 캡처</span><span class="sxs-lookup"><span data-stu-id="ed23a-299">Capture hello exit code of hello process toodetermine if it succeeded or failed</span></span>
  * <span data-ttu-id="ed23a-300">출력 파일에 저장 tookeep toopersistent 공간 절약</span><span class="sxs-lookup"><span data-stu-id="ed23a-300">Save any output files you want tookeep toopersistent storage</span></span>

<span data-ttu-id="ed23a-301">**표준 .NET 명령줄 프로젝트 파일**</span><span class="sxs-lookup"><span data-stu-id="ed23a-301">**Standard .NET command line project files**</span></span>

* <span data-ttu-id="ed23a-302">`App.config`: 표준 .NET 응용 프로그램 구성 파일</span><span class="sxs-lookup"><span data-stu-id="ed23a-302">`App.config`: Standard .NET application configuration file.</span></span>
* <span data-ttu-id="ed23a-303">`Packages.config`: 표준 NuGet 패키지 종속성 파일</span><span class="sxs-lookup"><span data-stu-id="ed23a-303">`Packages.config`: Standard NuGet package dependency file.</span></span>
* <span data-ttu-id="ed23a-304">`Program.cs`: Hello 프로그램 진입점 및 최상위 예외 처리 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-304">`Program.cs`: Contains hello program entry point and top-level exception handling.</span></span>

## <a name="implementing-hello-task-processor"></a><span data-ttu-id="ed23a-305">Hello 작업 프로세서 구현</span><span class="sxs-lookup"><span data-stu-id="ed23a-305">Implementing hello task processor</span></span>
<span data-ttu-id="ed23a-306">Hello 프로세서 작업 서식 파일 프로젝트를 열면 hello 프로젝트 hello TaskProcessor.cs 파일 기본적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-306">When you open hello Task Processor template project, hello project will have hello TaskProcessor.cs file open by default.</span></span> <span data-ttu-id="ed23a-307">아래에 표시 된 hello run () 메서드를 사용 하 여 작업에서 hello 작업에 대 한 hello 실행 논리를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-307">You can implement hello run logic for hello tasks in your workload by using hello Run() method shown below:</span></span>

```csharp
/// <summary>
/// Runs hello task processing logic. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello task processor framework invokes hello Run method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation will execute an external program (from resource files or
/// an application package), check hello exit code of that program and
/// save output files toopersistent storage.
/// </summary>
public async Task<int> Run()

{
    try
    {
        //Your code for hello task processor goes here.
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
> <span data-ttu-id="ed23a-308">hello run () 메서드 hello에 주석이 추가 된 섹션은 hello만 섹션 toomodify 하는 작업에서 hello 작업에 대 한 hello 실행 논리를 추가 하 여 대상으로 하는 hello 프로세서 작업 템플릿 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-308">hello annotated section in hello Run() method is hello only section of hello Task Processor template code that is intended for you toomodify by adding hello run logic for hello tasks in your workload.</span></span> <span data-ttu-id="ed23a-309">Toomodify hello 서식 파일의 다른 섹션을 사용 하도록 하려는 경우 먼저 파악해 두십시오 hello 일괄 처리 설명서를 검토 하 고 일부 hello 일괄 처리 코드 샘플을 시험 하 여 일괄 처리 작동 하는 방식을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-309">If you want toomodify a different section of hello template, please first familiarize yourself with how Batch works by reviewing hello Batch documentation and trying out a few of hello Batch code samples.</span></span>
> 
> 

<span data-ttu-id="ed23a-310">hello run () 메서드는 hello 명령줄을 시작, 하나 이상의 프로세스를 시작, 모든 프로세스 toocomplete 기다리는 hello 결과 저장 및 마지막 종료 코드를 반환 하는 일을 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-310">hello Run() method is responsible for launching hello command line, starting one or more processes, waiting for all process toocomplete, saving hello results, and finally returning with an exit code.</span></span> <span data-ttu-id="ed23a-311">run () 메서드 hello hello 처리 작업에 대 한 논리를 구현 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-311">hello Run() method is where you implement hello processing logic for your tasks.</span></span> <span data-ttu-id="ed23a-312">드립니다; hello run () 메서드를 호출 하는 hello 작업 프로세서 프레임 워크 toocall 필요가 없습니다 것 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-312">hello task processor framework invokes hello Run() method for you; you do not need toocall it yourself.</span></span>

<span data-ttu-id="ed23a-313">Run() 구현에서는 다음에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-313">Your Run() implementation has access to:</span></span>

* <span data-ttu-id="ed23a-314">hello 통해 작업 매개 변수를 hello `_parameters` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-314">hello task parameters, via hello `_parameters` field.</span></span>
* <span data-ttu-id="ed23a-315">hello 통해 작업 및 작업 id hello `_jobId` 및 `_taskId` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-315">hello job and task ids, via hello `_jobId` and `_taskId` fields.</span></span>
* <span data-ttu-id="ed23a-316">hello 통해 hello 작업 구성 `_configuration` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-316">hello task configuration, via hello `_configuration` field.</span></span>

<span data-ttu-id="ed23a-317">**태스크 실패**</span><span class="sxs-lookup"><span data-stu-id="ed23a-317">**Task failure**</span></span>

<span data-ttu-id="ed23a-318">오류가 발생 한 경우 예외를 throw 하 여 hello run () 메서드를 종료할 수 있습니다 되지만이 hello 최상위 수준의 예외 처리기 hello 작업 종료 코드를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-318">In case of failure, you can exit hello Run() method by throwing an exception, but this leaves hello top level exception handler in control of hello task exit code.</span></span> <span data-ttu-id="ed23a-319">Hello 작업 및 기타 되어서는 안 진단 목적을 위해 다양 한 유형의 실패, 예를 들어 구분할 수 있도록 toocontrol hello 종료 코드를 필요 하거나 몇 가지 오류 모드를 종료 해야 하기 때문에 다음을 반환 하 여 hello run () 메서드를 종료 해야는 0이 아닌 종료 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-319">If you need toocontrol hello exit code so that you can distinguish different types of failure, for example for diagnostic purposes or because some failure modes should terminate hello job and others should not, then you should exit hello Run() method by returning a non-zero exit code.</span></span> <span data-ttu-id="ed23a-320">이 hello 작업 종료 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-320">This becomes hello task exit code.</span></span>

### <a name="exit-codes-and-exceptions-in-hello-task-processor-template"></a><span data-ttu-id="ed23a-321">종료 코드와 hello 프로세서 작업 서식 파일의 예외</span><span class="sxs-lookup"><span data-stu-id="ed23a-321">Exit codes and exceptions in hello Task Processor template</span></span>
<span data-ttu-id="ed23a-322">종료 코드와 예외는 프로그램을 실행 하는의 메커니즘 toodetermine hello 결과 제공 하 고 hello 프로그램 hello 실행 된 모든 문제를 식별에 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-322">Exit codes and exceptions provide a mechanism toodetermine hello outcome of running a program, and they can help identify any problems with hello execution of hello program.</span></span> <span data-ttu-id="ed23a-323">hello 프로세서 작업 템플릿 hello 종료 코드 및이 섹션에 설명 된 예외를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-323">hello Task Processor template implements hello exit codes and exceptions described in this section.</span></span>

<span data-ttu-id="ed23a-324">Hello 프로세서 작업 템플릿을 사용 하 여 구현 되는 프로세서 작업 세 가지 가능한 종료 코드를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-324">A task processor task that is implemented with hello Task Processor template can return three possible exit codes:</span></span>

| <span data-ttu-id="ed23a-325">코드</span><span class="sxs-lookup"><span data-stu-id="ed23a-325">Code</span></span> | <span data-ttu-id="ed23a-326">설명</span><span class="sxs-lookup"><span data-stu-id="ed23a-326">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ed23a-327">[Process.ExitCode][process_exitcode]</span><span class="sxs-lookup"><span data-stu-id="ed23a-327">[Process.ExitCode][process_exitcode]</span></span> |<span data-ttu-id="ed23a-328">hello 작업 프로세서 toocompletion 실행 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-328">hello task processor ran toocompletion.</span></span> <span data-ttu-id="ed23a-329">이 의미 하지는 성공적으로 호출 된 해당 hello 프로그램 참고-hello 작업 프로세서만 성공적으로 실행 하 고 예외 없이 후 처리를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-329">Note that this does not imply that hello program you invoked was successful – only that hello task processor invoked it successfully and performed any post-processing without exceptions.</span></span> <span data-ttu-id="ed23a-330">hello 종료 코드의 hello 의미 hello 호출 프로그램에 따라 다릅니다. – hello 프로그램 성공 했 고 다른 종료 코드 이면 hello 프로그램 실패 종료 코드 0 일반적으로 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-330">hello meaning of hello exit code depends on hello invoked program – typically exit code 0 means hello program succeeded and any other exit code means hello program failed.</span></span> |
| <span data-ttu-id="ed23a-331">1</span><span class="sxs-lookup"><span data-stu-id="ed23a-331">1</span></span> |<span data-ttu-id="ed23a-332">hello 작업 프로세서에서 '예상된' 부분이 hello 프로그램의 예외로 인해 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-332">hello task processor failed with an exception in an 'expected' part of hello program.</span></span> <span data-ttu-id="ed23a-333">hello 예외는 번역 된 tooa `TaskProcessorException` 와 진단 정보 및 해결에 대 한 제안을 오류 hello 가능한 경우.</span><span class="sxs-lookup"><span data-stu-id="ed23a-333">hello exception was translated tooa `TaskProcessorException` with diagnostic information and, where possible, suggestions for resolving hello failure.</span></span> |
| <span data-ttu-id="ed23a-334">2</span><span class="sxs-lookup"><span data-stu-id="ed23a-334">2</span></span> |<span data-ttu-id="ed23a-335">hello 작업 프로세서 '예기치 않은' 예외로 인해 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-335">hello task processor failed with an 'unexpected' exception.</span></span> <span data-ttu-id="ed23a-336">hello 예외는 출력 기록된 toostandard 했지만 hello 작업 프로세서 수 없습니다 tooadd 추가 진단 또는 업데이트 관리 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-336">hello exception was logged toostandard output, but hello task processor was unable tooadd any additional diagnostic or remediation information.</span></span> |

> [!NOTE]
> <span data-ttu-id="ed23a-337">호출 하는 hello 프로그램이 종료 코드 1 및 2 tooindicate 특정 오류 모드를 사용 하는 경우 다음 종료 코드 1과 2를 사용 하 여 프로세서 작업 오류에 대 한가 모호 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-337">If hello program you invoke uses exit codes 1 and 2 tooindicate specific failure modes, then using exit codes 1 and 2 for task processor errors is ambiguous.</span></span> <span data-ttu-id="ed23a-338">Hello Program.cs 파일의 hello 예외 사례를 편집 하 여 이러한 작업 오류 코드 프로세서 toodistinctive 종료 코드를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-338">You can change these task processor error codes toodistinctive exit codes by editing hello exception cases in hello Program.cs file.</span></span>
> 
> 

<span data-ttu-id="ed23a-339">예외에서 반환 하는 모든 hello 정보 stderr.txt 및 stdout.txt 파일에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-339">All hello information returned by exceptions is written into stdout.txt and stderr.txt files.</span></span> <span data-ttu-id="ed23a-340">자세한 내용은 hello 일괄 처리 설명서에서에서 오류 처리를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-340">For more information, see Error Handling, in hello Batch documentation.</span></span>

### <a name="client-considerations"></a><span data-ttu-id="ed23a-341">클라이언트 고려 사항</span><span class="sxs-lookup"><span data-stu-id="ed23a-341">Client considerations</span></span>
<span data-ttu-id="ed23a-342">**Storage 자격 증명**</span><span class="sxs-lookup"><span data-stu-id="ed23a-342">**Storage credentials**</span></span>

<span data-ttu-id="ed23a-343">예를 들어 hello 파일 규칙 도우미 라이브러리를 사용 하 여 Azure blob 저장소 toopersist 출력을 사용 하 여 작업 프로세서 경우 너무 액세스 해야*어느* 클라우드 스토리지 계정 자격 증명 hello *또는* 공유 액세스 서명 (SAS)를 포함 하는 blob 컨테이너 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-343">If your task processor uses Azure blob storage toopersist outputs, for example using hello file conventions helper library, then it needs access too*either* hello cloud storage account credentials *or* a blob container URL that includes a shared access signature (SAS).</span></span> <span data-ttu-id="ed23a-344">hello 서식 파일에는 일반적인 환경 변수를 통해 자격 증명을 제공 하는 것에 대 한 지원이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-344">hello template includes support for providing credentials via common environment variables.</span></span> <span data-ttu-id="ed23a-345">클라이언트는 다음과 같이 hello 저장소 자격 증명을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-345">Your client can pass hello storage credentials as follows:</span></span>

```csharp
job.CommonEnvironmentSettings = new [] {
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

<span data-ttu-id="ed23a-346">hello 저장소 계정은 hello hello 통해 TaskProcessor 클래스에서에서 사용할 수 있는 다음 `_configuration.StorageAccount` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-346">hello storage account is then available in hello TaskProcessor class via hello `_configuration.StorageAccount` property.</span></span>

<span data-ttu-id="ed23a-347">Toouse 된 SAS는 컨테이너 URL을 선호 하는 경우 작업 일반적인 환경 설정, 통해 이름을 전달할 수도 있습니다 하지만 hello 작업 프로세서 템플릿을 포함 하지는 않습니다이 기본적으로 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-347">If you prefer toouse a container URL with SAS, you can also pass this via an job common environment setting, but hello task processor template does not currently include built-in support for this.</span></span>

<span data-ttu-id="ed23a-348">**Storage 설정**</span><span class="sxs-lookup"><span data-stu-id="ed23a-348">**Storage setup**</span></span>

<span data-ttu-id="ed23a-349">해당 hello 클라이언트 또는 작업 관리자 태스크가 hello 작업 toohello 작업을 추가 하기 전에 작업에 필요한 모든 컨테이너를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-349">It is recommended that hello client or job manager task create any containers required by tasks before adding hello tasks toohello job.</span></span> <span data-ttu-id="ed23a-350">컨테이너 URL을 사용 하 여 SAS로으로 URL을 포함 하지 않을 경우 권한 toocreate hello 컨테이너 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-350">This is mandatory if you use a container URL with SAS, as such a URL does not include permission toocreate hello container.</span></span> <span data-ttu-id="ed23a-351">Toocall CloudBlobContainer.CreateIfNotExistsAsync hello 컨테이너에 있는 모든 작업을 저장 하는 대로 저장소 계정 자격 증명을 전달 하는 경우에 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-351">It is recommended even if you pass storage account credentials, as it saves every task having toocall CloudBlobContainer.CreateIfNotExistsAsync on hello container.</span></span>

## <a name="pass-parameters-and-environment-variables"></a><span data-ttu-id="ed23a-352">매개 변수 및 환경 변수 전달</span><span class="sxs-lookup"><span data-stu-id="ed23a-352">Pass parameters and environment variables</span></span>
### <a name="pass-environment-settings"></a><span data-ttu-id="ed23a-353">환경 설정 전달</span><span class="sxs-lookup"><span data-stu-id="ed23a-353">Pass environment settings</span></span>
<span data-ttu-id="ed23a-354">클라이언트 환경 설정의 hello 형태로 정보 toohello 작업 관리자 태스크를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-354">A client can pass information toohello job manager task in hello form of environment settings.</span></span> <span data-ttu-id="ed23a-355">Hello의 일부로 실행 될 hello 작업 프로세서 작업 생성 작업을 계산 하는 경우이 정보 hello 작업 관리자 태스크에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-355">This information can then be used by hello job manager task when generating hello task processor tasks that will run as part of hello compute job.</span></span> <span data-ttu-id="ed23a-356">환경 설정으로 전달할 수 있는 hello 정보의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-356">Examples of hello information that you can pass as environment settings are:</span></span>

* <span data-ttu-id="ed23a-357">Storage 계정 이름 및 계정 키</span><span class="sxs-lookup"><span data-stu-id="ed23a-357">Storage account name and account keys</span></span>
* <span data-ttu-id="ed23a-358">배치 계정 URL</span><span class="sxs-lookup"><span data-stu-id="ed23a-358">Batch account URL</span></span>
* <span data-ttu-id="ed23a-359">배치 계정 키</span><span class="sxs-lookup"><span data-stu-id="ed23a-359">Batch account key</span></span>

<span data-ttu-id="ed23a-360">hello를 사용 하 여 hello 일괄 처리 서비스에 간단한 메커니즘 toopass 환경 설정을 tooa 작업 관리자 태스크가 `EnvironmentSettings` 속성 [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask]합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-360">hello Batch service has a simple mechanism toopass environment settings tooa job manager task by using hello `EnvironmentSettings` property in [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask].</span></span>

<span data-ttu-id="ed23a-361">예를 들어 tooget hello `BatchClient` 인스턴스 일괄 처리 계정에 대 한 hello 클라이언트에서 환경 변수는 hello URL을 코딩 하 고 공유 hello 일괄 처리 계정에 대 한 키 자격 증명을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-361">For example, tooget hello `BatchClient` instance for a Batch account, you can pass as environment variables from hello client code hello URL and shared key credentials for hello Batch account.</span></span> <span data-ttu-id="ed23a-362">마찬가지로, tooaccess hello 저장소 계정을 연결 된 toohello 일괄 처리 계정, 환경 변수로 hello 저장소 계정 이름 및 hello 저장소 계정 키를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-362">Likewise, tooaccess hello storage account that is linked toohello Batch account, you can pass hello storage account name and hello storage account key as environment variables.</span></span>

### <a name="pass-parameters-toohello-job-manager-template"></a><span data-ttu-id="ed23a-363">Toohello 작업 관리자 템플릿 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="ed23a-363">Pass parameters toohello Job Manager template</span></span>
<span data-ttu-id="ed23a-364">대부분의 경우에서 유용 toopass 작업당 매개 변수 toohello 작업 관리자 작업 프로세스 toocontrol hello 작업 중 하나 또는 tooconfigure hello 작업에 대 한 hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-364">In many cases, it's useful toopass per-job parameters toohello job manager task, either toocontrol hello job splitting process or tooconfigure hello tasks for hello job.</span></span> <span data-ttu-id="ed23a-365">이렇게 하려면 hello 작업 관리자 태스크에 대 한 리소스 파일로 parameters.json 라는 JSON 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-365">You can do this by uploading a JSON file named parameters.json as a resource file for hello job manager task.</span></span> <span data-ttu-id="ed23a-366">hello 매개 변수 hello에서 제공 될 수 있습니다 `JobSplitter._parameters` hello 작업 관리자 서식 파일의 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-366">hello parameters can then become available in hello `JobSplitter._parameters` field in hello Job Manager template.</span></span>

> [!NOTE]
> <span data-ttu-id="ed23a-367">hello 기본 제공 매개 변수 처리기 문자열-문자열 사전만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-367">hello built-in parameter handler supports only string-to-string dictionaries.</span></span> <span data-ttu-id="ed23a-368">매개 변수 값으로 toopass 복잡 한 JSON 값을 원하는 됩니다 필요 toopass 문자열로 이러한 및 hello 작업 분할에 구문 분석 하거나 경우 hello 프레임 워크의 수정 `Configuration.GetJobParameters` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ed23a-368">If you want toopass complex JSON values as parameter values, you will need toopass these as strings and parse them in hello job splitter, or modify hello framework's `Configuration.GetJobParameters` method.</span></span>
> 
> 

### <a name="pass-parameters-toohello-task-processor-template"></a><span data-ttu-id="ed23a-369">Toohello 작업 프로세서 템플릿 매개 변수 전달</span><span class="sxs-lookup"><span data-stu-id="ed23a-369">Pass parameters toohello Task Processor template</span></span>
<span data-ttu-id="ed23a-370">전달할 수도 있습니다 매개 변수 tooindividual 작업 hello 프로세서 작업 서식 파일을 사용 하 여 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-370">You can also pass parameters tooindividual tasks implemented using hello Task Processor template.</span></span> <span data-ttu-id="ed23a-371">마찬가지로 hello 작업 관리자 템플릿을 사용 하 여 hello 작업 프로세서 템플릿은 찾습니다 라는 리소스 파일</span><span class="sxs-lookup"><span data-stu-id="ed23a-371">Just as with hello job manager template, hello task processor template looks for a resource file named</span></span>

<span data-ttu-id="ed23a-372">parameters.json, 고이 있는 경우 hello 매개 변수 사전으로 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-372">parameters.json, and if found it loads it as hello parameters dictionary.</span></span> <span data-ttu-id="ed23a-373">두 가지 방법을 toopass 매개 변수 toohello 작업 프로세서 작업에 대 한 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-373">There are a couple of options for how toopass parameters toohello task processor tasks:</span></span>

* <span data-ttu-id="ed23a-374">Hello JSON 작업 매개 변수를 다시 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-374">Reuse hello job parameters JSON.</span></span> <span data-ttu-id="ed23a-375">Hello 유일한 매개 변수는 작업 수준 요소 (예: 렌더링 높이 너비) 경우에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-375">This works well if hello only parameters are job-wide ones (for example, a render height and width).</span></span> <span data-ttu-id="ed23a-376">toodo이 hello 작업 분할에는 CloudTask을 만들 때 ResourceFiles hello 작업 관리자 태스크에서에서 참조 toohello parameters.json 리소스 파일 개체를 추가 (`JobSplitter._jobManagerTask.ResourceFiles`) toohello CloudTask ResourceFiles 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-376">toodo this, when creating a CloudTask in hello job splitter, add a reference toohello parameters.json resource file object from hello job manager task's ResourceFiles (`JobSplitter._jobManagerTask.ResourceFiles`) toohello CloudTask's ResourceFiles collection.</span></span>
* <span data-ttu-id="ed23a-377">생성 및 작업 분할 실행의 일부로 작업별 parameters.json 문서를 업로드 하 고 hello 작업의 리소스 파일 컬렉션에 해당 blob을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-377">Generate and upload a task-specific parameters.json document as part of job splitter execution, and reference that blob in hello task's resource files collection.</span></span> <span data-ttu-id="ed23a-378">다양한 태스크에 서로 다른 매개 변수가 있는 경우 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-378">This is necessary if different tasks have different parameters.</span></span> <span data-ttu-id="ed23a-379">Hello 프레임 인덱스를 매개 변수로 toohello 태스크를 전달 되는 3D 렌더링 시나리오를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-379">An example might be a 3D rendering scenario where hello frame index is passed toohello task as a parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="ed23a-380">hello 기본 제공 매개 변수 처리기 문자열-문자열 사전만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-380">hello built-in parameter handler supports only string-to-string dictionaries.</span></span> <span data-ttu-id="ed23a-381">매개 변수 값으로 toopass 복잡 한 JSON 값을 원하는 됩니다 필요 toopass 문자열로 이러한 및 hello 작업 프로세서에서 구문 분석 하거나 경우 hello 프레임 워크의 수정 `Configuration.GetTaskParameters` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ed23a-381">If you want toopass complex JSON values as parameter values, you will need toopass these as strings and parse them in hello task processor, or modify hello framework's `Configuration.GetTaskParameters` method.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ed23a-382">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ed23a-382">Next steps</span></span>
### <a name="persist-job-and-task-output-tooazure-storage"></a><span data-ttu-id="ed23a-383">작업을 유지 하 고 출력 tooAzure 저장소 작업</span><span class="sxs-lookup"><span data-stu-id="ed23a-383">Persist job and task output tooAzure Storage</span></span>
<span data-ttu-id="ed23a-384">Batch 솔루션 개발 시 다른 유용한 도구는 [Azure Batch 파일 규칙][nuget_package]입니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-384">Another helpful tool in Batch solution development is [Azure Batch File Conventions][nuget_package].</span></span> <span data-ttu-id="ed23a-385">일괄 처리.NET 응용 프로그램 tooeasily 저장소에서 (현재 미리 보기)에이.NET 클래스 라이브러리를 사용 하 고 Azure 저장소에서 작업 출력 tooand를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-385">Use this .NET class library (currently in preview) in your Batch .NET applications tooeasily store and retrieve task outputs tooand from Azure Storage.</span></span> <span data-ttu-id="ed23a-386">[Azure 일괄 처리 작업 및 태스크 출력 유지](batch-task-output.md) hello 라이브러리와 사용법에 대 한 자세한 내용은 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-386">[Persist Azure Batch job and task output](batch-task-output.md) contains a full discussion of hello library and its usage.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="ed23a-387">배치 포럼</span><span class="sxs-lookup"><span data-stu-id="ed23a-387">Batch Forum</span></span>
<span data-ttu-id="ed23a-388">hello [Azure 배치 포럼] [ forum] 는 좋은 toodiscuss 일괄 처리를 놓고 hello 서비스에 대 한 질문은 msdn 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-388">hello [Azure Batch Forum][forum] on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="ed23a-389">유용한 "고정" 게시물을 참조하고 Batch 솔루션을 빌드하는 동안 질문이 생기면 즉시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="ed23a-389">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

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
