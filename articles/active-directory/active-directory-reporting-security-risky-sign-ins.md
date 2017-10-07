---
title: "hello Azure Active Directory 포털에서 aaaRisky 로그인 보고서 | Microsoft Docs"
description: "Hello Azure Active Directory 포털에서 hello 위험한 로그인 보고서에 알아보기"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="209bf-103">Hello Azure Active Directory 포털에서 위험한 로그인 보고서</span><span class="sxs-lookup"><span data-stu-id="209bf-103">Risky sign-ins report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="209bf-104">Azure Active Directory (Azure AD)에 hello 보안 보고서와 함께 환경에서 손상 된 사용자 계정의 hello 확률에 대 한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-104">With hello security reports in Azure Active Directory (Azure AD) you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="209bf-105">Azure AD 사용자 계정이 관련된 tooyour 의심 스러운 동작을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-105">Azure AD detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="209bf-106">작업이 감지된 경우 *위험 이벤트*라는 레코드가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="209bf-107">자세한 내용은 [Azure Active Directory 위험 이벤트](active-directory-identity-protection-risk-events.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="209bf-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="209bf-108">hello 위험 이벤트는 사용 되는 toocalculate 감지 함:</span><span class="sxs-lookup"><span data-stu-id="209bf-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="209bf-109">**위험한 로그인** -위험한 로그인이 사용자 계정의 hello 정당한 소유자가 아닌 사용자에 의해 수행 된 로그인 시도에 대 한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="209bf-110">자세한 내용은 [위험한 로그인](active-directory-identityprotection.md#risky-sign-ins)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="209bf-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="209bf-111">**위험 플래그가 지정된 사용자** - 위험한 사용자는 손상되었을 수 있는 사용자 계정에 대한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="209bf-112">자세한 내용은 [위험 플래그가 지정된 사용자](active-directory-identityprotection.md#users-flagged-for-risk)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="209bf-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="209bf-113">[Azure 포털 hello](https://portal.azure.com), hello 보안 hello에 보고서를 찾을 수 있습니다 **Azure Active Directory** hello 블레이드 **보안** 섹션.</span><span class="sxs-lookup"><span data-stu-id="209bf-113">In [hello Azure portal](https://portal.azure.com), you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span> 

![위험한 로그인](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="209bf-115">어떤 Azure AD 라이선스가 tooaccess 보안 보고서 필요 한가요?</span><span class="sxs-lookup"><span data-stu-id="209bf-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="209bf-116">모든 Azure Active Directory 버전에서 위험한 로그인 보고서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-116">All editions of Azure Active Directory provide you with risky sign-ins reports.</span></span>  
<span data-ttu-id="209bf-117">그러나 보고서 세분성 수준의 hello hello 버전 간에 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="209bf-118">Hello에 **Azure Active Directory Free 및 Basic edition**, 이미 위험한 로그인 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of risky sign-ins.</span></span> 

- <span data-ttu-id="209bf-119">hello **Azure Active Directory 프리미엄 1** edition 확장이 모델도 tooexamine를 사용 하 여 각 보고서에 대해 검색 된 위험 이벤트 원본으로 사용 하는 hello의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="209bf-120">hello **Azure Active Directory 프리미엄 2** 버전은 hello로 가장 자세한 정보에 대 한 모든 기본 위험 이벤트 및이 통해 있습니다 tooconfigured 자동으로 응답 하는 tooconfigure 보안 정책 제공 위험 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="209bf-121">Azure Active Directory 무료 및 기본 버전</span><span class="sxs-lookup"><span data-stu-id="209bf-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="209bf-122">hello Azure Active Directory free 및 basic edition 제공 위험한 로그인 검색 된 목록이 사용자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-122">hello Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span></span> <span data-ttu-id="209bf-123">이 보고서는 다음을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-123">This report lists:</span></span>

- <span data-ttu-id="209bf-124">**사용자** -hello hello 로그인 작업 중 사용 된 hello 사용자의 이름</span><span class="sxs-lookup"><span data-stu-id="209bf-124">**User** - hello name of hello user that was used during hello sign-in operation</span></span>
- <span data-ttu-id="209bf-125">**IP** -hello hello 장치를 사용 하는 tooconnect tooAzure Active Directory의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="209bf-125">**IP** - hello IP address of hello device that was used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="209bf-126">**위치** -tooconnect tooAzure Active Directory를 사용 하는 hello 위치</span><span class="sxs-lookup"><span data-stu-id="209bf-126">**Location** - hello location used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="209bf-127">**로그인 시간** -때 hello 로그인 수행한 hello 시간</span><span class="sxs-lookup"><span data-stu-id="209bf-127">**Sign-in time** - hello time when hello sign-in was performed</span></span>
- <span data-ttu-id="209bf-128">**상태** -hello hello에 대 한 로그인의 상태</span><span class="sxs-lookup"><span data-stu-id="209bf-128">**Status** - hello status of hello sign-in</span></span>


![위험한 로그인](./media/active-directory-reporting-security-risky-sign-ins/01.png)

<span data-ttu-id="209bf-130">Hello 위험한 로그인 조사에 따르면 피드백 tooAzure Active Directory에서 작업을 수행 하는 hello의 형태로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-130">Based on your investigation of hello risky sign-in, you can provide feedback tooAzure Active Directory in form of hello following actions:</span></span>

- <span data-ttu-id="209bf-131">해결</span><span class="sxs-lookup"><span data-stu-id="209bf-131">Resolve</span></span>
- <span data-ttu-id="209bf-132">가양성으로 표시</span><span class="sxs-lookup"><span data-stu-id="209bf-132">Mark as false positive</span></span>
- <span data-ttu-id="209bf-133">무시</span><span class="sxs-lookup"><span data-stu-id="209bf-133">Ignore</span></span>
- <span data-ttu-id="209bf-134">다시 활성화</span><span class="sxs-lookup"><span data-stu-id="209bf-134">Reactivate</span></span>

![위험한 로그인](./media/active-directory-reporting-security-risky-sign-ins/21.png)

<span data-ttu-id="209bf-136">자세한 내용은 [수동으로 위험 이벤트 닫기](active-directory-identityprotection.md#closing-risk-events-manually)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="209bf-136">For more details, see [Closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>

<span data-ttu-id="209bf-137">이 보고서는 다음과 같은 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-137">This report provides you with an option to:</span></span>

- <span data-ttu-id="209bf-138">리소스 검색</span><span class="sxs-lookup"><span data-stu-id="209bf-138">Searh resources</span></span>
- <span data-ttu-id="209bf-139">Hello 보고서 데이터를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-139">Download hello report data</span></span>


![위험한 로그인](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="209bf-141">Azure Active Directory Premium Edition</span><span class="sxs-lookup"><span data-stu-id="209bf-141">Azure Active Directory premium editions</span></span>

<span data-ttu-id="209bf-142">hello Azure Active Directory premium edition에서 hello 위험한 로그인 보고서를 제공 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-142">hello risky sign-ins report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="209bf-143">Hello에 대 한 정보를 집계 [이벤트 유형을 위험](active-directory-identity-protection-risk-events.md) 검색</span><span class="sxs-lookup"><span data-stu-id="209bf-143">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="209bf-144">옵션 toodownload hello 보고서</span><span class="sxs-lookup"><span data-stu-id="209bf-144">An option toodownload hello report</span></span>


![위험한 로그인](./media/active-directory-reporting-security-risky-sign-ins/456.png)


<span data-ttu-id="209bf-146">위험 이벤트를 선택하면 위험 이벤트에 대한 자세한 보고서 보기가 제공되고 다음과 같은 작업이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-146">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span></span>

- <span data-ttu-id="209bf-147">옵션 tooconfigure는 [사용자 위험 관리 정책](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="209bf-147">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  

- <span data-ttu-id="209bf-148">Hello 위험 이벤트에 대 한 hello 검색 시간 표시 막대 검토</span><span class="sxs-lookup"><span data-stu-id="209bf-148">Review hello detection timeline for hello risk event</span></span>  

- <span data-ttu-id="209bf-149">이 이벤트가 감지된 사용자 목록 검토</span><span class="sxs-lookup"><span data-stu-id="209bf-149">Review a list of users for which this risk event has been detected</span></span>

- <span data-ttu-id="209bf-150">[위험 이벤트를 수동으로 닫거나](active-directory-identityprotection.md#closing-risk-events-manually) 수동으로 닫은 위험 이벤트를 다시 활성화</span><span class="sxs-lookup"><span data-stu-id="209bf-150">[Manually close risk events](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![위험한 로그인](./media/active-directory-reporting-security-risky-sign-ins/457.png)

<span data-ttu-id="209bf-152">사용자를 선택하면 사용자에 대한 자세한 보고서 보기가 제공되고 다음과 같은 작업이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-152">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="209bf-153">열기 hello 로그인 기능을 모두 보려면</span><span class="sxs-lookup"><span data-stu-id="209bf-153">Open hello All sign-ins view</span></span>

- <span data-ttu-id="209bf-154">Hello 사용자의 암호를 다시 설정</span><span class="sxs-lookup"><span data-stu-id="209bf-154">Reset hello user's password</span></span>

- <span data-ttu-id="209bf-155">모든 이벤트 해제</span><span class="sxs-lookup"><span data-stu-id="209bf-155">Dismiss all events</span></span>

- <span data-ttu-id="209bf-156">Hello 사용자에 대 한 보고 된 위험 이벤트를 조사 합니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-156">Investigate reported risk events for hello user.</span></span> 


![위험한 로그인](./media/active-directory-reporting-security-risky-sign-ins/324.png)


<span data-ttu-id="209bf-158">위험 이벤트 tooinvestigate hello 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-158">tooinvestigate a risk event, select one from hello list.</span></span>  
<span data-ttu-id="209bf-159">Hello 열립니다 **세부 정보** 블레이드가 위험 이벤트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-159">This opens hello **Details** blade for this risk event.</span></span> <span data-ttu-id="209bf-160">Hello에 **세부 정보** 블레이드에서 hello 옵션 tooeither 있는 [위험 상황을 수동으로 닫고](active-directory-identityprotection.md#closing-risk-events-manually) 또는 수동으로 닫힌된 위험 이벤트를 다시 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="209bf-160">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![위험한 로그인](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a><span data-ttu-id="209bf-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="209bf-162">Next steps</span></span>

- <span data-ttu-id="209bf-163">Azure Active Directory ID 보호에 대한 자세한 내용은 [Azure Active Directory ID 보호](active-directory-identityprotection.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="209bf-163">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

