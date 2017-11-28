---
title: "Azure Cosmos DB: Xamarin 및 Facebook 인증으로 웹앱 작성 | Microsoft Docs"
description: "Tooconnect tooand에서는.NET 코드 샘플은 Azure Cosmos DB 쿼리를 표시."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a><span data-ttu-id="ec20c-103">Azure Cosmos DB: .NET, Xamarin 및 Facebook 인증으로 웹앱 작성</span><span class="sxs-lookup"><span data-stu-id="ec20c-103">Azure Cosmos DB: Build a web app with .NET, Xamarin, and Facebook authentication</span></span>

<span data-ttu-id="ec20c-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="ec20c-105">신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="ec20c-106">이 빠른 시작 toocreate Azure Cosmos DB 계정, 문서 데이터베이스 및 컬렉션 사용 하 여 Azure 포털을 hello 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="ec20c-107">그런 다음 빌드 하 고 hello 기반으로 할 일 목록 웹 앱을 배포 합니다 [DocumentDB.NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), 연산자 및 hello Azure Cosmos DB 권한 부여 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), and hello Azure Cosmos DB authorization engine.</span></span> <span data-ttu-id="ec20c-108">hello 할 일 목록 웹 앱 Facebook 인증을 사용 하 여 사용자가 toologin 수 있도록 하는 사용자 단위 데이터 패턴을 구현 하 고 자신의 toodo 항목을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-108">hello todo list web app implements a per-user data pattern that enables users toologin using Facebook Auth and manage their own toodo items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec20c-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ec20c-109">Prerequisites</span></span>

<span data-ttu-id="ec20c-110">설치 된 Visual Studio 2017 없는 경우 다운로드 하 고 hello를 사용 하 여 수 **무료** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="ec20c-111">사용할 수 있는지 확인 **Azure 개발** hello Visual Studio 설정 중입니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="ec20c-112">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="ec20c-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="ec20c-113">컬렉션 추가</span><span class="sxs-lookup"><span data-stu-id="ec20c-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="ec20c-114">Hello 샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="ec20c-114">Clone hello sample application</span></span>

<span data-ttu-id="ec20c-115">이제 github에서 복제는 DocumentDB API 앱 hello 연결 문자열을 설정 하 고 실행 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="ec20c-116">얼마나 쉬운지 데이터로 toowork 프로그래밍 방식으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-116">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="ec20c-117">예: git bash git 터미널 윈도우를 열고 및 `cd` tooa 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-117">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="ec20c-118">다음 명령은 tooclone hello 샘플 리포지토리 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. <span data-ttu-id="ec20c-119">Visual Studio에서 hello samples/xamarin/UserItems/xamarin.forms 폴더에서 다음 hello DocumentDBTodo.sln 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-119">Then open hello DocumentDBTodo.sln file from hello samples/xamarin/UserItems/xamarin.forms folder in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="ec20c-120">Hello 코드 검토</span><span class="sxs-lookup"><span data-stu-id="ec20c-120">Review hello code</span></span>

<span data-ttu-id="ec20c-121">hello 코드 hello Xamarin 폴더에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-121">hello code in hello Xamarin folder contains:</span></span>

* <span data-ttu-id="ec20c-122">Xamarin 앱.</span><span class="sxs-lookup"><span data-stu-id="ec20c-122">Xamarin app.</span></span> <span data-ttu-id="ec20c-123">hello 앱 UserItems 라는 분할 된 컬렉션에 hello 사용자의 할 일 항목을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-123">hello app stores hello user's todo items in a partitioned collection named UserItems.</span></span>
* <span data-ttu-id="ec20c-124">리소스 토큰 broker API.</span><span class="sxs-lookup"><span data-stu-id="ec20c-124">Resource token broker API.</span></span> <span data-ttu-id="ec20c-125">간단한 ASP.NET 웹 API toobroker Azure Cosmos DB 리소스 toohello hello 앱의 사용자는 로그인 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-125">A simple ASP.NET Web API toobroker Azure Cosmos DB resource tokens toohello logged in users of hello app.</span></span> <span data-ttu-id="ec20c-126">리소스 토큰은 사용자의 데이터에 기록 하는 hello 액세스 toohello 함께 hello 응용 프로그램을 제공 하는 수명이 짧은 액세스 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-126">Resource tokens are short-lived access tokens that provide hello app with hello access toohello logged in user's data.</span></span>

<span data-ttu-id="ec20c-127">아래 hello 다이어그램 hello 인증 및 데이터 흐름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-127">hello authentication and data flow is illustrated in hello diagram below.</span></span>

* <span data-ttu-id="ec20c-128">hello UserItems 컬렉션 hello 파티션 키를 사용 하 여 만든 ' / userid'.</span><span class="sxs-lookup"><span data-stu-id="ec20c-128">hello UserItems collection is created with hello partition key '/userid'.</span></span> <span data-ttu-id="ec20c-129">지정 된 컬렉션에 대 한 파티션 키 하면 Azure Cosmos DB tooscale 무한 hello 사용자와 항목 수로 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-129">Specifying a partition key for a collection allows Azure Cosmos DB tooscale infinitely as hello number of users and items grows.</span></span>
* <span data-ttu-id="ec20c-130">hello Xamarin 앱에 Facebook 자격 증명으로 사용자가 toologin을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-130">hello Xamarin app allows users toologin with Facebook credentials.</span></span>
* <span data-ttu-id="ec20c-131">hello Xamarin 앱에서 Facebook 액세스 토큰 tooauthenticate ResourceTokenBroker API 사용</span><span class="sxs-lookup"><span data-stu-id="ec20c-131">hello Xamarin app uses Facebook access token tooauthenticate with ResourceTokenBroker API</span></span>
* <span data-ttu-id="ec20c-132">hello 리소스 토큰 브로커 API 앱 서비스 인증 기능을 사용 하는 hello 요청을 인증 하 고 hello 인증 된 사용자의 파티션 키를 공유 하는 읽기/쓰기 액세스 tooall 문서와 함께 Azure Cosmos DB 리소스 토큰을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-132">hello resource token broker API authenticates hello request using App Service Auth feature, and requests an Azure Cosmos DB resource token with read/write access tooall documents sharing hello authenticated user's partition key.</span></span>
* <span data-ttu-id="ec20c-133">리소스 토큰 브로커 hello 리소스 토큰 toohello 클라이언트 응용 프로그램을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-133">Resource token broker returns hello resource token toohello client app.</span></span>
* <span data-ttu-id="ec20c-134">hello 앱 hello 리소스 토큰을 사용 하 여 hello 사용자의 할 일 항목에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-134">hello app accesses hello user's todo items using hello resource token.</span></span>

![샘플 데이터를 사용한 Todo 앱](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a><span data-ttu-id="ec20c-136">연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="ec20c-136">Update your connection string</span></span>

<span data-ttu-id="ec20c-137">이제 돌아가서 toohello Azure 포털 tooget 연결 문자열 정보를 hello 앱에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-137">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="ec20c-138">Hello에 [Azure 포털](http://portal.azure.com/), 프로그램 Azure Cosmos DB에에서 account, 왼쪽 탐색 hello 클릭 **키**, 클릭 하 고 **읽기-쓰기 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-138">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="ec20c-139">Hello 다음 단계에서 hello Web.config 파일로 hello 화면 toocopy hello URI의 hello 오른쪽에서 복사 단추 hello와 기본 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-139">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello Web.config file in hello next step.</span></span>

    ![표시 및 hello Azure 포털에에서 액세스 키, 키 블레이드에서 복사](./media/create-documentdb-xamarin-dotnet/keys.png)

2. <span data-ttu-id="ec20c-141">Visual Studio 2017에 hello azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker 폴더에 hello Web.config 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-141">In Visual Studio 2017, open hello Web.config file in hello azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folder.</span></span> 

3. <span data-ttu-id="ec20c-142">Hello 포털 (hello 복사 단추 사용)에서 URI 값을 복사 하 고 쉽게 hello hello accountUrl web.config에서의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-142">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello accountUrl in Web.config.</span></span> 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. <span data-ttu-id="ec20c-143">그런 다음 hello 포털에서 기본 키 값을 복사 하 고 쉽게 hello hello accountKey Web.congif에서의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-143">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello accountKey in Web.congif.</span></span> 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

<span data-ttu-id="ec20c-144">이제 앱을 업데이트 한 toocommunicate Azure Cosmos DB와 함께 필요한 모든 hello 정보 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-144">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-hello-web-app"></a><span data-ttu-id="ec20c-145">빌드 및 hello 웹 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="ec20c-145">Build and deploy hello web app</span></span>

1. <span data-ttu-id="ec20c-146">Hello Azure 포털, 한 앱 서비스 웹 사이트 toohost hello 리소스 토큰 브로커를 API를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-146">In hello Azure portal, create an App Service website toohost hello Resource token broker API.</span></span>
2. <span data-ttu-id="ec20c-147">Azure 포털 hello에 hello 리소스 토큰 브로커 API 웹 사이트의 hello 응용 프로그램 설정 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-147">In hello Azure portal, open hello App Settings blade of hello Resource token broker API website.</span></span> <span data-ttu-id="ec20c-148">앱 설정에 따라 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-148">Fill in hello following app settings:</span></span>

    * <span data-ttu-id="ec20c-149">accountUrl-hello Azure Cosmos DB 계정 키 탭에서 hello Azure Cosmos DB 계정 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-149">accountUrl - hello Azure Cosmos DB account URL from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="ec20c-150">accountKey-Azure Cosmos DB 계정 키 탭 hello에서에서 hello Azure Cosmos DB 계정 마스터 키입니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-150">accountKey - hello Azure Cosmos DB account master key from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="ec20c-151">사용자가 만든 데이터베이스와 컬렉션의 databaseId 및 collectionId</span><span class="sxs-lookup"><span data-stu-id="ec20c-151">databaseId and collectionId of your created database and collection</span></span>

3. <span data-ttu-id="ec20c-152">Hello ResourceTokenBroker 솔루션 tooyour 만든 웹 사이트를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-152">Publish hello ResourceTokenBroker solution tooyour created website.</span></span>

4. <span data-ttu-id="ec20c-153">Hello Xamarin 프로젝트를 열고 tooTodoItemManager.cs 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-153">Open hello Xamarin project, and navigate tooTodoItemManager.cs.</span></span> <span data-ttu-id="ec20c-154">Hello 리소스 토큰 브로커 웹 사이트에 대 한 hello 기본 https url로 resourceTokenBrokerURL 뿐만 아니라 accountURL, collectionId, databaseId에 대 한 hello 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-154">Fill in hello values for accountURL, collectionId, databaseId, as well as resourceTokenBrokerURL as hello base https url for hello resource token broker website.</span></span>

5. <span data-ttu-id="ec20c-155">전체 hello [어떻게 tooconfigure 앱 서비스 응용 프로그램 toouse Facebook 로그인](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) 자습서 toosetup Facebook 인증 hello ResourceTokenBroker 웹 사이트 및 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-155">Complete hello [How tooconfigure your App Service application toouse Facebook login](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) tutorial toosetup Facebook authentication and configure hello ResourceTokenBroker website.</span></span>

    <span data-ttu-id="ec20c-156">Hello Xamarin 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-156">Run hello Xamarin app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="ec20c-157">Sla hello Azure 포털에서에서 검토 하 고</span><span class="sxs-lookup"><span data-stu-id="ec20c-157">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="ec20c-158">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="ec20c-158">Clean up resources</span></span>

<span data-ttu-id="ec20c-159">것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제:</span><span class="sxs-lookup"><span data-stu-id="ec20c-159">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="ec20c-160">Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 다음 방금 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-160">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you just created.</span></span> 
2. <span data-ttu-id="ec20c-161">리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-161">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec20c-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ec20c-162">Next steps</span></span>

<span data-ttu-id="ec20c-163">이 빠른 시작에서 toocreate Azure Cosmos DB 계정을 hello 데이터 탐색기를 사용 하 여 컬렉션을 만들 및 빌드 및 Xamarin 앱을 배포 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-163">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="ec20c-164">이제 tooyour Cosmos DB 계정 추가 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ec20c-164">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="ec20c-165">Azure Cosmos DB로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="ec20c-165">Import data into Azure Cosmos DB</span></span>](import-data.md)
