---
title: "Azure Service Fabric 응용 프로그램 배포 | Microsoft Docs"
description: "FabricClient API를 사용하여 Service Fabric에서 응용 프로그램을 배포 및 제거합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: 2e4ca1069b4e8e473b26b790e81770b41e25ff50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a><span data-ttu-id="e16a0-103">FabricClient를 사용하여 응용 프로그램 배포 및 제거</span><span class="sxs-lookup"><span data-stu-id="e16a0-103">Deploy and remove applications using FabricClient</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e16a0-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e16a0-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="e16a0-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e16a0-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="e16a0-106">FabricClient API</span><span class="sxs-lookup"><span data-stu-id="e16a0-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="e16a0-107">일단 [응용 프로그램 형식이 패키지화되면][10] Azure Service Fabric 클러스터에 배포될 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="e16a0-108">배포에는 다음 세 단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-108">Deployment involves the following three steps:</span></span>

1. <span data-ttu-id="e16a0-109">이미지 저장소에 응용 프로그램 패키지 업로드</span><span class="sxs-lookup"><span data-stu-id="e16a0-109">Upload the application package to the image store</span></span>
2. <span data-ttu-id="e16a0-110">응용 프로그램 형식 등록</span><span class="sxs-lookup"><span data-stu-id="e16a0-110">Register the application type</span></span>
3. <span data-ttu-id="e16a0-111">응용 프로그램 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="e16a0-111">Create the application instance</span></span>

<span data-ttu-id="e16a0-112">응용 프로그램을 배포하고 인스턴스가 클러스터에서 실행되면 응용 프로그램 인스턴스와 해당 응용 프로그램 형식을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-112">After an application is deployed and an instance is running in the cluster, you can delete the application instance and its application type.</span></span> <span data-ttu-id="e16a0-113">클러스터에서 응용 프로그램을 완전히 제거하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-113">To completely remove an application from the cluster involves the following steps:</span></span>

1. <span data-ttu-id="e16a0-114">실행 중인 응용 프로그램 인스턴스 제거(또는 삭제)</span><span class="sxs-lookup"><span data-stu-id="e16a0-114">Remove (or delete) the running application instance</span></span>
2. <span data-ttu-id="e16a0-115">더 이상 필요하지 않은 경우 응용 프로그램 유형 등록 취소</span><span class="sxs-lookup"><span data-stu-id="e16a0-115">Unregister the application type if you no longer need it</span></span>
3. <span data-ttu-id="e16a0-116">이미지 저장소에서 응용 프로그램 패키지 제거</span><span class="sxs-lookup"><span data-stu-id="e16a0-116">Remove the application package from the image store</span></span>

<span data-ttu-id="e16a0-117">로컬 개발 클러스터에서 [Visual Studio를 사용하여 응용 프로그램을 개발 및 배포](service-fabric-publish-app-remote-cluster.md)하는 경우 이전의 모든 단계는 PowerShell 스크립트를 통해 자동으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="e16a0-118">이 스크립트는 응용 프로그램 프로젝트의 *Scripts* 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-118">This script is found in the *Scripts* folder of the application project.</span></span> <span data-ttu-id="e16a0-119">이 문서에서는 Visual Studio 외부에서 동일한 작업을 수행할 수 있도록 스크립트에서 수행하는 작업에 대한 배경을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-119">This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-to-the-cluster"></a><span data-ttu-id="e16a0-120">클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="e16a0-120">Connect to the cluster</span></span>
<span data-ttu-id="e16a0-121">이 문서의 코드 예제 중 하나를 실행하기 전에 [FabricClient](/dotnet/api/system.fabric.fabricclient) 인스턴스를 만들어 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-121">Connect to the cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of the code examples in this article.</span></span> <span data-ttu-id="e16a0-122">로컬 개발 클러스터 또는 원격 클러스터나 Azure Active Directory, X509 인증서 또는 Windows Active Directory를 사용하여 보안된 클러스터에 연결하는 예제는 [보안 클러스터에 연결](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e16a0-122">For examples of connecting to a local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span></span> <span data-ttu-id="e16a0-123">로컬 개발 클러스터에 연결하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-123">To connect to the local development cluster, run the following:</span></span>

```csharp
// Connect to the local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-the-application-package"></a><span data-ttu-id="e16a0-124">응용 프로그램 패키지 업로드</span><span class="sxs-lookup"><span data-stu-id="e16a0-124">Upload the application package</span></span>
<span data-ttu-id="e16a0-125">Visual Studio에서 *MyApplication*이라는 응용 프로그램을 빌드하고 패키지한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-125">Suppose you build and package an application named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="e16a0-126">기본적으로 ApplicationManifest.xml에 나열된 응용 프로그램 유형 이름은 "MyApplicationType"입니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-126">By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="e16a0-127">필요한 응용 프로그램 매니페스트, 서비스 매니페스트 및 코드/구성/데이터 패키지가 포함된 응용 프로그램 패키지는 *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-127">The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span>

<span data-ttu-id="e16a0-128">응용 프로그램 패키지를 업로드하면 내부 Service Fabric 구성 요소에 의해 액세스할 수 있는 위치에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-128">Uploading the application package puts it in a location that's accessible by the internal Service Fabric components.</span></span> <span data-ttu-id="e16a0-129">Service Fabric은 응용 프로그램 패키지를 등록하는 동안 응용 프로그램 패키지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-129">Service Fabric verifies the application package during the registration of the application package.</span></span> <span data-ttu-id="e16a0-130">단, 로컬로 응용 프로그램 패키지를 확인하려는 경우(예: 업로드하기 전에) [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-130">However, if you want to verify the application package locally (i.e., before uploading), use the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="e16a0-131">[CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API는 응용 프로그램 패키지를 클러스터 이미지 저장소에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-131">The [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploads the application package to the cluster image store.</span></span> 

<span data-ttu-id="e16a0-132">응용 프로그램 패키지가 크거나 파일이 많은 경우 [압축](service-fabric-package-apps.md#compress-a-package)한 다음, PowerShell을 사용하여 이미지 저장소에 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-132">If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it to the image store using PowerShell.</span></span> <span data-ttu-id="e16a0-133">압축은 파일의 크기와 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-133">The compression reduces the size and the number of files.</span></span>

<span data-ttu-id="e16a0-134">이미지 저장소 및 이미지 저장소 연결 문자열에 대한 보충 정보는 [이미지 저장소 연결 문자열 이해](service-fabric-image-store-connection-string.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e16a0-134">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

## <a name="register-the-application-package"></a><span data-ttu-id="e16a0-135">응용 프로그램 패키지 등록</span><span class="sxs-lookup"><span data-stu-id="e16a0-135">Register the application package</span></span>
<span data-ttu-id="e16a0-136">응용 프로그램 매니페스트에 선언된 응용 프로그램 형식과 버전은 응용 프로그램 패키지를 등록할 때 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-136">The application type and version declared in the application manifest become available for use when the application package is registered.</span></span> <span data-ttu-id="e16a0-137">시스템은 이전 단계에서 업로드된 패키지를 읽고, 패키지를 확인하며, 처리된 패키지를 내부 시스템 위치에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-137">The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.</span></span>  

<span data-ttu-id="e16a0-138">[ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API는 클러스터에 응용 프로그램 형식을 등록한 후 배포에 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-138">The [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers the application type in the cluster and make it available for deployment.</span></span>

<span data-ttu-id="e16a0-139">[GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API는 성공적으로 등록된 모든 응용 프로그램 형식에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-139">The [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API provides information about all successfully registered application types.</span></span> <span data-ttu-id="e16a0-140">이 API를 사용하여 등록이 완료된 시기를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-140">You can use this API to determine when the registration is done.</span></span>

## <a name="create-an-application-instance"></a><span data-ttu-id="e16a0-141">응용 프로그램 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="e16a0-141">Create an application instance</span></span>
<span data-ttu-id="e16a0-142">[CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API를 사용하여 성공적으로 등록된 모든 응용 프로그램 형식에서 응용 프로그램을 인스턴스화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-142">You can instantiate an application from any application type that has been registered successfully by using the [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span></span> <span data-ttu-id="e16a0-143">각 응용 프로그램의 이름은 반드시 *"fabric:"* 체계로 시작하고 각 응용 프로그램 인스턴스에 대해 고유해야 합니다(클러스터 내).</span><span class="sxs-lookup"><span data-stu-id="e16a0-143">The name of each application must start with the *"fabric:"* scheme and must be unique for each application instance (within a cluster).</span></span> <span data-ttu-id="e16a0-144">대상 응용 프로그램 형식의 응용 프로그램 매니페스트에 정의된 모든 기본 서비스도 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-144">Any default services defined in the application manifest of the target application type are also created.</span></span>

<span data-ttu-id="e16a0-145">등록된 응용 프로그램 형식의 주어진 어떤 버전에 대해서도 여러 개의 응용 프로그램 인스턴스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-145">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="e16a0-146">각 응용 프로그램 인스턴스는 자체 작업 디렉터리 및 프로세스 집합과는 별도로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-146">Each application instance runs in isolation, with its own working directory and set of processes.</span></span>

<span data-ttu-id="e16a0-147">클러스터에서 실행 중인 명명된 응용 프로그램과 서비스를 확인하려면 [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) 및 [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) API를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-147">To see which named applications and services are running in the cluster, run the [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.</span></span>

## <a name="create-a-service-instance"></a><span data-ttu-id="e16a0-148">서비스 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="e16a0-148">Create a service instance</span></span>
<span data-ttu-id="e16a0-149">[CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API를 사용하여 서비스 형식에서 서비스를 인스턴스화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-149">You can instantiate a service from a service type using the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span></span>  <span data-ttu-id="e16a0-150">서비스가 응용 프로그램 매니페스트에서 기본 서비스로 선언되면 응용 프로그램이 인스턴스화될 때 해당 서비스도 인스턴스화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-150">If the service is declared as a default service in the application manifest, the service is instantiated when the application is instantiated.</span></span>  <span data-ttu-id="e16a0-151">이미 인스턴스화된 서비스에 대해 [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API를 호출하면 FabricErrorCode.ServiceAlreadyExists 값의 오류 코드를 포함하는 FabricException 형식의 예외를 반환하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-151">Calling the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API for a service that is already instantiated will return an exception of type FabricException containing an error code with a value of FabricErrorCode.ServiceAlreadyExists.</span></span>

## <a name="remove-a-service-instance"></a><span data-ttu-id="e16a0-152">서비스 인스턴스 제거</span><span class="sxs-lookup"><span data-stu-id="e16a0-152">Remove a service instance</span></span>
<span data-ttu-id="e16a0-153">서비스 인스턴스가 더 이상 필요하지 않을 경우 [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API를 호출하여 실행 중인 응용 프로그램 인스턴스에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-153">When a service instance is no longer needed, you can remove it from the running application instance by calling the [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span></span>  

> [!WARNING]
> <span data-ttu-id="e16a0-154">이 작업은 되돌릴 수 없으며 서비스 상태는 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-154">This operation cannot be reversed, and service state cannot be recovered.</span></span>

## <a name="remove-an-application-instance"></a><span data-ttu-id="e16a0-155">응용 프로그램 인스턴스 제거</span><span class="sxs-lookup"><span data-stu-id="e16a0-155">Remove an application instance</span></span>
<span data-ttu-id="e16a0-156">응용 프로그램 인스턴스가 더 이상 필요하지 않은 경우 [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API를 사용하여 이름별로 영구적으로 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-156">When an application instance is no longer needed, you can permanently remove it by name using the [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span></span> <span data-ttu-id="e16a0-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync)는 모든 서비스 상태를 영구적으로 제거하고 해당 응용 프로그램에 속한 모든 서비스를 자동으로 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong to the application as well, permanently removing all service state.</span></span>

> [!WARNING]
> <span data-ttu-id="e16a0-158">이 작업은 되돌릴 수 없으며 응용 프로그램 상태는 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-158">This operation cannot be reversed, and application state cannot be recovered.</span></span>

## <a name="unregister-an-application-type"></a><span data-ttu-id="e16a0-159">응용 프로그램 유형 등록 취소</span><span class="sxs-lookup"><span data-stu-id="e16a0-159">Unregister an application type</span></span>
<span data-ttu-id="e16a0-160">특정 버전의 응용 프로그램 형식이 더 이상 필요하지 않으면 [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API를 사용하여 해당 응용 프로그램 형식의 버전을 등록 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-160">When a particular version of an application type is no longer needed, you should unregister that particular version of the application type using the [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span></span> <span data-ttu-id="e16a0-161">사용하지 않는 응용 프로그램 형식의 버전을 등록 취소하면 이미지 저장소에서 사용하는 저장 공간이 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-161">Unregistering unused versions of application types releases storage space used by the image store.</span></span> <span data-ttu-id="e16a0-162">응용 프로그램 형식의 버전은 해당 응용 프로그램 형식의 버전에 대해 인스턴스화된 응용 프로그램이나 해당 응용 프로그램 형식의 버전을 참조하는 보류 중인 응용 프로그램이 없는 한 등록 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-162">A version of an application type can be unregistered as long as no applications are instantiated against that version of the application type and no pending application upgrades are referencing that version of the application type.</span></span>

## <a name="remove-an-application-package-from-the-image-store"></a><span data-ttu-id="e16a0-163">이미지 저장소에서 응용 프로그램 패키지 제거</span><span class="sxs-lookup"><span data-stu-id="e16a0-163">Remove an application package from the image store</span></span>
<span data-ttu-id="e16a0-164">응용 프로그램 패키지가 더 이상 필요하지 않은 경우 [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API를 사용하여 이미지 저장소에서 삭제하여 시스템 리소스를 확보할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-164">When an application package is no longer needed, you can delete it from the image store to free up system resources using the [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e16a0-165">문제 해결</span><span class="sxs-lookup"><span data-stu-id="e16a0-165">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="e16a0-166">Copy-ServiceFabricApplicationPackage가 ImageStoreConnectionString을 요청함</span><span class="sxs-lookup"><span data-stu-id="e16a0-166">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="e16a0-167">서비스 패브릭 SDK 환경은 이미 올바른 기본 설정값을 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-167">The Service Fabric SDK environment should already have the correct defaults set up.</span></span> <span data-ttu-id="e16a0-168">하지만 필요한 경우 모든 명령에 대한 ImageStoreConnectionString은 서비스 패브릭 클러스터가 사용 중인 값과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-168">But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using.</span></span> <span data-ttu-id="e16a0-169">[Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) 및 Get-ImageStoreConnectionStringFromClusterManifest 명령을 사용하여 검색된 클러스터 매니페스트에서 ImageStoreConnectionString을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-169">You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="e16a0-170">서비스 패브릭 SDK PowerShell 모듈의 일부인 **Get ImageStoreConnectionStringFromClusterManifest** cmdlet는 이미지 저장소 연결 문자열을 가져오는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-170">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="e16a0-171">SDK 모듈을 가져오려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-171">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


<span data-ttu-id="e16a0-172">ImageStoreConnectionString은 클러스터 매니페스트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-172">The ImageStoreConnectionString is found in the cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="e16a0-173">이미지 저장소 및 이미지 저장소 연결 문자열에 대한 보충 정보는 [이미지 저장소 연결 문자열 이해](service-fabric-image-store-connection-string.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e16a0-173">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="e16a0-174">대형 응용 프로그램 패키지 배포</span><span class="sxs-lookup"><span data-stu-id="e16a0-174">Deploy large application package</span></span>
<span data-ttu-id="e16a0-175">문제: 대형 응용 프로그램 패키지(GB 단위)에 대한 [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API 시간이 초과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-175">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API times out for a large application package (order of GB).</span></span>
<span data-ttu-id="e16a0-176">다음을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="e16a0-176">Try:</span></span>
- <span data-ttu-id="e16a0-177">[CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) 메서드에 `timeout` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-177">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span></span> <span data-ttu-id="e16a0-178">기본적으로 시간 제한은 30분입니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-178">By default, the timeout is 30 minutes.</span></span>
- <span data-ttu-id="e16a0-179">원본 컴퓨터와 클러스터 간의 네트워크 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-179">Check the network connection between your source machine and cluster.</span></span> <span data-ttu-id="e16a0-180">연결 속도가 느린 경우 네트워크 연결 상태가 좋은 컴퓨터를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-180">If the connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="e16a0-181">클라이언트 컴퓨터가 클러스터가 아닌 다른 지역에 있는 경우 해당 클러스터와 가깝거나 동일한 지역에 있는 클라이언트 컴퓨터를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-181">If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.</span></span>
- <span data-ttu-id="e16a0-182">외부 제한에 도달하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-182">Check if you are hitting external throttling.</span></span> <span data-ttu-id="e16a0-183">예를 들어 Azure 저장소를 사용하도록 이미지 저장소를 구성한 경우 업로드가 제한될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-183">For example, when the image store is configured to use azure storage, upload may be throttled.</span></span>

<span data-ttu-id="e16a0-184">문제: 패키지 업로드가 성공적으로 완료되었지만 [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API 시간이 초과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-184">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API times out.</span></span>
<span data-ttu-id="e16a0-185">다음을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="e16a0-185">Try:</span></span>
- <span data-ttu-id="e16a0-186">이미지 저장소에 복사하기 전에 [패키지를 압축합니다](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="e16a0-186">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span>
<span data-ttu-id="e16a0-187">압축하면 파일의 크기와 수가 줄어들므로 Service Fabric에서 수행해야 하는 트래픽과 작업량도 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-187">The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="e16a0-188">업로드 작업이 느려질 수 있지만(특히 압축 시간이 포함되는 경우), 응용 프로그램 유형을 더 빠르게 등록 및 등록 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-188">The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.</span></span>
- <span data-ttu-id="e16a0-189">[ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API에 `timeout` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-189">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API with `timeout` parameter.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="e16a0-190">많은 파일이 있는 응용 프로그램 패키지 배포</span><span class="sxs-lookup"><span data-stu-id="e16a0-190">Deploy application package with many files</span></span>
<span data-ttu-id="e16a0-191">문제: 많은 파일(1,000개 단위)이 있는 응용 프로그램 패키지에 대한 [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync)가 시간이 초과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-191">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="e16a0-192">다음을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="e16a0-192">Try:</span></span>
- <span data-ttu-id="e16a0-193">이미지 저장소에 복사하기 전에 [패키지를 압축합니다](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="e16a0-193">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span> <span data-ttu-id="e16a0-194">압축하면 파일의 수가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-194">The compression reduces the number of files.</span></span>
- <span data-ttu-id="e16a0-195">[ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync)에 `timeout` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-195">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span></span>

## <a name="code-example"></a><span data-ttu-id="e16a0-196">코드 예제</span><span class="sxs-lookup"><span data-stu-id="e16a0-196">Code example</span></span>
<span data-ttu-id="e16a0-197">다음 예제에서는 응용 프로그램 패키지를 이미지 저장소로 복사하고, 응용 프로그램 형식을 프로비전하고, 응용 프로그램 인스턴스를 만들고, 서비스 인스턴스를 만들고, 응용 프로그램 형식의 프로비전을 취소하고, 이미지 저장소에서 응용 프로그램 패키지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="e16a0-197">The following example copies an application package to the image store, provisions the application type, creates an application instance, creates a service instance, removes the application instance, un-provisions the application type, and deletes the application package from the image store.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect to the cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy the application package to a location in the image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied to {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy to Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision the application.  "MyApplicationV1" is the folder in the image store where the application package is located. 
    // The application type with name "MyApplicationType" and version "1.0.0" (both are found in the application manifest) 
    // is now registered in the cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create the application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create the stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create the service instance.  If the service is declared as a default service in the ApplicationManifest.xml,
    // the service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from the application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision the application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete the application package from a location in the image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a><span data-ttu-id="e16a0-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e16a0-198">Next steps</span></span>
[<span data-ttu-id="e16a0-199">서비스 패브릭 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="e16a0-199">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="e16a0-200">서비스 패브릭 상태 소개</span><span class="sxs-lookup"><span data-stu-id="e16a0-200">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="e16a0-201">서비스 패브릭 서비스 진단 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e16a0-201">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="e16a0-202">서비스 패브릭에서 응용 프로그램 모델링</span><span class="sxs-lookup"><span data-stu-id="e16a0-202">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
