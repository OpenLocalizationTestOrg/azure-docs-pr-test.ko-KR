---
title: "Cisco ASA 장치 tooAzure VPN 게이트웨이 연결-aaaSample 구성 | Microsoft Docs"
description: "이 문서에서는 Cisco ASA 장치 tooAzure VPN 게이트웨이 연결에 대 한 샘플 구성 합니다."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: dad13e02afe8dad2379db750eb09602e08e8ea99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a><span data-ttu-id="9f2f2-103">샘플 구성: Cisco ASA 장치(IKEv2/BGP 아님)</span><span class="sxs-lookup"><span data-stu-id="9f2f2-103">Sample configuration: Cisco ASA device (IKEv2/no BGP)</span></span>
<span data-ttu-id="9f2f2-104">이 문서에서는 Cisco ASA 장치 tooAzure VPN 게이트웨이 연결에 대 한 샘플 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-104">This article provides sample configurations for Cisco ASA devices connecting tooAzure VPN gateways.</span></span>

## <a name="device-at-a-glance"></a><span data-ttu-id="9f2f2-105">장치 개요</span><span class="sxs-lookup"><span data-stu-id="9f2f2-105">Device at a glance</span></span>

|                        |                                   |
| ---                    | ---                               |
| <span data-ttu-id="9f2f2-106">장치 공급 업체</span><span class="sxs-lookup"><span data-stu-id="9f2f2-106">Device vendor</span></span>          | <span data-ttu-id="9f2f2-107">시스코</span><span class="sxs-lookup"><span data-stu-id="9f2f2-107">Cisco</span></span>                             |
| <span data-ttu-id="9f2f2-108">장치 모델</span><span class="sxs-lookup"><span data-stu-id="9f2f2-108">Device model</span></span>           | <span data-ttu-id="9f2f2-109">ASA(적응 보안 어플라이언스)</span><span class="sxs-lookup"><span data-stu-id="9f2f2-109">ASA (Adaptive Security Appliance)</span></span> |
| <span data-ttu-id="9f2f2-110">대상 버전</span><span class="sxs-lookup"><span data-stu-id="9f2f2-110">Target version</span></span>         | <span data-ttu-id="9f2f2-111">8.4+</span><span class="sxs-lookup"><span data-stu-id="9f2f2-111">8.4+</span></span>                              |
| <span data-ttu-id="9f2f2-112">테스트 모델</span><span class="sxs-lookup"><span data-stu-id="9f2f2-112">Tested model</span></span>           | <span data-ttu-id="9f2f2-113">ASA 5505</span><span class="sxs-lookup"><span data-stu-id="9f2f2-113">ASA 5505</span></span>                          |
| <span data-ttu-id="9f2f2-114">테스트 버전</span><span class="sxs-lookup"><span data-stu-id="9f2f2-114">Tested version</span></span>         | <span data-ttu-id="9f2f2-115">9.2</span><span class="sxs-lookup"><span data-stu-id="9f2f2-115">9.2</span></span>                               |
| <span data-ttu-id="9f2f2-116">IKE 버전</span><span class="sxs-lookup"><span data-stu-id="9f2f2-116">IKE version</span></span>            | <span data-ttu-id="9f2f2-117">**IKEv2**</span><span class="sxs-lookup"><span data-stu-id="9f2f2-117">**IKEv2**</span></span>                         |
| <span data-ttu-id="9f2f2-118">BGP</span><span class="sxs-lookup"><span data-stu-id="9f2f2-118">BGP</span></span>                    | <span data-ttu-id="9f2f2-119">**아니요**</span><span class="sxs-lookup"><span data-stu-id="9f2f2-119">**No**</span></span>                            |
| <span data-ttu-id="9f2f2-120">Azure VPN 게이트웨이 유형</span><span class="sxs-lookup"><span data-stu-id="9f2f2-120">Azure VPN gateway type</span></span> | <span data-ttu-id="9f2f2-121">**경로 기반** VPN 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="9f2f2-121">**Route-based** VPN gateway</span></span>       |
|                        |                                   |

> [!NOTE]
> 1. <span data-ttu-id="9f2f2-122">Cisco ASA 장치 tooan Azure 연결 하는 hello 구성 아래 **경로 기반** 에 설명 된 대로 "UserPolicyBasedTrafficSelectors" 옵션을 사용자 지정 IPsec/IKE 정책을 사용 하 여 VPN 게이트웨이 [이 여기서](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9f2f2-122">hello configuration below connects a Cisco ASA device tooan Azure **route-based** VPN gateway using custom IPsec/IKE policy with "UserPolicyBasedTrafficSelectors" option, as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>
> 2. <span data-ttu-id="9f2f2-123">ASA 장치 toouse 필요 **IKEv2** 액세스 목록 기반 구성을 사용 하 여 VTI 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-123">It requires ASA devices toouse **IKEv2** with access-list-based configurations, not VTI-based.</span></span>
> 3. <span data-ttu-id="9f2f2-124">VPN 장치 공급 업체 사양을 tooensure hello 정책은 온-프레미스 VPN 장치 지원에 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-124">Please consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span>

## <a name="vpn-device-requirements"></a><span data-ttu-id="9f2f2-125">VPN 장치 요구 사항</span><span class="sxs-lookup"><span data-stu-id="9f2f2-125">VPN device requirements</span></span>
<span data-ttu-id="9f2f2-126">Azure VPN 게이트웨이 도구 모음 tooestablish S2S VPN 터널에 대 한 표준의 IPsec/IKE 프로토콜을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-126">Azure VPN gateways use standard IPsec/IKE protocol suites tooestablish S2S VPN tunnels.</span></span> <span data-ttu-id="9f2f2-127">너무 참조[에 대 한 VPN 장치](vpn-gateway-about-vpn-devices.md) hello에 대 한 자세한 IPsec/IKE 프로토콜 매개 변수 및 Azure VPN 게이트웨이에 대 한 기본 암호화 알고리즘입니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-127">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="9f2f2-128">에 설명 된 대로 암호화 알고리즘 및 키 길이 특정 연결에 대 한 정확한 조합 hello를 선택적으로 지정할 수 [암호화 요구 사항에 대 한](vpn-gateway-about-compliance-crypto.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-128">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span> <span data-ttu-id="9f2f2-129">암호화 알고리즘 및 키 길이의 특정 조합을 선택 하는 경우 해당 사양을 hello를 사용 하 여 VPN 장치에 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-129">If you select a specific combination of cryptographic algorithms and key strengths, please make sure you use hello corresponding specifications on your VPN devices.</span></span>

## <a name="single-vpn-tunnel"></a><span data-ttu-id="9f2f2-130">단일 VPN 터널</span><span class="sxs-lookup"><span data-stu-id="9f2f2-130">Single VPN tunnel</span></span>
<span data-ttu-id="9f2f2-131">이 토폴로지는 Azure VPN 게이트웨이와 온-프레미스 VPN 장치 간에 단일 S2S VPN 터널로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-131">This topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="9f2f2-132">필요에 따라 hello VPN 터널에서 BGP를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-132">You can optionally configure BGP across hello VPN tunnel.</span></span>

![단일 터널](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

<span data-ttu-id="9f2f2-134">너무 참조[단일 터널 설치](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) 단계별 지침 toobuild hello Azure 구성 하세요.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-134">Refer too[Single tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) for detailed, step-by-step instructions toobuild hello Azure configurations.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="9f2f2-135">네트워크 및 VPN 게이트웨이 정보</span><span class="sxs-lookup"><span data-stu-id="9f2f2-135">Network and VPN gateway information</span></span>
<span data-ttu-id="9f2f2-136">이 여기서는이 샘플 hello에 대 한 hello 매개 변수를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-136">This section list hello parameters for hello this sample.</span></span>

| <span data-ttu-id="9f2f2-137">**매개 변수**</span><span class="sxs-lookup"><span data-stu-id="9f2f2-137">**Parameter**</span></span>                | <span data-ttu-id="9f2f2-138">**값**</span><span class="sxs-lookup"><span data-stu-id="9f2f2-138">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="9f2f2-139">VNet 주소 접두사</span><span class="sxs-lookup"><span data-stu-id="9f2f2-139">VNet address prefixes</span></span>        | <span data-ttu-id="9f2f2-140">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="9f2f2-140">10.11.0.0/16</span></span><br><span data-ttu-id="9f2f2-141">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="9f2f2-141">10.12.0.0/16</span></span> |
| <span data-ttu-id="9f2f2-142">Azure VPN 게이트웨이 IP</span><span class="sxs-lookup"><span data-stu-id="9f2f2-142">Azure VPN gateway IP</span></span>         | <span data-ttu-id="9f2f2-143">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="9f2f2-143">Azure_Gateway_Public_IP</span></span>      |
| <span data-ttu-id="9f2f2-144">온-프레미스 주소 접두사</span><span class="sxs-lookup"><span data-stu-id="9f2f2-144">On-premises address prefixes</span></span> | <span data-ttu-id="9f2f2-145">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="9f2f2-145">10.51.0.0/16</span></span><br><span data-ttu-id="9f2f2-146">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="9f2f2-146">10.52.0.0/16</span></span> |
| <span data-ttu-id="9f2f2-147">온-프레미스 VPN 장치 IP</span><span class="sxs-lookup"><span data-stu-id="9f2f2-147">On-premises VPN device IP</span></span>    | <span data-ttu-id="9f2f2-148">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="9f2f2-148">OnPrem_Device_Public_IP</span></span>     |
| <span data-ttu-id="9f2f2-149">*VNet BGP ASN</span><span class="sxs-lookup"><span data-stu-id="9f2f2-149">*VNet BGP ASN</span></span>                | <span data-ttu-id="9f2f2-150">65010</span><span class="sxs-lookup"><span data-stu-id="9f2f2-150">65010</span></span>                        |
| <span data-ttu-id="9f2f2-151">*Azure BGP 피어 IP</span><span class="sxs-lookup"><span data-stu-id="9f2f2-151">*Azure BGP peer IP</span></span>           | <span data-ttu-id="9f2f2-152">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="9f2f2-152">10.12.255.30</span></span>                 |
| <span data-ttu-id="9f2f2-153">*온-프레미스 BGP ASN</span><span class="sxs-lookup"><span data-stu-id="9f2f2-153">*On-premises BGP ASN</span></span>         | <span data-ttu-id="9f2f2-154">65050</span><span class="sxs-lookup"><span data-stu-id="9f2f2-154">65050</span></span>                        |
| <span data-ttu-id="9f2f2-155">*온-프레미스 BGP 피어 IP</span><span class="sxs-lookup"><span data-stu-id="9f2f2-155">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="9f2f2-156">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="9f2f2-156">10.52.255.254</span></span>                |
|                              |                              |

* <span data-ttu-id="9f2f2-157">(*) BGP에 대한 선택적 매개 변수만 해당</span><span class="sxs-lookup"><span data-stu-id="9f2f2-157">(*) Optional parameters for BGP only.</span></span>

### <a name="ipsecike-policy--parameters"></a><span data-ttu-id="9f2f2-158">IPsec/IKE 정책 및 매개 변수</span><span class="sxs-lookup"><span data-stu-id="9f2f2-158">IPsec/IKE policy & parameters</span></span>

<span data-ttu-id="9f2f2-159">hello 아래 표에 hello IPsec/IKE 알고리즘 및 hello 샘플에 사용 된 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-159">hello table below lists hello IPsec/IKE algorithms and parameters used in hello sample.</span></span> <span data-ttu-id="9f2f2-160">프로그램 VPN 장치 사양 toomake 위에 나열 된 모든 알고리즘 VPN 장치 모델와 펌웨어 버전에서 사용할 수 있는지를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-160">Please consult your VPN device specifications toomake sure all algorithms listed above are supported by your VPN device models and firmware versions.</span></span>

| <span data-ttu-id="9f2f2-161">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="9f2f2-161">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="9f2f2-162">**값**</span><span class="sxs-lookup"><span data-stu-id="9f2f2-162">**Value**</span></span>                            |
| ---              | ---                                  |
| <span data-ttu-id="9f2f2-163">IKEv2 암호화</span><span class="sxs-lookup"><span data-stu-id="9f2f2-163">IKEv2 Encryption</span></span> | <span data-ttu-id="9f2f2-164">AES256</span><span class="sxs-lookup"><span data-stu-id="9f2f2-164">AES256</span></span>                               |
| <span data-ttu-id="9f2f2-165">IKEv2 무결성</span><span class="sxs-lookup"><span data-stu-id="9f2f2-165">IKEv2 Integrity</span></span>  | <span data-ttu-id="9f2f2-166">SHA384</span><span class="sxs-lookup"><span data-stu-id="9f2f2-166">SHA384</span></span>                               |
| <span data-ttu-id="9f2f2-167">DH 그룹</span><span class="sxs-lookup"><span data-stu-id="9f2f2-167">DH Group</span></span>         | <span data-ttu-id="9f2f2-168">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="9f2f2-168">DHGroup24</span></span>                            |
| <span data-ttu-id="9f2f2-169">IPsec 암호화</span><span class="sxs-lookup"><span data-stu-id="9f2f2-169">IPsec Encryption</span></span> | <span data-ttu-id="9f2f2-170">AES256</span><span class="sxs-lookup"><span data-stu-id="9f2f2-170">AES256</span></span>                               |
| <span data-ttu-id="9f2f2-171">IPsec 무결성</span><span class="sxs-lookup"><span data-stu-id="9f2f2-171">IPsec Integrity</span></span>  | <span data-ttu-id="9f2f2-172">SHA1</span><span class="sxs-lookup"><span data-stu-id="9f2f2-172">SHA1</span></span>                                 |
| <span data-ttu-id="9f2f2-173">PFS 그룹</span><span class="sxs-lookup"><span data-stu-id="9f2f2-173">PFS Group</span></span>        | <span data-ttu-id="9f2f2-174">PFS24</span><span class="sxs-lookup"><span data-stu-id="9f2f2-174">PFS24</span></span>                                |
| <span data-ttu-id="9f2f2-175">QM SA 수명</span><span class="sxs-lookup"><span data-stu-id="9f2f2-175">QM SA Lifetime</span></span>   | <span data-ttu-id="9f2f2-176">7200초</span><span class="sxs-lookup"><span data-stu-id="9f2f2-176">7200 seconds</span></span>                         |
| <span data-ttu-id="9f2f2-177">트래픽 선택기</span><span class="sxs-lookup"><span data-stu-id="9f2f2-177">Traffic Selector</span></span> | <span data-ttu-id="9f2f2-178">UsePolicyBasedTrafficSelectors $True</span><span class="sxs-lookup"><span data-stu-id="9f2f2-178">UsePolicyBasedTrafficSelectors $True</span></span> |
| <span data-ttu-id="9f2f2-179">미리 공유한 키</span><span class="sxs-lookup"><span data-stu-id="9f2f2-179">Pre-Shared Key</span></span>   | <span data-ttu-id="9f2f2-180">PreSharedKey</span><span class="sxs-lookup"><span data-stu-id="9f2f2-180">PreSharedKey</span></span>                         |
|                  |                                      |

- <span data-ttu-id="9f2f2-181">(*) 일부 장치에서 IPsec 무결성은 GCM-AES가 IPsec 암호화 알고리즘으로 사용되는 경우 "null"이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-181">(*) On some device, IPsec integrity must be "null" if GCM-AES is used as IPsec encryption algorithm.</span></span>

### <a name="device-notes"></a><span data-ttu-id="9f2f2-182">장치 정보</span><span class="sxs-lookup"><span data-stu-id="9f2f2-182">Device notes</span></span>

>[!NOTE]
>
> 1. <span data-ttu-id="9f2f2-183">IKEv2 지원에는 ASA 버전 8.4 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-183">IKEv2 support requires ASA version 8.4 and above.</span></span>
> 2. <span data-ttu-id="9f2f2-184">더 높은 DH 및 PFS 그룹 지원(그룹 5 이외)에는 ASA 버전 9.x가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-184">Higher DH and PFS group support (beyond Group 5) requires ASA version 9.x.</span></span>
> 3. <span data-ttu-id="9f2f2-185">SHA-256, SHA-384, SHA-512로 AES GCM 및 IPsec 무결성을 사용하는 IPsec 암호화 지원에는 최신 ASA 하드웨어에서 ASA 버전 9.x가 필요합니다. ASA 5505, 5510, 5520, 5540, 5550, 5580은 지원되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-185">IPsec encryption with AES-GCM and IPsec integrity with SHA-256, SHA-384, SHA-512 support requires ASA version 9.x on newer ASA hardware; ASA 5505, 5510, 5520, 5540, 5550, 5580 are **not** supported.</span></span> <span data-ttu-id="9f2f2-186">(Hello 공급 업체 사양 tooconfirm 확인 하십시오.)</span><span class="sxs-lookup"><span data-stu-id="9f2f2-186">(Please check hello vendor specifications tooconfirm.)</span></span>
>


### <a name="sample-device-configurations"></a><span data-ttu-id="9f2f2-187">샘플 장치 구성</span><span class="sxs-lookup"><span data-stu-id="9f2f2-187">Sample device configurations</span></span>
<span data-ttu-id="9f2f2-188">아래의 hello 스크립트 hello 토폴로지를 기반으로 하는 샘플 구성 및 위에 나열 된 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-188">hello script below provides a sample configuration based on hello topology and parameters listed above.</span></span> <span data-ttu-id="9f2f2-189">hello S2S VPN 터널 구성의 hello 부분을 다음으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-189">hello S2S VPN tunnel configuration consists of hello following parts:</span></span>

1. <span data-ttu-id="9f2f2-190">인터페이스 및 경로</span><span class="sxs-lookup"><span data-stu-id="9f2f2-190">Interfaces & routes</span></span>
2. <span data-ttu-id="9f2f2-191">액세스 목록</span><span class="sxs-lookup"><span data-stu-id="9f2f2-191">Access lists</span></span>
3. <span data-ttu-id="9f2f2-192">IKE 정책 및 매개 변수(1단계 또는 기본 모드)</span><span class="sxs-lookup"><span data-stu-id="9f2f2-192">IKE policy and parameters (Phase 1 or Main Mode)</span></span>
4. <span data-ttu-id="9f2f2-193">IPsec 정책 및 매개 변수(2단계 또는 빠른 모드)</span><span class="sxs-lookup"><span data-stu-id="9f2f2-193">IPsec policy and parameters (Phase 2 or Quick Mode)</span></span>
5. <span data-ttu-id="9f2f2-194">기타 매개 변수(TCP MSS 고정 등)</span><span class="sxs-lookup"><span data-stu-id="9f2f2-194">Other parameters (TCP MSS clamping, etc.)</span></span>

>[!IMPORTANT] 
><span data-ttu-id="9f2f2-195">아래에 나열 된 hello 추가 구성을 완료 하 고 hello 자리 표시자 hello 실제 값으로 대체 했는지 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-195">Please make sure you complete hello additional configuration listed below and replace hello placeholders with hello actual values:</span></span>
> 
> - <span data-ttu-id="9f2f2-196">인터페이스 내부와 외부에 대해 인터페이스 구성</span><span class="sxs-lookup"><span data-stu-id="9f2f2-196">Interface configuration for both inside and outside interfaces</span></span>
> - <span data-ttu-id="9f2f2-197">내부/개인 및 외부/공용 네트워크에 대한 경로</span><span class="sxs-lookup"><span data-stu-id="9f2f2-197">Routes for your inside/private and outside/public networks</span></span>
> - <span data-ttu-id="9f2f2-198">모든 이름 및 정책 번호는 고유 hello 장치에서 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-198">Ensure all names and policy numbers are unique on hello device</span></span>
> - <span data-ttu-id="9f2f2-199">장치에서 hello 암호화 알고리즘이 지원 되는지 확인</span><span class="sxs-lookup"><span data-stu-id="9f2f2-199">Ensure hello cryptographic algorithms are supported on your device</span></span>
> - <span data-ttu-id="9f2f2-200">Hello 다음 자리 표시자 hello 실제 값으로 바꾸기</span><span class="sxs-lookup"><span data-stu-id="9f2f2-200">Replace hello following place holders with hello actual values</span></span>
>   - <span data-ttu-id="9f2f2-201">외부 인터페이스 이름: "outside"</span><span class="sxs-lookup"><span data-stu-id="9f2f2-201">Outside interface name: "outside"</span></span>
>   - <span data-ttu-id="9f2f2-202">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="9f2f2-202">Azure_Gateway_Public_IP</span></span>
>   - <span data-ttu-id="9f2f2-203">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="9f2f2-203">OnPrem_Device_Public_IP</span></span>
>   - <span data-ttu-id="9f2f2-204">IKE Pre_Shared_Key</span><span class="sxs-lookup"><span data-stu-id="9f2f2-204">IKE Pre_Shared_Key</span></span>
>   - <span data-ttu-id="9f2f2-205">VNet 및 로컬 네트워크 게이트웨이 이름(VNetName, LNGName)</span><span class="sxs-lookup"><span data-stu-id="9f2f2-205">VNet and local network gateway names (VNetName, LNGName)</span></span>
>   - <span data-ttu-id="9f2f2-206">VNet 및 온-프레미스 네트워크 주소 접두사</span><span class="sxs-lookup"><span data-stu-id="9f2f2-206">VNet and on-premises network address prefixes</span></span>
>   - <span data-ttu-id="9f2f2-207">적절한 네트워크 마스크</span><span class="sxs-lookup"><span data-stu-id="9f2f2-207">Proper netmasks</span></span>

#### <a name="sample-configuration"></a><span data-ttu-id="9f2f2-208">샘플 구성</span><span class="sxs-lookup"><span data-stu-id="9f2f2-208">Sample configuration</span></span>

```
! Sample ASA configuration for connecting tooAzure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace hello following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - hello Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with hello actual nexthop IP address
!
! (*) Must be unique names in hello device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on hello outside interface or vlan
!     > <PrivateIPAddress> on hello inside interface or vlan; e.g., 10.51.0.1/24
!     > Route tooconnect too<Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between hello ASA and hello Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding toohello <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines hello on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify hello access-list between hello Azure VNet and your on-premises network.
!       This access list defines hello IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between hello on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure hello policy number is not used
!       - integrity and prf must be hello same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as hello crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned tooyour outside interface, you must use
!         hello same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses hello access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses hello proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS too1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a><span data-ttu-id="9f2f2-209">간단한 디버깅 명령</span><span class="sxs-lookup"><span data-stu-id="9f2f2-209">Simple debugging commands</span></span>

<span data-ttu-id="9f2f2-210">디버깅 목적을 위한 일부 ASA 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-210">Here are some ASA commands for debugging purposes:</span></span>

1. <span data-ttu-id="9f2f2-211">표시 IPsec과 IKE SA hello</span><span class="sxs-lookup"><span data-stu-id="9f2f2-211">Show hello IPsec and IKE SA's</span></span>
    - <span data-ttu-id="9f2f2-212">"show crypto ipsec sa"</span><span class="sxs-lookup"><span data-stu-id="9f2f2-212">"show crypto ipsec sa"</span></span>
    - <span data-ttu-id="9f2f2-213">"show crypto ikev2 sa"</span><span class="sxs-lookup"><span data-stu-id="9f2f2-213">"show crypto ikev2 sa"</span></span>
2. <span data-ttu-id="9f2f2-214">시작 중 디버그 모드-이의 가져올 수 매우 불안정 hello 콘솔</span><span class="sxs-lookup"><span data-stu-id="9f2f2-214">Entering debug mode - this can get very noisy on hello console</span></span>
    - <span data-ttu-id="9f2f2-215">"debug crypto ikev2 platform <level>"</span><span class="sxs-lookup"><span data-stu-id="9f2f2-215">"debug crypto ikev2 platform <level>"</span></span>
    - <span data-ttu-id="9f2f2-216">"debug crypto ikev2 protocol <level>"</span><span class="sxs-lookup"><span data-stu-id="9f2f2-216">"debug crypto ikev2 protocol <level>"</span></span>
3. <span data-ttu-id="9f2f2-217">현재 구성 나열</span><span class="sxs-lookup"><span data-stu-id="9f2f2-217">List current configurations</span></span>
    - <span data-ttu-id="9f2f2-218">"실행 표시"-표시 hello hello 장치;에서 현재 구성 사용할 수 있습니다 hello hello 구성의 다양 한 하위 명령을 toolist 특정 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-218">"show run" - shows hello current configurations on hello device; you can use hello various sub-commands toolist specific parts of hello configuration.</span></span> <span data-ttu-id="9f2f2-219">예: "show run crypto", "show run access-list", "show run tunnel-group" 등</span><span class="sxs-lookup"><span data-stu-id="9f2f2-219">E.g., "show run crypto", "show run access-list", "show run tunnel-group", etc.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9f2f2-220">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9f2f2-220">Next steps</span></span>
<span data-ttu-id="9f2f2-221">참조 [크로스-프레미스 및 VNet 대 VNet 연결에 대해 액티브-액티브 VPN 게이트웨이 구성](vpn-gateway-activeactive-rm-powershell.md) 단계 tooconfigure 액티브-액티브 크로스-프레미스 및 VNet 대 VNet 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2f2-221">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

