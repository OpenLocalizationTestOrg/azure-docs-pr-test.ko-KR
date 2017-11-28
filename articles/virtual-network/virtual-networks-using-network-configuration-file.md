---
title: "Azure 가상 네트워크 (클래식)-네트워크 구성 파일 aaaConfigure | Microsoft Docs"
description: "자세한 내용은 어떻게 toocreate 및 내보내기, 변경 및 네트워크 구성 파일을 가져오는 하 여 가상 네트워크 (클래식)를 수정 합니다."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="4132c-103">네트워크 구성 파일을 사용하여 가상 네트워크(클래식) 구성</span><span class="sxs-lookup"><span data-stu-id="4132c-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4132c-104">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="4132c-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="4132c-106">대부분의 새로운 배포 hello 리소스 관리자 배포 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="4132c-107">수 만들고 hello Azure CLI (명령줄 인터페이스) 1.0 또는 Azure PowerShell을 사용 하 여 네트워크 구성 파일을 통한 가상 네트워크 (클래식)를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-107">You can create and configure a virtual network (classic) with a network configuration file using hello Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="4132c-108">네트워크 구성 파일을 사용 하 여 hello Azure 리소스 관리자 배포 모델을 통해 가상 네트워크를 수정 하거나 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-108">You cannot create or modify a virtual network through hello Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="4132c-109">Azure 포털 toocreate hello를 사용 하 여 또는 네트워크 구성 파일을 사용 하 여 가상 네트워크 (클래식)를 수정 하, 사용할 수 있지만 Azure 포털 toocreate 네트워크 구성 파일을 사용 하지 않고 가상 네트워크 (클래식) hello 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-109">You cannot use hello Azure portal toocreate or modify a virtual network (classic) using a network configuration file, however you can use hello Azure portal toocreate a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="4132c-110">만들기 및 네트워크 구성 파일을 사용 하 여 가상 네트워크 (클래식)를 구성 내보내기, 변경 및 hello 파일을 가져오는 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing hello file.</span></span>

## <span data-ttu-id="4132c-111"><a name="export"></a>네트워크 구성 파일 내보내기</span><span class="sxs-lookup"><span data-stu-id="4132c-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="4132c-112">PowerShell 또는 hello Azure CLI tooexport 네트워크 구성 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-112">You can use PowerShell or hello Azure CLI tooexport a network configuration file.</span></span> <span data-ttu-id="4132c-113">PowerShell은 Azure CLI hello json 파일을 내보내는 동안 XML 파일로를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-113">PowerShell exports an XML file, while hello Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="4132c-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4132c-114">PowerShell</span></span>
 
1. <span data-ttu-id="4132c-115">[Azure PowerShell을 설치 하 고 tooAzure 로그인](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-115">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="4132c-116">Hello 디렉터리 변경 (및 존재 확인) 및 파일 이름을 hello에 다음 명령을 실행 후 원하는 hello 명령 tooexport hello 네트워크 구성 파일로:</span><span class="sxs-lookup"><span data-stu-id="4132c-116">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="4132c-117">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4132c-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="4132c-118">[Hello Azure CLI 1.0 설치](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-118">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="4132c-119">Hello 남은 Azure CLI 1.0 명령 프롬프트에서 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-119">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="4132c-120">TooAzure hello를 입력 하 여 로그인 `azure login` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-120">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="4132c-121">Hello를 입력 하 여 asm 모드에 있는 확인 `azure config mode asm` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-121">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="4132c-122">Hello 디렉터리 변경 (및 존재 확인) 및 파일 이름을 hello에 다음 명령을 실행 후 원하는 hello 명령 tooexport hello 네트워크 구성 파일로:</span><span class="sxs-lookup"><span data-stu-id="4132c-122">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="4132c-123">네트워크 구성 파일 만들기 또는 수정</span><span class="sxs-lookup"><span data-stu-id="4132c-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="4132c-124">네트워크 구성 파일 (PowerShell 사용) 하는 경우 XML 파일 또는 json 파일 (경우 hello Azure CLI를 사용 하 여).</span><span class="sxs-lookup"><span data-stu-id="4132c-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using hello Azure CLI).</span></span> <span data-ttu-id="4132c-125">모든 텍스트 또는 XML/json 편집기 hello 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-125">You can edit hello file in any text, or XML/json editor.</span></span> <span data-ttu-id="4132c-126">hello [네트워크 구성 파일 스키마 설정](https://msdn.microsoft.com/library/azure/jj157100.aspx) 아티클은 모든 설정에 대 한 세부 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-126">hello [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="4132c-127">Hello 설정의 추가 설명을 참조 하십시오. [가상 네트워크와 설정을 보려면](virtual-network-manage-network.md#view-vnet)합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-127">For additional explanation of hello settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="4132c-128">hello 변경 toohello 파일:</span><span class="sxs-lookup"><span data-stu-id="4132c-128">hello changes you make toohello file:</span></span>

- <span data-ttu-id="4132c-129">맞아야 hello 스키마 또는 가져오기 hello 네트워크 구성 파일 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-129">Must comply with hello schema, or importing hello network configuration file will fail.</span></span>
- <span data-ttu-id="4132c-130">구독에 대한 모든 기존 네트워크 설정을 덮어쓰므로 수정할 때는 특히 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="4132c-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="4132c-131">예를 들어 hello 예제 네트워크 구성 파일에 나오는 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-131">For example, reference hello example network configuration files that follow.</span></span> <span data-ttu-id="4132c-132">Hello 원본 파일에 포함 된 두 개의 예를 들어 **VirtualNetworkSite** 인스턴스, 그리고 하는 hello 예제에 나와 있는 것 처럼, 하 게 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-132">Say hello original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in hello examples.</span></span> <span data-ttu-id="4132c-133">Azure hello hello에 대 한 가상 네트워크 삭제 hello 파일을 가져올 때 **VirtualNetworkSite** 인스턴스 hello 파일에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-133">When you import hello file, Azure deletes hello virtual network for hello **VirtualNetworkSite** instance you removed in hello file.</span></span> <span data-ttu-id="4132c-134">이 간단한 시나리오에서는 리소스가 없는 hello 가상 네트워크에 있던 가정 했습니다 마치 hello 가상 네트워크를 삭제할 수 없습니다, 그리고 및 hello 가져오기 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-134">This simplified scenario assumes no resources were in hello virtual network, as if there were, hello virtual network could not be deleted, and hello import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4132c-135">Azure 고려 하는 서브넷으로 tooit 배포 **사용에서**합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-135">Azure considers a subnet that has something deployed tooit as **in use**.</span></span> <span data-ttu-id="4132c-136">사용 중인 서브넷은 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="4132c-137">네트워크 구성 파일에서 서브넷 정보를 수정 하기 전에 아무 것도 수정 하 고 있지 않습니다 toohello 서브넷 tooa 다른 서브넷 배포를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-137">Before modifying subnet information in a network configuration file, move anything that you have deployed toohello subnet tooa different subnet that isn't being modified.</span></span> <span data-ttu-id="4132c-138">참조 [VM 또는 역할 인스턴스 tooa 다른 서브넷 이동](virtual-networks-move-vm-role-to-subnet.md) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-138">See [Move a VM or Role Instance tooa Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="4132c-139">PowerShell과 함께 사용할 XML 예제</span><span class="sxs-lookup"><span data-stu-id="4132c-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="4132c-140">hello 다음 네트워크 구성 파일 예에서는 가상 네트워크를 만들어 명명 된 *myVirtualNetwork* 의 주소 공간과 *10.0.0.0/16* hello에 *미국 동부* Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-140">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="4132c-141">라는 하나의 서브넷을 포함 하는 가상 네트워크 hello *mySubnet* 의 주소 접두사가 *10.0.0.0/24*합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-141">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

<span data-ttu-id="4132c-142">내보낸 hello 네트워크 구성 파일의 내용이 들어 있을 경우 수 복사 hello XML hello 이전 예에서 하 새 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-142">If hello network configuration file you exported contains no contents, you can copy hello XML in hello previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-hello-azure-cli-10"></a><span data-ttu-id="4132c-143">예제 JSON hello Azure CLI 1.0로 사용 하기 위해</span><span class="sxs-lookup"><span data-stu-id="4132c-143">Example JSON for use with hello Azure CLI 1.0</span></span>

<span data-ttu-id="4132c-144">hello 다음 네트워크 구성 파일 예에서는 가상 네트워크를 만들어 명명 된 *myVirtualNetwork* 의 주소 공간과 *10.0.0.0/16* hello에 *미국 동부* Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-144">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="4132c-145">라는 하나의 서브넷을 포함 하는 가상 네트워크 hello *mySubnet* 의 주소 접두사가 *10.0.0.0/24*합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-145">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

<span data-ttu-id="4132c-146">내보낸 hello 네트워크 구성 파일의 내용이 들어 있을 경우 수 복사 hello json hello 이전 예에서 하 새 파일에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-146">If hello network configuration file you exported contains no contents, you can copy hello json in hello previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="4132c-147"><a name="import"></a>네트워크 구성 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="4132c-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="4132c-148">PowerShell 또는 hello Azure CLI tooimport 네트워크 구성 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-148">You can use PowerShell or hello Azure CLI tooimport a network configuration file.</span></span> <span data-ttu-id="4132c-149">PowerShell은 Azure CLI hello json 파일을 가져오는 동안 XML 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-149">PowerShell imports an XML file, while hello Azure CLI imports a json file.</span></span> <span data-ttu-id="4132c-150">Hello 가져오기에 실패 하면 해당 hello 파일 hello 준수 확인 [네트워크 구성 스키마](https://msdn.microsoft.com/library/azure/jj157100.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-150">If hello import fails, confirm that hello file complies with hello [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="4132c-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4132c-151">PowerShell</span></span>
 
1. <span data-ttu-id="4132c-152">[Azure PowerShell을 설치 하 고 tooAzure 로그인](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-152">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="4132c-153">Hello 디렉터리와 파일 이름을 다음 필요에 따라 명령을 hello 변경한 하십시오 hello 명령 tooimport hello 네트워크 구성 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-153">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="4132c-154">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4132c-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="4132c-155">[Hello Azure CLI 1.0 설치](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-155">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="4132c-156">Hello 남은 Azure CLI 1.0 명령 프롬프트에서 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-156">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="4132c-157">TooAzure hello를 입력 하 여 로그인 `azure login` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-157">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="4132c-158">Hello를 입력 하 여 asm 모드에 있는 확인 `azure config mode asm` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-158">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="4132c-159">Hello 디렉터리와 파일 이름을 다음 필요에 따라 명령을 hello 변경한 하십시오 hello 명령 tooimport hello 네트워크 구성 파일을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4132c-159">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
