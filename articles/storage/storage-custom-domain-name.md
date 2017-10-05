---
title: "Azure Blob Storage 끝점에 대한 사용자 지정 도메인 이름 구성 | Microsoft Docs"
description: "Azure Portal을 사용하여 고유한 CNAME(정식 이름)을 Azure Storage 계정의 Blob Storage 끝점에 매핑합니다."
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
ms.openlocfilehash: 69e0713ab4221c51b89ec0f1ffedba8b6deea88c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-custom-domain-name-for-your-blob-storage-endpoint"></a><span data-ttu-id="38f4b-103">Blob 저장소 끝점에 대한 사용자 지정 도메인 이름 구성</span><span class="sxs-lookup"><span data-stu-id="38f4b-103">Configure a custom domain name for your Blob storage endpoint</span></span>

<span data-ttu-id="38f4b-104">Azure 저장소 계정에서 Blob 데이터에 액세스할 수 있도록 사용자 지정 도메인을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-104">You can configure a custom domain for accessing blob data in your Azure storage account.</span></span> <span data-ttu-id="38f4b-105">Blob 저장소의 기본 끝점은 `<storage-account-name>.blob.core.windows.net`입니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-105">The default endpoint for Blob storage is `<storage-account-name>.blob.core.windows.net`.</span></span> <span data-ttu-id="38f4b-106">**www.contoso.com**과 같은 사용자 지정 도메인 및 하위 도메인을 저장소 계정의 Blob 끝점에 매핑하면 사용자도 해당 도메인을 사용하여 저장소 계정의 Blob 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-106">If you map a custom domain and subdomain like **www.contoso.com** to the blob endpoint for your storage account, your users can then access blob data in your storage account using that domain.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38f4b-107">Azure Storage는 아직 기본적으로 사용자 지정 도메인으로 HTTPS를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-107">Azure Storage does not yet natively support HTTPS with custom domains.</span></span> <span data-ttu-id="38f4b-108">현재 [Azure CDN을 사용하여 HTTP를 통한 사용자 지정 도메인으로 Blob에 액세스](./storage-https-custom-domain-cdn.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-108">You can currently [Use the Azure CDN to access blobs with custom domains over HTTPS](./storage-https-custom-domain-cdn.md).</span></span>
>

<span data-ttu-id="38f4b-109">다음 표는 이름이 **mystorageaccount**인 저장소 계정에 있는 Blob 데이터에 액세스하기 위한 여러 샘플 URL을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-109">The following table shows a few sample URLs for blob data located in a storage account named **mystorageaccount**.</span></span> <span data-ttu-id="38f4b-110">저장소 계정에 등록된 사용자 지정 도메인은 **www.contoso.com**입니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-110">The custom domain registered for the storage account is **www.contoso.com**:</span></span>

| <span data-ttu-id="38f4b-111">리소스 종류</span><span class="sxs-lookup"><span data-stu-id="38f4b-111">Resource Type</span></span> | <span data-ttu-id="38f4b-112">기본 URL</span><span class="sxs-lookup"><span data-stu-id="38f4b-112">Default URL</span></span> | <span data-ttu-id="38f4b-113">사용자 지정 도메인 URL</span><span class="sxs-lookup"><span data-stu-id="38f4b-113">Custom domain URL</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38f4b-114">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="38f4b-114">Storage account</span></span> | <span data-ttu-id="38f4b-115">http://mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="38f4b-115">http://mystorageaccount.blob.core.windows.net</span></span> | <span data-ttu-id="38f4b-116">http://www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="38f4b-116">http://www.contoso.com</span></span> |
| <span data-ttu-id="38f4b-117">Blob</span><span class="sxs-lookup"><span data-stu-id="38f4b-117">Blob</span></span> |<span data-ttu-id="38f4b-118">http://mystorageaccount.blob.core.windows.net/mycontainer/myblob</span><span class="sxs-lookup"><span data-stu-id="38f4b-118">http://mystorageaccount.blob.core.windows.net/mycontainer/myblob</span></span> | <span data-ttu-id="38f4b-119">http://www.contoso.com/mycontainer/myblob</span><span class="sxs-lookup"><span data-stu-id="38f4b-119">http://www.contoso.com/mycontainer/myblob</span></span> |
| <span data-ttu-id="38f4b-120">루트 컨테이너</span><span class="sxs-lookup"><span data-stu-id="38f4b-120">Root container</span></span> | <span data-ttu-id="38f4b-121">http://mystorageaccount.blob.core.windows.net/myblob 또는 http://mystorageaccount.blob.core.windows.net/$root/myblob</span><span class="sxs-lookup"><span data-stu-id="38f4b-121">http://mystorageaccount.blob.core.windows.net/myblob or http://mystorageaccount.blob.core.windows.net/$root/myblob</span></span>| <span data-ttu-id="38f4b-122">http://www.contoso.com/myblob 또는 http://www.contoso.com/$root/myblob</span><span class="sxs-lookup"><span data-stu-id="38f4b-122">http://www.contoso.com/myblob or http://www.contoso.com/$root/myblob</span></span> |

## <a name="direct-vs-intermediary-domain-mapping"></a><span data-ttu-id="38f4b-123">직접 도메인 매핑과 중간 도메인 매핑</span><span class="sxs-lookup"><span data-stu-id="38f4b-123">Direct vs. intermediary domain mapping</span></span>

<span data-ttu-id="38f4b-124">저장소 계정의 Blob 끝점에 사용자 지정 도메인을 가리키는 방법에는 두 가지가 있으며 이는 직접 CNAME 매핑 방법과 *asverify* 중간 하위 도메인을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-124">There are two ways to point your custom domain to the blob endpoint for your storage account: direct CNAME mapping, and using the *asverify* intermediary subdomain.</span></span>

### <a name="direct-cname-mapping"></a><span data-ttu-id="38f4b-125">직접 CNAME 매핑</span><span class="sxs-lookup"><span data-stu-id="38f4b-125">Direct CNAME mapping</span></span>

<span data-ttu-id="38f4b-126">첫 번째 가장 단순한 방법은 사용자 지정 도메인 및 하위 도메인을 Blob 끝점에 직접 매핑하는 CNAME(정식 이름) 레코드를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-126">The first, and simplest, method is to create a canonical name (CNAME) record that maps your custom domain and subdomain directly to the blob endpoint.</span></span> <span data-ttu-id="38f4b-127">CNAME 레코드는 원본 도메인을 대상 도메인에 매핑하는 DNS(Domain Name System) 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-127">A CNAME record is a domain name system (DNS) feature that maps a source domain to a destination domain.</span></span> <span data-ttu-id="38f4b-128">이 경우 원본 도메인은 고유한 사용자 지정 도메인과 하위 도메인입니다(예: *www.contoso.com*).</span><span class="sxs-lookup"><span data-stu-id="38f4b-128">In this case, the source domain is your own custom domain and subdomain, for example *www.contoso.com*.</span></span> <span data-ttu-id="38f4b-129">대상 도메인은 Blob service 끝점입니다(예: *mystorageaccount.blob.core.windows.net*).</span><span class="sxs-lookup"><span data-stu-id="38f4b-129">The destination domain is your Blob service endpoint, for example *mystorageaccount.blob.core.windows.net*.</span></span>

<span data-ttu-id="38f4b-130">직접 매핑하는 방법은 [사용자 지정 도메인 등록](#register-a-custom-domain)에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-130">The direct method is covered in [Register a custom domain](#register-a-custom-domain).</span></span>

### <a name="intermediary-mapping-with-asverify"></a><span data-ttu-id="38f4b-131">*asverify*를 사용하여 중간 매핑</span><span class="sxs-lookup"><span data-stu-id="38f4b-131">Intermediary mapping with *asverify*</span></span>

<span data-ttu-id="38f4b-132">두 번째 방법 역시 CNAME 레코드를 사용하지만 Azure에서 인식하는 특수 하위 도메인 **asverify**를 사용하여 가동 중지 시간을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-132">The second method also uses CNAME records, but first employs a special subdomain recognized by Azure to avoid downtime: **asverify**.</span></span>

<span data-ttu-id="38f4b-133">사용자 지정 도메인을 Blob 끝점에 매핑하는 프로세스로 인해 [Azure Portal](https://portal.azure.com)에서 도메인을 등록하는 동안 도메인이 잠시 가동 중지될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-133">The process of mapping your custom domain to a blob endpoint can result in a brief period of downtime for the domain while you are registering it in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="38f4b-134">사용자 지정 도메인에서 가동 중지 시간이 0이어야 하는 SLA(서비스 수준 계약)가 설정된 응용 프로그램을 현재 지원하고 있다면 Azure *asverify* 하위 도메인을 중간 등록 단계로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-134">If your custom domain is currently supporting an application with a service-level agreement (SLA) that requires zero downtime, then you can use the Azure *asverify* subdomain as an intermediate registration step.</span></span> <span data-ttu-id="38f4b-135">이 중간 단계를 통해 DNS 매핑이 진행되는 동안 사용자가 도메인에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-135">This intermediate step ensures users are able to access your domain while the DNS mapping takes place.</span></span>

<span data-ttu-id="38f4b-136">중간 방법은 [*asverify* 하위 도메인을 사용하여 사용자 지정 도메인 등록](#register-a-custom-domain-using-the-asverify-subdomain)에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-136">The intermediary method is covered in [Register a custom domain using the *asverify* subdomain](#register-a-custom-domain-using-the-asverify-subdomain).</span></span>

## <a name="register-a-custom-domain"></a><span data-ttu-id="38f4b-137">사용자 지정 도메인 등록</span><span class="sxs-lookup"><span data-stu-id="38f4b-137">Register a custom domain</span></span>
<span data-ttu-id="38f4b-138">사용자가 도메인을 잠시 사용할 수 없더라도 괜찮은 경우나 사용자 지정 도메인에서 현재 응용 프로그램을 호스트하지 않는 경우에 이 절차에 따라 사용자 지정 도메인을 등록하세요.</span><span class="sxs-lookup"><span data-stu-id="38f4b-138">Use this procedure to register your custom domain if you have no concerns about the domain being briefly unavailable to your users, or if your custom domain is not currently hosting an application.</span></span>

<span data-ttu-id="38f4b-139">사용자 지정 도메인이 가동 중지 시간이 없어야 하는 응용 프로그램을 현재 지원하고 있다면 [*asverify* 하위 도메인을 사용하여 사용자 지정 도메인 등록](#register-a-custom-domain-using-the-asverify-subdomain)에서 설명한 절차를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="38f4b-139">If your custom domain is currently supporting an application that cannot have any downtime, follow the procedure outlined in [Register a custom domain using the *asverify* subdomain](#register-a-custom-domain-using-the-asverify-subdomain).</span></span>

<span data-ttu-id="38f4b-140">사용자 지정 도메인 이름을 구성하려면 DNS에서 새 CNAME 레코드를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-140">To configure a custom domain name, you must create a new CNAME record in DNS.</span></span> <span data-ttu-id="38f4b-141">CNAME 레코드에서 도메인 이름의 별칭을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-141">The CNAME record specifies an alias for a domain name.</span></span> <span data-ttu-id="38f4b-142">이 경우에는 사용자 지정 도메인의 주소를 저장소 계정의 Blob Storage 끝점에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-142">In this case, it maps the address of your custom domain to the Blob storage endpoint for your storage account.</span></span>

<span data-ttu-id="38f4b-143">일반적으로 도메인 등록 기관의 웹 사이트에서 도메인의 DNS 설정을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-143">Typically, you can manage your domain's DNS settings on your domain registrar's website.</span></span> <span data-ttu-id="38f4b-144">각 등록 기관은 서로 유사하면서 약간 다른 방법으로 CNAME 레코드를 지정하지만 개념은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-144">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concept is the same.</span></span> <span data-ttu-id="38f4b-145">일부 기본 도메인 등록 패키지에서 DNS 구성을 제공하지 않으므로 CNAME 레코드를 만들려면 먼저 도메인 등록 패키지를 업그레이드해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-145">Some basic domain registration packages do not offer DNS configuration, so you may need to upgrade your domain registration package before you can create the CNAME record.</span></span>

1. <span data-ttu-id="38f4b-146">[Azure Portal](https://portal.azure.com)의 저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-146">Navigate to your storage account in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="38f4b-147">메뉴 블레이드의 **BLOB SERVICE**에서 **사용자 지정 도메인**을 선택하여 *사용자 지정 도메인* 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-147">Under **BLOB SERVICE** on the menu blade, select **Custom domain** to open the *Custom domain* blade.</span></span>
1. <span data-ttu-id="38f4b-148">도메인 등록 기관의 웹 사이트에 로그온한 다음 DNS 관리 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-148">Log on to your domain registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="38f4b-149">**도메인 이름**, **DNS** 또는 **이름 서버 관리**와 같은 섹션에서 이를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-149">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
1. <span data-ttu-id="38f4b-150">CNAME을 관리하기 위한 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-150">Find the section for managing CNAMEs.</span></span> <span data-ttu-id="38f4b-151">고급 설정 페이지로 이동하여 **CNAME**, **별칭** 또는 **하위 도메인**과 같은 단어를 찾아야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-151">You may have to go to an advanced settings page and look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
1. <span data-ttu-id="38f4b-152">새 CNAME 레코드를 만들어 **www** 또는 **photos**와 같은 하위 도메인 별칭을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-152">Create a new CNAME record and provide a subdomain alias such as **www** or **photos**.</span></span> <span data-ttu-id="38f4b-153">그런 다음 Blob service 끝점인 호스트 이름을 **mystorageaccount.blob.core.windows.net** 형식으로 지정합니다. 여기에서 *mystorageaccount*는 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-153">Then provide a host name, which is your Blob service endpoint, in the format **mystorageaccount.blob.core.windows.net** (where *mystorageaccount* is the name of your storage account).</span></span> <span data-ttu-id="38f4b-154">사용할 호스트 이름은 [Azure Portal](https://portal.azure.com)에 *사용자 지정 도메인* 블레이드의 항목 #1에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-154">The host name to use appears in item #1 of the *Custom domain* blade in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="38f4b-155">[Azure Portal](https://portal.azure.com)에서 *사용자 지정 도메인* 블레이드의 텍스트 상자에 하위 도메인을 포함하여 사용자 지정 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-155">In the text box on the *Custom domain* blade in the [Azure portal](https://portal.azure.com), enter the name of your custom domain, including the subdomain.</span></span> <span data-ttu-id="38f4b-156">예를 들어 도메인이 **contoso.com**이고 하위 도메인 별칭이 **www**이면 **www.contoso.com**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-156">For example, if your domain is **contoso.com** and your subdomain alias is **www**, enter **www.contoso.com**.</span></span> <span data-ttu-id="38f4b-157">하위 도메인이 **photos**이면 **photos.contoso.com**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-157">If your subdomain is **photos**, enter **photos.contoso.com**.</span></span> <span data-ttu-id="38f4b-158">하위 도메인은 *필수*입니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-158">The subdomain is *required*.</span></span>
1. <span data-ttu-id="38f4b-159">*사용자 지정 도메인* 블레이드에서 **저장**을 선택하여 사용자 지정 도메인을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-159">Select **Save** on the *Custom domain* blade to register your custom domain.</span></span> <span data-ttu-id="38f4b-160">등록에 성공한 경우 저장소 계정이 성공적으로 업데이트되었음을 알리는 포털 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-160">If the registration is successful, you will see a portal notification that your storage account was successfully updated.</span></span>

<span data-ttu-id="38f4b-161">새 CNAME 레코드가 DNS를 통해 전파된 후 적절한 사용 권한이 있는 사용자는 사용자 지정 도메인을 사용하여 Blob 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-161">Once your new CNAME record has propagated through DNS, your users can view blob data by using your custom domain, so long as they have the appropriate permissions.</span></span>

## <a name="register-a-custom-domain-using-the-asverify-subdomain"></a><span data-ttu-id="38f4b-162">*asverify* 하위 도메인을 사용하여 사용자 지정 도메인 등록</span><span class="sxs-lookup"><span data-stu-id="38f4b-162">Register a custom domain using the *asverify* subdomain</span></span>
<span data-ttu-id="38f4b-163">사용자 지정 도메인이 가동 중지 시간이 없어야 하는 SLA가 있는 응용 프로그램을 현재 지원하고 있는 경우 이 절차에 따라 사용자 지정 도메인을 등록하세요.</span><span class="sxs-lookup"><span data-stu-id="38f4b-163">Use this procedure to register your custom domain if your custom domain is currently supporting an application with an SLA that requires that there be no downtime.</span></span> <span data-ttu-id="38f4b-164">`asverify.<subdomain>.<customdomain>`에서 `asverify.<storageaccount>.blob.core.windows.net`을 가리키는 CNAME을 만들어 Azure에 도메인을 미리 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-164">By creating a CNAME that points from `asverify.<subdomain>.<customdomain>` to `asverify.<storageaccount>.blob.core.windows.net`, you can pre-register your domain with Azure.</span></span> <span data-ttu-id="38f4b-165">그런 다음 `<subdomain>.<customdomain>`에서 `<storageaccount>.blob.core.windows.net`을 가리키는 두 번째 CNAME을 만들 수 있습니다. 그러면 사용자 지정 도메인에 대한 지점 트래픽이 Blob 끝점으로 직접 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-165">You can then create a second CNAME that points from `<subdomain>.<customdomain>` to `<storageaccount>.blob.core.windows.net`, at which point traffic to your custom domain will be directed to your blob endpoint.</span></span>

<span data-ttu-id="38f4b-166">**asverify** 하위 도메인은 Azure에서 인식하는 특수한 하위 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-166">The **asverify** subdomain is a special subdomain recognized by Azure.</span></span> <span data-ttu-id="38f4b-167">고유한 하위 도메인 앞에 `asverify`를 추가하면 도메인의 DNS 레코드를 수정하지 않아도 Azure에서 사용자 지정 도메인을 인식할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-167">By prepending `asverify` to your own subdomain, you permit Azure to recognize your custom domain without modifying the DNS record for the domain.</span></span> <span data-ttu-id="38f4b-168">도메인의 DNS 레코드를 수정하면 가동 중지 시간 없이 Blob 끝점에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-168">When you do modify the DNS record for the domain, it will be mapped to the blob endpoint with no downtime.</span></span>

1. <span data-ttu-id="38f4b-169">[Azure Portal](https://portal.azure.com)의 저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-169">Navigate to your storage account in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="38f4b-170">메뉴 블레이드의 **BLOB SERVICE**에서 **사용자 지정 도메인**을 선택하여 *사용자 지정 도메인* 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-170">Under **BLOB SERVICE** on the menu blade, select **Custom domain** to open the *Custom domain* blade.</span></span>
1. <span data-ttu-id="38f4b-171">DNS 공급자의 웹 사이트에 로그온한 다음 DNS 관리 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-171">Log on to your DNS provider's website and go to the page for managing DNS.</span></span> <span data-ttu-id="38f4b-172">**도메인 이름**, **DNS** 또는 **이름 서버 관리**와 같은 섹션에서 이를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-172">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
1. <span data-ttu-id="38f4b-173">CNAME을 관리하기 위한 섹션을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-173">Find the section for managing CNAMEs.</span></span> <span data-ttu-id="38f4b-174">고급 설정 페이지로 이동하여 **CNAME**, **별칭** 또는 **하위 도메인**과 같은 단어를 찾아야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-174">You may have to go to an advanced settings page and look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
1. <span data-ttu-id="38f4b-175">새 CNAME 레코드를 만들어 *asverify* 하위 도메인을 포함한 하위 도메인 별칭을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-175">Create a new CNAME record, and provide a subdomain alias that includes the *asverify* subdomain.</span></span> <span data-ttu-id="38f4b-176">예를 들어 **asverify.www** 또는 **asverify.photos**입니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-176">For example, **asverify.www** or **asverify.photos**.</span></span> <span data-ttu-id="38f4b-177">그런 다음 Blob service 끝점인 호스트 이름을 **asverify.mystorageaccount.blob.core.windows.net** 형식으로 지정합니다. 여기에서 **mystorageaccount**는 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-177">Then provide a host name, which is your Blob service endpoint, in the format **asverify.mystorageaccount.blob.core.windows.net** (where **mystorageaccount** is the name of your storage account).</span></span> <span data-ttu-id="38f4b-178">사용할 호스트 이름이 [Azure Portal](https://portal.azure.com)에서 *사용자 지정 도메인* 블레이드의 항목 #2에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-178">The host name to use appears in item #2 of the *Custom domain* blade in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="38f4b-179">[Azure Portal](https://portal.azure.com)에서 *사용자 지정 도메인* 블레이드의 텍스트 상자에 하위 도메인을 포함하여 사용자 지정 도메인 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-179">In the text box on the *Custom domain* blade in the [Azure portal](https://portal.azure.com), enter the name of your custom domain, including the subdomain.</span></span> <span data-ttu-id="38f4b-180">*asverify*를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-180">Do not include *asverify*.</span></span> <span data-ttu-id="38f4b-181">예를 들어 도메인이 **contoso.com**이고 하위 도메인 별칭이 **www**이면 **www.contoso.com**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-181">For example, if your domain is **contoso.com** and your subdomain alias is **www**, enter **www.contoso.com**.</span></span> <span data-ttu-id="38f4b-182">하위 도메인이 **photos**이면 **photos.contoso.com**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-182">If your subdomain is **photos**, enter **photos.contoso.com**.</span></span> <span data-ttu-id="38f4b-183">하위 도메인은 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-183">The subdomain is required.</span></span>
1. <span data-ttu-id="38f4b-184">**간접 CNAME 유효성 검사 사용** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-184">Select the **Use indirect CNAME validation** checkbox.</span></span>
1. <span data-ttu-id="38f4b-185">*사용자 지정 도메인* 블레이드에서 **저장**을 선택하여 사용자 지정 도메인을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-185">Select **Save** on the *Custom domain* blade to register your custom domain.</span></span> <span data-ttu-id="38f4b-186">등록에 성공한 경우 저장소 계정이 성공적으로 업데이트되었음을 알리는 포털 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-186">If the registration is successful, you will see a portal notification stating that your storage account was successfully updated.</span></span> <span data-ttu-id="38f4b-187">이제 사용자 지정 도메인이 Azure에서 확인되었지만 도메인에 대한 트래픽은 아직 저장소 계정으로 라우팅되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-187">At this point, your custom domain has been verified by Azure, but traffic to your domain is not yet being routed to your storage account.</span></span>
1. <span data-ttu-id="38f4b-188">DNS 공급자의 웹 사이트로 돌아가 하위 도메인을 Blob service 끝점에 매핑한 CNAME 레코드를 하나 더 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-188">Return to your DNS provider's website, and create another CNAME record that maps your subdomain to your Blob service endpoint.</span></span> <span data-ttu-id="38f4b-189">예를 들어 하위 도메인을 **www** 또는 **photos**(*asverify* 없이)로 지정하고 호스트 이름을 **mystorageaccount.blob.core.windows.net**으로 지정합니다. 여기서 **mystorageaccount**는 저장소 계정의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-189">For example, specify the subdomain as **www** or **photos** (without the *asverify*), and the hostname as **mystorageaccount.blob.core.windows.net** (where **mystorageaccount** is the name of your storage account).</span></span> <span data-ttu-id="38f4b-190">이 단계에서 사용자 지정 도메인 등록이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-190">With this step, the registration of your custom domain is complete.</span></span>
1. <span data-ttu-id="38f4b-191">마지막으로 **asverify** 하위 도메인을 포함하여 만든 CNAME 레코드는 중간 단계로만 필요하므로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-191">Finally, you can delete the CNAME record you created containing the **asverify** subdomain, as it was necessary only as an intermediary step.</span></span>

<span data-ttu-id="38f4b-192">새 CNAME 레코드가 DNS를 통해 전파된 후 적절한 사용 권한이 있는 사용자는 사용자 지정 도메인을 사용하여 Blob 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-192">Once your new CNAME record has propagated through DNS, your users can view blob data by using your custom domain, so long as they have the appropriate permissions.</span></span>

## <a name="test-your-custom-domain"></a><span data-ttu-id="38f4b-193">사용자 지정 도메인 테스트</span><span class="sxs-lookup"><span data-stu-id="38f4b-193">Test your custom domain</span></span>

<span data-ttu-id="38f4b-194">사용자 지정 도메인이 Blob service 끝점에 실제로 매핑되었는지 확인하려면 저장소 계정 내의 공용 컨테이너에 Blob을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-194">To confirm your custom domain is indeed mapped to your Blob service endpoint, create a blob in a public container within your storage account.</span></span> <span data-ttu-id="38f4b-195">그런 다음 웹 브라우저에서 다음 형식의 URI를 사용하여 Blob에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-195">Then, in a web browser, use a URI in the following format to access the blob:</span></span>

`http://<subdomain.customdomain>/<mycontainer>/<myblob>`

<span data-ttu-id="38f4b-196">예를 들어 다음 URI를 사용하여 **photos.contoso.com** 사용자 지정 하위 도메인의 **myforms** 컨테이너에 대한 웹 양식에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-196">For example, you might use the following URI to access a web form in the **myforms** container in the **photos.contoso.com** custom subdomain:</span></span>

`http://photos.contoso.com/myforms/applicationform.htm`

## <a name="deregister-a-custom-domain"></a><span data-ttu-id="38f4b-197">사용자 지정 도메인 등록 취소</span><span class="sxs-lookup"><span data-stu-id="38f4b-197">Deregister a custom domain</span></span>

<span data-ttu-id="38f4b-198">Blob Storage 끝점에 대한 사용자 지정 도메인 등록을 취소하려면 다음 절차 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-198">To deregister a custom domain for your Blob storage endpoint, use one of the following procedures.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="38f4b-199">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="38f4b-199">Azure portal</span></span>

<span data-ttu-id="38f4b-200">Azure Portal에서 다음을 수행하여 사용자 지정 도메인 설정을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-200">Perform the following in the Azure portal to remove the custom domain setting:</span></span>

1. <span data-ttu-id="38f4b-201">[Azure Portal](https://portal.azure.com)의 저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-201">Navigate to your storage account in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="38f4b-202">메뉴 블레이드의 **BLOB SERVICE**에서 **사용자 지정 도메인**을 선택하여 *사용자 지정 도메인* 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-202">Under **BLOB SERVICE** on the menu blade, select **Custom domain** to open the *Custom domain* blade.</span></span>
1. <span data-ttu-id="38f4b-203">사용자 지정 도메인 이름이 포함된 텍스트 상자의 콘텐츠를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-203">Clear the contents of the text box containing your custom domain name.</span></span>
1. <span data-ttu-id="38f4b-204">**저장** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-204">Select the **Save** button.</span></span>

<span data-ttu-id="38f4b-205">사용자 지정 도메인이 성공적으로 제거된 경우 저장소 계정이 성공적으로 업데이트되었음을 알리는 포털 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-205">When the custom domain has been removed successfully, you will see a portal notification stating that your storage account was successfully updated.</span></span>

### <a name="azure-cli-20"></a><span data-ttu-id="38f4b-206">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="38f4b-206">Azure CLI 2.0</span></span>

<span data-ttu-id="38f4b-207">[az storage account update](https://docs.microsoft.com/cli/azure/storage/account#update) CLI 명령을 사용하고 `--custom-domain` 인수 값에 빈 문자열(`""`)을 지정하여 사용자 지정 도메인 등록을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-207">Use the [az storage account update](https://docs.microsoft.com/cli/azure/storage/account#update) CLI command and specify an empty string (`""`) for the `--custom-domain` argument value to remove a custom domain registration.</span></span>

* <span data-ttu-id="38f4b-208">명령 형식:</span><span class="sxs-lookup"><span data-stu-id="38f4b-208">Command format:</span></span>

  ```azurecli
  az storage account update \
      --name <storage-account-name> \
      --resource-group <resource-group-name> \
      --custom-domain ""
  ```

* <span data-ttu-id="38f4b-209">명령 예:</span><span class="sxs-lookup"><span data-stu-id="38f4b-209">Command example:</span></span>

  ```azurecli
  az storage account update \
      --name mystorageaccount \
      --resource-group myresourcegroup \
      --custom-domain ""
  ```

### <a name="powershell"></a><span data-ttu-id="38f4b-210">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38f4b-210">PowerShell</span></span>

<span data-ttu-id="38f4b-211">[Set-AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) PowerShell cmdlet을 사용하고 `-CustomDomainName` 인수 값에 빈 문자열(`""`)을 지정하여 사용자 지정 도메인 등록을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="38f4b-211">Use the [Set-AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) PowerShell cmdlet and specify an empty string (`""`) for the `-CustomDomainName` argument value to remove a custom domain registration.</span></span>

* <span data-ttu-id="38f4b-212">명령 형식:</span><span class="sxs-lookup"><span data-stu-id="38f4b-212">Command format:</span></span>

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "<resource-group-name>" `
      -AccountName "<storage-account-name>" `
      -CustomDomainName ""
  ```

* <span data-ttu-id="38f4b-213">명령 예:</span><span class="sxs-lookup"><span data-stu-id="38f4b-213">Command example:</span></span>

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "myresourcegroup" `
      -AccountName "mystorageaccount" `
      -CustomDomainName ""
  ```

## <a name="next-steps"></a><span data-ttu-id="38f4b-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="38f4b-214">Next steps</span></span>
* [<span data-ttu-id="38f4b-215">사용자 지정 도메인을 Azure CDN(Content Delivery Network) 끝점에 매핑</span><span class="sxs-lookup"><span data-stu-id="38f4b-215">Map a custom domain to an Azure Content Delivery Network (CDN) endpoint</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="38f4b-216">Azure CDN을 사용하여 HTTPS를 통한 사용자 지정 도메인으로 Blob 액세스</span><span class="sxs-lookup"><span data-stu-id="38f4b-216">Using the Azure CDN to access blobs with custom domains over HTTPS</span></span>](./storage-https-custom-domain-cdn.md)
