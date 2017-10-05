---
title: "Azure 사이트 간 VPN 연결에서 연결할 수 없는 문제 해결 | Microsoft Docs"
description: "갑자기 작동 중단되어 다시 연결할 수 없는 사이트 간 VPN 연결 문제를 해결하는 방법을 알아봅니다."
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
ms.openlocfilehash: e7a3da64895f0307e5d6c3563672205a2f93a7d2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="a1170-103">문제 해결: Azure 사이트 간 VPN 연결에서 연결할 수 없고 작동이 중지됨</span><span class="sxs-lookup"><span data-stu-id="a1170-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="a1170-104">온-프레미스 네트워크와 Azure Virtual Network 사이에 사이트 간 VPN 연결을 구성한 후 VPN 연결이 갑자기 작동을 중지하며, 이를 다시 연결할 수 없는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, the VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="a1170-105">이 문서에서는 이 문제를 해결하는 데 도움이 되는 문제 해결 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="a1170-106">문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="a1170-106">Troubleshooting steps</span></span>

<span data-ttu-id="a1170-107">이 문제를 해결하려면 먼저 [Azure VPN 게이트웨이를 다시 설정](vpn-gateway-resetgw-classic.md)한 다음 온-프레미스 VPN 장치에서 터널을 다시 설정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-107">To resolve the problem, first try to [reset the Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset the tunnel from the on-premises VPN device.</span></span> <span data-ttu-id="a1170-108">문제가 계속되면 다음 단계에 따라 문제의 원인을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-108">If the problem persists, follow these steps to identify the cause of the problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="a1170-109">필수 조건 단계</span><span class="sxs-lookup"><span data-stu-id="a1170-109">Prerequisite step</span></span>

<span data-ttu-id="a1170-110">Azure VPN 게이트웨이 유형을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-110">Check the type of the Azure VPN gateway.</span></span>

1. <span data-ttu-id="a1170-111">[Azure 포털](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-111">Go to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a1170-112">VPN 게이트웨이에 대한 **개요** 페이지에서 유형 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-112">Check the **Overview** page of the VPN gateway for the type information.</span></span>
    
    ![게이트웨이 개요](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-the-on-premises-vpn-device-is-validated"></a><span data-ttu-id="a1170-114">1단계.</span><span class="sxs-lookup"><span data-stu-id="a1170-114">Step 1.</span></span> <span data-ttu-id="a1170-115">온-프레미스 VPN 장치가 확인되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="a1170-115">Check whether the on-premises VPN device is validated</span></span>

1. <span data-ttu-id="a1170-116">[확인된 VPN 장치 및 운영 체제 버전](vpn-gateway-about-vpn-devices.md#devicetable)을 사용 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="a1170-117">확인된 VPN 장치가 아닌 경우 장치 제조업체에 호환성 문제가 있는지 문의해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-117">If the device is not a validated VPN device, you might have to contact the device manufacturer to see if there is a compatibility issue.</span></span>

2. <span data-ttu-id="a1170-118">VPN 장치가 올바르게 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-118">Make sure that the VPN device is correctly configured.</span></span> <span data-ttu-id="a1170-119">자세한 내용은 [장치 구성 예제 편집](/vpn-gateway-about-vpn-devices.md#editing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1170-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-the-shared-key"></a><span data-ttu-id="a1170-120">2단계.</span><span class="sxs-lookup"><span data-stu-id="a1170-120">Step 2.</span></span> <span data-ttu-id="a1170-121">공유 키 확인</span><span class="sxs-lookup"><span data-stu-id="a1170-121">Verify the shared key</span></span>

<span data-ttu-id="a1170-122">온-프레미스 VPN 장치와 Azure Virtual Network VPN의 공유 키를 비교하여 키가 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-122">Compare the shared key for the on-premises VPN device to the Azure Virtual Network VPN to make sure that the keys match.</span></span> 

<span data-ttu-id="a1170-123">Azure VPN 연결에 대한 공유 키를 보려면 다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-123">To view the shared key for the Azure VPN connection, use one of the following methods:</span></span>

<span data-ttu-id="a1170-124">**Azure 포털**</span><span class="sxs-lookup"><span data-stu-id="a1170-124">**Azure portal**</span></span>

1. <span data-ttu-id="a1170-125">만든 VPN 게이트웨이 사이트 간 연결로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-125">Go to the VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="a1170-126">**설정** 섹션에서 **공유 키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-126">In the **Settings** section, click **Shared key**.</span></span>
    
    ![공유 키](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="a1170-128">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="a1170-128">**Azure PowerShell**</span></span>

<span data-ttu-id="a1170-129">Azure Resource Manager 배포 모델:</span><span class="sxs-lookup"><span data-stu-id="a1170-129">For the Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="a1170-130">클래식 배포 모델:</span><span class="sxs-lookup"><span data-stu-id="a1170-130">For the classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-the-vpn-peer-ips"></a><span data-ttu-id="a1170-131">3단계.</span><span class="sxs-lookup"><span data-stu-id="a1170-131">Step 3.</span></span> <span data-ttu-id="a1170-132">VPN 피어 IP 확인</span><span class="sxs-lookup"><span data-stu-id="a1170-132">Verify the VPN peer IPs</span></span>

-   <span data-ttu-id="a1170-133">Azure의 **로컬 네트워크 게이트웨이** 개체에 있는 IP 정의가 온-프레미스 장치 IP와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-133">The IP definition in the **Local Network Gateway** object in Azure should match the on-premises device IP.</span></span>
-   <span data-ttu-id="a1170-134">온-프레미스 장치에 설정된 Azure 게이트웨이 IP 정의는 Azure 게이트웨이 IP와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-134">The Azure gateway IP definition that is set on the on-premises device should match the Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-the-gateway-subnet"></a><span data-ttu-id="a1170-135">4단계.</span><span class="sxs-lookup"><span data-stu-id="a1170-135">Step 4.</span></span> <span data-ttu-id="a1170-136">게이트웨이 서브넷에서 UDR 및 NSG 확인</span><span class="sxs-lookup"><span data-stu-id="a1170-136">Check UDR and NSGs on the gateway subnet</span></span>

<span data-ttu-id="a1170-137">게이트웨이 서브넷에서 UDR(사용자 정의 라우팅) 또는 NSG(네트워크 보안 그룹)를 확인하고 제거한 다음 결과를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on the gateway subnet, and then test the result.</span></span> <span data-ttu-id="a1170-138">문제가 해결되면 적용된 UDR 또는 NSG의 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-138">If the problem is resolved, validate the settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-the-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="a1170-139">5단계.</span><span class="sxs-lookup"><span data-stu-id="a1170-139">Step 5.</span></span> <span data-ttu-id="a1170-140">온-프레미스 VPN 장치 외부 인터페이스 주소 확인</span><span class="sxs-lookup"><span data-stu-id="a1170-140">Check the on-premises VPN device external interface address</span></span>

- <span data-ttu-id="a1170-141">VPN 장치의 인터넷 연결 IP 주소가 Azure의 **로컬 네트워크** 정의에 포함된 경우 이따금 연결 끊김이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-141">If the Internet-facing IP address of the VPN device is included in the **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="a1170-142">장치의 외부 인터페이스는 직접 인터넷에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-142">The device's external interface must be directly on the Internet.</span></span> <span data-ttu-id="a1170-143">인터넷과 장치 간에는 NAT(Network Address Translation) 또는 방화벽이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-143">There should be no network address translation or firewall between the Internet and the device.</span></span>
- <span data-ttu-id="a1170-144">가상 IP가 있도록 방화벽 클러스터링을 구성하려면 클러스터를 분해하고 VPN 어플라이언스를 직접 공용 인터페이스에 표시하여 게이트웨이가 연결할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-144">To configure firewall clustering to have a virtual IP, you must break the cluster and expose the VPN appliance directly to a public interface that the gateway can interface with.</span></span>

### <a name="step-6-verify-that-the-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="a1170-145">6단계.</span><span class="sxs-lookup"><span data-stu-id="a1170-145">Step 6.</span></span> <span data-ttu-id="a1170-146">서브넷이 정확하게 일치하는지 확인(Azure 정책 기반 게이트웨이)</span><span class="sxs-lookup"><span data-stu-id="a1170-146">Verify that the subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="a1170-147">Azure Virtual Network와 Azure Virtual Network에 대한 온-프레미스 정의 간에 서브넷이 정확하게 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-147">Verify that the subnets match exactly between the Azure virtual network and on-premises definitions for the Azure virtual network.</span></span>
-   <span data-ttu-id="a1170-148">**로컬 네트워크 게이트웨이**와 온-프레미스 네트워크에 대한 온-프레미스 정의 간에 서브넷이 정확하게 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-148">Verify that the subnets match exactly between the **Local Network Gateway** and on-premises definitions for the on-premises network.</span></span>

### <a name="step-7-verify-the-azure-gateway-health-probe"></a><span data-ttu-id="a1170-149">7단계.</span><span class="sxs-lookup"><span data-stu-id="a1170-149">Step 7.</span></span> <span data-ttu-id="a1170-150">Azure 게이트웨이 상태 프로브 확인</span><span class="sxs-lookup"><span data-stu-id="a1170-150">Verify the Azure gateway health probe</span></span>

1. <span data-ttu-id="a1170-151">[상태 프로브](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-151">Go to the [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="a1170-152">인증서 경고를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-152">Click through the certificate warning.</span></span>
3. <span data-ttu-id="a1170-153">응답이 수신되면 VPN 게이트웨이가 정상으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-153">If you receive a response, the VPN gateway is considered healthy.</span></span> <span data-ttu-id="a1170-154">응답을 수신하지 못하면 게이트웨이가 정상이 아니거나 게이트웨이 서브넷에 문제를 일으키는 NSG가 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-154">If you don't receive a response, the gateway might not be healthy or an NSG on the gateway subnet is causing the problem.</span></span> <span data-ttu-id="a1170-155">다음 텍스트는 샘플 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-155">The following text is a sample response:</span></span>

    <span data-ttu-id="a1170-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">기본 인스턴스: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span><span class="sxs-lookup"><span data-stu-id="a1170-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-the-on-premises-vpn-device-has-the-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="a1170-157">8단계:</span><span class="sxs-lookup"><span data-stu-id="a1170-157">Step 8.</span></span> <span data-ttu-id="a1170-158">온-프레미스 VPN 장치에 PFS(Perfect Forward Secrecy) 기능이 사용하도록 설정되어 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="a1170-158">Check whether the on-premises VPN device has the perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="a1170-159">PFS(Perfect Forward Secrecy) 기능은 연결 끊김 문제를 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-159">The perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="a1170-160">VPN 장치에 PFS(Perfect Forward Secrecy) 기능이 사용하도록 설정되어 있으면 이 기능을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-160">If the VPN device has perfect forward secrecy enabled, disable the feature.</span></span> <span data-ttu-id="a1170-161">그런 다음 VPN 게이트웨이 IPsec 정책을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a1170-161">Then update the VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1170-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a1170-162">Next steps</span></span>

-   [<span data-ttu-id="a1170-163">가상 네트워크에 대한 사이트 간 연결 구성</span><span class="sxs-lookup"><span data-stu-id="a1170-163">Configure a site-to-site connection to a virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="a1170-164">사이트 간 VPN 연결에 대한 IPsec/IKE 정책 구성</span><span class="sxs-lookup"><span data-stu-id="a1170-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
