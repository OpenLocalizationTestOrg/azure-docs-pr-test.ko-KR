---
title: "Azure AD Connect Synchronization Service Manager 작업 | Microsoft Docs"
description: "Azure AD Connect에 대 한 hello 동기화 서비스 관리자의에서 작업 탭 hello를 이해 합니다."
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
ms.openlocfilehash: decbc53613d456a71cd116c40c5e1fd761efd4af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-sync-service-manager-operations-tab"></a><span data-ttu-id="f1456-103">Hello 동기화 서비스 관리자가 작업 탭을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f1456-103">Using hello Sync Service Manager Operations tab</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

<span data-ttu-id="f1456-105">작업 탭 hello hello 가장 최근 작업에서 hello 결과 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-105">hello operations tab shows hello results from hello most recent operations.</span></span> <span data-ttu-id="f1456-106">이 탭은 키 toounderstand 며 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-106">This tab is key toounderstand and troubleshoot issues.</span></span>

## <a name="understand-hello-information-visible-in-hello-operations-tab"></a><span data-ttu-id="f1456-107">Hello 작업 탭에 표시 하는 hello 정보 이해</span><span class="sxs-lookup"><span data-stu-id="f1456-107">Understand hello information visible in hello operations tab</span></span>
<span data-ttu-id="f1456-108">hello 위쪽 절반 시간 순서에 따라 모든 실행을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-108">hello top half shows all runs in chronological order.</span></span> <span data-ttu-id="f1456-109">기본적으로 hello 작업 로그 정보를 유지 관리 hello에 대 한 지난 7 일 하지만 hello로이 설정을 변경할 수 있습니다 [스케줄러](active-directory-aadconnectsync-feature-scheduler.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-109">By default, hello operations log keeps information about hello last seven days, but this setting can be changed with hello [scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span> <span data-ttu-id="f1456-110">성공 상태를 표시 하지 않는 모든 실행에 대 한 toolook을 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-110">You want toolook for any run that does not show a success status.</span></span> <span data-ttu-id="f1456-111">Hello hello 머리글을 클릭 하 여 정렬을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-111">You can change hello sorting by clicking hello headers.</span></span>

<span data-ttu-id="f1456-112">hello **상태** 열이 hello 가장 중요 한 정보 및 실행에 대해 가장 심각한 문제를 hello 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-112">hello **Status** column is hello most important information and shows hello most severe problem for a run.</span></span> <span data-ttu-id="f1456-113">간단히 요약 한 hello 가장 일반적인 상태 tooinvestigate 우선 순위 순서 대로 다음과 같습니다 (여기서 * 나타내는 여러 가지 가능한 오류 문자열)입니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-113">Here is a quick summary of hello most common statuses in order of priority tooinvestigate (where * indicate several possible error strings).</span></span>

| <span data-ttu-id="f1456-114">가동 상태</span><span class="sxs-lookup"><span data-stu-id="f1456-114">Status</span></span> | <span data-ttu-id="f1456-115">주석</span><span class="sxs-lookup"><span data-stu-id="f1456-115">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="f1456-116">stopped-*</span><span class="sxs-lookup"><span data-stu-id="f1456-116">stopped-*</span></span> |<span data-ttu-id="f1456-117">hello 실행을 완료할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-117">hello run could not complete.</span></span> <span data-ttu-id="f1456-118">예를 들어 경우 hello 원격 시스템 다운 되어에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-118">For example, if hello remote system is down and cannot be contacted.</span></span> |
| <span data-ttu-id="f1456-119">stopped-error-limit</span><span class="sxs-lookup"><span data-stu-id="f1456-119">stopped-error-limit</span></span> |<span data-ttu-id="f1456-120">5000개보다 많은 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-120">There are more than 5,000 errors.</span></span> <span data-ttu-id="f1456-121">실행 하는 hello toohello 오류가 많이 인해 자동으로 중지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-121">hello run was automatically stopped due toohello large number of errors.</span></span> |
| <span data-ttu-id="f1456-122">completed-\*-errors</span><span class="sxs-lookup"><span data-stu-id="f1456-122">completed-\*-errors</span></span> |<span data-ttu-id="f1456-123">hello 실행을 완료 하지만 조사 해야 하는 오류 (미만 5000).</span><span class="sxs-lookup"><span data-stu-id="f1456-123">hello run completed, but there are errors (fewer than 5,000) that should be investigated.</span></span> |
| <span data-ttu-id="f1456-124">completed-\*-warnings</span><span class="sxs-lookup"><span data-stu-id="f1456-124">completed-\*-warnings</span></span> |<span data-ttu-id="f1456-125">실행 하는 hello 완료 되었지만 일부 데이터가 예상 hello 상태에 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-125">hello run completed, but some data is not in hello expected state.</span></span> <span data-ttu-id="f1456-126">오류가 발생하는 경우 이 메시지는 일반적으로 증상일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-126">If you have errors, then this message is usually only a symptom.</span></span> <span data-ttu-id="f1456-127">오류를 해결할 때까지 경고를 조사하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-127">Until you have addressed errors, you should not investigate warnings.</span></span> |
| <span data-ttu-id="f1456-128">성공</span><span class="sxs-lookup"><span data-stu-id="f1456-128">success</span></span> |<span data-ttu-id="f1456-129">문제가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-129">No issues.</span></span> |

<span data-ttu-id="f1456-130">행을 선택 하면 hello 아래쪽의를 실행 하는 tooshow hello 세부 정보를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-130">When you select a row, hello bottom updates tooshow hello details of that run.</span></span> <span data-ttu-id="f1456-131">toohello hello 아래쪽의 맨 왼쪽, 목록 라는 해야할 **단계 #**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-131">toohello far left of hello bottom, you might have a list saying **Step #**.</span></span> <span data-ttu-id="f1456-132">이 목록은 각 도메인을 단계로 나타내는 포리스트에 여러 도메인이 있는 경우에만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-132">This list only appears if you have multiple domains in your forest where each domain is represented by a step.</span></span> <span data-ttu-id="f1456-133">hello 도메인 이름은 hello 머리글 아래에서 찾을 수 있습니다 **파티션**합니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-133">hello domain name can be found under hello heading **Partition**.</span></span> <span data-ttu-id="f1456-134">아래 **동기화 통계**, 처리 된 변경 내용 수 hello에 대 한 자세한 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-134">Under **Synchronization Statistics**, you can find more information about hello number of changes that were processed.</span></span> <span data-ttu-id="f1456-135">Hello 링크 tooget hello 변경 개체의 목록을 클릭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-135">You can click hello links tooget a list of hello changed objects.</span></span> <span data-ttu-id="f1456-136">오류가 있는 개체가 있으면 해당 오류는 **동기화 오류**아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-136">If you have objects with errors, those errors show up under **Synchronization Errors**.</span></span>

<span data-ttu-id="f1456-137">자세한 내용은 [동기화되지 않는 개체 문제 해결](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1456-137">For more information, see [troubleshoot an object that is not synchronizing](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1456-138">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f1456-138">Next steps</span></span>
<span data-ttu-id="f1456-139">Hello에 대 한 자세한 [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md) 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-139">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="f1456-140">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f1456-140">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
