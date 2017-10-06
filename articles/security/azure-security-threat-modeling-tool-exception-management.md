---
title: "Azure 관리-Microsoft 위협 모델링 도구-aaaException | Microsoft Docs"
description: "hello 위협 모델링 도구에에서 노출 위협에 대 한 완화"
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
ms.openlocfilehash: 247096c10deeca94ebb9b19df7ba60e442ca1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="c0bc9-103">보안 프레임: 예외 관리 | 해결 방법</span><span class="sxs-lookup"><span data-stu-id="c0bc9-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="c0bc9-104">제품/서비스</span><span class="sxs-lookup"><span data-stu-id="c0bc9-104">Product/Service</span></span> | <span data-ttu-id="c0bc9-105">문서</span><span class="sxs-lookup"><span data-stu-id="c0bc9-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="c0bc9-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="c0bc9-107">WCF - 구성 파일에 serviceDebug 노드를 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="c0bc9-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="c0bc9-108">WCF - 구성 파일에 serviceMetadata 노드를 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="c0bc9-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="c0bc9-109">**앱 API**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="c0bc9-110">ASP.NET Web API에서 적절한 예외 처리가 수행되었는지 확인 </span><span class="sxs-lookup"><span data-stu-id="c0bc9-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="c0bc9-111">**웹 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="c0bc9-112">오류 메시지에 보안 정보를 노출하지 않음</span><span class="sxs-lookup"><span data-stu-id="c0bc9-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="c0bc9-113">기본 오류 처리 페이지 구현 </span><span class="sxs-lookup"><span data-stu-id="c0bc9-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="c0bc9-114">IIS의 배포 방법을 tooRetail 설정</span><span class="sxs-lookup"><span data-stu-id="c0bc9-114">Set Deployment Method tooRetail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="c0bc9-115">안전한 예외 실패</span><span class="sxs-lookup"><span data-stu-id="c0bc9-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="c0bc9-116"><a id="servicedebug"></a>WCF - 구성 파일에 serviceDebug 노드를 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="c0bc9-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="c0bc9-117">제목</span><span class="sxs-lookup"><span data-stu-id="c0bc9-117">Title</span></span>                   | <span data-ttu-id="c0bc9-118">세부 정보</span><span class="sxs-lookup"><span data-stu-id="c0bc9-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0bc9-119">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-119">**Component**</span></span>               | <span data-ttu-id="c0bc9-120">WCF</span><span class="sxs-lookup"><span data-stu-id="c0bc9-120">WCF</span></span> | 
| <span data-ttu-id="c0bc9-121">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-121">**SDL Phase**</span></span>               | <span data-ttu-id="c0bc9-122">빌드</span><span class="sxs-lookup"><span data-stu-id="c0bc9-122">Build</span></span> |  
| <span data-ttu-id="c0bc9-123">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-123">**Applicable Technologies**</span></span> | <span data-ttu-id="c0bc9-124">일반, .NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="c0bc9-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="c0bc9-125">**특성**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-125">**Attributes**</span></span>              | <span data-ttu-id="c0bc9-126">해당 없음</span><span class="sxs-lookup"><span data-stu-id="c0bc9-126">N/A</span></span>  |
| <span data-ttu-id="c0bc9-127">**참조**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-127">**References**</span></span>              | <span data-ttu-id="c0bc9-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify, 영국](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="c0bc9-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="c0bc9-129">**단계**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-129">**Steps**</span></span> | <span data-ttu-id="c0bc9-130">Windows Communication Framework (WCF) 서비스 구성된 tooexpose 디버깅 정보를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-130">Windows Communication Framework (WCF) services can be configured tooexpose debugging information.</span></span> <span data-ttu-id="c0bc9-131">디버그 정보를 프로덕션 환경에서는 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="c0bc9-132">hello `<serviceDebug>` 태그는 WCF 서비스에 대 한 hello 디버그 정보 기능이 활성화 되어 있는지를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-132">hello `<serviceDebug>` tag defines whether hello debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="c0bc9-133">Hello 특성 includeExceptionDetailInFaults tootrue 설정 되 면 hello 응용 프로그램에서 예외 정보 tooclients를 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-133">If hello attribute includeExceptionDetailInFaults is set tootrue, exception information from hello application will be returned tooclients.</span></span> <span data-ttu-id="c0bc9-134">공격자가 디버깅 출력 toomount 대상에 대 한 공격 hello 프레임 워크, 데이터베이스 또는 hello 응용 프로그램에서 사용 하는 다른 리소스에서 얻습니다 hello 추가 정보를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-134">Attackers can leverage hello additional information they gain from debugging output toomount attacks targeted on hello framework, database, or other resources used by hello application.</span></span> |

### <a name="example"></a><span data-ttu-id="c0bc9-135">예제</span><span class="sxs-lookup"><span data-stu-id="c0bc9-135">Example</span></span>
<span data-ttu-id="c0bc9-136">hello 다음 구성 파일에는 hello `<serviceDebug>` 태그:</span><span class="sxs-lookup"><span data-stu-id="c0bc9-136">hello following configuration file includes hello `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="c0bc9-137">Hello 서비스의 디버깅 정보를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-137">Disable debugging information in hello service.</span></span> <span data-ttu-id="c0bc9-138">Hello를 제거 하 여이 작업을 수행할 수 수 `<serviceDebug>` 응용 프로그램 구성 파일에서 이러한 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-138">This can be accomplished by removing hello `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="c0bc9-139"><a id="servicemetadata"></a>WCF - 구성 파일에 serviceMetadata 노드를 포함하지 않음</span><span class="sxs-lookup"><span data-stu-id="c0bc9-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="c0bc9-140">제목</span><span class="sxs-lookup"><span data-stu-id="c0bc9-140">Title</span></span>                   | <span data-ttu-id="c0bc9-141">세부 정보</span><span class="sxs-lookup"><span data-stu-id="c0bc9-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0bc9-142">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-142">**Component**</span></span>               | <span data-ttu-id="c0bc9-143">WCF</span><span class="sxs-lookup"><span data-stu-id="c0bc9-143">WCF</span></span> | 
| <span data-ttu-id="c0bc9-144">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-144">**SDL Phase**</span></span>               | <span data-ttu-id="c0bc9-145">빌드</span><span class="sxs-lookup"><span data-stu-id="c0bc9-145">Build</span></span> |  
| <span data-ttu-id="c0bc9-146">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-146">**Applicable Technologies**</span></span> | <span data-ttu-id="c0bc9-147">일반</span><span class="sxs-lookup"><span data-stu-id="c0bc9-147">Generic</span></span> |
| <span data-ttu-id="c0bc9-148">**특성**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-148">**Attributes**</span></span>              | <span data-ttu-id="c0bc9-149">일반, .NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="c0bc9-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="c0bc9-150">**참조**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-150">**References**</span></span>              | <span data-ttu-id="c0bc9-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify, 영국](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="c0bc9-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="c0bc9-152">**단계**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-152">**Steps**</span></span> | <span data-ttu-id="c0bc9-153">서비스에 대 한 정보를 공개적으로 노출 공격자가 어떻게 hello 서비스 악용할 수에 대 한 중요 한 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit hello service.</span></span> <span data-ttu-id="c0bc9-154">hello `<serviceMetadata>` 태그 hello 메타 데이터 게시 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-154">hello `<serviceMetadata>` tag enables hello metadata publishing feature.</span></span> <span data-ttu-id="c0bc9-155">서비스 메타데이터에는 공개적으로 액세스할 수 없게 해야 하는 중요한 정보가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="c0bc9-156">여기에 최소한 tooaccess hello 메타 데이터 및 불필요 한 정보가 노출 되지 않도록 신뢰할 수 있는 사용자만 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-156">At a minimum, only allow trusted users tooaccess hello metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="c0bc9-157">더 좋은 방법은 hello 기능 toopublish 메타 데이터를 완전히 비활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-157">Better yet, entirely disable hello ability toopublish metadata.</span></span> <span data-ttu-id="c0bc9-158">안전 WCF 구성 hello 포함 되지 것입니다 `<serviceMetadata>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-158">A safe WCF configuration will not contain hello `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="c0bc9-159"><a id="exception"></a>ASP.NET Web API에서 적절한 예외 처리가 수행되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="c0bc9-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="c0bc9-160">제목</span><span class="sxs-lookup"><span data-stu-id="c0bc9-160">Title</span></span>                   | <span data-ttu-id="c0bc9-161">세부 정보</span><span class="sxs-lookup"><span data-stu-id="c0bc9-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0bc9-162">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-162">**Component**</span></span>               | <span data-ttu-id="c0bc9-163">Web API</span><span class="sxs-lookup"><span data-stu-id="c0bc9-163">Web API</span></span> | 
| <span data-ttu-id="c0bc9-164">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-164">**SDL Phase**</span></span>               | <span data-ttu-id="c0bc9-165">빌드</span><span class="sxs-lookup"><span data-stu-id="c0bc9-165">Build</span></span> |  
| <span data-ttu-id="c0bc9-166">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-166">**Applicable Technologies**</span></span> | <span data-ttu-id="c0bc9-167">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="c0bc9-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="c0bc9-168">**특성**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-168">**Attributes**</span></span>              | <span data-ttu-id="c0bc9-169">해당 없음</span><span class="sxs-lookup"><span data-stu-id="c0bc9-169">N/A</span></span>  |
| <span data-ttu-id="c0bc9-170">**참조**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-170">**References**</span></span>              | <span data-ttu-id="c0bc9-171">[ASP.NET Web API에서 예외 처리](http://www.asp.net/web-api/overview/error-handling/exception-handling), [ASP.NET Web API의 모델 유효성 검사](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="c0bc9-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="c0bc9-172">**단계**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-172">**Steps**</span></span> | <span data-ttu-id="c0bc9-173">기본적으로 ASP.NET Web API에서 확인할 수 없는 대부분의 예외는 `500, Internal Server Error` 상태 코드의 HTTP 응답으로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="c0bc9-174">예제</span><span class="sxs-lookup"><span data-stu-id="c0bc9-174">Example</span></span>
<span data-ttu-id="c0bc9-175">hello API에서 반환 된 toocontrol hello 상태 코드 `HttpResponseException` 아래와 같이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-175">toocontrol hello status code returned by hello API, `HttpResponseException` can be used as shown below:</span></span> 
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

### <a name="example"></a><span data-ttu-id="c0bc9-176">예제</span><span class="sxs-lookup"><span data-stu-id="c0bc9-176">Example</span></span>
<span data-ttu-id="c0bc9-177">Hello 예외 응답에 보다 세부적인 제어에 대 한 hello `HttpResponseMessage` 아래와 같이 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-177">For further control on hello exception response, hello `HttpResponseMessage` class can be used as shown below:</span></span> 
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
<span data-ttu-id="c0bc9-178">처리 되지 않은 hello 형식의 되지 않는 예외 toocatch `HttpResponseException`, 예외 필터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-178">toocatch unhandled exceptions that are not of hello type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="c0bc9-179">예외 필터 구현 hello `System.Web.Http.Filters.IExceptionFilter` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-179">Exception filters implement hello `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="c0bc9-180">hello 가장 간단한 방법은 toowrite 예외 필터는 hello에서 tooderive `System.Web.Http.Filters.ExceptionFilterAttribute` 클래스 및 hello OnException 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-180">hello simplest way toowrite an exception filter is tooderive from hello `System.Web.Http.Filters.ExceptionFilterAttribute` class and override hello OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="c0bc9-181">예제</span><span class="sxs-lookup"><span data-stu-id="c0bc9-181">Example</span></span>
<span data-ttu-id="c0bc9-182">다음은 `NotImplementedException`을 HTTP 상태 코드 `501, Not Implemented`로 변환하는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
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

<span data-ttu-id="c0bc9-183">여러 가지 방법으로 tooregister 웹 API 예외 필터는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-183">There are several ways tooregister a Web API exception filter:</span></span>
- <span data-ttu-id="c0bc9-184">작업 기준</span><span class="sxs-lookup"><span data-stu-id="c0bc9-184">By action</span></span>
- <span data-ttu-id="c0bc9-185">컨트롤러 기준</span><span class="sxs-lookup"><span data-stu-id="c0bc9-185">By controller</span></span>
- <span data-ttu-id="c0bc9-186">전역적으로</span><span class="sxs-lookup"><span data-stu-id="c0bc9-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="c0bc9-187">예제</span><span class="sxs-lookup"><span data-stu-id="c0bc9-187">Example</span></span>
<span data-ttu-id="c0bc9-188">tooapply hello 필터 tooa 특정 작업, hello 필터 특성 toohello 액션으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-188">tooapply hello filter tooa specific action, add hello filter as an attribute toohello action:</span></span> 
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
### <a name="example"></a><span data-ttu-id="c0bc9-189">예제</span><span class="sxs-lookup"><span data-stu-id="c0bc9-189">Example</span></span>
<span data-ttu-id="c0bc9-190">hello에 대 한 동작 tooapply hello 필터 tooall는 `controller`, 특성 toohello로 hello 필터 추가 `controller` 클래스:</span><span class="sxs-lookup"><span data-stu-id="c0bc9-190">tooapply hello filter tooall of hello actions on a `controller`, add hello filter as an attribute toohello `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="c0bc9-191">예제</span><span class="sxs-lookup"><span data-stu-id="c0bc9-191">Example</span></span>
<span data-ttu-id="c0bc9-192">tooapply hello tooall Web API 컨트롤러 필터링 전체적으로, hello 필터 toohello의 인스턴스를 추가 `GlobalConfiguration.Configuration.Filters` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-192">tooapply hello filter globally tooall Web API controllers, add an instance of hello filter toohello `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="c0bc9-193">이 컬렉션의 예외 필터 tooany Web API 컨트롤러 작업을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-193">Exception filters in this collection apply tooany Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="c0bc9-194">예제</span><span class="sxs-lookup"><span data-stu-id="c0bc9-194">Example</span></span>
<span data-ttu-id="c0bc9-195">모델 유효성 검사에 대 한 hello 모델 상태 tooCreateErrorResponse 메서드 아래와 같이 전달 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-195">For model validation, hello model state can be passed tooCreateErrorResponse method as shown below:</span></span> 
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

<span data-ttu-id="c0bc9-196">예외 처리에 대 한 자세한 내용은 hello references 섹션에 hello 링크와 ASP.Net Web API에서 모델 유효성 검사를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-196">Check hello links in hello references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="c0bc9-197"><a id="messages"></a>오류 메시지에 보안 정보를 노출하지 않음</span><span class="sxs-lookup"><span data-stu-id="c0bc9-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="c0bc9-198">제목</span><span class="sxs-lookup"><span data-stu-id="c0bc9-198">Title</span></span>                   | <span data-ttu-id="c0bc9-199">세부 정보</span><span class="sxs-lookup"><span data-stu-id="c0bc9-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0bc9-200">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-200">**Component**</span></span>               | <span data-ttu-id="c0bc9-201">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c0bc9-201">Web Application</span></span> | 
| <span data-ttu-id="c0bc9-202">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-202">**SDL Phase**</span></span>               | <span data-ttu-id="c0bc9-203">빌드</span><span class="sxs-lookup"><span data-stu-id="c0bc9-203">Build</span></span> |  
| <span data-ttu-id="c0bc9-204">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-204">**Applicable Technologies**</span></span> | <span data-ttu-id="c0bc9-205">일반</span><span class="sxs-lookup"><span data-stu-id="c0bc9-205">Generic</span></span> |
| <span data-ttu-id="c0bc9-206">**특성**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-206">**Attributes**</span></span>              | <span data-ttu-id="c0bc9-207">해당 없음</span><span class="sxs-lookup"><span data-stu-id="c0bc9-207">N/A</span></span>  |
| <span data-ttu-id="c0bc9-208">**참조**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-208">**References**</span></span>              | <span data-ttu-id="c0bc9-209">해당 없음</span><span class="sxs-lookup"><span data-stu-id="c0bc9-209">N/A</span></span>  |
| <span data-ttu-id="c0bc9-210">**단계**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-210">**Steps**</span></span> | <p><span data-ttu-id="c0bc9-211">일반 오류 메시지가 제공 되며 직접 toohello 사용자 중요 한 응용 프로그램 데이터를 포함 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-211">Generic error messages are provided directly toohello user without including sensitive application data.</span></span> <span data-ttu-id="c0bc9-212">중요한 데이터의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="c0bc9-213">서버 이름</span><span class="sxs-lookup"><span data-stu-id="c0bc9-213">Server names</span></span></li><li><span data-ttu-id="c0bc9-214">연결 문자열</span><span class="sxs-lookup"><span data-stu-id="c0bc9-214">Connection strings</span></span></li><li><span data-ttu-id="c0bc9-215">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="c0bc9-215">Usernames</span></span></li><li><span data-ttu-id="c0bc9-216">암호</span><span class="sxs-lookup"><span data-stu-id="c0bc9-216">Passwords</span></span></li><li><span data-ttu-id="c0bc9-217">SQL 프로시저</span><span class="sxs-lookup"><span data-stu-id="c0bc9-217">SQL procedures</span></span></li><li><span data-ttu-id="c0bc9-218">동적 SQL 오류의 세부 정보</span><span class="sxs-lookup"><span data-stu-id="c0bc9-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="c0bc9-219">스택 추적 및 코드 줄</span><span class="sxs-lookup"><span data-stu-id="c0bc9-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="c0bc9-220">메모리에 저장된 변수</span><span class="sxs-lookup"><span data-stu-id="c0bc9-220">Variables stored in memory</span></span></li><li><span data-ttu-id="c0bc9-221">드라이브 및 폴더 위치</span><span class="sxs-lookup"><span data-stu-id="c0bc9-221">Drive and folder locations</span></span></li><li><span data-ttu-id="c0bc9-222">응용 프로그램 설치 지점</span><span class="sxs-lookup"><span data-stu-id="c0bc9-222">Application install points</span></span></li><li><span data-ttu-id="c0bc9-223">호스트 구성 설정</span><span class="sxs-lookup"><span data-stu-id="c0bc9-223">Host configuration settings</span></span></li><li><span data-ttu-id="c0bc9-224">기타 내부 응용 프로그램 정보</span><span class="sxs-lookup"><span data-stu-id="c0bc9-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="c0bc9-225">응용 프로그램 내의 모든 오류를 트래핑하고 일반 오류 메시지를 제공할 뿐 아니라 IIS 내에서 사용자 지정 오류를 사용하도록 설정하면 정보가 공개되지 않도록 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="c0bc9-226">SQL Server 데이터베이스 및.NET 예외 처리, 다른 오류 아키텍처, 처리 중 특히 자세한 정보 및 매우 유용한 tooa 악의적인 사용자가 응용 프로그램 프로 파일링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful tooa malicious user profiling your application.</span></span> <span data-ttu-id="c0bc9-227">클래스의 내용을 hello.NET 예외 클래스에서 파생 되며 예기치 않은 예외가 실수로 되지 않도록 적합 한 예외 처리 있는지 확인 하는 디스플레이 hello 발생 하는 직접 toohello 사용자 직접 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-227">Do not directly display hello contents of a class derived from hello .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly toohello user.</span></span></p><ul><li><span data-ttu-id="c0bc9-228">일반 오류 메시지를 직접 toohello 사용자 hello 예외/오류 메시지에서 직접 찾을 트래버스하여 특정 세부 정보를 추상화를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-228">Provide generic error messages directly toohello user that abstract away specific details found directly in hello exception/error message</span></span></li><li><span data-ttu-id="c0bc9-229">수행 하지 표시 hello 내용의.NET 예외 클래스를 직접 toohello 사용자</span><span class="sxs-lookup"><span data-stu-id="c0bc9-229">Do not display hello contents of a .NET exception class directly toohello user</span></span></li><li><span data-ttu-id="c0bc9-230">모든 오류 메시지를 트래핑 하 고 해당 하는 경우 일반 오류 메시지 보낸된 toohello 응용 프로그램 클라이언트를 통해 hello 사용자에 게 알리는</span><span class="sxs-lookup"><span data-stu-id="c0bc9-230">Trap all error messages and if appropriate inform hello user via a generic error message sent toohello application client</span></span></li><li><span data-ttu-id="c0bc9-231">Toohello 사용자 hello 특히 반환 값을 직접 hello 내용의 hello 예외 클래스를 노출 하지 않는 `.ToString()`, 또는 hello hello 메시지, 스택 추적 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-231">Do not expose hello contents of hello Exception class directly toohello user, especially hello return value from `.ToString()`, or hello values of hello Message or StackTrace properties.</span></span> <span data-ttu-id="c0bc9-232">안전 하 게이 정보를 기록 하 고 더 무해 메시지 toohello 사용자 표시</span><span class="sxs-lookup"><span data-stu-id="c0bc9-232">Securely log this information and display a more innocuous message toohello user</span></span></li></ul>|

## <span data-ttu-id="c0bc9-233"><a id="default"></a>기본 오류 처리 페이지 구현</span><span class="sxs-lookup"><span data-stu-id="c0bc9-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="c0bc9-234">제목</span><span class="sxs-lookup"><span data-stu-id="c0bc9-234">Title</span></span>                   | <span data-ttu-id="c0bc9-235">세부 정보</span><span class="sxs-lookup"><span data-stu-id="c0bc9-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0bc9-236">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-236">**Component**</span></span>               | <span data-ttu-id="c0bc9-237">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c0bc9-237">Web Application</span></span> | 
| <span data-ttu-id="c0bc9-238">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-238">**SDL Phase**</span></span>               | <span data-ttu-id="c0bc9-239">빌드</span><span class="sxs-lookup"><span data-stu-id="c0bc9-239">Build</span></span> |  
| <span data-ttu-id="c0bc9-240">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-240">**Applicable Technologies**</span></span> | <span data-ttu-id="c0bc9-241">일반</span><span class="sxs-lookup"><span data-stu-id="c0bc9-241">Generic</span></span> |
| <span data-ttu-id="c0bc9-242">**특성**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-242">**Attributes**</span></span>              | <span data-ttu-id="c0bc9-243">해당 없음</span><span class="sxs-lookup"><span data-stu-id="c0bc9-243">N/A</span></span>  |
| <span data-ttu-id="c0bc9-244">**참조**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-244">**References**</span></span>              | <span data-ttu-id="c0bc9-245">[ASP.NET 오류 페이지 설정 대화 상자 편집](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="c0bc9-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="c0bc9-246">**단계**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-246">**Steps**</span></span> | <p><span data-ttu-id="c0bc9-247">ASP.NET 응용 프로그램이 실패하고 HTTP/1.x 500 내부 서버 오류가 발생하거나 기능 구성(예: 요청 필터링)으로 인해 페이지가 표시되지 않을 경우 오류 메시지가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="c0bc9-248">관리자 친숙 한 메시지 toohello 클라이언트, 상세한 오류 메시지 toohello 클라이언트 또는 자세한 오류 메시지 toolocalhost만 hello 응용 프로그램을 표시할지 여부를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-248">Administrators can choose whether or not hello application should display a friendly message toohello client, detailed error message toohello client, or detailed error message toolocalhost only.</span></span> <span data-ttu-id="c0bc9-249">hello <customErrors> hello web.config의 태그는 세 가지 모드:</span><span class="sxs-lookup"><span data-stu-id="c0bc9-249">hello <customErrors> tag in hello web.config has three modes:</span></span></p><ul><li><span data-ttu-id="c0bc9-250">**On:** 사용자 지정 오류가 사용되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="c0bc9-251">defaultRedirect 특성을 지정하지 않으면 사용자에게 일반 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="c0bc9-252">toohello 원격 클라이언트 및 로컬 호스트 toohello hello 사용자 지정 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-252">hello custom errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="c0bc9-253">**Off:** 사용자 지정 오류가 사용되지 않도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="c0bc9-254">hello 자세한 ASP.NET 오류가 표시 됩니다 toohello 원격 클라이언트와 toohello 로컬 호스트</span><span class="sxs-lookup"><span data-stu-id="c0bc9-254">hello detailed ASP.NET errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="c0bc9-255">**RemoteOnly:** 지정 ASP.NET 오류는 toohello 로컬 호스트를 표시 하 고는 사용자 지정 오류만 toohello 원격 클라이언트에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-255">**RemoteOnly:** Specifies that custom errors are shown only toohello remote clients, and that ASP.NET errors are shown toohello local host.</span></span> <span data-ttu-id="c0bc9-256">이 hello 기본값</span><span class="sxs-lookup"><span data-stu-id="c0bc9-256">This is hello default value</span></span></li></ul><p><span data-ttu-id="c0bc9-257">열기 hello `web.config` hello 응용 프로그램/사이트에 대 한 파일을 hello 태그 중 하나에 있는지 확인 `<customErrors mode="RemoteOnly" />` 또는 `<customErrors mode="On" />` 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-257">Open hello `web.config` file for hello application/site and ensure that hello tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="c0bc9-258"><a id="deployment"></a>IIS의 배포 방법을 tooRetail 설정</span><span class="sxs-lookup"><span data-stu-id="c0bc9-258"><a id="deployment"></a>Set Deployment Method tooRetail in IIS</span></span>

| <span data-ttu-id="c0bc9-259">제목</span><span class="sxs-lookup"><span data-stu-id="c0bc9-259">Title</span></span>                   | <span data-ttu-id="c0bc9-260">세부 정보</span><span class="sxs-lookup"><span data-stu-id="c0bc9-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0bc9-261">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-261">**Component**</span></span>               | <span data-ttu-id="c0bc9-262">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c0bc9-262">Web Application</span></span> | 
| <span data-ttu-id="c0bc9-263">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-263">**SDL Phase**</span></span>               | <span data-ttu-id="c0bc9-264">배포</span><span class="sxs-lookup"><span data-stu-id="c0bc9-264">Deployment</span></span> |  
| <span data-ttu-id="c0bc9-265">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-265">**Applicable Technologies**</span></span> | <span data-ttu-id="c0bc9-266">일반</span><span class="sxs-lookup"><span data-stu-id="c0bc9-266">Generic</span></span> |
| <span data-ttu-id="c0bc9-267">**특성**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-267">**Attributes**</span></span>              | <span data-ttu-id="c0bc9-268">해당 없음</span><span class="sxs-lookup"><span data-stu-id="c0bc9-268">N/A</span></span>  |
| <span data-ttu-id="c0bc9-269">**참조**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-269">**References**</span></span>              | <span data-ttu-id="c0bc9-270">[배포 요소(ASP.NET 설정 스키마)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="c0bc9-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="c0bc9-271">**단계**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-271">**Steps**</span></span> | <p><span data-ttu-id="c0bc9-272">hello `<deployment retail>` 스위치 프로덕션 IIS 서버에서 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-272">hello `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="c0bc9-273">이 스위치는 hello 최상의 성능을 사용 하 여 실행 toohelp 사용 되는 응용 프로그램 및 자세한 오류 가능한 최소 보안 정보를 사용 하지 않도록 설정 하 여 leakages hello 해제 hello 기능 toodisplay 페이지, 응용 프로그램의 능력 toogenerate 추적 출력 메시지 tooend 사용자 및 hello 디버그 스위치를 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-273">This switch is used toohelp applications run with hello best possible performance and least possible security information leakages by disabling hello application's ability toogenerate trace output on a page, disabling hello ability toodisplay detailed error messages tooend users, and disabling hello debug switch.</span></span></p><p><span data-ttu-id="c0bc9-274">종종 활성 개발 중에 실패한 요청 추적 및 디버그와 같은 개발자 중심의 스위치 및 옵션이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="c0bc9-275">모든 프로덕션 서버에서 배포 방법 hello tooretail을 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-275">It is recommended that hello deployment method on any production server be set tooretail.</span></span> <span data-ttu-id="c0bc9-276">hello machine.config 파일을 열고 되도록 `<deployment retail="true" />` tootrue 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-276">open hello machine.config file and ensure that `<deployment retail="true" />` remains set tootrue.</span></span></p>|

## <span data-ttu-id="c0bc9-277"><a id="fail"></a>안전한 예외 실패</span><span class="sxs-lookup"><span data-stu-id="c0bc9-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="c0bc9-278">제목</span><span class="sxs-lookup"><span data-stu-id="c0bc9-278">Title</span></span>                   | <span data-ttu-id="c0bc9-279">세부 정보</span><span class="sxs-lookup"><span data-stu-id="c0bc9-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="c0bc9-280">**구성 요소**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-280">**Component**</span></span>               | <span data-ttu-id="c0bc9-281">웹 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c0bc9-281">Web Application</span></span> | 
| <span data-ttu-id="c0bc9-282">**SDL 단계**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-282">**SDL Phase**</span></span>               | <span data-ttu-id="c0bc9-283">빌드</span><span class="sxs-lookup"><span data-stu-id="c0bc9-283">Build</span></span> |  
| <span data-ttu-id="c0bc9-284">**적용 가능한 기술**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-284">**Applicable Technologies**</span></span> | <span data-ttu-id="c0bc9-285">일반</span><span class="sxs-lookup"><span data-stu-id="c0bc9-285">Generic</span></span> |
| <span data-ttu-id="c0bc9-286">**특성**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-286">**Attributes**</span></span>              | <span data-ttu-id="c0bc9-287">해당 없음</span><span class="sxs-lookup"><span data-stu-id="c0bc9-287">N/A</span></span>  |
| <span data-ttu-id="c0bc9-288">**참조**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-288">**References**</span></span>              | [<span data-ttu-id="c0bc9-289">안전하게 실패</span><span class="sxs-lookup"><span data-stu-id="c0bc9-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="c0bc9-290">**단계**</span><span class="sxs-lookup"><span data-stu-id="c0bc9-290">**Steps**</span></span> | <span data-ttu-id="c0bc9-291">응용 프로그램은 안전하게 실패해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-291">Application should fail safely.</span></span> <span data-ttu-id="c0bc9-292">수행되는 특정 결정에 따라 부울 값을 반환하는 모든 메서드는 신중하게 예외 블록을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="c0bc9-293">논리 오류 때문에 부주의 hello 예외 블록 기록 될 때 보안 문제 크립 toowhich 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-293">There are lot of logical errors due toowhich security issues creep in, when hello exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="c0bc9-294">예제</span><span class="sxs-lookup"><span data-stu-id="c0bc9-294">Example</span></span>
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
                        //// Adding additional check tooenable CMS urls if they are not hosted on same domain.
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
<span data-ttu-id="c0bc9-295">메서드 위에 hello 일부 예외가 발생 하는 경우 항상 True를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-295">hello above method will always return True, if some exception happens.</span></span> <span data-ttu-id="c0bc9-296">잘못 된 URL을 제공 하는 hello 최종 사용자는 브라우저 측면 hello 하지만 hello `Uri()` 생성자 하지 않습니다,이 예외를 throw 합니다 및 hello 희생자 toohello 유효 하지만 잘못 된 형식의 URL은 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c0bc9-296">If hello end user provides a malformed URL, that hello browser respects, but hello `Uri()` constructor doesn't, this will throw an exception, and hello victim will be taken toohello valid but malformed URL.</span></span> 
