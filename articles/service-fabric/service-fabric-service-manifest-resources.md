---
title: "Service Fabric 서비스 끝점 지정 | Microsoft Docs"
description: "HTTPS 끝점을 설정하는 방법을 포함하여 서비스 매니페스트에서 끝점 리소스를 설명하는 방법"
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
ms.openlocfilehash: 08141edfbc8be9bf7bf303419e1e482d5f884860
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="6851f-103">서비스 매니페스트에서 리소스 지정</span><span class="sxs-lookup"><span data-stu-id="6851f-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="6851f-104">개요</span><span class="sxs-lookup"><span data-stu-id="6851f-104">Overview</span></span>
<span data-ttu-id="6851f-105">서비스 매니페스트를 사용하면 컴파일된 코드를 변경하지 않고도 서비스에서 사용하는 리소스를 선언/변경할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-105">The service manifest allows resources that are used by the service to be declared/changed without changing the compiled code.</span></span> <span data-ttu-id="6851f-106">Azure 서비스 패브릭은 서비스에 대한 끝점 리소스 구성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-106">Azure Service Fabric supports configuration of endpoint resources for the service.</span></span> <span data-ttu-id="6851f-107">서비스 매니페스트에 지정된 리소스에 대한 액세스는 응용 프로그램 매니페스트의 SecurityGroup을 통해 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-107">The access to the resources that are specified in the service manifest can be controlled via the SecurityGroup in the application manifest.</span></span> <span data-ttu-id="6851f-108">리소스를 선언하면 배포 시에 이러한 리소스를 변경할 수 있으며 즉, 서비스에 새로운 구성 메커니즘을 도입하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-108">The declaration of resources allows these resources to be changed at deployment time, meaning the service doesn't need to introduce a new configuration mechanism.</span></span> <span data-ttu-id="6851f-109">ServiceManifest.xml 파일에 대한 스키마 정의는 Service Fabric SDK 및 도구와 함께 *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-109">The schema definition for the ServiceManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="6851f-110">끝점</span><span class="sxs-lookup"><span data-stu-id="6851f-110">Endpoints</span></span>
<span data-ttu-id="6851f-111">서비스 매니페스트에 끝점 리소스가 정의되면 서비스 패브릭에서는 포트가 명시적으로 지정되지 않을 경우 예약된 응용 프로그램 포트 범위에 포함되는 포트를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-111">When an endpoint resource is defined in the service manifest, Service Fabric assigns ports from the reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="6851f-112">예를 들어 이 단락 다음에 제공된 매니페스트 코드 조각에 지정된 끝점 *ServiceEndpoint1* 을 보세요.</span><span class="sxs-lookup"><span data-stu-id="6851f-112">For example, look at the endpoint *ServiceEndpoint1* specified in the manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="6851f-113">또한 서비스에서 리소스의 특정 포트를 요청할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="6851f-114">다른 클러스터 노드에서 실행되는 서비스 복제본을 다른 포트 번호에 할당할 수 있으며, 같은 노드에서 실행되는 서비스의 복제본은 포트를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on the same node share the port.</span></span> <span data-ttu-id="6851f-115">그러면 서비스 복제본은 복제 및 클라이언트 요청의 수신 대기를 위해 필요한 경우 이러한 포트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-115">The service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="6851f-116">구성 패키지 설정 파일(settings.xml)의 끝점 참조에 대한 자세한 내용은 [상태 저장 Reliable Services 구성](service-fabric-reliable-services-configuration.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6851f-116">Refer to [Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) to read more about referencing endpoints from the config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="6851f-117">예: 서비스에 대한 HTTP 끝점 지정</span><span class="sxs-lookup"><span data-stu-id="6851f-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="6851f-118">다음 서비스 매니페스트는 &lt;Resources&gt; 요소에서 한 개의 TCP 끝점 리소스와 두 개의 HTTP 끝점 리소스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-118">The following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in the &lt;Resources&gt; element.</span></span>

<span data-ttu-id="6851f-119">HTTP 끝점은 서비스 패브릭에 의해 자동으로 ACL 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         This name must match the string used in the RegisterServiceType call in Program.cs. -->
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

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by the replicator for replicating the state of your service.
           This endpoint is configured through the ReplicatorSettings config section in the Settings.xml
           file under the ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="6851f-120">예: 서비스에 대한 HTTPS 끝점 지정</span><span class="sxs-lookup"><span data-stu-id="6851f-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="6851f-121">HTTPS 프로토콜은 서버 인증을 제공하며, 클라이언트-서버 통신을 암호화하는 데에도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-121">The HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="6851f-122">Service Fabric 서비스에서 HTTPS를 사용할 수 있도록 설정하려면 위의 *ServiceEndpoint3* 끝점과 같이 서비스 매니페스트의 *리소스 -> 끝점 -> 끝점* 섹션에서 프로토콜을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-122">To enable HTTPS on your Service Fabric service, specify the protocol in the *Resources -> Endpoints -> Endpoint* section of the service manifest, as shown earlier for the endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="6851f-123">서비스의 프로토콜은 응용 프로그램 업그레이드 중에 변경될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="6851f-124">업그레이드 중에 변경되는 경우 불안정한 변경이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="6851f-125">HTTPS에 대해 설정해야 하는 예제 ApplicationManifest는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-125">Here is an example ApplicationManifest that you need to set for HTTPS.</span></span> <span data-ttu-id="6851f-126">인증서에 대한 지문을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-126">The thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="6851f-127">EndpointRef는 HTTPS 프로토콜을 설정하는 ServiceManifest의 EndpointResource에 대한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-127">The EndpointRef is a reference to EndpointResource in ServiceManifest, for which you set the HTTPS protocol.</span></span> <span data-ttu-id="6851f-128">둘 이상의 Endpointcertificate를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-128">You can add more than one EndpointCertificate.</span></span>  

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
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion
       should match the Name and Version attributes of the ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- The section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
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

## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="6851f-129">ServiceManifest.xml에서 끝점 재정의</span><span class="sxs-lookup"><span data-stu-id="6851f-129">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="6851f-130">ApplicationManifest에서 ConfigOverrides 섹션의 형제로 지정될 ResourceOverrides 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-130">In the ApplicationManifest add a ResourceOverrides section which will be a sibling to ConfigOverrides section.</span></span> <span data-ttu-id="6851f-131">이 섹션에서는 ServiceManiifest에 지정된 resources 섹션의 Endpoints 섹션에 대한 재정의를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-131">In this section you can specify the override for the Endpoints section in the resources section specified in the Service manifest.</span></span>

<span data-ttu-id="6851f-132">ApplicationParameters를 사용하여 ServiceManifest에서 EndPoint를 재정의하려면 ApplicationManifest를 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-132">In order to override EndPoint in ServiceManifest using ApplicationParameters change the ApplicationManifest as following:</span></span>

<span data-ttu-id="6851f-133">ServiceManifestImport 섹션에서 새 섹션 "ResourceOverrides"를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-133">In the ServiceManifestImport section add a new section "ResourceOverrides"</span></span>

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

<span data-ttu-id="6851f-134">Parameters에서 아래 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-134">In the Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="6851f-135">예를 들어 응용 프로그램을 배포하는 동안 다음 값을 ApplicationParameters로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-135">While deploying the application now you can pass in these values as ApplicationParameters for example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="6851f-136">참고: ApplicationParameters에 제공된 값이 비어 있으면 해당 EndPointName에 대한 ServiceManifest에 제공된 기본값으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-136">Note: If the values provide for the ApplicationParameters is empty we go back to the default value provided in the ServiceManifest for the corresponding EndPointName.</span></span>

<span data-ttu-id="6851f-137">예:</span><span class="sxs-lookup"><span data-stu-id="6851f-137">For example:</span></span>

<span data-ttu-id="6851f-138">ServiceManifest에서 다음을 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-138">If in the ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="6851f-139">또한 Applications 매개 변수에 대한 Port1 및 Protocol1 값은 null이거나 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-139">And the Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="6851f-140">포트는 여전히 ServiceFabric에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-140">The port is still decided by ServiceFabric.</span></span> <span data-ttu-id="6851f-141">또한 Protocol은 tcp가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-141">And the Protocol will tcp.</span></span>

<span data-ttu-id="6851f-142">잘못된 값을 지정한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-142">Suppose you specify a wrong value.</span></span> <span data-ttu-id="6851f-143">Port의 경우처럼 int 대신 문자열 값 "Foo"를 지정했습니다.  New-ServiceFabricApplication 명령은 다음 오류와 함께 실패합니다. 'ResourceOverrides' 섹션에서 이름이 'ServiceEndpoint1'이고 특성이 'Port1'인 재정의 매개 변수가 잘못되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-143">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : The override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="6851f-144">지정된 값은 'Foo'이지만 'int'가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6851f-144">The value specified is 'Foo' and required is 'int'.</span></span>
