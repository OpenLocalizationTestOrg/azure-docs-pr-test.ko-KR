---
title: "Azure 리소스 관리자 템플릿을 사용 하 여 Linux 계산 리소스 aaaDeploying | Microsoft Docs"
description: "Azure 가상 컴퓨터 DotNet Core 자습서"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 1c4d419e-ba0e-45e4-a9dd-7ee9975a86f9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0bc26805860fed47923d46fc84f357060f68a951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="073d8-103">Linux VM용 Azure Resource Manager 템플릿을 사용하는 응용 프로그램 아키텍처</span><span class="sxs-lookup"><span data-stu-id="073d8-103">Application architecture with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="073d8-104">Azure 리소스 관리자 배포를 개발할 때 계산 매핑된 toobe tooAzure 리소스 및 서비스 요구 사항 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-104">When developing an Azure Resource Manager deployment, compute requirements need toobe mapped tooAzure resources and services.</span></span> <span data-ttu-id="073d8-105">응용 프로그램으로 구성 된 경우 여러 http 끝점, 데이터베이스 및 서비스 캐싱 데이터 hello 이러한 각 구성이 요소를 호스트 하는 Azure 리소스 필요 toobe 합리화 합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-105">If an application consists of several http endpoints, a database, and a data caching service, hello Azure resources that host each of these components needs toobe rationalized.</span></span> <span data-ttu-id="073d8-106">예를 들어, hello 샘플 음악 스토어 응용 프로그램에 가상 컴퓨터에서 호스팅되는 웹 응용 프로그램 및 Azure SQL 데이터베이스에서 호스트 되는 SQL 데이터베이스에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-106">For instance, hello sample Music Store application includes a web application that is hosted on a virtual machine, and a SQL database, which is hosted in Azure SQL database.</span></span> 

<span data-ttu-id="073d8-107">이 문서 hello 샘플 Azure 리소스 관리자 템플릿 hello Music Store 계산 리소스 구성 방법에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-107">This document details how hello Music Store compute resources are configured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="073d8-108">모든 종속성 및 고유한 구성이 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-108">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="073d8-109">Hello 최상의 경험에 대 한 미리 hello 솔루션 tooyour Azure 구독 및 Azure 리소스 관리자 템플릿 hello와 함께 작업의 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-109">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="073d8-110">hello 완전 한 템플릿 여기 – 있습니다 [ubuntu 음악 스토어 배포](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux)합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-110">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span> 

## <a name="virtual-machine"></a><span data-ttu-id="073d8-111">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="073d8-111">Virtual Machine</span></span>
<span data-ttu-id="073d8-112">hello 음악 스토어 응용 프로그램에 고객 찾아볼 수도 있고 음악 구매 웹 응용 프로그램에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-112">hello Music Store application includes a web application where customers can browse and purchase music.</span></span> <span data-ttu-id="073d8-113">웹 응용 프로그램을 호스트할 수 있는 여러 Azure 서비스가 있지만 이 예제에서는 가상 컴퓨터가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-113">While there are several Azure services that can host web applications, for this example, a Virtual Machine is used.</span></span> <span data-ttu-id="073d8-114">Hello 샘플 음악 스토어 템플릿을 사용 하 여, 가상 컴퓨터가 배포 된, 웹 서버 설치 및 hello 음악 스토어 웹 사이트 설치 및 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-114">Using hello sample Music Store template, a virtual machine is deployed, a web server install, and hello Music Store website installed and configured.</span></span> <span data-ttu-id="073d8-115">이 문서의 hello 위해서만 hello 가상 컴퓨터 배포에 자세히 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-115">For hello sake of this article, only hello virtual machine deployment is detailed.</span></span> <span data-ttu-id="073d8-116">웹 서버 hello 및 hello 응용 프로그램의 hello 구성 이후 문서에 자세히 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-116">hello configuration of hello web server and hello application is detailed in a later article.</span></span>

<span data-ttu-id="073d8-117">가상 컴퓨터에 Visual Studio 새 리소스 추가 마법사를 사용 하거나 hello 배포 템플릿을에 유효한 JSON을 삽입 하 여 hello를 사용 하 여 tooa 템플릿을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-117">A virtual machine can be added tooa template using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into hello deployment template.</span></span> <span data-ttu-id="073d8-118">가상 컴퓨터를 배포할 때는 몇 가지 관련 리소스도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-118">When deploying a virtual machine, several related resources are also needed.</span></span> <span data-ttu-id="073d8-119">Visual Studio toocreate hello 템플릿을 사용 하는 경우 이러한 리소스 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-119">If using Visual Studio toocreate hello template, these resources are created for you.</span></span> <span data-ttu-id="073d8-120">Hello 서식 파일을 수동으로 생성할 하는 경우 이러한 리소스 toobe 삽입 하 고 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-120">If manually constructing hello template, these resources need toobe inserted and configured.</span></span>

<span data-ttu-id="073d8-121">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [가상 컴퓨터 JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295)합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-121">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine JSON](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).</span></span>

```json
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

<span data-ttu-id="073d8-122">배포 된 후 가상 컴퓨터 속성 hello hello Azure 포털에서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-122">Once deployed, hello virtual machine properties can be seen in hello Azure portal.</span></span>

![가상 컴퓨터](./media/dotnet-core-2-architecture/vm.png)

## <a name="storage-account"></a><span data-ttu-id="073d8-124">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="073d8-124">Storage Account</span></span>
<span data-ttu-id="073d8-125">저장소 계정에는 많은 저장소 옵션과 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-125">Storage accounts have many storage options and capabilities.</span></span> <span data-ttu-id="073d8-126">Azure 가상 컴퓨터의 컨텍스트에 hello에 대 한 저장소 계정을 hello 가상 컴퓨터의 가상 하드 드라이브를 hello 및 모든 추가 데이터 디스크를 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-126">For hello context of Azure Virtual machines, a storage account holds hello virtual hard drives of hello virtual machine and any additional data disks.</span></span> <span data-ttu-id="073d8-127">hello Music Store 샘플 hello 배포에 하나의 저장소 계정 toohold hello 가상 하드 드라이브의 각 가상 컴퓨터를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-127">hello Music Store sample includes one storage account toohold hello virtual hard drive of each virtual machine in hello deployment.</span></span> 

<span data-ttu-id="073d8-128">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [저장소 계정](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109)합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-128">Follow this link toosee hello JSON sample within hello Resource Manager template – [Storage Account](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).</span></span>

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

<span data-ttu-id="073d8-129">저장소 계정은 hello 가상 컴퓨터의 hello 리소스 관리자 템플릿 선언 내에 있는 가상 컴퓨터와 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-129">A storage account is associate with a virtual machine inside hello Resource Manager template declaration of hello virtual machine.</span></span> 

<span data-ttu-id="073d8-130">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [가상 컴퓨터 및 저장소 계정 연결](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341)합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine and Storage Account association](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).</span></span>

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

<span data-ttu-id="073d8-131">배포 후 hello 저장소 계정 hello Azure 포털에서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-131">After deployment, hello storage account can be viewed in hello Azure portal.</span></span>

![저장소 계정](./media/dotnet-core-2-architecture/storacct.png)

<span data-ttu-id="073d8-133">Hello 저장소 계정 blob 컨테이너를 클릭 하면, hello 템플릿을 사용 하 여 배포 된 각 가상 컴퓨터에 대 한 가상 하드 드라이브 파일 hello 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-133">Clicking into hello storage account blob container, hello virtual hard drive file for each virtual machine deployed with hello template can be seen.</span></span>

![가상 하드 드라이브](./media/dotnet-core-2-architecture/vhd.png)

<span data-ttu-id="073d8-135">Azure 저장소에 대한 자세한 내용은 [저장소 설명서](https://azure.microsoft.com/documentation/services/storage/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="073d8-135">For more information on Azure Storage, see [Azure Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>

## <a name="virtual-network"></a><span data-ttu-id="073d8-136">가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="073d8-136">Virtual Network</span></span>
<span data-ttu-id="073d8-137">가상 컴퓨터를 다른 가상 컴퓨터 및 Azure 리소스와 hello 기능 toocommunicate 같은 내부 네트워킹을 필요한 경우에 Azure 가상 네트워크 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-137">If a virtual machine requires internal networking such as hello ability toocommunicate with other virtual machines and Azure resources, an Azure Virtual Network is required.</span></span>  <span data-ttu-id="073d8-138">가상 네트워크를 만들지 않습니다 hello 가상 컴퓨터를 통해 액세스할 수 있는 인터넷 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-138">A virtual network does not make hello virtual machine accessible over hello internet.</span></span> <span data-ttu-id="073d8-139">공용 연결에는 공용 IP 주소가 필요합니다. 이 내용은 이 시리즈의 뒷부분에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-139">Public connectivity requires a public IP address, which is detailed later in this series.</span></span>

<span data-ttu-id="073d8-140">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [가상 네트워크 및 서브넷](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136)합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-140">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Network and Subnets](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).</span></span>

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

<span data-ttu-id="073d8-141">Hello Azure 포털에서에서 가상 네트워크 hello hello 다음 이미지 처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-141">From hello Azure portal, hello virtual network looks like hello following image.</span></span> <span data-ttu-id="073d8-142">가상 네트워크에 연결 된 toohello hello 템플릿을 사용 하 여 배포한 모든 가상 컴퓨터 인지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-142">Notice that all virtual machines deployed with hello template are attached toohello virtual network.</span></span>

![가상 네트워크](./media/dotnet-core-2-architecture/vnet.png)

## <a name="network-interface"></a><span data-ttu-id="073d8-144">네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="073d8-144">Network Interface</span></span>
 <span data-ttu-id="073d8-145">네트워크 인터페이스에는 가상 컴퓨터 tooa 가상 네트워크, 가상 네트워크 hello에에서 정의 된 tooa 서브넷 좀 더 구체적으로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-145">A network interface connects a virtual machine tooa virtual network, more specifically tooa subnet that has been defined in hello virtual network.</span></span> 

 <span data-ttu-id="073d8-146">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [네트워크 인터페이스](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166)합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-146">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Interface](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceNamePrefix'), copyindex())]",
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
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'SSH-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig1",
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
              "id": "[concat(variables('lbID'),'/inboundNatRules/SSH-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

<span data-ttu-id="073d8-147">각 가상 컴퓨터 리소스에는 네트워크 프로필이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-147">Each virtual machine resource includes a network profile.</span></span> <span data-ttu-id="073d8-148">hello 네트워크 인터페이스는이 프로필에 hello 가상 컴퓨터와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-148">hello network interface is associated with hello virtual machine in this profile.</span></span>  

<span data-ttu-id="073d8-149">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [가상 컴퓨터 네트워크 프로필](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350)합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-149">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Network Profile](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).</span></span>

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceNamePrefix'), copyindex()))]"
    }
  ]
}
```

<span data-ttu-id="073d8-150">Hello Azure 포털에서에서 네트워크 인터페이스 hello hello 다음 이미지 처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-150">From hello Azure portal, hello network interface looks like hello following image.</span></span> <span data-ttu-id="073d8-151">hello 네트워크 인터페이스 리소스에 hello 내부 IP 주소 및 hello 가상 컴퓨터 연결을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-151">hello internal IP address and hello virtual machine association can be seen on hello network interface resource.</span></span>

![네트워크 인터페이스](./media/dotnet-core-2-architecture/nic.png)

<span data-ttu-id="073d8-153">Azure 가상 네트워크에 대한 자세한 내용은 [Azure 가상 네트워크 설명서](https://azure.microsoft.com/documentation/services/virtual-network/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="073d8-153">For more information on Azure Virtual Networks, see [Azure Virtual Network documentation](https://azure.microsoft.com/documentation/services/virtual-network/).</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="073d8-154">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="073d8-154">Azure SQL Database</span></span>
<span data-ttu-id="073d8-155">또한 hello 음악 스토어 웹 사이트, Azure SQL 데이터베이스를 호스팅하는 tooa 가상 컴퓨터는 배포 된 toohost hello Music Store 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-155">In addition tooa virtual machine hosting hello Music Store website, an Azure SQL Database is deployed toohost hello Music Store database.</span></span> <span data-ttu-id="073d8-156">여기 Azure SQL 데이터베이스를 사용 하 여 hello 장점은 가상 컴퓨터의 두 번째 집합은 필요 하지 확장성 및 가용성 변환은 hello 서비스에입니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-156">hello advantage of using Azure SQL Database here is that a second set of virtual machines is not required, and scale and availability is built into hello service.</span></span>

<span data-ttu-id="073d8-157">Visual Studio 새 리소스 추가 마법사를 사용 하거나 유효한 JSON 서식 파일에 삽입 하 여 hello를 사용 하 여 Azure SQL 데이터베이스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-157">An Azure SQL database can be added using hello Visual Studio Add New Resource wizard, or by inserting valid JSON into a template.</span></span> <span data-ttu-id="073d8-158">SQL Server 리소스 hello 사용자 이름 및 hello SQL 인스턴스에 대해 관리 권한이 부여 되는 암호를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-158">hello SQL Server resource includes a user name and password that is granted administrative rights on hello SQL instance.</span></span> <span data-ttu-id="073d8-159">또한 SQL 방화벽 리소스도 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-159">Also, a SQL firewall resource is added.</span></span> <span data-ttu-id="073d8-160">기본적으로 Azure에서 호스팅되는 응용 프로그램 수 tooconnect hello SQL 인스턴스와 됩니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-160">By default, applications hosted in Azure are able tooconnect with hello SQL instance.</span></span> <span data-ttu-id="073d8-161">tooallow 외부 응용 프로그램 같은 SQL Server Management studio tooconnect toohello SQL 인스턴스 hello 방화벽 toobe 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-161">tooallow external application such a SQL Server Management studio tooconnect toohello SQL instance, hello firewall needs toobe configured.</span></span> <span data-ttu-id="073d8-162">Hello Music Store 데모 hello 위해서 hello 기본 구성은 문제가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-162">For hello sake of hello Music Store demo, hello default configuration is fine.</span></span> 

<span data-ttu-id="073d8-163">Hello 리소스 관리자 템플릿-내에서이 링크 toosee hello JSON 샘플을 따라 [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401)합니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-163">Follow this link toosee hello JSON sample within hello Resource Manager template – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).</span></span>

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicStoreSqlName')]",
  "location": "[resourceGroup().location]",

  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('sqlAdminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicStoreSqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

<span data-ttu-id="073d8-164">Hello SQL server 및 MusicStore 데이터베이스 hello Azure 포털에에서 표시 되는 보기입니다.</span><span class="sxs-lookup"><span data-stu-id="073d8-164">A view of hello SQL server and MusicStore database as seen in hello Azure portal.</span></span>

![SQL Server](./media/dotnet-core-2-architecture/sql.png)

<span data-ttu-id="073d8-166">Azure SQL Database 배포에 대한 자세한 내용은 [Azure SQL Database 설명서](https://azure.microsoft.com/documentation/services/sql-database/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="073d8-166">For more information on deploying Azure SQL Database, see [Azure SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/).</span></span>

## <a name="next-step"></a><span data-ttu-id="073d8-167">다음 단계</span><span class="sxs-lookup"><span data-stu-id="073d8-167">Next step</span></span>
<hr>

[<span data-ttu-id="073d8-168">2단계 - Azure Resource Manager 템플릿의 액세스 및 보안</span><span class="sxs-lookup"><span data-stu-id="073d8-168">Step 2 - Access and Security in Azure Resource Manager Templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

