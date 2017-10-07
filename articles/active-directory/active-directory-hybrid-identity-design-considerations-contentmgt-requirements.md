---
title: "aaaAzure Active Directory 하이브리드 id 디자인 고려 사항-콘텐츠 관리 요구 사항을 결정 | Microsoft Docs"
description: "어떻게 toodetermine hello 비즈니스의 콘텐츠 관리 요구 사항에 대 한 정보를 제공 합니다. 일반적으로 사용자가 자신의 장치에 있을 때 있다고 생각할 수 또한 여러 자격 증명을 사용 하 여 그에 따라 toohello 응용 프로그램을 대체 합니다. 것이 중요 한 toodifferentiate 콘텐츠 hello 회사 자격 증명을 사용 하 여 만든 것과 개인 자격 증명을 사용 하 여 생성 합니다. Id 솔루션 해야 클라우드 서비스 tooprovide와 수 toointeract 동안 원활한 환경을 toohello 최종 사용자가 개인 정보 보호 및 데이터 유출 로부터 보호 하는 hello 기능을 강화 합니다."
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
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="2b9d2-106">하이브리드 ID 솔루션에 대한 콘텐츠 관리 요구 사항 확인</span><span class="sxs-lookup"><span data-stu-id="2b9d2-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="2b9d2-107">Hello 콘텐츠 관리 요구 사항 이해 비즈니스가 필요할 수에 대 한 영향을 결정 하는 하이브리드 identity 솔루션 toouse에.</span><span class="sxs-lookup"><span data-stu-id="2b9d2-107">Understanding hello content management requirements for your business may direct affect your decision on which hybrid identity solution toouse.</span></span> <span data-ttu-id="2b9d2-108">와 hello 확산 됨에 따라 여러 장치 및 사용자가 toobring의 hello 기능이 자신의 장치 ([BYOD](http://aka.ms/byodcg)), hello 회사는 자체 데이터를 보호 해야 하지만 또한 유지 하도록 사용자의 개인 정보 그대로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b9d2-108">With hello proliferation of multiple devices and hello capability of users toobring their own devices ([BYOD](http://aka.ms/byodcg)), hello company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="2b9d2-109">일반적으로 사용자가 자신의 장치에 있을 때 있다고 생각할 수 또한 여러 자격 증명을 사용 하 여 그에 따라 toohello 응용 프로그램을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b9d2-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according toohello application that he uses.</span></span> <span data-ttu-id="2b9d2-110">것이 중요 한 toodifferentiate 콘텐츠 hello 회사 자격 증명을 사용 하 여 만든 것과 개인 자격 증명을 사용 하 여 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b9d2-110">It is important toodifferentiate what content was created using personal credentials versus hello ones created using corporate credentials.</span></span> <span data-ttu-id="2b9d2-111">Id 솔루션 해야 클라우드 서비스 tooprovide와 수 toointeract 동안 원활한 환경을 toohello 최종 사용자가 개인 정보 보호 및 데이터 유출 로부터 보호 하는 hello 기능을 강화 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b9d2-111">Your identity solution should be able toointeract with cloud services tooprovide a seamless experience toohello end user while ensure his privacy and increase hello protection against data leakage.</span></span> 

<span data-ttu-id="2b9d2-112">Id 솔루션 아래 hello 그림에 나와 있는 것 처럼 순서 tooprovide 콘텐츠 관리의 다른 기술 제어에서 활용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b9d2-112">Your identity solution will be leveraged by different technical controls in order tooprovide content management as shown in hello figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="2b9d2-113">**ID 관리 시스템을 활용하는 보안 컨트롤**</span><span class="sxs-lookup"><span data-stu-id="2b9d2-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="2b9d2-114">일반적으로 콘텐츠 관리 요구 사항을 hello 다음 영역에서에서 id 관리 시스템과 활용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b9d2-114">In general, content management requirements will leverage your identity management system in hello following areas:</span></span>

* <span data-ttu-id="2b9d2-115">개인 정보: 리소스를 소유 하는 hello 사용자를 식별 하 고 hello 적절 한 컨트롤 toomaintain 무결성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b9d2-115">Privacy: identifying hello user that owns a resource and applying hello appropriate controls toomaintain integrity.</span></span>
* <span data-ttu-id="2b9d2-116">데이터 분류: hello 사용자 또는 그룹 및 tooits 분류에 따라 액세스 tooan 개체의 수준을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b9d2-116">Data Classification: identify hello user or group and level of access tooan object according tooits classification.</span></span> 
* <span data-ttu-id="2b9d2-117">데이터를 유출할 보호: tooavoid 유출 데이터를 보호 하는 일을 담당 하는 보안 제어 hello id 시스템 toovalidate hello 사용자의 id 가진 toointeract이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b9d2-117">Data Leakage Protection: security controls responsible for protecting data tooavoid leakage will need toointeract with hello identity system toovalidate hello user’s identity.</span></span> <span data-ttu-id="2b9d2-118">이는 감사 내역을 위해서도 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="2b9d2-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="2b9d2-119">데이터 분류에 대한 모범 사례 및 지침에 대한 자세한 내용은 [클라우드 준비를 위한 데이터 분류](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b9d2-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="2b9d2-120">다음 해당 hello 확인 하이브리드 id 솔루션을 계획 하는 경우 게시 된 질문은 tooyour 조직의 요구 사항에 따라:</span><span class="sxs-lookup"><span data-stu-id="2b9d2-120">When planning your hybrid identity solution ensure that hello following questions are answered according tooyour organization’s requirements:</span></span>

* <span data-ttu-id="2b9d2-121">회사에가 보안 제어 위치 tooenforce 데이터 개인 정보 보호에 있습니까?</span><span class="sxs-lookup"><span data-stu-id="2b9d2-121">Does your company have security controls in place tooenforce data privacy?</span></span>
  * <span data-ttu-id="2b9d2-122">그러한 경우 해당 보안 제어 삭제 됩니다 계속 tooadopt는 hello 하이브리드 id 솔루션으로 수 toointegrate?</span><span class="sxs-lookup"><span data-stu-id="2b9d2-122">If yes, will those security controls be able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="2b9d2-123">회사에서 데이터 분류를 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="2b9d2-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="2b9d2-124">그러한 경우 진행 중인 tooadopt는 hello 하이브리드 id 솔루션으로 hello 현재 솔루션 수 toointegrate은?</span><span class="sxs-lookup"><span data-stu-id="2b9d2-124">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="2b9d2-125">현재 회사에 데이터 유출에 대한 솔루션이 있나요?</span><span class="sxs-lookup"><span data-stu-id="2b9d2-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="2b9d2-126">그러한 경우 진행 중인 tooadopt는 hello 하이브리드 id 솔루션으로 hello 현재 솔루션 수 toointegrate은?</span><span class="sxs-lookup"><span data-stu-id="2b9d2-126">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="2b9d2-127">Tooaudit 액세스 tooresources 회사에 필요 합니까?</span><span class="sxs-lookup"><span data-stu-id="2b9d2-127">Does your company need tooaudit access tooresources?</span></span>
  * <span data-ttu-id="2b9d2-128">그렇다면 어떤 유형의 리소스인가요?</span><span class="sxs-lookup"><span data-stu-id="2b9d2-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="2b9d2-129">그렇다면 어떤 수준의 정보가 필요한가요?</span><span class="sxs-lookup"><span data-stu-id="2b9d2-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="2b9d2-130">예, 여기서 hello 감사 로그 상주해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b9d2-130">If yes, where hello audit log must reside?</span></span> <span data-ttu-id="2b9d2-131">온-프레미스 또는 클라우드에서 hello?</span><span class="sxs-lookup"><span data-stu-id="2b9d2-131">On-premises or in hello cloud?</span></span>
* <span data-ttu-id="2b9d2-132">회사에 tooencrypt 필요 합니까 (SSNs, 신용 카드 번호 등)의 중요 한 데이터가 포함 된 모든 메일?</span><span class="sxs-lookup"><span data-stu-id="2b9d2-132">Does your company need tooencrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="2b9d2-133">회사에 tooencrypt 필요 합니까 외부 비즈니스 파트너와 공유 하는 모든 문서/콘텐츠?</span><span class="sxs-lookup"><span data-stu-id="2b9d2-133">Does your company need tooencrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="2b9d2-134">회사 전자 메일의 특정 종류의 tooenforce 회사 정책에 필요 합니까 (모든 회신 없음 수행, 전달 금지)?</span><span class="sxs-lookup"><span data-stu-id="2b9d2-134">Does your company need tooenforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="2b9d2-135">각 응답 tootake 메모 있는지를 확인 하 고 hello 응답 hello 도입한 이유를 이해 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b9d2-135">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="2b9d2-136">[데이터 보호 전략 정의](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) 에서는 hello 사용 가능한 옵션과 각 옵션의 장단점을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="2b9d2-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="2b9d2-137">질문에 답변함으로써 비즈니스 요구 사항에 가장 적합한 옵션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b9d2-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2b9d2-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2b9d2-138">Next steps</span></span>
[<span data-ttu-id="2b9d2-139">액세스 제어 요구 사항 확인</span><span class="sxs-lookup"><span data-stu-id="2b9d2-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="2b9d2-140">참고 항목</span><span class="sxs-lookup"><span data-stu-id="2b9d2-140">See Also</span></span>
[<span data-ttu-id="2b9d2-141">설계 고려 사항 개요</span><span class="sxs-lookup"><span data-stu-id="2b9d2-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

