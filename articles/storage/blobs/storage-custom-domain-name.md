---
title: "Azure Blob 저장소 끝점에 대 한 사용자 지정 도메인 이름 aaaConfigure | Microsoft Docs"
description: "Azure 저장소 계정에 Azure 포털 toomap hello 사용자 고유의 정식 이름 (CNAME) toohello Blob 저장소 끝점을 사용 합니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: aaafd8c5-eacb-49dc-8c8b-3f7011ad5e92
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: marsma
ms.openlocfilehash: bfee6d28039f389ba2e2ed6b28d43894b6e15469
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-for-your-blob-storage-endpoint"></a><span data-ttu-id="2480d-103">Blob 저장소 끝점에 대한 사용자 지정 도메인 이름 구성</span><span class="sxs-lookup"><span data-stu-id="2480d-103">Configure a custom domain name for your Blob storage endpoint</span></span>

<span data-ttu-id="2480d-104">Azure 저장소 계정에서 Blob 데이터에 액세스할 수 있도록 사용자 지정 도메인을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-104">You can configure a custom domain for accessing blob data in your Azure storage account.</span></span> <span data-ttu-id="2480d-105">Blob 저장소에 대 한 기본 끝점을 hello `<storage-account-name>.blob.core.windows.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-105">hello default endpoint for Blob storage is `<storage-account-name>.blob.core.windows.net`.</span></span> <span data-ttu-id="2480d-106">사용자 지정 도메인과 같은 하위 도메인을 매핑하는 경우 **www.contoso.com** toohello 저장소 계정의 blob 끝점, 사용자가 액세스할 수 blob 해당 도메인을 사용 하 여 저장소 계정에는 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-106">If you map a custom domain and subdomain like **www.contoso.com** toohello blob endpoint for your storage account, your users can then access blob data in your storage account using that domain.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2480d-107">Azure Storage는 아직 기본적으로 사용자 지정 도메인으로 HTTPS를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-107">Azure Storage does not yet natively support HTTPS with custom domains.</span></span> <span data-ttu-id="2480d-108">현재 수 [hello Azure CDN tooaccess blob를 사용 하 여 HTTPS를 통해 사용자 지정 도메인과](storage-https-custom-domain-cdn.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-108">You can currently [Use hello Azure CDN tooaccess blobs with custom domains over HTTPS](storage-https-custom-domain-cdn.md).</span></span>
>

<span data-ttu-id="2480d-109">hello 다음 표에 나와 라는 저장소 계정에 있는 blob 데이터에 대 한 몇 가지 샘플 Url **mystorageaccount**합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-109">hello following table shows a few sample URLs for blob data located in a storage account named **mystorageaccount**.</span></span> <span data-ttu-id="2480d-110">저장소 계정이 hello에 대 한 hello 사용자 지정 도메인 등록 **www.contoso.com**:</span><span class="sxs-lookup"><span data-stu-id="2480d-110">hello custom domain registered for hello storage account is **www.contoso.com**:</span></span>

| <span data-ttu-id="2480d-111">리소스 종류</span><span class="sxs-lookup"><span data-stu-id="2480d-111">Resource Type</span></span> | <span data-ttu-id="2480d-112">기본 URL</span><span class="sxs-lookup"><span data-stu-id="2480d-112">Default URL</span></span> | <span data-ttu-id="2480d-113">사용자 지정 도메인 URL</span><span class="sxs-lookup"><span data-stu-id="2480d-113">Custom domain URL</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2480d-114">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="2480d-114">Storage account</span></span> | <span data-ttu-id="2480d-115">http://mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="2480d-115">http://mystorageaccount.blob.core.windows.net</span></span> | <span data-ttu-id="2480d-116">http://www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="2480d-116">http://www.contoso.com</span></span> |
| <span data-ttu-id="2480d-117">Blob</span><span class="sxs-lookup"><span data-stu-id="2480d-117">Blob</span></span> |<span data-ttu-id="2480d-118">http://mystorageaccount.blob.core.windows.net/mycontainer/myblob</span><span class="sxs-lookup"><span data-stu-id="2480d-118">http://mystorageaccount.blob.core.windows.net/mycontainer/myblob</span></span> | <span data-ttu-id="2480d-119">http://www.contoso.com/mycontainer/myblob</span><span class="sxs-lookup"><span data-stu-id="2480d-119">http://www.contoso.com/mycontainer/myblob</span></span> |
| <span data-ttu-id="2480d-120">루트 컨테이너</span><span class="sxs-lookup"><span data-stu-id="2480d-120">Root container</span></span> | <span data-ttu-id="2480d-121">http://mystorageaccount.blob.core.windows.net/myblob 또는 http://mystorageaccount.blob.core.windows.net/$root/myblob</span><span class="sxs-lookup"><span data-stu-id="2480d-121">http://mystorageaccount.blob.core.windows.net/myblob or http://mystorageaccount.blob.core.windows.net/$root/myblob</span></span>| <span data-ttu-id="2480d-122">http://www.contoso.com/myblob 또는 http://www.contoso.com/$root/myblob</span><span class="sxs-lookup"><span data-stu-id="2480d-122">http://www.contoso.com/myblob or http://www.contoso.com/$root/myblob</span></span> |

## <a name="direct-vs-intermediary-domain-mapping"></a><span data-ttu-id="2480d-123">직접 도메인 매핑과 중간 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="2480d-123">Direct vs. intermediary domain mapping</span></span>

<span data-ttu-id="2480d-124">두 가지 방법으로 toopoint 저장소 계정에 대 한 사용자 지정 도메인 toohello blob 끝점 가지: CNAME 매핑과 hello를 사용 하 여 직접 *asverify* 중간 하위 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-124">There are two ways toopoint your custom domain toohello blob endpoint for your storage account: direct CNAME mapping, and using hello *asverify* intermediary subdomain.</span></span>

### <a name="direct-cname-mapping"></a><span data-ttu-id="2480d-125">직접 CNAME 매핑</span><span class="sxs-lookup"><span data-stu-id="2480d-125">Direct CNAME mapping</span></span>

<span data-ttu-id="2480d-126">hello 첫 번째 및 가장 간단한 방법은 toocreate toohello blob 끝점을 직접 사용자 지정 도메인 및 하위 도메인을 매핑하는 정식 이름 (CNAME) 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-126">hello first, and simplest, method is toocreate a canonical name (CNAME) record that maps your custom domain and subdomain directly toohello blob endpoint.</span></span> <span data-ttu-id="2480d-127">CNAME 레코드는 원본 도메인 tooa 대상 도메인을 매핑하는 도메인 이름 (DNS) 시스템 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-127">A CNAME record is a domain name system (DNS) feature that maps a source domain tooa destination domain.</span></span> <span data-ttu-id="2480d-128">이 경우 hello 원본 도메인은 사용자 고유의 사용자 지정 도메인 및 하위 도메인, 예를 들어 *www.contoso.com*. hello 대상 도메인은 Blob 서비스 끝점, 예를 들어  *mystorageaccount.blob.core.windows.net*합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-128">In this case, hello source domain is your own custom domain and subdomain, for example *www.contoso.com*. hello destination domain is your Blob service endpoint, for example *mystorageaccount.blob.core.windows.net*.</span></span>

<span data-ttu-id="2480d-129">hello 직접적인 방법에 대해서는 [사용자 지정 도메인 등록](#register-a-custom-domain)합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-129">hello direct method is covered in [Register a custom domain](#register-a-custom-domain).</span></span>

### <a name="intermediary-mapping-with-asverify"></a><span data-ttu-id="2480d-130">*asverify*를 사용하여 중간 매핑</span><span class="sxs-lookup"><span data-stu-id="2480d-130">Intermediary mapping with *asverify*</span></span>

<span data-ttu-id="2480d-131">두 번째 방법은 hello 또한 CNAME 레코드를 사용 하 여 하지만 Azure tooavoid 가동 중지 시간에서 인식 되는 특별 한 하위 도메인을 사용 하는 먼저: **asverify**합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-131">hello second method also uses CNAME records, but first employs a special subdomain recognized by Azure tooavoid downtime: **asverify**.</span></span>

<span data-ttu-id="2480d-132">사용자 지정 도메인 tooa blob 끝점을 매핑하 hello 프로세스 hello에 등록 하는 동안 hello 도메인에 대 한 가동 중지 시간이 짧은 기간 동안 될 수 있습니다 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-132">hello process of mapping your custom domain tooa blob endpoint can result in a brief period of downtime for hello domain while you are registering it in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2480d-133">사용자 지정 도메인에서 현재 작동 중단 시간이 없는 필요로 하는 서비스 수준 계약 (SLA)으로 응용 프로그램을 지 원하는 경우 hello Azure를 사용할 수 있습니다 *asverify* 중간 등록 단계와 하위 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-133">If your custom domain is currently supporting an application with a service-level agreement (SLA) that requires zero downtime, then you can use hello Azure *asverify* subdomain as an intermediate registration step.</span></span> <span data-ttu-id="2480d-134">중간 이렇게 하면 사용자 수 tooaccess 도메인 클래스 중는 hello DNS 매핑이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-134">This intermediate step ensures users are able tooaccess your domain while hello DNS mapping takes place.</span></span>

<span data-ttu-id="2480d-135">hello 중간 메서드에 대해서는 [hello를 사용 하 여 사용자 지정 도메인 등록 *asverify* 하위 도메인](#register-a-custom-domain-using-the-asverify-subdomain)합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-135">hello intermediary method is covered in [Register a custom domain using hello *asverify* subdomain](#register-a-custom-domain-using-the-asverify-subdomain).</span></span>

## <a name="register-a-custom-domain"></a><span data-ttu-id="2480d-136">사용자 지정 도메인 등록</span><span class="sxs-lookup"><span data-stu-id="2480d-136">Register a custom domain</span></span>
<span data-ttu-id="2480d-137">없거나 현재 사용자 지정 도메인이 응용 프로그램을 호스팅하지 않는 tooyour 간단 하 게 사용할 수 없는 사용자가 되 고 hello 도메인에 대 한 문제 없이 경우이 절차 tooregister 사용자 지정 도메인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-137">Use this procedure tooregister your custom domain if you have no concerns about hello domain being briefly unavailable tooyour users, or if your custom domain is not currently hosting an application.</span></span>

<span data-ttu-id="2480d-138">현재 사용자 지정 도메인이 가동 중지 시간을 가질 수 없는 응용 프로그램을 지원 하 고, 경우에 설명 된 hello 절차에 따라 [hello를 사용 하 여 사용자 지정 도메인 등록 *asverify* 하위 도메인](#register-a-custom-domain-using-the-asverify-subdomain)합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-138">If your custom domain is currently supporting an application that cannot have any downtime, follow hello procedure outlined in [Register a custom domain using hello *asverify* subdomain](#register-a-custom-domain-using-the-asverify-subdomain).</span></span>

<span data-ttu-id="2480d-139">사용자 지정 도메인 이름을 tooconfigure 만들어야 새 CNAME 레코드를 DNS에 합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-139">tooconfigure a custom domain name, you must create a new CNAME record in DNS.</span></span> <span data-ttu-id="2480d-140">hello CNAME 레코드는 도메인 이름에 대 한 별칭을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-140">hello CNAME record specifies an alias for a domain name.</span></span> <span data-ttu-id="2480d-141">이 경우 저장소 계정에 대 한 사용자 지정 도메인 toohello Blob 저장소 끝점 주소가 hello를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-141">In this case, it maps hello address of your custom domain toohello Blob storage endpoint for your storage account.</span></span>

<span data-ttu-id="2480d-142">일반적으로 도메인 등록 기관의 웹 사이트에서 도메인의 DNS 설정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-142">Typically, you can manage your domain's DNS settings on your domain registrar's website.</span></span> <span data-ttu-id="2480d-143">각 등록자 CNAME 레코드를 지정 하는 유사 하지만 약간 다른 방법은 갖지만 hello 개념 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-143">Each registrar has a similar but slightly different method of specifying a CNAME record, but hello concept is hello same.</span></span> <span data-ttu-id="2480d-144">일부 기본 도메인 등록 패키지 제공 하지 않습니다 DNS 구성을 tooupgrade 수 있으므로 도메인 등록 패키지 hello CNAME 레코드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-144">Some basic domain registration packages do not offer DNS configuration, so you may need tooupgrade your domain registration package before you can create hello CNAME record.</span></span>

1. <span data-ttu-id="2480d-145">Hello에 tooyour 저장소 계정을 탐색 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-145">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="2480d-146">아래 **BLOB 서비스** hello 메뉴 블레이드에서 선택 **사용자 지정 도메인** tooopen hello *사용자 지정 도메인* 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-146">Under **BLOB SERVICE** on hello menu blade, select **Custom domain** tooopen hello *Custom domain* blade.</span></span>
1. <span data-ttu-id="2480d-147">Tooyour 도메인 등록 기관의 웹 사이트에서 오류를 로깅하고 toohello DNS 관리 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-147">Log on tooyour domain registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="2480d-148">**도메인 이름**, **DNS** 또는 **이름 서버 관리**와 같은 섹션에서 이를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-148">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
1. <span data-ttu-id="2480d-149">CNAMEs를 관리 하기 위한 hello 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-149">Find hello section for managing CNAMEs.</span></span> <span data-ttu-id="2480d-150">Toogo tooan 고급 설정 페이지를 hello 단어를 검색할 수도 있습니다 **CNAME**, **별칭**, 또는 **하위 도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-150">You may have toogo tooan advanced settings page and look for hello words **CNAME**, **Alias**, or **Subdomains**.</span></span>
1. <span data-ttu-id="2480d-151">새 CNAME 레코드를 만들어 **www** 또는 **photos**와 같은 하위 도메인 별칭을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-151">Create a new CNAME record and provide a subdomain alias such as **www** or **photos**.</span></span> <span data-ttu-id="2480d-152">그런 다음 hello 형태로 표시 하 여 Blob 서비스 끝점 호스트 이름, 제공 **mystorageaccount.blob.core.windows.net** (여기서 *mystorageaccount* hello 저장소 계정의 이름입니다).</span><span class="sxs-lookup"><span data-stu-id="2480d-152">Then provide a host name, which is your Blob service endpoint, in hello format **mystorageaccount.blob.core.windows.net** (where *mystorageaccount* is hello name of your storage account).</span></span> <span data-ttu-id="2480d-153">hello의 항목 # 1에에서 표시 되는 hello 호스트 이름 toouse *사용자 지정 도메인* hello 블레이드 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-153">hello host name toouse appears in item #1 of hello *Custom domain* blade in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="2480d-154">Hello에 hello 텍스트 상자에서 *사용자 지정 도메인* hello 블레이드 [Azure 포털](https://portal.azure.com), hello hello 하위 도메인을 포함 하 여 사용자 지정 도메인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-154">In hello text box on hello *Custom domain* blade in hello [Azure portal](https://portal.azure.com), enter hello name of your custom domain, including hello subdomain.</span></span> <span data-ttu-id="2480d-155">예를 들어 도메인이 **contoso.com**이고 하위 도메인 별칭이 **www**이면 **www.contoso.com**을 입력합니다. 하위 도메인 경우 **사진**, 입력 **photos.contoso.com**. hello 하위 도메인이 *필요한*합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-155">For example, if your domain is **contoso.com** and your subdomain alias is **www**, enter **www.contoso.com**. If your subdomain is **photos**, enter **photos.contoso.com**. hello subdomain is *required*.</span></span>
1. <span data-ttu-id="2480d-156">선택 **저장** hello에 *사용자 지정 도메인* 블레이드 tooregister 사용자 지정 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-156">Select **Save** on hello *Custom domain* blade tooregister your custom domain.</span></span> <span data-ttu-id="2480d-157">Hello 등록에 성공 하면 저장소 계정의 성공적으로 업데이트 된 포털 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-157">If hello registration is successful, you will see a portal notification that your storage account was successfully updated.</span></span>

<span data-ttu-id="2480d-158">새 CNAME 레코드는 DNS를 통해 전파 된, 사용자가으로 hello 적절 한 사용 권한을 갖습니다 사용자 지정 도메인을 사용 하 여 blob 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-158">Once your new CNAME record has propagated through DNS, your users can view blob data by using your custom domain, so long as they have hello appropriate permissions.</span></span>

## <a name="register-a-custom-domain-using-hello-asverify-subdomain"></a><span data-ttu-id="2480d-159">Hello를 사용 하 여 사용자 지정 도메인 등록 *asverify* 하위 도메인</span><span class="sxs-lookup"><span data-stu-id="2480d-159">Register a custom domain using hello *asverify* subdomain</span></span>
<span data-ttu-id="2480d-160">이 절차 tooregister를 사용 하 여 사용자 지정 도메인 사용자 지정 도메인으로 SLA 요구 하는 응용 프로그램에서 현재 지 원하는 경우 가동 중지 시간 없이 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-160">Use this procedure tooregister your custom domain if your custom domain is currently supporting an application with an SLA that requires that there be no downtime.</span></span> <span data-ttu-id="2480d-161">로 가리키는 CNAME를 만들면 여 `asverify.<subdomain>.<customdomain>` 너무`asverify.<storageaccount>.blob.core.windows.net`, Azure 사용한 도메인을 미리 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-161">By creating a CNAME that points from `asverify.<subdomain>.<customdomain>` too`asverify.<storageaccount>.blob.core.windows.net`, you can pre-register your domain with Azure.</span></span> <span data-ttu-id="2480d-162">시작 하는 두 번째 CNAME를 만들 수 있습니다 `<subdomain>.<customdomain>` 너무`<storageaccount>.blob.core.windows.net`, 이때 트래픽 tooyour 사용자 지정 도메인 tooyour 방향이 지정 된 blob 끝점 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-162">You can then create a second CNAME that points from `<subdomain>.<customdomain>` too`<storageaccount>.blob.core.windows.net`, at which point traffic tooyour custom domain will be directed tooyour blob endpoint.</span></span>

<span data-ttu-id="2480d-163">hello **asverify** 하위 도메인은 Azure에서 인식 되는 특별 한 하위 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-163">hello **asverify** subdomain is a special subdomain recognized by Azure.</span></span> <span data-ttu-id="2480d-164">앞에 추가 하 여 `asverify` tooyour 자체 하위 도메인을 허용 하면 Azure toorecognize 사용자 지정 도메인 hello 도메인에 대 한 hello DNS 레코드를 수정 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-164">By prepending `asverify` tooyour own subdomain, you permit Azure toorecognize your custom domain without modifying hello DNS record for hello domain.</span></span> <span data-ttu-id="2480d-165">Hello 도메인에 대 한 hello DNS 레코드를 수정 수행 하면 중단 시간 없이 매핑된 toohello blob 끝점 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-165">When you do modify hello DNS record for hello domain, it will be mapped toohello blob endpoint with no downtime.</span></span>

1. <span data-ttu-id="2480d-166">Hello에 tooyour 저장소 계정을 탐색 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-166">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="2480d-167">아래 **BLOB 서비스** hello 메뉴 블레이드에서 선택 **사용자 지정 도메인** tooopen hello *사용자 지정 도메인* 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-167">Under **BLOB SERVICE** on hello menu blade, select **Custom domain** tooopen hello *Custom domain* blade.</span></span>
1. <span data-ttu-id="2480d-168">Tooyour DNS 공급자의 웹 사이트에서 오류를 로깅하고 toohello DNS 관리 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-168">Log on tooyour DNS provider's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="2480d-169">**도메인 이름**, **DNS** 또는 **이름 서버 관리**와 같은 섹션에서 이를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-169">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
1. <span data-ttu-id="2480d-170">CNAMEs를 관리 하기 위한 hello 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-170">Find hello section for managing CNAMEs.</span></span> <span data-ttu-id="2480d-171">Toogo tooan 고급 설정 페이지를 hello 단어를 검색할 수도 있습니다 **CNAME**, **별칭**, 또는 **하위 도메인**합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-171">You may have toogo tooan advanced settings page and look for hello words **CNAME**, **Alias**, or **Subdomains**.</span></span>
1. <span data-ttu-id="2480d-172">새 CNAME 레코드를 만들고 hello를 포함 하는 하위 도메인 별칭을 제공 *asverify* 하위 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-172">Create a new CNAME record, and provide a subdomain alias that includes hello *asverify* subdomain.</span></span> <span data-ttu-id="2480d-173">예를 들어 **asverify.www** 또는 **asverify.photos**입니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-173">For example, **asverify.www** or **asverify.photos**.</span></span> <span data-ttu-id="2480d-174">그런 다음 hello 형태로 표시 하 여 Blob 서비스 끝점 호스트 이름, 제공 **asverify.mystorageaccount.blob.core.windows.net** (여기서 **mystorageaccount** hello 저장소 계정의 이름입니다).</span><span class="sxs-lookup"><span data-stu-id="2480d-174">Then provide a host name, which is your Blob service endpoint, in hello format **asverify.mystorageaccount.blob.core.windows.net** (where **mystorageaccount** is hello name of your storage account).</span></span> <span data-ttu-id="2480d-175">hello 호스트 이름 toouse hello의 항목 # 2에에서 표시 *사용자 지정 도메인* hello 블레이드 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-175">hello host name toouse appears in item #2 of hello *Custom domain* blade in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="2480d-176">Hello에 hello 텍스트 상자에서 *사용자 지정 도메인* hello 블레이드 [Azure 포털](https://portal.azure.com), hello hello 하위 도메인을 포함 하 여 사용자 지정 도메인 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-176">In hello text box on hello *Custom domain* blade in hello [Azure portal](https://portal.azure.com), enter hello name of your custom domain, including hello subdomain.</span></span> <span data-ttu-id="2480d-177">*asverify*를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-177">Do not include *asverify*.</span></span> <span data-ttu-id="2480d-178">예를 들어 도메인이 **contoso.com**이고 하위 도메인 별칭이 **www**이면 **www.contoso.com**을 입력합니다. 하위 도메인 경우 **사진**, 입력 **photos.contoso.com**. hello 하위 도메인이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-178">For example, if your domain is **contoso.com** and your subdomain alias is **www**, enter **www.contoso.com**. If your subdomain is **photos**, enter **photos.contoso.com**. hello subdomain is required.</span></span>
1. <span data-ttu-id="2480d-179">선택 hello **간접 CNAME 유효성 검사를 사용 하 여** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-179">Select hello **Use indirect CNAME validation** checkbox.</span></span>
1. <span data-ttu-id="2480d-180">선택 **저장** hello에 *사용자 지정 도메인* 블레이드 tooregister 사용자 지정 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-180">Select **Save** on hello *Custom domain* blade tooregister your custom domain.</span></span> <span data-ttu-id="2480d-181">Hello 등록에 성공 하면 저장소 계정의 성공적으로 업데이트 했는지 한다는 포털 알림 메시지를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-181">If hello registration is successful, you will see a portal notification stating that your storage account was successfully updated.</span></span> <span data-ttu-id="2480d-182">이 시점에서 Azure에 의해 확인 된 사용자 지정 도메인 관리 되지만 트래픽 tooyour 도메인을 아직 라우팅이 tooyour 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="2480d-182">At this point, your custom domain has been verified by Azure, but traffic tooyour domain is not yet being routed tooyour storage account.</span></span>
1. <span data-ttu-id="2480d-183">Tooyour DNS 공급자의 웹 사이트를 반환 하 고 하위 도메인 tooyour Blob 서비스 끝점을 매핑하는 다른 CNAME 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-183">Return tooyour DNS provider's website, and create another CNAME record that maps your subdomain tooyour Blob service endpoint.</span></span> <span data-ttu-id="2480d-184">예를 들어 hello 하위 도메인으로 지정 **www** 또는 **사진** (hello 없이 *asverify*), 호스트 이름으로 hello 및  **mystorageaccount.blob.core.windows.net** (여기서 **mystorageaccount** hello 저장소 계정의 이름입니다).</span><span class="sxs-lookup"><span data-stu-id="2480d-184">For example, specify hello subdomain as **www** or **photos** (without hello *asverify*), and hello hostname as **mystorageaccount.blob.core.windows.net** (where **mystorageaccount** is hello name of your storage account).</span></span> <span data-ttu-id="2480d-185">이 단계를 통해 사용자 지정 도메인의 hello 등록 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-185">With this step, hello registration of your custom domain is complete.</span></span>
1. <span data-ttu-id="2480d-186">마지막으로, 포함 하는 hello 만든 hello CNAME 레코드를 삭제할 수 있습니다 **asverify** 하위 도메인으로이 중간 단계로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-186">Finally, you can delete hello CNAME record you created containing hello **asverify** subdomain, as it was necessary only as an intermediary step.</span></span>

<span data-ttu-id="2480d-187">새 CNAME 레코드는 DNS를 통해 전파 된, 사용자가으로 hello 적절 한 사용 권한을 갖습니다 사용자 지정 도메인을 사용 하 여 blob 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-187">Once your new CNAME record has propagated through DNS, your users can view blob data by using your custom domain, so long as they have hello appropriate permissions.</span></span>

## <a name="test-your-custom-domain"></a><span data-ttu-id="2480d-188">사용자 지정 도메인 테스트</span><span class="sxs-lookup"><span data-stu-id="2480d-188">Test your custom domain</span></span>

<span data-ttu-id="2480d-189">사용자 지정 도메인은 tooconfirm tooyour Blob 서비스 끝점을 실제로 매핑된, 저장소 계정 내에서 공용 컨테이너에서 blob을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-189">tooconfirm your custom domain is indeed mapped tooyour Blob service endpoint, create a blob in a public container within your storage account.</span></span> <span data-ttu-id="2480d-190">그런 다음 웹 브라우저에서 hello 형식 tooaccess hello blob 뒤에 URI을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-190">Then, in a web browser, use a URI in hello following format tooaccess hello blob:</span></span>

`http://<subdomain.customdomain>/<mycontainer>/<myblob>`

<span data-ttu-id="2480d-191">예를 들어 다음 URI tooaccess hello에서 web form hello를 사용할 수 있습니다 **myforms** 컨테이너에서 hello **photos.contoso.com** 사용자 지정 하위 도메인:</span><span class="sxs-lookup"><span data-stu-id="2480d-191">For example, you might use hello following URI tooaccess a web form in hello **myforms** container in hello **photos.contoso.com** custom subdomain:</span></span>

`http://photos.contoso.com/myforms/applicationform.htm`

## <a name="deregister-a-custom-domain"></a><span data-ttu-id="2480d-192">사용자 지정 도메인 등록 취소</span><span class="sxs-lookup"><span data-stu-id="2480d-192">Deregister a custom domain</span></span>

<span data-ttu-id="2480d-193">Blob 저장소 끝점에 대 한 사용자 지정 도메인 tooderegister 다음 절차를 수행 하는 hello 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-193">tooderegister a custom domain for your Blob storage endpoint, use one of hello following procedures.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="2480d-194">Azure portal</span><span class="sxs-lookup"><span data-stu-id="2480d-194">Azure portal</span></span>

<span data-ttu-id="2480d-195">Hello Azure 포털 tooremove hello 사용자 지정 도메인 설정에 hello 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-195">Perform hello following in hello Azure portal tooremove hello custom domain setting:</span></span>

1. <span data-ttu-id="2480d-196">Hello에 tooyour 저장소 계정을 탐색 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-196">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="2480d-197">아래 **BLOB 서비스** hello 메뉴 블레이드에서 선택 **사용자 지정 도메인** tooopen hello *사용자 지정 도메인* 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-197">Under **BLOB SERVICE** on hello menu blade, select **Custom domain** tooopen hello *Custom domain* blade.</span></span>
1. <span data-ttu-id="2480d-198">사용자 지정 도메인 이름을 포함 하는 hello 텍스트 상자의 선택을 취소 hello 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-198">Clear hello contents of hello text box containing your custom domain name.</span></span>
1. <span data-ttu-id="2480d-199">선택 hello **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-199">Select hello **Save** button.</span></span>

<span data-ttu-id="2480d-200">사용자 지정 도메인 hello 성공적으로 제거 되 면 저장소 계정을 성공적으로 업데이트 했는지 한다는 포털 알림 메시지를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-200">When hello custom domain has been removed successfully, you will see a portal notification stating that your storage account was successfully updated.</span></span>

### <a name="azure-cli-20"></a><span data-ttu-id="2480d-201">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2480d-201">Azure CLI 2.0</span></span>

<span data-ttu-id="2480d-202">사용 하 여 hello [az 저장소 계정 업데이트](https://docs.microsoft.com/cli/azure/storage/account#update) CLI 명령 및 빈 문자열을 지정 (`""`) hello에 대 한 `--custom-domain` 인수 값 tooremove 사용자 지정 도메인 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-202">Use hello [az storage account update](https://docs.microsoft.com/cli/azure/storage/account#update) CLI command and specify an empty string (`""`) for hello `--custom-domain` argument value tooremove a custom domain registration.</span></span>

* <span data-ttu-id="2480d-203">명령 형식:</span><span class="sxs-lookup"><span data-stu-id="2480d-203">Command format:</span></span>

  ```azurecli
  az storage account update \
      --name <storage-account-name> \
      --resource-group <resource-group-name> \
      --custom-domain ""
  ```

* <span data-ttu-id="2480d-204">명령 예:</span><span class="sxs-lookup"><span data-stu-id="2480d-204">Command example:</span></span>

  ```azurecli
  az storage account update \
      --name mystorageaccount \
      --resource-group myresourcegroup \
      --custom-domain ""
  ```

### <a name="powershell"></a><span data-ttu-id="2480d-205">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2480d-205">PowerShell</span></span>

<span data-ttu-id="2480d-206">사용 하 여 hello [집합 AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) PowerShell cmdlet 빈 문자열을 지정 하 고 (`""`) hello에 대 한 `-CustomDomainName` 인수 값 tooremove 사용자 지정 도메인 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2480d-206">Use hello [Set-AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) PowerShell cmdlet and specify an empty string (`""`) for hello `-CustomDomainName` argument value tooremove a custom domain registration.</span></span>

* <span data-ttu-id="2480d-207">명령 형식:</span><span class="sxs-lookup"><span data-stu-id="2480d-207">Command format:</span></span>

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "<resource-group-name>" `
      -AccountName "<storage-account-name>" `
      -CustomDomainName ""
  ```

* <span data-ttu-id="2480d-208">명령 예:</span><span class="sxs-lookup"><span data-stu-id="2480d-208">Command example:</span></span>

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "myresourcegroup" `
      -AccountName "mystorageaccount" `
      -CustomDomainName ""
  ```

## <a name="next-steps"></a><span data-ttu-id="2480d-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2480d-209">Next steps</span></span>
* [<span data-ttu-id="2480d-210">사용자 지정 도메인 tooan Azure 콘텐츠 배달 네트워크 (CDN) 끝점 매핑</span><span class="sxs-lookup"><span data-stu-id="2480d-210">Map a custom domain tooan Azure Content Delivery Network (CDN) endpoint</span></span>](../../cdn/cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="2480d-211">HTTPS를 통해 사용자 지정 도메인에서 hello Azure CDN tooaccess blob 사용</span><span class="sxs-lookup"><span data-stu-id="2480d-211">Using hello Azure CDN tooaccess blobs with custom domains over HTTPS</span></span>](storage-https-custom-domain-cdn.md)
