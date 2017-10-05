---
title: "예외 관리 - Microsoft 위협 모델링 도구 - Azure | Microsoft Docs"
description: "위협 모델링 도구에 노출되는 위협 해결 방법"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: bbf357b902474a1812eb7a5a2c914d0c8b91934b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="0ead2-103">보안 프레임: 예외 관리 | 해결 방법</span><span class="sxs-lookup"><span data-stu-id="0ead2-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="0ead2-104">제품/서비스</span><span class="sxs-lookup"><span data-stu-id="0ead2-104">Product/Service</span></span> | <span data-ttu-id="0ead2-105">문서</span><span class="sxs-lookup"><span data-stu-id="0ead2-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="0ead2-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="0ead2-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="0ead2-107">WCF - 구성 파일에 serviceDebug 노드를 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="0ead2-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="0ead2-108">WCF - 구성 파일에 serviceMetadata 노드를 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="0ead2-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="0ead2-109">**앱 API**</span><span class="sxs-lookup"><span data-stu-id="0ead2-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="0ead2-110">ASP.NET Web API에서 적절한 예외 처리가 수행되었는지 확인 </span><span class="sxs-lookup"><span data-stu-id="0ead2-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="0ead2-111">**웹 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="0ead2-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="0ead2-112">오류 메시지에 보안 정보를 노출하지 않음</span><span class="sxs-lookup"><span data-stu-id="0ead2-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="0ead2-113">기본 오류 처리 페이지 구현 </span><span class="sxs-lookup"><span data-stu-id="0ead2-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="0ead2-114">IIS에서 배포 방법을 일반 정품으로 설정</span><span class="sxs-lookup"><span data-stu-id="0ead2-114">Set Deployment Method to Retail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="0ead2-115">안전한 예외 실패</span><span class="sxs-lookup"><span data-stu-id="0ead2-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="0ead2-116"><a id="servicedebug"></a>WCF - 구성 파일에 serviceDebug 노드를 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="0ead2-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="0ead2-117">제목</span><span class="sxs-lookup"><span data-stu-id="0ead2-117">Title</span></span>                   | <span data-ttu-id="0ead2-118">세부 정보</span><span class="sxs-lookup"><span data-stu-id="0ead2-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="0ead2-119">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="0ead2-119">**Component**</span></span>               | <span data-ttu-id="0ead2-120">WCF</span><span class="sxs-lookup"><span data-stu-id="0ead2-120">WCF</span></span> | 
| <span data-ttu-id="0ead2-121">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="0ead2-121">**SDL Phase**</span></span>               | <span data-ttu-id="0ead2-122">빌드</span><span class="sxs-lookup"><span data-stu-id="0ead2-122">Build</span></span> |  
| <span data-ttu-id="0ead2-123">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="0ead2-123">**Applicable Technologies**</span></span> | <span data-ttu-id="0ead2-124">일반, .NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="0ead2-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="0ead2-125">**특성**</span><span class="sxs-lookup"><span data-stu-id="0ead2-125">**Attributes**</span></span>              | <span data-ttu-id="0ead2-126">해당 없음</span><span class="sxs-lookup"><span data-stu-id="0ead2-126">N/A</span></span>  |
| <span data-ttu-id="0ead2-127">**참조**</span><span class="sxs-lookup"><span data-stu-id="0ead2-127">**References**</span></span>              | <span data-ttu-id="0ead2-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify, 영국](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="0ead2-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="0ead2-129">**단계**</span><span class="sxs-lookup"><span data-stu-id="0ead2-129">**Steps**</span></span> | <span data-ttu-id="0ead2-130">WCF(Windows Communication Framework) 서비스는 디버깅 정보를 노출하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-130">Windows Communication Framework (WCF) services can be configured to expose debugging information.</span></span> <span data-ttu-id="0ead2-131">디버그 정보를 프로덕션 환경에서는 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="0ead2-132">`<serviceDebug>` 태그는 WCF 서비스에 대해 디버그 정보 기능이 사용되는지 여부를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-132">The `<serviceDebug>` tag defines whether the debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="0ead2-133">특성 includeExceptionDetailInFaults를 true로 설정하면 응용 프로그램에서 예외 정보가 클라이언트로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-133">If the attribute includeExceptionDetailInFaults is set to true, exception information from the application will be returned to clients.</span></span> <span data-ttu-id="0ead2-134">공격자는 디버깅 출력에서 얻은 추가 정보를 활용하여 프레임워크, 데이터베이스 또는 응용 프로그램이 사용하는 기타 리소스를 대상으로 공격을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-134">Attackers can leverage the additional information they gain from debugging output to mount attacks targeted on the framework, database, or other resources used by the application.</span></span> |

### <a name="example"></a><span data-ttu-id="0ead2-135">예제</span><span class="sxs-lookup"><span data-stu-id="0ead2-135">Example</span></span>
<span data-ttu-id="0ead2-136">다음 구성 파일에는 `<serviceDebug>` 태그가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-136">The following configuration file includes the `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="0ead2-137">서비스에서 디버깅 정보를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-137">Disable debugging information in the service.</span></span> <span data-ttu-id="0ead2-138">이 작업은 응용 프로그램 구성 파일에서 `<serviceDebug>` 태그를 제거하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-138">This can be accomplished by removing the `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="0ead2-139"><a id="servicemetadata"></a>WCF - 구성 파일에 serviceMetadata 노드를 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="0ead2-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="0ead2-140">제목</span><span class="sxs-lookup"><span data-stu-id="0ead2-140">Title</span></span>                   | <span data-ttu-id="0ead2-141">세부 정보</span><span class="sxs-lookup"><span data-stu-id="0ead2-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="0ead2-142">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="0ead2-142">**Component**</span></span>               | <span data-ttu-id="0ead2-143">WCF</span><span class="sxs-lookup"><span data-stu-id="0ead2-143">WCF</span></span> | 
| <span data-ttu-id="0ead2-144">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="0ead2-144">**SDL Phase**</span></span>               | <span data-ttu-id="0ead2-145">빌드</span><span class="sxs-lookup"><span data-stu-id="0ead2-145">Build</span></span> |  
| <span data-ttu-id="0ead2-146">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="0ead2-146">**Applicable Technologies**</span></span> | <span data-ttu-id="0ead2-147">일반</span><span class="sxs-lookup"><span data-stu-id="0ead2-147">Generic</span></span> |
| <span data-ttu-id="0ead2-148">**특성**</span><span class="sxs-lookup"><span data-stu-id="0ead2-148">**Attributes**</span></span>              | <span data-ttu-id="0ead2-149">일반, .NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="0ead2-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="0ead2-150">**참조**</span><span class="sxs-lookup"><span data-stu-id="0ead2-150">**References**</span></span>              | <span data-ttu-id="0ead2-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify, 영국](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="0ead2-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="0ead2-152">**단계**</span><span class="sxs-lookup"><span data-stu-id="0ead2-152">**Steps**</span></span> | <span data-ttu-id="0ead2-153">서비스에 대한 정보를 공개적으로 노출하면 공격자는 서비스를 악용하는 방법에 대한 중요한 아이디어를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit the service.</span></span> <span data-ttu-id="0ead2-154">`<serviceMetadata>` 태그는 메타데이터 게시 기능을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-154">The `<serviceMetadata>` tag enables the metadata publishing feature.</span></span> <span data-ttu-id="0ead2-155">서비스 메타데이터에는 공개적으로 액세스할 수 없게 해야 하는 중요한 정보가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="0ead2-156">적어도, 신뢰할 수 있는 사용자만 메타데이터에 액세스하도록 허용하고 불필요한 정보가 노출되지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-156">At a minimum, only allow trusted users to access the metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="0ead2-157">더 나아가 메타데이터를 게시하는 기능은 완전히 사용하지 않도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-157">Better yet, entirely disable the ability to publish metadata.</span></span> <span data-ttu-id="0ead2-158">안전한 WCF 구성에는 `<serviceMetadata>` 태그가 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-158">A safe WCF configuration will not contain the `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="0ead2-159"><a id="exception"></a>ASP.NET Web API에서 적절한 예외 처리가 수행되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="0ead2-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="0ead2-160">제목</span><span class="sxs-lookup"><span data-stu-id="0ead2-160">Title</span></span>                   | <span data-ttu-id="0ead2-161">세부 정보</span><span class="sxs-lookup"><span data-stu-id="0ead2-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="0ead2-162">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="0ead2-162">**Component**</span></span>               | <span data-ttu-id="0ead2-163">Web API</span><span class="sxs-lookup"><span data-stu-id="0ead2-163">Web API</span></span> | 
| <span data-ttu-id="0ead2-164">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="0ead2-164">**SDL Phase**</span></span>               | <span data-ttu-id="0ead2-165">빌드</span><span class="sxs-lookup"><span data-stu-id="0ead2-165">Build</span></span> |  
| <span data-ttu-id="0ead2-166">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="0ead2-166">**Applicable Technologies**</span></span> | <span data-ttu-id="0ead2-167">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="0ead2-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="0ead2-168">**특성**</span><span class="sxs-lookup"><span data-stu-id="0ead2-168">**Attributes**</span></span>              | <span data-ttu-id="0ead2-169">해당 없음</span><span class="sxs-lookup"><span data-stu-id="0ead2-169">N/A</span></span>  |
| <span data-ttu-id="0ead2-170">**참조**</span><span class="sxs-lookup"><span data-stu-id="0ead2-170">**References**</span></span>              | <span data-ttu-id="0ead2-171">[ASP.NET Web API에서 예외 처리](http://www.asp.net/web-api/overview/error-handling/exception-handling), [ASP.NET Web API의 모델 유효성 검사](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="0ead2-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="0ead2-172">**단계**</span><span class="sxs-lookup"><span data-stu-id="0ead2-172">**Steps**</span></span> | <span data-ttu-id="0ead2-173">기본적으로 ASP.NET Web API에서 확인할 수 없는 대부분의 예외는 `500, Internal Server Error` 상태 코드의 HTTP 응답으로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="0ead2-174">예제</span><span class="sxs-lookup"><span data-stu-id="0ead2-174">Example</span></span>
<span data-ttu-id="0ead2-175">API에서 반환되는 상태 코드를 제어하려면 아래와 같이 `HttpResponseException`을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-175">To control the status code returned by the API, `HttpResponseException` can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        throw new HttpResponseException(HttpStatusCode.NotFound);
    }
    return item;
}
```

### <a name="example"></a><span data-ttu-id="0ead2-176">예제</span><span class="sxs-lookup"><span data-stu-id="0ead2-176">Example</span></span>
<span data-ttu-id="0ead2-177">예외 응답을 추가적으로 제어하려면 아래와 같이 `HttpResponseMessage` 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-177">For further control on the exception response, the `HttpResponseMessage` class can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var resp = new HttpResponseMessage(HttpStatusCode.NotFound)
        {
            Content = new StringContent(string.Format("No product with ID = {0}", id)),
            ReasonPhrase = "Product ID Not Found"
        }
        throw new HttpResponseException(resp);
    }
    return item;
}
```
<span data-ttu-id="0ead2-178">`HttpResponseException` 형식이 아닌 처리되지 않은 예외를 catch하려면 예외 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-178">To catch unhandled exceptions that are not of the type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="0ead2-179">예외 필터는 `System.Web.Http.Filters.IExceptionFilter` 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-179">Exception filters implement the `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="0ead2-180">예외 필터를 작성하는 가장 간단한 방법은 `System.Web.Http.Filters.ExceptionFilterAttribute` 클래스에서 파생하고 OnException 메서드를 재정의하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-180">The simplest way to write an exception filter is to derive from the `System.Web.Http.Filters.ExceptionFilterAttribute` class and override the OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="0ead2-181">예제</span><span class="sxs-lookup"><span data-stu-id="0ead2-181">Example</span></span>
<span data-ttu-id="0ead2-182">다음은 `NotImplementedException`을 HTTP 상태 코드 `501, Not Implemented`로 변환하는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
```C#
namespace ProductStore.Filters
{
    using System;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http.Filters;

    public class NotImplExceptionFilterAttribute : ExceptionFilterAttribute 
    {
        public override void OnException(HttpActionExecutedContext context)
        {
            if (context.Exception is NotImplementedException)
            {
                context.Response = new HttpResponseMessage(HttpStatusCode.NotImplemented);
            }
        }
    }
}
```

<span data-ttu-id="0ead2-183">다음과 같은 여러 가지 방법으로 Web API 예외 필터를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-183">There are several ways to register a Web API exception filter:</span></span>
- <span data-ttu-id="0ead2-184">작업 기준</span><span class="sxs-lookup"><span data-stu-id="0ead2-184">By action</span></span>
- <span data-ttu-id="0ead2-185">컨트롤러 기준</span><span class="sxs-lookup"><span data-stu-id="0ead2-185">By controller</span></span>
- <span data-ttu-id="0ead2-186">전역적으로</span><span class="sxs-lookup"><span data-stu-id="0ead2-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="0ead2-187">예제</span><span class="sxs-lookup"><span data-stu-id="0ead2-187">Example</span></span>
<span data-ttu-id="0ead2-188">특정 작업에 필터를 적용하려면 필터를 작업에 특성으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-188">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span> 
```C#
public class ProductsController : ApiController
{
    [NotImplExceptionFilter]
    public Contact GetContact(int id)
    {
        throw new NotImplementedException("This method is not implemented");
    }
}
```
### <a name="example"></a><span data-ttu-id="0ead2-189">예제</span><span class="sxs-lookup"><span data-stu-id="0ead2-189">Example</span></span>
<span data-ttu-id="0ead2-190">`controller`의 모든 작업에 필터를 적용하려면 필터를 `controller` 클래스에 특성으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-190">To apply the filter to all of the actions on a `controller`, add the filter as an attribute to the `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="0ead2-191">예제</span><span class="sxs-lookup"><span data-stu-id="0ead2-191">Example</span></span>
<span data-ttu-id="0ead2-192">모든 Web API 컨트롤러에는 전역적으로 필터를 적용하려면 필터의 인스턴스를 `GlobalConfiguration.Configuration.Filters` 컬렉션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-192">To apply the filter globally to all Web API controllers, add an instance of the filter to the `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="0ead2-193">이 컬렉션의 예외 필터는 모든 Web API 컨트롤러 작업에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-193">Exception filters in this collection apply to any Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="0ead2-194">예제</span><span class="sxs-lookup"><span data-stu-id="0ead2-194">Example</span></span>
<span data-ttu-id="0ead2-195">모델 유효성 검사를 위해 모델 상태를 아래와 같이 CreateErrorResponse 메서드에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-195">For model validation, the model state can be passed to CreateErrorResponse method as shown below:</span></span> 
```C#
public HttpResponseMessage PostProduct(Product item)
{
    if (!ModelState.IsValid)
    {
        return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
    }
    // Implementation not shown...
}
```

<span data-ttu-id="0ead2-196">ASP.Net Web API에서 예외 처리 및 모델 유효성 검사에 대한 자세한 내용은 참조 섹션의 링크를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0ead2-196">Check the links in the references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="0ead2-197"><a id="messages"></a>오류 메시지에 보안 정보를 노출하지 않음</span><span class="sxs-lookup"><span data-stu-id="0ead2-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="0ead2-198">제목</span><span class="sxs-lookup"><span data-stu-id="0ead2-198">Title</span></span>                   | <span data-ttu-id="0ead2-199">세부 정보</span><span class="sxs-lookup"><span data-stu-id="0ead2-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="0ead2-200">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="0ead2-200">**Component**</span></span>               | <span data-ttu-id="0ead2-201">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="0ead2-201">Web Application</span></span> | 
| <span data-ttu-id="0ead2-202">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="0ead2-202">**SDL Phase**</span></span>               | <span data-ttu-id="0ead2-203">빌드</span><span class="sxs-lookup"><span data-stu-id="0ead2-203">Build</span></span> |  
| <span data-ttu-id="0ead2-204">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="0ead2-204">**Applicable Technologies**</span></span> | <span data-ttu-id="0ead2-205">일반</span><span class="sxs-lookup"><span data-stu-id="0ead2-205">Generic</span></span> |
| <span data-ttu-id="0ead2-206">**특성**</span><span class="sxs-lookup"><span data-stu-id="0ead2-206">**Attributes**</span></span>              | <span data-ttu-id="0ead2-207">해당 없음</span><span class="sxs-lookup"><span data-stu-id="0ead2-207">N/A</span></span>  |
| <span data-ttu-id="0ead2-208">**참조**</span><span class="sxs-lookup"><span data-stu-id="0ead2-208">**References**</span></span>              | <span data-ttu-id="0ead2-209">해당 없음</span><span class="sxs-lookup"><span data-stu-id="0ead2-209">N/A</span></span>  |
| <span data-ttu-id="0ead2-210">**단계**</span><span class="sxs-lookup"><span data-stu-id="0ead2-210">**Steps**</span></span> | <p><span data-ttu-id="0ead2-211">일반 오류 메시지는 중요한 응용 프로그램 데이터를 포함하지 않고 사용자에게 직접 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-211">Generic error messages are provided directly to the user without including sensitive application data.</span></span> <span data-ttu-id="0ead2-212">중요한 데이터의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="0ead2-213">서버 이름</span><span class="sxs-lookup"><span data-stu-id="0ead2-213">Server names</span></span></li><li><span data-ttu-id="0ead2-214">연결 문자열</span><span class="sxs-lookup"><span data-stu-id="0ead2-214">Connection strings</span></span></li><li><span data-ttu-id="0ead2-215">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="0ead2-215">Usernames</span></span></li><li><span data-ttu-id="0ead2-216">암호</span><span class="sxs-lookup"><span data-stu-id="0ead2-216">Passwords</span></span></li><li><span data-ttu-id="0ead2-217">SQL 프로시저</span><span class="sxs-lookup"><span data-stu-id="0ead2-217">SQL procedures</span></span></li><li><span data-ttu-id="0ead2-218">동적 SQL 오류의 세부 정보</span><span class="sxs-lookup"><span data-stu-id="0ead2-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="0ead2-219">스택 추적 및 코드 줄</span><span class="sxs-lookup"><span data-stu-id="0ead2-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="0ead2-220">메모리에 저장된 변수</span><span class="sxs-lookup"><span data-stu-id="0ead2-220">Variables stored in memory</span></span></li><li><span data-ttu-id="0ead2-221">드라이브 및 폴더 위치</span><span class="sxs-lookup"><span data-stu-id="0ead2-221">Drive and folder locations</span></span></li><li><span data-ttu-id="0ead2-222">응용 프로그램 설치 지점</span><span class="sxs-lookup"><span data-stu-id="0ead2-222">Application install points</span></span></li><li><span data-ttu-id="0ead2-223">호스트 구성 설정</span><span class="sxs-lookup"><span data-stu-id="0ead2-223">Host configuration settings</span></span></li><li><span data-ttu-id="0ead2-224">기타 내부 응용 프로그램 정보</span><span class="sxs-lookup"><span data-stu-id="0ead2-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="0ead2-225">응용 프로그램 내의 모든 오류를 트래핑하고 일반 오류 메시지를 제공할 뿐 아니라 IIS 내에서 사용자 지정 오류를 사용하도록 설정하면 정보가 공개되지 않도록 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="0ead2-226">다른 오류 처리 아키텍처 중에서 SQL Server Database 및 .NET 예외 처리는 사용자 응용 프로그램을 프로파일링하는 악의적인 사용자에게 특히 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful to a malicious user profiling your application.</span></span> <span data-ttu-id="0ead2-227">.NET 예외 클래스에서 파생된 클래스의 내용을 직접 표시하지 않도록 하고, 예기치 않은 예외가 사용자에게 실수로 직접 표시되지 않도록 적절한 예외 처리를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-227">Do not directly display the contents of a class derived from the .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly to the user.</span></span></p><ul><li><span data-ttu-id="0ead2-228">예외/오류 메시지에서 직접 확인되는 특정 세부 정보를 추상화하는 일반적인 오류 메시지를 사용자에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-228">Provide generic error messages directly to the user that abstract away specific details found directly in the exception/error message</span></span></li><li><span data-ttu-id="0ead2-229">.NET 예외 클래스의 내용을 사용자에게 직접 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-229">Do not display the contents of a .NET exception class directly to the user</span></span></li><li><span data-ttu-id="0ead2-230">모든 오류 메시지를 트래핑하고, 해당하는 경우 응용 프로그램 클라이언트에 전송된 일반 오류 메시지를 통해 사용자에게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-230">Trap all error messages and if appropriate inform the user via a generic error message sent to the application client</span></span></li><li><span data-ttu-id="0ead2-231">예외 클래스의 내용, 특히 `.ToString()`의 반환 값 또는 Message 또는 StackTrace 속성 값을 사용자에게 직접 공개하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-231">Do not expose the contents of the Exception class directly to the user, especially the return value from `.ToString()`, or the values of the Message or StackTrace properties.</span></span> <span data-ttu-id="0ead2-232">이 정보를 안전하게 기록하고 사용자에게는 좀 더 무해한 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-232">Securely log this information and display a more innocuous message to the user</span></span></li></ul>|

## <span data-ttu-id="0ead2-233"><a id="default"></a>기본 오류 처리 페이지 구현</span><span class="sxs-lookup"><span data-stu-id="0ead2-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="0ead2-234">제목</span><span class="sxs-lookup"><span data-stu-id="0ead2-234">Title</span></span>                   | <span data-ttu-id="0ead2-235">세부 정보</span><span class="sxs-lookup"><span data-stu-id="0ead2-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="0ead2-236">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="0ead2-236">**Component**</span></span>               | <span data-ttu-id="0ead2-237">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="0ead2-237">Web Application</span></span> | 
| <span data-ttu-id="0ead2-238">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="0ead2-238">**SDL Phase**</span></span>               | <span data-ttu-id="0ead2-239">빌드</span><span class="sxs-lookup"><span data-stu-id="0ead2-239">Build</span></span> |  
| <span data-ttu-id="0ead2-240">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="0ead2-240">**Applicable Technologies**</span></span> | <span data-ttu-id="0ead2-241">일반</span><span class="sxs-lookup"><span data-stu-id="0ead2-241">Generic</span></span> |
| <span data-ttu-id="0ead2-242">**특성**</span><span class="sxs-lookup"><span data-stu-id="0ead2-242">**Attributes**</span></span>              | <span data-ttu-id="0ead2-243">해당 없음</span><span class="sxs-lookup"><span data-stu-id="0ead2-243">N/A</span></span>  |
| <span data-ttu-id="0ead2-244">**참조**</span><span class="sxs-lookup"><span data-stu-id="0ead2-244">**References**</span></span>              | <span data-ttu-id="0ead2-245">[ASP.NET 오류 페이지 설정 대화 상자 편집](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="0ead2-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="0ead2-246">**단계**</span><span class="sxs-lookup"><span data-stu-id="0ead2-246">**Steps**</span></span> | <p><span data-ttu-id="0ead2-247">ASP.NET 응용 프로그램이 실패하고 HTTP/1.x 500 내부 서버 오류가 발생하거나 기능 구성(예: 요청 필터링)으로 인해 페이지가 표시되지 않을 경우 오류 메시지가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="0ead2-248">관리자는 응용 프로그램이 클라이언트에 자세한 오류 메시지를 표시할지 또는 localhost에만 자세한 오류 메시지를 표시할지를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-248">Administrators can choose whether or not the application should display a friendly message to the client, detailed error message to the client, or detailed error message to localhost only.</span></span> <span data-ttu-id="0ead2-249">web.config의 <customErrors> 태그는 다음 세 가지 모드로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-249">The <customErrors> tag in the web.config has three modes:</span></span></p><ul><li><span data-ttu-id="0ead2-250">**On:** 사용자 지정 오류가 사용되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="0ead2-251">defaultRedirect 특성을 지정하지 않으면 사용자에게 일반 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="0ead2-252">원격 클라이언트 및 로컬 호스트에 사용자 지정 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-252">The custom errors are shown to the remote clients and to the local host</span></span></li><li><span data-ttu-id="0ead2-253">**Off:** 사용자 지정 오류가 사용되지 않도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="0ead2-254">원격 클라이언트 및 로컬 호스트에 자세한 ASP.NET 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-254">The detailed ASP.NET errors are shown to the remote clients and to the local host</span></span></li><li><span data-ttu-id="0ead2-255">**RemoteOnly:** 사용자 지정 오류가 원격 클라이언트에만 표시되고 로컬 호스트에는 ASP.NET 오류가 표시되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-255">**RemoteOnly:** Specifies that custom errors are shown only to the remote clients, and that ASP.NET errors are shown to the local host.</span></span> <span data-ttu-id="0ead2-256">이것이 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-256">This is the default value</span></span></li></ul><p><span data-ttu-id="0ead2-257">응용 프로그램/사이트에 대한 `web.config` 파일을 열고 태그에 `<customErrors mode="RemoteOnly" />` 또는 `<customErrors mode="On" />`이 정의되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-257">Open the `web.config` file for the application/site and ensure that the tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="0ead2-258"><a id="deployment"></a>IIS에서 배포 방법을 일반 정품으로 설정</span><span class="sxs-lookup"><span data-stu-id="0ead2-258"><a id="deployment"></a>Set Deployment Method to Retail in IIS</span></span>

| <span data-ttu-id="0ead2-259">제목</span><span class="sxs-lookup"><span data-stu-id="0ead2-259">Title</span></span>                   | <span data-ttu-id="0ead2-260">세부 정보</span><span class="sxs-lookup"><span data-stu-id="0ead2-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="0ead2-261">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="0ead2-261">**Component**</span></span>               | <span data-ttu-id="0ead2-262">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="0ead2-262">Web Application</span></span> | 
| <span data-ttu-id="0ead2-263">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="0ead2-263">**SDL Phase**</span></span>               | <span data-ttu-id="0ead2-264">배포</span><span class="sxs-lookup"><span data-stu-id="0ead2-264">Deployment</span></span> |  
| <span data-ttu-id="0ead2-265">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="0ead2-265">**Applicable Technologies**</span></span> | <span data-ttu-id="0ead2-266">일반</span><span class="sxs-lookup"><span data-stu-id="0ead2-266">Generic</span></span> |
| <span data-ttu-id="0ead2-267">**특성**</span><span class="sxs-lookup"><span data-stu-id="0ead2-267">**Attributes**</span></span>              | <span data-ttu-id="0ead2-268">해당 없음</span><span class="sxs-lookup"><span data-stu-id="0ead2-268">N/A</span></span>  |
| <span data-ttu-id="0ead2-269">**참조**</span><span class="sxs-lookup"><span data-stu-id="0ead2-269">**References**</span></span>              | <span data-ttu-id="0ead2-270">[배포 요소(ASP.NET 설정 스키마)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="0ead2-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="0ead2-271">**단계**</span><span class="sxs-lookup"><span data-stu-id="0ead2-271">**Steps**</span></span> | <p><span data-ttu-id="0ead2-272">`<deployment retail>` 스위치는 프로덕션 IIS 서버에서 사용되도록 고안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-272">The `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="0ead2-273">이 스위치는 응용 프로그램이 페이지에서 추적 출력을 생성하는 기능을 사용하지 않도록 설정하고, 최종 사용자에게 자세한 오류 메시지를 표시하는 기능을 사용하지 않도록 설정하고, 디버그 스위치를 사용하지 않도록 설정하여 성능을 최대화하고 보안 정보 노출을 최소화하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-273">This switch is used to help applications run with the best possible performance and least possible security information leakages by disabling the application's ability to generate trace output on a page, disabling the ability to display detailed error messages to end users, and disabling the debug switch.</span></span></p><p><span data-ttu-id="0ead2-274">종종 활성 개발 중에 실패한 요청 추적 및 디버그와 같은 개발자 중심의 스위치 및 옵션이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="0ead2-275">프로덕션 서버의 배포 방법을 일반 정품으로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-275">It is recommended that the deployment method on any production server be set to retail.</span></span> <span data-ttu-id="0ead2-276">machine.config 파일을 열고 `<deployment retail="true" />`을 true 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-276">open the machine.config file and ensure that `<deployment retail="true" />` remains set to true.</span></span></p>|

## <span data-ttu-id="0ead2-277"><a id="fail"></a>안전한 예외 실패</span><span class="sxs-lookup"><span data-stu-id="0ead2-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="0ead2-278">제목</span><span class="sxs-lookup"><span data-stu-id="0ead2-278">Title</span></span>                   | <span data-ttu-id="0ead2-279">세부 정보</span><span class="sxs-lookup"><span data-stu-id="0ead2-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="0ead2-280">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="0ead2-280">**Component**</span></span>               | <span data-ttu-id="0ead2-281">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="0ead2-281">Web Application</span></span> | 
| <span data-ttu-id="0ead2-282">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="0ead2-282">**SDL Phase**</span></span>               | <span data-ttu-id="0ead2-283">빌드</span><span class="sxs-lookup"><span data-stu-id="0ead2-283">Build</span></span> |  
| <span data-ttu-id="0ead2-284">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="0ead2-284">**Applicable Technologies**</span></span> | <span data-ttu-id="0ead2-285">일반</span><span class="sxs-lookup"><span data-stu-id="0ead2-285">Generic</span></span> |
| <span data-ttu-id="0ead2-286">**특성**</span><span class="sxs-lookup"><span data-stu-id="0ead2-286">**Attributes**</span></span>              | <span data-ttu-id="0ead2-287">해당 없음</span><span class="sxs-lookup"><span data-stu-id="0ead2-287">N/A</span></span>  |
| <span data-ttu-id="0ead2-288">**참조**</span><span class="sxs-lookup"><span data-stu-id="0ead2-288">**References**</span></span>              | [<span data-ttu-id="0ead2-289">안전하게 실패</span><span class="sxs-lookup"><span data-stu-id="0ead2-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="0ead2-290">**단계**</span><span class="sxs-lookup"><span data-stu-id="0ead2-290">**Steps**</span></span> | <span data-ttu-id="0ead2-291">응용 프로그램은 안전하게 실패해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-291">Application should fail safely.</span></span> <span data-ttu-id="0ead2-292">수행되는 특정 결정에 따라 부울 값을 반환하는 모든 메서드는 신중하게 예외 블록을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="0ead2-293">부주의하게 예외 블록이 작성되면 보안 문제로 인한 논리적 오류가 많이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-293">There are lot of logical errors due to which security issues creep in, when the exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="0ead2-294">예제</span><span class="sxs-lookup"><span data-stu-id="0ead2-294">Example</span></span>
```C#
        public static bool ValidateDomain(string pathToValidate, Uri currentUrl)
        {
            try
            {
                if (!string.IsNullOrWhiteSpace(pathToValidate))
                {
                    var domain = RetrieveDomain(currentUrl);
                    var replyPath = new Uri(pathToValidate);
                    var replyDomain = RetrieveDomain(replyPath);

                    if (string.Compare(domain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                    {
                        //// Adding additional check to enable CMS urls if they are not hosted on same domain.
                        if (!string.IsNullOrWhiteSpace(Utilities.CmsBase))
                        {
                            var cmsDomain = RetrieveDomain(new Uri(Utilities.Base.Trim()));
                            if (string.Compare(cmDomain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                            {
                                return false;
                            }
                            else
                            {
                                return true;
                            }
                        }

                        return false;
                    }
                }

                return true;
            }
            catch (UriFormatException ex)
            {
                LogHelper.LogException("Utilities:ValidateDomain", ex);
                return true;
            }
        }
```
<span data-ttu-id="0ead2-295">예외가 발생하면 항상 위 메서드는 True를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-295">The above method will always return True, if some exception happens.</span></span> <span data-ttu-id="0ead2-296">최종 사용자가 잘못된 형식의 URL을 제공할 경우 브라우저는 이를 유지하지만 `Uri()` 생성자는 그렇지 않을 경우 예외가 throw되며 사용자는 유효하지만 형식이 잘못된 URL을 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ead2-296">If the end user provides a malformed URL, that the browser respects, but the `Uri()` constructor doesn't, this will throw an exception, and the victim will be taken to the valid but malformed URL.</span></span> 