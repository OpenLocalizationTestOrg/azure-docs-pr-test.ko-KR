---
title: "Azure 사이트 간 VPN 일시적 연결 끊김 문제 해결 | Microsoft Docs"
description: "사이트 간 VPN 연결이 자주 끊어지는 문제를 해결하는 방법을 알아봅니다."
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
ms.openlocfilehash: 99a790617baa65116bfba976cd9279627e8775f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="b357f-103">문제 해결: Azure 사이트 간 VPN 일시적 연결 끊김</span><span class="sxs-lookup"><span data-stu-id="b357f-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="b357f-104">새로운 또는 기존 Microsoft Azure 지점 및 사이트 간 VPN 연결이 안정적이지 않거나 연결이 자주 끊어지는 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-104">You might experience the problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="b357f-105">이 문서에서는 이 문제의 원인을 식별하여 문제를 해결하는 데 도움이 되는 문제 해결 단계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-105">This article provides troubleshoot steps to help you identify and resolve the cause of the problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="b357f-106">문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="b357f-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="b357f-107">필수 조건 단계</span><span class="sxs-lookup"><span data-stu-id="b357f-107">Prerequisite step</span></span>

<span data-ttu-id="b357f-108">Azure Virtual Network Gateway의 형식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-108">Check the type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="b357f-109">[Azure 포털](https://portal.azure.com)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-109">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b357f-110">Virtual Network Gateway의 **개요** 페이지에서 형식 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-110">Check the **Overview** page of the virtual network gateway for the type information.</span></span>
    
    ![게이트웨이 개요](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-the-on-premises-vpn-device-is-validated"></a><span data-ttu-id="b357f-112">1단계 온-프레미스 VPN 장치가 확인되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="b357f-112">Step 1 Check whether the on-premises VPN device is validated</span></span>

1. <span data-ttu-id="b357f-113">[확인된 VPN 장치 및 운영 체제 버전](vpn-gateway-about-vpn-devices.md#devicetable)을 사용 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="b357f-114">VPN 장치가 확인되지 않은 경우 장치 제조업체에 호환성 문제가 있는지 문의해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-114">If the VPN device is not validated, you may have to contact the device manufacturer to see if there is any compatibility issue.</span></span>
2. <span data-ttu-id="b357f-115">VPN 장치가 올바르게 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-115">Make sure that the VPN device is correctly configured.</span></span> <span data-ttu-id="b357f-116">자세한 내용은 [장치 구성 샘플 편집](vpn-gateway-about-vpn-devices.md#editing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b357f-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-the-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="b357f-117">2단계 보안 연결 설정 확인(정책 기반 Azure Virtual Network Gateway의 경우)</span><span class="sxs-lookup"><span data-stu-id="b357f-117">Step 2 Check the Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="b357f-118">Microsoft Azure의 **로컬 네트워크 게이트웨이** 정의에 있는 가상 네트워크, 서브넷 및 범위가 온-프레미스 VPN 장치의 구성과 같은지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-118">Make sure that the virtual network, subnets and, ranges in the **Local network gateway** definition in Microsoft Azure are same as the configuration on the on-premises VPN device.</span></span>
2. <span data-ttu-id="b357f-119">보안 연결 설정이 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-119">Verify that the Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="b357f-120">3단계 게이트웨이 서브넷에 대한 사용자 정의 경로 또는 네트워크 보안 그룹 확인</span><span class="sxs-lookup"><span data-stu-id="b357f-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="b357f-121">게이트웨이 서브넷의 사용자 정의 경로가 일부 트래픽은 제한하고 다른 트래픽은 허용하고 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-121">A user-defined route on the gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="b357f-122">이 경우 VPN 연결이 일부 트래픽에 대해서는 불안정하고 다른 트래픽에 대해서는 양호한 것으로 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-122">This makes it appear that the VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-the-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="b357f-123">4단계 “서브넷 쌍당 하나의 VPN 터널” 설정 확인(정책 기반 가상 네트워크 게이트웨이의 경우)</span><span class="sxs-lookup"><span data-stu-id="b357f-123">Step 4 Check the "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="b357f-124">온-프레미스 VPN 장치가 정책 기반 가상 네트워크 게이트웨이에 대해 **서브넷 쌍당 하나의 VPN 터널**을 가지도록 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-124">Make sure that the on-premises VPN device is set to have **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="b357f-125">5단계 보안 연결 제한 확인(정책 기반 가상 네트워크 게이트웨이의 경우)</span><span class="sxs-lookup"><span data-stu-id="b357f-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="b357f-126">정책 기반 가상 네트워크 게이트웨이에는 200개의 서브넷 보안 연결 쌍 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-126">The Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="b357f-127">Azure Virtual Network 서브넷 수를 로컬 서브넷 수로 곱한 값이 200보다 큰 경우 이따금 서브넷 연결이 끊어지는 현상이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-127">If the number of Azure virtual network subnets multiplied times by the number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="b357f-128">6단계 온-프레미스 VPN 장치 외부 인터페이스 주소 확인</span><span class="sxs-lookup"><span data-stu-id="b357f-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="b357f-129">VPN 장치의 인터넷 연결 IP 주소가 Azure의 **로컬 네트워크 게이트웨이** 정의에 포함된 경우 이따금 연결 끊김이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-129">If the Internet facing IP address of the VPN device is included in the **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="b357f-130">장치의 외부 인터페이스는 직접 인터넷에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-130">The device's external interface must be directly on the Internet.</span></span> <span data-ttu-id="b357f-131">인터넷과 장치 간에는 NAT(Network Address Translation) 또는 방화벽이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-131">There should be no Network Address Translation (NAT) or firewall between the Internet and the device.</span></span>
-  <span data-ttu-id="b357f-132">가상 IP가 있도록 방화벽 클러스터링을 구성하는 경우 클러스터를 분해하고 VPN 어플라이언스를 직접 공용 게이트웨이에 표시하여 게이트웨이가 연결할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-132">If you configure Firewall Clustering to have a virtual IP, you must break the cluster and expose the VPN appliance directly to a public interface that the gateway can interface with.</span></span>

### <a name="step-7-check-whether-the-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="b357f-133">7단계 온-프레미스 VPN 장치에 PFS(Perfect Forward Secrecy)가 사용하도록 설정되어 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="b357f-133">Step 7 Check whether the on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="b357f-134">**PFS(Perfect Forward Secrecy)** 기능은 연결 끊김 문제를 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-134">The **Perfect Forward Secrecy** feature can cause the disconnection problems.</span></span> <span data-ttu-id="b357f-135">VPN 장치에 **PFS(Perfect Forward Secrecy)** 기능이 사용하도록 설정되어 있으면 이 기능을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-135">If the VPN device has **Perfect forward Secrecy** enabled, disable the feature.</span></span> <span data-ttu-id="b357f-136">그런 다음 [가상 네트워크 게이트웨이 IPsec 정책을 업데이트](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy)합니다.</span><span class="sxs-lookup"><span data-stu-id="b357f-136">Then [update the virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b357f-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b357f-137">Next steps</span></span>

- [<span data-ttu-id="b357f-138">가상 네트워크에 대한 사이트 간 연결 구성</span><span class="sxs-lookup"><span data-stu-id="b357f-138">Configure a Site-to-Site connection to a virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="b357f-139">사이트 간 VPN 연결에 대한 IPsec/IKE 정책 구성</span><span class="sxs-lookup"><span data-stu-id="b357f-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

