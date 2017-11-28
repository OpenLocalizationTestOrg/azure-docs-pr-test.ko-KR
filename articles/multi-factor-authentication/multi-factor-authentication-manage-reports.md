---
title: "Azure MFA에 대 한 aaaAccess 및 사용 보고서 | Microsoft Docs"
description: "Toouse Azure Multi-factor Authentication 기능-보고서 hello 하는 방법을 설명 합니다."
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
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="a37f1-103">Azure Multi-Factor Authentication에서 보고서</span><span class="sxs-lookup"><span data-stu-id="a37f1-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="a37f1-104">Azure Multi-Factor Authentication은 사용자 및 사용자의 조직에서 사용할 수 있는 다양한 보고서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="a37f1-105">이러한 보고서는 hello Multi-factor Authentication 관리 포털을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-105">These reports can be accessed through hello Multi-Factor Authentication Management Portal.</span></span> <span data-ttu-id="a37f1-106">hello 다음은 hello 사용할 수 있는 보고서의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-106">hello following is a list of hello available reports:</span></span>

| <span data-ttu-id="a37f1-107">보고서</span><span class="sxs-lookup"><span data-stu-id="a37f1-107">Report</span></span> | <span data-ttu-id="a37f1-108">설명</span><span class="sxs-lookup"><span data-stu-id="a37f1-108">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a37f1-109">사용</span><span class="sxs-lookup"><span data-stu-id="a37f1-109">Usage</span></span> |<span data-ttu-id="a37f1-110">hello 사용의 전반적인 사용량, 사용자 요약 및 사용자 세부 정보 표시 정보를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-110">hello usage reports display information on overall usage, user summary, and user details.</span></span> |
| <span data-ttu-id="a37f1-111">서버 상태</span><span class="sxs-lookup"><span data-stu-id="a37f1-111">Server Status</span></span> |<span data-ttu-id="a37f1-112">이 보고서는 사용자 계정과 연결 된 Multi-factor Authentication 서버 hello 상태를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-112">This report displays hello status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="a37f1-113">차단된 사용자 기록</span><span class="sxs-lookup"><span data-stu-id="a37f1-113">Blocked User History</span></span> |<span data-ttu-id="a37f1-114">이러한 보고서의 요청 tooblock hello 기록 표시 또는 사용자를 차단 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-114">These reports show hello history of requests tooblock or unblock users.</span></span> |
| <span data-ttu-id="a37f1-115">무시된 사용자 기록</span><span class="sxs-lookup"><span data-stu-id="a37f1-115">Bypassed User History</span></span> |<span data-ttu-id="a37f1-116">사용자의 전화 번호에 대 한 요청 toobypass Multi-factor Authentication의 hello 기록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-116">Shows hello history of requests toobypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="a37f1-117">사기 행위 경고</span><span class="sxs-lookup"><span data-stu-id="a37f1-117">Fraud Alert</span></span> |<span data-ttu-id="a37f1-118">지정한 hello 날짜 범위 동안 제출 된 사기 행위 경고 기록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-118">Shows a history of fraud alerts submitted during hello date range you specified.</span></span> |
| <span data-ttu-id="a37f1-119">Queued</span><span class="sxs-lookup"><span data-stu-id="a37f1-119">Queued</span></span> |<span data-ttu-id="a37f1-120">처리 및 해당 상태에 대해 대기 중인 보고서가 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-120">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="a37f1-121">Hello 보고서 완료 되 면 링크 toodownload 또는 보기 hello 보고서가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-121">A link toodownload or view hello report is provided when hello report is complete.</span></span> |

## <a name="view-reports"></a><span data-ttu-id="a37f1-122">보고서 보기</span><span class="sxs-lookup"><span data-stu-id="a37f1-122">View reports</span></span>
1. <span data-ttu-id="a37f1-123">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-123">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="a37f1-124">Hello 왼쪽에서 Active Directory를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-124">On hello left, select Active Directory.</span></span>
3. <span data-ttu-id="a37f1-125">인증 공급자를 사용하는지 여부에 따라 이 두 옵션 중 하나를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-125">Follow one of these two options, depending on whether you use Auth Providers:</span></span>
   * <span data-ttu-id="a37f1-126">**옵션 1**: hello Multi-factor Auth 공급자 탭을 클릭 합니다. MFA 공급자를 선택 하 고 hello 클릭 **관리** hello 아래쪽 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-126">**Option 1**: Click hello Multi-Factor Auth Providers tab. Select your MFA provider and click hello **Manage** button at hello bottom.</span></span>
   * <span data-ttu-id="a37f1-127">**옵션 2**: 디렉터리 및 이동 toohello 선택 **구성** 탭 합니다. Hello multi-factor authentication 섹션에서 선택 **서비스 설정 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-127">**Option 2**: Select your directory and go toohello **Configure** tab. Under hello multi-factor authentication section, select **Manage service settings**.</span></span> <span data-ttu-id="a37f1-128">Hello MFA 서비스 설정 페이지의 맨 아래 hello에 hello Go toohello 위의 포털 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-128">At hello bottom of hello MFA Service Settings page, click hello Go toohello portal link.</span></span>
4. <span data-ttu-id="a37f1-129">Azure Multi-factor Authentication 관리 포털 hello hello에서 원하는 보고서 hello 유형을 선택 **보고서를 볼** hello 왼쪽 탐색의에서 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="a37f1-129">In hello Azure Multi-Factor Authentication Management Portal, select hello type of report you want from hello **View a Report** section in hello left navigation.</span></span>

<span data-ttu-id="a37f1-130"><center>![클라우드](./media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="a37f1-130"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="a37f1-131">**추가 리소스**</span><span class="sxs-lookup"><span data-stu-id="a37f1-131">**Additional Resources**</span></span>

* [<span data-ttu-id="a37f1-132">사용자</span><span class="sxs-lookup"><span data-stu-id="a37f1-132">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="a37f1-133">MSDN에서 Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="a37f1-133">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)
