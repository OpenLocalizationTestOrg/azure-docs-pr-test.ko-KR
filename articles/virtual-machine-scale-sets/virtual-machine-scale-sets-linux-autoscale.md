---
title: "Linux 가상 컴퓨터 크기 집합 자동 크기 조정 | Microsoft Docs"
description: "Azure CLI를 사용하여 Linux 가상 컴퓨터 크기 집합 자동 크기 조정 설정"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 83e93d9c-cac0-41d3-8316-6016f5ed0ce4
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: eff4add1cb16fe25022787668dc1d2277845dd95
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="1595d-103">가상 컴퓨터 크기 집합에서 Linux 컴퓨터 자동 확장</span><span class="sxs-lookup"><span data-stu-id="1595d-103">Automatically scale Linux machines in a virtual machine scale set</span></span>
<span data-ttu-id="1595d-104">가상 컴퓨터 크기 집합은 동일한 가상 컴퓨터를 집합으로 쉽게 배포하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="1595d-105">규모 집합은 대규모 응용 프로그램에 대한 높은 확장성과 사용자 지정 가능한 계산 계층을 제공하고 Windows 플랫폼 이미지, Linux 플랫폼 이미지, 사용자 지정 이미지 및 확장을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="1595d-106">자세한 내용은 [가상 컴퓨터 크기 집합 개요](virtual-machine-scale-sets-overview.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="1595d-106">To learn more, see [Virtual Machine Scale Sets Overview](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="1595d-107">이 자습서에서는 Ubuntu Linux의 최신 버전을 사용하여 Linux 가상 컴퓨터의 크기 집합을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-107">This tutorial shows you how to create a scale set of Linux virtual machines using the latest version of Ubuntu Linux.</span></span> <span data-ttu-id="1595d-108">또한 이 자습서는 집합의 컴퓨터 수를 자동으로 조정하는 방법도 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-108">The tutorial also shows you how to automatically scale the machines in the set.</span></span> <span data-ttu-id="1595d-109">Azure Resource Manager 템플릿을 작성하고 Azure CLI를 통해 배포하여 크기 집합을 만들고 크기 조정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-109">You create the scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure CLI.</span></span> <span data-ttu-id="1595d-110">템플릿에 대한 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1595d-110">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="1595d-111">크기 집합의 자동 확장에 대한 자세한 내용은 [자동 크기 조정 및 가상 컴퓨터 크기 집합](virtual-machine-scale-sets-autoscale-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1595d-111">To learn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="1595d-112">이 자습서에서는 다음 리소스 및 확장을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-112">In this tutorial, you deploy the following resources and extensions:</span></span>

* <span data-ttu-id="1595d-113">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="1595d-113">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="1595d-114">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="1595d-114">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="1595d-115">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="1595d-115">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="1595d-116">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="1595d-116">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="1595d-117">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="1595d-117">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="1595d-118">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="1595d-118">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="1595d-119">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="1595d-119">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="1595d-120">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="1595d-120">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="1595d-121">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="1595d-121">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="1595d-122">Resource Manager 리소스에 대한 자세한 내용은 [Azure Resource Manager 및 클래식 배포](../azure-resource-manager/resource-manager-deployment-model.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1595d-122">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

<span data-ttu-id="1595d-123">이 자습서의 단계를 시작하기 전에 [Azure CLI를 설치합니다](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1595d-123">Before you get started with the steps in this tutorial, [install the Azure CLI](../cli-install-nodejs.md).</span></span>

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="1595d-124">1단계: 리소스 그룹 및 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1595d-124">Step 1: Create a resource group and a storage account</span></span>

1. <span data-ttu-id="1595d-125">**Microsoft Azure에 로그인**</span><span class="sxs-lookup"><span data-stu-id="1595d-125">**Sign in to Microsoft Azure**</span></span>  
<span data-ttu-id="1595d-126">명령줄 인터페이스(Bash, 터미널, 명령 프롬프트)에서 Resource Manager 모드로 전환한 후 [회사 또는 학교 ID를 사용하여 로그인](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login)합니다. Azure 계정에 대한 대화형 로그인 환경 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-126">In your command-line interface (Bash, Terminal, Command prompt), switch to Resource Manager mode, and then [log in with your work or school id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Follow the prompts for an interactive login experience to your Azure account.</span></span>

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > <span data-ttu-id="1595d-127">회사 또는 학교 ID가 있고 2단계 인증이 사용되도록 설정되지 않은 경우 `azure login -u`와 해당 ID를 사용하여 대화형 세션 없이 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-127">If you have a work or school ID and you do not have two-factor authentication enabled, use `azure login -u` with the ID to log in without an interactive session.</span></span> <span data-ttu-id="1595d-128">회사 또는 학교 ID가 없는 경우 [개인 Microsoft 계정에서 회사 또는 학교 ID를 만들 수 있습니다](../active-directory/active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1595d-128">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../active-directory/active-directory-users-create-azure-portal.md).</span></span>
    
2. <span data-ttu-id="1595d-129">**리소스 그룹 만들기**</span><span class="sxs-lookup"><span data-stu-id="1595d-129">**Create a resource group**</span></span>  
<span data-ttu-id="1595d-130">모든 리소스는 리소스 그룹에 배포되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-130">All resources must be deployed to a resource group.</span></span> <span data-ttu-id="1595d-131">이 자습서의 경우 리소스 그룹의 이름을 **vmsstest1**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-131">For this tutorial, name the resource group **vmsstest1**.</span></span>
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. <span data-ttu-id="1595d-132">**새 리소스 그룹에 저장소 계정 배포**</span><span class="sxs-lookup"><span data-stu-id="1595d-132">**Deploy a storage account into the new resource group**</span></span>  
<span data-ttu-id="1595d-133">이 저장소 계정은 템플릿이 저장되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-133">This storage account is where the template is stored.</span></span> <span data-ttu-id="1595d-134">**vmsstestsa**라는 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-134">Create a storage account named **vmsstestsa**.</span></span>
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-the-template"></a><span data-ttu-id="1595d-135">2단계: 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="1595d-135">Step 2: Create the template</span></span>
<span data-ttu-id="1595d-136">Azure 리소스 관리자 템플릿을 사용하면 리소스와 관련 배포 매개 변수에 대한 JSON 설명을 사용하여 Azure 리소스를 함께 배포하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-136">An Azure Resource Manager template makes it possible for you to deploy and manage Azure resources together by using a JSON description of the resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="1595d-137">원하는 편집기에서 VMSSTemplate.json 파일을 만들고 템플릿을 지원하기 위한 초기 JSON 구조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-137">In your favorite editor, create the file VMSSTemplate.json and add the initial JSON structure to support the template.</span></span>

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. <span data-ttu-id="1595d-138">매개 변수가 항상 필요한 것은 아니지만 템플릿이 배포될 때 값을 입력하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-138">Parameters are not always required, but they provide a way to input values when the template is deployed.</span></span> <span data-ttu-id="1595d-139">템플릿에 추가한 매개 변수 부모 요소 아래에 다음과 같은 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-139">Add these parameters under the parameters parent element that you added to the template.</span></span>

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * <span data-ttu-id="1595d-140">크기 집합의 컴퓨터에 액세스하는 데 사용하는 별도 가상 컴퓨터의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-140">A name for the separate virtual machine that is used to access the machines in the scale set.</span></span>
   * <span data-ttu-id="1595d-141">템플릿이 저장된 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-141">A name for the storage account where the template is stored.</span></span>
   * <span data-ttu-id="1595d-142">규모 집합에서 처음으로 만들기 위한 가상 컴퓨터의 인스턴스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-142">The number of instances of virtual machines to initially create in the scale set.</span></span>
   * <span data-ttu-id="1595d-143">가상 컴퓨터의 관리자 계정 이름 및 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-143">A name and password of the administrator account on the virtual machines.</span></span>
   * <span data-ttu-id="1595d-144">크기 집합을 지원하기 위해 만들어진 리소스에 대한 이름 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-144">A name prefix for the resources that are created to support the scale set.</span></span>

3. <span data-ttu-id="1595d-145">템플릿에서 변수를 사용하여 자주 변경되는 값 또는 매개 변수 값의 조합에서 만들어야 하는 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-145">Variables can be used in a template to specify values that may change frequently or values that need to be created from a combination of parameter values.</span></span> <span data-ttu-id="1595d-146">템플릿에 추가한 변수 부모 요소 아래에 다음과 같은 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-146">Add these variables under the variables parent element that you added to the template.</span></span>

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
    "wadlogs": "<WadCfg><DiagnosticMonitorConfiguration>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor\\PercentProcessorTime\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU percentage guest OS\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```

   * <span data-ttu-id="1595d-147">네트워크 인터페이스에서 사용되는 DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-147">DNS names that are used by the network interfaces.</span></span>
   * <span data-ttu-id="1595d-148">가상 네트워크 및 서브넷에 대한 IP 주소 이름 및 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-148">The IP address names and prefixes for the virtual network and subnets.</span></span>
   * <span data-ttu-id="1595d-149">가상 네트워크, 부하 분산 장치 및 네트워크 인터페이스의 이름 및 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-149">The names and identifiers of the virtual network, load balancer, and network interfaces.</span></span>
   * <span data-ttu-id="1595d-150">규모 집합의 컴퓨터와 연결된 계정에 대한 저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-150">Storage account names for the accounts associated with the machines in the scale set.</span></span>
   * <span data-ttu-id="1595d-151">가상 컴퓨터에 설치되어 있는 진단 확장에 대한 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-151">Settings for the Diagnostics extension that is installed on the virtual machines.</span></span> <span data-ttu-id="1595d-152">진단 확장에 대한 자세한 내용은 [Azure Resource Manager 템플릿을 사용한 모니터링 및 진단으로 Windows 가상 컴퓨터 만들기](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1595d-152">For more information about the Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="1595d-153">템플릿에 추가된 리소스 부모 요소 아래에 저장소 계정 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-153">Add the storage account resource under the resources parent element that you added to the template.</span></span> <span data-ttu-id="1595d-154">이 템플릿은 루프를 사용하여 운영 체제 디스크 및 진단 데이터가 저장되는 권장되는 5개의 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-154">This template uses a loop to create the recommended five storage accounts where the operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="1595d-155">이 계정 집합은 현재 최대인 규모 집합에서 최대 100개의 가상 컴퓨터를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-155">This set of accounts can support up to 100 virtual machines in a scale set, which is the current maximum.</span></span> <span data-ttu-id="1595d-156">템플릿에 대한 매개 변수에서 제공하는 접미사와 결합된 변수에서 정의된 문자 지정자와 함께 각 저장소 계정 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-156">Each storage account is named with a letter designator that was defined in the variables combined with the suffix that you provide in the parameters for the template.</span></span>
   
        {
          "type": "Microsoft.Storage/storageAccounts",
          "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
          "apiVersion": "2015-06-15",
          "copy": {
            "name": "storageLoop",
            "count": 5
          },
          "location": "[resourceGroup().location]",
          "properties": { "accountType": "Standard_LRS" }
        },

5. <span data-ttu-id="1595d-157">가상 네트워크 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-157">Add the virtual network resource.</span></span> <span data-ttu-id="1595d-158">자세한 내용은 [네트워크 리소스 공급자](../virtual-network/resource-groups-networking.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1595d-158">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. <span data-ttu-id="1595d-159">부하 분산 장치 및 네트워크 인터페이스에서 사용되는 공용 IP 주소 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-159">Add the public IP address resources that are used by the load balancer and network interface.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. <span data-ttu-id="1595d-160">규모 집합에서 사용되는 부하 분산 장치 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-160">Add the load balancer resource that is used by the scale set.</span></span> <span data-ttu-id="1595d-161">자세한 내용은 [부하 분산 장치에 대한 Azure 리소스 관리자 지원](../load-balancer/load-balancer-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1595d-161">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 22
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="1595d-162">별도의 가상 컴퓨터에서 사용하는 네트워크 인터페이스 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-162">Add the network interface resource that is used by the separate virtual machine.</span></span> <span data-ttu-id="1595d-163">크기 집합의 컴퓨터는 공용 IP 주소를 통해 액세스할 수 없기 때문에 컴퓨터에 원격으로 액세스하기 위해 동일한 가상 네트워크에 별도의 가상 컴퓨터가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-163">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in the same virtual network to remotely access the machines.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. <span data-ttu-id="1595d-164">확장 집합과 동일한 네트워크에 별도의 가상 컴퓨터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-164">Add the separate virtual machine in the same network as the scale set.</span></span>

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "14.04.4-LTS",
            "version": "latest"
          },
          "osDisk": {
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        }
      }
    },
    ```

10. <span data-ttu-id="1595d-165">가상 컴퓨터 크기 집합 리소스를 추가하고 크기 집합의 모든 가상 컴퓨터에 설치되어 있는 진단 확장을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-165">Add the virtual machine scale set resource and specify the diagnostics extension that is installed on all virtual machines in the scale set.</span></span> <span data-ttu-id="1595d-166">이 리소스에 대한 설정 중 대부분은 가상 컴퓨터 리소스와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-166">Many of the settings for this resource are similar with the virtual machine resource.</span></span> <span data-ttu-id="1595d-167">주요 차이점은 크기 집합의 가상 컴퓨터 수를 지정하는 용량 요소와 가상 컴퓨터를 업데이트하는 방식을 지정하는 upgradePolicy입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-167">The main differences are the capacity element that specifies the number of virtual machines in the scale set and upgradePolicy that specifies how updates are made to virtual machines.</span></span> <span data-ttu-id="1595d-168">크기 집합은 모든 저장소 계정이 dependsOn 요소로 지정된 대로 만들어질 때까지 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-168">The scale set is not created until all the storage accounts are created as specified with the dependsOn element.</span></span>

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4],'.blob.core.windows.net/vmss')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "Canonical",
              "offer": "UbuntuServer",
              "sku": "14.04.4-LTS",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name":"LinuxDiagnostic",
                "properties": {
                  "publisher":"Microsoft.OSTCExtensions",
                  "type":"LinuxDiagnostic",
                  "typeHandlerVersion":"2.1",
                  "autoUpgradeMinorVersion":false,
                  "settings": {
                    "xmlCfg":"[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount":"[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName":"[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey":"[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint":"https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="1595d-169">규모 집합이 집합의 컴퓨터에서 프로세서 사용량에 따라 조정하는 방법을 정의하는 autoscaleSettings 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-169">Add the autoscaleSettings resource that defines how the scale set adjusts based on processor usage on the machines in the set.</span></span>

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor\\PercentProcessorTime",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```
    
    <span data-ttu-id="1595d-170">이 자습서의 경우 다음 값이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-170">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="1595d-171">**metricName**</span><span class="sxs-lookup"><span data-stu-id="1595d-171">**metricName**</span></span>  
    <span data-ttu-id="1595d-172">이 값은 wadperfcounter 변수에 정의한 성능 카운터와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-172">This value is the same as the performance counter that we defined in the wadperfcounter variable.</span></span> <span data-ttu-id="1595d-173">진단 확장은 이 변수를 사용하여 **Processor\PercentProcessorTime** 카운터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-173">Using that variable, the Diagnostics extension collects the **Processor\PercentProcessorTime** counter.</span></span>
    
    * <span data-ttu-id="1595d-174">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="1595d-174">**metricResourceUri**</span></span>  
    <span data-ttu-id="1595d-175">이 값은 가상 컴퓨터 크기 집합의 리소스 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-175">This value is the resource identifier of the virtual machine scale set.</span></span>
    
    * <span data-ttu-id="1595d-176">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="1595d-176">**timeGrain**</span></span>  
    <span data-ttu-id="1595d-177">이 값은 수집되는 메트릭의 세분성입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-177">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="1595d-178">이 템플릿에서는 1분으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-178">In this template, it is set to one minute.</span></span>
    
    * <span data-ttu-id="1595d-179">**statistic**</span><span class="sxs-lookup"><span data-stu-id="1595d-179">**statistic**</span></span>  
    <span data-ttu-id="1595d-180">이 값은 자동 크기 조정 작업을 수용하기 위해 메트릭을 결합하는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-180">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="1595d-181">가능한 값은 평균, 최소, 최대입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-181">The possible values are: Average, Min, Max.</span></span> <span data-ttu-id="1595d-182">이 템플릿에서는 가상 컴퓨터의 평균 총 CPU 사용량이 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-182">In this template, the average total CPU usage of the virtual machines is collected.</span></span>

    * <span data-ttu-id="1595d-183">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="1595d-183">**timeWindow**</span></span>  
    <span data-ttu-id="1595d-184">이 값은 인스턴스 데이터가 수집되는 시간 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-184">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="1595d-185">5분에서 12시간 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-185">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="1595d-186">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="1595d-186">**timeAggregation**</span></span>  
    <span data-ttu-id="1595d-187">이 값은 시간이 지남에 따라 수집된 데이터가 결합되어야 하는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-187">his value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="1595d-188">기본값은 평균입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-188">The default value is Average.</span></span> <span data-ttu-id="1595d-189">가능한 값은 평균, 최소, 최대, 마지막, 합계, 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-189">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="1595d-190">**operator**</span><span class="sxs-lookup"><span data-stu-id="1595d-190">**operator**</span></span>  
    <span data-ttu-id="1595d-191">이 값은 메트릭 데이터와 임계값을 비교하는 데 사용되는 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-191">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="1595d-192">가능한 값은 Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-192">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="1595d-193">**threshold**</span><span class="sxs-lookup"><span data-stu-id="1595d-193">**threshold**</span></span>  
    <span data-ttu-id="1595d-194">이 값은 크기 조정 작업을 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-194">This value triggers the scale action.</span></span> <span data-ttu-id="1595d-195">이 템플릿에서 집합의 컴퓨터 간 평균 CPU 사용량이 50%가 넘는 경우 컴퓨터가 규모 집합에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-195">In this template, machines are added to the scale set when the average CPU usage among machines in the set is over 50%.</span></span>
    
    * <span data-ttu-id="1595d-196">**direction**</span><span class="sxs-lookup"><span data-stu-id="1595d-196">**direction**</span></span>  
    <span data-ttu-id="1595d-197">이 값은 임계값이 달성되었을 때 수행되는 동작을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-197">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="1595d-198">가능한 값은 증가 또는 감소입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-198">The possible values are Increase or Decrease.</span></span> <span data-ttu-id="1595d-199">이 템플릿에서 규모 집합의 가상 컴퓨터 수는 임계값이 정의된 시간 창에서 50%가 넘는 경우 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-199">In this template, the number of virtual machines in the scale set is increased if the threshold is over 50% in the defined time window.</span></span>

    * <span data-ttu-id="1595d-200">**type**</span><span class="sxs-lookup"><span data-stu-id="1595d-200">**type**</span></span>  
    <span data-ttu-id="1595d-201">이 값은 발생되어야 하는 동작의 유형이며 ChangeCount로 설정되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-201">This value is the type of action that should occur and must be set to ChangeCount.</span></span>
    
    * <span data-ttu-id="1595d-202">**값**</span><span class="sxs-lookup"><span data-stu-id="1595d-202">**value**</span></span>  
    <span data-ttu-id="1595d-203">이 값은 크기 집합에서 추가되거나 제거된 가상 컴퓨터의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-203">This value is the number of virtual machines that are added or removed from the scale set.</span></span> <span data-ttu-id="1595d-204">이 값은 1 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-204">This value must be 1 or greater.</span></span> <span data-ttu-id="1595d-205">기본값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-205">The default value is 1.</span></span> <span data-ttu-id="1595d-206">이 템플릿에서 규모 집합의 컴퓨터 수는 임계값에 도달한 경우 1씩 증가합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-206">In this template, the number of machines in the scale set increases by 1 when the threshold is met.</span></span>

    * <span data-ttu-id="1595d-207">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="1595d-207">**cooldown**</span></span>  
    <span data-ttu-id="1595d-208">이 값은 다음 작업이 발생하기 전에 마지막 크기 조정 작업 이후에 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-208">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="1595d-209">이 값은 1분에서 1주 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-209">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="1595d-210">템플릿 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-210">Save the template file.</span></span>    

## <a name="step-3-upload-the-template-to-storage"></a><span data-ttu-id="1595d-211">3단계: 템플릿을 저장소에 업로드</span><span class="sxs-lookup"><span data-stu-id="1595d-211">Step 3: Upload the template to storage</span></span>
<span data-ttu-id="1595d-212">1단계에서 만든 저장소 계정의 계정 이름 및 기본 키를 알고 있는 한 템플릿을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-212">The template can be uploaded as long as you know the name and primary key of the storage account that you created in step 1.</span></span>

1. <span data-ttu-id="1595d-213">명령줄 인터페이스(Bash, 터미널, 명령 프롬프트)에서 이러한 명령을 실행하여 저장소 계정에 액세스하는 데 필요한 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-213">In your command-line interface (Bash, Terminal, Command prompt), run these commands to set the environment variables needed to access the storage account:</span></span>

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    <span data-ttu-id="1595d-214">Azure 포털에서 저장소 계정 리소스를 볼 때 열쇠 아이콘을 클릭하여 키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-214">You can get the key by clicking the key icon when viewing the storage account resource in the Azure portal.</span></span> <span data-ttu-id="1595d-215">Windows 명령 프롬프트를 사용할 때 export 대신 **set** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-215">When using a Windows command prompt, type **set** instead of export.</span></span>

2. <span data-ttu-id="1595d-216">템플릿을 저장할 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-216">Create the container for storing the template.</span></span>
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. <span data-ttu-id="1595d-217">새 컨테이너에 템플릿 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-217">Upload the template file to the new container.</span></span>
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-the-template"></a><span data-ttu-id="1595d-218">4단계: 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="1595d-218">Step 4: Deploy the template</span></span>
<span data-ttu-id="1595d-219">템플릿을 만들었으므로 리소스 배포를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-219">Now that you created the template, you can start deploying the resources.</span></span> <span data-ttu-id="1595d-220">이 명령을 사용하여 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-220">Use this command to start the process:</span></span>

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

<span data-ttu-id="1595d-221">Enter 키를 누르면 지정한 변수에 대한 값을 제공하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-221">When you press enter, you are prompted to provide values for the variables you assigned.</span></span> <span data-ttu-id="1595d-222">다음 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-222">Provide these values:</span></span>

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

<span data-ttu-id="1595d-223">모든 리소스가 성공적으로 배포되는 데 15분 정도가 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-223">It should take about 15 minutes for all the resources to successfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="1595d-224">포털의 기능을 사용하여 리소스를 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-224">You can also use the portal’s ability to deploy the resources.</span></span> <span data-ttu-id="1595d-225">다음 링크를 사용합니다. https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template></span><span class="sxs-lookup"><span data-stu-id="1595d-225">Use this link: https://portal.azure.com/#create/Microsoft.Template/uri/<link to VM Scale Set JSON template></span></span>


## <a name="step-5-monitor-resources"></a><span data-ttu-id="1595d-226">5단계: 리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="1595d-226">Step 5: Monitor resources</span></span>
<span data-ttu-id="1595d-227">이러한 메서드를 사용하여 가상 컴퓨터 규모 집합에 대한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-227">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="1595d-228">Azure 포털 - 포털을 사용하여 현재 제한된 양의 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-228">The Azure portal - You can currently get a limited amount of information using the portal.</span></span>

* <span data-ttu-id="1595d-229">[Azure 리소스 탐색기](https://resources.azure.com/) - 크기 집합의 현재 상태를 탐색하는 데 가장 적합한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-229">The [Azure Resource Explorer](https://resources.azure.com/) - This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="1595d-230">이 경로를 따르고 사용자가 만든 규모 집합의 인스턴스 보기가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-230">Follow this path and you should see the instance view of the scale set that you created:</span></span>
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* <span data-ttu-id="1595d-231">Azure CLI - 이 명령을 사용하여 몇 가지 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-231">Azure CLI - Use this command to get some information:</span></span>

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* <span data-ttu-id="1595d-232">다른 컴퓨터와 마찬가지로 jumpbox 가상 컴퓨터에 연결한 다음 개별 프로세스를 모니터링하도록 규모 집합의 가상 컴퓨터에 원격으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-232">Connect to the jumpbox virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="1595d-233">규모 집합에 대한 정보를 얻기 위해 전체 REST API를 [가상 컴퓨터 크기 규모 집합](https://msdn.microsoft.com/library/mt589023.aspx)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-233">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx).</span></span>

## <a name="step-6-remove-the-resources"></a><span data-ttu-id="1595d-234">6단계: 리소스 제거</span><span class="sxs-lookup"><span data-stu-id="1595d-234">Step 6: Remove the resources</span></span>
<span data-ttu-id="1595d-235">Azure에서 사용되는 리소스에 대한 요금이 부과되기 때문에, 더 이상 필요하지 않은 리소스를 항상 삭제하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-235">Because you are charged for resources used in Azure, it is always a good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="1595d-236">리소스 그룹에서 각 리소스를 개별적으로 삭제할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-236">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="1595d-237">리소스 그룹을 삭제하면 모든 해당 리소스가 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-237">You can delete the resource group and all its resources are automatically deleted.</span></span>

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a><span data-ttu-id="1595d-238">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1595d-238">Next steps</span></span>
* <span data-ttu-id="1595d-239">[Azure Monitor 플랫폼 간 CLI 빠른 시작 샘플](../monitoring-and-diagnostics/insights-cli-samples.md)에서 Azure Monitor 모니터링 기능 예제를 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="1595d-239">Find examples of Azure Monitor monitoring features in [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>
* <span data-ttu-id="1595d-240">[크기 자동 조정 작업을 사용하여 Azure Monitor에서 전자 메일 및 웹후크 경고 알림 보내기](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)에서 알림 기능에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="1595d-240">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="1595d-241">[감사 로그를 사용하여 Azure Monitor에서 전자 메일 및 웹후크 경고 알림을 보내는](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md) 방법을 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="1595d-241">Learn how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>
* <span data-ttu-id="1595d-242">Virtual Machine Scale Sets의 자동 크기 조정 기능을 실행하도록 Python/bottle 앱을 설정하는 [Ubuntu 16.04의 자동 크기 조정 데모 앱](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) 템플릿을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1595d-242">Check out the [Autoscale demo app on Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) template that sets up a Python/bottle app to exercise the automatic scaling functionality of Virtual Machine Scale Sets.</span></span>

