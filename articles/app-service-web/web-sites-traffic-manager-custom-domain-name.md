---
title: "Azure 앱 서비스 부하 분산에 대 한 트래픽 관리자를 사용 하는 웹 앱에 대 한 사용자 지정 도메인 이름 aaaConfigure 합니다."
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
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="f283c-103">트래픽 관리자를 사용하는 Azure 앱 서비스의 웹 앱에 대한 사용자 지정 도메인 이름 구성</span><span class="sxs-lookup"><span data-stu-id="f283c-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="f283c-104">이 문서에서는 부하 분산을 위해 트래픽 관리자를 사용하는 Azure 앱 서비스에서 사용자 지정 도메인 이름을 사용하는 일반 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="f283c-105">DNS 레코드 이해</span><span class="sxs-lookup"><span data-stu-id="f283c-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="f283c-106">표준 모드에 대해 웹 앱 구성</span><span class="sxs-lookup"><span data-stu-id="f283c-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="f283c-107">사용자 지정 도메인에 대한 DNS 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="f283c-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="f283c-108">Azure 앱 서비스 웹 앱을 통해 도메인을 구입한 한 후 다음 단계를 건너뛰고 있습니다 toohello의 마지막 단계를 참조 하는 경우 [는 웹 응용 프로그램 도메인을 구입](custom-dns-web-site-buydomains-web-app.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="f283c-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="f283c-109">tooassociate Azure 앱 서비스의 웹 앱과 사용자 지정 도메인을 추가 해야 새 항목 hello DNS 테이블의 사용자 지정 도메인에 대 한 hello 도메인 등록자에서 도메인 이름을 구매한에서 제공 하는 도구를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-109">tooassociate your custom domain with a web app in Azure App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by hello domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="f283c-110">다음 단계 toolocate hello를 사용 하 여 및 hello DNS 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-110">Use hello following steps toolocate and use hello DNS tools.</span></span>

1. <span data-ttu-id="f283c-111">도메인 등록자에 tooyour 계정에 로그인 하 고 DNS 레코드를 관리 하기 위한 페이지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-111">Sign in tooyour account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="f283c-112">링크 검색 또는 hello 사이트의 영역으로 표시 **도메인 이름**, **DNS**, 또는 **이름 서버 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-112">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="f283c-113">링크 toothis 페이지를 찾을 수 있습니다 수 계정 정보를 보고 하 고 다음 링크를와 같은 찾고 종종 **내 도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-113">Often a link toothis page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="f283c-114">도메인 이름에 대 한 hello 관리 페이지를 발견 하면 tooedit hello DNS 레코드를 허용 하는 링크를 찾아보십시오.</span><span class="sxs-lookup"><span data-stu-id="f283c-114">Once you have found hello management page for your domain name, look for a link that allows you tooedit hello DNS records.</span></span> <span data-ttu-id="f283c-115">이 링크는 **영역 파일**, **DNS 레코드** 또는 **고급** 구성 링크로 나열될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="f283c-116">hello 페이지의 레코드를 연결 하는 항목 등 이미 만든는 것 '**@**'또는'\*' '도메인 주차' 페이지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-116">hello page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="f283c-117">또한 **www**와 같은 일반 하위 도메인에 대한 레코드가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="f283c-118">hello 페이지 언급 **CNAME 레코드**, 드롭 다운 tooselect 레코드 종류를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-118">hello page will mention **CNAME records**, or provide a drop-down tooselect a record type.</span></span> <span data-ttu-id="f283c-119">**A records** 및 **MX 레코드**와 같은 다른 레코드를 나타낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="f283c-120">어떤 경우에는 CNAME 레코드를 **별칭 레코드**와 같은 다른 이름으로 부릅니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="f283c-121">hello 페이지에는 너무 사용 하는 필드**지도** 에서 **호스트 이름** 또는 **도메인 이름** tooanother 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-121">hello page will also have fields that allow you too**map** from a **Host name** or **Domain name** tooanother domain name.</span></span>
3. <span data-ttu-id="f283c-122">각 등록자의 hello 세부 사항 다 일반적 상태에 매핑해야 *에서* 사용자 지정 도메인 이름 (같은 **contoso.com**,) *를* hello 트래픽 관리자 도메인 이름 (**contoso.trafficmanager.net**) 웹 앱에 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-122">While hello specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* hello Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f283c-123">또는 앱 tooit 바인딩할 toopreemptively를 해야 하는 레코드는 이미 사용 중인 경우는 추가 CNAME 레코드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-123">Alternatively, if a record is already in use and you need toopreemptively bind your apps tooit, you can create an additional CNAME record.</span></span> <span data-ttu-id="f283c-124">예를 들어 toopreemptively 바인딩 **www.contoso.com** tooyour 웹 응용 프로그램에서 CNAME 레코드를 만들 **awverify.www** 너무**contoso.trafficmanager.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-124">For example, toopreemptively bind **www.contoso.com** tooyour web app, create a CNAME record from **awverify.www** too**contoso.trafficmanager.net**.</span></span> <span data-ttu-id="f283c-125">그런 다음 hello "www" CNAME 레코드를 변경 하지 않고 "www.contoso.com" tooyour 웹 앱을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-125">You can then add "www.contoso.com" tooyour Web App without changing hello "www" CNAME record.</span></span> <span data-ttu-id="f283c-126">자세한 내용은 [사용자 지정 도메인에서 웹앱에 대한 DNS 레코드 만들기][CREATEDNS]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f283c-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="f283c-127">등록자에서 DNS 레코드를 수정 또는 추가 완료 되 면 hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-127">Once you have finished adding or modifying DNS records at your registrar, save hello changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="f283c-128">트래픽 관리자 사용</span><span class="sxs-lookup"><span data-stu-id="f283c-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="f283c-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f283c-129">Next steps</span></span>
<span data-ttu-id="f283c-130">자세한 내용은 참조 hello [Node.js 개발자 센터](/develop/nodejs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="f283c-130">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
