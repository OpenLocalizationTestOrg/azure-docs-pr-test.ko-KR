---
title: "문제 해결: Azure Active Directory 활동 로그의 누락된 데이터 | Microsoft Docs"
description: "Azure Active Directory 보고에 사용할 수 있는 다양한 보고서 나열"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 7cbe4337-bb77-4ee0-b254-3e368be06db7
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 47617f8f727027de113a0f503308c8accc58859e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="i-cant-find-some-actions-that-i-performed-in-the-azure-active-directory-activity-log"></a><span data-ttu-id="78f15-103">Azure Active Directory 활동 로그에서 수행한 일부 작업을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="78f15-103">I can’t find some actions that I performed in the Azure Active Directory activity log</span></span>


## <a name="symptoms"></a><span data-ttu-id="78f15-104">증상</span><span class="sxs-lookup"><span data-stu-id="78f15-104">Symptoms</span></span>

<span data-ttu-id="78f15-105">Azure Portal에서 일부 작업을 수행했고 `Activity logs > Audit Logs` 블레이드에서 해당 작업에 대한 감사 로그가 표시될 것을 예상했지만 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="78f15-105">I performed some actions in the Azure portal and expected to see the audit logs for those actions in the `Activity logs > Audit Logs` blade, but I can’t find them.</span></span>

 ![보고](./media/active-directory-reporting-troubleshoot-missing-audit-data/01.png)
 

## <a name="cause"></a><span data-ttu-id="78f15-107">원인</span><span class="sxs-lookup"><span data-stu-id="78f15-107">Cause</span></span>

<span data-ttu-id="78f15-108">작업이 활동 감사 로그에 즉시 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="78f15-108">Actions don’t appear immediately in the Activity Audit log.</span></span> <span data-ttu-id="78f15-109">포털에서 감사 로그가 표시되는 데 작업이 수행된 시간부터 15분에서 1시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78f15-109">It can take anywhere from 15 minutes to an hour to see the audit logs in the portal from the time the operation is performed.</span></span>

## <a name="resolution"></a><span data-ttu-id="78f15-110">해결 방법</span><span class="sxs-lookup"><span data-stu-id="78f15-110">Resolution</span></span>

<span data-ttu-id="78f15-111">15분에서 1시간 동안 기다렸다가 로그에 작업이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="78f15-111">Wait for 15 minutes to an hour and see if the actions appear in the log.</span></span> <span data-ttu-id="78f15-112">여전히 표시되지 않으면 지원 티켓을 제기해 주세요. 살펴보도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="78f15-112">If you still don’t see them, please raise a support ticket with us and we will look into it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="78f15-113">다음 단계</span><span class="sxs-lookup"><span data-stu-id="78f15-113">Next steps</span></span>
<span data-ttu-id="78f15-114">[Azure Active Directory 보고 FAQ](active-directory-reporting-faq.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="78f15-114">See the [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

