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
# <a name="security-frame-exception-management--mitigations"></a>보안 프레임: 예외 관리 | 해결 방법 
| 제품/서비스 | 문서 |
| --------------- | ------- |
| **WCF** | <ul><li>[WCF - 구성 파일에 serviceDebug 노드를 포함하지 않음](#servicedebug)</li><li>[WCF - 구성 파일에 serviceMetadata 노드를 포함하지 않음](#servicemetadata)</li></ul> |
| **앱 API** | <ul><li>[ASP.NET Web API에서 적절한 예외 처리가 수행되었는지 확인 ](#exception)</li></ul> |
| **웹 응용 프로그램** | <ul><li>[오류 메시지에 보안 정보를 노출하지 않음](#messages)</li><li>[기본 오류 처리 페이지 구현 ](#default)</li><li>[IIS의 배포 방법을 tooRetail 설정](#deployment)</li><li>[안전한 예외 실패](#fail)</li></ul> |

## <a id="servicedebug"></a>WCF - 구성 파일에 serviceDebug 노드를 포함하지 않음

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반, .NET Framework 3 |
| **특성**              | 해당 없음  |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify, 영국](https://vulncat.fortify.com/en/vulncat/index.html) |
| **단계** | Windows Communication Framework (WCF) 서비스 구성된 tooexpose 디버깅 정보를 수 있습니다. 디버그 정보를 프로덕션 환경에서는 사용하지 않아야 합니다. hello `<serviceDebug>` 태그는 WCF 서비스에 대 한 hello 디버그 정보 기능이 활성화 되어 있는지를 정의 합니다. Hello 특성 includeExceptionDetailInFaults tootrue 설정 되 면 hello 응용 프로그램에서 예외 정보 tooclients를 반환 됩니다. 공격자가 디버깅 출력 toomount 대상에 대 한 공격 hello 프레임 워크, 데이터베이스 또는 hello 응용 프로그램에서 사용 하는 다른 리소스에서 얻습니다 hello 추가 정보를 활용할 수 있습니다. |

### <a name="example"></a>예제
hello 다음 구성 파일에는 hello `<serviceDebug>` 태그: 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
Hello 서비스의 디버깅 정보를 사용 하지 않도록 설정 합니다. Hello를 제거 하 여이 작업을 수행할 수 수 `<serviceDebug>` 응용 프로그램 구성 파일에서 이러한 태그입니다. 

## <a id="servicemetadata"></a>WCF - 구성 파일에 serviceMetadata 노드를 포함하지 않음

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | WCF | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 일반, .NET Framework 3 |
| **참조**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify, 영국](https://vulncat.fortify.com/en/vulncat/index.html) |
| **단계** | 서비스에 대 한 정보를 공개적으로 노출 공격자가 어떻게 hello 서비스 악용할 수에 대 한 중요 한 정보를 제공할 수 있습니다. hello `<serviceMetadata>` 태그 hello 메타 데이터 게시 기능을 사용할 수 있습니다. 서비스 메타데이터에는 공개적으로 액세스할 수 없게 해야 하는 중요한 정보가 포함될 수 있습니다. 여기에 최소한 tooaccess hello 메타 데이터 및 불필요 한 정보가 노출 되지 않도록 신뢰할 수 있는 사용자만 허용 합니다. 더 좋은 방법은 hello 기능 toopublish 메타 데이터를 완전히 비활성화 합니다. 안전 WCF 구성 hello 포함 되지 것입니다 `<serviceMetadata>` 태그입니다. |

## <a id="exception"></a>ASP.NET Web API에서 적절한 예외 처리가 수행되었는지 확인

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | Web API | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | MVC 5, MVC 6 |
| **특성**              | 해당 없음  |
| **참조**              | [ASP.NET Web API에서 예외 처리](http://www.asp.net/web-api/overview/error-handling/exception-handling), [ASP.NET Web API의 모델 유효성 검사](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| **단계** | 기본적으로 ASP.NET Web API에서 확인할 수 없는 대부분의 예외는 `500, Internal Server Error` 상태 코드의 HTTP 응답으로 변환됩니다.|

### <a name="example"></a>예제
hello API에서 반환 된 toocontrol hello 상태 코드 `HttpResponseException` 아래와 같이 사용할 수 있습니다. 
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

### <a name="example"></a>예제
Hello 예외 응답에 보다 세부적인 제어에 대 한 hello `HttpResponseMessage` 아래와 같이 클래스를 사용할 수 있습니다. 
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
처리 되지 않은 hello 형식의 되지 않는 예외 toocatch `HttpResponseException`, 예외 필터를 사용할 수 있습니다. 예외 필터 구현 hello `System.Web.Http.Filters.IExceptionFilter` 인터페이스입니다. hello 가장 간단한 방법은 toowrite 예외 필터는 hello에서 tooderive `System.Web.Http.Filters.ExceptionFilterAttribute` 클래스 및 hello OnException 메서드를 재정의 합니다. 

### <a name="example"></a>예제
다음은 `NotImplementedException`을 HTTP 상태 코드 `501, Not Implemented`로 변환하는 필터입니다. 
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

여러 가지 방법으로 tooregister 웹 API 예외 필터는 있습니다.
- 작업 기준
- 컨트롤러 기준
- 전역적으로

### <a name="example"></a>예제
tooapply hello 필터 tooa 특정 작업, hello 필터 특성 toohello 액션으로 추가 합니다. 
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
### <a name="example"></a>예제
hello에 대 한 동작 tooapply hello 필터 tooall는 `controller`, 특성 toohello로 hello 필터 추가 `controller` 클래스: 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a>예제
tooapply hello tooall Web API 컨트롤러 필터링 전체적으로, hello 필터 toohello의 인스턴스를 추가 `GlobalConfiguration.Configuration.Filters` 컬렉션입니다. 이 컬렉션의 예외 필터 tooany Web API 컨트롤러 작업을 적용합니다. 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a>예제
모델 유효성 검사에 대 한 hello 모델 상태 tooCreateErrorResponse 메서드 아래와 같이 전달 될 수 있습니다. 
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

예외 처리에 대 한 자세한 내용은 hello references 섹션에 hello 링크와 ASP.Net Web API에서 모델 유효성 검사를 확인 합니다. 

## <a id="messages"></a>오류 메시지에 보안 정보를 노출하지 않음

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | 해당 없음  |
| **단계** | <p>일반 오류 메시지가 제공 되며 직접 toohello 사용자 중요 한 응용 프로그램 데이터를 포함 하지 않고 있습니다. 중요한 데이터의 예는 다음과 같습니다.</p><ul><li>서버 이름</li><li>연결 문자열</li><li>사용자 이름</li><li>암호</li><li>SQL 프로시저</li><li>동적 SQL 오류의 세부 정보</li><li>스택 추적 및 코드 줄</li><li>메모리에 저장된 변수</li><li>드라이브 및 폴더 위치</li><li>응용 프로그램 설치 지점</li><li>호스트 구성 설정</li><li>기타 내부 응용 프로그램 정보</li></ul><p>응용 프로그램 내의 모든 오류를 트래핑하고 일반 오류 메시지를 제공할 뿐 아니라 IIS 내에서 사용자 지정 오류를 사용하도록 설정하면 정보가 공개되지 않도록 하는 데 도움이 됩니다. SQL Server 데이터베이스 및.NET 예외 처리, 다른 오류 아키텍처, 처리 중 특히 자세한 정보 및 매우 유용한 tooa 악의적인 사용자가 응용 프로그램 프로 파일링 됩니다. 클래스의 내용을 hello.NET 예외 클래스에서 파생 되며 예기치 않은 예외가 실수로 되지 않도록 적합 한 예외 처리 있는지 확인 하는 디스플레이 hello 발생 하는 직접 toohello 사용자 직접 수행 합니다.</p><ul><li>일반 오류 메시지를 직접 toohello 사용자 hello 예외/오류 메시지에서 직접 찾을 트래버스하여 특정 세부 정보를 추상화를 제공 합니다.</li><li>수행 하지 표시 hello 내용의.NET 예외 클래스를 직접 toohello 사용자</li><li>모든 오류 메시지를 트래핑 하 고 해당 하는 경우 일반 오류 메시지 보낸된 toohello 응용 프로그램 클라이언트를 통해 hello 사용자에 게 알리는</li><li>Toohello 사용자 hello 특히 반환 값을 직접 hello 내용의 hello 예외 클래스를 노출 하지 않는 `.ToString()`, 또는 hello hello 메시지, 스택 추적 속성 값입니다. 안전 하 게이 정보를 기록 하 고 더 무해 메시지 toohello 사용자 표시</li></ul>|

## <a id="default"></a>기본 오류 처리 페이지 구현

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [ASP.NET 오류 페이지 설정 대화 상자 편집](https://technet.microsoft.com/library/dd569096(WS.10).aspx) |
| **단계** | <p>ASP.NET 응용 프로그램이 실패하고 HTTP/1.x 500 내부 서버 오류가 발생하거나 기능 구성(예: 요청 필터링)으로 인해 페이지가 표시되지 않을 경우 오류 메시지가 생성됩니다. 관리자 친숙 한 메시지 toohello 클라이언트, 상세한 오류 메시지 toohello 클라이언트 또는 자세한 오류 메시지 toolocalhost만 hello 응용 프로그램을 표시할지 여부를 선택할 수 있습니다. hello <customErrors> hello web.config의 태그는 세 가지 모드:</p><ul><li>**On:** 사용자 지정 오류가 사용되도록 지정합니다. defaultRedirect 특성을 지정하지 않으면 사용자에게 일반 오류가 표시됩니다. toohello 원격 클라이언트 및 로컬 호스트 toohello hello 사용자 지정 오류가 표시 됩니다.</li><li>**Off:** 사용자 지정 오류가 사용되지 않도록 지정합니다. hello 자세한 ASP.NET 오류가 표시 됩니다 toohello 원격 클라이언트와 toohello 로컬 호스트</li><li>**RemoteOnly:** 지정 ASP.NET 오류는 toohello 로컬 호스트를 표시 하 고는 사용자 지정 오류만 toohello 원격 클라이언트에 표시 됩니다. 이 hello 기본값</li></ul><p>열기 hello `web.config` hello 응용 프로그램/사이트에 대 한 파일을 hello 태그 중 하나에 있는지 확인 `<customErrors mode="RemoteOnly" />` 또는 `<customErrors mode="On" />` 정의 합니다.</p>|

## <a id="deployment"></a>IIS의 배포 방법을 tooRetail 설정

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 배포 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [배포 요소(ASP.NET 설정 스키마)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx) |
| **단계** | <p>hello `<deployment retail>` 스위치 프로덕션 IIS 서버에서 위한 것입니다. 이 스위치는 hello 최상의 성능을 사용 하 여 실행 toohelp 사용 되는 응용 프로그램 및 자세한 오류 가능한 최소 보안 정보를 사용 하지 않도록 설정 하 여 leakages hello 해제 hello 기능 toodisplay 페이지, 응용 프로그램의 능력 toogenerate 추적 출력 메시지 tooend 사용자 및 hello 디버그 스위치를 사용 하지 않도록 설정 합니다.</p><p>종종 활성 개발 중에 실패한 요청 추적 및 디버그와 같은 개발자 중심의 스위치 및 옵션이 사용됩니다. 모든 프로덕션 서버에서 배포 방법 hello tooretail을 설정 하는 것이 좋습니다. hello machine.config 파일을 열고 되도록 `<deployment retail="true" />` tootrue 설정 됩니다.</p>|

## <a id="fail"></a>안전한 예외 실패

| 제목                   | 세부 정보      |
| ----------------------- | ------------ |
| **구성 요소**               | 웹 응용 프로그램 | 
| **SDL 단계**               | 빌드 |  
| **적용 가능한 기술** | 일반 |
| **특성**              | 해당 없음  |
| **참조**              | [안전하게 실패](https://www.owasp.org/index.php/Fail_securely) |
| **단계** | 응용 프로그램은 안전하게 실패해야 합니다. 수행되는 특정 결정에 따라 부울 값을 반환하는 모든 메서드는 신중하게 예외 블록을 만들어야 합니다. 논리 오류 때문에 부주의 hello 예외 블록 기록 될 때 보안 문제 크립 toowhich 많이 있습니다.|

### <a name="example"></a>예제
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
메서드 위에 hello 일부 예외가 발생 하는 경우 항상 True를 반환 합니다. 잘못 된 URL을 제공 하는 hello 최종 사용자는 브라우저 측면 hello 하지만 hello `Uri()` 생성자 하지 않습니다,이 예외를 throw 합니다 및 hello 희생자 toohello 유효 하지만 잘못 된 형식의 URL은 제거 됩니다. 
