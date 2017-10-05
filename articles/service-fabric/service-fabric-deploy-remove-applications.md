---
title: "Azure Service Fabric 응용 프로그램 배포 | Microsoft Docs"
description: "PowerShell을 사용하여 Service Fabric에서 응용 프로그램을 배포 및 제거하는 방법"
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
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: edef23a8cdab7fd0bef54456f0caabb9db273bf9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="f5b49-103">PowerShell을 사용하여 응용 프로그램 배포 및 제거</span><span class="sxs-lookup"><span data-stu-id="f5b49-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f5b49-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5b49-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="f5b49-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f5b49-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="f5b49-106">FabricClient API</span><span class="sxs-lookup"><span data-stu-id="f5b49-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="f5b49-107">일단 [응용 프로그램 형식이 패키지화되면][10] Azure Service Fabric 클러스터에 배포될 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="f5b49-108">배포에는 다음 세 단계가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-108">Deployment involves the following three steps:</span></span>

1. <span data-ttu-id="f5b49-109">이미지 저장소에 응용 프로그램 패키지 업로드</span><span class="sxs-lookup"><span data-stu-id="f5b49-109">Upload the application package to the image store</span></span>
2. <span data-ttu-id="f5b49-110">응용 프로그램 형식 등록</span><span class="sxs-lookup"><span data-stu-id="f5b49-110">Register the application type</span></span>
3. <span data-ttu-id="f5b49-111">응용 프로그램 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="f5b49-111">Create the application instance</span></span>

<span data-ttu-id="f5b49-112">응용 프로그램을 배포하고 인스턴스가 클러스터에서 실행되면 응용 프로그램 인스턴스와 해당 응용 프로그램 형식을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-112">After an application is deployed and an instance is running in the cluster, you can delete the application instance and its application type.</span></span> <span data-ttu-id="f5b49-113">클러스터에서 응용 프로그램을 완전히 제거하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-113">To completely remove an application from the cluster involves the following steps:</span></span>

1. <span data-ttu-id="f5b49-114">실행 중인 응용 프로그램 인스턴스 제거(또는 삭제)</span><span class="sxs-lookup"><span data-stu-id="f5b49-114">Remove (or delete) the running application instance</span></span>
2. <span data-ttu-id="f5b49-115">더 이상 필요하지 않은 경우 응용 프로그램 유형 등록 취소</span><span class="sxs-lookup"><span data-stu-id="f5b49-115">Unregister the application type if you no longer need it</span></span>
3. <span data-ttu-id="f5b49-116">이미지 저장소에서 응용 프로그램 패키지 제거</span><span class="sxs-lookup"><span data-stu-id="f5b49-116">Remove the application package from the image store</span></span>

<span data-ttu-id="f5b49-117">로컬 개발 클러스터에서 [Visual Studio를 사용하여 응용 프로그램을 개발 및 배포](service-fabric-publish-app-remote-cluster.md)하는 경우 이전의 모든 단계는 PowerShell 스크립트를 통해 자동으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="f5b49-118">이 스크립트는 응용 프로그램 프로젝트의 *Scripts* 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-118">This script is found in the *Scripts* folder of the application project.</span></span> <span data-ttu-id="f5b49-119">이 문서에서는 Visual Studio 외부에서 동일한 작업을 수행할 수 있도록 스크립트에서 수행하는 작업에 대한 배경을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-119">This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-to-the-cluster"></a><span data-ttu-id="f5b49-120">클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="f5b49-120">Connect to the cluster</span></span>
<span data-ttu-id="f5b49-121">이 문서에서는 PowerShell 명령을 실행하기에 앞서 언제나 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps)를 사용하여 Service Fabric 클러스터에 연결하는 것으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) to connect to the Service Fabric cluster.</span></span> <span data-ttu-id="f5b49-122">로컬 개발 클러스터에 연결하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-122">To connect to the local development cluster, run the following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="f5b49-123">Azure Active Directory, X509 인증서 또는 Windows Active Directory를 사용하여 보안된 원격 클러스터 또는 클러스터에 연결하는 예제는 [보안 클러스터에 연결](service-fabric-connect-to-secure-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5b49-123">For examples of connecting to a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-the-application-package"></a><span data-ttu-id="f5b49-124">응용 프로그램 패키지 업로드</span><span class="sxs-lookup"><span data-stu-id="f5b49-124">Upload the application package</span></span>
<span data-ttu-id="f5b49-125">응용 프로그램 패키지를 업로드하면 내부 서비스 패브릭 구성 요소에 의해 액세스할 수 있는 위치에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-125">Uploading the application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="f5b49-126">로컬로 응용 프로그램 패키지를 확인하려는 경우 [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-126">If you want to verify the application package locally, use the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="f5b49-127">[Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 명령으로 응용 프로그램 패키지를 클러스터 이미지 저장소에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-127">The [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads the application package to the cluster image store.</span></span>
<span data-ttu-id="f5b49-128">서비스 패브릭 SDK PowerShell 모듈의 일부인 **Get ImageStoreConnectionStringFromClusterManifest** cmdlet는 이미지 저장소 연결 문자열을 가져오는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-128">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="f5b49-129">SDK 모듈을 가져오려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-129">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="f5b49-130">Visual Studio 2015에서 *MyApplication*이라는 응용 프로그램을 빌드하고 패키지한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-130">Suppose you build and package an application named *MyApplication* in Visual Studio 2015.</span></span> <span data-ttu-id="f5b49-131">기본적으로 ApplicationManifest.xml에 나열된 응용 프로그램 유형 이름은 "MyApplicationType"입니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-131">By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="f5b49-132">필요한 응용 프로그램 매니페스트, 서비스 매니페스트 및 코드/구성/데이터 패키지가 포함된 응용 프로그램 패키지는 *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-132">The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="f5b49-133">다음 명령은 응용 프로그램 패키지의 내용을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-133">The following command lists the contents of the application package:</span></span>

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

<span data-ttu-id="f5b49-134">응용 프로그램 패키지가 크거나 파일이 많은 경우 [압축할 수 있습니다](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="f5b49-134">If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="f5b49-135">압축은 파일의 크기와 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-135">The compression reduces the size and the number of files.</span></span>
<span data-ttu-id="f5b49-136">부작용은 응용 프로그램 유형 등록 및 등록 취소가 빠르다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-136">The side effect is that registering and un-registering the application type are faster.</span></span> <span data-ttu-id="f5b49-137">업로드 시간은 현재 느려질 수 있습니다. 패키지를 압축하는 시간이 포함되는 경우 특히 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-137">Upload time may be slower currently, especially if you include the time to compress the package.</span></span> 

<span data-ttu-id="f5b49-138">패키지를 압축하려면 동일한 [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-138">To compress a package, use the same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span> <span data-ttu-id="f5b49-139">압축은 업로드와 별도로 `SkipCopy` 플래그를 사용하거나 업로드 작업과 함께 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-139">Compression can be done separate from upload, by using the `SkipCopy` flag, or together with the upload operation.</span></span> <span data-ttu-id="f5b49-140">압축된 패키지에 압축을 적용하면 아무런 변화가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="f5b49-141">압축된 패키지를 풀려면 `UncompressPackage` 스위치와 함께 [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-141">To uncompress a compressed package, use the same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command with the `UncompressPackage` switch.</span></span>

<span data-ttu-id="f5b49-142">다음 cmdlet은 패키지를 이미지 저장소에 복사하지 않고 압축합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-142">The following cmdlet compresses the package without copying it to the image store.</span></span> <span data-ttu-id="f5b49-143">이제 패키지에 `Code` 및 `Config` 패키지의 압축 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-143">The package now includes zipped files for the `Code` and `Config` packages.</span></span> <span data-ttu-id="f5b49-144">응용 프로그램 및 서비스 매니페스트는 많은 내부 작업(특정 유효성 검사를 위한 패키지 공유, 응용 프로그램 유형 이름 및 버전 추출 등)에 필요하기 때문에 압축되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-144">The application and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="f5b49-145">매니페스트를 압축하면 이러한 작업이 비효율적으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-145">Zipping the manifests would make these operations inefficient.</span></span>

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

<span data-ttu-id="f5b49-146">대형 응용 프로그램 패키지의 경우 압축하는 데 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-146">For large application packages, the compression takes time.</span></span> <span data-ttu-id="f5b49-147">최상의 결과를 얻으려면 빠른 SSD 드라이브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="f5b49-148">압축된 패키지의 압축 시간과 크기도 패키지 내용에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-148">The compression times and the size of the compressed package also differ based on the package content.</span></span>
<span data-ttu-id="f5b49-149">예를 들어 압축 시간과 함께 초기 크기 및 압축된 패키지 크기를 보여 주는 일부 패키지의 압축 통계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-149">For example, here is compression statistics for some packages, which show the initial and the compressed package size, with the compression time.</span></span>

|<span data-ttu-id="f5b49-150">초기 크기(MB)</span><span class="sxs-lookup"><span data-stu-id="f5b49-150">Initial size (MB)</span></span>|<span data-ttu-id="f5b49-151">파일 수</span><span class="sxs-lookup"><span data-stu-id="f5b49-151">File count</span></span>|<span data-ttu-id="f5b49-152">압축 시간</span><span class="sxs-lookup"><span data-stu-id="f5b49-152">Compression Time</span></span>|<span data-ttu-id="f5b49-153">압축된 패키지 크기(MB)</span><span class="sxs-lookup"><span data-stu-id="f5b49-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="f5b49-154">100</span><span class="sxs-lookup"><span data-stu-id="f5b49-154">100</span></span>|<span data-ttu-id="f5b49-155">100</span><span class="sxs-lookup"><span data-stu-id="f5b49-155">100</span></span>|<span data-ttu-id="f5b49-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="f5b49-156">00:00:03.3547592</span></span>|<span data-ttu-id="f5b49-157">60</span><span class="sxs-lookup"><span data-stu-id="f5b49-157">60</span></span>|
|<span data-ttu-id="f5b49-158">512</span><span class="sxs-lookup"><span data-stu-id="f5b49-158">512</span></span>|<span data-ttu-id="f5b49-159">100</span><span class="sxs-lookup"><span data-stu-id="f5b49-159">100</span></span>|<span data-ttu-id="f5b49-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="f5b49-160">00:00:16.3850303</span></span>|<span data-ttu-id="f5b49-161">307</span><span class="sxs-lookup"><span data-stu-id="f5b49-161">307</span></span>|
|<span data-ttu-id="f5b49-162">1024</span><span class="sxs-lookup"><span data-stu-id="f5b49-162">1024</span></span>|<span data-ttu-id="f5b49-163">500</span><span class="sxs-lookup"><span data-stu-id="f5b49-163">500</span></span>|<span data-ttu-id="f5b49-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="f5b49-164">00:00:32.5907950</span></span>|<span data-ttu-id="f5b49-165">615</span><span class="sxs-lookup"><span data-stu-id="f5b49-165">615</span></span>|
|<span data-ttu-id="f5b49-166">2048</span><span class="sxs-lookup"><span data-stu-id="f5b49-166">2048</span></span>|<span data-ttu-id="f5b49-167">1000</span><span class="sxs-lookup"><span data-stu-id="f5b49-167">1000</span></span>|<span data-ttu-id="f5b49-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="f5b49-168">00:01:04.3775554</span></span>|<span data-ttu-id="f5b49-169">1231</span><span class="sxs-lookup"><span data-stu-id="f5b49-169">1231</span></span>|
|<span data-ttu-id="f5b49-170">5012</span><span class="sxs-lookup"><span data-stu-id="f5b49-170">5012</span></span>|<span data-ttu-id="f5b49-171">100</span><span class="sxs-lookup"><span data-stu-id="f5b49-171">100</span></span>|<span data-ttu-id="f5b49-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="f5b49-172">00:02:45.2951288</span></span>|<span data-ttu-id="f5b49-173">3074</span><span class="sxs-lookup"><span data-stu-id="f5b49-173">3074</span></span>|

<span data-ttu-id="f5b49-174">압축된 패키지는 필요에 따라 하나 또는 여러 개의 Service Fabric 클러스터에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-174">Once a package is compressed, it can be uploaded to one or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="f5b49-175">배포 메커니즘은 압축된 패키지와 압축되지 않은 패키지에 대해 모두 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-175">The deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="f5b49-176">압축된 패키지는 클러스터 이미지 저장소에 그대로 저장되며, 먼저 노드에서 압축이 풀린 후에 응용 프로그램이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-176">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span></span>


<span data-ttu-id="f5b49-177">다음 예제에서는 패키지를 이미지 저장소의 "MyApplicationV1"이라는 폴더에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-177">The following example uploads the package to the image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="f5b49-178">서비스 패브릭 SDK PowerShell 모듈의 일부인 **Get ImageStoreConnectionStringFromClusterManifest** cmdlet는 이미지 저장소 연결 문자열을 가져오는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-178">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="f5b49-179">SDK 모듈을 가져오려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-179">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="f5b49-180">*-ApplicationPackagePathInImageStore* 매개 변수를 지정하지 않으면 응용 프로그램 패키지가 이미지 저장소의 “Debug” 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-180">If you do not specify the *-ApplicationPackagePathInImageStore* parameter, the application package is copied into the "Debug" folder in the image store.</span></span>

<span data-ttu-id="f5b49-181">패키지를 업로드하는 데 걸리는 시간은 여러 요소에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-181">The time it takes to upload a package differs depending on multiple factors.</span></span> <span data-ttu-id="f5b49-182">이러한 요소 중 일부는 패키지의 파일 수, 패키지 크기 및 파일 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-182">Some of these factors are the number of files in the package, the package size, and the file sizes.</span></span> <span data-ttu-id="f5b49-183">원본 컴퓨터와 Service Fabric 클러스터 간의 네트워크 속도 업로드 시간에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-183">The network speed between the source machine and the Service Fabric cluster also impacts the upload time.</span></span> <span data-ttu-id="f5b49-184">[Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)의 기본 시간 제한은 30분입니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-184">The default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minutes.</span></span>
<span data-ttu-id="f5b49-185">설명된 요소에 따라 시간 제한을 늘려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-185">Depending on the described factors, you may have to increase the timeout.</span></span> <span data-ttu-id="f5b49-186">복사 호출에서 패키지를 압축하는 경우 압축 시간도 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-186">If you are compressing the package in the copy call, you need to also consider the compression time.</span></span>

<span data-ttu-id="f5b49-187">이미지 저장소 및 이미지 저장소 연결 문자열에 대한 보충 정보는 [이미지 저장소 연결 문자열 이해](service-fabric-image-store-connection-string.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5b49-187">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

## <a name="register-the-application-package"></a><span data-ttu-id="f5b49-188">응용 프로그램 패키지 등록</span><span class="sxs-lookup"><span data-stu-id="f5b49-188">Register the application package</span></span>
<span data-ttu-id="f5b49-189">응용 프로그램 매니페스트에 선언된 응용 프로그램 형식과 버전은 응용 프로그램 패키지를 등록할 때 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-189">The application type and version declared in the application manifest become available for use when the application package is registered.</span></span> <span data-ttu-id="f5b49-190">시스템은 이전 단계에서 업로드된 패키지를 읽고, 패키지를 확인하며, 처리된 패키지를 내부 시스템 위치에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-190">The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.</span></span>  

<span data-ttu-id="f5b49-191">[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet을 실행하여 클러스터에서 응용 프로그램 유형을 등록하고 배포할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-191">Run the [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet to register the application type in the cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="f5b49-192">“MyApplicationV1”은 응용 프로그램 패키지가 있는 이미지 저장소의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-192">"MyApplicationV1" is the folder in the image store where the application package is located.</span></span> <span data-ttu-id="f5b49-193">이름이 "MyApplicationType"이고 버전이 "1.0.0"인(둘 다 응용 프로그램 매니페스트에 있음) 응용 프로그램 유형이 이제 클러스터에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-193">The application type with name "MyApplicationType" and version "1.0.0" (both are found in the application manifest) is now registered in the cluster.</span></span>

<span data-ttu-id="f5b49-194">[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 명령은 시스템에서 응용 프로그램 패키지를 성공적으로 등록한 후에만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-194">The [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command returns only after the system has successfully registered the application package.</span></span> <span data-ttu-id="f5b49-195">등록에 걸리는 시간은 응용 프로그램 패키지의 크기 및 콘텐츠에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-195">How long registration takes depends on the size and contents of the application package.</span></span> <span data-ttu-id="f5b49-196">**-TimeoutSec** 매개 변수는 필요한 경우 더 긴 제한 시간을 제공합니다(기본 제한 시간은 60초).</span><span class="sxs-lookup"><span data-stu-id="f5b49-196">If needed, the **-TimeoutSec** parameter can be used to supply a longer timeout (the default timeout is 60 seconds).</span></span>

<span data-ttu-id="f5b49-197">대형 응용 프로그램 패키지가 있거나 시간 제한이 발생하는 경우 **-Async** 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-197">If you have a large application package or if you are experiencing timeouts, use the **-Async** parameter.</span></span> <span data-ttu-id="f5b49-198">클러스터에서 register 명령을 승인할 때 명령이 반환되고 필요에 따라 처리가 계속됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-198">The command returns when the cluster accepts the register command, and the processing continues as needed.</span></span>
<span data-ttu-id="f5b49-199">[Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) 명령은 성공적으로 등록된 모든 응용 프로그램 유형 버전과 해당 등록 상태를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-199">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="f5b49-200">이 명령을 사용하여 등록이 완료된 시기를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-200">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-the-application"></a><span data-ttu-id="f5b49-201">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f5b49-201">Create the application</span></span>
<span data-ttu-id="f5b49-202">[New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet을 사용하여 성공적으로 등록된 모든 응용 프로그램 유형 버전에서 응용 프로그램을 인스턴스화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-202">You can instantiate an application from any application type version that has been registered successfully by using the [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="f5b49-203">각 응용 프로그램의 이름은 반드시 *“fabric:”* 체계로 시작하고 각 응용 프로그램 인스턴스에 대해 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-203">The name of each application must start with the *"fabric:"* scheme and must be unique for each application instance.</span></span> <span data-ttu-id="f5b49-204">대상 응용 프로그램 형식의 응용 프로그램 매니페스트에 정의된 모든 기본 서비스도 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-204">Any default services defined in the application manifest of the target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="f5b49-205">등록된 응용 프로그램 형식의 주어진 어떤 버전에 대해서도 여러 개의 응용 프로그램 인스턴스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-205">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="f5b49-206">각 응용 프로그램 인스턴스는 자체 작업 디렉터리 및 프로세스와는 별도로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-206">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="f5b49-207">클러스터에서 실행 중인 명명된 응용 프로그램과 서비스를 확인하려면 [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) 및 [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-207">To see which named apps and services are running in the cluster, run the [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a><span data-ttu-id="f5b49-208">응용 프로그램 제거</span><span class="sxs-lookup"><span data-stu-id="f5b49-208">Remove an application</span></span>
<span data-ttu-id="f5b49-209">응용 프로그램 인스턴스가 더 이상 필요하지 않은 경우 [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet을 사용하여 해당 응용 프로그램 인스턴스를 이름별로 영구적으로 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-209">When an application instance is no longer needed, you can permanently remove it by name using the [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="f5b49-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps)은 응용 프로그램에 속한 모든 서비스를 자동으로 제거하고, 해당 서비스 상태를 모두 영구적으로 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatically removes all services that belong to the application as well, permanently removing all service state.</span></span> 

> [!WARNING]
> <span data-ttu-id="f5b49-211">이 작업은 되돌릴 수 없으며 응용 프로그램 상태는 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-211">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="f5b49-212">응용 프로그램 유형 등록 취소</span><span class="sxs-lookup"><span data-stu-id="f5b49-212">Unregister an application type</span></span>
<span data-ttu-id="f5b49-213">특정 버전의 응용 프로그램 유형이 더 이상 필요하지 않으면 [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet을 사용하여 해당 응용 프로그램 유형을 등록 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-213">When a particular version of an application type is no longer needed, you should unregister the application type using the [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="f5b49-214">사용하지 않는 응용 프로그램 유형을 등록 취소하면 이미지 저장소에서 사용하는 저장 공간이 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-214">Unregistering unused application types releases storage space used by the image store.</span></span> <span data-ttu-id="f5b49-215">응용 프로그램 형식은 이에 대해 인스턴스화된 응용 프로그램이나 이를 참조하는 보류 중인 응용 프로그램이 없는 한 등록 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-215">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="f5b49-216">[Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps)을 실행하여 현재 클러스터에 등록된 응용 프로그램 유형을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-216">Run [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) to see the application types currently registered in the cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="f5b49-217">[Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps)을 실행하여 특정 응용 프로그램 유형의 등록을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-217">Run [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) to unregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-the-image-store"></a><span data-ttu-id="f5b49-218">이미지 저장소에서 응용 프로그램 패키지 제거</span><span class="sxs-lookup"><span data-stu-id="f5b49-218">Remove an application package from the image store</span></span>
<span data-ttu-id="f5b49-219">응용 프로그램 패키지가 더 이상 필요하지 않은 경우 이미지 저장소에서 해당 응용 프로그램 패키지를 삭제하여 시스템 리소스를 확보할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-219">When an application package is no longer needed, you can delete it from the image store to free up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="f5b49-220">문제 해결</span><span class="sxs-lookup"><span data-stu-id="f5b49-220">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="f5b49-221">Copy-ServiceFabricApplicationPackage가 ImageStoreConnectionString을 요청함</span><span class="sxs-lookup"><span data-stu-id="f5b49-221">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="f5b49-222">서비스 패브릭 SDK 환경은 이미 올바른 기본 설정값을 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-222">The Service Fabric SDK environment should already have the correct defaults set up.</span></span> <span data-ttu-id="f5b49-223">하지만 필요한 경우 모든 명령에 대한 ImageStoreConnectionString은 서비스 패브릭 클러스터가 사용 중인 값과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-223">But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using.</span></span> <span data-ttu-id="f5b49-224">[Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) 및 Get-ImageStoreConnectionStringFromClusterManifest 명령을 사용하여 검색된 클러스터 매니페스트에서 ImageStoreConnectionString을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-224">You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="f5b49-225">서비스 패브릭 SDK PowerShell 모듈의 일부인 **Get ImageStoreConnectionStringFromClusterManifest** cmdlet는 이미지 저장소 연결 문자열을 가져오는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-225">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="f5b49-226">SDK 모듈을 가져오려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-226">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="f5b49-227">ImageStoreConnectionString은 클러스터 매니페스트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-227">The ImageStoreConnectionString is found in the cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="f5b49-228">이미지 저장소 및 이미지 저장소 연결 문자열에 대한 보충 정보는 [이미지 저장소 연결 문자열 이해](service-fabric-image-store-connection-string.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f5b49-228">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="f5b49-229">대형 응용 프로그램 패키지 배포</span><span class="sxs-lookup"><span data-stu-id="f5b49-229">Deploy large application package</span></span>
<span data-ttu-id="f5b49-230">문제: 대형 응용 프로그램 패키지(GB 단위)에 대한 [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 시간이 초과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-230">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="f5b49-231">다음을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="f5b49-231">Try:</span></span>
- <span data-ttu-id="f5b49-232">[Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 명령에 `TimeoutSec` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-232">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="f5b49-233">기본적으로 시간 제한은 30분입니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-233">By default, the timeout is 30 minutes.</span></span>
- <span data-ttu-id="f5b49-234">원본 컴퓨터와 클러스터 간의 네트워크 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-234">Check the network connection between your source machine and cluster.</span></span> <span data-ttu-id="f5b49-235">연결 속도가 느린 경우 네트워크 연결 상태가 좋은 컴퓨터를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-235">If the connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="f5b49-236">클라이언트 컴퓨터가 클러스터가 아닌 다른 지역에 있는 경우 해당 클러스터와 가깝거나 동일한 지역에 있는 클라이언트 컴퓨터를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-236">If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.</span></span>
- <span data-ttu-id="f5b49-237">외부 제한에 도달하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-237">Check if you are hitting external throttling.</span></span> <span data-ttu-id="f5b49-238">예를 들어 Azure 저장소를 사용하도록 이미지 저장소를 구성한 경우 업로드가 제한될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-238">For example, when the image store is configured to use azure storage, upload may be throttled.</span></span>

<span data-ttu-id="f5b49-239">문제: 패키지 업로드가 성공적으로 완료되었지만 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 시간이 초과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-239">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out.</span></span>
<span data-ttu-id="f5b49-240">다음을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="f5b49-240">Try:</span></span>
- <span data-ttu-id="f5b49-241">이미지 저장소에 복사하기 전에 [패키지를 압축합니다](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="f5b49-241">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span>
<span data-ttu-id="f5b49-242">압축하면 파일의 크기와 수가 줄어들므로 Service Fabric에서 수행해야 하는 트래픽과 작업량도 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-242">The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="f5b49-243">업로드 작업이 느려질 수 있지만(특히 압축 시간이 포함되는 경우), 응용 프로그램 유형을 더 빠르게 등록 및 등록 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-243">The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.</span></span>
- <span data-ttu-id="f5b49-244">[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)에 `TimeoutSec` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-244">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="f5b49-245">[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)에 `Async` 스위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-245">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="f5b49-246">명령은 클러스터가 명령을 수락하고 응용 프로그램 형식의 등록을 비동기적으로 계속하는 경우 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-246">The command returns when the cluster accepts the command and the registration of the application type continues asynchronously.</span></span> <span data-ttu-id="f5b49-247">이러한 이유로 더 긴 시간 제한을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-247">For this reason, there is no need to specify a higher timeout in this case.</span></span> <span data-ttu-id="f5b49-248">[Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) 명령은 성공적으로 등록된 모든 응용 프로그램 유형 버전과 해당 등록 상태를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-248">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="f5b49-249">이 명령을 사용하여 등록이 완료된 시기를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-249">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="f5b49-250">많은 파일이 있는 응용 프로그램 패키지 배포</span><span class="sxs-lookup"><span data-stu-id="f5b49-250">Deploy application package with many files</span></span>
<span data-ttu-id="f5b49-251">문제: 많은 파일(1,000개 단위)이 있는 응용 프로그램 패키지에 대한 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 시간이 초과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-251">Issue: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="f5b49-252">다음을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="f5b49-252">Try:</span></span>
- <span data-ttu-id="f5b49-253">이미지 저장소에 복사하기 전에 [패키지를 압축합니다](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="f5b49-253">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span> <span data-ttu-id="f5b49-254">압축하면 파일의 수가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-254">The compression reduces the number of files.</span></span>
- <span data-ttu-id="f5b49-255">[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)에 `TimeoutSec` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-255">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="f5b49-256">[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)에 `Async` 스위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-256">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="f5b49-257">명령은 클러스터가 명령을 수락하고 응용 프로그램 형식의 등록을 비동기적으로 계속하는 경우 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-257">The command returns when the cluster accepts the command and the registration of the application type continues asynchronously.</span></span>
<span data-ttu-id="f5b49-258">이러한 이유로 더 긴 시간 제한을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-258">For this reason, there is no need to specify a higher timeout in this case.</span></span> <span data-ttu-id="f5b49-259">[Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) 명령은 성공적으로 등록된 모든 응용 프로그램 유형 버전과 해당 등록 상태를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-259">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="f5b49-260">이 명령을 사용하여 등록이 완료된 시기를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5b49-260">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a><span data-ttu-id="f5b49-261">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5b49-261">Next steps</span></span>
[<span data-ttu-id="f5b49-262">서비스 패브릭 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="f5b49-262">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="f5b49-263">서비스 패브릭 상태 소개</span><span class="sxs-lookup"><span data-stu-id="f5b49-263">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="f5b49-264">서비스 패브릭 서비스 진단 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f5b49-264">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="f5b49-265">서비스 패브릭에서 응용 프로그램 모델링</span><span class="sxs-lookup"><span data-stu-id="f5b49-265">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
