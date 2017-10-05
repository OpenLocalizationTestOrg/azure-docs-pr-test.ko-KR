---
title: "Service Fabric 프로젝트 만들기 다음 단계 | Microsoft Docs"
description: "이 문서에는 서비스 패브릭에 대한 핵심 개발 작업 집합에 대한 링크가 포함되어있습니다."
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
ms.openlocfilehash: 74019850c507902d9ef7ec47a364fff234aaf32b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="c3f3a-103">서비스 패브릭 응용 프로그램 및 다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3f3a-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="c3f3a-104">Azure 서비스 패브릭 응용 프로그램이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="c3f3a-105">이 문서에서는 프로젝트와 몇 가지 잠재적인 다음 단계의 구성에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-105">This article describes the makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="c3f3a-106">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="c3f3a-106">Your application</span></span>
<span data-ttu-id="c3f3a-107">모든 새 응용 프로그램에는 응용 프로그램 프로젝트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-107">Every new application includes an application project.</span></span> <span data-ttu-id="c3f3a-108">선택한 서비스의 형식에 따라 하나 또는 두 개의 추가 프로젝트가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-108">There may be one or two additional projects, depending on the type of service chosen.</span></span>

### <a name="the-application-project"></a><span data-ttu-id="c3f3a-109">응용 프로그램 프로젝트</span><span class="sxs-lookup"><span data-stu-id="c3f3a-109">The application project</span></span>
<span data-ttu-id="c3f3a-110">응용 프로그램 프로젝트는 다음으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-110">The application project consists of:</span></span>

* <span data-ttu-id="c3f3a-111">응용 프로그램을 구성하는 서비스에 대한 참조 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-111">A set of references to the services that make up your application.</span></span>
* <span data-ttu-id="c3f3a-112">클러스터 끝점과 관련된 기본 설정과 같은 다른 환경에서의 작업에 대한 기본 설정과 기본적으로 업그레이드 배포를 수행하는 여부 사항을 유지하는 데 사용할 수 있는 세 개의 게시 프로필(1-노드 로컬, 5-노드 로컬 및 클라우드)입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use to maintain preferences for working with different environments--such as preferences related to a cluster endpoint and whether to perform upgrade deployments by default.</span></span>
* <span data-ttu-id="c3f3a-113">서비스에 대해 만들려는 파티션 수와 같은 환경 관련 응용 프로그램 구성을 유지하는 데 사용할 수 있는 세 개의 응용 프로그램 매개 변수 파일(위와 동일)입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-113">Three application parameter files (same as above) that you can use to maintain environment-specific application configurations, such as the number of partitions to create for a service.</span></span>
* <span data-ttu-id="c3f3a-114">응용 프로그램을 명령줄에서 배포하거나 자동화된 연속 통합 및 배포 파이프라인의 일부로 배포하는 경우에 사용할 수 있는 배포 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-114">A deployment script that you can use to deploy your application from the command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="c3f3a-115">응용 프로그램을 설명하는 응용 프로그램 매니페스트입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-115">The application manifest, which describes the application.</span></span> <span data-ttu-id="c3f3a-116">ApplicationPackageRoot 폴더에서 매니페스트를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-116">You can find the manifest under the ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="c3f3a-117">상태 비저장 서비스</span><span class="sxs-lookup"><span data-stu-id="c3f3a-117">Stateless service</span></span>
<span data-ttu-id="c3f3a-118">새 상태 비저장 서비스를 추가하면 Visual Studio는 서비스 프로젝트를 `StatelessService`에서 나온 형식을 포함하는 솔루션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-118">When you add a new stateless service, Visual Studio adds a service project to your solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="c3f3a-119">서비스는 카운터의 로컬 변수를 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-119">The service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="c3f3a-120">상태 저장 서비스</span><span class="sxs-lookup"><span data-stu-id="c3f3a-120">Stateful service</span></span>
<span data-ttu-id="c3f3a-121">새 상태 저장 서비스를 추가하면 Visual Studio는 서비스 프로젝트를 `StatefulService`에서 나온 형식을 포함하는 솔루션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-121">When you add a new stateful service, Visual Studio adds a service project to your solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="c3f3a-122">서비스는 `RunAsync` 메서드의 카운터를 증가시키고 그 결과를 `ReliableDictionary`에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-122">The service increments a counter in its `RunAsync` method and stores the result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="c3f3a-123">행위자 서비스</span><span class="sxs-lookup"><span data-stu-id="c3f3a-123">Actor service</span></span>
<span data-ttu-id="c3f3a-124">새 Reliable Actor를 추가하는 경우 Visual Studio가 두 개의 프로젝트, 즉 행위자 프로젝트와 인터페이스 프로젝트를 솔루션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-124">When you add a new reliable actor, Visual Studio adds two projects to your solution: an actor project and an interface project.</span></span>

<span data-ttu-id="c3f3a-125">행위자 프로젝트는 행위자의 상태 내에서 안정적으로 유지되는 카운터의 값을 설정하고 가져오는 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-125">The actor project provides methods for setting and getting the value of a counter that is reliably persisted within the actor's state.</span></span> <span data-ttu-id="c3f3a-126">인터페이스 프로젝트는 다른 서비스가 행위자를 호출하는 데 사용할 수 있는 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-126">The interface project provides an interface that other services can use to invoke the actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="c3f3a-127">상태 비저장 웹 API</span><span class="sxs-lookup"><span data-stu-id="c3f3a-127">Stateless Web API</span></span>
<span data-ttu-id="c3f3a-128">상태 비저장 웹 API 프로젝트는 응용 프로그램을 외부 클라이언트에 공개하는 데 사용할 수 있는 기본 웹 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-128">The stateless Web API project provides a basic web service that you can use to open your application to external clients.</span></span> <span data-ttu-id="c3f3a-129">프로젝트 구성 방법에 대한 자세한 내용은 [OWIN 자체 호스팅을 포함한 서비스 패브릭 웹 API 서비스](service-fabric-reliable-services-communication-webapi.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-129">For more information about how the project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="c3f3a-130">ASP.NET core</span><span class="sxs-lookup"><span data-stu-id="c3f3a-130">ASP.NET core</span></span>
<span data-ttu-id="c3f3a-131">Service Fabric SDK는 독립 실행형 ASP.NET 코어 프로젝트에 사용할 수 있는 ASP.NET 코어 템플릿의 동일한 집합(비어 있음, [웹 API][aspnet-webapi] 및 [웹 응용 프로그램][aspnet-webapp])을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-131">The Service Fabric SDK provides the same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="c3f3a-132">게스트 실행 파일 및 게스트 컨테이너</span><span class="sxs-lookup"><span data-stu-id="c3f3a-132">Guest executables and guest containers</span></span>

<span data-ttu-id="c3f3a-133">Service Fabric 'guest'는 플랫폼의 프로그래밍 모델로 구축되지 않은 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-133">A Service Fabric 'guest' is a service that is not built with the platform's programming models.</span></span> <span data-ttu-id="c3f3a-134">게스트에 대한 이진 파일을 [응용 프로그램 패키지에 직접](service-fabric-deploy-existing-app.md) 또는 [컨테이너 이미지를 통해](service-fabric-deploy-container.md) 패키지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-134">You can package the binaries for a guest either [directly in the application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="c3f3a-135">두 경우 모두 Visual Studio에서 응용 프로그램 프로젝트의 **ApplicationPackageRoot** 폴더에 필요한 아티팩트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-135">In both cases, Visual Studio creates the necessary artifacts in the **ApplicationPackageRoot** folder of the application project.</span></span> <span data-ttu-id="c3f3a-136">Visual Studio는 해당 코드가 다른 위치에 이미 있으므로 새 서비스 프로젝트를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-136">Visual Studio will not create a new service project because the code already exists elsewhere.</span></span> <span data-ttu-id="c3f3a-137">Service Fabric 응용 프로그램 프로젝트와 함께 게스트 프로젝트를 관리하려는 경우 동일한 Visual Studio 솔루션에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-137">If you would like to manage your guest projects alongside the Service Fabric application project, you can add them to the same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3f3a-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3f3a-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="c3f3a-139">Azure 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="c3f3a-139">Create an Azure cluster</span></span>
<span data-ttu-id="c3f3a-140">서비스 패브릭 SDK는 개발 및 테스트를 위한 로컬 클러스터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-140">The Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="c3f3a-141">Azure에서 클러스터를 만들려면 [Azure Portal에서 Service Fabric 클러스터 설정][create-cluster-in-portal]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-141">To create a cluster in Azure, see [Setting up a Service Fabric cluster from the Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-to-azure"></a><span data-ttu-id="c3f3a-142">Azure에 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="c3f3a-142">Publish your application to Azure</span></span>
<span data-ttu-id="c3f3a-143">Visual Studio에서 Azure 클러스터로 직접 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-143">You can publish your application directly from Visual Studio to an Azure cluster.</span></span> <span data-ttu-id="c3f3a-144">방법을 알아보려면 [Azure에 응용 프로그램 게시][publish-app-to-azure]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-144">To learn how, see [Publishing your application to Azure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-to-visualize-your-cluster"></a><span data-ttu-id="c3f3a-145">서비스 패브릭 탐색기를 사용하여 클러스터 시각화</span><span class="sxs-lookup"><span data-stu-id="c3f3a-145">Use Service Fabric Explorer to visualize your cluster</span></span>
<span data-ttu-id="c3f3a-146">서비스 패브릭 탐색기는 배포된 응용 프로그램 및 물리적 레이아웃을 포함하여 클러스터를 쉽게 시각화할 수 있는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-146">Service Fabric Explorer offers an easy way to visualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="c3f3a-147">자세한 내용은 [Service Fabric Explorer를 사용하여 클러스터 시각화][visualize-with-sfx]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-147">To learn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="c3f3a-148">서비스 버전 관리 및 업그레이드</span><span class="sxs-lookup"><span data-stu-id="c3f3a-148">Version and upgrade your services</span></span>
<span data-ttu-id="c3f3a-149">서비스 패브릭을 통해 응용 프로그램에서 독립적인 서비스의 버전 관리 및 업그레이드를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="c3f3a-150">자세한 내용은 [서비스 버전 관리 및 업그레이드][app-upgrade-tutorial]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-150">To learn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="c3f3a-151">Visual Studio Team Services를 사용하여 지속적인 통합 구성</span><span class="sxs-lookup"><span data-stu-id="c3f3a-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="c3f3a-152">Service Fabric 응용 프로그램에 대해 지속적인 통합 프로세스를 설정할 수 있는 방법을 알아보려면 [Visual Studio Team Services를 사용하여 지속적인 통합 구성][ci-with-vso]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f3a-152">To learn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

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
