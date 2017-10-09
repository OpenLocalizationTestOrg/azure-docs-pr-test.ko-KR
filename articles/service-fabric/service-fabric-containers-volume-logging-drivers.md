---
title: "서비스 패브릭 Docker 작성 미리 보기 aaaAzure | Microsoft Docs"
description: "Azure 서비스 패브릭 형식 toomake Docker Compose를 허용 하기 서비스 패브릭을 사용 하 여 보다 쉽게 tooorchestrate exsiting 컨테이너입니다. 이 지원은 현재 미리 보기로 제공되고 있습니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 824044fd698f0ed94c4212722bc82187905315dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="e549a-104">컨테이너에 대한 볼륨 플러그 인 및 로깅 드라이버 지정</span><span class="sxs-lookup"><span data-stu-id="e549a-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="e549a-105">Service Fabric은 컨테이너 서비스에 대한 [Docker 볼륨 플러그 인](https://docs.docker.com/engine/extend/plugins_volume/) 및 [Docker 로깅 드라이버](https://docs.docker.com/engine/admin/logging/overview/) 지정을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e549a-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="e549a-106">hello 플러그 인 매니페스트를 수행 하는 hello와 같이 hello 응용 프로그램 매니페스트에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e549a-106">hello plugins are specified in hello application manifest as shown in hello following manifest:</span></span>


```xml
?xml version="1.0" encoding="UTF-8"?>
<ApplicationManifest ApplicationTypeName="WinNodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <Description>Calculator Application</Description>
    <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
      <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
    </Parameters>
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeServicePackage" ServiceManifestVersion="1.0"/>
     <Policies>
       <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv"> 
        <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
        <RepositoryCredentials PasswordEncrypted="false" Password="****" AccountName="test"/>
        <LogConfig Driver="etwlogs" >
          <DriverOption Name="test" Value="vale"/>
        </LogConfig>
        <Volume Source="c:\workspace" Destination="c:\testmountlocation1" IsReadOnly="false"></Volume>
        <Volume Source="d:\myfolder" Destination="c:\testmountlocation2" IsReadOnly="true"> </Volume>
        <Volume Source="myexternalvolume" Destination="c:\testmountlocation3" Driver="sf" IsReadOnly="true"></Volume>
       </ContainerHostPolicies>
   </Policies>
    </ServiceManifestImport>
    <ServiceTemplates>
        <StatelessService ServiceTypeName="StatelessNodeService" InstanceCount="5">
            <SingletonPartition></SingletonPartition>
        </StatelessService>
    </ServiceTemplates>
</ApplicationManifest>
```

<span data-ttu-id="e549a-107">앞 예제는 hello에서 hello `Source` hello에 대 한 태그 `Volume` toohello 소스 폴더를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="e549a-107">In hello preceding example, hello `Source` tag for hello `Volume` refers toohello source folder.</span></span> <span data-ttu-id="e549a-108">hello 소스 폴더는 hello hello 컨테이너 또는 영구 원격 저장소를 호스팅하는 VM에에서 있는 폴더 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e549a-108">hello source folder could be a folder in hello VM that hosts hello containers or a persistent remote store.</span></span> <span data-ttu-id="e549a-109">hello `Destination` 태그는 hello hello 위치 `Source` 매핑된 toowithin hello 컨테이너 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e549a-109">hello `Destination` tag is hello location that hello `Source` is mapped toowithin hello running container.</span></span> 

<span data-ttu-id="e549a-110">볼륨 플러그 인을 지정할 때 서비스 패브릭 지정 된 hello 매개 변수를 사용 하 여 hello 볼륨을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e549a-110">When specifying a volume plugin, Service Fabric automatically creates hello volume using hello parameters specified.</span></span> <span data-ttu-id="e549a-111">hello `Source` 태그는 hello 볼륨 및 hello hello 이름 `Driver` 태그 hello 볼륨 드라이버 플러그 인을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e549a-111">hello `Source` tag is hello name of hello volume, and hello `Driver` tag specifies hello volume driver plugin.</span></span> <span data-ttu-id="e549a-112">Hello를 사용 하 여 옵션을 지정할 수 있습니다 `DriverOption` hello 다음 코드 조각에에서 나와 있는 것 처럼 태그:</span><span class="sxs-lookup"><span data-stu-id="e549a-112">Options can be specified using hello `DriverOption` tag as shown in hello following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="e549a-113">Docker 로그 드라이버 지정 된 경우 필요한 toodeploy 에이전트 (또는 컨테이너) toohandle hello hello 클러스터 로그인입니다.</span><span class="sxs-lookup"><span data-stu-id="e549a-113">If a Docker log driver is specified, it is necessary toodeploy agents (or containers) toohandle hello logs in hello cluster.</span></span>  <span data-ttu-id="e549a-114">hello `DriverOption` 태그 사용된 toospecify 로그 드라이버 옵션도 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e549a-114">hello `DriverOption` tag can be used toospecify log driver options as well.</span></span>

<span data-ttu-id="e549a-115">Toohello 문서 toodeploy 컨테이너 tooa 서비스 패브릭 클러스터를 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e549a-115">Refer toohello following articles toodeploy containers tooa Service Fabric cluster:</span></span>


[<span data-ttu-id="e549a-116">Service Fabric에 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="e549a-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

