---
title: "Azure 테이블 저장소 및 Visual Studio 연결 된 서비스 (ASP.NET) aaaGet 시작 | Microsoft Docs"
description: "Visual Studio에서 ASP.NET 프로젝트에서 Azure 테이블 저장소를 사용 하 여 Visual Studio 연결 된 서비스를 사용 하 여 tooa 저장소 계정을 연결한 후 tooget을 시작 하는 방법"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: af81a326-18f4-4449-bc0d-e96fba27c1f8
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraigb
ms.openlocfilehash: 04f79db7aad60ca51c3c866da1f4b01d9e11ac52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a>Azure Table Storage 및 Visual Studio 연결 서비스 시작
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>개요

Azure 테이블 저장소에서는 많은 양의 구조화 된 데이터를 toostore 있습니다. hello 서비스는 내부 및 외부 hello Azure 클라우드에서 인증 된 호출을 허용 하는 NoSQL 데이터 저장소입니다. Azure 테이블은 구조화된 비관계형 데이터를 저장하는 데 적합합니다.

이 자습서에서는 Azure 테이블 저장소 엔터티를 사용 하 여 몇 가지 일반적인 시나리오에 대 한 ASP.NET toowrite 코드 하는 방법을 보여 줍니다. 이러한 시나리오는 테이블 만들기 및 테이블 엔터티 추가, 쿼리 및 삭제를 포함합니다. 

##<a name="prerequisites"></a>필수 조건

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure 저장소 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>MVC 컨트롤러 만들기 

1. Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **컨트롤러**, hello 상황에 맞는 메뉴에서 **추가-컨트롤러 >**합니다.

    ![컨트롤러 tooan ASP.NET MVC 응용 프로그램 추가](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. Hello에 **추가 스 캐 폴드** 대화 상자에서 **MVC 5 컨트롤러-비어 있지**, 선택한 **추가**합니다.

    ![MVC 컨트롤러 유형 지정](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. Hello에 **컨트롤러 추가** 대화 상자에서 이름 hello 컨트롤러 *TablesController*를 선택 하 고 **추가**합니다.

    ![Hello MVC 컨트롤러 이름](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. Hello 다음 추가 *를 사용 하 여* 지시문 toohello `TablesController.cs` 파일:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a>모델 클래스 만들기

사용 하 여 다양 한 hello 예제가 문서는 **TableEntity**-라는 클래스를 파생 **CustomerEntity**합니다. 단계를 수행 하는 hello 모델 클래스와이 클래스를 선언 하는 과정을 안내 합니다.

1. Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **모델**, hello 상황에 맞는 메뉴에서 **추가-클래스 >**합니다.

1. Hello에 **새 항목 추가** 대화 상자에서 이름 hello 클래스 **CustomerEntity**합니다.

1. 열기 hello `CustomerEntity.cs` 파일을 선택한 다음 hello 추가 **를 사용 하 여** 지시문:

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. 완료 되 면 hello 클래스는 코드 다음 hello와 같이 선언 됩니다 되도록 hello 클래스를 수정 합니다. 라고 하는 엔터티 클래스를 선언 하는 hello 클래스 **CustomerEntity** hello 행 키로 고객의 이름 및 성 hello 파티션 키로 사용 하 여 hello 하 합니다.

    ```csharp
    public class CustomerEntity : TableEntity
    {
        public CustomerEntity(string lastName, string firstName)
        {
            this.PartitionKey = lastName;
            this.RowKey = firstName;
        }

        public CustomerEntity() { }

        public string Email { get; set; }
    }
    ```

## <a name="create-a-table"></a>테이블 만들기

hello 아래 단계에 설명 방법을 toocreate 테이블:

> [!NOTE]
> 
> 이 섹션의 hello 단계를 완료 하는 것으로 가정 [hello 개발 환경 설정](#set-up-the-development-environment)합니다. 

1. 열기 hello `TablesController.cs` 파일입니다.

1. **ActionResult**를 반환하는 **CreateTable**이라는 메서드를 추가합니다.

    ```csharp
    public ActionResult CreateTable()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Hello 내 **CreateTable** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다. 사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Table service 클라이언트를 나타내는 **CloudTableClient** 개체를 가져옵니다.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. 가져오기는 **CloudTable** 참조 toohello 원하는 테이블 이름을 나타내는 개체입니다. hello **CloudTableClient.GetTableReference** 메서드 테이블 저장소에 대 한 요청을 만들지 않습니다. hello 테이블이 존재 여부 hello 참조가 반환 됩니다. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Hello 호출 **CloudTable.CreateIfNotExists** 메서드 toocreate hello 테이블이 아직 존재 하지 않는 경우. hello **CloudTable.CreateIfNotExists** 메서드 반환 **true** hello 테이블이 존재 하지 않는 성공적으로 생성 되는 경우. 그렇지 않으면 **false**가 반환됩니다.    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. 업데이트 hello **ViewBag** hello 테이블의 hello 이름의 합니다.

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **테이블**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.

1. Hello에 **뷰 추가** 대화 상자에서 입력 **CreateTable** hello 뷰 이름과 선택에 대 한 **추가**합니다.

1. 열기 `CreateTable.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **테이블 만들기** toosee 스크린 샷 다음 유사한 toohello 결과:
  
    ![테이블 만들기](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    앞에서 설명한 대로 hello **CloudTable.CreateIfNotExists** 메서드 반환 **true** hello 테이블 존재 하지 않는 있고 만들어지는 경우에 합니다. 따라서 hello 테이블이 존재 하는 경우 hello 앱을 실행 하면 hello 메서드는 반환 **false**합니다. toorun hello 앱 여러 번 삭제 해야 hello 테이블 hello 응용 프로그램을 다시 실행 하기 전에. Hello 통해 hello 테이블 삭제를 수행할 수 있습니다 **CloudTable.Delete** 메서드. Hello를 사용 하 여 hello 테이블을 삭제할 수도 있습니다 [Azure 포털](http://go.microsoft.com/fwlink/p/?LinkID=525040) 또는 hello [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)합니다.  

## <a name="add-an-entity-tooa-table"></a>엔터티 tooa 테이블 추가

*엔터티* tooC 매핑할\# 사용자 지정 클래스를 사용 하 여 개체에서 파생 된 **TableEntity**합니다. 엔터티 tooa 테이블 tooadd hello 엔터티 속성을 정의 하는 클래스를 만듭니다. 이 섹션에서는 hello 행 키로 고객의 이름 및 성 hello 파티션 키로 사용 하는 엔터티 클래스 toodefine hello 하는 방법을 볼 수 있습니다. 함께 엔터티의 파티션과 행 키는 hello 엔터티 hello 테이블에 고유 하 게 식별 합니다. 동일한 파티션 키를 가진 엔터티는 다른 파티션 키를 가진 엔터티보다 더 빨리 쿼리할 수 있지만 다양한 파티션 키를 사용하면 병렬 작업 확장성이 커집니다. Hello 테이블 서비스에 저장 해야 하는 모든 속성에 대 한 hello 속성 노출 설정 하 고 값을 검색 하는 지원 되는 형식의 공용 속성 이어야 합니다.
엔터티 클래스를 hello *해야* 공용 매개 변수 없는 생성자를 선언 합니다.

> [!NOTE]
> 
> 이 섹션의 hello 단계를 완료 하는 것으로 가정 [hello 개발 환경 설정](#set-up-the-development-environment)합니다.

1. 열기 hello `TablesController.cs` 파일입니다.

1. 추가 하는 hello hello에 대 한 코드 하므로 지시문 다음 hello `TablesController.cs` hello 파일에 액세스할 수 **CustomerEntity** 클래스:

    ```csharp
    using StorageAspnet.Models;
    ```

1. **ActionResult**를 반환하는 **AddEntity**라는 메서드를 추가합니다.

    ```csharp
    public ActionResult AddEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Hello 내 **AddEntity** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다. 사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Table service 클라이언트를 나타내는 **CloudTableClient** 개체를 가져옵니다.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. 가져오기는 **CloudTable** 참조 toohello 테이블 toowhich를 tooadd hello에 대 한 새 엔터티는 것을 나타내는 개체입니다. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. 인스턴스화 및 초기화 hello **CustomerEntity** 클래스입니다.

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. 만들기는 **TableOperation** hello customer 엔터티를 삽입 하는 개체입니다.

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. 호출 hello 여 hello 삽입 작업을 실행 **CloudTable.Execute** 메서드. Hello를 검사 하 여 hello 연산의 hello 결과 확인할 수 있습니다 **TableResult.HttpStatusCode** 속성입니다. 2xx의 상태 코드가 나타냅니다 hello 클라이언트에서 요청 된 hello 동작을 처리 했습니다. 예를 들어 성공적으로 삽입 한 새 엔터티는 HTTP 상태 코드 204, 즉 hello 작업이 성공적으로 처리 되 고 hello 서버는 콘텐츠를 반환 하지 않았습니다 발생 합니다.

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. 업데이트 hello **ViewBag** hello 테이블 이름 및 hello 삽입 작업의 hello 결과 포함 합니다.

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **테이블**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.

1. Hello에 **뷰 추가** 대화 상자에서 입력 **AddEntity** hello 뷰 이름과 선택에 대 한 **추가**합니다.

1. 열기 `AddEntity.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **엔터티 추가** toosee 스크린 샷 다음 유사한 toohello 결과:
  
    ![엔터티 추가](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    Hello 엔터티 hello 섹션의 hello 단계에 따라 추가 되는지 확인할 수 있습니다 [단일 엔터티를 가져올](#get-a-single-entity)합니다. Hello를 사용할 수도 있습니다 [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview 모든 테이블에 대 한 엔터티를 hello 합니다.

## <a name="add-a-batch-of-entities-tooa-table"></a>엔터티 tooa 테이블의 일괄 처리 추가

또한 toobeing 수에 너무[한 번에 하나씩는 엔터티 tooa 테이블 추가](#add-an-entity-to-a-table), 일괄 처리에서 엔터티를 추가할 수도 있습니다. 엔터티 일괄 처리의 추가 hello 수가 줄어 코드와 hello Azure 테이블 서비스 간의 왕복 회수 합니다. 단계를 수행 하는 hello 방법을 tooadd 여러 엔터티 tooa 테이블의 단일 삽입 작업을 보여 줍니다.

> [!NOTE]
> 
> 이 섹션의 hello 단계를 완료 하는 것으로 가정 [hello 개발 환경 설정](#set-up-the-development-environment)합니다.

1. 열기 hello `TablesController.cs` 파일입니다.

1. **ActionResult**를 반환하는 **AddEntities**라는 메서드를 추가합니다.

    ```csharp
    public ActionResult AddEntities()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Hello 내 **AddEntities** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다. 사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Table service 클라이언트를 나타내는 **CloudTableClient** 개체를 가져옵니다.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. 가져오기는 **CloudTable** 하락 tooadd hello에 대 한 새 엔터티는 한 참조 toohello 테이블 toowhich를 나타내는 개체입니다. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. Hello에 따라 일부 고객 개체를 인스턴스화할 **CustomerEntity** 모델 hello 섹션에 제공 된 클래스 [엔터티 tooa 테이블 추가](#add-an-entity-to-a-table)합니다.

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. **TableBatchOperation** 개체를 가져옵니다.

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. 엔터티 toohello 일괄 처리 삽입 작업 개체를 추가 합니다.

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. 호출 hello 여 hello 일괄 처리 삽입 작업을 실행 **CloudTable.ExecuteBatch** 메서드.   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. hello **CloudTable.ExecuteBatch** 메서드 목록을 반환 **TableResult** 개체 여기서 각 **TableResult** 개체 검사 toodetermine hello 성공 또는 실패 수 각 개별 작업입니다. 예를 들어 각 작업의 hello 결과 표시 하는 hello 보기를 hello 목록 tooa 뷰에 전달 됩니다. 
 
    ```csharp
    return View(results);
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **테이블**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.

1. Hello에 **뷰 추가** 대화 상자에서 입력 **AddEntities** hello 뷰 이름과 선택에 대 한 **추가**합니다.

1. 열기 `AddEntities.cshtml`, 및을 hello 다음과 같이 수정 합니다.

    ```csharp
    @model IEnumerable<Microsoft.WindowsAzure.Storage.Table.TableResult>
    @{
        ViewBag.Title = "AddEntities";
    }
    
    <h2>Add-entities results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        @foreach (var result in Model)
        {
        <tr>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@result.HttpStatusCode</td>
        </tr>
        }
    </table>
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **엔터티를 추가** toosee 스크린 샷 다음 유사한 toohello 결과:
  
    ![엔터티 추가](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    Hello 엔터티 hello 섹션의 hello 단계에 따라 추가 되는지 확인할 수 있습니다 [단일 엔터티를 가져올](#get-a-single-entity)합니다. Hello를 사용할 수도 있습니다 [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooview 모든 테이블에 대 한 엔터티를 hello 합니다.

## <a name="get-a-single-entity"></a>단일 엔터티 가져오기

이 섹션에서는 엔터티의 행 키 및 파티션 키 사용 하 여 테이블에서 단일 엔터티 tooget hello 하는 방법을 보여 줍니다. 

> [!NOTE]
> 
> 이 섹션의 hello 단계를 완료 하는 것으로 가정 [hello 개발 환경 설정](#set-up-the-development-environment), 데이터를 사용 하 고 [엔터티 tooa 테이블의 일괄 처리 추가](#add-a-batch-of-entities-to-a-table)합니다. 

1. 열기 hello `TablesController.cs` 파일입니다.

1. **ActionResult**를 반환하는 **GetSingle**이라는 메서드를 추가합니다.

    ```csharp
    public ActionResult GetSingle()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Hello 내 **GetSingle** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다. 사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Table service 클라이언트를 나타내는 **CloudTableClient** 개체를 가져옵니다.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. 가져오기는 **CloudTable** hello 엔터티 가져오려는 참조 toohello 테이블을 나타내는 개체입니다. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. **TableEntity**에서 파생된 엔터티 개체를 사용하는 검색 작업 개체를 만듭니다. hello 첫 번째 매개 변수는 hello *partitionKey*, hello 두 번째 매개 변수는 hello 및 *rowKey*합니다. Hello를 사용 하 여 **CustomerEntity** 클래스 및 hello 섹션에 제공 된 데이터 [엔터티 tooa 테이블의 일괄 처리 추가](#add-a-batch-of-entities-to-a-table), 다음 코드 조각 쿼리 hello 테이블에 대 한 hello는 **CustomerEntity** 인 엔터티는 *partitionKey* "Smith"의 값 및 *rowKey* "Ben"의 값:

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. Hello 검색 작업을 실행 합니다.   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. 디스플레이 대 한 hello 결과 toohello 보기를 전달 합니다.

    ```csharp
    return View(result);
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **테이블**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.

1. Hello에 **뷰 추가** 대화 상자에서 입력 **GetSingle** hello 뷰 이름과 선택에 대 한 **추가**합니다.

1. 열기 `GetSingle.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "GetSingle";
    }
    
    <h2>Get Single results</h2>
    
    <table border="1">
        <tr>
            <th>HTTP result</th>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        <tr>
            <td>@Model.HttpStatusCode</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).Email)</td>
        </tr>
    </table>
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **단일 가져오기** toosee 스크린 샷 다음 유사한 toohello 결과:
  
    ![단일 가져오기](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a>파티션의 모든 엔터티 가져오기

Hello 섹션에서 설명한 것 처럼 [엔터티 tooa 테이블 추가](#add-an-entity-to-a-table)는 파티션 및 행 키의 hello 조합 테이블에서 엔터티를 고유 하 게 식별 합니다. 동일한 파티션 키를 가진 엔터티는 다른 파티션 키를 가진 엔터티보다 더 빨리 쿼리할 수 있습니다. 이 섹션에서는 어떻게 tooquery에서 지정된 된 파티션의 모든 hello 엔터티에 대 한 테이블입니다.  

> [!NOTE]
> 
> 이 섹션의 hello 단계를 완료 하는 것으로 가정 [hello 개발 환경 설정](#set-up-the-development-environment), 데이터를 사용 하 고 [엔터티 tooa 테이블의 일괄 처리 추가](#add-a-batch-of-entities-to-a-table)합니다. 

1. 열기 hello `TablesController.cs` 파일입니다.

1. **ActionResult**를 반환하는 **GetPartition**이라는 메서드를 추가합니다.

    ```csharp
    public ActionResult GetPartition()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Hello 내 **GetPartition** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다. 사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Table service 클라이언트를 나타내는 **CloudTableClient** 개체를 가져옵니다.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. 가져오기는 **CloudTable** hello 엔터티 가져오려는 참조 toohello 테이블을 나타내는 개체입니다. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. 인스턴스화하는 **TableQuery** hello에 hello 쿼리를 지정 하는 개체 **여기서** 절. Hello를 사용 하 여 **CustomerEntity** 클래스 및 hello 섹션에 제공 된 데이터 [엔터티 tooa 테이블의 일괄 처리 추가](#add-a-batch-of-entities-to-a-table), 여기서 hello hello 다음 코드 조각 쿼리 hello 테이블 모든 엔터티에 대 한  **PartitionKey** (고객의 성을) "Smith"의 값이 있습니다.

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. 루프 내에서 호출 hello **CloudTable.ExecuteQuerySegmented** hello 이전 단계에서 인스턴스화한 hello 쿼리 개체를 전달 합니다.  hello **CloudTable.ExecuteQuerySegmented** 메서드가 반환 되는 **TableContinuationToken** 개체를-때 **null** -더 많은 엔터티가 있는 tooretrieve 합니다. Hello 루프 내에서 엔터티를 반환 하는 hello를 통해 다른 루프 tooiterate를 사용 합니다. 다음 코드 예제는 hello, tooa 목록 각 반환 된 엔터티를 추가 합니다. 루프 끝을 한 번 hello, hello 목록 표시에 대 한 tooa 보기 전달 됩니다. 

    ```csharp
    List<CustomerEntity> customers = new List<CustomerEntity>();
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = table.ExecuteQuerySegmented(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity customer in resultSegment.Results)
        {
            customers.Add(customer);
        }
    } while (token != null);

    return View(customers);
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **테이블**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.

1. Hello에 **뷰 추가** 대화 상자에서 입력 **GetPartition** hello 뷰 이름과 선택에 대 한 **추가**합니다.

1. 열기 `GetPartition.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.

    ```csharp
    @model IEnumerable<StorageAspnet.Models.CustomerEntity>
    @{
        ViewBag.Title = "GetPartition";
    }
    
    <h2>Get Partition results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        @foreach (var customer in Model)
        {
        <tr>
            <td>@(customer.RowKey)</td>
            <td>@(customer.PartitionKey)</td>
            <td>@(customer.Email)</td>
        </tr>
        }
    </table>
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **가져올 파티션** toosee 스크린 샷 다음 유사한 toohello 결과:
  
    ![파티션 가져오기](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a>엔터티 삭제

이 섹션에서는 어떻게 toodelete 테이블에서 엔터티.

> [!NOTE]
> 
> 이 섹션의 hello 단계를 완료 하는 것으로 가정 [hello 개발 환경 설정](#set-up-the-development-environment), 데이터를 사용 하 고 [엔터티 tooa 테이블의 일괄 처리 추가](#add-a-batch-of-entities-to-a-table)합니다. 

1. 열기 hello `TablesController.cs` 파일입니다.

1. **ActionResult**를 반환하는 **DeleteEntity**라는 메서드를 추가합니다.

    ```csharp
    public ActionResult DeleteEntity()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Hello 내 **DeleteEntity** 메서드를 가져오기는 **CloudStorageAccount** 저장소 계정 정보를 나타내는 개체입니다. 사용 하 여 hello 다음 코드 tooget hello 저장소 연결 문자열 및 저장소 계정 정보 hello Azure 서비스 구성: (변경  *&lt;저장소 계정 이름 >* hello Azure 저장소의 toohello 이름 계정에 액세스할 때는입니다.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Table service 클라이언트를 나타내는 **CloudTableClient** 개체를 가져옵니다.
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. 가져오기는 **CloudTable** hello 엔터티는 삭제할 참조 toohello 테이블을 나타내는 개체입니다. 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. **TableEntity**에서 파생된 엔터티 개체를 사용하는 삭제 작업 개체를 만듭니다. 이 경우 hello 사용 **CustomerEntity** 클래스 및 hello 섹션에 제공 된 데이터 [엔터티 tooa 테이블의 일괄 처리 추가](#add-a-batch-of-entities-to-a-table)합니다. 엔터티의 hello **ETag** tooa 유효한 값을 설정 해야 합니다.  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. Hello 삭제 작업을 수행 합니다.   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. 디스플레이 대 한 hello 결과 toohello 보기를 전달 합니다.

    ```csharp
    return View(result);
    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰** 폴더를 마우스 오른쪽 단추로 클릭 **테이블**, hello 상황에 맞는 메뉴에서 선택 하 고 **추가보기->**.

1. Hello에 **뷰 추가** 대화 상자에서 입력 **DeleteEntity** hello 뷰 이름과 선택에 대 한 **추가**합니다.

1. 열기 `DeleteEntity.cshtml`, 다음 코드 조각 hello 모양이 되도록 수정 합니다.

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "DeleteEntity";
    }
    
    <h2>Delete Entity results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        <tr>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@Model.HttpStatusCode</td>
        </tr>
    </table>

    ```

1. Hello에 **솔루션 탐색기**, hello 확장 **뷰 공유->** 폴더를 연 `_Layout.cshtml`합니다.

1. Hello 후 마지막 **Html.ActionLink**, hello 다음 추가 **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. Hello 응용 프로그램을 실행 하 고 선택 **엔터티 삭제** toosee 스크린 샷 다음 유사한 toohello 결과:
  
    ![단일 가져오기](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a>다음 단계
Azure에 데이터를 저장 하기 위한 추가 옵션에 대 한 자세한 기능 가이드 toolearn을 봅니다.

  * [Azure Blob 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [Azure 큐 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)](../storage/vs-storage-aspnet-getting-started-queues.md)
