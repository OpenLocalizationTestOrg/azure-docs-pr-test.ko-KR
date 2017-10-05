---
title: "Azure SQL의 Columnstore 인덱스 성능 개선 | Microsoft Docs"
description: "메모리 요구 사항을 줄이거나 사용 가능한 메모리를 늘려 columnstore 인덱스가 각 행 그룹으로 압축되는 행 수를 최대화합니다."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: f0e0b839b4a0c216eee2eb5134d43b91d8f83289
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="39ef3-103">columnstore의 행 그룹 품질 최대화</span><span class="sxs-lookup"><span data-stu-id="39ef3-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="39ef3-104">행 그룹 품질은 행 그룹의 행 수에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-104">Rowgroup quality is determined by the number of rows in a rowgroup.</span></span> <span data-ttu-id="39ef3-105">메모리 요구 사항을 줄이거나 사용 가능한 메모리를 늘려 columnstore 인덱스가 각 행 그룹으로 압축되는 행 수를 최대화합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-105">Reduce memory requirements or increase the available memory to maximize the number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="39ef3-106">이 방법을 사용하여 columnstore 인덱스에 대한 압축 비율 및 쿼리 성능을 개선시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-106">Use these methods to improve compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-the-rowgroup-size-matters"></a><span data-ttu-id="39ef3-107">행 그룹 크기가 중요한 이유</span><span class="sxs-lookup"><span data-stu-id="39ef3-107">Why the rowgroup size matters</span></span>
<span data-ttu-id="39ef3-108">columnstore 인덱스는 개별 행 그룹의 열 세그먼트를 검색하여 테이블을 검색하므로 각 행 그룹에서 행 수를 최대화하면 쿼리 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing the number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="39ef3-109">행 그룹에 행 수가 많은 경우 데이터 압축이 향상되며 따라서 디스크에서 읽어올 데이터가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-109">When rowgroups have a high number of rows, data compression improves which means there is less data to read from disk.</span></span>

<span data-ttu-id="39ef3-110">행 그룹 에 대한 자세한 내용은 [Columnstore 인덱스 가이드](https://msdn.microsoft.com/library/gg492088.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39ef3-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="39ef3-111">행 그룹의 대상 크기</span><span class="sxs-lookup"><span data-stu-id="39ef3-111">Target size for rowgroups</span></span>
<span data-ttu-id="39ef3-112">최적의 쿼리 성능을 위해 columnstore 인덱스에서 행 그룹당 행 수를 최대화하는 것을 목표로 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-112">For best query performance, the goal is to maximize the number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="39ef3-113">행 그룹은 최대 1,048,576개의 행을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="39ef3-114">행 그룹당 최대 행 수를 포함하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-114">It's okay to not have the maximum number of rows per rowgroup.</span></span> <span data-ttu-id="39ef3-115">Columnstore 인덱스는 행 그룹에 100,000개 이상의 행이 있을 때 적절한 성능을 달성합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="39ef3-116">압축 중에 행 그룹을 잘라낼 수 있음</span><span class="sxs-lookup"><span data-stu-id="39ef3-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="39ef3-117">대량 로드 또는 columnstore 인덱스 다시 작성 중에는 각 행 그룹에 대해 지정된 모든 행을 압축하기에 메모리가 부족할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available to compress all the rows designated for each rowgroup.</span></span> <span data-ttu-id="39ef3-118">메모리가 부족할 때 columnstore 인덱스는 columnstore로 압축이 성공할 수 있도록 행 그룹 크기를 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-118">When there is memory pressure, columnstore indexes trim the rowgroup sizes so compression into the columnstore can succeed.</span></span> 

<span data-ttu-id="39ef3-119">10,000개 이상의 행을 각 행 그룹으로 압축하기에 메모리가 부족한 경우 SQL Data Warehouse에서 오류를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-119">When there is insufficient memory to compress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="39ef3-120">대량 로드에 대한 자세한 내용은 [클러스터형 columnstore 인덱스로 대량 로드](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39ef3-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-to-monitor-rowgroup-quality"></a><span data-ttu-id="39ef3-121">행 그룹 품질을 모니터링 하는 방법</span><span class="sxs-lookup"><span data-stu-id="39ef3-121">How to monitor rowgroup quality</span></span>

<span data-ttu-id="39ef3-122">행 그룹의 행 수, 행 그룹이 잘린 경우 해당 이유 등의 유용한 정보를 표시하는 DMV(sys.dm_pdw_nodes_db_column_store_row_group_physical_stats)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and the reason for trimming if there was trimming.</span></span> <span data-ttu-id="39ef3-123">다음 보기를 만들면 이 DMV를 간편하게 쿼리하여 행 그룹 잘라내기에 대한 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-123">You can create the following view as a handy way to query this DMV to get information on rowgroup trimming.</span></span>

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

<span data-ttu-id="39ef3-124">trim_reason_desc는 행 그룹이 잘렸는지 여부를 나타냅니다. trim_reason_desc = NO_TRIM은 행 그룹이 잘리지 않았으며 최적의 품질임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-124">The trim_reason_desc tells whether the rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="39ef3-125">아래의 잘림 이유는 행 그룹이 중간에 잘렸음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-125">The following trim reasons indicate premature trimming of the rowgroup:</span></span>
- <span data-ttu-id="39ef3-126">BULKLOAD: 로드에 대해 들어오는 행 배치의 행 수가 1백만 개 미만이면 이 자르기 이유가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-126">BULKLOAD: This trim reason is used when the incoming batch of rows for the load had less than 1 million rows.</span></span> <span data-ttu-id="39ef3-127">삽입되는 행 수가 10만 개보다 많으면 엔진은 델타 저장소에 행을 삽입하지 않고 압축된 행 그룹을 만들지만 자르기 이유를 BULKLOAD로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-127">The engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed to inserting into the delta store) but sets the trim reason to BULKLOAD.</span></span> <span data-ttu-id="39ef3-128">이 시나리오에서는 행이 더 많이 누적되도록 배치 로드 기간을 늘리는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-128">In this scenario, consider increasing your batch load window to accumulate more rows.</span></span> <span data-ttu-id="39ef3-129">또한 행 그룹은 파티션 경계를 벗어나도록 배치될 수 없으므로, 파티션 구성표를 다시 평가하여 파티션이 너무 세밀하지 않은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-129">Also, reevaluate your partitioning scheme to ensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="39ef3-130">MEMORY_LIMITATION: 행이 1백만 개인 행 그룹을 만들려는 경우 엔진에는 일정량의 작업 메모리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-130">MEMORY_LIMITATION: To create row groups with 1 million rows, a certain amount of working memory is required by the engine.</span></span> <span data-ttu-id="39ef3-131">로딩 세션의 사용 가능한 메모리가 필요한 작업 메모리보다 적으면 행 그룹이 중간에 잘립니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-131">When available memory of the loading session is less than the required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="39ef3-132">필요한 메모리를 예측하고 메모리를 추가로 할당하는 방법은 다음 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-132">The following sections explain how to estimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="39ef3-133">DICTIONARY_SIZE: 이 자르기 이유는 너비 및/또는 높이 값이 큰 카디널리티 문자열이 포함된 문자열 열이 하나 이상 있어서 행 그룹이 잘렸음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="39ef3-134">메모리에서 사전 크기는 16MB로 제한되며, 이 제한에 도달하면 행 그룹은 압축됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-134">The dictionary size is limited to 16 MB in memory and once this limit is reached the row group is compressed.</span></span> <span data-ttu-id="39ef3-135">이러한 상황이 발생하는 경우 문제가 되는 열을 별도의 테이블에 포함해 보세요.</span><span class="sxs-lookup"><span data-stu-id="39ef3-135">If you do run into this situation, consider isolating the problematic column into a separate table.</span></span>

## <a name="how-to-estimate-memory-requirements"></a><span data-ttu-id="39ef3-136">메모리 요구 사항을 예측하는 방법</span><span class="sxs-lookup"><span data-stu-id="39ef3-136">How to estimate memory requirements</span></span>

<!--
To view an estimate of the memory requirements to compress a rowgroup of maximum size into a columnstore index, download and run the view [dbo.vCS_mon_mem_grant](). This view shows the size of the memory grant that a rowgroup requires for compression in to the columnstore.
-->

<span data-ttu-id="39ef3-137">한 개의 행 그룹을 압축하는 데 필요한 최대 메모리는 대략적으로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-137">The maximum required memory to compress one rowgroup is approximately</span></span>

- <span data-ttu-id="39ef3-138">72MB +</span><span class="sxs-lookup"><span data-stu-id="39ef3-138">72 MB +</span></span>
- <span data-ttu-id="39ef3-139">\#행 \* \#열 \* 8바이트 +</span><span class="sxs-lookup"><span data-stu-id="39ef3-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="39ef3-140">\#행 \* \#short-string-columns \* 32바이트 +</span><span class="sxs-lookup"><span data-stu-id="39ef3-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="39ef3-141">압축 사전인 경우 \#long-string-columns \* 16MB</span><span class="sxs-lookup"><span data-stu-id="39ef3-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="39ef3-142">여기서 short-string-columns는 32바이트 이하의 문자열 데이터 형식을 사용하고 long-string-columns는 32바이트를 초과하는 문자열 데이터 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="39ef3-143">긴 문자열은 텍스트 압축용으로 고안된 압축 방법으로 압축됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="39ef3-144">이 압축 방법은 *사전*을 사용하여 텍스트 패턴을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-144">This compression method uses a *dictionary* to store text patterns.</span></span> <span data-ttu-id="39ef3-145">사전의 최대 크기는 16MB입니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-145">The maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="39ef3-146">행 그룹에는 긴 문자열 각각에 대해 사전이 한 개만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-146">There is only one dictionary for each long string column in the rowgroup.</span></span>

<span data-ttu-id="39ef3-147">columnstore 메모리 요구 사항에 대한 자세한 내용은 [Azure SQL Data Warehouse 확장: 구성 및 지침](https://myignite.microsoft.com/videos/14822) 비디오를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39ef3-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-to-reduce-memory-requirements"></a><span data-ttu-id="39ef3-148">메모리 요구 사항을 줄이는 방법</span><span class="sxs-lookup"><span data-stu-id="39ef3-148">Ways to reduce memory requirements</span></span>

<span data-ttu-id="39ef3-149">다음 기술을 사용하여 행 그룹을 columnstore 인덱스로 압축하기 위한 메모리 요구 사항을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-149">Use the following techniques to reduce the memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="39ef3-150">적은 수의 열 사용</span><span class="sxs-lookup"><span data-stu-id="39ef3-150">Use fewer columns</span></span>
<span data-ttu-id="39ef3-151">가능한 경우 열 수를 줄여서 테이블을 설계하세요.</span><span class="sxs-lookup"><span data-stu-id="39ef3-151">If possible, design the table with fewer columns.</span></span> <span data-ttu-id="39ef3-152">행 그룹이 columnstore로 압축된 경우 columnstore 인덱스는 각 열 세그먼트를 별도로 압축합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-152">When a rowgroup is compressed into the columnstore, the columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="39ef3-153">따라서 열 수가 늘어나면 행 그룹을 압축하기 위한 메모리 요구 사항이 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-153">Therefore the memory requirements to compress a rowgroup increase as the number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="39ef3-154">적은 수의 문자열 열 사용</span><span class="sxs-lookup"><span data-stu-id="39ef3-154">Use fewer string columns</span></span>
<span data-ttu-id="39ef3-155">문자열 데이터 형식의 열에는 숫자 및 날짜 데이터 형식보다 더 많은 메모리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="39ef3-156">메모리 요구 사항을 줄이려면 팩트 테이블에서 문자열 열을 제거하고 더 작은 차원 테이블에 배치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-156">To reduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="39ef3-157">문자열 압축을 위한 추가 메모리 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="39ef3-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="39ef3-158">32자 이하의 문자열 데이터 형식에는 값당 32바이트가 더 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-158">String data types up to 32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="39ef3-159">32자를 초과하는 문자열 데이터 형식은 사전 방법을 사용하여 압축됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="39ef3-160">행 그룹의 각 열에는 사전을 작성하기 위해 최대 16MB가 더 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-160">Each column in the rowgroup can require up to an additional 16 MB to build the dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="39ef3-161">오버 분할 방지</span><span class="sxs-lookup"><span data-stu-id="39ef3-161">Avoid over-partitioning</span></span>

<span data-ttu-id="39ef3-162">Columnstore 인덱스는 파티션당 행 그룹을 하나 이상 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="39ef3-163">SQL Data Warehouse에서는 데이터가 배포되고 각 배포가 분할되므로 파티션 수가 금방 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-163">In SQL Data Warehouse, the number of partitions grows quickly because the data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="39ef3-164">테이블에 너무 많은 파티션이 있으면 행 그룹을 채우기에 충분하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-164">If the table has too many partitions, there might not be enough rows to fill the rowgroups.</span></span> <span data-ttu-id="39ef3-165">행이 부족하다고 해서 압축 중에 메모리 부족이 발생하지는 않지만 행 그룹에서 최적의 columnstore 쿼리 성능을 달성하지 못하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-165">The lack of rows does not create memory pressure during compression, but it leads to rowgroups that do not achieve the best columnstore query performance.</span></span>

<span data-ttu-id="39ef3-166">오버 분할을 방지하는 다른 이유는 행을 분할된 테이블의 columnstore 인덱스에 로드하는 데 메모리 오버헤드가 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-166">Another reason to avoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="39ef3-167">로드하는 동안 많은 파티션이 들어오는 행을 수신할 수 있으며 각 파티션이 압축할 행을 충분히 포함할 때까지 행은 메모리에 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-167">During a load, many partitions could receive the incoming rows, which are held in memory until each partition has enough rows to be compressed.</span></span> <span data-ttu-id="39ef3-168">너무 많은 파티션이 있으면 메모리 부족이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-the-load-query"></a><span data-ttu-id="39ef3-169">로드 쿼리 간소화</span><span class="sxs-lookup"><span data-stu-id="39ef3-169">Simplify the load query</span></span>

<span data-ttu-id="39ef3-170">데이터베이스는 쿼리에서 모든 연산자 간 쿼리에 대한 메모리 부여를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-170">The database shares the memory grant for a query among all the operators in the query.</span></span> <span data-ttu-id="39ef3-171">로드 쿼리에 복잡한 정렬 및 조인이 있는 경우 압축에 사용 가능한 메모리가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-171">When a load query has complex sorts and joins, the memory available for compression is reduced.</span></span>

<span data-ttu-id="39ef3-172">쿼리를 로드하는 데만 집중할 로드 쿼리를 디자인합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-172">Design the load query to focus only on loading the query.</span></span> <span data-ttu-id="39ef3-173">데이터 변환을 실행해야 할 경우 로드 쿼리와 별도로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-173">If you need to run transformations on the data, run them separate from the load query.</span></span> <span data-ttu-id="39ef3-174">예를 들어, 힙 테이블의 데이터를 준비하고 변환을 실행한 후 준비 테이블을 columnstore 인덱스에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-174">For example, stage the data in a heap table, run the transformations, and then load the staging table into the columnstore index.</span></span> <span data-ttu-id="39ef3-175">또한 데이터를 먼저 로드한 후 MPP 시스템을 사용하여 데이터를 변환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-175">You can also load the data first and then use the MPP system to transform the data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="39ef3-176">MAXDOP 조정</span><span class="sxs-lookup"><span data-stu-id="39ef3-176">Adjust MAXDOP</span></span>

<span data-ttu-id="39ef3-177">각 배포에서는 배포당 사용 가능한 CPU 코어가 두 개 이상 있는 경우 행 그룹을 columnstore로 병렬로 압축합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-177">Each distribution compresses rowgroups into the columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="39ef3-178">병렬 처리는 메모리 부족 및 행 그룹 트리밍을 야기할 수 있는 추가 메모리 리소스를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-178">The parallelism requires additional memory resources, which can lead to memory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="39ef3-179">메모리 부족을 줄이기 위해 MAXDOP 쿼리 힌트를 사용하여 로드 작업이 각 배포 내에서 직렬 모드로 강제로 실행되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-179">To reduce memory pressure, you can use the MAXDOP query hint to force the load operation to run in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-to-allocate-more-memory"></a><span data-ttu-id="39ef3-180">더 많은 메모리를 할당하는 방법</span><span class="sxs-lookup"><span data-stu-id="39ef3-180">Ways to allocate more memory</span></span>

<span data-ttu-id="39ef3-181">DWU 크기와 사용자 리소스 클래스를 함께 사용하여 사용자 쿼리에 사용 가능한 메모리 양을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-181">DWU size and the user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="39ef3-182">로드 쿼리에 대한 메모리 부여를 늘리려면 DWU 수를 늘리거나 리소스 클래스 수를 늘리면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-182">To increase the memory grant for a load query, you can either increase the number of DWUs or increase the resource class.</span></span>

- <span data-ttu-id="39ef3-183">DWU 수를 늘리려면 [성능을 조정하려면 어떻게 해야 합니까?](sql-data-warehouse-manage-compute-overview.md#scale-compute)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39ef3-183">To increase the DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="39ef3-184">쿼리에 대한 리소스 클래스를 변경하려면 [사용자 리소스 클래스 변경 예제](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39ef3-184">To change the resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="39ef3-185">예를 들어 DWU 100에서는 smallrc 리소스 클래스의 사용자는 배포당 100MB의 메모리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-185">For example, on DWU 100 a user in the smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="39ef3-186">자세한 내용은 [SQL Data Warehouse의 동시성](sql-data-warehouse-develop-concurrency.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39ef3-186">For the details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="39ef3-187">고품질 행 그룹 크기를 가져오려면 700MB의 메모리가 필요하다고 판단된다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-187">Suppose you determine that you need 700 MB of memory to get high-quality rowgroup sizes.</span></span> <span data-ttu-id="39ef3-188">다음 예제는 충분한 메모리로 로드 쿼리를 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-188">These examples show how you can run the load query with enough memory.</span></span>

- <span data-ttu-id="39ef3-189">DWU 1000 및 mediumrc를 사용하면 메모리 부여는 800MB입니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="39ef3-190">DWU 600 및 largerc를 사용하면 메모리 부여는 800MB입니다.</span><span class="sxs-lookup"><span data-stu-id="39ef3-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="39ef3-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="39ef3-191">Next steps</span></span>

<span data-ttu-id="39ef3-192">SQL Data Warehouse의 성능을 향상시키기 위해 여러 가지 방법을 찾으려면 [성능 개요](sql-data-warehouse-overview-manage-user-queries.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39ef3-192">To find more ways to improve performance in SQL Data Warehouse, see the [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
