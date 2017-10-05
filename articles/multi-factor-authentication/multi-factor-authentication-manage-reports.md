---
title: "Azure MFA에 대한 액세스 및 사용 보고서 | Microsoft Docs"
description: "Azure Multi-Factor Authentication 기능 - 보고서를 사용하는 방법을 설명합니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: f76e726c6a67de4b0472c0e97f9e72c31c14c4f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="0d4ae-103">Azure Multi-Factor Authentication에서 보고서</span><span class="sxs-lookup"><span data-stu-id="0d4ae-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="0d4ae-104">Azure Multi-Factor Authentication은 사용자 및 사용자의 조직에서 사용할 수 있는 다양한 보고서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="0d4ae-105">이러한 보고서는 Multi-Factor Authentication 관리 포털을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-105">These reports can be accessed through the Multi-Factor Authentication Management Portal.</span></span> <span data-ttu-id="0d4ae-106">다음은 사용 가능한 보고서의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-106">The following is a list of the available reports:</span></span>

| <span data-ttu-id="0d4ae-107">보고서</span><span class="sxs-lookup"><span data-stu-id="0d4ae-107">Report</span></span> | <span data-ttu-id="0d4ae-108">설명</span><span class="sxs-lookup"><span data-stu-id="0d4ae-108">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0d4ae-109">사용 현황</span><span class="sxs-lookup"><span data-stu-id="0d4ae-109">Usage</span></span> |<span data-ttu-id="0d4ae-110">사용 현황 보고서는 전반적인 사용 현황, 사용자 요약 및 사용자 세부 내용에 대한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-110">The usage reports display information on overall usage, user summary, and user details.</span></span> |
| <span data-ttu-id="0d4ae-111">서버 상태</span><span class="sxs-lookup"><span data-stu-id="0d4ae-111">Server Status</span></span> |<span data-ttu-id="0d4ae-112">이 보고서는 계정에 연결된 Multi-Factor Authentication 서버의 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-112">This report displays the status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="0d4ae-113">차단된 사용자 기록</span><span class="sxs-lookup"><span data-stu-id="0d4ae-113">Blocked User History</span></span> |<span data-ttu-id="0d4ae-114">이러한 보고서는 사용자 차단 또는 차단 해제 요청 기록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-114">These reports show the history of requests to block or unblock users.</span></span> |
| <span data-ttu-id="0d4ae-115">무시된 사용자 기록</span><span class="sxs-lookup"><span data-stu-id="0d4ae-115">Bypassed User History</span></span> |<span data-ttu-id="0d4ae-116">사용자의 전화번호에 대한 Multi-Factor Authentication 무시 요청 기록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-116">Shows the history of requests to bypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="0d4ae-117">사기 행위 경고</span><span class="sxs-lookup"><span data-stu-id="0d4ae-117">Fraud Alert</span></span> |<span data-ttu-id="0d4ae-118">지정한 날짜 범위 동안 제출된 사기 행위 경고 기록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-118">Shows a history of fraud alerts submitted during the date range you specified.</span></span> |
| <span data-ttu-id="0d4ae-119">Queued</span><span class="sxs-lookup"><span data-stu-id="0d4ae-119">Queued</span></span> |<span data-ttu-id="0d4ae-120">처리 및 해당 상태에 대해 대기 중인 보고서가 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-120">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="0d4ae-121">보고서가 완료되면 보고서를 다운로드하거나 볼 링크가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-121">A link to download or view the report is provided when the report is complete.</span></span> |

## <a name="view-reports"></a><span data-ttu-id="0d4ae-122">보고서 보기</span><span class="sxs-lookup"><span data-stu-id="0d4ae-122">View reports</span></span>
1. <span data-ttu-id="0d4ae-123">[Azure 클래식 포털](https://manage.windowsazure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-123">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="0d4ae-124">왼쪽에서 Active Directory를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-124">On the left, select Active Directory.</span></span>
3. <span data-ttu-id="0d4ae-125">인증 공급자를 사용하는지 여부에 따라 이 두 옵션 중 하나를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-125">Follow one of these two options, depending on whether you use Auth Providers:</span></span>
   * <span data-ttu-id="0d4ae-126">**옵션 1**: 다단계 인증 공급자 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-126">**Option 1**: Click the Multi-Factor Auth Providers tab.</span></span> <span data-ttu-id="0d4ae-127">MFA 공급자를 선택하고 맨 아래에 있는 **관리** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-127">Select your MFA provider and click the **Manage** button at the bottom.</span></span>
   * <span data-ttu-id="0d4ae-128">**옵션 2**: 디렉터리를 선택하고 **구성** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-128">**Option 2**: Select your directory and go to the **Configure** tab.</span></span> <span data-ttu-id="0d4ae-129">Multi-Factor Authentication 섹션에서 **서비스 설정 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-129">Under the multi-factor authentication section, select **Manage service settings**.</span></span> <span data-ttu-id="0d4ae-130">MFA 서비스 설정 페이지의 맨 아래에서 포털로 이동 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-130">At the bottom of the MFA Service Settings page, click the Go to the portal link.</span></span>
4. <span data-ttu-id="0d4ae-131">Azure Multi-Factor Authentication 관리 포털의 왼쪽 탐색에 있는 **보고서 보기** 섹션에서 보고서의 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0d4ae-131">In the Azure Multi-Factor Authentication Management Portal, select the type of report you want from the **View a Report** section in the left navigation.</span></span>

<span data-ttu-id="0d4ae-132"><center>![클라우드](./media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="0d4ae-132"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="0d4ae-133">**추가 리소스**</span><span class="sxs-lookup"><span data-stu-id="0d4ae-133">**Additional Resources**</span></span>

* [<span data-ttu-id="0d4ae-134">사용자</span><span class="sxs-lookup"><span data-stu-id="0d4ae-134">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="0d4ae-135">MSDN에서 Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="0d4ae-135">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)
