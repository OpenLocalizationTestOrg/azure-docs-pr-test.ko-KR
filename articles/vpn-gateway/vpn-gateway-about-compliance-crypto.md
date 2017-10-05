---
title: "암호화 요구 사항 및 Azure VPN Gateway 정보 | Microsoft Docs"
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
ms.openlocfilehash: c789e6c278fc0c58c64f5d96e57f94aee5a6cefc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a><span data-ttu-id="ac39d-103">암호화 요구 사항 및 Azure VPN Gateway 정보</span><span class="sxs-lookup"><span data-stu-id="ac39d-103">About cryptographic requirements and Azure VPN gateways</span></span>

<span data-ttu-id="ac39d-104">이 문서에서는 Azure 내에서 크로스-프레미스 S2S VPN 터널 및 VNet 간 연결 모두에 대한 암호화 요구 사항을 충족하도록 Azure VPN Gateway를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ac39d-104">This article discusses how you can configure Azure VPN gateways to satisfy your cryptographic requirements for both cross-premises S2S VPN tunnels and VNet-to-VNet connections within Azure.</span></span> 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a><span data-ttu-id="ac39d-105">Azure VPN Gateway에 대한 IPsec 및 IKE 정책 매개 변수 정보</span><span class="sxs-lookup"><span data-stu-id="ac39d-105">About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="ac39d-106">IPsec 및 IKE 프로토콜 표준은 다양하게 결합된 다양한 암호화 알고리즘을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ac39d-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="ac39d-107">고객이 특정 조합의 암호화 알고리즘 및 매개 변수를 요청하지 않으면 Azure VPN Gateway에서 기본 제안 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ac39d-107">If customers do not request a specific combination of cryptographic algorithms and parameters, Azure VPN gateways use a set of default proposals.</span></span> <span data-ttu-id="ac39d-108">기본 정책 집합은 기본 구성에서 광범위한 타사 VPN 장치와의 상호 운용성을 극대화하기 위해 선택되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ac39d-108">The default policy sets were chosen to maximize interoperability with a wide range of third-party VPN devices in default configurations.</span></span> <span data-ttu-id="ac39d-109">따라서 정책 및 제안 수에서 사용 가능한 암호화 알고리즘 및 키 길이의 가능한 모든 조합을 다룰 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ac39d-109">As a result, the policies and the number of proposals cannot cover all possible combinations of available cryptographic algorithms and key strengths.</span></span>

<span data-ttu-id="ac39d-110">Azure VPN Gateway에 대한 기본 정책 집합은 [사이트 간 VPN Gateway 연결에 대한 VPN 장치 및 IPsec/IKE 매개 변수 정보](vpn-gateway-about-vpn-devices.md) 문서에 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac39d-110">The default policy set for Azure VPN gateway is listed in the document: [About VPN devices and IPsec/IKE parameters for Site-to-Site VPN Gateway connections](vpn-gateway-about-vpn-devices.md).</span></span>

## <a name="cryptographic-requirements"></a><span data-ttu-id="ac39d-111">암호화 요구 사항</span><span class="sxs-lookup"><span data-stu-id="ac39d-111">Cryptographic requirements</span></span>
<span data-ttu-id="ac39d-112">특정 암호화 알고리즘 또는 매개 변수가 필요한 통신의 경우, 일반적으로 규정 준수 또는 보안 요구 사항으로 인해 고객은 이제 Azure 기본 정책 집합 대신 특정 암호화 알고리즘 및 키 강도와 함께 사용자 지정 IPsec/IKE 정책을 사용하도록 Azure VPN Gateway를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac39d-112">For communications that require specific cryptographic algorithms or parameters, typically due to compliance or security requirements, customers can now configure their Azure VPN gateways to use a custom IPsec/IKE policy with specific cryptographic algorithms and key strengths, rather than the Azure default policy sets.</span></span>

<span data-ttu-id="ac39d-113">예를 들어 Azure VPN Gateway에 대한 IKEv2 기본 모드 정책은 Diffie-Hellman Group 2(1024비트)만 활용하는 반면, 고객은 Group 14(2048비트), Group 24(2048비트 MODP Group), ECP(elliptic curve groups) 256 또는 384비트(각각 Group 19 및 Group 20) 등 IKE에서 사용할 더 강력한 그룹을 지정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac39d-113">For example, the IKEv2 main mode policies for Azure VPN gateways utilize only Diffie-Hellman Group 2 (1024 bits), whereas customers may need to specify stronger groups to be used in IKE, such as Group 14 (2048-bit), Group 24 (2048-bit MODP Group), or ECP (elliptic curve groups) 256 or 384 bit (Group 19 and Group 20, respectively).</span></span> <span data-ttu-id="ac39d-114">유사한 요구 사항은 IPsec 빠른 모드 정책에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac39d-114">Similar requirements apply to IPsec quick mode policies as well.</span></span>

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a><span data-ttu-id="ac39d-115">Azure VPN Gateway의 사용자 지정 IPsec/IKE 정책</span><span class="sxs-lookup"><span data-stu-id="ac39d-115">Custom IPsec/IKE policy with Azure VPN gateways</span></span>
<span data-ttu-id="ac39d-116">이제 Azure VPN Gateway에서 연결별 사용자 지정 IPsec/IKE 정책을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ac39d-116">Azure VPN gateways now support per-connection, custom IPsec/IKE policy.</span></span> <span data-ttu-id="ac39d-117">아래 예제에 나와 있는 것처럼 사이트 간 또는 VNet 간 연결에 대해 원하는 키 강도를 가진 IPsec 및 IKE에 대한 특정 암호화 알고리즘 조합을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac39d-117">For a Site-to-Site or VNet-to-VNet connection, you can choose a specific combination of cryptographic algorithms for IPsec and IKE with the desired key strength, as shown in the following example:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

<span data-ttu-id="ac39d-119">IPsec/IKE 정책을 만들어 새 연결 또는 기존 연결에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac39d-119">You can create an IPsec/IKE policy and apply to a new or existing connection.</span></span> 

### <a name="workflow"></a><span data-ttu-id="ac39d-120">워크플로</span><span class="sxs-lookup"><span data-stu-id="ac39d-120">Workflow</span></span>

1. <span data-ttu-id="ac39d-121">다른 방법 문서에 설명된 대로 연결 토폴로지에 대한 가상 네트워크, VPN Gateway 또는 로컬 네트워크 게이트웨이 만들기</span><span class="sxs-lookup"><span data-stu-id="ac39d-121">Create the virtual networks, VPN gateways, or local network gateways for your connectivity topology as described in other how-to documents</span></span>
2. <span data-ttu-id="ac39d-122">IPsec/IKE 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="ac39d-122">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="ac39d-123">S2S 또는 VNet 간 연결을 만들 때 정책을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac39d-123">You can apply the policy when you create a S2S or VNet-to-VNet connection</span></span>
4. <span data-ttu-id="ac39d-124">연결이 이미 생성된 경우 기존 연결에 정책을 적용하거나 업데이트할 수 있음</span><span class="sxs-lookup"><span data-stu-id="ac39d-124">If the connection is already created, you can apply or update the policy to an existing connection</span></span>


## <a name="ipsecike-policy-faq"></a><span data-ttu-id="ac39d-125">IPsec/IKE 정책 FAQ</span><span class="sxs-lookup"><span data-stu-id="ac39d-125">IPsec/IKE policy FAQ</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a><span data-ttu-id="ac39d-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ac39d-126">Next steps</span></span>
<span data-ttu-id="ac39d-127">연결에 대한 사용자 지정 IPsec/IKE 정책을 구성하는 방법에 대한 단계별 지침은 [IPsec/IKE 정책 구성](vpn-gateway-ipsecikepolicy-rm-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac39d-127">See [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) for step-by-step instructions on configuring custom IPsec/IKE policy on a connection.</span></span>

<span data-ttu-id="ac39d-128">또한 UsePolicyBasedTrafficSelectors 옵션에 대한 자세한 내용은 [여러 정책 기반 VPN 장치 연결](vpn-gateway-connect-multiple-policybased-rm-ps.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac39d-128">See also [Connect multiple policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) to learn more about the UsePolicyBasedTrafficSelectors option.</span></span>