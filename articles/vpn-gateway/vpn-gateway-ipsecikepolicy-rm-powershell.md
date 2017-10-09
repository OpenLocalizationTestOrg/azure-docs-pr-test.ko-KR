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
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a><span data-ttu-id="c9979-103">S2S VPN 또는 VNet 간 연결에 대한 IPsec/IKE 정책 구성</span><span class="sxs-lookup"><span data-stu-id="c9979-103">Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections</span></span>

<span data-ttu-id="c9979-104">이 문서는 hello 단계 tooconfigure hello 리소스 관리자 배포 모델 및 PowerShell을 사용 하 여 사이트 간 VPN 또는 VNet 대 VNet 연결을 위한 IPsec/IKE 정책을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-104">This article walks you through hello steps tooconfigure IPsec/IKE policy for Site-to-Site VPN or VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <span data-ttu-id="c9979-105"><a name="about"></a>Azure VPN Gateway에 대한 IPsec 및 IKE 정책 매개 변수 정보</span><span class="sxs-lookup"><span data-stu-id="c9979-105"><a name="about"></a>About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="c9979-106">IPsec 및 IKE 프로토콜 표준은 다양하게 결합된 다양한 암호화 알고리즘을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="c9979-107">너무 참조[Azure VPN 게이트웨이 및 암호화 요구 사항에 대 한](vpn-gateway-about-compliance-crypto.md) toosee이 도울 수 있는 방법 크로스-프레미스 및 VNet 대 VNet 연결을 확인 하면 규정 준수 또는 보안 요구 사항을 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-107">Refer too[About cryptographic requirements and Azure VPN gateways](vpn-gateway-about-compliance-crypto.md) toosee how this can help ensuring cross-premises and VNet-to-VNet connectivity satisfy your compliance or security requirements.</span></span>

<span data-ttu-id="c9979-108">이 문서 toocreate 지침을 제공 하 고 IPsec/IKE 정책을 구성 하 고 tooa 기존 또는 새 연결을 적용:</span><span class="sxs-lookup"><span data-stu-id="c9979-108">This article provides instructions toocreate and configure an IPsec/IKE policy and apply tooa new or existing connection:</span></span>

* [<span data-ttu-id="c9979-109">1-워크플로 toocreate 부 및 IPsec/IKE 정책 설정</span><span class="sxs-lookup"><span data-stu-id="c9979-109">Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>](#workflow)
* [<span data-ttu-id="c9979-110">2부 - 지원되는 암호화 알고리즘 및 키 수준</span><span class="sxs-lookup"><span data-stu-id="c9979-110">Part 2 - Supported cryptographic algorithms and key strengths</span></span>](#params)
* [<span data-ttu-id="c9979-111">3부 - IPsec/IKE 정책을 사용하여 새 S2S VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-111">Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>](#crossprem)
* [<span data-ttu-id="c9979-112">4부 - IPsec/IKE 정책을 사용하여 새 VNet 간 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-112">Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>](#vnet2vnet)
* [<span data-ttu-id="c9979-113">5부 - 연결에 대한 IPsec/IKE 정책 관리(만들기, 추가, 제거)</span><span class="sxs-lookup"><span data-stu-id="c9979-113">Part 5 - Manage (create, add, remove) IPsec/IKE policy for a connection</span></span>](#managepolicy)

> [!IMPORTANT]
> 1. <span data-ttu-id="c9979-114">IPsec/IKE 정책 hello 게이트웨이 Sku를 다음에 작동 한다는 note:</span><span class="sxs-lookup"><span data-stu-id="c9979-114">Note that IPsec/IKE policy only works on hello following gateway SKUs:</span></span>
>    * <span data-ttu-id="c9979-115">***VpnGw1, VpnGw2, VpnGw3***(경로 기반)</span><span class="sxs-lookup"><span data-stu-id="c9979-115">***VpnGw1, VpnGw2, VpnGw3*** (route-based)</span></span>
>    * <span data-ttu-id="c9979-116">***Standard*** 및 ***HighPerformance***(경로 기반)</span><span class="sxs-lookup"><span data-stu-id="c9979-116">***Standard*** and ***HighPerformance*** (route-based)</span></span>
> 2. <span data-ttu-id="c9979-117">지정된 연결에 대해 ***하나의*** 정책 조합만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-117">You can only specify ***one*** policy combination for a given connection.</span></span>
> 3. <span data-ttu-id="c9979-118">IKE(주 모드)와 IPsec(빠른 모드) 둘 다에 대한 모든 알고리즘 및 매개 변수를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-118">You must specify all algorithms and parameters for both IKE (Main Mode) and IPsec (Quick Mode).</span></span> <span data-ttu-id="c9979-119">부분 정책 지정은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-119">Partial policy specification is not allowed.</span></span>
> 4. <span data-ttu-id="c9979-120">VPN 장치 공급 업체 사양을 tooensure hello 정책은 온-프레미스 VPN 장치 지원에 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c9979-120">Consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span> <span data-ttu-id="c9979-121">Hello 정책 호환 되지 않습니다 S2S 또는 VNet 대 VNet 연결을 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-121">S2S or VNet-to-VNet connections cannot establish if hello policies are incompatible.</span></span>

## <span data-ttu-id="c9979-122"><a name ="workflow"></a>1-워크플로 toocreate 부 및 IPsec/IKE 정책 설정</span><span class="sxs-lookup"><span data-stu-id="c9979-122"><a name ="workflow"></a>Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>
<span data-ttu-id="c9979-123">이 섹션에서는 연결 S2S VPN 또는 VNet 대 VNet 연결 hello 워크플로 toocreate 및 update IPsec/IKE 정책 설명:</span><span class="sxs-lookup"><span data-stu-id="c9979-123">This section outlines hello workflow toocreate and update IPsec/IKE policy on a S2S VPN or VNet-to-VNet connection:</span></span>
1. <span data-ttu-id="c9979-124">가상 네트워크 및 VPN Gateway 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-124">Create a virtual network and a VPN gateway</span></span>
2. <span data-ttu-id="c9979-125">프레미스 간 연결에 대한 로컬 네트워크 게이트웨이 또는 VNet 간 연결에 대한 다른 가상 네트워크 및 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-125">Create a local network gateway for cross premises connection, or another virtual network and gateway for VNet-to-VNet connection</span></span>
3. <span data-ttu-id="c9979-126">선택한 알고리즘 및 매개 변수를 사용하여 IPsec/IKE 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-126">Create an IPsec/IKE policy with selected algorithms and parameters</span></span>
4. <span data-ttu-id="c9979-127">Hello IPsec/IKE 정책을 사용 하 여 연결 (IPsec 또는 VNet2VNet) 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-127">Create a connection (IPsec or VNet2VNet) with hello IPsec/IKE policy</span></span>
5. <span data-ttu-id="c9979-128">기존 연결에 대한 IPsec/IKE 정책 추가/업데이트/제거</span><span class="sxs-lookup"><span data-stu-id="c9979-128">Add/update/remove an IPsec/IKE policy for an existing connection</span></span>

<span data-ttu-id="c9979-129">이 문서의 지침 hello를 사용 하 여를 설정 하 고 hello 다이어그램에 나타난 대로 IPsec/IKE 정책을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-129">hello instructions in this article helps you set up and configure IPsec/IKE policies as shown in hello diagram:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <span data-ttu-id="c9979-131"><a name ="params"></a>2부 - 지원되는 암호화 알고리즘 및 키 수준</span><span class="sxs-lookup"><span data-stu-id="c9979-131"><a name ="params"></a>Part 2 - Supported cryptographic algorithms & key strengths</span></span>

<span data-ttu-id="c9979-132">hello 다음 표에 지원 되는 hello 암호화 알고리즘 및 hello 고객에 의해 구성 가능한 키 길이:</span><span class="sxs-lookup"><span data-stu-id="c9979-132">hello following table lists hello supported cryptographic algorithms and key strengths configurable by hello customers:</span></span>

| <span data-ttu-id="c9979-133">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="c9979-133">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="c9979-134">**옵션**</span><span class="sxs-lookup"><span data-stu-id="c9979-134">**Options**</span></span>    |
| ---  | --- 
| <span data-ttu-id="c9979-135">IKEv2 암호화</span><span class="sxs-lookup"><span data-stu-id="c9979-135">IKEv2 Encryption</span></span> | <span data-ttu-id="c9979-136">AES256, AES192, AES128, DES3, DES</span><span class="sxs-lookup"><span data-stu-id="c9979-136">AES256, AES192, AES128, DES3, DES</span></span>  
| <span data-ttu-id="c9979-137">IKEv2 무결성</span><span class="sxs-lookup"><span data-stu-id="c9979-137">IKEv2 Integrity</span></span>  | <span data-ttu-id="c9979-138">SHA384, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="c9979-138">SHA384, SHA256, SHA1, MD5</span></span>  |
| <span data-ttu-id="c9979-139">DH 그룹</span><span class="sxs-lookup"><span data-stu-id="c9979-139">DH Group</span></span>         | <span data-ttu-id="c9979-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, 없음</span><span class="sxs-lookup"><span data-stu-id="c9979-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None</span></span> |
| <span data-ttu-id="c9979-141">IPsec 암호화</span><span class="sxs-lookup"><span data-stu-id="c9979-141">IPsec Encryption</span></span> | <span data-ttu-id="c9979-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, 없음</span><span class="sxs-lookup"><span data-stu-id="c9979-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span></span>    |
| <span data-ttu-id="c9979-143">IPsec 무결성</span><span class="sxs-lookup"><span data-stu-id="c9979-143">IPsec Integrity</span></span>  | <span data-ttu-id="c9979-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span><span class="sxs-lookup"><span data-stu-id="c9979-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span></span> |
| <span data-ttu-id="c9979-145">PFS 그룹</span><span class="sxs-lookup"><span data-stu-id="c9979-145">PFS Group</span></span>        | <span data-ttu-id="c9979-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, 없음</span><span class="sxs-lookup"><span data-stu-id="c9979-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None</span></span> 
| <span data-ttu-id="c9979-147">QM SA 수명</span><span class="sxs-lookup"><span data-stu-id="c9979-147">QM SA Lifetime</span></span>   | <span data-ttu-id="c9979-148">(**선택 사항**: 지정되지 않으면 기본값이 사용됨)</span><span class="sxs-lookup"><span data-stu-id="c9979-148">(**Optional**: default values are used if not specified)</span></span><br><span data-ttu-id="c9979-149">초(정수, **최소 300**/기본값 27,000초)</span><span class="sxs-lookup"><span data-stu-id="c9979-149">Seconds (integer; **min. 300**/default 27000 seconds)</span></span><br><span data-ttu-id="c9979-150">KB(정수, **최소 1,024**/기본값 102,400,000KB)</span><span class="sxs-lookup"><span data-stu-id="c9979-150">KBytes (integer; **min. 1024**/default 102400000 KBytes)</span></span>   |
| <span data-ttu-id="c9979-151">트래픽 선택기</span><span class="sxs-lookup"><span data-stu-id="c9979-151">Traffic Selector</span></span> | <span data-ttu-id="c9979-152">UsePolicyBasedTrafficSelectors** ($True/$False - **선택 사항**, 지정되지 않으면 기본값 $False)</span><span class="sxs-lookup"><span data-stu-id="c9979-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, default $False if not specified)</span></span>    |
|  |  |

> [!IMPORTANT]
> 1. <span data-ttu-id="c9979-153">**선택 해야 GCMAES IPsec 암호화 알고리즘의 경우와 사용 하는 경우 IPsec 무결성;에 대 한 동일한 GCMAES 알고리즘 및 키 길이 hello 예를 들어 GCMAES128 둘 다에 대해 사용 하 여**</span><span class="sxs-lookup"><span data-stu-id="c9979-153">**If GCMAES is used as for IPsec Encryption algorithm, you must select hello same GCMAES algorithm and key length for IPsec Integrity; for example, using GCMAES128 for both**</span></span>
> 2. <span data-ttu-id="c9979-154">Hello Azure VPN 게이트웨이 28, 800 초 IKEv2 주 모드 SA 수명 동안 고정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-154">IKEv2 Main Mode SA lifetime is fixed at 28,800 seconds on hello Azure VPN gateways</span></span>
> 3. <span data-ttu-id="c9979-155">설정 "UsePolicyBasedTrafficSelectors" $True 연결에는 구성 너무 hello Azure VPN 게이트웨이 tooconnect toopolicy 기반 VPN 방화벽 온-프레미스 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-155">Setting "UsePolicyBasedTrafficSelectors" too$True on a connection will configure hello Azure VPN gateway tooconnect toopolicy-based VPN firewall on premises.</span></span> <span data-ttu-id="c9979-156">VPN 장치에는 온-프레미스 네트워크 (로컬 네트워크 게이트웨이) 접두사 hello Azure 가상 네트워크 접두사를의 모든 조합으로 정의 된 hello 일치 하는 트래픽을 선택기 tooensure 필요한 PolicyBasedTrafficSelectors을 설정한 경우 대신 any-에-any입니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-156">If you enable PolicyBasedTrafficSelectors, you need tooensure your VPN device has hello matching traffic selectors defined with all combinations of your on-premises network (local network gateway) prefixes to/from hello Azure virtual network prefixes, instead of any-to-any.</span></span> <span data-ttu-id="c9979-157">예를 들어 온-프레미스 네트워크 접두사는 10.1.0.0/16 및 10.2.0.0/16, 하는 경우 가상 네트워크 접두사는 192.168.0.0/16 및 172.16.0.0/16 트래픽 선택기 뒤 toospecify hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-157">For example, if your on-premises network prefixes are 10.1.0.0/16 and 10.2.0.0/16, and your virtual network prefixes are 192.168.0.0/16 and 172.16.0.0/16, you need toospecify hello following traffic selectors:</span></span>
>    * <span data-ttu-id="c9979-158">10.1.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c9979-158">10.1.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="c9979-159">10.1.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c9979-159">10.1.0.0/16 <====> 172.16.0.0/16</span></span>
>    * <span data-ttu-id="c9979-160">10.2.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c9979-160">10.2.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="c9979-161">10.2.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c9979-161">10.2.0.0/16 <====> 172.16.0.0/16</span></span>

<span data-ttu-id="c9979-162">정책 기반 트래픽 선택기에 대한 자세한 내용은 [여러 온-프레미스 정책 기반 VPN 장치 연결](vpn-gateway-connect-multiple-policybased-rm-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9979-162">For more information regarding policy-based traffic selectors, see [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

<span data-ttu-id="c9979-163">다음 표에 hello hello hello 사용자 지정 정책에서 지 원하는 해당 Diffie-hellman 그룹:</span><span class="sxs-lookup"><span data-stu-id="c9979-163">hello following table lists hello corresponding Diffie-Hellman Groups supported by hello custom policy:</span></span>

| <span data-ttu-id="c9979-164">**Diffie-Hellman 그룹**</span><span class="sxs-lookup"><span data-stu-id="c9979-164">**Diffie-Hellman Group**</span></span>  | <span data-ttu-id="c9979-165">**DHGroup**</span><span class="sxs-lookup"><span data-stu-id="c9979-165">**DHGroup**</span></span>              | <span data-ttu-id="c9979-166">**PFSGroup**</span><span class="sxs-lookup"><span data-stu-id="c9979-166">**PFSGroup**</span></span> | <span data-ttu-id="c9979-167">**키 길이**</span><span class="sxs-lookup"><span data-stu-id="c9979-167">**Key length**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c9979-168">1</span><span class="sxs-lookup"><span data-stu-id="c9979-168">1</span></span>                         | <span data-ttu-id="c9979-169">DHGroup1</span><span class="sxs-lookup"><span data-stu-id="c9979-169">DHGroup1</span></span>                 | <span data-ttu-id="c9979-170">PFS1</span><span class="sxs-lookup"><span data-stu-id="c9979-170">PFS1</span></span>         | <span data-ttu-id="c9979-171">768비트 MODP</span><span class="sxs-lookup"><span data-stu-id="c9979-171">768-bit MODP</span></span>   |
| <span data-ttu-id="c9979-172">2</span><span class="sxs-lookup"><span data-stu-id="c9979-172">2</span></span>                         | <span data-ttu-id="c9979-173">DHGroup2</span><span class="sxs-lookup"><span data-stu-id="c9979-173">DHGroup2</span></span>                 | <span data-ttu-id="c9979-174">PFS2</span><span class="sxs-lookup"><span data-stu-id="c9979-174">PFS2</span></span>         | <span data-ttu-id="c9979-175">1024비트 MODP</span><span class="sxs-lookup"><span data-stu-id="c9979-175">1024-bit MODP</span></span>  |
| <span data-ttu-id="c9979-176">14</span><span class="sxs-lookup"><span data-stu-id="c9979-176">14</span></span>                        | <span data-ttu-id="c9979-177">DHGroup14</span><span class="sxs-lookup"><span data-stu-id="c9979-177">DHGroup14</span></span><br><span data-ttu-id="c9979-178">DHGroup2048</span><span class="sxs-lookup"><span data-stu-id="c9979-178">DHGroup2048</span></span> | <span data-ttu-id="c9979-179">PFS2048</span><span class="sxs-lookup"><span data-stu-id="c9979-179">PFS2048</span></span>      | <span data-ttu-id="c9979-180">2048비트 MODP</span><span class="sxs-lookup"><span data-stu-id="c9979-180">2048-bit MODP</span></span>  |
| <span data-ttu-id="c9979-181">19</span><span class="sxs-lookup"><span data-stu-id="c9979-181">19</span></span>                        | <span data-ttu-id="c9979-182">ECP256</span><span class="sxs-lookup"><span data-stu-id="c9979-182">ECP256</span></span>                   | <span data-ttu-id="c9979-183">ECP256</span><span class="sxs-lookup"><span data-stu-id="c9979-183">ECP256</span></span>       | <span data-ttu-id="c9979-184">256비트 ECP</span><span class="sxs-lookup"><span data-stu-id="c9979-184">256-bit ECP</span></span>    |
| <span data-ttu-id="c9979-185">20</span><span class="sxs-lookup"><span data-stu-id="c9979-185">20</span></span>                        | <span data-ttu-id="c9979-186">ECP384</span><span class="sxs-lookup"><span data-stu-id="c9979-186">ECP384</span></span>                   | <span data-ttu-id="c9979-187">ECP284</span><span class="sxs-lookup"><span data-stu-id="c9979-187">ECP284</span></span>       | <span data-ttu-id="c9979-188">384비트 ECP</span><span class="sxs-lookup"><span data-stu-id="c9979-188">384-bit ECP</span></span>    |
| <span data-ttu-id="c9979-189">24</span><span class="sxs-lookup"><span data-stu-id="c9979-189">24</span></span>                        | <span data-ttu-id="c9979-190">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="c9979-190">DHGroup24</span></span>                | <span data-ttu-id="c9979-191">PFS24</span><span class="sxs-lookup"><span data-stu-id="c9979-191">PFS24</span></span>        | <span data-ttu-id="c9979-192">2048비트 MODP</span><span class="sxs-lookup"><span data-stu-id="c9979-192">2048-bit MODP</span></span>  |

<span data-ttu-id="c9979-193">너무 참조[RFC3526](https://tools.ietf.org/html/rfc3526) 및 [RFC5114](https://tools.ietf.org/html/rfc5114) 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-193">Refer too[RFC3526](https://tools.ietf.org/html/rfc3526) and [RFC5114](https://tools.ietf.org/html/rfc5114) for more details.</span></span>

## <span data-ttu-id="c9979-194"><a name ="crossprem"></a>3부 - IPsec/IKE 정책을 사용하여 새 S2S VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-194"><a name ="crossprem"></a>Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>

<span data-ttu-id="c9979-195">이 섹션에서는 hello IPsec/IKE 정책과 S2S VPN 연결을 만드는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-195">This section walks you through hello steps of creating a S2S VPN connection with an IPsec/IKE policy.</span></span> <span data-ttu-id="c9979-196">hello 다음 단계를 만듭니다 hello 연결 hello 다이어그램에 나타난 대로:</span><span class="sxs-lookup"><span data-stu-id="c9979-196">hello following steps create hello connection as shown in hello diagram:</span></span>

![s2s-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

<span data-ttu-id="c9979-198">S2S VPN 연결을 만드는 자세한 단계별 지침은 [S2S VPN 연결 만들기](vpn-gateway-create-site-to-site-rm-powershell.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9979-198">See [Create a S2S VPN connection](vpn-gateway-create-site-to-site-rm-powershell.md) for more detailed step-by-step instructions for creating a S2S VPN connection.</span></span>

### <span data-ttu-id="c9979-199"><a name="before"></a>시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="c9979-199"><a name="before"></a>Before you begin</span></span>

* <span data-ttu-id="c9979-200">Azure 구독이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-200">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="c9979-201">Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 계정](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-201">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c9979-202">Hello Azure 리소스 관리자 PowerShell cmdlet을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-202">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="c9979-203">참조 [Azure PowerShell 개요](/powershell/azure/overview) hello PowerShell cmdlet을 설치 하는 방법에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-203">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <span data-ttu-id="c9979-204"><a name="createvnet1"></a>1 단계-hello 가상 네트워크, VPN 게이트웨이와 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-204"><a name="createvnet1"></a>Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="c9979-205">1. 변수 선언</span><span class="sxs-lookup"><span data-stu-id="c9979-205">1. Declare your variables</span></span>

<span data-ttu-id="c9979-206">이 연습에서는 먼저 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-206">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="c9979-207">프로덕션 환경에 구성 하는 경우 사용자의 정보로 있는지 tooreplace hello 값 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-207">Be sure tooreplace hello values with your own when configuring for production.</span></span>

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="c9979-208">2. Tooyour 구독을 연결 하 고 새 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-208">2. Connect tooyour subscription and create a new resource group</span></span>

<span data-ttu-id="c9979-209">TooPowerShell 모드 toouse hello 리소스 관리자 cmdlet을 전환 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-209">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="c9979-210">자세한 내용은 [리소스 관리자에서 Windows PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9979-210">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="c9979-211">PowerShell 콘솔을 열고 tooyour 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-211">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="c9979-212">다음 샘플 toohelp 연결한 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-212">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="c9979-213">3. Hello 가상 네트워크, VPN 게이트웨이와 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-213">3. Create hello virtual network, VPN gateway, and local network gateway</span></span>

<span data-ttu-id="c9979-214">다음 예제는 hello 세 개의 서브넷 및 hello VPN 게이트웨이 사용 하 여 TestVNet1, hello 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-214">hello following sample creates hello virtual network, TestVNet1, with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="c9979-215">값을 대체할 때 언제나 게이트웨이 서브넷 이름을 GatewaySubnet라고 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-215">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="c9979-216">다른 이름을 지정하는 경우 게이트웨이 만들기가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-216">If you name it something else, your gateway creation fails.</span></span>

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

### <span data-ttu-id="c9979-217"><a name="s2sconnection"></a>2단계 - IPsec/IKE 정책을 사용하여 S2S VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-217"><a name="s2sconnection"></a>Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="c9979-218">1. IPsec/IKE 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-218">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="c9979-219">다음 샘플 스크립트는 hello hello로 IPsec/IKE 정책을 만듭니다 알고리즘 및 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="c9979-219">hello following sample script creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>

* <span data-ttu-id="c9979-220">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="c9979-220">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="c9979-221">IPsec: AES256, SHA256, PFS24, SA 수명 7,200초 및 2,048KB</span><span class="sxs-lookup"><span data-stu-id="c9979-221">IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

<span data-ttu-id="c9979-222">사용 해야 GCMAES ipsec을 사용 하면 동일한 GCMAES 알고리즘 및 키 길이 IPsec 암호화와 무결성에 대 한 예를 들어 hello:</span><span class="sxs-lookup"><span data-stu-id="c9979-222">If you use GCMAES for IPsec, you must use hello same GCMAES algorithm and key length for both IPsec encryption and integrity, for example:</span></span>

* <span data-ttu-id="c9979-223">IKEv2: AES256, SHA384, DHGroup24</span><span class="sxs-lookup"><span data-stu-id="c9979-223">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="c9979-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA 수명 7200초 및 2048KB</span><span class="sxs-lookup"><span data-stu-id="c9979-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="c9979-225">2. IPsec/IKE 정책 hello로 hello S2S VPN 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-225">2. Create hello S2S VPN connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="c9979-226">S2S VPN 연결을 만들고 앞에서 만든 hello IPsec/IKE 정책을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-226">Create an S2S VPN connection and apply hello IPsec/IKE policy created earlier.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="c9979-227">선택적으로 추가할 수 있습니다 "-UsePolicyBasedTrafficSelectors $True" toohello 연결 만듭니다 cmdlet tooenable Azure VPN 게이트웨이 tooconnect toopolicy 기반 VPN 장치와 온-프레미스로 위에서 설명한 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-227">You can optionally add "-UsePolicyBasedTrafficSelectors $True" toohello create connection cmdlet tooenable Azure VPN gateway tooconnect toopolicy-based VPN devices on premises, as described above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9979-228">연결에 IPsec/IKE 정책을 지정 되 면 hello Azure VPN 게이트웨이 보내거나 지정 된 암호화 알고리즘 및 키 길이 특정 연결에 IPsec/IKE 제안 hello 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-228">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="c9979-229">Hello 연결에 대 한 온-프레미스 VPN 장치를 사용 하거나 그렇지 않으면 hello S2S VPN 터널을 설정 하지 것입니다 hello 정확한 정책 조합을 받아들이는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-229">Make sure your on-premises VPN device for hello connection uses or accepts hello exact policy combination, otherwise hello S2S VPN tunnel will not establish.</span></span>


## <span data-ttu-id="c9979-230"><a name ="vnet2vnet"></a>4부 - IPsec/IKE 정책을 사용하여 새 VNet 간 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-230"><a name ="vnet2vnet"></a>Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>

<span data-ttu-id="c9979-231">hello IPsec/IKE 정책을 사용 하 여 VNet 대 VNet 연결을 만드는 단계는 S2S VPN 연결의 유사한 toothat 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-231">hello steps of creating a VNet-to-VNet connection with an IPsec/IKE policy are similar toothat of a S2S VPN connection.</span></span> <span data-ttu-id="c9979-232">hello 다음 예제 스크립트 만들기 hello 연결 hello 다이어그램에 나타난 대로:</span><span class="sxs-lookup"><span data-stu-id="c9979-232">hello following sample scripts create hello connection as shown in hello diagram:</span></span>

![v2v-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

<span data-ttu-id="c9979-234">VNet 간 연결을 만드는 자세한 단계는 [VNet 간 연결 만들기](vpn-gateway-vnet-vnet-rm-ps.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9979-234">See [Create a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) for more detailed steps for creating a VNet-to-VNet connection.</span></span> <span data-ttu-id="c9979-235">완료 해야 [3 부](#crossprem) toocreate TestVNet1를 구성 하 고 VPN 게이트웨이 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-235">You must complete [Part 3](#crossprem) toocreate and configure TestVNet1 and hello VPN Gateway.</span></span>

### <span data-ttu-id="c9979-236"><a name="createvnet2"></a>1 단계-hello 두 번째 가상 네트워크 및 VPN 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-236"><a name="createvnet2"></a>Step 1 - Create hello second virtual network and VPN gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="c9979-237">1. 변수 선언</span><span class="sxs-lookup"><span data-stu-id="c9979-237">1. Declare your variables</span></span>

<span data-ttu-id="c9979-238">수 있는지 tooreplace 것 hello 사용 하 여 hello 값 구성에 대 한 toouse 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-238">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a><span data-ttu-id="c9979-239">2. Hello 새 리소스 그룹에 hello 두 번째 가상 네트워크 및 VPN 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-239">2. Create hello second virtual network and VPN gateway in hello new resource group</span></span>

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

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="c9979-240">2 단계-IPsec/IKE 정책 hello로 VNet toVNet 연결 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-240">Step 2 - Create a VNet-toVNet connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="c9979-241">비슷한 toohello S2S VPN 연결을 IPsec/IKE 정책을 만든 다음 toopolicy toohello 새 연결을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-241">Similar toohello S2S VPN connection, create an IPsec/IKE policy then apply toopolicy toohello new connection.</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="c9979-242">1. IPsec/IKE 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="c9979-242">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="c9979-243">다음 샘플 스크립트는 hello hello로 다른 IPsec/IKE 정책을 만듭니다 알고리즘 및 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="c9979-243">hello following sample script creates a different IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="c9979-244">IKEv2: AES128, SHA1, DHGroup14</span><span class="sxs-lookup"><span data-stu-id="c9979-244">IKEv2: AES128, SHA1, DHGroup14</span></span>
* <span data-ttu-id="c9979-245">IPsec: GCMAES128, GCMAES128, PFS14, SA 수명 7,200초 및 4,096KB</span><span class="sxs-lookup"><span data-stu-id="c9979-245">IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB</span></span>

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a><span data-ttu-id="c9979-246">2. IPsec/IKE 정책 hello VNet 대 VNet 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-246">2. Create VNet-to-VNet connections with hello IPsec/IKE policy</span></span>

<span data-ttu-id="c9979-247">VNet 대 VNet 연결을 만들고 사용자가 만든 hello IPsec/IKE 정책을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-247">Create a VNet-to-VNet connection and apply hello IPsec/IKE policy you created.</span></span> <span data-ttu-id="c9979-248">이 예에서 두 게이트웨이 hello에는 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-248">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="c9979-249">가능한 toocreate 이며와 모두 연결을 구성 하도록 hello hello에 동일한 IPsec/IKE 정책을 같은 PowerShell 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-249">So it is possible toocreate and configure both connections with hello same IPsec/IKE policy in hello same PowerShell session.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> <span data-ttu-id="c9979-250">연결에 IPsec/IKE 정책을 지정 되 면 hello Azure VPN 게이트웨이 보내거나 지정 된 암호화 알고리즘 및 키 길이 특정 연결에 IPsec/IKE 제안 hello 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-250">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="c9979-251">확인 한 다음 있는지 hello IPsec 정책을 모두 연결 된 hello 동일 하지만, 그렇지 않으면 VNet 대 VNet 연결을 설정 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-251">Make sure hello IPsec policies for both connections are hello same, otherwise the VNet-to-VNet connection will not establish.</span></span>

<span data-ttu-id="c9979-252">다음이 단계를 완료 한 후 몇 분 안에 hello 연결이 설정 되 고 hello hello 시작 부분에 표시 된 대로 네트워크 토폴로지를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-252">After completing these steps, hello connection is established in a few minutes, and you will have hello following network topology as shown in hello beginning:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <span data-ttu-id="c9979-254"><a name ="managepolicy"></a>5부 - 연결에 대한 IPsec/IKE 정책 업데이트</span><span class="sxs-lookup"><span data-stu-id="c9979-254"><a name ="managepolicy"></a>Part 5 - Update IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="c9979-255">표시 하는 hello 마지막 섹션 toomanage 기존 S2S 또는 VNet 대 VNet 연결에 대 한 IPsec/IKE 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-255">hello last section shows you how toomanage IPsec/IKE policy for an existing S2S or VNet-to-VNet connection.</span></span> <span data-ttu-id="c9979-256">아래 hello 연습 hello 다음 연결에 대 한 작업을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-256">hello exercise below walks you through hello following operations on a connection:</span></span>

1. <span data-ttu-id="c9979-257">연결의 IPsec/IKE 정책 hello를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-257">Show hello IPsec/IKE policy of a connection</span></span>
2. <span data-ttu-id="c9979-258">추가 하거나 hello IPsec/IKE 정책 tooa 연결 업데이트</span><span class="sxs-lookup"><span data-stu-id="c9979-258">Add or update hello IPsec/IKE policy tooa connection</span></span>
3. <span data-ttu-id="c9979-259">연결에서 hello IPsec/IKE 정책 제거</span><span class="sxs-lookup"><span data-stu-id="c9979-259">Remove hello IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="c9979-260">hello 동일한 단계 적용 tooboth S2S 및 VNet 대 VNet 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-260">hello same steps apply tooboth S2S and VNet-to-VNet connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c9979-261">IPsec/IKE 정책은 *표준* 및 *고성능* 경로 기반 VPN 게이트웨이에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-261">IPsec/IKE policy is supported on *Standard* and *HighPerformance* route-based VPN gateways only.</span></span> <span data-ttu-id="c9979-262">Hello 기본 게이트웨이 SKU 또는 hello 정책 기반 VPN 게이트웨이 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-262">It does not work on hello Basic gateway SKU or hello policy-based VPN gateway.</span></span>

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a><span data-ttu-id="c9979-263">1. 연결의 IPsec/IKE 정책 hello를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-263">1. Show hello IPsec/IKE policy of a connection</span></span>

<span data-ttu-id="c9979-264">다음 예제는 hello tooget 연결에 구성 된 IPsec/IKE 정책 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-264">hello following example shows how tooget hello IPsec/IKE policy configured on a connection.</span></span> <span data-ttu-id="c9979-265">hello 스크립트는 또한 위의 hello 연습에서 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-265">hello scripts also continue from hello exercises above.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="c9979-266">마지막 명령은 hello 되어 hello 연결에 구성 된 hello 현재 IPsec/IKE 정책을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-266">hello last command lists hello current IPsec/IKE policy configured on hello connection, if there is any.</span></span> <span data-ttu-id="c9979-267">샘플 출력 다음 hello hello 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-267">hello following sample output is for hello connection:</span></span>

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

<span data-ttu-id="c9979-268">IPsec/IKE 정책 구성 안 됨 이면 hello 명령 (PS > $connection6.policy)는 빈 반환 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-268">If there is no IPsec/IKE policy configured, hello command (PS> $connection6.policy) gets an empty return.</span></span> <span data-ttu-id="c9979-269">IPsec/IKE hello 연결에 구성 되어 있지 않습니다 이지만 사용자 지정 하는 IPsec/IKE 정책이 없는 있다는 것을 의미 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-269">It does not mean IPsec/IKE is not configured on hello connection, but that there is no custom IPsec/IKE policy.</span></span> <span data-ttu-id="c9979-270">hello 실제 연결은 온-프레미스 VPN 장치 및 hello Azure VPN 게이트웨이 간의 협상 hello 기본 정책이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-270">hello actual connection uses hello default policy negotiated between your on-premises VPN device and hello Azure VPN gateway.</span></span>

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a><span data-ttu-id="c9979-271">2. 연결에 대한 IPsec/IKE 정책 추가 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="c9979-271">2. Add or update an IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="c9979-272">hello 단계 tooadd 새 정책 또는 업데이트 한 연결에서 기존 정책을 사용 하면 동일한 hello: 새 정책을 만든 다음 hello 새 정책 toohello 연결을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-272">hello steps tooadd a new policy or update an existing policy on a connection are hello same: create a new policy then apply hello new policy toohello connection.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

<span data-ttu-id="c9979-273">tooenable 때 tooan 연결 온-프레미스 정책 기반 VPN 장치를 "UsePolicyBasedTrafficSelectors" hello 추가 "-UsePolicyBaseTrafficSelectors" 매개 변수 toohello cmdlet 너무 설정 또는 $False toodisable hello 옵션:</span><span class="sxs-lookup"><span data-stu-id="c9979-273">tooenable "UsePolicyBasedTrafficSelectors" when connecting tooan on-premises policy-based VPN device, add hello "-UsePolicyBaseTrafficSelectors" parameter toohello cmdlet, or set it too$False toodisable hello option:</span></span>

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

<span data-ttu-id="c9979-274">Hello 연결을 가져올 수 있습니다 hello 정책이 업데이트 되는 경우 다시 toocheck 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-274">You can get hello connection again toocheck if hello policy is updated.</span></span>

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="c9979-275">다음 예제는 hello와 같이 hello 마지막 줄의 hello 출력을 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-275">You should see hello output from hello last line, as shown in hello following example:</span></span>

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

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a><span data-ttu-id="c9979-276">3. 연결에서 IPsec/IKE 정책 제거</span><span class="sxs-lookup"><span data-stu-id="c9979-276">3. Remove an IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="c9979-277">Hello Azure VPN 게이트웨이 백 toohello 되돌립니다 연결에서 사용자 지정 정책 hello를 제거 하면 [기본 IPsec/IKE 제안 목록을](vpn-gateway-about-vpn-devices.md) 및 다시 온-프레미스 VPN 장치와 재협상 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-277">Once you remove hello custom policy from a connection, hello Azure VPN gateway reverts back toohello [default list of IPsec/IKE proposals](vpn-gateway-about-vpn-devices.md) and renegotiates again with your on-premises VPN device.</span></span>

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

<span data-ttu-id="c9979-278">사용할 수 있습니다 hello 정책 hello 연결에서 제거 된 경우 동일한 스크립트 toocheck hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-278">You can use hello same script toocheck if hello policy has been removed from hello connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9979-279">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c9979-279">Next steps</span></span>

<span data-ttu-id="c9979-280">정책 기반 트래픽 선택기에 대한 자세한 내용은 [여러 온-프레미스 정책 기반 VPN 장치 연결](vpn-gateway-connect-multiple-policybased-rm-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9979-280">See [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) for more details regarding policy-based traffic selectors.</span></span>

<span data-ttu-id="c9979-281">연결이 완료 되 면 가상 컴퓨터 tooyour 가상 네트워크를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c9979-281">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="c9979-282">단계는 [가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c9979-282">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
