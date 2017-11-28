---
title: "응용 프로그램 프록시 응용 프로그램에 대 한 aaaApplication 페이지가 제대로 표시 되지 않으면 | Microsoft Docs"
description: "Azure AD와 통합 한 hello 페이지 응용 프로그램 프록시 응용 프로그램에서 제대로 표시 되지 않습니다 때 지침"
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
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="04c83-103">응용 프로그램 페이지가 응용 프로그램 프록시 응용 프로그램에 올바르게 표시되지 않음</span><span class="sxs-lookup"><span data-stu-id="04c83-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="04c83-104">이 문서가 도움이 되었나요 Azure Active Directory 응용 프로그램 프록시 응용 프로그램과 tootroubleshoot 문제 toohello 페이지를 이동 하지만 내용 hello 페이지에 올바르게 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04c83-104">This article help you tootroubleshoot issues with Azure Active Directory Application Proxy applications when you navigate toohello page, but something on hello page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="04c83-105">개요</span><span class="sxs-lookup"><span data-stu-id="04c83-105">Overview</span></span>
<span data-ttu-id="04c83-106">응용 프로그램 프록시 응용 프로그램을 게시할 때는 hello 응용 프로그램에 액세스할 때 루트 아래에 페이지는 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c83-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing hello application.</span></span> <span data-ttu-id="04c83-107">Hello 페이지가 올바르게 표시 되지 않습니다, hello 루트 내부 URL hello 응용 프로그램에 사용 되는 일부 페이지 리소스 누락 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c83-107">If hello page isn’t displaying correctly, hello root internal URL used for hello application may be missing some page resources.</span></span> <span data-ttu-id="04c83-108">tooresolve, 게시 되었는지 확인 *모든* hello 페이지에 대 한 리소스를 응용 프로그램의 일부로 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c83-108">tooresolve, make sure you have published *all* hello resources for hello page as part of your application.</span></span>

<span data-ttu-id="04c83-109">네트워크 추적을 열어이 hello 문제를 확인할 수 있습니다 (F12 또는 Fiddler와 같은 도구 Internet Explorer/Edge) hello 페이지를 로드 하 고 404 오류 찾고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04c83-109">You can verify this is hello issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading hello page, and looking for 404 errors.</span></span> <span data-ttu-id="04c83-110">현재 찾을 수 없습니다 및 게시 toobe 다시 열어야 하는 hello 페이지를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="04c83-110">That indicates hello pages that currently cannot be found and may still need toobe published.</span></span>

<span data-ttu-id="04c83-111">이 경우의 예로 비용에 따른 응용 프로그램의 내부 URL을 사용 하 여 게시를 가정해 <http://myapps/expenses>, 하지만 hello 앱 hello 스타일 시트를 사용 하 여 <http://myapps/style.css>합니다.</span><span class="sxs-lookup"><span data-stu-id="04c83-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but hello app uses hello stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="04c83-112">이 경우 hello 스타일 시트 동안 tooload style.css 동안 404 오류를 throw hello 비용에 따른 응용 프로그램을 로드 하므로 응용 프로그램에서 게시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04c83-112">In this case, hello stylesheet is not published in your application, so loading hello expenses app throw a 404 error while trying tooload style.css.</span></span> <span data-ttu-id="04c83-113">이 예제에서는 hello 문제를 해결 hello 응용 프로그램의 내부 url을 게시 하 여 <http://myapp/> 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c83-113">In this example, hello problem would be resolved by publishing hello application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="04c83-114">하나의 응용 프로그램으로 게시하는 문제</span><span class="sxs-lookup"><span data-stu-id="04c83-114">Problems with publishing as one application</span></span>

<span data-ttu-id="04c83-115">가능한 toopublish 없으면 내의 모든 리소스 hello 동일한 응용 프로그램, 여러 응용 프로그램이 toopublish 필요 하 고 간의 링크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c83-115">If it is not possible toopublish all resources within hello same application, you need toopublish multiple applications and enable links between them.</span></span>

<span data-ttu-id="04c83-116">toodo 것이 좋습니다 hello를 사용 하 여 [사용자 지정 도메인](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="04c83-116">toodo so, we recommend using hello [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="04c83-117">그러나이 솔루션에는 도메인에 대 한 hello 인증서를 소유 하 고 응용 프로그램 정규화 된 도메인 이름 (Fqdn)을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04c83-117">However, this solution requires that you own hello certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="04c83-118">다른 옵션에 대 한 참조 hello [끊어진된 링크 설명서 문제를 해결](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1)합니다.</span><span class="sxs-lookup"><span data-stu-id="04c83-118">For other options, see hello [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04c83-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04c83-119">Next steps</span></span>
[<span data-ttu-id="04c83-120">Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="04c83-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
