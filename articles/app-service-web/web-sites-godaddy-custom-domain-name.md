---
title: "Azure 앱 서비스 (GoDaddy)의 사용자 지정 도메인 이름 aaaConfigure"
description: "GoDaddy 및 Azure 웹 앱에서에서 toouse 도메인 이름을 하는 방법에 대해 알아봅니다"
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="b4cf7-103">GoDaddy에서 직접 구입한 Azure 앱 서비스에서 사용자 지정 도메인 이름 구성</span><span class="sxs-lookup"><span data-stu-id="b4cf7-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="b4cf7-104">Azure 앱 서비스 웹 앱을 통해 도메인을 구입한 다음 toohello의 마지막 단계를 참조 하면 [는 웹 응용 프로그램 도메인을 구입](custom-dns-web-site-buydomains-web-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-104">If you have purchased domain through Azure App Service Web Apps then refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="b4cf7-105">이 문서에서는 [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)를 사용하여 [GoDaddy](https://godaddy.com)에서 직접 구매한 사용자 지정 도메인 이름 사용에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="b4cf7-106">DNS 레코드 이해</span><span class="sxs-lookup"><span data-stu-id="b4cf7-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="b4cf7-107">사용자 지정 도메인에 대한 DNS 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="b4cf7-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="b4cf7-108">tooassociate 앱 서비스에서 웹 앱과 사용자 지정 도메인을 추가 해야 새 항목 hello DNS 테이블의 사용자 지정 도메인에 대 한 GoDaddy에서 제공 하는 도구를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-108">tooassociate your custom domain with a web app in App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="b4cf7-109">단계 toolocate hello DNS 도구 GoDaddy.com에 대 한 다음 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b4cf7-109">Use hello following steps toolocate hello DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="b4cf7-110">GoDaddy.com 가진 tooyour 계정에 로그인 하 고 선택 **내 계정** 차례로 **내 도메인 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-110">Log on tooyour account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="b4cf7-111">Azure 웹 앱과 함께 toouse 원하는 선택 하는 hello 도메인 이름에 대 한 선택 hello 드롭 다운 메뉴 **DNS 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-111">Select hello drop-down menu for hello domain name that you wish toouse with your Azure web app and select **Manage DNS**.</span></span>
   
    ![GoDaddy의 사용자 지정 도메인 페이지](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="b4cf7-113">Hello에서 **도메인 세부 정보** 페이지, toohello 스크롤하여 **DNS 영역 파일** 탭 합니다. 추가 하 고 도메인 이름에 대 한 DNS 레코드를 수정에 사용 되는 hello 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-113">From hello **Domain details** page, scroll toohello **DNS Zone File** tab. This is hello section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![DNS Zone File 탭](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="b4cf7-115">선택 **레코드 추가** tooadd 기존 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-115">Select **Add Record** tooadd an existing record.</span></span>
   
    <span data-ttu-id="b4cf7-116">너무**편집** 기존 레코드, hello 레코드 옆에 있는 select hello 펜 및 용지 아이콘입니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-116">too**edit** an existing record, select hello pen & paper icon beside hello record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b4cf7-117">새 레코드를 추가하기 전에 GoDaddy에서 많이 사용되는 하위 도메인에 대한 DNS 레코드(편집기에서 **Host**)(예: **email**, **files**, **mail** 등)를 이미 만든 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-117">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="b4cf7-118">Hello 이름 toouse 이미 있으면 hello 새로 만드는 대신 기존 레코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-118">If hello name you wish toouse already exists, modify hello existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="b4cf7-119">레코드를 추가할 때 먼저 hello 레코드 종류를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-119">When adding a record, you must first select hello record type.</span></span>
   
    ![레코드 유형 선택](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="b4cf7-121">다음으로 hello를 입력 해야 **호스트** (사용자 지정 도메인 또는 하위 도메인 hello) 및 어떤 it **가리키는**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-121">Next, you must provide hello **Host** (hello custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![영역 레코드 추가](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="b4cf7-123">추가 하는 경우는 **A (호스트) 레코드** -hello를 설정 해야 **호스트** 필드 tooeither  **@**  (이 루트 도메인 이름 같은 나타냅니다  **contoso.com**,) * (여러 하위 도메인을 일치 하는 와일드 카드) 또는 toouse 원하는 hello 하위 도메인 (예를 들어 **www**.) Hello를 설정 해야 **가리키는** Azure 웹 앱의 toohello IP 주소 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-123">When adding an **A (host) record** - you must set hello **Host** field tooeither **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or hello sub-domain you wish toouse (for example, **www**.) You must set hello **Points to** field toohello IP address of your Azure web app.</span></span>
   * <span data-ttu-id="b4cf7-124">추가 하는 경우는 **CNAME (별칭) 레코드** -hello를 설정 해야 **호스트** toouse 원하는 필드 toohello 하위 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-124">When adding a **CNAME (alias) record** - you must set hello **Host** field toohello sub-domain you wish toouse.</span></span> <span data-ttu-id="b4cf7-125">예를 들면 **www**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-125">For example, **www**.</span></span> <span data-ttu-id="b4cf7-126">Hello를 설정 해야 **가리키는** 필드 toohello **. azurewebsites.net** Azure 웹 앱의 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-126">You must set hello **Points to** field toohello **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="b4cf7-127">예를 들어 **contoso.azurewebsites.net**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-127">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="b4cf7-128">**다른 항목 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-128">Click **Add Another**.</span></span>
5. <span data-ttu-id="b4cf7-129">선택 **TXT** hello 레코드 유형으로 지정는 **호스트** 값  **@**  및 **가리키는** 값  **&lt;yourwebappname&gt;. azurewebsites.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-129">Select **TXT** as hello record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b4cf7-130">이 TXT 레코드는 레코드 또는 hello 첫 번째 TXT 레코드 hello에 설명 된 hello 도메인의 소유를 Azure toovalidate에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-130">This TXT record is used by Azure toovalidate that you own hello domain described by hello A record or hello first TXT record.</span></span> <span data-ttu-id="b4cf7-131">Hello 도메인에 대 한 hello Azure 포털의에서 웹 앱 매핑된 toohello를 수행한 후에이 TXT 레코드 항목을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-131">Once hello domain has been mapped toohello web app in hello Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="b4cf7-132">추가 완료 하거나 클릭 하 여 레코드를 수정 **마침** toosave 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-132">When you have finished adding or modifying records, click **Finish** toosave changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a><span data-ttu-id="b4cf7-133">웹 앱에서 hello 도메인 이름을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="b4cf7-133">Enable hello domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="b4cf7-134">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-134">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b4cf7-135">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4cf7-135">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="b4cf7-136">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="b4cf7-136">What's changed</span></span>
* <span data-ttu-id="b4cf7-137">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b4cf7-137">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

