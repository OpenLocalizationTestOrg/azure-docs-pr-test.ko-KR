---
title: "Azure 서비스 패브릭 CLI를 사용 하 여 aaaManage Azure 서비스 패브릭 응용 프로그램"
description: "Azure 서비스 패브릭 CLI를 사용 하 여 Azure 서비스 패브릭에서 toodeploy 및 제거 하는 응용 프로그램을 클러스터링 하는 방법을 알아봅니다"
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: d9f98cee1d70f71a2aab68ff556956619910e4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a><span data-ttu-id="87c81-103">Azure Service Fabric CLI를 사용하여 Azure Service Fabric 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="87c81-103">Manage an Azure Service Fabric application by using Azure Service Fabric CLI</span></span>

<span data-ttu-id="87c81-104">자세한 내용은 방법 Azure 서비스 패브릭 클러스터에서 실행 되는 toocreate 및 delete 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87c81-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="87c81-105">Prerequisites</span></span>

* <span data-ttu-id="87c81-106">Service Fabric CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-106">Install Service Fabric CLI.</span></span> <span data-ttu-id="87c81-107">그런 다음, Service Fabric 클러스터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="87c81-108">자세한 내용은 [Service Fabric CLI 시작](service-fabric-cli.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87c81-108">For more information, see [Get started with Service Fabric CLI](service-fabric-cli.md).</span></span>

* <span data-ttu-id="87c81-109">서비스 패브릭 응용 프로그램 패키지 준비 toobe를 배포 했습니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="87c81-110">방법에 대 한 자세한 내용은 tooauthor 및 응용 프로그램 패키지에 대해 알아보세요 hello [서비스 패브릭 응용 프로그램 모델](service-fabric-application-model.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="87c81-111">개요</span><span class="sxs-lookup"><span data-stu-id="87c81-111">Overview</span></span>

<span data-ttu-id="87c81-112">toodeploy 새 응용 프로그램을 다음이 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="87c81-113">응용 프로그램 패키지 toohello 서비스 패브릭 이미지 저장소를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="87c81-114">응용 프로그램 유형을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-114">Provision an application type.</span></span>
3. <span data-ttu-id="87c81-115">응용 프로그램을 지정하고 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-115">Specify and create an application.</span></span>
4. <span data-ttu-id="87c81-116">서비스를 지정하고 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-116">Specify and create services.</span></span>

<span data-ttu-id="87c81-117">tooremove 기존 응용 프로그램에 다음이 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="87c81-118">Hello 응용 프로그램을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-118">Delete hello application.</span></span>
2. <span data-ttu-id="87c81-119">해제 hello 응용 프로그램 종류를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="87c81-120">Hello 이미지 저장소 콘텐츠를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="87c81-121">새 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="87c81-121">Deploy a new application</span></span>

<span data-ttu-id="87c81-122">toodeploy 새 응용 프로그램 작업을 수행 하는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="87c81-122">toodeploy a new application, complete hello following tasks:</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="87c81-123">새 응용 프로그램 패키지 toohello 이미지 저장소에 업로드</span><span class="sxs-lookup"><span data-stu-id="87c81-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="87c81-124">응용 프로그램을 만들기 전에 hello 응용 프로그램 패키지 toohello 서비스 패브릭 이미지 저장소를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span>

<span data-ttu-id="87c81-125">예를 들어, 응용 프로그램 패키지 hello에 있으면 `app_package_dir` 디렉터리를 사용 하 여 hello 다음 명령을 tooupload hello 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="87c81-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir
```

<span data-ttu-id="87c81-126">대형 응용 프로그램 패키지에 대 한 hello를 지정할 수 있습니다 `--show-progress` hello 업로드의 toodisplay hello 진행률 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="87c81-127">프로 비전 hello 응용 프로그램 종류</span><span class="sxs-lookup"><span data-stu-id="87c81-127">Provision hello application type</span></span>

<span data-ttu-id="87c81-128">Hello 업로드가 완료 되 면 hello 응용 프로그램을 프로 비전 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="87c81-129">tooprovision hello 응용 프로그램, 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="87c81-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="87c81-130">값에 대 한 hello `application-type-build-path` hello 응용 프로그램 패키지의 업로드 위치 hello 디렉터리 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="87c81-131">응용 프로그램 유형에서 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="87c81-131">Create an application from an application type</span></span>

<span data-ttu-id="87c81-132">Hello 응용 프로그램을 프로 비전 한 후 사용 하 여 hello 다음 tooname 명령 하 고 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="87c81-133">`app-name`hello 응용 프로그램 인스턴스에 대해 toouse 되도록 hello 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="87c81-134">이전에 프로비전된 응용 프로그램 매니페스트에서 추가 매개 변수를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="87c81-135">hello 응용 프로그램 이름은 hello 접두사로 시작 `fabric:/`합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="87c81-136">Hello 새 응용 프로그램에 대 한 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="87c81-136">Create services for hello new application</span></span>

<span data-ttu-id="87c81-137">응용 프로그램을 만든 후 hello 응용 프로그램에서 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="87c81-138">다음 예제는 hello, 응용 프로그램에서 새 상태 비저장 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="87c81-139">응용 프로그램을 만들 수 있는 hello 서비스는 서비스 매니페스트의 hello 이전에 프로 비전 된 응용 프로그램 패키지에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="87c81-140">응용 프로그램 배포 및 상태 확인</span><span class="sxs-lookup"><span data-stu-id="87c81-140">Verify application deployment and health</span></span>

<span data-ttu-id="87c81-141">tooverify 모든 것이 정상 상태 명령을 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-141">tooverify everything is healthy, use hello following health commands:</span></span>

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

<span data-ttu-id="87c81-142">hello 서비스가 정상 임을 tooverify hello 서비스와 응용 프로그램의 유사한 명령 tooretrieve hello 상태를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and the application:</span></span>

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

<span data-ttu-id="87c81-143">정상 서비스 및 응용 프로그램은 `HealthState` 값이 `Ok`입니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="87c81-144">기존 응용 프로그램 제거</span><span class="sxs-lookup"><span data-stu-id="87c81-144">Remove an existing application</span></span>

<span data-ttu-id="87c81-145">tooremove 응용 프로그램 작업을 수행 하는 전체 hello:</span><span class="sxs-lookup"><span data-stu-id="87c81-145">tooremove an application, complete hello following tasks:</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="87c81-146">Hello 응용 프로그램 삭제</span><span class="sxs-lookup"><span data-stu-id="87c81-146">Delete hello application</span></span>

<span data-ttu-id="87c81-147">toodelete hello 응용 프로그램, 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="87c81-147">toodelete hello application, use hello following command:</span></span>

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="87c81-148">응용 프로그램 종류 hello를 프로 비전 해제</span><span class="sxs-lookup"><span data-stu-id="87c81-148">Unprovision hello application type</span></span>

<span data-ttu-id="87c81-149">Hello 응용 프로그램을 삭제 하면 응용 프로그램 종류 hello를 프로 비전 해제 필요 없는 경우 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="87c81-150">toounprovision hello 응용 프로그램 종류, 다음 명령을 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="87c81-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="87c81-151">hello 이름과 hello 이전에 프로 비전 된 응용 프로그램 매니페스트에서 버전 hello 형식 이름 및 형식 버전이 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="87c81-152">Hello 응용 프로그램 패키지를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-152">Delete hello application package</span></span>

<span data-ttu-id="87c81-153">응용 프로그램 종류 hello를 프로 비전 해제가, 후에 필요 없는 경우 hello 이미지 저장소에서 hello 응용 프로그램 패키지를 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="87c81-154">응용 프로그램 패키지를 삭제하면 디스크 공간을 확보하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="87c81-155">다음 명령을 사용 하 여 hello hello 이미지 저장소에서 toodelete hello 응용 프로그램 패키지:</span><span class="sxs-lookup"><span data-stu-id="87c81-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
sfctl store delete --content-path app_package_dir
```

<span data-ttu-id="87c81-156">`content-path`hello 응용 프로그램을 만들 때 업로드 된 hello 디렉터리의 hello 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="upgrade-application"></a><span data-ttu-id="87c81-157">응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="87c81-157">Upgrade application</span></span>

<span data-ttu-id="87c81-158">응용 프로그램을 만든 후 반복할 수 있습니다 hello 단계 tooprovision 응용 프로그램의 두 번째 버전의 동일한 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-158">After creating your application, you can repeat hello same set of steps tooprovision a second version of your application.</span></span> <span data-ttu-id="87c81-159">그런 다음 서비스 패브릭 응용 프로그램 업그레이드로 toorunning hello hello 응용 프로그램의 두 번째 버전을 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-159">Then, with a Service Fabric application upgrade you can transition toorunning hello second version of hello application.</span></span> <span data-ttu-id="87c81-160">자세한 내용은 hello 설명서를 참조 [서비스 패브릭 응용 프로그램 업그레이드](service-fabric-application-upgrade.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-160">For more information, see hello documentation on [Service Fabric application upgrades](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="87c81-161">tooperform 업그레이드 하는 첫 번째 프로 비전 hello 다음 버전의 응용 프로그램 사용 하 여 hello는 이전과 동일한 명령을 hello:</span><span class="sxs-lookup"><span data-stu-id="87c81-161">tooperform an upgrade, first provision hello next version of hello application using hello same commands as before:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

<span data-ttu-id="87c81-162">한 후 모니터링 되는 자동 업그레이드를 tooperform hello 다음 명령을 실행 하 여 hello 업그레이드를 시작 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-162">It is recommended then tooperform a monitored automatic upgrade, launch hello upgrade by running hello following command:</span></span>

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

<span data-ttu-id="87c81-163">업그레이드를 수행하면 지정된 설정으로 기존 매개 변수가 재정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-163">Upgrades override existing parameters with whatever set is specified.</span></span> <span data-ttu-id="87c81-164">필요한 경우 응용 프로그램 매개 변수를 인수 toohello 업그레이드 명령으로 전달 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-164">Application parameters should be passed as arguments toohello upgrade command, if necessary.</span></span> <span data-ttu-id="87c81-165">응용 프로그램 매개 변수는 JSON 개체로 암호화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-165">Application parameters should be encoded as a JSON object.</span></span>

<span data-ttu-id="87c81-166">hello를 사용할 수 있습니다, tooretrieve 매개 변수가 이전에 지정한 `sfctl application info` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-166">tooretrieve any parameters previously specified, you can use hello `sfctl application info` command.</span></span>

<span data-ttu-id="87c81-167">Hello 상태를 사용 하 여 검색할 수는 응용 프로그램 업그레이드가 진행에서 되 면 하는 경우는 `sfctl application upgrade-status` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-167">When an application upgrade is in progress, hello status can be retrieved using the `sfctl application upgrade-status` command.</span></span>

<span data-ttu-id="87c81-168">마지막으로, 업그레이드 하는 진행 중인 취소 toobe 필요한 경우 사용할 수 있습니다 hello `sfctl application upgrade-rollback` tooroll 다시 hello 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="87c81-168">Finally, if an upgrade is in progress and needs toobe canceled, you can use hello `sfctl application upgrade-rollback` tooroll back hello upgrade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87c81-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="87c81-169">Next steps</span></span>

* [<span data-ttu-id="87c81-170">Service Fabric CLI 기본 사항</span><span class="sxs-lookup"><span data-stu-id="87c81-170">Service Fabric CLI basics</span></span>](service-fabric-cli.md)
* [<span data-ttu-id="87c81-171">Linux에서 Service Fabric 시작</span><span class="sxs-lookup"><span data-stu-id="87c81-171">Getting started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="87c81-172">Service Fabric 응용 프로그램 업그레이드 시작</span><span class="sxs-lookup"><span data-stu-id="87c81-172">Launching a Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
