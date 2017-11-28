---
title: "가상 네트워크 게이트웨이 삭제: PowerShell: Azure 클래식 | Microsoft Docs"
description: "클래식 배포 모델에서 PowerShell을 사용하여 가상 네트워크 게이트웨이를 삭제합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: cherylmc
ms.openlocfilehash: b1bc18307227a728e2bc8fd95e30fdc1cbdb8c59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell-classic"></a><span data-ttu-id="c31d5-103">PowerShell(클래식)을 사용하여 가상 네트워크 삭제</span><span class="sxs-lookup"><span data-stu-id="c31d5-103">Delete a virtual network gateway using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c31d5-104">Resource Manager - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c31d5-104">Resource Manager - Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="c31d5-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="c31d5-105">Resource Manager - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="c31d5-106">클래식 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="c31d5-106">Classic - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="c31d5-107">이 문서에서는 PowerShell을 사용하여 클래식 배포 모델에서 VPN Gateway를 삭제하도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-107">This article helps you delete a VPN gateway in the classic deployment model by using PowerShell.</span></span> <span data-ttu-id="c31d5-108">가상 네트워크 게이트웨이가 삭제되면 네트워크 구성 파일을 수정하여 더 이상 사용하지 않는 요소를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-108">After the virtual network gateway has been deleted, modify the network configuration file to remove elements that you are no longer using.</span></span>

##<span data-ttu-id="c31d5-109"><a name="connect"></a>1단계: Azure에 연결</span><span class="sxs-lookup"><span data-stu-id="c31d5-109"><a name="connect"></a>Step 1: Connect to Azure</span></span>

### <a name="1-install-the-latest-powershell-cmdlets"></a><span data-ttu-id="c31d5-110">1. 최신 PowerShell cmdlet을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-110">1. Install the latest PowerShell cmdlets.</span></span>

<span data-ttu-id="c31d5-111">최신 버전의 Azure SM(서비스 관리) PowerShell cmdlet을 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-111">Download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="c31d5-112">자세한 내용은 [Azure PowerShell 설치 및 구성하는 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c31d5-112">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="c31d5-113">2. Azure 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-113">2. Connect to your Azure account.</span></span> 

<span data-ttu-id="c31d5-114">상승된 권한으로 PowerShell 콘솔을 열고 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-114">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="c31d5-115">연결에 도움이 되도록 다음 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-115">Use the following example to help you connect:</span></span>

```powershell
Add-AzureAccount
```

## <span data-ttu-id="c31d5-116"><a name="export"></a>2단계: 네트워크 구성 파일 내보내기 및 확인</span><span class="sxs-lookup"><span data-stu-id="c31d5-116"><a name="export"></a>Step 2: Export and view the network configuration file</span></span>

<span data-ttu-id="c31d5-117">컴퓨터에 디렉터리를 만들고 디렉터리에 네트워크 구성 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-117">Create a directory on your computer and then export the network configuration file to the directory.</span></span> <span data-ttu-id="c31d5-118">이 파일을 사용하여 현재 구성 정보를 보고 네트워크 구성을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-118">You use this file to both view the current configuration information, and also to modify the network configuration.</span></span>

<span data-ttu-id="c31d5-119">이 예제에서는 네트워크 구성 파일을 C:\AzureNet으로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-119">In this example, the network configuration file is exported to C:\AzureNet.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="c31d5-120">텍스트 편집기로 파일을 열고 클래식 VNet의 이름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-120">Open the file with a text editor and view the name for your classic VNet.</span></span> <span data-ttu-id="c31d5-121">Azure Portal에서 VNet을 만든 경우 Azure에서 사용되는 전체 이름은 포털에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-121">When you create a VNet in the Azure portal, the full name that Azure uses is not visible in the portal.</span></span> <span data-ttu-id="c31d5-122">예를 들어 Azure Portal에서 'ClassicVNet1'이라는 이름의 VNet은 네트워크 구성 파일에서 훨씬 더 긴 이름으로 유지될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-122">For example, a VNet that appears to be named 'ClassicVNet1' in the Azure portal, may have a much longer name in the network configuration file.</span></span> <span data-ttu-id="c31d5-123">즉, 'Group ClassicRG1 ClassicVNet1'과 유사하게 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-123">The name might look something like: 'Group ClassicRG1 ClassicVNet1'.</span></span> <span data-ttu-id="c31d5-124">가상 네트워크 이름은 **‘VirtualNetworkSite name =’**으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-124">Virtual network names are listed as **'VirtualNetworkSite name ='**.</span></span> <span data-ttu-id="c31d5-125">PowerShell cmdlet을 실행할 때는 네트워크 구성 파일의 이름을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-125">Use the names in the network configuration file when running your PowerShell cmdlets.</span></span>

## <span data-ttu-id="c31d5-126"><a name="delete"></a>3단계: 가상 네트워크 게이트웨이 삭제</span><span class="sxs-lookup"><span data-stu-id="c31d5-126"><a name="delete"></a>Step 3: Delete the virtual network gateway</span></span>

<span data-ttu-id="c31d5-127">가상 네트워크 게이트웨이를 삭제하면 게이트웨이를 통해 설정된 VNet에 대한 모든 연결이 끊어집니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-127">When you delete a virtual network gateway, all connections to the VNet through the gateway are disconnected.</span></span> <span data-ttu-id="c31d5-128">P2S 클라이언트를 VNet에 연결한 경우 경고 없이 연결이 끊어집니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-128">If you have P2S clients connected to the VNet, they will be disconnected without warning.</span></span>

<span data-ttu-id="c31d5-129">이 예제에서는 가상 네트워크 게이트웨이를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-129">This example deletes the virtual network gateway.</span></span> <span data-ttu-id="c31d5-130">네트워크 구성 파일에서 가상 네트워크의 전체 이름을 사용하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-130">Make sure to use the full name of the virtual network from the network configuration file.</span></span>

```powershell
Remove-AzureVNetGateway -VNetName "Group ClassicRG1 ClassicVNet1"
```

<span data-ttu-id="c31d5-131">성공하면 반환되는 출력에 다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-131">If successful, the return shows:</span></span>

```
Status : Successful
```

## <span data-ttu-id="c31d5-132"><a name="modify"></a>4단계: 네트워크 구성 파일 수정</span><span class="sxs-lookup"><span data-stu-id="c31d5-132"><a name="modify"></a>Step 4: Modify the network configuration file</span></span>

<span data-ttu-id="c31d5-133">가상 네트워크 게이트웨이를 삭제하는 경우 cmdlet에서 네트워크 구성 파일을 수정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-133">When you delete a virtual network gateway, the cmdlet does not modify the network configuration file.</span></span> <span data-ttu-id="c31d5-134">더 이상 사용 되지 않는 요소를 제거하려면 파일을 수동으로 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-134">You need to modify the file to remove the elements that are no longer being used.</span></span> <span data-ttu-id="c31d5-135">다음 섹션에서는 다운로드한 네트워크 구성 파일을 수정하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-135">The following sections help you modify the network configuration file that you downloaded.</span></span>

### <span data-ttu-id="c31d5-136"><a name="lnsref"></a>로컬 네트워크 사이트 참조</span><span class="sxs-lookup"><span data-stu-id="c31d5-136"><a name="lnsref"></a>Local Network Site References</span></span>

<span data-ttu-id="c31d5-137">사이트 참조 정보를 제거하려면 구성을 **ConnectionsToLocalNetwork/LocalNetworkSiteRef**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-137">To remove site reference information, make configuration changes to **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span></span> <span data-ttu-id="c31d5-138">로컬 사이트 참조를 제거하면 Azure에서 터널을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-138">Removing a local site reference triggers Azure to delete a tunnel.</span></span> <span data-ttu-id="c31d5-139">만든 구성에 따라 **LocalNetworkSiteRef**가 나열되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-139">Depending on the configuration that you created, you may not have a **LocalNetworkSiteRef** listed.</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
     <LocalNetworkSiteRef name="D1BFC9CB_Site2">
       <Connection type="IPsec" />
     </LocalNetworkSiteRef>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

<span data-ttu-id="c31d5-140">예제:</span><span class="sxs-lookup"><span data-stu-id="c31d5-140">Example:</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

###<span data-ttu-id="c31d5-141"><a name="lns"></a>로컬 네트워크 사이트 수</span><span class="sxs-lookup"><span data-stu-id="c31d5-141"><a name="lns"></a>Local Network Sites</span></span>

<span data-ttu-id="c31d5-142">더 이상 사용하지 않는 모든 로컬 사이트를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-142">Remove any local sites that you are no longer using.</span></span> <span data-ttu-id="c31d5-143">만든 구성에 따라 **LocalNetworkSite**가 나열되지 않았을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-143">Depending on the configuration you created, it is possible that you don't have a **LocalNetworkSite** listed.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
  <LocalNetworkSite name="Site3">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>57.179.18.164</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

<span data-ttu-id="c31d5-144">이 예제에서는 Site3만 제거했습니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-144">In this example, we removed only Site3.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

### <span data-ttu-id="c31d5-145"><a name="clientaddresss"></a>클라이언트 AddressPool</span><span class="sxs-lookup"><span data-stu-id="c31d5-145"><a name="clientaddresss"></a>Client AddressPool</span></span>

<span data-ttu-id="c31d5-146">P2S를 VNet에 연결한 경우 **VPNClientAddressPool**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-146">If you had a P2S connection to your VNet, you will have a **VPNClientAddressPool**.</span></span> <span data-ttu-id="c31d5-147">삭제한 가상 네트워크 게이트웨이에 해당하는 클라이언트 주소 풀을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-147">Remove the client address pools that correspond to the virtual network gateway that you deleted.</span></span>

```
<Gateway>
    <VPNClientAddressPool>
      <AddressPrefix>10.1.0.0/24</AddressPrefix>
    </VPNClientAddressPool>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

<span data-ttu-id="c31d5-148">예제:</span><span class="sxs-lookup"><span data-stu-id="c31d5-148">Example:</span></span>

```
<Gateway>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

### <span data-ttu-id="c31d5-149"><a name="gwsub"></a>게이트웨이 서브넷</span><span class="sxs-lookup"><span data-stu-id="c31d5-149"><a name="gwsub"></a>GatewaySubnet</span></span>

<span data-ttu-id="c31d5-150">VNet에 해당하는 **GatewaySubnet**을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-150">Delete the **GatewaySubnet** that corresponds to the VNet.</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
   <Subnet name="GatewaySubnet">
     <AddressPrefix>10.11.1.0/29</AddressPrefix>
   </Subnet>
 </Subnets>
```

<span data-ttu-id="c31d5-151">예제:</span><span class="sxs-lookup"><span data-stu-id="c31d5-151">Example:</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
 </Subnets>
```

## <span data-ttu-id="c31d5-152"><a name="upload"></a>5단계: 네트워크 구성 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="c31d5-152"><a name="upload"></a>Step 5: Upload the network configuration file</span></span>

<span data-ttu-id="c31d5-153">변경 내용을 저장하고 Azure에 네트워크 구성 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-153">Save your changes and upload the network configuration file to Azure.</span></span> <span data-ttu-id="c31d5-154">사용자 환경에 필요한 대로 파일 경로를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-154">Make sure you change the file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="c31d5-155">성공한 경우 반환되는 출력에 다음 예제와 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c31d5-155">If successful, the return shows something similar to this example:</span></span>

```
OperationDescription        OperationId                      OperationStatus                                                
--------------------        -----------                      ---------------                                           
Set-AzureVNetConfig         e0ee6e66-9167-cfa7-a746-7casb9   Succeeded