---
title: "Windows 가상 컴퓨터 크기 집합 aaaAutoscale | Microsoft Docs"
description: "Azure PowerShell을 사용하여 Windows 가상 컴퓨터 확장 집합 자동 크기 조정 설정"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88886cad-a2f0-46bc-8b58-32ac2189fc93
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 67cf1c5063ceba4fc076dc270090defdbddbcfe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="2df02-103">가상 컴퓨터 확장 집합에서 자동으로 컴퓨터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="2df02-103">Automatically scale machines in a virtual machine scale set</span></span>
<span data-ttu-id="2df02-104">가상 컴퓨터 크기 집합에 더 쉽게 있습니다 toodeploy 고 집합으로 동일한 가상 컴퓨터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="2df02-105">규모 집합은 대규모 응용 프로그램에 대한 높은 확장성과 사용자 지정 가능한 계산 계층을 제공하고 Windows 플랫폼 이미지, Linux 플랫폼 이미지, 사용자 지정 이미지 및 확장을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="2df02-106">규모 집합에 대한 자세한 내용은 [가상 컴퓨터 규모 집합](virtual-machine-scale-sets-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2df02-106">For more information about scale sets, see [Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="2df02-107">이 자습서의 Windows 컴퓨터와 가상 컴퓨터 자동으로 크기 조정 hello hello에 크기 집합 toocreate 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-107">This tutorial shows you how toocreate a scale set of Windows virtual machines and automatically scale hello machines in hello set.</span></span> <span data-ttu-id="2df02-108">Azure 리소스 관리자 템플릿 만들기 및 Azure PowerShell을 사용 하 여 배포 하 여 크기 조정 설정 hello 눈금을 만들 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-108">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure PowerShell.</span></span> <span data-ttu-id="2df02-109">템플릿에 대한 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2df02-109">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="2df02-110">크기 집합의 자동 크기 조정에 대 한 더 toolearn 참조 [자동 크기 조정 및 가상 컴퓨터 크기 조정 설정](virtual-machine-scale-sets-autoscale-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-110">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="2df02-111">이 문서에서는 hello 다음 배포 리소스 및 확장:</span><span class="sxs-lookup"><span data-stu-id="2df02-111">In this article, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="2df02-112">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="2df02-112">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="2df02-113">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="2df02-113">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="2df02-114">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="2df02-114">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="2df02-115">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="2df02-115">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="2df02-116">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="2df02-116">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="2df02-117">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="2df02-117">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="2df02-118">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="2df02-118">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="2df02-119">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="2df02-119">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="2df02-120">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="2df02-120">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="2df02-121">Resource Manager 리소스에 대한 자세한 내용은 [Azure Resource Manager 및 클래식 배포](../azure-resource-manager/resource-manager-deployment-model.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2df02-121">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="step-1-install-azure-powershell"></a><span data-ttu-id="2df02-122">1단계: Azure PowerShell 설치</span><span class="sxs-lookup"><span data-stu-id="2df02-122">Step 1: Install Azure PowerShell</span></span>
<span data-ttu-id="2df02-123">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) hello 최신 버전의 Azure PowerShell을 설치, 구독을 선택 하 고 tooAzure 로그인 하는 방법에 대 한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooAzure.</span></span>

## <a name="step-2-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="2df02-124">2단계: 리소스 그룹 및 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="2df02-124">Step 2: Create a resource group and a storage account</span></span>
1. <span data-ttu-id="2df02-125">**리소스 그룹 만들기** – 모든 리소스는 배포 된 tooa 리소스 그룹 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-125">**Create a resource group** – All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="2df02-126">사용 하 여 [새로 AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) 리소스 그룹 이름이 toocreate **vmsstestrg1**합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-126">Use [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx) toocreate a resource group named **vmsstestrg1**.</span></span>
2. <span data-ttu-id="2df02-127">**저장소 계정 만들기** –이 저장소 계정은 hello 템플릿이 보관 된입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-127">**Create a storage account** – This storage account is where hello template is stored.</span></span> <span data-ttu-id="2df02-128">사용 하 여 [새로 AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) 라는 저장소 계정 toocreate **vmsstestsa**합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-128">Use [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) toocreate a storage account named **vmsstestsa**.</span></span>

## <a name="step-3-create-hello-template"></a><span data-ttu-id="2df02-129">3 단계: hello 서식 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="2df02-129">Step 3: Create hello template</span></span>
<span data-ttu-id="2df02-130">Azure 리소스 관리자 템플릿 toodeploy 있습니다 수 있도록 하 고 hello 리소스 및 관련된 배포 매개 변수의 JSON 설명을 사용 하 여 Azure 리소스를 함께 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-130">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="2df02-131">선호 하는 편집기에서 hello 파일 C:\VMSSTemplate.json 만들고 hello 초기 JSON 구조 toosupport hello 템플릿을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-131">In your favorite editor, create hello file C:\VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

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

2. <span data-ttu-id="2df02-132">매개 변수는 항상 필수 이지만 제공 방법을 tooinput 값 hello 서식 파일이 배포 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="2df02-132">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="2df02-133">Toohello 템플릿을 추가한 hello 매개 변수 부모 요소 아래에 이러한 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-133">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json   
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
    * <span data-ttu-id="2df02-134">Hello 눈금에 사용 되는 tooaccess hello 컴퓨터 있는 hello 별도 가상 컴퓨터에 대 한 이름이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-134">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
    * <span data-ttu-id="2df02-135">hello 템플릿이 보관 된 hello 저장소 계정의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-135">hello name of hello storage account where hello template is stored.</span></span>
    * <span data-ttu-id="2df02-136">가상 컴퓨터 tooinitially hello 수가 hello 크기 집합에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-136">hello number of virtual machines tooinitially create in hello scale set.</span></span>
    * <span data-ttu-id="2df02-137">hello 이름과 hello 가상 컴퓨터에 대 한 hello 관리자 계정의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-137">hello name and password of hello administrator account on hello virtual machines.</span></span>
    * <span data-ttu-id="2df02-138">Toosupport hello 눈금 만들어진 hello 리소스에 대 한 이름 접두사를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-138">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="2df02-139">변수는 자주 변경 될 수 있는 템플릿 toospecify 값에 사용할 수 있습니다 또는 toobe 해야 하는 값이 매개 변수 값의 조합에서 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-139">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="2df02-140">Toohello 템플릿을 추가한 hello 변수 부모 요소 아래에 이러한 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-140">Add these variables under hello variables parent element that you added toohello template.</span></span>

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
      "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```
   
    * <span data-ttu-id="2df02-141">Hello 네트워크 인터페이스에서 사용 되는 DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-141">DNS names that are used by hello network interfaces.</span></span>

        * <span data-ttu-id="2df02-142">hello IP 주소 이름 및 hello 가상 네트워크 및 서브넷에 대 한 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-142">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
        * <span data-ttu-id="2df02-143">hello 이름 및 식별자 hello 가상 네트워크의 부하 분산 장치, 및 네트워크 인터페이스.</span><span class="sxs-lookup"><span data-stu-id="2df02-143">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
        * <span data-ttu-id="2df02-144">Hello 크기 집합의 hello 컴퓨터와 연결 된 hello 계정에 대 한 저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-144">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
        * <span data-ttu-id="2df02-145">Hello hello 가상 컴퓨터에 설치 된 진단 확장에 대 한 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-145">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="2df02-146">Hello 진단 확장에 대 한 자세한 내용은 참조 [모니터링 및 Azure 리소스 관리자 템플릿을 사용 하 여 진단을 사용 하 여 Windows 가상 컴퓨터를 만들](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-146">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="2df02-147">Hello 저장소 계정 리소스 toohello 템플릿을 추가한 hello 리소스 부모 요소 아래에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-147">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="2df02-148">이 템플릿은 hello 운영 체제 디스크 및 진단 데이터 저장 된 다섯 개의 저장소 계정을 권장 루프 toocreate hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-148">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="2df02-149">계정의이 집합 hello 현재 최대 크기 집합의 too100 가상 컴퓨터를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-149">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="2df02-150">각 저장소 계정은 hello 서식 파일에 대 한 hello 매개 변수에서 제공 하는 hello 접두사와 함께 하는 hello 변수에 정의 된 문자 지정자도 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-150">Each storage account is named with a letter designator that was defined in hello variables combined with hello prefix that you provide in hello parameters for hello template.</span></span>

    ```json
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
    ```

5. <span data-ttu-id="2df02-151">Hello 가상 네트워크 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-151">Add hello virtual network resource.</span></span> <span data-ttu-id="2df02-152">자세한 내용은 [네트워크 리소스 공급자](../virtual-network/resource-groups-networking.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2df02-152">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="2df02-153">Hello 공용 IP 주소 리소스 hello에서 사용 되는 부하 분산 장치 및 네트워크 인터페이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-153">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

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

7. <span data-ttu-id="2df02-154">Hello 크기 집합에서 사용 되는 hello 부하 분산 장치 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-154">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="2df02-155">자세한 내용은 [부하 분산 장치에 대한 Azure 리소스 관리자 지원](../load-balancer/load-balancer-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2df02-155">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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
                "id": "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
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
              "backendPort": 3389
            }
          }
        ]
      }
    },
    ```

8. <span data-ttu-id="2df02-156">Hello hello 별도 가상 컴퓨터에서 사용 되는 네트워크 인터페이스 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-156">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="2df02-157">컴퓨터 크기 집합의 공용 IP 주소를 통해 액세스할 수 없습니다, 때문에 별도 가상 컴퓨터에에서 만들어집니다 hello 동일한 가상 네트워크 tooremotely 액세스 hello 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="2df02-157">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

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

9. <span data-ttu-id="2df02-158">Hello hello 크기 집합으로 동일한 네트워크에 hello 별도 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-158">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

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
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2012-R2-Datacenter",
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

10. <span data-ttu-id="2df02-159">Hello 가상 컴퓨터 크기 집합 리소스를 추가 하 고 hello 크기 집합의 모든 가상 컴퓨터에 설치 되어 있는 hello 진단 확장을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-159">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="2df02-160">이 리소스에 대 한 hello 설정 중 대부분 hello 가상 컴퓨터 리소스와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-160">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="2df02-161">hello 주요 차이점은 hello 크기 집합의 가상 컴퓨터의 hello 수를 지정 하는 hello 용량 요소 및 upgradePolicy 업데이트 toovirtual 컴퓨터 적용 하는 방법을 지정 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-161">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set, and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="2df02-162">hello 크기 집합 만들어지지 모든 hello 저장소 계정이 생성 될 때까지 hello dependsOn 요소와 지정 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-162">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

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
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3], '.blob.core.windows.net/vhds')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4], '.blob.core.windows.net/vhds')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "MicrosoftWindowsServer",
              "offer": "WindowsServer",
              "sku": "2012-R2-Datacenter",
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
                "name": "Microsoft.Insights.VMDiagnosticsSettings",
                "properties": {
                  "publisher": "Microsoft.Azure.Diagnostics",
                  "type": "IaaSDiagnostics",
                  "typeHandlerVersion": "1.5",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount": "[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey": "[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint": "https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. <span data-ttu-id="2df02-163">Hello 크기 집합 hello 크기 집합의 hello 머신에서 hello 프로세서 사용량에 따라 조정 방법을 정의 하는 hello autoscaleSettings 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-163">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on hello processor usage on hello machines in hello scale set.</span></span>

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
                  "metricName": "\\Processor(_Total)\\% Processor Time",
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

    <span data-ttu-id="2df02-164">이 자습서의 경우 다음 값이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-164">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="2df02-165">**metricName**</span><span class="sxs-lookup"><span data-stu-id="2df02-165">**metricName**</span></span>  
    <span data-ttu-id="2df02-166">이 값은 hello wadperfcounter 변수에 정의한 hello 성능 카운터와 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-166">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="2df02-167">해당 변수를 사용 하 여 진단 확장 hello 수집 hello **Processor(_Total)\% 프로세서 시간** 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-167">Using that variable, hello Diagnostics extension collects hello  **Processor(_Total)\% Processor Time** counter.</span></span>
    
    * <span data-ttu-id="2df02-168">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="2df02-168">**metricResourceUri**</span></span>  
    <span data-ttu-id="2df02-169">이 값은 hello 가상 컴퓨터 크기 집합의 hello 리소스 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-169">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="2df02-170">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="2df02-170">**timeGrain**</span></span>  
    <span data-ttu-id="2df02-171">이 값은 hello 메트릭을 수집 하는 hello 세분성입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-171">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="2df02-172">이 서식 파일에서 설정 tooone 분입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-172">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="2df02-173">**statistic**</span><span class="sxs-lookup"><span data-stu-id="2df02-173">**statistic**</span></span>  
    <span data-ttu-id="2df02-174">이 값 hello 메트릭은 결합된 tooaccommodate hello 자동 작업 크기 조정 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-174">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="2df02-175">hello 가능한 값은: 평균, 최소값, 최대값입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-175">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="2df02-176">이 서식 파일에서 hello 총 CPU 사용량의 hello 가상 컴퓨터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-176">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>
    
    * <span data-ttu-id="2df02-177">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="2df02-177">**timeWindow**</span></span>  
    <span data-ttu-id="2df02-178">이 값은 hello 인스턴스 데이터를 수집 하는 시간 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-178">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="2df02-179">5분에서 12시간 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-179">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="2df02-180">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="2df02-180">**timeAggregation**</span></span>  
    <span data-ttu-id="2df02-181">그의 값은 시간이 지남에 따라 수집 되는 hello 데이터를 결합 하는 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-181">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="2df02-182">hello 기본값은 평균입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-182">hello default value is Average.</span></span> <span data-ttu-id="2df02-183">hello 가능한 값은: 평균, 최소값, 최대값, 마지막, 합계, 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-183">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="2df02-184">**operator**</span><span class="sxs-lookup"><span data-stu-id="2df02-184">**operator**</span></span>  
    <span data-ttu-id="2df02-185">이 값은 hello 연산자가 사용 되는 toocompare hello 메트릭 데이터와 hello 임계값입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-185">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="2df02-186">hello 가능한 값은: Equals, NotEquals, 보다 큼, GreaterThanOrEqual, LessThan, LessThanOrEqual 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-186">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="2df02-187">**threshold**</span><span class="sxs-lookup"><span data-stu-id="2df02-187">**threshold**</span></span>  
    <span data-ttu-id="2df02-188">이 값은 hello 크기 조정 작업을 트리거하는 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-188">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="2df02-189">이 서식 파일에서 컴퓨터 toohello에 크기 집합 hello 평균 CPU 사용량이 hello 집합의 컴퓨터에 50% 초과 하는 경우 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-189">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="2df02-190">**direction**</span><span class="sxs-lookup"><span data-stu-id="2df02-190">**direction**</span></span>  
    <span data-ttu-id="2df02-191">이 값은 hello 임계값이 작업을 수행 하는 경우 수행 하는 hello 동작을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-191">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="2df02-192">hello 가능한 값은 증가 또는 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-192">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="2df02-193">이 서식 파일에서 hello hello 크기 집합의 가상 컴퓨터 수가 증가 hello 임계값 hello 정의 된 기간에 50% 이상인 경우.</span><span class="sxs-lookup"><span data-stu-id="2df02-193">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>
    
    * <span data-ttu-id="2df02-194">**type**</span><span class="sxs-lookup"><span data-stu-id="2df02-194">**type**</span></span>  
    <span data-ttu-id="2df02-195">이 값은 hello 유형의 동작을 발생 해야 하며 tooChangeCount 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-195">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="2df02-196">**값**</span><span class="sxs-lookup"><span data-stu-id="2df02-196">**value**</span></span>  
    <span data-ttu-id="2df02-197">이 값은 추가 되거나 hello 크기 집합에서 제거 된 가상 컴퓨터의 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-197">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="2df02-198">이 값은 1 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-198">This value must be 1 or greater.</span></span> <span data-ttu-id="2df02-199">hello 기본값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-199">hello default value is 1.</span></span> <span data-ttu-id="2df02-200">이 서식 파일에서 hello 규모에 맞게 컴퓨터 hello 수 hello 임계값이 충족 하는 경우 1 씩 증가 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-200">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>
    
    * <span data-ttu-id="2df02-201">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="2df02-201">**cooldown**</span></span>  
    <span data-ttu-id="2df02-202">이 값은 hello 시간 toowait hello 마지막 크기 조정 작업 이후 hello 다음 작업이 발생 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="2df02-202">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="2df02-203">이 값은 1분에서 1주 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-203">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="2df02-204">Hello 서식 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-204">Save hello template file.</span></span>    

## <a name="step-4-upload-hello-template-toostorage"></a><span data-ttu-id="2df02-205">4 단계: hello 템플릿 toostorage 업로드</span><span class="sxs-lookup"><span data-stu-id="2df02-205">Step 4: Upload hello template toostorage</span></span>
<span data-ttu-id="2df02-206">hello 이름과 1 단계에서 만든 hello 저장소 계정의 기본 키를 알고으로 hello 서식 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-206">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="2df02-207">Hello Microsoft Azure PowerShell 창에서 1 단계에서 만든 hello 저장소 계정의 hello 이름을 지정 하는 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-207">In hello Microsoft Azure PowerShell window, set a variable that specifies hello name of hello storage account that you created in step 1.</span></span>
   
    ```powershell
    $storageAccountName = "vmstestsa"
    ```

2. <span data-ttu-id="2df02-208">Hello hello 저장소 계정의 기본 키를 지정 하는 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-208">Set a variable that specifies hello primary key of hello storage account.</span></span>
   
    ```powershell
    $storageAccountKey = "<primary-account-key>"
    ```
   
   <span data-ttu-id="2df02-209">저장소 계정 리소스 hello hello Azure 포털에서에서 볼 때 hello 열쇠 아이콘을 클릭 하 여이 키를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-209">You can get this key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span>
3. <span data-ttu-id="2df02-210">hello 스토리지 계정으로 사용 되는 toovalidate 작업 하는 hello 저장소 계정 컨텍스트 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-210">Create hello storage account context object that is used toovalidate operations with hello storage account.</span></span>
   
    ```powershell
    $ctx = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
    ```

4. <span data-ttu-id="2df02-211">Hello 서식 파일을 저장 하기 위한 hello 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-211">Create hello container for storing hello template.</span></span>

    ```powershell
    $containerName = "templates"
    New-AzureStorageContainer -Name $containerName -Context $ctx  -Permission Blob
    ```

5. <span data-ttu-id="2df02-212">Hello toohello 새 컨테이너 템플릿 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-212">Upload hello template file toohello new container.</span></span>

    ```powershell   
    $blobName = "VMSSTemplate.json"
    $fileName = "C:\" + $BlobName
    Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob  $blobName -Context $ctx
    ```

## <a name="step-5-deploy-hello-template"></a><span data-ttu-id="2df02-213">5 단계: 배포 hello 서식 파일</span><span class="sxs-lookup"><span data-stu-id="2df02-213">Step 5: Deploy hello template</span></span>
<span data-ttu-id="2df02-214">Hello 서식 파일을 만든 했으므로 hello 리소스 배포를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-214">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="2df02-215">이 명령은 toostart hello 프로세스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-215">Use this command toostart hello process:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name "vmsstestdp1" -ResourceGroupName "vmsstestrg1" -TemplateUri "https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json"
```

<span data-ttu-id="2df02-216">키를 누르면 입력을 hello 변수 할당에 대 한 증명된 tooprovide 값 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-216">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="2df02-217">다음 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-217">Provide these values:</span></span>

```powershell
vmName: vmsstestvm1
  vmSSName: vmsstest1
  instanceCount: 5
  adminUserName: vmadmin1
  adminPassword: VMpass1
  resourcePrefix: vmsstest
```

<span data-ttu-id="2df02-218">모든 hello 리소스 toosuccessfully 배포에 대 일 분 정도 취해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-218">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="2df02-219">Hello 포털의 기능 toodeploy hello 리소스를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-219">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="2df02-220">다음 링크를 사용합니다. "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"</span><span class="sxs-lookup"><span data-stu-id="2df02-220">Use this link: "https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>"</span></span>
> 
> 

## <a name="step-6-monitor-resources"></a><span data-ttu-id="2df02-221">6단계: 리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="2df02-221">Step 6: Monitor resources</span></span>
<span data-ttu-id="2df02-222">이러한 메서드를 사용하여 가상 컴퓨터 규모 집합에 대한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-222">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="2df02-223">Azure 포털 hello-현재 제한 된 양의 hello 포털을 사용 하 여 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-223">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>
* <span data-ttu-id="2df02-224">hello [Azure 리소스 탐색기](https://resources.azure.com/) -이 도구는 hello hello 크기 집합의 현재 상태를 탐색에 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-224">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="2df02-225">이 경로 따라 하 고 hello 눈금의 hello 인스턴스 보기 설정 하 여 만든 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-225">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    <span data-ttu-id="2df02-226">구독 > {사용자의 구독} > resourceGroups > vmsstestrg1 > 공급자 > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span><span class="sxs-lookup"><span data-stu-id="2df02-226">subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines</span></span>

* <span data-ttu-id="2df02-227">Azure PowerShell-이 명령은 tooget 일부 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-227">Azure PowerShell - Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
  ```
  
  <span data-ttu-id="2df02-228">또는</span><span class="sxs-lookup"><span data-stu-id="2df02-228">Or</span></span>
  
  ```powershell
  Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceView
  ```

* <span data-ttu-id="2df02-229">Hello 눈금 집합 toomonitor 개별 프로세스에 hello 가상 컴퓨터에 원격으로 액세스할 수 있습니다 및 다른 컴퓨터는 것 처럼 toohello 별도 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-229">Connect toohello separate virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="2df02-230">규모 집합에 대한 정보를 얻기 위해 전체 REST API를 [가상 컴퓨터 규모 집합](https://msdn.microsoft.com/library/mt589023.aspx)</span><span class="sxs-lookup"><span data-stu-id="2df02-230">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx)</span></span>

## <a name="step-7-remove-hello-resources"></a><span data-ttu-id="2df02-231">7 단계: hello 리소스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-231">Step 7: Remove hello resources</span></span>
<span data-ttu-id="2df02-232">Azure에서 사용 되는 리소스에 대 한 요금이 청구 되므로 항상 것은 더 이상 필요 없는 것이 좋습니다 toodelete 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-232">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="2df02-233">각 리소스는 리소스 그룹에서 별도로 toodelete을 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-233">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="2df02-234">Hello 리소스 그룹을 삭제할 수 있습니다 및 모든 리소스를 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-234">You can delete hello resource group and all its resources are automatically deleted.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name vmsstestrg1
  ```

<span data-ttu-id="2df02-235">리소스 그룹 tookeep을 원하는 경우 hello에 크기 집합만 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-235">If you want tookeep your resource group, you can delete hello scale set only.</span></span>

  ```powershell
  Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name"
  ```

## <a name="next-steps"></a><span data-ttu-id="2df02-236">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2df02-236">Next steps</span></span>
* <span data-ttu-id="2df02-237">관리 방금 hello 크기 집합의 hello 정보를 사용 하 여 만든 [가상 컴퓨터 크기 집합의 가상 컴퓨터를 관리](virtual-machine-scale-sets-windows-manage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2df02-237">Manage hello scale set that you just created using hello information in [Manage virtual machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-manage.md).</span></span>
* <span data-ttu-id="2df02-238">[가상 컴퓨터 확장 집합을 사용하여 수직 자동 크기 조정](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span><span class="sxs-lookup"><span data-stu-id="2df02-238">Learn more about vertical scaling by reviewing [Vertical autoscale with Virtual Machine Scale sets](virtual-machine-scale-sets-vertical-scale-reprovision.md)</span></span>
* <span data-ttu-id="2df02-239">[Azure Monitor PowerShell 빠른 시작 샘플](../monitoring-and-diagnostics/insights-powershell-samples.md)에서 Azure Monitor 모니터링 기능 예제를 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="2df02-239">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>
* <span data-ttu-id="2df02-240">알림 기능에 대 한 자세한 내용은 [Azure 모니터에서 자동 크기 조정 작업 toosend 전자 메일 및 webhook 경고 알림 사용](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="2df02-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="2df02-241">너무 방법에 대해 알아봅니다[Azure 모니터에서 사용 하 여 감사 로그를 toosend webhook 및 전자 메일 경고 알림](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="2df02-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

