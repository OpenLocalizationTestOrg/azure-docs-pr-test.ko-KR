---
title: "Azure Cosmos DB에 Robomongo 사용 | Microsoft Docs"
description: "Azure Cosmos DB: MongoDB API 계정으로 Robomongo를 사용하는 방법을 알아봅니다."
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
ms.openlocfilehash: 8983594776a1bbe413a6d7cf2cd518f0e327648a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="98e7c-104">Azure Cosmos DB: MongoDB API 계정으로 Robomongo 사용</span><span class="sxs-lookup"><span data-stu-id="98e7c-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="98e7c-105">Robomongo를 사용하여 Azure Cosmos DB: MongoDB API 계정에 연결하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7c-105">To connect to an Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="98e7c-106">[Robomongo](https://robomongo.org/) 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="98e7c-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="98e7c-107">Azure Cosmos DB: MongoDB API 계정의 [연결 문자열](connect-mongodb-account.md) 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7c-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="98e7c-108">Robomongo를 사용하여 연결</span><span class="sxs-lookup"><span data-stu-id="98e7c-108">Connect using Robomongo</span></span>
<span data-ttu-id="98e7c-109">Azure Cosmos DB: MongoDB API 계정을 Robomongo MongoDB 연결에 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7c-109">To add your Azure Cosmos DB: API for MongoDB account to the Robomongo MongoDB Connections, perform the following steps.</span></span>

1. <span data-ttu-id="98e7c-110">[여기](connect-mongodb-account.md)에 있는 지침을 사용하여 Azure Cosmos DB: MongoDB API 계정 연결 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7c-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![연결 문자열 블레이드의 스크린샷](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="98e7c-112">*Robomongo.exe* 실행</span><span class="sxs-lookup"><span data-stu-id="98e7c-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="98e7c-113">연결을 관리하려면 **파일**에서 연결 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7c-113">Click the connection button under **File** to manage your connections.</span></span> <span data-ttu-id="98e7c-114">그런 다음 **MongoDB 연결** 창에서 **만들기**를 클릭하면 **연결 설정** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="98e7c-114">Then, click **Create** in the **MongoDB Connections** window, which will open up the **Connection Settings** window.</span></span>

4. <span data-ttu-id="98e7c-115">**연결 설정** 창에서 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7c-115">In the **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="98e7c-116">그런 다음 1단계의 연결 정보에서 **호스트** 및 **포트**를 찾아 **주소** 및 **포트**에 각각 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7c-116">Then, find the **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Robomongo 연결 관리의 스크린샷](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="98e7c-118">**인증** 탭에서 **인증 수행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7c-118">On the **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="98e7c-119">그런 다음 데이터베이스(기본값은 *관리자*), **사용자 이름** 및 **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7c-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="98e7c-120">**사용자 이름** 및 **암호**는 모두 1단계의 연결 정보에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98e7c-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Robomongo 인증 탭의 스크린샷](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="98e7c-122">**SSL** 탭에서 **SSL 프로토콜 사용**을 선택한 다음 **인증 방법**을 **자체 서명된 인증서**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7c-122">On the **SSL** tab, check **Use SSL protocol**, then change the **Authentication Method** to **Self-signed Certificate**.</span></span>

    ![Robomongo SSL 탭의 스크린샷](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="98e7c-124">마지막으로 **테스트**를 클릭하여 연결할 수 있는지 확인한 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="98e7c-124">Finally, click **Test** to verify that you are able to connect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98e7c-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98e7c-125">Next steps</span></span>
* <span data-ttu-id="98e7c-126">Azure Cosmos DB: MongoDB API [샘플](mongodb-samples.md)을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="98e7c-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
