---
title: "응용 프로그램 페이지가 응용 프로그램 프록시 응용 프로그램에 올바르게 표시되지 않음 | Microsoft Docs"
description: "페이지에서 Azure AD와 통합한 응용 프로그램 프록시 응용 프로그램을 제대로 표시하지 않는 경우 가이드입니다."
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
ms.openlocfilehash: cac4c333e59ef9a0f28a2f93a7afee22eeafd54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="8d0a6-103">응용 프로그램 페이지가 응용 프로그램 프록시 응용 프로그램에 올바르게 표시되지 않음</span><span class="sxs-lookup"><span data-stu-id="8d0a6-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="8d0a6-104">이 문서를 통해 페이지로 이동하지만 페이지가 올바르게 표시하지 않는 경우 Azure Active Directory 응용 프로그램 프록시 응용 프로그램의 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0a6-104">This article help you to troubleshoot issues with Azure Active Directory Application Proxy applications when you navigate to the page, but something on the page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="8d0a6-105">개요</span><span class="sxs-lookup"><span data-stu-id="8d0a6-105">Overview</span></span>
<span data-ttu-id="8d0a6-106">응용 프로그램 프록시 앱을 게시하면 응용 프로그램에 액세스할 때 루트의 페이지에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0a6-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing the application.</span></span> <span data-ttu-id="8d0a6-107">페이지에 올바르게 표시되지 않으면 응용 프로그램에 사용되는 루트 내부 URL에는 일부 페이지 리소스가 누락될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0a6-107">If the page isn’t displaying correctly, the root internal URL used for the application may be missing some page resources.</span></span> <span data-ttu-id="8d0a6-108">이 문제를 해결하려면 페이지의 *모든* 리소스를 응용 프로그램의 일부분으로 게시했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0a6-108">To resolve, make sure you have published *all* the resources for the page as part of your application.</span></span>

<span data-ttu-id="8d0a6-109">네트워크 추적기를 열고, 페이지를 로드하고, 404 오류를 찾아서 문제를 확인할 수 있습니다(예: Internet Explorer/Edge의 Fiddler 또는 F12 도구).</span><span class="sxs-lookup"><span data-stu-id="8d0a6-109">You can verify this is the issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading the page, and looking for 404 errors.</span></span> <span data-ttu-id="8d0a6-110">현재 찾을 수 없고 게시해야 하는 페이지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8d0a6-110">That indicates the pages that currently cannot be found and may still need to be published.</span></span>

<span data-ttu-id="8d0a6-111">이 경우에 예를 들어 <http://myapps/expenses>라는 내부 URL을 사용하여 비용 응용 프로그램을 게시했지만 앱에서 <http://myapps/style.css> 스타일 시트를 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0a6-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but the app uses the stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="8d0a6-112">이 경우에 비용 앱을 로드하면 style.css를 로드하는 동안 404 오류를 throw하므로 스타일 시트는 응용 프로그램에서 게시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0a6-112">In this case, the stylesheet is not published in your application, so loading the expenses app throw a 404 error while trying to load style.css.</span></span> <span data-ttu-id="8d0a6-113">이 예제에서는 대신 <http://myapp/>이라는 내부 URL을 사용하여 응용 프로그램을 게시하여 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0a6-113">In this example, the problem would be resolved by publishing the application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="8d0a6-114">하나의 응용 프로그램으로 게시하는 문제</span><span class="sxs-lookup"><span data-stu-id="8d0a6-114">Problems with publishing as one application</span></span>

<span data-ttu-id="8d0a6-115">동일한 응용 프로그램 내에서 모든 리소스를 게시할 수 없는 경우 여러 응용 프로그램을 게시하고 이들 간의 링크를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0a6-115">If it is not possible to publish all resources within the same application, you need to publish multiple applications and enable links between them.</span></span>

<span data-ttu-id="8d0a6-116">이렇게 하려면 [사용자 지정 도메인](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) 솔루션을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8d0a6-116">To do so, we recommend using the [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="8d0a6-117">그러나 이 솔루션에서 사용자는 도메인의 인증서를 소유하고 응용 프로그램은 FQDN(정규화된 도메인 이름)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d0a6-117">However, this solution requires that you own the certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="8d0a6-118">다른 옵션은 [끊어진 링크 문제 해결 설명서](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d0a6-118">For other options, see the [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d0a6-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8d0a6-119">Next steps</span></span>
[<span data-ttu-id="8d0a6-120">Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="8d0a6-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
