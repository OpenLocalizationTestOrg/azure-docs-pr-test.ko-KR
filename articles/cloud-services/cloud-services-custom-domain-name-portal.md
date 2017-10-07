---
title: "클라우드 서비스에서 사용자 지정 도메인 이름 aaaConfigure | Microsoft Docs"
description: "자세한 내용은 어떻게 tooexpose Azure에 응용 프로그램이 나 데이터 toohello DNS 설정을 구성 하 여 사용자 지정 도메인에 인터넷 합니다.  이러한 예제는 hello Azure 포털을 사용합니다."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: a0f3186b6022fbc4570ef1ce4b921426842bde76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="a46e3-104">Azure 클라우드 서비스에 대한 사용자 지정 도메인 이름 구성</span><span class="sxs-lookup"><span data-stu-id="a46e3-104">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a46e3-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="a46e3-105">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="a46e3-106">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="a46e3-106">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="a46e3-107">클라우드 서비스를 만들 때 Azure 할당의 하위 도메인이 tooa **cloudapp.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-107">When you create a Cloud Service, Azure assigns it tooa subdomain of **cloudapp.net**.</span></span> <span data-ttu-id="a46e3-108">예를 들어 클라우드 서비스 이름이 "contoso" 이면 사용자의 사용자에 게 수 tooaccess http://contoso.cloudapp.net 같은 URL에서 응용 프로그램 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-108">For example, if your Cloud Service is named "contoso", your users will be able tooaccess your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="a46e3-109">Azure는 가상 IP 주소도 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-109">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="a46e3-110">그러나 **contoso.com**등의 고유한 도메인 이름에도 응용 프로그램을 표시할 수 있습니다. 이 문서에서는 설명 어떻게 tooreserve 또는 클라우드 서비스 웹 역할에 대 한 사용자 지정 도메인 이름을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-110">However, you can also expose your application on your own domain name, such as **contoso.com**. This article explains how tooreserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="a46e3-111">CNAME 및 A 레코드가 무엇인지 이미 알고 있나요?</span><span class="sxs-lookup"><span data-stu-id="a46e3-111">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="a46e3-112">[Hello 설명은 이전 점프](#add-a-cname-record-for-your-custom-domain)합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-112">[Jump past hello explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="a46e3-113">이 작업의 hello 프로시저 tooAzure 클라우드 서비스를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-113">hello procedures in this task apply tooAzure Cloud Services.</span></span> <span data-ttu-id="a46e3-114">앱 서비스의 경우 [이것](../app-service-web/web-sites-custom-domain-name.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a46e3-114">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="a46e3-115">저장소 계정의 경우 [이것](../storage/blobs/storage-custom-domain-name.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a46e3-115">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

<p/>

> [!TIP]
> <span data-ttu-id="a46e3-116">더 빠르게-안내 새로운 Azure hello를 사용 하 여 [단계별 연습](http://support.microsoft.com/kb/2990804)!</span><span class="sxs-lookup"><span data-stu-id="a46e3-116">Get going faster--use hello NEW Azure [guided walkthrough](http://support.microsoft.com/kb/2990804)!</span></span>  <span data-ttu-id="a46e3-117">이 연습을 통해 사용자 지정 도메인 이름을 연결하고 SSL을 사용하여 Azure 클라우드 서비스 또는 Azure 웹 사이트와의 통신을 보호하는 등의 작업을 매우 쉽게 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-117">It makes associating a custom domain name AND securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="a46e3-118">CNAME 및 A 레코드 이해</span><span class="sxs-lookup"><span data-stu-id="a46e3-118">Understand CNAME and A records</span></span>
<span data-ttu-id="a46e3-119">그러나 CNAME (또는 별칭 레코드) 및 A 레코드 모두 tooassociate 특정 서버와 도메인 이름을 사용 하면 (또는 경우 서비스) 다르게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-119">CNAME (or alias records) and A records both allow you tooassociate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="a46e3-120">또한 일부 특정 고려 사항이 어떤 toouse 결정 하기 전에 고려해 야 하는 Azure 클라우드 서비스와 A 레코드를 사용 하는 경우 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which toouse.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="a46e3-121">CNAME 또는 별칭 레코드</span><span class="sxs-lookup"><span data-stu-id="a46e3-121">CNAME or Alias record</span></span>
<span data-ttu-id="a46e3-122">매핑하는 CNAME 레코드는 *특정* 도메인에 같은 **contoso.com** 또는 **www.contoso.com**, tooa 정규 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, tooa canonical domain name.</span></span> <span data-ttu-id="a46e3-123">이 경우 hello 정규 도메인 이름에는 hello **[myapp].cloudapp.net** Azure의 도메인 이름을 응용 프로그램을 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-123">In this case, hello canonical domain name is hello **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="a46e3-124">Hello CNAME 만듭니다 hello에 대 한 별칭을 만든 후 **[myapp].cloudapp.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-124">Once created, hello CNAME creates an alias for hello **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="a46e3-125">hello CNAME 항목 toohello IP 주소를 갖게 프로그램 **[myapp].cloudapp.net** hello 클라우드 서비스의 hello IP 주소가 변경 되 면 없는 tootake 조치 하므로 자동으로 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-125">hello CNAME entry will resolve toohello IP address of your **[myapp].cloudapp.net** service automatically, so if hello IP address of hello cloud service changes, you do not have tootake any action.</span></span>

> [!NOTE]
> <span data-ttu-id="a46e3-126">일부 도메인 등록 기관에서는 toomap 하위 도메인 예: www.contoso.com 및 루트 이름이 아니라 contoso.com 등의 CNAME 레코드를 사용 하는 경우. CNAME 레코드에 대 한 자세한 내용은 사용자 등록 기관에서 제공 하는 hello 설명서를 참조 하십시오. [CNAME 레코드에 대 한 Wikipedia 항목 hello](http://en.wikipedia.org/wiki/CNAME_record), 또는 hello [IETF 도메인 이름-구현 및 사양](http://tools.ietf.org/html/rfc1035) 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-126">Some domain registrars only allow you toomap subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see hello documentation provided by your registrar, [hello Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or hello [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="a46e3-127">A 레코드</span><span class="sxs-lookup"><span data-stu-id="a46e3-127">A record</span></span>
<span data-ttu-id="a46e3-128">*A* 레코드와 같은 도메인을 매핑합니다 **contoso.com** 또는 **www.contoso.com**, *또는 와일드 카드 도메인* 같은  **\*. contoso.com**, tooan IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-128">An *A* record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, tooan IP address.</span></span> <span data-ttu-id="a46e3-129">Azure 클라우드 서비스의 경우 hello hello hello 서비스의 가상 IP입니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-129">In hello case of an Azure Cloud Service, hello virtual IP of hello service.</span></span> <span data-ttu-id="a46e3-130">와 같은 와일드 카드를 사용 하는 항목이 하나 있을 수에 CNAME 레코드를 통해 A 레코드의 주요 장점은 hello 이므로 \* **. contoso.com**, 같은 여러 하위 도메인에 대 한 요청을 처리할 것는  **mail.contoso.com**, **login.contoso.com**, 또는 **www.contso.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-130">So hello main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="a46e3-131">A 레코드 매핑되어 있으므로 tooa 고정 IP 주소를 클라우드 서비스의 변경 내용을 toohello IP 주소를 자동으로 해결 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-131">Since an A record is mapped tooa static IP address, it cannot automatically resolve changes toohello IP address of your Cloud Service.</span></span> <span data-ttu-id="a46e3-132">클라우드 서비스에서 사용 하는 hello IP 주소가 hello 처음 tooan 빈 슬롯 (프로덕션 또는 스테이징.)를 배포할 때 할당 된 Hello 슬롯에 대 한 hello 배포를 삭제 하면 hello IP 주소는 Azure에 의해 해제 되 고 모든 이후 배포 toohello 슬롯 새 IP 주소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-132">hello IP address used by your Cloud Service is allocated hello first time you deploy tooan empty slot (either production or staging.) If you delete hello deployment for hello slot, hello IP address is released by Azure and any future deployments toohello slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="a46e3-133">편리 하 게 지정 된 배포 슬롯 (프로덕션 또는 스테이징)의 IP 주소 hello 스테이징 및 프로덕션 배포 또는 기존 배포의 전체 업그레이드 수행 사이의 테스트할 때 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-133">Conveniently, hello IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="a46e3-134">이러한 작업 수행에 대 한 자세한 내용은 참조 하십시오. [어떻게 toomanage 클라우드 서비스](cloud-services-how-to-manage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-134">For more information on performing these actions, see [How toomanage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="a46e3-135">사용자 지정 도메인에 대한 CNAME 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="a46e3-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="a46e3-136">toocreate CNAME 레코드를 추가 해야 새 항목 hello DNS 테이블의 사용자 지정 도메인에 대 한 등록 기관에서 제공 하는 hello 도구를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-136">toocreate a CNAME record, you must add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="a46e3-137">각 등록자 CNAME 레코드를 지정 하는 유사 하지만 약간 다른 방법은 갖지만 개념은 hello hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="a46e3-138">이러한 메서드 toofind hello 중 하나를 사용 하 여 **. cloudapp.net에** tooyour 클라우드 서비스에 할당 된 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-138">Use one of these methods toofind hello **.cloudapp.net** domain name assigned tooyour cloud service.</span></span>
   
   * <span data-ttu-id="a46e3-139">로그인 toohello [Azure 포털], 클라우드 서비스를 선택, hello를 살펴보고 **Essentials** 섹션 했는데 이후에 hello **사이트 URL** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-139">Login toohello [Azure portal], select your cloud service, look at hello **Essentials** section and then find hello **Site URL** entry.</span></span>
     
       ![hello 사이트 URL을 보여 주는 빠른 보기 섹션][csurl]
     
       <span data-ttu-id="a46e3-141">**또는**</span><span class="sxs-lookup"><span data-stu-id="a46e3-141">**OR**</span></span>
   * <span data-ttu-id="a46e3-142">설치 및 구성 [Azure Powershell](/powershell/azure/overview)를 사용 하 여 hello 명령을 누른 다음:</span><span class="sxs-lookup"><span data-stu-id="a46e3-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="a46e3-143">CNAME 레코드를 만들 때 필요 합니다에 따라 두 가지 방법 중 하나에서 반환 된 hello URL에 사용 되는 hello 도메인 이름을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-143">Save hello domain name used in hello URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="a46e3-144">Tooyour DNS 등록 기관의 웹 사이트에서 오류를 로깅하고 toohello DNS 관리 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-144">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="a46e3-145">링크 검색 또는 hello 사이트의 영역으로 표시 **도메인 이름**, **DNS**, 또는 **이름 서버 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-145">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="a46e3-146">이제 CNAME을 선택하거나 입력할 수 있는 위치를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="a46e3-147">드롭다운에서 입력 하거나 이동 하 여 고급 설정 페이지 tooan tooselect hello 레코드가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-147">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span> <span data-ttu-id="a46e3-148">Hello 단어 찾아야 **CNAME**, **별칭**, 또는 **하위 도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-148">You should look for hello words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="a46e3-149">도 제공 해야 hello 도메인 또는 하위 도메인 별칭 CNAME hello에 대 한 같은 **www** toocreate에 대 한 별칭을 사용할 경우 **www.customdomain.com**합니다. Hello로 나타날 수 있습니다 hello 루트 도메인에 대 한 별칭 toocreate 하려는 경우 '**@**' 등록자의 DNS 도구에서 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-149">You must also provide hello domain or subdomain alias for hello CNAME, such as **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate an alias for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="a46e3-150">정식 호스트 이름을 제공해야 합니다. 이 경우에는 응용 프로그램의 **cloudapp.net** 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="a46e3-151">CNAME 레코드의 다음 hello에서 모든 트래픽을 전달 하는 예를 들어 **www.contoso.com** 너무**contoso.cloudapp.net**, 배포 된 응용 프로그램의 사용자 지정 도메인 이름을 hello:</span><span class="sxs-lookup"><span data-stu-id="a46e3-151">For example, hello following CNAME record forwards all traffic from **www.contoso.com** too**contoso.cloudapp.net**, hello custom domain name of your deployed application:</span></span>

| <span data-ttu-id="a46e3-152">별칭/호스트 이름/하위 도메인</span><span class="sxs-lookup"><span data-stu-id="a46e3-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="a46e3-153">정식 도메인</span><span class="sxs-lookup"><span data-stu-id="a46e3-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="a46e3-154">www</span><span class="sxs-lookup"><span data-stu-id="a46e3-154">www</span></span> |<span data-ttu-id="a46e3-155">contoso.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="a46e3-155">contoso.cloudapp.net</span></span> |

> [!NOTE]
> <span data-ttu-id="a46e3-156">방문자 **www.contoso.com** 프로세스를 전달 하는 hello 보이지 않는 toothe 최종 사용자는 hello true 호스트 (contoso.cloudapp.net) 표시 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-156">A visitor of **www.contoso.com** will never see hello true host (contoso.cloudapp.net), so hello forwarding process is invisible toothe end user.</span></span>
> 
> <span data-ttu-id="a46e3-157">hello 위의 적용 하는 예제 hello에 tootraffic **www** 하위 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-157">hello example above only applies tootraffic at hello **www** subdomain.</span></span> <span data-ttu-id="a46e3-158">CNAME 레코드와 함께 와일드카드를 사용할 수 없으므로 각 도메인/하위 도메인에 대해 하나의 CNAME을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="a46e3-159">와 같은 하위 도메인의 경우에서 toodirect 트래픽을 원하는 경우 *. contoso.com, tooyour cloudapp.net 주소를 구성할 수 있습니다는 **URL 리디렉션** 또는 **앞으로 URL** DNS 설정 등의 항목 하거나 A 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-159">If you want toodirect  traffic from subdomains, such as *.contoso.com, tooyour cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="a46e3-160">사용자 지정 도메인에 대한 A 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="a46e3-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="a46e3-161">toocreate A 레코드를 먼저 클라우드 서비스의 가상 IP 주소 hello 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-161">toocreate an A record, you must first find hello virtual IP address of your cloud service.</span></span> <span data-ttu-id="a46e3-162">그런 다음 등록 기관에서 제공 하는 hello 도구를 사용 하 여 사용자 지정 도메인에 대 한 hello DNS 테이블의 새 항목을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-162">Then add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="a46e3-163">각 등록자 A 레코드를 지정 하는 유사 하지만 약간 다른 방법은 갖지만 개념은 hello hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-163">Each registrar has a similar but slightly different method of specifying an A record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="a46e3-164">Hello 다음 클라우드 서비스의 메서드 tooget hello IP 주소 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-164">Use one of hello following methods tooget hello IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="a46e3-165">로그인 toohello [Azure 포털], 클라우드 서비스를 선택, hello를 살펴보고 **Essentials** 섹션 했는데 이후에 hello **공용 IP 주소** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-165">Login toohello [Azure portal], select your cloud service, look at hello **Essentials** section and then find hello **Public IP addresses** entry.</span></span>
     
       ![hello VIP를 보여 주는 빠른 보기 섹션][vip]
     
       <span data-ttu-id="a46e3-167">**또는**</span><span class="sxs-lookup"><span data-stu-id="a46e3-167">**OR**</span></span>
   * <span data-ttu-id="a46e3-168">설치 및 구성 [Azure Powershell](/powershell/azure/overview)를 사용 하 여 hello 명령을 누른 다음:</span><span class="sxs-lookup"><span data-stu-id="a46e3-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="a46e3-169">A 레코드를 만들 때 필요한는 hello IP 주소를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-169">Save hello IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="a46e3-170">Tooyour DNS 등록 기관의 웹 사이트에서 오류를 로깅하고 toohello DNS 관리 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-170">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="a46e3-171">링크 검색 또는 hello 사이트의 영역으로 표시 **도메인 이름**, **DNS**, 또는 **이름 서버 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-171">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="a46e3-172">이제 A 레코드를 선택하거나 입력할 수 있는 위치를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-172">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="a46e3-173">드롭다운에서 입력 하거나 이동 하 여 고급 설정 페이지 tooan tooselect hello 레코드가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-173">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span>
4. <span data-ttu-id="a46e3-174">선택 하거나 입력 hello 도메인 또는 하위 도메인을이 A 레코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-174">Select or enter hello domain or subdomain that will use this A record.</span></span> <span data-ttu-id="a46e3-175">예를 들어 선택 **www** toocreate에 대 한 별칭을 사용할 경우 **www.customdomain.com**합니다. 모든 하위 도메인에 대 한 와일드 카드 항목 toocreate 하려는 경우 입력 ' * * * '입니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-175">For example, select **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate a wildcard entry for all subdomains, enter '*****'.</span></span> <span data-ttu-id="a46e3-176">그러면 **mail.customdomain.com**, **login.customdomain.com**, **www.customdomain.com** 등의 모든 하위 도메인이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-176">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="a46e3-177">Hello 루트 도메인에 대 한 toocreate A 레코드를 원하는 경우 hello로 나타날 수 있습니다 '**@**' 등록자의 DNS 도구에서 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-177">If you want toocreate an A record for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="a46e3-178">필드를 제공 하는 hello에 클라우드 서비스의 hello IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-178">Enter hello IP address of your cloud service in hello provided field.</span></span> <span data-ttu-id="a46e3-179">이 클라우드 서비스 배포의 hello IP 주소로 hello A 레코드에 사용 되는 hello 도메인 항목에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-179">This associates hello domain entry used in hello A record with hello IP address of your cloud service deployment.</span></span>

<span data-ttu-id="a46e3-180">레코드의 다음 hello에서 모든 트래픽을 전달 하는 예를 들어 **contoso.com** 너무**137.135.70.239**, 배포 된 응용 프로그램의 IP 주소를 hello:</span><span class="sxs-lookup"><span data-stu-id="a46e3-180">For example, hello following A record forwards all traffic from **contoso.com** too**137.135.70.239**, hello IP address of your deployed application:</span></span>

| <span data-ttu-id="a46e3-181">호스트 이름/하위 도메인</span><span class="sxs-lookup"><span data-stu-id="a46e3-181">Host name/Subdomain</span></span> | <span data-ttu-id="a46e3-182">IP 주소</span><span class="sxs-lookup"><span data-stu-id="a46e3-182">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="a46e3-183">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="a46e3-183">137.135.70.239</span></span> |

<span data-ttu-id="a46e3-184">이 예제에서는 hello 루트 도메인에 대 한 A 레코드를 만드는 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-184">This example demonstrates creating an A record for hello root domain.</span></span> <span data-ttu-id="a46e3-185">와일드 카드 항목 toocover toocreate을 원하는 경우 입력 하위 도메인을 모두 ' * * * ' hello 하위 도메인으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-185">If you wish toocreate a wildcard entry toocover all subdomains, you would enter '*****' as hello subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="a46e3-186">Azure의 IP 주소는 기본적으로 동적입니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-186">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="a46e3-187">Toouse 수도 있습니다는 [예약 된 IP 주소](../virtual-network/virtual-networks-reserved-public-ip.md) IP 주소가 변경 되지 않고 tooensure 합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-187">You will probably want toouse a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a46e3-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a46e3-188">Next steps</span></span>
* [<span data-ttu-id="a46e3-189">TooManage 클라우드 서비스 하는 방법</span><span class="sxs-lookup"><span data-stu-id="a46e3-189">How tooManage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="a46e3-190">어떻게 tooMap CDN 콘텐츠 tooa 사용자 지정 도메인</span><span class="sxs-lookup"><span data-stu-id="a46e3-190">How tooMap CDN Content tooa Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="a46e3-191">[클라우드 서비스의 일반 구성](cloud-services-how-to-configure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a46e3-191">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="a46e3-192">너무 방법에 대해 알아봅니다[클라우드 서비스 배포](cloud-services-how-to-create-deploy-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a46e3-192">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="a46e3-193">[SSL 인증서](cloud-services-configure-ssl-certificate-portal.md)구성</span><span class="sxs-lookup"><span data-stu-id="a46e3-193">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[Azure 포털]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
