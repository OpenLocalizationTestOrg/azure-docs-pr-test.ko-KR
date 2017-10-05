---
title: "Azure Cloud Services 앱을 마이크로 서비스로 변환 | Microsoft Docs"
description: "이 가이드에서는 클라우드 서비스에서 서비스 패브릭으로 마이그레이션할 수 있도록 클라우드 서비스 웹과 작업자 역할 및 서비스 패브릭 상태 비저장 서비스를 비교합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4ab1f83e88b262b1752300b2786340d9abca8154
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="guide-to-converting-web-and-worker-roles-to-service-fabric-stateless-services"></a><span data-ttu-id="e8df7-103">웹 및 작업자 역할을 서비스 패브릭 상태 비저장 서비스로 변환하기 위한 가이드</span><span class="sxs-lookup"><span data-stu-id="e8df7-103">Guide to converting Web and Worker Roles to Service Fabric stateless services</span></span>
<span data-ttu-id="e8df7-104">이 문서에서는 클라우드 서비스 웹 및 작업자 역할을 서비스 패브릭 상태 비저장 서비스로 마이그레이션하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-104">This article describes how to migrate your Cloud Services Web and Worker Roles to Service Fabric stateless services.</span></span> <span data-ttu-id="e8df7-105">클라우드 서비스에서 전반적인 아키텍처를 대략적으로 동일하게 유지하는 응용 프로그램에 대한 서비스 패브릭으로의 가장 간단한 마이그레이션 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-105">This is the simplest migration path from Cloud Services to Service Fabric for applications whose overall architecture is going to stay roughly the same.</span></span>

## <a name="cloud-service-project-to-service-fabric-application-project"></a><span data-ttu-id="e8df7-106">클라우드 서비스 프로젝트에서 서비스 패브릭 응용 프로그램 프로젝트</span><span class="sxs-lookup"><span data-stu-id="e8df7-106">Cloud Service project to Service Fabric application project</span></span>
 <span data-ttu-id="e8df7-107">클라우드 서비스 프로젝트 및 서비스 패브릭 응용 프로그램 프로젝트는 유사한 구조를 가지며 모두 응용 프로그램에 대한 배포 단위를 나타냅니다. 즉, 각각은 응용 프로그램을 실행하도록 배포되는 완전한 패키지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent the deployment unit for your application - that is, they each define the complete package that is deployed to run your application.</span></span> <span data-ttu-id="e8df7-108">클라우드 서비스 프로젝트는 하나 이상의 웹 또는 작업자 역할을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="e8df7-109">유사하게 서비스 패브릭 응용 프로그램 프로젝트에는 하나 이상의 서비스가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="e8df7-110">클라우드 서비스 프로젝트는 응용 프로그램 배포를 VM 배포와 결합하므로 VM 구성 설정을 포함하고 반면에 서비스 패브릭 응용 프로그램 프로젝트는 서비스 패브릭 클러스터의 기존 VM 집합에 배포되는 응용 프로그램을 정의한다는 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-110">The difference is that the Cloud Service project couples the application deployment with a VM deployment and thus contains VM configuration settings in it, whereas the Service Fabric Application project only defines an application that will be deployed to a set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="e8df7-111">Service Fabric 클러스터 자체는 Resource Manager 템플릿 또는 Azure Portal을 통해 한 번만 배포되고 여러 Service Fabric 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-111">The Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through the Azure portal, and multiple Service Fabric applications can be deployed to it.</span></span>

![서비스 패브릭 및 클라우드 서비스 프로젝트 비교][3]

## <a name="worker-role-to-stateless-service"></a><span data-ttu-id="e8df7-113">작업자 역할에서 상태 비저장 서비스</span><span class="sxs-lookup"><span data-stu-id="e8df7-113">Worker Role to stateless service</span></span>
<span data-ttu-id="e8df7-114">개념적으로 작업자 역할은 모든 작업 인스턴스는 동일하고 언제든지 인스턴스에 요청을 라우팅할 수 있음을 의미하는 상태 비저장 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of the workload is identical and requests can be routed to any instance at any time.</span></span> <span data-ttu-id="e8df7-115">각 인스턴스는 이전 요청을 기억하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-115">Each instance is not expected to remember the previous request.</span></span> <span data-ttu-id="e8df7-116">작업이 작동 중인 상태는 Azure 테이블 저장소 또는 Azure Document DB와 같은 외부 상태 저장소에서 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-116">State that the workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="e8df7-117">서비스 패브릭에서 이러한 유형의 작업은 상태 비저장 서비스에 의해 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="e8df7-118">작업자 역할을 서비스 패브릭으로 마이그레이션하는 가장 간단한 방법은 작업자 역할 코드를 상태 비저장 서비스로 변환하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-118">The simplest approach to migrating a Worker Role to Service Fabric can be done by converting Worker Role code to a Stateless Service.</span></span>

![작업자 역할에서 상태 비저장 서비스][4]

## <a name="web-role-to-stateless-service"></a><span data-ttu-id="e8df7-120">웹 역할에서 상태 비저장 서비스</span><span class="sxs-lookup"><span data-stu-id="e8df7-120">Web Role to stateless service</span></span>
<span data-ttu-id="e8df7-121">작업자 역할과 마찬가지로 웹 역할도 상태 비저장 작업을 나타내므로 개념적으로 서비스 패브릭 상태 비저장 서비스에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-121">Similar to Worker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped to a Service Fabric stateless service.</span></span> <span data-ttu-id="e8df7-122">그러나 웹 역할과 달리 서비스 패브릭은 IIS를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="e8df7-123">웹 역할의 웹 응용 프로그램을 상태 비저장 서비스에 마이그레이션하려면 자체 호스팅될 수 있고 ASP.NET Core 1과 같은 IIS 또는 System.Web에 의존하지 않는 웹 프레임워크로 이동이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-123">To migrate a web application from a Web Role to a stateless service requires first moving to a web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="e8df7-124">**응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="e8df7-124">**Application**</span></span> | <span data-ttu-id="e8df7-125">**지원됨**</span><span class="sxs-lookup"><span data-stu-id="e8df7-125">**Supported**</span></span> | <span data-ttu-id="e8df7-126">**마이그레이션 경로**</span><span class="sxs-lookup"><span data-stu-id="e8df7-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8df7-127">ASP.NET 웹 양식</span><span class="sxs-lookup"><span data-stu-id="e8df7-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="e8df7-128">아니요</span><span class="sxs-lookup"><span data-stu-id="e8df7-128">No</span></span> |<span data-ttu-id="e8df7-129">ASP.NET Core 1 MVC로 변환</span><span class="sxs-lookup"><span data-stu-id="e8df7-129">Convert to ASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="e8df7-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="e8df7-130">ASP.NET MVC</span></span> |<span data-ttu-id="e8df7-131">마이그레이션 사용</span><span class="sxs-lookup"><span data-stu-id="e8df7-131">With Migration</span></span> |<span data-ttu-id="e8df7-132">ASP.NET Core 1 MVC로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="e8df7-132">Upgrade to ASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="e8df7-133">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="e8df7-133">ASP.NET Web API</span></span> |<span data-ttu-id="e8df7-134">마이그레이션 사용</span><span class="sxs-lookup"><span data-stu-id="e8df7-134">With Migration</span></span> |<span data-ttu-id="e8df7-135">자체 호스팅된 서버 또는 ASP.NET Core 1 사용</span><span class="sxs-lookup"><span data-stu-id="e8df7-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="e8df7-136">ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="e8df7-136">ASP.NET Core 1</span></span> |<span data-ttu-id="e8df7-137">예</span><span class="sxs-lookup"><span data-stu-id="e8df7-137">Yes</span></span> |<span data-ttu-id="e8df7-138">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8df7-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="e8df7-139">진입점 API 및 수명 주기</span><span class="sxs-lookup"><span data-stu-id="e8df7-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="e8df7-140">작업자 역할 및 서비스 패브릭 서비스 API는 비슷한 진입점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="e8df7-141">**진입점**</span><span class="sxs-lookup"><span data-stu-id="e8df7-141">**Entry Point**</span></span> | <span data-ttu-id="e8df7-142">**작업자 역할**</span><span class="sxs-lookup"><span data-stu-id="e8df7-142">**Worker Role**</span></span> | <span data-ttu-id="e8df7-143">**서비스 패브릭 서비스**</span><span class="sxs-lookup"><span data-stu-id="e8df7-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8df7-144">처리 중</span><span class="sxs-lookup"><span data-stu-id="e8df7-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="e8df7-145">VM 시작</span><span class="sxs-lookup"><span data-stu-id="e8df7-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="e8df7-146">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8df7-146">N/A</span></span> |
| <span data-ttu-id="e8df7-147">VM 중지</span><span class="sxs-lookup"><span data-stu-id="e8df7-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="e8df7-148">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8df7-148">N/A</span></span> |
| <span data-ttu-id="e8df7-149">클라이언트 요청에 대한 수신기 열기</span><span class="sxs-lookup"><span data-stu-id="e8df7-149">Open listener for client requests</span></span> |<span data-ttu-id="e8df7-150">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8df7-150">N/A</span></span> |<ul><li> <span data-ttu-id="e8df7-151">상태 비저장인 경우 `CreateServiceInstanceListener()`</span><span class="sxs-lookup"><span data-stu-id="e8df7-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="e8df7-152">상태 저장인 경우 `CreateServiceReplicaListener()`</span><span class="sxs-lookup"><span data-stu-id="e8df7-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="e8df7-153">작업자 역할</span><span class="sxs-lookup"><span data-stu-id="e8df7-153">Worker Role</span></span>
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="e8df7-154">서비스 패브릭 상태 비저장 서비스</span><span class="sxs-lookup"><span data-stu-id="e8df7-154">Service Fabric Stateless Service</span></span>
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

<span data-ttu-id="e8df7-155">둘 모두는 처리를 시작하는 기본 "실행" 재정의를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-155">Both have a primary "Run" override in which to begin processing.</span></span> <span data-ttu-id="e8df7-156">Service Fabric 서비스는 `Run`, `Start` 및 `Stop`을 단일 액세스 지점, `RunAsync`로 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="e8df7-157">서비스는 `RunAsync`가 시작될 때 작동을 시작해야 하고 `RunAsync` 메서드의 CancellationToken이 신호될 때 작동을 중지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-157">Your service should begin working when `RunAsync` starts, and should stop working when the `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="e8df7-158">작업자 역할 및 서비스 패브릭 서비스의 수명 주기 및 수명 간에는 몇 가지 주요 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-158">There are several key differences between the lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="e8df7-159">**수명 주기:** 가장 큰 차이점은 작업자 역할은 VM이므로 해당 수명 주기는 VM의 시작 및 중지 시기에 대한 이벤트를 포함하는 VM에 연결되어 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-159">**Lifecycle:** The biggest difference is that a Worker Role is a VM and so its lifecycle is tied to the VM, which includes events for when the VM starts and stops.</span></span> <span data-ttu-id="e8df7-160">서비스 패브릭 서비스는 VM 수명 주기와 별개의 수명 주기를 가지므로 관련되지 않으므로 호스트 VM 또는 컴퓨터의 시작 및 중지 시기에 대한 이벤트를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-160">A Service Fabric service has a lifecycle that is separate from the VM lifecycle, so it does not include events for when the host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="e8df7-161">**수명:** `Run` 메서드가 종료되는 경우 작업자 역할 인스턴스는 재활용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-161">**Lifetime:** A Worker Role instance will recycle if the `Run` method exits.</span></span> <span data-ttu-id="e8df7-162">하지만 서비스 패브릭 서비스의 `RunAsync` 메서드는 완료될 때까지 실행할 수 있고 서비스 인스턴스는 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-162">The `RunAsync` method in a Service Fabric service however can run to completion and the service instance will stay up.</span></span> 

<span data-ttu-id="e8df7-163">서비스 패브릭은 클라이언트 요청을 수신 대기하는 서비스에 대한 선택적 통신 설정 진입점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="e8df7-164">RunAsync와 통신 진입점은 서비스 패브릭 서비스에서 선택적 재정의입니다. 서비스는 클라이언트 요청을 수신 대기하거나 처리 루프를 실행하거나 둘 다 수행하도록 선택할 수 있습니다. 클라이언트 요청을 계속해서 수신 대기할 수 있기 때문에 RunAsync 메서드가 서비스 인스턴스를 다시 시작하지 않고 종료하도록 허용되는 것은 이 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-164">Both the RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose to only listen to client requests, or only run a processing loop, or both - which is why the RunAsync method is allowed to exit without restarting the service instance, because it may continue to listen for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="e8df7-165">응용 프로그램 API 및 환경</span><span class="sxs-lookup"><span data-stu-id="e8df7-165">Application API and environment</span></span>
<span data-ttu-id="e8df7-166">클라우드 서비스 환경 API는 현재 VM 인스턴스에 대한 정보 및 기능 뿐만 아니라 다른 VM 역할 인스턴스에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-166">The Cloud Services environment API provides information and functionality for the current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="e8df7-167">서비스 패브릭은 해당 런타임과 관련된 정보 및 서비스가 현재 실행 중인 노드에 대한 일부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-167">Service Fabric provides information related to its runtime and some information about the node a service is currently running on.</span></span> 

| <span data-ttu-id="e8df7-168">**환경 작업**</span><span class="sxs-lookup"><span data-stu-id="e8df7-168">**Environment Task**</span></span> | <span data-ttu-id="e8df7-169">**클라우드 서비스**</span><span class="sxs-lookup"><span data-stu-id="e8df7-169">**Cloud Services**</span></span> | <span data-ttu-id="e8df7-170">**서비스 패브릭**</span><span class="sxs-lookup"><span data-stu-id="e8df7-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8df7-171">구성 설정 및 변경 알림</span><span class="sxs-lookup"><span data-stu-id="e8df7-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="e8df7-172">로컬 저장소</span><span class="sxs-lookup"><span data-stu-id="e8df7-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="e8df7-173">끝점 정보</span><span class="sxs-lookup"><span data-stu-id="e8df7-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="e8df7-174">현재 인스턴스: `RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="e8df7-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="e8df7-175">다른 역할 및 인스턴스: `RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="e8df7-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="e8df7-176">현재 노드 주소의 경우 `NodeContext`</span><span class="sxs-lookup"><span data-stu-id="e8df7-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="e8df7-177">서비스 끝점 검색의 경우 `FabricClient` 및 `ServicePartitionResolver`</span><span class="sxs-lookup"><span data-stu-id="e8df7-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="e8df7-178">환경 에뮬레이션</span><span class="sxs-lookup"><span data-stu-id="e8df7-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="e8df7-179">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8df7-179">N/A</span></span> |
| <span data-ttu-id="e8df7-180">동시 변경 이벤트</span><span class="sxs-lookup"><span data-stu-id="e8df7-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="e8df7-181">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e8df7-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="e8df7-182">구성 설정</span><span class="sxs-lookup"><span data-stu-id="e8df7-182">Configuration settings</span></span>
<span data-ttu-id="e8df7-183">클라우드 서비스의 구성 설정은 VM 역할에 대해 설정되고 해당 VM 역할의 모든 인스턴스에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-183">Configuration settings in Cloud Services are set for a VM role and apply to all instances of that VM role.</span></span> <span data-ttu-id="e8df7-184">이러한 설정은 ServiceConfiguration.*.cscfg 파일에서 설정된 키-값 쌍이며 RoleEnvironment를 통해 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="e8df7-185">서비스 패브릭에서 VM은 여러 서비스 및 응용 프로그램을 호스팅할 수 있으므로 설정은 VM이 아닌 각 서비스 및 각 응용 프로그램에 개별적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-185">In Service Fabric, settings apply individually to each service and to each application, rather than to a VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="e8df7-186">서비스는 세 가지 패키지로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="e8df7-187">**코드:** 서비스를 실행하는 데 필요한 서비스 실행 파일, 이진 파일, DLL 및 다른 모든 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-187">**Code:** contains the service executables, binaries, DLLs, and any other files a service needs to run.</span></span>
* <span data-ttu-id="e8df7-188">**Config:** 서비스에 대한 모든 구성 파일 및 설정.</span><span class="sxs-lookup"><span data-stu-id="e8df7-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="e8df7-189">**데이터:** 서비스와 관련된 정적 데이터 파일.</span><span class="sxs-lookup"><span data-stu-id="e8df7-189">**Data:** static data files associated with the service.</span></span>

<span data-ttu-id="e8df7-190">이러한 각 패키지는 서비스를 독립적으로 버전 지정 및 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="e8df7-191">클라우드 서비스와 마찬가지로 config 패키지는 API를 통해 프로그래밍 방식으로 액세스할 수 있으며 이벤트는 config 패키지 변경의 서비스를 알리기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-191">Similar to Cloud Services, a config package can be accessed programmatically through an API and events are available to notify the service of a config package change.</span></span> <span data-ttu-id="e8df7-192">App.config 파일의 앱 설정 섹션과 유사한 키-값 구성 및 프로그래밍 방식 액세스에 Settings.xml 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-192">A Settings.xml file can be used for key-value configuration and programmatic access similar to the app settings section of an App.config file.</span></span> <span data-ttu-id="e8df7-193">그러나 클라우드 서비스와는 달리 서비스 패브릭 config 패키지는 XML, JSON, YAML 또는 사용자 지정 이진 형식이든 모든 형식의 구성 파일을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="e8df7-194">구성 액세스</span><span class="sxs-lookup"><span data-stu-id="e8df7-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="e8df7-195">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="e8df7-195">Cloud Services</span></span>
<span data-ttu-id="e8df7-196">ServiceConfiguration.*.cscfg의 구성 설정은 `RoleEnvironment`을(를) 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="e8df7-197">이러한 설정은 동일한 클라우드 서비스 배포 내에서 모든 역할 인스턴스에 전역적으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-197">These settings are globally available to all role instances in the same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="e8df7-198">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="e8df7-198">Service Fabric</span></span>
<span data-ttu-id="e8df7-199">각 서비스에는 자체 개별 구성 패키지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="e8df7-200">클러스터의 모든 응용 프로그램에서 액세스할 수 있는 전역 구성 설정에 대한 기본 제공 메커니즘이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="e8df7-201">구성 패키지 내에서 서비스 패브릭의 특별한 Settings.xml 구성 파일을 사용할 때 가능한 응용 프로그램 수준에서 응용 프로그램 수준 구성 설정을 가능하도록 하는 Settings.xml의 값을 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at the application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="e8df7-202">구성 설정은 서비스의 `CodePackageActivationContext`을(를) 통한 각 서비스 인스턴스 내의 액세스입니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-202">Configuration settings are accesses within each service instance through the service's `CodePackageActivationContext`.</span></span>

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a><span data-ttu-id="e8df7-203">구성 업데이트 이벤트</span><span class="sxs-lookup"><span data-stu-id="e8df7-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="e8df7-204">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="e8df7-204">Cloud Services</span></span>
<span data-ttu-id="e8df7-205">`RoleEnvironment.Changed` 이벤트는 환경에서 구성 변경과 같은 변경이 발생할 때 모든 역할 인스턴스를 알리는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-205">The `RoleEnvironment.Changed` event is used to notify all role instances when a change occurs in the environment, such as a configuration change.</span></span> <span data-ttu-id="e8df7-206">역할 인스턴스를 재활용하거나 작업자 프로세스를 다시 시작하지 않고 구성 업데이트를 사용하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-206">This is used to consume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get the list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="e8df7-207">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="e8df7-207">Service Fabric</span></span>
<span data-ttu-id="e8df7-208">서비스의 각 세 가지 패키지 유형(코드, 구성 및 데이터)은 패키지를 업데이트, 추가 또는 제거하는 경우 서비스 인스턴스를 알리는 이벤트를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-208">Each of the three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="e8df7-209">서비스는 각 유형의 여러 패키지를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="e8df7-210">예를 들어 서비스에는 각각 개별적으로 버전이 지정되고 업그레이드 가능한 여러 config 패키지가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="e8df7-211">이러한 이벤트는 서비스 인스턴스를 다시 시작하지 않고 서비스 패키지의 변경 내용을 사용하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-211">These events are available to consume changes in service packages without restarting the service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="e8df7-212">시작 작업</span><span class="sxs-lookup"><span data-stu-id="e8df7-212">Startup tasks</span></span>
<span data-ttu-id="e8df7-213">시작 작업은 응용 프로그램이 시작되기 전에 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="e8df7-214">시작 작업은 상승된 권한을 사용하여 설치 스크립트를 실행하는 데 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-214">A startup task is typically used to run setup scripts using elevated privileges.</span></span> <span data-ttu-id="e8df7-215">클라우드 서비스와 서비스 패브릭은 시작 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="e8df7-216">주요 차이점은 클라우드 서비스에서 시작 작업은 역할 인스턴스의 일부이므로 VM에 연결되는 반면 서비스 패브릭에서 시작 작업은 특정 VM에 연결되지 않은 서비스에 연결된다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-216">The main difference is that in Cloud Services, a startup task is tied to a VM because it is part of a role instance, whereas in Service Fabric a startup task is tied to a service, which is not tied to any particular VM.</span></span>

| <span data-ttu-id="e8df7-217">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="e8df7-217">Cloud Services</span></span> | <span data-ttu-id="e8df7-218">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="e8df7-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8df7-219">구성 위치</span><span class="sxs-lookup"><span data-stu-id="e8df7-219">Configuration location</span></span> |<span data-ttu-id="e8df7-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="e8df7-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="e8df7-221">권한</span><span class="sxs-lookup"><span data-stu-id="e8df7-221">Privileges</span></span> |<span data-ttu-id="e8df7-222">"제한된" 또는 "상승된"</span><span class="sxs-lookup"><span data-stu-id="e8df7-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="e8df7-223">시퀀싱</span><span class="sxs-lookup"><span data-stu-id="e8df7-223">Sequencing</span></span> |<span data-ttu-id="e8df7-224">"간단", "백그라운드", "포그라운드"</span><span class="sxs-lookup"><span data-stu-id="e8df7-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="e8df7-225">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="e8df7-225">Cloud Services</span></span>
<span data-ttu-id="e8df7-226">클라우드 서비스에서 시작 진입점은 ServiceDefinition.csdef에서 역할별로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a><span data-ttu-id="e8df7-227">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="e8df7-227">Service Fabric</span></span>
<span data-ttu-id="e8df7-228">서비스 패브릭에서 시작 진입점은 ServiceManifest.xml에서 서비스별로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a><span data-ttu-id="e8df7-229">개발 환경에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="e8df7-229">A note about development environment</span></span>
<span data-ttu-id="e8df7-230">클라우드 서비스와 서비스 패브릭은 프로젝트 템플릿 및 로컬과 Azure 모두로 디버깅, 구성 및 배포에 대한 지원을 사용하여 Visual Studio와 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and to Azure.</span></span> <span data-ttu-id="e8df7-231">클라우드 서비스와 서비스 패브릭은 로컬 개발 런타임 환경도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="e8df7-232">차이점은 클라우드 서비스 개발 런타임은 실행하는 Azure 환경을 에뮬레이션하는 반면 서비스 패브릭은 에뮬레이터를 사용하지 않고 전체 서비스 패브릭 런타임을 사용한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-232">The difference is that while the Cloud Service development runtime emulates the Azure environment on which it runs, Service Fabric does not use an emulator - it uses the complete Service Fabric runtime.</span></span> <span data-ttu-id="e8df7-233">로컬 개발 컴퓨터에서 실행하는 서비스 패브릭 환경은 프로덕션 환경에서 실행하는 동일한 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="e8df7-233">The Service Fabric environment you run on your local development machine is the same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8df7-234">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8df7-234">Next steps</span></span>
<span data-ttu-id="e8df7-235">서비스 패브릭 기능의 전체 집합을 활용하는 방법을 이해하려면 서비스 패브릭 신뢰할 수 있는 서비스 및 클라우드 서비스와 서비스 패브릭 응용 프로그램 아키텍처 간의 기본적인 차이점에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e8df7-235">Read more about Service Fabric Reliable Services and the fundamental differences between Cloud Services and Service Fabric application architecture to understand how to take advantage of the full set of Service Fabric features.</span></span>

* [<span data-ttu-id="e8df7-236">서비스 패브릭 신뢰할 수 있는 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="e8df7-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="e8df7-237">클라우드 서비스와 서비스 패브릭 간의 차이점에 대한 개념 가이드</span><span class="sxs-lookup"><span data-stu-id="e8df7-237">Conceptual guide to the differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
