---
title: "Azure Data Factory에서 지 원하는 aaaCompute 환경 | Microsoft Docs"
description: "Azure 데이터 팩터리 파이프라인 (예: Azure HDInsight) tootransform 또는 프로세스 데이터에서 사용할 수 있는 컴퓨팅 환경에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6877a7e8-1a58-4cfb-bbd3-252ac72e4145
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 07/25/2017
ms.author: shlo
ms.openlocfilehash: aba7d7de695bc1c7d475f1e741ee3b3e884151c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="compute-environments-supported-by-azure-data-factory"></a><span data-ttu-id="26cbd-103">Azure Data Factory에서 지원하는 컴퓨팅 환경</span><span class="sxs-lookup"><span data-stu-id="26cbd-103">Compute environments supported by Azure Data Factory</span></span>
<span data-ttu-id="26cbd-104">이 문서에서는 다른 계산 환경 tooprocess를 사용 하 여 또는 데이터를 변형할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-104">This article explains different compute environments that you can use tooprocess or transform data.</span></span> <span data-ttu-id="26cbd-105">또한 이러한 계산 환경 tooan Azure 데이터 팩터리에 연결 하는 연결 된 서비스를 구성할 때 Data Factory에서 지 원하는 다른 구성 (주문형 스트림과 bring 직접)에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-105">It also provides details about different configurations (on-demand vs. bring your own) supported by Data Factory when configuring linked services linking these compute environments tooan Azure data factory.</span></span>

<span data-ttu-id="26cbd-106">hello 다음 표에서 계산 환경에서 실행할 수 있는 Data Factory와 hello 활동에서 지 원하는 목록을.</span><span class="sxs-lookup"><span data-stu-id="26cbd-106">hello following table provides a list of compute environments supported by Data Factory and hello activities that can run on them.</span></span> 

| <span data-ttu-id="26cbd-107">컴퓨팅 환경</span><span class="sxs-lookup"><span data-stu-id="26cbd-107">Compute environment</span></span> | <span data-ttu-id="26cbd-108">작업</span><span class="sxs-lookup"><span data-stu-id="26cbd-108">activities</span></span> |
| --- | --- |
| <span data-ttu-id="26cbd-109">[주문형 HDInsight 클러스터](#azure-hdinsight-on-demand-linked-service) 또는 [사용자 고유의 HDInsight 클러스터](#azure-hdinsight-linked-service)</span><span class="sxs-lookup"><span data-stu-id="26cbd-109">[On-demand HDInsight cluster](#azure-hdinsight-on-demand-linked-service) or [your own HDInsight cluster](#azure-hdinsight-linked-service)</span></span> |<span data-ttu-id="26cbd-110">[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop 스트리밍](data-factory-hadoop-streaming-activity.md)</span><span class="sxs-lookup"><span data-stu-id="26cbd-110">[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop Streaming](data-factory-hadoop-streaming-activity.md)</span></span> |
| [<span data-ttu-id="26cbd-111">Azure 배치</span><span class="sxs-lookup"><span data-stu-id="26cbd-111">Azure Batch</span></span>](#azure-batch-linked-service) |[<span data-ttu-id="26cbd-112">DotNet</span><span class="sxs-lookup"><span data-stu-id="26cbd-112">DotNet</span></span>](data-factory-use-custom-activities.md) |
| [<span data-ttu-id="26cbd-113">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="26cbd-113">Azure Machine Learning</span></span>](#azure-machine-learning-linked-service) |[<span data-ttu-id="26cbd-114">Machine Learning 작업: 배치 실행 및 업데이트 리소스</span><span class="sxs-lookup"><span data-stu-id="26cbd-114">Machine Learning activities: Batch Execution and Update Resource</span></span>](data-factory-azure-ml-batch-execution-activity.md) |
| [<span data-ttu-id="26cbd-115">Azure 데이터 레이크 분석</span><span class="sxs-lookup"><span data-stu-id="26cbd-115">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics-linked-service) |[<span data-ttu-id="26cbd-116">데이터 레이크 분석 U-SQL</span><span class="sxs-lookup"><span data-stu-id="26cbd-116">Data Lake Analytics U-SQL</span></span>](data-factory-usql-activity.md) |
| <span data-ttu-id="26cbd-117">[Azure SQL](#azure-sql-linked-service), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-linked-service), [SQL Server](#sql-server-linked-service)</span><span class="sxs-lookup"><span data-stu-id="26cbd-117">[Azure SQL](#azure-sql-linked-service), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-linked-service), [SQL Server](#sql-server-linked-service)</span></span> |[<span data-ttu-id="26cbd-118">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="26cbd-118">Stored Procedure</span></span>](data-factory-stored-proc-activity.md) |

## <a name="supported-hdinsight-versions-in-azure-data-factory"></a><span data-ttu-id="26cbd-119">Azure Data Factory에서 지원되는 HDInsight 버전</span><span class="sxs-lookup"><span data-stu-id="26cbd-119">Supported HDInsight versions in Azure Data Factory</span></span>
<span data-ttu-id="26cbd-120">Azure HDInsight는 언제든 배포할 수 있는 여러 Hadoop 클러스터 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-120">Azure HDInsight supports multiple Hadoop cluster versions that can be deployed at any time.</span></span> <span data-ttu-id="26cbd-121">각 버전 선택 사항을 hello Hortonworks Data Platform (HDP) 배포의 특정 버전 및 해당 배포에 포함 된 구성 요소 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-121">Each version choice creates a specific version of hello Hortonworks Data Platform (HDP) distribution and a set of components that are contained within that distribution.</span></span> <span data-ttu-id="26cbd-122">HDInsight tooprovide 최신 Hadoop 에코 시스템 구성 요소 및 수정 프로그램의 지원 되는 버전의 hello 목록을 업데이트 하는 Microsoft 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-122">Microsoft keeps updating hello list of supported versions of HDInsight tooprovide latest Hadoop ecosystem components and fixes.</span></span> <span data-ttu-id="26cbd-123">hello HDInsight 3.2 2017 년 4 월 1에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-123">hello HDInsight 3.2 is deprecated on April 1, 2017.</span></span> <span data-ttu-id="26cbd-124">자세한 내용은 [지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26cbd-124">For detailed information, see [supported HDInsight versions](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>

<span data-ttu-id="26cbd-125">이로 인해 HDInsight 3.2 클러스터에 대해 실행되는 활동이 있는 기존 Azure Data Factory에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-125">This impacts existing Azure Data Factories that have Activities running against HDInsight 3.2 clusters.</span></span> <span data-ttu-id="26cbd-126">사용자가 toofollow hello 지침 섹션 tooupdate 다음 hello에 영향을 받는 데이터 팩터리 hello 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-126">We recommend users toofollow hello guidelines in hello following section tooupdate hello impacted Data Factories:</span></span>

### <a name="for-linked-services-pointing-tooyour-own-hdinsight-clusters"></a><span data-ttu-id="26cbd-127">연결 된 서비스에 대 한 tooyour 자체 HDInsight 클러스터를 가리키는</span><span class="sxs-lookup"><span data-stu-id="26cbd-127">For Linked Services pointing tooyour own HDInsight clusters</span></span>
* <span data-ttu-id="26cbd-128">**3.2 또는 클러스터 아래 HDInsight를 소유 하는 HDInsight 연결 된 서비스를 가리키는 tooyour:**</span><span class="sxs-lookup"><span data-stu-id="26cbd-128">**HDInsight Linked Services pointing tooyour own HDInsight 3.2 or below clusters:**</span></span>

  <span data-ttu-id="26cbd-129">Azure Data Factory 지원 자체 HDInsight 클러스터 HDI 3.1에서 너무 제출 작업 tooyour[최신 지원 hello HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-129">Azure Data Factory supports submitting jobs tooyour own HDInsight clusters from HDI 3.1 too[hello latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span> <span data-ttu-id="26cbd-130">그러나 더 이상 후 만들 수 없습니다 3.2 HDInsight 클러스터에서 설명 하는 hello 사용 중단 정책에 따라 2017 년 4 월 1 [지원 되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-130">However, you can no longer create HDInsight 3.2 cluster after April 1, 2017 based on hello deprecation policy documented in [supported HDInsight versions](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>  

  <span data-ttu-id="26cbd-131">**권장 사항:**</span><span class="sxs-lookup"><span data-stu-id="26cbd-131">**Recommendations:**</span></span> 
  * <span data-ttu-id="26cbd-132">테스트 tooensure hello 호환성 hello 너무이 연결 된 서비스를 참조 하는 작업의 수행[최신 지원 hello HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) 에 설명 된 정보로 [Hadoop 사용할 수 있는 구성 요소 다른 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) 및 [Hortonworks 릴리스 정보 HDInsight 버전에 연결 된](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-132">Perform tests tooensure hello compatibility of hello Activities that reference this Linked Services too[hello latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) with information documented in [Hadoop components available with different HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) and [Hortonworks release notes associated with HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).</span></span>
  * <span data-ttu-id="26cbd-133">3.2 HDInsight 클러스터를 너무 업그레이드[최신 지원 hello HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello 최신 Hadoop 에코 시스템 구성 요소 및 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-133">Upgrade your HDInsight 3.2 cluster too[hello latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello latest Hadoop ecosystem components and fixes.</span></span> 

* <span data-ttu-id="26cbd-134">**3.3 또는 클러스터 위에 HDInsight를 소유 하는 HDInsight 연결 된 서비스를 가리키는 tooyour:**</span><span class="sxs-lookup"><span data-stu-id="26cbd-134">**HDInsight Linked Services pointing tooyour own HDInsight 3.3 or above clusters:**</span></span>

  <span data-ttu-id="26cbd-135">Azure Data Factory 지원 자체 HDInsight 클러스터 HDI 3.1에서 너무 제출 작업 tooyour[최신 지원 hello HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-135">Azure Data Factory supports submitting jobs tooyour own HDInsight clusters from HDI 3.1 too[hello latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span> 
  
  <span data-ttu-id="26cbd-136">**권장 사항:**</span><span class="sxs-lookup"><span data-stu-id="26cbd-136">**Recommendations:**</span></span> 
  * <span data-ttu-id="26cbd-137">Data Factory 관점에서 보면 아무런 작업도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-137">No action is required from Data Factory perspective.</span></span> <span data-ttu-id="26cbd-138">그러나 HDInsight의 낮은 버전에 있는 경우 여전히 줄이려면 업그레이드 너무[최신 지원 hello HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello 최신 Hadoop 에코 시스템 구성 요소 및 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-138">However, if you are on a lower version of HDInsight, we still recommend upgrading too[hello latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello latest Hadoop ecosystem components and fixes.</span></span>

### <a name="for-hdinsight-on-demand-linked-services"></a><span data-ttu-id="26cbd-139">주문형 HDInsight 연결된 서비스의 경우</span><span class="sxs-lookup"><span data-stu-id="26cbd-139">For HDInsight On-Demand Linked Services</span></span>
* <span data-ttu-id="26cbd-140">**주문형 HDInsight 연결된 서비스 JSON 정의에 지정되어 있는 버전 3.2 이하:**</span><span class="sxs-lookup"><span data-stu-id="26cbd-140">**Version 3.2 or below is specified in HDInsight On-Demand Linked Services JSON definition:**</span></span>
  
  <span data-ttu-id="26cbd-141">Azure Data Factory에서는 **2017년 5월 15일**부터 버전 3.3 이상의 주문형 HDInsight 클러스터 만들기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-141">Azure Data Factory will support creation of On-Demand HDInsight clusters of version 3.3 or more from **05/15/2017** onwards.</span></span> <span data-ttu-id="26cbd-142">와 연결 된 서비스 너무 확장은 기존 주문형 HDInsight 3.2에 대 한 지원의 hello 끝**2017/15/07**합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-142">And, hello end of support for existing on-demand HDInsight 3.2 linked services is extended too**07/15/2017**.</span></span>  

  <span data-ttu-id="26cbd-143">**권장 사항:**</span><span class="sxs-lookup"><span data-stu-id="26cbd-143">**Recommendations:**</span></span> 
  * <span data-ttu-id="26cbd-144">테스트 tooensure hello 호환성 hello 너무이 연결 된 서비스를 참조 하는 작업의 수행 [최신 지원 hello HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) 에 설명 된 정보로 [Hadoop 사용할 수 있는 구성 요소 다른 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) 및 [Hortonworks 릴리스 정보 HDInsight 버전에 연결 된](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-144">Perform tests tooensure hello compatibility of hello Activities that reference this Linked Services too [hello latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) with information documented in [Hadoop components available with different HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) and [Hortonworks release notes associated with HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).</span></span>
  * <span data-ttu-id="26cbd-145">하기 전에 **2017/15/07**, 주문형 HDI 연결 된 서비스 JSON 정의에서 hello Version 속성을 너무 업데이트[최신 지원 hello HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello 최신 Hadoop 에코 시스템 구성 요소 및 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-145">Before **07/15/2017**, update hello Version property in On-Demand HDI Linked Service JSON definition too[hello latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello latest Hadoop ecosystem components and fixes.</span></span> <span data-ttu-id="26cbd-146">자세한 JSON 정의 대 한 참조 toohello [Azure HDInsight 주문형 연결 된 서비스 샘플](#azure-hdinsight-on-demand-linked-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-146">For detailed JSON definition, refer toohello [Azure HDInsight On-Demand Linked Service sample](#azure-hdinsight-on-demand-linked-service).</span></span> 

* <span data-ttu-id="26cbd-147">**주문형 HDInsight 연결된 서비스에 지정되지 않은 버전:**</span><span class="sxs-lookup"><span data-stu-id="26cbd-147">**Version not specified in On-Demand HDInsight Linked Services:**</span></span>
  
  <span data-ttu-id="26cbd-148">Azure Data Factory에서는 **2017년 5월 15일**부터 버전 3.3 이상의 주문형 HDInsight 클러스터 만들기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-148">Azure Data Factory will support creation of on-demand HDInsight clusters of version 3.3 or more from **05/15/2017** onwards.</span></span> <span data-ttu-id="26cbd-149">지원 tooexisting 주문형 HDInsight 3.2 연결 된 서비스의 hello 끝 너무 확장 되 고**2017/15/07**합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-149">And, hello end of support tooexisting on-demand HDInsight 3.2 linked services is extended too**07/15/2017**.</span></span> 

  <span data-ttu-id="26cbd-150">하기 전에 **2017/15/07**, hello 기본 버전에 대 한 값을 입력 하지 않으면 및 osType 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-150">Before **07/15/2017**, if left blank, hello default values for version and osType properties are:</span></span> 

  | <span data-ttu-id="26cbd-151">속성</span><span class="sxs-lookup"><span data-stu-id="26cbd-151">Property</span></span> | <span data-ttu-id="26cbd-152">기본값</span><span class="sxs-lookup"><span data-stu-id="26cbd-152">Default Value</span></span> | <span data-ttu-id="26cbd-153">필수</span><span class="sxs-lookup"><span data-stu-id="26cbd-153">Required</span></span> |
  | --- | --- | --- |
  <span data-ttu-id="26cbd-154">버전</span><span class="sxs-lookup"><span data-stu-id="26cbd-154">Version</span></span>   | <span data-ttu-id="26cbd-155">Windows 클러스터용 HDI 3.1 및 Linux 클러스터용 HDI 3.2</span><span class="sxs-lookup"><span data-stu-id="26cbd-155">HDI 3.1 for Windows cluster and HDI 3.2 for Linux cluster.</span></span>| <span data-ttu-id="26cbd-156">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-156">No</span></span>
  <span data-ttu-id="26cbd-157">osType</span><span class="sxs-lookup"><span data-stu-id="26cbd-157">osType</span></span> | <span data-ttu-id="26cbd-158">hello 기본값은 Windows</span><span class="sxs-lookup"><span data-stu-id="26cbd-158">hello default is Windows</span></span> | <span data-ttu-id="26cbd-159">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-159">No</span></span>

  <span data-ttu-id="26cbd-160">후 **2017/15/07**, hello 기본 버전에 대 한 값을 입력 하지 않으면 및 osType 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-160">After **07/15/2017**, if left blank, hello default values for version and osType properties are:</span></span>

  | <span data-ttu-id="26cbd-161">속성</span><span class="sxs-lookup"><span data-stu-id="26cbd-161">Property</span></span> | <span data-ttu-id="26cbd-162">기본값</span><span class="sxs-lookup"><span data-stu-id="26cbd-162">Default Value</span></span> | <span data-ttu-id="26cbd-163">필수</span><span class="sxs-lookup"><span data-stu-id="26cbd-163">Required</span></span> |
  | --- | --- | --- |
  <span data-ttu-id="26cbd-164">버전</span><span class="sxs-lookup"><span data-stu-id="26cbd-164">Version</span></span>   | <span data-ttu-id="26cbd-165">Windows 클러스터용 HDI 3.3 및 Linux 클러스터용 3.5.</span><span class="sxs-lookup"><span data-stu-id="26cbd-165">HDI 3.3 for Windows cluster and 3.5 for Linux cluster.</span></span>    | <span data-ttu-id="26cbd-166">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-166">No</span></span>
  <span data-ttu-id="26cbd-167">osType</span><span class="sxs-lookup"><span data-stu-id="26cbd-167">osType</span></span> | <span data-ttu-id="26cbd-168">hello 기본값은 Linux</span><span class="sxs-lookup"><span data-stu-id="26cbd-168">hello default is Linux</span></span>   | <span data-ttu-id="26cbd-169">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-169">No</span></span>

  <span data-ttu-id="26cbd-170">**권장 사항:**</span><span class="sxs-lookup"><span data-stu-id="26cbd-170">**Recommendations:**</span></span> 
  * <span data-ttu-id="26cbd-171">하기 전에 **2017/15/07**, 테스트 tooensure hello 호환성 hello 너무이 연결 된 서비스를 참조 하는 작업의 수행[최신 지원 hello HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) 설명 정보로 [Hadoop 다른 HDInsight 버전을 사용할 수 있는 구성 요소](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) 및 [Hortonworks 릴리스 정보 HDInsight 버전에 연결 된](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-171">Before **07/15/2017**, perform tests tooensure hello compatibility of hello Activities that reference this Linked Services too[hello latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) with information documented in [Hadoop components available with different HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) and [Hortonworks release notes associated with HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).</span></span>  
  * <span data-ttu-id="26cbd-172">후 **2017/15/07**, toooverride hello 기본 설정을 선택 하는 경우 osType 및 버전 값을 명시적으로 지정 했는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="26cbd-172">After **07/15/2017**, make sure you explicitly specify osType and version values if you would like toooverride hello default settings.</span></span> 

>[!Note]
><span data-ttu-id="26cbd-173">현재 Azure Data Factory는 Azure Data Lake Store를 기본 저장소로 사용하는 HDInsight 클러스터를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-173">Currently Azure Data Factory does not support HDInsight clusters using Azure Data Lake Store as primary store.</span></span> <span data-ttu-id="26cbd-174">Azure Storage를 HDInsight 클러스터의 기본 저장소로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-174">Use Azure Storage as primary store for HDInsight clusters.</span></span> 
>  
>  

## <a name="on-demand-compute-environment"></a><span data-ttu-id="26cbd-175">주문형 계산 환경</span><span class="sxs-lookup"><span data-stu-id="26cbd-175">On-demand compute environment</span></span>
<span data-ttu-id="26cbd-176">이러한 유형의 구성 hello 컴퓨팅 환경은 완전히 hello Azure 데이터 팩터리 서비스에서 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-176">In this type of configuration, hello computing environment is fully managed by hello Azure Data Factory service.</span></span> <span data-ttu-id="26cbd-177">자동으로 작업은 전송 된 tooprocess 데이터 전에 hello 데이터 팩터리 서비스에서 만든 및 hello 작업이 완료 될 때 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-177">It is automatically created by hello Data Factory service before a job is submitted tooprocess data and removed when hello job is completed.</span></span> <span data-ttu-id="26cbd-178">Hello 요청 시 계산 환경에 대 한 연결 된 서비스를 만들 지정, 구성, 및 작업 실행, 클러스터 관리 및 작업 부트스트랩에 대 한 세부적인 설정을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-178">You can create a linked service for hello on-demand compute environment, configure it, and control granular settings for job execution, cluster management, and bootstrapping actions.</span></span>

> [!NOTE]
> <span data-ttu-id="26cbd-179">요청 시 구성 hello는 현재 Azure HDInsight 클러스터에만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-179">hello on-demand configuration is currently supported only for Azure HDInsight clusters.</span></span>
> 
> 

## <a name="azure-hdinsight-on-demand-linked-service"></a><span data-ttu-id="26cbd-180">Azure HDInsight 주문형 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="26cbd-180">Azure HDInsight On-Demand Linked Service</span></span>
<span data-ttu-id="26cbd-181">hello Azure 데이터 팩터리 서비스는 Windows/Linux 기반에 주문형 HDInsight 클러스터 tooprocess 데이터를 자동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-181">hello Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster tooprocess data.</span></span> <span data-ttu-id="26cbd-182">hello 클러스터 hello hello 클러스터와 연결 된 hello 저장소 계정 (hello JSON의에서 linkedServiceName 속성)와 동일한 지역에에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-182">hello cluster is created in hello same region as hello storage account (linkedServiceName property in hello JSON) associated with hello cluster.</span></span> <span data-ttu-id="26cbd-183">hello 저장소 계정에는 범용 표준 Azure 저장소 계정 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-183">hello storage account must be a general-purpose standard Azure storage account.</span></span> 

<span data-ttu-id="26cbd-184">Hello 다음에 유의 하십시오 **중요** 포인트에 대 한 주문형 HDInsight 연결 된 서비스:</span><span class="sxs-lookup"><span data-stu-id="26cbd-184">Note hello following **important** points about on-demand HDInsight linked service:</span></span>

* <span data-ttu-id="26cbd-185">요청 시 hello 표시 되지 않으면 Azure 구독에서 생성 하는 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-185">You do not see hello on-demand HDInsight cluster created in your Azure subscription.</span></span> <span data-ttu-id="26cbd-186">hello Azure 데이터 팩터리 서비스에서 사용자 대신 hello 주문형 HDInsight 클러스터를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-186">hello Azure Data Factory service manages hello on-demand HDInsight cluster on your behalf.</span></span>
* <span data-ttu-id="26cbd-187">hello 주문형 HDInsight 클러스터에서 실행 되는 작업에 대 한 로그 복사 hello HDInsight 클러스터와 연결 된 toohello 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="26cbd-187">hello logs for jobs that are run on an on-demand HDInsight cluster are copied toohello storage account associated with hello HDInsight cluster.</span></span> <span data-ttu-id="26cbd-188">Hello hello에서 Azure 포털에서에서 이러한 로그에 액세스할 수 **작업 실행 세부 정보** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-188">You can access these logs from hello Azure portal in hello **Activity Run Details** blade.</span></span> <span data-ttu-id="26cbd-189">세부 정보는 [파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 문서를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="26cbd-189">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>
* <span data-ttu-id="26cbd-190">Hello HDInsight 클러스터를 가장 하는 hello 시간 및 실행 되는 작업에 대해서만 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-190">You are charged only for hello time when hello HDInsight cluster is up and running jobs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26cbd-191">일반적으로 걸리는 **20 분** 또는 필요에 따라 더 많은 tooprovision Azure HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-191">It typically takes **20 minutes** or more tooprovision an Azure HDInsight cluster on demand.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="26cbd-192">예제</span><span class="sxs-lookup"><span data-stu-id="26cbd-192">Example</span></span>
<span data-ttu-id="26cbd-193">다음 JSON hello Linux 기반에 주문형 HDInsight 연결 된 서비스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-193">hello following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="26cbd-194">hello 데이터 팩터리 서비스를 자동으로 만듭니다는 **Linux 기반** HDInsight 클러스터는 데이터 조각을 처리 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="26cbd-194">hello Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

<span data-ttu-id="26cbd-195">Windows 기반 HDInsight 클러스터 toouse 설정 **osType** 너무**windows** hello 기본값 그대로 hello 속성을 사용 하지 않는 또는: windows 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-195">toouse a Windows-based HDInsight cluster, set **osType** too**windows** or do not use hello property as hello default value is: windows.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="26cbd-196">hello HDInsight 클러스터를 만듭니다는 **기본 컨테이너** hello JSON에에서 지정 된 hello blob 저장소에 (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="26cbd-196">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="26cbd-197">HDInsight 클러스터 hello 삭제 될 때이 컨테이너를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-197">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="26cbd-198">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-198">This behavior is by design.</span></span> <span data-ttu-id="26cbd-199">주문형 HDInsight 연결 된 서비스와 HDInsight 클러스터를 분할 영역 해야 처리 하지 않으면 기존 라이브 클러스터 toobe 때마다 만드는 (**timeToLive**) hello 처리가 완료 되 면 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-199">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span> 
> 
> <span data-ttu-id="26cbd-200">많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-200">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="26cbd-201">Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-201">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="26cbd-202">이러한 컨테이너의 hello 이름 패턴을 따르도록: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-202">hello names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span></span> <span data-ttu-id="26cbd-203">와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) toodelete 컨테이너에 Azure blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-203">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="26cbd-204">properties</span><span class="sxs-lookup"><span data-stu-id="26cbd-204">Properties</span></span>
| <span data-ttu-id="26cbd-205">속성</span><span class="sxs-lookup"><span data-stu-id="26cbd-205">Property</span></span> | <span data-ttu-id="26cbd-206">설명</span><span class="sxs-lookup"><span data-stu-id="26cbd-206">Description</span></span> | <span data-ttu-id="26cbd-207">필수</span><span class="sxs-lookup"><span data-stu-id="26cbd-207">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26cbd-208">type</span><span class="sxs-lookup"><span data-stu-id="26cbd-208">type</span></span> |<span data-ttu-id="26cbd-209">너무 hello 유형 속성을 설정 해야**HDInsightOnDemand**합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-209">hello type property should be set too**HDInsightOnDemand**.</span></span> |<span data-ttu-id="26cbd-210">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-210">Yes</span></span> |
| <span data-ttu-id="26cbd-211">clusterSize</span><span class="sxs-lookup"><span data-stu-id="26cbd-211">clusterSize</span></span> |<span data-ttu-id="26cbd-212">Hello 클러스터의 작업자/데이터 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-212">Number of worker/data nodes in hello cluster.</span></span> <span data-ttu-id="26cbd-213">hello HDInsight 클러스터는 헤드 노드 hello이이 속성에 대해 지정 하는 작업자 노드 수와 함께 2으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-213">hello HDInsight cluster is created with 2 head nodes along with hello number of worker nodes you specify for this property.</span></span> <span data-ttu-id="26cbd-214">hello 노드는 크기는 4 작업자 노드 클러스터는 24 코어 4 개 코어에 Standard_D3 (4\*작업자 노드 + 2에 대 한 4 = 16 코어가\*헤드 노드에 대 한 4 = 8 코어).</span><span class="sxs-lookup"><span data-stu-id="26cbd-214">hello nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="26cbd-215">참조 [HDInsight 클러스터를 만드는 Linux 기반 Hadoop](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) hello Standard_D3 계층에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-215">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about hello Standard_D3 tier.</span></span> |<span data-ttu-id="26cbd-216">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-216">Yes</span></span> |
| <span data-ttu-id="26cbd-217">timetolive</span><span class="sxs-lookup"><span data-stu-id="26cbd-217">timetolive</span></span> |<span data-ttu-id="26cbd-218">hello는 hello 주문형 HDInsight 클러스터에 대 한 유휴 시간을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-218">hello allowed idle time for hello on-demand HDInsight cluster.</span></span> <span data-ttu-id="26cbd-219">기간 hello 주문형 HDInsight 클러스터의 연결이 유지 hello 클러스터에 다른 활성 작업이 있는 경우 실행 작업을 완료 한 후 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-219">Specifies how long hello on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in hello cluster.</span></span><br/><br/><span data-ttu-id="26cbd-220">예를 들어 활동 실행 6 분 및 timetolive 않습니다 too5 분, 5 분 후 hello에 대 한 연결 유지 hello 클러스터 유지할 6 분의 처리를 실행 하는 hello 활동을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-220">For example, if an activity run takes 6 minutes and timetolive is set too5 minutes, hello cluster stays alive for 5 minutes after hello 6 minutes of processing hello activity run.</span></span> <span data-ttu-id="26cbd-221">Hello에서 처리 된를 실행 하는 다른 활동을 hello 6 분 동안 창을 실행 하는 경우 동일한 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-221">If another activity run is executed with hello 6-minutes window, it is processed by hello same cluster.</span></span><br/><br/><span data-ttu-id="26cbd-222">주문형 HDInsight 클러스터를 만드는 작업은 비용이 많이 드는 작업 (이 걸릴 수), 따라서 데이터 팩터리의 필요한 tooimprove 성능으로이 설정을 사용 하 여 주문형 HDInsight 클러스터를 다시 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-222">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed tooimprove performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="26cbd-223">Timetolive 값 too0로 설정 하면 hello 클러스터 hello 활동이 실행 완료 되는 즉시 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-223">If you set timetolive value too0, hello cluster is deleted as soon as hello activity run completes.</span></span> <span data-ttu-id="26cbd-224">반면, 높은 값을 설정 하는 경우 hello 클러스터 불필요 하 게 많은 비용이 발생 유휴 유지 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-224">Whereas, if you set a high value, hello cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="26cbd-225">따라서이 필요에 따라 hello 적절 한 값을 설정 하는 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-225">Therefore, it is important that you set hello appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="26cbd-226">Hello timetolive 속성 값을 적절 하 게 설정 하는 경우 여러 파이프라인 hello 주문형 HDInsight 클러스터의 hello 인스턴스를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-226">If hello timetolive property value is appropriately set, multiple pipelines can share hello instance of hello on-demand HDInsight cluster.</span></span>  |<span data-ttu-id="26cbd-227">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-227">Yes</span></span> |
| <span data-ttu-id="26cbd-228">버전</span><span class="sxs-lookup"><span data-stu-id="26cbd-228">version</span></span> |<span data-ttu-id="26cbd-229">Hello HDInsight 클러스터의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-229">Version of hello HDInsight cluster.</span></span> <span data-ttu-id="26cbd-230">hello은 Windows 클러스터에 대 한 3.1 및 3.2 Linux 클러스터에 대 한</span><span class="sxs-lookup"><span data-stu-id="26cbd-230">hello default value is 3.1 for Windows cluster and 3.2 for Linux cluster.</span></span> |<span data-ttu-id="26cbd-231">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-231">No</span></span> |
| <span data-ttu-id="26cbd-232">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="26cbd-232">linkedServiceName</span></span> | <span data-ttu-id="26cbd-233">Azure 저장소 연결 서비스 toobe를 저장 하 고 데이터 처리에 대 한 hello 주문형 클러스터에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-233">Azure Storage linked service toobe used by hello on-demand cluster for storing and processing data.</span></span> <span data-ttu-id="26cbd-234">hello HDInsight 클러스터를 만드는 hello에 동일한 Azure 저장소 계정과이 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-234">hello HDInsight cluster is created in hello same region as this Azure Storage account.</span></span><p><span data-ttu-id="26cbd-235">현재, hello 저장소로 Azure 데이터 레이크 저장소를 사용 하는 주문형 HDInsight 클러스터를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-235">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as hello storage.</span></span> <span data-ttu-id="26cbd-236">Azure 데이터 레이크 저장소에서 처리 하는 HDInsight에서 toostore hello 결과 데이터를 원하는 hello Azure Blob 저장소 toohello Azure 데이터 레이크 저장소에서에서 복사 작업 toocopy hello 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-236">If you want toostore hello result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity toocopy hello data from hello Azure Blob Storage toohello Azure Data Lake Store.</span></span> </p>  | <span data-ttu-id="26cbd-237">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-237">Yes</span></span> |
| <span data-ttu-id="26cbd-238">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="26cbd-238">additionalLinkedServiceNames</span></span> |<span data-ttu-id="26cbd-239">HDInsight hello에 대 한 추가 저장소 계정을 연결 된 서비스 hello 데이터 팩터리 서비스에서 사용자 대신 등록할 수 있도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-239">Specifies additional storage accounts for hello HDInsight linked service so that hello Data Factory service can register them on your behalf.</span></span> <span data-ttu-id="26cbd-240">이러한 저장소 계정은 hello에 있어야에서 생성 된 hello 동일 hello HDInsight 클러스터와 동일한 지역 hello 저장소 계정과 linkedServiceName로 지정 된 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-240">These storage accounts must be in hello same region as hello HDInsight cluster, which is created in hello same region as hello storage account specified by linkedServiceName.</span></span> |<span data-ttu-id="26cbd-241">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-241">No</span></span> |
| <span data-ttu-id="26cbd-242">osType</span><span class="sxs-lookup"><span data-stu-id="26cbd-242">osType</span></span> |<span data-ttu-id="26cbd-243">운영 체제 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-243">Type of operating system.</span></span> <span data-ttu-id="26cbd-244">허용되는 값은 Windows(기본값) 및 Linux입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-244">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="26cbd-245">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-245">No</span></span> |
| <span data-ttu-id="26cbd-246">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="26cbd-246">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="26cbd-247">Azure SQL 연결의 hello 이름에 해당 지점 toohello HCatalog 데이터베이스를 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-247">hello name of Azure SQL linked service that point toohello HCatalog database.</span></span> <span data-ttu-id="26cbd-248">hello 주문형 HDInsight 클러스터는 hello metastore로 hello Azure SQL 데이터베이스를 사용 하 여 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-248">hello on-demand HDInsight cluster is created by using hello Azure SQL database as hello metastore.</span></span> |<span data-ttu-id="26cbd-249">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-249">No</span></span> |

#### <a name="additionallinkedservicenames-json-example"></a><span data-ttu-id="26cbd-250">additionalLinkedServiceNames JSON 예제</span><span class="sxs-lookup"><span data-stu-id="26cbd-250">additionalLinkedServiceNames JSON example</span></span>

```json
"additionalLinkedServiceNames": [
    "otherLinkedServiceName1",
    "otherLinkedServiceName2"
  ]
```

### <a name="advanced-properties"></a><span data-ttu-id="26cbd-251">고급 속성</span><span class="sxs-lookup"><span data-stu-id="26cbd-251">Advanced Properties</span></span>
<span data-ttu-id="26cbd-252">또한 hello 다음과 같은 hello 주문형 HDInsight 클러스터의 hello 세분화 된 구성에 대 한 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-252">You can also specify hello following properties for hello granular configuration of hello on-demand HDInsight cluster.</span></span>

| <span data-ttu-id="26cbd-253">속성</span><span class="sxs-lookup"><span data-stu-id="26cbd-253">Property</span></span> | <span data-ttu-id="26cbd-254">설명</span><span class="sxs-lookup"><span data-stu-id="26cbd-254">Description</span></span> | <span data-ttu-id="26cbd-255">필수</span><span class="sxs-lookup"><span data-stu-id="26cbd-255">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="26cbd-256">coreConfiguration</span><span class="sxs-lookup"><span data-stu-id="26cbd-256">coreConfiguration</span></span> |<span data-ttu-id="26cbd-257">Hello HDInsight 클러스터 toobe 생성에 대 한 hello 핵심 구성 매개 변수 (예: 핵심 site.xml)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-257">Specifies hello core configuration parameters (as in core-site.xml) for hello HDInsight cluster toobe created.</span></span> |<span data-ttu-id="26cbd-258">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-258">No</span></span> |
| <span data-ttu-id="26cbd-259">hBaseConfiguration</span><span class="sxs-lookup"><span data-stu-id="26cbd-259">hBaseConfiguration</span></span> |<span data-ttu-id="26cbd-260">Hello HBase 구성 매개 변수 (hbase-site.xml) hello HDInsight 클러스터에 대 한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-260">Specifies hello HBase configuration parameters (hbase-site.xml) for hello HDInsight cluster.</span></span> |<span data-ttu-id="26cbd-261">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-261">No</span></span> |
| <span data-ttu-id="26cbd-262">hdfsConfiguration</span><span class="sxs-lookup"><span data-stu-id="26cbd-262">hdfsConfiguration</span></span> |<span data-ttu-id="26cbd-263">Hello HDFS 구성 매개 변수 (hdfs-site.xml) hello HDInsight 클러스터에 대 한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-263">Specifies hello HDFS configuration parameters (hdfs-site.xml) for hello HDInsight cluster.</span></span> |<span data-ttu-id="26cbd-264">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-264">No</span></span> |
| <span data-ttu-id="26cbd-265">hiveConfiguration</span><span class="sxs-lookup"><span data-stu-id="26cbd-265">hiveConfiguration</span></span> |<span data-ttu-id="26cbd-266">Hello hive 구성 매개 변수 (hive-site.xml) hello HDInsight 클러스터에 대 한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-266">Specifies hello hive configuration parameters (hive-site.xml) for hello HDInsight cluster.</span></span> |<span data-ttu-id="26cbd-267">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-267">No</span></span> |
| <span data-ttu-id="26cbd-268">mapReduceConfiguration</span><span class="sxs-lookup"><span data-stu-id="26cbd-268">mapReduceConfiguration</span></span> |<span data-ttu-id="26cbd-269">Hello MapReduce 구성 매개 변수 (mapred-site.xml) hello HDInsight 클러스터에 대 한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-269">Specifies hello MapReduce configuration parameters (mapred-site.xml) for hello HDInsight cluster.</span></span> |<span data-ttu-id="26cbd-270">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-270">No</span></span> |
| <span data-ttu-id="26cbd-271">oozieConfiguration</span><span class="sxs-lookup"><span data-stu-id="26cbd-271">oozieConfiguration</span></span> |<span data-ttu-id="26cbd-272">Hello Oozie 구성 매개 변수 (oozie-site.xml) hello HDInsight 클러스터에 대 한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-272">Specifies hello Oozie configuration parameters (oozie-site.xml) for hello HDInsight cluster.</span></span> |<span data-ttu-id="26cbd-273">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-273">No</span></span> |
| <span data-ttu-id="26cbd-274">stormConfiguration</span><span class="sxs-lookup"><span data-stu-id="26cbd-274">stormConfiguration</span></span> |<span data-ttu-id="26cbd-275">Hello Storm 구성 매개 변수 (storm-site.xml) hello HDInsight 클러스터에 대 한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-275">Specifies hello Storm configuration parameters (storm-site.xml) for hello HDInsight cluster.</span></span> |<span data-ttu-id="26cbd-276">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-276">No</span></span> |
| <span data-ttu-id="26cbd-277">yarnConfiguration</span><span class="sxs-lookup"><span data-stu-id="26cbd-277">yarnConfiguration</span></span> |<span data-ttu-id="26cbd-278">Hello Yarn 구성 매개 변수 (yarn-site.xml) hello HDInsight 클러스터에 대 한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-278">Specifies hello Yarn configuration parameters (yarn-site.xml) for hello HDInsight cluster.</span></span> |<span data-ttu-id="26cbd-279">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-279">No</span></span> |

#### <a name="example--on-demand-hdinsight-cluster-configuration-with-advanced-properties"></a><span data-ttu-id="26cbd-280">예제 - 고급 속성을 포함하는 주문형 HDInsight 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="26cbd-280">Example – On-demand HDInsight cluster configuration with advanced properties</span></span>

```json
{
  "name": " HDInsightOnDemandLinkedService",
  "properties": {
    "type": "HDInsightOnDemand",
    "typeProperties": {
      "clusterSize": 16,
      "timeToLive": "01:30:00",
      "linkedServiceName": "adfods1",
      "coreConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "hiveConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "mapReduceConfiguration": {
        "mapreduce.reduce.java.opts": "-Xmx4000m",
        "mapreduce.map.java.opts": "-Xmx4000m",
        "mapreduce.map.memory.mb": "5000",
        "mapreduce.reduce.memory.mb": "5000",
        "mapreduce.job.reduce.slowstart.completedmaps": "0.8"
      },
      "yarnConfiguration": {
        "yarn.app.mapreduce.am.resource.mb": "5000",
        "mapreduce.map.memory.mb": "5000"
      },
      "additionalLinkedServiceNames": [
        "datafeeds",
        "adobedatafeed"
      ]
    }
  }
}
```

### <a name="node-sizes"></a><span data-ttu-id="26cbd-281">노드 크기</span><span class="sxs-lookup"><span data-stu-id="26cbd-281">Node sizes</span></span>
<span data-ttu-id="26cbd-282">다음과 같은 속성 hello를 사용 하 여 h e a d, 데이터 및 사육 노드의 hello 크기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-282">You can specify hello sizes of head, data, and zookeeper nodes using hello following properties:</span></span> 

| <span data-ttu-id="26cbd-283">속성</span><span class="sxs-lookup"><span data-stu-id="26cbd-283">Property</span></span> | <span data-ttu-id="26cbd-284">설명</span><span class="sxs-lookup"><span data-stu-id="26cbd-284">Description</span></span> | <span data-ttu-id="26cbd-285">필수</span><span class="sxs-lookup"><span data-stu-id="26cbd-285">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="26cbd-286">headNodeSize</span><span class="sxs-lookup"><span data-stu-id="26cbd-286">headNodeSize</span></span> |<span data-ttu-id="26cbd-287">Hello hello 헤드 노드 크기를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-287">Specifies hello size of hello head node.</span></span> <span data-ttu-id="26cbd-288">hello 기본값은: Standard_D3 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-288">hello default value is: Standard_D3.</span></span> <span data-ttu-id="26cbd-289">Hello 참조 **노드 크기를 지정** 자세한 내용은 섹션.</span><span class="sxs-lookup"><span data-stu-id="26cbd-289">See hello **Specifying node sizes** section for details.</span></span> |<span data-ttu-id="26cbd-290">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-290">No</span></span> |
| <span data-ttu-id="26cbd-291">dataNodeSize</span><span class="sxs-lookup"><span data-stu-id="26cbd-291">dataNodeSize</span></span> |<span data-ttu-id="26cbd-292">Hello 데이터 노드의 hello 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-292">Specifies hello size of hello data node.</span></span> <span data-ttu-id="26cbd-293">hello 기본값은: Standard_D3 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-293">hello default value is: Standard_D3.</span></span> |<span data-ttu-id="26cbd-294">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-294">No</span></span> |
| <span data-ttu-id="26cbd-295">zookeeperNodeSize</span><span class="sxs-lookup"><span data-stu-id="26cbd-295">zookeeperNodeSize</span></span> |<span data-ttu-id="26cbd-296">Hello Zoo 키퍼 노드의 hello 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-296">Specifies hello size of hello Zoo Keeper node.</span></span> <span data-ttu-id="26cbd-297">hello 기본값은: Standard_D3 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-297">hello default value is: Standard_D3.</span></span> |<span data-ttu-id="26cbd-298">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-298">No</span></span> |

#### <a name="specifying-node-sizes"></a><span data-ttu-id="26cbd-299">노드 크기 지정</span><span class="sxs-lookup"><span data-stu-id="26cbd-299">Specifying node sizes</span></span>
<span data-ttu-id="26cbd-300">Hello 참조 [가상 컴퓨터의 크기](../virtual-machines/linux/sizes.md) toospecify hello 이전 섹션에서 언급 한 hello 속성에 대 한 해야 하는 문자열 값에 대 한 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-300">See hello [Sizes of Virtual Machines](../virtual-machines/linux/sizes.md) article for string values you need toospecify for hello properties mentioned in hello previous section.</span></span> <span data-ttu-id="26cbd-301">hello 값 필요 tooconform toohello **Cmdlet 및 API** hello 문서에서 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-301">hello values need tooconform toohello **CMDLETs & APIS** referenced in hello article.</span></span> <span data-ttu-id="26cbd-302">Hello 문서의 보시 Large (기본값) 크기의 데이터 노드가 hello 시나리오에는 충분 하지 않을 수 있는 7 GB 메모리를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-302">As you can see in hello article, hello data node of Large (default) size has 7-GB memory, which may not be good enough for your scenario.</span></span> 

<span data-ttu-id="26cbd-303">D4 toocreate 작업자 노드 및 헤드 노드 크기를 지정 **Standard_D4** headNodeSize 및 dataNodeSize 속성에 대 한 hello 값으로.</span><span class="sxs-lookup"><span data-stu-id="26cbd-303">If you want toocreate D4 sized head nodes and worker nodes, specify **Standard_D4** as hello value for headNodeSize and dataNodeSize properties.</span></span> 

```json
"headNodeSize": "Standard_D4",    
"dataNodeSize": "Standard_D4",
```

<span data-ttu-id="26cbd-304">이러한 속성에 대 한 잘못 된 값을 지정 하면 hello 다음 나타날 수 있습니다 **오류:** toocreate 클러스터 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-304">If you specify a wrong value for these properties, you may receive hello following **error:** Failed toocreate cluster.</span></span> <span data-ttu-id="26cbd-305">예외: 수 없습니다 toocomplete hello 클러스터 만들기 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-305">Exception: Unable toocomplete hello cluster create operation.</span></span> <span data-ttu-id="26cbd-306">작업이 실패했습니다. 오류 코드는 '400'입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-306">Operation failed with code '400'.</span></span> <span data-ttu-id="26cbd-307">클러스터의 상태가 '오류'로 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-307">Cluster left behind state: 'Error'.</span></span> <span data-ttu-id="26cbd-308">메시지: 'PreClusterCreationValidationFailure'.</span><span class="sxs-lookup"><span data-stu-id="26cbd-308">Message: 'PreClusterCreationValidationFailure'.</span></span> <span data-ttu-id="26cbd-309">이 오류를 받으면 hello를 사용 하 고 있는지 확인 **CMDLET 및 API** hello hello 테이블에서 이름이 [가상 컴퓨터의 크기](../virtual-machines/linux/sizes.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="26cbd-309">When you receive this error, ensure that you are using hello **CMDLET & APIS** name from hello table in hello [Sizes of Virtual Machines](../virtual-machines/linux/sizes.md) article.</span></span>  

## <a name="bring-your-own-compute-environment"></a><span data-ttu-id="26cbd-310">사용자 고유의 계산 환경 가져오기</span><span class="sxs-lookup"><span data-stu-id="26cbd-310">Bring your own compute environment</span></span>
<span data-ttu-id="26cbd-311">이 구성의 형식에서는 사용자가 이미 기존 컴퓨팅 환경을 데이터 팩터리에서 연결된 서비스로 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-311">In this type of configuration, users can register an already existing computing environment as a linked service in Data Factory.</span></span> <span data-ttu-id="26cbd-312">hello 컴퓨팅 환경을 hello 사용자에 의해 관리 되는 데이터 팩터리 서비스 hello 사용 tooexecute hello 활동 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-312">hello computing environment is managed by hello user and hello Data Factory service uses it tooexecute hello activities.</span></span>

<span data-ttu-id="26cbd-313">이러한 유형의 구성 계산 환경 hello에서 다음에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-313">This type of configuration is supported for hello following compute environments:</span></span>

* <span data-ttu-id="26cbd-314">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="26cbd-314">Azure HDInsight</span></span>
* <span data-ttu-id="26cbd-315">Azure 배치</span><span class="sxs-lookup"><span data-stu-id="26cbd-315">Azure Batch</span></span>
* <span data-ttu-id="26cbd-316">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="26cbd-316">Azure Machine Learning</span></span>
* <span data-ttu-id="26cbd-317">Azure 데이터 레이크 분석</span><span class="sxs-lookup"><span data-stu-id="26cbd-317">Azure Data Lake Analytics</span></span>
* <span data-ttu-id="26cbd-318">Azure SQL DB, Azure SQL DW, SQL Server</span><span class="sxs-lookup"><span data-stu-id="26cbd-318">Azure SQL DB, Azure SQL DW, SQL Server</span></span>

## <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="26cbd-319">Azure HDInsight 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="26cbd-319">Azure HDInsight Linked Service</span></span>
<span data-ttu-id="26cbd-320">데이터 팩터리에 Azure HDInsight 연결 된 서비스 tooregister 고유한 HDInsight 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-320">You can create an Azure HDInsight linked service tooregister your own HDInsight cluster with Data Factory.</span></span>

### <a name="example"></a><span data-ttu-id="26cbd-321">예제</span><span class="sxs-lookup"><span data-stu-id="26cbd-321">Example</span></span>

```json
{
  "name": "HDInsightLinkedService",
  "properties": {
    "type": "HDInsight",
    "typeProperties": {
      "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
      "userName": "admin",
      "password": "<password>",
      "linkedServiceName": "MyHDInsightStoragelinkedService"
    }
  }
}
```

### <a name="properties"></a><span data-ttu-id="26cbd-322">속성</span><span class="sxs-lookup"><span data-stu-id="26cbd-322">Properties</span></span>
| <span data-ttu-id="26cbd-323">속성</span><span class="sxs-lookup"><span data-stu-id="26cbd-323">Property</span></span> | <span data-ttu-id="26cbd-324">설명</span><span class="sxs-lookup"><span data-stu-id="26cbd-324">Description</span></span> | <span data-ttu-id="26cbd-325">필수</span><span class="sxs-lookup"><span data-stu-id="26cbd-325">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26cbd-326">type</span><span class="sxs-lookup"><span data-stu-id="26cbd-326">type</span></span> |<span data-ttu-id="26cbd-327">너무 hello 유형 속성을 설정 해야**HDInsight**합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-327">hello type property should be set too**HDInsight**.</span></span> |<span data-ttu-id="26cbd-328">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-328">Yes</span></span> |
| <span data-ttu-id="26cbd-329">clusterUri</span><span class="sxs-lookup"><span data-stu-id="26cbd-329">clusterUri</span></span> |<span data-ttu-id="26cbd-330">hello hello HDInsight 클러스터의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-330">hello URI of hello HDInsight cluster.</span></span> |<span data-ttu-id="26cbd-331">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-331">Yes</span></span> |
| <span data-ttu-id="26cbd-332">username</span><span class="sxs-lookup"><span data-stu-id="26cbd-332">username</span></span> |<span data-ttu-id="26cbd-333">Tooconnect tooan 기존 HDInsight 클러스터를 사용 하는 hello 사용자 toobe의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-333">Specify hello name of hello user toobe used tooconnect tooan existing HDInsight cluster.</span></span> |<span data-ttu-id="26cbd-334">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-334">Yes</span></span> |
| <span data-ttu-id="26cbd-335">암호</span><span class="sxs-lookup"><span data-stu-id="26cbd-335">password</span></span> |<span data-ttu-id="26cbd-336">Hello 사용자 계정의 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-336">Specify password for hello user account.</span></span> |<span data-ttu-id="26cbd-337">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-337">Yes</span></span> |
| <span data-ttu-id="26cbd-338">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="26cbd-338">linkedServiceName</span></span> | <span data-ttu-id="26cbd-339">Hello HDInsight 클러스터의 hello toohello Azure blob 저장소를 참조 하는 Azure 저장소 연결 서비스의 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-339">Name of hello Azure Storage linked service that refers toohello Azure blob storage used by hello HDInsight cluster.</span></span> <p><span data-ttu-id="26cbd-340">현재 이 속성에 대한 Azure Data Lake Store 연결된 서비스를 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-340">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="26cbd-341">Hello HDInsight 클러스터에 데이터 레이크 저장소 액세스 toohello 경우 Hive/Pig 스크립트에서 hello Azure 데이터 레이크 저장소의에서 데이터를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-341">If hello HDInsight cluster has access toohello Data Lake Store, you may access data in hello Azure Data Lake Store from Hive/Pig scripts.</span></span> </p>  |<span data-ttu-id="26cbd-342">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-342">Yes</span></span> |

## <a name="azure-batch-linked-service"></a><span data-ttu-id="26cbd-343">Azure 일괄 처리 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="26cbd-343">Azure Batch Linked Service</span></span>
<span data-ttu-id="26cbd-344">Azure 배치 연결 서비스 tooregister 가상 컴퓨터 (Vm) tooa 데이터 팩터리의 일괄 처리 풀을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-344">You can create an Azure Batch linked service tooregister a Batch pool of virtual machines (VMs) tooa data factory.</span></span> <span data-ttu-id="26cbd-345">Azure 일괄 처리 또는 Azure HDInsight를 사용하여 .NET 사용자 지정 활동을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-345">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span>

<span data-ttu-id="26cbd-346">새 tooAzure 일괄 처리 서비스는 경우 다음 항목을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="26cbd-346">See following topics if you are new tooAzure Batch service:</span></span>

* <span data-ttu-id="26cbd-347">[Azure 배치 기본 사항](../batch/batch-technical-overview.md) hello Azure 배치 서비스에 대 한 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-347">[Azure Batch basics](../batch/batch-technical-overview.md) for an overview of hello Azure Batch service.</span></span>
* <span data-ttu-id="26cbd-348">[New-azurebatchaccount](https://msdn.microsoft.com/library/mt125880.aspx) cmdlet toocreate Azure 배치 계정 (또는) [Azure 포털](../batch/batch-account-create-portal.md) toocreate hello Azure 배치 계정을 Azure 포털을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-348">[New-AzureBatchAccount](https://msdn.microsoft.com/library/mt125880.aspx) cmdlet toocreate an Azure Batch account (or) [Azure portal](../batch/batch-account-create-portal.md) toocreate hello Azure Batch account using Azure portal.</span></span> <span data-ttu-id="26cbd-349">참조 [PowerShell 사용 하 여 Azure 배치 계정 toomanage](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) hello cmdlet을 사용 하는 자세한 방법은 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-349">See [Using PowerShell toomanage Azure Batch Account](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) topic for detailed instructions on using hello cmdlet.</span></span>
* <span data-ttu-id="26cbd-350">[New-azurebatchpool](https://msdn.microsoft.com/library/mt125936.aspx) cmdlet toocreate Azure 배치 풀 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-350">[New-AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) cmdlet toocreate an Azure Batch pool.</span></span>

### <a name="example"></a><span data-ttu-id="26cbd-351">예제</span><span class="sxs-lookup"><span data-stu-id="26cbd-351">Example</span></span>

```json
{
  "name": "AzureBatchLinkedService",
  "properties": {
    "type": "AzureBatch",
    "typeProperties": {
      "accountName": "<Azure Batch account name>",
      "accessKey": "<Azure Batch account key>",
      "poolName": "<Azure Batch pool name>",
      "linkedServiceName": "<Specify associated storage linked service reference here>"
    }
  }
}
```

<span data-ttu-id="26cbd-352">추가 "**.\< 지역 이름\>**"hello에 대 한 일괄 처리 계정 이름을 toohello **accountName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-352">Append "**.\<region name\>**" toohello name of your batch account for hello **accountName** property.</span></span> <span data-ttu-id="26cbd-353">예제:</span><span class="sxs-lookup"><span data-stu-id="26cbd-353">Example:</span></span>

```json
"accountName": "mybatchaccount.eastus"
```

<span data-ttu-id="26cbd-354">두 번째 방법은 tooprovide hello batchUri 끝점 hello 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="26cbd-354">Another option is tooprovide hello batchUri endpoint as shown in hello following sample:</span></span>

```json
"accountName": "adfteam",
"batchUri": "https://eastus.batch.azure.com",
```

### <a name="properties"></a><span data-ttu-id="26cbd-355">properties</span><span class="sxs-lookup"><span data-stu-id="26cbd-355">Properties</span></span>
| <span data-ttu-id="26cbd-356">속성</span><span class="sxs-lookup"><span data-stu-id="26cbd-356">Property</span></span> | <span data-ttu-id="26cbd-357">설명</span><span class="sxs-lookup"><span data-stu-id="26cbd-357">Description</span></span> | <span data-ttu-id="26cbd-358">필수</span><span class="sxs-lookup"><span data-stu-id="26cbd-358">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26cbd-359">type</span><span class="sxs-lookup"><span data-stu-id="26cbd-359">type</span></span> |<span data-ttu-id="26cbd-360">너무 hello 유형 속성을 설정 해야**AzureBatch**합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-360">hello type property should be set too**AzureBatch**.</span></span> |<span data-ttu-id="26cbd-361">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-361">Yes</span></span> |
| <span data-ttu-id="26cbd-362">accountName</span><span class="sxs-lookup"><span data-stu-id="26cbd-362">accountName</span></span> |<span data-ttu-id="26cbd-363">Azure 배치 계정 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-363">Name of hello Azure Batch account.</span></span> |<span data-ttu-id="26cbd-364">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-364">Yes</span></span> |
| <span data-ttu-id="26cbd-365">accessKey</span><span class="sxs-lookup"><span data-stu-id="26cbd-365">accessKey</span></span> |<span data-ttu-id="26cbd-366">Hello Azure 배치 계정에 대 한 액세스 키입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-366">Access key for hello Azure Batch account.</span></span> |<span data-ttu-id="26cbd-367">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-367">Yes</span></span> |
| <span data-ttu-id="26cbd-368">poolName</span><span class="sxs-lookup"><span data-stu-id="26cbd-368">poolName</span></span> |<span data-ttu-id="26cbd-369">가상 컴퓨터의 hello 풀의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-369">Name of hello pool of virtual machines.</span></span> |<span data-ttu-id="26cbd-370">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-370">Yes</span></span> |
| <span data-ttu-id="26cbd-371">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="26cbd-371">linkedServiceName</span></span> |<span data-ttu-id="26cbd-372">Hello이 Azure 배치 연결 된 서비스와 연결 된 Azure 저장소 연결 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-372">Name of hello Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="26cbd-373">준비 파일에 대 한이 연결 된 서비스는 필요한 toorun hello 활동 및 hello 활동 실행 로그를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-373">This linked service is used for staging files required toorun hello activity and storing hello activity execution logs.</span></span> |<span data-ttu-id="26cbd-374">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-374">Yes</span></span> |

## <a name="azure-machine-learning-linked-service"></a><span data-ttu-id="26cbd-375">Azure 기계 학습 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="26cbd-375">Azure Machine Learning Linked Service</span></span>
<span data-ttu-id="26cbd-376">Azure 기계 학습 연결 서비스 tooregister를 끝점 tooa 데이터 팩터리 점수 매기기 기계 학습 일괄 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-376">You create an Azure Machine Learning linked service tooregister a Machine Learning batch scoring endpoint tooa data factory.</span></span>

### <a name="example"></a><span data-ttu-id="26cbd-377">예제</span><span class="sxs-lookup"><span data-stu-id="26cbd-377">Example</span></span>

```json
{
  "name": "AzureMLLinkedService",
  "properties": {
    "type": "AzureML",
    "typeProperties": {
      "mlEndpoint": "https://[batch scoring endpoint]/jobs",
      "apiKey": "<apikey>"
    }
  }
}
```

### <a name="properties"></a><span data-ttu-id="26cbd-378">속성</span><span class="sxs-lookup"><span data-stu-id="26cbd-378">Properties</span></span>
| <span data-ttu-id="26cbd-379">속성</span><span class="sxs-lookup"><span data-stu-id="26cbd-379">Property</span></span> | <span data-ttu-id="26cbd-380">설명</span><span class="sxs-lookup"><span data-stu-id="26cbd-380">Description</span></span> | <span data-ttu-id="26cbd-381">필수</span><span class="sxs-lookup"><span data-stu-id="26cbd-381">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26cbd-382">형식</span><span class="sxs-lookup"><span data-stu-id="26cbd-382">Type</span></span> |<span data-ttu-id="26cbd-383">hello type 속성이로 설정 해야: **AzureML**합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-383">hello type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="26cbd-384">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-384">Yes</span></span> |
| <span data-ttu-id="26cbd-385">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="26cbd-385">mlEndpoint</span></span> |<span data-ttu-id="26cbd-386">hello 일괄 처리 첨 수 매기기 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-386">hello batch scoring URL.</span></span> |<span data-ttu-id="26cbd-387">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-387">Yes</span></span> |
| <span data-ttu-id="26cbd-388">apiKey</span><span class="sxs-lookup"><span data-stu-id="26cbd-388">apiKey</span></span> |<span data-ttu-id="26cbd-389">hello 작업 영역 모델의 API를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-389">hello published workspace model’s API.</span></span> |<span data-ttu-id="26cbd-390">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-390">Yes</span></span> |

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="26cbd-391">Azure 데이터 레이크 분석 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="26cbd-391">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="26cbd-392">만들 프로그램 **Azure 데이터 레이크 분석** 서비스 toolink Azure Data Lake 분석 계산 서비스 tooan Azure 데이터 팩터리에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-392">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory.</span></span> <span data-ttu-id="26cbd-393">데이터 레이크 분석 U-SQL 작업 hello 파이프라인의 hello toothis 연결 된 서비스를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-393">hello Data Lake Analytics U-SQL activity in hello pipeline refers toothis linked service.</span></span> 

<span data-ttu-id="26cbd-394">hello 다음 표에서 hello에 대 한 설명을 hello JSON 정의에서 사용 되는 일반 속성.</span><span class="sxs-lookup"><span data-stu-id="26cbd-394">hello following table provides descriptions for hello generic properties used in hello JSON definition.</span></span> <span data-ttu-id="26cbd-395">서비스 주체와 사용자 자격 증명 인증 중에서 추가로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-395">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="26cbd-396">속성</span><span class="sxs-lookup"><span data-stu-id="26cbd-396">Property</span></span> | <span data-ttu-id="26cbd-397">설명</span><span class="sxs-lookup"><span data-stu-id="26cbd-397">Description</span></span> | <span data-ttu-id="26cbd-398">필수</span><span class="sxs-lookup"><span data-stu-id="26cbd-398">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26cbd-399">**type**</span><span class="sxs-lookup"><span data-stu-id="26cbd-399">**type**</span></span> |<span data-ttu-id="26cbd-400">hello type 속성이로 설정 해야: **AzureDataLakeAnalytics**합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-400">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="26cbd-401">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-401">Yes</span></span> |
| <span data-ttu-id="26cbd-402">**accountName**</span><span class="sxs-lookup"><span data-stu-id="26cbd-402">**accountName**</span></span> |<span data-ttu-id="26cbd-403">Azure 데이터 레이크 분석 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-403">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="26cbd-404">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-404">Yes</span></span> |
| <span data-ttu-id="26cbd-405">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="26cbd-405">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="26cbd-406">Azure 데이터 레이크 분석 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-406">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="26cbd-407">아니요</span><span class="sxs-lookup"><span data-stu-id="26cbd-407">No</span></span> |
| <span data-ttu-id="26cbd-408">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="26cbd-408">**subscriptionId**</span></span> |<span data-ttu-id="26cbd-409">Azure 구독 ID</span><span class="sxs-lookup"><span data-stu-id="26cbd-409">Azure subscription id</span></span> |<span data-ttu-id="26cbd-410">아니요 (지정 하지 않으면 데이터 팩터리에 사용 되는 hello의 구독) 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="26cbd-410">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="26cbd-411">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="26cbd-411">**resourceGroupName**</span></span> |<span data-ttu-id="26cbd-412">Azure 리소스 그룹 이름</span><span class="sxs-lookup"><span data-stu-id="26cbd-412">Azure resource group name</span></span> |<span data-ttu-id="26cbd-413">아니요 (지정 하지 않으면 리소스 그룹의 데이터 팩터리에 사용 되는 hello) 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="26cbd-413">No (If not specified, resource group of hello data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="26cbd-414">서비스 주체 인증(권장)</span><span class="sxs-lookup"><span data-stu-id="26cbd-414">Service principal authentication (recommended)</span></span>
<span data-ttu-id="26cbd-415">toouse 서비스 보안 주체 인증 레지스터 것 hello Azure Active Directory (Azure AD) 및 권한 부여의 응용 프로그램 엔터티 tooData 레이크 스토어에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-415">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="26cbd-416">자세한 단계는 [서비스 간 인증](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26cbd-416">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="26cbd-417">사용 되는 값을 다음 hello 기록 toodefine hello 연결 된 서비스:</span><span class="sxs-lookup"><span data-stu-id="26cbd-417">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="26cbd-418">응용 프로그램 UI</span><span class="sxs-lookup"><span data-stu-id="26cbd-418">Application ID</span></span>
* <span data-ttu-id="26cbd-419">응용 프로그램 키</span><span class="sxs-lookup"><span data-stu-id="26cbd-419">Application key</span></span> 
* <span data-ttu-id="26cbd-420">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="26cbd-420">Tenant ID</span></span>

<span data-ttu-id="26cbd-421">Hello 다음과 같은 속성을 지정 하 여 서비스 사용자 인증을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-421">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="26cbd-422">속성</span><span class="sxs-lookup"><span data-stu-id="26cbd-422">Property</span></span> | <span data-ttu-id="26cbd-423">설명</span><span class="sxs-lookup"><span data-stu-id="26cbd-423">Description</span></span> | <span data-ttu-id="26cbd-424">필수</span><span class="sxs-lookup"><span data-stu-id="26cbd-424">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="26cbd-425">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="26cbd-425">**servicePrincipalId**</span></span> | <span data-ttu-id="26cbd-426">Hello 응용 프로그램의 클라이언트 ID를 지정</span><span class="sxs-lookup"><span data-stu-id="26cbd-426">Specify hello application's client ID.</span></span> | <span data-ttu-id="26cbd-427">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-427">Yes</span></span> |
| <span data-ttu-id="26cbd-428">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="26cbd-428">**servicePrincipalKey**</span></span> | <span data-ttu-id="26cbd-429">Hello 응용 프로그램의 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-429">Specify hello application's key.</span></span> | <span data-ttu-id="26cbd-430">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-430">Yes</span></span> |
| <span data-ttu-id="26cbd-431">**테넌트**</span><span class="sxs-lookup"><span data-stu-id="26cbd-431">**tenant**</span></span> | <span data-ttu-id="26cbd-432">응용 프로그램에 속한 아래 hello 테 넌 트 정보 (도메인 이름 또는 테 넌 트 ID)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-432">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="26cbd-433">Hello Azure 포털의 오른쪽 위 모서리 hello에에서 hello 마우스 호버 하 여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-433">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="26cbd-434">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-434">Yes</span></span> |

<span data-ttu-id="26cbd-435">**예제: 서비스 주체 인증**</span><span class="sxs-lookup"><span data-stu-id="26cbd-435">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="26cbd-436">사용자 자격 증명 인증</span><span class="sxs-lookup"><span data-stu-id="26cbd-436">User credential authentication</span></span>
<span data-ttu-id="26cbd-437">또는 hello 다음과 같은 속성을 지정 하 여 Data Lake 분석에 대 한 사용자 자격 증명 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-437">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying hello following properties:</span></span>

| <span data-ttu-id="26cbd-438">속성</span><span class="sxs-lookup"><span data-stu-id="26cbd-438">Property</span></span> | <span data-ttu-id="26cbd-439">설명</span><span class="sxs-lookup"><span data-stu-id="26cbd-439">Description</span></span> | <span data-ttu-id="26cbd-440">필수</span><span class="sxs-lookup"><span data-stu-id="26cbd-440">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="26cbd-441">**권한 부여**</span><span class="sxs-lookup"><span data-stu-id="26cbd-441">**authorization**</span></span> | <span data-ttu-id="26cbd-442">Hello 클릭 **Authorize** hello 데이터 팩터리 편집기 단추를 선택한 hello 자동 생성 된 권한 부여 URL toothis 속성을 할당 하 여 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-442">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="26cbd-443">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-443">Yes</span></span> |
| <span data-ttu-id="26cbd-444">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="26cbd-444">**sessionId**</span></span> | <span data-ttu-id="26cbd-445">Hello OAuth 권한 부여 세션에서 OAuth 세션 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-445">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="26cbd-446">각 세션 ID는 고유하고 한 번만 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-446">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="26cbd-447">이 설정은 hello 데이터 팩터리 편집기를 사용 하는 경우 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-447">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="26cbd-448">예</span><span class="sxs-lookup"><span data-stu-id="26cbd-448">Yes</span></span> |

<span data-ttu-id="26cbd-449">**예제: 사용자 자격 증명 인증**</span><span class="sxs-lookup"><span data-stu-id="26cbd-449">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="26cbd-450">토큰 만료</span><span class="sxs-lookup"><span data-stu-id="26cbd-450">Token expiration</span></span>
<span data-ttu-id="26cbd-451">hello를 사용 하 여 생성 하는 인증 코드를 hello **Authorize** 단추 잠시 후에 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-451">hello authorization code you generated by using hello **Authorize** button expires after sometime.</span></span> <span data-ttu-id="26cbd-452">다음 표에 다양 한 유형의 사용자 계정에 대 한 만료 시간 hello에 대 한 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="26cbd-452">See hello following table for hello expiration times for different types of user accounts.</span></span> <span data-ttu-id="26cbd-453">Hello 다음과 같은 오류 메시지가 표시 될 수 있습니다 때 인증 hello **토큰이 만료 된**: 작업 오류를 자격 증명: invalid_grant-AADSTS70002: 자격 증명 유효성 검사 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-453">You may see hello following error message when hello authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="26cbd-454">AADSTS70008: hello 액세스 권한 부여가 만료 되었거나 해지 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-454">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="26cbd-455">추적 ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 상관관계 ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 타임스탬프: 2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="26cbd-455">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="26cbd-456">사용자 유형</span><span class="sxs-lookup"><span data-stu-id="26cbd-456">User type</span></span> | <span data-ttu-id="26cbd-457">다음 시간 후에 만료</span><span class="sxs-lookup"><span data-stu-id="26cbd-457">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="26cbd-458">Azure Active Directory에서 관리되지 않는 사용자 계정(@hotmail.com, @live.com 등)</span><span class="sxs-lookup"><span data-stu-id="26cbd-458">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="26cbd-459">12시간</span><span class="sxs-lookup"><span data-stu-id="26cbd-459">12 hours</span></span> |
| <span data-ttu-id="26cbd-460">AAD(Azure Active Directory)에서 관리되는 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="26cbd-460">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="26cbd-461">hello 마지막 조각 실행 한 후 14 일입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-461">14 days after hello last slice run.</span></span> <br/><br/><span data-ttu-id="26cbd-462">OAuth 기반 연결된 서비스를 기반으로 하는 조각이 14일마다 한 번 이상 실행된 경우 90일</span><span class="sxs-lookup"><span data-stu-id="26cbd-462">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="26cbd-463">tooavoid/resolve이 오류를 hello를 사용 하 여 권한을 다시 부여 **Authorize** 때 hello 단추 **토큰이 만료 되** hello 연결 된 서비스를 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-463">tooavoid/resolve this error, reauthorize using hello **Authorize** button when hello **token expires** and redeploy hello linked service.</span></span> <span data-ttu-id="26cbd-464">다음과 같은 코드를 사용하여 프로그래밍 방식으로 **sessionId** 및 **권한 부여** 속성의 값을 생성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-464">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

<span data-ttu-id="26cbd-465">참조 [AzureDataLakeStoreLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), 및 [AuthorizationSessionGetResponse 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) 세부 정보에 대 한 항목 hello Data Factory 클래스 hello 코드에 사용 정보 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-465">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about hello Data Factory classes used in hello code.</span></span> <span data-ttu-id="26cbd-466">에 대 한 참조 추가: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll hello WindowsFormsWebAuthenticationDialog 클래스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-466">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for hello WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="azure-sql-linked-service"></a><span data-ttu-id="26cbd-467">Azure SQL 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="26cbd-467">Azure SQL Linked Service</span></span>
<span data-ttu-id="26cbd-468">Azure SQL 연결 서비스를 만들고 사용 하 여 hello로 [저장 프로시저 작업](data-factory-stored-proc-activity.md) tooinvoke 데이터 팩토리 파이프라인에서 저장된 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-468">You create an Azure SQL linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> <span data-ttu-id="26cbd-469">이 연결된 서비스에 대한 자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26cbd-469">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse-linked-service"></a><span data-ttu-id="26cbd-470">Azure SQL Data Warehouse 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="26cbd-470">Azure SQL Data Warehouse Linked Service</span></span>
<span data-ttu-id="26cbd-471">Azure SQL 데이터 웨어하우스 연결 된 서비스를 만들고 사용 하 여 hello로 [저장 프로시저 작업](data-factory-stored-proc-activity.md) tooinvoke 데이터 팩토리 파이프라인에서 저장된 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-471">You create an Azure SQL Data Warehouse linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> <span data-ttu-id="26cbd-472">이 연결된 서비스에 대한 자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26cbd-472">See [Azure SQL Data Warehouse Connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="sql-server-linked-service"></a><span data-ttu-id="26cbd-473">SQL Server 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="26cbd-473">SQL Server Linked Service</span></span>
<span data-ttu-id="26cbd-474">SQL Server 연결 된 서비스를 만들고 사용 하 여 hello로 [저장 프로시저 작업](data-factory-stored-proc-activity.md) tooinvoke 데이터 팩토리 파이프라인에서 저장된 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="26cbd-474">You create a SQL Server linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> <span data-ttu-id="26cbd-475">이 연결된 서비스에 대한 자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26cbd-475">See [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article for details about this linked service.</span></span>

