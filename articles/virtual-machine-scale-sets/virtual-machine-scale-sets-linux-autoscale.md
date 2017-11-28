---
title: "Linux 가상 컴퓨터 크기 집합 aaaAutoscale | Microsoft Docs"
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
ms.openlocfilehash: 4352b94ec2973c37bc5616e3be25bd0c9442632b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="f6bd6-103">가상 컴퓨터 크기 집합에서 Linux 컴퓨터 자동 확장</span><span class="sxs-lookup"><span data-stu-id="f6bd6-103">Automatically scale Linux machines in a virtual machine scale set</span></span>
<span data-ttu-id="f6bd6-104">가상 컴퓨터 크기 집합에 더 쉽게 있습니다 toodeploy 고 집합으로 동일한 가상 컴퓨터를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="f6bd6-105">규모 집합은 대규모 응용 프로그램에 대한 높은 확장성과 사용자 지정 가능한 계산 계층을 제공하고 Windows 플랫폼 이미지, Linux 플랫폼 이미지, 사용자 지정 이미지 및 확장을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="f6bd6-106">toolearn 더 참조 [가상 컴퓨터 크기 조정 설정 개요](virtual-machine-scale-sets-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-106">toolearn more, see [Virtual Machine Scale Sets Overview](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="f6bd6-107">이 자습서 toocreate 소수 hello Ubuntu Linux의 최신 버전을 사용 하 여 Linux 가상 컴퓨터의 설정 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-107">This tutorial shows you how toocreate a scale set of Linux virtual machines using hello latest version of Ubuntu Linux.</span></span> <span data-ttu-id="f6bd6-108">hello 자습서도에서는 tooautomatically 배율 hello 컴퓨터 hello에 설정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-108">hello tutorial also shows you how tooautomatically scale hello machines in hello set.</span></span> <span data-ttu-id="f6bd6-109">Azure 리소스 관리자 템플릿을 만들고 Azure CLI를 사용 하 여 정책을 배포 하 여 크기 조정 설정 hello 눈금을 만들 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-109">You create hello scale set and set up scaling by creating an Azure Resource Manager template and deploying it using Azure CLI.</span></span> <span data-ttu-id="f6bd6-110">템플릿에 대한 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-110">For more information about templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> <span data-ttu-id="f6bd6-111">크기 집합의 자동 크기 조정에 대 한 더 toolearn 참조 [자동 크기 조정 및 가상 컴퓨터 크기 조정 설정](virtual-machine-scale-sets-autoscale-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-111">toolearn more about automatic scaling of scale sets, see [Automatic scaling and Virtual Machine Scale Sets](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

<span data-ttu-id="f6bd6-112">이 자습서에서는 hello 다음 배포 리소스 및 확장:</span><span class="sxs-lookup"><span data-stu-id="f6bd6-112">In this tutorial, you deploy hello following resources and extensions:</span></span>

* <span data-ttu-id="f6bd6-113">Microsoft.Storage/storageAccounts</span><span class="sxs-lookup"><span data-stu-id="f6bd6-113">Microsoft.Storage/storageAccounts</span></span>
* <span data-ttu-id="f6bd6-114">Microsoft.Network/virtualNetworks</span><span class="sxs-lookup"><span data-stu-id="f6bd6-114">Microsoft.Network/virtualNetworks</span></span>
* <span data-ttu-id="f6bd6-115">Microsoft.Network/publicIPAddresses</span><span class="sxs-lookup"><span data-stu-id="f6bd6-115">Microsoft.Network/publicIPAddresses</span></span>
* <span data-ttu-id="f6bd6-116">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="f6bd6-116">Microsoft.Network/loadBalancers</span></span>
* <span data-ttu-id="f6bd6-117">Microsoft.Network/networkInterfaces</span><span class="sxs-lookup"><span data-stu-id="f6bd6-117">Microsoft.Network/networkInterfaces</span></span>
* <span data-ttu-id="f6bd6-118">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="f6bd6-118">Microsoft.Compute/virtualMachines</span></span>
* <span data-ttu-id="f6bd6-119">Microsoft.Compute/virtualMachineScaleSets</span><span class="sxs-lookup"><span data-stu-id="f6bd6-119">Microsoft.Compute/virtualMachineScaleSets</span></span>
* <span data-ttu-id="f6bd6-120">Microsoft.Insights.VMDiagnosticsSettings</span><span class="sxs-lookup"><span data-stu-id="f6bd6-120">Microsoft.Insights.VMDiagnosticsSettings</span></span>
* <span data-ttu-id="f6bd6-121">Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="f6bd6-121">Microsoft.Insights/autoscaleSettings</span></span>

<span data-ttu-id="f6bd6-122">Resource Manager 리소스에 대한 자세한 내용은 [Azure Resource Manager 및 클래식 배포](../azure-resource-manager/resource-manager-deployment-model.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-122">For more information about Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

<span data-ttu-id="f6bd6-123">이 자습서에서는 hello 단계를 시작 하기 전에 [hello Azure CLI 설치](../cli-install-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-123">Before you get started with hello steps in this tutorial, [install hello Azure CLI](../cli-install-nodejs.md).</span></span>

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a><span data-ttu-id="f6bd6-124">1단계: 리소스 그룹 및 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="f6bd6-124">Step 1: Create a resource group and a storage account</span></span>

1. <span data-ttu-id="f6bd6-125">**TooMicrosoft Azure에 로그인**</span><span class="sxs-lookup"><span data-stu-id="f6bd6-125">**Sign in tooMicrosoft Azure**</span></span>  
<span data-ttu-id="f6bd6-126">명령줄 인터페이스 (Bash, 터미널, 명령 프롬프트)에서 tooResource 관리자 모드를 전환 했다가 [id 사용 하 여 회사 또는 학교 로그](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login)합니다. 대화형 로그인 경험 tooyour Azure 계정에 대 한 hello 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-126">In your command-line interface (Bash, Terminal, Command prompt), switch tooResource Manager mode, and then [log in with your work or school id](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Follow hello prompts for an interactive login experience tooyour Azure account.</span></span>

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > <span data-ttu-id="f6bd6-127">회사 또는 학교 ID 및 2 단계 인증을 사용을 사용 하 여 수행 하는 경우 `azure login -u` hello ID toolog에서 대화형 세션 없이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-127">If you have a work or school ID and you do not have two-factor authentication enabled, use `azure login -u` with hello ID toolog in without an interactive session.</span></span> <span data-ttu-id="f6bd6-128">회사 또는 학교 ID가 없는 경우 [개인 Microsoft 계정에서 회사 또는 학교 ID를 만들 수 있습니다](../active-directory/active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f6bd6-128">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../active-directory/active-directory-users-create-azure-portal.md).</span></span>
    
2. <span data-ttu-id="f6bd6-129">**리소스 그룹 만들기**</span><span class="sxs-lookup"><span data-stu-id="f6bd6-129">**Create a resource group**</span></span>  
<span data-ttu-id="f6bd6-130">모든 리소스를 배포 된 tooa 리소스 그룹이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-130">All resources must be deployed tooa resource group.</span></span> <span data-ttu-id="f6bd6-131">이 자습서에 대 한 hello 리소스 그룹의 이름을 **vmsstest1**합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-131">For this tutorial, name hello resource group **vmsstest1**.</span></span>
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. <span data-ttu-id="f6bd6-132">**저장소 계정 hello 새 리소스 그룹에 배포**</span><span class="sxs-lookup"><span data-stu-id="f6bd6-132">**Deploy a storage account into hello new resource group**</span></span>  
<span data-ttu-id="f6bd6-133">이 저장소 계정은 hello 템플릿이 보관 된입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-133">This storage account is where hello template is stored.</span></span> <span data-ttu-id="f6bd6-134">**vmsstestsa**라는 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-134">Create a storage account named **vmsstestsa**.</span></span>
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-hello-template"></a><span data-ttu-id="f6bd6-135">2 단계: hello 서식 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="f6bd6-135">Step 2: Create hello template</span></span>
<span data-ttu-id="f6bd6-136">Azure 리소스 관리자 템플릿 toodeploy 있습니다 수 있도록 하 고 hello 리소스 및 관련된 배포 매개 변수의 JSON 설명을 사용 하 여 Azure 리소스를 함께 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-136">An Azure Resource Manager template makes it possible for you toodeploy and manage Azure resources together by using a JSON description of hello resources and associated deployment parameters.</span></span>

1. <span data-ttu-id="f6bd6-137">선호 하는 편집기에서 hello 파일 VMSSTemplate.json 만들고 hello 초기 JSON 구조 toosupport hello 템플릿을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-137">In your favorite editor, create hello file VMSSTemplate.json and add hello initial JSON structure toosupport hello template.</span></span>

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

2. <span data-ttu-id="f6bd6-138">매개 변수는 항상 필수 이지만 제공 방법을 tooinput 값 hello 서식 파일이 배포 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-138">Parameters are not always required, but they provide a way tooinput values when hello template is deployed.</span></span> <span data-ttu-id="f6bd6-139">Toohello 템플릿을 추가한 hello 매개 변수 부모 요소 아래에 이러한 매개 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-139">Add these parameters under hello parameters parent element that you added toohello template.</span></span>

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * <span data-ttu-id="f6bd6-140">Hello 눈금에 사용 되는 tooaccess hello 컴퓨터 있는 hello 별도 가상 컴퓨터에 대 한 이름이 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-140">A name for hello separate virtual machine that is used tooaccess hello machines in hello scale set.</span></span>
   * <span data-ttu-id="f6bd6-141">Hello 템플릿이 보관 된 hello 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-141">A name for hello storage account where hello template is stored.</span></span>
   * <span data-ttu-id="f6bd6-142">hello 크기 집합의 hello tooinitially 가상 컴퓨터의 인스턴스 수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-142">hello number of instances of virtual machines tooinitially create in hello scale set.</span></span>
   * <span data-ttu-id="f6bd6-143">이름과 hello 가상 컴퓨터에 대 한 hello 관리자 계정의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-143">A name and password of hello administrator account on hello virtual machines.</span></span>
   * <span data-ttu-id="f6bd6-144">Toosupport hello 눈금 만들어진 hello 리소스에 대 한 이름 접두사를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-144">A name prefix for hello resources that are created toosupport hello scale set.</span></span>

3. <span data-ttu-id="f6bd6-145">변수는 자주 변경 될 수 있는 템플릿 toospecify 값에 사용할 수 있습니다 또는 toobe 해야 하는 값이 매개 변수 값의 조합에서 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-145">Variables can be used in a template toospecify values that may change frequently or values that need toobe created from a combination of parameter values.</span></span> <span data-ttu-id="f6bd6-146">Toohello 템플릿을 추가한 hello 변수 부모 요소 아래에 이러한 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-146">Add these variables under hello variables parent element that you added toohello template.</span></span>

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

   * <span data-ttu-id="f6bd6-147">Hello 네트워크 인터페이스에서 사용 되는 DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-147">DNS names that are used by hello network interfaces.</span></span>
   * <span data-ttu-id="f6bd6-148">hello IP 주소 이름 및 hello 가상 네트워크 및 서브넷에 대 한 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-148">hello IP address names and prefixes for hello virtual network and subnets.</span></span>
   * <span data-ttu-id="f6bd6-149">hello 이름 및 식별자 hello 가상 네트워크의 부하 분산 장치, 및 네트워크 인터페이스.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-149">hello names and identifiers of hello virtual network, load balancer, and network interfaces.</span></span>
   * <span data-ttu-id="f6bd6-150">Hello 크기 집합의 hello 컴퓨터와 연결 된 hello 계정에 대 한 저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-150">Storage account names for hello accounts associated with hello machines in hello scale set.</span></span>
   * <span data-ttu-id="f6bd6-151">Hello hello 가상 컴퓨터에 설치 된 진단 확장에 대 한 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-151">Settings for hello Diagnostics extension that is installed on hello virtual machines.</span></span> <span data-ttu-id="f6bd6-152">Hello 진단 확장에 대 한 자세한 내용은 참조 [모니터링 및 Azure 리소스 관리자 템플릿을 사용 하 여 진단을 사용 하 여 Windows 가상 컴퓨터를 만들](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-152">For more information about hello Diagnostics extension, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

4. <span data-ttu-id="f6bd6-153">Hello 저장소 계정 리소스 toohello 템플릿을 추가한 hello 리소스 부모 요소 아래에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-153">Add hello storage account resource under hello resources parent element that you added toohello template.</span></span> <span data-ttu-id="f6bd6-154">이 템플릿은 hello 운영 체제 디스크 및 진단 데이터 저장 된 다섯 개의 저장소 계정을 권장 루프 toocreate hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-154">This template uses a loop toocreate hello recommended five storage accounts where hello operating system disks and diagnostic data are stored.</span></span> <span data-ttu-id="f6bd6-155">계정의이 집합 hello 현재 최대 크기 집합의 too100 가상 컴퓨터를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-155">This set of accounts can support up too100 virtual machines in a scale set, which is hello current maximum.</span></span> <span data-ttu-id="f6bd6-156">각 저장소 계정은 hello 서식 파일에 대 한 hello 매개 변수에서 제공 하는 hello 접미사와 결합 하는 hello 변수에 정의 된 문자 지정자도 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-156">Each storage account is named with a letter designator that was defined in hello variables combined with hello suffix that you provide in hello parameters for hello template.</span></span>
   
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

5. <span data-ttu-id="f6bd6-157">Hello 가상 네트워크 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-157">Add hello virtual network resource.</span></span> <span data-ttu-id="f6bd6-158">자세한 내용은 [네트워크 리소스 공급자](../virtual-network/resource-groups-networking.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-158">For more information, see [Network Resource Provider](../virtual-network/resource-groups-networking.md).</span></span>

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

6. <span data-ttu-id="f6bd6-159">Hello 공용 IP 주소 리소스 hello에서 사용 되는 부하 분산 장치 및 네트워크 인터페이스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-159">Add hello public IP address resources that are used by hello load balancer and network interface.</span></span>

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

7. <span data-ttu-id="f6bd6-160">Hello 크기 집합에서 사용 되는 hello 부하 분산 장치 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-160">Add hello load balancer resource that is used by hello scale set.</span></span> <span data-ttu-id="f6bd6-161">자세한 내용은 [부하 분산 장치에 대한 Azure 리소스 관리자 지원](../load-balancer/load-balancer-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-161">For more information, see [Azure Resource Manager Support for Load Balancer](../load-balancer/load-balancer-arm.md).</span></span>

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

8. <span data-ttu-id="f6bd6-162">Hello hello 별도 가상 컴퓨터에서 사용 되는 네트워크 인터페이스 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-162">Add hello network interface resource that is used by hello separate virtual machine.</span></span> <span data-ttu-id="f6bd6-163">컴퓨터 크기 집합의 공용 IP 주소를 통해 액세스할 수 없습니다, 때문에 별도 가상 컴퓨터에에서 만들어집니다 hello 동일한 가상 네트워크 tooremotely 액세스 hello 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-163">Because machines in a scale set aren't accessible through a public IP address, a separate virtual machine is created in hello same virtual network tooremotely access hello machines.</span></span>

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

9. <span data-ttu-id="f6bd6-164">Hello hello 크기 집합으로 동일한 네트워크에 hello 별도 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-164">Add hello separate virtual machine in hello same network as hello scale set.</span></span>

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

10. <span data-ttu-id="f6bd6-165">Hello 가상 컴퓨터 크기 집합 리소스를 추가 하 고 hello 크기 집합의 모든 가상 컴퓨터에 설치 되어 있는 hello 진단 확장을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-165">Add hello virtual machine scale set resource and specify hello diagnostics extension that is installed on all virtual machines in hello scale set.</span></span> <span data-ttu-id="f6bd6-166">이 리소스에 대 한 hello 설정 중 대부분 hello 가상 컴퓨터 리소스와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-166">Many of hello settings for this resource are similar with hello virtual machine resource.</span></span> <span data-ttu-id="f6bd6-167">hello 주요 차이점은 hello 크기 집합의 가상 컴퓨터의 hello 수를 지정 하는 hello 용량 요소 및 upgradePolicy 업데이트 toovirtual 컴퓨터 적용 하는 방법을 지정 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-167">hello main differences are hello capacity element that specifies hello number of virtual machines in hello scale set and upgradePolicy that specifies how updates are made toovirtual machines.</span></span> <span data-ttu-id="f6bd6-168">hello 크기 집합 만들어지지 모든 hello 저장소 계정이 생성 될 때까지 hello dependsOn 요소와 지정 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-168">hello scale set is not created until all hello storage accounts are created as specified with hello dependsOn element.</span></span>

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

11. <span data-ttu-id="f6bd6-169">Hello 크기 집합 hello 집합의 hello 컴퓨터의 프로세스 사용량에 따라 조정 방법을 정의 하는 hello autoscaleSettings 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-169">Add hello autoscaleSettings resource that defines how hello scale set adjusts based on processor usage on hello machines in hello set.</span></span>

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
    
    <span data-ttu-id="f6bd6-170">이 자습서의 경우 다음 값이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-170">For this tutorial, these values are important:</span></span>
    
    * <span data-ttu-id="f6bd6-171">**metricName**</span><span class="sxs-lookup"><span data-stu-id="f6bd6-171">**metricName**</span></span>  
    <span data-ttu-id="f6bd6-172">이 값은 hello wadperfcounter 변수에 정의한 hello 성능 카운터와 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-172">This value is hello same as hello performance counter that we defined in hello wadperfcounter variable.</span></span> <span data-ttu-id="f6bd6-173">해당 변수를 사용 하 여 진단 확장 hello 수집 hello **Processor\PercentProcessorTime** 카운터입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-173">Using that variable, hello Diagnostics extension collects hello **Processor\PercentProcessorTime** counter.</span></span>
    
    * <span data-ttu-id="f6bd6-174">**metricResourceUri**</span><span class="sxs-lookup"><span data-stu-id="f6bd6-174">**metricResourceUri**</span></span>  
    <span data-ttu-id="f6bd6-175">이 값은 hello 가상 컴퓨터 크기 집합의 hello 리소스 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-175">This value is hello resource identifier of hello virtual machine scale set.</span></span>
    
    * <span data-ttu-id="f6bd6-176">**timeGrain**</span><span class="sxs-lookup"><span data-stu-id="f6bd6-176">**timeGrain**</span></span>  
    <span data-ttu-id="f6bd6-177">이 값은 hello 메트릭을 수집 하는 hello 세분성입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-177">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="f6bd6-178">이 서식 파일에서 설정 tooone 분입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-178">In this template, it is set tooone minute.</span></span>
    
    * <span data-ttu-id="f6bd6-179">**statistic**</span><span class="sxs-lookup"><span data-stu-id="f6bd6-179">**statistic**</span></span>  
    <span data-ttu-id="f6bd6-180">이 값 hello 메트릭은 결합된 tooaccommodate hello 자동 작업 크기 조정 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-180">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="f6bd6-181">hello 가능한 값은: 평균, 최소값, 최대값입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-181">hello possible values are: Average, Min, Max.</span></span> <span data-ttu-id="f6bd6-182">이 서식 파일에서 hello 총 CPU 사용량의 hello 가상 컴퓨터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-182">In this template, hello average total CPU usage of hello virtual machines is collected.</span></span>

    * <span data-ttu-id="f6bd6-183">**timeWindow**</span><span class="sxs-lookup"><span data-stu-id="f6bd6-183">**timeWindow**</span></span>  
    <span data-ttu-id="f6bd6-184">이 값은 hello 인스턴스 데이터를 수집 하는 시간 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-184">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="f6bd6-185">5분에서 12시간 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-185">It must be between 5 minutes and 12 hours.</span></span>
    
    * <span data-ttu-id="f6bd6-186">**timeAggregation**</span><span class="sxs-lookup"><span data-stu-id="f6bd6-186">**timeAggregation**</span></span>  
    <span data-ttu-id="f6bd6-187">그의 값은 시간이 지남에 따라 수집 되는 hello 데이터를 결합 하는 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-187">his value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="f6bd6-188">hello 기본값은 평균입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-188">hello default value is Average.</span></span> <span data-ttu-id="f6bd6-189">hello 가능한 값은: 평균, 최소값, 최대값, 마지막, 합계, 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-189">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span>
    
    * <span data-ttu-id="f6bd6-190">**operator**</span><span class="sxs-lookup"><span data-stu-id="f6bd6-190">**operator**</span></span>  
    <span data-ttu-id="f6bd6-191">이 값은 hello 연산자가 사용 되는 toocompare hello 메트릭 데이터와 hello 임계값입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-191">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="f6bd6-192">hello 가능한 값은: Equals, NotEquals, 보다 큼, GreaterThanOrEqual, LessThan, LessThanOrEqual 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-192">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span>
    
    * <span data-ttu-id="f6bd6-193">**threshold**</span><span class="sxs-lookup"><span data-stu-id="f6bd6-193">**threshold**</span></span>  
    <span data-ttu-id="f6bd6-194">이 값에는 hello 크기 조정 작업이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-194">This value triggers hello scale action.</span></span> <span data-ttu-id="f6bd6-195">이 서식 파일에서 컴퓨터 toohello에 크기 집합 hello 평균 CPU 사용량이 hello 집합의 컴퓨터에 50% 초과 하는 경우 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-195">In this template, machines are added toohello scale set when hello average CPU usage among machines in hello set is over 50%.</span></span>
    
    * <span data-ttu-id="f6bd6-196">**direction**</span><span class="sxs-lookup"><span data-stu-id="f6bd6-196">**direction**</span></span>  
    <span data-ttu-id="f6bd6-197">이 값은 hello 임계값이 작업을 수행 하는 경우 수행 하는 hello 동작을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-197">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="f6bd6-198">hello 가능한 값은 증가 또는 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-198">hello possible values are Increase or Decrease.</span></span> <span data-ttu-id="f6bd6-199">이 서식 파일에서 hello hello 크기 집합의 가상 컴퓨터 수가 증가 hello 임계값 hello 정의 된 기간에 50% 이상인 경우.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-199">In this template, hello number of virtual machines in hello scale set is increased if hello threshold is over 50% in hello defined time window.</span></span>

    * <span data-ttu-id="f6bd6-200">**type**</span><span class="sxs-lookup"><span data-stu-id="f6bd6-200">**type**</span></span>  
    <span data-ttu-id="f6bd6-201">이 값은 hello 유형의 동작을 발생 해야 하며 tooChangeCount 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-201">This value is hello type of action that should occur and must be set tooChangeCount.</span></span>
    
    * <span data-ttu-id="f6bd6-202">**값**</span><span class="sxs-lookup"><span data-stu-id="f6bd6-202">**value**</span></span>  
    <span data-ttu-id="f6bd6-203">이 값은 추가 되거나 hello 크기 집합에서 제거 된 가상 컴퓨터의 hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-203">This value is hello number of virtual machines that are added or removed from hello scale set.</span></span> <span data-ttu-id="f6bd6-204">이 값은 1 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-204">This value must be 1 or greater.</span></span> <span data-ttu-id="f6bd6-205">hello 기본값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-205">hello default value is 1.</span></span> <span data-ttu-id="f6bd6-206">이 서식 파일에서 hello 규모에 맞게 컴퓨터 hello 수 hello 임계값이 충족 하는 경우 1 씩 증가 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-206">In this template, hello number of machines in hello scale set increases by 1 when hello threshold is met.</span></span>

    * <span data-ttu-id="f6bd6-207">**cooldown**</span><span class="sxs-lookup"><span data-stu-id="f6bd6-207">**cooldown**</span></span>  
    <span data-ttu-id="f6bd6-208">이 값은 hello 시간 toowait hello 마지막 크기 조정 작업 이후 hello 다음 작업이 발생 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-208">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="f6bd6-209">이 값은 1분에서 1주 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-209">This value must be between one minute and one week.</span></span>

12. <span data-ttu-id="f6bd6-210">Hello 서식 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-210">Save hello template file.</span></span>    

## <a name="step-3-upload-hello-template-toostorage"></a><span data-ttu-id="f6bd6-211">3 단계: hello 템플릿 toostorage 업로드</span><span class="sxs-lookup"><span data-stu-id="f6bd6-211">Step 3: Upload hello template toostorage</span></span>
<span data-ttu-id="f6bd6-212">hello 이름과 1 단계에서 만든 hello 저장소 계정의 기본 키를 알고으로 hello 서식 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-212">hello template can be uploaded as long as you know hello name and primary key of hello storage account that you created in step 1.</span></span>

1. <span data-ttu-id="f6bd6-213">명령줄 인터페이스 (Bash, 터미널, 명령 프롬프트)에서 다음이 명령을 실행 tooset hello 환경 변수 tooaccess hello 필요한 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-213">In your command-line interface (Bash, Terminal, Command prompt), run these commands tooset hello environment variables needed tooaccess hello storage account:</span></span>

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    <span data-ttu-id="f6bd6-214">저장소 계정 리소스 hello hello Azure 포털에서에서 볼 때 hello 열쇠 아이콘을 클릭 하 여 hello 키를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-214">You can get hello key by clicking hello key icon when viewing hello storage account resource in hello Azure portal.</span></span> <span data-ttu-id="f6bd6-215">Windows 명령 프롬프트를 사용할 때 export 대신 **set** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-215">When using a Windows command prompt, type **set** instead of export.</span></span>

2. <span data-ttu-id="f6bd6-216">Hello 서식 파일을 저장 하기 위한 hello 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-216">Create hello container for storing hello template.</span></span>
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. <span data-ttu-id="f6bd6-217">Hello toohello 새 컨테이너 템플릿 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-217">Upload hello template file toohello new container.</span></span>
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-hello-template"></a><span data-ttu-id="f6bd6-218">4 단계: 배포 hello 서식 파일</span><span class="sxs-lookup"><span data-stu-id="f6bd6-218">Step 4: Deploy hello template</span></span>
<span data-ttu-id="f6bd6-219">Hello 서식 파일을 만든 했으므로 hello 리소스 배포를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-219">Now that you created hello template, you can start deploying hello resources.</span></span> <span data-ttu-id="f6bd6-220">이 명령은 toostart hello 프로세스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-220">Use this command toostart hello process:</span></span>

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

<span data-ttu-id="f6bd6-221">키를 누르면 입력을 hello 변수 할당에 대 한 증명된 tooprovide 값 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-221">When you press enter, you are prompted tooprovide values for hello variables you assigned.</span></span> <span data-ttu-id="f6bd6-222">다음 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-222">Provide these values:</span></span>

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

<span data-ttu-id="f6bd6-223">모든 hello 리소스 toosuccessfully 배포에 대 일 분 정도 취해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-223">It should take about 15 minutes for all hello resources toosuccessfully be deployed.</span></span>

> [!NOTE]
> <span data-ttu-id="f6bd6-224">Hello 포털의 기능 toodeploy hello 리소스를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-224">You can also use hello portal’s ability toodeploy hello resources.</span></span> <span data-ttu-id="f6bd6-225">다음 링크를 사용합니다. https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template></span><span class="sxs-lookup"><span data-stu-id="f6bd6-225">Use this link: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template></span></span>


## <a name="step-5-monitor-resources"></a><span data-ttu-id="f6bd6-226">5단계: 리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="f6bd6-226">Step 5: Monitor resources</span></span>
<span data-ttu-id="f6bd6-227">이러한 메서드를 사용하여 가상 컴퓨터 규모 집합에 대한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-227">You can get some information about virtual machine scale sets using these methods:</span></span>

* <span data-ttu-id="f6bd6-228">Azure 포털 hello-현재 제한 된 양의 hello 포털을 사용 하 여 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-228">hello Azure portal - You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="f6bd6-229">hello [Azure 리소스 탐색기](https://resources.azure.com/) -이 도구는 hello hello 크기 집합의 현재 상태를 탐색에 가장 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-229">hello [Azure Resource Explorer](https://resources.azure.com/) - This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="f6bd6-230">이 경로 따라 하 고 hello 눈금의 hello 인스턴스 보기 설정 하 여 만든 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-230">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* <span data-ttu-id="f6bd6-231">-Azure CLI 명령을 tooget이 일부 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-231">Azure CLI - Use this command tooget some information:</span></span>

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* <span data-ttu-id="f6bd6-232">Hello 눈금 집합 toomonitor 개별 프로세스에 hello 가상 컴퓨터에 원격으로 액세스할 수 있습니다 및 다른 컴퓨터는 것 처럼 toohello jumpbox 가상 컴퓨터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-232">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

> [!NOTE]
> <span data-ttu-id="f6bd6-233">규모 집합에 대한 정보를 얻기 위해 전체 REST API를 [가상 컴퓨터 크기 규모 집합](https://msdn.microsoft.com/library/mt589023.aspx)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-233">A complete REST API for obtaining information about scale sets can be found in [Virtual Machine Scale Sets](https://msdn.microsoft.com/library/mt589023.aspx).</span></span>

## <a name="step-6-remove-hello-resources"></a><span data-ttu-id="f6bd6-234">6 단계: hello 리소스를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-234">Step 6: Remove hello resources</span></span>
<span data-ttu-id="f6bd6-235">Azure에서 사용 되는 리소스에 대 한 요금이 청구 되므로 항상 것은 더 이상 필요 없는 것이 좋습니다 toodelete 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-235">Because you are charged for resources used in Azure, it is always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="f6bd6-236">각 리소스는 리소스 그룹에서 별도로 toodelete을 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-236">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="f6bd6-237">Hello 리소스 그룹을 삭제할 수 있습니다 및 모든 리소스를 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-237">You can delete hello resource group and all its resources are automatically deleted.</span></span>

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a><span data-ttu-id="f6bd6-238">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6bd6-238">Next steps</span></span>
* <span data-ttu-id="f6bd6-239">[Azure Monitor 플랫폼 간 CLI 빠른 시작 샘플](../monitoring-and-diagnostics/insights-cli-samples.md)에서 Azure Monitor 모니터링 기능 예제를 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-239">Find examples of Azure Monitor monitoring features in [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md)</span></span>
* <span data-ttu-id="f6bd6-240">알림 기능에 대 한 자세한 내용은 [Azure 모니터에서 자동 크기 조정 작업 toosend 전자 메일 및 webhook 경고 알림 사용](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="f6bd6-240">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)</span></span>
* <span data-ttu-id="f6bd6-241">너무 방법에 대해 알아봅니다[Azure 모니터에서 사용 하 여 감사 로그를 toosend webhook 및 전자 메일 경고 알림](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="f6bd6-241">Learn how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>
* <span data-ttu-id="f6bd6-242">체크 아웃 hello [Ubuntu 16.04에서 데모 앱의 자동 크기 조정](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) Python/bottle 앱 tooexercise hello 자동 크기 조정 설정 하는 가상 컴퓨터의 기능을 크기 조정 설정 하는 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="f6bd6-242">Check out hello [Autoscale demo app on Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) template that sets up a Python/bottle app tooexercise hello automatic scaling functionality of Virtual Machine Scale Sets.</span></span>

