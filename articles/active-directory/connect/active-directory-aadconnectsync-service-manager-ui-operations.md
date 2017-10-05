---
title: "Azure AD Connect Synchronization Service Manager 작업 | Microsoft Docs"
description: "Azure AD Connect의 Synchronization Service Manager에 있는 작업 탭을 이해합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1475e4fcd11eb008badba49665f4af6029a1697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="using-the-sync-service-manager-operations-tab"></a><span data-ttu-id="f2003-103">Sync Service Manager 작업 탭 사용</span><span class="sxs-lookup"><span data-stu-id="f2003-103">Using the Sync Service Manager Operations tab</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

<span data-ttu-id="f2003-105">작업 탭에서는 최근 작업의 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-105">The operations tab shows the results from the most recent operations.</span></span> <span data-ttu-id="f2003-106">이 탭은 문제를 이해하고 해결하는 데 핵심적인 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-106">This tab is key to understand and troubleshoot issues.</span></span>

## <a name="understand-the-information-visible-in-the-operations-tab"></a><span data-ttu-id="f2003-107">작업 탭에 표시되는 정보를 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-107">Understand the information visible in the operations tab</span></span>
<span data-ttu-id="f2003-108">위쪽 절반에서 모든 실행이 시간순으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-108">The top half shows all runs in chronological order.</span></span> <span data-ttu-id="f2003-109">기본적으로 작업 로그는 지난 7일에 대한 정보를 유지하지만 이 설정은 [스케줄러](active-directory-aadconnectsync-feature-scheduler.md)에 따라 변동될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-109">By default, the operations log keeps information about the last seven days, but this setting can be changed with the [scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span> <span data-ttu-id="f2003-110">성공 상태를 표시하지 않는 실행을 찾아보려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-110">You want to look for any run that does not show a success status.</span></span> <span data-ttu-id="f2003-111">헤더를 클릭하여 정렬을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-111">You can change the sorting by clicking the headers.</span></span>

<span data-ttu-id="f2003-112">**상태** 열은 가장 중요한 정보이며 실행에 대해 가장 심각한 문제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-112">The **Status** column is the most important information and shows the most severe problem for a run.</span></span> <span data-ttu-id="f2003-113">다음은 조사할 우선 순위에 따른 가장 일반적인 상태에 대한 간단한 요약입니다(여기서 *는 여러 가능한 오류 문자열을 나타냄).</span><span class="sxs-lookup"><span data-stu-id="f2003-113">Here is a quick summary of the most common statuses in order of priority to investigate (where * indicate several possible error strings).</span></span>

| <span data-ttu-id="f2003-114">상태</span><span class="sxs-lookup"><span data-stu-id="f2003-114">Status</span></span> | <span data-ttu-id="f2003-115">주석</span><span class="sxs-lookup"><span data-stu-id="f2003-115">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="f2003-116">stopped-*</span><span class="sxs-lookup"><span data-stu-id="f2003-116">stopped-*</span></span> |<span data-ttu-id="f2003-117">실행을 완료하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-117">The run could not complete.</span></span> <span data-ttu-id="f2003-118">예를 들어 원격 시스템이 다운되어 연결할 수 없는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-118">For example, if the remote system is down and cannot be contacted.</span></span> |
| <span data-ttu-id="f2003-119">stopped-error-limit</span><span class="sxs-lookup"><span data-stu-id="f2003-119">stopped-error-limit</span></span> |<span data-ttu-id="f2003-120">5000개보다 많은 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-120">There are more than 5,000 errors.</span></span> <span data-ttu-id="f2003-121">많은 오류로 인해 실행이 자동으로 중지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-121">The run was automatically stopped due to the large number of errors.</span></span> |
| <span data-ttu-id="f2003-122">completed-\*-errors</span><span class="sxs-lookup"><span data-stu-id="f2003-122">completed-\*-errors</span></span> |<span data-ttu-id="f2003-123">실행이 완료되었지만 조사해야 할 오류가 있습니다(5,000개 미만).</span><span class="sxs-lookup"><span data-stu-id="f2003-123">The run completed, but there are errors (fewer than 5,000) that should be investigated.</span></span> |
| <span data-ttu-id="f2003-124">completed-\*-warnings</span><span class="sxs-lookup"><span data-stu-id="f2003-124">completed-\*-warnings</span></span> |<span data-ttu-id="f2003-125">실행이 완료되었지만 일부 데이터가 예상된 상태가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-125">The run completed, but some data is not in the expected state.</span></span> <span data-ttu-id="f2003-126">오류가 발생하는 경우 이 메시지는 일반적으로 증상일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-126">If you have errors, then this message is usually only a symptom.</span></span> <span data-ttu-id="f2003-127">오류를 해결할 때까지 경고를 조사하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-127">Until you have addressed errors, you should not investigate warnings.</span></span> |
| <span data-ttu-id="f2003-128">성공</span><span class="sxs-lookup"><span data-stu-id="f2003-128">success</span></span> |<span data-ttu-id="f2003-129">문제가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-129">No issues.</span></span> |

<span data-ttu-id="f2003-130">행을 선택하면 해당 실행의 세부 정보가 표시되도록 아래쪽이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-130">When you select a row, the bottom updates to show the details of that run.</span></span> <span data-ttu-id="f2003-131">아래 맨 왼쪽에 **#단계**라는 목록이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-131">To the far left of the bottom, you might have a list saying **Step #**.</span></span> <span data-ttu-id="f2003-132">이 목록은 각 도메인을 단계로 나타내는 포리스트에 여러 도메인이 있는 경우에만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-132">This list only appears if you have multiple domains in your forest where each domain is represented by a step.</span></span> <span data-ttu-id="f2003-133">도메인 이름은 **파티션**머리글 아래에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-133">The domain name can be found under the heading **Partition**.</span></span> <span data-ttu-id="f2003-134">**동기화 통계**아래에서 처리된 변경 내용의 수에 대한 자세한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-134">Under **Synchronization Statistics**, you can find more information about the number of changes that were processed.</span></span> <span data-ttu-id="f2003-135">링크를 클릭하여 변경된 개체의 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-135">You can click the links to get a list of the changed objects.</span></span> <span data-ttu-id="f2003-136">오류가 있는 개체가 있으면 해당 오류는 **동기화 오류**아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-136">If you have objects with errors, those errors show up under **Synchronization Errors**.</span></span>

<span data-ttu-id="f2003-137">자세한 내용은 [동기화되지 않는 개체 문제 해결](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f2003-137">For more information, see [troubleshoot an object that is not synchronizing](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2003-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f2003-138">Next steps</span></span>
<span data-ttu-id="f2003-139">[Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-139">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="f2003-140">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f2003-140">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
