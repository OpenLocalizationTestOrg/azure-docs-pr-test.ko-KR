---
title: "Azure Service Bus WCF 릴레이 자습서 | Microsoft Docs"
description: "WCF Relay를 사용하여 Service Bus 클라이언트 응용 프로그램과 서비스를 빌드합니다."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 5347bf85cad32b59677369d51a1f36529aef6662
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="b3719-103">Azure WCF 릴레이 자습서</span><span class="sxs-lookup"><span data-stu-id="b3719-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="b3719-104">이 자습서에서는 Azure Relay를 사용하여 WCF 릴레이 클라이언트 응용 프로그램 및 서비스를 빌드하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-104">This tutorial describes how to build a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="b3719-105">[Service Bus 메시징](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging)을 사용하는 유사한 자습서는 [Service Bus 큐 시작](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3719-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="b3719-106">이 자습서를 통해 WCF 릴레이 클라이언트 및 서비스 응용 프로그램을 만드는 데 필요한 단계를 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-106">Working through this tutorial gives you an understanding of the steps that are required to create a WCF Relay client and service application.</span></span> <span data-ttu-id="b3719-107">기존 WCF 대응처럼 서비스는 하나 이상의 끝점을 노출하는 구문으로, 각각 하나 이상의 서비스 작업을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="b3719-108">서비스 끝점은 서비스를 찾을 수 있는 주소, 클라이언트가 서비스와 통신해야 하는 정보가 포함된 바인딩, 서비스가 클라이언트에 제공하는 기능을 정의하는 계약을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-108">The endpoint of a service specifies an address where the service can be found, a binding that contains the information that a client must communicate with the service, and a contract that defines the functionality provided by the service to its clients.</span></span> <span data-ttu-id="b3719-109">WCF와 WCF 릴레이 간의 가장 큰 차이는 끝점이 컴퓨터의 로컬이 아닌 클라우드에서 노출된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-109">The main difference between WCF and WCF Relay is that the endpoint is exposed in the cloud instead of locally on your computer.</span></span>

<span data-ttu-id="b3719-110">이 자습서의 항목을 순서대로 진행한 후에는 실행되는 서비스와, 서비스 작업을 호출할 수 있는 클라이언트가 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-110">After you work through the sequence of topics in this tutorial, you will have a running service, and a client that can invoke the operations of the service.</span></span> <span data-ttu-id="b3719-111">첫 번째 항목에서는 계정을 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-111">The first topic describes how to set up an account.</span></span> <span data-ttu-id="b3719-112">다음 단계에서는 계약을 사용하는 서비스 정의 방법, 서비스 구현 방법, 클라우드에서의 서비스 구성 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-112">The next steps describe how to define a service that uses a contract, how to implement the service, and how to configure the service in code.</span></span> <span data-ttu-id="b3719-113">또한 서비스 호스팅 및 실행 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-113">They also describe how to host and run the service.</span></span> <span data-ttu-id="b3719-114">만들어지는 서비스는 자체 호스팅되며 클라이언트와 서비스가 동일한 컴퓨터에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-114">The service that is created is self-hosted and the client and service run on the same computer.</span></span> <span data-ttu-id="b3719-115">코드 또는 구성 파일을 사용하여 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-115">You can configure the service by using either code or a configuration file.</span></span>

<span data-ttu-id="b3719-116">마지막 세 단계에서는 클라이언트 응용 프로그램 만들기 및 구성 방법과, 호스트의 기능에 액세스할 수 있는 클라이언트 만들기 및 사용 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-116">The final three steps describe how to create a client application, configure the client application, and create and use a client that can access the functionality of the host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3719-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b3719-117">Prerequisites</span></span>

<span data-ttu-id="b3719-118">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-118">To complete this tutorial, you'll need the following:</span></span>

* <span data-ttu-id="b3719-119">[Microsoft Visual Studio 2015 이상](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="b3719-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="b3719-120">이 자습서에서는 Visual Studio 2017을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="b3719-121">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="b3719-121">An active Azure account.</span></span> <span data-ttu-id="b3719-122">계정이 없는 경우 몇 분 만에 무료 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="b3719-123">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/free/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3719-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="b3719-124">서비스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="b3719-124">Create a service namespace</span></span>

<span data-ttu-id="b3719-125">첫 단계는 네임스페이스를 만들고 [SAS(공유 액세스 서명)](../service-bus-messaging/service-bus-sas.md) 키를 확보합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-125">The first step is to create a namespace, and to obtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="b3719-126">네임스페이스는 릴레이 서비스를 통해 노출되는 각 응용 프로그램에 대한 응용 프로그램 경계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-126">A namespace provides an application boundary for each application exposed through the relay service.</span></span> <span data-ttu-id="b3719-127">SAS 키는 서비스 네임스페이스가 만들어질 때 시스템에 의해 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-127">A SAS key is automatically generated by the system when a service namespace is created.</span></span> <span data-ttu-id="b3719-128">서비스 네임스페이스 및 SAS 키 조합은 Azure에 자격 증명을 제공하여 응용 프로그램에 대한 액세스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-128">The combination of service namespace and SAS key provides the credentials for Azure to authenticate access to an application.</span></span> <span data-ttu-id="b3719-129">[여기의 지침](relay-create-namespace-portal.md)을 따라 릴레이 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-129">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="b3719-130">WCF 서비스 계약 정의</span><span class="sxs-lookup"><span data-stu-id="b3719-130">Define a WCF service contract</span></span>

<span data-ttu-id="b3719-131">서비스 계약은 서비스가 지원하는 작업(메서드 또는 함수에 대한 웹 서비스 용어)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-131">The service contract specifies what operations (the web service terminology for methods or functions) the service supports.</span></span> <span data-ttu-id="b3719-132">계약은 C++, C#, 또는 Visual Basic 인터페이스를 정의하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="b3719-133">인터페이스의 각 메서드는 특정 서비스 작업에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-133">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="b3719-134">각 인터페이스에는 [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) 특성이 적용되어야 하고 각 작업에는 [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) 특성이 적용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-134">Each interface must have the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied to it, and each operation must have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied to it.</span></span> <span data-ttu-id="b3719-135">[ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) 특성이 적용된 인터페이스의 메서드에 [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) 특성이 지정되지 않은 경우 해당 메서드가 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-135">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="b3719-136">이 작업을 위한 코드는 과정을 수행하면서 예제에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-136">The code for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="b3719-137">보다 큰 규모로 진행된 계약 및 서비스 논의에 대한 자세한 내용은 WCF 설명서의 [서비스 디자인 및 구현](https://msdn.microsoft.com/library/ms729746.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3719-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in the WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="b3719-138">인터페이스와 함께 릴레이 계약 만들기</span><span class="sxs-lookup"><span data-stu-id="b3719-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="b3719-139">**시작** 메뉴의 프로그램을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택하여 Visual Studio를 관리자 권한으로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-139">Open Visual Studio as an administrator by right-clicking the program in the **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="b3719-140">새 콘솔 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-140">Create a new console application project.</span></span> <span data-ttu-id="b3719-141">**파일** 메뉴를 클릭하고 **새로 만들기**를 선택한 다음 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-141">Click the **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="b3719-142">**새 프로젝트** 대화 상자에서 **Visual C#**을 클릭합니다. **Visual C#**이 표시되지 않으면 **다른 언어**에서 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-142">In the **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="b3719-143">**콘솔 앱(.NET Framework)** 템플릿을 클릭하고 **EchoService**로 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-143">Click the **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="b3719-144">**확인** 을 클릭하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-144">Click **OK** to create the project.</span></span>

    ![][2]

3. <span data-ttu-id="b3719-145">서비스 버스 NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-145">Install the Service Bus NuGet package.</span></span> <span data-ttu-id="b3719-146">이 패키지는 WCF **System.ServiceModel** 뿐만 아니라 Service Bus 라이브러리에 대한 참조를 자동으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-146">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="b3719-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx)은 WCF의 기본 기능에 프로그래밍 방식으로 액세스할 수 있도록 하는 네임스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables you to programmatically access the basic features of WCF.</span></span> <span data-ttu-id="b3719-148">서비스 버스는 WCF의 많은 개체와 특성을 사용하여 서비스 계약을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-148">Service Bus uses many of the objects and attributes of WCF to define service contracts.</span></span>

    <span data-ttu-id="b3719-149">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-149">In Solution Explorer, right-click the project, and then click **Manage NuGet Packages...**.</span></span> <span data-ttu-id="b3719-150">**찾아보기** 탭을 클릭한 다음 `Microsoft Azure Service Bus`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-150">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="b3719-151">프로젝트 이름이 **버전** 상자에서 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-151">Ensure that the project name is selected in the **Version(s)** box.</span></span> <span data-ttu-id="b3719-152">**설치**를 클릭하고 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-152">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="b3719-153">아직 열리지 않은 경우 솔루션 탐색기에서 Program.cs 파일을 두 번 클릭하여 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-153">In Solution Explorer, double-click the Program.cs file to open it in the editor, if it is not already open.</span></span>
5. <span data-ttu-id="b3719-154">파일 맨 위에 다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-154">Add the following using statements at the top of the file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="b3719-155">네임스페이스 이름을 기본 이름인 **EchoService**에서 **Microsoft.ServiceBus.Samples**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-155">Change the namespace name from its default name of **EchoService** to **Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b3719-156">이 자습서에서는 [WCF 클라이언트 구성](#configure-the-wcf-client) 단계에서 구성 파일에 사용되는 계약 기반 관리 유형의 네임스페이스인 C# 네임스페이스 **Microsoft.ServiceBus.Samples**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-156">This tutorial uses the C# namespace **Microsoft.ServiceBus.Samples**, which is the namespace of the contract-based managed type that is used in the configuration file in the [Configure the WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="b3719-157">이 샘플을 빌드할 때 아무 네임스페이스나 지정할 수 있지만, 응용 프로그램 구성 파일에서 계약과 서비스의 네임스페이스를 그에 맞게 수정하지 않으면 자습서가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-157">You can specify any namespace you want when you build this sample; however, the tutorial will not work unless you then modify the namespaces of the contract and service accordingly, in the application configuration file.</span></span> <span data-ttu-id="b3719-158">App.config 파일에서 지정한 네임스페이스는 C# 파일에서 지정한 네임스페이스와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-158">The namespace specified in the App.config file must be the same as the namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="b3719-159">`Microsoft.ServiceBus.Samples` 네임스페이스 선언 직후 네임스페이스 안에서 이름이 `IEchoContract`인 새 인터페이스를 정의하고 네임스페이스 값이 `http://samples.microsoft.com/ServiceModel/Relay/`인 `ServiceContractAttribute` 특성을 해당 인터페이스에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-159">Directly after the `Microsoft.ServiceBus.Samples` namespace declaration, but within the namespace, define a new interface named `IEchoContract` and apply the `ServiceContractAttribute` attribute to the interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="b3719-160">네임스페이스 값은 코드 전반에 사용하는 네임스페이스에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-160">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="b3719-161">대신 네임스페이스 값은 이 계약에 대한 고유 식별자로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-161">Instead, the namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="b3719-162">네임스페이스를 명시적으로 지정하면 기본 네임스페이스 값이 계약 이름에 추가되는 경우를 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-162">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span> <span data-ttu-id="b3719-163">네임스페이스 선언 후 다음 코드를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-163">Paste the following code after the namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="b3719-164">일반적으로 서비스 계약 네임스페이스는 버전 정보가 들어있는 명명 체계를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-164">Typically, the service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="b3719-165">서비스 계약 네임 스페이스에 버전 정보를 포함하면 서비스에서 새로운 네임스페이스로 새 서비스 계약을 정의하고 새 끝점에 노출함으로써 주요 변경 내용을 분리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-165">Including version information in the service contract namespace enables services to isolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="b3719-166">이렇게 하면 클라이언트가 업데이트 없이도 기존의 서비스 계약을 지속적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-166">In this manner, clients can continue to use the old service contract without having to be updated.</span></span> <span data-ttu-id="b3719-167">버전 정보는 날짜 또는 빌드 번호로 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-167">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="b3719-168">자세한 내용은 [서비스 버전 관리](http://go.microsoft.com/fwlink/?LinkID=180498)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3719-168">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="b3719-169">이 자습서에서는 서비스 계약 네임 스페이스의 명명 체계에 버전 정보가 포함되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-169">For the purposes of this tutorial, the naming scheme of the service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="b3719-170">`IEchoContract` 인터페이스 내에서 다음과 같이 `IEchoContract` 계약이 인터페이스에 노출하는 단일 작업에 대한 메서드를 선언하고 공개 WCF 릴레이 계약의 일부로 노출하려는 메서드에 `OperationContractAttribute` 특성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-170">Within the `IEchoContract` interface, declare a method for the single operation the `IEchoContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="b3719-171">다음과 같이 `IEchoContract` 인터페이스 정의 바로 다음에 `IEchoContract` 및 `IClientChannel` 인터페이스에서 모두 상속되는 채널을 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-171">Directly after the `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also to the `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="b3719-172">채널은 호스트 및 클라이언트가 서로 정보를 전달하는 WCF 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-172">A channel is the WCF object through which the host and client pass information to each other.</span></span> <span data-ttu-id="b3719-173">나중에 두 응용 프로그램 간에 정보를 에코할 채널에 대한 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-173">Later, you will write code against the channel to echo information between the two applications.</span></span>
10. <span data-ttu-id="b3719-174">**빌드** 메뉴에서 **솔루션 빌드**를 클릭하거나 **Ctrl+Shift+B**를 눌러 지금까지 수행한 작업이 정확한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-174">From the **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="b3719-175">예제</span><span class="sxs-lookup"><span data-stu-id="b3719-175">Example</span></span>

<span data-ttu-id="b3719-176">다음 코드는 WCF 릴레이 계약을 정의하는 기본 인터페이스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-176">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="b3719-177">이제 인터페이스를 만들었으므로 해당 인터페이스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-177">Now that the interface is created, you can implement the interface.</span></span>

## <a name="implement-the-wcf-contract"></a><span data-ttu-id="b3719-178">WCF 계약 구현</span><span class="sxs-lookup"><span data-stu-id="b3719-178">Implement the WCF contract</span></span>

<span data-ttu-id="b3719-179">Azure 릴레이를 만들려면 첫째로 계약을 만들어야 하는데, 계약은 인터페이스를 사용하여 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-179">Creating an Azure relay requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="b3719-180">인터페이스를 만드는 방법에 자세한 내용은 이전 단계를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="b3719-180">For more information about creating the interface, see the previous step.</span></span> <span data-ttu-id="b3719-181">다음 단계는 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-181">The next step is to implement the interface.</span></span> <span data-ttu-id="b3719-182">여기에는 사용자 정의 `IEchoContract` 인터페이스를 구현하는 이름이 `EchoService`인 클래스를 만드는 단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-182">This involves creating a class named `EchoService` that implements the user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="b3719-183">인터페이스를 구현한 후 App.config 구성 파일을 사용하여 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-183">After you implement the interface, you then configure the interface using an App.config configuration file.</span></span> <span data-ttu-id="b3719-184">구성 파일은 서비스 이름, 계약 이름, 릴레이 서비스와 통신에 사용되는 프로토콜 유형과 같은 응용 프로그램에 필요한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-184">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="b3719-185">이 작업에 사용되는 코드는 과정을 수행하면서 예제에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-185">The code used for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="b3719-186">서비스 계약을 구현하는 방법에 대한 보다 일반적인 논의 내용을 보려면 WCF 설명서의 [서비스 계약 구현](https://msdn.microsoft.com/library/ms733764.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3719-186">For a more general discussion about how to implement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in the WCF documentation.</span></span>

1. <span data-ttu-id="b3719-187">`IEchoContract` 인터페이스 정의 바로 뒤에 이름이 `EchoService`인 클래스를 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-187">Create a new class named `EchoService` directly after the definition of the `IEchoContract` interface.</span></span> <span data-ttu-id="b3719-188">`EchoService` 클래스가 `IEchoContract` 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-188">The `EchoService` class implements the `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="b3719-189">다른 인터페이스 구현과 유사하게, 다른 파일에 정의를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-189">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="b3719-190">하지만, 이 자습서에서는 구현이 인터페이스 정의 및 `Main` 메서드와 같은 파일에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-190">However, for this tutorial, the implementation is located in the same file as the interface definition and the `Main` method.</span></span>
2. <span data-ttu-id="b3719-191">[ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) 특성을 `IEchoContract` 인터페이스에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-191">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the `IEchoContract` interface.</span></span> <span data-ttu-id="b3719-192">특성은 서비스 이름 및 네임스페이스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-192">The attribute specifies the service name and namespace.</span></span> <span data-ttu-id="b3719-193">그러면 `EchoService` 클래스는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-193">After doing so, the `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="b3719-194">`EchoService` 클래스의 `IEchoContract` 인터페이스에서 정의된 `Echo` 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-194">Implement the `Echo` method defined in the `IEchoContract` interface in the `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="b3719-195">**빌드**를 클릭한 다음 **솔루션 빌드**를 클릭하여 작업이 정확한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-195">Click **Build**, then click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="define-the-configuration-for-the-service-host"></a><span data-ttu-id="b3719-196">서비스 호스트에 대한 구성 정의</span><span class="sxs-lookup"><span data-stu-id="b3719-196">Define the configuration for the service host</span></span>

1. <span data-ttu-id="b3719-197">구성 파일은 WCF 구성 파일과 매우 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-197">The configuration file is very similar to a WCF configuration file.</span></span> <span data-ttu-id="b3719-198">여기에는 서비스 이름, 끝점(즉, 클라이언트와 호스트가 서로 통신하도록 Azure Relay가 노출하는 위치) 및 바인딩(통신에 사용되는 프로토콜 유형)이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-198">It includes the service name, endpoint (that is, the location that Azure Relay exposes for clients and hosts to communicate with each other), and the binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="b3719-199">주요 차이점은 구성된 이 서비스 끝점이 .NET Framework에 속하지 않는 [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) 바인딩을 참조한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-199">The main difference is that this configured service endpoint refers to a [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of the .NET Framework.</span></span> <span data-ttu-id="b3719-200">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding)은 서비스에서 정의한 바인딩 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-200">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of the bindings defined by the service.</span></span>
2. <span data-ttu-id="b3719-201">**솔루션 탐색기**에서 App.config 파일을 두 번 클릭하여 Visual Studio 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-201">In **Solution Explorer**, double-click the App.config file to open it in the Visual Studio editor.</span></span>
3. <span data-ttu-id="b3719-202">`<appSettings>` 요소에서 자리 표시자를 이전 단계에서 복사한 서비스 네임스페이스 및 SAS 키의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-202">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="b3719-203">`<system.serviceModel>` 태그 안에 `<services>` 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-203">Within the `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="b3719-204">단일 구성 파일 내에 여러 릴레이 응용 프로그램을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-204">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="b3719-205">그러나 이 자습서에서는 하나만 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-205">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="b3719-206">`<services>` 요소 안에서 `<service>` 요소를 추가하여 서비스의 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-206">Within the `<services>` element, add a `<service>` element to define the name of the service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="b3719-207">`<service>` 요소 안에서 끝점 계약의 위치와 해당 끝점의 바인딩 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-207">Within the `<service>` element, define the location of the endpoint contract, and also the type of binding for the endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="b3719-208">끝점은 클라이언트가 호스트 응용 프로그램을 검색하는 위치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-208">The endpoint defines where the client will look for the host application.</span></span> <span data-ttu-id="b3719-209">나중에 이 자습서에서는 이 단계를 사용하여 Azure Relay를 통해 호스트를 완전히 공개하는 URI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-209">Later, the tutorial uses this step to create a URI that fully exposes the host through Azure Relay.</span></span> <span data-ttu-id="b3719-210">바인딩은 릴레이 서비스와의 통신에 TCP를 프로토콜로 사용한다고 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-210">The binding declares that we are using TCP as the protocol to communicate with the relay service.</span></span>
7. <span data-ttu-id="b3719-211">**빌드** 메뉴에서 **솔루션 빌드**를 클릭하여 작업이 정확한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-211">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="b3719-212">예</span><span class="sxs-lookup"><span data-stu-id="b3719-212">Example</span></span>

<span data-ttu-id="b3719-213">다음 코드에서는 서비스 계약의 구현을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-213">The following code shows the implementation of the service contract.</span></span>

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

<span data-ttu-id="b3719-214">다음 예제에서는 서비스 호스트와 관련된 App.config 파일의 기본 형식을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-214">The following code shows the basic format of the App.config file associated with the service host.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-to-register-with-the-relay-service"></a><span data-ttu-id="b3719-215">릴레이 서비스에 등록할 기본 웹 서비스 호스팅 및 실행</span><span class="sxs-lookup"><span data-stu-id="b3719-215">Host and run a basic web service to register with the relay service</span></span>

<span data-ttu-id="b3719-216">이 단계에서는 Azure Relay 서비스를 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-216">This step describes how to run an Azure Relay service.</span></span>

### <a name="create-the-relay-credentials"></a><span data-ttu-id="b3719-217">릴레이 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="b3719-217">Create the relay credentials</span></span>

1. <span data-ttu-id="b3719-218">`Main()`에서 콘솔 창으로부터 읽은 네임스페이스와 SAS 키를 저장할 두 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-218">In `Main()`, create two variables in which to store the namespace and the SAS key that are read from the console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="b3719-219">SAS 키는 나중에 프로젝트에 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-219">The SAS key will be used later to access your project.</span></span> <span data-ttu-id="b3719-220">네임스페이스는 서비스 URI를 만들기 위해 매개 변수 형태로 `CreateServiceUri`에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-220">The namespace is passed as a parameter to `CreateServiceUri` to create a service URI.</span></span>
2. <span data-ttu-id="b3719-221">[TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) 개체를 사용하여 SAS 키를 자격 증명 유형으로 사용할 것임을 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-221">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as the credential type.</span></span> <span data-ttu-id="b3719-222">마지막 단계에서 추가한 코드 바로 뒤에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-222">Add the following code directly after the code added in the last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-the-service"></a><span data-ttu-id="b3719-223">서비스에 대한 기준 주소 만들기</span><span class="sxs-lookup"><span data-stu-id="b3719-223">Create a base address for the service</span></span>

<span data-ttu-id="b3719-224">마지막 단계에서 추가한 코드 뒤에 서비스의 기본 주소에 대한 `Uri` 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-224">After the code you added in the last step, create a `Uri` instance for the base address of the service.</span></span> <span data-ttu-id="b3719-225">이 URI는 서비스 버스 체계, 네임스페이스 및 서비스 인터페이스의 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-225">This URI specifies the Service Bus scheme, the namespace, and the path of the service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="b3719-226">"sb"는 Service Bus scheme(서비스 버스 체계)의 약어로, TCP를 프로토콜로 사용할 것임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-226">"sb" is an abbreviation for the Service Bus scheme, and indicates that we are using TCP as the protocol.</span></span> <span data-ttu-id="b3719-227">이 내용은 [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx)이 바인딩으로 지정되었던 이전에도 구성 파일에 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-227">This was also previously indicated in the configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as the binding.</span></span>

<span data-ttu-id="b3719-228">이 자습서에 대한 URI는 `sb://putServiceNamespaceHere.windows.net/EchoService`입니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-228">For this tutorial, the URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-the-service-host"></a><span data-ttu-id="b3719-229">서비스 호스트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="b3719-229">Create and configure the service host</span></span>

1. <span data-ttu-id="b3719-230">연결 모드를 `AutoDetect`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-230">Set the connectivity mode to `AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="b3719-231">연결 모드는 HTTP 또는 TCP 등, 서비스가 릴레이 서비스와의 통신에 사용하는 프로토콜을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-231">The connectivity mode describes the protocol the service uses to communicate with the relay service; either HTTP or TCP.</span></span> <span data-ttu-id="b3719-232">서비스는 기본 설정 `AutoDetect`를 사용하여 TCP가 사용 가능하면 TCP를 통해, 사용할 수 없으면 HTTP를 통해 Azure Relay에 대한 연결을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-232">Using the default setting `AutoDetect`, the service attempts to connect to Azure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="b3719-233">이 항목은 클라이언트 통신에 대해 서비스가 지정한 프로토콜과는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-233">Note that this differs from the protocol the service specifies for client communication.</span></span> <span data-ttu-id="b3719-234">해당 프로토콜은 사용한 바인딩에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-234">That protocol is determined by the binding used.</span></span> <span data-ttu-id="b3719-235">예를 들어, 서비스에서 끝점이 HTTP를 통해 클라이언트와 통신하도록 지정하는 [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) 바인딩을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-235">For example, a service can use the [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="b3719-236">동일한 서비스에서 서비스가 TCP를 통해 Azure Relay와 통신하도록 **ConnectivityMode.AutoDetect**를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-236">That same service could specify **ConnectivityMode.AutoDetect** so that the service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="b3719-237">이 섹션 앞부분에서 만든 URI를 사용하여 서비스 호스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-237">Create the service host, using the URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="b3719-238">서비스 호스트는 서비스를 인스턴스화하는 WCF 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-238">The service host is the WCF object that instantiates the service.</span></span> <span data-ttu-id="b3719-239">이 개체에 만들려는 서비스 형식(`EchoService` 형식)을 전달하며 서비스를 노출하려는 주소에도 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-239">Here, you pass it the type of service you want to create (an `EchoService` type), and also to the address at which you want to expose the service.</span></span>
3. <span data-ttu-id="b3719-240">Program.cs 파일 맨 위에 [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) 및 [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description)에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-240">At the top of the Program.cs file, add references to [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="b3719-241">`Main()`으로 돌아가 공용 액세스가 가능하도록 끝점을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-241">Back in `Main()`, configure the endpoint to enable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="b3719-242">이 단계에서는 응용 프로그램이 프로젝트에 대한 ATOM 피드를 조사하여 공개적으로 찾을 수 있는 릴레이 서비스를 알립니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-242">This step informs the relay service that your application can be found publicly by examining the ATOM feed for your project.</span></span> <span data-ttu-id="b3719-243">**DiscoveryType**을 **private**해도 클라이언트는 여전히 서비스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-243">If you set **DiscoveryType** to **private**, a client would still be able to access the service.</span></span> <span data-ttu-id="b3719-244">그러나 릴레이 네임스페이스를 검색할 때는 서비스가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-244">However, the service would not appear when it searches the Relay namespace.</span></span> <span data-ttu-id="b3719-245">대신 클라이언트 끝점 경로를 미리 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-245">Instead, the client would have to know the endpoint path beforehand.</span></span>
5. <span data-ttu-id="b3719-246">서비스 자격 증명을 App.config 파일에 정의된 서비스 끝점에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-246">Apply the service credentials to the service endpoints defined in the App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="b3719-247">이전 단계에서 설명한 것처럼 구성 파일에서 여러 서비스와 끝점을 선언할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-247">As stated in the previous step, you could have declared multiple services and endpoints in the configuration file.</span></span> <span data-ttu-id="b3719-248">그렇게 한 경우 이 코드는 구성 파일을 트래버스하여 자격 증명을 적용해야 하는 모든 끝점을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-248">If you had, this code would traverse the configuration file and search for every endpoint to which it should apply your credentials.</span></span> <span data-ttu-id="b3719-249">그러나 이 자습서에서는 구성 파일에 단 하나의 끝점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-249">However, for this tutorial, the configuration file has only one endpoint.</span></span>

### <a name="open-the-service-host"></a><span data-ttu-id="b3719-250">서비스 호스트 열기</span><span class="sxs-lookup"><span data-stu-id="b3719-250">Open the service host</span></span>

1. <span data-ttu-id="b3719-251">서비스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-251">Open the service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="b3719-252">서비스가 실행 중임을 사용자에게 알리고 서비스 종료 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-252">Inform the user that the service is running, and explain how to shut down the service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="b3719-253">완료되면 서비스 호스트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-253">When finished, close the service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="b3719-254">**Ctrl+Shift+B**를 눌러 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-254">Press **Ctrl+Shift+B** to build the project.</span></span>

### <a name="example"></a><span data-ttu-id="b3719-255">예</span><span class="sxs-lookup"><span data-stu-id="b3719-255">Example</span></span>

<span data-ttu-id="b3719-256">완료된 서비스 코드는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-256">Your completed service code should appear as follows.</span></span> <span data-ttu-id="b3719-257">코드는 자습서에 포함된 이전 단계의 구현 및 서비스 계약을 포함하고 콘솔 응용 프로그램에 서비스를 호스트합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-257">The code includes the service contract and implementation from previous steps in the tutorial, and hosts the service in a console application.</span></span>

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create the credentials object for the endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create the service URI based on the service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create the service host reading the configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create the ServiceRegistrySettings behavior for the endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add the Relay credentials to all endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open the service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            // Close the service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-the-service-contract"></a><span data-ttu-id="b3719-258">서비스 계약에 대한 WCF 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="b3719-258">Create a WCF client for the service contract</span></span>

<span data-ttu-id="b3719-259">다음 단계는 클라이언트 응용 프로그램을 만들고 이후 단계에서 구현하는 서비스 계약을 정의하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-259">The next step is to create a client application and define the service contract you will implement in later steps.</span></span> <span data-ttu-id="b3719-260">이 단계의 대부분은 App.config 파일을 편집하며 자격 증명을 사용하여 릴레이 서비스에 연결하는 등, 서비스를 만드는 단계와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-260">Note that many of these steps resemble the steps used to create a service: defining a contract, editing an App.config file, using credentials to connect to the relay service, and so on.</span></span> <span data-ttu-id="b3719-261">이 작업에 사용되는 코드는 과정을 수행하면서 예제에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-261">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="b3719-262">다음을 수행하여 클라이언트에 대 해 현재 Visual Studio 솔루션에서 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-262">Create a new project in the current Visual Studio solution for the client by doing the following:</span></span>

   1. <span data-ttu-id="b3719-263">솔루션 탐색기에서 해당 서비스를 포함하는 동일한 솔루션 중 현재 솔루션(프로젝트 아님)을 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-263">In Solution Explorer, in the same solution that contains the service, right-click the current solution (not the project), and click **Add**.</span></span> <span data-ttu-id="b3719-264">그런 후 **새 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-264">Then click **New Project**.</span></span>
   2. <span data-ttu-id="b3719-265">**새 프로젝트 추가** 대화 상자에서 **Visual C#**을 클릭하고(**Visual C#**이 표시되지 않으면 **다른 언어**에서 찾음) **콘솔 앱(.NET Framework)** 템플릿을 선택한 후 **EchoClient**로 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-265">In the **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select the **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="b3719-266">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-266">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="b3719-267">솔루션 탐색기에서 **EchoClient** 프로젝트에 있는 Program.cs 파일을 두 번 클릭하여 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-267">In Solution Explorer, double-click the Program.cs file in the **EchoClient** project to open it in the editor, if it is not already open.</span></span>
3. <span data-ttu-id="b3719-268">네임스페이스 이름을 기본 이름인 `EchoClient`에서 `Microsoft.ServiceBus.Samples`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-268">Change the namespace name from its default name of `EchoClient` to `Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="b3719-269">[Service Bus NuGet 패키지](https://www.nuget.org/packages/WindowsAzure.ServiceBus) 설치: 솔루션 탐색기에서 **EchoClient** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음, **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-269">Install the [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click the **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="b3719-270">**찾아보기** 탭을 클릭한 다음 `Microsoft Azure Service Bus`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-270">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="b3719-271">**설치**를 클릭하고 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-271">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="b3719-272">Program.cs 파일에 [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) 네임스페이스에 대한 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-272">Add a `using` statement for the [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in the Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="b3719-273">다음 예제와 같이 서비스 계약 정의를 네임스페이스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-273">Add the service contract definition to the namespace, as shown in the following example.</span></span> <span data-ttu-id="b3719-274">이 정의는 **Service** 프로젝트에 사용되는 정의와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-274">Note that this definition is identical to the definition used in the **Service** project.</span></span> <span data-ttu-id="b3719-275">이 코드는 `Microsoft.ServiceBus.Samples` 네임스페이스 위쪽에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-275">You should add this code at the top of the `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="b3719-276">**Ctrl+Shift+B**를 눌러 클라이언트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-276">Press **Ctrl+Shift+B** to build the client.</span></span>

### <a name="example"></a><span data-ttu-id="b3719-277">예제</span><span class="sxs-lookup"><span data-stu-id="b3719-277">Example</span></span>

<span data-ttu-id="b3719-278">다음 코드에서는 **EchoClient** 프로젝트에서 Program.cs 파일의 현재 상태를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-278">The following code shows the current status of the Program.cs file in the **EchoClient** project.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-the-wcf-client"></a><span data-ttu-id="b3719-279">WCF 클라이언트 구성 </span><span class="sxs-lookup"><span data-stu-id="b3719-279">Configure the WCF client</span></span>

<span data-ttu-id="b3719-280">이 단계에서는 이 자습서의 앞에서 만든 서비스에 액세스하는 기본 클라이언트 응용 프로그램의 App.config 파일을 만듭니다. </span><span class="sxs-lookup"><span data-stu-id="b3719-280">In this step, you create an App.config file for a basic client application that accesses the service created previously in this tutorial.</span></span> <span data-ttu-id="b3719-281">이 App.config 파일은 계약, 바인딩 및 끝점의 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-281">This App.config file defines the contract, binding, and name of the endpoint.</span></span> <span data-ttu-id="b3719-282">이 작업에 사용되는 코드는 과정을 수행하면서 예제에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-282">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="b3719-283">솔루션 탐색기의 **EchoClient** 프로젝트에서 **App.config**를 두 번 클릭하여 Visual Studio 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-283">In Solution Explorer, in the **EchoClient** project, double-click **App.config** to open the file in the Visual Studio editor.</span></span>
2. <span data-ttu-id="b3719-284">`<appSettings>` 요소에서 자리 표시자를 이전 단계에서 복사한 서비스 네임스페이스 및 SAS 키의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-284">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="b3719-285">System.serviceModel 요소 안에서 `<client>` 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-285">Within the system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="b3719-286">이 단계에서는 WCF 스타일 클라이언트 응용 프로그램을 정의함을 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-286">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="b3719-287">`client` 요소 내에서 끝점의 이름, 계약, 바인딩 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-287">Within the `client` element, define the name, contract, and binding type for the endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="b3719-288">이 단계에서는 끝점 이름, 서비스에서 정의한 계약, 클라이언트가 TCP를 사용하여 Azure Relay와 통신한다는 사실을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-288">This step defines the name of the endpoint, the contract defined in the service, and the fact that the client application uses TCP to communicate with Azure Relay.</span></span> <span data-ttu-id="b3719-289">끝점 이름은 이 끝점 구성을 서비스 URI에 연결하는 다음 절차에서 사용됩니다. </span><span class="sxs-lookup"><span data-stu-id="b3719-289">The endpoint name is used in the next step to link this endpoint configuration with the service URI.</span></span>
5. <span data-ttu-id="b3719-290">**파일**을 클릭한 다음 **모두 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-290">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="b3719-291">예제</span><span class="sxs-lookup"><span data-stu-id="b3719-291">Example</span></span>

<span data-ttu-id="b3719-292">다음 코드는 Echo 클라이언트에 대한 App.config 파일을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-292">The following code shows the App.config file for the Echo client.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-the-wcf-client"></a><span data-ttu-id="b3719-293">WCF 클라이언트 구현</span><span class="sxs-lookup"><span data-stu-id="b3719-293">Implement the WCF client</span></span>
<span data-ttu-id="b3719-294">이 단계에서는 이 자습서의 앞에서 만든 서비스에 액세스하는 기본 클라이언트 응용 프로그램을 구현합니다. </span><span class="sxs-lookup"><span data-stu-id="b3719-294">In this step, you implement a basic client application that accesses the service you created previously in this tutorial.</span></span> <span data-ttu-id="b3719-295">서비스와 마찬가지로, 클라이언트는 Azure Relay 액세스와 많은 동일한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-295">Similar to the service, the client performs many of the same operations to access Azure Relay:</span></span>

1. <span data-ttu-id="b3719-296">연결 모드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-296">Sets the connectivity mode.</span></span>
2. <span data-ttu-id="b3719-297">호스트 서비스를 찾는 URI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-297">Creates the URI that locates the host service.</span></span>
3. <span data-ttu-id="b3719-298">보안 자격 증명을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-298">Defines the security credentials.</span></span>
4. <span data-ttu-id="b3719-299">연결에 자격 증명을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-299">Applies the credentials to the connection.</span></span>
5. <span data-ttu-id="b3719-300">연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-300">Opens the connection.</span></span>
6. <span data-ttu-id="b3719-301">응용 프로그램 특정 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-301">Performs the application-specific tasks.</span></span>
7. <span data-ttu-id="b3719-302">연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-302">Closes the connection.</span></span>

<span data-ttu-id="b3719-303">그러나 주요 차이 중 하나는 클라이언트 응용 프로그램이 채널을 사용하여 릴레이 서비스에 연결하는 것과 달리 서비스는 **ServiceHost**에 대한 호출을 사용한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-303">However, one of the main differences is that the client application uses a channel to connect to the relay service, whereas the service uses a call to **ServiceHost**.</span></span> <span data-ttu-id="b3719-304">이 작업에 사용되는 코드는 과정을 수행하면서 예제에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-304">The code used for these tasks is provided in the example following the procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="b3719-305">클라이언트 응용 프로그램 구현</span><span class="sxs-lookup"><span data-stu-id="b3719-305">Implement a client application</span></span>
1. <span data-ttu-id="b3719-306">연결 모드를 **AutoDetect**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-306">Set the connectivity mode to **AutoDetect**.</span></span> <span data-ttu-id="b3719-307">**EchoClient** 응용 프로그램의 `Main()` 메서드 내에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-307">Add the following code inside the `Main()` method of the **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="b3719-308">서비스 네임스페이스에 대한 값과, 콘솔에서 읽은 SAS 키를 담을 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-308">Define variables to hold the values for the service namespace, and SAS key that are read from the console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="b3719-309">릴레이 프로젝트에서 호스트의 위치를 정의하는 URI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-309">Create the URI that defines the location of the host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="b3719-310">서비스 네임스페이스 끝점에 대한 자격 증명 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-310">Create the credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="b3719-311">App.config 파일에 설명된 구성을 로드하는 채널 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-311">Create the channel factory that loads the configuration described in the App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="b3719-312">채널 팩터리는 서비스 및 클라이언트 응용 프로그램이 통신하기 위해 경유하는 채널을 만드는 WCF 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-312">A channel factory is a WCF object that creates a channel through which the service and client applications communicate.</span></span>
6. <span data-ttu-id="b3719-313">자격 증명을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-313">Apply the credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="b3719-314">서비스에 대한 채널을 만들어 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-314">Create and open the channel to the service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="b3719-315">에코에 대해 기본 사용자 인터페이스 및 기능을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-315">Write the basic user interface and functionality for the echo.</span></span>

    ```csharp
    Console.WriteLine("Enter text to echo (or [Enter] to exit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    <span data-ttu-id="b3719-316">이 코드에서는 서비스에 대한 프록시로 채널 개체의 인스턴스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-316">Note that the code uses the instance of the channel object as a proxy for the service.</span></span>
9. <span data-ttu-id="b3719-317">채널을 닫고, 팩터리를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-317">Close the channel, and close the factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="b3719-318">예</span><span class="sxs-lookup"><span data-stu-id="b3719-318">Example</span></span>

<span data-ttu-id="b3719-319">완성된 코드는 다음과 같으며 클라이언트 응용 프로그램을 만드는 방법, 서비스 작업 호출 방법 및 작업 호출 완료 후 클라이언트를 닫는 방법 등을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-319">Your completed code should appear as follows, showing how to create a client application, how to call the operations of the service, and how to close the client after the operation call is finished.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text to echo (or [Enter] to exit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-the-applications"></a><span data-ttu-id="b3719-320">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="b3719-320">Run the applications</span></span>

1. <span data-ttu-id="b3719-321">**Ctrl+Shift+B**를 눌러 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-321">Press **Ctrl+Shift+B** to build the solution.</span></span> <span data-ttu-id="b3719-322">이렇게 하면 이전 단계에서 만든 클라이언트 프로젝트와 서비스 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-322">This builds both the client project and the service project that you created in the previous steps.</span></span>
2. <span data-ttu-id="b3719-323">클라이언트 응용 프로그램을 실행하기 전에 서비스 응용 프로그램이 실행 중인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-323">Before running the client application, you must make sure that the service application is running.</span></span> <span data-ttu-id="b3719-324">Visual Studio의 솔루션 탐색기에서 **EchoService** 솔루션을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-324">In Solution Explorer in Visual Studio, right-click the **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="b3719-325">솔루션 속성 대화 상자에서 **시작 프로젝트**를 클릭한 다음 **여러 개의 시작 프로젝트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-325">In the solution properties dialog box, click **Startup Project**, then click the **Multiple startup projects** button.</span></span> <span data-ttu-id="b3719-326">**EchoService**가 목록 맨 처음에 나오는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-326">Make sure **EchoService** appears first in the list.</span></span>
4. <span data-ttu-id="b3719-327">**EchoService** 및 **EchoClient** 프로젝트의 **작업** 상자를 모두 **시작**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-327">Set the **Action** box for both the **EchoService** and **EchoClient** projects to **Start**.</span></span>

    ![][5]
5. <span data-ttu-id="b3719-328">**프로젝트 종속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-328">Click **Project Dependencies**.</span></span> <span data-ttu-id="b3719-329">**프로젝트** 상자에서 **EchoClient**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-329">In the **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="b3719-330">**다음에 종속** 상자에서 **EchoService**가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-330">In the **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="b3719-331">**확인**을 클릭하여 **속성** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-331">Click **OK** to dismiss the **Properties** dialog.</span></span>
7. <span data-ttu-id="b3719-332">**F5** 키를 눌러 두 프로젝트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-332">Press **F5** to run both projects.</span></span>
8. <span data-ttu-id="b3719-333">두 콘솔 창을 열고 네임스페이스 이름에 대한 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-333">Both console windows open and prompt you for the namespace name.</span></span> <span data-ttu-id="b3719-334">서비스가 먼저 실행되어야 하므로 **EchoService** 콘솔 창에서 네임스페이스를 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-334">The service must run first, so in the **EchoService** console window, enter the namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="b3719-335">다음으로, SAS 키를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-335">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="b3719-336">SAS 키를 입력하고 ENTER를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-336">Enter the SAS key and press ENTER.</span></span>

    <span data-ttu-id="b3719-337">콘솔 창의 출력 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-337">Here is example output from the console window.</span></span> <span data-ttu-id="b3719-338">여기서 입력한 값은 오직 예시용입니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-338">Note that the values provided here are for example purposes only.</span></span>

    <span data-ttu-id="b3719-339">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="b3719-339">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="b3719-340">서비스 응용 프로그램은 다음 예제에서처럼 콘솔 창에 수신 중인 주소를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-340">The service application prints to the console window the address on which it's listening, as seen in the following example.</span></span>

    <span data-ttu-id="b3719-341">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span><span class="sxs-lookup"><span data-stu-id="b3719-341">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span></span>
10. <span data-ttu-id="b3719-342">**EchoClient** 콘솔 창에서 이전에 서비스 응용 프로그램에 입력한 동일한 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-342">In the **EchoClient** console window, enter the same information that you entered previously for the service application.</span></span> <span data-ttu-id="b3719-343">이전 단계에 따라 클라이언트 응용 프로그램에 동일한 서비스 네임스페이스 및 SAS 키 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-343">Follow the previous steps to enter the same service namespace and SAS key values for the client application.</span></span>
11. <span data-ttu-id="b3719-344">이 값을 입력한 후 클라이언트가 서비스에 대한 채널을 열고 다음 콘솔 출력 예제에서 보이는 것처럼 여러 텍스트를 입력하라는 메시지가 표시됩니다. </span><span class="sxs-lookup"><span data-stu-id="b3719-344">After entering these values, the client opens a channel to the service and prompts you to enter some text as seen in the following console output example.</span></span>

    `Enter text to echo (or [Enter] to exit):`

    <span data-ttu-id="b3719-345">서비스 응용 프로그램에 보낼 여러 텍스트를 입력하고 Enter를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-345">Enter some text to send to the service application and press Enter.</span></span> <span data-ttu-id="b3719-346">이 텍스트는 에코 서비스 작업을 통해 서비스에 전달되며 다음 예제 출력에서처럼 서비스 콘솔 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-346">This text is sent to the service through the Echo service operation and appears in the service console window as in the following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="b3719-347">클라이언트 응용 프로그램은 원본 텍스트인 `Echo` 작업의 반환 값을 받아 콘솔 창에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-347">The client application receives the return value of the `Echo` operation, which is the original text, and prints it to its console window.</span></span> <span data-ttu-id="b3719-348">클라이언트 콘솔 창의 출력 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-348">The following is example output from the client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="b3719-349">이런 방식으로 클라이언트에서 서비스로 문자 메시지를 지속적으로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-349">You can continue sending text messages from the client to the service in this manner.</span></span> <span data-ttu-id="b3719-350">작업을 마치면 클라이언트와 서비스 콘솔 창에서 Enter를 눌러 두 응용 프로그램을 모두 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-350">When you are finished, press Enter in the client and service console windows to end both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3719-351">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b3719-351">Next steps</span></span>

<span data-ttu-id="b3719-352">이 자습서에서는 Service Bus의 WCF 릴레이 기능을 사용하여 Azure Relay 클라이언트 응용 프로그램 및 서비스를 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3719-352">This tutorial showed how to build an Azure Relay client application and service using the WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="b3719-353">[Service Bus 메시징](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging)을 사용하는 유사한 자습서는 [Service Bus 큐 시작](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3719-353">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="b3719-354">Azure 릴레이에 대한 자세한 내용은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3719-354">To learn more about Azure Relay, see the following topics.</span></span>

* [<span data-ttu-id="b3719-355">Azure Service Bus 아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="b3719-355">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="b3719-356">Azure Relay 개요</span><span class="sxs-lookup"><span data-stu-id="b3719-356">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="b3719-357">.NET과 함께 WCF 릴레이 서비스를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="b3719-357">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
