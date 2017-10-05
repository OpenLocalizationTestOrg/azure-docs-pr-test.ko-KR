---
title: "페이지의 링크가 응용 프로그램 프록시 응용 프로그램에서 작동하지 않음 | Microsoft Docs"
description: "Azure AD와 통합한 응용 프로그램 프록시 응용 프로그램에 대한 링크가 끊어지는 문제를 해결하는 방법"
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
ms.openlocfilehash: 83c4261fab0498541591c01f9bb692b396c7b751
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="links-on-the-page-dont-work-for-an-application-proxy-application"></a><span data-ttu-id="108d8-103">페이지의 링크가 응용 프로그램 프록시 응용 프로그램에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-103">Links on the page don't work for an Application Proxy application</span></span>

<span data-ttu-id="108d8-104">이 문서를 통해 Azure Active Directory 응용 프로그램 프록시 응용 프로그램의 링크가 올바르게 작동하지 않는 원인을 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-104">This article help you to troubleshoot why links on your Azure Active Directory Application Proxy application don't work correctly.</span></span>

## <a name="overview"></a><span data-ttu-id="108d8-105">개요</span><span class="sxs-lookup"><span data-stu-id="108d8-105">Overview</span></span> 
<span data-ttu-id="108d8-106">응용 프로그램 프록시 앱을 게시한 후에 응용 프로그램에서 기본적으로 작동하는 유일한 링크는 게시된 루트 URL 내에 포함된 대상에 대한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-106">After publishing an Application Proxy app, the only links that work by default in the application are links to destinations contained within the published root URL.</span></span> <span data-ttu-id="108d8-107">응용 프로그램 내에 있는 링크가 작동하지 않으면 응용 프로그램의 내부 URL은 아마도 응용 프로그램 내에서 링크의 모든 대상을 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-107">The links within the applications aren’t working, the internal URL for the application probably does not include all the destinations of links within the application.</span></span>

<span data-ttu-id="108d8-108">**이런 문제가 발생하는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="108d8-108">**Why does this happen?**</span></span> <span data-ttu-id="108d8-109">응용 프로그램에서 링크를 클릭하면 응용 프로그램 프록시는 동일한 응용 프로그램 내에서 내부 URL 또는 외부에서 사용 가능한 URL을 확인하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-109">When clicking a link in an application, Application Proxy tries to resolve the URL as either an internal URL within the same application, or as an externally available URL.</span></span> <span data-ttu-id="108d8-110">링크가 동일한 응용 프로그램에 속하지 않는 내부 URL을 가리키는 경우 이러한 버킷 중 하나에 속하지 않고 찾을 수 없다는 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-110">If the link points to an internal URL that is not within the same application, it does not belong to either of these buckets and result in a not found error.</span></span>

## <a name="ways-you-can-resolve-broken-links"></a><span data-ttu-id="108d8-111">끊어진 링크 문제를 해결할 수 있는 방법</span><span class="sxs-lookup"><span data-stu-id="108d8-111">Ways you can resolve broken links</span></span>

<span data-ttu-id="108d8-112">이 문제를 해결하는 방법은 세 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-112">There are three ways to resolve this issue.</span></span> <span data-ttu-id="108d8-113">아래 문제는 복잡성이 높은 순으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-113">The choices below are in listed in increasing complexity.</span></span>

1.  <span data-ttu-id="108d8-114">내부 URL이 응용 프로그램의 모든 관련 링크를 포함하는 루트인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-114">Make sure the internal URL is a root that contains all the relevant links for the application.</span></span> <span data-ttu-id="108d8-115">이렇게 하면 모든 링크를 동일한 응용 프로그램 내에 게시된 콘텐츠로 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-115">This allows all links to be resolved as content published within the same application.</span></span>

    <span data-ttu-id="108d8-116">내부 URL을 변경하지만 사용자의 방문 페이지를 변경하지 않으려는 경우 홈 페이지 URL을 이전에 게시된 내부 URL로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-116">If you change the internal URL but don’t want to change the landing page for users, change the Home page URL to the previously published internal URL.</span></span> <span data-ttu-id="108d8-117">이를 위해 "Azure Active Directory" -&gt; 앱 등록 -&gt; 응용 프로그램 선택 -&gt; 속성으로 이동하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-117">This can be done by going to “Azure Active Directory” -&gt; App Registrations -&gt; select the application -&gt; Properties.</span></span> <span data-ttu-id="108d8-118">이 속성 탭에서 원하는 방문 페이지로 조정할 수 있는 "홈 페이지 URL" 필드를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-118">In this properties tab, you see the field “Home Page URL” which you can adjust to be the desired landing page.</span></span>

2.  <span data-ttu-id="108d8-119">응용 프로그램에서 FQDN(정규화된 도메인 이름)을 사용하는 경우 [사용자 지정 도메인](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)을 사용하여 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-119">If your applications use fully qualified domain names (FQDNs), use [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) to publish your applications.</span></span> <span data-ttu-id="108d8-120">이 기능을 사용하면 동일한 URL을 내부 및 외부에서 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-120">This feature allows the same URL to be used both internally and externally.</span></span>

    <span data-ttu-id="108d8-121">내부 URL에 대한 응용 프로그램 내의 링크도 외부에서 인식하므로 이 옵션은 응용 프로그램의 링크가 응용 프로그램 프록시를 통해 외부에서 액세스될 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-121">This option ensures that the links in your application are externally accessible through Application Proxy since the links within the application to internal URLs are also recognized externally.</span></span> <span data-ttu-id="108d8-122">모든 링크가 게시된 응용 프로그램에 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-122">Note that all links still need to belong to a published application.</span></span> <span data-ttu-id="108d8-123">그러나 이 옵션을 사용하면 링크가 동일한 응용 프로그램에 속하지 않고 여러 응용 프로그램에 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-123">However, with this option the links do not need to belong to the same application and can belong to multiple applications.</span></span>

3.  <span data-ttu-id="108d8-124">이러한 옵션 중 어느 것도 쉽지 않은 경우 URL 변환/다시 작성을 수행하는 새로운 기능의 미리 보기에 조인합니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-124">If neither of these options are feasible, you join the preview for a new feature that do URL translation/rewriting.</span></span> <span data-ttu-id="108d8-125">이 옵션을 사용하여 응용 프로그램의 HTML 본문에 있는 내부 URL 또는 링크를 번역하거나 게시된 외부 앱 프록시 URL에 "매핑"합니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-125">With this option, internal URLs or links that exist in the HTML body of your applications be translated, or “mapped”, to the published external App Proxy URLs.</span></span> <span data-ttu-id="108d8-126">HTML 또는 CSS의 링크에만 작동하며 링크가 JS를 통해 생성되는 경우 도움이 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-126">This only works for links in the HTML or CSS, and this not help if your link is generated through JS.</span></span> 

<span data-ttu-id="108d8-127">결과적으로 가능하면 [사용자 지정 도메인](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) 솔루션을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-127">As a result, we strongly recommend using the [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution if possible.</span></span> <span data-ttu-id="108d8-128">미리 보기에 조인하지 않으려는 경우 applicationId를 사용하여 <aadapfeedback@microsoft.com>을 전자 메일로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="108d8-128">If you do want to join the preview, email <aadapfeedback@microsoft.com> with the applicationId(s).</span></span>

## <a name="next-steps"></a><span data-ttu-id="108d8-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="108d8-129">Next steps</span></span>
[<span data-ttu-id="108d8-130">기존 온-프레미스 프록시 서버 작업</span><span class="sxs-lookup"><span data-stu-id="108d8-130">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)

