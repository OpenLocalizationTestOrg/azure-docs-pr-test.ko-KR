---
title: "서비스 패브릭 서비스 끝점 aaaSpecifying | Microsoft Docs"
description: "방법을 비롯 하 여 서비스의 toodescribe 끝점 리소스 매니페스트 어떻게 tooset HTTPS 끝점을"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: da36cbdb-6531-4dae-88e8-a311ab71520d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: subramar
ms.openlocfilehash: a4ebee353ce5cf86583673674246094f03f368be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="5b432-103">서비스 매니페스트에서 리소스 지정</span><span class="sxs-lookup"><span data-stu-id="5b432-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="5b432-104">개요</span><span class="sxs-lookup"><span data-stu-id="5b432-104">Overview</span></span>
<span data-ttu-id="5b432-105">hello 서비스 매니페스트 hello 컴파일된 코드를 변경 하지 않고 선언/변경할 hello 서비스 toobe에서 사용 되는 리소스를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-105">hello service manifest allows resources that are used by hello service toobe declared/changed without changing hello compiled code.</span></span> <span data-ttu-id="5b432-106">Azure 서비스 패브릭 hello 서비스에 대 한 끝점 리소스의 구성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-106">Azure Service Fabric supports configuration of endpoint resources for hello service.</span></span> <span data-ttu-id="5b432-107">hello toohello 리소스에 액세스 hello 서비스 매니페스트에 지정 된 hello 응용 프로그램 매니페스트에서 SecurityGroup hello를 통해 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-107">hello access toohello resources that are specified in hello service manifest can be controlled via hello SecurityGroup in hello application manifest.</span></span> <span data-ttu-id="5b432-108">리소스의 hello 선언 이러한 리소스 toobe를 hello 서비스 toointroduce 새로운 구성 메커니즘이 필요 하지 않은 즉 배포 시 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-108">hello declaration of resources allows these resources toobe changed at deployment time, meaning hello service doesn't need toointroduce a new configuration mechanism.</span></span> <span data-ttu-id="5b432-109">hello hello ServiceManifest.xml 파일에 대 한 스키마 정의 hello 서비스 패브릭 SDK와 함께 설치 되 고 너무 도구*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*합니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-109">hello schema definition for hello ServiceManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="5b432-110">끝점</span><span class="sxs-lookup"><span data-stu-id="5b432-110">Endpoints</span></span>
<span data-ttu-id="5b432-111">끝점에서에서 정의 된 hello 서비스 매니페스트, 포트를 명시적으로 지정 되지 않은 경우 포트 서비스 패브릭에 hello 예약 응용 프로그램 포트 범위에서 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-111">When an endpoint resource is defined in hello service manifest, Service Fabric assigns ports from hello reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="5b432-112">예를 들어 hello 끝점 확인 *ServiceEndpoint1* 이 단락 뒤에 제공 된 hello 매니페스트 조각에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-112">For example, look at hello endpoint *ServiceEndpoint1* specified in hello manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="5b432-113">또한 서비스에서 리소스의 특정 포트를 요청할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="5b432-114">서비스 복제본 다른 클러스터 노드에서 실행 중인 복제본 실행 되는 서비스의 동일한 노드 공유 hello 포트 hello 하는 동안 다른 포트 번호를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on hello same node share hello port.</span></span> <span data-ttu-id="5b432-115">서비스 복제본 hello를 유도할 수 있습니다 이러한 포트 필요에 따라 복제 및 클라이언트 요청을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-115">hello service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="5b432-116">너무 참조[신뢰할 수 있는 상태 저장 서비스 구성](service-fabric-reliable-services-configuration.md) tooread hello 구성 패키지 설정 파일 (settings.xml)에서 끝점 참조에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-116">Refer too[Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) tooread more about referencing endpoints from hello config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="5b432-117">예: 서비스에 대한 HTTP 끝점 지정</span><span class="sxs-lookup"><span data-stu-id="5b432-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="5b432-118">hello 다음 서비스 매니페스트 TCP 끝점 리소스가 두 개에서 및 정의 두 HTTP 끝점 리소스 hello &lt;리소스&gt; 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-118">hello following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in hello &lt;Resources&gt; element.</span></span>

<span data-ttu-id="5b432-119">HTTP 끝점은 서비스 패브릭에 의해 자동으로 ACL 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         This name must match hello string used in hello RegisterServiceType call in Program.cs. -->
    <StatefulServiceType ServiceTypeName="Stateful1Type" HasPersistedState="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <ExeHost>
        <Program>Stateful1.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by hello replicator for replicating hello state of your service.
           This endpoint is configured through hello ReplicatorSettings config section in hello Settings.xml
           file under hello ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="5b432-120">예: 서비스에 대한 HTTPS 끝점 지정</span><span class="sxs-lookup"><span data-stu-id="5b432-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="5b432-121">HTTPS 프로토콜 hello 서버 인증을 제공 하 고 클라이언트-서버 통신을 암호화 하는 것에 대 한 때도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-121">hello HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="5b432-122">서비스 패브릭 서비스에서 HTTPS tooenable hello에 hello 프로토콜을 지정 *리소스 끝점-> 끝점->* hello 서비스 매니페스트를 앞에서 보았듯이 hello 끝점에 대 한 섹션 *ServiceEndpoint3* .</span><span class="sxs-lookup"><span data-stu-id="5b432-122">tooenable HTTPS on your Service Fabric service, specify hello protocol in hello *Resources -> Endpoints -> Endpoint* section of hello service manifest, as shown earlier for hello endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="5b432-123">서비스의 프로토콜은 응용 프로그램 업그레이드 중에 변경될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="5b432-124">업그레이드 중에 변경되는 경우 불안정한 변경이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="5b432-125">다음은 예제 ApplicationManifest tooset HTTPS 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-125">Here is an example ApplicationManifest that you need tooset for HTTPS.</span></span> <span data-ttu-id="5b432-126">인증서에 대 한 hello 지문을 제공 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-126">hello thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="5b432-127">hello EndpointRef hello HTTPS 프로토콜 사용 하도록 설정한 ServiceManifest의 참조 tooEndpointResource입니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-127">hello EndpointRef is a reference tooEndpointResource in ServiceManifest, for which you set hello HTTPS protocol.</span></span> <span data-ttu-id="5b432-128">둘 이상의 Endpointcertificate를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-128">You can add more than one EndpointCertificate.</span></span>  

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="Application1Type"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
    <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
    <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Stateful1">
      <StatefulService ServiceTypeName="Stateful1Type" TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]" MinReplicaSetSize="[Stateful1_ ]">
        <UniformInt64Partition PartitionCount="[Stateful1_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
      </StatefulService>
    </Service>
  </DefaultServices>
  <Certificates>
    <EndpointCertificate Name="TestCert1" X509FindValue="FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0" X509StoreName="MY" />  
  </Certificates>
</ApplicationManifest>
```

## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="5b432-129">ServiceManifest.xml에서 끝점 재정의</span><span class="sxs-lookup"><span data-stu-id="5b432-129">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="5b432-130">Hello ApplicationManifest에서에서 형제 tooConfigOverrides 섹션 될 ResourceOverrides 섹션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-130">In hello ApplicationManifest add a ResourceOverrides section which will be a sibling tooConfigOverrides section.</span></span> <span data-ttu-id="5b432-131">이 섹션의 hello 서비스 매니페스트에 지정 된 hello 리소스 섹션에 끝점 섹션 hello에 대 한 hello 재정의 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-131">In this section you can specify hello override for hello Endpoints section in hello resources section specified in hello Service manifest.</span></span>

<span data-ttu-id="5b432-132">다음과 같이 ApplicationManifest hello 순서 toooverride ApplicationParameters 변경을 사용 하 여 ServiceManifest의 끝점에서에서:</span><span class="sxs-lookup"><span data-stu-id="5b432-132">In order toooverride EndPoint in ServiceManifest using ApplicationParameters change hello ApplicationManifest as following:</span></span>

<span data-ttu-id="5b432-133">Hello ServiceManifestImport 섹션에서에서 "ResourceOverrides" 새 섹션 추가</span><span class="sxs-lookup"><span data-stu-id="5b432-133">In hello ServiceManifestImport section add a new section "ResourceOverrides"</span></span>

```xml
<ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <ResourceOverrides>
      <Endpoints>
        <Endpoint Name="ServiceEndpoint" Port="[Port]" Protocol="[Protocol]" Type="[Type]" />
        <Endpoint Name="ServiceEndpoint1" Port="[Port1]" Protocol="[Protocol1] "/>
      </Endpoints>
    </ResourceOverrides>
        <Policies>
           <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint"/>
        </Policies>
  </ServiceManifestImport>
```

<span data-ttu-id="5b432-134">hello 아래 매개 변수 추가:</span><span class="sxs-lookup"><span data-stu-id="5b432-134">In hello Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="5b432-135">Hello 응용 프로그램을 지금 배포 하는 동안으로 전달할 수 있습니다 이러한 값에 ApplicationParameters 예:</span><span class="sxs-lookup"><span data-stu-id="5b432-135">While deploying hello application now you can pass in these values as ApplicationParameters for example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="5b432-136">참고: hello ApplicationParameters 비어에 대 한 hello 값을 제공 하는 경우 돌아간 toohello 기본 EndPointName에 해당 하는 hello에 대 한 hello ServiceManifest에에서 제공 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-136">Note: If hello values provide for hello ApplicationParameters is empty we go back toohello default value provided in hello ServiceManifest for hello corresponding EndPointName.</span></span>

<span data-ttu-id="5b432-137">예:</span><span class="sxs-lookup"><span data-stu-id="5b432-137">For example:</span></span>

<span data-ttu-id="5b432-138">Hello ServiceManifest 지정한 경우</span><span class="sxs-lookup"><span data-stu-id="5b432-138">If in hello ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="5b432-139">포트 1 hello 및 응용 프로그램 매개 변수에 대 한 Protocol1 값이 null 이거나 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-139">And hello Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="5b432-140">hello 포트 ServiceFabric로 계속 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-140">hello port is still decided by ServiceFabric.</span></span> <span data-ttu-id="5b432-141">되며 hello 프로토콜은 tcp 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-141">And hello Protocol will tcp.</span></span>

<span data-ttu-id="5b432-142">잘못된 값을 지정한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-142">Suppose you specify a wrong value.</span></span> <span data-ttu-id="5b432-143">Port의 경우처럼 int 대신 문자열 값 "Foo"를 지정했습니다.  새 ServiceFabricApplication 오류와 함께 명령이 실패 합니다: 'ResourceOverrides' 섹션에서 '포트 1' name 'ServiceEndpoint1' 특성을 가진 hello 재정의 매개 변수가 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-143">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : hello override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="5b432-144">지정 된 값이 hello 'Foo' 이며 'int'가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b432-144">hello value specified is 'Foo' and required is 'int'.</span></span>
