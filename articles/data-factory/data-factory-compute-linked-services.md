---
title: "Azure Data Factory에서 지원하는 컴퓨팅 환경 | Microsoft Docs"
description: "데이터의 변환 또는 처리를 위해 Azure Data Factory 파이프라인(예: Azure HDInsight)에서 사용할 수 있는 계산 환경을 알아봅니다."
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
ms.openlocfilehash: da7110614e684656da3ef9830780606e1576684d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="compute-environments-supported-by-azure-data-factory"></a><span data-ttu-id="7ae5f-103">Azure Data Factory에서 지원하는 컴퓨팅 환경</span><span class="sxs-lookup"><span data-stu-id="7ae5f-103">Compute environments supported by Azure Data Factory</span></span>
<span data-ttu-id="7ae5f-104">이 문서는 프로세스 또는 변환 데이터에 사용할 수 있는 다양한 계산 환경을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-104">This article explains different compute environments that you can use to process or transform data.</span></span> <span data-ttu-id="7ae5f-105">또한 이러한 계산 환경을 Azure 데이터 팩터리에 연결하는 연결된 서비스를 구성하는 경우 데이터 팩터리에서 지원하는 다른 구성(주문형 vs. 사용자 고유)에 대한 자세한 내용을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-105">It also provides details about different configurations (on-demand vs. bring your own) supported by Data Factory when configuring linked services linking these compute environments to an Azure data factory.</span></span>

<span data-ttu-id="7ae5f-106">다음 표는 Data Factory 및 실행할 수 있는 작업에서 지원하는 컴퓨팅 환경 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-106">The following table provides a list of compute environments supported by Data Factory and the activities that can run on them.</span></span> 

| <span data-ttu-id="7ae5f-107">컴퓨팅 환경</span><span class="sxs-lookup"><span data-stu-id="7ae5f-107">Compute environment</span></span> | <span data-ttu-id="7ae5f-108">작업</span><span class="sxs-lookup"><span data-stu-id="7ae5f-108">activities</span></span> |
| --- | --- |
| <span data-ttu-id="7ae5f-109">[주문형 HDInsight 클러스터](#azure-hdinsight-on-demand-linked-service) 또는 [사용자 고유의 HDInsight 클러스터](#azure-hdinsight-linked-service)</span><span class="sxs-lookup"><span data-stu-id="7ae5f-109">[On-demand HDInsight cluster](#azure-hdinsight-on-demand-linked-service) or [your own HDInsight cluster](#azure-hdinsight-linked-service)</span></span> |<span data-ttu-id="7ae5f-110">[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop 스트리밍](data-factory-hadoop-streaming-activity.md)</span><span class="sxs-lookup"><span data-stu-id="7ae5f-110">[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop Streaming](data-factory-hadoop-streaming-activity.md)</span></span> |
| [<span data-ttu-id="7ae5f-111">Azure 배치</span><span class="sxs-lookup"><span data-stu-id="7ae5f-111">Azure Batch</span></span>](#azure-batch-linked-service) |[<span data-ttu-id="7ae5f-112">DotNet</span><span class="sxs-lookup"><span data-stu-id="7ae5f-112">DotNet</span></span>](data-factory-use-custom-activities.md) |
| [<span data-ttu-id="7ae5f-113">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="7ae5f-113">Azure Machine Learning</span></span>](#azure-machine-learning-linked-service) |[<span data-ttu-id="7ae5f-114">Machine Learning 작업: 배치 실행 및 업데이트 리소스</span><span class="sxs-lookup"><span data-stu-id="7ae5f-114">Machine Learning activities: Batch Execution and Update Resource</span></span>](data-factory-azure-ml-batch-execution-activity.md) |
| [<span data-ttu-id="7ae5f-115">Azure 데이터 레이크 분석</span><span class="sxs-lookup"><span data-stu-id="7ae5f-115">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics-linked-service) |[<span data-ttu-id="7ae5f-116">데이터 레이크 분석 U-SQL</span><span class="sxs-lookup"><span data-stu-id="7ae5f-116">Data Lake Analytics U-SQL</span></span>](data-factory-usql-activity.md) |
| <span data-ttu-id="7ae5f-117">[Azure SQL](#azure-sql-linked-service), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-linked-service), [SQL Server](#sql-server-linked-service)</span><span class="sxs-lookup"><span data-stu-id="7ae5f-117">[Azure SQL](#azure-sql-linked-service), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-linked-service), [SQL Server](#sql-server-linked-service)</span></span> |[<span data-ttu-id="7ae5f-118">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="7ae5f-118">Stored Procedure</span></span>](data-factory-stored-proc-activity.md) |

## <a name="supported-hdinsight-versions-in-azure-data-factory"></a><span data-ttu-id="7ae5f-119">Azure Data Factory에서 지원되는 HDInsight 버전</span><span class="sxs-lookup"><span data-stu-id="7ae5f-119">Supported HDInsight versions in Azure Data Factory</span></span>
<span data-ttu-id="7ae5f-120">Azure HDInsight는 언제든 배포할 수 있는 여러 Hadoop 클러스터 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-120">Azure HDInsight supports multiple Hadoop cluster versions that can be deployed at any time.</span></span> <span data-ttu-id="7ae5f-121">각 버전을 선택하면 특정 버전의 HDP(Hortonworks Data Platform) 배포 및 배포에 포함된 구성 요소 집합이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-121">Each version choice creates a specific version of the Hortonworks Data Platform (HDP) distribution and a set of components that are contained within that distribution.</span></span> <span data-ttu-id="7ae5f-122">Microsoft는 지원되는 HDInsight 버전 목록을 계속 업데이트하여 최신 Hadoop 에코시스템 구성 요소 및 수정 프로그램을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-122">Microsoft keeps updating the list of supported versions of HDInsight to provide latest Hadoop ecosystem components and fixes.</span></span> <span data-ttu-id="7ae5f-123">HDInsight 3.2는 2017년 4월 1일부터 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-123">The HDInsight 3.2 is deprecated on April 1, 2017.</span></span> <span data-ttu-id="7ae5f-124">자세한 내용은 [지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-124">For detailed information, see [supported HDInsight versions](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>

<span data-ttu-id="7ae5f-125">이로 인해 HDInsight 3.2 클러스터에 대해 실행되는 활동이 있는 기존 Azure Data Factory에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-125">This impacts existing Azure Data Factories that have Activities running against HDInsight 3.2 clusters.</span></span> <span data-ttu-id="7ae5f-126">영향을 받는 Data Factory를 업데이트하려면 사용자는 다음 섹션의 지침을 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-126">We recommend users to follow the guidelines in the following section to update the impacted Data Factories:</span></span>

### <a name="for-linked-services-pointing-to-your-own-hdinsight-clusters"></a><span data-ttu-id="7ae5f-127">사용자 고유의 HDInsight 클러스터를 가리키는 연결된 서비스의 경우</span><span class="sxs-lookup"><span data-stu-id="7ae5f-127">For Linked Services pointing to your own HDInsight clusters</span></span>
* <span data-ttu-id="7ae5f-128">**사용자 고유의 HDInsight 3.2 이하 클러스터를 가리키는 HDInsight 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-128">**HDInsight Linked Services pointing to your own HDInsight 3.2 or below clusters:**</span></span>

  <span data-ttu-id="7ae5f-129">Azure Data Factory는 HDI 3.1에서 [최신의 지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)까지 사용자 고유의 HDInsight 클러스터에 제출하는 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-129">Azure Data Factory supports submitting jobs to your own HDInsight clusters from HDI 3.1 to [the latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span> <span data-ttu-id="7ae5f-130">그러나 [지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)에서 설명하는 사용 중단 정책에 따라 2017년 4월 1일 이후로는 더 이상 HDInsight 3.2 클러스터를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-130">However, you can no longer create HDInsight 3.2 cluster after April 1, 2017 based on the deprecation policy documented in [supported HDInsight versions](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>  

  <span data-ttu-id="7ae5f-131">**권장 사항:**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-131">**Recommendations:**</span></span> 
  * <span data-ttu-id="7ae5f-132">이 연결된 서비스를 참조하는 활동과 [최신의 지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)의 호환성을 보장하기 위해 [각 HDInsight 버전에서 제공되는 Hadoop 구성 요소](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) 및 [HDInsight 버전과 관련된 Hortonworks 릴리스 정보](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)에서 설명하는 정보와 함께 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-132">Perform tests to ensure the compatibility of the Activities that reference this Linked Services to [the latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) with information documented in [Hadoop components available with different HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) and [Hortonworks release notes associated with HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).</span></span>
  * <span data-ttu-id="7ae5f-133">HDInsight 3.2 클러스터를 [최신의 지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)으로 업그레이드하여 최신 Hadoop 에코시스템 구성 요소 및 수정 프로그램을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-133">Upgrade your HDInsight 3.2 cluster to [the latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) to get the latest Hadoop ecosystem components and fixes.</span></span> 

* <span data-ttu-id="7ae5f-134">**사용자 고유의 HDInsight 3.3 이상의 클러스터를 가리키는 HDInsight 연결된 서비스:**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-134">**HDInsight Linked Services pointing to your own HDInsight 3.3 or above clusters:**</span></span>

  <span data-ttu-id="7ae5f-135">Azure Data Factory는 HDI 3.1에서 [최신의 지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)까지 사용자 고유의 HDInsight 클러스터에 제출하는 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-135">Azure Data Factory supports submitting jobs to your own HDInsight clusters from HDI 3.1 to [the latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span> 
  
  <span data-ttu-id="7ae5f-136">**권장 사항:**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-136">**Recommendations:**</span></span> 
  * <span data-ttu-id="7ae5f-137">Data Factory 관점에서 보면 아무런 작업도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-137">No action is required from Data Factory perspective.</span></span> <span data-ttu-id="7ae5f-138">그러나 하위 버전의 HDInsight를 사용하는 경우에도 [최신의 지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)으로 업그레이드하여 최신 Hadoop 생태계 구성 요소 및 수정 프로그램을 얻는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-138">However, if you are on a lower version of HDInsight, we still recommend upgrading to [the latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) to get the latest Hadoop ecosystem components and fixes.</span></span>

### <a name="for-hdinsight-on-demand-linked-services"></a><span data-ttu-id="7ae5f-139">주문형 HDInsight 연결된 서비스의 경우</span><span class="sxs-lookup"><span data-stu-id="7ae5f-139">For HDInsight On-Demand Linked Services</span></span>
* <span data-ttu-id="7ae5f-140">**주문형 HDInsight 연결된 서비스 JSON 정의에 지정되어 있는 버전 3.2 이하:**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-140">**Version 3.2 or below is specified in HDInsight On-Demand Linked Services JSON definition:**</span></span>
  
  <span data-ttu-id="7ae5f-141">Azure Data Factory에서는 **2017년 5월 15일**부터 버전 3.3 이상의 주문형 HDInsight 클러스터 만들기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-141">Azure Data Factory will support creation of On-Demand HDInsight clusters of version 3.3 or more from **05/15/2017** onwards.</span></span> <span data-ttu-id="7ae5f-142">기존의 주문형 HDInsight 3.2 연결된 서비스에 대한 지원 종료는 **2017년 7월 15일**까지로 연장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-142">And, the end of support for existing on-demand HDInsight 3.2 linked services is extended to **07/15/2017**.</span></span>  

  <span data-ttu-id="7ae5f-143">**권장 사항:**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-143">**Recommendations:**</span></span> 
  * <span data-ttu-id="7ae5f-144">이 연결된 서비스를 참조하는 활동과 [최신의 지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)의 호환성을 보장하기 위해 [각 HDInsight 버전에서 제공되는 Hadoop 구성 요소](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) 및 [HDInsight 버전과 관련된 Hortonworks 릴리스 정보](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)에서 설명하는 정보와 함께 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-144">Perform tests to ensure the compatibility of the Activities that reference this Linked Services to  [the latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) with information documented in [Hadoop components available with different HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) and [Hortonworks release notes associated with HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).</span></span>
  * <span data-ttu-id="7ae5f-145">**2017년 7월 15일** 이전까지 주문형 HDI 연결된 서비스 JSON 정의의 Version 속성을 [최신의 지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)으로 업데이트하여 최신 Hadoop 생태계 구성 요소 및 수정 프로그램을 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-145">Before **07/15/2017**, update the Version property in On-Demand HDI Linked Service JSON definition to [the latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) to get the latest Hadoop ecosystem components and fixes.</span></span> <span data-ttu-id="7ae5f-146">JSON 정의에 대한 자세한 내용은 [주문형 Azure HDInsight 연결된 서비스 샘플](#azure-hdinsight-on-demand-linked-service)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-146">For detailed JSON definition, refer to the [Azure HDInsight On-Demand Linked Service sample](#azure-hdinsight-on-demand-linked-service).</span></span> 

* <span data-ttu-id="7ae5f-147">**주문형 HDInsight 연결된 서비스에 지정되지 않은 버전:**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-147">**Version not specified in On-Demand HDInsight Linked Services:**</span></span>
  
  <span data-ttu-id="7ae5f-148">Azure Data Factory에서는 **2017년 5월 15일**부터 버전 3.3 이상의 주문형 HDInsight 클러스터 만들기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-148">Azure Data Factory will support creation of on-demand HDInsight clusters of version 3.3 or more from **05/15/2017** onwards.</span></span> <span data-ttu-id="7ae5f-149">기존의 주문형 HDInsight 3.2 연결된 서비스에 대한 지원 종료는 **2017년 7월 15일**까지로 연장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-149">And, the end of support to existing on-demand HDInsight 3.2 linked services is extended to **07/15/2017**.</span></span> 

  <span data-ttu-id="7ae5f-150">**2017년 7월 15일** 이전까지 version 및 osType 속성의 값을 비워 두는 경우 해당 속성의 기본값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-150">Before **07/15/2017**, if left blank, the default values for version and osType properties are:</span></span> 

  | <span data-ttu-id="7ae5f-151">속성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-151">Property</span></span> | <span data-ttu-id="7ae5f-152">기본값</span><span class="sxs-lookup"><span data-stu-id="7ae5f-152">Default Value</span></span> | <span data-ttu-id="7ae5f-153">필수</span><span class="sxs-lookup"><span data-stu-id="7ae5f-153">Required</span></span> |
  | --- | --- | --- |
  <span data-ttu-id="7ae5f-154">버전</span><span class="sxs-lookup"><span data-stu-id="7ae5f-154">Version</span></span>   | <span data-ttu-id="7ae5f-155">Windows 클러스터용 HDI 3.1 및 Linux 클러스터용 HDI 3.2</span><span class="sxs-lookup"><span data-stu-id="7ae5f-155">HDI 3.1 for Windows cluster and HDI 3.2 for Linux cluster.</span></span>| <span data-ttu-id="7ae5f-156">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-156">No</span></span>
  <span data-ttu-id="7ae5f-157">osType</span><span class="sxs-lookup"><span data-stu-id="7ae5f-157">osType</span></span> | <span data-ttu-id="7ae5f-158">기본값: Windows</span><span class="sxs-lookup"><span data-stu-id="7ae5f-158">The default is Windows</span></span> | <span data-ttu-id="7ae5f-159">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-159">No</span></span>

  <span data-ttu-id="7ae5f-160">**2017년 7월 15일** 이후 version 및 osType 속성의 값을 비워 두는 경우 해당 속성의 기본값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-160">After **07/15/2017**, if left blank, the default values for version and osType properties are:</span></span>

  | <span data-ttu-id="7ae5f-161">속성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-161">Property</span></span> | <span data-ttu-id="7ae5f-162">기본값</span><span class="sxs-lookup"><span data-stu-id="7ae5f-162">Default Value</span></span> | <span data-ttu-id="7ae5f-163">필수</span><span class="sxs-lookup"><span data-stu-id="7ae5f-163">Required</span></span> |
  | --- | --- | --- |
  <span data-ttu-id="7ae5f-164">버전</span><span class="sxs-lookup"><span data-stu-id="7ae5f-164">Version</span></span>   | <span data-ttu-id="7ae5f-165">Windows 클러스터용 HDI 3.3 및 Linux 클러스터용 3.5.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-165">HDI 3.3 for Windows cluster and 3.5 for Linux cluster.</span></span>    | <span data-ttu-id="7ae5f-166">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-166">No</span></span>
  <span data-ttu-id="7ae5f-167">osType</span><span class="sxs-lookup"><span data-stu-id="7ae5f-167">osType</span></span> | <span data-ttu-id="7ae5f-168">기본값: Linux</span><span class="sxs-lookup"><span data-stu-id="7ae5f-168">The default is Linux</span></span> | <span data-ttu-id="7ae5f-169">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-169">No</span></span>

  <span data-ttu-id="7ae5f-170">**권장 사항:**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-170">**Recommendations:**</span></span> 
  * <span data-ttu-id="7ae5f-171">**2017년 7월 15일** 이전까지 이 연결된 서비스를 참조하는 활동과 [최신의 지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)의 호환성을 보장하기 위해 [각 HDInsight 버전에서 제공되는 Hadoop 구성 요소](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) 및 [HDInsight 버전과 관련된 Hortonworks 릴리스 정보](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)에서 설명하는 정보와 함께 테스트를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-171">Before **07/15/2017**, perform tests to ensure the compatibility of the Activities that reference this Linked Services to [the latest supported HDInsight version](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) with information documented in [Hadoop components available with different HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) and [Hortonworks release notes associated with HDInsight versions](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions).</span></span>  
  * <span data-ttu-id="7ae5f-172">**2017년 7월 15일** 이후 기본 설정을 재정의하려는 경우 osType 및 버전 값을 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-172">After **07/15/2017**, make sure you explicitly specify osType and version values if you would like to override the default settings.</span></span> 

>[!Note]
><span data-ttu-id="7ae5f-173">현재 Azure Data Factory는 Azure Data Lake Store를 기본 저장소로 사용하는 HDInsight 클러스터를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-173">Currently Azure Data Factory does not support HDInsight clusters using Azure Data Lake Store as primary store.</span></span> <span data-ttu-id="7ae5f-174">Azure Storage를 HDInsight 클러스터의 기본 저장소로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-174">Use Azure Storage as primary store for HDInsight clusters.</span></span> 
>  
>  

## <a name="on-demand-compute-environment"></a><span data-ttu-id="7ae5f-175">주문형 계산 환경</span><span class="sxs-lookup"><span data-stu-id="7ae5f-175">On-demand compute environment</span></span>
<span data-ttu-id="7ae5f-176">이 구성의 형식에서는 컴퓨팅 환경은 Azure 데이터 팩터리 서비스에 의해 완벽하게 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-176">In this type of configuration, the computing environment is fully managed by the Azure Data Factory service.</span></span> <span data-ttu-id="7ae5f-177">데이터를 처리하기 위한 작업을 제출하기 전에 데이터 팩터리 서비스에서 자동으로 컴퓨팅 환경을 만들고 작업이 완료되면 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-177">It is automatically created by the Data Factory service before a job is submitted to process data and removed when the job is completed.</span></span> <span data-ttu-id="7ae5f-178">사용자는 주문형 계산 환경에 대한 연결된 서비스를 만들고 구성하며 작업 실행, 클러스터 관리, 부트스트래핑 작업에 대한 세부적인 설정을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-178">You can create a linked service for the on-demand compute environment, configure it, and control granular settings for job execution, cluster management, and bootstrapping actions.</span></span>

> [!NOTE]
> <span data-ttu-id="7ae5f-179">주문형 구성은 현재 Azure HDInsight 클러스터에 대해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-179">The on-demand configuration is currently supported only for Azure HDInsight clusters.</span></span>
> 
> 

## <a name="azure-hdinsight-on-demand-linked-service"></a><span data-ttu-id="7ae5f-180">Azure HDInsight 주문형 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="7ae5f-180">Azure HDInsight On-Demand Linked Service</span></span>
<span data-ttu-id="7ae5f-181">Azure 데이터 팩터리 서비스는 데이터를 처리하는 Windows/Linux 기반 주문형 HDInsight 클러스터를 자동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-181">The Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster to process data.</span></span> <span data-ttu-id="7ae5f-182">클러스터는 클러스터와 연결된 저장소 계정(JSON에서 linkedServiceName 속성)과 동일한 하위 지역에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-182">The cluster is created in the same region as the storage account (linkedServiceName property in the JSON) associated with the cluster.</span></span> <span data-ttu-id="7ae5f-183">저장소 계정은 범용 표준 Azure Storage 계정이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-183">The storage account must be a general-purpose standard Azure storage account.</span></span> 

<span data-ttu-id="7ae5f-184">주문형 HDInsight 연결된 서비스에 대해 다음 **중요한** 점에 유의하십시오.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-184">Note the following **important** points about on-demand HDInsight linked service:</span></span>

* <span data-ttu-id="7ae5f-185">Azure 구독에서 만든 주문형 HDInsight 클러스터는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-185">You do not see the on-demand HDInsight cluster created in your Azure subscription.</span></span> <span data-ttu-id="7ae5f-186">Azure 데이터 팩터리 서비스는 사용자를 대신해 주문형 HDInsight 클러스터를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-186">the Azure Data Factory service manages the on-demand HDInsight cluster on your behalf.</span></span>
* <span data-ttu-id="7ae5f-187">주문형 HDInsight 클러스터에서 실행하는 작업에 대한 로그는 HDInsight 클러스터와 연결된 저장소 계정에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-187">The logs for jobs that are run on an on-demand HDInsight cluster are copied to the storage account associated with the HDInsight cluster.</span></span> <span data-ttu-id="7ae5f-188">**작업 실행 세부 정보** 블레이드의 Azure 포털에서 이러한 로그에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-188">You can access these logs from the Azure portal in the **Activity Run Details** blade.</span></span> <span data-ttu-id="7ae5f-189">세부 정보는 [파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 문서를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-189">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>
* <span data-ttu-id="7ae5f-190">HDInsight 클러스터가 작업을 실행 중인 경우에 대해서만 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-190">You are charged only for the time when the HDInsight cluster is up and running jobs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ae5f-191">주문형 Azure HDInsight 클러스터를 프로비전하는 데 일반적으로 **20분** 이상이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-191">It typically takes **20 minutes** or more to provision an Azure HDInsight cluster on demand.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="7ae5f-192">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-192">Example</span></span>
<span data-ttu-id="7ae5f-193">다음 JSON는 Linux 기반 주문형 HDInsight 연결된 서비스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-193">The following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="7ae5f-194">Data Factory 서비스는 데이터 조각을 처리하는 경우 **Linux 기반** HDInsight 클러스터를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-194">The Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

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

<span data-ttu-id="7ae5f-195">Windows 기반 HDInsight 클러스터를 사용하려면 **osType**을 **windows**로 설정하거나 기본값(windows)으로 속성을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-195">To use a Windows-based HDInsight cluster, set **osType** to **windows** or do not use the property as the default value is: windows.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="7ae5f-196">HDInsight 클러스터는 JSON(**linkedServiceName**)에서 지정한 Blob Storage에 **기본 컨테이너**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-196">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="7ae5f-197">HDInsight는 클러스터가 삭제될 때 이 컨테이너를 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-197">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="7ae5f-198">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-198">This behavior is by design.</span></span> <span data-ttu-id="7ae5f-199">주문형 HDInsight 연결된 서비스에서는 기존 라이브 클러스터(**timeToLive**)가 없는 한 슬라이스를 처리해야 할 때마다 HDInsight 클러스터가 만들어지며 처리가 완료되면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-199">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span> 
> 
> <span data-ttu-id="7ae5f-200">많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-200">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="7ae5f-201">작업의 문제 해결을 위해 이 항목들이 필요하지 않다면 저장소 비용을 줄이기 위해 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-201">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="7ae5f-202">이러한 컨테이너의 이름은 `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp` 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-202">The names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span></span> <span data-ttu-id="7ae5f-203">[Microsoft 저장소 탐색기](http://storageexplorer.com/) 같은 도구를 사용하여 Azure Blob Storage에서 컨테이너를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-203">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="7ae5f-204">속성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-204">Properties</span></span>
| <span data-ttu-id="7ae5f-205">속성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-205">Property</span></span> | <span data-ttu-id="7ae5f-206">설명</span><span class="sxs-lookup"><span data-stu-id="7ae5f-206">Description</span></span> | <span data-ttu-id="7ae5f-207">필수</span><span class="sxs-lookup"><span data-stu-id="7ae5f-207">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7ae5f-208">type</span><span class="sxs-lookup"><span data-stu-id="7ae5f-208">type</span></span> |<span data-ttu-id="7ae5f-209">형식 속성은 **HDInsightOnDemand**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-209">The type property should be set to **HDInsightOnDemand**.</span></span> |<span data-ttu-id="7ae5f-210">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-210">Yes</span></span> |
| <span data-ttu-id="7ae5f-211">clusterSize</span><span class="sxs-lookup"><span data-stu-id="7ae5f-211">clusterSize</span></span> |<span data-ttu-id="7ae5f-212">클러스터의 작업자/데이터 노드 수</span><span class="sxs-lookup"><span data-stu-id="7ae5f-212">Number of worker/data nodes in the cluster.</span></span> <span data-ttu-id="7ae5f-213">HDInsight 클러스터는 속성에 지정한 작업자 노드의 수와 함께 2개의 헤드 노드로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-213">The HDInsight cluster is created with 2 head nodes along with the number of worker nodes you specify for this property.</span></span> <span data-ttu-id="7ae5f-214">노드의 크기는 4개 코어를 포함한 Standard_D3이므로, 4개 작업자 노드 클러스터에서 24개 코어(작업자 노드용 4\*4 = 16코어 및 헤드 노드용 2\*4 = 8코어)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-214">The nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="7ae5f-215">Standard_D3 계층에 대한 자세한 내용은 [HDInsight에서 Linux 기반 Hadoop 클러스터 만들기](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-215">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about the Standard_D3 tier.</span></span> |<span data-ttu-id="7ae5f-216">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-216">Yes</span></span> |
| <span data-ttu-id="7ae5f-217">timetolive</span><span class="sxs-lookup"><span data-stu-id="7ae5f-217">timetolive</span></span> |<span data-ttu-id="7ae5f-218">주문형 HDInsight 클러스터에 대한 허용된 유휴 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-218">The allowed idle time for the on-demand HDInsight cluster.</span></span> <span data-ttu-id="7ae5f-219">클러스터에 다른 활성 작업이 없으면 작업이 완료된 후에 주문형 HDInsight 클러스터가 유지될 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-219">Specifies how long the on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in the cluster.</span></span><br/><br/><span data-ttu-id="7ae5f-220">예를 들어 활동 실행에 6분이 걸리고 timetolive이 5분으로 설정된 경우 클러스터는 활동을 처리하는 6분 동안 실행된 후에 5분 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-220">For example, if an activity run takes 6 minutes and timetolive is set to 5 minutes, the cluster stays alive for 5 minutes after the 6 minutes of processing the activity run.</span></span> <span data-ttu-id="7ae5f-221">다른 활동 실행이 6분 창을 실행하는 경우 동일한 클러스터에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-221">If another activity run is executed with the 6-minutes window, it is processed by the same cluster.</span></span><br/><br/><span data-ttu-id="7ae5f-222">주문형 HDInsight 클러스터를 만드는 데는 많은 시간이 걸려 값 비싼 작업이 되므로 필요할 때마다 이 설정을 사용하여 주문형 HDInsight 클러스터를 다시 사용함으로써 데이터 팩터리의 성능을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-222">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed to improve performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="7ae5f-223">timetolive 값을 0으로 설정한 경우 클러스터는 작업 실행이 완료되는 즉시 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-223">If you set timetolive value to 0, the cluster is deleted as soon as the activity run completes.</span></span> <span data-ttu-id="7ae5f-224">반면 높은 값을 설정하는 경우 클러스터는 불필요하게 많은 비용이 발생하는 유휴 상태에 머무를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-224">Whereas, if you set a high value, the cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="7ae5f-225">따라서 필요에 따라 적절한 값을 설정하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-225">Therefore, it is important that you set the appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="7ae5f-226">timetolive 속성 값이 적절하게 설정되는 경우 여러 파이프라인은 주문형 HDInsight 클러스터의 인스턴스를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-226">If the timetolive property value is appropriately set, multiple pipelines can share the instance of the on-demand HDInsight cluster.</span></span>  |<span data-ttu-id="7ae5f-227">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-227">Yes</span></span> |
| <span data-ttu-id="7ae5f-228">버전</span><span class="sxs-lookup"><span data-stu-id="7ae5f-228">version</span></span> |<span data-ttu-id="7ae5f-229">HDInsight 클러스터의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-229">Version of the HDInsight cluster.</span></span> <span data-ttu-id="7ae5f-230">기본값은 Windows 클러스터의 경우 3.1이고 Linux 클러스터의 경우 3.2입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-230">The default value is 3.1 for Windows cluster and 3.2 for Linux cluster.</span></span> |<span data-ttu-id="7ae5f-231">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-231">No</span></span> |
| <span data-ttu-id="7ae5f-232">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7ae5f-232">linkedServiceName</span></span> | <span data-ttu-id="7ae5f-233">데이터를 저장 및 처리하기 위해 주문형 클러스터에서 사용하는 Azure Storage 연결 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-233">Azure Storage linked service to be used by the on-demand cluster for storing and processing data.</span></span> <span data-ttu-id="7ae5f-234">HDInsight 클러스터는 Azure Storage 계정과 동일한 지역에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-234">The HDInsight cluster is created in the same region as this Azure Storage account.</span></span><p><span data-ttu-id="7ae5f-235">현재 Azure Data Lake Store를 저장소로 사용하는 주문형 HDInsight 클러스터를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-235">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as the storage.</span></span> <span data-ttu-id="7ae5f-236">HDInsight 처리의 결과 데이터를 Azure Data Lake Store에 저장하려면 복사 작업을 사용하여 Azure Blob Storage의 데이터를 Azure Data Lake Store로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-236">If you want to store the result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity to copy the data from the Azure Blob Storage to the Azure Data Lake Store.</span></span> </p>  | <span data-ttu-id="7ae5f-237">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-237">Yes</span></span> |
| <span data-ttu-id="7ae5f-238">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="7ae5f-238">additionalLinkedServiceNames</span></span> |<span data-ttu-id="7ae5f-239">HDInsight 연결된 서비스에 대한 추가 저장소 계정을 지정하므로 데이터 팩터리 서비스가 사용자를 대신해 계정을 등록할 수 있습니다. </span><span class="sxs-lookup"><span data-stu-id="7ae5f-239">Specifies additional storage accounts for the HDInsight linked service so that the Data Factory service can register them on your behalf.</span></span> <span data-ttu-id="7ae5f-240">이러한 저장소 계정은 linkedServiceName에 지정된 저장소 계정과 동일한 지역에 생성된 HDInsight 클러스터와 동일한 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-240">These storage accounts must be in the same region as the HDInsight cluster, which is created in the same region as the storage account specified by linkedServiceName.</span></span> |<span data-ttu-id="7ae5f-241">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-241">No</span></span> |
| <span data-ttu-id="7ae5f-242">osType</span><span class="sxs-lookup"><span data-stu-id="7ae5f-242">osType</span></span> |<span data-ttu-id="7ae5f-243">운영 체제 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-243">Type of operating system.</span></span> <span data-ttu-id="7ae5f-244">허용되는 값은 Windows(기본값) 및 Linux입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-244">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="7ae5f-245">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-245">No</span></span> |
| <span data-ttu-id="7ae5f-246">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7ae5f-246">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="7ae5f-247">HCatalog 데이터베이스를 가리키는 Azure SQL 연결된 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-247">The name of Azure SQL linked service that point to the HCatalog database.</span></span> <span data-ttu-id="7ae5f-248">주문형 HDInsight 클러스터는 Azure SQL Database를 metastore로 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-248">The on-demand HDInsight cluster is created by using the Azure SQL database as the metastore.</span></span> |<span data-ttu-id="7ae5f-249">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-249">No</span></span> |

#### <a name="additionallinkedservicenames-json-example"></a><span data-ttu-id="7ae5f-250">additionalLinkedServiceNames JSON 예제</span><span class="sxs-lookup"><span data-stu-id="7ae5f-250">additionalLinkedServiceNames JSON example</span></span>

```json
"additionalLinkedServiceNames": [
    "otherLinkedServiceName1",
    "otherLinkedServiceName2"
  ]
```

### <a name="advanced-properties"></a><span data-ttu-id="7ae5f-251">고급 속성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-251">Advanced Properties</span></span>
<span data-ttu-id="7ae5f-252">또한 주문형 HDInsight 클러스터의 세부적인 구성에 다음 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-252">You can also specify the following properties for the granular configuration of the on-demand HDInsight cluster.</span></span>

| <span data-ttu-id="7ae5f-253">속성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-253">Property</span></span> | <span data-ttu-id="7ae5f-254">설명</span><span class="sxs-lookup"><span data-stu-id="7ae5f-254">Description</span></span> | <span data-ttu-id="7ae5f-255">필수</span><span class="sxs-lookup"><span data-stu-id="7ae5f-255">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7ae5f-256">coreConfiguration</span><span class="sxs-lookup"><span data-stu-id="7ae5f-256">coreConfiguration</span></span> |<span data-ttu-id="7ae5f-257">만들어지는 HDInsight 클러스터에 대한 핵심 구성 매개 변수(core-site.xml에서 처럼)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-257">Specifies the core configuration parameters (as in core-site.xml) for the HDInsight cluster to be created.</span></span> |<span data-ttu-id="7ae5f-258">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-258">No</span></span> |
| <span data-ttu-id="7ae5f-259">hBaseConfiguration</span><span class="sxs-lookup"><span data-stu-id="7ae5f-259">hBaseConfiguration</span></span> |<span data-ttu-id="7ae5f-260">HDInsight 클러스터에 대한 HBase 구성 매개 변수(hbase-site.xml)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-260">Specifies the HBase configuration parameters (hbase-site.xml) for the HDInsight cluster.</span></span> |<span data-ttu-id="7ae5f-261">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-261">No</span></span> |
| <span data-ttu-id="7ae5f-262">hdfsConfiguration</span><span class="sxs-lookup"><span data-stu-id="7ae5f-262">hdfsConfiguration</span></span> |<span data-ttu-id="7ae5f-263">HDInsight 클러스터에 대한 HDFS 구성 매개 변수(hdfs-site.xml)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-263">Specifies the HDFS configuration parameters (hdfs-site.xml) for the HDInsight cluster.</span></span> |<span data-ttu-id="7ae5f-264">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-264">No</span></span> |
| <span data-ttu-id="7ae5f-265">hiveConfiguration</span><span class="sxs-lookup"><span data-stu-id="7ae5f-265">hiveConfiguration</span></span> |<span data-ttu-id="7ae5f-266">HDInsight 클러스터에 대한 hive 구성 매개 변수(hive-site.xml)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-266">Specifies the hive configuration parameters (hive-site.xml) for the HDInsight cluster.</span></span> |<span data-ttu-id="7ae5f-267">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-267">No</span></span> |
| <span data-ttu-id="7ae5f-268">mapReduceConfiguration</span><span class="sxs-lookup"><span data-stu-id="7ae5f-268">mapReduceConfiguration</span></span> |<span data-ttu-id="7ae5f-269">HDInsight 클러스터에 대한 MapReduce 구성 매개 변수(mapred-site.xml)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-269">Specifies the MapReduce configuration parameters (mapred-site.xml) for the HDInsight cluster.</span></span> |<span data-ttu-id="7ae5f-270">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-270">No</span></span> |
| <span data-ttu-id="7ae5f-271">oozieConfiguration</span><span class="sxs-lookup"><span data-stu-id="7ae5f-271">oozieConfiguration</span></span> |<span data-ttu-id="7ae5f-272">HDInsight 클러스터에 대한 Oozie 구성 매개 변수(oozie-site.xml)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-272">Specifies the Oozie configuration parameters (oozie-site.xml) for the HDInsight cluster.</span></span> |<span data-ttu-id="7ae5f-273">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-273">No</span></span> |
| <span data-ttu-id="7ae5f-274">stormConfiguration</span><span class="sxs-lookup"><span data-stu-id="7ae5f-274">stormConfiguration</span></span> |<span data-ttu-id="7ae5f-275">HDInsight 클러스터에 대한 Storm 구성 매개 변수(storm-site.xml)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-275">Specifies the Storm configuration parameters (storm-site.xml) for the HDInsight cluster.</span></span> |<span data-ttu-id="7ae5f-276">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-276">No</span></span> |
| <span data-ttu-id="7ae5f-277">yarnConfiguration</span><span class="sxs-lookup"><span data-stu-id="7ae5f-277">yarnConfiguration</span></span> |<span data-ttu-id="7ae5f-278">HDInsight 클러스터에 대한 Yarn 구성 매개 변수(yarn-site.xml)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-278">Specifies the Yarn configuration parameters (yarn-site.xml) for the HDInsight cluster.</span></span> |<span data-ttu-id="7ae5f-279">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-279">No</span></span> |

#### <a name="example--on-demand-hdinsight-cluster-configuration-with-advanced-properties"></a><span data-ttu-id="7ae5f-280">예제 - 고급 속성을 포함하는 주문형 HDInsight 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-280">Example – On-demand HDInsight cluster configuration with advanced properties</span></span>

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

### <a name="node-sizes"></a><span data-ttu-id="7ae5f-281">노드 크기</span><span class="sxs-lookup"><span data-stu-id="7ae5f-281">Node sizes</span></span>
<span data-ttu-id="7ae5f-282">다음 속성을 사용하여 헤드, 데이터 및 Zookeeper 노드의 크기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-282">You can specify the sizes of head, data, and zookeeper nodes using the following properties:</span></span> 

| <span data-ttu-id="7ae5f-283">속성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-283">Property</span></span> | <span data-ttu-id="7ae5f-284">설명</span><span class="sxs-lookup"><span data-stu-id="7ae5f-284">Description</span></span> | <span data-ttu-id="7ae5f-285">필수</span><span class="sxs-lookup"><span data-stu-id="7ae5f-285">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7ae5f-286">headNodeSize</span><span class="sxs-lookup"><span data-stu-id="7ae5f-286">headNodeSize</span></span> |<span data-ttu-id="7ae5f-287">헤드 노드의 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-287">Specifies the size of the head node.</span></span> <span data-ttu-id="7ae5f-288">기본값은 Standard_D3입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-288">The default value is: Standard_D3.</span></span> <span data-ttu-id="7ae5f-289">자세한 내용은 **노드 크기 지정** 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-289">See the **Specifying node sizes** section for details.</span></span> |<span data-ttu-id="7ae5f-290">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-290">No</span></span> |
| <span data-ttu-id="7ae5f-291">dataNodeSize</span><span class="sxs-lookup"><span data-stu-id="7ae5f-291">dataNodeSize</span></span> |<span data-ttu-id="7ae5f-292">데이터 노드의 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-292">Specifies the size of the data node.</span></span> <span data-ttu-id="7ae5f-293">기본값은 Standard_D3입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-293">The default value is: Standard_D3.</span></span> |<span data-ttu-id="7ae5f-294">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-294">No</span></span> |
| <span data-ttu-id="7ae5f-295">zookeeperNodeSize</span><span class="sxs-lookup"><span data-stu-id="7ae5f-295">zookeeperNodeSize</span></span> |<span data-ttu-id="7ae5f-296">Zookeeper 노드의 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-296">Specifies the size of the Zoo Keeper node.</span></span> <span data-ttu-id="7ae5f-297">기본값은 Standard_D3입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-297">The default value is: Standard_D3.</span></span> |<span data-ttu-id="7ae5f-298">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-298">No</span></span> |

#### <a name="specifying-node-sizes"></a><span data-ttu-id="7ae5f-299">노드 크기 지정</span><span class="sxs-lookup"><span data-stu-id="7ae5f-299">Specifying node sizes</span></span>
<span data-ttu-id="7ae5f-300">이전 섹션에 언급된 속성에 대해 지정해야 하는 문자열 값은 [가상 컴퓨터 크기](../virtual-machines/linux/sizes.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-300">See the [Sizes of Virtual Machines](../virtual-machines/linux/sizes.md) article for string values you need to specify for the properties mentioned in the previous section.</span></span> <span data-ttu-id="7ae5f-301">값은 이 문서에서 참조된 **Cmdlet 및 API**를 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-301">The values need to conform to the **CMDLETs & APIS** referenced in the article.</span></span> <span data-ttu-id="7ae5f-302">이 문서에서 볼 수 있는 것처럼 크게(기본값) 크기의 데이터 노드는 메모리가 7GB이므로 시나리오에 맞지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-302">As you can see in the article, the data node of Large (default) size has 7-GB memory, which may not be good enough for your scenario.</span></span> 

<span data-ttu-id="7ae5f-303">D4 크기의 헤드 노드 및 작업자 노드를 만들려는 경우 headNodeSize 및 dataNodeSize 속성에 대한 값으로 **Standard_D4**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-303">If you want to create D4 sized head nodes and worker nodes, specify **Standard_D4** as the value for headNodeSize and dataNodeSize properties.</span></span> 

```json
"headNodeSize": "Standard_D4",    
"dataNodeSize": "Standard_D4",
```

<span data-ttu-id="7ae5f-304">이러한 속성에 잘못된 값을 지정하는 경우 다음과 같은 오류가 발생할 수 있습니다. **오류:** 클러스터를 만들지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-304">If you specify a wrong value for these properties, you may receive the following **error:** Failed to create cluster.</span></span> <span data-ttu-id="7ae5f-305">예외: 클러스터 만들기 작업을 완료할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-305">Exception: Unable to complete the cluster create operation.</span></span> <span data-ttu-id="7ae5f-306">작업이 실패했습니다. 오류 코드는 '400'입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-306">Operation failed with code '400'.</span></span> <span data-ttu-id="7ae5f-307">클러스터의 상태가 '오류'로 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-307">Cluster left behind state: 'Error'.</span></span> <span data-ttu-id="7ae5f-308">메시지: 'PreClusterCreationValidationFailure'.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-308">Message: 'PreClusterCreationValidationFailure'.</span></span> <span data-ttu-id="7ae5f-309">이 오류가 발생하면 [가상 컴퓨터 크기](../virtual-machines/linux/sizes.md) 문서의 테이블에서 **CMDLET 및 API** 이름을 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-309">When you receive this error, ensure that you are using the **CMDLET & APIS** name from the table in the [Sizes of Virtual Machines](../virtual-machines/linux/sizes.md) article.</span></span>  

## <a name="bring-your-own-compute-environment"></a><span data-ttu-id="7ae5f-310">사용자 고유의 계산 환경 가져오기</span><span class="sxs-lookup"><span data-stu-id="7ae5f-310">Bring your own compute environment</span></span>
<span data-ttu-id="7ae5f-311">이 구성의 형식에서는 사용자가 이미 기존 컴퓨팅 환경을 데이터 팩터리에서 연결된 서비스로 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-311">In this type of configuration, users can register an already existing computing environment as a linked service in Data Factory.</span></span> <span data-ttu-id="7ae5f-312">컴퓨팅 환경은 이를 사용하여 작업을 실행하는 데이터 팩터리 서비스와 사용자에 의해 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-312">The computing environment is managed by the user and the Data Factory service uses it to execute the activities.</span></span>

<span data-ttu-id="7ae5f-313">이 구성의 형식은 다음의 계산 환경에 대해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-313">This type of configuration is supported for the following compute environments:</span></span>

* <span data-ttu-id="7ae5f-314">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ae5f-314">Azure HDInsight</span></span>
* <span data-ttu-id="7ae5f-315">Azure 배치</span><span class="sxs-lookup"><span data-stu-id="7ae5f-315">Azure Batch</span></span>
* <span data-ttu-id="7ae5f-316">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="7ae5f-316">Azure Machine Learning</span></span>
* <span data-ttu-id="7ae5f-317">Azure 데이터 레이크 분석</span><span class="sxs-lookup"><span data-stu-id="7ae5f-317">Azure Data Lake Analytics</span></span>
* <span data-ttu-id="7ae5f-318">Azure SQL DB, Azure SQL DW, SQL Server</span><span class="sxs-lookup"><span data-stu-id="7ae5f-318">Azure SQL DB, Azure SQL DW, SQL Server</span></span>

## <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="7ae5f-319">Azure HDInsight 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="7ae5f-319">Azure HDInsight Linked Service</span></span>
<span data-ttu-id="7ae5f-320">Azure HDInsight 연결된 서비스를 만들어서 데이터 팩터리를 사용하는 사용자 고유의 HDInsight 클러스터를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-320">You can create an Azure HDInsight linked service to register your own HDInsight cluster with Data Factory.</span></span>

### <a name="example"></a><span data-ttu-id="7ae5f-321">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-321">Example</span></span>

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

### <a name="properties"></a><span data-ttu-id="7ae5f-322">속성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-322">Properties</span></span>
| <span data-ttu-id="7ae5f-323">속성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-323">Property</span></span> | <span data-ttu-id="7ae5f-324">설명</span><span class="sxs-lookup"><span data-stu-id="7ae5f-324">Description</span></span> | <span data-ttu-id="7ae5f-325">필수</span><span class="sxs-lookup"><span data-stu-id="7ae5f-325">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7ae5f-326">type</span><span class="sxs-lookup"><span data-stu-id="7ae5f-326">type</span></span> |<span data-ttu-id="7ae5f-327">형식 속성은 **HDInsight**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-327">The type property should be set to **HDInsight**.</span></span> |<span data-ttu-id="7ae5f-328">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-328">Yes</span></span> |
| <span data-ttu-id="7ae5f-329">clusterUri</span><span class="sxs-lookup"><span data-stu-id="7ae5f-329">clusterUri</span></span> |<span data-ttu-id="7ae5f-330">HDInsight 클러스터의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-330">The URI of the HDInsight cluster.</span></span> |<span data-ttu-id="7ae5f-331">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-331">Yes</span></span> |
| <span data-ttu-id="7ae5f-332">username</span><span class="sxs-lookup"><span data-stu-id="7ae5f-332">username</span></span> |<span data-ttu-id="7ae5f-333">기존 HDInsight 클러스터에 연결하는데 사용할 사용자의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-333">Specify the name of the user to be used to connect to an existing HDInsight cluster.</span></span> |<span data-ttu-id="7ae5f-334">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-334">Yes</span></span> |
| <span data-ttu-id="7ae5f-335">password</span><span class="sxs-lookup"><span data-stu-id="7ae5f-335">password</span></span> |<span data-ttu-id="7ae5f-336">사용자 계정으로 password를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-336">Specify password for the user account.</span></span> |<span data-ttu-id="7ae5f-337">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-337">Yes</span></span> |
| <span data-ttu-id="7ae5f-338">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7ae5f-338">linkedServiceName</span></span> | <span data-ttu-id="7ae5f-339">HDInsight 클러스터에서 사용하는 Azure Blob Storage를 참조하는 Azure Storage 연결된 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-339">Name of the Azure Storage linked service that refers to the Azure blob storage used by the HDInsight cluster.</span></span> <p><span data-ttu-id="7ae5f-340">현재 이 속성에 대한 Azure Data Lake Store 연결된 서비스를 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-340">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="7ae5f-341">HDInsight 클러스터가 Data Lake Store에 액세스할 경우 Hive/Pig 스크립트의 Azure Data Lake Store에 있는 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-341">If the HDInsight cluster has access to the Data Lake Store, you may access data in the Azure Data Lake Store from Hive/Pig scripts.</span></span> </p>  |<span data-ttu-id="7ae5f-342">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-342">Yes</span></span> |

## <a name="azure-batch-linked-service"></a><span data-ttu-id="7ae5f-343">Azure 일괄 처리 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="7ae5f-343">Azure Batch Linked Service</span></span>
<span data-ttu-id="7ae5f-344">Azure 일괄 처리 연결된 서비스를 만들어 데이터 팩터리에 가상 컴퓨터(VM)의 일괄 처리 풀을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-344">You can create an Azure Batch linked service to register a Batch pool of virtual machines (VMs) to a data factory.</span></span> <span data-ttu-id="7ae5f-345">Azure 일괄 처리 또는 Azure HDInsight를 사용하여 .NET 사용자 지정 활동을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-345">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span>

<span data-ttu-id="7ae5f-346">Azure 배치 서비스가 처음이라면 다음 항목을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-346">See following topics if you are new to Azure Batch service:</span></span>

* <span data-ttu-id="7ae5f-347">[Azure 배치 기본 사항](../batch/batch-technical-overview.md) 입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-347">[Azure Batch basics](../batch/batch-technical-overview.md) for an overview of the Azure Batch service.</span></span>
* <span data-ttu-id="7ae5f-348">Azure 배치 계정을 만드는 [New-AzureBatchAccount](https://msdn.microsoft.com/library/mt125880.aspx) cmdlet 또는 Azure 배치 계정을 만드는 [Azure Portal](../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7ae5f-348">[New-AzureBatchAccount](https://msdn.microsoft.com/library/mt125880.aspx) cmdlet to create an Azure Batch account (or) [Azure portal](../batch/batch-account-create-portal.md) to create the Azure Batch account using Azure portal.</span></span> <span data-ttu-id="7ae5f-349">이 cmdlet 사용에 관한 자세한 지침은 [PowerShell을 사용하여 Azure Batch 계정 관리](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) 항목을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-349">See [Using PowerShell to manage Azure Batch Account](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) topic for detailed instructions on using the cmdlet.</span></span>
* <span data-ttu-id="7ae5f-350">[New-AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) cmdlet을 사용하여 Azure 배치 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-350">[New-AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) cmdlet to create an Azure Batch pool.</span></span>

### <a name="example"></a><span data-ttu-id="7ae5f-351">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-351">Example</span></span>

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

<span data-ttu-id="7ae5f-352">**accountName** 속성의 배치 계정의 이름에 "**.\<region name\>**"을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-352">Append "**.\<region name\>**" to the name of your batch account for the **accountName** property.</span></span> <span data-ttu-id="7ae5f-353">예제:</span><span class="sxs-lookup"><span data-stu-id="7ae5f-353">Example:</span></span>

```json
"accountName": "mybatchaccount.eastus"
```

<span data-ttu-id="7ae5f-354">다른 옵션은 다음 샘플에 표시된 것처럼 batchUri 끝점을 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-354">Another option is to provide the batchUri endpoint as shown in the following sample:</span></span>

```json
"accountName": "adfteam",
"batchUri": "https://eastus.batch.azure.com",
```

### <a name="properties"></a><span data-ttu-id="7ae5f-355">속성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-355">Properties</span></span>
| <span data-ttu-id="7ae5f-356">속성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-356">Property</span></span> | <span data-ttu-id="7ae5f-357">설명</span><span class="sxs-lookup"><span data-stu-id="7ae5f-357">Description</span></span> | <span data-ttu-id="7ae5f-358">필수</span><span class="sxs-lookup"><span data-stu-id="7ae5f-358">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7ae5f-359">type</span><span class="sxs-lookup"><span data-stu-id="7ae5f-359">type</span></span> |<span data-ttu-id="7ae5f-360">형식 속성은 **AzureBatch**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-360">The type property should be set to **AzureBatch**.</span></span> |<span data-ttu-id="7ae5f-361">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-361">Yes</span></span> |
| <span data-ttu-id="7ae5f-362">accountName</span><span class="sxs-lookup"><span data-stu-id="7ae5f-362">accountName</span></span> |<span data-ttu-id="7ae5f-363">Azure Batch 계정의 이름</span><span class="sxs-lookup"><span data-stu-id="7ae5f-363">Name of the Azure Batch account.</span></span> |<span data-ttu-id="7ae5f-364">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-364">Yes</span></span> |
| <span data-ttu-id="7ae5f-365">accessKey</span><span class="sxs-lookup"><span data-stu-id="7ae5f-365">accessKey</span></span> |<span data-ttu-id="7ae5f-366">Azure Batch 계정에 대한 선택키</span><span class="sxs-lookup"><span data-stu-id="7ae5f-366">Access key for the Azure Batch account.</span></span> |<span data-ttu-id="7ae5f-367">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-367">Yes</span></span> |
| <span data-ttu-id="7ae5f-368">poolName</span><span class="sxs-lookup"><span data-stu-id="7ae5f-368">poolName</span></span> |<span data-ttu-id="7ae5f-369">가상 컴퓨터의 풀 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-369">Name of the pool of virtual machines.</span></span> |<span data-ttu-id="7ae5f-370">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-370">Yes</span></span> |
| <span data-ttu-id="7ae5f-371">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7ae5f-371">linkedServiceName</span></span> |<span data-ttu-id="7ae5f-372">Azure 일괄 처리 연결된 서비스와 관련된 Azure 저장소 연결된 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-372">Name of the Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="7ae5f-373">이 연결된 서비스는 활동을 실행하는 데 필요한 파일을 스테이징하고 활동 실행 로그를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-373">This linked service is used for staging files required to run the activity and storing the activity execution logs.</span></span> |<span data-ttu-id="7ae5f-374">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-374">Yes</span></span> |

## <a name="azure-machine-learning-linked-service"></a><span data-ttu-id="7ae5f-375">Azure 기계 학습 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="7ae5f-375">Azure Machine Learning Linked Service</span></span>
<span data-ttu-id="7ae5f-376">Azure 컴퓨터 학습 연결된 서비스를 만들어 데이터 팩토리에 끝점을 매기는 기계 학습 일괄 처리를 등록합니다. </span><span class="sxs-lookup"><span data-stu-id="7ae5f-376">You create an Azure Machine Learning linked service to register a Machine Learning batch scoring endpoint to a data factory.</span></span>

### <a name="example"></a><span data-ttu-id="7ae5f-377">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-377">Example</span></span>

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

### <a name="properties"></a><span data-ttu-id="7ae5f-378">속성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-378">Properties</span></span>
| <span data-ttu-id="7ae5f-379">속성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-379">Property</span></span> | <span data-ttu-id="7ae5f-380">설명</span><span class="sxs-lookup"><span data-stu-id="7ae5f-380">Description</span></span> | <span data-ttu-id="7ae5f-381">필수</span><span class="sxs-lookup"><span data-stu-id="7ae5f-381">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7ae5f-382">type</span><span class="sxs-lookup"><span data-stu-id="7ae5f-382">Type</span></span> |<span data-ttu-id="7ae5f-383">형식 속성은 **AzureML**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-383">The type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="7ae5f-384">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-384">Yes</span></span> |
| <span data-ttu-id="7ae5f-385">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="7ae5f-385">mlEndpoint</span></span> |<span data-ttu-id="7ae5f-386">일괄 처리 점수 매기기 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-386">The batch scoring URL.</span></span> |<span data-ttu-id="7ae5f-387">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-387">Yes</span></span> |
| <span data-ttu-id="7ae5f-388">apiKey</span><span class="sxs-lookup"><span data-stu-id="7ae5f-388">apiKey</span></span> |<span data-ttu-id="7ae5f-389">게시된 작업 영역 모델의 API입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-389">The published workspace model’s API.</span></span> |<span data-ttu-id="7ae5f-390">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-390">Yes</span></span> |

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="7ae5f-391">Azure 데이터 레이크 분석 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="7ae5f-391">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="7ae5f-392">Azure 데이터 레이크 분석 계산 서비스와 Azure Data Factory에 연결하는 **Azure 데이터 레이크 분석** 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-392">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory.</span></span> <span data-ttu-id="7ae5f-393">파이프라인에서 데이터 레이크 분석 U-SQL 작업은 이 연결된 서비스를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-393">The Data Lake Analytics U-SQL activity in the pipeline refers to this linked service.</span></span> 

<span data-ttu-id="7ae5f-394">다음 표에는 JSON 정의에서 사용하는 일반 속성에 대한 설명이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-394">The following table provides descriptions for the generic properties used in the JSON definition.</span></span> <span data-ttu-id="7ae5f-395">서비스 주체와 사용자 자격 증명 인증 중에서 추가로 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-395">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="7ae5f-396">속성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-396">Property</span></span> | <span data-ttu-id="7ae5f-397">설명</span><span class="sxs-lookup"><span data-stu-id="7ae5f-397">Description</span></span> | <span data-ttu-id="7ae5f-398">필수</span><span class="sxs-lookup"><span data-stu-id="7ae5f-398">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7ae5f-399">**type**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-399">**type**</span></span> |<span data-ttu-id="7ae5f-400">type 속성은 **AzureDataLakeAnalytics**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-400">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="7ae5f-401">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-401">Yes</span></span> |
| <span data-ttu-id="7ae5f-402">**accountName**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-402">**accountName**</span></span> |<span data-ttu-id="7ae5f-403">Azure 데이터 레이크 분석 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-403">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="7ae5f-404">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-404">Yes</span></span> |
| <span data-ttu-id="7ae5f-405">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-405">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="7ae5f-406">Azure 데이터 레이크 분석 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-406">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="7ae5f-407">아니요</span><span class="sxs-lookup"><span data-stu-id="7ae5f-407">No</span></span> |
| <span data-ttu-id="7ae5f-408">**subscriptionId**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-408">**subscriptionId**</span></span> |<span data-ttu-id="7ae5f-409">Azure 구독 ID</span><span class="sxs-lookup"><span data-stu-id="7ae5f-409">Azure subscription id</span></span> |<span data-ttu-id="7ae5f-410">아니요(지정하지 않으면 Data Factory의 구독이 사용됨).</span><span class="sxs-lookup"><span data-stu-id="7ae5f-410">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="7ae5f-411">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-411">**resourceGroupName**</span></span> |<span data-ttu-id="7ae5f-412">Azure 리소스 그룹 이름</span><span class="sxs-lookup"><span data-stu-id="7ae5f-412">Azure resource group name</span></span> |<span data-ttu-id="7ae5f-413">아니요(지정하지 않으면 Data Factory의 리소스 그룹이 사용됨).</span><span class="sxs-lookup"><span data-stu-id="7ae5f-413">No (If not specified, resource group of the data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="7ae5f-414">서비스 주체 인증(권장)</span><span class="sxs-lookup"><span data-stu-id="7ae5f-414">Service principal authentication (recommended)</span></span>
<span data-ttu-id="7ae5f-415">서비스 주체 인증을 사용하려면 Azure AD(Azure Active Directory)에서 응용 프로그램 엔터티를 등록한 후 Data Lake Store에서 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-415">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="7ae5f-416">자세한 단계는 [서비스 간 인증](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-416">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="7ae5f-417">연결된 서비스를 정의하는 데 사용되므로 다음 값을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-417">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="7ae5f-418">응용 프로그램 UI</span><span class="sxs-lookup"><span data-stu-id="7ae5f-418">Application ID</span></span>
* <span data-ttu-id="7ae5f-419">응용 프로그램 키</span><span class="sxs-lookup"><span data-stu-id="7ae5f-419">Application key</span></span> 
* <span data-ttu-id="7ae5f-420">테넌트 ID</span><span class="sxs-lookup"><span data-stu-id="7ae5f-420">Tenant ID</span></span>

<span data-ttu-id="7ae5f-421">다음 속성을 지정하여 서비스 주체 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-421">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="7ae5f-422">속성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-422">Property</span></span> | <span data-ttu-id="7ae5f-423">설명</span><span class="sxs-lookup"><span data-stu-id="7ae5f-423">Description</span></span> | <span data-ttu-id="7ae5f-424">필수</span><span class="sxs-lookup"><span data-stu-id="7ae5f-424">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7ae5f-425">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-425">**servicePrincipalId**</span></span> | <span data-ttu-id="7ae5f-426">응용 프로그램의 클라이언트 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-426">Specify the application's client ID.</span></span> | <span data-ttu-id="7ae5f-427">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-427">Yes</span></span> |
| <span data-ttu-id="7ae5f-428">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-428">**servicePrincipalKey**</span></span> | <span data-ttu-id="7ae5f-429">응용 프로그램의 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-429">Specify the application's key.</span></span> | <span data-ttu-id="7ae5f-430">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-430">Yes</span></span> |
| <span data-ttu-id="7ae5f-431">**테넌트**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-431">**tenant**</span></span> | <span data-ttu-id="7ae5f-432">응용 프로그램이 있는 테넌트 정보(도메인 이름 또는 테넌트 ID)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-432">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="7ae5f-433">Azure Portal의 오른쪽 위 모서리에 마우스를 이동하여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-433">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="7ae5f-434">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-434">Yes</span></span> |

<span data-ttu-id="7ae5f-435">**예제: 서비스 주체 인증**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-435">**Example: Service principal authentication**</span></span>
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

### <a name="user-credential-authentication"></a><span data-ttu-id="7ae5f-436">사용자 자격 증명 인증</span><span class="sxs-lookup"><span data-stu-id="7ae5f-436">User credential authentication</span></span>
<span data-ttu-id="7ae5f-437">또는 다음 속성을 지정하여 Data Lake Analytics에 대해 사용자 자격 증명 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-437">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying the following properties:</span></span>

| <span data-ttu-id="7ae5f-438">속성</span><span class="sxs-lookup"><span data-stu-id="7ae5f-438">Property</span></span> | <span data-ttu-id="7ae5f-439">설명</span><span class="sxs-lookup"><span data-stu-id="7ae5f-439">Description</span></span> | <span data-ttu-id="7ae5f-440">필수</span><span class="sxs-lookup"><span data-stu-id="7ae5f-440">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="7ae5f-441">**권한 부여**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-441">**authorization**</span></span> | <span data-ttu-id="7ae5f-442">Data Factory 편집기에서 **권한 부여** 단추를 클릭하고 자격 증명을 입력합니다. 그러면 자동 생성된 authorization URL이 이 속성에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-442">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="7ae5f-443">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-443">Yes</span></span> |
| <span data-ttu-id="7ae5f-444">**sessionId**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-444">**sessionId**</span></span> | <span data-ttu-id="7ae5f-445">OAuth 권한 부여 세션에서 가져온 OAuth 세션 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-445">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="7ae5f-446">각 세션 ID는 고유하고 한 번만 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-446">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="7ae5f-447">이 설정은 Data Factory 편집기를 사용하는 경우 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-447">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="7ae5f-448">예</span><span class="sxs-lookup"><span data-stu-id="7ae5f-448">Yes</span></span> |

<span data-ttu-id="7ae5f-449">**예제: 사용자 자격 증명 인증**</span><span class="sxs-lookup"><span data-stu-id="7ae5f-449">**Example: User credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="7ae5f-450">토큰 만료</span><span class="sxs-lookup"><span data-stu-id="7ae5f-450">Token expiration</span></span>
<span data-ttu-id="7ae5f-451">**권한 부여** 단추를 사용하여 생성된 인증 코드는 잠시 후 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-451">The authorization code you generated by using the **Authorize** button expires after sometime.</span></span> <span data-ttu-id="7ae5f-452">다양한 유형의 사용자 계정에 대한 만료 시간은 다음 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-452">See the following table for the expiration times for different types of user accounts.</span></span> <span data-ttu-id="7ae5f-453">인증 **토큰이 만료**되는 경우 다음과 같은 오류 메시지가 표시될 수 있습니다. 자격 증명 작업 오류: invalid_grant - AADSTS70002: 자격 증명 유효성 검사 오류.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-453">You may see the following error message when the authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="7ae5f-454">"자격 증명 작업 오류: invalid_grant - AADSTS70002: 자격 증명의 유효성 검사 오류 AADSTS70008: 제공된 액세스 권한 부여가 만료되었거나 해지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-454">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="7ae5f-455">추적 ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 상관관계 ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 타임스탬프: 2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="7ae5f-455">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="7ae5f-456">사용자 유형</span><span class="sxs-lookup"><span data-stu-id="7ae5f-456">User type</span></span> | <span data-ttu-id="7ae5f-457">다음 시간 후에 만료</span><span class="sxs-lookup"><span data-stu-id="7ae5f-457">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="7ae5f-458">Azure Active Directory에서 관리되지 않는 사용자 계정(@hotmail.com, @live.com 등)</span><span class="sxs-lookup"><span data-stu-id="7ae5f-458">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="7ae5f-459">12시간</span><span class="sxs-lookup"><span data-stu-id="7ae5f-459">12 hours</span></span> |
| <span data-ttu-id="7ae5f-460">AAD(Azure Active Directory)에서 관리되는 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="7ae5f-460">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="7ae5f-461">마지막 조각이 실행된 후 14일</span><span class="sxs-lookup"><span data-stu-id="7ae5f-461">14 days after the last slice run.</span></span> <br/><br/><span data-ttu-id="7ae5f-462">OAuth 기반 연결된 서비스를 기반으로 하는 조각이 14일마다 한 번 이상 실행된 경우 90일</span><span class="sxs-lookup"><span data-stu-id="7ae5f-462">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="7ae5f-463">이 오류를 방지/해결하려면 **토큰이 만료**되면 **권한 부여** 단추를 사용하여 다시 인증하고 연결된 서비스를 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-463">To avoid/resolve this error, reauthorize using the **Authorize** button when the **token expires** and redeploy the linked service.</span></span> <span data-ttu-id="7ae5f-464">다음과 같은 코드를 사용하여 프로그래밍 방식으로 **sessionId** 및 **권한 부여** 속성의 값을 생성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-464">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

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

<span data-ttu-id="7ae5f-465">코드에 사용되는 Data Factory 클래스에 대한 세부 정보는 [AzureDataLakeStoreLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx) 및 [AuthorizationSessionGetResponse 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-465">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about the Data Factory classes used in the code.</span></span> <span data-ttu-id="7ae5f-466">WindowsFormsWebAuthenticationDialog 클래스의 Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-466">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for the WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="azure-sql-linked-service"></a><span data-ttu-id="7ae5f-467">Azure SQL 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="7ae5f-467">Azure SQL Linked Service</span></span>
<span data-ttu-id="7ae5f-468">Azure SQL 연결된 서비스를 만들고 [저장 프로시저 활동](data-factory-stored-proc-activity.md) 에서 사용하여 Data Factory 파이프라인에서 저장 프로시저를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-468">You create an Azure SQL linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> <span data-ttu-id="7ae5f-469">이 연결된 서비스에 대한 자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-469">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse-linked-service"></a><span data-ttu-id="7ae5f-470">Azure SQL Data Warehouse 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="7ae5f-470">Azure SQL Data Warehouse Linked Service</span></span>
<span data-ttu-id="7ae5f-471">Azure SQL Data Warehouse 연결된 서비스를 만들고 [저장 프로시저 활동](data-factory-stored-proc-activity.md) 에서 사용하여 Data Factory 파이프라인에서 저장 프로시저를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-471">You create an Azure SQL Data Warehouse linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> <span data-ttu-id="7ae5f-472">이 연결된 서비스에 대한 자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-472">See [Azure SQL Data Warehouse Connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="sql-server-linked-service"></a><span data-ttu-id="7ae5f-473">SQL Server 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="7ae5f-473">SQL Server Linked Service</span></span>
<span data-ttu-id="7ae5f-474">SQL Server 연결된 서비스를 만들고 [저장 프로시저 활동](data-factory-stored-proc-activity.md) 에서 사용하여 Data Factory 파이프라인에서 저장 프로시저를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-474">You create a SQL Server linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> <span data-ttu-id="7ae5f-475">이 연결된 서비스에 대한 자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ae5f-475">See [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article for details about this linked service.</span></span>

