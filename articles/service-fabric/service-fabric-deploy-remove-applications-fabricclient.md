---
title: "서비스 패브릭 응용 프로그램 배포 aaaAzure | Microsoft Docs"
description: "Hello FabricClient Api toodeploy 방법과 서비스 패브릭에서 응용 프로그램을 제거 합니다."
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
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a><span data-ttu-id="bceb0-103">FabricClient를 사용하여 응용 프로그램 배포 및 제거</span><span class="sxs-lookup"><span data-stu-id="bceb0-103">Deploy and remove applications using FabricClient</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bceb0-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bceb0-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="bceb0-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bceb0-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="bceb0-106">FabricClient API</span><span class="sxs-lookup"><span data-stu-id="bceb0-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="bceb0-107">일단 [응용 프로그램 형식이 패키지화되면][10] Azure Service Fabric 클러스터에 배포될 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="bceb0-108">배포에는 세 단계를 수행 하는 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="bceb0-109">Hello 응용 프로그램 패키지 toohello 이미지 저장소에 업로드</span><span class="sxs-lookup"><span data-stu-id="bceb0-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="bceb0-110">Hello 응용 프로그램 형식 등록</span><span class="sxs-lookup"><span data-stu-id="bceb0-110">Register hello application type</span></span>
3. <span data-ttu-id="bceb0-111">Hello 응용 프로그램 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="bceb0-111">Create hello application instance</span></span>

<span data-ttu-id="bceb0-112">한 후 응용 프로그램이 배포 된 hello 클러스터에서 실행 중인 인스턴스를 hello 응용 프로그램 인스턴스 및 해당 응용 프로그램 종류를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="bceb0-113">hello 클러스터에서 응용 프로그램 toocompletely 제거 단계를 수행 하는 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="bceb0-114">응용 프로그램 인스턴스를 실행 하는 hello 제거 (또는 삭제)</span><span class="sxs-lookup"><span data-stu-id="bceb0-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="bceb0-115">필요 없는 hello 응용 프로그램 종류를 등록 취소</span><span class="sxs-lookup"><span data-stu-id="bceb0-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="bceb0-116">Hello 이미지 저장소에서 hello 응용 프로그램 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="bceb0-117">사용 하는 경우 [배포 및 응용 프로그램 디버깅에 대 한 Visual Studio](service-fabric-publish-app-remote-cluster.md) 앞의 단계를 hello 모든 로컬 개발 클러스터에는 PowerShell 스크립트를 통해 자동으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="bceb0-118">이 스크립트는 hello에서 발견 되 *스크립트* hello 응용 프로그램 프로젝트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="bceb0-119">이 문서에서는 수행할 수 있도록 해당 스크립트가 수행 하는 작업에 배경 제공 hello Visual Studio 외부에서 이와 동일한 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="bceb0-120">Toohello 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="bceb0-120">Connect toohello cluster</span></span>
<span data-ttu-id="bceb0-121">Toohello 클러스터를 생성 하 여 연결 된 [FabricClient](/dotnet/api/system.fabric.fabricclient) 이 문서의 코드 예제는 hello 실행 하기 전에 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="bceb0-121">Connect toohello cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of hello code examples in this article.</span></span> <span data-ttu-id="bceb0-122">원격 클러스터 연결 tooa 로컬 개발 클러스터 또는 클러스터 X509 Azure Active Directory를 사용 하 여 보안의 예제를 보려면 인증서 또는 Windows Active Directory 참조 [연결 tooa 보안 클러스터](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis)합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-122">For examples of connecting tooa local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span></span> <span data-ttu-id="bceb0-123">tooconnect toohello 로컬 개발 클러스터 hello 다음 실행:</span><span class="sxs-lookup"><span data-stu-id="bceb0-123">tooconnect toohello local development cluster, run hello following:</span></span>

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a><span data-ttu-id="bceb0-124">Hello 응용 프로그램 패키지 업로드</span><span class="sxs-lookup"><span data-stu-id="bceb0-124">Upload hello application package</span></span>
<span data-ttu-id="bceb0-125">Visual Studio에서 *MyApplication*이라는 응용 프로그램을 빌드하고 패키지한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-125">Suppose you build and package an application named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="bceb0-126">기본적으로 hello 응용 프로그램 유형 이름은 ApplicationManifest.xml hello에 나열 된 "MyApplicationType"는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-126">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="bceb0-127">hello hello 필요한 응용 프로그램 매니페스트, 서비스 매니페스트 및 코드/config/데이터 패키지를 포함 하는 응용 프로그램 패키지에 있는 *C:\Users\&lt; username&gt;\Documents\Visual Studio 2017\Projects\ MyApplication\MyApplication\pkg\Debug*합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-127">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span>

<span data-ttu-id="bceb0-128">Hello 응용 프로그램 패키지 업로드 hello 내부 서비스 패브릭 구성 요소에서 액세스할 수 있는 위치에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-128">Uploading hello application package puts it in a location that's accessible by hello internal Service Fabric components.</span></span> <span data-ttu-id="bceb0-129">서비스 패브릭 hello 응용 프로그램 패키지의 hello 등록 하는 동안 hello 응용 프로그램 패키지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-129">Service Fabric verifies hello application package during hello registration of hello application package.</span></span> <span data-ttu-id="bceb0-130">그러나 tooverify hello 응용 프로그램 패키지를 로컬로 (즉, 업로드 하기 전에) 하려는 경우 사용할 hello [테스트 ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bceb0-130">However, if you want tooverify hello application package locally (i.e., before uploading), use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="bceb0-131">hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API hello 응용 프로그램 패키지 toohello 클러스터 이미지 저장소에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-131">hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploads hello application package toohello cluster image store.</span></span> 

<span data-ttu-id="bceb0-132">Hello 응용 프로그램 패키지 큰 많은 파일의 경우, 다음을 할 수 있습니다 [압축](service-fabric-package-apps.md#compress-a-package) PowerShell을 사용 하 여 toohello 이미지 저장소를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-132">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it toohello image store using PowerShell.</span></span> <span data-ttu-id="bceb0-133">hello 압축 hello 크기와 파일 hello 수가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-133">hello compression reduces hello size and hello number of files.</span></span>

<span data-ttu-id="bceb0-134">참조 [hello 이미지 저장소 연결 문자열을 이해](service-fabric-image-store-connection-string.md) 보충 정보에 대 한 hello 이미지 저장소 및 이미지 연결 문자열을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-134">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="bceb0-135">Hello 응용 프로그램 패키지를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-135">Register hello application package</span></span>
<span data-ttu-id="bceb0-136">hello 응용 프로그램 유형 및 버전 hello 응용 프로그램 패키지를 등록 하면 사용 하기 위해 사용할 수 있게 하는 hello 응용 프로그램 매니페스트에 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-136">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="bceb0-137">hello 시스템 hello 이전 단계에서 업로드 된 hello 패키지가, hello 패키지를 확인, hello 패키지 내용 처리 읽고 처리 하는 hello 패키지 tooan 내부 시스템 위치에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-137">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="bceb0-138">hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API 레지스터 hello hello 클러스터에서 응용 프로그램 종류와 배포에 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-138">hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers hello application type in hello cluster and make it available for deployment.</span></span>

<span data-ttu-id="bceb0-139">hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API는 모든 성공적으로 등록 된 응용 프로그램 종류에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-139">hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API provides information about all successfully registered application types.</span></span> <span data-ttu-id="bceb0-140">이 API toodetermine hello 등록 수행 되는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-140">You can use this API toodetermine when hello registration is done.</span></span>

## <a name="create-an-application-instance"></a><span data-ttu-id="bceb0-141">응용 프로그램 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="bceb0-141">Create an application instance</span></span>
<span data-ttu-id="bceb0-142">Hello를 사용 하 여 성공적으로 등록 된 모든 응용 프로그램 종류에서 응용 프로그램을 인스턴스화할 수 [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API입니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-142">You can instantiate an application from any application type that has been registered successfully by using hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span></span> <span data-ttu-id="bceb0-143">각 응용 프로그램의 hello 이름 hello로 시작 해야 *"패브릭:"* 구성표 및 각 응용 프로그램 인스턴스의 (클러스터) 내에서 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-143">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance (within a cluster).</span></span> <span data-ttu-id="bceb0-144">Hello 대상 응용 프로그램 종류의 응용 프로그램 매니페스트 hello에에서 정의 된 기본 서비스 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-144">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

<span data-ttu-id="bceb0-145">등록된 응용 프로그램 형식의 주어진 어떤 버전에 대해서도 여러 개의 응용 프로그램 인스턴스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-145">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="bceb0-146">각 응용 프로그램 인스턴스는 자체 작업 디렉터리 및 프로세스 집합과는 별도로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-146">Each application instance runs in isolation, with its own working directory and set of processes.</span></span>

<span data-ttu-id="bceb0-147">hello를 실행 하는 hello 클러스터에서 실행 하는 응용 프로그램 및 서비스 이라는 toosee [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) 및 [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) Api입니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-147">toosee which named applications and services are running in hello cluster, run hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.</span></span>

## <a name="create-a-service-instance"></a><span data-ttu-id="bceb0-148">서비스 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="bceb0-148">Create a service instance</span></span>
<span data-ttu-id="bceb0-149">Hello를 사용 하 여 서비스 유형에 서 서비스를 인스턴스화할 수 [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API입니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-149">You can instantiate a service from a service type using hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span></span>  <span data-ttu-id="bceb0-150">Hello 서비스 hello 응용 프로그램 매니페스트에서 기본 서비스로 선언 된 경우에 hello 서비스 hello 응용 프로그램 인스턴스화될 때 인스턴스화됩니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-150">If hello service is declared as a default service in hello application manifest, hello service is instantiated when hello application is instantiated.</span></span>  <span data-ttu-id="bceb0-151">호출 hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) 인스턴스화된 이미 서비스에 대 한 API FabricException FabricErrorCode.ServiceAlreadyExists 값으로는 오류 코드가 포함 된 형식의 예외를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-151">Calling hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API for a service that is already instantiated will return an exception of type FabricException containing an error code with a value of FabricErrorCode.ServiceAlreadyExists.</span></span>

## <a name="remove-a-service-instance"></a><span data-ttu-id="bceb0-152">서비스 인스턴스 제거</span><span class="sxs-lookup"><span data-stu-id="bceb0-152">Remove a service instance</span></span>
<span data-ttu-id="bceb0-153">서비스 인스턴스를 더 이상 필요 하면 hello를 호출 하 여 응용 프로그램 인스턴스를 실행 하는 hello에서 제거할 수 없습니다 [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API입니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-153">When a service instance is no longer needed, you can remove it from hello running application instance by calling hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span></span>  

> [!WARNING]
> <span data-ttu-id="bceb0-154">이 작업은 되돌릴 수 없으며 서비스 상태는 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-154">This operation cannot be reversed, and service state cannot be recovered.</span></span>

## <a name="remove-an-application-instance"></a><span data-ttu-id="bceb0-155">응용 프로그램 인스턴스 제거</span><span class="sxs-lookup"><span data-stu-id="bceb0-155">Remove an application instance</span></span>
<span data-ttu-id="bceb0-156">응용 프로그램 인스턴스가 필요 하지 않은 경우 제거할 수 없습니다 영구적으로 hello를 사용 하 여 이름 [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API입니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-156">When an application instance is no longer needed, you can permanently remove it by name using hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span></span> <span data-ttu-id="bceb0-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) 도, 영구적으로 모든 서비스 상태를 제거 하는 toohello 응용 프로그램에 포함 된 모든 서비스를 자동으로 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span>

> [!WARNING]
> <span data-ttu-id="bceb0-158">이 작업은 되돌릴 수 없으며 응용 프로그램 상태는 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-158">This operation cannot be reversed, and application state cannot be recovered.</span></span>

## <a name="unregister-an-application-type"></a><span data-ttu-id="bceb0-159">응용 프로그램 유형 등록 취소</span><span class="sxs-lookup"><span data-stu-id="bceb0-159">Unregister an application type</span></span>
<span data-ttu-id="bceb0-160">특정 버전의 hello를 사용 하 여 hello 응용 프로그램 종류를 등록 취소 해야 응용 프로그램 종류의 특정 버전은 더 이상 필요 없는, [등록 취소 ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API입니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-160">When a particular version of an application type is no longer needed, you should unregister that particular version of hello application type using hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span></span> <span data-ttu-id="bceb0-161">응용 프로그램 종류 버전 저장소 공간의 hello 이미지 저장소에서 사용 하는 사용 하지 않는 버전의 등록을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-161">Unregistering unused versions of application types releases storage space used by hello image store.</span></span> <span data-ttu-id="bceb0-162">응용 프로그램 종류의 버전으로 응용 프로그램이 없습니다. 해당 버전의 hello 응용 프로그램 종류에 대해 인스턴스화되고 없는 보류 중인 응용 프로그램 업그레이드 hello 응용 프로그램 종류의 해당 버전을 참조 하는 등록 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-162">A version of an application type can be unregistered as long as no applications are instantiated against that version of hello application type and no pending application upgrades are referencing that version of hello application type.</span></span>

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="bceb0-163">Hello 이미지 저장소에서 응용 프로그램 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-163">Remove an application package from hello image store</span></span>
<span data-ttu-id="bceb0-164">응용 프로그램 패키지를 더 이상 필요 hello를 사용 하 여 시스템 리소스를 hello 이미지 저장소 toofree에서 삭제할 수 [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API입니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-164">When an application package is no longer needed, you can delete it from hello image store toofree up system resources using hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="bceb0-165">문제 해결</span><span class="sxs-lookup"><span data-stu-id="bceb0-165">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="bceb0-166">Copy-ServiceFabricApplicationPackage가 ImageStoreConnectionString을 요청함</span><span class="sxs-lookup"><span data-stu-id="bceb0-166">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="bceb0-167">서비스 패브릭 SDK 환경 hello hello 기본값을 설정 하 고 올바른 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-167">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="bceb0-168">하지만 해당 hello 서비스 패브릭 클러스터를 사용 하 여 모든 명령에 대 한 hello ImageStoreConnectionString 해야 hello 값 필요한 경우 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-168">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="bceb0-169">Hello ImageStoreConnectionString hello 클러스터 매니페스트에서 찾을 수 있습니다 hello를 사용 하 여 검색 [Get ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) 및 Get ImageStoreConnectionStringFromClusterManifest 명령:</span><span class="sxs-lookup"><span data-stu-id="bceb0-169">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="bceb0-170">hello **Get ImageStoreConnectionStringFromClusterManifest** hello 서비스 패브릭 SDK PowerShell 모듈의 일부인 cmdlet을 사용 하는 tooget hello 이미지인 연결 문자열을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-170">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="bceb0-171">tooimport hello SDK 모듈을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-171">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


<span data-ttu-id="bceb0-172">hello ImageStoreConnectionString은 hello 클러스터 매니페스트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-172">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="bceb0-173">참조 [hello 이미지 저장소 연결 문자열을 이해](service-fabric-image-store-connection-string.md) 보충 정보에 대 한 hello 이미지 저장소 및 이미지 연결 문자열을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-173">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="bceb0-174">대형 응용 프로그램 패키지 배포</span><span class="sxs-lookup"><span data-stu-id="bceb0-174">Deploy large application package</span></span>
<span data-ttu-id="bceb0-175">문제: 대형 응용 프로그램 패키지(GB 단위)에 대한 [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API 시간이 초과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-175">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API times out for a large application package (order of GB).</span></span>
<span data-ttu-id="bceb0-176">다음을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="bceb0-176">Try:</span></span>
- <span data-ttu-id="bceb0-177">[CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) 메서드에 `timeout` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-177">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span></span> <span data-ttu-id="bceb0-178">기본적으로 hello 제한 시간 30 분입니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-178">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="bceb0-179">원본 컴퓨터와 클러스터 간에 hello 네트워크 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-179">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="bceb0-180">Hello 연결이 느린 경우에 컴퓨터를 사용 하 여 더 나은 네트워크 연결을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-180">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="bceb0-181">Hello 클라이언트 컴퓨터가 hello 클러스터와 다른 지역에 있는 경우에 hello 클러스터와 가깝거나 동일한 지역에 클라이언트 컴퓨터를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-181">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="bceb0-182">외부 제한에 도달하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-182">Check if you are hitting external throttling.</span></span> <span data-ttu-id="bceb0-183">예를 들어 hello 이미지 저장소에 구성 된 toouse azure 저장소가, 업로드 제한 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-183">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="bceb0-184">문제: 패키지 업로드가 성공적으로 완료되었지만 [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API 시간이 초과되었습니다. 다음을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="bceb0-184">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API times out. Try:</span></span>
- <span data-ttu-id="bceb0-185">[Hello 패키지를 압축](service-fabric-package-apps.md#compress-a-package) toohello 이미지 저장소를 복사 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="bceb0-185">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="bceb0-186">hello 압축 hello 크기가 줄어들고에 hello 트래픽 양이 감소 하 고 해당 서비스 패브릭 작업 hello 수의 파일을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-186">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="bceb0-187">hello 업로드 작업 (특히 포함 하는 경우 hello 압축 시간)에 속도가 느려질 수 있습니다, 하지만 등록 및 등록을 취소할 hello 응용 프로그램 종류는 더 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-187">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="bceb0-188">[ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API에 `timeout` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-188">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API with `timeout` parameter.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="bceb0-189">많은 파일이 있는 응용 프로그램 패키지 배포</span><span class="sxs-lookup"><span data-stu-id="bceb0-189">Deploy application package with many files</span></span>
<span data-ttu-id="bceb0-190">문제: 많은 파일(1,000개 단위)이 있는 응용 프로그램 패키지에 대한 [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync)가 시간이 초과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-190">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="bceb0-191">다음을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="bceb0-191">Try:</span></span>
- <span data-ttu-id="bceb0-192">[Hello 패키지를 압축](service-fabric-package-apps.md#compress-a-package) toohello 이미지 저장소를 복사 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="bceb0-192">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="bceb0-193">hello 압축 hello 파일 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-193">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="bceb0-194">[ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync)에 `timeout` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-194">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span></span>

## <a name="code-example"></a><span data-ttu-id="bceb0-195">코드 예제</span><span class="sxs-lookup"><span data-stu-id="bceb0-195">Code example</span></span>
<span data-ttu-id="bceb0-196">hello 다음 예제에서는 응용 프로그램 패키지 toohello 이미지 저장소에 복사, 응용 프로그램 종류 hello를 프로 비전, 응용 프로그램 인스턴스, 만들어집니다에서 서비스 인스턴스를 제거 hello 응용 프로그램 인스턴스 취소를 프로 비전 hello 응용 프로그램 종류 및 hello 이미지 저장소에서 hello 응용 프로그램 패키지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="bceb0-196">hello following example copies an application package toohello image store, provisions hello application type, creates an application instance, creates a service instance, removes hello application instance, un-provisions hello application type, and deletes hello application package from hello image store.</span></span>

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

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
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

    //  Create hello application instance.
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

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
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

    // Delete an application instance from hello application type.
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

    // Un-provision hello application type.
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

    // Delete hello application package from a location in hello image store.
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

## <a name="next-steps"></a><span data-ttu-id="bceb0-197">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bceb0-197">Next steps</span></span>
[<span data-ttu-id="bceb0-198">서비스 패브릭 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="bceb0-198">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="bceb0-199">서비스 패브릭 상태 소개</span><span class="sxs-lookup"><span data-stu-id="bceb0-199">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="bceb0-200">서비스 패브릭 서비스 진단 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="bceb0-200">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="bceb0-201">서비스 패브릭에서 응용 프로그램 모델링</span><span class="sxs-lookup"><span data-stu-id="bceb0-201">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
