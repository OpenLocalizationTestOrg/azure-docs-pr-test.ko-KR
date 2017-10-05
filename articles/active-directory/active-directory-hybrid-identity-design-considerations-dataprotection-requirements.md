---
title: "Azure Active Directory 하이브리드 ID 디자인 고려 사항 - 데이터 보호 요구 사항 확인 | Microsoft Docs"
description: "하이브리드 ID 솔루션을 계획할 때 이러한 요구 사항을 가장 잘 수행할 수 있도록 비즈니스에 대한 데이터 보호 요구 사항 및 사용할 수 있는 옵션을 식별합니다."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 40dc4baa-fe82-4ab6-a3e4-f36fa9dcd0df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 96bf9d4c26a22f718c29804c11681199e775f589
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="plan-for-enhancing-data-security-through-strong-identity-solution"></a><span data-ttu-id="a000c-103">강력한 ID 솔루션을 통해 데이터 보안을 향상하기 위한 계획</span><span class="sxs-lookup"><span data-stu-id="a000c-103">Plan for enhancing data security through strong identity solution</span></span>
<span data-ttu-id="a000c-104">데이터를 보호하려면 먼저 해당 데이터에 액세스할 수 있는 사용자를 식별하고 인증 및 권한 부여 기능을 제공하기 위해 이 프로세스의 일부로 시스템과 통합할 수 있는 ID 솔루션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-104">The first step to protect the data is identify who can access that data and as part of this process you need to have an identity solution that can integrates with your system to provide authentication and authorization capabilities.</span></span> <span data-ttu-id="a000c-105">인증 및 권한 부여는 종종 서로 혼동되고 역할은 오해됩니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-105">Authentication and authorization are often confused with each other and their roles misunderstood.</span></span> <span data-ttu-id="a000c-106">아래 그림에 표시된 대로 실제로 매우 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-106">In reality they are quite different, as shown in the figure below:</span></span>

![](./media/hybrid-id-design-considerations/mobile-devicemgt-lifecycle.png)

<span data-ttu-id="a000c-107">**모바일 장치 관리 수명 주기 단계**</span><span class="sxs-lookup"><span data-stu-id="a000c-107">**Mobile device management lifecycle stages**</span></span>

<span data-ttu-id="a000c-108">하이브리드 ID 솔루션을 계획할 때 이러한 요구 사항을 가장 잘 수행할 수 있도록 비즈니스에 대한 데이터 보호 요구 사항 및 사용할 수 있는 옵션을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-108">When planning your hybrid identity solution you must understand the data protection requirements for your business and which options are available to best fulfil these requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="a000c-109">데이터 보안에 대한 계획을 완료하면 [Multi-Factor Authentication 요구 사항 확인](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) 을 검토하여 Multi-Factor Authentication에 관한 선택이 이 섹션에서의 결정에 영향받지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-109">Once you finish planning for data security, review [Determine multi-factor authentication requirements](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) to ensure that your selections regarding multi-factor authentication requirements were not affected by the decisions you made in this section.</span></span>
> 
> 

## <a name="determine-data-protection-requirements"></a><span data-ttu-id="a000c-110">데이터 보호 요구 사항 결정</span><span class="sxs-lookup"><span data-stu-id="a000c-110">Determine data protection requirements</span></span>
<span data-ttu-id="a000c-111">이동성의 시대에 회사에는 대부분 공통의 목표가 있습니다. 생산성을 향상시키기 위해 온-프레미스하는 동안 또는 어디서든 원격으로 사용자가 모바일 장치에서 생산성을 높일 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-111">In the age of mobility, most companies have a common goal: enable their users to be productive on their mobile devices while on-premises or remotely from anywhere in order to increase productivity.</span></span> <span data-ttu-id="a000c-112">이것이 공통의 목적일 수 있는 반면 이러한 요구 사항이 있는 회사는 또한 회사의 데이터 보안을 유지하고 사용자의 개인 정보를 유지하기 위해 완화해야 하는 위협의 양에 관한 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-112">While this could be a common goal, companies that have such requirement will also be concern regarding the amount of threats that must be mitigated in order to keep company’s data secure and maintain user’s privacy.</span></span> <span data-ttu-id="a000c-113">각 회사는 이런 점에서 다른 요구 사항이 있을 수 있습니다. 회사가 행동하는 업계에 따라 달라질 수 있는 다른 규정 준수 규칙은 다른 설계 결정으로 이어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-113">Each company might have different requirements in this regard; different compliance rules that will vary according to which industry the company is acting will lead to different design decisions.</span></span> 

<span data-ttu-id="a000c-114">그러나 업계에 관계 없이 탐색 하 고 유효성을 검사해야 할 일부 보안 사항이 있으며 이는 다음 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-114">However, there are some security aspects that should be explored and validated, regardless of the industry, which are explained in the next section.</span></span>

## <a name="data-protection-paths"></a><span data-ttu-id="a000c-115">데이터 보호 경로</span><span class="sxs-lookup"><span data-stu-id="a000c-115">Data protection paths</span></span>
![](./media/hybrid-id-design-considerations/data-protection-paths.png)

<span data-ttu-id="a000c-116">**데이터 보호 경로**</span><span class="sxs-lookup"><span data-stu-id="a000c-116">**Data protection paths**</span></span>

<span data-ttu-id="a000c-117">위 다이어그램에서 ID 구성 요소는 데이터가 액세스되기 전에 첫번째로 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-117">In the above diagram, the identity component will be the first one to be verified before data is accessed.</span></span> <span data-ttu-id="a000c-118">그러나 이 데이터는 액세스하는 동안 다양한 상태일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-118">However, this data can be in different states during the time it was accessed.</span></span> <span data-ttu-id="a000c-119">이 다이어그램의 각 숫자는 데이터가 특정 시점에 위치할 수 있는 경로를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-119">Each number on this diagram represents a path in which data can be located at some point in time.</span></span> <span data-ttu-id="a000c-120">이러한 숫자는 아래에 설명됩니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-120">These numbers are explained below:</span></span>

1. <span data-ttu-id="a000c-121">장치 수준에서 데이터 보호.</span><span class="sxs-lookup"><span data-stu-id="a000c-121">Data protection at the device level.</span></span>
2. <span data-ttu-id="a000c-122">전송 중에 데이터 보호.</span><span class="sxs-lookup"><span data-stu-id="a000c-122">Data protection while in transit.</span></span>
3. <span data-ttu-id="a000c-123">휴지 상태의 온-프레미스에서 데이터 보호.</span><span class="sxs-lookup"><span data-stu-id="a000c-123">Data protection while at rest on-premises.</span></span>
4. <span data-ttu-id="a000c-124">휴지 상태의 클라우드에서 데이터 보호.</span><span class="sxs-lookup"><span data-stu-id="a000c-124">Data protection while at rest in the cloud.</span></span>

<span data-ttu-id="a000c-125">IT가 해당 단계에서 각각 스스로 데어타를 보호할 수 있는 기술적 제어가 직접 하이브리드 ID 솔루션에서 제공되지 않지만 하이브리드 ID 솔루션은 데이터에 대한 액세스를 부여하기 전에 온-프레미스 및 클라우드 ID 관리 리소스를 활용하여 사용자를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-125">Although the technical controls that will enable IT to protect the data itself on each one of those phases are not directly offered by the hybrid identity solution, it is necessary that the hybrid identity solution is capable of leveraging both on-premises and cloud identity management resources to identify the user before grant access to the data.</span></span> <span data-ttu-id="a000c-126">하이브리드 ID 솔루션을 계획할 때에는 조직의 요구 사항에 따라 다음 질문에 답변해 보세요.</span><span class="sxs-lookup"><span data-stu-id="a000c-126">When planning your hybrid identity solution ensure that the following questions are answered according to your organization’s requirements:</span></span>

## <a name="data-protection-at-rest"></a><span data-ttu-id="a000c-127">휴지 상태의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="a000c-127">Data protection at rest</span></span>
<span data-ttu-id="a000c-128">데이터(장치, 클라우드 또는 온-프레미스)가 휴지 상태인 것과 관계 없이 이런 맥락에서 조직의 필요를 이해하는 평가를 수행하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-128">Regardless of where the data is at rest (device, cloud or on-premises), it is important to perform an assessment to understand the organization needs in this regard.</span></span> <span data-ttu-id="a000c-129">이 영역의 경우 다음 질문을 묻는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-129">For this area, ensure that the following questions are asked:</span></span>

* <span data-ttu-id="a000c-130">회사는 미사용 데이터를 보호해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="a000c-130">Does your company need to protect data at rest?</span></span>
  * <span data-ttu-id="a000c-131">그렇다면 하이브리드 ID 솔루션은 현재 온-프레미스 인프라와 통합할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a000c-131">If yes, is the hybrid identity solution able to integrate with your current on-premises infrastructure?</span></span>
  * <span data-ttu-id="a000c-132">그렇다면 하이브리드 ID 솔루션은 클라우드에 위치한 워크로드와 통합할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="a000c-132">If yes, is the hybrid identity solution able to integrate with your workloads located in the cloud?</span></span>
* <span data-ttu-id="a000c-133">클라우드 ID 관리는 사용자의 자격 증명 및 클라우드에 저장된 다른 데이터를 보호할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="a000c-133">Is the cloud identity management able to protect the user’s credentials and other data stored in the cloud?</span></span>

## <a name="data-protection-in-transit"></a><span data-ttu-id="a000c-134">전송 중인 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="a000c-134">Data protection in transit</span></span>
<span data-ttu-id="a000c-135">장치와 데이터 센터 또는 장치와 클라우드 간에 전송 중인 데이터는 보호되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-135">Data in transit between the device and the datacenter or between the device and the cloud must be protected.</span></span> <span data-ttu-id="a000c-136">그러나 전송 중인 상태는 반드시 클라우드 서비스 외부의 구성 요소와 통신 프로세스를 의미하지 않습니다. 또한 예를 들어 두 가상 네트워크 간에 내부적으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-136">However, being in-transit does not necessarily mean a communications process with a component outside of your cloud service; it moves internally, also, such as between two virtual networks.</span></span> <span data-ttu-id="a000c-137">이 영역의 경우 다음 질문을 묻는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-137">For this area, ensure that the following questions are asked:</span></span>

* <span data-ttu-id="a000c-138">회사가 전송 중인 데이터를 보호해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="a000c-138">Does your company need to protect data in transit?</span></span>
  * <span data-ttu-id="a000c-139">그렇다면 하이브리드 ID 솔루션은 SSL/TLS와 같은 보안 제어와 통합할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="a000c-139">If yes, is the hybrid identity solution able to integrate with secure controls such as SSL/TLS?</span></span>
* <span data-ttu-id="a000c-140">클라우드 ID 관리는 서명된 디렉터리 저장소(내부 및 데이터 센터 간) 간에 트래픽을 유지합니까?</span><span class="sxs-lookup"><span data-stu-id="a000c-140">Does the cloud identity management keep the traffic to and within the directory store (within and between datacenters) signed?</span></span>

## <a name="compliance"></a><span data-ttu-id="a000c-141">규정 준수</span><span class="sxs-lookup"><span data-stu-id="a000c-141">Compliance</span></span>
<span data-ttu-id="a000c-142">규정, 법률 및 규정 준수 요구 사항은 회사가 속해 있는 업계에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-142">Regulations, laws and regulatory compliance requirements will vary according to the industry that your company belongs.</span></span> <span data-ttu-id="a000c-143">강력하게 규제된 업계에 있는 회사는 규정 준수 문제와 관련된 ID 관리 문제를 해결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-143">Companies in high regulated industries must address identity-management concerns related to compliance issues.</span></span> <span data-ttu-id="a000c-144">SOX(Sarbanes-Oxley), HIPAA(Health Insurance Portability and Accountability Act), GLBA(Gramm-Leach-Bliley Act) 및 PCI DSS(Payment Card Industry Data Security Standard)와 같은 규정은 ID 및 액세스에 관해 매우 엄격합니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-144">Regulations such as Sarbanes-Oxley (SOX), the Health Insurance Portability and Accountability Act (HIPAA), the Gramm-Leach-Bliley Act (GLBA) and the Payment Card Industry Data Security Standard (PCI DSS) are very strict regarding identity and access.</span></span> <span data-ttu-id="a000c-145">회사가 도입하는 하이브리드 ID 솔루션에는 하나 이상의 이러한 규정 요구 사항을 충족하는 핵심 기능이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-145">The hybrid identity solution that your company will adopt must have the core capabilities that will fulfill the requirements of one or more of these regulations.</span></span> <span data-ttu-id="a000c-146">이 영역의 경우 다음 질문을 묻는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-146">For this area, ensure that the following questions are asked:</span></span>

* <span data-ttu-id="a000c-147">하이브리드 ID 솔루션은 비즈니스에 대한 규정 요구 사항을 준수합니까?</span><span class="sxs-lookup"><span data-stu-id="a000c-147">Is the hybrid identity solution compliant with the regulatory requirements for your business?</span></span>
* <span data-ttu-id="a000c-148">하이브리드 ID 솔루션에는 회사가 규정 요구 사항을 준수할 수 있게 해주는 기본 제공 기능이 있습니다?</span><span class="sxs-lookup"><span data-stu-id="a000c-148">Does the hybrid identity solution has built in capabilities that will enable your company to be compliant regulatory requirements?</span></span> 

> [!NOTE]
> <span data-ttu-id="a000c-149">각 답변을 주목하고 답변 이유를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-149">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="a000c-150">[데이터 보호 전략 정의](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 에서는 사용할 수 있는 옵션과 각 옵션의 장점/단점을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-150">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="a000c-151">질문에 답변함으로써 비즈니스 요구 사항에 가장 적합한 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a000c-151">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a000c-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a000c-152">Next steps</span></span>
 [<span data-ttu-id="a000c-153">콘텐츠 관리 요구 사항 결정</span><span class="sxs-lookup"><span data-stu-id="a000c-153">Determine content management requirements</span></span>](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)

## <a name="see-also"></a><span data-ttu-id="a000c-154">참고 항목</span><span class="sxs-lookup"><span data-stu-id="a000c-154">See Also</span></span>
[<span data-ttu-id="a000c-155">설계 고려 사항 개요</span><span class="sxs-lookup"><span data-stu-id="a000c-155">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

