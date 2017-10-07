---
title: "aaaAzure 팀 데이터 과학 프로세스 개요 | Microsoft Docs"
description: "데이터 과학 방법론 toodeliver 예측 분석 솔루션을 제공 지능형 응용 프로그램 및입니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 2ba03585a6f6f855faaa3b5c0c75149cad0a88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-overview"></a><span data-ttu-id="9491a-103">Team Data Science Process 개요</span><span class="sxs-lookup"><span data-stu-id="9491a-103">Team Data Science Process overview</span></span>

<span data-ttu-id="9491a-104">hello 팀 데이터 과학 프로세스 (TDSP)는는 agile 반복 데이터 과학 방법론 toodeliver 예측 분석 솔루션 및 지능형 응용 프로그램 효율적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-104">hello Team Data Science Process (TDSP) is an agile, iterative data science methodology toodeliver predictive analytics solutions and intelligent applications efficiently.</span></span> <span data-ttu-id="9491a-105">TDSP는 팀 공동 작업 및 학습을 향상하도록 돕습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-105">TDSP helps improve team collaboration and learning.</span></span> <span data-ttu-id="9491a-106">Hello에 대 한 유용한 정보 및 구조에서 Microsoft 및 기타 hello 업계의 hello 데이터 과학 이니셔티브의 성공적인 구현을 용이 하 게 하는 추출할을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-106">It contains a distillation of hello best practices and structures from Microsoft and others in hello industry that facilitate hello successful implementation of data science initiatives.</span></span> <span data-ttu-id="9491a-107">hello ´ ֲ toohelp 회사에는 완벽 하 게 해당 분석 프로그램의 hello 장점을 실제 이용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-107">hello goal is toohelp companies fully realize hello benefits of their analytics program.</span></span>

<span data-ttu-id="9491a-108">이 문서에서는 TDSP 및 주요 구성 요소의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-108">This article provides an overview of TDSP and its main components.</span></span> <span data-ttu-id="9491a-109">다양 한 도구와 구현 될 수 있는 hello 프로세스 여기의 일반적인 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-109">We provide a generic description of hello process here that can be implemented with a variety of tools.</span></span> <span data-ttu-id="9491a-110">Hello 프로젝트 작업 및 hello 프로세스의 수명 주기 hello에에서 관련 된 역할의 더 자세한 설명은 추가 연결 된 항목에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-110">A more detailed description of hello project tasks and roles involved in hello lifecycle of hello process is provided in additional linked topics.</span></span> <span data-ttu-id="9491a-111">Tooimplement hello Microsoft 도구 및 인프라 tooimplement hello TDSP을 사용 하 여 팀에서의 특정 집합을 사용 하 여 TDSP도 제공 방법에 대 한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-111">Guidance on how tooimplement hello TDSP using a specific set of Microsoft tools and infrastructure that we use tooimplement hello TDSP in our teams is also provided.</span></span>

## <a name="key-components-of-hello-tdsp"></a><span data-ttu-id="9491a-112">Hello TDSP의 주요 구성 요소</span><span class="sxs-lookup"><span data-stu-id="9491a-112">Key components of hello TDSP</span></span>

<span data-ttu-id="9491a-113">TDSP hello 다음과 같은 주요 구성 요소가 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-113">TDSP comprises of hello following key components:</span></span>

- <span data-ttu-id="9491a-114">**데이터 과학 수명 주기** 정의</span><span class="sxs-lookup"><span data-stu-id="9491a-114">A **data science lifecycle** definition</span></span>
- <span data-ttu-id="9491a-115">**표준화된 프로젝트 구조**</span><span class="sxs-lookup"><span data-stu-id="9491a-115">A **standardized project structure**</span></span>
- <span data-ttu-id="9491a-116">데이터 과학 프로젝트에 대한 **인프라 및 리소스**</span><span class="sxs-lookup"><span data-stu-id="9491a-116">**Infrastructure and resources** for data science projects</span></span>
- <span data-ttu-id="9491a-117">프로젝트 실행에 대한 **도구 및 유틸리티**</span><span class="sxs-lookup"><span data-stu-id="9491a-117">**Tools and utilities** for project execution</span></span>


## <a name="data-science-lifecycle"></a><span data-ttu-id="9491a-118">데이터 과학 수명 주기</span><span class="sxs-lookup"><span data-stu-id="9491a-118">Data science lifecycle</span></span>

<span data-ttu-id="9491a-119">hello 팀 데이터 과학 프로세스 (TDSP) 데이터 과학 프로젝트의 수명 주기 toostructure hello 개발을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-119">hello Team Data Science Process (TDSP) provides a lifecycle toostructure hello development of your data science projects.</span></span> <span data-ttu-id="9491a-120">hello 수명 주기에서 다음에 나오는 프로젝트 일반적으로 실행 될 때 시작 toofinish hello 단계를 간략하게 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-120">hello lifecycle outlines hello steps, from start toofinish, that projects usually follow when they are executed.</span></span>

<span data-ttu-id="9491a-121">다른 데이터 과학 수명 주기를와 같은 사용 중인 경우 [CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) 회사의 사용자 지정 프로세스를 계속 사용할 수 있습니다 또는 해당 개발의 hello 컨텍스트에서 작업 기반 TDSP hello 주기 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-121">If you are using another data science lifecycle, such as [CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) or your organization's own custom process, you can still use hello task-based TDSP in hello context of those development lifecycles.</span></span> <span data-ttu-id="9491a-122">상위 수준에서 이러한 다양한 방법에는 많은 공통점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-122">At a high level, these different methodologies have much in common.</span></span> 

<span data-ttu-id="9491a-123">이 수명 주기는 지능형 응용 프로그램의 일부로 제공되는 데이터 과학 프로젝트를 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-123">This lifecycle has been designed for data science projects that ship as part of intelligent applications.</span></span> <span data-ttu-id="9491a-124">이러한 응용 프로그램은 예측 분석을 위해 기계 학습 또는 인공 지능 모델을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-124">These applications deploy machine learning or artificial intelligence models for predictive analytics.</span></span> <span data-ttu-id="9491a-125">예비 데이터 과학 프로젝트 또는 임시 분석 프로젝트에서 이 프로세스를 사용하여 활용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-125">Exploratory data science projects or ad hoc analytics projects can also benefit from using this process.</span></span> <span data-ttu-id="9491a-126">하지만 이러한 경우에 설명 된 hello 단계 중 일부는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-126">But in such cases some of hello steps described may not be needed.</span></span>    

<span data-ttu-id="9491a-127">hello TDSP 수명 주기는 반복적으로 실행 되는 5 개의 주요 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-127">hello TDSP lifecycle is composed of five major stages that are executed iteratively:</span></span>

* <span data-ttu-id="9491a-128">**비즈니스 이해**</span><span class="sxs-lookup"><span data-stu-id="9491a-128">**Business Understanding**</span></span>
* <span data-ttu-id="9491a-129">**데이터 취득 및 이해**</span><span class="sxs-lookup"><span data-stu-id="9491a-129">**Data Acquisition and Understanding**</span></span>
* <span data-ttu-id="9491a-130">**모델링**</span><span class="sxs-lookup"><span data-stu-id="9491a-130">**Modeling**</span></span>
* <span data-ttu-id="9491a-131">**배포웹사이트를**</span><span class="sxs-lookup"><span data-stu-id="9491a-131">**Deployment**</span></span>
* <span data-ttu-id="9491a-132">**고객 승인**</span><span class="sxs-lookup"><span data-stu-id="9491a-132">**Customer Acceptance**</span></span>

<span data-ttu-id="9491a-133">여기 hello의 시각적 표현인 **팀 데이터 과학 프로세스 수명 주기**합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-133">Here is a visual representation of hello **Team Data Science Process lifecycle**.</span></span> 

![TDSP 수명 주기](./media/data-science-process-overview/tdsp-lifecycle.png) 

<span data-ttu-id="9491a-135">hello 목표, 작업 및 TDSP에 hello 주기의 각 단계에 대 한 설명서 아티팩트에에서 설명 된 hello [팀 데이터 과학 프로세스 수명 주기](data-science-process-lifecycle.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-135">hello goals, tasks, and documentation artifacts for each stage of hello lifecycle in TDSP are described in hello [Team Data Science Process lifecycle](data-science-process-lifecycle.md) topic.</span></span> <span data-ttu-id="9491a-136">이러한 작업 및 아티팩트는 프로젝트 역할과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-136">These tasks and artifacts are associated with project roles:</span></span>

- <span data-ttu-id="9491a-137">솔루션 설계자</span><span class="sxs-lookup"><span data-stu-id="9491a-137">Solution architect</span></span>
- <span data-ttu-id="9491a-138">프로젝트 관리자</span><span class="sxs-lookup"><span data-stu-id="9491a-138">Project manager</span></span>
- <span data-ttu-id="9491a-139">데이터 과학자</span><span class="sxs-lookup"><span data-stu-id="9491a-139">Data scientist</span></span>
- <span data-ttu-id="9491a-140">프로젝트 책임자</span><span class="sxs-lookup"><span data-stu-id="9491a-140">Project lead</span></span> 

<span data-ttu-id="9491a-141">hello 다음 다이어그램에서는 hello (파란색) 작업과 hello 세로 축) (에 이러한 역할에 대 한 hello 가로 축) (에 hello 주기의 각 단계와 관련 된 (녹색)으로 아티팩트의 표 뷰.</span><span class="sxs-lookup"><span data-stu-id="9491a-141">hello following diagram provides a grid view of hello tasks (in blue) and artifacts (in green) associated with each stage of hello lifecycle (on hello horizontal axis) for these roles (on hello vertical axis).</span></span> 

![TDSP 역할 및 작업](./media/data-science-process-overview/tdsp-tasks-by-roles.png)

## <a name="standardized-project-structure"></a><span data-ttu-id="9491a-143">표준화된 프로젝트 구조</span><span class="sxs-lookup"><span data-stu-id="9491a-143">Standardized project structure</span></span>

<span data-ttu-id="9491a-144">모든 프로젝트 디렉터리 구조를 공유 하 고 프로젝트의 문서에 대 한 서식 파일을 사용 하면 해당 프로젝트에 대 한 hello 팀 구성원 toofind 정보를 쉽게 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-144">Having all projects share a directory structure and use templates for project documents makes it easy for hello team members toofind information about their projects.</span></span> <span data-ttu-id="9491a-145">모든 코드 및 문서 Git, TFS 또는 Subversion tooenable 팀 공동 작업와 같은 버전 제어 시스템 (VC)에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-145">All code and documents are stored in a version control system (VCS) like Git, TFS, or Subversion tooenable team collaboration.</span></span> <span data-ttu-id="9491a-146">작업 및 Jira와 같은 시스템을 추적 하는 agile 프로젝트의 기능을 추적, Rally, Visual Studio Team Services 추적할 수 있게 가깝게 개별 기능에 대 한 hello 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-146">Tracking tasks and features in an agile project tracking system like Jira, Rally, Visual Studio Team Services allows closer tracking of hello code for individual features.</span></span> <span data-ttu-id="9491a-147">이러한 추적에는 팀 tooobtain을 더 비용을 추산 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-147">Such tracking also enables teams tooobtain better cost estimates.</span></span> <span data-ttu-id="9491a-148">TDSP 버전 관리, 정보 보안 및 공동 작업에 대 한 hello VCS에 각 프로젝트에 대 한 별도 저장소를 만드는 것을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-148">TDSP recommends creating a separate repository for each project on hello VCS for versioning, information security, and collaboration.</span></span> <span data-ttu-id="9491a-149">hello는 hello 조직 전체에서 모든 프로젝트는 데 도움이 됩니다 빌드 조직의 지식에 대 한 구조를 표준화 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-149">hello standardized structure for all projects helps build institutional knowledge across hello organization.</span></span>

<span data-ttu-id="9491a-150">Hello 폴더 구조 및 기본 위치에 필요한 문서에 대 한 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-150">We provide templates for hello folder structure and required documents in standard locations.</span></span> <span data-ttu-id="9491a-151">이 폴더 구조는 hello 파일 데이터 탐색 및 기능 추출에 대 한 코드를 포함 하 고 해당 모델 반복 레코드를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-151">This folder structure organizes hello files that contain code for data exploration and feature extraction, and that record model iterations.</span></span> <span data-ttu-id="9491a-152">이러한 템플릿을 사용 하면 다른 사용자가 수행 하는 팀 멤버 toounderstand 작업에 대 한 보다 쉽게 새 멤버 tooteams tooadd 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-152">These templates make it easier for team members toounderstand work done by others and tooadd new members tooteams.</span></span> <span data-ttu-id="9491a-153">것이 쉬운 tooview 및 업데이트 문서 템플릿 마크 다운 형태로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-153">It is easy tooview and update document templates in markdown format.</span></span> <span data-ttu-id="9491a-154">각 프로젝트 tooinsure hello 문제는 잘 정의 된 및 해당 결과물 hello 품질 예상을 충족에 대 한 주요 질문으로 tooprovide 검사 목록 서식 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-154">Use templates tooprovide checklists with key questions for each project tooinsure that hello problem is well-defined and that deliverables meet hello quality expected.</span></span> <span data-ttu-id="9491a-155">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-155">Examples include:</span></span>

- <span data-ttu-id="9491a-156">프로젝트 기본 문서 toodocument hello 비즈니스 문제 및 hello 프로젝트의 범위</span><span class="sxs-lookup"><span data-stu-id="9491a-156">a project charter toodocument hello business problem and scope of hello project</span></span>
- <span data-ttu-id="9491a-157">데이터는 toodocument hello 구조와 hello 원시 데이터의 통계를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-157">data reports toodocument hello structure and statistics of hello raw data</span></span>
- <span data-ttu-id="9491a-158">모델 보고서 toodocument hello 파생 기능</span><span class="sxs-lookup"><span data-stu-id="9491a-158">model reports toodocument hello derived features</span></span>
- <span data-ttu-id="9491a-159">ROC 곡선 또는 MSE와 같은 모델 성능 메트릭</span><span class="sxs-lookup"><span data-stu-id="9491a-159">model performance metrics such as ROC curves or MSE</span></span>


![TDSP 디렉터리](./media/data-science-process-overview/tdsp-dir-structure.png)

<span data-ttu-id="9491a-161">hello 디렉터리 구조에서 복제할 수 있는 [Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate)합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-161">hello directory structure can be cloned from [Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate).</span></span>

## <a name="infrastructure-and-resources-for-data-science-projects"></a><span data-ttu-id="9491a-162">데이터 과학 프로젝트에 대한 인프라 및 리소스</span><span class="sxs-lookup"><span data-stu-id="9491a-162">Infrastructure and resources for data science projects</span></span>

<span data-ttu-id="9491a-163">TDSP는 다음과 같은 공유 분석 및 저장소 인프라를 관리하기 위한 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-163">TDSP provides recommendations for managing shared analytics and storage infrastructure such as:</span></span>

- <span data-ttu-id="9491a-164">데이터 집합을 저장하기 위한 클라우드 파일 시스템,</span><span class="sxs-lookup"><span data-stu-id="9491a-164">cloud file systems for storing datasets,</span></span> 
- <span data-ttu-id="9491a-165">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="9491a-165">databases</span></span>
- <span data-ttu-id="9491a-166">빅 데이터(Hadoop 또는 Spark) 클러스터</span><span class="sxs-lookup"><span data-stu-id="9491a-166">big data (Hadoop or Spark) clusters</span></span> 
- <span data-ttu-id="9491a-167">기계 학습 서비스</span><span class="sxs-lookup"><span data-stu-id="9491a-167">machine learning services.</span></span> 

<span data-ttu-id="9491a-168">hello 분석 및 저장소 인프라 hello 클라우드 또는 온-프레미스 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-168">hello analytics and storage infrastructure can be in hello cloud or on-premises.</span></span> <span data-ttu-id="9491a-169">이는 원시 및 처리된 데이터 집합이 저장되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-169">This is where raw and processed datasets are stored.</span></span> <span data-ttu-id="9491a-170">이 인프라는 재현 가능한 분석을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-170">This infrastructure enables reproducible analysis.</span></span> <span data-ttu-id="9491a-171">또한 불필요 한 인프라 비용 및 tooinconsistencies 될 수 있는 중복을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-171">It also avoids duplication, which can lead tooinconsistencies and unnecessary infrastructure costs.</span></span> <span data-ttu-id="9491a-172">도구는 tooprovision hello 공유 리소스, 추적 하 고 각 팀 멤버 tooconnect toothose 리소스를 안전 하 게 허용 제공.</span><span class="sxs-lookup"><span data-stu-id="9491a-172">Tools are provided tooprovision hello shared resources, track them, and allow each team member tooconnect toothose resources securely.</span></span> <span data-ttu-id="9491a-173">프로젝트 멤버가 일관성 있는 계산 환경을 만들도록 하는 것도 좋은 연습입니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-173">It is also a good practice have project members create a consistent compute environment.</span></span> <span data-ttu-id="9491a-174">그러면 다른 팀 멤버는 실험을 복제하고 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-174">Different team members can then replicate and validate experiments.</span></span>

<span data-ttu-id="9491a-175">여러 프로젝트에서 작업하고 다양한 클라우드 분석 인프라 구성 요소를 공유하는 팀의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-175">Here is an example of a team working on multiple projects and sharing various cloud analytics infrastructure components.</span></span>

![TDSP 인프라](./media/data-science-process-overview/tdsp-analytics-infra.png)


## <a name="tools-and-utilities-for-project-execution"></a><span data-ttu-id="9491a-177">프로젝트 실행에 대한 도구 및 유틸리티</span><span class="sxs-lookup"><span data-stu-id="9491a-177">Tools and utilities for project execution</span></span>

<span data-ttu-id="9491a-178">대부분의 조직에서 프로세스를 소개하는 것은 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-178">Introducing processes in most organizations is challenging.</span></span> <span data-ttu-id="9491a-179">도구는 tooimplement hello 데이터 과학 프로세스 및 수명 주기 hello 일관성의 도입을 증가 시킬 낮은 hello 장벽을 tooand 도움말을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-179">Tools provided tooimplement hello data science process and lifecycle help lower hello barriers tooand increase hello consistency of their adoption.</span></span> <span data-ttu-id="9491a-180">TDSP 팀 내에서 toojump 시작 단기간 TDSP 초기 집합이 도구 및 스크립트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-180">TDSP provides an initial set of tools and scripts toojump-start adoption of TDSP within a team.</span></span> <span data-ttu-id="9491a-181">또한 hello hello 데이터 과학 수명 주기 데이터 탐색 및 초기 계획 모델링 등의 일반적인 작업 중 일부를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-181">It also helps automate some of hello common tasks in hello data science lifecycle such as data exploration and baseline modeling.</span></span> <span data-ttu-id="9491a-182">개인에 대 한 toocontribute 공유 도구와 유틸리티는 팀의 코드를 공유 저장소로 제공에 잘 정의 된 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-182">There is a well-defined structure provided for individuals toocontribute shared tools and utilities into their team’s shared code repository.</span></span> <span data-ttu-id="9491a-183">이러한 리소스는 다음 hello 팀 또는 hello 조직 내 다른 프로젝트에서 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-183">These resources can then be leveraged by other projects within hello team or hello organization.</span></span> <span data-ttu-id="9491a-184">또한 TDSP 도구 및 유틸리티 toohello 전체 커뮤니티의 tooenable hello 기여를 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-184">TDSP also plans tooenable hello contributions of tools and utilities toohello whole community.</span></span> <span data-ttu-id="9491a-185">hello TDSP 유틸리티에서 복제할 수 있는 [Github](https://github.com/Azure/Azure-TDSP-Utilities)합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-185">hello TDSP utilities can be cloned from [Github](https://github.com/Azure/Azure-TDSP-Utilities).</span></span>


## <a name="next-steps"></a><span data-ttu-id="9491a-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9491a-186">Next steps</span></span>

<span data-ttu-id="9491a-187">[데이터 과학 프로세스 팀: 역할 및 작업](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md) hello 핵심 인력 역할 및이 프로세스를 표준화 하는 데이터 과학 팀에 대 한 관련된 작업에 간략하게 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491a-187">[Team Data Science Process: Roles and tasks](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md) Outlines hello key personnel roles and their associated tasks for a data science team that standardizes on this process.</span></span> 
