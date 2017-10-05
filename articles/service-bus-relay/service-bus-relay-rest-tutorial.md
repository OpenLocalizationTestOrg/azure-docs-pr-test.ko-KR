---
title: "Azure Relay를 사용하는 Service Bus REST 자습서 | Microsoft Docs"
description: "REST 기반 인터페이스를 표시하는 간단한 Azure Service Bus 릴레이 호스트 응용 프로그램을 구축합니다."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: 0db9dbd2d2743907e3f0b259228201d4f5d0c3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="f4ceb-103">Azure WCF 릴레이 REST 자습서</span><span class="sxs-lookup"><span data-stu-id="f4ceb-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="f4ceb-104">이 자습서에서는 REST 기반 인터페이스를 표시하는 간단한 Azure Relay 호스트 응용 프로그램을 구축하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-104">This tutorial describes how to build a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="f4ceb-105">REST는 웹 브라우저와 같은 웹 클라이언트가 HTTP 요청을 통해 서비스 버스 API에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-105">REST enables a web client, such as a web browser, to access the Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="f4ceb-106">자습서에서는 WCF(Windows Communication Foundation) REST 프로그래밍 모델을 사용하여 서비스 버스에 REST 서비스를 구축합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-106">The tutorial uses the Windows Communication Foundation (WCF) REST programming model to construct a REST service on Service Bus.</span></span> <span data-ttu-id="f4ceb-107">자세한 내용은 WCF 설명서의 [WCF REST 프로그래밍 모델](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) 및 [서비스 디자인 및 구현](/dotnet/framework/wcf/designing-and-implementing-services)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in the WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="f4ceb-108">단계 1: 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="f4ceb-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="f4ceb-109">Azure에서 릴레이 기능 사용을 시작하려면 먼저 서비스 네임스페이스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-109">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="f4ceb-110">네임스페이스는 응용 프로그램 내에서 Azure 리소스의 주소를 지정하기 위한 범위 컨테이너를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="f4ceb-111">[여기의 지침](relay-create-namespace-portal.md)을 따라 릴레이 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-111">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-to-use-with-azure-relay"></a><span data-ttu-id="f4ceb-112">2단계: Azure Relay와 사용할 REST 기반 WCF 서비스 계약 정의</span><span class="sxs-lookup"><span data-stu-id="f4ceb-112">Step 2: Define a REST-based WCF service contract to use with Azure Relay</span></span>

<span data-ttu-id="f4ceb-113">WCF REST 스타일 서비스를 만들 때 계약을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-113">When you create a WCF REST-style service, you must define the contract.</span></span> <span data-ttu-id="f4ceb-114">계약은 호스트가 지원하는 작업을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-114">The contract specifies what operations the host supports.</span></span> <span data-ttu-id="f4ceb-115">서비스 작업은 웹 서비스 메서드로 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="f4ceb-116">계약은 C++, C#, 또는 Visual Basic 인터페이스를 정의하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="f4ceb-117">인터페이스의 각 메서드는 특정 서비스 작업에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-117">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="f4ceb-118">[ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) 특성은 각 인터페이스에 반드시 적용되어야 하고, [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) 속성은 각 작업에 반드시 적용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-118">The [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied to each interface, and the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied to each operation.</span></span> <span data-ttu-id="f4ceb-119">[OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx)을 포함하는 인터페이스의 메서드에 [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx)이 없으면 해당 메서드는 드러나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-119">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="f4ceb-120">이 작업에 사용되는 코드는 과정을 수행하면서 예제에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-120">The code used for these tasks is shown in the example following the procedure.</span></span>

<span data-ttu-id="f4ceb-121">WCF 계약과 REST 스타일 계약의 주요 차이는 [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx)에 대한 속성의 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-121">The primary difference between a WCF contract and a REST-style contract is the addition of a property to the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="f4ceb-122">이 속성을 사용하면 인터페이스의 메서드를 인터페이스 반대편의 메서드로 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-122">This property enables you to map a method in your interface to a method on the other side of the interface.</span></span> <span data-ttu-id="f4ceb-123">이 경우 [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx)을 사용하여 메서드를 HTTP GET으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) to link a method to HTTP GET.</span></span> <span data-ttu-id="f4ceb-124">이렇게 하면 서비스 버스가 인터페이스로 보낸 명령을 정확하게 검색하고 해석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-124">This allows Service Bus to accurately retrieve and interpret commands sent to the interface.</span></span>

### <a name="to-create-a-contract-with-an-interface"></a><span data-ttu-id="f4ceb-125">인터페이스와 함께 계약을 만들려면</span><span class="sxs-lookup"><span data-stu-id="f4ceb-125">To create a contract with an interface</span></span>

1. <span data-ttu-id="f4ceb-126">Visual Studio를 관리자 권한으로 열고 **시작 메뉴**에서 프로그램을 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-126">Open Visual Studio as an administrator: right-click the program in the **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="f4ceb-127">새 콘솔 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-127">Create a new console application project.</span></span> <span data-ttu-id="f4ceb-128">**파일** 메뉴를 클릭하고 **새로 만들기**와 **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-128">Click the **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="f4ceb-129">**새 프로젝트** 대화 상자에서 **Visual C#**을 클릭하고 **콘솔 응용 프로그램** 템플릿을 선택하여 **ImageListener**로 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-129">In the **New Project** dialog box, click **Visual C#**, select the **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="f4ceb-130">기본 **위치**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-130">Use the default **Location**.</span></span> <span data-ttu-id="f4ceb-131">**확인** 을 클릭하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-131">Click **OK** to create the project.</span></span>
3. <span data-ttu-id="f4ceb-132">C# 프로젝트의 경우 Visual Studio는 `Program.cs` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="f4ceb-133">이 클래스는 콘솔 응용 프로그램 프로젝트를 제대로 구축하는데 필요한 빈 `Main()` 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-133">This class contains an empty `Main()` method, required for a console application project to build correctly.</span></span>
4. <span data-ttu-id="f4ceb-134">Service Bus에 참조를 추가하고 Service Bus NuGet 패키지를 설치하여 프로젝트에 **System.ServiceModel.dll**를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-134">Add references to Service Bus and **System.ServiceModel.dll** to the project by installing the Service Bus NuGet package.</span></span> <span data-ttu-id="f4ceb-135">이 패키지는 WCF **System.ServiceModel** 뿐만 아니라 Service Bus 라이브러리에 대한 참조를 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-135">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="f4ceb-136">솔루션 탐색기에서 **ImageListener**프로젝트를 마우스 오른쪽 단추로 클릭한 다음, **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-136">In Solution Explorer, right-click the **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="f4ceb-137">**찾아보기** 탭을 클릭한 다음 `Microsoft Azure Service Bus`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-137">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="f4ceb-138">**설치**를 클릭하고 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-138">Click **Install**, and accept the terms of use.</span></span>
5. <span data-ttu-id="f4ceb-139">프로젝트에 대해 **System.ServiceModel.Web.dll**에 참조를 명시적으로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-139">You must explicitly add a reference to **System.ServiceModel.Web.dll** to the project:</span></span>
   
    <span data-ttu-id="f4ceb-140">a.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-140">a.</span></span> <span data-ttu-id="f4ceb-141">솔루션 탐색기에서 프로젝트 폴더 아래 **참조** 폴더를 마우스 오른쪽 단추로 클릭한 후 **참조 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-141">In Solution Explorer, right-click the **References** folder under the project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="f4ceb-142">b.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-142">b.</span></span> <span data-ttu-id="f4ceb-143">**참조 추가** 대화 상자에서 왼쪽의 **프레임워크** 탭을 클릭하고 **검색** 상자에 **System.ServiceModel.Web**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-143">In the **Add Reference** dialog box, click the **Framework** tab on the left-hand side and in the **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="f4ceb-144">**System.ServiceModel.Web** 확인란을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-144">Select the **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="f4ceb-145">Program.cs 파일 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-145">Add the following `using` statements at the top of the Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="f4ceb-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx)은 WCF의 기본 기능에 프로그래밍 방식의 액세스를 가능하게 하는 네임스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables programmatic access to basic features of WCF.</span></span> <span data-ttu-id="f4ceb-147">WCF 릴레이는 WCF의 많은 개체와 특성을 사용하여 서비스 계약을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-147">WCF Relay uses many of the objects and attributes of WCF to define service contracts.</span></span> <span data-ttu-id="f4ceb-148">이 네임스페이스는 대부분의 릴레이 응용 프로그램에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="f4ceb-149">마찬가지로 [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx)는 채널을 정의하는데 도움을 주는데, 이 개체를 통해 Azure Relay 및 클라이언트 웹 브라우저와 통신하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define the channel, which is the object through which you communicate with Azure Relay and the client web browser.</span></span> <span data-ttu-id="f4ceb-150">마지막으로 [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx)에는 웹 기반 응용 프로그램을 만들 수 있도록 하는 형식이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains the types that enable you to create web-based applications.</span></span>
7. <span data-ttu-id="f4ceb-151">`ImageListener` 네임스페이스의 이름을 **Microsoft.ServiceBus.Samples**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-151">Rename the `ImageListener` namespace to **Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="f4ceb-152">네임스페이스 선언의 중괄호를 연 바로 다음에는 새 인터페이스를 정의하여 이름을 **IImageContract**로 정하고 해당 인터페이스에 **ServiceContractAttribute** 특성의 값을 `http://samples.microsoft.com/ServiceModel/Relay/`로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-152">Directly after the opening curly brace of the namespace declaration, define a new interface named **IImageContract** and apply the **ServiceContractAttribute** attribute to the interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="f4ceb-153">네임스페이스 값은 코드 전반에 사용하는 네임스페이스에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-153">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="f4ceb-154">네임스페이스 값은 이 계약에 대한 고유 식별자로 사용되며 버전 정보가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-154">The namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="f4ceb-155">자세한 내용은 [서비스 버전 관리](http://go.microsoft.com/fwlink/?LinkID=180498)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="f4ceb-156">네임스페이스를 명시적으로 지정하면 기본 네임스페이스 값이 계약 이름에 추가되는 경우를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-156">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="f4ceb-157">`IImageContract` 인터페이스 내에서 `IImageContract` 계약이 인터페이스에 노출하는 단일 작업에 대한 메서드를 선언하고 공개 서비스 버스 계약의 일부로 노출하려는 메서드에 `OperationContractAttribute` 특성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-157">Within the `IImageContract` interface, declare a method for the single operation the `IImageContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="f4ceb-158">**OperationContract** 특성에 **WebGet** 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-158">In the **OperationContract** attribute, add the **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="f4ceb-159">그렇게 하면 릴레이 서비스가 HTTP GET 요청을 `GetImage`로 라우팅할 수 있고 `GetImage`의 반환 값을 HTTP GETRESPONSE 회신으로 해석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-159">Doing so enables the relay service to route HTTP GET requests to `GetImage`, and to translate the return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="f4ceb-160">자습서 뒷부분에서 웹 브라우저를 사용하여 이 메서드를 액세스하고 브라우저에 이미지를 표시할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-160">Later in the tutorial, you will use a web browser to access this method, and to display the image in the browser.</span></span>
11. <span data-ttu-id="f4ceb-161">`IImageContract` 정의 바로 다음에 `IImageContract` 및 `IClientChannel` 인터페이스로부터 상속되는 채널을 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-161">Directly after the `IImageContract` definition, declare a channel that inherits from both the `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="f4ceb-162">채널은 서비스 및 클라이언트가 서로 정보를 전달하는 WCF 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-162">A channel is the WCF object through which the service and client pass information to each other.</span></span> <span data-ttu-id="f4ceb-163">나중에 호스트 응용 프로그램에서 채널을 만들 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-163">Later, you will create the channel in your host application.</span></span> <span data-ttu-id="f4ceb-164">Azure Relay는 이 채널을 사용하여 브라우저의 HTTP GET 요청을 **GetImage** 구현으로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-164">Azure Relay then uses this channel to pass the HTTP GET requests from the browser to your **GetImage** implementation.</span></span> <span data-ttu-id="f4ceb-165">릴레이는 이 채널을 사용하여 **GetImage** 반환 값을 가져와서 클라이언트 브라우저에 대한 HTTP GETRESPONSE로 해석하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-165">The relay also uses the channel to take the **GetImage** return value and translate it into an HTTP GETRESPONSE for the client browser.</span></span>
12. <span data-ttu-id="f4ceb-166">**빌드** 메뉴에서 **솔루션 빌드**를 클릭하여 지금까지 수행한 작업이 정확한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-166">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="f4ceb-167">예제</span><span class="sxs-lookup"><span data-stu-id="f4ceb-167">Example</span></span>
<span data-ttu-id="f4ceb-168">다음 코드는 WCF 릴레이 계약을 정의하는 기본 인터페이스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-168">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-to-use-service-bus"></a><span data-ttu-id="f4ceb-169">3단계: 서비스 버스를 사용할 REST 기반 WCF 서비스 계약을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-169">Step 3: Implement a REST-based WCF service contract to use Service Bus</span></span>
<span data-ttu-id="f4ceb-170">REST 스타일 WCF 릴레이 서비스를 만들려면 첫째로 계약을 만들어야 하는데, 계약은 인터페이스를 사용하여 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-170">Creating a REST-style WCF Relay service requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="f4ceb-171">다음 단계는 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-171">The next step is to implement the interface.</span></span> <span data-ttu-id="f4ceb-172">이 과정 중에 사용자 정의 **IImageContract** 인터페이스를 구현하는 **ImageService**라는 클래스가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-172">This involves creating a class named **ImageService** that implements the user-defined **IImageContract** interface.</span></span> <span data-ttu-id="f4ceb-173">계약을 구현한 후 App.config 파일을 사용하여 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-173">After you implement the contract, you then configure the interface using an App.config file.</span></span> <span data-ttu-id="f4ceb-174">구성 파일은 서비스 이름, 계약 이름, 릴레이 서비스와 통신에 사용되는 프로토콜 유형과 같은 응용 프로그램에 필요한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-174">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="f4ceb-175">이 작업에 사용되는 코드는 과정을 수행하면서 예제에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-175">The code used for these tasks is provided in the example following the procedure.</span></span>

<span data-ttu-id="f4ceb-176">이전 단계에서와 마찬가지로 REST 스타일 계약과 WCF 릴레이 계약의 구현 간에는 거의 차이가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-176">As with the previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="to-implement-a-rest-style-service-bus-contract"></a><span data-ttu-id="f4ceb-177">REST 스타일 서비스 버스 계약을 구현하려면</span><span class="sxs-lookup"><span data-stu-id="f4ceb-177">To implement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="f4ceb-178">**IImageContract** 인터페이스의 정의 바로 다음에 **ImageService**라는 새 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-178">Create a new class named **ImageService** directly after the definition of the **IImageContract** interface.</span></span> <span data-ttu-id="f4ceb-179">**ImageService** 클래스는 **IImageContract** 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-179">The **ImageService** class implements the **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="f4ceb-180">다른 인터페이스 구현과 유사하게, 다른 파일에 정의를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-180">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="f4ceb-181">하지만 이 자습서의 경우 구현은 인터페이스 정의 및 `Main()` 메서드와 동일한 파일에서 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-181">However, for this tutorial, the implementation appears in the same file as the interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="f4ceb-182">[ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) 특성을 **IImageService** 클래스에 적용하여 클래스가 WCF 계약의 구현이라는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-182">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the **IImageService** class to indicate that the class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="f4ceb-183">앞에서 설명한 바와 같이 이 네임스페이스는 기존의 네임스페이스가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="f4ceb-184">대신, 계약을 식별하는 WCF 아키텍처의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-184">Instead, it is part of the WCF architecture that identifies the contract.</span></span> <span data-ttu-id="f4ceb-185">자세한 내용은 WCF 설명서의 [데이터 계약 이름](https://msdn.microsoft.com/library/ms731045.aspx) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-185">For more information, see the [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in the WCF documentation.</span></span>
3. <span data-ttu-id="f4ceb-186">.jpg 이미지를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-186">Add a .jpg image to your project.</span></span>  
   
    <span data-ttu-id="f4ceb-187">이것은 서비스가 수신 브라우저에 표시하는 그림입니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-187">This is a picture that the service displays in the receiving browser.</span></span> <span data-ttu-id="f4ceb-188">프로젝트를 마우스 오른쪽 단추로 클릭한 후 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="f4ceb-189">그 다음 **기존 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-189">Then click **Existing Item**.</span></span> <span data-ttu-id="f4ceb-190">**기존 항목 추가** 대화 상자를 사용하여 적절한 .jpg을 찾은 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-190">Use the **Add Existing Item** dialog box to browse to an appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="f4ceb-191">파일을 추가할 때 **파일 이름:** 필드 옆의 드롭다운 목록에서 **모든 파일**이 반드시 선택되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-191">When adding the file, make sure that **All Files** is selected in the drop-down list next to the **File name:** field.</span></span> <span data-ttu-id="f4ceb-192">이 자습서의 나머지 부분에서는 이미지의 이름을 "image.jpg"로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-192">The rest of this tutorial assumes that the name of the image is "image.jpg".</span></span> <span data-ttu-id="f4ceb-193">다른 파일이 있으면 이미지 이름을 변경하거나 보완하도록 코드를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-193">If you have a different file, you will have to rename the image, or change your code to compensate.</span></span>
4. <span data-ttu-id="f4ceb-194">실행 중인 서비스가 이미지 파일을 반드시 찾게 하려면 **솔루션 탐색기**에서 이미지 파일을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-194">To make sure that the running service can find the image file, in **Solution Explorer** right-click the image file, then click **Properties**.</span></span> <span data-ttu-id="f4ceb-195">**속성** 창에서 **출력 디렉터리로 복사**를 **변경된 내용만 복사**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-195">In the **Properties** pane, set **Copy to Output Directory** to **Copy if newer**.</span></span>
5. <span data-ttu-id="f4ceb-196">프로젝트에 대한 **System.Drawing.dll** 어셈블리에 참고를 추가하고 다음 연결된 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-196">Add a reference to the **System.Drawing.dll** assembly to the project, and also add the following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="f4ceb-197">**ImageService** 클래스에서 비트맵을 로드하는 다음과 같은 생성자를 추가하고 클라이언트 브라우저로 보낼 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-197">In the **ImageService** class, add the following constructor that loads the bitmap and prepares to send it to the client browser.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. <span data-ttu-id="f4ceb-198">이전 코드 바로 다음에 이미지를 포함하는 HTTP 메시지를 반환하기 위해 **ImageService** 클래스에 다음과 같은 **GetImage** 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-198">Directly after the previous code, add the following **GetImage** method in the **ImageService** class to return an HTTP message that contains the image.</span></span>
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    <span data-ttu-id="f4ceb-199">이 구현은 **MemoryStream**을 사용하여 이미지를 가져오고 브라우저로의 스트리밍을 위해 준비시킵니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-199">This implementation uses **MemoryStream** to retrieve the image and prepare it for streaming to the browser.</span></span> <span data-ttu-id="f4ceb-200">스트림 위치는 0에서 시작하고 스트림 콘텐츠를 jpeg로 선언하고 정보를 스트리밍합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-200">It starts the stream position at zero, declares the stream content as a jpeg, and streams the information.</span></span>
8. <span data-ttu-id="f4ceb-201">**빌드** 메뉴에서 **솔루션 빌드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-201">From the **Build** menu, click **Build Solution**.</span></span>

### <a name="to-define-the-configuration-for-running-the-web-service-on-service-bus"></a><span data-ttu-id="f4ceb-202">서비스 버스에서 웹 서비스를 실행하기 위한 구성을 정의하려면</span><span class="sxs-lookup"><span data-stu-id="f4ceb-202">To define the configuration for running the web service on Service Bus</span></span>
1. <span data-ttu-id="f4ceb-203">**솔루션 탐색기**에서 **App.config**를 두 번 클릭하여 Visual Studio 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-203">In **Solution Explorer**, double-click **App.config** to open it in the Visual Studio editor.</span></span>
   
    <span data-ttu-id="f4ceb-204">**App.config** 파일에는 서비스 이름, 끝점(즉, 클라이언트와 호스트가 서로 통신하도록 Azure Relay가 노출하는 위치) 및 바인딩(통신에 사용되는 프로토콜 유형)이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-204">The **App.config** file includes the service name, endpoint (that is, the location Azure Relay exposes for clients and hosts to communicate with each other), and binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="f4ceb-205">여기서 주요 차이점은 구성된 서비스 끝점이 [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) 바인딩을 참조한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-205">The main difference here is that the configured service endpoint refers to a [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="f4ceb-206">`<system.serviceModel>` XML 요소는 하나 이상의 서비스를 정의하는 WCF 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-206">The `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="f4ceb-207">여기서 서비스 이름 및 끝점을 정의하는데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-207">Here, it is used to define the service name and endpoint.</span></span> <span data-ttu-id="f4ceb-208">`<system.serviceModel>` 요소의 아래에(여전히 `<system.serviceModel>` 내에서) 다음과 같은 콘텐츠를 포함하는 `<bindings>` 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-208">At the bottom of the `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has the following content.</span></span> <span data-ttu-id="f4ceb-209">이것은 응용 프로그램에서 사용되는 바인딩을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-209">This defines the bindings used in the application.</span></span> <span data-ttu-id="f4ceb-210">여러 바인딩을 정의할 수 있지만 이 자습서에서는 하나만 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    <span data-ttu-id="f4ceb-211">이전 코드는 WCF 릴레이 [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) 바인딩과 **relayClientAuthenticationType** 세트를 **None**으로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-211">The previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set to **None**.</span></span> <span data-ttu-id="f4ceb-212">이 설정은 이 바인딩을 사용하는 끝점에 클라이언트 자격 증명이 필요 없다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="f4ceb-213">`<bindings>` 요소 다음에 `<services>` 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-213">After the `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="f4ceb-214">바인딩과 유사하게 단일 구성 파일 내에 여러 서비스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-214">Similar to the bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="f4ceb-215">하지만 이 자습서에서는 하나만 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-215">However, for this tutorial, you define only one.</span></span>
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    <span data-ttu-id="f4ceb-216">이 단계는 이전에 정의된 기본 **webHttpRelayBinding**을 사용하는 서비스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-216">This step configures a service that uses the previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="f4ceb-217">기본 **sbTokenProvider**도 사용하며, 이것은 다음 단계에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-217">It also uses the default **sbTokenProvider**, which is defined in the next step.</span></span>
4. <span data-ttu-id="f4ceb-218">`<services>` 요소 다음으로 다음과 같은 콘텐츠로 `<behaviors>` 요소를 만들고, "SAS_KEY"를 [Azure Portal][Azure portal]로부터 이전에 확보한 *공유 액세스 서명*(SAS) 키로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-218">After the `<services>` element, create a `<behaviors>` element with the following content, replacing "SAS_KEY" with the *Shared Access Signature* (SAS) key you previously obtained from the [Azure portal][Azure portal].</span></span>
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. <span data-ttu-id="f4ceb-219">계속 App.config의 `<appSettings>` 요소에서 연결 문자열 값을 포털에서 이전에 얻은 전체 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-219">Still in App.config, in the `<appSettings>` element, replace the entire connection string value with the connection string you previously obtained from the portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="f4ceb-220">**빌드** 메뉴에서 **솔루션 빌드**를 클릭하여 전체 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-220">From the **Build** menu, click **Build Solution** to build the entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="f4ceb-221">예</span><span class="sxs-lookup"><span data-stu-id="f4ceb-221">Example</span></span>
<span data-ttu-id="f4ceb-222">다음 코드는 **WebHttpRelayBinding** 바인딩을 사용하여 Service Bus에서 실행되는 REST 기반 서비스에 대한 계약 및 서비스 구현을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-222">The following code shows the contract and service implementation for a REST-based service that is running on  Service Bus using the **WebHttpRelayBinding** binding.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="f4ceb-223">다음 예제에서는 서비스와 관련된 App.config 파일을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-223">The following example shows the App.config file associated with the service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove the ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-the-rest-based-wcf-service-to-use-azure-relay"></a><span data-ttu-id="f4ceb-224">4단계: Azure Relay를 사용하기 위해 REST 기반 WCF 서비스를 호스팅</span><span class="sxs-lookup"><span data-stu-id="f4ceb-224">Step 4: Host the REST-based WCF service to use Azure Relay</span></span>
<span data-ttu-id="f4ceb-225">이 단계에서는 WCF 릴레이와 함께 콘솔 응용 프로그램을 사용하여 웹 서비스를 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-225">This step describes how to run a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="f4ceb-226">이 단계에서 작성되는 전체 코드는 과정을 수행하면서 예제에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-226">A complete listing of the code written in this step is provided in the example following the procedure.</span></span>

### <a name="to-create-a-base-address-for-the-service"></a><span data-ttu-id="f4ceb-227">서비스에 대한 기본 주소를 만들려면</span><span class="sxs-lookup"><span data-stu-id="f4ceb-227">To create a base address for the service</span></span>
1. <span data-ttu-id="f4ceb-228">`Main()` 함수 선언에서 프로젝트의 네임스페이스를 저장할 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-228">In the `Main()` function declaration, create a variable to store the namespace of your project.</span></span> <span data-ttu-id="f4ceb-229">`yourNamespace`를 이전에 만든 릴레이 네임스페이스의 이름으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-229">Make sure to replace `yourNamespace` with the name of the Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="f4ceb-230">서비스 버스는 네임스페이스 이름을 사용하여 고유 URI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-230">Service Bus uses the name of your namespace to create a unique URI.</span></span>
2. <span data-ttu-id="f4ceb-231">네임스페이스를 기반으로 하는 서비스 기본 주소에 대한 `Uri` 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-231">Create a `Uri` instance for the base address of the service that is based on the namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="to-create-and-configure-the-web-service-host"></a><span data-ttu-id="f4ceb-232">웹 서비스 호스트를 만들고 구성하려면</span><span class="sxs-lookup"><span data-stu-id="f4ceb-232">To create and configure the web service host</span></span>
* <span data-ttu-id="f4ceb-233">이 섹션 앞부분에서 만든 URI 주소를 사용하여 웹 서비스 호스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-233">Create the web service host, using the URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="f4ceb-234">서비스 호스트는 호스트 응용 프로그램을 인스턴스화하는 WCF 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-234">The service host is the WCF object that instantiates the host application.</span></span> <span data-ttu-id="f4ceb-235">이 예제는 만들려는 호스트의 형식(**ImageService**)을 전달하고 호스트 응용 프로그램을 노출하려는 주소를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-235">This example passes it the type of host you want to create (an **ImageService**), and also the address at which you want to expose the host application.</span></span>

### <a name="to-run-the-web-service-host"></a><span data-ttu-id="f4ceb-236">웹 서비스 호스트를 실행하려면</span><span class="sxs-lookup"><span data-stu-id="f4ceb-236">To run the web service host</span></span>
1. <span data-ttu-id="f4ceb-237">서비스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-237">Open the service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="f4ceb-238">이제 서비스가 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-238">The service is now running.</span></span>
2. <span data-ttu-id="f4ceb-239">서비스가 실행 중임을 나타내고 서비스를 중지하는 방법을 알리는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-239">Display a message indicating that the service is running, and how to stop the service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy the following address into a browser to see the image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="f4ceb-240">완료되면 서비스 호스트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-240">When finished, close the service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="f4ceb-241">예</span><span class="sxs-lookup"><span data-stu-id="f4ceb-241">Example</span></span>
<span data-ttu-id="f4ceb-242">다음 예제는 자습서에 포함된 이전 단계의 구현 및 서비스 계약을 포함하고 콘솔 응용 프로그램에 서비스를 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-242">The following example includes the service contract and implementation from previous steps in the tutorial and hosts the service in a console application.</span></span> <span data-ttu-id="f4ceb-243">다음 코드를 이름이 ImageListener.exe인 실행 파일로 컴파일 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-243">Compile the following code into an executable named ImageListener.exe.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy the following address into a browser to see the image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-the-code"></a><span data-ttu-id="f4ceb-244">코드 컴파일</span><span class="sxs-lookup"><span data-stu-id="f4ceb-244">Compiling the code</span></span>
<span data-ttu-id="f4ceb-245">솔루션을 빌드한 후 다음을 수행하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-245">After building the solution, do the following to run the application:</span></span>

1. <span data-ttu-id="f4ceb-246">**F5** 키를 누르거나 실행 파일 위치(ImageListener\bin\Debug\ImageListener.exe)로 이동하여 서비스를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-246">Press **F5**, or browse to the executable file location (ImageListener\bin\Debug\ImageListener.exe), to run the service.</span></span> <span data-ttu-id="f4ceb-247">다음 단계를 수행하는 데 필요하므로 앱을 실행 중인 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-247">Keep the app running, as it's required to perform the next step.</span></span>
2. <span data-ttu-id="f4ceb-248">이미지를 보려면 명령 프롬프트에서 주소를 복사하여 브라우저로 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-248">Copy and paste the address from the command prompt into a browser to see the image.</span></span>
3. <span data-ttu-id="f4ceb-249">완료되면 명령 프롬프트 창에서 **Enter** 키를 눌러 앱을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-249">When you are finished, press **Enter** in the command prompt window to close the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4ceb-250">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4ceb-250">Next steps</span></span>
<span data-ttu-id="f4ceb-251">이제 서비스 버스 릴레이를 사용하는 응용 프로그램을 빌드했습니다. Azure Relay에 대한 자세한 정보는 다음 문서를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="f4ceb-251">Now that you've built an application that uses the Service Bus relay service, see the following articles to learn more about Azure Relay:</span></span>

* [<span data-ttu-id="f4ceb-252">Azure Service Bus 아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="f4ceb-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="f4ceb-253">Azure Relay 개요</span><span class="sxs-lookup"><span data-stu-id="f4ceb-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="f4ceb-254">.NET과 함께 WCF 릴레이 서비스를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="f4ceb-254">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
