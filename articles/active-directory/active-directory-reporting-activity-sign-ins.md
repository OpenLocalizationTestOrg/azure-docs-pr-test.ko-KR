---
title: "Azure Active Directory 포털의 로그인 작업 보고서 | Microsoft Docs"
description: "Azure Active Directory 포털의 로그인 작업 보고서 소개"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: b9e61950654ba427b09dd608d354589a0804aaa5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-activity-reports-in-the-azure-active-directory-portal"></a><span data-ttu-id="eb760-103">Azure Active Directory 포털의 로그인 작업 보고서</span><span class="sxs-lookup"><span data-stu-id="eb760-103">Sign-in activity reports in the Azure Active Directory portal</span></span>

<span data-ttu-id="eb760-104">[Azure Portal](https://portal.azure.com)에서 Azure Active Directory(Azure AD) 보고를 통해 사용자 환경의 작동 방법을 결정하는 데 필요한 모든 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-104">With Azure Active Directory (Azure AD) reporting in the [Azure portal](https://portal.azure.com), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="eb760-105">Azure Active Directory의 보고 아키텍처는 다음 구성 요소로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-105">The reporting architecture in Azure Active Directory consists of the following components:</span></span>

- <span data-ttu-id="eb760-106">**활동**</span><span class="sxs-lookup"><span data-stu-id="eb760-106">**Activity**</span></span> 
    - <span data-ttu-id="eb760-107">**로그인 활동** – 관리되는 응용 프로그램 및 사용자 로그인 활동의 사용량에 대한 정보</span><span class="sxs-lookup"><span data-stu-id="eb760-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="eb760-108">**감사 로그** - 사용자 및 그룹 관리, 관리되는 응용 프로그램 및 디렉터리 활동에 대한 시스템 작업 정보</span><span class="sxs-lookup"><span data-stu-id="eb760-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="eb760-109">**보안**</span><span class="sxs-lookup"><span data-stu-id="eb760-109">**Security**</span></span> 
    - <span data-ttu-id="eb760-110">**위험한 로그인** - 위험한 로그인은 사용자 계정의 정당한 소유자가 아닌 사용자에 의해 수행된 로그인 시도에 대한 지표입니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="eb760-111">자세한 내용은 위험한 로그인을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb760-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="eb760-112">**위험 플래그가 지정된 사용자** - 위험한 사용자는 손상되었을 수 있는 사용자 계정에 대한 표시기입니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="eb760-113">자세한 내용은 위험 플래그가 지정된 사용자를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb760-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="eb760-114">이 항목에서는 로그인 활동에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-114">This topic gives you an overview of the sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="eb760-115">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="eb760-115">Pre-requisite</span></span>

### <a name="who-can-access-the-data"></a><span data-ttu-id="eb760-116">데이터에 액세스할 수 있는 사용자는 누구인가요?</span><span class="sxs-lookup"><span data-stu-id="eb760-116">Who can access the data?</span></span>
* <span data-ttu-id="eb760-117">보안 관리 또는 보안 판독기 역할의 사용자</span><span class="sxs-lookup"><span data-stu-id="eb760-117">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="eb760-118">전역 관리자</span><span class="sxs-lookup"><span data-stu-id="eb760-118">Global Admins</span></span>
* <span data-ttu-id="eb760-119">모든 사용자(비관리자)가 자신의 로그인에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-to-access-sign-in-activity"></a><span data-ttu-id="eb760-120">로그인 작업에 액세스하는 데 필요한 Azure AD 라이선스는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="eb760-120">What Azure AD license do you need to access sign-in activity?</span></span>
* <span data-ttu-id="eb760-121">모든 로그인 활동 보고서를 보려면 테넌트에 이와 관련된 Azure AD Premium 라이선스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-121">Your tenant must have an Azure AD Premium license associated with it to see the all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="eb760-122">로그인 활동</span><span class="sxs-lookup"><span data-stu-id="eb760-122">Signs-in activities</span></span>

<span data-ttu-id="eb760-123">보고서에서 사용자 로그인에 의해 제공되는 정보를 사용하여 다음과 같은 질문에 대한 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-123">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

* <span data-ttu-id="eb760-124">사용자의 로그인 패턴이란?</span><span class="sxs-lookup"><span data-stu-id="eb760-124">What is the sign-in pattern of a user?</span></span>
* <span data-ttu-id="eb760-125">한 주 동안 얼마나 많은 사용자가 로그인했나요?</span><span class="sxs-lookup"><span data-stu-id="eb760-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="eb760-126">이러한 로그인의 상태란?</span><span class="sxs-lookup"><span data-stu-id="eb760-126">What’s the status of these sign-ins?</span></span>

<span data-ttu-id="eb760-127">모든 로그인 작업 데이터의 첫 번째 진입점은 **Azure Active**의 [작업] 섹션에 있는 **로그인**입니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-127">Your first entry point to all sign-in activities data is **Sign-ins** in the Activity section of **Azure Active**.</span></span>


<span data-ttu-id="eb760-128">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/61.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="eb760-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="eb760-129">감사 로그에는 다음 항목을 보여 주는 기본 목록 보기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="eb760-130">관련된 사용자</span><span class="sxs-lookup"><span data-stu-id="eb760-130">the related user</span></span>
- <span data-ttu-id="eb760-131">사용자에 로그인한 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="eb760-131">the application the user has signed-in to</span></span>
- <span data-ttu-id="eb760-132">로그인 상태</span><span class="sxs-lookup"><span data-stu-id="eb760-132">the sign-in status</span></span>
- <span data-ttu-id="eb760-133">로그인 시간</span><span class="sxs-lookup"><span data-stu-id="eb760-133">the sign-in time</span></span>

<span data-ttu-id="eb760-134">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/41.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="eb760-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="eb760-135">도구 모음에서 **열**을 클릭하여 목록 보기를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-135">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="eb760-136">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/19.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="eb760-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="eb760-137">그러면 추가 필드를 표시하거나 이미 표시된 필드를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-137">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="eb760-138">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/42.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="eb760-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="eb760-139">목록 보기에서 항목을 클릭하면 사용할 수 있는 세부 정보를 모두 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-139">By clicking an item in the list view, you get all available details about it.</span></span>

<span data-ttu-id="eb760-140">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/43.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="eb760-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="eb760-141">로그인 활동 필터링</span><span class="sxs-lookup"><span data-stu-id="eb760-141">Filtering sign-in activities</span></span>

<span data-ttu-id="eb760-142">보고된 데이터를 자신에게 적합한 수준으로 좁히려면 다음 필드를 사용하여 로그인 데이터를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-142">To narrow down the reported data to a level that works for you, you can filter the sign-ins data using the following fields:</span></span>

- <span data-ttu-id="eb760-143">시간 간격</span><span class="sxs-lookup"><span data-stu-id="eb760-143">Time interval</span></span>
- <span data-ttu-id="eb760-144">사용자</span><span class="sxs-lookup"><span data-stu-id="eb760-144">User</span></span>
- <span data-ttu-id="eb760-145">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="eb760-145">Application</span></span>
- <span data-ttu-id="eb760-146">클라이언트</span><span class="sxs-lookup"><span data-stu-id="eb760-146">Client</span></span>
- <span data-ttu-id="eb760-147">로그인 상태</span><span class="sxs-lookup"><span data-stu-id="eb760-147">Sign-in status</span></span>

<span data-ttu-id="eb760-148">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/44.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="eb760-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="eb760-149">**시간 간격** 필터를 사용하면 반환된 데이터의 시간 범위를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-149">The **time interval** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="eb760-150">가능한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-150">Possible values are:</span></span>

- <span data-ttu-id="eb760-151">1개월</span><span class="sxs-lookup"><span data-stu-id="eb760-151">1 month</span></span>
- <span data-ttu-id="eb760-152">7 일</span><span class="sxs-lookup"><span data-stu-id="eb760-152">7 days</span></span>
- <span data-ttu-id="eb760-153">24시간</span><span class="sxs-lookup"><span data-stu-id="eb760-153">24 hours</span></span>
- <span data-ttu-id="eb760-154">사용자 지정</span><span class="sxs-lookup"><span data-stu-id="eb760-154">Custom</span></span>

<span data-ttu-id="eb760-155">사용자 지정 시간 범위를 선택하면 시작 시간과 종료 시간을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="eb760-156">**사용자** 필터를 사용하면 관심 있는 사용자의 이름이나 UPN(사용자 계정 이름)을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-156">The **user** filter enables you to specify the name or the user principal name (UPN) of the user you care about.</span></span>

<span data-ttu-id="eb760-157">**응용 프로그램** 필터를 사용하면 관심 있는 응용 프로그램의 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-157">The **application** filter enables you to specify the name of the application you care about.</span></span>

<span data-ttu-id="eb760-158">**클라이언트** 필터를 사용하면 관심 있는 장치에 대한 정보를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-158">The **client** filter enables you to specify information about the device you care about.</span></span>

<span data-ttu-id="eb760-159">**로그인 상태** 필터를 사용하면 다음 필터 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-159">The **sign-in status** filter enables you to select one of the following filter:</span></span>

- <span data-ttu-id="eb760-160">모두</span><span class="sxs-lookup"><span data-stu-id="eb760-160">All</span></span>
- <span data-ttu-id="eb760-161">성공</span><span class="sxs-lookup"><span data-stu-id="eb760-161">Success</span></span>
- <span data-ttu-id="eb760-162">실패</span><span class="sxs-lookup"><span data-stu-id="eb760-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="eb760-163">로그인 활동 바로 가기</span><span class="sxs-lookup"><span data-stu-id="eb760-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="eb760-164">Azure Active Directory 외에도 Azure Portal에서는 로그인 활동 데이터에 대한 다음 두 개의 추가 진입점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-164">In addition to Azure Active Directory, the Azure portal provides you with two additional entry points to sign-in activities data:</span></span>

- <span data-ttu-id="eb760-165">개요</span><span class="sxs-lookup"><span data-stu-id="eb760-165">Users and groups</span></span>
- <span data-ttu-id="eb760-166">Enterprise 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="eb760-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="eb760-167">사용자 및 그룹 로그인 활동</span><span class="sxs-lookup"><span data-stu-id="eb760-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="eb760-168">보고서에서 사용자 로그인에 의해 제공되는 정보를 사용하여 다음과 같은 질문에 대한 대답을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-168">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

- <span data-ttu-id="eb760-169">사용자의 로그인 패턴이란?</span><span class="sxs-lookup"><span data-stu-id="eb760-169">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="eb760-170">한 주 동안 얼마나 많은 사용자가 로그인했나요?</span><span class="sxs-lookup"><span data-stu-id="eb760-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="eb760-171">이러한 로그인의 상태란?</span><span class="sxs-lookup"><span data-stu-id="eb760-171">What’s the status of these sign-ins?</span></span>



<span data-ttu-id="eb760-172">이 데이터에 대한 진입점은 **사용자 및 그룹**의 **개요** 섹션에서 사용자 로그인 그래프입니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-172">Your entry point to this data is the user sign-in graph in the **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="eb760-173">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/45.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="eb760-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="eb760-174">사용자 로그인 그래프에서는 지정된 기간 내에 모든 사용자에 대한 로그인의 주간 집계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-174">The user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="eb760-175">시간에 대한 기본값은 30일입니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-175">The default for the time period is 30 days.</span></span>

<span data-ttu-id="eb760-176">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/46.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="eb760-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="eb760-177">로그인 그래프에서 한 날짜를 클릭하면 해당 날짜의 로그인 활동에 대한 자세한 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-177">When you click on a day in the sign-in graph, you get a detailed list of the sign-in activities for this day.</span></span>

<span data-ttu-id="eb760-178">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/41.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="eb760-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="eb760-179">로그인 활동 목록에서 각 행은 다음과 같이 선택된 로그인에 대한 자세한 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-179">Each row in the sign-in activities list gives you the detailed information about the selected sign-in such as:</span></span>

* <span data-ttu-id="eb760-180">누가 로그인했나요?</span><span class="sxs-lookup"><span data-stu-id="eb760-180">Who has signed in?</span></span>
* <span data-ttu-id="eb760-181">관련된 UPN는 무엇이었나요?</span><span class="sxs-lookup"><span data-stu-id="eb760-181">What was the related UPN?</span></span>
* <span data-ttu-id="eb760-182">어떤 응용 프로그램이 로그인할 대상이었나요?</span><span class="sxs-lookup"><span data-stu-id="eb760-182">What application was the target of the sign-in?</span></span>
* <span data-ttu-id="eb760-183">로그인의 IP 주소는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="eb760-183">What is the IP address of the sign-in?</span></span>
* <span data-ttu-id="eb760-184">로그인의 상태는 어떠했나요?</span><span class="sxs-lookup"><span data-stu-id="eb760-184">What was the status of the sign-in?</span></span>

<span data-ttu-id="eb760-185">**로그인** 옵션은 모든 사용자의 로그인에 대한 전체 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-185">The **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="eb760-186">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/51.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="eb760-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="eb760-187">관리되는 응용 프로그램의 사용량</span><span class="sxs-lookup"><span data-stu-id="eb760-187">Usage of managed applications</span></span>

<span data-ttu-id="eb760-188">로그인 데이터의 응용 프로그램 중심 보기를 사용하여 다음과 같은 질문에 대답할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="eb760-189">누가 내 응용 프로그램을 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="eb760-189">Who is using my applications?</span></span>
* <span data-ttu-id="eb760-190">조직에서 상위 3개의 응용 프로그램은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="eb760-190">What are the top 3 applications in your organization?</span></span>
* <span data-ttu-id="eb760-191">최근에 응용 프로그램을 롤아웃했습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-191">I have recently rolled out an application.</span></span> <span data-ttu-id="eb760-192">어떻게 작동하고 있나요?</span><span class="sxs-lookup"><span data-stu-id="eb760-192">How is it doing?</span></span>

<span data-ttu-id="eb760-193">이 데이터에 대한 진입점은 **엔터프라이즈 응용 프로그램**의 **개요** 섹션에 있는 지난 30일 간의 보고서에서 조직에 포함된 상위 3개의 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-193">Your entry point to this data is the top 3 applications in your organization within the last 30 days report in the **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="eb760-194">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/64.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="eb760-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="eb760-195">지정된 기간 동안 상위 3가지 응용 프로그램에 대한 로그인의 주간 사용량 그래프 집계입니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-195">The app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="eb760-196">시간에 대한 기본값은 30일입니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-196">The default for the time period is 30 days.</span></span>

<span data-ttu-id="eb760-197">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/47.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="eb760-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="eb760-198">원하면 특정 응용 프로그램에 포커스를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-198">If you want to, you can set the focus on a specific application.</span></span>


<span data-ttu-id="eb760-199">![보고](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="eb760-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="eb760-200">앱 사용량 그래프에서 날짜를 클릭하면 로그인 활동의 자세한 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-200">When you click on a day in the app usage graph, you get a detailed list of the sign-in activities.</span></span>


<span data-ttu-id="eb760-201">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/48.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="eb760-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="eb760-202">**로그인** 옵션을 선택하면 응용 프로그램에 대한 모든 로그인 이벤트의 전체적인 개요를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb760-202">The **Sign-ins** option gives you a complete overview of all sign-in events to your applications.</span></span>

<span data-ttu-id="eb760-203">![로그인 활동](./media/active-directory-reporting-activity-sign-ins/49.png "로그인 활동")</span><span class="sxs-lookup"><span data-stu-id="eb760-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="eb760-204">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb760-204">Next steps</span></span>

<span data-ttu-id="eb760-205">로그인 활동 오류 코드에 대해 자세히 알아보려면 [Azure Active Directory 포털의 로그인 활동 보고서 오류 코드](active-directory-reporting-activity-sign-ins-errors.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb760-205">If you want to know more about sign-in activity error codes, see the [Sign-in activity report error codes in the Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

