---
title: "aaaManage 서비스 패브릭에서 여러 환경 | Microsoft Docs"
description: "서비스 패브릭 응용 프로그램에서 컴퓨터의 한 컴퓨터 toothousands 클러스터에서 실행할 수 있습니다. 일부 경우 tooconfigure 다르게 이러한 다양 한 환경에 대 한 응용 프로그램 원할 수 있습니다. 이 문서에서는 어떻게 환경당 toodefine 다른 응용 프로그램 매개 변수입니다."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="ea817-105">여러 환경에 대한 응용 프로그램 매개 변수 관리</span><span class="sxs-lookup"><span data-stu-id="ea817-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="ea817-106">하나의 toomany 수천 대의 컴퓨터에서에서 임의의 위치를 사용 하 여 Azure 서비스 패브릭 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-106">You can create Azure Service Fabric clusters by using anywhere from one toomany thousands of machines.</span></span> <span data-ttu-id="ea817-107">응용 프로그램 이진 파일은이 다양 한 환경에서 수정 없이 실행할 수, 하는 동안 경우가 종종 있습니다 tooconfigure hello 응용 프로그램 다르게 hello에 배포 하는 컴퓨터 수에 따라.</span><span class="sxs-lookup"><span data-stu-id="ea817-107">While application binaries can run without modification across this wide spectrum of environments, you often want tooconfigure hello application differently, depending on hello number of machines you're deploying to.</span></span>

<span data-ttu-id="ea817-108">간단한 예로 상태 비저장 서비스에 대해 `InstanceCount` 를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="ea817-109">Azure에서 응용 프로그램을 실행 하는 경우 일반적으로 원하는 tooset "-1"이 매개 변수 toohello 특수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-109">When you are running applications in Azure, you generally want tooset this parameter toohello special value of "-1".</span></span> <span data-ttu-id="ea817-110">이 구성 서비스 hello 클러스터 (또는 배치 제약 조건을 설정 하는 경우 hello 노드 유형에 서 모든 노드)의 모든 노드에서 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-110">This configuration ensures that your service is running on every node in hello cluster (or every node in hello node type if you have set a placement constraint).</span></span> <span data-ttu-id="ea817-111">그러나이 구성은 적합 하지 않은 단일 컴퓨터 클러스터에 대 한 동일한 hello에서 수신 하는 여러 프로세스를 가질 수 없으므로 단일 컴퓨터에서 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on hello same endpoint on a single machine.</span></span> <span data-ttu-id="ea817-112">일반적으로 설정 대신 `InstanceCount` 너무 "1".</span><span class="sxs-lookup"><span data-stu-id="ea817-112">Instead, you typically set `InstanceCount` too"1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="ea817-113">환경 특정 매개 변수 지정</span><span class="sxs-lookup"><span data-stu-id="ea817-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="ea817-114">hello 솔루션 toothis 구성 문제는 매개 변수가 있는 기본 서비스 및 해당 매개 변수 값에 대 한 지정된 된 환경에서 작성 하는 응용 프로그램 매개 변수 파일의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-114">hello solution toothis configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="ea817-115">기본 서비스 및 응용 프로그램 매개 변수 서비스 매니페스트 및 hello 응용 프로그램에서 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-115">Default services and application parameters are configured in hello application and service manifests.</span></span> <span data-ttu-id="ea817-116">hello hello ServiceManifest.xml 및 ApplicationManifest.xml 파일에 대 한 스키마 정의 hello 서비스 패브릭 SDK와 함께 설치 및 도구 너무*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="ea817-116">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml files is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="ea817-117">기본 서비스</span><span class="sxs-lookup"><span data-stu-id="ea817-117">Default services</span></span>
<span data-ttu-id="ea817-118">서비스 패브릭 응용 프로그램은 서비스 인스턴스의 컬렉션으로 이루어 집니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="ea817-119">Toocreate 빈 응용 프로그램에 대 한 불가능 하 고 다음 모든 서비스 인스턴스를 동적으로 만들, 대부분의 응용 프로그램에는 hello 응용 프로그램 인스턴스화될 때 항상 생성 해야 하는 핵심 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-119">While it is possible for you toocreate an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when hello application is instantiated.</span></span> <span data-ttu-id="ea817-120">이들은 참조 tooas "기본 서비스"입니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-120">These are referred tooas "default services".</span></span> <span data-ttu-id="ea817-121">Hello 응용 프로그램 매니페스트는 대괄호에 포함 된-환경 구성에 대 한 자리 표시자에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-121">They are specified in hello application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

<span data-ttu-id="ea817-122">각 명명 된 매개 변수는 hello hello 응용 프로그램 매니페스트의 hello 매개 변수 요소 내에서 정의 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-122">Each of hello named parameters must be defined within hello Parameters element of hello application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="ea817-123">hello DefaultValue 특성 hello 값 toobe hello는 보다 구체적인 매개 변수가 없는 경우 지정된 된 환경에 대 한 사용을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-123">hello DefaultValue attribute specifies hello value toobe used in hello absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="ea817-124">모든 서비스 인스턴스 매개 변수가 환경 단위 구성에 적합하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="ea817-125">위의 hello 예제 LowKey hello 및 hello 서비스의 파티션 구성표에 대 한 HighKey 값 hello 파티션 범위는 hello 환경이 아닌 hello 데이터 도메인의 함수 때문에 명시적으로 hello 서비스의 모든 인스턴스에 대해 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-125">In hello example above, hello LowKey and HighKey values for hello service's partitioning scheme are explicitly defined for all instances of hello service since hello partition range is a function of hello data domain, not hello environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="ea817-126">환경 단위 서비스 구성 설정</span><span class="sxs-lookup"><span data-stu-id="ea817-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="ea817-127">hello [서비스 패브릭 응용 프로그램 모델](service-fabric-application-model.md) 활성화 서비스는 런타임에 읽을 수 있는 사용자 지정 키-값 쌍을 포함 하는 tooinclude 구성 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-127">hello [Service Fabric application model](service-fabric-application-model.md) enables services tooinclude configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="ea817-128">이러한 설정의 hello 값 수를 지정 하 여도 환경으로 구분 하는 수는 `ConfigOverride` hello 응용 프로그램 매니페스트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-128">hello values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in hello application manifest.</span></span>

<span data-ttu-id="ea817-129">Hello에 대 한 hello Config\Settings.xml 파일의 설정에 따라 hello 있다고 가정 하 고 `Stateful1` 서비스:</span><span class="sxs-lookup"><span data-stu-id="ea817-129">Suppose that you have hello following setting in hello Config\Settings.xml file for hello `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="ea817-130">toooverride 특정 응용 프로그램/환경 쌍에 대 한이 값 만들기는 `ConfigOverride` hello 응용 프로그램 매니페스트에서 hello 서비스 매니페스트를 가져올 때.</span><span class="sxs-lookup"><span data-stu-id="ea817-130">toooverride this value for a specific application/environment pair, create a `ConfigOverride` when you import hello service manifest in hello application manifest.</span></span>

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
<span data-ttu-id="ea817-131">이 매개 변수는 위에 표시된 대로 환경에서 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="ea817-132">Hello 응용 프로그램 매니페스트의 hello 매개 변수 섹션에서 선언 하 고 hello 응용 프로그램 매개 변수 파일에서 환경 관련 값을 지정 하 여이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-132">You can do this by declaring it in hello parameters section of hello application manifest and specifying environment-specific values in hello application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="ea817-133">Hello 경우 서비스 구성 설정의 세 위치는 hello 키 값을 설정할 수 있습니다: hello 서비스 구성 패키지, 응용 프로그램 매니페스트 hello 및 hello 응용 프로그램 매개 변수 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-133">In hello case of service configuration settings, there are three places where hello value of a key can be set: hello service configuration package, hello application manifest, and hello application parameter file.</span></span> <span data-ttu-id="ea817-134">서비스 패브릭은 항상 hello 응용 프로그램 매개 변수 파일에서 먼저 지정 하는 경우, 다음 응용 프로그램 매니페스트를 hello 선택한 구성 패키지를 마지막으로 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-134">Service Fabric will always choose from hello application parameter file first (if specified), then hello application manifest, and finally hello configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="ea817-135">환경 변수 설정 및 사용</span><span class="sxs-lookup"><span data-stu-id="ea817-135">Setting and using environment variables</span></span> 
<span data-ttu-id="ea817-136">지정 하 고 및 hello ServiceManifest.xml 파일에서 환경 변수를 설정 하 고, 인스턴스별로에 hello ApplicationManifest.xml 파일에서이 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-136">You can specify and set environment variables in hello ServiceManifest.xml file and then override these in hello ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="ea817-137">아래 hello 예제에서는 두 개의 환경 변수를 보여 줍니다. 설정 값을 가진 및 다른 hello 재정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-137">hello example below shows two environment variables, one with a value set and hello other is overridden.</span></span> <span data-ttu-id="ea817-138">Hello에 tooset 환경 변수 값 방식으로 구성 재정의에 사용 된 해당 이러한 동일한 응용 프로그램 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-138">You can use application parameters tooset environment variables values in hello same way that these were used for config overrides.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```
<span data-ttu-id="ea817-139">hello ApplicationManifest.xml, hello로 hello ServiceManifest의에서 참조 hello 코드 패키지에서에서 toooverride hello 환경 변수 `EnvironmentOverrides` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-139">toooverride hello environment variables in hello ApplicationManifest.xml, reference hello code package in hello ServiceManifest with hello `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="ea817-140">명명 된 인스턴스를 서비스 하는 hello 만들어지면 hello 환경 변수 코드에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-140">Once hello named service instance is created you can access hello environment variables from code.</span></span> <span data-ttu-id="ea817-141">예를 들어 C#에서 할 수 있는 hello 다음</span><span class="sxs-lookup"><span data-stu-id="ea817-141">e.g. In C# you can do hello following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="ea817-142">Service Fabric 환경 변수</span><span class="sxs-lookup"><span data-stu-id="ea817-142">Service Fabric environment variables</span></span>
<span data-ttu-id="ea817-143">Service Fabric에는 각 서비스 인스턴스에 대해 설정된 기본 제공 환경 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="ea817-144">hello 전체 목록은 환경 변수는 아래 hello에 굵게 표시 된 hello 서비스에 사용 됩니다 하는 경우 hello 되 고 다른 서비스 패브릭 런타임에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-144">hello full list of environment variables is below, where hello ones in bold are hello ones that you will use in your service, hello other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="ea817-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="ea817-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="ea817-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="ea817-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="ea817-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="ea817-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="ea817-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="ea817-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="ea817-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="ea817-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="ea817-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="ea817-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="ea817-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span><span class="sxs-lookup"><span data-stu-id="ea817-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="ea817-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="ea817-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="ea817-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="ea817-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="ea817-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="ea817-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="ea817-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="ea817-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="ea817-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="ea817-156">Fabric_NodeId</span></span>
* <span data-ttu-id="ea817-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="ea817-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="ea817-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="ea817-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="ea817-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="ea817-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="ea817-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="ea817-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="ea817-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="ea817-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="ea817-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="ea817-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="ea817-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="ea817-163">FabricPackageFileName</span></span>

<span data-ttu-id="ea817-164">hello 코드 belows toolist 서비스 패브릭 환경 변수를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-164">hello code belows shows how toolist hello Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="ea817-165">hello 다음은 예제 호출 응용 프로그램 종류에 대 한 환경 변수의 `GuestExe.Application` 서비스 유형으로 호출 `FrontEndService` 로컬 개발 컴퓨터에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-165">hello following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="ea817-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span><span class="sxs-lookup"><span data-stu-id="ea817-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="ea817-167">**Fabric_CodePackageName = Code**</span><span class="sxs-lookup"><span data-stu-id="ea817-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="ea817-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="ea817-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="ea817-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="ea817-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="ea817-170">**Fabric_NodeName = _Node_2**</span><span class="sxs-lookup"><span data-stu-id="ea817-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="ea817-171">응용 프로그램 매개 변수 파일</span><span class="sxs-lookup"><span data-stu-id="ea817-171">Application parameter files</span></span>
<span data-ttu-id="ea817-172">hello 서비스 패브릭 응용 프로그램 프로젝트는 하나 이상의 응용 프로그램 매개 변수 파일을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-172">hello Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="ea817-173">각각의 hello hello 응용 프로그램 매니페스트에서 정의 된 hello 매개 변수에 대 한 특정 값을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-173">Each of them defines hello specific values for hello parameters that are defined in hello application manifest:</span></span>

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
<span data-ttu-id="ea817-174">기본적으로 새 응용 프로그램은 Local.1Node.xml, Local.5Node.xml 및 Cloud.xml라는 세 응용 프로그램 매개 변수 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![솔루션 탐색기에서 응용 프로그램 매개 변수 파일][app-parameters-solution-explorer]

<span data-ttu-id="ea817-176">toocreate 매개 변수 파일 단순히 복사 하 고 기존 붙여 하 고 새 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-176">toocreate a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="ea817-177">배포하는 동안 환경 단위 매개 변수 식별</span><span class="sxs-lookup"><span data-stu-id="ea817-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="ea817-178">배포 시 응용 프로그램과 함께 toochoose hello 적절 한 매개 변수 파일 tooapply가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-178">At deployment time, you need toochoose hello appropriate parameter file tooapply with your application.</span></span> <span data-ttu-id="ea817-179">Visual Studio에서 hello 게시 대화 상자를 통해 또는 PowerShell을 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-179">You can do this through hello Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="ea817-180">Visual Studio에서 배포</span><span class="sxs-lookup"><span data-stu-id="ea817-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="ea817-181">Visual Studio에서 응용 프로그램을 게시할 때 사용할 수 있는 매개 변수 파일의 hello 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-181">You can choose from hello list of available parameter files when you publish your application in Visual Studio.</span></span>

![Hello 게시 대화 상자에서 매개 변수 파일 선택][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="ea817-183">PowerShell에서 배포</span><span class="sxs-lookup"><span data-stu-id="ea817-183">Deploy from PowerShell</span></span>
<span data-ttu-id="ea817-184">hello `Deploy-FabricApplication.ps1` hello 응용 프로그램 프로젝트 템플릿을에 포함 된 PowerShell 스크립트를 매개 변수로 게시 프로필을 받아들이고 hello PublishProfile 참조 toohello 응용 프로그램 매개 변수 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-184">hello `Deploy-FabricApplication.ps1` PowerShell script included in hello application project template accepts a publish profile as a parameter and hello PublishProfile contains a reference toohello application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="ea817-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ea817-185">Next steps</span></span>
<span data-ttu-id="ea817-186">이 항목에서 설명 하는 hello 핵심 개념 중 일부에 대해 자세히 toolearn 참조 hello [서비스 패브릭 기술 개요](service-fabric-technical-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ea817-186">toolearn more about some of hello core concepts that are discussed in this topic, see hello [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="ea817-187">Visual Studio에서 사용할 수 있는 다른 앱 관리 기능에 대한 정보는 [Visual Studio에서 서비스 패브릭 응용 프로그램 관리](service-fabric-manage-application-in-visual-studio.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ea817-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
