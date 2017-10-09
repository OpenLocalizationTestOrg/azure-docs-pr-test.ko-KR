---
title: "Linux 용 Azure 가상 컴퓨터 확장 aaaOMS | Microsoft Docs"
description: "가상 컴퓨터 확장을 사용 하 여 Linux 가상 컴퓨터에 hello OMS 에이전트를 배포 합니다."
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
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a><span data-ttu-id="3af53-103">Linux용 OMS 가상 컴퓨터 확장</span><span class="sxs-lookup"><span data-stu-id="3af53-103">OMS virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="3af53-104">개요</span><span class="sxs-lookup"><span data-stu-id="3af53-104">Overview</span></span>

<span data-ttu-id="3af53-105">OMS(Operations Management Suite)는 클라우드와 온-프레미스 자산에서 모니터링, 경고 및 경고 수정 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-105">Operations Management Suite (OMS) provides monitoring, alerting, and alert remediation capabilities across cloud and on-premises assets.</span></span> <span data-ttu-id="3af53-106">Linux 용 OMS 에이전트 가상 컴퓨터 확장 hello 게시 되 고 Microsoft에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-106">hello OMS Agent virtual machine extension for Linux is published and supported by Microsoft.</span></span> <span data-ttu-id="3af53-107">Azure 가상 컴퓨터에 hello OMS 에이전트를 설치 하 고 기존 OMS 작업 영역에 가상 컴퓨터를 등록 하는 hello 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-107">hello extension installs hello OMS agent on Azure virtual machines, and enrolls virtual machines into an existing OMS workspace.</span></span> <span data-ttu-id="3af53-108">이 문서 정보 hello Linux 용 OMS 가상 컴퓨터 확장 hello에 대 한 플랫폼, 구성 및 배포 옵션을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-108">This document details hello supported platforms, configurations, and deployment options for hello OMS virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3af53-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="3af53-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="3af53-110">운영 체제</span><span class="sxs-lookup"><span data-stu-id="3af53-110">Operating system</span></span>

<span data-ttu-id="3af53-111">OMS 에이전트 확장 hello 이러한 Linux 배포에 대해 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-111">hello OMS Agent extension can be run against these Linux distributions.</span></span>

| <span data-ttu-id="3af53-112">배포</span><span class="sxs-lookup"><span data-stu-id="3af53-112">Distribution</span></span> | <span data-ttu-id="3af53-113">버전</span><span class="sxs-lookup"><span data-stu-id="3af53-113">Version</span></span> |
|---|---|
| <span data-ttu-id="3af53-114">CentOS Linux</span><span class="sxs-lookup"><span data-stu-id="3af53-114">CentOS Linux</span></span> | <span data-ttu-id="3af53-115">5, 6 및 7</span><span class="sxs-lookup"><span data-stu-id="3af53-115">5, 6, and 7</span></span> |
| <span data-ttu-id="3af53-116">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="3af53-116">Oracle Linux</span></span> | <span data-ttu-id="3af53-117">5, 6 및 7</span><span class="sxs-lookup"><span data-stu-id="3af53-117">5, 6, and 7</span></span> |
| <span data-ttu-id="3af53-118">Red Hat Enterprise Linux Server</span><span class="sxs-lookup"><span data-stu-id="3af53-118">Red Hat Enterprise Linux Server</span></span> | <span data-ttu-id="3af53-119">5, 6 및 7</span><span class="sxs-lookup"><span data-stu-id="3af53-119">5, 6 and 7</span></span> |
| <span data-ttu-id="3af53-120">Debian GNU/Linux</span><span class="sxs-lookup"><span data-stu-id="3af53-120">Debian GNU/Linux</span></span> | <span data-ttu-id="3af53-121">6, 7 및 8</span><span class="sxs-lookup"><span data-stu-id="3af53-121">6, 7, and 8</span></span> |
| <span data-ttu-id="3af53-122">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="3af53-122">Ubuntu</span></span> | <span data-ttu-id="3af53-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="3af53-123">12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS</span></span> |
| <span data-ttu-id="3af53-124">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="3af53-124">SUSE Linux Enterprise Server</span></span> | <span data-ttu-id="3af53-125">11 및 12</span><span class="sxs-lookup"><span data-stu-id="3af53-125">11 and 12</span></span> |

### <a name="internet-connectivity"></a><span data-ttu-id="3af53-126">인터넷 연결</span><span class="sxs-lookup"><span data-stu-id="3af53-126">Internet connectivity</span></span>

<span data-ttu-id="3af53-127">Linux 용 OMS 에이전트 확장 hello hello 대상 가상 컴퓨터는 연결 된 toohello 필요 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-127">hello OMS Agent extension for Linux requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="3af53-128">확장 스키마</span><span class="sxs-lookup"><span data-stu-id="3af53-128">Extension schema</span></span>

<span data-ttu-id="3af53-129">hello 다음 JSON 스키마를 보여 줍니다 hello hello OMS 에이전트 확장에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-129">hello following JSON shows hello schema for hello OMS Agent extension.</span></span> <span data-ttu-id="3af53-130">hello 확장 hello 대상 OMS 작업 영역;에서 hello 작업 영역 ID와 작업 영역 키 필요 hello OMS 포털에서 이러한 값을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-130">hello extension requires hello workspace ID and workspace key from hello target OMS workspace; these values can be found in hello OMS portal.</span></span> <span data-ttu-id="3af53-131">중요 한 데이터로 처리 되어야 hello 작업 영역 키를 보호 설정 구성에 저장 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-131">Because hello workspace key should be treated as sensitive data, it should be stored in a protected setting configuration.</span></span> <span data-ttu-id="3af53-132">Azure VM 확장으로 보호 된 데이터를 설정 하는 암호화 되 고 hello 대상 가상 컴퓨터에 암호를 해독할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-132">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span> <span data-ttu-id="3af53-133">**workspaceId** 및 **workspaceKey**는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-133">Note that **workspaceId** and **workspaceKey** are case-sensitive.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="3af53-134">속성 값</span><span class="sxs-lookup"><span data-stu-id="3af53-134">Property values</span></span>

| <span data-ttu-id="3af53-135">이름</span><span class="sxs-lookup"><span data-stu-id="3af53-135">Name</span></span> | <span data-ttu-id="3af53-136">값/예제</span><span class="sxs-lookup"><span data-stu-id="3af53-136">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="3af53-137">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3af53-137">apiVersion</span></span> | <span data-ttu-id="3af53-138">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="3af53-138">2015-06-15</span></span> |
| <span data-ttu-id="3af53-139">publisher</span><span class="sxs-lookup"><span data-stu-id="3af53-139">publisher</span></span> | <span data-ttu-id="3af53-140">Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="3af53-140">Microsoft.EnterpriseCloud.Monitoring</span></span> |
| <span data-ttu-id="3af53-141">type</span><span class="sxs-lookup"><span data-stu-id="3af53-141">type</span></span> | <span data-ttu-id="3af53-142">OmsAgentForLinux</span><span class="sxs-lookup"><span data-stu-id="3af53-142">OmsAgentForLinux</span></span> |
| <span data-ttu-id="3af53-143">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="3af53-143">typeHandlerVersion</span></span> | <span data-ttu-id="3af53-144">1.4</span><span class="sxs-lookup"><span data-stu-id="3af53-144">1.4</span></span> |
| <span data-ttu-id="3af53-145">workspaceId(예)</span><span class="sxs-lookup"><span data-stu-id="3af53-145">workspaceId (e.g)</span></span> | <span data-ttu-id="3af53-146">6f680a37-00c6-41c7-a93f-1437e3462574</span><span class="sxs-lookup"><span data-stu-id="3af53-146">6f680a37-00c6-41c7-a93f-1437e3462574</span></span> |
| <span data-ttu-id="3af53-147">workspaceKey(예)</span><span class="sxs-lookup"><span data-stu-id="3af53-147">workspaceKey (e.g)</span></span> | <span data-ttu-id="3af53-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span><span class="sxs-lookup"><span data-stu-id="3af53-148">z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ==</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="3af53-149">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="3af53-149">Template deployment</span></span>

<span data-ttu-id="3af53-150">Azure Resource Manager 템플릿을 사용하여 Azure VM 확장을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-150">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="3af53-151">서식 파일은 온 보 딩 tooOMS 같은 구성 된 후 배포 해야 하는 하나 이상의 가상 컴퓨터를 배포 하는 경우에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-151">Templates are ideal when deploying one or more virtual machines that require post deployment configuration such as onboarding tooOMS.</span></span> <span data-ttu-id="3af53-152">Hello에 hello OMS 에이전트 VM 확장을 포함 하는 샘플 리소스 관리자 템플릿이 있습니다 [Azure 빠른 시작 갤러리](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm)합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-152">A sample Resource Manager template that includes hello OMS Agent VM extension can be found on hello [Azure Quick Start Gallery](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm).</span></span> 

<span data-ttu-id="3af53-153">가상 컴퓨터 확장에 대 한 hello JSON 구성 hello 가상 컴퓨터 리소스 내에 중첩 된 또는 hello 루트 또는 리소스 관리자 JSON 서식 파일의 최상위 수준에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-153">hello JSON configuration for a virtual machine extension can be nested inside hello virtual machine resource, or placed at hello root or top level of a Resource Manager JSON template.</span></span> <span data-ttu-id="3af53-154">hello JSON 구성의 배치 hello hello 리소스 이름 및 형식을의 hello 값을 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-154">hello placement of hello JSON configuration affects hello value of hello resource name and type.</span></span> <span data-ttu-id="3af53-155">자세한 내용은 [자식 리소스의 이름 및 형식 설정](../../azure-resource-manager/resource-manager-template-child-resource.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3af53-155">For more information, see [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md).</span></span> 

<span data-ttu-id="3af53-156">hello 다음 예에서는 가정 hello OMS 확장 hello 가상 컴퓨터 리소스 내에 중첩 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-156">hello following example assumes hello OMS extension is nested inside hello virtual machine resource.</span></span> <span data-ttu-id="3af53-157">Hello JSON hello에 위치한 hello 확장을 리소스를 중첩할 때 `"resources": []` hello 가상 컴퓨터의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-157">When nesting hello extension resource, hello JSON is placed in hello `"resources": []` object of hello virtual machine.</span></span>

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

<span data-ttu-id="3af53-158">Hello 서식 파일의 루트 hello에 hello 확장 JSON를 배치할 때 참조 toohello 부모 가상 컴퓨터를 포함 하는 hello 리소스 이름 및 hello 유형은 hello 중첩 된 구성에 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-158">When placing hello extension JSON at hello root of hello template, hello resource name includes a reference toohello parent virtual machine, and hello type reflects hello nested configuration.</span></span>  

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

## <a name="azure-cli-deployment"></a><span data-ttu-id="3af53-159">Azure CLI 배포</span><span class="sxs-lookup"><span data-stu-id="3af53-159">Azure CLI deployment</span></span>

<span data-ttu-id="3af53-160">hello Azure CLI 사용된 toodeploy hello OMS 에이전트 VM 확장 tooan 기존 가상 컴퓨터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-160">hello Azure CLI can be used toodeploy hello OMS Agent VM extension tooan existing virtual machine.</span></span> <span data-ttu-id="3af53-161">OMS 작업 영역에서 설정과 hello OMS 키와 OMS ID를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-161">Replace hello OMS key and OMS ID with those from your OMS workspace.</span></span> 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="3af53-162">문제 해결 및 지원</span><span class="sxs-lookup"><span data-stu-id="3af53-162">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="3af53-163">문제 해결</span><span class="sxs-lookup"><span data-stu-id="3af53-163">Troubleshoot</span></span>

<span data-ttu-id="3af53-164">Hello Azure 포털에서에서 하 고 hello Azure CLI를 사용 하 여 확장 배포의 hello 상태에 대 한 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-164">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="3af53-165">hello 명령을 사용 하 여 다음을 실행 하는 특정된 VM에 대 한 확장의 toosee hello 배포 상태 hello Azure CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-165">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="3af53-166">확장 실행은 기록된 toohello 다음 파일을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-166">Extension execution output is logged toohello following file:</span></span>

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a><span data-ttu-id="3af53-167">오류 코드 및 해당 의미</span><span class="sxs-lookup"><span data-stu-id="3af53-167">Error codes and their meanings</span></span>

| <span data-ttu-id="3af53-168">오류 코드</span><span class="sxs-lookup"><span data-stu-id="3af53-168">Error Code</span></span> | <span data-ttu-id="3af53-169">의미</span><span class="sxs-lookup"><span data-stu-id="3af53-169">Meaning</span></span> | <span data-ttu-id="3af53-170">가능한 작업</span><span class="sxs-lookup"><span data-stu-id="3af53-170">Possible Action</span></span> |
| :---: | --- | --- |
| <span data-ttu-id="3af53-171">10</span><span class="sxs-lookup"><span data-stu-id="3af53-171">10</span></span> | <span data-ttu-id="3af53-172">VM이 이미 연결 된 tooan OMS 작업 영역</span><span class="sxs-lookup"><span data-stu-id="3af53-172">VM is already connected tooan OMS workspace</span></span> | <span data-ttu-id="3af53-173">tooconnect hello VM toohello 작업 영역 hello 확장 스키마에 지정 된 stopOnMultipleConnections toofalse 공용 설정에서 설정 하거나이 속성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-173">tooconnect hello VM toohello workspace specified in hello extension schema, set stopOnMultipleConnections toofalse in public settings or remove this property.</span></span> <span data-ttu-id="3af53-174">이 VM은 연결된 각 작업 영역에 대해 한 번만 비용이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-174">This VM gets billed once for each workspace it is connected to.</span></span> |
| <span data-ttu-id="3af53-175">11</span><span class="sxs-lookup"><span data-stu-id="3af53-175">11</span></span> | <span data-ttu-id="3af53-176">제공 된 잘못 된 구성 toohello 확장</span><span class="sxs-lookup"><span data-stu-id="3af53-176">Invalid config provided toohello extension</span></span> | <span data-ttu-id="3af53-177">Hello 앞 예제 tooset 배포에 필요한 모든 속성 값을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-177">Follow hello preceding examples tooset all property values necessary for deployment.</span></span> |
| <span data-ttu-id="3af53-178">12</span><span class="sxs-lookup"><span data-stu-id="3af53-178">12</span></span> | <span data-ttu-id="3af53-179">hello dpkg 패키지 관리자 잠겨 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-179">hello dpkg package manager is locked</span></span> | <span data-ttu-id="3af53-180">모든 dpkg 업데이트 작업이 hello 컴퓨터에서 완료 하 고 다시 시도 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3af53-180">Make sure all dpkg update operations on hello machine have finished and retry.</span></span> |
| <span data-ttu-id="3af53-181">20</span><span class="sxs-lookup"><span data-stu-id="3af53-181">20</span></span> | <span data-ttu-id="3af53-182">조기 호출 사용 설정</span><span class="sxs-lookup"><span data-stu-id="3af53-182">Enable called prematurely</span></span> | <span data-ttu-id="3af53-183">[Azure Linux 에이전트 업데이트 hello](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello 사용 가능한 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-183">[Update hello Azure Linux Agent](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello latest available version.</span></span> |
| <span data-ttu-id="3af53-184">51</span><span class="sxs-lookup"><span data-stu-id="3af53-184">51</span></span> | <span data-ttu-id="3af53-185">이 확장 hello VM의 운영 체제에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-185">This extension is not supported on hello VM's operation system</span></span> | |
| <span data-ttu-id="3af53-186">55</span><span class="sxs-lookup"><span data-stu-id="3af53-186">55</span></span> | <span data-ttu-id="3af53-187">Toohello Microsoft Operations Management Suite 서비스에 연결할 수 없음</span><span class="sxs-lookup"><span data-stu-id="3af53-187">Cannot connect toohello Microsoft Operations Management Suite service</span></span> | <span data-ttu-id="3af53-188">인터넷 액세스 또는 올바른 HTTP 프록시가 제공 된다는 것 hello 시스템 중 하나에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-188">Check that hello system either has Internet access, or that a valid HTTP proxy has been provided.</span></span> <span data-ttu-id="3af53-189">또한 hello 작업 영역 ID의 hello 정확성을 확인</span><span class="sxs-lookup"><span data-stu-id="3af53-189">Additionally, check hello correctness of hello workspace ID.</span></span> |

<span data-ttu-id="3af53-190">Hello에서 추가 문제 해결 정보를 확인할 수 있습니다 [Linux에 대 한 OMS 에이전트 문제 해결 가이드](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#)합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-190">Additional troubleshooting information can be found on hello [OMS-Agent-for-Linux Troubleshooting Guide](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).</span></span>

### <a name="support"></a><span data-ttu-id="3af53-191">지원</span><span class="sxs-lookup"><span data-stu-id="3af53-191">Support</span></span>

<span data-ttu-id="3af53-192">이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다 Azure 전문가의 hello hello [MSDN Azure 및 스택 오버플로 포럼](https://azure.microsoft.com/en-us/support/forums/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-192">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="3af53-193">또는 Azure 기술 지원 인시던트를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-193">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="3af53-194">Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/en-us/support/options/) 지원 받기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-194">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="3af53-195">Azure 지원을 사용 하는 방법에 대 한 내용은 하세요 hello [Microsoft Azure 지원 FAQ](https://azure.microsoft.com/en-us/support/faq/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3af53-195">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
