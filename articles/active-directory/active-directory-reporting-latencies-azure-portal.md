---
title: "Azure Active Directory 보고 대기 시간 | Microsoft Docs"
description: "Azure Portal에 보고 이벤트를 표시하는 데 걸리는 시간에 대해 알아보기"
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
ms.openlocfilehash: 93cb0baeab8f13f81257ed1bd32ed08561c54b72
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="81706-103">Azure Active Directory 보고 대기 시간</span><span class="sxs-lookup"><span data-stu-id="81706-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="81706-104">Azure Active Directory에서 [보고](active-directory-preview-explainer.md)를 통해 사용자 환경의 작동 방법을 결정하는 데 필요한 모든 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81706-104">With [reporting](active-directory-preview-explainer.md) in the Azure Active Directory, you get all the information you need to determine how your environment is doing.</span></span> <span data-ttu-id="81706-105">보고 데이터가 Azure Porta에 표시되는 데 걸리는 시간을 대기 시간이라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="81706-105">The amount of time it takes for reporting data to show up in the Azure portal is also known as latency.</span></span> 

<span data-ttu-id="81706-106">이 항목에서는 Azure Portal의 모든 보고 범주에 대한 대기 시간 정보를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="81706-106">This topic lists the latency information for the all reporting categories in the Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="81706-107">작업 보고서</span><span class="sxs-lookup"><span data-stu-id="81706-107">Activity reports</span></span>

<span data-ttu-id="81706-108">활동 보고에는 다음 두 가지 영역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81706-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="81706-109">**로그인 활동** – 관리되는 응용 프로그램 및 사용자 로그인 활동의 사용량에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="81706-109">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="81706-110">**감사 로그** - 사용자 및 그룹 관리, 관리되는 응용 프로그램 및 디렉터리 활동에 대한 시스템 활동 정보</span><span class="sxs-lookup"><span data-stu-id="81706-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="81706-111">다음 표에는 활동 보고서에 대한 대기 시간 정보가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81706-111">The following table lists the latency information for activity reports.</span></span>

| <span data-ttu-id="81706-112">보고서</span><span class="sxs-lookup"><span data-stu-id="81706-112">Report</span></span> | <span data-ttu-id="81706-113">최소</span><span class="sxs-lookup"><span data-stu-id="81706-113">Minimum</span></span> | <span data-ttu-id="81706-114">평균</span><span class="sxs-lookup"><span data-stu-id="81706-114">Average</span></span> | <span data-ttu-id="81706-115">최대</span><span class="sxs-lookup"><span data-stu-id="81706-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="81706-116">감사 로그</span><span class="sxs-lookup"><span data-stu-id="81706-116">Audit logs</span></span>             | <span data-ttu-id="81706-117">30분</span><span class="sxs-lookup"><span data-stu-id="81706-117">30 minutes</span></span>  | <span data-ttu-id="81706-118">45분</span><span class="sxs-lookup"><span data-stu-id="81706-118">45 Minutes</span></span> | <span data-ttu-id="81706-119">1시간</span><span class="sxs-lookup"><span data-stu-id="81706-119">1 hour</span></span>     |
| <span data-ttu-id="81706-120">로그인</span><span class="sxs-lookup"><span data-stu-id="81706-120">Sign-ins</span></span>               | <span data-ttu-id="81706-121">15분</span><span class="sxs-lookup"><span data-stu-id="81706-121">15 minutes</span></span>  | <span data-ttu-id="81706-122">15분</span><span class="sxs-lookup"><span data-stu-id="81706-122">15 minutes</span></span> | <span data-ttu-id="81706-123">2시간*</span><span class="sxs-lookup"><span data-stu-id="81706-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="81706-124">레거시 Office 응용 프로그램에서 들어오는 일부 로그인 활동 데이터의 경우 보고 데이터가 표시되는 데 8시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81706-124">For some sign-ins activity data coming from legacy office applications, it can take to 8 hours for the reporting data to show up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="81706-125">보안 보고서</span><span class="sxs-lookup"><span data-stu-id="81706-125">Security reports</span></span>

<span data-ttu-id="81706-126">보안 보고에는 다음 두 가지 영역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81706-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="81706-127">**위험한 로그인** - 위험한 로그인은 사용자 계정의 정당한 소유자가 아닌 사용자에 의해 수행된 로그인 시도에 대한 지표입니다.</span><span class="sxs-lookup"><span data-stu-id="81706-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 
- <span data-ttu-id="81706-128">**위험 플래그가 지정된 사용자** - 위험한 사용자는 손상되었을 수 있는 사용자 계정에 대한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="81706-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="81706-129">다음 표에는 보안 보고서에 대한 대기 시간 정보가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81706-129">The following table lists the latency information for security reports.</span></span>

| <span data-ttu-id="81706-130">보고서</span><span class="sxs-lookup"><span data-stu-id="81706-130">Report</span></span> | <span data-ttu-id="81706-131">최소</span><span class="sxs-lookup"><span data-stu-id="81706-131">Minimum</span></span> | <span data-ttu-id="81706-132">평균</span><span class="sxs-lookup"><span data-stu-id="81706-132">Average</span></span> | <span data-ttu-id="81706-133">최대</span><span class="sxs-lookup"><span data-stu-id="81706-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="81706-134">위험에 노출된 사용자</span><span class="sxs-lookup"><span data-stu-id="81706-134">Users at risk</span></span>          | <span data-ttu-id="81706-135">5분</span><span class="sxs-lookup"><span data-stu-id="81706-135">5 minutes</span></span>   | <span data-ttu-id="81706-136">15분</span><span class="sxs-lookup"><span data-stu-id="81706-136">15 minutes</span></span>  | <span data-ttu-id="81706-137">2시간</span><span class="sxs-lookup"><span data-stu-id="81706-137">2 hours</span></span>  |
| <span data-ttu-id="81706-138">위험한 로그인</span><span class="sxs-lookup"><span data-stu-id="81706-138">Risky sign-ins</span></span>         | <span data-ttu-id="81706-139">5분</span><span class="sxs-lookup"><span data-stu-id="81706-139">5 minutes</span></span>   | <span data-ttu-id="81706-140">15분</span><span class="sxs-lookup"><span data-stu-id="81706-140">15 minutes</span></span>  | <span data-ttu-id="81706-141">2시간</span><span class="sxs-lookup"><span data-stu-id="81706-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="81706-142">위험 이벤트</span><span class="sxs-lookup"><span data-stu-id="81706-142">Risk events</span></span>

<span data-ttu-id="81706-143">Azure Active Directory는 적응 기계 학습 알고리즘 및 추론을 사용하여 사용자의 계정과 관련된 의심스러운 작업을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="81706-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="81706-144">검색된 각 의심스러운 동작은 위험 이벤트라는 레코드에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="81706-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="81706-145">다음 표에는 위험 이벤트에 대한 대기 시간 정보가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="81706-145">The following table lists the latency information for risk events.</span></span>

| <span data-ttu-id="81706-146">보고서</span><span class="sxs-lookup"><span data-stu-id="81706-146">Report</span></span> | <span data-ttu-id="81706-147">최소</span><span class="sxs-lookup"><span data-stu-id="81706-147">Minimum</span></span> | <span data-ttu-id="81706-148">평균</span><span class="sxs-lookup"><span data-stu-id="81706-148">Average</span></span> | <span data-ttu-id="81706-149">최대</span><span class="sxs-lookup"><span data-stu-id="81706-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="81706-150">익명 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="81706-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="81706-151">5분</span><span class="sxs-lookup"><span data-stu-id="81706-151">5 minutes</span></span> |<span data-ttu-id="81706-152">15분</span><span class="sxs-lookup"><span data-stu-id="81706-152">15 Minutes</span></span> |<span data-ttu-id="81706-153">2시간</span><span class="sxs-lookup"><span data-stu-id="81706-153">2 hours</span></span> |
| <span data-ttu-id="81706-154">알 수 없는 위치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="81706-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="81706-155">5분</span><span class="sxs-lookup"><span data-stu-id="81706-155">5 minutes</span></span> |<span data-ttu-id="81706-156">15분</span><span class="sxs-lookup"><span data-stu-id="81706-156">15 Minutes</span></span> |<span data-ttu-id="81706-157">2시간</span><span class="sxs-lookup"><span data-stu-id="81706-157">2 hours</span></span> |
| <span data-ttu-id="81706-158">자격 증명이 손실된 사용자</span><span class="sxs-lookup"><span data-stu-id="81706-158">Users with leaked credentials</span></span> |<span data-ttu-id="81706-159">2시간</span><span class="sxs-lookup"><span data-stu-id="81706-159">2 hours</span></span> |<span data-ttu-id="81706-160">4시간</span><span class="sxs-lookup"><span data-stu-id="81706-160">4 hours</span></span> |<span data-ttu-id="81706-161">8시간</span><span class="sxs-lookup"><span data-stu-id="81706-161">8 hours</span></span> |
| <span data-ttu-id="81706-162">비정상적 위치로 불가능한 이동</span><span class="sxs-lookup"><span data-stu-id="81706-162">Impossible travel to atypical locations</span></span> |<span data-ttu-id="81706-163">5분</span><span class="sxs-lookup"><span data-stu-id="81706-163">5 minutes</span></span> |<span data-ttu-id="81706-164">1시간</span><span class="sxs-lookup"><span data-stu-id="81706-164">1 hour</span></span> |<span data-ttu-id="81706-165">8시간</span><span class="sxs-lookup"><span data-stu-id="81706-165">8 hours</span></span>  |
| <span data-ttu-id="81706-166">감염된 장치에서 로그인</span><span class="sxs-lookup"><span data-stu-id="81706-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="81706-167">2시간</span><span class="sxs-lookup"><span data-stu-id="81706-167">2 hours</span></span> |<span data-ttu-id="81706-168">4시간</span><span class="sxs-lookup"><span data-stu-id="81706-168">4 hours</span></span> |<span data-ttu-id="81706-169">8시간</span><span class="sxs-lookup"><span data-stu-id="81706-169">8 hours</span></span>  |
| <span data-ttu-id="81706-170">의심스러운 작업이 있는 IP 주소에서 로그인</span><span class="sxs-lookup"><span data-stu-id="81706-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="81706-171">2시간</span><span class="sxs-lookup"><span data-stu-id="81706-171">2 hours</span></span> |<span data-ttu-id="81706-172">4시간</span><span class="sxs-lookup"><span data-stu-id="81706-172">4 hours</span></span> |<span data-ttu-id="81706-173">8시간</span><span class="sxs-lookup"><span data-stu-id="81706-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="81706-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="81706-174">Next steps</span></span>

<span data-ttu-id="81706-175">Azure Portal의 활동 보고서에 자세히 알아보려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81706-175">If you want to know more about the activity reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="81706-176">Azure Active Directory 포털의 로그인 활동 보고서</span><span class="sxs-lookup"><span data-stu-id="81706-176">Sign-in activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="81706-177">Azure Active Directory 포털의 감사 활동 보고서</span><span class="sxs-lookup"><span data-stu-id="81706-177">Audit activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="81706-178">Azure Portal의 보안 보고서에 자세히 알아보려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81706-178">If you want to know more about the security reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="81706-179">Azure Active Directory 포털에서 제공하는 위험에 노출된 사용자 보안 보고서</span><span class="sxs-lookup"><span data-stu-id="81706-179">Users at risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="81706-180">Azure Active Directory 포털에서 제공하는 위험한 로그인 보고서</span><span class="sxs-lookup"><span data-stu-id="81706-180">Risky sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="81706-181">위험 이벤트에 대한 자세한 내용은 [Azure Active Directory 위험 이벤트](active-directory-reporting-risk-events.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81706-181">If you want to know more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
