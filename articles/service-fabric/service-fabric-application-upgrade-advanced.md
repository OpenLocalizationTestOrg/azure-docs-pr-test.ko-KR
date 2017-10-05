---
title: "고급 응용 프로그램 업그레이드 항목 | Microsoft Docs"
description: "이 문서에서는 서비스 패브릭 응용 프로그램 업그레이드와 관련된 고급 항목을 다룹니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: 8d3b922f3d50b645ac9db2cc879a319df1262e0a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a><span data-ttu-id="83442-103">서비스 패브릭 응용 프로그램 업그레이드: 고급 항목</span><span class="sxs-lookup"><span data-stu-id="83442-103">Service Fabric application upgrade: advanced topics</span></span>
## <a name="adding-or-removing-services-during-an-application-upgrade"></a><span data-ttu-id="83442-104">응용 프로그램을 업그레이드하는 동안 서비스 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="83442-104">Adding or removing services during an application upgrade</span></span>
<span data-ttu-id="83442-105">새 서비스가 이미 배포된 응용 프로그램에 추가되고 업그레이드로 게시되면 새 서비스는 배포된 응용 프로그램에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="83442-105">If a new service is added to an application that is already deployed, and published as an upgrade, the new service is added to the deployed application.</span></span>  <span data-ttu-id="83442-106">이러한 업그레이드는 응용 프로그램에 이미 속하는 서비스에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="83442-106">Such an upgrade does not affect any of the services that were already part of the application.</span></span> <span data-ttu-id="83442-107">하지만 새 서비스가 활성화(`New-ServiceFabricService` cmdlet 사용)되려면 추가된 서비스 인스턴스가 시작되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-107">However, an instance of the service that was added must be started for the new service to be active (using the `New-ServiceFabricService` cmdlet).</span></span>

<span data-ttu-id="83442-108">업그레이드의 일부로 응용 프로그램에서 서비스를 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83442-108">Services can also be removed from an application as part of an upgrade.</span></span> <span data-ttu-id="83442-109">그러나 업그레이드를 계속하기 전에 삭제하려는 서비스의 모든 현재 인스턴스를 중지해야 합니다(`Remove-ServiceFabricService` cmdlet 사용).</span><span class="sxs-lookup"><span data-stu-id="83442-109">However, all current instances of the to-be-deleted service must be stopped before proceeding with the upgrade (using the `Remove-ServiceFabricService` cmdlet).</span></span>

## <a name="manual-upgrade-mode"></a><span data-ttu-id="83442-110">수동 업그레이드 모드</span><span class="sxs-lookup"><span data-stu-id="83442-110">Manual upgrade mode</span></span>
> [!NOTE]
> <span data-ttu-id="83442-111">모니터링되지 않는 수동 모드는 업그레이드가 실패 또는 일시 중단된 경우에만 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-111">The unmonitored manual mode should be considered only for a failed or suspended upgrade.</span></span> <span data-ttu-id="83442-112">서비스 패브릭 응용 프로그램에 권장되는 업그레이드 모드는 모니터링 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="83442-112">The monitored mode is the recommended upgrade mode for Service Fabric applications.</span></span>
>
>

<span data-ttu-id="83442-113">Azure 서비스 패브릭은 개발 및 프로덕션 클러스터를 지원하는 여러 업그레이드 모드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-113">Azure Service Fabric provides multiple upgrade modes to support development and production clusters.</span></span> <span data-ttu-id="83442-114">선택한 배포 옵션은 환경마다 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83442-114">Deployment options chosen may be different for different environments.</span></span>

<span data-ttu-id="83442-115">모니터링되는 롤링 응용 프로그램 업그레이드는 프로덕션 환경에서 가장 많이 사용되는 업그레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="83442-115">The monitored rolling application upgrade is the most typical upgrade to use in the production environment.</span></span> <span data-ttu-id="83442-116">업그레이드 정책이 지정되면 서비스 패브릭에서는 응용 프로그램이 정상인지 확인한 후 업그레이드를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-116">When the upgrade policy is specified, Service Fabric ensures that the application is healthy before the upgrade proceeds.</span></span>

 <span data-ttu-id="83442-117">응용 프로그램 관리자는 수동 롤링 응용 프로그램 업그레이드 모드를 사용하여 여러 업그레이드 도메인의 모든 업그레이드 진행 상황을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83442-117">The application administrator can use the manual rolling application upgrade mode to have total control over the upgrade progress through the various upgrade domains.</span></span> <span data-ttu-id="83442-118">이 모드는 응용 프로그램의 데이터가 이미 손실된 경우처럼 사용자 지정 또는 복잡한 상태 평가 정책이 필요하거나 일반적이지 않은 업그레이드가 수행될 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, the application is already in data loss).</span></span>

<span data-ttu-id="83442-119">마지막으로 자동화된 롤링 응용 프로그램 업그레이드는 서비스를 개발하는 동안 개발 또는 테스트 환경에서 빠른 반복 주기를 제공하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-119">Finally, the automated rolling application upgrade is useful for development or testing environments to provide a fast iteration cycle during service development.</span></span>

## <a name="change-to-manual-upgrade-mode"></a><span data-ttu-id="83442-120">수동 업그레이드 모드로 변경</span><span class="sxs-lookup"><span data-stu-id="83442-120">Change to manual upgrade mode</span></span>
<span data-ttu-id="83442-121">**수동**--현재 UD에서 응용 프로그램 업그레이드를 중지하고 업그레이드 모드를 모니터링되지 않은 수동 모드로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-121">**Manual**--Stop the application upgrade at the current UD and change the upgrade mode to Unmonitored Manual.</span></span> <span data-ttu-id="83442-122">관리자가 수동으로 **MoveNextApplicationUpgradeDomainAsync** 를 호출하고 새 업그레이드를 초기화하여 업그레이드를 진행하거나 롤백을 트리거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-122">The administrator needs to manually call **MoveNextApplicationUpgradeDomainAsync** to proceed with the upgrade or trigger a rollback by initiating a new upgrade.</span></span> <span data-ttu-id="83442-123">업그레이드가 수동 모드로 전환되면 새 업그레이드가 초기화될 때까지 수동 모드가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="83442-123">Once the upgrade enters into the Manual mode, it stays in the Manual mode until a new upgrade is initiated.</span></span> <span data-ttu-id="83442-124">**GetApplicationUpgradeProgressAsync** 명령은 FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-124">The **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span></span>

## <a name="upgrade-with-a-diff-package"></a><span data-ttu-id="83442-125">diff 패키지로 업그레이드</span><span class="sxs-lookup"><span data-stu-id="83442-125">Upgrade with a diff package</span></span>
<span data-ttu-id="83442-126">완전한 자체 포함 응용 프로그램 패키지로 프로비전하여 서비스 패브릭 응용 프로그램을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83442-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span></span> <span data-ttu-id="83442-127">또한 업데이트된 응용 프로그램 파일과 업데이트된 응용 프로그램 매니페스트 및 서비스 매니페스트 파일만 포함하는 diff 패키지를 사용하여 응용 프로그램을 업그레이드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83442-127">An application can also be upgraded by using a diff package that contains only the updated application files, the updated application manifest, and the service manifest files.</span></span>

<span data-ttu-id="83442-128">전체 응용 프로그램 패키지에는 서비스 패브릭 응용 프로그램을 시작 및 실행하는 데 필요한 모든 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83442-128">A full application package contains all the files necessary to start and run a Service Fabric application.</span></span> <span data-ttu-id="83442-129">diff 패키지는 마지막 프로비전과 현재 업그레이드 사이에 변경된 파일과 전체 응용 프로그램 매니페스트 및 서비스 매니페스트 파일만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-129">A diff package contains only the files that changed between the last provision and the current upgrade, plus the full application manifest and the service manifest files.</span></span> <span data-ttu-id="83442-130">빌드 레이아웃에서 찾을 수 없는 응용 프로그램 매니페스트 또는 서비스 매니페스트의 모든 참조는 이미지 저장소에서 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="83442-130">Any reference in the application manifest or service manifest that can't be found in the build layout is searched for in the image store.</span></span>

<span data-ttu-id="83442-131">전체 응용 프로그램 패키지는 클러스터에 응용 프로그램을 처음으로 설치할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-131">Full application packages are required for the first installation of an application to the cluster.</span></span> <span data-ttu-id="83442-132">후속 업데이트는 전체 응용 프로그램 패키지도 가능하고 diff 패키지도 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-132">Subsequent updates can be either a full application package or a diff package.</span></span>

<span data-ttu-id="83442-133">다음과 같은 경우에는 diff 패키지를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="83442-133">Occasions when using a diff package would be a good choice:</span></span>

* <span data-ttu-id="83442-134">여러 서비스 매니페스트 파일 및/또는 여러 코드 패키지, config 패키지 또는 데이터 패키지를 참조하는 대형 응용 프로그램 패키지가 있는 경우에는 diff 패키지가 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="83442-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span></span>
* <span data-ttu-id="83442-135">응용 프로그램 빌드 프로세스에서 직접 빌드 레이아웃을 생성하는 배포 시스템을 사용하는 경우에는 diff 패키지가 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="83442-135">A diff package is preferred when you have a deployment system that generates the build layout directly from your application build process.</span></span> <span data-ttu-id="83442-136">이 경우 코드가 변경되지 않았더라도 새로 빌드된 어셈블리는 다른 체크섬을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="83442-136">In this case, even though the code hasn't changed, newly built assemblies get a different checksum.</span></span> <span data-ttu-id="83442-137">전체 응용 프로그램 패키지를 사용하려면 모든 코드 패키지의 버전을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-137">Using a full application package would require you to update the version on all code packages.</span></span> <span data-ttu-id="83442-138">diff 패키지를 사용하면 변경된 파일과 버전이 변경된 매니페스트 파일만 제공하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83442-138">Using a diff package, you only provide the files that changed and the manifest files where the version has changed.</span></span>

<span data-ttu-id="83442-139">Visual Studio를 사용하여 응용 프로그램이 업그레이드되는 경우 diff 패키지가 자동으로 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="83442-139">When an application is upgraded using Visual Studio, the diff package is published automatically.</span></span> <span data-ttu-id="83442-140">diff 패키지를 수동으로 만들려면 응용 프로그램 매니페스트 및 서비스 매니페스트를 업데이트해야 하지만 변경된 패키지만 최종 응용 프로그램 패키지에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-140">To create a diff package manually, the application manifest, and the service manifests must be updated, but only the changed packages should be included in the final application package.</span></span>

<span data-ttu-id="83442-141">예를 들어 다음 응용 프로그램을 시작하겠습니다(이해하기 쉽도록 버전 번호 제공).</span><span class="sxs-lookup"><span data-stu-id="83442-141">For example, let's start with the following application (version numbers provided for ease of understanding):</span></span>

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="83442-142">이제 PowerShell을 사용하여 diff 패키지로 service1의 코드 패키지만 업데이트하려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="83442-142">Now, let's assume you wanted to update only the code package of service1 using a diff package using PowerShell.</span></span> <span data-ttu-id="83442-143">이제 업데이트된 응용 프로그램은 다음과 같은 폴더 구조를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="83442-143">Now, your updated application has the following folder structure:</span></span>

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="83442-144">이 경우 응용 프로그램 매니페스트를 2.0.0으로 업데이트하고 service1에 대한 서비스 매니페스트가 코드 패키지 업데이트를 반영하도록 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-144">In this case, you update the application manifest to 2.0.0, and the service manifest for service1 to reflect the code package update.</span></span> <span data-ttu-id="83442-145">응용 프로그램 패키지에 대한 폴더 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="83442-145">The folder for your application package would have the following structure:</span></span>

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a><span data-ttu-id="83442-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="83442-146">Next steps</span></span>
<span data-ttu-id="83442-147">[Visual Studio를 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial.md) 에서는 Visual Studio를 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="83442-148">[Powershell을 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial-powershell.md) 에서는 PowerShell을 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="83442-149">[업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md)를 사용하여 응용 프로그램 업그레이드 방법을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="83442-150">[데이터 직렬화](service-fabric-application-upgrade-data-serialization.md)사용 방법을 익혀 응용 프로그램 업그레이드와 호환되도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="83442-150">Make your application upgrades compatible by learning how to use [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="83442-151">[응용 프로그램 업그레이드 문제 해결](service-fabric-application-upgrade-troubleshooting.md)의 단계를 참조하여 응용 프로그램 업그레이드 중 발생하는 일반적인 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="83442-151">Fix common problems in application upgrades by referring to the steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
