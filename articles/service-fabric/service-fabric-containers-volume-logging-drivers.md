---
title: "Azure Service Fabric Docker Compose 미리 보기 | Microsoft Docs"
description: "Azure Service Fabric은 Docker Compose 형식을 수락하여 Service Fabric을 통해 기존 컨테이너를 보다 쉽게 조정할 수 있도록 합니다. 이 지원은 현재 미리 보기로 제공되고 있습니다."
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
ms.openlocfilehash: b12ef95add6347621f7d4865fac46568f91a1e12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="0e25e-104">컨테이너에 대한 볼륨 플러그 인 및 로깅 드라이버 지정</span><span class="sxs-lookup"><span data-stu-id="0e25e-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="0e25e-105">Service Fabric은 컨테이너 서비스에 대한 [Docker 볼륨 플러그 인](https://docs.docker.com/engine/extend/plugins_volume/) 및 [Docker 로깅 드라이버](https://docs.docker.com/engine/admin/logging/overview/) 지정을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0e25e-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="0e25e-106">플러그 인은 다음 매니페스트에 표시된 대로 응용 프로그램 매니페스트에서 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e25e-106">The plugins are specified in the application manifest as shown in the following manifest:</span></span>


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

<span data-ttu-id="0e25e-107">앞의 예제에서 `Volume`에 대한 `Source` 태그는 원본 폴더를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0e25e-107">In the preceding example, the `Source` tag for the `Volume` refers to the source folder.</span></span> <span data-ttu-id="0e25e-108">원본 폴더는 컨테이너 또는 영구 원격 저장소를 호스트하는 VM의 폴더일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e25e-108">The source folder could be a folder in the VM that hosts the containers or a persistent remote store.</span></span> <span data-ttu-id="0e25e-109">`Destination` 태그는 실행 중인 컨테이너에서 `Source`가 매핑되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="0e25e-109">The `Destination` tag is the location that the `Source` is mapped to within the running container.</span></span> 

<span data-ttu-id="0e25e-110">볼륨 플러그 인을 지정할 때 Service Fabric은 지정된 매개 변수를 사용하여 볼륨을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e25e-110">When specifying a volume plugin, Service Fabric automatically creates the volume using the parameters specified.</span></span> <span data-ttu-id="0e25e-111">`Source` 태그는 볼륨의 이름이며 `Driver` 태그는 볼륨 드라이버 플러그 인을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e25e-111">The `Source` tag is the name of the volume, and the `Driver` tag specifies the volume driver plugin.</span></span> <span data-ttu-id="0e25e-112">다음 코드 조각에 나와 있는 대로 `DriverOption` 태그를 사용하여 옵션을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e25e-112">Options can be specified using the `DriverOption` tag as shown in the following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="0e25e-113">Docker 로그 드라이버가 지정된 경우 클러스터의 로그를 처리할 에이전트(또는 컨테이너)를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e25e-113">If a Docker log driver is specified, it is necessary to deploy agents (or containers) to handle the logs in the cluster.</span></span>  <span data-ttu-id="0e25e-114">`DriverOption` 태그를 사용하여 로그 드라이버 옵션을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e25e-114">The `DriverOption` tag can be used to specify log driver options as well.</span></span>

<span data-ttu-id="0e25e-115">Service Fabric 클러스터에 컨테이너를 배포하려면 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e25e-115">Refer to the following articles to deploy containers to a Service Fabric cluster:</span></span>


[<span data-ttu-id="0e25e-116">Service Fabric에 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="0e25e-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

