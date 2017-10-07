---
title: "aaaGetting hello Azure AD 보고 API 시작 | Microsoft Docs"
description: "Tooget를 어떻게 시작 hello Azure Active Directory 보고 API"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/18/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: bb7d72ba445daa367d7502889c38a605a16f26d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api"></a><span data-ttu-id="e54fe-103">Azure Active Directory 보고 API hello 시작</span><span class="sxs-lookup"><span data-stu-id="e54fe-103">Getting started with hello Azure Active Directory reporting API</span></span>

<span data-ttu-id="e54fe-104">Azure Active Directory는 다양한 보고서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e54fe-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="e54fe-105">이러한 보고서의 hello 데이터 SIEM 시스템, 감사, 비즈니스 인텔리전스 도구 등 매우 유용한 tooyour 응용 프로그램을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e54fe-105">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="e54fe-106">hello Azure AD reporting Api는 REST 기반 Api 집합을 통해 toohello 데이터에 프로그래밍 방식 액세스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e54fe-106">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="e54fe-107">다양한 프로그래밍 언어 및 도구에서 이러한 API를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e54fe-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="e54fe-108">이 문서에서는 tooget hello Azure AD 보고를 시작 해야 하는 hello 정보로 Api입니다.</span><span class="sxs-lookup"><span data-stu-id="e54fe-108">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="e54fe-109">Hello 다음 섹션에서는 hello를 사용 하는 방법에 대 한 자세한 내용은 감사 하 고 로그인 Api를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="e54fe-109">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> 

<span data-ttu-id="e54fe-110">질문과 대답(FAQ)는 [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq)를 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="e54fe-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="e54fe-111">문제는 [지원 티켓을 파일로 저장하세요](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="e54fe-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="e54fe-112">학습 맵</span><span class="sxs-lookup"><span data-stu-id="e54fe-112">Learning map</span></span>
1. <span data-ttu-id="e54fe-113">**준비** -API 예제를 테스트 하려면 먼저 toocomplete hello [필수 구성 요소 tooaccess hello Azure AD 보고 API](active-directory-reporting-api-prerequisites-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e54fe-113">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="e54fe-114">**탐색** -hello 보고 Api의 첫 번째 인상을 가져오기:</span><span class="sxs-lookup"><span data-stu-id="e54fe-114">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="e54fe-115">Hello 샘플을 사용 하 여 hello 감사 API에 대 한</span><span class="sxs-lookup"><span data-stu-id="e54fe-115">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="e54fe-116">Hello 샘플을 사용 하 여 hello 로그인 활동 보고서 API에 대 한</span><span class="sxs-lookup"><span data-stu-id="e54fe-116">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="e54fe-117">**사용자 지정** - 고유한 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e54fe-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="e54fe-118">Hello 감사 API 참조를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e54fe-118">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="e54fe-119">Hello 로그인 활동 보고서를 사용 하 여 API 참조</span><span class="sxs-lookup"><span data-stu-id="e54fe-119">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="e54fe-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e54fe-120">Next Steps</span></span>
<span data-ttu-id="e54fe-121">자세한 내용을 보려면 toosee 하려는 경우이 링크를 사용 하 여 사용 가능한 모든 Azure AD Graph API 끝점: [https://graph.windows.net/tenant-name/activities/$ metadata? api 버전 = beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta)합니다.</span><span class="sxs-lookup"><span data-stu-id="e54fe-121">If you are curious toosee all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

