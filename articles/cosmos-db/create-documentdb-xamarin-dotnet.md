---
title: "Azure Cosmos DB: Xamarin 및 Facebook 인증으로 웹앱 작성 | Microsoft Docs"
description: "Azure Cosmos DB에 연결 및 쿼리하는 데 사용할 수 있는 .NET 코드 샘플을 제시합니다."
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
ms.openlocfilehash: 4ea97c2aca6769843d0210ffeae6f95531a21f10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a><span data-ttu-id="3ef4f-103">Azure Cosmos DB: .NET, Xamarin 및 Facebook 인증으로 웹앱 작성</span><span class="sxs-lookup"><span data-stu-id="3ef4f-103">Azure Cosmos DB: Build a web app with .NET, Xamarin, and Facebook authentication</span></span>

<span data-ttu-id="3ef4f-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="3ef4f-105">Azure Cosmos DB의 핵심인 전역 배포 및 수평적 크기 조정 기능의 이점을 활용하여 문서, 키/값 및 그래프 데이터베이스를 빠르게 만들고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="3ef4f-106">이 빠른 시작에서는 Azure Portal을 사용하여 Azure Cosmos DB 계정, 문서 데이터베이스 및 컬렉션을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="3ef4f-107">그런 다음, [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/) 및 Azure Cosmos DB 인증 엔진에서 작성된 할일 목록 웹앱을 빌드 및 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-107">You'll then build and deploy a todo list web app built on the [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), and the Azure Cosmos DB authorization engine.</span></span> <span data-ttu-id="3ef4f-108">할일 목록 웹앱은 사용자가 Facebook 인증을 사용하여 로그인한 후 자신의 할일 항목을 관리할 수 있는 사용자별 데이터 패턴을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-108">The todo list web app implements a per-user data pattern that enables users to login using Facebook Auth and manage their own to do items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ef4f-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3ef4f-109">Prerequisites</span></span>

<span data-ttu-id="3ef4f-110">Visual Studio 2017이 아직 설치되지 않은 경우 **체험판** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)을 다운로드하고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="3ef4f-111">Visual Studio를 설정하는 동안 **Azure 개발**을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="3ef4f-112">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="3ef4f-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="3ef4f-113">컬렉션 추가</span><span class="sxs-lookup"><span data-stu-id="3ef4f-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="3ef4f-114">샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="3ef4f-114">Clone the sample application</span></span>

<span data-ttu-id="3ef4f-115">이제 github에서 DocumentDB API 앱을 복제하고 연결 문자열을 설정한 후 실행해 보도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-115">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="3ef4f-116">프로그래밍 방식으로 데이터를 사용하여 얼마나 쉽게 작업할 수 있는지 알게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-116">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="3ef4f-117">git bash와 같은 git 터미널 창을 열고 `cd`를 수행하여 작업 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-117">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="3ef4f-118">다음 명령을 실행하여 샘플 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-118">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. <span data-ttu-id="3ef4f-119">그런 다음, Visual Studio에서 samples/xamarin/UserItems/xamarin.forms 폴더의 DocumentDBTodo.sln 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-119">Then open the DocumentDBTodo.sln file from the samples/xamarin/UserItems/xamarin.forms folder in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="3ef4f-120">코드 검토</span><span class="sxs-lookup"><span data-stu-id="3ef4f-120">Review the code</span></span>

<span data-ttu-id="3ef4f-121">Xamarin 폴더의 코드에는 다음이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-121">The code in the Xamarin folder contains:</span></span>

* <span data-ttu-id="3ef4f-122">Xamarin 앱.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-122">Xamarin app.</span></span> <span data-ttu-id="3ef4f-123">이 앱은 UserItems라는 분할 컬렉션에 사용자의 할일 항목을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-123">The app stores the user's todo items in a partitioned collection named UserItems.</span></span>
* <span data-ttu-id="3ef4f-124">리소스 토큰 broker API.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-124">Resource token broker API.</span></span> <span data-ttu-id="3ef4f-125">앱에 로그인한 사용자에게 Azure Cosmos DB 리소스 토큰을 중개하는 간단한 ASP.NET Web API입니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-125">A simple ASP.NET Web API to broker Azure Cosmos DB resource tokens to the logged in users of the app.</span></span> <span data-ttu-id="3ef4f-126">리소스 토큰은 로그인한 사용자의 데이터에 액세스할 수 있는 앱을 제공하는 단기 액세스 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-126">Resource tokens are short-lived access tokens that provide the app with the access to the logged in user's data.</span></span>

<span data-ttu-id="3ef4f-127">아래 다이어그램에서는 인증 및 데이터 흐름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-127">The authentication and data flow is illustrated in the diagram below.</span></span>

* <span data-ttu-id="3ef4f-128">UserItems 컬렉션은 '/userid' 파티션 키를 사용하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-128">The UserItems collection is created with the partition key '/userid'.</span></span> <span data-ttu-id="3ef4f-129">컬렉션에 대한 파티션 키를 지정하면 사용자 및 항목 수가 증가함에 따라 Azure Cosmos DB를 무제한으로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-129">Specifying a partition key for a collection allows Azure Cosmos DB to scale infinitely as the number of users and items grows.</span></span>
* <span data-ttu-id="3ef4f-130">Xamarin 앱을 사용하면 사용자가 Facebook 자격 증명으로 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-130">The Xamarin app allows users to login with Facebook credentials.</span></span>
* <span data-ttu-id="3ef4f-131">Xamarin 앱은 Facebook 액세스 토큰을 사용하여 ResourceTokenBroker API를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-131">The Xamarin app uses Facebook access token to authenticate with ResourceTokenBroker API</span></span>
* <span data-ttu-id="3ef4f-132">리소스 토큰 broker API는 App Service 인증 기능을 사용하여 요청을 인증하고, 인증된 사용자의 파티션 키를 공유하는 모든 문서에 대해 읽기/쓰기 액세스를 수행할 수 있는 Azure Cosmos DB 리소스 토큰을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-132">The resource token broker API authenticates the request using App Service Auth feature, and requests an Azure Cosmos DB resource token with read/write access to all documents sharing the authenticated user's partition key.</span></span>
* <span data-ttu-id="3ef4f-133">리소스 토큰 broker는 클라이언트 앱에 리소스 토큰을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-133">Resource token broker returns the resource token to the client app.</span></span>
* <span data-ttu-id="3ef4f-134">앱은 리소스 토큰을 사용하여 사용자의 할일 항목에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-134">The app accesses the user's todo items using the resource token.</span></span>

![샘플 데이터를 사용한 Todo 앱](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a><span data-ttu-id="3ef4f-136">연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="3ef4f-136">Update your connection string</span></span>

<span data-ttu-id="3ef4f-137">이제 Azure Portal로 다시 이동하여 연결 문자열 정보를 가져와서 앱에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-137">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="3ef4f-138">[Azure Portal](http://portal.azure.com/)의 Azure Cosmos DB 계정에서 왼쪽 탐색 창의 **키**를 클릭한 다음 **읽기-쓰기 키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-138">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="3ef4f-139">다음 단계에서 화면 오른쪽의 복사 단추를 사용하여 URI 및 기본 키를 Web.config 파일에 복사하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-139">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the Web.config file in the next step.</span></span>

    ![Azure Portal에서 선택 키 보기 및 복사, 키 블레이드](./media/create-documentdb-xamarin-dotnet/keys.png)

2. <span data-ttu-id="3ef4f-141">Visual Studio 2017에서 azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker 폴더의 Web.config 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-141">In Visual Studio 2017, open the Web.config file in the azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folder.</span></span> 

3. <span data-ttu-id="3ef4f-142">포털에서 URI 값을 복사(복사 단추 사용)한 후 이 값을 Web.config에서 accountUrl 값으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-142">Copy your URI value from the portal (using the copy button) and make it the value of the accountUrl in Web.config.</span></span> 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. <span data-ttu-id="3ef4f-143">그 다음, 포털에서 사용자의 기본 키 값을 복사한 후 Web.config에서 accountKey 값으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-143">Then copy your PRIMARY KEY value from the portal and make it the value of the accountKey in Web.congif.</span></span> 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

<span data-ttu-id="3ef4f-144">이제 Azure Cosmos DB와 통신하는 데 필요한 모든 정보로 앱이 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-144">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-the-web-app"></a><span data-ttu-id="3ef4f-145">웹앱 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="3ef4f-145">Build and deploy the web app</span></span>

1. <span data-ttu-id="3ef4f-146">Azure Portal에서 리소스 토큰 broker API를 호스트하는 App Service 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-146">In the Azure portal, create an App Service website to host the Resource token broker API.</span></span>
2. <span data-ttu-id="3ef4f-147">Azure Portal에서 리소스 토큰 broker API 웹 사이트의 앱 설정 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-147">In the Azure portal, open the App Settings blade of the Resource token broker API website.</span></span> <span data-ttu-id="3ef4f-148">다음 앱 설정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-148">Fill in the following app settings:</span></span>

    * <span data-ttu-id="3ef4f-149">accountUrl - Azure Cosmos DB 계정의 키 탭의 Azure Cosmos DB 계정 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-149">accountUrl - The Azure Cosmos DB account URL from the Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="3ef4f-150">accountKey - Azure Cosmos DB 계정의 키 탭의 Azure Cosmos DB 계정 마스터 키입니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-150">accountKey - The Azure Cosmos DB account master key from the Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="3ef4f-151">사용자가 만든 데이터베이스와 컬렉션의 databaseId 및 collectionId</span><span class="sxs-lookup"><span data-stu-id="3ef4f-151">databaseId and collectionId of your created database and collection</span></span>

3. <span data-ttu-id="3ef4f-152">생성된 웹 사이트에 ResourceTokenBroker 솔루션을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-152">Publish the ResourceTokenBroker solution to your created website.</span></span>

4. <span data-ttu-id="3ef4f-153">Xamarin 프로젝트를 열고 TodoItemManager.cs로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-153">Open the Xamarin project, and navigate to TodoItemManager.cs.</span></span> <span data-ttu-id="3ef4f-154">리소스 토큰 broker 웹 사이트에 대한 기본 https URL로 resourceTokenBrokerURL을 입력하고 accountURL, collectionId, databaseId에 대한 값도 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-154">Fill in the values for accountURL, collectionId, databaseId, as well as resourceTokenBrokerURL as the base https url for the resource token broker website.</span></span>

5. <span data-ttu-id="3ef4f-155">Facebook 인증을 설정하고 ResourceTokenBroker 웹 사이트를 구성하려면 [Facebook 로그인을 사용하도록 App Service 응용 프로그램을 구성하는 방법](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) 자습서를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-155">Complete the [How to configure your App Service application to use Facebook login](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) tutorial to setup Facebook authentication and configure the ResourceTokenBroker website.</span></span>

    <span data-ttu-id="3ef4f-156">Xamarin 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-156">Run the Xamarin app.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="3ef4f-157">Azure Portal에서 SLA 검토</span><span class="sxs-lookup"><span data-stu-id="3ef4f-157">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="3ef4f-158">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="3ef4f-158">Clean up resources</span></span>

<span data-ttu-id="3ef4f-159">이 앱을 계속 사용하지 않으려면 Azure Portal에서 다음 단계에 따라 이 빠른 시작에서 만든 리소스를 모두 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-159">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span> 

1. <span data-ttu-id="3ef4f-160">Azure Portal의 왼쪽 메뉴에서 **리소스 그룹**을 클릭한 다음, 방금 만든 리소스의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-160">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you just created.</span></span> 
2. <span data-ttu-id="3ef4f-161">리소스 그룹 페이지에서 **삭제**를 클릭하고 텍스트 상자에서 삭제할 리소스의 이름을 입력한 다음 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-161">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ef4f-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3ef4f-162">Next steps</span></span>

<span data-ttu-id="3ef4f-163">이 빠른 시작에서, Azure Cosmos DB 계정을 만들고, 데이터 탐색기를 사용하여 컬렉션을 만들고, Xamarin 앱을 작성 및 배포하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-163">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="3ef4f-164">이제 사용자의 Cosmos DB 계정에 추가 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ef4f-164">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ef4f-165">Azure Cosmos DB로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="3ef4f-165">Import data into Azure Cosmos DB</span></span>](import-data.md)
