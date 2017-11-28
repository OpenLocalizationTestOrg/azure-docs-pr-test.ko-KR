---
title: "aaaAzure Active Directory 보고서 대기 시간이 | Microsoft Docs"
description: "Azure 포털에서 tooshow 이벤트를 보고 하는 데 걸리는 시간의 hello 크기에 대 한 자세한 내용은"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="1ac2e-103">Azure Active Directory 보고 대기 시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="1ac2e-104">와 [보고](active-directory-preview-explainer.md) hello Azure Active Directory 환경을 어떻게 진행 되는 toodetermine 필요한 모든 hello 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1ac2e-104">With [reporting](active-directory-preview-explainer.md) in hello Azure Active Directory, you get all hello information you need toodetermine how your environment is doing.</span></span> <span data-ttu-id="1ac2e-105">hello Azure 포털에서에서 위로 데이터 tooshow 대기 시간 이라고 보고 하는 데 걸리는 시간 hello 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac2e-105">hello amount of time it takes for reporting data tooshow up in hello Azure portal is also known as latency.</span></span> 

<span data-ttu-id="1ac2e-106">이 항목에서는 hello Azure 포털의에서 모든 보고 범주 hello에 대 한 hello 대기 시간 정보를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac2e-106">This topic lists hello latency information for hello all reporting categories in hello Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="1ac2e-107">작업 보고서</span><span class="sxs-lookup"><span data-stu-id="1ac2e-107">Activity reports</span></span>

<span data-ttu-id="1ac2e-108">활동 보고에는 다음 두 가지 영역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac2e-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="1ac2e-109">**로그인 활동** – 관리 되는 응용 프로그램 및 사용자 로그인 활동의 hello 사용에 대 한 정보</span><span class="sxs-lookup"><span data-stu-id="1ac2e-109">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="1ac2e-110">**감사 로그** - 사용자 및 그룹 관리, 관리되는 응용 프로그램 및 디렉터리 활동에 대한 시스템 활동 정보</span><span class="sxs-lookup"><span data-stu-id="1ac2e-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="1ac2e-111">다음 표에서 hello 활동 보고서에 대 한 hello 대기 시간 정보를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac2e-111">hello following table lists hello latency information for activity reports.</span></span>

| <span data-ttu-id="1ac2e-112">보고서</span><span class="sxs-lookup"><span data-stu-id="1ac2e-112">Report</span></span> | <span data-ttu-id="1ac2e-113">최소</span><span class="sxs-lookup"><span data-stu-id="1ac2e-113">Minimum</span></span> | <span data-ttu-id="1ac2e-114">평균</span><span class="sxs-lookup"><span data-stu-id="1ac2e-114">Average</span></span> | <span data-ttu-id="1ac2e-115">최대</span><span class="sxs-lookup"><span data-stu-id="1ac2e-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="1ac2e-116">감사 로그</span><span class="sxs-lookup"><span data-stu-id="1ac2e-116">Audit logs</span></span>             | <span data-ttu-id="1ac2e-117">30분</span><span class="sxs-lookup"><span data-stu-id="1ac2e-117">30 minutes</span></span>  | <span data-ttu-id="1ac2e-118">45분</span><span class="sxs-lookup"><span data-stu-id="1ac2e-118">45 Minutes</span></span> | <span data-ttu-id="1ac2e-119">1시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-119">1 hour</span></span>     |
| <span data-ttu-id="1ac2e-120">로그인</span><span class="sxs-lookup"><span data-stu-id="1ac2e-120">Sign-ins</span></span>               | <span data-ttu-id="1ac2e-121">15분</span><span class="sxs-lookup"><span data-stu-id="1ac2e-121">15 minutes</span></span>  | <span data-ttu-id="1ac2e-122">15분</span><span class="sxs-lookup"><span data-stu-id="1ac2e-122">15 minutes</span></span> | <span data-ttu-id="1ac2e-123">2시간*</span><span class="sxs-lookup"><span data-stu-id="1ac2e-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="1ac2e-124">레거시 office 응용 프로그램에서 가져온 일부 로그인 활동 데이터를 보고 데이터 tooshow hello에 대 한 too8 시간 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac2e-124">For some sign-ins activity data coming from legacy office applications, it can take too8 hours for hello reporting data tooshow up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="1ac2e-125">보안 보고서</span><span class="sxs-lookup"><span data-stu-id="1ac2e-125">Security reports</span></span>

<span data-ttu-id="1ac2e-126">보안 보고에는 다음 두 가지 영역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ac2e-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="1ac2e-127">**위험한 로그인** -위험한 로그인이 사용자 계정의 hello 정당한 소유자가 아닌 사용자에 의해 수행 된 로그인 시도에 대 한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac2e-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 
- <span data-ttu-id="1ac2e-128">**위험 플래그가 지정된 사용자** - 위험한 사용자는 손상되었을 수 있는 사용자 계정에 대한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="1ac2e-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="1ac2e-129">다음 표에서 hello 보안 보고서에 대 한 hello 대기 시간 정보를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac2e-129">hello following table lists hello latency information for security reports.</span></span>

| <span data-ttu-id="1ac2e-130">보고서</span><span class="sxs-lookup"><span data-stu-id="1ac2e-130">Report</span></span> | <span data-ttu-id="1ac2e-131">최소</span><span class="sxs-lookup"><span data-stu-id="1ac2e-131">Minimum</span></span> | <span data-ttu-id="1ac2e-132">평균</span><span class="sxs-lookup"><span data-stu-id="1ac2e-132">Average</span></span> | <span data-ttu-id="1ac2e-133">최대</span><span class="sxs-lookup"><span data-stu-id="1ac2e-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="1ac2e-134">위험에 노출된 사용자</span><span class="sxs-lookup"><span data-stu-id="1ac2e-134">Users at risk</span></span>          | <span data-ttu-id="1ac2e-135">5분</span><span class="sxs-lookup"><span data-stu-id="1ac2e-135">5 minutes</span></span>   | <span data-ttu-id="1ac2e-136">15분</span><span class="sxs-lookup"><span data-stu-id="1ac2e-136">15 minutes</span></span>  | <span data-ttu-id="1ac2e-137">2시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-137">2 hours</span></span>  |
| <span data-ttu-id="1ac2e-138">위험한 로그인</span><span class="sxs-lookup"><span data-stu-id="1ac2e-138">Risky sign-ins</span></span>         | <span data-ttu-id="1ac2e-139">5분</span><span class="sxs-lookup"><span data-stu-id="1ac2e-139">5 minutes</span></span>   | <span data-ttu-id="1ac2e-140">15분</span><span class="sxs-lookup"><span data-stu-id="1ac2e-140">15 minutes</span></span>  | <span data-ttu-id="1ac2e-141">2시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="1ac2e-142">위험 이벤트</span><span class="sxs-lookup"><span data-stu-id="1ac2e-142">Risk events</span></span>

<span data-ttu-id="1ac2e-143">Azure Active Directory 적응 컴퓨터 학습 알고리즘 및 추론 toodetect 의심 스러운 동작을 관련된 tooyour 사용자 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac2e-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="1ac2e-144">검색된 각 의심스러운 동작은 위험 이벤트라는 레코드에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ac2e-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="1ac2e-145">다음 표에서 hello 위험 이벤트에 대 한 hello 대기 시간 정보를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac2e-145">hello following table lists hello latency information for risk events.</span></span>

| <span data-ttu-id="1ac2e-146">보고서</span><span class="sxs-lookup"><span data-stu-id="1ac2e-146">Report</span></span> | <span data-ttu-id="1ac2e-147">최소</span><span class="sxs-lookup"><span data-stu-id="1ac2e-147">Minimum</span></span> | <span data-ttu-id="1ac2e-148">평균</span><span class="sxs-lookup"><span data-stu-id="1ac2e-148">Average</span></span> | <span data-ttu-id="1ac2e-149">최대</span><span class="sxs-lookup"><span data-stu-id="1ac2e-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="1ac2e-150">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="1ac2e-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="1ac2e-151">5분</span><span class="sxs-lookup"><span data-stu-id="1ac2e-151">5 minutes</span></span> |<span data-ttu-id="1ac2e-152">15분</span><span class="sxs-lookup"><span data-stu-id="1ac2e-152">15 Minutes</span></span> |<span data-ttu-id="1ac2e-153">2시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-153">2 hours</span></span> |
| <span data-ttu-id="1ac2e-154">알 수 없는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="1ac2e-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="1ac2e-155">5분</span><span class="sxs-lookup"><span data-stu-id="1ac2e-155">5 minutes</span></span> |<span data-ttu-id="1ac2e-156">15분</span><span class="sxs-lookup"><span data-stu-id="1ac2e-156">15 Minutes</span></span> |<span data-ttu-id="1ac2e-157">2시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-157">2 hours</span></span> |
| <span data-ttu-id="1ac2e-158">자격 증명이 손실된 사용자</span><span class="sxs-lookup"><span data-stu-id="1ac2e-158">Users with leaked credentials</span></span> |<span data-ttu-id="1ac2e-159">2시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-159">2 hours</span></span> |<span data-ttu-id="1ac2e-160">4시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-160">4 hours</span></span> |<span data-ttu-id="1ac2e-161">8시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-161">8 hours</span></span> |
| <span data-ttu-id="1ac2e-162">이동 불가능 tooatypical 위치</span><span class="sxs-lookup"><span data-stu-id="1ac2e-162">Impossible travel tooatypical locations</span></span> |<span data-ttu-id="1ac2e-163">5분</span><span class="sxs-lookup"><span data-stu-id="1ac2e-163">5 minutes</span></span> |<span data-ttu-id="1ac2e-164">1시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-164">1 hour</span></span> |<span data-ttu-id="1ac2e-165">8시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-165">8 hours</span></span>  |
| <span data-ttu-id="1ac2e-166">감염된 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="1ac2e-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="1ac2e-167">2시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-167">2 hours</span></span> |<span data-ttu-id="1ac2e-168">4시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-168">4 hours</span></span> |<span data-ttu-id="1ac2e-169">8시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-169">8 hours</span></span>  |
| <span data-ttu-id="1ac2e-170">의심스러운 작업이 있는 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="1ac2e-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="1ac2e-171">2시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-171">2 hours</span></span> |<span data-ttu-id="1ac2e-172">4시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-172">4 hours</span></span> |<span data-ttu-id="1ac2e-173">8시간</span><span class="sxs-lookup"><span data-stu-id="1ac2e-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="1ac2e-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ac2e-174">Next steps</span></span>

<span data-ttu-id="1ac2e-175">Hello Azure 포털에서에서 hello 활동 보고서에 대 한 자세한 tooknow, 참조:</span><span class="sxs-lookup"><span data-stu-id="1ac2e-175">If you want tooknow more about hello activity reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="1ac2e-176">Hello Azure Active Directory 포털의 로그인 활동 보고서</span><span class="sxs-lookup"><span data-stu-id="1ac2e-176">Sign-in activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="1ac2e-177">감사 hello Azure Active Directory 포털에서 활동 보고서</span><span class="sxs-lookup"><span data-stu-id="1ac2e-177">Audit activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="1ac2e-178">Hello Azure 포털에서에서 hello 보안 보고서에 대 한 자세한 tooknow, 참조:</span><span class="sxs-lookup"><span data-stu-id="1ac2e-178">If you want tooknow more about hello security reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="1ac2e-179">Hello Azure Active Directory 포털에서 위험 보안 보고서에 있는 사용자</span><span class="sxs-lookup"><span data-stu-id="1ac2e-179">Users at risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="1ac2e-180">Hello Azure Active Directory 포털에서 위험한 로그인 보고서</span><span class="sxs-lookup"><span data-stu-id="1ac2e-180">Risky sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="1ac2e-181">Tooknow 위험 이벤트에 대 한 자세한 참조 [Azure Active Directory 위험 이벤트](active-directory-reporting-risk-events.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ac2e-181">If you want tooknow more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
