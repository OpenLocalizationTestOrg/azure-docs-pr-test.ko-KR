---
title: "VPN 게이트웨이 개요: tooAzure 가상 네트워크 크로스-프레미스 VPN 연결 만들기 | Microsoft Docs"
description: "이 VPN 게이트웨이 개요 hello 방법으로 tooconnect tooAzure 가상 네트워크 VPN 연결을 사용 하 여 hello 인터넷을 통해 설명 합니다. 기본 연결 구성의 다이어그램이 포함됩니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 2358dd5a-cd76-42c3-baf3-2f35aadc64c8
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/05/2017
ms.author: cherylmc
ms.openlocfilehash: 899270734270632a5b12d56021c924e977725a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway"></a><span data-ttu-id="a8b8d-104">VPN Gateway 정보</span><span class="sxs-lookup"><span data-stu-id="a8b8d-104">About VPN Gateway</span></span>

<span data-ttu-id="a8b8d-105">VPN 게이트웨이 가상 네트워크 게이트웨이 공용 연결 tooan 간에 암호화 된 트래픽을 온-프레미스 위치 보내는 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-105">A VPN gateway is a type of virtual network gateway that sends encrypted traffic across a public connection tooan on-premises location.</span></span> <span data-ttu-id="a8b8d-106">또한 hello Microsoft 네트워크를 통해 Azure 가상 네트워크 간의 VPN 게이트웨이 toosend 암호화 된 트래픽을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-106">You can also use VPN gateways toosend encrypted traffic between Azure virtual networks over hello Microsoft network.</span></span> <span data-ttu-id="a8b8d-107">Azure 가상 네트워크와 온-프레미스 사이트 간의 네트워크 트래픽을 암호화 toosend 만들어야 VPN 게이트웨이 가상 네트워크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-107">toosend encrypted network traffic between your Azure virtual network and your on-premises site, you must create a VPN gateway for your virtual network.</span></span>

<span data-ttu-id="a8b8d-108">하지만 각 가상 네트워크 VPN 게이트웨이 하나만 가질 수 있습니다, 여러 연결 toohello를 만들 수 있습니다 VPN 게이트웨이 동일한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-108">Each virtual network can have only one VPN gateway, however, you can create multiple connections toohello same VPN gateway.</span></span> <span data-ttu-id="a8b8d-109">한 가지 예로 다중 사이트 연결 구성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-109">An example of this is a Multi-Site connection configuration.</span></span> <span data-ttu-id="a8b8d-110">여러 연결 toohello를 만들 때 동일한 VPN 게이트웨이에 지점-사이트 Vpn, hello 게이트웨이에 사용할 수 있는 공유 hello 대역폭을 비롯 한 모든 VPN 터널 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-110">When you create multiple connections toohello same VPN gateway, all VPN tunnels, including Point-to-Site VPNs, share hello bandwidth that is available for hello gateway.</span></span>

### <span data-ttu-id="a8b8d-111"><a name="whatis"></a>가상 네트워크 게이트웨이란?</span><span class="sxs-lookup"><span data-stu-id="a8b8d-111"><a name="whatis"></a>What is a virtual network gateway?</span></span>

<span data-ttu-id="a8b8d-112">가상 네트워크 게이트웨이 두 이루어져 또는 더 많은 가상 컴퓨터 배포 hello GatewaySubnet 이라는 tooa 특정 서브넷.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-112">A virtual network gateway is composed of two or more virtual machines that are deployed tooa specific subnet called hello GatewaySubnet.</span></span> <span data-ttu-id="a8b8d-113">GatewaySubnet hello 가상 네트워크 게이트웨이 만들 때 함께 생성 되는 hello에 있는 Vm 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-113">hello VMs that are located in hello GatewaySubnet are created when you create hello virtual network gateway.</span></span> <span data-ttu-id="a8b8d-114">가상 네트워크 게이트웨이 Vm은 구성 된 toocontain 라우팅 테이블 및 특정 toohello 게이트웨이 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-114">Virtual network gateway VMs are configured toocontain routing tables and gateway services specific toohello gateway.</span></span> <span data-ttu-id="a8b8d-115">Hello hello 가상 네트워크 게이트웨이의 일부인 가상 컴퓨터를 직접 구성할 수 없습니다 및 추가 리소스 toohello GatewaySubnet 배포 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-115">You can't directly configure hello VMs that are part of hello virtual network gateway and you should never deploy additional resources toohello GatewaySubnet.</span></span>

<span data-ttu-id="a8b8d-116">특정 유형의 트래픽을 암호화 하는 가상 네트워크 게이트웨이 만듭니다 hello 게이트웨이 유형 'Vpn'를 사용 하 여 가상 네트워크 게이트웨이 만들 때 VPN 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-116">When you create a virtual network gateway using hello gateway type 'Vpn', it creates a specific type of virtual network gateway that encrypts traffic; a VPN gateway.</span></span> <span data-ttu-id="a8b8d-117">VPN 게이트웨이 too45 분 toocreate 차지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-117">A VPN gateway can take up too45 minutes toocreate.</span></span> <span data-ttu-id="a8b8d-118">Hello VPN 게이트웨이에 대 한 hello Vm 배포 toohello GatewaySubnet 되는 중 이므로 이며 지정한 hello 설정으로 구성 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-118">This is because hello VMs for hello VPN gateway are being deployed toohello GatewaySubnet and configured with hello settings that you specified.</span></span> <span data-ttu-id="a8b8d-119">선택한 게이트웨이 SKU hello Vm은 얼마나 강력한 hello를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-119">hello Gateway SKU that you select determines how powerful hello VMs are.</span></span>

## <span data-ttu-id="a8b8d-120"><a name="gwsku"></a>게이트웨이 SKU</span><span class="sxs-lookup"><span data-stu-id="a8b8d-120"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

## <span data-ttu-id="a8b8d-121"><a name="configuring"></a>VPN Gateway 구성</span><span class="sxs-lookup"><span data-stu-id="a8b8d-121"><a name="configuring"></a>Configuring a VPN Gateway</span></span>

<span data-ttu-id="a8b8d-122">VPN Gateway 연결은 특정 설정으로 구성된 여러 리소스에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-122">A VPN gateway connection relies on multiple resources that are configured with specific settings.</span></span> <span data-ttu-id="a8b8d-123">일부 경우에는 특정 순서로 구성 해야 하지만 대부분의 hello 리소스 별도로 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-123">Most of hello resources can be configured separately, although they must be configured in a certain order in some cases.</span></span>

### <span data-ttu-id="a8b8d-124"><a name="settings"></a>설정</span><span class="sxs-lookup"><span data-stu-id="a8b8d-124"><a name="settings"></a>Settings</span></span>

<span data-ttu-id="a8b8d-125">hello 각 리소스에 대해 선택한 설정이 중요 한 toocreating 성공적으로 연결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-125">hello settings that you chose for each resource are critical toocreating a successful connection.</span></span> <span data-ttu-id="a8b8d-126">VPN Gateway의 개별 리소스 및 설정에 대한 정보는 [VPN Gateway 설정 정보](vpn-gateway-about-vpn-gateway-settings.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-126">For information about individual resources and settings for VPN Gateway, see [About VPN Gateway settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span> <span data-ttu-id="a8b8d-127">hello 문서 정보 toohelp을 게이트웨이 유형, VPN 유형, 연결 유형, 게이트웨이 서브넷, 로컬 네트워크 게이트웨이 및 기타 다양 한 리소스 설정을 tooconsider를 취소할 수 있음을 이해 하 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-127">hello article contains information toohelp you understand gateway types, VPN types, connection types, gateway subnets, local network gateways, and various other resource settings that you may want tooconsider.</span></span>

### <span data-ttu-id="a8b8d-128"><a name="tools"></a>배포 도구</span><span class="sxs-lookup"><span data-stu-id="a8b8d-128"><a name="tools"></a>Deployment tools</span></span>

<span data-ttu-id="a8b8d-129">만들고 Azure 포털 hello 등과 같은 하나의 구성 도구를 사용 하 여 리소스를 구성 하는 아웃 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-129">You can start out creating and configuring resources using one configuration tool, such as hello Azure portal.</span></span> <span data-ttu-id="a8b8d-130">나중에 PowerShell, tooconfigure 추가 리소스 등 tooswitch tooanother 도구를 결정 하거나 해당 하는 경우 기존 리소스를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-130">You can later decide tooswitch tooanother tool, such as PowerShell, tooconfigure additional resources, or modify existing resources when applicable.</span></span> <span data-ttu-id="a8b8d-131">현재 hello Azure 포털에서에서 모든 리소스 및 리소스 설정을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-131">Currently, you can't configure every resource and resource setting in hello Azure portal.</span></span> <span data-ttu-id="a8b8d-132">각 연결 토폴로지에 대 한 hello 아티클의 hello 지침에는 특정 구성 도구가 필요한 경우를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-132">hello instructions in hello articles for each connection topology specify when a specific configuration tool is needed.</span></span> 

### <span data-ttu-id="a8b8d-133"><a name="models"></a>배포 모델</span><span class="sxs-lookup"><span data-stu-id="a8b8d-133"><a name="models"></a>Deployment model</span></span>

<span data-ttu-id="a8b8d-134">VPN 게이트웨이 구성할 때 수행 하는 hello 단계에 따라 다릅니다 hello 배포 모델을 사용 하 여 toocreate 가상 네트워크.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-134">When you configure a VPN gateway, hello steps you take depend on hello deployment model that you used toocreate your virtual network.</span></span> <span data-ttu-id="a8b8d-135">예를 들어 VNet을 만들 경우 hello 클래식 배포 모델을 사용 하 여 hello 지침을 사용 하 고 hello 클래식 배포에 대 한 지침 toocreate 모델 VPN 게이트웨이 설정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-135">For example, if you created your VNet using hello classic deployment model, you use hello guidelines and instructions for hello classic deployment model toocreate and configure your VPN gateway settings.</span></span> <span data-ttu-id="a8b8d-136">배포 모델에 대한 자세한 내용은 [Resource Manager 배포 및 클래식 배포 모델 이해](../azure-resource-manager/resource-manager-deployment-model.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-136">For more information about deployment models, see [Understanding Resource Manager and classic deployment models](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <span data-ttu-id="a8b8d-137"><a name="diagrams"></a>연결 토폴로지 다이어그램</span><span class="sxs-lookup"><span data-stu-id="a8b8d-137"><a name="diagrams"></a>Connection topology diagrams</span></span>

<span data-ttu-id="a8b8d-138">것이 중요 한 tooknow VPN 게이트웨이 연결에 사용할 수 있는 다른 여러 구성을 지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-138">It's important tooknow that there are different configurations available for VPN gateway connections.</span></span> <span data-ttu-id="a8b8d-139">필요에 맞는 최적의 구성을 toodetermine가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-139">You need toodetermine which configuration best fits your needs.</span></span> <span data-ttu-id="a8b8d-140">Hello 섹션 아래에서 VPN 게이트웨이 연결을 수행 하는 hello에 대 한 정보 및 토폴로지 다이어그램을 볼 수 있습니다: 다음 섹션 hello 나열 하는 테이블을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-140">In hello sections below, you can view information and topology diagrams about hello following VPN gateway connections: hello following sections contain tables which list:</span></span>

* <span data-ttu-id="a8b8d-141">사용 가능한 배포 모델</span><span class="sxs-lookup"><span data-stu-id="a8b8d-141">Available deployment model</span></span>
* <span data-ttu-id="a8b8d-142">사용 가능한 구성 도구</span><span class="sxs-lookup"><span data-stu-id="a8b8d-142">Available configuration tools</span></span>
* <span data-ttu-id="a8b8d-143">연결 된 링크를 직접 tooan 문서, 사용 가능한 경우</span><span class="sxs-lookup"><span data-stu-id="a8b8d-143">Links that take you directly tooan article, if available</span></span>

<span data-ttu-id="a8b8d-144">사용 하 여 hello 다이어그램 및 설명이 toohelp 요구 사항 hello 연결 토폴로지 toomatch를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-144">Use hello diagrams and descriptions toohelp select hello connection topology toomatch your requirements.</span></span> <span data-ttu-id="a8b8d-145">hello 다이어그램에 표시 hello 주 초기 토폴로지 이지만 가능한 toobuild 지침으로 hello 다이어그램을 사용 하 여 보다 복잡 한 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-145">hello diagrams show hello main baseline topologies, but it's possible toobuild more complex configurations using hello diagrams as a guideline.</span></span>

## <span data-ttu-id="a8b8d-146"><a name="s2smulti"></a>사이트 간 및 다중 사이트(IPsec/IKE VPN 터널)</span><span class="sxs-lookup"><span data-stu-id="a8b8d-146"><a name="s2smulti"></a>Site-to-Site and Multi-Site (IPsec/IKE VPN tunnel)</span></span>

### <span data-ttu-id="a8b8d-147"><a name="S2S"></a>사이트 간</span><span class="sxs-lookup"><span data-stu-id="a8b8d-147"><a name="S2S"></a>Site-to-Site</span></span>

<span data-ttu-id="a8b8d-148">S2S(사이트 간) VPN Gateway 연결은 IPsec/IKE(IKEv1 또는 IKEv2) VPN 터널을 통한 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-148">A Site-to-Site (S2S) VPN gateway connection is a connection over IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="a8b8d-149">S2S 연결에는 VPN 장치에 있는 온-프레미스 NAT 내부의 및 공용 IP 주소 할당 tooit 필요</span><span class="sxs-lookup"><span data-stu-id="a8b8d-149">A S2S connection requires a VPN device located on-premises that has a public IP address assigned tooit and is not located behind a NAT.</span></span> <span data-ttu-id="a8b8d-150">S2S 연결은 프레미스 간 및 하이브리드 구성에 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-150">S2S connections can be used for cross-premises and hybrid configurations.</span></span>   

![Azure VPN Gateway 사이트 간 연결 예제](./media/vpn-gateway-about-vpngateways/vpngateway-site-to-site-connection-diagram.png)

### <span data-ttu-id="a8b8d-152"><a name="Multi"></a>다중 사이트</span><span class="sxs-lookup"><span data-stu-id="a8b8d-152"><a name="Multi"></a>Multi-Site</span></span>

<span data-ttu-id="a8b8d-153">이러한 종류의 연결에는 hello 사이트 간 연결의 변형입니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-153">This type of connection is a variation of hello Site-to-Site connection.</span></span> <span data-ttu-id="a8b8d-154">가상 네트워크 게이트웨이에서 둘 이상의 VPN 연결을 만드는, toomultiple를 연결 하는 일반적으로 온-프레미스 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-154">You create more than one VPN connection from your virtual network gateway, typically connecting toomultiple on-premises sites.</span></span> <span data-ttu-id="a8b8d-155">여러 연결을 사용하는 경우 경로 기반 VPN 유형(클래식 VNet을 사용하는 경우 동적 게이트웨이)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-155">When working with multiple connections, you must use a RouteBased VPN type (known as a dynamic gateway when working with classic VNets).</span></span> <span data-ttu-id="a8b8d-156">각 가상 네트워크에서 하나의 VPN 게이트웨이 하나만 사용할 수 있습니다, 때문에 hello 게이트웨이 통해 모든 연결 hello 사용 가능한 대역폭을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-156">Because each virtual network can only have one VPN gateway, all connections through hello gateway share hello available bandwidth.</span></span> <span data-ttu-id="a8b8d-157">이는 "다중 사이트" 연결이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-157">This is often called a "multi-site" connection.</span></span>

![Azure VPN Gateway 다중 사이트 연결 예제](./media/vpn-gateway-about-vpngateways/vpngateway-multisite-connection-diagram.png)

### <a name="deployment-models-and-methods-for-site-to-site-and-multi-site"></a><span data-ttu-id="a8b8d-159">사이트 간 및 다중 사이트의 배포 모델 및 메서드</span><span class="sxs-lookup"><span data-stu-id="a8b8d-159">Deployment models and methods for Site-to-Site and Multi-Site</span></span>

[!INCLUDE [vpn-gateway-table-site-to-site](../../includes/vpn-gateway-table-site-to-site-include.md)]

## <span data-ttu-id="a8b8d-160"><a name="P2S"></a>지점 및 사이트 간(SSTP를 통한 VPN)</span><span class="sxs-lookup"><span data-stu-id="a8b8d-160"><a name="P2S"></a>Point-to-Site (VPN over SSTP)</span></span>

<span data-ttu-id="a8b8d-161">지점 및 사이트 간 (P2S) VPN 게이트웨이 사용 하면 개별 클라이언트 컴퓨터에서 보안 연결 tooyour 가상 네트워크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-161">A Point-to-Site (P2S) VPN gateway lets you create a secure connection tooyour virtual network from an individual client computer.</span></span> <span data-ttu-id="a8b8d-162">지점-사이트 VPN 연결은 tooconnect tooyour 가정 이나 회의에서 통신 하는 경우 등의 원격 위치에서 VNet을 원하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-162">Point-to-Site VPN connections are useful when you want tooconnect tooyour VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="a8b8d-163">P2S VPN tooconnect tooa VNet을 필요로 하는 몇 가지 클라이언트만 있으면 사이트 간 VPN 대신 유용한 솔루션 toouse 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-163">A P2S VPN is also a useful solution toouse instead of a Site-to-Site VPN when you have only a few clients that need tooconnect tooa VNet.</span></span> 

<span data-ttu-id="a8b8d-164">S2S 연결과 달리 P2S 연결은 온-프레미스 공용 IP 주소 또는 VPN 장치가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-164">Unlike S2S connections, P2S connections do not require an on-premises public-facing IP address or a VPN device.</span></span> <span data-ttu-id="a8b8d-165">P2S 연결을 통해 S2S 연결 사용 하 여 호환 되는 두 연결에 대 한 구성 요구 사항 hello 모든으로 동일한 VPN 게이트웨이에 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-165">P2S connections can be used with S2S connections through hello same VPN gateway, as long as all hello configuration requirements for both connections are compatible.</span></span>

<span data-ttu-id="a8b8d-166">P2S 사용 하 여 hello 소켓 SSTP Secure Tunneling Protocol (), SSL 기반 VPN 프로토콜인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-166">P2S uses hello Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="a8b8d-167">Hello 클라이언트 컴퓨터에서 시작 하 여 P2S VPN을 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-167">A P2S VPN connection is established by starting it from hello client computer.</span></span>

![Azure VPN Gateway 지점 및 사이트 연결 예제](./media/vpn-gateway-about-vpngateways/vpngateway-point-to-site-connection-diagram.png)

### <a name="deployment-models-and-methods-for-point-to-site"></a><span data-ttu-id="a8b8d-169">지점 및 사이트에 대한 배포 모델 및 메서드</span><span class="sxs-lookup"><span data-stu-id="a8b8d-169">Deployment models and methods for Point-to-Site</span></span>

[!INCLUDE [vpn-gateway-table-point-to-site](../../includes/vpn-gateway-table-point-to-site-include.md)]

## <span data-ttu-id="a8b8d-170"><a name="V2V"></a>VNet 간 연결(IPsec/IKE VPN 터널)</span><span class="sxs-lookup"><span data-stu-id="a8b8d-170"><a name="V2V"></a>VNet-to-VNet connections (IPsec/IKE VPN tunnel)</span></span>

<span data-ttu-id="a8b8d-171">가상 네트워크 tooanother 가상 네트워크 (VNet 대 VNet) 연결 하는 유사한 tooconnecting VNet tooan 온-프레미스 사이트 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-171">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="a8b8d-172">두 연결 유형에서는 VPN 게이트웨이 tooprovide IPsec/IKE를 사용 하 여 보안 터널을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-172">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="a8b8d-173">VNet 간 통신을 다중 사이트 연결 구성과 통합할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-173">You can even combine VNet-to-VNet communication with multi-site connection configurations.</span></span> <span data-ttu-id="a8b8d-174">이렇게 하면 프레미스 간 연결을 가상 네트워크 간 연결과 결합하는 네트워크 토폴로지를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-174">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity.</span></span>

<span data-ttu-id="a8b8d-175">hello Vnet에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-175">hello VNets you connect can be:</span></span>

* <span data-ttu-id="a8b8d-176">hello에 같거나 다른 지역</span><span class="sxs-lookup"><span data-stu-id="a8b8d-176">in hello same or different regions</span></span>
* <span data-ttu-id="a8b8d-177">hello에 같거나 다른 데이터 집합 구독</span><span class="sxs-lookup"><span data-stu-id="a8b8d-177">in hello same or different subscriptions</span></span> 
* <span data-ttu-id="a8b8d-178">hello에 같거나 다른 배포 모델</span><span class="sxs-lookup"><span data-stu-id="a8b8d-178">in hello same or different deployment models</span></span>

![Azure VPN 게이트웨이 VNet tooVNet 연결 예](./media/vpn-gateway-about-vpngateways/vpngateway-vnet-to-vnet-connection-diagram.png)

### <a name="connections-between-deployment-models"></a><span data-ttu-id="a8b8d-180">배포 모델 간의 연결</span><span class="sxs-lookup"><span data-stu-id="a8b8d-180">Connections between deployment models</span></span>

<span data-ttu-id="a8b8d-181">Azure에는 현재 클래식 및 Resource Manager 등 두 개의 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-181">Azure currently has two deployment models: classic and Resource Manager.</span></span> <span data-ttu-id="a8b8d-182">일정 기간 동안 Azure를 사용한 경우 Azure VM 및 인스턴스 역할이 클래식 VNet에서 실행되고 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-182">If you have been using Azure for some time, you probably have Azure VMs and instance roles running in a classic VNet.</span></span> <span data-ttu-id="a8b8d-183">이후의 VM 및 역할 인스턴스는 Resource Manager에서 만들 VNet에서 실행되고 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-183">Your newer VMs and role instances may be running in a VNet created in Resource Manager.</span></span> <span data-ttu-id="a8b8d-184">다른 리소스와 직접 하나의 VNet toocommunicate에 hello Vnet tooallow 사이의 연결 hello 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-184">You can create a connection between hello VNets tooallow hello resources in one VNet toocommunicate directly with resources in another.</span></span>

### <a name="vnet-peering"></a><span data-ttu-id="a8b8d-185">VNet 피어링</span><span class="sxs-lookup"><span data-stu-id="a8b8d-185">VNet peering</span></span>

<span data-ttu-id="a8b8d-186">가상 네트워크는 특정 요구 사항을 충족으로 수 toouse VNet toocreate 해당 연결을 피어 링을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-186">You may be able toouse VNet peering toocreate your connection, as long as your virtual network meets certain requirements.</span></span> <span data-ttu-id="a8b8d-187">VNet 피어링은 가상 네트워크 게이트웨이를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-187">VNet peering does not use a virtual network gateway.</span></span> <span data-ttu-id="a8b8d-188">자세한 내용은 [VNet 피어링](../virtual-network/virtual-network-peering-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-188">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

### <a name="deployment-models-and-methods-for-vnet-to-vnet"></a><span data-ttu-id="a8b8d-189">VNet 간 배포 모델 및 메서드</span><span class="sxs-lookup"><span data-stu-id="a8b8d-189">Deployment models and methods for VNet-to-VNet</span></span>

[!INCLUDE [vpn-gateway-table-vnet-to-vnet](../../includes/vpn-gateway-table-vnet-to-vnet-include.md)]

## <span data-ttu-id="a8b8d-190"><a name="ExpressRoute"></a>ExpressRoute(전용 개인 연결)</span><span class="sxs-lookup"><span data-stu-id="a8b8d-190"><a name="ExpressRoute"></a>ExpressRoute (dedicated private connection)</span></span>

<span data-ttu-id="a8b8d-191">Microsoft Azure ExpressRoute를 사용 하면 연결 공급자를 통해 지원 되는 전용된 개인 연결을 통해 hello Microsoft 클라우드로 온-프레미스 네트워크를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-191">Microsoft Azure ExpressRoute lets you extend your on-premises networks into hello Microsoft cloud over a dedicated private connection facilitated by a connectivity provider.</span></span> <span data-ttu-id="a8b8d-192">ExpressRoute를 사용 Microsoft Azure, Office 365, CRM Online과 같은 연결 tooMicrosoft 클라우드 서비스를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-192">With ExpressRoute, you can establish connections tooMicrosoft cloud services, such as Microsoft Azure, Office 365, and CRM Online.</span></span> <span data-ttu-id="a8b8d-193">공동 배치 시설에서 연결 공급자를 통해 임의의(IP VPN) 네트워크, 지점간 이더넷 네트워크 또는 가상 간 연결에서 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-193">Connectivity can be from an any-to-any (IP VPN) network, a point-to-point Ethernet network, or a virtual cross-connection through a connectivity provider at a co-location facility.</span></span>

<span data-ttu-id="a8b8d-194">ExpressRoute 연결은 hello를 통해 이동 하지 않도록 공용 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-194">ExpressRoute connections do not go over hello public Internet.</span></span> <span data-ttu-id="a8b8d-195">이렇게 하면 express 경로 연결 toooffer 안정성, 빨라진 속도, 낮은 대기 시간, 및 일반 연결 보다 보안성이 높으며 더 많은 hello 인터넷을 통해.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-195">This allows ExpressRoute connections toooffer more reliability, faster speeds, lower latencies, and higher security than typical connections over hello Internet.</span></span>

<span data-ttu-id="a8b8d-196">ExpressRoute 연결은 필수 구성의 일부분으로 가상 네트워크 게이트웨이를 사용하지만 VPN Gateway는 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-196">An ExpressRoute connection does not use a VPN gateway, although it does use a virtual network gateway as part of its required configuration.</span></span> <span data-ttu-id="a8b8d-197">ExpressRoute 연결에서 hello 가상 네트워크 게이트웨이 'Vpn' 대신 'ExpressRoute' hello 게이트웨이 유형으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-197">In an ExpressRoute connection, hello virtual network gateway is configured with hello gateway type 'ExpressRoute', rather than 'Vpn'.</span></span> <span data-ttu-id="a8b8d-198">ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 기술 개요](../expressroute/expressroute-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-198">For more information about ExpressRoute, see hello [ExpressRoute technical overview](../expressroute/expressroute-introduction.md).</span></span>

## <span data-ttu-id="a8b8d-199"><a name="coexisting"></a>사이트 간 및 ExpressRoute 공존 연결</span><span class="sxs-lookup"><span data-stu-id="a8b8d-199"><a name="coexisting"></a>Site-to-Site and ExpressRoute coexisting connections</span></span>

<span data-ttu-id="a8b8d-200">ExpressRoute는 WAN에서 직접는 전용된 연결 (하지 않고 공용 인터넷 hello) tooMicrosoft Azure를 포함 한 서비스를 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-200">ExpressRoute is a direct, dedicated connection from your WAN (not over hello public Internet) tooMicrosoft Services, including Azure.</span></span> <span data-ttu-id="a8b8d-201">사이트-사이트 VPN 트래픽의 hello를 통해 암호화 여행 공용 인터넷 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-201">Site-to-Site VPN traffic travels encrypted over hello public Internet.</span></span> <span data-ttu-id="a8b8d-202">되 고 수 tooconfigure 사이트 간 VPN 및 express 경로 연결 hello 동일한 가상 네트워크에 대해 여러 가지 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-202">Being able tooconfigure Site-to-Site VPN and ExpressRoute connections for hello same virtual network has several advantages.</span></span>

<span data-ttu-id="a8b8d-203">ExpressRoute를에 대 한 보안 장애 조치 경로와 사이트 간 VPN을 구성 하거나 네트워크의 일부가 아닌 하지만 ExpressRoute를 통해 연결 된 사이트 간 Vpn tooconnect toosites를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-203">You can configure a Site-to-Site VPN as a secure failover path for ExpressRoute, or use Site-to-Site VPNs tooconnect toosites that are not part of your network, but that are connected through ExpressRoute.</span></span> <span data-ttu-id="a8b8d-204">확인에 대 한 두 가상 네트워크 게이트웨이 hello 동일한 가상 네트워크, hello 게이트웨이 유형 'Vpn' 및 'ExpressRoute' hello 게이트웨이 유형을 사용 하 여 hello를 사용 하 여이 구성에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-204">Notice that this configuration requires two virtual network gateways for hello same virtual network, one using hello gateway type 'Vpn', and hello other using hello gateway type 'ExpressRoute'.</span></span>

![ExpressRoute 및 VPN Gateway 공존 연결 예제](./media/vpn-gateway-about-vpngateways/expressroute-vpngateway-coexisting-connections-diagram.png)

### <a name="deployment-models-and-methods-for-s2s-and-expressroute"></a><span data-ttu-id="a8b8d-206">S2S 및 ExpressRoute에 대한 배포 모델 및 메서드</span><span class="sxs-lookup"><span data-stu-id="a8b8d-206">Deployment models and methods for S2S and ExpressRoute</span></span>

[!INCLUDE [vpn-gateway-table-coexist](../../includes/vpn-gateway-table-coexist-include.md)]

## <a name="pricing"></a><span data-ttu-id="a8b8d-207">가격</span><span class="sxs-lookup"><span data-stu-id="a8b8d-207">Pricing</span></span>

[!INCLUDE [vpn-gateway-about-pricing-include](../../includes/vpn-gateway-about-pricing-include.md)]

<span data-ttu-id="a8b8d-208">VPN Gateway용 게이트웨이 SKU에 대한 자세한 내용은 [게이트웨이 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-208">For more information about gateway SKUs for VPN Gateway, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <span data-ttu-id="a8b8d-209"><a name="faq"></a>FAQ</span><span class="sxs-lookup"><span data-stu-id="a8b8d-209"><a name="faq"></a>FAQ</span></span>

<span data-ttu-id="a8b8d-210">VPN 게이트웨이에 대 한 자주 묻는 질문에 대 한 참조 hello [VPN 게이트웨이 FAQ](vpn-gateway-vpn-faq.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-210">For frequently asked questions about VPN gateway, see hello [VPN Gateway FAQ](vpn-gateway-vpn-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8b8d-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a8b8d-211">Next steps</span></span>

- <span data-ttu-id="a8b8d-212">VPN Gateway 구성을 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-212">Plan your VPN gateway configuration.</span></span> <span data-ttu-id="a8b8d-213">[VPN Gateway 계획 및 설계](vpn-gateway-plan-design.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-213">See [VPN Gateway Planning and Design](vpn-gateway-plan-design.md).</span></span>
- <span data-ttu-id="a8b8d-214">보기 hello [VPN 게이트웨이 FAQ](vpn-gateway-vpn-faq.md) 추가 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-214">View hello [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) for additional information.</span></span>
- <span data-ttu-id="a8b8d-215">보기 hello [구독 및 서비스 제한](../azure-subscription-service-limits.md#networking-limits)합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-215">View hello [Subscription and service limits](../azure-subscription-service-limits.md#networking-limits).</span></span>
- <span data-ttu-id="a8b8d-216">일부 hello에 대 한 자세한 내용은 다른 키 [네트워킹 기능](../networking/networking-overview.md) Azure의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8b8d-216">Learn about some of hello other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>
