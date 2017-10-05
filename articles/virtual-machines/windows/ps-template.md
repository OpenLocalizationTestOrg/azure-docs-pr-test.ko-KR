---
title: "Azure에서 템플릿을 사용하여 Windows VM 만들기 | Microsoft Docs"
description: "Resource Manager 템플릿 및 PowerShell을 사용하여 새 Windows VM을 쉽게 만들 수 있습니다."
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
ms.openlocfilehash: ddab80262fe27c1f5995858ec7de75d7c46df081
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="ef5b7-103">Resource Manager 템플릿을 사용하여 Windows 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="ef5b7-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="ef5b7-104">이 문서에서는 PowerShell을 사용하여 Azure Resource Manager 템플릿을 배포하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-104">This article shows you how to deploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="ef5b7-105">만든 템플릿은 단일 서브넷을 사용하는 새 가상 네트워크에서 Windows Server를 실행하는 단일 가상 컴퓨터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-105">The template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="ef5b7-106">가상 컴퓨터 리소스에 대한 자세한 설명은 [Azure Resource Manager 템플릿의 가상 컴퓨터](template-description.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="ef5b7-107">템플릿에 있는 모든 리소스에 대한 자세한 내용은 [Azure Resource Manager 템플릿 연습](../../azure-resource-manager/resource-manager-template-walkthrough.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="ef5b7-108">이 문서의 단계를 수행하려면 약 5분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-108">It should take about five minutes to do the steps in this article.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="ef5b7-109">Azure Powershell 설치</span><span class="sxs-lookup"><span data-stu-id="ef5b7-109">Install Azure PowerShell</span></span>

<span data-ttu-id="ef5b7-110">최신 버전의 Azure PowerShell 설치, 구독 선택, 자신의 계정에 로그인하는 방법에 대해서는 [Azure PowerShell 설치 및 구성 방법](../../powershell-install-configure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-110">See [How to install and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="ef5b7-111">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ef5b7-111">Create a resource group</span></span>

<span data-ttu-id="ef5b7-112">모든 리소스는 [리소스 그룹](../../azure-resource-manager/resource-group-overview.md)에 배포되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="ef5b7-113">리소스를 만들 수 있는 사용 가능한 위치 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="ef5b7-114">선택한 위치에서 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-114">Create the resource group in the location that you select.</span></span> <span data-ttu-id="ef5b7-115">이 예제에서는 **미국 서부** 지역에 **myResourceGroup**이라는 이름의 리소스 그룹을 만드는 과정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-115">This example shows the creation of a resource group named **myResourceGroup** in the **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-the-files"></a><span data-ttu-id="ef5b7-116">파일 만들기</span><span class="sxs-lookup"><span data-stu-id="ef5b7-116">Create the files</span></span>

<span data-ttu-id="ef5b7-117">이 단계에서는 리소스를 배포하는 템플릿 파일과 템플릿에 매개 변수 값을 제공하는 매개 변수 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-117">In this step, you create a template file that deploys the resources and a parameters file that supplies parameter values to the template.</span></span> <span data-ttu-id="ef5b7-118">또한 Azure Resource Manager 작업을 수행하는 데 사용되는 권한 부여 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-118">You also create an authorization file that is used to perform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="ef5b7-119">*CreateVMTemplate.json*이라는 파일을 만들고 이 JSON 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-119">Create a file named *CreateVMTemplate.json* and add this JSON code to it:</span></span>

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

2. <span data-ttu-id="ef5b7-120">*Parameters.json*이라는 파일을 만들고 이 JSON 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-120">Create a file named *Parameters.json* and add this JSON code to it:</span></span>

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

3. <span data-ttu-id="ef5b7-121">새 저장소 계정 및 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="ef5b7-121">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="ef5b7-122">저장소 계정에 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-122">Upload the files to the storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="ef5b7-123">-File 경로를 파일을 저장한 위치로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-123">Change the -File paths to the location where you stored the files.</span></span>

## <a name="create-the-resources"></a><span data-ttu-id="ef5b7-124">리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="ef5b7-124">Create the resources</span></span>

<span data-ttu-id="ef5b7-125">매개 변수를 사용하여 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="ef5b7-125">Deploy the template using the parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="ef5b7-126">로컬 파일에서 템플릿 및 매개 변수를 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-126">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="ef5b7-127">자세한 내용은 [Azure Storage와 함께 Azure PowerShell 사용](../../storage/common/storage-powershell-guide-full.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-127">To learn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef5b7-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef5b7-128">Next Steps</span></span>

- <span data-ttu-id="ef5b7-129">배포에 문제가 있는 경우 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](../../resource-manager-common-deployment-errors.md)을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-129">If there were issues with the deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="ef5b7-130">[Azure PowerShell 모듈을 사용하여 Windows VM 만들기 및 관리](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 가상 컴퓨터를 만들고 관리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ef5b7-130">Learn how to create and manage a virtual machine in [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

