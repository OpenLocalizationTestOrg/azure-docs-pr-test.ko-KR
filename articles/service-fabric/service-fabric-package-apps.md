---
title: "Azure Service Fabric 앱 패키징 | Microsoft Docs"
description: "클러스터에 배포하기 전에 Service Fabric 응용 프로그램을 패키지하는 방법입니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: 486a27d7ca576c8fe1552c02eb24ece6b8bb2ba8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="package-an-application"></a><span data-ttu-id="a2d37-103">응용 프로그램 패키지 작성</span><span class="sxs-lookup"><span data-stu-id="a2d37-103">Package an application</span></span>
<span data-ttu-id="a2d37-104">이 문서에서는 Service Fabric 응용 프로그램을 패키지하고 배포를 준비하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-104">This article describes how to package a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="a2d37-105">패키지 레이아웃</span><span class="sxs-lookup"><span data-stu-id="a2d37-105">Package layout</span></span>
<span data-ttu-id="a2d37-106">Service Fabric 클러스터에 배포할 수 있도록 응용 프로그램 매니페스트, 하나 이상의 서비스 매니페스트 및 기타 필요한 패키지 파일을 특정 레이아웃으로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-106">The application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="a2d37-107">이 문서에 예로 제공된 매니페스트를 다음 디렉터리 구조로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-107">The example manifests in this article would need to be organized in the following directory structure:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

<span data-ttu-id="a2d37-108">폴더는 각 해당 요소의 **Name** 특성과 일치하도록 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-108">The folders are named to match the **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="a2d37-109">예를 들어 서비스 매니페스트에 이름이 각각 **MyCodeA**와 **MyCodeB**인 코드 패키지가 두 개 있으면 이와 동일한 이름의 폴더 두 개에 각 코드 패키지에 필요한 바이너리가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-109">For example, if the service manifest contained two code packages with the names **MyCodeA** and **MyCodeB**, then two folders with the same names would contain the necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="a2d37-110">SetupEntryPoint 사용</span><span class="sxs-lookup"><span data-stu-id="a2d37-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="a2d37-111">**SetupEntryPoint** 를 사용하는 일반적인 시나리오는 서비스를 시작하기 전에 실행 파일을 실행해야 하는 경우 또는 높은 권한을 사용하여 작업을 수행해야 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-111">Typical scenarios for using **SetupEntryPoint** are when you need to run an executable before the service starts or you need to perform an operation with elevated privileges.</span></span> <span data-ttu-id="a2d37-112">예:</span><span class="sxs-lookup"><span data-stu-id="a2d37-112">For example:</span></span>

* <span data-ttu-id="a2d37-113">서비스 실행 파일에 필요한 환경 변수를 설정하고 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-113">Setting up and initializing environment variables that the service executable needs.</span></span> <span data-ttu-id="a2d37-114">이것은 Service Fabric 프로그래밍 모델을 통해 작성된 실행 파일에만 국한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-114">It is not limited to only executables written via the Service Fabric programming models.</span></span> <span data-ttu-id="a2d37-115">예를 들어 npm.exe 파일에는 node.js 응용 프로그램 배포를 위해 구성되는 환경 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="a2d37-116">보안 인증서를 설치하여 액세스 제어를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="a2d37-117">**SetupEntryPoint**를 구성하는 방법에 대한 자세한 내용은 [서비스 설치 진입점에 대한 정책 구성](service-fabric-application-runas-security.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a2d37-117">For more information on how to configure the **SetupEntryPoint**, see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="a2d37-118">구성</span><span class="sxs-lookup"><span data-stu-id="a2d37-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="a2d37-119">Visual Studio를 사용하여 패키지 빌드</span><span class="sxs-lookup"><span data-stu-id="a2d37-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="a2d37-120">Visual Studio 2015를 사용하여 응용 프로그램을 만드는 경우 패키지 명령을 사용하여 위에서 설명한 레이아웃과 일치하는 패키지를 자동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-120">If you use Visual Studio 2015 to create your application, you can use the Package command to automatically create a package that matches the layout described above.</span></span>

<span data-ttu-id="a2d37-121">패키지를 만들려면 솔루션 탐색기에서 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭하고 아래와 같이 패키지 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-121">To create a package, right-click the application project in Solution Explorer and choose the Package command, as shown below:</span></span>

![Visual Studio를 통해 응용 프로그램 패키징][vs-package-command]

<span data-ttu-id="a2d37-123">패키징이 완료되면 **출력** 창에서 패키지의 위치를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-123">When packaging is complete, you can find the location of the package in the **Output** window.</span></span> <span data-ttu-id="a2d37-124">Visual Studio에서 응용 프로그램을 배포 또는 디버깅할 때 패키징 단계가 자동으로 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-124">The packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="a2d37-125">명령줄로 패키지 빌드</span><span class="sxs-lookup"><span data-stu-id="a2d37-125">Build a package by command line</span></span>
<span data-ttu-id="a2d37-126">`msbuild.exe`를 사용하여 응용 프로그램을 프로그래밍 방식으로 패키징할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-126">It is also possible to programmatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="a2d37-127">내부적으로 보면 Visual Studio가 실행하고 있으므로 출력은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-127">Under the hood, Visual Studio is running it so the output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-the-package"></a><span data-ttu-id="a2d37-128">패키지 테스트</span><span class="sxs-lookup"><span data-stu-id="a2d37-128">Test the package</span></span>
<span data-ttu-id="a2d37-129">[Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) 명령을 사용하여 PowerShell을 통해 로컬에서 패키지 구조를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-129">You can verify the package structure locally through PowerShell by using the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="a2d37-130">이 명령은 매니페스트 구문 해석 문제를 확인하고 모든 참조의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="a2d37-131">이 명령은 패키지에 포함된 디렉터리와 파일의 구조적 정확성만 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-131">This command only verifies the structural correctness of the directories and files in the package.</span></span>
<span data-ttu-id="a2d37-132">필요한 파일이 모두 있는지 확인한 후에 코드 또는 데이터 패키지 내용을 검사하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-132">It doesn't verify any of the code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : The EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="a2d37-133">이 오류는 서비스 매니페스트 *SetupEntryPoint* 에서 참조되는 **MySetup.bat** 파일이 코드 패키지에 없다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-133">This error shows that the *MySetup.bat* file referenced in the service manifest **SetupEntryPoint** is missing from the code package.</span></span> <span data-ttu-id="a2d37-134">누락된 파일이 추가되면, 응용 프로그램 검사가 통과됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-134">After the missing file is added, the application verification passes:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

<span data-ttu-id="a2d37-135">응용 프로그램에 [응용 프로그램 매개 변수](service-fabric-manage-multiple-environment-app-configuration.md)가 정의되어 있으면 적절한 유효성 검사를 위해 [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps)에 이 매개 변수를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="a2d37-136">응용 프로그램을 배포할 클러스터를 알고 있는 경우 `ImageStoreConnectionString` 매개 변수에 전달하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-136">If you know the cluster where the application will be deployed, it is recommended you pass in the `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="a2d37-137">이 경우 이미 클러스터에서 실행 중인 이전 버전의 응용 프로그램에 대해서도 패키지의 유효성이 검사됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-137">In this case, the package is also validated against previous versions of the application that are already running in the cluster.</span></span> <span data-ttu-id="a2d37-138">예를 들어 유효성 검사를 통해 동일한 버전이지만 다른 내용이 포함된 패키지를 이미 배포했는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-138">For example, the validation can detect whether a package with the same version but different content was already deployed.</span></span>  

<span data-ttu-id="a2d37-139">응용 프로그램이 올바르게 패키지되고 유효성 검사를 통과하는 경우 압축이 필요하면 파일의 크기와 수를 기반으로 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-139">Once the application is packaged correctly and passes validation, evaluate based on the size and the number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="a2d37-140">패키지 압축</span><span class="sxs-lookup"><span data-stu-id="a2d37-140">Compress a package</span></span>
<span data-ttu-id="a2d37-141">패키지가 크거나 파일이 많은 경우 이를 압축하여 더 빠르게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="a2d37-142">압축은 파일 수와 패키지 크기를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-142">Compression reduces the number of files and the package size.</span></span>
<span data-ttu-id="a2d37-143">압축된 응용 프로그램 패키지의 경우 [응용 프로그램 패키지 업로드](service-fabric-deploy-remove-applications.md#upload-the-application-package) 작업에 걸리는 시간이 압축되지 않은 패키지 업로드에 비해 더 길어질 수 있지만(특히 압축 시간이 포함되는 경우), [등록](service-fabric-deploy-remove-applications.md#register-the-application-package) 및 [응용 프로그램 유형 등록 취소](service-fabric-deploy-remove-applications.md#unregister-an-application-type)는 압축된 응용 프로그램 패키지가 더 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-143">For a compressed application package, [Uploading the application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared to uploading the uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering the application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="a2d37-144">배포 메커니즘은 압축된 패키지와 압축되지 않은 패키지에 대해 모두 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-144">The deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="a2d37-145">압축된 패키지는 클러스터 이미지 저장소에 그대로 저장되며, 먼저 노드에서 압축이 풀린 후에 응용 프로그램이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-145">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span></span>
<span data-ttu-id="a2d37-146">압축은 유효한 Service Fabric 패키지를 압축된 버전으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-146">The compression replaces the valid Service Fabric package with the compressed version.</span></span> <span data-ttu-id="a2d37-147">폴더에 대한 쓰기 권한을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-147">The folder must allow write permissions.</span></span> <span data-ttu-id="a2d37-148">이미 압축된 패키지에 압축을 실행하면 아무런 변화가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="a2d37-149">`CompressPackage` 스위치와 함께 [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) PowerShell 명령을 실행하여 패키지를 압축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-149">You can compress a package by running the Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="a2d37-150">`UncompressPackage` 스위치를 사용하면 동일한 명령으로 패키지의 압축을 풀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-150">You can uncompress the package with the same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="a2d37-151">다음 명령은 패키지를 이미지 저장소에 복사하지 않고 압축합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-151">The following command compresses the package without copying it to the image store.</span></span> <span data-ttu-id="a2d37-152">`SkipCopy` 플래그 없이 [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)를 사용하여 필요에 따라 하나 이상의 Service Fabric 클러스터에 압축된 패키지를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-152">You can copy a compressed package to one or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without the `SkipCopy` flag.</span></span>
<span data-ttu-id="a2d37-153">이제 패키지에 `code`, `config` 및 `data` 패키지의 압축 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-153">The package now includes zipped files for the `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="a2d37-154">응용 프로그램 매니페스트 및 서비스 매니페스트는 많은 내부 작업(특정 유효성 검사를 위한 패키지 공유, 응용 프로그램 유형 이름 및 버전 추출 등)에 필요하기 때문에 압축되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-154">The application manifest and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="a2d37-155">매니페스트를 압축하면 이러한 작업이 비효율적으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-155">Zipping the manifests would make these operations inefficient.</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

<span data-ttu-id="a2d37-156">또는 [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)를 사용하여 한번에 패키지를 압축하고 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-156">Alternatively, you can compress and copy the package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="a2d37-157">패키지가 크면 패키지를 압축하고 클러스터에 업로드하는 데 걸리는 시간을 충분히 허용할 만큼 긴 시간 제한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-157">If the package is large, provide a high enough timeout to allow time for both the package compression and the upload to the cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="a2d37-158">내부적으로 Service Fabric은 유효성 검사를 위해 응용 프로그램 패키지에 대한 체크섬을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-158">Internally, Service Fabric computes checksums for the application packages for validation.</span></span> <span data-ttu-id="a2d37-159">압축을 사용할 때 체크섬은 각 패키지의 압축된 버전에서 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-159">When using compression, the checksums are computed on the zipped versions of each package.</span></span>
<span data-ttu-id="a2d37-160">압축되지 않은 버전의 응용 프로그램 패키지를 복사했고 동일한 패키지에 대해 압축을 사용하려는 경우 체크섬 불일치가 발생하지 않도록 `code`, `config` 및 `data` 패키지 버전을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-160">If you copied an uncompressed version of your application package, and you want to use compression for the same package, you must change the versions of the `code`, `config`, and `data` packages to avoid checksum mismatch.</span></span> <span data-ttu-id="a2d37-161">패키지가 변경되지 않은 경우 버전을 변경하는 대신 [diff 프로비저닝](service-fabric-application-upgrade-advanced.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-161">If the packages are unchanged, instead of changing the version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="a2d37-162">이 옵션을 사용하는 경우 변경되지 않은 패키지를 포함하지 말고 서비스 매니페스트에서 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-162">With this option, do not include the unchanged package instead reference it from the service manifest.</span></span>

<span data-ttu-id="a2d37-163">마찬가지로 압축된 버전의 패키지를 업로드했고 압축되지 않은 패키지를 사용하려는 경우 체크섬이 일치하지 않도록 버전을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-163">Similarly, if you uploaded a compressed version of the package and you want to use an uncompressed package, you must update the versions to avoid the checksum mismatch.</span></span>

<span data-ttu-id="a2d37-164">이제 패키지를 올바르게 패키지하고, 유효성을 검사하고, 압축하여(필요한 경우) 하나 이상의 Service Fabric 클러스터에 [배포](service-fabric-deploy-remove-applications.md)할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-164">The package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) to one or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="a2d37-165">Visual Studio를 사용하여 배포하는 경우 패키지 압축</span><span class="sxs-lookup"><span data-stu-id="a2d37-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="a2d37-166">`CopyPackageParameters` 요소를 게시 프로필에 추가하여 배포 중인 패키지를 압축하고 `CompressPackage` 특성을 `true`으로 설정하도록 Visual Studio에 지시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-166">You can instruct Visual Studio to compress packages on deployment, by adding the `CopyPackageParameters` element to your publish profile, and set the `CompressPackage` attribute to `true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="a2d37-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a2d37-167">Next steps</span></span>
<span data-ttu-id="a2d37-168">[응용 프로그램 배포 및 제거][10]에서는 PowerShell을 사용하여 응용 프로그램 인스턴스를 관리하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-168">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances</span></span>

<span data-ttu-id="a2d37-169">[여러 환경에 대한 응용 프로그램 매개 변수 관리][11]에서는 여러 응용 프로그램 인스턴스의 매개 변수 및 환경 변수를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-169">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="a2d37-170">[응용 프로그램에 대한 보안 정책 구성][12]에서는 액세스를 제한하는 보안 정책에 따라 서비스를 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a2d37-170">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
