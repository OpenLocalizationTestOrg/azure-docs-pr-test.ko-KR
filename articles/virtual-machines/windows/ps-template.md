---
title: "Azure에서 서식 파일에서 Windows VM aaaCreate | Microsoft Docs"
description: "리소스 관리자 템플릿을 사용 하 여 및 PowerShell tooeasily 새로운 Windows VM을 생성 합니다."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19129d61-8c04-4aa9-a01f-361a09466805
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 630111482c7dc046091632e2ed458ac143325d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="feb83-103">Resource Manager 템플릿을 사용하여 Windows 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="feb83-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="feb83-104">이 문서에서는 Azure 리소스 관리자 toodeploy PowerShell을 사용 하 여 템플릿을 합니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-104">This article shows you how toodeploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="feb83-105">만든 hello 템플릿을 단일 서브넷으로 새 가상 네트워크에서 Windows Server를 실행 하는 단일 가상 컴퓨터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="feb83-106">에 대 한 자세한 설명은 hello 가상 컴퓨터 리소스를 참조 하세요. [가상 컴퓨터는 Azure 리소스 관리자 템플릿](template-description.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="feb83-107">서식 파일의 모든 hello 리소스에 대 한 자세한 내용은 참조 [Azure 리소스 관리자 템플릿 연습](../../azure-resource-manager/resource-manager-template-walkthrough.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="feb83-108">이 문서의 단계를 toodo hello 5 분 정도 걸리는 합니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-108">It should take about five minutes toodo hello steps in this article.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="feb83-109">Azure Powershell 설치</span><span class="sxs-lookup"><span data-stu-id="feb83-109">Install Azure PowerShell</span></span>

<span data-ttu-id="feb83-110">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](../../powershell-install-configure.md) hello 최신 버전의 Azure PowerShell을 설치, 구독을 선택 하 고 tooyour 계정에 로그인 하는 방법에 대 한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-110">See [How tooinstall and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="feb83-111">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="feb83-111">Create a resource group</span></span>

<span data-ttu-id="feb83-112">모든 리소스는 [리소스 그룹](../../azure-resource-manager/resource-group-overview.md)에 배포되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="feb83-113">리소스를 만들 수 있는 사용 가능한 위치 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="feb83-114">Hello 리소스 그룹을 선택 하는 hello 위치에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-114">Create hello resource group in hello location that you select.</span></span> <span data-ttu-id="feb83-115">이 예제에는 명명 된 리소스 그룹의 hello 만드는 방법을 보여 줍니다. **myResourceGroup** hello에 **West US** 위치:</span><span class="sxs-lookup"><span data-stu-id="feb83-115">This example shows hello creation of a resource group named **myResourceGroup** in hello **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-hello-files"></a><span data-ttu-id="feb83-116">Hello 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="feb83-116">Create hello files</span></span>

<span data-ttu-id="feb83-117">이 단계에서는 hello 리소스를 배포 하는 템플릿 파일 및 매개 변수 값 toohello 서식 파일을 제공 하는 매개 변수 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-117">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="feb83-118">권한 부여 되는 파일을 사용 하는 tooperform Azure 리소스 관리자 작업을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-118">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="feb83-119">라는 파일을 만들어 *CreateVMTemplate.json* 이 JSON 코드 tooit 추가:</span><span class="sxs-lookup"><span data-stu-id="feb83-119">Create a file named *CreateVMTemplate.json* and add this JSON code tooit:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
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
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

2. <span data-ttu-id="feb83-120">라는 파일을 만들어 *Parameters.json* 이 JSON 코드 tooit 추가:</span><span class="sxs-lookup"><span data-stu-id="feb83-120">Create a file named *Parameters.json* and add this JSON code tooit:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

3. <span data-ttu-id="feb83-121">새 저장소 계정 및 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="feb83-121">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="feb83-122">Hello, toohello 저장소 계정 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-122">Upload hello files toohello storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="feb83-123">변경 hello-파일 경로 toohello 위치 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-123">Change hello -File paths toohello location where you stored hello files.</span></span>

## <a name="create-hello-resources"></a><span data-ttu-id="feb83-124">Hello 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="feb83-124">Create hello resources</span></span>

<span data-ttu-id="feb83-125">Hello 매개 변수를 사용 하 여 hello 템플릿을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-125">Deploy hello template using hello parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="feb83-126">로컬 파일에서 템플릿 및 매개 변수를 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-126">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="feb83-127">toolearn 더 참조 [Azure 저장소와 Azure PowerShell을 사용 하 여](../../storage/common/storage-powershell-guide-full.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-127">toolearn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="feb83-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="feb83-128">Next Steps</span></span>

- <span data-ttu-id="feb83-129">살펴보면 걸리는 hello 배포 문제가 있는 경우 [Azure 리소스 관리자와 일반적인 Azure 배포 오류 문제 해결](../../resource-manager-common-deployment-errors.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-129">If there were issues with hello deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="feb83-130">자세한 내용은 어떻게 toocreate에 가상 컴퓨터를 관리 하 고 [만들기 hello Azure PowerShell 모듈을 사용 하 여 Windows Vm을 관리 하 고](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="feb83-130">Learn how toocreate and manage a virtual machine in [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

