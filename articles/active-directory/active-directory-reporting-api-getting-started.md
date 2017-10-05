---
title: "Azure AD 클래식 포털에서 Azure AD Reporting API 시작 | Microsoft Docs"
description: "Azure Active Directory Reporting API를 시작하는 방법"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/18/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5e98b660fe19bb8abebf1c3b996b6295a6c4e728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api-on-the-azure-ad-classic-portal"></a><span data-ttu-id="43934-103">Azure AD 클래식 포털에서 Azure Active Directory Reporting API 시작</span><span class="sxs-lookup"><span data-stu-id="43934-103">Getting started with the Azure Active Directory reporting API on the Azure AD classic portal</span></span>
<span data-ttu-id="43934-104">*이 항목은 [Azure Active Directory Reporting 가이드](active-directory-reporting-guide.md)의 일부입니다.*</span><span class="sxs-lookup"><span data-stu-id="43934-104">*This topic is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="43934-105">Azure Active Directory는 다양한 보고서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="43934-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="43934-106">이러한 보고서의 데이터는 SIEM 시스템, 감사 및 비즈니스 인텔리전스 도구와 같은 응용 프로그램에 매우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43934-106">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="43934-107">Azure AD Reporting API는 일련의 REST 기반 API를 통해 데이터에 프로그래밍 방식으로 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="43934-107">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="43934-108">다양한 프로그래밍 언어 및 도구에서 이러한 API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43934-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="43934-109">이 문서에서는 Azure AD Reporting API를 시작하는 데 필요한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="43934-109">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="43934-110">다음 섹션에는 감사 및 로그인 API를 사용하는 방법에 대한 자세한 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43934-110">In the next section, you find more details about using the audit and sign-in APIs.</span></span> <span data-ttu-id="43934-111">다른 모든 API는 [Azure AD 보고서 및 이벤트(미리 보기)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43934-111">For all other APIs, see the [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="43934-112">질문, 문제 또는 피드백은 [AAD Reporting 도움말](mailto:aadreportinghelp@microsoft.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="43934-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="43934-113">학습 맵</span><span class="sxs-lookup"><span data-stu-id="43934-113">Learning map</span></span>
1. <span data-ttu-id="43934-114">**준비** - API 샘플을 테스트하기 전에 [Azure AD Reporting API에 액세스하기 위한 필수 구성 요소](active-directory-reporting-api-prerequisites.md)를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43934-114">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="43934-115">**탐색** - Reporting API의 첫 인상을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="43934-115">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="43934-116">감사 API에 대한 샘플 사용</span><span class="sxs-lookup"><span data-stu-id="43934-116">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="43934-117">로그인 활동 보고서 API에 대한 샘플 사용</span><span class="sxs-lookup"><span data-stu-id="43934-117">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="43934-118">**사용자 지정** - 고유한 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43934-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="43934-119">감사 API 참조 사용</span><span class="sxs-lookup"><span data-stu-id="43934-119">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="43934-120">로그인 활동 보고서 API 참조 사용</span><span class="sxs-lookup"><span data-stu-id="43934-120">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="43934-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="43934-121">Next Steps</span></span>
<span data-ttu-id="43934-122">궁금하시다면 [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta)로 이동하여 모든 사용 가능한 Azure AD Graph API 끝점을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43934-122">If you are curious to see all of the available Azure AD Graph API endpoints by navigating to [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

