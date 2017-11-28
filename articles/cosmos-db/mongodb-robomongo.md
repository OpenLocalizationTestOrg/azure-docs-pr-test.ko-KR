---
title: Azure Cosmos db Robomongo aaaUse | Microsoft Docs
description: "자세한 내용은 방법 toouse Azure Cosmos DB와 함께 Robomongo: MongoDB 계정에 대 한 API"
keywords: robomongo
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
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="7aad2-104">Azure Cosmos DB: MongoDB API 계정으로 Robomongo 사용</span><span class="sxs-lookup"><span data-stu-id="7aad2-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="7aad2-105">Azure Cosmos DB tooconnect tooan: Robomongo를 사용 하 여 MongoDB 계정에 대 한 API를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aad2-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="7aad2-106">[Robomongo](https://robomongo.org/) 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="7aad2-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="7aad2-107">Azure Cosmos DB: MongoDB API 계정의 [연결 문자열](connect-mongodb-account.md) 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7aad2-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="7aad2-108">Robomongo를 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="7aad2-108">Connect using Robomongo</span></span>
<span data-ttu-id="7aad2-109">tooadd Azure Cosmos DB: MongoDB 계정 toohello Robomongo MongoDB 연결에 대 한 API hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aad2-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello Robomongo MongoDB Connections, perform hello following steps.</span></span>

1. <span data-ttu-id="7aad2-110">Azure Cosmos DB 검색: hello 지침을 사용 하 여 MongoDB 계정 연결 정보에 대 한 API [여기](connect-mongodb-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7aad2-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Hello 연결 문자열 블레이드의 스크린 샷](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="7aad2-112">*Robomongo.exe* 실행</span><span class="sxs-lookup"><span data-stu-id="7aad2-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="7aad2-113">아래 hello 연결 단추를 클릭 **파일** toomanage 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aad2-113">Click hello connection button under **File** toomanage your connections.</span></span> <span data-ttu-id="7aad2-114">클릭 **만들기** hello에 **MongoDB 연결** hello를 열 수 있는 창을 **연결 설정을** 창.</span><span class="sxs-lookup"><span data-stu-id="7aad2-114">Then, click **Create** in hello **MongoDB Connections** window, which will open up hello **Connection Settings** window.</span></span>

4. <span data-ttu-id="7aad2-115">Hello에 **연결 설정을** 창에서 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aad2-115">In hello **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="7aad2-116">그런 다음 hello 찾을 **호스트** 및 **포트** 에 입력 하 고 1 단계에서 연결 정보를에서 만든 **주소** 및 **포트**각각 .</span><span class="sxs-lookup"><span data-stu-id="7aad2-116">Then, find hello **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![연결을 관리 하는 Robomongo hello 스크린 샷](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="7aad2-118">Hello에 **인증** 탭을 클릭 **수행 인증**합니다.</span><span class="sxs-lookup"><span data-stu-id="7aad2-118">On hello **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="7aad2-119">그런 다음 데이터베이스(기본값은 *관리자*), **사용자 이름** 및 **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7aad2-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="7aad2-120">**사용자 이름** 및 **암호**는 모두 1단계의 연결 정보에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aad2-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Hello Robomongo 인증 탭 스크린 샷](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="7aad2-122">Hello에 **SSL** 탭 **SSL 사용 되는 프로토콜**, 다음 hello 변경 **인증 방법을** 너무**자체 서명 된 인증서**합니다.</span><span class="sxs-lookup"><span data-stu-id="7aad2-122">On hello **SSL** tab, check **Use SSL protocol**, then change hello **Authentication Method** too**Self-signed Certificate**.</span></span>

    ![Hello Robomongo SSL 탭 스크린 샷](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="7aad2-124">마지막으로, 클릭 **테스트** 수 tooconnect 다음 있는지 tooverify **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="7aad2-124">Finally, click **Test** tooverify that you are able tooconnect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7aad2-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7aad2-125">Next steps</span></span>
* <span data-ttu-id="7aad2-126">Azure Cosmos DB: MongoDB API [샘플](mongodb-samples.md)을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="7aad2-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
