---
title: "Azure 기계 학습에 대 한 고급 분석 시나리오 aaaIdentify | Microsoft Docs"
description: "이렇게 하면 고급 팀 데이터 과학 프로세스 hello로 예측 분석에 대 한 hello 적절 한 시나리오를 선택 합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="03435-103">Azure 기계 학습의 고급 분석 시나리오</span><span class="sxs-lookup"><span data-stu-id="03435-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="03435-104">이 문서에서는 hello 다양 한 예제 데이터 원본 및 hello에서 처리 될 수 있는 대상 시나리오를 설명 [팀 데이터 과학 프로세스 (TDSP)](data-science-process-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-104">This article outlines hello variety of sample data sources and target scenarios that can be handled by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="03435-105">hello TDSP 팀 toocollaborate 지능형 응용 프로그램을 구축에 대 한 체계적인 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-105">hello TDSP provides a systematic approach for teams toocollaborate on building intelligent applications.</span></span> <span data-ttu-id="03435-106">여기에 제시 된 hello 시나리오 hello 데이터 특징별, 소스 위치 및 Azure에서 대상 저장소에 종속 된 hello 데이터 처리 워크플로에서 사용할 수 있는 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="03435-106">hello scenarios presented here illustrate options available in hello data processing workflow that depend on hello data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="03435-107">hello **의사 결정 트리** hello 마지막 섹션에 표시 된 데이터와 목표에 적합 한 hello 샘플 시나리오를 선택 하면에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-107">hello **decision tree** for selecting hello sample scenarios that is appropriate for your data and objective is presented in hello last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="03435-108">각각 hello 다음 섹션의 예제 시나리오를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-108">Each of hello following sections presents a sample scenario.</span></span> <span data-ttu-id="03435-109">각 시나리오에 대해 가능한 데이터 과학 또는 고급 분석 흐름 및 지원되는 Azure 리소스가 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03435-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="03435-110">**모든 hello 다음 시나리오에 대 한 해야 합니다.**
> </span><span class="sxs-lookup"><span data-stu-id="03435-110">**For all of hello following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="03435-111">[저장소 계정 만들기](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="03435-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="03435-112">Azure 기계 학습 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="03435-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="03435-113"><a name="smalllocal"></a>시나리오 \#1: 로컬 파일에 작은 toomedium 표 형식 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="03435-113"><a name="smalllocal"></a>Scenario \#1: Small toomedium tabular dataset in a local files</span></span>
![작은 toomedium 로컬 파일][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="03435-115">추가 Azure 리소스: 없음</span><span class="sxs-lookup"><span data-stu-id="03435-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="03435-116">Toohello 로그인 [Azure 기계 학습 스튜디오](https://studio.azureml.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-116">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="03435-117">데이터 집합을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-117">Upload a dataset.</span></span>
3. <span data-ttu-id="03435-118">데이터 집합을 업로드한 Azure 컴퓨터 학습 실험 흐름을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="03435-119"><a name="smalllocalprocess"></a>시나리오 \#2: 처리를 필요로 하는 로컬 파일의 작은 toomedium 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="03435-119"><a name="smalllocalprocess"></a>Scenario \#2: Small toomedium dataset of local files that require processing</span></span>
![처리를 사용 하 여 작은 toomedium 로컬 파일][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="03435-121">추가 Azure 리소스: Azure 가상 컴퓨터 (IPython Notebook 서버)</span><span class="sxs-lookup"><span data-stu-id="03435-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="03435-122">IPython Notebook을 실행하는 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="03435-123">데이터 tooan Azure storage 컨테이너를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-123">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="03435-124">IPython Notebook에서 데이터를 사전 처리하고 정리하며, Azure 저장소 컨테이너에서 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="03435-125">테이블 형식, 데이터 toocleaned를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-125">Transform data toocleaned, tabular form.</span></span>
5. <span data-ttu-id="03435-126">Azure Blob에 변환된 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="03435-127">Toohello 로그인 [Azure 기계 학습 스튜디오](https://studio.azureml.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-127">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="03435-128">Hello를 사용 하 여 Azure blob에서 hello 데이터 읽기 [데이터 가져오기] [ import-data] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="03435-128">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="03435-129">수집된 데이터 집합으로 시작하여 Azure 컴퓨터 학습 실험 흐름을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="03435-130"><a name="largelocal"></a>시나리오 \#3: 로컬 파일에서 큰 데이터 집합, Azure Blob을 대상으로 함</span><span class="sxs-lookup"><span data-stu-id="03435-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![큰 로컬 파일][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="03435-132">추가 Azure 리소스: Azure 가상 컴퓨터 (IPython Notebook 서버)</span><span class="sxs-lookup"><span data-stu-id="03435-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="03435-133">IPython Notebook을 실행하는 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="03435-134">데이터 tooan Azure storage 컨테이너를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-134">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="03435-135">IPython Notebook에서 데이터를 사전 처리하고 정리하며, Azure Blob에서 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="03435-136">필요한 경우 데이터 toocleaned, 테이블 형식 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-136">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="03435-137">데이터를 탐색하고 필요에 따라 기능을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="03435-138">중소 데이터 샘플을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="03435-139">Azure blob에 hello 샘플링 된 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-139">Save hello sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="03435-140">Toohello 로그인 [Azure 기계 학습 스튜디오](https://studio.azureml.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-140">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="03435-141">Hello를 사용 하 여 Azure blob에서 hello 데이터 읽기 [데이터 가져오기] [ import-data] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="03435-141">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="03435-142">수집된 데이터 집합으로 시작하여 Azure 컴퓨터 학습 실험 흐름을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="03435-143"><a name="smalllocaltodb"></a>시나리오 \#4: Azure 가상 컴퓨터에서 SQL Server를 대상으로 하는 로컬 파일의 작은 toomedium 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="03435-143"><a name="smalllocaltodb"></a>Scenario \#4: Small toomedium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Azure에서 작은 toomedium 로컬 파일 tooSQL DB][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="03435-145">추가 Azure 리소스: Azure 가상 컴퓨터 (SQL Server / IPython Notebook 서버)</span><span class="sxs-lookup"><span data-stu-id="03435-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="03435-146">SQL Server + IPython Notebook을 실행하는 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="03435-147">데이터 tooan Azure storage 컨테이너를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-147">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="03435-148">IPython Notebook을 사용하여 Azure 저장소 컨테이너에서 데이터를 사전 처리하고 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="03435-149">필요한 경우 데이터 toocleaned, 테이블 형식 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-149">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="03435-150">데이터 tooVM 로컬 파일 저장 (IPython 노트북 VM에서 실행 되 고, 로컬 드라이브 tooVM 드라이브 참조).</span><span class="sxs-lookup"><span data-stu-id="03435-150">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
6. <span data-ttu-id="03435-151">Azure VM에서 실행 되는 데이터 tooSQL 서버 데이터베이스를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-151">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="03435-152">옵션 \#1: SQL Server Management Studio 사용.</span><span class="sxs-lookup"><span data-stu-id="03435-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="03435-153">로그인 tooSQL 서버 VM</span><span class="sxs-lookup"><span data-stu-id="03435-153">Login tooSQL Server VM</span></span>
   * <span data-ttu-id="03435-154">SQL Server Management Studio를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="03435-155">데이터베이스 및 대상 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-155">Create database and target tables.</span></span>
   * <span data-ttu-id="03435-156">VM-로컬 파일에서 메서드 tooload hello 데이터를 가져오기 하는 hello 대량 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-156">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
   
   <span data-ttu-id="03435-157">옵션 \#2: IPython Notebook 사용 – 중간 및 대규모 데이터 집합을 권장하지 않음</span><span class="sxs-lookup"><span data-stu-id="03435-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="03435-158">ODBC 연결 문자열 tooaccess SQL Server VM에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-158">Use ODBC connection string tooaccess SQL Server on VM.</span></span>
   * <span data-ttu-id="03435-159">데이터베이스 및 대상 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-159">Create database and target tables.</span></span>
   * <span data-ttu-id="03435-160">VM-로컬 파일에서 메서드 tooload hello 데이터를 가져오기 하는 hello 대량 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-160">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
7. <span data-ttu-id="03435-161">데이터를 탐색하고 필요에 따라 기능을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-161">Explore data, create features as needed.</span></span> <span data-ttu-id="03435-162">참고 hello 기능 toobe hello 데이터베이스 테이블에서 구체화 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03435-162">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="03435-163">Hello 필요한 쿼리 toocreate을 확인만 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-163">Only note hello necessary query toocreate them.</span></span>
8. <span data-ttu-id="03435-164">필요하거나 원하는 경우 데이터 샘플 크기를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="03435-165">Toohello 로그인 [Azure 기계 학습 스튜디오](https://studio.azureml.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-165">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="03435-166">읽기 hello 데이터 직접에서 hello hello를 사용 하 여 SQL Server [데이터 가져오기] [ import-data] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="03435-166">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="03435-167">필드를 추출 하는 붙여넣기 hello 필요한 쿼리 기능을 만들고 직접 hello에에서 필요한 경우 데이터를 샘플링 [데이터 가져오기] [ import-data] 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-167">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="03435-168">수집된 데이터 집합으로 시작하여 Azure 컴퓨터 학습 실험 흐름을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="03435-169"><a name="largelocaltodb"></a>시나리오 \#5: 로컬 파일의 큰 데이터 집합, Azure VM의 SQL Server를 대상으로 함</span><span class="sxs-lookup"><span data-stu-id="03435-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![Azure의 큰 로컬 파일 tooSQL DB][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="03435-171">추가 Azure 리소스: Azure 가상 컴퓨터 (SQL Server / IPython Notebook 서버)</span><span class="sxs-lookup"><span data-stu-id="03435-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="03435-172">SQL Server 및 IPython Notebook 서버를 실행하는 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="03435-173">데이터 tooan Azure storage 컨테이너를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-173">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="03435-174">(선택 사항) 데이터를 사전 처리하고 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="03435-175">a.</span><span class="sxs-lookup"><span data-stu-id="03435-175">a.</span></span>  <span data-ttu-id="03435-176">IPython Notebook에서 데이터를 사전 처리하고 정리하며, Azure에서 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="03435-177">b.</span><span class="sxs-lookup"><span data-stu-id="03435-177">b.</span></span>  <span data-ttu-id="03435-178">필요한 경우 데이터 toocleaned, 테이블 형식 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-178">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="03435-179">c.</span><span class="sxs-lookup"><span data-stu-id="03435-179">c.</span></span>  <span data-ttu-id="03435-180">데이터 tooVM 로컬 파일 저장 (IPython 노트북 VM에서 실행 되 고, 로컬 드라이브 tooVM 드라이브 참조).</span><span class="sxs-lookup"><span data-stu-id="03435-180">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="03435-181">Azure VM에서 실행 되는 데이터 tooSQL 서버 데이터베이스를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-181">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="03435-182">a.</span><span class="sxs-lookup"><span data-stu-id="03435-182">a.</span></span>  <span data-ttu-id="03435-183">로그인 tooSQL 서버 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="03435-183">Login tooSQL Server VM.</span></span>
   
   <span data-ttu-id="03435-184">b.</span><span class="sxs-lookup"><span data-stu-id="03435-184">b.</span></span>  <span data-ttu-id="03435-185">데이터를 저장하지 경우, Azure에서 데이터 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-185">If data not saved already, download data files from Azure</span></span>
   
       storage container toolocal-VM folder.
   
   <span data-ttu-id="03435-186">c.</span><span class="sxs-lookup"><span data-stu-id="03435-186">c.</span></span>  <span data-ttu-id="03435-187">SQL Server Management Studio를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="03435-188">d.</span><span class="sxs-lookup"><span data-stu-id="03435-188">d.</span></span>  <span data-ttu-id="03435-189">데이터베이스 및 대상 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="03435-190">e.</span><span class="sxs-lookup"><span data-stu-id="03435-190">e.</span></span>  <span data-ttu-id="03435-191">Hello 대량 중 하나를 사용 방법을 tooload hello 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="03435-191">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="03435-192">f.</span><span class="sxs-lookup"><span data-stu-id="03435-192">f.</span></span>  <span data-ttu-id="03435-193">테이블 조인에 필요한 경우 인덱스 tooexpedite 조인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-193">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="03435-194">큰 데이터 크기의 더 빠른 로드에 대 한 분할 된 테이블 만들고 hello 데이터 병렬로 대량 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="03435-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import hello data in parallel.</span></span> <span data-ttu-id="03435-195">자세한 내용은 참조 [병렬 데이터 가져오기 tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-195">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="03435-196">데이터를 탐색하고 필요에 따라 기능을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-196">Explore data, create features as needed.</span></span> <span data-ttu-id="03435-197">참고 hello 기능 toobe hello 데이터베이스 테이블에서 구체화 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03435-197">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="03435-198">Hello 필요한 쿼리 toocreate을 확인만 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-198">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="03435-199">필요하거나 원하는 경우 데이터 샘플 크기를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="03435-200">Toohello 로그인 [Azure 기계 학습 스튜디오](https://studio.azureml.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-200">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="03435-201">읽기 hello 데이터 직접에서 hello hello를 사용 하 여 SQL Server [데이터 가져오기] [ import-data] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="03435-201">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="03435-202">필드를 추출 하는 붙여넣기 hello 필요한 쿼리 기능을 만들고 직접 hello에에서 필요한 경우 데이터를 샘플링 [데이터 가져오기] [ import-data] 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-202">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="03435-203">업로드 데이터 집합으로 단순 Azure 기계 학습 실험 흐름 시작</span><span class="sxs-lookup"><span data-stu-id="03435-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="03435-204"><a name="largedbtodb"></a>시나리오 \#6: 온-프레미스의 SQL 서버 데이터베이스의 큰 데이터 집합, Azure 가상 컴퓨터의 SQL Server를 대상으로 함</span><span class="sxs-lookup"><span data-stu-id="03435-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![대형 SQL DB 온-프레미스 tooSQL DB Azure에서][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="03435-206">추가 Azure 리소스: Azure 가상 컴퓨터 (SQL Server / IPython Notebook 서버)</span><span class="sxs-lookup"><span data-stu-id="03435-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="03435-207">SQL Server 및 IPython Notebook 서버를 실행하는 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="03435-208">Hello 데이터 중 하나 사용 하 여 SQL Server toodump 파일에서 메서드 tooexport hello 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="03435-208">Use one of hello data export methods tooexport hello data from SQL Server toodump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="03435-209">대체 (빠른) 메서드 toomove hello 전체 데이터베이스 toothe SQL Server 인스턴스로 Azure의 hello 온-프레미스 데이터베이스에서 모든 데이터 toomove를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-209">If you decide toomove all data from hello on-prem database, an alternate (faster) method toomove hello full database toothe SQL Server instance in Azure.</span></span> <span data-ttu-id="03435-210">Hello 단계 tooexport 데이터, 데이터베이스 및 부하/가져오기 데이터 toohello 대상 데이터베이스 만들기를 건너뛰고 hello 대체 방법에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-210">Skip hello steps tooexport data, create database, and load/import data toohello target database and follow hello alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="03435-211">덤프 파일 tooAzure 저장소 컨테이너를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-211">Upload dump files tooAzure storage container.</span></span>
4. <span data-ttu-id="03435-212">Azure 가상 컴퓨터에서 실행 하는 hello 데이터 tooa SQL Server 데이터베이스를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-212">Load hello data tooa SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="03435-213">a.</span><span class="sxs-lookup"><span data-stu-id="03435-213">a.</span></span>  <span data-ttu-id="03435-214">SQL Server VM toohello를 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-214">Login toohello SQL Server VM.</span></span>
   
   <span data-ttu-id="03435-215">b.</span><span class="sxs-lookup"><span data-stu-id="03435-215">b.</span></span>  <span data-ttu-id="03435-216">Azure 저장소 컨테이너 toohello VM 로컬 폴더에서 데이터 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-216">Download data files from an Azure storage container toohello local-VM folder.</span></span>
   
   <span data-ttu-id="03435-217">c.</span><span class="sxs-lookup"><span data-stu-id="03435-217">c.</span></span>  <span data-ttu-id="03435-218">SQL Server Management Studio를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="03435-219">d.</span><span class="sxs-lookup"><span data-stu-id="03435-219">d.</span></span>  <span data-ttu-id="03435-220">데이터베이스 및 대상 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="03435-221">e.</span><span class="sxs-lookup"><span data-stu-id="03435-221">e.</span></span>  <span data-ttu-id="03435-222">Hello 대량 중 하나를 사용 방법을 tooload hello 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="03435-222">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="03435-223">f.</span><span class="sxs-lookup"><span data-stu-id="03435-223">f.</span></span>  <span data-ttu-id="03435-224">테이블 조인에 필요한 경우 인덱스 tooexpedite 조인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-224">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="03435-225">큰 데이터 크기의 더 빠른 로드에 대 한 동시에 분할 된 테이블 및 toobulk 가져오기 hello 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-225">For faster loading of large data sizes, create partitioned tables and toobulk import hello data in parallel.</span></span> <span data-ttu-id="03435-226">자세한 내용은 참조 [병렬 데이터 가져오기 tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-226">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="03435-227">데이터를 탐색하고 필요에 따라 기능을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-227">Explore data, create features as needed.</span></span> <span data-ttu-id="03435-228">참고 hello 기능 toobe hello 데이터베이스 테이블에서 구체화 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03435-228">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="03435-229">Hello 필요한 쿼리 toocreate을 확인만 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-229">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="03435-230">필요하거나 원하는 경우 데이터 샘플 크기를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="03435-231">Toohello 로그인 [Azure 기계 학습 스튜디오](https://studio.azureml.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-231">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="03435-232">읽기 hello 데이터 직접에서 hello hello를 사용 하 여 SQL Server [데이터 가져오기] [ import-data] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="03435-232">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="03435-233">필드를 추출 하는 붙여넣기 hello 필요한 쿼리 기능을 만들고 직접 hello에에서 필요한 경우 데이터를 샘플링 [데이터 가져오기] [ import-data] 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-233">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="03435-234">업로드 데이터 집합으로 단순 Azure 기계 학습 실험 흐름 시작</span><span class="sxs-lookup"><span data-stu-id="03435-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a><span data-ttu-id="03435-235">대체 방법 toocopy 온-프레미스 SQL Server tooAzure SQL 데이터베이스에서에서 전체 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="03435-235">Alternate method toocopy a full database from an on-premises  SQL Server tooAzure SQL Database</span></span>
![Local DB를 분리 하 고 Azure에서 DB tooSQL 연결][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="03435-237">추가 Azure 리소스: Azure 가상 컴퓨터 (SQL Server / IPython Notebook 서버)</span><span class="sxs-lookup"><span data-stu-id="03435-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="03435-238">tooreplicate hello 전체 SQL Server 데이터베이스의 SQL Server VM을 복사 해야 데이터베이스에서 한 위치/서버 tooanother 해당 hello 데이터베이스를 일시적으로 오프 라인 수 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-238">tooreplicate hello entire SQL Server database in your SQL Server VM, you should copy a database from one location/server tooanother, assuming that hello database can be taken temporarily offline.</span></span> <span data-ttu-id="03435-239">SQL Server Management Studio 개체 탐색기 hello 또는 hello 동등한 TRANSACT-SQL 명령을 사용 하 여이 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-239">You do this in hello SQL Server Management Studio Object Explorer, or using hello equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="03435-240">Hello 원본 위치에서 hello 데이터베이스를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-240">Detach hello database at hello source location.</span></span> <span data-ttu-id="03435-241">자세한 내용은 [데이터베이스 분리](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03435-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="03435-242">Windows 탐색기나 Windows 명령 프롬프트 창에서 복사 hello 데이터베이스 파일 및 로그 파일을 Azure에서 SQL Server VM hello 파일 toohello 대상 위치를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-242">In Windows Explorer or Windows Command Prompt window, copy hello detached database file or files and log file or files toohello target location on hello SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="03435-243">복사 하는 hello 파일 toohello 대상 SQL Server 인스턴스에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-243">Attach hello copied files toohello target SQL Server instance.</span></span> <span data-ttu-id="03435-244">자세한 내용은 [데이터베이스 연결](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="03435-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="03435-245">[분리 및 연결을 사용하여 데이터베이스 이동(Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="03435-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="03435-246"><a name="largedbtohive"></a>시나리오 \#7: 로컬 파일의 빅 데이터, Azure HDInsight Hadoop 클러스터의 Hive 데이터베이스를 대상으로 함</span><span class="sxs-lookup"><span data-stu-id="03435-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![로컬 대상 Hive의 빅 데이터][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="03435-248">추가 Azure 리소스: Azure HDInsight Hadoop 클러스터 및 Azure Virtual Machine(IPython Notebook 서버)</span><span class="sxs-lookup"><span data-stu-id="03435-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="03435-249">IPython Notebook 서버를 실행하는 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="03435-250">Azure HDInsight Hadoop 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="03435-251">(선택 사항) 데이터를 사전 처리하고 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="03435-252">a.</span><span class="sxs-lookup"><span data-stu-id="03435-252">a.</span></span>  <span data-ttu-id="03435-253">IPython Notebook에서 데이터를 사전 처리하고 정리하며, Azure에서 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="03435-254">b.</span><span class="sxs-lookup"><span data-stu-id="03435-254">b.</span></span>  <span data-ttu-id="03435-255">필요한 경우 데이터 toocleaned, 테이블 형식 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-255">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="03435-256">c.</span><span class="sxs-lookup"><span data-stu-id="03435-256">c.</span></span>  <span data-ttu-id="03435-257">데이터 tooVM 로컬 파일 저장 (IPython 노트북 VM에서 실행 되 고, 로컬 드라이브 tooVM 드라이브 참조).</span><span class="sxs-lookup"><span data-stu-id="03435-257">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="03435-258">Hello 2 단계에서 선택한 hello Hadoop 클러스터의 데이터 toohello 기본 컨테이너를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-258">Upload data toohello default container of hello Hadoop cluster selected in hello step 2.</span></span>
5. <span data-ttu-id="03435-259">Azure HDInsight Hadoop 클러스터에서 데이터 tooHive 데이터베이스를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-259">Load data tooHive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="03435-260">a.</span><span class="sxs-lookup"><span data-stu-id="03435-260">a.</span></span>  <span data-ttu-id="03435-261">Hello Hadoop 클러스터의 헤드 노드 toohello 로그인</span><span class="sxs-lookup"><span data-stu-id="03435-261">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="03435-262">b.</span><span class="sxs-lookup"><span data-stu-id="03435-262">b.</span></span>  <span data-ttu-id="03435-263">Hadoop 명령줄 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="03435-263">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="03435-264">c.</span><span class="sxs-lookup"><span data-stu-id="03435-264">c.</span></span>  <span data-ttu-id="03435-265">명령에 의해 hello Hive 루트 디렉터리를 입력 `cd %hive_home%\bin` 에서 Hadoop 명령줄입니다.</span><span class="sxs-lookup"><span data-stu-id="03435-265">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="03435-266">d.</span><span class="sxs-lookup"><span data-stu-id="03435-266">d.</span></span>  <span data-ttu-id="03435-267">Hello 하이브 쿼리 toocreate 데이터베이스 및 테이블을 실행 하 고 blob 저장소 tooHive 테이블에서 데이터를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-267">Run hello Hive queries toocreate database and tables, and load data from blob storage tooHive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="03435-268">Hello 데이터 크기가 크면 사용자 파티션이 있는 hello Hive 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03435-268">If hello data is big, users can create hello Hive table with partitions.</span></span> <span data-ttu-id="03435-269">그런 다음, 사용자가 사용할 수는 `for` hello 하이브 테이블 파티션에 의해 분할에 헤드 노드 tooload 데이터 hello에 hello Hadoop 명령줄에서에서 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="03435-269">Then, users can use a `for` loop in hello Hadoop Command Line on hello head node tooload data into hello Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="03435-270">Hadoop 명령줄에서 데이터를 탐색하고 필요에 따라 기능을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="03435-271">참고 hello 기능 toobe hello 데이터베이스 테이블에서 구체화 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03435-271">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="03435-272">Hello 필요한 쿼리 toocreate을 확인만 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-272">Only note hello necessary query toocreate them.</span></span>
   
   <span data-ttu-id="03435-273">a.</span><span class="sxs-lookup"><span data-stu-id="03435-273">a.</span></span>  <span data-ttu-id="03435-274">Hello Hadoop 클러스터의 헤드 노드 toohello 로그인</span><span class="sxs-lookup"><span data-stu-id="03435-274">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="03435-275">b.</span><span class="sxs-lookup"><span data-stu-id="03435-275">b.</span></span>  <span data-ttu-id="03435-276">Hadoop 명령줄 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="03435-276">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="03435-277">c.</span><span class="sxs-lookup"><span data-stu-id="03435-277">c.</span></span>  <span data-ttu-id="03435-278">명령에 의해 hello Hive 루트 디렉터리를 입력 `cd %hive_home%\bin` 에서 Hadoop 명령줄입니다.</span><span class="sxs-lookup"><span data-stu-id="03435-278">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="03435-279">d.</span><span class="sxs-lookup"><span data-stu-id="03435-279">d.</span></span>  <span data-ttu-id="03435-280">Hello Hadoop 클러스터 tooexplore hello 데이터의 hello 헤드 노드에서 hello 하이브 쿼리 Hadoop 명령 줄에서 실행 하 고 필요에 따라 기능을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="03435-280">Run hello Hive queries in Hadoop Command Line on hello head node of hello Hadoop cluster tooexplore hello data and create features as needed.</span></span>
7. <span data-ttu-id="03435-281">필요한 경우 원하는, Azure 기계 학습 스튜디오에서 데이터 toofit hello 샘플.</span><span class="sxs-lookup"><span data-stu-id="03435-281">If needed and/or desired, sample hello data toofit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="03435-282">Toohello 로그인 [Azure 기계 학습 스튜디오](https://studio.azureml.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-282">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="03435-283">Hello에서 직접 hello 데이터를 읽는 `Hive Queries` hello를 사용 하 여 [데이터 가져오기] [ import-data] 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="03435-283">Read hello data directly from hello `Hive Queries` using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="03435-284">필드를 추출 하는 붙여넣기 hello 필요한 쿼리 기능을 만들고 직접 hello에에서 필요한 경우 데이터를 샘플링 [데이터 가져오기] [ import-data] 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-284">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="03435-285">업로드 데이터 집합으로 단순 Azure 기계 학습 실험 흐름 시작</span><span class="sxs-lookup"><span data-stu-id="03435-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="03435-286"><a name="decisiontree"></a>시나리오 선택 의사 결정 트리</span><span class="sxs-lookup"><span data-stu-id="03435-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="03435-287">hello 다음 다이어그램 위에서 설명한 hello 시나리오 및 요약 hello 고급 분석 프로세스 및 기술 선택한 내용을 tooeach 항목별로 hello 시나리오를 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="03435-287">hello following diagram summarizes hello scenarios described above and hello Advanced Analytics Process and Technology choices made that take you tooeach of hello itemized scenarios.</span></span> <span data-ttu-id="03435-288">데이터 처리, 탐색, 기능 엔지니어링 및 샘플링 걸릴 수 있습니다는 하나 또는 중간 hello 소스에서 / 환경-메서드 및/또는 더 – 대상 환경에 배치한 필요에 따라 반복적으로 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03435-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at hello source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="03435-289">만 hello 다이어그램 일부 가능한 흐름을 사용 하 게 되 고 철저 한 열거형을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="03435-289">hello diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![샘플 DS 프로세스 연습 시나리오][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="03435-291">고급 분석 작동 예제</span><span class="sxs-lookup"><span data-stu-id="03435-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="03435-292">사용 하는 종단 간 Azure 기계 학습 연습에 대 한 hello 고급 분석 프로세스 및 기술 공용 데이터 집합을 사용 하 여 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="03435-292">For end-to-end Azure Machine Learning walkthroughs that employ hello Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="03435-293">[실행 중인 팀 데이터 과학 프로세스: SQL Server 사용](machine-learning-data-science-process-sql-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="03435-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="03435-294">[실행 중인 팀 데이터 과학 프로세스: HDInsight Hadoop 클러스터 사용](machine-learning-data-science-process-hive-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="03435-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
