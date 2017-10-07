---
title: "aaaGetting hello Azure AD 클래식 포털에서 Azure AD hello 보고 API 시작 | Microsoft Docs"
description: "Tooget를 어떻게 시작 hello Azure Active Directory 보고 API"
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
ms.openlocfilehash: 52e22d442650731fc6ed28991fc65f9182af0540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api-on-hello-azure-ad-classic-portal"></a><span data-ttu-id="e4d39-103">Azure Active Directory 보고 API hello Azure AD 클래식 포털에서 hello 시작</span><span class="sxs-lookup"><span data-stu-id="e4d39-103">Getting started with hello Azure Active Directory reporting API on hello Azure AD classic portal</span></span>
<span data-ttu-id="e4d39-104">*이 항목은 hello의 일부 [Azure Active Directory Reporting 가이드](active-directory-reporting-guide.md)합니다.*</span><span class="sxs-lookup"><span data-stu-id="e4d39-104">*This topic is part of hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="e4d39-105">Azure Active Directory는 다양한 보고서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4d39-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="e4d39-106">이러한 보고서의 hello 데이터 SIEM 시스템, 감사, 비즈니스 인텔리전스 도구 등 매우 유용한 tooyour 응용 프로그램을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4d39-106">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="e4d39-107">hello Azure AD reporting Api는 REST 기반 Api 집합을 통해 toohello 데이터에 프로그래밍 방식 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4d39-107">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="e4d39-108">다양한 프로그래밍 언어 및 도구에서 이러한 API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4d39-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="e4d39-109">이 문서에서는 tooget hello Azure AD 보고를 시작 해야 하는 hello 정보로 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="e4d39-109">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="e4d39-110">Hello 다음 섹션에서는 hello를 사용 하는 방법에 대 한 자세한 내용은 감사 하 고 로그인 Api를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="e4d39-110">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> <span data-ttu-id="e4d39-111">다른 모든 Api에 대 한 참조 hello [Azure AD 보고서 및 events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) 문서.</span><span class="sxs-lookup"><span data-stu-id="e4d39-111">For all other APIs, see hello [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="e4d39-112">질문, 문제 또는 피드백은 [AAD Reporting 도움말](mailto:aadreportinghelp@microsoft.com)에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="e4d39-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="e4d39-113">학습 맵</span><span class="sxs-lookup"><span data-stu-id="e4d39-113">Learning map</span></span>
1. <span data-ttu-id="e4d39-114">**준비** -API 예제를 테스트 하려면 먼저 toocomplete hello [필수 구성 요소 tooaccess hello Azure AD 보고 API](active-directory-reporting-api-prerequisites.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4d39-114">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="e4d39-115">**탐색** -hello 보고 Api의 첫 번째 인상을 가져오기:</span><span class="sxs-lookup"><span data-stu-id="e4d39-115">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="e4d39-116">Hello 샘플을 사용 하 여 hello 감사 API에 대 한</span><span class="sxs-lookup"><span data-stu-id="e4d39-116">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="e4d39-117">Hello 샘플을 사용 하 여 hello 로그인 활동 보고서 API에 대 한</span><span class="sxs-lookup"><span data-stu-id="e4d39-117">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="e4d39-118">**사용자 지정** - 고유한 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4d39-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="e4d39-119">Hello 감사 API 참조를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e4d39-119">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="e4d39-120">Hello 로그인 활동 보고서를 사용 하 여 API 참조</span><span class="sxs-lookup"><span data-stu-id="e4d39-120">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="e4d39-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e4d39-121">Next Steps</span></span>
<span data-ttu-id="e4d39-122">자세한 내용을 보려면 toosee 하려는 경우 사용 가능한 Azure AD Graph API 끝점 너무 이동 하 여 hello 모든[https://graph.windows.net/tenant-name/reports/$ metadata? api 버전 = beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4d39-122">If you are curious toosee all of hello available Azure AD Graph API endpoints by navigating too[https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

