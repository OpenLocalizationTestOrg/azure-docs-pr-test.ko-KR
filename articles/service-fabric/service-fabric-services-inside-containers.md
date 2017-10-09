---
title: "aaaHow toocontainerize에 Azure 서비스 패브릭 microservices (미리 보기)"
description: "Azure 서비스 패브릭 서비스 패브릭 microservices 새 기능 toocontainerize 추가 되었습니다. 이 기능은 현재 미리 보기로 제공됩니다."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: anmolah
editor: anmolah
ms.assetid: 0b41efb3-4063-4600-89f5-b077ea81fa3a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/04/2017
ms.author: anmola
ms.openlocfilehash: 6edaff73c0828707c7fa736669ba8084663d31ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a><span data-ttu-id="f636a-104">서비스 패브릭 안정성 서비스 하는 toocontainerize 방법 및 Reliable Actors (미리 보기)</span><span class="sxs-lookup"><span data-stu-id="f636a-104">How toocontainerize your Service Fabric Reliable Services and Reliable Actors (Preview)</span></span>

<span data-ttu-id="f636a-105">Service Fabric은 Service Fabric 마이크로 서비스(Reliable Services 및 Reliable Actor 기반 서비스)를 컨테이너화하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-105">Service Fabric supports containerizing Service Fabric microservices (Reliable Services, and Reliable Actor based services).</span></span> <span data-ttu-id="f636a-106">자세한 내용은 [Service Fabric 컨테이너](service-fabric-containers-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f636a-106">For more information, see [service fabric containers](service-fabric-containers-overview.md).</span></span>


 <span data-ttu-id="f636a-107">이 기능은 미리 보기 이므로이 문서에서는 다양 한 단계 tooget 컨테이너 내에서 실행 중인 서비스 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-107">This feature is in preview and this article provides hello various steps tooget your service running inside a container.</span></span>  

> [!NOTE]
> <span data-ttu-id="f636a-108">이 기능은 미리 보기로 제공되며 프로덕션에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-108">This feature is in preview and is not supported in production.</span></span> <span data-ttu-id="f636a-109">현재 이 기능은 Windows에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-109">Currently this feature only works for Windows.</span></span>

## <a name="steps-toocontainerize-your-service-fabric-application"></a><span data-ttu-id="f636a-110">서비스 패브릭 응용 프로그램 toocontainerize 단계</span><span class="sxs-lookup"><span data-stu-id="f636a-110">Steps toocontainerize your Service Fabric Application</span></span>

1. <span data-ttu-id="f636a-111">Visual Studio에서 Service Fabric 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-111">Open your Service Fabric application in Visual Studio.</span></span>

2. <span data-ttu-id="f636a-112">클래스 추가 [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="f636a-112">Add class [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour project.</span></span> <span data-ttu-id="f636a-113">이 클래스의 hello 코드는 도우미 toocorrectly 부하 hello 서비스 패브릭 런타임 바이너리 응용 프로그램 내 때 컨테이너 내에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-113">hello code in this class is a helper toocorrectly load hello Service Fabric runtime binaries inside your application when running inside a container.</span></span>

3. <span data-ttu-id="f636a-114">각 코드 패키지에 대 한 toocontainerize, hello 프로그램 진입점에서 초기화 hello 로더 원할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-114">For each code package you would like toocontainerize, initialize hello loader at hello program entry point.</span></span> <span data-ttu-id="f636a-115">다음 코드 조각 tooyour 프로그램 항목 지점 파일 hello에 표시 된 hello 정적 생성자를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-115">Add hello static constructor shown in hello following code snippet tooyour program entry point file.</span></span>

  ```csharp
  namespace MyApplication
  {
      internal static class Program
      {
          static Program()
          {
              SFBinaryLoader.Initialize();
          }

          /// <summary>
          /// This is hello entry point of hello service host process.
          /// </summary>
          private static void Main()
          {
  ```

4. <span data-ttu-id="f636a-116">프로젝트를 빌드 및 [패키지](service-fabric-package-apps.md#Package-App)합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-116">Build and [package](service-fabric-package-apps.md#Package-App) your project.</span></span> <span data-ttu-id="f636a-117">toobuild 및 패키지를 만들고, 솔루션 탐색기에서 hello 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 하 hello 선택 **패키지** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-117">toobuild and create a package, right-click hello application project in Solution Explorer and choose hello **Package** command.</span></span>

5. <span data-ttu-id="f636a-118">모든 코드 패키지에 대 한 필요한 toocontainerize, PowerShell 스크립트 실행된 hello [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1)합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-118">For every code package you need toocontainerize, run hello PowerShell script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span></span> <span data-ttu-id="f636a-119">hello 사용법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-119">hello usage is as follows:</span></span>
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  <span data-ttu-id="f636a-120">hello 스크립트 $dockerPackageOutputDirectoryPath에서 Docker 아티팩트 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-120">hello script creates a folder with Docker artifacts at $dockerPackageOutputDirectoryPath.</span></span> <span data-ttu-id="f636a-121">생성 된 hello Dockerfile tooexpose 등 필요에 따라 설치 스크립트를 실행 하는 모든 포트를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-121">Modify hello generated Dockerfile tooexpose any ports, run setup scripts etc. based on your needs.</span></span>

6. <span data-ttu-id="f636a-122">다음 해야 너무[빌드](service-fabric-get-started-containers.md#Build-Containers) 및 [푸시](service-fabric-get-started-containers.md#Push-Containers) Docker 컨테이너 패키지 tooyour 리포지토리에 합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-122">Next you need too[build](service-fabric-get-started-containers.md#Build-Containers) and [push](service-fabric-get-started-containers.md#Push-Containers) your Docker container package tooyour repository.</span></span>

7. <span data-ttu-id="f636a-123">컨테이너 이미지, 리포지토리 정보, 레지스트리 인증 및 포트와 호스트 간 매핑을 tooadd ServiceManifest.xml 및 ApplicationManifest.xml hello를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-123">Modify hello ApplicationManifest.xml and ServiceManifest.xml tooadd your container image, repository information, registry authentication, and port-to-host mapping.</span></span> <span data-ttu-id="f636a-124">Hello 매니페스트를 수정 하기 위한 참조 [Azure Service Fabric 컨테이너 응용 프로그램을 만들려면](service-fabric-get-started-containers.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-124">For modifying hello manifests, see [Create an Azure Service Fabric container application](service-fabric-get-started-containers.md).</span></span> <span data-ttu-id="f636a-125">hello 코드 패키지 정의 hello 서비스 매니페스트 요구 toobe 해당 컨테이너 이미지를 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-125">hello code package definition in hello service manifest needs toobe replaced with corresponding container image.</span></span> <span data-ttu-id="f636a-126">있는지 toochange hello EntryPoint tooa h o s t 형식을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="f636a-126">Make sure toochange hello EntryPoint tooa ContainerHost type.</span></span>

  ```xml
<!-- Code package is your service executable. -->
<CodePackage Name="Code" Version="1.0.0">
  <EntryPoint>
    <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
    <ContainerHost>
      <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
    </ContainerHost>
  </EntryPoint>
  <!-- Pass environment variables tooyour container: -->    
</CodePackage>
  ```

8. <span data-ttu-id="f636a-127">복제기 및 서비스 끝점에 대 한 hello 포트와 호스트 간 매핑을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-127">Add hello port-to-host mapping for your replicator and service endpoint.</span></span> <span data-ttu-id="f636a-128">서비스 패브릭에서 런타임 시 이러한 포트를 모두 할당 된 이후 hello ContainerPort 매핑에 대 한 포트 할당 toozero toouse hello가 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-128">Since both these ports are assigned at runtime by Service Fabric, hello ContainerPort is set toozero toouse hello assigned port for mapping.</span></span>

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. <span data-ttu-id="f636a-129">tootest이 응용이 프로그램 toodeploy 필요한 것 tooa 클러스터 5.7 또는 더 높은 버전을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-129">tootest this application, you need toodeploy it tooa cluster that is running version 5.7 or higher.</span></span> <span data-ttu-id="f636a-130">또한 tooedit 필요 하 고 hello 클러스터 설정을 tooenable이 미리 보기 기능을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-130">In addition, you need tooedit and update hello cluster settings tooenable this preview feature.</span></span> <span data-ttu-id="f636a-131">이 hello 단계에 따라 [문서](service-fabric-cluster-fabric-settings.md) tooadd hello 설정은 다음에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-131">Follow hello steps in this [article](service-fabric-cluster-fabric-settings.md) tooadd hello setting shown next.</span></span>
```
      {
        "name": "Hosting",
        "parameters": [
          {
            "name": "FabricContainerAppsEnabled",
            "value": "true"
          }
        ]
      }
```
10. <span data-ttu-id="f636a-132">다음 [배포](service-fabric-deploy-remove-applications.md) hello 응용 프로그램 패키지 toothis 클러스터를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-132">Next [deploy](service-fabric-deploy-remove-applications.md) hello edited application package toothis cluster.</span></span>

<span data-ttu-id="f636a-133">이제 컨테이너화된 Service Fabric 응용 프로그램이 클러스터를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-133">You should now have a containerized Service Fabric application running your cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f636a-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f636a-134">Next steps</span></span>
* <span data-ttu-id="f636a-135">[Service Fabric의 컨테이너](service-fabric-get-started-containers.md)를 실행하는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-135">Learn more about running [containers on Service Fabric](service-fabric-get-started-containers.md).</span></span>
* <span data-ttu-id="f636a-136">서비스 패브릭 hello에 대 한 자세한 내용은 [응용 프로그램 수명 주기](service-fabric-application-lifecycle.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f636a-136">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
