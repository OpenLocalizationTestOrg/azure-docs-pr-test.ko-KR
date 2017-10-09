---
title: "aaaService 패브릭 프로젝트 생성 다음 단계 | Microsoft Docs"
description: "서비스 패브릭 용 핵심 개발 작업의 링크 tooa 집합을 포함 하는이 문서"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="c28f7-103">서비스 패브릭 응용 프로그램 및 다음 단계</span><span class="sxs-lookup"><span data-stu-id="c28f7-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="c28f7-104">Azure 서비스 패브릭 응용 프로그램이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="c28f7-105">이 문서에는 몇 가지 잠재적인 다음 단계와 프로젝트의 hello 구성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-105">This article describes hello makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="c28f7-106">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c28f7-106">Your application</span></span>
<span data-ttu-id="c28f7-107">모든 새 응용 프로그램에는 응용 프로그램 프로젝트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-107">Every new application includes an application project.</span></span> <span data-ttu-id="c28f7-108">선택한 서비스의 hello 유형에 따라 하나 또는 두 개의 추가 프로젝트 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-108">There may be one or two additional projects, depending on hello type of service chosen.</span></span>

### <a name="hello-application-project"></a><span data-ttu-id="c28f7-109">hello 응용 프로그램 프로젝트</span><span class="sxs-lookup"><span data-stu-id="c28f7-109">hello application project</span></span>
<span data-ttu-id="c28f7-110">hello 응용 프로그램 프로젝트 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-110">hello application project consists of:</span></span>

* <span data-ttu-id="c28f7-111">응용 프로그램을 구성 하는 toohello 서비스 참조의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-111">A set of references toohello services that make up your application.</span></span>
* <span data-ttu-id="c28f7-112">3 개의 게시 프로필 (1 개 노드 로컬, 5 노드 로컬 및 클라우드) toomaintain 설정을 기본 설정 관련된 tooa 클러스터 끝점 및 tooperform 기본적으로 배포를 업그레이드 하는 여부와 같은 다른 환경-작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use toomaintain preferences for working with different environments--such as preferences related tooa cluster endpoint and whether tooperform upgrade deployments by default.</span></span>
* <span data-ttu-id="c28f7-113">세 개의 응용 프로그램 매개 변수 파일 (위 항목과 동일) 서비스에 대 한 파티션 toocreate hello 수와 같이 toomaintain 환경 관련 응용 프로그램 구성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-113">Three application parameter files (same as above) that you can use toomaintain environment-specific application configurations, such as hello number of partitions toocreate for a service.</span></span>
* <span data-ttu-id="c28f7-114">사용할 수 있는 toodeploy hello 명령줄에서 또는 자동화 된 연속 통합 및 배포 파이프라인의 일부로 응용 프로그램 배포 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-114">A deployment script that you can use toodeploy your application from hello command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="c28f7-115">hello 응용 프로그램 매니페스트 hello 응용 프로그램에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-115">hello application manifest, which describes hello application.</span></span> <span data-ttu-id="c28f7-116">Hello ApplicationPackageRoot 폴더 hello 매니페스트를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-116">You can find hello manifest under hello ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="c28f7-117">상태 비저장 서비스</span><span class="sxs-lookup"><span data-stu-id="c28f7-117">Stateless service</span></span>
<span data-ttu-id="c28f7-118">새 상태 비저장 서비스를 추가 하면 Visual Studio에서 하위 유형을 포함 하는 서비스 프로젝트 tooyour 솔루션 추가 `StatelessService`합니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-118">When you add a new stateless service, Visual Studio adds a service project tooyour solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="c28f7-119">hello 서비스 카운터의 지역 변수를 증가 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-119">hello service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="c28f7-120">상태 저장 서비스</span><span class="sxs-lookup"><span data-stu-id="c28f7-120">Stateful service</span></span>
<span data-ttu-id="c28f7-121">새 상태 저장 서비스를 추가 하면 Visual Studio에서 하위 유형을 포함 하는 서비스 프로젝트 tooyour 솔루션 추가 `StatefulService`합니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-121">When you add a new stateful service, Visual Studio adds a service project tooyour solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="c28f7-122">hello 서비스 카운터를 증가 시키는에 해당 `RunAsync` 메서드 및 저장소 hello 결과에 `ReliableDictionary`합니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-122">hello service increments a counter in its `RunAsync` method and stores hello result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="c28f7-123">행위자 서비스</span><span class="sxs-lookup"><span data-stu-id="c28f7-123">Actor service</span></span>
<span data-ttu-id="c28f7-124">새 신뢰할 수 있는 작업자를 추가 하면 Visual Studio에서는 두 개의 프로젝트 tooyour 솔루션 추가: 행위자 프로젝트 및 인터페이스 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="c28f7-124">When you add a new reliable actor, Visual Studio adds two projects tooyour solution: an actor project and an interface project.</span></span>

<span data-ttu-id="c28f7-125">hello 행위자 프로젝트 설정에 대 한 메서드를 제공 하 고 hello 카운터 값을 가져오는 hello 행위자 상태 내에서 안정적으로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-125">hello actor project provides methods for setting and getting hello value of a counter that is reliably persisted within hello actor's state.</span></span> <span data-ttu-id="c28f7-126">hello 인터페이스 프로젝트 인터페이스는 다른 서비스 제공 tooinvoke hello 행위자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-126">hello interface project provides an interface that other services can use tooinvoke hello actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="c28f7-127">상태 비저장 웹 API</span><span class="sxs-lookup"><span data-stu-id="c28f7-127">Stateless Web API</span></span>
<span data-ttu-id="c28f7-128">hello 상태 비저장 웹 API 프로젝트는 기본 제공 웹 서비스를 사용할 수 있는 tooopen tooexternal 클라이언트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-128">hello stateless Web API project provides a basic web service that you can use tooopen your application tooexternal clients.</span></span> <span data-ttu-id="c28f7-129">Hello 프로젝트 구성 방법에 대 한 자세한 내용은 참조 [OWIN 자체 호스트 된 서비스 패브릭 웹 API 서비스](service-fabric-reliable-services-communication-webapi.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-129">For more information about how hello project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="c28f7-130">ASP.NET core</span><span class="sxs-lookup"><span data-stu-id="c28f7-130">ASP.NET core</span></span>
<span data-ttu-id="c28f7-131">서비스 패브릭 SDK hello 제공 독립 실행형 ASP.NET Core 프로젝트에 사용할 수 있는 ASP.NET Core 서식 파일의 설정 같은 hello: 비어 있는 경우 [웹 API][aspnet-webapi], 및 [웹 응용 프로그램][aspnet-webapp].</span><span class="sxs-lookup"><span data-stu-id="c28f7-131">hello Service Fabric SDK provides hello same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="c28f7-132">게스트 실행 파일 및 게스트 컨테이너</span><span class="sxs-lookup"><span data-stu-id="c28f7-132">Guest executables and guest containers</span></span>

<span data-ttu-id="c28f7-133">서비스 패브릭은 'guest' hello 플랫폼의 프로그래밍 모델을 기본 제공 되지 않는 하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-133">A Service Fabric 'guest' is a service that is not built with hello platform's programming models.</span></span> <span data-ttu-id="c28f7-134">게스트에 대 한 hello 바이너리 하거나 패키지 [hello 응용 프로그램 패키지에 직접](service-fabric-deploy-existing-app.md) 또는 [컨테이너 이미지를 통해](service-fabric-deploy-container.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-134">You can package hello binaries for a guest either [directly in hello application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="c28f7-135">두 경우 모두 Visual Studio 만듭니다 hello hello에 필요한 아티팩트 **ApplicationPackageRoot** hello 응용 프로그램 프로젝트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-135">In both cases, Visual Studio creates hello necessary artifacts in hello **ApplicationPackageRoot** folder of hello application project.</span></span> <span data-ttu-id="c28f7-136">Visual Studio hello 코드는 이미 다른 곳에서 존재 하므로 새 서비스 프로젝트가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-136">Visual Studio will not create a new service project because hello code already exists elsewhere.</span></span> <span data-ttu-id="c28f7-137">게스트 hello 서비스 패브릭 응용 프로그램 프로젝트와 함께 프로젝트 toomanage를 원하는 경우 추가할 수 있습니다 toohello 같은 Visual Studio 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-137">If you would like toomanage your guest projects alongside hello Service Fabric application project, you can add them toohello same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c28f7-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c28f7-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="c28f7-139">Azure 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="c28f7-139">Create an Azure cluster</span></span>
<span data-ttu-id="c28f7-140">서비스 패브릭 SDK hello 개발 및 테스트에 대 한 로컬 클러스터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-140">hello Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="c28f7-141">Azure에서 클러스터 toocreate 참조 [hello Azure 포털에서에서 서비스 패브릭 클러스터를 설정할][create-cluster-in-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-141">toocreate a cluster in Azure, see [Setting up a Service Fabric cluster from hello Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-tooazure"></a><span data-ttu-id="c28f7-142">응용 프로그램 tooAzure 게시</span><span class="sxs-lookup"><span data-stu-id="c28f7-142">Publish your application tooAzure</span></span>
<span data-ttu-id="c28f7-143">Visual Studio tooan Azure 클러스터에서 직접 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-143">You can publish your application directly from Visual Studio tooan Azure cluster.</span></span> <span data-ttu-id="c28f7-144">toolearn를 확인 하려면 어떻게 해야 [응용 프로그램 tooAzure 게시][publish-app-to-azure]합니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-144">toolearn how, see [Publishing your application tooAzure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a><span data-ttu-id="c28f7-145">클러스터 서비스 패브릭 탐색기 toovisualize를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-145">Use Service Fabric Explorer toovisualize your cluster</span></span>
<span data-ttu-id="c28f7-146">서비스 패브릭 탐색기 클러스터에 배포 된 응용 프로그램 및 물리적 레이아웃을 포함 하 여 쉽게 toovisualize를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-146">Service Fabric Explorer offers an easy way toovisualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="c28f7-147">toolearn 더 참조 [서비스 패브릭 탐색기를 사용 하 여 클러스터 시각화][visualize-with-sfx]합니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-147">toolearn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="c28f7-148">서비스 버전 관리 및 업그레이드</span><span class="sxs-lookup"><span data-stu-id="c28f7-148">Version and upgrade your services</span></span>
<span data-ttu-id="c28f7-149">서비스 패브릭을 통해 응용 프로그램에서 독립적인 서비스의 버전 관리 및 업그레이드를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="c28f7-150">toolearn 더 참조 [버전 관리 및 서비스 업그레이드][app-upgrade-tutorial]합니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-150">toolearn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="c28f7-151">Visual Studio Team Services를 사용하여 지속적인 통합 구성</span><span class="sxs-lookup"><span data-stu-id="c28f7-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="c28f7-152">toolearn 서비스 패브릭 응용 프로그램에 대 한 연속 통합 프로세스를 설정할 수 있습니다 참조 [Visual Studio Team Services와 연속 통합을 구성][ci-with-vso]합니다.</span><span class="sxs-lookup"><span data-stu-id="c28f7-152">toolearn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
