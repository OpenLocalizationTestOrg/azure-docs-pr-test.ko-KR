---
title: "기존 실행 tooAzure 서비스 패브릭 aaaDeploy | Microsoft Docs"
description: "게스트 실행 파일을 사용할 수 있도록으로 기존 응용 프로그램 toopackage tooa 서비스 패브릭 클러스터를 배포 하는 방법에 대 한 연습"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a><span data-ttu-id="1ac82-103">게스트 실행 tooService 패브릭 배포</span><span class="sxs-lookup"><span data-stu-id="1ac82-103">Deploy a guest executable tooService Fabric</span></span>
<span data-ttu-id="1ac82-104">Azure Service Fabric에서 Node.js, Java 또는 C++과 같은 모든 종류의 코드를 서비스로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="1ac82-105">서비스 패브릭 게스트 실행 파일로 toothese 유형의 서비스를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-105">Service Fabric refers toothese types of services as guest executables.</span></span>

<span data-ttu-id="1ac82-106">게스트 실행 파일은 서비스 패브릭에서 상태 비저장 서비스처럼 취급됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="1ac82-107">결과적으로 가용성 및 기타 메트릭을 기반으로 클러스터의 노드에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="1ac82-108">이 문서에서는 설명 방법을 toopackage Visual Studio 또는 명령줄 유틸리티를 사용 하 여 게스트 실행 tooa 서비스 패브릭 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-108">This article describes how toopackage and deploy a guest executable tooa Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="1ac82-109">이 문서에서는 hello 단계 toopackage 게스트 실행 파일을 포함 하 고 패브릭 tooService 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-109">In this article, we cover hello steps toopackage a guest executable and deploy it tooService Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="1ac82-110">서비스 패브릭에서 게스트 실행 파일을 실행할 때의 이점</span><span class="sxs-lookup"><span data-stu-id="1ac82-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="1ac82-111">서비스 패브릭 클러스터에서 실행 되는 게스트는 여러 가지 이점을 toorunning:</span><span class="sxs-lookup"><span data-stu-id="1ac82-111">There are several advantages toorunning a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="1ac82-112">고가용성.</span><span class="sxs-lookup"><span data-stu-id="1ac82-112">High availability.</span></span> <span data-ttu-id="1ac82-113">Service Fabric에서 실행되는 응용 프로그램은 고가용성 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="1ac82-114">Service Fabric은 응용 프로그램 인스턴스가 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="1ac82-115">상태 모니터링.</span><span class="sxs-lookup"><span data-stu-id="1ac82-115">Health monitoring.</span></span> <span data-ttu-id="1ac82-116">Service Fabric 상태 모니터링은 응용 프로그램이 실행 중인지 감지하고 오류가 있으면 진단 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="1ac82-117">응용 프로그램 수명 주기 관리.</span><span class="sxs-lookup"><span data-stu-id="1ac82-117">Application lifecycle management.</span></span> <span data-ttu-id="1ac82-118">중단 시간 없이 업그레이드를 제공할 뿐 아니라 서비스 패브릭 보고 업그레이드 하는 동안 잘못 된 상태 이벤트는 경우 자동 롤백 toohello 이전 버전을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback toohello previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="1ac82-119">밀도.</span><span class="sxs-lookup"><span data-stu-id="1ac82-119">Density.</span></span> <span data-ttu-id="1ac82-120">각 응용 프로그램 toorun 자체 하드웨어에 대 한 hello 필요가 없도록 하므로 클러스터의 여러 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-120">You can run multiple applications in a cluster, which eliminates hello need for each application toorun on its own hardware.</span></span>
* <span data-ttu-id="1ac82-121">검색 기능: REST를 사용 하 여 호출할 수 있습니다 hello 서비스 패브릭 명명 서비스 toofind 다른 서비스 hello 클러스터에.</span><span class="sxs-lookup"><span data-stu-id="1ac82-121">Discoverability: Using REST you can call hello Service Fabric Naming service toofind other services in hello cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="1ac82-122">샘플</span><span class="sxs-lookup"><span data-stu-id="1ac82-122">Samples</span></span>
* [<span data-ttu-id="1ac82-123">게스트 실행 파일을 패키징 및 배포하는 샘플</span><span class="sxs-lookup"><span data-stu-id="1ac82-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="1ac82-124">REST를 사용 하 여 hello 명명 서비스를 통해 두 개의 게스트 실행 파일 (C# 및 nodejs) 통신의 샘플</span><span class="sxs-lookup"><span data-stu-id="1ac82-124">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="1ac82-125">응용 프로그램 및 서비스 매니페스트 파일 개요</span><span class="sxs-lookup"><span data-stu-id="1ac82-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="1ac82-126">게스트 실행 파일을 배포의 일환으로, 것은 유용 toounderstand hello 서비스 패브릭 패키징 및 배포 모델에 설명 된 대로 [응용 프로그램 모델](service-fabric-application-model.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-126">As part of deploying a guest executable, it is useful toounderstand hello Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="1ac82-127">두 개의 XML 파일이 hello 서비스 패브릭 패키징 모델 사용: 응용 프로그램 및 서비스 매니페스트 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-127">hello Service Fabric packaging model relies on two XML files: hello application and service manifests.</span></span> <span data-ttu-id="1ac82-128">hello 스키마 정의 hello ServiceManifest.xml 및 ApplicationManifest.xml 파일은와 함께 설치에 대 한 hello에 서비스 패브릭 SDK *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="1ac82-128">hello schema definition for hello ApplicationManifest.xml and ServiceManifest.xml files is installed with hello Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="1ac82-129">**응용 프로그램 매니페스트** hello 응용 프로그램 매니페스트는 사용 되는 toodescribe hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-129">**Application manifest** hello application manifest is used toodescribe hello application.</span></span> <span data-ttu-id="1ac82-130">구성 하는 hello 서비스 및 다른 매개 변수를 사용 하는 toodefine 어떻게 하나 이상의 서비스를 배포, hello 인스턴스 수 등을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-130">It lists hello services that compose it, and other parameters that are used toodefine how one or more services should be deployed, such as hello number of instances.</span></span>

  <span data-ttu-id="1ac82-131">Service Fabric에서 응용 프로그램은 배포 및 업그레이드 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="1ac82-132">응용 프로그램은 잠재적인 오류 및 잠재적 롤백이 관리되는 하나의 단위로 업그레이드될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="1ac82-133">서비스 패브릭 보장 hello 업그레이드 프로세스 중 하나는 성공 또는 hello 업그레이드가 실패 하면, 남지 않습니다 hello 응용 프로그램 알 수 없거나 불안정 한 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-133">Service Fabric guarantees that hello upgrade process is either successful, or, if hello upgrade fails, does not leave hello application in an unknown or unstable state.</span></span>
* <span data-ttu-id="1ac82-134">**서비스 매니페스트** hello 서비스 매니페스트는 서비스의 hello 구성 요소를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-134">**Service manifest** hello service manifest describes hello components of a service.</span></span> <span data-ttu-id="1ac82-135">Hello 이름 및 유형의 서비스를 같은 데이터를 코드 및 구성을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-135">It includes data, such as hello name and type of service, and its code and configuration.</span></span> <span data-ttu-id="1ac82-136">hello 서비스 매니페스트도 몇 가지 추가 매개 변수가 포함 될 수 있는 배포 된 후 tooconfigure hello 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-136">hello service manifest also includes some additional parameters that can be used tooconfigure hello service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="1ac82-137">응용 프로그램 패키지 파일 구조</span><span class="sxs-lookup"><span data-stu-id="1ac82-137">Application package file structure</span></span>
<span data-ttu-id="1ac82-138">응용 프로그램 tooService 패브릭 toodeploy hello 응용 프로그램은 미리 정의 된 디렉터리 구조를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-138">toodeploy an application tooService Fabric, hello application should follow a predefined directory structure.</span></span> <span data-ttu-id="1ac82-139">hello 다음은 해당 구조의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-139">hello following is an example of that structure.</span></span>

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

<span data-ttu-id="1ac82-140">hello ApplicationPackageRoot hello 응용 프로그램을 정의 하는 hello ApplicationManifest.xml 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-140">hello ApplicationPackageRoot contains hello ApplicationManifest.xml file that defines hello application.</span></span> <span data-ttu-id="1ac82-141">Hello 응용 프로그램에 포함 된 각 서비스에 대 한 하위 디렉터리에 사용 되는 toocontain hello 서비스에 필요한 아티팩트를 hello 모든입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-141">A subdirectory for each service included in hello application is used toocontain all hello artifacts that hello service requires.</span></span> <span data-ttu-id="1ac82-142">이러한 하위 디렉터리는 hello ServiceManifest.xml 및 일반적으로 다음 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-142">These subdirectories are hello ServiceManifest.xml and, typically, hello following:</span></span>

* <span data-ttu-id="1ac82-143">*Code*.</span><span class="sxs-lookup"><span data-stu-id="1ac82-143">*Code*.</span></span> <span data-ttu-id="1ac82-144">이 디렉터리는 hello 서비스 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-144">This directory contains hello service code.</span></span>
* <span data-ttu-id="1ac82-145">*Config*. 이 디렉터리에 Settings.xml 파일 (및 필요에 따라 다른 파일) hello 서비스 런타임 tooretrieve 특정 구성 설정에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-145">*Config*. This directory contains a Settings.xml file (and other files if necessary) that hello service can access at runtime tooretrieve specific configuration settings.</span></span>
* <span data-ttu-id="1ac82-146">*Data*.</span><span class="sxs-lookup"><span data-stu-id="1ac82-146">*Data*.</span></span> <span data-ttu-id="1ac82-147">이는 추가 디렉터리 toostore 추가 로컬 데이터를 hello 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-147">This is an additional directory toostore additional local data that hello service may need.</span></span> <span data-ttu-id="1ac82-148">데이터에 사용 되는 toostore만 임시 데이터 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-148">Data should be used toostore only ephemeral data.</span></span> <span data-ttu-id="1ac82-149">서비스 패브릭 hello 서비스 toobe (예: 장애 조치 중) 위치를 변경 해야 하는 경우 변경 내용을 toohello 데이터 디렉터리를 복제 또는 복사 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-149">Service Fabric does not copy or replicate changes toohello data directory if hello service needs toobe relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="1ac82-150">Toocreate hello 없는 `config` 및 `data` 필요가 없는 경우에 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-150">You don't have toocreate hello `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="1ac82-151">기존 실행 파일 패키징</span><span class="sxs-lookup"><span data-stu-id="1ac82-151">Package an existing executable</span></span>
<span data-ttu-id="1ac82-152">게스트 실행 파일을 패키징할 때 선택할 수 있습니다 어느 toouse Visual Studio 프로젝트 템플릿 또는 너무[hello 응용 프로그램 패키지를 수동으로 만들](#manually)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-152">When packaging a guest executable, you can choose either toouse a Visual Studio project template or too[create hello application package manually](#manually).</span></span> <span data-ttu-id="1ac82-153">응용 프로그램 패키지 구조 hello Visual Studio를 사용 하 고 드립니다 hello 새 프로젝트 템플릿을 통해 매니페스트 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-153">Using Visual Studio, hello application package structure and manifest files are created by hello new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="1ac82-154">hello 가장 쉬운 방법은 toopackage는 기존 Windows 서비스로 실행 파일은 Visual Studio toouse와 Linux toouse Yeoman</span><span class="sxs-lookup"><span data-stu-id="1ac82-154">hello easiest way toopackage an existing Windows executable into a service is toouse Visual Studio and on Linux toouse Yeoman</span></span>
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a><span data-ttu-id="1ac82-155">Visual Studio toopackage를 사용 하 고 기존 실행 파일 배포</span><span class="sxs-lookup"><span data-stu-id="1ac82-155">Use Visual Studio toopackage and deploy an existing executable</span></span>
<span data-ttu-id="1ac82-156">Visual Studio는 서비스 패브릭 서비스 템플릿 toohelp을 게스트 실행 tooa 서비스 패브릭 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-156">Visual Studio provides a Service Fabric service template toohelp you deploy a guest executable tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="1ac82-157">**파일** > **새 프로젝트**를 선택하여 Service Fabric 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-157">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="1ac82-158">선택 **게스트 실행 파일** hello 서비스 템플릿으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-158">Choose **Guest Executable** as hello service template.</span></span>
3. <span data-ttu-id="1ac82-159">클릭 **찾아보기** tooselect hello 폴더는 실행 파일, hello 매개 변수 toocreate hello 서비스 hello 나머지를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-159">Click **Browse** tooselect hello folder with your executable and fill in hello rest of hello parameters toocreate hello service.</span></span>
   * <span data-ttu-id="1ac82-160">*코드 패키지 동작*.</span><span class="sxs-lookup"><span data-stu-id="1ac82-160">*Code Package Behavior*.</span></span> <span data-ttu-id="1ac82-161">수 집합 toocopy 프로그램 폴더 toohello Visual Studio 프로젝트의 모든 hello 콘텐츠 실행 hello 변경 되지 않는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-161">Can be set toocopy all hello content of your folder toohello Visual Studio Project, which is useful if hello executable does not change.</span></span> <span data-ttu-id="1ac82-162">Hello 실행 toochange 예상 하 고 새 빌드를 hello 기능 toopick를 동적으로 원하는 대신 toolink toohello 폴더를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-162">If you expect hello executable toochange and want hello ability toopick up new builds dynamically, you can choose toolink toohello folder instead.</span></span> <span data-ttu-id="1ac82-163">Visual Studio에서 hello 응용 프로그램 프로젝트를 만들 때 연결 된 폴더를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-163">You can use linked folders when creating hello application project in Visual Studio.</span></span> <span data-ttu-id="1ac82-164">이렇게 수 있게 tooupdate hello 게스트 실행 파일의 원본 대상에 hello 프로젝트 내에서 toohello 원본 위치에서 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-164">This links toohello source location from within hello project, making it possible for you tooupdate hello guest executable in its source destination.</span></span> <span data-ttu-id="1ac82-165">이러한 업데이트를 사용 하면 빌드에 hello 응용 프로그램 패키지의 일부가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-165">Those updates become part of hello application package on build.</span></span>
   * <span data-ttu-id="1ac82-166">*프로그램* toostart hello 서비스를 실행 해야 하는 hello 실행 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-166">*Program* specifies hello executable that should be run toostart hello service.</span></span>
   * <span data-ttu-id="1ac82-167">*인수* 전달 되어야 하는 toohello 실행 hello 인수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-167">*Arguments* specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="1ac82-168">인수가 있는 매개 변수 목록이 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-168">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="1ac82-169">*작업 폴더* toobe 시작이 일어나는 hello 프로세스에 대 한 hello 작업 디렉터리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-169">*WorkingFolder* specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="1ac82-170">세 가지 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-170">You can specify three values:</span></span>
     * <span data-ttu-id="1ac82-171">`CodeBase`해당 hello 작업 디렉터리 toobe hello 응용 프로그램 패키지의 toohello 코드 디렉터리를 설정 하 고 중임을 지정 합니다 (`Code` hello 파일 구조를 앞에 표시 된 디렉터리).</span><span class="sxs-lookup"><span data-stu-id="1ac82-171">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="1ac82-172">`CodePackage`해당 hello 작업 디렉터리 toobe hello 응용 프로그램 패키지의 루트 toohello 설정 되기 지정 (`GuestService1Pkg` hello 파일 구조를 앞에 표시).</span><span class="sxs-lookup"><span data-stu-id="1ac82-172">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="1ac82-173">`Work`hello 파일은 작업 라는 하위 디렉터리에 저장을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-173">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="1ac82-174">서비스에 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-174">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="1ac82-175">서비스 끝점 통신을 위해 필요로 한다면 hello 프로토콜, 포트 및 형식 toohello ServiceManifest.xml 파일 이제 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-175">If your service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="1ac82-176">예: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`</span><span class="sxs-lookup"><span data-stu-id="1ac82-176">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="1ac82-177">이제 hello 패키지를 사용 하 고 Visual Studio에서 hello 솔루션을 디버그 하 여 로컬 클러스터에 대해 작업을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-177">You can now use hello package and publish action against your local cluster by debugging hello solution in Visual Studio.</span></span> <span data-ttu-id="1ac82-178">준비가 되 면 원격 클러스터를 tooa hello 응용 프로그램을 게시 하거나 hello 솔루션 toosource 컨트롤에서 확인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-178">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span>
7. <span data-ttu-id="1ac82-179">이 문서 toosee toohello 끝을 어떻게 이동 tooview 서비스 패브릭 탐색기에서 실행 중인 게스트 실행 서비스.</span><span class="sxs-lookup"><span data-stu-id="1ac82-179">Go toohello end of this article toosee how tooview your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="1ac82-180">Yoeman toopackage를 사용 하 여 및 Linux 기반 기존 실행 파일 배포</span><span class="sxs-lookup"><span data-stu-id="1ac82-180">Use Yoeman toopackage and deploy an existing executable on Linux</span></span>

<span data-ttu-id="1ac82-181">Linux에서 실행 되는 게스트를 배포 하기 위한 hello 프로시저 csharp 또는 java 응용 프로그램 배포와 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-181">hello procedure for creating and deploying a guest executable on Linux is hello same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="1ac82-182">터미널에서 `yo azuresfguest`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-182">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="1ac82-183">응용 프로그램의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-183">Name your application.</span></span>
3. <span data-ttu-id="1ac82-184">서비스 이름을 지정 하 고 hello 실행 파일의 경로 및 사용 하 여 호출 해야 하는 hello 매개 변수를 포함 하 여 hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-184">Name your service, and provide hello details including path of hello executable and hello parameters it must be invoked with.</span></span>

<span data-ttu-id="1ac82-185">Yeoman 응용 프로그램 패키지 hello 적절 한 응용 프로그램으로 만들고와 함께 매니페스트 파일 설치 및 스크립트를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-185">Yeoman creates an application package with hello appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="1ac82-186">기존 실행 파일을 수동으로 패키징하고 배포하기</span><span class="sxs-lookup"><span data-stu-id="1ac82-186">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="1ac82-187">수동으로 게스트 실행 파일을 압축 hello 프로세스 hello 일반적인 단계를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-187">hello process of manually packaging a guest executable is based on hello following general steps:</span></span>

1. <span data-ttu-id="1ac82-188">Hello 패키지 디렉터리 구조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-188">Create hello package directory structure.</span></span>
2. <span data-ttu-id="1ac82-189">Hello 응용 프로그램의 코드 및 구성 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-189">Add hello application's code and configuration files.</span></span>
3. <span data-ttu-id="1ac82-190">Hello 서비스 매니페스트 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-190">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="1ac82-191">Hello 응용 프로그램 매니페스트 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-191">Edit hello application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a><span data-ttu-id="1ac82-192">Hello 패키지 디렉터리 구조 만들기</span><span class="sxs-lookup"><span data-stu-id="1ac82-192">Create hello package directory structure</span></span>
<span data-ttu-id="1ac82-193">Hello 이전 섹션에에서 설명 된 대로 hello 디렉터리 구조를 만들어서 시작할 수 있습니다 "응용 프로그램 패키지 파일 구조입니다."</span><span class="sxs-lookup"><span data-stu-id="1ac82-193">You can start by creating hello directory structure, as described in hello preceding section, "Application package file structure."</span></span>

### <a name="add-hello-applications-code-and-configuration-files"></a><span data-ttu-id="1ac82-194">Hello 응용 프로그램의 코드 및 구성 파일 추가</span><span class="sxs-lookup"><span data-stu-id="1ac82-194">Add hello application's code and configuration files</span></span>
<span data-ttu-id="1ac82-195">Hello 디렉터리 구조를 만든 후에 hello 코드 및 config 디렉터리 아래의 hello 응용 프로그램의 코드 및 구성 파일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-195">After you have created hello directory structure, you can add hello application's code and configuration files under hello code and config directories.</span></span> <span data-ttu-id="1ac82-196">또한 추가 디렉터리 또는 hello code 또는 config 디렉터리 아래의 하위 디렉터리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-196">You can also create additional directories or subdirectories under hello code or config directories.</span></span>

<span data-ttu-id="1ac82-197">서비스 패브릭 않습니다는 `xcopy` hello 응용 프로그램 루트 디렉터리를 두 개의 상위 디렉터리, 코드 및 설정을 만드는 것 외에 없는 미리 정의 된 구조 toouse 이므로 hello 콘텐츠의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-197">Service Fabric does an `xcopy` of hello content of hello application root directory, so there is no predefined structure toouse other than creating two top directories, code and settings.</span></span> <span data-ttu-id="1ac82-198">하지만 원한다면 다른 이름을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-198">(You can pick different names if you want.</span></span> <span data-ttu-id="1ac82-199">자세한 내용은 hello 다음 섹션에 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="1ac82-199">More details are in hello next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="1ac82-200">모든 hello 파일 및 응용 프로그램 요구 hello 종속성을 포함 하는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-200">Make sure that you include all hello files and dependencies that hello application needs.</span></span> <span data-ttu-id="1ac82-201">서비스 패브릭 여기서 hello 응용 프로그램의 서비스는 배포 진행 중인 toobe hello 클러스터의 모든 노드에서 hello 응용 프로그램 패키지의 콘텐츠 hello를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-201">Service Fabric copies hello content of hello application package on all nodes in hello cluster where hello application's services are going toobe deployed.</span></span> <span data-ttu-id="1ac82-202">hello 패키지 hello 일일이 toorun 모든 hello 코드를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-202">hello package should contain all hello code that hello application needs toorun.</span></span> <span data-ttu-id="1ac82-203">Hello 종속성 이미 설치 되어 있음을 가정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="1ac82-203">Do not assume that hello dependencies are already installed.</span></span>
>
>

### <a name="edit-hello-service-manifest-file"></a><span data-ttu-id="1ac82-204">Hello 서비스 매니페스트 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-204">Edit hello service manifest file</span></span>
<span data-ttu-id="1ac82-205">hello 다음 단계는 tooedit hello 서비스 매니페스트 파일 tooinclude hello 다음 정보:</span><span class="sxs-lookup"><span data-stu-id="1ac82-205">hello next step is tooedit hello service manifest file tooinclude hello following information:</span></span>

* <span data-ttu-id="1ac82-206">hello hello 서비스 형식의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-206">hello name of hello service type.</span></span> <span data-ttu-id="1ac82-207">서비스 패브릭 tooidentify 서비스를 사용 하는 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-207">This is an ID that Service Fabric uses tooidentify a service.</span></span>
* <span data-ttu-id="1ac82-208">hello 명령 toouse toolaunch hello 응용 프로그램 (ExeHost)입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-208">hello command toouse toolaunch hello application (ExeHost).</span></span>
* <span data-ttu-id="1ac82-209">Toobe 해야 하는 모든 스크립트 tooset hello 응용 프로그램 (SetupEntrypoint)을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-209">Any script that needs toobe run tooset up hello application (SetupEntrypoint).</span></span>

<span data-ttu-id="1ac82-210">hello 다음은의 예로 `ServiceManifest.xml` 파일:</span><span class="sxs-lookup"><span data-stu-id="1ac82-210">hello following is an example of a `ServiceManifest.xml` file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

<span data-ttu-id="1ac82-211">다음 섹션 hello hello tooupdate 해야 하는 hello 파일의 다른 부분을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-211">hello following sections go over hello different parts of hello file that you need tooupdate.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="1ac82-212">ServiceTypes 업데이트</span><span class="sxs-lookup"><span data-stu-id="1ac82-212">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="1ac82-213">`ServiceTypeName`의 이름을 자유롭게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-213">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="1ac82-214">hello hello 값은 사용 `ApplicationManifest.xml` 파일 tooidentify hello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-214">hello value is used in hello `ApplicationManifest.xml` file tooidentify hello service.</span></span>
* <span data-ttu-id="1ac82-215">`UseImplicitHost="true"`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-215">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="1ac82-216">이 특성을 hello 서비스는 자체 포함 된 응용 프로그램을 기반으로 되므로 모든 서비스 패브릭 필요 toodo toolaunch 서비스 패브릭 지시 프로세스로의 상태를 모니터링 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-216">This attribute tells Service Fabric that hello service is based on a self-contained app, so all Service Fabric needs toodo is toolaunch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="1ac82-217">CodePackage 업데이트</span><span class="sxs-lookup"><span data-stu-id="1ac82-217">Update CodePackage</span></span>
<span data-ttu-id="1ac82-218">hello CodePackage 요소 hello 서비스 코드의 hello 위치 (및 버전)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-218">hello CodePackage element specifies hello location (and version) of hello service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="1ac82-219">hello `Name` 요소 hello 디렉터리 hello 서비스의 코드를 포함 하는 hello 응용 프로그램 패키지에 사용 되는 toospecify hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-219">hello `Name` element is used toospecify hello name of hello directory in hello application package that contains hello service's code.</span></span> <span data-ttu-id="1ac82-220">`CodePackage`hello 역시 `version` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-220">`CodePackage` also has hello `version` attribute.</span></span> <span data-ttu-id="1ac82-221">이러한 방식은 사용된 toospecify hello 버전의 hello 코드 하며도 수 서비스 패브릭에서 hello 응용 프로그램 수명 주기 관리 인프라를 사용 하 여 tooupgrade hello 서비스 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-221">This can be used toospecify hello version of hello code, and can also potentially be used tooupgrade hello service's code by using hello application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="1ac82-222">선택 사항: SetupEntryPoint 업데이트</span><span class="sxs-lookup"><span data-stu-id="1ac82-222">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="1ac82-223">hello SetupEntryPoint 요소는 사용 되는 toospecify hello 서비스 코드를 시작 하기 전에 실행 해야 하는 모든 실행 파일 또는 배치 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-223">hello SetupEntryPoint element is used toospecify any executable or batch file that should be executed before hello service's code is launched.</span></span> <span data-ttu-id="1ac82-224">이므로 단계는 선택 사항 toobe 초기화가 없으므로 필요한 경우 포함할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-224">It is an optional step, so it does not need toobe included if there is no initialization required.</span></span> <span data-ttu-id="1ac82-225">SetupEntryPoint hello hello 서비스를 다시 시작 될 때마다 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-225">hello SetupEntryPoint is executed every time hello service is restarted.</span></span>

<span data-ttu-id="1ac82-226">설치 스크립트 toobe hello 응용 프로그램의 설치 여러 스크립트에 필요한 경우 단일 배치 파일에서 그룹화 할 하나만 SetupEntryPoint가.</span><span class="sxs-lookup"><span data-stu-id="1ac82-226">There is only one SetupEntryPoint, so setup scripts need toobe grouped in a single batch file if hello application's setup requires multiple scripts.</span></span> <span data-ttu-id="1ac82-227">SetupEntryPoint hello 모든 형식의 파일을 실행할 수 있습니다: 실행 파일, 배치 파일 및 PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1ac82-227">hello SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="1ac82-228">자세한 내용은 [SetupEntryPoint 구성](service-fabric-application-runas-security.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ac82-228">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="1ac82-229">앞 예제는 hello, SetupEntryPoint hello 라는 배치 파일 실행 `LaunchConfig.cmd` 에 있는 hello 즉 `scripts` hello 코드 디렉터리 (WorkingFolder 요소 hello tooCodeBase 설정 가정)의 하위 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-229">In hello preceding example, hello SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in hello `scripts` subdirectory of hello code directory (assuming hello WorkingFolder element is set tooCodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="1ac82-230">EntryPoint 업데이트</span><span class="sxs-lookup"><span data-stu-id="1ac82-230">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="1ac82-231">hello `EntryPoint` hello 서비스 매니페스트 파일에 요소가 사용 되는 toospecify 어떻게 toolaunch hello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-231">hello `EntryPoint` element in hello service manifest file is used toospecify how toolaunch hello service.</span></span> <span data-ttu-id="1ac82-232">hello `ExeHost` hello 실행 파일 (및 인수) 요소를 지정 해야 하는 toolaunch hello 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-232">hello `ExeHost` element specifies hello executable (and arguments) that should be used toolaunch hello service.</span></span>

* <span data-ttu-id="1ac82-233">`Program`hello hello 서비스를 시작 해야 하는 hello 실행 파일 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-233">`Program` specifies hello name of hello executable that should start hello service.</span></span>
* <span data-ttu-id="1ac82-234">`Arguments`전달 되어야 하는 toohello 실행 hello 인수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-234">`Arguments` specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="1ac82-235">인수가 있는 매개 변수 목록이 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-235">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="1ac82-236">`WorkingFolder`시작 toobe 이동 하는 hello 프로세스에 대 한 hello 작업 디렉터리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-236">`WorkingFolder` specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="1ac82-237">세 가지 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-237">You can specify three values:</span></span>
  * <span data-ttu-id="1ac82-238">`CodeBase`해당 hello 작업 디렉터리 toobe hello 응용 프로그램 패키지의 toohello 코드 디렉터리를 설정 하 고 중임을 지정 합니다 (`Code` 디렉터리 hello 파일 구조를 앞에서).</span><span class="sxs-lookup"><span data-stu-id="1ac82-238">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory in hello preceding file structure).</span></span>
  * <span data-ttu-id="1ac82-239">`CodePackage`해당 hello 작업 디렉터리 toobe hello 응용 프로그램 패키지의 루트 toohello 설정 되기 지정 (`GuestService1Pkg` hello 파일 구조를 앞에).</span><span class="sxs-lookup"><span data-stu-id="1ac82-239">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` in hello preceding file structure).</span></span>
    * <span data-ttu-id="1ac82-240">`Work`hello 파일은 작업 라는 하위 디렉터리에 저장을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-240">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="1ac82-241">hello 작업 폴더는 상대 경로 hello 응용 프로그램이 나 초기화 스크립트에서 사용할 수 있도록 유용한 tooset hello 올바른 작업 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-241">hello WorkingFolder is useful tooset hello correct working directory so that relative paths can be used by either hello application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="1ac82-242">통신을 위해 끝점을 업데이트하고 명명 서비스에 등록</span><span class="sxs-lookup"><span data-stu-id="1ac82-242">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="1ac82-243">앞 예제는 hello에서 hello `Endpoint` 요소 hello 응용 프로그램에서 수신할 수 있는 hello 끝점을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-243">In hello preceding example, hello `Endpoint` element specifies hello endpoints that hello application can listen on.</span></span> <span data-ttu-id="1ac82-244">이 예제에서는 hello Node.js 응용 프로그램의 http 포트 3000 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-244">In this example, hello Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="1ac82-245">또한 요청 서비스 패브릭 toopublish이 끝점 toohello 명명 서비스 다른 서비스는 hello 끝점 주소 toothis service를 검색할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-245">Furthermore you can ask Service Fabric toopublish this endpoint toohello Naming Service so other services can discover hello endpoint address toothis service.</span></span> <span data-ttu-id="1ac82-246">이렇게 하면 게스트 실행 파일 서비스 간의 toobe 수 toocommunicate 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-246">This enables you toobe able toocommunicate between services that are guest executables.</span></span>
<span data-ttu-id="1ac82-247">hello 게시 된 끝점 주소는 hello 폼의 `UriScheme://IPAddressOrFQDN:Port/PathSuffix`합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-247">hello published endpoint address is of hello form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="1ac82-248">`UriScheme` 및 `PathSuffix`는 선택적 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-248">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="1ac82-249">`IPAddressOrFQDN`이며 hello IP 주소 또는이 실행 파일에 배치 되는 hello 노드의 정규화 된 도메인 이름 수에 대 한 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-249">`IPAddressOrFQDN` is hello IP address or fully qualified domain name of hello node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="1ac82-250">에 hello 다음 예제에서는 hello 서비스에 한 번 배포 되 면 서비스 패브릭 탐색기 표시에서 비슷한 끝점 너무`http://10.1.4.92:3000/myapp/` hello 서비스 인스턴스에 대 한 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-250">In hello following example, once hello service is deployed, in Service Fabric Explorer you see an endpoint similar too`http://10.1.4.92:3000/myapp/` published for hello service instance.</span></span> <span data-ttu-id="1ac82-251">또는 로컬 컴퓨터인 경우, `http://localhost:3000/myapp/`가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-251">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="1ac82-252">이러한 주소를 사용할 수 있습니다 [역방향 프록시](service-fabric-reverseproxy.md) 서비스 간의 toocommunicate 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-252">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) toocommunicate between services.</span></span>

### <a name="edit-hello-application-manifest-file"></a><span data-ttu-id="1ac82-253">Hello 응용 프로그램 매니페스트 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-253">Edit hello application manifest file</span></span>
<span data-ttu-id="1ac82-254">Hello를 구성한 후 `Servicemanifest.xml` 파일을 일부 변경 내용이 toohello toomake 필요한 `ApplicationManifest.xml` hello tooensure 서비스 유형 및 이름을 사용 되는 올바른 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-254">Once you have configured hello `Servicemanifest.xml` file, you need toomake some changes toohello `ApplicationManifest.xml` file tooensure that hello correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="1ac82-255">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="1ac82-255">ServiceManifestImport</span></span>
<span data-ttu-id="1ac82-256">Hello에 `ServiceManifestImport` 요소인 tooinclude hello 응용 프로그램에서 지정 하는 하나 이상의 서비스를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-256">In hello `ServiceManifestImport` element, you can specify one or more services that you want tooinclude in hello app.</span></span> <span data-ttu-id="1ac82-257">사용 하 여 서비스 참조는 `ServiceManifestName`, 여기서 hello hello hello 디렉터리 이름을 지정 하는 `ServiceManifest.xml` 파일은 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-257">Services are referenced with `ServiceManifestName`, which specifies hello name of hello directory where hello `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="1ac82-258">로깅 설정</span><span class="sxs-lookup"><span data-stu-id="1ac82-258">Set up logging</span></span>
<span data-ttu-id="1ac82-259">게스트 실행 파일에 대 한 hello 응용 프로그램 및 구성 스크립트는 모든 오류를 표시 하는 경우 유용한 toobe 수 toosee 콘솔 로그 toofind 아웃 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-259">For guest executables, it is useful toobe able toosee console logs toofind out if hello application and configuration scripts show any errors.</span></span>
<span data-ttu-id="1ac82-260">콘솔 리디렉션을 hello에서 구성할 수 있습니다 `ServiceManifest.xml` hello를 사용 하 여 파일 `ConsoleRedirection` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-260">Console redirection can be configured in hello `ServiceManifest.xml` file using hello `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="1ac82-261">Hello 콘솔 리디렉션 정책 hello 응용 프로그램 장애 조치에 영향을 줄 수 있으므로 프로덕션에 배포 된 응용 프로그램에서 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="1ac82-261">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="1ac82-262">로컬 개발 및 디버깅 목적으로*만* 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="1ac82-262">*Only* use this for local development and debugging purposes.</span></span>  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="1ac82-263">`ConsoleRedirection`사용 되는 tooredirect 콘솔 출력 (stdout 및 stderr) tooa 작업 디렉터리를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-263">`ConsoleRedirection` can be used tooredirect console output (both stdout and stderr) tooa working directory.</span></span> <span data-ttu-id="1ac82-264">Hello 설치 또는 hello 서비스 패브릭 클러스터에 hello 응용 프로그램의 실행 중에 오류가 없는 hello 기능 tooverify 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-264">This provides hello ability tooverify that there are no errors during hello setup or execution of hello application in hello Service Fabric cluster.</span></span>

<span data-ttu-id="1ac82-265">`FileRetentionCount`hello 작업 디렉터리에 저장 됩니다 파일 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-265">`FileRetentionCount` determines how many files are saved in hello working directory.</span></span> <span data-ttu-id="1ac82-266">5, 예를 들어 의미 hello 이전 5 실행에 대 한 로그 파일 hello hello 작업 디렉터리에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-266">A value of 5, for example, means that hello log files for hello previous five executions are stored in hello working directory.</span></span>

<span data-ttu-id="1ac82-267">`FileMaxSizeInKb`hello hello 로그 파일의 최대 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-267">`FileMaxSizeInKb` specifies hello maximum size of hello log files.</span></span>

<span data-ttu-id="1ac82-268">로그 파일은 hello 서비스의 작업 디렉터리 중 하나에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-268">Log files are saved in one of hello service's working directories.</span></span> <span data-ttu-id="1ac82-269">hello 파일이 있는 toodetermine 서비스 패브릭 탐색기 toodetermine,는 노드 hello 서비스가 실행 되 고 사용 되는 작업 디렉터리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-269">toodetermine where hello files are located, use Service Fabric Explorer toodetermine which node hello service is running on, and which working directory is being used.</span></span> <span data-ttu-id="1ac82-270">이 프로세스는 이 문서의 뒷부분에서 다루겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-270">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="1ac82-271">배포</span><span class="sxs-lookup"><span data-stu-id="1ac82-271">Deployment</span></span>
<span data-ttu-id="1ac82-272">hello 마지막 단계는 너무[응용 프로그램을 배포](service-fabric-deploy-remove-applications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-272">hello last step is too[deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="1ac82-273">PowerShell 스크립트 표시 방법을 따르는 hello toodeploy 응용 프로그램 toohello 로컬 개발 클러스터와 새 서비스 패브릭 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-273">hello following PowerShell script shows how toodeploy your application toohello local development cluster, and start a new Service Fabric service.</span></span>

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> <span data-ttu-id="1ac82-274">[Hello 패키지를 압축](service-fabric-package-apps.md#compress-a-package) hello 패키지 크거나 많은 파일을 포함 하는 경우 toohello 이미지 저장소를 복사 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="1ac82-274">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store if hello package is large or has many files.</span></span> <span data-ttu-id="1ac82-275">[여기](service-fabric-deploy-remove-applications.md#upload-the-application-package)서 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="1ac82-275">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="1ac82-276">서비스 패브릭 서비스를 다양한 "구성"으로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-276">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="1ac82-277">예를 들어 단일 또는 여러 인스턴스로 배포할 수 또는 hello 서비스 패브릭 클러스터의 각 노드에서 hello 서비스의 한 인스턴스가 하는 방식으로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-277">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of hello service on each node of hello Service Fabric cluster.</span></span>

<span data-ttu-id="1ac82-278">hello `InstanceCount` hello의 매개 변수 `New-ServiceFabricService` cmdlet은 사용 되는 toospecify hello 서비스의 인스턴스 개수 hello 서비스 패브릭 클러스터에서 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-278">hello `InstanceCount` parameter of hello `New-ServiceFabricService` cmdlet is used toospecify how many instances of hello service should be launched in hello Service Fabric cluster.</span></span> <span data-ttu-id="1ac82-279">Hello를 설정할 수 있습니다 `InstanceCount` hello 유형의 배포 하는 응용 프로그램에 따라 값을 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-279">You can set hello `InstanceCount` value, depending on hello type of application that you are deploying.</span></span> <span data-ttu-id="1ac82-280">두 hello 가장 일반적인 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-280">hello two most common scenarios are:</span></span>

* <span data-ttu-id="1ac82-281">`InstanceCount = "1"`</span><span class="sxs-lookup"><span data-stu-id="1ac82-281">`InstanceCount = "1"`.</span></span> <span data-ttu-id="1ac82-282">이 경우 hello 서비스의 인스턴스가 하나만 hello 클러스터에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-282">In this case, only one instance of hello service is deployed in hello cluster.</span></span> <span data-ttu-id="1ac82-283">서비스 패브릭 스케줄러 노드 hello 서비스에 배포 된 toobe 되기 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-283">Service Fabric's scheduler determines which node hello service is going toobe deployed on.</span></span>
* <span data-ttu-id="1ac82-284">`InstanceCount ="-1"`</span><span class="sxs-lookup"><span data-stu-id="1ac82-284">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="1ac82-285">이 경우 hello 서비스의 인스턴스 하나 hello 서비스 패브릭 클러스터의 모든 노드에 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-285">In this case, one instance of hello service is deployed on every node in hello Service Fabric cluster.</span></span> <span data-ttu-id="1ac82-286">hello 결과 (하나만)의 인스턴스가 단 각 노드에 대 한 hello 서비스 hello 클러스터에 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-286">hello result is having one (and only one) instance of hello service for each node in hello cluster.</span></span>

<span data-ttu-id="1ac82-287">클라이언트 응용 프로그램 필요 너무 "연결" hello 클러스터 toouse hello 끝점의 hello 노드 tooany 때문에 이것이 프런트 엔드 응용 프로그램 (예를 들어 REST 끝점의 경우)에 대 한 유용한 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-287">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need too"connect" tooany of hello nodes in hello cluster toouse hello endpoint.</span></span> <span data-ttu-id="1ac82-288">예를 들어 hello 서비스 패브릭 클러스터의 모든 노드에 부하 분산 장치 연결된 tooa 하는 경우이 구성은 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-288">This configuration can also be used when, for example, all nodes of hello Service Fabric cluster are connected tooa load balancer.</span></span> <span data-ttu-id="1ac82-289">클라이언트 트래픽이 hello 클러스터의 모든 노드에서 실행 되는 hello 서비스에서 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-289">Client traffic can then be distributed across hello service that is running on all nodes in hello cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="1ac82-290">실행 중인 응용 프로그램 확인</span><span class="sxs-lookup"><span data-stu-id="1ac82-290">Check your running application</span></span>
<span data-ttu-id="1ac82-291">서비스 패브릭 탐색기 hello 서비스가 실행 되 고 hello 노드를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-291">In Service Fabric Explorer, identify hello node where hello service is running.</span></span> <span data-ttu-id="1ac82-292">이 예제에서는 Node1에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-292">In this example, it runs on Node1:</span></span>

![서비스가 실행 중인 노드](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="1ac82-294">Toohello 노드를 탐색 하 고 toohello 응용 프로그램을 찾아볼 경우 hello 필수 노드 정보를 디스크에서의 위치를 포함 하 여 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-294">If you navigate toohello node and browse toohello application, you see hello essential node information, including its location on disk.</span></span>

![디스크 상의 위치](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="1ac82-296">서버 탐색기를 사용 하 여 toohello 디렉터리를 찾을 때는 hello 다음 스크린 샷에서 같이 hello 작업 디렉터리 및 hello 서비스의 로그 폴더를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-296">If you browse toohello directory by using Server Explorer, you can find hello working directory and hello service's log folder, as shown in hello following screenshot:</span></span> 

![로그 위치](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="1ac82-298">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ac82-298">Next steps</span></span>
<span data-ttu-id="1ac82-299">이 문서에서는 배웠습니다 어떻게 toopackage 게스트 실행 파일 및 tooService 패브릭 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac82-299">In this article, you have learned how toopackage a guest executable and deploy it tooService Fabric.</span></span> <span data-ttu-id="1ac82-300">다음 관련된 정보 및 작업에 대 한 아티클을 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="1ac82-300">See hello following articles for related information and tasks.</span></span>

* <span data-ttu-id="1ac82-301">[패키징 및 배포 게스트 실행 파일에 대 한 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), hello 패키징 도구의 링크 toohello 시험판 포함</span><span class="sxs-lookup"><span data-stu-id="1ac82-301">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link toohello prerelease of hello packaging tool</span></span>
* [<span data-ttu-id="1ac82-302">REST를 사용 하 여 hello 명명 서비스를 통해 두 개의 게스트 실행 파일 (C# 및 nodejs) 통신의 샘플</span><span class="sxs-lookup"><span data-stu-id="1ac82-302">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="1ac82-303">여러 개의 게스트 실행 파일 배포</span><span class="sxs-lookup"><span data-stu-id="1ac82-303">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="1ac82-304">Visual Studio를 사용하여 처음으로 서비스 패브릭 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="1ac82-304">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
