---
title: "Azure Service Fabric에 기존 실행 파일 배포 | Microsoft Docs"
description: "Service Fabric 클러스터에 배포할 수 있도록 기존 응용 프로그램을 게스트 실행 파일로 패키징하는 방법에 대한 연습"
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
ms.openlocfilehash: a1db3dda674ffe43587333d88f3816549af3019c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-guest-executable-to-service-fabric"></a><span data-ttu-id="d83e4-103">서비스 패브릭에 게스트 실행 파일 배포</span><span class="sxs-lookup"><span data-stu-id="d83e4-103">Deploy a guest executable to Service Fabric</span></span>
<span data-ttu-id="d83e4-104">Azure Service Fabric에서 Node.js, Java 또는 C++과 같은 모든 종류의 코드를 서비스로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="d83e4-105">Service Fabric에서는 이러한 유형의 서비스를 게스트 실행 파일이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-105">Service Fabric refers to these types of services as guest executables.</span></span>

<span data-ttu-id="d83e4-106">게스트 실행 파일은 서비스 패브릭에서 상태 비저장 서비스처럼 취급됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="d83e4-107">결과적으로 가용성 및 기타 메트릭을 기반으로 클러스터의 노드에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="d83e4-108">이 문서에서는 Visual Studio 또는 명령줄 유틸리티를 사용하여 Service Fabric 클러스터에 게스트 실행 파일을 패키징 및 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-108">This article describes how to package and deploy a guest executable to a Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="d83e4-109">이 문서에서는 게스트 실행 파일을 패키징하고 Service Fabric에 배포하는 단계를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-109">In this article, we cover the steps to package a guest executable and deploy it to Service Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="d83e4-110">서비스 패브릭에서 게스트 실행 파일을 실행할 때의 이점</span><span class="sxs-lookup"><span data-stu-id="d83e4-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="d83e4-111">Service Fabric 클러스터에서 게스트 실행 파일을 실행하면 다음과 같은 몇 가지 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-111">There are several advantages to running a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="d83e4-112">고가용성.</span><span class="sxs-lookup"><span data-stu-id="d83e4-112">High availability.</span></span> <span data-ttu-id="d83e4-113">Service Fabric에서 실행되는 응용 프로그램은 고가용성 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="d83e4-114">Service Fabric은 응용 프로그램 인스턴스가 실행 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="d83e4-115">상태 모니터링.</span><span class="sxs-lookup"><span data-stu-id="d83e4-115">Health monitoring.</span></span> <span data-ttu-id="d83e4-116">Service Fabric 상태 모니터링은 응용 프로그램이 실행 중인지 감지하고 오류가 있으면 진단 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="d83e4-117">응용 프로그램 수명 주기 관리.</span><span class="sxs-lookup"><span data-stu-id="d83e4-117">Application lifecycle management.</span></span> <span data-ttu-id="d83e4-118">Service Fabric은 가동 중지 시간 없이 업그레이드를 제공할 뿐 아니라 업그레이드 중에 나쁜 상태 이벤트가 보고되면 이전 버전으로 자동 롤백을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback to the previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="d83e4-119">밀도.</span><span class="sxs-lookup"><span data-stu-id="d83e4-119">Density.</span></span> <span data-ttu-id="d83e4-120">한 클러스터에서 여러 응용 프로그램을 실행할 수 있으므로 응용 프로그램을 고유의 하드웨어에서 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-120">You can run multiple applications in a cluster, which eliminates the need for each application to run on its own hardware.</span></span>
* <span data-ttu-id="d83e4-121">검색 가능성: REST 사용 Service Fabric 명명 서비스를 호출하여 클러스터에서 다른 서비스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-121">Discoverability: Using REST you can call the Service Fabric Naming service to find other services in the cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="d83e4-122">샘플</span><span class="sxs-lookup"><span data-stu-id="d83e4-122">Samples</span></span>
* [<span data-ttu-id="d83e4-123">게스트 실행 파일을 패키징 및 배포하는 샘플</span><span class="sxs-lookup"><span data-stu-id="d83e4-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="d83e4-124">REST를 사용하여 이름 지정 서비스를 통해 통신하는 두 게스트 실행 파일(C# 및 nodejs)의 샘플</span><span class="sxs-lookup"><span data-stu-id="d83e4-124">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="d83e4-125">응용 프로그램 및 서비스 매니페스트 파일 개요</span><span class="sxs-lookup"><span data-stu-id="d83e4-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="d83e4-126">게스트 실행 파일을 배포하는 일환으로 [응용 프로그램 모델](service-fabric-application-model.md)에 설명된 Service Fabric 패키징 및 배포 모델을 이해하는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-126">As part of deploying a guest executable, it is useful to understand the Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="d83e4-127">Service Fabric 패키징 모델은 두 XML 파일(응용 프로그램 및 서비스 매니페스트)에 의존합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-127">The Service Fabric packaging model relies on two XML files: the application and service manifests.</span></span> <span data-ttu-id="d83e4-128">ApplicationManifest.xml 및 ServiceManifest.xml에 대한 스키마 정의는 Service Fabric SDK와 함께 *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-128">The schema definition for the ApplicationManifest.xml and ServiceManifest.xml files is installed with the Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="d83e4-129">**응용 프로그램 매니페스트** 응용 프로그램 매니페스트는 응용 프로그램을 설명하는 데 사용되며</span><span class="sxs-lookup"><span data-stu-id="d83e4-129">**Application manifest** The application manifest is used to describe the application.</span></span> <span data-ttu-id="d83e4-130">응용 프로그램을 구성하는 서비스와 하나 이상의 서비스 배포 방법(예: 인스턴스 수)을 정의하는 데 사용되는 기타 매개 변수를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-130">It lists the services that compose it, and other parameters that are used to define how one or more services should be deployed, such as the number of instances.</span></span>

  <span data-ttu-id="d83e4-131">Service Fabric에서 응용 프로그램은 배포 및 업그레이드 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="d83e4-132">응용 프로그램은 잠재적인 오류 및 잠재적 롤백이 관리되는 하나의 단위로 업그레이드될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="d83e4-133">Service Fabric은 업그레이드 프로세스의 성공을 보장하며, 업그레이드가 실패할 경우 응용 프로그램을 알 수 없거나 불안정한 상태로 남겨 두지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-133">Service Fabric guarantees that the upgrade process is either successful, or, if the upgrade fails, does not leave the application in an unknown or unstable state.</span></span>
* <span data-ttu-id="d83e4-134">**서비스 매니페스트** 서비스 매니페스트는 서비스의 구성 요소를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-134">**Service manifest** The service manifest describes the components of a service.</span></span> <span data-ttu-id="d83e4-135">서비스의 이름 및 유형과 같은 데이터와 그에 대한 코드 및 구성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-135">It includes data, such as the name and type of service, and its code and configuration.</span></span> <span data-ttu-id="d83e4-136">또한 서비스 매니페스트는 서비스가 배포되면 서비스를 구성하는 데 사용할 수 있는 몇 가지 추가 매개 변수도 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-136">The service manifest also includes some additional parameters that can be used to configure the service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="d83e4-137">응용 프로그램 패키지 파일 구조</span><span class="sxs-lookup"><span data-stu-id="d83e4-137">Application package file structure</span></span>
<span data-ttu-id="d83e4-138">응용 프로그램을 Service Fabric에 배포하려면 응용 프로그램은 미리 정의된 디렉터리 구조를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-138">To deploy an application to Service Fabric, the application should follow a predefined directory structure.</span></span> <span data-ttu-id="d83e4-139">다음은 해당 구조의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-139">The following is an example of that structure.</span></span>

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

<span data-ttu-id="d83e4-140">ApplicationPackageRoot는 응용 프로그램을 정의하는 ApplicationManifest.xml 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-140">The ApplicationPackageRoot contains the ApplicationManifest.xml file that defines the application.</span></span> <span data-ttu-id="d83e4-141">응용 프로그램에 포함된 각 서비스에 대한 하위 디렉터리 서비스는 서비스가 필요한 모든 아티팩트를 포함하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-141">A subdirectory for each service included in the application is used to contain all the artifacts that the service requires.</span></span> <span data-ttu-id="d83e4-142">이러한 하위 디렉터리는 ServiceManifest.xml이며 일반적으로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-142">These subdirectories are the ServiceManifest.xml and, typically, the following:</span></span>

* <span data-ttu-id="d83e4-143">*Code*.</span><span class="sxs-lookup"><span data-stu-id="d83e4-143">*Code*.</span></span> <span data-ttu-id="d83e4-144">이 디렉터리는 서비스 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-144">This directory contains the service code.</span></span>
* <span data-ttu-id="d83e4-145">*Config*.</span><span class="sxs-lookup"><span data-stu-id="d83e4-145">*Config*.</span></span> <span data-ttu-id="d83e4-146">이 디렉터리는 런타임에 서비스가 액세스하여 특정 구성 설정을 검색할 수 있는 settings.xml 파일(필요한 경우 다른 파일도 포함)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-146">This directory contains a Settings.xml file (and other files if necessary) that the service can access at runtime to retrieve specific configuration settings.</span></span>
* <span data-ttu-id="d83e4-147">*Data*.</span><span class="sxs-lookup"><span data-stu-id="d83e4-147">*Data*.</span></span> <span data-ttu-id="d83e4-148">서비스에 필요할 수도 있는 추가 로컬 데이터를 저장하는 추가 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-148">This is an additional directory to store additional local data that the service may need.</span></span> <span data-ttu-id="d83e4-149">Data는 사용 후 삭제되는 데이터를 저장하는 용도로만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-149">Data should be used to store only ephemeral data.</span></span> <span data-ttu-id="d83e4-150">예를 들어 장애 조치 중에 서비스를 다시 배치해야 하는 경우 Service Fabric은 변경 내용을 데이터 디렉터리에 복사 또는 복제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-150">Service Fabric does not copy or replicate changes to the data directory if the service needs to be relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="d83e4-151">`config` 및 `data` 디렉터리가 필요 없으면 만들지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-151">You don't have to create the `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="d83e4-152">기존 실행 파일 패키징</span><span class="sxs-lookup"><span data-stu-id="d83e4-152">Package an existing executable</span></span>
<span data-ttu-id="d83e4-153">게스트 실행 파일을 패키징할 경우 Visual Studio 프로젝트 템플릿을 사용하거나 [응용 프로그램 패키지를 수동으로 만들도록](#manually) 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-153">When packaging a guest executable, you can choose either to use a Visual Studio project template or to [create the application package manually](#manually).</span></span> <span data-ttu-id="d83e4-154">Visual Studio를 사용하면 새 프로젝트 템플릿에 의해 응용 프로그램 패키지 구조 및 매니페스트 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-154">Using Visual Studio, the application package structure and manifest files are created by the new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="d83e4-155">기존 Windows 실행 파일을 서비스로 패키징하는 가장 쉬운 방법은 Visual Studio 및 Linux의 Yeoman을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-155">The easiest way to package an existing Windows executable into a service is to use Visual Studio and on Linux to use Yeoman</span></span>
>

## <a name="use-visual-studio-to-package-and-deploy-an-existing-executable"></a><span data-ttu-id="d83e4-156">Visual Studio를 사용하여 기존 실행 파일 패키징 및 배포</span><span class="sxs-lookup"><span data-stu-id="d83e4-156">Use Visual Studio to package and deploy an existing executable</span></span>
<span data-ttu-id="d83e4-157">Visual Studio는 게스트 실행 파일을 서비스 패브릭 클러스터에 배포할 수 있도록 서비스 패브릭 서비스 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-157">Visual Studio provides a Service Fabric service template to help you deploy a guest executable to a Service Fabric cluster.</span></span>

1. <span data-ttu-id="d83e4-158">**파일** > **새 프로젝트**를 선택하여 Service Fabric 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-158">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="d83e4-159">**게스트 실행 파일**을 서비스 템플릿으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-159">Choose **Guest Executable** as the service template.</span></span>
3. <span data-ttu-id="d83e4-160">**찾아보기**를 클릭하여 실행 파일이 포함된 폴더를 선택하고 매개 변수의 나머지를 입력하여 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-160">Click **Browse** to select the folder with your executable and fill in the rest of the parameters to create the service.</span></span>
   * <span data-ttu-id="d83e4-161">*코드 패키지 동작*.</span><span class="sxs-lookup"><span data-stu-id="d83e4-161">*Code Package Behavior*.</span></span> <span data-ttu-id="d83e4-162">폴더의 모든 콘텐츠를 Visual Studio 프로젝트에 복사하도록 설정할 수 있으며 이것은 실행 파일이 변경되지 않는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-162">Can be set to copy all the content of your folder to the Visual Studio Project, which is useful if the executable does not change.</span></span> <span data-ttu-id="d83e4-163">실행 파일을 변경하고 동적으로 새 빌드를 선택할 수 있는 기능을 원하는 경우 대신 폴더에 연결하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-163">If you expect the executable to change and want the ability to pick up new builds dynamically, you can choose to link to the folder instead.</span></span> <span data-ttu-id="d83e4-164">Visual Studio에서 응용 프로그램 프로젝트를 만들 경우 연결된 폴더를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-164">You can use linked folders when creating the application project in Visual Studio.</span></span> <span data-ttu-id="d83e4-165">이는 프로젝트 내에서 원본 위치에 연결되면 원본 대상에서 게스트 실행 파일을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-165">This links to the source location from within the project, making it possible for you to update the guest executable in its source destination.</span></span> <span data-ttu-id="d83e4-166">이 업데이트는 빌드의 응용 프로그램 패키지의 일부가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-166">Those updates become part of the application package on build.</span></span>
   * <span data-ttu-id="d83e4-167">*프로그램*은 서비스를 시작하기 위해 실행해야 하는 실행 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-167">*Program* specifies the executable that should be run to start the service.</span></span>
   * <span data-ttu-id="d83e4-168">*인수*는 실행 파일에 전달되어야 하는 인수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-168">*Arguments* specifies the arguments that should be passed to the executable.</span></span> <span data-ttu-id="d83e4-169">인수가 있는 매개 변수 목록이 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-169">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="d83e4-170">*WorkingFolder*는 시작될 프로세스에 대한 작업 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-170">*WorkingFolder* specifies the working directory for the process that is going to be started.</span></span> <span data-ttu-id="d83e4-171">세 가지 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-171">You can specify three values:</span></span>
     * <span data-ttu-id="d83e4-172">`CodeBase`는 작업 디렉터리가 응용 프로그램 패키지의 코드 디렉터리에 설정되도록 지정합니다(이전 파일 구조에 표시된 `Code` 디렉터리).</span><span class="sxs-lookup"><span data-stu-id="d83e4-172">`CodeBase` specifies that the working directory is going to be set to the code directory in the application package (`Code` directory shown in the preceding file structure).</span></span>
     * <span data-ttu-id="d83e4-173">`CodePackage`는 작업 디렉터리가 응용 프로그램 패키지의 루트에 설정되도록 지정합니다(이전 파일 구조에 표시된 `GuestService1Pkg`).</span><span class="sxs-lookup"><span data-stu-id="d83e4-173">`CodePackage` specifies that the working directory is going to be set to the root of the application package    (`GuestService1Pkg` shown in the preceding file structure).</span></span>
     * <span data-ttu-id="d83e4-174">`Work`는 파일이 work라는 하위 디렉터리에 배치되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-174">`Work` specifies that the files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="d83e4-175">서비스에 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-175">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="d83e4-176">서비스에서 통신에 끝점이 필요한 경우 이제 프로토콜, 포트, 형식을 ServiceManifest.xml 파일에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-176">If your service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="d83e4-177">예: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`</span><span class="sxs-lookup"><span data-stu-id="d83e4-177">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="d83e4-178">이제 패키지를 사용하고 Visual Studio에서 솔루션을 디버깅하여 로컬 클러스터에 대해 작업을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-178">You can now use the package and publish action against your local cluster by debugging the solution in Visual Studio.</span></span> <span data-ttu-id="d83e4-179">준비가 되면 원격 클러스터로 응용 프로그램을 게시하거나 원본 제어에 대한 솔루션을 체크 인합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-179">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span></span>
7. <span data-ttu-id="d83e4-180">Service Fabric Explorer에서 실행 중인 게스트 실행 파일 서비스를 보는 방법을 보려면 이 문서의 끝으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-180">Go to the end of this article to see how to view your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-to-package-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="d83e4-181">Yoeman을 사용하여 Linux에서 기존 실행 파일을 수동으로 패키징 및 배포</span><span class="sxs-lookup"><span data-stu-id="d83e4-181">Use Yoeman to package and deploy an existing executable on Linux</span></span>

<span data-ttu-id="d83e4-182">Linux에서 실행되는 게스트를 만들고 배포하는 절차는 csharp 또는 java 응용 프로그램 배포와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-182">The procedure for creating and deploying a guest executable on Linux is the same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="d83e4-183">터미널에서 `yo azuresfguest`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-183">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="d83e4-184">응용 프로그램의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-184">Name your application.</span></span>
3. <span data-ttu-id="d83e4-185">서비스 이름을 지정하고 호출해야 하는 실행 파일 및 매개 변수의 경로를 포함하는 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-185">Name your service, and provide the details including path of the executable and the parameters it must be invoked with.</span></span>

<span data-ttu-id="d83e4-186">Yeoman은 설치 및 제거 스크립트와 함께 해당 응용 프로그램과 매니페스트 파일로 응용 프로그램 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-186">Yeoman creates an application package with the appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="d83e4-187">기존 실행 파일을 수동으로 패키징하고 배포하기</span><span class="sxs-lookup"><span data-stu-id="d83e4-187">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="d83e4-188">게스트 실행 파일을 수동으로 패키징하는 과정은 다음과 같은 일반 단계를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-188">The process of manually packaging a guest executable is based on the following general steps:</span></span>

1. <span data-ttu-id="d83e4-189">패키지 디렉터리 구조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-189">Create the package directory structure.</span></span>
2. <span data-ttu-id="d83e4-190">응용 프로그램의 코드 및 구성 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-190">Add the application's code and configuration files.</span></span>
3. <span data-ttu-id="d83e4-191">서비스 매니페스트 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-191">Edit the service manifest file.</span></span>
4. <span data-ttu-id="d83e4-192">응용 프로그램 매니페스트 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-192">Edit the application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you to create the ApplicationPackage automatically. The tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-the-package-directory-structure"></a><span data-ttu-id="d83e4-193">패키지 디렉터리 구조 만들기</span><span class="sxs-lookup"><span data-stu-id="d83e4-193">Create the package directory structure</span></span>
<span data-ttu-id="d83e4-194">이전 섹션에서 "응용 프로그램 패키지 파일 구조"에 설명된 대로 디렉터리 구조를 만들어서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-194">You can start by creating the directory structure, as described in the preceding section, "Application package file structure."</span></span>

### <a name="add-the-applications-code-and-configuration-files"></a><span data-ttu-id="d83e4-195">응용 프로그램의 코드 및 구성 파일 추가</span><span class="sxs-lookup"><span data-stu-id="d83e4-195">Add the application's code and configuration files</span></span>
<span data-ttu-id="d83e4-196">디렉터리 구조를 만든 후에 응용 프로그램의 코드 및 구성 파일을 코드 및 구성 디렉터리 아래에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-196">After you have created the directory structure, you can add the application's code and configuration files under the code and config directories.</span></span> <span data-ttu-id="d83e4-197">코드 또는 구성 디렉터리 아래에 하위 디렉터리 또는 추가 디렉터리를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-197">You can also create additional directories or subdirectories under the code or config directories.</span></span>

<span data-ttu-id="d83e4-198">Service Fabric은 응용 프로그램 루트 디렉터리의 내용에 대한 `xcopy`를 수행하므로 두 상위 디렉터리인 code 및 settings를 만들지 않고도 사용할 수 있는 미리 정의된 구조가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-198">Service Fabric does an `xcopy` of the content of the application root directory, so there is no predefined structure to use other than creating two top directories, code and settings.</span></span> <span data-ttu-id="d83e4-199">하지만 원한다면 다른 이름을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-199">(You can pick different names if you want.</span></span> <span data-ttu-id="d83e4-200">자세한 내용은 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d83e4-200">More details are in the next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="d83e4-201">응용 프로그램이 필요한 모든 파일 및 종속성을 포함했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-201">Make sure that you include all the files and dependencies that the application needs.</span></span> <span data-ttu-id="d83e4-202">Service Fabric은 응용 프로그램의 서비스를 배포할 클러스터의 모든 노드에서 응용 프로그램 패키지의 콘텐츠를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-202">Service Fabric copies the content of the application package on all nodes in the cluster where the application's services are going to be deployed.</span></span> <span data-ttu-id="d83e4-203">패키지에는 응용 프로그램 실행에 필요한 모든 코드가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-203">The package should contain all the code that the application needs to run.</span></span> <span data-ttu-id="d83e4-204">종속성이 이미 설치되어 있다고 가정하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d83e4-204">Do not assume that the dependencies are already installed.</span></span>
>
>

### <a name="edit-the-service-manifest-file"></a><span data-ttu-id="d83e4-205">서비스 매니페스트 파일 편집</span><span class="sxs-lookup"><span data-stu-id="d83e4-205">Edit the service manifest file</span></span>
<span data-ttu-id="d83e4-206">다음 정보를 포함하도록 서비스 매니페스트 파일을 편집하는 것이 다음 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-206">The next step is to edit the service manifest file to include the following information:</span></span>

* <span data-ttu-id="d83e4-207">서비스 형식 이름</span><span class="sxs-lookup"><span data-stu-id="d83e4-207">The name of the service type.</span></span> <span data-ttu-id="d83e4-208">서비스 패브릭이 서비스를 식별하기 위해 사용하는 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-208">This is an ID that Service Fabric uses to identify a service.</span></span>
* <span data-ttu-id="d83e4-209">응용 프로그램을 시작하기 위해 사용하는 명령(ExeHost).</span><span class="sxs-lookup"><span data-stu-id="d83e4-209">The command to use to launch the application (ExeHost).</span></span>
* <span data-ttu-id="d83e4-210">응용 프로그램을 설치하기 위해 실행해야 하는 모든 스크립트(SetupEntryPoint)</span><span class="sxs-lookup"><span data-stu-id="d83e4-210">Any script that needs to be run to set up the application (SetupEntrypoint).</span></span>

<span data-ttu-id="d83e4-211">다음은 `ServiceManifest.xml` 파일의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-211">The following is an example of a `ServiceManifest.xml` file:</span></span>

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

<span data-ttu-id="d83e4-212">다음 섹션에서 업데이트해야 하는 파일의 다른 부분을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-212">The following sections go over the different parts of the file that you need to update.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="d83e4-213">ServiceTypes 업데이트</span><span class="sxs-lookup"><span data-stu-id="d83e4-213">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="d83e4-214">`ServiceTypeName`의 이름을 자유롭게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-214">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="d83e4-215">이 값은 `ApplicationManifest.xml` 파일에서 서비스를 식별하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-215">The value is used in the `ApplicationManifest.xml` file to identify the service.</span></span>
* <span data-ttu-id="d83e4-216">`UseImplicitHost="true"`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-216">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="d83e4-217">이 특성은 서비스가 자체 포함된 앱을 기반으로 하므로 모든 서비스 패브릭이 응용 프로그램을 프로세스로 실행하여 상태를 모니터링해야 한다는 사실을 서비스 패브릭에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-217">This attribute tells Service Fabric that the service is based on a self-contained app, so all Service Fabric needs to do is to launch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="d83e4-218">CodePackage 업데이트</span><span class="sxs-lookup"><span data-stu-id="d83e4-218">Update CodePackage</span></span>
<span data-ttu-id="d83e4-219">CodePackage 요소는 서비스 코드의 위치(및 버전)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-219">The CodePackage element specifies the location (and version) of the service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="d83e4-220">`Name` 요소는 서비스 코드가 들어 있는 응용 프로그램 패키지의 디렉터리 이름을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-220">The `Name` element is used to specify the name of the directory in the application package that contains the service's code.</span></span> <span data-ttu-id="d83e4-221">`CodePackage`에도 `version` 특성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-221">`CodePackage` also has the `version` attribute.</span></span> <span data-ttu-id="d83e4-222">이 요소는 코드 버전을 지정하는 데 사용할 수 있으며, Service Fabric에서 응용 프로그램 수명 주기 관리 인프라를 사용하여 서비스 코드를 업그레이드하는 데 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-222">This can be used to specify the version of the code, and can also potentially be used to upgrade the service's code by using the application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="d83e4-223">선택 사항: SetupEntryPoint 업데이트</span><span class="sxs-lookup"><span data-stu-id="d83e4-223">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="d83e4-224">SetupEntryPoint 요소는 서비스의 코드를 시작하기 전에 실행되어야 하는 실행 파일 또는 배치 파일을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-224">The SetupEntryPoint element is used to specify any executable or batch file that should be executed before the service's code is launched.</span></span> <span data-ttu-id="d83e4-225">선택적 단계이므로 초기화가 필수가 아닌 경우에는 포함되지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-225">It is an optional step, so it does not need to be included if there is no initialization required.</span></span> <span data-ttu-id="d83e4-226">SetupEntrypoint는 서비스를 다시 시작할 때마다 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-226">The SetupEntryPoint is executed every time the service is restarted.</span></span>

<span data-ttu-id="d83e4-227">SetupEntryPoint가 하나밖에 없으므로 응용 프로그램의 설치에 여러 스크립트가 필요한 경우 설치 스크립트를 배치 파일 하나에 그룹화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-227">There is only one SetupEntryPoint, so setup scripts need to be grouped in a single batch file if the application's setup requires multiple scripts.</span></span> <span data-ttu-id="d83e4-228">SetupEntryPoint는 실행 파일, 배치 파일, PowerShell cmdlet 등 각종 파일을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-228">The SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="d83e4-229">자세한 내용은 [SetupEntryPoint 구성](service-fabric-application-runas-security.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d83e4-229">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="d83e4-230">앞의 예제에서 SetupEntryPoint는 코드 디렉터리의 `scripts` 하위 디렉터리에 있는 `LaunchConfig.cmd`라는 배치 파일을 실행합니다(WorkingFolder 요소가 CodeBase로 설정되어 있다고 가정).</span><span class="sxs-lookup"><span data-stu-id="d83e4-230">In the preceding example, the SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in the `scripts` subdirectory of the code directory (assuming the WorkingFolder element is set to CodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="d83e4-231">EntryPoint 업데이트</span><span class="sxs-lookup"><span data-stu-id="d83e4-231">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="d83e4-232">서비스 매니페스트 파일의 `EntryPoint` 요소는 서비스를 시작하는 방법을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-232">The `EntryPoint` element in the service manifest file is used to specify how to launch the service.</span></span> <span data-ttu-id="d83e4-233">`ExeHost` 요소는 서비스를 시작하는 데 사용되어야 하는 실행 파일(및 인수)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-233">The `ExeHost` element specifies the executable (and arguments) that should be used to launch the service.</span></span>

* <span data-ttu-id="d83e4-234">`Program`은 서비스를 시작해야 하는 실행 파일의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-234">`Program` specifies the name of the executable that should start the service.</span></span>
* <span data-ttu-id="d83e4-235">`Arguments` 는 실행 파일에 전달되어야 하는 인수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-235">`Arguments` specifies the arguments that should be passed to the executable.</span></span> <span data-ttu-id="d83e4-236">인수가 있는 매개 변수 목록이 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-236">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="d83e4-237">`WorkingFolder`는 곧 시작될 프로세스의 작업 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-237">`WorkingFolder` specifies the working directory for the process that is going to be started.</span></span> <span data-ttu-id="d83e4-238">세 가지 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-238">You can specify three values:</span></span>
  * <span data-ttu-id="d83e4-239">`CodeBase`는 작업 디렉터리가 응용 프로그램 패키지의 코드 디렉터리에 설정되도록 지정합니다(이전 파일 구조의 `Code` 디렉터리).</span><span class="sxs-lookup"><span data-stu-id="d83e4-239">`CodeBase` specifies that the working directory is going to be set to the code directory in the application package (`Code` directory in the preceding file structure).</span></span>
  * <span data-ttu-id="d83e4-240">`CodePackage`는 작업 디렉터리가 응용 프로그램 패키지의 루트에 설정되도록 지정합니다(이전 파일 구조의 `GuestService1Pkg`).</span><span class="sxs-lookup"><span data-stu-id="d83e4-240">`CodePackage` specifies that the working directory is going to be set to the root of the application package    (`GuestService1Pkg` in the preceding file structure).</span></span>
    * <span data-ttu-id="d83e4-241">`Work`는 파일이 work라는 하위 디렉터리에 배치되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-241">`Work` specifies that the files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="d83e4-242">WorkingFolder는 응용 프로그램 또는 초기화 스크립트에서 상대 경로를 사용할 수 있도록 올바른 작업 디렉터리를 설정하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-242">The WorkingFolder is useful to set the correct working directory so that relative paths can be used by either the application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="d83e4-243">통신을 위해 끝점을 업데이트하고 명명 서비스에 등록</span><span class="sxs-lookup"><span data-stu-id="d83e4-243">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="d83e4-244">앞의 예제에서 `Endpoint` 요소는 응용 프로그램에서 수신 대기할 수 있는 끝점을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-244">In the preceding example, the `Endpoint` element specifies the endpoints that the application can listen on.</span></span> <span data-ttu-id="d83e4-245">이 예제에서 Node.js 응용 프로그램은 포트 3000의 http에 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-245">In this example, the Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="d83e4-246">또한 다른 서비스가 이 서비스에 대한 끝점 주소를 검색할 수 있도록 Service Fabric에 이 끝점을 명명 서비스에 게시하도록 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-246">Furthermore you can ask Service Fabric to publish this endpoint to the Naming Service so other services can discover the endpoint address to this service.</span></span> <span data-ttu-id="d83e4-247">이렇게 하면 게스트 실행 파일인 서비스 간에 통신을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-247">This enables you to be able to communicate between services that are guest executables.</span></span>
<span data-ttu-id="d83e4-248">게시된 끝점 주소는 `UriScheme://IPAddressOrFQDN:Port/PathSuffix`형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-248">The published endpoint address is of the form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="d83e4-249">`UriScheme` 및 `PathSuffix`는 선택적 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-249">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="d83e4-250">`IPAddressOrFQDN`은 이 실행 파일이 배치되고 계산되는 노드의 IP 주소 또는 정규화된 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-250">`IPAddressOrFQDN` is the IP address or fully qualified domain name of the node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="d83e4-251">다음 예제에서 서비스가 배포되면, 서비스 인스턴스에 대해 게시된 `http://10.1.4.92:3000/myapp/`와 유사한 끝점이 Service Fabric Explorer에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-251">In the following example, once the service is deployed, in Service Fabric Explorer you see an endpoint similar to `http://10.1.4.92:3000/myapp/` published for the service instance.</span></span> <span data-ttu-id="d83e4-252">또는 로컬 컴퓨터인 경우, `http://localhost:3000/myapp/`가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-252">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="d83e4-253">이 주소를 [역방향 프록시](service-fabric-reverseproxy.md)와 사용하여 서비스 간에 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-253">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) to communicate between services.</span></span>

### <a name="edit-the-application-manifest-file"></a><span data-ttu-id="d83e4-254">응용 프로그램 매니페스트 파일 편집</span><span class="sxs-lookup"><span data-stu-id="d83e4-254">Edit the application manifest file</span></span>
<span data-ttu-id="d83e4-255">`Servicemanifest.xml` 파일을 구성했으면 `ApplicationManifest.xml` 파일을 변경하여 올바른 서비스 유형 및 이름이 사용되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-255">Once you have configured the `Servicemanifest.xml` file, you need to make some changes to the `ApplicationManifest.xml` file to ensure that the correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="d83e4-256">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="d83e4-256">ServiceManifestImport</span></span>
<span data-ttu-id="d83e4-257">`ServiceManifestImport` 요소에서 앱에 포함할 서비스를 하나 이상 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-257">In the `ServiceManifestImport` element, you can specify one or more services that you want to include in the app.</span></span> <span data-ttu-id="d83e4-258">서비스는 `ServiceManifest.xml` 파일이 있는 디렉터리의 이름을 지정하는 `ServiceManifestName`으로 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-258">Services are referenced with `ServiceManifestName`, which specifies the name of the directory where the `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="d83e4-259">로깅 설정</span><span class="sxs-lookup"><span data-stu-id="d83e4-259">Set up logging</span></span>
<span data-ttu-id="d83e4-260">게스트 실행 파일의 경우 응용 프로그램 및 구성 스크립트가 오류를 표시할 때 콘솔 로그를 볼 수 있으므로 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-260">For guest executables, it is useful to be able to see console logs to find out if the application and configuration scripts show any errors.</span></span>
<span data-ttu-id="d83e4-261">콘솔 리디렉션은 `ConsoleRedirection` 요소를 사용하여 `ServiceManifest.xml` 파일에 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-261">Console redirection can be configured in the `ServiceManifest.xml` file using the `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="d83e4-262">절대 프로덕션에 배포된 응용 프로그램의 콘솔 리디렉션 정책은 사용하지 마세요. 응용 프로그램 장애 조치(failover)에 영향을 줄 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-262">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span></span> <span data-ttu-id="d83e4-263">로컬 개발 및 디버깅 목적으로*만* 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="d83e4-263">*Only* use this for local development and debugging purposes.</span></span>  
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

<span data-ttu-id="d83e4-264">`ConsoleRedirection`은 콘솔 출력(stdout 및 stderr)을 작업 디렉터리에 리디렉션하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-264">`ConsoleRedirection` can be used to redirect console output (both stdout and stderr) to a working directory.</span></span> <span data-ttu-id="d83e4-265">이는 Service Fabric 클러스터에서 응용 프로그램을 설치하거나 실행하는 동안 오류가 없는지를 확인하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-265">This provides the ability to verify that there are no errors during the setup or execution of the application in the Service Fabric cluster.</span></span>

<span data-ttu-id="d83e4-266">`FileRetentionCount` 는 작업 디렉터리에 저장되는 파일의 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-266">`FileRetentionCount` determines how many files are saved in the working directory.</span></span> <span data-ttu-id="d83e4-267">예를 들어 값이 5이면 이전 5개 실행에 대한 로그 파일이 작업 디렉터리에 저장되었다는 뜻입니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-267">A value of 5, for example, means that the log files for the previous five executions are stored in the working directory.</span></span>

<span data-ttu-id="d83e4-268">`FileMaxSizeInKb`는 로그 파일의 최대 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-268">`FileMaxSizeInKb` specifies the maximum size of the log files.</span></span>

<span data-ttu-id="d83e4-269">로그 파일은 서비스의 작업 디렉터리 중 하나에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-269">Log files are saved in one of the service's working directories.</span></span> <span data-ttu-id="d83e4-270">파일이 어디에 있는지 확인하려면 Service Fabric Explorer를 사용하여 서비스가 실행 중인 노드와 현재 사용 중인 작업 디렉터리를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-270">To determine where the files are located, use Service Fabric Explorer to determine which node the service is running on, and which working directory is being used.</span></span> <span data-ttu-id="d83e4-271">이 프로세스는 이 문서의 뒷부분에서 다루겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-271">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="d83e4-272">배포</span><span class="sxs-lookup"><span data-stu-id="d83e4-272">Deployment</span></span>
<span data-ttu-id="d83e4-273">마지막 단계는 [응용 프로그램을 배포](service-fabric-deploy-remove-applications.md)하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-273">The last step is to [deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="d83e4-274">다음 PowerShell 스크립트는 로컬 개발 클러스터에 응용 프로그램을 배포하고 새 Service Fabric 서비스를 시작하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-274">The following PowerShell script shows how to deploy your application to the local development cluster, and start a new Service Fabric service.</span></span>

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
> <span data-ttu-id="d83e4-275">패키지가 크거나 파일이 많은 경우 이미지 저장소에 복사하기 전에 [패키지를 압축](service-fabric-package-apps.md#compress-a-package)합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-275">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store if the package is large or has many files.</span></span> <span data-ttu-id="d83e4-276">[여기](service-fabric-deploy-remove-applications.md#upload-the-application-package)서 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="d83e4-276">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="d83e4-277">서비스 패브릭 서비스를 다양한 "구성"으로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-277">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="d83e4-278">예를 들어 단일 또는 다중 인스턴스로 배포할 수도 있고, Service Fabric 클러스터의 각 노드에 서비스 인스턴스가 하나씩 있는 방식으로 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-278">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of the service on each node of the Service Fabric cluster.</span></span>

<span data-ttu-id="d83e4-279">`New-ServiceFabricService` cmdlet의 `InstanceCount` 매개 변수는 서비스 패브릭 클러스터에서 실행되어야 하는 서비스의 인스턴스 개수를 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-279">The `InstanceCount` parameter of the `New-ServiceFabricService` cmdlet is used to specify how many instances of the service should be launched in the Service Fabric cluster.</span></span> <span data-ttu-id="d83e4-280">배포하는 응용 프로그램의 유형에 따라 `InstanceCount` 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-280">You can set the `InstanceCount` value, depending on the type of application that you are deploying.</span></span> <span data-ttu-id="d83e4-281">가장 일반적인 두 가지 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-281">The two most common scenarios are:</span></span>

* <span data-ttu-id="d83e4-282">`InstanceCount = "1"`.</span><span class="sxs-lookup"><span data-stu-id="d83e4-282">`InstanceCount = "1"`.</span></span> <span data-ttu-id="d83e4-283">이 경우 단 한 개의 서비스 인스턴스가 클러스터에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-283">In this case, only one instance of the service is deployed in the cluster.</span></span> <span data-ttu-id="d83e4-284">서비스 패브릭의 스케줄러는 서비스를 배포할 노드를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-284">Service Fabric's scheduler determines which node the service is going to be deployed on.</span></span>
* <span data-ttu-id="d83e4-285">`InstanceCount ="-1"`.</span><span class="sxs-lookup"><span data-stu-id="d83e4-285">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="d83e4-286">이 경우 서비스의 단일 인스턴스가 Service Fabric 클러스터의 모든 노드에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-286">In this case, one instance of the service is deployed on every node in the Service Fabric cluster.</span></span> <span data-ttu-id="d83e4-287">그 결과 클러스터의 각 노드에 대한 서비스의 인스턴스를 하나(및 하나만) 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-287">The result is having one (and only one) instance of the service for each node in the cluster.</span></span>

<span data-ttu-id="d83e4-288">이 구성은 프런트 엔드 응용 프로그램(예: REST 끝점)에 유용합니다. 클라이언트 응용 프로그램은 끝점을 사용하려면 클러스터의 노드에 "연결"해야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-288">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need to "connect" to any of the nodes in the cluster to use the endpoint.</span></span> <span data-ttu-id="d83e4-289">예를 들어, Service Fabric 클러스터의 모든 노드가 부하 분산 장치에 연결된 경우 이 구성을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-289">This configuration can also be used when, for example, all nodes of the Service Fabric cluster are connected to a load balancer.</span></span> <span data-ttu-id="d83e4-290">그러면 클라이언트 트래픽을 클러스터의 모든 노드에서 실행되는 서비스에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-290">Client traffic can then be distributed across the service that is running on all nodes in the cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="d83e4-291">실행 중인 응용 프로그램 확인</span><span class="sxs-lookup"><span data-stu-id="d83e4-291">Check your running application</span></span>
<span data-ttu-id="d83e4-292">서비스 패브릭 탐색기에서 서비스가 실행되고 있는 노드를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-292">In Service Fabric Explorer, identify the node where the service is running.</span></span> <span data-ttu-id="d83e4-293">이 예제에서는 Node1에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-293">In this example, it runs on Node1:</span></span>

![서비스가 실행 중인 노드](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="d83e4-295">노드로 이동하여 응용 프로그램을 찾으면 디스크 상의 위치를 포함하여 필수 노드 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-295">If you navigate to the node and browse to the application, you see the essential node information, including its location on disk.</span></span>

![디스크 상의 위치](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="d83e4-297">서버 탐색기를 사용하여 디렉터리를 찾아보면 다음 스크린샷과 같이 작업 디렉터리 및 서비스의 로그 폴더를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-297">If you browse to the directory by using Server Explorer, you can find the working directory and the service's log folder, as shown in the following screenshot:</span></span> 

![로그 위치](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="d83e4-299">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d83e4-299">Next steps</span></span>
<span data-ttu-id="d83e4-300">이 문서에서는 게스트 실행 파일을 패키징하고 서비스 패브릭에 배포하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="d83e4-300">In this article, you have learned how to package a guest executable and deploy it to Service Fabric.</span></span> <span data-ttu-id="d83e4-301">관련 정보 및 작업에 대해 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d83e4-301">See the following articles for related information and tasks.</span></span>

* <span data-ttu-id="d83e4-302">패키징 도구 시험판의 링크를 포함하여 [게스트 실행 파일을 패키징 및 배포하는 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)</span><span class="sxs-lookup"><span data-stu-id="d83e4-302">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link to the prerelease of the packaging tool</span></span>
* [<span data-ttu-id="d83e4-303">REST를 사용하여 이름 지정 서비스를 통해 통신하는 두 게스트 실행 파일(C# 및 nodejs)의 샘플</span><span class="sxs-lookup"><span data-stu-id="d83e4-303">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="d83e4-304">여러 개의 게스트 실행 파일 배포</span><span class="sxs-lookup"><span data-stu-id="d83e4-304">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="d83e4-305">Visual Studio를 사용하여 처음으로 서비스 패브릭 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="d83e4-305">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
