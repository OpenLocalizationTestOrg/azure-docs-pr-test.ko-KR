---
title: "저장소 테이블 디자인 가이드 aaaAzure | Microsoft Docs"
description: "Azure 테이블 저장소에서 확장형 및 영구 테이블 디자인"
services: cosmos-db
documentationcenter: na
author: mimig1
manager: tadb
editor: tysonn
ms.assetid: 8e228b0c-2998-4462-8101-9f16517393ca
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 02/28/2017
ms.author: mimig
ms.openlocfilehash: 059f05a1d20e4d9537034b7ca133c5334bbefa04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-table-design-guide-designing-scalable-and-performant-tables"></a><span data-ttu-id="3a08f-103">Azure 저장소 테이블 디자인 가이드: 확장성이 뛰어난 디자인 및 성능이 뛰어난 테이블</span><span class="sxs-lookup"><span data-stu-id="3a08f-103">Azure Storage Table Design Guide: Designing Scalable and Performant Tables</span></span>
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="3a08f-104">toodesign 확장성과 성능이 뛰어난 테이블 다양 한 성능, 확장성 및 비용 등의 요소를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-104">toodesign scalable and performant tables you must consider a number of factors such as performance, scalability, and cost.</span></span> <span data-ttu-id="3a08f-105">관계형 데이터베이스에 대 한 스키마를 이전에 디자인에 이러한 고려 사항에 친숙 한 tooyou 됩니다 hello Azure 테이블 서비스 저장소 모델 및 관계형 모델 간의 몇 가지 유사점 상태인 분명 하지만 많은 중요 한 차이입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-105">If you have previously designed schemas for relational databases, these considerations will be familiar tooyou, but while there are some similarities between hello Azure Table service storage model and relational models, there are also many important differences.</span></span> <span data-ttu-id="3a08f-106">이러한 차이는 일반적으로 잘못 되었거나 비 직관적인 toosomeone 관계형 데이터베이스에 잘 알고 표시 될 수는 있지만 hello Azure 테이블 서비스와 같은 NoSQL 키/값 저장소를 디자인 하는 경우에 대 한 이해 수행 있는 여러 디자인 toovery 될 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-106">These differences typically lead toovery different designs that may look counter-intuitive or wrong toosomeone familiar with relational databases, but which do make good sense if you are designing for a NoSQL key/value store such as hello Azure Table service.</span></span> <span data-ttu-id="3a08f-107">테이블 서비스 hello 수십억 개의 엔터티 (행 관계형 데이터베이스 용어에서)의 데이터 또는 매우 높은 지원 해야 하는 데이터 집합에 포함 될 수 있는 디자인 된 toosupport 클라우드 규모 응용 프로그램 된다는 hello 사실에 입각 반영 됩니다 대부분의 디자인 차이점 트랜잭션 볼륨이: 따라서 데이터를 저장 하는 방법에 대 한 다르게 toothink 필요 하며 hello 테이블 서비스의 작동 방식을 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-107">Many of your design differences will reflect hello fact that hello Table service is designed toosupport cloud-scale applications that can contain billions of entities (rows in relational database terminology) of data or for datasets that must support very high transaction volumes: therefore, you need toothink differently about how you store your data and understand how hello Table service works.</span></span> <span data-ttu-id="3a08f-108">훨씬 더에 (및 저렴 한 비용)는 잘 설계 된 NoSQL 데이터 저장소 솔루션 tooscale 사용 하도록 설정할 수는 관계형 데이터베이스를 사용 하는 솔루션 보다 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-108">A well designed NoSQL data store can enable your solution tooscale much further (and at a lower cost) than a solution that uses a relational database.</span></span> <span data-ttu-id="3a08f-109">이 가이드에서는 이러한 항목에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-109">This guide helps you with these topics.</span></span>  

## <a name="about-hello-azure-table-service"></a><span data-ttu-id="3a08f-110">Hello Azure 테이블 서비스에 대 한</span><span class="sxs-lookup"><span data-stu-id="3a08f-110">About hello Azure Table service</span></span>
<span data-ttu-id="3a08f-111">이 섹션을 강조 표시 기능 중 일부 hello 키 hello 테이블 서비스의 성능과 확장성에 대 한 관련 toodesigning 특히는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-111">This section highlights some of hello key features of hello Table service that are especially relevant toodesigning for performance and scalability.</span></span> <span data-ttu-id="3a08f-112">새 tooAzure 저장소 및 테이블 서비스 hello 인 경우 먼저 읽어 [Azure 저장소 소개 tooMicrosoft](../storage/common/storage-introduction.md) 및 [.NET을 사용 하 여 Azure 테이블 저장소 시작](table-storage-how-to-use-dotnet.md) hello 나머지를 읽기 전에 아티클을 말합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-112">If you are new tooAzure Storage and hello Table service, first read [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) and [Get started with Azure Table Storage using .NET](table-storage-how-to-use-dotnet.md) before reading hello remainder of this article.</span></span> <span data-ttu-id="3a08f-113">이 가이드의 hello 초점은 hello 테이블 서비스에 있는 경우에 일부 설명은 hello Azure 큐 및 Blob 서비스에 사용 하는 방법으로 hello 솔루션에서 테이블 서비스와 함께 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-113">Although hello focus of this guide is on hello Table service, it will include some discussion of hello Azure Queue and Blob services, and how you might use them along with hello Table service in a solution.</span></span>  

<span data-ttu-id="3a08f-114">Hello 테이블 서비스는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3a08f-114">What is hello Table service?</span></span> <span data-ttu-id="3a08f-115">Hello 이름에서 예상과 hello 테이블 서비스는 테이블 형식으로 toostore 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-115">As you might expect from hello name, hello Table service uses a tabular format toostore data.</span></span> <span data-ttu-id="3a08f-116">Hello 표준 용어 hello 테이블의 각 행 엔터티를 나타내고 hello 열 저장소 hello 해당 엔터티에의 다양 한 속성.</span><span class="sxs-lookup"><span data-stu-id="3a08f-116">In hello standard terminology, each row of hello table represents an entity, and hello columns store hello various properties of that entity.</span></span> <span data-ttu-id="3a08f-117">모든 엔터티에 하나만 지정 하는 한 쌍의 키 toouniquely 하 고 테이블 서비스 hello 타임 스탬프 열 hello 엔터티를 마지막으로 수정한 tootrack 사용 (이 자동으로 발생 하 고 임의 값으로 수동으로 hello 타임 스탬프를 덮어쓸 수 없습니다).</span><span class="sxs-lookup"><span data-stu-id="3a08f-117">Every entity has a pair of keys toouniquely identify it, and a timestamp column that hello Table service uses tootrack when hello entity was last updated (this happens automatically and you cannot manually overwrite hello timestamp with an arbitrary value).</span></span> <span data-ttu-id="3a08f-118">테이블 서비스 hello이 마지막 수정 타임 스탬프 (LMT) toomanage 낙관적 동시성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-118">hello Table service uses this last-modified timestamp (LMT) toomanage optimistic concurrency.</span></span>  

> [!NOTE]
> <span data-ttu-id="3a08f-119">hello 테이블 서비스 REST API 작업 반환할는 **ETag** hello 마지막 수정 타임 스탬프 (LMT)에서 파생 되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-119">hello Table service REST API operations also return an **ETag** value that it derives from hello last-modified timestamp (LMT).</span></span> <span data-ttu-id="3a08f-120">사용 하 여이 문서에 hello 조건 ETag 및 LMT 교대로 toohello 참조 하기 때문에 동일한 데이터 원본으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-120">In this document we will use hello terms ETag and LMT interchangeably because they refer toohello same underlying data.</span></span>  
> 
> 

<span data-ttu-id="3a08f-121">hello 다음 예제에서는 간단한 테이블 디자인 toostore employee 및 department 엔터티를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-121">hello following example shows a simple table design toostore employee and department entities.</span></span> <span data-ttu-id="3a08f-122">이 가이드의 뒷부분에 나오는 hello 예 중 대부분은이 간단한 디자인 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-122">Many of hello examples shown later in this guide are based on this simple design.</span></span>  

<table>
<tr>
<th><span data-ttu-id="3a08f-123">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="3a08f-123">PartitionKey</span></span></th>
<th><span data-ttu-id="3a08f-124">RowKey</span><span class="sxs-lookup"><span data-stu-id="3a08f-124">RowKey</span></span></th>
<th><span data-ttu-id="3a08f-125">Timestamp</span><span class="sxs-lookup"><span data-stu-id="3a08f-125">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td><span data-ttu-id="3a08f-126">Marketing</span><span class="sxs-lookup"><span data-stu-id="3a08f-126">Marketing</span></span></td>
<td><span data-ttu-id="3a08f-127">00001</span><span class="sxs-lookup"><span data-stu-id="3a08f-127">00001</span></span></td>
<td><span data-ttu-id="3a08f-128">2014-08-22T00:50:32Z</span><span class="sxs-lookup"><span data-stu-id="3a08f-128">2014-08-22T00:50:32Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="3a08f-129">FirstName</span><span class="sxs-lookup"><span data-stu-id="3a08f-129">FirstName</span></span></th>
<th><span data-ttu-id="3a08f-130">LastName</span><span class="sxs-lookup"><span data-stu-id="3a08f-130">LastName</span></span></th>
<th><span data-ttu-id="3a08f-131">Age</span><span class="sxs-lookup"><span data-stu-id="3a08f-131">Age</span></span></th>
<th><span data-ttu-id="3a08f-132">Email</span><span class="sxs-lookup"><span data-stu-id="3a08f-132">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="3a08f-133">Don</span><span class="sxs-lookup"><span data-stu-id="3a08f-133">Don</span></span></td>
<td><span data-ttu-id="3a08f-134">Hall</span><span class="sxs-lookup"><span data-stu-id="3a08f-134">Hall</span></span></td>
<td><span data-ttu-id="3a08f-135">34</span><span class="sxs-lookup"><span data-stu-id="3a08f-135">34</span></span></td>
<td>donh@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td><span data-ttu-id="3a08f-136">Marketing</span><span class="sxs-lookup"><span data-stu-id="3a08f-136">Marketing</span></span></td>
<td><span data-ttu-id="3a08f-137">00002</span><span class="sxs-lookup"><span data-stu-id="3a08f-137">00002</span></span></td>
<td><span data-ttu-id="3a08f-138">2014-08-22T00:50:34Z</span><span class="sxs-lookup"><span data-stu-id="3a08f-138">2014-08-22T00:50:34Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="3a08f-139">FirstName</span><span class="sxs-lookup"><span data-stu-id="3a08f-139">FirstName</span></span></th>
<th><span data-ttu-id="3a08f-140">LastName</span><span class="sxs-lookup"><span data-stu-id="3a08f-140">LastName</span></span></th>
<th><span data-ttu-id="3a08f-141">Age</span><span class="sxs-lookup"><span data-stu-id="3a08f-141">Age</span></span></th>
<th><span data-ttu-id="3a08f-142">Email</span><span class="sxs-lookup"><span data-stu-id="3a08f-142">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="3a08f-143">Jun</span><span class="sxs-lookup"><span data-stu-id="3a08f-143">Jun</span></span></td>
<td><span data-ttu-id="3a08f-144">Cao</span><span class="sxs-lookup"><span data-stu-id="3a08f-144">Cao</span></span></td>
<td><span data-ttu-id="3a08f-145">47</span><span class="sxs-lookup"><span data-stu-id="3a08f-145">47</span></span></td>
<td>junc@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td><span data-ttu-id="3a08f-146">Marketing</span><span class="sxs-lookup"><span data-stu-id="3a08f-146">Marketing</span></span></td>
<td><span data-ttu-id="3a08f-147">부서</span><span class="sxs-lookup"><span data-stu-id="3a08f-147">Department</span></span></td>
<td><span data-ttu-id="3a08f-148">2014-08-22T00:50:30Z</span><span class="sxs-lookup"><span data-stu-id="3a08f-148">2014-08-22T00:50:30Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="3a08f-149">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="3a08f-149">DepartmentName</span></span></th>
<th><span data-ttu-id="3a08f-150">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="3a08f-150">EmployeeCount</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="3a08f-151">Marketing</span><span class="sxs-lookup"><span data-stu-id="3a08f-151">Marketing</span></span></td>
<td><span data-ttu-id="3a08f-152">153</span><span class="sxs-lookup"><span data-stu-id="3a08f-152">153</span></span></td>
</tr>
</table>
</td>
</tr>
<tr>
<td><span data-ttu-id="3a08f-153">Sales</span><span class="sxs-lookup"><span data-stu-id="3a08f-153">Sales</span></span></td>
<td><span data-ttu-id="3a08f-154">00010</span><span class="sxs-lookup"><span data-stu-id="3a08f-154">00010</span></span></td>
<td><span data-ttu-id="3a08f-155">2014-08-22T00:50:44Z</span><span class="sxs-lookup"><span data-stu-id="3a08f-155">2014-08-22T00:50:44Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="3a08f-156">FirstName</span><span class="sxs-lookup"><span data-stu-id="3a08f-156">FirstName</span></span></th>
<th><span data-ttu-id="3a08f-157">LastName</span><span class="sxs-lookup"><span data-stu-id="3a08f-157">LastName</span></span></th>
<th><span data-ttu-id="3a08f-158">Age</span><span class="sxs-lookup"><span data-stu-id="3a08f-158">Age</span></span></th>
<th><span data-ttu-id="3a08f-159">Email</span><span class="sxs-lookup"><span data-stu-id="3a08f-159">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="3a08f-160">Ken</span><span class="sxs-lookup"><span data-stu-id="3a08f-160">Ken</span></span></td>
<td><span data-ttu-id="3a08f-161">Kwok</span><span class="sxs-lookup"><span data-stu-id="3a08f-161">Kwok</span></span></td>
<td><span data-ttu-id="3a08f-162">23</span><span class="sxs-lookup"><span data-stu-id="3a08f-162">23</span></span></td>
<td>kenk@contoso.com</td>
</tr>
</table>
</td>
</tr>
</table>


<span data-ttu-id="3a08f-163">지금까지이 매우 유사한 tooa 테이블 관계형 데이터베이스의 필수 열 hello 되 hello 주요 차이점이 모양과 hello 기능 toostore 여러 엔터티 형식을 hello에 동일한 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-163">So far, this looks very similar tooa table in a relational database with hello key differences being hello mandatory columns, and hello ability toostore multiple entity types in hello same table.</span></span> <span data-ttu-id="3a08f-164">또한 각 hello 사용자 정의 속성와 같은 **FirstName** 또는 **Age** 에 정수 또는 문자열 정당한 같은 관계형 데이터베이스의 열 같은 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-164">In addition, each of hello user-defined properties such as **FirstName** or **Age** has a data type, such as integer or string, just like a column in a relational database.</span></span> <span data-ttu-id="3a08f-165">와 달리 관계형 데이터베이스의 테이블 서비스 속성을 가질 필요가 있다는 hello의 스키마가 지정 되지 않은 특성 hello hello 동일 하지만 각 엔터티에 대해 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-165">Although unlike in a relational database, hello schema-less nature of hello Table service means that a property need not have hello same data type on each entity.</span></span> <span data-ttu-id="3a08f-166">단일 속성에 toostore 복잡 한 데이터 형식, 예: JSON 또는 XML serialize 된 형식을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-166">toostore complex data types in a single property, you must use a serialized format such as JSON or XML.</span></span> <span data-ttu-id="3a08f-167">Hello 테이블 서비스와 같은 지원 데이터 형식, 지원 되는 날짜 범위, 명명 규칙 및 크기 제약 조건에 대 한 자세한 내용은 참조 [테이블 서비스 데이터 모델 이해 hello](http://msdn.microsoft.com/library/azure/dd179338.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-167">For more information about hello table service such as supported data types, supported date ranges, naming rules, and size constraints, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="3a08f-168">살펴보게 되겠지만, 사용자가 선택한 **PartitionKey** 및 **RowKey** 기본 toogood 테이블 디자인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-168">As you will see, your choice of **PartitionKey** and **RowKey** is fundamental toogood table design.</span></span> <span data-ttu-id="3a08f-169">테이블에 저장된 모든 엔터티에는 고유하게 조합된 **PartitionKey**와 **RowKey**가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-169">Every entity stored in a table must have a unique combination of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="3a08f-170">관계형 데이터베이스 테이블의 키와 마찬가지로 hello **PartitionKey** 및 **RowKey** 값은 인덱싱된 toocreate 빠른 조회를 사용 하도록 설정 된 클러스터형된 인덱스가 있어 합니다; 그러나 테이블 서비스 hello 생성 되지 않습니다 보조 인덱스 hello 들은 두 개의 파일 인덱싱된 속성 (뒷부분에서 설명 하는 hello 패턴의 일부 표시이 명백한 제한을 해결할 수는 방법).</span><span class="sxs-lookup"><span data-stu-id="3a08f-170">As with keys in a relational database table, hello **PartitionKey** and **RowKey** values are indexed toocreate a clustered index that enables fast look-ups; however, hello Table service does not create any secondary indexes so these are hello only two indexed properties (some of hello patterns described later show how you can work around this apparent limitation).</span></span>  

<span data-ttu-id="3a08f-171">테이블은 하나 이상의 파티션을 구성 하 고 다양 한 hello 디자인는 적절 한 선택 주위 결정 하는 대로 **PartitionKey** 및 **RowKey** toooptimize 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-171">A table is made up of one or more partitions, and as you will see, many of hello design decisions you make will be around choosing a suitable **PartitionKey** and **RowKey** toooptimize your solution.</span></span> <span data-ttu-id="3a08f-172">솔루션은 파티션으로 구성된 모든 엔터티를 포함하는 단일 테이블로 구성될 수 있지만 일반적으로 솔루션에는 여러 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-172">A solution could consist of just a single table that contains all your entities organized into partitions, but typically a solution will have multiple tables.</span></span> <span data-ttu-id="3a08f-173">표 수 toologically 엔터티를 구성 하 고, 사용 하 여 액세스 toohello 데이터를 관리할 수 있게 액세스 제어 목록, 단일 저장소 작업을 사용 하 여 전체 테이블을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-173">Tables help you toologically organize your entities, help you manage access toohello data using access control lists, and you can drop an entire table using a single storage operation.</span></span>  

### <a name="table-partitions"></a><span data-ttu-id="3a08f-174">테이블 파티션</span><span class="sxs-lookup"><span data-stu-id="3a08f-174">Table partitions</span></span>
<span data-ttu-id="3a08f-175">hello 계정 이름, 테이블 이름 및 **PartitionKey** 함께 hello 테이블 서비스는 hello 엔터티를 저장 하는 hello 저장소 서비스 내에서 파티션 hello를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-175">hello account name, table name and **PartitionKey** together identify hello partition within hello storage service where hello table service stores hello entity.</span></span> <span data-ttu-id="3a08f-176">주소 지정 체계 엔터티에 대 한 hello의 일부분인, 뿐만 아니라 파티션 트랜잭션에 대 한 범위를 정의 (참조 [엔터티 그룹 트랜잭션을](#entity-group-transactions) 아래), 및 hello 테이블 서비스 확장 하는 방법의 양식 hello 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-176">As well as being part of hello addressing scheme for entities, partitions define a scope for transactions (see [Entity Group Transactions](#entity-group-transactions) below), and form hello basis of how hello table service scales.</span></span> <span data-ttu-id="3a08f-177">파티션에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](../storage/common/storage-scalability-targets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a08f-177">For more information on partitions see [Azure Storage Scalability and Performance Targets](../storage/common/storage-scalability-targets.md).</span></span>  

<span data-ttu-id="3a08f-178">테이블 서비스 hello에서 개별 노드 하나 서비스 또는 파티션을 완료 및 동적으로 부하 분산 하 여 서비스 눈금 hello 노드 간에 파티션이 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-178">In hello Table service, an individual node services one or more complete partitions and hello service scales by dynamically load-balancing partitions across nodes.</span></span> <span data-ttu-id="3a08f-179">Hello 테이블 서비스의 수는 노드가 부하 상태에서 경우 *분할* hello 파티션 범위에 해당 노드를 서로 다른 노드에로 서비스; hello 서비스 수 트래픽 subsides 때 *병합* hello 파티션을에서 범위 단일 노드로 다시 quiet 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-179">If a node is under load, hello table service can *split* hello range of partitions serviced by that node onto different nodes; when traffic subsides, hello service can *merge* hello partition ranges from quiet nodes back onto a single node.</span></span>  

<span data-ttu-id="3a08f-180">Hello에 대 한 자세한 내용은 내부 hello 테이블 서비스를 하 고 세부적인 특히 hello 서비스에서 파티션을 관리 하는 방법 참조 hello 용지 [Microsoft Azure 저장소: A 항상 사용 가능한 클라우드 저장소 서비스 강력한 일관성](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).</span><span class="sxs-lookup"><span data-stu-id="3a08f-180">For more information about hello internal details of hello Table service, and in particular how hello service manages partitions, see hello paper [Microsoft Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).</span></span>  

### <a name="entity-group-transactions"></a><span data-ttu-id="3a08f-181">EGT(엔터티 그룹 트랜잭션)</span><span class="sxs-lookup"><span data-stu-id="3a08f-181">Entity Group Transactions</span></span>
<span data-ttu-id="3a08f-182">Hello 테이블 서비스에서에서 엔터티 그룹 트랜잭션 (EGTs)은 여러 엔터티 간에 자동 업데이트를 수행 하기 위한 hello만 기본 제공 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-182">In hello Table service, Entity Group Transactions (EGTs) are hello only built-in mechanism for performing atomic updates across multiple entities.</span></span> <span data-ttu-id="3a08f-183">EGTs 참조 tooas 사항도 *트랜잭션 일괄 처리* 일부 설명서에서는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-183">EGTs are also referred tooas *batch transactions* in some documentation.</span></span> <span data-ttu-id="3a08f-184">EGTs hello에 저장 된 엔터티 에서만 작동할 수 있습니다 동일한 파티션 (공유 hello 지정된 된 테이블에서 동일한 파티션 키) 이므로 해당 엔터티가 서로 hello에 tooensure 필요한 여러 엔터티에서 원자성 트랜잭션 동작 언제 든 지 동일한 파티션에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-184">EGTs can only operate on entities stored in hello same partition (share hello same partition key in a given table), so anytime you need atomic transactional behavior across multiple entities you need tooensure that those entities are in hello same partition.</span></span> <span data-ttu-id="3a08f-185">종종 hello 동일 테이블 (및 파티션)의 여러 엔터티 형식을 유지 하 고 서로 다른 엔터티 형식에 대 한 여러 테이블을 사용 하지에 대 한 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-185">This is often a reason for keeping multiple entity types in hello same table (and partition) and not using multiple tables for different entity types.</span></span> <span data-ttu-id="3a08f-186">단일 EGT는 최대 100개의 엔터티에서 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-186">A single EGT can operate on at most 100 entities.</span></span>  <span data-ttu-id="3a08f-187">처리 중요 tooensure에 대 한 여러 개의 동시 EGTs 제출 하는 경우 이러한 EGTs 그렇지 않으면 처리 지연 될 수 있습니다 EGTs 걸쳐 공통 되는 엔터티에 대해 작동 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="3a08f-187">If you submit multiple concurrent EGTs for processing it is important tooensure  those EGTs do not operate on entities that are common across EGTs as otherwise processing can be delayed.</span></span>

<span data-ttu-id="3a08f-188">EGTs tooevaluate 디자인에 대 한 잠재적인 영향에 대해서도 소개: 많은 파티션을 사용 하 여 늘어납니다 hello 확장성 응용 프로그램을 Azure의 부하 분산 요청 노드에서 기회가 늘어나기 때문이 hello로 제한 될 수 있습니다 응용 프로그램 tooperform 원자성 트랜잭션의 기능 및 데이터에 대 한 강력한 일관성을 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-188">EGTs also introduce a potential trade-off for you tooevaluate in your design: using more partitions will increase hello scalability of your application because Azure has more opportunities for load balancing requests across nodes, but this might limit hello ability of your application tooperform atomic transactions and maintain strong consistency for your data.</span></span> <span data-ttu-id="3a08f-189">또한 hello 트랜잭션 처리량을 단일 노드에 대해 예상할 수를 제한할 수 있는 파티션의 hello 수준에서 특정 확장성 목표 발생 되어: Azure 저장소 계정과 hello 테이블에 대 한 hello 확장성 목표에 대 한 자세한 내용은 서비스 참조, [Azure 저장소 확장성 및 성능 목표](../storage/common/storage-scalability-targets.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-189">Furthermore, there are specific scalability targets at hello level of a partition that might limit hello throughput of transactions you can expect for a single node: for more information about hello scalability targets for Azure storage accounts and hello table service, see [Azure Storage Scalability and Performance Targets](../storage/common/storage-scalability-targets.md).</span></span> <span data-ttu-id="3a08f-190">이 가이드의 뒷부분에 나오는 섹션에 설명 다양 한 디자인 전략 데 도움이 되는이 샘플과 같이 장단점을 관리 하 고 최상의 방법을 toochoose 파티션 키 기반 클라이언트 응용 프로그램의 hello 특정 요구 사항에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-190">Later sections of this guide discuss various design strategies that help you manage trade-offs such as this one, and discuss how best toochoose your partition key based on hello specific requirements of your client application.</span></span>  

### <a name="capacity-considerations"></a><span data-ttu-id="3a08f-191">용량 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3a08f-191">Capacity considerations</span></span>
<span data-ttu-id="3a08f-192">hello 다음 표에서 일부의 hello 키 값 toobe 테이블 서비스 솔루션을 디자인 하는 경우 인식 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-192">hello following table includes some of hello key values toobe aware of when you are designing a Table service solution:</span></span>  

| <span data-ttu-id="3a08f-193">Azure 저장소 계정의 총 용량</span><span class="sxs-lookup"><span data-stu-id="3a08f-193">Total capacity of an Azure storage account</span></span> | <span data-ttu-id="3a08f-194">500TB</span><span class="sxs-lookup"><span data-stu-id="3a08f-194">500 TB</span></span> |
| --- | --- |
| <span data-ttu-id="3a08f-195">Azure 저장소 계정에서 테이블의 수</span><span class="sxs-lookup"><span data-stu-id="3a08f-195">Number of tables in an Azure storage account</span></span> |<span data-ttu-id="3a08f-196">Hello 저장소 계정의 용량 hello로만 제한</span><span class="sxs-lookup"><span data-stu-id="3a08f-196">Limited only by hello capacity of hello storage account</span></span> |
| <span data-ttu-id="3a08f-197">테이블에 있는 파티션 수</span><span class="sxs-lookup"><span data-stu-id="3a08f-197">Number of partitions in a table</span></span> |<span data-ttu-id="3a08f-198">Hello 저장소 계정의 용량 hello로만 제한</span><span class="sxs-lookup"><span data-stu-id="3a08f-198">Limited only by hello capacity of hello storage account</span></span> |
| <span data-ttu-id="3a08f-199">파티션의 엔터티 수</span><span class="sxs-lookup"><span data-stu-id="3a08f-199">Number of entities in a partition</span></span> |<span data-ttu-id="3a08f-200">Hello 저장소 계정의 용량 hello로만 제한</span><span class="sxs-lookup"><span data-stu-id="3a08f-200">Limited only by hello capacity of hello storage account</span></span> |
| <span data-ttu-id="3a08f-201">개별 엔터티의 크기</span><span class="sxs-lookup"><span data-stu-id="3a08f-201">Size of an individual entity</span></span> |<span data-ttu-id="3a08f-202">최대 255 개의 속성을 최대 too1 MB (hello를 포함 하 여 **PartitionKey**, **RowKey**, 및 **타임 스탬프**)</span><span class="sxs-lookup"><span data-stu-id="3a08f-202">Up too1 MB with a maximum of 255 properties (including hello **PartitionKey**, **RowKey**, and **Timestamp**)</span></span> |
| <span data-ttu-id="3a08f-203">Hello 크기인 **PartitionKey**</span><span class="sxs-lookup"><span data-stu-id="3a08f-203">Size of hello **PartitionKey**</span></span> |<span data-ttu-id="3a08f-204">크기가 too1 KB 문자열</span><span class="sxs-lookup"><span data-stu-id="3a08f-204">A string up too1 KB in size</span></span> |
| <span data-ttu-id="3a08f-205">Hello 크기인 **RowKey**</span><span class="sxs-lookup"><span data-stu-id="3a08f-205">Size of hello **RowKey**</span></span> |<span data-ttu-id="3a08f-206">크기가 too1 KB 문자열</span><span class="sxs-lookup"><span data-stu-id="3a08f-206">A string up too1 KB in size</span></span> |
| <span data-ttu-id="3a08f-207">엔터티 그룹 트랜잭션의 크기</span><span class="sxs-lookup"><span data-stu-id="3a08f-207">Size of an Entity Group Transaction</span></span> |<span data-ttu-id="3a08f-208">트랜잭션이 최대 100 개의 엔터티가 포함 될 수 있습니다 및 hello 페이로드 크기는 4MB 미만 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-208">A transaction can include at most 100 entities and hello payload must be less than 4 MB in size.</span></span> <span data-ttu-id="3a08f-209">EGT는 한 번에 하나의 엔터티만 업데이트할 수 있음</span><span class="sxs-lookup"><span data-stu-id="3a08f-209">An EGT can only update an entity once.</span></span> |

<span data-ttu-id="3a08f-210">자세한 내용은 참조 [테이블 서비스 데이터 모델 이해 hello](http://msdn.microsoft.com/library/azure/dd179338.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-210">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>  

### <a name="cost-considerations"></a><span data-ttu-id="3a08f-211">비용 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3a08f-211">Cost considerations</span></span>
<span data-ttu-id="3a08f-212">테이블 저장소 상대적으로 비용이 많이 들지 않습니다. 하지만 hello 테이블 서비스를 사용 하는 솔루션의 평가판의 일부로 트랜잭션의 두 용량 사용량 및 hello 수량에 대 한 예상 비용을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-212">Table storage is relatively inexpensive, but you should include cost estimates for both capacity usage and hello quantity of transactions as part of your evaluation of any solution that uses hello Table service.</span></span> <span data-ttu-id="3a08f-213">그러나 순서 tooimprove hello에 정규화 되지 않은 또는 중복 데이터를 저장 하는 많은 시나리오에서 성능이 나 확장성을 솔루션의는 올바른 방법은 tootake.</span><span class="sxs-lookup"><span data-stu-id="3a08f-213">However, in many scenarios storing denormalized or duplicate data in order tooimprove hello performance or scalability of your solution is a valid approach tootake.</span></span> <span data-ttu-id="3a08f-214">가격 책정에 대한 자세한 내용은 [Azure 저장소 가격 책정](https://azure.microsoft.com/pricing/details/storage/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a08f-214">For more information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>  

## <a name="guidelines-for-table-design"></a><span data-ttu-id="3a08f-215">테이블 디자인 지침</span><span class="sxs-lookup"><span data-stu-id="3a08f-215">Guidelines for table design</span></span>
<span data-ttu-id="3a08f-216">이러한 목록 요약 테이블을 디자인할 때 염두에서 유지 해야 하는 hello 핵심 지침 몇 가지 하 고이 가이드 뒷부분에서 자세히 모두에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-216">These lists summarize some of hello key guidelines you should keep in mind when you are designing your tables, and this guide will address them all in more detail later in.</span></span> <span data-ttu-id="3a08f-217">이러한 지침은 hello 지침을 수행 해야 하는 일반적으로 관계형 데이터베이스 디자인에 대 한 매우 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-217">These guidelines are very different from hello guidelines you would typically follow for relational database design.</span></span>  

<span data-ttu-id="3a08f-218">사용자 테이블 서비스 솔루션 toobe 디자인 *읽을* 효율적인:</span><span class="sxs-lookup"><span data-stu-id="3a08f-218">Designing your Table service solution toobe *read* efficient:</span></span>

* <span data-ttu-id="3a08f-219">***읽기 작업이 많은 응용 프로그램의 쿼리를 위해 디자인합니다.***</span><span class="sxs-lookup"><span data-stu-id="3a08f-219">***Design for querying in read-heavy applications.***</span></span> <span data-ttu-id="3a08f-220">실행할 hello 쿼리 (특히 hello 대기 시간이 중요 한 것)에 대해 생각 하는 테이블을 디자인 하는 경우 먼저 엔터티를 업데이트할 것 방법에 대 한 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-220">When you are designing your tables, think about hello queries (especially hello latency sensitive ones) that you will execute before you think about how you will update your entities.</span></span> <span data-ttu-id="3a08f-221">이는 일반적으로 솔루션의 효율성 및 성능에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-221">This typically results in an efficient and performant solution.</span></span>  
* <span data-ttu-id="3a08f-222">***쿼리에서 PartitionKey와 RowKey 둘 다 지정합니다.***</span><span class="sxs-lookup"><span data-stu-id="3a08f-222">***Specify both PartitionKey and RowKey in your queries.***</span></span> <span data-ttu-id="3a08f-223">*쿼리를 가리키고* hello 가장 효율적인 테이블 서비스 쿼리는 같은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-223">*Point queries* such as these are hello most efficient table service queries.</span></span>  
* <span data-ttu-id="3a08f-224">***엔터티의 중복 복사본을 저장하는 것이 좋습니다.***</span><span class="sxs-lookup"><span data-stu-id="3a08f-224">***Consider storing duplicate copies of entities.***</span></span> <span data-ttu-id="3a08f-225">테이블 저장소는 비용이 적게 드는 것이 좋습니다 동일한 엔터티를 여러 번 (다른 키를 가진) hello 저장 tooenable 더 효율적인 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-225">Table storage is cheap so consider storing hello same entity multiple times (with different keys) tooenable more efficient queries.</span></span>  
* <span data-ttu-id="3a08f-226">***데이터를 비정규화하는 것이 좋습니다.***</span><span class="sxs-lookup"><span data-stu-id="3a08f-226">***Consider denormalizing your data.***</span></span> <span data-ttu-id="3a08f-227">테이블 저장소는 저렴하기 때문에 데이터를 비정규화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-227">Table storage is cheap so consider denormalizing your data.</span></span> <span data-ttu-id="3a08f-228">예를 들어 데이터 집계에 대 한 쿼리 하기만 tooaccess 단일 엔터티 있도록 요약 엔터티를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-228">For example, store summary entities so that queries for aggregate data only need tooaccess a single entity.</span></span>  
* <span data-ttu-id="3a08f-229">***복합 키 값을 사용하는 것이 좋습니다.***</span><span class="sxs-lookup"><span data-stu-id="3a08f-229">***Use compound key values.***</span></span> <span data-ttu-id="3a08f-230">hello 있는 키만이 **PartitionKey** 및 **RowKey**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-230">hello only keys you have are **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="3a08f-231">예를 들어 tooenable 대체 키가 지정 된 액세스 경로 tooentities 복합 키 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-231">For example, use compound key values tooenable alternate keyed access paths tooentities.</span></span>  
* <span data-ttu-id="3a08f-232">***쿼리 프로젝션을 사용합니다.***</span><span class="sxs-lookup"><span data-stu-id="3a08f-232">***Use query projection.***</span></span> <span data-ttu-id="3a08f-233">Hello 방금 hello 필요한 필드를 선택 하는 쿼리를 사용 하 여 hello 네트워크를 통해 전송 하는 데이터 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-233">You can reduce hello amount of data that you transfer over hello network by using queries that select just hello fields you need.</span></span>  

<span data-ttu-id="3a08f-234">사용자 테이블 서비스 솔루션 toobe 디자인 *쓰기* 효율적인:</span><span class="sxs-lookup"><span data-stu-id="3a08f-234">Designing your Table service solution toobe *write* efficient:</span></span>  

* <span data-ttu-id="3a08f-235">***핫 파티션을 만들지 마세요.***</span><span class="sxs-lookup"><span data-stu-id="3a08f-235">***Do not create hot partitions.***</span></span> <span data-ttu-id="3a08f-236">시간의 언제 든 지 여러 파티션에서 키 toospread 수 있도록 하는 사용자의 요청을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-236">Choose keys that enable you toospread your requests across multiple partitions at any point of time.</span></span>  
* <span data-ttu-id="3a08f-237">***트래픽 급증을 방지합니다.***</span><span class="sxs-lookup"><span data-stu-id="3a08f-237">***Avoid spikes in traffic.***</span></span> <span data-ttu-id="3a08f-238">Hello 트래픽을 적절 한 기간을 통해 매끄럽게 한 트래픽 급증을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-238">Smooth hello traffic over a reasonable period of time and avoid spikes in traffic.</span></span>
* <span data-ttu-id="3a08f-239">***각 엔터티 유형에 대한 별도의 테이블을 만들 필요가 없습니다.***</span><span class="sxs-lookup"><span data-stu-id="3a08f-239">***Don't necessarily create a separate table for each type of entity.***</span></span> <span data-ttu-id="3a08f-240">엔터티 형식 간에 원자성 트랜잭션을 요구 하면 저장할 수 있습니다 이러한 여러 엔터티 형식을 hello 파티션에 동일한 hello 같은 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-240">When you require atomic transactions across entity types, you can store these multiple entity types in hello same partition in hello same table.</span></span>
* <span data-ttu-id="3a08f-241">***Hello 최대 처리량을 조정 해야 것이 좋습니다.***</span><span class="sxs-lookup"><span data-stu-id="3a08f-241">***Consider hello maximum throughput you must achieve.***</span></span> <span data-ttu-id="3a08f-242">Hello 테이블 서비스에 대 한 확장성 목표 hello 알고 있어야 하며 디자인에서 되지 않도록 하면 tooexceed 확인 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-242">You must be aware of hello scalability targets for hello Table service and ensure that your design will not cause you tooexceed them.</span></span>  

<span data-ttu-id="3a08f-243">이 가이드에서는 이 모든 원칙을 실습해 볼 수 있는 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-243">As you read this guide, you will see examples that put all of these principles into practice.</span></span>  

## <a name="design-for-querying"></a><span data-ttu-id="3a08f-244">쿼리를 위한 디자인</span><span class="sxs-lookup"><span data-stu-id="3a08f-244">Design for querying</span></span>
<span data-ttu-id="3a08f-245">많이 사용, 쓰기 중심 또는 두 hello 혼합 하 여 테이블 서비스 솔루션을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-245">Table service solutions may be read intensive, write intensive, or a mix of hello two.</span></span> <span data-ttu-id="3a08f-246">이 섹션으로 읽기 작업을 효율적으로 하 여 테이블 서비스 toosupport 디자인할 때 고려에서 사항 toobear hello 집중 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-246">This section focuses on hello things toobear in mind when you are designing your Table service toosupport read operations efficiently.</span></span> <span data-ttu-id="3a08f-247">일반적으로 읽기 작업을 효율적으로 지원하는 디자인은 쓰기 작업에도 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-247">Typically, a design that supports read operations efficiently is also efficient for write operations.</span></span> <span data-ttu-id="3a08f-248">그러나 가지 추가 고려 사항 toobear 염두에서 디자인 toosupport 쓰기 작업을 hello 다음 섹션에서 설명 하는 경우 [데이터 수정 위한 디자인](#design-for-data-modification)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-248">However, there are additional considerations toobear in mind when designing toosupport write operations, discussed in hello next section, [Design for data modification](#design-for-data-modification).</span></span>

<span data-ttu-id="3a08f-249">테이블 서비스 솔루션 tooenable 프로그램을 디자인 하기 위한 좋은 출발점 tooread 데이터 효율적으로 tooask "하는 쿼리는 hello 테이블 서비스에서에서 필요한 응용 프로그램 요구 tooexecute tooretrieve hello 데이터가?"</span><span class="sxs-lookup"><span data-stu-id="3a08f-249">A good starting point for designing your Table service solution tooenable you tooread data efficiently is tooask "What queries will my application need tooexecute tooretrieve hello data it needs from hello Table service?"</span></span>  

> [!NOTE]
> <span data-ttu-id="3a08f-250">테이블 서비스 hello로는 것이 중요 tooget hello 디자인 올바른 들겠지만 많은 시간과 비용이 많이 드는 toochange 있기 때문에 나중에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-250">With hello Table service, it's important tooget hello design correct up front because it's difficult and expensive toochange it later.</span></span> <span data-ttu-id="3a08f-251">예를 들어 tooan 기존 데이터베이스 인덱스를 추가 하 여 가능한 tooaddress 성능 문제는 종종 관계형 데이터베이스에서:이 hello 테이블 서비스를 사용 하는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-251">For example, in a relational database it's often possible tooaddress performance issues simply by adding indexes tooan existing database: this is not an option with hello Table service.</span></span>  
> 
> 

<span data-ttu-id="3a08f-252">이 섹션을 쿼리 하기 위한 테이블을 디자인할 때 고려해 야 할 주요 문제를 hello에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-252">This section focuses on hello key issues you must address when you design your tables for querying.</span></span> <span data-ttu-id="3a08f-253">이 섹션에서 다루는 hello 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-253">hello topics covered in this section include:</span></span>

* [<span data-ttu-id="3a08f-254">PartitionKey 및 RowKey 선택이 쿼리 성능에 미치는 영향</span><span class="sxs-lookup"><span data-stu-id="3a08f-254">How your choice of PartitionKey and RowKey impacts query performance</span></span>](#how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance)
* [<span data-ttu-id="3a08f-255">적절한 PartitionKey 선택</span><span class="sxs-lookup"><span data-stu-id="3a08f-255">Choosing an appropriate PartitionKey</span></span>](#choosing-an-appropriate-partitionkey)
* [<span data-ttu-id="3a08f-256">Hello 테이블 서비스에 대 한 쿼리 최적화</span><span class="sxs-lookup"><span data-stu-id="3a08f-256">Optimizing queries for hello Table service</span></span>](#optimizing-queries-for-the-table-service)
* [<span data-ttu-id="3a08f-257">Hello 테이블 서비스의에서 데이터 정렬</span><span class="sxs-lookup"><span data-stu-id="3a08f-257">Sorting data in hello Table service</span></span>](#sorting-data-in-the-table-service)

### <a name="how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance"></a><span data-ttu-id="3a08f-258">PartitionKey 및 RowKey 선택이 쿼리 성능에 미치는 영향</span><span class="sxs-lookup"><span data-stu-id="3a08f-258">How your choice of PartitionKey and RowKey impacts query performance</span></span>
<span data-ttu-id="3a08f-259">hello 다음 예제에서는 가정 hello 테이블 서비스에서 다음 구조 hello로 employee 엔터티를 저장 하는 (대부분의 hello 예제 생략 hello **타임 스탬프** 명확성에 대 한 속성):</span><span class="sxs-lookup"><span data-stu-id="3a08f-259">hello following examples assume hello table service is storing employee entities with hello following structure (most of hello examples omit hello **Timestamp** property for clarity):</span></span>  

| <span data-ttu-id="3a08f-260">*열 이름*</span><span class="sxs-lookup"><span data-stu-id="3a08f-260">*Column name*</span></span> | <span data-ttu-id="3a08f-261">*데이터 형식*</span><span class="sxs-lookup"><span data-stu-id="3a08f-261">*Data type*</span></span> |
| --- | --- |
| <span data-ttu-id="3a08f-262">**PartitionKey** (부서 이름)</span><span class="sxs-lookup"><span data-stu-id="3a08f-262">**PartitionKey** (Department Name)</span></span> |<span data-ttu-id="3a08f-263">String</span><span class="sxs-lookup"><span data-stu-id="3a08f-263">String</span></span> |
| <span data-ttu-id="3a08f-264">**RowKey** (직원 Id)</span><span class="sxs-lookup"><span data-stu-id="3a08f-264">**RowKey** (Employee Id)</span></span> |<span data-ttu-id="3a08f-265">String</span><span class="sxs-lookup"><span data-stu-id="3a08f-265">String</span></span> |
| <span data-ttu-id="3a08f-266">**FirstName**</span><span class="sxs-lookup"><span data-stu-id="3a08f-266">**FirstName**</span></span> |<span data-ttu-id="3a08f-267">String</span><span class="sxs-lookup"><span data-stu-id="3a08f-267">String</span></span> |
| <span data-ttu-id="3a08f-268">**LastName**</span><span class="sxs-lookup"><span data-stu-id="3a08f-268">**LastName**</span></span> |<span data-ttu-id="3a08f-269">String</span><span class="sxs-lookup"><span data-stu-id="3a08f-269">String</span></span> |
| <span data-ttu-id="3a08f-270">**Age**</span><span class="sxs-lookup"><span data-stu-id="3a08f-270">**Age**</span></span> |<span data-ttu-id="3a08f-271">Integer</span><span class="sxs-lookup"><span data-stu-id="3a08f-271">Integer</span></span> |
| <span data-ttu-id="3a08f-272">**EmailAddress**</span><span class="sxs-lookup"><span data-stu-id="3a08f-272">**EmailAddress**</span></span> |<span data-ttu-id="3a08f-273">문자열</span><span class="sxs-lookup"><span data-stu-id="3a08f-273">String</span></span> |

<span data-ttu-id="3a08f-274">이전 섹션 hello [Azure 테이블 서비스 개요](#overview) hello 주요 기능 hello Azure 테이블 서비스의 쿼리에 대 한 디자인에 직접적인 영향을 주지 않은의 일부에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-274">hello earlier section [Azure Table service overview](#overview) describes some of hello key features of hello Azure Table service that have a direct influence on designing for query.</span></span> <span data-ttu-id="3a08f-275">이렇게 하면 테이블 서비스 쿼리를 디자인 하기 위한 일반적인 지침을 따르는 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-275">These result in hello following general guidelines for designing Table service queries.</span></span> <span data-ttu-id="3a08f-276">테이블 서비스 REST API 참조 항목에 대 한 hello에서에서 hello 필터 구문 아래 hello 예제에서 사용 되는 [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-276">Note that hello filter syntax used in hello examples below is from hello Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

* <span data-ttu-id="3a08f-277">A ***지점 쿼리*** hello 가장 효율적인 조회 toouse 이며 toobe 대용량 조회 또는 가장 짧은 대기 시간을 요구 하는 조회에 사용 되는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-277">A ***Point Query*** is hello most efficient lookup toouse and is recommended toobe used for high-volume lookups or lookups requiring lowest latency.</span></span> <span data-ttu-id="3a08f-278">이러한 쿼리 צ ְ ײ hello 인덱스 toolocate 개별 엔터티에 매우 효율적으로 hello 둘 다 지정 하 여 **PartitionKey** 및 **RowKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-278">Such a query can use hello indexes toolocate an individual entity very efficiently by specifying both hello **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="3a08f-279">예: $filter=(PartitionKey eq 'Sales') and (RowKey eq '2')</span><span class="sxs-lookup"><span data-stu-id="3a08f-279">For example: $filter=(PartitionKey eq 'Sales') and (RowKey eq '2')</span></span>  
* <span data-ttu-id="3a08f-280">가 두 번째로 가장는 ***범위 쿼리*** hello를 사용 하 여 **PartitionKey** 및 범위에 대 한 필터 **RowKey** tooreturn 둘 이상의 엔터티 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-280">Second best is a ***Range Query*** that uses hello **PartitionKey** and filters on a range of **RowKey** values tooreturn more than one entity.</span></span> <span data-ttu-id="3a08f-281">hello **PartitionKey** 값을 특정 파티션 및 hello 식별 **RowKey** 해당 파티션의 hello 엔터티 하위 집합을 식별 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-281">hello **PartitionKey** value identifies a specific partition, and hello **RowKey** values identify a subset of hello entities in that partition.</span></span> <span data-ttu-id="3a08f-282">예: $filter=PartitionKey eq 'Sales' and RowKey ge 'S' and RowKey lt 'T'</span><span class="sxs-lookup"><span data-stu-id="3a08f-282">For example: $filter=PartitionKey eq 'Sales' and RowKey ge 'S' and RowKey lt 'T'</span></span>  
* <span data-ttu-id="3a08f-283">세 번째 최고는 ***파티션 검색*** hello를 사용 하 여 **PartitionKey** 있고 다른 키가 아닌 속성에 대 한 필터는 둘 이상의 엔터티를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-283">Third best is a ***Partition Scan*** that uses hello **PartitionKey** and filters on another non-key property and that may return more than one entity.</span></span> <span data-ttu-id="3a08f-284">hello **PartitionKey** hello 속성 값을 해당 파티션의 hello 엔터티 하위 집합에 대 한 select 및 특정 파티션을 식별 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-284">hello **PartitionKey** value identifies a specific partition, and hello property values select for a subset of hello entities in that partition.</span></span> <span data-ttu-id="3a08f-285">예: $filter=PartitionKey eq 'Sales' and LastName eq 'Smith'</span><span class="sxs-lookup"><span data-stu-id="3a08f-285">For example: $filter=PartitionKey eq 'Sales' and LastName eq 'Smith'</span></span>  
* <span data-ttu-id="3a08f-286">A ***Table Scan*** hello는 **PartitionKey** 검색의 모든 테이블에 일치 하는 모든 항목에 대 한 다시 구성 하는 hello 파티션을 하므로 효율적이 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-286">A ***Table Scan*** does not include hello **PartitionKey** and is very inefficient because it searches all of hello partitions that make up your table in turn for any matching entities.</span></span> <span data-ttu-id="3a08f-287">필터 hello를 사용 하는 여부에 관계 없이 테이블 검색이 수행 **RowKey**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-287">It will perform a table scan regardless of whether or not your filter uses hello **RowKey**.</span></span> <span data-ttu-id="3a08f-288">예: $filter=LastName eq 'Jones'</span><span class="sxs-lookup"><span data-stu-id="3a08f-288">For example: $filter=LastName eq 'Jones'</span></span>  
* <span data-ttu-id="3a08f-289">여러 엔터티를 반환하는 쿼리는 **PartitionKey**와 **RowKey** 순으로 정렬된 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-289">Queries that return multiple entities return them sorted in **PartitionKey** and **RowKey** order.</span></span> <span data-ttu-id="3a08f-290">tooavoid 앞선 hello 엔터티 hello 클라이언트에서 선택 된 **RowKey** hello 가장 일반적인 정렬 순서를 정의 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-290">tooavoid resorting hello entities in hello client, choose a **RowKey** that defines hello most common sort order.</span></span>  

<span data-ttu-id="3a08f-291">사용는 "**또는**" 필터에 따라 toospecify **RowKey** 파티션 검색의 결과 값을 범위 쿼리로 처리 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-291">Note that using an "**or**" toospecify a filter based on **RowKey** values results in a partition scan and is not treated as a range query.</span></span> <span data-ttu-id="3a08f-292">따라서 다음과 같은 필터를 사용하는 쿼리는 피해야 합니다. $filter=PartitionKey eq 'Sales' and (RowKey eq '121' or RowKey eq '322')</span><span class="sxs-lookup"><span data-stu-id="3a08f-292">Therefore, you should avoid queries that use filters such as: $filter=PartitionKey eq 'Sales' and (RowKey eq '121' or RowKey eq '322')</span></span>  

<span data-ttu-id="3a08f-293">Hello 저장소 클라이언트 라이브러리 tooexecute 효율적인 쿼리를 사용 하 여 클라이언트 쪽 코드 예제 참조.</span><span class="sxs-lookup"><span data-stu-id="3a08f-293">For examples of client-side code that use hello Storage Client Library tooexecute efficient queries, see:</span></span>  

* [<span data-ttu-id="3a08f-294">Hello 저장소 클라이언트 라이브러리를 사용 하 여 지점 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-294">Executing a point query using hello Storage Client Library</span></span>](#executing-a-point-query-using-the-storage-client-library)
* [<span data-ttu-id="3a08f-295">LINQ를 사용하여 여러 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="3a08f-295">Retrieving multiple entities using LINQ</span></span>](#retrieving-multiple-entities-using-linq)
* [<span data-ttu-id="3a08f-296">서버 쪽 프로젝션</span><span class="sxs-lookup"><span data-stu-id="3a08f-296">Server-side projection</span></span>](#server-side-projection)  

<span data-ttu-id="3a08f-297">여러 엔터티를 처리할 수 있는 클라이언트 쪽 코드의 예에 대 한 형식에에서 저장 된 hello 동일 테이블 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3a08f-297">For examples of client-side code that can handle multiple entity types stored in hello same table, see:</span></span>  

* [<span data-ttu-id="3a08f-298">유형이 다른 엔터티 유형 작업</span><span class="sxs-lookup"><span data-stu-id="3a08f-298">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="choosing-an-appropriate-partitionkey"></a><span data-ttu-id="3a08f-299">적절한 PartitionKey 선택</span><span class="sxs-lookup"><span data-stu-id="3a08f-299">Choosing an appropriate PartitionKey</span></span>
<span data-ttu-id="3a08f-300">사용자가 선택한 **PartitionKey** 간의 균형 EGTs (tooensure 일관성) hello 필요 tooenables hello 사용 요구 사항이 toodistribute hello에 대 한 엔터티를 여러 파티션에 (tooensure 확장성이 뛰어난 솔루션).</span><span class="sxs-lookup"><span data-stu-id="3a08f-300">Your choice of **PartitionKey** should balance hello need tooenables hello use of EGTs (tooensure consistency) against hello requirement toodistribute your entities across multiple partitions (tooensure a scalable solution).</span></span>  

<span data-ttu-id="3a08f-301">최대에서는 단일 파티션의 모든 엔터티를 저장할 수 있지만이 솔루션의 hello 확장성이 제한 될 수 있습니다 이며 hello 테이블 서비스 요청 수 tooload 분산할 수 없도록 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-301">At one extreme, you could store all your entities in a single partition, but this may limit hello scalability of your solution and would prevent hello table service from being able tooload-balance requests.</span></span> <span data-ttu-id="3a08f-302">다른 한편으로는 hello에 확장성이 높은 것 및 hello 테이블 서비스 tooload 잔액 요청을 할 수 있게 하지만으로 인해 엔터티 그룹 트랜잭션을 사용 하 여 파티션당 하나의 엔터티가 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-302">At hello other extreme, you could store one entity per partition, which would be highly scalable and which enables hello table service tooload-balance requests, but which would prevent you from using entity group transactions.</span></span>  

<span data-ttu-id="3a08f-303">이상적 **PartitionKey** toouse 효율적인 쿼리를 수 있는 되며 충분 한 파티션을 tooensure 솔루션은 확장 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-303">An ideal **PartitionKey** is one that enables you toouse efficient queries and that has sufficient partitions tooensure your solution is scalable.</span></span> <span data-ttu-id="3a08f-304">일반적으로 엔터티에는 충분한 파티션으로 엔터티를 분산하는 적절한 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-304">Typically, you will find that your entities will have a suitable property that distributes your entities across sufficient partitions.</span></span>

> [!NOTE]
> <span data-ttu-id="3a08f-305">예를 들어 사용자 또는 직원에 대한 정보를 저장하는 시스템에서는 UserID가 적절한 PartitionKey일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-305">For example, in a system that stores information about users or employees, UserID may be a good PartitionKey.</span></span> <span data-ttu-id="3a08f-306">Hello 파티션 키로 지정 된 사용자 Id를 사용 하는 몇 개의 엔터티를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-306">You may have several entities that use a given UserID as hello partition key.</span></span> <span data-ttu-id="3a08f-307">사용자에 대한 데이터를 저장하는 각 엔터티는 단일 파티션으로 그룹화되므로 이러한 엔터티는 높은 확장성을 유지하면서 엔터티 그룹 트랜잭션을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-307">Each entity that stores data about a user is grouped into a single partition, and so these entities are accessible via entity group transactions, while still being highly scalable.</span></span>
> 
> 

<span data-ttu-id="3a08f-308">선택한에서 추가 고려 사항 사항이 **PartitionKey** 삽입, 업데이트 및 엔터티를 삭제 합니다 toohow 관련 된: hello 섹션을 참조 [데이터 수정 위한 디자인](#design-for-data-modification) 아래 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-308">There are additional considerations in your choice of **PartitionKey** that relate toohow you will insert, update, and delete entities: see hello section [Design for data modification](#design-for-data-modification) below.</span></span>  

### <a name="optimizing-queries-for-hello-table-service"></a><span data-ttu-id="3a08f-309">Hello 테이블 서비스에 대 한 쿼리 최적화</span><span class="sxs-lookup"><span data-stu-id="3a08f-309">Optimizing queries for hello Table service</span></span>
<span data-ttu-id="3a08f-310">테이블 서비스 hello hello를 사용 하 여 엔터티를 자동으로 인덱싱됩니다 **PartitionKey** 및 **RowKey** 단일 클러스터형된 인덱스의 값에 따라서 이유 지점 쿼리가 가장 효율적인 toouse를 hello는 hello .</span><span class="sxs-lookup"><span data-stu-id="3a08f-310">hello Table service automatically indexes your entities using hello **PartitionKey** and **RowKey** values in a single clustered index, hence hello reason that point queries are hello most efficient toouse.</span></span> <span data-ttu-id="3a08f-311">그러나 여러 가지 hello hello에서 클러스터형된 인덱스에는 다른 인덱스가 없는 **PartitionKey** 및 **RowKey**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-311">However, there are no indexes other than that on hello clustered index on hello **PartitionKey** and **RowKey**.</span></span>

<span data-ttu-id="3a08f-312">대부분의 디자인 여러 조건을 기반으로 하는 엔터티의 tooenable 조회 요구 사항을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-312">Many designs must meet requirements tooenable lookup of entities based on multiple criteria.</span></span> <span data-ttu-id="3a08f-313">예를 들어 전자 메일, 직원 ID 또는 성을 기반으로 직원 엔터티를 찾을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-313">For example, locating employee entities based on email, employee id, or last name.</span></span> <span data-ttu-id="3a08f-314">패턴 hello 섹션의 다음 hello [테이블 디자인 패턴](#table-design-patterns) 이러한 유형의 요구 사항 해결 하 고 hello 테이블 서비스 보조 인덱스를 제공 하지 않습니다 hello 팩트 해결 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-314">hello following patterns in hello section [Table Design Patterns](#table-design-patterns) address these types of requirement and describe ways of working around hello fact that hello Table service does not provide secondary indexes:</span></span>  

* <span data-ttu-id="3a08f-315">[파티션 내 보조 인덱스 패턴](#intra-partition-secondary-index-pattern) -복사본을 여러 개 사용 하 여 각 엔터티 다른 저장 **RowKey** 값 (hello에 같은 파티션) tooenable 신속 하 고 효율적인 조회 및 대체 정렬 순서를 사용 하 여 다른 **RowKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-315">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different **RowKey** values (in hello same partition) tooenable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="3a08f-316">[보조 인덱스 간 파티션 패턴](#inter-partition-secondary-index-pattern) -각 사용 하 여 엔터티 RowKey 값이 다른 별도 파티션을 또는 별도 테이블 tooenable 빠른의 여러 복사본을 저장 하 고 다른 를사용하여효율적인조회및대체정렬순서**RowKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-316">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions or in separate tables tooenable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="3a08f-317">[인덱스 엔터티 패턴](#index-entities-pattern) -인덱스 엔터티 tooenable 효율적인 검색 엔터티 목록을 반환 하는 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-317">[Index Entities Pattern](#index-entities-pattern) - Maintain index entities tooenable efficient searches that return lists of entities.</span></span>  

### <a name="sorting-data-in-hello-table-service"></a><span data-ttu-id="3a08f-318">Hello 테이블 서비스의에서 데이터 정렬</span><span class="sxs-lookup"><span data-stu-id="3a08f-318">Sorting data in hello Table service</span></span>
<span data-ttu-id="3a08f-319">hello 테이블 서비스에 따라 내림차순으로 정렬 하는 엔터티를 반환 합니다. **PartitionKey** 한 다음 **RowKey**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-319">hello Table service returns entities sorted in ascending order based on **PartitionKey** and then by **RowKey**.</span></span> <span data-ttu-id="3a08f-320">이러한 키가 문자열 값 및 숫자 값이 올바르게 정렬 tooensure tooa 고정 길이 변환 하 고 0은 사용이 채울 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-320">These keys are string values and tooensure that numeric values sort correctly, you should convert them tooa fixed length and pad them with zeroes.</span></span> <span data-ttu-id="3a08f-321">예를 들어 경우 hello 직원 id 값으로 사용할 있습니다 hello **RowKey** 는 정수 값, 직원 id를 변환 해야 **123** 너무**00000123**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-321">For example, if hello employee id value you use as hello **RowKey** is an integer value, you should convert employee id **123** too**00000123**.</span></span>  

<span data-ttu-id="3a08f-322">많은 응용 프로그램의 순서가 다른 toouse 데이터가 정렬 요구 사항이: 예를 들어, 이름별 또는 날짜를 조인 하 여 직원을 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-322">Many applications have requirements toouse data sorted in different orders: for example, sorting employees by name, or by joining date.</span></span> <span data-ttu-id="3a08f-323">패턴 hello 섹션의 다음 hello [테이블 디자인 패턴](#table-design-patterns) 엔터티에 대 한 tooalternate 정렬 순서 하는 방법을 주소:</span><span class="sxs-lookup"><span data-stu-id="3a08f-323">hello following patterns in hello section [Table Design Patterns](#table-design-patterns) address how tooalternate sort orders for your entities:</span></span>  

* <span data-ttu-id="3a08f-324">[파티션 내 보조 인덱스 패턴](#intra-partition-secondary-index-pattern) -다른 RowKey 값을 사용 하 여 각 엔터티의 여러 복사본을 저장 (hello에 같은 파티션) 다른 RowKey 값을 사용 하 여 tooenable 신속 하 고 효율적인 조회 및 대체 정렬 순서입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-324">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values (in hello same partition) tooenable fast and efficient lookups and alternate sort orders by using different RowKey values.</span></span>  
* <span data-ttu-id="3a08f-325">[보조 인덱스 간 파티션 패턴](#inter-partition-secondary-index-pattern) -tooenable 별도 테이블에서에서 별도 파티션의 빠르게 RowKey 값이 다른를 사용 하 여 각 엔터티의 여러 복사본을 저장 하 고 다른 RowKey를 사용 하 여 효율적인 조회 및 대체 정렬 순서 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-325">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions in separate tables tooenable fast and efficient lookups and alternate sort orders by using different RowKey values.</span></span>
* <span data-ttu-id="3a08f-326">[비상 로그 패턴](#log-tail-pattern) -검색 hello  *n*  엔터티 가장 최근에 추가 된 tooa 파티션을 사용 하 여 한 **RowKey** 역방향 날짜와 시간 순서에 정렬 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-326">[Log tail pattern](#log-tail-pattern) - Retrieve hello *n* entities most recently added tooa partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

## <a name="design-for-data-modification"></a><span data-ttu-id="3a08f-327">데이터 수정을 위한 디자인</span><span class="sxs-lookup"><span data-stu-id="3a08f-327">Design for data modification</span></span>
<span data-ttu-id="3a08f-328">이 섹션 삽입, 업데이트를 최적화 하기 위한 hello 디자인 고려 사항에 중점적으로 설명 하 고 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-328">This section focuses on hello design considerations for optimizing inserts, updates, and deletes.</span></span> <span data-ttu-id="3a08f-329">일부 경우에서와 마찬가지로 관계형 데이터베이스에 대 한 디자인에 (hello 기술을 관리 하기 위한 디자인 hello 하지만 데이터 수정에 대 한 최적화 하는 디자인에 대 한 쿼리를 최적화 하는 설계 간 절충 값 tooevaluate hello 해야 합니다. 상충 관계에서 서로 관계형 데이터베이스).</span><span class="sxs-lookup"><span data-stu-id="3a08f-329">In some cases, you will need tooevaluate hello trade-off between designs that optimize for querying against designs that optimize for data modification just as you do in designs for relational databases (although hello techniques for managing hello design trade-offs are different in a relational database).</span></span> <span data-ttu-id="3a08f-330">섹션 hello [테이블 디자인 패턴](#table-design-patterns) hello 테이블 서비스에 대 한 몇 가지 세부 디자인 패턴을 설명 하 고 몇 이러한 장단점에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-330">hello section [Table Design Patterns](#table-design-patterns) describes some detailed design patterns for hello Table service and highlights some these trade-offs.</span></span> <span data-ttu-id="3a08f-331">실제로 엔터티 쿼리에 최적화된 디자인은 대부분 엔터티를 수정하는 데에도 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-331">In practice, you will find that many designs optimized for querying entities also work well for modifying entities.</span></span>  

### <a name="optimizing-hello-performance-of-insert-update-and-delete-operations"></a><span data-ttu-id="3a08f-332">Hello 성능 최적화의 삽입, 업데이트 및 삭제 작업</span><span class="sxs-lookup"><span data-stu-id="3a08f-332">Optimizing hello performance of insert, update, and delete operations</span></span>
<span data-ttu-id="3a08f-333">tooupdate 또는 엔터티를 삭제, 수 tooidentify 있어야 hello를 사용 하 여 **PartitionKey** 및 **RowKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-333">tooupdate or delete an entity, you must be able tooidentify it by using hello **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="3a08f-334">사용자가 선택한 이러한 점에서 **PartitionKey** 및 **RowKey** 따라야 엔터티 수정 유사한 조건 tooyour 선택 toosupport 가리킨 쿼리 tooidentify 엔터티를 것 이므로 최대한 효율적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-334">In this respect, your choice of **PartitionKey** and **RowKey** for modifying entities should follow similar criteria tooyour choice toosupport point queries because you want tooidentify entities as efficiently as possible.</span></span> <span data-ttu-id="3a08f-335">Toouse는 비효율적인 파티션 또는 테이블 스캔 toolocate 순서 toodiscover hello에 엔터티를 원하지 않는 **PartitionKey** 및 **RowKey** 값 tooupdate 필요 하거나 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-335">You do not want toouse an inefficient partition or table scan toolocate an entity in order toodiscover hello **PartitionKey** and **RowKey** values you need tooupdate or delete it.</span></span>  

<span data-ttu-id="3a08f-336">패턴 hello 섹션의 다음 hello [테이블 디자인 패턴](#table-design-patterns) 주소 hello 성능 최적화 또는 삽입, 업데이트 및 삭제 작업:</span><span class="sxs-lookup"><span data-stu-id="3a08f-336">hello following patterns in hello section [Table Design Patterns](#table-design-patterns) address optimizing hello performance or your insert, update, and delete operations:</span></span>  

* <span data-ttu-id="3a08f-337">[패턴을 삭제 하는 정보의 양이](#high-volume-delete-pattern) -Enable hello 삭제는 대량의 동시 삭제에 대 한 모든 hello 엔터티는 각각의 별도 테이블에 저장 하 여 엔터티; hello 테이블을 삭제 하 여 hello 엔터티를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-337">[High volume delete pattern](#high-volume-delete-pattern) - Enable hello deletion of a high volume of entities by storing all hello entities for simultaneous deletion in their own separate table; you delete hello entities by deleting hello table.</span></span>  
* <span data-ttu-id="3a08f-338">[데이터 계열 패턴](#data-series-pattern) -저장소 전체 데이터 계열에는 단일 엔터티 toominimize hello 수가 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-338">[Data series pattern](#data-series-pattern) - Store complete data series in a single entity toominimize hello number of requests you make.</span></span>  
* <span data-ttu-id="3a08f-339">[넓은 엔터티 패턴](#wide-entities-pattern) -이상 252 속성을 가진 여러 개의 물리적 엔터티 toostore 논리적 엔터티를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-339">[Wide entities pattern](#wide-entities-pattern) - Use multiple physical entities toostore logical entities with more than 252 properties.</span></span>  
* <span data-ttu-id="3a08f-340">[큰 엔터티 패턴](#large-entities-pattern) -blob 저장소 toostore 큰 속성 값 사용.</span><span class="sxs-lookup"><span data-stu-id="3a08f-340">[Large entities pattern](#large-entities-pattern) - Use blob storage toostore large property values.</span></span>  

### <a name="ensuring-consistency-in-your-stored-entities"></a><span data-ttu-id="3a08f-341">저장된 엔터티의 일관성 유지</span><span class="sxs-lookup"><span data-stu-id="3a08f-341">Ensuring consistency in your stored entities</span></span>
<span data-ttu-id="3a08f-342">데이터 수정 최적화를 선택 하는 키 영향을 주는 다른 중요 한 요소 hello 어떻게 원자성 트랜잭션을 사용 하 여 tooensure 일관성.</span><span class="sxs-lookup"><span data-stu-id="3a08f-342">hello other key factor that influences your choice of keys for optimizing data modifications is how tooensure consistency by using atomic transactions.</span></span> <span data-ttu-id="3a08f-343">EGT toooperate hello에 저장 된 엔터티 에서만 사용할 수 있습니다 같은 파티션에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-343">You can only use an EGT toooperate on entities stored in hello same partition.</span></span>  

<span data-ttu-id="3a08f-344">패턴 hello 섹션의 다음 hello [테이블 디자인 패턴](#table-design-patterns) 일관성을 관리 하는 주소:</span><span class="sxs-lookup"><span data-stu-id="3a08f-344">hello following patterns in hello section [Table Design Patterns](#table-design-patterns) address managing consistency:</span></span>  

* <span data-ttu-id="3a08f-345">[파티션 내 보조 인덱스 패턴](#intra-partition-secondary-index-pattern) -복사본을 여러 개 사용 하 여 각 엔터티 다른 저장 **RowKey** 값 (hello에 같은 파티션) tooenable 신속 하 고 효율적인 조회 및 대체 정렬 순서를 사용 하 여 다른 **RowKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-345">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different **RowKey** values (in hello same partition) tooenable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="3a08f-346">[보조 인덱스 간 파티션 패턴](#inter-partition-secondary-index-pattern) -각 사용 하 여 엔터티 RowKey 값이 다른 별도 파티션을 또는 별도 테이블 tooenable 빠른의 여러 복사본을 저장 하 고 다른 를사용하여효율적인조회및대체정렬순서**RowKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-346">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions or in separate tables tooenable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="3a08f-347">[결과적으로 일관성 있는 트랜잭션 패턴](#eventually-consistent-transactions-pattern) - Azure 큐를 사용하여 파티션 경계 또는 저장소 시스템 경계 간에 결과적으로 일관성 있는 동작을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-347">[Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) - Enable eventually consistent behavior across partition boundaries or storage system boundaries by using Azure queues.</span></span>
* <span data-ttu-id="3a08f-348">[인덱스 엔터티 패턴](#index-entities-pattern) -인덱스 엔터티 tooenable 효율적인 검색 엔터티 목록을 반환 하는 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-348">[Index Entities Pattern](#index-entities-pattern) - Maintain index entities tooenable efficient searches that return lists of entities.</span></span>  
* <span data-ttu-id="3a08f-349">[비 정규화 패턴](#denormalization-pattern) -결합 되어 감사가 만들어집니다 관련 데이터를 함께 단일 엔터티 tooenable에 tooretrieve 모든 hello 필요한 데이터를 단일 지점 쿼리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-349">[Denormalization pattern](#denormalization-pattern) - Combine related data together in a single entity tooenable you tooretrieve all hello data you need with a single point query.</span></span>  
* <span data-ttu-id="3a08f-350">[데이터 계열 패턴](#data-series-pattern) -저장소 전체 데이터 계열에는 단일 엔터티 toominimize hello 수가 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-350">[Data series pattern](#data-series-pattern) - Store complete data series in a single entity toominimize hello number of requests you make.</span></span>  

<span data-ttu-id="3a08f-351">엔터티 그룹 트랜잭션에 대 한 정보를 hello 섹션을 참조 하십시오. [엔터티 그룹 트랜잭션을](#entity-group-transactions)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-351">For information about entity group transactions, see hello section [Entity Group Transactions](#entity-group-transactions).</span></span>  

### <a name="ensuring-your-design-for-efficient-modifications-facilitates-efficient-queries"></a><span data-ttu-id="3a08f-352">효율적인 수정을 위한 디자인이 효율적인 쿼리에도 유용</span><span class="sxs-lookup"><span data-stu-id="3a08f-352">Ensuring your design for efficient modifications facilitates efficient queries</span></span>
<span data-ttu-id="3a08f-353">대부분의 경우 특정 시나리오에 대 한 hello 대/소문자 인지 여부를 항상 효율적인 수정 작업에 효율적으로 쿼리 결과 대 한 디자인 평가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-353">In many cases, a design for efficient querying results in efficient modifications, but you should always evaluate whether this is hello case for your specific scenario.</span></span> <span data-ttu-id="3a08f-354">일부 hello 섹션의 hello 패턴 [테이블 디자인 패턴](#table-design-patterns) 명시적으로 쿼리 및 수정 엔터티 간의 장단점을 평가 하 고 각 유형의 작업이의 계정 hello 번호를 항상 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-354">Some of hello patterns in hello section [Table Design Patterns](#table-design-patterns) explicitly evaluate trade-offs between querying and modifying entities, and you should always take into account hello number of each type of operation.</span></span>  

<span data-ttu-id="3a08f-355">패턴 hello 섹션의 다음 hello [테이블 디자인 패턴](#table-design-patterns) 효율적인 쿼리를 위해 디자인 하 고 효율적인 데이터 수정을 위한 디자인 간의 장단점 주소:</span><span class="sxs-lookup"><span data-stu-id="3a08f-355">hello following patterns in hello section [Table Design Patterns](#table-design-patterns) address trade-offs between designing for efficient queries and designing for efficient data modification:</span></span>  

* <span data-ttu-id="3a08f-356">[복합 키 패턴](#compound-key-pattern) -사용 하 여 복합 **RowKey** 값 tooenable 클라이언트 toolookup 관련 데이터는 단일 지점에서 쿼리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-356">[Compound key pattern](#compound-key-pattern) - Use compound **RowKey** values tooenable a client toolookup related data with a single point query.</span></span>  
* <span data-ttu-id="3a08f-357">[비상 로그 패턴](#log-tail-pattern) -검색 hello  *n*  엔터티 가장 최근에 추가 된 tooa 파티션을 사용 하 여 한 **RowKey** 역방향 날짜와 시간 순서에 정렬 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-357">[Log tail pattern](#log-tail-pattern) - Retrieve hello *n* entities most recently added tooa partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

## <a name="encrypting-table-data"></a><span data-ttu-id="3a08f-358">테이블 데이터의 암호화</span><span class="sxs-lookup"><span data-stu-id="3a08f-358">Encrypting Table Data</span></span>
<span data-ttu-id="3a08f-359">삽입에 대 한 문자열 엔터티 속성의.NET Azure 저장소 클라이언트 라이브러리 지원 암호화 hello 및 교체 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-359">hello .NET Azure Storage Client Library supports encryption of string entity properties for insert and replace operations.</span></span> <span data-ttu-id="3a08f-360">이진 속성으로 암호화 하는 hello 문자열 hello 서비스에 저장 됩니다 및 암호 해독 한 후 뒤로 toostrings 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-360">hello encrypted strings are stored on hello service as binary properties, and they are converted back toostrings after decryption.</span></span>    

<span data-ttu-id="3a08f-361">테이블의 경우 또한 toohello 암호화 정책 사용자 지정 해야 hello 속성 toobe 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-361">For tables, in addition toohello encryption policy, users must specify hello properties toobe encrypted.</span></span> <span data-ttu-id="3a08f-362">이것은 특성(TableEntity에서 파생 되는 POCO 엔터티)을 지정[EncryptProperty]하거나 암호화 해결 프로그램 요청 옵션에서 수행할 수 있습니다. </span><span class="sxs-lookup"><span data-stu-id="3a08f-362">This can be done by either specifying an [EncryptProperty] attribute (for POCO entities that derive from TableEntity) or an encryption resolver in request options.</span></span> <span data-ttu-id="3a08f-363">암호화 해결 프로그램은 파티션 키, 행 키, 그리고 속성 이름 및 암호화 여부 속성을 나타내는  Bool방식을 반환하는 대표자입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-363">An encryption resolver is a delegate that takes a partition key, row key, and property name and returns a Boolean that indicates whether that property should be encrypted.</span></span> <span data-ttu-id="3a08f-364">암호화 하는 동안 toohello 통신에 쓰는 동안 속성을 암호화 해야 하는지 여부를 hello 클라이언트 라이브러리 정보 toodecide이를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-364">During encryption, hello client library will use this information toodecide whether a property should be encrypted while writing toohello wire.</span></span> <span data-ttu-id="3a08f-365">또한 hello 대리자 hello 가능성은 속성이 암호화 주위 논리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-365">hello delegate also provides for hello possibility of logic around how properties are encrypted.</span></span> <span data-ttu-id="3a08f-366">(예를 들어 X의 경우, A 속성을 암호화하고 그렇지 않은 경우 A와 B 속성을 암호화) 한다는 확인은 필요 하지 않은 tooprovide 읽기 또는 엔터티를 쿼리 하는 동안이 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-366">(For example, if X, then encrypt property A; otherwise encrypt properties A and B.) Note that it is not necessary tooprovide this information while reading or querying entities.</span></span>

<span data-ttu-id="3a08f-367">병합은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-367">Note that merge is not currently supported.</span></span> <span data-ttu-id="3a08f-368">속성 하위 집합 암호화 된 다른 키를 사용 하 여 이전에, 이후 hello 새 속성을 병합 하 고 hello 메타 데이터를 업데이트 하기만 하면 데이터가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-368">Since a subset of properties may have been encrypted previously using a different key, simply merging hello new properties and updating hello metadata will result in data loss.</span></span> <span data-ttu-id="3a08f-369">Hello 서비스에서 tooread hello 기존 엔터티를 호출 추가 서비스를 만드는 또는 속성 당 새 키를 사용 하는 적합 하지 않은 성능상의 이유로 필요 하거나 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-369">Merging either requires making extra service calls tooread hello pre-existing entity from hello service, or using a new key per property, both of which are not suitable for performance reasons.</span></span>     

<span data-ttu-id="3a08f-370">테이블 데이터를 암호화에 대한 정보는 [클라이언트측 암호화 및 Microsoft Azure 저장소에 대한 Azure 키 자격 증명 모음](../storage/common/storage-client-side-encryption.md)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="3a08f-370">For information about encrypting table data, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../storage/common/storage-client-side-encryption.md).</span></span>  

## <a name="modelling-relationships"></a><span data-ttu-id="3a08f-371">관계 모델링</span><span class="sxs-lookup"><span data-stu-id="3a08f-371">Modelling relationships</span></span>
<span data-ttu-id="3a08f-372">도메인 모델을 작성은 복잡 한 시스템의 hello 디자인에 중요 한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-372">Building domain models is a key step in hello design of complex systems.</span></span> <span data-ttu-id="3a08f-373">일반적으로 프로세스 tooidentify 엔터티를 모델링 하는 hello를 사용 하 고 hello 관계도 방식으로 toounderstand로 비즈니스 도메인 hello 및 시스템의 hello 디자인에 게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-373">Typically, you use hello modelling process tooidentify entities and hello relationships between them as a way toounderstand hello business domain and inform hello design of your system.</span></span> <span data-ttu-id="3a08f-374">이 ½ º å 어떻게 hello 테이블 서비스에 대 한 도메인 모델 toodesigns에 hello 일반적인 관계 유형 중 일부 번역할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-374">This section focuses on how you can translate some of hello common relationship types found in domain models toodesigns for hello Table service.</span></span> <span data-ttu-id="3a08f-375">논리적 데이터 모델 tooa 물리적 기반 NoSQL 데이터 모델에서 매핑의 hello 프로세스는 관계형 데이터베이스를 디자인할 때 사용 되는 매우 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-375">hello process of mapping from a logical data-model tooa physical NoSQL based data-model is very different from that used when designing a relational database.</span></span> <span data-ttu-id="3a08f-376">일반적으로 관계형 데이터베이스 디자인 중복 – 및 요약에 hello 데이터베이스의 작동 원리의 구현 방법을 hello 선언적 쿼리 기능을 최소화 하기 위한 액세스에 최적화 된 데이터 정규화 프로세스를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-376">Relational databases design typically assumes a data normalization process optimized for minimizing redundancy – and a declarative querying capability that abstracts how hello implementation of how hello database works.</span></span>  

### <a name="one-to-many-relationships"></a><span data-ttu-id="3a08f-377">일대다 관계</span><span class="sxs-lookup"><span data-stu-id="3a08f-377">One-to-many relationships</span></span>
<span data-ttu-id="3a08f-378">비즈니스 도메인 개체 간의 일대다 관계는 매우 빈번하게 발생합니다. 예를 들어 하나의 부서에 여러 직원이 있는 경우가 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-378">One-to-many relationships between business domain objects occur very frequently: for example, one department has many employees.</span></span> <span data-ttu-id="3a08f-379">테이블 서비스 각 장점 및 단점 관련 toohello 특정 시나리오를 될 수 있는 hello에는 몇 가지 방법으로 tooimplement 대 다 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-379">There are several ways tooimplement one-to-many relationships in hello Table service each with pros and cons that may be relevant toohello particular scenario.</span></span>  

<span data-ttu-id="3a08f-380">Hello 예제를 다국적 대기업의 수만 부서 및 employee 엔터티 여기서 모든 부서는 직원 및 각 직원 한 특정 부서와 관련 된 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-380">Consider hello example of a large multi-national corporation with tens of thousands of departments and employee entities where every department has many employees and each employee as associated with one specific department.</span></span> <span data-ttu-id="3a08f-381">한 가지 방법은 이러한 employee 엔터티 toostore 별도 부서입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-381">One approach is toostore separate department and employee entities such as these:</span></span>  

![][1]

<span data-ttu-id="3a08f-382">이 예에서는 hello에 따라 hello 형식 간의 암시적 대 다 관계가 **PartitionKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-382">This example shows an implicit one-to-many relationship between hello types based on hello **PartitionKey** value.</span></span> <span data-ttu-id="3a08f-383">각 부서에는 여러 직원이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-383">Each department can have many employees.</span></span>  

<span data-ttu-id="3a08f-384">해당 직원 관련된 엔터티를 같은 파티션 hello 및이 예제에서는 또한 department 엔터티를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-384">This example also shows a department entity and its related employee entities in hello same partition.</span></span> <span data-ttu-id="3a08f-385">Toouse 다른 파티션, 테이블 또는 심지어 hello 서로 다른 엔터티 형식에 대 한 저장소 계정을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-385">You could choose toouse different partitions, tables, or even storage accounts for hello different entity types.</span></span>  

<span data-ttu-id="3a08f-386">다른 접근 방식은 hello 다음 예제와 같이 toodenormalize 정규화 되지 않은 부서 데이터와 사용자 데이터 및 스토어만 employee 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-386">An alternative approach is toodenormalize your data and store only employee entities with denormalized department data as shown in hello following example.</span></span> <span data-ttu-id="3a08f-387">에서는이 특정 시나리오에서 정규화 되지 않은이 방법은 아닐 수 있습니다 hello 최상의 부서 관리자의 요구 사항 toobe 수 toochange hello 정보 때문에 있는 경우 toodo이 tooupdate hello 부서의 모든 직원을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-387">In this particular scenario, this denormalized approach may not be hello best if you have a requirement toobe able toochange hello details of a department manager because toodo this you need tooupdate every employee in hello department.</span></span>  

![][2]

<span data-ttu-id="3a08f-388">자세한 내용은 참조 hello [비 정규화 패턴](#denormalization-pattern) 이 가이드의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-388">For more information, see hello [Denormalization pattern](#denormalization-pattern) later in this guide.</span></span>  

<span data-ttu-id="3a08f-389">hello 다음 표에 요약 되어 hello 장점 및 단점을 employee 및 department 엔터티 대 다 관계가 있는 저장 하기 위해 위에서 설명한 hello 방법 중 한 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-389">hello following table summarizes hello pros and cons of each of hello approaches outlined above for storing employee and department entities that have a one-to-many relationship.</span></span> <span data-ttu-id="3a08f-390">예상 되는 빈도 tooperform 다양 한 작업을 고려해 야: 허용 toohave 해당 작업 으로만 자주 발생 하는 경우 비용이 많이 드는 작업이 포함 된 디자인 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-390">You should also consider how often you expect tooperform various operations: it may be acceptable toohave a design that includes an expensive operation if that operation only happens infrequently.</span></span>  

<table>
<tr>
<th><span data-ttu-id="3a08f-391">접근 방식</span><span class="sxs-lookup"><span data-stu-id="3a08f-391">Approach</span></span></th>
<th><span data-ttu-id="3a08f-392">장점</span><span class="sxs-lookup"><span data-stu-id="3a08f-392">Pros</span></span></th>
<th><span data-ttu-id="3a08f-393">단점</span><span class="sxs-lookup"><span data-stu-id="3a08f-393">Cons</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="3a08f-394">별도의 엔터티 유형, 동일한 파티션, 동일한 테이블</span><span class="sxs-lookup"><span data-stu-id="3a08f-394">Separate entity types, same partition, same table</span></span></td>
<td>
<ul>
<li><span data-ttu-id="3a08f-395">단일 작업으로 부서 엔터티를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-395">You can update a department entity with a single operation.</span></span></li>
<li><span data-ttu-id="3a08f-396">요구 사항 toomodify department 엔터티를 설정한 경우 EGT toomaintain 일관성을 사용할 수 있습니다 때마다 있습니다 업데이트/삽입/삭제 employee 엔터티.</span><span class="sxs-lookup"><span data-stu-id="3a08f-396">You can use an EGT toomaintain consistency if you have a requirement toomodify a department entity whenever you update/insert/delete an employee entity.</span></span> <span data-ttu-id="3a08f-397">예를 들어 각 부서의 직원 수를 유지 관리하는 경우가 여기에 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-397">For example if you maintain a departmental employee count for each department.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="3a08f-398">일부 클라이언트 작업에 대 한 tooretrieve는 employee 및 department 엔터티 둘 다 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-398">You may need tooretrieve both an employee and a department entity for some client activities.</span></span></li>
<li><span data-ttu-id="3a08f-399">Hello에 저장소 작업이 수행 동일한 파티션 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-399">Storage operations happen in hello same partition.</span></span> <span data-ttu-id="3a08f-400">대용량 트랜잭션의 경우 핫스폿이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-400">At high transaction volumes, this may result in a hotspot.</span></span></li>
<li><span data-ttu-id="3a08f-401">EGT를 사용 하 여 직원 tooa 새 부서를 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-401">You cannot move an employee tooa new department using an EGT.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="3a08f-402">별도의 엔터티 유형, 서로 다른 파티션, 테이블 또는 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="3a08f-402">Separate entity types, different partitions or tables or storage accounts</span></span></td>
<td>
<ul>
<li><span data-ttu-id="3a08f-403">단일 작업으로 부서 엔터티 또는 직원 엔터티를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-403">You can update a department entity or employee entity with a single operation.</span></span></li>
<li><span data-ttu-id="3a08f-404">많은 트랜잭션 볼륨에 도움이 될 수 있습니다이 더 많은 파티션 간에 확산 hello 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-404">At high transaction volumes, this may help spread hello load across more partitions.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="3a08f-405">일부 클라이언트 작업에 대 한 tooretrieve는 employee 및 department 엔터티 둘 다 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-405">You may need tooretrieve both an employee and a department entity for some client activities.</span></span></li>
<li><span data-ttu-id="3a08f-406">EGTs toomaintain 일관성을 사용할 수 없는 때 하면 업데이트/삽입/삭제는 직원 및 부서 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-406">You cannot use EGTs toomaintain consistency when you update/insert/delete an employee and update a department.</span></span> <span data-ttu-id="3a08f-407">예를 들어 부서 엔터티의 직원 수를 업데이트하는 경우가 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-407">For example, updating an employee count in a department entity.</span></span></li>
<li><span data-ttu-id="3a08f-408">EGT를 사용 하 여 직원 tooa 새 부서를 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-408">You cannot move an employee tooa new department using an EGT.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="3a08f-409">단일 엔터티 유형으로 비정규화</span><span class="sxs-lookup"><span data-stu-id="3a08f-409">Denormalize into single entity type</span></span></td>
<td>
<ul>
<li><span data-ttu-id="3a08f-410">단일 요청으로 필요한 모든 hello 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-410">You can retrieve all hello information you need with a single request.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="3a08f-411">(이 위해서는 있습니다 tooupdate 부서에 모든 hello 직원) tooupdate 부서 정보가 필요한 경우 비용이 많이 드는 toomaintain 일관성 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-411">It may be expensive toomaintain consistency if you need tooupdate department information (this would require you tooupdate all hello employees in a department).</span></span></li>
</ul>
</td>
</tr>
</table>

<span data-ttu-id="3a08f-412">이러한 옵션 중 hello 전문가 사이의 선택 방법과 관련 하 여 아래의 가장 중요 한 특정 응용 프로그램 시나리오에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-412">How you choose between these options, and which of hello pros and cons are most significant, depends on your specific application scenarios.</span></span> <span data-ttu-id="3a08f-413">예를 들어 얼마나 자주 수행 하면 부서 엔터티 수정; 모든 직원 쿼리 hello 추가 부서별 정보; 필요가 얼마나 비슷한지를? 파티션 또는 저장소 계정에서 toohello 확장성 제한</span><span class="sxs-lookup"><span data-stu-id="3a08f-413">For example, how often do you modify department entities; do all your employee queries need hello additional departmental information; how close are you toohello scalability limits on your partitions or your storage account?</span></span>  

### <a name="one-to-one-relationships"></a><span data-ttu-id="3a08f-414">일대일 관계</span><span class="sxs-lookup"><span data-stu-id="3a08f-414">One-to-one relationships</span></span>
<span data-ttu-id="3a08f-415">도메인 모델은 엔터티 간의 일대일 관계를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-415">Domain models may include one-to-one relationships between entities.</span></span> <span data-ttu-id="3a08f-416">Hello 테이블 서비스에에서 한 일 관계 tooimplement 해야 할 경우 필요할 때 tooretrieve 모두 두 개의 관련된 엔터티 toolink hello 하는 방법을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-416">If you need tooimplement a one-to-one relationship in hello Table service, you must also choose how toolink hello two related entities when you need tooretrieve them both.</span></span> <span data-ttu-id="3a08f-417">이 링크 암시적, hello 키 값에 규칙에 따라 또는 가능 명시적 hello 형태의에 대 한 링크를 저장 하 여 **PartitionKey** 및 **RowKey** 각 엔터티 tooits 값 관련 엔터티.</span><span class="sxs-lookup"><span data-stu-id="3a08f-417">This link can be either implicit, based on a convention in hello key values, or explicit by storing a link in hello form of **PartitionKey** and **RowKey** values in each entity tooits related entity.</span></span> <span data-ttu-id="3a08f-418">관련 엔터티 hello를 저장 해야 하는지 여부에 미치는 같은 파티션에 hello 하 hello 섹션을 참조 [대 다 관계](#one-to-many-relationships)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-418">For a discussion of whether you should store hello related entities in hello same partition, see hello section [One-to-many relationships](#one-to-many-relationships).</span></span>  

<span data-ttu-id="3a08f-419">구현 고려 사항 이어질 수 있는 있습니다 tooimplement 한 일 관계 hello 테이블 서비스에도 지 note:</span><span class="sxs-lookup"><span data-stu-id="3a08f-419">Note that there are also implementation considerations that might lead you tooimplement one-to-one relationships in hello Table service:</span></span>  

* <span data-ttu-id="3a08f-420">큰 엔터티 처리(자세한 내용은 [큰 엔터티 패턴](#large-entities-pattern)참조)</span><span class="sxs-lookup"><span data-stu-id="3a08f-420">Handling large entities (for more information, see [Large Entities Pattern](#large-entities-pattern)).</span></span>  
* <span data-ttu-id="3a08f-421">액세스 제어 구현(자세한 내용은 [공유 액세스 서명을 사용하여 액세스 제어](#controlling-access-with-shared-access-signatures)참조)</span><span class="sxs-lookup"><span data-stu-id="3a08f-421">Implementing access controls (for more information, see [Controlling access with Shared Access Signatures](#controlling-access-with-shared-access-signatures)).</span></span>  

### <a name="join-in-hello-client"></a><span data-ttu-id="3a08f-422">클라이언트 hello에 가입</span><span class="sxs-lookup"><span data-stu-id="3a08f-422">Join in hello client</span></span>
<span data-ttu-id="3a08f-423">테이블 서비스 hello 방법 toomodel 관계 있지만 있습니다 해야 잊지 hello hello 테이블 서비스를 사용 하기 위한 두 가지 주요 이유는 확장성 및 성능.</span><span class="sxs-lookup"><span data-stu-id="3a08f-423">Although there are ways toomodel relationships in hello Table service, you should not forget that hello two prime reasons for using hello Table service are scalability and performance.</span></span> <span data-ttu-id="3a08f-424">솔루션의 hello 성능 및 확장성을 손상 시킬 수 있는 많은 관계를 모델링 하는 경우 고려해 야 할 모든 hello 데이터 관계 테이블 디자인에 필요한 toobuild 경우.</span><span class="sxs-lookup"><span data-stu-id="3a08f-424">If you find you are modelling many relationships that compromise hello performance and scalability of your solution, you should ask yourself if it is necessary toobuild all hello data relationships into your table design.</span></span> <span data-ttu-id="3a08f-425">수 toosimplify hello 디자인 하 고 필요한 모든 조인을 수행 하는 클라이언트 응용 프로그램을 사용 하는 경우 솔루션의 hello 확장성과 성능을 향상 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-425">You may be able toosimplify hello design and improve hello scalability and performance of your solution if you let your client application perform any necessary joins.</span></span>  

<span data-ttu-id="3a08f-426">예를 들어 매우 자주 변경 되지 않는 데이터가 포함 된 작은 테이블의 경우 다음이 데이터를 한 번에 검색할 수 있고 hello 클라이언트에 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-426">For example, if you have small tables that contain data that does not change very often, then you can retrieve this data once and cache it on hello client.</span></span> <span data-ttu-id="3a08f-427">이 반복된 왕복을 방지할 수 tooretrieve hello 같은 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-427">This can avoid repeated roundtrips tooretrieve hello same data.</span></span> <span data-ttu-id="3a08f-428">이 가이드에서 살펴본 hello 예제에서 hello 부서 중소기업에서의 집합이 작은 가능성이 toobe 및 자주 있으므로 적합 한 클라이언트 응용 프로그램에 한 번만 다운로드할 수 있는 데이터 및 캐시 데이터를 모양으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-428">In hello examples we have looked at in this guide, hello set of departments in a small organization is likely toobe small and change infrequently making it a good candidate for data that client application can download once and cache as look up data.</span></span>  

### <a name="inheritance-relationships"></a><span data-ttu-id="3a08f-429">상속 관계</span><span class="sxs-lookup"><span data-stu-id="3a08f-429">Inheritance relationships</span></span>
<span data-ttu-id="3a08f-430">클라이언트 응용 프로그램의 클래스는 상속 관계 toorepresent 비즈니스 엔터티의 일부를 구성 하는 집합을 사용 하는 경우 hello 테이블 서비스에서에서 해당 엔터티를 쉽게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-430">If your client application uses a set of classes that form part of an inheritance relationship toorepresent business entities, you can easily persist those entities in hello Table service.</span></span> <span data-ttu-id="3a08f-431">예를 들어 클라이언트 응용 프로그램에 정의 된 클래스 집합을 추적 하는 hello 해야할 여기서 **사람** 클래스는 추상 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-431">For example, you might have hello following set of classes defined in your client application where **Person** is an abstract class.</span></span>

![][3]

<span data-ttu-id="3a08f-432">Hello hello에는 다음과 같은 엔터티를 사용 하 여 단일 Person 테이블을 사용 하 여 테이블 서비스에 두 개의 구체적 클래스의 인스턴스를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-432">You can persist instances of hello two concrete classes in hello Table service using a single Person table using entities in that look like this:</span></span>  

![][4]

<span data-ttu-id="3a08f-433">Hello 클라이언트 코드에서 동일한 테이블로의 엔터티 형식에 여러 작업에 대 한 자세한 내용은 hello 섹션을 참조 하십시오. [유형이 다른 엔터티 형식 작업](#working-with-heterogeneous-entity-types) 이 가이드의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-433">For more information about working with multiple entity types in hello same table in client code, see hello section [Working with heterogeneous entity types](#working-with-heterogeneous-entity-types) later in this guide.</span></span> <span data-ttu-id="3a08f-434">Toorecognize 클라이언트 코드의 엔터티 형식을 hello 하는 방법의 예를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-434">This provides examples of how toorecognize hello entity type in client code.</span></span>  

## <a name="table-design-patterns"></a><span data-ttu-id="3a08f-435">테이블 디자인 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-435">Table Design Patterns</span></span>
<span data-ttu-id="3a08f-436">이전 섹션에서 toooptimize 테이블와 디자인 방법 모두 엔터티 데이터를 검색할 쿼리를 사용 하 여에 대 한 삽입, 업데이트, 및 엔터티 데이터를 삭제 하는 방법에 대 한 자세한 내용은 일부에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-436">In previous sections, you have seen some detailed discussions about how toooptimize your table design for both retrieving entity data using queries and for inserting, updating, and deleting entity data.</span></span> <span data-ttu-id="3a08f-437">이 섹션에서는 테이블 서비스 솔루션에서 사용하기에 적합한 몇 가지 패턴에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-437">This section describes some patterns appropriate for use with Table service solutions.</span></span> <span data-ttu-id="3a08f-438">또한 어떻게 해결할 수 있습니다 거의 hello 문제와 장단점이이 가이드에서 이전에 발생 하는 중 일부에 대해 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-438">In addition, you will see how you can practically address some of hello issues and trade-offs raised previously in this guide.</span></span> <span data-ttu-id="3a08f-439">hello 다음 다이어그램에서는 요약 hello 다양 한 패턴 간에 hello 관계 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-439">hello following diagram summarizes hello relationships between hello different patterns:</span></span>  

![][5]

<span data-ttu-id="3a08f-440">위의 hello 패턴 지도 패턴 (파란색),이 가이드에 설명 되어 있는 바이러스 패턴 (주황) 간에 관계를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-440">hello pattern map above highlights some relationships between patterns (blue) and anti-patterns (orange) that are documented in this guide.</span></span> <span data-ttu-id="3a08f-441">물론 고려할 만한 다른 많은 패턴도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-441">There are of course many other patterns that are worth considering.</span></span> <span data-ttu-id="3a08f-442">예를 들어 hello 테이블 서비스에 대 한 주요 시나리오 중 하나는 toouse hello [구체화 된 뷰 패턴](https://msdn.microsoft.com/library/azure/dn589782.aspx) hello에서 [명령 쿼리 책임 분리 (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-442">For example, one of hello key scenarios for Table Service is toouse hello [Materialized View Pattern](https://msdn.microsoft.com/library/azure/dn589782.aspx) from hello [Command Query Responsibility Segregation (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) pattern.</span></span>  

### <a name="intra-partition-secondary-index-pattern"></a><span data-ttu-id="3a08f-443">파티션 간 보조 인덱스 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-443">Intra-partition secondary index pattern</span></span>
<span data-ttu-id="3a08f-444">복사본을 여러 개 사용 하 여 각 엔터티 다른 저장 **RowKey** 값 (hello에 같은 파티션) 다른을 사용 하 여 tooenable 신속 하 고 효율적인 조회 및 대체 정렬 순서 **RowKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-444">Store multiple copies of each entity using different **RowKey** values (in hello same partition) tooenable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span> <span data-ttu-id="3a08f-445">EGT를 사용하여 복사본 간의 업데이트를 일관성 있게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-445">Updates between copies can be kept consistent using EGT's.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="3a08f-446">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="3a08f-446">Context and problem</span></span>
<span data-ttu-id="3a08f-447">테이블 서비스 hello hello를 사용 하 여 엔터티를 자동으로 인덱싱됩니다 **PartitionKey** 및 **RowKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-447">hello Table service automatically indexes entities using hello **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="3a08f-448">이렇게 하면 클라이언트 응용 프로그램 tooretrieve 효율적으로 이러한 값을 사용 하는 엔터티.</span><span class="sxs-lookup"><span data-stu-id="3a08f-448">This enables a client application tooretrieve an entity efficiently using these values.</span></span> <span data-ttu-id="3a08f-449">예를 들어, 아래에 표시 된 hello 테이블 구조를 사용 하는 클라이언트 응용 프로그램 צ ְ ײ 지점 쿼리 tooretrieve 개별 employee 엔터티 hello 부서 이름 및 hello 직원 id를 사용 하 여 (hello **PartitionKey** 및  **RowKey** 값).</span><span class="sxs-lookup"><span data-stu-id="3a08f-449">For example, using hello table structure shown below, a client application can use a point query tooretrieve an individual employee entity by using hello department name and hello employee id (hello **PartitionKey** and **RowKey** values).</span></span> <span data-ttu-id="3a08f-450">또한 클라이언트는 각 부서 내에서 직원 ID별로 정렬된 엔터티를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-450">A client can also retrieve entities sorted by employee id within each department.</span></span>

![][6]

<span data-ttu-id="3a08f-451">또한 toobe 수 toofind 전자 메일 주소 등의 다른 속성의 hello 값에 따라 employee 엔터티를 원하는 경우 효율성이 떨어지는 파티션 검색 toofind 일치 하는 항목을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-451">If you also want toobe able toofind an employee entity based on hello value of another property, such as email address, you must use a less efficient partition scan toofind a match.</span></span> <span data-ttu-id="3a08f-452">Hello 테이블 서비스에서 보조 인덱스를 제공 하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-452">This is because hello table service does not provide secondary indexes.</span></span> <span data-ttu-id="3a08f-453">또한 없는 없습니다 옵션 toorequest 보다 다른 순서로 정렬 하는 직원의 목록이 **RowKey** 순서입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-453">In addition, there is no option toorequest a list of employees sorted in a different order than **RowKey** order.</span></span>  

#### <a name="solution"></a><span data-ttu-id="3a08f-454">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3a08f-454">Solution</span></span>
<span data-ttu-id="3a08f-455">보조 인덱스의 부족 hello 주위 toowork, 각 엔터티와 다른를 사용 하 여 각 복사본의 여러 복사본을 저장할 수 있습니다 **RowKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-455">toowork around hello lack of secondary indexes, you can store multiple copies of each entity with each copy using a different **RowKey** value.</span></span> <span data-ttu-id="3a08f-456">Hello 구조 아래에 표시 된 엔터티를 저장 하는 경우 전자 메일 주소 또는 직원 id에 따라 employee 엔터티를 효율적으로 검색할 수 있습니다. hello에 대 한 접두사 값 hello **RowKey**, "empid_" 및 "email_" 사용 하면 tooquery는 한 명의 직원과 또는 직원의 범위에 대 한 전자 메일 주소 또는 직원 id 범위를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-456">If you store an entity with hello structures shown below, you can efficiently retrieve employee entities based on email address or employee id. hello prefix values for hello **RowKey**, "empid_" and "email_" enable you tooquery for a single employee or a range of employees by using a range of email addresses or employee ids.</span></span>  

![][7]

<span data-ttu-id="3a08f-457">지점 쿼리를 지정 둘 다 두 필터 조건 (하나를 조회 직원 id와 전자 메일 주소를 조회 하나)를 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="3a08f-457">hello following two filter criteria (one looking up by employee id and one looking up by email address) both specify point queries:</span></span>  

* <span data-ttu-id="3a08f-458">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'empid_000223')</span><span class="sxs-lookup"><span data-stu-id="3a08f-458">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'empid_000223')</span></span>  
* <span data-ttu-id="3a08f-459">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'email_jonesj@contoso.com')</span><span class="sxs-lookup"><span data-stu-id="3a08f-459">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'email_jonesj@contoso.com')</span></span>  

<span data-ttu-id="3a08f-460">직원 id 순으로 정렬 된 범위 또는 hello hello에 적절 한 접두사가 포함 된 엔터티에 대 한 쿼리를 통해 전자 메일 주소 순서로 정렬 된 범위를 지정할 수 employee 엔터티 범위에 대 한 쿼리 하는 경우 **RowKey**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-460">If you query for a range of employee entities, you can specify a range sorted in employee id order, or a range sorted in email address order by querying for entities with hello appropriate prefix in hello **RowKey**.</span></span>  

* <span data-ttu-id="3a08f-461">toofind hello 범위 000100 too000199의 직원 id와 hello 영업 부서에 모든 hello 직원 사용: $filter = (PartitionKey eq '판매') 및 (RowKey ge 'empid_000100') 및 (RowKey le 'empid_000199')</span><span class="sxs-lookup"><span data-stu-id="3a08f-461">toofind all hello employees in hello Sales department with an employee id in hello range 000100 too000199 use: $filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000100') and (RowKey le 'empid_000199')</span></span>  
* <span data-ttu-id="3a08f-462">hello 영업 부서의 직원 hello로 시작 하는 전자 메일 주소와 hello 모든 toofind 문자 'a' 사용: $filter = (PartitionKey eq '판매') 및 (RowKey ge 'email_a') 및 (RowKey lt 'email_b')</span><span class="sxs-lookup"><span data-stu-id="3a08f-462">toofind all hello employees in hello Sales department with an email address starting with hello letter 'a' use: $filter=(PartitionKey eq 'Sales') and (RowKey ge 'email_a') and (RowKey lt 'email_b')</span></span>  
  
  <span data-ttu-id="3a08f-463">위의 hello 예에 사용 되는 hello 필터 구문에 대 한 자세한 내용은 참조 하십시오 hello 테이블 서비스 REST API에서에서는 [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-463">Note that hello filter syntax used in hello examples above is from hello Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="3a08f-464">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3a08f-464">Issues and considerations</span></span>
<span data-ttu-id="3a08f-465">Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:</span><span class="sxs-lookup"><span data-stu-id="3a08f-465">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="3a08f-466">테이블 저장소 상대적으로 경제적인 toouse 이므로 중복 데이터를 저장할 경우의 오버 헤드 비용 hello 중요 한 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-466">Table storage is relatively cheap toouse so hello cost overhead of storing duplicate data should not be a major concern.</span></span> <span data-ttu-id="3a08f-467">그러나 항상 예상 되는 저장소 요구 사항에 따라 디자인의 hello 비용을 평가 하 고만 중복 항목 toosupport hello 쿼리 실행 됩니다 클라이언트 응용 프로그램을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-467">However, you should always evaluate hello cost of your design based on your anticipated storage requirements and only add duplicate entities toosupport hello queries your client application will execute.</span></span>  
* <span data-ttu-id="3a08f-468">Hello 보조 인덱스 엔터티 hello 원래 엔터티로 분할 동일 hello에 저장 되므로 개별 파티션에 대 한 hello 확장성 목표를 초과 하지 않는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-468">Because hello secondary index entities are stored in hello same partition as hello original entities, you should ensure that you do not exceed hello scalability targets for an individual partition.</span></span>  
* <span data-ttu-id="3a08f-469">원자적으로 hello 엔터티의 EGTs tooupdate hello 두 복사본을 사용 하 여 중복 된 엔터티를 서로 일치 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-469">You can keep your duplicate entities consistent with each other by using EGTs tooupdate hello two copies of hello entity atomically.</span></span> <span data-ttu-id="3a08f-470">이 인해 hello에 엔터티의 모든 복사본 저장 해야 하는 동일한 파티션 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-470">This implies that you should store all copies of an entity in hello same partition.</span></span> <span data-ttu-id="3a08f-471">자세한 내용은 hello 섹션을 참조 하십시오. [엔터티 그룹 트랜잭션을 사용 하 여](#entity-group-transactions)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-471">For more information, see hello section [Using Entity Group Transactions](#entity-group-transactions).</span></span>  
* <span data-ttu-id="3a08f-472">hello에 사용 되는 값을 hello **RowKey** 각 엔터티에 대해 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-472">hello value used for hello **RowKey** must be unique for each entity.</span></span> <span data-ttu-id="3a08f-473">복합 키 값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-473">Consider using compound key values.</span></span>  
* <span data-ttu-id="3a08f-474">안쪽 여백 hello에 숫자 값 **RowKey** (예: hello 직원 id 000223) 하면 정렬 및 하한값과 상한값에 따라 필터링을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-474">Padding numeric values in hello **RowKey** (for example, hello employee id 000223), enables correct sorting and filtering based on upper and lower bounds.</span></span>  
* <span data-ttu-id="3a08f-475">반드시 불필요 tooduplicate 엔터티의 모든 hello 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-475">You do not necessarily need tooduplicate all hello properties of your entity.</span></span> <span data-ttu-id="3a08f-476">예를 들어 경우 hello 쿼리 해당 hello를 사용 하 여 조회 hello 엔터티 전자 메일 주소를 hello에 **RowKey** 필요 hello 직원의 나이, 이러한 엔터티는 다음 구조 hello 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-476">For example, if hello queries that lookup hello entities using hello email address in hello **RowKey** never need hello employee's age, these entities could have hello following structure:</span></span>

![][8]

* <span data-ttu-id="3a08f-477">일반적으로 더 나은 toostore 중복 데이터 사용 되며 모든 hello 필요한 데이터를 단일 쿼리를 검색할 수 있습니다, 엔터티 및 다른 toolookup hello 필요한 데이터 toouse 하나의 쿼리 toolocate 보다 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-477">It is typically better toostore duplicate data and ensure that you can retrieve all hello data you need with a single query, than toouse one query toolocate an entity and another toolookup hello required data.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="3a08f-478">때 toouse이이 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-478">When toouse this pattern</span></span>
<span data-ttu-id="3a08f-479">이 패턴을 사용 하 여 클라이언트 응용 프로그램 클라이언트 tooretrieve 엔터티가 서로 다른 정렬 순서에 필요한 경우에 다양 한 서로 다른 키를 사용 하 여 tooretrieve 엔터티 있고 다양 한 고유 값을 사용 하 여 각 엔터티를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-479">Use this pattern when your client application needs tooretrieve entities using a variety of different keys, when your client needs tooretrieve entities in different sort orders, and where you can identify each entity using a variety of unique values.</span></span> <span data-ttu-id="3a08f-480">그러나 해야 다른 hello를 사용 하 여 엔터티 조회를 수행 하는 경우 hello 파티션 확장성 제한 초과 하지 않는 **RowKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-480">However, you should be sure that you do not exceed hello partition scalability limits when you are performing entity lookups using hello different **RowKey** values.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="3a08f-481">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="3a08f-481">Related patterns and guidance</span></span>
<span data-ttu-id="3a08f-482">hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3a08f-482">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="3a08f-483">파티션 내 보조 인덱스 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-483">Inter-partition secondary index pattern</span></span>](#inter-partition-secondary-index-pattern)
* [<span data-ttu-id="3a08f-484">복합 키 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-484">Compound key pattern</span></span>](#compound-key-pattern)
* [<span data-ttu-id="3a08f-485">엔터티 그룹 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="3a08f-485">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="3a08f-486">유형이 다른 엔터티 유형 작업</span><span class="sxs-lookup"><span data-stu-id="3a08f-486">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)

### <a name="inter-partition-secondary-index-pattern"></a><span data-ttu-id="3a08f-487">파티션 간 보조 인덱스 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-487">Inter-partition secondary index pattern</span></span>
<span data-ttu-id="3a08f-488">복사본을 여러 개 사용 하 여 각 엔터티 다른 저장 **RowKey** 별도 파티션을 또는 별도 테이블 tooenable 신속 하 고 효율적인 조회 및 다른을 사용 하 여 대체 정렬 순서 값 **RowKey**값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-488">Store multiple copies of each entity using different **RowKey** values in separate partitions or in separate tables tooenable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="3a08f-489">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="3a08f-489">Context and problem</span></span>
<span data-ttu-id="3a08f-490">테이블 서비스 hello hello를 사용 하 여 엔터티를 자동으로 인덱싱됩니다 **PartitionKey** 및 **RowKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-490">hello Table service automatically indexes entities using hello **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="3a08f-491">이렇게 하면 클라이언트 응용 프로그램 tooretrieve 효율적으로 이러한 값을 사용 하는 엔터티.</span><span class="sxs-lookup"><span data-stu-id="3a08f-491">This enables a client application tooretrieve an entity efficiently using these values.</span></span> <span data-ttu-id="3a08f-492">예를 들어, 아래에 표시 된 hello 테이블 구조를 사용 하는 클라이언트 응용 프로그램 צ ְ ײ 지점 쿼리 tooretrieve 개별 employee 엔터티 hello 부서 이름 및 hello 직원 id를 사용 하 여 (hello **PartitionKey** 및  **RowKey** 값).</span><span class="sxs-lookup"><span data-stu-id="3a08f-492">For example, using hello table structure shown below, a client application can use a point query tooretrieve an individual employee entity by using hello department name and hello employee id (hello **PartitionKey** and **RowKey** values).</span></span> <span data-ttu-id="3a08f-493">또한 클라이언트는 각 부서 내에서 직원 ID별로 정렬된 엔터티를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-493">A client can also retrieve entities sorted by employee id within each department.</span></span>  

![][9]

<span data-ttu-id="3a08f-494">또한 toobe 수 toofind 전자 메일 주소 등의 다른 속성의 hello 값에 따라 employee 엔터티를 원하는 경우 효율성이 떨어지는 파티션 검색 toofind 일치 하는 항목을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-494">If you also want toobe able toofind an employee entity based on hello value of another property, such as email address, you must use a less efficient partition scan toofind a match.</span></span> <span data-ttu-id="3a08f-495">Hello 테이블 서비스에서 보조 인덱스를 제공 하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-495">This is because hello table service does not provide secondary indexes.</span></span> <span data-ttu-id="3a08f-496">또한 없는 없습니다 옵션 toorequest 보다 다른 순서로 정렬 하는 직원의 목록이 **RowKey** 순서입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-496">In addition, there is no option toorequest a list of employees sorted in a different order than **RowKey** order.</span></span>  

<span data-ttu-id="3a08f-497">이러한 엔터티에 대 한 트랜잭션 매우 큰 용량의 예측은 때 toominimize hello 위험이 hello 테이블 서비스 클라이언트를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-497">You are anticipating a very high volume of transactions against these entities and want toominimize hello risk of hello Table service throttling your client.</span></span>  

#### <a name="solution"></a><span data-ttu-id="3a08f-498">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3a08f-498">Solution</span></span>
<span data-ttu-id="3a08f-499">보조 인덱스의 부족 hello 주위 toowork, 복사본을 여러 개 사용 하 여 각 복사본에 있는 각 엔터티를 다른 저장할 수 있습니다 **PartitionKey** 및 **RowKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-499">toowork around hello lack of secondary indexes, you can store multiple copies of each entity with each copy using different **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="3a08f-500">Hello 구조 아래에 표시 된 엔터티를 저장 하는 경우 전자 메일 주소 또는 직원 id에 따라 employee 엔터티를 효율적으로 검색할 수 있습니다. hello에 대 한 접두사 값 hello **PartitionKey**, "empid_" 및 "email_"를 사용 하면 인덱싱할 있습니다 tooidentify 쿼리에 대 한 toouse 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-500">If you store an entity with hello structures shown below, you can efficiently retrieve employee entities based on email address or employee id. hello prefix values for hello **PartitionKey**, "empid_" and "email_" enable you tooidentify which index you want toouse for a query.</span></span>  

![][10]

<span data-ttu-id="3a08f-501">지점 쿼리를 지정 둘 다 두 필터 조건 (하나를 조회 직원 id와 전자 메일 주소를 조회 하나)를 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="3a08f-501">hello following two filter criteria (one looking up by employee id and one looking up by email address) both specify point queries:</span></span>  

* <span data-ttu-id="3a08f-502">$filter=(PartitionKey eq 'empid_Sales') and (RowKey eq '000223')</span><span class="sxs-lookup"><span data-stu-id="3a08f-502">$filter=(PartitionKey eq 'empid_Sales') and (RowKey eq '000223')</span></span>
* <span data-ttu-id="3a08f-503">$filter=(PartitionKey eq 'email_Sales') and (RowKey eq 'jonesj@contoso.com')</span><span class="sxs-lookup"><span data-stu-id="3a08f-503">$filter=(PartitionKey eq 'email_Sales') and (RowKey eq 'jonesj@contoso.com')</span></span>  

<span data-ttu-id="3a08f-504">직원 id 순으로 정렬 된 범위 또는 hello hello에 적절 한 접두사가 포함 된 엔터티에 대 한 쿼리를 통해 전자 메일 주소 순서로 정렬 된 범위를 지정할 수 employee 엔터티 범위에 대 한 쿼리 하는 경우 **RowKey**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-504">If you query for a range of employee entities, you can specify a range sorted in employee id order, or a range sorted in email address order by querying for entities with hello appropriate prefix in hello **RowKey**.</span></span>  

* <span data-ttu-id="3a08f-505">모든 hello에 직원 toofind hello 영업부 hello 범위의 직원 id와 **000100** 너무**000199** 직원 id 순서 사용에서 정렬: $filter = (PartitionKey eq ' empid_Sales') 및 (RowKey ge ' 000100') 및 (RowKey le '000199')</span><span class="sxs-lookup"><span data-stu-id="3a08f-505">toofind all hello employees in hello Sales department with an employee id in hello range **000100** too**000199** sorted in employee id order use: $filter=(PartitionKey eq 'empid_Sales') and (RowKey ge '000100') and (RowKey le '000199')</span></span>  
* <span data-ttu-id="3a08f-506">toofind에 정렬 된 'a'로 시작 하는 메일 주소로 hello 영업 부서에 모든 hello 직원 전자 메일 주소 순서 사용: $filter = (PartitionKey eq ' email_Sales') 및 (RowKey ge 'a') 및 (RowKey lt 'b')</span><span class="sxs-lookup"><span data-stu-id="3a08f-506">toofind all hello employees in hello Sales department with an email address that starts with 'a' sorted in email address order use: $filter=(PartitionKey eq 'email_Sales') and (RowKey ge 'a') and (RowKey lt 'b')</span></span>  

<span data-ttu-id="3a08f-507">위의 hello 예에 사용 되는 hello 필터 구문에 대 한 자세한 내용은 참조 하십시오 hello 테이블 서비스 REST API에서에서는 [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-507">Note that hello filter syntax used in hello examples above is from hello Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="3a08f-508">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3a08f-508">Issues and considerations</span></span>
<span data-ttu-id="3a08f-509">Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:</span><span class="sxs-lookup"><span data-stu-id="3a08f-509">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="3a08f-510">유지할 수 있습니다 중복 엔터티가 서로 일치 결국 hello를 사용 하 여 [결국 일관 된 트랜잭션 패턴](#eventually-consistent-transactions-pattern) toomaintain hello 기본 및 보조 인덱스 엔터티.</span><span class="sxs-lookup"><span data-stu-id="3a08f-510">You can keep your duplicate entities eventually consistent with each other by using hello [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) toomaintain hello primary and secondary index entities.</span></span>  
* <span data-ttu-id="3a08f-511">테이블 저장소 상대적으로 경제적인 toouse 이므로 중복 데이터를 저장할 경우의 오버 헤드 비용 hello 중요 한 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-511">Table storage is relatively cheap toouse so hello cost overhead of storing duplicate data should not be a major concern.</span></span> <span data-ttu-id="3a08f-512">그러나 항상 예상 되는 저장소 요구 사항에 따라 디자인의 hello 비용을 평가 하 고만 중복 항목 toosupport hello 쿼리 실행 됩니다 클라이언트 응용 프로그램을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-512">However, you should always evaluate hello cost of your design based on your anticipated storage requirements and only add duplicate entities toosupport hello queries your client application will execute.</span></span>  
* <span data-ttu-id="3a08f-513">hello에 사용 되는 값을 hello **RowKey** 각 엔터티에 대해 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-513">hello value used for hello **RowKey** must be unique for each entity.</span></span> <span data-ttu-id="3a08f-514">복합 키 값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-514">Consider using compound key values.</span></span>  
* <span data-ttu-id="3a08f-515">안쪽 여백 hello에 숫자 값 **RowKey** (예: hello 직원 id 000223) 하면 정렬 및 하한값과 상한값에 따라 필터링을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-515">Padding numeric values in hello **RowKey** (for example, hello employee id 000223), enables correct sorting and filtering based on upper and lower bounds.</span></span>  
* <span data-ttu-id="3a08f-516">반드시 불필요 tooduplicate 엔터티의 모든 hello 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-516">You do not necessarily need tooduplicate all hello properties of your entity.</span></span> <span data-ttu-id="3a08f-517">예를 들어 경우 hello 쿼리 해당 hello를 사용 하 여 조회 hello 엔터티 전자 메일 주소를 hello에 **RowKey** 필요 hello 직원의 나이, 이러한 엔터티는 다음 구조 hello 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-517">For example, if hello queries that lookup hello entities using hello email address in hello **RowKey** never need hello employee's age, these entities could have hello following structure:</span></span>
  
  ![][11]
* <span data-ttu-id="3a08f-518">일반적으로 toostore 중복 데이터를 보다 잘 하 고 사용 하 여 엔터티 toouse 하나의 쿼리 toolocate hello 보조 인덱스 보다는 단일 쿼리로 필요한 모든 hello 데이터를 검색할 수 있는 확인 및 다른 toolookup hello hello 기본 인덱스에 필요한 데이터.</span><span class="sxs-lookup"><span data-stu-id="3a08f-518">It is typically better toostore duplicate data and ensure that you can retrieve all hello data you need with a single query than toouse one query toolocate an entity using hello secondary index and another toolookup hello required data in hello primary index.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="3a08f-519">때 toouse이이 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-519">When toouse this pattern</span></span>
<span data-ttu-id="3a08f-520">이 패턴을 사용 하 여 클라이언트 응용 프로그램 클라이언트 tooretrieve 엔터티가 서로 다른 정렬 순서에 필요한 경우에 다양 한 서로 다른 키를 사용 하 여 tooretrieve 엔터티 있고 다양 한 고유 값을 사용 하 여 각 엔터티를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-520">Use this pattern when your client application needs tooretrieve entities using a variety of different keys, when your client needs tooretrieve entities in different sort orders, and where you can identify each entity using a variety of unique values.</span></span> <span data-ttu-id="3a08f-521">다른 hello를 사용 하 여 엔터티 조회를 수행 하는 경우 hello 파티션 확장성 제한을 초과 tooavoid 하려는 경우이 패턴을 사용 하 여 **RowKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-521">Use this pattern when you want tooavoid exceeding hello partition scalability limits when you are performing entity lookups using hello different **RowKey** values.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="3a08f-522">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="3a08f-522">Related patterns and guidance</span></span>
<span data-ttu-id="3a08f-523">hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3a08f-523">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="3a08f-524">결과적으로 일관성 있는 트랜잭션 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-524">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="3a08f-525">파티션 간 보조 인덱스 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-525">Intra-partition secondary index pattern</span></span>](#intra-partition-secondary-index-pattern)  
* [<span data-ttu-id="3a08f-526">복합 키 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-526">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="3a08f-527">엔터티 그룹 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="3a08f-527">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="3a08f-528">유형이 다른 엔터티 유형 작업</span><span class="sxs-lookup"><span data-stu-id="3a08f-528">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="eventually-consistent-transactions-pattern"></a><span data-ttu-id="3a08f-529">결과적으로 일관성 있는 트랜잭션 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-529">Eventually consistent transactions pattern</span></span>
<span data-ttu-id="3a08f-530">Azure 큐를 사용하여 파티션 경계 또는 저장소 시스템 경계 간에 결과적으로 일관성 있는 동작을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-530">Enable eventually consistent behavior across partition boundaries or storage system boundaries by using Azure queues.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="3a08f-531">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="3a08f-531">Context and problem</span></span>
<span data-ttu-id="3a08f-532">EGTs hello를 공유 하는 여러 엔터티 간에 원자성 트랜잭션을 사용 동일한 파티션 키입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-532">EGTs enable atomic transactions across multiple entities that share hello same partition key.</span></span> <span data-ttu-id="3a08f-533">성능 및 확장성 때문에 대 한 별도 파티션을 또는 별도 저장소 시스템 일관성 요구 사항이 있는 toostore 엔터티를 결정할 수 있습니다: 이러한 시나리오에서는 EGTs toomaintain 일관성을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-533">For performance and scalability reasons, you might decide toostore entities that have consistency requirements in separate partitions or in a separate storage system: in such a scenario, you cannot use EGTs toomaintain consistency.</span></span> <span data-ttu-id="3a08f-534">예를 들어 간의 요구 사항 toomaintain 결과적 일관성을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-534">For example, you might have a requirement toomaintain eventual consistency between:</span></span>  

* <span data-ttu-id="3a08f-535">동일한 테이블을 서로 다른 테이블의 다른 저장소 계정에서 hello에 두 개의 서로 다른 파티션에 저장 된 엔터티.</span><span class="sxs-lookup"><span data-stu-id="3a08f-535">Entities stored in two different partitions in hello same table, in different tables, in in different storage accounts.</span></span>  
* <span data-ttu-id="3a08f-536">Hello 테이블 서비스에에서 저장 된 엔터티 및 hello Blob 서비스에에서 저장 된 blob입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-536">An entity stored in hello Table service and a blob stored in hello Blob service.</span></span>  
* <span data-ttu-id="3a08f-537">파일 시스템의 hello 테이블 서비스 및 파일에 저장 하는 엔터티.</span><span class="sxs-lookup"><span data-stu-id="3a08f-537">An entity stored in hello Table service and a file in a file system.</span></span>  
* <span data-ttu-id="3a08f-538">엔터티는 hello 테이블 서비스에에서 저장 하면서 hello Azure 검색 서비스를 사용 하 여 인덱싱됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-538">An entity store in hello Table service yet indexed using hello Azure Search service.</span></span>  

#### <a name="solution"></a><span data-ttu-id="3a08f-539">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3a08f-539">Solution</span></span>
<span data-ttu-id="3a08f-540">Azure 큐를 사용하면 둘 이상의 파티션 또는 저장소 시스템 간에 결과적 일관성을 유지하는 솔루션을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-540">By using Azure queues, you can implement a solution that delivers eventual consistency across two or more partitions or storage systems.</span></span>
<span data-ttu-id="3a08f-541">tooillustrate 접근이 요구 사항 toobe 수 tooarchive 이전 employee 엔터티를 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-541">tooillustrate this approach, assume you have a requirement toobe able tooarchive old employee entities.</span></span> <span data-ttu-id="3a08f-542">이전 직원 엔터티는 거의 쿼리되지 않으므로 현재 직원을 다루는 활동에서 제외해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-542">Old employee entities are rarely queried and should be excluded from any activities that deal with current employees.</span></span> <span data-ttu-id="3a08f-543">tooimplement hello에 근무 중인 직원을 저장 하는이 요구 사항을 **현재** 테이블과 hello에 오래 된 직원 **보관** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-543">tooimplement this requirement you store active employees in hello **Current** table and old employees in hello **Archive** table.</span></span> <span data-ttu-id="3a08f-544">직원을 보관 해야 toodelete hello 엔터티로서 hello **현재** 테이블 및 엔터티 toohello hello 추가 **보관** 수 있지만 테이블을 사용할 수 없습니다 EGT tooperform 두 가지 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-544">Archiving an employee requires you toodelete hello entity from hello **Current** table and add hello entity toohello **Archive** table, but you cannot use an EGT tooperform these two operations.</span></span> <span data-ttu-id="3a08f-545">오류가 모두 또는 두 테이블에 엔터티 tooappear를 하면 tooavoid hello 위험 hello 보관 작업 결국 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-545">tooavoid hello risk that a failure causes an entity tooappear in both or neither tables, hello archive operation must be eventually consistent.</span></span> <span data-ttu-id="3a08f-546">hello 시퀀스 다이어그램을 다음 단계를 간략하게 설명 hello이이 작업에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-546">hello following sequence diagram outlines hello steps in this operation.</span></span> <span data-ttu-id="3a08f-547">자세한 내용은 예외 경로 hello 텍스트 다음에 대해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-547">More detail is provided for exception paths in hello text following.</span></span>  

![][12]

<span data-ttu-id="3a08f-548">클라이언트에서이 예제에서는 tooarchive 직원 #456 Azure 큐에서 메시지를 배치 하 여 hello 보관 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-548">A client initiates hello archive operation by placing a message on an Azure queue, in this example tooarchive employee #456.</span></span> <span data-ttu-id="3a08f-549">작업자 역할 새 메시지;에 대 한 hello 큐를 폴링합니다. 를 찾으면 hello 메시지 읽고 hello 큐에서 숨겨진된 복사본을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-549">A worker role polls hello queue for new messages; when it finds one, it reads hello message and leaves a hidden copy on hello queue.</span></span> <span data-ttu-id="3a08f-550">hello 작업자 역할 hello에서 hello 엔터티의 복사본을 다음 인출 **현재** hello에 복사본을 삽입, 테이블 **보관** 테이블 및 hello에서 원래 삭제 hello **현재**테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-550">hello worker role next fetches a copy of hello entity from hello **Current** table, inserts a copy in hello **Archive** table, and then deletes hello original from hello **Current** table.</span></span> <span data-ttu-id="3a08f-551">마지막으로, hello 이전 단계에서 오류가 발생 하지 인 경우 hello 작업자 역할 hello 큐에서 숨겨진된 hello 메시지를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-551">Finally, if there were no errors from hello previous steps, hello worker role deletes hello hidden message from hello queue.</span></span>  

<span data-ttu-id="3a08f-552">이 예제에서는 4 단계 삽입 hello 직원 hello **보관** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-552">In this example, step 4 inserts hello employee into hello **Archive** table.</span></span> <span data-ttu-id="3a08f-553">파일 시스템에 hello Blob 서비스에에서 hello 직원 tooa blob 또는 파일을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-553">It could add hello employee tooa blob in hello Blob service or a file in a file system.</span></span>  

#### <a name="recovering-from-failures"></a><span data-ttu-id="3a08f-554">오류 복구</span><span class="sxs-lookup"><span data-stu-id="3a08f-554">Recovering from failures</span></span>
<span data-ttu-id="3a08f-555">것이 중요 단계에서 작업 하는 hello **4** 및 **5** 해야 *idempotent* hello 작업자 역할 toorestart hello 보관 작업에 필요한 경우.</span><span class="sxs-lookup"><span data-stu-id="3a08f-555">It is important that hello operations in steps **4** and **5** must be *idempotent* in case hello worker role needs toorestart hello archive operation.</span></span> <span data-ttu-id="3a08f-556">단계에 대 한 hello 테이블 서비스를 사용 하는 경우 **4** "삽입 또는 교체" 작업을 사용 해야; 단계에 대 한 **5** 사용할지는 "경우 삭제 존재" 작업을 사용 하는 hello 클라이언트 라이브러리에서.</span><span class="sxs-lookup"><span data-stu-id="3a08f-556">If you are using hello Table service, for step **4** you should use an "insert or replace" operation; for step **5** you should use a "delete if exists" operation in hello client library you are using.</span></span> <span data-ttu-id="3a08f-557">다른 저장소 시스템을 사용하는 경우에는 적절한 idempotent 작업을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-557">If you are using another storage system, you must use an appropriate idempotent operation.</span></span>  

<span data-ttu-id="3a08f-558">Hello 작업자 역할 절대 단계를 완료 하는 경우 **6**, 후 시간 초과 hello 메시지 hello 큐에 다시 나타납니다. 후 작업자 역할 tootry tooreprocess hello에 대 한 해 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-558">If hello worker role never completes step **6**, then after a timeout hello message reappears on hello queue ready for hello worker role tootry tooreprocess it.</span></span> <span data-ttu-id="3a08f-559">hello 작업자 역할 hello 큐에 메시지를 읽은 횟수를 확인할 수 있습니다 및 플래그 tooa 전송 하 여 조사를 위해 "포이즌" 메시지를은 큐 구분 필요한 경우.</span><span class="sxs-lookup"><span data-stu-id="3a08f-559">hello worker role can check how many times a message on hello queue has been read and, if necessary, flag it is a "poison" message for investigation by sending it tooa separate queue.</span></span> <span data-ttu-id="3a08f-560">큐에서 제거한 횟수 큐의 메시지를 읽고 hello를 검사 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Get 메시지](https://msdn.microsoft.com/library/azure/dd179474.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-560">For more information about reading queue messages and checking hello dequeue count, see [Get Messages](https://msdn.microsoft.com/library/azure/dd179474.aspx).</span></span>  

<span data-ttu-id="3a08f-561">Hello 테이블 및 큐 서비스에서 일부 오류는 일시적인 오류 및 클라이언트 응용 프로그램에 적합 한 다시 시도 논리 toohandle 포함 되어야 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-561">Some errors from hello Table and Queue services are transient errors, and your client application should include suitable retry logic toohandle them.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="3a08f-562">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3a08f-562">Issues and considerations</span></span>
<span data-ttu-id="3a08f-563">Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:</span><span class="sxs-lookup"><span data-stu-id="3a08f-563">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="3a08f-564">이 솔루션은 트랜잭션 격리를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-564">This solution does not provide for transaction isolation.</span></span> <span data-ttu-id="3a08f-565">클라이언트 hello를 읽을 수는 예를 들어 **현재** 및 **보관** hello 작업자 역할이 단계 사이의 되었을 때 테이블 **4** 및 **5**, 참조 및 프로그램 hello 데이터의 일관성 없는 뷰.</span><span class="sxs-lookup"><span data-stu-id="3a08f-565">For example, a client could read hello **Current** and **Archive** tables when hello worker role was between steps **4** and **5**, and see an inconsistent view of hello data.</span></span> <span data-ttu-id="3a08f-566">Hello 데이터가 될 것 이라는 일관 된 결국 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-566">Note that hello data will be consistent eventually.</span></span>  
* <span data-ttu-id="3a08f-567">4-5 단계에서 순서 tooensure 결과적 일관성 idempotent 인지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-567">You must be sure that steps 4 and 5 are idempotent in order tooensure eventual consistency.</span></span>  
* <span data-ttu-id="3a08f-568">여러 큐 및 작업자 역할 인스턴스를 사용 하 여 hello 솔루션을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-568">You can scale hello solution by using multiple queues and worker role instances.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="3a08f-569">때 toouse이이 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-569">When toouse this pattern</span></span>
<span data-ttu-id="3a08f-570">여러 파티션 또는 테이블에 존재 하는 엔터티 간의 결과적 일관성 tooguarantee 하려는 경우이 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-570">Use this pattern when you want tooguarantee eventual consistency between entities that exist in different partitions or tables.</span></span> <span data-ttu-id="3a08f-571">Hello 테이블 서비스 및 hello Blob 서비스 및 기타 비 Azure 저장소 데이터 원본 데이터베이스 또는 hello 파일 시스템 등에서 작업에 대 한이 패턴 tooensure 결과적 일관성을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-571">You can extend this pattern tooensure eventual consistency for operations across hello Table service and hello Blob service and other non-Azure Storage data sources such as database or hello file system.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="3a08f-572">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="3a08f-572">Related patterns and guidance</span></span>
<span data-ttu-id="3a08f-573">hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3a08f-573">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="3a08f-574">엔터티 그룹 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="3a08f-574">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="3a08f-575">병합 또는 바꾸기</span><span class="sxs-lookup"><span data-stu-id="3a08f-575">Merge or replace</span></span>](#merge-or-replace)  

> [!NOTE]
> <span data-ttu-id="3a08f-576">트랜잭션 격리는 중요 한 tooyour 솔루션을 하는 경우 테이블 tooenable 다시 디자인 고려해 야 toouse EGTs 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-576">If transaction isolation is important tooyour solution, you should consider redesigning your tables tooenable you toouse EGTs.</span></span>  
> 
> 

### <a name="index-entities-pattern"></a><span data-ttu-id="3a08f-577">인덱스 엔터티 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-577">Index Entities Pattern</span></span>
<span data-ttu-id="3a08f-578">인덱스 엔터티 tooenable 효율적인 검색 엔터티 목록을 반환 하는 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-578">Maintain index entities tooenable efficient searches that return lists of entities.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="3a08f-579">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="3a08f-579">Context and problem</span></span>
<span data-ttu-id="3a08f-580">테이블 서비스 hello hello를 사용 하 여 엔터티를 자동으로 인덱싱됩니다 **PartitionKey** 및 **RowKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-580">hello Table service automatically indexes entities using hello **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="3a08f-581">이렇게 하면 클라이언트 응용 프로그램 tooretrieve를 효율적으로 지점 쿼리를 사용 하는 엔터티 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-581">This enables a client application tooretrieve an entity efficiently using a point query.</span></span> <span data-ttu-id="3a08f-582">예를 들어 아래에 표시 된 hello 테이블 구조를 사용 하 여 클라이언트 응용 프로그램이 효율적으로 검색할 수 개별 employee 엔터티 hello 부서 이름 및 hello 직원 id를 사용 하 여 (hello **PartitionKey** 및 **RowKey** ).</span><span class="sxs-lookup"><span data-stu-id="3a08f-582">For example, using hello table structure shown below, a client application can efficiently retrieve an individual employee entity by using hello department name and hello employee id (hello **PartitionKey** and **RowKey**).</span></span>  

![][13]

<span data-ttu-id="3a08f-583">싶다면의 employee 엔터티 목록을 성, 등의 다른 고유 하지 않은 속성의 hello 값에 따라 toobe 수 tooretrieve 효율성이 떨어지는 파티션을 사용 해야 인덱스 toolook를 사용 하지 않고 스캔 toofind 일치 항목을 직접 위로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-583">If you also want toobe able tooretrieve a list of employee entities based on hello value of another non-unique property, such as their last name, you must use a less efficient partition scan toofind matches rather than using an index toolook them up directly.</span></span> <span data-ttu-id="3a08f-584">Hello 테이블 서비스에서 보조 인덱스를 제공 하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-584">This is because hello table service does not provide secondary indexes.</span></span>  

#### <a name="solution"></a><span data-ttu-id="3a08f-585">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3a08f-585">Solution</span></span>
<span data-ttu-id="3a08f-586">위에 표시 된 직원 id 목록을 유지 관리 해야 하는 hello 엔터티 구조와 성 기준으로 tooenable 조회 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-586">tooenable lookup by last name with hello entity structure shown above, you must maintain lists of employee ids.</span></span> <span data-ttu-id="3a08f-587">Jones, 같은 특정 마지막 이름의 tooretrieve hello employee 엔터티를 원하는 경우에 먼저 성,으로 jones 이면 특정 인 직원에 대 한 hello 목록을 직원 id를 찾을 하 고 employee 엔터티를 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-587">If you want tooretrieve hello employee entities with a particular last name, such as Jones, you must first locate hello list of employee ids for employees with Jones as their last name, and then retrieve those employee entities.</span></span> <span data-ttu-id="3a08f-588">Hello 목록이 직원 id 저장 하기 위한 세 가지 옵션에는</span><span class="sxs-lookup"><span data-stu-id="3a08f-588">There are three main options for storing hello lists of employee ids:</span></span>  

* <span data-ttu-id="3a08f-589">Blob 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="3a08f-589">Use blob storage.</span></span>  
* <span data-ttu-id="3a08f-590">동일한 hello employee 엔터티를 분할 하는 hello에 인덱스 엔터티를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-590">Create index entities in hello same partition as hello employee entities.</span></span>  
* <span data-ttu-id="3a08f-591">별도의 파티션 또는 테이블에 인덱스 엔터티 만들기</span><span class="sxs-lookup"><span data-stu-id="3a08f-591">Create index entities in a separate partition or table.</span></span>  

<span data-ttu-id="3a08f-592"><u>옵션 #1: Blob 저장소 사용</u></span><span class="sxs-lookup"><span data-stu-id="3a08f-592"><u>Option #1: Use blob storage</u></span></span>  

<span data-ttu-id="3a08f-593">Hello 첫 번째 옵션에 대 한 모든 고유한 성 및 각 blob 저장소에 blob 목록을 만들면의 hello **PartitionKey** (부서) 및 **RowKey** 된 마지막는 직원에 대 한 값 (직원 id) 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-593">For hello first option, you create a blob for every unique last name, and in each blob store a list of hello **PartitionKey** (department) and **RowKey** (employee id) values for employees that have that last name.</span></span> <span data-ttu-id="3a08f-594">추가 하거나 해당 직원을 삭제할 때 hello 관련 blob의 hello 콘텐츠가 결국 hello employee 엔터티와 일치 하는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-594">When you add or delete an employee you should ensure that hello content of hello relevant blob is eventually consistent with hello employee entities.</span></span>  

<span data-ttu-id="3a08f-595"><u>옵션 2:</u> 에서 Create index 엔터티 hello 같은 파티션</span><span class="sxs-lookup"><span data-stu-id="3a08f-595"><u>Option #2:</u> Create index entities in hello same partition</span></span>  

<span data-ttu-id="3a08f-596">Hello 두 번째 옵션에 대 한 hello 다음 데이터를 저장 하는 인덱스 엔터티를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-596">For hello second option, use index entities that store hello following data:</span></span>  

![][14]

<span data-ttu-id="3a08f-597">hello **EmployeeIDs** 속성 hello 성 hello에 저장 된 직원에 대 한 직원 id 목록이 포함 **RowKey**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-597">hello **EmployeeIDs** property contains a list of employee ids for employees with hello last name stored in hello **RowKey**.</span></span>  

<span data-ttu-id="3a08f-598">hello 다음 단계에 간략하게 설명 hello 프로세스 hello 두 번째 옵션을 사용 하는 경우 새 직원을 추가 하는 경우 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-598">hello following steps outline hello process you should follow when you are adding a new employee if you are using hello second option.</span></span> <span data-ttu-id="3a08f-599">이 예제에서는 Id 000152 및 성 jones 이면 특정 hello 영업 부서의 직원을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-599">In this example, we are adding an employee with Id 000152 and a last name Jones in hello Sales department:</span></span>  

1. <span data-ttu-id="3a08f-600">Hello 인덱스 엔터티를 검색 한 **PartitionKey** 값 "Sales" 및 hello **RowKey** "Jones" 값</span><span class="sxs-lookup"><span data-stu-id="3a08f-600">Retrieve hello index entity with a **PartitionKey** value "Sales" and hello **RowKey** value "Jones."</span></span> <span data-ttu-id="3a08f-601">2 단계에서 hello이 엔터티 toouse의 ETag를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-601">Save hello ETag of this entity toouse in step 2.</span></span>  
2. <span data-ttu-id="3a08f-602">Hello 새 employee 엔터티를 삽입 하는 엔터티 그룹 트랜잭션은 (즉, 일괄 처리 작업)을 만듭니다 (**PartitionKey** "Sales" 값 및 **RowKey** "000152" 값), 업데이트 인덱스 엔터티 (hello및 **PartitionKey** "Sales" 값 및 **RowKey** "jones 이면 특정" 값) hello 새 직원 id toohello 목록 hello EmployeeIDs 필드에 추가 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-602">Create an entity group transaction (that is, a batch operation) that inserts hello new employee entity (**PartitionKey** value "Sales" and **RowKey** value "000152"), and updates hello index entity (**PartitionKey** value "Sales" and **RowKey** value "Jones") by adding hello new employee id toohello list in hello EmployeeIDs field.</span></span> <span data-ttu-id="3a08f-603">엔터티 그룹 트랜잭션에 대한 자세한 내용은 [엔터티 그룹 트랜잭션](#entity-group-transactions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a08f-603">For more information about entity group transactions, see [Entity Group Transactions](#entity-group-transactions).</span></span>  
3. <span data-ttu-id="3a08f-604">(다른 사용자가 방금 수정한 hello 인덱스 엔터티)는 낙관적 동시성 오류 때문에 실패 하면 hello 엔터티 그룹 트랜잭션은 해야 toostart 통해 1 단계부터 다시.</span><span class="sxs-lookup"><span data-stu-id="3a08f-604">If hello entity group transaction fails because of an optimistic concurrency error (someone else has just modified hello index entity), then you need toostart over at step 1 again.</span></span>  

<span data-ttu-id="3a08f-605">Hello 두 번째 옵션을 사용 하는 경우 비슷한 접근 방식을 toodeleting 직원을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-605">You can use a similar approach toodeleting an employee if you are using hello second option.</span></span> <span data-ttu-id="3a08f-606">직원의 성을 변경은 세 개의 엔터티를 업데이트 하는 엔터티 그룹 트랜잭션은 tooexecute 필요 하므로 약간 더 복잡 한: hello employee 엔터티, 이전 마지막 이름 hello에 대 한 hello 인덱스 엔터티 및 hello 새 마지막 이름에 대 한 hello 인덱스 엔터티.</span><span class="sxs-lookup"><span data-stu-id="3a08f-606">Changing an employee's last name is slightly more complex because you will need tooexecute an entity group transaction that updates three entities: hello employee entity, hello index entity for hello old last name, and hello index entity for hello new last name.</span></span> <span data-ttu-id="3a08f-607">그런 다음 낙관적 동시성을 사용 하 여 tooperform hello 업데이트를 사용할 수 있는 tooretrieve hello ETag 값 순서로 변경 하기 전에 각 엔터티를 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-607">You must retrieve each entity before making any changes in order tooretrieve hello ETag values that you can then use tooperform hello updates using optimistic concurrency.</span></span>  

<span data-ttu-id="3a08f-608">hello 다음 단계에 간략하게 설명 hello 프로세스 hello 두 번째 옵션을 사용 하는 경우 toolook 부서에서 특정된 성 가진 모든 직원으로 hello 해야 하는 경우 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-608">hello following steps outline hello process you should follow when you need toolook up all hello employees with a given last name in a department if you are using hello second option.</span></span> <span data-ttu-id="3a08f-609">이 예제에서는 hello 영업부에서 jones 이면 특정 이름 가진 모든 직원으로 hello 찾고:</span><span class="sxs-lookup"><span data-stu-id="3a08f-609">In this example, we are looking up all hello employees with last name Jones in hello Sales department:</span></span>  

1. <span data-ttu-id="3a08f-610">Hello 인덱스 엔터티를 검색 한 **PartitionKey** 값 "Sales" 및 hello **RowKey** "Jones" 값</span><span class="sxs-lookup"><span data-stu-id="3a08f-610">Retrieve hello index entity with a **PartitionKey** value "Sales" and hello **RowKey** value "Jones."</span></span>  
2. <span data-ttu-id="3a08f-611">Hello 목록이 직원 hello EmployeeIDs 필드의 Id 구문 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-611">Parse hello list of employee Ids in hello EmployeeIDs field.</span></span>  
3. <span data-ttu-id="3a08f-612">(예:가 전자 메일 주소) 이러한 직원 들의 각각에 대 한 추가 정보를 검색 hello employee 엔터티를 사용 하 여 각 **PartitionKey** "Sales" 값 및 **RowKey** 에서 값 2 단계에서 얻은 직원의 hello 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-612">If you need additional information about each of these employees (such as their email addresses), retrieve each of hello employee entities using **PartitionKey** value "Sales" and **RowKey** values from hello list of employees you obtained in step 2.</span></span>  

<span data-ttu-id="3a08f-613"><u>옵션 3:</u> 별도의 파티션 또는 테이블에 인덱스 엔터티 만들기</span><span class="sxs-lookup"><span data-stu-id="3a08f-613"><u>Option #3:</u> Create index entities in a separate partition or table</span></span>  

<span data-ttu-id="3a08f-614">Hello 세 번째 옵션에 대 한 hello 다음 데이터를 저장 하는 인덱스 엔터티를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-614">For hello third option, use index entities that store hello following data:</span></span>  

![][15]

<span data-ttu-id="3a08f-615">hello **EmployeeIDs** 속성 hello 성 hello에 저장 된 직원에 대 한 직원 id 목록이 포함 **RowKey**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-615">hello **EmployeeIDs** property contains a list of employee ids for employees with hello last name stored in hello **RowKey**.</span></span>  

<span data-ttu-id="3a08f-616">Hello 세 번째 옵션을 사용 하므로 hello employee 엔터티를를 별도 파티션으로 hello 인덱스 엔터티는 EGTs toomaintain 일관성을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-616">With hello third option, you cannot use EGTs toomaintain consistency because hello index entities are in a separate partition from hello employee entities.</span></span> <span data-ttu-id="3a08f-617">Hello 인덱스 엔터티는 결국 hello employee 엔터티와 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-617">You should ensure that hello index entities are eventually consistent with hello employee entities.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="3a08f-618">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3a08f-618">Issues and considerations</span></span>
<span data-ttu-id="3a08f-619">Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:</span><span class="sxs-lookup"><span data-stu-id="3a08f-619">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="3a08f-620">이 솔루션에 필요한 엔터티를 일치 하는 두 개 이상의 쿼리 tooretrieve: tooquery hello 인덱스 엔터티 tooobtain hello 목록은 한 **RowKey** 값, 및 다음 tooretrieve hello 목록에서 각 엔터티를 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-620">This solution requires at least two queries tooretrieve matching entities: one tooquery hello index entities tooobtain hello list of **RowKey** values, and then queries tooretrieve each entity in hello list.</span></span>  
* <span data-ttu-id="3a08f-621">개별 엔터티에 최대 크기는 1MB 옵션 #2 개이고 옵션 #3 hello 솔루션의 가정 해당 hello 목록이 있다고 지정된 성에 대 한 직원 id 되지 보다 큰 경우 1MB</span><span class="sxs-lookup"><span data-stu-id="3a08f-621">Given that an individual entity has a maximum size of 1 MB, option #2 and option #3 in hello solution assume that hello list of employee ids for any given last name is never greater than 1 MB.</span></span> <span data-ttu-id="3a08f-622">직원 id 목록은 hello 가능성이 toobe 크기가 1MB 보다 클 경우 #1 옵션을 사용 하 고 blob 저장소에 hello 인덱스 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-622">If hello list of employee ids is likely toobe greater than 1 MB in size, use option #1 and store hello index data in blob storage.</span></span>  
* <span data-ttu-id="3a08f-623">옵션 2를 사용 하는 경우 (EGTs toohandle 추가 하 고 직원, 삭제와 직원의 성을 변경 사용) 해야 지 평가할 수 트랜잭션 양이 hello는 지정한 파티션에서 hello 확장성 제한에 가까워집니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-623">If you use option #2 (using EGTs toohandle adding and deleting employees, and changing an employee's last name) you must evaluate if hello volume of transactions will approach hello scalability limits in a given partition.</span></span> <span data-ttu-id="3a08f-624">Hello 대/소문자 이면 큐 toohandle hello 업데이트를 사용 하는 결국 일관 된 솔루션 (#1 옵션이 나 옵션 3) 요청 하 고 있습니다 toostore hello employee 엔터티를를 별도 파티션으로 인덱스 엔터티 수를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-624">If this is hello case, you should consider an eventually consistent solution (option #1 or option #3) that uses queues toohandle hello update requests and enables you toostore your index entities in a separate partition from hello employee entities.</span></span>  
* <span data-ttu-id="3a08f-625">이 솔루션에서는 옵션 #2 한다고 가정 toolook를는 부서 내 성을 기준으로: tooretrieve hello 판매 부서의 성이 jones 이면 특정 직원의 목록을 원하는 예를 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-625">Option #2 in this solution assumes that you want toolook up by last name within a department: for example, you want tooretrieve a list of employees with a last name Jones in hello Sales department.</span></span> <span data-ttu-id="3a08f-626">성 jones 이면 특정 hello 전체 조직 전체에서 가진 모든 직원으로 hello toobe 수 toolook #1 옵션이 나 옵션 # 3을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-626">If you want toobe able toolook up all hello employees with a last name Jones across hello whole organization, use either option #1 or option #3.</span></span>
* <span data-ttu-id="3a08f-627">결과적 일관성을 제공 하는 큐 기반 솔루션을 구현할 수 있습니다 (hello 참조 [결국 일관 된 트랜잭션 패턴](#eventually-consistent-transactions-pattern) 자세한 세부 정보에 대 한).</span><span class="sxs-lookup"><span data-stu-id="3a08f-627">You can implement a queue-based solution that delivers eventual consistency (see hello [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) for more details).</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="3a08f-628">때 toouse이이 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-628">When toouse this pattern</span></span>
<span data-ttu-id="3a08f-629">Toolookup hello 성 jones 이면 특정 가진 모든 직원 등 공통 속성 값을 공유 하는 엔터티 집합을 원하는 경우이 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-629">Use this pattern when you want toolookup a set of entities that all share a common property value, such as all employees with hello last name Jones.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="3a08f-630">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="3a08f-630">Related patterns and guidance</span></span>
<span data-ttu-id="3a08f-631">hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3a08f-631">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="3a08f-632">복합 키 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-632">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="3a08f-633">결과적으로 일관성 있는 트랜잭션 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-633">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="3a08f-634">엔터티 그룹 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="3a08f-634">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="3a08f-635">유형이 다른 엔터티 유형 작업</span><span class="sxs-lookup"><span data-stu-id="3a08f-635">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="denormalization-pattern"></a><span data-ttu-id="3a08f-636">비정규화 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-636">Denormalization pattern</span></span>
<span data-ttu-id="3a08f-637">단일 엔터티 tooenable에서 함께 관련된 데이터를 결합 tooretrieve 모든 hello 필요한 데이터를 단일 지점 쿼리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-637">Combine related data together in a single entity tooenable you tooretrieve all hello data you need with a single point query.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="3a08f-638">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="3a08f-638">Context and problem</span></span>
<span data-ttu-id="3a08f-639">관계형 데이터베이스에 일반적으로 데이터 tooremove 중복 여러 테이블에서 데이터를 검색 하는 쿼리에서 결과 정규화 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-639">In a relational database, you typically normalize data tooremove duplication resulting in queries that retrieve data from multiple tables.</span></span> <span data-ttu-id="3a08f-640">Azure 테이블에 데이터를 표준화 하는 경우에 관련된 데이터를 여러 번 왕복 hello 클라이언트 toohello 서버 tooretrieve에서 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-640">If you normalize your data in Azure tables, you must make multiple round trips from hello client toohello server tooretrieve your related data.</span></span> <span data-ttu-id="3a08f-641">예를 들어 아래 표시 된 hello 테이블 구조와 필요한 두 라운드 트립을 tooretrieve hello 세부 정보는 부서에 대 한: 직원에 hello 관리자의 id와 다른 요청 toofetch hello 관리자의 세부 정보를 포함 하는 하나의 toofetch hello department 엔터티 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-641">For example, with hello table structure shown below you need two round trips tooretrieve hello details for a department: one toofetch hello department entity that includes hello manager's id, and then another request toofetch hello manager's details in an employee entity.</span></span>  

![][16]

#### <a name="solution"></a><span data-ttu-id="3a08f-642">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3a08f-642">Solution</span></span>
<span data-ttu-id="3a08f-643">두 개의 개별 엔터티인에 hello 데이터를 저장 하는 대신 hello 데이터를 비 정규화 하 고 hello 부서 엔터티에 hello 관리자의 세부 정보의 복사본을 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-643">Instead of storing hello data in two separate entities, denormalize hello data and keep a copy of hello manager's details in hello department entity.</span></span> <span data-ttu-id="3a08f-644">예:</span><span class="sxs-lookup"><span data-stu-id="3a08f-644">For example:</span></span>  

![][17]

<span data-ttu-id="3a08f-645">이러한 속성으로 저장 된 부서 엔터티에 이제 지점 쿼리를 사용 하 여 부서에 대해 필요한 모든 hello 세부 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-645">With department entities stored with these properties, you can now retrieve all hello details you need about a department using a point query.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="3a08f-646">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3a08f-646">Issues and considerations</span></span>
<span data-ttu-id="3a08f-647">Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:</span><span class="sxs-lookup"><span data-stu-id="3a08f-647">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="3a08f-648">일부 데이터를 두 번 저장하는 것과 관련된 약간의 비용 오버헤드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-648">There is some cost overhead associated with storing some data twice.</span></span> <span data-ttu-id="3a08f-649">hello 성능 (더 적은 요청 toohello 저장소 서비스에서 발생 함) 일반적으로 능가 이점이 hello 한계 저장소 비용이 증가 (이 비용은 부분적으로 오프셋 되 고 hello 트랜잭션 수가 감소 하 여 필요한 toofetch hello 세부 정보 부서).</span><span class="sxs-lookup"><span data-stu-id="3a08f-649">hello performance benefit (resulting from fewer requests toohello storage service) typically outweighs hello marginal increase in storage costs (and this cost is partially offset by a reduction in hello number of transactions you require toofetch hello details of a department).</span></span>  
* <span data-ttu-id="3a08f-650">관리자에 대 한 정보를 저장 하는 두 개의 엔터티를 hello hello 일관성을 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-650">You must maintain hello consistency of hello two entities that store information about managers.</span></span> <span data-ttu-id="3a08f-651">단일 원자성 트랜잭션 내에서 여러 엔터티 EGTs tooupdate를 사용 하 여 hello 일관성 문제를 처리할 수 있습니다: hello department 엔터티 및 hello 부서 관리자에 대 한 hello employee 엔터티에 hello에 저장 됩니다는 경우 같은 파티션 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-651">You can handle hello consistency issue by using EGTs tooupdate multiple entities in a single atomic transaction: in this case, hello department entity, and hello employee entity for hello department manager are stored in hello same partition.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="3a08f-652">때 toouse이이 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-652">When toouse this pattern</span></span>
<span data-ttu-id="3a08f-653">관련된 정보를 toolook를 자주 할 경우이 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-653">Use this pattern when you frequently need toolook up related information.</span></span> <span data-ttu-id="3a08f-654">이 패턴 hello 클라이언트에 필요한 tooretrieve hello 데이터를 확인 해야 하는 쿼리 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-654">This pattern reduces hello number of queries your client must make tooretrieve hello data it requires.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="3a08f-655">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="3a08f-655">Related patterns and guidance</span></span>
<span data-ttu-id="3a08f-656">hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3a08f-656">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="3a08f-657">복합 키 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-657">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="3a08f-658">엔터티 그룹 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="3a08f-658">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="3a08f-659">유형이 다른 엔터티 유형 작업</span><span class="sxs-lookup"><span data-stu-id="3a08f-659">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)

### <a name="compound-key-pattern"></a><span data-ttu-id="3a08f-660">복합 키 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-660">Compound key pattern</span></span>
<span data-ttu-id="3a08f-661">사용 하 여 복합 **RowKey** 값 tooenable 클라이언트 toolookup 관련 데이터는 단일 지점에서 쿼리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-661">Use compound **RowKey** values tooenable a client toolookup related data with a single point query.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="3a08f-662">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="3a08f-662">Context and problem</span></span>
<span data-ttu-id="3a08f-663">쿼리에서 매우 체계적 toouse 조인은 것이 관계형 데이터베이스 tooreturn 관련 단일 쿼리에서 데이터 toohello 클라이언트의 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-663">In a relational database, it is quite natural toouse joins in queries tooreturn related pieces of data toohello client in a single query.</span></span> <span data-ttu-id="3a08f-664">예를 들어 hello 직원 id toolook 성능 포함 및 해당 직원에 대 한 데이터를 검토 하는 관련 엔터티 그룹을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-664">For example, you might use hello employee id toolook up a list of related entities that contain performance and review data for that employee.</span></span>  

<span data-ttu-id="3a08f-665">Employee 엔터티를 저장 하는 구조를 다음 hello를 사용 하 여 hello 테이블 서비스에 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-665">Assume you are storing employee entities in hello Table service using hello following structure:</span></span>  

![][18]

<span data-ttu-id="3a08f-666">Tooreviews 관련 toostore 기록 데이터를 제공 해야 하 고 조직에 대 한 각 연도의 hello 직원에 대 한 성능 한 적이 toobe 수 tooaccess 연도별이 정보가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-666">You also need toostore historical data relating tooreviews and performance for each year hello employee has worked for your organization and you need toobe able tooaccess this information by year.</span></span> <span data-ttu-id="3a08f-667">한 가지 옵션은 toocreate 구조를 다음 hello로 엔터티를 저장 하는 다른 테이블:</span><span class="sxs-lookup"><span data-stu-id="3a08f-667">One option is toocreate another table that stores entities with hello following structure:</span></span>  

![][19]

<span data-ttu-id="3a08f-668">이 방법에 tooduplicate hello 새 엔터티 tooenable의 일부 정보 (예: 이름 및 성) 결정할 수 있습니다 tooretrieve 단일 요청으로 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-668">Notice that with this approach you may decide tooduplicate some information (such as first name and last name) in hello new entity tooenable you tooretrieve your data with a single request.</span></span> <span data-ttu-id="3a08f-669">그러나 원자 단위로 EGT tooupdate hello 두 엔터티를 사용할 수 없으므로 강력한 일관성을 유지할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-669">However, you cannot maintain strong consistency because you cannot use an EGT tooupdate hello two entities atomically.</span></span>  

#### <a name="solution"></a><span data-ttu-id="3a08f-670">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3a08f-670">Solution</span></span>
<span data-ttu-id="3a08f-671">새 엔터티 형식이 구조를 다음 hello로 엔터티를 사용 하 여 원본 테이블에 저장:</span><span class="sxs-lookup"><span data-stu-id="3a08f-671">Store a new entity type in your original table using entities with hello following structure:</span></span>  

![][20]

<span data-ttu-id="3a08f-672">Hello 어떻게 확인 **RowKey** 이제의 복합 키 이루어져 hello 직원 id와 수 있는 hello 검토 데이터의 hello 연도 tooretrieve 직원의 성과 hello 및 단일 엔터티에 대 한 단일 요청으로 데이터를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-672">Notice how hello **RowKey** is now a compound key made up of hello employee id and hello year of hello review data that enables you tooretrieve hello employee's performance and review data with a single request for a single entity.</span></span>  

<span data-ttu-id="3a08f-673">다음 예제는 hello (예: 000123 hello 영업 부서의 직원) 특정 직원에 대 한 모든 hello 검토 데이터를 검색 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-673">hello following example outlines how you can retrieve all hello review data for a particular employee (such as employee 000123 in hello Sales department):</span></span>  

<span data-ttu-id="3a08f-674">$filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000123') and (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments</span><span class="sxs-lookup"><span data-stu-id="3a08f-674">$filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000123') and (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="3a08f-675">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3a08f-675">Issues and considerations</span></span>
<span data-ttu-id="3a08f-676">Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:</span><span class="sxs-lookup"><span data-stu-id="3a08f-676">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="3a08f-677">쉽게 tooparse hello 있는 적합 한 구분 기호를 사용 해야 **RowKey** 값: 예를 들어 **000123_2012**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-677">You should use a suitable separator character that makes it easy tooparse hello **RowKey** value: for example, **000123_2012**.</span></span>  
* <span data-ttu-id="3a08f-678">Hello에 대 한 관련된 데이터를 포함 하는 다른 엔터티로 분할 동일 hello에이 엔터티를 저장할도 동일한 직원 이기 EGTs toomaintain 강력한 일관성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-678">You are also storing this entity in hello same partition as other entities that contain related data for hello same employee, which means you can use EGTs toomaintain strong consistency.</span></span>
* <span data-ttu-id="3a08f-679">이 패턴 적절 한지 여부를 hello 데이터 toodetermine을 쿼리 하는 빈도 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-679">You should consider how frequently you will query hello data toodetermine whether this pattern is appropriate.</span></span>  <span data-ttu-id="3a08f-680">예를 들어 액세스 하는 경우 자주 검토 데이터 hello 및 hello 주 직원 데이터 종종 별도 엔터티로 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-680">For example, if you will access hello review data infrequently and hello main employee data often you should keep them as separate entities.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="3a08f-681">때 toouse이이 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-681">When toouse this pattern</span></span>
<span data-ttu-id="3a08f-682">이 패턴을 사용 하 여 하나 toostore 하거나 이상의 관련 엔터티 쿼리 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-682">Use this pattern when you need toostore one or more related entities that you query frequently.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="3a08f-683">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="3a08f-683">Related patterns and guidance</span></span>
<span data-ttu-id="3a08f-684">hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3a08f-684">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="3a08f-685">엔터티 그룹 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="3a08f-685">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="3a08f-686">유형이 다른 엔터티 유형 작업</span><span class="sxs-lookup"><span data-stu-id="3a08f-686">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  
* [<span data-ttu-id="3a08f-687">결과적으로 일관성 있는 트랜잭션 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-687">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  

### <a name="log-tail-pattern"></a><span data-ttu-id="3a08f-688">로그 테일 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-688">Log tail pattern</span></span>
<span data-ttu-id="3a08f-689">Hello 검색  *n*  엔터티 가장 최근에 추가 된 tooa 파티션을 사용 하 여 한 **RowKey** 역방향 날짜와 시간 순서에 정렬 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-689">Retrieve hello *n* entities most recently added tooa partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="3a08f-690">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="3a08f-690">Context and problem</span></span>
<span data-ttu-id="3a08f-691">일반적인 요구 사항은 엔터티일 수 tooretrieve 가장 최근에 만든 hello, 예를 들어 hello 10 개의 가장 최근 비용 청구서 직원 제출한입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-691">A common requirement is be able tooretrieve hello most recently created entities, for example hello ten most recent expense claims submitted by an employee.</span></span> <span data-ttu-id="3a08f-692">테이블 쿼리 지원은 **$top** 작업 tooreturn hello를 먼저 쿼리  *n*  집합에서 엔터티에: 없는 해당 하는 쿼리 작업 tooreturn hello 마지막 n 개 엔터티 집합에는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-692">Table queries support a **$top** query operation tooreturn hello first *n* entities from a set: there is no equivalent query operation tooreturn hello last n entities in a set.</span></span>  

#### <a name="solution"></a><span data-ttu-id="3a08f-693">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3a08f-693">Solution</span></span>
<span data-ttu-id="3a08f-694">사용 하 여 저장소 hello 엔터티는 **RowKey** 는 자연스럽 게 반대 방향으로 정렬 합니다. 날짜/시간 순서 있으므로 hello 가장 최근 항목은 항상 hello를 사용 하 여 hello 테이블의 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-694">Store hello entities using a **RowKey** that naturally sorts in reverse date/time order by using so hello most recent entry is always hello first one in hello table.</span></span>  

<span data-ttu-id="3a08f-695">예를 들어 toobe 수 tooretrieve hello 직원 제출한 10 개의 가장 최근 비용 청구서, 현재 날짜/시간 hello에서 파생 된 역방향 눈금 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-695">For example, toobe able tooretrieve hello ten most recent expense claims submitted by an employee, you can use a reverse tick value derived from hello current date/time.</span></span> <span data-ttu-id="3a08f-696">hello 다음 C# 보여 주는 코드 예제는 한 가지 방법은 toocreate에 대 한 적합 한 "틱 반전" 값은 **RowKey** 가장 오래 된 가장 최근 toohello hello에서에서 정렬 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-696">hello following C# code sample shows one way toocreate a suitable "inverted ticks" value for a **RowKey** that sorts from hello most recent toohello oldest:</span></span>  

`string invertedTicks = string.Format("{0:D19}", DateTime.MaxValue.Ticks - DateTime.UtcNow.Ticks);`  

<span data-ttu-id="3a08f-697">Toohello 날짜/시간 값 코드 다음 hello를 사용 하 여 다시 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-697">You can get back toohello date time value using hello following code:</span></span>  

`DateTime dt = new DateTime(DateTime.MaxValue.Ticks - Int64.Parse(invertedTicks));`  

<span data-ttu-id="3a08f-698">hello 테이블 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-698">hello table query looks like this:</span></span>  

`https://myaccount.table.core.windows.net/EmployeeExpense(PartitionKey='empid')?$top=10`  

#### <a name="issues-and-considerations"></a><span data-ttu-id="3a08f-699">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3a08f-699">Issues and considerations</span></span>
<span data-ttu-id="3a08f-700">Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:</span><span class="sxs-lookup"><span data-stu-id="3a08f-700">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="3a08f-701">Hello 역방향 틱 값 앞에 오는 0으로 채움 해야 예상 대로 tooensure hello 문자열 값을 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-701">You must pad hello reverse tick value with leading zeroes tooensure hello string value sorts as expected.</span></span>  
* <span data-ttu-id="3a08f-702">Hello 확장성 목표는 파티션의 hello 수준에서 인식 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-702">You must be aware of hello scalability targets at hello level of a partition.</span></span> <span data-ttu-id="3a08f-703">핫스폿 파티션을 만들지 않도록 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="3a08f-703">Be careful not create hot spot partitions.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="3a08f-704">때 toouse이이 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-704">When toouse this pattern</span></span>
<span data-ttu-id="3a08f-705">역방향 날짜/시간 순서로 tooaccess 엔터티 필요 하거나 최근에 tooaccess hello 사용 해야 하는 경우이 패턴을 사용 하 여 엔터티를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-705">Use this pattern when you need tooaccess entities in reverse date/time order or when you need tooaccess hello most recently added entities.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="3a08f-706">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="3a08f-706">Related patterns and guidance</span></span>
<span data-ttu-id="3a08f-707">hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3a08f-707">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="3a08f-708">앞/뒤에 추가된 안티패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-708">Prepend / append anti-pattern</span></span>](#prepend-append-anti-pattern)  
* [<span data-ttu-id="3a08f-709">엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="3a08f-709">Retrieving entities</span></span>](#retrieving-entities)  

### <a name="high-volume-delete-pattern"></a><span data-ttu-id="3a08f-710">대용량 삭제 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-710">High volume delete pattern</span></span>
<span data-ttu-id="3a08f-711">동시 삭제에 대 한 모든 hello 엔터티 자체 별도 테이블에 저장 하 여 많은 양의 엔터티 hello 삭제 사용 hello 테이블을 삭제 하 여 hello 엔터티를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-711">Enable hello deletion of a high volume of entities by storing all hello entities for simultaneous deletion in their own separate table; you delete hello entities by deleting hello table.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="3a08f-712">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="3a08f-712">Context and problem</span></span>
<span data-ttu-id="3a08f-713">많은 응용 프로그램이 더 이상 필요 없는 toobe tooa 사용할 수 있는 클라이언트 응용 프로그램에는 기존 데이터를 삭제 하거나 해당 hello 응용 프로그램은 tooanother 저장 미디어를 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-713">Many applications delete old data which no longer needs toobe available tooa client application, or that hello application has archived tooanother storage medium.</span></span> <span data-ttu-id="3a08f-714">일반적으로 날짜까지 이러한 데이터를 식별: 예를 들어 60 일 이상 있는 모든 로그인 요청이의 요구 사항 toodelete 레코드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-714">You typically identify such data by a date: for example, you have a requirement toodelete records of all login requests that are more than 60 days old.</span></span>  

<span data-ttu-id="3a08f-715">Toouse hello 날짜 및 시간 hello 로그인 요청 hello에 대 한 가능한 디자인은 **RowKey**:</span><span class="sxs-lookup"><span data-stu-id="3a08f-715">One possible design is toouse hello date and time of hello login request in hello **RowKey**:</span></span>  

![][21]

<span data-ttu-id="3a08f-716">이 방법은 hello 응용 프로그램을 삽입 및 삭제를 별도 파티션으로 각 사용자에 대 한 로그인 엔터티 때문에 파티션 핫스폿에 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-716">This approach avoids partition hotspots because hello application can insert and delete login entities for each user in a separate partition.</span></span> <span data-ttu-id="3a08f-717">그러나이 방법은 많이 사용 될 수 있습니다 및 tooperform 먼저 때문에 많은 수의 엔터티가 있는 경우 시간이 오래 걸릴 table scan 순서 tooidentify에 모든 hello 엔터티 toodelete 않으며 각 이전 엔터티를 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-717">However, this approach may be costly and time consuming if you have a large number of entities because first you need tooperform a table scan in order tooidentify all hello entities toodelete, and then you must delete each old entity.</span></span> <span data-ttu-id="3a08f-718">참고 EGTs에 여러 개의 삭제 요청을 일괄 처리 하 여 hello 왕복 toohello 필요한 서버 toodelete hello 이전 엔터티 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-718">Note that you can reduce hello number of round trips toohello server required toodelete hello old entities by batching multiple delete requests into EGTs.</span></span>  

#### <a name="solution"></a><span data-ttu-id="3a08f-719">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3a08f-719">Solution</span></span>
<span data-ttu-id="3a08f-720">각 로그인 시도 날짜에 별도의 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-720">Use a separate table for each day of login attempts.</span></span> <span data-ttu-id="3a08f-721">엔터티를 삽입 하는 고 단순히 매일 한 테이블을 삭제할 경우의 질문은 기존 엔터티를 삭제 하는 경우 tooavoid 핫스폿에 위에 hello 엔터티 디자인을 사용할 수 있습니다 (단일 저장소 작업) 대신 찾기 및 수많은 삭제 개별 로그인 엔터티 매일입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-721">You can use hello entity design above tooavoid hotspots when you are inserting entities, and deleting old entities is now simply a question of deleting one table every day (a single storage operation) instead of finding and deleting hundreds and thousands of individual login entities every day.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="3a08f-722">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3a08f-722">Issues and considerations</span></span>
<span data-ttu-id="3a08f-723">Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:</span><span class="sxs-lookup"><span data-stu-id="3a08f-723">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="3a08f-724">디자인에 응용 프로그램은 특정 엔터티를 다른 데이터 또는 생성 한 집계 정보를 사용 하 여 링크를 검색 하는 등 hello 데이터를 사용 하 여 다른 방법을 지원 합니까?</span><span class="sxs-lookup"><span data-stu-id="3a08f-724">Does your design support other ways your application will use hello data such as looking up specific entities, linking with other data, or generating aggregate information?</span></span>  
* <span data-ttu-id="3a08f-725">디자인이 새 엔터티를 삽입할 때 핫스폿을 방지하나요?</span><span class="sxs-lookup"><span data-stu-id="3a08f-725">Does your design avoid hot spots when you are inserting new entities?</span></span>  
* <span data-ttu-id="3a08f-726">동일한 tooreuse를 원하는 경우 지연 hello 예상 삭제 한 후 테이블 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-726">Expect a delay if you want tooreuse hello same table name after deleting it.</span></span> <span data-ttu-id="3a08f-727">것이 더 나은 tooalways 고유한 테이블 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-727">It's better tooalways use unique table names.</span></span>  
* <span data-ttu-id="3a08f-728">Hello 테이블 서비스는 hello 액세스 패턴 및 노드에 hello 파티션을 배포 하는 동안 새 테이블을 처음 사용할 때의 몇 가지 제한 있기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-728">Expect some throttling when you first use a new table while hello Table service learns hello access patterns and distributes hello partitions across nodes.</span></span> <span data-ttu-id="3a08f-729">Toocreate 새 테이블이 필요 얼마나 자주 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-729">You should consider how frequently you need toocreate new tables.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="3a08f-730">때 toouse이이 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-730">When toouse this pattern</span></span>
<span data-ttu-id="3a08f-731">많은 양의 hello에서 삭제 해야 하는 엔터티 있는 경우이 패턴을 사용 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-731">Use this pattern when you have a high volume of entities that you must delete at hello same time.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="3a08f-732">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="3a08f-732">Related patterns and guidance</span></span>
<span data-ttu-id="3a08f-733">hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3a08f-733">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="3a08f-734">엔터티 그룹 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="3a08f-734">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="3a08f-735">엔터티 수정</span><span class="sxs-lookup"><span data-stu-id="3a08f-735">Modifying entities</span></span>](#modifying-entities)  

### <a name="data-series-pattern"></a><span data-ttu-id="3a08f-736">데이터 계열 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-736">Data series pattern</span></span>
<span data-ttu-id="3a08f-737">저장소 전체 데이터 계열에는 단일 엔터티 toominimize hello 수가 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-737">Store complete data series in a single entity toominimize hello number of requests you make.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="3a08f-738">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="3a08f-738">Context and problem</span></span>
<span data-ttu-id="3a08f-739">응용 프로그램 toostore 일련의 데이터는 일반적으로 필요 tooretrieve 한 번에 모두 일반적인 시나리오가입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-739">A common scenario is for an application toostore a series of data that it typically needs tooretrieve all at once.</span></span> <span data-ttu-id="3a08f-740">예를 들어 응용 프로그램에 각 직원 1 시간 마다 보냅니다 IM 메시지의 수를 기록 하 고 각 사용자로 보낸 메시지 수 hello 이전 24 시간 동안 정보 tooplot이를 사용 하 여 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-740">For example, your application might record how many IM messages each employee sends every hour, and then use this information tooplot how many messages each user sent over hello preceding 24 hours.</span></span> <span data-ttu-id="3a08f-741">하나의 디자인에는 각 직원에 대 한 toostore 24 엔터티 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-741">One design might be toostore 24 entities for each employee:</span></span>  

![][22]

<span data-ttu-id="3a08f-742">이 디자인에서는 있습니다 수를 쉽게 찾고 hello 응용 프로그램 tooupdate hello 메시지 개수 값 필요할 때마다 hello 엔터티 tooupdate 각 직원에 대 한 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-742">With this design, you can easily locate and update hello entity tooupdate for each employee whenever hello application needs tooupdate hello message count value.</span></span> <span data-ttu-id="3a08f-743">그러나 tooretrieve hello 정보 tooplot 차트 hello에 대 한 활동 hello 이전 24 시간, 24 엔터티를 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-743">However, tooretrieve hello information tooplot a chart of hello activity for hello preceding 24 hours, you must retrieve 24 entities.</span></span>  

#### <a name="solution"></a><span data-ttu-id="3a08f-744">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3a08f-744">Solution</span></span>
<span data-ttu-id="3a08f-745">디자인을 별도 속성 toostore hello 메시지 수와 각 시간에 대해 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-745">Use hello following design with a separate property toostore hello message count for each hour:</span></span>  

![][23]

<span data-ttu-id="3a08f-746">이 디자인에서는 특정 시간에 대 한 직원에 대 한 병합 작업 tooupdate hello 메시지 수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-746">With this design, you can use a merge operation tooupdate hello message count for an employee for a specific hour.</span></span> <span data-ttu-id="3a08f-747">이제 tooplot hello 차트 단일 엔터티에 대 한 요청을 사용 하 여 필요한 모든 hello 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-747">Now, you can retrieve all hello information you need tooplot hello chart using a request for a single entity.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="3a08f-748">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3a08f-748">Issues and considerations</span></span>
<span data-ttu-id="3a08f-749">Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:</span><span class="sxs-lookup"><span data-stu-id="3a08f-749">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="3a08f-750">전체 데이터 계열에는 단일 엔터티 (too252 속성을 있을 수 있는 엔터티)에 맞지 않는 경우 blob와 같은 대체 데이터 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-750">If your complete data series does not fit into a single entity (an entity can have up too252 properties), use an alternative data store such as a blob.</span></span>  
* <span data-ttu-id="3a08f-751">여러 클라이언트가 동시에 엔터티를 업데이트 하면 toouse hello **ETag** tooimplement 낙관적 동시성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-751">If you have multiple clients updating an entity simultaneously, you will need toouse hello **ETag** tooimplement optimistic concurrency.</span></span> <span data-ttu-id="3a08f-752">여러 클라이언트가 있는 경우 높은 경합이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-752">If you have many clients, you may experience high contention.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="3a08f-753">때 toouse이이 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-753">When toouse this pattern</span></span>
<span data-ttu-id="3a08f-754">Tooupdate 필요 하 고 개별 엔터티와 연결 된 데이터 계열을 검색 하는 경우이 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-754">Use this pattern when you need tooupdate and retrieve a data series associated with an individual entity.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="3a08f-755">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="3a08f-755">Related patterns and guidance</span></span>
<span data-ttu-id="3a08f-756">hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3a08f-756">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="3a08f-757">큰 엔터티 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-757">Large entities pattern</span></span>](#large-entities-pattern)  
* [<span data-ttu-id="3a08f-758">병합 또는 바꾸기</span><span class="sxs-lookup"><span data-stu-id="3a08f-758">Merge or replace</span></span>](#merge-or-replace)  
* <span data-ttu-id="3a08f-759">[결국 일관 된 트랜잭션 패턴](#eventually-consistent-transactions-pattern) (하는 경우를 저장 하는 hello 데이터 계열 blob)</span><span class="sxs-lookup"><span data-stu-id="3a08f-759">[Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) (if you are storing hello data series in a blob)</span></span>  

### <a name="wide-entities-pattern"></a><span data-ttu-id="3a08f-760">넓은 엔터티 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-760">Wide entities pattern</span></span>
<span data-ttu-id="3a08f-761">개 이상의 252 속성을 가진 여러 물리적 엔터티 toostore 논리적 엔터티를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-761">Use multiple physical entities toostore logical entities with more than 252 properties.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="3a08f-762">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="3a08f-762">Context and problem</span></span>
<span data-ttu-id="3a08f-763">개별 엔터티에 (hello 필수 시스템 속성은 제외) 252 개 이하의 속성이 있을 수 있습니다 및 총에서 1MB 이상 데이터를 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-763">An individual entity can have no more than 252 properties (excluding hello mandatory system properties) and cannot store more than 1 MB of data in total.</span></span> <span data-ttu-id="3a08f-764">관계형 데이터베이스에 일반적으로 얻게 hello 행 크기에 제한이 라운드 새 테이블을 추가 하 고 이들 간에 한 일 관계를 적용할 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-764">In a relational database, you would typically get round any limits on hello size of a row by adding a new table and enforcing a 1-to-1 relationship between them.</span></span>  

#### <a name="solution"></a><span data-ttu-id="3a08f-765">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3a08f-765">Solution</span></span>
<span data-ttu-id="3a08f-766">Hello 테이블 서비스를 사용 하 여 여러 엔터티 toorepresent 이상 252 속성을 가진 단일 큰 비즈니스 개체를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-766">Using hello Table service, you can store multiple entities toorepresent a single large business object with more than 252 properties.</span></span> <span data-ttu-id="3a08f-767">예를 들어 toostore hello IM 보낸 메시지 수 hello에 대 한 각 직원이 최근 365 일간의 수를 원하는 경우 스키마가 서로 다른 두 개의 엔터티를 사용 하 여 디자인 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-767">For example, if you want toostore a count of hello number of IM messages sent by each employee for hello last 365 days, you could use hello following design that uses two entities with different schemas:</span></span>  

![][24]

<span data-ttu-id="3a08f-768">Toomake 서로 동기화 하는 두 엔터티 tookeep를 업데이트 해야 하는 변경 해야 할 경우에 EGT를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-768">If you need toomake a change that requires updating both entities tookeep them synchronized with each other you can use an EGT.</span></span> <span data-ttu-id="3a08f-769">그렇지 않으면 특정 한 날에 대 한 단일 병합 작업 tooupdate hello 메시지 수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-769">Otherwise, you can use a single merge operation tooupdate hello message count for a specific day.</span></span> <span data-ttu-id="3a08f-770">데이터를 함께 사용 하는 두 개의 효율적인 요청과 함께 수행할 수 있는 두 엔터티를 검색 해야 하는 개별 직원에 대 한 hello 모든 tooretrieve는 **PartitionKey** 및 **RowKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-770">tooretrieve all hello data for an individual employee you must retrieve both entities, which you can do with two efficient requests that use both a **PartitionKey** and a **RowKey** value.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="3a08f-771">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3a08f-771">Issues and considerations</span></span>
<span data-ttu-id="3a08f-772">Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:</span><span class="sxs-lookup"><span data-stu-id="3a08f-772">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="3a08f-773">두 개 이상의 저장소 트랜잭션 관련 완료 하는 논리적 엔터티를 검색: 하나의 tooretrieve 실제 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-773">Retrieving a complete logical entity involves at least two storage transactions: one tooretrieve each physical entity.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="3a08f-774">때 toouse이이 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-774">When toouse this pattern</span></span>
<span data-ttu-id="3a08f-775">테이블 서비스 필요 toostore 엔터티 크기 또는 다양 한 속성이 있는 hello에 개별 엔터티에 대해 hello 제한을 초과 하는 경우이 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-775">Use this pattern when  need toostore entities whose size or number of properties exceeds hello limits for an individual entity in hello Table service.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="3a08f-776">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="3a08f-776">Related patterns and guidance</span></span>
<span data-ttu-id="3a08f-777">hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3a08f-777">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="3a08f-778">엔터티 그룹 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="3a08f-778">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="3a08f-779">병합 또는 바꾸기</span><span class="sxs-lookup"><span data-stu-id="3a08f-779">Merge or replace</span></span>](#merge-or-replace)

### <a name="large-entities-pattern"></a><span data-ttu-id="3a08f-780">큰 엔터티 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-780">Large entities pattern</span></span>
<span data-ttu-id="3a08f-781">Blob 저장소 toostore 큰 속성 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-781">Use blob storage toostore large property values.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="3a08f-782">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="3a08f-782">Context and problem</span></span>
<span data-ttu-id="3a08f-783">개별 엔터티는 총 1MB가 넘는 데이터를 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-783">An individual entity cannot store more than 1 MB of data in total.</span></span> <span data-ttu-id="3a08f-784">사용자 속성 중 하나 또는 여러 hello 엔터티 tooexceed의 총 크기가이 값을 발생 시킨 값을 저장, hello 테이블 서비스에에서 hello 전체 엔터티를 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-784">If one or several of your properties store values that cause hello total size of your entity tooexceed this value, you cannot store hello entire entity in hello Table service.</span></span>  

#### <a name="solution"></a><span data-ttu-id="3a08f-785">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3a08f-785">Solution</span></span>
<span data-ttu-id="3a08f-786">많은 양의 데이터를 포함 하는 하나 이상의 속성 때문에 크기가 1MB를 초과 하는 엔터티를 하는 경우에 hello Blob 서비스에에서 데이터를 저장 및 다음 hello 엔터티 속성에 hello blob의 hello 주소를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-786">If your entity exceeds 1 MB in size because one or more properties contain a large amount of data, you can store data in hello Blob service and then store hello address of hello blob in a property in hello entity.</span></span> <span data-ttu-id="3a08f-787">직원의 hello 사진 blob 저장소에 저장 하 고 링크 toohello 사진 hello에 저장할 수 예를 들어 **사진** employee 엔터티의 속성:</span><span class="sxs-lookup"><span data-stu-id="3a08f-787">For example, you can store hello photo of an employee in blob storage and store a link toohello photo in hello **Photo** property of your employee entity:</span></span>  

![][25]

#### <a name="issues-and-considerations"></a><span data-ttu-id="3a08f-788">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3a08f-788">Issues and considerations</span></span>
<span data-ttu-id="3a08f-789">Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:</span><span class="sxs-lookup"><span data-stu-id="3a08f-789">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="3a08f-790">Blob 서비스 hello hello 데이터와 hello 테이블 서비스의에서 hello 엔터티 간에 toomaintain 결과적 일관성 hello를 사용 하 여 [결국 일관 된 트랜잭션 패턴](#eventually-consistent-transactions-pattern) toomaintain 사용자 엔터티.</span><span class="sxs-lookup"><span data-stu-id="3a08f-790">toomaintain eventual consistency between hello entity in hello Table service and hello data in hello Blob service, use hello [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) toomaintain your entities.</span></span>
* <span data-ttu-id="3a08f-791">두 개 이상의 저장소 트랜잭션 포함를 전체 엔터티에 검색: 하나의 tooretrieve hello 엔터티와 하나의 tooretrieve hello blob 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-791">Retrieving a complete entity involves at least two storage transactions: one tooretrieve hello entity and one tooretrieve hello blob data.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="3a08f-792">때 toouse이이 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-792">When toouse this pattern</span></span>
<span data-ttu-id="3a08f-793">Toostore 엔터티 필요에 따라 크기가 hello 테이블 서비스에 개별 엔터티에 대해 hello 제한을 초과 해야 하는 경우이 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-793">Use this pattern when you need toostore entities whose size exceeds hello limits for an individual entity in hello Table service.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="3a08f-794">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="3a08f-794">Related patterns and guidance</span></span>
<span data-ttu-id="3a08f-795">hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3a08f-795">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="3a08f-796">결과적으로 일관성 있는 트랜잭션 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-796">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="3a08f-797">넓은 엔터티 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-797">Wide entities pattern</span></span>](#wide-entities-pattern)

<a name="prepend-append-anti-pattern"></a>

### <a name="prependappend-anti-pattern"></a><span data-ttu-id="3a08f-798">앞에 추가/뒤에 추가 안티패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-798">Prepend/append anti-pattern</span></span>
<span data-ttu-id="3a08f-799">여러 파티션에서 hello 삽입 분배 하 여 많은 양의 삽입이 있는 경우 확장성 향상.</span><span class="sxs-lookup"><span data-stu-id="3a08f-799">Increase scalability when you have a high volume of inserts by spreading hello inserts across multiple partitions.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="3a08f-800">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="3a08f-800">Context and problem</span></span>
<span data-ttu-id="3a08f-801">먼저 새 엔터티 toohello을 추가 하는 hello 응용 프로그램으로 인해 일반적으로 엔터티 tooyour 저장 된 엔터티를 추가 또는 앞에 추가 되거나 파티션을 파티션 시퀀스의 마지막 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-801">Prepending or appending entities tooyour stored entities typically results in hello application adding new entities toohello first or last partition of a sequence of partitions.</span></span> <span data-ttu-id="3a08f-802">이 경우 언제 든 지 hello 삽입의 모든 hello 테이블 서비스 부하 분산 되지 않도록 하 한 핫스폿을 생성 하는 동일한 파티션을 여러 노드에서 삽입 hello에서 수행 되며 사용자 응용 프로그램 toohit hello 확장성을 일으킬 수 있는 파티션에 대 한 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-802">In this case, all of hello inserts at any given time are taking place in hello same partition, creating a hotspot that prevents hello table service from load balancing inserts across multiple nodes, and possibly causing your application toohit hello scalability targets for partition.</span></span> <span data-ttu-id="3a08f-803">예를 들어 될 수 있는 엔터티 구조 아래와 같이 다음 직원이, 로그 네트워크 및 리소스에 액세스 하는 응용 프로그램이 있는 경우 hello 트랜잭션 양이 hello에 대 한 hello 확장성 목표에 도달 하면 핫스폿 되 고 현재 시간 파티션 개별 파티션:</span><span class="sxs-lookup"><span data-stu-id="3a08f-803">For example, if you have an application that logs network and resource access by employees, then an entity structure as shown below could result in hello current hour's partition becoming a hotspot if hello volume of transactions reaches hello scalability target for an individual partition:</span></span>  

![][26]

#### <a name="solution"></a><span data-ttu-id="3a08f-804">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3a08f-804">Solution</span></span>
<span data-ttu-id="3a08f-805">hello 다음과 같은 대체 엔터티 구조 방지 특정 파티션의에서 핫스폿을 hello 응용 프로그램 로그 이벤트로 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-805">hello following alternative entity structure avoids a hotspot on any particular partition as hello application logs events:</span></span>  

![][27]

<span data-ttu-id="3a08f-806">확인이 예제와 둘 다 hello **PartitionKey** 및 **RowKey** 복합 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-806">Notice with this example how both hello **PartitionKey** and **RowKey** are compound keys.</span></span> <span data-ttu-id="3a08f-807">hello **PartitionKey** 여러 파티션에서 hello 부서 및 직원 id toodistribute hello 로깅을 모두 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-807">hello **PartitionKey** uses both hello department and employee id toodistribute hello logging across multiple partitions.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="3a08f-808">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3a08f-808">Issues and considerations</span></span>
<span data-ttu-id="3a08f-809">Hello 지점을 결정할 때 다음 고려 어떻게 tooimplement이이 패턴:</span><span class="sxs-lookup"><span data-stu-id="3a08f-809">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="3a08f-810">hello 대체 키 구조 쿼리를 만드는 핫 파티션을 insert에 효율적으로 지원 hello 방지 하는 클라이언트 응용 프로그램에서는?</span><span class="sxs-lookup"><span data-stu-id="3a08f-810">Does hello alternative key structure that avoids creating hot partitions on inserts efficiently support hello queries your client application makes?</span></span>  
* <span data-ttu-id="3a08f-811">트랜잭션의 예상된 볼륨 가능성이 tooreach 개별 파티션에 대 한 hello 확장성 목표는 hello 저장소 서비스에 의해 스로틀 된 것을 의미 합니까?</span><span class="sxs-lookup"><span data-stu-id="3a08f-811">Does your anticipated volume of transactions mean that you are likely tooreach hello scalability targets for an individual partition and be throttled by hello storage service?</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="3a08f-812">때 toouse이이 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-812">When toouse this pattern</span></span>
<span data-ttu-id="3a08f-813">트랜잭션 볼륨 가능성이 tooresult 핫 파티션을 액세스할 때 hello 저장소 서비스에 의해 제한 되 면 hello 앞에 추가 하 고 추가 안티패턴을 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="3a08f-813">Avoid hello prepend/append anti-pattern when your volume of transactions is likely tooresult in throttling by hello storage service when you access a hot partition.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="3a08f-814">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="3a08f-814">Related patterns and guidance</span></span>
<span data-ttu-id="3a08f-815">hello 다음 패턴 및 지침은 수도 관련이 패턴을 구현 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3a08f-815">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="3a08f-816">복합 키 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-816">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="3a08f-817">로그 테일 패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-817">Log tail pattern</span></span>](#log-tail-pattern)  
* [<span data-ttu-id="3a08f-818">엔터티 수정</span><span class="sxs-lookup"><span data-stu-id="3a08f-818">Modifying entities</span></span>](#modifying-entities)  

### <a name="log-data-anti-pattern"></a><span data-ttu-id="3a08f-819">로그 데이터 안티패턴</span><span class="sxs-lookup"><span data-stu-id="3a08f-819">Log data anti-pattern</span></span>
<span data-ttu-id="3a08f-820">일반적으로 hello 테이블 서비스 toostore 로그 데이터 대신 hello Blob 서비스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-820">Typically, you should use hello Blob service instead of hello Table service toostore log data.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="3a08f-821">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="3a08f-821">Context and problem</span></span>
<span data-ttu-id="3a08f-822">로그 데이터는 tooretrieve 특정 날짜/시간 범위에 대 한 로그 항목의 선택에 대 한 일반적인 사용 사례: 응용 프로그램 로그 15시 04분 및 15:06 특정 날짜에 시작 하는 중요 한 메시지와 오류 hello 모든 toofind 원하는 예를 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-822">A common use case for log data is tooretrieve a selection of log entries for a specific date/time range: for example, you want toofind all hello error and critical messages that your application logged between 15:04 and 15:06 on a specific date.</span></span> <span data-ttu-id="3a08f-823">Toouse hello 날짜 및 시간 파티션의 hello 로그 메시지 toodetermine hello에 로그 항목을 저장 하지 않을:는 핫 분할에 대 한 결과 모든 hello 로그 엔터티 어느 시점에 공유 하 게 되므로 hello 동일 **PartitionKey** 값 (hello 섹션을 참조 [Prepend/추가 안티패턴](#prepend-append-anti-pattern)).</span><span class="sxs-lookup"><span data-stu-id="3a08f-823">You do not want toouse hello date and time of hello log message toodetermine hello partition you save log entities to: that results in a hot partition because at any given time, all hello log entities will share hello same **PartitionKey** value (see hello section [Prepend/append anti-pattern](#prepend-append-anti-pattern)).</span></span> <span data-ttu-id="3a08f-824">예를 들어 hello 응용 프로그램 toohello 파티션 hello 현재 날짜 및 시간에 대 한 모든 로그 메시지를 기록 하기 때문에 로그 메시지에 대 한 엔터티 스키마를 따르는 hello 핫 분할에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-824">For example, hello following entity schema for a log message results in a hot partition because hello application writes all log messages toohello partition for hello current date and hour:</span></span>  

![][28]

<span data-ttu-id="3a08f-825">이 예제에서는 hello **RowKey** 날짜/시간 순서 대로 정렬 된 로그 메시지를 저장 하는 hello 로그 메시지 tooensure의 hello 날짜 및 시간을 포함 하 고 여러 로그 메시지 hello 동일한 날짜 및 시간을 공유 하는 경우 메시지 id를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-825">In this example, hello **RowKey** includes hello date and time of hello log message tooensure that log messages are stored sorted in date/time order, and includes a message id in case multiple log messages share hello same date and time.</span></span>  

<span data-ttu-id="3a08f-826">또 다른 방법은 toouse는 **PartitionKey** 검색이 설정 되어 hello 응용 프로그램 파티션의 범위 전체에서 메시지를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-826">Another approach is toouse a **PartitionKey** that ensures that hello application writes messages across a range of partitions.</span></span> <span data-ttu-id="3a08f-827">예를 들어 hello 소스 hello 로그 메시지의 여러 파티션에서 방법을 toodistribute 메시지를 제공, 엔터티 스키마를 따르는 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-827">For example, if hello source of hello log message provides a way toodistribute messages across many partitions, you could use hello following entity schema:</span></span>  

![][29]

<span data-ttu-id="3a08f-828">그러나 hello 문제가이 스키마는 로그 메시지는 특정 시간 범위를 검색 해야 hello 모든 해당 tooretrieve hello 테이블의 모든 파티션에 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-828">However, hello problem with this schema is that tooretrieve all hello log messages for a specific time span you must search every partition in hello table.</span></span>

#### <a name="solution"></a><span data-ttu-id="3a08f-829">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3a08f-829">Solution</span></span>
<span data-ttu-id="3a08f-830">hello 이전 섹션 강조 표시 된 hello 문제 toouse 시도의 hello 테이블 서비스 toostore 로그 항목 두 불만족 제안, 디자인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-830">hello previous section highlighted hello problem of trying toouse hello Table service toostore log entries and suggested two, unsatisfactory, designs.</span></span> <span data-ttu-id="3a08f-831">로그 메시지를 작성 하는 성능 저하의 hello 위험을이 어 졌는 한 가지 해결 tooa 핫 파티션 hello 다른 솔루션으로 인해 쿼리 성능 저하 hello 요구 사항 tooscan 때문에 특정 시간 범위에 대 한 hello tooretrieve 로그 메시지를 테이블에서 모든 파티션 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-831">One solution led tooa hot partition with hello risk of poor performance writing log messages; hello other solution resulted in poor query performance because of hello requirement tooscan every partition in hello table tooretrieve log messages for a specific time span.</span></span> <span data-ttu-id="3a08f-832">Blob 저장소 이러한 종류의 시나리오에 대 한 더 나은 솔루션 소개 하며이 어떻게 Azure Storage Analytics hello 로그 데이터를 저장을 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-832">Blob storage offers a better solution for this type of scenario and this is how Azure Storage Analytics stores hello log data it collects.</span></span>  

<span data-ttu-id="3a08f-833">이 섹션에서는 Storage Analytics 저장 하는 방법을 로그 데이터를 blob 저장소에 이러한 접근 방식 toostoring 데이터 범위 내에서 일반적으로 쿼리 하는 그림으로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-833">This section outlines how Storage Analytics stores log data in blob storage as an illustration of this approach toostoring data that you typically query by range.</span></span>  

<span data-ttu-id="3a08f-834">Storage Analytics는 로그 메시지를 구분 기호로 분리된 형식으로 여러 Blob에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-834">Storage Analytics stores log messages in a delimited format in multiple blobs.</span></span> <span data-ttu-id="3a08f-835">hello 구분 기호로 분리 된 형식을 사용 하면 쉽게 클라이언트에 대 한 응용 프로그램 tooparse hello 데이터 hello 로그 메시지에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-835">hello delimited format makes it easy for a client application tooparse hello data in hello log message.</span></span>  

<span data-ttu-id="3a08f-836">Storage Analytics는 검색 하려는 hello 로그 메시지를 포함 하는 toolocate hello blob (또는 blob) 사용 하면 blob에 대 한 명명 규칙을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-836">Storage Analytics uses a naming convention for blobs that enables you toolocate hello blob (or blobs) that contain hello log messages for which you are searching.</span></span> <span data-ttu-id="3a08f-837">예를 들어 "queue/2014/07/31/1800/000001.log" 라는 blob는 2014 년 7 월 31 일 18시 시작 하는 hello 시간에 대 한 toohello 큐 서비스와 관련 된 로그 메시지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-837">For example, a blob named "queue/2014/07/31/1800/000001.log" contains log messages that relate toohello queue service for hello hour starting at 18:00 on 31 July 2014.</span></span> <span data-ttu-id="3a08f-838">"000001" hello이이 기간에 대 한 hello 첫 번째 로그 파일 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-838">hello "000001" indicates that this is hello first log file for this period.</span></span> <span data-ttu-id="3a08f-839">저장소 분석 또한 hello의 hello 타임 스탬프를 먼저 기록 및 마지막 hello blob의 메타 데이터의 일부로 hello 파일에 저장 된 메시지를 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-839">Storage Analytics also records hello timestamps of hello first and last log messages stored in hello file as part of hello blob's metadata.</span></span> <span data-ttu-id="3a08f-840">blob 저장소 이름 접두사에 따라 컨테이너에서 blob를 찾을 수 있습니다에 대 한 API hello: toolocate 큐를 포함 하는 모든 hello blob 데이터 18시 시작 하는 hello 시간에 대 한 로그, hello 접두사 "큐/2014/07/31/1800."를 사용할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="3a08f-840">hello API for blob storage enables you locate blobs in a container based on a name prefix: toolocate all hello blobs that contain queue log data for hello hour starting at 18:00, you can use hello prefix "queue/2014/07/31/1800."</span></span>  

<span data-ttu-id="3a08f-841">저장소 분석 로그 메시지를 내부적으로 버퍼링 하 고 hello 적절 한 blob를 정기적으로 업데이트 하거나 로그 항목의 최신 배치 hello로 새 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-841">Storage Analytics buffers log messages internally and then periodically updates hello appropriate blob or creates a new one with hello latest batch of log entries.</span></span> <span data-ttu-id="3a08f-842">Hello 수를 줄일 수이 쓰기 toohello blob 서비스 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-842">This reduces hello number of writes it must perform toohello blob service.</span></span>  

<span data-ttu-id="3a08f-843">Toomanage 안정성 (발생 하는 대로 모든 로그 항목 tooblob 저장소 쓰기) 및 비용 및 확장성 사이의 절충 값 hello 하는 방법을 고려해 야 사용자 응용 프로그램에서 유사한 솔루션을 구현 하는 경우 (응용 프로그램에서 업데이트를 버퍼링 하 고 tooblob 저장소에에서 작성 일괄 처리).</span><span class="sxs-lookup"><span data-stu-id="3a08f-843">If you are implementing a similar solution in your own application, you must consider how toomanage hello trade-off between reliability (writing every log entry tooblob storage as it happens) and cost and scalability (buffering updates in your application and writing them tooblob storage in batches).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="3a08f-844">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3a08f-844">Issues and considerations</span></span>
<span data-ttu-id="3a08f-845">Hello 포인트 toostore 데이터를 기록 하는 방법을 결정할 때 다음을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-845">Consider hello following points when deciding how toostore log data:</span></span>  

* <span data-ttu-id="3a08f-846">잠재적 핫 파티션을 방지하는 테이블 디자인을 만든 경우 로그 데이터에 효율적으로 액세스할 수 없는 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-846">If you create a table design that avoids potential hot partitions, you may find that you cannot access your log data efficiently.</span></span>  
* <span data-ttu-id="3a08f-847">tooprocess 로그 데이터, 클라이언트 종종 필요한 tooload 레코드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-847">tooprocess log data, a client often needs tooload many records.</span></span>  
* <span data-ttu-id="3a08f-848">로그 데이터는 구조화된 경우가 많지만 Blob 저장소가 더 나은 솔루션일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-848">Although log data is often structured, blob storage may be a better solution.</span></span>  

### <a name="implementation-considerations"></a><span data-ttu-id="3a08f-849">구현 고려 사항</span><span class="sxs-lookup"><span data-stu-id="3a08f-849">Implementation considerations</span></span>
<span data-ttu-id="3a08f-850">이 섹션 hello 이전 섹션에 설명 된 hello 패턴을 구현할 때 설명 염두에서 hello 고려 사항 toobear 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-850">This section discusses some of hello considerations toobear in mind when you implement hello patterns described in hello previous sections.</span></span> <span data-ttu-id="3a08f-851">이 섹션의 대부분 hello 저장소 클라이언트 라이브러리 (버전 4.3.0 hello 작성 시점에)를 사용 하는 C#으로 작성 된 예제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-851">Most of this section uses examples written in C# that use hello Storage Client Library (version 4.3.0 at hello time of writing).</span></span>  

### <a name="retrieving-entities"></a><span data-ttu-id="3a08f-852">엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="3a08f-852">Retrieving entities</span></span>
<span data-ttu-id="3a08f-853">Hello 섹션에서 설명한 대로 [를 쿼리 하기 위한 디자인](#design-for-querying), hello 가장 효율적인 쿼리는 지점 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-853">As discussed in hello section [Design for querying](#design-for-querying), hello most efficient query is a point query.</span></span> <span data-ttu-id="3a08f-854">그러나 일부 시나리오에서 할 수 있습니다 tooretrieve 여러 엔터티.</span><span class="sxs-lookup"><span data-stu-id="3a08f-854">However, in some scenarios you may need tooretrieve multiple entities.</span></span> <span data-ttu-id="3a08f-855">이 섹션에서는 hello 저장소 클라이언트 라이브러리를 사용 하 여 몇 가지 일반적인 접근 방식을 tooretrieving 엔터티를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-855">This section describes some common approaches tooretrieving entities using hello Storage Client Library.</span></span>  

#### <a name="executing-a-point-query-using-hello-storage-client-library"></a><span data-ttu-id="3a08f-856">Hello 저장소 클라이언트 라이브러리를 사용 하 여 지점 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-856">Executing a point query using hello Storage Client Library</span></span>
<span data-ttu-id="3a08f-857">hello 가장 쉬운 방법은 tooexecute 지점 쿼리는 toouse hello **검색** 로 엔터티를 검색 하는 hello 다음 C# 코드 조각에에서 나와 있는 것 처럼 작업 테이블을 **PartitionKey** 값 "Sales"와  **RowKey** "212" 값의:</span><span class="sxs-lookup"><span data-stu-id="3a08f-857">hello easiest way tooexecute a point query is toouse hello **Retrieve** table operation as shown in hello following C# code snippet that retrieves an entity with a **PartitionKey** of value "Sales" and a **RowKey** of value "212":</span></span>  

```csharp
TableOperation retrieveOperation = TableOperation.Retrieve<EmployeeEntity>("Sales", "212");
var retrieveResult = employeeTable.Execute(retrieveOperation);
if (retrieveResult.Result != null)
{
    EmployeeEntity employee = (EmployeeEntity)retrieveResult.Result;
    ...
}  
```

<span data-ttu-id="3a08f-858">이 예제에서는 hello 엔터티를 예상 하는 방법을 확인 형식의 toobe 검색 **EmployeeEntity**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-858">Notice how this example expects hello entity it retrieves toobe of type **EmployeeEntity**.</span></span>  

#### <a name="retrieving-multiple-entities-using-linq"></a><span data-ttu-id="3a08f-859">LINQ를 사용하여 여러 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="3a08f-859">Retrieving multiple entities using LINQ</span></span>
<span data-ttu-id="3a08f-860">저장소 클라이언트 라이브러리와 함께 LINQ를 사용하고 **where** 절이 있는 쿼리를 지정하여 여러 엔터티를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-860">You can retrieve multiple entities by using LINQ with Storage Client Library and specifying a query with a **where** clause.</span></span> <span data-ttu-id="3a08f-861">테이블 검색 tooavoid 항상 포함 해야 hello **PartitionKey** hello에 대 한 값 여기서 절, 가능한 경우 hello 및 **RowKey** tooavoid 테이블 및 파티션 검색 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-861">tooavoid a table scan, you should always include hello **PartitionKey** value in hello where clause, and if possible hello **RowKey** value tooavoid table and partition scans.</span></span> <span data-ttu-id="3a08f-862">hello 테이블 서비스에서는 제한 된 비교 연산자 (보다 큼, 보다 큰 또는 같음, 보다 작음, 작거나 또는, 같음, 같고 같지 않음) toouse 집합이 hello 여기서 절.</span><span class="sxs-lookup"><span data-stu-id="3a08f-862">hello table service supports a limited set of comparison operators (greater than, greater than or equal, less than, less than or equal, equal, and not equal) toouse in hello where clause.</span></span> <span data-ttu-id="3a08f-863">hello 다음 C# 코드 조각은 직원을 찾습니다 모든 hello "B" 인 마지막 이름은 시작 (해당 hello 가정 **RowKey** 저장소 hello 성) hello 영업 부서의 (hello 가정 **PartitionKey** 저장소 hello 부서 이름):</span><span class="sxs-lookup"><span data-stu-id="3a08f-863">hello following C# code snippet finds all hello employees whose last name starts with "B" (assuming that hello **RowKey** stores hello last name) in hello sales department (assuming hello **PartitionKey** stores hello department name):</span></span>  

```csharp
TableQuery<EmployeeEntity> employeeQuery = employeeTable.CreateQuery<EmployeeEntity>();
var query = (from employee in employeeQuery
            where employee.PartitionKey == "Sales" &&
            employee.RowKey.CompareTo("B") >= 0 &&
            employee.RowKey.CompareTo("C") < 0
            select employee).AsTableQuery();
var employees = query.Execute();  
```

<span data-ttu-id="3a08f-864">Hello 쿼리 둘 다 지정 방법을 **RowKey** 및 **PartitionKey** tooensure 성능을 향상 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-864">Notice how hello query specifies both a **RowKey** and a **PartitionKey** tooensure better performance.</span></span>  

<span data-ttu-id="3a08f-865">hello 다음 보여 주는 코드 예제 hello fluent API를 사용 하 여 해당 하는 기능 (fluent Api에 대 한 자세한 내용은 참조 일반적으로 [Fluent API를 디자인 하기 위한 모범 사례](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):</span><span class="sxs-lookup"><span data-stu-id="3a08f-865">hello following code sample shows equivalent functionality using hello fluent API (for more information about fluent APIs in general, see [Best Practices for Designing a Fluent API](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):</span></span>  

```csharp
TableQuery<EmployeeEntity> employeeQuery = new TableQuery<EmployeeEntity>().Where(
    TableQuery.CombineFilters(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition(
    "PartitionKey", QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.GenerateFilterCondition(
    "RowKey", QueryComparisons.GreaterThanOrEqual, "B")
),
TableOperators.And,
TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "C")
    )
);
var employees = employeeTable.ExecuteQuery(employeeQuery);  
```

> [!NOTE]
> <span data-ttu-id="3a08f-866">hello 샘플 중첩 여러 **CombineFilters** 메서드 tooinclude hello 세 개의 필터 조건을 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-866">hello sample nests multiple **CombineFilters** methods tooinclude hello three filter conditions.</span></span>  
> 
> 

#### <a name="retrieving-large-numbers-of-entities-from-a-query"></a><span data-ttu-id="3a08f-867">쿼리에서 여러 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="3a08f-867">Retrieving large numbers of entities from a query</span></span>
<span data-ttu-id="3a08f-868">최적의 쿼리는 **PartitionKey** 값과 **RowKey** 값을 기반으로 개별 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-868">An optimal query returns an individual entity based on a **PartitionKey** value and a **RowKey** value.</span></span> <span data-ttu-id="3a08f-869">그러나 일부 시나리오에서 할 수 있습니다 요구 사항 tooreturn 파티션 같거나 여러 파티션을 포함 하 여 hello에서 많은 엔터티.</span><span class="sxs-lookup"><span data-stu-id="3a08f-869">However, in some scenarios you may have a requirement tooreturn many entities from hello same partition or even from many partitions.</span></span>  

<span data-ttu-id="3a08f-870">이러한 시나리오에서는 응용 프로그램의 성능을 hello를 항상 완벽 하 게 테스트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-870">You should always fully test hello performance of your application in such scenarios.</span></span>  

<span data-ttu-id="3a08f-871">Hello 테이블 서비스에 대 한 쿼리 1,000 엔터티 최대 한 번에 반환할 수 있으며 최대 5 초 동안 실행 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-871">A query against hello table service may return a maximum of 1,000 entities at one time and may execute for a maximum of five seconds.</span></span> <span data-ttu-id="3a08f-872">연속 토큰 tooenable 클라이언트 응용 프로그램 toorequest hello hello hello 결과 집합에 포함 된 1, 000 개 엔터티, hello 쿼리가 5 초 안에 완료 되지 않은 논리값이 hello 쿼리 hello 파티션 경계를 교차 하는 경우 hello 테이블 서비스 다음 엔터티 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-872">If hello result set contains more than 1,000 entities, if hello query did not complete within five seconds, or if hello query crosses hello partition boundary, hello Table service returns a continuation token tooenable hello client application toorequest hello next set of entities.</span></span> <span data-ttu-id="3a08f-873">연속 토큰의 작동 방식에 대한 자세한 내용은 [쿼리 제한 시간 및 페이지 번호 매김](http://msdn.microsoft.com/library/azure/dd135718.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a08f-873">For more information about how continuation tokens work, see [Query Timeout and Pagination](http://msdn.microsoft.com/library/azure/dd135718.aspx).</span></span>  

<span data-ttu-id="3a08f-874">Hello 저장소 클라이언트 라이브러리를 사용 하는 경우 자동으로 처리할 수 연속 토큰 드립니다 hello 테이블 서비스에서에서 엔터티를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-874">If you are using hello Storage Client Library, it can automatically handle continuation tokens for you as it returns entities from hello Table service.</span></span> <span data-ttu-id="3a08f-875">hello 다음 C# 코드 샘플 hello 저장소 클라이언트 라이브러리를 자동으로 사용 하 여 연속 토큰 처리 hello 테이블 서비스는 응답에 반환 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="3a08f-875">hello following C# code sample using hello Storage Client Library automatically handles continuation tokens if hello table service returns them in a response:</span></span>  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

var employees = employeeTable.ExecuteQuery(employeeQuery);
foreach (var emp in employees)
{
        ...
}  
```

<span data-ttu-id="3a08f-876">C# 코드 다음 hello 연속 토큰을 명시적으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-876">hello following C# code handles continuation tokens explicitly:</span></span>  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

TableContinuationToken continuationToken = null;

do
{
        var employees = employeeTable.ExecuteQuerySegmented(
        employeeQuery, continuationToken);
    foreach (var emp in employees)
    {
    ...
    }
    continuationToken = employees.ContinuationToken;
} while (continuationToken != null);  
```

<span data-ttu-id="3a08f-877">연속 토큰을 명시적으로 사용 하 여 응용 프로그램 데이터의 다음 세그먼트 hello를 검색 하는 시기를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-877">By using continuation tokens explicitly, you can control when your application retrieves hello next segment of data.</span></span> <span data-ttu-id="3a08f-878">예를 들어 테이블에 저장 된 hello 엔터티를 통해 사용자가 toopage를 사용 하는 클라이언트 응용 프로그램, 경우 사용자 결정할 수 있도록 응용 프로그램에 사용 연속 토큰 tooretrieve hello 다음 hello 쿼리로 검색 된 모든 hello 엔터티를 통해 toopage 하지 hello 사용자 hello 현재 세그먼트에 있는 모든 hello 엔터티 집합에 대해 페이징을 완료 되 면 세그먼트입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-878">For example, if your client application enables users toopage through hello entities stored in a table, a user may decide not toopage through all hello entities retrieved by hello query so your application would only use a continuation token tooretrieve hello next segment when hello user had finished paging through all hello entities in hello current segment.</span></span> <span data-ttu-id="3a08f-879">이 접근 방식에는 몇 가지 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-879">This approach has several benefits:</span></span>  

* <span data-ttu-id="3a08f-880">하면 toolimit hello hello 테이블 서비스에서에서 데이터 tooretrieve 양과 hello 네트워크를 통해 이동 하는.</span><span class="sxs-lookup"><span data-stu-id="3a08f-880">It enables you toolimit hello amount of data tooretrieve from hello Table service and that you move over hello network.</span></span>  
* <span data-ttu-id="3a08f-881">있습니다 tooperform 비동기 IO를.net에서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-881">It enables you tooperform asynchronous IO in .NET.</span></span>  
* <span data-ttu-id="3a08f-882">하면 tooserialize hello 연속 토큰 toopersistent 저장소 응용 프로그램 크래시가의 hello 이벤트에서 계속 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-882">It enables you tooserialize hello continuation token toopersistent storage so you can continue in hello event of an application crash.</span></span>  

> [!NOTE]
> <span data-ttu-id="3a08f-883">일반적으로 연속 토큰은 1,000개(이보다 적을 수도 있음)의 엔터티가 포함된 세그먼트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-883">A continuation token typically returns a segment containing 1,000 entities, although it may be fewer.</span></span> <span data-ttu-id="3a08f-884">이것은 hello 경우에도 hello를 사용 하 여 쿼리에서 반환 하는 항목 수를 제한 하는 경우 **걸릴** tooreturn hello 처음 n 개 엔터티 조회 조건과 일치 하는: hello 테이블 서비스와 함께 n 개 엔터티를 보다 적으면를 포함 하는 세그먼트를 반환할 수 있습니다 연속 토큰 tooenable와 있습니다 tooretrieve 나머지 엔터티 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-884">This is also hello case if you limit hello number of entries a query returns by using **Take** tooreturn hello first n entities that match your lookup criteria: hello table service may return a segment containing fewer than n entities along with a continuation token tooenable you tooretrieve hello remaining entities.</span></span>  
> 
> 

<span data-ttu-id="3a08f-885">hello 다음 C# 코드를 보여 줍니다 세그먼트 내 반환 되는 엔터티의 toomodify hello 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="3a08f-885">hello following C# code shows how toomodify hello number of entities returned inside a segment:</span></span>  

```csharp
employeeQuery.TakeCount = 50;  
```

#### <a name="server-side-projection"></a><span data-ttu-id="3a08f-886">서버 쪽 프로젝션</span><span class="sxs-lookup"><span data-stu-id="3a08f-886">Server-side projection</span></span>
<span data-ttu-id="3a08f-887">단일 엔터티 too255 속성을 있고 too1 MB 단위로 크기를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-887">A single entity can have up too255 properties and be up too1 MB in size.</span></span> <span data-ttu-id="3a08f-888">모든 hello 속성이 필요 하지 않을 hello 테이블을 쿼리 하 고 엔터티를 검색할 때 및 데이터를 불필요 하 게 전송 하는 되지 않도록 (toohelp 대기 시간 및 비용을 감소 하는 데 사용).</span><span class="sxs-lookup"><span data-stu-id="3a08f-888">When you query hello table and retrieve entities, you may not need all hello properties and can avoid transferring data unnecessarily (toohelp reduce latency and cost).</span></span> <span data-ttu-id="3a08f-889">필요한 서버 쪽 프로젝션 tootransfer 정당한 hello 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-889">You can use server-side projection tootransfer just hello properties you need.</span></span> <span data-ttu-id="3a08f-890">hello 다음 예제는 검색만 hello **전자 메일** 속성 (함께 **PartitionKey**, **RowKey**, **타임 스탬프**, 및  **ETag**) hello 엔터티에서 hello 쿼리에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-890">hello following example is retrieves just hello **Email** property (along with **PartitionKey**, **RowKey**, **Timestamp**, and **ETag**) from hello entities selected by hello query.</span></span>  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
List<string> columns = new List<string>() { "Email" };
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter).Select(columns);

var entities = employeeTable.ExecuteQuery(employeeQuery);
foreach (var e in entities)
{
        Console.WriteLine("RowKey: {0}, EmployeeEmail: {1}", e.RowKey, e.Email);
}  
```

<span data-ttu-id="3a08f-891">Hello 어떻게 확인 **RowKey** 속성 tooretrieve hello 목록에 포함 되지 않은 경우에 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-891">Notice how hello **RowKey** value is available even though it was not included in hello list of properties tooretrieve.</span></span>  

### <a name="modifying-entities"></a><span data-ttu-id="3a08f-892">엔터티 수정</span><span class="sxs-lookup"><span data-stu-id="3a08f-892">Modifying entities</span></span>
<span data-ttu-id="3a08f-893">저장소 클라이언트 라이브러리 hello toomodify를 삽입, 삭제 및 업데이트 엔터티 여 hello 테이블 서비스에 저장 된 엔터티 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-893">hello Storage Client Library enables you toomodify your entities stored in hello table service by inserting, deleting, and updating entities.</span></span> <span data-ttu-id="3a08f-894">여러 삽입, 업데이트 및 삭제 작업 함께 tooreduce hello 수의 왕복 필요 하 고 솔루션의 hello 성능 향상 EGTs toobatch를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-894">You can use EGTs toobatch multiple insert, update, and delete operations together tooreduce hello number of round trips required and improve hello performance of your solution.</span></span>  

<span data-ttu-id="3a08f-895">참고 hello 저장소 클라이언트 라이브러리는 EGT를 일반적으로 실행 될 때 발생 한 예외 hello 일괄 처리 toofail 발생 시킨 hello 엔터티의 hello 인덱스를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-895">Note that exceptions thrown when hello Storage Client Library executes an EGT typically include hello index of hello entity that caused hello batch toofail.</span></span> <span data-ttu-id="3a08f-896">이는 EGT를 사용하는 코드를 디버그할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-896">This is helpful when you are debugging code that uses EGTs.</span></span>  

<span data-ttu-id="3a08f-897">디자인이 클라이언트 응용 프로그램에서 동시성 및 업데이트 작업을 처리하는 방법에 어떤 영향을 미치는지도 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-897">You should also consider how your design affects how your client application handles concurrency and update operations.</span></span>  

#### <a name="managing-concurrency"></a><span data-ttu-id="3a08f-898">동시성 관리</span><span class="sxs-lookup"><span data-stu-id="3a08f-898">Managing concurrency</span></span>
<span data-ttu-id="3a08f-899">기본적으로 hello 테이블 서비스는 낙관적 동시성 검사에 대 한 개별 엔터티 hello 수준에서 구현 **삽입**, **병합**, 및 **삭제** 작업 클라이언트 tooforce hello 테이블 서비스 toobypass 이러한 검사에 대 한 것이 가능 하지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-899">By default, hello table service implements optimistic concurrency checks at hello level of individual entities for **Insert**, **Merge**, and **Delete** operations, although it is possible for a client tooforce hello table service toobypass these checks.</span></span> <span data-ttu-id="3a08f-900">Hello 테이블 서비스 동시성을 관리 하는 방법에 대 한 자세한 내용은 참조 [Microsoft Azure 저장소에 대 한 동시성 관리](../storage/common/storage-concurrency.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-900">For more information about how hello table service manages concurrency, see  [Managing Concurrency in Microsoft Azure Storage](../storage/common/storage-concurrency.md).</span></span>  

#### <a name="merge-or-replace"></a><span data-ttu-id="3a08f-901">병합 또는 바꾸기</span><span class="sxs-lookup"><span data-stu-id="3a08f-901">Merge or replace</span></span>
<span data-ttu-id="3a08f-902">hello **대체** hello 방식의 **TableOperation** 클래스에는 항상 hello hello 테이블 서비스에서에서 전체 엔터티 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-902">hello **Replace** method of hello **TableOperation** class always replaces hello complete entity in hello Table service.</span></span> <span data-ttu-id="3a08f-903">Hello 저장 된 엔터티의 해당 속성이 존재 하는 경우 속성 hello 요청에 포함 되지 않은 경우 hello 요청 엔터티 hello에서 속성에 저장 되도록를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-903">If you do not include a property in hello request when that property exists in hello stored entity, hello request removes that property from hello stored entity.</span></span> <span data-ttu-id="3a08f-904">Tooremove 저장 엔터티에서 명시적으로 속성을 사용 하려는 경우가 아니면 hello 요청에서 모든 속성을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-904">Unless you want tooremove a property explicitly from a stored entity, you must include every property in hello request.</span></span>  

<span data-ttu-id="3a08f-905">Hello를 사용할 수 있습니다 **병합** hello 방식의 **TableOperation** 보내는 toohello 테이블 서비스 tooupdate 하려는 경우 엔터티 데이터 양을 tooreduce hello 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-905">You can use hello **Merge** method of hello **TableOperation** class tooreduce hello amount of data that you send toohello Table service when you want tooupdate an entity.</span></span> <span data-ttu-id="3a08f-906">hello **병합** 메서드 hello 요청에 포함 된 hello 엔터티에서 속성 값으로 저장 하는 hello 엔터티의 모든 속성을 대체 하지만 leaves 그대로 hello에서 속성을 hello 요청에 포함 되지 않은 엔터티를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-906">hello **Merge** method replaces any properties in hello stored entity with property values from hello entity included in hello request, but leaves intact any properties in hello stored entity that are not included in hello request.</span></span> <span data-ttu-id="3a08f-907">큰 엔터티를 있고만 tooupdate 적은 수의 요청에서 속성을 필요한 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-907">This is useful if you have large entities and only need tooupdate a small number of properties in a request.</span></span>  

> [!NOTE]
> <span data-ttu-id="3a08f-908">hello **대체** 및 **병합** hello 엔터티가 존재 하지 않는 경우 메서드가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-908">hello **Replace** and **Merge** methods fail if hello entity does not exist.</span></span> <span data-ttu-id="3a08f-909">사용 하 여 hello **InsertOrReplace** 및 **InsertOrMerge** 존재 하지 않는 경우 새 엔터티를 만드는 메서드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-909">As an alternative, you can use hello **InsertOrReplace** and **InsertOrMerge** methods that create a new entity if it doesn't exist.</span></span>  
> 
> 

### <a name="working-with-heterogeneous-entity-types"></a><span data-ttu-id="3a08f-910">유형이 다른 엔터티 유형 작업</span><span class="sxs-lookup"><span data-stu-id="3a08f-910">Working with heterogeneous entity types</span></span>
<span data-ttu-id="3a08f-911">hello 테이블 서비스는는 *스키마 없음* 테이블 저장소를 단일 테이블 디자인에 뛰어난 유연성을 제공 하는 여러 형식의 엔터티를 저장할 수 있다는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-911">hello Table service is a *schema-less* table store that means that a single table can store entities of multiple types providing great flexibility in your design.</span></span> <span data-ttu-id="3a08f-912">hello 다음 예제에서는 employee 및 department 엔터티 둘 다를 저장 하는 테이블 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-912">hello following example illustrates a table storing both employee and department entities:</span></span>  

<table>
<tr>
<th><span data-ttu-id="3a08f-913">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="3a08f-913">PartitionKey</span></span></th>
<th><span data-ttu-id="3a08f-914">RowKey</span><span class="sxs-lookup"><span data-stu-id="3a08f-914">RowKey</span></span></th>
<th><span data-ttu-id="3a08f-915">타임 스탬프</span><span class="sxs-lookup"><span data-stu-id="3a08f-915">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="3a08f-916">FirstName</span><span class="sxs-lookup"><span data-stu-id="3a08f-916">FirstName</span></span></th>
<th><span data-ttu-id="3a08f-917">LastName</span><span class="sxs-lookup"><span data-stu-id="3a08f-917">LastName</span></span></th>
<th><span data-ttu-id="3a08f-918">Age</span><span class="sxs-lookup"><span data-stu-id="3a08f-918">Age</span></span></th>
<th><span data-ttu-id="3a08f-919">Email</span><span class="sxs-lookup"><span data-stu-id="3a08f-919">Email</span></span></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="3a08f-920">FirstName</span><span class="sxs-lookup"><span data-stu-id="3a08f-920">FirstName</span></span></th>
<th><span data-ttu-id="3a08f-921">LastName</span><span class="sxs-lookup"><span data-stu-id="3a08f-921">LastName</span></span></th>
<th><span data-ttu-id="3a08f-922">Age</span><span class="sxs-lookup"><span data-stu-id="3a08f-922">Age</span></span></th>
<th><span data-ttu-id="3a08f-923">Email</span><span class="sxs-lookup"><span data-stu-id="3a08f-923">Email</span></span></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="3a08f-924">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="3a08f-924">DepartmentName</span></span></th>
<th><span data-ttu-id="3a08f-925">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="3a08f-925">EmployeeCount</span></span></th>
</tr>
<tr>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="3a08f-926">FirstName</span><span class="sxs-lookup"><span data-stu-id="3a08f-926">FirstName</span></span></th>
<th><span data-ttu-id="3a08f-927">LastName</span><span class="sxs-lookup"><span data-stu-id="3a08f-927">LastName</span></span></th>
<th><span data-ttu-id="3a08f-928">Age</span><span class="sxs-lookup"><span data-stu-id="3a08f-928">Age</span></span></th>
<th><span data-ttu-id="3a08f-929">Email</span><span class="sxs-lookup"><span data-stu-id="3a08f-929">Email</span></span></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

<span data-ttu-id="3a08f-930">각 엔터티에 여전히 **PartitionKey**, **RowKey** 및 **Timestamp** 값이 있어야 하지만 다른 속성 집합은 원하는 대로 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-930">Note that each entity must still have **PartitionKey**, **RowKey**, and **Timestamp** values, but may have any set of properties.</span></span> <span data-ttu-id="3a08f-931">또한 없는 toostore 어딘가에 해당 정보를 선택 하지 않으면 엔터티 tooindicate hello 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-931">Furthermore, there is nothing tooindicate hello type of an entity unless you choose toostore that information somewhere.</span></span> <span data-ttu-id="3a08f-932">Hello 엔터티 유형을 식별 하는 방법은 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-932">There are two options for identifying hello entity type:</span></span>  

* <span data-ttu-id="3a08f-933">Hello 엔터티 형식 toohello 앞 **RowKey** (또는 가능 환영 **PartitionKey**).</span><span class="sxs-lookup"><span data-stu-id="3a08f-933">Prepend hello entity type toohello **RowKey** (or possibly hello **PartitionKey**).</span></span> <span data-ttu-id="3a08f-934">**RowKey** 값을 예로 들어 **EMPLOYEE_000123** 또는 **DEPARTMENT_SALES**하십시오.</span><span class="sxs-lookup"><span data-stu-id="3a08f-934">For example, **EMPLOYEE_000123** or **DEPARTMENT_SALES** as **RowKey** values.</span></span>  
* <span data-ttu-id="3a08f-935">Hello 테이블 아래에 나와 있는 것 처럼 별도 속성 toorecord hello 엔터티 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-935">Use a separate property toorecord hello entity type as shown in hello table below.</span></span>  

<table>
<tr>
<th><span data-ttu-id="3a08f-936">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="3a08f-936">PartitionKey</span></span></th>
<th><span data-ttu-id="3a08f-937">RowKey</span><span class="sxs-lookup"><span data-stu-id="3a08f-937">RowKey</span></span></th>
<th><span data-ttu-id="3a08f-938">타임 스탬프</span><span class="sxs-lookup"><span data-stu-id="3a08f-938">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="3a08f-939">EntityType</span><span class="sxs-lookup"><span data-stu-id="3a08f-939">EntityType</span></span></th>
<th><span data-ttu-id="3a08f-940">FirstName</span><span class="sxs-lookup"><span data-stu-id="3a08f-940">FirstName</span></span></th>
<th><span data-ttu-id="3a08f-941">LastName</span><span class="sxs-lookup"><span data-stu-id="3a08f-941">LastName</span></span></th>
<th><span data-ttu-id="3a08f-942">Age</span><span class="sxs-lookup"><span data-stu-id="3a08f-942">Age</span></span></th>
<th><span data-ttu-id="3a08f-943">Email</span><span class="sxs-lookup"><span data-stu-id="3a08f-943">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="3a08f-944">Employee</span><span class="sxs-lookup"><span data-stu-id="3a08f-944">Employee</span></span></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="3a08f-945">EntityType</span><span class="sxs-lookup"><span data-stu-id="3a08f-945">EntityType</span></span></th>
<th><span data-ttu-id="3a08f-946">FirstName</span><span class="sxs-lookup"><span data-stu-id="3a08f-946">FirstName</span></span></th>
<th><span data-ttu-id="3a08f-947">LastName</span><span class="sxs-lookup"><span data-stu-id="3a08f-947">LastName</span></span></th>
<th><span data-ttu-id="3a08f-948">Age</span><span class="sxs-lookup"><span data-stu-id="3a08f-948">Age</span></span></th>
<th><span data-ttu-id="3a08f-949">Email</span><span class="sxs-lookup"><span data-stu-id="3a08f-949">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="3a08f-950">Employee</span><span class="sxs-lookup"><span data-stu-id="3a08f-950">Employee</span></span></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="3a08f-951">EntityType</span><span class="sxs-lookup"><span data-stu-id="3a08f-951">EntityType</span></span></th>
<th><span data-ttu-id="3a08f-952">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="3a08f-952">DepartmentName</span></span></th>
<th><span data-ttu-id="3a08f-953">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="3a08f-953">EmployeeCount</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="3a08f-954">department</span><span class="sxs-lookup"><span data-stu-id="3a08f-954">Department</span></span></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="3a08f-955">EntityType</span><span class="sxs-lookup"><span data-stu-id="3a08f-955">EntityType</span></span></th>
<th><span data-ttu-id="3a08f-956">FirstName</span><span class="sxs-lookup"><span data-stu-id="3a08f-956">FirstName</span></span></th>
<th><span data-ttu-id="3a08f-957">LastName</span><span class="sxs-lookup"><span data-stu-id="3a08f-957">LastName</span></span></th>
<th><span data-ttu-id="3a08f-958">Age</span><span class="sxs-lookup"><span data-stu-id="3a08f-958">Age</span></span></th>
<th><span data-ttu-id="3a08f-959">Email</span><span class="sxs-lookup"><span data-stu-id="3a08f-959">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="3a08f-960">Employee</span><span class="sxs-lookup"><span data-stu-id="3a08f-960">Employee</span></span></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

<span data-ttu-id="3a08f-961">hello 엔터티 형식 toohello 앞에 추가 하는 hello 첫 번째 옵션을 **RowKey**, 동일한 키 값 형식이 다른 두 개의 엔터티를 들 수 hello 가능성이 경우 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-961">hello first option, prepending hello entity type toohello **RowKey**, is useful if there is a possibility that two entities of different types might have hello same key value.</span></span> <span data-ttu-id="3a08f-962">또한 형식 함께 hello 파티션 동일 hello의 엔터티를 그룹화 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-962">It also groups entities of hello same type together in hello partition.</span></span>  

<span data-ttu-id="3a08f-963">hello이 섹션에 설명 된 기술을 특별히 관련 된 toohello 토론 [상속 관계](#inheritance-relationships) hello 섹션에이 가이드 앞부분에 있는 [관계를 모델링](#modelling-relationships)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-963">hello techniques discussed in this section are especially relevant toohello discussion [Inheritance relationships](#inheritance-relationships) earlier in this guide in hello section [Modelling relationships](#modelling-relationships).</span></span>  

> [!NOTE]
> <span data-ttu-id="3a08f-964">Hello 엔터티 형식 값 tooenable 클라이언트 응용 프로그램 tooevolve POCO 개체의 버전 번호를 포함 하는 것이 좋습니다. 하 고 다른 버전을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-964">You should consider including a version number in hello entity type value tooenable client applications tooevolve POCO objects and work with different versions.</span></span>  
> 
> 

<span data-ttu-id="3a08f-965">hello이 섹션의 나머지 부분에 설명 hello 저장소 클라이언트 라이브러리의에서 작업을 쉽고 hello의 엔터티 형식에 여러 개의 동일한 hello 기능 중 일부 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-965">hello remainder of this section describes some of hello features in hello Storage Client Library that facilitate working with multiple entity types in hello same table.</span></span>  

#### <a name="retrieving-heterogeneous-entity-types"></a><span data-ttu-id="3a08f-966">서로 다른 엔터티 유형 검색</span><span class="sxs-lookup"><span data-stu-id="3a08f-966">Retrieving heterogeneous entity types</span></span>
<span data-ttu-id="3a08f-967">Hello 저장소 클라이언트 라이브러리를 사용 하는 경우 여러 엔터티 형식을 사용 하기 위한 세 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-967">If you are using hello Storage Client Library, you have three options for working with multiple entity types.</span></span>  

<span data-ttu-id="3a08f-968">특정와 함께 저장 하는 hello 엔터티의 hello 형식을 알고 있는 경우 **RowKey** 및 **PartitionKey** 값 hello 이전 두 예와 같이 hello 엔터티를 검색 하는 경우 hello 엔터티 형식을 지정할 수 있습니다 형식의 엔터티를 검색 하는 **EmployeeEntity**: [hello 저장소 클라이언트 라이브러리를 사용 하 여 지점 쿼리를 실행](#executing-a-point-query-using-the-storage-client-library) 및 [LINQ를사용하여여러엔터티를검색](#retrieving-multiple-entities-using-linq).</span><span class="sxs-lookup"><span data-stu-id="3a08f-968">If you know hello type of hello entity stored with a specific **RowKey** and **PartitionKey** values, then you can specify hello entity type when you retrieve hello entity as shown in hello previous two examples that retrieve entities of type **EmployeeEntity**: [Executing a point query using hello Storage Client Library](#executing-a-point-query-using-the-storage-client-library) and [Retrieving multiple entities using LINQ](#retrieving-multiple-entities-using-linq).</span></span>  

<span data-ttu-id="3a08f-969">hello 두 번째 옵션은 toouse hello **DynamicTableEntity** 구체적인 POCO 엔터티 형식이 아닌 형식 (예: 속성 모음) (이 옵션 수 없는 필요 tooserialize 없기 때문에 성능이 향상 및 너무 hello 엔터티를 deserialize 합니다. NET 형식)입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-969">hello second option is toouse hello **DynamicTableEntity** type (a property bag) instead of a concrete POCO entity type (this option may also improve performance because there is no need tooserialize and deserialize hello entity too.NET types).</span></span> <span data-ttu-id="3a08f-970">C# 코드를 잠재적으로 다음 hello hello 테이블에서 다른 유형의 여러 항목을 검색 하지만로 모든 엔터티를 반환 **DynamicTableEntity** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="3a08f-970">hello following C# code potentially retrieves multiple entities of different types from hello table, but returns all entities as **DynamicTableEntity** instances.</span></span> <span data-ttu-id="3a08f-971">Hello 사용 하 여 다음 **EntityType** 각 엔터티의 속성 toodetermine hello 유형:</span><span class="sxs-lookup"><span data-stu-id="3a08f-971">It then uses hello **EntityType** property toodetermine hello type of each entity:</span></span>  

```csharp
string filter = TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("PartitionKey",
    QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("RowKey",
                    QueryComparisons.GreaterThanOrEqual, "B"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey",
        QueryComparisons.LessThan, "F")
    )
);
TableQuery<DynamicTableEntity> entityQuery =
    new TableQuery<DynamicTableEntity>().Where(filter);
var employees = employeeTable.ExecuteQuery(entityQuery);

IEnumerable<DynamicTableEntity> entities = employeeTable.ExecuteQuery(entityQuery);
foreach (var e in entities)
{
EntityProperty entityTypeProperty;
if (e.Properties.TryGetValue("EntityType", out entityTypeProperty))
{
    if (entityTypeProperty.StringValue == "Employee")
    {
        // Use entityTypeProperty, RowKey, PartitionKey, Etag, and Timestamp
        }
    }
}  
```

<span data-ttu-id="3a08f-972">해당 tooretrieve hello를 사용 해야 하는 다른 속성을 확인 **TryGetValue** 메서드 hello **속성** hello 속성 **DynamicTableEntity** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-972">Note that tooretrieve other properties you must use hello **TryGetValue** method on hello **Properties** property of hello **DynamicTableEntity** class.</span></span>  

<span data-ttu-id="3a08f-973">세 번째 방법은 hello를 사용 하 여 toocombine **DynamicTableEntity** 유형 및 **EntityResolver** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="3a08f-973">A third option is toocombine using hello **DynamicTableEntity** type and an **EntityResolver** instance.</span></span> <span data-ttu-id="3a08f-974">이렇게 하면 hello에 tooresolve toomultiple POCO 형식을 동일한 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-974">This enables you tooresolve toomultiple POCO types in hello same query.</span></span> <span data-ttu-id="3a08f-975">이 예제에서는 hello **EntityResolver** 대리자 hello를 사용 하는 **EntityType** hello 쿼리에서 반환 하는 엔터티의 hello 두 형식 간의 toodistinguish 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-975">In this example, hello **EntityResolver** delegate is using hello **EntityType** property toodistinguish between hello two types of entity that hello query returns.</span></span> <span data-ttu-id="3a08f-976">hello **해결** 방법은 hello를 사용 하 여 **확인자** tooresolve 위임 **DynamicTableEntity** 너무 인스턴스**TableEntity** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="3a08f-976">hello **Resolve** method uses hello **resolver** delegate tooresolve **DynamicTableEntity** instances too**TableEntity** instances.</span></span>  

```csharp
EntityResolver<TableEntity> resolver = (pk, rk, ts, props, etag) =>
{

        TableEntity resolvedEntity = null;
        if (props["EntityType"].StringValue == "Department")
        {
        resolvedEntity = new DepartmentEntity();
        }
        else if (props["EntityType"].StringValue == "Employee")
        {
        resolvedEntity = new EmployeeEntity();
        }
        else throw new ArgumentException("Unrecognized entity", "props");

        resolvedEntity.PartitionKey = pk;
        resolvedEntity.RowKey = rk;
        resolvedEntity.Timestamp = ts;
        resolvedEntity.ETag = etag;
        resolvedEntity.ReadEntity(props, null);
        return resolvedEntity;
};

string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<DynamicTableEntity> entityQuery =
        new TableQuery<DynamicTableEntity>().Where(filter);

var entities = employeeTable.ExecuteQuery(entityQuery, resolver);
foreach (var e in entities)
{
        if (e is DepartmentEntity)
        {
    ...
        }
        if (e is EmployeeEntity)
        {
    ...
        }
}  
```

#### <a name="modifying-heterogeneous-entity-types"></a><span data-ttu-id="3a08f-977">서로 다른 엔터티 유형 수정</span><span class="sxs-lookup"><span data-stu-id="3a08f-977">Modifying heterogeneous entity types</span></span>
<span data-ttu-id="3a08f-978">및를 알려 항상 hello 엔터티 형식을 삽입 하면 tooknow hello 유형의 엔터티 toodelete 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-978">You do not need tooknow hello type of an entity toodelete it, and you always know hello type of an entity when you insert it.</span></span> <span data-ttu-id="3a08f-979">사용할 수 있습니다 **DynamicTableEntity** 해당 형식을 모르는 및 POCO 엔터티 클래스를 사용 하지 않고 tooupdate 엔터티를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-979">However, you can use **DynamicTableEntity** type tooupdate an entity without knowing its type and without using a POCO entity class.</span></span> <span data-ttu-id="3a08f-980">hello 다음 코드 예제는 단일 엔터티를 검색 하 고 hello 확인 **EmployeeCount** 업데이트 하기 전에 속성이 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-980">hello following code sample retrieves a single entity, and checks hello **EmployeeCount** property exists before updating it.</span></span>  

```csharp
TableResult result =
        employeeTable.Execute(TableOperation.Retrieve(partitionKey, rowKey));
DynamicTableEntity department = (DynamicTableEntity)result.Result;

EntityProperty countProperty;

if (!department.Properties.TryGetValue("EmployeeCount", out countProperty))
{
        throw new
        InvalidOperationException("Invalid entity, EmployeeCount property not found.");
}
countProperty.Int32Value += 1;
employeeTable.Execute(TableOperation.Merge(department));  
```

### <a name="controlling-access-with-shared-access-signatures"></a><span data-ttu-id="3a08f-981">공유 액세스 서명을 사용하여 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="3a08f-981">Controlling access with Shared Access Signatures</span></span>
<span data-ttu-id="3a08f-982">공유 액세스 서명 (SAS) 토큰 tooenable 클라이언트 응용 프로그램 toomodify를 사용 하 여 (및 쿼리할 수 있습니다) hello 테이블 서비스와 직접 hello 필요 tooauthenticate 하지 않고 직접 테이블 엔터티.</span><span class="sxs-lookup"><span data-stu-id="3a08f-982">You can use Shared Access Signature (SAS) tokens tooenable client applications toomodify (and query) table entities directly without hello need tooauthenticate directly with hello table service.</span></span> <span data-ttu-id="3a08f-983">일반적으로, 응용 프로그램에서 세 가지 주요 이점을 toousing SAS입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-983">Typically, there are three main benefits toousing SAS in your application:</span></span>  

* <span data-ttu-id="3a08f-984">Toodistribute 불필요 저장소 계정 키 tooan 안전 하지 않은 플랫폼 (예: 모바일 장치)에 순서 tooallow 해당 장치 tooaccess 및 hello 테이블 서비스의에서 엔터티를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-984">You do not need toodistribute your storage account key tooan insecure platform (such as a mobile device) in order tooallow that device tooaccess and modify entities in hello Table service.</span></span>  
* <span data-ttu-id="3a08f-985">오프 로드할 수 있습니다 hello 작업의 일부 해당 웹 및 작업자 역할 최종 사용자 컴퓨터와 같은 엔터티 tooclient 장치 및 모바일 장치 관리를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-985">You can offload some of hello work that web and worker roles perform in managing your entities tooclient devices such as end-user computers and mobile devices.</span></span>  
* <span data-ttu-id="3a08f-986">에 제한 된 할당할 수 있으며 시간 제한 된 사용 권한 tooa 클라이언트 (예: toospecific 리소스 읽기 전용 액세스를 허용) 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-986">You can assign a constrained and time limited set of permissions tooa client (such as allowing read-only access toospecific resources).</span></span>  

<span data-ttu-id="3a08f-987">테이블 서비스 hello로 SAS 토큰을 사용 하는 방법에 대 한 자세한 내용은 참조 [공유 액세스 서명 (SAS)를 사용 하 여](../storage/common/storage-dotnet-shared-access-signature-part-1.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-987">For more information about using SAS tokens with hello Table service, see [Using Shared Access Signatures (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>  

<span data-ttu-id="3a08f-988">그러나 클라이언트 응용 프로그램 toohello 엔터티 hello 테이블 서비스에 권한을 부여 하는 hello SAS 토큰 여전히 생성 해야 합니다: 액세스 tooyour 저장소 계정 키를 보안에 환경에서이 작업을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-988">However, you must still generate hello SAS tokens that grant a client application toohello entities in hello table service: you should do this in an environment that has secure access tooyour storage account keys.</span></span> <span data-ttu-id="3a08f-989">일반적으로 웹 또는 작업자 역할 toogenerate hello SAS 토큰 및 tooyour 엔터티 액세스 해야 하는 toohello 클라이언트 응용 프로그램에 전달할를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-989">Typically, you use a web or worker role toogenerate hello SAS tokens and deliver them toohello client applications that need access tooyour entities.</span></span> <span data-ttu-id="3a08f-990">가 여전히 오버 헤드를 생성 하 고 SAS 토큰 tooclients 배달에 관련 된 최선의 방법 tooreduce 대량 시나리오에서 특히이 오버 헤드를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-990">Because there is still an overhead involved in generating and delivering SAS tokens tooclients, you should consider how best tooreduce this overhead, especially in high-volume scenarios.</span></span>  

<span data-ttu-id="3a08f-991">가능한 toogenerate tooa hello 테이블의에서 엔터티 집합이 있는 액세스 권한을 부여 하는 SAS 토큰은</span><span class="sxs-lookup"><span data-stu-id="3a08f-991">It is possible toogenerate a SAS token that grants access tooa subset of hello entities in a table.</span></span> <span data-ttu-id="3a08f-992">기본적으로 전체 테이블에 대 한 SAS 토큰 만들지만 이기도 가능한 toospecify의 범위는 해당 hello SAS 토큰 권한 부여 액세스 tooeither **PartitionKey** 값 또는 범위 **PartitionKey** 및  **RowKey** 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-992">By default, you create a SAS token for an entire table, but it is also possible toospecify that hello SAS token grant access tooeither a range of **PartitionKey** values, or a range of **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="3a08f-993">선택할 수 있습니다 toogenerate 시스템의 개별 사용자에 대 한 SAS 토큰 각 사용자의 SAS 토큰에 대 한 액세스만 허용 되도록 tootheir hello의 고유한 엔터티 테이블 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-993">You might choose toogenerate SAS tokens for individual users of your system such that each user's SAS token only allows them access tootheir own entities in hello table service.</span></span>  

### <a name="asynchronous-and-parallel-operations"></a><span data-ttu-id="3a08f-994">비동기 및 병렬 작업</span><span class="sxs-lookup"><span data-stu-id="3a08f-994">Asynchronous and parallel operations</span></span>
<span data-ttu-id="3a08f-995">여러 파티션에 요청을 분산하는 경우 비동기 또는 병렬 쿼리를 사용하여 처리량 및 클라이언트 응답성을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-995">Provided you are spreading your requests across multiple partitions, you can improve throughput and client responsiveness by using asynchronous or parallel queries.</span></span>
<span data-ttu-id="3a08f-996">예를 들어 둘 이상의 작업자 역할 인스턴스에서 테이블에 병렬로 액세스하는 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-996">For example, you might have two or more worker role instances accessing your tables in parallel.</span></span> <span data-ttu-id="3a08f-997">파티션의 특정 집합에 대 한 책임 개별 작업자 역할을 설치 하거나 여러 작업자 역할 인스턴스, 각 수 tooaccess 하기만 수도 있습니다는 테이블에서 파티션의 hello 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-997">You could have individual worker roles responsible for particular sets of partitions, or simply have multiple worker role instances, each able tooaccess all hello partitions in a table.</span></span>  

<span data-ttu-id="3a08f-998">클라이언트 인스턴스 내에서 저장소 작업을 비동기식으로 실행하여 처리량을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-998">Within a client instance, you can improve throughput by executing storage operations asynchronously.</span></span> <span data-ttu-id="3a08f-999">hello 저장소 클라이언트 라이브러리를 사용 하면 쉽게 toowrite 비동기 쿼리 및 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-999">hello Storage Client Library makes it easy toowrite asynchronous queries and modifications.</span></span> <span data-ttu-id="3a08f-1000">예를 들어 hello C# 코드 다음에 표시 된 대로 파티션의 모든 hello 엔터티를 검색 하는 hello 동기 메서드를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-1000">For example, you might start with hello synchronous method that retrieves all hello entities in a partition as shown in hello following C# code:</span></span>  

```csharp
private static void ManyEntitiesQuery(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

        TableContinuationToken continuationToken = null;

        do
        {
        var employees = employeeTable.ExecuteQuerySegmented(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
    {
        ...
    }
        continuationToken = employees.ContinuationToken;
        } while (continuationToken != null);
}  
```

<span data-ttu-id="3a08f-1001">Hello를 쿼리 하는 다음과 같이 비동기적으로 실행 되도록이 코드를 쉽게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-1001">You can easily modify this code so that hello query runs asynchronously as follows:</span></span>  

```csharp
private static async Task ManyEntitiesQueryAsync(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);
        TableContinuationToken continuationToken = null;

        do
        {
        var employees = await employeeTable.ExecuteQuerySegmentedAsync(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
        {
            ...
        }
        continuationToken = employees.ContinuationToken;
            } while (continuationToken != null);
}  
```

<span data-ttu-id="3a08f-1002">이 예에서 비동기 hello 다음과 같이 hello 동기 버전에서 변경 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-1002">In this asynchronous example, you can see hello following changes from hello synchronous version:</span></span>  

* <span data-ttu-id="3a08f-1003">hello 메서드 시그니처에 이제 hello 포함 **비동기** 한정자 및 반환 된 **작업** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="3a08f-1003">hello method signature now includes hello **async** modifier and returns a **Task** instance.</span></span>  
* <span data-ttu-id="3a08f-1004">호출 hello 대신 **ExecuteSegmented** 메서드 tooretrieve 결과, hello 메서드 이제 호출 hello **ExecuteSegmentedAsync** 메서드 및 사용 하 여 hello **await** 한정자 tooretrieve는 비동기적으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-1004">Instead of calling hello **ExecuteSegmented** method tooretrieve results, hello method now calls hello **ExecuteSegmentedAsync** method and uses hello **await** modifier tooretrieve results asynchronously.</span></span>  

<span data-ttu-id="3a08f-1005">hello 클라이언트 응용 프로그램이이 메서드가 여러 번 호출할 수 있습니다 (hello에 대 한 값이 서로 다른 **부서** 매개 변수), 각 쿼리에 별도 스레드에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-1005">hello client application can call this method multiple times (with different values for hello **department** parameter), and each query will run on a separate thread.</span></span>  

<span data-ttu-id="3a08f-1006">가 없는 비동기 버전의 hello **Execute** hello에 대 한 메서드 **TableQuery** 클래스 하므로 hello **a b l e** 인터페이스는 비동기 지원 열거형입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-1006">Note that there is no asynchronous version of hello **Execute** method in hello **TableQuery** class because hello **IEnumerable** interface does not support asynchronous enumeration.</span></span>  

<span data-ttu-id="3a08f-1007">엔터티를 비동기식으로 삽입, 업데이트 및 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-1007">You can also insert, update, and delete entities asynchronously.</span></span> <span data-ttu-id="3a08f-1008">다음 C# 예제는 hello 간단 하 고 동기 메서드 tooinsert 표시 하거나 employee 엔터티를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-1008">hello following C# example shows a simple, synchronous method tooinsert or replace an employee entity:</span></span>  

```csharp
private static void SimpleEmployeeUpsert(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = employeeTable
        .Execute(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

<span data-ttu-id="3a08f-1009">Hello 업데이트 다음과 같이 비동기적으로 실행 되도록이 코드를 쉽게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-1009">You can easily modify this code so that hello update runs asynchronously as follows:</span></span>  

```csharp
private static async Task SimpleEmployeeUpsertAsync(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = await employeeTable
        .ExecuteAsync(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

<span data-ttu-id="3a08f-1010">이 예에서 비동기 hello 다음과 같이 hello 동기 버전에서 변경 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-1010">In this asynchronous example, you can see hello following changes from hello synchronous version:</span></span>  

* <span data-ttu-id="3a08f-1011">hello 메서드 시그니처에 이제 hello 포함 **비동기** 한정자 및 반환 된 **작업** 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="3a08f-1011">hello method signature now includes hello **async** modifier and returns a **Task** instance.</span></span>  
* <span data-ttu-id="3a08f-1012">호출 hello 대신 **Execute** 메서드 tooupdate hello 엔터티, hello 메서드 이제 호출 hello **ExecuteAsync** 메서드 및 사용 하 여 hello **await** 한정자 tooretrieve 비동기적으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-1012">Instead of calling hello **Execute** method tooupdate hello entity, hello method now calls hello **ExecuteAsync** method and uses hello **await** modifier tooretrieve results asynchronously.</span></span>  

<span data-ttu-id="3a08f-1013">hello 클라이언트 응용 프로그램에서 이와 같은 여러 비동기 메서드를 호출할 수 및 각 메서드 호출 마다 별도 스레드에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-1013">hello client application can call multiple asynchronous methods like this one, and each method invocation will run on a separate thread.</span></span>  

### <a name="credits"></a><span data-ttu-id="3a08f-1014">크레딧</span><span class="sxs-lookup"><span data-stu-id="3a08f-1014">Credits</span></span>
<span data-ttu-id="3a08f-1015">Hello 기여도 대 한 Azure 팀의 멤버가 따르는 toothank hello 같은: Dominic Betts, Jason Hogg, 장 Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Vinay 샤 및 Serdar Ozler로 Microsoft DX에서 Tom 적입니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-1015">We would like toothank hello following members of hello Azure team for their contributions: Dominic Betts, Jason Hogg, Jean Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Vinay Shah and Serdar Ozler as well as  Tom Hollander from Microsoft DX.</span></span> 

<span data-ttu-id="3a08f-1016">또한 toothank hello 검토 주기 동안 Microsoft mvp 인 고객의 의견에 대 한 다음 같은: Igor Papirov 및 Edward Bakker 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a08f-1016">We would also like toothank hello following Microsoft MVP's for their valuable feedback during review cycles: Igor Papirov and Edward Bakker.</span></span>

[1]: ./media/storage-table-design-guide/storage-table-design-IMAGE01.png
[2]: ./media/storage-table-design-guide/storage-table-design-IMAGE02.png
[3]: ./media/storage-table-design-guide/storage-table-design-IMAGE03.png
[4]: ./media/storage-table-design-guide/storage-table-design-IMAGE04.png
[5]: ./media/storage-table-design-guide/storage-table-design-IMAGE05.png
[6]: ./media/storage-table-design-guide/storage-table-design-IMAGE06.png
[7]: ./media/storage-table-design-guide/storage-table-design-IMAGE07.png
[8]: ./media/storage-table-design-guide/storage-table-design-IMAGE08.png
[9]: ./media/storage-table-design-guide/storage-table-design-IMAGE09.png
[10]: ./media/storage-table-design-guide/storage-table-design-IMAGE10.png
[11]: ./media/storage-table-design-guide/storage-table-design-IMAGE11.png
[12]: ./media/storage-table-design-guide/storage-table-design-IMAGE12.png
[13]: ./media/storage-table-design-guide/storage-table-design-IMAGE13.png
[14]: ./media/storage-table-design-guide/storage-table-design-IMAGE14.png
[15]: ./media/storage-table-design-guide/storage-table-design-IMAGE15.png
[16]: ./media/storage-table-design-guide/storage-table-design-IMAGE16.png
[17]: ./media/storage-table-design-guide/storage-table-design-IMAGE17.png
[18]: ./media/storage-table-design-guide/storage-table-design-IMAGE18.png
[19]: ./media/storage-table-design-guide/storage-table-design-IMAGE19.png
[20]: ./media/storage-table-design-guide/storage-table-design-IMAGE20.png
[21]: ./media/storage-table-design-guide/storage-table-design-IMAGE21.png
[22]: ./media/storage-table-design-guide/storage-table-design-IMAGE22.png
[23]: ./media/storage-table-design-guide/storage-table-design-IMAGE23.png
[24]: ./media/storage-table-design-guide/storage-table-design-IMAGE24.png
[25]: ./media/storage-table-design-guide/storage-table-design-IMAGE25.png
[26]: ./media/storage-table-design-guide/storage-table-design-IMAGE26.png
[27]: ./media/storage-table-design-guide/storage-table-design-IMAGE27.png
[28]: ./media/storage-table-design-guide/storage-table-design-IMAGE28.png
[29]: ./media/storage-table-design-guide/storage-table-design-IMAGE29.png

