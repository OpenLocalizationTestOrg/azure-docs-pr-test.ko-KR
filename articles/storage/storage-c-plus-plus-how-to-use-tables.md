---
title: "aaaHow toouse 테이블 저장소 (c + +) | Microsoft Docs"
description: "Azure 테이블 저장소에는 NoSQL 데이터 저장소를 사용 하 여 hello 클라우드에서 구조화 된 데이터를 저장 합니다."
services: storage
documentationcenter: .net
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 8eee0031350ab6ff3f76fb288b2f896687aa17a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a><span data-ttu-id="4f79b-103">어떻게 toouse c + +에서 테이블 저장소</span><span class="sxs-lookup"><span data-stu-id="4f79b-103">How toouse Table storage from C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="4f79b-104">개요</span><span class="sxs-lookup"><span data-stu-id="4f79b-104">Overview</span></span>
<span data-ttu-id="4f79b-105">이 가이드 어떻게 tooperform 일반적인 시나리오를 사용 하 여 hello Azure 테이블 저장소 서비스에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-105">This guide will show you how tooperform common scenarios by using hello Azure Table storage service.</span></span> <span data-ttu-id="4f79b-106">hello 예제 c + +에서 작성 되 고 hello를 사용 하 여 [c + +에 대 한 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-cpp/blob/master/README.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-106">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="4f79b-107">hello 가이드에서 다루는 시나리오 포함 **만들고 테이블 삭제** 및 **테이블 엔터티 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-107">hello scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="4f79b-108">이 가이드의 대상으로 c + + 버전 1.0.0 이상용 Azure 저장소 클라이언트 라이브러리를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-108">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="4f79b-109">hello 권장 버전을 통해 사용할 수 있는 저장소 클라이언트 라이브러리, 2.2.0 [NuGet](http://www.nuget.org/packages/wastorage) 또는 [GitHub](https://github.com/Azure/azure-storage-cpp/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-109">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="4f79b-110">C++ 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="4f79b-110">Create a C++ application</span></span>
<span data-ttu-id="4f79b-111">이 가이드에서는 C++ 응용 프로그램 내에서 실행할 수 있는 저장소 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-111">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="4f79b-112">toodo tooinstall, 나오는 c + +에 대 한 Azure 저장소 클라이언트 라이브러리를 hello 및 Azure 구독에 Azure 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-112">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="4f79b-113">Azure 저장소 클라이언트 라이브러리 tooinstall hello c + +에 대 한 hello 다음 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-113">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="4f79b-114">**Linux:** hello에 대 한 부여 hello 지침에 따라 [c + + 추가 정보에 대 한 Azure 저장소 클라이언트 라이브러리](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) 페이지.</span><span class="sxs-lookup"><span data-stu-id="4f79b-114">**Linux:** Follow hello instructions given on hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="4f79b-115">**Windows:** Visual Studio에서 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-115">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="4f79b-116">Hello에 형식 hello 다음 명령은 [NuGet 패키지 관리자 콘솔](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-116">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="4f79b-117">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="4f79b-117">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="4f79b-118">사용자 응용 프로그램 tooaccess 테이블 저장소 구성</span><span class="sxs-lookup"><span data-stu-id="4f79b-118">Configure your application tooaccess Table storage</span></span>
<span data-ttu-id="4f79b-119">Hello 다음 포함 toouse hello Azure 저장소 Api tooaccess 테이블 저장할 hello c + + 파일의 문 toohello 맨 위에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="4f79b-120">Azure 저장소 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="4f79b-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="4f79b-121">Azure 저장소 클라이언트는 저장소 연결 문자열 toostore 끝점을 사용 하 여 및 데이터 관리 서비스에 액세스 하기 위한 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="4f79b-122">클라이언트 응용 프로그램을 실행할 때 형식에 따라 hello hello 저장소 연결 문자열을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-122">When running a client application, you must provide hello storage connection string in hello following format.</span></span> <span data-ttu-id="4f79b-123">저장소 계정 및 hello 저장소 액세스 키 hello 저장소 계정에 대 한 hello 이름을 사용 하 여 hello에 나열 된 [Azure 포털](https://portal.azure.com) hello에 대 한 *AccountName* 및 *AccountKey* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-123">Use hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="4f79b-124">저장소 계정 및 액세스 키에 대한 자세한 내용은 [Azure 저장소 계정 정보](storage-create-storage-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f79b-124">For information on storage accounts and access keys, see [About Azure storage accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="4f79b-125">이 예에서는 정적 필드 toohold hello 연결 문자열을 선언할 수는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-125">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="4f79b-126">tootest 응용 프로그램에서 로컬 Windows 기반 컴퓨터를 Azure hello를 사용할 수 있습니다 [저장소 에뮬레이터](storage-use-emulator.md) hello로 설치 된 [Azure SDK](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-126">tootest your application in your local Windows-based computer, you can use hello Azure [storage emulator](storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="4f79b-127">hello 저장소 에뮬레이터는 로컬 개발 컴퓨터에서 사용할 수 있는 하는 hello Azure Blob, 큐 및 테이블 서비스를 시뮬레이션 하는 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-127">hello storage emulator is a utility that simulates hello Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="4f79b-128">hello 다음 예제는 어떻게는 정적 필드 toohold hello 연결 문자열 tooyour 로컬 저장소 에뮬레이터를 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-128">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="4f79b-129">toostart hello Azure 저장소 에뮬레이터, hello 클릭 **시작** hello Windows 키 단추를 클릭 하거나 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-129">toostart hello Azure storage emulator, click hello **Start** button or press hello Windows key.</span></span> <span data-ttu-id="4f79b-130">입력을 시작 **Azure 저장소 에뮬레이터**를 선택한 후 **Microsoft Azure 저장소 에뮬레이터** hello 응용 프로그램 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-130">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="4f79b-131">hello 다음과 같은 샘플 가정 이러한 두 가지 방법 tooget hello 저장소 연결 문자열 중 하나 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-131">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="4f79b-132">연결 문자열 검색</span><span class="sxs-lookup"><span data-stu-id="4f79b-132">Retrieve your connection string</span></span>
<span data-ttu-id="4f79b-133">Hello를 사용할 수 있습니다 **cloud_storage_account** 클래스 toorepresent 저장소 계정 정보.</span><span class="sxs-lookup"><span data-stu-id="4f79b-133">You can use hello **cloud_storage_account** class toorepresent your storage account information.</span></span> <span data-ttu-id="4f79b-134">tooretrieve 저장소 계정 hello 저장소 연결 문자열 정보, hello 구문 분석 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-134">tooretrieve your storage account information from hello storage connection string, you can use hello parse method.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="4f79b-135">다음으로, 참조 tooa 가져올 **cloud_table_client** 클래스를 엔터티 내에 저장 된 hello 테이블 저장소 서비스 및 테이블에 대 한 개체 참조를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-135">Next, get a reference tooa **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within hello Table storage service.</span></span> <span data-ttu-id="4f79b-136">hello 다음 코드에서는 **cloud_table_client** 위에 검색에서는 hello 저장소 계정 개체를 사용 하 여 개체:</span><span class="sxs-lookup"><span data-stu-id="4f79b-136">hello following code creates a **cloud_table_client** object by using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="4f79b-137">테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="4f79b-137">Create a table</span></span>
<span data-ttu-id="4f79b-138">**cloud_table_client** 개체를 사용하면 테이블 및 엔터티에 대한 참조 개체를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-138">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="4f79b-139">hello 다음 코드에서는 **cloud_table_client** 개체 및 toocreate 새 테이블을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-139">hello following code creates a **cloud_table_client** object and uses it toocreate a new table.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="4f79b-140">엔터티 tooa 테이블 추가</span><span class="sxs-lookup"><span data-stu-id="4f79b-140">Add an entity tooa table</span></span>
<span data-ttu-id="4f79b-141">tooadd은 엔터티 tooa 테이블을 새로 만들 **table_entity** 개체를 너무 전달**table_operation:: insert_entity**합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-141">tooadd an entity tooa table, create a new **table_entity** object and pass it too**table_operation::insert_entity**.</span></span> <span data-ttu-id="4f79b-142">hello 다음 코드 hello 고객의 이름으로 사용 hello 행 키 이름 및 성 hello 파티션 키로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-142">hello following code uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="4f79b-143">함께 엔터티의 파티션과 행 키는 hello 엔터티 hello 테이블에 고유 하 게 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-143">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="4f79b-144">Hello 동일한 파티션 키를 서로 다른 것 보다 더 빠르게 쿼리할 수 있는 엔터티의 파티션 키, 하지만 다양 한 파티션 키를 사용 하 여 병렬 작업 확장성이 높아집니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-144">Entities with hello same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="4f79b-145">자세한 내용은 [Microsoft Azure 저장소 성능 및 확장성 검사 목록](storage-performance-checklist.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f79b-145">For more information, see [Microsoft Azure storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<span data-ttu-id="4f79b-146">hello 다음 코드에서는의 새 인스턴스 **table_entity** 저장 된 일부 고객 데이터 toobe 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-146">hello following code creates a new instance of **table_entity** with some customer data toobe stored.</span></span> <span data-ttu-id="4f79b-147">코드의 다음 호출 hello **table_operation:: insert_entity** toocreate는 **table_operation** tooinsert 엔터티를 테이블에 개체 및 연결 된 새 테이블 엔터티 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-147">hello code next calls **table_operation::insert_entity** toocreate a **table_operation** object tooinsert an entity into a table, and associates hello new table entity with it.</span></span> <span data-ttu-id="4f79b-148">Hello hello에 메서드를 실행할 hello 코드 호출 마지막으로, **cloud_table** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-148">Finally, hello code calls hello execute method on hello **cloud_table** object.</span></span> <span data-ttu-id="4f79b-149">및 새 hello **table_operation** hello "people" 테이블로 요청 toohello 테이블 서비스 tooinsert hello 새 customer 엔터티를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-149">And hello new **table_operation** sends a request toohello Table service tooinsert hello new customer entity into hello "people" table.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="4f79b-150">엔터티 일괄 삽입</span><span class="sxs-lookup"><span data-stu-id="4f79b-150">Insert a batch of entities</span></span>
<span data-ttu-id="4f79b-151">한 번의 쓰기 작업에서 엔터티 toohello 테이블 서비스의 일괄 처리를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-151">You can insert a batch of entities toohello Table service in one write operation.</span></span> <span data-ttu-id="4f79b-152">hello 다음 코드에서는 **table_batch_operation** 개체를 작업 tooit 삽입 3 개를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-152">hello following code creates a **table_batch_operation** object, and then adds three insert operations tooit.</span></span> <span data-ttu-id="4f79b-153">각 삽입 작업은 해당 값을 설정 하는 새 엔터티 개체를 만들어 추가 되 고 hello를 호출한 다음 insert 메서드 hello에 **table_batch_operation** 개체 tooassociate hello 엔터티를 새 작업을 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-153">Each insert operation is added by creating a new entity object, setting its values, and then calling hello insert method on hello **table_batch_operation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="4f79b-154">그런 다음 **cloud_table.execute** tooexecute hello 작업 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-154">Then, **cloud_table.execute** is called tooexecute hello operation.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

<span data-ttu-id="4f79b-155">일괄 처리 작업에 일부의 toonote:</span><span class="sxs-lookup"><span data-stu-id="4f79b-155">Some things toonote on batch operations:</span></span>  

* <span data-ttu-id="4f79b-156">Too100 insert, delete, merge, replace, 조합 단일 일괄 처리에서에서 삽입 또는 병합 및 삽입 또는 바꾸기 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-156">You can perform up too100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="4f79b-157">일괄 처리 작업이 hello hello 일괄 처리에서 유일한 작업 하는 경우 검색 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-157">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>  
* <span data-ttu-id="4f79b-158">단일 일괄 처리 작업의 모든 엔터티가 hello 있어야 합니다. 동일한 파티션 키입니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-158">All entities in a single batch operation must have hello same partition key.</span></span>  
* <span data-ttu-id="4f79b-159">일괄 처리 작업은 제한 된 tooa 4MB 데이터 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-159">A batch operation is limited tooa 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="4f79b-160">파티션의 모든 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="4f79b-160">Retrieve all entities in a partition</span></span>
<span data-ttu-id="4f79b-161">파티션에서 사용 하 여 모든 엔터티에 대 한 테이블 tooquery는 **table_query** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-161">tooquery a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="4f79b-162">hello 다음 코드 예제에서는 지정 엔터티 'Smith'는 hello 파티션 키에 대 한 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-162">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="4f79b-163">이 예제는 hello 쿼리 결과 toohello 콘솔의 각 엔터티에의 hello 필드를 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-163">This example prints hello fields of each entity in hello query results toohello console.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

<span data-ttu-id="4f79b-164">이 예의 쿼리 hello hello 필터 조건과 일치 하는 모든 hello 엔터티를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-164">hello query in this example brings all hello entities that match hello filter criteria.</span></span> <span data-ttu-id="4f79b-165">큰 테이블을 한 toodownload hello 테이블 엔터티를 자주 사용 하는 경우 데이터 Azure 저장소 blob에 대신 저장 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-165">If you have large tables and need toodownload hello table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="4f79b-166">파티션의 엔터티 범위 검색</span><span class="sxs-lookup"><span data-stu-id="4f79b-166">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="4f79b-167">않으려면 tooquery 파티션에서 모든 hello 엔터티, 행 키 필터와 hello 파티션 키 필터를 결합 하 여 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-167">If you don't want tooquery all hello entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="4f79b-168">hello 다음 코드 예제에서는 두 개의 필터 tooget 모든 엔터티 파티션에 'Smith' hello 행 키 (이름)이 이전 hello 알파벳에서 사용 되는 'E'는 문자로 시작 하 고 다음 hello 쿼리 결과 출력 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-168">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter earlier than 'E' in hello alphabet and then prints hello query results.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="4f79b-169">단일 엔터티 검색</span><span class="sxs-lookup"><span data-stu-id="4f79b-169">Retrieve a single entity</span></span>
<span data-ttu-id="4f79b-170">단일, 특정 엔터티 쿼리 tooretrieve를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-170">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="4f79b-171">hello 다음 코드에서는 **table_operation:: retrieve_entity** toospecify hello 고객 ' 홍길동 '.</span><span class="sxs-lookup"><span data-stu-id="4f79b-171">hello following code uses **table_operation::retrieve_entity** toospecify hello customer 'Jeff Smith'.</span></span> <span data-ttu-id="4f79b-172">이 메서드는 컬렉션을이 아닌 하나의 엔터티를 반환 하 고 hello 반환 된 값은 **table_result**합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-172">This method returns just one entity, rather than a collection, and hello returned value is in **table_result**.</span></span> <span data-ttu-id="4f79b-173">쿼리에서 모두 파티션 및 행 키를 지정 하는 hello 가장 빠른 방법은 tooretrieve hello 테이블 서비스에서 단일 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-173">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a><span data-ttu-id="4f79b-174">엔터티 바꾸기</span><span class="sxs-lookup"><span data-stu-id="4f79b-174">Replace an entity</span></span>
<span data-ttu-id="4f79b-175">엔터티에 tooreplace hello 테이블 서비스에서 검색, hello 엔터티 개체를 수정 및 다음 hello 변경 내용을 저장할 toohello 테이블 서비스를 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-175">tooreplace an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="4f79b-176">hello 다음 코드 변경 기존 고객의 전화 번호 및 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-176">hello following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="4f79b-177">**table_operation::insert_entity**를 호출하는 대신, 이 코드에서는 **table_operation::replace_entity**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-177">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="4f79b-178">이렇게 하면 hello 서버 hello 엔터티 hello 작업이 실패 하는 경우, 검색 된 이후 변경 되지 않은 hello 엔터티 toobe hello 서버에서 완전히 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-178">This causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="4f79b-179">이 오류는 tooprevent 검색 hello와 응용 프로그램의 다른 구성 요소 업데이트 간 응용 프로그램에서 변경 내용을 덮어쓰는 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-179">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="4f79b-180">hello 적절 한 처리가 오류는 tooretrieve hello 엔터티 다시를 원하는 대로 변경한 (여전히 유효한 경우) 한 다음 다른를 수행 **table_operation:: replace_entity** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-180">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="4f79b-181">다음 섹션 hello 방법을 살펴보겠습니다 toooverride이이 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-181">hello next section will show you how toooverride this behavior.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="4f79b-182">엔터티 삽입 또는 바꾸기</span><span class="sxs-lookup"><span data-stu-id="4f79b-182">Insert-or-replace an entity</span></span>
<span data-ttu-id="4f79b-183">**table_operation:: replace_entity** hello 엔터티 hello 서버에서 검색 된 이후 변경 된 경우 작업이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-183">**table_operation::replace_entity** operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="4f79b-184">에 대 한 순서에서 첫 번째 hello 서버에서 hello 엔터티를 검색 해야 또한 **table_operation:: replace_entity** toobe 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-184">Furthermore, you must retrieve hello entity from hello server first in order for **table_operation::replace_entity** toobe successful.</span></span> <span data-ttu-id="4f79b-185">그러나 경우에 따라 모르는 hello 엔터티 hello 서버에 있고 hello 현재 값에 저장 된 관련 되지 않은 경우-업데이트 내용을 모두 덮어쓰도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-185">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="4f79b-186">tooaccomplish이를 사용 하 여 한 **table_operation:: insert_or_replace_entity** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-186">tooaccomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="4f79b-187">이 작업이 존재 하지 않으면 하거나 hello 마지막 업데이트가 수행 된 경우에 관계 없이 수행 하면 대체 하는 경우 hello 엔터티를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-187">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span> <span data-ttu-id="4f79b-188">다음 코드 예제는 hello, 홍길동에 대 한 hello customer 엔터티를 아직 검색, 하지만 한 다음 다시 toohello 서버를 통해 저장 **table_operation:: insert_or_replace_entity**합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-188">In hello following code example, hello customer entity for Jeff Smith is still retrieved, but it is then saved back toohello server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="4f79b-189">Toohello 엔터티 간의 hello 검색 및 업데이트 작업의 모든 업데이트를 덮어쓰게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-189">Any updates made toohello entity between hello retrieval and update operation will be overwritten.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="4f79b-190">엔터티 속성 하위 집합 쿼리</span><span class="sxs-lookup"><span data-stu-id="4f79b-190">Query a subset of entity properties</span></span>
<span data-ttu-id="4f79b-191">쿼리 tooa 테이블 엔터티의 몇 개의 속성을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-191">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="4f79b-192">hello 쿼리에서 hello 코드 다음에 사용 하 여 hello **table_query:: set_select_columns** 메서드 tooreturn hello 전자 메일 주소만 hello 테이블에 있는 엔터티.</span><span class="sxs-lookup"><span data-stu-id="4f79b-192">hello query in hello following code uses hello **table_query::set_select_columns** method tooreturn only hello email addresses of entities in hello table.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> <span data-ttu-id="4f79b-193">모든 속성을 검색하는 것보다 엔터티의 몇 가지 속성을 쿼리하는 것이 더 효율적인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-193">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="4f79b-194">엔터티 삭제</span><span class="sxs-lookup"><span data-stu-id="4f79b-194">Delete an entity</span></span>
<span data-ttu-id="4f79b-195">엔터티를 검색한 다음 쉽게 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-195">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="4f79b-196">Hello 엔터티 검색 되 면 호출 **table_operation:: delete_entity** hello 엔터티 toodelete 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-196">Once hello entity is retrieved, call **table_operation::delete_entity** with hello entity toodelete.</span></span> <span data-ttu-id="4f79b-197">그런 다음 hello 호출 **cloud_table.execute** 메서드.</span><span class="sxs-lookup"><span data-stu-id="4f79b-197">Then call hello **cloud_table.execute** method.</span></span> <span data-ttu-id="4f79b-198">hello 다음 코드를 검색 하 고 파티션 키 "Smith"와 "Jeff"의 행 키가 있는 엔터티를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-198">hello following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a><span data-ttu-id="4f79b-199">테이블 삭제</span><span class="sxs-lookup"><span data-stu-id="4f79b-199">Delete a table</span></span>
<span data-ttu-id="4f79b-200">마지막으로, 다음 코드 예제는 hello 저장소 계정에서 테이블을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-200">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="4f79b-201">삭제 된 테이블을 사용할 수 없는 toobe hello 삭제 시간 기간에 대 한 다시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-201">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a><span data-ttu-id="4f79b-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f79b-202">Next steps</span></span>
<span data-ttu-id="4f79b-203">테이블 저장소의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn Azure 저장소에 대 한 자세한 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-203">Now that you've learned hello basics of table storage, follow these links toolearn more about Azure Storage:</span></span>  

* <span data-ttu-id="4f79b-204">[Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork 시각적으로 Windows, macOS 등 및 Linux에서 Azure 저장소 데이터로 사용 하면 Microsoft에서 가능한 독립 실행형 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="4f79b-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="4f79b-205">어떻게 toouse c + +에서 Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="4f79b-205">How toouse Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="4f79b-206">어떻게 toouse c + +에서 큐 저장소</span><span class="sxs-lookup"><span data-stu-id="4f79b-206">How toouse Queue storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="4f79b-207">C++에서 Azure 저장소 리소스 나열</span><span class="sxs-lookup"><span data-stu-id="4f79b-207">List Azure Storage resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="4f79b-208">C++용 Storage Client Library 참조(영문)</span><span class="sxs-lookup"><span data-stu-id="4f79b-208">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="4f79b-209">Azure 저장소 설명서</span><span class="sxs-lookup"><span data-stu-id="4f79b-209">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
