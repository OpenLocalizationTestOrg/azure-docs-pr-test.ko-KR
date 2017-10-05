---
title: "Azure Team Data Science Process 개요 | Microsoft Docs"
description: "예측 분석 솔루션 및 지능형 응용 프로그램을 제공하는 데이터 과학 방법론을 제공합니다."
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
ms.openlocfilehash: 006a1465a7cdced1878111beee709c8da4bc310f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="team-data-science-process-overview"></a><span data-ttu-id="e214c-103">Team Data Science Process 개요</span><span class="sxs-lookup"><span data-stu-id="e214c-103">Team Data Science Process overview</span></span>

<span data-ttu-id="e214c-104">TDSP(Team Data Science Process)는 예측 분석 솔루션 및 지능형 응용 프로그램을 효율적으로 제공하는 기민한 반복 데이터 과학 방법론입니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-104">The Team Data Science Process (TDSP) is an agile, iterative data science methodology to deliver predictive analytics solutions and intelligent applications efficiently.</span></span> <span data-ttu-id="e214c-105">TDSP는 팀 공동 작업 및 학습을 향상하도록 돕습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-105">TDSP helps improve team collaboration and learning.</span></span> <span data-ttu-id="e214c-106">데이터 과학 이니셔티브의 성공적인 구현을 용이하게 하는 산업의 Microsoft 및 기타 업계에서 모범 사례 및 구조의 추출을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-106">It contains a distillation of the best practices and structures from Microsoft and others in the industry that facilitate the successful implementation of data science initiatives.</span></span> <span data-ttu-id="e214c-107">목표는 회사가 해당 분석 프로그램의 이점을 완전히 이해하도록 돕는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-107">The goal is to help companies fully realize the benefits of their analytics program.</span></span>

<span data-ttu-id="e214c-108">이 문서에서는 TDSP 및 주요 구성 요소의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-108">This article provides an overview of TDSP and its main components.</span></span> <span data-ttu-id="e214c-109">다양한 도구와 구현될 수 있는 프로세스의 일반적인 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-109">We provide a generic description of the process here that can be implemented with a variety of tools.</span></span> <span data-ttu-id="e214c-110">프로젝트 작업 및 프로세스의 수명 주기와 관련된 역할의 더 자세한 설명은 추가 연결된 항목에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-110">A more detailed description of the project tasks and roles involved in the lifecycle of the process is provided in additional linked topics.</span></span> <span data-ttu-id="e214c-111">팀에서 TDSP를 구현하는 데 사용하는 Microsoft 도구 및 인프라의 특정 집합을 사용하여 TDSP를 구현하는 방법에 대한 지침도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-111">Guidance on how to implement the TDSP using a specific set of Microsoft tools and infrastructure that we use to implement the TDSP in our teams is also provided.</span></span>

## <a name="key-components-of-the-tdsp"></a><span data-ttu-id="e214c-112">TDSP의 주요 구성 요소</span><span class="sxs-lookup"><span data-stu-id="e214c-112">Key components of the TDSP</span></span>

<span data-ttu-id="e214c-113">TDSP는 다음 주요 구성 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-113">TDSP comprises of the following key components:</span></span>

- <span data-ttu-id="e214c-114">**데이터 과학 수명 주기** 정의</span><span class="sxs-lookup"><span data-stu-id="e214c-114">A **data science lifecycle** definition</span></span>
- <span data-ttu-id="e214c-115">**표준화된 프로젝트 구조**</span><span class="sxs-lookup"><span data-stu-id="e214c-115">A **standardized project structure**</span></span>
- <span data-ttu-id="e214c-116">데이터 과학 프로젝트에 대한 **인프라 및 리소스**</span><span class="sxs-lookup"><span data-stu-id="e214c-116">**Infrastructure and resources** for data science projects</span></span>
- <span data-ttu-id="e214c-117">프로젝트 실행에 대한 **도구 및 유틸리티**</span><span class="sxs-lookup"><span data-stu-id="e214c-117">**Tools and utilities** for project execution</span></span>


## <a name="data-science-lifecycle"></a><span data-ttu-id="e214c-118">데이터 과학 수명 주기</span><span class="sxs-lookup"><span data-stu-id="e214c-118">Data science lifecycle</span></span>

<span data-ttu-id="e214c-119">TDSP(Team Data Science Process)는 데이터 과학 프로젝트의 개발을 구조화하는 수명 주기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-119">The Team Data Science Process (TDSP) provides a lifecycle to structure the development of your data science projects.</span></span> <span data-ttu-id="e214c-120">수명 주기는 일반적으로 프로젝트가 실행될 때 시작부터 끝까지 따라야 하는 단계를 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-120">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span>

<span data-ttu-id="e214c-121">다른 데이터 과학의 수명 주기(예: [CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) 또는 조직의 사용자 지정 프로세스)를 사용하는 경우 개발 수명 주기의 맥락에서 작업 기반 TDSP를 계속 사용할 수 있습니다 .</span><span class="sxs-lookup"><span data-stu-id="e214c-121">If you are using another data science lifecycle, such as [CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) or your organization's own custom process, you can still use the task-based TDSP in the context of those development lifecycles.</span></span> <span data-ttu-id="e214c-122">상위 수준에서 이러한 다양한 방법에는 많은 공통점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-122">At a high level, these different methodologies have much in common.</span></span> 

<span data-ttu-id="e214c-123">이 수명 주기는 지능형 응용 프로그램의 일부로 제공되는 데이터 과학 프로젝트를 위해 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-123">This lifecycle has been designed for data science projects that ship as part of intelligent applications.</span></span> <span data-ttu-id="e214c-124">이러한 응용 프로그램은 예측 분석을 위해 기계 학습 또는 인공 지능 모델을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-124">These applications deploy machine learning or artificial intelligence models for predictive analytics.</span></span> <span data-ttu-id="e214c-125">예비 데이터 과학 프로젝트 또는 임시 분석 프로젝트에서 이 프로세스를 사용하여 활용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-125">Exploratory data science projects or ad hoc analytics projects can also benefit from using this process.</span></span> <span data-ttu-id="e214c-126">하지만 이러한 경우 설명된 몇 가지 단계가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-126">But in such cases some of the steps described may not be needed.</span></span>    

<span data-ttu-id="e214c-127">TDSP 수명 주기는 반복적으로 실행되는 5가지 주요 단계로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-127">The TDSP lifecycle is composed of five major stages that are executed iteratively:</span></span>

* <span data-ttu-id="e214c-128">**비즈니스 이해**</span><span class="sxs-lookup"><span data-stu-id="e214c-128">**Business Understanding**</span></span>
* <span data-ttu-id="e214c-129">**데이터 취득 및 이해**</span><span class="sxs-lookup"><span data-stu-id="e214c-129">**Data Acquisition and Understanding**</span></span>
* <span data-ttu-id="e214c-130">**모델링**</span><span class="sxs-lookup"><span data-stu-id="e214c-130">**Modeling**</span></span>
* <span data-ttu-id="e214c-131">**배포웹사이트를**</span><span class="sxs-lookup"><span data-stu-id="e214c-131">**Deployment**</span></span>
* <span data-ttu-id="e214c-132">**고객 승인**</span><span class="sxs-lookup"><span data-stu-id="e214c-132">**Customer Acceptance**</span></span>

<span data-ttu-id="e214c-133">다음은 **팀 데이터 과학 프로세스 수명 주기**의 시각적 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-133">Here is a visual representation of the **Team Data Science Process lifecycle**.</span></span> 

![TDSP 수명 주기](./media/data-science-process-overview/tdsp-lifecycle.png) 

<span data-ttu-id="e214c-135">TDSP에서 주기의 각 단계에 대한 목표, 작업 및 설명서 아티팩트는 [Team Data Science Process 수명 주기](data-science-process-lifecycle.md) 항목에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-135">The goals, tasks, and documentation artifacts for each stage of the lifecycle in TDSP are described in the [Team Data Science Process lifecycle](data-science-process-lifecycle.md) topic.</span></span> <span data-ttu-id="e214c-136">이러한 작업 및 아티팩트는 프로젝트 역할과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-136">These tasks and artifacts are associated with project roles:</span></span>

- <span data-ttu-id="e214c-137">솔루션 설계자</span><span class="sxs-lookup"><span data-stu-id="e214c-137">Solution architect</span></span>
- <span data-ttu-id="e214c-138">프로젝트 관리자</span><span class="sxs-lookup"><span data-stu-id="e214c-138">Project manager</span></span>
- <span data-ttu-id="e214c-139">데이터 과학자</span><span class="sxs-lookup"><span data-stu-id="e214c-139">Data scientist</span></span>
- <span data-ttu-id="e214c-140">프로젝트 책임자</span><span class="sxs-lookup"><span data-stu-id="e214c-140">Project lead</span></span> 

<span data-ttu-id="e214c-141">다음 다이어그램은 이러한 작업(세로 축)에 대한 수명 주기(가로 축)의 각 역할에 관련된 작업(파란색) 및 아티팩트(녹색)의 그리드 뷰를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-141">The following diagram provides a grid view of the tasks (in blue) and artifacts (in green) associated with each stage of the lifecycle (on the horizontal axis) for these roles (on the vertical axis).</span></span> 

![TDSP 역할 및 작업](./media/data-science-process-overview/tdsp-tasks-by-roles.png)

## <a name="standardized-project-structure"></a><span data-ttu-id="e214c-143">표준화된 프로젝트 구조</span><span class="sxs-lookup"><span data-stu-id="e214c-143">Standardized project structure</span></span>

<span data-ttu-id="e214c-144">모든 프로젝트가 디렉터리 구조를 공유하고 프로젝트의 문서에 대한 템플릿을 사용하면 팀 멤버가 회사 프로젝트에 대한 정보를 쉽게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-144">Having all projects share a directory structure and use templates for project documents makes it easy for the team members to find information about their projects.</span></span> <span data-ttu-id="e214c-145">모든 코드 및 문서는 팀 공동 작업을 활성화하도록 Git, TFS 또는 Subversion과 같은 VCS(버전 제어 시스템)에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-145">All code and documents are stored in a version control system (VCS) like Git, TFS, or Subversion to enable team collaboration.</span></span> <span data-ttu-id="e214c-146">Jira, Rally, Visual Studio Team Services와 같은 기민한 프로젝트 추적 시스템의 추적 작업 및 기능을 통해 개별 기능에 대한 코드를 자세히 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-146">Tracking tasks and features in an agile project tracking system like Jira, Rally, Visual Studio Team Services allows closer tracking of the code for individual features.</span></span> <span data-ttu-id="e214c-147">또한 이러한 추적을 통해 팀은 더 나은 비용 예측을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-147">Such tracking also enables teams to obtain better cost estimates.</span></span> <span data-ttu-id="e214c-148">TDSP는 버전 관리, 정보 보안 및 공동 작업에 대해 VCS에 각 프로젝트에 대한 별도 리포지토리를 만드는 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-148">TDSP recommends creating a separate repository for each project on the VCS for versioning, information security, and collaboration.</span></span> <span data-ttu-id="e214c-149">모든 프로젝트에 대한 표준화된 구조를 통해 조직 전체에 걸쳐 기업 정보를 구축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-149">The standardized structure for all projects helps build institutional knowledge across the organization.</span></span>

<span data-ttu-id="e214c-150">폴더 구조에 대한 템플릿 및 기본 위치에 필요한 문서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-150">We provide templates for the folder structure and required documents in standard locations.</span></span> <span data-ttu-id="e214c-151">이 폴더 구조는 데이터 탐색 및 기능 추출에 대한 코드를 포함하고 모델 반복을 기록하는 파일을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-151">This folder structure organizes the files that contain code for data exploration and feature extraction, and that record model iterations.</span></span> <span data-ttu-id="e214c-152">이러한 템플릿을 통해 팀 멤버는 다른 사용자가 수행한 작업을 이해하고 팀에 새 멤버를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-152">These templates make it easier for team members to understand work done by others and to add new members to teams.</span></span> <span data-ttu-id="e214c-153">마크다운 형식으로 문서 템플릿을 보고 업데이트하는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-153">It is easy to view and update document templates in markdown format.</span></span> <span data-ttu-id="e214c-154">템플릿을 사용하여 문제가 잘 정의되고 결과물이 예상 품질을 충족하도록 각 프로젝트에 대한 주요 질문이 있는 검사 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-154">Use templates to provide checklists with key questions for each project to insure that the problem is well-defined and that deliverables meet the quality expected.</span></span> <span data-ttu-id="e214c-155">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-155">Examples include:</span></span>

- <span data-ttu-id="e214c-156">비즈니스 문제 및 프로젝트의 범위를 문서화하는 프로젝트 헌장</span><span class="sxs-lookup"><span data-stu-id="e214c-156">a project charter to document the business problem and scope of the project</span></span>
- <span data-ttu-id="e214c-157">원시 데이터의 구조 및 통계를 문서화하는 데이터 보고서</span><span class="sxs-lookup"><span data-stu-id="e214c-157">data reports to document the structure and statistics of the raw data</span></span>
- <span data-ttu-id="e214c-158">파생된 기능을 문서화하는 모델 보고서</span><span class="sxs-lookup"><span data-stu-id="e214c-158">model reports to document the derived features</span></span>
- <span data-ttu-id="e214c-159">ROC 곡선 또는 MSE와 같은 모델 성능 메트릭</span><span class="sxs-lookup"><span data-stu-id="e214c-159">model performance metrics such as ROC curves or MSE</span></span>


![TDSP 디렉터리](./media/data-science-process-overview/tdsp-dir-structure.png)

<span data-ttu-id="e214c-161">디렉터리 구조는 [Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate)에서 복제될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-161">The directory structure can be cloned from [Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate).</span></span>

## <a name="infrastructure-and-resources-for-data-science-projects"></a><span data-ttu-id="e214c-162">데이터 과학 프로젝트에 대한 인프라 및 리소스</span><span class="sxs-lookup"><span data-stu-id="e214c-162">Infrastructure and resources for data science projects</span></span>

<span data-ttu-id="e214c-163">TDSP는 다음과 같은 공유 분석 및 저장소 인프라를 관리하기 위한 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-163">TDSP provides recommendations for managing shared analytics and storage infrastructure such as:</span></span>

- <span data-ttu-id="e214c-164">데이터 집합을 저장하기 위한 클라우드 파일 시스템,</span><span class="sxs-lookup"><span data-stu-id="e214c-164">cloud file systems for storing datasets,</span></span> 
- <span data-ttu-id="e214c-165">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="e214c-165">databases</span></span>
- <span data-ttu-id="e214c-166">빅 데이터(Hadoop 또는 Spark) 클러스터</span><span class="sxs-lookup"><span data-stu-id="e214c-166">big data (Hadoop or Spark) clusters</span></span> 
- <span data-ttu-id="e214c-167">기계 학습 서비스</span><span class="sxs-lookup"><span data-stu-id="e214c-167">machine learning services.</span></span> 

<span data-ttu-id="e214c-168">분석 및 저장소 인프라는 클라우드 또는 온-프레미스에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-168">The analytics and storage infrastructure can be in the cloud or on-premises.</span></span> <span data-ttu-id="e214c-169">이는 원시 및 처리된 데이터 집합이 저장되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-169">This is where raw and processed datasets are stored.</span></span> <span data-ttu-id="e214c-170">이 인프라는 재현 가능한 분석을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-170">This infrastructure enables reproducible analysis.</span></span> <span data-ttu-id="e214c-171">또한 불일치 및 불필요한 인프라 비용이 발생할 수 있는 복제를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-171">It also avoids duplication, which can lead to inconsistencies and unnecessary infrastructure costs.</span></span> <span data-ttu-id="e214c-172">도구는 공유 리소스를 프로비전하고, 이를 추적하고, 각 팀 멤버가 해당 리소스에 안전하게 연결할 수 있도록 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-172">Tools are provided to provision the shared resources, track them, and allow each team member to connect to those resources securely.</span></span> <span data-ttu-id="e214c-173">프로젝트 멤버가 일관성 있는 계산 환경을 만들도록 하는 것도 좋은 연습입니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-173">It is also a good practice have project members create a consistent compute environment.</span></span> <span data-ttu-id="e214c-174">그러면 다른 팀 멤버는 실험을 복제하고 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-174">Different team members can then replicate and validate experiments.</span></span>

<span data-ttu-id="e214c-175">여러 프로젝트에서 작업하고 다양한 클라우드 분석 인프라 구성 요소를 공유하는 팀의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-175">Here is an example of a team working on multiple projects and sharing various cloud analytics infrastructure components.</span></span>

![TDSP 인프라](./media/data-science-process-overview/tdsp-analytics-infra.png)


## <a name="tools-and-utilities-for-project-execution"></a><span data-ttu-id="e214c-177">프로젝트 실행에 대한 도구 및 유틸리티</span><span class="sxs-lookup"><span data-stu-id="e214c-177">Tools and utilities for project execution</span></span>

<span data-ttu-id="e214c-178">대부분의 조직에서 프로세스를 소개하는 것은 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-178">Introducing processes in most organizations is challenging.</span></span> <span data-ttu-id="e214c-179">데이터 과학 프로세스 및 수명 주기 구현을 위해 제공된 도구는 장벽을 낮추고 해당 도입의 일관성을 증가시키도록 돕습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-179">Tools provided to implement the data science process and lifecycle help lower the barriers to and increase the consistency of their adoption.</span></span> <span data-ttu-id="e214c-180">TDSP는 팀 내에서 TDSP의 도입을 신속하게 시작하도록 초기 도구 집합 및 스크립트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-180">TDSP provides an initial set of tools and scripts to jump-start adoption of TDSP within a team.</span></span> <span data-ttu-id="e214c-181">또한 데이터 탐색 및 기준 모델링과 같은 데이터 과학 수명 주기의 일부 일반적인 작업을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-181">It also helps automate some of the common tasks in the data science lifecycle such as data exploration and baseline modeling.</span></span> <span data-ttu-id="e214c-182">공유 도구 및 유틸리티를 팀의 공유 코드 리포지토리에 기여하도록 개인에 대해 제공되는 잘 정의된 구조가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-182">There is a well-defined structure provided for individuals to contribute shared tools and utilities into their team’s shared code repository.</span></span> <span data-ttu-id="e214c-183">그러면 이러한 리소스는 팀 또는 조직 내의 다른 프로젝트에서 활용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-183">These resources can then be leveraged by other projects within the team or the organization.</span></span> <span data-ttu-id="e214c-184">또한 TDSP는 전체 커뮤니티에 대한 도구 및 유틸리티의 기여를 활성화하도록 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-184">TDSP also plans to enable the contributions of tools and utilities to the whole community.</span></span> <span data-ttu-id="e214c-185">TDSP 유틸리티는 [Github](https://github.com/Azure/Azure-TDSP-Utilities)에서 복제될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-185">The TDSP utilities can be cloned from [Github](https://github.com/Azure/Azure-TDSP-Utilities).</span></span>


## <a name="next-steps"></a><span data-ttu-id="e214c-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e214c-186">Next steps</span></span>

<span data-ttu-id="e214c-187">[Team Data Science Process: 역할 및 작업](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md) 이 프로세스를 표준화하는 데이터 과학 팀에 대한 핵심 인력 역할 및 관련된 작업에 대해 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e214c-187">[Team Data Science Process: Roles and tasks](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md) Outlines the key personnel roles and their associated tasks for a data science team that standardizes on this process.</span></span> 
