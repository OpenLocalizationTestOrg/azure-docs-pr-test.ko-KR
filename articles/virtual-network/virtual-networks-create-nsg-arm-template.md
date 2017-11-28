---
title: "네트워크 보안 그룹 만들기 - Azure Resource Manager 템플릿| Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 네트워크 보안 그룹을 만들고 배포하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: f3e7385d-717c-44ff-be20-f9aa450aa99b
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 88f7e5b2144daee7bf1c8e7312ba98e6fa967899
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a><span data-ttu-id="6df5a-103">Azure Resource Manager 템플릿을 사용하여 네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="6df5a-103">Create network security groups using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="6df5a-104">이 문서에서는 리소스 관리자 배포 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-104">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="6df5a-105">[클래식 배포 모델에서 NSG를 만들](virtual-networks-create-nsg-classic-ps.md)수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-105">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a><span data-ttu-id="6df5a-106">템플릿 파일의 NSG 리소스</span><span class="sxs-lookup"><span data-stu-id="6df5a-106">NSG resources in a template file</span></span>
<span data-ttu-id="6df5a-107">[샘플 템플릿](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json)을 보고 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-107">You can view and download the [sample template](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span></span>

<span data-ttu-id="6df5a-108">다음 섹션에서는 시나리오를 기반으로 프런트 엔드 NSG의 정의를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-108">The following section shows the definition of the front-end NSG, based on the scenario.</span></span>

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Network/networkSecurityGroups",
"name": "[parameters('frontEndNSGName')]",
"location": "[resourceGroup().location]",
"tags": {
  "displayName": "NSG - Front End"
},
"properties": {
  "securityRules": [
    {
      "name": "rdp-rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 100,
        "direction": "Inbound"
      }
    },
    {
      "name": "web-rule",
      "properties": {
        "description": "Allow WEB",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 101,
        "direction": "Inbound"
      }
    }
  ]
}
```
<span data-ttu-id="6df5a-109">프런트 엔드 서브넷에 NSG를 연결하려면 템플릿에서 서브넷 정의를 변경하고 NSG에 대한 참조 ID를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-109">To associate the NSG to the front-end subnet, you have to change the subnet definition in the template, and use the reference id for the NSG.</span></span>

```json
"subnets": [
  {
    "name": "[parameters('frontEndSubnetName')]",
    "properties": {
      "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
      "networkSecurityGroup": {
      "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
      }
    }
  }, 
```

<span data-ttu-id="6df5a-110">템플릿의 백 엔드 NSG 및 백 엔드 서브넷에 대해 동일한 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-110">Notice the same being done for the back-end NSG and the back-end subnet in the template.</span></span>

## <a name="deploy-the-arm-template-by-using-click-to-deploy"></a><span data-ttu-id="6df5a-111">클릭하여 배포하는 방식으로 ARM 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="6df5a-111">Deploy the ARM template by using click to deploy</span></span>
<span data-ttu-id="6df5a-112">공용 저장소에서 사용할 수 있는 샘플 템플릿은 위에 설명된 시나리오를 생성하는 데 사용된 기본값을 포함하는 매개 변수 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-112">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="6df5a-113">클릭하여 배포하는 방식으로 이 템플릿을 배포하려면 [이 링크](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG)에 따라 **Azure에 배포**를 클릭하고 필요한 경우 기본 매개 변수 값을 대체하고 포털의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-113">To deploy this template using click to deploy, follow [this link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-arm-template-by-using-powershell"></a><span data-ttu-id="6df5a-114">PowerShell을 사용하여 ARM 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="6df5a-114">Deploy the ARM template by using PowerShell</span></span>
<span data-ttu-id="6df5a-115">PowerShell을 사용하여 다운로드한 ARM 템플릿을 배포하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-115">To deploy the ARM template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="6df5a-116">Azure PowerShell을 처음 사용하는 경우 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)의 지침을 따라 설치 및 구성을 합니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-116">If you have never used Azure PowerShell, follow the instructions in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) to install and configure it.</span></span>
2. <span data-ttu-id="6df5a-117">**`New-AzureRmResourceGroup`** cmdlet을 실행하고 템플릿을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-117">Run the **`New-AzureRmResourceGroup`** cmdlet to create a resource group using the template.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="6df5a-118">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="6df5a-118">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *                  
   
        Resources         :
                            Name                Type                                     Location
                            ==================  =======================================  ========
                            sqlAvSet            Microsoft.Compute/availabilitySets       westus  
                            webAvSet            Microsoft.Compute/availabilitySets       westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            Web1                Microsoft.Compute/virtualMachines        westus  
                            Web2                Microsoft.Compute/virtualMachines        westus  
                            TestNICSQL1         Microsoft.Network/networkInterfaces      westus  
                            TestNICSQL2         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb1         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb2         Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            TestPIPSQL1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPSQL2         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb2         Microsoft.Network/publicIPAddresses      westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus  
   
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-the-arm-template-by-using-the-azure-cli"></a><span data-ttu-id="6df5a-119">Azure CLI를 사용하여 ARM 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="6df5a-119">Deploy the ARM template by using the Azure CLI</span></span>
<span data-ttu-id="6df5a-120">Azure CLI를 사용하여 ARM 템플릿을 배포하려면 아래 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="6df5a-120">To deploy the ARM template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="6df5a-121">Azure CLI를 처음 사용하는 경우 [Azure CLI 설치 및 구성](../cli-install-nodejs.md) 을 참조하고 Azure 계정 및 구독을 선택하는 부분까지 관련 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-121">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="6df5a-122">아래와 같이 **`azure config mode`** 명령을 실행하여 리소스 관리자 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-122">Run the **`azure config mode`** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="6df5a-123">다음은 위의 명령에 대해 예상된 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-123">The following is the expected output for the command:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="6df5a-124">위에서 다운로드하고 수정한 템플릿 및 매개 변수를 사용하여 새 VNet을 배포하기 위해 **`azure group deployment create`** cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-124">Run the **`azure group deployment create`** cmdlet to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="6df5a-125">출력 다음에 표시되는 목록은 사용되는 매개 변수를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-125">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="6df5a-126">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="6df5a-126">Expected output:</span></span>
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Creating resource group TestRG
        info:    Created resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK
   
   * <span data-ttu-id="6df5a-127">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="6df5a-127">**-n (or --name)**.</span></span> <span data-ttu-id="6df5a-128">만들 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-128">Name of the resource group to be created.</span></span>
   * <span data-ttu-id="6df5a-129">**-l (or --location)**.</span><span class="sxs-lookup"><span data-stu-id="6df5a-129">**-l (or --location)**.</span></span> <span data-ttu-id="6df5a-130">리소스 그룹이 생성되는 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-130">Azure region where the resource group will be created.</span></span>
   * <span data-ttu-id="6df5a-131">**-f (or --template-file)**.</span><span class="sxs-lookup"><span data-stu-id="6df5a-131">**-f (or --template-file)**.</span></span> <span data-ttu-id="6df5a-132">ARM 템플릿 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-132">Path to your ARM template file.</span></span>
   * <span data-ttu-id="6df5a-133">**-e(또는 --parameters-file)**.</span><span class="sxs-lookup"><span data-stu-id="6df5a-133">**-e (or --parameters-file)**.</span></span> <span data-ttu-id="6df5a-134">ARM 매개 변수 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="6df5a-134">Path to your ARM parameters file.</span></span>

