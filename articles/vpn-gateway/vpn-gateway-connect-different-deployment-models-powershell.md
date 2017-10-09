---
title: "클래식 가상 네트워크 tooAzure 리소스 관리자 Vnet 연결: PowerShell | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 클래식 Vnet 및 VPN 게이트웨이 및 PowerShell을 사용 하 여 리소스 관리자 Vnet 간의 VPN 연결"
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
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a><span data-ttu-id="20b6d-103">PowerShell을 사용하여 다양한 배포 모델에서 가상 네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="20b6d-103">Connect virtual networks from different deployment models using PowerShell</span></span>



<span data-ttu-id="20b6d-104">이 문서 tooconnect 클래식 Vnet tooResource 관리자 Vnet tooallow 서로 hello 별도 배포 모델 toocommunicate에 배치 된 리소스를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-104">This article shows you how tooconnect classic VNets tooResource Manager VNets tooallow hello resources located in hello separate deployment models toocommunicate with each other.</span></span> <span data-ttu-id="20b6d-105">이 문서의 단계 hello PowerShell을 사용 하지만 hello 문서가이 목록에서 선택 하 여 hello Azure 포털을 사용 하 여이 구성을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-105">hello steps in this article use PowerShell, but you can also create this configuration using hello Azure portal by selecting hello article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="20b6d-106">포털</span><span class="sxs-lookup"><span data-stu-id="20b6d-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="20b6d-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="20b6d-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="20b6d-108">비슷한 tooconnecting VNet tooan 온-프레미스 사이트 위치는 클래식 VNet tooa 리소스 관리자 VNet를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-108">Connecting a classic VNet tooa Resource Manager VNet is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="20b6d-109">두 연결 유형에서는 VPN 게이트웨이 tooprovide IPsec/IKE를 사용 하 여 보안 터널을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-109">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="20b6d-110">다른 구독 및 다른 지역에 있는 VNet 간에 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="20b6d-111">으로 구성 된 hello 게이트웨이 동적 또는 경로 기반으로 연결 tooon 온-프레미스 네트워크에 이미 있는 Vnet을 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-111">You can also connect VNets that already have connections tooon-premises networks, as long as hello gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="20b6d-112">VNet 대 VNet 연결에 대 한 자세한 내용은 참조 hello [VNet 대 VNet FAQ](#faq) hello이이 문서의 뒷부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-112">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span> 

<span data-ttu-id="20b6d-113">Vnet hello에 있는 경우 동일한 지역 경우가 있습니다 tooinstead VNet 피어 링을 사용 하 여 연결을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-113">If your VNets are in hello same region, you may want tooinstead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="20b6d-114">VNet 피어링은 VPN Gateway를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="20b6d-115">자세한 내용은 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20b6d-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

## <a name="before-beginning"></a><span data-ttu-id="20b6d-116">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="20b6d-116">Before beginning</span></span>

<span data-ttu-id="20b6d-117">hello 다음 단계 과정을 단계별로 hello 설정 필요한 tooconfigure 동적 또는 경로 기반 게이트웨이 각 VNet에 대 한 고 hello 게이트웨이 간에 VPN 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-117">hello following steps walk you through hello settings necessary tooconfigure a dynamic or route-based gateway for each VNet and create a VPN connection between hello gateways.</span></span> <span data-ttu-id="20b6d-118">이 구성은 고정 또는 정책 기반 게이트웨이를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-118">This configuration does not support static or policy-based gateways.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="20b6d-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="20b6d-119">Prerequisites</span></span>

* <span data-ttu-id="20b6d-120">두 VNet이 이미 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-120">Both VNets have already been created.</span></span>
* <span data-ttu-id="20b6d-121">Vnet을 서로 중첩 하지 않거나 겹치는 hello에 대 한 주소 범위 hello hello 게이트웨이에 연결할 수 있습니다 하는 다른 연결에 대 한 hello 범위를 사용 하 여입니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-121">hello address ranges for hello VNets do not overlap with each other, or overlap with any of hello ranges for other connections that hello gateways may be connected to.</span></span>
* <span data-ttu-id="20b6d-122">Hello 최신 PowerShell cmdlet을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-122">You have installed hello latest PowerShell cmdlets.</span></span> <span data-ttu-id="20b6d-123">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span> <span data-ttu-id="20b6d-124">서비스 관리 (SM) hello와 hello 관리자 RM (리소스) cmdlet 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-124">Make sure you install both hello Service Management (SM) and hello Resource Manager (RM) cmdlets.</span></span> 

### <span data-ttu-id="20b6d-125"><a name="exampleref"></a>예제 설정</span><span class="sxs-lookup"><span data-stu-id="20b6d-125"><a name="exampleref"></a>Example settings</span></span>

<span data-ttu-id="20b6d-126">이러한 값 toocreate 테스트 환경을 사용 하거나 toothem 참조 toobetter hello이이 문서의 예제에서는 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-126">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

<span data-ttu-id="20b6d-127">**클래식 VNet 설정**</span><span class="sxs-lookup"><span data-stu-id="20b6d-127">**Classic VNet settings**</span></span>

<span data-ttu-id="20b6d-128">VNet 이름 = ClassicVNet </span><span class="sxs-lookup"><span data-stu-id="20b6d-128">VNet Name = ClassicVNet</span></span> <br>
<span data-ttu-id="20b6d-129">Location = West US</span><span class="sxs-lookup"><span data-stu-id="20b6d-129">Location = West US</span></span> <br>
<span data-ttu-id="20b6d-130">Virtual Network Address Spaces = 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="20b6d-130">Virtual Network Address Spaces = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="20b6d-131">Subnet-1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="20b6d-131">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="20b6d-132">GatewaySubnet = 10.0.0.32/29</span><span class="sxs-lookup"><span data-stu-id="20b6d-132">GatewaySubnet = 10.0.0.32/29</span></span> <br>
<span data-ttu-id="20b6d-133">Local Network Name = RMVNetLocal</span><span class="sxs-lookup"><span data-stu-id="20b6d-133">Local Network Name = RMVNetLocal</span></span> <br>
<span data-ttu-id="20b6d-134">GatewayType = DynamicRouting</span><span class="sxs-lookup"><span data-stu-id="20b6d-134">GatewayType = DynamicRouting</span></span>

<span data-ttu-id="20b6d-135">**Resource Manager VNet 설정**</span><span class="sxs-lookup"><span data-stu-id="20b6d-135">**Resource Manager VNet settings**</span></span>

<span data-ttu-id="20b6d-136">VNet 이름 = RMVNet </span><span class="sxs-lookup"><span data-stu-id="20b6d-136">VNet Name = RMVNet</span></span> <br>
<span data-ttu-id="20b6d-137">Resource Group = RG1</span><span class="sxs-lookup"><span data-stu-id="20b6d-137">Resource Group = RG1</span></span> <br>
<span data-ttu-id="20b6d-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="20b6d-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="20b6d-139">Subnet-1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="20b6d-139">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="20b6d-140">GatewaySubnet = 192.168.0.0/26</span><span class="sxs-lookup"><span data-stu-id="20b6d-140">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="20b6d-141">Location = East US</span><span class="sxs-lookup"><span data-stu-id="20b6d-141">Location = East US</span></span> <br>
<span data-ttu-id="20b6d-142">Gateway public IP name = gwpip</span><span class="sxs-lookup"><span data-stu-id="20b6d-142">Gateway public IP name = gwpip</span></span> <br>
<span data-ttu-id="20b6d-143">Local Network Gateway = ClassicVNetLocal</span><span class="sxs-lookup"><span data-stu-id="20b6d-143">Local Network Gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="20b6d-144">Virtual Network Gateway name = RMGateway</span><span class="sxs-lookup"><span data-stu-id="20b6d-144">Virtual Network Gateway name = RMGateway</span></span> <br>
<span data-ttu-id="20b6d-145">게이트웨이 IP 주소 구성 = gwipconfig</span><span class="sxs-lookup"><span data-stu-id="20b6d-145">Gateway IP addressing configuration = gwipconfig</span></span>

## <span data-ttu-id="20b6d-146"><a name="createsmgw"></a>섹션 1-구성 클래식 VNet hello</span><span class="sxs-lookup"><span data-stu-id="20b6d-146"><a name="createsmgw"></a>Section 1 - Configure hello classic VNet</span></span>
### <a name="part-1---download-your-network-configuration-file"></a><span data-ttu-id="20b6d-147">1부 - 네트워크 구성 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="20b6d-147">Part 1 - Download your network configuration file</span></span>
1. <span data-ttu-id="20b6d-148">관리자 권한을 가진 hello PowerShell 콘솔에서 Azure 계정 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-148">Log in tooyour Azure account in hello PowerShell console with elevated rights.</span></span> <span data-ttu-id="20b6d-149">hello 다음 cmdlet hello 로그인 자격 증명을 묻는 Azure 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-149">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="20b6d-150">로그인 한 후 PowerShell tooAzure를 사용할 수 있도록 계정 설정을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-150">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span> <span data-ttu-id="20b6d-151">이 부분의 hello 구성 SM PowerShell cmdlet toocomplete hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-151">You use hello SM PowerShell cmdlets toocomplete this part of hello configuration.</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="20b6d-152">Hello 다음 명령을 실행 하 여 Azure 네트워크 구성 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-152">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="20b6d-153">Hello 위치의 hello tooexport tooa 다른 필요한 경우 파일 위치를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-153">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. <span data-ttu-id="20b6d-154">열기 hello.xml 파일 tooedit 다운로드 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-154">Open hello .xml file that you downloaded tooedit it.</span></span> <span data-ttu-id="20b6d-155">예를 보려면 hello 네트워크 구성 파일 참조 hello [네트워크 구성 스키마](https://msdn.microsoft.com/library/jj157100.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-155">For an example of hello network configuration file, see hello [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span></span>

### <a name="part-2--verify-hello-gateway-subnet"></a><span data-ttu-id="20b6d-156">파트 2-hello 게이트웨이 서브넷을 확인</span><span class="sxs-lookup"><span data-stu-id="20b6d-156">Part 2 -Verify hello gateway subnet</span></span>
<span data-ttu-id="20b6d-157">Hello에 **VirtualNetworkSites** 요소를 하나 아직 만들어지지 않은 경우 게이트웨이 서브넷 tooyour VNet을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-157">In hello **VirtualNetworkSites** element, add a gateway subnet tooyour VNet if one has not already been created.</span></span> <span data-ttu-id="20b6d-158">Hello 네트워크 구성 파일에서 작업할 때는 hello 게이트웨이 서브넷 이름을 지정 해야 "GatewaySubnet" 또는 Azure에서 인식 하 고 게이트웨이 서브넷으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-158">When working with hello network configuration file, hello gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="20b6d-159">**예제:**</span><span class="sxs-lookup"><span data-stu-id="20b6d-159">**Example:**</span></span>

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

### <a name="part-3---add-hello-local-network-site"></a><span data-ttu-id="20b6d-160">3 부-hello 로컬 네트워크 사이트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-160">Part 3 - Add hello local network site</span></span>
<span data-ttu-id="20b6d-161">hello 로컬 네트워크 사이트를 추가 하면 tooconnect 원하는 RM VNet toowhich hello를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-161">hello local network site you add represents hello RM VNet toowhich you want tooconnect.</span></span> <span data-ttu-id="20b6d-162">추가 **LocalNetworkSites** 요소 toohello 파일이 존재 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="20b6d-162">Add a **LocalNetworkSites** element toohello file if one doesn't already exist.</span></span> <span data-ttu-id="20b6d-163">이 시점에서 hello 구성에서 hello VPNGatewayAddress 수 때문일 모든 유효한 공용 IP 주소 아직 리소스 관리자 VNet hello에 대 한 hello 게이트웨이 만들지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-163">At this point in hello configuration, hello VPNGatewayAddress can be any valid public IP address because we haven't yet created hello gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="20b6d-164">Hello 게이트웨이 작성 하는 것이 자리 표시자 IP 주소를 hello 올바른 공용 IP 주소와 toohello RM 게이트웨이에 할당 된 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-164">Once we create hello gateway, we replace this placeholder IP address with hello correct public IP address that has been assigned toohello RM gateway.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a><span data-ttu-id="20b6d-165">-4 부 hello 로컬 네트워크 사이트와 연결할 hello VNet</span><span class="sxs-lookup"><span data-stu-id="20b6d-165">Part 4 - Associate hello VNet with hello local network site</span></span>
<span data-ttu-id="20b6d-166">이 섹션에서는 원하는 tooconnect hello 로컬 네트워크 사이트 지정 VNet 대 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-166">In this section, we specify hello local network site that you want tooconnect hello VNet to.</span></span> <span data-ttu-id="20b6d-167">이 경우 이전에 참조 되는 리소스 관리자 VNet hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-167">In this case, it is hello Resource Manager VNet that you referenced earlier.</span></span> <span data-ttu-id="20b6d-168">있는지 hello 이름을 일치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-168">Make sure hello names match.</span></span> <span data-ttu-id="20b6d-169">이 단계에서는 게이트웨이를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-169">This step does not create a gateway.</span></span> <span data-ttu-id="20b6d-170">Hello 로컬 네트워크 게이트웨이 hello에에 연결을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-170">It specifies hello local network that hello gateway will connect to.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a><span data-ttu-id="20b6d-171">5 부-hello 파일을 저장 하 고, 업로드</span><span class="sxs-lookup"><span data-stu-id="20b6d-171">Part 5 - Save hello file and upload</span></span>
<span data-ttu-id="20b6d-172">Hello 파일을 저장 한 후 hello 다음 명령을 실행 하 여 tooAzure을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-172">Save hello file, then import it tooAzure by running hello following command.</span></span> <span data-ttu-id="20b6d-173">사용자 환경의 필요에 따라 hello 파일 경로 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-173">Make sure you change hello file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="20b6d-174">Hello 가져오기 성공 했는지 보여 주는 비슷한 결과 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-174">You will see a similar result showing that hello import succeeded.</span></span>

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a><span data-ttu-id="20b6d-175">6 단계-hello 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="20b6d-175">Part 6 - Create hello gateway</span></span>

<span data-ttu-id="20b6d-176">이 예제를 실행 하기 전에 toohello 참조 hello 정확한 이름을 해당 Azure에 대 한 다운로드 한 네트워크 구성 파일에서는 toosee 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-176">Before running this example, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="20b6d-177">클래식 가상 네트워크에 대 한 hello 값을 포함 하는 hello 네트워크 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-177">hello network configuration file contains hello values for your classic virtual networks.</span></span> <span data-ttu-id="20b6d-178">경우에 따라 클래식에서 클래식 VNet 설정을 만들 때 Vnet hello 네트워크 구성 파일에서 변경 된에 대 한 hello 이름을 hello hello 배포 모델의 toohello 차이 때문에 Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-178">Sometimes hello names for classic VNets are changed in hello network configuration file when creating classic VNet settings in hello Azure portal due toohello differences in hello deployment models.</span></span> <span data-ttu-id="20b6d-179">예를 들어 Azure 포털 toocreate 클래식 VNet 라는 ' 클래식 VNet' 및 'ClassicRG' 라는 리소스 그룹에서 만든 hello를 사용 하는 hello 네트워크 구성 파일에 포함 된 hello 이름이 변환된 too'Group ClassicRG 클래식 VNet 되었습니다 '.</span><span class="sxs-lookup"><span data-stu-id="20b6d-179">For example, if you used hello Azure portal toocreate a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', hello name that is contained in hello network configuration file is converted too'Group ClassicRG Classic VNet'.</span></span> <span data-ttu-id="20b6d-180">공백이 포함 된 VNet의 hello 이름을 지정할 때 hello 값 주위에 따옴표를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-180">When specifying hello name of a VNet that contains spaces, use quotation marks around hello value.</span></span>


<span data-ttu-id="20b6d-181">다음 예제에서는 toocreate 동적 라우팅 게이트웨이 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-181">Use hello following example toocreate a dynamic routing gateway:</span></span>

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

<span data-ttu-id="20b6d-182">Hello를 사용 하 여 hello 게이트웨이의 hello 상태를 확인할 수 있습니다 **Get AzureVNetGateway** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="20b6d-182">You can check hello status of hello gateway by using hello **Get-AzureVNetGateway** cmdlet.</span></span>

## <span data-ttu-id="20b6d-183"><a name="creatermgw"></a>섹션 2: hello RM VNet 게이트웨이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-183"><a name="creatermgw"></a>Section 2: Configure hello RM VNet gateway</span></span>
<span data-ttu-id="20b6d-184">toocreate hello RM VNet에 대 한 VPN 게이트웨이 hello 다음 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-184">toocreate a VPN gateway for hello RM VNet, follow hello following instructions.</span></span> <span data-ttu-id="20b6d-185">Hello hello 클래식 VNet 게이트웨이 공용 IP 주소를 검색 한 후 hello 설명 하는 단계를 시작 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="20b6d-185">Don't start hello steps until after you have retrieved hello public IP address for hello classic VNet's gateway.</span></span> 

1. <span data-ttu-id="20b6d-186">Hello PowerShell 콘솔에서 Azure 계정 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-186">Log in tooyour Azure account in hello PowerShell console.</span></span> <span data-ttu-id="20b6d-187">hello 다음 cmdlet hello 로그인 자격 증명을 묻는 Azure 계정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-187">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="20b6d-188">로그인 한 후 PowerShell tooAzure를 사용할 수 있도록 계정 설정은 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-188">After logging in, your account settings are downloaded so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  <span data-ttu-id="20b6d-189">둘 이상의 구독이 있는 경우 Azure 구독 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-189">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
   
  <span data-ttu-id="20b6d-190">Toouse hello 구독을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-190">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="20b6d-191">로컬 네트워크 게이트웨이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-191">Create a local network gateway.</span></span> <span data-ttu-id="20b6d-192">가상 네트워크에서 로컬 네트워크 게이트웨이 hello 일반적으로 tooyour 온-프레미스 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-192">In a virtual network, hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="20b6d-193">이 경우 로컬 네트워크 게이트웨이 hello tooyour 클래식 VNet을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-193">In this case, hello local network gateway refers tooyour Classic VNet.</span></span> <span data-ttu-id="20b6d-194">Azure 수 tooit를 참조 하 고으로 hello 주소 공간 접두사를 지정 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-194">Give it a name by which Azure can refer tooit, and also specify hello address space prefix.</span></span> <span data-ttu-id="20b6d-195">Azure는 tooidentify 어떤 트래픽 toosend tooyour 온-프레미스 위치를 지정 하는 hello IP 주소 접두사를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-195">Azure uses hello IP address prefix you specify tooidentify which traffic toosend tooyour on-premises location.</span></span> <span data-ttu-id="20b6d-196">게이트웨이 만들기 전에 여기에서 tooadjust hello 정보 이상 필요한 경우 수정할 수 있습니다 hello 값과 실행된 hello 샘플 다시.</span><span class="sxs-lookup"><span data-stu-id="20b6d-196">If you need tooadjust hello information here later, before creating your gateway, you can modify hello values and run hello sample again.</span></span>
   
   <span data-ttu-id="20b6d-197">**-이름** tooassign toorefer toohello 로컬 네트워크 게이트웨이 원하는 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-197">**-Name** is hello name you want tooassign toorefer toohello local network gateway.</span></span><br><span data-ttu-id="20b6d-198">
   **-AddressPrefix** 는 hello 클래식 VNet에 대 한 주소 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-198">
   **-AddressPrefix** is hello Address Space for your classic VNet.</span></span><br><span data-ttu-id="20b6d-199">
**-GatewayIpAddress** 는 hello hello 클래식 VNet 게이트웨이의 공용 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-199">
**-GatewayIpAddress** is hello public IP address of hello classic VNet's gateway.</span></span> <span data-ttu-id="20b6d-200">Toochange hello 다음 샘플 tooreflect hello 올바른 IP 주소로 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-200">Be sure toochange hello following sample tooreflect hello correct IP address.</span></span><br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. <span data-ttu-id="20b6d-201">에 대 한 공용 IP 주소 toobe toohello 할당 된 가상 네트워크 게이트웨이 리소스 관리자 VNet hello 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-201">Request a public IP address toobe allocated toohello virtual network gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="20b6d-202">원하는 toouse hello IP 주소를 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-202">You can't specify hello IP address that you want toouse.</span></span> <span data-ttu-id="20b6d-203">hello IP 주소 toohello 가상 네트워크 게이트웨이 동적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-203">hello IP address is dynamically allocated toohello virtual network gateway.</span></span> <span data-ttu-id="20b6d-204">그러나이이 hello IP 주소 변경 내용을 의미 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-204">However, this does not mean hello IP address changes.</span></span> <span data-ttu-id="20b6d-205">hello 유일한 시간 hello 가상 네트워크 게이트웨이 IP 주소 변경 내용을 게이트웨이 hello 경우는 삭제 하 고 다시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-205">hello only time hello virtual network gateway IP address changes is when hello gateway is deleted and recreated.</span></span> <span data-ttu-id="20b6d-206">크기 조정, 다시 설정, 또는 기타 내부 유지 관리/업그레이드 hello 게이트웨이의 바뀌지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-206">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of hello gateway.</span></span>

  <span data-ttu-id="20b6d-207">이 단계에서는 이후 단계에 사용되는 변수도 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-207">In this step, we also set a variable that is used in a later step.</span></span>

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. <span data-ttu-id="20b6d-208">가상 네트워크에 게이트웨이 서브넷이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-208">Verify that your virtual network has a gateway subnet.</span></span> <span data-ttu-id="20b6d-209">게이트웨이 서브넷이 없다면 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-209">If no gateway subnet exists, add one.</span></span> <span data-ttu-id="20b6d-210">Hello 게이트웨이 서브넷 이름이 있는지 확인 *GatewaySubnet*합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-210">Make sure hello gateway subnet is named *GatewaySubnet*.</span></span>
5. <span data-ttu-id="20b6d-211">Hello 다음 명령을 실행 하 여 hello 게이트웨이에 사용 하는 hello 서브넷을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-211">Retrieve hello subnet used for hello gateway by running hello following command.</span></span> <span data-ttu-id="20b6d-212">이 단계에서는 hello 다음 단계에서 사용 되는 변수 toobe도 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-212">In this step, we also set a variable toobe used in hello next step.</span></span>
   
   <span data-ttu-id="20b6d-213">**-이름** 리소스 관리자 VNet의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-213">**-Name** is hello name of your Resource Manager VNet.</span></span><br><span data-ttu-id="20b6d-214">
   **-ResourceGroupName** VNet 연결 된 해당 hello hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-214">
**-ResourceGroupName** is hello resource group that hello VNet is associated with.</span></span> <span data-ttu-id="20b6d-215">hello 게이트웨이 서브넷이이 VNet에 이미 존재 해야 하며 이름은 *GatewaySubnet* toowork 제대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-215">hello gateway subnet must already exist for this VNet and must be named *GatewaySubnet* toowork properly.</span></span><br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. <span data-ttu-id="20b6d-216">Hello 게이트웨이 IP 주소 지정 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-216">Create hello gateway IP addressing configuration.</span></span> <span data-ttu-id="20b6d-217">hello 게이트웨이 구성 hello 서브넷과 공용 IP 주소 toouse hello 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-217">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="20b6d-218">다음 샘플 toocreate hello 게이트웨이 구성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-218">Use hello following sample toocreate your gateway configuration.</span></span>

  <span data-ttu-id="20b6d-219">이 단계에서는 hello **-SubnetId** 및 **-PublicIpAddressId** 매개 변수에 전달 해야 hello id 속성 hello 서브넷 및 IP 주소 개체의 각각.</span><span class="sxs-lookup"><span data-stu-id="20b6d-219">In this step, hello **-SubnetId** and **-PublicIpAddressId** parameters must be passed hello id property from hello subnet, and IP address objects, respectively.</span></span> <span data-ttu-id="20b6d-220">간단한 문자열을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-220">You can't use a simple string.</span></span> <span data-ttu-id="20b6d-221">이러한 변수는 공용 IP hello 단계 toorequest에 설정 되 고 hello 단계 tooretrieve hello 서브넷.</span><span class="sxs-lookup"><span data-stu-id="20b6d-221">These variables are set in hello step toorequest a public IP and hello step tooretrieve hello subnet.</span></span>

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. <span data-ttu-id="20b6d-222">Hello 다음 명령을 실행 하 여 hello 리소스 관리자 가상 네트워크 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-222">Create hello Resource Manager virtual network gateway by running hello following command.</span></span> <span data-ttu-id="20b6d-223">hello `-VpnType` 해야 *RouteBased*합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-223">hello `-VpnType` must be *RouteBased*.</span></span> <span data-ttu-id="20b6d-224">Hello 게이트웨이 toocreate 45 분 이상 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-224">It can take 45 minutes or more for hello gateway toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. <span data-ttu-id="20b6d-225">Hello VPN 게이트웨이 만든 후 hello 공용 IP 주소를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-225">Copy hello public IP address once hello VPN gateway has been created.</span></span> <span data-ttu-id="20b6d-226">클래식 VNet에 대 한 hello 로컬 네트워크 설정을 구성 하는 경우 해당 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-226">You use it when you configure hello local network settings for your Classic VNet.</span></span> <span data-ttu-id="20b6d-227">Hello 다음 cmdlet tooretrieve hello 공용 IP 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-227">You can use hello following cmdlet tooretrieve hello public IP address.</span></span> <span data-ttu-id="20b6d-228">hello 공용 IP 주소에에서 나열 된 hello로 반환 *IpAddress*합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-228">hello public IP address is listed in hello return as *IpAddress*.</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a><span data-ttu-id="20b6d-229">섹션 3: hello 클래식 VNet 로컬 사이트 설정 수정</span><span class="sxs-lookup"><span data-stu-id="20b6d-229">Section 3: Modify hello classic VNet local site settings</span></span>

<span data-ttu-id="20b6d-230">이 섹션에서는 작업할 hello 클래식 VNet입니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-230">In this section, you work with hello classic VNet.</span></span> <span data-ttu-id="20b6d-231">Hello 자리 표시자 IP 주소를 사용 하는 tooconnect toohello 리소스 관리자 VNet 게이트웨이 될 hello 로컬 사이트 설정을 지정할 때 사용 되는 바꿀 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-231">You replace hello placeholder IP address that you used when specifying hello local site settings that will be used tooconnect toohello Resource Manager VNet gateway.</span></span> 

1. <span data-ttu-id="20b6d-232">Hello 네트워크 구성 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-232">Export hello network configuration file.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="20b6d-233">텍스트 편집기를 사용 하 여 VPNGatewayAddress를 hello 값을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-233">Using a text editor, modify hello value for VPNGatewayAddress.</span></span> <span data-ttu-id="20b6d-234">Hello hello 리소스 관리자 게이트웨이의 공용 IP 주소와 hello 자리 표시자 IP 주소를 바꾼 다음 hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-234">Replace hello placeholder IP address with hello public IP address of hello Resource Manager gateway and then save hello changes.</span></span>

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. <span data-ttu-id="20b6d-235">가져오기 hello 네트워크 구성 파일 tooAzure 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-235">Import hello modified network configuration file tooAzure.</span></span>

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <span data-ttu-id="20b6d-236"><a name="connect"></a>섹션 4: hello 게이트웨이 간의 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="20b6d-236"><a name="connect"></a>Section 4: Create a connection between hello gateways</span></span>
<span data-ttu-id="20b6d-237">Hello 게이트웨이 간의 연결을 만드는 PowerShell이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-237">Creating a connection between hello gateways requires PowerShell.</span></span> <span data-ttu-id="20b6d-238">Hello PowerShell cmdlet의 Azure 계정 toouse hello 클래식 버전 tooadd를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-238">You may need tooadd your Azure Account toouse hello classic version of hello  PowerShell cmdlets.</span></span> <span data-ttu-id="20b6d-239">toodo를 사용 하 여 **Add-azureaccount**합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-239">toodo so, use **Add-AzureAccount**.</span></span>

1. <span data-ttu-id="20b6d-240">Hello PowerShell 콘솔에서 공유 키를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-240">In hello PowerShell console, set your shared key.</span></span> <span data-ttu-id="20b6d-241">참조 toohello hello cmdlet을 실행 하기 전에 hello 정확한 이름을 해당 Azure에 대 한 다운로드 한 네트워크 구성 파일에서는 toosee 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-241">Before running hello cmdlets, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="20b6d-242">공백이 포함 된 VNet의 hello 이름을 지정할 때 hello 값에 단일 따옴표를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-242">When specifying hello name of a VNet that contains spaces, use single quotation marks around hello value.</span></span><br><br><span data-ttu-id="20b6d-243">다음 예에서 **-VNetName** hello의 hello 이름인 클래식 VNet 및 **-LocalNetworkSiteName** hello 로컬 네트워크 사이트에 대해 지정한 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-243">In following example, **-VNetName** is hello name of hello classic VNet and **-LocalNetworkSiteName** is hello name you specified for hello local network site.</span></span> <span data-ttu-id="20b6d-244">hello **-에서 SharedKey** 생성 하 고 지정 하는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-244">hello **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="20b6d-245">Hello 예에서 'abc123' 사용 하지만 생성 하 고 조금 더 복잡 한 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-245">In hello example, we used 'abc123', but you can generate and use something more complex.</span></span> <span data-ttu-id="20b6d-246">중요 한 점은 여기에서 지정한 hello 값 hello hello 연결을 만들 때 hello 다음 단계에서 지정 하는 같은 값 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-246">hello important thing is that hello value you specify here must be hello same value that you specify in hello next step when you create your connection.</span></span> <span data-ttu-id="20b6d-247">hello 반환 표시할지 **상태: 성공**합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-247">hello return should show **Status: Successful**.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. <span data-ttu-id="20b6d-248">Hello 다음 명령을 실행 하 여 hello VPN 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-248">Create hello VPN connection by running hello following commands:</span></span>
   
  <span data-ttu-id="20b6d-249">Hello 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-249">Set hello variables.</span></span>

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  <span data-ttu-id="20b6d-250">Hello 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-250">Create hello connection.</span></span> <span data-ttu-id="20b6d-251">해당 hello 확인 **-ConnectionType** ipsec, Vnet2Vnet 없습니다.</span><span class="sxs-lookup"><span data-stu-id="20b6d-251">Notice that hello **-ConnectionType** is IPsec, not Vnet2Vnet.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a><span data-ttu-id="20b6d-252">섹션 5: 연결 확인</span><span class="sxs-lookup"><span data-stu-id="20b6d-252">Section 5: Verify your connections</span></span>

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a><span data-ttu-id="20b6d-253">프로그램 클래식 VNet tooyour 리소스 관리자 VNet에서에서 tooverify hello 연결</span><span class="sxs-lookup"><span data-stu-id="20b6d-253">tooverify hello connection from your classic VNet tooyour Resource Manager VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="20b6d-254">PowerShell</span><span class="sxs-lookup"><span data-stu-id="20b6d-254">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="20b6d-255">Azure portal</span><span class="sxs-lookup"><span data-stu-id="20b6d-255">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a><span data-ttu-id="20b6d-256">리소스 관리자 VNet tooyour에서 tooverify hello 연결 클래식 VNet</span><span class="sxs-lookup"><span data-stu-id="20b6d-256">tooverify hello connection from your Resource Manager VNet tooyour classic VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="20b6d-257">PowerShell</span><span class="sxs-lookup"><span data-stu-id="20b6d-257">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="20b6d-258">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="20b6d-258">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="20b6d-259"><a name="faq"></a>VNet 간 FAQ</span><span class="sxs-lookup"><span data-stu-id="20b6d-259"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

