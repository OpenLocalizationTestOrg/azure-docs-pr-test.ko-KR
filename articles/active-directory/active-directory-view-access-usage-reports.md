---
title: "액세스 및 사용 보고서 보기 | Microsoft Docs"
description: "액세스 및 사용 보고서를 사용하여 조직 디렉터리의 무결성 및 보안을 보는 방법에 대해 설명합니다."
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: a074bc4e-cf3f-4ad1-8cc6-4199d2e09ce4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 038ac79ebf61c6429fbf7ca21eefe9414bcfc03a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="view-your-access-and-usage-reports"></a><span data-ttu-id="a2522-103">액세스 및 사용 보고서 보기</span><span class="sxs-lookup"><span data-stu-id="a2522-103">View your access and usage reports</span></span>
<span data-ttu-id="a2522-104">*이 설명서는 [Azure Active Directory Reporting 가이드](active-directory-reporting-guide.md)의 일부입니다.*</span><span class="sxs-lookup"><span data-stu-id="a2522-104">*This documentation is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="a2522-105">Azure Active Directory의 액세스 및 사용 보고서를 사용하여 조직 디렉터리의 무결성 및 보안을 볼 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="a2522-105">You can use Azure Active Directory's access and usage reports to gain visibility into the integrity and security of your organization’s directory.</span></span> <span data-ttu-id="a2522-106">이 정보를 사용하면 디렉터리 관리자는 가능한 보안 위험이 발생할 수 있는 위치를 보다 잘 결정하여 이러한 위험을 적절하게 완화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-106">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan to mitigate those risks.</span></span>

<span data-ttu-id="a2522-107">Azure 관리 포털에서 보고서는 다음과 같은 방식으로 분류되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-107">In the Azure Management Portal, reports are categorized in the following ways:</span></span>

* <span data-ttu-id="a2522-108">비정상 보고서 – 비정상으로 확인된 로그인 이벤트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-108">Anomaly reports – Contain sign in events that we found to be anomalous.</span></span> <span data-ttu-id="a2522-109">이러한 활동을 인식하고 이벤트가 의심스러운지 확인할 수 있게 해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-109">Our goal is to make you aware of such activity and enable you to be able to make a determination about whether an event is suspicious.</span></span>
* <span data-ttu-id="a2522-110">통합 응용 프로그램 보고서 – 클라우드 응용 프로그램이 조직에서 사용되는 방식을 파악할 수 있게 해 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-110">Integrated Application reports – Provides insights into how cloud applications are being used in your organization.</span></span> <span data-ttu-id="a2522-111">Azure Active Directory는 수천 개의 클라우드 응용 프로그램과 통합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-111">Azure Active Directory offers integration with thousands of cloud applications.</span></span>
* <span data-ttu-id="a2522-112">오류 보고서 – 외부 응용 프로그램에 계정을 프로비전할 때 발생할 수 있는 오류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-112">Error reports – Indicate errors that may occur when provisioning accounts to external applications.</span></span>
* <span data-ttu-id="a2522-113">사용자별 보고서 – 특정 사용자에 대한 장치/로그인 활동 데이터를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-113">User-specific reports – Display device/sign in activity data for a specific user.</span></span>
* <span data-ttu-id="a2522-114">활동 로그 - 최근 24시간, 최근 7일 또는 최근 30일 이내에 감사된 모든 이벤트의 레코드와 그룹 활동 변경 사항, 암호 재설정 및 등록 활동이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-114">Activity logs – Contain a record of all audited events within the last 24 hours, last 7 days, or last 30 days, as well as group activity changes, and password reset and registration activity.</span></span>

> [!NOTE]
> * <span data-ttu-id="a2522-115">일부 고급 비정상 보고서 및 리소스 사용 보고서는 [Azure Active Directory Premium](active-directory-get-started-premium.md)을 사용하도록 설정하는 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-115">Some advanced anomaly and resource usage reports are only available when you enable [Azure Active Directory Premium](active-directory-get-started-premium.md).</span></span> <span data-ttu-id="a2522-116">고급 보고서는 액세스 보안을 향상하고, 잠재적 위협에 대응하고, 장치 액세스 및 응용 프로그램 사용에 대한 진단에 액세스하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-116">Advanced reports help you improve access security, respond to potential threats and get access to analytics on device access and application usage.</span></span>
> * <span data-ttu-id="a2522-117">중국 고객의 경우 전 세계의 Azure Active Directory 인스턴스를 사용하여 Azure Active Directory Premium 및 Basic 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-117">Azure Active Directory Premium and Basic editions are available for customers in China using the worldwide instance of Azure Active Directory.</span></span> <span data-ttu-id="a2522-118">Azure Active Directory Premium 및 Basic 버전은 현재 중국 21Vianet이 운영하는 Microsoft Azure에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-118">Azure Active Directory Premium and Basic editions are not currently supported in the Microsoft Azure service operated by 21Vianet in China.</span></span> <span data-ttu-id="a2522-119">자세한 내용은 [Azure Active Directory 포럼](https://feedback.azure.com/forums/169401-azure-active-directory/)을 통해 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a2522-119">For more information, contact us at the [Azure Active Directory Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).</span></span>
> 
> 

## <a name="reports"></a><span data-ttu-id="a2522-120">보고서</span><span class="sxs-lookup"><span data-stu-id="a2522-120">Reports</span></span>
| <span data-ttu-id="a2522-121">보고서</span><span class="sxs-lookup"><span data-stu-id="a2522-121">Report</span></span> | <span data-ttu-id="a2522-122">설명</span><span class="sxs-lookup"><span data-stu-id="a2522-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a2522-123">**비정상적인 작업 보고서**</span><span class="sxs-lookup"><span data-stu-id="a2522-123">**Anomalous activity reports**</span></span> | |
| [<span data-ttu-id="a2522-124">알 수 없는 원본에서 로그인</span><span class="sxs-lookup"><span data-stu-id="a2522-124">Sign ins from unknown sources</span></span>](active-directory-reporting-sign-ins-from-unknown-sources.md) |<span data-ttu-id="a2522-125">추적 없이 로그인하려고 한 경우를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-125">May indicate an attempt to sign in without being traced.</span></span> |
| [<span data-ttu-id="a2522-126">여러 번의 실패 후 로그인</span><span class="sxs-lookup"><span data-stu-id="a2522-126">Sign ins after multiple failures</span></span>](active-directory-reporting-sign-ins-after-multiple-failures.md) |<span data-ttu-id="a2522-127">성공적인 무작위 공격을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-127">May indicate a successful brute force attack.</span></span> |
| [<span data-ttu-id="a2522-128">여러 지역에서의 로그인</span><span class="sxs-lookup"><span data-stu-id="a2522-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md) |<span data-ttu-id="a2522-129">여러 사용자가 같은 계정으로 로그인함을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-129">May indicate that multiple users are signing in with the same account.</span></span> |
| [<span data-ttu-id="a2522-130">의심스러운 활동을 포함하는 IP 주소의 로그인</span><span class="sxs-lookup"><span data-stu-id="a2522-130">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md) |<span data-ttu-id="a2522-131">지속적인된 침입 시도 후에 성공적인 로그인을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-131">May indicate a successful sign in after a sustained intrusion attempt.</span></span> |
| [<span data-ttu-id="a2522-132">감염 가능성이 있는 장치에서의 로그인</span><span class="sxs-lookup"><span data-stu-id="a2522-132">Sign ins from possibly infected devices</span></span>](active-directory-reporting-sign-ins-from-possibly-infected-devices.md) |<span data-ttu-id="a2522-133">감염 가능성이 있는 장치에서 로그인하려고 한 경우를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-133">May indicate an attempt to sign in from possibly infected devices.</span></span> |
| [<span data-ttu-id="a2522-134">비정상적인 로그인 활동</span><span class="sxs-lookup"><span data-stu-id="a2522-134">Irregular sign in activity</span></span>](active-directory-reporting-irregular-sign-in-activity.md) |<span data-ttu-id="a2522-135">사용자의 로그인 패턴에 대한 비정상적인 이벤트를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-135">May indicate events anomalous to users’ sign in patterns.</span></span> |
| [<span data-ttu-id="a2522-136">비정상적인 로그인 활동을 포함하는 사용자 보고서</span><span class="sxs-lookup"><span data-stu-id="a2522-136">Users with anomalous sign in activity</span></span>](active-directory-reporting-users-with-anomalous-sign-in-activity.md) |<span data-ttu-id="a2522-137">손상된 계정을 가진 사용자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-137">Indicates users whose accounts may have been compromised.</span></span> |
| <span data-ttu-id="a2522-138">자격 증명이 손실된 사용자</span><span class="sxs-lookup"><span data-stu-id="a2522-138">Users with leaked credentials</span></span> |<span data-ttu-id="a2522-139">자격 증명이 손실된 사용자</span><span class="sxs-lookup"><span data-stu-id="a2522-139">Users with leaked credentials</span></span> |
| <span data-ttu-id="a2522-140">**활동 로그**</span><span class="sxs-lookup"><span data-stu-id="a2522-140">**Activity logs**</span></span> | |
| <span data-ttu-id="a2522-141">감사 보고서</span><span class="sxs-lookup"><span data-stu-id="a2522-141">Audit report</span></span> |<span data-ttu-id="a2522-142">디렉토리에서 감사된 이벤트</span><span class="sxs-lookup"><span data-stu-id="a2522-142">Audited events in your directory</span></span> |
| <span data-ttu-id="a2522-143">암호 재설정 활동</span><span class="sxs-lookup"><span data-stu-id="a2522-143">Password reset activity</span></span> |<span data-ttu-id="a2522-144">조직에서 발생하는 암호 재설정의 세부 정보 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-144">Provides a detailed view of password resets that occur in your organization.</span></span> |
| <span data-ttu-id="a2522-145">암호 재설정 등록 활동</span><span class="sxs-lookup"><span data-stu-id="a2522-145">Password reset registration activity</span></span> |<span data-ttu-id="a2522-146">조직에서 발생하는 암호 재설정 등록의 세부 정보 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-146">Provides a detailed view of password reset registrations that occur in your organization.</span></span> |
| <span data-ttu-id="a2522-147">셀프 서비스 그룹 활동</span><span class="sxs-lookup"><span data-stu-id="a2522-147">Self service groups activity</span></span> |<span data-ttu-id="a2522-148">사용자 디렉토리의 모든 그룹 자체 서비스 활동에 대한 활동 로그를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-148">Provides an activity log to all group self service activity in your directory</span></span> |
| <span data-ttu-id="a2522-149">**통합된 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="a2522-149">**Integrated applications**</span></span> | |
| <span data-ttu-id="a2522-150">응용 프로그램 사용 현황</span><span class="sxs-lookup"><span data-stu-id="a2522-150">Application usage</span></span> |<span data-ttu-id="a2522-151">디렉토리와 통합하는 모든 SaaS 응용 프로그램에 대한 사용 현황 요약을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-151">Provides a usage summary for all SaaS applications integrated with your directory.</span></span> |
| <span data-ttu-id="a2522-152">계정 프로비전 활동</span><span class="sxs-lookup"><span data-stu-id="a2522-152">Account provisioning activity</span></span> |<span data-ttu-id="a2522-153">외부 응용 프로그램에 계정을 프로비전하려는 시도의 기록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-153">Provides a history of attempts to provision accounts to external applications.</span></span> |
| <span data-ttu-id="a2522-154">암호 롤오버 상태</span><span class="sxs-lookup"><span data-stu-id="a2522-154">Password rollover status</span></span> |<span data-ttu-id="a2522-155">SaaS 응용 프로그램의 자동 암호 롤오버 상태의 자세한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-155">Provides a detailed overview of automatic password rollover status of SaaS applications.</span></span> |
| <span data-ttu-id="a2522-156">계정 프로비전 오류</span><span class="sxs-lookup"><span data-stu-id="a2522-156">Account provisioning errors</span></span> |<span data-ttu-id="a2522-157">외부 응용 프로그램에 대한 사용자의 액세스에 대한 영향을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-157">Indicates an impact to users’ access to external applications.</span></span> |
| <span data-ttu-id="a2522-158">**권한 관리**</span><span class="sxs-lookup"><span data-stu-id="a2522-158">**Rights management**</span></span> | |
| <span data-ttu-id="a2522-159">RMS 사용 현황</span><span class="sxs-lookup"><span data-stu-id="a2522-159">RMS usage</span></span> |<span data-ttu-id="a2522-160">권한 관리 사용 현황에 대한 요약을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-160">Provides a summary for Rights Management usage</span></span> |
| <span data-ttu-id="a2522-161">가장 활동적인 RMS 사용자</span><span class="sxs-lookup"><span data-stu-id="a2522-161">Most active RMS users</span></span> |<span data-ttu-id="a2522-162">RMS로 보호된 파일에 액세스하는 상위 1000명의 활성 사용자를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-162">Lists top 1000 active users who accessed RMS-protected files</span></span> |
| <span data-ttu-id="a2522-163">RMS 장치 사용</span><span class="sxs-lookup"><span data-stu-id="a2522-163">RMS device usage</span></span> |<span data-ttu-id="a2522-164">RMS로 보호된 파일에 액세스하는 데 사용된 장치를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-164">Lists devices used for accessing RMS-protected files</span></span> |
| <span data-ttu-id="a2522-165">RMS 사용 응용 프로그램 사용 현황</span><span class="sxs-lookup"><span data-stu-id="a2522-165">RMS enabled application usage</span></span> |<span data-ttu-id="a2522-166">RMS 사용 응용 프로그램의 사용 현황을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-166">Provides usage of RMS enabled applications</span></span> |

## <a name="report-editions"></a><span data-ttu-id="a2522-167">보고서 버전</span><span class="sxs-lookup"><span data-stu-id="a2522-167">Report editions</span></span>
| <span data-ttu-id="a2522-168">보고서</span><span class="sxs-lookup"><span data-stu-id="a2522-168">Report</span></span> | <span data-ttu-id="a2522-169">무료</span><span class="sxs-lookup"><span data-stu-id="a2522-169">Free</span></span> | <span data-ttu-id="a2522-170">Basic</span><span class="sxs-lookup"><span data-stu-id="a2522-170">Basic</span></span> | <span data-ttu-id="a2522-171">Premium</span><span class="sxs-lookup"><span data-stu-id="a2522-171">Premium</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a2522-172">**비정상적인 작업 보고서**</span><span class="sxs-lookup"><span data-stu-id="a2522-172">**Anomalous activity reports**</span></span> | | | |
| <span data-ttu-id="a2522-173">알 수 없는 원본에서 로그인</span><span class="sxs-lookup"><span data-stu-id="a2522-173">Sign ins from unknown sources</span></span> |<span data-ttu-id="a2522-174">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-174">✓</span></span> |<span data-ttu-id="a2522-175">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-175">✓</span></span> |<span data-ttu-id="a2522-176">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-176">✓</span></span> |
| <span data-ttu-id="a2522-177">여러 번의 실패 후 로그인</span><span class="sxs-lookup"><span data-stu-id="a2522-177">Sign ins after multiple failures</span></span> |<span data-ttu-id="a2522-178">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-178">✓</span></span> |<span data-ttu-id="a2522-179">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-179">✓</span></span> |<span data-ttu-id="a2522-180">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-180">✓</span></span> |
| <span data-ttu-id="a2522-181">여러 지역에서의 로그인</span><span class="sxs-lookup"><span data-stu-id="a2522-181">Sign ins from multiple geographies</span></span> |<span data-ttu-id="a2522-182">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-182">✓</span></span> |<span data-ttu-id="a2522-183">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-183">✓</span></span> |<span data-ttu-id="a2522-184">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-184">✓</span></span> |
| <span data-ttu-id="a2522-185">의심스러운 활동을 포함하는 IP 주소의 로그인</span><span class="sxs-lookup"><span data-stu-id="a2522-185">Sign ins from IP addresses with suspicious activity</span></span> | | |<span data-ttu-id="a2522-186">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-186">✓</span></span> |
| <span data-ttu-id="a2522-187">감염 가능성이 있는 장치에서의 로그인</span><span class="sxs-lookup"><span data-stu-id="a2522-187">Sign ins from possibly infected devices</span></span> | | |<span data-ttu-id="a2522-188">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-188">✓</span></span> |
| <span data-ttu-id="a2522-189">비정상적인 로그인 활동</span><span class="sxs-lookup"><span data-stu-id="a2522-189">Irregular sign in activity</span></span> | | |<span data-ttu-id="a2522-190">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-190">✓</span></span> |
| <span data-ttu-id="a2522-191">비정상적인 로그인 활동을 포함하는 사용자 보고서</span><span class="sxs-lookup"><span data-stu-id="a2522-191">Users with anomalous sign in activity</span></span> | | |<span data-ttu-id="a2522-192">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-192">✓</span></span> |
| <span data-ttu-id="a2522-193">자격 증명이 손실된 사용자</span><span class="sxs-lookup"><span data-stu-id="a2522-193">Users with leaked credentials</span></span> | | |<span data-ttu-id="a2522-194">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-194">✓</span></span> |
| <span data-ttu-id="a2522-195">**활동 로그**</span><span class="sxs-lookup"><span data-stu-id="a2522-195">**Activity logs**</span></span> | | | |
| <span data-ttu-id="a2522-196">감사 보고서</span><span class="sxs-lookup"><span data-stu-id="a2522-196">Audit report</span></span> |<span data-ttu-id="a2522-197">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-197">✓</span></span> |<span data-ttu-id="a2522-198">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-198">✓</span></span> |<span data-ttu-id="a2522-199">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-199">✓</span></span> |
| <span data-ttu-id="a2522-200">암호 재설정 활동</span><span class="sxs-lookup"><span data-stu-id="a2522-200">Password reset activity</span></span> | | |<span data-ttu-id="a2522-201">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-201">✓</span></span> |
| <span data-ttu-id="a2522-202">암호 재설정 등록 활동</span><span class="sxs-lookup"><span data-stu-id="a2522-202">Password reset registration activity</span></span> | | |<span data-ttu-id="a2522-203">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-203">✓</span></span> |
| <span data-ttu-id="a2522-204">셀프 서비스 그룹 활동</span><span class="sxs-lookup"><span data-stu-id="a2522-204">Self service groups activity</span></span> | | |<span data-ttu-id="a2522-205">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-205">✓</span></span> |
| <span data-ttu-id="a2522-206">**통합된 응용 프로그램**</span><span class="sxs-lookup"><span data-stu-id="a2522-206">**Integrated applications**</span></span> | | | |
| <span data-ttu-id="a2522-207">응용 프로그램 사용 현황</span><span class="sxs-lookup"><span data-stu-id="a2522-207">Application usage</span></span> | | |<span data-ttu-id="a2522-208">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-208">✓</span></span> |
| <span data-ttu-id="a2522-209">계정 프로비전 활동</span><span class="sxs-lookup"><span data-stu-id="a2522-209">Account provisioning activity</span></span> |<span data-ttu-id="a2522-210">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-210">✓</span></span> |<span data-ttu-id="a2522-211">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-211">✓</span></span> |<span data-ttu-id="a2522-212">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-212">✓</span></span> |
| <span data-ttu-id="a2522-213">암호 롤오버 상태</span><span class="sxs-lookup"><span data-stu-id="a2522-213">Password rollover status</span></span> | | |<span data-ttu-id="a2522-214">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-214">✓</span></span> |
| <span data-ttu-id="a2522-215">계정 프로비전 오류</span><span class="sxs-lookup"><span data-stu-id="a2522-215">Account provisioning errors</span></span> |<span data-ttu-id="a2522-216">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-216">✓</span></span> |<span data-ttu-id="a2522-217">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-217">✓</span></span> |<span data-ttu-id="a2522-218">✓</span><span class="sxs-lookup"><span data-stu-id="a2522-218">✓</span></span> |
| <span data-ttu-id="a2522-219">**권한 관리**</span><span class="sxs-lookup"><span data-stu-id="a2522-219">**Rights managment**</span></span> | | | |
| <span data-ttu-id="a2522-220">RMS 사용 현황</span><span class="sxs-lookup"><span data-stu-id="a2522-220">RMS usage</span></span> | | |<span data-ttu-id="a2522-221">RMS만 해당</span><span class="sxs-lookup"><span data-stu-id="a2522-221">RMS Only</span></span> |
| <span data-ttu-id="a2522-222">가장 활동적인 RMS 사용자</span><span class="sxs-lookup"><span data-stu-id="a2522-222">Most active RMS users</span></span> | | |<span data-ttu-id="a2522-223">RMS만 해당</span><span class="sxs-lookup"><span data-stu-id="a2522-223">RMS Only</span></span> |
| <span data-ttu-id="a2522-224">RMS 장치 사용</span><span class="sxs-lookup"><span data-stu-id="a2522-224">RMS device usage</span></span> | | |<span data-ttu-id="a2522-225">RMS만 해당</span><span class="sxs-lookup"><span data-stu-id="a2522-225">RMS Only</span></span> |
| <span data-ttu-id="a2522-226">RMS 사용 응용 프로그램 사용 현황</span><span class="sxs-lookup"><span data-stu-id="a2522-226">RMS enabled application usage</span></span> | | |<span data-ttu-id="a2522-227">RMS만 해당</span><span class="sxs-lookup"><span data-stu-id="a2522-227">RMS Only</span></span> |

## <a name="anomalous-activity-reports"></a><span data-ttu-id="a2522-228">비정상적인 활동 보고서</span><span class="sxs-lookup"><span data-stu-id="a2522-228">Anomalous activity reports</span></span>
<p><span data-ttu-id="a2522-229">비정상적인 로그인 활동 보고서는 Office365, Azure 관리 포털, Azure AD 액세스 패널, Sharepoint Online, Dynamics CRM Online 및 기타 Microsoft 온라인 서비스에 대한 의심스러운 로그인 활동에 플래그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-229">The anomalous sign in activity reports flag suspicious sign in activity to Office365, Azure Management Portal, Azure AD Access Panel, Sharepoint Online, Dynamics CRM Online, and other Microsoft online services.</span></span></p>

<p><span data-ttu-id="a2522-230">"여러 번의 실패 후 로그인" 보고서를 제외하고 이러한 모든 보고서는 페더레이션 공급자에 관계없이 앞서 언급한 서비스에 대한 의심스러운 <i>페더레이션</i> 로그인에도 플래그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-230">All of these reports, except the "Sign ins after multiple failures" report, also flag suspicious <i>federated</i> sign ins to the aforementioned services, regardless of the federation provider.</span></span> </p>

<p><span data-ttu-id="a2522-231">사용할 수 있는 보고서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-231">The following reports are available:</span></span> </p><ul>

<li><span data-ttu-id="a2522-232">[알 수 없는 원본에서 로그인](active-directory-reporting-sign-ins-from-unknown-sources.md)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-232">[Sign ins from unknown sources](active-directory-reporting-sign-ins-from-unknown-sources.md).</span></span></li>

<li><span data-ttu-id="a2522-233">[여러 번의 실패 후 로그인](active-directory-reporting-sign-ins-after-multiple-failures의 일부입니다.md)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-233">[Sign ins after multiple failures](active-directory-reporting-sign-ins-after-multiple-failures.md).</span></span></li>

<li><span data-ttu-id="a2522-234">[여러 지역에서의 로그인](active-directory-reporting-sign-ins-from-multiple-geographies의 일부입니다.md)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-234">[Sign ins from multiple geographies](active-directory-reporting-sign-ins-from-multiple-geographies.md).</span></span></li>

<li><span data-ttu-id="a2522-235">[의심스러운 활동을 포함하는 IP 주소의 로그인](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity의 일부입니다.md)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-235">[Sign ins from IP addresses with suspicious activity](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md).</span></span></li>

<li><span data-ttu-id="a2522-236">[비정상적인 로그인 활동](active-directory-reporting-irregular-sign-in-activity의 일부입니다.md)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-236">[Irregular sign in activity](active-directory-reporting-irregular-sign-in-activity.md).</span></span></li>

<li><span data-ttu-id="a2522-237">[감염 가능성이 있는 장치에서의 로그인](active-directory-reporting-sign-ins-from-possibly-infected-devices의 일부입니다.md)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-237">[Sign ins from possibly infected devices](active-directory-reporting-sign-ins-from-possibly-infected-devices.md).</span></span></li>

<li><span data-ttu-id="a2522-238">[비정상적인 로그인 활동을 포함하는 사용자 보고서](active-directory-reporting-users-with-anomalous-sign-in-activity.md)의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-238">[Users with anomalous sign in activity](active-directory-reporting-users-with-anomalous-sign-in-activity.md).</span></span></li>

<li><span data-ttu-id="a2522-239">자격 증명이 손실된 사용자</span><span class="sxs-lookup"><span data-stu-id="a2522-239">Users with leaked credentials</span></span></li></ul>

## <a name="activity-logs"></a><span data-ttu-id="a2522-240">활동 로그</span><span class="sxs-lookup"><span data-stu-id="a2522-240">Activity logs</span></span>
### <a name="audit-report"></a><span data-ttu-id="a2522-241">감사 보고서</span><span class="sxs-lookup"><span data-stu-id="a2522-241">Audit report</span></span>
| <span data-ttu-id="a2522-242">설명</span><span class="sxs-lookup"><span data-stu-id="a2522-242">Description</span></span> | <span data-ttu-id="a2522-243">보고서 위치</span><span class="sxs-lookup"><span data-stu-id="a2522-243">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="a2522-244">최근 24시간, 최근 7일 또는 최근 30일 내에 감사된 모든 이벤트의 레코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-244">Shows a record of all audited events within the last 24 hours, last 7 days, or last 30 days.</span></span> <br /> <span data-ttu-id="a2522-245">자세한 내용은 [Azure Active Directory 감사 보고서 이벤트](active-directory-reporting-audit-events.md)</span><span class="sxs-lookup"><span data-stu-id="a2522-245">For more information, see [Azure Active Directory Audit Report Events](active-directory-reporting-audit-events.md)</span></span> |<span data-ttu-id="a2522-246">디렉터리 > 보고서 탭</span><span class="sxs-lookup"><span data-stu-id="a2522-246">Directory > Reports tab</span></span> |

![감사 보고서](./media/active-directory-view-access-usage-reports/auditReport.PNG)

### <a name="password-reset-activity"></a><span data-ttu-id="a2522-248">암호 재설정 활동</span><span class="sxs-lookup"><span data-stu-id="a2522-248">Password reset activity</span></span>
| <span data-ttu-id="a2522-249">설명</span><span class="sxs-lookup"><span data-stu-id="a2522-249">Description</span></span> | <span data-ttu-id="a2522-250">보고서 위치</span><span class="sxs-lookup"><span data-stu-id="a2522-250">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="a2522-251">조직 내에서 발생한 모든 암호 재설정 시도를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-251">Shows all password reset attempts that have occurred in your organization.</span></span> |<span data-ttu-id="a2522-252">디렉터리 > 보고서 탭</span><span class="sxs-lookup"><span data-stu-id="a2522-252">Directory > Reports tab</span></span> |

![암호 재설정 활동](./media/active-directory-view-access-usage-reports/passwordResetActivity.PNG)

### <a name="password-reset-registration-activity"></a><span data-ttu-id="a2522-254">암호 재설정 등록 활동</span><span class="sxs-lookup"><span data-stu-id="a2522-254">Password reset registration activity</span></span>
| <span data-ttu-id="a2522-255">설명</span><span class="sxs-lookup"><span data-stu-id="a2522-255">Description</span></span> | <span data-ttu-id="a2522-256">보고서 위치</span><span class="sxs-lookup"><span data-stu-id="a2522-256">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="a2522-257">조직 내에서 발생한 모든 암호 재설정 등록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-257">Shows all password reset registrations that have occurred in your organization</span></span> |<span data-ttu-id="a2522-258">디렉터리 > 보고서 탭</span><span class="sxs-lookup"><span data-stu-id="a2522-258">Directory > Reports tab</span></span> |

![암호 재설정 등록 활동](./media/active-directory-view-access-usage-reports/passwordResetRegistrationActivity.PNG)

### <a name="self-service-groups-activity"></a><span data-ttu-id="a2522-260">셀프 서비스 그룹 활동</span><span class="sxs-lookup"><span data-stu-id="a2522-260">Self service groups activity</span></span>
| <span data-ttu-id="a2522-261">설명</span><span class="sxs-lookup"><span data-stu-id="a2522-261">Description</span></span> | <span data-ttu-id="a2522-262">보고서 위치</span><span class="sxs-lookup"><span data-stu-id="a2522-262">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="a2522-263">디렉터리의 셀프 서비스 관리 그룹에 대한 모든 활동을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-263">Shows all activity for the self-service managed groups in your directory.</span></span> |<span data-ttu-id="a2522-264">디렉터리 > 사용자 > <i>사용자</i> > 장치 탭</span><span class="sxs-lookup"><span data-stu-id="a2522-264">Directory > Users > <i>User</i> > Devices tab</span></span> |

![셀프 서비스 그룹 활동](./media/active-directory-view-access-usage-reports/selfServiceGroupsActivity.PNG)

## <a name="integrated-applications-reports"></a><span data-ttu-id="a2522-266">통합된 응용 프로그램 보고서</span><span class="sxs-lookup"><span data-stu-id="a2522-266">Integrated applications reports</span></span>
### <a name="application-usage-summary"></a><span data-ttu-id="a2522-267">응용 프로그램 사용: 요약</span><span class="sxs-lookup"><span data-stu-id="a2522-267">Application usage: summary</span></span>
| <span data-ttu-id="a2522-268">설명</span><span class="sxs-lookup"><span data-stu-id="a2522-268">Description</span></span> | <span data-ttu-id="a2522-269">보고서 위치</span><span class="sxs-lookup"><span data-stu-id="a2522-269">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="a2522-270">디렉터리에서의 모든 SaaS 응용 프로그램에 대한 사용 현황을 확인하려는 경우 이 보고서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-270">Use this report when you want to see usage for all the SaaS applications in your directory.</span></span> <span data-ttu-id="a2522-271">이 보고서는 액세스 패널에서 해당 응용 프로그램을 클릭한 횟수를 기반으로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-271">This report is based on the number of times users have clicked on the application in the Access Panel.</span></span> |<span data-ttu-id="a2522-272">디렉터리 > 보고서 탭</span><span class="sxs-lookup"><span data-stu-id="a2522-272">Directory > Reports tab</span></span> |

<span data-ttu-id="a2522-273">이 보고서에는 사전 통합된 Microsoft 응용 프로그램을 비롯하여 디렉터리에 액세스 권한이 있는 *모든* 응용 프로그램에 대한 로그인이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-273">This report includes sign ins to *all* applications that your directory has access to, including pre-integrated Microsoft applications.</span></span>

<span data-ttu-id="a2522-274">사전 통합된 Microsoft 응용 프로그램에는 Office 365, Sharepoint, Azure 관리 포털 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-274">Pre-integrated Microsoft applications include Office 365, Sharepoint, the Azure Management Portal, and others.</span></span>

![응용 프로그램 사용 요약](./media/active-directory-view-access-usage-reports/applicationUsage.PNG)

### <a name="application-usage-detailed"></a><span data-ttu-id="a2522-276">응용 프로그램 사용: 세부</span><span class="sxs-lookup"><span data-stu-id="a2522-276">Application usage: detailed</span></span>
| <span data-ttu-id="a2522-277">설명</span><span class="sxs-lookup"><span data-stu-id="a2522-277">Description</span></span> | <span data-ttu-id="a2522-278">보고서 위치</span><span class="sxs-lookup"><span data-stu-id="a2522-278">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="a2522-279">특정 SaaS 응용 프로그램이 어느 정도 사용되고 있는지 확인하려는 경우 이 보고서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-279">Use this report when you want to see how much a specific SaaS application is being used.</span></span> <span data-ttu-id="a2522-280">이 보고서는 액세스 패널에서 해당 응용 프로그램을 클릭한 횟수를 기반으로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-280">This report is based on the number of times users have clicked on the application in the Access Panel.</span></span> |<span data-ttu-id="a2522-281">디렉터리 > 보고서 탭</span><span class="sxs-lookup"><span data-stu-id="a2522-281">Directory > Reports tab</span></span> |

### <a name="application-dashboard"></a><span data-ttu-id="a2522-282">응용 프로그램 대시보드</span><span class="sxs-lookup"><span data-stu-id="a2522-282">Application dashboard</span></span>
| <span data-ttu-id="a2522-283">설명</span><span class="sxs-lookup"><span data-stu-id="a2522-283">Description</span></span> | <span data-ttu-id="a2522-284">보고서 위치</span><span class="sxs-lookup"><span data-stu-id="a2522-284">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="a2522-285">이 보고서는 선택한 시간 간격 동안 조직 사용자의 누적 응용 프로그램 로그인을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-285">This report indicates cumulative sign ins to the application by users in your organization, over a selected time interval.</span></span> <span data-ttu-id="a2522-286">대시보드 페이지의 차트는 해당 응용 프로그램의 모든 사용 추세를 식별하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-286">The chart on the dashboard page will help you identify trends for all usage of that application.</span></span> |<span data-ttu-id="a2522-287">디렉터리 > 응용 프로그램 > 대시보드 탭</span><span class="sxs-lookup"><span data-stu-id="a2522-287">Directory > Application > Dashboard tab</span></span> |

## <a name="error-reports"></a><span data-ttu-id="a2522-288">오류 보고서</span><span class="sxs-lookup"><span data-stu-id="a2522-288">Error reports</span></span>
### <a name="account-provisioning-errors"></a><span data-ttu-id="a2522-289">계정 프로비전 오류</span><span class="sxs-lookup"><span data-stu-id="a2522-289">Account provisioning errors</span></span>
| <span data-ttu-id="a2522-290">설명</span><span class="sxs-lookup"><span data-stu-id="a2522-290">Description</span></span> | <span data-ttu-id="a2522-291">보고서 위치</span><span class="sxs-lookup"><span data-stu-id="a2522-291">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="a2522-292">이 보고서를 사용하면 SaaS 응용 프로그램에서 Azure Active Directory로의 계정 동기화 중에 발생한 오류를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-292">Use this to monitor errors that occur during the synchronization of accounts from SaaS applications to Azure Active Directory.</span></span> |<span data-ttu-id="a2522-293">디렉터리 > 보고서 탭</span><span class="sxs-lookup"><span data-stu-id="a2522-293">Directory > Reports tab</span></span> |

![계정 프로비전 오류](./media/active-directory-view-access-usage-reports/accountProvisioningErrors.PNG)

## <a name="user-specific-reports"></a><span data-ttu-id="a2522-295">사용자별 보고서</span><span class="sxs-lookup"><span data-stu-id="a2522-295">User-specific reports</span></span>
### <a name="devices"></a><span data-ttu-id="a2522-296">장치</span><span class="sxs-lookup"><span data-stu-id="a2522-296">Devices</span></span>
| <span data-ttu-id="a2522-297">설명</span><span class="sxs-lookup"><span data-stu-id="a2522-297">Description</span></span> | <span data-ttu-id="a2522-298">보고서 위치</span><span class="sxs-lookup"><span data-stu-id="a2522-298">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="a2522-299">특정 사용자가 Azure Active Directory에 액세스하는 데 사용한 장치의 IP 주소 및 지리적 위치를 확인하려는 경우 이 보고서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-299">Use this report when you want to see the IP address and geographical location of devices that a specific user has used to access Azure Active Directory.</span></span> |<span data-ttu-id="a2522-300">디렉터리 > 사용자 > <i>사용자</i> > 장치 탭</span><span class="sxs-lookup"><span data-stu-id="a2522-300">Directory > Users > <i>User</i> > Devices tab</span></span> |

### <a name="activity"></a><span data-ttu-id="a2522-301">작업</span><span class="sxs-lookup"><span data-stu-id="a2522-301">Activity</span></span>
| <span data-ttu-id="a2522-302">설명</span><span class="sxs-lookup"><span data-stu-id="a2522-302">Description</span></span> | <span data-ttu-id="a2522-303">보고서 위치</span><span class="sxs-lookup"><span data-stu-id="a2522-303">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="a2522-304">사용자에 대한 로그인 활동을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-304">Shows the sign in activity for a user.</span></span> <span data-ttu-id="a2522-305">보고서에는 로그인한 응용 프로그램, 사용한 장치, IP 주소, 위치 등의 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-305">The report includes information like the application signed into, device used, IP address, and location.</span></span> <span data-ttu-id="a2522-306">Microsoft 계정으로 로그인하는 사용자에 대한 기록은 수집되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-306">We do not collect the history for users that sign in with a Microsoft account.</span></span> |<span data-ttu-id="a2522-307">디렉터리 > 사용자 > <i>사용자</i> > 활동 탭</span><span class="sxs-lookup"><span data-stu-id="a2522-307">Directory > Users > <i>User</i> > Activity tab</span></span> |

#### <a name="sign-in-events-included-in-the-user-activity-report"></a><span data-ttu-id="a2522-308">사용자 활동 보고서에 포함된 로그인 이벤트</span><span class="sxs-lookup"><span data-stu-id="a2522-308">Sign in events included in the User Activity report</span></span>
<span data-ttu-id="a2522-309">특정 유형의 로그인 이벤트만 사용자 활동 보고서에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-309">Only certain types of sign in events will appear in the User Activity report.</span></span>

| <span data-ttu-id="a2522-310">이벤트 유형</span><span class="sxs-lookup"><span data-stu-id="a2522-310">Event type</span></span> | <span data-ttu-id="a2522-311">포함 여부</span><span class="sxs-lookup"><span data-stu-id="a2522-311">Included?</span></span> |
| --- | --- |
| <span data-ttu-id="a2522-312">[액세스 패널](http://myapps.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="a2522-312">Sign ins to the [Access Panel](http://myapps.microsoft.com/)</span></span> |<span data-ttu-id="a2522-313">예</span><span class="sxs-lookup"><span data-stu-id="a2522-313">Yes</span></span> |
| <span data-ttu-id="a2522-314">[Azure 관리 포털](https://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="a2522-314">Sign ins to the [Azure Management Portal](https://manage.windowsazure.com/)</span></span> |<span data-ttu-id="a2522-315">예</span><span class="sxs-lookup"><span data-stu-id="a2522-315">Yes</span></span> |
| <span data-ttu-id="a2522-316">[Microsoft Azure 포털](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="a2522-316">Sign ins to the [Microsoft Azure Portal](https://portal.azure.com/)</span></span> |<span data-ttu-id="a2522-317">예</span><span class="sxs-lookup"><span data-stu-id="a2522-317">Yes</span></span> |
| <span data-ttu-id="a2522-318">[Office 365 포털](http://portal.office.com/)</span><span class="sxs-lookup"><span data-stu-id="a2522-318">Sign ins to the [Office 365 portal](http://portal.office.com/)</span></span> |<span data-ttu-id="a2522-319">예</span><span class="sxs-lookup"><span data-stu-id="a2522-319">Yes</span></span> |
| <span data-ttu-id="a2522-320">Outlook 같은 네이티브 응용 프로그램에 로그인(아래 예외 참조)</span><span class="sxs-lookup"><span data-stu-id="a2522-320">Sign ins to a native application, like Outlook (see exception below)</span></span> |<span data-ttu-id="a2522-321">예</span><span class="sxs-lookup"><span data-stu-id="a2522-321">Yes</span></span> |
| <span data-ttu-id="a2522-322">Salesforce 같은 액세스 패널을 통해 페더레이션/프로 비전된 응용 프로그램에 로그인</span><span class="sxs-lookup"><span data-stu-id="a2522-322">Sign ins to a federated/provisioned app through the Access Panel, like Salesforce</span></span> |<span data-ttu-id="a2522-323">예</span><span class="sxs-lookup"><span data-stu-id="a2522-323">Yes</span></span> |
| <span data-ttu-id="a2522-324">Twitter 같은 액세스 패널을 통해 암호 기반 응용 프로그램에 로그인</span><span class="sxs-lookup"><span data-stu-id="a2522-324">Sign ins to a password-based app through the Access Panel, like Twitter</span></span> |<span data-ttu-id="a2522-325">예</span><span class="sxs-lookup"><span data-stu-id="a2522-325">Yes</span></span> |
| <span data-ttu-id="a2522-326">디렉터리에 추가된 사용자 지정 비즈니스 응용 프로그램에 로그인</span><span class="sxs-lookup"><span data-stu-id="a2522-326">Sign ins to a custom business app that has been added to the directory</span></span> |<span data-ttu-id="a2522-327">아니요(포함 예정)</span><span class="sxs-lookup"><span data-stu-id="a2522-327">No (Coming soon)</span></span> |
| <span data-ttu-id="a2522-328">디렉토리에 추가된 Azure AD 응용 프로그램 프록시 앱에 로그인</span><span class="sxs-lookup"><span data-stu-id="a2522-328">Sign ins to an Azure AD Application Proxy app that has been added to the directory</span></span> |<span data-ttu-id="a2522-329">아니요(포함 예정)</span><span class="sxs-lookup"><span data-stu-id="a2522-329">No (Coming soon)</span></span> |

> <span data-ttu-id="a2522-330">참고: 이 보고서의 노이즈를 줄이기 위해 [Microsoft Online Services 로그인 도우미](http://community.office365.com/en-us/w/sso/534.aspx) 를 통한 로그인은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-330">Note: To reduce the amount of noise in this report, sign ins by the [Microsoft Online Services Sign-In Assistant](http://community.office365.com/en-us/w/sso/534.aspx) are not shown.</span></span>
> 
> 

## <a name="things-to-consider-if-you-suspect-security-breach"></a><span data-ttu-id="a2522-331">보안 위반이 의심될 때 고려할 사항</span><span class="sxs-lookup"><span data-stu-id="a2522-331">Things to consider if you suspect security breach</span></span>
<span data-ttu-id="a2522-332">사용자 계정이 손상되었다고 의심되거나 클라우드에서 디렉터리 데이터의 보안 위반을 초래할 수 있는 의심스러운 사용자 활동이 있는 경우 다음 작업 중 하나 이상을 고려하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-332">If you suspect that a user account may be compromised or any kind of suspicious user activity that may lead to a security breach of your directory data in the cloud, you may want to consider one or more of the following actions:</span></span>

* <span data-ttu-id="a2522-333">사용자에게 연락하여 활동 확인</span><span class="sxs-lookup"><span data-stu-id="a2522-333">Contact the user to verify the activity</span></span>
* <span data-ttu-id="a2522-334">사용자 암호 재설정</span><span class="sxs-lookup"><span data-stu-id="a2522-334">Reset the user's password</span></span>
* <span data-ttu-id="a2522-335">[다단계 인증](../multi-factor-authentication/multi-factor-authentication-get-started.md) 사용</span><span class="sxs-lookup"><span data-stu-id="a2522-335">[Enable multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md) for additional security</span></span>

## <a name="view-or-download-a-report"></a><span data-ttu-id="a2522-336">보고서 보기 또는 다운로드</span><span class="sxs-lookup"><span data-stu-id="a2522-336">View or download a report</span></span>
1. <span data-ttu-id="a2522-337">Azure 클래식 포털에서 **Active Directory**를 클릭하고 조직의 디렉터리 이름을 클릭한 다음 **보고서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-337">In the Azure classic portal, click **Active Directory**, click the name of your organization’s directory, and then click **Reports**.</span></span>
2. <span data-ttu-id="a2522-338">보고서 페이지에서 보거나 다운로드하려는 보고서를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-338">On the Reports page, click the report you want to view and/or download.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a2522-339">처음으로 Azure Active Directory의 보고 기능을 사용하는 경우 옵트인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-339">If this is the first time you have used the reporting feature of Azure Active Directory, you will see a message to Opt In.</span></span> <span data-ttu-id="a2522-340">동의하는 경우 계속하려면 확인 표시 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-340">If you agree, click the check mark icon to continue.</span></span>
   > 
   > 
3. <span data-ttu-id="a2522-341">간격 옆의 드롭다운 메뉴를 클릭한 후 이 보고서를 생성할 때 사용해야 하는 다음 시간 범위 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-341">Click the drop-down menu next to Interval, and then select one of the following time ranges that should be used when generating this report:</span></span>
   
   * <span data-ttu-id="a2522-342">최근 24시간</span><span class="sxs-lookup"><span data-stu-id="a2522-342">Last 24 hours</span></span>
   * <span data-ttu-id="a2522-343">최근 7일</span><span class="sxs-lookup"><span data-stu-id="a2522-343">Last 7 days</span></span>
   * <span data-ttu-id="a2522-344">최근 30일</span><span class="sxs-lookup"><span data-stu-id="a2522-344">Last 30 days</span></span>
4. <span data-ttu-id="a2522-345">확인 표시 아이콘을 클릭하여 보고서를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-345">Click the check mark icon to run the report.</span></span>
   * <span data-ttu-id="a2522-346">최대 1000개의 이벤트가 Azure 클래식 포털에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-346">Up to 1000 events will be shown in the Azure classic portal.</span></span>
5. <span data-ttu-id="a2522-347">해당하는 경우 **다운로드** 를 클릭하여 오프라인으로 보거나 보관하기 위해 CSV(쉼표로 구분된 값) 형식의 압축 파일로 보고서를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-347">If applicable, click **Download** to download the report to a compressed file in comma-separated values (CSV) format for offline viewing or archiving purposes.</span></span>
   * <span data-ttu-id="a2522-348">최대 75,000개의 이벤트가 다운로드한 파일에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-348">Up to 75,000 events will be included in the downloaded file.</span></span>
   * <span data-ttu-id="a2522-349">더 많은 데이터는 [Azure AD Reporting API](active-directory-reporting-api-getting-started.md)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="a2522-349">For more data, check out the [Azure AD Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

## <a name="ignore-an-event"></a><span data-ttu-id="a2522-350">이벤트 무시</span><span class="sxs-lookup"><span data-stu-id="a2522-350">Ignore an event</span></span>
<span data-ttu-id="a2522-351">비정상 보고서를 본다면 관련 보고서에 표시된 다양한 이벤트를 무시할 수 있다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-351">If you are viewing any anomaly reports, you may notice that you can ignore various events that show up in related reports.</span></span> <span data-ttu-id="a2522-352">이벤트를 무시하려면 보고서에서 해당 이벤트를 강조 표시한 후 **무시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-352">To ignore an event, simply highlight the event in the report and then click **Ignore**.</span></span> <span data-ttu-id="a2522-353">**무시** 단추를 클릭하면 강조 표시된 이벤트가 영구적으로 보고서에서 제거되며 허가받은 전역 관리자만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2522-353">The **Ignore** button will permanently remove the highlighted event from the report and can only be used by licensed global admins.</span></span>

## <a name="automatic-email-notifications"></a><span data-ttu-id="a2522-354">자동 전자 메일 알림</span><span class="sxs-lookup"><span data-stu-id="a2522-354">Automatic email notifications</span></span>
<span data-ttu-id="a2522-355">Azure AD의 보고 알림에 대한 자세한 내용은 [Azure Active Directory Reporting 알림](active-directory-reporting-notifications.md)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="a2522-355">For more information about Azure AD's reporting notifications, check out [Azure Active Directory Reporting Notifications](active-directory-reporting-notifications.md).</span></span>

## <a name="whats-next"></a><span data-ttu-id="a2522-356">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a2522-356">What's next</span></span>
* [<span data-ttu-id="a2522-357">Azure Active Directory Premium 시작</span><span class="sxs-lookup"><span data-stu-id="a2522-357">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="a2522-358">로그인 및 액세스 패널 페이지에 회사 브랜딩 추가하기</span><span class="sxs-lookup"><span data-stu-id="a2522-358">Add company branding to your Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

