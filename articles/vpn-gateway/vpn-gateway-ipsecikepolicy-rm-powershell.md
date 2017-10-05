---
title: "S2S VPN 또는 VNet 간 연결에 대한 IPsec/IKE 정책 구성: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "이 문서에서는 Azure Resource Manager 및 PowerShell을 사용하여 Azure VPN Gateway와의 S2S 또는 VNet 간 연결에 대한 IPsec/IKE 정책을 구성하는 방법을 안내합니다."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: 798014b6e8d4495db99ef2e2d2ea487ae7d02fd0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a><span data-ttu-id="b27bd-103">S2S VPN 또는 VNet 간 연결에 대한 IPsec/IKE 정책 구성</span><span class="sxs-lookup"><span data-stu-id="b27bd-103">Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections</span></span>

<span data-ttu-id="b27bd-104">이 문서에서는 Resource Manager 배포 모델 및 PowerShell을 사용하여 사이트 간 VPN 또는 VNet 간 연결에 대한 IPsec/IKE 정책을 구성하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-104">This article walks you through the steps to configure IPsec/IKE policy for Site-to-Site VPN or VNet-to-VNet connections using the Resource Manager deployment model and PowerShell.</span></span>

## <span data-ttu-id="b27bd-105"><a name="about"></a>Azure VPN Gateway에 대한 IPsec 및 IKE 정책 매개 변수 정보</span><span class="sxs-lookup"><span data-stu-id="b27bd-105"><a name="about"></a>About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="b27bd-106">IPsec 및 IKE 프로토콜 표준은 다양하게 결합된 다양한 암호화 알고리즘을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="b27bd-107">이러한 지원이 어떻게 프레미스 간 및 VNet 간 연결이 준수 또는 보안 요구 사항을 충족하도록 하는 데 도움이 될 수 있는지를 확인하려면 [암호화 요구 사항 및 Azure VPN Gateway 정보](vpn-gateway-about-compliance-crypto.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b27bd-107">Refer to [About cryptographic requirements and Azure VPN gateways](vpn-gateway-about-compliance-crypto.md) to see how this can help ensuring cross-premises and VNet-to-VNet connectivity satisfy your compliance or security requirements.</span></span>

<span data-ttu-id="b27bd-108">이 문서에서는 IPsec/IKE 정책을 만들고 구성하여 새 연결 또는 기존 연결에 적용하기 위한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-108">This article provides instructions to create and configure an IPsec/IKE policy and apply to a new or existing connection:</span></span>

* [<span data-ttu-id="b27bd-109">1부 - IPsec/IKE 정책을 만들고 설정하는 워크플로</span><span class="sxs-lookup"><span data-stu-id="b27bd-109">Part 1 - Workflow to create and set IPsec/IKE policy</span></span>](#workflow)
* [<span data-ttu-id="b27bd-110">2부 - 지원되는 암호화 알고리즘 및 키 수준</span><span class="sxs-lookup"><span data-stu-id="b27bd-110">Part 2 - Supported cryptographic algorithms and key strengths</span></span>](#params)
* [<span data-ttu-id="b27bd-111">3부 - IPsec/IKE 정책을 사용하여 새 S2S VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-111">Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>](#crossprem)
* [<span data-ttu-id="b27bd-112">4부 - IPsec/IKE 정책을 사용하여 새 VNet 간 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-112">Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>](#vnet2vnet)
* [<span data-ttu-id="b27bd-113">5부 - 연결에 대한 IPsec/IKE 정책 관리(만들기, 추가, 제거)</span><span class="sxs-lookup"><span data-stu-id="b27bd-113">Part 5 - Manage (create, add, remove) IPsec/IKE policy for a connection</span></span>](#managepolicy)

> [!IMPORTANT]
> 1. <span data-ttu-id="b27bd-114">IPsec/IKE 정책은 다음 게이트웨이 SKU에만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-114">Note that IPsec/IKE policy only works on the following gateway SKUs:</span></span>
>    * <span data-ttu-id="b27bd-115">***VpnGw1, VpnGw2, VpnGw3***(경로 기반)</span><span class="sxs-lookup"><span data-stu-id="b27bd-115">***VpnGw1, VpnGw2, VpnGw3*** (route-based)</span></span>
>    * <span data-ttu-id="b27bd-116">***Standard*** 및 ***HighPerformance***(경로 기반)</span><span class="sxs-lookup"><span data-stu-id="b27bd-116">***Standard*** and ***HighPerformance*** (route-based)</span></span>
> 2. <span data-ttu-id="b27bd-117">지정된 연결에 대해 ***하나의*** 정책 조합만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-117">You can only specify ***one*** policy combination for a given connection.</span></span>
> 3. <span data-ttu-id="b27bd-118">IKE(주 모드)와 IPsec(빠른 모드) 둘 다에 대한 모든 알고리즘 및 매개 변수를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-118">You must specify all algorithms and parameters for both IKE (Main Mode) and IPsec (Quick Mode).</span></span> <span data-ttu-id="b27bd-119">부분 정책 지정은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-119">Partial policy specification is not allowed.</span></span>
> 4. <span data-ttu-id="b27bd-120">해당 VPN 장치 공급업체 사양을 참조하여 정책이 해당 온-프레미스 VPN 장치에서 지원되는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="b27bd-120">Consult with your VPN device vendor specifications to ensure the policy is supported on your on-premises VPN devices.</span></span> <span data-ttu-id="b27bd-121">정책이 호환되지 않는 경우 S2S 또는 VNet 간 연결을 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-121">S2S or VNet-to-VNet connections cannot establish if the policies are incompatible.</span></span>

## <span data-ttu-id="b27bd-122"><a name ="workflow"></a>1부 - IPsec/IKE 정책을 만들고 설정하는 워크플로</span><span class="sxs-lookup"><span data-stu-id="b27bd-122"><a name ="workflow"></a>Part 1 - Workflow to create and set IPsec/IKE policy</span></span>
<span data-ttu-id="b27bd-123">이 섹션에서는 S2S VPN 또는 VNet 간 연결에 대한 IPsec/IKE 정책을 만들고 업데이트하는 워크플로를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-123">This section outlines the workflow to create and update IPsec/IKE policy on a S2S VPN or VNet-to-VNet connection:</span></span>
1. <span data-ttu-id="b27bd-124">가상 네트워크 및 VPN Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-124">Create a virtual network and a VPN gateway</span></span>
2. <span data-ttu-id="b27bd-125">프레미스 간 연결에 대한 로컬 네트워크 게이트웨이 또는 VNet 간 연결에 대한 다른 가상 네트워크 및 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-125">Create a local network gateway for cross premises connection, or another virtual network and gateway for VNet-to-VNet connection</span></span>
3. <span data-ttu-id="b27bd-126">선택한 알고리즘 및 매개 변수를 사용하여 IPsec/IKE 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-126">Create an IPsec/IKE policy with selected algorithms and parameters</span></span>
4. <span data-ttu-id="b27bd-127">IPsec/IKE 정책을 사용하여 연결(IPsec 또는 VNet 간) 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-127">Create a connection (IPsec or VNet2VNet) with the IPsec/IKE policy</span></span>
5. <span data-ttu-id="b27bd-128">기존 연결에 대한 IPsec/IKE 정책 추가/업데이트/제거</span><span class="sxs-lookup"><span data-stu-id="b27bd-128">Add/update/remove an IPsec/IKE policy for an existing connection</span></span>

<span data-ttu-id="b27bd-129">이 문서의 지침에서는 다음 다이어그램에 표시된 대로 IPsec/IKE 정책을 설정하고 구성하도록 돕습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-129">The instructions in this article helps you set up and configure IPsec/IKE policies as shown in the diagram:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <span data-ttu-id="b27bd-131"><a name ="params"></a>2부 - 지원되는 암호화 알고리즘 및 키 수준</span><span class="sxs-lookup"><span data-stu-id="b27bd-131"><a name ="params"></a>Part 2 - Supported cryptographic algorithms & key strengths</span></span>

<span data-ttu-id="b27bd-132">다음 표에는 고객이 구성 가능하도록 지원되는 암호화 알고리즘 및 키 강도가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-132">The following table lists the supported cryptographic algorithms and key strengths configurable by the customers:</span></span>

| <span data-ttu-id="b27bd-133">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="b27bd-133">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="b27bd-134">**옵션**</span><span class="sxs-lookup"><span data-stu-id="b27bd-134">**Options**</span></span>    |
| ---  | --- 
| <span data-ttu-id="b27bd-135">IKEv2 암호화</span><span class="sxs-lookup"><span data-stu-id="b27bd-135">IKEv2 Encryption</span></span> | <span data-ttu-id="b27bd-136">AES256, AES192, AES128, DES3, DES</span><span class="sxs-lookup"><span data-stu-id="b27bd-136">AES256, AES192, AES128, DES3, DES</span></span>  
| <span data-ttu-id="b27bd-137">IKEv2 무결성</span><span class="sxs-lookup"><span data-stu-id="b27bd-137">IKEv2 Integrity</span></span>  | <span data-ttu-id="b27bd-138">SHA384, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="b27bd-138">SHA384, SHA256, SHA1, MD5</span></span>  |
| <span data-ttu-id="b27bd-139">DH 그룹</span><span class="sxs-lookup"><span data-stu-id="b27bd-139">DH Group</span></span>         | <span data-ttu-id="b27bd-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, 없음</span><span class="sxs-lookup"><span data-stu-id="b27bd-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None</span></span> |
| <span data-ttu-id="b27bd-141">IPsec 암호화</span><span class="sxs-lookup"><span data-stu-id="b27bd-141">IPsec Encryption</span></span> | <span data-ttu-id="b27bd-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, 없음</span><span class="sxs-lookup"><span data-stu-id="b27bd-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span></span>    |
| <span data-ttu-id="b27bd-143">IPsec 무결성</span><span class="sxs-lookup"><span data-stu-id="b27bd-143">IPsec Integrity</span></span>  | <span data-ttu-id="b27bd-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="b27bd-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span></span> |
| <span data-ttu-id="b27bd-145">PFS 그룹</span><span class="sxs-lookup"><span data-stu-id="b27bd-145">PFS Group</span></span>        | <span data-ttu-id="b27bd-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, 없음</span><span class="sxs-lookup"><span data-stu-id="b27bd-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None</span></span> 
| <span data-ttu-id="b27bd-147">QM SA 수명</span><span class="sxs-lookup"><span data-stu-id="b27bd-147">QM SA Lifetime</span></span>   | <span data-ttu-id="b27bd-148">(**선택 사항**: 지정되지 않으면 기본값이 사용됨)</span><span class="sxs-lookup"><span data-stu-id="b27bd-148">(**Optional**: default values are used if not specified)</span></span><br><span data-ttu-id="b27bd-149">초(정수, **최소 300**/기본값 27,000초)</span><span class="sxs-lookup"><span data-stu-id="b27bd-149">Seconds (integer; **min. 300**/default 27000 seconds)</span></span><br><span data-ttu-id="b27bd-150">KB(정수, **최소 1,024**/기본값 102,400,000KB)</span><span class="sxs-lookup"><span data-stu-id="b27bd-150">KBytes (integer; **min. 1024**/default 102400000 KBytes)</span></span>   |
| <span data-ttu-id="b27bd-151">트래픽 선택기</span><span class="sxs-lookup"><span data-stu-id="b27bd-151">Traffic Selector</span></span> | <span data-ttu-id="b27bd-152">UsePolicyBasedTrafficSelectors** ($True/$False - **선택 사항**, 지정되지 않으면 기본값 $False)</span><span class="sxs-lookup"><span data-stu-id="b27bd-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, default $False if not specified)</span></span>    |
|  |  |

> [!IMPORTANT]
> 1. <span data-ttu-id="b27bd-153">**GCMAES가 IPsec 암호화 알고리즘에 사용되면 IPsec 무결성에 대해 동일한 GCMAES 알고리즘 및 키 길이를 선택해야 합니다(예: 둘 다에 대해 GCMAES128 사용).**</span><span class="sxs-lookup"><span data-stu-id="b27bd-153">**If GCMAES is used as for IPsec Encryption algorithm, you must select the same GCMAES algorithm and key length for IPsec Integrity; for example, using GCMAES128 for both**</span></span>
> 2. <span data-ttu-id="b27bd-154">IKEv2 주 모드 SA 수명은 Azure VPN Gateway에서 28,800초로 고정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-154">IKEv2 Main Mode SA lifetime is fixed at 28,800 seconds on the Azure VPN gateways</span></span>
> 3. <span data-ttu-id="b27bd-155">연결에 대해 “UsePolicyBasedTrafficSelectors”를 $True로 설정하면 온-프레미스의 정책 기반 VPN 방화벽에 연결되도록 Azure VPN Gateway가 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-155">Setting "UsePolicyBasedTrafficSelectors" to $True on a connection will configure the Azure VPN gateway to connect to policy-based VPN firewall on premises.</span></span> <span data-ttu-id="b27bd-156">PolicyBasedTrafficSelectors를 사용하도록 설정한 경우 VPN 장치에 온-프레미스 네트워크(로컬 네트워크 게이트웨이) 접두사 및 Azure Virtual Network 접두사 간의 모든 조합으로 정의된 일치하는 트래픽 선택기가 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-156">If you enable PolicyBasedTrafficSelectors, you need to ensure your VPN device has the matching traffic selectors defined with all combinations of your on-premises network (local network gateway) prefixes to/from the Azure virtual network prefixes, instead of any-to-any.</span></span> <span data-ttu-id="b27bd-157">예를 들어 온-프레미스 네트워크 접두사가 10.1.0.0/16 및 10.2.0.0/16이고 가상 네트워크 접두사가 192.168.0.0/16 및 172.16.0.0/16이면 다음 트래픽 선택기를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-157">For example, if your on-premises network prefixes are 10.1.0.0/16 and 10.2.0.0/16, and your virtual network prefixes are 192.168.0.0/16 and 172.16.0.0/16, you need to specify the following traffic selectors:</span></span>
>    * <span data-ttu-id="b27bd-158">10.1.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b27bd-158">10.1.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="b27bd-159">10.1.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b27bd-159">10.1.0.0/16 <====> 172.16.0.0/16</span></span>
>    * <span data-ttu-id="b27bd-160">10.2.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b27bd-160">10.2.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="b27bd-161">10.2.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b27bd-161">10.2.0.0/16 <====> 172.16.0.0/16</span></span>

<span data-ttu-id="b27bd-162">정책 기반 트래픽 선택기에 대한 자세한 내용은 [여러 온-프레미스 정책 기반 VPN 장치 연결](vpn-gateway-connect-multiple-policybased-rm-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b27bd-162">For more information regarding policy-based traffic selectors, see [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

<span data-ttu-id="b27bd-163">다음 표에는 사용자 지정 정책에서 지원하는 해당 Diffie-hellman 그룹이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-163">The following table lists the corresponding Diffie-Hellman Groups supported by the custom policy:</span></span>

| <span data-ttu-id="b27bd-164">**Diffie-Hellman 그룹**</span><span class="sxs-lookup"><span data-stu-id="b27bd-164">**Diffie-Hellman Group**</span></span>  | <span data-ttu-id="b27bd-165">**DHGroup**</span><span class="sxs-lookup"><span data-stu-id="b27bd-165">**DHGroup**</span></span>              | <span data-ttu-id="b27bd-166">**PFSGroup**</span><span class="sxs-lookup"><span data-stu-id="b27bd-166">**PFSGroup**</span></span> | <span data-ttu-id="b27bd-167">**키 길이**</span><span class="sxs-lookup"><span data-stu-id="b27bd-167">**Key length**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b27bd-168">1</span><span class="sxs-lookup"><span data-stu-id="b27bd-168">1</span></span>                         | <span data-ttu-id="b27bd-169">DHGroup1</span><span class="sxs-lookup"><span data-stu-id="b27bd-169">DHGroup1</span></span>                 | <span data-ttu-id="b27bd-170">PFS1</span><span class="sxs-lookup"><span data-stu-id="b27bd-170">PFS1</span></span>         | <span data-ttu-id="b27bd-171">768비트 MODP</span><span class="sxs-lookup"><span data-stu-id="b27bd-171">768-bit MODP</span></span>   |
| <span data-ttu-id="b27bd-172">2</span><span class="sxs-lookup"><span data-stu-id="b27bd-172">2</span></span>                         | <span data-ttu-id="b27bd-173">DHGroup2</span><span class="sxs-lookup"><span data-stu-id="b27bd-173">DHGroup2</span></span>                 | <span data-ttu-id="b27bd-174">PFS2</span><span class="sxs-lookup"><span data-stu-id="b27bd-174">PFS2</span></span>         | <span data-ttu-id="b27bd-175">1024비트 MODP</span><span class="sxs-lookup"><span data-stu-id="b27bd-175">1024-bit MODP</span></span>  |
| <span data-ttu-id="b27bd-176">14</span><span class="sxs-lookup"><span data-stu-id="b27bd-176">14</span></span>                        | <span data-ttu-id="b27bd-177">DHGroup14</span><span class="sxs-lookup"><span data-stu-id="b27bd-177">DHGroup14</span></span><br><span data-ttu-id="b27bd-178">DHGroup2048</span><span class="sxs-lookup"><span data-stu-id="b27bd-178">DHGroup2048</span></span> | <span data-ttu-id="b27bd-179">PFS2048</span><span class="sxs-lookup"><span data-stu-id="b27bd-179">PFS2048</span></span>      | <span data-ttu-id="b27bd-180">2048비트 MODP</span><span class="sxs-lookup"><span data-stu-id="b27bd-180">2048-bit MODP</span></span>  |
| <span data-ttu-id="b27bd-181">19</span><span class="sxs-lookup"><span data-stu-id="b27bd-181">19</span></span>                        | <span data-ttu-id="b27bd-182">ECP256</span><span class="sxs-lookup"><span data-stu-id="b27bd-182">ECP256</span></span>                   | <span data-ttu-id="b27bd-183">ECP256</span><span class="sxs-lookup"><span data-stu-id="b27bd-183">ECP256</span></span>       | <span data-ttu-id="b27bd-184">256비트 ECP</span><span class="sxs-lookup"><span data-stu-id="b27bd-184">256-bit ECP</span></span>    |
| <span data-ttu-id="b27bd-185">20</span><span class="sxs-lookup"><span data-stu-id="b27bd-185">20</span></span>                        | <span data-ttu-id="b27bd-186">ECP384</span><span class="sxs-lookup"><span data-stu-id="b27bd-186">ECP384</span></span>                   | <span data-ttu-id="b27bd-187">ECP284</span><span class="sxs-lookup"><span data-stu-id="b27bd-187">ECP284</span></span>       | <span data-ttu-id="b27bd-188">384비트 ECP</span><span class="sxs-lookup"><span data-stu-id="b27bd-188">384-bit ECP</span></span>    |
| <span data-ttu-id="b27bd-189">24</span><span class="sxs-lookup"><span data-stu-id="b27bd-189">24</span></span>                        | <span data-ttu-id="b27bd-190">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="b27bd-190">DHGroup24</span></span>                | <span data-ttu-id="b27bd-191">PFS24</span><span class="sxs-lookup"><span data-stu-id="b27bd-191">PFS24</span></span>        | <span data-ttu-id="b27bd-192">2048비트 MODP</span><span class="sxs-lookup"><span data-stu-id="b27bd-192">2048-bit MODP</span></span>  |

<span data-ttu-id="b27bd-193">자세한 내용은 [RFC3526](https://tools.ietf.org/html/rfc3526) 및 [RFC5114](https://tools.ietf.org/html/rfc5114)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b27bd-193">Refer to [RFC3526](https://tools.ietf.org/html/rfc3526) and [RFC5114](https://tools.ietf.org/html/rfc5114) for more details.</span></span>

## <span data-ttu-id="b27bd-194"><a name ="crossprem"></a>3부 - IPsec/IKE 정책을 사용하여 새 S2S VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-194"><a name ="crossprem"></a>Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>

<span data-ttu-id="b27bd-195">이 섹션에서는 IPsec/IKE 정책을 사용하여 S2S VPN 연결을 만드는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-195">This section walks you through the steps of creating a S2S VPN connection with an IPsec/IKE policy.</span></span> <span data-ttu-id="b27bd-196">다음 단계에서는 다음 다이어그램에 표시된 대로 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-196">The following steps create the connection as shown in the diagram:</span></span>

![s2s-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

<span data-ttu-id="b27bd-198">S2S VPN 연결을 만드는 자세한 단계별 지침은 [S2S VPN 연결 만들기](vpn-gateway-create-site-to-site-rm-powershell.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b27bd-198">See [Create a S2S VPN connection](vpn-gateway-create-site-to-site-rm-powershell.md) for more detailed step-by-step instructions for creating a S2S VPN connection.</span></span>

### <span data-ttu-id="b27bd-199"><a name="before"></a>시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="b27bd-199"><a name="before"></a>Before you begin</span></span>

* <span data-ttu-id="b27bd-200">Azure 구독이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-200">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="b27bd-201">Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-201">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b27bd-202">Azure Resource Manager PowerShell cmdlet을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-202">Install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="b27bd-203">PowerShell cmdlet 설치에 대한 자세한 내용은 [Azure PowerShell 개요](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b27bd-203">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <span data-ttu-id="b27bd-204"><a name="createvnet1"></a>1단계 - 가상 네트워크, VPN Gateway 및 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-204"><a name="createvnet1"></a>Step 1 - Create the virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="b27bd-205">1. 변수 선언</span><span class="sxs-lookup"><span data-stu-id="b27bd-205">1. Declare your variables</span></span>

<span data-ttu-id="b27bd-206">이 연습에서는 먼저 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-206">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="b27bd-207">생산을 위해 구성하는 경우 값을 사용자의 값으로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-207">Be sure to replace the values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="b27bd-208">2. 구독에 연결하고 새 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-208">2. Connect to your subscription and create a new resource group</span></span>

<span data-ttu-id="b27bd-209">리소스 관리자 cmdlet을 사용하려면 PowerShell 모드로 전환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-209">Make sure you switch to PowerShell mode to use the Resource Manager cmdlets.</span></span> <span data-ttu-id="b27bd-210">자세한 내용은 [리소스 관리자에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b27bd-210">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="b27bd-211">PowerShell 콘솔을 열고 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-211">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="b27bd-212">연결에 도움이 되도록 다음 샘플을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-212">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="b27bd-213">3. 가상 네트워크, VPN Gateway 및 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-213">3. Create the virtual network, VPN gateway, and local network gateway</span></span>

<span data-ttu-id="b27bd-214">아래 샘플은 세 개의 서브넷과 VPN Gateway가 있는 가상 네트워크 TestVNet1을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-214">The following sample creates the virtual network, TestVNet1, with three subnets, and the VPN gateway.</span></span> <span data-ttu-id="b27bd-215">값을 대체할 때 언제나 게이트웨이 서브넷 이름을 GatewaySubnet라고 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-215">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="b27bd-216">다른 이름을 지정하는 경우 게이트웨이 만들기가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-216">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <span data-ttu-id="b27bd-217"><a name="s2sconnection"></a>2단계 - IPsec/IKE 정책을 사용하여 S2S VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-217"><a name="s2sconnection"></a>Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="b27bd-218">1. IPsec/IKE 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-218">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="b27bd-219">다음 샘플 스크립트는 다음 알고리즘 및 매개 변수를 사용하여 IPsec/IKE 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-219">The following sample script creates an IPsec/IKE policy with the following algorithms and parameters:</span></span>

* <span data-ttu-id="b27bd-220">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="b27bd-220">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="b27bd-221">IPsec: AES256, SHA256, PFS24, SA 수명 7,200초 및 2,048KB</span><span class="sxs-lookup"><span data-stu-id="b27bd-221">IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

<span data-ttu-id="b27bd-222">IPsec으로 GCMAES를 사용하는 경우 IPsec 암호화 및 무결성 모두에 대해 동일한 GCMAES 알고리즘 및 키 길이를 사용해야 합니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-222">If you use GCMAES for IPsec, you must use the same GCMAES algorithm and key length for both IPsec encryption and integrity, for example:</span></span>

* <span data-ttu-id="b27bd-223">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="b27bd-223">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="b27bd-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA 수명 7200초 및 2048KB</span><span class="sxs-lookup"><span data-stu-id="b27bd-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-the-s2s-vpn-connection-with-the-ipsecike-policy"></a><span data-ttu-id="b27bd-225">2. IPsec/IKE 정책을 사용하여 S2S VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-225">2. Create the S2S VPN connection with the IPsec/IKE policy</span></span>

<span data-ttu-id="b27bd-226">S2S VPN 연결을 만들고 이전에 만든 IPsec/IKE 정책을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-226">Create an S2S VPN connection and apply the IPsec/IKE policy created earlier.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="b27bd-227">필요한 경우 “-UsePolicyBasedTrafficSelectors $True”를 추가하여 연결 cmdlet을 만듦으로써 Azure VPN Gateway가 위에 설명된 대로 온-프레미스의 정책 기반 VPN 장치에 연결하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-227">You can optionally add "-UsePolicyBasedTrafficSelectors $True" to the create connection cmdlet to enable Azure VPN gateway to connect to policy-based VPN devices on premises, as described above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b27bd-228">연결에 IPsec/IKE 정책이 지정되고 나면 Azure VPN Gateway는 해당 특정 연결에 지정된 암호화 알고리즘 및 키 수준으로 된 IPsec/IKE 제안만 보내거나 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-228">Once an IPsec/IKE policy is specified on a connection, the Azure VPN gateway will only send or accept the IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="b27bd-229">연결에 대한 온-프레미스 VPN 장치에서 정확한 정책 조합을 사용하거나 수락하는지 확인합니다. 그러지 않으면 S2S VPN 터널이 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-229">Make sure your on-premises VPN device for the connection uses or accepts the exact policy combination, otherwise the S2S VPN tunnel will not establish.</span></span>


## <span data-ttu-id="b27bd-230"><a name ="vnet2vnet"></a>4부 - IPsec/IKE 정책을 사용하여 새 VNet 간 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-230"><a name ="vnet2vnet"></a>Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>

<span data-ttu-id="b27bd-231">IPsec/IKE 정책을 사용하여 VNet 간 연결을 만드는 단계는 S2S VPN 연결을 만드는 단계와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-231">The steps of creating a VNet-to-VNet connection with an IPsec/IKE policy are similar to that of a S2S VPN connection.</span></span> <span data-ttu-id="b27bd-232">다음 샘플 스크립트는 다음 다이어그램에 표시된 대로 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-232">The following sample scripts create the connection as shown in the diagram:</span></span>

![v2v-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

<span data-ttu-id="b27bd-234">VNet 간 연결을 만드는 자세한 단계는 [VNet 간 연결 만들기](vpn-gateway-vnet-vnet-rm-ps.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b27bd-234">See [Create a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) for more detailed steps for creating a VNet-to-VNet connection.</span></span> <span data-ttu-id="b27bd-235">TestVNet1 및 VPN Gateway를 만들고 구성하려면 [3부](#crossprem)를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-235">You must complete [Part 3](#crossprem) to create and configure TestVNet1 and the VPN Gateway.</span></span>

### <span data-ttu-id="b27bd-236"><a name="createvnet2"></a>1단계 - 두 번째 가상 네트워크 및 VPN 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-236"><a name="createvnet2"></a>Step 1 - Create the second virtual network and VPN gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="b27bd-237">1. 변수 선언</span><span class="sxs-lookup"><span data-stu-id="b27bd-237">1. Declare your variables</span></span>

<span data-ttu-id="b27bd-238">값을 구성에 사용할 값으로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-238">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-the-second-virtual-network-and-vpn-gateway-in-the-new-resource-group"></a><span data-ttu-id="b27bd-239">2. 새 리소스 그룹에 두 번째 가상 네트워크 및 VPN 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-239">2. Create the second virtual network and VPN gateway in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-the-ipsecike-policy"></a><span data-ttu-id="b27bd-240">2단계 - IPsec/IKE 정책을 사용하여 VNet 간 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-240">Step 2 - Create a VNet-toVNet connection with the IPsec/IKE policy</span></span>

<span data-ttu-id="b27bd-241">S2S VPN 연결과 유사하게 IPsec/IKE 정책을 만든 다음 새 연결에 정책을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-241">Similar to the S2S VPN connection, create an IPsec/IKE policy then apply to policy to the new connection.</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="b27bd-242">1. IPsec/IKE 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-242">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="b27bd-243">다음 샘플 스크립트는 다음 알고리즘 및 매개 변수를 사용하여 다른 IPsec/IKE 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-243">The following sample script creates a different IPsec/IKE policy with the following algorithms and parameters:</span></span>
* <span data-ttu-id="b27bd-244">IKEv2: AES128, SHA1, DHGroup14</span><span class="sxs-lookup"><span data-stu-id="b27bd-244">IKEv2: AES128, SHA1, DHGroup14</span></span>
* <span data-ttu-id="b27bd-245">IPsec: GCMAES128, GCMAES128, PFS14, SA 수명 7,200초 및 4,096KB</span><span class="sxs-lookup"><span data-stu-id="b27bd-245">IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB</span></span>

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-the-ipsecike-policy"></a><span data-ttu-id="b27bd-246">2. IPsec/IKE 정책을 사용하여 VNet 간 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="b27bd-246">2. Create VNet-to-VNet connections with the IPsec/IKE policy</span></span>

<span data-ttu-id="b27bd-247">VNet 간 연결을 만들고 만든 IPsec/IKE 정책을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-247">Create a VNet-to-VNet connection and apply the IPsec/IKE policy you created.</span></span> <span data-ttu-id="b27bd-248">이 예제에서 두 게이트웨이는 동일한 구독에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-248">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="b27bd-249">따라서 같은 PowerShell 세션에서 같은 IPsec/IKE 정책을 사용하여 두 연결을 만들고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-249">So it is possible to create and configure both connections with the same IPsec/IKE policy in the same PowerShell session.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> <span data-ttu-id="b27bd-250">연결에 IPsec/IKE 정책이 지정되고 나면 Azure VPN Gateway는 해당 특정 연결에 지정된 암호화 알고리즘 및 키 수준으로 된 IPsec/IKE 제안만 보내거나 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-250">Once an IPsec/IKE policy is specified on a connection, the Azure VPN gateway will only send or accept the IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="b27bd-251">두 연결에 대한 IPsec 정책이 같은지 확인합니다. 그러지 않으면 VNet 간 연결이 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-251">Make sure the IPsec policies for both connections are the same, otherwise the VNet-to-VNet connection will not establish.</span></span>

<span data-ttu-id="b27bd-252">이러한 단계를 완료하고 나면 몇 분 후에 연결이 설정되고, 시작 부분에 표시된 대로 다음과 같은 네트워크 토폴로지가 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-252">After completing these steps, the connection is established in a few minutes, and you will have the following network topology as shown in the beginning:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <span data-ttu-id="b27bd-254"><a name ="managepolicy"></a>5부 - 연결에 대한 IPsec/IKE 정책 업데이트</span><span class="sxs-lookup"><span data-stu-id="b27bd-254"><a name ="managepolicy"></a>Part 5 - Update IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="b27bd-255">마지막 섹션에서는 기존 S2S 또는 VNet 간 연결에 대한 IPsec/IKE 정책을 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-255">The last section shows you how to manage IPsec/IKE policy for an existing S2S or VNet-to-VNet connection.</span></span> <span data-ttu-id="b27bd-256">아래 연습에서는 연결에 대한 다음 작업을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-256">The exercise below walks you through the following operations on a connection:</span></span>

1. <span data-ttu-id="b27bd-257">연결의 IPsec/IKE 정책 표시</span><span class="sxs-lookup"><span data-stu-id="b27bd-257">Show the IPsec/IKE policy of a connection</span></span>
2. <span data-ttu-id="b27bd-258">연결에 대한 IPsec/IKE 정책 추가 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="b27bd-258">Add or update the IPsec/IKE policy to a connection</span></span>
3. <span data-ttu-id="b27bd-259">연결에서 IPsec/IKE 정책 제거</span><span class="sxs-lookup"><span data-stu-id="b27bd-259">Remove the IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="b27bd-260">같은 단계가 S2S 연결과 VNet 간 연결에도 모두 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-260">The same steps apply to both S2S and VNet-to-VNet connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b27bd-261">IPsec/IKE 정책은 *표준* 및 *고성능* 경로 기반 VPN 게이트웨이에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-261">IPsec/IKE policy is supported on *Standard* and *HighPerformance* route-based VPN gateways only.</span></span> <span data-ttu-id="b27bd-262">기본 게이트웨이 SKU 또는 정책 기반 VPN 게이트웨이에서는 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-262">It does not work on the Basic gateway SKU or the policy-based VPN gateway.</span></span>

#### <a name="1-show-the-ipsecike-policy-of-a-connection"></a><span data-ttu-id="b27bd-263">1. 연결의 IPsec/IKE 정책 표시</span><span class="sxs-lookup"><span data-stu-id="b27bd-263">1. Show the IPsec/IKE policy of a connection</span></span>

<span data-ttu-id="b27bd-264">다음 예제는 연결에 대해 IPsec/IKE 정책을 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-264">The following example shows how to get the IPsec/IKE policy configured on a connection.</span></span> <span data-ttu-id="b27bd-265">또한 스크립트는 위의 연습에서 계속됩니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-265">The scripts also continue from the exercises above.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="b27bd-266">마지막 명령은 연결에 대해 구성된 현재 IPsec/IKE 정책이 있는 경우 이를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-266">The last command lists the current IPsec/IKE policy configured on the connection, if there is any.</span></span> <span data-ttu-id="b27bd-267">다음 샘플 출력은 연결에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-267">The following sample output is for the connection:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

<span data-ttu-id="b27bd-268">구성된 IPsec/IKE 정책이 없는 경우 명령(PS> $connection6.policy)을 실행한 결과로 반환되는 내용이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-268">If there is no IPsec/IKE policy configured, the command (PS> $connection6.policy) gets an empty return.</span></span> <span data-ttu-id="b27bd-269">반환되는 내용이 없다고 해서 연결에 대해 IPsec/IKE 정책이 구성되지 않았다는 의미는 아니며, 사용자 지정 IPsec/IKE 정책이 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-269">It does not mean IPsec/IKE is not configured on the connection, but that there is no custom IPsec/IKE policy.</span></span> <span data-ttu-id="b27bd-270">실제 연결은 온-프레미스 VPN 장치 및 Azure VPN Gateway 간에 협상된 기본 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-270">The actual connection uses the default policy negotiated between your on-premises VPN device and the Azure VPN gateway.</span></span>

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a><span data-ttu-id="b27bd-271">2. 연결에 대한 IPsec/IKE 정책 추가 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="b27bd-271">2. Add or update an IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="b27bd-272">연결에 대한 새 정책을 추가하거나 기존 정책을 업데이트하는 단계는 같습니다. 새 정책을 만든 다음 연결에 새 정책을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-272">The steps to add a new policy or update an existing policy on a connection are the same: create a new policy then apply the new policy to the connection.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

<span data-ttu-id="b27bd-273">온-프레미스 정책 기반 VPN 장치에 연결할 때 “UsePolicyBasedTrafficSelectors”를 사용하도록 설정하려면 cmdlet에 “-UsePolicyBaseTrafficSelectors” 매개 변수를 추가하거나, 이 매개 변수를 $False로 설정하여 옵션을 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-273">To enable "UsePolicyBasedTrafficSelectors" when connecting to an on-premises policy-based VPN device, add the "-UsePolicyBaseTrafficSelectors" parameter to the cmdlet, or set it to $False to disable the option:</span></span>

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

<span data-ttu-id="b27bd-274">연결을 다시 가져와 정책이 업데이트되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-274">You can get the connection again to check if the policy is updated.</span></span>

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="b27bd-275">마지막 줄의 출력은 다음 예제와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-275">You should see the output from the last line, as shown in the following example:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a><span data-ttu-id="b27bd-276">3. 연결에서 IPsec/IKE 정책 제거</span><span class="sxs-lookup"><span data-stu-id="b27bd-276">3. Remove an IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="b27bd-277">연결에서 사용자 지정 정책을 제거하고 나면 Azure VPN Gateway는 [IPsec/IKE 제안의 기본 목록](vpn-gateway-about-vpn-devices.md)으로 되돌려지고 온-프레미스 VPN 장치와 다시 협상합니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-277">Once you remove the custom policy from a connection, the Azure VPN gateway reverts back to the [default list of IPsec/IKE proposals](vpn-gateway-about-vpn-devices.md) and renegotiates again with your on-premises VPN device.</span></span>

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

<span data-ttu-id="b27bd-278">같은 스크립트를 사용하여 연결에서 정책이 제거되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-278">You can use the same script to check if the policy has been removed from the connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b27bd-279">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b27bd-279">Next steps</span></span>

<span data-ttu-id="b27bd-280">정책 기반 트래픽 선택기에 대한 자세한 내용은 [여러 온-프레미스 정책 기반 VPN 장치 연결](vpn-gateway-connect-multiple-policybased-rm-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b27bd-280">See [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) for more details regarding policy-based traffic selectors.</span></span>

<span data-ttu-id="b27bd-281">연결이 완료되면 가상 네트워크에 가상 컴퓨터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b27bd-281">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="b27bd-282">단계는 [가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b27bd-282">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>