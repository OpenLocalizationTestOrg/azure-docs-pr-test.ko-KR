---
title: "클라우드 서비스 역할 구성 XPath 참고 자료 | Microsoft Docs"
description: "클라우드 서비스 역할 구성에서 설정을 환경 변수로 노출하기 위해 사용할 수 있는 다양한 XPath 설정입니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: fd6efac829d3fd9e2840362b8d2ff423add566d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="29c27-103">XPath를 사용하여 역할 구성 설정을 환경 변수로 노출</span><span class="sxs-lookup"><span data-stu-id="29c27-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="29c27-104">클라우드 서비스 작업자 또는 웹 역할 서비스 정의 파일에서 런타임 구성 값을 환경 변수로 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-104">In the cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="29c27-105">다음 XPath 값(API 값에 해당)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-105">The following XPath values are supported (which correspond to API values).</span></span>

<span data-ttu-id="29c27-106">이러한 XPath 값을 [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) 라이브러리를 통해서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-106">These XPath values are also available through the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="29c27-107">앱이 에뮬레이터에서 실행 중임</span><span class="sxs-lookup"><span data-stu-id="29c27-107">App running in emulator</span></span>
<span data-ttu-id="29c27-108">앱이 에뮬레이터에서 실행 중임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-108">Indicates that the app is running in the emulator.</span></span>

| <span data-ttu-id="29c27-109">형식</span><span class="sxs-lookup"><span data-stu-id="29c27-109">Type</span></span> | <span data-ttu-id="29c27-110">예</span><span class="sxs-lookup"><span data-stu-id="29c27-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="29c27-111">XPath</span><span class="sxs-lookup"><span data-stu-id="29c27-111">XPath</span></span> |<span data-ttu-id="29c27-112">xpath="/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="29c27-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="29c27-113">코드</span><span class="sxs-lookup"><span data-stu-id="29c27-113">Code</span></span> |<span data-ttu-id="29c27-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="29c27-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="29c27-115">배포 ID</span><span class="sxs-lookup"><span data-stu-id="29c27-115">Deployment ID</span></span>
<span data-ttu-id="29c27-116">인스턴스의 배포 ID를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-116">Retrieves the deployment ID for the instance.</span></span>

| <span data-ttu-id="29c27-117">형식</span><span class="sxs-lookup"><span data-stu-id="29c27-117">Type</span></span> | <span data-ttu-id="29c27-118">예</span><span class="sxs-lookup"><span data-stu-id="29c27-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="29c27-119">XPath</span><span class="sxs-lookup"><span data-stu-id="29c27-119">XPath</span></span> |<span data-ttu-id="29c27-120">xpath="/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="29c27-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="29c27-121">코드</span><span class="sxs-lookup"><span data-stu-id="29c27-121">Code</span></span> |<span data-ttu-id="29c27-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="29c27-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="29c27-123">역할 ID</span><span class="sxs-lookup"><span data-stu-id="29c27-123">Role ID</span></span>
<span data-ttu-id="29c27-124">인스턴스의 현재 역할 ID를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-124">Retrieves the current role ID for the instance.</span></span>

| <span data-ttu-id="29c27-125">형식</span><span class="sxs-lookup"><span data-stu-id="29c27-125">Type</span></span> | <span data-ttu-id="29c27-126">예</span><span class="sxs-lookup"><span data-stu-id="29c27-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="29c27-127">XPath</span><span class="sxs-lookup"><span data-stu-id="29c27-127">XPath</span></span> |<span data-ttu-id="29c27-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="29c27-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="29c27-129">코드</span><span class="sxs-lookup"><span data-stu-id="29c27-129">Code</span></span> |<span data-ttu-id="29c27-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="29c27-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="29c27-131">도메인 업데이트</span><span class="sxs-lookup"><span data-stu-id="29c27-131">Update domain</span></span>
<span data-ttu-id="29c27-132">인스턴스의 업데이트 도메인을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-132">Retrieves the update domain of the instance.</span></span>

| <span data-ttu-id="29c27-133">형식</span><span class="sxs-lookup"><span data-stu-id="29c27-133">Type</span></span> | <span data-ttu-id="29c27-134">예</span><span class="sxs-lookup"><span data-stu-id="29c27-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="29c27-135">XPath</span><span class="sxs-lookup"><span data-stu-id="29c27-135">XPath</span></span> |<span data-ttu-id="29c27-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="29c27-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="29c27-137">코드</span><span class="sxs-lookup"><span data-stu-id="29c27-137">Code</span></span> |<span data-ttu-id="29c27-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="29c27-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="29c27-139">장애 도메인</span><span class="sxs-lookup"><span data-stu-id="29c27-139">Fault domain</span></span>
<span data-ttu-id="29c27-140">인스턴스의 장애 도메인을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-140">Retrieves the fault domain of the instance.</span></span>

| <span data-ttu-id="29c27-141">형식</span><span class="sxs-lookup"><span data-stu-id="29c27-141">Type</span></span> | <span data-ttu-id="29c27-142">예</span><span class="sxs-lookup"><span data-stu-id="29c27-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="29c27-143">XPath</span><span class="sxs-lookup"><span data-stu-id="29c27-143">XPath</span></span> |<span data-ttu-id="29c27-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="29c27-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="29c27-145">코드</span><span class="sxs-lookup"><span data-stu-id="29c27-145">Code</span></span> |<span data-ttu-id="29c27-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="29c27-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="29c27-147">역할 이름</span><span class="sxs-lookup"><span data-stu-id="29c27-147">Role name</span></span>
<span data-ttu-id="29c27-148">인스턴스의 역할 이름을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-148">Retrieves the role name of the instances.</span></span>

| <span data-ttu-id="29c27-149">형식</span><span class="sxs-lookup"><span data-stu-id="29c27-149">Type</span></span> | <span data-ttu-id="29c27-150">예</span><span class="sxs-lookup"><span data-stu-id="29c27-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="29c27-151">XPath</span><span class="sxs-lookup"><span data-stu-id="29c27-151">XPath</span></span> |<span data-ttu-id="29c27-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="29c27-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="29c27-153">코드</span><span class="sxs-lookup"><span data-stu-id="29c27-153">Code</span></span> |<span data-ttu-id="29c27-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="29c27-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="29c27-155">구성 설정</span><span class="sxs-lookup"><span data-stu-id="29c27-155">Config setting</span></span>
<span data-ttu-id="29c27-156">지정된 구성 설정의 값을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-156">Retrieves the value of the specified configuration setting.</span></span>

| <span data-ttu-id="29c27-157">형식</span><span class="sxs-lookup"><span data-stu-id="29c27-157">Type</span></span> | <span data-ttu-id="29c27-158">예</span><span class="sxs-lookup"><span data-stu-id="29c27-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="29c27-159">XPath</span><span class="sxs-lookup"><span data-stu-id="29c27-159">XPath</span></span> |<span data-ttu-id="29c27-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span><span class="sxs-lookup"><span data-stu-id="29c27-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="29c27-161">코드</span><span class="sxs-lookup"><span data-stu-id="29c27-161">Code</span></span> |<span data-ttu-id="29c27-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="29c27-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="29c27-163">로컬 저장소 경로</span><span class="sxs-lookup"><span data-stu-id="29c27-163">Local storage path</span></span>
<span data-ttu-id="29c27-164">인스턴스에 대한 로컬 저장소 경로를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-164">Retrieves the local storage path for the instance.</span></span>

| <span data-ttu-id="29c27-165">형식</span><span class="sxs-lookup"><span data-stu-id="29c27-165">Type</span></span> | <span data-ttu-id="29c27-166">예</span><span class="sxs-lookup"><span data-stu-id="29c27-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="29c27-167">XPath</span><span class="sxs-lookup"><span data-stu-id="29c27-167">XPath</span></span> |<span data-ttu-id="29c27-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span><span class="sxs-lookup"><span data-stu-id="29c27-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="29c27-169">코드</span><span class="sxs-lookup"><span data-stu-id="29c27-169">Code</span></span> |<span data-ttu-id="29c27-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span><span class="sxs-lookup"><span data-stu-id="29c27-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="29c27-171">로컬 저장소 크기</span><span class="sxs-lookup"><span data-stu-id="29c27-171">Local storage size</span></span>
<span data-ttu-id="29c27-172">인스턴스의 로컬 저장소 크기를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-172">Retrieves the size of the local storage for the instance.</span></span>

| <span data-ttu-id="29c27-173">형식</span><span class="sxs-lookup"><span data-stu-id="29c27-173">Type</span></span> | <span data-ttu-id="29c27-174">예</span><span class="sxs-lookup"><span data-stu-id="29c27-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="29c27-175">XPath</span><span class="sxs-lookup"><span data-stu-id="29c27-175">XPath</span></span> |<span data-ttu-id="29c27-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="29c27-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="29c27-177">코드</span><span class="sxs-lookup"><span data-stu-id="29c27-177">Code</span></span> |<span data-ttu-id="29c27-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="29c27-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="29c27-179">끝점 프로토콜</span><span class="sxs-lookup"><span data-stu-id="29c27-179">Endpoint protocol</span></span>
<span data-ttu-id="29c27-180">인스턴스의 끝점 프로토콜을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-180">Retrieves the endpoint protocol for the instance.</span></span>

| <span data-ttu-id="29c27-181">형식</span><span class="sxs-lookup"><span data-stu-id="29c27-181">Type</span></span> | <span data-ttu-id="29c27-182">예</span><span class="sxs-lookup"><span data-stu-id="29c27-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="29c27-183">XPath</span><span class="sxs-lookup"><span data-stu-id="29c27-183">XPath</span></span> |<span data-ttu-id="29c27-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="29c27-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="29c27-185">코드</span><span class="sxs-lookup"><span data-stu-id="29c27-185">Code</span></span> |<span data-ttu-id="29c27-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span><span class="sxs-lookup"><span data-stu-id="29c27-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="29c27-187">끝점 IP</span><span class="sxs-lookup"><span data-stu-id="29c27-187">Endpoint IP</span></span>
<span data-ttu-id="29c27-188">지정된 끝점의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-188">Gets the specified endpoint's IP address.</span></span>

| <span data-ttu-id="29c27-189">형식</span><span class="sxs-lookup"><span data-stu-id="29c27-189">Type</span></span> | <span data-ttu-id="29c27-190">예</span><span class="sxs-lookup"><span data-stu-id="29c27-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="29c27-191">XPath</span><span class="sxs-lookup"><span data-stu-id="29c27-191">XPath</span></span> |<span data-ttu-id="29c27-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span><span class="sxs-lookup"><span data-stu-id="29c27-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="29c27-193">코드</span><span class="sxs-lookup"><span data-stu-id="29c27-193">Code</span></span> |<span data-ttu-id="29c27-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="29c27-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="29c27-195">끝점 포트</span><span class="sxs-lookup"><span data-stu-id="29c27-195">Endpoint port</span></span>
<span data-ttu-id="29c27-196">인스턴스의 끝점 포트를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-196">Retrieves the endpoint port for the instance.</span></span>

| <span data-ttu-id="29c27-197">형식</span><span class="sxs-lookup"><span data-stu-id="29c27-197">Type</span></span> | <span data-ttu-id="29c27-198">예</span><span class="sxs-lookup"><span data-stu-id="29c27-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="29c27-199">XPath</span><span class="sxs-lookup"><span data-stu-id="29c27-199">XPath</span></span> |<span data-ttu-id="29c27-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span><span class="sxs-lookup"><span data-stu-id="29c27-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="29c27-201">코드</span><span class="sxs-lookup"><span data-stu-id="29c27-201">Code</span></span> |<span data-ttu-id="29c27-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="29c27-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="29c27-203">예제</span><span class="sxs-lookup"><span data-stu-id="29c27-203">Example</span></span>
<span data-ttu-id="29c27-204">다음은 [@emulated xpath 값](#app-running-in-emulator)으로 설정된 환경 변수 `TestIsEmulated`를 사용하여 시작 작업을 만드는 작업자 역할의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set to the [@emulated xpath value](#app-running-in-emulator).</span></span> 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a><span data-ttu-id="29c27-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="29c27-205">Next steps</span></span>
<span data-ttu-id="29c27-206">[ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) 파일에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-206">Learn more about the [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="29c27-207">[ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="29c27-208">역할에 대해 [원격 데스크톱](cloud-services-role-enable-remote-desktop.md) 을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="29c27-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

