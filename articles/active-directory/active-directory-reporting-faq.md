---
title: "Azure Active Directory 보고 FAQ | Microsoft Docs"
description: "Azure Active Directory 보고 FAQ입니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: accf292f70bf0eafdefc00c3feeaf8e346605401
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="fa576-103">Azure Active Directory 보고 FAQ</span><span class="sxs-lookup"><span data-stu-id="fa576-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="fa576-104">이 문서에는 Azure Active Directory 보고에 대한 FAQ(질문과 대답)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-104">This article includes answers to frequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="fa576-105">자세한 내용은 [Azure Active Directory 보고](active-directory-reporting-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa576-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="fa576-106">**Q: Azure Portal에서 활동 로그 (감사 및 로그인)의 데이터 보존은 어떻게 됩니까?**</span><span class="sxs-lookup"><span data-stu-id="fa576-106">**Q: What is the data retention for activity logs (Audit and Sign-ins) in the Azure portal?**</span></span> 

<span data-ttu-id="fa576-107">**A:** 무료 고객의 경우 7일의 데이터 보존을 제공하고 Azure AD Premium 1 또는 2 Premium 라이선스로 전환하면 최대 30일간 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-107">**A:** We provide 7 days of data for our free customers and by switching to an Azure AD Premium 1 or Premium 2 license, you can access data for up to 30 days.</span></span> <span data-ttu-id="fa576-108">보존에 대한 자세한 내용은 [Azure Active Directory 보고서 보존 정책](active-directory-reporting-retention.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa576-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="fa576-109">**Q: 내 작업을 완료한 후 얼마나 지나야 활동 데이터를 볼 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="fa576-109">**Q: How long does it take until I can see the Activity data after I have completed my task?**</span></span>

<span data-ttu-id="fa576-110">**A:** 감사 활동 로그에는 15분에서 1시간까지의 대기 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-110">**A:** Audit activity logs have a latency ranging from 15 mins to an hour.</span></span> <span data-ttu-id="fa576-111">로그인 활동 로그의 대기 시간은 15분(대부분의 레코드)에서 최대 2시간(일부 레코드)입니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up to 2 hours for a few records.</span></span>

---

<span data-ttu-id="fa576-112">**Q: Azure Portal에서 해당 활동을 보거나 API를 통해 데이터를 가져오기 위해 전역 관리자 권한이 필요합니까?**</span><span class="sxs-lookup"><span data-stu-id="fa576-112">**Q: Do I need to be a global admin to see the activity logs in the Azure Portal or to get data through the API?**</span></span>

<span data-ttu-id="fa576-113">**A:** 아니요.</span><span class="sxs-lookup"><span data-stu-id="fa576-113">**A:** No.</span></span> <span data-ttu-id="fa576-114">**보안 읽기 권한자**, **보안 관리자** 또는 **전역 관리자**라면 Azure Portal에서 데이터를 보거나 API를 통해 액세스하여 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** to see reporting data in Azure Portal or by accessing it through the API.</span></span>

---

<span data-ttu-id="fa576-115">**Q: Azure Portal을 통해 Office 365 활동 로그 정보를 얻을 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="fa576-115">**Q: Can I get Office 365 activity log information through the Azure portal?**</span></span>

<span data-ttu-id="fa576-116">**A:** Office 365 활동 및 Azure AD 활동 로그가 많은 디렉터리 리소스를 공유하더라도 Office 365 활동 로그를 전체 보기로 보려는 경우, Office 365 관리 센터로 이동하여 Office 365 활동 로그 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of the directory resources, if you want a full view of the Office 365 activity logs, you should go to the Office 365 Admin Center to get Office 365 Activity log information.</span></span>

---


<span data-ttu-id="fa576-117">**Q: Office 365 활동 로그에 대한 정보를 얻기 위해 어떤 API를 사용해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="fa576-117">**Q: Which APIs do I use to get information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="fa576-118">**A:** Office 365 관리 API를 사용하여 [API를 통해 Office 365 활동 로그](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview)에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-118">**A:** Use the Office 365 Management APIs to access the [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="fa576-119">**Q: Azure Portal에서 몇 개의 레코드를 다운로드할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="fa576-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="fa576-120">**A:** Azure Portal에서 최대 120,000개의 레코드를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-120">**A:** You can download up to 120K records from the Azure portal.</span></span> <span data-ttu-id="fa576-121">레코드는 *가장 최근* 순으로 정렬되며 기본적으로 가장 최근의 120,000개의 레코드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-121">The records are sorted by *most recent* and by default, you get the most recent 120K records.</span></span> 

---

<span data-ttu-id="fa576-122">**Q: API 활동을 통해 몇 개의 레코드를 쿼리할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="fa576-122">**Q: How many records can I query through the activities API?**</span></span>

<span data-ttu-id="fa576-123">**A:** 최대 1백만 개의 레코드를 쿼리할 수 있습니다(top 연산자를 사용하지 않는 경우 가장 최근 순으로 레코드를 정렬함).</span><span class="sxs-lookup"><span data-stu-id="fa576-123">**A:** You can query up to 1 million records (if you don’t use the top operator, which sorts the record by most recent).</span></span> <span data-ttu-id="fa576-124">"top" 연산자를 사용하면 500,000개의 레코드를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-124">If you do use the “top” operator, you can query up to 500K records.</span></span> <span data-ttu-id="fa576-125">여기[여기](active-directory-reporting-api-getting-started.md)에서 API를 사용하는 방법에 대한 샘플 쿼리를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-125">You can find sample queries on how to use the API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="fa576-126">**Q: Premium 라이선스는 어떻게 받을 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="fa576-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="fa576-127">**A:** 이 질문에 대한 답변은 [Azure Active Directory Premium 시작하기](active-directory-get-started-premium.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fa576-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer to this question.</span></span>

---

<span data-ttu-id="fa576-128">**Q: Premium 라이선스를 받은 후 활동 데이터를 보는 데 얼마나 걸리나요?**</span><span class="sxs-lookup"><span data-stu-id="fa576-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="fa576-129">**A:** 무료 라이선스로서 활동 데이터가 이미 있는 경우 동일한 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-129">**A:** If you already have activities data as a free license, then you can see the same data.</span></span> <span data-ttu-id="fa576-130">모든 데이터가 없으면 1일이나 2일 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="fa576-131">**Q: Azure AD Premium 라이선스를 받은 후 지난 달의 데이터를 볼 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="fa576-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="fa576-132">**A:**: 최근에 Premium 버전(평가판 버전을 포함)으로 전환한 경우 최대 7일간 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-132">**A:** If you have recently switched to a Premium version (including a trial version), you can see data up to 7 days initially.</span></span> <span data-ttu-id="fa576-133">데이터가 누적된 경우 최대 30일간 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-133">When data accumulates, you will see up to 30 days.</span></span>

---

<span data-ttu-id="fa576-134">**Q: ID 보호에 위험 이벤트가 있지만 모든 로그인에서 해당 로그인이 표시되는 것은 아닙니다. 이것은 예상된 동작인가요?**</span><span class="sxs-lookup"><span data-stu-id="fa576-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in the all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="fa576-135">**A:** 예. ID 보호는 대화형인지 여부에 관계없이 모든 인증 흐름의 위험을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="fa576-136">그러나 모든 로그인은 대화형 로그인만 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-136">However, all sign-ins only report shows only the interactive sign-ins.</span></span>

---

<span data-ttu-id="fa576-137">**Q: Azure Portal에서 "위험 플래그가 지정된 사용자" 보고서를 다운로드하려면 어떻게 해야 하나요?**</span><span class="sxs-lookup"><span data-stu-id="fa576-137">**Q: How can I download the “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="fa576-138">**A:** *위험 플래그가 지정된 사용자* 보고서를 다운로드하는 옵션이 곧 추가될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-138">**A:** The option to download *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="fa576-139">**Q: Azure Portal에서 로그인 또는 사용자에게 위험 플래그가 지정된 이유를 어떻게 알 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="fa576-139">**Q: How do I know why a sign-in or a user was flagged risky in the Azure portal?**</span></span>

<span data-ttu-id="fa576-140">**A:** Premium Edition 고객은 "위험 플래그가 지정된 사용자"에서 사용자를 클릭하거나 "위험한 로그인"을 클릭하여 기본 위험 이벤트에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-140">**A:** Premium edition customers can learn more about the underlying risk events by clicking on the user in “Users flagged for risk” or by clicking on the “Risky sign-ins”.</span></span> <span data-ttu-id="fa576-141">Free 및 Basic Edition 고객은 기본 위험 이벤트 정보 없이도 위험에 처한 사용자 및 로그인을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-141">Free and Basic edition customers get to see the at-risk users and sign-ins without the underlying risk event information.</span></span>

---

<span data-ttu-id="fa576-142">**Q: IP 주소는 로그인 및 위험한 로그인 보고서에서 어떻게 계산됩니까?**</span><span class="sxs-lookup"><span data-stu-id="fa576-142">**Q: How are IP addresses calculated in the sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="fa576-143">**A:** IP 주소는 IP 주소와 해당 주소가 실제로 연결된 컴퓨터 간에 확실한 연결이 없는 경우와 같은 방법으로 발급됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where the computer with that address is physically located.</span></span> <span data-ttu-id="fa576-144">모바일 공급자 및 클라이언트 장치가 실제로 사용되는 위치에서 종종 매우 먼 중앙 풀에서 IP 주소를 발급하는 VPN과 같은 요인에 의해 복잡합니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where the client device is actually used.</span></span> <span data-ttu-id="fa576-145">위의 설명을 고려하면 IP 주소를 실제 위치로 변환하는 것은 추적, 레지스트리 데이터, 역방향 조회 및 기타 정보에 기반한 최상의 노력입니다.</span><span class="sxs-lookup"><span data-stu-id="fa576-145">Given the above, converting IP address to a physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---
