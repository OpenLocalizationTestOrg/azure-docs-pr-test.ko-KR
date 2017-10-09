---
<span data-ttu-id="3abdb-101">제목: aaa "Azure Cosmos DB: Golang 여 MongoDB API 콘솔 응용 프로그램을 빌드하고 hello Azure 포털 | Microsoft Docs "설명: tooconnect tooand를 사용할 수 있는 Golang 코드 샘플에는 서비스에서 Azure Cosmos DB 쿼리 표시: cosmos db 작성자: Durgaprasad Budhwani 관리자: jhubbard 편집기: mimig1</span><span class="sxs-lookup"><span data-stu-id="3abdb-101">title: aaa"Azure Cosmos DB: Build a MongoDB API console app with Golang and hello Azure portal | Microsoft Docs" description: Presents a Golang code sample you can use tooconnect tooand query Azure Cosmos DB services: cosmos-db author: Durgaprasad-Budhwani manager: jhubbard editor: mimig1</span></span>

<span data-ttu-id="3abdb-102">ms.service: cosmos db ms.topic: 문서 hero ms.date: 07/21/2017 ms.author: mimig</span><span class="sxs-lookup"><span data-stu-id="3abdb-102">ms.service: cosmos-db ms.topic: hero-article ms.date: 07/21/2017 ms.author: mimig</span></span>
---

# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-hello-azure-portal"></a><span data-ttu-id="3abdb-103">Azure Cosmos DB: Golang 여 MongoDB API 콘솔 응용 프로그램을 빌드하고 hello Azure 포털</span><span class="sxs-lookup"><span data-stu-id="3abdb-103">Azure Cosmos DB: Build a MongoDB API console app with Golang and hello Azure portal</span></span>

<span data-ttu-id="3abdb-104">Azure Cosmos DB는 전 세계에 배포된 Microsoft의 다중 모델 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="3abdb-105">신속 하 게 만들기 및 문서, 키/값 및 hello 글로벌 배포 및 수평 확장이 기능 Cosmos DB Azure의 hello 핵심에에서 활용 중 일부는 그래프 데이터베이스를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="3abdb-106">이 빠른 시작에서는 방법을 기존 toouse [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) 로 작성 된 응용 [Golang](https://golang.org/) MongoDB 클라이언트 연결을 지 원하는 tooyour Azure Cosmos DB 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-106">This quick-start demonstrates how toouse an existing [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) app written in [Golang](https://golang.org/) and connect it tooyour Azure Cosmos DB database, which supports MongoDB client connections.</span></span>

<span data-ttu-id="3abdb-107">즉, Golang 응용 프로그램 연결 하는 MongoDB Api를 사용 하 여 tooa 데이터베이스만 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-107">In other words, your Golang application only knows that it's connecting tooa database using MongoDB APIs.</span></span> <span data-ttu-id="3abdb-108">투명 데이터 hello toohello 응용 Azure Cosmos DB에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-108">It is transparent toohello application that hello data is stored in Azure Cosmos DB.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3abdb-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3abdb-109">Prerequisites</span></span>

- <span data-ttu-id="3abdb-110">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="3abdb-110">An Azure subscription.</span></span> <span data-ttu-id="3abdb-111">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-111">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free) before you begin.</span></span>
- <span data-ttu-id="3abdb-112">[이동](https://golang.org/dl/) 및 hello에 대 한 기본 지식이 [이동](https://golang.org/) 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-112">[Go](https://golang.org/dl/) and a basic knowledge of hello [Go](https://golang.org/) language.</span></span>
- <span data-ttu-id="3abdb-113">Jetbrains의 [Gogland](https://www.jetbrains.com/go/), Microsoft의 [Visual Studio Code](https://code.visualstudio.com/) 또는 [Atom](https://atom.io/)과 같은 IDE입니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-113">An IDE — [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span> <span data-ttu-id="3abdb-114">이 자습서에서는 Goglang을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-114">In this tutorial, I'm using Goglang.</span></span>

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="3abdb-115">데이터베이스 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="3abdb-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="3abdb-116">Hello 샘플 응용 프로그램 복제</span><span class="sxs-lookup"><span data-stu-id="3abdb-116">Clone hello sample application</span></span>

<span data-ttu-id="3abdb-117">Hello 샘플 응용 프로그램을 복제 하 고 hello 필요한 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-117">Clone hello sample application and install hello required packages.</span></span>

1. <span data-ttu-id="3abdb-118">기본적으로 C:\Go\ 된 hello GOROOT\src 폴더 안에 CosmosDBSample 라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-118">Create a folder named CosmosDBSample inside hello GOROOT\src folder, which is C:\Go\ by default.</span></span>
2. <span data-ttu-id="3abdb-119">Hello 다음 git 터미널 윈도우를 사용 하 여 hello CosmosDBSample 폴더로 git bash tooclone hello 샘플 저장소와 같은 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-119">Run hello following command using a git terminal window such as git bash tooclone hello sample repository into hello CosmosDBSample folder.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  <span data-ttu-id="3abdb-120">다음 명령은 tooget hello mgo 패키지 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-120">Run hello following command tooget hello mgo package.</span></span> 

    ```
    go get gopkg.in/mgo.v2
    ```

<span data-ttu-id="3abdb-121">hello [mgo](http://labix.org/mgo) 드라이버 (으로 발음 *mango*)은 한 [MongoDB](http://www.mongodb.org/) hello에 대 한 드라이버 [언어 이동](http://golang.org/) rich를 구현 하 고 제대로 테스트 선택 영역에서 표준 Go 관용구를 수행 하는 매우 간단한 API 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-121">hello [mgo](http://labix.org/mgo) driver (pronounced as *mango*) is a [MongoDB](http://www.mongodb.org/) driver for hello [Go language](http://golang.org/) that implements a rich and well tested selection of features under a very simple API following standard Go idioms.</span></span>

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a><span data-ttu-id="3abdb-122">연결 문자열 업데이트</span><span class="sxs-lookup"><span data-stu-id="3abdb-122">Update your connection string</span></span>

<span data-ttu-id="3abdb-123">이제 돌아가서 toohello Azure 포털 tooget 연결 문자열 정보를 hello 앱에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-123">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="3abdb-124">클릭 **빠른 시작** 왼쪽된 탐색 메뉴 hello와 클릭 **다른** hello Go 응용 프로그램에 필요한 tooview hello 연결 문자열 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-124">Click **Quick start** in hello left navigation menu, and then click **Other** tooview hello connection string information required by hello Go application.</span></span>

2. <span data-ttu-id="3abdb-125">Goglang, hello GOROOT\CosmosDBSample 디렉터리에 hello main.go 파일 열고 hello 스크린 샷 다음 그림과 같이 hello Azure 포털에서에서 hello 연결 문자열 정보를 사용 하 여 코드의 줄을 다음 hello를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-125">In Goglang, open hello main.go file in hello GOROOT\CosmosDBSample directory and update hello following lines of code using hello connection string information from hello Azure portal as shown in hello following screenshot.</span></span> 

    <span data-ttu-id="3abdb-126">hello 데이터베이스 이름이 hello의 hello 접두사인 **호스트** hello Azure 포털 연결 문자열 창에는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-126">hello Database name is hello prefix of hello **Host** value in hello Azure portal connection string pane.</span></span> <span data-ttu-id="3abdb-127">Hello 이미지 아래에 표시 된 hello 계정에 대 한 hello 데이터베이스 이름은 golang 코치입니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-127">For hello account shown in hello image below, hello Database name is golang-coach.</span></span>

    ```go
    Database: "hello prefix of hello Host value in hello Azure portal",
    Username: "hello Username in hello Azure portal",
    Password: "hello Password in hello Azure portal",
    ```

    ![빠른 시작 창에서 기타 hello Azure 포털 보여 주는 hello 연결 문자열 정보 탭](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. <span data-ttu-id="3abdb-129">Hello main.go 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-129">Save hello main.go file.</span></span>

## <a name="review-hello-code"></a><span data-ttu-id="3abdb-130">Hello 코드 검토</span><span class="sxs-lookup"><span data-stu-id="3abdb-130">Review hello code</span></span>

<span data-ttu-id="3abdb-131">Hello main.go 파일에서 일어나는 빠르게 검토를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-131">Let's make a quick review of what's happening in hello main.go file.</span></span> 

### <a name="connecting-hello-go-app-tooazure-cosmos-db"></a><span data-ttu-id="3abdb-132">Hello Go 앱 tooAzure Cosmos DB에 연결</span><span class="sxs-lookup"><span data-stu-id="3abdb-132">Connecting hello Go app tooAzure Cosmos DB</span></span>

<span data-ttu-id="3abdb-133">Azure Cosmos DB hello MongoDB SSL 사용을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-133">Azure Cosmos DB supports hello SSL-enabled MongoDB.</span></span> <span data-ttu-id="3abdb-134">tooconnect tooan MongoDB SSL 사용 가능 해야 toodefine hello **DialServer** 함수 [mgo 합니다. DialInfo](http://gopkg.in/mgo.v2#DialInfo), 확인 하 고 hello 활용 [tls. *전화* ](http://golang.org/pkg/crypto/tls#Dial) tooperform hello 연결 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-134">tooconnect tooan SSL-enabled MongoDB, you need toodefine hello **DialServer** function in [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo), and make use of hello [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) function tooperform hello connection.</span></span>

<span data-ttu-id="3abdb-135">다음 코드 조각 Golang hello Azure Cosmos DB MongoDB api hello Go 응용 프로그램을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-135">hello following Golang code snippet connects hello Go app with Azure Cosmos DB MongoDB API.</span></span> <span data-ttu-id="3abdb-136">hello *DialInfo* MongoDB 클러스터와의 세션을 설정 하기 위한 옵션을 포함 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-136">hello *DialInfo* class holds options for establishing a session with a MongoDB cluster.</span></span>

```go
// DialInfo holds options for establishing a session with a MongoDB cluster.
dialInfo := &mgo.DialInfo{
    Addrs:    []string{"golang-couch.documents.azure.com:10255"}, // Get HOST + PORT
    Timeout:  60 * time.Second,
    Database: "database", // It can be anything
    Username: "username", // Username
    Password: "Azure database connect password from Azure Portal", // PASSWORD
    DialServer: func(addr *mgo.ServerAddr) (net.Conn, error) {
        return tls.Dial("tcp", addr.String(), &tls.Config{})
    },
}

// Create a session which maintains a pool of socket connections
// tooour Azure Cosmos DB MongoDB database.
session, err := mgo.DialWithInfo(dialInfo)

if err != nil {
    fmt.Printf("Can't connect toomongo, go error %v\n", err)
    os.Exit(1)
}

defer session.Close()

// SetSafe changes hello session safety mode.
// If hello safe parameter is nil, hello session is put in unsafe mode, 
// and writes become fire-and-forget,
// without error checking. hello unsafe mode is faster since operations won't hold on waiting for a confirmation.
// 
session.SetSafe(&mgo.Safe{})
```

<span data-ttu-id="3abdb-137">hello **mgo 합니다. Dial()** 메서드 SSL 연결이 없을 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-137">hello **mgo.Dial()** method is used when there is no SSL connection.</span></span> <span data-ttu-id="3abdb-138">SSL 연결에 대 한 hello **mgo 합니다. DialWithInfo()** 방법이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-138">For an SSL connection, hello **mgo.DialWithInfo()** method is required.</span></span>

<span data-ttu-id="3abdb-139">Hello 인스턴스의 **DialWIthInfo {}** 개체는 사용 되는 toocreate hello 세션 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-139">An instance of hello **DialWIthInfo{}** object is used toocreate hello session object.</span></span> <span data-ttu-id="3abdb-140">Hello 세션이 구성 되 면 다음 코드 조각 hello를 사용 하 여 hello 컬렉션을 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-140">Once hello session is established, you can access hello collection by using hello following code snippet:</span></span>

```go
collection := session.DB(“database”).C(“package”)
```

<a id="create-document"></a>

### <a name="create-a-document"></a><span data-ttu-id="3abdb-141">문서 만들기</span><span class="sxs-lookup"><span data-stu-id="3abdb-141">Create a document</span></span>

```go
// Model
type Package struct {
    Id bson.ObjectId  `bson:"_id,omitempty"`
    FullName      string
    Description   string
    StarsCount    int
    ForksCount    int
    LastUpdatedBy string
}

// insert Document in collection
err = collection.Insert(&Package{
    FullName:"react",
    Description:"A framework for building native apps with React.",
    ForksCount: 11392,
    StarsCount:48794,
    LastUpdatedBy:"shergin",

})

if err != nil {
    log.Fatal("Problem inserting data: ", err)
    return
}
```

### <a name="query-or-read-a-document"></a><span data-ttu-id="3abdb-142">문서 쿼리 또는 읽기</span><span class="sxs-lookup"><span data-stu-id="3abdb-142">Query or read a document</span></span>

<span data-ttu-id="3abdb-143">Azure Cosmos DB는 각 컬렉션에 저장된 JSON 문서에 대해 다양한 쿼리를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-143">Azure Cosmos DB supports rich queries against JSON documents stored in each collection.</span></span> <span data-ttu-id="3abdb-144">hello 다음 샘플 코드는 쿼리를 보여 줍니다 컬렉션에 hello 문서에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-144">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

```go
// Get a Document from hello collection
result := Package{}
err = collection.Find(bson.M{"fullname": "react"}).One(&result)
if err != nil {
    log.Fatal("Error finding record: ", err)
    return
}

fmt.Println("Description:", result.Description)
```


### <a name="update-a-document"></a><span data-ttu-id="3abdb-145">문서 업데이트</span><span class="sxs-lookup"><span data-stu-id="3abdb-145">Update a document</span></span>

```go
// Update a document
updateQuery := bson.M{"_id": result.Id}
change := bson.M{"$set": bson.M{"fullname": "react-native"}}
err = collection.Update(updateQuery, change)
if err != nil {
    log.Fatal("Error updating record: ", err)
    return
}
```

### <a name="delete-a-document"></a><span data-ttu-id="3abdb-146">문서 삭제</span><span class="sxs-lookup"><span data-stu-id="3abdb-146">Delete a document</span></span>

<span data-ttu-id="3abdb-147">Azure Cosmos DB는 JSON 문서 삭제를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-147">Azure Cosmos DB supports deleting JSON documents.</span></span>

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-hello-app"></a><span data-ttu-id="3abdb-148">Hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="3abdb-148">Run hello app</span></span>

1. <span data-ttu-id="3abdb-149">Goglang, 확인 하 여 GOPATH (아래에서 사용 가능한 **파일**, **설정**, **이동**, **GOPATH**) hello 위치는 hello에 포함 gopkg 되었습니다, USERPROFILE\go은 기본적으로 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-149">In Goglang, ensure that your GOPATH (available under **File**, **Settings**, **Go**, **GOPATH**) include hello location in which hello gopkg was installed, which is USERPROFILE\go by default.</span></span> 
2. <span data-ttu-id="3abdb-150">줄 주석 처리 hello hello 문서를 91-96 줄을 삭제 하는 실행 중인 hello 앱 후 hello 문서를 볼 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-150">Comment out hello lines that delete hello document, lines 91-96, so that you can see hello document after running hello app.</span></span>
3. <span data-ttu-id="3abdb-151">Goglang에서 **실행**을 클릭한 후 **'main.go 빌드 및 실행' 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-151">In Goglang, click **Run**, and then click **Run 'Build main.go and run'**.</span></span>

    <span data-ttu-id="3abdb-152">hello 앱 완료 되 고 hello에서 만든 hello 문서에 대 한 설명을 표시 [문서 만들기](#create-document)합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-152">hello app finishes and displays hello description of hello document created in [Create a document](#create-document).</span></span>
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![Goglang hello 응용 프로그램의 hello 출력 표시](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a><span data-ttu-id="3abdb-154">데이터 탐색기에서 문서 검토</span><span class="sxs-lookup"><span data-stu-id="3abdb-154">Review your document in Data Explorer</span></span>

<span data-ttu-id="3abdb-155">이동 다시 Azure 포털 toosee toohello 데이터 탐색기에서 문서.</span><span class="sxs-lookup"><span data-stu-id="3abdb-155">Go back toohello Azure portal toosee your document in Data Explorer.</span></span>

1. <span data-ttu-id="3abdb-156">클릭 **데이터 탐색기 (미리 보기)** hello 왼쪽된 탐색 메뉴에서 확장 **golang 코치**, **패키지**, 클릭 하 고 **문서**합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-156">Click **Data Explorer (Preview)** in hello left navigation menu, expand **golang-coach**, **package**, and then click **Documents**.</span></span> <span data-ttu-id="3abdb-157">Hello에 **문서** 탭에서 hello \_hello 오른쪽 창에서 id toodisplay hello 문서.</span><span class="sxs-lookup"><span data-stu-id="3abdb-157">In hello **Documents** tab, click hello \_id toodisplay hello document in hello right pane.</span></span> 

    ![데이터 탐색기 표시 된 새로 만든 hello 문서](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. <span data-ttu-id="3abdb-159">다음을 작업 영역을 hello 문서 인라인 클릭 **업데이트** toosave 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-159">You can then work with hello document inline and click **Update** toosave it.</span></span> <span data-ttu-id="3abdb-160">또한 hello 문서를 삭제 하거나 새 문서 또는 쿼리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-160">You can also delete hello document, or create new documents or queries.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="3abdb-161">Sla hello Azure 포털에서에서 검토 하 고</span><span class="sxs-lookup"><span data-stu-id="3abdb-161">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="3abdb-162">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="3abdb-162">Clean up resources</span></span>

<span data-ttu-id="3abdb-163">것 toocontinue toouse이 응용이 프로그램을 만들이 빠른 시작 하 여 hello Azure 포털에서에서 단계를 수행 하는 hello로 리소스를 모두 삭제:</span><span class="sxs-lookup"><span data-stu-id="3abdb-163">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="3abdb-164">Hello Azure 포털에서에서 왼쪽 메뉴 hello에서에서 클릭 **리소스 그룹** 만든 hello 리소스의 hello 이름을 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-164">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="3abdb-165">리소스 그룹 페이지에서 클릭 **삭제**hello 텍스트 상자에 hello 리소스 toodelete의 hello 이름을 입력 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-165">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3abdb-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3abdb-166">Next steps</span></span>

<span data-ttu-id="3abdb-167">이 퀵 스타트의 어떻게 toocreate Azure Cosmos DB 계정 및 실행을 사용 하 여 Golang 앱 hello API MongoDB에 대 한 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-167">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a Golang app using hello API for MongoDB.</span></span> <span data-ttu-id="3abdb-168">이제 tooyour Cosmos DB 계정 추가 데이터를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3abdb-168">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="3abdb-169">Hello MongoDB API에 대 한 Azure Cosmos DB로 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="3abdb-169">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)
