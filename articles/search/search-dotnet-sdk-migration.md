---
title: "Azure 검색.NET SDK 버전 1.1 aaaUpgrading toohello | Microsoft Docs"
description: "Azure 검색.NET SDK 버전 1.1 toohello 업그레이드"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a><span data-ttu-id="ebef0-103">Azure 검색.NET SDK 버전 3 toohello 업그레이드</span><span class="sxs-lookup"><span data-stu-id="ebef0-103">Upgrading toohello Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="ebef0-104">버전 2.0 preview 또는 이전 버전의 hello를 사용 하는 경우 [Azure 검색.NET SDK](https://aka.ms/search-sdk),이 여기서 응용 프로그램 toouse 버전 3을 업그레이드 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-104">If you're using version 2.0-preview or older of hello [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application toouse version 3.</span></span>

<span data-ttu-id="ebef0-105">Hello SDK의 보다 일반적인 연습을 포함 하 여 예제를 보려면 참조 [toouse Azure.NET 응용 프로그램에서 검색 하는 방법](search-howto-dotnet-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-105">For a more general walkthrough of hello SDK including examples, see [How toouse Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="ebef0-106">Hello Azure 검색.NET SDK의 버전 3 이전 버전의 일부 변경 내용이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-106">Version 3 of hello Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="ebef0-107">대부분 소소한 변경이므로 코드를 변경하는 데 최소한의 작업만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="ebef0-108">참조 [단계 tooupgrade](#UpgradeSteps) 방법에 대 한 지침은 toochange 코드 toouse hello 새 SDK 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-108">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="ebef0-109">버전 1.0.2-preview 사용 중인 경우, 이전 또는 다음 tooversion 3을 업그레이드 한 tooversion 1.1를 먼저 업그레이드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-109">If you're using version 1.0.2-preview or older, you should upgrade tooversion 1.1 first, and then upgrade tooversion 3.</span></span> <span data-ttu-id="ebef0-110">참조 [부록: 단계 tooupgrade tooversion 1.1](#UpgradeStepsV1) 지침에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-110">See [Appendix: Steps tooupgrade tooversion 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="ebef0-111">Azure 검색 서비스 인스턴스를 최신 hello를 비롯 한 몇 가지 REST API 버전을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-111">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="ebef0-112">이것은 더 이상 최신 하나 hello 코드 toouse hello 최신 버전으로 마이그레이션하는 것을 권장 하는 경우 toouse 버전을 계속할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-112">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span> <span data-ttu-id="ebef0-113">Hello REST API를 사용할 경우 hello api 버전 매개 변수를 통해 모든 요청에서 hello API 버전을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-113">When using hello REST API, you must specify hello API version in every request via hello api-version parameter.</span></span> <span data-ttu-id="ebef0-114">Hello.NET SDK를 사용할 때는 hello 버전의 SDK 사용 하는 hello hello hello REST API의 해당 버전을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-114">When using hello .NET SDK, hello version of hello SDK you’re using determines hello corresponding version of hello REST API.</span></span> <span data-ttu-id="ebef0-115">이전 SDK를 사용 하는 경우 계속할 수 있습니다 toorun 변경 하지 않고 해당 코드 경우에 hello 서비스 업그레이드 toosupport 최신 API 버전.</span><span class="sxs-lookup"><span data-stu-id="ebef0-115">If you are using an older SDK, you can continue toorun that code with no changes even if hello service is upgraded toosupport a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="ebef0-116">버전 3의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="ebef0-116">What's new in version 3</span></span>
<span data-ttu-id="ebef0-117">Hello Azure 검색.NET SDK 대상 hello 최신 버전의 세 번째 버전의 hello Azure 검색 REST API, 특히: 2016-09-01의 일반 공급 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-117">Version 3 of hello Azure Search .NET SDK targets hello latest generally available version of hello Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="ebef0-118">이렇게 하면 가능한 toouse hello 다음을 비롯 한.NET 응용 프로그램에서 Azure 검색의 여러 가지 새로운 기능:</span><span class="sxs-lookup"><span data-stu-id="ebef0-118">This makes it possible toouse many new features of Azure Search from a .NET application, including hello following:</span></span>

* [<span data-ttu-id="ebef0-119">사용자 지정 분석기</span><span class="sxs-lookup"><span data-stu-id="ebef0-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="ebef0-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) 및 [Azure Table Storage](search-howto-indexing-azure-tables.md) 인덱서 지원</span><span class="sxs-lookup"><span data-stu-id="ebef0-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="ebef0-121">[필드 매핑](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="ebef0-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="ebef0-122">Etag는 업데이트를 지원 tooenable 안전 동시 인덱스 정의 인덱서 및 데이터 원본</span><span class="sxs-lookup"><span data-stu-id="ebef0-122">ETags support tooenable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="ebef0-123">모델 클래스를 데코레이팅하 하 고 새 hello를 사용 하 여 인덱스 필드 정의 선언적으로 구축에 대 한 지원 `FieldBuilder` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-123">Support for building index field definitions declaratively by decorating your model class and using hello new `FieldBuilder` class.</span></span>
* <span data-ttu-id="ebef0-124">.NET Core와 .NET 이식 가능 프로필 111에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="ebef0-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="ebef0-125">단계 tooupgrade</span><span class="sxs-lookup"><span data-stu-id="ebef0-125">Steps tooupgrade</span></span>
<span data-ttu-id="ebef0-126">먼저, NuGet 참조에 대 한 업데이트 `Microsoft.Azure.Search` 어느 hello NuGet 패키지 관리자 콘솔을 사용 하 여 또는으로 프로젝트 참조를 마우스 오른쪽 단추로 클릭 하 고 Visual Studio에서 "관리 NuGet 패키지..."를 선택 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="ebef0-127">NuGet을 다운로드 한 hello 새 패키지와 종속 되 면 프로젝트를 다시 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="ebef0-127">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="ebef0-128">코드가 구조화된 방식에 따라 다시 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="ebef0-129">이 경우 준비 toogo 넌!</span><span class="sxs-lookup"><span data-stu-id="ebef0-129">If so, you're ready toogo!</span></span>

<span data-ttu-id="ebef0-130">빌드 오류가 발생 하면 빌드 오류가 hello 다음과 같이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-130">If your build fails, you should see a build error like hello following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="ebef0-131">다음 단계 hello toofix이 빌드 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-131">hello next step is toofix this build error.</span></span> <span data-ttu-id="ebef0-132">참조 [버전 3의에서 주요 변경 내용](#ListOfChanges) hello 오류 발생 원인에 대 한 세부 정보에 대 한 방법과 toofix 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes hello error and how toofix it.</span></span>

<span data-ttu-id="ebef0-133">추가 빌드 표시 될 수 있습니다 경고 관련 tooobsolete 메서드 또는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-133">You may see additional build warnings related tooobsolete methods or properties.</span></span> <span data-ttu-id="ebef0-134">hello 경고 어떤 toouse 대신 hello의 사용 되지 않는 기능에 대 한 지침을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-134">hello warnings will include instructions on what toouse instead of hello deprecated feature.</span></span> <span data-ttu-id="ebef0-135">예를 들어, 응용 프로그램 사용 hello `IndexingParameters.Base64EncodeKeys` 속성을 가져와야 한다는 경고`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span><span class="sxs-lookup"><span data-stu-id="ebef0-135">For example, if your application uses hello `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="ebef0-136">모든 빌드 오류를 해결 한 면 변경할 수 있습니다 tooyour 응용 프로그램 tootake 새 기능을 이용 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="ebef0-136">Once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span> <span data-ttu-id="ebef0-137">Hello SDK의에서 새로운 기능에 자세히 설명 되어 [버전 3의에서 새로운 기능](#WhatsNew)합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-137">New features in hello SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="ebef0-138">버전 3의 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="ebef0-138">Breaking changes in version 3</span></span>
<span data-ttu-id="ebef0-139">있는 적은 수의 코드가 필요할 수 있는 주요 변경 내용 버전 3에서에서 변경 또한 toorebuilding 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-139">There a small number of breaking changes in version 3 that may require code changes in addition toorebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="ebef0-140">Indexes.GetClient 반환 형식</span><span class="sxs-lookup"><span data-stu-id="ebef0-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="ebef0-141">hello `Indexes.GetClient` 메서드 새 반환 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-141">hello `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="ebef0-142">반환 된 이전에 `SearchIndexClient`, 너무 변경 된`ISearchIndexClient` -미리 보기, 버전 2.0에서 변경 tooversion 3 통해 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-142">Previously, it returned `SearchIndexClient`, but this was changed too`ISearchIndexClient` in version 2.0-preview, and that change carries over tooversion 3.</span></span> <span data-ttu-id="ebef0-143">이 원하는 toomock hello toosupport 고객 `GetClient` 모의 구현을 반환 하 여 단위 테스트에 대 한 메서드 `ISearchIndexClient`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-143">This is toosupport customers that wish toomock hello `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="ebef0-144">예제</span><span class="sxs-lookup"><span data-stu-id="ebef0-144">Example</span></span>
<span data-ttu-id="ebef0-145">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="ebef0-146">Toothis toofix 변경할 수 있습니다 빌드 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-146">You can change it toothis toofix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a><span data-ttu-id="ebef0-147">AnalyzerName, 데이터 형식 및 다른 사용자는 더 이상 암시적으로 변환할 toostrings</span><span class="sxs-lookup"><span data-stu-id="ebef0-147">AnalyzerName, DataType, and others are no longer implicitly convertible toostrings</span></span>
<span data-ttu-id="ebef0-148">Hello에서 파생 되는 Azure 검색.NET SDK에서 여러 형식을 `ExtensibleEnum`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-148">There are many types in hello Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="ebef0-149">이전에 이러한 형식이 된 모두 암시적으로 변환할 수 tootype `string`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-149">Previously these types were all implicitly convertible tootype `string`.</span></span> <span data-ttu-id="ebef0-150">그러나 hello는 버그가 발견 된 `Object.Equals` 이러한 클래스 및 해결 hello 버그 필요한이 암시적 변환은 사용 하지 않도록 설정에 대 한 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-150">However, a bug was discovered in hello `Object.Equals` implementation for these classes, and fixing hello bug required disabling this implicit conversion.</span></span> <span data-ttu-id="ebef0-151">명시적 변환 너무`string` 는 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-151">Explicit conversion too`string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="ebef0-152">예제</span><span class="sxs-lookup"><span data-stu-id="ebef0-152">Example</span></span>
<span data-ttu-id="ebef0-153">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-153">If your code looks like this:</span></span>

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

<span data-ttu-id="ebef0-154">Toothis toofix 변경할 수 있습니다 빌드 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-154">You can change it toothis toofix any build errors:</span></span>

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a><span data-ttu-id="ebef0-155">더 이상 사용되지 않는 멤버가 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-155">Removed obsolete members</span></span>

<span data-ttu-id="ebef0-156">빌드 오류 관련된 toomethods 또는 버전 2.0-미리 보기에서 사용 되지 않는 것으로 표시 되어 이후에 버전 3에서에서 제거 된 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-156">You may see build errors related toomethods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="ebef0-157">다음은 이러한 오류가 발생 하는 경우 어떻게 tooresolve 해당:</span><span class="sxs-lookup"><span data-stu-id="ebef0-157">If you encounter such errors, here is how tooresolve them:</span></span>

- <span data-ttu-id="ebef0-158">`ScoringParameter(string name, string value)` 구문을 사용한 경우 `ScoringParameter(string name, IEnumerable<string> values)`을 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="ebef0-159">Hello를 사용 하는 경우 `ScoringParameter.Value` 속성을 사용 하 여 hello `ScoringParameter.Values` 속성 또는 hello `ToString` 메서드 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-159">If you were using hello `ScoringParameter.Value` property, use hello `ScoringParameter.Values` property or hello `ToString` method instead.</span></span>
- <span data-ttu-id="ebef0-160">Hello를 사용 하는 경우 `SearchRequestOptions.RequestId` 속성을 사용 하 여 hello `ClientRequestId` 속성 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-160">If you were using hello `SearchRequestOptions.RequestId` property, use hello `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="ebef0-161">제거된 미리 보기 기능</span><span class="sxs-lookup"><span data-stu-id="ebef0-161">Removed preview features</span></span>

<span data-ttu-id="ebef0-162">버전 2.0 preview tooversion 3에서에서 업그레이드 하는 경우에 JSON과 CSV 구문 분석 Blob 인덱서에 대 한 지원을 제거 된 것에 있으므로 이러한 기능은 여전히 미리 보기 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-162">If you are upgrading from version 2.0-preview tooversion 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="ebef0-163">특히 다음 hello의 메서드를 hello `IndexingParametersExtensions` 클래스 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-163">Specifically, hello following methods of hello `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="ebef0-164">응용 프로그램에 이러한 기능에 대 한 강한 종속성의 hello Azure 검색.NET SDK 수 tooupgrade tooversion 3 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-164">If your application has a hard dependency on these features, you will not be able tooupgrade tooversion 3 of hello Azure Search .NET SDK.</span></span> <span data-ttu-id="ebef0-165">Toouse 버전 2.0-미리 보기를 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-165">You can continue toouse version 2.0-preview.</span></span> <span data-ttu-id="ebef0-166">하지만 **프로덕션 응용 프로그램에서는 미리 보기 SDK를 사용하지 않는 것이 좋습니다**.</span><span class="sxs-lookup"><span data-stu-id="ebef0-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="ebef0-167">미리 보기 기능은 평가용일 뿐이며 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="ebef0-168">결론</span><span class="sxs-lookup"><span data-stu-id="ebef0-168">Conclusion</span></span>
<span data-ttu-id="ebef0-169">Hello Azure 검색.NET SDK를 사용 하 여 대 한 자세한 내용이 필요한 경우 참조는 최근에 업데이트 된 [방법](search-howto-dotnet-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-169">If you need more details on using hello Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="ebef0-170">Hello SDK에 피드백을 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-170">We welcome your feedback on hello SDK.</span></span> <span data-ttu-id="ebef0-171">문제가 발생 하면 느껴집니다 무료 tooask us hello에 대 한 도움말 [Azure 검색 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch)합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-171">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="ebef0-172">버그를 발견 하는 경우 hello에 문제를 보고할 수 있습니다 [Azure.NET SDK GitHub 리포지토리](https://github.com/Azure/azure-sdk-for-net/issues)합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-172">If you find a bug, you can file an issue in hello [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="ebef0-173">문제 제목으로 tooprefix 있는지 확인 "검색 SDK:".</span><span class="sxs-lookup"><span data-stu-id="ebef0-173">Make sure tooprefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="ebef0-174">Azure 검색을 이용해 주셔서 감사합니다!</span><span class="sxs-lookup"><span data-stu-id="ebef0-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a><span data-ttu-id="ebef0-175">부록: 단계 tooupgrade tooversion 1.1</span><span class="sxs-lookup"><span data-stu-id="ebef0-175">Appendix: Steps tooupgrade tooversion 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="ebef0-176">이 섹션에는 Azure 검색.NET SDK 버전 1.0.2-preview hello 및 이전 toousers만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-176">This section applies only toousers of hello Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="ebef0-177">먼저, NuGet 참조에 대 한 업데이트 `Microsoft.Azure.Search` 어느 hello NuGet 패키지 관리자 콘솔을 사용 하 여 또는으로 프로젝트 참조를 마우스 오른쪽 단추로 클릭 하 고 Visual Studio에서 "관리 NuGet 패키지..."를 선택 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="ebef0-178">NuGet을 다운로드 한 hello 새 패키지와 종속 되 면 프로젝트를 다시 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="ebef0-178">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="ebef0-179">경우에 버전 1.0.0-preview, 1.0.1-preview, 또는 1.0.2-preview, hello 빌드를 사용 하 여 이전에 성공적으로 되며 준비 toogo 본인이!</span><span class="sxs-lookup"><span data-stu-id="ebef0-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, hello build should succeed and you're ready toogo!</span></span>

<span data-ttu-id="ebef0-180">버전 0.13.0-preview 이전에 사용한 경우 또는 이전 버전을 표시 되어야 빌드 hello 다음과 같은 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-180">If you were previously using version 0.13.0-preview or older, you should see build errors like hello following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="ebef0-181">hello 다음 단계 toofix hello 빌드 오류가 발생 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-181">hello next step is toofix hello build errors one by one.</span></span> <span data-ttu-id="ebef0-182">대부분은 hello SDK에서에서 이름이 바뀐 일부 클래스 및 메서드 이름을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-182">Most will require changing some class and method names that have been renamed in hello SDK.</span></span> <span data-ttu-id="ebef0-183">[버전 1.1의 주요 변경 내용 목록](#ListOfChangesV1) 에는 이러한 이름 변경 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="ebef0-184">사용자 지정 클래스 toomodel 문서를 사용 하 고 nullable이 아닌 기본 형식 속성에 해당 클래스에는 경우 (예를 들어 `int` 또는 `bool` C#), 버그 수정에에서 없는 hello 1.1 버전의 hello SDK는 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-184">If you're using custom classes toomodel your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in hello 1.1 version of hello SDK of which you should be aware.</span></span> <span data-ttu-id="ebef0-185">자세한 내용은 [1.1 버전의 버그 수정](#BugFixesV1) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ebef0-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="ebef0-186">마지막으로, 모든 빌드 오류를 해결 한 면 변경할 수 있습니다 tooyour 응용 프로그램 tootake 새 기능을 이용 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="ebef0-186">Finally, once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="ebef0-187">버전 1.1의 주요 변경 내용 목록</span><span class="sxs-lookup"><span data-stu-id="ebef0-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="ebef0-188">hello 다음과 같은 기준으로 정렬 됩니다 hello 가능성 hello 변경 응용 프로그램 코드에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-188">hello following list is ordered by hello likelihood that hello change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="ebef0-189">IndexBatch 및 IndexAction 변경</span><span class="sxs-lookup"><span data-stu-id="ebef0-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="ebef0-190">`IndexBatch.Create`이름을 바꾼 너무`IndexBatch.New` 더 이상 존재 하 고는 `params` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-190">`IndexBatch.Create` has been renamed too`IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="ebef0-191">다양한 형식의 작업(병합, 삭제 등)이 혼합된 배치에는 `IndexBatch.New` 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="ebef0-192">또한 가지가 새 정적 일괄 처리를 만들기 위한 동일한 모든 hello 작업은 여기서 hello: `Delete`, `Merge`, `MergeOrUpload`, 및 `Upload`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-192">In addition, there are new static methods for creating batches where all hello actions are hello same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="ebef0-193">`IndexAction` 은 더 이상 public 생성자를 포함하지 않으며 해당 속성은 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="ebef0-194">다양 한 용도 대 한 작업을 만들기 위한 hello 새 정적 메서드를 사용 해야: `Delete`, `Merge`, `MergeOrUpload`, 및 `Upload`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-194">You should use hello new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="ebef0-195">`IndexAction.Create` 는 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="ebef0-196">문서에만 사용 하는 hello 오버 로드를 사용 하는 경우 확인 되었는지 toouse `Upload` 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-196">If you used hello overload that takes only a document, make sure toouse `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="ebef0-197">예제</span><span class="sxs-lookup"><span data-stu-id="ebef0-197">Example</span></span>
<span data-ttu-id="ebef0-198">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="ebef0-199">Toothis toofix 변경할 수 있습니다 빌드 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-199">You can change it toothis toofix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="ebef0-200">원하는 경우 있습니다 수 더욱 간소화 것 toothis:</span><span class="sxs-lookup"><span data-stu-id="ebef0-200">If you want, you can further simplify it toothis:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="ebef0-201">IndexBatchException 변경</span><span class="sxs-lookup"><span data-stu-id="ebef0-201">IndexBatchException changes</span></span>
<span data-ttu-id="ebef0-202">hello `IndexBatchException.IndexResponse` 속성 이름을 바꾼 너무`IndexingResults`, 고 해당 형식이 이제 `IList<IndexingResult>`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-202">hello `IndexBatchException.IndexResponse` property has been renamed too`IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="ebef0-203">예제</span><span class="sxs-lookup"><span data-stu-id="ebef0-203">Example</span></span>
<span data-ttu-id="ebef0-204">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="ebef0-205">Toothis toofix 변경할 수 있습니다 빌드 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-205">You can change it toothis toofix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="ebef0-206">작업 메서드 변경</span><span class="sxs-lookup"><span data-stu-id="ebef0-206">Operation method changes</span></span>
<span data-ttu-id="ebef0-207">Hello Azure 검색.NET SDK에 있는 각 작업에 대 한 동기 및 비동기 호출자 메서드 오버 로드 집합으로 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-207">Each operation in hello Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="ebef0-208">hello 서명 및 이러한 메서드 오버 로드의 예상 되는 버전에서 변경 되었습니다 1.1.</span><span class="sxs-lookup"><span data-stu-id="ebef0-208">hello signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="ebef0-209">예를 들어 hello "인덱스 통계 가져오기" 작업 hello SDK의 이전 버전에서는 이러한 서명이 노출:</span><span class="sxs-lookup"><span data-stu-id="ebef0-209">For example, hello "Get Index Statistics" operation in older versions of hello SDK exposed these signatures:</span></span>

<span data-ttu-id="ebef0-210">`IIndexOperations`:</span><span class="sxs-lookup"><span data-stu-id="ebef0-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="ebef0-211">`IndexOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="ebef0-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="ebef0-212">에 대 한 hello 메서드 서명을 다음과 같은 버전 1.1에서에서 동일한 작업 hello:</span><span class="sxs-lookup"><span data-stu-id="ebef0-212">hello method signatures for hello same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="ebef0-213">`IIndexesOperations`:</span><span class="sxs-lookup"><span data-stu-id="ebef0-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="ebef0-214">`IndexesOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="ebef0-214">In `IndexesOperationsExtensions`:</span></span>

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

<span data-ttu-id="ebef0-215">버전 1.1 부터는 hello Azure 검색.NET SDK에서는 작업 메서드가 다르게 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-215">Starting with version 1.1, hello Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="ebef0-216">이제 선택적 매개 변수는 추가 메서드 오버로드가 아닌 기본 매개 변수로 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="ebef0-217">메서드 오버 로드 수가 hello 때로는 크게 감소 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-217">This reduces hello number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="ebef0-218">hello 확장 메서드는 이제 hello 불필요 한 세부 정보는 HTTP hello 호출자에서 많은 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-218">hello extension methods now hide a lot of hello extraneous details of HTTP from hello caller.</span></span> <span data-ttu-id="ebef0-219">예를 들어 이전 버전의 SDK는 하면 자주는 HTTP 상태 코드로 응답 개체를 반환 하는 hello 필요 toocheck 작업 메서드가 throw 되므로 `CloudException` 상태 코드를 오류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-219">For example, older versions of hello SDK returned a response object with an HTTP status code, which you often didn't need toocheck because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="ebef0-220">새 확장 메서드 반환 모델 개체에 hello, 저장 하면 hello toounwrap 않고 코드에서 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-220">hello new extension methods just return model objects, saving you hello trouble of having toounwrap them in your code.</span></span>
* <span data-ttu-id="ebef0-221">반대로, hello 코어 인터페이스 이제 메서드를 노출 필요할 경우 hello HTTP 수준에서 더 많은 제어를 제공 하는.</span><span class="sxs-lookup"><span data-stu-id="ebef0-221">Conversely, hello core interfaces now expose methods that give you more control at hello HTTP level if you need it.</span></span> <span data-ttu-id="ebef0-222">이제 새 hello, 요청에 포함 된 사용자 지정 HTTP 헤더 toobe에 전달할 수 있습니다 `AzureOperationResponse<T>` 반환 형식에 직접 액세스 toohello 제공 `HttpRequestMessage` 및 `HttpResponseMessage` hello 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-222">You can now pass in custom HTTP headers toobe included in requests, and hello new `AzureOperationResponse<T>` return type gives you direct access toohello `HttpRequestMessage` and `HttpResponseMessage` for hello operation.</span></span> <span data-ttu-id="ebef0-223">`AzureOperationResponse`hello에 정의 된 `Microsoft.Rest.Azure` 네임 스페이스 하 고 대체 `Hyak.Common.OperationResponse`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-223">`AzureOperationResponse` is defined in hello `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="ebef0-224">ScoringParameters 변경</span><span class="sxs-lookup"><span data-stu-id="ebef0-224">ScoringParameters changes</span></span>
<span data-ttu-id="ebef0-225">라는 새 클래스 `ScoringParameter` 되었습니다 추가 hello 최신 SDK toomake에 검색 쿼리에 쉽게 tooprovide 매개 변수 tooscoring 프로필.</span><span class="sxs-lookup"><span data-stu-id="ebef0-225">A new class named `ScoringParameter` has been added in hello latest SDK toomake it easier tooprovide parameters tooscoring profiles in a search query.</span></span> <span data-ttu-id="ebef0-226">이전에 hello `ScoringProfiles` hello 속성 `SearchParameters` 클래스도 입력 `IList<string>`; 으로 형식화 되어 이제 `IList<ScoringParameter>`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-226">Previously hello `ScoringProfiles` property of hello `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="ebef0-227">예제</span><span class="sxs-lookup"><span data-stu-id="ebef0-227">Example</span></span>
<span data-ttu-id="ebef0-228">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="ebef0-229">Toothis toofix 변경할 수 있습니다 빌드 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-229">You can change it toothis toofix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="ebef0-230">모델 클래스 변경</span><span class="sxs-lookup"><span data-stu-id="ebef0-230">Model class changes</span></span>
<span data-ttu-id="ebef0-231">에 설명 된 toohello 서명 변경할 인해 [변하는지 메서드](#OperationMethodChanges), 많은 클래스 hello에 `Microsoft.Azure.Search.Models` 네임 스페이스 이름이 변경 되거나 제거 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-231">Due toohello signature changes described in [Operation method changes](#OperationMethodChanges), many classes in hello `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="ebef0-232">예:</span><span class="sxs-lookup"><span data-stu-id="ebef0-232">For example:</span></span>

* <span data-ttu-id="ebef0-233">`IndexDefinitionResponse`는 `AzureOperationResponse<Index>`로 대체되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="ebef0-234">`DocumentSearchResponse`너무 이름이 변경 되었습니다.`DocumentSearchResult`</span><span class="sxs-lookup"><span data-stu-id="ebef0-234">`DocumentSearchResponse` has been renamed too`DocumentSearchResult`</span></span>
* <span data-ttu-id="ebef0-235">`IndexResult`너무 이름이 변경 되었습니다.`IndexingResult`</span><span class="sxs-lookup"><span data-stu-id="ebef0-235">`IndexResult` has been renamed too`IndexingResult`</span></span>
* <span data-ttu-id="ebef0-236">`Documents.Count()`이제 반환는 `long` 대신 hello 문서 수와는`DocumentCountResponse`</span><span class="sxs-lookup"><span data-stu-id="ebef0-236">`Documents.Count()` now returns a `long` with hello document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="ebef0-237">`IndexGetStatisticsResponse`너무 이름이 변경 되었습니다.`IndexGetStatisticsResult`</span><span class="sxs-lookup"><span data-stu-id="ebef0-237">`IndexGetStatisticsResponse` has been renamed too`IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="ebef0-238">`IndexListResponse`너무 이름이 변경 되었습니다.`IndexListResult`</span><span class="sxs-lookup"><span data-stu-id="ebef0-238">`IndexListResponse` has been renamed too`IndexListResult`</span></span>

<span data-ttu-id="ebef0-239">toosummarize, `OperationResponse`-모델 개체를 제거한 toowrap만 존재 하는 클래스를 파생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-239">toosummarize, `OperationResponse`-derived classes that existed only toowrap a model object have been removed.</span></span> <span data-ttu-id="ebef0-240">hello 나머지 클래스가에서 변경 자신의 접미사 `Response` 너무`Result`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-240">hello remaining classes have had their suffix changed from `Response` too`Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="ebef0-241">예제</span><span class="sxs-lookup"><span data-stu-id="ebef0-241">Example</span></span>
<span data-ttu-id="ebef0-242">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-242">If your code looks like this:</span></span>

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

<span data-ttu-id="ebef0-243">Toothis toofix 변경할 수 있습니다 빌드 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-243">You can change it toothis toofix any build errors:</span></span>

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="ebef0-244">응답 클래스 및 IEnumerable</span><span class="sxs-lookup"><span data-stu-id="ebef0-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="ebef0-245">코드에 영향을 줄 수 있는 추가 변경은 더 이상 `IEnumerable<T>`을 구현하지 않는 컬렉션을 보유하는 응답 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="ebef0-246">대신, hello 컬렉션 속성을 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-246">Instead, you can access hello collection property directly.</span></span> <span data-ttu-id="ebef0-247">예를 들어 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="ebef0-248">Toothis toofix 변경할 수 있습니다 빌드 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-248">You can change it toothis toofix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="ebef0-249">웹 응용 프로그램에 대한 특수 사례</span><span class="sxs-lookup"><span data-stu-id="ebef0-249">Special case for web applications</span></span>
<span data-ttu-id="ebef0-250">Serialize 하는 웹 응용 프로그램의 경우 `DocumentSearchResponse` toohello 브라우저 된 toosend 검색 결과 직접 toochange 코드 또는 합니다 hello 결과 올바르게 serialize 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-250">If you have a web application that serializes `DocumentSearchResponse` directly toosend search results toohello browser, you will need toochange your code or hello results will not serialize correctly.</span></span> <span data-ttu-id="ebef0-251">예를 들어 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-251">For example, if your code looks like this:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

<span data-ttu-id="ebef0-252">Hello를 가져와서 변경할 수 있습니다 `.Results` hello 검색 응답 toofix 검색 결과 렌더링의 속성:</span><span class="sxs-lookup"><span data-stu-id="ebef0-252">You can change it by getting hello `.Results` property of hello search response toofix search result rendering:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

<span data-ttu-id="ebef0-253">나면 toolook 이러한 경우에 대 한 코드에서 직접; **hello 컴파일러 경고를 표시 하지 있습니다** 때문에 `JsonResult.Data` 유형의 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-253">You will have toolook for such cases in your code yourself; **hello compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="ebef0-254">CloudException 변경</span><span class="sxs-lookup"><span data-stu-id="ebef0-254">CloudException changes</span></span>
<span data-ttu-id="ebef0-255">hello `CloudException` 클래스가 hello에서 이동 `Hyak.Common` 네임 스페이스 toohello `Microsoft.Rest.Azure` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-255">hello `CloudException` class has moved from hello `Hyak.Common` namespace toohello `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="ebef0-256">또한 해당 `Error` 속성 이름을 바꾼 너무`Body`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-256">Also, its `Error` property has been renamed too`Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="ebef0-257">SearchServiceClient 및 SearchIndexClient 변경</span><span class="sxs-lookup"><span data-stu-id="ebef0-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="ebef0-258">hello 유형의 hello `Credentials` 에서 속성이 변경 `SearchCredentials` tooits 기본 클래스 `ServiceClientCredentials`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-258">hello type of hello `Credentials` property has changed from `SearchCredentials` tooits base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="ebef0-259">Tooaccess hello 해야 할 경우 `SearchCredentials` 의 `SearchIndexClient` 또는 `SearchServiceClient`, 새 hello 따르십시오 `SearchCredentials` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-259">If you need tooaccess hello `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use hello new `SearchCredentials` property.</span></span>

<span data-ttu-id="ebef0-260">이전 버전의 SDK, hello `SearchServiceClient` 및 `SearchIndexClient` 하는 생성자에는 `HttpClient` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-260">In older versions of hello SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="ebef0-261">이는 `HttpClientHandler` 및 `DelegatingHandler` 개체 배열을 사용하는 생성자로 대체되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="ebef0-262">이렇게 하면 보다 쉽게 tooinstall 사용자 지정 처리기 toopre 프로세스 HTTP 요청 필요한 경우.</span><span class="sxs-lookup"><span data-stu-id="ebef0-262">This makes it easier tooinstall custom handlers toopre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="ebef0-263">마지막으로, 하는 생성자를 hello는 `Uri` 및 `SearchCredentials` 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-263">Finally, hello constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="ebef0-264">예를 들어, 다음과 같은 코드가 있는 경우</span><span class="sxs-lookup"><span data-stu-id="ebef0-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="ebef0-265">Toothis toofix 변경할 수 있습니다 빌드 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-265">You can change it toothis toofix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="ebef0-266">또한 hello 유형의 hello 자격 매개 변수를 증명 하는 참고 너무 변경 되었습니다`ServiceClientCredentials`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-266">Also note that hello type of hello credentials parameter has changed too`ServiceClientCredentials`.</span></span> <span data-ttu-id="ebef0-267">이으 나 가능성이 tooaffect 이후 코드 `SearchCredentials` 에서 파생 된 `ServiceClientCredentials`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-267">This is unlikely tooaffect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="ebef0-268">요청 ID 전달</span><span class="sxs-lookup"><span data-stu-id="ebef0-268">Passing a request ID</span></span>
<span data-ttu-id="ebef0-269">Hello SDK의 이전 버전에서는 hello에 요청 ID를 설정할 수 있습니다 `SearchServiceClient` 또는 `SearchIndexClient` 하며 모든 요청 toohello REST API에에서 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-269">In older versions of hello SDK, you could set a request ID on hello `SearchServiceClient` or `SearchIndexClient` and it would be included in every request toohello REST API.</span></span> <span data-ttu-id="ebef0-270">이 toocontact 지원이 필요한 경우 검색 서비스와의 문제를 해결 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-270">This is useful for troubleshooting issues with your search service if you need toocontact support.</span></span> <span data-ttu-id="ebef0-271">그러나이 toouse hello 모든 작업에 대해 동일한 ID 아니라 모든 작업에 대 한 보다 유용한 tooset 고유한 요청 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-271">However, it is more useful tooset a unique request ID for every operation rather than toouse hello same ID for all operations.</span></span> <span data-ttu-id="ebef0-272">이러한 이유로 hello `SetClientRequestId` 방식의 `SearchServiceClient` 및 `SearchIndexClient` 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-272">For this reason, hello `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="ebef0-273">대신, 전달할 수 있습니다 요청 ID tooeach 작업 메서드가 hello를 통해 선택적 `SearchRequestOptions` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-273">Instead, you can pass a request ID tooeach operation method via hello optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="ebef0-274">Hello SDK의 이후 릴리스에서 다른 Azure Sdk에서 사용 하는 hello 접근 방식으로 일치 하는 요청 ID를 전역적으로 클라이언트에서 설정 hello 개체에 대 한 새로운 메커니즘을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-274">In a future release of hello SDK, we will add a new mechanism for setting a request ID globally on hello client objects that is consistent with hello approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="ebef0-275">예제</span><span class="sxs-lookup"><span data-stu-id="ebef0-275">Example</span></span>
<span data-ttu-id="ebef0-276">다음과 같은 코드가 있는 경우</span><span class="sxs-lookup"><span data-stu-id="ebef0-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="ebef0-277">Toothis toofix 변경할 수 있습니다 빌드 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-277">You can change it toothis toofix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="ebef0-278">인터페이스 이름 변경</span><span class="sxs-lookup"><span data-stu-id="ebef0-278">Interface name changes</span></span>
<span data-ttu-id="ebef0-279">hello 작업 그룹 인터페이스 이름에는 모든 변경 된 toobe와 해당 속성 이름 일치:</span><span class="sxs-lookup"><span data-stu-id="ebef0-279">hello operation group interface names have all changed toobe consistent with their corresponding property names:</span></span>

* <span data-ttu-id="ebef0-280">유형의 hello `ISearchServiceClient.Indexes` 에서 이름을 바꾼 `IIndexOperations` 너무`IIndexesOperations`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-280">hello type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` too`IIndexesOperations`.</span></span>
* <span data-ttu-id="ebef0-281">유형의 hello `ISearchServiceClient.Indexers` 에서 이름을 바꾼 `IIndexerOperations` 너무`IIndexersOperations`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-281">hello type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` too`IIndexersOperations`.</span></span>
* <span data-ttu-id="ebef0-282">유형의 hello `ISearchServiceClient.DataSources` 에서 이름을 바꾼 `IDataSourceOperations` 너무`IDataSourcesOperations`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-282">hello type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` too`IDataSourcesOperations`.</span></span>
* <span data-ttu-id="ebef0-283">유형의 hello `ISearchIndexClient.Documents` 에서 이름을 바꾼 `IDocumentOperations` 너무`IDocumentsOperations`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-283">hello type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` too`IDocumentsOperations`.</span></span>

<span data-ttu-id="ebef0-284">이 변경 되지 않으면 오류가 나 가능성이 tooaffect 코드 테스트를 위해 이러한 인터페이스의 모의 개체를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-284">This change is unlikely tooaffect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="ebef0-285">1.1 버전의 버그 수정</span><span class="sxs-lookup"><span data-stu-id="ebef0-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="ebef0-286">이전 버전의 사용자 지정 모델 클래스 hello Azure 검색.NET SDK 연관 시키는 tooserialization의 버그가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-286">There was a bug in older versions of hello Azure Search .NET SDK relating tooserialization of custom model classes.</span></span> <span data-ttu-id="ebef0-287">hello 버그 nullable이 아닌 값 형식의 속성을 사용 하 여 사용자 지정 모델 클래스를 만든 경우에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-287">hello bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-tooreproduce"></a><span data-ttu-id="ebef0-288">단계 tooreproduce</span><span class="sxs-lookup"><span data-stu-id="ebef0-288">Steps tooreproduce</span></span>
<span data-ttu-id="ebef0-289">Null이 허용되지 않는 값 형식의 속성으로 사용자 지정 모델 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="ebef0-290">예를 들어 `int?` 대신 `int` 형식의 공용 `UnitCount` 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="ebef0-291">해당 형식의 기본 값 hello 사용 하 여 문서를 인덱싱할 경우 (예: 0에 대 한 `int`), hello 필드는 Azure 검색에서 null이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-291">If you index a document with hello default value of that type (for example, 0 for `int`), hello field will be null in Azure Search.</span></span> <span data-ttu-id="ebef0-292">이후에 해당 문서에 대 한 검색 하는 경우 hello `Search` 되 `JsonSerializationException` 변환할 수 없는 메시지가 `null` 너무`int`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-292">If you subsequently search for that document, hello `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` too`int`.</span></span>

<span data-ttu-id="ebef0-293">또한 필터 null toohello 인덱스 hello 의도 한 값 대신 기록 되었기 때문에 예상 대로 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-293">Also, filters may not work as expected since null was written toohello index instead of hello intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="ebef0-294">수정 세부 정보</span><span class="sxs-lookup"><span data-stu-id="ebef0-294">Fix details</span></span>
<span data-ttu-id="ebef0-295">Hello SDK의 버전 1.1에서에서이 문제를 해결 했습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-295">We have fixed this issue in version 1.1 of hello SDK.</span></span> <span data-ttu-id="ebef0-296">이제 다음과 같이 모델 클래스가 있고</span><span class="sxs-lookup"><span data-stu-id="ebef0-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="ebef0-297">설정한 `IntValue` too0, 값은 이제 올바르게 hello 통신 중에 0으로 직렬화 하 hello 인덱스에는 0으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-297">and you set `IntValue` too0, that value is now correctly serialized as 0 on hello wire and stored as 0 in hello index.</span></span> <span data-ttu-id="ebef0-298">또한 왕복이 예상대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="ebef0-299">이 접근 방식으로 인식 한 잠재적인 문제 toobe: 너무 있는 모델 유형을 사용 하 여 nullable이 아닌 속성을 갖는 경우**보장** 문서가 인덱스에는 hello 해당 필드에 대 한 null 값이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-299">There is one potential issue toobe aware of with this approach: If you use a model type with a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="ebef0-300">Hello SDK도 아니고 hello Azure 검색 REST API 할 수 있습니다 tooenforce이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-300">Neither hello SDK nor hello Azure Search REST API will help you tooenforce this.</span></span>

<span data-ttu-id="ebef0-301">이 가상의 중요 하지 않은 것: 있는 인덱스를 추가 하면 새 필드 tooan 기존 유형의 경우를 가정해 보십시오 `Edm.Int32`합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="ebef0-302">Hello 인덱스 정의 업데이트 한 후 모든 문서 (Azure 검색에서 null을 허용 하지 않는 형식도) 이후 해당 새 필드에 대해 null 값을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-302">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="ebef0-303">다음으로 nullable이 아닌 모델 클래스를 사용 하는 경우 `int` 해당 필드에 대 한 속성을 얻게 됩니다는 `JsonSerializationException` tooretrieve 문서 하려고 할 때 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="ebef0-304">이러한 이유로 모델 클래스에는 Null을 허용하는 형식을 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="ebef0-305">이 hello 및 버그 수정 프로그램 대 한 자세한 내용은 참조 하십시오 [GitHub에서이 문제](https://github.com/Azure/azure-sdk-for-net/issues/1063)합니다.</span><span class="sxs-lookup"><span data-stu-id="ebef0-305">For more details on this bug and hello fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

