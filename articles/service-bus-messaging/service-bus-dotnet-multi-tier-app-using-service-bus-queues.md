---
title: "Azure 서비스 버스를 사용 하 여 다중 계층 응용 프로그램 aaa.NET | Microsoft Docs"
description: "서비스 버스 큐 toocommunicate 계층 사이 사용 하 여 Azure에서 다중 계층 응용 프로그램을 개발 하는 때 도움이 되는.NET 자습서입니다."
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
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="539dc-103">Azure 서비스 버스 큐를 사용하는 .NET 다중 계층 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="539dc-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="539dc-104">소개</span><span class="sxs-lookup"><span data-stu-id="539dc-104">Introduction</span></span>
<span data-ttu-id="539dc-105">Microsoft Azure가 Visual Studio를 사용 하 여 쉽게, hello.NET 용 Azure SDK를 무료 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-105">Developing for Microsoft Azure is easy using Visual Studio and hello free Azure SDK for .NET.</span></span> <span data-ttu-id="539dc-106">이 자습서에서는 hello 단계 toocreate 로컬 환경에서 실행 되는 여러 Azure 리소스를 사용 하는 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-106">This tutorial walks you through hello steps toocreate an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="539dc-107">Hello 다음에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-107">You will learn hello following:</span></span>

* <span data-ttu-id="539dc-108">어떻게 tooenable 단일 Azure 개발 컴퓨터에서 다운로드 및 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-108">How tooenable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="539dc-109">어떻게 Azure에 대 한 Visual Studio toodevelop toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-109">How toouse Visual Studio toodevelop for Azure.</span></span>
* <span data-ttu-id="539dc-110">어떻게 toocreate 웹 및 작업자 역할을 사용 하 여 Azure에서 다중 계층 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-110">How toocreate a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="539dc-111">사이의 toocommunicate 서비스 버스 큐를 사용 하 여 눈금 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-111">How toocommunicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="539dc-112">이 자습서에서는 빌드하고 Azure 클라우드 서비스에서 hello 다중 계층 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-112">In this tutorial you'll build and run hello multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="539dc-113">hello 프런트 엔드는 ASP.NET MVC 웹 역할 및 hello 백 엔드는 서비스 버스 큐를 사용 하는 작업자 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-113">hello front end is an ASP.NET MVC web role and hello back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="539dc-114">만들 수 있습니다 같은 다중 계층 응용 프로그램 프런트 엔드 hello와 배포 tooan 클라우드 서비스가 아닌 Azure 웹 사이트를 웹 프로젝트로 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-114">You can create hello same multi-tier application with hello front end as a web project, that is deployed tooan Azure website instead of a cloud service.</span></span> <span data-ttu-id="539dc-115">Hello 아웃 보십시오 [.NET에서-프레미스/클라우드 하이브리드 응용 프로그램](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-115">You can also try out hello [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="539dc-116">hello 다음 스크린 샷에 표시 완료 hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-116">hello following screen shot shows hello completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="539dc-117">시나리오 개요: 역할 간 통신</span><span class="sxs-lookup"><span data-stu-id="539dc-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="539dc-118">hello 프런트 엔드 UI 구성 요소, hello 웹 역할에서 실행을 처리 하는 것에 대 한 주문 toosubmit hello 작업자 역할에서 실행 하는 hello 중간 계층 논리와 상호 작용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-118">toosubmit an order for processing, hello front-end UI component, running in hello web role, must interact with hello middle tier logic running in hello worker role.</span></span> <span data-ttu-id="539dc-119">이 예제에서는 서비스 버스 메시징 hello 계층 간 hello 통신에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-119">This example uses Service Bus messaging for hello communication between hello tiers.</span></span>

<span data-ttu-id="539dc-120">서비스 버스를 사용 하 여 hello 웹 및 중간 계층 간의 메시징 분리 하는 두 구성 요소.</span><span class="sxs-lookup"><span data-stu-id="539dc-120">Using Service Bus messaging between hello web and middle tiers decouples the two components.</span></span> <span data-ttu-id="539dc-121">반대로 hello toodirect 메시징 (즉, TCP 또는 HTTP) 웹 계층 toohello 중간 계층을 직접; 연결 되지 않습니다 대신 안정적으로 hello 중간 계층은 tooconsume 준비 될 때까지 유지 하 고 처리 하는 서비스 버스에 메시지로 작업의 단위 밀어냅니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-121">In contrast toodirect messaging (that is, TCP or HTTP), hello web tier does not connect toohello middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until hello middle tier is ready tooconsume and process them.</span></span>

<span data-ttu-id="539dc-122">두 엔터티 toosupport 조정 된 메시징을 제공 하는 서비스 버스: 큐 및 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-122">Service Bus provides two entities toosupport brokered messaging: queues and topics.</span></span> <span data-ttu-id="539dc-123">큐와 각 메시지를 보낼 toohello 큐는 단일 수신기에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-123">With queues, each message sent toohello queue is consumed by a single receiver.</span></span> <span data-ttu-id="539dc-124">항목 게시 된 각 메시지 hello 항목으로 등록 하는 사용 가능한 tooa 구독 수는 hello 게시/구독 패턴을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-124">Topics support hello publish/subscribe pattern in which each published message is made available tooa subscription registered with hello topic.</span></span> <span data-ttu-id="539dc-125">각 구독은 메시지의 고유한 큐를 논리적으로 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="539dc-126">메시지 전달 hello 구독 큐 toothose hello 필터와 일치 하는 hello 집합을 제한 하는 필터 규칙으로 구독을 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-126">Subscriptions can also be configured with filter rules that restrict hello set of messages passed to hello subscription queue toothose that match hello filter.</span></span> <span data-ttu-id="539dc-127">hello 다음 예제에서는 서비스 버스 큐.</span><span class="sxs-lookup"><span data-stu-id="539dc-127">hello following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="539dc-128">이 통신 메커니즘은 직접 메시징에 비해 몇 가지 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="539dc-129">**임시 분리**</span><span class="sxs-lookup"><span data-stu-id="539dc-129">**Temporal decoupling.**</span></span> <span data-ttu-id="539dc-130">Hello 비동기 메시징 패턴을 사용한 생산자와 소비자가 아니어도 hello에서 온라인으로 동시 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-130">With hello asynchronous messaging pattern, producers and consumers need not be online at hello same time.</span></span> <span data-ttu-id="539dc-131">서비스 버스 사용 중인 파티가 hello를 받을 준비가 될 때까지 메시지를 안정적으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-131">Service Bus reliably stores messages until hello consuming party is ready to receive them.</span></span> <span data-ttu-id="539dc-132">이 통해 연결이 해제 하거나 자발적으로 tooa 구성 요소 크래시 등 기한 또는 유지 관리에 대 한 예를 들어 시스템 전체에 영향을 주지 않고 hello 분산 응용 프로그램 toobe의 hello 구성 요소.</span><span class="sxs-lookup"><span data-stu-id="539dc-132">This enables hello components of hello distributed application toobe disconnected, either voluntarily, for example, for maintenance, or due tooa component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="539dc-133">또한 응용 프로그램을 사용 하는 hello은 hello 하루 중 특정 시간 동안 toocome 온라인 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-133">Furthermore, hello consuming application might only need toocome online during certain times of hello day.</span></span>
* <span data-ttu-id="539dc-134">**부하 평준화**</span><span class="sxs-lookup"><span data-stu-id="539dc-134">**Load leveling.**</span></span> <span data-ttu-id="539dc-135">각 작업 단위에 필요한 hello 처리 시간은 일반적으로 일정는 많은 응용 프로그램에서 시스템 부하 시간이 지남에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-135">In many applications, system load varies over time, while hello processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="539dc-136">여 메시지 생산자와 소비자는 큐와 최대 부하 대신 평균 부하 tooaccommodate 프로 비전 하는 응용 프로그램 (hello 작업자)만 요구 toobe를 사용해 해당 hello 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-136">Intermediating message producers and consumers with a queue means that hello consuming application (hello worker) only needs toobe provisioned tooaccommodate average load rather than peak load.</span></span> <span data-ttu-id="539dc-137">증가 하 고 hello 수신 부하가 변경 됨에 따라 축소 하는 hello 큐의 hello 깊이입니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-137">hello depth of hello queue grows and contracts as hello incoming load varies.</span></span> <span data-ttu-id="539dc-138">직접 money hello 양의 인프라 필요한 tooservice hello 응용 프로그램 부하를 기준으로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-138">This directly saves money in terms of hello amount of infrastructure required tooservice hello application load.</span></span>
* <span data-ttu-id="539dc-139">**부하 분산**</span><span class="sxs-lookup"><span data-stu-id="539dc-139">**Load balancing.**</span></span> <span data-ttu-id="539dc-140">부하가 증가 하면 작업자 프로세스가 더 추가할 수 있습니다 tooread hello 큐에서.</span><span class="sxs-lookup"><span data-stu-id="539dc-140">As load increases, more worker processes can be added tooread from hello queue.</span></span> <span data-ttu-id="539dc-141">Hello 작업자 프로세스 중 하나에만 각 메시지를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-141">Each message is processed by only one of hello worker processes.</span></span> <span data-ttu-id="539dc-142">또한이 끌어오기 기반 부하 분산 사용 하면 hello 작업자 컴퓨터의 최적 사용 작업자 컴퓨터의 관점에서 처리 능력을 다른 경우에 자신의 최대 속도로 메시지를 가져올 때.</span><span class="sxs-lookup"><span data-stu-id="539dc-142">Furthermore, this pull-based load balancing enables optimal use of hello worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="539dc-143">이 패턴을 hello 종종 *경쟁 소비자* 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-143">This pattern is often termed hello *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="539dc-144">다음 섹션 hello이이 아키텍처를 구현 하는 hello 코드에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-144">hello following sections discuss hello code that implements this architecture.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="539dc-145">Hello 개발 환경 설정</span><span class="sxs-lookup"><span data-stu-id="539dc-145">Set up hello development environment</span></span>
<span data-ttu-id="539dc-146">Azure 응용 프로그램 개발을 시작 하려면 먼저 hello 도구 가져오고 개발 환경을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-146">Before you can begin developing Azure applications, get hello tools and set up your development environment.</span></span>

1. <span data-ttu-id="539dc-147">Hello SDK에서에서 hello Azure SDK for.NET 설치 [다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-147">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="539dc-148">Hello에 **.NET** 열 hello 버전 [Visual Studio](http://www.visualstudio.com) 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-148">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="539dc-149">이 자습서 사용 하 여 Visual Studio 2015에서에서 hello 실행 하지만 Visual Studio 2017를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-149">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="539dc-150">Toorun 라는 메시지가 표시 하거나 저장 hello 설치 관리자를 클릭 **실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-150">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="539dc-151">Hello에 **웹 플랫폼 설치 관리자**, 클릭 **설치** hello 설치를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-151">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="539dc-152">Hello 설치가 완료 되 면 할 모든 필요한 toostart toodevelop hello 앱.</span><span class="sxs-lookup"><span data-stu-id="539dc-152">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="539dc-153">hello SDK는 Visual Studio에서 Azure 응용 프로그램을 쉽게 개발할 수 있는 도구를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-153">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="539dc-154">네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="539dc-154">Create a namespace</span></span>
<span data-ttu-id="539dc-155">다음 단계 hello toocreate 서비스 네임 스페이스 이며 공유 액세스 서명 (SAS) 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-155">hello next step is toocreate a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="539dc-156">네임스페이스는 서비스 버스를 통해 노출되는 각 응용 프로그램에 대한 응용 프로그램 경계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="539dc-157">네임 스페이스를 만들 때 SAS 키 hello 시스템에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-157">A SAS key is generated by hello system when a namespace is created.</span></span> <span data-ttu-id="539dc-158">네임 스페이스와 SAS 키 조합 hello 서비스 버스 tooauthenticate 액세스 tooan 응용 프로그램에 대 한 hello 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-158">hello combination of namespace and SAS key provides hello credentials for Service Bus tooauthenticate access tooan application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="539dc-159">웹 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="539dc-159">Create a web role</span></span>
<span data-ttu-id="539dc-160">이 섹션에서는 응용 프로그램의 프런트 엔드 hello 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-160">In this section, you build hello front end of your application.</span></span> <span data-ttu-id="539dc-161">먼저, 응용 프로그램을 표시 하는 hello 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-161">First, you create hello pages that your application displays.</span></span>
<span data-ttu-id="539dc-162">그 후 항목 tooa 서비스 버스 큐를 전송 하 고 hello 큐에 대 한 상태 정보를 표시 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-162">After that, add code that submits items tooa Service Bus queue and displays status information about hello queue.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="539dc-163">Hello 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="539dc-163">Create hello project</span></span>
1. <span data-ttu-id="539dc-164">Visual Studio를 시작 관리자 권한을 사용 하 여,: 마우스 오른쪽 단추 클릭 hello **Visual Studio** 프로그램 아이콘을 클릭 하 고 **관리자 권한으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-164">Using administrator privileges, start Visual Studio: right-click hello **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="539dc-165">이 문서의 뒷부분에 설명 된 hello Azure 계산 에뮬레이터는 Visual Studio를 관리자 권한으로 시작할 수 없다는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-165">hello Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="539dc-166">Hello에 Visual Studio에서 **파일** 메뉴를 클릭 **새로**, 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-166">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="539dc-167">**설치된 템플릿**의 **Visual C#**에서 **클라우드**를 클릭한 다음 **Azure Cloud Service**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="539dc-168">이름 hello 프로젝트 **MultiTierApp**합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-168">Name hello project **MultiTierApp**.</span></span> <span data-ttu-id="539dc-169">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="539dc-170">**.NET Framework 4.5** 역할에서 **ASP.NET 웹 역할**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="539dc-171">위로 마우스를 가져가고 **WebRole1** 아래 **Azure 클라우드 서비스 솔루션**hello 연필 아이콘을 클릭 하 고 너무 hello 웹 역할의 이름을 바꿀**FrontendWebRole**합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click hello pencil icon, and rename hello web role too**FrontendWebRole**.</span></span> <span data-ttu-id="539dc-172">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-172">Then click **OK**.</span></span> <span data-ttu-id="539dc-173">"FrontEnd"가 아니라 소문자 "e"를 사용하여 "Frontend"를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="539dc-174">Hello에서 **새 ASP.NET 프로젝트** 대화 상자의 hello **´ ï ´** 목록에서 클릭 **MVC**합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-174">From hello **New ASP.NET Project** dialog box, in hello **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="539dc-175">Hello에 여전히 **새 ASP.NET 프로젝트** 대화 상자를 클릭 hello **인증 변경** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-175">Still in hello **New ASP.NET Project** dialog box, click hello **Change Authentication** button.</span></span> <span data-ttu-id="539dc-176">Hello에 **인증 변경** 대화 상자를 클릭 **인증 안 함**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-176">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="539dc-177">이 자습서의 경우 사용자 로그인이 필요하지 않은 앱을 배포하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="539dc-178">Hello에 다시 **새 ASP.NET 프로젝트** 대화 상자를 클릭 **확인** toocreate hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="539dc-178">Back in hello **New ASP.NET Project** dialog box, click **OK** toocreate hello project.</span></span>
8. <span data-ttu-id="539dc-179">**솔루션 탐색기**, hello에 **FrontendWebRole** 프로젝트를 마우스 오른쪽 단추로 클릭 **참조**, 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-179">In **Solution Explorer**, in hello **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="539dc-180">Hello 클릭 **찾아보기** tab, 이후 검색할 `Microsoft Azure Service Bus`합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-180">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="539dc-181">선택 hello **WindowsAzure.ServiceBus** 클릭, 패키지 **설치**, hello 사용 약관을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-181">Select hello **WindowsAzure.ServiceBus** package, click **Install**, and accept hello terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="539dc-182">이제 클라이언트 어셈블리를 참조 하 고 몇 가지 새 코드 파일이 추가 되었습니다. 해당 hello 필요한 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-182">Note that hello required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="539dc-183">**솔루션 탐색기**에서 **모델**을 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 다음 **클래스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="539dc-184">Hello에 **이름** 상자 hello 이름을 입력 합니다 **OnlineOrder.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-184">In hello **Name** box, type hello name **OnlineOrder.cs**.</span></span> <span data-ttu-id="539dc-185">그런 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-185">Then click **Add**.</span></span>

### <a name="write-hello-code-for-your-web-role"></a><span data-ttu-id="539dc-186">웹 역할에 대 한 hello 코드 작성</span><span class="sxs-lookup"><span data-stu-id="539dc-186">Write hello code for your web role</span></span>
<span data-ttu-id="539dc-187">이 섹션에서는 hello 응용 프로그램이 표시 하는 다양 한 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-187">In this section, you create hello various pages that your application displays.</span></span>

1. <span data-ttu-id="539dc-188">Visual Studio에서 hello OnlineOrder.cs 파일에서 기존 네임 스페이스 정을 코드 다음 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-188">In hello OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with hello following code:</span></span>
   
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
2. <span data-ttu-id="539dc-189">**솔루션 탐색기**에서 **Controllers\HomeController.cs**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="539dc-190">Hello 다음 추가 **를 사용 하 여** hello hello 맨 문 파일 서비스 버스와 방금 만든 모델에 대 한 tooinclude hello 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-190">Add hello following **using** statements at hello top of hello file tooinclude hello namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="539dc-191">또한 Visual Studio에서 hello HomeController.cs 파일에서 기존 네임 스페이스 정의 코드 다음 hello로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-191">Also in hello HomeController.cs file in Visual Studio, replace the existing namespace definition with hello following code.</span></span> <span data-ttu-id="539dc-192">이 코드는 hello 제출 항목 toohello 큐를 처리 하기 위한 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-192">This code contains methods for handling hello submission of items toohello queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
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
4. <span data-ttu-id="539dc-193">Hello에서 **빌드** 메뉴를 클릭 하 여 **솔루션 빌드** tootest hello 정확도 지금까지 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-193">From hello **Build** menu, click **Build Solution** tootest hello accuracy of your work so far.</span></span>
5. <span data-ttu-id="539dc-194">이제 hello에 대 한 hello 보기를 만들 `Submit()` 앞에서 만든 메서드.</span><span class="sxs-lookup"><span data-stu-id="539dc-194">Now, create hello view for hello `Submit()` method you created earlier.</span></span> <span data-ttu-id="539dc-195">Hello 내에서 마우스 오른쪽 단추로 클릭 `Submit()` 메서드 (hello 오버 로드 `Submit()` 매개 변수를 사용 하는)을 선택한 후 **뷰 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-195">Right-click within hello `Submit()` method (hello overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="539dc-196">Hello 보기를 만드는 방법에 대 한 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-196">A dialog box appears for creating hello view.</span></span> <span data-ttu-id="539dc-197">Hello에 **템플릿** 목록에서 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-197">In hello **Template** list, choose **Create**.</span></span> <span data-ttu-id="539dc-198">Hello에 **모델 클래스** 목록에서 클릭 hello **OnlineOrder** 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-198">In hello **Model class** list, click hello **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="539dc-199">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-199">Click **Add**.</span></span>
8. <span data-ttu-id="539dc-200">이제 변경 hello 응용 프로그램의 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-200">Now, change hello displayed name of your application.</span></span> <span data-ttu-id="539dc-201">**솔루션 탐색기**를 두 번 클릭은 **Views\Shared\\_Layout.cshtml** tooopen 파일 hello Visual Studio 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="539dc-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="539dc-202">**내 ASP.NET 응용 프로그램**과 일치하는 모든 항목을 **LITWARE 제품**으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="539dc-203">Hello 제거 **홈**, **에 대 한**, 및 **연락처** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-203">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="539dc-204">Hello 강조 표시 된 코드를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-204">Delete hello highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="539dc-205">Hello 제출 페이지 tooinclude hello 큐에 대 한 일부 정보를 마지막으로 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-205">Finally, modify hello submission page tooinclude some information about hello queue.</span></span> <span data-ttu-id="539dc-206">**솔루션 탐색기**를 두 번 클릭은 **Views\Home\Submit.cshtml** tooopen 파일 hello Visual Studio 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="539dc-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="539dc-207">다음 줄을 다음 hello 추가 `<h2>Submit</h2>`합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-207">Add hello following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="539dc-208">지금은 hello `ViewBag.MessageCount` 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-208">For now, hello `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="539dc-209">나중에 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="539dc-210">이제 UI를 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-210">You now have implemented your UI.</span></span> <span data-ttu-id="539dc-211">누르면 **F5** toorun 응용 프로그램이 예상 대로 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-211">You can press **F5** toorun your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a><span data-ttu-id="539dc-212">항목 tooa 서비스 버스 큐를 전송 하기 위한 hello 코드 작성</span><span class="sxs-lookup"><span data-stu-id="539dc-212">Write hello code for submitting items tooa Service Bus queue</span></span>
<span data-ttu-id="539dc-213">이제 항목 tooa 큐 전송에 대 한 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-213">Now, add code for submitting items tooa queue.</span></span> <span data-ttu-id="539dc-214">먼저 서비스 버스 큐 연결 정보를 포함하는 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="539dc-215">그런 다음 Global.aspx.cs에서 연결을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="539dc-216">HomeController.cs tooactually 전송 항목 tooa 서비스 버스 큐의 앞부분에서 만든 hello 제출 코드를 마지막으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-216">Finally, update hello submission code you created earlier in HomeController.cs tooactually submit items tooa Service Bus queue.</span></span>

1. <span data-ttu-id="539dc-217">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **FrontendWebRole** (하지 hello 역할, hello 프로젝트를 마우스 오른쪽 단추 클릭).</span><span class="sxs-lookup"><span data-stu-id="539dc-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click hello project, not hello role).</span></span> <span data-ttu-id="539dc-218">**추가**를 클릭한 후 **클래스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="539dc-219">Hello 클래스 이름을 **QueueConnector.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-219">Name hello class **QueueConnector.cs**.</span></span> <span data-ttu-id="539dc-220">클릭 **추가** toocreate hello 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-220">Click **Add** toocreate hello class.</span></span>
3. <span data-ttu-id="539dc-221">이제 hello 연결 정보를 캡슐화 하 고 hello 연결 tooa 서비스 버스 큐를 초기화 하는 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-221">Now, add code that encapsulates hello connection information and initializes hello connection tooa Service Bus queue.</span></span> <span data-ttu-id="539dc-222">코드를 다음 hello hello QueueConnector.cs의 전체 내용을 바꾸고 값을 입력 `your Service Bus namespace` (네임 스페이스 이름) 및 `yourKey`, 하는 hello **기본 키** hello Azure에서에서 이전에 가져온 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-222">Replace hello entire contents of QueueConnector.cs with hello following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is hello **primary key** you previously obtained from hello Azure portal.</span></span>
   
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
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="539dc-223">이제 **Initialize** 메서드가 호출되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="539dc-224">**솔루션 탐색기**에서 **Global.asax\Global.asax.cs**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="539dc-225">Hello 다음 hello의 hello 끝에 코드 줄을 추가 **Application_Start** 메서드.</span><span class="sxs-lookup"><span data-stu-id="539dc-225">Add hello following line of code at hello end of hello **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="539dc-226">마지막으로, 항목 toohello 큐를 제출 하려면 앞에서 만든 hello 웹 코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-226">Finally, update hello web code you created earlier, to submit items toohello queue.</span></span> <span data-ttu-id="539dc-227">**솔루션 탐색기**에서 **Controllers\HomeController.cs**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="539dc-228">업데이트 hello `Submit()` 메서드 (hello 오버 로드에 매개 변수가 없으면) 다음과 같이 tooget hello 메시지 수 hello 큐에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-228">Update hello `Submit()` method (hello overload that takes no parameters) as follows tooget hello message count for hello queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="539dc-229">업데이트 hello `Submit(OnlineOrder order)` 메서드 (hello 오버 로드 매개 변수를 사용 하는) 다음과 같이 toosubmit 주문 정보 toohello 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-229">Update hello `Submit(OnlineOrder order)` method (hello overload that takes one parameter) as follows toosubmit order information toohello queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="539dc-230">이제 hello 응용 프로그램을 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-230">You can now run hello application again.</span></span> <span data-ttu-id="539dc-231">주문 제출 때마다 hello 메시지 수가 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-231">Each time you submit an order, hello message count increases.</span></span>
   
   ![][18]

## <a name="create-hello-worker-role"></a><span data-ttu-id="539dc-232">Hello 작업자 역할 만들기</span><span class="sxs-lookup"><span data-stu-id="539dc-232">Create hello worker role</span></span>
<span data-ttu-id="539dc-233">이제 hello 주문 제출을 처리 하는 hello 작업자 역할을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-233">You will now create hello worker role that processes hello order submissions.</span></span> <span data-ttu-id="539dc-234">이 예에서는 hello **서비스 버스 큐가 있는 작업자 역할** Visual Studio 프로젝트 템플릿이 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-234">This example uses hello **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="539dc-235">이미 hello 포털에서 필요한 hello 자격 증명을 획득 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-235">You already obtained hello required credentials from hello portal.</span></span>

1. <span data-ttu-id="539dc-236">Visual Studio tooyour Azure 계정을 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-236">Make sure you have connected Visual Studio tooyour Azure account.</span></span>
2. <span data-ttu-id="539dc-237">Visual Studio에서의 **솔루션 탐색기** 마우스 오른쪽 단추로 클릭는 **역할** hello 아래에 폴더 **MultiTierApp** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="539dc-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under hello **MultiTierApp** project.</span></span>
3. <span data-ttu-id="539dc-238">**추가**를 클릭한 후 **새 작업자 역할 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="539dc-239">hello **새 역할 프로젝트 추가** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-239">hello **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="539dc-240">Hello에 **새 역할 프로젝트 추가** 대화 상자를 클릭 **서비스 버스 큐가 있는 작업자 역할**합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-240">In hello **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="539dc-241">Hello에 **이름** 상자, 이름 hello 프로젝트 **OrderProcessingRole**합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-241">In hello **Name** box, name hello project **OrderProcessingRole**.</span></span> <span data-ttu-id="539dc-242">그런 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-242">Then click **Add**.</span></span>
6. <span data-ttu-id="539dc-243">Hello "서비스 버스 네임 스페이스 만들기" 섹션 toohello 클립보드의 9 단계에서 가져온 hello 연결 문자열을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-243">Copy hello connection string that you obtained in step 9 of hello "Create a Service Bus namespace" section toohello clipboard.</span></span>
7. <span data-ttu-id="539dc-244">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **OrderProcessingRole** 5 단계에서 만든 (오른쪽 단추로 클릭 하 고 있는지 확인 **OrderProcessingRole** 아래**역할**, 하지 클래스 hello 및).</span><span class="sxs-lookup"><span data-stu-id="539dc-244">In **Solution Explorer**, right-click hello **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not hello class).</span></span> <span data-ttu-id="539dc-245">그런 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="539dc-246">Hello에 **설정** hello 탭 **속성** 대화 상자, hello 내부를 클릭 **값** 에 대 한 **Microsoft.ServiceBus.ConnectionString**, 6 단계에서 복사한 hello 끝점 값을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-246">On hello **Settings** tab of hello **Properties** dialog box, click inside hello **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste hello endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="539dc-247">만들기는 **OnlineOrder** hello 큐에서 처리 하는 동안 toorepresent hello orders 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-247">Create an **OnlineOrder** class toorepresent hello orders as you process them from hello queue.</span></span> <span data-ttu-id="539dc-248">이미 만든 클래스를 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="539dc-249">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **OrderProcessingRole** 클래스 (하지 hello 역할, hello 클래스 아이콘을 마우스 오른쪽 단추 클릭).</span><span class="sxs-lookup"><span data-stu-id="539dc-249">In **Solution Explorer**, right-click hello **OrderProcessingRole** class (right-click hello class icon, not hello role).</span></span> <span data-ttu-id="539dc-250">**추가**를 클릭한 후 **기존 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="539dc-251">Toohello 하위 폴더에 대 한 찾아보기 **FrontendWebRole\Models**를 두 번 클릭 하 고 **OnlineOrder.cs** tooadd 것 toothis 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="539dc-251">Browse toohello subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** tooadd it toothis project.</span></span>
11. <span data-ttu-id="539dc-252">**WorkerRole.cs**, hello의 hello 값 변경 **QueueName** 변수 `"ProcessingQueue"` 너무`"OrdersQueue"` hello 코드 다음에 표시 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-252">In **WorkerRole.cs**, change hello value of hello **QueueName** variable from `"ProcessingQueue"` too`"OrdersQueue"` as shown in hello following code.</span></span>
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="539dc-253">Hello 다음 추가 문을 사용 하 여 hello hello WorkerRole.cs 파일 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-253">Add hello following using statement at hello top of hello WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="539dc-254">Hello에 `Run()` 함수 hello 내부 `OnMessage()` 호출, hello hello 내용 바꾸기 `try` 코드 다음 hello로 절.</span><span class="sxs-lookup"><span data-stu-id="539dc-254">In hello `Run()` function, inside hello `OnMessage()` call, replace hello contents of hello `try` clause with hello following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="539dc-255">Hello 응용 프로그램을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-255">You have completed hello application.</span></span> <span data-ttu-id="539dc-256">솔루션 탐색기에서 hello MultiTierApp 프로젝트를 마우스 오른쪽 단추로 클릭 하 여 hello 전체 응용 프로그램을 테스트할 수 있습니다 선택 **시작 프로젝트로 설정**, 한 다음 F5 키를 눌러 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-256">You can test hello full application by right-clicking hello MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="539dc-257">메시지 수는 증가 하지 않습니다 hello 작업자 역할 hello 큐에서 항목을 처리 하 고 완료 된 것으로 표시 하기 때문에 유의 합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-257">Note that the message count does not increment, because hello worker role processes items from hello queue and marks them as complete.</span></span> <span data-ttu-id="539dc-258">Hello Azure 계산 에뮬레이터 UI를 확인 하 여 작업자 역할의 hello 추적 출력을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-258">You can see hello trace output of your worker role by viewing hello Azure Compute Emulator UI.</span></span> <span data-ttu-id="539dc-259">작업 표시줄의 알림 영역 hello에에서 hello 에뮬레이터 아이콘을 마우스 오른쪽 단추로 클릭 하 고 선택 하 여이 작업을 수행할 수 **계산 에뮬레이터 UI 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="539dc-259">You can do this by right-clicking hello emulator icon in hello notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="539dc-260">다음 단계</span><span class="sxs-lookup"><span data-stu-id="539dc-260">Next steps</span></span>
<span data-ttu-id="539dc-261">서비스 버스에 대 한 자세한 toolearn hello 다음 리소스 참조:</span><span class="sxs-lookup"><span data-stu-id="539dc-261">toolearn more about Service Bus, see hello following resources:</span></span>  

* <span data-ttu-id="539dc-262">[Azure Service Bus 설명서][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="539dc-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="539dc-263">[Service Bus 서비스 페이지][sbacom]</span><span class="sxs-lookup"><span data-stu-id="539dc-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="539dc-264">[어떻게 tooUse 서비스 버스 큐][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="539dc-264">[How tooUse Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="539dc-265">다중 계층 시나리오에 대해 자세히 toolearn 참조:</span><span class="sxs-lookup"><span data-stu-id="539dc-265">toolearn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="539dc-266">[저장소 테이블, 큐 및 Blob을 사용하는 .NET 다중 계층 응용 프로그램][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="539dc-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

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
