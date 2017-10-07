---
title: "aaaCustomize Swashbuckle 생성 API 정의"
description: "자세한 내용은 방법 Azure 앱 서비스에서 API 앱에 대 한 Swashbuckle에서 생성 되는 toocustomize API Swagger 정의 합니다."
services: app-service\api
documentationcenter: .net
author: bradygaster
manager: erikre
editor: jimbe
ms.assetid: 6b8cbc38-d282-4a0f-b0c5-762631bae6f3
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: e31c665f8993533c5ec9a935e42cce34f86a5ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-swashbuckle-generated-api-definitions"></a><span data-ttu-id="bbf31-103">Swashbuckle 생성 API 정의 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="bbf31-103">Customize Swashbuckle-generated API definitions</span></span>
## <a name="overview"></a><span data-ttu-id="bbf31-104">개요</span><span class="sxs-lookup"><span data-stu-id="bbf31-104">Overview</span></span>
<span data-ttu-id="bbf31-105">이 문서에서는 설명 toocustomize Swashbuckle toohandle 일반적인 시나리오 tooalter 사용할 수 있는 기본 동작을 hello 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="bbf31-105">This article explains how toocustomize Swashbuckle toohandle common scenarios where you may want tooalter hello default behavior:</span></span>

* <span data-ttu-id="bbf31-106">Swashbuckle는 컨트롤러 메서드의 오버 로드에 대한 중복 작업 식별자를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-106">Swashbuckle generates duplicate operation identifiers for overloads of controller methods</span></span>
* <span data-ttu-id="bbf31-107">Swashbuckle 메서드에서 유효한 응답은 HTTP 200 (OK)에 해당 hello 가정</span><span class="sxs-lookup"><span data-stu-id="bbf31-107">Swashbuckle assumes that hello only valid response from a method is HTTP 200 (OK)</span></span> 

## <a name="customize-operation-identifier-generation"></a><span data-ttu-id="bbf31-108">작업 식별자 생성 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="bbf31-108">Customize operation identifier generation</span></span>
<span data-ttu-id="bbf31-109">Swashbuckle은 컨트롤러 이름과 메서드 이름을 연결하여 Swagger 작업 식별자를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-109">Swashbuckle generates Swagger operation identifiers by concatenating controller name and method name.</span></span> <span data-ttu-id="bbf31-110">이 패턴은 메서드가 여러 번 오버로드되는 경우 문제가 발생합니다. Swashbuckle에서 중복된 작업 ID를 생성하며 이는 잘못된 Swagger JSON입니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-110">This pattern creates a problem when you have multiple overloads of a method: Swashbuckle generates duplicate operation ids, which is invalid Swagger JSON.</span></span>

<span data-ttu-id="bbf31-111">예를 들어 hello 컨트롤러 코드 다음 세 가지 Contact_Get 작업 id Swashbuckle toogenerate를 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-111">For example, hello following controller code causes Swashbuckle toogenerate three Contact_Get operation ids.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

<span data-ttu-id="bbf31-112">이 예제에 대 한 hello 다음과 같은 고유한 이름을 hello 메서드를 제공 하 여 수동으로 hello 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-112">You can solve hello problem manually by giving hello methods unique names, such as hello following for this example:</span></span>

* <span data-ttu-id="bbf31-113">가져오기</span><span class="sxs-lookup"><span data-stu-id="bbf31-113">Get</span></span>
* <span data-ttu-id="bbf31-114">GetById</span><span class="sxs-lookup"><span data-stu-id="bbf31-114">GetById</span></span>
* <span data-ttu-id="bbf31-115">GetPage</span><span class="sxs-lookup"><span data-stu-id="bbf31-115">GetPage</span></span>

<span data-ttu-id="bbf31-116">hello는 대체 항목은 tooextend Swashbuckle toomake 고유한 작업 id를 자동으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-116">hello alternative is tooextend Swashbuckle toomake it automatically generate unique operation ids.</span></span>

<span data-ttu-id="bbf31-117">hello 다음 단계 표시 방법을 사용 하 여 Swashbuckle toocustomize hello *SwaggerConfig.cs* hello Visual Studio API 앱 미리 보기 프로젝트 템플릿에 의해 hello 프로젝트에 포함 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-117">hello following steps show how toocustomize Swashbuckle by using hello *SwaggerConfig.cs* file that is included in hello project by hello Visual Studio API Apps Preview project template.</span></span>  <span data-ttu-id="bbf31-118">또한 API 앱으로 배포하도록 구성한 Web API 프로젝트에서 Swashbuckle을 사용자 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-118">You can also customize Swashbuckle in a Web API project that you configure for deployment as an API app.</span></span>

1. <span data-ttu-id="bbf31-119">사용자 지정 `IOperationFilter` 구현 만들기</span><span class="sxs-lookup"><span data-stu-id="bbf31-119">Create a custom `IOperationFilter` implementation</span></span> 
   
    <span data-ttu-id="bbf31-120">hello `IOperationFilter` 인터페이스 확장 지점을 제공 Swashbuckle 하려는 사용자에 게 toocustomize hello Swagger 메타 데이터가 프로세스의 다양 한 측면입니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-120">hello `IOperationFilter` interface provides an extensibility point for Swashbuckle users who want toocustomize various aspects of hello Swagger metadata process.</span></span> <span data-ttu-id="bbf31-121">hello 다음 코드에서는 hello 작업 id 세대 동작을 변경 하는 한 가지 방법은</span><span class="sxs-lookup"><span data-stu-id="bbf31-121">hello following code demonstrates one method of changing hello operation-id-generation behavior.</span></span> <span data-ttu-id="bbf31-122">hello 코드에는 매개 변수 이름은 toohello 작업 id 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-122">hello code appends parameter names toohello operation id name.</span></span>  
   
        using Swashbuckle.Swagger;
        using System.Web.Http.Description;
   
        namespace ContactsList
        {
            public class MultipleOperationsWithSameVerbFilter : IOperationFilter
            {
                public void Apply(
                    Operation operation,
                    SchemaRegistry schemaRegistry,
                    ApiDescription apiDescription)
                {
                    if (operation.parameters != null)
                    {
                        operation.operationId += "By";
                        foreach (var parm in operation.parameters)
                        {
                            operation.operationId += string.Format("{0}",parm.name);
                        }
                    }
                }
            }
        }
2. <span data-ttu-id="bbf31-123">*App_Start\SwaggerConfig.cs* 파일, 호출 hello `OperationFilter` 메서드 toocause Swashbuckle toouse hello 새 `IOperationFilter` 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-123">In *App_Start\SwaggerConfig.cs* file, call hello `OperationFilter` method toocause Swashbuckle toouse hello new `IOperationFilter` implementation.</span></span>
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    <span data-ttu-id="bbf31-124">hello *SwaggerConfig.cs* hello Swashbuckle NuGet 패키지 여 삭제 된 파일 확장 지점의 많은 주석 처리 된 예제를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-124">hello *SwaggerConfig.cs* file that is dropped in by hello Swashbuckle NuGet package contains many commented-out examples of extensibility points.</span></span> <span data-ttu-id="bbf31-125">hello 추가 설명이 여기 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-125">hello additional comments are not shown here.</span></span> 
   
    <span data-ttu-id="bbf31-126">이렇게 변경 하면 `IOperationFilter` 구현에 사용 되 고 생성 된 고유한 작업 id toobe 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-126">After you make this change, your `IOperationFilter` implementation is used and causes unique operation ids toobe generated.</span></span>
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a><span data-ttu-id="bbf31-127">200 이외의 응답 코드 허용</span><span class="sxs-lookup"><span data-stu-id="bbf31-127">Allow response codes other than 200</span></span>
<span data-ttu-id="bbf31-128">기본적으로 Swashbuckle 가정 HTTP 200 (OK) 응답은 hello *만* 올바른 웹 API 메서드에서 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-128">By default, Swashbuckle assumes that an HTTP 200 (OK) response is hello *only* legitimate response from a Web API method.</span></span> <span data-ttu-id="bbf31-129">일부 경우에 hello 클라이언트 tooraise 예외가 발생 하지 않고 tooreturn에 다른 응답 코드를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-129">In some cases, you may want tooreturn other response codes without causing hello client tooraise an exception.</span></span>  <span data-ttu-id="bbf31-130">예를 들어 hello 다음 웹 API 코드 시나리오를 보여 줍니다 hello 클라이언트 tooaccept 원할 200 또는 404 대 한 유효한 응답으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-130">For example, hello following Web API code demonstrates a scenario in which you would want hello client tooaccept either a 200 or a 404 as valid responses.</span></span>

    [ResponseType(typeof(Contact))]
    public HttpResponseMessage Get(int id)
    {
        var contacts = GetContacts();

        var requestedContact = contacts.FirstOrDefault(x => x.Id == id);

        if (requestedContact == null)
        {
            return Request.CreateResponse(HttpStatusCode.NotFound);
        }
        else
        {
            return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
        }
    }

<span data-ttu-id="bbf31-131">이 시나리오에서는 hello Swashbuckle 기본적으로 생성 하는 Swagger 하나만 합법적인 HTTP 상태 코드, HTTP 200를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-131">In this scenario, hello Swagger that Swashbuckle generates by default specifies only one legitimate HTTP status code, HTTP 200.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

<span data-ttu-id="bbf31-132">클라이언트 hello에 대 한 hello API Swagger 정의 toogenerate 코드를 사용 하는 Visual Studio, HTTP 200 이외의 모든 응답에 대 한 예외가 발생 하는 클라이언트 코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-132">Since Visual Studio uses hello Swagger API definition toogenerate code for hello client, it creates client code that raises an exception for any response other than an HTTP 200.</span></span> <span data-ttu-id="bbf31-133">이 샘플 웹 API 메서드에 대 한 생성 된 C# 클라이언트에서 아래 hello 코드가입니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-133">hello code below is from a C# client generated for this sample Web API method.</span></span>

    if (statusCode != HttpStatusCode.OK)
    {
        HttpOperationException<object> ex = new HttpOperationException<object>();
        ex.Request = httpRequest;
        ex.Response = httpResponse;
        ex.Body = null;
        if (shouldTrace)
        {
            ServiceClientTracing.Error(invocationId, ex);
        }
        throw ex;
    } 

<span data-ttu-id="bbf31-134">XML 주석 또는 hello를 사용 하 여 Swashbuckle 제공 hello 목록이 생성 하거나 예상된 HTTP 응답 코드를 사용자 지정 하는 두 가지 `SwaggerResponse` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-134">Swashbuckle provides two ways of customizing hello list of expected HTTP response codes that it generates, using XML comments or hello `SwaggerResponse` attribute.</span></span> <span data-ttu-id="bbf31-135">hello 특성을 보다 쉽게 이지만 이상 Swashbuckle 5.1.5에서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-135">hello attribute is easier, but it is only available in Swashbuckle 5.1.5 or later.</span></span> <span data-ttu-id="bbf31-136">hello API 앱 미리 보기 새 프로젝트 템플릿은 Visual Studio 2013에서 포함 Swashbuckle 5.0.0, 버전 이므로 hello 서식 파일을 사용 하 고 tooupdate Swashbuckle 하지 않을 경우 수정할 수 있는 유일한 방법은 toouse XML 주석입니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-136">hello API Apps preview new-project template in Visual Studio 2013 includes Swashbuckle version 5.0.0, so if you used hello template and don't want tooupdate Swashbuckle, your only option is toouse XML comments.</span></span> 

### <a name="customize-expected-response-codes-using-xml-comments"></a><span data-ttu-id="bbf31-137">XML 주석을 사용하여 예상되는 응답 코드 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="bbf31-137">Customize expected response codes using XML comments</span></span>
<span data-ttu-id="bbf31-138">Swashbuckle 버전 5.1.5 보다 이전 이면이 메서드 toospecify 응답 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-138">Use this method toospecify response codes if your Swashbuckle version is earlier than 5.1.5.</span></span>

1. <span data-ttu-id="bbf31-139">먼저, toospecify에 대 한 HTTP 응답 코드를 원하는 hello 방법에 비해 XML 문서 주석을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-139">First, add XML documentation comments over hello methods you wish toospecify HTTP response codes for.</span></span> <span data-ttu-id="bbf31-140">다음 예제는 hello와 마찬가지로 코드에서 위에 표시 및 적용 hello XML 문서 tooit 초래 hello 샘플 웹 API 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-140">Taking hello sample Web API action shown above and applying hello XML documentation tooit would result in code like hello following example.</span></span> 
   
        /// <summary>
        /// Returns hello specified contact.
        /// </summary>
        /// <param name="id">hello ID of hello contact.</param>
        /// <returns>A contact record with an HTTP 200, or null with an HTTP 404.</returns>
        /// <response code="200">OK</response>
        /// <response code="404">Not Found</response>
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
   
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
2. <span data-ttu-id="bbf31-141">Hello에 대 한 지침도 *SwaggerConfig.cs* toodirect Swashbuckle toomake 사용 하 여 hello XML 문서 파일의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-141">Add instructions in hello *SwaggerConfig.cs* file toodirect Swashbuckle toomake use of hello XML documentation file.</span></span>
   
   * <span data-ttu-id="bbf31-142">열기 *SwaggerConfig.cs* hello에서 메서드를 만들고 *SwaggerConfig* 클래스 toospecify hello 경로 toohello 문서 XML 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-142">Open *SwaggerConfig.cs* and create a method on hello *SwaggerConfig* class toospecify hello path toohello documentation XML file.</span></span> 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * <span data-ttu-id="bbf31-143">Hello에서 아래로 스크롤하여 *SwaggerConfig.cs* 아래 스크린샷과 hello와 유사한 코드의 hello 주석 줄이 표시 될 때까지 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-143">Scroll down in hello *SwaggerConfig.cs* file until you see hello commented-out line of code resembling hello screen shot below.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * <span data-ttu-id="bbf31-144">Hello 줄 tooenable hello XML 주석 처리 Swagger 생성 하는 동안 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-144">Uncomment hello line tooenable hello XML comments processing during Swagger generation.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. <span data-ttu-id="bbf31-145">순서 toogenerate hello XML 문서 파일에서 hello 프로젝트의 속성으로 이동 하 고 아래 hello 스크린샷에 표시 된 대로 hello XML 문서 파일을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-145">In order toogenerate hello XML documentation file, go into hello project's properties and enable hello XML documentation file as shown in hello screenshot below.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

<span data-ttu-id="bbf31-146">이러한 단계를 수행 되 면 hello Swagger JSON Swashbuckle에 의해 생성 된 hello XML 주석에서 지정한 hello HTTP 응답 코드를 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-146">Once you perform these steps, hello Swagger JSON generated by Swashbuckle will reflect hello HTTP response codes that you specified in hello XML comments.</span></span> <span data-ttu-id="bbf31-147">아래의 스크린 샷은 hello이 새 JSON 페이로드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-147">hello screenshot below demonstrates this new JSON payload.</span></span> 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

<span data-ttu-id="bbf31-148">Visual Studio tooregenerate hello 클라이언트 코드를 사용 하 여 REST API에 대 한 경우 허용 toohandle hello의 null을 반환 하는 방법을를 사용 중인 코드 toomake 결정 하는 예외를 발생 하지 않고 hello C# 코드 hello 찾을 수 없습니다 및 HTTP OK 상태 코드는 수락 연락처 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-148">When you use Visual Studio tooregenerate hello client code for your REST API, hello C# code accepts both hello HTTP OK and Not Found status codes without raising an exception, allowing your consuming code toomake decisions on how toohandle hello return of a null Contact record.</span></span> 

        if (statusCode != HttpStatusCode.OK && statusCode != HttpStatusCode.NotFound)
        {
            HttpOperationException<object> ex = new HttpOperationException<object>();
            ex.Request = httpRequest;
            ex.Response = httpResponse;
            ex.Body = null;
            if (shouldTrace)
            {
                ServiceClientTracing.Error(invocationId, ex);
            }
                throw ex;
        }

<span data-ttu-id="bbf31-149">이 데모에서는 hello 코드에서 확인할 수 있습니다 [이 GitHub 리포지토리](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-149">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span></span> <span data-ttu-id="bbf31-150">Hello 웹 API 프로젝트 XML 문서 주석 여 표시 된이 API에 대해 생성 된 클라이언트를 포함 하는 콘솔 응용 프로그램 프로젝트가입니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-150">Along with hello Web API project marked up with XML documentation comments is a Console Application project that contains a generated client for this API.</span></span> 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a><span data-ttu-id="bbf31-151">Hello SwaggerResponse 특성을 사용 하 여 예상된 응답 코드를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="bbf31-151">Customize expected response codes using hello SwaggerResponse attribute</span></span>
<span data-ttu-id="bbf31-152">hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) 특성은 이상 Swashbuckle 5.1.5에서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-152">hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) attribute is available in Swashbuckle 5.1.5 and later.</span></span> <span data-ttu-id="bbf31-153">프로젝트에서 이전 버전을 설치 하는 경우이 섹션의이 특성을 사용할 수 있도록 tooupdate hello Swashbuckle NuGet 패키지 하는 방법을 설명 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-153">In case you have an earlier version in your project, this section starts by explaining how tooupdate hello Swashbuckle NuGet package so that you can use this attribute.</span></span>

1. <span data-ttu-id="bbf31-154">**솔루션 탐색기**에서 웹 API 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-154">In **Solution Explorer**, right-click your Web API project and click **Manage NuGet Packages**.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. <span data-ttu-id="bbf31-155">Hello 클릭 *업데이트* 단추 다음 toohello *Swashbuckle* NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-155">Click hello *Update* button next toohello *Swashbuckle* NuGet package.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. <span data-ttu-id="bbf31-156">Hello 추가 *SwaggerResponse* toospecify 유효한 HTTP 응답 코드 원하는 toohello 웹 API 작업 메서드에 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-156">Add hello *SwaggerResponse* attributes toohello Web API action methods for which you want toospecify valid HTTP response codes.</span></span> 
   
        [SwaggerResponse(HttpStatusCode.OK)]
        [SwaggerResponse(HttpStatusCode.NotFound)]
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
4. <span data-ttu-id="bbf31-157">추가 `using` hello 특성의 네임 스페이스에 대 한 문:</span><span class="sxs-lookup"><span data-stu-id="bbf31-157">Add a `using` statement for hello attribute's namespace:</span></span>
   
        using Swashbuckle.Swagger.Annotations;
5. <span data-ttu-id="bbf31-158">Toohello 찾아보기 */swagger/docs/v1* 하려면 프로젝트의 다양 한 HTTP 응답 코드에 표시 됩니다. hello URL hello Swagger JSON입니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-158">Browse toohello */swagger/docs/v1* URL of your project and hello various HTTP response codes will be visible in hello Swagger JSON.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

<span data-ttu-id="bbf31-159">이 데모에서는 hello 코드에서 확인할 수 있습니다 [이 GitHub 리포지토리](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-159">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span></span> <span data-ttu-id="bbf31-160">Hello와 함께 웹 API 프로젝트 hello로 데코레이팅 *SwaggerResponse* 특성은이 API에 대해 생성 된 클라이언트를 포함 하는 콘솔 응용 프로그램 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-160">Along with hello Web API project decorated with hello *SwaggerResponse* attribute is a Console Application project that contains a generated client for this API.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bbf31-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bbf31-161">Next steps</span></span>
<span data-ttu-id="bbf31-162">이 문서는 toocustomize hello 방법은 Swashbuckle 작업 id 및 유효한 응답 코드를 생성 하는 방법을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="bbf31-162">This article has shown how toocustomize hello way Swashbuckle generates operation ids and valid response codes.</span></span> <span data-ttu-id="bbf31-163">자세한 내용은 [GitHub의 Swashbuckle](https://github.com/domaindrivendev/Swashbuckle)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bbf31-163">For more information, see [Swashbuckle on GitHub](https://github.com/domaindrivendev/Swashbuckle).</span></span>

