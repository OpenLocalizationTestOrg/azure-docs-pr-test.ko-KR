---
title: "Stream Analytics에서 참조 데이터 및 조회 테이블 사용 | Microsoft Docs"
description: "Stream Analytics 쿼리에서 참조 데이터 사용"
keywords: "조회 테이블, 참조 데이터"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 06103be5-553a-4da1-8a8d-3be9ca2aff54
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3fd9c869be68d624a59ffb09ee53e31cd5a2f71b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="using-reference-data-or-lookup-tables-in-a-stream-analytics-input-stream"></a><span data-ttu-id="6c9e6-104">Stream Analytics 입력 스트림에서 참조 데이터 또는 조회 테이블 사용</span><span class="sxs-lookup"><span data-stu-id="6c9e6-104">Using reference data or lookup tables in a Stream Analytics input stream</span></span>
<span data-ttu-id="6c9e6-105">참조 데이터(조회 테이블이라고도 함)는 정적이거나 느리게 변경되는 특성을 지닌 한정된 데이터 집합으로, 데이터 스트림을 조회하거나 상관 관계를 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-105">Reference data (also known as a lookup table) is a finite data set that is static or slowing changing in nature, used to perform a lookup or to correlate with your data stream.</span></span> <span data-ttu-id="6c9e6-106">Azure Stream Analytics 작업에서 참조 데이터를 사용하려면 일반적으로 쿼리에서 [참조 데이터 조인](https://msdn.microsoft.com/library/azure/dn949258.aspx)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-106">To make use of reference data in your Azure Stream Analytics job, you will generally use a [Reference Data Join](https://msdn.microsoft.com/library/azure/dn949258.aspx) in your Query.</span></span> <span data-ttu-id="6c9e6-107">Stream Analytics에서는 참조 데이터에 대한 저장소 계층으로 Azure Blob Storage를 사용하고 Azure Data Factory를 통해 참조 데이터로 사용하기 위해 참조 데이터를 [개수에 관계 없이 클라우드 기반 및 온-프레미스 데이터 저장소](../data-factory/data-factory-data-movement-activities.md)형태로 Azure Blob Storage로 변환 및/또는 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-107">Stream Analytics uses Azure Blob storage as the storage layer for Reference Data, and with Azure Data Factory reference data can be transformed and/or copied to Azure Blob storage, for use as Reference Data, from [any number of cloud-based and on-premises data stores](../data-factory/data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="6c9e6-108">참조 데이터는 BLOB 이름에서 지정한 날짜/시간의 오름차순에 따라 BLOB의 시퀀스(입력 구성에서 정의)로 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-108">Reference data is modeled as a sequence of blobs (defined in the input configuration) in ascending order of the date/time specified in the blob name.</span></span> <span data-ttu-id="6c9e6-109">시퀀스의 마지막 BLOB에서 지정한 것보다 **이후인** 날짜/시간을 사용하여 시퀀스의 마지막에 추가하는 것**만** 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-109">It **only** supports adding to the end of the sequence by using a date/time **greater** than the one specified by the last blob in the sequence.</span></span>

<span data-ttu-id="6c9e6-110">Stream Analytics에는 **blob당 100MB의 제한**이 적용되지만 **경로 패턴** 속성을 사용하면 작업은 여러 참조 Blob을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-110">Stream Analytics has a **limit of 100 MB per blob** but jobs can process multiple reference blobs by using the **path pattern** property.</span></span>


## <a name="configuring-reference-data"></a><span data-ttu-id="6c9e6-111">참조 데이터 구성</span><span class="sxs-lookup"><span data-stu-id="6c9e6-111">Configuring reference data</span></span>
<span data-ttu-id="6c9e6-112">참조 데이터를 구성하려면 먼저 **참조 데이터**형식의 입력을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-112">To configure your reference data, you first need to create an input that is of type **Reference Data**.</span></span> <span data-ttu-id="6c9e6-113">다음 표에서 설명과 함께 참조 데이터 입력을 만드는 동안 제공해야 하는 각 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-113">The table below explains each property that you will need to provide while creating the reference data input with its description:</span></span>


<table>
<tbody>
<tr>
<td><span data-ttu-id="6c9e6-114">속성 이름</span><span class="sxs-lookup"><span data-stu-id="6c9e6-114">Property Name</span></span></td>
<td><span data-ttu-id="6c9e6-115">설명</span><span class="sxs-lookup"><span data-stu-id="6c9e6-115">Description</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6c9e6-116">입력 별칭</span><span class="sxs-lookup"><span data-stu-id="6c9e6-116">Input Alias</span></span></td>
<td><span data-ttu-id="6c9e6-117">이 입력을 참조하도록 작업 쿼리에서 사용할 친숙한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-117">A friendly name that will be used in the job query to reference this input.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6c9e6-118">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="6c9e6-118">Storage Account</span></span></td>
<td><span data-ttu-id="6c9e6-119">Blob이 위치한 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-119">The name of the storage account where your blobs are located.</span></span> <span data-ttu-id="6c9e6-120">Stream Analytics 작업과 동일한 구독에 있으면 드롭다운에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-120">If it’s in the same subscription as your Stream Analytics Job, you can select it from the drop-down.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6c9e6-121">저장소 계정 키</span><span class="sxs-lookup"><span data-stu-id="6c9e6-121">Storage Account Key</span></span></td>
<td><span data-ttu-id="6c9e6-122">저장소 계정과 연결된 비밀 키입니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-122">The secret key associated with the storage account.</span></span> <span data-ttu-id="6c9e6-123">저장소 계정이 Stream Analytics 작업과 동일한 구독에 있으면 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-123">This gets automatically populated if the storage account is in the same subscription as your Stream Analytics job.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6c9e6-124">저장소 컨테이너</span><span class="sxs-lookup"><span data-stu-id="6c9e6-124">Storage Container</span></span></td>
<td><span data-ttu-id="6c9e6-125">컨테이너는 Microsoft Azure Blob 서비스에 저장된 Blob에 대한 논리적 그룹화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-125">Containers provide a logical grouping for blobs stored in the Microsoft Azure Blob service.</span></span> <span data-ttu-id="6c9e6-126">Blob 서비스에 Blob을 업로드하는 경우 해당 Blob에 대한 컨테이너를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-126">When you upload a blob to the Blob service, you must specify a container for that blob.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6c9e6-127">경로 패턴</span><span class="sxs-lookup"><span data-stu-id="6c9e6-127">Path Pattern</span></span></td>
<td><span data-ttu-id="6c9e6-128">지정된 컨테이너 내에서 Blob을 찾는 데 사용되는 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-128">The path used to locate your blobs within the specified container.</span></span> <span data-ttu-id="6c9e6-129">경로 내에서 다음 두 변수의 인스턴스 중 하나 이상을 지정하도록 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-129">Within the path, you may choose to specify one or more instances of the following 2 variables:</span></span><BR><span data-ttu-id="6c9e6-130">{date}, {time}</span><span class="sxs-lookup"><span data-stu-id="6c9e6-130">{date}, {time}</span></span><BR><span data-ttu-id="6c9e6-131">예 1: products/{date}/{time}/product-list.csv</span><span class="sxs-lookup"><span data-stu-id="6c9e6-131">Example 1: products/{date}/{time}/product-list.csv</span></span><BR><span data-ttu-id="6c9e6-132">예 2: products/{date}/product-list.csv</span><span class="sxs-lookup"><span data-stu-id="6c9e6-132">Example 2: products/{date}/product-list.csv</span></span>
</tr>
<tr>
<td><span data-ttu-id="6c9e6-133">날짜 형식[선택 사항]</span><span class="sxs-lookup"><span data-stu-id="6c9e6-133">Date Format [optional]</span></span></td>
<td><span data-ttu-id="6c9e6-134">지정한 경로 패턴 내에서 {date}를 사용한 경우 Blob이 구성되는 날짜 형식을 지원되는 형식 드롭다운에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-134">If you have used {date} within the Path Pattern that you specified, then you can select the date format in which your blobs are organized from the drop-down of supported formats.</span></span><BR><span data-ttu-id="6c9e6-135">예: YYYY/MM/DD, MM/DD/YYYY 등</span><span class="sxs-lookup"><span data-stu-id="6c9e6-135">Example: YYYY/MM/DD, MM/DD/YYYY, etc.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6c9e6-136">시간 형식[선택 사항]</span><span class="sxs-lookup"><span data-stu-id="6c9e6-136">Time Format [optional]</span></span></td>
<td><span data-ttu-id="6c9e6-137">지정한 경로 패턴 내에서 {time}을 사용한 경우 Blob이 구성되는 시간 형식을 지원되는 형식 드롭다운에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-137">If you have used {time} within the Path Pattern that you specified, then you can select the time format in which your blobs are organized from the drop-down of supported formats.</span></span><BR><span data-ttu-id="6c9e6-138">예: HH, HH/mm 또는 HH-mm</span><span class="sxs-lookup"><span data-stu-id="6c9e6-138">Example: HH, HH/mm, or HH-mm</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6c9e6-139">이벤트 직렬화 형식</span><span class="sxs-lookup"><span data-stu-id="6c9e6-139">Event Serialization Format</span></span></td>
<td><span data-ttu-id="6c9e6-140">쿼리가 예상대로 작동하는지 확인하려면 Stream Analytics은 들어오는 데이터 스트림으로 사용 중인 직렬화 형식을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-140">To make sure your queries work the way you expect, Stream Analytics needs to know which serialization format you're using for incoming data streams.</span></span> <span data-ttu-id="6c9e6-141">참조 데이터에 대해 지원되는 형식은 CSV 및 JSON입니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-141">For Reference Data, the supported formats are CSV and JSON.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6c9e6-142">인코딩</span><span class="sxs-lookup"><span data-stu-id="6c9e6-142">Encoding</span></span></td>
<td><span data-ttu-id="6c9e6-143">지금은 지원되는 인코딩 형식이 UTF-8뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-143">UTF-8 is the only supported encoding format at this time</span></span></td>
</tr>
</tbody>
</table>

## <a name="generating-reference-data-on-a-schedule"></a><span data-ttu-id="6c9e6-144">일정에 따라 참조 데이터 생성</span><span class="sxs-lookup"><span data-stu-id="6c9e6-144">Generating reference data on a schedule</span></span>
<span data-ttu-id="6c9e6-145">참조 데이터가 느리게 변경되는 데이터 집합인 경우 {date} 및 {time} 대체 토큰을 사용하여 입력 구성의 경로 패턴을 지정하여 참조 데이터 새로 고침 지원을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-145">If your reference data is a slowly changing data set, then support for refreshing reference data is enabled by specifying a path pattern in the input configuration using the {date} and {time} substitution tokens.</span></span> <span data-ttu-id="6c9e6-146">Stream Analytics이 이 경로 패턴에 따라 업데이트된 참조 데이터 정의를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-146">Stream Analytics picks up the updated reference data definitions based on this path pattern.</span></span> <span data-ttu-id="6c9e6-147">예를 들어 날짜 형식 **“YYYY-MM-DD”** 및 시간 형식 **“HH-mm”**의 `sample/{date}/{time}/products.csv` 패턴은 UTC 표준 시간대 2015년 4월 16일 오후 5시 30분에 Stream Analytics에서 업데이트된 Blob `sample/2015-04-16/17-30/products.csv`을 선택하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-147">For example, a pattern of `sample/{date}/{time}/products.csv` with a date format of **“YYYY-MM-DD”** and a time format of **“HH-mm”** instructs Stream Analytics to pick up the updated blob `sample/2015-04-16/17-30/products.csv` at 5:30 PM on April 16th, 2015 UTC time zone.</span></span>

> [!NOTE]
> <span data-ttu-id="6c9e6-148">현재 Stream Analytics 작업은 컴퓨터 시간이 Blob 이름에 인코딩된 시간으로 진행하는 경우에만 Blob 새로 고침을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-148">Currently Stream Analytics jobs look for the blob refresh only when the machine time advances to the time encoded in the blob name.</span></span> <span data-ttu-id="6c9e6-149">예를 들어 작업은 가능한 빨리 `sample/2015-04-16/17-30/products.csv`를 찾지만 표준 시간대 2015년 4월 16일 오후 5시 30분보다 이르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-149">For example, the job will look for `sample/2015-04-16/17-30/products.csv` as soon as possible but no earlier than 5:30 PM on April 16th, 2015 UTC time zone.</span></span> <span data-ttu-id="6c9e6-150">마지막으로 검색된 것보다 이전에 인코딩된 시간으로 Blob을 찾지 *않습니다* .</span><span class="sxs-lookup"><span data-stu-id="6c9e6-150">It will *never* look for a blob with an encoded time earlier than the last one that is discovered.</span></span>
> 
> <span data-ttu-id="6c9e6-151">예:</span><span class="sxs-lookup"><span data-stu-id="6c9e6-151">E.g.</span></span> <span data-ttu-id="6c9e6-152">작업이 Blob `sample/2015-04-16/17-30/products.csv`를 발견하면 2015년 4월 16일 오후 5시 30분 이전에 인코딩된 날짜의 모든 파일을 무시합니다. 따라서 늦게 도착하는 `sample/2015-04-16/17-25/products.csv` Blob이 동일한 컨테이너에 만들어지는 경우 작업은 이를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-152">once the job finds the blob `sample/2015-04-16/17-30/products.csv` it will ignore any files with an encoded date earlier than 5:30 PM April 16th, 2015 so if a late arriving `sample/2015-04-16/17-25/products.csv` blob gets created in the same container the job will not use it.</span></span>
> 
> <span data-ttu-id="6c9e6-153">마찬가지로 `sample/2015-04-16/17-30/products.csv`가 2015년 4월 16일 오후 10시 3분에 생성되었지만 컨테이너에 이전 날짜의 Blob이 없는 경우 작업은 2015년 4월 16일 오후 10시 3분에 시작하는 이 파일을 사용하고 그때까지 이전 참조 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-153">Likewise if `sample/2015-04-16/17-30/products.csv` is only produced at 10:03 PM April 16th, 2015 but no blob with an earlier date is present in the container, the job will use this file starting at 10:03 PM April 16th, 2015 and use the previous reference data until then.</span></span>
> 
> <span data-ttu-id="6c9e6-154">이에 대한 예외는 시간을 거슬러 데이터를 재처리해야 하는 작업이거나 작업을 최초로 시작할 때입니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-154">An exception to this is when the job needs to re-process data back in time or when the job is first started.</span></span> <span data-ttu-id="6c9e6-155">시작 시점에 작업은 지정된 작업 시작 시간 이전에 생성된 가장 최근 Blob을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-155">At start time the job is looking for the most recent blob produced before the job start time specified.</span></span> <span data-ttu-id="6c9e6-156">이렇게 하면 작업을 시작할 때 **비어 있지 않은** 참조 데이터가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-156">This is done to ensure that there is a **non-empty** reference data set when the job starts.</span></span> <span data-ttu-id="6c9e6-157">찾을 수 없는 경우 작업은 다음 진단 `Initializing input without a valid reference data blob for UTC time <start time>`을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-157">If one cannot be found, the job displays the following diagnostic: `Initializing input without a valid reference data blob for UTC time <start time>`.</span></span>
> 
> 

<span data-ttu-id="6c9e6-158">Stream Analytics에서 참조 데이터 정의를 업데이트하는 데 필요한 업데이트된 Blob을 만드는 작업을 오케스트레이션하는 데 [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-158">[Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) can be used to orchestrate the task of creating the updated blobs required by Stream Analytics to update reference data definitions.</span></span> <span data-ttu-id="6c9e6-159">데이터 팩터리는 데이터의 이동과 변환을 조율하고 자동화하는 클라우드 기반의 데이터 통합 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-159">Data Factory is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="6c9e6-160">데이터 팩터리는 [많은 수의 클라우드 기반 및 온-프레미스 데이터 저장소 연결](../data-factory/data-factory-data-movement-activities.md) 을 지원하고 사용자가 지정한 정기적인 일정으로 데이터를 쉽게 이동할 수 있도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-160">Data Factory supports [connecting to a large number of cloud based and on-premises data stores](../data-factory/data-factory-data-movement-activities.md) and moving data easily on a regular schedule that you specify.</span></span> <span data-ttu-id="6c9e6-161">미리 정의된 일정에 따라 새로 고쳐지는 Stream Analytics을 위한 참조 데이터를 생성하는 데이터 팩터리 파이프라인 설정 방법에 대한 단계별 지침과 자세한 내용은 이 [GitHub 샘플](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-161">For more information and step by step guidance on how to set up a Data Factory pipeline to generate reference data for Stream Analytics which refreshes on a pre-defined schedule, check out this [GitHub sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs).</span></span>

## <a name="tips-on-refreshing-your-reference-data"></a><span data-ttu-id="6c9e6-162">참조 데이터 새로고침 팁</span><span class="sxs-lookup"><span data-stu-id="6c9e6-162">Tips on refreshing your reference data</span></span>
1. <span data-ttu-id="6c9e6-163">참조 데이터 BLOB를 덮어쓰면 Stream Analytics이 해당 BLOB를 다시 로드하지 않으며 경우에 따라 작업이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-163">Overwriting reference data blobs will not cause Stream Analytics to reload the blob and in some cases it can cause the job to fail.</span></span> <span data-ttu-id="6c9e6-164">참조 데이터를 변경할 때는 작업 입력에서 정의된 것과 동일한 컨테이너 및 경로 패턴을 사용하여 새 BLOB를 추가하고 시퀀스의 마지막 BLOB에서 지정한 것보다 **나중인** 날짜/시간을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-164">The recommended way to change reference data is to add a new blob using the same container and path pattern defined in the job input and use a date/time **greater** than the one specified by the last blob in the sequence.</span></span>
2. <span data-ttu-id="6c9e6-165">참조 데이터 Blob은 Blob의 “마지막 수정" 시간 순서가 **아니라** {date} 및 {time}을 대체하여 Blob 이름에 지정한 날짜와 시간으로만 순서가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-165">Reference data blobs are **not** ordered by the blob’s “Last Modified” time but only by the time and date specified in the blob name using the {date} and {time} substitutions.</span></span>
3. <span data-ttu-id="6c9e6-166">드물지만 작업의 시간을 되돌려야 할 경우가 있으므로 참조 데이터 BLOB을 변경 또는 삭제해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-166">On a few occasions, a job must go back in time, therefore reference data blobs must not be altered or deleted.</span></span>

## <a name="get-help"></a><span data-ttu-id="6c9e6-167">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="6c9e6-167">Get help</span></span>
<span data-ttu-id="6c9e6-168">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="6c9e6-168">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c9e6-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6c9e6-169">Next steps</span></span>
<span data-ttu-id="6c9e6-170">사물 인터넷에서 발생한 데이터에 대한 스트리밍 분석용 관리 서비스, 스트림 분석에 대해 소개하였습니다.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-170">You've been introduced to Stream Analytics, a managed service for streaming analytics on data from the Internet of Things.</span></span> <span data-ttu-id="6c9e6-171">이 서비스에 대해 자세히 알아보려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c9e6-171">To learn more about this service, see:</span></span>

* [<span data-ttu-id="6c9e6-172">Azure 스트림 분석 사용 시작</span><span class="sxs-lookup"><span data-stu-id="6c9e6-172">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6c9e6-173">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="6c9e6-173">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6c9e6-174">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="6c9e6-174">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6c9e6-175">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="6c9e6-175">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
