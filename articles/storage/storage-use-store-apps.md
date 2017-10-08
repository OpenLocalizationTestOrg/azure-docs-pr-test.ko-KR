---
title: "Windows 스토어 앱에서 Azure 저장소 aaaUse | Microsoft Docs"
description: "Windows 저장 하는 toocreate 방법에 대해 알아봅니다 Azure Blob, 큐, 테이블 또는 파일 저장소를 사용 하는 응용 프로그램입니다."
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
ms.openlocfilehash: ac21b0695c0d77c1d81c1b921718fb929945d45e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a><span data-ttu-id="0a955-103">어떻게 Windows 스토어 앱에서 Azure 저장소 toouse</span><span class="sxs-lookup"><span data-stu-id="0a955-103">How toouse Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="0a955-104">개요</span><span class="sxs-lookup"><span data-stu-id="0a955-104">Overview</span></span>
<span data-ttu-id="0a955-105">이 가이드에서 Azure 저장소를 활용 하는 Windows 스토어 앱 개발 tooget 시작 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-105">This guide shows how tooget started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="0a955-106">필요한 도구 다운로드</span><span class="sxs-lookup"><span data-stu-id="0a955-106">Download required tools</span></span>
* <span data-ttu-id="0a955-107">[Visual Studio](https://www.visualstudio.com/downloads/) 쉽게 toobuild를 사용 하면 디버그, 지역화, 패키지 및 Windows 스토어 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy toobuild, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="0a955-108">Visual Studio 2012 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="0a955-109">hello [Azure 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage) Azure 저장소를 사용 하기 위한 Windows 런타임 클래스 라이브러리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-109">hello [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="0a955-110">[WCF 데이터 서비스 도구 Windows 스토어 앱 용](http://www.microsoft.com/download/details.aspx?id=30714) Visual Studio에서 Windows 스토어 앱에 대 한 클라이언트 쪽 OData 지 원하는 hello 서비스 참조 추가 경험을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends hello Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="0a955-111">앱 개발</span><span class="sxs-lookup"><span data-stu-id="0a955-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="0a955-112">준비</span><span class="sxs-lookup"><span data-stu-id="0a955-112">Getting ready</span></span>
<span data-ttu-id="0a955-113">Visual Studio 2012 이상에서 새 Windows 스토어 앱 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![store-apps-storage-vs-project][store-apps-storage-vs-project]

<span data-ttu-id="0a955-115">다음으로, 마우스 오른쪽 단추로 클릭 하 여 참조 toohello Azure 저장소 클라이언트 라이브러리를 추가 **참조**, **참조 추가**, 다음 toohello Windows Runtime 용 저장소 클라이언트 라이브러리를 검색 하 고 있는 다운로드:</span><span class="sxs-lookup"><span data-stu-id="0a955-115">Next, add a reference toohello Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing toohello Storage Client Library for Windows Runtime that you downloaded:</span></span>

![store-apps-storage-choose-library][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a><span data-ttu-id="0a955-117">Hello Blob로 hello 라이브러리 및 큐 서비스를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0a955-117">Using hello library with hello Blob and Queue services</span></span>
<span data-ttu-id="0a955-118">이 응용 프로그램 준비 toocall hello Azure Blob 및 큐 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-118">At this point, your app is ready toocall hello Azure Blob and Queue services.</span></span> <span data-ttu-id="0a955-119">Hello 다음 추가 **를 사용 하 여** 문의 하 여 Azure 저장소 형식을 직접 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-119">Add hello following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="0a955-120">다음으로 단추 tooyour 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-120">Next, add a button tooyour page.</span></span> <span data-ttu-id="0a955-121">다음 코드 tooits hello 추가 **클릭** 이벤트 hello를 사용 하 여 이벤트 처리기 메서드를 수정 하 고 [async 키워드](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="0a955-121">Add hello following code tooits **Click** event and modify your event handler method by using hello [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="0a955-122">이 코드에서는 두 개의 문자열 변수인 *accountName* 및 *accountKey*가 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="0a955-123">저장소 계정 및 hello 계정 키의 해당 계정에 연관 된 hello 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-123">They represent hello name of your storage account and hello account key that is associated with that account.</span></span>

<span data-ttu-id="0a955-124">빌드하고 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-124">Build and run hello application.</span></span> <span data-ttu-id="0a955-125">Hello 단추를 클릭 하는 컨테이너 이름을 지정 여부를 확인 *container1* 계정에 있으며 다음 없으면 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-125">Clicking hello button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-hello-library-with-hello-table-service"></a><span data-ttu-id="0a955-126">Hello 라이브러리를 사용 하 여 테이블 서비스 hello로</span><span class="sxs-lookup"><span data-stu-id="0a955-126">Using hello library with hello Table service</span></span>
<span data-ttu-id="0a955-127">Windows 스토어 응용 프로그램 라이브러리 hello에 대 한 WCF Data Services에 hello Azure 테이블 서비스와 함께 사용 되는 toocommunicate 않은 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-127">Types that are used toocommunicate with hello Azure Table service depend on WCF Data Services for hello Windows Store app library.</span></span> <span data-ttu-id="0a955-128">다음으로, 참조 toohello WCF 라이브러리를 사용 하 여 hello 패키지 관리자 콘솔이 필요한 추가:</span><span class="sxs-lookup"><span data-stu-id="0a955-128">Next, add a reference toohello required WCF libraries by using hello Package Manager Console:</span></span>

![store-apps-storage-package-manager][store-apps-storage-package-manager]

<span data-ttu-id="0a955-130">사용 하 여 hello 다음 명령은 toopoint 컴퓨터의 패키지 관리자 toohello 위치:</span><span class="sxs-lookup"><span data-stu-id="0a955-130">Use hello following command toopoint Package Manager toohello location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="0a955-131">이 명령은 모든 필요한 참조 tooyour 프로젝트를 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-131">This command will automatically add all required references tooyour project.</span></span> <span data-ttu-id="0a955-132">Toouse 하지 않을 경우 패키지 관리자 콘솔 hello, 로컬 컴퓨터 toohello 패키지 소스 목록에 hello WCF Data Services NuGet 폴더에 추가 하 고 다음에 설명 된 대로 hello UI 통해 hello 참조를 추가할 수 [관리 NuGet 패키지를 사용 하 여 hello 대화](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog)합니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-132">If you do not want toouse hello Package Manager Console, you can add hello WCF Data Services NuGet folder on your local machine toohello list of package sources and then add hello reference through hello UI, as described in [Managing NuGet Packages Using hello Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="0a955-133">Hello WCF Data Services NuGet 패키지를 참조 하는 경우 프로그램 단추에 hello 코드 변경 **클릭** 이벤트:</span><span class="sxs-lookup"><span data-stu-id="0a955-133">When you have referenced hello WCF Data Services NuGet package, change hello code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="0a955-134">이 코드는 *table1* 이라는 테이블이 계정이 있는지 확인하고 없으면 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="0a955-135">또한 동일한 패키지를 다운로드 하는 hello에서 사용 하지 않는 참조 tooMicrosoft.WindowsAzure.Storage.Table.dll을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-135">You can also add a reference tooMicrosoft.WindowsAzure.Storage.Table.dll, which is available in hello same package that you downloaded.</span></span> <span data-ttu-id="0a955-136">이 라이브러리에는 리플렉션 기반 직렬화 및 일반 쿼리와 같은 추가 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="0a955-137">이 라이브러리는 JavaScript를 지원하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0a955-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
