---
title: "App Service Mobile Apps로 관리되는 클라이언트 라이브러리 작업(Windows) | Microsoft Docs"
description: "Windows 및 Xamarin 앱에서 Azure 앱 서비스 모바일 앱용 .NET 클라이언트를 사용하는 방법에 대해 알아봅니다."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0280785c-e027-4e0d-aaf2-6f155e5a6197
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 01/04/2017
ms.author: glenga
ms.openlocfilehash: 5f4cc3e97ba7adde2aaac471951a3130d79910f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="a62e1-103">Azure 모바일 앱에 관리되는 클라이언트를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="a62e1-103">How to use the managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="a62e1-104">개요</span><span class="sxs-lookup"><span data-stu-id="a62e1-104">Overview</span></span>
<span data-ttu-id="a62e1-105">이 가이드에서는 Windows 및 Xamarin 앱용 Azure 앱 서비스 모바일 앱에 관리되는 클라이언트 라이브러리를 사용하는 일반적인 시나리오를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-105">This guide shows you how to perform common scenarios using the managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="a62e1-106">Mobile Apps를 처음 접하는 경우 먼저 [Azure Mobile Apps 빠른 시작][1] 자습서를 완료하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-106">If you are new to Mobile Apps, you should consider first completing the [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="a62e1-107">이 가이드에서는 클라이언트 쪽 관리되는 SDK에 초점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-107">In this guide, we focus on the client-side managed SDK.</span></span> <span data-ttu-id="a62e1-108">모바일 앱에 대한 서버 쪽 SDK에 대해 자세히 알아보려면 [.NET 서버 SDK][2] 또는 [Node.js 서버 SDK][3]에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a62e1-108">To learn more about the server-side SDKs for Mobile Apps, see the documentation for the [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="a62e1-109">참조 설명서</span><span class="sxs-lookup"><span data-stu-id="a62e1-109">Reference documentation</span></span>
<span data-ttu-id="a62e1-110">클라이언트 SDK에 대한 참조 설명서는 [Azure Mobile Apps .NET 클라이언트 참조][4]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-110">The reference documentation for the client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="a62e1-111">[Azure 샘플 GitHub 리포지토리][5]에서 몇 가지 클라이언트 샘플을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-111">You can also find several client samples in the [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="a62e1-112">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="a62e1-112">Supported Platforms</span></span>
<span data-ttu-id="a62e1-113">.NET 플랫폼은 다음과 같은 플랫폼을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-113">The .NET Platform supports the following platforms:</span></span>

* <span data-ttu-id="a62e1-114">API 19-24(Nougat를 통한 KitKat)용 Xamarin Android 릴리스</span><span class="sxs-lookup"><span data-stu-id="a62e1-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="a62e1-115">iOS 버전 8.0 이상을 위한 Xamarin iOS 릴리스</span><span class="sxs-lookup"><span data-stu-id="a62e1-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="a62e1-116">범용 Windows 플랫폼</span><span class="sxs-lookup"><span data-stu-id="a62e1-116">Universal Windows Platform</span></span>
* <span data-ttu-id="a62e1-117">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="a62e1-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="a62e1-118">Silverlight 응용 프로그램을 제외한 Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="a62e1-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="a62e1-119">"서버-흐름" 인증은 표시된 UI에 웹 보기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-119">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="a62e1-120">장치가 웹 보기 UI를 표시할 수 없는 경우 다른 인증 방법이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-120">If the device is not able to present a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="a62e1-121">따라서 이 SDK는 Watch 유형 또는 그와 비슷하게 제한된 장치에는 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="a62e1-122"><a name="setup"></a>설정 및 필수 조건</span><span class="sxs-lookup"><span data-stu-id="a62e1-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="a62e1-123">하나 이상의 테이블에 포함된 모바일 앱 백 엔드 프로젝트를 이미 만들고 게시했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="a62e1-124">이 토픽에 사용되는 코드에서, 테이블은 이름이 `TodoItem`(이)고 `Id`, `Text` 및 `Complete` 열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-124">In the code used in this topic, the table is named `TodoItem` and it has the following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="a62e1-125">이 테이블은 [Azure Mobile Apps 빠른 시작 자습서][1]를 완료할 때 만들었던 것과 동일한 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-125">This table is the same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="a62e1-126">C#에서 해당하는 형식화된 클라이언트 쪽 형식은 다음 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-126">The corresponding typed client-side type in C# is the following class:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }
}
```

<span data-ttu-id="a62e1-127">[JsonPropertyAttribute][6]는 클라이언트 필드와 테이블 필드 간의 *PropertyName* 매핑을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-127">The [JsonPropertyAttribute][6] is used to define the *PropertyName* mapping between the client field and the table field.</span></span>

<span data-ttu-id="a62e1-128">Mobile Apps 백 엔드에서 테이블을 만드는 방법을 알아보려면 [.NET 서버 SDK 토픽][7] 또는 [Node.js 서버 SDK 토픽][8]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a62e1-128">To learn how to create tables in your Mobile Apps backend, see the [.NET Server SDK topic][7] or the [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="a62e1-129">빠른 시작을 사용하여 Azure Portal에서 Mobile App 백 엔드를 만든 경우 **Azure Portal** 에서 [Azure Portal]설정을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-129">If you created your Mobile App backend in the Azure portal using the QuickStart, you can also use the **Easy tables** setting in the [Azure portal].</span></span>

### <a name="how-to-install-the-managed-client-sdk-package"></a><span data-ttu-id="a62e1-130">방법: 관리되는 클라이언트 SDK 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="a62e1-130">How to: Install the managed client SDK package</span></span>
<span data-ttu-id="a62e1-131">다음 메서드 중 하나를 사용하여 [NuGet][9]에서 Mobile Apps용 관리되는 클라이언트 SDK 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-131">Use one of the following methods to install the managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="a62e1-132">**Visual Studio**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 클릭한 다음, `Microsoft.Azure.Mobile.Client` 패키지를 검색하고 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="a62e1-133">**Xamarin Studio**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **NuGet 패키지 추가**를 클릭한 다음, `Microsoft.Azure.Mobile.Client ` 패키지를 검색하고 **패키지 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="a62e1-134">기본 활동 파일에 다음 **using** 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-134">In your main activity file, remember to add the following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="a62e1-135"><a name="symbolsource"></a>방법: Visual Studio에서 디버그 작업</span><span class="sxs-lookup"><span data-stu-id="a62e1-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="a62e1-136">Microsoft.Azure.Mobile 네임스페이스의 기호는 [SymbolSource][10]에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-136">The symbols for the Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="a62e1-137">SymbolSource를 Visual Studio와 통합하려면 [SymbolSource 지침][11]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a62e1-137">Refer to the [SymbolSource instructions][11] to integrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="a62e1-138"><a name="create-client"></a>Mobile Apps 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="a62e1-138"><a name="create-client"></a>Create the Mobile Apps client</span></span>
<span data-ttu-id="a62e1-139">다음 코드는 모바일 앱 백 엔드에 액세스하는 데 사용되는 [MobileServiceClient][12] 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-139">The following code creates the [MobileServiceClient][12] object that is used to access your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="a62e1-140">위의 코드에서 `MOBILE_APP_URL` 을 모바일 앱 백 엔드의 URL로 대체하며 이는 [Azure Portal]의 모바일 앱 백 엔드에 대한 블레이드에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-140">In the preceding code, replace `MOBILE_APP_URL` with the URL of the Mobile App backend, which is found in the blade for your Mobile App backend in the [Azure portal].</span></span> <span data-ttu-id="a62e1-141">MobileServiceClient 개체는 단일 항목이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-141">The MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="a62e1-142">테이블 작업</span><span class="sxs-lookup"><span data-stu-id="a62e1-142">Work with Tables</span></span>
<span data-ttu-id="a62e1-143">다음 섹션에는 레코드를 검색하고 테이블 내에서 데이터를 수정하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-143">The following section details how to search and retrieve records and modify the data within the table.</span></span>  <span data-ttu-id="a62e1-144">다음 토픽을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-144">The following topics are covered:</span></span>

* [<span data-ttu-id="a62e1-145">테이블 참조 만들기</span><span class="sxs-lookup"><span data-stu-id="a62e1-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="a62e1-146">쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="a62e1-146">Query data</span></span>](#querying)
* [<span data-ttu-id="a62e1-147">반환된 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="a62e1-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="a62e1-148">반환된 데이터 정렬</span><span class="sxs-lookup"><span data-stu-id="a62e1-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="a62e1-149">페이지에서 데이터 반환</span><span class="sxs-lookup"><span data-stu-id="a62e1-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="a62e1-150">특정 열 선택</span><span class="sxs-lookup"><span data-stu-id="a62e1-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="a62e1-151">ID로 레코드 조회</span><span class="sxs-lookup"><span data-stu-id="a62e1-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="a62e1-152">형식화되지 않은 쿼리 처리</span><span class="sxs-lookup"><span data-stu-id="a62e1-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="a62e1-153">데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="a62e1-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="a62e1-154">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="a62e1-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="a62e1-155">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="a62e1-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="a62e1-156">충돌 해결 및 낙관적 동시성</span><span class="sxs-lookup"><span data-stu-id="a62e1-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="a62e1-157">Windows 사용자 인터페이스에 바인딩</span><span class="sxs-lookup"><span data-stu-id="a62e1-157">Binding to a Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="a62e1-158">페이지 크기 변경</span><span class="sxs-lookup"><span data-stu-id="a62e1-158">Changing the Page Size</span></span>](#pagesize)

### <span data-ttu-id="a62e1-159"><a name="instantiating"></a>방법: 테이블 참조 만들기</span><span class="sxs-lookup"><span data-stu-id="a62e1-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="a62e1-160">백 엔드 테이블의 데이터에 액세스하거나 데이터를 수정하는 모든 코드는 `MobileServiceTable` 개체의 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-160">All the code that accesses or modifies data in a backend table calls functions on the `MobileServiceTable` object.</span></span> <span data-ttu-id="a62e1-161">다음과 같이 [GetTable] 메서드를 호출하여 테이블에 대한 참조를 구합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-161">Obtain a reference to the table by calling the [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="a62e1-162">반환된 개체는 형식화된 직렬화 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-162">The returned object uses the typed serialization model.</span></span> <span data-ttu-id="a62e1-163">형식화되지 않은 직렬화 모델도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="a62e1-164">다음 예제는 [형식화되지 않은 테이블에 참조를 만듭니다.]</span><span class="sxs-lookup"><span data-stu-id="a62e1-164">The following example [creates a reference to an untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="a62e1-165">형식화되지 않은 쿼리에서 기본 OData 쿼리 문자열을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-165">In untyped queries, you must specify the underlying OData query string.</span></span>

### <span data-ttu-id="a62e1-166"><a name="querying"></a>방법: 모바일 앱에서 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="a62e1-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="a62e1-167">이 섹션에서는 다음 기능을 비롯하여 모바일 앱 백 엔드에 대한 쿼리를 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-167">This section describes how to issue queries to the Mobile App backend, which includes the following functionality:</span></span>

* [<span data-ttu-id="a62e1-168">반환된 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="a62e1-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="a62e1-169">반환된 데이터 정렬</span><span class="sxs-lookup"><span data-stu-id="a62e1-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="a62e1-170">페이지에서 데이터 반환</span><span class="sxs-lookup"><span data-stu-id="a62e1-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="a62e1-171">특정 열 선택</span><span class="sxs-lookup"><span data-stu-id="a62e1-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="a62e1-172">ID를 기준으로 데이터 조회</span><span class="sxs-lookup"><span data-stu-id="a62e1-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="a62e1-173">모든 행이 반환되는 것을 방지하기 위해 서버 기반 페이지 크기가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-173">A server-driven page size is enforced to prevent all rows from being returned.</span></span>  <span data-ttu-id="a62e1-174">페이징은 대규모 데이터 집합에 대한 기본 요청이 서비스에 부정적인 영향을 미치지 않게 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-174">Paging keeps default requests for large data sets from negatively impacting the service.</span></span>  <span data-ttu-id="a62e1-175">50개가 넘는 행을 반환하려면 [페이지에서 데이터 반환](#paging)에서 설명하는 대로 `Skip` 및 `Take` 메서드를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="a62e1-175">To return more than 50 rows, use the `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="a62e1-176"><a name="filtering"></a>방법: 반환된 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="a62e1-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="a62e1-177">다음 코드는 쿼리에 `Where` 절을 포함하여 데이터를 필터링하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-177">The following code illustrates how to filter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="a62e1-178">이 코드에서는 `todoTable`에서 해당 `Complete` 속성이 `false`인 모든 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-178">It returns all items from `todoTable` whose `Complete` property is equal to `false`.</span></span> <span data-ttu-id="a62e1-179">[Where] 함수는 테이블에 대한 쿼리에 행 필터링 조건자를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-179">The [Where] function applies a row filtering predicate to the query against the table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="a62e1-180">브라우저 개발자 도구 또는 [Fiddler]와 같은 메시지 검사 소프트웨어를 사용하여 백 엔드에 전송된 요청의 URI를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-180">You can view the URI of the request sent to the backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="a62e1-181">이 요청 URI에서 알 수 있듯이 쿼리 문자열이 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-181">If you look at the request URI, notice that the query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="a62e1-182">이 OData 요청은 서버 SDK에 의해 SQL 쿼리로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-182">This OData request is translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="a62e1-183">`Where` 메서드에 전달되는 함수는 조건을 임의의 수만큼 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-183">The function that is passed to the `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="a62e1-184">이 예는 서버 SDK에 의해 SQL 쿼리로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-184">This example would be translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="a62e1-185">이 쿼리는 여러 절로 분할될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="a62e1-186">두 메서드는 동등하며 서로 교환해서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-186">The two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="a62e1-187">여러 조건자를 하나의 쿼리&mdash;에서 연결하는 첫 번째 옵션&mdash;이 더 간편하며 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-187">The former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="a62e1-188">`Where` 절은 OData 하위 집합으로 변환되는 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-188">The `Where` clause supports operations that be translated into the OData subset.</span></span> <span data-ttu-id="a62e1-189">작업에는 다음 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-189">Operations include:</span></span>

* <span data-ttu-id="a62e1-190">관계형 연산자(==, !=, <, <=, >, >=),</span><span class="sxs-lookup"><span data-stu-id="a62e1-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="a62e1-191">산술 연산자(+, -, /, *, %),</span><span class="sxs-lookup"><span data-stu-id="a62e1-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="a62e1-192">숫자 정밀도(Math.Floor, Math.Ceiling),</span><span class="sxs-lookup"><span data-stu-id="a62e1-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="a62e1-193">문자열 함수(Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span><span class="sxs-lookup"><span data-stu-id="a62e1-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="a62e1-194">날짜 속성(연도, 월, 일, 시, 분, 초),</span><span class="sxs-lookup"><span data-stu-id="a62e1-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="a62e1-195">개체의 액세스 속성,</span><span class="sxs-lookup"><span data-stu-id="a62e1-195">Access properties of an object, and</span></span>
* <span data-ttu-id="a62e1-196">이러한 연산자를 결합하는 식.</span><span class="sxs-lookup"><span data-stu-id="a62e1-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="a62e1-197">서버 SDK가 지원하는 것을 고려할 때 [OData v3 설명서]를 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-197">When considering what the Server SDK supports, you can consider the [OData v3 Documentation].</span></span>

### <span data-ttu-id="a62e1-198"><a name="sorting"></a>방법: 반환된 데이터 정렬</span><span class="sxs-lookup"><span data-stu-id="a62e1-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="a62e1-199">다음 코드는 쿼리에 [OrderBy] 또는 [OrderByDescending] 함수를 포함하여 데이터를 정렬하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-199">The following code illustrates how to sort data by including an [OrderBy] or [OrderByDescending] function in the query.</span></span> <span data-ttu-id="a62e1-200">`todoTable`의 항목을 `Text` 필드를 기준으로 오름차순 정렬한 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-200">It returns items from `todoTable` sorted ascending by the `Text` field.</span></span>

```
// Sort items in ascending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderBy(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();

// Sort items in descending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderByDescending(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();
```

### <span data-ttu-id="a62e1-201"><a name="paging"></a>방법: 페이지에서 데이터 반환</span><span class="sxs-lookup"><span data-stu-id="a62e1-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="a62e1-202">기본적으로 백 엔드는 첫 50개 행만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-202">By default, the backend returns only the first 50 rows.</span></span> <span data-ttu-id="a62e1-203">[Take] 메서드를 호출하여 반환 행 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-203">You can increase the number of returned rows by calling the [Take] method.</span></span> <span data-ttu-id="a62e1-204">`Take` 을(를) [Skip] 메서드와 함께 사용하면 쿼리에서 반환되는 전체 데이터 집합의 특정 "페이지"가 요청됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-204">Use `Take` along with the [Skip] method to request a specific "page" of the total dataset returned by the query.</span></span> <span data-ttu-id="a62e1-205">다음 쿼리를 실행하면 테이블에서 맨 위에 있는 세 개의 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-205">The following query, when executed, returns the top three items in the table.</span></span>

```
// Define a filtered query that returns the top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="a62e1-206">수정된 다음 쿼리는 처음 세 개 결과를 건너뛰고 그 다음 세 개 결과를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-206">The following revised query skips the first three results and returns the next three results.</span></span> <span data-ttu-id="a62e1-207">이 쿼리는 두 번째 데이터 "페이지"를 생성하며, 페이지 크기는 세 개 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-207">This query produces the second "page" of data, where the page size is three items.</span></span>

```
// Define a filtered query that skips the top 3 items and returns the next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="a62e1-208">[IncludeTotalCount] 메서드는 지정된 페이징/제한 절을 무시하고, 반환되었어야 할 *모든* 레코드의 총 개수를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-208">The [IncludeTotalCount] method requests the total count for *all* the records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="a62e1-209">실제 앱에서는 Pager 컨트롤이나 그와 비슷한 UI에서 이전 예제와 비슷한 쿼리를 사용하여 페이지를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-209">In a real world app, you can use queries similar to the preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="a62e1-210">모바일 앱 백 엔드에서 50행 제한을 재정의하려면 [EnableQueryAttribute] 를 공용 GET 메서드에도 적용하고 페이징 동작을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-210">To override the 50-row limit in a Mobile App backend, you must also apply the [EnableQueryAttribute] to the public GET method and specify the paging behavior.</span></span> <span data-ttu-id="a62e1-211">메서드에 적용할 때 다음은 최대 반환 행을 1000으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-211">When applied to the method, the following sets the maximum returned rows to 1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="a62e1-212"><a name="selecting"></a>방법: 특정 열 선택</span><span class="sxs-lookup"><span data-stu-id="a62e1-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="a62e1-213">쿼리에 [Select] 절을 추가하면 결과에 포함할 속성 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-213">You can specify which set of properties to include in the results by adding a [Select] clause to your query.</span></span> <span data-ttu-id="a62e1-214">예를 들어 다음 코드는 하나의 필드만 선택하는 방법 및 여러 필드를 선택하고 형식을 지정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-214">For example, the following code shows how to select just one field and also how to select and format multiple fields:</span></span>

```
// Select one field -- just the Text
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => todoItem.Text);
List<string> items = await query.ToListAsync();

// Select multiple fields -- both Complete and Text info
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => string.Format("{0} -- {1}",
                    todoItem.Text.PadRight(30), todoItem.Complete ?
                    "Now complete!" : "Incomplete!"));
List<string> items = await query.ToListAsync();
```

<span data-ttu-id="a62e1-215">지금까지 설명한 모든 함수는 가산적이므로 계속해서 연결 상태를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-215">All the functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="a62e1-216">연결된 각 호출은 더 많은 쿼리에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-216">Each chained call affects more of the query.</span></span> <span data-ttu-id="a62e1-217">한 가지 예를 더 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="a62e1-218"><a name="lookingup"></a>방법: ID를 기준으로 데이터 조회</span><span class="sxs-lookup"><span data-stu-id="a62e1-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="a62e1-219">[LookupAsync] 함수를 사용하여 데이터베이스에서 특정 ID를 가진 개체를 조회할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-219">The [LookupAsync] function can be used to look up objects from the database with a particular ID.</span></span>

```
// This query filters out the item with the ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="a62e1-220"><a name="untypedqueries"></a>방법: 형식화되지 않은 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="a62e1-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="a62e1-221">형식화되지 않은 테이블 개체를 사용하여 쿼리를 실행하는 경우 다음 예제와 같이 [ReadAsync]를 호출하여 OData 쿼리 문자열을 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-221">When executing a query using an untyped table object, you must explicitly specify the OData query string by calling [ReadAsync], as in the following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="a62e1-222">속성 모음처럼 사용할 수 있는 JSON 값이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="a62e1-223">JToken 및 Newtonsoft Json.NET에 대한 자세한 내용은 [Json.NET] 사이트를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a62e1-223">For more information on JToken and Newtonsoft Json.NET, see the [Json.NET] site.</span></span>

### <span data-ttu-id="a62e1-224"><a name="inserting"></a>방법: 모바일 앱 백 엔드에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="a62e1-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="a62e1-225">모든 클라이언트 형식은 **ID**라는 멤버를 포함해야 하며 이는 기본적으로 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="a62e1-226">이 **ID** 는 CRUD 작업 및 오프라인 동기화를 수행하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-226">This **Id** is required to perform CRUD operations and for offline sync.</span></span> <span data-ttu-id="a62e1-227">다음 코드는 [InsertAsync] 메서드를 사용하여 테이블에 새 행을 삽입하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-227">The following code illustrates how to use the [InsertAsync] method to insert new rows into a table.</span></span> <span data-ttu-id="a62e1-228">매개 변수에는 .NET 개체로 삽입할 데이터가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-228">The parameter contains the data to be inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="a62e1-229">삽입하는 동안 고유한 사용자 지정 ID 값이 `todoItem` 에 포함되어 있지 않으면 서버에서 GUID를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-229">If a unique custom ID value is not included in the `todoItem` during an insert, a GUID is generated by the server.</span></span>
<span data-ttu-id="a62e1-230">호출이 반환된 후 개체를 검사하여 생성된 Id를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-230">You can retrieve the generated Id by inspecting the object after the call returns.</span></span>

<span data-ttu-id="a62e1-231">형식화되지 않은 데이터를 삽입하려는 경우 Json.NET을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-231">To insert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="a62e1-232">다음은 메일 주소를 고유 문자열 id로 사용하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-232">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="a62e1-233">ID 값으로 작업</span><span class="sxs-lookup"><span data-stu-id="a62e1-233">Working with ID values</span></span>
<span data-ttu-id="a62e1-234">모바일 앱은 테이블의 **id** 열에 대한 고유한 사용자 지정 문자열 값을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-234">Mobile Apps supports unique custom string values for the table's **id** column.</span></span> <span data-ttu-id="a62e1-235">문자열 값은 응용 프로그램에서 전자 메일 주소 또는 사용자 이름과 같은 사용자 지정 값을 ID에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-235">A string value allows applications to use custom values such as email addresses or user names for the ID.</span></span>  <span data-ttu-id="a62e1-236">문자열 ID는 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-236">String IDs provide you with the following benefits:</span></span>

* <span data-ttu-id="a62e1-237">ID는 데이터베이스에 대한 왕복 없이도 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-237">IDs are generated without making a round trip to the database.</span></span>
* <span data-ttu-id="a62e1-238">여러 테이블 또는 데이터베이스의 레코드를 병합하기가 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-238">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="a62e1-239">응용 프로그램의 논리를 통해 ID 값이 더 효율적으로 통합될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-239">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="a62e1-240">문자열 ID 값이 삽입된 레코드에 설정되지 않은 경우 모바일 앱 백 엔드는 해당 ID에 대한 고유한 값을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-240">When a string ID value is not set on an inserted record, the Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="a62e1-241">[Guid.NewGuid] 메서드를 사용하여 클라이언트나 백엔드에서 고유한 ID 값을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-241">You can use the [Guid.NewGuid] method to generate your own ID values, either on the client or in the backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="a62e1-242"><a name="modifying"></a>방법: 모바일 앱 백 엔드의 데이터 수정</span><span class="sxs-lookup"><span data-stu-id="a62e1-242"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="a62e1-243">다음 코드는 [UpdateAsync] 메서드를 사용하여 새로운 정보가 포함된 같은 ID로 기존 기록을 업데이트하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-243">The following code illustrates how to use the [UpdateAsync] method to update an existing record with the same ID with new information.</span></span> <span data-ttu-id="a62e1-244">매개 변수에는 .NET 개체로 업데이트할 데이터가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-244">The parameter contains the data to be updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="a62e1-245">형식화되지 않은 데이터를 업데이트하려는 경우 다음과 같이 [Json.NET] 을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-245">To update untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="a62e1-246">업데이트할 때 `id` 필드를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-246">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="a62e1-247">백 엔드는 `id` 필드를 사용하여 업데이트할 행을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-247">The backend uses the `id` field to identify which row to update.</span></span> <span data-ttu-id="a62e1-248">`id` 필드는 `InsertAsync` 호출의 결과에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-248">The `id` field can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="a62e1-249">`id` 값을 제공하지 않고 항목을 업데이트하려고 할 때 `ArgumentException`이(가) 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-249">An `ArgumentException` is raised if you try to update an item without providing the `id` value.</span></span>

### <span data-ttu-id="a62e1-250"><a name="deleting"></a>방법: 모바일 앱 백 엔드의 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="a62e1-250"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="a62e1-251">다음 코드는 [DeleteAsync] 메서드를 사용하여 기존 인스턴스를 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-251">The following code illustrates how to use the [DeleteAsync] method to delete an existing instance.</span></span> <span data-ttu-id="a62e1-252">인스턴스는 `todoItem`에 설정된 `id` 필드로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-252">The instance is identified by the `id` field set on the `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="a62e1-253">형식화되지 않은 데이터를 삭제하려면 다음과 같이 Json.NET을 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-253">To delete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="a62e1-254">삭제를 요청할 때 ID를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-254">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="a62e1-255">다른 속성은 서비스에 전달되지 않거나 서비스에서 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-255">Other properties are not passed to the service or are ignored at the service.</span></span> <span data-ttu-id="a62e1-256">`DeleteAsync` 호출의 결과는 일반적으로 `null`입니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-256">The result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="a62e1-257">전달할 ID는 `InsertAsync` 호출의 결과에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-257">The ID to pass in can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="a62e1-258">`id` 필드를 지정하지 않고 항목을 삭제하려고 할 때 `MobileServiceInvalidOperationException`이(가) 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-258">A `MobileServiceInvalidOperationException` is thrown when you try to delete an item without specifying the `id` field.</span></span>

### <span data-ttu-id="a62e1-259"><a name="optimisticconcurrency"></a>방법: 충돌 해결에 낙관적 동시성 사용</span><span class="sxs-lookup"><span data-stu-id="a62e1-259"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="a62e1-260">두 개 이상의 클라이언트가 동시에 동일 항목의 변경 내용을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-260">Two or more clients may write changes to the same item at the same time.</span></span> <span data-ttu-id="a62e1-261">충돌 검색 없이, 마지막으로 쓴 내용이 이전 업데이트를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-261">Without conflict detection, the last write would overwrite any previous updates.</span></span> <span data-ttu-id="a62e1-262">**낙관적 동시성 제어** 에서는 각 트랜잭션이 커밋할 수 있으므로 리소스 잠금을 사용하지 않는다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-262">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="a62e1-263">트랜잭션을 커밋하기 전에 낙관적 동시성 제어는 다른 트랜잭션에서 데이터를 수정하지 않았음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-263">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified the data.</span></span> <span data-ttu-id="a62e1-264">데이터가 수정된 경우에는 커밋 중인 트랜잭션이 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-264">If the data has been modified, the committing transaction is rolled back.</span></span>

<span data-ttu-id="a62e1-265">모바일 앱은 모바일 앱 백 엔드의 각 테이블에 대해 정의된 `version` 시스템 속성 열을 사용하는 각 항목의 변경 내용을 추적하여 낙관적 동시성 제어를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-265">Mobile Apps supports optimistic concurrency control by tracking changes to each item using the `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="a62e1-266">레코드가 업데이트될 때마다 모바일 앱은 해당 레코드의 `version` 속성을 새 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-266">Each time a record is updated, Mobile Apps sets the `version` property for that record to a new value.</span></span> <span data-ttu-id="a62e1-267">각 업데이트 요청 중에 요청에 포함된 레코드의 `version` 속성이 서버에 있는 레코드의 동일 속성과 비교됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-267">During each update request, the `version` property of the record included with the request is compared to the same property for the record on the server.</span></span> <span data-ttu-id="a62e1-268">요청과 함께 전달된 버전이 백 엔드와 일치하지 않는 경우 클라이언트 라이브러리는 `MobileServicePreconditionFailedException<T>` 예외를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-268">If the version passed with the request does not match the backend, then the client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="a62e1-269">예외에 포함된 형식은 백 엔드의 레코드이며 서버 버전의 레코드를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-269">The type included with the exception is the record from the backend containing the servers version of the record.</span></span> <span data-ttu-id="a62e1-270">그러면 응용 프로그램은 이 정보를 사용하여 변경을 커밋하기 위해 백 엔드의 올바른 `version` 값으로 업데이트 요청을 다시 실행할지 여부를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-270">The application can then use this information to decide whether to execute the update request again with the correct `version` value from the backend to commit changes.</span></span>

<span data-ttu-id="a62e1-271">낙관적 동시성을 사용하기 위해 `version` 시스템 속성의 테이블 클래스에 대해 열을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-271">Define a column on the table class for the `version` system property to enable optimistic concurrency.</span></span> <span data-ttu-id="a62e1-272">예:</span><span class="sxs-lookup"><span data-stu-id="a62e1-272">For example:</span></span>

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }

    // *** Enable Optimistic Concurrency *** //
    [JsonProperty(PropertyName = "version")]
    public string Version { set; get; }
}
```

<span data-ttu-id="a62e1-273">형식화되지 않은 테이블을 사용하는 응용 프로그램은 다음과 같이 테이블의 `SystemProperties`에 대해 `Version` 플래그를 설정하여 낙관적 동시성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-273">Applications using untyped tables enable optimistic concurrency by setting the `Version` flag on the `SystemProperties` of the table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="a62e1-274">낙관적 동시성을 사용하는 것 외에도 [UpdateAsync]를 호출할 때 코드에서 `MobileServicePreconditionFailedException<T>` 예외를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-274">In addition to enabling optimistic concurrency, you must also catch the `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="a62e1-275">업데이트된 레코드에 올바른 `version` 을(를) 적용하여 충돌을 해결하고 해결된 레코드로 [UpdateAsync] 를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-275">Resolve the conflict by applying the correct `version` to the updated record and call [UpdateAsync] with the resolved record.</span></span> <span data-ttu-id="a62e1-276">다음 코드는 감지된 쓰기 충돌을 해결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-276">The following code shows how to resolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at the remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, the item has changed since the last query
        // Resolve the conflict between the local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user to choose the resoltion between versions
    MessageDialog msgDialog = new MessageDialog(
        String.Format("Server Text: \"{0}\" \nLocal Text: \"{1}\"\n",
        serverItem.Text, localItem.Text),
        "CONFLICT DETECTED - Select a resolution:");

    UICommand localBtn = new UICommand("Commit Local Text");
    UICommand ServerBtn = new UICommand("Leave Server Text");
    msgDialog.Commands.Add(localBtn);
    msgDialog.Commands.Add(ServerBtn);

    localBtn.Invoked = async (IUICommand command) =>
    {
        // To resolve the conflict, update the version of the item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while the user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="a62e1-277">자세한 내용은 [Azure Mobile Apps에서 오프라인 데이터 동기화] 토픽을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a62e1-277">For more information, see the [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="a62e1-278"><a name="binding"></a>방법: 모바일 앱 데이터를 Windows 사용자 인터페이스에 바인딩</span><span class="sxs-lookup"><span data-stu-id="a62e1-278"><a name="binding"></a>How to: Bind Mobile Apps data to a Windows user interface</span></span>
<span data-ttu-id="a62e1-279">이 섹션에서는 반환된 데이터 개체를 Windows 앱의 UI 요소를 사용해서 표시하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-279">This section shows how to display returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="a62e1-280">다음 예제 코드는 완료되지 않은 항목에 대한 쿼리를 사용하여 목록의 소스에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-280">The following example code binds to the source of the list with a query for incomplete items.</span></span> <span data-ttu-id="a62e1-281">[MobileServiceCollection]은 Mobile Apps 인식 바인딩 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-281">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound to a UI list control
IEnumerable itemsControl  = items;

// Bind this to a ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="a62e1-282">관리되는 런타임의 일부 컨트롤은 [ISupportIncrementalLoading]이라는 인터페이스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-282">Some controls in the managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="a62e1-283">이 인터페이스에서는 사용자가 스크롤할 때 컨트롤이 추가 데이터를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-283">This interface allows controls to request extra data when the user scrolls.</span></span> <span data-ttu-id="a62e1-284">컨트롤에서 발생하는 호출을 자동으로 처리하는 [MobileServiceIncrementalLoadingCollection]을 통해 유니버설 Windows 앱용으로 이 인터페이스를 기본적으로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-284">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from the controls.</span></span> <span data-ttu-id="a62e1-285">다음과 같이 Windows 앱에서 `MobileServiceIncrementalLoadingCollection` 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-285">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="a62e1-286">Windows Phone 8 및 "Silverlight" 앱에서 새 컬렉션을 사용하려면 `IMobileServiceTableQuery<T>` 및 `IMobileServiceTable<T>`에서 `ToCollection` 확장 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-286">To use the new collection on Windows Phone 8 and "Silverlight" apps, use the `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="a62e1-287">데이터를 로드하려면 `LoadMoreItemsAsync()`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-287">To load data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="a62e1-288">`ToCollectionAsync` 또는 `ToCollection`을 호출하여 만들어진 컬렉션을 사용하는 경우 UI 컨트롤에 바인딩할 수 있는 컬렉션을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-288">When you use the collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound to UI controls.</span></span>  <span data-ttu-id="a62e1-289">이 컬렉션은 페이징을 인식합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-289">This collection is paging-aware.</span></span>  <span data-ttu-id="a62e1-290">이 컬렉션은 네트워크에서 데이터를 로드하므로 가끔 로드가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-290">Since the collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="a62e1-291">이 오류를 처리하려면 `LoadMoreItemsAsync` 호출의 결과로 발생한 예외를 처리하도록 `MobileServiceIncrementalLoadingCollection`에 대한 `OnException` 메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-291">To handle such failures, override the `OnException` method on `MobileServiceIncrementalLoadingCollection` to handle exceptions resulting from calls to `LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="a62e1-292">테이블에 여러 필드가 있지만 그 중 일부만 컨트롤에 표시하려는 경우를 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-292">Consider if your table has many fields but you only want to display some of them in your control.</span></span> <span data-ttu-id="a62e1-293">앞에서 나온 “[특정 열 선택](#selecting)” 섹션의 지침에 따라 UI에 표시할 특정 열을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-293">You may use the guidance in the preceding section "[Select specific columns](#selecting)" to select specific columns to display in the UI.</span></span>

### <span data-ttu-id="a62e1-294"><a name="pagesize"></a>페이지 크기 변경</span><span class="sxs-lookup"><span data-stu-id="a62e1-294"><a name="pagesize"></a>Change the Page size</span></span>
<span data-ttu-id="a62e1-295">Azure Mobile Apps는 기본적으로 요청당 최대 50개의 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-295">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="a62e1-296">클라이언트와 서버 모두에서 최대 페이지 크기를 늘려 페이징 크기를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-296">You can change the paging size by increasing the maximum page size on both the client and server.</span></span>  <span data-ttu-id="a62e1-297">요청된 페이지 크기를 늘리려면 `PullAsync()`를 사용하는 경우 `PullOptions`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-297">To increase the requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="a62e1-298">서버 내에서 `PageSize` 를 100보다 크거나 같게 지정했다고 가정할 경우 각 요청에서 최대 100개의 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-298">Assuming you have made the `PageSize` equal to or greater than 100 within the server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="a62e1-299"><a name="#offlinesync"></a>오프라인 데이터 작업</span><span class="sxs-lookup"><span data-stu-id="a62e1-299"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="a62e1-300">오프 라인 테이블은 오프 라인일 때 사용 하기 위해 로컬 SQLite 저장소에서 저장소 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-300">Offline tables use a local SQLite store to store data for use when offline.</span></span>  <span data-ttu-id="a62e1-301">모든 테이블 작업은 원격 서버 저장소 대신 로컬 SQLite 저장소에 대해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-301">All table operations are done against the local SQLite store instead of the remote server store.</span></span>  <span data-ttu-id="a62e1-302">오프라인 테이블을 만들려면, 먼저 프로젝트를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-302">To create an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="a62e1-303">Visual Studio에서 솔루션 > **솔루션에 대한 NuGet 패키지 관리...**를 마우스 오른쪽 단추로 클릭한 후 솔루션의 모든 프로젝트에서 **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet 패키지를 검색하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-303">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span></span>
2. <span data-ttu-id="a62e1-304">(선택 사항) Windows 장치를 지원하려면 다음 SQLite 런타임 패키지 중 하나를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-304">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span></span>

   * <span data-ttu-id="a62e1-305">**Windows 8.1 런타임:** [Windows 8.1][3]용 SQLite를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-305">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="a62e1-306">**Windows Phone 8.1:** [Windows Phone 8.1][4]용 SQLite를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-306">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="a62e1-307">**범용 Windows 플랫폼** [범용 Windows용 SQLite][5]를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-307">**Universal Windows Platform** Install [SQLite for the Universal Windows][5].</span></span>
3. <span data-ttu-id="a62e1-308">(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="a62e1-308">(Optional).</span></span> <span data-ttu-id="a62e1-309">Windows 장치의 경우, **참조** > **참조 추가...**, **Windows** 폴더 > **확장**을 펼친 후, **Visual C++ 2013 Runtime for Windows** SDK와 함께 해당 **SQLite for Windows** SDK를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-309">For Windows devices, click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**, then enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="a62e1-310">SQLite SDK 이름은 Windows 플랫폼마다 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-310">The SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="a62e1-311">테이블 참조를 만들기 전에, 로컬 저장소를 준비해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-311">Before a table reference can be created, the local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes the SyncContext using the default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="a62e1-312">클라이언트를 만든 후 저장소 초기화는 일반적으로 즉시 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-312">Store initialization is normally done immediately after the client is created.</span></span>  <span data-ttu-id="a62e1-313">**OfflineDbPath**는 모든 플랫폼에서 사용하기에 적합한 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-313">The **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="a62e1-314">경로가 정규화 된 경로인 경우 (즉, 슬래시로 시작), 해당 경로를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-314">If the path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="a62e1-315">경로가 정규화되지 않은 경우 파일은 플랫폼 특정 위치에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-315">If the path is not fully qualified, the file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="a62e1-316">IOS 및 Android 장치에 대한 기본 경로는 "개인 파일" 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-316">For iOS and Android devices, the default path is the "Personal Files" folder.</span></span>
* <span data-ttu-id="a62e1-317">Windows 장치에 대한 기본 경로는 응용 프로그램별 "AppData" 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-317">For Windows devices, the default path is the application-specific "AppData" folder.</span></span>

<span data-ttu-id="a62e1-318">`GetSyncTable<>` 메서드를 사용하여 테이블 참조를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-318">A table reference can be obtained using the `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="a62e1-319">오프라인 테이블을 사용하여 인증할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-319">You do not need to authenticate to use an offline table.</span></span>  <span data-ttu-id="a62e1-320">백 엔드 서비스와 통신하는 경우 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-320">You only need to authenticate when you are communicating with the backend service.</span></span>

### <span data-ttu-id="a62e1-321"><a name="syncoffline"></a>오프라인 테이블 동기화</span><span class="sxs-lookup"><span data-stu-id="a62e1-321"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="a62e1-322">기본적으로 오프라인 테이블은 백 엔드와 동기화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-322">Offline tables are not synchronized with the backend by default.</span></span>  <span data-ttu-id="a62e1-323">동기화는 두 부분으로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-323">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="a62e1-324">새 항목 다운로드에서 별도로 변경 내용을 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-324">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="a62e1-325">다음은 일반적인 동기화 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-325">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //The first parameter is a query name that is used internally by the client SDK to implement incremental sync.
            //Use a different query name for each unique query in your program
            "allTodoItems",
            this.todoTable.CreateQuery());
    }
    catch (MobileServicePushFailedException exc)
    {
        if (exc.PushResult != null)
        {
            syncErrors = exc.PushResult.Errors;
        }
    }

    // Simple error/conflict handling. A real application would handle the various errors like network conditions,
    // server conflicts and others via the IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting to server's copy.
                await error.CancelAndUpdateItemAsync(error.Result);
            }
            else
            {
                // Discard local change.
                await error.CancelAndDiscardItemAsync();
            }

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

<span data-ttu-id="a62e1-326">`PullAsync`에 대한 첫 번째 인수가 null인 경우, 증분 동기화가 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-326">If the first argument to `PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="a62e1-327">각 동기화 작업은 모든 레코드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-327">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="a62e1-328">SDK는 레코드를 끌어오기 전에 암시적 `PushAsync()`을(를) 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-328">The SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="a62e1-329">`PullAsync()` 메서드에서 충돌 처리가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-329">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="a62e1-330">온라인 테이블과 같은 방식으로 충돌을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-330">You can deal with conflicts in the same way as online tables.</span></span>  <span data-ttu-id="a62e1-331">충돌은 삽입, 업데이트 또는 삭제하는 동안 이를 대신하여 `PullAsync()`이 호출될 때 충돌이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-331">The conflict is produced when `PullAsync()` is called instead of during the insert, update, or delete.</span></span> <span data-ttu-id="a62e1-332">여러 충돌이 발생하는 경우 단일 MobileServicePushFailedException에 함께 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-332">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="a62e1-333">각 오류를 개별적으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-333">Handle each failure separately.</span></span>

## <span data-ttu-id="a62e1-334"><a name="#customapi"></a>사용자 지정 API 작업</span><span class="sxs-lookup"><span data-stu-id="a62e1-334"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="a62e1-335">사용자 지정 API는 삽입, 업데이트, 삭제 또는 읽기 작업에 매핑되지 않는 서버 기능을 노출하는 사용자 지정 끝점을 정의할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-335">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="a62e1-336">사용자 지정 API를 사용하면 HTTP 메시지 헤더 읽기와 설정 및 JSON 이외의 메시지 본문 형식 정의를 비롯하여 더 효율적으로 메시징을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-336">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="a62e1-337">클라이언트에서 [InvokeApiAsync] 메서드 중 하나를 호출하여 사용자 지정 API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-337">You call a custom API by calling one of the [InvokeApiAsync] methods on the client.</span></span> <span data-ttu-id="a62e1-338">예를 들어 다음 코드 줄은 백 엔드에서 **completeAll** API로 POST 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-338">For example, the following line of code sends a POST request to the **completeAll** API on the backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="a62e1-339">이 양식은 형식화된 메서드 호출이며 **MarkAllResult** 반환 형식을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-339">This form is a typed method call and requires that the **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="a62e1-340">형식화된 메서드와 형식화되지 않은 메서드가 모두 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-340">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="a62e1-341">InvokeApiAsync() 메소드는 API가 '/'로 시작하는 경우를 제외하고 호출하려는 API 앞에 '/api/'를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-341">The InvokeApiAsync() method prepends '/api/' to the API that you wish to call unless the API starts with a '/'.</span></span>
<span data-ttu-id="a62e1-342">예:</span><span class="sxs-lookup"><span data-stu-id="a62e1-342">For example:</span></span>

* <span data-ttu-id="a62e1-343">`InvokeApiAsync("completeAll",...)` - 백 엔드에서 /api/completeAll 호출</span><span class="sxs-lookup"><span data-stu-id="a62e1-343">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on the backend</span></span>
* <span data-ttu-id="a62e1-344">`InvokeApiAsync("/.auth/me",...)` - 백 엔드에서 /.auth/me 호출</span><span class="sxs-lookup"><span data-stu-id="a62e1-344">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on the backend</span></span>

<span data-ttu-id="a62e1-345">InvokeApiAsync를 사용하여 Azure Mobile Apps로 정의되지 않은 WebAPI를 포함한 WebAPI를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-345">You can use InvokeApiAsync to call any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="a62e1-346">InvokeApiAsync()를 사용할 경우 인증 헤더를 포함한 적합한 헤더가 요청과 함께 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-346">When you use InvokeApiAsync(), the appropriate headers, including authentication headers, are sent with the request.</span></span>

## <span data-ttu-id="a62e1-347"><a name="authentication"></a>사용자 인증</span><span class="sxs-lookup"><span data-stu-id="a62e1-347"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="a62e1-348">Mobile Apps는 Facebook, Google, Microsoft 계정, Twitter 및 Azure Active Directory와 같이 다양한 외부 ID 공급자를 사용하여 앱 사용자의 인증 및 권한 부여를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-348">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="a62e1-349">테이블에 대해 사용 권한을 설정하여 특정 작업을 위한 액세스를 인증된 사용자로만 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-349">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="a62e1-350">인증된 사용자의 ID를 사용하여 서버 스크립트에 인증 규칙을 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-350">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="a62e1-351">자세한 내용은 [앱에 인증 추가]자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a62e1-351">For more information, see the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="a62e1-352">두 가지의 인증 흐름이 지원 됩니다: *클라이언트 관리* 및 *서버 관리* 흐름입니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-352">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="a62e1-353">서버 관리 흐름의 경우 공급자의 웹 인증 인터페이스를 사용하므로 인증 경험이 가장 단순합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-353">The server-managed flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="a62e1-354">클라이언트 관리 흐름의 경우 공급자 특정 장치별 SDK를 사용하므로 장치 특정 기능을 통해 더욱 강력한 통합이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-354">The client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="a62e1-355">프로덕션 앱에서 클라이언트 관리 흐름을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-355">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="a62e1-356">인증을 설정하려면 하나 이상의 ID 공급자로 앱을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-356">To set up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="a62e1-357">ID 공급자는 앱의 클라이언트 ID 및 클라이언트 암호를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-357">The identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="a62e1-358">그러면 Azure App Service 인증/권한 부여를 사용할 수 있도록 백 엔드에서 이러한 값이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-358">These values are then set in your backend to enable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="a62e1-359">자세한 내용은 [앱에 인증 추가]자습서의 자세한 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="a62e1-359">For more information, follow the detailed instructions in the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="a62e1-360">이 섹션에서 다루는 토픽은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-360">The following topics are covered in this section:</span></span>

* [<span data-ttu-id="a62e1-361">클라이언트 관리 인증</span><span class="sxs-lookup"><span data-stu-id="a62e1-361">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="a62e1-362">서버 관리 인증</span><span class="sxs-lookup"><span data-stu-id="a62e1-362">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="a62e1-363">인증 토큰 캐시</span><span class="sxs-lookup"><span data-stu-id="a62e1-363">Caching the authentication token</span></span>](#caching)

### <span data-ttu-id="a62e1-364"><a name="clientflow"></a>클라이언트 관리 인증</span><span class="sxs-lookup"><span data-stu-id="a62e1-364"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="a62e1-365">앱이 독립적으로 ID 공급자에 연결한 후 반환된 토큰을 백 엔드로 로그인하는 동안 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-365">Your app can independently contact the identity provider and then provide the returned token during login with your backend.</span></span> <span data-ttu-id="a62e1-366">이 클라이언트 흐름을 사용하면 단일 로그온 환경을 사용자에게 제공하거나 ID 공급자로부터 더 많은 사용자 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-366">This client flow enables you to provide a single sign-on experience for users or to retrieve additional user data from the identity provider.</span></span> <span data-ttu-id="a62e1-367">클라이언트 흐름 인증은 ID 공급자 SDK가 UX 느낌을 그대로 제공하고 추가 사용자 지정을 허용하기에 서버 흐름보다 선호도가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-367">Client flow authentication is preferred to using a server flow as the identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="a62e1-368">다음 클라이언트 흐름 인증 패턴에 대한 예제가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-368">Examples are provided for the following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="a62e1-369">Active Directory 인증 라이브러리</span><span class="sxs-lookup"><span data-stu-id="a62e1-369">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="a62e1-370">Facebook 또는 Google</span><span class="sxs-lookup"><span data-stu-id="a62e1-370">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="a62e1-371">Live SDK</span><span class="sxs-lookup"><span data-stu-id="a62e1-371">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="a62e1-372"><a name="adal"></a>Active Directory 인증 라이브러리를 사용하여 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="a62e1-372"><a name="adal"></a>Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="a62e1-373">Azure Active Directory 인증을 사용하여 클라이언트에서 사용자 인증을 시작하려면 Active Directory 인증 라이브러리(ADAL)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-373">You can use the Active Directory Authentication Library (ADAL) to initiate user authentication from the client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="a62e1-374">다음으로 [Active Directory 로그온에 앱 서비스를 구성하는 방법] 자습서를 수행하여 AAD 로그인에 모바일 앱 백 엔드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-374">Configure your mobile app backend for AAD sign-on by following the [How to configure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="a62e1-375">네이티브 클라이언트 응용 프로그램을 등록하는 선택적 단계를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-375">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="a62e1-376">Visual Studio 또는 Xamarin Studio에서 프로젝트를 열고 `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet 패키지에 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-376">In Visual Studio or Xamarin Studio, open your project and add a reference to the `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="a62e1-377">검색할 때 시험판 버전을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-377">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="a62e1-378">사용하는 플랫폼에 따라 응용 프로그램에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-378">Add the following code to your application, according to the platform you are using.</span></span> <span data-ttu-id="a62e1-379">각각에서 다음과 같이 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-379">In each, make the following replacements:</span></span>

   * <span data-ttu-id="a62e1-380">**INSERT-AUTHORITY-HERE** 를 응용 프로그램이 프로비전된 테넌트의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-380">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="a62e1-381">형식은 https://login.microsoftonline.com/contoso.onmicrosoft.com이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-381">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="a62e1-382">이 값은 [Azure 클래식 포털]의 Azure Active Directory에 있는 도메인 탭에서 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-382">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="a62e1-383">**INSERT-RESOURCE-ID-HERE** 를 모바일 앱 백 엔드에 대한 클라이언트 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-383">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="a62e1-384">포털의 Azure **Active Directory 설정**에 있는 **고급** 탭에서 클라이언트 ID를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-384">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="a62e1-385">**INSERT-CLIENT-ID-HERE** 를 네이티브 클라이언트 응용 프로그램에서 복사한 클라이언트 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-385">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="a62e1-386">HTTPS 체계를 사용하여 **INSERT-REDIRECT-URI-HERE** 를 사이트의 */.auth/login/done* 끝점으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-386">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="a62e1-387">이 값은 *https://contoso.azurewebsites.net/.auth/login/done*과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-387">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="a62e1-388">각 플랫폼에 필요한 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-388">The code needed for each platform follows:</span></span>

     <span data-ttu-id="a62e1-389">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="a62e1-389">**Windows:**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        while (user == null)
        {
            string message;
            try
            {
                AuthenticationContext ac = new AuthenticationContext(authority);
                AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                    new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, false) );
                JObject payload = new JObject();
                payload["access_token"] = ar.AccessToken;
                user = await App.MobileService.LoginAsync(
                    MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
                message = string.Format("You are now logged in - {0}", user.UserId);
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
    ```

     <span data-ttu-id="a62e1-390">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="a62e1-390">**Xamarin.iOS**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync(UIViewController view)
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(view));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine(@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
        }
    }
    ```

     <span data-ttu-id="a62e1-391">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="a62e1-391">**Xamarin.Android**</span></span>

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(this));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(ex.Message);
            builder.SetTitle("You must log in. Login Required");
            builder.Create().Show();
        }
    }
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {

        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ```

#### <span data-ttu-id="a62e1-392"><a name="client-facebook"></a>Facebook 또는 Google의 토큰을 사용하는 Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="a62e1-392"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="a62e1-393">다음과 같은 Facebook 또는 Google용 코드 조각에 나온 대로 클라이언트 흐름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-393">You can use the client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using the Facebook or Google SDK.
token.Add("access_token", "access_token_value");

private MobileServiceUser user;
private async Task AuthenticateAsync()
{
    while (user == null)
    {
        string message;
        try
        {
            // Change MobileServiceAuthenticationProvider.Facebook
            // to MobileServiceAuthenticationProvider.Google if using Google auth.
            user = await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
            message = string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

#### <span data-ttu-id="a62e1-394"><a name="client-livesdk"></a>Live SDK와 함께 Microsoft 계정을 사용한 단일 로그인</span><span class="sxs-lookup"><span data-stu-id="a62e1-394"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with the Live SDK</span></span>
<span data-ttu-id="a62e1-395">사용자를 인증하려면 먼저 Microsoft 계정 개발자 센터에서 앱을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-395">To authenticate users, you must register your app at the Microsoft account Developer Center.</span></span> <span data-ttu-id="a62e1-396">모바일 앱 백 엔드의 등록 세부 정보를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-396">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="a62e1-397">Microsoft 계정 등록을 만들어서 모바일 앱 백 엔드에 연결하려면 [Microsoft 계정 로그인을 사용하도록 앱 등록]의 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-397">To create a Microsoft account registration and connect it to your Mobile App backend, complete the steps in [Register your app to use a Microsoft account login].</span></span> <span data-ttu-id="a62e1-398">Windows 스토어 및 Windows Phone 8/Silverlight 버전의 앱이 둘 다 있는 경우 Windows 스토어 버전을 먼저 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-398">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register the Windows Store version first.</span></span>

<span data-ttu-id="a62e1-399">다음 코드는 Live SDK를 사용하여 인증하고 반환된 토큰을 사용하여 모바일 앱 백 엔드에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-399">The following code authenticates using Live SDK and uses the returned token to sign in to your Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get the URL the Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create the authentication client for Windows Store using the service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create the authentication client for Windows Phone using the client ID of the registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request the authentication token from the Live authentication service.
        // The wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about the logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use the Microsoft account auth token to sign in to App Service.
            MobileServiceUser loginResult = await App.MobileService
                .LoginWithMicrosoftAccountAsync(result.Session.AuthenticationToken);

            // Display a personalized sign-in greeting.
            string title = string.Format("Welcome {0}!", meResult.Result["first_name"]);
            var message = string.Format("You are now logged in - {0}", loginResult.UserId);
            var dialog = new MessageDialog(message, title);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
        else
        {
            session = null;
            var dialog = new MessageDialog("You must log in.", "Login Required");
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
}
```

<span data-ttu-id="a62e1-400">자세한 내용은 [Windows Live SDK] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a62e1-400">For more information, see the [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="a62e1-401"><a name="serverflow"></a>서버 관리 인증</span><span class="sxs-lookup"><span data-stu-id="a62e1-401"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="a62e1-402">ID 공급자를 등록하고 나면, 공급자의 [MobileServiceAuthenticationProvider] 값을 사용하여 MobileServiceClient의 [LoginAsync] 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-402">Once you have registered your identity provider, call the [LoginAsync] method on the [MobileServiceClient] with the [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="a62e1-403">예를 들어 다음 코드는 Facebook을 사용한 서버 흐름 로그인을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-403">For example, the following code initiates a server flow sign-in by using Facebook.</span></span>

```
private MobileServiceUser user;
private async System.Threading.Tasks.Task Authenticate()
{
    while (user == null)
    {
        string message;
        try
        {
            user = await client
                .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
            message =
                string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

<span data-ttu-id="a62e1-404">Facebook 이외의 ID 공급자를 사용하는 경우, [MobileServiceAuthenticationProvider] 값을 공급자에 대한 값으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-404">If you are using an identity provider other than Facebook, change the value of [MobileServiceAuthenticationProvider] to the value for your provider.</span></span>

<span data-ttu-id="a62e1-405">서버 흐름에서 Azure App Service는 선택한 공급자의 로그인 페이지를 표시하여 OAuth 인증 흐름을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-405">In a server flow, Azure App Service manages the OAuth authentication flow by displaying the sign-in page of the selected provider.</span></span>  <span data-ttu-id="a62e1-406">ID 공급자가 결과를 반환하면 Azure App Service가 App Service 인증 토큰을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-406">Once the identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="a62e1-407">[LoginAsync] 메서드는 [MobileServiceUser]를 반환하며, 여기서 인증된 사용자의 [UserId] 및 [MobileServiceAuthenticationToken]이 JWT(JSON web token)로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-407">The [LoginAsync] method returns a [MobileServiceUser], which provides both the [UserId] of the authenticated user and the [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="a62e1-408">이 토큰은 캐시했다가 만료될 때까지 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-408">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="a62e1-409">자세한 내용은 [인증 토큰 캐시](#caching)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="a62e1-409">For more information, see [Caching the authentication token](#caching).</span></span>

### <span data-ttu-id="a62e1-410"><a name="caching"></a>인증 토큰 캐시</span><span class="sxs-lookup"><span data-stu-id="a62e1-410"><a name="caching"></a>Caching the authentication token</span></span>
<span data-ttu-id="a62e1-411">경우에 따라 공급자의 인증 토큰을 저장하여 첫 번째 인증 후 login 메서드에 대한 호출을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-411">In some cases, the call to the login method can be avoided after the first successful authentication by storing the authentication token from the provider.</span></span>  <span data-ttu-id="a62e1-412">Windows 스토어 및 UWP 앱은 [PasswordVault] 를 사용하여 다음과 같이 성공적인 로그인 후 현재 인증 토큰을 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-412">Windows Store and UWP apps can use [PasswordVault] to cache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="a62e1-413">UserId 값은 자격 증명의 사용자 이름으로 저장되며 토큰은 암호로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-413">The UserId value is stored as the UserName of the credential and the token is the stored as the Password.</span></span> <span data-ttu-id="a62e1-414">이후 시작 시 캐시된 자격 증명에 대한 **PasswordVault** 를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-414">On subsequent start-ups, you can check the **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="a62e1-415">다음 예제는 검색될 때 캐시된 자격 증명을 사용하고 그렇지 않으면 백 엔드로 인증을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-415">The following example uses cached credentials when they are found, and otherwise attempts to authenticate again with the backend:</span></span>

```
// Try to retrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create the current user from the stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache the token as shown above.
}
```

<span data-ttu-id="a62e1-416">사용자를 로그아웃할 때 다음과 같이 저장된 자격 증명도 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-416">When you sign out a user, you must also remove the stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="a62e1-417">Xamarin 앱은 [Xamarin.Auth] API를 사용하여 **Account** 개체에 자격 증명을 안전하게 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-417">Xamarin    apps use the [Xamarin.Auth] APIs to securely store credentials in an **Account** object.</span></span> <span data-ttu-id="a62e1-418">이러한 API 사용의 예제는 [ContosoMoments 사진 공유 샘플](https://github.com/azure-appservice-samples/ContosoMoments)에서 [AuthStore.cs] 코드 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a62e1-418">For an example of using these APIs, see the [AuthStore.cs] code file in the [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="a62e1-419">클라이언트 관리 인증을 사용하는 경우 Facebook 또는 Twitter와 같은 공급자로부터 얻은 액세스 토큰을 캐시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-419">When you use client-managed authentication, you can also cache the access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="a62e1-420">다음과 같이 백 엔드에서 새 인증 토큰을 요청하기 위해 이 토큰을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-420">This token can be supplied to request a new authentication token from the backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using the access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="a62e1-421"><a name="pushnotifications"></a>푸시 알림</span><span class="sxs-lookup"><span data-stu-id="a62e1-421"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="a62e1-422">다음 토픽에서는 푸시 알림에 대해 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-422">The following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="a62e1-423">푸시 알림 등록</span><span class="sxs-lookup"><span data-stu-id="a62e1-423">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="a62e1-424">Windows 스토어 패키지 SID 가져오기</span><span class="sxs-lookup"><span data-stu-id="a62e1-424">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="a62e1-425">플랫폼 간 템플릿을 사용하여 등록</span><span class="sxs-lookup"><span data-stu-id="a62e1-425">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="a62e1-426"><a name="register-for-push"></a>방법: 푸시 알림 등록</span><span class="sxs-lookup"><span data-stu-id="a62e1-426"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="a62e1-427">모바일 앱 클라이언트를 사용하면 Azure 알림 허브로 푸시 알림을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-427">The Mobile Apps client enables you to register for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="a62e1-428">등록할 때 플랫폼 특정 푸시 알림 서비스(PNS)에서 구하는 핸들을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-428">When registering, you obtain a handle that you obtain from the platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="a62e1-429">그런 다음 등록을 만들 때 태그와 함께 이 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-429">You then provide this value along with any tags when you create the registration.</span></span> <span data-ttu-id="a62e1-430">다음 코드는 Windows 알림 서비스(WNS)를 통한 푸시 알림에 Windows 앱을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-430">The following code registers your Windows app for push notifications with the Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using the new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="a62e1-431">WNS에 푸시하는 경우, [Windows 스토어 패키지 SID를 가져와야](#package-sid) 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-431">If you are pushing to WNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="a62e1-432">템플릿 등록 방법을 비롯하여 Windows 앱에 대한 자세한 내용은 [앱에 푸시 알림 추가]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a62e1-432">For more information on Windows apps, including how to register for template registrations, see [Add push notifications to your app].</span></span>

<span data-ttu-id="a62e1-433">클라이언트에서 태그 요청은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-433">Requesting tags from the client is not supported.</span></span>  <span data-ttu-id="a62e1-434">태그 요청은 등록에서 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-434">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="a62e1-435">태그로 장치를 등록하려는 경우 사용자를 대신해 알림 허브 API를 사용하여 등록을 수행하는 사용자 지정 API를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-435">If you wish to register your device with tags, create a Custom API that uses the Notification Hubs API to perform the registration on your behalf.</span></span>  <span data-ttu-id="a62e1-436">`RegisterNativeAsync()` 메서드 대신에 [사용자 지정 API를 호출합니다.](#customapi)</span><span class="sxs-lookup"><span data-stu-id="a62e1-436">[Call the Custom API](#customapi) instead of the `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="a62e1-437"><a name="package-sid"></a>방법: Windows 스토어 패키지 SID 가져오기</span><span class="sxs-lookup"><span data-stu-id="a62e1-437"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="a62e1-438">Windows 스토어 앱에서 푸시 알림 사용에 패키지 SID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-438">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="a62e1-439">패키지 SID를 수신하려면, Windows 스토어에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-439">To receive a package SID, register your application with the Windows Store.</span></span>

<span data-ttu-id="a62e1-440">이 값을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="a62e1-440">To obtain this value:</span></span>

1. <span data-ttu-id="a62e1-441">Visual Studio 솔루션 탐색기에서 Windows 스토어 앱 프로젝트를 마우스 오른쪽 단추로 클릭하고, **스토어** > **스토어와 앱을 연결...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-441">In Visual Studio Solution Explorer, right-click the Windows Store app project, click **Store** > **Associate App with the Store...**.</span></span>
2. <span data-ttu-id="a62e1-442">마법사에서 **다음**을 클릭하고, Microsoft 계정으로 로그인하고, **새로운 앱 이름 예약**에서 앱 이름을 입력한 후 **예약**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-442">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="a62e1-443">앱을 등록한 후에는 앱 이름을 선택하고 **다음**, **연결**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-443">After the app registration is successfully created, select the app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="a62e1-444">Microsoft 계정을 사용하여 [Windows 개발자 센터] 에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-444">Log in to the [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="a62e1-445">**내 앱**에서 방금 만든 앱 등록을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-445">Under **My apps**, click the app registration you created.</span></span>
5. <span data-ttu-id="a62e1-446">**앱 관리** > **앱 ID**를 클릭한 다음, 아래로 스크롤하여 **패키지 SID**를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-446">Click **App management** > **App identity**, and then scroll down to find your **Package SID**.</span></span>

<span data-ttu-id="a62e1-447">패키지 SID를 URI로 처리하여 다양하게 사용할 수 있으며, 이 경우 *ms-app://* 를 스키마로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-447">Many uses of the package SID treat it as a URI, in which case you need to use *ms-app://* as the scheme.</span></span> <span data-ttu-id="a62e1-448">이 값을 접두사로 연결하여 만든 패키지 SID의 버전을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-448">Make note of the version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="a62e1-449">iOS 또는 Android 플랫폼에서 실행되는 앱을 등록하려면 Xamarin 앱에 추가 코드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-449">Xamarin apps require some additional code to be able to register an app running on the iOS or Android platforms.</span></span> <span data-ttu-id="a62e1-450">자세한 내용은 사용하는 플랫폼에 대한 토픽을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a62e1-450">For more information, see the topic for your platform:</span></span>

* [<span data-ttu-id="a62e1-451">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="a62e1-451">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="a62e1-452">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="a62e1-452">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="a62e1-453"><a name="register-xplat"></a>방법: 플랫폼 간 알림을 보내기 위해 푸시 템플릿 등록</span><span class="sxs-lookup"><span data-stu-id="a62e1-453"><a name="register-xplat"></a>How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="a62e1-454">템플릿을 등록하려면 다음과 같이 템플릿으로 `RegisterAsync()` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-454">To register templates, use the `RegisterAsync()` method with the templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="a62e1-455">템플릿은 `JObject` 형식이어야 하며 다음 JSON 형식으로 여러 템플릿을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-455">Your templates should be `JObject` types and can contain multiple templates in the following JSON format:</span></span>

```
public JObject myTemplates()
{
    // single template for Windows Notification Service toast
    var template = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(message)</text></binding></visual></toast>";

    var templates = new JObject
    {
        ["generic-message"] = new JObject
        {
            ["body"] = template,
            ["headers"] = new JObject
            {
                ["X-WNS-Type"] = "wns/toast"
            },
            ["tags"] = new JArray()
        },
        ["more-templates"] = new JObject {...}
    };
    return templates;
}
```

<span data-ttu-id="a62e1-456">또한 **RegisterAsync()** 메서드는 보조 타일을 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-456">The method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="a62e1-457">보안을 위해 등록하는 동안 모든 태그가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-457">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="a62e1-458">설치에 태그를 추가하거나 설치 내에 템플릿을 추가하려면 [Azure Mobile Apps에 대해 .NET 백 엔드 서버 SDK로 작업]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a62e1-458">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="a62e1-459">이러한 등록된 템플릿을 활용하여 알림을 보내려면 [Notification Hubs API]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a62e1-459">To send notifications utilizing these registered templates, refer to the [Notification Hubs APIs].</span></span>

## <span data-ttu-id="a62e1-460"><a name="misc"></a>기타 토픽</span><span class="sxs-lookup"><span data-stu-id="a62e1-460"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="a62e1-461"><a name="errors"></a>방법: 오류 처리</span><span class="sxs-lookup"><span data-stu-id="a62e1-461"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="a62e1-462">백 엔드에서 오류가 발생하는 경우 클라이언트 SDK가 `MobileServiceInvalidOperationException`을 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-462">When an error occurs in the backend, the client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="a62e1-463">다음 예제에서는 백 엔드에서 반환되는 예외를 처리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-463">The following example shows how to handle an exception that is returned by the backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into the database. When the operation completes
    // and App Service has assigned an Id, the item is added to the CollectionView
    try
    {
        await todoTable.InsertAsync(todoItem);
        items.Add(todoItem);
    }
    catch (MobileServiceInvalidOperationException e)
    {
        // Handle error
    }
}
```

<span data-ttu-id="a62e1-464">오류 조건을 처리하는 또 다른 예는 [Mobile Apps 파일 샘플]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-464">Another example of dealing with error conditions can be found in the [Mobile Apps Files Sample].</span></span> <span data-ttu-id="a62e1-465">[LoggingHandler] 예제는 백 엔드에 대해 생성되는 요청을 기록하는 로깅 대리자 처리기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-465">The [LoggingHandler] example provides a logging delegate handler to log the requests being made to the backend.</span></span>

### <span data-ttu-id="a62e1-466"><a name="headers"></a>방법: 요청 헤더 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="a62e1-466"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="a62e1-467">특정 앱 시나리오를 지원하려면 모바일 앱 백 엔드와의 통신을 사용자 지정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-467">To support your specific app scenario, you might need to customize communication with the Mobile App backend.</span></span> <span data-ttu-id="a62e1-468">예를들어, 모든 보내는 요청이나 변경 응답 상태 코드에 사용자 지정 헤더를 추가하고자 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-468">For example, you may want to add a custom header to every outgoing request or even change responses status codes.</span></span> <span data-ttu-id="a62e1-469">다음 예제와 같이 사용자 지정 [DelegatingHandler]를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a62e1-469">You can use a custom [DelegatingHandler], as in the following example:</span></span>

```
public async Task CallClientWithHandler()
{
    MobileServiceClient client = new MobileServiceClient("AppUrl", new MyHandler());
    IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
    var newItem = new TodoItem { Text = "Hello world", Complete = false };
    await todoTable.InsertAsync(newItem);
}

public class MyHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage>
        SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        // Change the request-side here based on the HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do the request
        var response = await base.SendAsync(request, cancellationToken);

        // Change the response-side here based on the HttpResponseMessage

        // Return the modified response
        return response;
    }
}
```


<!-- Anchors. -->


<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-windows-store-dotnet-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[4]: https://msdn.microsoft.com/en-us/library/azure/mt419521(v=azure.10).aspx
[5]: https://github.com/Azure-Samples
[6]: http://www.newtonsoft.com/json/help/html/Properties_T_Newtonsoft_Json_JsonPropertyAttribute.htm
[7]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[8]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[9]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/
[10]: http://www.symbolsource.org/
[11]: http://www.symbolsource.org/Public/Wiki/Using
[12]: https://msdn.microsoft.com/en-us/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient(v=azure.10).aspx

<span data-ttu-id="a62e1-470">[앱에 인증 추가]: app-service-mobile-windows-store-dotnet-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="a62e1-470">[Add authentication to your app]: app-service-mobile-windows-store-dotnet-get-started-users.md</span></span>
<span data-ttu-id="a62e1-471">[Azure Mobile Apps에서 오프라인 데이터 동기화]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="a62e1-471">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="a62e1-472">[앱에 푸시 알림 추가]: app-service-mobile-windows-store-dotnet-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="a62e1-472">[Add push notifications to your app]: app-service-mobile-windows-store-dotnet-get-started-push.md</span></span>
<span data-ttu-id="a62e1-473">[Microsoft 계정 로그인을 사용하도록 앱 등록]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="a62e1-473">[Register your app to use a Microsoft account login]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="a62e1-474">[Active Directory 로그온에 앱 서비스를 구성하는 방법]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="a62e1-474">[How to configure App Service for Active Directory login]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>

<!-- Microsoft URLs. -->
<span data-ttu-id="a62e1-475">[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-475">[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-476">[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-476">[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-477">[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-477">[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-478">[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-478">[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-479">[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-479">[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-480">[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-480">[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-481">[형식화되지 않은 테이블에 참조를 만듭니다.]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-481">[creates a reference to an untyped table]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-482">[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-482">[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-483">[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-483">[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-484">[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-484">[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-485">[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-485">[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-486">[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-486">[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-487">[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-487">[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-488">[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-488">[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-489">[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-489">[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-490">[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-490">[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-491">[Take]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-491">[Take]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-492">[Select]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-492">[Select]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-493">[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-493">[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-494">[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-494">[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx</span></span>
<span data-ttu-id="a62e1-495">[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-495">[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-496">[Where]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-496">[Where]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx</span></span>
<span data-ttu-id="a62e1-497">[Azure Portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="a62e1-497">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="a62e1-498">[Azure 클래식 포털]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="a62e1-498">[Azure classic portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="a62e1-499">[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-499">[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx</span></span>
<span data-ttu-id="a62e1-500">[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-500">[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx</span></span>
<span data-ttu-id="a62e1-501">[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-501">[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx</span></span>
<span data-ttu-id="a62e1-502">[Windows 개발자 센터]: https://dev.windows.com/en-us/overview</span><span class="sxs-lookup"><span data-stu-id="a62e1-502">[Windows Dev Center]: https://dev.windows.com/en-us/overview</span></span>
<span data-ttu-id="a62e1-503">[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-503">[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx</span></span>
<span data-ttu-id="a62e1-504">[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-504">[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx</span></span>
<span data-ttu-id="a62e1-505">[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-505">[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx</span></span>
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
<span data-ttu-id="a62e1-506">[Notification Hubs API]: https://msdn.microsoft.com/library/azure/dn495101.aspx</span><span class="sxs-lookup"><span data-stu-id="a62e1-506">[Notification Hubs APIs]: https://msdn.microsoft.com/library/azure/dn495101.aspx</span></span>
<span data-ttu-id="a62e1-507">[Mobile Apps 파일 샘플]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files</span><span class="sxs-lookup"><span data-stu-id="a62e1-507">[Mobile Apps Files Sample]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files</span></span>
<span data-ttu-id="a62e1-508">[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63</span><span class="sxs-lookup"><span data-stu-id="a62e1-508">[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63</span></span>

<!-- External URLs -->
<span data-ttu-id="a62e1-509">[OData v3 설명서]: http://www.odata.org/documentation/odata-version-3-0/</span><span class="sxs-lookup"><span data-stu-id="a62e1-509">[OData v3 Documentation]: http://www.odata.org/documentation/odata-version-3-0/</span></span>
<span data-ttu-id="a62e1-510">[Fiddler]: http://www.telerik.com/fiddler</span><span class="sxs-lookup"><span data-stu-id="a62e1-510">[Fiddler]: http://www.telerik.com/fiddler</span></span>
<span data-ttu-id="a62e1-511">[Json.NET]: http://www.newtonsoft.com/json</span><span class="sxs-lookup"><span data-stu-id="a62e1-511">[Json.NET]: http://www.newtonsoft.com/json</span></span>
<span data-ttu-id="a62e1-512">[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/</span><span class="sxs-lookup"><span data-stu-id="a62e1-512">[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/</span></span>
<span data-ttu-id="a62e1-513">[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments</span><span class="sxs-lookup"><span data-stu-id="a62e1-513">[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments</span></span>
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
