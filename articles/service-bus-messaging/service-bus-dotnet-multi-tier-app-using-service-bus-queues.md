---
title: "Azure Service Bus를 사용하는 .NET 다중 계층 응용 프로그램 | Microsoft Docs"
description: "Azure에서 서비스 버스 큐를 사용하여 계층 간에 통신하는 다중 계층 응용 프로그램을 개발하는 데 도움이 되는 .NET 자습서입니다."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 8b502f5ac5d89801d390a872e7a8b06e094ecbba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="cdead-103">Azure 서비스 버스 큐를 사용하는 .NET 다중 계층 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="cdead-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="cdead-104">소개</span><span class="sxs-lookup"><span data-stu-id="cdead-104">Introduction</span></span>
<span data-ttu-id="cdead-105">Visual Studio 및 무료로 제공되는 Azure SDK for .NET을 사용하면 Microsoft Azure용 개발이 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-105">Developing for Microsoft Azure is easy using Visual Studio and the free Azure SDK for .NET.</span></span> <span data-ttu-id="cdead-106">이 자습서에서는 로컬 환경에서 실행되는 여러 Azure 리소스를 사용하는 응용 프로그램을 만드는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-106">This tutorial walks you through the steps to create an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="cdead-107">다음을 학습합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-107">You will learn the following:</span></span>

* <span data-ttu-id="cdead-108">한 번 다운로드하고 설치하여 Azure 개발용 컴퓨터를 사용하도록 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="cdead-108">How to enable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="cdead-109">Visual Studio를 사용하여 Azure용으로 개발하는 방법</span><span class="sxs-lookup"><span data-stu-id="cdead-109">How to use Visual Studio to develop for Azure.</span></span>
* <span data-ttu-id="cdead-110">웹 및 작업자 역할을 사용하여 Azure에서 다중 계층 응용 프로그램을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="cdead-110">How to create a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="cdead-111">서비스 버스 큐를 사용하여 계층 간에 통신하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-111">How to communicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="cdead-112">이 자습서에서는 Azure 클라우드 서비스에서 다중 계층 응용 프로그램을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-112">In this tutorial you'll build and run the multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="cdead-113">프런트 엔드는 ASP.NET MVC 웹 역할이고 백 엔드는 Service Bus 큐를 사용하는 작업자 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-113">The front end is an ASP.NET MVC web role and the back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="cdead-114">클라우드 서비스가 아닌 Azure 웹 사이트에 배포되는 웹 프로젝트와 동일한 다중 계층 응용 프로그램(프런트 엔드 포함)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-114">You can create the same multi-tier application with the front end as a web project, that is deployed to an Azure website instead of a cloud service.</span></span> <span data-ttu-id="cdead-115">[.NET 온-프레미스/클라우드 하이브리드 응용 프로그램](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) 자습서를 시도해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-115">You can also try out the [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="cdead-116">다음 스크린샷에서는 완성된 응용 프로그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-116">The following screen shot shows the completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="cdead-117">시나리오 개요: 역할 간 통신</span><span class="sxs-lookup"><span data-stu-id="cdead-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="cdead-118">처리할 주문을 제출하려면 웹 역할에서 실행되는 프런트 엔드 UI 구성 요소가 작업자 역할에서 실행되는 중간 계층 논리와 상호 작용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-118">To submit an order for processing, the front-end UI component, running in the web role, must interact with the middle tier logic running in the worker role.</span></span> <span data-ttu-id="cdead-119">이 예제에서는 계층 간 통신에 Service Bus 메시징을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-119">This example uses Service Bus messaging for the communication between the tiers.</span></span>

<span data-ttu-id="cdead-120">웹과 중간 계층 간에 Service Bus 메시징을 사용하면 두 구성 요소가 분리됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-120">Using Service Bus messaging between the web and middle tiers decouples the two components.</span></span> <span data-ttu-id="cdead-121">직접 메시징(즉, TCP 또는 HTTP)과 달리 웹 계층은 중간 계층에 직접 연결되지 않고 작업 단위를 메시지로 서비스 버스에 푸시하여 중간 계층에서 사용하고 처리할 준비가 될 때까지 안정적으로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-121">In contrast to direct messaging (that is, TCP or HTTP), the web tier does not connect to the middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until the middle tier is ready to consume and process them.</span></span>

<span data-ttu-id="cdead-122">서비스 버스는 조정된 메시징을 지원하는 두 개의 엔터티인 큐와 토픽을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-122">Service Bus provides two entities to support brokered messaging: queues and topics.</span></span> <span data-ttu-id="cdead-123">큐를 사용하면 큐로 전송된 각 메시지가 단일 수신기에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-123">With queues, each message sent to the queue is consumed by a single receiver.</span></span> <span data-ttu-id="cdead-124">토픽은 게시된 각 메시지를 토픽에 등록된 구독에서 사용할 수 있게 하는 게시/구독 패턴을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-124">Topics support the publish/subscribe pattern in which each published message is made available to a subscription registered with the topic.</span></span> <span data-ttu-id="cdead-125">각 구독은 메시지의 고유한 큐를 논리적으로 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="cdead-126">또한 구독은 구독 큐에 전달되는 메시지 집합을 필터와 일치하는 메시지로 제한하는 필터 규칙을 사용하여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-126">Subscriptions can also be configured with filter rules that restrict the set of messages passed to the subscription queue to those that match the filter.</span></span> <span data-ttu-id="cdead-127">다음 예에서는 서비스 버스 큐를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-127">The following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="cdead-128">이 통신 메커니즘은 직접 메시징에 비해 몇 가지 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="cdead-129">**임시 분리**</span><span class="sxs-lookup"><span data-stu-id="cdead-129">**Temporal decoupling.**</span></span> <span data-ttu-id="cdead-130">비동기 메시징 패턴을 사용하면 생산자와 소비자가 동시에 온라인 상태일 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-130">With the asynchronous messaging pattern, producers and consumers need not be online at the same time.</span></span> <span data-ttu-id="cdead-131">서비스 버스는 소비하는 쪽에서 메시지를 수신할 준비가 될 때까지 메시지를 안정적으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-131">Service Bus reliably stores messages until the consuming party is ready to receive them.</span></span> <span data-ttu-id="cdead-132">따라서 전체 시스템에는 영향을 주지 않고 자발적으로(예: 유지 관리의 경우) 또는 구성 요소 크래시로 인해 분산 응용 프로그램 구성 요소의 연결을 끊을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-132">This enables the components of the distributed application to be disconnected, either voluntarily, for example, for maintenance, or due to a component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="cdead-133">또한 소비 응용 프로그램은 하루 중 특정 기간 동안만 온라인 상태로 전환해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-133">Furthermore, the consuming application might only need to come online during certain times of the day.</span></span>
* <span data-ttu-id="cdead-134">**부하 평준화**</span><span class="sxs-lookup"><span data-stu-id="cdead-134">**Load leveling.**</span></span> <span data-ttu-id="cdead-135">많은 응용 프로그램에서 시스템 부하는 시간에 따라 다르지만 각 작업 단위에 필요한 처리 시간은 일반적으로 일정합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-135">In many applications, system load varies over time, while the processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="cdead-136">큐를 사용한 메시지 생산자와 소비자 조정은 최대 부하가 아닌 평균 부하를 수용하려면 소비 응용 프로그램(작업자)만 프로비전해야 함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-136">Intermediating message producers and consumers with a queue means that the consuming application (the worker) only needs to be provisioned to accommodate average load rather than peak load.</span></span> <span data-ttu-id="cdead-137">수신 부하가 변경됨에 따라 큐의 깊이가 증가하고 축소됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-137">The depth of the queue grows and contracts as the incoming load varies.</span></span> <span data-ttu-id="cdead-138">따라서 응용 프로그램 부하를 제공하는 데 필요한 인프라의 크기와 관련하여 비용이 직접적으로 절약됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-138">This directly saves money in terms of the amount of infrastructure required to service the application load.</span></span>
* <span data-ttu-id="cdead-139">**부하 분산**</span><span class="sxs-lookup"><span data-stu-id="cdead-139">**Load balancing.**</span></span> <span data-ttu-id="cdead-140">부하가 증가하면 뷰에서 읽을 작업자 프로세스가 더 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-140">As load increases, more worker processes can be added to read from the queue.</span></span> <span data-ttu-id="cdead-141">각 메시지는 하나의 작업자 프로세스를 통해서만 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-141">Each message is processed by only one of the worker processes.</span></span> <span data-ttu-id="cdead-142">또한 이 가져오기 기반 부하 분산에서는 작업자 컴퓨터가 최대 속도로 메시지를 가져올 때 처리 능력이 다른 경우에도 작업자 컴퓨터의 최적 사용률을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-142">Furthermore, this pull-based load balancing enables optimal use of the worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="cdead-143">이 패턴을 종종 *경쟁 소비자* 패턴이라고 부릅니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-143">This pattern is often termed the *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="cdead-144">다음 섹션에서는 이 아키텍처를 구현하는 코드에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-144">The following sections discuss the code that implements this architecture.</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="cdead-145">개발 환경 설정</span><span class="sxs-lookup"><span data-stu-id="cdead-145">Set up the development environment</span></span>
<span data-ttu-id="cdead-146">Azure 응용 프로그램 개발을 시작하려면 먼저 도구를 얻고 개발 환경을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-146">Before you can begin developing Azure applications, get the tools and set up your development environment.</span></span>

1. <span data-ttu-id="cdead-147">SDK [다운로드 페이지](https://azure.microsoft.com/downloads/)에서 .NET용 Azure SDK를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-147">Install the Azure SDK for .NET from the SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="cdead-148">**.NET** 열에서 사용 중인 [Visual Studio](http://www.visualstudio.com) 버전을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-148">In the **.NET** column, click the version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="cdead-149">이 자습서의 단계에서는 Visual Studio 2015를 사용하지만 Visual Studio 2017에도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-149">The steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="cdead-150">설치 관리자를 실행할지 또는 저장할지를 묻는 메시지가 표시되면 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-150">When prompted to run or save the installer, click **Run**.</span></span>
4. <span data-ttu-id="cdead-151">**웹 플랫폼 설치 관리자**에서 **설치**를 클릭하여 설치를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-151">In the **Web Platform Installer**, click **Install** and proceed with the installation.</span></span>
5. <span data-ttu-id="cdead-152">설치가 완료되면 앱을 개발하기 시작하는 데 필요한 내용이 모두 준비된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-152">Once the installation is complete, you will have everything necessary to start to develop the app.</span></span> <span data-ttu-id="cdead-153">SDK에는 Visual Studio에서 Azure 응용 프로그램을 쉽게 개발할 수 있는 도구가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-153">The SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="cdead-154">네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="cdead-154">Create a namespace</span></span>
<span data-ttu-id="cdead-155">다음 단계에서는 서비스 네임스페이스를 만들고 SAS(공유 액세스 서명) 키를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-155">The next step is to create a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="cdead-156">네임스페이스는 서비스 버스를 통해 노출되는 각 응용 프로그램에 대한 응용 프로그램 경계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="cdead-157">SAS 키는 네임스페이스가 만들어질 때 시스템에 의해 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-157">A SAS key is generated by the system when a namespace is created.</span></span> <span data-ttu-id="cdead-158">네임스페이스 및 SAS 키 조합은 서비스 버스에 자격 증명을 제공하여 응용 프로그램에 대한 액세스를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-158">The combination of namespace and SAS key provides the credentials for Service Bus to authenticate access to an application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="cdead-159">웹 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="cdead-159">Create a web role</span></span>
<span data-ttu-id="cdead-160">이 섹션에서는 응용 프로그램의 프런트 엔드를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-160">In this section, you build the front end of your application.</span></span> <span data-ttu-id="cdead-161">먼저 응용 프로그램에서 표시하는 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-161">First, you create the pages that your application displays.</span></span>
<span data-ttu-id="cdead-162">그런 다음 서비스 버스 큐에 항목을 제출하고 큐에 대한 상태 정보를 표시하는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-162">After that, add code that submits items to a Service Bus queue and displays status information about the queue.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="cdead-163">프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="cdead-163">Create the project</span></span>
1. <span data-ttu-id="cdead-164">관리자 권한을 사용하여 Visual Studio 시작: **Visual Studio** 프로그램 아이콘을 마우스 오른쪽 단추로 클릭한 다음 **관리자 권한으로 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-164">Using administrator privileges, start Visual Studio: right-click the **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="cdead-165">이 문서의 뒷부분에서 설명하는 Azure 계산 에뮬레이터를 사용하려면 Visual Studio를 관리자 권한으로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-165">The Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="cdead-166">Visual Studio의 **파일** 메뉴에서 **새로 만들기**를 클릭한 다음 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-166">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="cdead-167">**설치된 템플릿**의 **Visual C#**에서 **클라우드**를 클릭한 다음 **Azure Cloud Service**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="cdead-168">프로젝트의 이름을 **MultiTierApp**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-168">Name the project **MultiTierApp**.</span></span> <span data-ttu-id="cdead-169">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="cdead-170">**.NET Framework 4.5** 역할에서 **ASP.NET 웹 역할**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="cdead-171">**Azure Cloud Service 솔루션**에서 **WebRole1**을 마우스로 가리키고 연필 아이콘을 클릭한 다음 웹 역할의 이름을 **FrontendWebRole**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click the pencil icon, and rename the web role to **FrontendWebRole**.</span></span> <span data-ttu-id="cdead-172">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-172">Then click **OK**.</span></span> <span data-ttu-id="cdead-173">"FrontEnd"가 아니라 소문자 "e"를 사용하여 "Frontend"를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="cdead-174">**새 ASP.NET 프로젝트** 대화 상자의 **템플릿 선택** 목록에서 **MVC**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-174">From the **New ASP.NET Project** dialog box, in the **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="cdead-175">**새 ASP.NET 프로젝트** 대화 상자에서 **인증 변경** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-175">Still in the **New ASP.NET Project** dialog box, click the **Change Authentication** button.</span></span> <span data-ttu-id="cdead-176">**인증 변경** 대화 상자에서 **인증 없음**, **확인**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-176">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="cdead-177">이 자습서의 경우 사용자 로그인이 필요하지 않은 앱을 배포하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="cdead-178">**새 ASP.NET 프로젝트** 대화 상자로 돌아와서 **확인**을 클릭하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-178">Back in the **New ASP.NET Project** dialog box, click **OK** to create the project.</span></span>
8. <span data-ttu-id="cdead-179">**FrontendWebRole** 프로젝트의 **솔루션 탐색기**에서 **참조**를 마우스 오른쪽 단추로 클릭한 후 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-179">In **Solution Explorer**, in the **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="cdead-180">**찾아보기** 탭을 클릭한 다음 `Microsoft Azure Service Bus`를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-180">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="cdead-181">**WindowsAzure.ServiceBus** 패키지를 선택하고 **설치**를 클릭하고 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-181">Select the **WindowsAzure.ServiceBus** package, click **Install**, and accept the terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="cdead-182">이제 필요한 클라이언트 어셈블리가 참조되고 몇 가지 새 코드 파일이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-182">Note that the required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="cdead-183">**솔루션 탐색기**에서 **모델**을 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 다음 **클래스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="cdead-184">**이름** 상자에 **OnlineOrder.cs**라는 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-184">In the **Name** box, type the name **OnlineOrder.cs**.</span></span> <span data-ttu-id="cdead-185">그런 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-185">Then click **Add**.</span></span>

### <a name="write-the-code-for-your-web-role"></a><span data-ttu-id="cdead-186">웹 역할에 대한 코드 작성</span><span class="sxs-lookup"><span data-stu-id="cdead-186">Write the code for your web role</span></span>
<span data-ttu-id="cdead-187">이 섹션에서는 응용 프로그램에서 표시하는 다양한 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-187">In this section, you create the various pages that your application displays.</span></span>

1. <span data-ttu-id="cdead-188">Visual Studio의 OnlineOrder.cs 파일에서 기존 네임스페이스 정의를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-188">In the OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with the following code:</span></span>
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. <span data-ttu-id="cdead-189">**솔루션 탐색기**에서 **Controllers\HomeController.cs**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="cdead-190">파일 맨 위에 다음 **using** 문을 추가하여 Service Bus뿐만 아니라 방금 만든 모델에 대한 네임스페이스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-190">Add the following **using** statements at the top of the file to include the namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="cdead-191">또한 Visual Studio의 HomeController.cs 파일에서 기존 네임스페이스 정의를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-191">Also in the HomeController.cs file in Visual Studio, replace the existing namespace definition with the following code.</span></span> <span data-ttu-id="cdead-192">이 코드에는 큐에 대한 항목 제출을 처리하는 메서드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-192">This code contains methods for handling the submission of items to the queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect to Submit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for the submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from the submission
           // form.
           [HttpPost]
           // Attribute to help prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting to queue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. <span data-ttu-id="cdead-193">**빌드** 메뉴에서 **솔루션 빌드**를 클릭하여 지금까지의 작업에 대한 정확성을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-193">From the **Build** menu, click **Build Solution** to test the accuracy of your work so far.</span></span>
5. <span data-ttu-id="cdead-194">이제 위에서 만든 `Submit()` 메서드에 대한 보기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-194">Now, create the view for the `Submit()` method you created earlier.</span></span> <span data-ttu-id="cdead-195">`Submit()` 메서드(매개 변수를 사용하지 않는 `Submit()`의 오버로드) 내에서 마우스 오른쪽 단추로 클릭한 다음 **보기 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-195">Right-click within the `Submit()` method (the overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="cdead-196">보기를 만들 수 있는 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-196">A dialog box appears for creating the view.</span></span> <span data-ttu-id="cdead-197">**템플릿** 목록에서 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-197">In the **Template** list, choose **Create**.</span></span> <span data-ttu-id="cdead-198">**모델 클래스** 목록에서 **OnlineOrder** 클래스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-198">In the **Model class** list, click the **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="cdead-199">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-199">Click **Add**.</span></span>
8. <span data-ttu-id="cdead-200">이제 응용 프로그램의 표시 이름을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-200">Now, change the displayed name of your application.</span></span> <span data-ttu-id="cdead-201">**솔루션 탐색기**에서 **Views\Shared\\_Layout.cshtml** 파일을 두 번 클릭하여 Visual Studio 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file to open it in the Visual Studio editor.</span></span>
9. <span data-ttu-id="cdead-202">**내 ASP.NET 응용 프로그램**과 일치하는 모든 항목을 **LITWARE 제품**으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="cdead-203">**홈**, **정보** 및 **연락처** 링크를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-203">Remove the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="cdead-204">강조 표시된 코드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-204">Delete the highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="cdead-205">마지막으로 큐에 대한 일부 정보를 포함하도록 제출 페이지를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-205">Finally, modify the submission page to include some information about the queue.</span></span> <span data-ttu-id="cdead-206">**솔루션 탐색기**에서 **Views\Home\Submit.cshtml** 파일을 두 번 클릭하여 Visual Studio 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file to open it in the Visual Studio editor.</span></span> <span data-ttu-id="cdead-207">`<h2>Submit</h2>` 뒤에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-207">Add the following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="cdead-208">이제 `ViewBag.MessageCount`은(는) 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-208">For now, the `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="cdead-209">나중에 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting to be processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="cdead-210">이제 UI를 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-210">You now have implemented your UI.</span></span> <span data-ttu-id="cdead-211">**F5** 키를 눌러 응용 프로그램을 실행하고 예상대로 나타나는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-211">You can press **F5** to run your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-the-code-for-submitting-items-to-a-service-bus-queue"></a><span data-ttu-id="cdead-212">서비스 버스 큐에 항목을 제출하는 코드 작성</span><span class="sxs-lookup"><span data-stu-id="cdead-212">Write the code for submitting items to a Service Bus queue</span></span>
<span data-ttu-id="cdead-213">이제 큐에 항목을 제출하는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-213">Now, add code for submitting items to a queue.</span></span> <span data-ttu-id="cdead-214">먼저 서비스 버스 큐 연결 정보를 포함하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="cdead-215">그런 다음 Global.aspx.cs에서 연결을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="cdead-216">끝으로, 앞에서 만든 제출 코드를 HomeController.cs에서 업데이트하여 항목을 서비스 버스 큐에 실제로 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-216">Finally, update the submission code you created earlier in HomeController.cs to actually submit items to a Service Bus queue.</span></span>

1. <span data-ttu-id="cdead-217">**솔루션 탐색기**에서 **FrontendWebRole**을 마우스 오른쪽 단추로 클릭합니다(역할이 아닌 프로젝트를 마우스 오른쪽 단추로 클릭).</span><span class="sxs-lookup"><span data-stu-id="cdead-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click the project, not the role).</span></span> <span data-ttu-id="cdead-218">**추가**를 클릭한 후 **클래스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="cdead-219">클래스 이름을 **QueueConnector.cs**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-219">Name the class **QueueConnector.cs**.</span></span> <span data-ttu-id="cdead-220">**추가**를 클릭하여 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-220">Click **Add** to create the class.</span></span>
3. <span data-ttu-id="cdead-221">이제 연결 정보를 캡슐화하고 서비스 버스 큐에 대한 연결을 초기화하는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-221">Now, add code that encapsulates the connection information and initializes the connection to a Service Bus queue.</span></span> <span data-ttu-id="cdead-222">QueueConnector.cs의 전체 내용을 다음 코드로 바꾸고 `your Service Bus namespace`(네임스페이스 이름) 및 `yourKey`의 값을 입력합니다. 이는 Azure Portal에서 이전에 가져온 **기본 키**입니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-222">Replace the entire contents of QueueConnector.cs with the following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is the **primary key** you previously obtained from the Azure portal.</span></span>
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from the portal.
           public const string Namespace = "your Service Bus namespace";
   
           // The name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create the namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http to be friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create the namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create the queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client to the queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="cdead-223">이제 **Initialize** 메서드가 호출되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="cdead-224">**솔루션 탐색기**에서 **Global.asax\Global.asax.cs**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="cdead-225">다음 코드 줄을 **Application_Start** 메서드의 끝에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-225">Add the following line of code at the end of the **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="cdead-226">끝으로, 앞에서 만든 웹 코드를 업데이트하여 항목을 큐에 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-226">Finally, update the web code you created earlier, to submit items to the queue.</span></span> <span data-ttu-id="cdead-227">**솔루션 탐색기**에서 **Controllers\HomeController.cs**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="cdead-228">다음과 같이 `Submit()` 메서드(매개 변수를 사용하지 않는 오버로드)를 업데이트하여 큐에 대한 메시지 수를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-228">Update the `Submit()` method (the overload that takes no parameters) as follows to get the message count for the queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you to perform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get the queue, and obtain the message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="cdead-229">다음과 같이 `Submit(OnlineOrder order)` 메서드(하나의 매개 변수를 사용하는 오버로드)를 업데이트하여 큐에 주문 정보를 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-229">Update the `Submit(OnlineOrder order)` method (the overload that takes one parameter) as follows to submit order information to the queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from the order.
           var message = new BrokeredMessage(order);
   
           // Submit the order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="cdead-230">이제 응용 프로그램을 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-230">You can now run the application again.</span></span> <span data-ttu-id="cdead-231">주문을 제출할 때마다 메시지 수가 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-231">Each time you submit an order, the message count increases.</span></span>
   
   ![][18]

## <a name="create-the-worker-role"></a><span data-ttu-id="cdead-232">작업자 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="cdead-232">Create the worker role</span></span>
<span data-ttu-id="cdead-233">이제 주문 제출을 처리하는 작업자 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-233">You will now create the worker role that processes the order submissions.</span></span> <span data-ttu-id="cdead-234">이 예제에서는 **Service Bus 큐가 있는 작업자 역할** Visual Studio 프로젝트 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-234">This example uses the **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="cdead-235">포털에서 필요한 자격 증명을 이미 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-235">You already obtained the required credentials from the portal.</span></span>

1. <span data-ttu-id="cdead-236">Visual Studio를 Azure 계정에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-236">Make sure you have connected Visual Studio to your Azure account.</span></span>
2. <span data-ttu-id="cdead-237">Visual Studio의 **솔루션 탐색기**에서 **MultiTierApp** 프로젝트 아래의 **역할** 폴더를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under the **MultiTierApp** project.</span></span>
3. <span data-ttu-id="cdead-238">**추가**를 클릭한 후 **새 작업자 역할 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="cdead-239">**새 역할 프로젝트 추가** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-239">The **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="cdead-240">**새 역할 프로젝트 추가** 대화 상자에서 **Service Bus 큐가 있는 작업자 역할**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-240">In the **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="cdead-241">**이름** 상자에서 프로젝트 이름을 **OrderProcessingRole**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-241">In the **Name** box, name the project **OrderProcessingRole**.</span></span> <span data-ttu-id="cdead-242">그런 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-242">Then click **Add**.</span></span>
6. <span data-ttu-id="cdead-243">"서비스 버스 네임스페이스 만들기" 섹션의 9단계에서 얻은 연결 문자열을 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-243">Copy the connection string that you obtained in step 9 of the "Create a Service Bus namespace" section to the clipboard.</span></span>
7. <span data-ttu-id="cdead-244">**솔루션 탐색기**에서, 5단계에서 만든 **OrderProcessingRole**을 마우스 오른쪽 단추로 클릭합니다. 이때 클래스가 아니라 **역할**에서 **OrderProcessingRole**을 마우스 오른쪽 단추로 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-244">In **Solution Explorer**, right-click the **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not the class).</span></span> <span data-ttu-id="cdead-245">그런 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="cdead-246">**속성** 대화 상자의 **설정** 탭에서 **Microsoft.ServiceBus.ConnectionString**의 **값** 상자 내부를 클릭한 다음 6단계에서 복사한 끝점 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-246">On the **Settings** tab of the **Properties** dialog box, click inside the **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste the endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="cdead-247">**OnlineOrder** 클래스를 만들어 큐에서 처리할 때 주문을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-247">Create an **OnlineOrder** class to represent the orders as you process them from the queue.</span></span> <span data-ttu-id="cdead-248">이미 만든 클래스를 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="cdead-249">**솔루션 탐색기**에서 **OrderProcessingRole** 클래스를 마우스 오른쪽 단추로 클릭합니다(역할이 아닌 클래스 아이콘을 마우스 오른쪽 단추로 클릭).</span><span class="sxs-lookup"><span data-stu-id="cdead-249">In **Solution Explorer**, right-click the **OrderProcessingRole** class (right-click the class icon, not the role).</span></span> <span data-ttu-id="cdead-250">**추가**를 클릭한 후 **기존 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="cdead-251">**FrontendWebRole\Models**의 하위 폴더로 이동하고 **OnlineOrder.cs**를 두 번 클릭하여 이 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-251">Browse to the subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** to add it to this project.</span></span>
11. <span data-ttu-id="cdead-252">**WorkerRole.cs**에서 다음 코드와 같이 **QueueName** 변수 값을 `"ProcessingQueue"`에서 `"OrdersQueue"`(으)로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-252">In **WorkerRole.cs**, change the value of the **QueueName** variable from `"ProcessingQueue"` to `"OrdersQueue"` as shown in the following code.</span></span>
    
    ```csharp
    // The name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="cdead-253">WorkerRole.cs 파일 맨 위에 다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-253">Add the following using statement at the top of the WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="cdead-254">`Run()` 함수의 `OnMessage()` 호출 내에서 `try` 절의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-254">In the `Run()` function, inside the `OnMessage()` call, replace the contents of the `try` clause with the following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View the message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="cdead-255">응용 프로그램을 완성했습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-255">You have completed the application.</span></span> <span data-ttu-id="cdead-256">솔루션 탐색기에서 MultiTierApp 프로젝트를 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트로 설정**을 선택한 후 F5 키를 눌러 전체 응용 프로그램을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-256">You can test the full application by right-clicking the MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="cdead-257">작업자 역할에서 큐의 항목을 처리하고 완료로 표시하므로 메시지 수가 증가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-257">Note that the message count does not increment, because the worker role processes items from the queue and marks them as complete.</span></span> <span data-ttu-id="cdead-258">Azure 계산 에뮬레이터 UI를 표시하여 작업자 역할의 추적 출력을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-258">You can see the trace output of your worker role by viewing the Azure Compute Emulator UI.</span></span> <span data-ttu-id="cdead-259">이 작업은 작업 표시줄의 알림 영역에 있는 에뮬레이터 아이콘을 마우스 오른쪽 단추로 클릭하고 **계산 에뮬레이터 UI 표시**를 선택하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdead-259">You can do this by right-clicking the emulator icon in the notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="cdead-260">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cdead-260">Next steps</span></span>
<span data-ttu-id="cdead-261">서비스 버스에 대한 자세한 내용은 다음 리소스를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="cdead-261">To learn more about Service Bus, see the following resources:</span></span>  

* <span data-ttu-id="cdead-262">[Azure Service Bus 설명서][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="cdead-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="cdead-263">[Service Bus 서비스 페이지][sbacom]</span><span class="sxs-lookup"><span data-stu-id="cdead-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="cdead-264">[Service Bus 큐를 사용하는 방법][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="cdead-264">[How to Use Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="cdead-265">다중 계층 시나리오에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdead-265">To learn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="cdead-266">[저장소 테이블, 큐 및 Blob을 사용하는 .NET 다중 계층 응용 프로그램][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="cdead-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
