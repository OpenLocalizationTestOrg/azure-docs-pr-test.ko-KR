---
title: "서비스 패브릭 응용 프로그램 배포 aaaAzure | Microsoft Docs"
description: "어떻게 toodeploy 및 제거 PowerShell을 사용 하 여 서비스 패브릭 응용 프로그램입니다."
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
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="afb13-103">PowerShell을 사용하여 응용 프로그램 배포 및 제거</span><span class="sxs-lookup"><span data-stu-id="afb13-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="afb13-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="afb13-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="afb13-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="afb13-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="afb13-106">FabricClient API</span><span class="sxs-lookup"><span data-stu-id="afb13-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="afb13-107">일단 [응용 프로그램 형식이 패키지화되면][10] Azure Service Fabric 클러스터에 배포될 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="afb13-108">배포에는 세 단계를 수행 하는 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="afb13-109">Hello 응용 프로그램 패키지 toohello 이미지 저장소에 업로드</span><span class="sxs-lookup"><span data-stu-id="afb13-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="afb13-110">Hello 응용 프로그램 형식 등록</span><span class="sxs-lookup"><span data-stu-id="afb13-110">Register hello application type</span></span>
3. <span data-ttu-id="afb13-111">Hello 응용 프로그램 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="afb13-111">Create hello application instance</span></span>

<span data-ttu-id="afb13-112">한 후 응용 프로그램이 배포 된 hello 클러스터에서 실행 중인 인스턴스를 hello 응용 프로그램 인스턴스 및 해당 응용 프로그램 종류를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="afb13-113">hello 클러스터에서 응용 프로그램 toocompletely 제거 단계를 수행 하는 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="afb13-114">응용 프로그램 인스턴스를 실행 하는 hello 제거 (또는 삭제)</span><span class="sxs-lookup"><span data-stu-id="afb13-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="afb13-115">필요 없는 hello 응용 프로그램 종류를 등록 취소</span><span class="sxs-lookup"><span data-stu-id="afb13-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="afb13-116">Hello 이미지 저장소에서 hello 응용 프로그램 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="afb13-117">사용 하는 경우 [배포 및 응용 프로그램 디버깅에 대 한 Visual Studio](service-fabric-publish-app-remote-cluster.md) 앞의 단계를 hello 모든 로컬 개발 클러스터에는 PowerShell 스크립트를 통해 자동으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="afb13-118">이 스크립트는 hello에서 발견 되 *스크립트* hello 응용 프로그램 프로젝트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="afb13-119">이 문서에서는 수행할 수 있도록 해당 스크립트가 수행 하는 작업에 배경 제공 hello Visual Studio 외부에서 이와 동일한 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="afb13-120">Toohello 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="afb13-120">Connect toohello cluster</span></span>
<span data-ttu-id="afb13-121">이 문서에는 PowerShell 명령을 실행 하기 전에 항상 사용 하 여 시작 [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello 서비스 패브릭 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello Service Fabric cluster.</span></span> <span data-ttu-id="afb13-122">tooconnect toohello 로컬 개발 클러스터 hello 다음 실행:</span><span class="sxs-lookup"><span data-stu-id="afb13-122">tooconnect toohello local development cluster, run hello following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="afb13-123">Tooa 원격 클러스터 또는 클러스터 X509 Azure Active Directory를 사용 하 여 보안 연결의 예제를 보려면 인증서 또는 Windows Active Directory 참조 [연결 tooa 보안 클러스터](service-fabric-connect-to-secure-cluster.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-123">For examples of connecting tooa remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-hello-application-package"></a><span data-ttu-id="afb13-124">Hello 응용 프로그램 패키지 업로드</span><span class="sxs-lookup"><span data-stu-id="afb13-124">Upload hello application package</span></span>
<span data-ttu-id="afb13-125">Hello 응용 프로그램 패키지를 업로드 하는 중 내부 서비스 패브릭 구성 요소에서 액세스할 수 있는 위치에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-125">Uploading hello application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="afb13-126">Tooverify hello 응용 프로그램 패키지를 로컬로 원할 경우 사용 하 여 hello [테스트 ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="afb13-126">If you want tooverify hello application package locally, use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="afb13-127">hello [복사 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 업로드 응용 프로그램 패키지 toohello 클러스터 이미지 저장소 hello 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-127">hello [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads hello application package toohello cluster image store.</span></span>
<span data-ttu-id="afb13-128">hello **Get ImageStoreConnectionStringFromClusterManifest** hello 서비스 패브릭 SDK PowerShell 모듈의 일부인 cmdlet을 사용 하는 tooget hello 이미지인 연결 문자열을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-128">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="afb13-129">tooimport hello SDK 모듈을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-129">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="afb13-130">Visual Studio 2015에서 *MyApplication*이라는 응용 프로그램을 빌드하고 패키지한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-130">Suppose you build and package an application named *MyApplication* in Visual Studio 2015.</span></span> <span data-ttu-id="afb13-131">기본적으로 hello 응용 프로그램 유형 이름은 ApplicationManifest.xml hello에 나열 된 "MyApplicationType"는 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-131">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="afb13-132">hello hello 필요한 응용 프로그램 매니페스트, 서비스 매니페스트 및 코드/config/데이터 패키지를 포함 하는 응용 프로그램 패키지에 있는 *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\ MyApplication\MyApplication\pkg\Debug*합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-132">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="afb13-133">hello 다음 명령은 나열 hello hello 응용 프로그램 패키지 내용의 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-133">hello following command lists hello contents of hello application package:</span></span>

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

<span data-ttu-id="afb13-134">Hello 응용 프로그램 패키지 큰 많은 파일의 경우, 다음을 할 수 있습니다 [압축](service-fabric-package-apps.md#compress-a-package)합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-134">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="afb13-135">hello 압축 hello 크기와 파일 hello 수가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-135">hello compression reduces hello size and hello number of files.</span></span>
<span data-ttu-id="afb13-136">hello 부작용은 해당 등록 및 등록을 취소 hello 응용 프로그램 종류는 경우 더욱 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-136">hello side effect is that registering and un-registering hello application type are faster.</span></span> <span data-ttu-id="afb13-137">업로드 시간이 느려질 수 있습니다 현재 hello 타임 toocompress hello 패키지를 포함 하는 경우에 특히.</span><span class="sxs-lookup"><span data-stu-id="afb13-137">Upload time may be slower currently, especially if you include hello time toocompress hello package.</span></span> 

<span data-ttu-id="afb13-138">패키지를 사용 하 여 toocompress hello 동일 [복사 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-138">toocompress a package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span> <span data-ttu-id="afb13-139">압축에서에서 수행할 수 있습니다 별도 업로드 hello를 사용 하 여 `SkipCopy` 플래그를 지정 하거나 hello와 함께 작업을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-139">Compression can be done separate from upload, by using hello `SkipCopy` flag, or together with hello upload operation.</span></span> <span data-ttu-id="afb13-140">압축된 패키지에 압축을 적용하면 아무런 변화가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="afb13-141">압축된 된 패키지를 사용 하 여 toouncompress hello 동일 [복사 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) hello로 명령을 `UncompressPackage` 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-141">toouncompress a compressed package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command with hello `UncompressPackage` switch.</span></span>

<span data-ttu-id="afb13-142">hello 다음 cmdlet 압축 hello 패키지 toohello 이미지 저장소를 복사 하지 않고 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-142">hello following cmdlet compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="afb13-143">hello 패키지는 이제 hello에 대 한 압축 된 파일을 포함 `Code` 및 `Config` 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-143">hello package now includes zipped files for hello `Code` and `Config` packages.</span></span> <span data-ttu-id="afb13-144">hello 응용 프로그램 및 서비스 매니페스트 hello 하지 압축 된, 많은 내부 작업 (예: 공유, 특정 유효성 검사에 대 한 응용 프로그램 유형 이름 및 버전 추출 패키지)에 필요 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-144">hello application and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="afb13-145">이동식 hello 매니페스트는 비효율적인 이러한 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-145">Zipping hello manifests would make these operations inefficient.</span></span>

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

<span data-ttu-id="afb13-146">대형 응용 프로그램 패키지에 대 한 hello 압축 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-146">For large application packages, hello compression takes time.</span></span> <span data-ttu-id="afb13-147">최상의 결과를 얻으려면 빠른 SSD 드라이브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="afb13-148">hello 압축 시간과 hello 압축 된 패키지의 hello 크기 또한 hello 패키지 내용에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-148">hello compression times and hello size of hello compressed package also differ based on hello package content.</span></span>
<span data-ttu-id="afb13-149">예를 들어 일부 패키지에는 초기 hello를 표시 하 고 hello 압축 시간으로 압축 된 패키지 크기 hello에 대 한 압축 통계 같습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-149">For example, here is compression statistics for some packages, which show hello initial and hello compressed package size, with hello compression time.</span></span>

|<span data-ttu-id="afb13-150">초기 크기(MB)</span><span class="sxs-lookup"><span data-stu-id="afb13-150">Initial size (MB)</span></span>|<span data-ttu-id="afb13-151">파일 수</span><span class="sxs-lookup"><span data-stu-id="afb13-151">File count</span></span>|<span data-ttu-id="afb13-152">압축 시간</span><span class="sxs-lookup"><span data-stu-id="afb13-152">Compression Time</span></span>|<span data-ttu-id="afb13-153">압축된 패키지 크기(MB)</span><span class="sxs-lookup"><span data-stu-id="afb13-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="afb13-154">100</span><span class="sxs-lookup"><span data-stu-id="afb13-154">100</span></span>|<span data-ttu-id="afb13-155">100</span><span class="sxs-lookup"><span data-stu-id="afb13-155">100</span></span>|<span data-ttu-id="afb13-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="afb13-156">00:00:03.3547592</span></span>|<span data-ttu-id="afb13-157">60</span><span class="sxs-lookup"><span data-stu-id="afb13-157">60</span></span>|
|<span data-ttu-id="afb13-158">512</span><span class="sxs-lookup"><span data-stu-id="afb13-158">512</span></span>|<span data-ttu-id="afb13-159">100</span><span class="sxs-lookup"><span data-stu-id="afb13-159">100</span></span>|<span data-ttu-id="afb13-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="afb13-160">00:00:16.3850303</span></span>|<span data-ttu-id="afb13-161">307</span><span class="sxs-lookup"><span data-stu-id="afb13-161">307</span></span>|
|<span data-ttu-id="afb13-162">1024</span><span class="sxs-lookup"><span data-stu-id="afb13-162">1024</span></span>|<span data-ttu-id="afb13-163">500</span><span class="sxs-lookup"><span data-stu-id="afb13-163">500</span></span>|<span data-ttu-id="afb13-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="afb13-164">00:00:32.5907950</span></span>|<span data-ttu-id="afb13-165">615</span><span class="sxs-lookup"><span data-stu-id="afb13-165">615</span></span>|
|<span data-ttu-id="afb13-166">2048</span><span class="sxs-lookup"><span data-stu-id="afb13-166">2048</span></span>|<span data-ttu-id="afb13-167">1000</span><span class="sxs-lookup"><span data-stu-id="afb13-167">1000</span></span>|<span data-ttu-id="afb13-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="afb13-168">00:01:04.3775554</span></span>|<span data-ttu-id="afb13-169">1231</span><span class="sxs-lookup"><span data-stu-id="afb13-169">1231</span></span>|
|<span data-ttu-id="afb13-170">5012</span><span class="sxs-lookup"><span data-stu-id="afb13-170">5012</span></span>|<span data-ttu-id="afb13-171">100</span><span class="sxs-lookup"><span data-stu-id="afb13-171">100</span></span>|<span data-ttu-id="afb13-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="afb13-172">00:02:45.2951288</span></span>|<span data-ttu-id="afb13-173">3074</span><span class="sxs-lookup"><span data-stu-id="afb13-173">3074</span></span>|

<span data-ttu-id="afb13-174">패키지 압축 되 면 필요에 따라 여러 서비스 패브릭 클러스터 또는 업로드 된 tooone 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-174">Once a package is compressed, it can be uploaded tooone or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="afb13-175">hello 배포 메커니즘은 압축 된 백업과 압축 되지 않은 패키지에 대 한 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-175">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="afb13-176">Hello 패키지 압축 된 경우 hello 클러스터 이미지 저장소에 따라서 저장 되 고 hello 응용 프로그램을 실행 하기 전에 hello 노드에서 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-176">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>


<span data-ttu-id="afb13-177">hello 다음 예제에서는 hello 패키지 toohello 이미지 저장소에 업로드 "MyApplicationV1" 라는 폴더:</span><span class="sxs-lookup"><span data-stu-id="afb13-177">hello following example uploads hello package toohello image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="afb13-178">hello **Get ImageStoreConnectionStringFromClusterManifest** hello 서비스 패브릭 SDK PowerShell 모듈의 일부인 cmdlet을 사용 하는 tooget hello 이미지인 연결 문자열을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-178">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="afb13-179">tooimport hello SDK 모듈을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-179">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="afb13-180">Hello를 지정 하지 않으면 *-ApplicationPackagePathInImageStore* hello 응용 프로그램 패키지 매개 변수는 hello 이미지 저장소에 hello "Debug" 폴더에 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-180">If you do not specify hello *-ApplicationPackagePathInImageStore* parameter, hello application package is copied into hello "Debug" folder in hello image store.</span></span>

<span data-ttu-id="afb13-181">hello 시간이 tooupload 패키지 여러 요인에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-181">hello time it takes tooupload a package differs depending on multiple factors.</span></span> <span data-ttu-id="afb13-182">이러한 요소 중 일부는 hello hello 패키지, 패키지 크기 hello 및 hello 파일 크기의 파일 수입니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-182">Some of these factors are hello number of files in hello package, hello package size, and hello file sizes.</span></span> <span data-ttu-id="afb13-183">hello 원본 컴퓨터와 hello 서비스 패브릭 클러스터 간의 네트워크 속도가 hello hello 업로드 시간에도 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-183">hello network speed between hello source machine and hello Service Fabric cluster also impacts hello upload time.</span></span> <span data-ttu-id="afb13-184">기본 시간 제한을 hello [복사 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 30 분입니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-184">hello default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minutes.</span></span>
<span data-ttu-id="afb13-185">에 따라 설명된 요소 hello, tooincrease hello 제한 시간을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-185">Depending on hello described factors, you may have tooincrease hello timeout.</span></span> <span data-ttu-id="afb13-186">Tooalso hello 복사 호출에서 hello 패키지를 압축 하는 경우 해야 hello 압축 시간을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-186">If you are compressing hello package in hello copy call, you need tooalso consider hello compression time.</span></span>

<span data-ttu-id="afb13-187">참조 [hello 이미지 저장소 연결 문자열을 이해](service-fabric-image-store-connection-string.md) 보충 정보에 대 한 hello 이미지 저장소 및 이미지 연결 문자열을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-187">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="afb13-188">Hello 응용 프로그램 패키지를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-188">Register hello application package</span></span>
<span data-ttu-id="afb13-189">hello 응용 프로그램 유형 및 버전 hello 응용 프로그램 패키지를 등록 하면 사용 하기 위해 사용할 수 있게 하는 hello 응용 프로그램 매니페스트에 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-189">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="afb13-190">hello 시스템 hello 이전 단계에서 업로드 된 hello 패키지가, hello 패키지를 확인, hello 패키지 내용 처리 읽고 처리 하는 hello 패키지 tooan 내부 시스템 위치에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-190">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="afb13-191">Hello 실행 [레지스터 ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister hello hello 클러스터에서 응용 프로그램 종류 및 배포에 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-191">Run hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister hello application type in hello cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="afb13-192">"MyApplicationV1"는 hello 응용 프로그램 패키지가 위치한 hello 이미지 저장소 hello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-192">"MyApplicationV1" is hello folder in hello image store where hello application package is located.</span></span> <span data-ttu-id="afb13-193">hello 응용 프로그램 유형 이름이 "MyApplicationType" 고 버전이 "1.0.0" (둘 다에 있습니다. 응용 프로그램 매니페스트 hello)이 이제 hello 클러스터에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-193">hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) is now registered in hello cluster.</span></span>

<span data-ttu-id="afb13-194">hello [레지스터 ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 명령은 hello 시스템에 성공적으로 등록 된 hello 응용 프로그램 패키지 한 후에 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-194">hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command returns only after hello system has successfully registered hello application package.</span></span> <span data-ttu-id="afb13-195">시간 등록은 hello 크기와 hello 응용 프로그램 패키지의 내용에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-195">How long registration takes depends on hello size and contents of hello application package.</span></span> <span data-ttu-id="afb13-196">필요한 경우 hello **-TimeoutSec** 매개 변수를 사용 하는 toosupply 긴 시간 제한 수 (hello 기본 제한 시간은 60 초)입니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-196">If needed, hello **-TimeoutSec** parameter can be used toosupply a longer timeout (hello default timeout is 60 seconds).</span></span>

<span data-ttu-id="afb13-197">패키지 또는 hello를 사용 하 여 시간 초과 발생 하는 경우 큰 응용 프로그램의 경우 **-Async** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-197">If you have a large application package or if you are experiencing timeouts, use hello **-Async** parameter.</span></span> <span data-ttu-id="afb13-198">hello 명령은 hello 클러스터 hello 등록 명령을 수락 하 고 필요에 따라 hello 처리가 계속를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-198">hello command returns when hello cluster accepts hello register command, and hello processing continues as needed.</span></span>
<span data-ttu-id="afb13-199">hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) 명령은 모든 성공적으로 등록 된 응용 프로그램 유형 버전 및 해당 등록 상태를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-199">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="afb13-200">이 명령은 toodetermine hello 등록 수행 되는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-200">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a><span data-ttu-id="afb13-201">Hello 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="afb13-201">Create hello application</span></span>
<span data-ttu-id="afb13-202">Hello를 사용 하 여 성공적으로 등록 된 모든 응용 프로그램 종류 버전에서 응용 프로그램을 인스턴스화할 수 [새로 ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="afb13-202">You can instantiate an application from any application type version that has been registered successfully by using hello [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="afb13-203">각 응용 프로그램의 hello 이름 hello로 시작 해야 *"fabric:"* 구성표 및 각 응용 프로그램 인스턴스에 대해 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-203">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance.</span></span> <span data-ttu-id="afb13-204">Hello 대상 응용 프로그램 종류의 응용 프로그램 매니페스트 hello에에서 정의 된 기본 서비스 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-204">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="afb13-205">등록된 응용 프로그램 형식의 주어진 어떤 버전에 대해서도 여러 개의 응용 프로그램 인스턴스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-205">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="afb13-206">각 응용 프로그램 인스턴스는 자체 작업 디렉터리 및 프로세스와는 별도로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-206">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="afb13-207">hello를 실행 하는 hello 클러스터에서 실행 하는 앱 및 서비스 이라는 toosee [Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) 및 [Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="afb13-207">toosee which named apps and services are running in hello cluster, run hello [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span></span>

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

## <a name="remove-an-application"></a><span data-ttu-id="afb13-208">응용 프로그램 제거</span><span class="sxs-lookup"><span data-stu-id="afb13-208">Remove an application</span></span>
<span data-ttu-id="afb13-209">응용 프로그램 인스턴스가 필요 하지 않은 경우 제거할 수 없습니다 영구적으로 hello를 사용 하 여 이름 [제거 ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="afb13-209">When an application instance is no longer needed, you can permanently remove it by name using hello [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="afb13-210">[제거 ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) 도, 영구적으로 모든 서비스 상태를 제거 하는 toohello 응용 프로그램에 포함 된 모든 서비스를 자동으로 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span> 

> [!WARNING]
> <span data-ttu-id="afb13-211">이 작업은 되돌릴 수 없으며 응용 프로그램 상태는 복구할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-211">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="afb13-212">응용 프로그램 유형 등록 취소</span><span class="sxs-lookup"><span data-stu-id="afb13-212">Unregister an application type</span></span>
<span data-ttu-id="afb13-213">Hello를 사용 하 여 hello 응용 프로그램 종류를 등록 취소 해야 응용 프로그램 종류의 특정 버전은 더 이상 필요 없는, [등록 취소 ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="afb13-213">When a particular version of an application type is no longer needed, you should unregister hello application type using hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="afb13-214">등록을 취소 사용 하지 않는 응용 프로그램 종류 버전 저장소 공간 hello 이미지 저장소에서 사용 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-214">Unregistering unused application types releases storage space used by hello image store.</span></span> <span data-ttu-id="afb13-215">응용 프로그램 형식은 이에 대해 인스턴스화된 응용 프로그램이나 이를 참조하는 보류 중인 응용 프로그램이 없는 한 등록 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-215">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="afb13-216">실행 [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee hello 응용 프로그램 종류는 현재 hello 클러스터에 등록 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-216">Run [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee hello application types currently registered in hello cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="afb13-217">실행 [등록 취소 ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister 특정 응용 프로그램 종류:</span><span class="sxs-lookup"><span data-stu-id="afb13-217">Run [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="afb13-218">Hello 이미지 저장소에서 응용 프로그램 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-218">Remove an application package from hello image store</span></span>
<span data-ttu-id="afb13-219">응용 프로그램 패키지 더 이상 필요 하면 시스템 리소스를 hello 이미지 저장소 toofree에서 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-219">When an application package is no longer needed, you can delete it from hello image store toofree up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="afb13-220">문제 해결</span><span class="sxs-lookup"><span data-stu-id="afb13-220">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="afb13-221">Copy-ServiceFabricApplicationPackage가 ImageStoreConnectionString을 요청함</span><span class="sxs-lookup"><span data-stu-id="afb13-221">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="afb13-222">서비스 패브릭 SDK 환경 hello hello 기본값을 설정 하 고 올바른 이미 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-222">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="afb13-223">하지만 해당 hello 서비스 패브릭 클러스터를 사용 하 여 모든 명령에 대 한 hello ImageStoreConnectionString 해야 hello 값 필요한 경우 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-223">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="afb13-224">Hello ImageStoreConnectionString hello 클러스터 매니페스트에서 찾을 수 있습니다 hello를 사용 하 여 검색 [Get ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) 및 Get ImageStoreConnectionStringFromClusterManifest 명령:</span><span class="sxs-lookup"><span data-stu-id="afb13-224">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="afb13-225">hello **Get ImageStoreConnectionStringFromClusterManifest** hello 서비스 패브릭 SDK PowerShell 모듈의 일부인 cmdlet을 사용 하는 tooget hello 이미지인 연결 문자열을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-225">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="afb13-226">tooimport hello SDK 모듈을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-226">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="afb13-227">hello ImageStoreConnectionString은 hello 클러스터 매니페스트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-227">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="afb13-228">참조 [hello 이미지 저장소 연결 문자열을 이해](service-fabric-image-store-connection-string.md) 보충 정보에 대 한 hello 이미지 저장소 및 이미지 연결 문자열을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-228">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="afb13-229">대형 응용 프로그램 패키지 배포</span><span class="sxs-lookup"><span data-stu-id="afb13-229">Deploy large application package</span></span>
<span data-ttu-id="afb13-230">문제: 대형 응용 프로그램 패키지(GB 단위)에 대한 [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 시간이 초과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-230">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="afb13-231">다음을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="afb13-231">Try:</span></span>
- <span data-ttu-id="afb13-232">[Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 명령에 `TimeoutSec` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-232">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="afb13-233">기본적으로 hello 제한 시간 30 분입니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-233">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="afb13-234">원본 컴퓨터와 클러스터 간에 hello 네트워크 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-234">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="afb13-235">Hello 연결이 느린 경우에 컴퓨터를 사용 하 여 더 나은 네트워크 연결을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-235">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="afb13-236">Hello 클라이언트 컴퓨터가 hello 클러스터와 다른 지역에 있는 경우에 hello 클러스터와 가깝거나 동일한 지역에 클라이언트 컴퓨터를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-236">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="afb13-237">외부 제한에 도달하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-237">Check if you are hitting external throttling.</span></span> <span data-ttu-id="afb13-238">예를 들어 hello 이미지 저장소에 구성 된 toouse azure 저장소가, 업로드 제한 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-238">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="afb13-239">문제: 패키지 업로드가 성공적으로 완료되었지만 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 시간이 초과되었습니다. 다음을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="afb13-239">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out. Try:</span></span>
- <span data-ttu-id="afb13-240">[Hello 패키지를 압축](service-fabric-package-apps.md#compress-a-package) toohello 이미지 저장소를 복사 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="afb13-240">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="afb13-241">hello 압축 hello 크기가 줄어들고에 hello 트래픽 양이 감소 하 고 해당 서비스 패브릭 작업 hello 수의 파일을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-241">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="afb13-242">hello 업로드 작업 (특히 포함 하는 경우 hello 압축 시간)에 속도가 느려질 수 있습니다, 하지만 등록 및 등록을 취소할 hello 응용 프로그램 종류는 더 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-242">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="afb13-243">[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)에 `TimeoutSec` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-243">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="afb13-244">[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)에 `Async` 스위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-244">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="afb13-245">hello 명령은 hello 클러스터 hello 명령을 수락 하 고 hello 응용 프로그램 종류의 hello 등록 계속 비동기식으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-245">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span> <span data-ttu-id="afb13-246">이러한 이유로 있습니다 없습니다 필요 toospecify 정하도록이 경우.</span><span class="sxs-lookup"><span data-stu-id="afb13-246">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="afb13-247">hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) 명령은 모든 성공적으로 등록 된 응용 프로그램 유형 버전 및 해당 등록 상태를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-247">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="afb13-248">이 명령은 toodetermine hello 등록 수행 되는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-248">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="afb13-249">많은 파일이 있는 응용 프로그램 패키지 배포</span><span class="sxs-lookup"><span data-stu-id="afb13-249">Deploy application package with many files</span></span>
<span data-ttu-id="afb13-250">문제: 많은 파일(1,000개 단위)이 있는 응용 프로그램 패키지에 대한 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) 시간이 초과되었습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-250">Issue: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="afb13-251">다음을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="afb13-251">Try:</span></span>
- <span data-ttu-id="afb13-252">[Hello 패키지를 압축](service-fabric-package-apps.md#compress-a-package) toohello 이미지 저장소를 복사 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="afb13-252">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="afb13-253">hello 압축 hello 파일 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-253">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="afb13-254">[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)에 `TimeoutSec` 매개 변수를 사용하여 더 긴 시간 제한을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-254">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="afb13-255">[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)에 `Async` 스위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-255">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="afb13-256">hello 명령은 hello 클러스터 hello 명령을 수락 하 고 hello 응용 프로그램 종류의 hello 등록 계속 비동기식으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-256">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span>
<span data-ttu-id="afb13-257">이러한 이유로 있습니다 없습니다 필요 toospecify 정하도록이 경우.</span><span class="sxs-lookup"><span data-stu-id="afb13-257">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="afb13-258">hello [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) 명령은 모든 성공적으로 등록 된 응용 프로그램 유형 버전 및 해당 등록 상태를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-258">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="afb13-259">이 명령은 toodetermine hello 등록 수행 되는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afb13-259">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a><span data-ttu-id="afb13-260">다음 단계</span><span class="sxs-lookup"><span data-stu-id="afb13-260">Next steps</span></span>
[<span data-ttu-id="afb13-261">서비스 패브릭 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="afb13-261">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="afb13-262">서비스 패브릭 상태 소개</span><span class="sxs-lookup"><span data-stu-id="afb13-262">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="afb13-263">서비스 패브릭 서비스 진단 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="afb13-263">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="afb13-264">서비스 패브릭에서 응용 프로그램 모델링</span><span class="sxs-lookup"><span data-stu-id="afb13-264">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
