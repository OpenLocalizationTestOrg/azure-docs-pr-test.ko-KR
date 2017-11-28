---
title: "Cosmos DB Azure 계정에 대 한 연결 문자열 aaaMongoDB | Microsoft Docs"
description: "어떻게 tooconnect MongoDB 앱 tooan Azure Cosmos DB는 MongoDB 연결 문자열을 사용 하 여을 계정에 대해 알아봅니다."
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
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a><span data-ttu-id="9a99c-104">MongoDB 응용 프로그램 tooAzure Cosmos DB에 연결</span><span class="sxs-lookup"><span data-stu-id="9a99c-104">Connect a MongoDB application tooAzure Cosmos DB</span></span>
<span data-ttu-id="9a99c-105">어떻게 tooconnect MongoDB 앱 tooan Azure Cosmos DB는 MongoDB 연결 문자열을 사용 하 여을 계정에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-105">Learn how tooconnect your MongoDB app tooan Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="9a99c-106">Azure Cosmos DB 데이터베이스 hello 데이터로 사용할 수 있습니다 MongoDB 앱에 대 한 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-106">You can then use an Azure Cosmos DB database as hello data store for your MongoDB app.</span></span> 

<span data-ttu-id="9a99c-107">이 자습서에서는 두 가지 방법으로 tooretrieve 연결 문자열 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-107">This tutorial provides two ways tooretrieve connection string information:</span></span>

- <span data-ttu-id="9a99c-108">[hello quick start 메서드](#QuickstartConnection),.NET, Node.js, MongoDB 셸, Java, 및 Python 드라이버와 함께 사용 하기 위해</span><span class="sxs-lookup"><span data-stu-id="9a99c-108">[hello quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="9a99c-109">[사용자 지정 연결 문자열 방법을 hello](#GetCustomConnection), 다른 드라이버와 함께 사용 하기 위해</span><span class="sxs-lookup"><span data-stu-id="9a99c-109">[hello custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a99c-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9a99c-110">Prerequisites</span></span>

- <span data-ttu-id="9a99c-111">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="9a99c-111">An Azure account.</span></span> <span data-ttu-id="9a99c-112">Azure 계정이 없으면 지금 [무료 Azure 계정](https://azure.microsoft.com/free/)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="9a99c-113">Azure Cosmos DB 계정.</span><span class="sxs-lookup"><span data-stu-id="9a99c-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="9a99c-114">자세한 내용은 [.net MongoDB API 웹 응용 프로그램을 빌드 및 Azure 포털 hello](create-mongodb-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-114">For instructions, see [Build a MongoDB API web app with .NET and hello Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="9a99c-115"><a id="QuickstartConnection"></a>빠른 시작 hello를 사용 하 여 hello MongoDB 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-115"><a id="QuickstartConnection"></a>Get hello MongoDB connection string by using hello quick start</span></span>
1. <span data-ttu-id="9a99c-116">인터넷 브라우저를 toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-116">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9a99c-117">Hello에 **Azure Cosmos DB** 블레이드에서 MongoDB 계정에 대 한 선택 hello API입니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-117">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="9a99c-118">Hello 계정 블레이드의 hello 왼쪽된 창에서 클릭 **퀵 스타트**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-118">In hello left pane of hello account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="9a99c-119">플랫폼(**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="9a99c-120">드라이버나 도구가 목록에 없더라도 계속해서 더 많은 연결 코드 조각을 문서화하므로 걱정하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="9a99c-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="9a99c-121">원하는에 아래 의견을 보내주세요. toosee 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-121">Please comment below on what you'd like toosee.</span></span> <span data-ttu-id="9a99c-122">toolearn 어떻게 toocraft 자체 연결 읽을 [hello 계정 연결 문자열 정보를 가져올](#GetCustomConnection)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-122">toolearn how toocraft your own connection, read [Get hello account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="9a99c-123">복사한 hello 코드 조각 MongoDB 앱에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-123">Copy and paste hello code snippet into your MongoDB app.</span></span>

    ![빠른 시작 블레이드](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="9a99c-125"><a id="GetCustomConnection"></a>Hello MongoDB 연결 문자열 toocustomize 가져오기</span><span class="sxs-lookup"><span data-stu-id="9a99c-125"><a id="GetCustomConnection"></a> Get hello MongoDB connection string toocustomize</span></span>
1. <span data-ttu-id="9a99c-126">인터넷 브라우저를 toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-126">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9a99c-127">Hello에 **Azure Cosmos DB** 블레이드에서 MongoDB 계정에 대 한 선택 hello API입니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-127">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="9a99c-128">Hello 계정 블레이드의 hello 왼쪽된 창에서 클릭 **연결 문자열**합니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-128">In hello left pane of hello account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="9a99c-129">hello **연결 문자열** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-129">hello **Connection String** blade opens.</span></span> <span data-ttu-id="9a99c-130">Preconstructed 연결 문자열을 포함 하 여 MongoDB에 대 한 드라이버를 사용 하 여 모든 hello 정보 필요한 tooconnect toohello 계정을에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-130">It has all hello information necessary tooconnect toohello account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![연결 문자열 블레이드](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="9a99c-132">연결 문자열 요구 사항</span><span class="sxs-lookup"><span data-stu-id="9a99c-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="9a99c-133">Azure Cosmos DB에는 엄격한 보안 요구 사항과 표준이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="9a99c-134">Azure Cosmos DB 계정에는 *SSL*을 통한 인증 및 보안 통신이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="9a99c-135">Azure Cosmos DB 지원 hello 표준 MongoDB 연결 문자열 URI 형식으로 두 가지 특정 요구 사항: Azure Cosmos DB 계정 인증 및 SSL 통해 보안 통신에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-135">Azure Cosmos DB supports hello standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="9a99c-136">따라서 hello 연결 문자열 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-136">So, hello connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="9a99c-137">이 문자열의 hello 값 hello에서 사용할 수 있는 **연결 문자열** 블레이드 앞에 표시 된:</span><span class="sxs-lookup"><span data-stu-id="9a99c-137">hello values of this string are available in hello **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="9a99c-138">Username(필수): Azure Cosmos DB 계정 이름</span><span class="sxs-lookup"><span data-stu-id="9a99c-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="9a99c-139">Password(필수): Azure Cosmos DB 계정 암호</span><span class="sxs-lookup"><span data-stu-id="9a99c-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="9a99c-140">호스트 (필수): hello Azure Cosmos DB 계정의 FQDN입니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-140">Host (required): FQDN of hello Azure Cosmos DB account.</span></span>
* <span data-ttu-id="9a99c-141">Port(필수): 10255</span><span class="sxs-lookup"><span data-stu-id="9a99c-141">Port (required): 10255.</span></span>
* <span data-ttu-id="9a99c-142">데이터베이스 (옵션): hello 데이터베이스 연결 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-142">Database (optional): hello database that hello connection uses.</span></span> <span data-ttu-id="9a99c-143">Hello 기본 데이터베이스 "test"가 없는 데이터베이스를 제공 하는 경우</span><span class="sxs-lookup"><span data-stu-id="9a99c-143">If no database is provided, hello default database is "test."</span></span>
* <span data-ttu-id="9a99c-144">ssl=true(필수)</span><span class="sxs-lookup"><span data-stu-id="9a99c-144">ssl=true (required)</span></span>

<span data-ttu-id="9a99c-145">예를 들어 hello에 표시 된 hello 계정 **연결 문자열** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-145">For example, consider hello account shown in hello **Connection String** blade.</span></span> <span data-ttu-id="9a99c-146">유효한 연결 문자열은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="9a99c-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9a99c-147">Next steps</span></span>
* <span data-ttu-id="9a99c-148">너무 방법에 대해 알아봅니다[MongoChef를 사용 하 여](mongodb-mongochef.md) MongoDB 계정에 대 한 Azure Cosmos DB API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-148">Learn how too[use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="9a99c-149">MongoDB에 대 한 확인 하 여 hello Azure Cosmos DB API를 탐색 [샘플](mongodb-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9a99c-149">Explore hello Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
