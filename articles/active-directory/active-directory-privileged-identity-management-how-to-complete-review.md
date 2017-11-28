---
title: "aaaHow toocomplete 액세스 검토 | Microsoft Docs"
description: "자세한 내용은 Azure AD Privileged Identity Management에 대 한 액세스 검토를 시작한 후 어떻게 toocomplete 하 고 보기 hello 결과"
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
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="ada04-103">어떻게 toocomplete 액세스에서에서 검토 하 고 Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="ada04-103">How toocomplete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="ada04-104">[보안 검토가 시작](active-directory-privileged-identity-management-how-to-start-security-review.md)된 후에 권한 있는 역할 관리자가 권한이 있는 액세스를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="ada04-105">Azure AD Privileged Identity Management (PIM)에서는 자동으로 액세스 tooreview 사용자에 게 확인 전자 메일을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users tooreview their access.</span></span> <span data-ttu-id="ada04-106">사용자 전자 메일을 받지 못했음을 보낼 수 있습니다 이러한 hello 지침 [어떻게 tooperform 보안 검토](active-directory-privileged-identity-management-how-to-perform-security-review.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-106">If a user did not get an email, you can send them hello instructions in [how tooperform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="ada04-107">Hello 보안 검토 기간이 끝나면 또는 모든 hello 사용자 자신의 셀프 검토를 마친 후에이 문서 toomanage hello 검토의 hello 단계를 수행 하 고 hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-107">After hello security review period is over, or all hello users have finished their self-review, follow hello steps in this article toomanage hello review and see hello results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="ada04-108">보안 검토 관리</span><span class="sxs-lookup"><span data-stu-id="ada04-108">Manage security reviews</span></span>
1. <span data-ttu-id="ada04-109">Toohello 이동 [Azure 포털](https://portal.azure.com/) 및 선택 hello **Azure AD Privileged Identity Management** 동영상이 대시보드에서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-109">Go toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="ada04-110">선택 hello **검토 액세스** hello 대시보드의 섹션.</span><span class="sxs-lookup"><span data-stu-id="ada04-110">Select hello **Access reviews** section of hello dashboard.</span></span>
3. <span data-ttu-id="ada04-111">원하는 toomanage hello 액세스 검토를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-111">Select hello access review that you want toomanage.</span></span>

<span data-ttu-id="ada04-112">Hello 액세스 검토 세부 정보 블레이드에서 해당 검토를 관리 하기 위한 숫자 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-112">On hello access review's detail blade there are a number options for managing that review.</span></span>

![PIM 액세스 검토 단추-스크린 샷][1]

### <a name="remind"></a><span data-ttu-id="ada04-114">알림</span><span class="sxs-lookup"><span data-stu-id="ada04-114">Remind</span></span>
<span data-ttu-id="ada04-115">액세스 검토 hello 사용자 자신을 검토할 수 있도록 설치 되 면 경우 hello **문제점이** 단추 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-115">If an access review is set up so that hello users review themselves, hello **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="ada04-116">중지</span><span class="sxs-lookup"><span data-stu-id="ada04-116">Stop</span></span>
<span data-ttu-id="ada04-117">모든 액세스 검토는 종료 날짜를 갖지만 hello를 사용할 수 있습니다 **중지** 단추 toofinish 일찍 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-117">All access reviews have an end date, but you can use hello **Stop** button toofinish it early.</span></span> <span data-ttu-id="ada04-118">모든 사용자가이 시간까지 검토 된 하지 않은 경우 그렇지 않은 것 수 tooafter hello 검토를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-118">If any users haven't been reviewed by this time, they won't be able tooafter you stop hello review.</span></span> <span data-ttu-id="ada04-119">검토를 중단한 후에는 다시 시작할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="ada04-120">적용</span><span class="sxs-lookup"><span data-stu-id="ada04-120">Apply</span></span>
<span data-ttu-id="ada04-121">액세스 검토 완료 되 면 하나 hello 종료 날짜에 도달 하거나 수동으로 중지 hello **적용** 단추 hello 검토의 hello 결과 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-121">After an access review is completed, either because you reached hello end date or stopped it manually, hello **Apply** button implements hello outcome of hello review.</span></span> <span data-ttu-id="ada04-122">검토 회의 hello 사용자의 액세스가 거부 되었습니다,이 역할 할당을 제거 하는 hello 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-122">If a user's access was denied in hello review, this is hello step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="ada04-123">내보내기</span><span class="sxs-lookup"><span data-stu-id="ada04-123">Export</span></span>
<span data-ttu-id="ada04-124">수동으로 hello 보안 검토의 tooapply hello 결과 찾으려는 경우 hello 검토를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-124">If you want tooapply hello results of hello security review manually, you can export hello review.</span></span> <span data-ttu-id="ada04-125">hello **내보내기** 단추 CSV 파일을 다운로드 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-125">hello **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="ada04-126">Hello 결과를 Excel 또는 CSV 파일을 여는 다른 프로그램을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-126">You can manage hello results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="ada04-127">삭제</span><span class="sxs-lookup"><span data-stu-id="ada04-127">Delete</span></span>
<span data-ttu-id="ada04-128">Hello에 관심이 없는 모든 추가로 검토, 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-128">If you are not interested in hello review any further, delete it.</span></span> <span data-ttu-id="ada04-129">hello **삭제** 단추 hello PIM 응용 프로그램에서에서 hello 검토를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-129">hello **Delete** button removes hello review from hello PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ada04-130">하지 삭제 발생 하기 전에 경고가 발생 되 면 검토 toodelete 되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ada04-130">You will not get a warning before deletion occurs, so be sure that you want toodelete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ada04-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ada04-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
