---
title: "Azure Resource Manager VNet에 클래식 가상 네트워크를 연결하는 방법: PowerShell | Microsoft Docs"
description: "VPN 게이트웨이 및 PowerShell을 사용하여 클래식 VNet 및 Resource Manager VNet 간에 VPN 연결을 만드는 방법을 알아봅니다"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 842a32e5304977af92706cdda464286983122247
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a><span data-ttu-id="4dc27-103">PowerShell을 사용하여 다양한 배포 모델에서 가상 네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="4dc27-103">Connect virtual networks from different deployment models using PowerShell</span></span>



<span data-ttu-id="4dc27-104">이 문서에서는 Resource Manager VNet에 클래식 VNet을 연결하여 별도의 배포 모델에 있는 리소스가 서로 통신하도록 허용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-104">This article shows you how to connect classic VNets to Resource Manager VNets to allow the resources located in the separate deployment models to communicate with each other.</span></span> <span data-ttu-id="4dc27-105">이 문서의 단계는 PowerShell을 사용하지만 이 목록에서 문서를 선택하여 Azure Portal을 사용하여 이 구성을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-105">The steps in this article use PowerShell, but you can also create this configuration using the Azure portal by selecting the article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4dc27-106">포털</span><span class="sxs-lookup"><span data-stu-id="4dc27-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="4dc27-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dc27-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="4dc27-108">클래식 VNet을 Resource Manager VNet에 연결하는 것은 VNet을 온-프레미스 사이트 위치에 연결하는 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-108">Connecting a classic VNet to a Resource Manager VNet is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="4dc27-109">두 연결 유형 모두 VPN 게이트웨이를 사용하여 IPsec/IKE를 통한 보안 터널을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-109">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="4dc27-110">다른 구독 및 다른 지역에 있는 VNet 간에 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="4dc27-111">또한 함께 구성된 게이트웨이가 동적이거나 경로 기반이면 온-프레미스 네트워크에 이미 연결된 VNet을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-111">You can also connect VNets that already have connections to on-premises networks, as long as the gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="4dc27-112">VNet 간 연결에 대한 자세한 내용은 이 문서의 끝에 있는 [VNet 간 FAQ](#faq) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4dc27-112">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span> 

<span data-ttu-id="4dc27-113">VNet이 동일한 지역에 있는 경우 VNet 피어링을 사용하여 연결하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-113">If your VNets are in the same region, you may want to instead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="4dc27-114">VNet 피어링은 VPN Gateway를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="4dc27-115">자세한 내용은 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4dc27-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

## <a name="before-beginning"></a><span data-ttu-id="4dc27-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="4dc27-116">Before beginning</span></span>

<span data-ttu-id="4dc27-117">다음 단계에서는 각 VNet에 대한 동적 또는 경로 기반 게이트웨이를 구성하고 게이트웨이 간에 VPN 연결을 만드는 데 필요한 설정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-117">The following steps walk you through the settings necessary to configure a dynamic or route-based gateway for each VNet and create a VPN connection between the gateways.</span></span> <span data-ttu-id="4dc27-118">이 구성은 고정 또는 정책 기반 게이트웨이를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-118">This configuration does not support static or policy-based gateways.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4dc27-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4dc27-119">Prerequisites</span></span>

* <span data-ttu-id="4dc27-120">두 VNet이 이미 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-120">Both VNets have already been created.</span></span>
* <span data-ttu-id="4dc27-121">VNet에 대한 주소 범위는 서로 겹치거나 게이트웨이가 연결되어 있는 다른 연결의 범위와 겹치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-121">The address ranges for the VNets do not overlap with each other, or overlap with any of the ranges for other connections that the gateways may be connected to.</span></span>
* <span data-ttu-id="4dc27-122">최신 PowerShell cmdlet을 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-122">You have installed the latest PowerShell cmdlets.</span></span> <span data-ttu-id="4dc27-123">자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4dc27-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span> <span data-ttu-id="4dc27-124">SM(서비스 관리)와 RM(Resource Manager) cmdlet을 모두 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-124">Make sure you install both the Service Management (SM) and the Resource Manager (RM) cmdlets.</span></span> 

### <span data-ttu-id="4dc27-125"><a name="exampleref"></a>예제 설정</span><span class="sxs-lookup"><span data-stu-id="4dc27-125"><a name="exampleref"></a>Example settings</span></span>

<span data-ttu-id="4dc27-126">이러한 값을 사용하여 테스트 환경을 만들거나 이 값을 참조하여 이 문서의 예제를 더 잘 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-126">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

<span data-ttu-id="4dc27-127">**클래식 VNet 설정**</span><span class="sxs-lookup"><span data-stu-id="4dc27-127">**Classic VNet settings**</span></span>

<span data-ttu-id="4dc27-128">VNet 이름 = ClassicVNet </span><span class="sxs-lookup"><span data-stu-id="4dc27-128">VNet Name = ClassicVNet</span></span> <br>
<span data-ttu-id="4dc27-129">Location = West US</span><span class="sxs-lookup"><span data-stu-id="4dc27-129">Location = West US</span></span> <br>
<span data-ttu-id="4dc27-130">Virtual Network Address Spaces = 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4dc27-130">Virtual Network Address Spaces = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="4dc27-131">Subnet-1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="4dc27-131">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="4dc27-132">GatewaySubnet = 10.0.0.32/29</span><span class="sxs-lookup"><span data-stu-id="4dc27-132">GatewaySubnet = 10.0.0.32/29</span></span> <br>
<span data-ttu-id="4dc27-133">Local Network Name = RMVNetLocal</span><span class="sxs-lookup"><span data-stu-id="4dc27-133">Local Network Name = RMVNetLocal</span></span> <br>
<span data-ttu-id="4dc27-134">GatewayType = DynamicRouting</span><span class="sxs-lookup"><span data-stu-id="4dc27-134">GatewayType = DynamicRouting</span></span>

<span data-ttu-id="4dc27-135">**Resource Manager VNet 설정**</span><span class="sxs-lookup"><span data-stu-id="4dc27-135">**Resource Manager VNet settings**</span></span>

<span data-ttu-id="4dc27-136">VNet 이름 = RMVNet </span><span class="sxs-lookup"><span data-stu-id="4dc27-136">VNet Name = RMVNet</span></span> <br>
<span data-ttu-id="4dc27-137">Resource Group = RG1</span><span class="sxs-lookup"><span data-stu-id="4dc27-137">Resource Group = RG1</span></span> <br>
<span data-ttu-id="4dc27-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4dc27-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="4dc27-139">Subnet-1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="4dc27-139">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="4dc27-140">GatewaySubnet = 192.168.0.0/26</span><span class="sxs-lookup"><span data-stu-id="4dc27-140">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="4dc27-141">Location = East US</span><span class="sxs-lookup"><span data-stu-id="4dc27-141">Location = East US</span></span> <br>
<span data-ttu-id="4dc27-142">Gateway public IP name = gwpip</span><span class="sxs-lookup"><span data-stu-id="4dc27-142">Gateway public IP name = gwpip</span></span> <br>
<span data-ttu-id="4dc27-143">Local Network Gateway = ClassicVNetLocal</span><span class="sxs-lookup"><span data-stu-id="4dc27-143">Local Network Gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="4dc27-144">Virtual Network Gateway name = RMGateway</span><span class="sxs-lookup"><span data-stu-id="4dc27-144">Virtual Network Gateway name = RMGateway</span></span> <br>
<span data-ttu-id="4dc27-145">게이트웨이 IP 주소 구성 = gwipconfig</span><span class="sxs-lookup"><span data-stu-id="4dc27-145">Gateway IP addressing configuration = gwipconfig</span></span>

## <span data-ttu-id="4dc27-146"><a name="createsmgw"></a>섹션 1 - 클래식 VNet 구성</span><span class="sxs-lookup"><span data-stu-id="4dc27-146"><a name="createsmgw"></a>Section 1 - Configure the classic VNet</span></span>
### <a name="part-1---download-your-network-configuration-file"></a><span data-ttu-id="4dc27-147">1부 - 네트워크 구성 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="4dc27-147">Part 1 - Download your network configuration file</span></span>
1. <span data-ttu-id="4dc27-148">관리자 권한으로 PowerShell 콘솔에서 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-148">Log in to your Azure account in the PowerShell console with elevated rights.</span></span> <span data-ttu-id="4dc27-149">다음 cmdlet가 Azure 계정에 대한 로그인 자격 증명을 유도합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-149">The following cmdlet prompts you for the login credentials for your Azure Account.</span></span> <span data-ttu-id="4dc27-150">로그인한 다음 Azure PowerShell에 사용할 수 있도록 계정 설정을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-150">After logging in, it downloads your account settings so that they are available to Azure PowerShell.</span></span> <span data-ttu-id="4dc27-151">구성의 이 부분을 완료하려면 SM PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-151">You use the SM PowerShell cmdlets to complete this part of the configuration.</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="4dc27-152">다음 명령을 실행하여 Azure 네트워크 구성 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-152">Export your Azure network configuration file by running the following command.</span></span> <span data-ttu-id="4dc27-153">필요한 경우 다른 위치로 내보낼 파일의 위치를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-153">You can change the location of the file to export to a different location if necessary.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. <span data-ttu-id="4dc27-154">다운로드한 .xml 파일을 열고 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-154">Open the .xml file that you downloaded to edit it.</span></span> <span data-ttu-id="4dc27-155">네트워크 구성 파일의 예는 [네트워크 구성 스키마](https://msdn.microsoft.com/library/jj157100.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4dc27-155">For an example of the network configuration file, see the [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span></span>

### <a name="part-2--verify-the-gateway-subnet"></a><span data-ttu-id="4dc27-156">2부 - 게이트웨이 서브넷 확인</span><span class="sxs-lookup"><span data-stu-id="4dc27-156">Part 2 -Verify the gateway subnet</span></span>
<span data-ttu-id="4dc27-157">**VirtualNetworkSites**요소에 게이트웨이 서브넷을 아직 만들지 않은 경우 VNet에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-157">In the **VirtualNetworkSites** element, add a gateway subnet to your VNet if one has not already been created.</span></span> <span data-ttu-id="4dc27-158">네트워크 구성 파일로 작업할 때 게이트웨이 서브넷의 이름은 "GatewaySubnet"이어야 합니다. 또는 Azure에서 게이트웨이 서브넷으로 인식하고 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-158">When working with the network configuration file, the gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="4dc27-159">**예제:**</span><span class="sxs-lookup"><span data-stu-id="4dc27-159">**Example:**</span></span>

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-the-local-network-site"></a><span data-ttu-id="4dc27-160">3단계 - 로컬 네트워크 사이트 추가</span><span class="sxs-lookup"><span data-stu-id="4dc27-160">Part 3 - Add the local network site</span></span>
<span data-ttu-id="4dc27-161">추가한 로컬 네트워크 사이트는 연결하려는 RM VNet을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-161">The local network site you add represents the RM VNet to which you want to connect.</span></span> <span data-ttu-id="4dc27-162">존재하지 않는 경우 파일에 **LocalNetworkSites** 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-162">Add a **LocalNetworkSites** element to the file if one doesn't already exist.</span></span> <span data-ttu-id="4dc27-163">구성의 이 시점에서 Resource Manager VNet에 대한 게이트웨이 아직 만들지 않았기 때문에 VPNGatewayAddress는 유효한 공용 IP 주소일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-163">At this point in the configuration, the VPNGatewayAddress can be any valid public IP address because we haven't yet created the gateway for the Resource Manager VNet.</span></span> <span data-ttu-id="4dc27-164">게이트웨이를 만들고 나면 이 자리 표시자 IP 주소를 RM 게이트웨이에 할당된 올바른 공용 IP 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-164">Once we create the gateway, we replace this placeholder IP address with the correct public IP address that has been assigned to the RM gateway.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-the-vnet-with-the-local-network-site"></a><span data-ttu-id="4dc27-165">4부 - 로컬 네트워크 사이트와 VNet 연결</span><span class="sxs-lookup"><span data-stu-id="4dc27-165">Part 4 - Associate the VNet with the local network site</span></span>
<span data-ttu-id="4dc27-166">이 섹션에서는 VNet을 연결하려는 로컬 네트워크 사이트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-166">In this section, we specify the local network site that you want to connect the VNet to.</span></span> <span data-ttu-id="4dc27-167">이 경우에 앞서 참조한 Resource Manager VNet입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-167">In this case, it is the Resource Manager VNet that you referenced earlier.</span></span> <span data-ttu-id="4dc27-168">이름이 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-168">Make sure the names match.</span></span> <span data-ttu-id="4dc27-169">이 단계에서는 게이트웨이를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-169">This step does not create a gateway.</span></span> <span data-ttu-id="4dc27-170">게이트웨이를 연결할 로컬 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-170">It specifies the local network that the gateway will connect to.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-the-file-and-upload"></a><span data-ttu-id="4dc27-171">5부 - 파일 저장 및 업로드</span><span class="sxs-lookup"><span data-stu-id="4dc27-171">Part 5 - Save the file and upload</span></span>
<span data-ttu-id="4dc27-172">파일을 저장하고 다음 명령을 실행하여 Azure에 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-172">Save the file, then import it to Azure by running the following command.</span></span> <span data-ttu-id="4dc27-173">사용자 환경에 필요한 대로 파일 경로를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-173">Make sure you change the file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="4dc27-174">가져오기가 성공했음을 보여 주는 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-174">You will see a similar result showing that the import succeeded.</span></span>

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-the-gateway"></a><span data-ttu-id="4dc27-175">6부 - 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="4dc27-175">Part 6 - Create the gateway</span></span>

<span data-ttu-id="4dc27-176">이 예제를 실행하기 전에 Azure에 필요한 정확한 이름에 대해서는 다운로드한 네트워크 구성 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4dc27-176">Before running this example, refer to the network configuration file that you downloaded for the exact names that Azure expects to see.</span></span> <span data-ttu-id="4dc27-177">네트워크 구성 파일에는 클래식 가상 네트워크에 대한 값이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-177">The network configuration file contains the values for your classic virtual networks.</span></span> <span data-ttu-id="4dc27-178">배포 모델의 차이 때문에 Azure Portal에서 클래식 Vnet 설정을 만들 때 네트워크 구성 파일에서 클래식 Vnet의 이름이 변경되는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-178">Sometimes the names for classic VNets are changed in the network configuration file when creating classic VNet settings in the Azure portal due to the differences in the deployment models.</span></span> <span data-ttu-id="4dc27-179">예를 들어 Azure Portal을 사용하여 'Classic VNet'이라는 클래식 VNet을 만들고 'ClassicRG'라는 리소스 그룹에 만들면 네트워크 구성 파일에 포함된 이름은 'Group ClassicRG Classic VNet'으로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-179">For example, if you used the Azure portal to create a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', the name that is contained in the network configuration file is converted to 'Group ClassicRG Classic VNet'.</span></span> <span data-ttu-id="4dc27-180">공백이 포함된 VNet의 이름을 지정할 때는 값을 따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-180">When specifying the name of a VNet that contains spaces, use quotation marks around the value.</span></span>


<span data-ttu-id="4dc27-181">다음 예제를 사용하여 동적 라우팅 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-181">Use the following example to create a dynamic routing gateway:</span></span>

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

<span data-ttu-id="4dc27-182">**Get-AzureVNetGateway** cmdlet을 사용하여 게이트웨이의 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-182">You can check the status of the gateway by using the **Get-AzureVNetGateway** cmdlet.</span></span>

## <span data-ttu-id="4dc27-183"><a name="creatermgw"></a>섹션 2: RM VNet 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="4dc27-183"><a name="creatermgw"></a>Section 2: Configure the RM VNet gateway</span></span>
<span data-ttu-id="4dc27-184">RM VNet에 대한 VPN 게이트웨이를 만들려면 다음 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="4dc27-184">To create a VPN gateway for the RM VNet, follow the following instructions.</span></span> <span data-ttu-id="4dc27-185">클래식 VNet의 게이트웨이에 대한 공용 IP 주소를 검색할 때까지 단계를 시작하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-185">Don't start the steps until after you have retrieved the public IP address for the classic VNet's gateway.</span></span> 

1. <span data-ttu-id="4dc27-186">PowerShell 콘솔에서 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-186">Log in to your Azure account in the PowerShell console.</span></span> <span data-ttu-id="4dc27-187">다음 cmdlet가 Azure 계정에 대한 로그인 자격 증명을 유도합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-187">The following cmdlet prompts you for the login credentials for your Azure Account.</span></span> <span data-ttu-id="4dc27-188">로그인한 다음 Azure PowerShell에 사용할 수 있도록 계정 설정이 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-188">After logging in, your account settings are downloaded so that they are available to Azure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  <span data-ttu-id="4dc27-189">둘 이상의 구독이 있는 경우 Azure 구독 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-189">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
   
  <span data-ttu-id="4dc27-190">사용할 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-190">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="4dc27-191">로컬 네트워크 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-191">Create a local network gateway.</span></span> <span data-ttu-id="4dc27-192">가상 네트워크에서 로컬 네트워크 게이트웨이는 일반적으로 온-프레미스 위치를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-192">In a virtual network, the local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="4dc27-193">이 경우에 로컬 네트워크 게이트웨이는 클래식 VNet을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-193">In this case, the local network gateway refers to your Classic VNet.</span></span> <span data-ttu-id="4dc27-194">Azure에서 참조할 수 있는 이름을 지정하고 주소 공간 접두사를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-194">Give it a name by which Azure can refer to it, and also specify the address space prefix.</span></span> <span data-ttu-id="4dc27-195">Azure는 지정된 IP 주소 접두사를 사용하여 온-프레미스 위치로 보낼 트래픽을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-195">Azure uses the IP address prefix you specify to identify which traffic to send to your on-premises location.</span></span> <span data-ttu-id="4dc27-196">나중에 게이트웨이를 만들기 전에 여기서 정보를 조정하는 경우 값을 수정하고 샘플을 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-196">If you need to adjust the information here later, before creating your gateway, you can modify the values and run the sample again.</span></span>
   
   <span data-ttu-id="4dc27-197">**-Name**은 로컬 네트워크 게이트웨이에 참조하기 위해 할당하려는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-197">**-Name** is the name you want to assign to refer to the local network gateway.</span></span><br><span data-ttu-id="4dc27-198">
   **-AddressPrefix**은 클래식 VNet에 대한 주소 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-198">
   **-AddressPrefix** is the Address Space for your classic VNet.</span></span><br><span data-ttu-id="4dc27-199">
**-GatewayIpAddress**은 클래식 VNet 게이트웨이의 공용 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-199">
**-GatewayIpAddress** is the public IP address of the classic VNet's gateway.</span></span> <span data-ttu-id="4dc27-200">다음 샘플이 올바른 IP 주소를 반영하도록 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-200">Be sure to change the following sample to reflect the correct IP address.</span></span><br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. <span data-ttu-id="4dc27-201">리소스 관리자 VNet에 대한 가상 네트워크 게이트웨이에 할당할 공용 IP 주소를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-201">Request a public IP address to be allocated to the virtual network gateway for the Resource Manager VNet.</span></span> <span data-ttu-id="4dc27-202">사용할 IP 주소를 지정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-202">You can't specify the IP address that you want to use.</span></span> <span data-ttu-id="4dc27-203">IP 주소는 가상 네트워크 게이트웨이에 동적으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-203">The IP address is dynamically allocated to the virtual network gateway.</span></span> <span data-ttu-id="4dc27-204">그러나 이로 인해 IP 주소가 변경되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-204">However, this does not mean the IP address changes.</span></span> <span data-ttu-id="4dc27-205">게이트웨이가 삭제되고 다시 만들어지는 경우에만 가상 네트워크 게이트웨이 IP 주소가 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-205">The only time the virtual network gateway IP address changes is when the gateway is deleted and recreated.</span></span> <span data-ttu-id="4dc27-206">크기 조정, 다시 설정 또는 게이트웨이의 기타 내부 유지 관리/업그레이드를 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-206">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of the gateway.</span></span>

  <span data-ttu-id="4dc27-207">이 단계에서는 이후 단계에 사용되는 변수도 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-207">In this step, we also set a variable that is used in a later step.</span></span>

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. <span data-ttu-id="4dc27-208">가상 네트워크에 게이트웨이 서브넷이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-208">Verify that your virtual network has a gateway subnet.</span></span> <span data-ttu-id="4dc27-209">게이트웨이 서브넷이 없다면 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-209">If no gateway subnet exists, add one.</span></span> <span data-ttu-id="4dc27-210">게이트웨이 서브넷의 이름을 *GatewaySubnet*으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-210">Make sure the gateway subnet is named *GatewaySubnet*.</span></span>
5. <span data-ttu-id="4dc27-211">다음 명령을 실행하여 게이트웨이에 사용된 서브넷을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-211">Retrieve the subnet used for the gateway by running the following command.</span></span> <span data-ttu-id="4dc27-212">이 단계에서는 다음 단계에서 사용할 변수도 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-212">In this step, we also set a variable to be used in the next step.</span></span>
   
   <span data-ttu-id="4dc27-213">**-Name**은 리소스 관리자 VNet의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-213">**-Name** is the name of your Resource Manager VNet.</span></span><br><span data-ttu-id="4dc27-214">
   **-ResourceGroupName**은 VNet과 연결된 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-214">
**-ResourceGroupName** is the resource group that the VNet is associated with.</span></span> <span data-ttu-id="4dc27-215">제대로 작동하려면 게이트웨이 서브넷이 이 VNet에 이미 존재하고 이름을 *GatewaySubnet* 으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-215">The gateway subnet must already exist for this VNet and must be named *GatewaySubnet* to work properly.</span></span><br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. <span data-ttu-id="4dc27-216">게이트웨이 IP 주소 지정 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-216">Create the gateway IP addressing configuration.</span></span> <span data-ttu-id="4dc27-217">게이트웨이 구성은 사용할 공용 IP 주소 및 서브넷을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-217">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="4dc27-218">다음 샘플을 사용하여 게이트웨이 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-218">Use the following sample to create your gateway configuration.</span></span>

  <span data-ttu-id="4dc27-219">**-SubnetId** 및 **-PublicIpAddressId** 매개 변수는 각각 서브넷 및 IP 주소 개체에서 id 속성이 전달되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-219">In this step, the **-SubnetId** and **-PublicIpAddressId** parameters must be passed the id property from the subnet, and IP address objects, respectively.</span></span> <span data-ttu-id="4dc27-220">간단한 문자열을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-220">You can't use a simple string.</span></span> <span data-ttu-id="4dc27-221">이러한 변수는 공용 IP를 요청하는 단계 및 서브넷을 검색하는 단계에서 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-221">These variables are set in the step to request a public IP and the step to retrieve the subnet.</span></span>

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. <span data-ttu-id="4dc27-222">리소스 관리자 가상 네트워크 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-222">Create the Resource Manager virtual network gateway by running the following command.</span></span> <span data-ttu-id="4dc27-223">`-VpnType` 는 *RouteBased*여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-223">The `-VpnType` must be *RouteBased*.</span></span> <span data-ttu-id="4dc27-224">게이트웨이를 만드는 데에는 45분 이상이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-224">It can take 45 minutes or more for the gateway to create.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. <span data-ttu-id="4dc27-225">VPN 게이트웨이가 만들어지면 공용 IP 주소를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-225">Copy the public IP address once the VPN gateway has been created.</span></span> <span data-ttu-id="4dc27-226">클래식 VNet에 대한 로컬 네트워크 설정을 구성할 때 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-226">You use it when you configure the local network settings for your Classic VNet.</span></span> <span data-ttu-id="4dc27-227">다음 cmdlet을 사용하여 공용 IP 주소를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-227">You can use the following cmdlet to retrieve the public IP address.</span></span> <span data-ttu-id="4dc27-228">공용 IP 주소가 *IpAddress*로 반환에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-228">The public IP address is listed in the return as *IpAddress*.</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-the-classic-vnet-local-site-settings"></a><span data-ttu-id="4dc27-229">섹션 3: 클래식 VNet 로컬 사이트 설정 수정</span><span class="sxs-lookup"><span data-stu-id="4dc27-229">Section 3: Modify the classic VNet local site settings</span></span>

<span data-ttu-id="4dc27-230">이 섹션에서는 클래식 VNet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-230">In this section, you work with the classic VNet.</span></span> <span data-ttu-id="4dc27-231">리소스 관리자 VNet 게이트웨이에 연결하는 데 사용될 로컬 사이트 설정을 지정할 때 사용한 자리 표시자 IP 주소를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-231">You replace the placeholder IP address that you used when specifying the local site settings that will be used to connect to the Resource Manager VNet gateway.</span></span> 

1. <span data-ttu-id="4dc27-232">네트워크 구성 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-232">Export the network configuration file.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="4dc27-233">텍스트 편집기를 사용하여 VPNGatewayAddress에 대한 값을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-233">Using a text editor, modify the value for VPNGatewayAddress.</span></span> <span data-ttu-id="4dc27-234">자리 표시자 IP 주소를 Resource Manager 게이트웨이의 공용 IP 주소로 바꾼 후 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-234">Replace the placeholder IP address with the public IP address of the Resource Manager gateway and then save the changes.</span></span>

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. <span data-ttu-id="4dc27-235">수정된 네트워크 구성 파일을 Azure로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-235">Import the modified network configuration file to Azure.</span></span>

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <span data-ttu-id="4dc27-236"><a name="connect"></a>섹션 4: 게이트웨이 간의 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="4dc27-236"><a name="connect"></a>Section 4: Create a connection between the gateways</span></span>
<span data-ttu-id="4dc27-237">게이트웨이 간의 연결을 만들려면 PowerShell이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-237">Creating a connection between the gateways requires PowerShell.</span></span> <span data-ttu-id="4dc27-238">Azure 계정을 추가하여 클래식 버전의 PowerShell cmdlet을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-238">You may need to add your Azure Account to use the classic version of the  PowerShell cmdlets.</span></span> <span data-ttu-id="4dc27-239">이 작업에는 **Add-AzureAccount**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-239">To do so, use **Add-AzureAccount**.</span></span>

1. <span data-ttu-id="4dc27-240">PowerShell 콘솔에서 공유 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-240">In the PowerShell console, set your shared key.</span></span> <span data-ttu-id="4dc27-241">이러한 cmdlet을 실행하기 전에 Azure에 필요한 정확한 이름에 대해서는 다운로드한 네트워크 구성 파일을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4dc27-241">Before running the cmdlets, refer to the network configuration file that you downloaded for the exact names that Azure expects to see.</span></span> <span data-ttu-id="4dc27-242">공백이 포함된 VNet의 이름을 지정할 때는 값을 작은따옴표로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-242">When specifying the name of a VNet that contains spaces, use single quotation marks around the value.</span></span><br><br><span data-ttu-id="4dc27-243">다음 예제에서 **-VNetName**은 클래식 VNet의 이름이고 **-LocalNetworkSiteName**은 로컬 네트워크 사이트에 대해 지정한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-243">In following example, **-VNetName** is the name of the classic VNet and **-LocalNetworkSiteName** is the name you specified for the local network site.</span></span> <span data-ttu-id="4dc27-244">**-SharedKey**는 사용자가 생성하고 지정하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-244">The **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="4dc27-245">이 예제에서는 'abc123'을 사용했으나 좀 더 복잡한 항목을 생성하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-245">In the example, we used 'abc123', but you can generate and use something more complex.</span></span> <span data-ttu-id="4dc27-246">중요한 점은 여기에서 지정한 값이 연결을 만드는 다음 단계에서 지정한 것과 동일한 값이어야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-246">The important thing is that the value you specify here must be the same value that you specify in the next step when you create your connection.</span></span> <span data-ttu-id="4dc27-247">반환 값에는 **상태:성공**이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-247">The return should show **Status: Successful**.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. <span data-ttu-id="4dc27-248">다음 명령을 실행하여 VPN 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-248">Create the VPN connection by running the following commands:</span></span>
   
  <span data-ttu-id="4dc27-249">변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-249">Set the variables.</span></span>

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  <span data-ttu-id="4dc27-250">연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-250">Create the connection.</span></span> <span data-ttu-id="4dc27-251">**-ConnectionType**은 Vnet2Vnet이 아닌 IPsec입니다.</span><span class="sxs-lookup"><span data-stu-id="4dc27-251">Notice that the **-ConnectionType** is IPsec, not Vnet2Vnet.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a><span data-ttu-id="4dc27-252">섹션 5: 연결 확인</span><span class="sxs-lookup"><span data-stu-id="4dc27-252">Section 5: Verify your connections</span></span>

### <a name="to-verify-the-connection-from-your-classic-vnet-to-your-resource-manager-vnet"></a><span data-ttu-id="4dc27-253">클래식 VNet에서 Resource Manager VNet으로의 연결을 확인하려면</span><span class="sxs-lookup"><span data-stu-id="4dc27-253">To verify the connection from your classic VNet to your Resource Manager VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="4dc27-254">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dc27-254">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="4dc27-255">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="4dc27-255">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="to-verify-the-connection-from-your-resource-manager-vnet-to-your-classic-vnet"></a><span data-ttu-id="4dc27-256">Resource Manager VNet에서 클래식 VNet으로의 연결을 확인하려면</span><span class="sxs-lookup"><span data-stu-id="4dc27-256">To verify the connection from your Resource Manager VNet to your classic VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="4dc27-257">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dc27-257">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="4dc27-258">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="4dc27-258">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="4dc27-259"><a name="faq"></a>VNet 간 FAQ</span><span class="sxs-lookup"><span data-stu-id="4dc27-259"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

