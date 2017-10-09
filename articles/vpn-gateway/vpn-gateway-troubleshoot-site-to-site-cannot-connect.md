---
title: "aaaTroubleshoot 연결할 수 없는 Azure 사이트 간 VPN 연결 | Microsoft Docs"
description: "자세한 내용은 어떻게 tootroubleshoot 사이트 간 VPN 연결 하는 갑자기 작동을 중단 하 고 다시 연결할 수 없습니다."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="527b0-103">문제 해결: Azure 사이트 간 VPN 연결에서 연결할 수 없고 작동이 중지됨</span><span class="sxs-lookup"><span data-stu-id="527b0-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="527b0-104">온-프레미스 네트워크와 Azure 가상 네트워크 간의 사이트 간 VPN 연결을 구성한 후 hello VPN 연결 갑자기 작동을 중지 하 고 다시 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, hello VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="527b0-105">이 문서에서는 문제 해결 단계 toohelp이이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="527b0-106">문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="527b0-106">Troubleshooting steps</span></span>

<span data-ttu-id="527b0-107">tooresolve hello 문제를 먼저 시도 합니다. 너무[재설정 hello Azure VPN 게이트웨이](vpn-gateway-resetgw-classic.md) hello 터널 hello 온-프레미스 VPN 장치를 다시 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-107">tooresolve hello problem, first try too[reset hello Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset hello tunnel from hello on-premises VPN device.</span></span> <span data-ttu-id="527b0-108">Hello 문제가 계속 되 면 hello 문제 중 해당 단계 tooidentify hello 인해를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-108">If hello problem persists, follow these steps tooidentify hello cause of hello problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="527b0-109">필수 조건 단계</span><span class="sxs-lookup"><span data-stu-id="527b0-109">Prerequisite step</span></span>

<span data-ttu-id="527b0-110">Hello hello Azure VPN 게이트웨이 유형을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-110">Check hello type of hello Azure VPN gateway.</span></span>

1. <span data-ttu-id="527b0-111">Toohello 이동 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-111">Go toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="527b0-112">Hello 확인 **개요** hello 형식 정보에 대 한 hello VPN 게이트웨이의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-112">Check hello **Overview** page of hello VPN gateway for hello type information.</span></span>
    
    ![Hello 게이트웨이 개요](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="527b0-114">1단계.</span><span class="sxs-lookup"><span data-stu-id="527b0-114">Step 1.</span></span> <span data-ttu-id="527b0-115">Hello 온-프레미스 VPN 장치의 유효성을 검사 하는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="527b0-115">Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="527b0-116">[확인된 VPN 장치 및 운영 체제 버전](vpn-gateway-about-vpn-devices.md#devicetable)을 사용 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="527b0-117">유효성이 검사 된 VPN 장치 hello 장치가 아닌 경우 호환성 문제가 있는 경우 toocontact hello 장치 제조업체 toosee를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-117">If hello device is not a validated VPN device, you might have toocontact hello device manufacturer toosee if there is a compatibility issue.</span></span>

2. <span data-ttu-id="527b0-118">해당 hello VPN 장치가 올바르게 구성 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-118">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="527b0-119">자세한 내용은 [장치 구성 예제 편집](/vpn-gateway-about-vpn-devices.md#editing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="527b0-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-hello-shared-key"></a><span data-ttu-id="527b0-120">2단계.</span><span class="sxs-lookup"><span data-stu-id="527b0-120">Step 2.</span></span> <span data-ttu-id="527b0-121">Hello 공유 키를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-121">Verify hello shared key</span></span>

<span data-ttu-id="527b0-122">Hello hello 온-프레미스 VPN 장치 toohello Azure 가상 네트워크 VPN toomake hello 키와 일치 하는지에 대 한 공유 키를 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-122">Compare hello shared key for hello on-premises VPN device toohello Azure Virtual Network VPN toomake sure that hello keys match.</span></span> 

<span data-ttu-id="527b0-123">hello tooview hello Azure VPN 연결에 대 한 공유 키를 사용 하 여 hello 메서드를 다음 중 하나:</span><span class="sxs-lookup"><span data-stu-id="527b0-123">tooview hello shared key for hello Azure VPN connection, use one of hello following methods:</span></span>

<span data-ttu-id="527b0-124">**Azure 포털**</span><span class="sxs-lookup"><span data-stu-id="527b0-124">**Azure portal**</span></span>

1. <span data-ttu-id="527b0-125">만든 toohello VPN 게이트웨이 사이트 간 연결을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-125">Go toohello VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="527b0-126">Hello에 **설정** 섹션에서 클릭 **공유 키**합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-126">In hello **Settings** section, click **Shared key**.</span></span>
    
    ![공유 키](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="527b0-128">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="527b0-128">**Azure PowerShell**</span></span>

<span data-ttu-id="527b0-129">Hello Azure 리소스 관리자 배포 모델:</span><span class="sxs-lookup"><span data-stu-id="527b0-129">For hello Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="527b0-130">Hello 클래식 배포 모델:</span><span class="sxs-lookup"><span data-stu-id="527b0-130">For hello classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a><span data-ttu-id="527b0-131">3단계.</span><span class="sxs-lookup"><span data-stu-id="527b0-131">Step 3.</span></span> <span data-ttu-id="527b0-132">Hello VPN 피어 Ip 확인</span><span class="sxs-lookup"><span data-stu-id="527b0-132">Verify hello VPN peer IPs</span></span>

-   <span data-ttu-id="527b0-133">hello에 IP 정의 hello **로컬 네트워크 게이트웨이** 개체 Azure의 hello 온-프레미스 장치 IP와 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-133">hello IP definition in hello **Local Network Gateway** object in Azure should match hello on-premises device IP.</span></span>
-   <span data-ttu-id="527b0-134">hello Azure 게이트웨이 IP 정의 hello에 설정 된 온-프레미스 장치에는 hello Azure 게이트웨이 IP와 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-134">hello Azure gateway IP definition that is set on hello on-premises device should match hello Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a><span data-ttu-id="527b0-135">4단계.</span><span class="sxs-lookup"><span data-stu-id="527b0-135">Step 4.</span></span> <span data-ttu-id="527b0-136">Hello 게이트웨이 서브넷에 Nsg 및 UDR 확인</span><span class="sxs-lookup"><span data-stu-id="527b0-136">Check UDR and NSGs on hello gateway subnet</span></span>

<span data-ttu-id="527b0-137">에 대 한 확인 하 고 hello 게이트웨이 서브넷에 라우팅 사용자 정의 (UDR) 또는 (Nsg) 네트워크 보안 그룹을 제거 하 고 hello 결과 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on hello gateway subnet, and then test hello result.</span></span> <span data-ttu-id="527b0-138">Hello 문제가 해결 되 면 hello 설정을 적용 UDR 또는 NSG의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-138">If hello problem is resolved, validate hello settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="527b0-139">5단계.</span><span class="sxs-lookup"><span data-stu-id="527b0-139">Step 5.</span></span> <span data-ttu-id="527b0-140">Hello 온-프레미스 VPN 장치 외부 인터페이스 주소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-140">Check hello on-premises VPN device external interface address</span></span>

- <span data-ttu-id="527b0-141">Hello hello VPN 장치의 인터넷 연결 IP 주소는 hello에 포함 되어 있으면 **로컬 네트워크** 정의 Azure에서 산발적 연결 끊김 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-141">If hello Internet-facing IP address of hello VPN device is included in hello **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="527b0-142">hello 장치 외부 인터페이스 해야 hello 인터넷에서 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-142">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="527b0-143">네트워크 주소 변환 또는 인터넷 hello 및 hello 장치 사이 방화벽이 없습니다 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-143">There should be no network address translation or firewall between hello Internet and hello device.</span></span>
- <span data-ttu-id="527b0-144">tooconfigure 방화벽 클러스터링 toohave 가상 IP hello 클러스터를 중단 하 고 tooa 공용 인터페이스는 hello 게이트웨이 수와 상호 작용할 직접 hello VPN 어플라이언스를 노출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-144">tooconfigure firewall clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="527b0-145">6단계.</span><span class="sxs-lookup"><span data-stu-id="527b0-145">Step 6.</span></span> <span data-ttu-id="527b0-146">Hello 서브넷 정확히 일치 하는지 확인 하십시오 (정책 기반 Azure 게이트웨이)</span><span class="sxs-lookup"><span data-stu-id="527b0-146">Verify that hello subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="527b0-147">Hello 서브넷 hello Azure 가상 네트워크와 Azure 가상 네트워크 hello에 대 한 온-프레미스 정의 간에 정확히 일치 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-147">Verify that hello subnets match exactly between hello Azure virtual network and on-premises definitions for hello Azure virtual network.</span></span>
-   <span data-ttu-id="527b0-148">Hello 서브넷 hello 간에 정확히 일치 하는지 확인 **로컬 네트워크 게이트웨이** 및 온-프레미스 hello 온-프레미스 네트워크에 대 한 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-148">Verify that hello subnets match exactly between hello **Local Network Gateway** and on-premises definitions for hello on-premises network.</span></span>

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a><span data-ttu-id="527b0-149">7단계.</span><span class="sxs-lookup"><span data-stu-id="527b0-149">Step 7.</span></span> <span data-ttu-id="527b0-150">Hello Azure 게이트웨이 상태 프로브를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-150">Verify hello Azure gateway health probe</span></span>

1. <span data-ttu-id="527b0-151">Toohello 이동 [상태 프로브](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe)합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-151">Go toohello [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="527b0-152">Hello 인증서 경고를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-152">Click through hello certificate warning.</span></span>
3. <span data-ttu-id="527b0-153">응답을 수신 하는 경우 hello VPN 게이트웨이 정상인 상태로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-153">If you receive a response, hello VPN gateway is considered healthy.</span></span> <span data-ttu-id="527b0-154">응답을 수신 하지 않는 hello 게이트웨이 정상 수 없거나 hello 게이트웨이 서브넷에 NSG hello 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-154">If you don't receive a response, hello gateway might not be healthy or an NSG on hello gateway subnet is causing hello problem.</span></span> <span data-ttu-id="527b0-155">hello 텍스트 다음은 샘플 응답:</span><span class="sxs-lookup"><span data-stu-id="527b0-155">hello following text is a sample response:</span></span>

    <span data-ttu-id="527b0-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">기본 인스턴스: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span><span class="sxs-lookup"><span data-stu-id="527b0-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="527b0-157">8단계:</span><span class="sxs-lookup"><span data-stu-id="527b0-157">Step 8.</span></span> <span data-ttu-id="527b0-158">여부 hello 온-프레미스 VPN 장치에 hello 전달 완전 기능 사용 확인</span><span class="sxs-lookup"><span data-stu-id="527b0-158">Check whether hello on-premises VPN device has hello perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="527b0-159">hello 전달 완전 기능에는 연결을 끊는 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-159">hello perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="527b0-160">Hello VPN 장치 활성화 전달 완전 있으면 hello 기능을 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-160">If hello VPN device has perfect forward secrecy enabled, disable hello feature.</span></span> <span data-ttu-id="527b0-161">Hello VPN 게이트웨이 IPsec 정책을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="527b0-161">Then update hello VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="527b0-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="527b0-162">Next steps</span></span>

-   [<span data-ttu-id="527b0-163">사이트 간 연결 tooa 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="527b0-163">Configure a site-to-site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="527b0-164">사이트 간 VPN 연결에 대한 IPsec/IKE 정책 구성</span><span class="sxs-lookup"><span data-stu-id="527b0-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
