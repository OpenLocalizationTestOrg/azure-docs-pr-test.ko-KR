---
title: "문제 해결: Azure Active Directory 작업 로그 다운로드 한 hello에 누락 된 데이터 | Microsoft Docs"
description: "다운로드 한 Azure Active Directory 작업 로그에서 확인 toomissing 데이터를 제공합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a><span data-ttu-id="1ce12-103">내가 다운로드 한 hello Azure Active Directory 작업 로그에서 모든 데이터를 찾을 수 없는</span><span class="sxs-lookup"><span data-stu-id="1ce12-103">I can’t find any data in hello Azure Active Directory activity logs I have downloaded</span></span>


## <a name="symptoms"></a><span data-ttu-id="1ce12-104">증상</span><span class="sxs-lookup"><span data-stu-id="1ce12-104">Symptoms</span></span>

<span data-ttu-id="1ce12-105">I (감사 또는 로그인) hello 활동 로그를 다운로드 하 고 hello 시간 선택에 대 한 모든 hello 레코드가 표시 되지 않는 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1ce12-105">I downloaded hello activity logs (audit or sign-ins) and I don’t see all hello records for hello time I chose.</span></span> <span data-ttu-id="1ce12-106">그 이유는</span><span class="sxs-lookup"><span data-stu-id="1ce12-106">Why?</span></span> 

 ![보고](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a><span data-ttu-id="1ce12-108">원인</span><span class="sxs-lookup"><span data-stu-id="1ce12-108">Cause</span></span>

<span data-ttu-id="1ce12-109">Hello 눈금 too120K 레코드를 가장 하 여 정렬 제한 되어 hello Azure 포털에서에서 활동 로그를 다운로드 하면 최신입니다.</span><span class="sxs-lookup"><span data-stu-id="1ce12-109">When you download activity logs in hello Azure portal, we limit hello scale too120K records, sorted by most recent.</span></span> 

## <a name="resolution"></a><span data-ttu-id="1ce12-110">해결 방법</span><span class="sxs-lookup"><span data-stu-id="1ce12-110">Resolution</span></span>

<span data-ttu-id="1ce12-111">활용할 수 있는 [Azure AD Reporting Api](active-directory-reporting-api-getting-started.md) toofetch 특정된 시점에서 tooa 백만 레코드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ce12-111">You can leverage [Azure AD Reporting APIs](active-directory-reporting-api-getting-started.md) toofetch up tooa million records at any given point.</span></span> <span data-ttu-id="1ce12-112">이 권장 방법은 toorun hello 보고 Api toofetch를 호출 하는 일정에 따라 스크립트를 증분 방식에서 시간 동안 기록 (예:: 매일 또는 매주)입니다.</span><span class="sxs-lookup"><span data-stu-id="1ce12-112">Our recommended approach is toorun a script on a scheduled basis that calls hello reporting APIs toofetch records in an incremental fashion over a period of time (e.g., daily or weekly).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ce12-113">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ce12-113">Next steps</span></span>
<span data-ttu-id="1ce12-114">Hello 참조 [FAQ를 보고 하는 Azure Active Directory](active-directory-reporting-faq.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1ce12-114">See hello [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

