---
title: "가상 컴퓨터 확장 집합 템플릿에 대해 알아보기 | Microsoft Docs"
description: "가상 컴퓨터 확장 집합에 대한 실행 가능한 최소 확장 집합 템플릿을 만드는 방법 알아보기"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: 65f02c4675eb752dcc82e9a1d1c7f6c2c193fc32
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a><span data-ttu-id="27648-103">Virtual Machine Scale Sets 템플릿에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="27648-103">Learn about virtual machine scale set templates</span></span>
<span data-ttu-id="27648-104">[Azure Resource Manager 템플릿](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment)은 관련된 리소스 그룹을 배포하는 유용한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="27648-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way to deploy groups of related resources.</span></span> <span data-ttu-id="27648-105">이 자습서 시리즈에서는 실행 가능한 최소 확장 집합 템플릿을 만드는 방법과 이러한 템플릿을 다양한 시나리오에 맞게 수정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27648-105">This tutorial series shows how to create a minimum viable scale set template and how to modify this template to suit various scenarios.</span></span> <span data-ttu-id="27648-106">모든 예제는 [GitHub 리포지토리](https://github.com/gatneil/mvss)에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="27648-106">All examples come from this [GitHub repository](https://github.com/gatneil/mvss).</span></span> 

<span data-ttu-id="27648-107">이 템플릿은 간단하게 제작되었습니다.</span><span class="sxs-lookup"><span data-stu-id="27648-107">This template is intended to be simple.</span></span> <span data-ttu-id="27648-108">확장 집합 템플릿의 전체 예제를 보려면 [Azure 빠른 시작 템플릿 GitHub 리포지토리](https://github.com/Azure/azure-quickstart-templates)를 참조하고 문자열 `vmss`가 포함된 폴더를 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="27648-108">For more complete examples of scale set templates, see the [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) and search for folders that contain the string `vmss`.</span></span>

<span data-ttu-id="27648-109">템플릿 생성에 익숙한 경우 "다음 단계" 섹션으로 건너뛰어 템플릿을 수정하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27648-109">If you are already familiar with creating templates, you can skip to the "Next steps" section to see how to modify this template.</span></span>

## <a name="review-the-template"></a><span data-ttu-id="27648-110">템플릿 검토</span><span class="sxs-lookup"><span data-stu-id="27648-110">Review the template</span></span>

<span data-ttu-id="27648-111">GitHub를 사용하여 실행 가능한 최소 확장 집합 템플릿 [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json)을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-111">Use GitHub to review our minimum viable scale set template, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span></span>

<span data-ttu-id="27648-112">이 자습서에서는 diff(`git diff master minimum-viable-scale-set`)를 검토하여 실행 가능한 최소 확장 집합 템플릿을 하나씩 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="27648-112">In this tutorial, we examine the diff (`git diff master minimum-viable-scale-set`) to create the minimum viable scale set template piece by piece.</span></span>

## <a name="define-schema-and-contentversion"></a><span data-ttu-id="27648-113">$schema 및 contentVersion 정의</span><span class="sxs-lookup"><span data-stu-id="27648-113">Define $schema and contentVersion</span></span>
<span data-ttu-id="27648-114">먼저 템플릿에서 `$schema` 및 `contentVersion`을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-114">First, we define `$schema` and `contentVersion` in the template.</span></span> <span data-ttu-id="27648-115">`$schema` 요소는 템플릿 언어의 버전을 정의하고 Visual Studio 구문 강조 표시 및 유사한 유효성 검사 기능에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="27648-115">The `$schema` element defines the version of the template language and is used for Visual Studio syntax highlighting and similar validation features.</span></span> <span data-ttu-id="27648-116">`contentVersion` 요소는 Azure에 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27648-116">The `contentVersion` element is not used by Azure.</span></span> <span data-ttu-id="27648-117">대신 템플릿 버전을 추적하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27648-117">Instead, it helps you keep track of the template version.</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a><span data-ttu-id="27648-118">매개 변수 정의</span><span class="sxs-lookup"><span data-stu-id="27648-118">Define parameters</span></span>
<span data-ttu-id="27648-119">다음으로 두 개의 매개 변수인 `adminUsername` 및 `adminPassword`를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-119">Next, we define two parameters, `adminUsername` and `adminPassword`.</span></span> <span data-ttu-id="27648-120">매개 변수는 배포 시 사용자가 지정하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="27648-120">Parameters are values you specify at the time of deployment.</span></span> <span data-ttu-id="27648-121">`adminUsername` 매개 변수는 단순히 `string` 형식이지만 `adminPassword`가 비밀이기 때문에 `securestring` 형식을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-121">The `adminUsername` parameter is simply a `string` type, but because `adminPassword` is a secret, we give it type `securestring`.</span></span> <span data-ttu-id="27648-122">이러한 매개 변수는 나중에 확장 집합 구성에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="27648-122">Later, these parameters are passed into the scale set configuration.</span></span>

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a><span data-ttu-id="27648-123">변수 정의</span><span class="sxs-lookup"><span data-stu-id="27648-123">Define variables</span></span>
<span data-ttu-id="27648-124">Resource Manager 템플릿을 사용하여 나중에 템플릿에 사용할 변수를 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27648-124">Resource Manager templates also let you define variables to be used later in the template.</span></span> <span data-ttu-id="27648-125">여기 예제에서는 변수를 사용하지 않기 때문에 JSON 개체가 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27648-125">Our example doesn't use any variables, so we've left the JSON object empty.</span></span>

```json
  "variables": {},
```

## <a name="define-resources"></a><span data-ttu-id="27648-126">리소스 정의</span><span class="sxs-lookup"><span data-stu-id="27648-126">Define resources</span></span>
<span data-ttu-id="27648-127">다음은 템플릿의 리소스 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="27648-127">Next is the resources section of the template.</span></span> <span data-ttu-id="27648-128">여기에 실제 배포할 항목을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-128">Here, you define what you actually want to deploy.</span></span> <span data-ttu-id="27648-129">`parameters` 및 `variables`(JSON 개체)과 달리 `resources`는 JSON 개체의 JSON 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="27648-129">Unlike `parameters` and `variables` (which are JSON objects), `resources` is a JSON list of JSON objects.</span></span>

```json
   "resources": [
```

<span data-ttu-id="27648-130">모든 리소스에는 `type`, `name`, `apiVersion` 및 `location` 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-130">All resources require `type`, `name`, `apiVersion`, and `location` properties.</span></span> <span data-ttu-id="27648-131">이 예제의 첫 번째 리소스는 `Microsft.Network/virtualNetwork` 형식이고 이름은 `myVnet`이며 apiVersion은 `2016-03-30`입니다.</span><span class="sxs-lookup"><span data-stu-id="27648-131">This example's first resource has type `Microsft.Network/virtualNetwork`, name `myVnet`, and apiVersion `2016-03-30`.</span></span> <span data-ttu-id="27648-132">(리소스 형식에 대한 최신 API 버전을 찾으려면 [Azure REST API 설명서](https://docs.microsoft.com/rest/api/)를 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="27648-132">(To find the latest API version for a resource type, see the [Azure REST API documentation](https://docs.microsoft.com/rest/api/).)</span></span>

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a><span data-ttu-id="27648-133">위치 지정</span><span class="sxs-lookup"><span data-stu-id="27648-133">Specify location</span></span>
<span data-ttu-id="27648-134">가상 네트워크의 위치를 지정하려면 [Resource Manager 템플릿 함수](../azure-resource-manager/resource-group-template-functions.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-134">To specify the location for the virtual network, we use a [Resource Manager template function](../azure-resource-manager/resource-group-template-functions.md).</span></span> <span data-ttu-id="27648-135">이 함수는 `"[<template-function>]"`처럼 따옴표와 대괄호로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-135">This function must be enclosed in quotes and square brackets like this: `"[<template-function>]"`.</span></span> <span data-ttu-id="27648-136">이 경우에는 `resourceGroup` 함수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-136">In this case, we use the `resourceGroup` function.</span></span> <span data-ttu-id="27648-137">인수는 취하지 않고 이 배포가 배포될 리소스 그룹에 대한 메타데이터를 포함하는 JSON 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-137">It takes in no arguments and returns a JSON object with metadata about the resource group this deployment is being deployed to.</span></span> <span data-ttu-id="27648-138">리소스 그룹은 배포 시에 사용자가 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-138">The resource group is set by the user at the time of deployment.</span></span> <span data-ttu-id="27648-139">그런 후 `.location`으로 이 JSON 개체를 인덱싱하여 JSON 개체에서의 위치를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="27648-139">We then index into this JSON object with `.location` to get the location from the JSON object.</span></span>

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a><span data-ttu-id="27648-140">가상 네트워크 속성 지정</span><span class="sxs-lookup"><span data-stu-id="27648-140">Specify virtual network properties</span></span>
<span data-ttu-id="27648-141">각 Resource Manager 리소스에는 해당 리소스 관련 구성에 대한 자체 `properties` 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27648-141">Each Resource Manager resource has its own `properties` section for configurations specific to the resource.</span></span> <span data-ttu-id="27648-142">이 경우에는 가상 네트워크에 개인 IP 주소 범위 `10.0.0.0/16`을 사용하는 하나의 서브넷만 있도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-142">In this case, we specify that the virtual network should have one subnet using the private IP address range `10.0.0.0/16`.</span></span> <span data-ttu-id="27648-143">확장 집합은 항상 하나의 서브넷에 포함되며</span><span class="sxs-lookup"><span data-stu-id="27648-143">A scale set is always contained within one subnet.</span></span> <span data-ttu-id="27648-144">여러 서브넷에 걸쳐 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="27648-144">It cannot span subnets.</span></span>

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a><span data-ttu-id="27648-145">dependsOn 목록 추가</span><span class="sxs-lookup"><span data-stu-id="27648-145">Add dependsOn list</span></span>
<span data-ttu-id="27648-146">필수 `type`, `name`, `apiVersion`, `location` 속성 외에도 각 리소스는 선택적인 `dependsOn` 목록 문자열을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27648-146">In addition to the required `type`, `name`, `apiVersion`, and `location` properties, each resource can have an optional `dependsOn` list of strings.</span></span> <span data-ttu-id="27648-147">이 목록은 이 리소스를 배포하기 전에 이 배포의 다른 리소스가 완료해야 하는 것을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-147">This list specifies which other resources from this deployment must finish before deploying this resource.</span></span>

<span data-ttu-id="27648-148">이 경우 목록에 요소가 하나만 있으며 해당 요소는 이전 예제의 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="27648-148">In this case, there is only one element in the list, the virtual network from the previous example.</span></span> <span data-ttu-id="27648-149">VM을 만들려면 먼저 확장 집합에 네트워크가 있어야 하므로 이러한 종속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-149">We specify this dependency because the scale set needs the network to exist before creating any VMs.</span></span> <span data-ttu-id="27648-150">이러한 방식으로 확장 집합은 네트워크 속성에 이전에 지정된 IP 주소 범위의 개인 IP 주소를 이러한 VM에 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27648-150">This way, the scale set can give these VMs private IP addresses from the IP address range previously specified in the network properties.</span></span> <span data-ttu-id="27648-151">dependsOn 목록에 있는 각 문자열의 형식은 `<type>/<name>`입니다.</span><span class="sxs-lookup"><span data-stu-id="27648-151">The format of each string in the dependsOn list is `<type>/<name>`.</span></span> <span data-ttu-id="27648-152">가상 네트워크 리소스 정의에 이전에 사용된 것과 동일한 `type` 및 `name`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-152">Use the same `type` and `name` used previously in the virtual network resource definition.</span></span>

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a><span data-ttu-id="27648-153">확장 집합 속성 지정</span><span class="sxs-lookup"><span data-stu-id="27648-153">Specify scale set properties</span></span>
<span data-ttu-id="27648-154">확장 집합에는 VM을 사용자 지정하기 위한 속성이 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27648-154">Scale sets have many properties for customizing the VMs in the scale set.</span></span> <span data-ttu-id="27648-155">이러한 속성의 전체 목록은 [확장 집합 REST API 설명서](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27648-155">For a full list of these properties, see the [scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span></span> <span data-ttu-id="27648-156">이 자습서에서는 일반적으로 사용되는 몇 가지 속성만 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-156">For this tutorial, we will set only a few commonly used properties.</span></span>
### <a name="supply-vm-size-and-capacity"></a><span data-ttu-id="27648-157">VM 크기 및 용량 제공</span><span class="sxs-lookup"><span data-stu-id="27648-157">Supply VM size and capacity</span></span>
<span data-ttu-id="27648-158">확장 집합은 만들 VM의 크기("sku 이름") 및 이러한 크기로 만들려는 VM의 수("sku 용량")를 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-158">The scale set needs to know what size of VM to create ("sku name") and how many such VMs to create ("sku capacity").</span></span> <span data-ttu-id="27648-159">사용 가능한 VM 크기를 확인하려면 [VM 크기 설명서](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27648-159">To see which VM sizes are available, see the [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span></span>

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a><span data-ttu-id="27648-160">업데이트 유형 선택</span><span class="sxs-lookup"><span data-stu-id="27648-160">Choose type of updates</span></span>
<span data-ttu-id="27648-161">또한 확장 집합은 확장 집합의 업데이트 처리 방법을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-161">The scale set also needs to know how to handle updates on the scale set.</span></span> <span data-ttu-id="27648-162">현재 `Manual` 및 `Automatic`의 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27648-162">Currently, there are two options, `Manual` and `Automatic`.</span></span> <span data-ttu-id="27648-163">두 옵션 사이의 차이점에 대한 자세한 내용은 [확장 집합을 업그레이드하는 방법](./virtual-machine-scale-sets-upgrade-scale-set.md)에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27648-163">For more information on the differences between the two, see the documentation on [how to upgrade a scale set](./virtual-machine-scale-sets-upgrade-scale-set.md).</span></span>

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a><span data-ttu-id="27648-164">VM 운영 체제 선택</span><span class="sxs-lookup"><span data-stu-id="27648-164">Choose VM operating system</span></span>
<span data-ttu-id="27648-165">확장 집합은 VM에 적용할 운영 체제도 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-165">The scale set needs to know what operating system to put on the VMs.</span></span> <span data-ttu-id="27648-166">여기서는 완벽하게 패치된 Ubuntu 16.04 LTS 이미지를 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="27648-166">Here, we create the VMs with a fully patched Ubuntu 16.04-LTS image.</span></span>

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a><span data-ttu-id="27648-167">computerNamePrefix 지정</span><span class="sxs-lookup"><span data-stu-id="27648-167">Specify computerNamePrefix</span></span>
<span data-ttu-id="27648-168">확장 집합은 다수의 VM을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-168">The scale set deploys multiple VMs.</span></span> <span data-ttu-id="27648-169">각각의 VM 이름을 지정하는 대신 `computerNamePrefix`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-169">Instead of specifying each VM name, we specify `computerNamePrefix`.</span></span> <span data-ttu-id="27648-170">확장 집합은 각 VM의 접두사에 인덱스를 추가하기 때문에 VM 이름은 `<computerNamePrefix>_<auto-generated-index>` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="27648-170">The scale set appends an index to the prefix for each VM, so VM names have the form `<computerNamePrefix>_<auto-generated-index>`.</span></span>

<span data-ttu-id="27648-171">이 코드 조각에서는 이전 매개 변수를 사용하여 확장 집합의 모든 VM에 대한 관리자 사용자 이름 및 암호를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-171">In the following snippet, we use the parameters from before to set the administrator username and password for all VMs in the scale set.</span></span> <span data-ttu-id="27648-172">이 작업은 `parameters` 템플릿 함수를 사용하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-172">We do this with the `parameters` template function.</span></span> <span data-ttu-id="27648-173">이 함수는 참조할 매개 변수를 지정하는 문자열을 취하여 해당 매개 변수의 값을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-173">This function takes in a string that specifies which parameter to refer to and outputs the value for that parameter.</span></span>

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a><span data-ttu-id="27648-174">VM 네트워크 구성 지정</span><span class="sxs-lookup"><span data-stu-id="27648-174">Specify VM network configuration</span></span>
<span data-ttu-id="27648-175">마지막으로 확장 집합의 VM에 대한 네트워크 구성을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-175">Finally, we need to specify the network configuration for the VMs in the scale set.</span></span> <span data-ttu-id="27648-176">이 경우 이전에 만든 서브넷의 ID만 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27648-176">In this case, we only need to specify the ID of the subnet created earlier.</span></span> <span data-ttu-id="27648-177">이렇게 하면 확장 집합이 이 서브넷의 네트워크 인터페이스를 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="27648-177">This tells the scale set to put the network interfaces in this subnet.</span></span>

<span data-ttu-id="27648-178">`resourceId` 템플릿 함수를 사용하여 서브넷을 포함하는 가상 네트워크의 ID를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27648-178">You can get the ID of the virtual network containing the subnet by using the `resourceId` template function.</span></span> <span data-ttu-id="27648-179">이 함수는 리소스의 형식 및 이름을 취한 후 해당 리소스의 정규화된 식별자를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-179">This function takes in the type and name of a resource and returns the fully qualified identifier of that resource.</span></span> <span data-ttu-id="27648-180">이 ID는 `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="27648-180">This ID has the form: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span></span>

<span data-ttu-id="27648-181">그러나 가상 네트워크의 식별자로는 충분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27648-181">However, the identifier of the virtual network is not enough.</span></span> <span data-ttu-id="27648-182">확장 집합 VM이 위치할 구체적인 서브넷을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-182">You must specify the specific subnet that the scale set VMs should be in.</span></span> <span data-ttu-id="27648-183">이 작업을 수행하려면 `/subnets/mySubnet`을 가상 네트워크의 ID에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-183">To do this, concatenate `/subnets/mySubnet` to the ID of the virtual network.</span></span> <span data-ttu-id="27648-184">결과는 서브넷의 정규화된 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="27648-184">The result is the fully qualified ID of the subnet.</span></span> <span data-ttu-id="27648-185">이 연결은 일련의 문자열을 취한 후 해당 연결을 반환하는 `concat` 함수를 사용하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="27648-185">Do this concatenation with the `concat` function, which takes in a series of strings and returns their concatenation.</span></span>

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a><span data-ttu-id="27648-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="27648-186">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
