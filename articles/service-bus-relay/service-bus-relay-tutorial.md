---
title: "서비스 버스 WCF 릴레이 자습서 aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="e233a-103">Azure WCF 릴레이 자습서</span><span class="sxs-lookup"><span data-stu-id="e233a-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="e233a-104">이 자습서에서는 간단한 WCF 릴레이 하는 toobuild 방법을 설명 하 고 Azure 릴레이 사용 하 여 서비스 클라이언트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-104">This tutorial describes how toobuild a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="e233a-105">[Service Bus 메시징](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging)을 사용하는 유사한 자습서는 [Service Bus 큐 시작](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e233a-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="e233a-106">이 자습서를 통해 작업 hello 단계를 필요한 toocreate WCF 릴레이 클라이언트와 서비스 응용 프로그램의 이해를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-106">Working through this tutorial gives you an understanding of hello steps that are required toocreate a WCF Relay client and service application.</span></span> <span data-ttu-id="e233a-107">기존 WCF 대응처럼 서비스는 하나 이상의 끝점을 노출하는 구문으로, 각각 하나 이상의 서비스 작업을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="e233a-108">서비스의 끝점 hello hello 서비스를 찾을 수 있는, 주소 hello 서비스 tooits 클라이언트에서 제공 하는 hello 기능을 정의 하는 계약 hello 서비스와 통신 하는 hello 정보를 포함 하는 바인딩을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-108">hello endpoint of a service specifies an address where hello service can be found, a binding that contains hello information that a client must communicate with hello service, and a contract that defines hello functionality provided by hello service tooits clients.</span></span> <span data-ttu-id="e233a-109">hello는 주요 차이점이 WCF와 WCF 릴레이 컴퓨터에 로컬로 대신 hello 클라우드에서 해당 hello 끝점이 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-109">hello main difference between WCF and WCF Relay is that hello endpoint is exposed in hello cloud instead of locally on your computer.</span></span>

<span data-ttu-id="e233a-110">이 자습서의 항목 hello 시퀀스를 통해 작업 한 후 hello 서비스의 hello 작업을 호출할 수 있는 클라이언트 및 서비스를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-110">After you work through hello sequence of topics in this tutorial, you will have a running service, and a client that can invoke hello operations of hello service.</span></span> <span data-ttu-id="e233a-111">hello 첫 번째 항목에 설명 어떻게 tooset 계정.</span><span class="sxs-lookup"><span data-stu-id="e233a-111">hello first topic describes how tooset up an account.</span></span> <span data-ttu-id="e233a-112">hello 다음 단계로 진행 방법을 toodefine 서비스 및 사용 하는 계약, 어떻게 tooimplement hello 서비스를 어떻게 tooconfigure hello 코드의 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-112">hello next steps describe how toodefine a service that uses a contract, how tooimplement hello service, and how tooconfigure hello service in code.</span></span> <span data-ttu-id="e233a-113">또한 설명 방법을 hello 서비스 toohost 및 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-113">They also describe how toohost and run hello service.</span></span> <span data-ttu-id="e233a-114">hello 만들어진 서비스는 자체 호스트 되며 hello에서 실행 하는 hello 클라이언트와 서비스가 동일한 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="e233a-114">hello service that is created is self-hosted and hello client and service run on hello same computer.</span></span> <span data-ttu-id="e233a-115">코드 또는 구성 파일을 사용 하 여 hello 서비스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-115">You can configure hello service by using either code or a configuration file.</span></span>

<span data-ttu-id="e233a-116">toocreate 클라이언트 응용 프로그램을 hello 클라이언트 응용 프로그램을 구성 하 고 만들고 방법 hello 호스트의 hello 기능에 액세스할 수 있는 클라이언트를 사용 하 여 hello 마지막 세 단계에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-116">hello final three steps describe how toocreate a client application, configure hello client application, and create and use a client that can access hello functionality of hello host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e233a-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e233a-117">Prerequisites</span></span>

<span data-ttu-id="e233a-118">toocomplete이이 자습서에서는 다음 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-118">toocomplete this tutorial, you'll need hello following:</span></span>

* <span data-ttu-id="e233a-119">[Microsoft Visual Studio 2015 이상](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="e233a-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="e233a-120">이 자습서에서는 Visual Studio 2017을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="e233a-121">활성 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="e233a-121">An active Azure account.</span></span> <span data-ttu-id="e233a-122">계정이 없는 경우 몇 분 만에 무료 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="e233a-123">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/free/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e233a-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="e233a-124">서비스 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e233a-124">Create a service namespace</span></span>

<span data-ttu-id="e233a-125">hello 첫 번째 단계는 toocreate 네임 스페이스 및 tooobtain는 [공유 액세스 서명 (SAS)](../service-bus-messaging/service-bus-sas.md) 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-125">hello first step is toocreate a namespace, and tooobtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="e233a-126">네임 스페이스 hello 릴레이 서비스를 통해 노출 된 각 응용 프로그램에 대 한 응용 프로그램 경계를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-126">A namespace provides an application boundary for each application exposed through hello relay service.</span></span> <span data-ttu-id="e233a-127">SAS 키가 서비스 네임 스페이스를 만들 때 hello 시스템에서 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-127">A SAS key is automatically generated by hello system when a service namespace is created.</span></span> <span data-ttu-id="e233a-128">서비스 네임 스페이스와 SAS 키 조합 hello Azure tooauthenticate access tooan 응용 프로그램에 대 한 hello 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-128">hello combination of service namespace and SAS key provides hello credentials for Azure tooauthenticate access tooan application.</span></span> <span data-ttu-id="e233a-129">Hello에 따라 [여기에 지침이](relay-create-namespace-portal.md) toocreate 릴레이 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-129">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="e233a-130">WCF 서비스 계약 정의</span><span class="sxs-lookup"><span data-stu-id="e233a-130">Define a WCF service contract</span></span>

<span data-ttu-id="e233a-131">hello 서비스 계약은 작업 (메서드 또는 함수에 대 한 hello 웹 서비스 용어) hello 서비스에서 지 원하는 사항를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-131">hello service contract specifies what operations (hello web service terminology for methods or functions) hello service supports.</span></span> <span data-ttu-id="e233a-132">계약은 C++, C#, 또는 Visual Basic 인터페이스를 정의하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="e233a-133">Hello 인터페이스의 각 메서드에 tooa 특정 서비스 작업에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-133">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="e233a-134">각 인터페이스 hello 있어야 [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) 특성이 tooit를 적용 하 고 각 작업에는 hello 있어야 합니다. [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit 특성이 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-134">Each interface must have hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied tooit, and each operation must have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied tooit.</span></span> <span data-ttu-id="e233a-135">Hello 변수가 있는 인터페이스의 메서드가 [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) 특성에 hello 없는 [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) 특성을 메서드가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-135">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="e233a-136">이러한 작업에 대 한 hello 코드 hello 절차 다음에 hello 예에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-136">hello code for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="e233a-137">계약 및 서비스의 더 큰 논의 알려면 [서비스 디자인 및 구현](https://msdn.microsoft.com/library/ms729746.aspx) hello WCF 설명서에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in hello WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="e233a-138">인터페이스와 함께 릴레이 계약 만들기</span><span class="sxs-lookup"><span data-stu-id="e233a-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="e233a-139">Hello에 hello 프로그램을 마우스 오른쪽 단추로 클릭 하 여 관리자 권한으로 Visual Studio를 열고 **시작** 메뉴에서 **관리자 권한으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-139">Open Visual Studio as an administrator by right-clicking hello program in hello **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="e233a-140">새 콘솔 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-140">Create a new console application project.</span></span> <span data-ttu-id="e233a-141">Hello 클릭 **파일** 메뉴와 선택 **새로**, 클릭 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-141">Click hello **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="e233a-142">Hello에 **새 프로젝트** 대화 상자에서 클릭 **Visual C#** (경우 **Visual C#** 가 보이지 않으면에서 **다른 언어**).</span><span class="sxs-lookup"><span data-stu-id="e233a-142">In hello **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="e233a-143">Hello 클릭 **콘솔 응용 프로그램 (.NET Framework)** 서식 파일을 하 고 이름을 **EchoService**합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-143">Click hello **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="e233a-144">클릭 **확인** toocreate hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="e233a-144">Click **OK** toocreate hello project.</span></span>

    ![][2]

3. <span data-ttu-id="e233a-145">Hello Service Bus NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-145">Install hello Service Bus NuGet package.</span></span> <span data-ttu-id="e233a-146">이 패키지는 hello WCF 뿐만 아니라 참조 toohello 서비스 버스 라이브러리에 자동으로 추가 **System.ServiceModel**합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-146">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="e233a-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) tooprogrammatically 액세스 hello WCF의 기본 기능을 사용 하는 hello 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables you tooprogrammatically access hello basic features of WCF.</span></span> <span data-ttu-id="e233a-148">서비스 버스는 여러 hello 개체 및 WCF toodefine 서비스 계약의 특성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-148">Service Bus uses many of hello objects and attributes of WCF toodefine service contracts.</span></span>

    <span data-ttu-id="e233a-149">솔루션 탐색기에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리...** . Hello 클릭 **찾아보기** tab, 이후 검색할 `Microsoft Azure Service Bus`합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-149">In Solution Explorer, right-click hello project, and then click **Manage NuGet Packages...**. Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="e233a-150">해당 hello 프로젝트 이름을 hello에 선택 되어 있는지 확인 **버전** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-150">Ensure that hello project name is selected in hello **Version(s)** box.</span></span> <span data-ttu-id="e233a-151">클릭 **설치**, hello 사용 약관을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-151">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="e233a-152">솔루션 탐색기에서 hello Program.cs 파일 tooopen 아직 없는 경우 hello 편집기에서 열을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-152">In Solution Explorer, double-click hello Program.cs file tooopen it in hello editor, if it is not already open.</span></span>
5. <span data-ttu-id="e233a-153">Hello 다음 추가 hello 파일 hello 상단의 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="e233a-153">Add hello following using statements at hello top of hello file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="e233a-154">기본 이름 만으로는 hello 네임 스페이스 이름 변경 **EchoService** 너무**Microsoft.ServiceBus.Samples**합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-154">Change hello namespace name from its default name of **EchoService** too**Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="e233a-155">이 자습서에서는 hello C# 네임 스페이스 **Microsoft.ServiceBus.Samples**, hello hello 구성 파일에서 사용 되는 형식을 관리 되는 계약 기반 hello의 hello 네임 스페이스는 [hello WCF 클라이언트구성](#configure-the-wcf-client) 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-155">This tutorial uses hello C# namespace **Microsoft.ServiceBus.Samples**, which is hello namespace of hello contract-based managed type that is used in hello configuration file in hello [Configure hello WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="e233a-156">이 샘플; 빌드할 때 원하는 네임 스페이스를 지정할 수 있습니다. 그러나 hello 자습서 수정 하지 않는 한 다음 hello 계약 및 서비스의 네임 스페이스 hello 적절 하 게 hello 응용 프로그램 구성 파일에서 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-156">You can specify any namespace you want when you build this sample; however, hello tutorial will not work unless you then modify hello namespaces of hello contract and service accordingly, in hello application configuration file.</span></span> <span data-ttu-id="e233a-157">hello 파일 이어야 App.config에에서 지정 된 hello 네임을 hello C# 파일에 지정 된 hello 네임 스페이스와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-157">hello namespace specified in hello App.config file must be hello same as hello namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="e233a-158">Hello 바로 뒤 `Microsoft.ServiceBus.Samples` 네임 스페이스 선언을 hello 네임 스페이스 내에서 이라는 새 인터페이스를 정의 하지만 `IEchoContract` hello 적용 `ServiceContractAttribute` 의 네임 스페이스 값을 가진 특성 toohello 인터페이스 `http://samples.microsoft.com/ServiceModel/Relay/`합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-158">Directly after hello `Microsoft.ServiceBus.Samples` namespace declaration, but within hello namespace, define a new interface named `IEchoContract` and apply hello `ServiceContractAttribute` attribute toohello interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="e233a-159">코드의 hello 범위 전체에서 사용 하는 hello 네임 스페이스에서 네임 스페이스 값 hello 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-159">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="e233a-160">대신, hello 네임 스페이스 값이이 계약에 대 한 고유 식별자로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-160">Instead, hello namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="e233a-161">Hello 네임 스페이스를 명시적으로 지정 하면 hello 기본 네임 스페이스 값을 toohello 계약 이름에 추가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-161">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span> <span data-ttu-id="e233a-162">Hello를 hello 네임 스페이스를 선언한 후 코드를 다음에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-162">Paste hello following code after hello namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="e233a-163">일반적으로 hello 서비스 계약 네임 스페이스에 버전 정보를 포함 하는 명명 체계를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-163">Typically, hello service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="e233a-164">Hello 서비스 계약 네임 스페이스에서 버전 정보를 포함 하 여 새 네임 스페이스로 새 서비스 계약을 정의 하 고 새 끝점에 노출 여 서비스 tooisolate 주요 변경 사항 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-164">Including version information in hello service contract namespace enables services tooisolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="e233a-165">이러한 방식으로 클라이언트 업데이트 toobe 필요 없이 toouse hello 이전 서비스 계약을 계속 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-165">In this manner, clients can continue toouse hello old service contract without having toobe updated.</span></span> <span data-ttu-id="e233a-166">버전 정보는 날짜 또는 빌드 번호로 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-166">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="e233a-167">자세한 내용은 [서비스 버전 관리](http://go.microsoft.com/fwlink/?LinkID=180498)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e233a-167">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="e233a-168">이 자습서의 hello 위해서 이름 지정 체계 hello 서비스 계약 네임 스페이스의 hello에 버전 정보</span><span class="sxs-lookup"><span data-stu-id="e233a-168">For hello purposes of this tutorial, hello naming scheme of hello service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="e233a-169">Hello 내 `IEchoContract` 인터페이스를 hello 단일 작업 hello에 대 한 메서드를 선언 `IEchoContract` hello에 노출 계약 인터페이스 및 hello 적용 `OperationContractAttribute` tooexpose의 일환으로 원하는 특성 toohello 방법을 hello 공용 WCF 릴레이 계약을 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-169">Within hello `IEchoContract` interface, declare a method for hello single operation hello `IEchoContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="e233a-170">Hello 바로 뒤 `IEchoContract` 인터페이스 정의 둘 다에서 상속 되는 채널을 선언 `IEchoContract` 및 또한 toohello `IClientChannel` 다음과 같이 인터페이스:</span><span class="sxs-lookup"><span data-stu-id="e233a-170">Directly after hello `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also toohello `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="e233a-171">채널은는 hello 호스트와 클라이언트가 전달 정보 tooeach 다른 hello WCF 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-171">A channel is hello WCF object through which hello host and client pass information tooeach other.</span></span> <span data-ttu-id="e233a-172">이상에서는 hello 두 응용 프로그램 간에 hello 채널 tooecho 정보에 대해 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-172">Later, you will write code against hello channel tooecho information between hello two applications.</span></span>
10. <span data-ttu-id="e233a-173">Hello에서 **빌드** 메뉴를 클릭 **솔루션 빌드** 하거나 키를 눌러 **Ctrl + Shift + B** tooconfirm hello 정확도 지금까지 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-173">From hello **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="e233a-174">예제</span><span class="sxs-lookup"><span data-stu-id="e233a-174">Example</span></span>

<span data-ttu-id="e233a-175">hello 코드 다음 WCF 릴레이 계약을 정의 하는 기본적인 인터페이스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-175">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

<span data-ttu-id="e233a-176">이제 hello 인터페이스를 만들었으므로 hello 인터페이스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-176">Now that hello interface is created, you can implement hello interface.</span></span>

## <a name="implement-hello-wcf-contract"></a><span data-ttu-id="e233a-177">Hello WCF 계약 구현</span><span class="sxs-lookup"><span data-stu-id="e233a-177">Implement hello WCF contract</span></span>

<span data-ttu-id="e233a-178">Azure 릴레이 만들기를 먼저 만들어야 인터페이스를 사용 하 여 정의 되는 hello 계약 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-178">Creating an Azure relay requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="e233a-179">Hello 인터페이스를 작성 하는 방법에 대 한 자세한 내용은 hello 이전 단계를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e233a-179">For more information about creating hello interface, see hello previous step.</span></span> <span data-ttu-id="e233a-180">hello 다음 단계는 tooimplement hello 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-180">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="e233a-181">라는 클래스를 생성이 포함 됩니다 `EchoService` 구현 하는 사용자 정의 hello `IEchoContract` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-181">This involves creating a class named `EchoService` that implements hello user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="e233a-182">Hello 인터페이스를 구현한 후 hello 인터페이스는 App.config 구성 파일을 사용 하 여 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-182">After you implement hello interface, you then configure hello interface using an App.config configuration file.</span></span> <span data-ttu-id="e233a-183">hello 구성 파일 hello hello 서비스 이름, hello 이름 hello 계약 및 hello 유형의 프로토콜을 사용 하는 toocommunicate hello 릴레이 서비스와 같은 hello 응용 프로그램에 필요한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-183">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="e233a-184">이러한 작업에 사용 되는 hello 코드 hello 절차 다음에 hello 예에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-184">hello code used for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="e233a-185">Tooimplement 서비스 계약 하는 방법에 대 한 자세한 논의 알려면 [서비스 계약 구현](https://msdn.microsoft.com/library/ms733764.aspx) hello WCF 설명서에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-185">For a more general discussion about how tooimplement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in hello WCF documentation.</span></span>

1. <span data-ttu-id="e233a-186">이라는 새 클래스를 만들 `EchoService` hello의 hello 정의 바로 뒤 `IEchoContract` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-186">Create a new class named `EchoService` directly after hello definition of hello `IEchoContract` interface.</span></span> <span data-ttu-id="e233a-187">hello `EchoService` 클래스 구현 hello `IEchoContract` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-187">hello `EchoService` class implements hello `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="e233a-188">비슷한 tooother 인터페이스 구현에 다른 파일에 hello 정의 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-188">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="e233a-189">그러나이 자습서에서는 hello 구현에 동일한 파일 hello 인터페이스 정의 및 hello hello `Main` 메서드.</span><span class="sxs-lookup"><span data-stu-id="e233a-189">However, for this tutorial, hello implementation is located in hello same file as hello interface definition and hello `Main` method.</span></span>
2. <span data-ttu-id="e233a-190">Hello 적용 [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) toohello 특성 `IEchoContract` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-190">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello `IEchoContract` interface.</span></span> <span data-ttu-id="e233a-191">hello 특성 hello 서비스 이름 및 네임 스페이스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-191">hello attribute specifies hello service name and namespace.</span></span> <span data-ttu-id="e233a-192">이렇게 하면 hello `EchoService` 클래스에는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-192">After doing so, hello `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="e233a-193">구현 hello `Echo` hello에 정의 된 메서드 `IEchoContract` hello에 대 한 인터페이스 `EchoService` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-193">Implement hello `Echo` method defined in hello `IEchoContract` interface in hello `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="e233a-194">클릭 **빌드**, 클릭 **솔루션 빌드** tooconfirm hello 여 작업이 정확 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-194">Click **Build**, then click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="define-hello-configuration-for-hello-service-host"></a><span data-ttu-id="e233a-195">Hello 서비스 호스트에 대 한 hello 구성 정의</span><span class="sxs-lookup"><span data-stu-id="e233a-195">Define hello configuration for hello service host</span></span>

1. <span data-ttu-id="e233a-196">hello 구성 파일은 매우 유사한 tooa WCF 구성 파일.</span><span class="sxs-lookup"><span data-stu-id="e233a-196">hello configuration file is very similar tooa WCF configuration file.</span></span> <span data-ttu-id="e233a-197">바인딩 (프로토콜을 사용 하는 toocommunicate hello 유형) hello 및 hello 서비스 이름, 끝점 (즉, hello 위치 서로 toocommunicate 클라이언트와 호스트에 대 한 Azure 릴레이 노출 하는), 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-197">It includes hello service name, endpoint (that is, hello location that Azure Relay exposes for clients and hosts toocommunicate with each other), and hello binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="e233a-198">hello 중요 한 차이점은이 구성 된 서비스 끝점 참조 tooa 한다고 [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) 바인딩을 hello.NET Framework의 일부가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-198">hello main difference is that this configured service endpoint refers tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of hello .NET Framework.</span></span> <span data-ttu-id="e233a-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) hello 서비스에 의해 정의 된 hello 바인딩 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of hello bindings defined by hello service.</span></span>
2. <span data-ttu-id="e233a-200">**솔루션 탐색기**, App.config 파일 tooopen hello를 두 번 클릭 hello Visual Studio 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="e233a-200">In **Solution Explorer**, double-click hello App.config file tooopen it in hello Visual Studio editor.</span></span>
3. <span data-ttu-id="e233a-201">Hello에 `<appSettings>` 요소 hello 자리 표시자 hello 서비스 네임 스페이스, 이름으로 대체 및 SAS 키를 이전 단계에서 복사한 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-201">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="e233a-202">Hello 내 `<system.serviceModel>` 태그, 추가 `<services>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-202">Within hello `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="e233a-203">단일 구성 파일 내에 여러 릴레이 응용 프로그램을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-203">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="e233a-204">그러나 이 자습서에서는 하나만 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-204">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="e233a-205">Hello 내 `<services>` 요소를 추가 `<service>` 요소 toodefine hello hello 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-205">Within hello `<services>` element, add a `<service>` element toodefine hello name of hello service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="e233a-206">Hello 내 `<service>` 요소인 hello 끝점 계약의 hello 위치를 정의 하 고 또한 hello 끝점에 대 한 바인딩 형식을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-206">Within hello `<service>` element, define hello location of hello endpoint contract, and also hello type of binding for hello endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="e233a-207">hello 끝점 hello 호스트 응용 프로그램에 대 한 hello 클라이언트를 찾을 위치를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-207">hello endpoint defines where hello client will look for hello host application.</span></span> <span data-ttu-id="e233a-208">이상 버전에서는 hello 자습서에서는이 단계 toocreate Azure 릴레이 통해 hello 호스트를 완벽 하 게 표시 하는 URI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-208">Later, hello tutorial uses this step toocreate a URI that fully exposes hello host through Azure Relay.</span></span> <span data-ttu-id="e233a-209">hello 바인딩 hello 릴레이 서비스와 프로토콜 toocommunicate hello 대로 TCP 사용 함을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-209">hello binding declares that we are using TCP as hello protocol toocommunicate with hello relay service.</span></span>
7. <span data-ttu-id="e233a-210">Hello에서 **빌드** 메뉴를 클릭 하 여 **솔루션 빌드** 작업이 tooconfirm hello 정확한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-210">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="e233a-211">예제</span><span class="sxs-lookup"><span data-stu-id="e233a-211">Example</span></span>

<span data-ttu-id="e233a-212">hello 다음 코드에서는 hello 서비스 계약의 hello 구현 된</span><span class="sxs-lookup"><span data-stu-id="e233a-212">hello following code shows hello implementation of hello service contract.</span></span>

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

<span data-ttu-id="e233a-213">hello 다음 코드에서는 hello hello 서비스 호스트와 연결 된 hello App.config 파일의 기본 형식</span><span class="sxs-lookup"><span data-stu-id="e233a-213">hello following code shows hello basic format of hello App.config file associated with hello service host.</span></span>

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

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a><span data-ttu-id="e233a-214">호스트 및 hello 릴레이 서비스와 기본 웹 서비스 tooregister 실행</span><span class="sxs-lookup"><span data-stu-id="e233a-214">Host and run a basic web service tooregister with hello relay service</span></span>

<span data-ttu-id="e233a-215">이 단계에서는 Azure 릴레이 하는 toorun 어떻게 설명 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-215">This step describes how toorun an Azure Relay service.</span></span>

### <a name="create-hello-relay-credentials"></a><span data-ttu-id="e233a-216">Hello 릴레이 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="e233a-216">Create hello relay credentials</span></span>

1. <span data-ttu-id="e233a-217">`Main()`hello hello 콘솔 창에서 읽는 SAS 키를 어떤 toostore hello 네임 스페이스에 두 개의 변수를 만들고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-217">In `Main()`, create two variables in which toostore hello namespace and hello SAS key that are read from hello console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="e233a-218">hello SAS 키 프로젝트에 사용 되는 이후 tooaccess 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-218">hello SAS key will be used later tooaccess your project.</span></span> <span data-ttu-id="e233a-219">hello 네임 스페이스 매개 변수로 너무 전달`CreateServiceUri` toocreate 서비스 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-219">hello namespace is passed as a parameter too`CreateServiceUri` toocreate a service URI.</span></span>
2. <span data-ttu-id="e233a-220">사용 하는 [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) 개체를 사용 하려는 SAS 키 hello 자격 증명 유형으로 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-220">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as hello credential type.</span></span> <span data-ttu-id="e233a-221">Hello 코드 hello 마지막 단계에서 추가한 hello 코드 바로 뒤에 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-221">Add hello following code directly after hello code added in hello last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a><span data-ttu-id="e233a-222">Hello 서비스에 대 한 기본 주소를 만들려면</span><span class="sxs-lookup"><span data-stu-id="e233a-222">Create a base address for hello service</span></span>

<span data-ttu-id="e233a-223">Hello hello 마지막 단계에서 추가한 코드 뒤 만들기는 `Uri` hello 기준 주소에 대 한 hello 서비스의 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="e233a-223">After hello code you added in hello last step, create a `Uri` instance for hello base address of hello service.</span></span> <span data-ttu-id="e233a-224">이 URI는 hello 서비스 버스 체계, hello 네임 스페이스 및 hello 서비스 인터페이스의 hello 경로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-224">This URI specifies hello Service Bus scheme, hello namespace, and hello path of hello service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="e233a-225">"sb" hello 서비스 버스 체계에 대 한 약어로 hello 프로토콜로 TCP를 사용 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-225">"sb" is an abbreviation for hello Service Bus scheme, and indicates that we are using TCP as hello protocol.</span></span> <span data-ttu-id="e233a-226">Hello 구성 파일에 이전에 지정 된이 때 [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) hello 바인딩으로 지정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-226">This was also previously indicated in hello configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as hello binding.</span></span>

<span data-ttu-id="e233a-227">이 자습서에 대 한 hello URI는 `sb://putServiceNamespaceHere.windows.net/EchoService`합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-227">For this tutorial, hello URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-hello-service-host"></a><span data-ttu-id="e233a-228">만들기 및 hello 서비스 호스트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-228">Create and configure hello service host</span></span>

1. <span data-ttu-id="e233a-229">너무 hello 연결 모드를 설정`AutoDetect`합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-229">Set hello connectivity mode too`AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="e233a-230">hello 연결 모드와 hello 릴레이 서비스; hello 프로토콜 hello 서비스 사용 하 여 toocommunicate 설명 HTTP 또는 TCP입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-230">hello connectivity mode describes hello protocol hello service uses toocommunicate with hello relay service; either HTTP or TCP.</span></span> <span data-ttu-id="e233a-231">Hello 기본 설정을 사용 하 여 `AutoDetect`, TCP를 사용할 수 없는 경우 hello 서비스를 사용할 수 있는 경우 TCP 및 HTTP를 통한 tooconnect tooAzure 릴레이 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-231">Using hello default setting `AutoDetect`, hello service attempts tooconnect tooAzure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="e233a-232">클라이언트 통신에 대 한 참고 hello 프로토콜 hello 서비스에서이 점에서 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-232">Note that this differs from hello protocol hello service specifies for client communication.</span></span> <span data-ttu-id="e233a-233">해당 프로토콜 사용 하는 hello 바인딩에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-233">That protocol is determined by hello binding used.</span></span> <span data-ttu-id="e233a-234">예를 들어 서비스 צ ְ ײ hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) 해당 끝점이 HTTP를 통해 클라이언트와 통신 하는 지정 하는 바인딩.</span><span class="sxs-lookup"><span data-stu-id="e233a-234">For example, a service can use hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="e233a-235">동일한 서비스 지정할 수 있었습니다 **ConnectivityMode.AutoDetect** hello 서비스와 통신 Azure 릴레이 TCP를 통한 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-235">That same service could specify **ConnectivityMode.AutoDetect** so that hello service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="e233a-236">이 섹션에서 만든 URI hello를 사용 하 여 hello 서비스 호스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-236">Create hello service host, using hello URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="e233a-237">hello 서비스 호스트는 hello 서비스를 인스턴스화하는 hello WCF 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-237">hello service host is hello WCF object that instantiates hello service.</span></span> <span data-ttu-id="e233a-238">여기에서는 공용 인터페이스로 전달 전달 hello 유형 toocreate 서비스의 원하는 (는 `EchoService` 유형), 및 tooexpose hello 서비스 원하는 toohello 주소도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-238">Here, you pass it hello type of service you want toocreate (an `EchoService` type), and also toohello address at which you want tooexpose hello service.</span></span>
3. <span data-ttu-id="e233a-239">Hello Program.cs 파일의 hello 위쪽 참조를 너무 추가[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) 및 [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description)합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-239">At hello top of hello Program.cs file, add references too[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="e233a-240">다시 `Main()`, hello 끝점 tooenable 공용 액세스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-240">Back in `Main()`, configure hello endpoint tooenable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="e233a-241">이 단계 응용 프로그램 프로젝트에 대 한 hello ATOM 피드를 검사 하 여 공개적으로 찾을 수 있음이 hello 릴레이 서비스에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-241">This step informs hello relay service that your application can be found publicly by examining hello ATOM feed for your project.</span></span> <span data-ttu-id="e233a-242">설정한 경우 **DiscoveryType** 너무**개인**, 클라이언트는 여전히 수 tooaccess hello 서비스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-242">If you set **DiscoveryType** too**private**, a client would still be able tooaccess hello service.</span></span> <span data-ttu-id="e233a-243">그러나 hello 릴레이 네임 스페이스를 검색할 때 hello 서비스가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-243">However, hello service would not appear when it searches hello Relay namespace.</span></span> <span data-ttu-id="e233a-244">대신, 클라이언트 hello 것 tooknow hello 끝점 경로 순서를 사전입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-244">Instead, hello client would have tooknow hello endpoint path beforehand.</span></span>
5. <span data-ttu-id="e233a-245">적용 hello 서비스 hello App.config 파일에 정의 된 toohello 서비스 끝점 자격 증명:</span><span class="sxs-lookup"><span data-stu-id="e233a-245">Apply hello service credentials toohello service endpoints defined in hello App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="e233a-246">Hello 이전 단계에서 언급 한 것 처럼 여러 서비스와 hello 구성 파일에서 끝점을 선언 했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-246">As stated in hello previous step, you could have declared multiple services and endpoints in hello configuration file.</span></span> <span data-ttu-id="e233a-247">이 코드는 hello 구성 파일 및 검색을 트래버스을 설치한 경우 모든 끝점 toowhich에 대 한 자격 증명을 적용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-247">If you had, this code would traverse hello configuration file and search for every endpoint toowhich it should apply your credentials.</span></span> <span data-ttu-id="e233a-248">그러나이 자습서에서는 hello 구성 파일에 끝점이 하나 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-248">However, for this tutorial, hello configuration file has only one endpoint.</span></span>

### <a name="open-hello-service-host"></a><span data-ttu-id="e233a-249">열기 hello 서비스 호스트</span><span class="sxs-lookup"><span data-stu-id="e233a-249">Open hello service host</span></span>

1. <span data-ttu-id="e233a-250">Hello 서비스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-250">Open hello service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="e233a-251">알릴 안녕 서비스 hello 사용자를 실행 하 고 설명 방법을 tooshut hello 서비스를 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-251">Inform hello user that hello service is running, and explain how tooshut down hello service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="e233a-252">완료 되 면 hello 서비스 호스트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-252">When finished, close hello service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="e233a-253">키를 눌러 **Ctrl + Shift + B** toobuild hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="e233a-253">Press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="example"></a><span data-ttu-id="e233a-254">예제</span><span class="sxs-lookup"><span data-stu-id="e233a-254">Example</span></span>

<span data-ttu-id="e233a-255">완료된 서비스 코드는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-255">Your completed service code should appear as follows.</span></span> <span data-ttu-id="e233a-256">hello 코드 hello 서비스 계약과 구현이 포함 되어 이전 단계에서 hello 자습서에서 및 호스트 hello 서비스 콘솔 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="e233a-256">hello code includes hello service contract and implementation from previous steps in hello tutorial, and hosts hello service in a console application.</span></span>

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

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a><span data-ttu-id="e233a-257">Hello 서비스 계약에 대해 WCF 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="e233a-257">Create a WCF client for hello service contract</span></span>

<span data-ttu-id="e233a-258">다음 단계 hello toocreate 클라이언트 응용 프로그램은 하 고 이후 단계에서 구현 하는 hello 서비스 계약을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-258">hello next step is toocreate a client application and define hello service contract you will implement in later steps.</span></span> <span data-ttu-id="e233a-259">Toocreate 서비스를 사용 하는 hello 단계를 유사한 여러이 단계 참고: 자격 증명 tooconnect toohello 릴레이 서비스를 사용 하 여 파일 및 등 App.config를 편집 하는 계약을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-259">Note that many of these steps resemble hello steps used toocreate a service: defining a contract, editing an App.config file, using credentials tooconnect toohello relay service, and so on.</span></span> <span data-ttu-id="e233a-260">이러한 작업에 사용 되는 hello 코드 hello 절차 다음에 hello 예에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-260">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="e233a-261">Hello 다음을 수행 하 여 hello hello 클라이언트에 대 한 현재 Visual Studio 솔루션에서 새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-261">Create a new project in hello current Visual Studio solution for hello client by doing hello following:</span></span>

   1. <span data-ttu-id="e233a-262">솔루션 탐색기에서에 hello 서비스가 포함 된 동일한 솔루션 hello hello 현재 솔루션 (하지 hello 프로젝트)를 마우스 오른쪽 단추로 클릭 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-262">In Solution Explorer, in hello same solution that contains hello service, right-click hello current solution (not hello project), and click **Add**.</span></span> <span data-ttu-id="e233a-263">그런 후 **새 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-263">Then click **New Project**.</span></span>
   2. <span data-ttu-id="e233a-264">Hello에 **새 프로젝트 추가** 대화 상자를 클릭 **Visual C#** (경우 **Visual C#** 가 보이지 않으면 아래를 봅니다 **다른 언어**)을 선택 hello **콘솔 응용 프로그램 (.NET Framework)** 서식 파일을 하 고 이름을 **EchoClient**합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-264">In hello **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select hello **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="e233a-265">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-265">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="e233a-266">솔루션 탐색기에서 hello에 hello Program.cs 파일을 두 번 클릭 **EchoClient** 프로젝트 tooopen 아직 없는 경우 hello 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-266">In Solution Explorer, double-click hello Program.cs file in hello **EchoClient** project tooopen it in hello editor, if it is not already open.</span></span>
3. <span data-ttu-id="e233a-267">기본 이름 만으로는 hello 네임 스페이스 이름 변경 `EchoClient` 너무`Microsoft.ServiceBus.Samples`합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-267">Change hello namespace name from its default name of `EchoClient` too`Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="e233a-268">Hello 설치 [Service Bus NuGet 패키지](https://www.nuget.org/packages/WindowsAzure.ServiceBus): 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **EchoClient** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-268">Install hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click hello **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="e233a-269">Hello 클릭 **찾아보기** tab, 이후 검색할 `Microsoft Azure Service Bus`합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-269">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="e233a-270">클릭 **설치**, hello 사용 약관을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-270">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="e233a-271">추가 `using` hello에 대 한 문을 [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) hello Program.cs 파일의 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-271">Add a `using` statement for hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in hello Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="e233a-272">다음 예제는 hello와 같이 hello 서비스 계약 정의 toohello 네임 스페이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-272">Add hello service contract definition toohello namespace, as shown in hello following example.</span></span> <span data-ttu-id="e233a-273">이 정의 hello에 사용 되는 동일한 toohello 정의 **서비스** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="e233a-273">Note that this definition is identical toohello definition used in hello **Service** project.</span></span> <span data-ttu-id="e233a-274">Hello hello 위쪽에이 코드를 추가 해야 `Microsoft.ServiceBus.Samples` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-274">You should add this code at hello top of hello `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="e233a-275">키를 눌러 **Ctrl + Shift + B** toobuild hello 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-275">Press **Ctrl+Shift+B** toobuild hello client.</span></span>

### <a name="example"></a><span data-ttu-id="e233a-276">예제</span><span class="sxs-lookup"><span data-stu-id="e233a-276">Example</span></span>

<span data-ttu-id="e233a-277">hello 다음 코드에서는 hello Program.cs 파일의 현재 상태 hello hello **EchoClient** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="e233a-277">hello following code shows hello current status of hello Program.cs file in hello **EchoClient** project.</span></span>

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

## <a name="configure-hello-wcf-client"></a><span data-ttu-id="e233a-278">Hello WCF 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="e233a-278">Configure hello WCF client</span></span>

<span data-ttu-id="e233a-279">이 단계에서는이 자습서의 앞부분에서 만든 hello 서비스에 액세스 하는 기본적인 클라이언트 응용 프로그램에 대 한 App.config 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-279">In this step, you create an App.config file for a basic client application that accesses hello service created previously in this tutorial.</span></span> <span data-ttu-id="e233a-280">이 App.config 파일에는 hello 계약, 바인딩 및 hello 끝점의 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-280">This App.config file defines hello contract, binding, and name of hello endpoint.</span></span> <span data-ttu-id="e233a-281">이러한 작업에 사용 되는 hello 코드 hello 절차 다음에 hello 예에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-281">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="e233a-282">Hello의 솔루션 탐색기에서 **EchoClient** 두 번 클릭 **App.config** hello Visual Studio 편집기에서 tooopen hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-282">In Solution Explorer, in hello **EchoClient** project, double-click **App.config** tooopen hello file in hello Visual Studio editor.</span></span>
2. <span data-ttu-id="e233a-283">Hello에 `<appSettings>` 요소 hello 자리 표시자 hello 서비스 네임 스페이스, 이름으로 대체 및 SAS 키를 이전 단계에서 복사한 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-283">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="e233a-284">Hello system.serviceModel 요소 내에서 추가 된 `<client>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-284">Within hello system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="e233a-285">이 단계에서는 WCF 스타일 클라이언트 응용 프로그램을 정의함을 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-285">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="e233a-286">Hello 내 `client` 요소인 hello 이름, 계약 및 hello 끝점에 대 한 바인딩 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-286">Within hello `client` element, define hello name, contract, and binding type for hello endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="e233a-287">이 단계에는 끝점 hello hello 서비스 및 클라이언트 응용 프로그램 hello toocommunicate TCP를 사용 하 여 Azure 릴레이 된 hello 팩트에 정의 된 hello 계약의 hello 이름을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-287">This step defines hello name of hello endpoint, hello contract defined in hello service, and hello fact that hello client application uses TCP toocommunicate with Azure Relay.</span></span> <span data-ttu-id="e233a-288">hello 끝점 이름이 사용 됩니다 hello 다음 단계에서 toolink hello 서비스 URI와이 끝점 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-288">hello endpoint name is used in hello next step toolink this endpoint configuration with hello service URI.</span></span>
5. <span data-ttu-id="e233a-289">**파일**을 클릭한 다음 **모두 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-289">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="e233a-290">예제</span><span class="sxs-lookup"><span data-stu-id="e233a-290">Example</span></span>

<span data-ttu-id="e233a-291">hello 다음 코드에서는 Echo 클라이언트 hello에 대 한 hello App.config 파일</span><span class="sxs-lookup"><span data-stu-id="e233a-291">hello following code shows hello App.config file for hello Echo client.</span></span>

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

## <a name="implement-hello-wcf-client"></a><span data-ttu-id="e233a-292">Hello WCF 클라이언트 구현</span><span class="sxs-lookup"><span data-stu-id="e233a-292">Implement hello WCF client</span></span>
<span data-ttu-id="e233a-293">이 단계에서는이 자습서에서는 이전에 만든 hello 서비스에 액세스 하는 기본적인 클라이언트 응용 프로그램을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-293">In this step, you implement a basic client application that accesses hello service you created previously in this tutorial.</span></span> <span data-ttu-id="e233a-294">다양 한 hello 유사한 toohello 서비스 hello client 수행 동일한 작업 tooaccess Azure 릴레이:</span><span class="sxs-lookup"><span data-stu-id="e233a-294">Similar toohello service, hello client performs many of hello same operations tooaccess Azure Relay:</span></span>

1. <span data-ttu-id="e233a-295">Hello 연결 모드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-295">Sets hello connectivity mode.</span></span>
2. <span data-ttu-id="e233a-296">Hello hello 호스트 서비스를 찾는 URI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-296">Creates hello URI that locates hello host service.</span></span>
3. <span data-ttu-id="e233a-297">Hello 보안 자격 증명을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-297">Defines hello security credentials.</span></span>
4. <span data-ttu-id="e233a-298">Hello toohello 연결 시 자격 증명을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-298">Applies hello credentials toohello connection.</span></span>
5. <span data-ttu-id="e233a-299">Hello 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-299">Opens hello connection.</span></span>
6. <span data-ttu-id="e233a-300">Hello 응용 프로그램별 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-300">Performs hello application-specific tasks.</span></span>
7. <span data-ttu-id="e233a-301">Hello 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-301">Closes hello connection.</span></span>

<span data-ttu-id="e233a-302">그러나 hello 주요 차이점 중 하나는 hello 클라이언트 응용 프로그램이 채널 tooconnect toohello 릴레이 서비스를 사용 하는 반면 hello 서비스 너무 호출 하 여**ServiceHost**합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-302">However, one of hello main differences is that hello client application uses a channel tooconnect toohello relay service, whereas hello service uses a call too**ServiceHost**.</span></span> <span data-ttu-id="e233a-303">이러한 작업에 사용 되는 hello 코드 hello 절차 다음에 hello 예에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-303">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="e233a-304">클라이언트 응용 프로그램 구현</span><span class="sxs-lookup"><span data-stu-id="e233a-304">Implement a client application</span></span>
1. <span data-ttu-id="e233a-305">너무 hello 연결 모드를 설정**자동 검색**합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-305">Set hello connectivity mode too**AutoDetect**.</span></span> <span data-ttu-id="e233a-306">Hello hello 내부에서 코드를 다음 추가 `Main()` hello 방식의 **EchoClient** 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-306">Add hello following code inside hello `Main()` method of hello **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="e233a-307">변수 toohold hello에 대 한 값 hello 서비스 네임 스페이스 및 SAS 키 hello 콘솔에서 읽기를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-307">Define variables toohold hello values for hello service namespace, and SAS key that are read from hello console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="e233a-308">Hello 릴레이 프로젝트에서 hello 호스트의 hello 위치를 정의 하는 URI를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-308">Create hello URI that defines hello location of hello host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="e233a-309">서비스 네임 스페이스 끝점에 대 한 hello 자격 증명 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-309">Create hello credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="e233a-310">Hello App.config 파일에 설명 된 hello 구성을 로드 하는 hello 채널 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-310">Create hello channel factory that loads hello configuration described in hello App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="e233a-311">채널 팩터리는 hello 서비스 및 클라이언트 응용 프로그램은 통신 채널을 만드는 WCF 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-311">A channel factory is a WCF object that creates a channel through which hello service and client applications communicate.</span></span>
6. <span data-ttu-id="e233a-312">Hello 자격 증명을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-312">Apply hello credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="e233a-313">만들고 hello 채널 toohello 서비스를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-313">Create and open hello channel toohello service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="e233a-314">Hello 기본 사용자 인터페이스와 에코 hello에 대 한 기능을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-314">Write hello basic user interface and functionality for hello echo.</span></span>

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
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

    <span data-ttu-id="e233a-315">참고 hello 코드에서는 프록시로 hello 채널 개체의 hello 인스턴스 hello 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-315">Note that hello code uses hello instance of hello channel object as a proxy for hello service.</span></span>
9. <span data-ttu-id="e233a-316">Hello 채널 및 닫기 hello 팩터리를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-316">Close hello channel, and close hello factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="e233a-317">예제</span><span class="sxs-lookup"><span data-stu-id="e233a-317">Example</span></span>

<span data-ttu-id="e233a-318">완성 된 코드는 다음과 같이 표시 되어야 toocreate 클라이언트 응용 프로그램, 어떻게 toocall hello hello 서비스의 작업 및 hello 작업 후 tooclose 클라이언트 hello 어떻게 호출 방법을 표시 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-318">Your completed code should appear as follows, showing how toocreate a client application, how toocall hello operations of hello service, and how tooclose hello client after hello operation call is finished.</span></span>

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

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
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

## <a name="run-hello-applications"></a><span data-ttu-id="e233a-319">Hello 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="e233a-319">Run hello applications</span></span>

1. <span data-ttu-id="e233a-320">키를 눌러 **Ctrl + Shift + B** toobuild hello 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-320">Press **Ctrl+Shift+B** toobuild hello solution.</span></span> <span data-ttu-id="e233a-321">Hello 클라이언트 프로젝트와 hello 이전 단계에서 만든 hello 서비스 프로젝트를 모두 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-321">This builds both hello client project and hello service project that you created in hello previous steps.</span></span>
2. <span data-ttu-id="e233a-322">실행 중인 hello 클라이언트 응용 프로그램 하기 전에 hello 서비스 응용 프로그램이 실행 되 고 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-322">Before running hello client application, you must make sure that hello service application is running.</span></span> <span data-ttu-id="e233a-323">Visual Studio에서 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **EchoService** 솔루션을 클릭 한 다음 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-323">In Solution Explorer in Visual Studio, right-click hello **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="e233a-324">Hello 솔루션 속성 대화 상자에서 클릭 **시작 프로젝트**, 클릭 hello **여러 개의 시작 프로젝트** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-324">In hello solution properties dialog box, click **Startup Project**, then click hello **Multiple startup projects** button.</span></span> <span data-ttu-id="e233a-325">확인 **EchoService** hello 목록에 맨 먼저 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-325">Make sure **EchoService** appears first in hello list.</span></span>
4. <span data-ttu-id="e233a-326">집합 hello **동작** 두 hello에 대 한 상자 **EchoService** 및 **EchoClient** 너무 프로젝트**시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-326">Set hello **Action** box for both hello **EchoService** and **EchoClient** projects too**Start**.</span></span>

    ![][5]
5. <span data-ttu-id="e233a-327">**프로젝트 종속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-327">Click **Project Dependencies**.</span></span> <span data-ttu-id="e233a-328">Hello에 **프로젝트** 상자 **EchoClient**합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-328">In hello **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="e233a-329">Hello에 **에 따라 달라 집니다** 상자의 **EchoService** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-329">In hello **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="e233a-330">클릭 **확인** toodismiss hello **속성** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="e233a-330">Click **OK** toodismiss hello **Properties** dialog.</span></span>
7. <span data-ttu-id="e233a-331">키를 눌러 **F5** toorun 두 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-331">Press **F5** toorun both projects.</span></span>
8. <span data-ttu-id="e233a-332">두 콘솔 창에서 열고 hello 네임 스페이스 이름에 대 한 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-332">Both console windows open and prompt you for hello namespace name.</span></span> <span data-ttu-id="e233a-333">hello 서비스를 실행 해야 먼저에서 계산 hello **EchoService** 콘솔 창 hello 네임 스페이스를 입력 한 다음 키를 누릅니다 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-333">hello service must run first, so in hello **EchoService** console window, enter hello namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="e233a-334">다음으로, SAS 키를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-334">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="e233a-335">Hello SAS 키를 입력 하 고 ENTER 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-335">Enter hello SAS key and press ENTER.</span></span>

    <span data-ttu-id="e233a-336">다음은 hello 콘솔 창에서 예제 출력이입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-336">Here is example output from hello console window.</span></span> <span data-ttu-id="e233a-337">Note는 hello 값 여기에 제공 된 예를 들어 목적 으로만 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-337">Note that hello values provided here are for example purposes only.</span></span>

    <span data-ttu-id="e233a-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="e233a-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="e233a-339">hello 서비스 응용 프로그램 hello 다음 예제와 같이 toohello 콘솔 창 hello 주소를 수신 대기 중인를 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-339">hello service application prints toohello console window hello address on which it's listening, as seen in hello following example.</span></span>

    <span data-ttu-id="e233a-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span><span class="sxs-lookup"><span data-stu-id="e233a-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span></span>
10. <span data-ttu-id="e233a-341">Hello에 **EchoClient** 콘솔 창, 입력 hello hello 서비스 응용 프로그램에 대해 이전에 입력 한 동일한 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-341">In hello **EchoClient** console window, enter hello same information that you entered previously for hello service application.</span></span> <span data-ttu-id="e233a-342">이전 단계 tooenter hello hello 다음과 같은 서비스 네임 스페이스 및 SAS 키 hello 클라이언트 응용 프로그램에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-342">Follow hello previous steps tooenter hello same service namespace and SAS key values for hello client application.</span></span>
11. <span data-ttu-id="e233a-343">이러한 값을 입력 한 후 hello 클라이언트 채널 toohello 서비스 열리고 hello 다음 콘솔 출력 예제와 같이 일부 텍스트 tooenter 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-343">After entering these values, hello client opens a channel toohello service and prompts you tooenter some text as seen in hello following console output example.</span></span>

    `Enter text tooecho (or [Enter] tooexit):`

    <span data-ttu-id="e233a-344">일부 텍스트 toosend toohello 서비스 응용 프로그램을 입력 하 고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-344">Enter some text toosend toohello service application and press Enter.</span></span> <span data-ttu-id="e233a-345">이 텍스트 toohello 서비스 hello Echo 서비스 작업을 통해 전송 되 고 다음 예제 출력 hello 같이 hello 서비스 콘솔 창에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-345">This text is sent toohello service through hello Echo service operation and appears in hello service console window as in hello following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="e233a-346">hello 클라이언트 응용 프로그램의 hello hello 반환 값을 받는 `Echo` hello 원래 텍스트 이며 출력 작업 tooits 콘솔 창입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-346">hello client application receives hello return value of hello `Echo` operation, which is hello original text, and prints it tooits console window.</span></span> <span data-ttu-id="e233a-347">hello 다음은 hello 클라이언트 콘솔 창 출력 예입니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-347">hello following is example output from hello client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="e233a-348">이런이 방식으로 hello client toohello 서비스에서 텍스트 메시지를 보내는 작업을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-348">You can continue sending text messages from hello client toohello service in this manner.</span></span> <span data-ttu-id="e233a-349">완료 되 면 enter hello 클라이언트 및 서비스 콘솔 windows tooend에서 응용 프로그램을 모두 합니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-349">When you are finished, press Enter in hello client and service console windows tooend both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e233a-350">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e233a-350">Next steps</span></span>

<span data-ttu-id="e233a-351">이 자습서는 toobuild Azure 릴레이 클라이언트 응용 프로그램 및 서비스를 사용 하 여 서비스 버스의 WCF 릴레이 기능을 hello 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="e233a-351">This tutorial showed how toobuild an Azure Relay client application and service using hello WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="e233a-352">[Service Bus 메시징](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging)을 사용하는 유사한 자습서는 [Service Bus 큐 시작](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e233a-352">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="e233a-353">Azure 릴레이 대 한 자세한 toolearn hello 다음 항목을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e233a-353">toolearn more about Azure Relay, see hello following topics.</span></span>

* [<span data-ttu-id="e233a-354">Azure Service Bus 아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="e233a-354">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="e233a-355">Azure Relay 개요</span><span class="sxs-lookup"><span data-stu-id="e233a-355">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="e233a-356">Toouse hello WCF.net 서비스를 릴레이 하는 방법</span><span class="sxs-lookup"><span data-stu-id="e233a-356">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
