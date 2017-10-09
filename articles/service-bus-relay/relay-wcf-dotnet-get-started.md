---
title: ".NET에서 Azure 릴레이 WCF 릴레이 aaaGet 시작 | Microsoft Docs"
description: "Azure 릴레이 WCF toouse 서로 다른 위치에서 호스팅되는 tooconnect 두 응용 프로그램을 릴레이 하는 방법에 대해 알아봅니다."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5493281a-c2e5-49f2-87ee-9d3ffb782c75
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: a652617fc2e9b7c8d62d39fa914f77df6e3a1771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a><span data-ttu-id="0f1b4-103">Azure 릴레이 WCF toouse.NET에서 릴레이 하는 방법</span><span class="sxs-lookup"><span data-stu-id="0f1b4-103">How toouse Azure Relay WCF relays with .NET</span></span>
<span data-ttu-id="0f1b4-104">이 문서에서는 toouse Azure 릴레이 서비스를 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-104">This article describes how toouse hello Azure Relay service.</span></span> <span data-ttu-id="0f1b4-105">hello 샘플 C#으로 작성 및 hello 서비스 버스 어셈블리에에서 포함 된 확장 된 hello Windows Communication Foundation (WCF) API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-105">hello samples are written in C# and use hello Windows Communication Foundation (WCF) API with extensions contained in hello Service Bus assembly.</span></span> <span data-ttu-id="0f1b4-106">Azure 릴레이 대 한 자세한 내용은 참조 hello [Azure 릴레이 개요](relay-what-is-it.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-106">For more information about Azure relay, see hello [Azure Relay overview](relay-what-is-it.md).</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a><span data-ttu-id="0f1b4-107">WCF 릴레이란?</span><span class="sxs-lookup"><span data-stu-id="0f1b4-107">What is WCF Relay?</span></span>

<span data-ttu-id="0f1b4-108">Azure hello [ *WCF 릴레이* ](relay-what-is-it.md) 서비스를 통해 Azure 데이터 센터와 자신의 온-프레미스 엔터프라이즈 환경에서 실행 되는 toobuild 하이브리드 응용 프로그램 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-108">hello Azure [*WCF Relay*](relay-what-is-it.md) service enables you toobuild hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span></span> <span data-ttu-id="0f1b4-109">hello 릴레이 서비스가이 용이 하 게 수 있게 함으로써 toosecurely tooopen 방화벽 연결 하지 않거나 없이도 회사의 엔터프라이즈 네트워크 toohello 공용 클라우드 내에 있는 Windows Communication Foundation (WCF) 서비스를 노출 합니다. 개입 수준이 변경 tooa 회사 네트워크 인프라를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-109">hello relay service facilitates this by enabling you toosecurely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network toohello public cloud, without having tooopen a firewall connection, or requiring intrusive changes tooa corporate network infrastructure.</span></span>

![WCF 릴레이 개념](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

<span data-ttu-id="0f1b4-111">Azure 릴레이 기존 엔터프라이즈 환경 내에서 WCF 서비스를 toohost 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-111">Azure Relay enables you toohost WCF services within your existing enterprise environment.</span></span> <span data-ttu-id="0f1b4-112">그런 다음 서비스에 대 한 들어오는 세션 및 요청 toothese WCF toohello 릴레이 Azure 내에서 실행 중인 수신 대기를 위임할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-112">You can then delegate listening for incoming sessions and requests toothese WCF services toohello relay service running within Azure.</span></span> <span data-ttu-id="0f1b4-113">이 통해 tooexpose 하는 Azure 또는 toomobile 작업자 또는 파트너 엑스트라넷 환경에서 실행 되는 이러한 서비스 tooapplication 코드.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-113">This enables you tooexpose these services tooapplication code running in Azure, or toomobile workers or extranet partner environments.</span></span> <span data-ttu-id="0f1b4-114">릴레이 통해 세분화 된 수준에서 이러한 서비스에 액세스할 수 있는 toosecurely 제어할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-114">Relay enables you toosecurely control who can access these services at a fine-grained level.</span></span> <span data-ttu-id="0f1b4-115">강력 하 고 안전한 방법 tooexpose 응용 프로그램 기능 및 기존 엔터프라이즈 솔루션 및 활용이 hello 클라우드에서 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-115">It provides a powerful and secure way tooexpose application functionality and data from your existing enterprise solutions and take advantage of it from hello cloud.</span></span>

<span data-ttu-id="0f1b4-116">이 문서에서는 Azure 릴레이 toocreate toouse WCF 웹 서비스를 노출 하는 방법을 두 당사자 간에 보안 대화를 구현 하는 TCP 채널 바인딩을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-116">This article discusses how toouse Azure Relay toocreate a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a><span data-ttu-id="0f1b4-117">Service Bus NuGet 패키지를 hello</span><span class="sxs-lookup"><span data-stu-id="0f1b4-117">Get hello Service Bus NuGet package</span></span>
<span data-ttu-id="0f1b4-118">hello [Service Bus NuGet 패키지](https://www.nuget.org/packages/WindowsAzure.ServiceBus) hello 가장 쉬운 방법은 tooget hello 서비스 버스 API 및 tooconfigure hello 서비스 버스 종속성의 모든 응용 프로그램은 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-118">hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is hello easiest way tooget hello Service Bus API and tooconfigure your application with all of hello Service Bus dependencies.</span></span> <span data-ttu-id="0f1b4-119">프로젝트에서 tooinstall hello NuGet 패키지는 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-119">tooinstall hello NuGet package in your project, do hello following:</span></span>

1. <span data-ttu-id="0f1b4-120">솔루션 탐색기에서 **참조**를 마우스 오른쪽 단추로 클릭한 후 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="0f1b4-121">"서비스 버스" 및 선택 hello에 대 한 검색 **Microsoft Azure 서비스 버스** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-121">Search for "Service Bus" and select hello **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="0f1b4-122">클릭 **설치** toocomplete hello 설치의 경우 다음 hello 다음 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-122">Click **Install** toocomplete hello installation, then close hello following dialog box:</span></span>
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a><span data-ttu-id="0f1b4-123">SOAP 웹 서비스를 노출하고 TCP와 함께 이용</span><span class="sxs-lookup"><span data-stu-id="0f1b4-123">Expose and consume a SOAP web service with TCP</span></span>
<span data-ttu-id="0f1b4-124">통해 외부 기존 WCF SOAP 웹 서비스 tooexpose 변경 toohello 서비스 바인딩 및 주소와 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-124">tooexpose an existing WCF SOAP web service for external consumption, you must make changes toohello service bindings and addresses.</span></span> <span data-ttu-id="0f1b4-125">이 tooyour 구성 파일을 변경 해야 하거나 설정 하 고 구성 된 WCF 서비스는 방법에 따라 코드 변경 내용을 채워야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-125">This may require changes tooyour configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span></span> <span data-ttu-id="0f1b4-126">WCF toohave 있는지 있습니다 참고 여러 네트워크 끝점을 통해 동일한 서비스 hello, hello 기존 유지할 수 있도록 외부에 대 한 릴레이 끝점을 추가 하는 동안 내부 끝점에 액세스 hello 동일한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-126">Note that WCF allows you toohave multiple network endpoints over hello same service, so you can retain hello existing internal endpoints while adding relay endpoints for external access at hello same time.</span></span>

<span data-ttu-id="0f1b4-127">이 태스크에서는 간단한 WCF 서비스를 빌드 및 릴레이 수신기 tooit 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-127">In this task, you build a simple WCF service and add a relay listener tooit.</span></span> <span data-ttu-id="0f1b4-128">이 연습 Visual studio에 대해 어느 정도 알고 있다고 가정 하 고 프로젝트를 만드는 모든 hello 세부 정보를 통해 이동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all hello details of creating a project.</span></span> <span data-ttu-id="0f1b4-129">대신, hello 코드 중점적으로 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-129">Instead, it focuses on hello code.</span></span>

<span data-ttu-id="0f1b4-130">다음이 단계를 시작 하기 전에 hello 환 결 프로시저 tooset 다음을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-130">Before starting these steps, complete hello following procedure tooset up your environment:</span></span>

1. <span data-ttu-id="0f1b4-131">Visual Studio 내에서 두 개의 프로젝트가 "클라이언트" 및 "서비스" hello 솔루션 내를 포함 하는 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within hello solution.</span></span>
2. <span data-ttu-id="0f1b4-132">Hello Service Bus NuGet 패키지 tooboth 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-132">Add hello Service Bus NuGet package tooboth projects.</span></span> <span data-ttu-id="0f1b4-133">이 패키지는 모든 hello 필요한 어셈블리 참조 tooyour 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-133">This package adds all hello necessary assembly references tooyour projects.</span></span>

### <a name="how-toocreate-hello-service"></a><span data-ttu-id="0f1b4-134">Toocreate 서비스 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="0f1b4-134">How toocreate hello service</span></span>
<span data-ttu-id="0f1b4-135">먼저 hello 서비스 자체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-135">First, create hello service itself.</span></span> <span data-ttu-id="0f1b4-136">모든 WCF 서비스는 적어도 다음 세 가지 요소로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-136">Any WCF service consists of at least three distinct parts:</span></span>

* <span data-ttu-id="0f1b4-137">메시지를 교환 하 고 어떤 작업은 호출 toobe 설명 하는 계약의 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-137">Definition of a contract that describes what messages are exchanged and what operations are toobe invoked.</span></span>
* <span data-ttu-id="0f1b4-138">해당 계약의 구현</span><span class="sxs-lookup"><span data-stu-id="0f1b4-138">Implementation of that contract.</span></span>
* <span data-ttu-id="0f1b4-139">Hello WCF 서비스를 호스트 하 고 여러 끝점을 노출 하는 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-139">Host that hosts hello WCF service and exposes several endpoints.</span></span>

<span data-ttu-id="0f1b4-140">이 단원의 hello 코드 예제에서는 이러한 각 구성이 요소를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-140">hello code examples in this section address each of these components.</span></span>

<span data-ttu-id="0f1b4-141">한 번의 작업을 정의 하는 hello 계약 `AddNumbers`, 두 개의 숫자를 추가 하 고 hello 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-141">hello contract defines a single operation, `AddNumbers`, that adds two numbers and returns hello result.</span></span> <span data-ttu-id="0f1b4-142">hello `IProblemSolverChannel` 인터페이스 사용 hello 클라이언트 toomore는 쉽게 hello 프록시 수명을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-142">hello `IProblemSolverChannel` interface enables hello client toomore easily manage hello proxy lifetime.</span></span> <span data-ttu-id="0f1b4-143">이러한 인터페이스 생성은 모범 사례로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-143">Creating such an interface is considered a best practice.</span></span> <span data-ttu-id="0f1b4-144">것이 좋습니다 tooput이 계약 별도 파일에는 정의 "클라이언트"와 "서비스" 프로젝트에서 해당 파일을 참조할 수 있지만 두 프로젝트 모두에 hello 코드를 복사할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-144">It's a good idea tooput this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy hello code into both projects.</span></span>

```csharp
using System.ServiceModel;

[ServiceContract(Namespace = "urn:ps")]
interface IProblemSolver
{
    [OperationContract]
    int AddNumbers(int a, int b);
}

interface IProblemSolverChannel : IProblemSolver, IClientChannel {}
```

<span data-ttu-id="0f1b4-145">Hello 계약 준비에서, 구현 hello는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-145">With hello contract in place, hello implementation is as follows:</span></span>

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a><span data-ttu-id="0f1b4-146">프로그래밍 방식으로 서비스 호스트를 구성</span><span class="sxs-lookup"><span data-stu-id="0f1b4-146">Configure a service host programmatically</span></span>
<span data-ttu-id="0f1b4-147">Hello 계약 및 위치에 대 한 구현을 사용 하 여 hello 서비스를 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-147">With hello contract and implementation in place, you can now host hello service.</span></span> <span data-ttu-id="0f1b4-148">호스트 내에서 발생 한 [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) hello 서비스 인스턴스를 관리 처리는 개체를 호스트 hello 메시지를 수신 대기 하는 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of hello service and hosts hello endpoints that listen for messages.</span></span> <span data-ttu-id="0f1b4-149">hello 다음 코드 hello 및 서비스를 구성 모두 일반 로컬 끝점은 릴레이 끝점 tooillustrate hello 형태를 나란히 내부 및 외부 끝점의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-149">hello following code configures hello service with both a regular local endpoint and a relay endpoint tooillustrate hello appearance, side by side, of internal and external endpoints.</span></span> <span data-ttu-id="0f1b4-150">Hello 문자열 대체 *네임 스페이스* 네임 스페이스 이름을 가진 및 *yourKey* hello 이전 설치 단계에서 얻은 hello SAS 키를 가진 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-150">Replace hello string *namespace* with your namespace name and *yourKey* with hello SAS key that you obtained in hello previous setup step.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));

sh.AddServiceEndpoint(
   typeof (IProblemSolver), new NetTcpBinding(),
   "net.tcp://localhost:9358/solver");

sh.AddServiceEndpoint(
   typeof(IProblemSolver), new NetTcpRelayBinding(),
   ServiceBusEnvironment.CreateServiceUri("sb", "namespace", "solver"))
    .Behaviors.Add(new TransportClientEndpointBehavior {
          TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", "<yourKey>")});

sh.Open();

Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();

sh.Close();
```

<span data-ttu-id="0f1b4-151">Hello에 있는 두 개의 끝점을 만들면 hello 예제에서는 같은 계약 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-151">In hello example, you create two endpoints that are on hello same contract implementation.</span></span> <span data-ttu-id="0f1b4-152">하나는 로컬 끝점이며 다른 하나는 Azure Relay를 통해 프로젝션됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-152">One is local and one is projected through Azure Relay.</span></span> <span data-ttu-id="0f1b4-153">hello 주요 차이점은, hello 바인딩 [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) 로컬 hello에 대 한 및 [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) hello 릴레이 끝점 및 hello 주소에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-153">hello key differences between them are hello bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for hello local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for hello relay endpoint and hello addresses.</span></span> <span data-ttu-id="0f1b4-154">hello 로컬 끝점에는 고유한 포트와 로컬 네트워크 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-154">hello local endpoint has a local network address with a distinct port.</span></span> <span data-ttu-id="0f1b4-155">hello 릴레이 끝점에는 hello 문자열의 구성 된 끝점 주소 `sb`, 네임 스페이스 이름 및 "찾기" hello 경로</span><span class="sxs-lookup"><span data-stu-id="0f1b4-155">hello relay endpoint has an endpoint address composed of hello string `sb`, your namespace name, and hello path "solver."</span></span> <span data-ttu-id="0f1b4-156">이 인해 hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, 정규화 된 외부 DNS 이름으로 서비스 버스 (릴레이) TCP 끝점으로 hello 서비스 끝점을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-156">This results in hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying hello service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span></span> <span data-ttu-id="0f1b4-157">Hello 자리 표시자 hello로 바꿔 hello 코드를 추가 하는 경우 `Main` 함수 hello의 **서비스** 응용 프로그램을 작동 하는 서비스를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-157">If you place hello code replacing hello placeholders into hello `Main` function of hello **Service** application, you will have a functional service.</span></span> <span data-ttu-id="0f1b4-158">사용자 서비스 toolisten hello 릴레이에 대해서만 하려는 경우에 hello 로컬 끝점 선언을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-158">If you want your service toolisten exclusively on hello relay, remove hello local endpoint declaration.</span></span>

### <a name="configure-a-service-host-in-hello-appconfig-file"></a><span data-ttu-id="0f1b4-159">Hello App.config 파일에서 서비스 호스트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-159">Configure a service host in hello App.config file</span></span>
<span data-ttu-id="0f1b4-160">Hello App.config 파일을 사용 하 여 hello 호스트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-160">You can also configure hello host using hello App.config file.</span></span> <span data-ttu-id="0f1b4-161">hello 서비스 코드를이 예제의 호스팅 hello 다음 예제에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-161">hello service hosting code in this case appears in hello next example.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

<span data-ttu-id="0f1b4-162">hello 끝점 정의 hello App.config 파일로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-162">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="0f1b4-163">hello NuGet 패키지는 이미 정의 toohello App.config 파일의 범위를 추가 Azure 릴레이 대 한 필요한 hello 구성 확장은입니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-163">hello NuGet package has already added a range of definitions toohello App.config file, which are hello required configuration extensions for Azure Relay.</span></span> <span data-ttu-id="0f1b4-164">다음 예제는 hello 정확한 hello hello 이전 코드에 해당 하는 hello 바로 아래에 표시 되어야 **system.serviceModel** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-164">hello following example, which is hello exact equivalent of hello previous code, should appear directly beneath hello **system.serviceModel** element.</span></span> <span data-ttu-id="0f1b4-165">이 코드 예제에서는 프로젝트 C# 네임스페이스의 이름이 **Service**라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-165">This code example assumes that your project C# namespace is named **Service**.</span></span>
<span data-ttu-id="0f1b4-166">릴레이 네임 스페이스 이름 및 SAS 키와 함께 hello 자리 표시자를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-166">Replace hello placeholders with your relay namespace name and SAS key.</span></span>

```xml
<services>
    <service name="Service.ProblemSolver">
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpBinding"
                  address="net.tcp://localhost:9358/solver"/>
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpRelayBinding"
                  address="sb://<namespaceName>.servicebus.windows.net/solver"
                  behaviorConfiguration="sbTokenProvider"/>
    </service>
</services>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

<span data-ttu-id="0f1b4-167">이러한 변경을 수행한 후 hello 서비스가 시작 되 다가, 이전 처럼 두 개의 라이브 끝점으로: 하나의 로컬 및 hello 클라우드에서 하나의 수신 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-167">After you make these changes, hello service starts as it did before, but with two live endpoints: one local and one listening in hello cloud.</span></span>

### <a name="create-hello-client"></a><span data-ttu-id="0f1b4-168">Hello 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="0f1b4-168">Create hello client</span></span>
#### <a name="configure-a-client-programmatically"></a><span data-ttu-id="0f1b4-169">프로그래밍 방식으로 클라이언트를 구성</span><span class="sxs-lookup"><span data-stu-id="0f1b4-169">Configure a client programmatically</span></span>
<span data-ttu-id="0f1b4-170">tooconsume hello 서비스를 사용 하 여 WCF 클라이언트를 생성할 수 있습니다는 [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-170">tooconsume hello service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span></span> <span data-ttu-id="0f1b4-171">서비스 버스는 SAS를 사용하여 구현된 토큰 기반 보안 모델을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-171">Service Bus uses a token-based security model implemented using SAS.</span></span> <span data-ttu-id="0f1b4-172">hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) 클래스 일부 잘 알려진 토큰 공급자를 반환 하는 기본 제공 팩터리 메서드로 보안 토큰 공급자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-172">hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span></span> <span data-ttu-id="0f1b4-173">hello 다음 예제에서는 hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) hello 적절 한 SAS 토큰의 메서드 toohandle hello 획득 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-173">hello following example uses hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method toohandle hello acquisition of hello appropriate SAS token.</span></span> <span data-ttu-id="0f1b4-174">hello 이름과 키를는 hello 이전 섹션에 설명 된 대로 hello 포털에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-174">hello name and key are those obtained from hello portal as described in hello previous section.</span></span>

<span data-ttu-id="0f1b4-175">첫 번째, 참조 또는 복사 hello `IProblemSolver` hello 서비스에서 코드를 클라이언트 프로젝트에 계약입니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-175">First, reference or copy hello `IProblemSolver` contract code from hello service into your client project.</span></span>

<span data-ttu-id="0f1b4-176">그런 다음 hello의 hello 코드를 대체 `Main` 다시 릴레이 네임 스페이스 및 SAS 키와 함께 hello 개체 틀 텍스트를 대체 하는 hello 클라이언트의 메서드.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-176">Then, replace hello code in hello `Main` method of hello client, again replacing hello placeholder text with your relay namespace and SAS key.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>(
    new NetTcpRelayBinding(),
    new EndpointAddress(ServiceBusEnvironment.CreateServiceUri("sb", "<namespaceName>", "solver")));

cf.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior
            { TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey","<yourKey>") });

using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="0f1b4-177">이제 hello 클라이언트와를 실행 하는 hello 서비스를 빌드할 수 있습니다 (hello 서비스를 먼저 실행), hello 클라이언트 hello 서비스를 호출 하 고 출력 및 **9**합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-177">You can now build hello client and hello service, run them (run hello service first), and hello client calls hello service and prints **9**.</span></span> <span data-ttu-id="0f1b4-178">실행할 수 있습니다 hello 클라이언트와 서버가 서로 다른 컴퓨터에서 네트워크를 통해 및 hello 통신은 계속 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-178">You can run hello client and server on different machines, even across networks, and hello communication will still work.</span></span> <span data-ttu-id="0f1b4-179">hello 클라이언트 코드 hello 클라우드 또는 로컬로 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-179">hello client code can also run in hello cloud or locally.</span></span>

#### <a name="configure-a-client-in-hello-appconfig-file"></a><span data-ttu-id="0f1b4-180">Hello App.config 파일에 있는 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="0f1b4-180">Configure a client in hello App.config file</span></span>
<span data-ttu-id="0f1b4-181">코드 다음 hello tooconfigure hello 클라이언트를 사용 하 여 App.config 파일을 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-181">hello following code shows how tooconfigure hello client using hello App.config file.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="0f1b4-182">hello 끝점 정의 hello App.config 파일로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-182">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="0f1b4-183">hello은 앞에 나열 된 hello 코드와 같은 hello, 다음 예제에서는 직접 아래에 나타납니다 hello `<system.serviceModel>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-183">hello following example, which is hello same as hello code listed previously, should appear directly beneath hello `<system.serviceModel>` element.</span></span> <span data-ttu-id="0f1b4-184">여기에서 이전 처럼 바꿔야 hello 자리 표시자 릴레이 네임 스페이스 및 SAS 키와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-184">Here, as before, you must replace hello placeholders with your relay namespace and SAS key.</span></span>

```xml
<client>
    <endpoint name="solver" contract="Service.IProblemSolver"
              binding="netTcpRelayBinding"
              address="sb://<namespaceName>.servicebus.windows.net/solver"
              behaviorConfiguration="sbTokenProvider"/>
</client>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

## <a name="next-steps"></a><span data-ttu-id="0f1b4-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f1b4-185">Next steps</span></span>
<span data-ttu-id="0f1b4-186">릴레이 Azure의 hello 기본 사항 학습 한, 했으므로 이러한 링크 toolearn 자세한 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-186">Now that you've learned hello basics of Azure Relay, follow these links toolearn more.</span></span>

* [<span data-ttu-id="0f1b4-187">Azure 릴레이란?</span><span class="sxs-lookup"><span data-stu-id="0f1b4-187">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="0f1b4-188">Azure Service Bus 아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="0f1b4-188">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="0f1b4-189">서비스 버스 예제를 다운로드할 [Azure 샘플] [ Azure samples] hello 참조 또는 [서비스 버스 예제 개요][overview of Service Bus samples]합니다.</span><span class="sxs-lookup"><span data-stu-id="0f1b4-189">Download Service Bus samples from [Azure samples][Azure samples] or see hello [overview of Service Bus samples][overview of Service Bus samples].</span></span>

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
