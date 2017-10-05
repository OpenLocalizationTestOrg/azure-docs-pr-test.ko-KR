---
title: "Azure CLI 2.0을 사용하여 Azure Service Fabric 응용 프로그램 관리"
description: "Azure CLI 2.0을 사용하여 Azure Service Fabric 클러스터에서 응용 프로그램을 배포하고 제거하는 방법을 알아봅니다."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: 5728339236e3819b301e428f9d7a8add08f02b3e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="4d937-103">Azure CLI 2.0을 사용하여 Azure Service Fabric 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="4d937-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="4d937-104">Azure Service Fabric 클러스터에서 실행 중인 응용 프로그램을 만들고 삭제하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-104">Learn how to create and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d937-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4d937-105">Prerequisites</span></span>

* <span data-ttu-id="4d937-106">Azure CLI 2.0을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="4d937-107">그런 다음, Service Fabric 클러스터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="4d937-108">자세한 내용은 [Azure CLI 2.0 시작](service-fabric-azure-cli-2-0.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d937-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="4d937-109">배포를 위해 Service Fabric 응용 프로그램 패키지를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-109">Have a Service Fabric application package ready to be deployed.</span></span> <span data-ttu-id="4d937-110">응용 프로그램 작성 및 패키지 방법에 대한 자세한 정보는 [Service Fabric 응용 프로그램 모델](service-fabric-application-model.md)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-110">For more information about how to author and package an application, read about the [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="4d937-111">개요</span><span class="sxs-lookup"><span data-stu-id="4d937-111">Overview</span></span>

<span data-ttu-id="4d937-112">새 응용 프로그램을 배포하려면 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-112">To deploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="4d937-113">Service Fabric 이미지 저장소에 응용 프로그램 패키지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-113">Upload an application package to the Service Fabric image store.</span></span>
2. <span data-ttu-id="4d937-114">응용 프로그램 유형을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-114">Provision an application type.</span></span>
3. <span data-ttu-id="4d937-115">응용 프로그램을 지정하고 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-115">Specify and create an application.</span></span>
4. <span data-ttu-id="4d937-116">서비스를 지정하고 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-116">Specify and create services.</span></span>

<span data-ttu-id="4d937-117">기존 응용 프로그램을 제거하려면 다음이 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-117">To remove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="4d937-118">응용 프로그램을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-118">Delete the application.</span></span>
2. <span data-ttu-id="4d937-119">관련된 응용 프로그램 유형의 프로비전을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-119">Unprovision the associated application type.</span></span>
3. <span data-ttu-id="4d937-120">이미지 저장소 콘텐츠를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-120">Delete the image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="4d937-121">새 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="4d937-121">Deploy a new application</span></span>

<span data-ttu-id="4d937-122">새 응용 프로그램을 배포하려면 다음 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-122">To deploy a new application, complete the following tasks.</span></span>

### <a name="upload-a-new-application-package-to-the-image-store"></a><span data-ttu-id="4d937-123">이미지 저장소에 새 응용 프로그램 패키지 업로드</span><span class="sxs-lookup"><span data-stu-id="4d937-123">Upload a new application package to the image store</span></span>

<span data-ttu-id="4d937-124">응용 프로그램을 만들기 전에 Service Fabric 이미지 저장소에 응용 프로그램 패키지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-124">Before you create an application, upload the application package to the Service Fabric image store.</span></span> 

<span data-ttu-id="4d937-125">예를 들어, 응용 프로그램 패키지가 `app_package_dir` 디렉터리에 있는 경우 다음 명령을 사용하여 디렉터리를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-125">For example, if your application package is in the `app_package_dir` directory, use the following commands to upload the directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="4d937-126">대형 응용 프로그램 패키지의 경우 `--show-progress` 옵션을 지정하여 업로드 진행률을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-126">For large application packages, you can specify the `--show-progress` option to display the progress of the upload.</span></span>

### <a name="provision-the-application-type"></a><span data-ttu-id="4d937-127">응용 프로그램 유형 프로비전</span><span class="sxs-lookup"><span data-stu-id="4d937-127">Provision the application type</span></span>

<span data-ttu-id="4d937-128">업로드가 완료되면 응용 프로그램을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-128">When the upload is finished, provision the application.</span></span> <span data-ttu-id="4d937-129">응용 프로그램을 프로비전하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-129">To provision the application, use the following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="4d937-130">`application-type-build-path`의 값은 응용 프로그램 패키지를 업로드하는 디렉터리의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-130">The value for `application-type-build-path` is the name of the directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="4d937-131">응용 프로그램 유형에서 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="4d937-131">Create an application from an application type</span></span>

<span data-ttu-id="4d937-132">응용 프로그램을 프로비전한 후에는 다음 명령을 사용하여 응용 프로그램 이름을 지정하고 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-132">After you provision the application, use the following command to name and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="4d937-133">`app-name`은 응용 프로그램 인스턴스에 사용하려는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-133">`app-name` is the name that you want to use for the application instance.</span></span> <span data-ttu-id="4d937-134">이전에 프로비전된 응용 프로그램 매니페스트에서 추가 매개 변수를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="4d937-135">응용 프로그램 이름은 `fabric:/` 접두사로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-135">The application name must start with the prefix `fabric:/`.</span></span>

### <a name="create-services-for-the-new-application"></a><span data-ttu-id="4d937-136">새 응용 프로그램에 대한 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="4d937-136">Create services for the new application</span></span>

<span data-ttu-id="4d937-137">응용 프로그램이 만들어진 후에는 응용 프로그램에서 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-137">After you have created an application, create services from the application.</span></span> <span data-ttu-id="4d937-138">다음 예의 경우, 응용 프로그램에서 새 상태 비저장 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-138">In the following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="4d937-139">응용 프로그램에서 만들 수 있는 서비스는 이전에 프로비전된 응용 프로그램 패키지 내의 서비스 매니페스트에 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-139">The services that you can create from an application are defined in a service manifest in the previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="4d937-140">응용 프로그램 배포 및 상태 확인</span><span class="sxs-lookup"><span data-stu-id="4d937-140">Verify application deployment and health</span></span>

<span data-ttu-id="4d937-141">응용 프로그램 및 서비스가 성공적으로 배포되었는지 확인하려면 응용 프로그램 및 서비스가 나열되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-141">To verify that an application and service were successfully deployed, check that the application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="4d937-142">서비스가 정상 상태인지 확인하려면 유사한 명령을 사용하여 서비스와 응용 프로그램의 상태를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-142">To verify that the service is healthy, use similar commands to retrieve the health of both the service and the application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="4d937-143">정상 서비스 및 응용 프로그램은 `HealthState` 값이 `Ok`입니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="4d937-144">기존 응용 프로그램 제거</span><span class="sxs-lookup"><span data-stu-id="4d937-144">Remove an existing application</span></span>

<span data-ttu-id="4d937-145">응용 프로그램을 제거하려면 다음 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-145">To remove an application, complete the following tasks.</span></span>

### <a name="delete-the-application"></a><span data-ttu-id="4d937-146">응용 프로그램 삭제</span><span class="sxs-lookup"><span data-stu-id="4d937-146">Delete the application</span></span>

<span data-ttu-id="4d937-147">응용 프로그램을 삭제하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-147">To delete the application, use the following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-the-application-type"></a><span data-ttu-id="4d937-148">응용 프로그램 유형 프로비전 해제</span><span class="sxs-lookup"><span data-stu-id="4d937-148">Unprovision the application type</span></span>

<span data-ttu-id="4d937-149">응용 프로그램을 삭제한 후에는 더 이상 필요 없는 경우 응용 프로그램 유형의 프로비전을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-149">After you delete the application, you can unprovision the application type if you no longer need it.</span></span> <span data-ttu-id="4d937-150">응용 프로그램 유형을 프로비전 해제하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-150">To unprovision the application type, use the following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="4d937-151">유형 이름 및 유형 버전은 이전에 프로비전된 응용 프로그램 매니페스트의 이름 및 버전과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-151">The type name and type version must match the name and version in the previously provisioned application manifest.</span></span>

### <a name="delete-the-application-package"></a><span data-ttu-id="4d937-152">응용 프로그램 패키지 삭제</span><span class="sxs-lookup"><span data-stu-id="4d937-152">Delete the application package</span></span>

<span data-ttu-id="4d937-153">응용 프로그램 유형이 프로비전 해제된 후에는 더 이상 필요하지 않은 경우 응용 프로그램 패키지를 이미지 저장소에서 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-153">After you have unprovisioned the application type, you can delete the application package from the image store if you no longer need it.</span></span> <span data-ttu-id="4d937-154">응용 프로그램 패키지를 삭제하면 디스크 공간을 확보하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="4d937-155">이미지 저장소에서 응용 프로그램 패키지를 삭제하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-155">To delete the application package from the image store, use the following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="4d937-156">`content-path`는 응용 프로그램을 만들 때 업로드한 디렉터리의 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d937-156">`content-path` must be the name of the directory that you uploaded when you created the application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="4d937-157">관련 문서</span><span class="sxs-lookup"><span data-stu-id="4d937-157">Related articles</span></span>

* [<span data-ttu-id="4d937-158">Service Fabric 및 Azure CLI 2.0 시작</span><span class="sxs-lookup"><span data-stu-id="4d937-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="4d937-159">Service Fabric XPlat CLI 시작</span><span class="sxs-lookup"><span data-stu-id="4d937-159">Get started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
