---
title: "Azure 앱 서비스에 대한 사용자 지정 도메인 이름 구성(GoDaddy)"
description: "Azure 웹 앱에서 GoDaddy의 도메인 이름을 사용하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 158c5dc06f83e16633d3c2fbb4eb27d3e8af030c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="688c3-103">GoDaddy에서 직접 구입한 Azure 앱 서비스에서 사용자 지정 도메인 이름 구성</span><span class="sxs-lookup"><span data-stu-id="688c3-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="688c3-104">Azure 앱 서비스 웹앱을 통해 도메인을 구입한 경우 [웹앱 도메인 구입](custom-dns-web-site-buydomains-web-app.md)의 최종 단계를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="688c3-104">If you have purchased domain through Azure App Service Web Apps then refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="688c3-105">이 문서에서는 [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714)를 사용하여 [GoDaddy](https://godaddy.com)에서 직접 구매한 사용자 지정 도메인 이름 사용에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="688c3-106">DNS 레코드 이해</span><span class="sxs-lookup"><span data-stu-id="688c3-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="688c3-107">사용자 지정 도메인에 대한 DNS 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="688c3-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="688c3-108">사용자 지정 도메인과 앱 서비스의 웹 앱을 연결하려면 GoDaddy에서 제공하는 도구를 사용하여 DNS 테이블에서 사용자 지정 도메인에 대한 새 항목을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-108">To associate your custom domain with a web app in App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="688c3-109">GoDaddy.comy용 DNS 도구를 찾으려면 다음 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="688c3-109">Use the following steps to locate the DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="688c3-110">사용 중인 계정으로 GoDaddy.com에 로그인하고 **My Account**를 클릭한 후 **Manage my domains**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-110">Log on to your account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="688c3-111">Azure 웹앱에서 사용할 도메인 이름에 대한 드롭다운 메뉴를 선택한 후 **DNS 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-111">Select the drop-down menu for the domain name that you wish to use with your Azure web app and select **Manage DNS**.</span></span>
   
    ![GoDaddy의 사용자 지정 도메인 페이지](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="688c3-113">**Domain details** 페이지에서 **DNS Zone File** 탭으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-113">From the **Domain details** page, scroll to the **DNS Zone File** tab.</span></span> <span data-ttu-id="688c3-114">이는 도메인 이름의 DNS 레코드를 추가 및 수정할 때 사용한 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-114">This is the section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![DNS Zone File 탭](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="688c3-116">**Add Record** 를 선택하여 기존 레코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-116">Select **Add Record** to add an existing record.</span></span>
   
    <span data-ttu-id="688c3-117">기존 레코드를 **편집**하려면 해당 레코드 옆의 펜과 종이 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-117">To **edit** an existing record, select the pen & paper icon beside the record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="688c3-118">새 레코드를 추가하기 전에 GoDaddy에서 많이 사용되는 하위 도메인에 대한 DNS 레코드(편집기에서 **Host**)(예: **email**, **files**, **mail** 등)를 이미 만든 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-118">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="688c3-119">사용하려는 이름이 이미 있는 경우 새로 만들지 않고 기존 레코드를 수정하십시오.</span><span class="sxs-lookup"><span data-stu-id="688c3-119">If the name you wish to use already exists, modify the existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="688c3-120">레코드를 추가할 때 먼저 레코드 유형을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-120">When adding a record, you must first select the record type.</span></span>
   
    ![레코드 유형 선택](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="688c3-122">그런 다음 **Host**(사용자 지정 도메인 또는 하위 도메인) 및 해당 호스트의 **Points to** 항목을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-122">Next, you must provide the **Host** (the custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![영역 레코드 추가](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="688c3-124">**A (host) record**를 추가할 때 **Host** 필드를 **@**(**contoso.com**과 같은 루트 도메인 이름을 나타냄) * (모든 하위 도메인을 나타내는 와일드카드) 또는 사용할 하위 도메인(예: **www**)으로 설정해야 합니다. **Points to** 필드를 Azure 웹앱의 IP 주소로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-124">When adding an **A (host) record** - you must set the **Host** field to either **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or the sub-domain you wish to use (for example, **www**.) You must set the **Points to** field to the IP address of your Azure web app.</span></span>
   * <span data-ttu-id="688c3-125">**CNAME (alias) record**를 추가할 때 **Host** 필드를, 사용할 하위 도메인으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-125">When adding a **CNAME (alias) record** - you must set the **Host** field to the sub-domain you wish to use.</span></span> <span data-ttu-id="688c3-126">예를 들면 **www**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-126">For example, **www**.</span></span> <span data-ttu-id="688c3-127">**Points to** 필드는 Azure 웹 앱의 **.azurewebsites.net** 도메인 이름으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-127">You must set the **Points to** field to the **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="688c3-128">예를 들어 **contoso.azurewebsites.net**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-128">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="688c3-129">**다른 항목 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-129">Click **Add Another**.</span></span>
5. <span data-ttu-id="688c3-130">레코드 유형으로 **TXT**를 선택한 다음 **@**의 **호스트** 값 및 **&lt;yourwebappname&gt;.azurewebsites.net**의 **Points to** 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-130">Select **TXT** as the record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="688c3-131">이 TXT 레코드는 Azure에서 A 레코드 또는 첫 번째 TXT 레코드가 설명하는 도메인을 개발자가 소유하고 있는지 확인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-131">This TXT record is used by Azure to validate that you own the domain described by the A record or the first TXT record.</span></span> <span data-ttu-id="688c3-132">도메인이 Azure 포털에서 웹앱으로 매핑되면 이 TXT 레코드 항목을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-132">Once the domain has been mapped to the web app in the Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="688c3-133">레코드 추가 또는 수정을 완료하면 **Finish** 를 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-133">When you have finished adding or modifying records, click **Finish** to save changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-the-domain-name-on-your-web-app"></a><span data-ttu-id="688c3-134">웹 앱에서 도메인 이름 사용</span><span class="sxs-lookup"><span data-stu-id="688c3-134">Enable the domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="688c3-135">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. App Service에서 단기 스타터 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-135">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="688c3-136">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="688c3-136">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="688c3-137">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="688c3-137">What's changed</span></span>
* <span data-ttu-id="688c3-138">웹 사이트에서 앱 서비스로의 변경에 대한 지침은 [Azure App Service와 이 서비스가 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="688c3-138">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

