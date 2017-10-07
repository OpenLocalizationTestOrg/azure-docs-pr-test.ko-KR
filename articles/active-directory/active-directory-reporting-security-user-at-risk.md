---
title: "hello Azure Active Directory 포털에서 위험 보안 보고서에 대 한 플래그가 지정 aaaUsers | Microsoft Docs"
description: "Hello Azure Active Directory 포털에서 위험 보안 보고서에 대 한 플래그를 지정 하는 hello 사용자에 대 한 자세한 내용은"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="07c6a-103">Hello Azure Active Directory 포털에서 위험 보안 보고서에 대 한 플래그가 지정 된 사용자</span><span class="sxs-lookup"><span data-stu-id="07c6a-103">Users flagged for risk security report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="07c6a-104">Hello hello Azure Active Directory (Azure AD)에 보안 보고서에 사용자 환경에서 손상 된 사용자 계정의 hello 확률에 대 한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-104">With hello security reports in hello Azure Active Directory (Azure AD), you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="07c6a-105">Azure Active Directory 사용자 계정이 관련된 tooyour 의심 스러운 동작을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-105">Azure Active Directory detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="07c6a-106">작업이 감지된 경우 *위험 이벤트*라는 레코드가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="07c6a-107">자세한 내용은 [Azure Active Directory 위험 이벤트](active-directory-identity-protection-risk-events.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07c6a-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="07c6a-108">hello 위험 이벤트는 사용 되는 toocalculate 감지 함:</span><span class="sxs-lookup"><span data-stu-id="07c6a-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="07c6a-109">**위험한 로그인** -위험한 로그인이 사용자 계정의 hello 정당한 소유자가 아닌 사용자에 의해 수행 된 로그인 시도에 대 한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="07c6a-110">자세한 내용은 [위험한 로그인](active-directory-identityprotection.md#risky-sign-ins)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07c6a-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="07c6a-111">**위험 플래그가 지정된 사용자** - 위험한 사용자는 손상되었을 수 있는 사용자 계정에 대한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="07c6a-112">자세한 내용은 [위험 플래그가 지정된 사용자](active-directory-identityprotection.md#users-flagged-for-risk)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07c6a-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="07c6a-113">Hello Azure 포털에서에서 찾을 수 있습니다 hello 보안 hello를 보고 **Azure Active Directory** hello 블레이드 **보안** 섹션.</span><span class="sxs-lookup"><span data-stu-id="07c6a-113">In hello Azure portal, you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span>  

![위험한 로그인](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="07c6a-115">어떤 Azure AD 라이선스가 tooaccess 보안 보고서 필요 한가요?</span><span class="sxs-lookup"><span data-stu-id="07c6a-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="07c6a-116">모든 Azure Active Directory 버전에서 위험 플래그가 지정된 사용자 보고서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="07c6a-117">그러나 보고서 세분성 수준의 hello hello 버전 간에 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="07c6a-118">Hello에 **Azure Active Directory Free 및 Basic edition**, 이미 위험에 대 한 플래그가 지정 된 사용자 목록을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="07c6a-119">hello **Azure Active Directory 프리미엄 1** edition 확장이 모델도 tooexamine를 사용 하 여 각 보고서에 대해 검색 된 위험 이벤트 원본으로 사용 하는 hello의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="07c6a-120">hello **Azure Active Directory 프리미엄 2** 버전을 제공 하는 모든 기본 위험 이벤트에 대 한 가장 자세한 정보를 hello 및 tooconfigured 위험을 자동으로 응답 하는 tooconfigure 보안 정책을 사용 하면 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="07c6a-121">Azure Active Directory 무료 및 기본 버전</span><span class="sxs-lookup"><span data-stu-id="07c6a-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="07c6a-122">hello Azure Active Directory free 및 basic 버전에서 위험 보고서에 대 한 플래그를 지정 하는 hello 사용자가 손상 되었을 수 있는 사용자 계정의 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-122">hello users flagged for risk report in hello Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![위험한 로그인](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="07c6a-124">사용자를 선택 하면 hello 관련된 사용자 데이터 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-124">Selecting a user opens hello related user data blade.</span></span>
<span data-ttu-id="07c6a-125">사용자가 위험에 대 한 hello 사용자 로그인 기록을 검토할 수 있으며 필요한 경우 hello 암호 재설정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-125">For users that are at risk, you can review hello user’s sign-in history and reset hello password if necessary.</span></span>

![위험한 로그인](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="07c6a-127">이 대화 상자는 다음과 같은 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="07c6a-128">Hello 보고서 다운로드</span><span class="sxs-lookup"><span data-stu-id="07c6a-128">Download hello report</span></span>

- <span data-ttu-id="07c6a-129">사용자 검색</span><span class="sxs-lookup"><span data-stu-id="07c6a-129">Search users</span></span>

![위험한 로그인](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="07c6a-131">Azure Active Directory Premium Edition</span><span class="sxs-lookup"><span data-stu-id="07c6a-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="07c6a-132">hello Azure Active Directory premium edition에서 위험 보고서에 대 한 플래그를 지정 하는 hello 사용자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-132">hello users flagged for risk report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="07c6a-133">손상되었을 수 있는 [사용자 계정 목록](active-directory-identityprotection.md#users-flagged-for-risk)</span><span class="sxs-lookup"><span data-stu-id="07c6a-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="07c6a-134">Hello에 대 한 정보를 집계 [이벤트 유형을 위험](active-directory-identity-protection-risk-events.md) 검색</span><span class="sxs-lookup"><span data-stu-id="07c6a-134">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="07c6a-135">옵션 toodownload hello 보고서</span><span class="sxs-lookup"><span data-stu-id="07c6a-135">An option toodownload hello report</span></span>

- <span data-ttu-id="07c6a-136">옵션 tooconfigure는 [사용자 위험 관리 정책](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="07c6a-136">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![위험한 로그인](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="07c6a-138">사용자를 선택하면 사용자에 대한 자세한 보고서 보기가 제공되고 다음과 같은 작업이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="07c6a-139">열기 hello 로그인 기능을 모두 보려면</span><span class="sxs-lookup"><span data-stu-id="07c6a-139">Open hello All sign-ins view</span></span>

- <span data-ttu-id="07c6a-140">Hello 사용자의 암호를 다시 설정</span><span class="sxs-lookup"><span data-stu-id="07c6a-140">Reset hello user's password</span></span>

- <span data-ttu-id="07c6a-141">모든 이벤트 해제</span><span class="sxs-lookup"><span data-stu-id="07c6a-141">Dismiss all events</span></span>

- <span data-ttu-id="07c6a-142">Hello 사용자에 대 한 보고 된 위험 이벤트를 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-142">Investigate reported risk events for hello user.</span></span> 


![위험한 로그인](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="07c6a-144">위험 이벤트 tooinvestigate hello 목록 tooopen hello에서 하나를 선택 합니다. **세부 정보** 블레이드가 위험 이벤트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-144">tooinvestigate a risk event, select one from hello list tooopen hello **Details** blade for this risk event.</span></span> <span data-ttu-id="07c6a-145">Hello에 **세부 정보** 블레이드에서 hello 옵션 tooeither 있는 [위험 상황을 수동으로 닫고](active-directory-identityprotection.md#closing-risk-events-manually) 또는 수동으로 닫힌된 위험 이벤트를 다시 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c6a-145">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![위험한 로그인](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="07c6a-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="07c6a-147">Next steps</span></span>

- <span data-ttu-id="07c6a-148">Azure Active Directory ID 보호에 대한 자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="07c6a-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

