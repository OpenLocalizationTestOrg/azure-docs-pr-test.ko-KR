---
title: "Azure Service Fabric Docker Compose 미리 보기"
description: "Azure Service Fabric은 Service Fabric을 사용하여 기존 컨테이너를 보다 쉽게 조정할 수 있도록 Docker Compose 형식을 수락합니다. 이 지원은 현재 미리 보기로 제공되고 있습니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e05d1a3d6111e3bbc34008226bcd1fdf35935450
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="0f7d5-104">Azure Service Fabric의 Docker Compose 응용 프로그램 지원(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="0f7d5-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="0f7d5-105">Docker는 다중 컨테이너 응용 프로그램을 정의하기 위해 [docker-compose.yml](https://docs.docker.com/compose) 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-105">Docker uses the [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="0f7d5-106">Docker에 익숙한 고객이 Azure Service Fabric에서 기존 컨테이너 응용 프로그램을 쉽게 조정하도록 하기 위해 플랫폼에 기본적으로 Docker Compose에 대한 미리 보기 지원을 포함했습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-106">To make it easy for customers familiar with Docker to orchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in the platform.</span></span> <span data-ttu-id="0f7d5-107">Service Fabric은 `docker-compose.yml` 파일의 버전 3 이상을 수락할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="0f7d5-108">이 지원은 미리 보기로 제공되므로 Compose 지시문의 하위 집합만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="0f7d5-109">예를 들어 응용 프로그램 업그레이드는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="0f7d5-110">그러나 응용 프로그램을 업그레이드하는 대신 항상 제거한 후 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="0f7d5-111">이 미리 보기를 사용하려면 해당하는 SDK와 함께 Azure Portal을 통해 Service Fabric 런타임 버전 5.7 이상을 사용하여 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-111">To use this preview, create your cluster with version 5.7 or greater of the Service Fabric runtime through the Azure portal along with the corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="0f7d5-112">이 기능은 미리 보기로 제공되며 프로덕션에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="0f7d5-113">Service Fabric에서 Docker Compose 파일 배포</span><span class="sxs-lookup"><span data-stu-id="0f7d5-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="0f7d5-114">다음 명령은 다른 Service Fabric 응용 프로그램과 유사하게 모니터링하고 관리할 수 있는 Service Fabric 응용 프로그램(이전 예제의 `fabric:/TestContainerApp`)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-114">The following commands create a Service Fabric application (named `fabric:/TestContainerApp` in the preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="0f7d5-115">상태 쿼리에 대해서는 지정된 응용 프로그램 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-115">You can use the specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="0f7d5-116">PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="0f7d5-116">Use PowerShell</span></span>

<span data-ttu-id="0f7d5-117">PowerShell에서 다음 명령을 실행하여 docker-compose.yml 파일에서 Service Fabric Compose 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-117">Create a Service Fabric Compose application from a docker-compose.yml file by running the following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="0f7d5-118">`RegistryUserName` 및 `RegistryPassword`는 컨테이너 레지스트리 사용자 이름 및 암호를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-118">`RegistryUserName` and `RegistryPassword` refer to the container registry username and password.</span></span> <span data-ttu-id="0f7d5-119">응용 프로그램을 완료한 후에는 다음 명령을 사용하여 그 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-119">After you've completed the application, you can check its status by using the following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="0f7d5-120">PowerShell을 통해 Compose 응용 프로그램을 삭제하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-120">To delete the Compose application through PowerShell, use the following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="0f7d5-121">Azure Service Fabric CLI(sfctl) 사용</span><span class="sxs-lookup"><span data-stu-id="0f7d5-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="0f7d5-122">또는 다음 Service Fabric CLI 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-122">Alternatively, you can use the following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="0f7d5-123">응용 프로그램을 만든 후에는 다음 명령을 사용하여 그 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-123">After you've created the application, you can check its status by using the following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="0f7d5-124">Compose 응용 프로그램을 삭제하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-124">To delete the Compose application, use the following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="0f7d5-125">지원되는 Compose 지시문</span><span class="sxs-lookup"><span data-stu-id="0f7d5-125">Supported Compose directives</span></span>

<span data-ttu-id="0f7d5-126">이 미리 보기에서는 다음과 같은 기본 형식을 포함하여 Compose 버전 3형식의 구성 옵션 하위 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-126">This preview supports a subset of the configuration options from the Compose version 3 format, including the following primitives:</span></span>

* <span data-ttu-id="0f7d5-127">서비스 > 배포 > 복제본</span><span class="sxs-lookup"><span data-stu-id="0f7d5-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="0f7d5-128">서비스 > 배포 > 배치 > 제약 조건</span><span class="sxs-lookup"><span data-stu-id="0f7d5-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="0f7d5-129">서비스 > 배포 > 리소스 > 제한</span><span class="sxs-lookup"><span data-stu-id="0f7d5-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="0f7d5-130">-cpu-shares</span><span class="sxs-lookup"><span data-stu-id="0f7d5-130">-cpu-shares</span></span>
    * <span data-ttu-id="0f7d5-131">-memory</span><span class="sxs-lookup"><span data-stu-id="0f7d5-131">-memory</span></span>
    * <span data-ttu-id="0f7d5-132">-memory-swap</span><span class="sxs-lookup"><span data-stu-id="0f7d5-132">-memory-swap</span></span>
* <span data-ttu-id="0f7d5-133">서비스 > 명령</span><span class="sxs-lookup"><span data-stu-id="0f7d5-133">Services > Commands</span></span>
* <span data-ttu-id="0f7d5-134">서비스 > 환경</span><span class="sxs-lookup"><span data-stu-id="0f7d5-134">Services > Environment</span></span>
* <span data-ttu-id="0f7d5-135">서비스 > 포트</span><span class="sxs-lookup"><span data-stu-id="0f7d5-135">Services > Ports</span></span>
* <span data-ttu-id="0f7d5-136">서비스 > 이미지</span><span class="sxs-lookup"><span data-stu-id="0f7d5-136">Services > Image</span></span>
* <span data-ttu-id="0f7d5-137">서비스 > 격리(Windows에만 해당)</span><span class="sxs-lookup"><span data-stu-id="0f7d5-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="0f7d5-138">서비스 > 로깅 > 드라이버</span><span class="sxs-lookup"><span data-stu-id="0f7d5-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="0f7d5-139">서비스 > 로깅 > 드라이버 > 옵션</span><span class="sxs-lookup"><span data-stu-id="0f7d5-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="0f7d5-140">볼륨 및 배포 > 볼륨</span><span class="sxs-lookup"><span data-stu-id="0f7d5-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="0f7d5-141">클러스터는 [Service Fabric 리소스 관리](service-fabric-resource-governance.md)에 설명된 대로 리소스 제한을 적용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-141">Set up the cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="0f7d5-142">다른 모든 Docker Compose 지시문은 이 미리 보기에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="0f7d5-143">ServiceDnsName 계산</span><span class="sxs-lookup"><span data-stu-id="0f7d5-143">ServiceDnsName computation</span></span>

<span data-ttu-id="0f7d5-144">Compose 파일에 지정하는 서비스 이름이 정규화된 도메인 이름(즉, 마침표 [.] 포함)인 경우 Service Fabric에서 등록된 DNS 이름은 `<ServiceName>`(마침표 포함)입니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-144">If the service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), the DNS name registered by Service Fabric is `<ServiceName>` (including the dot).</span></span> <span data-ttu-id="0f7d5-145">정규화된 도메인 이름이 아닌 경우 응용 프로그램 이름의 각 경로 세그먼트는 서비스 DNS 이름의 도메인 레이블이 됩니다. 이때 첫 번째 경로 세그먼트가 최상위 도메인 레이블이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-145">If not, each path segment in the application name becomes a domain label in the service DNS name, with the first path segment becoming the top-level domain label.</span></span>

<span data-ttu-id="0f7d5-146">예를 들어 지정된 응용 프로그램 이름이 `fabric:/SampleApp/MyComposeApp`인 경우 `<ServiceName>.MyComposeApp.SampleApp`은 등록된 DNS 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-146">For example, if the specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be the registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="0f7d5-147">Compose(인스턴스 정의) 및 Service Fabric 응용 프로그램 모델(형식 정의) 간 차이</span><span class="sxs-lookup"><span data-stu-id="0f7d5-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="0f7d5-148">docker-compose.yml 파일은 해당 속성 및 구성을 포함하는 컨테이너의 배포 가능 집합을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="0f7d5-149">예를 들어 파일에는 환경 변수 및 포트가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-149">For example, the file can contain environment variables and ports.</span></span> <span data-ttu-id="0f7d5-150">배치 제약 조건, 리소스 제한, DNS 이름과 같은 배포 매개 변수는 docker-compose.yml 파일에도 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in the docker-compose.yml file.</span></span>

<span data-ttu-id="0f7d5-151">[Service Fabric 응용 프로그램 모델](service-fabric-application-model.md)은 서비스 형식 및 응용 프로그램 형식을 사용합니다. 여기서 동일한 형식의 여러 응용 프로그램 인스턴스를 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-151">The [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of the same type.</span></span> <span data-ttu-id="0f7d5-152">예를 들어 고객이 각자 하나의 응용 프로그램 인스턴스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="0f7d5-153">이 형식 기반 모델은 런타임에 등록된 동일한 응용 프로그램 유형의 여러 버전을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-153">This type-based model supports multiple versions of the same application type that's registered with the runtime.</span></span>

<span data-ttu-id="0f7d5-154">예를 들어 고객 A에는 1.0 형식의 AppTypeA로 인스턴스화된 응용 프로그램이 있고, 고객 B에는 동일한 형식 및 버전으로 인스턴스화된 다른 응용 프로그램을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with the same type and version.</span></span> <span data-ttu-id="0f7d5-155">응용 프로그램 유형은 응용 프로그램 매니페스트에서 정의하고, 응용 프로그램 이름 및 배포 매개 변수는 응용 프로그램을 만들 때 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-155">You define the application types in the application manifests, and you specify the application name and deployment parameters when you create the application.</span></span>

<span data-ttu-id="0f7d5-156">이 모델을 사용하면 유연하게 작업할 수 있지만 매니페스트 파일에서 형식이 암시되는 좀 더 간단한 인스턴스 기반 모델을 지원하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-156">Although this model offers flexibility, we are also planning to support a simpler, instance-based deployment model where types are implicit from the manifest file.</span></span> <span data-ttu-id="0f7d5-157">이 모델에서 각 응용 프로그램은 자체의 독립적인 매니페스트를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="0f7d5-158">인스턴스 기반 배포 형식인 docker-compose.yml에 대한 지원을 추가하여 이러한 방식을 미리 검토하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f7d5-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f7d5-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f7d5-159">Next steps</span></span>

* <span data-ttu-id="0f7d5-160">[Service Fabric 응용 프로그램 모델](service-fabric-application-model.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="0f7d5-160">Read up on the [Service Fabric application model](service-fabric-application-model.md)</span></span>
* [<span data-ttu-id="0f7d5-161">Service Fabric CLI 시작</span><span class="sxs-lookup"><span data-stu-id="0f7d5-161">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)
