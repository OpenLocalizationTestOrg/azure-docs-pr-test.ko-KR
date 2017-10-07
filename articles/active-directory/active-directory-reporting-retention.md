---
title: "aaaAzure Active Directory 보고서 보존 정책 | Microsoft Docs"
description: "Azure Active Directory에서 보고서 데이터 보존 정책"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="d1714-103">Azure Active Directory 보고서 보존 정책</span><span class="sxs-lookup"><span data-stu-id="d1714-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="d1714-104">이 항목 toohello Azure Active Directory에서 각기 다른 활동이 보고서 hello에 대 한 데이터 보존 hello와 함께에서 가장 일반적인 질문을 답변 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d1714-104">This topic provides you with answers toohello most common questions in conjunction with hello data retention for hello different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="d1714-105">**Q: 시작 작업 데이터의 hello 컬렉션 어떻게 얻을 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="d1714-105">**Q: How can you get hello collection of activity data started?**</span></span>

<span data-ttu-id="d1714-106">**A:**</span><span class="sxs-lookup"><span data-stu-id="d1714-106">**A:**</span></span>

| <span data-ttu-id="d1714-107">Azure AD 버전</span><span class="sxs-lookup"><span data-stu-id="d1714-107">Azure AD Edition</span></span> | <span data-ttu-id="d1714-108">수집 시작</span><span class="sxs-lookup"><span data-stu-id="d1714-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="d1714-109">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="d1714-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="d1714-110">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="d1714-110">Azure AD Premium P2</span></span> | <span data-ttu-id="d1714-111">구독 등록 시</span><span class="sxs-lookup"><span data-stu-id="d1714-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="d1714-112">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="d1714-112">Azure AD Free</span></span> | <span data-ttu-id="d1714-113">처음으로 열면 hello hello [Azure Active Directory 블레이드](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) hello를 사용 하 여 또는 [Api를 보고 합니다.](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="d1714-113">hello first time you open hello [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use hello [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="d1714-114">**Q: 언제 활동 데이터 hello Azure 포털에서에서 사용할 수 있는?**</span><span class="sxs-lookup"><span data-stu-id="d1714-114">**Q: When is your activity data available in hello Azure portal?**</span></span>

<span data-ttu-id="d1714-115">**A:**</span><span class="sxs-lookup"><span data-stu-id="d1714-115">**A:**</span></span>

- <span data-ttu-id="d1714-116">**즉시** -hello Azure 클래식 포털에서에서 보고서를 이미 작업 한 경우</span><span class="sxs-lookup"><span data-stu-id="d1714-116">**Immediately** - If you have already been working with reports in hello Azure classic portal</span></span>
- <span data-ttu-id="d1714-117">**2 시간 이내에** -켜지 않은 reporting hello Azure 클래식 포털에서에서 하는 경우</span><span class="sxs-lookup"><span data-stu-id="d1714-117">**Within 2 hours** - If you haven’t turned reporting on  in hello Azure classic portal</span></span>

---
<span data-ttu-id="d1714-118">**Q: 시작 하는 보안 신호의 hello 컬렉션 어떻게 얻을 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="d1714-118">**Q: How can you get hello collection of security signals started?**</span></span>  

<span data-ttu-id="d1714-119">**A:** 보안 신호에 대 한 hello 수집 프로세스가 때 옵트인 toouse hello Identity 보호 센터를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1714-119">**A:** For security signals, hello collection process starts when you opt-in toouse hello Identity Protection Center.</span></span> 


---
<span data-ttu-id="d1714-120">**Q: 얼마나 오래 hello 수집 된 데이터 저장 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="d1714-120">**Q: For how long is hello collected data stored?**</span></span>

<span data-ttu-id="d1714-121">**A:**</span><span class="sxs-lookup"><span data-stu-id="d1714-121">**A:**</span></span>

<span data-ttu-id="d1714-122">**작업 보고서**</span><span class="sxs-lookup"><span data-stu-id="d1714-122">**Activity reports**</span></span>    

| <span data-ttu-id="d1714-123">보고서</span><span class="sxs-lookup"><span data-stu-id="d1714-123">Report</span></span>                 | <span data-ttu-id="d1714-124">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="d1714-124">Azure AD Free</span></span> | <span data-ttu-id="d1714-125">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="d1714-125">Azure AD Premium P1</span></span> | <span data-ttu-id="d1714-126">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="d1714-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="d1714-127">디렉터리 감사</span><span class="sxs-lookup"><span data-stu-id="d1714-127">Directory Audit</span></span>        | <span data-ttu-id="d1714-128">7 일</span><span class="sxs-lookup"><span data-stu-id="d1714-128">7 days</span></span>        | <span data-ttu-id="d1714-129">30일</span><span class="sxs-lookup"><span data-stu-id="d1714-129">30 days</span></span>             | <span data-ttu-id="d1714-130">30일</span><span class="sxs-lookup"><span data-stu-id="d1714-130">30 days</span></span>             |
| <span data-ttu-id="d1714-131">로그인 작업</span><span class="sxs-lookup"><span data-stu-id="d1714-131">Sign-in Activity</span></span>       | <span data-ttu-id="d1714-132">7 일</span><span class="sxs-lookup"><span data-stu-id="d1714-132">7 days</span></span>        | <span data-ttu-id="d1714-133">30일</span><span class="sxs-lookup"><span data-stu-id="d1714-133">30 days</span></span>             | <span data-ttu-id="d1714-134">30일</span><span class="sxs-lookup"><span data-stu-id="d1714-134">30 days</span></span>             |

<span data-ttu-id="d1714-135">**보안 신호**</span><span class="sxs-lookup"><span data-stu-id="d1714-135">**Security Signals**</span></span>

| <span data-ttu-id="d1714-136">보고서</span><span class="sxs-lookup"><span data-stu-id="d1714-136">Report</span></span>         | <span data-ttu-id="d1714-137">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="d1714-137">Azure AD Free</span></span> | <span data-ttu-id="d1714-138">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="d1714-138">Azure AD Premium P1</span></span> | <span data-ttu-id="d1714-139">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="d1714-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="d1714-140">위험에 노출된 사용자</span><span class="sxs-lookup"><span data-stu-id="d1714-140">Users at risk</span></span>  | <span data-ttu-id="d1714-141">7 일</span><span class="sxs-lookup"><span data-stu-id="d1714-141">7 days</span></span>        | <span data-ttu-id="d1714-142">30일</span><span class="sxs-lookup"><span data-stu-id="d1714-142">30 days</span></span>             | <span data-ttu-id="d1714-143">90일</span><span class="sxs-lookup"><span data-stu-id="d1714-143">90 days</span></span>             |
| <span data-ttu-id="d1714-144">위험한 로그인</span><span class="sxs-lookup"><span data-stu-id="d1714-144">Risky sign-ins</span></span> | <span data-ttu-id="d1714-145">7 일</span><span class="sxs-lookup"><span data-stu-id="d1714-145">7 days</span></span>        | <span data-ttu-id="d1714-146">30일</span><span class="sxs-lookup"><span data-stu-id="d1714-146">30 days</span></span>             | <span data-ttu-id="d1714-147">90일</span><span class="sxs-lookup"><span data-stu-id="d1714-147">90 days</span></span>             |

---