---
title: "부하 분산을 위해 트래픽 관리자를 사용하는 Azure 앱 서비스의 사용자 지정 도메인 이름 구성"
description: "부하 분산을 위해 트래픽 관리자를 포함하는 Azure 앱 서비스의 웹 앱에 대한 사용자 지정 도메인 이름을 사용합니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 5f099201d9018a6f8577cb3daf127d09560fb94b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="d748c-103">트래픽 관리자를 사용하는 Azure 앱 서비스의 웹 앱에 대한 사용자 지정 도메인 이름 구성</span><span class="sxs-lookup"><span data-stu-id="d748c-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="d748c-104">이 문서에서는 부하 분산을 위해 트래픽 관리자를 사용하는 Azure 앱 서비스에서 사용자 지정 도메인 이름을 사용하는 일반 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="d748c-105">DNS 레코드 이해</span><span class="sxs-lookup"><span data-stu-id="d748c-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="d748c-106">표준 모드에 대해 웹 앱 구성</span><span class="sxs-lookup"><span data-stu-id="d748c-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="d748c-107">사용자 지정 도메인에 대한 DNS 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="d748c-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="d748c-108">Azure 앱 서비스 웹앱을 통해 도메인을 구입한 경우 다음 단계를 생략하고 [웹앱 도메인 구입](custom-dns-web-site-buydomains-web-app.md) 문서의 최종 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d748c-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="d748c-109">사용자 지정 도메인을 Azure 앱 서비스의 웹 앱에 연결하려면 도메인 이름을 구입한 도메인 등록 기관에서 제공하는 도구를 사용하여 DNS 테이블에 사용자 지정 도메인에 대한 새 항목을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-109">To associate your custom domain with a web app in Azure App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by the domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="d748c-110">DNS 도구를 찾아 사용하려면 다음 단계를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="d748c-110">Use the following steps to locate and use the DNS tools.</span></span>

1. <span data-ttu-id="d748c-111">도메인 등록 기관에서 계정에 로그인하고 DNS 레코드 관리에 대한 페이지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-111">Sign in to your account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="d748c-112">**도메인 이름**, **DNS** 또는 **이름 서버 관리**로 레이블이 지정된 사이트의 링크 또는 영역을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-112">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="d748c-113">종종 이 페이지에 대한 링크는 계정 정보를 확인한 다음 **내 도메인**과 같은 링크를 검색하여 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-113">Often a link to this page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="d748c-114">도메인 이름에 대한 관리 페이지를 찾았으면 DNS 레코드를 편집할 수 있는 링크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-114">Once you have found the management page for your domain name, look for a link that allows you to edit the DNS records.</span></span> <span data-ttu-id="d748c-115">이 링크는 **영역 파일**, **DNS 레코드** 또는 **고급** 구성 링크로 나열될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="d748c-116">페이지에는 '**@**' 또는 '\*'를 '도메인 파킹' 페이지에 연결하는 항목과 같은 몇 가지 레코드가 이미 만들어져 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-116">The page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="d748c-117">또한 **www**와 같은 일반 하위 도메인에 대한 레코드가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="d748c-118">페이지는 **CNAME 레코드**를 나타내거나 레코드 유형을 선택할 수 있는 드롭다운을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-118">The page will mention **CNAME records**, or provide a drop-down to select a record type.</span></span> <span data-ttu-id="d748c-119">**A records** 및 **MX 레코드**와 같은 다른 레코드를 나타낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="d748c-120">어떤 경우에는 CNAME 레코드를 **별칭 레코드**와 같은 다른 이름으로 부릅니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="d748c-121">또한 페이지에는 **호스트 이름** 또는 **도메인 이름**에서 다른 도메인 이름으로 **매핑**할 수 있는 필드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-121">The page will also have fields that allow you to **map** from a **Host name** or **Domain name** to another domain name.</span></span>
3. <span data-ttu-id="d748c-122">각 등록 기관에 대한 구체적인 설명은 다르지만 일반적으로 사용자 지정 도메인 이름(예: **contoso.com**)*에서* 웹앱에 사용하는 트래픽 관리자 도메인 이름(**contoso.trafficmanager.net**)*으로* 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-122">While the specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* the Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d748c-123">또는 레코드를 이미 사용 중이고 앱을 우선적으로 바인딩해야 하는 경우 추가 CNAME 레코드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-123">Alternatively, if a record is already in use and you need to preemptively bind your apps to it, you can create an additional CNAME record.</span></span> <span data-ttu-id="d748c-124">예를 들어 웹앱에 **www.contoso.com**을 우선적으로 바인딩하려면 **awverify.www**에서 **contoso.trafficmanager.net**으로 CNAME 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-124">For example, to preemptively bind **www.contoso.com** to your web app, create a CNAME record from **awverify.www** to **contoso.trafficmanager.net**.</span></span> <span data-ttu-id="d748c-125">그런 다음 "www" CNAME 레코드를 변경하지 않고 "www.contoso.com"을 웹앱에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-125">You can then add "www.contoso.com" to your Web App without changing the "www" CNAME record.</span></span> <span data-ttu-id="d748c-126">자세한 내용은 [사용자 지정 도메인에서 웹앱에 대한 DNS 레코드 만들기][CREATEDNS]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d748c-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="d748c-127">등록 기관에서 DNS 레코드를 추가하거나 수정했으면 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d748c-127">Once you have finished adding or modifying DNS records at your registrar, save the changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="d748c-128">트래픽 관리자 사용</span><span class="sxs-lookup"><span data-stu-id="d748c-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="d748c-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d748c-129">Next steps</span></span>
<span data-ttu-id="d748c-130">자세한 내용은 [Node.js 개발자 센터](/develop/nodejs/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d748c-130">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
