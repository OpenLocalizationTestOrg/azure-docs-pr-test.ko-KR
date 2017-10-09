---
title: "Azure 사이트 간 VPN 연결이 일시적으로 끊어진 aaaTroubleshoot | Microsoft Docs"
description: "Tootroubleshoot 정기적으로 분리 하는 hello 사이트 간 VPN 연결에 문제가 hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="e9f33-103">문제 해결: Azure 사이트 간 VPN 일시적 연결 끊김</span><span class="sxs-lookup"><span data-stu-id="e9f33-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="e9f33-104">새로운 또는 기존 Microsoft Azure 지점 및 사이트 간 VPN 연결 안정적이 지 않은 또는 정기적으로 연결을 끊습니다 hello 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-104">You might experience hello problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="e9f33-105">이 문서에서는 확인 하 고 hello 문제의 hello 원인을 해결 단계 toohelp 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-105">This article provides troubleshoot steps toohelp you identify and resolve hello cause of hello problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="e9f33-106">문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="e9f33-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="e9f33-107">필수 조건 단계</span><span class="sxs-lookup"><span data-stu-id="e9f33-107">Prerequisite step</span></span>

<span data-ttu-id="e9f33-108">Azure 가상 네트워크 게이트웨이 hello 유형을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-108">Check hello type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="e9f33-109">너무 이동[Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-109">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e9f33-110">Hello 확인 **개요** hello 형식 정보에 대 한 hello 가상 네트워크 게이트웨이의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-110">Check hello **Overview** page of hello virtual network gateway for hello type information.</span></span>
    
    ![hello 게이트웨이의 hello 개요](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="e9f33-112">Hello 온-프레미스 VPN 장치의 유효성을 검사 하는지 여부를 1 단계</span><span class="sxs-lookup"><span data-stu-id="e9f33-112">Step 1 Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="e9f33-113">[확인된 VPN 장치 및 운영 체제 버전](vpn-gateway-about-vpn-devices.md#devicetable)을 사용 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="e9f33-114">Hello VPN 장치 검증 되지 않은 경우에 모든 호환성 문제가 있는 경우 toocontact hello 장치 제조업체 toosee를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-114">If hello VPN device is not validated, you may have toocontact hello device manufacturer toosee if there is any compatibility issue.</span></span>
2. <span data-ttu-id="e9f33-115">해당 hello VPN 장치가 올바르게 구성 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-115">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="e9f33-116">자세한 내용은 [장치 구성 샘플 편집](vpn-gateway-about-vpn-devices.md#editing)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9f33-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="e9f33-117">2 단계 확인 hello 보안 연결 설정 (정책 기반 Azure 가상 네트워크 게이트웨이)</span><span class="sxs-lookup"><span data-stu-id="e9f33-117">Step 2 Check hello Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="e9f33-118">확인 hello 가상 네트워크, 서브넷 및 범위 hello에 **로컬 네트워크 게이트웨이** 정의 Microsoft Azure의 hello 구성 hello 온-프레미스 VPN 장치에서와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-118">Make sure that hello virtual network, subnets and, ranges in hello **Local network gateway** definition in Microsoft Azure are same as hello configuration on hello on-premises VPN device.</span></span>
2. <span data-ttu-id="e9f33-119">Hello 보안 연결 설정을 일치 하는 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-119">Verify that hello Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="e9f33-120">3단계 게이트웨이 서브넷에 대한 사용자 정의 경로 또는 네트워크 보안 그룹 확인</span><span class="sxs-lookup"><span data-stu-id="e9f33-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="e9f33-121">Hello 게이트웨이 서브넷의 사용자 정의 경로 사용 하는 일부 트래픽을 제한 하 고 다른 트래픽을 허용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-121">A user-defined route on hello gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="e9f33-122">이렇게 하면 일부 트래픽에 대 한 신뢰할 수 없는 및 다른 사용자에 대 한 좋은 hello VPN 연결 인지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-122">This makes it appear that hello VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="e9f33-123">4 단계 확인 "서브넷 쌍 당 하나의 VPN 터널" hello (정책 기반 가상 네트워크 게이트웨이)에 대 한 설정</span><span class="sxs-lookup"><span data-stu-id="e9f33-123">Step 4 Check hello "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="e9f33-124">해당 hello 온-프레미스 VPN 장치가 toohave 설정 되어 있는지 확인 **서브넷 쌍 당 하나의 VPN 터널** 정책 기반 가상 네트워크 게이트웨이에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-124">Make sure that hello on-premises VPN device is set toohave **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="e9f33-125">5단계 보안 연결 제한 확인(정책 기반 가상 네트워크 게이트웨이의 경우)</span><span class="sxs-lookup"><span data-stu-id="e9f33-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="e9f33-126">hello 정책 기반 가상 네트워크 게이트웨이 서브넷 보안 연결 쌍 200의 제한이 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-126">hello Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="e9f33-127">Azure 가상 네트워크 서브넷의 hello 수 번 곱한 hello로 로컬 서브넷의 수는 200 보다 크고, 연결 끊기 산발적 인 서브넷을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e9f33-127">If hello number of Azure virtual network subnets multiplied times by hello number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="e9f33-128">6단계 온-프레미스 VPN 장치 외부 인터페이스 주소 확인</span><span class="sxs-lookup"><span data-stu-id="e9f33-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="e9f33-129">Hello VPN 장치의 IP 주소를 사용 하는 인터넷 hello에 포함 되어 있으면 hello **로컬 네트워크 게이트웨이** 정의 Azure에서 산발적 연결 끊김 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-129">If hello Internet facing IP address of hello VPN device is included in hello **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="e9f33-130">hello 장치 외부 인터페이스 해야 hello 인터넷에서 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-130">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="e9f33-131">네트워크 주소 변환 (NAT) 또는 인터넷 hello 및 hello 장치 사이 방화벽이 없습니다 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-131">There should be no Network Address Translation (NAT) or firewall between hello Internet and hello device.</span></span>
-  <span data-ttu-id="e9f33-132">방화벽 클러스터링 toohave 가상 IP를 구성 하는 경우에 hello 클러스터를 중단 하 고 게이트웨이 hello tooa 공용 인터페이스와 상호 작용할 수 있는 직접 hello VPN 어플라이언스를 노출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-132">If you configure Firewall Clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="e9f33-133">Hello 온-프레미스 VPN 장치에 전달 완전 사용 여부를 7 확인 단계</span><span class="sxs-lookup"><span data-stu-id="e9f33-133">Step 7 Check whether hello on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="e9f33-134">hello **Perfect Forward Secrecy** 기능 hello 연결 끊기 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-134">hello **Perfect Forward Secrecy** feature can cause hello disconnection problems.</span></span> <span data-ttu-id="e9f33-135">Hello VPN 장치에 있으면 **forward Secrecy 완벽 한** hello 기능을 해제를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-135">If hello VPN device has **Perfect forward Secrecy** enabled, disable hello feature.</span></span> <span data-ttu-id="e9f33-136">그런 다음 [hello 가상 네트워크 게이트웨이 IPsec 정책 업데이트](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy)합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f33-136">Then [update hello virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9f33-137">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e9f33-137">Next steps</span></span>

- [<span data-ttu-id="e9f33-138">사이트 간 연결 tooa 가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="e9f33-138">Configure a Site-to-Site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="e9f33-139">사이트 간 VPN 연결에 대한 IPsec/IKE 정책 구성</span><span class="sxs-lookup"><span data-stu-id="e9f33-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

