---
title: "Azure Cosmos DB 계정에 대한 MongoDB 연결 문자열 | Microsoft Docs"
description: "MongoDB 연결 문자열을 사용하여 MongoDB 앱을 Azure Cosmos DB 계정에 연결하는 방법에 대해 알아봅니다."
keywords: "MongoDB 연결 문자열"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: 5a47001705531d971d3181df9c0aa8f957168845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-mongodb-application-to-azure-cosmos-db"></a><span data-ttu-id="a91cd-104">Azure Cosmos DB에 MongoDB 응용 프로그램 연결</span><span class="sxs-lookup"><span data-stu-id="a91cd-104">Connect a MongoDB application to Azure Cosmos DB</span></span>
<span data-ttu-id="a91cd-105">MongoDB 연결 문자열을 사용하여 MongoDB 앱을 Azure Cosmos DB 계정에 연결하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-105">Learn how to connect your MongoDB app to an Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="a91cd-106">그런 다음 Azure Cosmos DB 데이터베이스를 MongoDB 앱의 데이터 저장소로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-106">You can then use an Azure Cosmos DB database as the data store for your MongoDB app.</span></span> 

<span data-ttu-id="a91cd-107">이 자습서에서는 연결 문자열 정보를 검색하는 다음 두 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-107">This tutorial provides two ways to retrieve connection string information:</span></span>

- <span data-ttu-id="a91cd-108">[빠른 시작 방법](#QuickstartConnection) - .NET, Node.js, MongoDB Shell, Java 및 Python 드라이버와 함께 사용</span><span class="sxs-lookup"><span data-stu-id="a91cd-108">[The quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="a91cd-109">[사용자 지정 연결 문자열 방법](#GetCustomConnection) - 다른 드라이버와 함께 사용</span><span class="sxs-lookup"><span data-stu-id="a91cd-109">[The custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a91cd-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a91cd-110">Prerequisites</span></span>

- <span data-ttu-id="a91cd-111">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="a91cd-111">An Azure account.</span></span> <span data-ttu-id="a91cd-112">Azure 계정이 없으면 지금 [무료 Azure 계정](https://azure.microsoft.com/free/)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="a91cd-113">Azure Cosmos DB 계정.</span><span class="sxs-lookup"><span data-stu-id="a91cd-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="a91cd-114">지침은 [.NET 및 Azure Portal에서 MongoDB API 웹앱 빌드](create-mongodb-dotnet.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a91cd-114">For instructions, see [Build a MongoDB API web app with .NET and the Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="a91cd-115"><a id="QuickstartConnection"></a>빠른 시작을 사용하여 MongoDB 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="a91cd-115"><a id="QuickstartConnection"></a>Get the MongoDB connection string by using the quick start</span></span>
1. <span data-ttu-id="a91cd-116">인터넷 브라우저에서 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-116">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a91cd-117">**Azure Cosmos DB** 블레이드에서 MongoDB용 API 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-117">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="a91cd-118">계정 블레이드의 왼쪽 창에서 **빠른 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-118">In the left pane of the account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="a91cd-119">플랫폼(**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="a91cd-120">드라이버나 도구가 목록에 없더라도 계속해서 더 많은 연결 코드 조각을 문서화하므로 걱정하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a91cd-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="a91cd-121">아래에 보고 싶은 항목에 대한 의견을 보내주세요.</span><span class="sxs-lookup"><span data-stu-id="a91cd-121">Please comment below on what you'd like to see.</span></span> <span data-ttu-id="a91cd-122">사용자 고유의 연결을 만드는 방법을 알아보려면 [계정 연결 문자열 정보 가져오기](#GetCustomConnection)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a91cd-122">To learn how to craft your own connection, read [Get the account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="a91cd-123">코드 조각을 복사하여 MongoDB 앱에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-123">Copy and paste the code snippet into your MongoDB app.</span></span>

    ![빠른 시작 블레이드](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="a91cd-125"><a id="GetCustomConnection"></a> 사용자 지정할 MongoDB 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="a91cd-125"><a id="GetCustomConnection"></a> Get the MongoDB connection string to customize</span></span>
1. <span data-ttu-id="a91cd-126">인터넷 브라우저에서 [Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-126">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a91cd-127">**Azure Cosmos DB** 블레이드에서 MongoDB용 API 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-127">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="a91cd-128">계정 블레이드의 왼쪽 창에서 **연결 문자열**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-128">In the left pane of the account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="a91cd-129">**연결 문자열** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-129">The **Connection String** blade opens.</span></span> <span data-ttu-id="a91cd-130">여기에는 미리 구성된 연결 문자열을 비롯해 MongoDB용 드라이버를 사용하여 계정에 연결하는 데 필요한 모든 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-130">It has all the information necessary to connect to the account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![연결 문자열 블레이드](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="a91cd-132">연결 문자열 요구 사항</span><span class="sxs-lookup"><span data-stu-id="a91cd-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="a91cd-133">Azure Cosmos DB에는 엄격한 보안 요구 사항과 표준이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="a91cd-134">Azure Cosmos DB 계정에는 *SSL*을 통한 인증 및 보안 통신이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="a91cd-135">Azure Cosmos DB는 두 가지 특정 요구 사항을 포함한 표준 MongoDB 연결 문자열 URI 형식을 지원합니다. Azure Cosmos DB 계정에는 인증 및 SSL을 통한 보안 통신이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-135">Azure Cosmos DB supports the standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="a91cd-136">따라서 연결 문자열 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-136">So, the connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="a91cd-137">이 문자열의 값은 위에 표시된 **연결 문자열** 블레이드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-137">The values of this string are available in the **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="a91cd-138">Username(필수): Azure Cosmos DB 계정 이름</span><span class="sxs-lookup"><span data-stu-id="a91cd-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="a91cd-139">Password(필수): Azure Cosmos DB 계정 암호</span><span class="sxs-lookup"><span data-stu-id="a91cd-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="a91cd-140">Host(필수): Azure Cosmos DB 계정의 FQDN</span><span class="sxs-lookup"><span data-stu-id="a91cd-140">Host (required): FQDN of the Azure Cosmos DB account.</span></span>
* <span data-ttu-id="a91cd-141">Port(필수): 10255</span><span class="sxs-lookup"><span data-stu-id="a91cd-141">Port (required): 10255.</span></span>
* <span data-ttu-id="a91cd-142">Database(선택): 연결에서 사용하는 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="a91cd-142">Database (optional): The database that the connection uses.</span></span> <span data-ttu-id="a91cd-143">제공된 데이터베이스가 없는 경우 기본 데이터베이스는 "test"입니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-143">If no database is provided, the default database is "test."</span></span>
* <span data-ttu-id="a91cd-144">ssl=true(필수)</span><span class="sxs-lookup"><span data-stu-id="a91cd-144">ssl=true (required)</span></span>

<span data-ttu-id="a91cd-145">예를 들어 **연결 문자열** 블레이드에 표시된 계정을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-145">For example, consider the account shown in the **Connection String** blade.</span></span> <span data-ttu-id="a91cd-146">유효한 연결 문자열은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="a91cd-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a91cd-147">Next steps</span></span>
* <span data-ttu-id="a91cd-148">Azure Cosmos DB: MongoDB API 계정으로 [MongoChef를 사용](mongodb-mongochef.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-148">Learn how to [use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="a91cd-149">[샘플](mongodb-samples.md)을 통해 Azure Cosmos DB API for MongoDB를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="a91cd-149">Explore the Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
