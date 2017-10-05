---
title: "클라우드 서비스에서 사용자 지정 도메인 이름 구성| Microsoft Docs"
description: "DNS 설정을 구성하여 사용자 지정 도메인에서 Azure 응용 프로그램이나 도메인을 표시하는 방법을 알아봅니다."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 6a62c2b7-ea47-4cce-9d6a-0cca38357f42
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 9f872fd5119042945356225a80331da18f3a6d99
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="b25da-103">Azure 클라우드 서비스에 대한 사용자 지정 도메인 이름 구성</span><span class="sxs-lookup"><span data-stu-id="b25da-103">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b25da-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="b25da-104">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="b25da-105">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="b25da-105">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="b25da-106">클라우드 서비스를 만들면 Azure에서 cloudapp.net의 하위 도메인에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-106">When you create a Cloud Service, Azure assigns it to a subdomain of cloudapp.net.</span></span> <span data-ttu-id="b25da-107">예를 들어 클라우드 서비스의 이름이 "contoso"인 경우 사용자가 http://contoso.cloudapp.net과 같은 URL에서 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-107">For example, if your Cloud Service is named "contoso", your users will be able to access your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="b25da-108">Azure는 가상 IP 주소도 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-108">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="b25da-109">그러나 contoso.com 등의 고유한 도메인 이름에도 응용 프로그램을 표시할 수 있습니다. 이 문서에서는 클라우드 서비스 웹 역할에 대해 사용자 지정 도메인 이름을 예약 또는 구성하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-109">However, you can also expose your application on your own domain name, such as contoso.com. This article explains how to reserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="b25da-110">CNAME 및 A 레코드가 무엇인지 이미 알고 있나요?</span><span class="sxs-lookup"><span data-stu-id="b25da-110">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="b25da-111">[설명을 건너뛰고 이동하세요](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="b25da-111">[Jump past the explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="b25da-112">작업을 보다 빠르게 수행하려면</span><span class="sxs-lookup"><span data-stu-id="b25da-112">Get going faster!</span></span> <span data-ttu-id="b25da-113">Azure [안내 방식 연습](http://support.microsoft.com/kb/2990804)을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="b25da-113">Use the Azure [guided walkthrough](http://support.microsoft.com/kb/2990804).</span></span> <span data-ttu-id="b25da-114">이 연습을 통해 사용자 지정 도메인 이름을 연결하고 SSL을 사용하여 Azure 클라우드 서비스 또는 Azure 웹 사이트와의 통신을 보호하는 등의 작업을 매우 쉽게 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-114">It makes associating a custom domain name and securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

<p/>

> [!NOTE]
> <span data-ttu-id="b25da-115">이 작업의 절차는 Azure 클라우드 서비스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-115">The procedures in this task apply to Azure Cloud Services.</span></span> <span data-ttu-id="b25da-116">앱 서비스의 경우 [이것](../app-service-web/web-sites-custom-domain-name.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b25da-116">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="b25da-117">저장소 계정의 경우 [이것](../storage/blobs/storage-custom-domain-name.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b25da-117">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="b25da-118">CNAME 및 A 레코드 이해</span><span class="sxs-lookup"><span data-stu-id="b25da-118">Understand CNAME and A records</span></span>
<span data-ttu-id="b25da-119">CNAME(또는 별칭 레코드) 및 A 레코드는 둘 다 도메인 이름을 특정 서버(또는 이 경우 서비스)에 연결할 수 있게 해 주지만 다르게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-119">CNAME (or alias records) and A records both allow you to associate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="b25da-120">Azure 클라우드 서비스와 함께 A 레코드를 사용하는 경우의 몇 가지 특정 고려 사항도 있으며, 사용할 레코드를 결정하기 전에 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which to use.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="b25da-121">CNAME 또는 별칭 레코드</span><span class="sxs-lookup"><span data-stu-id="b25da-121">CNAME or Alias record</span></span>
<span data-ttu-id="b25da-122">CNAME 레코드는 *contoso.com* , **contoso.com** or **특정**도메인을 정식 도메인 이름에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, to a canonical domain name.</span></span> <span data-ttu-id="b25da-123">이 경우 정식 도메인 이름은 Azure 호스티드 응용 프로그램의 **[myapp].cloudapp.net** 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-123">In this case, the canonical domain name is the **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="b25da-124">CNAME을 만들면 **[myapp].cloudapp.net**에 대한 별칭이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-124">Once created, the CNAME creates an alias for the **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="b25da-125">CNAME 항목은 자동으로 **[myapp].cloudapp.net** 서비스의 IP 주소로 확인되기 때문에 클라우드 서비스의 IP 주소가 변경될 경우 아무 조치도 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-125">The CNAME entry will resolve to the IP address of your **[myapp].cloudapp.net** service automatically, so if the IP address of the cloud service changes, you do not have to take any action.</span></span>

> [!NOTE]
> <span data-ttu-id="b25da-126">www.contoso.com과 같은 CNAME 레코드를 사용하고 contoso.com과 같은 비루트 이름을 사용하면 일부 도메인 등록 기관에서 하위 도메인만 매핑할 수 있습니다. CNAME 레코드에 대한 자세한 내용은 등록 기관에서 제공하는 설명서인 [CNAME 레코드에 대한 Wikipedia 항목](http://en.wikipedia.org/wiki/CNAME_record) 또는 [IETF 도메인 이름 - 구현 및 사양](http://tools.ietf.org/html/rfc1035) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b25da-126">Some domain registrars only allow you to map subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see the documentation provided by your registrar, [the Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or the [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="b25da-127">A 레코드</span><span class="sxs-lookup"><span data-stu-id="b25da-127">A record</span></span>
<span data-ttu-id="b25da-128">A 레코드는 **contoso.com**, **www.contoso.com** 등의 도메인이나 **\*.contoso.com** 등의 *와일드카드 도메인*을 IP 주소에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-128">An A record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, to an IP address.</span></span> <span data-ttu-id="b25da-129">Azure 클라우드 서비스의 경우 서비스의 가상 IP입니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-129">In the case of an Azure Cloud Service, the virtual IP of the service.</span></span> <span data-ttu-id="b25da-130">따라서 A 레코드가 CNAME 레코드보다 나은 주요 장점은 \***.contoso.com**과 같이 와일드카드를 사용하는 항목을 사용할 수 있다는 것입니다. 이러한 항목은 **mail.contoso.com**, **login.contoso.com** 또는 **www.contso.com** 등의 여러 하위 도메인에 대한 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-130">So the main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="b25da-131">A 레코드는 고정 IP 주소에 매핑되므로 변경 내용을 클라우드 서비스의 IP 주소로 자동으로 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-131">Since an A record is mapped to a static IP address, it cannot automatically resolve changes to the IP address of your Cloud Service.</span></span> <span data-ttu-id="b25da-132">빈 슬롯(프로덕션 또는 스테이징)에 처음 배포할 때 클라우드 서비스에서 사용되는 IP 주소가 할당됩니다. 슬롯에 대한 배포를 삭제하면 Azure에서 IP 주소를 해제하며, 나중에 슬롯에 배포할 때 새 IP 주소가 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-132">The IP address used by your Cloud Service is allocated the first time you deploy to an empty slot (either production or staging.) If you delete the deployment for the slot, the IP address is released by Azure and any future deployments to the slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="b25da-133">편의상, 스테이징 배포와 프로덕션 배포 간에 전환하거나 기존 배포의 바로 업그레이드를 수행하는 경우 주어진 배포 슬롯(프로덕션 또는 스테이징)의 IP 주소가 지속됩니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-133">Conveniently, the IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="b25da-134">이러한 작업을 수행하는 방법에 대한 자세한 내용은 [클라우드 서비스를 관리하는 방법](cloud-services-how-to-manage.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b25da-134">For more information on performing these actions, see [How to manage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="b25da-135">사용자 지정 도메인에 대한 CNAME 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="b25da-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="b25da-136">CNAME 레코드를 만들려면 등록 기관에서 제공한 도구를 사용하여 사용자 지정 도메인에 대한 새 항목을 DNS 테이블에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-136">To create a CNAME record, you must add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="b25da-137">각 등록 기관은 서로 유사하지만 약간 다른 방법으로 CNAME 레코드를 지정하지만 개념은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concepts are the same.</span></span>

1. <span data-ttu-id="b25da-138">이러한 방법 중 하나를 사용하여 클라우드 서비스에 할당된 **.cloudapp.net** 도메인 이름을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-138">Use one of these methods to find the **.cloudapp.net** domain name assigned to your cloud service.</span></span>
   
   * <span data-ttu-id="b25da-139">[Azure 클래식 포털]에 로그인하고 클라우드 서비스를 선택한 다음 **대시보드**를 선택한 다음 **간략 상태** 섹션에서 **사이트 URL** 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-139">Login to the [Azure classic portal], select your cloud service, select **Dashboard**, and then find the **Site URL** entry in the **quick glance** section.</span></span>
     
       ![사이트 URL을 표시하는 한눈에 보기 섹션][csurl]
     
       <span data-ttu-id="b25da-141">**또는**</span><span class="sxs-lookup"><span data-stu-id="b25da-141">**OR**</span></span>  
   * <span data-ttu-id="b25da-142">[Azure Powershell](/powershell/azure/overview)을 설치 및 구성하고 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="b25da-143">CNAME 레코드를 만들 때 필요하므로 두 방법 중 하나에서 반환된 URL에 사용된 도메인 이름을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-143">Save the domain name used in the URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="b25da-144">DNS 등록 기관의 웹 사이트에 로그온한 다음 DNS 관리 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-144">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="b25da-145">**도메인 이름**, **DNS** 또는 **이름 서버 관리**로 레이블이 지정된 사이트의 링크 또는 영역을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-145">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="b25da-146">이제 CNAME을 선택하거나 입력할 수 있는 위치를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="b25da-147">드롭다운에서 레코드 유형을 선택하거나 고급 설정 페이지로 이동해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-147">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span> <span data-ttu-id="b25da-148">**CNAME**, **별칭** 또는 **하위 도메인**과 같은 단어를 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-148">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="b25da-149">**www.customdomain.com**에 대한 별칭을 만들려는 경우 **www**와 같은 CNAME에 대한 도메인 또는 하위 도메인 별칭도 제공해야 합니다. 루트 도메인에 대한 별칭을 만들려는 경우 등록 기관의 DNS 도구에서 '**@**' 기호로 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-149">You must also provide the domain or subdomain alias for the CNAME, such as **www** if you want to create an alias for **www.customdomain.com**. If you want to create an alias for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="b25da-150">정식 호스트 이름을 제공해야 합니다. 이 경우에는 응용 프로그램의 **cloudapp.net** 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="b25da-151">예를 들어 다음 CNAME 레코드는 **www.contoso.com**의 모든 트래픽을 배포된 응용 프로그램의 사용자 지정 도메인 이름인 **contoso.cloudapp.net**으로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-151">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.cloudapp.net**, the custom domain name of your deployed application:</span></span>

| <span data-ttu-id="b25da-152">별칭/호스트 이름/하위 도메인</span><span class="sxs-lookup"><span data-stu-id="b25da-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="b25da-153">정식 도메인</span><span class="sxs-lookup"><span data-stu-id="b25da-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="b25da-154">www</span><span class="sxs-lookup"><span data-stu-id="b25da-154">www</span></span> |<span data-ttu-id="b25da-155">contoso.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="b25da-155">contoso.cloudapp.net</span></span> |

<span data-ttu-id="b25da-156">**www.contoso.com** 의 방문자에게는 실제 호스트(contoso.cloudapp.net)가 표시되지 않으므로 최종 사용자가 전달 프로세스를 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-156">A visitor of **www.contoso.com** will never see the true host (contoso.cloudapp.net), so the forwarding process is invisible to the end user.</span></span>

> [!NOTE]
> <span data-ttu-id="b25da-157">위 예제는 **www** 하위 도메인의 트래픽에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-157">The example above only applies to traffic at the **www** subdomain.</span></span> <span data-ttu-id="b25da-158">CNAME 레코드와 함께 와일드카드를 사용할 수 없으므로 각 도메인/하위 도메인에 대해 하나의 CNAME을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="b25da-159">\*.contoso.com 등의 하위 도메인에서 cloudapp.net 주소로 트래픽을 보내려는 경우 DNS 설정에서 **URL 리디렉션** 또는 **URL 전달** 항목을 구성하거나 A 레코드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-159">If you want to direct  traffic from subdomains, such as \*.contoso.com, to your cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="b25da-160">사용자 지정 도메인에 대한 A 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="b25da-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="b25da-161">A 레코드를 만들려면 먼저 클라우드 서비스의 가상 IP 주소를 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-161">To create an A record, you must first find the virtual IP address of your cloud service.</span></span> <span data-ttu-id="b25da-162">그런 다음 등록 기관에서 제공한 도구를 사용하여 사용자 지정 도메인에 대한 새 항목을 DNS 테이블에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-162">Then add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="b25da-163">각 등록 기관은 서로 유사하지만 약간 다른 방법으로 A 레코드를 지정하지만 개념은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-163">Each registrar has a similar but slightly different method of specifying an A record, but the concepts are the same.</span></span>

1. <span data-ttu-id="b25da-164">다음 방법 중 하나를 사용하여 클라우드 서비스의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-164">Use one of the following methods to get the IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="b25da-165">[Azure 클래식 포털]에 로그인하고 클라우드 서비스를 선택한 다음 **대시보드**를 선택하고 **간략 상태** 섹션에서 **공용 VIP(가상 IP) 주소** 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-165">login to the [Azure classic portal], select your cloud service, select **Dashboard**, and then find the **Public Virtual IP (VIP) address** entry in the **quick glance** section.</span></span>
     
       ![VIP를 표시하는 한눈에 보기 섹션][vip]
     
       <span data-ttu-id="b25da-167">**또는**</span><span class="sxs-lookup"><span data-stu-id="b25da-167">**OR**</span></span>  
   * <span data-ttu-id="b25da-168">[Azure Powershell](/powershell/azure/overview)을 설치 및 구성하고 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="b25da-169">여러 끝점이 클라우드 서비스에 연결되어 있는 경우 IP 주소가 포함된 여러 줄을 받지만 모두 동일한 주소가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-169">If you have multiple endpoints associated with your cloud service, you will receive multiple lines containing the IP address, but all should display the same address.</span></span>
     
     <span data-ttu-id="b25da-170">A 레코드를 만들 때 필요하므로 IP 주소를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-170">Save the IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="b25da-171">DNS 등록 기관의 웹 사이트에 로그온한 다음 DNS 관리 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-171">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="b25da-172">**도메인 이름**, **DNS** 또는 **이름 서버 관리**로 레이블이 지정된 사이트의 링크 또는 영역을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-172">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="b25da-173">이제 A 레코드를 선택하거나 입력할 수 있는 위치를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-173">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="b25da-174">드롭다운에서 레코드 유형을 선택하거나 고급 설정 페이지로 이동해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-174">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span>
4. <span data-ttu-id="b25da-175">이 A 레코드를 사용할 도메인 또는 하위 도메인을 선택하거나 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-175">Select or enter the domain or subdomain that will use this A record.</span></span> <span data-ttu-id="b25da-176">예를 들어 **www.customdomain.com**에 대한 별칭을 만들려는 경우 **www**를 선택합니다. 모든 하위 도메인에 대한 와일드카드 항목을 만들려면 '__*__'를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-176">For example, select **www** if you want to create an alias for **www.customdomain.com**. If you want to create a wildcard entry for all subdomains, enter '__*__'.</span></span> <span data-ttu-id="b25da-177">그러면 **mail.customdomain.com**, **login.customdomain.com**, **www.customdomain.com** 등의 모든 하위 도메인이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-177">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="b25da-178">루트 도메인에 대한 A 레코드를 만들려는 경우 등록 기관의 DNS 도구에서 '**@**' 기호로 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-178">If you want to create an A record for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="b25da-179">제공된 필드에 클라우드 서비스의 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-179">Enter the IP address of your cloud service in the provided field.</span></span> <span data-ttu-id="b25da-180">그러면 A 레코드에 사용된 도메인 항목이 클라우드 서비스 배포의 IP 주소와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-180">This associates the domain entry used in the A record with the IP address of your cloud service deployment.</span></span>

<span data-ttu-id="b25da-181">예를 들어 다음 A 레코드는 모든 트래픽을 **contoso.com**에서 배포된 응용 프로그램의 IP 주소인 **137.135.70.239**로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-181">For example, the following A record forwards all traffic from **contoso.com** to **137.135.70.239**, the IP address of your deployed application:</span></span>

| <span data-ttu-id="b25da-182">호스트 이름/하위 도메인</span><span class="sxs-lookup"><span data-stu-id="b25da-182">Host name/Subdomain</span></span> | <span data-ttu-id="b25da-183">IP 주소</span><span class="sxs-lookup"><span data-stu-id="b25da-183">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="b25da-184">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="b25da-184">137.135.70.239</span></span> |

<span data-ttu-id="b25da-185">이 예제에서는 루트 도메인에 대한 A 레코드를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-185">This example demonstrates creating an A record for the root domain.</span></span> <span data-ttu-id="b25da-186">모든 하위 도메인을 포함할 와일드카드 항목을 만들려면 '__*__'를 하위 도메인으로 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-186">If you wish to create a wildcard entry to cover all subdomains, you would enter '__*__' as the subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="b25da-187">Azure의 IP 주소는 기본적으로 동적입니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-187">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="b25da-188">사용자의 IP 주소가 변경되지 않도록 [예약된 IP 주소](../virtual-network/virtual-networks-reserved-public-ip.md) 를 사용하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-188">You will probably want to use a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) to ensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b25da-189">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b25da-189">Next steps</span></span>
* [<span data-ttu-id="b25da-190">클라우드 서비스를 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="b25da-190">How to Manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="b25da-191">CDN 콘텐츠를 사용자 지정 도메인에 매핑하는 방법</span><span class="sxs-lookup"><span data-stu-id="b25da-191">How to Map CDN Content to a Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="b25da-192">[클라우드 서비스의 일반 구성](cloud-services-how-to-configure.md)</span><span class="sxs-lookup"><span data-stu-id="b25da-192">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="b25da-193">[클라우드 서비스를 배포](cloud-services-how-to-create-deploy.md)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b25da-193">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="b25da-194">[SSL 인증서](cloud-services-configure-ssl-certificate.md)구성</span><span class="sxs-lookup"><span data-stu-id="b25da-194">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates the subdomain with the storage account]: #create-cname
[Azure 클래식 포털]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
