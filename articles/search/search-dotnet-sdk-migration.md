---
title: "Azure Search .NET SDK 버전 1.1로 업그레이드 | Microsoft Docs"
description: "Azure 검색 .NET SDK 버전 1.1로 업그레이드"
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
ms.openlocfilehash: 9782454e3bfc697b63cde8aa28a14be0c393c36b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrading-to-the-azure-search-net-sdk-version-3"></a><span data-ttu-id="15ca9-103">Azure Search .NET SDK 버전 3으로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="15ca9-103">Upgrading to the Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="15ca9-104">버전 2.0-preview 또는 이전 버전의 [Azure Search .NET SDK](https://aka.ms/search-sdk)를 사용하는 경우 이 문서를 통해 버전 3으로 응용 프로그램을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-104">If you're using version 2.0-preview or older of the [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application to use version 3.</span></span>

<span data-ttu-id="15ca9-105">예제를 비롯하여 SDK에 대한 보다 일반적인 연습은 [.NET 응용 프로그램에서 Azure 검색을 사용하는 방법](search-howto-dotnet-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ca9-105">For a more general walkthrough of the SDK including examples, see [How to use Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="15ca9-106">Azure Search .NET SDK 버전 3에는 이전 버전에서 변경된 사항이 일부 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-106">Version 3 of the Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="15ca9-107">대부분 소소한 변경이므로 코드를 변경하는 데 최소한의 작업만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="15ca9-108">새 SDK 버전을 사용하는 코드를 변경하는 방법에 대한 지침은 [업그레이드 단계](#UpgradeSteps) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ca9-108">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="15ca9-109">1.0.2-preview 또는 이전 버전을 사용하는 경우 먼저 버전 1.1로 업그레이드한 후 버전 3으로 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-109">If you're using version 1.0.2-preview or older, you should upgrade to version 1.1 first, and then upgrade to version 3.</span></span> <span data-ttu-id="15ca9-110">지침은 [부록: 1.1 버전으로 업그레이드하는 단계](#UpgradeStepsV1) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ca9-110">See [Appendix: Steps to upgrade to version 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="15ca9-111">Azure Search 서비스 인스턴스는 최신 버전을 포함한 여러 REST API 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-111">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="15ca9-112">더 이상 최신 버전이 아닌 버전을 계속 사용할 수는 있지만 코드를 마이그레이션하여 최신 버전을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-112">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span> <span data-ttu-id="15ca9-113">REST API를 사용하는 경우 api-version 매개 변수를 통해 모든 요청에 API 버전을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-113">When using the REST API, you must specify the API version in every request via the api-version parameter.</span></span> <span data-ttu-id="15ca9-114">.NET SDK를 사용하는 경우 사용 중인 SDK의 버전에 따라 해당하는 REST API 버전이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-114">When using the .NET SDK, the version of the SDK you’re using determines the corresponding version of the REST API.</span></span> <span data-ttu-id="15ca9-115">이전 버전의 SDK를 사용하는 경우 최신 API 버전을 지원하기 위해 서비스가 업그레이드된 경우에도 변경 내용 없이 해당 코드를 계속 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-115">If you are using an older SDK, you can continue to run that code with no changes even if the service is upgraded to support a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="15ca9-116">버전 3의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="15ca9-116">What's new in version 3</span></span>
<span data-ttu-id="15ca9-117">Azure Search .NET SDK 버전 3은 Azure Search REST API의 최신 일반 공급 버전, 특히 2016-09-01을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-117">Version 3 of the Azure Search .NET SDK targets the latest generally available version of the Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="15ca9-118">이 버전이 있으면 다음을 비롯한 많은 Azure Search의 새 기능을 .NET 응용 프로그램에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-118">This makes it possible to use many new features of Azure Search from a .NET application, including the following:</span></span>

* [<span data-ttu-id="15ca9-119">사용자 지정 분석기</span><span class="sxs-lookup"><span data-stu-id="15ca9-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="15ca9-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) 및 [Azure Table Storage](search-howto-indexing-azure-tables.md) 인덱서 지원</span><span class="sxs-lookup"><span data-stu-id="15ca9-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="15ca9-121">[필드 매핑](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="15ca9-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="15ca9-122">인덱스 정의, 인덱서 및 데이터 원본의 안전한 동시 업데이트를 가능하게 하는 Etag 지원</span><span class="sxs-lookup"><span data-stu-id="15ca9-122">ETags support to enable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="15ca9-123">모델 클래스를 데코레이트하고 새 `FieldBuilder` 클래스를 사용하여 인덱스 필드 정의를 선언적으로 지원</span><span class="sxs-lookup"><span data-stu-id="15ca9-123">Support for building index field definitions declaratively by decorating your model class and using the new `FieldBuilder` class.</span></span>
* <span data-ttu-id="15ca9-124">.NET Core와 .NET 이식 가능 프로필 111에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="15ca9-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="15ca9-125">업그레이드 단계</span><span class="sxs-lookup"><span data-stu-id="15ca9-125">Steps to upgrade</span></span>
<span data-ttu-id="15ca9-126">먼저, NuGet 패키지 관리자 콘솔을 사용하거나 Visual Studio에서 프로젝트 참조를 마우스 오른쪽 단추로 클릭하고 "NuGet 패키지 관리..."를 선택하여 `Microsoft.Azure.Search` 에 대한 NuGet 참조를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="15ca9-127">NuGet에서 새 패키지와 해당 종속성을 다운로드했으면 프로젝트를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-127">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="15ca9-128">코드가 구조화된 방식에 따라 다시 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="15ca9-129">다시 빌드할 수 있으면 배포할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-129">If so, you're ready to go!</span></span>

<span data-ttu-id="15ca9-130">빌드가 실패하면 다음과 같은 빌드 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-130">If your build fails, you should see a build error like the following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' to 'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="15ca9-131">다음은 이러한 빌드 오류를 수정하는 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-131">The next step is to fix this build error.</span></span> <span data-ttu-id="15ca9-132">오류의 원인 및 해결 방법에 대한 자세한 내용은 [버전 3의 주요 변경 내용](#ListOfChanges)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ca9-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes the error and how to fix it.</span></span>

<span data-ttu-id="15ca9-133">사용되지 않은 메서드 또는 속성과 관련된 추가 빌드 경고가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-133">You may see additional build warnings related to obsolete methods or properties.</span></span> <span data-ttu-id="15ca9-134">경고에는 사용되지 않는 기능 대신 사용해야 하는 항목에 대한 지침이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-134">The warnings will include instructions on what to use instead of the deprecated feature.</span></span> <span data-ttu-id="15ca9-135">예를 들어 응용 프로그램이 `IndexingParameters.Base64EncodeKeys` 속성을 사용하는 경우 `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`와 같은 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-135">For example, if your application uses the `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="15ca9-136">모든 빌드 오류를 수정했다면 원하는 새 기능을 활용하도록 응용 프로그램을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-136">Once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span></span> <span data-ttu-id="15ca9-137">SDK의 새로운 기능에 대한 자세한 내용은 [버전 3의 새로운 기능](#WhatsNew)에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-137">New features in the SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="15ca9-138">버전 3의 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="15ca9-138">Breaking changes in version 3</span></span>
<span data-ttu-id="15ca9-139">응용 프로그램을 다시 빌드하는 것 외에도, 버전 3에는 코드 변경이 필요할 수 있는 몇 가지 주요 변경 내용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-139">There a small number of breaking changes in version 3 that may require code changes in addition to rebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="15ca9-140">Indexes.GetClient 반환 형식</span><span class="sxs-lookup"><span data-stu-id="15ca9-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="15ca9-141">`Indexes.GetClient` 메서드에는 새 반환 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-141">The `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="15ca9-142">이전에는 `SearchIndexClient`를 반환했으나 버전 2.0-preview에서는 `ISearchIndexClient`로 변경되었으며 이 변경 내용이 버전 3에도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-142">Previously, it returned `SearchIndexClient`, but this was changed to `ISearchIndexClient` in version 2.0-preview, and that change carries over to version 3.</span></span> <span data-ttu-id="15ca9-143">따라서 `ISearchIndexClient`의 모의 구현을 반환하여 단위 테스트를 위한 `GetClient` 메서드를 모의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-143">This is to support customers that wish to mock the `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="15ca9-144">예제</span><span class="sxs-lookup"><span data-stu-id="15ca9-144">Example</span></span>
<span data-ttu-id="15ca9-145">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="15ca9-146">빌드 오류를 수정하기 위해 다음으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-146">You can change it to this to fix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-to-strings"></a><span data-ttu-id="15ca9-147">AnalyzerName, DataType 등은 더 이상 암시적으로 문자열로 변환될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-147">AnalyzerName, DataType, and others are no longer implicitly convertible to strings</span></span>
<span data-ttu-id="15ca9-148">Azure Search .NET SDK에는 `ExtensibleEnum`에서 파생된 여러 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-148">There are many types in the Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="15ca9-149">이전에는 이러한 형식이 모두 `string` 형식으로 암시적으로 변환될 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-149">Previously these types were all implicitly convertible to type `string`.</span></span> <span data-ttu-id="15ca9-150">그러나 이러한 클래스의 `Object.Equals` 구현에서 버그가 발견되었으며 버그 수정을 위해 이러한 암시적 변환을 사용하지 않도록 설정해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-150">However, a bug was discovered in the `Object.Equals` implementation for these classes, and fixing the bug required disabling this implicit conversion.</span></span> <span data-ttu-id="15ca9-151">`string`로의 명시적 변환은 여전히 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-151">Explicit conversion to `string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="15ca9-152">예</span><span class="sxs-lookup"><span data-stu-id="15ca9-152">Example</span></span>
<span data-ttu-id="15ca9-153">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-153">If your code looks like this:</span></span>

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

<span data-ttu-id="15ca9-154">빌드 오류를 수정하기 위해 다음으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-154">You can change it to this to fix any build errors:</span></span>

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

### <a name="removed-obsolete-members"></a><span data-ttu-id="15ca9-155">더 이상 사용되지 않는 멤버가 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-155">Removed obsolete members</span></span>

<span data-ttu-id="15ca9-156">버전 2.0-preview에서 사용되지 않는 것으로 표시되고 이후에 버전 3에서 제거된 메서드 및 속성 관련 빌드 오류가 확인될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-156">You may see build errors related to methods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="15ca9-157">이러한 오류가 발생하는 경우 해결 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-157">If you encounter such errors, here is how to resolve them:</span></span>

- <span data-ttu-id="15ca9-158">`ScoringParameter(string name, string value)` 구문을 사용한 경우 `ScoringParameter(string name, IEnumerable<string> values)`을 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="15ca9-159">`ScoringParameter.Value` 속성을 사용한 경우 `ScoringParameter.Values` 속성 또는 `ToString` 메서드를 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-159">If you were using the `ScoringParameter.Value` property, use the `ScoringParameter.Values` property or the `ToString` method instead.</span></span>
- <span data-ttu-id="15ca9-160">`SearchRequestOptions.RequestId` 속성을 사용한 경우 `ClientRequestId` 속성을 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-160">If you were using the `SearchRequestOptions.RequestId` property, use the `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="15ca9-161">제거된 미리 보기 기능</span><span class="sxs-lookup"><span data-stu-id="15ca9-161">Removed preview features</span></span>

<span data-ttu-id="15ca9-162">버전 2.0-preview에서 버전 3으로 업그레이드하는 경우 Blob 인덱서의 JSON 및 CSV 구문 분석 지원은 미리 보기에는 계속 포함되지만 버전 3에서는 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-162">If you are upgrading from version 2.0-preview to version 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="15ca9-163">특히, `IndexingParametersExtensions` 클래스의 다음 메서드가 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-163">Specifically, the following methods of the `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="15ca9-164">응용 프로그램이 이러한 기능에 강력하게 종속될 경우 Azure Search .NET SDK 버전 3으로 업그레이드하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-164">If your application has a hard dependency on these features, you will not be able to upgrade to version 3 of the Azure Search .NET SDK.</span></span> <span data-ttu-id="15ca9-165">버전 2.0-preview는 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-165">You can continue to use version 2.0-preview.</span></span> <span data-ttu-id="15ca9-166">하지만 **프로덕션 응용 프로그램에서는 미리 보기 SDK를 사용하지 않는 것이 좋습니다**.</span><span class="sxs-lookup"><span data-stu-id="15ca9-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="15ca9-167">미리 보기 기능은 평가용일 뿐이며 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="15ca9-168">결론</span><span class="sxs-lookup"><span data-stu-id="15ca9-168">Conclusion</span></span>
<span data-ttu-id="15ca9-169">Azure 검색 .NET SDK를 사용하는 방법에 대한 자세한 정보가 필요한 경우 최근 업데이트된 [방법](search-howto-dotnet-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ca9-169">If you need more details on using the Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="15ca9-170">SDK에 대한 귀하의 피드백을 환영합니다!</span><span class="sxs-lookup"><span data-stu-id="15ca9-170">We welcome your feedback on the SDK.</span></span> <span data-ttu-id="15ca9-171">문제가 발생하면 [Azure 검색 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch)을 통해 자유롭게 도움을 요청하세요.</span><span class="sxs-lookup"><span data-stu-id="15ca9-171">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="15ca9-172">버그를 발견하는 경우 [Azure .NET SDK GitHub 리포지토리](https://github.com/Azure/azure-sdk-for-net/issues)에 문제를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-172">If you find a bug, you can file an issue in the [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="15ca9-173">문제 제목에 "검색 SDK:"라는 접두사를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-173">Make sure to prefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="15ca9-174">Azure 검색을 이용해 주셔서 감사합니다!</span><span class="sxs-lookup"><span data-stu-id="15ca9-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-to-upgrade-to-version-11"></a><span data-ttu-id="15ca9-175">부록: 1.1 버전으로 업그레이드하는 단계</span><span class="sxs-lookup"><span data-stu-id="15ca9-175">Appendix: Steps to upgrade to version 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="15ca9-176">이 섹션은 Azure Search .NET SDK 버전 1.0.2-preview 이상의 사용자에게만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-176">This section applies only to users of the Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="15ca9-177">먼저, NuGet 패키지 관리자 콘솔을 사용하거나 Visual Studio에서 프로젝트 참조를 마우스 오른쪽 단추로 클릭하고 "NuGet 패키지 관리..."를 선택하여 `Microsoft.Azure.Search` 에 대한 NuGet 참조를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="15ca9-178">NuGet에서 새 패키지와 해당 종속성을 다운로드했으면 프로젝트를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-178">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="15ca9-179">이전에 1.0.0-preview, 1.0.1-preview 또는 1.0.2-preview를 사용한 경우 빌드가 성공하고 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, the build should succeed and you're ready to go!</span></span>

<span data-ttu-id="15ca9-180">이전에 0.13.0-preview 또는 이전 버전을 사용한 경우 다음과 유사한 빌드 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-180">If you were previously using version 0.13.0-preview or older, you should see build errors like the following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: The type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="15ca9-181">다음은 빌드 오류를 하나씩 수정하는 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-181">The next step is to fix the build errors one by one.</span></span> <span data-ttu-id="15ca9-182">대부분은 SDK에서 이름이 변경된 일부 클래스와 메서드 이름을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-182">Most will require changing some class and method names that have been renamed in the SDK.</span></span> <span data-ttu-id="15ca9-183">[버전 1.1의 주요 변경 내용 목록](#ListOfChangesV1) 에는 이러한 이름 변경 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="15ca9-184">사용자 지정 클래스를 사용하여 문서를 모델링하고 해당 클래스에 Null이 허용되지 않는 기본 형식(예를 들어 C#의 `int` 또는 `bool`)이 있는 경우 알고 있어야 할 SDK 버전 1.1의 버그 수정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-184">If you're using custom classes to model your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in the 1.1 version of the SDK of which you should be aware.</span></span> <span data-ttu-id="15ca9-185">자세한 내용은 [1.1 버전의 버그 수정](#BugFixesV1) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ca9-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="15ca9-186">마지막으로, 모든 빌드 오류를 수정했다면 원하는 새 기능을 활용하도록 응용 프로그램을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-186">Finally, once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="15ca9-187">버전 1.1의 주요 변경 내용 목록</span><span class="sxs-lookup"><span data-stu-id="15ca9-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="15ca9-188">다음 목록은 변경이 응용 프로그램 코드에 영향을 줄 가능성 순서로 정렬되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-188">The following list is ordered by the likelihood that the change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="15ca9-189">IndexBatch 및 IndexAction 변경</span><span class="sxs-lookup"><span data-stu-id="15ca9-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="15ca9-190">`IndexBatch.Create`는 `IndexBatch.New`로 이름이 변경되었고 더 이상 `params` 인수를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-190">`IndexBatch.Create` has been renamed to `IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="15ca9-191">다양한 형식의 작업(병합, 삭제 등)이 혼합된 배치에는 `IndexBatch.New` 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="15ca9-192">또한 모든 작업이 동일한 배치를 만드는 새로운 정적 메서드가 제공됩니다(`Delete`, `Merge`, `MergeOrUpload` 및 `Upload`).</span><span class="sxs-lookup"><span data-stu-id="15ca9-192">In addition, there are new static methods for creating batches where all the actions are the same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="15ca9-193">`IndexAction` 은 더 이상 public 생성자를 포함하지 않으며 해당 속성은 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="15ca9-194">`Delete`, `Merge`, `MergeOrUpload` 및 `Upload`와 같은 다양한 용도의 작업을 만들기 위해서는 새로운 정적 메서드를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-194">You should use the new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="15ca9-195">`IndexAction.Create` 는 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="15ca9-196">한 개의 문서만 받는 오버로드를 사용한 경우 대신 `Upload` 를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-196">If you used the overload that takes only a document, make sure to use `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="15ca9-197">예</span><span class="sxs-lookup"><span data-stu-id="15ca9-197">Example</span></span>
<span data-ttu-id="15ca9-198">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="15ca9-199">빌드 오류를 수정하기 위해 다음으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-199">You can change it to this to fix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="15ca9-200">원하는 경우 이를 다음과 같이 보다 단순화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-200">If you want, you can further simplify it to this:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="15ca9-201">IndexBatchException 변경</span><span class="sxs-lookup"><span data-stu-id="15ca9-201">IndexBatchException changes</span></span>
<span data-ttu-id="15ca9-202">`IndexBatchException.IndexResponse` 속성이 `IndexingResults`로 이름이 변경되었고 형식은 이제 `IList<IndexingResult>`입니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-202">The `IndexBatchException.IndexResponse` property has been renamed to `IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="15ca9-203">예</span><span class="sxs-lookup"><span data-stu-id="15ca9-203">Example</span></span>
<span data-ttu-id="15ca9-204">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="15ca9-205">빌드 오류를 수정하기 위해 다음으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-205">You can change it to this to fix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="15ca9-206">작업 메서드 변경</span><span class="sxs-lookup"><span data-stu-id="15ca9-206">Operation method changes</span></span>
<span data-ttu-id="15ca9-207">Azure 검색 .NET SDK의 각 작업은 동기 및 비동기 호출자에 대한 메서드 오버로드 집합으로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-207">Each operation in the Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="15ca9-208">이러한 메서드 오버로드의 서명 및 팩터링이 버전 1.1에서 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-208">The signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="15ca9-209">예를 들어 이전 버전의 SDK에서 "인덱스 통계 가져오기" 작업은 다음과 같은 서명을 노출했습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-209">For example, the "Get Index Statistics" operation in older versions of the SDK exposed these signatures:</span></span>

<span data-ttu-id="15ca9-210">`IIndexOperations`:</span><span class="sxs-lookup"><span data-stu-id="15ca9-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="15ca9-211">`IndexOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="15ca9-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="15ca9-212">버전 1.1에서 동일한 작업에 대한 메서드 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-212">The method signatures for the same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="15ca9-213">`IIndexesOperations`:</span><span class="sxs-lookup"><span data-stu-id="15ca9-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="15ca9-214">`IndexesOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="15ca9-214">In `IndexesOperationsExtensions`:</span></span>

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

<span data-ttu-id="15ca9-215">버전 1.1부터 Azure 검색 .NET SDK가 작업 메서드를 다르게 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-215">Starting with version 1.1, the Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="15ca9-216">이제 선택적 매개 변수는 추가 메서드 오버로드가 아닌 기본 매개 변수로 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="15ca9-217">따라서 메서드 오버로드 수가 경우에 따라서는 상당히 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-217">This reduces the number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="15ca9-218">이제 확장 메서드는 호출자에게 HTTP의 불필요한 많은 세부 정보를 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-218">The extension methods now hide a lot of the extraneous details of HTTP from the caller.</span></span> <span data-ttu-id="15ca9-219">예를 들어 이전 버전의 SDK에서는 HTTP 상태 코드와 함께 응답 개체를 반환했지만 작업 메서드가 오류를 나타내는 상태 코드에 대해 `CloudException` 을 throw하므로 보통은 이를 확인할 필요가 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-219">For example, older versions of the SDK returned a response object with an HTTP status code, which you often didn't need to check because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="15ca9-220">새로운 확장 메서드는 모델 개체만 반환하여 코드에서 래핑 해제해야 하는 문제가 없어집니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-220">The new extension methods just return model objects, saving you the trouble of having to unwrap them in your code.</span></span>
* <span data-ttu-id="15ca9-221">반대로, 코어 인터페이스가 HTTP 수준에서 필요한 경우 보다 세밀한 제어를 제공하는 메서드를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-221">Conversely, the core interfaces now expose methods that give you more control at the HTTP level if you need it.</span></span> <span data-ttu-id="15ca9-222">이제 요청에 포함될 사용자 지정 HTTP 헤더를 전달할 수 있으며 새로운 `AzureOperationResponse<T>` 반환 형식으로 작업할 `HttpRequestMessage` 및 `HttpResponseMessage`에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-222">You can now pass in custom HTTP headers to be included in requests, and the new `AzureOperationResponse<T>` return type gives you direct access to the `HttpRequestMessage` and `HttpResponseMessage` for the operation.</span></span> <span data-ttu-id="15ca9-223">`AzureOperationResponse`는 `Microsoft.Rest.Azure` 네임스페이스에 정의되며 `Hyak.Common.OperationResponse`를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-223">`AzureOperationResponse` is defined in the `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="15ca9-224">ScoringParameters 변경</span><span class="sxs-lookup"><span data-stu-id="15ca9-224">ScoringParameters changes</span></span>
<span data-ttu-id="15ca9-225">최신 SDK에 새 클래스인 `ScoringParameter` 가 추가되어 검색 쿼리에 있는 점수 매기기 프로필에 매개 변수를 더 쉽게 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-225">A new class named `ScoringParameter` has been added in the latest SDK to make it easier to provide parameters to scoring profiles in a search query.</span></span> <span data-ttu-id="15ca9-226">`SearchParameters` 클래스의 `ScoringProfiles` 속성은 이전에는 `IList<string>`으로 입력되었지만 이제는 `IList<ScoringParameter>`로 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-226">Previously the `ScoringProfiles` property of the `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="15ca9-227">예제</span><span class="sxs-lookup"><span data-stu-id="15ca9-227">Example</span></span>
<span data-ttu-id="15ca9-228">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="15ca9-229">빌드 오류를 수정하기 위해 다음으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-229">You can change it to this to fix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="15ca9-230">모델 클래스 변경</span><span class="sxs-lookup"><span data-stu-id="15ca9-230">Model class changes</span></span>
<span data-ttu-id="15ca9-231">[작업 메서드 변경](#OperationMethodChanges)에 설명된 서명 변경으로 인해 `Microsoft.Azure.Search.Models` 네임스페이스의 많은 클래스가 이름이 변경되거나 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-231">Due to the signature changes described in [Operation method changes](#OperationMethodChanges), many classes in the `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="15ca9-232">예:</span><span class="sxs-lookup"><span data-stu-id="15ca9-232">For example:</span></span>

* <span data-ttu-id="15ca9-233">`IndexDefinitionResponse`는 `AzureOperationResponse<Index>`로 대체되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="15ca9-234">`DocumentSearchResponse`는 `DocumentSearchResult`로 이름이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-234">`DocumentSearchResponse` has been renamed to `DocumentSearchResult`</span></span>
* <span data-ttu-id="15ca9-235">`IndexResult`는 `IndexingResult`로 이름이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-235">`IndexResult` has been renamed to `IndexingResult`</span></span>
* <span data-ttu-id="15ca9-236">`Documents.Count()`는 `DocumentCountResponse` 대신 문서 수와 함께 `long`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-236">`Documents.Count()` now returns a `long` with the document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="15ca9-237">`IndexGetStatisticsResponse`는 `IndexGetStatisticsResult`로 이름이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-237">`IndexGetStatisticsResponse` has been renamed to `IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="15ca9-238">`IndexListResponse`는 `IndexListResult`로 이름이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-238">`IndexListResponse` has been renamed to `IndexListResult`</span></span>

<span data-ttu-id="15ca9-239">요약하자면 모델 개체를 래핑하기 위해서만 존재했던 `OperationResponse`파생 클래스가 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-239">To summarize, `OperationResponse`-derived classes that existed only to wrap a model object have been removed.</span></span> <span data-ttu-id="15ca9-240">나머지 클래스는 접미사가 `Response`에서 `Result`로 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-240">The remaining classes have had their suffix changed from `Response` to `Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="15ca9-241">예제</span><span class="sxs-lookup"><span data-stu-id="15ca9-241">Example</span></span>
<span data-ttu-id="15ca9-242">코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-242">If your code looks like this:</span></span>

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

<span data-ttu-id="15ca9-243">빌드 오류를 수정하기 위해 다음으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-243">You can change it to this to fix any build errors:</span></span>

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

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="15ca9-244">응답 클래스 및 IEnumerable</span><span class="sxs-lookup"><span data-stu-id="15ca9-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="15ca9-245">코드에 영향을 줄 수 있는 추가 변경은 더 이상 `IEnumerable<T>`을 구현하지 않는 컬렉션을 보유하는 응답 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="15ca9-246">대신, 컬렉션 속성에 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-246">Instead, you can access the collection property directly.</span></span> <span data-ttu-id="15ca9-247">예를 들어 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="15ca9-248">빌드 오류를 수정하기 위해 다음으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-248">You can change it to this to fix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="15ca9-249">웹 응용 프로그램에 대한 특수 사례</span><span class="sxs-lookup"><span data-stu-id="15ca9-249">Special case for web applications</span></span>
<span data-ttu-id="15ca9-250">`DocumentSearchResponse` 를 직접 serialize하여 검색 결과를 브라우저로 보내는 웹 응용 프로그램이 있는 경우 코드를 변경해야 하며 그렇지 않은 경우 결과가 제대로 serialize되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-250">If you have a web application that serializes `DocumentSearchResponse` directly to send search results to the browser, you will need to change your code or the results will not serialize correctly.</span></span> <span data-ttu-id="15ca9-251">예를 들어 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-251">For example, if your code looks like this:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want to search everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

<span data-ttu-id="15ca9-252">검색 결과 렌더링을 수정하기 위해 검색 응답의 `.Results` 속성을 가져와 이를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-252">You can change it by getting the `.Results` property of the search response to fix search result rendering:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want to search everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

<span data-ttu-id="15ca9-253">코드에서 직접 이러한 경우를 찾아야 합니다. `JsonResult.Data`가 `object` 형식이므로 **컴파일러가 경고해주지 않습니다**.</span><span class="sxs-lookup"><span data-stu-id="15ca9-253">You will have to look for such cases in your code yourself; **The compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="15ca9-254">CloudException 변경</span><span class="sxs-lookup"><span data-stu-id="15ca9-254">CloudException changes</span></span>
<span data-ttu-id="15ca9-255">`CloudException` 클래스가 `Hyak.Common` 네임스페이스에서 `Microsoft.Rest.Azure` 네임스페이스로 이동되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-255">The `CloudException` class has moved from the `Hyak.Common` namespace to the `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="15ca9-256">또한 해당 `Error` 속성의 이름이 `Body`로 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-256">Also, its `Error` property has been renamed to `Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="15ca9-257">SearchServiceClient 및 SearchIndexClient 변경</span><span class="sxs-lookup"><span data-stu-id="15ca9-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="15ca9-258">`Credentials` 속성의 형식이 `SearchCredentials`에서 기본 클래스 `ServiceClientCredentials`로 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-258">The type of the `Credentials` property has changed from `SearchCredentials` to its base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="15ca9-259">`SearchIndexClient` 또는 `SearchServiceClient`의 `SearchCredentials`에 액세스해야 하는 경우 새 `SearchCredentials` 속성을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="15ca9-259">If you need to access the `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use the new `SearchCredentials` property.</span></span>

<span data-ttu-id="15ca9-260">이전 버전의 SDK에서 `SearchServiceClient` 및 `SearchIndexClient`는 `HttpClient` 매개 변수를 사용하는 생성자를 포함했습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-260">In older versions of the SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="15ca9-261">이는 `HttpClientHandler` 및 `DelegatingHandler` 개체 배열을 사용하는 생성자로 대체되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="15ca9-262">이렇게 하면 필요한 경우 전처리 HTTP 요청에 사용자 지정 처리기를 쉽게 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-262">This makes it easier to install custom handlers to pre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="15ca9-263">마지막으로 `Uri` 및 `SearchCredentials`를 사용하는 생성자가 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-263">Finally, the constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="15ca9-264">예를 들어, 다음과 같은 코드가 있는 경우</span><span class="sxs-lookup"><span data-stu-id="15ca9-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="15ca9-265">빌드 오류를 수정하기 위해 다음으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-265">You can change it to this to fix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="15ca9-266">또한 자격 증명 매개 변수의 형식이 `ServiceClientCredentials`로 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-266">Also note that the type of the credentials parameter has changed to `ServiceClientCredentials`.</span></span> <span data-ttu-id="15ca9-267">`SearchCredentials`는 `ServiceClientCredentials`에서 파생되므로 코드에 영향을 줄 가능성은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-267">This is unlikely to affect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="15ca9-268">요청 ID 전달</span><span class="sxs-lookup"><span data-stu-id="15ca9-268">Passing a request ID</span></span>
<span data-ttu-id="15ca9-269">이전 버전의 SDK에서는 요청 ID를 `SearchServiceClient` 또는 `SearchIndexClient`에서 설정하고 REST API에 대한 모든 요청에 포함했습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-269">In older versions of the SDK, you could set a request ID on the `SearchServiceClient` or `SearchIndexClient` and it would be included in every request to the REST API.</span></span> <span data-ttu-id="15ca9-270">지원에 문의해야 하는 경우 검색 서비스로 문제를 해결하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-270">This is useful for troubleshooting issues with your search service if you need to contact support.</span></span> <span data-ttu-id="15ca9-271">그러나 모든 작업에 대해 동일한 ID를 사용하기보다는 모든 작업에 고유한 요청 ID를 설정하는 것이 더 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-271">However, it is more useful to set a unique request ID for every operation rather than to use the same ID for all operations.</span></span> <span data-ttu-id="15ca9-272">이러한 이유로 `SearchServiceClient` 및 `SearchIndexClient`의 `SetClientRequestId` 메서드는 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-272">For this reason, the `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="15ca9-273">대신, `SearchRequestOptions` 매개 변수(선택 사항)를 통해 요청 ID를 각 작업 메서드에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-273">Instead, you can pass a request ID to each operation method via the optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="15ca9-274">SDK의 이후 릴리스에서는 다른 Azure SDK에서 사용하는 방법과 일치하는 클라이언트 개체에서 요청 ID를 전역적으로 설정하는 새 메커니즘을 추가할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-274">In a future release of the SDK, we will add a new mechanism for setting a request ID globally on the client objects that is consistent with the approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="15ca9-275">예</span><span class="sxs-lookup"><span data-stu-id="15ca9-275">Example</span></span>
<span data-ttu-id="15ca9-276">다음과 같은 코드가 있는 경우</span><span class="sxs-lookup"><span data-stu-id="15ca9-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="15ca9-277">빌드 오류를 수정하기 위해 다음으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-277">You can change it to this to fix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="15ca9-278">인터페이스 이름 변경</span><span class="sxs-lookup"><span data-stu-id="15ca9-278">Interface name changes</span></span>
<span data-ttu-id="15ca9-279">작업 그룹 인터페이스 이름이 해당 속성 이름과 일치하도록 모두 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-279">The operation group interface names have all changed to be consistent with their corresponding property names:</span></span>

* <span data-ttu-id="15ca9-280">`ISearchServiceClient.Indexes` 형식이 `IIndexOperations`에서 `IIndexesOperations`로 이름 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-280">The type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` to `IIndexesOperations`.</span></span>
* <span data-ttu-id="15ca9-281">`ISearchServiceClient.Indexers` 형식이 `IIndexerOperations`에서 `IIndexersOperations`로 이름 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-281">The type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` to `IIndexersOperations`.</span></span>
* <span data-ttu-id="15ca9-282">`ISearchServiceClient.DataSources` 형식이 `IDataSourceOperations`에서 `IDataSourcesOperations`로 이름 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-282">The type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` to `IDataSourcesOperations`.</span></span>
* <span data-ttu-id="15ca9-283">`ISearchIndexClient.Documents` 형식이 `IDocumentOperations`에서 `IDocumentsOperations`로 이름 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-283">The type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` to `IDocumentsOperations`.</span></span>

<span data-ttu-id="15ca9-284">이 변경은 테스트 용도로 모의 인터페이스를 만들지 않은 경우 코드에 영향을 줄 가능성은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-284">This change is unlikely to affect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="15ca9-285">1.1 버전의 버그 수정</span><span class="sxs-lookup"><span data-stu-id="15ca9-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="15ca9-286">이전 버전의 Azure 검색 .NET SDK에는 사용자 지정 모델 클래스의 serialization과 관련된 버그가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-286">There was a bug in older versions of the Azure Search .NET SDK relating to serialization of custom model classes.</span></span> <span data-ttu-id="15ca9-287">Null이 허용되지 않는 값 형식의 속성으로 사용자 지정 모델 클래스를 만든 경우 버그가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-287">The bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-to-reproduce"></a><span data-ttu-id="15ca9-288">재현 단계</span><span class="sxs-lookup"><span data-stu-id="15ca9-288">Steps to reproduce</span></span>
<span data-ttu-id="15ca9-289">Null이 허용되지 않는 값 형식의 속성으로 사용자 지정 모델 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="15ca9-290">예를 들어 `int?` 대신 `int` 형식의 공용 `UnitCount` 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="15ca9-291">해당 형식의 기본 값을 사용하여 문서를 인덱싱할 경우(예: `int`에 대해 0) 필드는 Azure 검색에서 Null이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-291">If you index a document with the default value of that type (for example, 0 for `int`), the field will be null in Azure Search.</span></span> <span data-ttu-id="15ca9-292">이후에 해당 문서를 검색하면 `Search` 호출은 `null`을 `int`로 변환할 수 없다는 `JsonSerializationException`을 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-292">If you subsequently search for that document, the `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` to `int`.</span></span>

<span data-ttu-id="15ca9-293">또한 Null이 의도한 값 대신 인덱스에 기록되었으므로 필터가 예상대로 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-293">Also, filters may not work as expected since null was written to the index instead of the intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="15ca9-294">수정 세부 정보</span><span class="sxs-lookup"><span data-stu-id="15ca9-294">Fix details</span></span>
<span data-ttu-id="15ca9-295">SDK 버전 1.1에서 이 문제를 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-295">We have fixed this issue in version 1.1 of the SDK.</span></span> <span data-ttu-id="15ca9-296">이제 다음과 같이 모델 클래스가 있고</span><span class="sxs-lookup"><span data-stu-id="15ca9-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="15ca9-297">`IntValue` 를 0으로 설정하면 네트워크에서 해당 값이 0으로 올바르게 직렬화되고 인덱스에 0으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-297">and you set `IntValue` to 0, that value is now correctly serialized as 0 on the wire and stored as 0 in the index.</span></span> <span data-ttu-id="15ca9-298">또한 왕복이 예상대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="15ca9-299">이 접근 방식에서 알고 있어야 하는 한 가지 잠재적인 문제가 있습니다. Null이 허용되지 않는 속성의 모델 형식을 사용하는 경우 인덱스의 문서가 해당 필드에 대해 Null 값을 포함하지 않음을 **보장**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-299">There is one potential issue to be aware of with this approach: If you use a model type with a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="15ca9-300">SDK와 Azure 검색 REST API 모두 이를 적용하는 데 활용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-300">Neither the SDK nor the Azure Search REST API will help you to enforce this.</span></span>

<span data-ttu-id="15ca9-301">이것은 가상의 문제가 아닙니다. `Edm.Int32` 형식인 기존 인덱스에 새 필드를 추가하는 시나리오를 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="15ca9-302">인덱스 정의를 업데이트한 후 모든 문서는 해당하는 새 필드에 대해 Null 값을 포함하게 됩니다(Azure 검색에서 모든 형식은 Null을 허용하기 때문).</span><span class="sxs-lookup"><span data-stu-id="15ca9-302">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="15ca9-303">그런 다음 해당 필드에 대해 Null이 허용되지 않는 `int` 속성으로 모델 클래스를 사용하는 경우 문서를 검색하려고 시도할 때 다음과 같은 `JsonSerializationException`이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="15ca9-304">이러한 이유로 모델 클래스에는 Null을 허용하는 형식을 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="15ca9-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="15ca9-305">이 버그 및 수정에 대한 자세한 내용은 [GitHub에서 해당 문제](https://github.com/Azure/azure-sdk-for-net/issues/1063)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ca9-305">For more details on this bug and the fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

