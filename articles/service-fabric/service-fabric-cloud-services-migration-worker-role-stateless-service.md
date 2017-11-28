---
title: "Azure 클라우드 서비스 앱 toomicroservices aaaConvert | Microsoft Docs"
description: "클라우드 서비스 tooService 패브릭에서에서 작업자 역할 및 서비스 패브릭 상태 비저장 서비스 toohelp 마이그레이션할와이 가이드는 클라우드 서비스 웹을 비교 합니다."
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
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a><span data-ttu-id="11456-103">Tooconverting 웹 및 작업자 역할 tooService 패브릭 상태 비저장 서비스를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-103">Guide tooconverting Web and Worker Roles tooService Fabric stateless services</span></span>
<span data-ttu-id="11456-104">이 문서에서는 설명 방법을 toomigrate 클라우드 서비스 웹 및 작업자 역할 tooService 패브릭 상태 비저장 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="11456-104">This article describes how toomigrate your Cloud Services Web and Worker Roles tooService Fabric stateless services.</span></span> <span data-ttu-id="11456-105">이것은 클라우드 서비스 tooService 패브릭에서에서의 가장 간단한 마이그레이션 경로 hello 응용 프로그램 전체 아키텍처가 될 toostay 대략 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-105">This is hello simplest migration path from Cloud Services tooService Fabric for applications whose overall architecture is going toostay roughly hello same.</span></span>

## <a name="cloud-service-project-tooservice-fabric-application-project"></a><span data-ttu-id="11456-106">클라우드 서비스 프로젝트 tooService 패브릭 응용 프로그램 프로젝트</span><span class="sxs-lookup"><span data-stu-id="11456-106">Cloud Service project tooService Fabric application project</span></span>
 <span data-ttu-id="11456-107">클라우드 서비스 프로젝트는 서비스 패브릭 응용 프로그램 프로젝트는 유사한 구조와 모두 나타내는 hello 배포 단위 응용 프로그램-즉, 구성 파일은 각각 정의할 hello 완료 된 패키지를 배포 된 toorun 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent hello deployment unit for your application - that is, they each define hello complete package that is deployed toorun your application.</span></span> <span data-ttu-id="11456-108">클라우드 서비스 프로젝트는 하나 이상의 웹 또는 작업자 역할을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="11456-109">유사하게 서비스 패브릭 응용 프로그램 프로젝트에는 하나 이상의 서비스가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="11456-110">hello 클래스 간의 차이점은 hello 클라우드 서비스 프로젝트 직접 hello VM 배포와 응용 프로그램 배포, VM 구성 설정이 포함 되어 있으므로 반면 hello 서비스 패브릭 응용 프로그램 프로젝트에만 배포 될 응용 프로그램 정의 서비스 패브릭 클러스터에서 기존 Vm의 tooa 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="11456-110">hello difference is that hello Cloud Service project couples hello application deployment with a VM deployment and thus contains VM configuration settings in it, whereas hello Service Fabric Application project only defines an application that will be deployed tooa set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="11456-111">자체 hello 서비스 패브릭 클러스터 리소스 관리자 템플릿을 통해 또는 hello Azure 포털을 통해 및 여러 서비스 패브릭 응용 프로그램 수 tooit를 배포한 후에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11456-111">hello Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through hello Azure portal, and multiple Service Fabric applications can be deployed tooit.</span></span>

![서비스 패브릭 및 클라우드 서비스 프로젝트 비교][3]

## <a name="worker-role-toostateless-service"></a><span data-ttu-id="11456-113">작업자 역할 toostateless 서비스</span><span class="sxs-lookup"><span data-stu-id="11456-113">Worker Role toostateless service</span></span>
<span data-ttu-id="11456-114">개념적으로 작업자 역할은 hello 작업의 모든 인스턴스는 동일 하 고 요청 언제 든 지 라우트된 tooany 인스턴스가 될 수 있습니다 상태 비저장 워크 로드를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="11456-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of hello workload is identical and requests can be routed tooany instance at any time.</span></span> <span data-ttu-id="11456-115">각 인스턴스가 예상된 tooremember hello에 대 한 이전 요청 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-115">Each instance is not expected tooremember hello previous request.</span></span> <span data-ttu-id="11456-116">Hello 워크 로드의 작동 상태에 외부 상태 저장소와 같은 Azure 테이블 저장소 또는 Azure 문서 DB에서 관리 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-116">State that hello workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="11456-117">서비스 패브릭에서 이러한 유형의 작업은 상태 비저장 서비스에 의해 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="11456-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="11456-118">hello 가장 간단한 방법은 toomigrating 작업자 역할 tooService 패브릭 가능 하 여 작업자 역할 코드 tooa 상태 비저장 서비스를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-118">hello simplest approach toomigrating a Worker Role tooService Fabric can be done by converting Worker Role code tooa Stateless Service.</span></span>

![작업자 역할 tooStateless 서비스][4]

## <a name="web-role-toostateless-service"></a><span data-ttu-id="11456-120">웹 역할 toostateless 서비스</span><span class="sxs-lookup"><span data-stu-id="11456-120">Web Role toostateless service</span></span>
<span data-ttu-id="11456-121">비슷한 tooWorker 역할, 웹 역할도 상태 비저장 작업 나타내며 하므로 개념적으로 너무 수 매핑된 tooa 서비스 패브릭 상태 비저장 서비스 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-121">Similar tooWorker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped tooa Service Fabric stateless service.</span></span> <span data-ttu-id="11456-122">그러나 웹 역할과 달리 서비스 패브릭은 IIS를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="11456-123">toomigrate tooa 상태 비저장 서비스 웹 역할에서에서 웹 응용 프로그램 필요 최초의 이동 tooa 웹 프레임 워크를 자체 호스트 될 수 있습니다 및 IIS 또는 ASP.NET Core 1과 같은 System.Web에 종속 되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-123">toomigrate a web application from a Web Role tooa stateless service requires first moving tooa web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="11456-124">**응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="11456-124">**Application**</span></span> | <span data-ttu-id="11456-125">**지원됨**</span><span class="sxs-lookup"><span data-stu-id="11456-125">**Supported**</span></span> | <span data-ttu-id="11456-126">**마이그레이션 경로**</span><span class="sxs-lookup"><span data-stu-id="11456-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11456-127">ASP.NET 웹 양식</span><span class="sxs-lookup"><span data-stu-id="11456-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="11456-128">아니요</span><span class="sxs-lookup"><span data-stu-id="11456-128">No</span></span> |<span data-ttu-id="11456-129">변환 tooASP.NET 핵심 1 MVC</span><span class="sxs-lookup"><span data-stu-id="11456-129">Convert tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="11456-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="11456-130">ASP.NET MVC</span></span> |<span data-ttu-id="11456-131">마이그레이션 사용</span><span class="sxs-lookup"><span data-stu-id="11456-131">With Migration</span></span> |<span data-ttu-id="11456-132">업그레이드 tooASP.NET 핵심 1 MVC</span><span class="sxs-lookup"><span data-stu-id="11456-132">Upgrade tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="11456-133">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="11456-133">ASP.NET Web API</span></span> |<span data-ttu-id="11456-134">마이그레이션 사용</span><span class="sxs-lookup"><span data-stu-id="11456-134">With Migration</span></span> |<span data-ttu-id="11456-135">자체 호스팅된 서버 또는 ASP.NET Core 1 사용</span><span class="sxs-lookup"><span data-stu-id="11456-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="11456-136">ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="11456-136">ASP.NET Core 1</span></span> |<span data-ttu-id="11456-137">예</span><span class="sxs-lookup"><span data-stu-id="11456-137">Yes</span></span> |<span data-ttu-id="11456-138">해당 없음</span><span class="sxs-lookup"><span data-stu-id="11456-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="11456-139">진입점 API 및 수명 주기</span><span class="sxs-lookup"><span data-stu-id="11456-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="11456-140">작업자 역할 및 서비스 패브릭 서비스 API는 비슷한 진입점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="11456-141">**진입점**</span><span class="sxs-lookup"><span data-stu-id="11456-141">**Entry Point**</span></span> | <span data-ttu-id="11456-142">**작업자 역할**</span><span class="sxs-lookup"><span data-stu-id="11456-142">**Worker Role**</span></span> | <span data-ttu-id="11456-143">**서비스 패브릭 서비스**</span><span class="sxs-lookup"><span data-stu-id="11456-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11456-144">처리 중</span><span class="sxs-lookup"><span data-stu-id="11456-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="11456-145">VM 시작</span><span class="sxs-lookup"><span data-stu-id="11456-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="11456-146">해당 없음</span><span class="sxs-lookup"><span data-stu-id="11456-146">N/A</span></span> |
| <span data-ttu-id="11456-147">VM 중지</span><span class="sxs-lookup"><span data-stu-id="11456-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="11456-148">해당 없음</span><span class="sxs-lookup"><span data-stu-id="11456-148">N/A</span></span> |
| <span data-ttu-id="11456-149">클라이언트 요청에 대한 수신기 열기</span><span class="sxs-lookup"><span data-stu-id="11456-149">Open listener for client requests</span></span> |<span data-ttu-id="11456-150">해당 없음</span><span class="sxs-lookup"><span data-stu-id="11456-150">N/A</span></span> |<ul><li> <span data-ttu-id="11456-151">상태 비저장인 경우 `CreateServiceInstanceListener()`</span><span class="sxs-lookup"><span data-stu-id="11456-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="11456-152">상태 저장인 경우 `CreateServiceReplicaListener()`</span><span class="sxs-lookup"><span data-stu-id="11456-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="11456-153">작업자 역할</span><span class="sxs-lookup"><span data-stu-id="11456-153">Worker Role</span></span>
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

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="11456-154">서비스 패브릭 상태 비저장 서비스</span><span class="sxs-lookup"><span data-stu-id="11456-154">Service Fabric Stateless Service</span></span>
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

<span data-ttu-id="11456-155">둘 다는 toobegin 처리 주 "실행" 재정을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="11456-155">Both have a primary "Run" override in which toobegin processing.</span></span> <span data-ttu-id="11456-156">Service Fabric 서비스는 `Run`, `Start` 및 `Stop`을 단일 액세스 지점, `RunAsync`로 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="11456-157">서비스 작업 하는 경우 시작 해야 `RunAsync` 시작 되 고 해야 작동이 중지 hello `RunAsync` 메서드의 CancellationToken 신호를 받은 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-157">Your service should begin working when `RunAsync` starts, and should stop working when hello `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="11456-158">몇 가지 주요 차이점 hello 수명 주기 및 작업자 역할 및 서비스 패브릭 서비스의 수명이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-158">There are several key differences between hello lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="11456-159">**수명 주기:** hello 가장 큰 차이점은 작업자 역할 VM은 해당 수명 주기는 동 점된 toohello hello VM의 시작 및 중지 시기에 대 한 이벤트를 포함 하는 VM을 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-159">**Lifecycle:** hello biggest difference is that a Worker Role is a VM and so its lifecycle is tied toohello VM, which includes events for when hello VM starts and stops.</span></span> <span data-ttu-id="11456-160">서비스 패브릭 서비스 주기가 hello VM 수명 주기 별개 이므로 관련 되지 않은 대로 hello VM 또는 컴퓨터를 시작 및 중지를 호스트 하는 경우에 대 한 이벤트 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-160">A Service Fabric service has a lifecycle that is separate from hello VM lifecycle, so it does not include events for when hello host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="11456-161">**수명:** 경우 hello 작업자 역할 인스턴스를 재활용 합니다 `Run` 메서드 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11456-161">**Lifetime:** A Worker Role instance will recycle if hello `Run` method exits.</span></span> <span data-ttu-id="11456-162">그러나 hello `RunAsync` 서비스 패브릭 서비스에서 메서드 및 실행할 수 toocompletion hello 서비스 인스턴스를 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11456-162">hello `RunAsync` method in a Service Fabric service however can run toocompletion and hello service instance will stay up.</span></span> 

<span data-ttu-id="11456-163">서비스 패브릭은 클라이언트 요청을 수신 대기하는 서비스에 대한 선택적 통신 설정 진입점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="11456-164">Hello RunAsync와 통신 진입점은 서비스 패브릭 서비스-서비스 수 선택 tooonly 수신 대기 tooclient 요청 또는 처리 루프 또는 둘 다에 실행-이 hello RunAsync 메서드는 허용 하지 않고 tooexit 때문에 옵션 재정의 클라이언트 요청에 대 한 toolisten를 계속할 수 없기 때문에 hello 서비스 인스턴스를 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-164">Both hello RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose tooonly listen tooclient requests, or only run a processing loop, or both - which is why hello RunAsync method is allowed tooexit without restarting hello service instance, because it may continue toolisten for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="11456-165">응용 프로그램 API 및 환경</span><span class="sxs-lookup"><span data-stu-id="11456-165">Application API and environment</span></span>
<span data-ttu-id="11456-166">hello 클라우드 서비스 환경 API 정보 및 다른 VM 역할 인스턴스에 대 한 정보 뿐만 아니라 현재 VM 인스턴스 hello에 대 한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-166">hello Cloud Services environment API provides information and functionality for hello current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="11456-167">서비스 패브릭 tooits 런타임 관련 정보 및 hello 노드는 서비스에 대 한 정보에서 현재 실행 중인를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-167">Service Fabric provides information related tooits runtime and some information about hello node a service is currently running on.</span></span> 

| <span data-ttu-id="11456-168">**환경 작업**</span><span class="sxs-lookup"><span data-stu-id="11456-168">**Environment Task**</span></span> | <span data-ttu-id="11456-169">**클라우드 서비스**</span><span class="sxs-lookup"><span data-stu-id="11456-169">**Cloud Services**</span></span> | <span data-ttu-id="11456-170">**서비스 패브릭**</span><span class="sxs-lookup"><span data-stu-id="11456-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11456-171">구성 설정 및 변경 알림</span><span class="sxs-lookup"><span data-stu-id="11456-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="11456-172">로컬 저장소</span><span class="sxs-lookup"><span data-stu-id="11456-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="11456-173">끝점 정보</span><span class="sxs-lookup"><span data-stu-id="11456-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="11456-174">현재 인스턴스: `RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="11456-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="11456-175">다른 역할 및 인스턴스: `RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="11456-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="11456-176">현재 노드 주소의 경우 `NodeContext`</span><span class="sxs-lookup"><span data-stu-id="11456-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="11456-177">서비스 끝점 검색의 경우 `FabricClient` 및 `ServicePartitionResolver`</span><span class="sxs-lookup"><span data-stu-id="11456-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="11456-178">환경 에뮬레이션</span><span class="sxs-lookup"><span data-stu-id="11456-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="11456-179">해당 없음</span><span class="sxs-lookup"><span data-stu-id="11456-179">N/A</span></span> |
| <span data-ttu-id="11456-180">동시 변경 이벤트</span><span class="sxs-lookup"><span data-stu-id="11456-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="11456-181">해당 없음</span><span class="sxs-lookup"><span data-stu-id="11456-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="11456-182">구성 설정</span><span class="sxs-lookup"><span data-stu-id="11456-182">Configuration settings</span></span>
<span data-ttu-id="11456-183">클라우드 서비스의 구성 설정 VM 역할에 대해 설정 되 고 tooall 해당 VM 역할 인스턴스를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-183">Configuration settings in Cloud Services are set for a VM role and apply tooall instances of that VM role.</span></span> <span data-ttu-id="11456-184">이러한 설정은 ServiceConfiguration.*.cscfg 파일에서 설정된 키-값 쌍이며 RoleEnvironment를 통해 직접 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="11456-185">서비스 패브릭에서 설정이 적용 개별적으로 tooa VM 보다는 tooeach 서비스 tooeach 응용 프로그램 서비스 및 응용 프로그램을 여러 VM를 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-185">In Service Fabric, settings apply individually tooeach service and tooeach application, rather than tooa VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="11456-186">서비스는 세 가지 패키지로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="11456-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="11456-187">**코드:** hello 서비스 실행 파일, 이진 파일, Dll, 및 기타 파일에 포함 된 서비스가 필요한 toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-187">**Code:** contains hello service executables, binaries, DLLs, and any other files a service needs toorun.</span></span>
* <span data-ttu-id="11456-188">**Config:** 서비스에 대한 모든 구성 파일 및 설정.</span><span class="sxs-lookup"><span data-stu-id="11456-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="11456-189">**데이터:** hello 서비스와 연결 된 정적 데이터 파일.</span><span class="sxs-lookup"><span data-stu-id="11456-189">**Data:** static data files associated with hello service.</span></span>

<span data-ttu-id="11456-190">이러한 각 패키지는 서비스를 독립적으로 버전 지정 및 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="11456-191">API를 통해 비슷한 tooCloud 서비스를 구성 패키지를 프로그래밍 방식으로 액세스할 수 있습니다 및 이벤트는 사용할 수 있는 toonotify hello 서비스의 구성 패키지 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-191">Similar tooCloud Services, a config package can be accessed programmatically through an API and events are available toonotify hello service of a config package change.</span></span> <span data-ttu-id="11456-192">Settings.xml 파일 키-값 구성 및 프로그래밍 방식 액세스 비슷한 toohello 응용 프로그램 설정 섹션의 App.config 파일에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-192">A Settings.xml file can be used for key-value configuration and programmatic access similar toohello app settings section of an App.config file.</span></span> <span data-ttu-id="11456-193">그러나 클라우드 서비스와는 달리 서비스 패브릭 config 패키지는 XML, JSON, YAML 또는 사용자 지정 이진 형식이든 모든 형식의 구성 파일을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="11456-194">구성 액세스</span><span class="sxs-lookup"><span data-stu-id="11456-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="11456-195">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="11456-195">Cloud Services</span></span>
<span data-ttu-id="11456-196">ServiceConfiguration.*.cscfg의 구성 설정은 `RoleEnvironment`을(를) 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="11456-197">이러한 설정은 hello에 전체적으로 사용 가능한 tooall 역할 인스턴스는 동일한 클라우드 서비스 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-197">These settings are globally available tooall role instances in hello same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="11456-198">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="11456-198">Service Fabric</span></span>
<span data-ttu-id="11456-199">각 서비스에는 자체 개별 구성 패키지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="11456-200">클러스터의 모든 응용 프로그램에서 액세스할 수 있는 전역 구성 설정에 대한 기본 제공 메커니즘이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="11456-201">구성 패키지 내에서 서비스 패브릭 특수 Settings.xml 구성 파일을 사용할 때 가능한 응용 프로그램 수준 구성 설정을 지정 하기 hello 응용 프로그램 수준 Settings.xml에 값을 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at hello application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="11456-202">구성 설정은 hello 서비스를 통해 각 서비스 인스턴스 내의 액세스 `CodePackageActivationContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-202">Configuration settings are accesses within each service instance through hello service's `CodePackageActivationContext`.</span></span>

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

### <a name="configuration-update-events"></a><span data-ttu-id="11456-203">구성 업데이트 이벤트</span><span class="sxs-lookup"><span data-stu-id="11456-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="11456-204">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="11456-204">Cloud Services</span></span>
<span data-ttu-id="11456-205">hello `RoleEnvironment.Changed` 이벤트는 사용 되는 toonotify 변경 될 때 모든 역할 인스턴스가 구성 변경 등의 hello 환경에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-205">hello `RoleEnvironment.Changed` event is used toonotify all role instances when a change occurs in hello environment, such as a configuration change.</span></span> <span data-ttu-id="11456-206">역할 인스턴스 재활용 하거나 작업자 프로세스를 다시 시작 하지 않고 사용된 tooconsume 구성 업데이트입니다.</span><span class="sxs-lookup"><span data-stu-id="11456-206">This is used tooconsume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="11456-207">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="11456-207">Service Fabric</span></span>
<span data-ttu-id="11456-208">각 hello 세 패키지 형식-코드, 구성, 및 데이터 액세스 서비스에는 패키지 업데이트, 추가 또는 제거 하는 경우 서비스 인스턴스를 알려 주는 이벤트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-208">Each of hello three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="11456-209">서비스는 각 유형의 여러 패키지를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="11456-210">예를 들어 서비스에는 각각 개별적으로 버전이 지정되고 업그레이드 가능한 여러 config 패키지가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11456-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="11456-211">이러한 이벤트는 hello 서비스 인스턴스를 다시 시작 하지 않고 서비스 패키지에 사용할 수 있는 tooconsume 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-211">These events are available tooconsume changes in service packages without restarting hello service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="11456-212">시작 작업</span><span class="sxs-lookup"><span data-stu-id="11456-212">Startup tasks</span></span>
<span data-ttu-id="11456-213">시작 작업은 응용 프로그램이 시작되기 전에 수행되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="11456-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="11456-214">시작 작업에는 상승 된 권한을 사용 하 여 일반적으로 사용 되는 toorun 설치 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="11456-214">A startup task is typically used toorun setup scripts using elevated privileges.</span></span> <span data-ttu-id="11456-215">클라우드 서비스와 서비스 패브릭은 시작 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="11456-216">hello 주요 차이점은 해당 클라우드 서비스, 시작 작업은 동률된 tooa VM 역할 인스턴스는 속해 있기 때문에 서비스 패브릭 시작 작업 동률된 tooany 않은 동 점된 tooa 서비스입니다. 반면 특정 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="11456-216">hello main difference is that in Cloud Services, a startup task is tied tooa VM because it is part of a role instance, whereas in Service Fabric a startup task is tied tooa service, which is not tied tooany particular VM.</span></span>

| <span data-ttu-id="11456-217">클라우드 서비스</span><span class="sxs-lookup"><span data-stu-id="11456-217">Cloud Services</span></span> | <span data-ttu-id="11456-218">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="11456-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11456-219">구성 위치</span><span class="sxs-lookup"><span data-stu-id="11456-219">Configuration location</span></span> |<span data-ttu-id="11456-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="11456-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="11456-221">권한</span><span class="sxs-lookup"><span data-stu-id="11456-221">Privileges</span></span> |<span data-ttu-id="11456-222">"제한된" 또는 "상승된"</span><span class="sxs-lookup"><span data-stu-id="11456-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="11456-223">시퀀싱</span><span class="sxs-lookup"><span data-stu-id="11456-223">Sequencing</span></span> |<span data-ttu-id="11456-224">"간단", "백그라운드", "포그라운드"</span><span class="sxs-lookup"><span data-stu-id="11456-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="11456-225">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="11456-225">Cloud Services</span></span>
<span data-ttu-id="11456-226">클라우드 서비스에서 시작 진입점은 ServiceDefinition.csdef에서 역할별로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="11456-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

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

### <a name="service-fabric"></a><span data-ttu-id="11456-227">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="11456-227">Service Fabric</span></span>
<span data-ttu-id="11456-228">서비스 패브릭에서 시작 진입점은 ServiceManifest.xml에서 서비스별로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="11456-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

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

## <a name="a-note-about-development-environment"></a><span data-ttu-id="11456-229">개발 환경에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="11456-229">A note about development environment</span></span>
<span data-ttu-id="11456-230">클라우드 서비스와 서비스 패브릭 및 통합 되어 Visual studio 프로젝트 템플릿 디버깅, 구성 및 둘 다를 로컬로 배포에 대 한 지원 및 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and tooAzure.</span></span> <span data-ttu-id="11456-231">클라우드 서비스와 서비스 패브릭은 로컬 개발 런타임 환경도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="11456-232">hello 차이점은 hello 개발 런타임을 에뮬레이션 하는 클라우드 서비스 hello 실행 되는 Azure 환경, 서비스 패브릭 에뮬레이터를 사용 하지 않는-hello 전체 서비스 패브릭 런타임을 사용 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="11456-232">hello difference is that while hello Cloud Service development runtime emulates hello Azure environment on which it runs, Service Fabric does not use an emulator - it uses hello complete Service Fabric runtime.</span></span> <span data-ttu-id="11456-233">hello 로컬 개발 컴퓨터에서 실행 되는 환경이 서비스 패브릭 hello 프로덕션 환경에서 실행 되는 동일한 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="11456-233">hello Service Fabric environment you run on your local development machine is hello same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11456-234">다음 단계</span><span class="sxs-lookup"><span data-stu-id="11456-234">Next steps</span></span>
<span data-ttu-id="11456-235">서비스 패브릭 신뢰할 수 있는 서비스 및 클라우드 서비스 및 서비스 패브릭 응용 프로그램 아키텍처 toounderstand 서비스 패브릭 기능의 전체 hello tootake 활용을 설정 하는 방법 간의 근본적인 차이점 hello에 대 한 자세한 사용 되는 읽기입니다.</span><span class="sxs-lookup"><span data-stu-id="11456-235">Read more about Service Fabric Reliable Services and hello fundamental differences between Cloud Services and Service Fabric application architecture toounderstand how tootake advantage of hello full set of Service Fabric features.</span></span>

* [<span data-ttu-id="11456-236">서비스 패브릭 신뢰할 수 있는 서비스 시작</span><span class="sxs-lookup"><span data-stu-id="11456-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="11456-237">클라우드 서비스 및 서비스 패브릭 간의 개념적 가이드 toohello 차이점</span><span class="sxs-lookup"><span data-stu-id="11456-237">Conceptual guide toohello differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
