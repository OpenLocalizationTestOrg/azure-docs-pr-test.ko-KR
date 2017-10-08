---
title: "Azure sql에서 aaaImprove columnstore 인덱스 성능 | Microsoft Docs"
description: "메모리 요구 사항을 줄이거나 각 행 그룹에 columnstore 인덱스를 압축 하는 행의 hello toomaximize hello 수를 사용 가능한 메모리를 늘리십시오."
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
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="75c77-103">columnstore의 행 그룹 품질 최대화</span><span class="sxs-lookup"><span data-stu-id="75c77-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="75c77-104">행 그룹 품질 hello 행 그룹의 행 수가 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-104">Rowgroup quality is determined by hello number of rows in a rowgroup.</span></span> <span data-ttu-id="75c77-105">메모리 요구 사항을 줄이거나 각 행 그룹에 columnstore 인덱스를 압축 하는 행의 hello toomaximize hello 수를 사용 가능한 메모리를 늘리십시오.</span><span class="sxs-lookup"><span data-stu-id="75c77-105">Reduce memory requirements or increase hello available memory toomaximize hello number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="75c77-106">Columnstore 인덱스에 대 한 이러한 방법 tooimprove 압축 비율과 쿼리 성능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-106">Use these methods tooimprove compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-hello-rowgroup-size-matters"></a><span data-ttu-id="75c77-107">Hello 행 그룹 크기 중요 한 이유</span><span class="sxs-lookup"><span data-stu-id="75c77-107">Why hello rowgroup size matters</span></span>
<span data-ttu-id="75c77-108">개별 행 그룹의 열 세그먼트를 검색 하 여 한 테이블을 검색 하는 columnstore 인덱스, 하므로 쿼리 성능이 향상 hello 각 행 그룹의 행 수를 극대화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing hello number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="75c77-109">행 그룹이 많은 수의 행 데이터 압축으로, 디스크에서 작은 데이터 tooread 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-109">When rowgroups have a high number of rows, data compression improves which means there is less data tooread from disk.</span></span>

<span data-ttu-id="75c77-110">행 그룹 에 대한 자세한 내용은 [Columnstore 인덱스 가이드](https://msdn.microsoft.com/library/gg492088.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75c77-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="75c77-111">행 그룹의 대상 크기</span><span class="sxs-lookup"><span data-stu-id="75c77-111">Target size for rowgroups</span></span>
<span data-ttu-id="75c77-112">최고의 쿼리 성능을 위해 hello 목적은 toomaximize hello 수가 행 그룹당 최대 columnstore 인덱스의 행입니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-112">For best query performance, hello goal is toomaximize hello number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="75c77-113">행 그룹은 최대 1,048,576개의 행을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="75c77-114">덮어쓰려면 toonot hello 최대 행 그룹당 최대 행 수가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-114">It's okay toonot have hello maximum number of rows per rowgroup.</span></span> <span data-ttu-id="75c77-115">Columnstore 인덱스는 행 그룹에 100,000개 이상의 행이 있을 때 적절한 성능을 달성합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="75c77-116">압축 중에 행 그룹을 잘라낼 수 있음</span><span class="sxs-lookup"><span data-stu-id="75c77-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="75c77-117">대량 로드 또는 columnstore 인덱스 다시 작성 하는 동안 때로는 없는 각 행 그룹에 대해 지정 된 행을 hello 모두 만큼 충분 한 메모리 사용 가능한 toocompress 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available toocompress all hello rows designated for each rowgroup.</span></span> <span data-ttu-id="75c77-118">메모리 압박이 있는 경우 columnstore 인덱스는 hello columnstore로 압축 성공할 수 있도록 hello 행 그룹 크기를 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-118">When there is memory pressure, columnstore indexes trim hello rowgroup sizes so compression into hello columnstore can succeed.</span></span> 

<span data-ttu-id="75c77-119">각 행 그룹에 메모리가 부족 하 여 toocompress 적어도 10, 000 행 되는 경우 SQL 데이터 웨어하우스 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-119">When there is insufficient memory toocompress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="75c77-120">대량 로드에 대한 자세한 내용은 [클러스터형 columnstore 인덱스로 대량 로드](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75c77-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-toomonitor-rowgroup-quality"></a><span data-ttu-id="75c77-121">어떻게 toomonitor rowgroup 품질</span><span class="sxs-lookup"><span data-stu-id="75c77-121">How toomonitor rowgroup quality</span></span>

<span data-ttu-id="75c77-122">Trimming가 있을 경우 잘라내기 rowgroup 및 hello 이유의 행 수 등 유용한 정보를 노출 하는 DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and hello reason for trimming if there was trimming.</span></span> <span data-ttu-id="75c77-123">행 그룹 트리밍에 편리한 방법 tooquery로 보기를 수행 하는 hello이 DMV tooget 정보를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-123">You can create hello following view as a handy way tooquery this DMV tooget information on rowgroup trimming.</span></span>

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

<span data-ttu-id="75c77-124">hello trim_reason_desc hello rowgroup 잘린 있는지 여부를 알려 줍니다 (trim_reason_desc = 잘리지 했습니다 및 행 그룹은 최적의 품질 NO_TRIM 함축).</span><span class="sxs-lookup"><span data-stu-id="75c77-124">hello trim_reason_desc tells whether hello rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="75c77-125">hello 트림 다음과 같은 이유로 다음과 같이 나타냅니다. hello 행 그룹의 중간 트리밍</span><span class="sxs-lookup"><span data-stu-id="75c77-125">hello following trim reasons indicate premature trimming of hello rowgroup:</span></span>
- <span data-ttu-id="75c77-126">BULKLOAD: 트림이 이유는 hello 부하에 대 한 행의 들어오는 일괄 처리 hello 보다 작거나 1 백만 행이 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-126">BULKLOAD: This trim reason is used when hello incoming batch of rows for hello load had less than 1 million rows.</span></span> <span data-ttu-id="75c77-127">hello 델타 저장소로 것과 반대로 tooinserting) (으로 삽입 되는 100, 000 행 보다 큰 있지만 집합 hello 트림 이유 tooBULKLOAD 경우 hello 엔진은 압축 된 행 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-127">hello engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed tooinserting into hello delta store) but sets hello trim reason tooBULKLOAD.</span></span> <span data-ttu-id="75c77-128">이 시나리오에서는 더 많은 행에 일괄 처리 부하 창 tooaccumulate 증가 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-128">In this scenario, consider increasing your batch load window tooaccumulate more rows.</span></span> <span data-ttu-id="75c77-129">또한 상태가 아닙니다 너무 세분화 행 그룹 파티션 경계에 걸쳐 있을 수 하 여 파티션 구성표 tooensure 다시 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-129">Also, reevaluate your partitioning scheme tooensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="75c77-130">MEMORY_LIMITATION: hello 엔진에 의해 toocreate 행 그룹 1 백만 행, 일정량의 작업 중인 메모리에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-130">MEMORY_LIMITATION: toocreate row groups with 1 million rows, a certain amount of working memory is required by hello engine.</span></span> <span data-ttu-id="75c77-131">사용 가능한 메모리의 세션을 로드 하는 hello hello 작업 중인 메모리 필요한 것 보다 작은 경우 행 그룹 잘립니다 중간 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-131">When available memory of hello loading session is less than hello required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="75c77-132">다음 섹션 hello tooestimate 메모리 필요 하 고 더 많은 메모리를 할당 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-132">hello following sections explain how tooestimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="75c77-133">DICTIONARY_SIZE: 이 자르기 이유는 너비 및/또는 높이 값이 큰 카디널리티 문자열이 포함된 문자열 열이 하나 이상 있어서 행 그룹이 잘렸음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="75c77-134">hello 사전 크기는 MB 메모리 및이 한도 도달 hello 행 그룹이 압축 된 제한 too16입니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-134">hello dictionary size is limited too16 MB in memory and once this limit is reached hello row group is compressed.</span></span> <span data-ttu-id="75c77-135">이 경우를 실행 하는 않는 경우 hello 문제가 있는 열을 별도 테이블로 분리 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-135">If you do run into this situation, consider isolating hello problematic column into a separate table.</span></span>

## <a name="how-tooestimate-memory-requirements"></a><span data-ttu-id="75c77-136">어떻게 tooestimate 메모리 요구 사항</span><span class="sxs-lookup"><span data-stu-id="75c77-136">How tooestimate memory requirements</span></span>

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

<span data-ttu-id="75c77-137">hello 필요한 메모리를 최대 toocompress 한 행 그룹은 대략</span><span class="sxs-lookup"><span data-stu-id="75c77-137">hello maximum required memory toocompress one rowgroup is approximately</span></span>

- <span data-ttu-id="75c77-138">72MB +</span><span class="sxs-lookup"><span data-stu-id="75c77-138">72 MB +</span></span>
- <span data-ttu-id="75c77-139">\#행 \* \#열 \* 8바이트 +</span><span class="sxs-lookup"><span data-stu-id="75c77-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="75c77-140">\#행 \* \#short-string-columns \* 32바이트 +</span><span class="sxs-lookup"><span data-stu-id="75c77-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="75c77-141">압축 사전인 경우 \#long-string-columns \* 16MB</span><span class="sxs-lookup"><span data-stu-id="75c77-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="75c77-142">여기서 short-string-columns는 32바이트 이하의 문자열 데이터 형식을 사용하고 long-string-columns는 32바이트를 초과하는 문자열 데이터 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="75c77-143">긴 문자열은 텍스트 압축용으로 고안된 압축 방법으로 압축됩니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="75c77-144">이 압축 방법을 사용 하 여 한 *사전* toostore 텍스트 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-144">This compression method uses a *dictionary* toostore text patterns.</span></span> <span data-ttu-id="75c77-145">hello 사전의 최대 크기는 16MB입니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-145">hello maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="75c77-146">Hello 행 그룹의 각 긴 문자열 열에 대 한 사전이 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-146">There is only one dictionary for each long string column in hello rowgroup.</span></span>

<span data-ttu-id="75c77-147">columnstore 메모리 요구 사항에 대한 자세한 내용은 [Azure SQL Data Warehouse 확장: 구성 및 지침](https://myignite.microsoft.com/videos/14822) 비디오를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75c77-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-tooreduce-memory-requirements"></a><span data-ttu-id="75c77-148">같은 방법으로 tooreduce 메모리 요구 사항</span><span class="sxs-lookup"><span data-stu-id="75c77-148">Ways tooreduce memory requirements</span></span>

<span data-ttu-id="75c77-149">Hello 기술을 tooreduce hello 메모리 요구 사항을 준수 rowgroup을 columnstore 인덱스에 압축 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-149">Use hello following techniques tooreduce hello memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="75c77-150">적은 수의 열 사용</span><span class="sxs-lookup"><span data-stu-id="75c77-150">Use fewer columns</span></span>
<span data-ttu-id="75c77-151">가능 하면 열이 적은 hello 테이블을 디자인 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-151">If possible, design hello table with fewer columns.</span></span> <span data-ttu-id="75c77-152">Hello columnstore에 compressed 임을 hello columnstore 인덱스 각 열 세그먼트를 개별적으로 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-152">When a rowgroup is compressed into hello columnstore, hello columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="75c77-153">따라서 hello toocompress 행 그룹 hello 수 열 증가으로 증가 하는 메모리 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-153">Therefore hello memory requirements toocompress a rowgroup increase as hello number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="75c77-154">적은 수의 문자열 열 사용</span><span class="sxs-lookup"><span data-stu-id="75c77-154">Use fewer string columns</span></span>
<span data-ttu-id="75c77-155">문자열 데이터 형식의 열에는 숫자 및 날짜 데이터 형식보다 더 많은 메모리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="75c77-156">tooreduce 메모리 요구 사항을 팩트 테이블에서 문자열 열을 제거 하 고 더 작은 차원 테이블에 삽입 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-156">tooreduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="75c77-157">문자열 압축을 위한 추가 메모리 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="75c77-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="75c77-158">Too32 문자를 문자열 데이터 형식 값 당 32 바이트의 추가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-158">String data types up too32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="75c77-159">32자를 초과하는 문자열 데이터 형식은 사전 방법을 사용하여 압축됩니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="75c77-160">Hello 행 그룹의 각 열은 tooan 추가 16MB toobuild hello 사전을 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-160">Each column in hello rowgroup can require up tooan additional 16 MB toobuild hello dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="75c77-161">오버 분할 방지</span><span class="sxs-lookup"><span data-stu-id="75c77-161">Avoid over-partitioning</span></span>

<span data-ttu-id="75c77-162">Columnstore 인덱스는 파티션당 행 그룹을 하나 이상 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="75c77-163">SQL 데이터 웨어하우스, 파티션 수가 hello hello 데이터를 배포 하 고 각 배포는 분할 되므로 신속 하 게를 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-163">In SQL Data Warehouse, hello number of partitions grows quickly because hello data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="75c77-164">Hello 테이블에 너무 많은 분할 경우 있을 수 있습니다 하지 충분 한 행 toofill hello 행 그룹.</span><span class="sxs-lookup"><span data-stu-id="75c77-164">If hello table has too many partitions, there might not be enough rows toofill hello rowgroups.</span></span> <span data-ttu-id="75c77-165">행의 hello 부족 압축 하는 동안 메모리 부족을 만들지 않습니다 되지만 hello columnstore 최고의 쿼리 성능의 얻을 toorowgroups 유발 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-165">hello lack of rows does not create memory pressure during compression, but it leads toorowgroups that do not achieve hello best columnstore query performance.</span></span>

<span data-ttu-id="75c77-166">또 다른 이유 tooavoid 과도 하 게 분할은 분할된 된 테이블에서 columnstore 인덱스로 행을 로드 하는 오버 헤드를 메모리가입니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-166">Another reason tooavoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="75c77-167">로드 하는 동안 파티션 수는 각 파티션에 충분 한 행 toobe 압축 될 때까지 메모리에 보관 되는 hello 들어오는 행을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-167">During a load, many partitions could receive hello incoming rows, which are held in memory until each partition has enough rows toobe compressed.</span></span> <span data-ttu-id="75c77-168">너무 많은 파티션이 있으면 메모리 부족이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-hello-load-query"></a><span data-ttu-id="75c77-169">쿼리를 로드 하는 hello를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-169">Simplify hello load query</span></span>

<span data-ttu-id="75c77-170">hello 데이터베이스에 대 한 모든 hello 연산자 hello 쿼리 간에 쿼리 메모리 부여 hello를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-170">hello database shares hello memory grant for a query among all hello operators in hello query.</span></span> <span data-ttu-id="75c77-171">쿼리 로드에 복잡 한 정렬 및 조인이 있는 경우 압축에 대해 사용할 수 있는 hello 메모리 감소 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-171">When a load query has complex sorts and joins, hello memory available for compression is reduced.</span></span>

<span data-ttu-id="75c77-172">Hello 쿼리 로드에 대해서만 hello 부하 쿼리 toofocus를 디자인 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-172">Design hello load query toofocus only on loading hello query.</span></span> <span data-ttu-id="75c77-173">Hello 데이터에 대 한 toorun 변형 해야 할 경우 실행할 쿼리를 로드 하는 hello와 별도로 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-173">If you need toorun transformations on hello data, run them separate from hello load query.</span></span> <span data-ttu-id="75c77-174">예를 들어 단계 hello 데이터 힙 테이블에 hello 변환을 실행 하 고 hello columnstore 인덱스로 테이블을 준비 하는 hello를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-174">For example, stage hello data in a heap table, run hello transformations, and then load hello staging table into hello columnstore index.</span></span> <span data-ttu-id="75c77-175">먼저 hello 데이터를 로드할 수도 있고 hello MPP 시스템 tootransform hello 데이터를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-175">You can also load hello data first and then use hello MPP system tootransform hello data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="75c77-176">MAXDOP 조정</span><span class="sxs-lookup"><span data-stu-id="75c77-176">Adjust MAXDOP</span></span>

<span data-ttu-id="75c77-177">각 배포 배포 당 사용 가능한 CPU 코어를 하나 이상 없을 경우 병렬로 hello columnstore에 행 그룹을 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-177">Each distribution compresses rowgroups into hello columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="75c77-178">hello parallelism toomemory 압력과 rowgroup 트리밍 될 수 있는 추가 메모리 리소스를 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-178">hello parallelism requires additional memory resources, which can lead toomemory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="75c77-179">tooreduce 메모리가 중, 각 배포 내에서 직렬 모드로 hello MAXDOP 쿼리 힌트 tooforce hello 부하 작업 toorun를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-179">tooreduce memory pressure, you can use hello MAXDOP query hint tooforce hello load operation toorun in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a><span data-ttu-id="75c77-180">같은 방법으로 tooallocate 더 많은 메모리</span><span class="sxs-lookup"><span data-stu-id="75c77-180">Ways tooallocate more memory</span></span>

<span data-ttu-id="75c77-181">DWU 크기와 hello 사용자 리소스 클래스 메모리 크기는 사용자 쿼리를 실행할 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-181">DWU size and hello user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="75c77-182">tooincrease hello 메모리 Dwu hello 수를 증가 하거나 hello 리소스 클래스를 높일 수 있습니다 쿼리 로드에 대 한 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-182">tooincrease hello memory grant for a load query, you can either increase hello number of DWUs or increase hello resource class.</span></span>

- <span data-ttu-id="75c77-183">tooincrease hello dwu로, 참조 [성능 확장 방법을?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="75c77-183">tooincrease hello DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="75c77-184">쿼리의 경우 toochange hello 리소스 클래스 참조 [사용자 리소스 클래스 예제 변경](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example)합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-184">toochange hello resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="75c77-185">예를 들어 DWU 100에 hello smallrc 리소스 클래스에서 사용자 צ ְ ײ 100MB 메모리의 각 배포에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-185">For example, on DWU 100 a user in hello smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="75c77-186">Hello 세부 정보를 참조 하십시오. [SQL 데이터 웨어하우스의 동시성](sql-data-warehouse-develop-concurrency.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-186">For hello details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="75c77-187">700MB 메모리 tooget 고품질 행 그룹 크기의 필요 하다 고 판단 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-187">Suppose you determine that you need 700 MB of memory tooget high-quality rowgroup sizes.</span></span> <span data-ttu-id="75c77-188">이러한 예제 충분 한 메모리가 있는 hello 부하 쿼리를 실행 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-188">These examples show how you can run hello load query with enough memory.</span></span>

- <span data-ttu-id="75c77-189">DWU 1000 및 mediumrc를 사용하면 메모리 부여는 800MB입니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="75c77-190">DWU 600 및 largerc를 사용하면 메모리 부여는 800MB입니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="75c77-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75c77-191">Next steps</span></span>

<span data-ttu-id="75c77-192">toofind hello를 참조 하는 방법으로 tooimprove 성능이 SQL 데이터 웨어하우스에 [성능 개요](sql-data-warehouse-overview-manage-user-queries.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="75c77-192">toofind more ways tooimprove performance in SQL Data Warehouse, see hello [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
