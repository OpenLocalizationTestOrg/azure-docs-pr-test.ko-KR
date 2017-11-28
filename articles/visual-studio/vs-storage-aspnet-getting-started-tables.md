---
title: "Azure Table Storage 및 Visual Studio 연결 서비스 시작(ASP.NET) | Microsoft Docs"
description: "Visual Studio 연결 서비스를 사용하여 저장소 계정에 연결한 후 Visual Studio ASP.NET 프로젝트에서 Azure Table Storage 사용을 시작하는 방법입니다."
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
ms.openlocfilehash: 32a57e77bf6fe3cff88b9d6772ede9e6669ec75f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="8a406-103">Azure Table Storage 및 Visual Studio 연결 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="8a406-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="8a406-104">개요</span><span class="sxs-lookup"><span data-stu-id="8a406-104">Overview</span></span>

<span data-ttu-id="8a406-105">Azure 테이블 저장소를 사용하면 많은 양의 구조화된 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-105">Azure Table storage enables you to store large amounts of structured data.</span></span> <span data-ttu-id="8a406-106">이 서비스는 Azure 클라우드 내부 및 외부에서 인증된 호출을 수락하는 NoSQL 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-106">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="8a406-107">Azure 테이블은 구조화된 비관계형 데이터를 저장하는 데 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="8a406-108">이 자습서에서는 Azure Table Storage 항목을 사용하여 몇 가지 일반적인 시나리오에 대한 ASP.NET 코드를 작성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="8a406-109">이러한 시나리오는 테이블 만들기 및 테이블 엔터티 추가, 쿼리 및 삭제를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="8a406-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8a406-110">Prerequisites</span></span>

* [<span data-ttu-id="8a406-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8a406-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="8a406-112">Azure 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="8a406-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="8a406-113">MVC 컨트롤러 만들기</span><span class="sxs-lookup"><span data-stu-id="8a406-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="8a406-114">**솔루션 탐색기**에서 **컨트롤러**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->컨트롤러**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![ASP.NET MVC 앱에 컨트롤러 추가](./media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="8a406-116">**스캐폴드 추가** 대화 상자에서 **MVC 5 컨트롤러 - 비어 있음**을 선택하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![MVC 컨트롤러 유형 지정](./media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="8a406-118">**컨트롤러 추가** 대화 상자에서 컨트롤러 이름을*TablesController*로 설정하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-118">On the **Add Controller** dialog, name the controller *TablesController*, and select **Add**.</span></span>

    ![MVC 컨트롤러 이름 지정](./media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="8a406-120">다음 *using* 지시문을 `TablesController.cs` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-120">Add the following *using* directives to the `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="8a406-121">모델 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="8a406-121">Create a model class</span></span>

<span data-ttu-id="8a406-122">이 문서에서 대부분의 예제는 **CustomerEntity**라는 **TableEntity** 파생 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-122">Many of the examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="8a406-123">다음 단계는 모델 클래스로 이 클래스를 선언하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-123">The following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="8a406-124">**솔루션 탐색기**에서 **모델**을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->클래스**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-124">In the **Solution Explorer**, right-click **Models**, and, from the context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="8a406-125">**새 항목 추가** 대화 상자에서 클래스의 이름을 **CustomerEntity**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-125">On the **Add New Item** dialog, name the class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="8a406-126">`CustomerEntity.cs` 파일을 열고 다음 **using** 지시문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-126">Open the `CustomerEntity.cs` file, and add the following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="8a406-127">완료되면 클래스가 다음 코드와 같이 선언되도록 클래스를 해당 내용으로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-127">Modify the class so that, when finished, the class is declared as in the following code.</span></span> <span data-ttu-id="8a406-128">클래스는 고객의 이름을 행 키로 사용하고 성을 파티션 키로 사용하는 **CustomerEntity**라는 엔터티 클래스를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-128">The class declares an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span></span>

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

## <a name="create-a-table"></a><span data-ttu-id="8a406-129">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="8a406-129">Create a table</span></span>

<span data-ttu-id="8a406-130">다음 단계에서는 테이블을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-130">The following steps illustrate how to create a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="8a406-131">이 섹션에서는 [개발 환경 설정](#set-up-the-development-environment)의 단계를 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-131">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="8a406-132">`TablesController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-132">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="8a406-133">**ActionResult**를 반환하는 **CreateTable**이라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="8a406-134">**CreateTable** 메서드 내에서 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-134">Within the **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8a406-135">다음 코드를 사용하여 Azure 서비스 구성에서 저장소 연결 문자열과 저장소 계정 정보를 가져옵니다(*&lt;storage-account-name>*을 액세스하는 Azure 저장소 계정의 이름으로 변경).</span><span class="sxs-lookup"><span data-stu-id="8a406-135">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="8a406-136">Table service 클라이언트를 나타내는 **CloudTableClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="8a406-137">원하는 테이블 이름에 대한 참조를 나타내는 **CloudTable** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-137">Get a **CloudTable** object that represents a reference to the desired table name.</span></span> <span data-ttu-id="8a406-138">**CloudTableClient.GetTableReference** 메서드는 테이블 저장소에 대한 요청을 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-138">The **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="8a406-139">테이블이 있는지 여부에 관계없이 참조가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-139">The reference is returned whether or not the table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="8a406-140">테이블이 아직 없으면 **CloudTable.CreateIfNotExists** 메서드를 호출하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-140">Call the **CloudTable.CreateIfNotExists** method to create the table if it does not yet exist.</span></span> <span data-ttu-id="8a406-141">테이블이 없는 경우 테이블이 성공적으로 생성되면 **CloudTable.CreateIfNotExists** 메서드는 **true**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-141">The **CloudTable.CreateIfNotExists** method returns **true** if the table does not exist, and is successfully created.</span></span> <span data-ttu-id="8a406-142">그렇지 않으면 **false**가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="8a406-143">**ViewBag**을 테이블의 이름으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-143">Update the **ViewBag** with the name of the table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="8a406-144">**솔루션 탐색기**에서 **보기** 폴더를 확장한 다음 **Tables**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->보기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-144">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="8a406-145">**보기 추가** 대화 상자에서 보기 이름으로 **CreateTable**을 입력하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-145">On the **Add View** dialog, enter **CreateTable** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="8a406-146">`CreateTable.cshtml`을 열고 다음 코드 조각과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-146">Open `CreateTable.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="8a406-147">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-147">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8a406-148">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-148">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="8a406-149">응용 프로그램을 실행하고 **테이블 만들기**를 선택하여 다음 스크린샷과 유사한 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-149">Run the application, and select **Create table** to see results similar to the following screen shot:</span></span>
  
    ![테이블 만들기](./media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="8a406-151">앞에서 언급했듯이 테이블이 없고 만들어진 경우에만 **CloudTable.CreateIfNotExists** 메서드에서 **true**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-151">As mentioned previously, the **CloudTable.CreateIfNotExists** method returns **true** only when the table doesn't exist and is created.</span></span> <span data-ttu-id="8a406-152">따라서 테이블이 있을 때 앱을 실행하면 메서드에서 **false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-152">Therefore, if you run the app when the table exists, the method returns **false**.</span></span> <span data-ttu-id="8a406-153">앱을 여러 번 실행하려면 앱을 다시 실행하기 전에 테이블을 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-153">To run the app multiple times, you must delete the table before running the app again.</span></span> <span data-ttu-id="8a406-154">**CloudTable.Delete** 메서드를 통해 테이블 삭제를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-154">Deleting the table can be done via the **CloudTable.Delete** method.</span></span> <span data-ttu-id="8a406-155">또한 [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) 또는 [Microsoft Azure Storage 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)를 사용하여 테이블을 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-155">You can also delete the table using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="8a406-156">테이블에 엔터티 추가</span><span class="sxs-lookup"><span data-stu-id="8a406-156">Add an entity to a table</span></span>

<span data-ttu-id="8a406-157">*엔터티*는 **TableEntity**에서 파생된 사용자 지정 클래스를 사용하여 C\# 개체에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-157">*Entities* map to C\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="8a406-158">테이블에 엔터티를 추가하려면 엔터티의 속성을 정의하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-158">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="8a406-159">이 섹션에서는 고객의 이름을 행 키로 사용하고 성을 파티션 키로 사용하는 엔터티 클래스를 정의하는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-159">In this section, you'll see how to define an entity class that uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="8a406-160">엔터티의 파티션과 행 키가 결합되어 테이블에서 엔터티를 고유하게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-160">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="8a406-161">동일한 파티션 키를 가진 엔터티는 다른 파티션 키를 가진 엔터티보다 더 빨리 쿼리할 수 있지만 다양한 파티션 키를 사용하면 병렬 작업 확장성이 커집니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="8a406-162">테이블 서비스에 저장되어야 하는 속성의 경우 속성은 설정과 검색 값을 모두 표시하는 지원되는 형식의 공용 속성이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-162">For any property that should be stored in the table service, the property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="8a406-163">엔터티 클래스는 공용 매개 변수가 없는 생성자를 선언*해야* 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-163">The entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="8a406-164">이 섹션에서는 [개발 환경 설정](#set-up-the-development-environment)의 단계를 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-164">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="8a406-165">`TablesController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-165">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="8a406-166">`TablesController.cs` 파일의 코드가 **CustomerEntity** 클래스에 액세스할 수 있도록 다음 지시문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-166">Add the following directive so that the code in the `TablesController.cs` file can access the **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="8a406-167">**ActionResult**를 반환하는 **AddEntity**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="8a406-168">**AddEntity** 메서드 내에서 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-168">Within the **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8a406-169">다음 코드를 사용하여 Azure 서비스 구성에서 저장소 연결 문자열과 저장소 계정 정보를 가져옵니다(*&lt;storage-account-name>*을 액세스하는 Azure 저장소 계정의 이름으로 변경).</span><span class="sxs-lookup"><span data-stu-id="8a406-169">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="8a406-170">Table service 클라이언트를 나타내는 **CloudTableClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="8a406-171">새 엔터티를 추가하려는 테이블에 대한 참조를 나타내는 **CloudTable** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-171">Get a **CloudTable** object that represents a reference to the table to which you are going to add the new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="8a406-172">**CustomerEntity** 클래스를 인스턴스화 및 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-172">Instantiate and initialize the **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="8a406-173">customer 엔터티를 삽입하는 **TableOperation** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-173">Create a **TableOperation** object that inserts the customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="8a406-174">**CloudTable.Execute** 메서드를 호출하여 삽입 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-174">Execute the insert operation by calling the **CloudTable.Execute** method.</span></span> <span data-ttu-id="8a406-175">**TableResult.HttpStatusCode** 속성을 검사하여 작업의 결과를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-175">You can verify the result of the operation by inspecting the **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="8a406-176">상태 코드 2xx는 클라이언트에서 요청한 작업이 성공적으로 처리되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-176">A status code of 2xx indicates the action requested by the client was processed successfully.</span></span> <span data-ttu-id="8a406-177">예를 들어 새 엔터티를 성공적으로 삽입하면 작업이 성공적으로 처리되었고 서버가 어떤 콘텐츠도 반환하지 않았음을 의미하는 HTTP 상태 코드 204가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that the operation was successfully processed and the server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="8a406-178">**ViewBag**을 테이블 이름으로 업데이트하고 삽입 작업의 결과를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-178">Update the **ViewBag** with the table name, and the results of the insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="8a406-179">**솔루션 탐색기**에서 **보기** 폴더를 확장한 다음 **Tables**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->보기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-179">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="8a406-180">**보기 추가** 대화 상자에서 보기 이름으로 **AddEntity**를 입력하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-180">On the **Add View** dialog, enter **AddEntity** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="8a406-181">`AddEntity.cshtml`을 열고 다음 코드 조각과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-181">Open `AddEntity.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="8a406-182">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-182">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8a406-183">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-183">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="8a406-184">응용 프로그램을 실행하고 **엔터티 추가**를 선택하여 다음 스크린샷과 유사한 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-184">Run the application, and select **Add entity** to see results similar to the following screen shot:</span></span>
  
    ![엔터티 추가](./media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="8a406-186">[단일 엔터티 가져오기](#get-a-single-entity) 섹션의 단계를 수행하여 엔터티가 추가되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-186">You can verify that the entity was added by following the steps in the section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="8a406-187">[Microsoft Azure Storage 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)를 사용하여 테이블에 대한 모든 엔터티를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-187">You can also use the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to view all the entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-to-a-table"></a><span data-ttu-id="8a406-188">테이블에 엔터티를 일괄로 추가</span><span class="sxs-lookup"><span data-stu-id="8a406-188">Add a batch of entities to a table</span></span>

<span data-ttu-id="8a406-189">[한 번에 하나의 테이블에 엔터티를 추가](#add-an-entity-to-a-table)할 수 있을 뿐 아니라 엔터티를 일괄로 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-189">In addition to being able to [add an entity to a table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="8a406-190">엔터티를 일괄로 추가하면 코드와 Azure Table service 간의 왕복 수가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-190">Adding entities in batch reduces the number of round-trips between your code and the Azure table service.</span></span> <span data-ttu-id="8a406-191">다음 단계에서는 단일 삽입 작업으로 여러 엔터티를 테이블에 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-191">The following steps illustrate how to add multiple entities to a table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="8a406-192">이 섹션에서는 [개발 환경 설정](#set-up-the-development-environment)의 단계를 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-192">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="8a406-193">`TablesController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-193">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="8a406-194">**ActionResult**를 반환하는 **AddEntities**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="8a406-195">**AddEntities** 메서드 내에서 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-195">Within the **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8a406-196">다음 코드를 사용하여 Azure 서비스 구성에서 저장소 연결 문자열과 저장소 계정 정보를 가져옵니다(*&lt;storage-account-name>*을 액세스하는 Azure 저장소 계정의 이름으로 변경).</span><span class="sxs-lookup"><span data-stu-id="8a406-196">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="8a406-197">Table service 클라이언트를 나타내는 **CloudTableClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="8a406-198">새 엔터티를 추가하려는 테이블에 대한 참조를 나타내는 **CloudTable** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-198">Get a **CloudTable** object that represents a reference to the table to which you are going to add the new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="8a406-199">[테이블에 엔터티 추가](#add-an-entity-to-a-table) 섹션에 표시되는 **CustomerEntity** 모델 클래스에 따라 일부 고객 개체를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-199">Instantiate some customer objects based on the **CustomerEntity** model class presented in the section, [Add an entity to a table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="8a406-200">**TableBatchOperation** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="8a406-201">일괄 삽입 작업 개체에 엔터티를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-201">Add entities to the batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="8a406-202">**CloudTable.ExecuteBatch** 메서드를 호출하여 일괄 삽입 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-202">Execute the batch insert operation by calling the **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="8a406-203">**CloudTable.ExecuteBatch** 메서드는 **TableResult** 개체 목록을 반환합니다. 여기에서 각 개별 작업의 성공 여부를 확인하도록 각 **TableResult** 개체를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-203">The **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined to determine the success or failure of each individual operation.</span></span> <span data-ttu-id="8a406-204">이 예에서는 보기로 목록을 전달하고 보기에 각 작업의 결과를 표시하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-204">For this example, pass the list to a view and let the view display the results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="8a406-205">**솔루션 탐색기**에서 **보기** 폴더를 확장한 다음 **Tables**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->보기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="8a406-206">**보기 추가** 대화 상자에서 보기 이름으로 **AddEntities**를 입력하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-206">On the **Add View** dialog, enter **AddEntities** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="8a406-207">`AddEntities.cshtml`을 열고 다음과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-207">Open `AddEntities.cshtml`, and modify it so that it looks like the following.</span></span>

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

1. <span data-ttu-id="8a406-208">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8a406-209">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="8a406-210">응용 프로그램을 실행하고 **엔터티 추가**를 선택하여 다음 스크린샷과 유사한 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-210">Run the application, and select **Add entities** to see results similar to the following screen shot:</span></span>
  
    ![엔터티 추가](./media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="8a406-212">[단일 엔터티 가져오기](#get-a-single-entity) 섹션의 단계를 수행하여 엔터티가 추가되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-212">You can verify that the entity was added by following the steps in the section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="8a406-213">[Microsoft Azure Storage 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md)를 사용하여 테이블에 대한 모든 엔터티를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-213">You can also use the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to view all the entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="8a406-214">단일 엔터티 가져오기</span><span class="sxs-lookup"><span data-stu-id="8a406-214">Get a single entity</span></span>

<span data-ttu-id="8a406-215">이 섹션에서는 엔터티의 행 키 및 파티션 키를 사용하여 테이블에서 단일 엔터티를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-215">This section illustrates how to get a single entity from a table using the entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="8a406-216">이 섹션은 [개발 환경 설정](#set-up-the-development-environment)의 단계를 완료했다고 가정하고 [테이블에 엔터티를 일괄로 추가](#add-a-batch-of-entities-to-a-table)의 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-216">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="8a406-217">`TablesController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-217">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="8a406-218">**ActionResult**를 반환하는 **GetSingle**이라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="8a406-219">**GetSingle** 메서드 내에서 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-219">Within the **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8a406-220">다음 코드를 사용하여 Azure 서비스 구성에서 저장소 연결 문자열과 저장소 계정 정보를 가져옵니다(*&lt;storage-account-name>*을 액세스하는 Azure 저장소 계정의 이름으로 변경).</span><span class="sxs-lookup"><span data-stu-id="8a406-220">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="8a406-221">Table service 클라이언트를 나타내는 **CloudTableClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="8a406-222">엔터티를 검색하려는 테이블에 대한 참조를 나타내는 **CloudTable** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-222">Get a **CloudTable** object that represents a reference to the table from which you are retrieving the entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="8a406-223">**TableEntity**에서 파생된 엔터티 개체를 사용하는 검색 작업 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="8a406-224">첫 번째 매개 변수는 *partitionKey*이고, 두 번째 매개 변수는 *rowKey*입니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-224">The first parameter is the *partitionKey*, and the second parameter is the *rowKey*.</span></span> <span data-ttu-id="8a406-225">다음 코드 조각은 **CustomerEntity** 클래스 및 [테이블에 엔터티를 일괄로 추가](#add-a-batch-of-entities-to-a-table) 섹션에 표시되는 데이터를 사용하여 *partitionKey* 값 "Smith" 및 *rowKey* 값 "Ben"을 사용하여 테이블에서 **CustomerEntity** 엔터티를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-225">Using the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table), the following code snippet queries the table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="8a406-226">검색 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-226">Execute the retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="8a406-227">표시를 위해 결과를 보기에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-227">Pass the result to the view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="8a406-228">**솔루션 탐색기**에서 **보기** 폴더를 확장한 다음 **Tables**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->보기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-228">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="8a406-229">**보기 추가** 대화 상자에서 보기 이름으로 **GetSingle**을 입력하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-229">On the **Add View** dialog, enter **GetSingle** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="8a406-230">`GetSingle.cshtml`을 열고 다음 코드 조각과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-230">Open `GetSingle.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="8a406-231">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-231">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8a406-232">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-232">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="8a406-233">응용 프로그램을 실행하고 **단일 가져오기**를 선택하여 다음 스크린샷과 유사한 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-233">Run the application, and select **Get Single** to see results similar to the following screen shot:</span></span>
  
    ![단일 가져오기](./media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="8a406-235">파티션의 모든 엔터티 가져오기</span><span class="sxs-lookup"><span data-stu-id="8a406-235">Get all entities in a partition</span></span>

<span data-ttu-id="8a406-236">[테이블에 엔터티 추가](#add-an-entity-to-a-table) 섹션에서 설명했듯이 파티션 및 행 키의 조합은 테이블의 엔터티를 고유하게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-236">As mentioned in the section, [Add an entity to a table](#add-an-entity-to-a-table), the combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="8a406-237">동일한 파티션 키를 가진 엔터티는 다른 파티션 키를 가진 엔터티보다 더 빨리 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="8a406-238">이 섹션은 지정된 파티션에서 모든 엔터티에 대한 테이블을 쿼리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-238">This section illustrates how to query a table for all the entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="8a406-239">이 섹션은 [개발 환경 설정](#set-up-the-development-environment)의 단계를 완료했다고 가정하고 [테이블에 엔터티를 일괄로 추가](#add-a-batch-of-entities-to-a-table)의 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-239">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="8a406-240">`TablesController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-240">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="8a406-241">**ActionResult**를 반환하는 **GetPartition**이라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="8a406-242">**GetPartition** 메서드 내에서 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-242">Within the **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8a406-243">다음 코드를 사용하여 Azure 서비스 구성에서 저장소 연결 문자열과 저장소 계정 정보를 가져옵니다(*&lt;storage-account-name>*을 액세스하는 Azure 저장소 계정의 이름으로 변경).</span><span class="sxs-lookup"><span data-stu-id="8a406-243">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="8a406-244">Table service 클라이언트를 나타내는 **CloudTableClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="8a406-245">엔터티를 검색하려는 테이블에 대한 참조를 나타내는 **CloudTable** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-245">Get a **CloudTable** object that represents a reference to the table from which you are retrieving the entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="8a406-246">**TableQuery** 개체를 인스턴스화하고 **Where** 절에 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-246">Instantiate a **TableQuery** object specifying the query in the **Where** clause.</span></span> <span data-ttu-id="8a406-247">다음 코드 조각은 **CustomerEntity** 클래스 및 [테이블에 엔터티를 일괄로 추가](#add-a-batch-of-entities-to-a-table) 섹션에 표시되는 데이터를 사용하여 **PartitionKey**(고객의 성) 값이 "Smith"인 모든 엔터티를 테이블에서 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-247">Using the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table), the following code snippet queries the table for a all entities where the **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="8a406-248">루프 내에서 **CloudTable.ExecuteQuerySegmented** 메서드를 호출하고 이전 단계에서 인스턴스화한 쿼리 개체를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-248">Within a loop, call the **CloudTable.ExecuteQuerySegmented** method passing the query object you instantiated in the previous step.</span></span>  <span data-ttu-id="8a406-249">**CloudTable.ExecuteQuerySegmented** 메서드는 **TableContinuationToken** 개체를 반환합니다. 이 개체는 **null**인 경우 검색할 추가 엔터티가 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-249">The **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities to retrieve.</span></span> <span data-ttu-id="8a406-250">루프 내에서 다른 루프를 사용하여 반환된 엔터티를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-250">Within the loop, use another loop to iterate over the returned entities.</span></span> <span data-ttu-id="8a406-251">다음 코드 예제에서는 반환된 각 엔터티가 목록에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-251">In the following code example, each returned entity is added to a list.</span></span> <span data-ttu-id="8a406-252">루프가 종료되면 표시를 위해 목록이 보기에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-252">Once the loop ends, the list is passed to a view for display:</span></span> 

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

1. <span data-ttu-id="8a406-253">**솔루션 탐색기**에서 **보기** 폴더를 확장한 다음 **Tables**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->보기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-253">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="8a406-254">**보기 추가** 대화 상자에서 보기 이름으로 **GetPartition**을 입력하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-254">On the **Add View** dialog, enter **GetPartition** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="8a406-255">`GetPartition.cshtml`을 열고 다음 코드 조각과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-255">Open `GetPartition.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="8a406-256">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-256">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8a406-257">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-257">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="8a406-258">응용 프로그램을 실행하고 **파티션 가져오기**를 선택하여 다음 스크린샷과 유사한 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-258">Run the application, and select **Get Partition** to see results similar to the following screen shot:</span></span>
  
    ![파티션 가져오기](./media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="8a406-260">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="8a406-260">Delete an entity</span></span>

<span data-ttu-id="8a406-261">이 섹션에서는 테이블에서 엔터티를 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-261">This section illustrates how to delete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="8a406-262">이 섹션은 [개발 환경 설정](#set-up-the-development-environment)의 단계를 완료했다고 가정하고 [테이블에 엔터티를 일괄로 추가](#add-a-batch-of-entities-to-a-table)의 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-262">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="8a406-263">`TablesController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-263">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="8a406-264">**ActionResult**를 반환하는 **DeleteEntity**라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="8a406-265">**DeleteEntity** 메서드 내에서 저장소 계정 정보를 나타내는 **CloudStorageAccount** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-265">Within the **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8a406-266">다음 코드를 사용하여 Azure 서비스 구성에서 저장소 연결 문자열과 저장소 계정 정보를 가져옵니다(*&lt;storage-account-name>*을 액세스하는 Azure 저장소 계정의 이름으로 변경).</span><span class="sxs-lookup"><span data-stu-id="8a406-266">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="8a406-267">Table service 클라이언트를 나타내는 **CloudTableClient** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="8a406-268">엔터티를 삭제하려는 테이블에 대한 참조를 나타내는 **CloudTable** 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-268">Get a **CloudTable** object that represents a reference to the table from which you are deleting the entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="8a406-269">**TableEntity**에서 파생된 엔터티 개체를 사용하는 삭제 작업 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="8a406-270">이 경우 **CustomerEntity** 클래스 및 [테이블에 엔터티를 일괄로 추가](#add-a-batch-of-entities-to-a-table) 섹션에 표시되는 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-270">In this case, we use the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="8a406-271">엔터티의 **ETag**는 유효한 값으로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-271">The entity's **ETag** must be set to a valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="8a406-272">삭제 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-272">Execute the delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="8a406-273">표시를 위해 결과를 보기에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-273">Pass the result to the view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="8a406-274">**솔루션 탐색기**에서 **보기** 폴더를 확장한 다음 **Tables**를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **추가->보기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-274">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="8a406-275">**보기 추가** 대화 상자에서 보기 이름으로 **DeleteEntity**를 입력하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-275">On the **Add View** dialog, enter **DeleteEntity** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="8a406-276">`DeleteEntity.cshtml`을 열고 다음 코드 조각과 같이 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="8a406-277">**솔루션 탐색기**에서 **보기->공유됨** 폴더를 차례로 확장하고 `_Layout.cshtml`을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-277">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8a406-278">마지막 **Html.ActionLink** 뒤에 다음 **Html.ActionLink**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-278">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="8a406-279">응용 프로그램을 실행하고 **엔터티 삭제**를 선택하여 다음 스크린샷과 유사한 결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8a406-279">Run the application, and select **Delete entity** to see results similar to the following screen shot:</span></span>
  
    ![단일 가져오기](./media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="8a406-281">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8a406-281">Next steps</span></span>
<span data-ttu-id="8a406-282">Azure에 데이터를 저장하기 위한 추가 옵션에 대한 자세한 내용은 추가 기능 가이드를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="8a406-282">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="8a406-283">Azure Blob 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="8a406-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="8a406-284">Azure 큐 저장소 및 Visual Studio 연결된 서비스 시작(ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="8a406-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](../storage/vs-storage-aspnet-getting-started-queues.md)
