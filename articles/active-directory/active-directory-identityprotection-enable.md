---
title: "Azure Active Directory Id 보호 aaaEnabling | Microsoft Docs"
description: "자세한 내용은 방법 tooenable Azure Active Directory Id 보호 합니다."
services: active-directory
keywords: "Azure Active Directory ID 보호, 클라우드 앱 검색, 응용 프로그램 관리, 보안, 위험, 위험 수준, 취약점, 보안 정책"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f7a7ffaf-76bf-4cc7-96a1-86c944275c82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: d26f466f5c7d6a425528a277d98c2c4b341ff8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-active-directory-identity-protection"></a><span data-ttu-id="8c3f5-104">Azure Active Directory ID 보호 활성화</span><span class="sxs-lookup"><span data-stu-id="8c3f5-104">Enabling Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="8c3f5-105">Azure Active Directory ID 보호는 의심스러운 로그인 활동 및 잠재적인 취약성에 대한 통합된 보기를 제공하고 알림, 수정 권장 사항 및 위험 기반 정책을 통해 비즈니스를 보호하도록 도움을 주는 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="8c3f5-105">Azure Active Directory Identity Protection is a new capability that provides a consolidated view into suspicious sign-in activities and potential vulnerabilities and with notifications, remediation recommendations and risk-based policies helps you protect your business.</span></span> 

<span data-ttu-id="8c3f5-106">hello 서비스에서 검색 의심 스러운 활동 대입 공격, 무차별 암호와 같은 신호에 따라 권한 (관리자) id 및 최종 사용자에 대 한 유출 자격 증명을 로그인 생소 한 위치에서 장치를 실시간으로 이러한 활동에 대해 tooprotect 감염 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c3f5-106">hello service detects suspicious activities for end user and privileged (admin) identities based on signals like brute force attacks, leaked credentials, sign ins from unfamiliar locations, infected devices, tooprotect against these activities in real-time.</span></span> <span data-ttu-id="8c3f5-107">무엇 보다도 이러한 의심 스러운 활동에 따라, 사용자 위험 심각도 계산 및 위험 기반 정책을 구성할 수 있으며, 조직의 hello id를 자동으로 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c3f5-107">More importantly, based on these suspicious activities, a user risk severity is computed and risk-based policies can be configured and automatically protect hello identities of your organization.</span></span> <span data-ttu-id="8c3f5-108">자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8c3f5-108">For more details, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

<span data-ttu-id="8c3f5-109">이 항목의 표시 방법을 tooenable Azure Active Directory Id 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="8c3f5-109">This topics shows how tooenable Azure Active Directory Identity Protection.</span></span>

## <a name="steps-tooenable-azure-active-directory-identity-protection"></a><span data-ttu-id="8c3f5-110">단계 tooenable Azure Active Directory Id 보호</span><span class="sxs-lookup"><span data-stu-id="8c3f5-110">Steps tooenable Azure Active Directory Identity Protection</span></span>
1. <span data-ttu-id="8c3f5-111">[로그온](https://ms.portal.azure.com/) tooyour 전역 관리자로 Azure 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="8c3f5-111">[Sign-on](https://ms.portal.azure.com/) tooyour Azure portal as global administrator.</span></span> 
2. <span data-ttu-id="8c3f5-112">Hello Azure 포털에서에서 클릭 **마켓플레이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c3f5-112">In hello Azure portal, click **Marketplace**.</span></span>
   
    <span data-ttu-id="8c3f5-113">![만들기](./media/active-directory-identityprotection-enable/01.png "만들기")</span><span class="sxs-lookup"><span data-stu-id="8c3f5-113">![Create](./media/active-directory-identityprotection-enable/01.png "Create")</span></span>
3. <span data-ttu-id="8c3f5-114">Hello 응용 프로그램 목록에서 클릭 **보안 + Id**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c3f5-114">In hello applications list, click **Security + Identity**.</span></span>
   
    <span data-ttu-id="8c3f5-115">![만들기](./media/active-directory-identityprotection-enable/02.png "만들기")</span><span class="sxs-lookup"><span data-stu-id="8c3f5-115">![Create](./media/active-directory-identityprotection-enable/02.png "Create")</span></span>
4. <span data-ttu-id="8c3f5-116">**Azure AD ID 보호**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8c3f5-116">Click **Azure AD Identity Protection**.</span></span>
   
    <span data-ttu-id="8c3f5-117">![만들기](./media/active-directory-identityprotection-enable/03.png "만들기")</span><span class="sxs-lookup"><span data-stu-id="8c3f5-117">![Create](./media/active-directory-identityprotection-enable/03.png "Create")</span></span>
5. <span data-ttu-id="8c3f5-118">Hello에 **Azure AD Identity Protection** 블레이드에서 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="8c3f5-118">On hello **Azure AD Identity Protection** blade, click **Create**.</span></span>
   
    <span data-ttu-id="8c3f5-119">![만들기](./media/active-directory-identityprotection-enable/04.png "만들기")</span><span class="sxs-lookup"><span data-stu-id="8c3f5-119">![Create](./media/active-directory-identityprotection-enable/04.png "Create")</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c3f5-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8c3f5-120">Next Steps</span></span>
* [<span data-ttu-id="8c3f5-121">Azure Active Directory ID 보호</span><span class="sxs-lookup"><span data-stu-id="8c3f5-121">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

