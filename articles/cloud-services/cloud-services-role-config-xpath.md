---
title: "aaaCloud 서비스 역할 구성 XPath 치트 시트 | Microsoft Docs"
description: "안녕 다양 한 XPath 설정이 환경 변수로 hello 클라우드 서비스 역할 구성 tooexpose 설정에서 사용할 수 있습니다."
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
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="97466-103">XPath를 사용하여 역할 구성 설정을 환경 변수로 노출</span><span class="sxs-lookup"><span data-stu-id="97466-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="97466-104">Hello 클라우드 서비스 작업자 또는 웹 역할 서비스 정의 파일에서 환경 변수로 런타임 구성 값을 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97466-104">In hello cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="97466-105">다음 XPath 값에는 hello (tooAPI 값에 해당)는 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97466-105">hello following XPath values are supported (which correspond tooAPI values).</span></span>

<span data-ttu-id="97466-106">이러한 XPath 값은 hello를 통해 사용할 수 또한 [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="97466-106">These XPath values are also available through hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="97466-107">앱이 에뮬레이터에서 실행 중임</span><span class="sxs-lookup"><span data-stu-id="97466-107">App running in emulator</span></span>
<span data-ttu-id="97466-108">Hello 이러한 앱 hello 에뮬레이터에서 실행 되 고 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="97466-108">Indicates that hello app is running in hello emulator.</span></span>

| <span data-ttu-id="97466-109">형식</span><span class="sxs-lookup"><span data-stu-id="97466-109">Type</span></span> | <span data-ttu-id="97466-110">예</span><span class="sxs-lookup"><span data-stu-id="97466-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="97466-111">XPath</span><span class="sxs-lookup"><span data-stu-id="97466-111">XPath</span></span> |<span data-ttu-id="97466-112">xpath="/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="97466-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="97466-113">코드</span><span class="sxs-lookup"><span data-stu-id="97466-113">Code</span></span> |<span data-ttu-id="97466-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="97466-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="97466-115">배포 ID</span><span class="sxs-lookup"><span data-stu-id="97466-115">Deployment ID</span></span>
<span data-ttu-id="97466-116">Hello 인스턴스에 대 한 hello 배포 ID를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="97466-116">Retrieves hello deployment ID for hello instance.</span></span>

| <span data-ttu-id="97466-117">형식</span><span class="sxs-lookup"><span data-stu-id="97466-117">Type</span></span> | <span data-ttu-id="97466-118">예</span><span class="sxs-lookup"><span data-stu-id="97466-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="97466-119">XPath</span><span class="sxs-lookup"><span data-stu-id="97466-119">XPath</span></span> |<span data-ttu-id="97466-120">xpath="/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="97466-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="97466-121">코드</span><span class="sxs-lookup"><span data-stu-id="97466-121">Code</span></span> |<span data-ttu-id="97466-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="97466-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="97466-123">역할 ID</span><span class="sxs-lookup"><span data-stu-id="97466-123">Role ID</span></span>
<span data-ttu-id="97466-124">Hello hello 인스턴스의 현재 역할 ID를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="97466-124">Retrieves hello current role ID for hello instance.</span></span>

| <span data-ttu-id="97466-125">형식</span><span class="sxs-lookup"><span data-stu-id="97466-125">Type</span></span> | <span data-ttu-id="97466-126">예</span><span class="sxs-lookup"><span data-stu-id="97466-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="97466-127">XPath</span><span class="sxs-lookup"><span data-stu-id="97466-127">XPath</span></span> |<span data-ttu-id="97466-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="97466-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="97466-129">코드</span><span class="sxs-lookup"><span data-stu-id="97466-129">Code</span></span> |<span data-ttu-id="97466-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="97466-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="97466-131">도메인 업데이트</span><span class="sxs-lookup"><span data-stu-id="97466-131">Update domain</span></span>
<span data-ttu-id="97466-132">Hello 인스턴스의 hello 업데이트 도메인을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="97466-132">Retrieves hello update domain of hello instance.</span></span>

| <span data-ttu-id="97466-133">형식</span><span class="sxs-lookup"><span data-stu-id="97466-133">Type</span></span> | <span data-ttu-id="97466-134">예</span><span class="sxs-lookup"><span data-stu-id="97466-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="97466-135">XPath</span><span class="sxs-lookup"><span data-stu-id="97466-135">XPath</span></span> |<span data-ttu-id="97466-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="97466-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="97466-137">코드</span><span class="sxs-lookup"><span data-stu-id="97466-137">Code</span></span> |<span data-ttu-id="97466-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="97466-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="97466-139">장애 도메인</span><span class="sxs-lookup"><span data-stu-id="97466-139">Fault domain</span></span>
<span data-ttu-id="97466-140">Hello 인스턴스의 hello 장애 도메인을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="97466-140">Retrieves hello fault domain of hello instance.</span></span>

| <span data-ttu-id="97466-141">형식</span><span class="sxs-lookup"><span data-stu-id="97466-141">Type</span></span> | <span data-ttu-id="97466-142">예</span><span class="sxs-lookup"><span data-stu-id="97466-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="97466-143">XPath</span><span class="sxs-lookup"><span data-stu-id="97466-143">XPath</span></span> |<span data-ttu-id="97466-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="97466-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="97466-145">코드</span><span class="sxs-lookup"><span data-stu-id="97466-145">Code</span></span> |<span data-ttu-id="97466-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="97466-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="97466-147">역할 이름</span><span class="sxs-lookup"><span data-stu-id="97466-147">Role name</span></span>
<span data-ttu-id="97466-148">Hello 인스턴스의 hello 역할 이름을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="97466-148">Retrieves hello role name of hello instances.</span></span>

| <span data-ttu-id="97466-149">형식</span><span class="sxs-lookup"><span data-stu-id="97466-149">Type</span></span> | <span data-ttu-id="97466-150">예</span><span class="sxs-lookup"><span data-stu-id="97466-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="97466-151">XPath</span><span class="sxs-lookup"><span data-stu-id="97466-151">XPath</span></span> |<span data-ttu-id="97466-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="97466-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="97466-153">코드</span><span class="sxs-lookup"><span data-stu-id="97466-153">Code</span></span> |<span data-ttu-id="97466-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="97466-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="97466-155">구성 설정</span><span class="sxs-lookup"><span data-stu-id="97466-155">Config setting</span></span>
<span data-ttu-id="97466-156">Hello 검색 hello 값이 구성 설정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97466-156">Retrieves hello value of hello specified configuration setting.</span></span>

| <span data-ttu-id="97466-157">형식</span><span class="sxs-lookup"><span data-stu-id="97466-157">Type</span></span> | <span data-ttu-id="97466-158">예</span><span class="sxs-lookup"><span data-stu-id="97466-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="97466-159">XPath</span><span class="sxs-lookup"><span data-stu-id="97466-159">XPath</span></span> |<span data-ttu-id="97466-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span><span class="sxs-lookup"><span data-stu-id="97466-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="97466-161">코드</span><span class="sxs-lookup"><span data-stu-id="97466-161">Code</span></span> |<span data-ttu-id="97466-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="97466-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="97466-163">로컬 저장소 경로</span><span class="sxs-lookup"><span data-stu-id="97466-163">Local storage path</span></span>
<span data-ttu-id="97466-164">Hello 인스턴스에 대 한 hello 로컬 저장소 경로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="97466-164">Retrieves hello local storage path for hello instance.</span></span>

| <span data-ttu-id="97466-165">형식</span><span class="sxs-lookup"><span data-stu-id="97466-165">Type</span></span> | <span data-ttu-id="97466-166">예</span><span class="sxs-lookup"><span data-stu-id="97466-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="97466-167">XPath</span><span class="sxs-lookup"><span data-stu-id="97466-167">XPath</span></span> |<span data-ttu-id="97466-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span><span class="sxs-lookup"><span data-stu-id="97466-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="97466-169">코드</span><span class="sxs-lookup"><span data-stu-id="97466-169">Code</span></span> |<span data-ttu-id="97466-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span><span class="sxs-lookup"><span data-stu-id="97466-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="97466-171">로컬 저장소 크기</span><span class="sxs-lookup"><span data-stu-id="97466-171">Local storage size</span></span>
<span data-ttu-id="97466-172">Hello hello 인스턴스에 대 한 로컬 저장소의 hello 크기를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="97466-172">Retrieves hello size of hello local storage for hello instance.</span></span>

| <span data-ttu-id="97466-173">형식</span><span class="sxs-lookup"><span data-stu-id="97466-173">Type</span></span> | <span data-ttu-id="97466-174">예</span><span class="sxs-lookup"><span data-stu-id="97466-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="97466-175">XPath</span><span class="sxs-lookup"><span data-stu-id="97466-175">XPath</span></span> |<span data-ttu-id="97466-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="97466-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="97466-177">코드</span><span class="sxs-lookup"><span data-stu-id="97466-177">Code</span></span> |<span data-ttu-id="97466-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="97466-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="97466-179">끝점 프로토콜</span><span class="sxs-lookup"><span data-stu-id="97466-179">Endpoint protocol</span></span>
<span data-ttu-id="97466-180">Hello 인스턴스에 대 한 hello 끝점 프로토콜을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="97466-180">Retrieves hello endpoint protocol for hello instance.</span></span>

| <span data-ttu-id="97466-181">형식</span><span class="sxs-lookup"><span data-stu-id="97466-181">Type</span></span> | <span data-ttu-id="97466-182">예</span><span class="sxs-lookup"><span data-stu-id="97466-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="97466-183">XPath</span><span class="sxs-lookup"><span data-stu-id="97466-183">XPath</span></span> |<span data-ttu-id="97466-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="97466-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="97466-185">코드</span><span class="sxs-lookup"><span data-stu-id="97466-185">Code</span></span> |<span data-ttu-id="97466-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span><span class="sxs-lookup"><span data-stu-id="97466-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="97466-187">끝점 IP</span><span class="sxs-lookup"><span data-stu-id="97466-187">Endpoint IP</span></span>
<span data-ttu-id="97466-188">가져옵니다 hello 끝점의 IP 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97466-188">Gets hello specified endpoint's IP address.</span></span>

| <span data-ttu-id="97466-189">형식</span><span class="sxs-lookup"><span data-stu-id="97466-189">Type</span></span> | <span data-ttu-id="97466-190">예</span><span class="sxs-lookup"><span data-stu-id="97466-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="97466-191">XPath</span><span class="sxs-lookup"><span data-stu-id="97466-191">XPath</span></span> |<span data-ttu-id="97466-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span><span class="sxs-lookup"><span data-stu-id="97466-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="97466-193">코드</span><span class="sxs-lookup"><span data-stu-id="97466-193">Code</span></span> |<span data-ttu-id="97466-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="97466-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="97466-195">끝점 포트</span><span class="sxs-lookup"><span data-stu-id="97466-195">Endpoint port</span></span>
<span data-ttu-id="97466-196">Hello 인스턴스에 대 한 hello 끝점 포트를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="97466-196">Retrieves hello endpoint port for hello instance.</span></span>

| <span data-ttu-id="97466-197">형식</span><span class="sxs-lookup"><span data-stu-id="97466-197">Type</span></span> | <span data-ttu-id="97466-198">예</span><span class="sxs-lookup"><span data-stu-id="97466-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="97466-199">XPath</span><span class="sxs-lookup"><span data-stu-id="97466-199">XPath</span></span> |<span data-ttu-id="97466-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span><span class="sxs-lookup"><span data-stu-id="97466-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="97466-201">코드</span><span class="sxs-lookup"><span data-stu-id="97466-201">Code</span></span> |<span data-ttu-id="97466-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="97466-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="97466-203">예제</span><span class="sxs-lookup"><span data-stu-id="97466-203">Example</span></span>
<span data-ttu-id="97466-204">시작 작업 라는 환경 변수를 만드는 작업자 역할의 예로 `TestIsEmulated` toohello 설정 [ @emulated xpath 값](#app-running-in-emulator)합니다.</span><span class="sxs-lookup"><span data-stu-id="97466-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set toohello [@emulated xpath value](#app-running-in-emulator).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="97466-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="97466-205">Next steps</span></span>
<span data-ttu-id="97466-206">Hello에 대 한 자세한 [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="97466-206">Learn more about hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="97466-207">[ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="97466-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="97466-208">역할에 대해 [원격 데스크톱](cloud-services-role-enable-remote-desktop.md) 을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="97466-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

