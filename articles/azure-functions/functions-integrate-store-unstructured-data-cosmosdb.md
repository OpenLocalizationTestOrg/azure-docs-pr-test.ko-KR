---
title: "aaaStore Azure 함수 및 Cosmos DB를 사용 하 여 구조화 되지 않은 데이터"
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
ms.openlocfilehash: 48d6899c20d3e6f6b062725fca329972ead3c696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="store-unstructured-data-using-azure-functions-and-cosmos-db"></a><span data-ttu-id="650e1-104">Azure Functions 및 Cosmos DB를 사용하여 구조화되지 않은 데이터 저장</span><span class="sxs-lookup"><span data-stu-id="650e1-104">Store unstructured data using Azure Functions and Cosmos DB</span></span>

<span data-ttu-id="650e1-105">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 은 구조화 되지 않은 위한 훌륭한 방법 toostore 및 JSON 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-105">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a great way toostore unstructured and JSON data.</span></span> <span data-ttu-id="650e1-106">Cosmos DB를 Azure Functions와 함께 사용하면 관계형 데이터베이스에 데이터를 저장하는 데 필요한 것보다 훨씬 적은 코드를 사용하여 쉽고 빠르게 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-106">Combined with Azure Functions, Cosmos DB makes storing data quick and easy with much less code than required for storing data in a relational database.</span></span>

<span data-ttu-id="650e1-107">Azure 기능 입력 및 출력 바인딩은 함수에서 선언적으로 tooconnect tooexternal 서비스 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-107">In Azure Functions, input and output bindings provide a declarative way tooconnect tooexternal service data from your function.</span></span> <span data-ttu-id="650e1-108">이 항목에서는 tooupdate 하 여 기존 C# 작동 방식을 tooadd Cosmos DB 문서에 구조화 되지 않은 데이터를 저장 하는 출력 바인딩이 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-108">In this topic, learn how tooupdate an existing C# function tooadd an output binding that stores unstructured data in a Cosmos DB document.</span></span> 

![Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a><span data-ttu-id="650e1-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="650e1-110">Prerequisites</span></span>

<span data-ttu-id="650e1-111">toocomplete이이 자습서:</span><span class="sxs-lookup"><span data-stu-id="650e1-111">toocomplete this tutorial:</span></span>

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a><span data-ttu-id="650e1-112">출력 바인딩 추가</span><span class="sxs-lookup"><span data-stu-id="650e1-112">Add an output binding</span></span>

1. <span data-ttu-id="650e1-113">함수 앱과 함수를 모두 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-113">Expand both your function app and your function.</span></span>

1. <span data-ttu-id="650e1-114">선택 **통합** 및 **+ 새 출력**, hello에 hello 페이지의 오른쪽 위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-114">Select **Integrate** and **+ New Output**, which is at hello top right of hello page.</span></span> <span data-ttu-id="650e1-115">**Azure Cosmos DB**를 선택하고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-115">Choose **Azure Cosmos DB**, and click **Select**.</span></span>

    ![Cosmos DB 출력 바인딩 추가](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. <span data-ttu-id="650e1-117">사용 하 여 hello **Azure Cosmos DB 출력** hello 테이블에 지정 된 설정:</span><span class="sxs-lookup"><span data-stu-id="650e1-117">Use hello **Azure Cosmos DB output** settings as specified in hello table:</span></span> 

    ![Cosmos DB 출력 바인딩 구성](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | <span data-ttu-id="650e1-119">설정</span><span class="sxs-lookup"><span data-stu-id="650e1-119">Setting</span></span>      | <span data-ttu-id="650e1-120">제안 값</span><span class="sxs-lookup"><span data-stu-id="650e1-120">Suggested value</span></span>  | <span data-ttu-id="650e1-121">설명</span><span class="sxs-lookup"><span data-stu-id="650e1-121">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="650e1-122">**문서 매개 변수 이름**</span><span class="sxs-lookup"><span data-stu-id="650e1-122">**Document parameter name**</span></span> | <span data-ttu-id="650e1-123">taskDocument</span><span class="sxs-lookup"><span data-stu-id="650e1-123">taskDocument</span></span> | <span data-ttu-id="650e1-124">코드에서 toohello Cosmos DB 개체 참조 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-124">Name that refers toohello Cosmos DB object in code.</span></span> |
    | <span data-ttu-id="650e1-125">**데이터베이스 이름**</span><span class="sxs-lookup"><span data-stu-id="650e1-125">**Database name**</span></span> | <span data-ttu-id="650e1-126">taskDatabase</span><span class="sxs-lookup"><span data-stu-id="650e1-126">taskDatabase</span></span> | <span data-ttu-id="650e1-127">데이터베이스 toosave 문서의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-127">Name of database toosave documents.</span></span> |
    | <span data-ttu-id="650e1-128">**컬렉션 이름**</span><span class="sxs-lookup"><span data-stu-id="650e1-128">**Collection name**</span></span> | <span data-ttu-id="650e1-129">TaskCollection</span><span class="sxs-lookup"><span data-stu-id="650e1-129">TaskCollection</span></span> | <span data-ttu-id="650e1-130">Cosmos DB 데이터베이스의 컬렉션 이름.</span><span class="sxs-lookup"><span data-stu-id="650e1-130">Name of collection of Cosmos DB databases.</span></span> |
    | <span data-ttu-id="650e1-131">**True 이면 hello Cosmos DB 데이터베이스 및 컬렉션을 만듭니다.**</span><span class="sxs-lookup"><span data-stu-id="650e1-131">**If true, creates hello Cosmos DB database and collection**</span></span> | <span data-ttu-id="650e1-132">선택</span><span class="sxs-lookup"><span data-stu-id="650e1-132">Checked</span></span> | <span data-ttu-id="650e1-133">hello 컬렉션 이미 존재, 따라서 만들 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-133">hello collection doesn't already exist, so create it.</span></span> |

4. <span data-ttu-id="650e1-134">선택 **새로** 다음 toohello **Cosmos DB 문서 연결** , 레이블 지정 및 선택 **+ 새로 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-134">Select **New** next toohello **Cosmos DB document connection** label, and select **+ Create new**.</span></span> 

5. <span data-ttu-id="650e1-135">사용 하 여 hello **새 계정** hello 테이블에 지정 된 설정:</span><span class="sxs-lookup"><span data-stu-id="650e1-135">Use hello **New account** settings as specified in hello table:</span></span> 

    ![Cosmos DB 연결 구성](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | <span data-ttu-id="650e1-137">설정</span><span class="sxs-lookup"><span data-stu-id="650e1-137">Setting</span></span>      | <span data-ttu-id="650e1-138">제안 값</span><span class="sxs-lookup"><span data-stu-id="650e1-138">Suggested value</span></span>  | <span data-ttu-id="650e1-139">설명</span><span class="sxs-lookup"><span data-stu-id="650e1-139">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="650e1-140">**ID**</span><span class="sxs-lookup"><span data-stu-id="650e1-140">**ID**</span></span> | <span data-ttu-id="650e1-141">데이터베이스의 이름</span><span class="sxs-lookup"><span data-stu-id="650e1-141">Name of database</span></span> | <span data-ttu-id="650e1-142">Hello Cosmos DB 데이터베이스에 대 한 고유 ID</span><span class="sxs-lookup"><span data-stu-id="650e1-142">Unique ID for hello Cosmos DB database</span></span>  |
    | <span data-ttu-id="650e1-143">**API**</span><span class="sxs-lookup"><span data-stu-id="650e1-143">**API**</span></span> | <span data-ttu-id="650e1-144">SQL(DocumentDB)</span><span class="sxs-lookup"><span data-stu-id="650e1-144">SQL (DocumentDB)</span></span> | <span data-ttu-id="650e1-145">Hello 문서 데이터베이스 API를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-145">Select hello document database API.</span></span>  |
    | <span data-ttu-id="650e1-146">**구독**</span><span class="sxs-lookup"><span data-stu-id="650e1-146">**Subscription**</span></span> | <span data-ttu-id="650e1-147">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="650e1-147">Azure Subscription</span></span> | <span data-ttu-id="650e1-148">Azure 구독</span><span class="sxs-lookup"><span data-stu-id="650e1-148">Azure Subscription</span></span>  |
    | <span data-ttu-id="650e1-149">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="650e1-149">**Resource Group**</span></span> | <span data-ttu-id="650e1-150">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="650e1-150">myResourceGroup</span></span> |  <span data-ttu-id="650e1-151">함수에서 사용 하는 앱을 포함 하는 hello 기존 리소스 그룹을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-151">Use hello existing resource group that contains your function app.</span></span> |
    | <span data-ttu-id="650e1-152">**위치**:</span><span class="sxs-lookup"><span data-stu-id="650e1-152">**Location**</span></span>  | <span data-ttu-id="650e1-153">WestEurope</span><span class="sxs-lookup"><span data-stu-id="650e1-153">WestEurope</span></span> | <span data-ttu-id="650e1-154">함수 앱 이나 hello 저장 된 문서를 사용 하는 tooother 앱 tooeither 가까운 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-154">Select a location near tooeither your function app or tooother apps that use hello stored documents.</span></span>  |

6. <span data-ttu-id="650e1-155">클릭 **확인** toocreate hello 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-155">Click **OK** toocreate hello database.</span></span> <span data-ttu-id="650e1-156">몇 분 toocreate hello 데이터베이스를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-156">It may take a few minutes toocreate hello database.</span></span> <span data-ttu-id="650e1-157">Hello 데이터베이스를 만든 후 데이터베이스 연결 문자열 hello 함수 응용 프로그램 설정으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-157">After hello database is created, hello database connection string is stored as a function app setting.</span></span> <span data-ttu-id="650e1-158">이 앱 설정의 hello 이름에 삽입 됩니다 **Cosmos DB 계정 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-158">hello name of this app setting is inserted in **Cosmos DB account connection**.</span></span> 
 
8. <span data-ttu-id="650e1-159">Hello 연결 문자열을 설정한 후 선택 **저장** toocreate hello 바인딩.</span><span class="sxs-lookup"><span data-stu-id="650e1-159">After hello connection string is set, select **Save** toocreate hello binding.</span></span>

## <a name="update-hello-function-code"></a><span data-ttu-id="650e1-160">Hello 함수 코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-160">Update hello function code</span></span>

<span data-ttu-id="650e1-161">코드를 함수 hello 기존 C# 코드 다음 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-161">Replace hello existing C# function code with hello following code:</span></span>

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
<span data-ttu-id="650e1-162">이 코드 샘플 hello HTTP 요청 쿼리 문자열을 읽고 toofields hello에 할당 합니다 `taskDocument` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-162">This code sample reads hello HTTP Request query strings and assigns them toofields in hello `taskDocument` object.</span></span> <span data-ttu-id="650e1-163">hello `taskDocument` 바인딩 hello 바인딩된 문서 데이터베이스에 저장 된 바인딩 매개 변수 toobe이에서 hello 개체 데이터를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-163">hello `taskDocument` binding sends hello object data from this binding parameter toobe stored in hello bound document database.</span></span> <span data-ttu-id="650e1-164">hello 데이터베이스 hello hello 함수를 실행 하는 처음으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-164">hello database is created hello first time hello function runs.</span></span>

## <a name="test-hello-function-and-database"></a><span data-ttu-id="650e1-165">테스트 hello 함수 및 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="650e1-165">Test hello function and database</span></span>

1. <span data-ttu-id="650e1-166">오른쪽 창 hello를 확장 하 고 선택 **테스트**합니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-166">Expand hello right window and select **Test**.</span></span> <span data-ttu-id="650e1-167">아래 **쿼리**, 클릭 **+ 매개 변수 추가** hello toohello 쿼리 문자열 매개 변수를 다음 추가:</span><span class="sxs-lookup"><span data-stu-id="650e1-167">Under **Query**, click **+ Add parameter** and add hello following parameters toohello query string:</span></span>

    + `name`
    + `task`
    + `duedate`

2. <span data-ttu-id="650e1-168">**실행**을 클릭하고 200 상태가 반환되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-168">Click **Run** and verify that a 200 status is returned.</span></span>

    ![Cosmos DB 출력 바인딩 구성](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. <span data-ttu-id="650e1-170">Hello hello Azure 포털의 왼쪽, 확장 hello 아이콘 표시줄 형식 `cosmos` hello 검색 필드 및 선택 **Azure Cosmos DB**합니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-170">On hello left side of hello Azure portal, expand hello icon bar, type `cosmos` in hello search field, and select **Azure Cosmos DB**.</span></span>

    ![Hello Cosmos DB 서비스 검색](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. <span data-ttu-id="650e1-172">선택 hello 데이터베이스를 만든 다음 선택 **데이터 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-172">Select hello database you created, then select **Data Explorer**.</span></span> <span data-ttu-id="650e1-173">Hello 확장 **컬렉션** 노드 hello 새 문서를 선택 하 고 몇 가지 추가 메타 데이터와 함께 하 여 쿼리 문자열 값을 포함 하는 hello 문서를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-173">Expand hello **Collections** nodes, select hello new document, and confirm that hello document contains your query string values, along with some additional metadata.</span></span> 

    ![Cosmos DB 항목 확인](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

<span data-ttu-id="650e1-175">Cosmos DB 데이터베이스에 구조화 되지 않은 데이터를 저장 하는 바인딩 tooyour HTTP 트리거를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-175">You have successfully added a binding tooyour HTTP trigger that stores unstructured data in a Cosmos DB database.</span></span>

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="650e1-176">다음 단계</span><span class="sxs-lookup"><span data-stu-id="650e1-176">Next steps</span></span>

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="650e1-177">바인딩 tooa Cosmos DB 데이터베이스에 대 한 자세한 내용은 참조 [Azure 함수 Cosmos DB 바인딩](functions-bindings-documentdb.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="650e1-177">For more information about binding tooa Cosmos DB database, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>
