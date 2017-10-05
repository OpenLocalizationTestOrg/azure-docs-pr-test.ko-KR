---
title: "Azure Resource Manager 템플릿을 사용하여 WIndows 계산 리소스 배포 | Microsoft Docs"
description: "Azure 가상 컴퓨터 DotNet Core 자습서"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b026fe81-1bc1-4899-ac32-886091671498
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8a8b888195e52ea9669922a6a00a873025f3c375
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="d8979-103">Windows VM용 Azure Resource Manager 템플릿을 사용하는 응용 프로그램 아키텍처</span><span class="sxs-lookup"><span data-stu-id="d8979-103">Application architecture with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="d8979-104">Azure Resource Manager 배포를 개발할 때 계산 요구 사항을 Azure 리소스 및 서비스에 매핑해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-104">When developing an Azure Resource Manager deployment, compute requirements need to be mapped to Azure resources and services.</span></span> <span data-ttu-id="d8979-105">응용 프로그램이 몇 개의 http 끝점, 데이터베이스 및 데이터 캐싱 서비스로 구성되면 이러한 각 데이터는 구성 요소를 호스트하는 Azure 리소스를 합리적으로 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-105">If an application consists of several http endpoints, a database, and a data caching service, the Azure resources that host each of these components needs to be rationalized.</span></span> <span data-ttu-id="d8979-106">예를 들어 샘플 Music Store 응용 프로그램에는 가상 컴퓨터에 호스트되는 웹 응용 프로그램과 Azure SQL Database에 호스트되는 SQL Database가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-106">For instance, the sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="d8979-107">이 문서에서는 샘플 Azure Resource Manager 템플릿에서 Music Store 계산 리소스를 구성하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-107">This document details how the Music Store compute resources are configured in the sample Azure Resource Manager template.</span></span> <span data-ttu-id="d8979-108">모든 종속성 및 고유한 구성이 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="d8979-109">최상의 환경을 위해서는 솔루션 인스턴스를 Azure 구독에 미리 배포하고 Azure Resource Manager 템플릿을 따라 작업하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-109">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="d8979-110">전체 템플릿은 [Windows의 Music Store 배포](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-110">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="virtual-machine"></a><span data-ttu-id="d8979-111">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="d8979-111">Virtual Machine</span></span>
<span data-ttu-id="d8979-112">Music Store 응용 프로그램에는 고객이 음악을 찾아보고 구매할 수 있는 웹 응용 프로그램이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-112">The Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="d8979-113">웹 응용 프로그램을 호스트할 수 있는 여러 Azure 서비스가 있지만 이 예제에서는 가상 컴퓨터가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="d8979-114">샘플 Music Store 템플릿을 사용하여 가상 컴퓨터가 배포되고, 웹 서버가 설치되며 Music Store 웹 사이트가 설치 및 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-114">Using the sample Music Store template, a virtual machine is deployed, a web server install, and the Music Store website installed and configured.</span></span> <span data-ttu-id="d8979-115">이 문서에서는 목적에 맞게 가상 컴퓨터 배포만 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-115">For the sake of this article, only the virtual machine deployment is detailed.</span></span> <span data-ttu-id="d8979-116">웹 서버와 응용 프로그램의 구성은 다음 문서에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-116">The configuration of the web server and the application is detailed in a later article.</span></span>

<span data-ttu-id="d8979-117">Visual Studio 새 리소스 추가 마법사를 사용하거나 배포 템플릿에 유효한 JSON을 삽입하여 가상 컴퓨터를 템플릿에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-117">A virtual machine can be added to a template using the Visual Studio Add New Resource wizard, or by inserting valid JSON into the deployment template.</span></span> <span data-ttu-id="d8979-118">가상 컴퓨터를 배포할 때는 몇 가지 관련 리소스도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="d8979-119">Visual Studio를 사용하여 템플릿을 만들 경우 이러한 리소스가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-119">If using Visual Studio to create the template, these resources are created for you.</span></span> <span data-ttu-id="d8979-120">템플릿을 수동으로 생성하는 경우 이러한 리소스를 삽입하고 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-120">If manually constructing the template, these resources need to be inserted and configured.</span></span>

<span data-ttu-id="d8979-121">[가상 컴퓨터 JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-121">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).</span></span>

```json
{
  {
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
  ........<truncated>  
}
```

<span data-ttu-id="d8979-122">일단 배포되면 Azure Portal에서 가상 컴퓨터 속성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-122">Once deployed, the virtual machine properties can be seen in the Azure portal.</span></span>

![가상 컴퓨터](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a><span data-ttu-id="d8979-124">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="d8979-124">Storage Account</span></span>
<span data-ttu-id="d8979-125">저장소 계정에는 많은 저장소 옵션과 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="d8979-126">Azure 가상 컴퓨터의 컨텍스트에서 저장소 계정은 가상 컴퓨터의 가상 하드 드라이브와 추가 데이터 디스크를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-126">For the context of Azure Virtual machines, a storage account holds the virtual hard drives of the virtual machine and any additional data disks.</span></span> <span data-ttu-id="d8979-127">Music Store 샘플에는 배포에 각 가상 컴퓨터의 가상 하드 드라이브를 보유하기 위한 단일 저장소 계정이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-127">The Music Store sample includes one storage account to hold the virtual hard drive of each virtual machine in the deployment.</span></span> 

<span data-ttu-id="d8979-128">[저장소 계정](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-128">Follow this link to see the JSON sample within the Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

<span data-ttu-id="d8979-129">저장소 계정은 가상 컴퓨터의 Resource Manager 템플릿 선언 내에 있는 가상 컴퓨터와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-129">A storage account is associate with a virtual machine inside the Resource Manager template declaration of the virtual machine.</span></span> 

<span data-ttu-id="d8979-130">[가상 컴퓨터 및 저장소 계정 연결](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-130">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).</span></span>

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

<span data-ttu-id="d8979-131">배포 후에는 Azure Portal에서 해당 저장소 계정을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-131">After deployment, the storage account can be viewed in the Azure portal.</span></span>

![저장소 계정](./media/dotnet-core-2-architecture/storacct-win.png)

<span data-ttu-id="d8979-133">Storage 계정 blob 컨테이너를 클릭하면 템플릿을 통해 배포된 각 가상 컴퓨터의 가상 하드 드라이버 파일을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-133">Clicking into the storage account blob container, the virtual hard drive file for each virtual machine deployed with the template can be seen.</span></span>

![가상 하드 드라이브](./media/dotnet-core-2-architecture/vhd-win.png)

<span data-ttu-id="d8979-135">Azure 저장소에 대한 자세한 내용은 [저장소 설명서](https://azure.microsoft.com/documentation/services/storage/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8979-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="d8979-136">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="d8979-136">Virtual Network</span></span>
<span data-ttu-id="d8979-137">가상 컴퓨터에 다른 가상 컴퓨터 및 Azure 리소스와 통신하는 기능과 같은 내부 네트워킹이 필요한 경우 Azure 가상 네트워크가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-137">If a virtual machine requires internal networking such as the ability to communicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="d8979-138">가상 네트워크가 형성되었다고 해서 인터넷을 통해 가상 컴퓨터에 액세스할 수 있는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-138">A virtual network does not make the virtual machine accessible over the internet.</span></span> <span data-ttu-id="d8979-139">공용 연결에는 공용 IP 주소가 필요합니다. 이 내용은 이 시리즈의 뒷부분에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="d8979-140">[가상 네트워크 및 서브넷](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-140">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
    "subnets": [
      {
        "name": "[variables('subnetName')]",
        "properties": {
          "addressPrefix": "10.0.0.0/24",
          "networkSecurityGroup": {
            "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
          }
        }
      }
    ]
  }
}
```

<span data-ttu-id="d8979-141">Azure Portal에서 가상 네트워크는 다음 이미지와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-141">From the Azure portal, the virtual network looks like the following image.</span></span> <span data-ttu-id="d8979-142">템플릿을 사용하여 배포한 모든 가상 컴퓨터가 가상 네트워크에 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-142">Notice that all virtual machines deployed with the template are attached to the virtual network.</span></span>

![가상 네트워크](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a><span data-ttu-id="d8979-144">네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="d8979-144">Network Interface</span></span>
 <span data-ttu-id="d8979-145">네트워크 인터페이스는 가상 컴퓨터를 가상 네트워크에, 좀 더 구체적으로 말해서 가상 네트워크에 정의된 서브넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-145">A network interface connects a virtual machine to a virtual network, more specifically to a subnet that has been defined in the virtual network.</span></span> 

 <span data-ttu-id="d8979-146">[네트워크 인터페이스](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-146">Follow this link to see the JSON sample within the Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceName'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'RDP-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/RDP-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

<span data-ttu-id="d8979-147">각 가상 컴퓨터 리소스에는 네트워크 프로필이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="d8979-148">네트워크 인터페이스는 이 프로필에서 가상 컴퓨터와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-148">The network interface is associated with the virtual machine in this profile.</span></span>  

<span data-ttu-id="d8979-149">[가상 컴퓨터 네트워크 프로필](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330)링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-149">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="d8979-150">Azure Portal에서 네트워크 인터페이스는 다음 이미지와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-150">From the Azure portal, the network interface looks like the following image.</span></span> <span data-ttu-id="d8979-151">내부 IP 주소와 가상 컴퓨터 연결은 네트워크 인터페이스 리소스에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-151">The internal IP address and the virtual machine association can be seen on the network interface resource.</span></span>

![네트워크 인터페이스](./media/dotnet-core-2-architecture/nic-win.png)

<span data-ttu-id="d8979-153">Azure 가상 네트워크에 대한 자세한 내용은 [Azure 가상 네트워크 설명서](https://azure.microsoft.com/documentation/services/virtual-network/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8979-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="d8979-154">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d8979-154">Azure SQL Database</span></span>
<span data-ttu-id="d8979-155">Music Store 웹 사이트를 호스트하는 가상 컴퓨터 외에도, Azure SQL Database가 Music Store 데이터베이스를 호스트하기 위해 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-155">In addition to a virtual machine hosting the Music Store website, an Azure SQL Database is deployed to host the Music Store database.</span></span> <span data-ttu-id="d8979-156">여기서 Azure SQL Database를 사용하면 또 다른 가상 컴퓨터 집합을 사용하지 않아도 되며 크기 조정 및 가용성이 서비스에 기본적으로 제공된다는 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-156">The advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into the service.</span></span>

<span data-ttu-id="d8979-157">Visual Studio 새 리소스 추가 마법사를 사용하거나 템플릿에 유효한 JSON을 삽입하여 Azure SQL Database를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-157">An Azure SQL database can be added using the Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="d8979-158">SQL Server 리소스에는 SQL 인스턴스에 대해 관리자 권한이 부여되는 사용자 이름 및 암호가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-158">The SQL Server resource includes a user name and password that is granted administrative rights on the SQL instance.</span></span> <span data-ttu-id="d8979-159">또한 SQL 방화벽 리소스도 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="d8979-160">기본적으로 Azure에서 호스트되는 응용 프로그램은 SQL 인스턴스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-160">By default, applications hosted in Azure are able to connect with the SQL instance.</span></span> <span data-ttu-id="d8979-161">SQL Server Management Studio와 같은 외부 응용 프로그램이 SQL 인스턴스에 연결할 수 있게 하려면 방화벽을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-161">To allow external application such a SQL Server Management studio to connect to the SQL instance, the firewall needs to be configured.</span></span> <span data-ttu-id="d8979-162">Music Store 데모에 맞게 기본 구성에는 문제가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-162">For the sake of the Music Store demo, the default configuration is fine.</span></span> 

<span data-ttu-id="d8979-163">[Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379) 링크를 따라 Resource Manager 템플릿 내의 JSON 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d8979-163">Follow this link to see the JSON sample within the Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).</span></span>

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicstoresqlName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('adminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicstoresqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

<span data-ttu-id="d8979-164">Azure Portal에 표시되는 SQL Server 및 MusicStore 데이터베이스 보기.</span><span class="sxs-lookup"><span data-stu-id="d8979-164">A view of the SQL server and MusicStore database as seen in the Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

<span data-ttu-id="d8979-166">Azure SQL Database 배포에 대한 자세한 내용은 [Azure SQL Database 설명서](https://azure.microsoft.com/documentation/services/sql-database/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8979-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="d8979-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d8979-167">Next step</span></span>
<hr>

[<span data-ttu-id="d8979-168">2단계 - Azure Resource Manager 템플릿의 액세스 및 보안</span><span class="sxs-lookup"><span data-stu-id="d8979-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

