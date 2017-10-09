---
title: "컴퓨터 tooan 지점-사이트를 사용 하 여 Azure 가상 네트워크를 연결 하 고 인증 인증서: PowerShell | Microsoft Docs"
description: "인증서 인증을 사용 하는 지점-사이트 VPN 게이트웨이 연결을 생성 하 여 컴퓨터 tooyour 가상 네트워크를 안전 하 게 연결 합니다. 이 문서 toohello 리소스 관리자 배포 모델을 적용 하 고는 PowerShell을 사용 합니다."
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
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a><span data-ttu-id="788f1-104">지점 및 사이트 연결 tooa VNet 구성 인증서 인증을 사용 하 여: PowerShell</span><span class="sxs-lookup"><span data-stu-id="788f1-104">Configure a Point-to-Site connection tooa VNet using certificate authentication: PowerShell</span></span>

<span data-ttu-id="788f1-105">이 문서에서는 PowerShell을 사용 하 여 toocreate hello 리소스 관리자 배포에서 지점 및 사이트 연결 VNet을 모델링 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-105">This article shows you how toocreate a VNet with a Point-to-Site connection in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="788f1-106">이 구성은 인증서 tooauthenticate hello 클라이언트 연결을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-106">This configuration uses certificates tooauthenticate hello connecting client.</span></span> <span data-ttu-id="788f1-107">또한 서로 다른 배포 도구 또는 배포 모델을 사용 하 여 hello 다음 목록에서에서 다른 옵션을 선택 하 여이 구성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="788f1-108">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="788f1-108">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="788f1-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="788f1-109">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="788f1-110">Azure Portal(클래식)</span><span class="sxs-lookup"><span data-stu-id="788f1-110">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

<span data-ttu-id="788f1-111">지점 및 사이트 간 (P2S) VPN 게이트웨이 사용 하면 개별 클라이언트 컴퓨터에서 보안 연결 tooyour 가상 네트워크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-111">A Point-to-Site (P2S) VPN gateway lets you create a secure connection tooyour virtual network from an individual client computer.</span></span> <span data-ttu-id="788f1-112">지점-사이트 VPN 연결은 tooconnect tooyour 가정 이나 회의에서 통신 하는 경우 등의 원격 위치에서 VNet을 원하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-112">Point-to-Site VPN connections are useful when you want tooconnect tooyour VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="788f1-113">P2S VPN tooconnect tooa VNet을 필요로 하는 몇 가지 클라이언트만 있으면 사이트 간 VPN 대신 유용한 솔루션 toouse 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-113">A P2S VPN is also a useful solution toouse instead of a Site-to-Site VPN when you have only a few clients that need tooconnect tooa VNet.</span></span>

<span data-ttu-id="788f1-114">P2S 사용 하 여 hello 소켓 SSTP Secure Tunneling Protocol (), SSL 기반 VPN 프로토콜인 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-114">P2S uses hello Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="788f1-115">Hello 클라이언트 컴퓨터에서 시작 하 여 P2S VPN을 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-115">A P2S VPN connection is established by starting it from hello client computer.</span></span>

![컴퓨터 tooan 지점 및 사이트 연결 다이어그램-Azure VNet를 연결 합니다.](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

<span data-ttu-id="788f1-117">지점 및 사이트 인증서 인증 연결 hello 다음에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-117">Point-to-Site certificate authentication connections require hello following:</span></span>

* <span data-ttu-id="788f1-118">RouteBased VPN 게이트웨이입니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-118">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="788f1-119">hello tooAzure 업로드 된 루트 인증서에 대 한 공개 (키.cer 파일) 키입니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-119">hello public key (.cer file) for a root certificate, which is uploaded tooAzure.</span></span> <span data-ttu-id="788f1-120">Hello 인증서를 업로드 한 후 인증서를 신뢰할 수 있는 것으로 간주 됩니다 하 고 인증을 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-120">Once hello certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="788f1-121">Hello 루트 인증서에서 생성 되 고 toohello VNet 연결 하는 각 클라이언트 컴퓨터에 설치 되는 클라이언트 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-121">A client certificate that is generated from hello root certificate and installed on each client computer that will connect toohello VNet.</span></span> <span data-ttu-id="788f1-122">클라이언트 인증에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-122">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="788f1-123">VPN 클라이언트 구성 패키지.</span><span class="sxs-lookup"><span data-stu-id="788f1-123">A VPN client configuration package.</span></span> <span data-ttu-id="788f1-124">hello VPN 클라이언트 구성 패키지 hello hello 클라이언트 tooconnect toohello VNet에 대 한 필요한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-124">hello VPN client configuration package contains hello necessary information for hello client tooconnect toohello VNet.</span></span> <span data-ttu-id="788f1-125">hello 패키지 hello 기존 VPN 클라이언트는 네이티브 toohello Windows 운영 체제를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-125">hello package configures hello existing VPN client that is native toohello Windows operating system.</span></span> <span data-ttu-id="788f1-126">연결 하는 각 클라이언트 hello 구성 패키지를 사용 하 여 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-126">Each client that connects must be configured using hello configuration package.</span></span>

<span data-ttu-id="788f1-127">지점 및 사이트 간 연결에는 VPN 장치 또는 온-프레미스 공용 IP 주소가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-127">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="788f1-128">VPN 연결 hello SSTP (Secure Socket Tunneling Protocol)를 통해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-128">hello VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="788f1-129">Hello 서버 쪽에서 SSTP 버전 1.0, 1.1 및 1.2 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-129">On hello server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="788f1-130">클라이언트 hello 어떤 버전 toouse를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-130">hello client decides which version toouse.</span></span> <span data-ttu-id="788f1-131">Windows 8.1 이상에서는 기본적으로 SSTP 버전 1.2를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-131">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="788f1-132">지점 및 사이트 간 연결에 대 한 자세한 내용은 참조 hello [지점 및 사이트 간 FAQ](#faq) hello이이 문서의 뒷부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-132">For more information about Point-to-Site connections, see hello [Point-to-Site FAQ](#faq) at hello end of this article.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="788f1-133">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="788f1-133">Before beginning</span></span>

* <span data-ttu-id="788f1-134">Azure 구독이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-134">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="788f1-135">Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-135">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="788f1-136">Hello hello Azure 리소스 관리자 PowerShell cmdlet의 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-136">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="788f1-137">PowerShell cmdlet을 설치 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-137">For more information about installing PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="788f1-138"><a name="example"></a>예제 값</span><span class="sxs-lookup"><span data-stu-id="788f1-138"><a name="example"></a>Example values</span></span>

<span data-ttu-id="788f1-139">Hello 예제 값 toocreate 테스트 환경을 사용 하거나 toothese 값을 참조할 수 있습니다 toobetter hello이이 문서의 예제에서는 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-139">You can use hello example values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article.</span></span> <span data-ttu-id="788f1-140">섹션의 hello 변수 설정 [1](#declare) hello 문서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-140">We set hello variables in section [1](#declare) of hello article.</span></span> <span data-ttu-id="788f1-141">연습으로 hello 단계를 사용 하 고 변경 없이 hello 값을 사용 하거나 tooreflect 변경할 사용자 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-141">You can either use hello steps as a walk-through and use hello values without changing them, or change them tooreflect your environment.</span></span> 

* <span data-ttu-id="788f1-142">**이름: VNet1**</span><span class="sxs-lookup"><span data-stu-id="788f1-142">**Name: VNet1**</span></span>
* <span data-ttu-id="788f1-143">**주소 공간: 192.168.0.0/16** 및 **10.254.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="788f1-143">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="788f1-144">이 예제에서는이 구성을 여러 주소 공간을 사용 하는 둘 이상의 주소 공간이 tooillustrate를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-144">For this example, we use more than one address space tooillustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="788f1-145">하지만 이 구성에 여러 주소 공간이 반드시 필요한 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-145">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="788f1-146">**서브넷 이름: FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="788f1-146">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="788f1-147">**서브넷 주소 범위: 192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="788f1-147">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="788f1-148">**서브넷 이름: BackEnd**</span><span class="sxs-lookup"><span data-stu-id="788f1-148">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="788f1-149">**서브넷 주소 범위: 10.254.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="788f1-149">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="788f1-150">**서브넷 이름: GatewaySubnet**</span><span class="sxs-lookup"><span data-stu-id="788f1-150">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="788f1-151">hello 서브넷 이름 *GatewaySubnet* hello VPN 게이트웨이 toowork 필수 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-151">hello Subnet name *GatewaySubnet* is mandatory for hello VPN gateway toowork.</span></span>
  * <span data-ttu-id="788f1-152">**GatewaySubnet 주소 범위: 192.168.200.0/24**</span><span class="sxs-lookup"><span data-stu-id="788f1-152">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="788f1-153">**VPN 클라이언트 주소 풀: 172.16.201.0/24**</span><span class="sxs-lookup"><span data-stu-id="788f1-153">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="788f1-154">Toohello VNet이 지점 및 사이트 연결을 사용 하 여 연결 하는 VPN 클라이언트 hello VPN 클라이언트 주소 풀에서에서 IP 주소를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-154">VPN clients that connect toohello VNet using this Point-to-Site connection receive an IP address from hello VPN client address pool.</span></span>
* <span data-ttu-id="788f1-155">**구독:** 사용 하 고 있는지 확인 하는 둘 이상의 구독이 있는 경우 hello 올바르다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-155">**Subscription:** If you have more than one subscription, verify that you are using hello correct one.</span></span>
* <span data-ttu-id="788f1-156">**리소스 그룹: TestRG**</span><span class="sxs-lookup"><span data-stu-id="788f1-156">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="788f1-157">**위치: 미국 동부**</span><span class="sxs-lookup"><span data-stu-id="788f1-157">**Location: East US**</span></span>
* <span data-ttu-id="788f1-158">**DNS 서버: IP 주소** hello DNS 서버의 이름 확인을 위해 toouse 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-158">**DNS Server: IP address** of hello DNS server that you want toouse for name resolution.</span></span>
* <span data-ttu-id="788f1-159">**GW 이름: Vnet1GW**</span><span class="sxs-lookup"><span data-stu-id="788f1-159">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="788f1-160">**공용 IP 이름: VNet1GWPIP**</span><span class="sxs-lookup"><span data-stu-id="788f1-160">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="788f1-161">**VpnType: RouteBased**</span><span class="sxs-lookup"><span data-stu-id="788f1-161">**VpnType: RouteBased**</span></span> 

## <span data-ttu-id="788f1-162"><a name="declare"></a>1. 로그인 및 변수 설정</span><span class="sxs-lookup"><span data-stu-id="788f1-162"><a name="declare"></a>1. Log in and set variables</span></span>

<span data-ttu-id="788f1-163">이 섹션에서는 로그인 하 고이 구성에 사용 되는 hello 값을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-163">In this section, you log in and declare hello values used for this configuration.</span></span> <span data-ttu-id="788f1-164">hello 선언 값 hello 예제 스크립트에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-164">hello declared values are used in hello sample scripts.</span></span> <span data-ttu-id="788f1-165">사용자가 자신의 환경 hello 값 tooreflect를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-165">Change hello values tooreflect your own environment.</span></span> <span data-ttu-id="788f1-166">또는 값을 선언 하는 hello를 사용 하 고 실행으로 hello 단계를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-166">Or, you can use hello declared values and go through hello steps as an exercise.</span></span>

1. <span data-ttu-id="788f1-167">상승 된 권한으로 PowerShell 콘솔을 열고 tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-167">Open your PowerShell console with elevated privileges, and log in tooyour Azure account.</span></span> <span data-ttu-id="788f1-168">이 cmdlet hello 로그인 자격 증명을 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-168">This cmdlet prompts you for hello login credentials.</span></span> <span data-ttu-id="788f1-169">로그인 한 후 PowerShell tooAzure를 사용할 수 있도록 계정 설정을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-169">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="788f1-170">Azure 구독 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-170">Get a list of your Azure subscriptions.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="788f1-171">Toouse hello 구독을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-171">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="788f1-172">원하는 toouse hello 변수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-172">Declare hello variables that you want toouse.</span></span> <span data-ttu-id="788f1-173">다음 샘플, 필요한 경우 직접에 대 한 hello 값으로 대체 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-173">Use hello following sample, substituting hello values for your own when necessary.</span></span>

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

## <span data-ttu-id="788f1-174"><a name="ConfigureVNet"></a>2. VNet 구성</span><span class="sxs-lookup"><span data-stu-id="788f1-174"><a name="ConfigureVNet"></a>2. Configure a VNet</span></span>

1. <span data-ttu-id="788f1-175">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-175">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="788f1-176">Hello 명명 하 hello 가상 네트워크의 서브넷 구성 만들기 *프런트 엔드*, *백 엔드*, 및 *GatewaySubnet*합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-176">Create hello subnet configurations for hello virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="788f1-177">이러한 접두사 hello VNet 주소 공간에서 선언한의 일부 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-177">These prefixes must be part of hello VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="788f1-178">Hello 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-178">Create hello virtual network.</span></span>

  <span data-ttu-id="788f1-179">이 예제에서는 hello DNS 서버는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-179">In this example, hello DNS server is optional.</span></span> <span data-ttu-id="788f1-180">값을 지정하더라도 새 DNS 서버를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-180">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="788f1-181">hello DNS 서버 IP 주소 지정 하는 DNS 서버가 있어야에 연결 하는 hello 리소스에 대 한 hello 이름을 확인할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-181">hello DNS server IP address that you specify should be a DNS server that can resolve hello names for hello resources you are connecting to.</span></span> <span data-ttu-id="788f1-182">이 예에서는 개인 IP 주소를 사용 하지만 DNS 서버의 IP 주소 hello 아닌지 가능성이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-182">For this example, we used a private IP address, but it is likely that this is not hello IP address of your DNS server.</span></span> <span data-ttu-id="788f1-183">있는지 toouse 고유한 값 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-183">Be sure toouse your own values.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. <span data-ttu-id="788f1-184">앞에서 만든 가상 네트워크 hello에 대 한 hello 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-184">Specify hello variables for hello virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="788f1-185">VPN Gateway에는 공용 IP 주소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-185">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="788f1-186">먼저 hello IP 주소 리소스를 요청 하 고 가상 네트워크 게이트웨이 만들 때 tooit를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="788f1-186">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="788f1-187">hello IP 주소를 사용 hello VPN 게이트웨이 만들 때 toohello 리소스를 동적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-187">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="788f1-188">현재 VPN Gateway는 *동적* 공용 IP 주소 할당만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-188">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="788f1-189">고정 공용 IP 주소 할당을 요청할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-189">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="788f1-190">그러나 hello IP 주소가 변경 tooyour VPN 게이트웨이에 할당 된 이후에 하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-190">However, it doesn't mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="788f1-191">hello 유일한 시간 hello 공용 IP 주소 변경 내용을 게이트웨이 hello 때 삭제 되어 다시 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-191">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="788f1-192">VPN Gateway의 크기 조정, 다시 설정 또는 기타 내부 유지 관리/업그레이드 시에는 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-192">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

  <span data-ttu-id="788f1-193">동적으로 할당된 공용 IP 주소를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-193">Request a dynamically assigned public IP address.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <span data-ttu-id="788f1-194"><a name="creategateway"></a>3. Hello VPN 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="788f1-194"><a name="creategateway"></a>3. Create hello VPN gateway</span></span>

<span data-ttu-id="788f1-195">구성 하 고 VNet에 대 한 hello 가상 네트워크 게이트웨이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-195">Configure and create hello virtual network gateway for your VNet.</span></span>

* <span data-ttu-id="788f1-196">hello *-GatewayType* 해야 **Vpn** hello 및 *-VpnType* 해야 **RouteBased**합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-196">hello *-GatewayType* must be **Vpn** and hello *-VpnType* must be **RouteBased**.</span></span>
* <span data-ttu-id="788f1-197">Hello에 따라 too45 분 toocomplete을 사용할 수 있으며 VPN 게이트웨이 [게이트웨이 sku](vpn-gateway-about-vpn-gateway-settings.md) 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-197">A VPN gateway can take up too45 minutes toocomplete, depending on hello [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <span data-ttu-id="788f1-198"><a name="addresspool"></a>4. Hello VPN 클라이언트 주소 풀이 추가</span><span class="sxs-lookup"><span data-stu-id="788f1-198"><a name="addresspool"></a>4. Add hello VPN client address pool</span></span>

<span data-ttu-id="788f1-199">Hello VPN 게이트웨이 만들기를 완료 한 후에 hello VPN 클라이언트 주소 풀을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-199">After hello VPN gateway finishes creating, you can add hello VPN client address pool.</span></span> <span data-ttu-id="788f1-200">hello VPN 클라이언트 주소 풀이 있는 hello VPN 클라이언트가 IP 주소를 받을 연결할 때 hello 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-200">hello VPN client address pool is hello range from which hello VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="788f1-201">, 연결 하는 hello 온-프레미스 위치와 또는 VNet tooconnect을 hello로 중복 되지 않는 개인 IP 주소 범위를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-201">Use a private IP address range that does not overlap with hello on-premises location that you connect from, or with hello VNet that you want tooconnect to.</span></span> <span data-ttu-id="788f1-202">이 예제에서는 VPN 클라이언트 주소 풀이 hello로 선언 되는 [변수](#declare) 1 단계에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-202">In this example, hello VPN client address pool is declared as a [variable](#declare) in Step 1.</span></span>

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <span data-ttu-id="788f1-203"><a name="Certificates"></a>5. 인증서 생성</span><span class="sxs-lookup"><span data-stu-id="788f1-203"><a name="Certificates"></a>5. Generate certificates</span></span>

<span data-ttu-id="788f1-204">인증서는 지점-사이트 Vpn에 대 한 Azure tooauthenticate VPN 클라이언트에 의해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-204">Certificates are used by Azure tooauthenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="788f1-205">Hello hello 루트 인증서 tooAzure의 공개 키 정보를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-205">You upload hello public key information of hello root certificate tooAzure.</span></span> <span data-ttu-id="788f1-206">공개 키 hello는 '신뢰할 수 있는'으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-206">hello public key is then considered 'trusted'.</span></span> <span data-ttu-id="788f1-207">클라이언트 인증서 hello 신뢰할 수 있는 루트 인증서에서 생성 하 고 hello 인증서-현재 사용자/개인 인증서 저장소에서 각 클라이언트 컴퓨터에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-207">Client certificates must be generated from hello trusted root certificate, and then installed on each client computer in hello Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="788f1-208">연결 toohello VNet을 시작할 때 hello 인증서는 사용 되는 tooauthenticate hello 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-208">hello certificate is used tooauthenticate hello client when it initiates a connection toohello VNet.</span></span> 

<span data-ttu-id="788f1-209">자체 서명된 인증서를 사용하는 경우 특정 매개 변수를 사용하여 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-209">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="788f1-210">에 대 한 hello 지침을 사용 하 여 자체 서명 된 인증서를 만들 수 있습니다 [PowerShell 및 Windows 10](vpn-gateway-certificates-point-to-site.md), Windows 10를 설정 하지 않은 경우 사용할 수 있습니다 또는 [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-210">You can create a self-signed certificate using hello instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="788f1-211">자체 서명 된 루트 인증서 및 클라이언트 인증서를 생성할 때 hello 지침에 설명 된 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-211">It's important that you follow hello steps in hello instructions when generating self-signed root certificates and client certificates.</span></span> <span data-ttu-id="788f1-212">그렇지 않으면 hello 인증서 생성 P2S 연결와 호환 되지 않으며 연결 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-212">Otherwise, hello certificates you generate will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="788f1-213"><a name="cer"></a>1. Hello 루트 인증서에 대 한 hello.cer 파일을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="788f1-213"><a name="cer"></a>1. Obtain hello .cer file for hello root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <span data-ttu-id="788f1-214"><a name="generate"></a>2. 클라이언트 인증서 생성</span><span class="sxs-lookup"><span data-stu-id="788f1-214"><a name="generate"></a>2. Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="788f1-215"><a name="upload"></a>6. Hello 루트 인증서 공개 키 정보를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-215"><a name="upload"></a>6. Upload hello root certificate public key information</span></span>

<span data-ttu-id="788f1-216">VPN 게이트웨이에서 만들기가 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-216">Verify that your VPN gateway has finished creating.</span></span> <span data-ttu-id="788f1-217">완료 되 면 신뢰할 수 있는 루트 인증서 tooAzure에 대 한 (을 hello 공개 키 정보를 포함) hello.cer 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-217">Once it has completed, you can upload hello .cer file (which contains hello public key information) for a trusted root certificate tooAzure.</span></span> <span data-ttu-id="788f1-218">A.cer 파일이 업로드 되 면 Azure 사용할 수 tooauthenticate 클라이언트 hello 신뢰할 수 있는 루트 인증서에서 생성 된 클라이언트 인증서를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-218">Once a.cer file is uploaded, Azure can use it tooauthenticate clients that have installed a client certificate generated from hello trusted root certificate.</span></span> <span data-ttu-id="788f1-219">필요한 경우-tooa 총 20-나중를 신뢰할 수 있는 루트 인증서 파일을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-219">You can upload additional trusted root certificate files - up tooa total of 20 - later, if needed.</span></span>

1. <span data-ttu-id="788f1-220">사용자 고유의 hello 값 대체에 인증서 이름에 대 한 hello 변수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-220">Declare hello variable for your certificate name, replacing hello value with your own.</span></span>

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. <span data-ttu-id="788f1-221">고유의으로 hello 파일 경로 대체 하 고 hello cmdlet을 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="788f1-221">Replace hello file path with your own, and then run hello cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. <span data-ttu-id="788f1-222">공개 키 정보 tooAzure hello를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-222">Upload hello public key information tooAzure.</span></span> <span data-ttu-id="788f1-223">Hello 인증서 정보를 업로드 한 후 Azure에서는 신뢰할 수 있는 루트 인증서를이 toobe에 게 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-223">Once hello certificate information is uploaded, Azure considers this toobe a trusted root certificate.</span></span>

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <span data-ttu-id="788f1-224"><a name="clientconfig"></a>7. Hello VPN 클라이언트 구성 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-224"><a name="clientconfig"></a>7. Download hello VPN client configuration package</span></span>

<span data-ttu-id="788f1-225">hello 설정을 사용 하 여 hello 기본 VPN 클라이언트를 구성 하는 클라이언트 구성 패키지와 파일은 필요한 tooconnect toohello 가상 네트워크 tooconnect tooa VNet 지점-사이트 VPN을 사용 하 여 각 클라이언트를 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-225">tooconnect tooa VNet using a Point-to-Site VPN, each client must install a client configuration package that configures hello native VPN client with hello settings and files that are necessary tooconnect toohello virtual network.</span></span> <span data-ttu-id="788f1-226">hello 네이티브 Windows VPN 클라이언트를 구성 하는 hello VPN 클라이언트 구성 패키지, 다른 또는 새로운 VPN 클라이언트를 설치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-226">hello VPN client configuration package configures hello native Windows VPN client, it doesn't install a new or different VPN client.</span></span> 

<span data-ttu-id="788f1-227">클라이언트 hello에 대 한 hello 아키텍처를 일치 하는 hello 버전으로 각 클라이언트 컴퓨터에서 동일한 VPN 클라이언트 구성 패키지 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-227">You can use hello same VPN client configuration package on each client computer, as long as hello version matches hello architecture for hello client.</span></span> <span data-ttu-id="788f1-228">지원 되는 클라이언트 운영 체제의 hello 목록 참조 hello [지점 및 사이트 연결 FAQ](#faq) hello이이 문서의 뒷부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-228">For hello list of client operating systems that are supported, see hello [Point-to-Site connections FAQ](#faq) at hello end of this article.</span></span>

1. <span data-ttu-id="788f1-229">Hello 게이트웨이 만든 후에 생성 및 hello 클라이언트 구성 패키지를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-229">After hello gateway has been created, you can generate and download hello client configuration package.</span></span> <span data-ttu-id="788f1-230">이 예제에서는 64 비트 클라이언트에 대 한 hello 패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-230">This example downloads hello package for 64-bit clients.</span></span> <span data-ttu-id="788f1-231">Toodownload hello 32 비트 클라이언트 하려는 경우 'Amd64를'를 'x86' 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-231">If you want toodownload hello 32-bit client, replace 'Amd64' with 'x86'.</span></span> <span data-ttu-id="788f1-232">또한 hello Azure 포털을 사용 하 여 hello VPN 클라이언트를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-232">You can also download hello VPN client by using hello Azure portal.</span></span>

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. <span data-ttu-id="788f1-233">복사한 tooa 웹 브라우저 toodownload hello 패키지 hello 링크 주변 tooremove hello 따옴표 처리를 반환 하는 hello 링크를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-233">Copy and paste hello link that is returned tooa web browser toodownload hello package, taking care tooremove hello quotes surrounding hello link.</span></span> 
3. <span data-ttu-id="788f1-234">다운로드 하 고 hello 패키지 hello 클라이언트 컴퓨터에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-234">Download and install hello package on hello client computer.</span></span> <span data-ttu-id="788f1-235">SmartScreen 팝업이 표시되면 **자세한 정보**, **실행**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-235">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="788f1-236">Hello 패키지 tooinstall 다른 클라이언트 컴퓨터에 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-236">You can also save hello package tooinstall on other client computers.</span></span>
4. <span data-ttu-id="788f1-237">Hello 클라이언트 컴퓨터에서 이동 너무**네트워크 설정** 클릭 **VPN**합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-237">On hello client computer, navigate too**Network Settings** and click **VPN**.</span></span> <span data-ttu-id="788f1-238">hello VPN 연결에 연결 하는 hello 가상 네트워크의 hello 이름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-238">hello VPN connection shows hello name of hello virtual network that it connects to.</span></span>

## <span data-ttu-id="788f1-239"><a name="clientcertificate"></a>8. 내보낸 클라이언트 인증서 설치</span><span class="sxs-lookup"><span data-stu-id="788f1-239"><a name="clientcertificate"></a>8. Install an exported client certificate</span></span>

<span data-ttu-id="788f1-240">Hello 아닌 클라이언트 컴퓨터에서 toogenerate hello 클라이언트 인증서를 사용 하는 P2S toocreate 연결 tooinstall 클라이언트 인증서를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-240">If you want toocreate a P2S connection from a client computer other than hello one you used toogenerate hello client certificates, you need tooinstall a client certificate.</span></span> <span data-ttu-id="788f1-241">클라이언트 인증서를 설치할 때 클라이언트 인증서 hello을 내보낼 때 만든 hello 암호가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-241">When installing a client certificate, you need hello password that was created when hello client certificate was exported.</span></span> <span data-ttu-id="788f1-242">일반적으로의 hello 인증서를 두 번 클릭 하 고 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-242">Typically, it is just a matter of double-clicking hello certificate and installing it.</span></span>

<span data-ttu-id="788f1-243">Hello 클라이언트 인증서 hello 전체 인증서 체인 (즉, hello 기본값)와 함께.pfx로 내보낸 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-243">Make sure hello client certificate was exported as a .pfx along with hello entire certificate chain (which is hello default).</span></span> <span data-ttu-id="788f1-244">그렇지 않으면 hello 루트 인증서 정보를 hello 클라이언트 컴퓨터에 존재 하지 않는 및 hello 클라이언트 수 tooauthenticate를 제대로 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-244">Otherwise, hello root certificate information isn't present on hello client computer and hello client won't be able tooauthenticate properly.</span></span> <span data-ttu-id="788f1-245">자세한 내용은 [내보낸 클라이언트 인증서 설치](vpn-gateway-certificates-point-to-site.md#install)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="788f1-245">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span> 

## <span data-ttu-id="788f1-246"><a name="connect"></a>9. TooAzure 연결</span><span class="sxs-lookup"><span data-stu-id="788f1-246"><a name="connect"></a>9. Connect tooAzure</span></span>

1. <span data-ttu-id="788f1-247">hello 클라이언트 컴퓨터에서 tooconnect tooyour VNet tooVPN 연결 이동한 만든 hello VPN 연결을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-247">tooconnect tooyour VNet, on hello client computer, navigate tooVPN connections and locate hello VPN connection that you created.</span></span> <span data-ttu-id="788f1-248">가상 네트워크 이름이 hello를 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-248">It is named hello same name as your virtual network.</span></span> <span data-ttu-id="788f1-249">**Connect**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-249">Click **Connect**.</span></span> <span data-ttu-id="788f1-250">팝업 메시지 toousing hello 인증서 참조 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-250">A pop-up message may appear that refers toousing hello certificate.</span></span> <span data-ttu-id="788f1-251">클릭 **계속** toouse 상승 된 권한을 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-251">Click **Continue** toouse elevated privileges.</span></span> 
2. <span data-ttu-id="788f1-252">Hello에 **연결** 상태 페이지 클릭 **연결** toostart hello 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-252">On hello **Connection** status page, click **Connect** toostart hello connection.</span></span> <span data-ttu-id="788f1-253">표시 되 면 한 **인증서 선택** 화면에서 클라이언트 인증서 표시 된 hello toouse tooconnect 원하는 hello 하나 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-253">If you see a **Select Certificate** screen, verify that hello client certificate showing is hello one that you want toouse tooconnect.</span></span> <span data-ttu-id="788f1-254">없는 경우 hello 드롭 다운 화살표 tooselect hello 올바른 인증서를 사용 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-254">If it is not, use hello drop-down arrow tooselect hello correct certificate, and then click **OK**.</span></span>

  ![VPN 클라이언트가 tooAzure 연결](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="788f1-256">연결이 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-256">Your connection is established.</span></span>

  ![설정된 연결](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="788f1-258">P2S 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="788f1-258">Troubleshooting P2S connections</span></span>

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <span data-ttu-id="788f1-259"><a name="verify"></a>10. 연결 확인</span><span class="sxs-lookup"><span data-stu-id="788f1-259"><a name="verify"></a>10. Verify your connection</span></span>

1. <span data-ttu-id="788f1-260">VPN 연결을 활성 상태 인지 tooverify 관리자 명령 프롬프트를 열고 실행 *ipconfig/all*합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-260">tooverify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="788f1-261">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-261">View hello results.</span></span> <span data-ttu-id="788f1-262">받은 hello IP 주소가 구성에 지정 된 hello 지점-사이트 VPN 클라이언트 주소 풀 내의 hello 주소 중 하나 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-262">Notice that hello IP address you received is one of hello addresses within hello Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="788f1-263">hello 결과 비슷한 toothis 예제.</span><span class="sxs-lookup"><span data-stu-id="788f1-263">hello results are similar toothis example:</span></span>

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

## <span data-ttu-id="788f1-264"><a name="connectVM"></a>Tooa 가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="788f1-264"><a name="connectVM"></a>Connect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <span data-ttu-id="788f1-265"><a name="addremovecert"></a>루트 인증서 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="788f1-265"><a name="addremovecert"></a>Add or remove a root certificate</span></span>

<span data-ttu-id="788f1-266">Azure에서 신뢰할 수 있는 루트 인증서를 추가 및 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-266">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="788f1-267">루트 인증서를 제거 하면 hello 루트 인증서에서 생성 된 인증서가 있는 클라이언트를 인증할 수 없습니다 및 수 tooconnect 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-267">When you remove a root certificate, clients that have a certificate generated from hello root certificate can't authenticate and won't be able tooconnect.</span></span> <span data-ttu-id="788f1-268">클라이언트 tooauthenticate 원하는 연결 하는 경우 tooinstall 루트 인증서를 신뢰할 수 있는 (업로드) tooAzure에서 새 클라이언트 인증서를 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-268">If you want a client tooauthenticate and connect, you need tooinstall a new client certificate generated from a root certificate that is trusted (uploaded) tooAzure.</span></span>

### <span data-ttu-id="788f1-269"><a name="addtrustedroot"></a>tooadd 신뢰할 수 있는 루트 인증서</span><span class="sxs-lookup"><span data-stu-id="788f1-269"><a name="addtrustedroot"></a>tooadd a trusted root certificate</span></span>

<span data-ttu-id="788f1-270">Too20 루트 인증서.cer 파일 tooAzure를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-270">You can add up too20 root certificate .cer files tooAzure.</span></span> <span data-ttu-id="788f1-271">hello 다음 단계에서는 루트 인증서를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-271">hello following steps help you add a root certificate:</span></span>

#### <span data-ttu-id="788f1-272"><a name="certmethod1"></a>방법 1</span><span class="sxs-lookup"><span data-stu-id="788f1-272"><a name="certmethod1"></a>Method 1</span></span>

<span data-ttu-id="788f1-273">이 hello 가장 효율적인 방법 tooupload 루트 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-273">This is hello most efficient method tooupload a root certificate.</span></span>

1. <span data-ttu-id="788f1-274">.Cer 파일 tooupload hello를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-274">Prepare hello .cer file tooupload:</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. <span data-ttu-id="788f1-275">Hello 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-275">Upload hello file.</span></span> <span data-ttu-id="788f1-276">한 번에 하나의 파일만 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-276">You can only upload one file at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. <span data-ttu-id="788f1-277">tooverify 해당 hello 인증서 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-277">tooverify that hello certificate file uploaded:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <span data-ttu-id="788f1-278"><a name="certmethod2"></a>방법 2</span><span class="sxs-lookup"><span data-stu-id="788f1-278"><a name="certmethod2"></a>Method 2</span></span>

<span data-ttu-id="788f1-279">방법 1 보다 더 많은 단계를가지고 있지만이 메서드는 동일한 결과 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-279">This method is has more steps than Method 1, but has hello same result.</span></span> <span data-ttu-id="788f1-280">Tooview hello 인증서 데이터를 필요한 경우에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-280">It is included in case you need tooview hello certificate data.</span></span>

1. <span data-ttu-id="788f1-281">만들고 hello 새 루트 인증서 tooadd tooAzure를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-281">Create and prepare hello new root certificate tooadd tooAzure.</span></span> <span data-ttu-id="788f1-282">E-64로 인코딩된 X.509 대로 hello 공개 키를 내보냅니다 (합니다. CER) 하 고 텍스트 편집기로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-282">Export hello public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="788f1-283">다음 예제는 hello와 같이 hello 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-283">Copy hello values, as shown in hello following example:</span></span>

  ![인증서](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > <span data-ttu-id="788f1-285">Hello 인증서 데이터를 복사할 때 캐리지 리턴 또는 줄 바꿈 없이 한 연속 줄으로 hello 텍스트를 복사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-285">When copying hello certificate data, make sure that you copy hello text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="788f1-286">Toomodify hello 텍스트 편집기 too'Show 기호/표시 모든 문자 toosee hello 캐리지 리턴 및 줄에서 보기를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-286">You may need toomodify your view in hello text editor too'Show Symbol/Show all characters' toosee hello carriage returns and line feeds.</span></span>
  >
  >

2. <span data-ttu-id="788f1-287">변수로 hello 인증서 이름 및 키 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-287">Specify hello certificate name and key information as a variable.</span></span> <span data-ttu-id="788f1-288">다음 예제에서는 사용자 고유의 hello에서와 같이 hello 정보를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-288">Replace hello information with your own, as shown in hello following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="788f1-289">Hello 새 루트 인증서를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-289">Add hello new root certificate.</span></span> <span data-ttu-id="788f1-290">한번에 하나의 인증서만 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-290">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="788f1-291">다음 예제는 hello를 사용 하 여 해당 hello 새 인증서가 올바르게에 추가 하는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-291">You can verify that hello new certificate was added correctly by using hello following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <span data-ttu-id="788f1-292"><a name="removerootcert"></a>tooremove 루트 인증서</span><span class="sxs-lookup"><span data-stu-id="788f1-292"><a name="removerootcert"></a>tooremove a root certificate</span></span>

1. <span data-ttu-id="788f1-293">Hello 변수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-293">Declare hello variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="788f1-294">Hello 인증서를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-294">Remove hello certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="788f1-295">사용 하 여 hello 인증서 hello 예제 tooverify 다음를 제거 했습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-295">Use hello following example tooverify that hello certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <span data-ttu-id="788f1-296"><a name="revoke"></a>클라이언트 인증서 해지</span><span class="sxs-lookup"><span data-stu-id="788f1-296"><a name="revoke"></a>Revoke a client certificate</span></span>

<span data-ttu-id="788f1-297">클라이언트 인증서를 해지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-297">You can revoke client certificates.</span></span> <span data-ttu-id="788f1-298">hello 인증서 해지 목록을 통해 tooselectively 개별 클라이언트 인증서를 기반으로 하는 지점 및 사이트 연결을 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-298">hello certificate revocation list allows you tooselectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="788f1-299">이것은 신뢰할 수 있는 루트 인증서를 제거하는 것과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-299">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="788f1-300">Azure에서 신뢰할 수 있는 루트 인증서.cer를 제거 하면 모든 클라이언트 인증서를 서명 생성/된 hello 해지 된 루트 인증서에 의해 hello 액세스 권한을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-300">If you remove a trusted root certificate .cer from Azure, it revokes hello access for all client certificates generated/signed by hello revoked root certificate.</span></span> <span data-ttu-id="788f1-301">클라이언트 인증서를 해지 hello 루트 인증서를 대신 허용 hello 인증에 사용 하는 hello 루트 인증서 toocontinue toobe에서 생성 된 다른 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-301">Revoking a client certificate, rather than hello root certificate, allows hello other certificates that were generated from hello root certificate toocontinue toobe used for authentication.</span></span>

<span data-ttu-id="788f1-302">hello 일반적으로 개별 사용자에 대 한 세분화 된 액세스 제어에 대 한 해지 된 클라이언트 인증서를 사용 하는 동안 팀 또는 조직 수준에서 toouse hello 루트 인증서 toomanage 액세스가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-302">hello common practice is toouse hello root certificate toomanage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="788f1-303"><a name="revokeclientcert"></a>toorevoke 클라이언트 인증서</span><span class="sxs-lookup"><span data-stu-id="788f1-303"><a name="revokeclientcert"></a>toorevoke a client certificate</span></span>

1. <span data-ttu-id="788f1-304">Hello 클라이언트 인증서 지문을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-304">Retrieve hello client certificate thumbprint.</span></span> <span data-ttu-id="788f1-305">자세한 내용은 참조 [어떻게 tooretrieve hello 인증서의 지문을](https://msdn.microsoft.com/library/ms734695.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-305">For more information, see [How tooretrieve hello Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="788f1-306">Hello 정보 tooa 텍스트 편집기를 복사 하 고 모든 공백을 제거 하는 연속 문자열.</span><span class="sxs-lookup"><span data-stu-id="788f1-306">Copy hello information tooa text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="788f1-307">이 문자열은 hello 다음 단계에서 변수로 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-307">This string is declared as a variable in hello next step.</span></span>
3. <span data-ttu-id="788f1-308">Hello 변수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-308">Declare hello variables.</span></span> <span data-ttu-id="788f1-309">검색 있는지 toodeclare hello 지문 hello 이전 단계에서 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="788f1-309">Make sure toodeclare hello thumbprint you retrieved in hello previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="788f1-310">해지 된 인증서의 hello 지문 toohello 목록을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-310">Add hello thumbprint toohello list of revoked certificates.</span></span> <span data-ttu-id="788f1-311">Hello 지문을 추가 될 때 "Succeeded"를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="788f1-311">You see "Succeeded" when hello thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="788f1-312">해당 hello 지문 toohello 인증서 해지 목록에 추가 되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="788f1-312">Verify that hello thumbprint was added toohello certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="788f1-313">Hello 지문을 추가 된 후 hello 인증서 사용된 tooconnect를 더 이상 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-313">After hello thumbprint has been added, hello certificate can no longer be used tooconnect.</span></span> <span data-ttu-id="788f1-314">Tooconnect이이 인증서를 사용 하 여 시도 하는 클라이언트 hello 인증서를 더 이상 사용할 수 없다는 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-314">Clients that try tooconnect using this certificate receive a message saying that hello certificate is no longer valid.</span></span>

### <span data-ttu-id="788f1-315"><a name="reinstateclientcert"></a>tooreinstate 클라이언트 인증서</span><span class="sxs-lookup"><span data-stu-id="788f1-315"><a name="reinstateclientcert"></a>tooreinstate a client certificate</span></span>

<span data-ttu-id="788f1-316">Hello 지문 hello 해지 된 클라이언트 인증서 목록에서 제거 하 여 클라이언트 인증서를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-316">You can reinstate a client certificate by removing hello thumbprint from hello list of revoked client certificates.</span></span>

1. <span data-ttu-id="788f1-317">Hello 변수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-317">Declare hello variables.</span></span> <span data-ttu-id="788f1-318">Tooreinstate hello 인증서에 대 한 올바른 지문을 hello를 선언 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-318">Make sure you declare hello correct thumbprint for hello certificate that you want tooreinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="788f1-319">Hello 인증서 지문을 hello 인증서 해지 목록에서 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-319">Remove hello certificate thumbprint from hello certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="788f1-320">Hello 지문 hello 해지 목록에서 제거 되 면 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-320">Check if hello thumbprint is removed from hello revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <span data-ttu-id="788f1-321"><a name="faq"></a>지점 및 사이트 간 FAQ</span><span class="sxs-lookup"><span data-stu-id="788f1-321"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="788f1-322">다음 단계</span><span class="sxs-lookup"><span data-stu-id="788f1-322">Next steps</span></span>
<span data-ttu-id="788f1-323">연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-323">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="788f1-324">자세한 내용은 [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="788f1-324">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="788f1-325">네트워킹 및 가상 컴퓨터에 대해 자세히 toounderstand 참조 [Azure와 Linux VM 네트워크 개요](../virtual-machines/linux/azure-vm-network-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="788f1-325">toounderstand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>
