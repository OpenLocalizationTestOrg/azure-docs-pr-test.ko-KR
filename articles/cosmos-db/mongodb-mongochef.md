---
title: Azure Cosmos db MongoChef aaaUse | Microsoft Docs
description: "자세한 내용은 방법 toouse Azure Cosmos DB와 함께 MongoChef: MongoDB 계정에 대 한 API"
keywords: MongoChef
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 4b047797b231c34ccc6f2ed02416525c6228d596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="e8ce5-104">Azure Cosmos DB: MongoDB API 계정으로 MongoChef 사용</span><span class="sxs-lookup"><span data-stu-id="e8ce5-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="e8ce5-105">Azure Cosmos DB tooconnect tooan: MongoDB 계정에 대 한 API를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="e8ce5-106">[MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="e8ce5-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="e8ce5-107">Azure Cosmos DB: MongoDB API 계정의 [연결 문자열](connect-mongodb-account.md) 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-hello-connection-in-mongochef"></a><span data-ttu-id="e8ce5-108">MongoChef에 hello 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="e8ce5-108">Create hello connection in MongoChef</span></span>
<span data-ttu-id="e8ce5-109">tooadd Azure Cosmos DB: API MongoDB 계정 toohello MongoChef 연결 관리자에 대 한 수행 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello MongoChef connection manager, perform hello following steps.</span></span>

1. <span data-ttu-id="e8ce5-110">Azure Cosmos DB 검색: hello 지침을 사용 하 여 MongoDB 연결 정보에 대 한 API [여기](connect-mongodb-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Hello 연결 문자열 블레이드의 스크린 샷](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="e8ce5-112">클릭 **연결** tooopen hello 연결 관리자를 한 다음 클릭 **새 연결**</span><span class="sxs-lookup"><span data-stu-id="e8ce5-112">Click **Connect** tooopen hello Connection Manager, then click **New Connection**</span></span>

    ![Hello MongoChef 연결 관리자의 스크린 샷](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="e8ce5-114">Hello에 **새 연결** 창의 hello에 **서버** 탭을 hello hello Azure Cosmos DB의 호스트 (FQDN)을 입력: MongoDB 계정과 hello 포트에 대 한 API입니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-114">In hello **New Connection** window, on hello **Server** tab, enter hello HOST (FQDN) of hello Azure Cosmos DB: API for MongoDB account and hello PORT.</span></span>

    ![Hello MongoChef 연결 관리자 서버 탭 스크린 샷](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="e8ce5-116">Hello에 **새 연결** 창의 hello에 **인증** 탭, 인증 모드 선택 **(MONGODB CR 또는 SCARM-s h A-1) Standard** hello 사용자 이름을 입력 하 고 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-116">In hello **New Connection** window, on hello **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter hello USERNAME and PASSWORD.</span></span>  <span data-ttu-id="e8ce5-117">Hello 기본 인증 db (관리자)을 그대로 사용 하거나 사용자가 직접 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-117">Accept hello default authentication db (admin) or provide your own value.</span></span>

    ![Hello MongoChef 연결 관리자 인증 탭 스크린 샷](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="e8ce5-119">Hello에 **새 연결** 창의 hello에 **SSL** 탭에서 확인 hello **SSL 사용 되는 프로토콜 tooconnect** 확인란과 hello **Accept 서버 SSL에서 자체 서명 인증서** 라디오 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-119">In hello **New Connection** window, on hello **SSL** tab, check hello **Use SSL protocol tooconnect** check box and hello **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Hello MongoChef 연결 관리자 SSL 탭 스크린 샷](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="e8ce5-121">Hello 클릭 **연결 테스트** toovalidate hello 연결 정보 단추를 클릭 하 여 **확인** tooreturn toohello 새 연결 창에서 클릭 하 고 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-121">Click hello **Test Connection** button toovalidate hello connection information, click **OK** tooreturn toohello New Connection window, and then click **Save**.</span></span>

    ![Hello MongoChef 테스트 연결 창 스크린 샷](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a><span data-ttu-id="e8ce5-123">MongoChef toocreate 데이터베이스, 컬렉션 및 문서를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e8ce5-123">Use MongoChef toocreate a database, collection, and documents</span></span>
<span data-ttu-id="e8ce5-124">toocreate 데이터베이스, 컬렉션 및 MongoChef를 사용 하 여 문서 hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-124">toocreate a database, collection, and documents using MongoChef, perform hello following steps.</span></span>

1. <span data-ttu-id="e8ce5-125">**연결 관리자**hello 연결을 강조 표시 하 고 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-125">In **Connection Manager**, highlight hello connection and click **Connect**.</span></span>

    ![Hello MongoChef 연결 관리자의 스크린 샷](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="e8ce5-127">Hello 호스트를 마우스 오른쪽 단추로 클릭 하 고 선택 **데이터베이스 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-127">Right click hello host and choose **Add Database**.</span></span>  <span data-ttu-id="e8ce5-128">데이터베이스 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-128">Provide a database name and click **OK**.</span></span>

    ![Hello MongoChef 추가 데이터베이스 옵션의 스크린 샷](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="e8ce5-130">Hello 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 선택 **컬렉션 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-130">Right click hello database and choose **Add Collection**.</span></span>  <span data-ttu-id="e8ce5-131">컬렉션 이름을 지정하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-131">Provide a collection name and click **Create**.</span></span>

    ![Hello MongoChef 컬렉션 추가 옵션의 스크린 샷](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="e8ce5-133">Hello 클릭 **컬렉션** 메뉴 항목, 클릭 **문서 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-133">Click hello **Collection** menu item, then click **Add Document**.</span></span>

    ![Hello MongoChef 문서 추가 메뉴 항목의 스크린 샷](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="e8ce5-135">Hello 다음 붙여넣고 클릭 hello 문서 추가 대화 상자에서 **문서 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-135">In hello Add Document dialog, paste hello following and then click **Add Document**.</span></span>

        {
        "_id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
               { "firstName": "Thomas" },
               { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "isRegistered": true
        }
6. <span data-ttu-id="e8ce5-136">이 이번에는 다음 콘텐츠는 hello 다른 문서를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-136">Add another document, this time with hello following content.</span></span>

        {
        "_id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam",
                 "givenName": "Jesse",
                "gender": "female", "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            {
                "familyName": "Miller",
                 "givenName": "Lisa",
                 "gender": "female",
                 "grade": 8 }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
        }
7. <span data-ttu-id="e8ce5-137">샘플 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-137">Execute a sample query.</span></span> <span data-ttu-id="e8ce5-138">예를 들어 제품군 hello 성 'Andersen' 및 반환 hello 부모 및 상태 필드에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-138">For example, search for families with hello last name 'Andersen' and return hello parents and state fields.</span></span>

    ![MongoChef 쿼리 결과의 스크린샷](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="e8ce5-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8ce5-140">Next steps</span></span>
* <span data-ttu-id="e8ce5-141">Azure Cosmos DB: MongoDB API [샘플](mongodb-samples.md)을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="e8ce5-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
