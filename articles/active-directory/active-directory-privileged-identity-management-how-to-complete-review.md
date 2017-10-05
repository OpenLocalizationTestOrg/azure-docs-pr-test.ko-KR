---
title: "액세스 검토를 완료하는 방법 | Microsoft Docs"
description: "Azure AD Privileged Identity Management에서 액세스 검토를 시작한 후, 그것을 완료하고 결과를 보는 방법을 알아봅니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: ca2a1c7c287e4cf6b1b50cfb0068861b6f525596
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-complete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="d532a-103">Azure AD Privileged Identity Management의 액세스 검토를 완료하는 방법</span><span class="sxs-lookup"><span data-stu-id="d532a-103">How to complete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="d532a-104">[보안 검토가 시작](active-directory-privileged-identity-management-how-to-start-security-review.md)된 후에 권한 있는 역할 관리자가 권한이 있는 액세스를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="d532a-105">Azure AD PIM(Privileged Identity Management)이 사용자에게 해당 액세스를 검토하도록 요청하는 메일을 자동으로 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users to review their access.</span></span> <span data-ttu-id="d532a-106">사용자가 메일을 받지 못한 경우 [보안 검토를 수행하는 방법](active-directory-privileged-identity-management-how-to-perform-security-review.md)의 지침을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-106">If a user did not get an email, you can send them the instructions in [how to perform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="d532a-107">보안 검토 기간이 끝나거나 모든 사용자가 자체 검토를 완료하면 이 문서의 단계에 따라 검토를 관리하고 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-107">After the security review period is over, or all the users have finished their self-review, follow the steps in this article to manage the review and see the results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="d532a-108">보안 검토 관리</span><span class="sxs-lookup"><span data-stu-id="d532a-108">Manage security reviews</span></span>
1. <span data-ttu-id="d532a-109">[Azure 포털](https://portal.azure.com/) 로 이동하고 대시보드에서 **Azure AD Privileged Identity Management** 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-109">Go to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="d532a-110">대시보드의 **액세스 검토** 섹션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-110">Select the **Access reviews** section of the dashboard.</span></span>
3. <span data-ttu-id="d532a-111">관리하려는 액세스 검토를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-111">Select the access review that you want to manage.</span></span>

<span data-ttu-id="d532a-112">액세스 검토의 세부 정보 블레이드에는 검토를 관리하는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-112">On the access review's detail blade there are a number options for managing that review.</span></span>

![PIM 액세스 검토 단추-스크린 샷][1]

### <a name="remind"></a><span data-ttu-id="d532a-114">알림</span><span class="sxs-lookup"><span data-stu-id="d532a-114">Remind</span></span>
<span data-ttu-id="d532a-115">액세스 검토가 설정되어 사용자가 자체적으로 검토하는 경우 **알림** 단추가 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-115">If an access review is set up so that the users review themselves, the **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="d532a-116">중지</span><span class="sxs-lookup"><span data-stu-id="d532a-116">Stop</span></span>
<span data-ttu-id="d532a-117">모든 액세스 검토는 종료 날짜가 있지만, **중지** 단추를 사용하여 일찍 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-117">All access reviews have an end date, but you can use the **Stop** button to finish it early.</span></span> <span data-ttu-id="d532a-118">만일 이 때까지 검토하지 않은 사용자가 있다면, 검토를 중지한 후에는 그들을 검토할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-118">If any users haven't been reviewed by this time, they won't be able to after you stop the review.</span></span> <span data-ttu-id="d532a-119">검토를 중단한 후에는 다시 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="d532a-120">적용</span><span class="sxs-lookup"><span data-stu-id="d532a-120">Apply</span></span>
<span data-ttu-id="d532a-121">종료 날짜가 되었거나 수동으로 중지하여 액세스 검토가 완료되면, **적용** 단추가 검토 결과를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-121">After an access review is completed, either because you reached the end date or stopped it manually, the **Apply** button implements the outcome of the review.</span></span> <span data-ttu-id="d532a-122">사용자의 액세스가 검토 중에 거부되었다면, 이는 그들의 역할 할당을 제거할 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-122">If a user's access was denied in the review, this is the step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="d532a-123">내보내기</span><span class="sxs-lookup"><span data-stu-id="d532a-123">Export</span></span>
<span data-ttu-id="d532a-124">보안 검토 결과를 수동으로 적용하려는 경우 검토를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-124">If you want to apply the results of the security review manually, you can export the review.</span></span> <span data-ttu-id="d532a-125">**내보내기** 단추는 CSV 파일 다운로드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-125">The **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="d532a-126">Excel 또는 CSV 파일을 여는 다른 프로그램에서 결과를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-126">You can manage the results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="d532a-127">삭제</span><span class="sxs-lookup"><span data-stu-id="d532a-127">Delete</span></span>
<span data-ttu-id="d532a-128">더 이상 검토가 필요 없는 경우 검토를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-128">If you are not interested in the review any further, delete it.</span></span> <span data-ttu-id="d532a-129">**삭제** 단추는 PIM 응용 프로그램에서 검토를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-129">The **Delete** button removes the review from the PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d532a-130">삭제가 일어나기 전에 경고가 표시되지 않으므로 삭제를 원하는 검토인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d532a-130">You will not get a warning before deletion occurs, so be sure that you want to delete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d532a-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d532a-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
