---
title: "Azure Machine Learning을 위한 고급 분석 시나리오 확인 | Microsoft Docs"
description: "팀 데이터 과학 프로세스에서 고급 예측 분석을 수행하기 위한 적절한 시나리오를 선택합니다."
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
ms.openlocfilehash: fe4f74f2e0602d13eedb6ca186480291a9a5724f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="c3640-103">Azure 기계 학습의 고급 분석 시나리오</span><span class="sxs-lookup"><span data-stu-id="c3640-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="c3640-104">이 문서에서는 [TDSP(팀 데이터 과학 프로세스)](data-science-process-overview.md)로 처리할 수 있는 다양한 샘플 데이터 원본 및 대상 시나리오를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-104">This article outlines the variety of sample data sources and target scenarios that can be handled by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="c3640-105">TDSP는 지능형 응용 프로그램 개발을 위해 팀원들이 공동으로 작업하기 위한 체계적인 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-105">The TDSP provides a systematic approach for teams to collaborate on building intelligent applications.</span></span> <span data-ttu-id="c3640-106">여기에 제시된 시나리오는 Azure에서 데이터 특성, 원본 위치 및 대상 저장소를 기반으로 하는 데이터 처리 워크플로에서 사용 가능한 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-106">The scenarios presented here illustrate options available in the data processing workflow that depend on the data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="c3640-107">마지막 섹션에서는 데이터 및 목표에 적합한 샘플 시나리오를 선택하는 **의사 결정 트리** 를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-107">The **decision tree** for selecting the sample scenarios that is appropriate for your data and objective is presented in the last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="c3640-108">다음 섹션에서는 각각 샘플 시나리오를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-108">Each of the following sections presents a sample scenario.</span></span> <span data-ttu-id="c3640-109">각 시나리오에 대해 가능한 데이터 과학 또는 고급 분석 흐름 및 지원되는 Azure 리소스가 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="c3640-110">**이 모든 시나리오에서 다음을 수행해야 합니다.**
> </span><span class="sxs-lookup"><span data-stu-id="c3640-110">**For all of the following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="c3640-111">[저장소 계정 만들기](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="c3640-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="c3640-112">Azure 기계 학습 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="c3640-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="c3640-113"><a name="smalllocal"></a>시나리오 \#1: 로컬 파일에서 중간 테이블 형식 데이터 집합보다 작음</span><span class="sxs-lookup"><span data-stu-id="c3640-113"><a name="smalllocal"></a>Scenario \#1: Small to medium tabular dataset in a local files</span></span>
![보통 로컬 파일보다 작음][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="c3640-115">추가 Azure 리소스: 없음</span><span class="sxs-lookup"><span data-stu-id="c3640-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="c3640-116">[Azure 컴퓨터 학습 Studio](https://studio.azureml.net/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-116">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="c3640-117">데이터 집합을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-117">Upload a dataset.</span></span>
3. <span data-ttu-id="c3640-118">데이터 집합을 업로드한 Azure 컴퓨터 학습 실험 흐름을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="c3640-119"><a name="smalllocalprocess"></a>시나리오 \#2: 처리를 요구하는 로컬 파일의 보통 데이터 집합보다 작음</span><span class="sxs-lookup"><span data-stu-id="c3640-119"><a name="smalllocalprocess"></a>Scenario \#2: Small to medium dataset of local files that require processing</span></span>
![처리 중인 중간 로컬 파일보다 작음][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="c3640-121">추가 Azure 리소스: Azure 가상 컴퓨터 (IPython Notebook 서버)</span><span class="sxs-lookup"><span data-stu-id="c3640-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="c3640-122">IPython Notebook을 실행하는 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="c3640-123">Azure 저장소 컨테이너에 데이터를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-123">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="c3640-124">IPython Notebook에서 데이터를 사전 처리하고 정리하며, Azure 저장소 컨테이너에서 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="c3640-125">데이터를 정리된 테이블 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-125">Transform data to cleaned, tabular form.</span></span>
5. <span data-ttu-id="c3640-126">Azure Blob에 변환된 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="c3640-127">[Azure 컴퓨터 학습 Studio](https://studio.azureml.net/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-127">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="c3640-128">[데이터 가져오기][import-data] 모듈을 사용하여 Azure Blob에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-128">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="c3640-129">수집된 데이터 집합으로 시작하여 Azure 컴퓨터 학습 실험 흐름을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="c3640-130"><a name="largelocal"></a>시나리오 \#3: 로컬 파일에서 큰 데이터 집합, Azure Blob을 대상으로 함</span><span class="sxs-lookup"><span data-stu-id="c3640-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![큰 로컬 파일][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="c3640-132">추가 Azure 리소스: Azure 가상 컴퓨터 (IPython Notebook 서버)</span><span class="sxs-lookup"><span data-stu-id="c3640-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="c3640-133">IPython Notebook을 실행하는 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="c3640-134">Azure 저장소 컨테이너에 데이터를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-134">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="c3640-135">IPython Notebook에서 데이터를 사전 처리하고 정리하며, Azure Blob에서 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="c3640-136">필요한 경우, 데이터를 정리된 테이블 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-136">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="c3640-137">데이터를 탐색하고 필요에 따라 기능을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="c3640-138">중소 데이터 샘플을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="c3640-139">Azure Blob에 샘플링된 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-139">Save the sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="c3640-140">[Azure 컴퓨터 학습 Studio](https://studio.azureml.net/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-140">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="c3640-141">[데이터 가져오기][import-data] 모듈을 사용하여 Azure Blob에서 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-141">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="c3640-142">수집된 데이터 집합으로 시작하여 Azure 컴퓨터 학습 실험 흐름을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="c3640-143"><a name="smalllocaltodb"></a>시나리오 \#4: 로컬 파일의 보통 데이터 집합보다 작음, Azure 가상 컴퓨터의 SQL Server를 대상으로 함</span><span class="sxs-lookup"><span data-stu-id="c3640-143"><a name="smalllocaltodb"></a>Scenario \#4: Small to medium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Azure에서 SQL DB보다 중간인 로컬 파일보다 작음][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="c3640-145">추가 Azure 리소스: Azure 가상 컴퓨터 (SQL Server / IPython Notebook 서버)</span><span class="sxs-lookup"><span data-stu-id="c3640-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="c3640-146">SQL Server + IPython Notebook을 실행하는 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="c3640-147">Azure 저장소 컨테이너에 데이터를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-147">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="c3640-148">IPython Notebook을 사용하여 Azure 저장소 컨테이너에서 데이터를 사전 처리하고 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="c3640-149">필요한 경우, 데이터를 정리된 테이블 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-149">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="c3640-150">VM 로컬 파일에 데이터 저장합니다(IPython Notebook이 VM에서 실행되고, 로컬 드라이브가 VM 드라이브를 참조).</span><span class="sxs-lookup"><span data-stu-id="c3640-150">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
6. <span data-ttu-id="c3640-151">Azure VM에서 실행되는 SQL Server 데이터베이스에 데이터를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-151">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="c3640-152">옵션 \#1: SQL Server Management Studio 사용.</span><span class="sxs-lookup"><span data-stu-id="c3640-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="c3640-153">SQL Server VM에 로그인</span><span class="sxs-lookup"><span data-stu-id="c3640-153">Login to SQL Server VM</span></span>
   * <span data-ttu-id="c3640-154">SQL Server Management Studio를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="c3640-155">데이터베이스 및 대상 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-155">Create database and target tables.</span></span>
   * <span data-ttu-id="c3640-156">대량 가져오기 방법 중 하나를 사용하여 VM-로컬 파일의 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-156">Use one of the bulk import methods to load the data from VM-local files.</span></span>
   
   <span data-ttu-id="c3640-157">옵션 \#2: IPython Notebook 사용 – 중간 및 대규모 데이터 집합을 권장하지 않음</span><span class="sxs-lookup"><span data-stu-id="c3640-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="c3640-158">ODBC 연결 스트링을 사용하여 VM의 SQL 서버에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-158">Use ODBC connection string to access SQL Server on VM.</span></span>
   * <span data-ttu-id="c3640-159">데이터베이스 및 대상 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-159">Create database and target tables.</span></span>
   * <span data-ttu-id="c3640-160">대량 가져오기 방법 중 하나를 사용하여 VM-로컬 파일의 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-160">Use one of the bulk import methods to load the data from VM-local files.</span></span>
7. <span data-ttu-id="c3640-161">데이터를 탐색하고 필요에 따라 기능을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-161">Explore data, create features as needed.</span></span> <span data-ttu-id="c3640-162">기능을 데이터베이스 테이블에 구체화하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-162">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="c3640-163">필요한 쿼리를 기록하여 만들기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-163">Only note the necessary query to create them.</span></span>
8. <span data-ttu-id="c3640-164">필요하거나 원하는 경우 데이터 샘플 크기를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="c3640-165">[Azure 컴퓨터 학습 Studio](https://studio.azureml.net/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-165">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="c3640-166">[데이터 가져오기][import-data] 모듈을 사용하여 SQL Server에서 직접 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-166">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="c3640-167">[데이터 가져오기][import-data] 쿼리에서 직접 필요한 경우, 필드를 추출하는 데 필요한 쿼리를 붙여넣고, 기능을 만들고 데이터를 샘플링합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-167">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="c3640-168">수집된 데이터 집합으로 시작하여 Azure 컴퓨터 학습 실험 흐름을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="c3640-169"><a name="largelocaltodb"></a>시나리오 \#5: 로컬 파일의 큰 데이터 집합, Azure VM의 SQL Server를 대상으로 함</span><span class="sxs-lookup"><span data-stu-id="c3640-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![Azure의 SQL DB보다 큰 로컬 파일][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="c3640-171">추가 Azure 리소스: Azure 가상 컴퓨터 (SQL Server / IPython Notebook 서버)</span><span class="sxs-lookup"><span data-stu-id="c3640-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="c3640-172">SQL Server 및 IPython Notebook 서버를 실행하는 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="c3640-173">Azure 저장소 컨테이너에 데이터를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-173">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="c3640-174">(선택 사항) 데이터를 사전 처리하고 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="c3640-175">a.</span><span class="sxs-lookup"><span data-stu-id="c3640-175">a.</span></span>  <span data-ttu-id="c3640-176">IPython Notebook에서 데이터를 사전 처리하고 정리하며, Azure에서 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="c3640-177">b.</span><span class="sxs-lookup"><span data-stu-id="c3640-177">b.</span></span>  <span data-ttu-id="c3640-178">필요한 경우, 데이터를 정리된 테이블 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-178">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="c3640-179">c.</span><span class="sxs-lookup"><span data-stu-id="c3640-179">c.</span></span>  <span data-ttu-id="c3640-180">VM 로컬 파일에 데이터 저장합니다(IPython Notebook이 VM에서 실행되고, 로컬 드라이브가 VM 드라이브를 참조).</span><span class="sxs-lookup"><span data-stu-id="c3640-180">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="c3640-181">Azure VM에서 실행되는 SQL Server 데이터베이스에 데이터를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-181">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="c3640-182">a.</span><span class="sxs-lookup"><span data-stu-id="c3640-182">a.</span></span>  <span data-ttu-id="c3640-183">SQL Server VM에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-183">Login to SQL Server VM.</span></span>
   
   <span data-ttu-id="c3640-184">b.</span><span class="sxs-lookup"><span data-stu-id="c3640-184">b.</span></span>  <span data-ttu-id="c3640-185">데이터를 저장하지 경우, Azure에서 데이터 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-185">If data not saved already, download data files from Azure</span></span>
   
       storage container to local-VM folder.
   
   <span data-ttu-id="c3640-186">c.</span><span class="sxs-lookup"><span data-stu-id="c3640-186">c.</span></span>  <span data-ttu-id="c3640-187">SQL Server Management Studio를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="c3640-188">d.</span><span class="sxs-lookup"><span data-stu-id="c3640-188">d.</span></span>  <span data-ttu-id="c3640-189">데이터베이스 및 대상 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="c3640-190">e.</span><span class="sxs-lookup"><span data-stu-id="c3640-190">e.</span></span>  <span data-ttu-id="c3640-191">대량 가져오기 메서드 중 하나를 사용하여 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-191">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="c3640-192">f.</span><span class="sxs-lookup"><span data-stu-id="c3640-192">f.</span></span>  <span data-ttu-id="c3640-193">테이블 조인이 필요한 경우, 인덱스를 만들어 조인을 신속하게 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-193">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c3640-194">큰 데이터를 좀 더 빨리 로드하기 위해, 분할된 테이블을 만들고 병렬로 대량 데이터를 가져오는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import the data in parallel.</span></span> <span data-ttu-id="c3640-195">자세한 내용은 [SQL 분할된 테이블로 병렬로 데이터 가져오기](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3640-195">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="c3640-196">데이터를 탐색하고 필요에 따라 기능을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-196">Explore data, create features as needed.</span></span> <span data-ttu-id="c3640-197">기능을 데이터베이스 테이블에 구체화하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-197">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="c3640-198">필요한 쿼리를 기록하여 만들기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-198">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="c3640-199">필요하거나 원하는 경우 데이터 샘플 크기를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="c3640-200">[Azure 컴퓨터 학습 Studio](https://studio.azureml.net/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-200">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="c3640-201">[데이터 가져오기][import-data] 모듈을 사용하여 SQL Server에서 직접 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-201">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="c3640-202">[데이터 가져오기][import-data] 쿼리에서 직접 필요한 경우, 필드를 추출하는 데 필요한 쿼리를 붙여넣고, 기능을 만들고 데이터를 샘플링합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-202">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="c3640-203">업로드 데이터 집합으로 단순 Azure 기계 학습 실험 흐름 시작</span><span class="sxs-lookup"><span data-stu-id="c3640-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="c3640-204"><a name="largedbtodb"></a>시나리오 \#6: 온-프레미스의 SQL 서버 데이터베이스의 큰 데이터 집합, Azure 가상 컴퓨터의 SQL Server를 대상으로 함</span><span class="sxs-lookup"><span data-stu-id="c3640-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Azure의 SQL DB보다 큰 SQL DB 온-프레미스][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="c3640-206">추가 Azure 리소스: Azure 가상 컴퓨터 (SQL Server / IPython Notebook 서버)</span><span class="sxs-lookup"><span data-stu-id="c3640-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="c3640-207">SQL Server 및 IPython Notebook 서버를 실행하는 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="c3640-208">데이터 내보내기 메서드 중 하나를 사용하여 SQL Server에서 덤프 파일로 데이터를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-208">Use one of the data export methods to export the data from SQL Server to dump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c3640-209">온-프레미스 데이터베이스에서 모든 데이터를 이동하기로 결정한 경우, (빠른)메서드로 대체하여 전체 데이터베이스를 Azure의 SQL Server 인스턴스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-209">If you decide to move all data from the on-prem database, an alternate (faster) method to move the full database to the SQL Server instance in Azure.</span></span> <span data-ttu-id="c3640-210">데이터를 내보내고, 데이터베이스를 만들고 대상 데이터베이스로 데이터를 로드/가져오기하는 단계를 건너뛰고 대체 메서드를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-210">Skip the steps to export data, create database, and load/import data to the target database and follow the alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="c3640-211">Azure 저장소 컨테이너로 덤프 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-211">Upload dump files to Azure storage container.</span></span>
4. <span data-ttu-id="c3640-212">Azure 가상 컴퓨터에서 실행 중인 SQL Server 데이터베이스에 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-212">Load the data to a SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="c3640-213">a.</span><span class="sxs-lookup"><span data-stu-id="c3640-213">a.</span></span>  <span data-ttu-id="c3640-214">SQL Server VM에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-214">Login to the SQL Server VM.</span></span>
   
   <span data-ttu-id="c3640-215">b.</span><span class="sxs-lookup"><span data-stu-id="c3640-215">b.</span></span>  <span data-ttu-id="c3640-216">Azure 저장소 컨테이너에서 로컬 VM 폴더로 데이터 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-216">Download data files from an Azure storage container to the local-VM folder.</span></span>
   
   <span data-ttu-id="c3640-217">c.</span><span class="sxs-lookup"><span data-stu-id="c3640-217">c.</span></span>  <span data-ttu-id="c3640-218">SQL Server Management Studio를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="c3640-219">d.</span><span class="sxs-lookup"><span data-stu-id="c3640-219">d.</span></span>  <span data-ttu-id="c3640-220">데이터베이스 및 대상 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="c3640-221">e.</span><span class="sxs-lookup"><span data-stu-id="c3640-221">e.</span></span>  <span data-ttu-id="c3640-222">대량 가져오기 메서드 중 하나를 사용하여 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-222">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="c3640-223">f.</span><span class="sxs-lookup"><span data-stu-id="c3640-223">f.</span></span>  <span data-ttu-id="c3640-224">테이블 조인이 필요한 경우, 인덱스를 만들어 조인을 신속하게 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-224">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c3640-225">큰 데이터를 좀 더 빨리 로드하기 위해, 분할된 테이블을 만들고 병렬로 대량 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-225">For faster loading of large data sizes, create partitioned tables and to bulk import the data in parallel.</span></span> <span data-ttu-id="c3640-226">자세한 내용은 [SQL 분할된 테이블로 병렬로 데이터 가져오기](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3640-226">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="c3640-227">데이터를 탐색하고 필요에 따라 기능을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-227">Explore data, create features as needed.</span></span> <span data-ttu-id="c3640-228">기능을 데이터베이스 테이블에 구체화하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-228">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="c3640-229">필요한 쿼리를 기록하여 만들기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-229">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="c3640-230">필요하거나 원하는 경우 데이터 샘플 크기를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="c3640-231">[Azure 컴퓨터 학습 Studio](https://studio.azureml.net/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-231">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="c3640-232">[데이터 가져오기][import-data] 모듈을 사용하여 SQL Server에서 직접 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-232">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="c3640-233">[데이터 가져오기][import-data] 쿼리에서 직접 필요한 경우, 필드를 추출하는 데 필요한 쿼리를 붙여넣고, 기능을 만들고 데이터를 샘플링합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-233">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="c3640-234">업로드 데이터 집합으로 단순 Azure 기계 학습 실험 흐름 시작</span><span class="sxs-lookup"><span data-stu-id="c3640-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-to-copy-a-full-database-from-an-on-premises--sql-server-to-azure-sql-database"></a><span data-ttu-id="c3640-235">온-프레미스에서 Azure SQL Database로 전체 데이터베이스를 복사하는 대체 메서드</span><span class="sxs-lookup"><span data-stu-id="c3640-235">Alternate method to copy a full database from an on-premises  SQL Server to Azure SQL Database</span></span>
![로컬 DB를 분리하고 Azure의 SQL DB에 첨부][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="c3640-237">추가 Azure 리소스: Azure 가상 컴퓨터 (SQL Server / IPython Notebook 서버)</span><span class="sxs-lookup"><span data-stu-id="c3640-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="c3640-238">SQL Server VM에서 전체 SQL Server 데이터베이스를 복제하려면, 한 위치/서버에서 다른 위치/서버로 데이터베이스를 복사해야 하며, 데이터베이스가 일시적으로 오프라인 상태가 될 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-238">To replicate the entire SQL Server database in your SQL Server VM, you should copy a database from one location/server to another, assuming that the database can be taken temporarily offline.</span></span> <span data-ttu-id="c3640-239">SQL Server Management Studio 개체 탐색기 또는 해당하는 TRANSACT-SQL 명령을 사용하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-239">You do this in the SQL Server Management Studio Object Explorer, or using the equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="c3640-240">원본 위치에서 데이터베이스를 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-240">Detach the database at the source location.</span></span> <span data-ttu-id="c3640-241">자세한 내용은 [데이터베이스 분리](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3640-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="c3640-242">Windows 탐색기나 Windows 명령 프롬프트 창에서, 분리된 데이터베이스 파일을 복사하여 파일을 Azure의 SQL Server VM의 대상 위치에 로그합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-242">In Windows Explorer or Windows Command Prompt window, copy the detached database file or files and log file or files to the target location on the SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="c3640-243">복사된 파일을 대상 SQL Server 인스턴스에 첨부합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-243">Attach the copied files to the target SQL Server instance.</span></span> <span data-ttu-id="c3640-244">자세한 내용은 [데이터베이스 연결](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3640-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="c3640-245">[분리 및 연결을 사용하여 데이터베이스 이동(Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="c3640-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="c3640-246"><a name="largedbtohive"></a>시나리오 \#7: 로컬 파일의 빅 데이터, Azure HDInsight Hadoop 클러스터의 Hive 데이터베이스를 대상으로 함</span><span class="sxs-lookup"><span data-stu-id="c3640-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![로컬 대상 Hive의 빅 데이터][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="c3640-248">추가 Azure 리소스: Azure HDInsight Hadoop 클러스터 및 Azure Virtual Machine(IPython Notebook 서버)</span><span class="sxs-lookup"><span data-stu-id="c3640-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="c3640-249">IPython Notebook 서버를 실행하는 Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="c3640-250">Azure HDInsight Hadoop 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="c3640-251">(선택 사항) 데이터를 사전 처리하고 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="c3640-252">a.</span><span class="sxs-lookup"><span data-stu-id="c3640-252">a.</span></span>  <span data-ttu-id="c3640-253">IPython Notebook에서 데이터를 사전 처리하고 정리하며, Azure에서 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="c3640-254">b.</span><span class="sxs-lookup"><span data-stu-id="c3640-254">b.</span></span>  <span data-ttu-id="c3640-255">필요한 경우, 데이터를 정리된 테이블 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-255">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="c3640-256">c.</span><span class="sxs-lookup"><span data-stu-id="c3640-256">c.</span></span>  <span data-ttu-id="c3640-257">VM 로컬 파일에 데이터 저장합니다(IPython Notebook이 VM에서 실행되고, 로컬 드라이브가 VM 드라이브를 참조).</span><span class="sxs-lookup"><span data-stu-id="c3640-257">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="c3640-258">2단계에서 선택한 Hadoop 클러스터의 기본 컨테이너에 데이터를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-258">Upload data to the default container of the Hadoop cluster selected in the step 2.</span></span>
5. <span data-ttu-id="c3640-259">Azure HDInsight Hadoop 클러스터의 Hive 데이터베이스에 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-259">Load data to Hive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="c3640-260">a.</span><span class="sxs-lookup"><span data-stu-id="c3640-260">a.</span></span>  <span data-ttu-id="c3640-261">Hadoop 클러스터의 헤드 노드에 로그인</span><span class="sxs-lookup"><span data-stu-id="c3640-261">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="c3640-262">b.</span><span class="sxs-lookup"><span data-stu-id="c3640-262">b.</span></span>  <span data-ttu-id="c3640-263">Hadoop 명령줄을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-263">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="c3640-264">c.</span><span class="sxs-lookup"><span data-stu-id="c3640-264">c.</span></span>  <span data-ttu-id="c3640-265">Hadoop 명령줄의 명령 `cd %hive_home%\bin` 로 Hive 루트 디렉터리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-265">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="c3640-266">d.</span><span class="sxs-lookup"><span data-stu-id="c3640-266">d.</span></span>  <span data-ttu-id="c3640-267">Hive 쿼리를 실행하여 데이터베이스 및 테이블을 만들고 Blob 저장소에서 Hive 테이블로 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-267">Run the Hive queries to create database and tables, and load data from blob storage to Hive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c3640-268">데이터가 큰 경우 사용자는 파티션이 있는 Hive 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-268">If the data is big, users can create the Hive table with partitions.</span></span> <span data-ttu-id="c3640-269">그런 다음, 사용자는 헤드 노드의 Hadoop 명령줄에서 `for` 루프를 사용하여 파티션에서 분할된 Hive 테이블로 데이터를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-269">Then, users can use a `for` loop in the Hadoop Command Line on the head node to load data into the Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="c3640-270">Hadoop 명령줄에서 데이터를 탐색하고 필요에 따라 기능을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="c3640-271">기능을 데이터베이스 테이블에 구체화하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-271">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="c3640-272">필요한 쿼리를 기록하여 만들기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-272">Only note the necessary query to create them.</span></span>
   
   <span data-ttu-id="c3640-273">a.</span><span class="sxs-lookup"><span data-stu-id="c3640-273">a.</span></span>  <span data-ttu-id="c3640-274">Hadoop 클러스터의 헤드 노드에 로그인</span><span class="sxs-lookup"><span data-stu-id="c3640-274">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="c3640-275">b.</span><span class="sxs-lookup"><span data-stu-id="c3640-275">b.</span></span>  <span data-ttu-id="c3640-276">Hadoop 명령줄을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-276">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="c3640-277">c.</span><span class="sxs-lookup"><span data-stu-id="c3640-277">c.</span></span>  <span data-ttu-id="c3640-278">Hadoop 명령줄의 명령 `cd %hive_home%\bin` 로 Hive 루트 디렉터리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-278">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="c3640-279">d.</span><span class="sxs-lookup"><span data-stu-id="c3640-279">d.</span></span>  <span data-ttu-id="c3640-280">Hadoop 클러스터의 헤드 노드에 있는 Hadoop 명령줄에서 Hive 쿼리를 실행하여 필요에 따라 데이터를 탐색하고 기능을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-280">Run the Hive queries in Hadoop Command Line on the head node of the Hadoop cluster to explore the data and create features as needed.</span></span>
7. <span data-ttu-id="c3640-281">필요하거나 원하는 경우, Azure 컴퓨터 학습 Studio에 맞게 데이터를 샘플링합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-281">If needed and/or desired, sample the data to fit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="c3640-282">[Azure 컴퓨터 학습 Studio](https://studio.azureml.net/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-282">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="c3640-283">[데이터 가져오기][import-data] 모듈을 사용하여 `Hive Queries`에서 데이터를 직접 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-283">Read the data directly from the `Hive Queries` using the [Import Data][import-data] module.</span></span> <span data-ttu-id="c3640-284">[데이터 가져오기][import-data] 쿼리에서 직접 필요한 경우, 필드를 추출하는 데 필요한 쿼리를 붙여넣고, 기능을 만들고 데이터를 샘플링합니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-284">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="c3640-285">업로드 데이터 집합으로 단순 Azure 기계 학습 실험 흐름 시작</span><span class="sxs-lookup"><span data-stu-id="c3640-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="c3640-286"><a name="decisiontree"></a>시나리오 선택 의사 결정 트리</span><span class="sxs-lookup"><span data-stu-id="c3640-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="c3640-287">다음 다이어그램에는 위에서 설명한 시나리오 및 각 항목별 시나리오를 안내하도록 구성된 고급 분석 프로세스 및 기술이 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-287">The following diagram summarizes the scenarios described above and the Advanced Analytics Process and Technology choices made that take you to each of the itemized scenarios.</span></span> <span data-ttu-id="c3640-288">데이터 처리, 탐색, 기능 엔지니어링 및 샘플링은 소스, 중간 및/또는 대상 환경에서 하나 이상의 메서드/환경에서 발생할 수 있으며, 필요에 따라 반복적으로 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at the source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="c3640-289">이 다이어그램은 가능한 모든 흐름을 열거한 것이 아니라 일부만을 보여 줄 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="c3640-289">The diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![샘플 DS 프로세스 연습 시나리오][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="c3640-291">고급 분석 작동 예제</span><span class="sxs-lookup"><span data-stu-id="c3640-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="c3640-292">공용 데이터 집합에서 고급 분석 프로세스 및 기술을 사용하는 종단 간 Azure 기계 학습 연습에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3640-292">For end-to-end Azure Machine Learning walkthroughs that employ the Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="c3640-293">[실행 중인 팀 데이터 과학 프로세스: SQL Server 사용](machine-learning-data-science-process-sql-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="c3640-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="c3640-294">[실행 중인 팀 데이터 과학 프로세스: HDInsight Hadoop 클러스터 사용](machine-learning-data-science-process-hive-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="c3640-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

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
