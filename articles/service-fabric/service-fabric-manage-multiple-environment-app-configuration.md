---
title: "Service Fabric에서 여러 환경 관리 | Microsoft Docs"
description: "한 컴퓨터에서 수천 개의 컴퓨터에 이르는 클러스터에서 서비스 패브릭 응용 프로그램을 실행할 수 있습니다. 어떤 경우에 해당하는 다양한 환경에 대해 다르게 응용 프로그램을 구성하려 합니다. 이 문서에서는 환경 당 다른 응용 프로그램 매개 변수를 정의하는 방법을 설명합니다."
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
ms.openlocfilehash: 9317b3f0b7984e795c4205360ed58e2c4f3fbcb1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="6236d-105">여러 환경에 대한 응용 프로그램 매개 변수 관리</span><span class="sxs-lookup"><span data-stu-id="6236d-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="6236d-106">하나의 컴퓨터에서 수천개의 컴퓨터를 사용하여 Azure 서비스 패브릭 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-106">You can create Azure Service Fabric clusters by using anywhere from one to many thousands of machines.</span></span> <span data-ttu-id="6236d-107">응용 프로그램 이진 파일은 다양한 환경에 걸쳐 수정하지 않고 실행할 수 있는 반면 응용 프로그램은 배포하는 컴퓨터의 수에 따라 다르게 구성하려는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-107">While application binaries can run without modification across this wide spectrum of environments, you often want to configure the application differently, depending on the number of machines you're deploying to.</span></span>

<span data-ttu-id="6236d-108">간단한 예로 상태 비저장 서비스에 대해 `InstanceCount` 를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="6236d-109">Azure에서 응용 프로그램을 실행할 때 일반적으로 이 매개 변수를 "-1"이라는 특수 값으로 설정하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-109">When you are running applications in Azure, you generally want to set this parameter to the special value of "-1".</span></span> <span data-ttu-id="6236d-110">이 구성은 서비스가 클러스터의 모든 노드(또는 배치 제약 조건을 설정한 경우 노드 형식의 모든 노드)에서 실행하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-110">This configuration ensures that your service is running on every node in the cluster (or every node in the node type if you have set a placement constraint).</span></span> <span data-ttu-id="6236d-111">그러나 단일 컴퓨터의 동일한 끝점에서 수신하는 여러 프로세스를 가질 수 없으므로 이 구성은 단일 컴퓨터 클러스터에 적합하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on the same endpoint on a single machine.</span></span> <span data-ttu-id="6236d-112">대신 일반적으로 `InstanceCount`를 "1"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-112">Instead, you typically set `InstanceCount` to "1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="6236d-113">환경 특정 매개 변수 지정</span><span class="sxs-lookup"><span data-stu-id="6236d-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="6236d-114">이 구성 문제에 대한 해법은 지정된 환경에 대한 해당 매개 변수 값을 입력하는 매개 변수가 있는 기본 서비스 및 응용 프로그램 매개 변수 파일의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-114">The solution to this configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="6236d-115">기본 서비스 및 응용 프로그램 매개 변수는 응용 프로그램 및 서비스 매니페스트에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-115">Default services and application parameters are configured in the application and service manifests.</span></span> <span data-ttu-id="6236d-116">ServiceManifest.xml 및 ApplicationManifest.xml에 대한 스키마 정의는 Service Fabric SDK 및 도구와 함께 *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-116">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml files is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="6236d-117">기본 서비스</span><span class="sxs-lookup"><span data-stu-id="6236d-117">Default services</span></span>
<span data-ttu-id="6236d-118">서비스 패브릭 응용 프로그램은 서비스 인스턴스의 컬렉션으로 이루어 집니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="6236d-119">빈 응용 프로그램을 만들고 모든 서비스 인스턴스를 동적으로 만들 수 있지만 응용 프로그램 인스턴스화될 때 대부분의 응용 프로그램에는 항상 만들 수 있는 핵심 서비스 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-119">While it is possible for you to create an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when the application is instantiated.</span></span> <span data-ttu-id="6236d-120">이 서비스를 "기본 서비스" 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-120">These are referred to as "default services".</span></span> <span data-ttu-id="6236d-121">예비 대괄호에 포함된 환경 단위 구성에 대한 자리 표시자와 함께 응용 프로그램 매니페스트에서 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-121">They are specified in the application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

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

<span data-ttu-id="6236d-122">각각의 명명된 매개 변수는 응용 프로그램 매니페스트의 매개 변수 요소 내에서 정의되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-122">Each of the named parameters must be defined within the Parameters element of the application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="6236d-123">DefaultValue 특성은 지정된 환경에 보다 구체적인 매개 변수가 없는 경우 사용될 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-123">The DefaultValue attribute specifies the value to be used in the absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="6236d-124">모든 서비스 인스턴스 매개 변수가 환경 단위 구성에 적합하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="6236d-125">파티션 범위가 환경이 아닌 데이터 도메인의 함수이기 때문에 위의 예에서 서비스의 파티션 구성표에 대한 LowKey 및 HighKey 값은 서비스의 모든 인스턴스에 대해 명시적으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-125">In the example above, the LowKey and HighKey values for the service's partitioning scheme are explicitly defined for all instances of the service since the partition range is a function of the data domain, not the environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="6236d-126">환경 단위 서비스 구성 설정</span><span class="sxs-lookup"><span data-stu-id="6236d-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="6236d-127">[서비스 패브릭 응용 프로그램 모델](service-fabric-application-model.md) 을 사용하면 서비스가 런타임에 읽을 수 있는 사용자 지정 키-값 쌍을 포함하는 구성 패키지를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-127">The [Service Fabric application model](service-fabric-application-model.md) enables services to include configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="6236d-128">또한 이러한 설정 값은 응용 프로그램 매니페스트에서 `ConfigOverride` 를 지정하여 환경으로 구별될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-128">The values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in the application manifest.</span></span>

<span data-ttu-id="6236d-129">`Stateful1` 서비스에 대한 Config\Settings.xml 파일에 다음 설정이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-129">Suppose that you have the following setting in the Config\Settings.xml file for the `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="6236d-130">특정 응용 프로그램/환경 쌍에 대해 이 값을 재정의하려면 응용 프로그램 매니페스트에서 서비스 매니페스트를 가져올 때 `ConfigOverride` 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-130">To override this value for a specific application/environment pair, create a `ConfigOverride` when you import the service manifest in the application manifest.</span></span>

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
<span data-ttu-id="6236d-131">이 매개 변수는 위에 표시된 대로 환경에서 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="6236d-132">매개 변수 섹션에서 해당 매개 변수를 선언하고 응용 프로그램 매개 변수 파일에서 환경 특정 값을 지정하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-132">You can do this by declaring it in the parameters section of the application manifest and specifying environment-specific values in the application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="6236d-133">서비스 구성 설정의 경우 키의 값을 설정할 수 있는 세 가지 위치는 다음과 같습니다. 서비스 구성 패키지, 응용 프로그램 매니페스트 및 응용 프로그램 매개 변수 파일.</span><span class="sxs-lookup"><span data-stu-id="6236d-133">In the case of service configuration settings, there are three places where the value of a key can be set: the service configuration package, the application manifest, and the application parameter file.</span></span> <span data-ttu-id="6236d-134">서비스 패브릭은 (지정된 경우) 항상 응용 프로그램 매개 변수 파일에서 먼저 선택한 다음 응용 프로그램 매니페스트 및 마지막으로 구성 패키지에서 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-134">Service Fabric will always choose from the application parameter file first (if specified), then the application manifest, and finally the configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="6236d-135">환경 변수 설정 및 사용</span><span class="sxs-lookup"><span data-stu-id="6236d-135">Setting and using environment variables</span></span> 
<span data-ttu-id="6236d-136">ServiceManifest.xml 파일에 환경 변수를 지정 및 설정한 후 ApplicationManifest.xml 파일에서 인스턴스별로 이를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-136">You can specify and set environment variables in the ServiceManifest.xml file and then override these in the ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="6236d-137">아래 예제에서는 두 개의 환경 변수를 보여 주는데, 하나는 값 집합을 사용하고 다른 하나는 재정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-137">The example below shows two environment variables, one with a value set and the other is overridden.</span></span> <span data-ttu-id="6236d-138">구성 재정의에 사용되는 것과 동일한 방법으로 응용 프로그램 매개 변수를 사용하여 환경 변수 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-138">You can use application parameters to set environment variables values in the same way that these were used for config overrides.</span></span>

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
<span data-ttu-id="6236d-139">ApplicationManifest.xml의 환경 변수를 재정의하려면 `EnvironmentOverrides` 요소가 있는 ServiceManifest의 코드 패키지를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-139">To override the environment variables in the ApplicationManifest.xml, reference the code package in the ServiceManifest with the `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="6236d-140">명명된 서비스 인스턴스가 생성되면 코드에서 환경 변수에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-140">Once the named service instance is created you can access the environment variables from code.</span></span> <span data-ttu-id="6236d-141">예: C#에서 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-141">e.g. In C# you can do the following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="6236d-142">Service Fabric 환경 변수</span><span class="sxs-lookup"><span data-stu-id="6236d-142">Service Fabric environment variables</span></span>
<span data-ttu-id="6236d-143">Service Fabric에는 각 서비스 인스턴스에 대해 설정된 기본 제공 환경 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="6236d-144">환경 변수의 전체 목록은 아래에 제공됩니다. 여기서 굵게 표시된 환경 변수는 서비스에서 사용하게 되고 그렇지 않은 환경 변수는 Service Fabric 런타임에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-144">The full list of environment variables is below, where the ones in bold are the ones that you will use in your service, the other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="6236d-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="6236d-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="6236d-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="6236d-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="6236d-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="6236d-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="6236d-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="6236d-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="6236d-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="6236d-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="6236d-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="6236d-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="6236d-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span><span class="sxs-lookup"><span data-stu-id="6236d-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="6236d-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="6236d-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="6236d-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="6236d-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="6236d-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="6236d-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="6236d-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="6236d-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="6236d-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="6236d-156">Fabric_NodeId</span></span>
* <span data-ttu-id="6236d-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="6236d-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="6236d-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="6236d-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="6236d-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="6236d-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="6236d-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="6236d-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="6236d-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="6236d-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="6236d-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="6236d-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="6236d-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="6236d-163">FabricPackageFileName</span></span>

<span data-ttu-id="6236d-164">아래 코드에서는 Service Fabric 환경 변수를 나열하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-164">The code belows shows how to list the Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="6236d-165">다음은 로컬 개발 컴퓨터에서 실행할 때 `FrontEndService`라는 서비스 유형을 갖는 `GuestExe.Application`이라는 응용 프로그램 유형에 대한 환경 변수의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-165">The following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="6236d-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span><span class="sxs-lookup"><span data-stu-id="6236d-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="6236d-167">**Fabric_CodePackageName = Code**</span><span class="sxs-lookup"><span data-stu-id="6236d-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="6236d-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="6236d-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="6236d-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="6236d-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="6236d-170">**Fabric_NodeName = _Node_2**</span><span class="sxs-lookup"><span data-stu-id="6236d-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="6236d-171">응용 프로그램 매개 변수 파일</span><span class="sxs-lookup"><span data-stu-id="6236d-171">Application parameter files</span></span>
<span data-ttu-id="6236d-172">서비스 패브릭 응용 프로그램 프로젝트는 하나 이상의 응용 프로그램 매개 변수 파일을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-172">The Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="6236d-173">각각은 응용 프로그램 매니페스트에서 정의된 매개 변수에 특정 값을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-173">Each of them defines the specific values for the parameters that are defined in the application manifest:</span></span>

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
<span data-ttu-id="6236d-174">기본적으로 새 응용 프로그램은 Local.1Node.xml, Local.5Node.xml 및 Cloud.xml라는 세 응용 프로그램 매개 변수 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![솔루션 탐색기에서 응용 프로그램 매개 변수 파일][app-parameters-solution-explorer]

<span data-ttu-id="6236d-176">매개 변수 파일을 만들려면 기존 매개 변수 파일을 복사하고 붙여 넣은 다음 새 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-176">To create a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="6236d-177">배포하는 동안 환경 단위 매개 변수 식별</span><span class="sxs-lookup"><span data-stu-id="6236d-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="6236d-178">배포 시 적절한 매개 변수 파일을 선택하여 응용 프로그램에 적용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-178">At deployment time, you need to choose the appropriate parameter file to apply with your application.</span></span> <span data-ttu-id="6236d-179">Visual Studio의 게시 대화 상자 또는 PowerShell을 통해 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-179">You can do this through the Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="6236d-180">Visual Studio에서 배포</span><span class="sxs-lookup"><span data-stu-id="6236d-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="6236d-181">Visual Studio에서 응용 프로그램을 게시하는 경우 사용 가능한 매개 변수 파일의 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-181">You can choose from the list of available parameter files when you publish your application in Visual Studio.</span></span>

![게시 대화 상자에서 매개 변수 파일 선택][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="6236d-183">PowerShell에서 배포</span><span class="sxs-lookup"><span data-stu-id="6236d-183">Deploy from PowerShell</span></span>
<span data-ttu-id="6236d-184">응용 프로그램 프로젝트 템플릿에 포함된 `Deploy-FabricApplication.ps1` PowerShell 스크립트는 매개 변수로 게시 프로필을 수락하고 게시 프로필은 응용 프로그램 매개 변수 파일에 대한 참조를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6236d-184">The `Deploy-FabricApplication.ps1` PowerShell script included in the application project template accepts a publish profile as a parameter and the PublishProfile contains a reference to the application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="6236d-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6236d-185">Next steps</span></span>
<span data-ttu-id="6236d-186">이 토픽에서 설명하는 핵심 개념 중 일부에 대해 자세히 알아보려면 [서비스 패브릭 기술 개요](service-fabric-technical-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6236d-186">To learn more about some of the core concepts that are discussed in this topic, see the [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="6236d-187">Visual Studio에서 사용할 수 있는 다른 앱 관리 기능에 대한 정보는 [Visual Studio에서 서비스 패브릭 응용 프로그램 관리](service-fabric-manage-application-in-visual-studio.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6236d-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
