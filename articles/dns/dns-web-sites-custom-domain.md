---
title: "웹앱에 대한 사용자 지정 DNS 레코드 만들기 | Microsoft Docs"
description: "Azure DNS를 사용하여 웹앱에 대한 사용자 지정 도메인 DNS 레코드를 만드는 방법입니다."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: b054a41ecd69ee1c802d8403fe4b25128f016e3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="87459-103">사용자 지정 도메인에서 웹앱에 대한 DNS 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="87459-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="87459-104">Azure DNS를 사용하여 웹앱에 대한 사용자 지정 도메인을 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87459-104">You can use Azure DNS to host a custom domain for your web apps.</span></span> <span data-ttu-id="87459-105">예를 들어, Azure 웹앱을 만드는 중이며 사용자가 contoso.com 또는 www.contoso.com을 FQDN으로 사용하여 액세스하도록 설정하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-105">For example, you are creating an Azure web app and you want your users to access it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="87459-106">이렇게 하려면, 두 개의 레코드를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-106">To do this, you have to create two records:</span></span>

* <span data-ttu-id="87459-107">contoso.com을 가리키는 루트 "A" 레코드</span><span class="sxs-lookup"><span data-stu-id="87459-107">A root "A" record pointing to contoso.com</span></span>
* <span data-ttu-id="87459-108">A 레코드를 가리키는 www 이름에 대한 "CNAME" 레코드</span><span class="sxs-lookup"><span data-stu-id="87459-108">A "CNAME" record for the www name that points to the A record</span></span>

<span data-ttu-id="87459-109">Azure에서 웹앱에 대한 A 레코드를 만드는 경우 웹앱의 기본 IP 주소가 변경되면 A 레코드를 수동으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-109">Keep in mind that if you create an A record for a web app in Azure, the A record must be manually updated if the underlying IP address for the web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="87459-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="87459-110">Before you begin</span></span>

<span data-ttu-id="87459-111">시작하기 전에, 먼저 Azure DNS에서 DNS 영역을 만들고 등록 기관의 영역을 Azure DNS로 위임해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate the zone in your registrar to Azure DNS.</span></span>

1. <span data-ttu-id="87459-112">DNS 영역을 만들려면 [DNS 영역 만들기](dns-getstarted-create-dnszone.md)의 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-112">To create a DNS zone, follow the steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="87459-113">DNS를 Azure DNS로 위임하려면 [DNS domain delegation](dns-domain-delegation.md)(DNS 도메인 위임)의 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-113">To delegate your DNS to Azure DNS, follow the steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="87459-114">영역을 만들어서 Azure DNS에 위임한 후에는, 사용자 지정 도메인에 대한 레코드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87459-114">After creating a zone and delegating it to Azure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="87459-115">1. 사용자 지정 도메인에 대한 A 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="87459-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="87459-116">A 레코드는 이름을 해당 IP 주소에 매핑하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="87459-116">An A record is used to map a name to its IP address.</span></span> <span data-ttu-id="87459-117">다음 예제에서는 IPv4 주소에 @을 A 레코드로 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-117">In the following example we will assign @ as an A record to an IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="87459-118">1단계</span><span class="sxs-lookup"><span data-stu-id="87459-118">Step 1</span></span>

<span data-ttu-id="87459-119">A 레코드를 만들고 $rs 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-119">Create an A record and assign to a variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="87459-120">2단계</span><span class="sxs-lookup"><span data-stu-id="87459-120">Step 2</span></span>

<span data-ttu-id="87459-121">할당된 $rs 변수를 사용하여 이전에 만든 레코드 집합 "@"에 IPv4 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-121">Add the IPv4 value to the previously created record set "@" using the $rs variable assigned.</span></span> <span data-ttu-id="87459-122">할당된 IPv4 값은 웹앱의 IP 주소가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87459-122">The IPv4 value assigned will be the IP address for your web app.</span></span>

<span data-ttu-id="87459-123">웹앱의 IP 주소를 찾으려면 [Azure App Service에서 사용자 지정 도메인 이름 구성](../app-service-web/app-service-web-tutorial-custom-domain.md)의 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="87459-123">To find the IP address for a web app, follow the steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="87459-124">3단계</span><span class="sxs-lookup"><span data-stu-id="87459-124">Step 3</span></span>

<span data-ttu-id="87459-125">레코드 집합의 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-125">Commit the changes to the record set.</span></span> <span data-ttu-id="87459-126">`Set-AzureRMDnsRecordSet`를 사용하여 레코드 집합의 변경 내용을 Azure DNS로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-126">Use `Set-AzureRMDnsRecordSet` to upload the changes to the record set to Azure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="87459-127">2. 사용자 지정 도메인에 대한 CNAME 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="87459-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="87459-128">Azure DNS에서 이미 도메인을 관리하고 있는 경우( [DNS 도메인 위임](dns-domain-delegation.md)참조), 다음 예제를 사용하여 contoso.azurewebsites.net에 대한 CNAME 레코드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87459-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use the following the example to create a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="87459-129">1단계</span><span class="sxs-lookup"><span data-stu-id="87459-129">Step 1</span></span>

<span data-ttu-id="87459-130">PowerShell을 열고 새 CNAME 레코드 집합을 만든 다음 $rs 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-130">Open PowerShell and create a new CNAME record set and assign to a variable $rs.</span></span> <span data-ttu-id="87459-131">이 예제에서는 "contoso.com"이라는 DNS 영역에 "time to live"가 600초인 레코드 집합 형식 CNAME이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="87459-131">This example will create a record set type CNAME with a "time to live" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="87459-132">다음 예제는 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="87459-132">The following example is the response.</span></span>

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="87459-133">2단계</span><span class="sxs-lookup"><span data-stu-id="87459-133">Step 2</span></span>

<span data-ttu-id="87459-134">CNAME 레코드 집합을 만든 후에는 웹앱을 가리키는 별칭 값을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-134">Once the CNAME record set is created, you need to create an alias value which will point to the web app.</span></span>

<span data-ttu-id="87459-135">이전에 할당된 변수 "$rs"를 통해 아래 PowerShell 명령을 사용하여 웹앱 contoso.azurewebsites.net에 대한 별칭을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87459-135">Using the previously assigned variable "$rs" you can use the PowerShell command below to create the alias for the web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="87459-136">다음 예제는 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="87459-136">The following example is the response.</span></span>

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="87459-137">3단계</span><span class="sxs-lookup"><span data-stu-id="87459-137">Step 3</span></span>

<span data-ttu-id="87459-138">`Set-AzureRMDnsRecordSet` cmdlet을 사용하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-138">Commit the changes using the `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="87459-139">아래와 같이 nslookup으로 "www.contoso.com"을 쿼리하여 레코드가 올바르게 생성되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87459-139">You can validate the record was created correctly by querying the "www.contoso.com" using nslookup, as shown below:</span></span>

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="87459-140">웹앱에 대한 "awverify" 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="87459-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="87459-141">웹앱에 대해 A 레코드를 사용하려는 경우 사용자 지정 도메인의 소유자가 맞는지 확인하도록 검증 프로세스를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-141">If you decide to use an A record for your web app, you must go through a verification process to ensure you own the custom domain.</span></span> <span data-ttu-id="87459-142">이 검증 단계는 "awverify"라는 특수 CNAME 레코드를 만들어 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="87459-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="87459-143">이 섹션은 A 레코드에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="87459-143">This section applies to A records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="87459-144">1단계</span><span class="sxs-lookup"><span data-stu-id="87459-144">Step 1</span></span>

<span data-ttu-id="87459-145">"awverify" 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87459-145">Create the "awverify" record.</span></span> <span data-ttu-id="87459-146">아래 예제에서는 contoso.com에 대한 "awverify" 레코드를 만들어서 사용자 지정 도메인에 대한 소유권을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-146">In the example below, we will create the "aweverify" record for contoso.com to verify ownership for the custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="87459-147">다음 예제는 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="87459-147">The following example is the response.</span></span>

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="87459-148">2단계</span><span class="sxs-lookup"><span data-stu-id="87459-148">Step 2</span></span>

<span data-ttu-id="87459-149">"awverify" 레코드 집합이 생성되면, CNAME 레코드 집합 별칭을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-149">Once the record set "awverify" is created, assign the CNAME record set alias.</span></span> <span data-ttu-id="87459-150">아래 예제에서는 CNAME 레코드 집합 별칭을 awverify.contoso.azurewebsites.net에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-150">In the example below, we will assign the CNAMe record set alias to awverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="87459-151">다음 예제는 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="87459-151">The following example is the response.</span></span>

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="87459-152">3단계</span><span class="sxs-lookup"><span data-stu-id="87459-152">Step 3</span></span>

<span data-ttu-id="87459-153">아래 명령과 같이 `Set-AzureRMDnsRecordSet cmdlet`을 사용하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-153">Commit the changes using the `Set-AzureRMDnsRecordSet cmdlet`, as shown in the command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="87459-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="87459-154">Next steps</span></span>

<span data-ttu-id="87459-155">[Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) (앱 서비스에 대한 사용자 지정 도메인 이름 구성)의 단계에 따라 사용자 지정 도메인을 사용하도록 웹앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="87459-155">Follow the steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) to configure your web app to use a custom domain.</span></span>
