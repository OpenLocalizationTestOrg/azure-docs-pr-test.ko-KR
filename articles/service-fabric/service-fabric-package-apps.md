---
title: "Azure 서비스 패브릭 응용 프로그램 aaaPackage | Microsoft Docs"
description: "어떻게 toopackage tooa 클러스터를 배포 하기 전에 서비스 패브릭 응용 프로그램입니다."
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
ms.openlocfilehash: b3918e1e25e532acdc9440855213e1fa364ea000
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="package-an-application"></a><span data-ttu-id="29bbc-103">응용 프로그램 패키지 작성</span><span class="sxs-lookup"><span data-stu-id="29bbc-103">Package an application</span></span>
<span data-ttu-id="29bbc-104">이 문서에서는 설명 방법을 toopackage 서비스 패브릭 응용 프로그램 배포에 대 한 준비 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-104">This article describes how toopackage a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="29bbc-105">패키지 레이아웃</span><span class="sxs-lookup"><span data-stu-id="29bbc-105">Package layout</span></span>
<span data-ttu-id="29bbc-106">hello 응용 프로그램 매니페스트, 하나 이상의 서비스 매니페스트 및 기타 필수 패키지 배포를 서비스 패브릭 클러스터에 대 한 특정 레이아웃으로 파일을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-106">hello application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="29bbc-107">이 문서의 예제 매니페스트 hello toobe hello 디렉터리 구조를 다음에 구성 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-107">hello example manifests in this article would need toobe organized in hello following directory structure:</span></span>

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

<span data-ttu-id="29bbc-108">hello 폴더의 이름은 각각 toomatch hello **이름** 각 해당 요소의 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-108">hello folders are named toomatch hello **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="29bbc-109">예를 들어 hello 서비스 매니페스트 포함 된 두 개의 코드 패키지 hello 이름의 **MyCodeA** 및 **MyCodeB**, 동일한 이름에는 hello 사용 하 여 두 개의 폴더 hello 각 코드에 대 한 필요한 이진 파일 한 다음 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-109">For example, if hello service manifest contained two code packages with hello names **MyCodeA** and **MyCodeB**, then two folders with hello same names would contain hello necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="29bbc-110">SetupEntryPoint 사용</span><span class="sxs-lookup"><span data-stu-id="29bbc-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="29bbc-111">사용에 대 한 일반적인 시나리오 **SetupEntryPoint** toorun hello 서비스가 시작 되기 전에 실행 파일 이거나 tooperform 상승 된 권한으로 작업 해야 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="29bbc-111">Typical scenarios for using **SetupEntryPoint** are when you need toorun an executable before hello service starts or you need tooperform an operation with elevated privileges.</span></span> <span data-ttu-id="29bbc-112">예:</span><span class="sxs-lookup"><span data-stu-id="29bbc-112">For example:</span></span>

* <span data-ttu-id="29bbc-113">설정 하 고 서비스의 실행 요구 hello 환경 변수를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-113">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="29bbc-114">Hello 서비스 패브릭 프로그래밍 모델을 통해 작성 된 제한 tooonly 실행 파일이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-114">It is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="29bbc-115">예를 들어 npm.exe 파일에는 node.js 응용 프로그램 배포를 위해 구성되는 환경 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="29bbc-116">보안 인증서를 설치하여 액세스 제어를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="29bbc-117">방법에 대 한 자세한 내용은 tooconfigure hello **SetupEntryPoint**, 참조 [서비스 설치 시작 지점에 대 한 hello 정책 구성](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="29bbc-117">For more information on how tooconfigure hello **SetupEntryPoint**, see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="29bbc-118">구성</span><span class="sxs-lookup"><span data-stu-id="29bbc-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="29bbc-119">Visual Studio를 사용하여 패키지 빌드</span><span class="sxs-lookup"><span data-stu-id="29bbc-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="29bbc-120">Visual Studio 2015 toocreate 응용 프로그램을 사용 하는 경우 hello 명령 tooautomatically 위에서 설명한 hello 레이아웃와 일치 하는 패키지를 만든 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-120">If you use Visual Studio 2015 toocreate your application, you can use hello Package command tooautomatically create a package that matches hello layout described above.</span></span>

<span data-ttu-id="29bbc-121">toocreate 패키지를 솔루션 탐색기에서 hello 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 아래와 같이 hello 패키지 명령을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-121">toocreate a package, right-click hello application project in Solution Explorer and choose hello Package command, as shown below:</span></span>

![Visual Studio를 통해 응용 프로그램 패키징][vs-package-command]

<span data-ttu-id="29bbc-123">패키징 완료 되 면 hello에서 hello 패키지의 hello 위치를 찾을 수 있습니다 **출력** 창.</span><span class="sxs-lookup"><span data-stu-id="29bbc-123">When packaging is complete, you can find hello location of hello package in hello **Output** window.</span></span> <span data-ttu-id="29bbc-124">패키징 단계 hello 배포 하거나 Visual Studio에서 응용 프로그램을 디버깅할 때 자동으로 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-124">hello packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="29bbc-125">명령줄로 패키지 빌드</span><span class="sxs-lookup"><span data-stu-id="29bbc-125">Build a package by command line</span></span>
<span data-ttu-id="29bbc-126">사용 하 여 응용 프로그램을 가능한 tooprogrammatically 패키지 이기도 `msbuild.exe`합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-126">It is also possible tooprogrammatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="29bbc-127">Hello 내부적 Visual Studio 실행 되어 그 hello 출력은 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-127">Under hello hood, Visual Studio is running it so hello output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a><span data-ttu-id="29bbc-128">테스트 hello 패키지</span><span class="sxs-lookup"><span data-stu-id="29bbc-128">Test hello package</span></span>
<span data-ttu-id="29bbc-129">Hello를 사용 하 여 PowerShell 통해 로컬로 hello 패키지 구조를 확인할 수 있습니다 [테스트 ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-129">You can verify hello package structure locally through PowerShell by using hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="29bbc-130">이 명령은 매니페스트 구문 해석 문제를 확인하고 모든 참조의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="29bbc-131">이 명령은 hello 디렉터리 및 hello 패키지 파일의에서 압축 hello 구조적 올바른지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-131">This command only verifies hello structural correctness of hello directories and files in hello package.</span></span>
<span data-ttu-id="29bbc-132">필요한 모든 파일이 있는지 확인 하는 중 다음 hello 코드 또는 데이터 패키지 내용 중 하나를 확인 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-132">It doesn't verify any of hello code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="29bbc-133">이 오류는 해당 hello 표시 *MySetup.bat* hello 서비스 매니페스트에서 참조 하는 파일 **SetupEntryPoint** hello 코드 패키지에서 누락 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-133">This error shows that hello *MySetup.bat* file referenced in hello service manifest **SetupEntryPoint** is missing from hello code package.</span></span> <span data-ttu-id="29bbc-134">Hello 누락 된 파일이 추가 되 면 hello 응용 프로그램 검증 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-134">After hello missing file is added, hello application verification passes:</span></span>

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

<span data-ttu-id="29bbc-135">응용 프로그램에 [응용 프로그램 매개 변수](service-fabric-manage-multiple-environment-app-configuration.md)가 정의되어 있으면 적절한 유효성 검사를 위해 [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps)에 이 매개 변수를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="29bbc-136">Hello 클러스터 hello 응용 프로그램 배포 될 위치를 알고 있는 경우 것이 좋습니다 hello 전달 `ImageStoreConnectionString` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-136">If you know hello cluster where hello application will be deployed, it is recommended you pass in hello `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="29bbc-137">이 경우 hello 패키지 유효성이 검사 된다는 hello 클러스터에서 이미 실행 중인 이전 버전의 hello 응용 프로그램에 대해 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-137">In this case, hello package is also validated against previous versions of hello application that are already running in hello cluster.</span></span> <span data-ttu-id="29bbc-138">Hello 유효성 검사를 패키지 여부를 감지할 수는 예를 들어 hello와 동일한 버전 하지만 서로 다른 내용을 이미 배포 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-138">For example, hello validation can detect whether a package with hello same version but different content was already deployed.</span></span>  

<span data-ttu-id="29bbc-139">패키지 하 고 유효성 검사를 통과 하는 hello 응용 프로그램을 평가할 압축 필요 하지 않으면 hello 크기와 파일의 hello 수에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-139">Once hello application is packaged correctly and passes validation, evaluate based on hello size and hello number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="29bbc-140">패키지 압축</span><span class="sxs-lookup"><span data-stu-id="29bbc-140">Compress a package</span></span>
<span data-ttu-id="29bbc-141">패키지가 크거나 파일이 많은 경우 이를 압축하여 더 빠르게 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="29bbc-142">압축 파일 및 패키지 크기의 hello hello 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-142">Compression reduces hello number of files and hello package size.</span></span>
<span data-ttu-id="29bbc-143">압축 된 응용 프로그램 패키지에 대 한 [hello 응용 프로그램 패키지 업로드 중](service-fabric-deploy-remove-applications.md#upload-the-application-package) 비교 toouploading 더 이상 압축 되지 않은 패키지 (특별 하 게 하는 경우 압축 시간은에 포함) hello, 걸릴 수 있습니다 하지만 [를등록하는중](service-fabric-deploy-remove-applications.md#register-the-application-package) 및 [등록을 취소 hello 응용 프로그램 종류](service-fabric-deploy-remove-applications.md#unregister-an-application-type) 압축 된 응용 프로그램 패키지에 대 한 더 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-143">For a compressed application package, [Uploading hello application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared toouploading hello uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering hello application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="29bbc-144">hello 배포 메커니즘은 압축 된 백업과 압축 되지 않은 패키지에 대 한 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-144">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="29bbc-145">Hello 패키지 압축 된 경우 hello 클러스터 이미지 저장소에 따라서 저장 되 고 hello 응용 프로그램을 실행 하기 전에 hello 노드에서 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-145">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>
<span data-ttu-id="29bbc-146">hello 압축 hello 압축 된 버전으로 hello 올바른 서비스 패브릭 패키지를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-146">hello compression replaces hello valid Service Fabric package with hello compressed version.</span></span> <span data-ttu-id="29bbc-147">hello 폴더에 대 한 쓰기 권한을 허용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-147">hello folder must allow write permissions.</span></span> <span data-ttu-id="29bbc-148">이미 압축된 패키지에 압축을 실행하면 아무런 변화가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="29bbc-149">Hello Powershell 명령을 실행 하 여 패키지를 압축 [복사 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 와 `CompressPackage` 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-149">You can compress a package by running hello Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="29bbc-150">Hello 압축을 풀 수 hello로 동일 패키지 명령을 사용 하 여 `UncompressPackage` 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-150">You can uncompress hello package with hello same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="29bbc-151">hello 다음 명령을 압축 hello 패키지 toohello 이미지 저장소를 복사 하지 않고 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-151">hello following command compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="29bbc-152">사용 하 여 필요에 따라 압축 된 패키지 tooone 나 더 많은 서비스 패브릭 클러스터를 복사할 수 [복사 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) hello 없이 `SkipCopy` 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-152">You can copy a compressed package tooone or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without hello `SkipCopy` flag.</span></span>
<span data-ttu-id="29bbc-153">hello 패키지는 이제 hello에 대 한 압축 된 파일을 포함 `code`, `config`, 및 `data` 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-153">hello package now includes zipped files for hello `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="29bbc-154">hello 응용 프로그램 매니페스트 및 hello 서비스 매니페스트 되지 압축 된, 많은 내부 작업 (예: 공유, 특정 유효성 검사에 대 한 응용 프로그램 유형 이름 및 버전 추출 패키지)에 필요 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-154">hello application manifest and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="29bbc-155">이동식 hello 매니페스트는 비효율적인 이러한 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-155">Zipping hello manifests would make these operations inefficient.</span></span>

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

<span data-ttu-id="29bbc-156">압축 하 고 사용 하 여 hello 패키지를 복사할 수 또는 [복사 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 한 번에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-156">Alternatively, you can compress and copy hello package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="29bbc-157">Hello 패키지가 큰 경우 hello 패키지를 압축 및 hello 업로드 toohello 클러스터 모두에 대해 충분 한 상위 수준 시간 제한을 tooallow 시간을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-157">If hello package is large, provide a high enough timeout tooallow time for both hello package compression and hello upload toohello cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="29bbc-158">내부적으로 서비스 패브릭 응용 프로그램 패키지 유효성 검사를 hello에 대 한 체크섬을 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-158">Internally, Service Fabric computes checksums for hello application packages for validation.</span></span> <span data-ttu-id="29bbc-159">압축을 사용할 경우 각 패키지의 버전을 압축 하는 hello에 hello 체크섬이 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-159">When using compression, hello checksums are computed on hello zipped versions of each package.</span></span>
<span data-ttu-id="29bbc-160">응용 프로그램 패키지의 압축 되지 않은 프로그램 버전을 복사 하 고 hello에 대 한 toouse 압축 하려는 경우 같은 패키지의 hello hello 버전을 변경 해야 `code`, `config`, 및 `data` 패키지 tooavoid 체크섬이 일치 하지 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-160">If you copied an uncompressed version of your application package, and you want toouse compression for hello same package, you must change hello versions of hello `code`, `config`, and `data` packages tooavoid checksum mismatch.</span></span> <span data-ttu-id="29bbc-161">Hello 패키지 hello 버전을 변경 하는 대신 변경 되지 않은 경우 사용할 수 있습니다 [diff 프로 비전](service-fabric-application-upgrade-advanced.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-161">If hello packages are unchanged, instead of changing hello version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="29bbc-162">이 옵션을 변경 하지 않고 패키지 hello을 포함 하지 마십시오 대신 hello 서비스 매니페스트에서 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-162">With this option, do not include hello unchanged package instead reference it from hello service manifest.</span></span>

<span data-ttu-id="29bbc-163">마찬가지로, hello 패키지의 압축된 버전을 업로드 하는 경우 toouse 압축 되지 않은 패키지를 원하는 hello 버전 tooavoid hello 체크섬 불일치를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-163">Similarly, if you uploaded a compressed version of hello package and you want toouse an uncompressed package, you must update hello versions tooavoid hello checksum mismatch.</span></span>

<span data-ttu-id="29bbc-164">hello 패키지는 이제 패키지 올바르게, 유효성을 검사 하 고 압축 (필요한 경우), 준비 이므로 [배포](service-fabric-deploy-remove-applications.md) tooone 또는 더 많은 서비스 패브릭 클러스터를 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-164">hello package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) tooone or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="29bbc-165">Visual Studio를 사용하여 배포하는 경우 패키지 압축</span><span class="sxs-lookup"><span data-stu-id="29bbc-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="29bbc-166">Hello를 추가 하 여 Visual Studio toocompress 패키지 배포에 지시할 수 있습니다 `CopyPackageParameters` 요소 tooyour 게시 프로필을 및 hello 설정 `CompressPackage` 너무 특성`true`합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-166">You can instruct Visual Studio toocompress packages on deployment, by adding hello `CopyPackageParameters` element tooyour publish profile, and set hello `CompressPackage` attribute too`true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="29bbc-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="29bbc-167">Next steps</span></span>
<span data-ttu-id="29bbc-168">[배포 및 응용 프로그램을 제거할] [ 10] 설명 방법을 toouse PowerShell toomanage 응용 프로그램 인스턴스</span><span class="sxs-lookup"><span data-stu-id="29bbc-168">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances</span></span>

<span data-ttu-id="29bbc-169">[여러 환경에 대 한 응용 프로그램 매개 변수 관리] [ 11] 설명 방법을 tooconfigure 매개 변수 및 다른 응용 프로그램 인스턴스에 대 한 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-169">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="29bbc-170">[응용 프로그램에 대 한 보안 정책을 구성] [ 12] toorun 보안 정책 toorestrict 액세스에서 서비스 하는 방법에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="29bbc-170">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
