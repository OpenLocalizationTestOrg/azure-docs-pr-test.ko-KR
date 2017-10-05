---
title: "Azure Cosmos DB 리소스 모델 및 개념 | Microsoft Docs"
description: "데이터베이스, 컬렉션, UDF(사용자 정의 함수), 문서, 리소스 관리 권한 등으로 구성된 Azure Cosmos DB의 계층적 모델에 대해 알아봅니다."
keywords: "계층적 모델, cosmosdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: ef9d5c0c-0867-4317-bb1b-98e219799fd5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: anhoh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8051742c7c368d1ed84bcd90ab75b20f62105e2f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-hierarchical-resource-model-and-core-concepts"></a><span data-ttu-id="c6dde-104">Azure Cosmos DB 계층적 리소스 모델 및 핵심 개념</span><span class="sxs-lookup"><span data-stu-id="c6dde-104">Azure Cosmos DB hierarchical resource model and core concepts</span></span>
<span data-ttu-id="c6dde-105">Azure Cosmos DB에서 관리하는 데이터베이스 엔터티를 **리소스**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-105">The database entities that Azure Cosmos DB manages are referred to as **resources**.</span></span> <span data-ttu-id="c6dde-106">각 리소스는 논리적 URI를 통해 고유하게 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-106">Each resource is uniquely identified by a logical URI.</span></span> <span data-ttu-id="c6dde-107">표준 HTTP 동사, request/response 헤더 및 상태 코드를 사용해서 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-107">You can interact with the resources using standard HTTP verbs, request/response headers and status codes.</span></span> 

<span data-ttu-id="c6dde-108">이 문서를 읽어 보면 다음을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-108">By reading this article, you'll be able to answer the following questions:</span></span>

* <span data-ttu-id="c6dde-109">Cosmos DB의 리소스 모델이란?</span><span class="sxs-lookup"><span data-stu-id="c6dde-109">What is Cosmos DB's resource model?</span></span>
* <span data-ttu-id="c6dde-110">시스템 정의 리소스와 사용자 정의 리소스의 차이는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="c6dde-110">What are system defined resources as opposed to user defined resources?</span></span>
* <span data-ttu-id="c6dde-111">리소스를 어떻게 해결하나요?</span><span class="sxs-lookup"><span data-stu-id="c6dde-111">How do I address a resource?</span></span>
* <span data-ttu-id="c6dde-112">컬렉션을 어떻게 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="c6dde-112">How do I work with collections?</span></span>
* <span data-ttu-id="c6dde-113">저장된 프로시저, 트리거 및 UDF(사용자 정의 함수)를 사용하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="c6dde-113">How do I work with stored procedures, triggers and User Defined Functions (UDFs)?</span></span>

## <a name="hierarchical-resource-model"></a><span data-ttu-id="c6dde-114">계층적 리소스 모델</span><span class="sxs-lookup"><span data-stu-id="c6dde-114">Hierarchical resource model</span></span>
<span data-ttu-id="c6dde-115">다음 다이어그램에 표시된 대로, Cosmos DB의 계층적 **리소스 모델**은 단일 데이터베이스 계정 아래에 있고 각각 논리적이고 안정적인 URI를 통해 주소 지정이 가능한 리소스 집합으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-115">As the following diagram illustrates, the Cosmos DB hierarchical **resource model** consists of sets of resources under a database account, each addressable via a logical and stable URI.</span></span> <span data-ttu-id="c6dde-116">이 문서에서는 리소스 집합을 **피드** 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-116">A set of resources will be referred to as a **feed** in this article.</span></span> 

> [!NOTE]
> <span data-ttu-id="c6dde-117">Azure Cosmos DB는 통신 모델이 RESTful이며 [DocumentDB .NET 클라이언트 API](documentdb-sdk-dotnet.md)를 통해 사용할 수 있는 효율성 높은 TCP 프로토콜을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-117">Azure Cosmos DB offers a highly efficient TCP protocol which is also RESTful in its communication model, available through the [DocumentDB .NET client API](documentdb-sdk-dotnet.md).</span></span>
> 
> 

<span data-ttu-id="c6dde-118">![Azure Cosmos DB 계층적 리소스 모델][1]</span><span class="sxs-lookup"><span data-stu-id="c6dde-118">![Azure Cosmos DB hierarchical resource model][1]</span></span>  
<span data-ttu-id="c6dde-119">**계층적 리소스 모델**</span><span class="sxs-lookup"><span data-stu-id="c6dde-119">**Hierarchical resource model**</span></span>   

<span data-ttu-id="c6dde-120">리소스 작업을 시작하려면 Azure 구독을 사용해서 [데이터베이스 계정을 만들어야](create-documentdb-dotnet.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-120">To start working with resources, you must [create a database account](create-documentdb-dotnet.md) using your Azure subscription.</span></span> <span data-ttu-id="c6dde-121">데이터베이스 계정은 각각 여러 **컬렉션**을 포함하는 **데이터베이스** 집합으로 구성될 수 있고, 각 컬렉션에는 다시 **저장 프로시저, 트리거, UDF, 문서** 및 관련 **첨부 파일**이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-121">A database account can consist of a set of **databases**, each containing multiple **collections**, each of which in turn contain **stored procedures, triggers, UDFs, documents** and related **attachments**.</span></span> <span data-ttu-id="c6dde-122">또한 데이터베이스에는 **사용자**가 연관될 수 있으며, 이러한 각 사용자는 컬렉션, 저장 프로시저, 트리거, UDF, 문서 또는 첨부 파일에 액세스할 수 있는 **권한** 집합을 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-122">A database also has associated **users**, each with a set of **permissions** to access collections, stored procedures, triggers, UDFs, documents or attachments.</span></span> <span data-ttu-id="c6dde-123">데이터베이스, 사용자, 사용 권한 및 컬렉션은 잘 알려진 스키마가 있는 시스템 정의 리소스인 반면 문서 및 첨부 파일에는 임의의 사용자 정의 JSON 콘텐츠가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-123">While databases, users, permissions and collections are system-defined resources with well-known schemas, documents and attachments contain arbitrary, user defined JSON content.</span></span>  

| <span data-ttu-id="c6dde-124">리소스</span><span class="sxs-lookup"><span data-stu-id="c6dde-124">Resource</span></span> | <span data-ttu-id="c6dde-125">설명</span><span class="sxs-lookup"><span data-stu-id="c6dde-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c6dde-126">데이터베이스 계정</span><span class="sxs-lookup"><span data-stu-id="c6dde-126">Database account</span></span> |<span data-ttu-id="c6dde-127">데이터베이스 계정은 데이터베이스 집합 및 고정된 양의 첨부 파일용 Blob Storage에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-127">A database account is associated with a set of databases and a fixed amount of blob storage for attachments.</span></span> <span data-ttu-id="c6dde-128">Azure 구독을 사용하여 데이터베이스 계정을 하나 이상 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-128">You can create one or more database accounts using your Azure subscription.</span></span> <span data-ttu-id="c6dde-129">자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6dde-129">For more information, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span> |
| <span data-ttu-id="c6dde-130">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="c6dde-130">Database</span></span> |<span data-ttu-id="c6dde-131">데이터베이스는 여러 컬렉션으로 분할된 문서 저장소의 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-131">A database is a logical container of document storage partitioned across collections.</span></span> <span data-ttu-id="c6dde-132">또한 사용자 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-132">It is also a users container.</span></span> |
| <span data-ttu-id="c6dde-133">사용자</span><span class="sxs-lookup"><span data-stu-id="c6dde-133">User</span></span> |<span data-ttu-id="c6dde-134">사용 권한 범위 지정을 위한 논리적 네임스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-134">The logical namespace for scoping permissions.</span></span> |
| <span data-ttu-id="c6dde-135">사용 권한</span><span class="sxs-lookup"><span data-stu-id="c6dde-135">Permission</span></span> |<span data-ttu-id="c6dde-136">특정 리소스에 대한 액세스를 위해 사용자와 연결된 권한 부여 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-136">An authorization token associated with a user for access to a specific resource.</span></span> |
| <span data-ttu-id="c6dde-137">컬렉션</span><span class="sxs-lookup"><span data-stu-id="c6dde-137">Collection</span></span> |<span data-ttu-id="c6dde-138">컬렉션은 JSON 문서 및 관련 JavaScript 응용 프로그램 논리의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-138">A collection is a container of JSON documents and the associated JavaScript application logic.</span></span> <span data-ttu-id="c6dde-139">컬렉션은 해당 컬렉션과 연관된 성능 수준에 따라 [비용](performance-levels.md) 이 결정되는 청구 가능 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-139">A collection is a billable entity, where the [cost](performance-levels.md) is determined by the performance level associated with the collection.</span></span> <span data-ttu-id="c6dde-140">컬렉션은 하나 이상의 파티션/서버에 걸쳐 있을 수 있으며 크기가 거의 무제한인 저장소 또는 처리량을 처리하도록 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-140">Collections can span one or more partitions/servers and can scale to handle practically unlimited volumes of storage or throughput.</span></span> |
| <span data-ttu-id="c6dde-141">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="c6dde-141">Stored Procedure</span></span> |<span data-ttu-id="c6dde-142">JavaScript로 작성된 응용 프로그램 논리로, 컬렉션에 등록되고 데이터베이스 엔진 내에서 트랜잭션으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-142">Application logic written in JavaScript which is registered with a collection and transactionally executed within the database engine.</span></span> |
| <span data-ttu-id="c6dde-143">트리거</span><span class="sxs-lookup"><span data-stu-id="c6dde-143">Trigger</span></span> |<span data-ttu-id="c6dde-144">삽입, 바꾸기 또는 삭제 작업 전 후에 실행된 JavaScript로 작성된 응용 프로그램 논리입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-144">Application logic written in JavaScript executed before or after either an insert, replace or delete operation.</span></span> |
| <span data-ttu-id="c6dde-145">UDF</span><span class="sxs-lookup"><span data-stu-id="c6dde-145">UDF</span></span> |<span data-ttu-id="c6dde-146">JavaScript로 작성된 응용 프로그램 논리입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-146">Application logic written in JavaScript.</span></span> <span data-ttu-id="c6dde-147">UDF를 사용하면 사용자 지정 쿼리 연산자를 모델링하여 핵심 DocumentDB API 쿼리 언어를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-147">UDFs enable you to model a custom query operator and thereby extend the core DocumentDB API query language.</span></span> |
| <span data-ttu-id="c6dde-148">문서</span><span class="sxs-lookup"><span data-stu-id="c6dde-148">Document</span></span> |<span data-ttu-id="c6dde-149">사용자 정의(임의) JSON 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-149">User defined (arbitrary) JSON content.</span></span> <span data-ttu-id="c6dde-150">기본적으로 스키마를 정의할 필요가 없거나 컬렉션에 추가된 모든 문서에 대해 보조 인덱스를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-150">By default, no schema needs to be defined nor do secondary indices need to be provided for all the documents added to a collection.</span></span> |
| <span data-ttu-id="c6dde-151">첨부 파일</span><span class="sxs-lookup"><span data-stu-id="c6dde-151">Attachment</span></span> |<span data-ttu-id="c6dde-152">첨부 파일은 외부 blob/미디어에 대한 참조 및 관련 메타데이터가 포함된 특수 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-152">An attachment is a special document containing references and associated metadata for external blob/media.</span></span> <span data-ttu-id="c6dde-153">개발자는 Cosmos DB에서 blob을 관리하도록 선택하거나 OneDrive, Dropbox 등의 외부 Blob service 공급자를 사용하여 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-153">The developer can choose to have the blob managed by Cosmos DB or store it with an external blob service provider such as OneDrive, Dropbox, etc.</span></span> |

## <a name="system-vs-user-defined-resources"></a><span data-ttu-id="c6dde-154">시스템 정의 리소스와 사용자 정의 리소스 비교</span><span class="sxs-lookup"><span data-stu-id="c6dde-154">System vs. user defined resources</span></span>
<span data-ttu-id="c6dde-155">데이터베이스 계정, 데이터베이스, 컬렉션, 사용자, 사용 권한, 저장 프로시저, 트리거 및 UDF와 같은 리소스에는 모두 고정 스키마가 있으며 시스템 리소스라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-155">Resources such as database accounts, databases, collections, users, permissions, stored procedures, triggers, and UDFs - all have a fixed schema and are called system resources.</span></span> <span data-ttu-id="c6dde-156">반면, 문서 및 첨부 파일과 같은 리소스는 스키마에 제한이 없으며 사용자 정의 리소스의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-156">In contrast, resources such as documents and attachments have no restrictions on the schema and are examples of user defined resources.</span></span> <span data-ttu-id="c6dde-157">Cosmos DB에서는 시스템 및 사용자 정의 리소스 둘 다 표준 규격 JSON으로 표시되고 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-157">In Cosmos DB, both system and user defined resources are represented and managed as standard-compliant JSON.</span></span> <span data-ttu-id="c6dde-158">모든 리소스(시스템 또는 사용자 정의)에는 다음과 같은 공통 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-158">All resources, system or user defined, have the following common properties.</span></span>

> [!NOTE]
> <span data-ttu-id="c6dde-159">JSON 표현에서는 리소스의 모든 시스템 생성 속성 앞에 밑줄(_)이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-159">Note that all system generated properties in a resource are prefixed with an underscore (_) in their JSON representation.</span></span>
> 
> 

<table>
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="c6dde-160"><strong>속성</strong></span><span class="sxs-lookup"><span data-stu-id="c6dde-160"><strong>Property</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c6dde-161"><strong>사용자 설정 가능 또는 시스템 생성?</strong></span><span class="sxs-lookup"><span data-stu-id="c6dde-161"><strong>User settable or system generated?</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c6dde-162"><strong>목적</strong></span><span class="sxs-lookup"><span data-stu-id="c6dde-162"><strong>Purpose</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="c6dde-163">_rid</span><span class="sxs-lookup"><span data-stu-id="c6dde-163">_rid</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c6dde-164">시스템 생성</span><span class="sxs-lookup"><span data-stu-id="c6dde-164">System generated</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c6dde-165">리소스의 고유한 시스템 생성 계층적 식별자</span><span class="sxs-lookup"><span data-stu-id="c6dde-165">System generated, unique and hierarchical identifier of the resource</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="c6dde-166">_etag</span><span class="sxs-lookup"><span data-stu-id="c6dde-166">_etag</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c6dde-167">시스템 생성</span><span class="sxs-lookup"><span data-stu-id="c6dde-167">System generated</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c6dde-168">낙관적 동시성 제어에 필요한 리소스의 etag</span><span class="sxs-lookup"><span data-stu-id="c6dde-168">etag of the resource required for optimistic concurrency control</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="c6dde-169">_ts</span><span class="sxs-lookup"><span data-stu-id="c6dde-169">_ts</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c6dde-170">시스템 생성</span><span class="sxs-lookup"><span data-stu-id="c6dde-170">System generated</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c6dde-171">리소스의 마지막 업데이트 타임스탬프</span><span class="sxs-lookup"><span data-stu-id="c6dde-171">Last updated timestamp of the resource</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="c6dde-172">_self</span><span class="sxs-lookup"><span data-stu-id="c6dde-172">_self</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c6dde-173">시스템 생성</span><span class="sxs-lookup"><span data-stu-id="c6dde-173">System generated</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c6dde-174">리소스의 고유한 주소 지정 가능 URI</span><span class="sxs-lookup"><span data-stu-id="c6dde-174">Unique addressable URI of the resource</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="c6dde-175">id</span><span class="sxs-lookup"><span data-stu-id="c6dde-175">id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c6dde-176">시스템 생성</span><span class="sxs-lookup"><span data-stu-id="c6dde-176">System generated</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c6dde-177">리소스의 고유한 사용자 정의 이름(동일한 파티션 키 값 포함)</span><span class="sxs-lookup"><span data-stu-id="c6dde-177">User defined unique name of the resource (with the same partition key value).</span></span> <span data-ttu-id="c6dde-178">사용자가 ID를 지정하지 않는 경우 시스템에서 ID가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-178">If the user does not specify an id, an id will be system generated</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="wire-representation-of-resources"></a><span data-ttu-id="c6dde-179">리소스의 네트워크 표현</span><span class="sxs-lookup"><span data-stu-id="c6dde-179">Wire representation of resources</span></span>
<span data-ttu-id="c6dde-180">Cosmos DB는 JSON 표준 또는 특수 인코딩에 대한 소유 확장을 위임하지 않습니다. 표준 규격 JSON 문서로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-180">Cosmos DB does not mandate any proprietary extensions to the JSON standard or special encodings; it works with standard compliant JSON documents.</span></span>  

### <a name="addressing-a-resource"></a><span data-ttu-id="c6dde-181">리소스 주소 지정</span><span class="sxs-lookup"><span data-stu-id="c6dde-181">Addressing a resource</span></span>
<span data-ttu-id="c6dde-182">모든 리소스는 URI로 주소 지정이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-182">All resources are URI addressable.</span></span> <span data-ttu-id="c6dde-183">리소스의 **_self** 속성 값은 리소스의 상대 URI를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-183">The value of the **_self** property of a resource represents the relative URI of the resource.</span></span> <span data-ttu-id="c6dde-184">URI의 형식은 /\<feed\>/{_rid} 경로 세그먼트로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-184">The format of the URI consists of the /\<feed\>/{_rid} path segments:</span></span>  

| <span data-ttu-id="c6dde-185">_self 값</span><span class="sxs-lookup"><span data-stu-id="c6dde-185">Value of the _self</span></span> | <span data-ttu-id="c6dde-186">설명</span><span class="sxs-lookup"><span data-stu-id="c6dde-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c6dde-187">/dbs</span><span class="sxs-lookup"><span data-stu-id="c6dde-187">/dbs</span></span> |<span data-ttu-id="c6dde-188">데이터베이스 계정의 데이터베이스 피드</span><span class="sxs-lookup"><span data-stu-id="c6dde-188">Feed of databases under a database account</span></span> |
| <span data-ttu-id="c6dde-189">/dbs/{dbName}</span><span class="sxs-lookup"><span data-stu-id="c6dde-189">/dbs/{dbName}</span></span> |<span data-ttu-id="c6dde-190">{dbName} 값과 ID가 일치하는 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="c6dde-190">Database with an id matching the value {dbName}</span></span> |
| <span data-ttu-id="c6dde-191">/dbs/{dbName}/colls/</span><span class="sxs-lookup"><span data-stu-id="c6dde-191">/dbs/{dbName}/colls/</span></span> |<span data-ttu-id="c6dde-192">데이터베이스의 컬렉션 피드</span><span class="sxs-lookup"><span data-stu-id="c6dde-192">Feed of collections under a database</span></span> |
| <span data-ttu-id="c6dde-193">/dbs/{dbName}/colls/{collName}</span><span class="sxs-lookup"><span data-stu-id="c6dde-193">/dbs/{dbName}/colls/{collName}</span></span> |<span data-ttu-id="c6dde-194">{collName} 값과 ID가 일치하는 컬렉션</span><span class="sxs-lookup"><span data-stu-id="c6dde-194">Collection with an id matching the value {collName}</span></span> |
| <span data-ttu-id="c6dde-195">/dbs/{dbName}/colls/{collName}/docs</span><span class="sxs-lookup"><span data-stu-id="c6dde-195">/dbs/{dbName}/colls/{collName}/docs</span></span> |<span data-ttu-id="c6dde-196">컬렉션의 문서 피드</span><span class="sxs-lookup"><span data-stu-id="c6dde-196">Feed of documents under a collection</span></span> |
| <span data-ttu-id="c6dde-197">/dbs/{dbName}/colls/{collName}/docs/{docId}</span><span class="sxs-lookup"><span data-stu-id="c6dde-197">/dbs/{dbName}/colls/{collName}/docs/{docId}</span></span> |<span data-ttu-id="c6dde-198">{doc} 값과 ID가 일치하는 문서</span><span class="sxs-lookup"><span data-stu-id="c6dde-198">Document with an id matching the value {doc}</span></span> |
| <span data-ttu-id="c6dde-199">/dbs/{dbName}/users/</span><span class="sxs-lookup"><span data-stu-id="c6dde-199">/dbs/{dbName}/users/</span></span> |<span data-ttu-id="c6dde-200">데이터베이스의 사용자 피드</span><span class="sxs-lookup"><span data-stu-id="c6dde-200">Feed of users under a database</span></span> |
| <span data-ttu-id="c6dde-201">/dbs/{dbName}/users/{userId}</span><span class="sxs-lookup"><span data-stu-id="c6dde-201">/dbs/{dbName}/users/{userId}</span></span> |<span data-ttu-id="c6dde-202">{user} 값과 ID가 일치하는 사용자</span><span class="sxs-lookup"><span data-stu-id="c6dde-202">User with an id matching the value {user}</span></span> |
| <span data-ttu-id="c6dde-203">/dbs/{dbName}/users/{userId}/permissions</span><span class="sxs-lookup"><span data-stu-id="c6dde-203">/dbs/{dbName}/users/{userId}/permissions</span></span> |<span data-ttu-id="c6dde-204">사용자의 사용 권한 피드</span><span class="sxs-lookup"><span data-stu-id="c6dde-204">Feed of permissions under a user</span></span> |
| <span data-ttu-id="c6dde-205">/dbs/{dbName}/users/{userId}/permissions/{permissionId}</span><span class="sxs-lookup"><span data-stu-id="c6dde-205">/dbs/{dbName}/users/{userId}/permissions/{permissionId}</span></span> |<span data-ttu-id="c6dde-206">{permission} 값과 ID가 일치하는 사용 권한</span><span class="sxs-lookup"><span data-stu-id="c6dde-206">Permission with an id matching the value {permission}</span></span> |

<span data-ttu-id="c6dde-207">각 리소스에는 id 속성을 통해 노출되는 고유한 사용자 정의 이름도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-207">Each resource has a unique user defined name exposed via the id property.</span></span> <span data-ttu-id="c6dde-208">참고: 문서의 경우 사용자가 ID를 지정하지 않으면 지원되는 SDK에서 문서의 고유 ID를 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-208">Note: for documents, if the user does not specify an id, our supported SDKs will automatically generate a unique id for the document.</span></span> <span data-ttu-id="c6dde-209">id는 특정 상위 리소스 컨텍스트 내에서 고유한 최대 256자로 된 사용자 정의 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-209">The id is a user defined string, of up to 256 characters that is unique within the context of a specific parent resource.</span></span> 

<span data-ttu-id="c6dde-210">각 리소스에는 _rid 속성을 통해 사용할 수 있는 시스템 생성 계층적 리소스 식별자(RID라고도 함)도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-210">Each resource also has a system generated hierarchical resource identifier (also referred to as an RID), which is available via the _rid property.</span></span> <span data-ttu-id="c6dde-211">RID는 지정된 리소스의 전체 계층 구조를 인코드하며 분산 방식으로 참조 무결성을 적용하는 데 사용되는 매우 편리한 내부 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-211">The RID encodes the entire hierarchy of a given resource and it is a convenient internal representation used to enforce referential integrity in a distributed manner.</span></span> <span data-ttu-id="c6dde-212">RID는 데이터베이스 계정 내에서 고유하며 파티션 간 조회가 필요 없는 효율적인 라우팅을 위해 Cosmos DB에서 내부적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-212">The RID is unique within a database account and it is internally used by Cosmos DB for efficient routing without requiring cross partition lookups.</span></span> <span data-ttu-id="c6dde-213">_self 및 _rid 속성 값은 둘 다 리소스의 대체 정식 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-213">The values of the _self and the  _rid properties are both alternate and canonical representations of a resource.</span></span> 

<span data-ttu-id="c6dde-214">REST API는 id 및 _rid 속성으로 리소스의 주소 지정과 요청의 라우팅을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-214">The REST APIs support addressing of resources and routing of requests by both the id and the _rid properties.</span></span>

## <a name="database-accounts"></a><span data-ttu-id="c6dde-215">데이터베이스 계정</span><span class="sxs-lookup"><span data-stu-id="c6dde-215">Database accounts</span></span>
<span data-ttu-id="c6dde-216">Azure 구독을 사용하여 Cosmos DB 데이터베이스 계정을 하나 이상 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-216">You can provision one or more Cosmos DB database accounts using your Azure subscription.</span></span>

<span data-ttu-id="c6dde-217">Azure Portal([http://portal.azure.com/](https://portal.azure.com/))을 통해 Cosmos DB 데이터베이스 계정을 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-217">You can create and manage Cosmos DB database accounts via the Azure Portal at [http://portal.azure.com/](https://portal.azure.com/).</span></span> <span data-ttu-id="c6dde-218">데이터베이스 계정을 만들고 관리하려면 관리 액세스 권한이 필요하며 Azure 구독으로만 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-218">Creating and managing a database account requires administrative access and can only be performed under your Azure subscription.</span></span> 

### <a name="database-account-properties"></a><span data-ttu-id="c6dde-219">데이터베이스 계정 속성</span><span class="sxs-lookup"><span data-stu-id="c6dde-219">Database account properties</span></span>
<span data-ttu-id="c6dde-220">데이터베이스 계정 프로비전 및 관리의 일부로 다음 속성을 구성하고 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-220">As part of provisioning and managing a database account you can configure and read the following properties:</span></span>  

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="c6dde-221"><strong>속성 이름</strong></span><span class="sxs-lookup"><span data-stu-id="c6dde-221"><strong>Property Name</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c6dde-222"><strong>설명</strong></span><span class="sxs-lookup"><span data-stu-id="c6dde-222"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="c6dde-223">일관성 정책</span><span class="sxs-lookup"><span data-stu-id="c6dde-223">Consistency Policy</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c6dde-224">데이터베이스 계정 아래의 모든 컬렉션에 대한 기본 일관성 수준을 구성하려면 이 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-224">Set this property to configure the default consistency level for all the collections under your database account.</span></span> <span data-ttu-id="c6dde-225">[x-ms-consistency-level] 요청 헤더를 사용하여 요청 단위로 일관성 수준을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-225">You can override the consistency level on a per request basis using the [x-ms-consistency-level] request header.</span></span> <p><p><span data-ttu-id="c6dde-226">이 속성은 <i>사용자 정의 리소스</i>에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-226">Note that this property only applies to the <i>user defined resources</i>.</span></span> <span data-ttu-id="c6dde-227">모든 시스템 정의 리소스는 강력한 일관성으로 읽기/쿼리를 지원하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-227">All system defined resources are configured to support reads/queries with strong consistency.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="c6dde-228">권한 부여 키</span><span class="sxs-lookup"><span data-stu-id="c6dde-228">Authorization Keys</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="c6dde-229">이러한 키는 데이터베이스 계정 아래의 모든 리소스에 대한 관리 액세스 권한을 제공하는 기본 및 보조 마스터 키이며 읽기 전용 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-229">These are the primary and secondary master and readonly keys that provide administrative access to all of the resources under the database account.</span></span></p></td>
        </tr>
    </tbody>
</table>

<span data-ttu-id="c6dde-230">Azure Portal에서 데이터베이스 계정을 프로비전, 구성 및 관리하는 것뿐 아니라 [Azure Cosmos DB REST API](/rest/api/documentdb/) 및 [클라이언트 SDK](documentdb-sdk-dotnet.md)를 사용하여 프로그래밍 방식으로 Cosmos DB 데이터베이스 계정을 만들고 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-230">Note that in addition to provisioning, configuring and managing your database account from the Azure Portal, you can also programmatically create and manage Cosmos DB database accounts by using the [Azure Cosmos DB REST APIs](/rest/api/documentdb/) as well as [client SDKs](documentdb-sdk-dotnet.md).</span></span>  

## <a name="databases"></a><span data-ttu-id="c6dde-231">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="c6dde-231">Databases</span></span>
<span data-ttu-id="c6dde-232">Cosmos DB 데이터베이스는 다음 다이어그램에 표시된 것처럼 하나 이상의 컬렉션 및 사용자의 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-232">A Cosmos DB database is a logical container of one or more collections and users, as shown in the following diagram.</span></span> <span data-ttu-id="c6dde-233">Cosmos DB 데이터베이스 계정에 데이터베이스를 개수에 제한 없이 만들 수 있으며 제공 한도가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-233">You can create any number of databases under a Cosmos DB database account subject to offer limits.</span></span>  

<span data-ttu-id="c6dde-234">![데이터베이스 계정 및 컬렉션 계층적 모델][2]</span><span class="sxs-lookup"><span data-stu-id="c6dde-234">![Database account and collections hierarchical model][2]</span></span>  
<span data-ttu-id="c6dde-235">**데이터베이스는 사용자 및 컬렉션의 논리적 컨테이너입니다.**</span><span class="sxs-lookup"><span data-stu-id="c6dde-235">**A Database is a logical container of users and collections**</span></span>

<span data-ttu-id="c6dde-236">한 데이터베이스에는 컬렉션 내에서 분할된 거의 무제한의 문서 저장소를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-236">A database can contain virtually unlimited document storage partitioned within collections.</span></span>

### <a name="elastic-scale-of-a-cosmos-db-database"></a><span data-ttu-id="c6dde-237">Cosmos DB 데이터베이스의 탄력적인 확장</span><span class="sxs-lookup"><span data-stu-id="c6dde-237">Elastic scale of a Cosmos DB database</span></span>
<span data-ttu-id="c6dde-238">Cosmos DB 데이터베이스는 기본적으로 탄력적이며 SSD 지원 문서 저장소 및 프로비전된 처리량이 몇 GB에서 페타바이트 범위까지 다양합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-238">A Cosmos DB database is elastic by default – ranging from a few GB to petabytes of SSD backed document storage and provisioned throughput.</span></span> 

<span data-ttu-id="c6dde-239">기존의 RDBMS 데이터베이스와 달리 Cosmos DB의 데이터베이스는 단일 컴퓨터로 범위가 지정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-239">Unlike a database in traditional RDBMS, a database in Cosmos DB is not scoped to a single machine.</span></span> <span data-ttu-id="c6dde-240">Cosmos DB를 사용하면 응용 프로그램 확장 요구에 따라 컬렉션, 데이터베이스 또는 둘 다를 더 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-240">With Cosmos DB, as your application’s scale needs to grow, you can create more collections, databases, or both.</span></span> <span data-ttu-id="c6dde-241">실제로 Microsoft 내의 다양한 자사 응용 프로그램은 각각 테라바이트의 문서 저장소가 있는 컬렉션이 수천 개 포함된 대형 Cosmos DB 데이터베이스를 만들어 소비자 배율로 Cosmos DB를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-241">Indeed, various first party applications within Microsoft have been using Cosmos DB at a consumer scale by creating extremely large Cosmos DB databases each containing thousands of collections with terabytes of document storage.</span></span> <span data-ttu-id="c6dde-242">응용 프로그램의 크기 조정 요구 사항을 충족하기 위해 컬렉션을 추가 또는 제거하여 데이터베이스를 확장하거나 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-242">You can grow or shrink a database by adding or removing collections to meet your application’s scale requirements.</span></span> 

<span data-ttu-id="c6dde-243">제품에 적용되는 데이터베이스 내에 컬렉션을 개수에 제한 없이 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-243">You can create any number of collections within a database subject to the offer.</span></span> <span data-ttu-id="c6dde-244">각 컬렉션에는 선택한 성능 계층에 따라 SSD 지원 저장소 및 처리량이 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-244">Each collection has SSD backed storage and throughput provisioned for you depending on the selected performance tier.</span></span>

<span data-ttu-id="c6dde-245">Cosmos DB 데이터베이스는 사용자 컨테이너이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-245">A Cosmos DB database is also a container of users.</span></span> <span data-ttu-id="c6dde-246">다시 사용자는 컬렉션, 문서 및 첨부 파일에 대한 미세 조정된 권한 부여 및 액세스 권한을 제공하는 사용 권한 집합의 논리적 네임스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-246">A user, in-turn, is a logical namespace for a set of permissions that provides fine-grained authorization and access to collections, documents and attachments.</span></span>  

<span data-ttu-id="c6dde-247">Cosmos DB 리소스 모델의 다른 리소스와 마찬가지로, [REST API](/rest/api/documentdb/) 또는 [클라이언트 SDK](documentdb-sdk-dotnet.md)를 사용하여 데이터베이스를 쉽게 만들거나, 바꾸거나, 삭제하거나, 읽거나, 열거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-247">As with other resources in the Cosmos DB resource model, databases can be created, replaced, deleted, read or enumerated easily using either the [REST APIs](/rest/api/documentdb/) or any of the [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="c6dde-248">Cosmos DB는 데이터베이스 리소스의 메타데이터 읽기 또는 쿼리에 대해 강력한 일관성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-248">Cosmos DB guarantees strong consistency for reading or querying the metadata of a database resource.</span></span> <span data-ttu-id="c6dde-249">데이터베이스를 삭제하면 자동으로 컬렉션 또는 컬렉션 내에 포함된 사용자에 액세스할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-249">Deleting a database automatically ensures that you cannot access any of the collections or users contained within it.</span></span>   

## <a name="collections"></a><span data-ttu-id="c6dde-250">컬렉션</span><span class="sxs-lookup"><span data-stu-id="c6dde-250">Collections</span></span>
<span data-ttu-id="c6dde-251">Cosmos DB 컬렉션은 JSON 문서의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-251">A Cosmos DB collection is a container for your JSON documents.</span></span> 

### <a name="elastic-ssd-backed-document-storage"></a><span data-ttu-id="c6dde-252">탄력적 SSD 지원 문서 저장소</span><span class="sxs-lookup"><span data-stu-id="c6dde-252">Elastic SSD backed document storage</span></span>
<span data-ttu-id="c6dde-253">컬렉션은 본질적으로 탄력적입니다. 문서를 추가하거나 제거하면 자동으로 확장 및 축소됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-253">A collection is intrinsically elastic - it automatically grows and shrinks as you add or remove documents.</span></span> <span data-ttu-id="c6dde-254">컬렉션은 하나 이상의 물리적 파티션 또는 서버에 걸쳐 있을 수 있는 논리적 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-254">Collections are logical resources and can span one or more physical partitions or servers.</span></span> <span data-ttu-id="c6dde-255">컬렉션 내의 파티션 수는 컬렉션의 프로비전된 처리량 및 저장소 크기에 따라 Cosmos DB에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-255">The number of partitions within a collection is determined by Cosmos DB based on the storage size and the provisioned throughput of your collection.</span></span> <span data-ttu-id="c6dde-256">Cosmos DB의 모든 파티션은 고정된 양의 SSD 지원 저장소에 연결되며, 고가용성을 위해 복제됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-256">Every partition in Cosmos DB has a fixed amount of SSD-backed storage associated with it, and is replicated for high availability.</span></span> <span data-ttu-id="c6dde-257">파티션 관리는 Azure Cosmos DB에 의해 완전히 관리되므로 복잡한 코드를 작성하거나 파티션을 관리할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-257">Partition management is fully managed by Azure Cosmos DB, and you do not have to write complex code or manage your partitions.</span></span> <span data-ttu-id="c6dde-258">Cosmos DB 컬렉션은 저장소 및 처리량이 **거의 무제한**입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-258">Cosmos DB collections are **practically unlimited** in terms of storage and throughput.</span></span> 

### <a name="automatic-indexing-of-collections"></a><span data-ttu-id="c6dde-259">컬렉션의 자동 인덱싱</span><span class="sxs-lookup"><span data-stu-id="c6dde-259">Automatic indexing of collections</span></span>
<span data-ttu-id="c6dde-260">Cosmos DB는 진정한 스키마 없는 데이터베이스 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-260">Cosmos DB is a true schema-free database system.</span></span> <span data-ttu-id="c6dde-261">JSON 문서에 대해 스키마를 가정하거나 요구하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-261">It does not assume or require any schema for the JSON documents.</span></span> <span data-ttu-id="c6dde-262">컬렉션에 문서를 추가하면 Cosmos DB에서 자동으로 인덱싱하며 문서를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-262">As you add documents to a collection, Cosmos DB automatically indexes them and they are available for you to query.</span></span> <span data-ttu-id="c6dde-263">스키마 또는 보조 인덱스가 필요 없는 자동 문서 인덱싱은 Cosmos DB의 주요 기능이며 쓰기 최적화되고 잠금이 없으며 로그 구조화된 인덱스 유지 관리 기술을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-263">Automatic indexing of documents without requiring schema or secondary indexes is a key capability of Cosmos DB and is enabled by write-optimized, lock-free and log-structured index maintenance techniques.</span></span> <span data-ttu-id="c6dde-264">Cosmos DB는 일관성 있는 쿼리를 제공하는 동시에 매우 빠른 쓰기의 지속적인 볼륨을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-264">Cosmos DB supports sustained volume of extremely fast writes while still serving consistent queries.</span></span> <span data-ttu-id="c6dde-265">문서 및 인덱스 저장소는 각 컬렉션에서 사용하는 저장소를 계산하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-265">Both document and index storage are used to calculate the storage consumed by each collection.</span></span> <span data-ttu-id="c6dde-266">컬렉션에 대한 인덱싱 정책을 구성하여 인덱싱과 관련된 저장소 및 성능 절충을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-266">You can control the storage and performance trade-offs associated with indexing by configuring the indexing policy for a collection.</span></span> 

### <a name="configuring-the-indexing-policy-of-a-collection"></a><span data-ttu-id="c6dde-267">컬렉션의 인덱싱 정책 구성</span><span class="sxs-lookup"><span data-stu-id="c6dde-267">Configuring the indexing policy of a collection</span></span>
<span data-ttu-id="c6dde-268">각 컬렉션의 인덱싱 정책을 사용하여 인덱싱과 관련된 성능 및 저장소 절충을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-268">The indexing policy of each collection allows you to make performance and storage trade-offs associated with indexing.</span></span> <span data-ttu-id="c6dde-269">인덱싱 구성의 일부로 사용할 수 있는 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-269">The following options are available to you as part of indexing configuration:</span></span>  

* <span data-ttu-id="c6dde-270">컬렉션에서 모든 문서를 자동으로 인덱싱할지 여부를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-270">Choose whether the collection automatically indexes all of the documents or not.</span></span> <span data-ttu-id="c6dde-271">기본적으로 모든 문서가 자동으로 인덱싱됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-271">By default, all documents are automatically indexed.</span></span> <span data-ttu-id="c6dde-272">자동 인덱싱을 해제하고 특정 문서만 인덱스에 선택적으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-272">You can choose to turn off automatic indexing and selectively add only specific documents to the index.</span></span> <span data-ttu-id="c6dde-273">반대로 특정 문서만 선택적으로 제외할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-273">Conversely, you can selectively choose to exclude only specific documents.</span></span> <span data-ttu-id="c6dde-274">문서를 삽입하거나 바꾸거나 삭제하는 동안 컬렉션의 indexingPolicy에서 automatic 속성을 true 또는 false로 설정하고 [x-ms-indexingdirective] 요청 헤더를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-274">You can achieve this by setting the automatic property to be true or false on the indexingPolicy of a collection and using the [x-ms-indexingdirective] request header while inserting, replacing or deleting a document.</span></span>  
* <span data-ttu-id="c6dde-275">문서의 특정 경로나 패턴을 인덱스에 포함할지 아니면 제외할지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-275">Choose whether to include or exclude specific paths or patterns in your documents from the index.</span></span> <span data-ttu-id="c6dde-276">컬렉션의 indexingPolicy에서 각각 includedPaths 및 excludedPaths를 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-276">You can achieve this by setting includedPaths and excludedPaths on the indexingPolicy of a collection respectively.</span></span> <span data-ttu-id="c6dde-277">특정 경로 패턴의 범위 및 해시 쿼리에 대해 저장소 및 성능 절충을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-277">You can also configure the storage and performance trade-offs for range and hash queries for specific path patterns.</span></span> 
* <span data-ttu-id="c6dde-278">동기(일관성) 및 비동기(지연) 인덱스 업데이트 간에 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-278">Choose between synchronous (consistent) and asynchronous (lazy) index updates.</span></span> <span data-ttu-id="c6dde-279">기본적으로 컬렉션의 문서를 삽입하거나 바꾸거나 삭제할 때마다 인덱스가 동기적으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-279">By default, the index is updated synchronously on each insert, replace or delete of a document to the collection.</span></span> <span data-ttu-id="c6dde-280">이렇게 하면 쿼리에 문서 읽기와 동일한 일관성 수준을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-280">This enables the queries to honor the same consistency level as that of the document reads.</span></span> <span data-ttu-id="c6dde-281">Cosmos DB는 쓰기 최적화되며 동기 인덱스 유지 관리 및 일관성 있는 쿼리 처리와 함께 지속적인 대량 문서 쓰기를 지원하지만 인덱스를 지연 업데이트하도록 특정 컬렉션을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-281">While Cosmos DB is write optimized and supports sustained volumes of document writes along with synchronous index maintenance and serving consistent queries, you can configure certain collections to update their index lazily.</span></span> <span data-ttu-id="c6dde-282">지연 인덱스는 쓰기 성능을 더욱 향상하며 주로 읽기 중심인 컬렉션에 대한 대량 수집 시나리오에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-282">Lazy indexing boosts the write performance further and is ideal for bulk ingestion scenarios for primarily read-heavy collections.</span></span>

<span data-ttu-id="c6dde-283">인덱싱 정책은 컬렉션에서 PUT를 실행하여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-283">The indexing policy can be changed by executing a PUT on the collection.</span></span> <span data-ttu-id="c6dde-284">[클라이언트 SDK](documentdb-sdk-dotnet.md), [Azure Portal](https://portal.azure.com) 또는 [REST API](/rest/api/documentdb/)를 통해 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-284">This can be achieved either through the [client SDK](documentdb-sdk-dotnet.md), the [Azure Portal](https://portal.azure.com) or the [REST APIs](/rest/api/documentdb/).</span></span>

### <a name="querying-a-collection"></a><span data-ttu-id="c6dde-285">컬렉션 쿼리</span><span class="sxs-lookup"><span data-stu-id="c6dde-285">Querying a collection</span></span>
<span data-ttu-id="c6dde-286">컬렉션 내의 문서는 임의 스키마를 포함할 수 있으며, 스키마 또는 보조 인덱스를 미리 제공하지 않고 컬렉션 내의 문서를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-286">The documents within a collection can have arbitrary schemas and you can query documents within a collection without providing any schema or secondary indices upfront.</span></span> <span data-ttu-id="c6dde-287">JavaScript 기반 UDF를 통해 풍부한 계층적, 관계형 및 공간 연산자와 확장성을 제공하는 [Azure Cosmos DB DocumentDB API: SQL 구문 참조](https://msdn.microsoft.com/library/azure/dn782250.aspx)를 사용하여 컬렉션을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-287">You can query the collection using the [Azure Cosmos DB DocumentDB API: SQL syntax reference](https://msdn.microsoft.com/library/azure/dn782250.aspx), which provides rich hierarchical, relational, and spatial operators and extensibility via JavaScript-based UDFs.</span></span> <span data-ttu-id="c6dde-288">JSON 문법을 통해 JSON 문서를 트리로 모델링하고 레이블을 트리 노드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-288">JSON grammar allows for modeling JSON documents as trees with labels as the tree nodes.</span></span> <span data-ttu-id="c6dde-289">이 기능은 DocumentDB API의 자동 인덱싱 기술과 DocumentDB API의 SQL 언어 둘 다에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-289">This is exploited both by DocumentDB API’s automatic indexing techniques as well as DocumentDB API's SQL dialect.</span></span> <span data-ttu-id="c6dde-290">DocumentDB API 쿼리 언어는 다음 세 가지 주요 측면으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-290">The DocumetDB API query language consists of three main aspects:</span></span>   

1. <span data-ttu-id="c6dde-291">기본적으로 계층적 쿼리 및 프로젝션을 포함하는 트리 구조에 매핑되는 작은 쿼리 작업 집합</span><span class="sxs-lookup"><span data-stu-id="c6dde-291">A small set of query operations that map naturally to the tree structure including hierarchical queries and projections.</span></span> 
2. <span data-ttu-id="c6dde-292">컴퍼지션, 필터, 프로젝션, 집계 및 자체 조인을 포함하는 관계형 작업 하위 집합</span><span class="sxs-lookup"><span data-stu-id="c6dde-292">A subset of relational operations including composition, filter, projections, aggregates and self joins.</span></span> 
3. <span data-ttu-id="c6dde-293">(1) 및 (2)로 작동하는 순수 JavaScript기반 UDF</span><span class="sxs-lookup"><span data-stu-id="c6dde-293">Pure JavaScript based UDFs that work with (1) and (2).</span></span>  

<span data-ttu-id="c6dde-294">Cosmos DB 쿼리 모델은 기능, 효율성 및 간결성 간의 균형을 이루려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-294">The Cosmos DB query model attempts to strike a balance between functionality, efficiency and simplicity.</span></span> <span data-ttu-id="c6dde-295">Cosmos DB의 데이터베이스 엔진은 기본적으로 SQL 쿼리 문을 컴파일하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-295">The Cosmos DB database engine natively compiles and executes the SQL query statements.</span></span> <span data-ttu-id="c6dde-296">[REST API](/rest/api/documentdb/) 또는 [클라이언트 SDK](documentdb-sdk-dotnet.md)를 사용하여 컬렉션을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-296">You can query a collection using the [REST APIs](/rest/api/documentdb/) or any of the [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="c6dde-297">.NET SDK에는 LINQ 공급자가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-297">The .NET SDK comes with a LINQ provider.</span></span>

> [!TIP]
> <span data-ttu-id="c6dde-298">[Query Playground](https://www.documentdb.com/sql/demo)(쿼리 실습)에서 DocumentDB API를 사용해 보고 데이터 집합에 대해 SQL 쿼리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-298">You can try out the DocumentDB API and run SQL queries against our dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
> 
> 

## <a name="multi-document-transactions"></a><span data-ttu-id="c6dde-299">다중 문서 트랜잭션</span><span class="sxs-lookup"><span data-stu-id="c6dde-299">Multi-document transactions</span></span>
<span data-ttu-id="c6dde-300">데이터베이스 트랜잭션은 데이터 동시 변경을 처리하기 위한 안전하고 예측 가능한 프로그래밍 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-300">Database transactions provide a safe and predictable programming model for dealing with concurrent changes to the data.</span></span> <span data-ttu-id="c6dde-301">RDBMS에서 비즈니스 논리를 작성하는 기존 방법은 **저장 프로시저** 및/또는 **트리거**를 작성하고 트랜잭션 실행을 위해 데이터베이스 서버에 전달하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-301">In RDBMS, the traditional way to write business logic is to write **stored-procedures** and/or **triggers** and ship it to the database server for transactional execution.</span></span> <span data-ttu-id="c6dde-302">RDBMS에서는 응용 프로그램 프로그래머가 다음 두 가지 프로그래밍 언어를 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-302">In RDBMS, the application programmer is required to deal with two disparate programming languages:</span></span> 

* <span data-ttu-id="c6dde-303">(비트랜잭션) 응용 프로그램 프로그래밍 언어(예: JavaScript, Python, C#, Java 등)</span><span class="sxs-lookup"><span data-stu-id="c6dde-303">The (non-transactional) application programming language (e.g. JavaScript, Python, C#, Java, etc.)</span></span>
* <span data-ttu-id="c6dde-304">T-SQL(데이터베이스에서 고유하게 실행되는 트랜잭션 프로그래밍 언어)</span><span class="sxs-lookup"><span data-stu-id="c6dde-304">T-SQL, the transactional programming language which is natively executed by the database</span></span>

<span data-ttu-id="c6dde-305">데이터베이스 엔진 내에 직접 JavaScript 및 JSON을 전체 통합하므로 Cosmos DB는 저장 프로시저 및 트리거 측면에서 컬렉션에 대해 직접 JavaScript 기반 응용 프로그램 논리를 실행하기 위한 직관적 프로그래밍 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-305">By virtue of its deep commitment to JavaScript and JSON directly within the database engine, Cosmos DB provides an intuitive programming model for executing JavaScript based application logic directly on the collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="c6dde-306">여기에서는 다음 두 가지가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-306">This allows for both of the following:</span></span>

* <span data-ttu-id="c6dde-307">동시성 제어를 위한 효율적인 구현, 복구, 데이터베이스에 엔진에서 JSON 개체 그래프에 대한 직접적인 자동 인덱싱</span><span class="sxs-lookup"><span data-stu-id="c6dde-307">Efficient implementation of concurrency control, recovery, automatic indexing of the JSON object graphs directly in the database engine</span></span>
* <span data-ttu-id="c6dde-308">자연스러운 제어 흐름 표현, 변수 범위 지정, JavaScript 프로그래밍 언어로 직접 데이터베이스 트랜잭션과 예외 처리 Primitive의 통합</span><span class="sxs-lookup"><span data-stu-id="c6dde-308">Naturally expressing control flow, variable scoping, assignment and integration of exception handling primitives with database transactions directly in terms of the JavaScript programming language</span></span>

<span data-ttu-id="c6dde-309">그런 다음 컬렉션 수준에서 등록된 JavaScript 논리가 지정된 컬렉션의 문서에 대해 데이터베이스 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-309">The JavaScript logic registered at a collection level can then issue database operations on the documents of the given collection.</span></span> <span data-ttu-id="c6dde-310">Cosmos DB는 JavaScript 기반 저장 프로시저와 트리거를 앰비언트 ACID 트랜잭션 내에 암시적으로 래핑하고 컬렉션 내 문서에 스냅숏 격리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-310">Cosmos DB implicitly wraps the JavaScript based stored procedures and triggers within an ambient ACID transactions with snapshot isolation across documents within a collection.</span></span> <span data-ttu-id="c6dde-311">실행 중 JavaScript에서 예외가 발생하면 전체 트랜잭션이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-311">During the course of its execution, if the JavaScript throws an exception, then the entire transaction is aborted.</span></span> <span data-ttu-id="c6dde-312">결과로 생성된 프로그래밍 모델은 매우 단순하지만 강력합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-312">The resulting programming model is a very simple yet powerful.</span></span> <span data-ttu-id="c6dde-313">JavaScript 개발자는 익숙한 언어 구문과 라이브러리 기본 형식을 사용하는 동시에 "내구성" 있는 프로그래밍 모델을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-313">JavaScript developers get a “durable” programming model while still using their familiar language constructs and library primitives.</span></span>   

<span data-ttu-id="c6dde-314">버퍼 풀과 동일한 주소 공간에 있는 데이터베이스 엔진 내에서 직접 JavaScript를 실행할 수 있으므로 컬렉션 문서에 대한 데이터베이스 작업의 신속한 트랜잭션 실행이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-314">The ability to execute JavaScript directly within the database engine in the same address space as the buffer pool enables performant and transactional execution of database operations against the documents of a collection.</span></span> <span data-ttu-id="c6dde-315">또한 Cosmos DB 데이터베이스 엔진은 JSON 및 JavaScript를 전체 통합하므로 응용 프로그램과 데이터베이스의 형식 시스템 간 불일치가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-315">Furthermore, Cosmos DB database engine makes a deep commitment to the JSON and JavaScript eliminates any impedance mismatch between the type systems of application and the database.</span></span>   

<span data-ttu-id="c6dde-316">컬렉션을 만든 후 [REST API](/rest/api/documentdb/) 또는 [클라이언트 SDK](documentdb-sdk-dotnet.md)를 사용하여 저장 프로시저, 트리거 및 UDF를 컬렉션에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-316">After creating a collection, you can register stored procedures, triggers and UDFs with a collection using the [REST APIs](/rest/api/documentdb/) or any of the [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="c6dde-317">등록이 완료되면 참조하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-317">After registration, you can reference and execute them.</span></span> <span data-ttu-id="c6dde-318">아래 코드의 JavaScript로만 작성된 다음 저장 프로시저는 두 개의 인수(책 이름 및 저자 이름)를 사용하며 새 문서를 만들고 문서를 쿼리한 다음 업데이트합니다. 모든 작업은 암시적 ACID 트랜잭션 내에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-318">Consider the following stored procedure written entirely in JavaScript, the code below takes two arguments (book name and author name) and creates a new document, queries for a document and then updates it – all within an implicit ACID transaction.</span></span> <span data-ttu-id="c6dde-319">실행 중 언제든지 JavaScript 예외가 발생하면 전체 트랜잭션이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-319">At any point during the execution, if a JavaScript exception is thrown, the entire transaction aborts.</span></span>

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();        
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            {id: name, author: author},
            function(err, documentCreated) {
                if(err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function(err, matchingDocuments) {
                        if(err) throw new Error(err.message);

                        context.getResponse().setBody(matchingDocuments.length);

                        // Replace the author name for all documents that satisfied the query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don’t need to execute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);   
                        }
                    })
            })
    };

<span data-ttu-id="c6dde-320">클라이언트는 HTTP POST를 통한 트랜잭션 실행을 위해 위의 JavaScript 논리를 데이터베이스에 "전달"할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-320">The client can “ship” the above JavaScript logic to the database for transactional execution via HTTP POST.</span></span> <span data-ttu-id="c6dde-321">HTTP 메서드 사용에 대한 자세한 내용은 [Azure Cosmos DB 리소스와 RESTful 상호 작용](https://msdn.microsoft.com/library/azure/mt622086.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6dde-321">For more information about using HTTP methods, see [RESTful interactions with Azure Cosmos DB resources](https://msdn.microsoft.com/library/azure/mt622086.aspx).</span></span> 

    client.createStoredProcedureAsync(collection._self, {id: "CRUDProc", body: businessLogic})
       .then(function(createdStoredProcedure) {
            return client.executeStoredProcedureAsync(createdStoredProcedure.resource._self,
                "NoSQL Distilled",
                "Martin Fowler");
        })
        .then(function(result) {
            console.log(result);
        },
        function(error) {
            console.log(error);
        });


<span data-ttu-id="c6dde-322">데이터베이스는 기본적으로 JSON 및 JavaScript를 이해하므로 형식 시스템 불일치가 없으며 "OR 매핑" 또는 코드 생성 기술도 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-322">Notice that because the database natively understands JSON and JavaScript, there is no type system mismatch, no “OR mapping” or code generation magic required.</span></span>   

<span data-ttu-id="c6dde-323">저장 프로시저와 트리거는 현재 컬렉션 컨텍스트를 노출하는 잘 정의된 개체 모델을 통해 컬렉션 및 컬렉션 내 문서를 조작합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-323">Stored procedures and triggers interact with a collection and the documents in a collection through a well-defined object model, which exposes the current collection context.</span></span>  

<span data-ttu-id="c6dde-324">[REST API](/rest/api/documentdb/) 또는 [클라이언트 SDK](documentdb-sdk-dotnet.md)를 사용하여 DocumentDB API의 컬렉션을 쉽게 만들거나 삭제하거나 읽거나 열거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-324">Collections in the DocumentDB API can be created, deleted, read or enumerated easily using either the [REST APIs](/rest/api/documentdb/) or any of the [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="c6dde-325">DocumentDB API는 컬렉션의 메타데이터 읽기 또는 쿼리에 대해 항상 강력한 일관성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-325">The DocumentDB API always provides strong consistency for reading or querying the metadata of a collection.</span></span> <span data-ttu-id="c6dde-326">컬렉션을 삭제하면 자동으로 컬렉션 내에 포함된 문서, 첨부 파일, 저장 프로시저, 트리거 및 UDF에 액세스할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-326">Deleting a collection automatically ensures that you cannot access any of the documents, attachments, stored procedures, triggers, and UDFs contained within it.</span></span>   

## <a name="stored-procedures-triggers-and-user-defined-functions-udf"></a><span data-ttu-id="c6dde-327">저장 프로시저, 트리거 및 UDF(사용자 정의 함수)</span><span class="sxs-lookup"><span data-stu-id="c6dde-327">Stored procedures, triggers and User Defined Functions (UDF)</span></span>
<span data-ttu-id="c6dde-328">이전 섹션에서 설명한 대로 데이터베이스 엔진의 내부 트랜잭션 내에서 직접 실행할 응용 프로그램 논리를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-328">As described in the previous section, you can write application logic to run directly within a transaction inside of the database engine.</span></span> <span data-ttu-id="c6dde-329">전적으로 JavaScript로 응용 프로그램 논리를 작성하고 저장 프로시저, 트리거 또는 UDF로 모델링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-329">The application logic can be written entirely in JavaScript and can be modeled as a stored procedure, trigger or a UDF.</span></span> <span data-ttu-id="c6dde-330">저장 프로시저 또는 트리거 내의 JavaScript 코드는 컬렉션 내 문서를 삽입하거나 바꾸거나 삭제하거나 읽거나 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-330">The JavaScript code within a stored procedure or a trigger can insert, replace, delete, read or query documents within a collection.</span></span> <span data-ttu-id="c6dde-331">반면에 UDF 내에서 JavaScript는 문서를 삽입, 바꾸기 또는 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-331">On the other hand, the JavaScript within a UDF cannot insert, replace, or delete documents.</span></span> <span data-ttu-id="c6dde-332">UDF는 쿼리 결과 집합의 문서를 열거하고 다른 결과 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-332">UDFs enumerate the documents of a query's result set and produce another result set.</span></span> <span data-ttu-id="c6dde-333">다중 테넌트 지원을 위해 Cosmos DB는 엄격한 예약 기반 리소스 거버넌스를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-333">For multi-tenancy, Cosmos DB enforces a strict reservation based resource governance.</span></span> <span data-ttu-id="c6dde-334">각 저장 프로시저, 트리거 또는 UDF는 작업 수행을 위해 운영 체제 리소스의 고정 퀀텀을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-334">Each stored procedure, trigger or a UDF gets a fixed quantum of operating system resources to do its work.</span></span> <span data-ttu-id="c6dde-335">또한 저장 프로시저, 트리거 또는 UDF는 외부 JavaScript 라이브러리에 대해 연결할 수 없으며 할당된 리소스 예산을 초과할 경우 블랙리스트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-335">Furthermore, stored procedures, triggers or UDFs cannot link against external JavaScript libraries and are blacklisted if they exceed the resource budgets allocated to them.</span></span> <span data-ttu-id="c6dde-336">REST API를 통해 저장 프로시저, 트리거 또는 UDF를 컬렉션에 등록하거나 등록 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-336">You can register, unregister stored procedures, triggers or UDFs with a collection by using the REST APIs.</span></span>  <span data-ttu-id="c6dde-337">등록하면 저장 프로시저, 트리거 또는 UDF가 사전 컴파일되고 나중에 실행되는 바이트 코드로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-337">Upon registration a stored procedure, trigger, or a UDF is pre-compiled and stored as byte code which gets executed later.</span></span> <span data-ttu-id="c6dde-338">다음 섹션에서는 Cosmos DB JavaScript SDK를 사용하여 저장 프로시저, 트리거 및 UDF를 등록, 실행 및 등록 취소하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-338">The following section illustrate how you can use the Cosmos DB JavaScript SDK to register, execute, and unregister a stored procedure, trigger, and a UDF.</span></span> <span data-ttu-id="c6dde-339">JavaScript SDK는 [REST API](/rest/api/documentdb/) 위의 단순한 래퍼입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-339">The JavaScript SDK is a simple wrapper over the [REST APIs](/rest/api/documentdb/).</span></span> 

### <a name="registering-a-stored-procedure"></a><span data-ttu-id="c6dde-340">저장 프로시저 등록</span><span class="sxs-lookup"><span data-stu-id="c6dde-340">Registering a stored procedure</span></span>
<span data-ttu-id="c6dde-341">저장 프로시저 등록은 HTTP POST를 통해 컬렉션에 새 저장 프로시저 리소스를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-341">Registration of a stored procedure creates a new stored procedure resource on a collection via HTTP POST.</span></span>  

    var storedProc = {
        id: "validateAndCreate",
        body: function (documentToCreate) {
            documentToCreate.id = documentToCreate.id.toUpperCase();

            var collectionManager = getContext().getCollection();
            collectionManager.createDocument(collectionManager.getSelfLink(),
                documentToCreate,
                function(err, documentCreated) {
                    if(err) throw new Error('Error while creating document: ' + err.message;
                    getContext().getResponse().setBody('success - created ' + 
                            documentCreated.name);
                });
        }
    };

    client.createStoredProcedureAsync(collection._self, storedProc)
        .then(function (createdStoredProcedure) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-stored-procedure"></a><span data-ttu-id="c6dde-342">저장 프로시저 실행</span><span class="sxs-lookup"><span data-stu-id="c6dde-342">Executing a stored procedure</span></span>
<span data-ttu-id="c6dde-343">저장 프로시저 실행은 요청 본문에서 프로시저에 매개 변수를 전달하여 기존 저장 프로시저 리소스에 대해 HTTP POST를 실행하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-343">Execution of a stored procedure is done by issuing an HTTP POST against an existing stored procedure resource by passing parameters to the procedure in the request body.</span></span>

    var inputDocument = {id : "document1", author: "G. G. Marquez"};
    client.executeStoredProcedureAsync(createdStoredProcedure.resource._self, inputDocument)
        .then(function(executionResult) {
            assert.equal(executionResult, "success - created DOCUMENT1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-stored-procedure"></a><span data-ttu-id="c6dde-344">저장 프로시저 등록 취소</span><span class="sxs-lookup"><span data-stu-id="c6dde-344">Unregistering a stored procedure</span></span>
<span data-ttu-id="c6dde-345">저장 프로시저 등록 취소는 단순히 기존 저장 프로시저 리소스에 대해 HTTP DELETE를 실행하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-345">Unregistering a stored procedure is simply done by issuing an HTTP DELETE against an existing stored procedure resource.</span></span>   

    client.deleteStoredProcedureAsync(createdStoredProcedure.resource._self)
        .then(function (response) {
            return;
        }, function(error) {
            console.log("Error");
        });


### <a name="registering-a-pre-trigger"></a><span data-ttu-id="c6dde-346">사전 트리거 등록</span><span class="sxs-lookup"><span data-stu-id="c6dde-346">Registering a pre-trigger</span></span>
<span data-ttu-id="c6dde-347">트리거 등록은 HTTP POST를 통해 컬렉션에 새 트리거 리소스를 만들어 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-347">Registration of a trigger is done by creating a new trigger resource on a collection via HTTP POST.</span></span> <span data-ttu-id="c6dde-348">트리거가 사전 트리거인지 아니면 사후 트리거인지를 지정하고 연결될 수 있는 작업 유형(예: 만들기, 바꾸기, 삭제 또는 모두)을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-348">You can specify if the trigger is a pre or a post trigger and the type of operation it can be associated with (e.g. Create, Replace, Delete, or All).</span></span>   

    var preTrigger = {
        id: "upperCaseId",
        body: function() {
                var item = getContext().getRequest().getBody();
                item.id = item.id.toUpperCase();
                getContext().getRequest().setBody(item);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.All
    }

    client.createTriggerAsync(collection._self, preTrigger)
        .then(function (createdPreTrigger) {
            console.log("Successfully created trigger");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-pre-trigger"></a><span data-ttu-id="c6dde-349">사전 트리거 실행</span><span class="sxs-lookup"><span data-stu-id="c6dde-349">Executing a pre-trigger</span></span>
<span data-ttu-id="c6dde-350">트리거 실행은 요청 헤더를 통해 문서 리소스의 POST/PUT/DELETE 요청을 실행할 때 기존 트리거의 이름을 지정하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-350">Execution of a trigger is done by specifying the name of an existing trigger at the time of issuing the POST/PUT/DELETE request of a document resource via the request header.</span></span>  

    client.createDocumentAsync(collection._self, { id: "doc1", key: "Love in the Time of Cholera" }, { preTriggerInclude: "upperCaseId" })
        .then(function(createdDocument) {
            assert.equal(createdDocument.resource.id, "DOC1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-pre-trigger"></a><span data-ttu-id="c6dde-351">사전 트리거 등록 취소</span><span class="sxs-lookup"><span data-stu-id="c6dde-351">Unregistering a pre-trigger</span></span>
<span data-ttu-id="c6dde-352">트리거 등록 취소는 단순히 기존 트리거 리소스에 대해 HTTP DELETE를 실행하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-352">Unregistering a trigger is simply done via issuing an HTTP DELETE against an existing trigger resource.</span></span>  

    client.deleteTriggerAsync(createdPreTrigger._self);
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

### <a name="registering-a-udf"></a><span data-ttu-id="c6dde-353">UDF 등록</span><span class="sxs-lookup"><span data-stu-id="c6dde-353">Registering a UDF</span></span>
<span data-ttu-id="c6dde-354">UDF 등록은 HTTP POST를 통해 컬렉션에 새 UDF 리소스를 만들어 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-354">Registration of a UDF is done by creating a new UDF resource on a collection via HTTP POST.</span></span>  

    var udf = { 
        id: "mathSqrt",
        body: function(number) {
                return Math.sqrt(number);
        },
    };
    client.createUserDefinedFunctionAsync(collection._self, udf)
        .then(function (createdUdf) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-udf-as-part-of-the-query"></a><span data-ttu-id="c6dde-355">쿼리의 일부로 UDF 실행</span><span class="sxs-lookup"><span data-stu-id="c6dde-355">Executing a UDF as part of the query</span></span>
<span data-ttu-id="c6dde-356">UDF는 SQL 쿼리의 일부로 지정될 수 있으며, [DocumentDB API의 핵심 SQL 쿼리 언어](https://msdn.microsoft.com/library/azure/dn782250.aspx)를 확장하는 방법으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-356">A UDF can be specified as part of the SQL query and is used as a way to extend the core [SQL query language for the DocumentDB API](https://msdn.microsoft.com/library/azure/dn782250.aspx).</span></span>

    var filterQuery = "SELECT udf.mathSqrt(r.Age) AS sqrtAge FROM root r WHERE r.FirstName='John'";
    client.queryDocuments(collection._self, filterQuery).toArrayAsync();
        .then(function(queryResponse) {
            var queryResponseDocuments = queryResponse.feed;
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-udf"></a><span data-ttu-id="c6dde-357">UDF 등록 취소</span><span class="sxs-lookup"><span data-stu-id="c6dde-357">Unregistering a UDF</span></span>
<span data-ttu-id="c6dde-358">UDF 등록 취소는 단순히 기존 UDF 리소스에 대해 HTTP DELETE를 실행하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-358">Unregistering a UDF is simply done by issuing an HTTP DELETE against an existing UDF resource.</span></span>  

    client.deleteUserDefinedFunctionAsync(createdUdf._self)
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

<span data-ttu-id="c6dde-359">위 조각에서는 [JavaScript SDK](https://github.com/Azure/azure-documentdb-js)를 통한 등록(POST), 등록 취소(PUT), 읽기/나열(GET) 및 실행(POST)을 보여 주었지만 [REST API](/rest/api/documentdb/) 또는 다른 [클라이언트 SDK](documentdb-sdk-dotnet.md)를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-359">Although the snippets above showed the registration (POST), unregistration (PUT), read/list (GET) and execution (POST) via the [JavaScript SDK](https://github.com/Azure/azure-documentdb-js), you can also use the [REST APIs](/rest/api/documentdb/) or other [client SDKs](documentdb-sdk-dotnet.md).</span></span> 

## <a name="documents"></a><span data-ttu-id="c6dde-360">문서</span><span class="sxs-lookup"><span data-stu-id="c6dde-360">Documents</span></span>
<span data-ttu-id="c6dde-361">컬렉션의 임의 JSON 문서를 삽입하고, 바꾸고, 삭제하고, 읽고, 열거하고, 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-361">You can insert, replace, delete, read, enumerate and query arbitrary JSON documents in a collection.</span></span> <span data-ttu-id="c6dde-362">Cosmos DB는 스키마를 위임하지 않으며 컬렉션 내 문서 쿼리를 지원하기 위해 보조 인덱스가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-362">Cosmos DB does not mandate any schema and does not require secondary indexes in order to support querying over documents in a collection.</span></span> <span data-ttu-id="c6dde-363">문서의 최대 크기는 2MB입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-363">The maximum size for a document is 2 MB.</span></span>   

<span data-ttu-id="c6dde-364">진정한 개방형 데이터베이스 서비스인 Cosmos DB는 특수화된 데이터 형식(예: 날짜/시간) 또는 JSON 문서에 대한 특정 인코딩을 고안하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-364">Being a truly open database service, Cosmos DB does not invent any specialized data types (e.g. date time) or specific encodings for JSON documents.</span></span> <span data-ttu-id="c6dde-365">Cosmos DB는 다양한 문서 간의 관계를 분류하기 위한 특별한 JSON 규칙이 필요 없습니다. Cosmos DB의 SQL 구문에서 특별한 주석 없이 문서를 쿼리 및 프로젝션하는 강력한 계층적 관계형 쿼리 연산자를 제공하거나 고유 속성을 사용하여 문서 간의 관계를 분류해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-365">Note that Cosmos DB does not require any special JSON conventions to codify the relationships among various documents; the SQL syntax of Cosmos DB provides very powerful hierarchical and relational query operators to query and project documents without any special annotations or need to codify relationships among documents using distinguished properties.</span></span>  

<span data-ttu-id="c6dde-366">다른 모든 리소스와 마찬가지로, REST API 또는 [클라이언트 SDK](documentdb-sdk-dotnet.md)를 사용하여 문서를 쉽게 만들고, 바꾸고, 삭제하고, 읽고, 열거하고, 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-366">As with all other resources, documents can be created, replaced, deleted, read, enumerated and queried easily using either REST APIs or any of the [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="c6dde-367">문서를 삭제하면 중첩된 모든 첨부 파일에 해당하는 할당량이 즉시 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-367">Deleting a document instantly frees up the quota corresponding to all of the nested attachments.</span></span> <span data-ttu-id="c6dde-368">문서의 읽기 일관성 수준은 데이터베이스 계정의 일관성 정책을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-368">The read consistency level of documents follows the consistency policy on the database account.</span></span> <span data-ttu-id="c6dde-369">응용 프로그램의 데이터 일관성 요구 사항에 따라 요청 단위로 이 정책을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-369">This policy can be overridden on a per-request basis depending on data consistency requirements of your application.</span></span> <span data-ttu-id="c6dde-370">문서를 쿼리할 때 읽기 일관성은 컬렉션에 설정된 인덱싱 모드를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-370">When querying documents, the read consistency follows the indexing mode set on the collection.</span></span> <span data-ttu-id="c6dde-371">"일관성"의 경우 계정의 일관성 정책을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-371">For “consistent”, this follows the account’s consistency policy.</span></span> 

## <a name="attachments-and-media"></a><span data-ttu-id="c6dde-372">첨부 파일 및 미디어</span><span class="sxs-lookup"><span data-stu-id="c6dde-372">Attachments and media</span></span>
<span data-ttu-id="c6dde-373">Cosmos DB를 사용하면 Cosmos DB(계정당 최대 2GB) 또는 원격 미디어 저장소에 이진 Blob/미디어를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-373">Cosmos DB allows you to store binary blobs/media either with Cosmos DB (maximum of 2 GB per account) or to your own remote media store.</span></span> <span data-ttu-id="c6dde-374">또한 첨부 파일이라는 특수 문서 측면에서 미디어의 메타데이터를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-374">It also allows you to represent the metadata of a media in terms of a special document called attachment.</span></span> <span data-ttu-id="c6dde-375">Cosmos DB의 첨부 파일은 다른 곳에 저장된 미디어/blob을 참조하는 특수(JSON) 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-375">An attachment in Cosmos DB is a special (JSON) document that references the media/blob stored elsewhere.</span></span> <span data-ttu-id="c6dde-376">첨부 파일은 단순히 원격 미디어 저장소에 저장된 미디어의 메타데이터(예: 위치, 작성자 등)를 캡처하는 특수 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-376">An attachment is simply a special document that captures the metadata (e.g. location, author etc.) of a media stored in a remote media storage.</span></span> 

<span data-ttu-id="c6dde-377">Cosmos DB를 사용하여 잉크 주석과 설명, 강조, 책갈피, 등급, 좋아요/싫어요 등 지정된 사용자의 전자책에 대해 연결된 메타데이터를 저장하는 특수 읽기 응용 프로그램을 고려해 보세요.</span><span class="sxs-lookup"><span data-stu-id="c6dde-377">Consider a social reading application which uses Cosmos DB to store ink annotations, and metadata including comments, highlights, bookmarks, ratings, likes/dislikes etc. associated for an e-book of a given user.</span></span>   

* <span data-ttu-id="c6dde-378">책 자체의 내용은 Cosmos DB 데이터베이스 계정의 일부로 사용 가능한 미디어 저장소나 원격 미디어 저장소에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-378">The content of the book itself is stored in the media storage either available as part of Cosmos DB database account or a remote media store.</span></span> 
* <span data-ttu-id="c6dde-379">응용 프로그램은 각 사용자의 메타데이터를 개별 문서로 저장할 수 있습니다. 예를 들어 book1에 대한 Joe의 메타데이터는 /colls/joe/docs/book1로 참조된 문서에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-379">An application may store each user’s metadata as a distinct document -- e.g. Joe’s metadata for book1 is stored in a document referenced by /colls/joe/docs/book1.</span></span> 
* <span data-ttu-id="c6dde-380">지정된 사용자 책의 콘텐츠 페이지를 가리키는 첨부 파일은 해당 문서 아래에 저장됩니다(예: /colls/joe/docs/book1/chapter1, /colls/joe/docs/book1/chapter2 등).</span><span class="sxs-lookup"><span data-stu-id="c6dde-380">Attachments pointing to the content pages of a given book of a user are stored under the corresponding document e.g. /colls/joe/docs/book1/chapter1, /colls/joe/docs/book1/chapter2 etc.</span></span> 

<span data-ttu-id="c6dde-381">위에 나열된 예제에서는 ID를 사용하여 리소스 계층 구조를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-381">Note that the examples listed above use friendly ids to convey the resource hierarchy.</span></span> <span data-ttu-id="c6dde-382">고유한 리소스 ID를 사용하여 REST API를 통해 리소스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-382">Resources are accessed via the REST APIs through unique resource ids.</span></span> 

<span data-ttu-id="c6dde-383">Cosmos DB에서 관리되는 미디어의 경우 첨부 파일의 _media 속성이 해당 URI로 미디어를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-383">For the media that is managed by Cosmos DB, the _media property of the attachment will reference the media by its URI.</span></span> <span data-ttu-id="c6dde-384">Cosmos DB는 처리 중인 참조가 모두 삭제되면 미디어를 가비지 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-384">Cosmos DB will ensure to garbage collect the media when all of the outstanding references are dropped.</span></span> <span data-ttu-id="c6dde-385">새 미디어를 업로드하면 Cosmos DB에서 자동으로 첨부 파일을 생성하고 새로 추가한 미디어를 가리키도록 _media를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-385">Cosmos DB automatically generates the attachment when you upload the new media and populates the _media to point to the newly added media.</span></span> <span data-ttu-id="c6dde-386">직접 관리하는 원격 blob 저장소(예: OneDrive, Azure Storage, DropBox 등)에 미디어를 저장하는 경우에도 첨부 파일을 사용하여 미디어를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-386">If you choose to store the media in a remote blob store managed by you (e.g. OneDrive, Azure Storage, DropBox etc), you can still use attachments to reference the media.</span></span> <span data-ttu-id="c6dde-387">이 경우 직접 첨부 파일을 만들고 해당 _media 속성을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-387">In this case, you will create the attachment yourself and populate its _media property.</span></span>   

<span data-ttu-id="c6dde-388">다른 모든 리소스와 마찬가지로, REST API 또는 클라이언트 SDK를 사용하여 첨부 파일을 쉽게 만들거나, 바꾸거나, 삭제하거나, 읽거나, 열거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-388">As with all other resources, attachments can be created, replaced, deleted, read or enumerated easily using either REST APIs or any of the client SDKs.</span></span> <span data-ttu-id="c6dde-389">문서와 마찬가지로, 첨부 파일의 읽기 일관성 수준은 데이터베이스 계정의 일관성 정책을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-389">As with documents, the read consistency level of attachments follows the consistency policy on the database account.</span></span> <span data-ttu-id="c6dde-390">응용 프로그램의 데이터 일관성 요구 사항에 따라 요청 단위로 이 정책을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-390">This policy can be overridden on a per-request basis depending on data consistency requirements of your application.</span></span> <span data-ttu-id="c6dde-391">첨부 파일을 쿼리할 때 읽기 일관성은 컬렉션에 설정된 인덱싱 모드를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-391">When querying for attachments, the read consistency follows the indexing mode set on the collection.</span></span> <span data-ttu-id="c6dde-392">"일관성"의 경우 계정의 일관성 정책을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-392">For “consistent”, this follows the account’s consistency policy.</span></span> 
 

## <a name="users"></a><span data-ttu-id="c6dde-393">사용자</span><span class="sxs-lookup"><span data-stu-id="c6dde-393">Users</span></span>
<span data-ttu-id="c6dde-394">Cosmos DB 사용자는 사용 권한 그룹화를 위한 논리적 네임스페이스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-394">A Cosmos DB user represents a logical namespace for grouping permissions.</span></span> <span data-ttu-id="c6dde-395">Cosmos DB 사용자는 ID 관리 시스템이나 미리 정의된 응용 프로그램 역할의 사용자에 해당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-395">A Cosmos DB user may correspond to a user in an identity management system or a predefined application role.</span></span> <span data-ttu-id="c6dde-396">Cosmos DB에서 사용자는 단순히 데이터베이스 아래의 사용 권한 집합을 그룹화하는 추상화를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-396">For Cosmos DB, a user simply represents an abstraction to group a set of permissions under a database.</span></span>   

<span data-ttu-id="c6dde-397">응용 프로그램에 대해 다중 테넌트 지원을 구현하기 위해 실제 사용자 또는 응용 프로그램 테넌트에 해당하는 사용자를 Cosmos DB에 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-397">For implementing multi-tenancy in your application, you can create users in Cosmos DB which corresponds to your actual users or the tenants of your application.</span></span> <span data-ttu-id="c6dde-398">그런 다음 지정된 사용자에 대해 다양한 컬렉션, 문서, 첨부 파일 등의 액세스 제어에 해당하는 사용 권한을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-398">You can then create permissions for a given user that correspond to the access control over various collections, documents, attachments, etc.</span></span>   

<span data-ttu-id="c6dde-399">사용자 증가와 더불어 응용 프로그램이 확장되어야 하므로 데이터를 분할하는 다양한 방법을 채택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-399">As your applications need to scale with your user growth, you can adopt various ways to shard your data.</span></span> <span data-ttu-id="c6dde-400">각 사용자를 다음과 같이 모델링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-400">You can model each of your users as follows:</span></span>   

* <span data-ttu-id="c6dde-401">각 사용자가 데이터베이스에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-401">Each user maps to a database.</span></span>
* <span data-ttu-id="c6dde-402">각 사용자가 컬렉션에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-402">Each user maps to a collection.</span></span> 
* <span data-ttu-id="c6dde-403">여러 사용자에 해당하는 문서가 전용 컬렉션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-403">Documents corresponding to multiple users go to a dedicated collection.</span></span> 
* <span data-ttu-id="c6dde-404">여러 사용자에 해당하는 문서가 컬렉션 집합으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-404">Documents corresponding to multiple users go to a set of collections.</span></span>   

<span data-ttu-id="c6dde-405">선택한 특정 분할 전략에 관계없이 실제 사용자를 Cosmos DB 데이터베이스의 사용자로 모델링하고 세분화된 사용 권한을 각 사용자에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-405">Regardless of the specific sharding strategy you choose, you can model your actual users as users in Cosmos DB database and associate fine grained permissions to each user.</span></span>  

<span data-ttu-id="c6dde-406">![사용자 컬렉션][3]</span><span class="sxs-lookup"><span data-stu-id="c6dde-406">![User collections][3]</span></span>  
<span data-ttu-id="c6dde-407">**분할 전략 및 사용자 모델링**</span><span class="sxs-lookup"><span data-stu-id="c6dde-407">**Sharding strategies and modeling users**</span></span>

<span data-ttu-id="c6dde-408">다른 모든 리소스와 마찬가지로, REST API 또는 클라이언트 SDK를 사용하여 Cosmos DB의 사용자를 쉽게 만들거나, 바꾸거나, 삭제하거나, 읽거나, 열거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-408">Like all other resources, users in Cosmos DB can be created, replaced, deleted, read or enumerated easily using either REST APIs or any of the client SDKs.</span></span> <span data-ttu-id="c6dde-409">Cosmos DB는 사용자 리소스의 메타데이터 읽기 또는 쿼리에 대해 항상 강력한 일관성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-409">Cosmos DB always provides strong consistency for reading or querying the metadata of a user resource.</span></span> <span data-ttu-id="c6dde-410">사용자를 삭제하면 자동으로 사용자 내에 포함된 사용 권한에 액세스할 수 없게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-410">It is worth pointing out that deleting a user automatically ensures that you cannot access any of the permissions contained within it.</span></span> <span data-ttu-id="c6dde-411">Cosmos DB는 삭제된 사용자의 일부인 사용 권한 할당량을 백그라운드에서 회수하지만 삭제된 사용 권한을 즉시 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-411">Even though the Cosmos DB reclaims the quota of the permissions as part of the deleted user in the background, the deleted permissions is available instantly again for you to use.</span></span>  

## <a name="permissions"></a><span data-ttu-id="c6dde-412">권한</span><span class="sxs-lookup"><span data-stu-id="c6dde-412">Permissions</span></span>
<span data-ttu-id="c6dde-413">액세스 제어 관점에서 데이터베이스 계정, 데이터베이스, 사용자, 사용 권한 등의 리소스는 관리 권한이 필요하기 때문에 *관리* 리소스로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-413">From an access control perspective, resources such as database accounts, databases, users and permission are considered *administrative* resources since these require administrative permissions.</span></span> <span data-ttu-id="c6dde-414">반면, 컬렉션, 문서, 첨부 파일, 저장 프로시저, 트리거 및 UDF를 비롯한 리소스는 지정된 데이터베이스 아래로 범위가 지정되며 *응용 프로그램 리소스*로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-414">On the other hand, resources including the collections, documents, attachments, stored procedures, triggers, and UDFs are scoped under a given database and considered *application resources*.</span></span> <span data-ttu-id="c6dde-415">이를 액세스하는 두 가지 유형의 리소스 및 역할(즉, 관리자 및 사용자)에 따라 권한 부여 모델은 두 가지 유형의 *액세스 키*인 *마스터 키*와 *리소스 키*를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-415">Corresponding to the two types of resources and the roles that access them (namely the administrator and user), the authorization model defines two types of *access keys*: *master key* and *resource key*.</span></span> <span data-ttu-id="c6dde-416">마스터 키는 데이터베이스 계정의 일부이며 데이터베이스 계정을 프로비전하는 개발자(또는 관리자)에게 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-416">The master key is a part of the database account and is provided to the developer (or administrator) who is provisioning the database account.</span></span> <span data-ttu-id="c6dde-417">이 마스터 키는 관리 리소스 및 응용 프로그램 리소스 둘 다에 대한 액세스 권한 부여에 사용될 수 있다는 점에서 관리자 의미 체계를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-417">This master key has administrator semantics, in that it can be used to authorize access to both administrative and application resources.</span></span> <span data-ttu-id="c6dde-418">반면, 리소스 키는 *특정* 응용 프로그램 리소스에 대한 액세스를 허용하는 세분화된 액세스 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-418">In contrast, a resource key is a granular access key that allows access to a *specific* application resource.</span></span> <span data-ttu-id="c6dde-419">따라서 데이터베이스 사용자와 특정 리소스(예: 컬렉션, 문서, 첨부 파일, 저장 프로시저, 트리거 또는 UDF)에 대한 이 사용자의 사용 권한 간 관계를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-419">Thus, it captures the relationship between the user of a database and the permissions the user has for a specific resource (e.g. collection, document, attachment, stored procedure, trigger, or UDF).</span></span>   

<span data-ttu-id="c6dde-420">리소스 키를 받으려면 지정된 사용자로 사용 권한 리소스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-420">The only way to obtain a resource key is by creating a permission resource under a given user.</span></span> <span data-ttu-id="c6dde-421">사용 권한을 만들거나 검색하려면 권한 부여 헤더에 마스터 키가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-421">Note that In order to create or retrieve a permission, a master key must be presented in the authorization header.</span></span> <span data-ttu-id="c6dde-422">사용 권한 리소스는 리소스, 해당 액세스 권한 및 사용자를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-422">A permission resource ties the resource, its access and the user.</span></span> <span data-ttu-id="c6dde-423">사용 권한 리소스를 만든 후에는 사용자가 관련 리소스에 액세스하기 위해 관련 리소스 키만 제공하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-423">After creating a permission resource, the user only needs to present the associated resource key in order to gain access to the relevant resource.</span></span> <span data-ttu-id="c6dde-424">따라서 리소스 키를 사용 권한 리소스의 단순한 논리적 표현으로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-424">Hence, a resource key can be viewed as a logical and compact representation of the permission resource.</span></span>  

<span data-ttu-id="c6dde-425">다른 모든 리소스와 마찬가지로, REST API 또는 클라이언트 SDK를 사용하여 Cosmos DB의 사용 권한을 쉽게 만들거나, 바꾸거나, 삭제하거나, 읽거나, 열거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-425">As with all other resources, permissions in Cosmos DB can be created, replaced, deleted, read or enumerated easily using either REST APIs or any of the client SDKs.</span></span> <span data-ttu-id="c6dde-426">Cosmos DB는 사용 권한의 메타데이터 읽기 또는 쿼리에 대해 항상 강력한 일관성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-426">Cosmos DB always provides strong consistency for reading or querying the metadata of a permission.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c6dde-427">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c6dde-427">Next steps</span></span>
<span data-ttu-id="c6dde-428">[Cosmos DB 리소스와의 RESTful 상호 작용](https://msdn.microsoft.com/library/azure/mt622086.aspx)에서 HTTP 명령을 사용하여 리소스를 사용하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c6dde-428">Learn more about working with resources by using HTTP commands in [RESTful interactions with Cosmos DB resources](https://msdn.microsoft.com/library/azure/mt622086.aspx).</span></span>

[1]: media/documentdb-resources/resources1.png
[2]: media/documentdb-resources/resources2.png
[3]: media/documentdb-resources/resources3.png

