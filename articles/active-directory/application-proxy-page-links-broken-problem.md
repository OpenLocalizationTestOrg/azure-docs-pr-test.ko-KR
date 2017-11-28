---
title: "aaaLinks hello 페이지에서 응용 프로그램 프록시 응용 프로그램에 대해 작동 하지 않는 | Microsoft Docs"
description: "Azure AD와 통합 하는 응용 프로그램 프록시 응용 프로그램에 대 한 링크가 끊어진 tootroubleshoot 발급 하는 방법"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 77c1e22d27c7a6436d8e57e105037c2328180481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="links-on-hello-page-dont-work-for-an-application-proxy-application"></a><span data-ttu-id="99115-103">응용 프로그램 프록시 응용 프로그램에 대 한 hello 페이지에는 링크가 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99115-103">Links on hello page don't work for an Application Proxy application</span></span>

<span data-ttu-id="99115-104">이 문서가 도움이 되었나요 tootroubleshoot Azure Active Directory 응용 프로그램 프록시 응용 프로그램에 대 한 링크 올바르게 작동 하지 않는 이유.</span><span class="sxs-lookup"><span data-stu-id="99115-104">This article help you tootroubleshoot why links on your Azure Active Directory Application Proxy application don't work correctly.</span></span>

## <a name="overview"></a><span data-ttu-id="99115-105">개요</span><span class="sxs-lookup"><span data-stu-id="99115-105">Overview</span></span> 
<span data-ttu-id="99115-106">응용 프로그램 프록시 응용 프로그램을 게시 한 후 hello 링크만 hello 응용 프로그램에서 기본적으로 작업 링크 toodestinations hello 내에 포함 된 지 루트 URL을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="99115-106">After publishing an Application Proxy app, hello only links that work by default in hello application are links toodestinations contained within hello published root URL.</span></span> <span data-ttu-id="99115-107">hello 링크 hello 응용 프로그램 내에서 작동 하지 않는, hello 응용 프로그램에 대 한 내부 URL hello 아마도 모든 hello 대상 hello 응용 프로그램 내에서 링크의 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99115-107">hello links within hello applications aren’t working, hello internal URL for hello application probably does not include all hello destinations of links within hello application.</span></span>

<span data-ttu-id="99115-108">**이런 문제가 발생하는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="99115-108">**Why does this happen?**</span></span> <span data-ttu-id="99115-109">응용 프로그램 프록시 시도 tooresolve hello URL 내에서 내부 URL로 hello 동일 응용 프로그램에서 링크를 클릭 했을 때 응용 프로그램 또는 외부에서 사용 가능한 URL로 합니다.</span><span class="sxs-lookup"><span data-stu-id="99115-109">When clicking a link in an application, Application Proxy tries tooresolve hello URL as either an internal URL within hello same application, or as an externally available URL.</span></span> <span data-ttu-id="99115-110">Hello 링크 내에 없는 tooan 내부 URL을 가리키는 경우 hello 동일 응용 프로그램 이러한 버킷 tooeither 속해야 하며 찾을 수 없음 오류가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99115-110">If hello link points tooan internal URL that is not within hello same application, it does not belong tooeither of these buckets and result in a not found error.</span></span>

## <a name="ways-you-can-resolve-broken-links"></a><span data-ttu-id="99115-111">끊어진 링크 문제를 해결할 수 있는 방법</span><span class="sxs-lookup"><span data-stu-id="99115-111">Ways you can resolve broken links</span></span>

<span data-ttu-id="99115-112">이 문제는 세 가지 방법으로 tooresolve 합니다.</span><span class="sxs-lookup"><span data-stu-id="99115-112">There are three ways tooresolve this issue.</span></span> <span data-ttu-id="99115-113">아래 hello 선택 항목에 나열 된 복잡성에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99115-113">hello choices below are in listed in increasing complexity.</span></span>

1.  <span data-ttu-id="99115-114">내부 URL hello hello 응용 프로그램에 대 한 모든 hello 관련 링크를 포함 하는 루트 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="99115-114">Make sure hello internal URL is a root that contains all hello relevant links for hello application.</span></span> <span data-ttu-id="99115-115">이렇게 하면 동일한 hello 내에서 콘텐츠 게시로 확인 하는 모든 링크 toobe 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="99115-115">This allows all links toobe resolved as content published within hello same application.</span></span>

    <span data-ttu-id="99115-116">Hello 내부 URL을 변경 해도 toochange hello 사용자가 페이지를 방문 하지 않을 경우 hello 홈 페이지 URL toohello 변경 이전에 내부 URL을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="99115-116">If you change hello internal URL but don’t want toochange hello landing page for users, change hello Home page URL toohello previously published internal URL.</span></span> <span data-ttu-id="99115-117">너무 이동 하 여이 작업을 수행할 수 있습니다 "Azure Active Directory"-&gt; 앱 등록-&gt; hello 응용 프로그램-선택&gt; 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="99115-117">This can be done by going too“Azure Active Directory” -&gt; App Registrations -&gt; select hello application -&gt; Properties.</span></span> <span data-ttu-id="99115-118">이 속성 탭에서 조정할 수 있습니다 "홈 페이지 URL" hello 필드 표시 toobe hello 방문 페이지를 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="99115-118">In this properties tab, you see hello field “Home Page URL” which you can adjust toobe hello desired landing page.</span></span>

2.  <span data-ttu-id="99115-119">응용 프로그램에서 정규화 된 도메인 이름 (Fqdn)을 사용 하는 경우 사용 하 여 [사용자 지정 도메인](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) toopublish 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="99115-119">If your applications use fully qualified domain names (FQDNs), use [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) toopublish your applications.</span></span> <span data-ttu-id="99115-120">Hello 동일한 URL toobe 모두 내부적으로 사용 되며 외부에서이 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99115-120">This feature allows hello same URL toobe used both internally and externally.</span></span>

    <span data-ttu-id="99115-121">이 옵션 hello 응용 프로그램 toointernal Url에서 링크를 눌러도 hello 외부적으로 인식도 이후 응용 프로그램에서 hello 링크는 응용 프로그램 프록시를 통해 외부에서 액세스할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="99115-121">This option ensures that hello links in your application are externally accessible through Application Proxy since hello links within hello application toointernal URLs are also recognized externally.</span></span> <span data-ttu-id="99115-122">모든 링크에 여전히 toobelong tooa 필요 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="99115-122">Note that all links still need toobelong tooa published application.</span></span> <span data-ttu-id="99115-123">그러나이 옵션 hello 링크 필요 하지 않습니다 toobelong toohello 동일한 응용 프로그램 toomultiple 응용 프로그램에 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99115-123">However, with this option hello links do not need toobelong toohello same application and can belong toomultiple applications.</span></span>

3.  <span data-ttu-id="99115-124">이러한 옵션 중 어느 것도 쉽지 않은 경우 hello 미리 보기 URL 변환/다시 쓰기를 수행 하는 새로운 기능에 대 한 조인 합니다.</span><span class="sxs-lookup"><span data-stu-id="99115-124">If neither of these options are feasible, you join hello preview for a new feature that do URL translation/rewriting.</span></span> <span data-ttu-id="99115-125">이 옵션을 사용 내부 Url 또는 응용 프로그램의 HTML hello 본문에 있는 링크 수 toohello 외부 응용 프로그램 프록시 Url을 게시 변환 "매핑" 되거나, 합니다.</span><span class="sxs-lookup"><span data-stu-id="99115-125">With this option, internal URLs or links that exist in hello HTML body of your applications be translated, or “mapped”, toohello published external App Proxy URLs.</span></span> <span data-ttu-id="99115-126">HTML 또는 CSS hello에 대 한 링크에 대 한이 에서만 작동 하 고이 경우에 도움이 되지 링크가 JS를 통해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99115-126">This only works for links in hello HTML or CSS, and this not help if your link is generated through JS.</span></span> 

<span data-ttu-id="99115-127">결과적으로, 강력 하 게 사용할 수 있는 권장 hello [사용자 지정 도메인](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) 가능 하면 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="99115-127">As a result, we strongly recommend using hello [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution if possible.</span></span> <span data-ttu-id="99115-128">Toojoin hello 미리 보기를 보려면 전자 메일로 보내는 < aadapfeedback@microsoft.com > hello applicationId(s) 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99115-128">If you do want toojoin hello preview, email <aadapfeedback@microsoft.com> with hello applicationId(s).</span></span>

## <a name="next-steps"></a><span data-ttu-id="99115-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="99115-129">Next steps</span></span>
[<span data-ttu-id="99115-130">기존 온-프레미스 프록시 서버 작업</span><span class="sxs-lookup"><span data-stu-id="99115-130">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)

