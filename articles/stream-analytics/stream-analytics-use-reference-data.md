---
title: "스트림 분석에서 aaaUse 참조 데이터 및 조회 테이블 | Microsoft Docs"
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
ms.openlocfilehash: fb1d18fba920db5e097d0c95d333e8e8390d1589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-reference-data-or-lookup-tables-in-a-stream-analytics-input-stream"></a><span data-ttu-id="5cf1b-104">Stream Analytics 입력 스트림에서 참조 데이터 또는 조회 테이블 사용</span><span class="sxs-lookup"><span data-stu-id="5cf1b-104">Using reference data or lookup tables in a Stream Analytics input stream</span></span>
<span data-ttu-id="5cf1b-105">참조 데이터 (조회 테이블이 라고도 함)은 static이 한정 된 데이터 집합 또는 느려질 수 있으므로 본질적으로 변경 사용 tooperform 조회 또는 toocorrelate 데이터 스트림을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-105">Reference data (also known as a lookup table) is a finite data set that is static or slowing changing in nature, used tooperform a lookup or toocorrelate with your data stream.</span></span> <span data-ttu-id="5cf1b-106">참조 데이터의 toomake 사용 Azure 스트림 분석 작업을 일반적으로 사용 하는 [참조 데이터 Join](https://msdn.microsoft.com/library/azure/dn949258.aspx) 쿼리에 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-106">toomake use of reference data in your Azure Stream Analytics job, you will generally use a [Reference Data Join](https://msdn.microsoft.com/library/azure/dn949258.aspx) in your Query.</span></span> <span data-ttu-id="5cf1b-107">스트림 분석에서는 참조 데이터에 대 한 hello 저장소 계층으로 Azure Blob 저장소를 사용 하 고 Azure Data Factory 참조와 데이터 가능 참조 데이터로 사용 하기 위해 변환 된 및/또는 복사 된 tooAzure Blob 저장소에서 [클라우드 기반 개수에 관계 없이 및 온-프레미스 데이터 저장소](../data-factory/data-factory-data-movement-activities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-107">Stream Analytics uses Azure Blob storage as hello storage layer for Reference Data, and with Azure Data Factory reference data can be transformed and/or copied tooAzure Blob storage, for use as Reference Data, from [any number of cloud-based and on-premises data stores](../data-factory/data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="5cf1b-108">참조 데이터의 hello 날짜/시간 hello blob 이름에 지정 된 오름차순 (hello 입력된 구성에서 정의 됨)는 blob의 시퀀스도 모델링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-108">Reference data is modeled as a sequence of blobs (defined in hello input configuration) in ascending order of hello date/time specified in hello blob name.</span></span> <span data-ttu-id="5cf1b-109">그 **만** hello 시퀀스의 toohello 끝 날짜/시간을 사용 하 여 추가 지원 **큰** 보다 hello hello 시퀀스에서 마지막으로 hello blob에서 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-109">It **only** supports adding toohello end of hello sequence by using a date/time **greater** than hello one specified by hello last blob in hello sequence.</span></span>

<span data-ttu-id="5cf1b-110">스트림 분석에는 **blob 당 100MB 제한인** 작업 hello를 사용 하 여 여러 참조 blob을 처리할 수 있지만 **경로 패턴** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-110">Stream Analytics has a **limit of 100 MB per blob** but jobs can process multiple reference blobs by using hello **path pattern** property.</span></span>


## <a name="configuring-reference-data"></a><span data-ttu-id="5cf1b-111">참조 데이터 구성</span><span class="sxs-lookup"><span data-stu-id="5cf1b-111">Configuring reference data</span></span>
<span data-ttu-id="5cf1b-112">tooconfigure 참조 데이터를 먼저 입력 형식을 가진 toocreate **참조 데이터**합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-112">tooconfigure your reference data, you first need toocreate an input that is of type **Reference Data**.</span></span> <span data-ttu-id="5cf1b-113">hello 표에서 해당 설명과 함께 hello 참조 데이터 입력을 만드는 동안 tooprovide가 필요 합니다 각 속성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-113">hello table below explains each property that you will need tooprovide while creating hello reference data input with its description:</span></span>


<table>
<tbody>
<tr>
<td><span data-ttu-id="5cf1b-114">속성 이름</span><span class="sxs-lookup"><span data-stu-id="5cf1b-114">Property Name</span></span></td>
<td><span data-ttu-id="5cf1b-115">설명</span><span class="sxs-lookup"><span data-stu-id="5cf1b-115">Description</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5cf1b-116">입력 별칭</span><span class="sxs-lookup"><span data-stu-id="5cf1b-116">Input Alias</span></span></td>
<td><span data-ttu-id="5cf1b-117">Hello 작업 쿼리 tooreference이 입력에 사용 되는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-117">A friendly name that will be used in hello job query tooreference this input.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5cf1b-118">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="5cf1b-118">Storage Account</span></span></td>
<td><span data-ttu-id="5cf1b-119">hello hello 저장소 계정의 이름으로는 blob의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-119">hello name of hello storage account where your blobs are located.</span></span> <span data-ttu-id="5cf1b-120">Hello에 있으면 스트림 분석 작업으로 동일한 구독을 선택할 수 있습니다 hello 드롭다운 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-120">If it’s in hello same subscription as your Stream Analytics Job, you can select it from hello drop-down.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5cf1b-121">저장소 계정 키</span><span class="sxs-lookup"><span data-stu-id="5cf1b-121">Storage Account Key</span></span></td>
<td><span data-ttu-id="5cf1b-122">hello 저장소 계정과 연결 된 hello 비밀 키입니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-122">hello secret key associated with hello storage account.</span></span> <span data-ttu-id="5cf1b-123">이 자동으로 채워집니다 hello 저장소 계정이 hello에 경우 스트림 분석 작업으로 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-123">This gets automatically populated if hello storage account is in hello same subscription as your Stream Analytics job.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5cf1b-124">저장소 컨테이너</span><span class="sxs-lookup"><span data-stu-id="5cf1b-124">Storage Container</span></span></td>
<td><span data-ttu-id="5cf1b-125">컨테이너는 hello Microsoft Azure Blob 서비스에에서 저장 된 blob에 대 한 논리적 그룹화를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-125">Containers provide a logical grouping for blobs stored in hello Microsoft Azure Blob service.</span></span> <span data-ttu-id="5cf1b-126">Blob toohello Blob 서비스에 업로드할 때 해당 blob에 대 한 컨테이너를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-126">When you upload a blob toohello Blob service, you must specify a container for that blob.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5cf1b-127">경로 패턴</span><span class="sxs-lookup"><span data-stu-id="5cf1b-127">Path Pattern</span></span></td>
<td><span data-ttu-id="5cf1b-128">hello 경로 toolocate hello 지정 된 컨테이너 내에서 blob을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-128">hello path used toolocate your blobs within hello specified container.</span></span> <span data-ttu-id="5cf1b-129">Hello 경로 내 toospecify hello 두 변수를 다음의 하나 이상의 인스턴스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-129">Within hello path, you may choose toospecify one or more instances of hello following 2 variables:</span></span><BR><span data-ttu-id="5cf1b-130">{date}, {time}</span><span class="sxs-lookup"><span data-stu-id="5cf1b-130">{date}, {time}</span></span><BR><span data-ttu-id="5cf1b-131">예 1: products/{date}/{time}/product-list.csv</span><span class="sxs-lookup"><span data-stu-id="5cf1b-131">Example 1: products/{date}/{time}/product-list.csv</span></span><BR><span data-ttu-id="5cf1b-132">예 2: products/{date}/product-list.csv</span><span class="sxs-lookup"><span data-stu-id="5cf1b-132">Example 2: products/{date}/product-list.csv</span></span>
</tr>
<tr>
<td><span data-ttu-id="5cf1b-133">날짜 형식[선택 사항]</span><span class="sxs-lookup"><span data-stu-id="5cf1b-133">Date Format [optional]</span></span></td>
<td><span data-ttu-id="5cf1b-134">Hello 지정한 경로 패턴에 {date}를 사용한 경우 blob 구성 되는 hello 날짜 형식을 지원 되는 형식의 hello 드롭다운 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-134">If you have used {date} within hello Path Pattern that you specified, then you can select hello date format in which your blobs are organized from hello drop-down of supported formats.</span></span><BR><span data-ttu-id="5cf1b-135">예: YYYY/MM/DD, MM/DD/YYYY 등</span><span class="sxs-lookup"><span data-stu-id="5cf1b-135">Example: YYYY/MM/DD, MM/DD/YYYY, etc.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5cf1b-136">시간 형식[선택 사항]</span><span class="sxs-lookup"><span data-stu-id="5cf1b-136">Time Format [optional]</span></span></td>
<td><span data-ttu-id="5cf1b-137">Hello 지정한 경로 패턴에 {time}를 사용한 경우 blob 구성 되는 hello 시간 형식을 지원 되는 형식의 hello 드롭다운 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-137">If you have used {time} within hello Path Pattern that you specified, then you can select hello time format in which your blobs are organized from hello drop-down of supported formats.</span></span><BR><span data-ttu-id="5cf1b-138">예: HH, HH/mm 또는 HH-mm</span><span class="sxs-lookup"><span data-stu-id="5cf1b-138">Example: HH, HH/mm, or HH-mm</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5cf1b-139">이벤트 직렬화 형식</span><span class="sxs-lookup"><span data-stu-id="5cf1b-139">Event Serialization Format</span></span></td>
<td><span data-ttu-id="5cf1b-140">쿼리 hello 방식으로 예상 되는 스트림 분석 작동 toomake에 들어오는 데이터 스트림에 사용 될 serialization 형식 tooknow가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-140">toomake sure your queries work hello way you expect, Stream Analytics needs tooknow which serialization format you're using for incoming data streams.</span></span> <span data-ttu-id="5cf1b-141">참조 데이터에 대 한 지원 hello 형식은 CSV 및 JSON 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-141">For Reference Data, hello supported formats are CSV and JSON.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5cf1b-142">인코딩</span><span class="sxs-lookup"><span data-stu-id="5cf1b-142">Encoding</span></span></td>
<td><span data-ttu-id="5cf1b-143">U t F-8은 hello만 현재 지원 인코딩 형식</span><span class="sxs-lookup"><span data-stu-id="5cf1b-143">UTF-8 is hello only supported encoding format at this time</span></span></td>
</tr>
</tbody>
</table>

## <a name="generating-reference-data-on-a-schedule"></a><span data-ttu-id="5cf1b-144">일정에 따라 참조 데이터 생성</span><span class="sxs-lookup"><span data-stu-id="5cf1b-144">Generating reference data on a schedule</span></span>
<span data-ttu-id="5cf1b-145">그런 다음 참조 데이터는 느린 변경 데이터 집합, 참조 데이터 새로 고침에 대 한 지원 hello {date} 및 {time} 대체 토큰을 사용 하 여 hello 입력된 구성에서 경로 패턴을 지정 하 여 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-145">If your reference data is a slowly changing data set, then support for refreshing reference data is enabled by specifying a path pattern in hello input configuration using hello {date} and {time} substitution tokens.</span></span> <span data-ttu-id="5cf1b-146">스트림 분석은이 경로 패턴에 따라 업데이트 하는 hello 참조 데이터 정의를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-146">Stream Analytics picks up hello updated reference data definitions based on this path pattern.</span></span> <span data-ttu-id="5cf1b-147">예를 들어 패턴 `sample/{date}/{time}/products.csv` 의 날짜 형식으로 **"YYYY-월-일"** 및의 시간 형식 **"HH mm"** 업데이트 hello blob 스트림 분석 toopick 지시 `sample/2015-04-16/17-30/products.csv` 년 4 월 오후 5시 30분 16, 2015 UTC 표준 시간대입니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-147">For example, a pattern of `sample/{date}/{time}/products.csv` with a date format of **“YYYY-MM-DD”** and a time format of **“HH-mm”** instructs Stream Analytics toopick up hello updated blob `sample/2015-04-16/17-30/products.csv` at 5:30 PM on April 16th, 2015 UTC time zone.</span></span>

> [!NOTE]
> <span data-ttu-id="5cf1b-148">현재 스트림 분석 작업이 hello blob 이름으로 인코딩된 toohello 시간을 이동 하는 hello 컴퓨터 시간 하는 경우에 hello blob 새로 고침을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-148">Currently Stream Analytics jobs look for hello blob refresh only when hello machine time advances toohello time encoded in hello blob name.</span></span> <span data-ttu-id="5cf1b-149">Hello 작업에 대 한 예를 들어 보이는지 `sample/2015-04-16/17-30/products.csv` 가능한 있지만 이전 UTC 2015 년 4 월 16 일 오후 5시 30분 보다 표준 시간대는 즉시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-149">For example, hello job will look for `sample/2015-04-16/17-30/products.csv` as soon as possible but no earlier than 5:30 PM on April 16th, 2015 UTC time zone.</span></span> <span data-ttu-id="5cf1b-150">됩니다 *되지* 인코딩된 시간이 hello 마지막 트랜잭션이 검색 되는 것 보다 먼저 blob를 찾아보십시오.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-150">It will *never* look for a blob with an encoded time earlier than hello last one that is discovered.</span></span>
> 
> <span data-ttu-id="5cf1b-151">예:</span><span class="sxs-lookup"><span data-stu-id="5cf1b-151">E.g.</span></span> <span data-ttu-id="5cf1b-152">hello 작업 hello blob 발견 되 면 `sample/2015-04-16/17-30/products.csv` 인코딩된 날짜가 2015 년 4 월 16 일 오후 5 시 30 분 이전에 모든 파일을 무시 합니다 늦게 도착 하는 경우 `sample/2015-04-16/17-25/products.csv` blob 생성 hello에 동일한 컨테이너 hello 작업에서 사용 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-152">once hello job finds hello blob `sample/2015-04-16/17-30/products.csv` it will ignore any files with an encoded date earlier than 5:30 PM April 16th, 2015 so if a late arriving `sample/2015-04-16/17-25/products.csv` blob gets created in hello same container hello job will not use it.</span></span>
> 
> <span data-ttu-id="5cf1b-153">마찬가지로 경우 `sample/2015-04-16/17-30/products.csv` 오후 10시 03분 2015 년 4 월 16 일에 생성 된 하지만 이전 날짜로 사용 하 여 없는 blob hello 컨테이너에 있는지, hello 작업을 오후 10시 03분 2015 년 4 월 16 일에서 시작이 파일을 사용 하 고 그때 까지는 hello 이전 참조 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-153">Likewise if `sample/2015-04-16/17-30/products.csv` is only produced at 10:03 PM April 16th, 2015 but no blob with an earlier date is present in hello container, hello job will use this file starting at 10:03 PM April 16th, 2015 and use hello previous reference data until then.</span></span>
> 
> <span data-ttu-id="5cf1b-154">예외 toothis hello 작업 시간에 다시 toore 프로세스 데이터가 필요한 경우 또는 hello 작업이 처음 시작 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-154">An exception toothis is when hello job needs toore-process data back in time or when hello job is first started.</span></span> <span data-ttu-id="5cf1b-155">시작 시 hello hello 작업이 시작 될 지정 된 시간 전에 생성 되는 가장 최근의 blob에 대 한 시간 hello 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-155">At start time hello job is looking for hello most recent blob produced before hello job start time specified.</span></span> <span data-ttu-id="5cf1b-156">tooensure 이렇게는 **비어 있지 않은** hello 작업이 시작 될 때 데이터 집합을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-156">This is done tooensure that there is a **non-empty** reference data set when hello job starts.</span></span> <span data-ttu-id="5cf1b-157">Hello 작업 hello 다음 진단 표시를 찾을 수 없는 경우: `Initializing input without a valid reference data blob for UTC time <start time>`합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-157">If one cannot be found, hello job displays hello following diagnostic: `Initializing input without a valid reference data blob for UTC time <start time>`.</span></span>
> 
> 

<span data-ttu-id="5cf1b-158">[Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) 스트림 분석 tooupdate 참조 데이터 정의에 필요한 업데이트 hello blob을 만드는 사용 되는 tooorchestrate hello 작업일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-158">[Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) can be used tooorchestrate hello task of creating hello updated blobs required by Stream Analytics tooupdate reference data definitions.</span></span> <span data-ttu-id="5cf1b-159">데이터 팩터리는 오케스트레이션 하 고 데이터의 hello 이동 및 변환을 자동화 하는 클라우드 기반 데이터 통합 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-159">Data Factory is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="5cf1b-160">데이터 팩터리의 지원 [tooa 많은 수의 클라우드 기반 및 온-프레미스 데이터 저장소 연결](../data-factory/data-factory-data-movement-activities.md) 지정 하는 정기적으로 데이터를 쉽게 이동 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-160">Data Factory supports [connecting tooa large number of cloud based and on-premises data stores](../data-factory/data-factory-data-movement-activities.md) and moving data easily on a regular schedule that you specify.</span></span> <span data-ttu-id="5cf1b-161">자세한 정보 및 미리 정의 된 일정에 따라 새로 고쳐지는 스트림 분석에 대 한 데이터 팩터리를 tooset toogenerate 참조 데이터 파이프라인 하는 방법에 대 한 단계별 지침을 체크 아웃이 [GitHub 샘플](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs)합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-161">For more information and step by step guidance on how tooset up a Data Factory pipeline toogenerate reference data for Stream Analytics which refreshes on a pre-defined schedule, check out this [GitHub sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs).</span></span>

## <a name="tips-on-refreshing-your-reference-data"></a><span data-ttu-id="5cf1b-162">참조 데이터 새로고침 팁</span><span class="sxs-lookup"><span data-stu-id="5cf1b-162">Tips on refreshing your reference data</span></span>
1. <span data-ttu-id="5cf1b-163">참조 데이터 blob 덮어쓰기 스트림 분석 tooreload hello blob 재생을 hello 작업 toofail 일부 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-163">Overwriting reference data blobs will not cause Stream Analytics tooreload hello blob and in some cases it can cause hello job toofail.</span></span> <span data-ttu-id="5cf1b-164">hello 권장 방법은 toochange 참조 데이터는 tooadd hello hello 작업 입력에 동일한 컨테이너 및 경로 패턴은 정의 사용 하 여 새 blob 및 날짜/시간을 사용 하 여 **큰** 보다 hello hello 시퀀스에서 마지막으로 hello blob에서 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-164">hello recommended way toochange reference data is tooadd a new blob using hello same container and path pattern defined in hello job input and use a date/time **greater** than hello one specified by hello last blob in hello sequence.</span></span>
2. <span data-ttu-id="5cf1b-165">참조 데이터 blob는 **하지** hello blob "마지막으로 수정한 날짜" 시간 있지만 hello {date} 및 {time} 대체를 사용 하 여 hello blob 이름에 지정 된 날짜 및 시간 hello로만 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-165">Reference data blobs are **not** ordered by hello blob’s “Last Modified” time but only by hello time and date specified in hello blob name using hello {date} and {time} substitutions.</span></span>
3. <span data-ttu-id="5cf1b-166">드물지만 작업의 시간을 되돌려야 할 경우가 있으므로 참조 데이터 BLOB을 변경 또는 삭제해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-166">On a few occasions, a job must go back in time, therefore reference data blobs must not be altered or deleted.</span></span>

## <a name="get-help"></a><span data-ttu-id="5cf1b-167">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="5cf1b-167">Get help</span></span>
<span data-ttu-id="5cf1b-168">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="5cf1b-168">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5cf1b-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5cf1b-169">Next steps</span></span>
<span data-ttu-id="5cf1b-170">도입 된 tooStream hello 사물 인터넷에서에서 데이터에 대해 분석을 스트리밍에 대 한 관리 되는 서비스를 분석 한 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="5cf1b-170">You've been introduced tooStream Analytics, a managed service for streaming analytics on data from hello Internet of Things.</span></span> <span data-ttu-id="5cf1b-171">이 서비스에 대해 자세히 toolearn 참조:</span><span class="sxs-lookup"><span data-stu-id="5cf1b-171">toolearn more about this service, see:</span></span>

* [<span data-ttu-id="5cf1b-172">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="5cf1b-172">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="5cf1b-173">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="5cf1b-173">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="5cf1b-174">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="5cf1b-174">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="5cf1b-175">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="5cf1b-175">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
