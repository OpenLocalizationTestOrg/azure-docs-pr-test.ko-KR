---
title: "Azure Cosmos DB: DocumentDB API .NET Core 시작 자습서 | Microsoft Docs"
description: "트 온라인 데이터베이스와 C# 콘솔 응용 프로그램 hello Azure Cosmos DB DocumentDB API.NET Core SDK를 사용 하 여 생성 하는 자습서입니다."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: jhubbard
editor: 
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 5e7efb327252e9e73e9b2a340820eeecc6937fa5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a>Azure Cosmos DB: hello DocumentDB API 및.NET Core 시작
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [MongoDB용 Node.js](mongodb-samples.md)
> * [Node.JS](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

.NET Core 자습서와 함께 시작 하는 Azure Cosmos DB 용 toohello DocumentDB API를 시작! 이 자습서를 따라 하면 Azure Cosmos DB 리소스를 만들고 쿼리하는 콘솔 응용 프로그램이 생깁니다.

다음에 대해 설명합니다.

* 만들기 및 tooan Azure Cosmos DB 계정 연결
* Visual Studio 솔루션 구성
* 온라인 데이터베이스 만들기
* 컬렉션 만들기
* JSON 문서 만들기
* Hello 컬렉션 쿼리
* 문서 바꾸기
* 문서 삭제
* Hello 데이터베이스 삭제

시간이 없으십니까? 염려하지 마십시오. hello 완벽 한 솔루션에 있는 [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started)합니다. Toohello 점프 [hello 완벽 한 솔루션 섹션 가져오기](#GetSolution) 빠른 지침에 대 한 합니다.

Xamarin iOS, Android 또는 Forms toobuild 원하는 DocumentDB API 및.NET Core SDK hello를 사용 하 여 응용 프로그램? [Xamarin 및 Azure Cosmos DB를 사용하여 모바일 응용 프로그램 빌드](mobile-apps-with-xamarin.md)를 참조하세요.

> [!NOTE]
> 이 자습서에 사용 된 Azure Cosmos DB.NET Core SDK hello 유니버설 Windows 플랫폼 (UWP) 앱과 호환 되지 않습니다. Hello UWP 앱에서는.NET Core SDK의 미리 보기 버전에 대 한 전자 메일을 너무 보내기[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com)합니다.

이제 시작하겠습니다.

## <a name="prerequisites"></a>필수 조건
Hello 다음 항목이 있는지 확인 하십시오.

* 활성 Azure 계정. 계정이 없는 경우 [무료 계정](https://azure.microsoft.com/free/)에 등록할 수 있습니다. 
    * Hello 또는 사용할 수 있습니다 [Azure Cosmos DB 에뮬레이터](local-emulator.md) 이 자습서에 대 한 합니다.
* [Visual Studio 2017](https://www.visualstudio.com/vs/) 
    * Hello를 설치 하 여 hello 명령줄에서.NET Core 응용 프로그램을 개발할 수 MacOS 또는 Linux에서 작업할 경우 [.NET Core SDK](https://www.microsoft.com/net/core#macos) 선택한 hello 플랫폼에 대 한 합니다. 
    * Windows에서 작업할 경우 hello를 설치 하 여 hello 명령줄에서.NET Core 응용 프로그램을 개발할 수 있습니다 [.NET Core SDK](https://www.microsoft.com/net/core#windows)합니다. 
    * 자체 편집기를 사용하거나 Windows, Linux, MacOS에서 작동하는 무료 [Visual Studio Code](https://code.visualstudio.com/)를 다운로드할 수 있습니다. 

## <a name="step-1-create-an-azure-cosmos-db-account"></a>1단계: Azure Cosmos DB 계정 만들기
Azure Cosmos DB 계정을 만들어 보겠습니다. Toouse 원하는 계정을 이미 있는 경우 건너뛰어도 너무[Visual Studio 솔루션에 설치](#SetupVS)합니다. Hello Azure Cosmos DB 에뮬레이터를 사용 하는 경우 hello 단계에 따르십시오 [Azure Cosmos DB 에뮬레이터](local-emulator.md) toosetup 에뮬레이터 hello 및 너무 건너 뛸[Visual Studio 솔루션에 설치](#SetupVS)합니다.

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>2단계: Visual Studio 솔루션 설치
1. 컴퓨터에서 **Visual Studio 2017**을 엽니다.
2. Hello에 **파일** 메뉴 선택 **새로**를 선택한 후 **프로젝트**합니다.
3. Hello에 **새 프로젝트** 대화 상자에서 **템플릿** / **Visual C#** / **.NET Core** / **콘솔 응용 프로그램 (.NET Core)**, 프로젝트 이름을 **DocumentDBGettingStarted**, 클릭 하 고 **확인**합니다.

   ![새 프로젝트 창 hello 스크린 샷](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **DocumentDBGettingStarted**합니다.
5. 를 닫지 않고도 hello 메뉴를 클릭 **NuGet 패키지 관리...** .

   ![Hello 오른쪽 hello 프로젝트에 대 한 Clicked 메뉴를 스크린샷](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. Hello에 **NuGet** 탭을 클릭 **찾아보기** hello 창과 종류의 hello 위쪽 **azure documentdb** hello 검색 상자에 있습니다.
7. Hello 결과 내 찾을 **Microsoft.Azure.DocumentDB.Core** 클릭 **설치**합니다.
   .NET Core 용 클라이언트 라이브러리를 DocumentDB hello에 대 한 hello 패키지 ID가 [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core)합니다. 이 .NET Core NuGet 패키지에서 지원되지 않는 .NET Framework 버전(예: net461)을 대상으로 하는 경우 .NET Framework 4.5 이후의 모든 .NET Framework 버전을 지원하는 [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB)를 사용합니다.
8. Hello 메시지에 hello NuGet 패키지 설치 및 hello 사용권 계약에 동의 합니다.

잘하셨습니다. Hello 설치를 완료 했으므로 일부 코드 작성 시작 하겠습니다. [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started)에서 이 자습서의 완성된 코드 프로젝트를 찾을 수 있습니다.

## <a id="Connect"></a>3 단계: tooan Cosmos DB Azure 계정을 연결 하세요.
먼저,이 추가 응용 프로그램의 C# hello Program.cs 파일에 toohello 시작 부분을 참조 합니다.

```csharp
using System;

// ADD THIS PART tooYOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> 주문 toocomplete이이 자습서에서 위의 hello 종속성을 추가 해야 합니다.

이제, 두 가지 상수와 *클라이언트* 변수를 공용 클래스 *프로그램* 아래에 추가합니다.

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

다음으로 toohello head [Azure 포털](https://portal.azure.com) tooretrieve URI 및 기본 키입니다. hello Azure Cosmos DB URI 및 기본 키가 응용 프로그램 toounderstand에 필요한 위치 tooconnect 되며, Azure Cosmos DB tootrust에 대 한 응용 프로그램의 연결 합니다.

에 Azure 포털 hello, tooyour Azure Cosmos DB 계정을 탐색 한 다음 클릭 **키**합니다.

Hello 포털에서 hello URI를 복사 하 고 붙여 넣습니다 `<your endpoint URI>` hello program.cs 파일에 있습니다. 그러면 복사본 hello 포털에서 기본 키를 hello에 붙여 넣습니다 `<your key>`합니다. Hello Azure Cosmos DB 에뮬레이터를 사용 하는 경우 사용 하 여 `https://localhost:8081` hello 끝점 및에서 hello 잘 정의 된 인증 키로 [어떻게 Azure Cosmos DB 에뮬레이터 hello toodevelop를 사용 하 여](local-emulator.md)합니다. 확인 되었는지 tooremove hello < 및 > hello 끝점과 키 앞뒤에 큰따옴표를 둡니다.

![Azure 포털 hello NoSQL 자습서 toocreate C# 콘솔 응용 프로그램에서 사용 하는 hello 스크린 샷 계정에 강조 표시 하는 hello 활성 허브 hello 키 단추가 hello Azure Cosmos DB 계정 블레이드에서 강조 표시 및 hello URI, 기본 키 및 보조 키 값에 강조 표시 된 hello 키 블레이드에서 Azure Cosmos DB를 보여 줍니다.][keys]

Hello의 새 인스턴스를 만들어 hello 가져오는 시작된 응용 프로그램 시작 하겠습니다 **DocumentClient**합니다.

Hello 아래 **Main** 메서드를이 비동기 작업 호출 추가 **GetStartedDemo**는 새 우리의 인스턴스화하고 **DocumentClient**합니다.

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART tooYOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

Hello 다음 코드 toorun에서 해당 비동기 작업을 추가 하면 **Main** 메서드. hello **Main** 메서드 예외를 catch 하 고 toohello 콘솔에 씁니다.

```csharp
static void Main(string[] args)
{
        // ADD THIS PART tooYOUR CODE
        try
        {
                Program p = new Program();
                p.GetStartedDemo().Wait();
        }
        catch (DocumentClientException de)
        {
                Exception baseException = de.GetBaseException();
                Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
        }
        catch (Exception e)
        {
                Exception baseException = e.GetBaseException();
                Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
        }
        finally
        {
                Console.WriteLine("End of demo, press any key tooexit.");
                Console.ReadKey();
        }
```

키를 눌러 hello **DocumentDBGettingStarted** toobuild 단추 hello 응용 프로그램을 실행 합니다.

축하합니다. Tooan Azure Cosmos DB 계정을 성공적으로 연결한, 이제 살펴보겠습니다는 Azure Cosmos DB 리소스를 사용 합니다.  

## <a name="step-4-create-a-database"></a>4단계: 데이터베이스 만들기
데이터베이스를 만들기 위한 hello 코드를 추가 하기 전에 toohello 콘솔 작성 하기 위한 도우미 메서드를 추가 합니다.

복사 및 붙여넣기 hello **WriteToConsoleAndPromptToContinue** hello 아래 메서드 **GetStartedDemo** 메서드.

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

Azure Cosmos DB [데이터베이스](documentdb-resources.md#databases) hello를 사용 하 여 만들 수 [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) hello 방식의 **DocumentClient** 클래스입니다. 데이터베이스는 컬렉션에 분할 된 JSON 문서 저장소의 hello 논리적 컨테이너입니다.

복사 및 붙여넣기 hello 다음 코드 tooyour **GetStartedDemo** hello 클라이언트 만들기 아래 메서드. *FamilyDB*라는 데이터베이스가 생성됩니다.

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

키를 눌러 hello **DocumentDBGettingStarted** toorun 응용 프로그램 단추입니다.

축하합니다. Azure Cosmos DB 데이터베이스를 성공적으로 만들었습니다.  

## <a id="CreateColl"></a>5단계: 컬렉션 만들기
> [!WARNING]
> **CreateDocumentCollectionAsync** 는 가격 책정 의미가 포함된 예약된 처리량이 있는 새 컬렉션을 만듭니다. 자세한 내용은 [가격 페이지](https://azure.microsoft.com/pricing/details/cosmos-db/)를 참조하세요.

A [컬렉션](documentdb-resources.md#collections) hello를 사용 하 여 만들 수 [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) hello 방식의 **DocumentClient** 클래스입니다. 컬렉션은 JSON 문서 및 관련 JavaScript 응용 프로그램 논리의 컨테이너입니다.

복사 및 붙여넣기 hello 다음 코드 tooyour **GetStartedDemo** hello 데이터베이스 만들기 아래 메서드. *FamilyCollection_oa*라는 문서 컬렉션이 생성됩니다.

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

키를 눌러 hello **DocumentDBGettingStarted** toorun 응용 프로그램 단추입니다.

축하합니다. Azure Cosmos DB 데이터베이스 컬렉션을 성공적으로 만들었습니다.  

## <a id="CreateDoc"></a>6단계: JSON 문서 만들기
A [문서](documentdb-resources.md#documents) hello를 사용 하 여 만들 수 [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) hello 방식의 **DocumentClient** 클래스입니다. 문서는 사용자 정의(임의) JSON 콘텐츠입니다. 이제 하나 이상의 문서를 삽입할 수 있습니다. 원하는 toostore 데이터베이스의 데이터를 이미 있는 경우 Azure Cosmos DB를 사용할 수 있습니다 [데이터 마이그레이션 도구](import-data.md)합니다.

먼저 toocreate는 **제품군** 이 샘플에서 Azure Cosmos DB 내에 저장 하는 개체를 나타내는 클래스입니다. 또한 **가족** 내에서 사용되는 **부모**, **자식**, **애완 동물**, **주소** 하위 클래스를 만듭니다. 문서에는 JSON에서 **ID**로 직렬화된 **ID** 속성이 있어야 합니다. Hello 내부 하위 클래스 hello 후 다음을 추가 하 여 이러한 클래스를 만들 **GetStartedDemo** 메서드.

복사 및 붙여넣기 hello **제품군**, **부모**, **자식**, **애완 동물**, 및 **주소** 아래 클래스 hello **WriteToConsoleAndPromptToContinue** 메서드.

```csharp
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
    Console.WriteLine(format, args);
    Console.WriteLine("Press any key toocontinue ...");
    Console.ReadKey();
}

// ADD THIS PART tooYOUR CODE
public class Family
{
    [JsonProperty(PropertyName = "id")]
    public string Id { get; set; }
    public string LastName { get; set; }
    public Parent[] Parents { get; set; }
    public Child[] Children { get; set; }
    public Address Address { get; set; }
    public bool IsRegistered { get; set; }
    public override string ToString()
    {
            return JsonConvert.SerializeObject(this);
    }
}

public class Parent
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
}

public class Child
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
    public string Gender { get; set; }
    public int Grade { get; set; }
    public Pet[] Pets { get; set; }
}

public class Pet
{
    public string GivenName { get; set; }
}

public class Address
{
    public string State { get; set; }
    public string County { get; set; }
    public string City { get; set; }
}
```

복사 및 붙여넣기 hello **CreateFamilyDocumentIfNotExists** 아래 메서드 여 **CreateDocumentCollectionIfNotExists** 메서드.

```csharp
// ADD THIS PART tooYOUR CODE
private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
{
    try
    {
        await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
        this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
    }
    catch (DocumentClientException de)
    {
        if (de.StatusCode == HttpStatusCode.NotFound)
        {
            await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
            this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
        }
        else
        {
            throw;
        }
    }
}
```

두 문서, 각 hello Andersen 제품군 및 제품군 Wakefield hello를 삽입 합니다.

복사 및 붙여넣기 hello 코드 뒤에 오는 `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** hello 문서 컬렉션 만들기 아래 메서드.

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
Family andersenFamily = new Family
{
        Id = "Andersen.1",
        LastName = "Andersen",
        Parents = new Parent[]
        {
                new Parent { FirstName = "Thomas" },
                new Parent { FirstName = "Mary Kay" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FirstName = "Henriette Thaulow",
                        Gender = "female",
                        Grade = 5,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Fluffy" }
                        }
                }
        },
        Address = new Address { State = "WA", County = "King", City = "Seattle" },
        IsRegistered = true
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

Family wakefieldFamily = new Family
{
        Id = "Wakefield.7",
        LastName = "Wakefield",
        Parents = new Parent[]
        {
                new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                new Parent { FamilyName = "Miller", FirstName = "Ben" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FamilyName = "Merriam",
                        FirstName = "Jesse",
                        Gender = "female",
                        Grade = 8,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Goofy" },
                                new Pet { GivenName = "Shadow" }
                        }
                },
                new Child
                {
                        FamilyName = "Miller",
                        FirstName = "Lisa",
                        Gender = "female",
                        Grade = 1
                }
        },
        Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
        IsRegistered = false
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

키를 눌러 hello **DocumentDBGettingStarted** toorun 응용 프로그램 단추입니다.

축하합니다. 두 개의 Azure Cosmos DB 문서를 성공적으로 만들었습니다.  

![Hello 계정과 hello 온라인 데이터베이스, hello 컬렉션 hello NoSQL 자습서 toocreate C# 콘솔 응용 프로그램에서 사용 하는 hello 문서 간의 hello 계층 관계를 보여 주는 다이어그램](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>7단계: Azure Cosmos DB 리소스 쿼리
Azure Cosmos DB는 각 컬렉션에 저장된 JSON 문서에 대해 [다양한 쿼리](documentdb-sql-query.md)를 지원합니다.  hello 다음 샘플 코드를 보여 줍니다 다양 한 쿼리-두 Azure Cosmos DB SQL을 사용 하 여 것에 대해 실행할 수 있는 LINQ-뿐 아니라 구문 hello 문서 hello 이전 단계에서 삽입 했습니다.

복사 및 붙여넣기 hello **ExecuteSimpleQuery** 아래 메서드 여 **CreateFamilyDocumentIfNotExists** 메서드.

```csharp
// ADD THIS PART tooYOUR CODE
private void ExecuteSimpleQuery(string databaseName, string collectionName)
{
    // Set some common query options
    FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

        // Here we find hello Andersen family via its LastName
        IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                .Where(f => f.LastName == "Andersen");

        // hello query is executed synchronously here, but can also be executed asynchronously via hello IDocumentQuery<T> interface
        Console.WriteLine("Running LINQ query...");
        foreach (Family family in familyQuery)
        {
            Console.WriteLine("\tRead {0}", family);
        }

        // Now execute hello same query via direct SQL
        IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                queryOptions);

        Console.WriteLine("Running direct SQL query...");
        foreach (Family family in familyQueryInSql)
        {
                Console.WriteLine("\tRead {0}", family);
        }

        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

복사 및 붙여넣기 hello 다음 코드 tooyour **GetStartedDemo** hello 두 번째 문서 만들기 아래 메서드.

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

키를 눌러 hello **DocumentDBGettingStarted** toorun 응용 프로그램 단추입니다.

축하합니다. Azure Cosmos DB 컬렉션에 대한 쿼리가 성공적으로 수행되었습니다.

hello 다음 다이어그램에서는 구문 hello 컬렉션에 대해 호출 되는 hello Azure Cosmos DB SQL 쿼리를 만든 방법, 고 hello 동일한 논리 적용 toohello LINQ 쿼리도 합니다.

![다이어그램 hello 범위를 표현 하 고 hello 쿼리의 의미에서 사용 하는 hello NoSQL 자습서 toocreate C# 콘솔 응용 프로그램](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

hello [FROM](documentdb-sql-query.md#FromClause) Azure Cosmos DB 쿼리 범위 지정 된 tooa 단일 컬렉션에 이미 있으므로 키워드는 hello 쿼리에서 선택 사항입니다. 따라서 "FROM Families f"를 "FROM root r" 또는 선택한 다른 변수 이름으로 교체할 수 있습니다. DocumentDB는 제품군, 루트 또는 hello 변수 이름을 선택한, 기본적으로 참조 hello 현재 컬렉션을 유추 합니다.

## <a id="ReplaceDocument"></a>8단계: JSON 문서 바꾸기
Azure Cosmos DB는 JSON 문서 바꾸기를 지원합니다.  

복사 및 붙여넣기 hello **ReplaceFamilyDocument** 아래 메서드 여 **ExecuteSimpleQuery** 메서드.

```csharp
// ADD THIS PART tooYOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

복사 및 붙여넣기 hello 다음 코드 tooyour **GetStartedDemo** 메서드 아래 hello 쿼리를 실행 합니다. Hello 문서를 바꾼 후가 실행 되어 hello 동일 tooview 변경 hello 문서 다시 쿼리 합니다.

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

키를 눌러 hello **DocumentDBGettingStarted** toorun 응용 프로그램 단추입니다.

축하합니다. Azure Cosmos DB 문서를 성공적으로 대체했습니다.

## <a id="DeleteDocument"></a>9단계: JSON 문서 삭제
Azure Cosmos DB는 JSON 문서 삭제를 지원합니다.  

복사 및 붙여넣기 hello **DeleteFamilyDocument** 아래 메서드 여 **ReplaceFamilyDocument** 메서드.

```csharp
// ADD THIS PART tooYOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

복사 및 붙여넣기 hello 다음 코드 tooyour **GetStartedDemo** 메서드 아래 hello 두 번째 쿼리를 실행 합니다.

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

키를 눌러 hello **DocumentDBGettingStarted** toorun 응용 프로그램 단추입니다.

축하합니다. Azure Cosmos DB 문서를 성공적으로 삭제했습니다.

## <a id="DeleteDatabase"></a>10 단계: hello 데이터베이스를 삭제 합니다.
데이터베이스를 만들었습니다. 삭제 hello hello 데이터베이스와 모든 자식 리소스 (컬렉션, 문서 등)를 제거 합니다.

복사 및 붙여넣기 hello 다음 코드 tooyour **GetStartedDemo** hello 문서 아래 메서드 toodelete hello에 대 한 전체 데이터베이스 및 모든 자식 리소스를 삭제 합니다.

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

키를 눌러 hello **DocumentDBGettingStarted** toorun 응용 프로그램 단추입니다.

축하합니다. Azure Cosmos DB 데이터베이스를 성공적으로 삭제했습니다.

## <a id="Run"></a>11단계: C# 콘솔 응용 프로그램 모두 함께 실행
키를 눌러 hello **DocumentDBGettingStarted** 디버그 모드에서 Visual Studio toobuild hello 응용 프로그램에서 단추입니다.

Hello 출력 hello 콘솔 창에 get 시작된 응용 프로그램의 표시 되어야 합니다. hello 출력 hello hello 결과 보기는 쿼리를 추가 하 고 아래 예제에서는 텍스트 hello와 일치 해야 합니다.

```
Created FamilyDB_oa
Press any key toocontinue ...
Created FamilyCollection_oa
Press any key toocontinue ...
Created Family Andersen.1
Press any key toocontinue ...
Created Family Wakefield.7
Press any key toocontinue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Replaced Family Andersen.1
Press any key toocontinue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Deleted Family Andersen.1
End of demo, press any key tooexit.
```

축하합니다. Hello 자습서를 완료 하 고 C# 콘솔 응용 프로그램!

## <a id="GetSolution"></a>Hello 완료 자습서 솔루션 가져오기
이 문서에서 모든 hello 예제가 포함 된 toobuild hello GetStarted 솔루션 hello 다음이 필요 합니다.

* 활성 Azure 계정. 계정이 없는 경우 [무료 계정](https://azure.microsoft.com/free/)에 등록할 수 있습니다.
* [Azure Cosmos DB 계정][create-documentdb-dotnet.md#create-account].
* hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) 솔루션 GitHub에서 사용할 수 있습니다.

Visual Studio에서 Azure Cosmos DB.NET Core SDK에 대 한 DocumentDB API toorestore hello 참조 toohello hello를 마우스 오른쪽 단추로 클릭 **GetStarted** 클릭 한 다음 솔루션 탐색기에서 솔루션 **NuGet 패키지 복원을 사용**. 다음으로 hello Program.cs 파일에서 값을 업데이트 hello EndpointUrl 및 AuthorizationKey에 설명 된 대로 [tooan Cosmos DB Azure 계정을 연결](#Connect)합니다.

## <a name="next-steps"></a>다음 단계
* 보다 복잡한 ASP.NET MVC 자습서가 필요하신가요? [ASP.NET MVC 자습서: Azure Cosmos DB를 사용한 웹 응용 프로그램 개발](documentdb-dotnet-application.md)을 참조하세요.
* Xamarin iOS, Android 또는 Forms toodevelop를 원하는 Azure Cosmos DB.NET Core SDK에 대 한 DocumentDB API hello를 사용 하 여 응용 프로그램? [Xamarin 및 Azure Cosmos DB를 사용하여 모바일 응용 프로그램 빌드](mobile-apps-with-xamarin.md)를 참조하세요.
* Tooperform 확장 및 성능 Azure Cosmos DB를 사용 하 여 테스트를 선택 하십시오. [Azure Cosmos DB를 사용한 성능 및 규모 테스트](performance-testing.md)를 참조하세요.
* 너무 방법에 대해 알아봅니다[모니터 Azure Cosmos DB 요청, 사용 및 저장소](monitor-accounts.md)합니다.
* Hello에 우리의 샘플 데이터 집합에 대해 쿼리 실행 [Query Playground](https://www.documentdb.com/sql/demo)합니다.
* hello 프로그래밍 모델에 대해 자세히 toolearn 참조 [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)합니다.

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
