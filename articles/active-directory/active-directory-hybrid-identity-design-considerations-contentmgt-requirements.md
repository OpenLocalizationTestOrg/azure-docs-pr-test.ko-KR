---
title: "Azure Active Directory 하이브리드 ID 디자인 고려 사항 - 콘텐츠 관리 요구 사항 확인 | Microsoft Docs"
description: "비즈니스의 콘텐츠 관리 요구 사항을 확인하는 방법을 설명합니다. 일반적으로 사용자에게 자신만의 장치가 있는 경우 사용하는 응용 프로그램에 따라 변경되는 여러 자격 증명이 있을 수 있습니다. 개인 자격 증명을 사용하여 생성된 콘텐츠와 회사 자격 증명을 사용하여 생성된 콘텐츠를 구분하는 것이 중요합니다. ID 솔루션은 최종 사용자의 개인 정보를 보호하고 데이터 유출 방지 기능을 개선하면서, 클라우드 서비스와 상호 작용하여 최종 사용자에게 원활한 환경을 제공할 수 있어야 합니다."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 840de1e1fcba74285788d51d8f544375f0affa77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="df338-106">하이브리드 ID 솔루션에 대한 콘텐츠 관리 요구 사항 확인</span><span class="sxs-lookup"><span data-stu-id="df338-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="df338-107">비즈니스의 콘텐츠 관리 요구 사항에 대한 이해는 어떤 하이브리드 ID 솔루션을 사용할지 결정하는 데 직접적인 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df338-107">Understanding the content management requirements for your business may direct affect your decision on which hybrid identity solution to use.</span></span> <span data-ttu-id="df338-108">여러 장치 및 사용자가 자신의 장치를 가져오는 기능([BYOD](http://aka.ms/byodcg))이 확산됨에 따라 회사는 회사만의 데이터도 보호해야 하지만 사용자의 개인 정보도 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df338-108">With the proliferation of multiple devices and the capability of users to bring their own devices ([BYOD](http://aka.ms/byodcg)), the company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="df338-109">일반적으로 사용자에게 자신만의 장치가 있는 경우 사용하는 응용 프로그램에 따라 변경되는 여러 자격 증명이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df338-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according to the application that he uses.</span></span> <span data-ttu-id="df338-110">개인 자격 증명을 사용하여 생성된 콘텐츠와 회사 자격 증명을 사용하여 생성된 콘텐츠를 구분하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="df338-110">It is important to differentiate what content was created using personal credentials versus the ones created using corporate credentials.</span></span> <span data-ttu-id="df338-111">ID 솔루션은 최종 사용자의 개인 정보를 보호하고 데이터 유출 방지 기능을 개선하면서, 클라우드 서비스와 상호 작용하여 최종 사용자에게 원활한 환경을 제공할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df338-111">Your identity solution should be able to interact with cloud services to provide a seamless experience to the end user while ensure his privacy and increase the protection against data leakage.</span></span> 

<span data-ttu-id="df338-112">ID 솔루션은 아래 그림에 표시된 것처럼 콘텐츠 관리를 제공하기 위해 여러 기술적 컨트롤에서 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="df338-112">Your identity solution will be leveraged by different technical controls in order to provide content management as shown in the figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="df338-113">**ID 관리 시스템을 활용하는 보안 컨트롤**</span><span class="sxs-lookup"><span data-stu-id="df338-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="df338-114">일반적으로 콘텐츠 관리 요구 사항은 다음과 같은 영역에서 ID 관리 시스템을 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="df338-114">In general, content management requirements will leverage your identity management system in the following areas:</span></span>

* <span data-ttu-id="df338-115">개인 정보 보호: 리소스를 소유하는 사용자를 식별하고 적절한 컨트롤을 적용하여 무결성을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="df338-115">Privacy: identifying the user that owns a resource and applying the appropriate controls to maintain integrity.</span></span>
* <span data-ttu-id="df338-116">데이터 분류: 분류에 따라 사용자 또는 그룹 및 개체에 대한 액세스 수준을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="df338-116">Data Classification: identify the user or group and level of access to an object according to its classification.</span></span> 
* <span data-ttu-id="df338-117">데이터 유출 방지: 유출을 막기 위해 데이터 보호를 담당하는 보안 컨트롤은 ID 시스템과 상호 작용하여 사용자의 ID를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df338-117">Data Leakage Protection: security controls responsible for protecting data to avoid leakage will need to interact with the identity system to validate the user’s identity.</span></span> <span data-ttu-id="df338-118">이는 감사 내역을 위해서도 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="df338-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="df338-119">데이터 분류에 대한 모범 사례 및 지침에 대한 자세한 내용은 [클라우드 준비를 위한 데이터 분류](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="df338-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="df338-120">하이브리드 ID 솔루션을 계획할 때에는 조직의 요구 사항에 따라 다음 질문에 답변해 보세요.</span><span class="sxs-lookup"><span data-stu-id="df338-120">When planning your hybrid identity solution ensure that the following questions are answered according to your organization’s requirements:</span></span>

* <span data-ttu-id="df338-121">회사에 데이터 프라이버시를 시행하기 위한 보안 컨트롤이 있나요?</span><span class="sxs-lookup"><span data-stu-id="df338-121">Does your company have security controls in place to enforce data privacy?</span></span>
  * <span data-ttu-id="df338-122">보안 컨트롤이 있다면 그러한 보안 컨트롤이 채택하려는 하이브리드 ID 솔루션과 통합될 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="df338-122">If yes, will those security controls be able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="df338-123">회사에서 데이터 분류를 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="df338-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="df338-124">그렇다면 현재 솔루션이 채택하려는 하이브리드 ID 솔루션과 통합될 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="df338-124">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="df338-125">현재 회사에 데이터 유출에 대한 솔루션이 있나요?</span><span class="sxs-lookup"><span data-stu-id="df338-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="df338-126">그렇다면 현재 솔루션이 채택하려는 하이브리드 ID 솔루션과 통합될 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="df338-126">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="df338-127">회사가 리소스에 대한 액세스를 감사해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="df338-127">Does your company need to audit access to resources?</span></span>
  * <span data-ttu-id="df338-128">그렇다면 어떤 유형의 리소스인가요?</span><span class="sxs-lookup"><span data-stu-id="df338-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="df338-129">그렇다면 어떤 수준의 정보가 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="df338-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="df338-130">그렇다면 감사 로그는 어디에 있어야 하나요?</span><span class="sxs-lookup"><span data-stu-id="df338-130">If yes, where the audit log must reside?</span></span> <span data-ttu-id="df338-131">온-프레미스 또는 클라우드에 있어야 하나요?</span><span class="sxs-lookup"><span data-stu-id="df338-131">On-premises or in the cloud?</span></span>
* <span data-ttu-id="df338-132">회사가 중요한 데이터(SSN, 신용 카드 번호 등)를 포함하는 메일을 암호화해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="df338-132">Does your company need to encrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="df338-133">회사가 외부 비즈니스 파트너와 공유하는 모든 문서/내용을 암호화해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="df338-133">Does your company need to encrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="df338-134">회사가 특정 유형의 메일에 회사 정책을 적용해야 하나요(전체 회신 금지, 전달 금지)?</span><span class="sxs-lookup"><span data-stu-id="df338-134">Does your company need to enforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="df338-135">각 답변을 주목하고 답변 이유를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="df338-135">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="df338-136">[데이터 보호 전략 정의](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 에서는 사용할 수 있는 옵션과 각 옵션의 장점/단점을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="df338-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="df338-137">질문에 답변함으로써 비즈니스 요구 사항에 가장 적합한 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df338-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="df338-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="df338-138">Next steps</span></span>
[<span data-ttu-id="df338-139">액세스 제어 요구 사항 확인</span><span class="sxs-lookup"><span data-stu-id="df338-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="df338-140">참고 항목</span><span class="sxs-lookup"><span data-stu-id="df338-140">See Also</span></span>
[<span data-ttu-id="df338-141">설계 고려 사항 개요</span><span class="sxs-lookup"><span data-stu-id="df338-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

