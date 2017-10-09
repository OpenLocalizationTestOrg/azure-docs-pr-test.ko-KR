---
title: "고정 공용 IP 주소-Azure 리소스 관리자 템플릿 사용 하 여 VM aaaCreate | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿을 사용 하 여 toocreate 고정 공용 IP 사용 하 여 VM을 해결 하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a><span data-ttu-id="f4ad2-103">Azure Resource Manager 템플릿을 사용하여 고정 공용 IP 주소를 사용하는 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="f4ad2-103">Create a VM with a static public IP address using an Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4ad2-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f4ad2-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="f4ad2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4ad2-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="f4ad2-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f4ad2-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="f4ad2-107">템플릿</span><span class="sxs-lookup"><span data-stu-id="f4ad2-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="f4ad2-108">PowerShell(클래식)</span><span class="sxs-lookup"><span data-stu-id="f4ad2-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="f4ad2-109">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f4ad2-110">이 문서에서는 Microsoft hello 클래식 배포 모델 대신 대부분의 새 배포에 권장 하는 hello 리소스 관리자 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a><span data-ttu-id="f4ad2-111">템플릿 파일의 공용 IP 주소 리소스</span><span class="sxs-lookup"><span data-stu-id="f4ad2-111">Public IP address resources in a template file</span></span>
<span data-ttu-id="f4ad2-112">보고 하 고 hello 다운로드 [샘플 템플릿](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-112">You can view and download hello [sample template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).</span></span>

<span data-ttu-id="f4ad2-113">hello 다음 단원에서는 hello 공용 IP 리소스에 위의 hello 시나리오에 따라의 hello 정의:</span><span class="sxs-lookup"><span data-stu-id="f4ad2-113">hello following section shows hello definition of hello public IP resource, based on hello scenario above:</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

<span data-ttu-id="f4ad2-114">공지 hello **publicIPAllocationMethod** 너무 설정 된 속성*정적*합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-114">Notice hello **publicIPAllocationMethod** property, which is set too*Static*.</span></span> <span data-ttu-id="f4ad2-115">이 속성은 *동적*(기본값) 또는 *고정*이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-115">This property can be either *Dynamic* (default value) or *Static*.</span></span> <span data-ttu-id="f4ad2-116">할당 hello 공용 IP 주소가 변경 되지 않을 것임 toostatic 보장 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-116">Setting it toostatic guarantees that hello public IP address assigned will never change.</span></span>

<span data-ttu-id="f4ad2-117">hello 다음 단원에서는 hello 공용 IP 주소는 네트워크 인터페이스와 hello 연결:</span><span class="sxs-lookup"><span data-stu-id="f4ad2-117">hello following section shows hello association of hello public IP address with a network interface:</span></span>

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

<span data-ttu-id="f4ad2-118">공지 hello **publicIPAddress** toohello 가리키는 속성 **Id** 명명 된 리소스의 **variables('webVMSetting').pipName**합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-118">Notice hello **publicIPAddress** property pointing toohello **Id** of a resource named **variables('webVMSetting').pipName**.</span></span> <span data-ttu-id="f4ad2-119">위에 표시 된 hello 공용 IP 리소스의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-119">That is hello name of hello public IP resource shown above.</span></span>

<span data-ttu-id="f4ad2-120">위의 hello 네트워크 인터페이스 hello에 나열 된 마지막으로, **networkProfile** hello 만들려는 VM의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-120">Finally, hello network interface above is listed in hello **networkProfile** property of hello VM being created.</span></span>

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="f4ad2-121">Hello 템플릿을 사용 하 여 배포 toodeploy 클릭</span><span class="sxs-lookup"><span data-stu-id="f4ad2-121">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="f4ad2-122">hello 공용 저장소에서 사용할 수 있는 hello 샘플 템플릿 hello 기본 사용 되는 값 toogenerate hello 위에서 언급 한 시나리오를 포함 하는 매개 변수 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-122">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="f4ad2-123">toodeploy toodeploy를 클릭 하 여 사용 하 여이 템플릿을 클릭 **tooAzure 배포** hello에 대 한 hello Readme.md 파일에 [정적 PIP 사용 하 여 VM](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) 템플릿.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-123">toodeploy this template using click toodeploy, click **Deploy tooAzure** in hello Readme.md file for hello [VM with static PIP](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) template.</span></span> <span data-ttu-id="f4ad2-124">원하는 경우 hello 기본 매개 변수 값을 대체 하 고 hello 빈 매개 변수에 대 한 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-124">Replace hello default parameter values if desired and enter values for hello blank parameters.</span></span>  <span data-ttu-id="f4ad2-125">Hello 포털 toocreate 고정 공용 IP 주소를 사용 하는 가상 컴퓨터의에서 hello 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-125">Follow hello instructions in hello portal toocreate a virtual machine with a static public IP address.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="f4ad2-126">PowerShell을 사용 하 여 hello 서식 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-126">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="f4ad2-127">PowerShell을 사용 하 여 다운로드 한 toodeploy hello 템플릿을 다음 hello 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-127">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="f4ad2-128">Azure PowerShell을 처음 사용 하는 경우 전체 hello hello의 단계를 [어떻게 tooInstall 및 Azure PowerShell 구성](/powershell/azure/overview) 문서.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-128">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="f4ad2-129">PowerShell 콘솔에서 실행 hello `New-AzureRmResourceGroup` cmdlet toocreate 필요한 경우 새 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-129">In a PowerShell console, run hello `New-AzureRmResourceGroup` cmdlet toocreate a new resource group, if necessary.</span></span> <span data-ttu-id="f4ad2-130">만든 리소스 그룹을 이미 있는 경우에 3 toostep을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-130">If you already have a resource group created, go toostep 3.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    <span data-ttu-id="f4ad2-131">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="f4ad2-131">Expected output:</span></span>
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. <span data-ttu-id="f4ad2-132">PowerShell 콘솔에서 실행 hello `New-AzureRmResourceGroupDeployment` cmdlet toodeploy hello 템플릿.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-132">In a PowerShell console, run hello `New-AzureRmResourceGroupDeployment` cmdlet toodeploy hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    <span data-ttu-id="f4ad2-133">예상 출력:</span><span class="sxs-lookup"><span data-stu-id="f4ad2-133">Expected output:</span></span>
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="f4ad2-134">Hello Azure CLI를 사용 하 여 hello 서식 파일을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-134">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="f4ad2-135">toodeploy hello Azure CLI, 단계를 수행 하는 전체 hello 사용 하 여 서식 파일을 hello:</span><span class="sxs-lookup"><span data-stu-id="f4ad2-135">toodeploy hello template by using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="f4ad2-136">Azure CLI 처음 사용 하는 경우에서 다음과 같이 hello hello [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md) tooinstall 문서를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-136">If you have never used Azure CLI, follow hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article tooinstall and configure it.</span></span>
2. <span data-ttu-id="f4ad2-137">Hello 실행 `azure config mode` 명령 tooswitch tooResource 관리자 모드에서는 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-137">Run hello `azure config mode` command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="f4ad2-138">hello 예상 위의 hello 명령에 대 한 출력:</span><span class="sxs-lookup"><span data-stu-id="f4ad2-138">hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="f4ad2-139">열기 hello [매개 변수 파일](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), 해당 콘텐츠를 선택 하 고 컴퓨터에 tooa 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-139">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), select its content, and save it tooa file in your computer.</span></span> <span data-ttu-id="f4ad2-140">예를 들어 hello 매개 변수가 라는 tooa 파일이 저장 되 *parameters.json*합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-140">For this example, hello parameters are saved tooa file named *parameters.json*.</span></span> <span data-ttu-id="f4ad2-141">Hello 매개 변수 값을 원하는 경우 hello 파일 내에서 변경 있지만 여기에 최소한 것이 좋습니다 hello hello는 adminPassword 매개 변수 tooa 고유, 복잡 한 암호 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-141">Change hello parameter values within hello file if desired, but at a minimum, it's recommended that you change hello value for hello adminPassword parameter tooa unique, complex password.</span></span>
4. <span data-ttu-id="f4ad2-142">Hello 실행 `azure group deployment create` cmd toodeploy hello hello 템플릿 및 매개 변수를 사용 하 여 새 VNet이 파일 다운로드 하 고 위에서 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-142">Run hello `azure group deployment create` cmd toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="f4ad2-143">Hello 명령 아래에서 <path> hello 경로로 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4ad2-143">In hello command below, replace <path> with hello path you saved hello file to.</span></span> 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    <span data-ttu-id="f4ad2-144">예상 출력(사용한 매개 변수 값 나열):</span><span class="sxs-lookup"><span data-stu-id="f4ad2-144">Expected output (lists parameter values used):</span></span>

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

