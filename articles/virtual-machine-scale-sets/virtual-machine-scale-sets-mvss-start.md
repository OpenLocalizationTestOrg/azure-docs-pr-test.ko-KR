---
title: "가상 컴퓨터 크기에 대 한 aaaLearn 템플릿을 설정할 | Microsoft Docs"
description: "최소 실행 가능한 소수 자릿수 toocreate 가상 컴퓨터 크기 집합에 대 한 템플릿을 설정에 대해 알아봅니다"
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
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a><span data-ttu-id="9677d-103">Virtual Machine Scale Sets 템플릿에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="9677d-103">Learn about virtual machine scale set templates</span></span>
<span data-ttu-id="9677d-104">[Azure 리소스 관리자 템플릿](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) 은 훌륭한 방법 toodeploy 관련된 리소스의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="9677d-105">이 자습서 시리즈 표시 하 고 최소 실행 가능한 소수 자릿수 toocreate 템플릿을 설정 하는 방법 toomodify이 서식 파일 toosuit 다양 한 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-105">This tutorial series shows how toocreate a minimum viable scale set template and how toomodify this template toosuit various scenarios.</span></span> <span data-ttu-id="9677d-106">모든 예제는 [GitHub 리포지토리](https://github.com/gatneil/mvss)에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-106">All examples come from this [GitHub repository](https://github.com/gatneil/mvss).</span></span> 

<span data-ttu-id="9677d-107">이 서식 파일은 의도 한 toobe 단순 합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-107">This template is intended toobe simple.</span></span> <span data-ttu-id="9677d-108">눈금의 완전 한 예제에 대 한 템플릿 설정, hello 참조 [Azure 빠른 시작 템플릿 GitHub 리포지토리](https://github.com/Azure/azure-quickstart-templates) hello 문자열이 포함 된 폴더에 대 한 검색 `vmss`합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-108">For more complete examples of scale set templates, see hello [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) and search for folders that contain hello string `vmss`.</span></span>

<span data-ttu-id="9677d-109">"다음 단계" 섹션 toosee toohello을 어떻게 건너뛸 수 이미 템플릿 만들기에 대해 잘 알고 있다면 toomodify이 서식이 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-109">If you are already familiar with creating templates, you can skip toohello "Next steps" section toosee how toomodify this template.</span></span>

## <a name="review-hello-template"></a><span data-ttu-id="9677d-110">검토 hello 템플릿</span><span class="sxs-lookup"><span data-stu-id="9677d-110">Review hello template</span></span>

<span data-ttu-id="9677d-111">GitHub를 사용 하 여 tooreview 우리의 최소 실행 가능한 크기 집합 템플릿을 [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-111">Use GitHub tooreview our minimum viable scale set template, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span></span>

<span data-ttu-id="9677d-112">이 자습서에서는 hello diff 살펴보겠습니다 (`git diff master minimum-viable-scale-set`) toocreate hello 최소 실행 가능한 크기 집합 템플릿 하나씩 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-112">In this tutorial, we examine hello diff (`git diff master minimum-viable-scale-set`) toocreate hello minimum viable scale set template piece by piece.</span></span>

## <a name="define-schema-and-contentversion"></a><span data-ttu-id="9677d-113">$schema 및 contentVersion 정의</span><span class="sxs-lookup"><span data-stu-id="9677d-113">Define $schema and contentVersion</span></span>
<span data-ttu-id="9677d-114">첫째, 정의 `$schema` 및 `contentVersion` hello 서식 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-114">First, we define `$schema` and `contentVersion` in hello template.</span></span> <span data-ttu-id="9677d-115">hello `$schema` 요소 hello 버전의 hello 템플릿 언어를 정의 하 고 Visual Studio 구문 강조 표시와 비슷한 유효성 검사 기능에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-115">hello `$schema` element defines hello version of hello template language and is used for Visual Studio syntax highlighting and similar validation features.</span></span> <span data-ttu-id="9677d-116">hello `contentVersion` 요소가 Azure에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-116">hello `contentVersion` element is not used by Azure.</span></span> <span data-ttu-id="9677d-117">대신, 수 hello 템플릿 버전을 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-117">Instead, it helps you keep track of hello template version.</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a><span data-ttu-id="9677d-118">매개 변수 정의</span><span class="sxs-lookup"><span data-stu-id="9677d-118">Define parameters</span></span>
<span data-ttu-id="9677d-119">다음으로 두 개의 매개 변수인 `adminUsername` 및 `adminPassword`를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-119">Next, we define two parameters, `adminUsername` and `adminPassword`.</span></span> <span data-ttu-id="9677d-120">매개 변수는 배포의 hello 시 지정 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-120">Parameters are values you specify at hello time of deployment.</span></span> <span data-ttu-id="9677d-121">hello `adminUsername` 매개 변수는 단순히는 `string` 형식 때문에 `adminPassword` 는 암호로 형식 지정에서는 `securestring`합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-121">hello `adminUsername` parameter is simply a `string` type, but because `adminPassword` is a secret, we give it type `securestring`.</span></span> <span data-ttu-id="9677d-122">이상에서는 이러한 매개 변수 hello 배율 구성 설정에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-122">Later, these parameters are passed into hello scale set configuration.</span></span>

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
## <a name="define-variables"></a><span data-ttu-id="9677d-123">변수 정의</span><span class="sxs-lookup"><span data-stu-id="9677d-123">Define variables</span></span>
<span data-ttu-id="9677d-124">또한 리소스 관리자 템플릿을 사용 하 hello 서식 파일의 뒷부분에 나오는 사용 되는 변수 toobe 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-124">Resource Manager templates also let you define variables toobe used later in hello template.</span></span> <span data-ttu-id="9677d-125">예에서 사용 하는 hello JSON 개체를 빈 두었으며 하므로 모든 변수를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-125">Our example doesn't use any variables, so we've left hello JSON object empty.</span></span>

```json
  "variables": {},
```

## <a name="define-resources"></a><span data-ttu-id="9677d-126">리소스 정의</span><span class="sxs-lookup"><span data-stu-id="9677d-126">Define resources</span></span>
<span data-ttu-id="9677d-127">다음은 hello 템플릿의 리소스 섹션 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-127">Next is hello resources section of hello template.</span></span> <span data-ttu-id="9677d-128">실제로 수행할 동작을 정의 여기서 toodeploy 합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-128">Here, you define what you actually want toodeploy.</span></span> <span data-ttu-id="9677d-129">`parameters` 및 `variables`(JSON 개체)과 달리 `resources`는 JSON 개체의 JSON 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-129">Unlike `parameters` and `variables` (which are JSON objects), `resources` is a JSON list of JSON objects.</span></span>

```json
   "resources": [
```

<span data-ttu-id="9677d-130">모든 리소스에는 `type`, `name`, `apiVersion` 및 `location` 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-130">All resources require `type`, `name`, `apiVersion`, and `location` properties.</span></span> <span data-ttu-id="9677d-131">이 예제의 첫 번째 리소스는 `Microsft.Network/virtualNetwork` 형식이고 이름은 `myVnet`이며 apiVersion은 `2016-03-30`입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-131">This example's first resource has type `Microsft.Network/virtualNetwork`, name `myVnet`, and apiVersion `2016-03-30`.</span></span> <span data-ttu-id="9677d-132">(리소스 유형에 대 한 toofind hello 최신 API 버전 참조 hello [Azure REST API 설명서](https://docs.microsoft.com/rest/api/).)</span><span class="sxs-lookup"><span data-stu-id="9677d-132">(toofind hello latest API version for a resource type, see hello [Azure REST API documentation](https://docs.microsoft.com/rest/api/).)</span></span>

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a><span data-ttu-id="9677d-133">위치 지정</span><span class="sxs-lookup"><span data-stu-id="9677d-133">Specify location</span></span>
<span data-ttu-id="9677d-134">hello 가상 네트워크에 대 한 toospecify hello 위치를 사용 하 여 한 [리소스 관리자 템플릿 함수](../azure-resource-manager/resource-group-template-functions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-134">toospecify hello location for hello virtual network, we use a [Resource Manager template function](../azure-resource-manager/resource-group-template-functions.md).</span></span> <span data-ttu-id="9677d-135">이 함수는 `"[<template-function>]"`처럼 따옴표와 대괄호로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-135">This function must be enclosed in quotes and square brackets like this: `"[<template-function>]"`.</span></span> <span data-ttu-id="9677d-136">이 경우 hello 사용 `resourceGroup` 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-136">In this case, we use hello `resourceGroup` function.</span></span> <span data-ttu-id="9677d-137">인수를 사용 하 고이 배포를 배포 하 고 hello 리소스 그룹에 대 한 메타 데이터와 JSON 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-137">It takes in no arguments and returns a JSON object with metadata about hello resource group this deployment is being deployed to.</span></span> <span data-ttu-id="9677d-138">hello 리소스 그룹 배포의 hello 시 hello 사용자에 의해 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-138">hello resource group is set by hello user at hello time of deployment.</span></span> <span data-ttu-id="9677d-139">에서는 다음이 JSON 개체의 인덱스 `.location` hello JSON 개체에서 tooget hello 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-139">We then index into this JSON object with `.location` tooget hello location from hello JSON object.</span></span>

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a><span data-ttu-id="9677d-140">가상 네트워크 속성 지정</span><span class="sxs-lookup"><span data-stu-id="9677d-140">Specify virtual network properties</span></span>
<span data-ttu-id="9677d-141">각 리소스 관리자 리소스에는 자체 `properties` 구성 toohello 특정 리소스에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="9677d-141">Each Resource Manager resource has its own `properties` section for configurations specific toohello resource.</span></span> <span data-ttu-id="9677d-142">이 경우 해당 hello 가상 네트워크 hello 개인 IP 주소 범위를 사용 하는 서브넷 1 개 있어야 합니다. 지정 म `10.0.0.0/16`합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-142">In this case, we specify that hello virtual network should have one subnet using hello private IP address range `10.0.0.0/16`.</span></span> <span data-ttu-id="9677d-143">확장 집합은 항상 하나의 서브넷에 포함되며</span><span class="sxs-lookup"><span data-stu-id="9677d-143">A scale set is always contained within one subnet.</span></span> <span data-ttu-id="9677d-144">여러 서브넷에 걸쳐 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-144">It cannot span subnets.</span></span>

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

## <a name="add-dependson-list"></a><span data-ttu-id="9677d-145">dependsOn 목록 추가</span><span class="sxs-lookup"><span data-stu-id="9677d-145">Add dependsOn list</span></span>
<span data-ttu-id="9677d-146">또한 toohello 필요한 `type`, `name`, `apiVersion`, 및 `location` 속성, 각 리소스를 선택적 가질 수 있습니다 `dependsOn` 문자열의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-146">In addition toohello required `type`, `name`, `apiVersion`, and `location` properties, each resource can have an optional `dependsOn` list of strings.</span></span> <span data-ttu-id="9677d-147">이 목록은 이 리소스를 배포하기 전에 이 배포의 다른 리소스가 완료해야 하는 것을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-147">This list specifies which other resources from this deployment must finish before deploying this resource.</span></span>

<span data-ttu-id="9677d-148">이 경우 hello 이전 예제에서 가상 네트워크의 hello hello 목록의 요소가 하나 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-148">In this case, there is only one element in hello list, hello virtual network from hello previous example.</span></span> <span data-ttu-id="9677d-149">이 종속성 hello 크기 집합 필요 hello 네트워크 tooexist Vm을 만들기 전에 때문에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-149">We specify this dependency because hello scale set needs hello network tooexist before creating any VMs.</span></span> <span data-ttu-id="9677d-150">이러한 방식으로 hello 크기 집합 hello 네트워크 속성에 지정 된 이전 hello IP 주소 범위에서 이러한 Vm 개인 IP 주소를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-150">This way, hello scale set can give these VMs private IP addresses from hello IP address range previously specified in hello network properties.</span></span> <span data-ttu-id="9677d-151">hello hello dependsOn 목록의 각 문자열의 형식이 `<type>/<name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-151">hello format of each string in hello dependsOn list is `<type>/<name>`.</span></span> <span data-ttu-id="9677d-152">사용 하 여 hello 동일 `type` 및 `name` hello 가상 네트워크 리소스 정의에서 이전에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-152">Use hello same `type` and `name` used previously in hello virtual network resource definition.</span></span>

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
## <a name="specify-scale-set-properties"></a><span data-ttu-id="9677d-153">확장 집합 속성 지정</span><span class="sxs-lookup"><span data-stu-id="9677d-153">Specify scale set properties</span></span>
<span data-ttu-id="9677d-154">크기 집합은 hello Vm 크기 집합 hello에에서 사용자 지정 하기 위한 많은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-154">Scale sets have many properties for customizing hello VMs in hello scale set.</span></span> <span data-ttu-id="9677d-155">이러한 속성 목록은 전체 참조 hello [크기 REST API 설명서 집합](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set)합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-155">For a full list of these properties, see hello [scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span></span> <span data-ttu-id="9677d-156">이 자습서에서는 일반적으로 사용되는 몇 가지 속성만 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-156">For this tutorial, we will set only a few commonly used properties.</span></span>
### <a name="supply-vm-size-and-capacity"></a><span data-ttu-id="9677d-157">VM 크기 및 용량 제공</span><span class="sxs-lookup"><span data-stu-id="9677d-157">Supply VM size and capacity</span></span>
<span data-ttu-id="9677d-158">hello 눈금 VM toocreate ("sku 이름")의 크기 및 이러한 개수 Vm toocreate ("sku 용량") 요구 tooknow를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-158">hello scale set needs tooknow what size of VM toocreate ("sku name") and how many such VMs toocreate ("sku capacity").</span></span> <span data-ttu-id="9677d-159">어떤 VM 크기를 사용할 수 있는 toosee hello 참조 [VM 크기 설명서](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes)합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-159">toosee which VM sizes are available, see hello [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span></span>

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a><span data-ttu-id="9677d-160">업데이트 유형 선택</span><span class="sxs-lookup"><span data-stu-id="9677d-160">Choose type of updates</span></span>
<span data-ttu-id="9677d-161">hello 크기 집합에는 또한 toohandle hello 크기 집합에 업데이트 하는 방식 tooknow가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-161">hello scale set also needs tooknow how toohandle updates on hello scale set.</span></span> <span data-ttu-id="9677d-162">현재 `Manual` 및 `Automatic`의 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-162">Currently, there are two options, `Manual` and `Automatic`.</span></span> <span data-ttu-id="9677d-163">Hello 두 hello 차이에 대 한 자세한 내용은 hello 설명서를 참조 [배율 설정 하는 tooupgrade 방법을](./virtual-machine-scale-sets-upgrade-scale-set.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-163">For more information on hello differences between hello two, see hello documentation on [how tooupgrade a scale set](./virtual-machine-scale-sets-upgrade-scale-set.md).</span></span>

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a><span data-ttu-id="9677d-164">VM 운영 체제 선택</span><span class="sxs-lookup"><span data-stu-id="9677d-164">Choose VM operating system</span></span>
<span data-ttu-id="9677d-165">hello 크기 조정 요구 tooknow 어떤 운영 체제 tooput hello Vm에서 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-165">hello scale set needs tooknow what operating system tooput on hello VMs.</span></span> <span data-ttu-id="9677d-166">여기에서 완전히 패치 Ubuntu LTS 16.04 이미지로 hello Vm 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-166">Here, we create hello VMs with a fully patched Ubuntu 16.04-LTS image.</span></span>

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

### <a name="specify-computernameprefix"></a><span data-ttu-id="9677d-167">computerNamePrefix 지정</span><span class="sxs-lookup"><span data-stu-id="9677d-167">Specify computerNamePrefix</span></span>
<span data-ttu-id="9677d-168">hello 크기 집합 여러 Vm을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-168">hello scale set deploys multiple VMs.</span></span> <span data-ttu-id="9677d-169">각각의 VM 이름을 지정하는 대신 `computerNamePrefix`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-169">Instead of specifying each VM name, we specify `computerNamePrefix`.</span></span> <span data-ttu-id="9677d-170">hello 크기 집합 추가 인덱스 toohello 접두사 각 VM에 대 한 VM 이름 hello 형식으로 되어 있으므로 `<computerNamePrefix>_<auto-generated-index>`합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-170">hello scale set appends an index toohello prefix for each VM, so VM names have hello form `<computerNamePrefix>_<auto-generated-index>`.</span></span>

<span data-ttu-id="9677d-171">다음 코드 조각 hello, hello 크기 집합의 모든 Vm에 대 한 hello 매개 변수를 하기 전에 tooset hello 관리자 사용자 이름 및 암호 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-171">In hello following snippet, we use hello parameters from before tooset hello administrator username and password for all VMs in hello scale set.</span></span> <span data-ttu-id="9677d-172">Hello로 수행 `parameters` 템플릿 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-172">We do this with hello `parameters` template function.</span></span> <span data-ttu-id="9677d-173">이 함수는 매개 변수 toorefer tooand 해당 매개 변수에 대해 hello 값을 출력을 지정 하는 문자열에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-173">This function takes in a string that specifies which parameter toorefer tooand outputs hello value for that parameter.</span></span>

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a><span data-ttu-id="9677d-174">VM 네트워크 구성 지정</span><span class="sxs-lookup"><span data-stu-id="9677d-174">Specify VM network configuration</span></span>
<span data-ttu-id="9677d-175">마지막으로, hello 크기 집합의 hello Vm에 대 한 toospecify hello 네트워크 구성을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-175">Finally, we need toospecify hello network configuration for hello VMs in hello scale set.</span></span> <span data-ttu-id="9677d-176">이 경우 앞에서 만든 hello 서브넷의 toospecify hello ID만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-176">In this case, we only need toospecify hello ID of hello subnet created earlier.</span></span> <span data-ttu-id="9677d-177">이 hello 크기 집합 tooput hello 네트워크 인터페이스가이 서브넷의 값을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-177">This tells hello scale set tooput hello network interfaces in this subnet.</span></span>

<span data-ttu-id="9677d-178">Hello hello를 사용 하 여 hello 서브넷을 포함 하는 가상 네트워크의 hello ID를 얻을 수 `resourceId` 템플릿 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-178">You can get hello ID of hello virtual network containing hello subnet by using hello `resourceId` template function.</span></span> <span data-ttu-id="9677d-179">이 함수는 hello 유형 및 리소스의 이름을 사용 하 고 반환 hello 해당 리소스의 정규화 된 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-179">This function takes in hello type and name of a resource and returns hello fully qualified identifier of that resource.</span></span> <span data-ttu-id="9677d-180">이 ID는 hello 형식은 같습니다.`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span><span class="sxs-lookup"><span data-stu-id="9677d-180">This ID has hello form: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span></span>

<span data-ttu-id="9677d-181">그러나 hello 가상 네트워크의 hello 식별자 충분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-181">However, hello identifier of hello virtual network is not enough.</span></span> <span data-ttu-id="9677d-182">크기 집합 Vm에 있어야 hello hello 특정 서브넷을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-182">You must specify hello specific subnet that hello scale set VMs should be in.</span></span> <span data-ttu-id="9677d-183">toodo이를 연결할 `/subnets/mySubnet` hello 가상 네트워크의 toohello ID입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-183">toodo this, concatenate `/subnets/mySubnet` toohello ID of hello virtual network.</span></span> <span data-ttu-id="9677d-184">hello 결과 hello 서브넷의 정규화 된 hello ID입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-184">hello result is hello fully qualified ID of hello subnet.</span></span> <span data-ttu-id="9677d-185">이 연결은 hello로 수행 `concat` 일련의 문자열에서 사용 하 고 해당 연결을 반환 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="9677d-185">Do this concatenation with hello `concat` function, which takes in a series of strings and returns their concatenation.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9677d-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9677d-186">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
