---
title: "클라우드 서비스 및 서비스 패브릭 간의 aaaDifferences | Microsoft Docs"
description: "마이그레이션에 대 한 개념적인 개요 tooService 클라우드 서비스 패브릭에서에서 응용 프로그램입니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 0b87b1d3-88ad-4658-a465-9f05a3376dee
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: bbc5ef4fe0fe1b0da55454cb6b766925030198fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-hello-differences-between-cloud-services-and-service-fabric-before-migrating-applications"></a><span data-ttu-id="dfeb4-103">마이그레이션을 수행 하기 전에 클라우드 서비스 및 서비스 패브릭 hello 차이점에 대 한 자세한 내용은 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-103">Learn about hello differences between Cloud Services and Service Fabric before migrating applications.</span></span>
<span data-ttu-id="dfeb4-104">Microsoft Azure 서비스 패브릭은 확장성과 안정성이 뛰어난 분산된 응용 프로그램에 대 한 hello 차세대 클라우드 응용 프로그램 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-104">Microsoft Azure Service Fabric is hello next-generation cloud application platform for highly scalable, highly reliable distributed applications.</span></span> <span data-ttu-id="dfeb4-105">분산된 클라우드 응용 프로그램을 패키징, 배포, 업그레이드 및 관리하 위한 여러 가지 새로운 기능을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-105">It introduces many new features for packaging, deploying, upgrading, and managing distributed cloud applications.</span></span> 

<span data-ttu-id="dfeb4-106">클라우드 서비스 tooService 패브릭에서에서는 가이드 (영문) toomigrating 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-106">This is an introductory guide toomigrating applications from Cloud Services tooService Fabric.</span></span> <span data-ttu-id="dfeb4-107">클라우드 서비스와 서비스 패브릭 간의 아키텍처 및 디자인 차이점에 대해 주로 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-107">It focuses primarily on architectural and design differences between Cloud Services and Service Fabric.</span></span>

## <a name="applications-and-infrastructure"></a><span data-ttu-id="dfeb4-108">응용 프로그램 및 인프라</span><span class="sxs-lookup"><span data-stu-id="dfeb4-108">Applications and infrastructure</span></span>
<span data-ttu-id="dfeb4-109">클라우드 서비스 및 서비스 패브릭 근본적인 차이점 Vm, 작업, 및 응용 프로그램 사이 hello 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-109">A fundamental difference between Cloud Services and Service Fabric is hello relationship between VMs, workloads, and applications.</span></span> <span data-ttu-id="dfeb4-110">여기에 작업 tooperform 특정 작업을 작성 하거나 서비스를 제공 하는 hello 코드로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-110">A workload here is defined as hello code you write tooperform a specific task or provide a service.</span></span>

* <span data-ttu-id="dfeb4-111">**클라우드 서비스는 VM으로 응용 프로그램 배포에 대한 것입니다.**</span><span class="sxs-lookup"><span data-stu-id="dfeb4-111">**Cloud Services is about deploying applications as VMs.**</span></span> <span data-ttu-id="dfeb4-112">hello 코드를 작성 하는 웹 또는 작업자 역할과 같은 밀접 하 게 결합 된 tooa VM 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-112">hello code you write is tightly coupled tooa VM instance, such as a Web or Worker Role.</span></span> <span data-ttu-id="dfeb4-113">toodeploy 클라우드 서비스에서 작업 하나 toodeploy 또는 더 많은 VM 인스턴스 실행된 하는 hello 작업.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-113">toodeploy a workload in Cloud Services is toodeploy one or more VM instances that run hello workload.</span></span> <span data-ttu-id="dfeb4-114">응용 프로그램과 VM의 분리가 없으므로 응용 프로그램의 공식 정의가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-114">There is no separation of applications and VMs, and so there is no formal definition of an application.</span></span> <span data-ttu-id="dfeb4-115">응용 프로그램은 클라우드 서비스 배포 내에서 웹 또는 작업자 역할 인스턴스 집합 또는 전체 클라우드 서비스 배포로 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-115">An application can be thought of as a set of Web or Worker Role instances within a Cloud Services deployment or as an entire Cloud Services deployment.</span></span> <span data-ttu-id="dfeb4-116">이 예제에서 응용 프로그램은 역할 인스턴스 집합으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-116">In this example, an application is shown as a set of role instances.</span></span>

![클라우드 서비스 응용 프로그램 및 토폴로지][1]

* <span data-ttu-id="dfeb4-118">**배포 응용 프로그램 tooexisting Vm 또는 서비스 패브릭 Windows 또는 Linux에서 실행 되는 컴퓨터에 대 한 서비스 패브릭은입니다.**</span><span class="sxs-lookup"><span data-stu-id="dfeb4-118">**Service Fabric is about deploying applications tooexisting VMs or machines running Service Fabric on Windows or Linux.**</span></span> <span data-ttu-id="dfeb4-119">작성 하는 hello 서비스는 hello 추출 된 hello 서비스 패브릭 응용 프로그램 플랫폼으로 응용 프로그램에 배포 된 toomultiple 환경 될 수 있도록 하는 인프라를 내부에서 완전히 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-119">hello services you write are completely decoupled from hello underlying infrastructure, which is abstracted away by hello Service Fabric application platform, so an application can be deployed toomultiple environments.</span></span> <span data-ttu-id="dfeb4-120">서비스 패브릭에서 작업 "서비스" 라고 하 고 하나 이상의 서비스는 hello 서비스 패브릭 응용 프로그램 플랫폼에서 실행 되는 공식적으로 정의 된 응용 프로그램에 그룹화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-120">A workload in Service Fabric is called a "service," and one or more services are grouped in a formally-defined application that runs on hello Service Fabric application platform.</span></span> <span data-ttu-id="dfeb4-121">여러 응용 프로그램 배포 tooa 단일 서비스 패브릭 클러스터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-121">Multiple applications can be deployed tooa single Service Fabric cluster.</span></span>

![서비스 패브릭 응용 프로그램 및 토폴로지][2]

<span data-ttu-id="dfeb4-123">서비스 패브릭 자체는 Windows 또는 Linux에서 실행하는 응용 프로그램 플랫폼 계층인 반면 클라우드 서비스는 연결된 작업과 Azure에서 관리하는 VM을 배포하기 위한 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-123">Service Fabric itself is an application platform layer that runs on Windows or Linux, whereas Cloud Services is a system for deploying Azure-managed VMs with workloads attached.</span></span>
<span data-ttu-id="dfeb4-124">hello 서비스 패브릭 응용 프로그램 모델에 여러 가지 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-124">hello Service Fabric application model has a number of advantages:</span></span>

* <span data-ttu-id="dfeb4-125">빠른 배포 시간.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-125">Fast deployment times.</span></span> <span data-ttu-id="dfeb4-126">VM 인스턴스를 만드는 시간이 많이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-126">Creating VM instances can be time consuming.</span></span> <span data-ttu-id="dfeb4-127">서비스 패브릭 tooform 호스트 하는 클러스터 서비스 패브릭 응용 프로그램 플랫폼 hello 후에 Vm 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-127">In Service Fabric, VMs are only deployed once tooform a cluster that hosts hello Service Fabric application platform.</span></span> <span data-ttu-id="dfeb4-128">해당 지점에서 응용 프로그램 패키지에서 배포 된 toohello 클러스터가 매우 신속 하 게 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-128">From that point on, application packages can be deployed toohello cluster very quickly.</span></span>
* <span data-ttu-id="dfeb4-129">고밀도 호스팅.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-129">High-density hosting.</span></span> <span data-ttu-id="dfeb4-130">클라우드 서비스에서 작업자 역할 VM은 하나의 작업을 호스팅합니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-130">In Cloud Services, a Worker Role VM hosts one workload.</span></span> <span data-ttu-id="dfeb4-131">서비스 패브릭 응용 프로그램 의미 많은 수의 응용 프로그램 tooa 적은 수의 대규모 배포에 대 한 전반적인 비용을 낮출 수 있는 Vm 배포할 수 있습니다,를 실행 하는 hello Vm 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-131">In Service Fabric, applications are separate from hello VMs that run them, meaning you can deploy a large number of applications tooa small number of VMs, which can lower overall cost for larger deployments.</span></span>
* <span data-ttu-id="dfeb4-132">서비스 패브릭 플랫폼 수 모든 위치에서 실행 하는 hello Azure 또는 온-프레미스 Windows Server 또는 Linux 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-132">hello Service Fabric platform can run anywhere that has Windows Server or Linux machines, whether it's Azure or on-premises.</span></span> <span data-ttu-id="dfeb4-133">hello 플랫폼 응용 프로그램은 다른 환경에서 실행 될 수 있도록 hello 기본 인프라 위에 추상화 계층을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-133">hello platform provides an abstraction layer over hello underlying infrastructure so your application can run on different environments.</span></span> 
* <span data-ttu-id="dfeb4-134">분산된 응용 프로그램 관리.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-134">Distributed application management.</span></span> <span data-ttu-id="dfeb4-135">서비스 패브릭은 분산 응용 프로그램과 호스트 뿐 아니라 통해 수명 주기 동안 VM을 호스팅하는 hello와 독립적으로 관리 하거나 수명 주기를 컴퓨터 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-135">Service Fabric is a platform that not only hosts distributed applications, but also helps manage their lifecycle independently of hello hosting VM or machine lifecycle.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="dfeb4-136">응용 프로그램 아키텍처</span><span class="sxs-lookup"><span data-stu-id="dfeb4-136">Application architecture</span></span>
<span data-ttu-id="dfeb4-137">hello 클라우드 서비스 응용 프로그램의 아키텍처 일반적으로 포함 되어 서비스 버스, Azure 테이블 및 Blob 저장소, SQL, Redis, 등과 같은 다양 한 외부 서비스 종속성, 상태 및 데이터를 응용 프로그램 및 웹 간의 통신 toomanage hello 및 클라우드 서비스 배포에서 작업자 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-137">hello architecture of a Cloud Services application usually includes numerous external service dependencies, such as Service Bus, Azure Table and Blob Storage, SQL, Redis, and others toomanage hello state and data of an application and communication between Web and Worker Roles in a Cloud Services deployment.</span></span> <span data-ttu-id="dfeb4-138">완전한 클라우드 서비스 응용 프로그램의 예는 다음과 같이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-138">An example of a complete Cloud Services application might look like this:</span></span>  

![클라우드 서비스 아키텍처][9]

<span data-ttu-id="dfeb4-140">서비스 패브릭 응용 프로그램 서비스를 선택할 수도 toouse hello 동일한 외부 완전 한 응용 프로그램에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-140">Service Fabric applications can also choose toouse hello same external services in a complete application.</span></span> <span data-ttu-id="dfeb4-141">이 예제에서는 클라우드 서비스 아키텍처를 사용 하 여 클라우드 서비스 tooService 패브릭에서에서 hello 가장 간단한 마이그레이션 경로 hello 유지 서비스 패브릭 응용 프로그램을 tooreplace만 hello 클라우드 서비스 배포 전체 아키텍처 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-141">Using this example Cloud Services architecture, hello simplest migration path from Cloud Services tooService Fabric is tooreplace only hello Cloud Services deployment with a Service Fabric application, keeping hello overall architecture hello same.</span></span> <span data-ttu-id="dfeb4-142">hello 웹 및 작업자 역할에는 최소한의 코드 변경 내용으로 가져올된 tooService 패브릭 상태 비저장 서비스 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-142">hello Web and Worker Roles can be ported tooService Fabric stateless services with minimal code changes.</span></span>

![간단한 마이그레이션 후 서비스 패브릭 아키텍처][10]

<span data-ttu-id="dfeb4-144">이 단계에서는 hello 시스템 계속 toowork 이전과 동일 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-144">At this stage, hello system should continue toowork hello same as before.</span></span> <span data-ttu-id="dfeb4-145">서비스 패브릭의 상태 저장 기능을 활용하여 외부 상태 저장소는 적용 가능한 상태 저장 서비스로 내부화될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-145">Taking advantage of Service Fabric's stateful features, external state stores can be internalized as stateful services where applicable.</span></span> <span data-ttu-id="dfeb4-146">이 하기 전에 hello 외부 서비스와 마찬가지로 동일한 기능 tooyour 응용 프로그램을 제공 하는 사용자 지정 서비스를 작성 해야 하므로 웹 및 작업자 역할 tooService 패브릭 상태 비저장 서비스의 간단한 마이그레이션 보다 훨씬 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-146">This is more involved than a simple migration of Web and Worker Roles tooService Fabric stateless services, as it requires writing custom services that provide equivalent functionality tooyour application as hello external services did before.</span></span> <span data-ttu-id="dfeb4-147">이 따른 hello 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-147">hello benefits of doing so include:</span></span> 

* <span data-ttu-id="dfeb4-148">외부 종속성 제거</span><span class="sxs-lookup"><span data-stu-id="dfeb4-148">Removing external dependencies</span></span> 
* <span data-ttu-id="dfeb4-149">Hello 배포, 관리 및 업그레이드 모델을 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-149">Unifying hello deployment, management, and upgrade models.</span></span> 

<span data-ttu-id="dfeb4-150">이러한 서비스 내부화의 예제 결과 아키텍처는 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-150">An example resulting architecture of internalizing these services could look like this:</span></span>

![전체 마이그레이션 후 서비스 패브릭 아키텍처][11]

## <a name="communication-and-workflow"></a><span data-ttu-id="dfeb4-152">통신 및 워크플로</span><span class="sxs-lookup"><span data-stu-id="dfeb4-152">Communication and workflow</span></span>
<span data-ttu-id="dfeb4-153">대부분의 클라우드 서비스 응용 프로그램은 둘 이상의 계층으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-153">Most Cloud Service applications consist of more than one tier.</span></span> <span data-ttu-id="dfeb4-154">마찬가지로 서비스 패브릭 응용 프로그램은 둘 이상의 서비스(일반적으로 많은 서비스)로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-154">Similarly, a Service Fabric application consists of more than one service (typically many services).</span></span> <span data-ttu-id="dfeb4-155">두 일반적인 통신 모델은 직접 통신이며 외부 영구 저장소를 경유합니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-155">Two common communication models are direct communication and via an external durable storage.</span></span>

### <a name="direct-communication"></a><span data-ttu-id="dfeb4-156">직접 통신</span><span class="sxs-lookup"><span data-stu-id="dfeb4-156">Direct communication</span></span>
<span data-ttu-id="dfeb4-157">직접 통신을 사용하여 계층은 각 계층에서 노출된 끝점을 통해 직접 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-157">With direct communication, tiers can communicate directly through endpoint exposed by each tier.</span></span> <span data-ttu-id="dfeb4-158">상태 비저장 등의 환경에서는 클라우드 서비스,이 방법을 선택 하는 VM 역할의 인스턴스 하거나 임의로 또는 라운드 로빈 toobalance 부하 및 직접 연결 tooits 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-158">In stateless environments such as Cloud Services, this means selecting an instance of a VM role, either randomly or round-robin toobalance load, and connecting tooits endpoint directly.</span></span>

![클라우드 서비스 직접 통신][5]

 <span data-ttu-id="dfeb4-160">직접 통신은 서비스 패브릭에서 일반적인 통신 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-160">Direct communication is a common communication model in Service Fabric.</span></span> <span data-ttu-id="dfeb4-161">서비스 패브릭 및 클라우드 서비스 간의 주요 차이점 hello는 tooa 서비스 서비스 패브릭에서 연결 하는 반면 클라우드 서비스에서 tooa VM을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-161">hello key difference between Service Fabric and Cloud Services is that in Cloud Services you connect tooa VM, whereas in Service Fabric you connect tooa service.</span></span> <span data-ttu-id="dfeb4-162">이는 몇 가지 이유로 중요한 차이점입니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-162">This is an important distinction for a couple reasons:</span></span>

* <span data-ttu-id="dfeb4-163">서비스 패브릭에서 서비스가 지원 되지 않습니다 호스트 하는 바인딩된 toohello Vm 서비스는 hello 클러스터에서 이동할 수 있습니다 및 사실 주위 예상된 toomove 다양 한 이유로: 리소스 균형 조정, 장애 조치, 응용 프로그램 및 인프라 업그레이드 및 배치 또는 로드 제약 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-163">Services in Service Fabric are not bound toohello VMs that host them; services may move around in hello cluster, and in fact, are expected toomove around for various reasons: Resource balancing, failover, application and infrastructure upgrades, and placement or load constraints.</span></span> <span data-ttu-id="dfeb4-164">즉, 서비스 인스턴스의 주소는 언제든지 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-164">This means a service instance's address can change at any time.</span></span> 
* <span data-ttu-id="dfeb4-165">서비스 패브릭의 VM은 각각 고유 끝점으로 여러 서비스를 호스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-165">A VM in Service Fabric can host multiple services, each with unique endpoints.</span></span>

<span data-ttu-id="dfeb4-166">서비스 패브릭 명명 서비스를 서비스의 끝점 주소를 사용 하는 tooresolve 될 수 있는 hello 라고 하는 서비스 검색 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-166">Service Fabric provides a service discovery mechanism, called hello Naming Service, which can be used tooresolve endpoint addresses of services.</span></span> 

![서비스 패브릭 직접 통신][6]

### <a name="queues"></a><span data-ttu-id="dfeb4-168">큐</span><span class="sxs-lookup"><span data-stu-id="dfeb4-168">Queues</span></span>
<span data-ttu-id="dfeb4-169">클라우드 서비스와 같은 상태 비저장 환경의 계층 간 일반 통신 메커니즘은 toouse 외부 저장소 큐 toodurably tooanother 계층이 두 개를 작업 작업을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-169">A common communication mechanism between tiers in stateless environments such as Cloud Services is toouse an external storage queue toodurably store work tasks from one tier tooanother.</span></span> <span data-ttu-id="dfeb4-170">일반적인 시나리오에는 작업 tooan Azure 큐에서 전송 하는 웹 계층 또는 Service Bus 작업자 역할 인스턴스 수 큐에서 제거 하 고 hello 작업을 처리 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-170">A common scenario is a web tier that sends jobs tooan Azure Queue or Service Bus where Worker Role instances can dequeue and process hello jobs.</span></span>

![클라우드 서비스 큐 통신][7]

<span data-ttu-id="dfeb4-172">hello 서비스 패브릭에서 동일한 통신 모델을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-172">hello same communication model can be used in Service Fabric.</span></span> <span data-ttu-id="dfeb4-173">기존 클라우드 서비스 응용 프로그램 tooService 패브릭 마이그레이션하는 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-173">This can be useful when migrating an existing Cloud Services application tooService Fabric.</span></span> 

![서비스 패브릭 직접 통신][8]

## <a name="next-steps"></a><span data-ttu-id="dfeb4-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dfeb4-175">Next Steps</span></span>
<span data-ttu-id="dfeb4-176">hello 패브릭은 hello 유지 서비스 패브릭 응용 프로그램을 클라우드 서비스 배포 hello 응용 프로그램의 전반적인 아키텍처 대략 tooreplace는 클라우드 서비스 tooService에서 가장 간단한 마이그레이션 경로 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-176">hello simplest migration path from Cloud Services tooService Fabric is tooreplace only hello Cloud Services deployment with a Service Fabric application, keeping hello overall architecture of your application roughly hello same.</span></span> <span data-ttu-id="dfeb4-177">다음 문서는 hello toohelp convert 웹 또는 작업자 역할 tooa 서비스 패브릭 상태 비저장 서비스 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-177">hello following article provides a guide toohelp convert a Web or Worker Role tooa Service Fabric stateless service.</span></span>

* [<span data-ttu-id="dfeb4-178">간단한 마이그레이션: 웹 또는 작업자 역할 tooa 서비스 패브릭 상태 비저장 서비스를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfeb4-178">Simple migration: convert a Web or Worker Role tooa Service Fabric stateless service</span></span>](service-fabric-cloud-services-migration-worker-role-stateless-service.md)

<!--Image references-->
[1]: ./media/service-fabric-cloud-services-migration-differences/topology-cloud-services.png
[2]: ./media/service-fabric-cloud-services-migration-differences/topology-service-fabric.png
[5]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-direct.png
[6]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-direct.png
[7]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-queues.png
[8]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-queues.png
[9]: ./media/service-fabric-cloud-services-migration-differences/cloud-services-architecture.png
[10]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-simple.png
[11]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-full.png
