---
title: "Azure Active Directory 보고서 보존 정책 | Microsoft Docs"
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
ms.openlocfilehash: ffeba8a6c32a21c75af21f948bbd6ea88dd9278c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="099af-103">Azure Active Directory 보고서 보존 정책</span><span class="sxs-lookup"><span data-stu-id="099af-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="099af-104">이 문서에서는 Azure Active Directory의 여러 작업 보고서에 대한 데이터 보존과 함께 가장 일반적인 질문에 대한 대답을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="099af-104">This topic provides you with answers to the most common questions in conjunction with the data retention for the different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="099af-105">**Q: 작업 데이터 수집을 시작하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="099af-105">**Q: How can you get the collection of activity data started?**</span></span>

<span data-ttu-id="099af-106">**A:**</span><span class="sxs-lookup"><span data-stu-id="099af-106">**A:**</span></span>

| <span data-ttu-id="099af-107">Azure AD 버전</span><span class="sxs-lookup"><span data-stu-id="099af-107">Azure AD Edition</span></span> | <span data-ttu-id="099af-108">수집 시작</span><span class="sxs-lookup"><span data-stu-id="099af-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="099af-109">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="099af-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="099af-110">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="099af-110">Azure AD Premium P2</span></span> | <span data-ttu-id="099af-111">구독 등록 시</span><span class="sxs-lookup"><span data-stu-id="099af-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="099af-112">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="099af-112">Azure AD Free</span></span> | <span data-ttu-id="099af-113">처음으로 [Azure Active Directory 블레이드](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)를 열거나 [보고 API](https://aka.ms/aadreports)를 사용할 때</span><span class="sxs-lookup"><span data-stu-id="099af-113">The first time you open the [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use the [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="099af-114">**Q: Azure Portal에서 작업 데이터를 사용할 수 있는 시기는 언제인가요?**</span><span class="sxs-lookup"><span data-stu-id="099af-114">**Q: When is your activity data available in the Azure portal?**</span></span>

<span data-ttu-id="099af-115">**A:**</span><span class="sxs-lookup"><span data-stu-id="099af-115">**A:**</span></span>

- <span data-ttu-id="099af-116">**즉시** - 이미 Azure 클래식 포털에서 보고서로 작업한 적이 있는 경우</span><span class="sxs-lookup"><span data-stu-id="099af-116">**Immediately** - If you have already been working with reports in the Azure classic portal</span></span>
- <span data-ttu-id="099af-117">**2시간 이내** - Azure 클래식 포털에서 보고 기능을 설정하지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="099af-117">**Within 2 hours** - If you haven’t turned reporting on  in the Azure classic portal</span></span>

---
<span data-ttu-id="099af-118">**Q: 보안 신호 수집을 시작하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="099af-118">**Q: How can you get the collection of security signals started?**</span></span>  

<span data-ttu-id="099af-119">**A:** 보안 신호의 경우 ID 보호 센터를 사용하도록 옵트인할 때 수집 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="099af-119">**A:** For security signals, the collection process starts when you opt-in to use the Identity Protection Center.</span></span> 


---
<span data-ttu-id="099af-120">**Q: 수집된 데이터의 저장 기간은 얼마나 되나요?**</span><span class="sxs-lookup"><span data-stu-id="099af-120">**Q: For how long is the collected data stored?**</span></span>

<span data-ttu-id="099af-121">**A:**</span><span class="sxs-lookup"><span data-stu-id="099af-121">**A:**</span></span>

<span data-ttu-id="099af-122">**작업 보고서**</span><span class="sxs-lookup"><span data-stu-id="099af-122">**Activity reports**</span></span>    

| <span data-ttu-id="099af-123">보고서</span><span class="sxs-lookup"><span data-stu-id="099af-123">Report</span></span>                 | <span data-ttu-id="099af-124">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="099af-124">Azure AD Free</span></span> | <span data-ttu-id="099af-125">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="099af-125">Azure AD Premium P1</span></span> | <span data-ttu-id="099af-126">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="099af-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="099af-127">디렉터리 감사</span><span class="sxs-lookup"><span data-stu-id="099af-127">Directory Audit</span></span>        | <span data-ttu-id="099af-128">7 일</span><span class="sxs-lookup"><span data-stu-id="099af-128">7 days</span></span>        | <span data-ttu-id="099af-129">30일</span><span class="sxs-lookup"><span data-stu-id="099af-129">30 days</span></span>             | <span data-ttu-id="099af-130">30일</span><span class="sxs-lookup"><span data-stu-id="099af-130">30 days</span></span>             |
| <span data-ttu-id="099af-131">로그인 작업</span><span class="sxs-lookup"><span data-stu-id="099af-131">Sign-in Activity</span></span>       | <span data-ttu-id="099af-132">7 일</span><span class="sxs-lookup"><span data-stu-id="099af-132">7 days</span></span>        | <span data-ttu-id="099af-133">30일</span><span class="sxs-lookup"><span data-stu-id="099af-133">30 days</span></span>             | <span data-ttu-id="099af-134">30일</span><span class="sxs-lookup"><span data-stu-id="099af-134">30 days</span></span>             |

<span data-ttu-id="099af-135">**보안 신호**</span><span class="sxs-lookup"><span data-stu-id="099af-135">**Security Signals**</span></span>

| <span data-ttu-id="099af-136">보고서</span><span class="sxs-lookup"><span data-stu-id="099af-136">Report</span></span>         | <span data-ttu-id="099af-137">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="099af-137">Azure AD Free</span></span> | <span data-ttu-id="099af-138">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="099af-138">Azure AD Premium P1</span></span> | <span data-ttu-id="099af-139">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="099af-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="099af-140">위험에 노출된 사용자</span><span class="sxs-lookup"><span data-stu-id="099af-140">Users at risk</span></span>  | <span data-ttu-id="099af-141">7 일</span><span class="sxs-lookup"><span data-stu-id="099af-141">7 days</span></span>        | <span data-ttu-id="099af-142">30일</span><span class="sxs-lookup"><span data-stu-id="099af-142">30 days</span></span>             | <span data-ttu-id="099af-143">90일</span><span class="sxs-lookup"><span data-stu-id="099af-143">90 days</span></span>             |
| <span data-ttu-id="099af-144">위험한 로그인</span><span class="sxs-lookup"><span data-stu-id="099af-144">Risky sign-ins</span></span> | <span data-ttu-id="099af-145">7 일</span><span class="sxs-lookup"><span data-stu-id="099af-145">7 days</span></span>        | <span data-ttu-id="099af-146">30일</span><span class="sxs-lookup"><span data-stu-id="099af-146">30 days</span></span>             | <span data-ttu-id="099af-147">90일</span><span class="sxs-lookup"><span data-stu-id="099af-147">90 days</span></span>             |

---