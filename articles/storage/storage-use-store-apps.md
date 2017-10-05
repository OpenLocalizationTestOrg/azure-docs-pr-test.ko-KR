---
title: "Windows 스토어 앱에서 Azure Storage 사용 | Microsoft Docs"
description: "Azure Blob, 큐, 테이블 또는 파일 저장소를 사용하는 Windows 스토어 앱을 만드는 방법을 알아봅니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 63c4b29d-b2f2-4d7c-b164-a0d38f4d14f6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 43d38584270fbbbe6fa4e4ff8cef72ca44e14acc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-storage-in-windows-store-apps"></a><span data-ttu-id="c0afa-103">Windows 스토어 앱에서 Azure 저장소를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="c0afa-103">How to use Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="c0afa-104">개요</span><span class="sxs-lookup"><span data-stu-id="c0afa-104">Overview</span></span>
<span data-ttu-id="c0afa-105">이 가이드에서는 Azure 저장소를 사용하는 Windows 스토어 앱 개발을 시작하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-105">This guide shows how to get started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="c0afa-106">필요한 도구 다운로드</span><span class="sxs-lookup"><span data-stu-id="c0afa-106">Download required tools</span></span>
* <span data-ttu-id="c0afa-107">[Visual Studio](https://www.visualstudio.com/downloads/)는 Windows 스토어 앱을 쉽게 빌드, 디버그, 지역화, 패키징 및 배포할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy to build, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="c0afa-108">Visual Studio 2012 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="c0afa-109">[Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage) 는 Azure 저장소 작업을 위한 Windows 런타임 클래스 라이브러리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-109">The [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="c0afa-110">[Windows 스토어 앱을 위한 WCF 데이터 서비스 도구](http://www.microsoft.com/download/details.aspx?id=30714) 는 Visual Studio에서 Windows 스토어 앱 용 클라이언트쪽 OData 지원으로 서비스 참조 추가 환경을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends the Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="c0afa-111">앱 개발</span><span class="sxs-lookup"><span data-stu-id="c0afa-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="c0afa-112">준비</span><span class="sxs-lookup"><span data-stu-id="c0afa-112">Getting ready</span></span>
<span data-ttu-id="c0afa-113">Visual Studio 2012 이상에서 새 Windows 스토어 앱 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![store-apps-storage-vs-project][store-apps-storage-vs-project]

<span data-ttu-id="c0afa-115">다음으로 **참조**를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 클릭한 다음 다운로드한 Windows 런타임의 저장소 클라이언트 라이브러리로 이동하여 Azure Storage 클라이언트 라이브러리에 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-115">Next, add a reference to the Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing to the Storage Client Library for Windows Runtime that you downloaded:</span></span>

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-the-library-with-the-blob-and-queue-services"></a><span data-ttu-id="c0afa-117">Blob 및 큐 서비스로 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="c0afa-117">Using the library with the Blob and Queue services</span></span>
<span data-ttu-id="c0afa-118">이제 앱에서 Azure Blob 및 큐 서비스를 호출할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-118">At this point, your app is ready to call the Azure Blob and Queue services.</span></span> <span data-ttu-id="c0afa-119">Azure 저장소 형식을 직접 참조할 수 있도록 다음 **using** 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-119">Add the following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="c0afa-120">그런 다음, 페이지에 단추를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-120">Next, add a button to your page.</span></span> <span data-ttu-id="c0afa-121">다음 코드를 단추의 **Click** 이벤트에 추가하고 [async 키워드](http://msdn.microsoft.com/library/vstudio/hh156513.aspx)를 사용하여 이벤트 처리기 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-121">Add the following code to its **Click** event and modify your event handler method by using the [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="c0afa-122">이 코드에서는 두 개의 문자열 변수인 *accountName* 및 *accountKey*가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="c0afa-123">저장소 계정의 이름 및 해당 계정과 연결된 계정 키를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-123">They represent the name of your storage account and the account key that is associated with that account.</span></span>

<span data-ttu-id="c0afa-124">응용 프로그램을 빌드 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-124">Build and run the application.</span></span> <span data-ttu-id="c0afa-125">단추를 클릭하면 *container1* 이라는 컨테이너가 계정에 있는지 확인하고 없으면 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-125">Clicking the button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-the-library-with-the-table-service"></a><span data-ttu-id="c0afa-126">테이블 서비스로 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="c0afa-126">Using the library with the Table service</span></span>
<span data-ttu-id="c0afa-127">Azure 테이블 서비스와 통신하는 데 사용되는 형식은 Windows 스토어 앱 라이브러리용 WCF 데이터 서비스에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-127">Types that are used to communicate with the Azure Table service depend on WCF Data Services for the Windows Store app library.</span></span> <span data-ttu-id="c0afa-128">다음으로 패키지 관리자 콘솔을 사용하여 필요한 WCF 라이브러리에 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-128">Next, add a reference to the required WCF libraries by using the Package Manager Console:</span></span>

![store-apps-storage-package-manager][store-apps-storage-package-manager]

<span data-ttu-id="c0afa-130">다음 명령을 사용하여 패키지 관리자가 컴퓨터의 위치를 가리키도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-130">Use the following command to point Package Manager to the location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="c0afa-131">이 명령은 필요한 모든 참조를 프로젝트에 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-131">This command will automatically add all required references to your project.</span></span> <span data-ttu-id="c0afa-132">패키지 관리자 콘솔을 사용하지 않으려는 경우 로컬 컴퓨터의 WCF 데이터 서비스 NuGet 폴더를 패키지 원본 목록에 추가한 다음 [대화 상자를 사용하여 NuGet 패키지 관리](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog)(영문)에 설명된 대로 UI를 통해 참조를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-132">If you do not want to use the Package Manager Console, you can add the WCF Data Services NuGet folder on your local machine to the list of package sources and then add the reference through the UI, as described in [Managing NuGet Packages Using the Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="c0afa-133">WCF 데이터 서비스 NuGet 패키지를 참조한 경우 단추의 **Click** 이벤트에서 코드를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-133">When you have referenced the WCF Data Services NuGet package, change the code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="c0afa-134">이 코드는 *table1* 이라는 테이블이 계정이 있는지 확인하고 없으면 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="c0afa-135">다운로드한 동일한 패키지에 있는 Microsoft.WindowsAzure.Storage.Table.dll에 참조를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-135">You can also add a reference to Microsoft.WindowsAzure.Storage.Table.dll, which is available in the same package that you downloaded.</span></span> <span data-ttu-id="c0afa-136">이 라이브러리에는 리플렉션 기반 직렬화 및 일반 쿼리와 같은 추가 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="c0afa-137">이 라이브러리는 JavaScript를 지원하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c0afa-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
