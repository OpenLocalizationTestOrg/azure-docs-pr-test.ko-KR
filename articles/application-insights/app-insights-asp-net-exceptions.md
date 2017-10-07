---
title: "aaaDiagnose 오류와 예외를 웹 Azure Application Insights를 사용 하 여 앱 | Microsoft Docs"
description: "요청 원격 분석과 함께 ASP.NET 앱에서 예외를 캡처합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a>Application Insights를 사용하여 웹앱에서 예외 진단
라이브 웹앱의 예외는 [Application Insights](app-insights-overview.md)에서 보고됩니다. Hello 원인을 빠르게 진단할 수 있도록 실패 한 요청 예외 및 hello 클라이언트와 서버 모두에서 다른 이벤트와 연관 시킬 수 있습니다.

## <a name="set-up-exception-reporting"></a>예외 보고 설정
* 서버 응용 프로그램에서 보고 한 toohave 예외:
  * 앱 코드에서 [Application Insights SDK](app-insights-asp-net.md)를 설치합니다.
  * IIS 웹 서버: [Application Insights 에이전트](app-insights-monitor-performance-live-website-now.md)를 실행합니다.
  * Azure 웹 앱: hello 추가 [Application Insights 확장이](app-insights-azure-web-apps.md)
  * Java 웹 응용 프로그램: 설치 hello [Java 에이전트](app-insights-java-agent.md)
* Hello 설치 [JavaScript 코드 조각을](app-insights-javascript.md) 프로그램 웹 페이지 toocatch 브라우저 예외에서입니다.
* 일부 응용 프로그램 프레임 워크 또는 일부 설정을 사용 하 여 필요한 tootake 몇 가지 추가 단계 toocatch 예외가 더 이상 발생 합니다.
  * [웹 양식](#web-forms)
  * [MVC](#mvc)
  * [Web API 1.*](#web-api-1)
  * [Web API 2.*](#web-api-2)
  * [WCF](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a>Visual Studio를 사용하여 예외 진단
디버깅이 설정 된 상태로 Visual Studio toohelp에서 hello 응용 프로그램 솔루션을 엽니다.

F5 키를 사용 하 여 개발 컴퓨터 또는 서버에서 hello 앱을 실행 합니다.

Visual Studio에서 Application Insights 검색 창 hello를 열고 앱에서 toodisplay 이벤트를 설정 합니다. 디버그 하는 동안 hello Application Insights 단추를 클릭 하 여이 수행할 수 있습니다.

![Hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 Application Insights를 선택한 열려 있습니다.](./media/app-insights-asp-net-exceptions/34.png)

공지 hello 보고서 tooshow 정당한 예외를 필터링 할 수 있습니다.

*예외가 표시되지 않나요? [예외 캡처](#exceptions)를 참조하세요.*

예외 보고서 tooshow 해당 스택 추적을 클릭 합니다.
Hello 스택 추적 tooopen hello 관련 코드 파일에서에서 선 참조를 클릭 합니다.  

Hello 코드에서 CodeLens hello 예외에 대 한 데이터를 표시 되는지 확인 합니다.

![CodeLens 예외 알림.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 오류 진단
응용 프로그램의 hello Application Insights 개요에서 hello 오류 타일 예외에 대 한 차트 보여 주고 hello 목록과 함께 hello 가장 자주 오류가 발생 하는 Url 요청 HTTP 요청에 실패 했습니다.

![설정 선택, 오류](./media/app-insights-asp-net-exceptions/012-start.png)

클릭 hello 중 하나를 통해 실패 예외 hello hello 세부 정보를 볼 수 있습니다, 스택 추적의 hello 목록 tooget tooindividual 발견에서 예외 형식:

![실패 한 요청 및 예외 세부 정보에서 인스턴스를 hello 예외의 tooinstances 설정 됩니다.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

**또는** 요청의 hello 목록에서 시작 하 고 관련된 tooit 예외를 확인할 수 있습니다.

*예외가 표시되지 않나요? [예외 캡처](#exceptions)를 참조하세요.*


## <a name="custom-tracing-and-log-data"></a>사용자 지정 추적 및 로그 데이터
tooget 진단 데이터를 특정 tooyour 응용 프로그램, 코드 toosend 삽입할 수 있습니다 자신만 원격 분석 데이터. 이 hello 요청, 페이지 보기 및 기타 자동으로 수집 된 데이터와 함께 진단 검색에 표시 합니다.

여러 옵션이 있습니다.

* [trackevent ()](app-insights-api-custom-events-metrics.md#trackevent) hello 데이터도 보냅니다 진단 검색에서 사용자 지정 이벤트 아래에 표시 되지만 사용 패턴, 모니터링을 위해 일반적으로 사용 됩니다. 이벤트의 이름을 지정하고, [진단 검색을 필터링](app-insights-diagnostic-search.md)할 수 있는 문자열 속성 및 숫자 메트릭 수를 수행할 수있습니다. 
* [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) 를 사용하여 POST 정보와 같은 긴데이터를 보낼 수 있습니다.
* [TrackException()](#exceptions) 은 스택 추적을 보냅니다. [예외에 대해 자세히 알아보세요](#exceptions).
* 사용자가 이미 Log4Net 또는 NLog와 같은 로깅 프레임워크를 사용하는 경우, 요청과 예외 데이터와 함께 진단 검색 안에서 [이러한 로그를 캡처](app-insights-asp-net-trace-logs.md)하고 볼 수 있습니다.

이러한 이벤트를 열고 toosee [검색](app-insights-diagnostic-search.md)필터를 열고 사용자 지정 이벤트, 추적 또는 예외를 선택 합니다.

![드릴스루](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> 응용 프로그램 원격 분석을 많이 생성, hello 적응 샘플링 모듈 toohello 포털 이벤트의 대표 일부만 전송 하 여 전송 된 hello 볼륨을 자동으로 줄어듭니다. 관련된 이벤트를 탐색할 수 있도록 동일한 작업을 선택 하거나 그룹으로 선택 취소 해야 하는 hello에 포함 된 이벤트입니다. [샘플링에 대해 알아봅니다.](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a>Toosee 게시 데이터를 요청 하는 방법
요청 정보 tooyour 앱 POST 호출에 전송 된 hello 데이터를 포함 하지 않습니다. toohave이이 데이터를 보고 합니다.

* [Hello SDK 설치](app-insights-asp-net.md) 응용 프로그램 프로젝트에 있습니다.
* 응용 프로그램 toocall에 코드를 삽입 [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace)합니다. Hello 메시지 매개 변수에서 hello 게시 데이터를 보냅니다. 않으므로 헤드가 허용 toohello 크기 제한 toosend 정당한 hello 중요 한 데이터를 시도해 야 합니다.
* 실패 한 요청을 조사 하는 경우 연결 된 hello 추적을 찾습니다.  

![드릴스루](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <a name="exceptions"></a> 예외 및 관련 진단 데이터 캡처
처음에 표시 되지 않습니다 hello 포털에서 응용 프로그램에서 실패를 야기 하는 모든 hello 예외입니다. 모든 브라우저 예외 표시 됩니다 (hello를 사용 하 여 [JavaScript SDK](app-insights-javascript.md) 웹 페이지에서). IIS가 대부분 서버 예외를 발견 하 고 toowrite 약간의 코드 toosee 해야 하지만 해당 합니다.

다음을 수행할 수 있습니다.

* **예외를 명시적으로 기록** 예외 처리기 tooreport hello 예외에서 코드를 삽입 하 여 합니다.
* **예외를 자동으로 캡처** 합니다. 다양 한 유형의 프레임 워크에 대 한 hello 필요한 추가 서로 다릅니다.

## <a name="reporting-exceptions-explicitly"></a>예외를 명시적으로 보고
hello 가장 간단한 방법은 tooinsert 예외 처리기에서 호출 tooTrackException()입니다.

JavaScript

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

C#

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

VB

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

hello 속성 및 값 매개 변수는 선택적 이지만 필요한 [필터링 및 추가](app-insights-diagnostic-search.md) 추가 정보입니다. 예를 들어 여러 게임을 실행할 수 있는 앱이 있는 경우 모든 hello 예외 보고서 관련된 tooa 특정 게임을 찾을 수 있습니다. Tooeach 사전 처럼 때 항목을 추가할 수 있습니다.

## <a name="browser-exceptions"></a>브라우저 예외
대부분의 브라우저 예외가 보고됩니다.

웹 페이지 콘텐츠 배달 네트워크 또는 다른 도메인에서 스크립트 파일을 포함 하는 경우 스크립트 태그에 hello 특성 확인 ```crossorigin="anonymous"```, 해당 hello 서버 보냅니다 [CORS 헤더](http://enable-cors.org/)합니다. 이렇게 하면 스택 추적 tooget 및 이러한 리소스에서 처리 되지 않은 JavaScript 예외에 대 한 세부 정보입니다.

## <a name="web-forms"></a>웹 양식
Web forms hello HTTP 모듈 CustomErrors를 사용 하 여 구성 리디렉션을 없는 경우 수 toocollect hello 예외 됩니다.

하지만 활성 리디렉션을 설정한 경우 hello 줄 toohello Application_Error 함수 Global.asax.cs에서 다음을 추가 합니다. (아직 없는 경우 Global.asax 파일 추가).

*C#*

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a>MVC
경우 hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) 구성은 `Off`, 예외는 hello에 사용할 수 있는 경우가 [HTTP 모듈](https://msdn.microsoft.com/library/ms178468.aspx) toocollect 합니다. 그러나이 경우 `RemoteOnly` (기본값), 또는 `On`, 다음 hello 예외가 지워집니다 및 tooautomatically 수집할 Application Insights에 사용할 수 없습니다. Hello를 재정의 하 여이 해결할 수 [System.Web.Mvc.HandleErrorAttribute 클래스](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), hello 다른 버전에 대해 MVC 아래와 같이 재정의 hello 클래스를 적용 하 고 ([github 소스](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report hello exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a>MVC 2
컨트롤러에서 새 특성으로 hello HandleError 특성을 대체 합니다.

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[샘플](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a>MVC 3
Global.asax.cs에서 `AiHandleErrorAttribute` 를 글로벌 필터로 등록합니다.

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[샘플](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a>MVC 4, MVC5
FilterConfig.cs에서 AiHandleErrorAttribute를 글로벌 필터로 등록합니다.

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[샘플](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a>Web API 1.x
System.Web.Http.Filters.ExceptionFilterAttribute를 재정의합니다.

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

Hello 경우 WebApiConfig 클래스에서 toohello 전역 필터 구성을 추가 하거나이 재정의 된 특성 toospecific 컨트롤러를 추가할 수 있습니다.

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[샘플](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

Hello 예외 필터를 처리할 수 없는 경우에 여러 가지가 있습니다. 예:

* 컨트롤러 생성자에서 throw된 예외
* 메시지 처리기에서 throw된 예외
* 라우팅 중에 throw된 예외
* 응답 콘텐츠를 직렬화하는 동안 throw된 예외

## <a name="web-api-2x"></a>Web API 2.x
IExceptionLogger를 추가로 구현합니다.

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

경우 WebApiConfig이 toohello 서비스를 추가 합니다.

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  }

[샘플](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

또는 다음 방법을 사용해도 됩니다.

1. 대체 hello IExceptionHandler의 사용자 지정 구현으로 ExceptionHandler만 합니다. 이 동작은 때 호출 hello 프레임 워크는 응답 메시지 (hello 연결 예를 들어 중단 될 때에 not) toosend 여전히 수 toochoose
2. (에 설명 된 대로 웹 API 1.x 컨트롤러 위의 hello 섹션)-예외 필터를 모든 경우에에서 호출 되지 않습니다.

## <a name="wcf"></a>WCF
특성을 확장하고 IErrorHandler 및 IServiceBehavior를 구현하는 클래스를 추가합니다.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

Hello 특성 toohello 서비스 구현을 추가 합니다.

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[샘플](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a>예외 성능 카운터
있는 경우 [hello Application Insights 에이전트를 설치](app-insights-monitor-performance-live-website-now.md) 서버에서.NET으로 측정 된 hello 예외 속도 차트를 얻을 수 있습니다. 여기에는 처리된 .NET 예외와 처리되지 않은 .NET 예외가 모두 포함됩니다.

메트릭 탐색기 블레이드를 열고 새 차트를 추가한 다음 성능 카운터 아래에 나열된 **예외 속도**를 선택합니다.

hello.NET framework의 예외 hello 수를 계산 하는 간격에 되며 hello 간격의 길이 hello 나누어 hello 속도 계산 합니다.

Note 하다는 점을 TrackException 보고서를 계산 하 여 hello Application Insights 포털에서 계산 하는 hello '예외' 개수와에서 다릅니다. hello 샘플링 간격 다르고 hello SDK 모든 처리 및 처리 되지 않은 예외에 대 한 TrackException 보고서를 보내지 않습니다.

## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a>다음 단계
* [REST, SQL 및 기타 호출 toodependencies 모니터링](app-insights-asp-net-dependencies.md)
* [페이지 로드 시간, 브라우저 예외 및 AJAX 호출 모니터링](app-insights-javascript.md)
* [성능 카운터 모니터링](app-insights-performance-counters.md)
