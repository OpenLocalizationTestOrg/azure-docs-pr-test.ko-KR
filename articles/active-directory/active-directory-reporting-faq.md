---
title: "aaaAzure Active Directory 보고 FAQ | Microsoft Docs"
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
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="4a1a6-103">Azure Active Directory 보고 FAQ</span><span class="sxs-lookup"><span data-stu-id="4a1a6-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="4a1a6-104">이 문서는 질문과 대답 (Faq) Azure Active Directory 보고에 대 한 답변 toofrequently 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-104">This article includes answers toofrequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="4a1a6-105">자세한 내용은 [Azure Active Directory 보고](active-directory-reporting-azure-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="4a1a6-106">**Q: 이란 활동 로그 (감사 및 로그인)에 대 한 데이터 보존 hello hello Azure 포털에서**</span><span class="sxs-lookup"><span data-stu-id="4a1a6-106">**Q: What is hello data retention for activity logs (Audit and Sign-ins) in hello Azure portal?**</span></span> 

<span data-ttu-id="4a1a6-107">**A:** 무료 자사 고객을 위해 및 tooan Azure AD Premium 1 또는 2 Premium 라이선스를 전환 하 여 7 일 분량의 데이터를 제공, too30 일 구성에 대 한 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-107">**A:** We provide 7 days of data for our free customers and by switching tooan Azure AD Premium 1 or Premium 2 license, you can access data for up too30 days.</span></span> <span data-ttu-id="4a1a6-108">보존에 대한 자세한 내용은 [Azure Active Directory 보고서 보존 정책](active-directory-reporting-retention.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="4a1a6-109">**Q: 어떻게 시간이 걸리나요까지 작업 완료 된 후 hello 활동 데이터를 볼 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="4a1a6-109">**Q: How long does it take until I can see hello Activity data after I have completed my task?**</span></span>

<span data-ttu-id="4a1a6-110">**A:** 감사 작업 로그는 15 분 tooan 시간에서 사이의 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-110">**A:** Audit activity logs have a latency ranging from 15 mins tooan hour.</span></span> <span data-ttu-id="4a1a6-111">로그인 활동 로그에서 대부분의 레코드에 대 한 및 소수의 레코드에 대 한 too2 시간이 15 분 사이의 대기 시간이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up too2 hours for a few records.</span></span>

---

<span data-ttu-id="4a1a6-112">**Q: 전역 관리자 toosee hello 활동 hello Azure 포털 또는 hello API 통해 tooget 데이터 로그인 toobe 필요 합니까?**</span><span class="sxs-lookup"><span data-stu-id="4a1a6-112">**Q: Do I need toobe a global admin toosee hello activity logs in hello Azure Portal or tooget data through hello API?**</span></span>

<span data-ttu-id="4a1a6-113">**A:** 아니요.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-113">**A:** No.</span></span> <span data-ttu-id="4a1a6-114">일 수 있습니다는 **보안 판독기**, **보안 관리자** 또는 **전역 관리자** toosee 또는 hello API 통해 액세스 하 여 Azure 포털에서 데이터를 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** toosee reporting data in Azure Portal or by accessing it through hello API.</span></span>

---

<span data-ttu-id="4a1a6-115">**Q: hello Azure 포털을 통해 Office 365 활동 로그 정보를 얻을 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="4a1a6-115">**Q: Can I get Office 365 activity log information through hello Azure portal?**</span></span>

<span data-ttu-id="4a1a6-116">**A:** 있지만 Office 365 활동 및 Azure AD 활동 로그 공유 전체적으로 파악 하려는 경우 hello 디렉터리 리소스를 많이 hello Office 365 활동 로그, toohello Office 365 관리 센터 tooget Office 365 활동 로그 정보 정렬을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of hello directory resources, if you want a full view of hello Office 365 activity logs, you should go toohello Office 365 Admin Center tooget Office 365 Activity log information.</span></span>

---


<span data-ttu-id="4a1a6-117">**Q: 어떤 Api 않으면 Office 365 활동 로그에 대 한 tooget 정보를 사용 합니까?**</span><span class="sxs-lookup"><span data-stu-id="4a1a6-117">**Q: Which APIs do I use tooget information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="4a1a6-118">**A:** 사용 하 여 hello Office 365 관리 Api tooaccess hello [API를 통해 Office 365 활동 로그](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-118">**A:** Use hello Office 365 Management APIs tooaccess hello [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="4a1a6-119">**Q: Azure Portal에서 몇 개의 레코드를 다운로드할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="4a1a6-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="4a1a6-120">**A:** hello Azure 포털에서에서 too120K 레코드를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-120">**A:** You can download up too120K records from hello Azure portal.</span></span> <span data-ttu-id="4a1a6-121">hello 레코드 기준으로 정렬 됩니다 *가장 최근의* 기본적으로 가장 최근의 120 K hello 레코드 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-121">hello records are sorted by *most recent* and by default, you get hello most recent 120K records.</span></span> 

---

<span data-ttu-id="4a1a6-122">**Q: API hello 활동을 통해 몇 개의 레코드 쿼리할 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="4a1a6-122">**Q: How many records can I query through hello activities API?**</span></span>

<span data-ttu-id="4a1a6-123">**A:** too1 백만 레코드를 쿼리할 수 있습니다 (대부분 hello 레코드를 정렬 하는 hello top 연산자를 사용 하지 않으면 최근).</span><span class="sxs-lookup"><span data-stu-id="4a1a6-123">**A:** You can query up too1 million records (if you don’t use hello top operator, which sorts hello record by most recent).</span></span> <span data-ttu-id="4a1a6-124">Hello "top" 연산자를 사용 하면 too500K 레코드를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-124">If you do use hello “top” operator, you can query up too500K records.</span></span> <span data-ttu-id="4a1a6-125">어떻게 toouse hello API 여기에 샘플 쿼리를 찾을 수 있습니다 [여기](active-directory-reporting-api-getting-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-125">You can find sample queries on how toouse hello API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="4a1a6-126">**Q: Premium 라이선스는 어떻게 받을 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="4a1a6-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="4a1a6-127">**A:** 참조 [Azure Active Directory Premium 시작](active-directory-get-started-premium.md) 응답 toothis 질문에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer toothis question.</span></span>

---

<span data-ttu-id="4a1a6-128">**Q: Premium 라이선스를 받은 후 활동 데이터를 보는 데 얼마나 걸리나요?**</span><span class="sxs-lookup"><span data-stu-id="4a1a6-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="4a1a6-129">**A:** 활동 데이터 무료 라이선스를 이미 있는 경우 볼 수 있습니다 hello 같은 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-129">**A:** If you already have activities data as a free license, then you can see hello same data.</span></span> <span data-ttu-id="4a1a6-130">모든 데이터가 없으면 1일이나 2일 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="4a1a6-131">**Q: Azure AD Premium 라이선스를 받은 후 지난 달의 데이터를 볼 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="4a1a6-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="4a1a6-132">**A:** tooa Premium 버전 (평가판 버전 포함), 최근에 전환한 경우 데이터를 too7 일을 처음 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-132">**A:** If you have recently switched tooa Premium version (including a trial version), you can see data up too7 days initially.</span></span> <span data-ttu-id="4a1a6-133">데이터를 누적 하는 경우 too30 일 수를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-133">When data accumulates, you will see up too30 days.</span></span>

---

<span data-ttu-id="4a1a6-134">**Q: 위험 이벤트 Id 보호에서 있지만 표시 되지 않는 해당 로그인 hello에서 모든 로그인 합니다. 이것은 예상된 동작인가요?**</span><span class="sxs-lookup"><span data-stu-id="4a1a6-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in hello all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="4a1a6-135">**A:** 예. ID 보호는 대화형인지 여부에 관계없이 모든 인증 흐름의 위험을 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="4a1a6-136">그러나 모든 로그인만 보고서 대화형 로그인만 hello를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-136">However, all sign-ins only report shows only hello interactive sign-ins.</span></span>

---

<span data-ttu-id="4a1a6-137">**Q: Azure 포털에서 hello "위험 플래그가 지정 된 사용자 가" 보고서를 다운로드 하려면 어떻게 해야 합니까?**</span><span class="sxs-lookup"><span data-stu-id="4a1a6-137">**Q: How can I download hello “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="4a1a6-138">**A:** hello 옵션 toodownload *위험에 대 한 플래그가 지정 된 사용자가* 보고서 곧 추가 될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-138">**A:** hello option toodownload *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="4a1a6-139">**Q: 이유는 로그인 또는 사용자 플래그가 지정 된 hello Azure 포털에서에서 위험한 어떻게 알 수 있습니까?**</span><span class="sxs-lookup"><span data-stu-id="4a1a6-139">**Q: How do I know why a sign-in or a user was flagged risky in hello Azure portal?**</span></span>

<span data-ttu-id="4a1a6-140">**A:** Premium edition 고객 hello hello 사용자의 "위험 플래그가 지정 된 사용자"를 클릭 하 여 이나 hello "위험한 로그인"을 클릭 하 여 위험 이벤트의 원본에 대해 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-140">**A:** Premium edition customers can learn more about hello underlying risk events by clicking on hello user in “Users flagged for risk” or by clicking on hello “Risky sign-ins”.</span></span> <span data-ttu-id="4a1a6-141">Free 및 Basic edition 고객 hello 위험 이벤트 정보 원본으로 사용 하지 않고 toosee hello 위험 가능성이 있는 사용자와 로그인을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-141">Free and Basic edition customers get toosee hello at-risk users and sign-ins without hello underlying risk event information.</span></span>

---

<span data-ttu-id="4a1a6-142">**Q: IP 주소를 hello 로그인 및 로그인 위험한 보고서에서 계산 되는 어떻게 합니까?**</span><span class="sxs-lookup"><span data-stu-id="4a1a6-142">**Q: How are IP addresses calculated in hello sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="4a1a6-143">**A:** IP 주소는 IP 주소 및 해당 주소를 사용 하 여 hello 컴퓨터는 실제로 연결 되지 선언적 인지 하는 방식으로 발급 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where hello computer with that address is physically located.</span></span> <span data-ttu-id="4a1a6-144">이 모바일 공급자 및 hello 클라이언트 장치는 실제로 사용 위치에 크게 못 미치는 중앙 풀에서 IP 주소를 매우 자주 실행 하는 Vpn 등의 요인 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where hello client device is actually used.</span></span> <span data-ttu-id="4a1a6-145">IP 주소 tooa 물리적 위치를 변환 하 추적, 레지스트리 데이터, 역방향 모양 ups 및 기타 정보에 따라 최상의 노력은 위의 hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a1a6-145">Given hello above, converting IP address tooa physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---
