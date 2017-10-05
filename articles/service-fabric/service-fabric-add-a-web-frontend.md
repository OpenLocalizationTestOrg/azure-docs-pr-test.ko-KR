---
title: "ASP.NET Core를 사용하여 Azure Service Fabric 앱에 대한 프런트 엔드 만들기 | Microsoft Docs"
description: "Service Remoting을 통해 ASP.NET Core 프로젝트 및 서비스 간 통신을 사용하여 Service Fabric 응용 프로그램을 웹에 노출합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: b19aaa652f2c15573ded632ca1348e1a6752f080
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="78ce6-103">ASP.NET Core를 사용하여 응용 프로그램에 대한 웹 서비스 프런트 엔드 구축</span><span class="sxs-lookup"><span data-stu-id="78ce6-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="78ce6-104">기본적으로 Azure 서비스 패브릭 서비스는 웹에 공용 인터페이스를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-104">By default, Azure Service Fabric services do not provide a public interface to the web.</span></span> <span data-ttu-id="78ce6-105">HTTP 클라이언트에 응용 프로그램의 기능을 표시하려면 진입점 역할을 할 웹 프로젝트를 만든 후 그 곳에서 개별 서비스와 통신해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-105">To expose your application's functionality to HTTP clients, you have to create a web project to act as an entry point and then communicate from there to your individual services.</span></span>

<span data-ttu-id="78ce6-106">이 자습서에서는 [Visual Studio에서 첫 번째 응용 프로그램 만들기](service-fabric-create-your-first-application-in-visual-studio.md) 자습서에서 남겨둔 항목을 선택하고 상태 저장 카운터 서비스 앞에 ASP.NET Core 웹 서비스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-106">In this tutorial, we pick up where we left off in the [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add an ASP.NET Core web service in front of the stateful counter service.</span></span> <span data-ttu-id="78ce6-107">아직 수행하지 않은 경우 다시 돌아가서 먼저 해당 자습서를 단계별로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="set-up-your-environment-for-aspnet-core"></a><span data-ttu-id="78ce6-108">ASP.NET Core에 대한 환경 설정</span><span class="sxs-lookup"><span data-stu-id="78ce6-108">Set up your environment for ASP.NET Core</span></span>

<span data-ttu-id="78ce6-109">이 자습서를 따르려면 Visual Studio 2017이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-109">You need Visual Studio 2017 to follow along with this tutorial.</span></span> <span data-ttu-id="78ce6-110">모든 버전에서 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-110">Any edition will do.</span></span> 

 - [<span data-ttu-id="78ce6-111">Visual Studio 2017 설치</span><span class="sxs-lookup"><span data-stu-id="78ce6-111">Install Visual Studio 2017</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="78ce6-112">ASP.NET Core Service Fabric 응용 프로그램을 개발하려면 다음과 같은 작업을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-112">To develop ASP.NET Core Service Fabric applications, you should have the following workloads installed:</span></span>
 - <span data-ttu-id="78ce6-113">**Azure 개발**(*웹 및 클라우드* 아래)</span><span class="sxs-lookup"><span data-stu-id="78ce6-113">**Azure development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="78ce6-114">**ASP.NET 및 웹 개발**(*웹 및 클라우드* 아래)</span><span class="sxs-lookup"><span data-stu-id="78ce6-114">**ASP.NET and web development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="78ce6-115">**.NET Core 플랫폼 간 개발**(*다른 도구 집합* 아래)</span><span class="sxs-lookup"><span data-stu-id="78ce6-115">**.NET Core cross-platform development** (under *Other Toolsets*)</span></span>

>[!Note] 
><span data-ttu-id="78ce6-116">Visual Studio 2015용 .NET Core 도구는 더 이상 업데이트되지 않지만 여전히 Visual Studio 2015를 사용하는 경우 [.NET Core VS 2015 Tooling 미리 보기 2](https://www.microsoft.com/net/download/core)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-116">The .NET Core tools for Visual Studio 2015 are no longer being updated, however if you are still using Visual Studio 2015, you need to have [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="add-an-aspnet-core-service-to-your-application"></a><span data-ttu-id="78ce6-117">응용 프로그램에 ASP.NET Core 서비스 추가</span><span class="sxs-lookup"><span data-stu-id="78ce6-117">Add an ASP.NET Core service to your application</span></span>
<span data-ttu-id="78ce6-118">ASP.NET Core는 최신 웹 UI 및 Web API를 만드는 데 사용할 수 있는 가벼운 크로스 플랫폼 웹 개발 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-118">ASP.NET Core is a lightweight, cross-platform web development framework that you can use to create modern web UI and web APIs.</span></span> 

<span data-ttu-id="78ce6-119">기존 응용 프로그램에 ASP.NET Web API 프로젝트를 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-119">Let's add an ASP.NET Web API project to our existing application.</span></span>

1. <span data-ttu-id="78ce6-120">솔루션 탐색기에서 응용 프로그램 프로젝트 내의 **서비스**를 마우스 오른쪽 단추로 클릭하고 **추가 > 새 Service Fabric 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-120">In Solution Explorer, right-click **Services** within the application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![기존 응용 프로그램에 새 서비스 추가][vs-add-new-service]
2. <span data-ttu-id="78ce6-122">**서비스 만들기** 페이지에서 **ASP.NET Core**를 선택하고 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-122">On the **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![새 서비스 대화 상자에서 ASP.NET 웹 서비스 선택][vs-new-service-dialog]

3. <span data-ttu-id="78ce6-124">다음 페이지에서는 ASP.NET Core 프로젝트 템플릿 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-124">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="78ce6-125">Service Fabric 응용 프로그램에서 ASP.NET Core 프로젝트를 만드는 경우 약간의 코드만 추가해서 서비스를 Service Fabric 런타임에 등록할 수 있는 다음과 같은 동일한 선택 옵션을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-125">Note that these are the same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code to register the service with the Service Fabric runtime.</span></span> <span data-ttu-id="78ce6-126">이 자습서에서는 **Web API**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-126">For this tutorial, choose **Web API**.</span></span> <span data-ttu-id="78ce6-127">그러나 전체 웹 응용 프로그램을 구축하는 동일한 개념을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-127">However, you can apply the same concepts to building a full web application.</span></span>
   
    ![ASP.NET 프로젝트 유형 선택][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="78ce6-129">Web API 프로젝트를 만들었으면 응용 프로그램에 두 개의 서비스가 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-129">Once your Web API project is created, you should have two services in your application.</span></span> <span data-ttu-id="78ce6-130">계속해서 응용 프로그램을 구축하는 동안 똑같은 방법으로 더 많은 서비스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-130">As you continue to build your application, you can add more services in exactly the same way.</span></span> <span data-ttu-id="78ce6-131">각 서비스를 독립적으로 버전 지정 및 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-131">Each can be independently versioned and upgraded.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="78ce6-132">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="78ce6-132">Run the application</span></span>
<span data-ttu-id="78ce6-133">지금까지 수행한 작업의 결과를 살펴보려면 새 응용 프로그램을 배포하고 ASP.NET Core Web API 템플릿에서 제공하는 기본 동작을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-133">To get a sense of what we've done, let's deploy the new application and take a look at the default behavior that the ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="78ce6-134">Visual Studio에서 F5를 눌러 앱을 디버깅합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-134">Press F5 in Visual Studio to debug the app.</span></span>
2. <span data-ttu-id="78ce6-135">배포가 완료되면 Visual Studio에서 ASP.NET Web API 서비스의 루트에 브라우저를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-135">When deployment is complete, Visual Studio launches a browser to the root of the ASP.NET Web API service.</span></span> <span data-ttu-id="78ce6-136">ASP.NET Core Web API 템플릿은 루트에 대한 기본 동작을 제공하지 않으므로 브라우저에서 404 오류가 발생할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-136">The ASP.NET Core Web API template doesn't provide default behavior for the root, so you should see a 404 error in the browser.</span></span>
3. <span data-ttu-id="78ce6-137">브라우저에서 해당 위치에 `/api/values`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-137">Add `/api/values` to the location in the browser.</span></span> <span data-ttu-id="78ce6-138">이렇게 하면 Web API 템플릿에서 ValuesController `Get` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-138">This invokes the `Get` method on the ValuesController in the Web API template.</span></span> <span data-ttu-id="78ce6-139">두 개의 문자열을 포함하는 JSON 배열인 템플릿에서 제공하는 기본 응답을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-139">It returns the default response that is provided by the template--a JSON array that contains two strings:</span></span>
   
    ![ASP.NET Core Web API 템플릿에서 반환되는 기본값][browser-aspnet-template-values]
   
    <span data-ttu-id="78ce6-141">이 자습서가 끝나기 전에 이 페이지는 기본 문자열 대신 상태 저장 서비스의 가장 최신 카운터 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-141">By the end of the tutorial, this page will show the most recent counter value from our stateful service instead of the default strings.</span></span>

## <a name="connect-the-services"></a><span data-ttu-id="78ce6-142">서비스 연결</span><span class="sxs-lookup"><span data-stu-id="78ce6-142">Connect the services</span></span>
<span data-ttu-id="78ce6-143">서비스 패브릭은 신뢰할 수 있는 서비스와 유연하게 통신할 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-143">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="78ce6-144">단일 응용 프로그램 내에 TCP를 통해 액세스할 수 있는 서비스, HTTP REST API를 통해 액세스할 수 있는 다른 서비스 및 웹 소켓을 통해 액세스할 수 있는 다른 서비스가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-144">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="78ce6-145">제공되는 옵션 및 관련 장단점에 대한 배경 정보는 [서비스와의 통신](service-fabric-connect-and-communicate-with-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78ce6-145">For background on the options available and the tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="78ce6-146">이 자습서에서는 SDK에 제공된 [Service Fabric 서비스 원격](service-fabric-reliable-services-communication-remoting.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-146">In this tutorial, we use [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), provided in the SDK.</span></span>

<span data-ttu-id="78ce6-147">서비스 원격 접근 방식(원격 프로시저 호출 또는 RPC에서 모델링)에서 인터페이스를 정의하여 서비스에 대한 공용 계약의 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-147">In the Service Remoting approach (modeled on remote procedure calls or RPCs), you define an interface to act as the public contract for the service.</span></span> <span data-ttu-id="78ce6-148">해당 인터페이스를 사용하여 그런 다음 서비스와 상호 작용하기 위한 프록시 클래스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-148">Then, you use that interface to generate a proxy class for interacting with the service.</span></span>

### <a name="create-the-remoting-interface"></a><span data-ttu-id="78ce6-149">원격 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="78ce6-149">Create the remoting interface</span></span>
<span data-ttu-id="78ce6-150">상태 저장 서비스와 다른 서비스 간의 계약 역할을 수행할 인터페이스부터 만들겠습니다. 이 경우 ASP.NET Core 웹 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-150">Let's start by creating the interface to act as the contract between the stateful service and other services, in this case the ASP.NET Core web project.</span></span> <span data-ttu-id="78ce6-151">이 인터페이스는 RPC 호출을 위해 사용하는 모든 서비스에서 공유되어야 하므로 자체 클래스 라이브러리 프로젝트에 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-151">This interface must be shared by all services that use it to make RPC calls, so we'll create it in its own Class Library project.</span></span>

1. <span data-ttu-id="78ce6-152">솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **브라우저에서 해당 위치에** > **새 프로젝트**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-152">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>

2. <span data-ttu-id="78ce6-153">왼쪽의 탐색 창에서 **Visual C#** 항목을 선택한 다음 **클래스 라이브러리** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-153">Choose the **Visual C#** entry in the left navigation pane and then select the **Class Library** template.</span></span> <span data-ttu-id="78ce6-154">.NET Framework 버전이 **4.5.2**로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-154">Ensure that the .NET Framework version is set to **4.5.2**.</span></span>
   
    ![상태 저장 서비스에 대한 인터페이스 프로젝트 만들기][vs-add-class-library-project]

3. <span data-ttu-id="78ce6-156">**Microsoft.ServiceFabric.Services.Remoting** NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-156">Install the **Microsoft.ServiceFabric.Services.Remoting** NuGet package.</span></span> <span data-ttu-id="78ce6-157">NuGet 패키지 관리자에서 **Microsoft.ServiceFabric.Services.Remoting**을 검색하고 다음을 포함한 서비스 원격을 사용하는 솔루션에서 모든 프로젝트에 대해 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-157">Search for  **Microsoft.ServiceFabric.Services.Remoting** in the NuGet package manager and install it for all projects in the solution that use Service Remoting, including:</span></span>
   - <span data-ttu-id="78ce6-158">서비스 인터페이스를 포함하는 클래스 라이브러리 프로젝트</span><span class="sxs-lookup"><span data-stu-id="78ce6-158">The Class Library project that contains the service interface</span></span>
   - <span data-ttu-id="78ce6-159">상태 저장 서비스 프로젝트</span><span class="sxs-lookup"><span data-stu-id="78ce6-159">The Stateful Service project</span></span>
   - <span data-ttu-id="78ce6-160">ASP.NET Core 웹 서비스 프로젝트</span><span class="sxs-lookup"><span data-stu-id="78ce6-160">The ASP.NET Core web service project</span></span>
   
    ![서비스 NuGet 패키지 추가][vs-services-nuget-package]

4. <span data-ttu-id="78ce6-162">클래스 라이브러리에서 단일 메서드 `GetCountAsync`를 사용하여 인터페이스를 만들고, `Microsoft.ServiceFabric.Services.Remoting.IService`에서 해당 인터페이스를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-162">In the class library, create an interface with a single method, `GetCountAsync`, and extend the interface from `Microsoft.ServiceFabric.Services.Remoting.IService`.</span></span> <span data-ttu-id="78ce6-163">원격 인터페이스는 서비스 원격 인터페이스임을 나타내기 위해 이 인터페이스에서 파생되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-163">The remoting interface must derive from this interface to indicate that it is a Service Remoting interface.</span></span>
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-the-interface-in-your-stateful-service"></a><span data-ttu-id="78ce6-164">상태 저장 서비스에서 인터페이스 구현</span><span class="sxs-lookup"><span data-stu-id="78ce6-164">Implement the interface in your stateful service</span></span>
<span data-ttu-id="78ce6-165">인터페이스를 정의했으니 이제는 상태 저장 서비스를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-165">Now that we have defined the interface, we need to implement it in the stateful service.</span></span>

1. <span data-ttu-id="78ce6-166">상태 저장 서비스에서 인터페이스가 포함된 클래스 라이브러리 프로젝트에 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-166">In your stateful service, add a reference to the class library project that contains the interface.</span></span>
   
    ![상태 저장 서비스의 클래스 라이브러리 프로젝트에 참조 추가][vs-add-class-library-reference]
2. <span data-ttu-id="78ce6-168">`MyStatefulService`처럼 `StatefulService`에서 상속하는 클래스를 찾아 확장하여 `ICounter` 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-168">Locate the class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it to implement the `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. <span data-ttu-id="78ce6-169">이제 `ICounter` 인터페이스인 `GetCountAsync`에 정의된 단일 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-169">Now implement the single method that is defined in the `ICounter` interface, `GetCountAsync`.</span></span>
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-the-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="78ce6-170">서비스 원격 수신기를 사용하여 상태 저장 서비스를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-170">Expose the stateful service using a service remoting listener</span></span>
<span data-ttu-id="78ce6-171">구현된 `ICounter` 인터페이스와 함께 마지막 단계는 서비스 원격 통신 채널을 여는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-171">With the `ICounter` interface implemented, the final step is to open the Service Remoting communication channel.</span></span> <span data-ttu-id="78ce6-172">상태 저장 서비스의 경우 서비스 패브릭은 `CreateServiceReplicaListeners`라는 재정의 가능한 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-172">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="78ce6-173">이 메서드로 서비스에 사용하려는 통신 형식에 따라 하나 이상의 통신 수신기를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-173">With this method, you can specify one or more communication listeners, based on the type of communication that you want to enable for your service.</span></span>

> [!NOTE]
> <span data-ttu-id="78ce6-174">상태 비저장 서비스에 대한 통신 채널을 열기 위해 제공되는 메서드는 `CreateServiceInstanceListeners`입니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-174">The equivalent method for opening a communication channel to stateless services is called `CreateServiceInstanceListeners`.</span></span>

<span data-ttu-id="78ce6-175">이 경우에서는 기존 `CreateServiceReplicaListeners` 메서드를 바꾸고 `ServiceRemotingListener`의 인스턴스를 제공하며 이는 `ServiceProxy`을 통해 클라이언트에서 호출 가능한 RPC 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-175">In this case, we replace the existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

<span data-ttu-id="78ce6-176">`IService` 인터페이스의 `CreateServiceRemotingListener` 확장 메서드를 통해 모든 기본 설정을 사용하여 `ServiceRemotingListener`를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-176">The `CreateServiceRemotingListener` extension method on the `IService` interface allows you to easily create a `ServiceRemotingListener` with all default settings.</span></span> <span data-ttu-id="78ce6-177">이 확장 메서드를 사용하려면 `Microsoft.ServiceFabric.Services.Remoting.Runtime` 네임스페이스를 가져왔는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-177">To use this extension method, ensure you have the `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace imported.</span></span> 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-the-serviceproxy-class-to-interact-with-the-service"></a><span data-ttu-id="78ce6-178">ServiceProxy 클래스를 사용하여 서버와 상호 작용</span><span class="sxs-lookup"><span data-stu-id="78ce6-178">Use the ServiceProxy class to interact with the service</span></span>
<span data-ttu-id="78ce6-179">상태 저장 서비스는 RPC를 통한 다른 서비스에서 트래픽을 받을 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-179">Our stateful service is now ready to receive traffic from other services over RPC.</span></span> <span data-ttu-id="78ce6-180">따라서 ASP.NET 웹 서비스에서 해당 서비스와 통신하도록 코드를 추가하는 작업이 남았습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-180">So all that remains is adding the code to communicate with it from the ASP.NET web service.</span></span>

1. <span data-ttu-id="78ce6-181">ASP.NET 프로젝트에서 `ICounter` 인터페이스가 포함된 클래스 라이브러리에 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-181">In your ASP.NET project, add a reference to the class library that contains the `ICounter` interface.</span></span>

2. <span data-ttu-id="78ce6-182">앞에서 **Microsoft.ServiceFabric.Services.Remoting** NuGet 패키지를 ASP.NET 프로젝트에 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-182">Earlier you added the **Microsoft.ServiceFabric.Services.Remoting** NuGet package to the ASP.NET project.</span></span> <span data-ttu-id="78ce6-183">이 패키지는 상태 저장 서비스에 대한 RPC 호출을 만드는 데 사용하는 `ServiceProxy` 클래스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-183">This package provides the `ServiceProxy` class which you use to make RPC calls to the stateful service.</span></span> <span data-ttu-id="78ce6-184">이 NuGet 패키지가 ASP.NET Core 웹 서비스 프로젝트에 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-184">Ensure this NuGet package is installed in the ASP.NET Core web service project.</span></span>

4. <span data-ttu-id="78ce6-185">**Controllers** 폴더에서 `ValuesController` 클래스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-185">In the **Controllers** folder, open the `ValuesController` class.</span></span> <span data-ttu-id="78ce6-186">`Get` 메서드가 현재는 하드 코드된 문자열 배열 "value1" 및 "value2"만 반환하며 이 문자열은 앞서 브라우저에서 본 것과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-186">Note that the `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in the browser.</span></span> <span data-ttu-id="78ce6-187">이것을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-187">Replace this implementation with the following code:</span></span>
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    <span data-ttu-id="78ce6-188">코드의 첫 번째 줄이 핵심입니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-188">The first line of code is the key one.</span></span> <span data-ttu-id="78ce6-189">상태 저장 서비스에 ICounter 프록시를 만들려면 두 가지 정보, 즉 파티션 ID와 서비스 이름을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-189">To create the ICounter proxy to the stateful service, you need to provide two pieces of information: a partition ID and the name of the service.</span></span>
   
    <span data-ttu-id="78ce6-190">고객 ID, 우편 번호 등 사용자가 정의하는 키를 기반으로 상태를 여러 버킷으로 분류하여 상태 저장 서비스를 확장하도록 파티션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-190">You can use partitioning to scale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="78ce6-191">간단한 응용 프로그램에서 상태 저장 서비스에는 파티션이 하나밖에 없으므로 키는 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-191">In our trivial application, the stateful service only has one partition, so the key doesn't matter.</span></span> <span data-ttu-id="78ce6-192">아무 키를 입력해도 같은 파티션으로 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-192">Any key that you provide will lead to the same partition.</span></span> <span data-ttu-id="78ce6-193">서비스 분할에 대해 자세히 알아보려면 [서비스 패브릭 Reliable Services 분할 방법](service-fabric-concepts-partitioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78ce6-193">To learn more about partitioning services, see [How to partition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="78ce6-194">서비스 이름은 양식 패브릭의 URI입니다(예: /&lt;application_name&gt;/&lt;service_name&gt;).</span><span class="sxs-lookup"><span data-stu-id="78ce6-194">The service name is a URI of the form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="78ce6-195">서비스 패브릭에서는 이러한 두 가지 정보를 사용하여 요청을 보내야 하는 컴퓨터를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-195">With these two pieces of information, Service Fabric can uniquely identify the machine that requests should be sent to.</span></span> <span data-ttu-id="78ce6-196">또한 `ServiceProxy` 클래스는 상태 저장 서비스 파티션을 호스트하는 컴퓨터에 장애가 발생하여 다른 컴퓨터가 그 역할을 대신해야 하는 경우를 원활하게 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-196">The `ServiceProxy` class also seamlessly handles the case where the machine that hosts the stateful service partition fails and another machine must be promoted to take its place.</span></span> <span data-ttu-id="78ce6-197">이 추상화를 사용하면 다른 서비스를 처리하기 위한 클라이언트 코드 쓰기 작업이 훨씬 간단해집니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-197">This abstraction makes writing the client code to deal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="78ce6-198">프록시가 있으면 `GetCountAsync` 메서드만 호출하면 그 결과가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-198">Once we have the proxy, we simply invoke the `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="78ce6-199">수정된 응용 프로그램을 실행하려면 F5 키를 다시 누르면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-199">Press F5 again to run the modified application.</span></span> <span data-ttu-id="78ce6-200">이전과 마찬가지로, Visual Studio에서 자동으로 웹 프로젝트의 루트에 브라우저를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-200">As before, Visual Studio automatically launches the browser to the root of the web project.</span></span> <span data-ttu-id="78ce6-201">"api/values" 경로를 추가하면 반환되는 현재 카운터 값이 표시되야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-201">Add the "api/values" path, and you should see the current counter value returned.</span></span>
   
    ![브라우저에 표시되는 상태 저장 카운터 값][browser-aspnet-counter-value]
   
    <span data-ttu-id="78ce6-203">브라우저를 주기적으로 새로 고쳐 카운터 값 업데이트를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="78ce6-203">Refresh the browser periodically to see the counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="78ce6-204">Kestrel 및 WebListener</span><span class="sxs-lookup"><span data-stu-id="78ce6-204">Kestrel and WebListener</span></span>

<span data-ttu-id="78ce6-205">Kestrel로 알려진 기본 ASP.NET Core 웹 서버는 [현재 직접 인터넷 트래픽을 처리를 지원하지 않습니다](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span><span class="sxs-lookup"><span data-stu-id="78ce6-205">The default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span></span> <span data-ttu-id="78ce6-206">따라서 Service Fabric에 대한 ASP.NET Core 상태 비저장 서비스 템플릿은 기본적으로 [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-206">As a result, the ASP.NET Core stateless service template for Service Fabric uses [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="78ce6-207">Service Fabric의 Kestrel 및 WebListener에 대한 자세한 내용은 [Service Fabric Reliable Services의 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78ce6-207">To learn more about Kestrel and WebListener in Service Fabric services, please refer to [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

## <a name="connecting-to-a-reliable-actor-service"></a><span data-ttu-id="78ce6-208">Reliable Actor 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="78ce6-208">Connecting to a Reliable Actor service</span></span>
<span data-ttu-id="78ce6-209">이 자습서는 상태 저장 서비스와 통신하는 웹 프런트 엔드를 추가하는 방법에 초점을 맞추고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-209">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="78ce6-210">그러나 매우 비슷한 모델에 따라 행위자와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-210">However, you can follow a very similar model to talk to actors.</span></span> <span data-ttu-id="78ce6-211">사용자가 Reliable Actor 프로젝트를 만들면 Visual Studio에서 자동으로 인터페이스 프로젝트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-211">When you create a Reliable Actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="78ce6-212">사용자는 이 인터페이스를 사용하여 웹 프로젝트에 행위자와 통신하기 위한 행위자 프록시를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-212">You can use that interface to generate an actor proxy in the web project to communicate with the actor.</span></span> <span data-ttu-id="78ce6-213">통신 채널은 자동으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-213">The communication channel is provided automatically.</span></span> <span data-ttu-id="78ce6-214">따라서 사용자는 이 자습서에서 상태 저장 서비스에 대해 수행한 대로 `ServiceRemotingListener`를 설정하기 위해 동일한 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-214">So you do not need to do anything that is equivalent to establishing a `ServiceRemotingListener` like you did for the stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="78ce6-215">웹 서비스가 로컬 클러스터에서 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="78ce6-215">How web services work on your local cluster</span></span>
<span data-ttu-id="78ce6-216">일반적으로 로컬 클러스터에 배포된 다중 컴퓨터 클러스터에 동일한 Service Fabric 응용 프로그램을 정확히 배포할 수 있고 응용 프로그램이 예상대로 작동할 것으로 확신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-216">In general, you can deploy exactly the same Service Fabric application to a multi-machine cluster that you deployed on your local cluster and be highly confident that it works as you expect.</span></span> <span data-ttu-id="78ce6-217">왜냐하면 로컬 클러스터가 단일 컴퓨터로 축소된 5 노드 구성이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-217">This is because your local cluster is simply a five-node configuration that is collapsed to a single machine.</span></span>

<span data-ttu-id="78ce6-218">그러나 웹 서비스는 결정적인 차이가 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-218">When it comes to web services, however, there is one key nuance.</span></span> <span data-ttu-id="78ce6-219">Azure처럼 클러스터가 부하 분산 장치 뒤에 있는 경우 모든 컴퓨터에 웹 서비스를 배포해야 합니다. 부하 분산 장치가 단순히 라운드 로빈 방식으로 컴퓨터 간에 트래픽을 분산하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-219">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since the load balancer simply round-robins traffic across the machines.</span></span> <span data-ttu-id="78ce6-220">서비스에 대한 `InstanceCount`를 특수 값인 "-1"로 설정하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-220">You can do this by setting the `InstanceCount` for the service to the special value of "-1".</span></span>

<span data-ttu-id="78ce6-221">반면 웹 서비스를 로컬로 실행하는 경우 서비스의 인스턴스가 하나만 실행하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-221">By contrast, when you run a web service locally, you need to ensure that only one instance of the service is running.</span></span> <span data-ttu-id="78ce6-222">그렇지 않으면 동일한 경로 및 포트에서 수신하는 여러 프로세스에서 충돌을 일으킵니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-222">Otherwise, you run into conflicts from multiple processes that are listening on the same path and port.</span></span> <span data-ttu-id="78ce6-223">결과적으로 로컬 배포에 대해 웹 서비스 인스턴스 수를 "1"로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-223">As a result, the web service instance count should be set to "1" for local deployments.</span></span>

<span data-ttu-id="78ce6-224">여러 환경에 대한 여러 가지 구성 방법을 알아보려면 [여러 환경에 대한 응용 프로그램 매개 변수 관리](service-fabric-manage-multiple-environment-app-configuration.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78ce6-224">To learn how to configure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="78ce6-225">다음 단계</span><span class="sxs-lookup"><span data-stu-id="78ce6-225">Next steps</span></span>
<span data-ttu-id="78ce6-226">이제 ASP.NET Core를 통해 웹 프런트가 응용 프로그램에 사용할 수 있게 설정되었으므로 ASP.NET Core가 Service Fabric과 작동하는 방식을 깊이 있게 이해하도록 [Service Fabric Reliable Services의 ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="78ce6-226">Now that you have a web front end set up for your application with ASP.NET Core, learn more about [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) for an in-depth understanding of how ASP.NET Core works with Service Fabric.</span></span>

<span data-ttu-id="78ce6-227">다음에는 일반적으로 [서비스와 통신하는 방법에 대해 자세히 알아봄으로써](service-fabric-connect-and-communicate-with-services.md) Service Fabric에서 서비스 통신이 작동하는 방식을 완전히 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-227">Next, [learn more about communicating with services](service-fabric-connect-and-communicate-with-services.md) in general to get a complete picture of how service communication works in Service Fabric.</span></span>

<span data-ttu-id="78ce6-228">서비스 통신의 작동 방식을 잘 알고 있는 경우 [Azure에서 클러스터를 만들고 응용 프로그램을 클라우드에 배포](service-fabric-cluster-creation-via-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="78ce6-228">Once you have a good understanding of how service communication works, [create a cluster in Azure and deploy your application to the cloud](service-fabric-cluster-creation-via-portal.md).</span></span>

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
