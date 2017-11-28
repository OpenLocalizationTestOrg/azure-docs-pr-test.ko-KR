---
title: "앱 서비스 모바일 앱 hello로 aaaWorking 관리 되는 클라이언트 라이브러리 (Windows | Microsoft Docs"
description: "자세한 내용은 방법 toouse 창 및 Xamarin 앱과 Azure 앱 서비스 모바일 앱 용.NET 클라이언트입니다."
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
ms.openlocfilehash: b056e606b19406398f5b6faabb0931ad651125e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="96978-103">Toouse hello Azure 모바일 앱에 대 한 클라이언트를 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="96978-103">How toouse hello managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="96978-104">개요</span><span class="sxs-lookup"><span data-stu-id="96978-104">Overview</span></span>
<span data-ttu-id="96978-105">이 가이드에서는 tooperform 일반적인 시나리오 hello를 사용 하 여 Azure 앱 서비스 모바일 앱에 대 한 Windows 및 Xamarin 앱 용 클라이언트 라이브러리를 관리 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="96978-105">This guide shows you how tooperform common scenarios using hello managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="96978-106">첫 번째 완료 hello를 고려해 야 새로운 tooMobile 앱 인 경우 [Azure 모바일 앱 빠른 시작] [ 1] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-106">If you are new tooMobile Apps, you should consider first completing hello [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="96978-107">이 가이드에 집중 hello 클라이언트 SDK를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-107">In this guide, we focus on hello client-side managed SDK.</span></span> <span data-ttu-id="96978-108">모바일 앱에 대 한 서버 쪽 Sdk hello, hello에 대 한 hello 설명서를 참조에 대해 더 알아봅니다 toolearn [.NET 서버 SDK] [ 2] 또는 [Node.js 서버 SDK] [ 3].</span><span class="sxs-lookup"><span data-stu-id="96978-108">toolearn more about hello server-side SDKs for Mobile Apps, see hello documentation for hello [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="96978-109">참조 설명서</span><span class="sxs-lookup"><span data-stu-id="96978-109">Reference documentation</span></span>
<span data-ttu-id="96978-110">hello hello 클라이언트 SDK에 대 한 참조 설명서는 여기에서 찾을: [Azure 모바일 앱.NET 클라이언트 참조][4]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-110">hello reference documentation for hello client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="96978-111">Hello에 여러 클라이언트 샘플을 찾을 수도 [Azure 샘플 GitHub 리포지토리][5]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-111">You can also find several client samples in hello [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="96978-112">지원되는 플랫폼</span><span class="sxs-lookup"><span data-stu-id="96978-112">Supported Platforms</span></span>
<span data-ttu-id="96978-113">.NET 플랫폼 hello hello 다음 플랫폼을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-113">hello .NET Platform supports hello following platforms:</span></span>

* <span data-ttu-id="96978-114">API 19-24(Nougat를 통한 KitKat)용 Xamarin Android 릴리스</span><span class="sxs-lookup"><span data-stu-id="96978-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="96978-115">iOS 버전 8.0 이상을 위한 Xamarin iOS 릴리스</span><span class="sxs-lookup"><span data-stu-id="96978-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="96978-116">범용 Windows 플랫폼</span><span class="sxs-lookup"><span data-stu-id="96978-116">Universal Windows Platform</span></span>
* <span data-ttu-id="96978-117">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="96978-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="96978-118">Silverlight 응용 프로그램을 제외한 Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="96978-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="96978-119">hello "서버 흐름" 인증 UI를 표시 하는 hello에 대 한 보기를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-119">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="96978-120">Hello 장치가 수 toopresent WebView UI가 아닌 경우를 다른 인증 방법에는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-120">If hello device is not able toopresent a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="96978-121">따라서 이 SDK는 Watch 유형 또는 그와 비슷하게 제한된 장치에는 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="96978-122"><a name="setup"></a>설정 및 필수 조건</span><span class="sxs-lookup"><span data-stu-id="96978-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="96978-123">하나 이상의 테이블에 포함된 모바일 앱 백 엔드 프로젝트를 이미 만들고 게시했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="96978-124">Hello 테이블의 이름이이 항목에서 사용 하는 hello 코드, `TodoItem` hello 열 뒤에 있고: `Id`, `Text`, 및 `Complete`합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-124">In hello code used in this topic, hello table is named `TodoItem` and it has hello following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="96978-125">이 테이블은 동일한 테이블 완료 하면 만들어집니다 hello는 [Azure 모바일 앱 빠른 시작][1]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-125">This table is hello same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="96978-126">hello 해당 형식화 된 클라이언트 쪽에 있는 C# 형식이 클래스를 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="96978-126">hello corresponding typed client-side type in C# is hello following class:</span></span>

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

<span data-ttu-id="96978-127">hello [JsonPropertyAttribute] [ 6] 는 사용 되는 toodefine hello *PropertyName* hello client 필드와 hello 테이블 필드 간의 매핑입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-127">hello [JsonPropertyAttribute][6] is used toodefine hello *PropertyName* mapping between hello client field and hello table field.</span></span>

<span data-ttu-id="96978-128">toocreate 테이블 모바일 앱 백 엔드에 어떻게 toolearn 참조 hello [.NET 서버 SDK 항목] [ 7] 또는 hello [Node.js 서버 SDK 항목] [ 8] .</span><span class="sxs-lookup"><span data-stu-id="96978-128">toolearn how toocreate tables in your Mobile Apps backend, see hello [.NET Server SDK topic][7] or hello [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="96978-129">모바일 앱 백 엔드를 만든 경우 Azure hello 퀵 스타트 hello 사용 하 여 포털, hello를 사용할 수도 있습니다 **쉽게 테이블** hello 설정을 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-129">If you created your Mobile App backend in hello Azure portal using hello QuickStart, you can also use hello **Easy tables** setting in hello [Azure portal].</span></span>

### <a name="how-to-install-hello-managed-client-sdk-package"></a><span data-ttu-id="96978-130">방법: 설치 hello 클라이언트 SDK 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="96978-130">How to: Install hello managed client SDK package</span></span>
<span data-ttu-id="96978-131">Hello tooinstall hello 메서드를 다음 중 하나를 사용 클라이언트 SDK 패키지에서 모바일 앱에 대 한 관리 되는 [NuGet][9]:</span><span class="sxs-lookup"><span data-stu-id="96978-131">Use one of hello following methods tooinstall hello managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="96978-132">**Visual Studio** 프로젝트를 마우스 오른쪽 단추로 클릭 하 여, **NuGet 패키지 관리**, hello에 대 한 검색 `Microsoft.Azure.Mobile.Client` 패키지 하 고, 한 다음 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="96978-133">**Xamarin Studio** 프로젝트를 마우스 오른쪽 단추로 클릭 하 여, **추가** > **NuGet 패키지 추가**, hello에 대 한 검색 `Microsoft.Azure.Mobile.Client `패키지를 선택한 다음 클릭 **추가 패키지**합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="96978-134">기본 활동 파일에서 기억 tooadd hello 다음 **를 사용 하 여** 문:</span><span class="sxs-lookup"><span data-stu-id="96978-134">In your main activity file, remember tooadd hello following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="96978-135"><a name="symbolsource"></a>방법: Visual Studio에서 디버그 작업</span><span class="sxs-lookup"><span data-stu-id="96978-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="96978-136">hello Microsoft.Azure.Mobile 네임 스페이스에 대 한 hello 기호에서 사용할 수 있는 [SymbolSource][10]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-136">hello symbols for hello Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="96978-137">Toothe 참조 [SymbolSource 지침] [ 11] toointegrate SymbolSource Visual Studio와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-137">Refer toothe [SymbolSource instructions][11] toointegrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="96978-138"><a name="create-client"></a>Hello 모바일 앱 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="96978-138"><a name="create-client"></a>Create hello Mobile Apps client</span></span>
<span data-ttu-id="96978-139">hello 다음 코드에서는 hello [MobileServiceClient] [ 12] 개체를 사용 하는 tooaccess 모바일 앱 백 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-139">hello following code creates hello [MobileServiceClient][12] object that is used tooaccess your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="96978-140">Hello 코드 앞에, 바꿉니다 `MOBILE_APP_URL` hello 모바일 앱 백 엔드의 hello url,에 있는 hello에 모바일 앱 백 엔드에 대 한 블레이드 [Azure 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-140">In hello preceding code, replace `MOBILE_APP_URL` with hello URL of hello Mobile App backend, which is found in the blade for your Mobile App backend in hello [Azure portal].</span></span> <span data-ttu-id="96978-141">hello MobileServiceClient 개체는 단일 항목 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-141">hello MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="96978-142">테이블 작업</span><span class="sxs-lookup"><span data-stu-id="96978-142">Work with Tables</span></span>
<span data-ttu-id="96978-143">다음 섹션 세부 정보를 어떻게 hello toosearch 레코드를 검색 하 고 hello hello 테이블 내에 데이터를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-143">hello following section details how toosearch and retrieve records and modify hello data within hello table.</span></span>  <span data-ttu-id="96978-144">hello 다음 항목에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-144">hello following topics are covered:</span></span>

* [<span data-ttu-id="96978-145">테이블 참조 만들기</span><span class="sxs-lookup"><span data-stu-id="96978-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="96978-146">쿼리 데이터</span><span class="sxs-lookup"><span data-stu-id="96978-146">Query data</span></span>](#querying)
* [<span data-ttu-id="96978-147">반환된 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="96978-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="96978-148">반환된 데이터 정렬</span><span class="sxs-lookup"><span data-stu-id="96978-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="96978-149">페이지에서 데이터 반환</span><span class="sxs-lookup"><span data-stu-id="96978-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="96978-150">특정 열 선택</span><span class="sxs-lookup"><span data-stu-id="96978-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="96978-151">ID로 레코드 조회</span><span class="sxs-lookup"><span data-stu-id="96978-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="96978-152">형식화되지 않은 쿼리 처리</span><span class="sxs-lookup"><span data-stu-id="96978-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="96978-153">데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="96978-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="96978-154">데이터 업데이트</span><span class="sxs-lookup"><span data-stu-id="96978-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="96978-155">데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="96978-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="96978-156">충돌 해결 및 낙관적 동시성</span><span class="sxs-lookup"><span data-stu-id="96978-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="96978-157">바인딩 tooa Windows 사용자 인터페이스</span><span class="sxs-lookup"><span data-stu-id="96978-157">Binding tooa Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="96978-158">Hello 페이지 크기 변경</span><span class="sxs-lookup"><span data-stu-id="96978-158">Changing hello Page Size</span></span>](#pagesize)

### <span data-ttu-id="96978-159"><a name="instantiating"></a>방법: 테이블 참조 만들기</span><span class="sxs-lookup"><span data-stu-id="96978-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="96978-160">Hello에 함수를 호출 하는 백 엔드 테이블의 데이터 액세스 또는 수정 되는 모든 hello 코드가 `MobileServiceTable` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-160">All hello code that accesses or modifies data in a backend table calls functions on hello `MobileServiceTable` object.</span></span> <span data-ttu-id="96978-161">Hello를 호출 하 여 참조 toohello 테이블을 가져올 [GetTable] 다음과 같이 메서드:</span><span class="sxs-lookup"><span data-stu-id="96978-161">Obtain a reference toohello table by calling hello [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="96978-162">hello는 hello 형식의 serialization 모델을 사용 하는 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-162">hello returned object uses hello typed serialization model.</span></span> <span data-ttu-id="96978-163">형식화되지 않은 직렬화 모델도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="96978-164">다음 예제에서는 [참조 tooan 형식화 되지 않은 테이블을 만들고]:</span><span class="sxs-lookup"><span data-stu-id="96978-164">The following example [creates a reference tooan untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="96978-165">형식화 되지 않은 쿼리에 hello 기본 OData 쿼리 문자열을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-165">In untyped queries, you must specify hello underlying OData query string.</span></span>

### <span data-ttu-id="96978-166"><a name="querying"></a>방법: 모바일 앱에서 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="96978-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="96978-167">이 섹션에서는 tooissue hello 다음 기능을 포함 하는 toohello 모바일 앱 백엔드를 쿼리 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-167">This section describes how tooissue queries toohello Mobile App backend, which includes hello following functionality:</span></span>

* [<span data-ttu-id="96978-168">반환된 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="96978-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="96978-169">반환된 데이터 정렬</span><span class="sxs-lookup"><span data-stu-id="96978-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="96978-170">페이지에서 데이터 반환</span><span class="sxs-lookup"><span data-stu-id="96978-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="96978-171">특정 열 선택</span><span class="sxs-lookup"><span data-stu-id="96978-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="96978-172">ID를 기준으로 데이터 조회</span><span class="sxs-lookup"><span data-stu-id="96978-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="96978-173">서버 기반의 페이지 크기는 모든 행 반환 되지 않도록 적용된 tooprevent입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-173">A server-driven page size is enforced tooprevent all rows from being returned.</span></span>  <span data-ttu-id="96978-174">페이징은 hello 서비스에 부정적인 영향을 미치고에서 큰 데이터 집합에 대 한 기본 요청을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-174">Paging keeps default requests for large data sets from negatively impacting hello service.</span></span>  <span data-ttu-id="96978-175">hello를 사용 하 여 50 개 행 보다 tooreturn `Skip` 및 `Take` 메서드를에 설명 된 대로 [데이터 페이지를 반환](#paging)합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-175">tooreturn more than 50 rows, use hello `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="96978-176"><a name="filtering"></a>방법: 반환된 데이터 필터링</span><span class="sxs-lookup"><span data-stu-id="96978-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="96978-177">hello 다음 코드에서는 방법을 포함 하 여 toofilter 데이터는 `Where` 쿼리의 절에에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-177">hello following code illustrates how toofilter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="96978-178">모든 항목 반환 `todoTable` 인 `Complete` 속성은 너무`false`합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-178">It returns all items from `todoTable` whose `Complete` property is equal too`false`.</span></span> <span data-ttu-id="96978-179">hello [여기서] 함수는 행 필터링 hello 테이블에 대 한 hello 쿼리 조건자를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-179">hello [Where] function applies a row filtering predicate to hello query against hello table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="96978-180">메시지 검사 소프트웨어 같은 브라우저 개발자 도구를 사용 하 여 hello hello 보낸 요청 toohello 백 엔드의 URI를 볼 수 있습니다 또는 [Fiddler]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-180">You can view hello URI of hello request sent toohello backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="96978-181">Hello 요청 URI 보면 hello 쿼리 문자열을 수정 하는 사항을 참고 하십시오.</span><span class="sxs-lookup"><span data-stu-id="96978-181">If you look at hello request URI, notice that hello query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="96978-182">이 OData 요청 hello 서버 SDK에서 SQL 쿼리로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-182">This OData request is translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="96978-183">toohello 전달 된 함수는 hello `Where` 메서드는 임의 개수의 조건 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-183">hello function that is passed toohello `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="96978-184">이 예제는 hello 서버 SDK에서 SQL 쿼리도 변환할 수는:</span><span class="sxs-lookup"><span data-stu-id="96978-184">This example would be translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="96978-185">이 쿼리는 여러 절로 분할될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="96978-186">hello 두 메서드가 동일 하며, 같은 의미로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-186">hello two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="96978-187">첫 번째 옵션 hello&mdash;한 쿼리에서 여러 조건자를 연결 하&mdash;보다 간단 하 고 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-187">hello former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="96978-188">hello `Where` 절 수 있는 작업을 지원 hello OData 하위 집합으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-188">hello `Where` clause supports operations that be translated into hello OData subset.</span></span> <span data-ttu-id="96978-189">작업에는 다음 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-189">Operations include:</span></span>

* <span data-ttu-id="96978-190">관계형 연산자(==, !=, <, <=, >, >=),</span><span class="sxs-lookup"><span data-stu-id="96978-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="96978-191">산술 연산자(+, -, /, *, %),</span><span class="sxs-lookup"><span data-stu-id="96978-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="96978-192">숫자 정밀도(Math.Floor, Math.Ceiling),</span><span class="sxs-lookup"><span data-stu-id="96978-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="96978-193">문자열 함수(Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span><span class="sxs-lookup"><span data-stu-id="96978-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="96978-194">날짜 속성(연도, 월, 일, 시, 분, 초),</span><span class="sxs-lookup"><span data-stu-id="96978-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="96978-195">개체의 액세스 속성,</span><span class="sxs-lookup"><span data-stu-id="96978-195">Access properties of an object, and</span></span>
* <span data-ttu-id="96978-196">이러한 연산자를 결합하는 식.</span><span class="sxs-lookup"><span data-stu-id="96978-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="96978-197">무엇을 고려할 때 hello 서버 SDK에서 지 원하는 경우 hello를 고려할 수 있는 [OData v3 설명서]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-197">When considering what hello Server SDK supports, you can consider hello [OData v3 Documentation].</span></span>

### <span data-ttu-id="96978-198"><a name="sorting"></a>방법: 반환된 데이터 정렬</span><span class="sxs-lookup"><span data-stu-id="96978-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="96978-199">hello 다음 코드에서는 방법을 포함 하 여 toosort 데이터는 [OrderBy] 또는 [OrderByDescending] hello 쿼리에서 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-199">hello following code illustrates how toosort data by including an [OrderBy] or [OrderByDescending] function in hello query.</span></span> <span data-ttu-id="96978-200">항목을 반환 `todoTable` hello로 오름차순으로 정렬 `Text` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-200">It returns items from `todoTable` sorted ascending by hello `Text` field.</span></span>

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

### <span data-ttu-id="96978-201"><a name="paging"></a>방법: 페이지에서 데이터 반환</span><span class="sxs-lookup"><span data-stu-id="96978-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="96978-202">기본적으로 hello 백 엔드 첫 50 행만 hello을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-202">By default, hello backend returns only hello first 50 rows.</span></span> <span data-ttu-id="96978-203">Hello를 호출 하 여 반환 된 행의 hello 수를 늘려도 [걸릴] 메서드.</span><span class="sxs-lookup"><span data-stu-id="96978-203">You can increase hello number of returned rows by calling hello [Take] method.</span></span> <span data-ttu-id="96978-204">사용 하 여 `Take` hello 함께 [Skip] 메서드 toorequest 특정 "페이지" hello 전체 데이터 집합의 hello 쿼리에서 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-204">Use `Take` along with hello [Skip] method toorequest a specific "page" of hello total dataset returned by hello query.</span></span> <span data-ttu-id="96978-205">hello 다음 쿼리를 실행 하면 hello 상위 3 개의 항목 반환 hello 표에 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-205">hello following query, when executed, returns hello top three items in hello table.</span></span>

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="96978-206">hello 다음 수정 된 쿼리에서 건너뜁니다 hello 처음 세 결과 및 반환 hello 다음 세 개의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-206">hello following revised query skips hello first three results and returns hello next three results.</span></span> <span data-ttu-id="96978-207">이 쿼리는 hello의 두 번째 "페이지" 여기서 hello 페이지 크기는 세 가지 항목 데이터를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-207">This query produces hello second "page" of data, where hello page size is three items.</span></span>

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="96978-208">hello [IncludeTotalCount] 메서드 요청에 대 한 총 개수 hello *모든* 반환 되는, 지정 된 모든 paging/limit 절을 무시 하는 레코드 hello:</span><span class="sxs-lookup"><span data-stu-id="96978-208">hello [IncludeTotalCount] method requests hello total count for *all* hello records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="96978-209">실제 앱에서 페이지 간에 이동할 수 쿼리 비슷한 toohello 앞에 페이저 컨트롤 또는 UI를 비교할 수 있는 예제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-209">In a real world app, you can use queries similar toohello preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="96978-210">모바일 앱 백 엔드에서 toooverride hello 50 행 제한을 적용 해야 hello [EnableQueryAttribute] toohello 공용 GET 메서드 및 hello 페이징 동작을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-210">toooverride hello 50-row limit in a Mobile App backend, you must also apply hello [EnableQueryAttribute] toohello public GET method and specify hello paging behavior.</span></span> <span data-ttu-id="96978-211">때 적용 된 toohello 메서드를 다음 hello 반환 되는 최대 행 too1000을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-211">When applied toohello method, hello following sets the maximum returned rows too1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="96978-212"><a name="selecting"></a>방법: 특정 열 선택</span><span class="sxs-lookup"><span data-stu-id="96978-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="96978-213">추가 하 여 결과 집합 hello에 tooinclude 속성을 지정할 수는 [선택] 절 tooyour 쿼리 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-213">You can specify which set of properties tooinclude in hello results by adding a [Select] clause tooyour query.</span></span> <span data-ttu-id="96978-214">예를 들어 코드에서 보여 주는 방법을 따르는 hello tooselect 한 필드와도 방법을 tooselect 하 고 여러 필드의 서식을 지정:</span><span class="sxs-lookup"><span data-stu-id="96978-214">For example, hello following code shows how tooselect just one field and also how tooselect and format multiple fields:</span></span>

```
// Select one field -- just hello Text
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

<span data-ttu-id="96978-215">지금까지 설명한 함수 hello 모든 우리 수 유지 체인에 있으므로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-215">All hello functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="96978-216">연결 된 각 호출에 hello 쿼리 중에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="96978-216">Each chained call affects more of hello query.</span></span> <span data-ttu-id="96978-217">한 가지 예를 더 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="96978-218"><a name="lookingup"></a>방법: ID를 기준으로 데이터 조회</span><span class="sxs-lookup"><span data-stu-id="96978-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="96978-219">hello [LookupAsync] 함수는 특정 ID 사용 하 여 hello 데이터베이스에서 개체를 사용 하는 toolook 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-219">hello [LookupAsync] function can be used toolook up objects from hello database with a particular ID.</span></span>

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="96978-220"><a name="untypedqueries"></a>방법: 형식화되지 않은 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="96978-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="96978-221">OData 쿼리 문자열 hello를 호출 하 여 명시적으로 지정 해야 형식화 되지 않은 테이블 개체를 사용 하 여 쿼리를 실행할 때 [ReadAsync]와 같이, 다음 예제는 hello:</span><span class="sxs-lookup"><span data-stu-id="96978-221">When executing a query using an untyped table object, you must explicitly specify hello OData query string by calling [ReadAsync], as in hello following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="96978-222">속성 모음처럼 사용할 수 있는 JSON 값이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="96978-223">JToken 및 Newtonsoft Json.NET에 자세한 내용은 참조 hello [Json.NET] 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-223">For more information on JToken and Newtonsoft Json.NET, see hello [Json.NET] site.</span></span>

### <span data-ttu-id="96978-224"><a name="inserting"></a>방법: 모바일 앱 백 엔드에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="96978-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="96978-225">모든 클라이언트 형식은 **ID**라는 멤버를 포함해야 하며 이는 기본적으로 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="96978-226">이 **Id** CRUD 작업을 수행 하는 데 필요 하 고 오프 라인 동기화. hello 코드 다음에 대해 보여 줍니다 방법을 toouse hello [InsertAsync] 메서드 tooinsert 새 행을 테이블로 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-226">This **Id** is required to perform CRUD operations and for offline sync. hello following code illustrates how toouse hello [InsertAsync] method tooinsert new rows into a table.</span></span> <span data-ttu-id="96978-227">hello 매개 변수는 hello 데이터 toobe.NET 개체로 삽입을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-227">hello parameter contains hello data toobe inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="96978-228">고유한 사용자 지정 ID 값은 hello에 포함 되지 않은 경우 `todoItem` 삽입 시 GUID hello 서버에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-228">If a unique custom ID value is not included in hello `todoItem` during an insert, a GUID is generated by hello server.</span></span>
<span data-ttu-id="96978-229">검색할 수 있습니다 hello hello 호출 반환 후 hello 개체를 검사 하 여 Id를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-229">You can retrieve hello generated Id by inspecting hello object after hello call returns.</span></span>

<span data-ttu-id="96978-230">tooinsert 데이터 형식화 되지 않은, Json.NET 이용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-230">tooinsert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="96978-231">다음은 메일 주소를 고유 문자열 id로 사용하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-231">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="96978-232">ID 값으로 작업</span><span class="sxs-lookup"><span data-stu-id="96978-232">Working with ID values</span></span>
<span data-ttu-id="96978-233">모바일 앱 hello 테이블에 대 한 고유한 사용자 지정 문자열 값을 지원 하며 **id** 열입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-233">Mobile Apps supports unique custom string values for hello table's **id** column.</span></span> <span data-ttu-id="96978-234">문자열 값을 사용 하면 응용 프로그램 toouse hello id 사용자 이름 또는 전자 메일 주소와 같은 사용자 지정 값</span><span class="sxs-lookup"><span data-stu-id="96978-234">A string value allows applications toouse custom values such as email addresses or user names for hello ID.</span></span>  <span data-ttu-id="96978-235">문자열 Id 이점을 다음 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-235">String IDs provide you with hello following benefits:</span></span>

* <span data-ttu-id="96978-236">Id가 왕복 toohello 데이터베이스를 만들지 않고 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-236">IDs are generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="96978-237">레코드는 서로 다른 테이블 또는 데이터베이스에서 보다 쉽게 toomerge 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-237">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="96978-238">응용 프로그램의 논리를 통해 ID 값이 더 효율적으로 통합될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-238">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="96978-239">Hello 모바일 앱 백 엔드 ID에 대 한 고유한 값을 생성 하는 문자열 ID 값을 삽입된 한 레코드에 설정 하지 않으면 때</span><span class="sxs-lookup"><span data-stu-id="96978-239">When a string ID value is not set on an inserted record, hello Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="96978-240">Hello를 사용할 수 있습니다 [Guid.NewGuid] 메서드 toogenerate hello 백 엔드 또는 hello 클라이언트에서 고유한 ID 값입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-240">You can use hello [Guid.NewGuid] method toogenerate your own ID values, either on hello client or in hello backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="96978-241"><a name="modifying"></a>방법: 모바일 앱 백 엔드의 데이터 수정</span><span class="sxs-lookup"><span data-stu-id="96978-241"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="96978-242">hello 다음 코드에서는 어떻게 toouse hello [UpdateAsync] 새 정보로 ID 같습니다 메서드 tooupdate hello로 기존 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-242">hello following code illustrates how toouse hello [UpdateAsync] method tooupdate an existing record with hello same ID with new information.</span></span> <span data-ttu-id="96978-243">hello 매개 변수는 hello 데이터 toobe.NET 개체로 업데이트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-243">hello parameter contains hello data toobe updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="96978-244">이용할 수 있습니다, tooupdate 데이터 형식화 되지 않은 [Json.NET] 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-244">tooupdate untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="96978-245">업데이트할 때 `id` 필드를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-245">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="96978-246">hello 백 엔드에서 사용 hello `id` 필드 tooidentify tooupdate 행입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-246">hello backend uses hello `id` field tooidentify which row tooupdate.</span></span> <span data-ttu-id="96978-247">hello `id` hello의 hello 결과에서 필드를 가져올 수 있습니다 `InsertAsync` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-247">hello `id` field can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="96978-248">`ArgumentException` hello를 제공 하지 않고 tooupdate 항목을 시도 하면 발생 `id` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-248">An `ArgumentException` is raised if you try tooupdate an item without providing hello `id` value.</span></span>

### <span data-ttu-id="96978-249"><a name="deleting"></a>방법: 모바일 앱 백 엔드의 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="96978-249"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="96978-250">hello 다음 코드에서는 어떻게 toouse hello [DeleteAsync] 메서드 toodelete 기존 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="96978-250">hello following code illustrates how toouse hello [DeleteAsync] method toodelete an existing instance.</span></span> <span data-ttu-id="96978-251">hello 인스턴스 hello로 식별 됩니다 `id` hello에 설정 된 필드 `todoItem`합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-251">hello instance is identified by hello `id` field set on hello `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="96978-252">toodelete 데이터 형식화 되지 않은 다음과 같이 Json.NET의 이점은 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-252">toodelete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="96978-253">삭제를 요청할 때 ID를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-253">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="96978-254">다른 속성 toohello 서비스가 전달 되지 않은 또는 hello 서비스에서 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-254">Other properties are not passed toohello service or are ignored at hello service.</span></span> <span data-ttu-id="96978-255">hello의 결과 `DeleteAsync` 호출은 일반적으로 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-255">hello result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="96978-256">hello ID toopass hello의 hello 결과에서 얻을 수 있습니다 `InsertAsync` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-256">hello ID toopass in can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="96978-257">A `MobileServiceInvalidOperationException` hello를 지정 하지 않고 항목 toodelete 려 할 때 throw 되 `id` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-257">A `MobileServiceInvalidOperationException` is thrown when you try toodelete an item without specifying hello `id` field.</span></span>

### <span data-ttu-id="96978-258"><a name="optimisticconcurrency"></a>방법: 충돌 해결에 낙관적 동시성 사용</span><span class="sxs-lookup"><span data-stu-id="96978-258"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="96978-259">둘 이상의 클라이언트가 작성할 수 변경 toohello 동일 항목 hello에서 동일한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-259">Two or more clients may write changes toohello same item at hello same time.</span></span> <span data-ttu-id="96978-260">충돌 감지 하지 않고 hello 마지막 쓰기가 이전의 업데이트 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="96978-260">Without conflict detection, hello last write would overwrite any previous updates.</span></span> <span data-ttu-id="96978-261">**낙관적 동시성 제어** 에서는 각 트랜잭션이 커밋할 수 있으므로 리소스 잠금을 사용하지 않는다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-261">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="96978-262">트랜잭션을 커밋하기 전에 낙관적 동시성 제어는 다른 트랜잭션이 없어야 hello 데이터 수정 않았는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-262">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified hello data.</span></span> <span data-ttu-id="96978-263">Hello 데이터가 수정 된 트랜잭션 커밋은 hello가 롤백됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-263">If hello data has been modified, hello committing transaction is rolled back.</span></span>

<span data-ttu-id="96978-264">모바일 앱 hello를 사용 하 여 변경 내용을 tooeach 항목을 추적 하 여 낙관적 동시성 제어를 지 원하는 `version` 모바일 앱 백 엔드의 각 테이블에 대해 정의 된 시스템 속성 열입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-264">Mobile Apps supports optimistic concurrency control by tracking changes tooeach item using hello `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="96978-265">기록이 업데이트 될 때마다 모바일 앱 설정 hello `version` 속성에 대 한 tooa 새 값을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-265">Each time a record is updated, Mobile Apps sets hello `version` property for that record tooa new value.</span></span> <span data-ttu-id="96978-266">각 업데이트 요청을 하는 동안 hello `version` hello 요청에 포함 된 hello 레코드의 속성은 비교 toohello hello 서버의 hello 레코드에 대 한 동일한 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-266">During each update request, hello `version` property of hello record included with hello request is compared toohello same property for hello record on hello server.</span></span> <span data-ttu-id="96978-267">버전은 전달 된 hello 요청 hello 백 엔드에 맞지 않는 경우 hello 클라이언트 라이브러리를 발생 시킵니다는 `MobileServicePreconditionFailedException<T>` 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-267">If the version passed with hello request does not match hello backend, then hello client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="96978-268">hello hello 예외에 포함 된 형식은 hello 백 엔드 포함 hello 서버 버전의 hello 레코드 hello 레코드 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-268">hello type included with hello exception is hello record from hello backend containing hello servers version of hello record.</span></span> <span data-ttu-id="96978-269">hello 응용 프로그램을 유도할 수 있습니다이 정보 toodecide 여부 올바른 hello 사용 하 여 다시 tooexecute hello 업데이트 요청 `version` hello 백 엔드 toocommit 변경 된 내용에서 값입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-269">hello application can then use this information toodecide whether tooexecute hello update request again with hello correct `version` value from hello backend toocommit changes.</span></span>

<span data-ttu-id="96978-270">Hello 테이블 클래스 hello에 대 한 열을 정의 `version` 시스템 속성 tooenable 낙관적 동시성 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-270">Define a column on hello table class for hello `version` system property tooenable optimistic concurrency.</span></span> <span data-ttu-id="96978-271">예:</span><span class="sxs-lookup"><span data-stu-id="96978-271">For example:</span></span>

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

<span data-ttu-id="96978-272">형식화 되지 않은 테이블을 사용 하는 응용 프로그램 hello 설정 하 여 낙관적 동시성을 사용 `Version` 에 플래그는 `SystemProperties` hello의 테이블 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-272">Applications using untyped tables enable optimistic concurrency by setting hello `Version` flag on the `SystemProperties` of hello table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="96978-273">또한 tooenabling 낙관적 동시성도 hello를 catch 해야 `MobileServicePreconditionFailedException<T>` 를 호출할 때 코드에서 예외 [UpdateAsync]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-273">In addition tooenabling optimistic concurrency, you must also catch hello `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="96978-274">올바른 hello를 적용 하 여 hello 충돌을 해결 `version` toothe 업데이트 레코드 및 호출 [UpdateAsync] hello로 레코드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-274">Resolve hello conflict by applying hello correct `version` toothe updated record and call [UpdateAsync] with hello resolved record.</span></span> <span data-ttu-id="96978-275">코드 다음 hello tooresolve 쓰기 충돌이 한 번만 검색 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="96978-275">hello following code shows how tooresolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at hello remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, hello item has changed since hello last query
        // Resolve hello conflict between hello local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user toochoose hello resoltion between versions
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
        // tooresolve hello conflict, update hello version of hello item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while hello user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="96978-276">자세한 내용은 참조 hello [Azure 모바일 앱에서 데이터 동기화 오프 라인] 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-276">For more information, see hello [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="96978-277"><a name="binding"></a>방법: Bind 모바일 앱 데이터 tooa Windows 사용자 인터페이스</span><span class="sxs-lookup"><span data-stu-id="96978-277"><a name="binding"></a>How to: Bind Mobile Apps data tooa Windows user interface</span></span>
<span data-ttu-id="96978-278">이 섹션에서는 toodisplay Windows 앱에서 UI 요소를 사용 하 여 데이터 개체를 반환 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="96978-278">This section shows how toodisplay returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="96978-279">다음 예제 코드의 불완전 한 항목에 대 한 쿼리를 사용 하 여 hello 목록 toohello 소스에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-279">The following example code binds toohello source of hello list with a query for incomplete items.</span></span> <span data-ttu-id="96978-280">[MobileServiceCollection]은 Mobile Apps 인식 바인딩 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="96978-280">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound tooa UI list control
IEnumerable itemsControl  = items;

// Bind this tooa ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="96978-281">일부 컨트롤 hello에 관리 인터페이스를 호출 하는 런타임 지원이 [ISupportIncrementalLoading]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-281">Some controls in hello managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="96978-282">이 인터페이스에서는 컨트롤 toorequest hello 사용자가를 스크롤할 때 추가 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-282">This interface allows controls toorequest extra data when hello user scrolls.</span></span> <span data-ttu-id="96978-283">이 인터페이스에 대 한 유니버설 Windows 앱을 통해 기본적으로 지원 [MobileServiceIncrementalLoadingCollection], hello 컨트롤에서 호출 하 여 자동으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-283">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from hello controls.</span></span> <span data-ttu-id="96978-284">다음과 같이 Windows 앱에서 `MobileServiceIncrementalLoadingCollection` 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-284">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="96978-285">toouse hello "Silverlight" 및 Windows Phone 8 앱을 사용 하 여 hello에서 새 컬렉션 `ToCollection` 에 확장 메서드 `IMobileServiceTableQuery<T>` 및 `IMobileServiceTable<T>`합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-285">toouse hello new collection on Windows Phone 8 and "Silverlight" apps, use hello `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="96978-286">tooload 데이터 호출 `LoadMoreItemsAsync()`합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-286">tooload data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="96978-287">호출 하 여 만든 hello 컬렉션을 사용 하면 `ToCollectionAsync` 또는 `ToCollection`, 바인딩된 tooUI 컨트롤로 사용할 수 있는 컬렉션을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="96978-287">When you use hello collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound tooUI controls.</span></span>  <span data-ttu-id="96978-288">이 컬렉션은 페이징을 인식합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-288">This collection is paging-aware.</span></span>  <span data-ttu-id="96978-289">Hello 컬렉션이 네트워크에서 데이터를 로드, 하므로 경우에 따라 로드 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-289">Since hello collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="96978-290">toohandle hello를 재정의 하는 이러한 오류 `OnException` 메서드를 `MobileServiceIncrementalLoadingCollection` 너무 호출에서 발생 한 예외 toohandle`LoadMoreItemsAsync`합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-290">toohandle such failures, override hello `OnException` method on `MobileServiceIncrementalLoadingCollection` toohandle exceptions resulting from calls too`LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="96978-291">테이블에 여러 필드가 있지만 toodisplay 알아보려는 경우 고려 컨트롤에서 그 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-291">Consider if your table has many fields but you only want toodisplay some of them in your control.</span></span> <span data-ttu-id="96978-292">Hello 앞 섹션에서에서 hello 지침을 사용할 수 있습니다 "[특정 열을 선택](#selecting)" hello UI에서에서 특정 열 toodisplay tooselect 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-292">You may use hello guidance in hello preceding section "[Select specific columns](#selecting)" tooselect specific columns toodisplay in hello UI.</span></span>

### <span data-ttu-id="96978-293"><a name="pagesize"></a>페이지 크기 변경 hello</span><span class="sxs-lookup"><span data-stu-id="96978-293"><a name="pagesize"></a>Change hello Page size</span></span>
<span data-ttu-id="96978-294">Azure Mobile Apps는 기본적으로 요청당 최대 50개의 항목을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-294">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="96978-295">Hello 클라이언트와 서버 모두에서 hello 최대 페이지 크기를 늘려 hello 페이징 크기를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-295">You can change hello paging size by increasing hello maximum page size on both hello client and server.</span></span>  <span data-ttu-id="96978-296">tooincrease hello 요청 된 페이지 크기를 지정 `PullOptions` 사용 하는 경우 `PullAsync()`:</span><span class="sxs-lookup"><span data-stu-id="96978-296">tooincrease hello requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="96978-297">Hello 사항을 가정 `PageSize` hello 서버 내에서 100 보다 큰 같은 tooor 요청 최대 100 개의 항목을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-297">Assuming you have made hello `PageSize` equal tooor greater than 100 within hello server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="96978-298"><a name="#offlinesync"></a>오프라인 데이터 작업</span><span class="sxs-lookup"><span data-stu-id="96978-298"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="96978-299">오프 라인 테이블 오프 라인일 때 사용 하기 위해 로컬 SQLite 저장소 toostore 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-299">Offline tables use a local SQLite store toostore data for use when offline.</span></span>  <span data-ttu-id="96978-300">Hello에 대 한 작업은 수행 하는 테이블의 모든 로컬 SQLite hello 원격 서버 저장소 대신 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-300">All table operations are done against hello local SQLite store instead of hello remote server store.</span></span>  <span data-ttu-id="96978-301">toocreate를 오프 라인 테이블에는 먼저 프로젝트를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-301">toocreate an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="96978-302">Visual Studio에서 hello 솔루션 탐색기에서 > **솔루션에 대 한 NuGet 패키지 관리...** 다음 검색 하 고 설치는 **Microsoft.Azure.Mobile.Client.SQLiteStore** hello 솔루션의 모든 프로젝트에 대 한 NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-302">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="96978-303">(선택 사항) toosupport Windows 장치 hello SQLite 런타임 패키지를 다음 중 하나를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-303">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="96978-304">**Windows 8.1 런타임:** [Windows 8.1][3]용 SQLite를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-304">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="96978-305">**Windows Phone 8.1:** [Windows Phone 8.1][4]용 SQLite를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-305">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="96978-306">**유니버설 Windows 플랫폼** 설치 [유니버설 Windows hello에 대 한 SQLite][5]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-306">**Universal Windows Platform** Install [SQLite for hello Universal Windows][5].</span></span>
3. <span data-ttu-id="96978-307">(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="96978-307">(Optional).</span></span> <span data-ttu-id="96978-308">Windows 장치에 대 한 클릭 **참조** > **참조 추가...** , hello 확장 **Windows** 폴더 > **확장**, 적절 한 hello를 사용 하도록 설정 하면 **Windows 용 SQLite** hello 함께SDK **Windows 용 visual c + + 2013 런타임** SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-308">For Windows devices, click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**, then enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="96978-309">hello SQLite SDK 이름은 조금씩 각 Windows 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-309">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="96978-310">테이블 참조를 만들 수 있습니다, 전에 hello 로컬 저장소를 준비 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-310">Before a table reference can be created, hello local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="96978-311">저장소 초기화 hello 클라이언트를 만든 직후에 일반적으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-311">Store initialization is normally done immediately after hello client is created.</span></span>  <span data-ttu-id="96978-312">hello **OfflineDbPath** 지 원하는 모든 플랫폼에서 사용 하기에 적합 한 파일 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-312">hello **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="96978-313">Hello 경로 정규화 된 경로 이면 (즉,이 메서드는 먼저 슬래시), 아니면 해당 경로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-313">If hello path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="96978-314">Hello 경로 정규화 되지 않은 경우 hello 파일이 플랫폼 관련 위치에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-314">If hello path is not fully qualified, hello file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="96978-315">IOS 및 Android 장치에 대 한 hello 기본 경로 hello "개인 Files" 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-315">For iOS and Android devices, hello default path is hello "Personal Files" folder.</span></span>
* <span data-ttu-id="96978-316">Windows 장치에 대 한 hello 기본 경로 hello 응용 프로그램별 "AppData" 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-316">For Windows devices, hello default path is hello application-specific "AppData" folder.</span></span>

<span data-ttu-id="96978-317">Hello를 사용 하 여 테이블 참조를 가져올 수 있습니다 `GetSyncTable<>` 메서드:</span><span class="sxs-lookup"><span data-stu-id="96978-317">A table reference can be obtained using hello `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="96978-318">오프 라인 테이블 tooauthenticate toouse가 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-318">You do not need tooauthenticate toouse an offline table.</span></span>  <span data-ttu-id="96978-319">Hello 백 엔드 서비스와 통신 하는 경우에 tooauthenticate가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-319">You only need tooauthenticate when you are communicating with hello backend service.</span></span>

### <span data-ttu-id="96978-320"><a name="syncoffline"></a>오프라인 테이블 동기화</span><span class="sxs-lookup"><span data-stu-id="96978-320"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="96978-321">기본적으로 오프 라인 테이블 hello 백 엔드와 동기화 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-321">Offline tables are not synchronized with hello backend by default.</span></span>  <span data-ttu-id="96978-322">동기화는 두 부분으로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-322">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="96978-323">새 항목 다운로드에서 별도로 변경 내용을 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-323">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="96978-324">다음은 일반적인 동기화 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-324">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //hello first parameter is a query name that is used internally by hello client SDK tooimplement incremental sync.
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

    // Simple error/conflict handling. A real application would handle hello various errors like network conditions,
    // server conflicts and others via hello IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting tooserver's copy.
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

<span data-ttu-id="96978-325">하는 경우 첫 번째 인수를 너무 hello`PullAsync` 매개 변수가 null 이면 증분 동기화가 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-325">If hello first argument too`PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="96978-326">각 동기화 작업은 모든 레코드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="96978-326">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="96978-327">hello SDK 수행 암시적 `PushAsync()` 레코드를 끌어오려면 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-327">hello SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="96978-328">`PullAsync()` 메서드에서 충돌 처리가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-328">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="96978-329">처리할 수 있는 충돌을 방지 hello와 동일한 방법으로 온라인 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-329">You can deal with conflicts in hello same way as online tables.</span></span>  <span data-ttu-id="96978-330">hello 충돌 생성 되는 경우 `PullAsync()` 대신 hello 삽입, 업데이트 또는 삭제 하는 동안 호출 되어 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-330">hello conflict is produced when `PullAsync()` is called instead of during hello insert, update, or delete.</span></span> <span data-ttu-id="96978-331">여러 충돌이 발생하는 경우 단일 MobileServicePushFailedException에 함께 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-331">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="96978-332">각 오류를 개별적으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-332">Handle each failure separately.</span></span>

## <span data-ttu-id="96978-333"><a name="#customapi"></a>사용자 지정 API 작업</span><span class="sxs-lookup"><span data-stu-id="96978-333"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="96978-334">사용자 지정 API toodefine 사용자 지정 끝점을 서버 기능을 노출 하는 또는 하지 않는 매핑할 tooan 삽입, 업데이트, 삭제, 읽기 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-334">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="96978-335">사용자 지정 API를 사용하면 HTTP 메시지 헤더 읽기와 설정 및 JSON 이외의 메시지 본문 형식 정의를 비롯하여 더 효율적으로 메시징을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-335">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="96978-336">Hello 중 하나를 호출 하 여 사용자 지정 API 호출 [InvokeApiAsync] hello 클라이언트에 대 한 메서드.</span><span class="sxs-lookup"><span data-stu-id="96978-336">You call a custom API by calling one of hello [InvokeApiAsync] methods on hello client.</span></span> <span data-ttu-id="96978-337">예를 들어 다음 코드 줄을 hello 보냅니다 POST 요청 toohello **completeAll** hello 백 엔드에 API:</span><span class="sxs-lookup"><span data-stu-id="96978-337">For example, hello following line of code sends a POST request toohello **completeAll** API on hello backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="96978-338">이 폼은 형식화 된 메서드 호출 하며 해당 hello **MarkAllResult** 형식이 정의 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-338">This form is a typed method call and requires that hello **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="96978-339">형식화된 메서드와 형식화되지 않은 메서드가 모두 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-339">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="96978-340">hello InvokeApiAsync() 메서드 앞에 추가 한다고 toocall API hello로 시작 하지 않는 한 ' / api/toohello API는 '/'입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-340">hello InvokeApiAsync() method prepends '/api/' toohello API that you wish toocall unless hello API starts with a '/'.</span></span>
<span data-ttu-id="96978-341">예:</span><span class="sxs-lookup"><span data-stu-id="96978-341">For example:</span></span>

* <span data-ttu-id="96978-342">`InvokeApiAsync("completeAll",...)`hello 백 엔드에 /api/completeAll을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-342">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on hello backend</span></span>
* <span data-ttu-id="96978-343">`InvokeApiAsync("/.auth/me",...)`hello 백 엔드에 /.auth/me를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-343">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on hello backend</span></span>

<span data-ttu-id="96978-344">Azure 모바일 앱으로 정의 되어 있지 않은 해당 WebAPIs를 포함 하 여 모든 WebAPI InvokeApiAsync toocall를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-344">You can use InvokeApiAsync toocall any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="96978-345">InvokeApiAsync()를 사용 하는 경우 인증 헤더를 포함 하 여 hello 적절 한 헤더 hello 요청과 함께 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-345">When you use InvokeApiAsync(), hello appropriate headers, including authentication headers, are sent with hello request.</span></span>

## <span data-ttu-id="96978-346"><a name="authentication"></a>사용자 인증</span><span class="sxs-lookup"><span data-stu-id="96978-346"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="96978-347">Mobile Apps는 Facebook, Google, Microsoft 계정, Twitter 및 Azure Active Directory와 같이 다양한 외부 ID 공급자를 사용하여 앱 사용자의 인증 및 권한 부여를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-347">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="96978-348">권한을 설정할 수 있습니다에 특정 작업에 대 한 테이블 toorestrict 액세스 tooonly 인증 된 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-348">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="96978-349">서버 스크립트에 인증 된 사용자 tooimplement 권한 부여 규칙의 hello id를도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-349">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="96978-350">자세한 내용은 hello 자습서를 참조 하십시오. [추가 인증 tooyour 앱]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-350">For more information, see hello tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="96978-351">두 가지의 인증 흐름이 지원 됩니다: *클라이언트 관리* 및 *서버 관리* 흐름입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-351">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="96978-352">hello 서버 관리 흐름 hello 공급자의 웹 인증 인터페이스를 사용 hello 가장 간단한 인증 경험을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-352">hello server-managed flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="96978-353">더 구체적인 통합 장치 관련 기능을 공급자 특정 장치 관련 Sdk를 사용 hello 클라이언트에서 관리 하는 흐름 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-353">hello client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="96978-354">프로덕션 앱에서 클라이언트 관리 흐름을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-354">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="96978-355">인증을 tooset, 하나 이상의 id 공급자와 앱을 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-355">tooset up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="96978-356">hello id 공급자는 클라이언트 ID 및 앱에 대 한 클라이언트 암호를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-356">hello identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="96978-357">이러한 값은 프로그램 백 엔드 tooenable Azure 앱 서비스 인증/권한 부여에에서 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-357">These values are then set in your backend tooenable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="96978-358">자세한 내용은 hello 자습서에서 필요한 세부 정보 [추가 인증 tooyour 앱]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-358">For more information, follow hello detailed instructions in the tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="96978-359">이 섹션의 hello 다음 항목을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="96978-359">hello following topics are covered in this section:</span></span>

* [<span data-ttu-id="96978-360">클라이언트 관리 인증</span><span class="sxs-lookup"><span data-stu-id="96978-360">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="96978-361">서버 관리 인증</span><span class="sxs-lookup"><span data-stu-id="96978-361">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="96978-362">캐싱 hello 인증 토큰</span><span class="sxs-lookup"><span data-stu-id="96978-362">Caching hello authentication token</span></span>](#caching)

### <span data-ttu-id="96978-363"><a name="clientflow"></a>클라이언트 관리 인증</span><span class="sxs-lookup"><span data-stu-id="96978-363"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="96978-364">앱은 hello id 공급자를 독립적으로 문의 하 고 백 엔드를 로그인 하는 동안 hello 반환 된 토큰을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-364">Your app can independently contact hello identity provider and then provide hello returned token during login with your backend.</span></span> <span data-ttu-id="96978-365">이 클라이언트 흐름 tooprovide를 사용자나 hello id 공급자 로부터 tooretrieve 추가 사용자 데이터에 대 한 single sign on 환경이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-365">This client flow enables you tooprovide a single sign-on experience for users or tooretrieve additional user data from hello identity provider.</span></span> <span data-ttu-id="96978-366">클라이언트 흐름 인증은 기본 toousing 서버 흐름 hello id 공급자 SDK 원래의 UX 느낌을 제공 하 고 추가 사용자 지정을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-366">Client flow authentication is preferred toousing a server flow as hello identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="96978-367">클라이언트 흐름 인증 패턴을 따른 hello에 대 한 예제가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-367">Examples are provided for hello following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="96978-368">Active Directory 인증 라이브러리</span><span class="sxs-lookup"><span data-stu-id="96978-368">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="96978-369">Facebook 또는 Google</span><span class="sxs-lookup"><span data-stu-id="96978-369">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="96978-370">Live SDK</span><span class="sxs-lookup"><span data-stu-id="96978-370">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="96978-371"><a name="adal"></a>Active Directory 인증 라이브러리 hello로 사용자를 인증</span><span class="sxs-lookup"><span data-stu-id="96978-371"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="96978-372">Azure Active Directory 인증을 사용 하 여 hello 클라이언트로부터 hello Active Directory 인증 라이브러리 (ADAL) tooinitiate 사용자 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-372">You can use hello Active Directory Authentication Library (ADAL) tooinitiate user authentication from hello client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="96978-373">다음 hello 하 여 AAD 로그온에 대 한 모바일 앱 백 엔드 구성 [tooconfigure Active Directory 로그인에 대 한 서비스 응용 프로그램 방법] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-373">Configure your mobile app backend for AAD sign-on by following hello [How tooconfigure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="96978-374">네이티브 클라이언트 응용 프로그램 등록 되었는지 toocomplete hello 선택적 단계를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-374">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="96978-375">Visual Studio 또는 Xamarin Studio에서 프로젝트를 열고 추가 참조 toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-375">In Visual Studio or Xamarin Studio, open your project and add a reference toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="96978-376">검색할 때 시험판 버전을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-376">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="96978-377">다음 코드 tooyour 응용 프로그램, 사용 중인 toohello 플랫폼에 따라 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-377">Add hello following code tooyour application, according toohello platform you are using.</span></span> <span data-ttu-id="96978-378">, 각 교체를 수행 하는 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-378">In each, make hello following replacements:</span></span>

   * <span data-ttu-id="96978-379">대체 **INSERT-기관-여기** hello 테 넌 트 응용 프로그램을 프로 비전 하는 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-379">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="96978-380">형식은 https://login.microsoftonline.com/contoso.onmicrosoft.com이어야 합니다. Hello에 Azure Active Directory에서 hello 도메인 탭에서이 값을 복사할 수 있습니다 [Azure 클래식 포털]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-380">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="96978-381">대체 **리소스 ID 여기 삽입** 모바일 앱 백 엔드에 대 한 hello 클라이언트 ID로 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-381">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="96978-382">Hello에서 hello 클라이언트 ID를 가져올 수 **고급** 탭의 **Azure Active Directory 설정** hello 포털에서입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-382">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="96978-383">대체 **클라이언트 ID 여기 삽입** hello 네이티브 클라이언트 응용 프로그램에서 복사한 hello 클라이언트 ID로 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-383">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="96978-384">대체 **리디렉션 URI 여기 삽입** 웹 사이트와 */.auth/login/done* hello HTTPS 체계를 사용 하 여 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-384">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="96978-385">이 값은 형태가 됩니다 너무*https://contoso.azurewebsites.net/.auth/login/done*합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-385">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="96978-386">각 플랫폼에 대해 필요한 hello 코드가 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-386">hello code needed for each platform follows:</span></span>

     <span data-ttu-id="96978-387">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="96978-387">**Windows:**</span></span>

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

     <span data-ttu-id="96978-388">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="96978-388">**Xamarin.iOS**</span></span>

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

     <span data-ttu-id="96978-389">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="96978-389">**Xamarin.Android**</span></span>

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

#### <span data-ttu-id="96978-390"><a name="client-facebook"></a>Facebook 또는 Google의 토큰을 사용하는 Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="96978-390"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="96978-391">Facebook 또는 Google에 대 한이 코드 조각에 나와 있는 것 처럼 hello 클라이언트 흐름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-391">You can use hello client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using hello Facebook or Google SDK.
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
            // tooMobileServiceAuthenticationProvider.Google if using Google auth.
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

#### <span data-ttu-id="96978-392"><a name="client-livesdk"></a>Single Sign On와 Microsoft 계정을 사용 하 여 hello 라이브 SDK</span><span class="sxs-lookup"><span data-stu-id="96978-392"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with hello Live SDK</span></span>
<span data-ttu-id="96978-393">tooauthenticate 사용자 hello Microsoft 계정 개발자 센터에서 앱을 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-393">tooauthenticate users, you must register your app at hello Microsoft account Developer Center.</span></span> <span data-ttu-id="96978-394">모바일 앱 백 엔드의 등록 세부 정보를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-394">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="96978-395">단계를 완료 하는 hello toocreate Microsoft 계정 등록 및 tooyour 모바일 앱 백 엔드에서 연결, [등록 하면 앱 toouse Microsoft 계정 로그인]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-395">toocreate a Microsoft account registration and connect it tooyour Mobile App backend, complete hello steps in [Register your app toouse a Microsoft account login].</span></span> <span data-ttu-id="96978-396">Windows 스토어 및 Windows Phone 8/Silverlight 버전 모두 응용 프로그램의 경우 hello Windows 스토어 버전을 먼저 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-396">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register hello Windows Store version first.</span></span>

<span data-ttu-id="96978-397">hello 다음 코드 라이브 SDK를 사용 하 여 인증 사용 하 여 hello tooyour 모바일 앱 백 엔드에서 toosign 토큰을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-397">hello following code authenticates using Live SDK and uses hello returned token toosign in tooyour Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get hello URL hello Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create hello authentication client for Windows Store using hello service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create hello authentication client for Windows Phone using hello client ID of hello registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request hello authentication token from hello Live authentication service.
        // hello wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about hello logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use hello Microsoft account auth token toosign in tooApp Service.
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

<span data-ttu-id="96978-398">자세한 내용은 참조 hello [Windows Live SDK] 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-398">For more information, see hello [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="96978-399"><a name="serverflow"></a>서버 관리 인증</span><span class="sxs-lookup"><span data-stu-id="96978-399"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="96978-400">Id 공급자를 등록 하면 호출 hello [LoginAsync] 메서드 [MobileServiceClient] hello로 hello [MobileServiceAuthenticationProvider] 공급자의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-400">Once you have registered your identity provider, call hello [LoginAsync] method on hello [MobileServiceClient] with hello [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="96978-401">예를 들어 hello 다음 코드 시작 한 서버 흐름 로그인에서 Facebook을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-401">For example, hello following code initiates a server flow sign-in by using Facebook.</span></span>

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

<span data-ttu-id="96978-402">Facebook 이외의 id 공급자를 사용 하는 경우의 hello 값 변경 [MobileServiceAuthenticationProvider] toohello 값 공급자입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-402">If you are using an identity provider other than Facebook, change hello value of [MobileServiceAuthenticationProvider] toohello value for your provider.</span></span>

<span data-ttu-id="96978-403">서버 흐름 Azure 앱 서비스는 hello 선택한 공급자의 hello 로그인 페이지를 표시 하 여 hello OAuth 인증 흐름을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-403">In a server flow, Azure App Service manages hello OAuth authentication flow by displaying hello sign-in page of hello selected provider.</span></span>  <span data-ttu-id="96978-404">한 번 hello identity provider 반환, Azure 앱 서비스 앱 서비스 인증 토큰을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-404">Once hello identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="96978-405">hello [LoginAsync] 메서드가 반환 되는 [MobileServiceUser], 모두 hello를 제공 하는 [UserId] hello 인증 사용자 및 hello [ MobileServiceAuthenticationToken], JSON 웹 토큰 (JWT).</span><span class="sxs-lookup"><span data-stu-id="96978-405">hello [LoginAsync] method returns a [MobileServiceUser], which provides both hello [UserId] of hello authenticated user and hello [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="96978-406">이 토큰은 캐시했다가 만료될 때까지 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-406">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="96978-407">자세한 내용은 참조 [캐싱 hello 인증 토큰](#caching)합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-407">For more information, see [Caching hello authentication token](#caching).</span></span>

### <span data-ttu-id="96978-408"><a name="caching"></a>캐싱 hello 인증 토큰</span><span class="sxs-lookup"><span data-stu-id="96978-408"><a name="caching"></a>Caching hello authentication token</span></span>
<span data-ttu-id="96978-409">경우에 따라 hello 공급자 로부터 hello 인증 토큰을 저장 하 여 hello 통화 toohello 로그인 방법 hello 첫 번째 인증을 거친 후 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-409">In some cases, hello call toohello login method can be avoided after hello first successful authentication by storing hello authentication token from hello provider.</span></span>  <span data-ttu-id="96978-410">Windows 스토어 및 UWP 앱 צ ְ ײ [PasswordVault] toocache 현재 인증 토큰을 성공적으로 로그인 한 후 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-410">Windows Store and UWP apps can use [PasswordVault] toocache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="96978-411">사용자 Id 값 hello hello hello 자격 증명의 사용자 이름으로 저장 됩니다 및 hello 토큰은 hello 암호 hello로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-411">hello UserId value is stored as hello UserName of hello credential and hello token is hello stored as hello Password.</span></span> <span data-ttu-id="96978-412">후속 업체 hello 확인할 수 있습니다 **PasswordVault** 캐시 된 자격 증명에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-412">On subsequent start-ups, you can check hello **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="96978-413">hello 다음 예제에서는 캐시 된 자격 증명은 검색 되 고 그렇지 않으면 tooauthenticate hello 백 엔드를 사용 하 여 다시 시도 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="96978-413">hello following example uses cached credentials when they are found, and otherwise attempts tooauthenticate again with hello backend:</span></span>

```
// Try tooretrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create hello current user from hello stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache hello token as shown above.
}
```

<span data-ttu-id="96978-414">로그 아웃 하면 사용자를 제거 해야 hello 저장 된 자격 증명 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-414">When you sign out a user, you must also remove hello stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="96978-415">Xamarin 앱 hello를 사용 하 여 [Xamarin.Auth] Api toosecurely 저장 자격 증명에는 **계정** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="96978-415">Xamarin    apps use hello [Xamarin.Auth] APIs toosecurely store credentials in an **Account** object.</span></span> <span data-ttu-id="96978-416">이러한 Api를 사용 하는 예제를 참조 hello [AuthStore.cs] hello에서 코드 파일 [ContosoMoments 사진 샘플 공유](https://github.com/azure-appservice-samples/ContosoMoments)합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-416">For an example of using these APIs, see hello [AuthStore.cs] code file in hello [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="96978-417">클라이언트에서 관리 하는 인증을 사용 하면 Facebook 또는 Twitter와 같은 공급자 로부터 얻은 hello 액세스 토큰을 캐시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-417">When you use client-managed authentication, you can also cache hello access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="96978-418">이 토큰은 제공 된 toorequest hello 백 엔드에 있는 새 인증 토큰을 다음과 같이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-418">This token can be supplied toorequest a new authentication token from hello backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="96978-419"><a name="pushnotifications"></a>푸시 알림</span><span class="sxs-lookup"><span data-stu-id="96978-419"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="96978-420">hello 다음 항목을 설명 푸시 알림:</span><span class="sxs-lookup"><span data-stu-id="96978-420">hello following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="96978-421">푸시 알림 등록</span><span class="sxs-lookup"><span data-stu-id="96978-421">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="96978-422">Windows 스토어 패키지 SID 가져오기</span><span class="sxs-lookup"><span data-stu-id="96978-422">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="96978-423">플랫폼 간 템플릿을 사용하여 등록</span><span class="sxs-lookup"><span data-stu-id="96978-423">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="96978-424"><a name="register-for-push"></a>방법: 푸시 알림 등록</span><span class="sxs-lookup"><span data-stu-id="96978-424"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="96978-425">모바일 앱 클라이언트 hello Azure 알림 허브에 푸시 알림을 tooregister가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-425">hello Mobile Apps client enables you tooregister for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="96978-426">Hello 플랫폼별에서 가져와야 하는 핸들을 가져오고를 등록할 때 푸시 알림 서비스 (PNS).</span><span class="sxs-lookup"><span data-stu-id="96978-426">When registering, you obtain a handle that you obtain from hello platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="96978-427">그런 다음 hello 등록을 만들 때 모든 태그와 함께이 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-427">You then provide this value along with any tags when you create hello registration.</span></span> <span data-ttu-id="96978-428">hello 다음 코드를 등록 푸시 알림에 대 한 Windows 앱 Windows 알림 서비스 (WNS) hello로:</span><span class="sxs-lookup"><span data-stu-id="96978-428">hello following code registers your Windows app for push notifications with hello Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="96978-429">TooWNS를 밀어 넣는 경우 다음을 수행 해야 [Windows 스토어 패키지 SID를 가져올](#package-sid)합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-429">If you are pushing tooWNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="96978-430">Windows 앱에 대 한 자세한 내용은 tooregister 템플릿 등록에 대 한 참조를 포함 하 여 [추가 푸시 알림 tooyour 앱]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-430">For more information on Windows apps, including how tooregister for template registrations, see [Add push notifications tooyour app].</span></span>

<span data-ttu-id="96978-431">Hello 클라이언트에서 태그를 요청 하는 것은 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-431">Requesting tags from hello client is not supported.</span></span>  <span data-ttu-id="96978-432">태그 요청은 등록에서 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-432">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="96978-433">태그와 장치 tooregister 하려는 경우 사용자 대신 hello 알림 허브 API tooperform hello 등록을 사용 하는 사용자 지정 API를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="96978-433">If you wish tooregister your device with tags, create a Custom API that uses hello Notification Hubs API tooperform hello registration on your behalf.</span></span>  <span data-ttu-id="96978-434">[Hello 사용자 지정 API 호출](#customapi) hello 대신 `RegisterNativeAsync()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="96978-434">[Call hello Custom API](#customapi) instead of hello `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="96978-435"><a name="package-sid"></a>방법: Windows 스토어 패키지 SID 가져오기</span><span class="sxs-lookup"><span data-stu-id="96978-435"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="96978-436">Windows 스토어 앱에서 푸시 알림 사용에 패키지 SID가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-436">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="96978-437">패키지 SID tooreceive hello Windows 저장소로 응용 프로그램을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-437">tooreceive a package SID, register your application with hello Windows Store.</span></span>

<span data-ttu-id="96978-438">tooobtain이이 값:</span><span class="sxs-lookup"><span data-stu-id="96978-438">tooobtain this value:</span></span>

1. <span data-ttu-id="96978-439">Visual Studio 솔루션 탐색기, 마우스 오른쪽 단추로 클릭 hello Windows 스토어 응용 프로그램 프로젝트에서에서 클릭 **저장소** > **hello 저장소로 응용 프로그램 연결 중...** .</span><span class="sxs-lookup"><span data-stu-id="96978-439">In Visual Studio Solution Explorer, right-click hello Windows Store app project, click **Store** > **Associate App with hello Store...**.</span></span>
2. <span data-ttu-id="96978-440">Hello 마법사에서 **다음**, इ न क ा Microsoft ख에서 응용 프로그램에 대 한 이름을 입력 **새로운 앱 이름 예약**, 클릭 **예약**합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-440">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="96978-441">Hello 앱 등록을 성공적으로 만든 hello 응용 프로그램 이름 되 면 클릭 **다음**, 클릭 하 고 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-441">After hello app registration is successfully created, select hello app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="96978-442">Toohello 로그인 [Windows 개발자 센터] Microsoft 계정을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-442">Log in toohello [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="96978-443">아래 **My apps**를 만든 hello 앱 등록을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-443">Under **My apps**, click hello app registration you created.</span></span>
5. <span data-ttu-id="96978-444">클릭 **앱 관리** > **응용 프로그램 id**, 한 다음 toofind 아래로 스크롤하여 프로그램 **패키지 SID**합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-444">Click **App management** > **App identity**, and then scroll down toofind your **Package SID**.</span></span>

<span data-ttu-id="96978-445">Hello 패키지 SID의 다양 한 용도로로 처리는 URI toouse 필요한 경우 *ms-app: / /* hello 구성표로 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-445">Many uses of hello package SID treat it as a URI, in which case you need toouse *ms-app://* as hello scheme.</span></span> <span data-ttu-id="96978-446">패키지 SID 접두사로이 값을 연결 하 여 형성의 hello 버전을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="96978-446">Make note of hello version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="96978-447">Xamarin 앱 몇 가지 추가 코드 toobe 수 tooregister hello iOS 또는 Android 플랫폼에서 실행 되는 앱이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-447">Xamarin apps require some additional code toobe able tooregister an app running on hello iOS or Android platforms.</span></span> <span data-ttu-id="96978-448">자세한 내용은 플랫폼 hello 항목을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="96978-448">For more information, see hello topic for your platform:</span></span>

* [<span data-ttu-id="96978-449">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="96978-449">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="96978-450">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="96978-450">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="96978-451"><a name="register-xplat"></a>방법: 레지스터 푸시 템플릿 toosend 플랫폼 간 알림</span><span class="sxs-lookup"><span data-stu-id="96978-451"><a name="register-xplat"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="96978-452">tooregister 템플릿을 사용 하 여 hello `RegisterAsync()` 다음과 같이 hello 템플릿으로 메서드:</span><span class="sxs-lookup"><span data-stu-id="96978-452">tooregister templates, use hello `RegisterAsync()` method with hello templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="96978-453">템플릿이 있어야 `JObject` 가 입력 하 고 JSON 형식에 따라 hello에 템플릿이 여러 개 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-453">Your templates should be `JObject` types and can contain multiple templates in hello following JSON format:</span></span>

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

<span data-ttu-id="96978-454">메서드를 hello **RegisterAsync()** 도 보조 타일을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-454">hello method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="96978-455">보안을 위해 등록하는 동안 모든 태그가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="96978-455">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="96978-456">tooadd tooinstallations 또는 템플릿을 설치 내에서 태그를 삽입 하 고 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK와 작업]을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="96978-456">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="96978-457">등록 된 이러한 템플릿을 활용 toosend 알림을 참조 toohello [알림 허브 Api]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-457">toosend notifications utilizing these registered templates, refer toohello [Notification Hubs APIs].</span></span>

## <span data-ttu-id="96978-458"><a name="misc"></a>기타 토픽</span><span class="sxs-lookup"><span data-stu-id="96978-458"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="96978-459"><a name="errors"></a>방법: 오류 처리</span><span class="sxs-lookup"><span data-stu-id="96978-459"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="96978-460">Hello 백 엔드에 오류가 발생 하는 경우 hello client SDK를 발생 한 `MobileServiceInvalidOperationException`합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-460">When an error occurs in hello backend, hello client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="96978-461">다음 예제에서는 어떻게 toohandle hello 백엔드에서 반환 되는 예외:</span><span class="sxs-lookup"><span data-stu-id="96978-461">The following example shows how toohandle an exception that is returned by hello backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into hello database. When hello operation completes
    // and App Service has assigned an Id, hello item is added toohello CollectionView
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

<span data-ttu-id="96978-462">Hello에 오류 조건 처리 하는 또 다른 예로 있습니다 [모바일 앱 파일 샘플]합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-462">Another example of dealing with error conditions can be found in hello [Mobile Apps Files Sample].</span></span> <span data-ttu-id="96978-463">[LoggingHandler] 예제는 로깅 대리자 처리기 toolog hello 요청을 보내는 toohello 백 엔드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="96978-463">The [LoggingHandler] example provides a logging delegate handler toolog hello requests being made toohello backend.</span></span>

### <span data-ttu-id="96978-464"><a name="headers"></a>방법: 요청 헤더 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="96978-464"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="96978-465">toosupport 특정 앱 시나리오에서는 모바일 앱 백 엔드에서 hello와 toocustomize 통신을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-465">toosupport your specific app scenario, you might need toocustomize communication with hello Mobile App backend.</span></span> <span data-ttu-id="96978-466">예를 들어 원하는 tooadd 사용자 지정 헤더 tooevery 나가는 요청 또는 응답 상태 코드를 변경할 수도 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96978-466">For example, you may want tooadd a custom header tooevery outgoing request or even change responses status codes.</span></span> <span data-ttu-id="96978-467">사용자 지정을 사용할 수 있습니다 [DelegatingHandler]와 같이, 다음 예제는 hello:</span><span class="sxs-lookup"><span data-stu-id="96978-467">You can use a custom [DelegatingHandler], as in hello following example:</span></span>

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
        // Change hello request-side here based on hello HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do hello request
        var response = await base.SendAsync(request, cancellationToken);

        // Change hello response-side here based on hello HttpResponseMessage

        // Return hello modified response
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

[추가 인증 tooyour 앱]: app-service-mobile-windows-store-dotnet-get-started-users.md
[Azure 모바일 앱에서 데이터 동기화 오프 라인]: app-service-mobile-offline-data-sync.md
[추가 푸시 알림 tooyour 앱]: app-service-mobile-windows-store-dotnet-get-started-push.md
[등록 하면 앱 toouse Microsoft 계정 로그인]: app-service-mobile-how-to-configure-microsoft-authentication.md
[tooconfigure Active Directory 로그인에 대 한 서비스 응용 프로그램 방법]: app-service-mobile-how-to-configure-active-directory-authentication.md

<!-- Microsoft URLs. -->
[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx
[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx
[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx
[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx
[ MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx
[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx
[참조 tooan 형식화 되지 않은 테이블을 만들고]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx
[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx
[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx
[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx
[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx
[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx
[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx
[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx
[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx
[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx
[걸릴]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx
[선택]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx
[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx
[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx
[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx
[여기서]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx
[Azure 포털]: https://portal.azure.com/
[Azure 클래식 포털]: https://manage.windowsazure.com/
[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx
[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx
[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx
[Windows 개발자 센터]: https://dev.windows.com/en-us/overview
[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx
[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx
[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
[알림 허브 Api]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[모바일 앱 파일 샘플]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files
[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63

<!-- External URLs -->
[OData v3 설명서]: http://www.odata.org/documentation/odata-version-3-0/
[Fiddler]: http://www.telerik.com/fiddler
[Json.NET]: http://www.newtonsoft.com/json
[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/
[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
