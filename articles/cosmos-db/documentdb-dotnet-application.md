---
title: "Azure Cosmos DB용 ASP.NET MVC 자습서: 웹 응용 프로그램 개발 | Microsoft Docs"
description: "ASP.NET MVC 자습서 toocreate Azure Cosmos DB를 사용 하 여 MVC 웹 응용 프로그램 JSON을 저장하고 Azure Websites - ASP NET MVC 단계별 자습서에서 호스팅하는 todo 앱에서 데이터에 액세스합니다."
keywords: "ASP.NET MVC 자습서, 웹 응용 프로그램 개발, MVC 웹 응용 프로그램, ASP NET MVC 단계별 자습서"
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="_Toc395809351"></a>ASP.NET MVC 자습서: Azure Cosmos DB를 사용한 웹 응용 프로그램 개발
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.JS](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

toohighlight이이 문서에서는 방법을 보여 주는 하는 종단 간 연습을 제공 수 효율적으로 Azure Cosmos DB toostore를 활용 하 고 JSON 문서를 쿼리 하는 방법 toobuild Azure Cosmos DB를 사용 하 여 todo 앱. hello 작업 Azure Cosmos DB에서 JSON 문서도 저장 됩니다.

![Hello 할 일 목록 ASP NET MVC 자습서 단계별-이 자습서에서 만든 MVC 웹 응용 프로그램의 스크린 샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

이 연습에서는 toouse Azure에서 호스팅되는 ASP.NET MVC 웹 응용 프로그램에서 Azure Cosmos DB 서비스 toostore 및 액세스 데이터를 hello 하는 방법을 보여 줍니다. 표시 되 면 Azure Cosmos DB에만 초점을 두는 자습서에 대 한 원하는 하지 hello ASP.NET MVC 구성 요소 [Azure Cosmos DB C# 콘솔 응용 프로그램을 작성할](documentdb-get-started.md)합니다.

> [!TIP]
> 이 자습서에서는 이전에 ASP.NET MVC 및 Azure Websites를 사용해 본 경험이 있다고 가정합니다. 새 tooASP.NET 또는 hello [필수 구성 요소 도구](#_Toc395637760)에서 hello 전체 샘플 프로젝트를 다운로드 하는 것이 좋습니다 [GitHub] [ GitHub] hello 지침에 따라 이 샘플입니다. 를 만든 후 작성 된 것이 문서 toogain에 대 한 정보 hello 프로젝트의 hello 컨텍스트에서 hello 코드를 검토할 수 있습니다.
> 
> 

## <a name="_Toc395637760"></a>이 데이터베이스 자습서의 필수 조건
Hello이이 문서의 지침을 수행 하기 전에 hello 다음 있는지 확인 해야 합니다.

* 활성 Azure 계정. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요. 

    또는

    Hello의 로컬 설치 [Azure Cosmos DB 에뮬레이터](local-emulator.md)합니다.
* [Visual Studio 2017](http://www.visualstudio.com/).  
* Microsoft Azure SDK for.NET에 대 한 Visual Studio 2017 년 hello Visual Studio 설치 관리자를 통해 사용할 수 있습니다.

Microsoft Visual Studio 커뮤니티 2017을 사용 하 여이 문서에서 모든 hello 스크린 샷 수행 되었습니다. 시스템 구성에 다른 버전으로 경우 것으로 화면과 옵션 완전히 일치 하지 않습니다 되지만 hello 위의 필수 구성 요소를 충족 하는 경우에이 솔루션 작동 해야 합니다.

## <a name="_Toc395637761"></a>1단계: Azure Cosmos DB 데이터베이스 계정 만들기
Azure Cosmos DB 계정을 만들어 시작해 보겠습니다. 경우 이미 Azure Cosmos DB에 대 한 SQL (DocumentDB) 계정이 또는 사용 하는 경우이 자습서에 대 한 Azure Cosmos DB 에뮬레이터 hello를 건너뛸 수 있습니다 너무[새 ASP.NET MVC 응용 프로그램 만들기](#_Toc395637762)합니다.

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
이제 단계별로 어떻게 toocreate hello에서 새 ASP.NET MVC 응용 프로그램 명확 하 게 해제 합니다. 

## <a name="_Toc395637762"></a>2단계: 새 ASP.NET MVC 응용 프로그램 만들기

1. Hello에 Visual Studio에서 **파일** 메뉴 너무 가리킨**새로**, 클릭 하 고 **프로젝트**합니다. hello **새 프로젝트** 대화 상자가 나타납니다.

2. Hello에 **프로젝트 형식** 창 확장 **템플릿**, **Visual C#**, **웹**를 선택한 후 **ASP.NET 웹 응용 프로그램** .

      ![강조 표시 하는 hello ASP.NET 웹 응용 프로그램 프로젝트 형식과 함께 hello 새 프로젝트 대화 상자 스크린샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. Hello에 **이름** 상자 hello 프로젝트의 hello 이름을 입력 합니다. 이 자습서에서는 hello 이름 "todo"를 사용 합니다. 을 선택 하면 toouse이 아닌 다른 hello todo 네임 스페이스에 대 한이 자습서 발언 때마다 해야 tooadjust hello 제공 된 코드 샘플 toouse 응용 프로그램이 지정한 이름을. 
4. 클릭 **찾아보기** toonavigate toohello 폴더 위치 toocreate hello 프로젝트를 선택한 다음 클릭 **확인**합니다.
   
      hello **새 ASP.NET 웹 응용 프로그램** 대화 상자가 나타납니다.
   
    ![강조 표시 하는 hello MVC 응용 프로그램 템플릿 사용 하 여 hello 새 ASP.NET 웹 응용 프로그램 대화 상자 스크린 샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. Hello 템플릿 창에서 선택 **MVC**합니다.

6. 클릭 **확인** 주위 스 캐 폴딩 hello 빈 ASP.NET MVC 템플릿에서 해당 작업을 수행 하는 Visual Studio를 사용 하 고 있습니다. 

          
7. Visual Studio 완료 되 면 hello 상용구 MVC 응용 프로그램을 만드는 해야 빈 ASP.NET 응용 프로그램을 로컬로 실행할 수 있습니다.
   
    ASP.NET "Hello World" 모든 표시 hello 이유임 확실 하기 때문에 로컬로 실행 중인 hello 프로젝트 건너뜁니다 응용 프로그램입니다. 직선 tooadding Azure Cosmos DB toothis 프로젝트 및 응용 프로그램을 빌드 해 보겠습니다.

## <a name="_Toc395637767"></a>3 단계: Azure Cosmos DB tooyour MVC 웹 응용 프로그램 프로젝트 추가
이제 대부분이이 솔루션에 대 한 hello ASP.NET MVC 배관의 했으므로 Azure Cosmos DB tooour MVC 웹 응용 프로그램을 추가 하는이 자습서에서는 주요 목적은 toohello 보겠습니다.

1. hello Cosmos DB AZURE.NET SDK가 패키징되 어 NuGet 패키지로 배포 됩니다. tooget Visual Studio에서 NuGet 패키지를 hello, Visual Studio에서 hello NuGet 패키지 관리자를 사용 하 여 hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 **솔루션 탐색기** 클릭 한 다음 **NuGet 패키지 관리**합니다.
   
    ![Hello 스크린 샷 단추로 NuGet 패키지 관리 강조 표시 된 솔루션 탐색기에서 hello 웹 응용 프로그램 프로젝트에 대 한 옵션을 클릭 합니다.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    hello **NuGet 패키지 관리** 대화 상자가 나타납니다.
2. Hello NuGet에서에서 **찾아보기** 상자에서 입력 ***Azure DocumentDB***합니다. (hello 패키지 이름을 업데이트 tooAzure Cosmos DB 되지 않았습니다.)
   
    Hello 결과 통해 설치 hello **microsoft Microsoft.Azure.DocumentDB** 패키지 합니다. 이 다운로드 하 여 Newtonsoft.Json 등 모든 종속성 뿐 아니라 hello Azure Cosmos DB 패키지를 설치 합니다. 클릭 **확인** hello에 **미리 보기** 창 및 **동의** hello에 **라이선스 승인** 창 toocomplete hello 설치 합니다.
   
    ![화면 샷 hello NuGet 패키지 관리 창 hello 강조 표시 하는 Microsoft Azure DocumentDB 클라이언트 라이브러리](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      또는 hello 패키지 관리자 콘솔 tooinstall hello 패키지를 사용할 수 있습니다. toodo hello에 너무 **도구** 메뉴를 클릭 하 여 **NuGet 패키지 관리자**, 클릭 하 고 **패키지 관리자 콘솔**합니다. Hello 프롬프트 hello 다음을 입력 합니다.
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. Hello 패키지를 설치한 후 Visual Studio 솔루션에 두 개의 새 참조 추가, Microsoft.Azure.Documents.Client 및 Newtonsoft.Json을 사용 하 여 hello 다음을 비슷해야 합니다.
   
    ![화면 샷 hello 두 개의 참조 솔루션 탐색기에서 toohello JSON 데이터 프로젝트 추가](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <a name="_Toc395637763"></a>4 단계: hello ASP.NET MVC 응용 프로그램 설정
이제 hello 모델, 뷰 및 컨트롤러 toothis MVC 응용 프로그램을 추가 해 보겠습니다.

* [모델 추가](#_Toc395637764).
* [컨트롤러 추가](#_Toc395637765).
* [뷰 추가](#_Toc395637766).

### <a name="_Toc395637764"></a>JSON 데이터 모델 추가
Hello를 만들어 보겠습니다 **M** mvc에서 모델을 hello 합니다. 

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **모델** 폴더를 클릭 **추가**, 클릭 하 고 **클래스**합니다.
   
      hello **새 항목 추가** 대화 상자가 나타납니다.
2. 새 클래스의 이름을 **Item.cs**로 지정하고 **추가**를 클릭합니다. 
3. 이 새로운 **Item.cs** 파일, 마지막 hello hello 뒤에 다음 추가 *문을 사용 하 여*합니다.
   
        using Newtonsoft.Json;
4. 이제 이 코드를 
   
        public class Item
        {
        }
   
    코드 다음 안녕하세요와.
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    Azure Cosmos DB에서 모든 데이터는 hello 네트워크를 통해 전달 되 고 JSON으로 저장 합니다. 개체는 사용할 수 있습니다 JSON.NET 직렬화/역직렬화 toocontrol hello 방식으로 hello **JsonProperty** hello에서와 같이 특성 **항목** 방금 만든 클래스입니다. 그렇지 않으면 **가** toodo 했지만이 원하는 tooensure 내 속성 hello JSON camelCase 명명 규칙을 따르도록 합니다. 
   
    뿐만 아니라을 조정할 수 hello 속성 이름의 hello 형식은 JSON에 있지만 hello로 했던 처럼.NET 속성을 완전히 바꿀 수 있습니다 **설명** 속성입니다. 

### <a name="_Toc395637765"></a>컨트롤러 추가
Hello의 담당 **M**, 이제 hello를 만들어 보겠습니다 **C** mvc에서 컨트롤러 클래스입니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **컨트롤러** 폴더를 클릭 **추가**, 클릭 하 고 **컨트롤러**합니다.
   
    hello **추가 스 캐 폴드** 대화 상자가 나타납니다.
2. **MVC 5 컨트롤러 - 비어 있음**을 선택한 후 **추가**를 클릭합니다.
   
    ![MVC 5 컨트롤러 강조 표시 하는 빈 옵션 hello로 hello 스 캐 폴드 추가 대화 상자 스크린 샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. 새 컨트롤러의 이름을 **ItemController**
   
    ![Hello 컨트롤러 추가 대화 상자 스크린 샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    Visual Studio 솔루션에 새 ItemController.cs 파일로 hello hello 다음과 같이 해야 hello 파일을 만든 후 **솔루션 탐색기**합니다. 앞에서 만든 hello 새 Item.cs 파일 정보도 표시 됩니다.
   
    ![Hello Visual Studio 솔루션-hello 새 ItemController.cs 파일과 Item.cs 파일 강조 표시 된 솔루션 탐색기의 스크린샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    ItemController.cs 닫을 수 있습니다, 다시 tooit 나중 살펴보겠습니다. 

### <a name="_Toc395637766"></a>뷰 추가
이제 hello를 만들어 보겠습니다 **V** mvc에서는 뷰 hello:

* [항목 인덱스 뷰 추가](#AddItemIndexView).
* [새 항목 뷰 추가](#AddNewIndexView).
* [항목 편집 뷰 추가](#_Toc395888515).

#### <a name="AddItemIndexView"></a>항목 인덱스 뷰 추가
1. **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 hello 빈 **항목** hello를 추가 했을 때 Visual Studio를 만든 폴더에  **ItemController** 이전에 클릭 **추가**, 클릭 하 고 **보기**합니다.
   
    ![Visual Studio 강조 표시 하는 hello 뷰 추가 명령을 사용 하 여 만든 hello 항목 폴더를 나타내는 솔루션 탐색기의 스크린 샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. Hello에 **뷰 추가** 대화 상자에서 다음 hello지 않습니다.
   
   * Hello에 **뷰 이름** 상자에서 입력 ***인덱스***합니다.
   * Hello에 **템플릿** 상자 ***목록***합니다.
   * Hello에 **모델 클래스** 상자 ***항목 (할 일입니다. 모델)***합니다.
   * Hello 레이아웃 페이지 상자에 입력 ***~/Views/Shared/_Layout.cshtml***합니다.
     
   ![표시 된 hello 뷰 추가 대화 상자 스크린 샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. 이러한 값이 모두 설정된 후 **추가** 를 클릭하면 Visual Studio에서 새 템플릿 뷰를 만듭니다. 작업이 완료 되 면 만든 hello cshtml 파일이 열립니다. 우리는 나중에 다시 tooit 대로 Visual Studio에서 해당 파일을 닫을 수 있습니다.

#### <a name="AddNewIndexView"></a>새 항목 뷰 추가
만든 비슷한 toohow는 **항목 인덱스** 보기를 지금 만듭니다 새로 만들기에 대 한 새 보기 **항목**합니다.

1. **솔루션 탐색기**, 마우스 오른쪽 단추로 클릭 hello **항목** 폴더를 다시 클릭 **추가**, 클릭 하 고 **보기**합니다.
2. Hello에 **뷰 추가** 대화 상자에서 다음 hello지 않습니다.
   
   * Hello에 **뷰 이름** 상자에서 입력 ***만들기***합니다.
   * Hello에 **템플릿** 상자 ***만들기***합니다.
   * Hello에 **모델 클래스** 상자 ***항목 (할 일입니다. 모델)***합니다.
   * Hello 레이아웃 페이지 상자에 입력 ***~/Views/Shared/_Layout.cshtml***합니다.
   * **추가**를 클릭합니다.
   
#### <a name="_Toc395888515"></a>항목 편집 뷰 추가
마지막으로 편집을 위해 마지막 보기를 추가 하 고는 **항목** hello에 이전과 동일한 방식으로 합니다.

1. **솔루션 탐색기**, 마우스 오른쪽 단추로 클릭 hello **항목** 폴더를 다시 클릭 **추가**, 클릭 하 고 **보기**합니다.
2. Hello에 **뷰 추가** 대화 상자에서 다음 hello지 않습니다.
   
   * Hello에 **뷰 이름** 상자에서 입력 ***편집***합니다.
   * Hello에 **템플릿** 상자 ***편집***합니다.
   * Hello에 **모델 클래스** 상자 ***항목 (할 일입니다. 모델)***합니다.
   * Hello 레이아웃 페이지 상자에 입력 ***~/Views/Shared/_Layout.cshtml***합니다.
   * **추가**를 클릭합니다.

이 작업이 완료 되 면 나중 toothese 뷰를 반환 합니다에서는 Visual Studio에서 모든 hello cshtml 문서를 닫습니다.

## <a name="_Toc395637769"></a>5단계: Azure Cosmos DB 연결
Hello 표준 MVC 항목 처리, 했으므로 Azure Cosmos DB에 대 한 tooadding hello 코드를 설정 해 보겠습니다. 

이 섹션에서는 코드 toohandle hello 다음을 추가 하겠습니다.

* [완료되지 않은 항목 나열](#_Toc395637770).
* [항목 추가](#_Toc395637771).
* [항목 편집](#_Toc395637772).

### <a name="_Toc395637770"></a>MVC 웹 응용 프로그램에서 완료되지 않은 항목 나열
hello 첫 번째 것이 toodo은 추가 모든 hello 논리 tooconnect tooand 사용 하 여 Azure Cosmos DB를 포함 하는 클래스입니다. 이 자습서에 대 한 DocumentDBRepository 라는 tooa 저장소 클래스에서이 모든 논리를 캡슐화 할 것 했습니다. 

1. **솔루션 탐색기**hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 **추가**, 클릭 하 고 **클래스**합니다. Hello 새 클래스 이름을 **DocumentDBRepository** 클릭 **추가**합니다.
2. 새로 만든 hello에 **DocumentDBRepository** 클래스 및 hello 다음 추가 *문을 사용 하 여* hello 위에 *네임 스페이스* 선언
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    이제 이 코드를 
   
        public class DocumentDBRepository
        {
        }
   
    코드 다음 안녕하세요와.
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. 구성에서 일부 값을 읽는 하는 것, hello을 열고 **Web.config** 응용 프로그램의 파일 hello hello 아래 줄을 다음 추가 `<AppSettings>` 섹션.
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. 이제, 업데이트에 대 한 hello 값 *끝점* 및 *authKey* hello Azure 포털의 키 블레이드에서 hello를 사용 하 여 합니다. Hello를 사용 하 여 **URI** hello 끝점 설정 및 사용 하 여 hello hello 값으로 hello 키 블레이드에서 **기본 키**, 또는 **보조 키** hello의 hello 값으로 hello 키 블레이드에서 authKey 설정입니다.

    관리 배선 hello Azure Cosmos DB 리포지토리를 이제 보겠습니다 추가할이 응용 프로그램 논리.

1. hello 먼저 원하는 toobe 수 toodo 할 일 목록 응용 프로그램은 toodisplay hello 불완전 한 항목입니다.  복사 및 붙여넣기 hello 내 코드 조각 다음 hello **DocumentDBRepository** 클래스입니다.
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. 열기 hello **ItemController** 앞에 추가 하 고 hello 다음 추가 *문을 사용 하 여* hello 네임 스페이스 선언 위에 있습니다.
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    프로젝트 "todo"을 지정 하지 않은 경우 다음 필요한 tooupdate "todo를 사용 하 여. 모델 "; 프로젝트의 tooreflect hello 이름입니다.
   
    이제 이 코드를
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    코드 다음 안녕하세요와.
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. 열기 **Global.asax.cs** hello 줄 toohello 다음 추가 **Application_Start** 메서드 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

이 시점에서 솔루션에는 오류 없이 수 toobuild 이어야 합니다.

Toohello 거쳐야 hello 응용 프로그램을 지금 실행 한 경우 **HomeController** 및 hello **인덱스** 해당 컨트롤러의 보기입니다. 이 hello 시작 될 때 선택한 이유는 hello MVC 서식 파일 프로젝트에 대 한 기본 동작 hello 하지만 않도록 하는! 이 MVC 응용 프로그램 tooalter에서이 동작은 라우팅 hello를 변경해 보겠습니다.

열기 ***앱\_Start\RouteConfig.cs*** 찾을 hello 줄으로 시작 하 고 "기본값:" tooresemble hello 다음 변경 합니다.

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

이 구문은 이제 지시 hello URL toocontrol에 값을 지정 하지 않은 경우 hello 라우팅 동작 대신 ASP.NET MVC **홈**를 사용 하 여 **항목** hello 컨트롤러 및 사용자 **인덱스** hello 뷰로 합니다.

Hello 응용 프로그램을 실행 하는 경우에 호출 됩니다는 이제 프로그램 **ItemController** toohello 저장소 클래스에서 호출 되며 모든 hello 불완전 한 항목 toohello GetItems 메서드 tooreturn hello를 사용 하 여 있는 **뷰** \\ **항목**\\**인덱스** 보기. 

이 프로젝트를 지금 빌드하여 실행하면 이제 다음과 같이 표시됩니다.    

![Hello 할 일 목록 웹 응용 프로그램의이 데이터베이스 자습서에서 만든 스크린 샷](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <a name="_Toc395637771"></a>항목 추가
에 있는 빈 그리드가 toolook 보다 더 많은 한 일부 항목 데이터베이스로 넘어가면 적용 해 보겠습니다.

일부 코드를 너무 추가해보겠습니다 Azure Cosmos DB에서 Azure Cosmos DBRepository 및 ItemController toopersist hello 레코드입니다.

1. 다음 메서드 tooyour hello 추가 **DocumentDBRepository** 클래스입니다.
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   이 메서드는 단순히 tooit 전달 되는 개체를 사용 하 고 계속 되 면 Azure Cosmos DB에서.
2. Hello ItemController.cs 파일을 열고 hello 코드 조각 hello 클래스 내에서 다음을 추가 합니다. 이 ASP.NET MVC의 hello에 대 한 어떤 toodo 알고 어떻게 **만들기** 동작 합니다. 이 경우에 렌더링 hello 관련 앞에서 만든 Create.cshtml 보기.
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    이제 hello에서 hello 전송이 허용 하는이 컨트롤러에 몇 가지 더 많은 코드가 필요 **만들기** 보기.
3. Hello 코드 toohello 어떤 toodo이이 컨트롤러에 대 한 POST 양식으로 ASP.NET MVC에 알려 주는 ItemController.cs 클래스의 다음 블록을 추가 합니다.
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    이 코드 toohello DocumentDBRepository 호출 하 고 hello CreateItemAsync 메서드 toopersist hello 새 할 일 항목 toohello 데이터베이스를 사용 합니다. 
   
    **보안 정보**: hello **ValidateAntiForgeryToken** 특성은 사용 여기 toohelp 교차 사이트 요청 위조 공격에 대 한이 응용 프로그램을 보호 합니다. 이 특성을 추가 하는 것 보다 더 많은 tooit를 보기에는이 위조 방지 토큰으로 toowork 필요 없습니다. Hello 제목 및 예제는 어떻게 tooimplement이 올바르게 참조 하십시오에 대 한 자세한 [교차 사이트 요청 위조 방지][Preventing Cross-Site Request Forgery]합니다. 에 제공 된 소스 코드를 hello [GitHub] [ GitHub] hello 완전 한 구현에 있습니다.
   
    **보안 정보**: hello도 사용 **바인딩할** hello 메서드 매개 변수 toohelp 특성이 공격을 과도 하 게 게시 으로부터 보호 합니다. 자세한 내용은 [ASP.NET MVC의 기본 CRUD 작업(영문)][Basic CRUD Operations in ASP.NET MVC]을 참조하세요.

Hello 필요한 코드 tooadd 새 항목 tooour 데이터베이스를 완료 했습니다.

### <a name="_Toc395637772"></a>항목 편집
에 마지막으로 toodo, 않으며 하는 tooadd hello 기능 tooedit **항목** hello 데이터베이스와 toomark에서와 같이 완료 합니다. hello 보기 편집을 위해 이미 추가 되었으므로 toohello 프로젝트, 일부 코드 tooour 컨트롤러 및 toohello त ु म च tooadd 하므로 **DocumentDBRepository** 다시 클래스입니다.

1. Hello toohello 다음 추가 **DocumentDBRepository** 클래스입니다.
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    이러한 메서드의 첫 번째 hello **GetItem** 백 toohello 전달 되는 Azure Cosmos DB에서 항목을 인출 **ItemController** toohello에서 **편집** 보기.
   
    hello 메서드의 두 번째 hello 대체 hello 방금 추가한 **문서** hello 버전의 hello Azure Cosmos DB에서 **문서** hello에서 전달 된 **ItemController**합니다.
2. Hello toohello 다음 추가 **ItemController** 클래스입니다.
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    hello 첫 번째 메서드 핸들 hello hello에 hello 사용자가 클릭할 때 발생 하는 Http GET **편집** hello에서 링크 **인덱스** 보기. 이 메서드를 인출는 [ **문서** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) Azure Cosmos DB에서 toohello 전달 **편집** 보기.
   
    hello **편집** 보기 다음 Http POST toohello를 수행 **IndexController**합니다. 
   
    업데이트 하는 hello 개체 tooAzure Cosmos DB toobe 전달 핸들 추가 hello 두 번째 방법은 hello 데이터베이스에 보관 합니다.

응용 프로그램 toorun 필요한 모든 구성 되 고, 즉, 완료 되지 않은 목록 **항목**, 새로 추가 **항목**, 편집 및 **항목**합니다.

## <a name="_Toc395637773"></a>6 단계: hello 응용 프로그램을 로컬로 실행
로컬 컴퓨터의 tootest hello 응용 프로그램은 다음 hello지 않습니다.

1. 디버그 모드에서 Visual Studio toobuild hello 응용 프로그램에서 f5 키를 누르면 됩니다. Hello 응용 프로그램을 작성 하 고 실행 하기 전에 살펴본 hello 빈 그리드 페이지를 사용 하 여 브라우저:
   
    ![Hello 할 일 목록 웹 응용 프로그램의이 데이터베이스 자습서에서 만든 스크린 샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. Hello 클릭 **새로 만들기** 에 연결 하 고 추가 값 toohello **이름** 및 **설명** 필드입니다. Hello 둡니다 **완료** 확인란 새 그렇지 않으면 hello 선택 되지 않은 **항목** 완료 됨 상태로 추가 되 고 hello 초기 목록에 표시 되지 것입니다.
   
    ![Hello 뷰 만들기 스크린 샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. 클릭 **만들기** 리디렉션된 백 toohello 않으며 **인덱스** 보기 및 **항목** hello 목록에 나타납니다.
   
    ![Hello 인덱스 뷰 스크린 샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    몇 가지 더 무료 tooadd 느껴집니다 **항목** tooyour 할 일 목록입니다.
    
4. 클릭 **편집** 다음 tooan **항목** hello 목록에 toohello 취해집니다 **편집** hello를 포함 하 여 개체의 모든 속성을 업데이트할 수 있는 보기  **완료** 플래그입니다. Hello를 표시 하는 경우 **완료** 플래그를 클릭 하 여 **저장**, hello **항목** 완료 되지 않은 작업의 hello 목록에서 제거 됩니다.
   
    ![Hello 인덱스 뷰 hello Completed 확인란을 선택의 스크린 샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. Hello 앱을 테스트 하면 Ctrl + f 5 toostop hello 응용 프로그램 디버깅에 키를 누릅니다. 준비 toodeploy 넌!

## <a name="_Toc395637774"></a>7 단계: 배포 hello 응용 프로그램 tooAzure 앱 서비스 
Hello 완전 한 응용 프로그램을가지고 Azure Cosmos DB으로 제대로 작동 여기 toodeploy이 웹 앱 tooAzure 앱 서비스입니다.  

1. toopublish이 응용이 프로그램 모두 toodo 필요한은에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기** 클릭 **게시**합니다.
   
    ![Hello 솔루션 탐색기에서 게시 옵션의 스크린 샷](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. Hello에 **게시** 대화 상자에서 클릭 **Microsoft Azure 앱 서비스**을 선택한 후 **새로 만들기** toocreate 응용 프로그램 서비스를 프로 파일링 하거나 클릭 **선택 기존** toouse 기존 프로필입니다.

    ![Visual Studio에서 대화 상자 게시](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. 기존 Azure App Service 프로필이 있는 경우 구독 이름을 입력합니다. 사용 하 여 hello **보기** toosort 리소스 그룹 또는 리소스 종류를 필터링 한 다음 Azure 앱 서비스를 선택 합니다. 
   
    ![Visual Studio의 App Service 대화 상자](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. 새 Azure 앱 서비스 프로필 toocreate 클릭 **새로 만들기** hello에 **게시** 대화 상자. Hello에 **응용 프로그램 서비스 만들기** 대화 상자에서 웹 응용 프로그램 이름 및 적절 한 구독, 리소스 그룹 및 앱 서비스 계획을 입력 한 다음 클릭 **만들기**합니다.

    ![Visual Studio의 앱 서비스 만들기 대화 상자](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

몇 초 후에 Visual Studio에서 웹 응용 프로그램 게시를 완료하고 브라우저를 시작하며, Azure에서 실행되는 작업 내용을 확인할 수 있습니다.



## <a name="_Toc395637775"></a>다음 단계
축하합니다. 방금 첫 번째 ASP.NET MVC 웹 응용 프로그램을 Azure Cosmos DB를 사용 하 여 작성 하 고 tooAzure 게시 합니다. hello 전체 응용 프로그램의 경우 hello 세부 정보를 포함 하 여 소스 코드를 hello 및 삭제이 포함 되지 않은 기능 자습서를 다운로드 하거나에서 복제 된 항목 수 [GitHub][GitHub]합니다. 따라서 추가 tooyour 이러한 앱에 관심이 hello 코드 잡은 toothis 앱을 추가 합니다.

tooadd 추가 기능 tooyour 응용 프로그램을 검토 hello hello에서 사용할 수 있는 Api [Azure Cosmos DB.NET 라이브러리](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) 무료 toocontribute toohello Azure Cosmos DB.NET 라이브러리에 여겨지는 [GitHub] [GitHub]. 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
