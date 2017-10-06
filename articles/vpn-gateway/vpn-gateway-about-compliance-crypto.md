---
title: "aaaAbout 암호화 요구 사항 및 Azure VPN 게이트웨이 | Microsoft Docs"
description: "이 문서에서는 암호화 요구 사항 및 Azure VPN Gateway에 대해 알아봅니다."
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
ms.date: 05/22/2017
ms.author: yushwang
ms.openlocfilehash: af5f14d66beeea5316218f9788c4ad7876826162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a><span data-ttu-id="7119e-103">암호화 요구 사항 및 Azure VPN Gateway 정보</span><span class="sxs-lookup"><span data-stu-id="7119e-103">About cryptographic requirements and Azure VPN gateways</span></span>

<span data-ttu-id="7119e-104">이 문서에서는 Azure VPN 게이트웨이 toosatisfy 크로스-프레미스 S2S VPN 터널 및 Azure 내에서 VNet 대 VNet 연결을 모두에 대 한 암호화 요구 사항을 구성할 수 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7119e-104">This article discusses how you can configure Azure VPN gateways toosatisfy your cryptographic requirements for both cross-premises S2S VPN tunnels and VNet-to-VNet connections within Azure.</span></span> 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a><span data-ttu-id="7119e-105">Azure VPN Gateway에 대한 IPsec 및 IKE 정책 매개 변수 정보</span><span class="sxs-lookup"><span data-stu-id="7119e-105">About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="7119e-106">IPsec 및 IKE 프로토콜 표준은 다양하게 결합된 다양한 암호화 알고리즘을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7119e-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="7119e-107">고객이 특정 조합의 암호화 알고리즘 및 매개 변수를 요청하지 않으면 Azure VPN Gateway에서 기본 제안 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7119e-107">If customers do not request a specific combination of cryptographic algorithms and parameters, Azure VPN gateways use a set of default proposals.</span></span> <span data-ttu-id="7119e-108">hello 기본 정책 집합 기본 구성에 다양 한 범위의-타사 VPN 장치와 상호 운용성 toomaximize을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7119e-108">hello default policy sets were chosen toomaximize interoperability with a wide range of third-party VPN devices in default configurations.</span></span> <span data-ttu-id="7119e-109">결과적으로, hello 정책 및 hello 수가 제안 가능한 모든 조합을 사용할 수 있는 암호화 알고리즘 및 키 길이 처리할 수 없으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7119e-109">As a result, hello policies and hello number of proposals cannot cover all possible combinations of available cryptographic algorithms and key strengths.</span></span>

<span data-ttu-id="7119e-110">Azure VPN 게이트웨이 hello 문서에 나열 된에 설정 된 기본 정책과 hello: [에 대 한 VPN 장치 및 사이트 간 VPN 게이트웨이 연결에 대 한 IPsec/IKE 매개 변수](vpn-gateway-about-vpn-devices.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7119e-110">hello default policy set for Azure VPN gateway is listed in hello document: [About VPN devices and IPsec/IKE parameters for Site-to-Site VPN Gateway connections](vpn-gateway-about-vpn-devices.md).</span></span>

## <a name="cryptographic-requirements"></a><span data-ttu-id="7119e-111">암호화 요구 사항</span><span class="sxs-lookup"><span data-stu-id="7119e-111">Cryptographic requirements</span></span>
<span data-ttu-id="7119e-112">특정 암호화 알고리즘 또는 매개 변수를 필요로 하는 통신의 경우 일반적으로 인해 toocompliance 또는 보안 요구 사항 고객 이제 정책을 구성할 수 자신의 Azure VPN 게이트웨이 toouse는 사용자 지정 IPsec/IKE 암호화 특정 알고리즘 및 키 길이 보다는 hello Azure 기본 정책 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="7119e-112">For communications that require specific cryptographic algorithms or parameters, typically due toocompliance or security requirements, customers can now configure their Azure VPN gateways toouse a custom IPsec/IKE policy with specific cryptographic algorithms and key strengths, rather than hello Azure default policy sets.</span></span>

<span data-ttu-id="7119e-113">고객 toospecify 더 강력한 그룹 toobe 그룹 14 (2048 비트), 그룹 24 (2048 비트 MODP 그룹) 또는 (elliptic ECP 같은 IKE에 사용 해야 할 수 있지만 Azure VPN 게이트웨이에 대 한 hello IKEv2 주 모드 정책을 Diffie-hellman 그룹 2 (1024 비트)를 활용 하는 예를 들어 곡선을 그룹) 256 / 384 비트 (각각 그룹이 19, 그룹 20).</span><span class="sxs-lookup"><span data-stu-id="7119e-113">For example, hello IKEv2 main mode policies for Azure VPN gateways utilize only Diffie-Hellman Group 2 (1024 bits), whereas customers may need toospecify stronger groups toobe used in IKE, such as Group 14 (2048-bit), Group 24 (2048-bit MODP Group), or ECP (elliptic curve groups) 256 or 384 bit (Group 19 and Group 20, respectively).</span></span> <span data-ttu-id="7119e-114">이와 비슷한 요구 사항을 tooIPsec 빠른 모드 정책을 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7119e-114">Similar requirements apply tooIPsec quick mode policies as well.</span></span>

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a><span data-ttu-id="7119e-115">Azure VPN Gateway의 사용자 지정 IPsec/IKE 정책</span><span class="sxs-lookup"><span data-stu-id="7119e-115">Custom IPsec/IKE policy with Azure VPN gateways</span></span>
<span data-ttu-id="7119e-116">이제 Azure VPN Gateway에서 연결별 사용자 지정 IPsec/IKE 정책을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7119e-116">Azure VPN gateways now support per-connection, custom IPsec/IKE policy.</span></span> <span data-ttu-id="7119e-117">사이트 간 또는 VNet 대 VNet 연결을 선택할 수 있습니다는 암호화 알고리즘의 특정 조합을 IPsec과 IKE에 대 한 원하는 hello 키 강도 가진 hello 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="7119e-117">For a Site-to-Site or VNet-to-VNet connection, you can choose a specific combination of cryptographic algorithms for IPsec and IKE with hello desired key strength, as shown in hello following example:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

<span data-ttu-id="7119e-119">IPsec/IKE 정책을 만들고 tooa 기존 또는 새 연결을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7119e-119">You can create an IPsec/IKE policy and apply tooa new or existing connection.</span></span> 

### <a name="workflow"></a><span data-ttu-id="7119e-120">워크플로</span><span class="sxs-lookup"><span data-stu-id="7119e-120">Workflow</span></span>

1. <span data-ttu-id="7119e-121">다른 방법 toodocuments에 설명 된 대로 hello 가상 네트워크, VPN 게이트웨이 또는 연결 토폴로지에 대 한 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="7119e-121">Create hello virtual networks, VPN gateways, or local network gateways for your connectivity topology as described in other how-toodocuments</span></span>
2. <span data-ttu-id="7119e-122">IPsec/IKE 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="7119e-122">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="7119e-123">S2S 또는 VNet 대 VNet 연결을 만들 때 hello 정책을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7119e-123">You can apply hello policy when you create a S2S or VNet-to-VNet connection</span></span>
4. <span data-ttu-id="7119e-124">Hello 연결을 이미 만든 경우에 적용 하거나 hello 정책 tooan 기존 연결을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7119e-124">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>


## <a name="ipsecike-policy-faq"></a><span data-ttu-id="7119e-125">IPsec/IKE 정책 FAQ</span><span class="sxs-lookup"><span data-stu-id="7119e-125">IPsec/IKE policy FAQ</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a><span data-ttu-id="7119e-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7119e-126">Next steps</span></span>
<span data-ttu-id="7119e-127">연결에 대한 사용자 지정 IPsec/IKE 정책을 구성하는 방법에 대한 단계별 지침은 [IPsec/IKE 정책 구성](vpn-gateway-ipsecikepolicy-rm-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7119e-127">See [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) for step-by-step instructions on configuring custom IPsec/IKE policy on a connection.</span></span>

<span data-ttu-id="7119e-128">참고 항목 [여러 정책 기반 VPN 장치 연결](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn hello UsePolicyBasedTrafficSelectors 옵션에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7119e-128">See also [Connect multiple policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn more about hello UsePolicyBasedTrafficSelectors option.</span></span>
