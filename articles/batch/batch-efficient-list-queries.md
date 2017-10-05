---
title: "효율적인 목록 쿼리 디자인 - Azure Batch | Microsoft Docs"
description: "풀, 작업, 태스크 및 계산 노드와 같은 Batch 리소스에 대한 정보를 요청할 때 쿼리를 필터링하여 성능을 향상시킵니다."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 031fefeb-248e-4d5a-9bc2-f07e46ddd30d
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 08/02/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a80b207f591bd888d4749287527013c5e554fb6e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-queries-to-list-batch-resources-efficiently"></a><span data-ttu-id="27e64-103">쿼리를 만들어서 효율적으로 Batch 리소스 나열</span><span class="sxs-lookup"><span data-stu-id="27e64-103">Create queries to list Batch resources efficiently</span></span>

<span data-ttu-id="27e64-104">여기에서 [Batch .NET][api_net] 라이브러리를 사용하여 작업, 태스크 및 계산 노드를 쿼리할 때 서비스에서 반환되는 데이터의 양을 줄여 Azure Batch 응용 프로그램의 성능을 향상시키는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-104">Here you'll learn how to increase your Azure Batch application's performance by reducing the amount of data that is returned by the service when you query jobs, tasks, and compute nodes with the [Batch .NET][api_net] library.</span></span>

<span data-ttu-id="27e64-105">거의 모든 Batch 응용 프로그램은 정기적으로 Batch 서비스를 쿼리하는 특정 형식의 모니터링 또는 다른 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-105">Nearly all Batch applications need to perform some type of monitoring or other operation that queries the Batch service, often at regular intervals.</span></span> <span data-ttu-id="27e64-106">예를 들어 대기 중인 태스크가 작업에 남아 있는지 여부를 확인하려면 작업의 모든 태스크에 대한 데이터를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-106">For example, to determine whether there are any queued tasks remaining in a job, you must get data on every task in the job.</span></span> <span data-ttu-id="27e64-107">풀의 노드 상태를 확인하려면 풀의 모든 노드에서 데이터를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-107">To determine the status of nodes in your pool, you must get data on every node in the pool.</span></span> <span data-ttu-id="27e64-108">이 문서에서는 가장 효율적인 방법으로 이러한 쿼리를 실행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-108">This article explains how to execute such queries in the most efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="27e64-109">Batch 서비스는 작업 내 태스크를 계산하는 일반적인 시나리오에 대한 특별한 API 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-109">The Batch service provides special API support for the common scenario of counting tasks in a job.</span></span> <span data-ttu-id="27e64-110">목록 쿼리를 사용하는 대신, [Get Task Counts][rest_get_task_counts] 연산을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-110">Instead of using a list query for these, you can call the [Get Task Counts][rest_get_task_counts] operation.</span></span> <span data-ttu-id="27e64-111">Get Task Counts 연산은 보류 중, 실행 중 또는 완료 태스크 수, 성공 또는 실패한 태스크 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-111">Get Task Counts indicates how many tasks are pending, running or complete, and how many tasks have succeeded or failed.</span></span> <span data-ttu-id="27e64-112">Get Task Counts는 목록 쿼리보다 더 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-112">Get Task Counts is more efficient than a list query.</span></span> <span data-ttu-id="27e64-113">자세한 내용은 [상태별 작업 계수(미리 보기)](batch-get-task-counts.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27e64-113">For more information, see [Count tasks for a job by state (Preview)](batch-get-task-counts.md).</span></span> 
>
> <span data-ttu-id="27e64-114">2017-06-01.5.1 이전의 Batch 서비스 버전에서는 Get Task Counts 연산을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-114">The Get Task Counts operation is not available in Batch service versions earlier than 2017-06-01.5.1.</span></span> <span data-ttu-id="27e64-115">이전 버전의 서비스를 사용하는 경우, 대신 목록 쿼리를 사용하여 작업의 태스크를 계산하세요.</span><span class="sxs-lookup"><span data-stu-id="27e64-115">If you are using an older version of the service, then use a list query to count tasks in a job instead.</span></span>
>
> 

## <a name="meet-the-detaillevel"></a><span data-ttu-id="27e64-116">DetailLevel 충족</span><span class="sxs-lookup"><span data-stu-id="27e64-116">Meet the DetailLevel</span></span>
<span data-ttu-id="27e64-117">프로덕션 Batch 응용 프로그램에서 작업, 태스크 및 계산 노드 같은 엔터티가 수천 개 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-117">In a production Batch application, entities like jobs, tasks, and compute nodes can number in the thousands.</span></span> <span data-ttu-id="27e64-118">이러한 리소스에 대한 정보를 요청할 때는 잠재적으로 각 쿼리에서 대량의 데이터를 Batch 서비스에서 응용 프로그램으로 "아슬아슬하게 전달"해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-118">When you request information on these resources, a potentially large amount of data must "cross the wire" from the Batch service to your application on each query.</span></span> <span data-ttu-id="27e64-119">쿼리에서 반환하는 항목의 수와 정보의 형식을 제한하여 쿼리의 속도를 높이고, 그 결과로 응용 프로그램의 성능도 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-119">By limiting the number of items and type of information that is returned by a query, you can increase the speed of your queries, and therefore the performance of your application.</span></span>

<span data-ttu-id="27e64-120">이 [Batch .NET][api_net] API 코드 조각은 각 태스크의 속성 *모두*와 함께 작업과 관련된 *모든* 태스크를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-120">This [Batch .NET][api_net] API code snippet lists *every* task that is associated with a job, along with *all* of the properties of each task:</span></span>

```csharp
// Get a collection of all of the tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

<span data-ttu-id="27e64-121">그러나 쿼리에 "세부 수준"을 적용하여 훨씬 더 효율적인 목록 쿼리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-121">You can perform a much more efficient list query, however, by applying a "detail level" to your query.</span></span> <span data-ttu-id="27e64-122">[JobOperations.ListTasks][net_list_tasks] 메서드에 [ODATADetailLevel][odata] 개체를 제공하여 이를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-122">You do this by supplying an [ODATADetailLevel][odata] object to the [JobOperations.ListTasks][net_list_tasks] method.</span></span> <span data-ttu-id="27e64-123">이 코드 조각은 완료된 태스크의 ID, 명령줄 및 계산 노드 정보 속성만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-123">This snippet returns only the ID, command line, and compute node information properties of completed tasks:</span></span>

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties to return
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply the ODATADetailLevel to the ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

<span data-ttu-id="27e64-124">이 예제 시나리오에서 수천 개의 태스크가 작업에 있다면 두 번째 쿼리의 결과는 대개 첫 번째 결과보다 더 빨리 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-124">In this example scenario, if there are thousands of tasks in the job, the results from the second query will typically be returned much quicker than the first.</span></span> <span data-ttu-id="27e64-125">Batch .NET API를 사용하여 항목을 나열할 때 ODATADetailLevel 사용에 대한 자세한 내용은 [아래](#efficient-querying-in-batch-net)에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-125">More information about using ODATADetailLevel when you list items with the Batch .NET API is included [below](#efficient-querying-in-batch-net).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="27e64-126">응용 프로그램의 최고 효율성과 성능을 위해 *항상* .NET API 목록 호출에 ODATADetailLevel 개체를 제공하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-126">We highly recommend that you *always* supply an ODATADetailLevel object to your .NET API list calls to ensure maximum efficiency and performance of your application.</span></span> <span data-ttu-id="27e64-127">세부 정보 수준을 지정하여 Batch 서비스 응답 시간을 낮추고, 네트워크 사용률을 개선하며 클라이언트 응용 프로그램의 메모리 사용을 최소화하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-127">By specifying a detail level, you can help to lower Batch service response times, improve network utilization, and minimize memory usage by client applications.</span></span>
> 
> 

## <a name="filter-select-and-expand"></a><span data-ttu-id="27e64-128">Filter, select 및 expand</span><span class="sxs-lookup"><span data-stu-id="27e64-128">Filter, select, and expand</span></span>
<span data-ttu-id="27e64-129">[Batch .NET][api_net] 및 [Batch REST][api_rest] API는 목록에 반환되는 항목 수와 각각에 대해 반환되는 정보의 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-129">The [Batch .NET][api_net] and [Batch REST][api_rest] APIs provide the ability to reduce both the number of items that are returned in a list, as well as the amount of information that is returned for each.</span></span> <span data-ttu-id="27e64-130">이렇게 하려면 목록 쿼리를 수행할 때 **filter**, **select** 및 **expand 문자열**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-130">You do so by specifying **filter**, **select**, and **expand strings** when performing list queries.</span></span>

### <a name="filter"></a><span data-ttu-id="27e64-131">Filter</span><span class="sxs-lookup"><span data-stu-id="27e64-131">Filter</span></span>
<span data-ttu-id="27e64-132">filter 문자열은 반환되는 항목 수를 줄이는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-132">The filter string is an expression that reduces the number of items that are returned.</span></span> <span data-ttu-id="27e64-133">예를 들어, 한 작업에 대해 실행 중인 태스크만 나열하거나 태스크를 실행할 준비가 된 계산 노드만 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-133">For example, list only the running tasks for a job, or list only compute nodes that are ready to run tasks.</span></span>

* <span data-ttu-id="27e64-134">filter 문자열은 하나 이상의 식으로 구성된 문자열로 구성됩니다. 식은 속성 이름, 연산자, 값으로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-134">The filter string consists of one or more expressions, with an expression that consists of a property name, operator, and value.</span></span> <span data-ttu-id="27e64-135">각 속성에 대해 지원되는 연산자의 경우처럼 지정할 수 있는 속성은 쿼리한 항목 마다 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-135">The properties that can be specified are specific to each entity type that you query, as are the operators that are supported for each property.</span></span>
* <span data-ttu-id="27e64-136">`and` 및 `or` 논리 연산자를 사용하면 여러 식을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-136">Multiple expressions can be combined by using the logical operators `and` and `or`.</span></span>
* <span data-ttu-id="27e64-137">`(state eq 'running') and startswith(id, 'renderTask')` filter 문자열 예제는 실행 중인 "렌더링" 태스크만 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-137">This example filter string lists only the running "render" tasks: `(state eq 'running') and startswith(id, 'renderTask')`.</span></span>

### <a name="select"></a><span data-ttu-id="27e64-138">여기서</span><span class="sxs-lookup"><span data-stu-id="27e64-138">Select</span></span>
<span data-ttu-id="27e64-139">select 문자열은 각 항목에 대해 반환되는 속성 값을 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-139">The select string limits the property values that are returned for each item.</span></span> <span data-ttu-id="27e64-140">속성 이름의 목록을 지정하고 해당 속성 값은 쿼리 결과의 항목에 대해 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-140">You specify a list of property names, and only those property values are returned for the items in the query results.</span></span>

* <span data-ttu-id="27e64-141">select 문자열은 속성 이름을 쉼표로 구분한 목록으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-141">The select string consists of a comma-separated list of property names.</span></span> <span data-ttu-id="27e64-142">쿼리 중인 엔터티 형식에 대한 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-142">You can specify any of the properties for the entity type you are querying.</span></span>
* <span data-ttu-id="27e64-143">`id, state, stateTransitionTime` select 문자열 예제는 각 태스크에 대해 반환되어야 하는 세 가지 속성 값만 지정하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-143">This example select string specifies that only three property values should be returned for each task: `id, state, stateTransitionTime`.</span></span>

### <a name="expand"></a><span data-ttu-id="27e64-144">Expand</span><span class="sxs-lookup"><span data-stu-id="27e64-144">Expand</span></span>
<span data-ttu-id="27e64-145">expand 문자열은 특정 정보를 얻는 데 필요한 API 호출 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-145">The expand string reduces the number of API calls that are required to obtain certain information.</span></span> <span data-ttu-id="27e64-146">expand 문자열을 사용하면 단일 API 호출로 각 항목에 대한 자세한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-146">When you use an expand string, more information about each item can be obtained with a single API call.</span></span> <span data-ttu-id="27e64-147">엔터티의 목록을 첫 번째로 가져오기 보다 목록에서 각 항목에 대한 정보를 요청하여 단일 API 호출에서 동일한 정보를 얻기 위해 확장 문자열을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-147">Rather than first obtaining the list of entities, then requesting information for each item in the list, you use an expand string to obtain the same information in a single API call.</span></span> <span data-ttu-id="27e64-148">API 호출이 적어지면 성능이 향상되었음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-148">Less API calls means better performance.</span></span>

* <span data-ttu-id="27e64-149">select 문자열과 마찬가지로 expand 문자열은 목록 쿼리 결과에서 특정 데이터의 포함 여부를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-149">Similar to the select string, the expand string controls whether certain data is included in list query results.</span></span>
* <span data-ttu-id="27e64-150">expand 문자열은 작업 목록, 작업 일정, 태스크 및 풀에서 사용되는 경우에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-150">The expand string is only supported when it is used in listing jobs, job schedules, tasks, and pools.</span></span> <span data-ttu-id="27e64-151">현재 통계 정보만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-151">Currently, it only supports statistics information.</span></span>
* <span data-ttu-id="27e64-152">모든 속성이 필요하며 select 문자열을 지정하지 않은 경우, 통계 정보를 가져오려면 expand 문자열을 사용 *해야 합니다* .</span><span class="sxs-lookup"><span data-stu-id="27e64-152">When all properties are required and no select string is specified, the expand string *must* be used to get statistics information.</span></span> <span data-ttu-id="27e64-153">select 문자열을 사용하여 속성 하위 집합을 가져올 경우 select 문자열에서 `stats` 를 지정할 수 있으며 expand 문자열을 지정하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-153">If a select string is used to obtain a subset of properties, then `stats` can be specified in the select string, and the expand string does not need to be specified.</span></span>
* <span data-ttu-id="27e64-154">`stats` expand 문자열 예제는 목록에서 각 항목에 대해 반환되어야 하는 통계 정보를 지정하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-154">This example expand string specifies that statistics information should be returned for each item in the list: `stats`.</span></span>

> [!NOTE]
> <span data-ttu-id="27e64-155">세 가지 쿼리 문자열 형식(filter, select 및 expand) 중 하나를 구성할 때 속성 이름 및 사례가 해당 REST API 요소와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-155">When constructing any of the three query string types (filter, select, and expand), you must ensure that the property names and case match that of their REST API element counterparts.</span></span> <span data-ttu-id="27e64-156">예를 들어 .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) 클래스를 사용하는 경우 .NET 속성이 [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state)이더라도 **State** 대신 **state**를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-156">For example, when working with the .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) class, you must specify **state** instead of **State**, even though the .NET property is [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span></span> <span data-ttu-id="27e64-157">.NET 및 REST API 간의 속성 매핑은 아래 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27e64-157">See the tables below for property mappings between the .NET and REST APIs.</span></span>
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a><span data-ttu-id="27e64-158">filter, select, expand 문자열 규칙</span><span class="sxs-lookup"><span data-stu-id="27e64-158">Rules for filter, select, and expand strings</span></span>
* <span data-ttu-id="27e64-159">[Batch .NET][api_net] 또는 다른 Batch SDK 중 하나를 사용하는 경우에도 filter, select, expand 문자열의 속성 이름은 [Batch REST][api_rest] API에서와 동일하게 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-159">Properties names in filter, select, and expand strings should appear as they do in the [Batch REST][api_rest] API--even when you use [Batch .NET][api_net] or one of the other Batch SDKs.</span></span>
* <span data-ttu-id="27e64-160">모든 속성 이름은 대/소문자를 구분하지만, 속성 값은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-160">All property names are case-sensitive, but property values are case insensitive.</span></span>
* <span data-ttu-id="27e64-161">날짜/시간 문자열은 두 형식 중 하나가 될 수 있으며 `DateTime`으로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-161">Date/time strings can be one of two formats, and must be preceded with `DateTime`.</span></span>
  
  * <span data-ttu-id="27e64-162">W3C-DTF 형식 예제: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span><span class="sxs-lookup"><span data-stu-id="27e64-162">W3C-DTF format example: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span></span>
  * <span data-ttu-id="27e64-163">RFC 1123 형식 예제: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span><span class="sxs-lookup"><span data-stu-id="27e64-163">RFC 1123 format example: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span></span>
* <span data-ttu-id="27e64-164">부울 문자열은 `true` 또는 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-164">Boolean strings are either `true` or `false`.</span></span>
* <span data-ttu-id="27e64-165">잘못된 속성이나 연산자를 지정한 경우 `400 (Bad Request)` 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-165">If an invalid property or operator is specified, a `400 (Bad Request)` error will result.</span></span>

## <a name="efficient-querying-in-batch-net"></a><span data-ttu-id="27e64-166">Batch .NET에서 효율적인 쿼리</span><span class="sxs-lookup"><span data-stu-id="27e64-166">Efficient querying in Batch .NET</span></span>
<span data-ttu-id="27e64-167">[Batch .NET][api_net] API 안에서 [ODATADetailLevel][odata] 클래스를 filter, select 및 expand 문자열에 사용하여 작업을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-167">Within the [Batch .NET][api_net] API, the [ODATADetailLevel][odata] class is used for supplying filter, select, and expand strings to list operations.</span></span> <span data-ttu-id="27e64-168">ODataDetailLevel 클래스에는 생성자 내에 지정되어 있거나 개체에 직접 설정된 세 개의 공용 문자열 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-168">The ODataDetailLevel class has three public string properties that can be specified in the constructor, or set directly on the object.</span></span> <span data-ttu-id="27e64-169">ODataDetailLevel 개체를 [ListPools][net_list_pools], [ListJobs][net_list_jobs] 및 [ListTasks][net_list_tasks]와 같은 다양한 목록 작업에 매개 변수로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-169">You then pass the ODataDetailLevel object as a parameter to the various list operations such as [ListPools][net_list_pools], [ListJobs][net_list_jobs], and [ListTasks][net_list_tasks].</span></span>

* <span data-ttu-id="27e64-170">[ODATADetailLevel][odata].[FilterClause][odata_filter]: 반환되는 항목 수를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-170">[ODATADetailLevel][odata].[FilterClause][odata_filter]: Limit the number of items that are returned.</span></span>
* <span data-ttu-id="27e64-171">[ODATADetailLevel][odata].[SelectClause][odata_select]: 각 항목에 반환되는 속성 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-171">[ODATADetailLevel][odata].[SelectClause][odata_select]: Specify which property values are returned with each item.</span></span>
* <span data-ttu-id="27e64-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: 각 항목에 대한 별도 호출 대신 단일 API 호출의 모든 항목에 대한 데이터를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: Retrieve data for all items in a single API call instead of separate calls for each item.</span></span>

<span data-ttu-id="27e64-173">다음 코드 조각에서는 풀의 특정 집합에 대한 통계에 대해 Batch 서비스를 효율적으로 쿼리하기 위해 Batch .NET API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-173">The following code snippet uses the Batch .NET API to efficiently query the Batch service for the statistics of a specific set of pools.</span></span> <span data-ttu-id="27e64-174">이 시나리오에서 Batch 사용자는 테스트 및 프로덕션 풀을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-174">In this scenario, the Batch user has both test and production pools.</span></span> <span data-ttu-id="27e64-175">테스트 풀 ID는 "test"를 접두사로 사용하고 프로덕션 풀 ID는 "prod"를 접두사로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-175">The test pool IDs are prefixed with "test", and the production pool IDs are prefixed with "prod".</span></span> <span data-ttu-id="27e64-176">이 코드 조각에서 *myBatchClient* 는 다음과 같은 [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) 클래스의 인스턴스를 적절하게 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-176">In the snippet, *myBatchClient* is a properly initialized instance of the [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) class.</span></span>

```csharp
// First we need an ODATADetailLevel instance on which to set the filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want to pull only the "test" pools, so we limit the number of items returned
// by using a FilterClause and specifying that the pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// To further limit the data that crosses the wire, configure the SelectClause to
// limit the properties that are returned on each CloudPool object to only
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify the ExpandClause so that the .NET API pulls the statistics for the
// CloudPools in a single underlying REST API call. Note that we use the pool's
// REST API element name "stats" here as opposed to "Statistics" as it appears in
// the .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing the amount of data that is returned
// by specifying the detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> <span data-ttu-id="27e64-177">Select 및 Expand 절로 구성된 [ODATADetailLevel][odata]의 인스턴스는 반환되는 데이터의 양을 제한하기 위해 [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx)과 같은 적절한 Get 메서드에 전달할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-177">An instance of [ODATADetailLevel][odata] that is configured with Select and Expand clauses can also be passed to appropriate Get methods, such as [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), to limit the amount of data that is returned.</span></span>
> 
> 

## <a name="batch-rest-to-net-api-mappings"></a><span data-ttu-id="27e64-178">Batch REST를 .NET API에 매핑</span><span class="sxs-lookup"><span data-stu-id="27e64-178">Batch REST to .NET API mappings</span></span>
<span data-ttu-id="27e64-179">filter, select 및 expand 문자열의 속성 이름은 이름과 대소문자 모두 해당 REST API 항목을 반영 *해야 합니다* .</span><span class="sxs-lookup"><span data-stu-id="27e64-179">Property names in filter, select, and expand strings *must* reflect their REST API counterparts, both in name and case.</span></span> <span data-ttu-id="27e64-180">다음 표는 .NET과 REST API 간의 매핑을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-180">The tables below provide mappings between the .NET and REST API counterparts.</span></span>

### <a name="mappings-for-filter-strings"></a><span data-ttu-id="27e64-181">filter 문자열 매핑</span><span class="sxs-lookup"><span data-stu-id="27e64-181">Mappings for filter strings</span></span>
* <span data-ttu-id="27e64-182">**.NET 목록 메서드**: 이 열의 각 .NET API 메서드는 [ODATADetailLevel][odata] 개체를 매개 변수 형태로 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-182">**.NET list methods**: Each of the .NET API methods in this column accepts an [ODATADetailLevel][odata] object as a parameter.</span></span>
* <span data-ttu-id="27e64-183">**REST 목록 요청**: 이 열에 연결된 각 REST API 페이지에는 *filter* 문자열에서 허용되는 속성과 연산을 지정하는 테이블이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-183">**REST list requests**: Each REST API page linked to in this column contains a table that specifies the properties and operations that are allowed in *filter* strings.</span></span> <span data-ttu-id="27e64-184">[ODATADetailLevel.FilterClause][odata_filter] 문자열을 구성할 때 이 속성 이름과 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-184">You will use these property names and operations when you construct an [ODATADetailLevel.FilterClause][odata_filter] string.</span></span>

| <span data-ttu-id="27e64-185">.NET 목록 메서드</span><span class="sxs-lookup"><span data-stu-id="27e64-185">.NET list methods</span></span> | <span data-ttu-id="27e64-186">REST 목록 요청</span><span class="sxs-lookup"><span data-stu-id="27e64-186">REST list requests</span></span> |
| --- | --- |
| <span data-ttu-id="27e64-187">[CertificateOperations.ListCertificates][net_list_certs]</span><span class="sxs-lookup"><span data-stu-id="27e64-187">[CertificateOperations.ListCertificates][net_list_certs]</span></span> |<span data-ttu-id="27e64-188">[계정에 인증서 나열][rest_list_certs]</span><span class="sxs-lookup"><span data-stu-id="27e64-188">[List the certificates in an account][rest_list_certs]</span></span> |
| <span data-ttu-id="27e64-189">[CloudTask.ListNodeFiles][net_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="27e64-189">[CloudTask.ListNodeFiles][net_list_task_files]</span></span> |<span data-ttu-id="27e64-190">[태스크와 연관된 파일 나열][rest_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="27e64-190">[List the files associated with a task][rest_list_task_files]</span></span> |
| <span data-ttu-id="27e64-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="27e64-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span></span> |<span data-ttu-id="27e64-192">[작업 준비 및 작업에 대한 작업 릴리스 태스크의 상태 나열][rest_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="27e64-192">[List the status of the job preparation and job release tasks for a job][rest_list_jobprep_status]</span></span> |
| <span data-ttu-id="27e64-193">[JobOperations.ListJobs][net_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="27e64-193">[JobOperations.ListJobs][net_list_jobs]</span></span> |<span data-ttu-id="27e64-194">[계정에 작업 나열][rest_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="27e64-194">[List the jobs in an account][rest_list_jobs]</span></span> |
| <span data-ttu-id="27e64-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="27e64-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span></span> |<span data-ttu-id="27e64-196">[노드에 파일 나열][rest_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="27e64-196">[List the files on a node][rest_list_nodefiles]</span></span> |
| <span data-ttu-id="27e64-197">[JobOperations.ListTasks][net_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="27e64-197">[JobOperations.ListTasks][net_list_tasks]</span></span> |<span data-ttu-id="27e64-198">[작업과 연관된 태스크 나열][rest_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="27e64-198">[List the tasks associated with a job][rest_list_tasks]</span></span> |
| <span data-ttu-id="27e64-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="27e64-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span></span> |<span data-ttu-id="27e64-200">[계정에 작업 일정 나열][rest_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="27e64-200">[List the job schedules in an account][rest_list_job_schedules]</span></span> |
| <span data-ttu-id="27e64-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="27e64-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span></span> |<span data-ttu-id="27e64-202">[작업 일정과 연관된 작업 나열][rest_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="27e64-202">[List the jobs associated with a job schedule][rest_list_schedule_jobs]</span></span> |
| <span data-ttu-id="27e64-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="27e64-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span></span> |<span data-ttu-id="27e64-204">[풀에 계산 노드 나열][rest_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="27e64-204">[List the compute nodes in a pool][rest_list_compute_nodes]</span></span> |
| <span data-ttu-id="27e64-205">[PoolOperations.ListPools][net_list_pools]</span><span class="sxs-lookup"><span data-stu-id="27e64-205">[PoolOperations.ListPools][net_list_pools]</span></span> |<span data-ttu-id="27e64-206">[계정에 풀 나열][rest_list_pools]</span><span class="sxs-lookup"><span data-stu-id="27e64-206">[List the pools in an account][rest_list_pools]</span></span> |

### <a name="mappings-for-select-strings"></a><span data-ttu-id="27e64-207">select 문자열 매핑</span><span class="sxs-lookup"><span data-stu-id="27e64-207">Mappings for select strings</span></span>
* <span data-ttu-id="27e64-208">**Batch .NET 형식**: Batch .NET API 형식.</span><span class="sxs-lookup"><span data-stu-id="27e64-208">**Batch .NET types**: Batch .NET API types.</span></span>
* <span data-ttu-id="27e64-209">**REST API 엔터티**: 이 열의 각 페이지에는 형식에 대한 REST API 속성 이름을 나열하는 하나 이상의 표가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-209">**REST API entities**: Each page in this column contains one or more tables that list the REST API property names for the type.</span></span> <span data-ttu-id="27e64-210">이러한 속성 이름은 *select* 문자열을 구성할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-210">These property names are used when you construct *select* strings.</span></span> <span data-ttu-id="27e64-211">[ODATADetailLevel.SelectClause][odata_select] 문자열을 구성할 때 이와 동일한 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-211">You will use these same property names when you construct an [ODATADetailLevel.SelectClause][odata_select] string.</span></span>

| <span data-ttu-id="27e64-212">Batch .NET 형식</span><span class="sxs-lookup"><span data-stu-id="27e64-212">Batch .NET types</span></span> | <span data-ttu-id="27e64-213">REST API 엔터티</span><span class="sxs-lookup"><span data-stu-id="27e64-213">REST API entities</span></span> |
| --- | --- |
| <span data-ttu-id="27e64-214">[Certificate][net_cert]</span><span class="sxs-lookup"><span data-stu-id="27e64-214">[Certificate][net_cert]</span></span> |<span data-ttu-id="27e64-215">[인증서 정보 가져오기][rest_get_cert]</span><span class="sxs-lookup"><span data-stu-id="27e64-215">[Get information about a certificate][rest_get_cert]</span></span> |
| <span data-ttu-id="27e64-216">[CloudJob][net_job]</span><span class="sxs-lookup"><span data-stu-id="27e64-216">[CloudJob][net_job]</span></span> |<span data-ttu-id="27e64-217">[작업 정보 가져오기][rest_get_job]</span><span class="sxs-lookup"><span data-stu-id="27e64-217">[Get information about a job][rest_get_job]</span></span> |
| <span data-ttu-id="27e64-218">[CloudJobSchedule][net_schedule]</span><span class="sxs-lookup"><span data-stu-id="27e64-218">[CloudJobSchedule][net_schedule]</span></span> |<span data-ttu-id="27e64-219">[작업 일정 정보 가져오기][rest_get_schedule]</span><span class="sxs-lookup"><span data-stu-id="27e64-219">[Get information about a job schedule][rest_get_schedule]</span></span> |
| <span data-ttu-id="27e64-220">[ComputeNode][net_node]</span><span class="sxs-lookup"><span data-stu-id="27e64-220">[ComputeNode][net_node]</span></span> |<span data-ttu-id="27e64-221">[노드 정보 가져오기][rest_get_node]</span><span class="sxs-lookup"><span data-stu-id="27e64-221">[Get information about a node][rest_get_node]</span></span> |
| <span data-ttu-id="27e64-222">[CloudPool][net_pool]</span><span class="sxs-lookup"><span data-stu-id="27e64-222">[CloudPool][net_pool]</span></span> |<span data-ttu-id="27e64-223">[풀 정보 가져오기][rest_get_pool]</span><span class="sxs-lookup"><span data-stu-id="27e64-223">[Get information about a pool][rest_get_pool]</span></span> |
| <span data-ttu-id="27e64-224">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="27e64-224">[CloudTask][net_task]</span></span> |<span data-ttu-id="27e64-225">[태스크 정보 가져오기][rest_get_task]</span><span class="sxs-lookup"><span data-stu-id="27e64-225">[Get information about a task][rest_get_task]</span></span> |

## <a name="example-construct-a-filter-string"></a><span data-ttu-id="27e64-226">예: filter 문자열 구성</span><span class="sxs-lookup"><span data-stu-id="27e64-226">Example: construct a filter string</span></span>
<span data-ttu-id="27e64-227">[ODATADetailLevel.FilterClause][odata_filter]에 대한 filter 문자열을 구성할 때는 "filter 문자열에 대한 매핑"에서 위의 표를 참조하여 수행하려는 목록 작업에 해당하는 REST API 설명서 페이지를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-227">When you construct a filter string for [ODATADetailLevel.FilterClause][odata_filter], consult the table above under "Mappings for filter strings" to find the REST API documentation page that corresponds to the list operation that you wish to perform.</span></span> <span data-ttu-id="27e64-228">해당 페이지의 첫 번째 다중 행 표에 필터링 가능한 속성과 지원되는 연산자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-228">You will find the filterable properties and their supported operators in the first multirow table on that page.</span></span> <span data-ttu-id="27e64-229">예를 들어, 종료 코드가 0이 아닌 모든 태스크를 검색하려는 경우 [작업과 연결된 태스크 목록][rest_list_tasks]의 이 행은 적용 가능한 속성 문자열과 허용 가능한 연산자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-229">If you wish to retrieve all tasks whose exit code was nonzero, for example, this row on [List the tasks associated with a job][rest_list_tasks] specifies the applicable property string and allowable operators:</span></span>

| <span data-ttu-id="27e64-230">속성</span><span class="sxs-lookup"><span data-stu-id="27e64-230">Property</span></span> | <span data-ttu-id="27e64-231">허용되는 연산</span><span class="sxs-lookup"><span data-stu-id="27e64-231">Operations allowed</span></span> | <span data-ttu-id="27e64-232">형식</span><span class="sxs-lookup"><span data-stu-id="27e64-232">Type</span></span> |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

<span data-ttu-id="27e64-233">따라서 종료 코드가 0이 아닌 모든 작업을 나열하기 위한 filter 문자열은 다음과 같게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-233">Thus, the filter string for listing all tasks with a nonzero exit code would be:</span></span>

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a><span data-ttu-id="27e64-234">예: select 문자열 구성</span><span class="sxs-lookup"><span data-stu-id="27e64-234">Example: construct a select string</span></span>
<span data-ttu-id="27e64-235">[ODATADetailLevel.SelectClause][odata_select]를 구성하려면 "select 문자열에 대한 매핑"에서 위의 표를 참조하고 나열하는 엔터티 형식에 해당하는 REST API 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-235">To construct [ODATADetailLevel.SelectClause][odata_select], consult the table above under "Mappings for select strings" and navigate to the REST API page that corresponds to the type of entity that you are listing.</span></span> <span data-ttu-id="27e64-236">해당 페이지의 첫 번째 다중 행 표에 선택 가능한 속성과 지원되는 연산자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-236">You will find the selectable properties and their supported operators in the first multirow table on that page.</span></span> <span data-ttu-id="27e64-237">목록의 각 태스크에 대해 ID와 명령줄만 검색하려면 [태스크 관련 정보 가져오기][rest_get_task]의 해당하는 표에서 이 행을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-237">If you wish to retrieve only the ID and command line for each task in a list, for example, you will find these rows in the applicable table on [Get information about a task][rest_get_task]:</span></span>

| <span data-ttu-id="27e64-238">속성</span><span class="sxs-lookup"><span data-stu-id="27e64-238">Property</span></span> | <span data-ttu-id="27e64-239">형식</span><span class="sxs-lookup"><span data-stu-id="27e64-239">Type</span></span> | <span data-ttu-id="27e64-240">참고</span><span class="sxs-lookup"><span data-stu-id="27e64-240">Notes</span></span> |
|:--- |:--- |:--- |
| `id` |`String` |`The ID of the task.` |
| `commandLine` |`String` |`The command line of the task.` |

<span data-ttu-id="27e64-241">목록의 각 태스크와 함께 ID와 명령줄만 포함하기 위한 select 문자열은 다음과 같게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-241">The select string for including only the ID and command line with each listed task would then be:</span></span>

`id, commandLine`

## <a name="code-samples"></a><span data-ttu-id="27e64-242">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="27e64-242">Code samples</span></span>
### <a name="efficient-list-queries-code-sample"></a><span data-ttu-id="27e64-243">효율적인 목록 쿼리 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="27e64-243">Efficient list queries code sample</span></span>
<span data-ttu-id="27e64-244">GitHub의 [EfficientListQueries][efficient_query_sample] 샘플 프로젝트를 확인하여 응용 프로그램에서 효율적인 목록 쿼리가 성능에 미치는 영향을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-244">Check out the [EfficientListQueries][efficient_query_sample] sample project on GitHub to see how efficient list querying can affect performance in an application.</span></span> <span data-ttu-id="27e64-245">이 C# 콘솔 응용 프로그램은 많은 작업을 만들고 또 작업에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-245">This C# console application creates and adds a large number of tasks to a job.</span></span> <span data-ttu-id="27e64-246">그런 다음 [JobOperations.ListTasks][net_list_tasks] 메서드에 대한 여러 호출을 만들고 다른 속성 값으로 구성된 [ODATADetailLevel][odata] 개체를 전달하여 반환될 데이터의 크기를 다양화합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-246">Then, it makes multiple calls to the [JobOperations.ListTasks][net_list_tasks] method and passes [ODATADetailLevel][odata] objects that are configured with different property values to vary the amount of data to be returned.</span></span> <span data-ttu-id="27e64-247">다음과 유사한 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-247">It produces output similar to the following:</span></span>

```
Adding 5000 tasks to job jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER to query tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER to continue...
```

<span data-ttu-id="27e64-248">경과된 시간에서 보는 것처럼 반환되는 항목 수와 속성을 제한하여 쿼리 응답 시간을 크게 낮출 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-248">As shown in the elapsed times, you can greatly lower query response times by limiting the properties and the number of items that are returned.</span></span> <span data-ttu-id="27e64-249">이 샘플 프로젝트와 다른 샘플 프로젝트가 GitHub의 [azure-batch-samples][github_samples] 리포지토리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-249">You can find this and other sample projects in the [azure-batch-samples][github_samples] repository on GitHub.</span></span>

### <a name="batchmetrics-library-and-code-sample"></a><span data-ttu-id="27e64-250">BatchMetrics 라이브러리 및 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="27e64-250">BatchMetrics library and code sample</span></span>
<span data-ttu-id="27e64-251">위의 EfficientListQueries 코드 샘플 외에도 [azure-batch-samples][github_samples] GitHub 리포지토리에서 [BatchMetrics][batch_metrics] 프로젝트를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-251">In addition to the EfficientListQueries code sample above, you can find the [BatchMetrics][batch_metrics] project in the [azure-batch-samples][github_samples] GitHub repository.</span></span> <span data-ttu-id="27e64-252">BatchMetrics 샘플 프로젝트는 배치 API를 사용하여 Azure Batch 작업 진행률을 효율적으로 모니터링하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-252">The BatchMetrics sample project demonstrates how to efficiently monitor Azure Batch job progress using the Batch API.</span></span>

<span data-ttu-id="27e64-253">[BatchMetrics][batch_metrics] 샘플은 자체 프로젝트로 통합할 수 있는 .NET 클래스 라이브러리 프로젝트 및 라이브러리의 사용을 연습하고 설명하는 간단한 명령줄 프로그램을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-253">The [BatchMetrics][batch_metrics] sample includes a .NET class library project which you can incorporate into your own projects, and a simple command-line program to exercise and demonstrate the use of the library.</span></span>

<span data-ttu-id="27e64-254">프로젝트 내의 샘플 응용 프로그램은 다음 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-254">The sample application within the project demonstrates the following operations:</span></span>

1. <span data-ttu-id="27e64-255">필요한 속성에 대해서만 다운로드하기 위해 특정 특성 선택</span><span class="sxs-lookup"><span data-stu-id="27e64-255">Selecting specific attributes in order to download only the properties you need</span></span>
2. <span data-ttu-id="27e64-256">마지막 쿼리 이후에 변경 내용만 다운로드하기 위해 상태 전환 시간에서 필터링</span><span class="sxs-lookup"><span data-stu-id="27e64-256">Filtering on state transition times in order to download only changes since the last query</span></span>

<span data-ttu-id="27e64-257">예를 들어 다음 메서드는 BatchMetrics 라이브러리에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-257">For example, the following method appears in the BatchMetrics library.</span></span> <span data-ttu-id="27e64-258">쿼리되는 엔터티에 대해 `id` 및 `state` 속성만 가져와야 한다고 지정하는 ODATADetailLevel을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-258">It returns an ODATADetailLevel that specifies that only the `id` and `state` properties should be obtained for the entities that are queried.</span></span> <span data-ttu-id="27e64-259">또한 지정된 `DateTime` 매개 변수로 인해 상태가 변경된 엔터티만을 반환해야 한다고 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-259">It also specifies that only entities whose state has changed since the specified `DateTime` parameter should be returned.</span></span>

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a><span data-ttu-id="27e64-260">다음 단계</span><span class="sxs-lookup"><span data-stu-id="27e64-260">Next steps</span></span>
### <a name="parallel-node-tasks"></a><span data-ttu-id="27e64-261">병렬 노드 작업</span><span class="sxs-lookup"><span data-stu-id="27e64-261">Parallel node tasks</span></span>
<span data-ttu-id="27e64-262">[동시 노드 작업으로 Azure Batch 계산 리소스 사용 극대화](batch-parallel-node-tasks.md) 는 Batch 응용 프로그램 성능과 관련된 다른 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-262">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) is another article related to Batch application performance.</span></span> <span data-ttu-id="27e64-263">일부 유형의 작업은 더 크지만 더 적은 계산 노드에서의 병렬 작업 실행에서 이점을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-263">Some types of workloads can benefit from executing parallel tasks on larger--but fewer--compute nodes.</span></span> <span data-ttu-id="27e64-264">이러한 시나리오에 대한 자세한 내용은 문서의 [예제 시나리오](batch-parallel-node-tasks.md#example-scenario) 를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="27e64-264">Check out the [example scenario](batch-parallel-node-tasks.md#example-scenario) in the article for details on such a scenario.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="27e64-265">배치 포럼</span><span class="sxs-lookup"><span data-stu-id="27e64-265">Batch Forum</span></span>
<span data-ttu-id="27e64-266">MSDN의 [Azure Batch 포럼][forum]은 Batch를 설명하고 서비스에 대한 질문을 하는 데 많은 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-266">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="27e64-267">유용한 "고정" 게시물을 참조하고 Batch 솔루션을 빌드하는 동안 질문이 생기면 즉시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="27e64-267">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_metrics]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchMetrics
[efficient_query_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/EfficientListQueries
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_samples]: https://github.com/Azure/azure-batch-samples
[odata]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[odata_ctor]: https://msdn.microsoft.com/library/azure/dn866178.aspx
[odata_expand]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.expandclause.aspx
[odata_filter]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.filterclause.aspx
[odata_select]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.selectclause.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[rest_list_certs]: https://msdn.microsoft.com/library/azure/dn820154.aspx
[rest_list_compute_nodes]: https://msdn.microsoft.com/library/azure/dn820159.aspx
[rest_list_job_schedules]: https://msdn.microsoft.com/library/azure/mt282174.aspx
[rest_list_jobprep_status]: https://msdn.microsoft.com/library/azure/mt282170.aspx
[rest_list_jobs]: https://msdn.microsoft.com/library/azure/dn820117.aspx
[rest_list_nodefiles]: https://msdn.microsoft.com/library/azure/dn820151.aspx
[rest_list_pools]: https://msdn.microsoft.com/library/azure/dn820101.aspx
[rest_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/mt282169.aspx
[rest_list_task_files]: https://msdn.microsoft.com/library/azure/dn820142.aspx
[rest_list_tasks]: https://msdn.microsoft.com/library/azure/dn820187.aspx

[rest_get_cert]: https://msdn.microsoft.com/library/azure/dn820176.aspx
[rest_get_job]: https://msdn.microsoft.com/library/azure/dn820106.aspx
[rest_get_node]: https://msdn.microsoft.com/library/azure/dn820168.aspx
[rest_get_pool]: https://msdn.microsoft.com/library/azure/dn820165.aspx
[rest_get_schedule]: https://msdn.microsoft.com/library/azure/mt282171.aspx
[rest_get_task]: https://msdn.microsoft.com/library/azure/dn820133.aspx

[net_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificate.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_schedule]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjobschedule.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx

[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job