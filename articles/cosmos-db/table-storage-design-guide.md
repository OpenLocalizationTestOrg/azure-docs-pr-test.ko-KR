---
title: "Azure Storage 테이블 디자인 가이드 | Microsoft Docs"
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
ms.openlocfilehash: fd34fb135c76eed4041c29e00e98dde330dfe3f3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-table-design-guide-designing-scalable-and-performant-tables"></a><span data-ttu-id="f9ec4-103">Azure 저장소 테이블 디자인 가이드: 확장성이 뛰어난 디자인 및 성능이 뛰어난 테이블</span><span class="sxs-lookup"><span data-stu-id="f9ec4-103">Azure Storage Table Design Guide: Designing Scalable and Performant Tables</span></span>
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="f9ec4-104">확장형 및 영구 테이블을 디자인하려면 성능, 확장성, 비용 등 여러 가지 요소를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-104">To design scalable and performant tables you must consider a number of factors such as performance, scalability, and cost.</span></span> <span data-ttu-id="f9ec4-105">이전에 관계형 데이터베이스의 스키마를 디자인해 본 적이 있는 경우 이러한 고려 사항에 익숙하겠지만 Azure 테이블 서비스 저장소 모델과 관계형 모델 간에는 일부 유사한 점이 있는 반면 중요한 차이점도 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-105">If you have previously designed schemas for relational databases, these considerations will be familiar to you, but while there are some similarities between the Azure Table service storage model and relational models, there are also many important differences.</span></span> <span data-ttu-id="f9ec4-106">이러한 차이점으로 인해 일반적으로 관계형 데이터베이스에 익숙한 사용자에게는 직관에 반하거나 잘못된 것으로 보일 수 있지만 Azure 테이블 서비스와 같은 NoSQL 키/값 저장소를 디자인하는 경우에는 매우 적절한 완전히 다른 디자인이 도출됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-106">These differences typically lead to very different designs that may look counter-intuitive or wrong to someone familiar with relational databases, but which do make good sense if you are designing for a NoSQL key/value store such as the Azure Table service.</span></span> <span data-ttu-id="f9ec4-107">디자인 차이점의 대부분은 테이블 서비스는 수십억 개의 데이터 엔터티(관계 데이터베이스 용어로는 행)를 포함할 수 있거나 대용량 트랜잭션을 지원해야 하는 데이터 집합에 사용되는 클라우드 규모의 응용 프로그램을 지원하도록 디자인된다는 사실을 반영합니다. 따라서 데이터를 저장하는 방법을 다르게 생각하고 테이블 서비스의 작동 방식을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-107">Many of your design differences will reflect the fact that the Table service is designed to support cloud-scale applications that can contain billions of entities (rows in relational database terminology) of data or for datasets that must support very high transaction volumes: therefore, you need to think differently about how you store your data and understand how the Table service works.</span></span> <span data-ttu-id="f9ec4-108">잘 디자인된 NoSQL 데이터 저장소는 관계형 데이터베이스를 사용하는 솔루션보다 적은 비용으로 훨씬 뛰어난 확장성을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-108">A well designed NoSQL data store can enable your solution to scale much further (and at a lower cost) than a solution that uses a relational database.</span></span> <span data-ttu-id="f9ec4-109">이 가이드에서는 이러한 항목에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-109">This guide helps you with these topics.</span></span>  

## <a name="about-the-azure-table-service"></a><span data-ttu-id="f9ec4-110">Azure 테이블 서비스 정보</span><span class="sxs-lookup"><span data-stu-id="f9ec4-110">About the Azure Table service</span></span>
<span data-ttu-id="f9ec4-111">이 섹션에서는 특히 성능 및 확장성 디자인과 관련이 있는 테이블 서비스의 몇 가지 주요 기능을 중점적으로 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-111">This section highlights some of the key features of the Table service that are especially relevant to designing for performance and scalability.</span></span> <span data-ttu-id="f9ec4-112">Azure Storage와 Table service를 처음 접하는 경우 이 문서의 나머지 내용을 진행하기 전에 먼저 [Microsoft Azure Storage 소개](../storage/common/storage-introduction.md) 및 [.NET을 사용하여 Azure Table Storage 시작](table-storage-how-to-use-dotnet.md)을 읽어 보시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-112">If you are new to Azure Storage and the Table service, first read [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md) and [Get started with Azure Table Storage using .NET](table-storage-how-to-use-dotnet.md) before reading the remainder of this article.</span></span> <span data-ttu-id="f9ec4-113">이 가이드는 테이블 서비스에 중점을 두지만 Azure 큐 및 Blob 서비스를 소개하고 솔루션에서 테이블 서비스와 함께 이를 사용할 수 있는 방법에 대해서도 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-113">Although the focus of this guide is on the Table service, it will include some discussion of the Azure Queue and Blob services, and how you might use them along with the Table service in a solution.</span></span>  

<span data-ttu-id="f9ec4-114">테이블 서비스란?</span><span class="sxs-lookup"><span data-stu-id="f9ec4-114">What is the Table service?</span></span> <span data-ttu-id="f9ec4-115">이름에서 알 수 있듯이, 테이블 서비스에서는 테이블 형식을 사용하여 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-115">As you might expect from the name, the Table service uses a tabular format to store data.</span></span> <span data-ttu-id="f9ec4-116">표준 용어로, 테이블의 각 행은 엔터티를 나타내고 행은 해당 엔터티의 여러 속성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-116">In the standard terminology, each row of the table represents an entity, and the columns store the various properties of that entity.</span></span> <span data-ttu-id="f9ec4-117">모든 엔터티에는 해당 엔터티를 고유하게 식별하는 키 쌍과 테이블 서비스에서 엔터티가 마지막으로 업데이트된 시점을 추적(자동으로 발생하며, 타임스탬프를 임의 값으로 수동으로 덮어쓸 수 없음)하는 데 사용하는 타임스탬프 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-117">Every entity has a pair of keys to uniquely identify it, and a timestamp column that the Table service uses to track when the entity was last updated (this happens automatically and you cannot manually overwrite the timestamp with an arbitrary value).</span></span> <span data-ttu-id="f9ec4-118">테이블 서비스에서는 LMT(마지막 수정 타임스탬프)를 사용하여 낙관적 동시성을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-118">The Table service uses this last-modified timestamp (LMT) to manage optimistic concurrency.</span></span>  

> [!NOTE]
> <span data-ttu-id="f9ec4-119">또한 Table service REST API 작업은 LMT(마지막 수정 타임스탬프)에서 파생되는 **ETag** 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-119">The Table service REST API operations also return an **ETag** value that it derives from the last-modified timestamp (LMT).</span></span> <span data-ttu-id="f9ec4-120">이 문서에서는 ETag와 LMT를 상호 교환적으로 사용합니다. 이러한 용어는 동일한 기본 데이터를 의미하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-120">In this document we will use the terms ETag and LMT interchangeably because they refer to the same underlying data.</span></span>  
> 
> 

<span data-ttu-id="f9ec4-121">다음 예제에서는 직원 및 부서 엔터티를 저장하는 간단한 테이블 디자인을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-121">The following example shows a simple table design to store employee and department entities.</span></span> <span data-ttu-id="f9ec4-122">이 가이드의 뒷부분에 나오는 예제는 대부분 이 간단한 디자인을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-122">Many of the examples shown later in this guide are based on this simple design.</span></span>  

<table>
<tr>
<th><span data-ttu-id="f9ec4-123">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="f9ec4-123">PartitionKey</span></span></th>
<th><span data-ttu-id="f9ec4-124">RowKey</span><span class="sxs-lookup"><span data-stu-id="f9ec4-124">RowKey</span></span></th>
<th><span data-ttu-id="f9ec4-125">Timestamp</span><span class="sxs-lookup"><span data-stu-id="f9ec4-125">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td><span data-ttu-id="f9ec4-126">Marketing</span><span class="sxs-lookup"><span data-stu-id="f9ec4-126">Marketing</span></span></td>
<td><span data-ttu-id="f9ec4-127">00001</span><span class="sxs-lookup"><span data-stu-id="f9ec4-127">00001</span></span></td>
<td><span data-ttu-id="f9ec4-128">2014-08-22T00:50:32Z</span><span class="sxs-lookup"><span data-stu-id="f9ec4-128">2014-08-22T00:50:32Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="f9ec4-129">FirstName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-129">FirstName</span></span></th>
<th><span data-ttu-id="f9ec4-130">LastName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-130">LastName</span></span></th>
<th><span data-ttu-id="f9ec4-131">Age</span><span class="sxs-lookup"><span data-stu-id="f9ec4-131">Age</span></span></th>
<th><span data-ttu-id="f9ec4-132">Email</span><span class="sxs-lookup"><span data-stu-id="f9ec4-132">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="f9ec4-133">Don</span><span class="sxs-lookup"><span data-stu-id="f9ec4-133">Don</span></span></td>
<td><span data-ttu-id="f9ec4-134">Hall</span><span class="sxs-lookup"><span data-stu-id="f9ec4-134">Hall</span></span></td>
<td><span data-ttu-id="f9ec4-135">34</span><span class="sxs-lookup"><span data-stu-id="f9ec4-135">34</span></span></td>
<td>donh@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td><span data-ttu-id="f9ec4-136">Marketing</span><span class="sxs-lookup"><span data-stu-id="f9ec4-136">Marketing</span></span></td>
<td><span data-ttu-id="f9ec4-137">00002</span><span class="sxs-lookup"><span data-stu-id="f9ec4-137">00002</span></span></td>
<td><span data-ttu-id="f9ec4-138">2014-08-22T00:50:34Z</span><span class="sxs-lookup"><span data-stu-id="f9ec4-138">2014-08-22T00:50:34Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="f9ec4-139">FirstName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-139">FirstName</span></span></th>
<th><span data-ttu-id="f9ec4-140">LastName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-140">LastName</span></span></th>
<th><span data-ttu-id="f9ec4-141">Age</span><span class="sxs-lookup"><span data-stu-id="f9ec4-141">Age</span></span></th>
<th><span data-ttu-id="f9ec4-142">Email</span><span class="sxs-lookup"><span data-stu-id="f9ec4-142">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="f9ec4-143">Jun</span><span class="sxs-lookup"><span data-stu-id="f9ec4-143">Jun</span></span></td>
<td><span data-ttu-id="f9ec4-144">Cao</span><span class="sxs-lookup"><span data-stu-id="f9ec4-144">Cao</span></span></td>
<td><span data-ttu-id="f9ec4-145">47</span><span class="sxs-lookup"><span data-stu-id="f9ec4-145">47</span></span></td>
<td>junc@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td><span data-ttu-id="f9ec4-146">Marketing</span><span class="sxs-lookup"><span data-stu-id="f9ec4-146">Marketing</span></span></td>
<td><span data-ttu-id="f9ec4-147">부서</span><span class="sxs-lookup"><span data-stu-id="f9ec4-147">Department</span></span></td>
<td><span data-ttu-id="f9ec4-148">2014-08-22T00:50:30Z</span><span class="sxs-lookup"><span data-stu-id="f9ec4-148">2014-08-22T00:50:30Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="f9ec4-149">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-149">DepartmentName</span></span></th>
<th><span data-ttu-id="f9ec4-150">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="f9ec4-150">EmployeeCount</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="f9ec4-151">Marketing</span><span class="sxs-lookup"><span data-stu-id="f9ec4-151">Marketing</span></span></td>
<td><span data-ttu-id="f9ec4-152">153</span><span class="sxs-lookup"><span data-stu-id="f9ec4-152">153</span></span></td>
</tr>
</table>
</td>
</tr>
<tr>
<td><span data-ttu-id="f9ec4-153">Sales</span><span class="sxs-lookup"><span data-stu-id="f9ec4-153">Sales</span></span></td>
<td><span data-ttu-id="f9ec4-154">00010</span><span class="sxs-lookup"><span data-stu-id="f9ec4-154">00010</span></span></td>
<td><span data-ttu-id="f9ec4-155">2014-08-22T00:50:44Z</span><span class="sxs-lookup"><span data-stu-id="f9ec4-155">2014-08-22T00:50:44Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="f9ec4-156">FirstName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-156">FirstName</span></span></th>
<th><span data-ttu-id="f9ec4-157">LastName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-157">LastName</span></span></th>
<th><span data-ttu-id="f9ec4-158">Age</span><span class="sxs-lookup"><span data-stu-id="f9ec4-158">Age</span></span></th>
<th><span data-ttu-id="f9ec4-159">Email</span><span class="sxs-lookup"><span data-stu-id="f9ec4-159">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="f9ec4-160">Ken</span><span class="sxs-lookup"><span data-stu-id="f9ec4-160">Ken</span></span></td>
<td><span data-ttu-id="f9ec4-161">Kwok</span><span class="sxs-lookup"><span data-stu-id="f9ec4-161">Kwok</span></span></td>
<td><span data-ttu-id="f9ec4-162">23</span><span class="sxs-lookup"><span data-stu-id="f9ec4-162">23</span></span></td>
<td>kenk@contoso.com</td>
</tr>
</table>
</td>
</tr>
</table>


<span data-ttu-id="f9ec4-163">지금까지는 이 테이블은 필수 열이 있고 여러 엔터티 유형을 동일한 테이블에 저장할 수 있다는 점을 제외하고는 관계형 데이터베이스의 테이블과 매우 유사하게 보입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-163">So far, this looks very similar to a table in a relational database with the key differences being the mandatory columns, and the ability to store multiple entity types in the same table.</span></span> <span data-ttu-id="f9ec4-164">또한 **FirstName** 또는 **Age**와 같은 각 사용자 정의 속성에 관계형 데이터베이스의 열과 마찬가지로 정수 또는 문자열과 같은 데이터 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-164">In addition, each of the user-defined properties such as **FirstName** or **Age** has a data type, such as integer or string, just like a column in a relational database.</span></span> <span data-ttu-id="f9ec4-165">관계형 데이터베이스와 달리 테이블 서비스는 스키마 없음 속성을 갖추고 있기 때문에 각 엔터티의 데이터 유형이 동일하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-165">Although unlike in a relational database, the schema-less nature of the Table service means that a property need not have the same data type on each entity.</span></span> <span data-ttu-id="f9ec4-166">복잡한 데이터 형식을 단일 속성에 저장하려면 JSON 또는 XML과 같은 직렬화된 형식을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-166">To store complex data types in a single property, you must use a serialized format such as JSON or XML.</span></span> <span data-ttu-id="f9ec4-167">지원되는 데이터 형식, 지원되는 날짜 범위, 명명 규칙, 크기 제약 조건 등 테이블 서비스에 대한 자세한 내용은 [테이블 서비스 데이터 모델 이해](http://msdn.microsoft.com/library/azure/dd179338.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-167">For more information about the table service such as supported data types, supported date ranges, naming rules, and size constraints, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="f9ec4-168">**PartitionKey** 및 **RowKey** 선택은 적절한 테이블 디자인의 기본 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-168">As you will see, your choice of **PartitionKey** and **RowKey** is fundamental to good table design.</span></span> <span data-ttu-id="f9ec4-169">테이블에 저장된 모든 엔터티에는 고유하게 조합된 **PartitionKey**와 **RowKey**가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-169">Every entity stored in a table must have a unique combination of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="f9ec4-170">관계형 데이터베이스의 키와 마찬가지로 **PartitionKey** 및 **RowKey** 값은 빠른 조회를 지원하는 클러스터형 인덱스를 생성하기 위해 인덱싱됩니다. 그러나 Table service에서는 보조 인덱스를 만들지 않으므로 인덱싱된 속성은 이 두 개뿐입니다(이 명확한 제한 사항을 해결하는 방법은 뒷부분에 설명된 일부 패턴 참조).</span><span class="sxs-lookup"><span data-stu-id="f9ec4-170">As with keys in a relational database table, the **PartitionKey** and **RowKey** values are indexed to create a clustered index that enables fast look-ups; however, the Table service does not create any secondary indexes so these are the only two indexed properties (some of the patterns described later show how you can work around this apparent limitation).</span></span>  

<span data-ttu-id="f9ec4-171">테이블은 하나 이상의 파티션으로 구성되므로 디자인 의사 결정은 대부분 적절한 **PartitionKey** 및 **RowKey**를 선택하여 솔루션을 최적화하는 데 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-171">A table is made up of one or more partitions, and as you will see, many of the design decisions you make will be around choosing a suitable **PartitionKey** and **RowKey** to optimize your solution.</span></span> <span data-ttu-id="f9ec4-172">솔루션은 파티션으로 구성된 모든 엔터티를 포함하는 단일 테이블로 구성될 수 있지만 일반적으로 솔루션에는 여러 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-172">A solution could consist of just a single table that contains all your entities organized into partitions, but typically a solution will have multiple tables.</span></span> <span data-ttu-id="f9ec4-173">테이블을 사용하면 엔터티를 논리적으로 구성하고, 액세스 제어 목록을 사용하여 데이터 액세스를 보다 쉽게 관리하며, 단일 저장소 작업을 사용하여 전체 테이블을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-173">Tables help you to logically organize your entities, help you manage access to the data using access control lists, and you can drop an entire table using a single storage operation.</span></span>  

### <a name="table-partitions"></a><span data-ttu-id="f9ec4-174">테이블 파티션</span><span class="sxs-lookup"><span data-stu-id="f9ec4-174">Table partitions</span></span>
<span data-ttu-id="f9ec4-175">계정 이름, 테이블 이름 및 **PartitionKey** 가 함께 테이블 서비스에서 엔터티를 저장하는 저장소 서비스 내의 파티션을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-175">The account name, table name and **PartitionKey** together identify the partition within the storage service where the table service stores the entity.</span></span> <span data-ttu-id="f9ec4-176">파티션은 엔터티의 주소 지정 체계의 일부일 뿐만 아니라 트랜잭션의 범위를 정의(아래의 [EGT(엔터티 그룹 트랜잭션)](#entity-group-transactions) 참조)하며, 테이블 서비스를 확장하는 방법의 기초가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-176">As well as being part of the addressing scheme for entities, partitions define a scope for transactions (see [Entity Group Transactions](#entity-group-transactions) below), and form the basis of how the table service scales.</span></span> <span data-ttu-id="f9ec4-177">파티션에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](../storage/common/storage-scalability-targets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-177">For more information on partitions see [Azure Storage Scalability and Performance Targets](../storage/common/storage-scalability-targets.md).</span></span>  

<span data-ttu-id="f9ec4-178">테이블 서비스에서 개별 노드는 하나 이상의 전체 파티션을 지원하며, 서비스는 노드 간에 파티션 부하를 동적으로 분산하여 크기가 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-178">In the Table service, an individual node services one or more complete partitions and the service scales by dynamically load-balancing partitions across nodes.</span></span> <span data-ttu-id="f9ec4-179">하나의 노드에 부하가 걸려 있는 경우 Table service는 해당 노드가 지원하는 파티션 범위를 여러 노드로 *분할*할 수 있습니다. 트래픽이 진정되면 서비스는 안정된 노드의 파티션 범위를 단일 노드로 다시*병합*할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-179">If a node is under load, the table service can *split* the range of partitions serviced by that node onto different nodes; when traffic subsides, the service can *merge* the partition ranges from quiet nodes back onto a single node.</span></span>  

<span data-ttu-id="f9ec4-180">테이블 서비스의 내부 세부 정보, 특히 서비스에서 파티션을 관리하는 방법에 대한 자세한 내용은 [Microsoft Azure 저장소: 강력한 일관성과 함께 항상 사용 가능한 클라우드 저장소 서비스](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-180">For more information about the internal details of the Table service, and in particular how the service manages partitions, see the paper [Microsoft Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).</span></span>  

### <a name="entity-group-transactions"></a><span data-ttu-id="f9ec4-181">EGT(엔터티 그룹 트랜잭션)</span><span class="sxs-lookup"><span data-stu-id="f9ec4-181">Entity Group Transactions</span></span>
<span data-ttu-id="f9ec4-182">테이블 서비스에서 EGT(엔터티 그룹 트랜잭션)는 여러 엔터티 간에 원자성 업데이트를 수행하기 위한 유일한 기본 제공 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-182">In the Table service, Entity Group Transactions (EGTs) are the only built-in mechanism for performing atomic updates across multiple entities.</span></span> <span data-ttu-id="f9ec4-183">EGT를 일부 문서에서는 *일괄 처리 트랜잭션* 이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-183">EGTs are also referred to as *batch transactions* in some documentation.</span></span> <span data-ttu-id="f9ec4-184">EGT는 동일한 파티션(지정된 테이블에서 동일한 파티션 키 공유)에 저장된 엔터티에서만 작동할 수 있으므로 여러 엔터티에서 원자성 트랜잭션 동작이 필요한 경우 해당 엔터티가 동일한 파티션에 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-184">EGTs can only operate on entities stored in the same partition (share the same partition key in a given table), so anytime you need atomic transactional behavior across multiple entities you need to ensure that those entities are in the same partition.</span></span> <span data-ttu-id="f9ec4-185">따라서 서로 다른 엔터티 유형에 여러 테이블을 사용하지 말고 여러 엔터티 유형을 동일한 테이블(및 파티션)에 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-185">This is often a reason for keeping multiple entity types in the same table (and partition) and not using multiple tables for different entity types.</span></span> <span data-ttu-id="f9ec4-186">단일 EGT는 최대 100개의 엔터티에서 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-186">A single EGT can operate on at most 100 entities.</span></span>  <span data-ttu-id="f9ec4-187">처리를 위해 여러 개의 동시에 발생하는 EGT를 제출하는 경우에 이러한 EGT가 EGT 간에 공통되는 엔터티에서 작동되면 처리가 지연될 수 있으므로 그렇지 않도록 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-187">If you submit multiple concurrent EGTs for processing it is important to ensure  those EGTs do not operate on entities that are common across EGTs as otherwise processing can be delayed.</span></span>

<span data-ttu-id="f9ec4-188">EGT는 디자인에서 평가할 잠재적 장단점이 있습니다. 사용하는 파티션이 많으면 Azure에서 노드 간에 요청을 부하 분산할 기회가 많기 때문에 응용 프로그램의 확장성이 증가하지만 응용 프로그램이 원자성 트랜잭션을 수행하고 데이터에 대한 강력한 일관성을 유지 관리할 수 있는 능력이 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-188">EGTs also introduce a potential trade-off for you to evaluate in your design: using more partitions will increase the scalability of your application because Azure has more opportunities for load balancing requests across nodes, but this might limit the ability of your application to perform atomic transactions and maintain strong consistency for your data.</span></span> <span data-ttu-id="f9ec4-189">또한 파티션 수준에는 단일 노드에서 기대할 수 있는 트랜잭션 처리량을 제한하는 특정 확장성 목표가 있습니다. Azure Storage 계정 및 Table service의 확장성 목표에 대한 자세한 내용은 [Azure Storage 확장성 및 성능 목표](../storage/common/storage-scalability-targets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-189">Furthermore, there are specific scalability targets at the level of a partition that might limit the throughput of transactions you can expect for a single node: for more information about the scalability targets for Azure storage accounts and the table service, see [Azure Storage Scalability and Performance Targets](../storage/common/storage-scalability-targets.md).</span></span> <span data-ttu-id="f9ec4-190">이 가이드의 뒷부분에 나오는 섹션에서는 이와 같은 장단점을 관리하는 데 도움이 되는 여러 가지 디자인 전략을 소개하고, 클라이언트 응용 프로그램의 특정 요구 사항에 따라 파티션 키를 선택하는 최상의 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-190">Later sections of this guide discuss various design strategies that help you manage trade-offs such as this one, and discuss how best to choose your partition key based on the specific requirements of your client application.</span></span>  

### <a name="capacity-considerations"></a><span data-ttu-id="f9ec4-191">용량 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f9ec4-191">Capacity considerations</span></span>
<span data-ttu-id="f9ec4-192">다음 표에는 테이블 서비스 솔루션을 디자인할 때 알아야 할 몇 가지 키 값이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-192">The following table includes some of the key values to be aware of when you are designing a Table service solution:</span></span>  

| <span data-ttu-id="f9ec4-193">Azure 저장소 계정의 총 용량</span><span class="sxs-lookup"><span data-stu-id="f9ec4-193">Total capacity of an Azure storage account</span></span> | <span data-ttu-id="f9ec4-194">500TB</span><span class="sxs-lookup"><span data-stu-id="f9ec4-194">500 TB</span></span> |
| --- | --- |
| <span data-ttu-id="f9ec4-195">Azure 저장소 계정에서 테이블의 수</span><span class="sxs-lookup"><span data-stu-id="f9ec4-195">Number of tables in an Azure storage account</span></span> |<span data-ttu-id="f9ec4-196">저장소 계정의 용량에 의해서만 제한됨</span><span class="sxs-lookup"><span data-stu-id="f9ec4-196">Limited only by the capacity of the storage account</span></span> |
| <span data-ttu-id="f9ec4-197">테이블에 있는 파티션 수</span><span class="sxs-lookup"><span data-stu-id="f9ec4-197">Number of partitions in a table</span></span> |<span data-ttu-id="f9ec4-198">저장소 계정의 용량에 의해서만 제한됨</span><span class="sxs-lookup"><span data-stu-id="f9ec4-198">Limited only by the capacity of the storage account</span></span> |
| <span data-ttu-id="f9ec4-199">파티션의 엔터티 수</span><span class="sxs-lookup"><span data-stu-id="f9ec4-199">Number of entities in a partition</span></span> |<span data-ttu-id="f9ec4-200">저장소 계정의 용량에 의해서만 제한됨</span><span class="sxs-lookup"><span data-stu-id="f9ec4-200">Limited only by the capacity of the storage account</span></span> |
| <span data-ttu-id="f9ec4-201">개별 엔터티의 크기</span><span class="sxs-lookup"><span data-stu-id="f9ec4-201">Size of an individual entity</span></span> |<span data-ttu-id="f9ec4-202">최대 255개 속성을 포함하여 최대 1MB(**PartitionKey**, **RowKey** 및 **타임스탬프** 포함)</span><span class="sxs-lookup"><span data-stu-id="f9ec4-202">Up to 1 MB with a maximum of 255 properties (including the **PartitionKey**, **RowKey**, and **Timestamp**)</span></span> |
| <span data-ttu-id="f9ec4-203">**PartitionKey**</span><span class="sxs-lookup"><span data-stu-id="f9ec4-203">Size of the **PartitionKey**</span></span> |<span data-ttu-id="f9ec4-204">최대 1KB의 크기 문자열</span><span class="sxs-lookup"><span data-stu-id="f9ec4-204">A string up to 1 KB in size</span></span> |
| <span data-ttu-id="f9ec4-205">**RowKey**</span><span class="sxs-lookup"><span data-stu-id="f9ec4-205">Size of the **RowKey**</span></span> |<span data-ttu-id="f9ec4-206">최대 1KB의 크기 문자열</span><span class="sxs-lookup"><span data-stu-id="f9ec4-206">A string up to 1 KB in size</span></span> |
| <span data-ttu-id="f9ec4-207">엔터티 그룹 트랜잭션의 크기</span><span class="sxs-lookup"><span data-stu-id="f9ec4-207">Size of an Entity Group Transaction</span></span> |<span data-ttu-id="f9ec4-208">한 개 트랜잭션에는 최대 100개의 엔터티가 포함될 수 있고, 페이로드 크기는 4MB 미만이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-208">A transaction can include at most 100 entities and the payload must be less than 4 MB in size.</span></span> <span data-ttu-id="f9ec4-209">EGT는 한 번에 하나의 엔터티만 업데이트할 수 있음</span><span class="sxs-lookup"><span data-stu-id="f9ec4-209">An EGT can only update an entity once.</span></span> |

<span data-ttu-id="f9ec4-210">자세한 내용은 [테이블 서비스 데이터 모델 이해](http://msdn.microsoft.com/library/azure/dd179338.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-210">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>  

### <a name="cost-considerations"></a><span data-ttu-id="f9ec4-211">비용 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f9ec4-211">Cost considerations</span></span>
<span data-ttu-id="f9ec4-212">테이블 저장소는 비교적 저렴하지만 테이블 서비스를 사용하는 솔루션을 평가할 때 용량 사용과 트랜잭션 양 둘 다에 대한 예상 비용을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-212">Table storage is relatively inexpensive, but you should include cost estimates for both capacity usage and the quantity of transactions as part of your evaluation of any solution that uses the Table service.</span></span> <span data-ttu-id="f9ec4-213">그러나 대부분의 시나리오에서는 비정규화되거나 중복된 데이터를 저장하여 솔루션의 성능 또는 확장성을 개선하는 것이 유효한 접근 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-213">However, in many scenarios storing denormalized or duplicate data in order to improve the performance or scalability of your solution is a valid approach to take.</span></span> <span data-ttu-id="f9ec4-214">가격 책정에 대한 자세한 내용은 [Azure 저장소 가격 책정](https://azure.microsoft.com/pricing/details/storage/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-214">For more information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>  

## <a name="guidelines-for-table-design"></a><span data-ttu-id="f9ec4-215">테이블 디자인 지침</span><span class="sxs-lookup"><span data-stu-id="f9ec4-215">Guidelines for table design</span></span>
<span data-ttu-id="f9ec4-216">이 목록은 사용자의 테이블을 디자인할 때 염두에 두어야 하는 몇 가지 핵심 지침을 요약하고 이 가이드 뒷부분에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-216">These lists summarize some of the key guidelines you should keep in mind when you are designing your tables, and this guide will address them all in more detail later in.</span></span> <span data-ttu-id="f9ec4-217">이 지침은 일반적으로 관계형 데이터베이스 디자인을 수행하는 지침과 매우 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-217">These guidelines are very different from the guidelines you would typically follow for relational database design.</span></span>  

<span data-ttu-id="f9ec4-218">효율적으로 *읽을* 수 있도록 테이블 서비스 솔루션 디자인:</span><span class="sxs-lookup"><span data-stu-id="f9ec4-218">Designing your Table service solution to be *read* efficient:</span></span>

* <span data-ttu-id="f9ec4-219">***읽기 작업이 많은 응용 프로그램의 쿼리를 위해 디자인합니다.***</span><span class="sxs-lookup"><span data-stu-id="f9ec4-219">***Design for querying in read-heavy applications.***</span></span> <span data-ttu-id="f9ec4-220">테이블을 디자인할 때는 엔터티 업데이트 방법을 고려하기 전에 먼저 쿼리(특히 대기 시간이 중요한 쿼리)를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-220">When you are designing your tables, think about the queries (especially the latency sensitive ones) that you will execute before you think about how you will update your entities.</span></span> <span data-ttu-id="f9ec4-221">이는 일반적으로 솔루션의 효율성 및 성능에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-221">This typically results in an efficient and performant solution.</span></span>  
* <span data-ttu-id="f9ec4-222">***쿼리에서 PartitionKey와 RowKey 둘 다 지정합니다.***</span><span class="sxs-lookup"><span data-stu-id="f9ec4-222">***Specify both PartitionKey and RowKey in your queries.***</span></span> <span data-ttu-id="f9ec4-223">*지점 쿼리* 는 가장 효율적인 테이블 서비스 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-223">*Point queries* such as these are the most efficient table service queries.</span></span>  
* <span data-ttu-id="f9ec4-224">***엔터티의 중복 복사본을 저장하는 것이 좋습니다.***</span><span class="sxs-lookup"><span data-stu-id="f9ec4-224">***Consider storing duplicate copies of entities.***</span></span> <span data-ttu-id="f9ec4-225">테이블 저장소는 저렴하므로 여러 번 저장(다른 키를 사용하여)하여 쿼리의 효율성을 높이는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-225">Table storage is cheap so consider storing the same entity multiple times (with different keys) to enable more efficient queries.</span></span>  
* <span data-ttu-id="f9ec4-226">***데이터를 비정규화하는 것이 좋습니다.***</span><span class="sxs-lookup"><span data-stu-id="f9ec4-226">***Consider denormalizing your data.***</span></span> <span data-ttu-id="f9ec4-227">테이블 저장소는 저렴하기 때문에 데이터를 비정규화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-227">Table storage is cheap so consider denormalizing your data.</span></span> <span data-ttu-id="f9ec4-228">예를 들어 집계 데이터에 대한 쿼리에서 단일 엔터티에만 액세스하면 되도록 요약 엔터티를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-228">For example, store summary entities so that queries for aggregate data only need to access a single entity.</span></span>  
* <span data-ttu-id="f9ec4-229">***복합 키 값을 사용하는 것이 좋습니다.***</span><span class="sxs-lookup"><span data-stu-id="f9ec4-229">***Use compound key values.***</span></span> <span data-ttu-id="f9ec4-230">사용하는 키는 **PartitionKey**와 **RowKey**뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-230">The only keys you have are **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="f9ec4-231">예를 들어 복합 키 값을 사용하여 엔터티에 대한 대체 키 액세스 경로를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-231">For example, use compound key values to enable alternate keyed access paths to entities.</span></span>  
* <span data-ttu-id="f9ec4-232">***쿼리 프로젝션을 사용합니다.***</span><span class="sxs-lookup"><span data-stu-id="f9ec4-232">***Use query projection.***</span></span> <span data-ttu-id="f9ec4-233">필요한 필드만 선택하는 쿼리를 사용하여 네트워크를 통해 전송하는 데이터 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-233">You can reduce the amount of data that you transfer over the network by using queries that select just the fields you need.</span></span>  

<span data-ttu-id="f9ec4-234">효율적으로 *쓸* 수 있도록 테이블 서비스 솔루션을 디자인합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-234">Designing your Table service solution to be *write* efficient:</span></span>  

* <span data-ttu-id="f9ec4-235">***핫 파티션을 만들지 마세요.***</span><span class="sxs-lookup"><span data-stu-id="f9ec4-235">***Do not create hot partitions.***</span></span> <span data-ttu-id="f9ec4-236">언제든 여러 파티션으로 요청을 분산할 수 있는 키를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-236">Choose keys that enable you to spread your requests across multiple partitions at any point of time.</span></span>  
* <span data-ttu-id="f9ec4-237">***트래픽 급증을 방지합니다.***</span><span class="sxs-lookup"><span data-stu-id="f9ec4-237">***Avoid spikes in traffic.***</span></span> <span data-ttu-id="f9ec4-238">적절한 기간에 걸쳐 트래픽을 원활하게 유지하고 트래픽 급증을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-238">Smooth the traffic over a reasonable period of time and avoid spikes in traffic.</span></span>
* <span data-ttu-id="f9ec4-239">***각 엔터티 유형에 대한 별도의 테이블을 만들 필요가 없습니다.***</span><span class="sxs-lookup"><span data-stu-id="f9ec4-239">***Don't necessarily create a separate table for each type of entity.***</span></span> <span data-ttu-id="f9ec4-240">엔터티 유형 간에 원자성 트랜잭션이 필요한 경우 이러한 여러 엔터티 유형을 동일한 테이블의 동일한 파티션에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-240">When you require atomic transactions across entity types, you can store these multiple entity types in the same partition in the same table.</span></span>
* <span data-ttu-id="f9ec4-241">***달성해야 하는 최대 처리량을 고려합니다.***</span><span class="sxs-lookup"><span data-stu-id="f9ec4-241">***Consider the maximum throughput you must achieve.***</span></span> <span data-ttu-id="f9ec4-242">테이블 서비스의 확장성 목표를 알고 디자인으로 인해 이러한 목표가 초과되지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-242">You must be aware of the scalability targets for the Table service and ensure that your design will not cause you to exceed them.</span></span>  

<span data-ttu-id="f9ec4-243">이 가이드에서는 이 모든 원칙을 실습해 볼 수 있는 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-243">As you read this guide, you will see examples that put all of these principles into practice.</span></span>  

## <a name="design-for-querying"></a><span data-ttu-id="f9ec4-244">쿼리를 위한 디자인</span><span class="sxs-lookup"><span data-stu-id="f9ec4-244">Design for querying</span></span>
<span data-ttu-id="f9ec4-245">테이블 서비스 솔루션은 읽기 집중적이거나, 쓰기 집중적이거나, 이 두 가지가 혼합되어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-245">Table service solutions may be read intensive, write intensive, or a mix of the two.</span></span> <span data-ttu-id="f9ec4-246">이 섹션에서는 읽기 작업을 효율적으로 지원하는 테이블 서비스를 디자인할 때 알아야 할 사항에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-246">This section focuses on the things to bear in mind when you are designing your Table service to support read operations efficiently.</span></span> <span data-ttu-id="f9ec4-247">일반적으로 읽기 작업을 효율적으로 지원하는 디자인은 쓰기 작업에도 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-247">Typically, a design that supports read operations efficiently is also efficient for write operations.</span></span> <span data-ttu-id="f9ec4-248">그러나 쓰기 작업을 지원하도록 디자인할 때 염두에 두어야 하는 추가적인 고려 사항이 있습니다(다음에 나오는 [데이터 수정을 위한 디자인](#design-for-data-modification)섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="f9ec4-248">However, there are additional considerations to bear in mind when designing to support write operations, discussed in the next section, [Design for data modification](#design-for-data-modification).</span></span>

<span data-ttu-id="f9ec4-249">데이터를 효율적으로 읽을 수 있도록 테이블 서비스 솔루션을 디자인하려면 "응용 프로그램이 테이블 서비스에서 필요한 데이터를 검색하기 위해 실행해야 하는 쿼리는 무엇인가?"라는 질문에서 출발하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-249">A good starting point for designing your Table service solution to enable you to read data efficiently is to ask "What queries will my application need to execute to retrieve the data it needs from the Table service?"</span></span>  

> [!NOTE]
> <span data-ttu-id="f9ec4-250">Table service에서는 사전에 올바르게 디자인하는 것이 중요합니다. 나중에 변경하려면 작업이 어렵고 비용이 많이 들기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-250">With the Table service, it's important to get the design correct up front because it's difficult and expensive to change it later.</span></span> <span data-ttu-id="f9ec4-251">예를 들어 관계형 데이터베이스에서는 기존 데이터베이스에 인덱스를 추가하는 것만으로 성능 문제를 해결할 수 있는 경우가 종종 있습니다. 하지만 Table service에서는 그럴 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-251">For example, in a relational database it's often possible to address performance issues simply by adding indexes to an existing database: this is not an option with the Table service.</span></span>  
> 
> 

<span data-ttu-id="f9ec4-252">이 섹션에서는 쿼리를 위한 테이블을 디자인할 때 해결해야 하는 주요 문제를 중점적으로 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-252">This section focuses on the key issues you must address when you design your tables for querying.</span></span> <span data-ttu-id="f9ec4-253">이 섹션에서 다루는 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-253">The topics covered in this section include:</span></span>

* [<span data-ttu-id="f9ec4-254">PartitionKey 및 RowKey 선택이 쿼리 성능에 미치는 영향</span><span class="sxs-lookup"><span data-stu-id="f9ec4-254">How your choice of PartitionKey and RowKey impacts query performance</span></span>](#how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance)
* [<span data-ttu-id="f9ec4-255">적절한 PartitionKey 선택</span><span class="sxs-lookup"><span data-stu-id="f9ec4-255">Choosing an appropriate PartitionKey</span></span>](#choosing-an-appropriate-partitionkey)
* [<span data-ttu-id="f9ec4-256">테이블 서비스에 대한 쿼리 최적화</span><span class="sxs-lookup"><span data-stu-id="f9ec4-256">Optimizing queries for the Table service</span></span>](#optimizing-queries-for-the-table-service)
* [<span data-ttu-id="f9ec4-257">테이블 서비스에서 데이터 정렬</span><span class="sxs-lookup"><span data-stu-id="f9ec4-257">Sorting data in the Table service</span></span>](#sorting-data-in-the-table-service)

### <a name="how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance"></a><span data-ttu-id="f9ec4-258">PartitionKey 및 RowKey 선택이 쿼리 성능에 미치는 영향</span><span class="sxs-lookup"><span data-stu-id="f9ec4-258">How your choice of PartitionKey and RowKey impacts query performance</span></span>
<span data-ttu-id="f9ec4-259">다음 예제에서는 테이블 서비스가 다음과 같은 구조로 직원 엔터티를 저장하는 것으로 가정합니다(대부분의 예제에 명확성을 위해 **Timestamp** 속성이 생략되어 있음).</span><span class="sxs-lookup"><span data-stu-id="f9ec4-259">The following examples assume the table service is storing employee entities with the following structure (most of the examples omit the **Timestamp** property for clarity):</span></span>  

| <span data-ttu-id="f9ec4-260">*열 이름*</span><span class="sxs-lookup"><span data-stu-id="f9ec4-260">*Column name*</span></span> | <span data-ttu-id="f9ec4-261">*데이터 형식*</span><span class="sxs-lookup"><span data-stu-id="f9ec4-261">*Data type*</span></span> |
| --- | --- |
| <span data-ttu-id="f9ec4-262">**PartitionKey** (부서 이름)</span><span class="sxs-lookup"><span data-stu-id="f9ec4-262">**PartitionKey** (Department Name)</span></span> |<span data-ttu-id="f9ec4-263">String</span><span class="sxs-lookup"><span data-stu-id="f9ec4-263">String</span></span> |
| <span data-ttu-id="f9ec4-264">**RowKey** (직원 Id)</span><span class="sxs-lookup"><span data-stu-id="f9ec4-264">**RowKey** (Employee Id)</span></span> |<span data-ttu-id="f9ec4-265">String</span><span class="sxs-lookup"><span data-stu-id="f9ec4-265">String</span></span> |
| <span data-ttu-id="f9ec4-266">**FirstName**</span><span class="sxs-lookup"><span data-stu-id="f9ec4-266">**FirstName**</span></span> |<span data-ttu-id="f9ec4-267">String</span><span class="sxs-lookup"><span data-stu-id="f9ec4-267">String</span></span> |
| <span data-ttu-id="f9ec4-268">**LastName**</span><span class="sxs-lookup"><span data-stu-id="f9ec4-268">**LastName**</span></span> |<span data-ttu-id="f9ec4-269">String</span><span class="sxs-lookup"><span data-stu-id="f9ec4-269">String</span></span> |
| <span data-ttu-id="f9ec4-270">**Age**</span><span class="sxs-lookup"><span data-stu-id="f9ec4-270">**Age**</span></span> |<span data-ttu-id="f9ec4-271">Integer</span><span class="sxs-lookup"><span data-stu-id="f9ec4-271">Integer</span></span> |
| <span data-ttu-id="f9ec4-272">**EmailAddress**</span><span class="sxs-lookup"><span data-stu-id="f9ec4-272">**EmailAddress**</span></span> |<span data-ttu-id="f9ec4-273">String</span><span class="sxs-lookup"><span data-stu-id="f9ec4-273">String</span></span> |

<span data-ttu-id="f9ec4-274">이전 섹션 [Azure 테이블 서비스 개요](#overview) 에서는 쿼리를 위한 디자인에 직접적인 영향을 미치는 Azure 테이블 서비스의 주요 기능에 대해 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-274">The earlier section [Azure Table service overview](#overview) describes some of the key features of the Azure Table service that have a direct influence on designing for query.</span></span> <span data-ttu-id="f9ec4-275">이 섹션의 내용은 테이블 서비스 쿼리 디자인에 대한 다음과 같은 일반적인 지침으로 요약됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-275">These result in the following general guidelines for designing Table service queries.</span></span> <span data-ttu-id="f9ec4-276">아래 예제에 사용된 필터 구문은 테이블 서비스 REST API에서 가져온 것입니다(자세한 내용은 [엔터티 쿼리](http://msdn.microsoft.com/library/azure/dd179421.aspx)참조).</span><span class="sxs-lookup"><span data-stu-id="f9ec4-276">Note that the filter syntax used in the examples below is from the Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

* <span data-ttu-id="f9ec4-277">***지점 쿼리***는 가장 효율적인 조회 방법이며, 대용량 조회 또는 가장 낮은 대기 시간이 필요한 조회에 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-277">A ***Point Query*** is the most efficient lookup to use and is recommended to be used for high-volume lookups or lookups requiring lowest latency.</span></span> <span data-ttu-id="f9ec4-278">이러한 쿼리에서는 인덱스를 사용해 **PartitionKey** 및 **RowKey** 값을 지정하여 개별 엔터티를 매우 효율적으로 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-278">Such a query can use the indexes to locate an individual entity very efficiently by specifying both the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="f9ec4-279">예: $filter=(PartitionKey eq 'Sales') and (RowKey eq '2')</span><span class="sxs-lookup"><span data-stu-id="f9ec4-279">For example: $filter=(PartitionKey eq 'Sales') and (RowKey eq '2')</span></span>  
* <span data-ttu-id="f9ec4-280">두 번째로 좋은 방법은 **PartitionKey**를 사용하고 **RowKey** 값 범위를 필터링하여 둘 이상의 엔터티를 반환하는 ***Range Query***입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-280">Second best is a ***Range Query*** that uses the **PartitionKey** and filters on a range of **RowKey** values to return more than one entity.</span></span> <span data-ttu-id="f9ec4-281">**PartitionKey** 값은 특정 파티션을 식별하고, **RowKey** 값은 해당 파티션에 있는 엔터티의 하위 집합을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-281">The **PartitionKey** value identifies a specific partition, and the **RowKey** values identify a subset of the entities in that partition.</span></span> <span data-ttu-id="f9ec4-282">예: $filter=PartitionKey eq 'Sales' and RowKey ge 'S' and RowKey lt 'T'</span><span class="sxs-lookup"><span data-stu-id="f9ec4-282">For example: $filter=PartitionKey eq 'Sales' and RowKey ge 'S' and RowKey lt 'T'</span></span>  
* <span data-ttu-id="f9ec4-283">세 번째로 좋은 방법은 **PartitionKey**를 사용하고 키가 아닌 다른 속성을 필터링하여 둘 이상의 엔터티를 반환하는 ***파티션 검색***입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-283">Third best is a ***Partition Scan*** that uses the **PartitionKey** and filters on another non-key property and that may return more than one entity.</span></span> <span data-ttu-id="f9ec4-284">**PartitionKey** 값은 특정 파티션을 식별하고, 속성 값은 해당 파티션에 있는 엔터티의 하위 집합에 대해 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-284">The **PartitionKey** value identifies a specific partition, and the property values select for a subset of the entities in that partition.</span></span> <span data-ttu-id="f9ec4-285">예: $filter=PartitionKey eq 'Sales' and LastName eq 'Smith'</span><span class="sxs-lookup"><span data-stu-id="f9ec4-285">For example: $filter=PartitionKey eq 'Sales' and LastName eq 'Smith'</span></span>  
* <span data-ttu-id="f9ec4-286">***테이블 검색***은 **PartitionKey**를 포함하지 않으며, 테이블을 구성하는 모든 파티션에서 일치하는 모든 엔터티를 검색하기 때문에 매우 비효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-286">A ***Table Scan*** does not include the **PartitionKey** and is very inefficient because it searches all of the partitions that make up your table in turn for any matching entities.</span></span> <span data-ttu-id="f9ec4-287">필터에서 **RowKey**를 사용하는지 여부에 상관없이 테이블 검색을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-287">It will perform a table scan regardless of whether or not your filter uses the **RowKey**.</span></span> <span data-ttu-id="f9ec4-288">예: $filter=LastName eq 'Jones'</span><span class="sxs-lookup"><span data-stu-id="f9ec4-288">For example: $filter=LastName eq 'Jones'</span></span>  
* <span data-ttu-id="f9ec4-289">여러 엔터티를 반환하는 쿼리는 **PartitionKey**와 **RowKey** 순으로 정렬된 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-289">Queries that return multiple entities return them sorted in **PartitionKey** and **RowKey** order.</span></span> <span data-ttu-id="f9ec4-290">클라이언트에서 엔터티 재정렬을 방지하려면 가장 일반적인 정렬 순서를 정의하는 **RowKey**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-290">To avoid resorting the entities in the client, choose a **RowKey** that defines the most common sort order.</span></span>  

<span data-ttu-id="f9ec4-291">"**or**"를 사용하여 **RowKey** 값을 기반으로 필터를 지정하면 범위 쿼리로 처리되는 것이 아니라 파티션 검색이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-291">Note that using an "**or**" to specify a filter based on **RowKey** values results in a partition scan and is not treated as a range query.</span></span> <span data-ttu-id="f9ec4-292">따라서 다음과 같은 필터를 사용하는 쿼리는 피해야 합니다. $filter=PartitionKey eq 'Sales' and (RowKey eq '121' or RowKey eq '322')</span><span class="sxs-lookup"><span data-stu-id="f9ec4-292">Therefore, you should avoid queries that use filters such as: $filter=PartitionKey eq 'Sales' and (RowKey eq '121' or RowKey eq '322')</span></span>  

<span data-ttu-id="f9ec4-293">저장소 클라이언트 라이브러리를 사용하여 효율적인 쿼리를 실행하는 클라이언트 쪽 코드의 예는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-293">For examples of client-side code that use the Storage Client Library to execute efficient queries, see:</span></span>  

* [<span data-ttu-id="f9ec4-294">저장소 클라이언트 라이브러리를 사용하여 지점 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="f9ec4-294">Executing a point query using the Storage Client Library</span></span>](#executing-a-point-query-using-the-storage-client-library)
* [<span data-ttu-id="f9ec4-295">LINQ를 사용하여 여러 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="f9ec4-295">Retrieving multiple entities using LINQ</span></span>](#retrieving-multiple-entities-using-linq)
* [<span data-ttu-id="f9ec4-296">서버 쪽 프로젝션</span><span class="sxs-lookup"><span data-stu-id="f9ec4-296">Server-side projection</span></span>](#server-side-projection)  

<span data-ttu-id="f9ec4-297">동일한 테이블에 저장된 여러 엔터티 유형을 처리할 수 있는 클라이언트 쪽 코드의 예는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-297">For examples of client-side code that can handle multiple entity types stored in the same table, see:</span></span>  

* [<span data-ttu-id="f9ec4-298">유형이 다른 엔터티 유형 작업</span><span class="sxs-lookup"><span data-stu-id="f9ec4-298">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="choosing-an-appropriate-partitionkey"></a><span data-ttu-id="f9ec4-299">적절한 PartitionKey 선택</span><span class="sxs-lookup"><span data-stu-id="f9ec4-299">Choosing an appropriate PartitionKey</span></span>
<span data-ttu-id="f9ec4-300">**PartitionKey** 를 선택할 때는 EGT 사용에 대한 요구 사항(일관성 유지)과 여러 파티션에 엔터티를 분산하는 데 대한 요구 사항(솔루션의 확장성 향상) 간에 균형을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-300">Your choice of **PartitionKey** should balance the need to enables the use of EGTs (to ensure consistency) against the requirement to distribute your entities across multiple partitions (to ensure a scalable solution).</span></span>  

<span data-ttu-id="f9ec4-301">한 쪽으로 치우치면 모든 엔터티를 단일 파티션에 저장할 수 있지만 솔루션의 확장성이 제한되어 테이블 서비스에서 요청 부하를 분산하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-301">At one extreme, you could store all your entities in a single partition, but this may limit the scalability of your solution and would prevent the table service from being able to load-balance requests.</span></span> <span data-ttu-id="f9ec4-302">다른 쪽으로 치우치면 파티션당 하나의 엔터티를 저장하여 확장성을 높이고 테이블 서비스에서 요청 부하를 분산할 수 있지만 엔터티 그룹 트랜잭션을 사용하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-302">At the other extreme, you could store one entity per partition, which would be highly scalable and which enables the table service to load-balance requests, but which would prevent you from using entity group transactions.</span></span>  

<span data-ttu-id="f9ec4-303">이상적인 **PartitionKey** 는 효율적인 쿼리를 사용할 수 있도록 하고 솔루션을 확장할 수 있는 충분한 파티션이 있는 키입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-303">An ideal **PartitionKey** is one that enables you to use efficient queries and that has sufficient partitions to ensure your solution is scalable.</span></span> <span data-ttu-id="f9ec4-304">일반적으로 엔터티에는 충분한 파티션으로 엔터티를 분산하는 적절한 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-304">Typically, you will find that your entities will have a suitable property that distributes your entities across sufficient partitions.</span></span>

> [!NOTE]
> <span data-ttu-id="f9ec4-305">예를 들어 사용자 또는 직원에 대한 정보를 저장하는 시스템에서는 UserID가 적절한 PartitionKey일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-305">For example, in a system that stores information about users or employees, UserID may be a good PartitionKey.</span></span> <span data-ttu-id="f9ec4-306">지정된 UserID를 파티션 키로 사용하는 여러 엔터티가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-306">You may have several entities that use a given UserID as the partition key.</span></span> <span data-ttu-id="f9ec4-307">사용자에 대한 데이터를 저장하는 각 엔터티는 단일 파티션으로 그룹화되므로 이러한 엔터티는 높은 확장성을 유지하면서 엔터티 그룹 트랜잭션을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-307">Each entity that stores data about a user is grouped into a single partition, and so these entities are accessible via entity group transactions, while still being highly scalable.</span></span>
> 
> 

<span data-ttu-id="f9ec4-308">**PartitionKey**를 선택할 때 엔터티 삽입, 업데이트 및 삭제 방법과 관련된 추가 고려 사항이 있습니다. 자세한 내용은 아래의 [데이터 수정을 위한 디자인](#design-for-data-modification)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-308">There are additional considerations in your choice of **PartitionKey** that relate to how you will insert, update, and delete entities: see the section [Design for data modification](#design-for-data-modification) below.</span></span>  

### <a name="optimizing-queries-for-the-table-service"></a><span data-ttu-id="f9ec4-309">테이블 서비스에 대한 쿼리 최적화</span><span class="sxs-lookup"><span data-stu-id="f9ec4-309">Optimizing queries for the Table service</span></span>
<span data-ttu-id="f9ec4-310">Table service는 단일 클러스터형 인덱스의 **PartitionKey** 및 **RowKey** 값을 사용하여 엔터티를 자동으로 인덱싱하기 때문에 지점 쿼리가 가장 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-310">The Table service automatically indexes your entities using the **PartitionKey** and **RowKey** values in a single clustered index, hence the reason that point queries are the most efficient to use.</span></span> <span data-ttu-id="f9ec4-311">그러나 **PartitionKey** 및 **RowKey**에는 클러스터형 인덱스에 있는 인덱스만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-311">However, there are no indexes other than that on the clustered index on the **PartitionKey** and **RowKey**.</span></span>

<span data-ttu-id="f9ec4-312">대부분의 디자인은 여러 조건을 기반으로 엔터티를 조회할 수 있어야 한다는 요구 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-312">Many designs must meet requirements to enable lookup of entities based on multiple criteria.</span></span> <span data-ttu-id="f9ec4-313">예를 들어 전자 메일, 직원 ID 또는 성을 기반으로 직원 엔터티를 찾을 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-313">For example, locating employee entities based on email, employee id, or last name.</span></span> <span data-ttu-id="f9ec4-314">[테이블 디자인 패턴](#table-design-patterns) 섹션에 있는 다음 패턴은 이러한 유형의 요구 사항을 다루며, 테이블 서비스에서 보조 인덱스를 제공하지 않는 부분을 해결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-314">The following patterns in the section [Table Design Patterns](#table-design-patterns) address these types of requirement and describe ways of working around the fact that the Table service does not provide secondary indexes:</span></span>  

* <span data-ttu-id="f9ec4-315">[파티션 간 보조 인덱스 패턴](#intra-partition-secondary-index-pattern) - 서로 다른 **RowKey** 값을 사용하여 각 엔터티의 여러 복사본을 동일한 파티션에 저장하여 빠르고 효율적인 조회를 지원하며, 서로 다른 **RowKey** 값을 사용하여 대체 정렬 순서를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-315">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different **RowKey** values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="f9ec4-316">[파티션 간 보조 인덱스 패턴](#inter-partition-secondary-index-pattern) - 서로 다른 RowKey 값을 사용하여 각 엔터티의 여러 복사본을 별도의 파티션과 별도의 테이블에 저장하여 빠르고 효율적인 조회를 지원하며, 서로 다른 **RowKey** 값을 사용하여 대체 정렬 순서를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-316">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions or in separate tables to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="f9ec4-317">[인덱스 엔터티 패턴](#index-entities-pattern) - 인덱스 엔터티를 유지 관리하여 엔터티 목록을 반환하는 효율적인 검색을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-317">[Index Entities Pattern](#index-entities-pattern) - Maintain index entities to enable efficient searches that return lists of entities.</span></span>  

### <a name="sorting-data-in-the-table-service"></a><span data-ttu-id="f9ec4-318">테이블 서비스에서 데이터 정렬</span><span class="sxs-lookup"><span data-stu-id="f9ec4-318">Sorting data in the Table service</span></span>
<span data-ttu-id="f9ec4-319">Table service는 **PartitionKey**를 기준으로 한 다음 **RowKey**를 기준으로 하여 오름차순으로 정렬된 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-319">The Table service returns entities sorted in ascending order based on **PartitionKey** and then by **RowKey**.</span></span> <span data-ttu-id="f9ec4-320">이러한 키는 문자열 값이며, 숫자 값이 올바르게 정렬되도록 하려면 이를 고정 길이로 변환하고 0으로 채워야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-320">These keys are string values and to ensure that numeric values sort correctly, you should convert them to a fixed length and pad them with zeroes.</span></span> <span data-ttu-id="f9ec4-321">예를 들어 **RowKey**로 사용하는 직원 ID 값이 정수 값인 경우 직원 ID를 **123**에서 **00000123**으로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-321">For example, if the employee id value you use as the **RowKey** is an integer value, you should convert employee id **123** to **00000123**.</span></span>  

<span data-ttu-id="f9ec4-322">많은 응용 프로그램에서 서로 다른 순서로 정렬(예: 이름 또는 입사 날짜별로 직원 정렬)된 데이터를 사용할 수 있도록 요구하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-322">Many applications have requirements to use data sorted in different orders: for example, sorting employees by name, or by joining date.</span></span> <span data-ttu-id="f9ec4-323">섹션에 있는 다음 [테이블 디자인 패턴](#table-design-patterns) 은 엔터티의 순서를 대체 정렬하는 방법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-323">The following patterns in the section [Table Design Patterns](#table-design-patterns) address how to alternate sort orders for your entities:</span></span>  

* <span data-ttu-id="f9ec4-324">[파티션 간 보조 인덱스 패턴](#intra-partition-secondary-index-pattern) - 서로 다른 RowKey 값을 사용하여 각 엔터티의 여러 복사본을 동일한 파티션에 저장하여 빠르고 효율적인 조회를 지원하며, 서로 다른 RowKey 값을 사용하여 대체 정렬 순서를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-324">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different RowKey values.</span></span>  
* <span data-ttu-id="f9ec4-325">[파티션 간 보조 인덱스 패턴](#inter-partition-secondary-index-pattern) - 서로 다른 RowKey 값을 사용하여 각 엔터티의 여러 복사본을 별도의 파티션과 별도의 표에 저장하여 빠르고 효율적인 조회를 지원하며, 서로 다른 RowKey 값을 사용하여 대체 정렬 순서를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-325">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions in separate tables to enable fast and efficient lookups and alternate sort orders by using different RowKey values.</span></span>
* <span data-ttu-id="f9ec4-326">[로그 테일 패턴](#log-tail-pattern) - 날짜 및 시간 역순으로 정렬된 **RowKey** 값을 사용하여 가장 최근에 파티션에 추가된 *n* 엔터티를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-326">[Log tail pattern](#log-tail-pattern) - Retrieve the *n* entities most recently added to a partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

## <a name="design-for-data-modification"></a><span data-ttu-id="f9ec4-327">데이터 수정을 위한 디자인</span><span class="sxs-lookup"><span data-stu-id="f9ec4-327">Design for data modification</span></span>
<span data-ttu-id="f9ec4-328">이 섹션에서는 삽입, 업데이트 및 삭제를 최적화하기 위한 디자인 고려 사항을 중점적으로 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-328">This section focuses on the design considerations for optimizing inserts, updates, and deletes.</span></span> <span data-ttu-id="f9ec4-329">관계형 데이터베이스의 디자인과 마찬가지로(관계형 데이터베이스의 경우 디자인 장단점을 관리하는 기술이 다름), 쿼리에 최적화된 디자인과 데이터 수정에 최적화된 디자인 간의 장단점을 평가해야 하는 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-329">In some cases, you will need to evaluate the trade-off between designs that optimize for querying against designs that optimize for data modification just as you do in designs for relational databases (although the techniques for managing the design trade-offs are different in a relational database).</span></span> <span data-ttu-id="f9ec4-330">[테이블 디자인 패턴](#table-design-patterns) 섹션은 테이블 서비스에 대한 몇 가지 자세한 디자인 패턴을 알아보고 이러한 패턴의 일부 장단점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-330">The section [Table Design Patterns](#table-design-patterns) describes some detailed design patterns for the Table service and highlights some these trade-offs.</span></span> <span data-ttu-id="f9ec4-331">실제로 엔터티 쿼리에 최적화된 디자인은 대부분 엔터티를 수정하는 데에도 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-331">In practice, you will find that many designs optimized for querying entities also work well for modifying entities.</span></span>  

### <a name="optimizing-the-performance-of-insert-update-and-delete-operations"></a><span data-ttu-id="f9ec4-332">삽입, 업데이트 및 삭제 작업 성능 최적화</span><span class="sxs-lookup"><span data-stu-id="f9ec4-332">Optimizing the performance of insert, update, and delete operations</span></span>
<span data-ttu-id="f9ec4-333">엔터티를 업데이트하거나 삭제하려면 **PartitionKey** 및 **RowKey** 값을 사용하여 엔터티를 식별할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-333">To update or delete an entity, you must be able to identify it by using the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="f9ec4-334">이러한 점에서, 엔터티 수정을 위해 **PartitionKey** 및 **RowKey**를 선택할 때는 가급적 효율적으로 엔터티를 식별할 수 있어야 하므로 지점 쿼리를 지원하기 위해 선택한 것과 유사한 조건을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-334">In this respect, your choice of **PartitionKey** and **RowKey** for modifying entities should follow similar criteria to your choice to support point queries because you want to identify entities as efficiently as possible.</span></span> <span data-ttu-id="f9ec4-335">업데이트하거나 삭제해야 하는 **PartitionKey** 및 **RowKey** 값을 찾기 위해 비효율적인 파티션 또는 테이블 검색을 사용하여 엔터티를 찾고 싶지는 않을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-335">You do not want to use an inefficient partition or table scan to locate an entity in order to discover the **PartitionKey** and **RowKey** values you need to update or delete it.</span></span>  

<span data-ttu-id="f9ec4-336">[테이블 디자인 패턴](#table-design-patterns) 섹션의 다음 패턴은 성능 또는 삽입, 업데이트, 삭제 작업의 최적화를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-336">The following patterns in the section [Table Design Patterns](#table-design-patterns) address optimizing the performance or your insert, update, and delete operations:</span></span>  

* <span data-ttu-id="f9ec4-337">[대용량 삭제 패턴](#high-volume-delete-pattern) - 동시 삭제할 모든 엔터티를 고유한 별도의 테이블에 저장하여 대용량 엔터티 삭제를 지원합니다. 테이블을 삭제하면 엔터티가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-337">[High volume delete pattern](#high-volume-delete-pattern) - Enable the deletion of a high volume of entities by storing all the entities for simultaneous deletion in their own separate table; you delete the entities by deleting the table.</span></span>  
* <span data-ttu-id="f9ec4-338">[데이터 계열 패턴](#data-series-pattern) - 전체 데이터 계열을 단일 엔터티에 저장하여 요청 수를 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-338">[Data series pattern](#data-series-pattern) - Store complete data series in a single entity to minimize the number of requests you make.</span></span>  
* <span data-ttu-id="f9ec4-339">[넓은 엔터티 패턴](#wide-entities-pattern) - 여러 실제 엔터티를 사용하여 속성이 252개가 넘는 논리적 엔터티를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-339">[Wide entities pattern](#wide-entities-pattern) - Use multiple physical entities to store logical entities with more than 252 properties.</span></span>  
* <span data-ttu-id="f9ec4-340">[큰 엔터티 패턴](#large-entities-pattern) - Blob 저장소를 사용하여 큰 속성 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-340">[Large entities pattern](#large-entities-pattern) - Use blob storage to store large property values.</span></span>  

### <a name="ensuring-consistency-in-your-stored-entities"></a><span data-ttu-id="f9ec4-341">저장된 엔터티의 일관성 유지</span><span class="sxs-lookup"><span data-stu-id="f9ec4-341">Ensuring consistency in your stored entities</span></span>
<span data-ttu-id="f9ec4-342">데이터 수정을 최적화하기 위한 키 선택에 영향을 주는 다른 주요 요소는 원자성 트랜잭션을 사용하여 일관성을 유지하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-342">The other key factor that influences your choice of keys for optimizing data modifications is how to ensure consistency by using atomic transactions.</span></span> <span data-ttu-id="f9ec4-343">EGT는 동일한 파티션에 저장된 엔터티에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-343">You can only use an EGT to operate on entities stored in the same partition.</span></span>  

<span data-ttu-id="f9ec4-344">[테이블 디자인 패턴](#table-design-patterns) 섹션의 다음 패턴은 일관성 관리를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-344">The following patterns in the section [Table Design Patterns](#table-design-patterns) address managing consistency:</span></span>  

* <span data-ttu-id="f9ec4-345">[파티션 간 보조 인덱스 패턴](#intra-partition-secondary-index-pattern) - 서로 다른 **RowKey** 값을 사용하여 각 엔터티의 여러 복사본을 동일한 파티션에 저장하여 빠르고 효율적인 조회를 지원하며, 서로 다른 **RowKey** 값을 사용하여 대체 정렬 순서를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-345">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different **RowKey** values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="f9ec4-346">[파티션 간 보조 인덱스 패턴](#inter-partition-secondary-index-pattern) - 서로 다른 RowKey 값을 사용하여 각 엔터티의 여러 복사본을 별도의 파티션과 별도의 테이블에 저장하여 빠르고 효율적인 조회를 지원하며, 서로 다른 **RowKey** 값을 사용하여 대체 정렬 순서를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-346">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions or in separate tables to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="f9ec4-347">[결과적으로 일관성 있는 트랜잭션 패턴](#eventually-consistent-transactions-pattern) - Azure 큐를 사용하여 파티션 경계 또는 저장소 시스템 경계 간에 결과적으로 일관성 있는 동작을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-347">[Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) - Enable eventually consistent behavior across partition boundaries or storage system boundaries by using Azure queues.</span></span>
* <span data-ttu-id="f9ec4-348">[인덱스 엔터티 패턴](#index-entities-pattern) - 인덱스 엔터티를 유지 관리하여 엔터티 목록을 반환하는 효율적인 검색을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-348">[Index Entities Pattern](#index-entities-pattern) - Maintain index entities to enable efficient searches that return lists of entities.</span></span>  
* <span data-ttu-id="f9ec4-349">[비정규화 패턴](#denormalization-pattern) - 관련 데이터를 단일 엔터티에 함께 통합하여 단일 지점 쿼리로 필요한 모든 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-349">[Denormalization pattern](#denormalization-pattern) - Combine related data together in a single entity to enable you to retrieve all the data you need with a single point query.</span></span>  
* <span data-ttu-id="f9ec4-350">[데이터 계열 패턴](#data-series-pattern) - 전체 데이터 계열을 단일 엔터티에 저장하여 요청 수를 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-350">[Data series pattern](#data-series-pattern) - Store complete data series in a single entity to minimize the number of requests you make.</span></span>  

<span data-ttu-id="f9ec4-351">엔터티 그룹 트랜잭션에 대한 자세한 내용은 [엔터티 그룹 트랜잭션](#entity-group-transactions)섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-351">For information about entity group transactions, see the section [Entity Group Transactions](#entity-group-transactions).</span></span>  

### <a name="ensuring-your-design-for-efficient-modifications-facilitates-efficient-queries"></a><span data-ttu-id="f9ec4-352">효율적인 수정을 위한 디자인이 효율적인 쿼리에도 유용</span><span class="sxs-lookup"><span data-stu-id="f9ec4-352">Ensuring your design for efficient modifications facilitates efficient queries</span></span>
<span data-ttu-id="f9ec4-353">대부분의 경우 효율적인 쿼리를 위한 디자인은 효율적인 수정으로 이어지지만 항상 특정 시나리오에 이 사항이 적용되는지 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-353">In many cases, a design for efficient querying results in efficient modifications, but you should always evaluate whether this is the case for your specific scenario.</span></span> <span data-ttu-id="f9ec4-354">[테이블 디자인 패턴](#table-design-patterns) 섹션의 일부 패턴은 엔터티 쿼리와 수정 간의 장단점을 명시적으로 평가하므로 항상 각 작업 유형 수를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-354">Some of the patterns in the section [Table Design Patterns](#table-design-patterns) explicitly evaluate trade-offs between querying and modifying entities, and you should always take into account the number of each type of operation.</span></span>  

<span data-ttu-id="f9ec4-355">[테이블 디자인 패턴](#table-design-patterns) 섹션의 다음 패턴은 효율적인 쿼리를 위한 디자인과 효율적인 데이터 수정을 위한 디자인 간의 장단점을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-355">The following patterns in the section [Table Design Patterns](#table-design-patterns) address trade-offs between designing for efficient queries and designing for efficient data modification:</span></span>  

* <span data-ttu-id="f9ec4-356">[복합 키 패턴](#compound-key-pattern) - 복합 **RowKey** 키를 사용하여 클라이언트에서 단일 지점 쿼리로 관련 데이터를 조회하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-356">[Compound key pattern](#compound-key-pattern) - Use compound **RowKey** values to enable a client to lookup related data with a single point query.</span></span>  
* <span data-ttu-id="f9ec4-357">[로그 테일 패턴](#log-tail-pattern) - 날짜 및 시간 역순으로 정렬된 **RowKey** 값을 사용하여 가장 최근에 파티션에 추가된 *n* 엔터티를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-357">[Log tail pattern](#log-tail-pattern) - Retrieve the *n* entities most recently added to a partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

## <a name="encrypting-table-data"></a><span data-ttu-id="f9ec4-358">테이블 데이터의 암호화</span><span class="sxs-lookup"><span data-stu-id="f9ec4-358">Encrypting Table Data</span></span>
<span data-ttu-id="f9ec4-359">.NET Azure 저장소 클라이언트 라이브러리는 작업 삽입 및 삭제의 문자열 엔터티 속성 암호화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-359">The .NET Azure Storage Client Library supports encryption of string entity properties for insert and replace operations.</span></span> <span data-ttu-id="f9ec4-360">암호화된 문자열은 서비스에 이진 속성으로 저장되고 암호 해독 후에는 다시 문자열로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-360">The encrypted strings are stored on the service as binary properties, and they are converted back to strings after decryption.</span></span>    

<span data-ttu-id="f9ec4-361">테이블의 경우, 암호화 정책 외에도 사용자가 암호화할 속성을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-361">For tables, in addition to the encryption policy, users must specify the properties to be encrypted.</span></span> <span data-ttu-id="f9ec4-362">이것은 특성(TableEntity에서 파생 되는 POCO 엔터티)을 지정[EncryptProperty]하거나 암호화 해결 프로그램 요청 옵션에서 수행할 수 있습니다. </span><span class="sxs-lookup"><span data-stu-id="f9ec4-362">This can be done by either specifying an [EncryptProperty] attribute (for POCO entities that derive from TableEntity) or an encryption resolver in request options.</span></span> <span data-ttu-id="f9ec4-363">암호화 해결 프로그램은 파티션 키, 행 키, 그리고 속성 이름 및 암호화 여부 속성을 나타내는  Bool방식을 반환하는 대표자입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-363">An encryption resolver is a delegate that takes a partition key, row key, and property name and returns a Boolean that indicates whether that property should be encrypted.</span></span> <span data-ttu-id="f9ec4-364">암호화 하는 동안 클라이언트 라이브러리는 네트워크에 쓰는 동안 속성을 암호화 해야 하는지 여부를 결정하는데 이 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-364">During encryption, the client library will use this information to decide whether a property should be encrypted while writing to the wire.</span></span> <span data-ttu-id="f9ec4-365">대리자 속성은 암호화 하는 방법 논리의 가능성도 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-365">The delegate also provides for the possibility of logic around how properties are encrypted.</span></span> <span data-ttu-id="f9ec4-366">(예를 들어 X의 경우, A 속성을 암호화하고 그렇지 않은 경우 A와 B 속성을 암호화) 읽기 또는 엔터티를 쿼리 하는 동안은 이정보가 필요없다는 것을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-366">(For example, if X, then encrypt property A; otherwise encrypt properties A and B.) Note that it is not necessary to provide this information while reading or querying entities.</span></span>

<span data-ttu-id="f9ec4-367">병합은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-367">Note that merge is not currently supported.</span></span> <span data-ttu-id="f9ec4-368">속성의 하위 집합은 이전에 다른 키를 사용하여 암호화됐을 가능성이 있기 때문에 단순히 새로운 속성을 병합하는 것과 메타데이터를 업데이트 하는 것은 데이터 손실을 불러 올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-368">Since a subset of properties may have been encrypted previously using a different key, simply merging the new properties and updating the metadata will result in data loss.</span></span> <span data-ttu-id="f9ec4-369">서비스에서 기존 엔터티를 읽을 수 있는 추가 서비스 호출을 수행 하거나 속성 당 새 키를 사용하는 것 모두에 성능상의 이유로 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-369">Merging either requires making extra service calls to read the pre-existing entity from the service, or using a new key per property, both of which are not suitable for performance reasons.</span></span>     

<span data-ttu-id="f9ec4-370">테이블 데이터를 암호화에 대한 정보는 [클라이언트측 암호화 및 Microsoft Azure 저장소에 대한 Azure 키 자격 증명 모음](../storage/common/storage-client-side-encryption.md)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-370">For information about encrypting table data, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../storage/common/storage-client-side-encryption.md).</span></span>  

## <a name="modelling-relationships"></a><span data-ttu-id="f9ec4-371">관계 모델링</span><span class="sxs-lookup"><span data-stu-id="f9ec4-371">Modelling relationships</span></span>
<span data-ttu-id="f9ec4-372">도메인 모델 빌드는 복잡한 시스템의 디자인에서 중요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-372">Building domain models is a key step in the design of complex systems.</span></span> <span data-ttu-id="f9ec4-373">일반적으로 엔터티와 해당 엔터티 간의 관계를 식별하는 모델링 프로세스를 사용하여 비즈니스 도메인을 이해하고 시스템 디자인에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-373">Typically, you use the modelling process to identify entities and the relationships between them as a way to understand the business domain and inform the design of your system.</span></span> <span data-ttu-id="f9ec4-374">이 섹션에서는 도메인 모델에서 일반적으로 발견되는 일부 관계 유형을 테이블 서비스의 디자인으로 변환하는 방법을 중점적으로 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-374">This section focuses on how you can translate some of the common relationship types found in domain models to designs for the Table service.</span></span> <span data-ttu-id="f9ec4-375">논리적 데이터 모델과 실제 NoSQL 기반 데이터 모델을 매핑하는 프로세스는 관계형 데이터베이스를 디자인할 때 사용되는 프로세스와 매우 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-375">The process of mapping from a logical data-model to a physical NoSQL based data-model is very different from that used when designing a relational database.</span></span> <span data-ttu-id="f9ec4-376">관계형 데이터베이스 디자인에서는 일반적으로 중복을 최소화하는 데 최적화된 데이터 정규화 프로세스 및 데이터베이스 작동 방식의 구현을 추상화하는 선언적 쿼리 기능을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-376">Relational databases design typically assumes a data normalization process optimized for minimizing redundancy – and a declarative querying capability that abstracts how the implementation of how the database works.</span></span>  

### <a name="one-to-many-relationships"></a><span data-ttu-id="f9ec4-377">일대다 관계</span><span class="sxs-lookup"><span data-stu-id="f9ec4-377">One-to-many relationships</span></span>
<span data-ttu-id="f9ec4-378">비즈니스 도메인 개체 간의 일대다 관계는 매우 빈번하게 발생합니다. 예를 들어 하나의 부서에 여러 직원이 있는 경우가 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-378">One-to-many relationships between business domain objects occur very frequently: for example, one department has many employees.</span></span> <span data-ttu-id="f9ec4-379">테이블 서비스에서 일대다 관계를 구현하는 방법에는 여러 가지가 있으며, 각 방법마다 특정 시나리오와 관련될 수 있는 장단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-379">There are several ways to implement one-to-many relationships in the Table service each with pros and cons that may be relevant to the particular scenario.</span></span>  

<span data-ttu-id="f9ec4-380">수만 개의 부서 및 직원 엔터티가 있고, 모든 부서에 여러 직원이 있으며, 각 직원이 하나의 특정 부서에 연결된 대규모 다국적 기업을 예로 들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-380">Consider the example of a large multi-national corporation with tens of thousands of departments and employee entities where every department has many employees and each employee as associated with one specific department.</span></span> <span data-ttu-id="f9ec4-381">별도의 부서 및 직원 엔터티를 저장하는 한 가지 접근 방식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-381">One approach is to store separate department and employee entities such as these:</span></span>  

![][1]

<span data-ttu-id="f9ec4-382">이 예는 **PartitionKey** 값을 기반으로 형식 간의 암시적 일대다의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-382">This example shows an implicit one-to-many relationship between the types based on the **PartitionKey** value.</span></span> <span data-ttu-id="f9ec4-383">각 부서에는 여러 직원이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-383">Each department can have many employees.</span></span>  

<span data-ttu-id="f9ec4-384">또한 이 예에서는 부서 엔터티와 해당 관련 직원 엔터티가 동일한 파티션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-384">This example also shows a department entity and its related employee entities in the same partition.</span></span> <span data-ttu-id="f9ec4-385">여러 엔터티 유형에 대해 서로 다른 파티션, 테이블 또는 저장소 계정을 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-385">You could choose to use different partitions, tables, or even storage accounts for the different entity types.</span></span>  

<span data-ttu-id="f9ec4-386">다른 접근 방식은 다음 예와 같이 데이터를 비정규화하고 비정규화된 부서가 있는 직원 엔터티만 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-386">An alternative approach is to denormalize your data and store only employee entities with denormalized department data as shown in the following example.</span></span> <span data-ttu-id="f9ec4-387">이 특정 시나리오에서는 부서 관리자 정보를 변경할 수 있어야 하는 요구 사항이 있는 경우 이 비정규화된 접근 방식이 적합하지 않을 수 있습니다. 부서 관리자 정보를 변경하려면 부서의 모든 직원을 업데이트해야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-387">In this particular scenario, this denormalized approach may not be the best if you have a requirement to be able to change the details of a department manager because to do this you need to update every employee in the department.</span></span>  

![][2]

<span data-ttu-id="f9ec4-388">자세한 내용은 이 가이드의 뒷부분에 있는 [비정규화 패턴](#denormalization-pattern) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-388">For more information, see the [Denormalization pattern](#denormalization-pattern) later in this guide.</span></span>  

<span data-ttu-id="f9ec4-389">다음 표에는 일대다 관계가 있는 직원 및 부서 엔터티를 저장하는 측면에서 위에 설명된 각 접근 방식의 장단점이 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-389">The following table summarizes the pros and cons of each of the approaches outlined above for storing employee and department entities that have a one-to-many relationship.</span></span> <span data-ttu-id="f9ec4-390">여러 작업을 수행할 빈도도 고려해야 합니다. 비용이 많이 드는 작업이 자주 발생하지 않는 경우에만 해당 작업을 디자인에 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-390">You should also consider how often you expect to perform various operations: it may be acceptable to have a design that includes an expensive operation if that operation only happens infrequently.</span></span>  

<table>
<tr>
<th><span data-ttu-id="f9ec4-391">접근 방식</span><span class="sxs-lookup"><span data-stu-id="f9ec4-391">Approach</span></span></th>
<th><span data-ttu-id="f9ec4-392">장점</span><span class="sxs-lookup"><span data-stu-id="f9ec4-392">Pros</span></span></th>
<th><span data-ttu-id="f9ec4-393">단점</span><span class="sxs-lookup"><span data-stu-id="f9ec4-393">Cons</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="f9ec4-394">별도의 엔터티 유형, 동일한 파티션, 동일한 테이블</span><span class="sxs-lookup"><span data-stu-id="f9ec4-394">Separate entity types, same partition, same table</span></span></td>
<td>
<ul>
<li><span data-ttu-id="f9ec4-395">단일 작업으로 부서 엔터티를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-395">You can update a department entity with a single operation.</span></span></li>
<li><span data-ttu-id="f9ec4-396">직원 엔터티를 업데이트/삽입/삭제할 때마다 부서 엔터티를 수정해야 하는 경우 EGT를 사용하여 일관성을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-396">You can use an EGT to maintain consistency if you have a requirement to modify a department entity whenever you update/insert/delete an employee entity.</span></span> <span data-ttu-id="f9ec4-397">예를 들어 각 부서의 직원 수를 유지 관리하는 경우가 여기에 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-397">For example if you maintain a departmental employee count for each department.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="f9ec4-398">일부 클라이언트 활동의 경우 직원 및 부서 엔터티를 둘 다 검색해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-398">You may need to retrieve both an employee and a department entity for some client activities.</span></span></li>
<li><span data-ttu-id="f9ec4-399">저장소 작업이 동일한 파티션에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-399">Storage operations happen in the same partition.</span></span> <span data-ttu-id="f9ec4-400">대용량 트랜잭션의 경우 핫스폿이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-400">At high transaction volumes, this may result in a hotspot.</span></span></li>
<li><span data-ttu-id="f9ec4-401">EGT를 사용하여 직원을 새 부서로 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-401">You cannot move an employee to a new department using an EGT.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="f9ec4-402">별도의 엔터티 유형, 서로 다른 파티션, 테이블 또는 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="f9ec4-402">Separate entity types, different partitions or tables or storage accounts</span></span></td>
<td>
<ul>
<li><span data-ttu-id="f9ec4-403">단일 작업으로 부서 엔터티 또는 직원 엔터티를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-403">You can update a department entity or employee entity with a single operation.</span></span></li>
<li><span data-ttu-id="f9ec4-404">대용량 트랜잭션의 경우 더 많은 파티션으로 부하를 분산할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-404">At high transaction volumes, this may help spread the load across more partitions.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="f9ec4-405">일부 클라이언트 활동의 경우 직원 및 부서 엔터티를 둘 다 검색해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-405">You may need to retrieve both an employee and a department entity for some client activities.</span></span></li>
<li><span data-ttu-id="f9ec4-406">직원을 업데이트/삽입/삭제하고 부서를 업데이트할 때 EGT를 사용하여 일관성을 유지할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-406">You cannot use EGTs to maintain consistency when you update/insert/delete an employee and update a department.</span></span> <span data-ttu-id="f9ec4-407">예를 들어 부서 엔터티의 직원 수를 업데이트하는 경우가 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-407">For example, updating an employee count in a department entity.</span></span></li>
<li><span data-ttu-id="f9ec4-408">EGT를 사용하여 직원을 새 부서로 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-408">You cannot move an employee to a new department using an EGT.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="f9ec4-409">단일 엔터티 유형으로 비정규화</span><span class="sxs-lookup"><span data-stu-id="f9ec4-409">Denormalize into single entity type</span></span></td>
<td>
<ul>
<li><span data-ttu-id="f9ec4-410">단일 요청으로 필요한 모든 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-410">You can retrieve all the information you need with a single request.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="f9ec4-411">부서 정보를 업데이트해야 하는 경우 일관성을 유지하는 데 많은 비용이 들 수 있습니다(부서의 모든 직원을 업데이트해야 함).</span><span class="sxs-lookup"><span data-stu-id="f9ec4-411">It may be expensive to maintain consistency if you need to update department information (this would require you to update all the employees in a department).</span></span></li>
</ul>
</td>
</tr>
</table>

<span data-ttu-id="f9ec4-412">이러한 옵션 간에 선택하는 방법 및 가장 중요한 장단점은 특정 응용 프로그램 시나리오에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-412">How you choose between these options, and which of the pros and cons are most significant, depends on your specific application scenarios.</span></span> <span data-ttu-id="f9ec4-413">예를 들어 부서 엔터티를 수정하는 빈도, 모든 직원 쿼리를 수행하는 데 추가 부서 정보가 필요한지 여부, 파티션 또는 저장소 계정의 확장성 제한에 얼마나 근접했는지 여부 등에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-413">For example, how often do you modify department entities; do all your employee queries need the additional departmental information; how close are you to the scalability limits on your partitions or your storage account?</span></span>  

### <a name="one-to-one-relationships"></a><span data-ttu-id="f9ec4-414">일대일 관계</span><span class="sxs-lookup"><span data-stu-id="f9ec4-414">One-to-one relationships</span></span>
<span data-ttu-id="f9ec4-415">도메인 모델은 엔터티 간의 일대일 관계를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-415">Domain models may include one-to-one relationships between entities.</span></span> <span data-ttu-id="f9ec4-416">테이블 서비스에서 일대일 관계를 구현해야 하는 경우 두 관련 엔터티를 모두 검색해야 할 때 해당 엔터티를 연결하는 방법도 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-416">If you need to implement a one-to-one relationship in the Table service, you must also choose how to link the two related entities when you need to retrieve them both.</span></span> <span data-ttu-id="f9ec4-417">이 링크는 키 값의 명명 규칙에 따라 암시적일 수 있으며, 각 엔터티의 **PartitionKey** 및 **RowKey** 값 형식으로 링크를 해당 관련 엔터티에 저장할 경우 명시적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-417">This link can be either implicit, based on a convention in the key values, or explicit by storing a link in the form of **PartitionKey** and **RowKey** values in each entity to its related entity.</span></span> <span data-ttu-id="f9ec4-418">관련 엔터티를 동일한 파티션에 저장해야 하는지 여부에 대한 자세한 내용은 [일대다 관계](#one-to-many-relationships)섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-418">For a discussion of whether you should store the related entities in the same partition, see the section [One-to-many relationships](#one-to-many-relationships).</span></span>  

<span data-ttu-id="f9ec4-419">테이블 서비스에서 일대일 관계를 구현하기 위한 구현 고려 사항도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-419">Note that there are also implementation considerations that might lead you to implement one-to-one relationships in the Table service:</span></span>  

* <span data-ttu-id="f9ec4-420">큰 엔터티 처리(자세한 내용은 [큰 엔터티 패턴](#large-entities-pattern)참조)</span><span class="sxs-lookup"><span data-stu-id="f9ec4-420">Handling large entities (for more information, see [Large Entities Pattern](#large-entities-pattern)).</span></span>  
* <span data-ttu-id="f9ec4-421">액세스 제어 구현(자세한 내용은 [공유 액세스 서명을 사용하여 액세스 제어](#controlling-access-with-shared-access-signatures)참조)</span><span class="sxs-lookup"><span data-stu-id="f9ec4-421">Implementing access controls (for more information, see [Controlling access with Shared Access Signatures](#controlling-access-with-shared-access-signatures)).</span></span>  

### <a name="join-in-the-client"></a><span data-ttu-id="f9ec4-422">클라이언트에 조인</span><span class="sxs-lookup"><span data-stu-id="f9ec4-422">Join in the client</span></span>
<span data-ttu-id="f9ec4-423">테이블 서비스에서 관계를 모델링하는 방법에는 여러 가지가 있지만 테이블 서비스를 사용하는 두 가지 주요 이유는 확장성과 성능이라는 점을 잊어서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-423">Although there are ways to model relationships in the Table service, you should not forget that the two prime reasons for using the Table service are scalability and performance.</span></span> <span data-ttu-id="f9ec4-424">솔루션의 성능 및 확장성을 저하시키는 많은 관계를 모델링할 경우 모든 데이터 관계를 테이블 디자인에 빌드할 필요가 있는지 자문해 보아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-424">If you find you are modelling many relationships that compromise the performance and scalability of your solution, you should ask yourself if it is necessary to build all the data relationships into your table design.</span></span> <span data-ttu-id="f9ec4-425">클라이언트 응용 프로그램에서 필요한 조인을 수행할 수 있도록 하면 디자인을 간소화하고 솔루션의 확장성 및 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-425">You may be able to simplify the design and improve the scalability and performance of your solution if you let your client application perform any necessary joins.</span></span>  

<span data-ttu-id="f9ec4-426">예를 들어 자주 변경되지 않는 데이터가 포함된 작은 테이블이 있는 경우 이 데이터를 한 번 검색하여 클라이언트에 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-426">For example, if you have small tables that contain data that does not change very often, then you can retrieve this data once and cache it on the client.</span></span> <span data-ttu-id="f9ec4-427">그러면 동일한 데이터를 검색하기 위한 반복 작업을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-427">This can avoid repeated roundtrips to retrieve the same data.</span></span> <span data-ttu-id="f9ec4-428">이 가이드에서 살펴본 예제에서는 소규모 조직의 부서 집합이 작고 자주 변경되지 않을 수 있으므로 클라이언트 응용 프로그램에서 한 번 다운로드하여 조회 데이터로 캐시할 수 있는 데이터로 적절합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-428">In the examples we have looked at in this guide, the set of departments in a small organization is likely to be small and change infrequently making it a good candidate for data that client application can download once and cache as look up data.</span></span>  

### <a name="inheritance-relationships"></a><span data-ttu-id="f9ec4-429">상속 관계</span><span class="sxs-lookup"><span data-stu-id="f9ec4-429">Inheritance relationships</span></span>
<span data-ttu-id="f9ec4-430">클라이언트 응용 프로그램에서 상속 관계의 일부를 구성하는 클래스 집합을 사용하여 비즈니스 엔터티를 나타내는 경우 테이블 서비스에서 이러한 엔터티를 쉽게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-430">If your client application uses a set of classes that form part of an inheritance relationship to represent business entities, you can easily persist those entities in the Table service.</span></span> <span data-ttu-id="f9ec4-431">예를 들어 **사람** 이 추상 클래스인 클라이언트 응용 프로그램에 다음과 같은 클래스 집합이 정의되어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-431">For example, you might have the following set of classes defined in your client application where **Person** is an abstract class.</span></span>

![][3]

<span data-ttu-id="f9ec4-432">다음과 같이 엔터티를 사용하는 단일 Person 테이블을 사용하여 테이블 서비스에서 구체적 클래스 두 개의 인스턴스를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-432">You can persist instances of the two concrete classes in the Table service using a single Person table using entities in that look like this:</span></span>  

![][4]

<span data-ttu-id="f9ec4-433">클라이언트 코드에서 동일한 테이블에 있는 여러 엔터티 형식으로 작업하는 방법에 대한 자세한 내용은 이 가이드의 뒷부분에 있는 [형식이 다른 엔터티 형식 작업](#working-with-heterogeneous-entity-types) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-433">For more information about working with multiple entity types in the same table in client code, see the section [Working with heterogeneous entity types](#working-with-heterogeneous-entity-types) later in this guide.</span></span> <span data-ttu-id="f9ec4-434">이 섹션에서는 클라이언트 코드에서 엔터티 유형을 인식하는 방법에 대한 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-434">This provides examples of how to recognize the entity type in client code.</span></span>  

## <a name="table-design-patterns"></a><span data-ttu-id="f9ec4-435">테이블 디자인 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-435">Table Design Patterns</span></span>
<span data-ttu-id="f9ec4-436">이전 섹션에서는 쿼리를 사용하여 엔터티 데이터를 검색하고 엔터티 데이터를 삽입, 업데이트 및 삭제하는 데 테이블 디자인을 최적화하는 방법에 대해 자세히 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-436">In previous sections, you have seen some detailed discussions about how to optimize your table design for both retrieving entity data using queries and for inserting, updating, and deleting entity data.</span></span> <span data-ttu-id="f9ec4-437">이 섹션에서는 테이블 서비스 솔루션에서 사용하기에 적합한 몇 가지 패턴에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-437">This section describes some patterns appropriate for use with Table service solutions.</span></span> <span data-ttu-id="f9ec4-438">또한 이 가이드의 앞부분에서 제기된 문제 및 장단점 중 일부를 실용적으로 해결할 수 있는 방법도 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-438">In addition, you will see how you can practically address some of the issues and trade-offs raised previously in this guide.</span></span> <span data-ttu-id="f9ec4-439">다음 다이어그램에는 서로 다른 패턴 간의 관계가 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-439">The following diagram summarizes the relationships between the different patterns:</span></span>  

![][5]

<span data-ttu-id="f9ec4-440">위 패턴 맵에는 이 가이드에 설명된 패턴(파란색)과 안티패턴(주황색) 간의 몇 가지 관계가 강조되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-440">The pattern map above highlights some relationships between patterns (blue) and anti-patterns (orange) that are documented in this guide.</span></span> <span data-ttu-id="f9ec4-441">물론 고려할 만한 다른 많은 패턴도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-441">There are of course many other patterns that are worth considering.</span></span> <span data-ttu-id="f9ec4-442">예를 들어 Table service의 주요 시나리오 중 하나는 [CQRS(Command Query Responsibility Segregation)](https://msdn.microsoft.com/library/azure/jj554200.aspx) 패턴에서 [구체화된 뷰 패턴](https://msdn.microsoft.com/library/azure/dn589782.aspx)을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-442">For example, one of the key scenarios for Table Service is to use the [Materialized View Pattern](https://msdn.microsoft.com/library/azure/dn589782.aspx) from the [Command Query Responsibility Segregation (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) pattern.</span></span>  

### <a name="intra-partition-secondary-index-pattern"></a><span data-ttu-id="f9ec4-443">파티션 간 보조 인덱스 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-443">Intra-partition secondary index pattern</span></span>
<span data-ttu-id="f9ec4-444">서로 다른 **RowKey** 값(동일한 파티션에서)을 사용하여 각 엔터티의 여러 복사본을 저장하여 빠르고 효율적인 조회를 지원하며, 서로 다른 **RowKey** 값을 사용하여 대체 정렬 순서를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-444">Store multiple copies of each entity using different **RowKey** values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span> <span data-ttu-id="f9ec4-445">EGT를 사용하여 복사본 간의 업데이트를 일관성 있게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-445">Updates between copies can be kept consistent using EGT's.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="f9ec4-446">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="f9ec4-446">Context and problem</span></span>
<span data-ttu-id="f9ec4-447">Table service는 **PartitionKey** 및 **RowKey** 값을 사용하여 엔터티를 자동으로 인덱싱합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-447">The Table service automatically indexes entities using the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="f9ec4-448">따라서 클라이언트 응용 프로그램이 이러한 값을 사용하여 엔터티를 효율적으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-448">This enables a client application to retrieve an entity efficiently using these values.</span></span> <span data-ttu-id="f9ec4-449">예를 들어 아래에 표시된 테이블 구조를 사용할 경우 클라이언트 응용 프로그램은 지점 쿼리를 사용하여 부서 이름 및 직원 ID(**PartitionKey** 및 **RowKey** 값)로 개별 직원 엔터티를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-449">For example, using the table structure shown below, a client application can use a point query to retrieve an individual employee entity by using the department name and the employee id (the **PartitionKey** and **RowKey** values).</span></span> <span data-ttu-id="f9ec4-450">또한 클라이언트는 각 부서 내에서 직원 ID별로 정렬된 엔터티를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-450">A client can also retrieve entities sorted by employee id within each department.</span></span>

![][6]

<span data-ttu-id="f9ec4-451">전자 메일 주소와 같은 다른 속성 값으로 기반으로 직원 엔터티를 찾을 수 있도록 하려면 비효율적인 파티션 검색을 사용하여 일치하는 항목을 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-451">If you also want to be able to find an employee entity based on the value of another property, such as email address, you must use a less efficient partition scan to find a match.</span></span> <span data-ttu-id="f9ec4-452">테이블 서비스에서는 보조 인덱스를 제공하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-452">This is because the table service does not provide secondary indexes.</span></span> <span data-ttu-id="f9ec4-453">또한 **RowKey** 와 다른 순서로 정렬된 직원 목록을 요청하는 옵션도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-453">In addition, there is no option to request a list of employees sorted in a different order than **RowKey** order.</span></span>  

#### <a name="solution"></a><span data-ttu-id="f9ec4-454">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f9ec4-454">Solution</span></span>
<span data-ttu-id="f9ec4-455">보조 인덱스가 없는 문제를 해결하려면 각 엔터티의 여러 복사본을 다른 **RowKey** 값을 사용하는 각 복사본과 함께 저장하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-455">To work around the lack of secondary indexes, you can store multiple copies of each entity with each copy using a different **RowKey** value.</span></span> <span data-ttu-id="f9ec4-456">아래에 표시된 구조로 엔터티를 저장하면 전자 메일 주소 또는 직원 ID를 기반으로 직원 엔터티를 효율적으로 검색할 수 있습니다. **RowKey**의 접두사 값 "empid_" 및 "email_"은 전자 메일 주소 또는 직원 ID의 범위를 사용하여 단일 직원 또는 직원 범위를 쿼리할 수 있도록 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-456">If you store an entity with the structures shown below, you can efficiently retrieve employee entities based on email address or employee id. The prefix values for the **RowKey**, "empid_" and "email_" enable you to query for a single employee or a range of employees by using a range of email addresses or employee ids.</span></span>  

![][7]

<span data-ttu-id="f9ec4-457">다음 두 필터 조건(직원 ID로 조회하는 필터와 전자 메일 주소로 조회하는 필터)은 모두 지점 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-457">The following two filter criteria (one looking up by employee id and one looking up by email address) both specify point queries:</span></span>  

* <span data-ttu-id="f9ec4-458">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'empid_000223')</span><span class="sxs-lookup"><span data-stu-id="f9ec4-458">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'empid_000223')</span></span>  
* <span data-ttu-id="f9ec4-459">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'email_jonesj@contoso.com')</span><span class="sxs-lookup"><span data-stu-id="f9ec4-459">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'email_jonesj@contoso.com')</span></span>  

<span data-ttu-id="f9ec4-460">직원 엔터티 범위를 쿼리하는 경우 **RowKey**의 해당 접두사로 엔터티를 쿼리하여 직원 ID 순으로 정렬된 범위 또는 전자 메일 주소 순으로 정렬된 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-460">If you query for a range of employee entities, you can specify a range sorted in employee id order, or a range sorted in email address order by querying for entities with the appropriate prefix in the **RowKey**.</span></span>  

* <span data-ttu-id="f9ec4-461">Sales 부서에서 직원 ID 범위가 000100~000199인 모든 직원을 찾으려면 다음을 사용합니다. $filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000100') and (RowKey le 'empid_000199')</span><span class="sxs-lookup"><span data-stu-id="f9ec4-461">To find all the employees in the Sales department with an employee id in the range 000100 to 000199 use: $filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000100') and (RowKey le 'empid_000199')</span></span>  
* <span data-ttu-id="f9ec4-462">Sales 부서에서 이메일 주소가 'a'로 시작하는 모든 직원을 찾으려면 다음을 사용합니다. $filter=(PartitionKey eq 'Sales') and (RowKey ge 'email_a') and (RowKey lt 'email_b')</span><span class="sxs-lookup"><span data-stu-id="f9ec4-462">To find all the employees in the Sales department with an email address starting with the letter 'a' use: $filter=(PartitionKey eq 'Sales') and (RowKey ge 'email_a') and (RowKey lt 'email_b')</span></span>  
  
  <span data-ttu-id="f9ec4-463">위 예제에 사용된 필터 구문은 테이블 서비스 REST API에서 가져온 것입니다(자세한 내용은 [엔터티 쿼리](http://msdn.microsoft.com/library/azure/dd179421.aspx)참조).</span><span class="sxs-lookup"><span data-stu-id="f9ec4-463">Note that the filter syntax used in the examples above is from the Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="f9ec4-464">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f9ec4-464">Issues and considerations</span></span>
<span data-ttu-id="f9ec4-465">이 패턴을 구현할 방법을 결정할 때 다음 사항을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-465">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="f9ec4-466">테이블 저장소는 비교적 저렴하게 사용할 수 있으므로 중복 데이터 저장에 대한 비용 오버헤드가 주요 관심사여서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-466">Table storage is relatively cheap to use so the cost overhead of storing duplicate data should not be a major concern.</span></span> <span data-ttu-id="f9ec4-467">그러나 항상 예상된 저장소 요구 사항을 기반으로 디자인 비용을 평가하고, 클라이언트 응용 프로그램에서 실행할 쿼리를 지원하는 데 필요한 경우에만 중복 엔터티를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-467">However, you should always evaluate the cost of your design based on your anticipated storage requirements and only add duplicate entities to support the queries your client application will execute.</span></span>  
* <span data-ttu-id="f9ec4-468">보조 인덱스 엔터티는 원래 엔터티와 동일한 파티션에 저장되므로 개별 파티션의 확장성 목표를 초과하지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-468">Because the secondary index entities are stored in the same partition as the original entities, you should ensure that you do not exceed the scalability targets for an individual partition.</span></span>  
* <span data-ttu-id="f9ec4-469">EGT를 사용하여 엔터티의 두 복사본을 원자성으로 업데이트하는 방식으로 중복 엔터티를 서로 일관성 있게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-469">You can keep your duplicate entities consistent with each other by using EGTs to update the two copies of the entity atomically.</span></span> <span data-ttu-id="f9ec4-470">이는 엔터티의 모든 복사본을 동일한 파티션에 저장해야 함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-470">This implies that you should store all copies of an entity in the same partition.</span></span> <span data-ttu-id="f9ec4-471">자세한 내용은 [엔터티 그룹 트랜잭션 사용](#entity-group-transactions)섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-471">For more information, see the section [Using Entity Group Transactions](#entity-group-transactions).</span></span>  
* <span data-ttu-id="f9ec4-472">**RowKey** 에 사용된 값은 각 엔터티마다 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-472">The value used for the **RowKey** must be unique for each entity.</span></span> <span data-ttu-id="f9ec4-473">복합 키 값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-473">Consider using compound key values.</span></span>  
* <span data-ttu-id="f9ec4-474">**RowKey** 의 숫자 값을 채우면(예: 직원 ID 000223) 상한 및 하한에 따라 올바르게 정렬 및 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-474">Padding numeric values in the **RowKey** (for example, the employee id 000223), enables correct sorting and filtering based on upper and lower bounds.</span></span>  
* <span data-ttu-id="f9ec4-475">엔터티의 모든 속성을 복제할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-475">You do not necessarily need to duplicate all the properties of your entity.</span></span> <span data-ttu-id="f9ec4-476">예를 들어 **RowKey**에서 전자 메일 주소를 사용하여 엔터티를 조회하는 쿼리에 직원의 나이가 필요 없는 경우 이러한 엔터티의 구조는 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-476">For example, if the queries that lookup the entities using the email address in the **RowKey** never need the employee's age, these entities could have the following structure:</span></span>

![][8]

* <span data-ttu-id="f9ec4-477">일반적으로 중복 데이터를 저장하고 단일 쿼리로 필요한 모든 데이터를 검색할 수 있도록 하는 것이 하나의 쿼리를 사용하여 엔터티를 찾고 다른 쿼리를 사용하여 필요한 데이터를 조회하는 것보다 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-477">It is typically better to store duplicate data and ensure that you can retrieve all the data you need with a single query, than to use one query to locate an entity and another to lookup the required data.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="f9ec4-478">이 패턴을 사용해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="f9ec4-478">When to use this pattern</span></span>
<span data-ttu-id="f9ec4-479">클라이언트 응용 프로그램에서 다양한 키를 사용하여 엔터티를 검색해야 하는 경우, 클라이언트에서 다른 정렬 순서로 엔터티를 검색해야 하는 경우, 다양한 고유 값을 사용하여 각 엔터티를 식별할 수 있는 경우 등에 이 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-479">Use this pattern when your client application needs to retrieve entities using a variety of different keys, when your client needs to retrieve entities in different sort orders, and where you can identify each entity using a variety of unique values.</span></span> <span data-ttu-id="f9ec4-480">그러나 다른 **RowKey** 값을 사용하여 엔터티 조회를 수행할 때는 파티션 확장성 제한을 초과하지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-480">However, you should be sure that you do not exceed the partition scalability limits when you are performing entity lookups using the different **RowKey** values.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="f9ec4-481">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="f9ec4-481">Related patterns and guidance</span></span>
<span data-ttu-id="f9ec4-482">이 패턴을 구현할 때 다음 패턴 및 지침도 관련이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-482">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="f9ec4-483">파티션 내 보조 인덱스 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-483">Inter-partition secondary index pattern</span></span>](#inter-partition-secondary-index-pattern)
* [<span data-ttu-id="f9ec4-484">복합 키 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-484">Compound key pattern</span></span>](#compound-key-pattern)
* [<span data-ttu-id="f9ec4-485">엔터티 그룹 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="f9ec4-485">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="f9ec4-486">유형이 다른 엔터티 유형 작업</span><span class="sxs-lookup"><span data-stu-id="f9ec4-486">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)

### <a name="inter-partition-secondary-index-pattern"></a><span data-ttu-id="f9ec4-487">파티션 간 보조 인덱스 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-487">Inter-partition secondary index pattern</span></span>
<span data-ttu-id="f9ec4-488">서로 다른 **RowKey** 값을 사용하여 각 엔터티의 여러 복사본을 별도의 파티션 또는 별도의 테이블에 저장하여 빠르고 효율적인 조회를 지원하며, 서로 다른 **RowKey** 값을 사용하여 대체 정렬 순서를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-488">Store multiple copies of each entity using different **RowKey** values in separate partitions or in separate tables to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="f9ec4-489">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="f9ec4-489">Context and problem</span></span>
<span data-ttu-id="f9ec4-490">Table service는 **PartitionKey** 및 **RowKey** 값을 사용하여 엔터티를 자동으로 인덱싱합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-490">The Table service automatically indexes entities using the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="f9ec4-491">따라서 클라이언트 응용 프로그램이 이러한 값을 사용하여 엔터티를 효율적으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-491">This enables a client application to retrieve an entity efficiently using these values.</span></span> <span data-ttu-id="f9ec4-492">예를 들어 아래에 표시된 테이블 구조를 사용할 경우 클라이언트 응용 프로그램은 지점 쿼리를 사용하여 부서 이름 및 직원 ID(**PartitionKey** 및 **RowKey** 값)로 개별 직원 엔터티를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-492">For example, using the table structure shown below, a client application can use a point query to retrieve an individual employee entity by using the department name and the employee id (the **PartitionKey** and **RowKey** values).</span></span> <span data-ttu-id="f9ec4-493">또한 클라이언트는 각 부서 내에서 직원 ID별로 정렬된 엔터티를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-493">A client can also retrieve entities sorted by employee id within each department.</span></span>  

![][9]

<span data-ttu-id="f9ec4-494">전자 메일 주소와 같은 다른 속성 값으로 기반으로 직원 엔터티를 찾을 수 있도록 하려면 비효율적인 파티션 검색을 사용하여 일치하는 항목을 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-494">If you also want to be able to find an employee entity based on the value of another property, such as email address, you must use a less efficient partition scan to find a match.</span></span> <span data-ttu-id="f9ec4-495">테이블 서비스에서는 보조 인덱스를 제공하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-495">This is because the table service does not provide secondary indexes.</span></span> <span data-ttu-id="f9ec4-496">또한 **RowKey** 와 다른 순서로 정렬된 직원 목록을 요청하는 옵션도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-496">In addition, there is no option to request a list of employees sorted in a different order than **RowKey** order.</span></span>  

<span data-ttu-id="f9ec4-497">이러한 엔터티에 대한 트랜잭션 볼륨이 매우 클 것으로 예상되는 경우 클라이언트를 제한하여 테이블 서비스의 위험을 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-497">You are anticipating a very high volume of transactions against these entities and want to minimize the risk of the Table service throttling your client.</span></span>  

#### <a name="solution"></a><span data-ttu-id="f9ec4-498">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f9ec4-498">Solution</span></span>
<span data-ttu-id="f9ec4-499">보조 인덱스가 없는 문제를 해결하려면 각 엔터티의 여러 복사본을 다른 **PartitionKey** 및 **RowKey** 값을 사용하는 각 복사본과 함께 저장하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-499">To work around the lack of secondary indexes, you can store multiple copies of each entity with each copy using different **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="f9ec4-500">아래에 표시된 구조로 엔터티를 저장하면 전자 메일 주소 또는 직원 ID를 기반으로 직원 엔터티를 효율적으로 검색할 수 있습니다. **PartitionKey**의 접두사 값 "empid_" 및 "email_"은 쿼리에 사용할 수 있는 인덱스를 구분할 수 있도록 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-500">If you store an entity with the structures shown below, you can efficiently retrieve employee entities based on email address or employee id. The prefix values for the **PartitionKey**, "empid_" and "email_" enable you to identify which index you want to use for a query.</span></span>  

![][10]

<span data-ttu-id="f9ec4-501">다음 두 필터 조건(직원 ID로 조회하는 필터와 전자 메일 주소로 조회하는 필터)은 모두 지점 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-501">The following two filter criteria (one looking up by employee id and one looking up by email address) both specify point queries:</span></span>  

* <span data-ttu-id="f9ec4-502">$filter=(PartitionKey eq 'empid_Sales') and (RowKey eq '000223')</span><span class="sxs-lookup"><span data-stu-id="f9ec4-502">$filter=(PartitionKey eq 'empid_Sales') and (RowKey eq '000223')</span></span>
* <span data-ttu-id="f9ec4-503">$filter=(PartitionKey eq 'email_Sales') and (RowKey eq 'jonesj@contoso.com')</span><span class="sxs-lookup"><span data-stu-id="f9ec4-503">$filter=(PartitionKey eq 'email_Sales') and (RowKey eq 'jonesj@contoso.com')</span></span>  

<span data-ttu-id="f9ec4-504">직원 엔터티 범위를 쿼리하는 경우 **RowKey**의 해당 접두사로 엔터티를 쿼리하여 직원 ID 순으로 정렬된 범위 또는 전자 메일 주소 순으로 정렬된 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-504">If you query for a range of employee entities, you can specify a range sorted in employee id order, or a range sorted in email address order by querying for entities with the appropriate prefix in the **RowKey**.</span></span>  

* <span data-ttu-id="f9ec4-505">Sales 부서에서 직원 ID 순으로 정렬하여 직원 ID 범위가 **000100**~**000199**인 모든 직원을 찾으려면 다음을 사용합니다. $filter=(PartitionKey eq 'empid_Sales') and (RowKey ge '000100') and (RowKey le '000199')</span><span class="sxs-lookup"><span data-stu-id="f9ec4-505">To find all the employees in the Sales department with an employee id in the range **000100** to **000199** sorted in employee id order use: $filter=(PartitionKey eq 'empid_Sales') and (RowKey ge '000100') and (RowKey le '000199')</span></span>  
* <span data-ttu-id="f9ec4-506">Sales 부서에서 직원 이메일 주소순으로 정렬하여 이메일 주소가 'a'로 시작하는 모든 직원을 찾으려면 다음을 사용합니다. $filter=(PartitionKey eq 'email_Sales') and (RowKey ge 'a') and (RowKey lt 'b')</span><span class="sxs-lookup"><span data-stu-id="f9ec4-506">To find all the employees in the Sales department with an email address that starts with 'a' sorted in email address order use: $filter=(PartitionKey eq 'email_Sales') and (RowKey ge 'a') and (RowKey lt 'b')</span></span>  

<span data-ttu-id="f9ec4-507">위 예제에 사용된 필터 구문은 테이블 서비스 REST API에서 가져온 것입니다(자세한 내용은 [엔터티 쿼리](http://msdn.microsoft.com/library/azure/dd179421.aspx)참조).</span><span class="sxs-lookup"><span data-stu-id="f9ec4-507">Note that the filter syntax used in the examples above is from the Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="f9ec4-508">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f9ec4-508">Issues and considerations</span></span>
<span data-ttu-id="f9ec4-509">이 패턴을 구현할 방법을 결정할 때 다음 사항을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-509">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="f9ec4-510">[결과적으로 일관성 있는 트랜잭션 패턴](#eventually-consistent-transactions-pattern) 을 사용하여 주 인덱스 엔터티 및 보조 인덱스 엔터티를 유지 관리함으로써 중복 엔터티를 서로 일관성 있게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-510">You can keep your duplicate entities eventually consistent with each other by using the [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) to maintain the primary and secondary index entities.</span></span>  
* <span data-ttu-id="f9ec4-511">테이블 저장소는 비교적 저렴하게 사용할 수 있으므로 중복 데이터 저장에 대한 비용 오버헤드가 주요 관심사여서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-511">Table storage is relatively cheap to use so the cost overhead of storing duplicate data should not be a major concern.</span></span> <span data-ttu-id="f9ec4-512">그러나 항상 예상된 저장소 요구 사항을 기반으로 디자인 비용을 평가하고, 클라이언트 응용 프로그램에서 실행할 쿼리를 지원하는 데 필요한 경우에만 중복 엔터티를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-512">However, you should always evaluate the cost of your design based on your anticipated storage requirements and only add duplicate entities to support the queries your client application will execute.</span></span>  
* <span data-ttu-id="f9ec4-513">**RowKey** 에 사용된 값은 각 엔터티마다 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-513">The value used for the **RowKey** must be unique for each entity.</span></span> <span data-ttu-id="f9ec4-514">복합 키 값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-514">Consider using compound key values.</span></span>  
* <span data-ttu-id="f9ec4-515">**RowKey** 의 숫자 값을 채우면(예: 직원 ID 000223) 상한 및 하한에 따라 올바르게 정렬 및 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-515">Padding numeric values in the **RowKey** (for example, the employee id 000223), enables correct sorting and filtering based on upper and lower bounds.</span></span>  
* <span data-ttu-id="f9ec4-516">엔터티의 모든 속성을 복제할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-516">You do not necessarily need to duplicate all the properties of your entity.</span></span> <span data-ttu-id="f9ec4-517">예를 들어 **RowKey**에서 전자 메일 주소를 사용하여 엔터티를 조회하는 쿼리에 직원의 나이가 필요 없는 경우 이러한 엔터티의 구조는 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-517">For example, if the queries that lookup the entities using the email address in the **RowKey** never need the employee's age, these entities could have the following structure:</span></span>
  
  ![][11]
* <span data-ttu-id="f9ec4-518">일반적으로 중복 데이터를 저장하고 단일 쿼리로 필요한 모든 데이터를 검색할 수 있도록 하는 것이 하나의 쿼리를 사용하여 보조 인덱스에서 엔터티를 찾고 다른 쿼리를 사용하여 기본 인덱스에서 필요한 데이터를 조회하는 것보다 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-518">It is typically better to store duplicate data and ensure that you can retrieve all the data you need with a single query than to use one query to locate an entity using the secondary index and another to lookup the required data in the primary index.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="f9ec4-519">이 패턴을 사용해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="f9ec4-519">When to use this pattern</span></span>
<span data-ttu-id="f9ec4-520">클라이언트 응용 프로그램에서 다양한 키를 사용하여 엔터티를 검색해야 하는 경우, 클라이언트에서 다른 정렬 순서로 엔터티를 검색해야 하는 경우, 다양한 고유 값을 사용하여 각 엔터티를 식별할 수 있는 경우 등에 이 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-520">Use this pattern when your client application needs to retrieve entities using a variety of different keys, when your client needs to retrieve entities in different sort orders, and where you can identify each entity using a variety of unique values.</span></span> <span data-ttu-id="f9ec4-521">다른 **RowKey** 값을 사용하여 엔터티 조회를 수행할 때는 파티션 확장성 제한을 초과하지 않도록 하려는 경우에 이 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-521">Use this pattern when you want to avoid exceeding the partition scalability limits when you are performing entity lookups using the different **RowKey** values.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="f9ec4-522">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="f9ec4-522">Related patterns and guidance</span></span>
<span data-ttu-id="f9ec4-523">이 패턴을 구현할 때 다음 패턴 및 지침도 관련이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-523">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="f9ec4-524">결과적으로 일관성 있는 트랜잭션 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-524">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="f9ec4-525">파티션 간 보조 인덱스 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-525">Intra-partition secondary index pattern</span></span>](#intra-partition-secondary-index-pattern)  
* [<span data-ttu-id="f9ec4-526">복합 키 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-526">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="f9ec4-527">엔터티 그룹 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="f9ec4-527">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="f9ec4-528">유형이 다른 엔터티 유형 작업</span><span class="sxs-lookup"><span data-stu-id="f9ec4-528">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="eventually-consistent-transactions-pattern"></a><span data-ttu-id="f9ec4-529">결과적으로 일관성 있는 트랜잭션 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-529">Eventually consistent transactions pattern</span></span>
<span data-ttu-id="f9ec4-530">Azure 큐를 사용하여 파티션 경계 또는 저장소 시스템 경계 간에 결과적으로 일관성 있는 동작을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-530">Enable eventually consistent behavior across partition boundaries or storage system boundaries by using Azure queues.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="f9ec4-531">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="f9ec4-531">Context and problem</span></span>
<span data-ttu-id="f9ec4-532">EGT는 동일한 파티션 키를 공유하는 여러 엔터티 간의 원자성 트랜잭션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-532">EGTs enable atomic transactions across multiple entities that share the same partition key.</span></span> <span data-ttu-id="f9ec4-533">성능 및 확장성 때문에, 일관성 요구 사항이 있는 엔터티를 별도의 파티션 또는 별도의 저장소 시스템에 저장해야 할 수 있습니다. 이 시나리오에서는 EGT를 사용하여 일관성을 유지할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-533">For performance and scalability reasons, you might decide to store entities that have consistency requirements in separate partitions or in a separate storage system: in such a scenario, you cannot use EGTs to maintain consistency.</span></span> <span data-ttu-id="f9ec4-534">예를 들어 다음 엔터티 간에 결과적 일관성을 유지해야 하는 요구 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-534">For example, you might have a requirement to maintain eventual consistency between:</span></span>  

* <span data-ttu-id="f9ec4-535">동일한 테이블, 서로 다른 테이블 또는 서로 다른 저장소 계정의 두 파티션에 저장된 엔터티</span><span class="sxs-lookup"><span data-stu-id="f9ec4-535">Entities stored in two different partitions in the same table, in different tables, in in different storage accounts.</span></span>  
* <span data-ttu-id="f9ec4-536">테이블 서비스에 저장된 엔터티와 Blob 서비스에 저장된 Blob</span><span class="sxs-lookup"><span data-stu-id="f9ec4-536">An entity stored in the Table service and a blob stored in the Blob service.</span></span>  
* <span data-ttu-id="f9ec4-537">테이블 서비스에 저장된 엔터티와 파일 서비스에 저장된 파일</span><span class="sxs-lookup"><span data-stu-id="f9ec4-537">An entity stored in the Table service and a file in a file system.</span></span>  
* <span data-ttu-id="f9ec4-538">Azure 검색 서비스를 사용하여 아직 인덱싱되지 않은 테이블 서비스에 저장된 엔터티</span><span class="sxs-lookup"><span data-stu-id="f9ec4-538">An entity store in the Table service yet indexed using the Azure Search service.</span></span>  

#### <a name="solution"></a><span data-ttu-id="f9ec4-539">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f9ec4-539">Solution</span></span>
<span data-ttu-id="f9ec4-540">Azure 큐를 사용하면 둘 이상의 파티션 또는 저장소 시스템 간에 결과적 일관성을 유지하는 솔루션을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-540">By using Azure queues, you can implement a solution that delivers eventual consistency across two or more partitions or storage systems.</span></span>
<span data-ttu-id="f9ec4-541">이 접근 방식을 설명하기 위해 이전 직원 엔터티를 보관할 수 있어야 하는 요구 사항이 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-541">To illustrate this approach, assume you have a requirement to be able to archive old employee entities.</span></span> <span data-ttu-id="f9ec4-542">이전 직원 엔터티는 거의 쿼리되지 않으므로 현재 직원을 다루는 활동에서 제외해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-542">Old employee entities are rarely queried and should be excluded from any activities that deal with current employees.</span></span> <span data-ttu-id="f9ec4-543">이 요구 사항을 구현하기 위해 현재 직원을 **현재** 테이블에 저장하고 이전 직원을 **보관** 테이블에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-543">To implement this requirement you store active employees in the **Current** table and old employees in the **Archive** table.</span></span> <span data-ttu-id="f9ec4-544">직원을 보관하려면 **현재** 테이블에서 해당 엔터티를 삭제하고 **보관** 테이블에 엔터티를 추가해야 하지만 EGT를 사용하여 이 두 작업을 수행할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-544">Archiving an employee requires you to delete the entity from the **Current** table and add the entity to the **Archive** table, but you cannot use an EGT to perform these two operations.</span></span> <span data-ttu-id="f9ec4-545">오류로 인해 하나의 엔터티가 두 테이블 모두에 표시되거나 아무 테이블에도 표시되지 않는 위험을 방지하려면 보관 작업이 결과적으로 일관성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-545">To avoid the risk that a failure causes an entity to appear in both or neither tables, the archive operation must be eventually consistent.</span></span> <span data-ttu-id="f9ec4-546">다음 시퀀스 다이어그램에 이 작업의 단계가 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-546">The following sequence diagram outlines the steps in this operation.</span></span> <span data-ttu-id="f9ec4-547">다음 텍스트에 예외 경로에 대한 자세한 정보가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-547">More detail is provided for exception paths in the text following.</span></span>  

![][12]

<span data-ttu-id="f9ec4-548">클라이언트가 메시지를 Azure 큐에 추가하여 보관 작업을 시작합니다(이 예제의 경우 employee #456 보관).</span><span class="sxs-lookup"><span data-stu-id="f9ec4-548">A client initiates the archive operation by placing a message on an Azure queue, in this example to archive employee #456.</span></span> <span data-ttu-id="f9ec4-549">작업자 역할이 새 메시지에 대해 큐를 폴링합니다. 새 메시지를 찾은 경우 메시지를 읽고 숨겨진 복사본을 큐에 남겨 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-549">A worker role polls the queue for new messages; when it finds one, it reads the message and leaves a hidden copy on the queue.</span></span> <span data-ttu-id="f9ec4-550">작업자 역할이 **현재** 테이블에서 엔터티의 복사본을 가져와 **보관** 테이블에 삽입한 다음 **현재** 테이블에서 원래 엔터티를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-550">The worker role next fetches a copy of the entity from the **Current** table, inserts a copy in the **Archive** table, and then deletes the original from the **Current** table.</span></span> <span data-ttu-id="f9ec4-551">마지막으로 이전 단계에서 오류가 발생하지 않은 경우 작업자 역할이 큐에서 숨겨진 메시지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-551">Finally, if there were no errors from the previous steps, the worker role deletes the hidden message from the queue.</span></span>  

<span data-ttu-id="f9ec4-552">이 예제의 4단계에서는 직원을 **보관** 테이블에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-552">In this example, step 4 inserts the employee into the **Archive** table.</span></span> <span data-ttu-id="f9ec4-553">Blob 서비스의 Blob 또는 파일 시스템의 파일에 직원을 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-553">It could add the employee to a blob in the Blob service or a file in a file system.</span></span>  

#### <a name="recovering-from-failures"></a><span data-ttu-id="f9ec4-554">오류 복구</span><span class="sxs-lookup"><span data-stu-id="f9ec4-554">Recovering from failures</span></span>
<span data-ttu-id="f9ec4-555">작업자 역할이 보관 작업을 다시 시작해야 하는 것일 경우 **4**단계 및 **5**단계의 작업은 *멱등원*이어야 하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-555">It is important that the operations in steps **4** and **5** must be *idempotent* in case the worker role needs to restart the archive operation.</span></span> <span data-ttu-id="f9ec4-556">Table service를 사용하는 경우 **4**단계에서는 "삽입 또는 바꾸기" 작업을 사용하고, **5**단계에서는 사용 중인 클라이언트 라이브러리에서 "있는 경우 삭제" 작업을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-556">If you are using the Table service, for step **4** you should use an "insert or replace" operation; for step **5** you should use a "delete if exists" operation in the client library you are using.</span></span> <span data-ttu-id="f9ec4-557">다른 저장소 시스템을 사용하는 경우에는 적절한 idempotent 작업을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-557">If you are using another storage system, you must use an appropriate idempotent operation.</span></span>  

<span data-ttu-id="f9ec4-558">작업자 역할이 **6**단계를 완료하지 못한 경우에는 시간 초과 후 작업자 역할이 작업을 다시 처리할 수 있도록 준비된 큐에 메시지가 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-558">If the worker role never completes step **6**, then after a timeout the message reappears on the queue ready for the worker role to try to reprocess it.</span></span> <span data-ttu-id="f9ec4-559">작업자 역할은 큐의 메시지를 읽은 횟수를 확인할 수 있으며, 필요한 경우 별도의 큐로 보내 조사할 수 있도록 "포이즌" 메시지라는 플래그를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-559">The worker role can check how many times a message on the queue has been read and, if necessary, flag it is a "poison" message for investigation by sending it to a separate queue.</span></span> <span data-ttu-id="f9ec4-560">큐 메시지 읽기 및 큐에서 제거한 횟수 확인에 대한 자세한 내용은 [메시지 가져오기](https://msdn.microsoft.com/library/azure/dd179474.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-560">For more information about reading queue messages and checking the dequeue count, see [Get Messages](https://msdn.microsoft.com/library/azure/dd179474.aspx).</span></span>  

<span data-ttu-id="f9ec4-561">테이블 및 큐 서비스의 일부 오류는 일시적 오류이므로 클라이언트 응용 프로그램에 이를 처리할 수 있는 적절한 재시도 논리가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-561">Some errors from the Table and Queue services are transient errors, and your client application should include suitable retry logic to handle them.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="f9ec4-562">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f9ec4-562">Issues and considerations</span></span>
<span data-ttu-id="f9ec4-563">이 패턴을 구현할 방법을 결정할 때 다음 사항을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-563">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="f9ec4-564">이 솔루션은 트랜잭션 격리를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-564">This solution does not provide for transaction isolation.</span></span> <span data-ttu-id="f9ec4-565">예를 들어 작업자 역할이 **4**단계와 **5**단계 사이에 있을 때 클라이언트가 **현재** 및 **보관** 테이블을 읽으면 일관성 없는 데이터 뷰가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-565">For example, a client could read the **Current** and **Archive** tables when the worker role was between steps **4** and **5**, and see an inconsistent view of the data.</span></span> <span data-ttu-id="f9ec4-566">데이터는 결과적으로 일관성이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-566">Note that the data will be consistent eventually.</span></span>  
* <span data-ttu-id="f9ec4-567">결과적 일관성을 유지하려면 4단계와 5단계가 idempotent여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-567">You must be sure that steps 4 and 5 are idempotent in order to ensure eventual consistency.</span></span>  
* <span data-ttu-id="f9ec4-568">여러 큐 및 작업자 역할 인스턴스를 사용하여 솔루션을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-568">You can scale the solution by using multiple queues and worker role instances.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="f9ec4-569">이 패턴을 사용해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="f9ec4-569">When to use this pattern</span></span>
<span data-ttu-id="f9ec4-570">서로 다른 파티션 또는 테이블에 있는 엔터티 간의 결과적 일관성을 보장하려는 경우에 이 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-570">Use this pattern when you want to guarantee eventual consistency between entities that exist in different partitions or tables.</span></span> <span data-ttu-id="f9ec4-571">이 패턴을 확장하여 테이블 서비스와 Blob 서비스 및 Azure가 아닌 다른 저장소 데이터 원본(예: 데이터베이스 또는 파일 시스템) 간의 작업에 대한 결과적 일관성을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-571">You can extend this pattern to ensure eventual consistency for operations across the Table service and the Blob service and other non-Azure Storage data sources such as database or the file system.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="f9ec4-572">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="f9ec4-572">Related patterns and guidance</span></span>
<span data-ttu-id="f9ec4-573">이 패턴을 구현할 때 다음 패턴 및 지침도 관련이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-573">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="f9ec4-574">엔터티 그룹 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="f9ec4-574">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="f9ec4-575">병합 또는 바꾸기</span><span class="sxs-lookup"><span data-stu-id="f9ec4-575">Merge or replace</span></span>](#merge-or-replace)  

> [!NOTE]
> <span data-ttu-id="f9ec4-576">트랜잭션 격리가 솔루션에 중요한 경우 EGT를 사용할 수 있도록 테이블을 다시 디자인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-576">If transaction isolation is important to your solution, you should consider redesigning your tables to enable you to use EGTs.</span></span>  
> 
> 

### <a name="index-entities-pattern"></a><span data-ttu-id="f9ec4-577">인덱스 엔터티 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-577">Index Entities Pattern</span></span>
<span data-ttu-id="f9ec4-578">인덱스 엔터티를 유지 관리하여 엔터티 목록을 반환하는 효율적인 검색을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-578">Maintain index entities to enable efficient searches that return lists of entities.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="f9ec4-579">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="f9ec4-579">Context and problem</span></span>
<span data-ttu-id="f9ec4-580">Table service는 **PartitionKey** 및 **RowKey** 값을 사용하여 엔터티를 자동으로 인덱싱합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-580">The Table service automatically indexes entities using the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="f9ec4-581">따라서 클라이언트 응용 프로그램이 지점 쿼리를 사용하여 엔터티를 효율적으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-581">This enables a client application to retrieve an entity efficiently using a point query.</span></span> <span data-ttu-id="f9ec4-582">예를 들어 아래에 표시된 테이블 구조를 사용할 경우 클라이언트 응용 프로그램은 부서 이름 및 직원 ID(**PartitionKey** 및 **RowKey**)를 사용하여 개별 직원 엔터티를 효율적으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-582">For example, using the table structure shown below, a client application can efficiently retrieve an individual employee entity by using the department name and the employee id (the **PartitionKey** and **RowKey**).</span></span>  

![][13]

<span data-ttu-id="f9ec4-583">이름과 같은 고유하지 않은 다른 속성 값을 기반으로 직원 엔터티 목록을 검색할 수 있도록 하려는 경우에는 인덱스를 사용하여 직접 조회하지 말고 비효율적인 파티션 검색을 사용하여 일치하는 항목을 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-583">If you also want to be able to retrieve a list of employee entities based on the value of another non-unique property, such as their last name, you must use a less efficient partition scan to find matches rather than using an index to look them up directly.</span></span> <span data-ttu-id="f9ec4-584">테이블 서비스에서는 보조 인덱스를 제공하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-584">This is because the table service does not provide secondary indexes.</span></span>  

#### <a name="solution"></a><span data-ttu-id="f9ec4-585">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f9ec4-585">Solution</span></span>
<span data-ttu-id="f9ec4-586">위에 표시된 엔터티 구조에서 성으로 조회할 수 있도록 하려면 직원 ID 목록을 유지 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-586">To enable lookup by last name with the entity structure shown above, you must maintain lists of employee ids.</span></span> <span data-ttu-id="f9ec4-587">특정 성(예: Jones)을 가진 직원 엔터티를 검색하려면 먼저 직원 ID 목록에서 성이 Jones인 직원을 찾은 다음 해당 직원 엔터티를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-587">If you want to retrieve the employee entities with a particular last name, such as Jones, you must first locate the list of employee ids for employees with Jones as their last name, and then retrieve those employee entities.</span></span> <span data-ttu-id="f9ec4-588">직원 ID 목록을 저장하는 기본 옵션에는 다음 세 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-588">There are three main options for storing the lists of employee ids:</span></span>  

* <span data-ttu-id="f9ec4-589">Blob 저장소 사용</span><span class="sxs-lookup"><span data-stu-id="f9ec4-589">Use blob storage.</span></span>  
* <span data-ttu-id="f9ec4-590">직원 엔터티와 동일한 파티션에 인덱스 엔터티 만들기</span><span class="sxs-lookup"><span data-stu-id="f9ec4-590">Create index entities in the same partition as the employee entities.</span></span>  
* <span data-ttu-id="f9ec4-591">별도의 파티션 또는 테이블에 인덱스 엔터티 만들기</span><span class="sxs-lookup"><span data-stu-id="f9ec4-591">Create index entities in a separate partition or table.</span></span>  

<span data-ttu-id="f9ec4-592"><u>옵션 #1: Blob 저장소 사용</u></span><span class="sxs-lookup"><span data-stu-id="f9ec4-592"><u>Option #1: Use blob storage</u></span></span>  

<span data-ttu-id="f9ec4-593">첫 번째 옵션의 경우 모든 고유한 성에 대한 Blob을 만들고, 각 Blob에 해당 성을 가진 직원의 **PartitionKey**(부서) 및 **RowKey**(직원 ID) 값 목록을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-593">For the first option, you create a blob for every unique last name, and in each blob store a list of the **PartitionKey** (department) and **RowKey** (employee id) values for employees that have that last name.</span></span> <span data-ttu-id="f9ec4-594">직원을 추가하거나 삭제할 때는 관련 Blob의 내용이 직원 엔터티와 결과적으로 일관성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-594">When you add or delete an employee you should ensure that the content of the relevant blob is eventually consistent with the employee entities.</span></span>  

<span data-ttu-id="f9ec4-595"><u>옵션 #2:</u> 동일한 파티션에 인덱스 엔터티 만들기</span><span class="sxs-lookup"><span data-stu-id="f9ec4-595"><u>Option #2:</u> Create index entities in the same partition</span></span>  

<span data-ttu-id="f9ec4-596">두 번째 옵션의 경우 다음 데이터를 저장하는 인덱스 엔터티를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-596">For the second option, use index entities that store the following data:</span></span>  

![][14]

<span data-ttu-id="f9ec4-597">**EmployeeIDs** 속성은 **RowKey**에 저장된 성을 가진 직원의 직원 ID 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-597">The **EmployeeIDs** property contains a list of employee ids for employees with the last name stored in the **RowKey**.</span></span>  

<span data-ttu-id="f9ec4-598">다음 단계에서는 두 번째 옵션을 사용하는 경우 새 직원을 추가할 때 따라야 하는 프로세스를 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-598">The following steps outline the process you should follow when you are adding a new employee if you are using the second option.</span></span> <span data-ttu-id="f9ec4-599">이 예제에서는 ID가 000152이고 성이 Jones인 직원을 Sales 부서에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-599">In this example, we are adding an employee with Id 000152 and a last name Jones in the Sales department:</span></span>  

1. <span data-ttu-id="f9ec4-600">**PartitionKey** 값 "Sales"와 **RowKey** 값 "Jones"를 사용하여 인덱스 엔터티를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-600">Retrieve the index entity with a **PartitionKey** value "Sales" and the **RowKey** value "Jones."</span></span> <span data-ttu-id="f9ec4-601">이 엔터티의 ETag를 2단계에서 사용하기 위해 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-601">Save the ETag of this entity to use in step 2.</span></span>  
2. <span data-ttu-id="f9ec4-602">새 직원 ID를 EmployeeIDs 필드의 목록에 추가하여 새 직원 엔터티(**PartitionKey** 값 "Sales" 및 **RowKey** 값 "000152")를 삽입하고 인덱스 엔터티(**PartitionKey** 값 "Sales" 및 **RowKey** 값 "Jones")를 업데이트하는 엔터티 그룹 트랜젝션(즉 배치 작업)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-602">Create an entity group transaction (that is, a batch operation) that inserts the new employee entity (**PartitionKey** value "Sales" and **RowKey** value "000152"), and updates the index entity (**PartitionKey** value "Sales" and **RowKey** value "Jones") by adding the new employee id to the list in the EmployeeIDs field.</span></span> <span data-ttu-id="f9ec4-603">엔터티 그룹 트랜잭션에 대한 자세한 내용은 [엔터티 그룹 트랜잭션](#entity-group-transactions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-603">For more information about entity group transactions, see [Entity Group Transactions](#entity-group-transactions).</span></span>  
3. <span data-ttu-id="f9ec4-604">낙관적 동시성 오류(다른 사람이 인덱스 엔터티를 방금 수정한 경우)로 인해 엔터티 그룹 트랜잭션에 실패한 경우 1단계부터 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-604">If the entity group transaction fails because of an optimistic concurrency error (someone else has just modified the index entity), then you need to start over at step 1 again.</span></span>  

<span data-ttu-id="f9ec4-605">두 번째 옵션을 사용하는 경우 이와 유사한 접근 방식을 사용하여 직원을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-605">You can use a similar approach to deleting an employee if you are using the second option.</span></span> <span data-ttu-id="f9ec4-606">직원의 성을 변경하는 것은 조금 더 복잡합니다. 세 엔터티, 즉 직원 엔터티, 이전 성의 인덱스 엔터티 및 새 성의 인덱스 엔터티를 업데이트하는 엔터티 그룹 트랜잭션를 실행해야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-606">Changing an employee's last name is slightly more complex because you will need to execute an entity group transaction that updates three entities: the employee entity, the index entity for the old last name, and the index entity for the new last name.</span></span> <span data-ttu-id="f9ec4-607">낙관적 동시성을 사용하여 업데이트를 수행하는 데 사용할 수 있는 ETag 값을 검색하려면 먼저 변경하기 전에 각 엔터티를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-607">You must retrieve each entity before making any changes in order to retrieve the ETag values that you can then use to perform the updates using optimistic concurrency.</span></span>  

<span data-ttu-id="f9ec4-608">다음 단계에서는 두 번째 옵션을 사용하는 경우 부서에서 지정된 성을 가진 모든 직원을 조회할 때 따라야 하는 프로세스를 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-608">The following steps outline the process you should follow when you need to look up all the employees with a given last name in a department if you are using the second option.</span></span> <span data-ttu-id="f9ec4-609">이 예제에서는 Sales 부서에서 성이 Jones인 모든 직원을 조회합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-609">In this example, we are looking up all the employees with last name Jones in the Sales department:</span></span>  

1. <span data-ttu-id="f9ec4-610">**PartitionKey** 값 "Sales"와 **RowKey** 값 "Jones"를 사용하여 인덱스 엔터티를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-610">Retrieve the index entity with a **PartitionKey** value "Sales" and the **RowKey** value "Jones."</span></span>  
2. <span data-ttu-id="f9ec4-611">EmployeeIDs 필드에서 직원 ID 목록을 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-611">Parse the list of employee Ids in the EmployeeIDs field.</span></span>  
3. <span data-ttu-id="f9ec4-612">이러한 각 직원에 대한 추가 정보(예: 전자 메일 주소)가 필요한 경우 2단계에서 가져온 직원 목록에서 **PartitionKey** 값 "Sales" 및 **RowKey** 값을 사용하여 각 직원 엔터티를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-612">If you need additional information about each of these employees (such as their email addresses), retrieve each of the employee entities using **PartitionKey** value "Sales" and **RowKey** values from the list of employees you obtained in step 2.</span></span>  

<span data-ttu-id="f9ec4-613"><u>옵션 3:</u> 별도의 파티션 또는 테이블에 인덱스 엔터티 만들기</span><span class="sxs-lookup"><span data-stu-id="f9ec4-613"><u>Option #3:</u> Create index entities in a separate partition or table</span></span>  

<span data-ttu-id="f9ec4-614">세 번째 옵션의 경우 다음 데이터를 저장하는 인덱스 엔터티를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-614">For the third option, use index entities that store the following data:</span></span>  

![][15]

<span data-ttu-id="f9ec4-615">**EmployeeIDs** 속성은 **RowKey**에 저장된 성을 가진 직원의 직원 ID 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-615">The **EmployeeIDs** property contains a list of employee ids for employees with the last name stored in the **RowKey**.</span></span>  

<span data-ttu-id="f9ec4-616">세 번째 옵션을 사용하는 경우에는 인덱스 엔터티가 직원 엔터티와 별도의 파티션에 있기 때문에 EGT를 사용하여 일관성을 유지할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-616">With the third option, you cannot use EGTs to maintain consistency because the index entities are in a separate partition from the employee entities.</span></span> <span data-ttu-id="f9ec4-617">인덱스 엔터티와 직원 엔터티가 결과적으로 일관성이 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-617">You should ensure that the index entities are eventually consistent with the employee entities.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="f9ec4-618">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f9ec4-618">Issues and considerations</span></span>
<span data-ttu-id="f9ec4-619">이 패턴을 구현할 방법을 결정할 때 다음 사항을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-619">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="f9ec4-620">이 솔루션에서는 쿼리를 두 번 이상 실행하여 일치하는 엔터티를 검색해야 합니다. 즉, 인덱스 엔터티를 쿼리하여 **RowKey** 값 목록을 가져온 다음, 목록의 각 엔터티를 검색하는 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-620">This solution requires at least two queries to retrieve matching entities: one to query the index entities to obtain the list of **RowKey** values, and then queries to retrieve each entity in the list.</span></span>  
* <span data-ttu-id="f9ec4-621">개별 엔터티의 최대 크기가 1MB인 경우 이 솔루션의 옵션 2와 옵션 3에서는 지정된 성에 대한 직원 ID 목록이 1MB를 초과하지 않는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-621">Given that an individual entity has a maximum size of 1 MB, option #2 and option #3 in the solution assume that the list of employee ids for any given last name is never greater than 1 MB.</span></span> <span data-ttu-id="f9ec4-622">직원 ID 목록이 1MB를 초과할 가능성이 있는 경우에는 옵션 1을 사용하여 인덱스 데이터를 Blob 저장소에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-622">If the list of employee ids is likely to be greater than 1 MB in size, use option #1 and store the index data in blob storage.</span></span>  
* <span data-ttu-id="f9ec4-623">옵션 2(EGT를 사용하여 직원 추가 및 삭제, 직원의 성 변경 처리)를 사용하는 경우 트랙잭션 볼륨이 지정된 파티션의 확장성 제한에 근접하는지 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-623">If you use option #2 (using EGTs to handle adding and deleting employees, and changing an employee's last name) you must evaluate if the volume of transactions will approach the scalability limits in a given partition.</span></span> <span data-ttu-id="f9ec4-624">이 경우 큐를 사용하여 업데이트 요청을 처리하고, 인덱스 엔터티를 직원 엔터티와 별도의 파티션에 저장할 수 있도록 해주는 결과적으로 일관성 있는 솔루션(옵션 1 또는 옵션 3)을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-624">If this is the case, you should consider an eventually consistent solution (option #1 or option #3) that uses queues to handle the update requests and enables you to store your index entities in a separate partition from the employee entities.</span></span>  
* <span data-ttu-id="f9ec4-625">이 솔루션의 옵션 2에서는 부서 내에서 성으로 조회할 것으로 가정합니다. 예를 들어 Sales 부서에서 성이 Jones인 직원 목록을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-625">Option #2 in this solution assumes that you want to look up by last name within a department: for example, you want to retrieve a list of employees with a last name Jones in the Sales department.</span></span> <span data-ttu-id="f9ec4-626">전체 조직에서 성이 Jones인 모든 직원을 조회할 수 있도록 하려면 옵션 1 또는 옵션 3을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-626">If you want to be able to look up all the employees with a last name Jones across the whole organization, use either option #1 or option #3.</span></span>
* <span data-ttu-id="f9ec4-627">결과적 일관성을 제공하는 큐 기반 솔루션을 구현할 수 있습니다. 자세한 내용은 [결과적으로 일관성 있는 트랜잭션 패턴](#eventually-consistent-transactions-pattern)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-627">You can implement a queue-based solution that delivers eventual consistency (see the [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) for more details).</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="f9ec4-628">이 패턴을 사용해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="f9ec4-628">When to use this pattern</span></span>
<span data-ttu-id="f9ec4-629">모두 공통된 속성 값(예: 성이 Jones인 모든 직원)을 공유하는 엔터티 집합을 조회하려는 경우에 이 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-629">Use this pattern when you want to lookup a set of entities that all share a common property value, such as all employees with the last name Jones.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="f9ec4-630">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="f9ec4-630">Related patterns and guidance</span></span>
<span data-ttu-id="f9ec4-631">이 패턴을 구현할 때 다음 패턴 및 지침도 관련이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-631">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="f9ec4-632">복합 키 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-632">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="f9ec4-633">결과적으로 일관성 있는 트랜잭션 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-633">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="f9ec4-634">엔터티 그룹 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="f9ec4-634">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="f9ec4-635">유형이 다른 엔터티 유형 작업</span><span class="sxs-lookup"><span data-stu-id="f9ec4-635">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="denormalization-pattern"></a><span data-ttu-id="f9ec4-636">비정규화 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-636">Denormalization pattern</span></span>
<span data-ttu-id="f9ec4-637">관련 데이터를 단일 엔터티에 함께 통합하여 단일 지점 쿼리로 필요한 모든 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-637">Combine related data together in a single entity to enable you to retrieve all the data you need with a single point query.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="f9ec4-638">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="f9ec4-638">Context and problem</span></span>
<span data-ttu-id="f9ec4-639">관계형 데이터베이스에서는 일반적으로 데이터를 정규화하여 중복을 제거함으로써 여러 테이블에서 데이터를 검색하는 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-639">In a relational database, you typically normalize data to remove duplication resulting in queries that retrieve data from multiple tables.</span></span> <span data-ttu-id="f9ec4-640">Azure 테이블의 데이터를 정규화한 경우 클라이언트와 버 간에 여러 번 왕복하여 관련 데이터를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-640">If you normalize your data in Azure tables, you must make multiple round trips from the client to the server to retrieve your related data.</span></span> <span data-ttu-id="f9ec4-641">예를 들어 아래 표시된 테이블 구조에서 부서에 대한 세부 정보를 검색하려면 두 번 왕복해야 합니다. 즉, 관리자 ID가 포함된 부서 엔터티를 가져온 다음 다른 요청을 통해 직원 엔터티에서 관리자의 세부 정보를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-641">For example, with the table structure shown below you need two round trips to retrieve the details for a department: one to fetch the department entity that includes the manager's id, and then another request to fetch the manager's details in an employee entity.</span></span>  

![][16]

#### <a name="solution"></a><span data-ttu-id="f9ec4-642">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f9ec4-642">Solution</span></span>
<span data-ttu-id="f9ec4-643">두 개의 별도 엔터티에 데이터를 저장하는 대신 데이터를 비정규화하여 부서 엔터티에 관리자 세부 정보의 복사본을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-643">Instead of storing the data in two separate entities, denormalize the data and keep a copy of the manager's details in the department entity.</span></span> <span data-ttu-id="f9ec4-644">예:</span><span class="sxs-lookup"><span data-stu-id="f9ec4-644">For example:</span></span>  

![][17]

<span data-ttu-id="f9ec4-645">이러한 속성이 저장된 부서 엔터티의 경우 이제 지점 쿼리를 사용하여 부서에 대한 모든 세부 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-645">With department entities stored with these properties, you can now retrieve all the details you need about a department using a point query.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="f9ec4-646">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f9ec4-646">Issues and considerations</span></span>
<span data-ttu-id="f9ec4-647">이 패턴을 구현할 방법을 결정할 때 다음 사항을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-647">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="f9ec4-648">일부 데이터를 두 번 저장하는 것과 관련된 약간의 비용 오버헤드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-648">There is some cost overhead associated with storing some data twice.</span></span> <span data-ttu-id="f9ec4-649">그러나 일반적으로 성능 이점(저장소 서비스에 대한 요청 수 감소로 인한 이점)이 저장소 비용(이 비용은 부서 세부 정보를 가져오는 데 필요한 트랜잭션 수의 감소로 인해 부분적으로 상쇄됨)을 훨씬 능가합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-649">The performance benefit (resulting from fewer requests to the storage service) typically outweighs the marginal increase in storage costs (and this cost is partially offset by a reduction in the number of transactions you require to fetch the details of a department).</span></span>  
* <span data-ttu-id="f9ec4-650">관리자에 대한 정보를 저장하는 두 엔터티의 일관성을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-650">You must maintain the consistency of the two entities that store information about managers.</span></span> <span data-ttu-id="f9ec4-651">EGT를 사용하여 여러 엔터티를 단일 원자성 트랜잭션에서 업데이트하는 방식으로 일관성 문제를 처리할 수 있습니다. 이 경우 부서 엔터티와 부서 관리자에 대한 직원 엔터티는 동일한 파티션에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-651">You can handle the consistency issue by using EGTs to update multiple entities in a single atomic transaction: in this case, the department entity, and the employee entity for the department manager are stored in the same partition.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="f9ec4-652">이 패턴을 사용해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="f9ec4-652">When to use this pattern</span></span>
<span data-ttu-id="f9ec4-653">관련 정보를 자주 조회해야 하는 경우에 이 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-653">Use this pattern when you frequently need to look up related information.</span></span> <span data-ttu-id="f9ec4-654">이 패턴은 클라이언트에서 필요한 데이터를 검색하기 위해 실행해야 하는 쿼리 수를 줄여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-654">This pattern reduces the number of queries your client must make to retrieve the data it requires.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="f9ec4-655">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="f9ec4-655">Related patterns and guidance</span></span>
<span data-ttu-id="f9ec4-656">이 패턴을 구현할 때 다음 패턴 및 지침도 관련이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-656">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="f9ec4-657">복합 키 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-657">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="f9ec4-658">엔터티 그룹 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="f9ec4-658">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="f9ec4-659">유형이 다른 엔터티 유형 작업</span><span class="sxs-lookup"><span data-stu-id="f9ec4-659">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)

### <a name="compound-key-pattern"></a><span data-ttu-id="f9ec4-660">복합 키 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-660">Compound key pattern</span></span>
<span data-ttu-id="f9ec4-661">복합 **RowKey** 값을 사용하여 클라이언트에서 단일 지점 쿼리로 관련 데이터를 조회하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-661">Use compound **RowKey** values to enable a client to lookup related data with a single point query.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="f9ec4-662">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="f9ec4-662">Context and problem</span></span>
<span data-ttu-id="f9ec4-663">관계형 데이터베이스에서는 쿼리에서 조인을 사용하여 관련 데이터 조각을 단일 쿼리의 클라이언트로 반환하는 것이 매우 자연스러운 일입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-663">In a relational database, it is quite natural to use joins in queries to return related pieces of data to the client in a single query.</span></span> <span data-ttu-id="f9ec4-664">예를 들어 직원 ID를 사용하여 해당 직원에 대한 성과 및 검토 데이터가 포함된 관련 엔터티 목록을 조회할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-664">For example, you might use the employee id to look up a list of related entities that contain performance and review data for that employee.</span></span>  

<span data-ttu-id="f9ec4-665">다음 구조를 사용하여 직원 엔터티를 테이블 서비스에 저장하는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-665">Assume you are storing employee entities in the Table service using the following structure:</span></span>  

![][18]

<span data-ttu-id="f9ec4-666">또한 매년 직원이 조직을 위해 일한 성과 및 검토와 관련된 기록 데이터를 저장하고 연도별로 이 정보에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-666">You also need to store historical data relating to reviews and performance for each year the employee has worked for your organization and you need to be able to access this information by year.</span></span> <span data-ttu-id="f9ec4-667">한 가지 옵션은 다음 구조로 엔터티를 저장하는 다른 테이블을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-667">One option is to create another table that stores entities with the following structure:</span></span>  

![][19]

<span data-ttu-id="f9ec4-668">이 접근 방식을 사용하면 일부 정보(예: 이름 및 성)를 새 엔터티에 복제하여 단일 요청으로 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-668">Notice that with this approach you may decide to duplicate some information (such as first name and last name) in the new entity to enable you to retrieve your data with a single request.</span></span> <span data-ttu-id="f9ec4-669">그러나 EGT를 사용하여 두 엔터티를 원자성으로 업데이트할 수 없기 때문에 강력한 일관성을 유지할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-669">However, you cannot maintain strong consistency because you cannot use an EGT to update the two entities atomically.</span></span>  

#### <a name="solution"></a><span data-ttu-id="f9ec4-670">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f9ec4-670">Solution</span></span>
<span data-ttu-id="f9ec4-671">다음 구조의 엔터티를 사용하여 새 엔터티 유형을 원래 테이블에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-671">Store a new entity type in your original table using entities with the following structure:</span></span>  

![][20]

<span data-ttu-id="f9ec4-672">이제 **RowKey** 는 직원 ID와 검토 데이터의 연도로 구성된 복합 키이며 이 키를 사용하여 단일 엔터티에 대한 단일 요청으로 직원의 성과 및 검토 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-672">Notice how the **RowKey** is now a compound key made up of the employee id and the year of the review data that enables you to retrieve the employee's performance and review data with a single request for a single entity.</span></span>  

<span data-ttu-id="f9ec4-673">다음 예제에서는 특정 직원(예: Sales 부서의 직원 000123)에 대한 모든 검토 데이터를 검색할 수 있는 방법을 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-673">The following example outlines how you can retrieve all the review data for a particular employee (such as employee 000123 in the Sales department):</span></span>  

<span data-ttu-id="f9ec4-674">$filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000123') and (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments</span><span class="sxs-lookup"><span data-stu-id="f9ec4-674">$filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000123') and (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="f9ec4-675">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f9ec4-675">Issues and considerations</span></span>
<span data-ttu-id="f9ec4-676">이 패턴을 구현할 방법을 결정할 때 다음 사항을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-676">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="f9ec4-677">**RowKey** 값을 쉽게 구문 분석할 수 있는 적절한 구분 기호 문자(예: **000123_2012**)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-677">You should use a suitable separator character that makes it easy to parse the **RowKey** value: for example, **000123_2012**.</span></span>  
* <span data-ttu-id="f9ec4-678">또한 이 엔터티를 동일한 직원에 대한 관련 데이터가 포함된 다른 엔터티와 동일한 파티션에 저장합니다. 이렇게 하면 EGT를 사용하여 강력한 일관성을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-678">You are also storing this entity in the same partition as other entities that contain related data for the same employee, which means you can use EGTs to maintain strong consistency.</span></span>
* <span data-ttu-id="f9ec4-679">이 패턴이 적절한지 확인하기 위해 데이터를 쿼리할 빈도를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-679">You should consider how frequently you will query the data to determine whether this pattern is appropriate.</span></span>  <span data-ttu-id="f9ec4-680">예를 들어 검토 데이터에는 자주 액세스하지 않고 기본 직원 데이터에는 자주 액세스하는 경우 이를 별도의 엔터티로 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-680">For example, if you will access the review data infrequently and the main employee data often you should keep them as separate entities.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="f9ec4-681">이 패턴을 사용해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="f9ec4-681">When to use this pattern</span></span>
<span data-ttu-id="f9ec4-682">자주 쿼리하는 하나 이상의 관련 엔터티를 저장해야 하는 경우에 이 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-682">Use this pattern when you need to store one or more related entities that you query frequently.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="f9ec4-683">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="f9ec4-683">Related patterns and guidance</span></span>
<span data-ttu-id="f9ec4-684">이 패턴을 구현할 때 다음 패턴 및 지침도 관련이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-684">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="f9ec4-685">엔터티 그룹 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="f9ec4-685">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="f9ec4-686">유형이 다른 엔터티 유형 작업</span><span class="sxs-lookup"><span data-stu-id="f9ec4-686">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  
* [<span data-ttu-id="f9ec4-687">결과적으로 일관성 있는 트랜잭션 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-687">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  

### <a name="log-tail-pattern"></a><span data-ttu-id="f9ec4-688">로그 테일 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-688">Log tail pattern</span></span>
<span data-ttu-id="f9ec4-689">날짜 및 시간 역순으로 정렬된 **RowKey** 값을 사용하여 가장 최근에 파티션에 추가된 *n*개의 엔터티를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-689">Retrieve the *n* entities most recently added to a partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="f9ec4-690">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="f9ec4-690">Context and problem</span></span>
<span data-ttu-id="f9ec4-691">일반적인 요구 사항은 가장 최근에 생성된 엔터티(예: 직원이 제출한 가장 최근 비용 청구 10개)를 검색할 수 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-691">A common requirement is be able to retrieve the most recently created entities, for example the ten most recent expense claims submitted by an employee.</span></span> <span data-ttu-id="f9ec4-692">테이블 쿼리는 집합에서 첫 번째 엔터티를 반환하는 **$top** 쿼리 작업을 지원합니다. 집합에 있는 마지막 *n*개의 엔터티를 반환하는 동등한 쿼리 작업은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-692">Table queries support a **$top** query operation to return the first *n* entities from a set: there is no equivalent query operation to return the last n entities in a set.</span></span>  

#### <a name="solution"></a><span data-ttu-id="f9ec4-693">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f9ec4-693">Solution</span></span>
<span data-ttu-id="f9ec4-694">가장 최근 항목이 항상 테이블의 첫 번째 항목이 되도록 날짜/시간 역순으로 자연스럽게 정렬하는 **RowKey** 를 사용하여 엔터티를 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-694">Store the entities using a **RowKey** that naturally sorts in reverse date/time order by using so the most recent entry is always the first one in the table.</span></span>  

<span data-ttu-id="f9ec4-695">예를 들어 직원이 제출한 가장 최근 비용 청구 10개를 검색하려면 현재 날짜/시간에서 파생된 역방향 틱 값을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-695">For example, to be able to retrieve the ten most recent expense claims submitted by an employee, you can use a reverse tick value derived from the current date/time.</span></span> <span data-ttu-id="f9ec4-696">다음 C# 코드 샘플은 가장 최근 항목부터 가장 오래된 항목까지 정렬하는 **RowKey** 에 대한 적절한 "반전된 틱" 값을 만드는 한 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-696">The following C# code sample shows one way to create a suitable "inverted ticks" value for a **RowKey** that sorts from the most recent to the oldest:</span></span>  

`string invertedTicks = string.Format("{0:D19}", DateTime.MaxValue.Ticks - DateTime.UtcNow.Ticks);`  

<span data-ttu-id="f9ec4-697">다음 코드를 사용하여 날짜/시간 값을 되돌릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-697">You can get back to the date time value using the following code:</span></span>  

`DateTime dt = new DateTime(DateTime.MaxValue.Ticks - Int64.Parse(invertedTicks));`  

<span data-ttu-id="f9ec4-698">테이블 쿼리는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-698">The table query looks like this:</span></span>  

`https://myaccount.table.core.windows.net/EmployeeExpense(PartitionKey='empid')?$top=10`  

#### <a name="issues-and-considerations"></a><span data-ttu-id="f9ec4-699">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f9ec4-699">Issues and considerations</span></span>
<span data-ttu-id="f9ec4-700">이 패턴을 구현할 방법을 결정할 때 다음 사항을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-700">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="f9ec4-701">문자열 값이 예상대로 정렬되도록 하려면 선행 0으로 역방향 틱 값을 채워야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-701">You must pad the reverse tick value with leading zeroes to ensure the string value sorts as expected.</span></span>  
* <span data-ttu-id="f9ec4-702">파티션 수준의 확장성 목표를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-702">You must be aware of the scalability targets at the level of a partition.</span></span> <span data-ttu-id="f9ec4-703">핫스폿 파티션을 만들지 않도록 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-703">Be careful not create hot spot partitions.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="f9ec4-704">이 패턴을 사용해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="f9ec4-704">When to use this pattern</span></span>
<span data-ttu-id="f9ec4-705">날짜/시간 역순으로 엔터티에 액세스해야 하는 경우 또는 가장 최근에 추가된 엔터티에 액세스해야 하는 경우에 이 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-705">Use this pattern when you need to access entities in reverse date/time order or when you need to access the most recently added entities.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="f9ec4-706">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="f9ec4-706">Related patterns and guidance</span></span>
<span data-ttu-id="f9ec4-707">이 패턴을 구현할 때 다음 패턴 및 지침도 관련이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-707">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="f9ec4-708">앞/뒤에 추가된 안티패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-708">Prepend / append anti-pattern</span></span>](#prepend-append-anti-pattern)  
* [<span data-ttu-id="f9ec4-709">엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="f9ec4-709">Retrieving entities</span></span>](#retrieving-entities)  

### <a name="high-volume-delete-pattern"></a><span data-ttu-id="f9ec4-710">대용량 삭제 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-710">High volume delete pattern</span></span>
<span data-ttu-id="f9ec4-711">동시 삭제할 모든 엔터티를 고유한 별도의 테이블에 저장하여 대용량 엔터티 삭제를 지원합니다. 테이블을 삭제하면 엔터티가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-711">Enable the deletion of a high volume of entities by storing all the entities for simultaneous deletion in their own separate table; you delete the entities by deleting the table.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="f9ec4-712">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="f9ec4-712">Context and problem</span></span>
<span data-ttu-id="f9ec4-713">대부분의 응용 프로그램은 클라이언트 응용 프로그램에서 더 이상 사용할 필요가 없거나 응용 프로그램이 다른 저장 매체에 보관한 경우 이전 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-713">Many applications delete old data which no longer needs to be available to a client application, or that the application has archived to another storage medium.</span></span> <span data-ttu-id="f9ec4-714">일반적으로 이러한 데이터는 날짜로 식별합니다. 예를 들어 60일이 지난 모든 로그인 요청에 대한 레코드를 삭제해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-714">You typically identify such data by a date: for example, you have a requirement to delete records of all login requests that are more than 60 days old.</span></span>  

<span data-ttu-id="f9ec4-715">한 가지 가능한 디자인은 **RowKey**에서 로그인 요청 날짜 및 시간을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-715">One possible design is to use the date and time of the login request in the **RowKey**:</span></span>  

![][21]

<span data-ttu-id="f9ec4-716">이 접근 방식을 사용하면 응용 프로그램이 각 사용자에 대한 로그인 엔터티를 별도의 파티션에 삽입하고 삭제할 수 있기 때문에 파티션 핫스폿이 방지됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-716">This approach avoids partition hotspots because the application can insert and delete login entities for each user in a separate partition.</span></span> <span data-ttu-id="f9ec4-717">그러나 이 접근 방식은 엔터티 수가 많은 경우 삭제할 모든 엔터티를 식별하기 위해 먼저 테이블 검색을 수행한 다음 각 이전 엔터티를 삭제해야 하기 때문에 시간과 비용이 많이 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-717">However, this approach may be costly and time consuming if you have a large number of entities because first you need to perform a table scan in order to identify all the entities to delete, and then you must delete each old entity.</span></span> <span data-ttu-id="f9ec4-718">여러 삭제 요청을 EGT로 일괄 처리하면 이전 엔터티를 삭제하는 데 필요한 서버 왕복 횟수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-718">Note that you can reduce the number of round trips to the server required to delete the old entities by batching multiple delete requests into EGTs.</span></span>  

#### <a name="solution"></a><span data-ttu-id="f9ec4-719">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f9ec4-719">Solution</span></span>
<span data-ttu-id="f9ec4-720">각 로그인 시도 날짜에 별도의 테이블을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-720">Use a separate table for each day of login attempts.</span></span> <span data-ttu-id="f9ec4-721">위의 엔터티 디자인을 사용하면 엔터티를 삽입할 때 핫스폿을 방지할 수 있으며, 매일 수십만 개의 개별 로그인 엔터티를 찾아서 삭제하는 대신 매일 하나의 테이블만 삭제하면 되므로(단일 저장소 작업) 이전 엔터티 삭제가 간편해집니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-721">You can use the entity design above to avoid hotspots when you are inserting entities, and deleting old entities is now simply a question of deleting one table every day (a single storage operation) instead of finding and deleting hundreds and thousands of individual login entities every day.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="f9ec4-722">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f9ec4-722">Issues and considerations</span></span>
<span data-ttu-id="f9ec4-723">이 패턴을 구현할 방법을 결정할 때 다음 사항을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-723">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="f9ec4-724">디자인이 응용 프로그램에서 데이터를 사용하는 다른 방식(예: 특정 엔터티 조회, 다른 데이터와 연결 또는 집계 정보 생성)을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="f9ec4-724">Does your design support other ways your application will use the data such as looking up specific entities, linking with other data, or generating aggregate information?</span></span>  
* <span data-ttu-id="f9ec4-725">디자인이 새 엔터티를 삽입할 때 핫스폿을 방지하나요?</span><span class="sxs-lookup"><span data-stu-id="f9ec4-725">Does your design avoid hot spots when you are inserting new entities?</span></span>  
* <span data-ttu-id="f9ec4-726">테이블을 삭제한 후 동일한 테이블 이름을 다시 사용하려는 경우 지연이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-726">Expect a delay if you want to reuse the same table name after deleting it.</span></span> <span data-ttu-id="f9ec4-727">항상 고유한 테이블 이름을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-727">It's better to always use unique table names.</span></span>  
* <span data-ttu-id="f9ec4-728">새 테이블을 처음 사용할 때 테이블 서비스에서 액세스 패턴을 학습하고 노드 간에 파티션을 분산하는 동안 일부 제한이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-728">Expect some throttling when you first use a new table while the Table service learns the access patterns and distributes the partitions across nodes.</span></span> <span data-ttu-id="f9ec4-729">새 테이블을 만들어야 하는 빈도를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-729">You should consider how frequently you need to create new tables.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="f9ec4-730">이 패턴을 사용해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="f9ec4-730">When to use this pattern</span></span>
<span data-ttu-id="f9ec4-731">동시에 삭제해야 하는 엔터티가 많은 경우에 이 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-731">Use this pattern when you have a high volume of entities that you must delete at the same time.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="f9ec4-732">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="f9ec4-732">Related patterns and guidance</span></span>
<span data-ttu-id="f9ec4-733">이 패턴을 구현할 때 다음 패턴 및 지침도 관련이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-733">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="f9ec4-734">엔터티 그룹 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="f9ec4-734">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="f9ec4-735">엔터티 수정</span><span class="sxs-lookup"><span data-stu-id="f9ec4-735">Modifying entities</span></span>](#modifying-entities)  

### <a name="data-series-pattern"></a><span data-ttu-id="f9ec4-736">데이터 계열 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-736">Data series pattern</span></span>
<span data-ttu-id="f9ec4-737">전체 데이터 계열을 단일 엔터티에 저장하여 요청 수를 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-737">Store complete data series in a single entity to minimize the number of requests you make.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="f9ec4-738">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="f9ec4-738">Context and problem</span></span>
<span data-ttu-id="f9ec4-739">일반적인 시나리오에서 응용 프로그램은 보통 모든 엔터티를 동시에 검색하는 데 필요한 데이터 계열을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-739">A common scenario is for an application to store a series of data that it typically needs to retrieve all at once.</span></span> <span data-ttu-id="f9ec4-740">예를 들어 응용 프로그램은 각 직원이 매시간 보내는 IM 메시지 수를 기록한 다음 이 정보를 사용하여 각 사용자가 이전 24시간 동안 보낸 메시지 수를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-740">For example, your application might record how many IM messages each employee sends every hour, and then use this information to plot how many messages each user sent over the preceding 24 hours.</span></span> <span data-ttu-id="f9ec4-741">한 가지 디자인은 각 직원에 대한 24개의 엔터티를 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-741">One design might be to store 24 entities for each employee:</span></span>  

![][22]

<span data-ttu-id="f9ec4-742">이 디자인을 사용하면 응용 프로그램이 메시지 수 값을 업데이트해야 할 때마다 각 직원에 대한 엔터티를 쉽게 찾아서 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-742">With this design, you can easily locate and update the entity to update for each employee whenever the application needs to update the message count value.</span></span> <span data-ttu-id="f9ec4-743">그러나 이전 24시간 동안의 활동에 대한 차트를 그리기 위해 정보를 검색하려면 24개의 엔터티를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-743">However, to retrieve the information to plot a chart of the activity for the preceding 24 hours, you must retrieve 24 entities.</span></span>  

#### <a name="solution"></a><span data-ttu-id="f9ec4-744">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f9ec4-744">Solution</span></span>
<span data-ttu-id="f9ec4-745">개별 속성과 함께 다음 디자인을 사용하여 각 시간에 대한 메시지 수를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-745">Use the following design with a separate property to store the message count for each hour:</span></span>  

![][23]

<span data-ttu-id="f9ec4-746">이 디자인을 사용하면 병합 작업을 통해 특정 시간 동안 각 직원의 메시지 수를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-746">With this design, you can use a merge operation to update the message count for an employee for a specific hour.</span></span> <span data-ttu-id="f9ec4-747">이제 단일 엔터티에 대한 요청을 사용하여 차트를 그리는 데 필요한 모든 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-747">Now, you can retrieve all the information you need to plot the chart using a request for a single entity.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="f9ec4-748">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f9ec4-748">Issues and considerations</span></span>
<span data-ttu-id="f9ec4-749">이 패턴을 구현할 방법을 결정할 때 다음 사항을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-749">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="f9ec4-750">전체 데이터 계열을 단일 엔터티에 포함할 수 없는 경우(하나의 엔터티가 최대 252개의 속성을 유지할 수 있음) Blob와 같은 다른 데이터 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-750">If your complete data series does not fit into a single entity (an entity can have up to 252 properties), use an alternative data store such as a blob.</span></span>  
* <span data-ttu-id="f9ec4-751">여러 클라이언트에서 동시에 엔터티를 업데이트하는 경우 **ETag** 를 사용하여 낙관적 동시성을 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-751">If you have multiple clients updating an entity simultaneously, you will need to use the **ETag** to implement optimistic concurrency.</span></span> <span data-ttu-id="f9ec4-752">여러 클라이언트가 있는 경우 높은 경합이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-752">If you have many clients, you may experience high contention.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="f9ec4-753">이 패턴을 사용해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="f9ec4-753">When to use this pattern</span></span>
<span data-ttu-id="f9ec4-754">개별 엔터티와 연관된 데이터 계열을 업데이트하고 검색해야 하는 경우에 이 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-754">Use this pattern when you need to update and retrieve a data series associated with an individual entity.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="f9ec4-755">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="f9ec4-755">Related patterns and guidance</span></span>
<span data-ttu-id="f9ec4-756">이 패턴을 구현할 때 다음 패턴 및 지침도 관련이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-756">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="f9ec4-757">큰 엔터티 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-757">Large entities pattern</span></span>](#large-entities-pattern)  
* [<span data-ttu-id="f9ec4-758">병합 또는 바꾸기</span><span class="sxs-lookup"><span data-stu-id="f9ec4-758">Merge or replace</span></span>](#merge-or-replace)  
* <span data-ttu-id="f9ec4-759">[결과적으로 일관성 있는 트랜잭션 패턴](#eventually-consistent-transactions-pattern) (데이터 계열을 Blob에 저장하는 경우)</span><span class="sxs-lookup"><span data-stu-id="f9ec4-759">[Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) (if you are storing the data series in a blob)</span></span>  

### <a name="wide-entities-pattern"></a><span data-ttu-id="f9ec4-760">넓은 엔터티 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-760">Wide entities pattern</span></span>
<span data-ttu-id="f9ec4-761">여러 실제 엔터티를 사용하여 속성이 252개가 넘는 논리적 엔터티를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-761">Use multiple physical entities to store logical entities with more than 252 properties.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="f9ec4-762">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="f9ec4-762">Context and problem</span></span>
<span data-ttu-id="f9ec4-763">개별 엔터티는 252개가 넘는 속성(필수 시스템 속성 제외)을 가질 수 없으며, 총 1MB가 넘는 데이터를 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-763">An individual entity can have no more than 252 properties (excluding the mandatory system properties) and cannot store more than 1 MB of data in total.</span></span> <span data-ttu-id="f9ec4-764">관계형 데이터베이스는 일반적으로 새 테이블을 추가하고 일대일 관계를 적용하여 행 크기에 대한 제한을 피합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-764">In a relational database, you would typically get round any limits on the size of a row by adding a new table and enforcing a 1-to-1 relationship between them.</span></span>  

#### <a name="solution"></a><span data-ttu-id="f9ec4-765">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f9ec4-765">Solution</span></span>
<span data-ttu-id="f9ec4-766">테이블 서비스를 사용하면 여러 엔터티를 저장하여 252개가 넘는 속성을 가진 대규모 단일 비즈니스 개체를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-766">Using the Table service, you can store multiple entities to represent a single large business object with more than 252 properties.</span></span> <span data-ttu-id="f9ec4-767">예를 들어 각 직원이 지난 365일 동안 보낸 IM 메시지 수를 저장하려는 경우 스키마가 서로 다른 두 개의 엔터티를 사용하는 다음 디자인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-767">For example, if you want to store a count of the number of IM messages sent by each employee for the last 365 days, you could use the following design that uses two entities with different schemas:</span></span>  

![][24]

<span data-ttu-id="f9ec4-768">서로 동기화된 상태로 유지하기 위해 두 엔터티를 모두 업데이트해야 하는 변경 사항을 적용하려는 경우 EGT를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-768">If you need to make a change that requires updating both entities to keep them synchronized with each other you can use an EGT.</span></span> <span data-ttu-id="f9ec4-769">그렇지 않으면 단일 병합 작업을 사용하여 특정 날짜의 메시지 수를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-769">Otherwise, you can use a single merge operation to update the message count for a specific day.</span></span> <span data-ttu-id="f9ec4-770">개별 직원에 대한 모든 데이터를 검색하려면 **PartitionKey** 및 **RowKey** 값을 둘 다 사용하는 두 가지 효율적인 요청으로 이 작업을 수행할 수 있는 엔터티를 모두 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-770">To retrieve all the data for an individual employee you must retrieve both entities, which you can do with two efficient requests that use both a **PartitionKey** and a **RowKey** value.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="f9ec4-771">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f9ec4-771">Issues and considerations</span></span>
<span data-ttu-id="f9ec4-772">이 패턴을 구현할 방법을 결정할 때 다음 사항을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-772">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="f9ec4-773">전체 논리적 엔터티를 검색하는 데에는 적어도 두 개의 저장소 트랜잭션이 필요합니다. 그 중 하나는 각 실제 엔터티를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-773">Retrieving a complete logical entity involves at least two storage transactions: one to retrieve each physical entity.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="f9ec4-774">이 패턴을 사용해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="f9ec4-774">When to use this pattern</span></span>
<span data-ttu-id="f9ec4-775">속성의 크기 또는 개수가 Table service의 개별 엔터티에 대한 한도를 초과하는 엔터티를 저장해야 하는 경우에 이 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-775">Use this pattern when  need to store entities whose size or number of properties exceeds the limits for an individual entity in the Table service.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="f9ec4-776">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="f9ec4-776">Related patterns and guidance</span></span>
<span data-ttu-id="f9ec4-777">이 패턴을 구현할 때 다음 패턴 및 지침도 관련이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-777">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="f9ec4-778">엔터티 그룹 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="f9ec4-778">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="f9ec4-779">병합 또는 바꾸기</span><span class="sxs-lookup"><span data-stu-id="f9ec4-779">Merge or replace</span></span>](#merge-or-replace)

### <a name="large-entities-pattern"></a><span data-ttu-id="f9ec4-780">큰 엔터티 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-780">Large entities pattern</span></span>
<span data-ttu-id="f9ec4-781">Blob 저장소를 사용하여 큰 속성 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-781">Use blob storage to store large property values.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="f9ec4-782">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="f9ec4-782">Context and problem</span></span>
<span data-ttu-id="f9ec4-783">개별 엔터티는 총 1MB가 넘는 데이터를 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-783">An individual entity cannot store more than 1 MB of data in total.</span></span> <span data-ttu-id="f9ec4-784">하나 이상의 속성에 엔터티의 총 크기가 이 값을 초과하게 만드는 값이 저장된 경우에는 테이블 서비스에 전체 엔터티를 저장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-784">If one or several of your properties store values that cause the total size of your entity to exceed this value, you cannot store the entire entity in the Table service.</span></span>  

#### <a name="solution"></a><span data-ttu-id="f9ec4-785">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f9ec4-785">Solution</span></span>
<span data-ttu-id="f9ec4-786">하나 이상의 속성에 많은 데이터가 포함되어 있어 엔터티의 크기가 1MB를 초과하는 경우 Blob 서비스에 데이터를 저장한 다음 엔터티의 속성에 해당 Blob의 주소를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-786">If your entity exceeds 1 MB in size because one or more properties contain a large amount of data, you can store data in the Blob service and then store the address of the blob in a property in the entity.</span></span> <span data-ttu-id="f9ec4-787">예를 들어 직원의 사진을 Blob 저장소에 저장하고 해당 사진의 링크를 직원 엔터티의 **사진** 속성에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-787">For example, you can store the photo of an employee in blob storage and store a link to the photo in the **Photo** property of your employee entity:</span></span>  

![][25]

#### <a name="issues-and-considerations"></a><span data-ttu-id="f9ec4-788">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f9ec4-788">Issues and considerations</span></span>
<span data-ttu-id="f9ec4-789">이 패턴을 구현할 방법을 결정할 때 다음 사항을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-789">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="f9ec4-790">테이블 서비스의 엔터티와 Blob 서비스의 데이터 간에 결과적 일관성을 유지하려면 [결과적으로 일관성 있는 트랜잭션 패턴](#eventually-consistent-transactions-pattern) 을 사용하여 엔터티를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-790">To maintain eventual consistency between the entity in the Table service and the data in the Blob service, use the [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) to maintain your entities.</span></span>
* <span data-ttu-id="f9ec4-791">전체 엔터티를 검색하는 데에는 적어도 두 개의 저장소 트랜잭션이 필요합니다. 그 중 하나는 엔터티를 검색하고, 또 하나는 Blob 데이터를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-791">Retrieving a complete entity involves at least two storage transactions: one to retrieve the entity and one to retrieve the blob data.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="f9ec4-792">이 패턴을 사용해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="f9ec4-792">When to use this pattern</span></span>
<span data-ttu-id="f9ec4-793">크기가 테이블 서비스의 개별 엔터티에 대한 제한을 초과하는 엔터티를 저장해야 하는 경우에 이 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-793">Use this pattern when you need to store entities whose size exceeds the limits for an individual entity in the Table service.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="f9ec4-794">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="f9ec4-794">Related patterns and guidance</span></span>
<span data-ttu-id="f9ec4-795">이 패턴을 구현할 때 다음 패턴 및 지침도 관련이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-795">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="f9ec4-796">결과적으로 일관성 있는 트랜잭션 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-796">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="f9ec4-797">넓은 엔터티 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-797">Wide entities pattern</span></span>](#wide-entities-pattern)

<a name="prepend-append-anti-pattern"></a>

### <a name="prependappend-anti-pattern"></a><span data-ttu-id="f9ec4-798">앞에 추가/뒤에 추가 안티패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-798">Prepend/append anti-pattern</span></span>
<span data-ttu-id="f9ec4-799">대용량 삽입이 있는 경우 여러 파티션 간에 삽입을 분산하여 확장성을 높입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-799">Increase scalability when you have a high volume of inserts by spreading the inserts across multiple partitions.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="f9ec4-800">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="f9ec4-800">Context and problem</span></span>
<span data-ttu-id="f9ec4-801">저장된 엔터티 앞 또는 뒤에 엔터티를 추가하면 일반적으로 응용 프로그램에서 파티션 시퀀스의 첫 번째 또는 마지막 파티션에 새 엔터티를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-801">Prepending or appending entities to your stored entities typically results in the application adding new entities to the first or last partition of a sequence of partitions.</span></span> <span data-ttu-id="f9ec4-802">이 경우 지정된 시간의 모든 삽입이 동일한 파티션에서 발생하므로 테이블 서비스에서 여러 노드 간에 삽입 부하를 분산할 수 없는 핫스폿이 생성되며, 응용 프로그램이 파티션의 확장성 목표에 도달하게 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-802">In this case, all of the inserts at any given time are taking place in the same partition, creating a hotspot that prevents the table service from load balancing inserts across multiple nodes, and possibly causing your application to hit the scalability targets for partition.</span></span> <span data-ttu-id="f9ec4-803">예를 들어 직원의 네트워크 및 리소스 액세스를 기록하는 응용 프로그램이 있는 경우 아래 표시된 엔터티 구조에서는 트랜잭션 볼륨이 개별 파티션의 확장성 목표에 도달하면 현재 시간의 파티션이 핫스폿이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-803">For example, if you have an application that logs network and resource access by employees, then an entity structure as shown below could result in the current hour's partition becoming a hotspot if the volume of transactions reaches the scalability target for an individual partition:</span></span>  

![][26]

#### <a name="solution"></a><span data-ttu-id="f9ec4-804">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f9ec4-804">Solution</span></span>
<span data-ttu-id="f9ec4-805">다음 대체 엔터티 구조는 응용 프로그램에서 이벤트를 기록할 때 특정 파티션의 핫스폿을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-805">The following alternative entity structure avoids a hotspot on any particular partition as the application logs events:</span></span>  

![][27]

<span data-ttu-id="f9ec4-806">이 예제에서는 **PartitionKey**와 **RowKey**가 복합 키입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-806">Notice with this example how both the **PartitionKey** and **RowKey** are compound keys.</span></span> <span data-ttu-id="f9ec4-807">**PartitionKey** 는 부서 및 직원 ID를 모두 사용하여 여러 파티션 간에 로깅을 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-807">The **PartitionKey** uses both the department and employee id to distribute the logging across multiple partitions.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="f9ec4-808">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f9ec4-808">Issues and considerations</span></span>
<span data-ttu-id="f9ec4-809">이 패턴을 구현할 방법을 결정할 때 다음 사항을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-809">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="f9ec4-810">삽입 시 핫 파티션 생성을 효율적으로 방지하는 대체 키 구조가 클라이언트 응용 프로그램의 쿼리를 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="f9ec4-810">Does the alternative key structure that avoids creating hot partitions on inserts efficiently support the queries your client application makes?</span></span>  
* <span data-ttu-id="f9ec4-811">예상한 트랜잭션 볼륨이 개별 파티션에 대한 확장성 목표에 도달하고 저장소 서비스에 의해 제한될 가능성이 있음을 의미하나요?</span><span class="sxs-lookup"><span data-stu-id="f9ec4-811">Does your anticipated volume of transactions mean that you are likely to reach the scalability targets for an individual partition and be throttled by the storage service?</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="f9ec4-812">이 패턴을 사용해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="f9ec4-812">When to use this pattern</span></span>
<span data-ttu-id="f9ec4-813">핫 파티션에 액세스할 때 트랜잭션 볼륨으로 인해 저장소 서비스에 의한 제한이 발생할 수 있을 때는 앞에 추가/뒤에 추가 안티패턴을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-813">Avoid the prepend/append anti-pattern when your volume of transactions is likely to result in throttling by the storage service when you access a hot partition.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="f9ec4-814">관련 패턴 및 지침</span><span class="sxs-lookup"><span data-stu-id="f9ec4-814">Related patterns and guidance</span></span>
<span data-ttu-id="f9ec4-815">이 패턴을 구현할 때 다음 패턴 및 지침도 관련이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-815">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="f9ec4-816">복합 키 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-816">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="f9ec4-817">로그 테일 패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-817">Log tail pattern</span></span>](#log-tail-pattern)  
* [<span data-ttu-id="f9ec4-818">엔터티 수정</span><span class="sxs-lookup"><span data-stu-id="f9ec4-818">Modifying entities</span></span>](#modifying-entities)  

### <a name="log-data-anti-pattern"></a><span data-ttu-id="f9ec4-819">로그 데이터 안티패턴</span><span class="sxs-lookup"><span data-stu-id="f9ec4-819">Log data anti-pattern</span></span>
<span data-ttu-id="f9ec4-820">일반적으로 테이블 서비스 대신 Blob 서비스를 사용하여 로그 데이터를 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-820">Typically, you should use the Blob service instead of the Table service to store log data.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="f9ec4-821">컨텍스트 및 문제점</span><span class="sxs-lookup"><span data-stu-id="f9ec4-821">Context and problem</span></span>
<span data-ttu-id="f9ec4-822">로그 데이터의 일반적인 사용 사례는 특정 날짜/시간 범위의 선택적 로그 항목을 검색하는 것입니다. 예를 들어 응용 프로그램이 특정 날짜의 15:04에서 15:06 사이에 기록한 모든 오류 및 중요 메시지를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-822">A common use case for log data is to retrieve a selection of log entries for a specific date/time range: for example, you want to find all the error and critical messages that your application logged between 15:04 and 15:06 on a specific date.</span></span> <span data-ttu-id="f9ec4-823">로그 엔터티를 저장한 파티션을 확인하는 데에는 로그 메시지의 날짜 및 시간을 사용하지 않습니다. 메시지의 날짜 및 시간을 사용하면 지정된 시간에 모든 로그 엔터티가 동일한 **PartitionKey** 값을 공유하기 때문에 핫 파티션이 발생합니다([앞에 추가/뒤에 추가 안티패턴](#prepend-append-anti-pattern) 섹션 참조).</span><span class="sxs-lookup"><span data-stu-id="f9ec4-823">You do not want to use the date and time of the log message to determine the partition you save log entities to: that results in a hot partition because at any given time, all the log entities will share the same **PartitionKey** value (see the section [Prepend/append anti-pattern](#prepend-append-anti-pattern)).</span></span> <span data-ttu-id="f9ec4-824">예를 들어 로그 메시지에 대한 다음 엔터티 스키마의 경우 응용 프로그램이 현재 날짜 및 시간에 대한 모든 로그 메시지를 파티션에 쓰기 때문에 핫 파티션이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-824">For example, the following entity schema for a log message results in a hot partition because the application writes all log messages to the partition for the current date and hour:</span></span>  

![][28]

<span data-ttu-id="f9ec4-825">이 예제에서 **RowKey** 는 로그 메시지가 날짜/시간 순으로 정렬되어 저장되도록 해당 로그 메시지의 날짜 및 시간을 포함하며, 여러 로그 메시지에서 동일한 날짜 및 시간을 공유하는 경우의 메시지 ID를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-825">In this example, the **RowKey** includes the date and time of the log message to ensure that log messages are stored sorted in date/time order, and includes a message id in case multiple log messages share the same date and time.</span></span>  

<span data-ttu-id="f9ec4-826">또 다른 접근 방식은 응용 프로그램이 파티션 범위에 메시지를 쓰도록 하는 **PartitionKey** 를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-826">Another approach is to use a **PartitionKey** that ensures that the application writes messages across a range of partitions.</span></span> <span data-ttu-id="f9ec4-827">예를 들어 로그 메시지의 원본이 여러 파티션 간에 메시지를 분산할 수 있는 방법을 제공하는 경우 다음 엔터티 스키마를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-827">For example, if the source of the log message provides a way to distribute messages across many partitions, you could use the following entity schema:</span></span>  

![][29]

<span data-ttu-id="f9ec4-828">그러나 이 스키마의 문제점은 특정 시간대의 모든 로그 메시지를 검색하려면 테이블의 모든 파티션을 검색해야 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-828">However, the problem with this schema is that to retrieve all the log messages for a specific time span you must search every partition in the table.</span></span>

#### <a name="solution"></a><span data-ttu-id="f9ec4-829">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f9ec4-829">Solution</span></span>
<span data-ttu-id="f9ec4-830">이전 섹션에서는 테이블 서비스를 사용하여 로그 항목을 저장하려는 경우의 문제점을 설명하고 불만족스러운 두 가지 디자인을 제시했습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-830">The previous section highlighted the problem of trying to use the Table service to store log entries and suggested two, unsatisfactory, designs.</span></span> <span data-ttu-id="f9ec4-831">한 가지 솔루션은 로그 메시지 작성 성능의 저하 위험으로 인해 핫 파티션이 발생했으며, 다른 솔루션은 특정 시간대의 로그 메시지를 검색하려면 테이블의 모든 파티션을 검색해야 하기 때문에 쿼리 성능이 저하되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-831">One solution led to a hot partition with the risk of poor performance writing log messages; the other solution resulted in poor query performance because of the requirement to scan every partition in the table to retrieve log messages for a specific time span.</span></span> <span data-ttu-id="f9ec4-832">Blob 저장소는 이 유형의 시나리오에 보다 효율적인 솔루션을 제공하며, Azure Storage Analytics에서는 수집한 로그 데이터를 이 방법으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-832">Blob storage offers a better solution for this type of scenario and this is how Azure Storage Analytics stores the log data it collects.</span></span>  

<span data-ttu-id="f9ec4-833">이 섹션에서는 일반적으로 범위로 쿼리한 데이터를 저장하는 접근 방식을 보여 주면서 Storage Analytics가 로그 데이터를 Blob 저장소에 저장하는 방법을 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-833">This section outlines how Storage Analytics stores log data in blob storage as an illustration of this approach to storing data that you typically query by range.</span></span>  

<span data-ttu-id="f9ec4-834">Storage Analytics는 로그 메시지를 구분 기호로 분리된 형식으로 여러 Blob에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-834">Storage Analytics stores log messages in a delimited format in multiple blobs.</span></span> <span data-ttu-id="f9ec4-835">구분 기호로 분리된 형식을 사용하면 클라이언트 응용 프로그램에서 로그 메시지의 데이터를 쉽게 구문 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-835">The delimited format makes it easy for a client application to parse the data in the log message.</span></span>  

<span data-ttu-id="f9ec4-836">Storage Analytics는 검색할 로그 메시지가 포함된 Blob를 찾을 수 있도록 Blob에 대한 명명 규칙을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-836">Storage Analytics uses a naming convention for blobs that enables you to locate the blob (or blobs) that contain the log messages for which you are searching.</span></span> <span data-ttu-id="f9ec4-837">예를 들어 "queue/2014/07/31/1800/000001.log"라는 Blob에는 2014년 7월 31일 오후 6시 이후의 큐 서비스와 관련된 로그 메시지가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-837">For example, a blob named "queue/2014/07/31/1800/000001.log" contains log messages that relate to the queue service for the hour starting at 18:00 on 31 July 2014.</span></span> <span data-ttu-id="f9ec4-838">"000001"은 이것이 이 기간 동안의 첫 번째 로그 파일임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-838">The "000001" indicates that this is the first log file for this period.</span></span> <span data-ttu-id="f9ec4-839">또한 Storage Analytics는 파일에 저장된 첫 번째 및 마지막 로그 메시지의 타임스탬프를 Blob 메타데이터의 일부로 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-839">Storage Analytics also records the timestamps of the first and last log messages stored in the file as part of the blob's metadata.</span></span> <span data-ttu-id="f9ec4-840">Blob 저장소용 API를 사용하면 이름 접두사를 기반으로 컨테이너에서 Blob를 찾을 수 있습니다. 오후 6시 이후의 큐 로그 데이터가 들어 있는 모든 Blob를 찾으려면 접두사 "queue/2014/07/31/1800"을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-840">The API for blob storage enables you locate blobs in a container based on a name prefix: to locate all the blobs that contain queue log data for the hour starting at 18:00, you can use the prefix "queue/2014/07/31/1800."</span></span>  

<span data-ttu-id="f9ec4-841">Storage Analytics는 로그 메시지를 내부적으로 버퍼한 다음 해당 Blob를 주기적으로 업데이트하거나 최신 로그 항목 집합으로 새 Blob를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-841">Storage Analytics buffers log messages internally and then periodically updates the appropriate blob or creates a new one with the latest batch of log entries.</span></span> <span data-ttu-id="f9ec4-842">이는 Blob 서비스에 수행해야 하는 쓰기 수를 줄여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-842">This reduces the number of writes it must perform to the blob service.</span></span>  

<span data-ttu-id="f9ec4-843">사용자 고유의 응용 프로그램에서 이와 유사한 솔루션을 구현하는 경우 안정성(모든 로그 항목을 Blob 저장소에 쓰기), 비용 및 확장성(응용 프로그램의 업데이트 버퍼링 및 Blob 저장소에 일괄 작업으로 쓰기) 간의 장단점을 관리할 방법을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-843">If you are implementing a similar solution in your own application, you must consider how to manage the trade-off between reliability (writing every log entry to blob storage as it happens) and cost and scalability (buffering updates in your application and writing them to blob storage in batches).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="f9ec4-844">문제 및 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f9ec4-844">Issues and considerations</span></span>
<span data-ttu-id="f9ec4-845">로그 데이터를 저장할 방법을 결정할 때 다음 사항을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-845">Consider the following points when deciding how to store log data:</span></span>  

* <span data-ttu-id="f9ec4-846">잠재적 핫 파티션을 방지하는 테이블 디자인을 만든 경우 로그 데이터에 효율적으로 액세스할 수 없는 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-846">If you create a table design that avoids potential hot partitions, you may find that you cannot access your log data efficiently.</span></span>  
* <span data-ttu-id="f9ec4-847">로그 데이터를 처리하기 위해 클라이언트에서 많은 레코드를 로드해야 하는 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-847">To process log data, a client often needs to load many records.</span></span>  
* <span data-ttu-id="f9ec4-848">로그 데이터는 구조화된 경우가 많지만 Blob 저장소가 더 나은 솔루션일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-848">Although log data is often structured, blob storage may be a better solution.</span></span>  

### <a name="implementation-considerations"></a><span data-ttu-id="f9ec4-849">구현 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f9ec4-849">Implementation considerations</span></span>
<span data-ttu-id="f9ec4-850">이 섹션에서는 이전 섹션에 설명된 패턴을 구현할 때 염두에 두어야 하는 몇 가지 고려 사항을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-850">This section discusses some of the considerations to bear in mind when you implement the patterns described in the previous sections.</span></span> <span data-ttu-id="f9ec4-851">이 섹션에서는 대부분 저장소 클라이언트 라이브러리(이 문서 작성 당시 버전 4.3.0)를 사용하는 C#으로 작성된 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-851">Most of this section uses examples written in C# that use the Storage Client Library (version 4.3.0 at the time of writing).</span></span>  

### <a name="retrieving-entities"></a><span data-ttu-id="f9ec4-852">엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="f9ec4-852">Retrieving entities</span></span>
<span data-ttu-id="f9ec4-853">[쿼리를 위한 디자인](#design-for-querying)섹션에 설명된 대로 가장 효율적인 쿼리는 지점 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-853">As discussed in the section [Design for querying](#design-for-querying), the most efficient query is a point query.</span></span> <span data-ttu-id="f9ec4-854">그러나 일부 시나리오에서는 여러 엔터티를 검색해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-854">However, in some scenarios you may need to retrieve multiple entities.</span></span> <span data-ttu-id="f9ec4-855">이 섹션에서는 저장소 클라이언트 라이브러리를 사용하여 엔터티를 검색하는 몇 가지 일반적인 접근 방식을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-855">This section describes some common approaches to retrieving entities using the Storage Client Library.</span></span>  

#### <a name="executing-a-point-query-using-the-storage-client-library"></a><span data-ttu-id="f9ec4-856">저장소 클라이언트 라이브러리를 사용하여 지점 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="f9ec4-856">Executing a point query using the Storage Client Library</span></span>
<span data-ttu-id="f9ec4-857">지점 쿼리를 실행하는 가장 간편한 방법은 **PartitionKey** 값이 "Sales"이고 **RowKey** 값이 "212"인 엔터티를 검색하는 **Retrieve** 테이블 작업을 다음 C# 코드 조각에 표시된 대로 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-857">The easiest way to execute a point query is to use the **Retrieve** table operation as shown in the following C# code snippet that retrieves an entity with a **PartitionKey** of value "Sales" and a **RowKey** of value "212":</span></span>  

```csharp
TableOperation retrieveOperation = TableOperation.Retrieve<EmployeeEntity>("Sales", "212");
var retrieveResult = employeeTable.Execute(retrieveOperation);
if (retrieveResult.Result != null)
{
    EmployeeEntity employee = (EmployeeEntity)retrieveResult.Result;
    ...
}  
```

<span data-ttu-id="f9ec4-858">이 예제에서는 검색할 엔터티의 형식이 **EmployeeEntity**인 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-858">Notice how this example expects the entity it retrieves to be of type **EmployeeEntity**.</span></span>  

#### <a name="retrieving-multiple-entities-using-linq"></a><span data-ttu-id="f9ec4-859">LINQ를 사용하여 여러 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="f9ec4-859">Retrieving multiple entities using LINQ</span></span>
<span data-ttu-id="f9ec4-860">저장소 클라이언트 라이브러리와 함께 LINQ를 사용하고 **where** 절이 있는 쿼리를 지정하여 여러 엔터티를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-860">You can retrieve multiple entities by using LINQ with Storage Client Library and specifying a query with a **where** clause.</span></span> <span data-ttu-id="f9ec4-861">테이블 스캔을 방지하려면 항상 where 절에 **PartitionKey** 값을 포함해야 하며, 가능한 경우 **RowKey** 값을 포함하여 테이블 및 파티션 스캔을 방지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-861">To avoid a table scan, you should always include the **PartitionKey** value in the where clause, and if possible the **RowKey** value to avoid table and partition scans.</span></span> <span data-ttu-id="f9ec4-862">테이블 서비스에서는 where 절에 사용할 수 있는 비교 연산자 집합(보다 큼, 보다 크거나 같음, 보다 작음, 보다 작거나 같음, 같음 및 같지 않음)이 제한되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-862">The table service supports a limited set of comparison operators (greater than, greater than or equal, less than, less than or equal, equal, and not equal) to use in the where clause.</span></span> <span data-ttu-id="f9ec4-863">다음 C# 코드 조각은 영업 부서(**PartitionKey**에 부서 이름이 저장되어 있는 것으로 가정)에서 성이 "B"(**RowKey**에 성이 저장되어 있는 것으로 가정)로 시작하는 모든 직원을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-863">The following C# code snippet finds all the employees whose last name starts with "B" (assuming that the **RowKey** stores the last name) in the sales department (assuming the **PartitionKey** stores the department name):</span></span>  

```csharp
TableQuery<EmployeeEntity> employeeQuery = employeeTable.CreateQuery<EmployeeEntity>();
var query = (from employee in employeeQuery
            where employee.PartitionKey == "Sales" &&
            employee.RowKey.CompareTo("B") >= 0 &&
            employee.RowKey.CompareTo("C") < 0
            select employee).AsTableQuery();
var employees = query.Execute();  
```

<span data-ttu-id="f9ec4-864">더 나은 성능을 위해 쿼리에서 **RowKey** 및 **PartitionKey**를 둘 다 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-864">Notice how the query specifies both a **RowKey** and a **PartitionKey** to ensure better performance.</span></span>  

<span data-ttu-id="f9ec4-865">다음 코드 예제에서는 흐름 API를 사용하여 동일한 기능을 보여 줍니다(일반적인 흐름 API에 대한 자세한 내용은 [흐름 API 디자인 모범 사례](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)참조).</span><span class="sxs-lookup"><span data-stu-id="f9ec4-865">The following code sample shows equivalent functionality using the fluent API (for more information about fluent APIs in general, see [Best Practices for Designing a Fluent API](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):</span></span>  

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
> <span data-ttu-id="f9ec4-866">이 샘플에서는 세 가지 필터 조건을 포함하기 위해 여러 **CombineFilters** 메서드를 중첩합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-866">The sample nests multiple **CombineFilters** methods to include the three filter conditions.</span></span>  
> 
> 

#### <a name="retrieving-large-numbers-of-entities-from-a-query"></a><span data-ttu-id="f9ec4-867">쿼리에서 여러 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="f9ec4-867">Retrieving large numbers of entities from a query</span></span>
<span data-ttu-id="f9ec4-868">최적의 쿼리는 **PartitionKey** 값과 **RowKey** 값을 기반으로 개별 엔터티를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-868">An optimal query returns an individual entity based on a **PartitionKey** value and a **RowKey** value.</span></span> <span data-ttu-id="f9ec4-869">그러나 일부 시나리오에서는 동일한 파티션 또는 여러 파티션에서 여러 엔터티를 반환해야 하는 요구 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-869">However, in some scenarios you may have a requirement to return many entities from the same partition or even from many partitions.</span></span>  

<span data-ttu-id="f9ec4-870">이러한 시나리오에서는 항상 응용 프로그램의 성능을 철저히 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-870">You should always fully test the performance of your application in such scenarios.</span></span>  

<span data-ttu-id="f9ec4-871">테이블 서비스에 대한 쿼리는 한 번에 최대 1,000개의 엔터티를 반환할 수 있으며, 최대 5초 동안 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-871">A query against the table service may return a maximum of 1,000 entities at one time and may execute for a maximum of five seconds.</span></span> <span data-ttu-id="f9ec4-872">결과 집합에 1,000개가 넘는 엔터티가 포함되거나, 쿼리가 5초 이내에 완료되지 않거나, 쿼리가 파티션 경계를 넘은 경우 테이블 서비스는 클라이언트 응용 프로그램이 다음 엔터티 집합을 요청할 수 있도록 연속 토큰을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-872">If the result set contains more than 1,000 entities, if the query did not complete within five seconds, or if the query crosses the partition boundary, the Table service returns a continuation token to enable the client application to request the next set of entities.</span></span> <span data-ttu-id="f9ec4-873">연속 토큰의 작동 방식에 대한 자세한 내용은 [쿼리 제한 시간 및 페이지 번호 매김](http://msdn.microsoft.com/library/azure/dd135718.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-873">For more information about how continuation tokens work, see [Query Timeout and Pagination](http://msdn.microsoft.com/library/azure/dd135718.aspx).</span></span>  

<span data-ttu-id="f9ec4-874">저장소 클라이언트 라이브러리를 사용하는 경우 테이블 서비스에서 엔터티를 반환할 때 연속 토큰을 자동으로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-874">If you are using the Storage Client Library, it can automatically handle continuation tokens for you as it returns entities from the Table service.</span></span> <span data-ttu-id="f9ec4-875">저장소 클라이언트 라이브러리를 사용하는 다음 C# 코드 예제는 테이블 서비스가 응답으로 반환하는 연속 토큰을 자동으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-875">The following C# code sample using the Storage Client Library automatically handles continuation tokens if the table service returns them in a response:</span></span>  

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

<span data-ttu-id="f9ec4-876">다음 C# 코드는 연속 토큰을 명시적으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-876">The following C# code handles continuation tokens explicitly:</span></span>  

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

<span data-ttu-id="f9ec4-877">연속 토큰을 명시적으로 사용하면 응용 프로그램이 데이터의 다음 세그먼트를 검색하는 시점을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-877">By using continuation tokens explicitly, you can control when your application retrieves the next segment of data.</span></span> <span data-ttu-id="f9ec4-878">예를 들어 클라이언트 응용 프로그램이 테이블에 저장된 엔터티의 페이징을 지원하는 경우, 사용자는 쿼리에서 검색된 일부 엔터티를 페이징하지 않도록 결정하여 현재 세그먼트의 모든 엔터티에 대한 페이징을 완료했을 때 응용 프로그램이 연속 토큰만을 사용하여 다음 세그먼트를 검색하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-878">For example, if your client application enables users to page through the entities stored in a table, a user may decide not to page through all the entities retrieved by the query so your application would only use a continuation token to retrieve the next segment when the user had finished paging through all the entities in the current segment.</span></span> <span data-ttu-id="f9ec4-879">이 접근 방식에는 몇 가지 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-879">This approach has several benefits:</span></span>  

* <span data-ttu-id="f9ec4-880">테이블 서비스에서 검색할 데이터의 양을 제한하고 네트워크를 통해 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-880">It enables you to limit the amount of data to retrieve from the Table service and that you move over the network.</span></span>  
* <span data-ttu-id="f9ec4-881">.NET에서 비동기 IO를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-881">It enables you to perform asynchronous IO in .NET.</span></span>  
* <span data-ttu-id="f9ec4-882">연속 토큰을 영구 저장소에 직렬화하여 응용 프로그램의 작동이 중단된 경우에도 작업을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-882">It enables you to serialize the continuation token to persistent storage so you can continue in the event of an application crash.</span></span>  

> [!NOTE]
> <span data-ttu-id="f9ec4-883">일반적으로 연속 토큰은 1,000개(이보다 적을 수도 있음)의 엔터티가 포함된 세그먼트를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-883">A continuation token typically returns a segment containing 1,000 entities, although it may be fewer.</span></span> <span data-ttu-id="f9ec4-884">이는 **수행**을 사용해 쿼리에서 반환되는 항목 수를 제한하여 조회 조건과 일치하는 첫 번째 n개의 엔터티를 반환하도록 한 경우에도 마찬가지입니다. Table service는 나머지 엔터티를 검색할 수 있도록 연속 토큰과 함께 n개 미만의 엔터티가 포함된 세그먼트를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-884">This is also the case if you limit the number of entries a query returns by using **Take** to return the first n entities that match your lookup criteria: the table service may return a segment containing fewer than n entities along with a continuation token to enable you to retrieve the remaining entities.</span></span>  
> 
> 

<span data-ttu-id="f9ec4-885">다음 C# 코드에서는 세그먼트 내에서 반환되는 엔터티 수를 수정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-885">The following C# code shows how to modify the number of entities returned inside a segment:</span></span>  

```csharp
employeeQuery.TakeCount = 50;  
```

#### <a name="server-side-projection"></a><span data-ttu-id="f9ec4-886">서버 쪽 프로젝션</span><span class="sxs-lookup"><span data-stu-id="f9ec4-886">Server-side projection</span></span>
<span data-ttu-id="f9ec4-887">단일 엔터티는 최대 255개의 속성을 가질 수 있으며, 크기가 최대 1MB일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-887">A single entity can have up to 255 properties and be up to 1 MB in size.</span></span> <span data-ttu-id="f9ec4-888">테이블을 쿼리하여 엔터티를 검색할 때 필요 없는 속성을 제외하여 데이터가 불필요하게 전송되는 것을 방지할 수 있습니다(이 경우 대기 시간이 단축되고 비용이 절감됨).</span><span class="sxs-lookup"><span data-stu-id="f9ec4-888">When you query the table and retrieve entities, you may not need all the properties and can avoid transferring data unnecessarily (to help reduce latency and cost).</span></span> <span data-ttu-id="f9ec4-889">서버 쪽 프로젝션을 사용하여 필요한 속성만 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-889">You can use server-side projection to transfer just the properties you need.</span></span> <span data-ttu-id="f9ec4-890">다음 예제에서는 쿼리에서 선택한 엔터티에서 **Email** 속성만(**PartitionKey**, **RowKey**, **Timestamp** 및 **ETag**와 함께) 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-890">The following example is retrieves just the **Email** property (along with **PartitionKey**, **RowKey**, **Timestamp**, and **ETag**) from the entities selected by the query.</span></span>  

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

<span data-ttu-id="f9ec4-891">**RowKey** 값은 검색할 속성 목록에 포함되지 않은 경우에도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-891">Notice how the **RowKey** value is available even though it was not included in the list of properties to retrieve.</span></span>  

### <a name="modifying-entities"></a><span data-ttu-id="f9ec4-892">엔터티 수정</span><span class="sxs-lookup"><span data-stu-id="f9ec4-892">Modifying entities</span></span>
<span data-ttu-id="f9ec4-893">저장소 클라이언트 라이브러리를 사용하면 엔터티를 삽입, 삭제 및 업데이트하여 테이블 서비스에 저장된 엔터티를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-893">The Storage Client Library enables you to modify your entities stored in the table service by inserting, deleting, and updating entities.</span></span> <span data-ttu-id="f9ec4-894">EGT를 사용하면 여러 삽입, 업데이트 및 삭제 작업을 일괄적으로 수행하여 필요한 왕복 횟수를 줄이고 솔루션의 성능을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-894">You can use EGTs to batch multiple insert, update, and delete operations together to reduce the number of round trips required and improve the performance of your solution.</span></span>  

<span data-ttu-id="f9ec4-895">저장소 클라이언트 라이브러리에서 EGT를 실행할 때 발생하는 예외에는 일반적으로 일괄 처리가 실패하도록 하는 엔터티의 인덱스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-895">Note that exceptions thrown when the Storage Client Library executes an EGT typically include the index of the entity that caused the batch to fail.</span></span> <span data-ttu-id="f9ec4-896">이는 EGT를 사용하는 코드를 디버그할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-896">This is helpful when you are debugging code that uses EGTs.</span></span>  

<span data-ttu-id="f9ec4-897">디자인이 클라이언트 응용 프로그램에서 동시성 및 업데이트 작업을 처리하는 방법에 어떤 영향을 미치는지도 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-897">You should also consider how your design affects how your client application handles concurrency and update operations.</span></span>  

#### <a name="managing-concurrency"></a><span data-ttu-id="f9ec4-898">동시성 관리</span><span class="sxs-lookup"><span data-stu-id="f9ec4-898">Managing concurrency</span></span>
<span data-ttu-id="f9ec4-899">기본적으로 클라이언트가 Table service에서 이러한 확인을 강제로 무시하도록 할 수도 있지만 Table service는 개별 엔터티 수준에서 **삽입**, **병합** 및 **삭제** 작업에 대한 낙관적 동시성 확인을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-899">By default, the table service implements optimistic concurrency checks at the level of individual entities for **Insert**, **Merge**, and **Delete** operations, although it is possible for a client to force the table service to bypass these checks.</span></span> <span data-ttu-id="f9ec4-900">Table service에서 동시성을 관리하는 방법에 대한 자세한 내용은 [Microsoft Azure Storage에서 동시성 관리](../storage/common/storage-concurrency.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-900">For more information about how the table service manages concurrency, see  [Managing Concurrency in Microsoft Azure Storage](../storage/common/storage-concurrency.md).</span></span>  

#### <a name="merge-or-replace"></a><span data-ttu-id="f9ec4-901">병합 또는 바꾸기</span><span class="sxs-lookup"><span data-stu-id="f9ec4-901">Merge or replace</span></span>
<span data-ttu-id="f9ec4-902">**TableOperation** 클래스의 **바꾸기** 메서드는 항상 Table service의 전체 엔터티를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-902">The **Replace** method of the **TableOperation** class always replaces the complete entity in the Table service.</span></span> <span data-ttu-id="f9ec4-903">저장된 엔터티에 존재하는 속성을 포함하지 않으면 요청 시 저장된 엔터티에서 해당 속성이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-903">If you do not include a property in the request when that property exists in the stored entity, the request removes that property from the stored entity.</span></span> <span data-ttu-id="f9ec4-904">저장된 엔터티에서 속성을 명시적으로 제거하지 않은 한 모든 속성을 요청에 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-904">Unless you want to remove a property explicitly from a stored entity, you must include every property in the request.</span></span>  

<span data-ttu-id="f9ec4-905">엔터티를 업데이트할 때 **TableOperation** 클래스의 **병합** 메서드를 사용하여 Table service로 보낼 데이터의 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-905">You can use the **Merge** method of the **TableOperation** class to reduce the amount of data that you send to the Table service when you want to update an entity.</span></span> <span data-ttu-id="f9ec4-906">**병합** 메서드는 저장된 엔터티의 모든 속성을 요청에 포함된 엔터티의 속성 값으로 바꾸지만 요청에 포함되지 않은 속성은 저장된 엔터티에 그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-906">The **Merge** method replaces any properties in the stored entity with property values from the entity included in the request, but leaves intact any properties in the stored entity that are not included in the request.</span></span> <span data-ttu-id="f9ec4-907">이는 엔터티가 많을 때 요청에서 소수의 속성만 업데이트해야 하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-907">This is useful if you have large entities and only need to update a small number of properties in a request.</span></span>  

> [!NOTE]
> <span data-ttu-id="f9ec4-908">엔터티가 존재하지 않으면 **바꾸기** 및 **병합** 메서드가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-908">The **Replace** and **Merge** methods fail if the entity does not exist.</span></span> <span data-ttu-id="f9ec4-909">또는 엔터티가 존재하지 않는 경우 새 엔터티를 만드는 **InsertOrReplace** 및 **InsertOrMerge** 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-909">As an alternative, you can use the **InsertOrReplace** and **InsertOrMerge** methods that create a new entity if it doesn't exist.</span></span>  
> 
> 

### <a name="working-with-heterogeneous-entity-types"></a><span data-ttu-id="f9ec4-910">유형이 다른 엔터티 유형 작업</span><span class="sxs-lookup"><span data-stu-id="f9ec4-910">Working with heterogeneous entity types</span></span>
<span data-ttu-id="f9ec4-911">테이블 서비스는 *스키마가 없는* 테이블 저장소이며 이는 단일 테이블이 뛰어난 디자인 유연성을 제공하는 여러 형식의 엔터티를 저장할 수 있다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-911">The Table service is a *schema-less* table store that means that a single table can store entities of multiple types providing great flexibility in your design.</span></span> <span data-ttu-id="f9ec4-912">다음 예제에서는 직원 및 부서 엔터티를 모두 저장하는 테이블을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-912">The following example illustrates a table storing both employee and department entities:</span></span>  

<table>
<tr>
<th><span data-ttu-id="f9ec4-913">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="f9ec4-913">PartitionKey</span></span></th>
<th><span data-ttu-id="f9ec4-914">RowKey</span><span class="sxs-lookup"><span data-stu-id="f9ec4-914">RowKey</span></span></th>
<th><span data-ttu-id="f9ec4-915">타임 스탬프</span><span class="sxs-lookup"><span data-stu-id="f9ec4-915">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="f9ec4-916">FirstName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-916">FirstName</span></span></th>
<th><span data-ttu-id="f9ec4-917">LastName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-917">LastName</span></span></th>
<th><span data-ttu-id="f9ec4-918">Age</span><span class="sxs-lookup"><span data-stu-id="f9ec4-918">Age</span></span></th>
<th><span data-ttu-id="f9ec4-919">Email</span><span class="sxs-lookup"><span data-stu-id="f9ec4-919">Email</span></span></th>
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
<th><span data-ttu-id="f9ec4-920">FirstName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-920">FirstName</span></span></th>
<th><span data-ttu-id="f9ec4-921">LastName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-921">LastName</span></span></th>
<th><span data-ttu-id="f9ec4-922">Age</span><span class="sxs-lookup"><span data-stu-id="f9ec4-922">Age</span></span></th>
<th><span data-ttu-id="f9ec4-923">Email</span><span class="sxs-lookup"><span data-stu-id="f9ec4-923">Email</span></span></th>
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
<th><span data-ttu-id="f9ec4-924">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-924">DepartmentName</span></span></th>
<th><span data-ttu-id="f9ec4-925">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="f9ec4-925">EmployeeCount</span></span></th>
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
<th><span data-ttu-id="f9ec4-926">FirstName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-926">FirstName</span></span></th>
<th><span data-ttu-id="f9ec4-927">LastName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-927">LastName</span></span></th>
<th><span data-ttu-id="f9ec4-928">Age</span><span class="sxs-lookup"><span data-stu-id="f9ec4-928">Age</span></span></th>
<th><span data-ttu-id="f9ec4-929">Email</span><span class="sxs-lookup"><span data-stu-id="f9ec4-929">Email</span></span></th>
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

<span data-ttu-id="f9ec4-930">각 엔터티에 여전히 **PartitionKey**, **RowKey** 및 **Timestamp** 값이 있어야 하지만 다른 속성 집합은 원하는 대로 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-930">Note that each entity must still have **PartitionKey**, **RowKey**, and **Timestamp** values, but may have any set of properties.</span></span> <span data-ttu-id="f9ec4-931">또한 해당 정보를 저장하도록 선택하지 않은 경우 엔터티 유형을 나타내는 항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-931">Furthermore, there is nothing to indicate the type of an entity unless you choose to store that information somewhere.</span></span> <span data-ttu-id="f9ec4-932">엔터티 유형을 식별하는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-932">There are two options for identifying the entity type:</span></span>  

* <span data-ttu-id="f9ec4-933">**RowKey**(또는 **PartitionKey**) 앞에 엔터티 형식을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-933">Prepend the entity type to the **RowKey** (or possibly the **PartitionKey**).</span></span> <span data-ttu-id="f9ec4-934">**RowKey** 값을 예로 들어 **EMPLOYEE_000123** 또는 **DEPARTMENT_SALES**하십시오.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-934">For example, **EMPLOYEE_000123** or **DEPARTMENT_SALES** as **RowKey** values.</span></span>  
* <span data-ttu-id="f9ec4-935">아래 표에 표시된 대로 별도의 속성을 사용하여 엔터티 유형을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-935">Use a separate property to record the entity type as shown in the table below.</span></span>  

<table>
<tr>
<th><span data-ttu-id="f9ec4-936">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="f9ec4-936">PartitionKey</span></span></th>
<th><span data-ttu-id="f9ec4-937">RowKey</span><span class="sxs-lookup"><span data-stu-id="f9ec4-937">RowKey</span></span></th>
<th><span data-ttu-id="f9ec4-938">타임 스탬프</span><span class="sxs-lookup"><span data-stu-id="f9ec4-938">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="f9ec4-939">EntityType</span><span class="sxs-lookup"><span data-stu-id="f9ec4-939">EntityType</span></span></th>
<th><span data-ttu-id="f9ec4-940">FirstName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-940">FirstName</span></span></th>
<th><span data-ttu-id="f9ec4-941">LastName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-941">LastName</span></span></th>
<th><span data-ttu-id="f9ec4-942">Age</span><span class="sxs-lookup"><span data-stu-id="f9ec4-942">Age</span></span></th>
<th><span data-ttu-id="f9ec4-943">Email</span><span class="sxs-lookup"><span data-stu-id="f9ec4-943">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="f9ec4-944">Employee</span><span class="sxs-lookup"><span data-stu-id="f9ec4-944">Employee</span></span></td>
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
<th><span data-ttu-id="f9ec4-945">EntityType</span><span class="sxs-lookup"><span data-stu-id="f9ec4-945">EntityType</span></span></th>
<th><span data-ttu-id="f9ec4-946">FirstName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-946">FirstName</span></span></th>
<th><span data-ttu-id="f9ec4-947">LastName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-947">LastName</span></span></th>
<th><span data-ttu-id="f9ec4-948">Age</span><span class="sxs-lookup"><span data-stu-id="f9ec4-948">Age</span></span></th>
<th><span data-ttu-id="f9ec4-949">Email</span><span class="sxs-lookup"><span data-stu-id="f9ec4-949">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="f9ec4-950">Employee</span><span class="sxs-lookup"><span data-stu-id="f9ec4-950">Employee</span></span></td>
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
<th><span data-ttu-id="f9ec4-951">EntityType</span><span class="sxs-lookup"><span data-stu-id="f9ec4-951">EntityType</span></span></th>
<th><span data-ttu-id="f9ec4-952">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-952">DepartmentName</span></span></th>
<th><span data-ttu-id="f9ec4-953">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="f9ec4-953">EmployeeCount</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="f9ec4-954">department</span><span class="sxs-lookup"><span data-stu-id="f9ec4-954">Department</span></span></td>
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
<th><span data-ttu-id="f9ec4-955">EntityType</span><span class="sxs-lookup"><span data-stu-id="f9ec4-955">EntityType</span></span></th>
<th><span data-ttu-id="f9ec4-956">FirstName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-956">FirstName</span></span></th>
<th><span data-ttu-id="f9ec4-957">LastName</span><span class="sxs-lookup"><span data-stu-id="f9ec4-957">LastName</span></span></th>
<th><span data-ttu-id="f9ec4-958">Age</span><span class="sxs-lookup"><span data-stu-id="f9ec4-958">Age</span></span></th>
<th><span data-ttu-id="f9ec4-959">Email</span><span class="sxs-lookup"><span data-stu-id="f9ec4-959">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="f9ec4-960">Employee</span><span class="sxs-lookup"><span data-stu-id="f9ec4-960">Employee</span></span></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

<span data-ttu-id="f9ec4-961">**RowKey**앞에 엔터티 유형을 추가하는 첫 번째 옵션은 유형이 서로 다른 두 엔터티의 키 값이 동일할 수 있는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-961">The first option, prepending the entity type to the **RowKey**, is useful if there is a possibility that two entities of different types might have the same key value.</span></span> <span data-ttu-id="f9ec4-962">또한 이 옵션은 동일한 유형의 엔터티를 파티션에서 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-962">It also groups entities of the same type together in the partition.</span></span>  

<span data-ttu-id="f9ec4-963">이 섹션에 설명된 기술은 특히 이 가이드 앞부분에 나오는 [관계 모델링](#modelling-relationships) 섹션의 [상속 관계](#inheritance-relationships)와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-963">The techniques discussed in this section are especially relevant to the discussion [Inheritance relationships](#inheritance-relationships) earlier in this guide in the section [Modelling relationships](#modelling-relationships).</span></span>  

> [!NOTE]
> <span data-ttu-id="f9ec4-964">클라이언트 응용 프로그램이 POCO 개체를 구체화하고 여러 버전에서 작동하도록 하려면 엔터티 유형 값에 버전 번호를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-964">You should consider including a version number in the entity type value to enable client applications to evolve POCO objects and work with different versions.</span></span>  
> 
> 

<span data-ttu-id="f9ec4-965">이 섹션의 나머지 부분에서는 동일한 테이블의 여러 엔터티 유형으로 작업하는 데 용이한 저장소 클라이언트 라이브러리의 몇 가지 기능에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-965">The remainder of this section describes some of the features in the Storage Client Library that facilitate working with multiple entity types in the same table.</span></span>  

#### <a name="retrieving-heterogeneous-entity-types"></a><span data-ttu-id="f9ec4-966">서로 다른 엔터티 유형 검색</span><span class="sxs-lookup"><span data-stu-id="f9ec4-966">Retrieving heterogeneous entity types</span></span>
<span data-ttu-id="f9ec4-967">저장소 클라이언트 라이브러리를 사용하는 경우 여러 엔터티 유형으로 작업하는 세 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-967">If you are using the Storage Client Library, you have three options for working with multiple entity types.</span></span>  

<span data-ttu-id="f9ec4-968">특정 **RowKey** 및 **PartitionKey** 값과 함께 저장된 엔터티의 유형을 알고 있는 경우에는 유형이 **EmployeeEntity**인 엔터티를 검색하는 이전 두 예제([Storage 클라이언트 라이브러리를 사용하여 지점 쿼리 실행](#executing-a-point-query-using-the-storage-client-library) 및 [LINQ를 사용하여 여러 엔터티 검색](#retrieving-multiple-entities-using-linq))와 같이 엔터티를 검색할 때 엔터티 유형을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-968">If you know the type of the entity stored with a specific **RowKey** and **PartitionKey** values, then you can specify the entity type when you retrieve the entity as shown in the previous two examples that retrieve entities of type **EmployeeEntity**: [Executing a point query using the Storage Client Library](#executing-a-point-query-using-the-storage-client-library) and [Retrieving multiple entities using LINQ](#retrieving-multiple-entities-using-linq).</span></span>  

<span data-ttu-id="f9ec4-969">두 번째 옵션은 구체적 POCO 엔터티 형식 대신 **DynamicTableEntity** 형식(속성 모음)을 사용하는 것입니다(이 옵션을 사용하면 엔터티를 .NET 형식으로 직렬화 및 역직렬화할 필요가 없으므로 성능이 향상될 수도 있습니다).</span><span class="sxs-lookup"><span data-stu-id="f9ec4-969">The second option is to use the **DynamicTableEntity** type (a property bag) instead of a concrete POCO entity type (this option may also improve performance because there is no need to serialize and deserialize the entity to .NET types).</span></span> <span data-ttu-id="f9ec4-970">다음 C# 코드는 잠재적으로 테이블에서 다양한 형식의 여러 엔터티를 검색하지만 모든 엔터티를 **DynamicTableEntity** 인스턴스로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-970">The following C# code potentially retrieves multiple entities of different types from the table, but returns all entities as **DynamicTableEntity** instances.</span></span> <span data-ttu-id="f9ec4-971">그런 다음 **EntityType** 속성을 사용하여 각 엔터티의 형식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-971">It then uses the **EntityType** property to determine the type of each entity:</span></span>  

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

<span data-ttu-id="f9ec4-972">다른 속성을 검색하려면 **DynamicTableEntity** 클래스의 **Properties** 속성에서 **TryGetValue** 메서드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-972">Note that to retrieve other properties you must use the **TryGetValue** method on the **Properties** property of the **DynamicTableEntity** class.</span></span>  

<span data-ttu-id="f9ec4-973">세 번째 옵션은 **DynamicTableEntity** 유형과 **EntityResolver** 인스턴스를 함께 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-973">A third option is to combine using the **DynamicTableEntity** type and an **EntityResolver** instance.</span></span> <span data-ttu-id="f9ec4-974">이 옵션을 사용하면 동일한 쿼리에서 여러 POCO 유형을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-974">This enables you to resolve to multiple POCO types in the same query.</span></span> <span data-ttu-id="f9ec4-975">이 예제에서 **EntityResolver** 대리자가 **EntityType** 속성을 사용하여 쿼리에서 반환된 엔터티의 두 가지 형식을 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-975">In this example, the **EntityResolver** delegate is using the **EntityType** property to distinguish between the two types of entity that the query returns.</span></span> <span data-ttu-id="f9ec4-976">**Resolve** 메서드는 **resolver** 대리자를 사용하여 **DynamicTableEntity** 인스턴스를 **TableEntity** 인스턴스에 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-976">The **Resolve** method uses the **resolver** delegate to resolve **DynamicTableEntity** instances to **TableEntity** instances.</span></span>  

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

#### <a name="modifying-heterogeneous-entity-types"></a><span data-ttu-id="f9ec4-977">서로 다른 엔터티 유형 수정</span><span class="sxs-lookup"><span data-stu-id="f9ec4-977">Modifying heterogeneous entity types</span></span>
<span data-ttu-id="f9ec4-978">엔터티를 삭제할 때는 엔터티 유형을 몰라도 되지만 엔터티를 삽입할 때는 항상 엔터티 유형을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-978">You do not need to know the type of an entity to delete it, and you always know the type of an entity when you insert it.</span></span> <span data-ttu-id="f9ec4-979">그러나 **DynamicTableEntity** 형식을 사용하면 형식을 모르는 경우에도 POCO 엔터티 클래스를 사용하지 않고 엔터티를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-979">However, you can use **DynamicTableEntity** type to update an entity without knowing its type and without using a POCO entity class.</span></span> <span data-ttu-id="f9ec4-980">다음 코드 샘플에서는 단일 엔터티를 검색하여 업데이트하기 전에 **EmployeeCount** 속성이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-980">The following code sample retrieves a single entity, and checks the **EmployeeCount** property exists before updating it.</span></span>  

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

### <a name="controlling-access-with-shared-access-signatures"></a><span data-ttu-id="f9ec4-981">공유 액세스 서명을 사용하여 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="f9ec4-981">Controlling access with Shared Access Signatures</span></span>
<span data-ttu-id="f9ec4-982">SAS(공유 액세스 서명) 토큰을 사용하여 클라이언트 응용 프로그램이 테이블 서비스에 직접 인증하지 않고도 테이블 엔터티를 직접 수정(및 쿼리)하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-982">You can use Shared Access Signature (SAS) tokens to enable client applications to modify (and query) table entities directly without the need to authenticate directly with the table service.</span></span> <span data-ttu-id="f9ec4-983">일반적으로 응용 프로그램에서 SAS를 사용할 경우 세 가지 주요 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-983">Typically, there are three main benefits to using SAS in your application:</span></span>  

* <span data-ttu-id="f9ec4-984">해당 장치가 테이블 서비스의 엔터티에 액세스하고 수정할 수 있도록 하기 위해 보안되지 않는 플랫폼(예: 모바일 장치)에 저장소 계정 키를 배포할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-984">You do not need to distribute your storage account key to an insecure platform (such as a mobile device) in order to allow that device to access and modify entities in the Table service.</span></span>  
* <span data-ttu-id="f9ec4-985">웹 및 작업자 역할이 엔터티를 관리하면서 수행하는 일부 작업을 최종 사용자 컴퓨터 및 모바일 장치와 같은 클라이언트 장치로 오프로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-985">You can offload some of the work that web and worker roles perform in managing your entities to client devices such as end-user computers and mobile devices.</span></span>  
* <span data-ttu-id="f9ec4-986">제약적이고 시간 제한된 권한 집합(예: 특정 리소스에 대한 읽기 전용 액세스 허용)을 클라이언트에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-986">You can assign a constrained and time limited set of permissions to a client (such as allowing read-only access to specific resources).</span></span>  

<span data-ttu-id="f9ec4-987">테이블 서비스에서 SAS 토큰 사용에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](../storage/common/storage-dotnet-shared-access-signature-part-1.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-987">For more information about using SAS tokens with the Table service, see [Using Shared Access Signatures (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>  

<span data-ttu-id="f9ec4-988">그러나 클라이언트 응용 프로그램에 테이블 서비스의 엔터티에 대한 권한을 부여하는 SAS 토큰을 여전히 생성해야 합니다. 저장소 계정 키에 대한 보안 액세스가 있는 환경에서 이렇게 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-988">However, you must still generate the SAS tokens that grant a client application to the entities in the table service: you should do this in an environment that has secure access to your storage account keys.</span></span> <span data-ttu-id="f9ec4-989">일반적으로 웹 또는 작업자 역할을 사용하여 SAS 토큰을 생성하고 엔터티에 액세스해야 하는 클라이언트 응용 프로그램에 이를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-989">Typically, you use a web or worker role to generate the SAS tokens and deliver them to the client applications that need access to your entities.</span></span> <span data-ttu-id="f9ec4-990">SAS 토큰을 생성하여 클라이언트에 제공하는 작업과 관련된 오버헤드가 여전히 있으므로 특히 대용량 시나리오에서 이 오버헤드를 줄일 수 있는 최상의 방법을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-990">Because there is still an overhead involved in generating and delivering SAS tokens to clients, you should consider how best to reduce this overhead, especially in high-volume scenarios.</span></span>  

<span data-ttu-id="f9ec4-991">테이블에 있는 엔터티의 하위 집합에 대한 액세스 권한을 부여하는 SAS 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-991">It is possible to generate a SAS token that grants access to a subset of the entities in a table.</span></span> <span data-ttu-id="f9ec4-992">기본적으로 전체 테이블에 대한 SAS 토큰을 만들지만 이 SAS 토큰이 **PartitionKey** 값 범위 또는 **PartitionKey** 및 **RowKey** 값 범위에 대한 액세스 권한을 부여하도록 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-992">By default, you create a SAS token for an entire table, but it is also possible to specify that the SAS token grant access to either a range of **PartitionKey** values, or a range of **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="f9ec4-993">각 사용자의 SAS 토큰이 Table service에 있는 해당 사용자의 고유 엔터티에 대한 액세스만 허용하도록 시스템의 개별 사용자에 대한 SAS 토큰을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-993">You might choose to generate SAS tokens for individual users of your system such that each user's SAS token only allows them access to their own entities in the table service.</span></span>  

### <a name="asynchronous-and-parallel-operations"></a><span data-ttu-id="f9ec4-994">비동기 및 병렬 작업</span><span class="sxs-lookup"><span data-stu-id="f9ec4-994">Asynchronous and parallel operations</span></span>
<span data-ttu-id="f9ec4-995">여러 파티션에 요청을 분산하는 경우 비동기 또는 병렬 쿼리를 사용하여 처리량 및 클라이언트 응답성을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-995">Provided you are spreading your requests across multiple partitions, you can improve throughput and client responsiveness by using asynchronous or parallel queries.</span></span>
<span data-ttu-id="f9ec4-996">예를 들어 둘 이상의 작업자 역할 인스턴스에서 테이블에 병렬로 액세스하는 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-996">For example, you might have two or more worker role instances accessing your tables in parallel.</span></span> <span data-ttu-id="f9ec4-997">특정 파티션 집합을 담당하는 개별 작업자 역할을 두거나, 여러 작업자 역할 인스턴스에서 각각 테이블의 모든 파티션에 액세스할 수 있도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-997">You could have individual worker roles responsible for particular sets of partitions, or simply have multiple worker role instances, each able to access all the partitions in a table.</span></span>  

<span data-ttu-id="f9ec4-998">클라이언트 인스턴스 내에서 저장소 작업을 비동기식으로 실행하여 처리량을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-998">Within a client instance, you can improve throughput by executing storage operations asynchronously.</span></span> <span data-ttu-id="f9ec4-999">저장소 클라이언트 라이브러리를 사용하면 비동기 쿼리 및 수정 사항을 쉽게 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-999">The Storage Client Library makes it easy to write asynchronous queries and modifications.</span></span> <span data-ttu-id="f9ec4-1000">예를 들어 다음 C# 코드와 같이 파티션의 모든 엔터티를 검색하는 동기 메서드로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1000">For example, you might start with the synchronous method that retrieves all the entities in a partition as shown in the following C# code:</span></span>  

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

<span data-ttu-id="f9ec4-1001">그런 다음 쿼리가 비동기식으로 실행되도록 아래와 같이 이 코드를 쉽게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1001">You can easily modify this code so that the query runs asynchronously as follows:</span></span>  

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

<span data-ttu-id="f9ec4-1002">이 비동기 예제에서는 동기 버전에서 다음 사항이 변경된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1002">In this asynchronous example, you can see the following changes from the synchronous version:</span></span>  

* <span data-ttu-id="f9ec4-1003">이제 메서드 서명은 **async** 수정자를 포함하고 **Task** 인스턴스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1003">The method signature now includes the **async** modifier and returns a **Task** instance.</span></span>  
* <span data-ttu-id="f9ec4-1004">**ExecuteSegmented** 메서드를 호출하여 결과를 검색하는 대신, 이제 메서드에서 **ExecuteSegmentedAsync** 메서드를 호출하고 **await** 한정자를 사용하여 결과를 비동기식으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1004">Instead of calling the **ExecuteSegmented** method to retrieve results, the method now calls the **ExecuteSegmentedAsync** method and uses the **await** modifier to retrieve results asynchronously.</span></span>  

<span data-ttu-id="f9ec4-1005">클라이언트 응용 프로그램은(서로 다른 **department** 매개 변수 값)이 메서드를 여러 번 호출할 수 있으며, 각 쿼리는 별도의 스레드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1005">The client application can call this method multiple times (with different values for the **department** parameter), and each query will run on a separate thread.</span></span>  

<span data-ttu-id="f9ec4-1006">**TableQuery** 클래스의 **Execute** 메서드는 비동기 버전이 없습니다. **IEnumerable** 인터페이스가 비동기 열거형을 지원하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1006">Note that there is no asynchronous version of the **Execute** method in the **TableQuery** class because the **IEnumerable** interface does not support asynchronous enumeration.</span></span>  

<span data-ttu-id="f9ec4-1007">엔터티를 비동기식으로 삽입, 업데이트 및 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1007">You can also insert, update, and delete entities asynchronously.</span></span> <span data-ttu-id="f9ec4-1008">다음 C# 예제에서는 직원 엔터티를 삽입하거나 바꾸는 간단한 동기 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1008">The following C# example shows a simple, synchronous method to insert or replace an employee entity:</span></span>  

```csharp
private static void SimpleEmployeeUpsert(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = employeeTable
        .Execute(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

<span data-ttu-id="f9ec4-1009">업데이트가 비동기식으로 실행되도록 아래와 같이 이 코드를 쉽게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1009">You can easily modify this code so that the update runs asynchronously as follows:</span></span>  

```csharp
private static async Task SimpleEmployeeUpsertAsync(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = await employeeTable
        .ExecuteAsync(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

<span data-ttu-id="f9ec4-1010">이 비동기 예제에서는 동기 버전에서 다음 사항이 변경된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1010">In this asynchronous example, you can see the following changes from the synchronous version:</span></span>  

* <span data-ttu-id="f9ec4-1011">이제 메서드 서명은 **async** 수정자를 포함하고 **Task** 인스턴스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1011">The method signature now includes the **async** modifier and returns a **Task** instance.</span></span>  
* <span data-ttu-id="f9ec4-1012">**Execute** 메서드를 호출하여 엔터티를 업데이트하는 대신, 이제 메서드에서 **ExecuteAsync** 메서드를 호출하고 **await** 한정자를 사용하여 결과를 비동기식으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1012">Instead of calling the **Execute** method to update the entity, the method now calls the **ExecuteAsync** method and uses the **await** modifier to retrieve results asynchronously.</span></span>  

<span data-ttu-id="f9ec4-1013">클라이언트 응용 프로그램은 이와 같은 여러 비동기 메서드를 호출할 수 있으며, 각 메서드 호출은 별도의 스레드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1013">The client application can call multiple asynchronous methods like this one, and each method invocation will run on a separate thread.</span></span>  

### <a name="credits"></a><span data-ttu-id="f9ec4-1014">크레딧</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1014">Credits</span></span>
<span data-ttu-id="f9ec4-1015">이 문서에 기여해 주신 Azure 팀원인 Dominic Betts, Jason Hogg, Jean Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Vinay Shah, Serdar Ozler과 Microsoft DX의 Tom Hollander에게 감사드립니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1015">We would like to thank the following members of the Azure team for their contributions: Dominic Betts, Jason Hogg, Jean Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Vinay Shah and Serdar Ozler as well as  Tom Hollander from Microsoft DX.</span></span> 

<span data-ttu-id="f9ec4-1016">또한 검토 과정에서 소중한 의견을 제공해 주신 Microsoft MVP인 Igor Papirov 및 Edward Bakker에게도 감사드립니다.</span><span class="sxs-lookup"><span data-stu-id="f9ec4-1016">We would also like to thank the following Microsoft MVP's for their valuable feedback during review cycles: Igor Papirov and Edward Bakker.</span></span>

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

