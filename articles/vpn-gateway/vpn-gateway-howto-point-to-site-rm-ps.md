---
title: "지점 및 사이트 간 연결과 인증서 인증을 사용하여 Azure Virtual Network에 컴퓨터 연결: PowerShell | Microsoft Docs"
description: "인증서 인증을 사용하여 지점 및 사이트 간 VPN 게이트웨이 연결을 만들어 가상 네트워크에 안전하게 컴퓨터를 연결합니다. 이 문서는 Resource Manager 배포 모델에 적용되며 PowerShell을 사용합니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: 2e072ada13b8c742fe7f2e14737c9376f7677906
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-a-point-to-site-connection-to-a-vnet-using-certificate-authentication-powershell"></a><span data-ttu-id="25562-104">인증서 인증을 사용하여 VNet에 지점 및 사이트 간 연결 구성: PowerShell</span><span class="sxs-lookup"><span data-stu-id="25562-104">Configure a Point-to-Site connection to a VNet using certificate authentication: PowerShell</span></span>

<span data-ttu-id="25562-105">이 문서에서는 Resource Manager 배포 모델에서 PowerShell을 사용하여 지점 및 사이트 간 연결로 VNet을 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="25562-105">This article shows you how to create a VNet with a Point-to-Site connection in the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="25562-106">이 구성은 인증서를 사용하여 연결 중인 클라이언트를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-106">This configuration uses certificates to authenticate the connecting client.</span></span> <span data-ttu-id="25562-107">다른 배포 도구 또는 배포 모델을 사용하는 경우 다음 목록에서 별도의 옵션을 선택하여 이 구성을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="25562-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="25562-108">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="25562-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="25562-109">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="25562-110">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="25562-110">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

<span data-ttu-id="25562-111">지점 및 사이트 간(P2S) VPN Gateway를 통해 개별 클라이언트 컴퓨터에서 가상 네트워크에 안전한 연결을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-111">A Point-to-Site (P2S) VPN gateway lets you create a secure connection to your virtual network from an individual client computer.</span></span> <span data-ttu-id="25562-112">지점 및 사이트 간 VPN 연결은 집 또는 회의에서 원격 통신하는 경우와 같이 원격 위치에서 VNet에 연결하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-112">Point-to-Site VPN connections are useful when you want to connect to your VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="25562-113">VNet에 연결해야 하는 몇 가지 클라이언트만 있는 경우에 사이트 간 VPN 대신 P2S VPN을 사용하는 것도 유용한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="25562-113">A P2S VPN is also a useful solution to use instead of a Site-to-Site VPN when you have only a few clients that need to connect to a VNet.</span></span>

<span data-ttu-id="25562-114">P2S는 SSL 기반 VPN 프로토콜인 SSTP(Secure Socket Tunneling Protocol)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-114">P2S uses the Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="25562-115">클라이언트 컴퓨터에서 시작하여 P2S VPN 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-115">A P2S VPN connection is established by starting it from the client computer.</span></span>

![Azure VNet-지점 및 사이트 간 연결 다이어그램에 컴퓨터 연결](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

<span data-ttu-id="25562-117">지점 및 사이트 간 인증서 인증 연결을 사용하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-117">Point-to-Site certificate authentication connections require the following:</span></span>

* <span data-ttu-id="25562-118">RouteBased VPN 게이트웨이입니다.</span><span class="sxs-lookup"><span data-stu-id="25562-118">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="25562-119">Azure에 업로드된 루트 인증서에 대한 공개 키(.cer 파일)입니다.</span><span class="sxs-lookup"><span data-stu-id="25562-119">The public key (.cer file) for a root certificate, which is uploaded to Azure.</span></span> <span data-ttu-id="25562-120">인증서가 업로드되면 신뢰할 수 있는 인증서로 간주되며 인증에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="25562-120">Once the certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="25562-121">루트 인증서에서 생성되고 VNet에 연결할 각 클라이언트 컴퓨터에 설치된 클라이언트 인증서.</span><span class="sxs-lookup"><span data-stu-id="25562-121">A client certificate that is generated from the root certificate and installed on each client computer that will connect to the VNet.</span></span> <span data-ttu-id="25562-122">클라이언트 인증에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="25562-122">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="25562-123">VPN 클라이언트 구성 패키지.</span><span class="sxs-lookup"><span data-stu-id="25562-123">A VPN client configuration package.</span></span> <span data-ttu-id="25562-124">VPN 클라이언트 구성 패키지에는 클라이언트를 VNet에 연결하는 데 필요한 정보가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-124">The VPN client configuration package contains the necessary information for the client to connect to the VNet.</span></span> <span data-ttu-id="25562-125">패키지는 Windows 운영 체제에 기본적으로 제공된 기존의 VPN 클라이언트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-125">The package configures the existing VPN client that is native to the Windows operating system.</span></span> <span data-ttu-id="25562-126">구성 패키지를 사용하여 연결되는 각 클라이언트를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-126">Each client that connects must be configured using the configuration package.</span></span>

<span data-ttu-id="25562-127">지점 및 사이트 간 연결에는 VPN 장치 또는 온-프레미스 공용 IP 주소가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-127">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="25562-128">VPN 연결은 SSTP(Secure Socket Tunneling Protocol)를 통해 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="25562-128">The VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="25562-129">서버 쪽에서 SSTP 버전 1.0, 1.1 및 1.2를 지원하며,</span><span class="sxs-lookup"><span data-stu-id="25562-129">On the server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="25562-130">클라이언트에서 사용할 버전을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-130">The client decides which version to use.</span></span> <span data-ttu-id="25562-131">Windows 8.1 이상에서는 기본적으로 SSTP 버전 1.2를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-131">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="25562-132">지점 및 사이트 간 연결에 대한 자세한 내용은 이 문서의 끝에 있는 [지점 및 사이트 간 FAQ](#faq)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25562-132">For more information about Point-to-Site connections, see the [Point-to-Site FAQ](#faq) at the end of this article.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="25562-133">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="25562-133">Before beginning</span></span>

* <span data-ttu-id="25562-134">Azure 구독이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-134">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="25562-135">Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-135">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="25562-136">최신 버전의 Azure Resource Manager PowerShell cmdlet을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-136">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="25562-137">PowerShell cmdlet 설치에 대한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25562-137">For more information about installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="25562-138"><a name="example"></a>예제 값</span><span class="sxs-lookup"><span data-stu-id="25562-138"><a name="example"></a>Example values</span></span>

<span data-ttu-id="25562-139">예제 값을 사용하여 테스트 환경을 만들거나 이 값을 참조하여 이 문서의 예제를 보다 정확하게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-139">You can use the example values to create a test environment, or refer to these values to better understand the examples in this article.</span></span> <span data-ttu-id="25562-140">문서의 섹션 [1](#declare)에서 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-140">We set the variables in section [1](#declare) of the article.</span></span> <span data-ttu-id="25562-141">단계를 계속 따라가며 값을 변경 없이 사용해도 되고, 사용자 환경을 반영하도록 값을 변경해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25562-141">You can either use the steps as a walk-through and use the values without changing them, or change them to reflect your environment.</span></span> 

* <span data-ttu-id="25562-142">**이름: VNet1**</span><span class="sxs-lookup"><span data-stu-id="25562-142">**Name: VNet1**</span></span>
* <span data-ttu-id="25562-143">**주소 공간: 192.168.0.0/16** 및 **10.254.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="25562-143">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="25562-144">이 예제에서는 둘 이상의 주소 공간을 사용하여 이 구성이 여러 주소 공간에서 작동하는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="25562-144">For this example, we use more than one address space to illustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="25562-145">하지만 이 구성에 여러 주소 공간이 반드시 필요한 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="25562-145">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="25562-146">**서브넷 이름: FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="25562-146">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="25562-147">**서브넷 주소 범위: 192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="25562-147">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="25562-148">**서브넷 이름: BackEnd**</span><span class="sxs-lookup"><span data-stu-id="25562-148">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="25562-149">**서브넷 주소 범위: 10.254.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="25562-149">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="25562-150">**서브넷 이름: GatewaySubnet**</span><span class="sxs-lookup"><span data-stu-id="25562-150">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="25562-151">서브넷 이름 *GatewaySubnet*은 VPN Gateway가 작동하기 위한 필수 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="25562-151">The Subnet name *GatewaySubnet* is mandatory for the VPN gateway to work.</span></span>
  * <span data-ttu-id="25562-152">**GatewaySubnet 주소 범위: 192.168.200.0/24**</span><span class="sxs-lookup"><span data-stu-id="25562-152">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="25562-153">**VPN 클라이언트 주소 풀: 172.16.201.0/24**</span><span class="sxs-lookup"><span data-stu-id="25562-153">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="25562-154">이 지점 및 사이트 간 연결을 사용하여 VNet에 연결되는 VPN 클라이언트는 VPN 클라이언트 주소 풀에서 IP 주소를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-154">VPN clients that connect to the VNet using this Point-to-Site connection receive an IP address from the VPN client address pool.</span></span>
* <span data-ttu-id="25562-155">**구독:** 구독이 2개 이상 있는 경우 올바른 구독을 사용 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-155">**Subscription:** If you have more than one subscription, verify that you are using the correct one.</span></span>
* <span data-ttu-id="25562-156">**리소스 그룹: TestRG**</span><span class="sxs-lookup"><span data-stu-id="25562-156">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="25562-157">**위치: 미국 동부**</span><span class="sxs-lookup"><span data-stu-id="25562-157">**Location: East US**</span></span>
* <span data-ttu-id="25562-158">**DNS 서버: 이름 확인에 사용할 DNS 서버의 IP 주소**.</span><span class="sxs-lookup"><span data-stu-id="25562-158">**DNS Server: IP address** of the DNS server that you want to use for name resolution.</span></span>
* <span data-ttu-id="25562-159">**GW 이름: Vnet1GW**</span><span class="sxs-lookup"><span data-stu-id="25562-159">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="25562-160">**공용 IP 이름: VNet1GWPIP**</span><span class="sxs-lookup"><span data-stu-id="25562-160">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="25562-161">**VpnType: RouteBased**</span><span class="sxs-lookup"><span data-stu-id="25562-161">**VpnType: RouteBased**</span></span> 

## <span data-ttu-id="25562-162"><a name="declare"></a>1. 로그인 및 변수 설정</span><span class="sxs-lookup"><span data-stu-id="25562-162"><a name="declare"></a>1. Log in and set variables</span></span>

<span data-ttu-id="25562-163">이 섹션에서는 로그인하고 이 구성에 사용되는 값을 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-163">In this section, you log in and declare the values used for this configuration.</span></span> <span data-ttu-id="25562-164">선언된 값은 예제 스크립트에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="25562-164">The declared values are used in the sample scripts.</span></span> <span data-ttu-id="25562-165">값을 변경하여 고유한 환경을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-165">Change the values to reflect your own environment.</span></span> <span data-ttu-id="25562-166">또는 선언된 값을 사용하고 단계를 연습 삼아 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-166">Or, you can use the declared values and go through the steps as an exercise.</span></span>

1. <span data-ttu-id="25562-167">상승된 권한으로 PowerShell 콘솔을 열고 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-167">Open your PowerShell console with elevated privileges, and log in to your Azure account.</span></span> <span data-ttu-id="25562-168">이 cmdlet은 로그인 자격 증명을 요구하는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-168">This cmdlet prompts you for the login credentials.</span></span> <span data-ttu-id="25562-169">로그인한 다음 Azure PowerShell에 사용할 수 있도록 계정 설정을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-169">After logging in, it downloads your account settings so that they are available to Azure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="25562-170">Azure 구독 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="25562-170">Get a list of your Azure subscriptions.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="25562-171">사용할 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-171">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="25562-172">사용할 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-172">Declare the variables that you want to use.</span></span> <span data-ttu-id="25562-173">다음 샘플을 사용하여 필요할 때 고유한 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-173">Use the following sample, substituting the values for your own when necessary.</span></span>

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <span data-ttu-id="25562-174"><a name="ConfigureVNet"></a>2. VNet 구성</span><span class="sxs-lookup"><span data-stu-id="25562-174"><a name="ConfigureVNet"></a>2. Configure a VNet</span></span>

1. <span data-ttu-id="25562-175">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="25562-175">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="25562-176">가상 네트워크에 대한 서브넷 구성을 만들고 *FrontEnd*, *BackEnd* 및 *GatewaySubnet*으로 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-176">Create the subnet configurations for the virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="25562-177">이러한 접두사는 선언된 VNet 주소 공간의 일부여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-177">These prefixes must be part of the VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="25562-178">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="25562-178">Create the virtual network.</span></span>

  <span data-ttu-id="25562-179">이 예제에서 DNS 서버는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="25562-179">In this example, the DNS server is optional.</span></span> <span data-ttu-id="25562-180">값을 지정하더라도 새 DNS 서버를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-180">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="25562-181">지정한 DNS 서버는 연결 중인 리소스에 대한 이름을 확인할 수 있는 DNS 서버 IP 주소여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-181">The DNS server IP address that you specify should be a DNS server that can resolve the names for the resources you are connecting to.</span></span> <span data-ttu-id="25562-182">이 예에서는 개인 IP 주소를 사용하지만 DNS 서버의 IP 주소가 아닐 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-182">For this example, we used a private IP address, but it is likely that this is not the IP address of your DNS server.</span></span> <span data-ttu-id="25562-183">고유한 값을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-183">Be sure to use your own values.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. <span data-ttu-id="25562-184">만든 가상 네트워크에 대한 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-184">Specify the variables for the virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="25562-185">VPN Gateway에는 공용 IP 주소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-185">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="25562-186">먼저 IP 주소 리소스를 요청하고, 가상 네트워크 게이트웨이를 만들 때 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-186">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="25562-187">VPN Gateway가 생성될 때 IP 주소는 리소스에 동적으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="25562-187">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="25562-188">현재 VPN Gateway는 *동적* 공용 IP 주소 할당만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-188">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="25562-189">고정 공용 IP 주소 할당을 요청할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-189">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="25562-190">하지만 IP 주소가 VPN 게이트웨이에 할당된 후 변경되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="25562-190">However, it doesn't mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="25562-191">게이트웨이가 삭제되고 다시 만들어지는 경우에만 공용 IP 주소가 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="25562-191">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="25562-192">VPN Gateway의 크기 조정, 다시 설정 또는 기타 내부 유지 관리/업그레이드 시에는 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-192">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

  <span data-ttu-id="25562-193">동적으로 할당된 공용 IP 주소를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-193">Request a dynamically assigned public IP address.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <span data-ttu-id="25562-194"><a name="creategateway"></a>3. VPN Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="25562-194"><a name="creategateway"></a>3. Create the VPN gateway</span></span>

<span data-ttu-id="25562-195">VNet용 가상 네트워크 게이트웨이를 구성하고 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="25562-195">Configure and create the virtual network gateway for your VNet.</span></span>

* <span data-ttu-id="25562-196">*-GatewayType*은 **Vpn**이어야 하고 *-VpnType*은 **RouteBased**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-196">The *-GatewayType* must be **Vpn** and the *-VpnType* must be **RouteBased**.</span></span>
* <span data-ttu-id="25562-197">VPN 게이트웨이는 선택한 [게이트웨이 SKU](vpn-gateway-about-vpn-gateway-settings.md)에 따라 완료하는 데 최대 45분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-197">A VPN gateway can take up to 45 minutes to complete, depending on the [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <span data-ttu-id="25562-198"><a name="addresspool"></a>4. VPN 클라이언트 주소 풀 추가</span><span class="sxs-lookup"><span data-stu-id="25562-198"><a name="addresspool"></a>4. Add the VPN client address pool</span></span>

<span data-ttu-id="25562-199">VPN 게이트웨이에서 만들기를 완료한 후에 VPN 클라이언트 주소 풀을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-199">After the VPN gateway finishes creating, you can add the VPN client address pool.</span></span> <span data-ttu-id="25562-200">VPN 클라이언트 주소 풀은 연결할 때 VPN 클라이언트에서 IP 주소를 받는 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="25562-200">The VPN client address pool is the range from which the VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="25562-201">연결 원본이 되는 온-프레미스 위치 또는 연결 대상이 되는 VNet과 겹치지 않는 개인 IP 주소 범위를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-201">Use a private IP address range that does not overlap with the on-premises location that you connect from, or with the VNet that you want to connect to.</span></span> <span data-ttu-id="25562-202">이 예제에서 VPN 클라이언트 주소 풀은 1단계에서 [변수](#declare)로 선언되었습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-202">In this example, the VPN client address pool is declared as a [variable](#declare) in Step 1.</span></span>

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <span data-ttu-id="25562-203"><a name="Certificates"></a>5. 인증서 생성</span><span class="sxs-lookup"><span data-stu-id="25562-203"><a name="Certificates"></a>5. Generate certificates</span></span>

<span data-ttu-id="25562-204">인증서는 지점 및 사이트 간 VPN에 대한 VPN 클라이언트를 인증하기 위해 Azure에 의해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="25562-204">Certificates are used by Azure to authenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="25562-205">Azure에 루트 인증서의 공개 키 정보를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-205">You upload the public key information of the root certificate to Azure.</span></span> <span data-ttu-id="25562-206">그러면 해당 공개 키가 '신뢰할 수 있는 키'로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="25562-206">The public key is then considered 'trusted'.</span></span> <span data-ttu-id="25562-207">클라이언트 인증서는 신뢰할 수 있는 루트 인증서에서 생성한 다음 각 클라이언트 컴퓨터의 [인증서 - 현재 사용자/개인] 인증서 저장소에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-207">Client certificates must be generated from the trusted root certificate, and then installed on each client computer in the Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="25562-208">인증서는 VNet에 대한 연결을 시작할 때 해당 클라이언트를 인증하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="25562-208">The certificate is used to authenticate the client when it initiates a connection to the VNet.</span></span> 

<span data-ttu-id="25562-209">자체 서명된 인증서를 사용하는 경우 특정 매개 변수를 사용하여 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-209">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="25562-210">[PowerShell 및 Windows 10](vpn-gateway-certificates-point-to-site.md)에 대한 지침을 사용하여 자체 서명된 인증서를 만들 수 있고 Windows 10을 사용하지 않는 경우 [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-210">You can create a self-signed certificate using the instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="25562-211">자체 서명된 루트 인증서 및 클라이언트 인증서를 생성할 때 지침에 나와 있는 단계를 따르는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-211">It's important that you follow the steps in the instructions when generating self-signed root certificates and client certificates.</span></span> <span data-ttu-id="25562-212">그렇지 않으면 생성된 인증서가 P2S 연결과 호환되지 않으며 연결 오류가 발생하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25562-212">Otherwise, the certificates you generate will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="25562-213"><a name="cer"></a>1. 루트 인증서용 .cer 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="25562-213"><a name="cer"></a>1. Obtain the .cer file for the root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <span data-ttu-id="25562-214"><a name="generate"></a>2. 클라이언트 인증서 생성</span><span class="sxs-lookup"><span data-stu-id="25562-214"><a name="generate"></a>2. Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="25562-215"><a name="upload"></a>6. 루트 인증서 공개 키 정보 업로드</span><span class="sxs-lookup"><span data-stu-id="25562-215"><a name="upload"></a>6. Upload the root certificate public key information</span></span>

<span data-ttu-id="25562-216">VPN 게이트웨이에서 만들기가 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-216">Verify that your VPN gateway has finished creating.</span></span> <span data-ttu-id="25562-217">완료되었으면 신뢰할 수 있는 루트 인증서의 .cer 파일(공개 키 정보 포함)을 Azure로 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-217">Once it has completed, you can upload the .cer file (which contains the public key information) for a trusted root certificate to Azure.</span></span> <span data-ttu-id="25562-218">a.cer 파일이 업로드되면 Azure는 이.cer 파일을 사용하여 신뢰할 수 있는 루트 인증서에서 생성된 클라이언트 인증서를 설치한 클라이언트를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-218">Once a.cer file is uploaded, Azure can use it to authenticate clients that have installed a client certificate generated from the trusted root certificate.</span></span> <span data-ttu-id="25562-219">필요한 경우 나중에 신뢰할 수 있는 루트 인증서 파일을 최대 20개까지 추가로 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-219">You can upload additional trusted root certificate files - up to a total of 20 - later, if needed.</span></span>

1. <span data-ttu-id="25562-220">인증서 이름에 대한 변수를 선언하고 변수를 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="25562-220">Declare the variable for your certificate name, replacing the value with your own.</span></span>

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. <span data-ttu-id="25562-221">파일 경로를 고유한 값으로 바꾼 후 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-221">Replace the file path with your own, and then run the cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. <span data-ttu-id="25562-222">공개 키 정보를 Azure에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-222">Upload the public key information to Azure.</span></span> <span data-ttu-id="25562-223">인증서 정보가 업로드되면 Azure는 이를 신뢰할 수 있는 루트 인증서로 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-223">Once the certificate information is uploaded, Azure considers this to be a trusted root certificate.</span></span>

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <span data-ttu-id="25562-224"><a name="clientconfig"></a>7. VPN 클라이언트 구성 패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="25562-224"><a name="clientconfig"></a>7. Download the VPN client configuration package</span></span>

<span data-ttu-id="25562-225">지점 및 사이트 간 VPN을 사용하여 VNet에 연결하려면, 각 클라이언트가 가상 네트워크에 연결하는 데 필요한 파일 및 설정으로 원시 VPN 클라이언트를 구성하는 클라이언트 구성 패키지를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-225">To connect to a VNet using a Point-to-Site VPN, each client must install a client configuration package that configures the native VPN client with the settings and files that are necessary to connect to the virtual network.</span></span> <span data-ttu-id="25562-226">VPN 클라이언트 구성 패키지는 원시 Windows VPN 클라이언트를 구성하며 다른 새로운 VPN 클라이언트를 설치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-226">The VPN client configuration package configures the native Windows VPN client, it doesn't install a new or different VPN client.</span></span> 

<span data-ttu-id="25562-227">버전이 클라이언트의 아키텍처와 일치하는 한 각 클라이언트 컴퓨터에서 동일한 VPN 클라이언트 구성 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-227">You can use the same VPN client configuration package on each client computer, as long as the version matches the architecture for the client.</span></span> <span data-ttu-id="25562-228">지원되는 클라이언트 운영 체제의 목록은 이 문서 끝의 [지점 및 사이트 간 연결 FAQ](#faq)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25562-228">For the list of client operating systems that are supported, see the [Point-to-Site connections FAQ](#faq) at the end of this article.</span></span>

1. <span data-ttu-id="25562-229">게이트웨이를 만들었으면 클라이언트 구성 패키지를 생성하고 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-229">After the gateway has been created, you can generate and download the client configuration package.</span></span> <span data-ttu-id="25562-230">이 예제에서는 64비트 클라이언트용 패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-230">This example downloads the package for 64-bit clients.</span></span> <span data-ttu-id="25562-231">32비트 클라이언트를 다운로드하려는 경우 'Amd64'를h 'x86'으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="25562-231">If you want to download the 32-bit client, replace 'Amd64' with 'x86'.</span></span> <span data-ttu-id="25562-232">Azure Portal을 사용하여 VPN 클라이언트를 다운로드할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-232">You can also download the VPN client by using the Azure portal.</span></span>

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. <span data-ttu-id="25562-233">패키지를 다운로드하기 위해 반환된 링크를 둘러싼 따옴표를 조심스럽게 제거한 채로 복사한 다음 웹 브라우저에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-233">Copy and paste the link that is returned to a web browser to download the package, taking care to remove the quotes surrounding the link.</span></span> 
3. <span data-ttu-id="25562-234">클라이언트 컴퓨터에 패키지를 다운하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-234">Download and install the package on the client computer.</span></span> <span data-ttu-id="25562-235">SmartScreen 팝업이 표시되면 **자세한 정보**, **실행**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-235">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="25562-236">다른 클라이언트 컴퓨터에 설치하기 위해 패키지를 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-236">You can also save the package to install on other client computers.</span></span>
4. <span data-ttu-id="25562-237">클라이언트 컴퓨터에서 **네트워크 설정**으로 이동하고 **VPN**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-237">On the client computer, navigate to **Network Settings** and click **VPN**.</span></span> <span data-ttu-id="25562-238">VPN 연결에서 연결되는 가상 네트워크의 이름을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-238">The VPN connection shows the name of the virtual network that it connects to.</span></span>

## <span data-ttu-id="25562-239"><a name="clientcertificate"></a>8. 내보낸 클라이언트 인증서 설치</span><span class="sxs-lookup"><span data-stu-id="25562-239"><a name="clientcertificate"></a>8. Install an exported client certificate</span></span>

<span data-ttu-id="25562-240">클라이언트 인증서를 생성하는 데 사용한 것 외의 클라이언트 컴퓨터에서 P2S 연결을 만들려는 경우 클라이언트 인증서를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-240">If you want to create a P2S connection from a client computer other than the one you used to generate the client certificates, you need to install a client certificate.</span></span> <span data-ttu-id="25562-241">클라이언트 인증서를 설치하는 경우 클라이언트 인증서를 내보낼 때 만든 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-241">When installing a client certificate, you need the password that was created when the client certificate was exported.</span></span> <span data-ttu-id="25562-242">일반적으로 이 인증서를 두 번 클릭하고 설치하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="25562-242">Typically, it is just a matter of double-clicking the certificate and installing it.</span></span>

<span data-ttu-id="25562-243">전체 인증서 체인(즉, 기본값)과 함께.pfx로 클라이언트 인증서를 내보냈는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-243">Make sure the client certificate was exported as a .pfx along with the entire certificate chain (which is the default).</span></span> <span data-ttu-id="25562-244">그렇지 않은 경우, 루트 인증서 정보가 클라이언트 컴퓨터에 존재하지 않으며 클라이언트를 제대로 인증할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-244">Otherwise, the root certificate information isn't present on the client computer and the client won't be able to authenticate properly.</span></span> <span data-ttu-id="25562-245">자세한 내용은 [내보낸 클라이언트 인증서 설치](vpn-gateway-certificates-point-to-site.md#install)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25562-245">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span> 

## <span data-ttu-id="25562-246"><a name="connect"></a>9. Azure에 연결</span><span class="sxs-lookup"><span data-stu-id="25562-246"><a name="connect"></a>9. Connect to Azure</span></span>

1. <span data-ttu-id="25562-247">VNet에 연결하려면 클라이언트 컴퓨터에서 VPN 연결로 이동하고 만든 VPN 연결을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-247">To connect to your VNet, on the client computer, navigate to VPN connections and locate the VPN connection that you created.</span></span> <span data-ttu-id="25562-248">가상 네트워크와 같은 이름이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="25562-248">It is named the same name as your virtual network.</span></span> <span data-ttu-id="25562-249">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-249">Click **Connect**.</span></span> <span data-ttu-id="25562-250">인증서 사용을 안내하는 팝업 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-250">A pop-up message may appear that refers to using the certificate.</span></span> <span data-ttu-id="25562-251">**계속**을 클릭하여 상승된 권한을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-251">Click **Continue** to use elevated privileges.</span></span> 
2. <span data-ttu-id="25562-252">**연결** 상태 페이지에서 **연결**을 클릭하여 연결을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-252">On the **Connection** status page, click **Connect** to start the connection.</span></span> <span data-ttu-id="25562-253">**인증서 선택** 화면에서 표시되는 클라이언트 인증서가 연결하는 데 사용할 인증서인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-253">If you see a **Select Certificate** screen, verify that the client certificate showing is the one that you want to use to connect.</span></span> <span data-ttu-id="25562-254">그렇지 않은 경우 드롭다운 화살표를 사용하여 올바른 인증서를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-254">If it is not, use the drop-down arrow to select the correct certificate, and then click **OK**.</span></span>

  ![VPN 클라이언트에서 Azure에 연결](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="25562-256">연결이 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-256">Your connection is established.</span></span>

  ![설정된 연결](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="25562-258">P2S 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="25562-258">Troubleshooting P2S connections</span></span>

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <span data-ttu-id="25562-259"><a name="verify"></a>10. 연결 확인</span><span class="sxs-lookup"><span data-stu-id="25562-259"><a name="verify"></a>10. Verify your connection</span></span>

1. <span data-ttu-id="25562-260">VPN 연결이 활성인지를 확인하려면, 관리자 권한 명령 프롬프트를 열고 *ipconfig/all*을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-260">To verify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="25562-261">결과를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-261">View the results.</span></span> <span data-ttu-id="25562-262">받은 IP 주소가 구성에 지정한 지점 및 사이트 VPN 클라이언트 주소 풀 내의 주소 중 하나인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-262">Notice that the IP address you received is one of the addresses within the Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="25562-263">결과는 다음 예제와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-263">The results are similar to this example:</span></span>

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <span data-ttu-id="25562-264"><a name="connectVM"></a>가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="25562-264"><a name="connectVM"></a>Connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <span data-ttu-id="25562-265"><a name="addremovecert"></a>루트 인증서 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="25562-265"><a name="addremovecert"></a>Add or remove a root certificate</span></span>

<span data-ttu-id="25562-266">Azure에서 신뢰할 수 있는 루트 인증서를 추가 및 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-266">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="25562-267">루트 인증서를 제거하면 해당 루트 인증서에서 생성된 인증서가 있는 클라이언트를 인증하지 못하게 되며 연결할 수도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-267">When you remove a root certificate, clients that have a certificate generated from the root certificate can't authenticate and won't be able to connect.</span></span> <span data-ttu-id="25562-268">클라이언트를 인증하고 연결하려는 경우 Azure에 (업로드된)신뢰할 수 있는 루트 인증서에서 생성된 새 클라이언트 인증서를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-268">If you want a client to authenticate and connect, you need to install a new client certificate generated from a root certificate that is trusted (uploaded) to Azure.</span></span>

### <span data-ttu-id="25562-269"><a name="addtrustedroot"></a>신뢰할 수 있는 루트 인증서를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="25562-269"><a name="addtrustedroot"></a>To add a trusted root certificate</span></span>

<span data-ttu-id="25562-270">Azure에 최대 20개의 루트 인증서 .cer 파일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-270">You can add up to 20 root certificate .cer files to Azure.</span></span> <span data-ttu-id="25562-271">다음 단계를 사용하면 루트 인증서를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-271">The following steps help you add a root certificate:</span></span>

#### <span data-ttu-id="25562-272"><a name="certmethod1"></a>방법 1</span><span class="sxs-lookup"><span data-stu-id="25562-272"><a name="certmethod1"></a>Method 1</span></span>

<span data-ttu-id="25562-273">루트 인증서를 업로드하는 가장 효율적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="25562-273">This is the most efficient method to upload a root certificate.</span></span>

1. <span data-ttu-id="25562-274">업로드할 .cer 파일을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-274">Prepare the .cer file to upload:</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. <span data-ttu-id="25562-275">파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-275">Upload the file.</span></span> <span data-ttu-id="25562-276">한 번에 하나의 파일만 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-276">You can only upload one file at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. <span data-ttu-id="25562-277">인증서 파일이 업로드되었는지 확인하려면</span><span class="sxs-lookup"><span data-stu-id="25562-277">To verify that the certificate file uploaded:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <span data-ttu-id="25562-278"><a name="certmethod2"></a>방법 2</span><span class="sxs-lookup"><span data-stu-id="25562-278"><a name="certmethod2"></a>Method 2</span></span>

<span data-ttu-id="25562-279">이 방법은 방법 1보다 더 많은 단계를 포함하지만 결과는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-279">This method is has more steps than Method 1, but has the same result.</span></span> <span data-ttu-id="25562-280">인증서 데이터를 보는 데 필요한 경우 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="25562-280">It is included in case you need to view the certificate data.</span></span>

1. <span data-ttu-id="25562-281">Azure에 추가할 새 루트 인증서를 만들고 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-281">Create and prepare the new root certificate to add to Azure.</span></span> <span data-ttu-id="25562-282">Base-64로 인코딩된 X.509(.CER)로 공개 키를 내보내고 텍스트 편집기로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="25562-282">Export the public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="25562-283">다음 예제와 같이 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-283">Copy the values, as shown in the following example:</span></span>

  ![인증서](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > <span data-ttu-id="25562-285">인증서 데이터를 복사하는 경우 캐리지 리턴 또는 줄 바꿈 없이 하나의 연속 줄로 텍스트를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-285">When copying the certificate data, make sure that you copy the text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="25562-286">캐리지 리턴 및 줄 바꿈을 보려면 '기호 표시/모든 문자 표시'에 대한 텍스트 편집기의 보기를 수정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-286">You may need to modify your view in the text editor to 'Show Symbol/Show all characters' to see the carriage returns and line feeds.</span></span>
  >
  >

2. <span data-ttu-id="25562-287">인증서 이름 및 키 정보를 변수로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-287">Specify the certificate name and key information as a variable.</span></span> <span data-ttu-id="25562-288">다음 예제에 나와 있는 것처럼 정보를 고유한 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="25562-288">Replace the information with your own, as shown in the following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="25562-289">새 루트 인증서를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-289">Add the new root certificate.</span></span> <span data-ttu-id="25562-290">한번에 하나의 인증서만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-290">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="25562-291">다음 예제를 사용하여 새 인증서가 올바르게 추가되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-291">You can verify that the new certificate was added correctly by using the following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <span data-ttu-id="25562-292"><a name="removerootcert"></a>루트 인증서를 제거하려면</span><span class="sxs-lookup"><span data-stu-id="25562-292"><a name="removerootcert"></a>To remove a root certificate</span></span>

1. <span data-ttu-id="25562-293">변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-293">Declare the variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="25562-294">인증서를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-294">Remove the certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="25562-295">다음 예제를 사용하여 인증서가 성공적으로 제거되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-295">Use the following example to verify that the certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <span data-ttu-id="25562-296"><a name="revoke"></a>클라이언트 인증서 해지</span><span class="sxs-lookup"><span data-stu-id="25562-296"><a name="revoke"></a>Revoke a client certificate</span></span>

<span data-ttu-id="25562-297">클라이언트 인증서를 해지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-297">You can revoke client certificates.</span></span> <span data-ttu-id="25562-298">인증서 해지 목록에서 개별 클라이언트 인증서를 기반으로 하는 지점 및 사이트 간 연결을 선택적으로 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-298">The certificate revocation list allows you to selectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="25562-299">이것은 신뢰할 수 있는 루트 인증서를 제거하는 것과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="25562-299">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="25562-300">Azure에서 신뢰할 수 있는 루트 인증서 .cer를 제거하면, 해지된 루트 인증서로 생성/서명된 모든 클라이언트 인증서에 대한 액세스 권한도 해지됩니다.</span><span class="sxs-lookup"><span data-stu-id="25562-300">If you remove a trusted root certificate .cer from Azure, it revokes the access for all client certificates generated/signed by the revoked root certificate.</span></span> <span data-ttu-id="25562-301">루트 인증서가 아닌 클라이언트 인증서를 해지하면 루트 인증서에서 생성된 다른 인증서를 인증에 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-301">Revoking a client certificate, rather than the root certificate, allows the other certificates that were generated from the root certificate to continue to be used for authentication.</span></span>

<span data-ttu-id="25562-302">해지된 클라이언트 인증서를 사용하는 동안 개별 사용자의 세분화된 액세스 제어를 위해 일반적으로 루트 인증서를 사용하여 팀 또는 조직 수준에서 액세스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-302">The common practice is to use the root certificate to manage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="25562-303"><a name="revokeclientcert"></a>클라이언트 인증서를 해지하려면</span><span class="sxs-lookup"><span data-stu-id="25562-303"><a name="revokeclientcert"></a>To revoke a client certificate</span></span>

1. <span data-ttu-id="25562-304">클라이언트 인증서 지문을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-304">Retrieve the client certificate thumbprint.</span></span> <span data-ttu-id="25562-305">자세한 내용은 [인증서의 지문을 검색하는 방법](https://msdn.microsoft.com/library/ms734695.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25562-305">For more information, see [How to retrieve the Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="25562-306">텍스트 편집기에 정보를 복사하고 연속 문자열이 되도록 공백을 모두 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-306">Copy the information to a text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="25562-307">이 문자열은 다음 단계에서 변수로 선언됩니다.</span><span class="sxs-lookup"><span data-stu-id="25562-307">This string is declared as a variable in the next step.</span></span>
3. <span data-ttu-id="25562-308">변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-308">Declare the variables.</span></span> <span data-ttu-id="25562-309">이전 단계에서 검색된 지문을 선언해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-309">Make sure to declare the thumbprint you retrieved in the previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="25562-310">해지된 인증서 목록에 지문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-310">Add the thumbprint to the list of revoked certificates.</span></span> <span data-ttu-id="25562-311">지문이 추가되면 "성공"이라고 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="25562-311">You see "Succeeded" when the thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="25562-312">지문이 인증서 해지 목록에 추가되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-312">Verify that the thumbprint was added to the certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="25562-313">지문이 추가된 후에는 인증서를 더 이상 연결에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-313">After the thumbprint has been added, the certificate can no longer be used to connect.</span></span> <span data-ttu-id="25562-314">이 인증서를 사용하여 연결하려는 클라이언트에서 인증서가 더 이상 유효하지 않다고 하는 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-314">Clients that try to connect using this certificate receive a message saying that the certificate is no longer valid.</span></span>

### <span data-ttu-id="25562-315"><a name="reinstateclientcert"></a>클라이언트 인증서를 복구하려면</span><span class="sxs-lookup"><span data-stu-id="25562-315"><a name="reinstateclientcert"></a>To reinstate a client certificate</span></span>

<span data-ttu-id="25562-316">해지된 클라이언트 인증서 목록에서 지문을 제거하여 클라이언트 인증서를 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-316">You can reinstate a client certificate by removing the thumbprint from the list of revoked client certificates.</span></span>

1. <span data-ttu-id="25562-317">변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-317">Declare the variables.</span></span> <span data-ttu-id="25562-318">복구하려는 인증서에 대한 올바른 지문을 선언해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-318">Make sure you declare the correct thumbprint for the certificate that you want to reinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="25562-319">인증서 지문을 인증서 해지 목록에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-319">Remove the certificate thumbprint from the certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="25562-320">해지된 목록에서 지문이 제거되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="25562-320">Check if the thumbprint is removed from the revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <span data-ttu-id="25562-321"><a name="faq"></a>지점 및 사이트 간 FAQ</span><span class="sxs-lookup"><span data-stu-id="25562-321"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="25562-322">다음 단계</span><span class="sxs-lookup"><span data-stu-id="25562-322">Next steps</span></span>
<span data-ttu-id="25562-323">연결이 완료되면 가상 네트워크에 가상 컴퓨터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25562-323">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="25562-324">자세한 내용은 [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25562-324">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="25562-325">네트워킹 및 가상 컴퓨터에 대한 자세한 내용은 [Azure 및 Linux VM 네트워크 개요](../virtual-machines/linux/azure-vm-network-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25562-325">To understand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>