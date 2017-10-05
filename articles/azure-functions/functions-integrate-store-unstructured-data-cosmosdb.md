---
title: "Azure Functions 및 Cosmos DB를 사용하여 구조화되지 않은 데이터 저장"
description: "Azure Functions 및 Cosmos DB를 사용하여 구조화되지 않은 데이터 저장"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, Functions, 이벤트 처리, Cosmos DB, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: 
ms.service: functions
ms.devlang: csharp
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 7c18676ff94ec7da17094abc5f33fb3c6a79895f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="store-unstructured-data-using-azure-functions-and-cosmos-db"></a><span data-ttu-id="32169-104">Azure Functions 및 Cosmos DB를 사용하여 구조화되지 않은 데이터 저장</span><span class="sxs-lookup"><span data-stu-id="32169-104">Store unstructured data using Azure Functions and Cosmos DB</span></span>

<span data-ttu-id="32169-105">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)는 구조화되지 않은 데이터 및 JSON 데이터를 저장하기 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="32169-105">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a great way to store unstructured and JSON data.</span></span> <span data-ttu-id="32169-106">Cosmos DB를 Azure Functions와 함께 사용하면 관계형 데이터베이스에 데이터를 저장하는 데 필요한 것보다 훨씬 적은 코드를 사용하여 쉽고 빠르게 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32169-106">Combined with Azure Functions, Cosmos DB makes storing data quick and easy with much less code than required for storing data in a relational database.</span></span>

<span data-ttu-id="32169-107">Azure Functions에서 입력 및 출력 바인딩은 함수에서 외부 서비스 데이터로 연결하기 위한 선언적 방식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-107">In Azure Functions, input and output bindings provide a declarative way to connect to external service data from your function.</span></span> <span data-ttu-id="32169-108">이 토픽에서는 기존 C# 함수를 업데이트하여 구조화되지 않은 데이터를 Cosmos DB 문서에 저장하는 출력 바인딩을 추가하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="32169-108">In this topic, learn how to update an existing C# function to add an output binding that stores unstructured data in a Cosmos DB document.</span></span> 

![Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a><span data-ttu-id="32169-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="32169-110">Prerequisites</span></span>

<span data-ttu-id="32169-111">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-111">To complete this tutorial:</span></span>

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a><span data-ttu-id="32169-112">출력 바인딩 추가</span><span class="sxs-lookup"><span data-stu-id="32169-112">Add an output binding</span></span>

1. <span data-ttu-id="32169-113">함수 앱과 함수를 모두 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-113">Expand both your function app and your function.</span></span>

1. <span data-ttu-id="32169-114">페이지 오른쪽 위에서 **통합** 및 **+ 새 출력**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-114">Select **Integrate** and **+ New Output**, which is at the top right of the page.</span></span> <span data-ttu-id="32169-115">**Azure Cosmos DB**를 선택하고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-115">Choose **Azure Cosmos DB**, and click **Select**.</span></span>

    ![Cosmos DB 출력 바인딩 추가](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. <span data-ttu-id="32169-117">다음 표에 지정된 대로 **Azure Cosmos DB 출력** 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-117">Use the **Azure Cosmos DB output** settings as specified in the table:</span></span> 

    ![Cosmos DB 출력 바인딩 구성](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | <span data-ttu-id="32169-119">설정</span><span class="sxs-lookup"><span data-stu-id="32169-119">Setting</span></span>      | <span data-ttu-id="32169-120">제안 값</span><span class="sxs-lookup"><span data-stu-id="32169-120">Suggested value</span></span>  | <span data-ttu-id="32169-121">설명</span><span class="sxs-lookup"><span data-stu-id="32169-121">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="32169-122">**문서 매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="32169-122">**Document parameter name**</span></span> | <span data-ttu-id="32169-123">taskDocument</span><span class="sxs-lookup"><span data-stu-id="32169-123">taskDocument</span></span> | <span data-ttu-id="32169-124">코드에서 Cosmos DB 개체를 참조하는 이름.</span><span class="sxs-lookup"><span data-stu-id="32169-124">Name that refers to the Cosmos DB object in code.</span></span> |
    | <span data-ttu-id="32169-125">**데이터베이스 이름**</span><span class="sxs-lookup"><span data-stu-id="32169-125">**Database name**</span></span> | <span data-ttu-id="32169-126">taskDatabase</span><span class="sxs-lookup"><span data-stu-id="32169-126">taskDatabase</span></span> | <span data-ttu-id="32169-127">문서를 저장할 데이터베이스의 이름.</span><span class="sxs-lookup"><span data-stu-id="32169-127">Name of database to save documents.</span></span> |
    | <span data-ttu-id="32169-128">**컬렉션 이름**</span><span class="sxs-lookup"><span data-stu-id="32169-128">**Collection name**</span></span> | <span data-ttu-id="32169-129">TaskCollection</span><span class="sxs-lookup"><span data-stu-id="32169-129">TaskCollection</span></span> | <span data-ttu-id="32169-130">Cosmos DB 데이터베이스의 컬렉션 이름.</span><span class="sxs-lookup"><span data-stu-id="32169-130">Name of collection of Cosmos DB databases.</span></span> |
    | <span data-ttu-id="32169-131">**true이면 Cosmos DB 데이터베이스 및 컬렉션을 만듭니다.**</span><span class="sxs-lookup"><span data-stu-id="32169-131">**If true, creates the Cosmos DB database and collection**</span></span> | <span data-ttu-id="32169-132">선택</span><span class="sxs-lookup"><span data-stu-id="32169-132">Checked</span></span> | <span data-ttu-id="32169-133">아직 컬렉션이 없으므로 지금 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32169-133">The collection doesn't already exist, so create it.</span></span> |

4. <span data-ttu-id="32169-134">**Cosmos DB 문서 연결** 레이블 옆에 있는 **새로 만들기**를 선택하고 **+ 새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-134">Select **New** next to the **Cosmos DB document connection** label, and select **+ Create new**.</span></span> 

5. <span data-ttu-id="32169-135">다음 표에 지정된 대로 **새 계정** 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-135">Use the **New account** settings as specified in the table:</span></span> 

    ![Cosmos DB 연결 구성](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | <span data-ttu-id="32169-137">설정</span><span class="sxs-lookup"><span data-stu-id="32169-137">Setting</span></span>      | <span data-ttu-id="32169-138">제안 값</span><span class="sxs-lookup"><span data-stu-id="32169-138">Suggested value</span></span>  | <span data-ttu-id="32169-139">설명</span><span class="sxs-lookup"><span data-stu-id="32169-139">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="32169-140">**ID**</span><span class="sxs-lookup"><span data-stu-id="32169-140">**ID**</span></span> | <span data-ttu-id="32169-141">데이터베이스의 이름</span><span class="sxs-lookup"><span data-stu-id="32169-141">Name of database</span></span> | <span data-ttu-id="32169-142">Cosmos DB 데이터베이스의 고유한 ID</span><span class="sxs-lookup"><span data-stu-id="32169-142">Unique ID for the Cosmos DB database</span></span>  |
    | <span data-ttu-id="32169-143">**API**</span><span class="sxs-lookup"><span data-stu-id="32169-143">**API**</span></span> | <span data-ttu-id="32169-144">SQL(DocumentDB)</span><span class="sxs-lookup"><span data-stu-id="32169-144">SQL (DocumentDB)</span></span> | <span data-ttu-id="32169-145">문서 데이터베이스 API를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-145">Select the document database API.</span></span>  |
    | <span data-ttu-id="32169-146">**구독**</span><span class="sxs-lookup"><span data-stu-id="32169-146">**Subscription**</span></span> | <span data-ttu-id="32169-147">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="32169-147">Azure Subscription</span></span> | <span data-ttu-id="32169-148">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="32169-148">Azure Subscription</span></span>  |
    | <span data-ttu-id="32169-149">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="32169-149">**Resource Group**</span></span> | <span data-ttu-id="32169-150">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="32169-150">myResourceGroup</span></span> |  <span data-ttu-id="32169-151">함수 앱이 포함된 기존 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-151">Use the existing resource group that contains your function app.</span></span> |
    | <span data-ttu-id="32169-152">**위치**</span><span class="sxs-lookup"><span data-stu-id="32169-152">**Location**</span></span>  | <span data-ttu-id="32169-153">WestEurope</span><span class="sxs-lookup"><span data-stu-id="32169-153">WestEurope</span></span> | <span data-ttu-id="32169-154">함수 앱 또는 저장된 문서를 사용하는 다른 앱과 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-154">Select a location near to either your function app or to other apps that use the stored documents.</span></span>  |

6. <span data-ttu-id="32169-155">**확인**을 클릭하여 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32169-155">Click **OK** to create the database.</span></span> <span data-ttu-id="32169-156">데이터베이스를 만드는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32169-156">It may take a few minutes to create the database.</span></span> <span data-ttu-id="32169-157">데이터베이스가 생성되면 데이터베이스 연결 문자열이 함수 앱 설정으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="32169-157">After the database is created, the database connection string is stored as a function app setting.</span></span> <span data-ttu-id="32169-158">이 앱 설정의 이름이 **Cosmos DB 계정 연결**에 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="32169-158">The name of this app setting is inserted in **Cosmos DB account connection**.</span></span> 
 
8. <span data-ttu-id="32169-159">연결 문자열이 설정된 후에는 **저장**을 선택하여 바인딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32169-159">After the connection string is set, select **Save** to create the binding.</span></span>

## <a name="update-the-function-code"></a><span data-ttu-id="32169-160">함수 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="32169-160">Update the function code</span></span>

<span data-ttu-id="32169-161">기존 C# 함수 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="32169-161">Replace the existing C# function code with the following code:</span></span>

```csharp
using System.Net;

public static HttpResponseMessage Run(HttpRequestMessage req, out object taskDocument, TraceWriter log)
{
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    string task = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "task", true) == 0)
        .Value;

    string duedate = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "duedate", true) == 0)
        .Value;

    taskDocument = new {
        name = name,
        duedate = duedate.ToString(),
        task = task
    };

    if (name != "" && task != "") {
        return req.CreateResponse(HttpStatusCode.OK);
    }
    else {
        return req.CreateResponse(HttpStatusCode.BadRequest);
    }
}

```
<span data-ttu-id="32169-162">이 코드 샘플은 HTTP 요청 쿼리 문자열을 읽고 `taskDocument` 개체의 필드에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-162">This code sample reads the HTTP Request query strings and assigns them to fields in the `taskDocument` object.</span></span> <span data-ttu-id="32169-163">`taskDocument` 바인딩은 이 바인딩 매개 변수의 개체 데이터 중에서 바인딩된 문서 데이터베이스에 저장할 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="32169-163">The `taskDocument` binding sends the object data from this binding parameter to be stored in the bound document database.</span></span> <span data-ttu-id="32169-164">함수가 처음으로 실행될 때 데이터베이스가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="32169-164">The database is created the first time the function runs.</span></span>

## <a name="test-the-function-and-database"></a><span data-ttu-id="32169-165">함수 및 데이터베이스 테스트</span><span class="sxs-lookup"><span data-stu-id="32169-165">Test the function and database</span></span>

1. <span data-ttu-id="32169-166">오른쪽 창을 확장하고 **테스트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-166">Expand the right window and select **Test**.</span></span> <span data-ttu-id="32169-167">**쿼리** 아래에서 **+ 매개 변수 추가**를 클릭하고 쿼리 문자열에 다음 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-167">Under **Query**, click **+ Add parameter** and add the following parameters to the query string:</span></span>

    + `name`
    + `task`
    + `duedate`

2. <span data-ttu-id="32169-168">**실행**을 클릭하고 200 상태가 반환되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-168">Click **Run** and verify that a 200 status is returned.</span></span>

    ![Cosmos DB 출력 바인딩 구성](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. <span data-ttu-id="32169-170">Azure Portal의 왼쪽에서 아이콘 표시줄을 확장하고, 검색 필드에 `cosmos`를 입력하고, **Azure Cosmos DB**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-170">On the left side of the Azure portal, expand the icon bar, type `cosmos` in the search field, and select **Azure Cosmos DB**.</span></span>

    ![Cosmos DB 서비스 검색](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. <span data-ttu-id="32169-172">만든 데이터베이스를 선택한 다음 **데이터 탐색기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-172">Select the database you created, then select **Data Explorer**.</span></span> <span data-ttu-id="32169-173">**컬렉션** 노드를 확장하고, 새 문서를 선택하고, 문서에 일부 추가 메타데이터와 함께 쿼리 문자열 값이 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="32169-173">Expand the **Collections** nodes, select the new document, and confirm that the document contains your query string values, along with some additional metadata.</span></span> 

    ![Cosmos DB 항목 확인](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

<span data-ttu-id="32169-175">구조화되지 않은 데이터를 Cosmos DB 데이터베이스에 저장하는 HTTP 트리거에 성공적으로 바인딩을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="32169-175">You have successfully added a binding to your HTTP trigger that stores unstructured data in a Cosmos DB database.</span></span>

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="32169-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="32169-176">Next steps</span></span>

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="32169-177">Cosmos DB 데이터베이스에 바인딩하는 자세한 내용은 [Azure Functions Cosmos DB 바인딩](functions-bindings-documentdb.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="32169-177">For more information about binding to a Cosmos DB database, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>
