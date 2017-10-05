---
title: "Linux용 OMS Azure Virtual Machine 확장 | Microsoft Docs"
description: "가상 컴퓨터 확장을 사용하여 Linux 가상 컴퓨터에 OMS 에이전트를 배포합니다."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 138fc8c98ea6f409b28407b20851c96ecc618b09
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="37d54-103">Linux용 OMS 가상 컴퓨터 확장</span><span class="sxs-lookup"><span data-stu-id="37d54-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="37d54-104">개요</span><span class="sxs-lookup"><span data-stu-id="37d54-104">Overview</span></span>

<span data-ttu-id="37d54-105">OMS(Operations Management Suite)는 클라우드와 온-프레미스 자산에서 모니터링, 경고 및 경고 수정 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="37d54-106">Linux용 OMS 에이전트 가상 컴퓨터 확장은 Microsoft에서 게시 및 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-106">The OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="37d54-107">확장 버전은 Azure Virtual Machines에 OMS 에이전트를 설치하고 기존 OMS 작업 영역에 가상 컴퓨터를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-107">The extension installs the OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="37d54-108">이 문서에서는 지원되는 플랫폼, 구성 및 Linux용 OMS 가상 컴퓨터 확장에 대한 배포 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-108">This document details the supported platforms, configurations, and deployment options for the OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37d54-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="37d54-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="37d54-110">운영 체제</span><span class="sxs-lookup"><span data-stu-id="37d54-110">Operating system</span></span>

<span data-ttu-id="37d54-111">OM 에이전트 확장은 다음 Linux 배포판에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-111">The OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="37d54-112">배포</span><span class="sxs-lookup"><span data-stu-id="37d54-112">Distribution</span></span> | <span data-ttu-id="37d54-113">버전</span><span class="sxs-lookup"><span data-stu-id="37d54-113">Version</span></span> |
|---|---|
| <span data-ttu-id="37d54-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="37d54-114">CentOS Linux</span></span> | <span data-ttu-id="37d54-115">5, 6 및 7</span><span class="sxs-lookup"><span data-stu-id="37d54-115">5, 6, and 7</span></span> |
| <span data-ttu-id="37d54-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="37d54-116">Oracle Linux</span></span> | <span data-ttu-id="37d54-117">5, 6 및 7</span><span class="sxs-lookup"><span data-stu-id="37d54-117">5, 6, and 7</span></span> |
| <span data-ttu-id="37d54-118">Red Hat Enterprise Linux Server</span><span class="sxs-lookup"><span data-stu-id="37d54-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="37d54-119">5, 6 및 7</span><span class="sxs-lookup"><span data-stu-id="37d54-119">5, 6 and 7</span></span> |
| <span data-ttu-id="37d54-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="37d54-120">Debian GNU/Linux</span></span> | <span data-ttu-id="37d54-121">6, 7 및 8</span><span class="sxs-lookup"><span data-stu-id="37d54-121">6, 7, and 8</span></span> |
| <span data-ttu-id="37d54-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="37d54-122">Ubuntu</span></span> | <span data-ttu-id="37d54-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="37d54-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span></span> |
| <span data-ttu-id="37d54-124">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="37d54-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="37d54-125">11 및 12</span><span class="sxs-lookup"><span data-stu-id="37d54-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="37d54-126">인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="37d54-126">Internet connectivity</span></span>

<span data-ttu-id="37d54-127">Linux용 OMS 에이전트 확장은 대상 가상 컴퓨터가 인터넷에 연결되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-127">The OMS Agent extension for Linux requires that the target virtual machine is connected to the internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="37d54-128">확장 스키마</span><span class="sxs-lookup"><span data-stu-id="37d54-128">Extension schema</span></span>

<span data-ttu-id="37d54-129">다음 JSON은 OMS 에이전트 확장에 대한 스키마를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-129">The following JSON shows the schema for the OMS Agent extension.</span></span> <span data-ttu-id="37d54-130">이 확장은 대상 OMS 작업 영역에서 작업 영역 ID와 작업 영역 키가 필요하며, 이러한 값은 OMS 포털에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-130">The extension requires the workspace ID and workspace key from the target OMS workspace; these values can be found in the OMS portal.</span></span> <span data-ttu-id="37d54-131">작업 영역 키는 중요한 데이터로 처리되므로 보호되는 설정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-131">Because the workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="37d54-132">Azure VM 확장으로 보호되는 설정 데이터는 암호화되어 대상 가상 컴퓨터에서만 해독됩니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-132">Azure VM extension protected setting data is encrypted, and only decrypted on the target virtual machine.</span></span> <span data-ttu-id="37d54-133">**workspaceId** 및 **workspaceKey**는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a><span data-ttu-id="37d54-134">속성 값</span><span class="sxs-lookup"><span data-stu-id="37d54-134">Property values</span></span>

| <span data-ttu-id="37d54-135">이름</span><span class="sxs-lookup"><span data-stu-id="37d54-135">Name</span></span> | <span data-ttu-id="37d54-136">값/예제</span><span class="sxs-lookup"><span data-stu-id="37d54-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="37d54-137">apiVersion</span><span class="sxs-lookup"><span data-stu-id="37d54-137">apiVersion</span></span> | <span data-ttu-id="37d54-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="37d54-138">2015-06-15</span></span> |
| <span data-ttu-id="37d54-139">publisher</span><span class="sxs-lookup"><span data-stu-id="37d54-139">publisher</span></span> | <span data-ttu-id="37d54-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="37d54-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="37d54-141">type</span><span class="sxs-lookup"><span data-stu-id="37d54-141">type</span></span> | <span data-ttu-id="37d54-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="37d54-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="37d54-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="37d54-143">typeHandlerVersion</span></span> | <span data-ttu-id="37d54-144">1.4</span><span class="sxs-lookup"><span data-stu-id="37d54-144">1.4</span></span> |
| <span data-ttu-id="37d54-145">workspaceId(예)</span><span class="sxs-lookup"><span data-stu-id="37d54-145">workspaceId (e.g)</span></span> | <span data-ttu-id="37d54-146">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="37d54-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="37d54-147">workspaceKey(예)</span><span class="sxs-lookup"><span data-stu-id="37d54-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="37d54-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="37d54-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="37d54-149">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="37d54-149">Template deployment</span></span>

<span data-ttu-id="37d54-150">Azure Resource Manager 템플릿을 사용하여 Azure VM 확장을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="37d54-151">템플릿은 OMS에 온보딩과 같이 배포 후 구성이 필요한 하나 이상의 Virtual Machines를 배포하는 경우에 이상적입니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding to OMS.</span></span> <span data-ttu-id="37d54-152">OMS 에이전트 VM 확장을 포함하는 샘플 Resource Manager 템플릿은 [Azure 빠른 시작 갤러리](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-152">A sample Resource Manager template that includes the OMS Agent VM extension can be found on the [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="37d54-153">가상 컴퓨터 확장에 대한 JSON 구성은 가상 컴퓨터 리소스 내에 중첩되거나 루트 또는 최상위 수준의 Resource Manager JSON 템플릿에 배치될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-153">The JSON configuration for a virtual machine extension can be nested inside the virtual machine resource, or placed at the root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="37d54-154">JSON 구성의 배치는 리소스 이름 및 형식 값에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-154">The placement of the JSON configuration affects the value of the resource name and type.</span></span> <span data-ttu-id="37d54-155">자세한 내용은 [자식 리소스의 이름 및 형식 설정](../../azure-resource-manager/resource-manager-template-child-resource.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37d54-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="37d54-156">다음 예제에서는 OMS 확장이 가상 컴퓨터 리소스 내에 중첩되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-156">The following example assumes the OMS extension is nested inside the virtual machine resource.</span></span> <span data-ttu-id="37d54-157">확장 리소스를 중첩하는 경우 JSON은 가상 컴퓨터의 `"resources": []` 개체에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-157">When nesting the extension resource, the JSON is placed in the `"resources": []` object of the virtual machine.</span></span>

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

<span data-ttu-id="37d54-158">템플릿의 루트에 JSON 확장을 배치하면 리소스 이름에 부모 가상 컴퓨터에 대한 참조가 포함되며 형식은 중첩된 구성을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-158">When placing the extension JSON at the root of the template, the resource name includes a reference to the parent virtual machine, and the type reflects the nested configuration.</span></span>  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a><span data-ttu-id="37d54-159">Azure CLI 배포</span><span class="sxs-lookup"><span data-stu-id="37d54-159">Azure CLI deployment</span></span>

<span data-ttu-id="37d54-160">Azure CLI를 사용하여 OMS 에이전트 VM 확장을 기존 가상 컴퓨터에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-160">The Azure CLI can be used to deploy the OMS Agent VM extension to an existing virtual machine.</span></span> <span data-ttu-id="37d54-161">OMS 키 및 OMS ID를 OMS 작업 영역의 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-161">Replace the OMS key and OMS ID with those from your OMS workspace.</span></span> 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="37d54-162">문제 해결 및 지원</span><span class="sxs-lookup"><span data-stu-id="37d54-162">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="37d54-163">문제 해결</span><span class="sxs-lookup"><span data-stu-id="37d54-163">Troubleshoot</span></span>

<span data-ttu-id="37d54-164">확장 배포 상태에 대한 데이터는 Azure CLI를 사용하여 Azure Portal에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-164">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure CLI.</span></span> <span data-ttu-id="37d54-165">지정된 VM에 대한 확장의 배포 상태를 보려면 Azure CLI를 사용하여 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-165">To see the deployment state of extensions for a given VM, run the following command using the Azure CLI.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="37d54-166">확장 실행 출력은 다음 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-166">Extension execution output is logged to the following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a><span data-ttu-id="37d54-167">오류 코드 및 해당 의미</span><span class="sxs-lookup"><span data-stu-id="37d54-167">Error codes and their meanings</span></span>

| <span data-ttu-id="37d54-168">오류 코드</span><span class="sxs-lookup"><span data-stu-id="37d54-168">Error Code</span></span> | <span data-ttu-id="37d54-169">의미</span><span class="sxs-lookup"><span data-stu-id="37d54-169">Meaning</span></span> | <span data-ttu-id="37d54-170">가능한 작업</span><span class="sxs-lookup"><span data-stu-id="37d54-170">Possible Action</span></span> |
| :---: | --- | --- |
| <span data-ttu-id="37d54-171">10</span><span class="sxs-lookup"><span data-stu-id="37d54-171">10</span></span> | <span data-ttu-id="37d54-172">VM이 OMS 작업 영역에 이미 연결됨</span><span class="sxs-lookup"><span data-stu-id="37d54-172">VM is already connected to an OMS workspace</span></span> | <span data-ttu-id="37d54-173">VM을 확장 스키마에 지정된 작업 영역에 연결하려면 공용 설정에서 stopOnMultipleConnections를 false로 설정하거나 이 속성을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-173">To connect the VM to the workspace specified in the extension schema, set stopOnMultipleConnections to false in public settings or remove this property.</span></span> <span data-ttu-id="37d54-174">이 VM은 연결된 각 작업 영역에 대해 한 번만 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-174">This VM gets billed once for each workspace it is connected to.</span></span> |
| <span data-ttu-id="37d54-175">11</span><span class="sxs-lookup"><span data-stu-id="37d54-175">11</span></span> | <span data-ttu-id="37d54-176">확장에 잘못된 구성이 제공됨</span><span class="sxs-lookup"><span data-stu-id="37d54-176">Invalid config provided to the extension</span></span> | <span data-ttu-id="37d54-177">이전 예제에 따라 배포에 필요한 모든 속성 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-177">Follow the preceding examples to set all property values necessary for deployment.</span></span> |
| <span data-ttu-id="37d54-178">12</span><span class="sxs-lookup"><span data-stu-id="37d54-178">12</span></span> | <span data-ttu-id="37d54-179">dpkg 패키지 관리자가 잠겨 있음</span><span class="sxs-lookup"><span data-stu-id="37d54-179">The dpkg package manager is locked</span></span> | <span data-ttu-id="37d54-180">컴퓨터의 모든 dpkg 업데이트 작업이 완료되었는지 확인하고 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-180">Make sure all dpkg update operations on the machine have finished and retry.</span></span> |
| <span data-ttu-id="37d54-181">20</span><span class="sxs-lookup"><span data-stu-id="37d54-181">20</span></span> | <span data-ttu-id="37d54-182">조기 호출 사용 설정</span><span class="sxs-lookup"><span data-stu-id="37d54-182">Enable called prematurely</span></span> | <span data-ttu-id="37d54-183">[Azure Linux 에이전트를 사용 가능한 최신 버전으로 업데이트](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent)합니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-183">[Update the Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) to the latest available version.</span></span> |
| <span data-ttu-id="37d54-184">51</span><span class="sxs-lookup"><span data-stu-id="37d54-184">51</span></span> | <span data-ttu-id="37d54-185">이 확장이 VM의 운영 체제에서 지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="37d54-185">This extension is not supported on the VM's operation system</span></span> | |
| <span data-ttu-id="37d54-186">55</span><span class="sxs-lookup"><span data-stu-id="37d54-186">55</span></span> | <span data-ttu-id="37d54-187">Microsoft Operations Management Suite 서비스에 연결할 수 없음</span><span class="sxs-lookup"><span data-stu-id="37d54-187">Cannot connect to the Microsoft Operations Management Suite service</span></span> | <span data-ttu-id="37d54-188">시스템에서 인터넷에 액세스할 수 있는지 또는 유효한 HTTP 프록시가 제공되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-188">Check that the system either has Internet access, or that a valid HTTP proxy has been provided.</span></span> <span data-ttu-id="37d54-189">또한 작업 영역 ID가 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-189">Additionally, check the correctness of the workspace ID.</span></span> |

<span data-ttu-id="37d54-190">추가 문제 해결 정보는 [MS-Agent-for-Linux 문제 해결 가이드](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-190">Additional troubleshooting information can be found on the [OMS-Agent-for-Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span></span>

### <a name="support"></a><span data-ttu-id="37d54-191">지원</span><span class="sxs-lookup"><span data-stu-id="37d54-191">Support</span></span>

<span data-ttu-id="37d54-192">이 문서의 어디에서든 도움이 필요한 경우 [MSDN Azure 및 Stack Overflow 포럼](https://azure.microsoft.com/en-us/support/forums/)에서 Azure 전문가에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-192">If you need more help at any point in this article, you can contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="37d54-193">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-193">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="37d54-194">[Azure 지원 사이트](https://azure.microsoft.com/en-us/support/options/)로 가서 지원 받기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="37d54-194">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="37d54-195">Azure 지원을 사용하는 방법에 대한 자세한 내용은 [Microsoft Azure 지원 FAQ](https://azure.microsoft.com/en-us/support/faq/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="37d54-195">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
