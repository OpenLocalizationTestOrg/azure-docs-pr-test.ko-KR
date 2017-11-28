---
title: "웹 앱에 대 한 사용자 지정 DNS 레코드 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate 사용자 지정 도메인 DNS Azure DNS를 사용 하 여 웹 앱에 대 한 기록 합니다."
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
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="ccc9b-103">사용자 지정 도메인에서 웹앱에 대한 DNS 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="ccc9b-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="ccc9b-104">웹 앱에 대 한 Azure DNS toohost 사용자 지정 도메인을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-104">You can use Azure DNS toohost a custom domain for your web apps.</span></span> <span data-ttu-id="ccc9b-105">예를 들어 Azure 웹 앱을 만드는 하 고 사용자가 tooaccess 하려는 하거나 하 여 www.contoso.com 또는 contoso.com을 사용 하 여 FQDN으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-105">For example, you are creating an Azure web app and you want your users tooaccess it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="ccc9b-106">toodo이 toocreate 두 레코드가:</span><span class="sxs-lookup"><span data-stu-id="ccc9b-106">toodo this, you have toocreate two records:</span></span>

* <span data-ttu-id="ccc9b-107">"A" 루트 레코드 포인팅 toocontoso.com</span><span class="sxs-lookup"><span data-stu-id="ccc9b-107">A root "A" record pointing toocontoso.com</span></span>
* <span data-ttu-id="ccc9b-108">"CNAME" toohello 가리키는 hello www 이름에 대 한 기록 레코드</span><span class="sxs-lookup"><span data-stu-id="ccc9b-108">A "CNAME" record for hello www name that points toohello A record</span></span>

<span data-ttu-id="ccc9b-109">Azure에서 웹 앱에 대 한 A 레코드를 만든 경우 레코드를 수동으로 업데이트 해야 하는 hello hello 웹 응용 프로그램은 변경에 대 한 기본 IP 주소를 hello 염두에서에 둬야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-109">Keep in mind that if you create an A record for a web app in Azure, hello A record must be manually updated if hello underlying IP address for hello web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ccc9b-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="ccc9b-110">Before you begin</span></span>

<span data-ttu-id="ccc9b-111">시작 하기 전에 먼저 Azure DNS에서 DNS 영역을 생성 하며 hello 영역 프로그램 등록자 tooAzure DNS에에서 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate hello zone in your registrar tooAzure DNS.</span></span>

1. <span data-ttu-id="ccc9b-112">toocreate DNS 영역에서 다음과 같이 hello [DNS 영역을 만드는](dns-getstarted-create-dnszone.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-112">toocreate a DNS zone, follow hello steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="ccc9b-113">toodelegate 프로그램 DNS tooAzure DNS에서 다음과 같이 hello [DNS 도메인 위임](dns-domain-delegation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-113">toodelegate your DNS tooAzure DNS, follow hello steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="ccc9b-114">영역을 만드는 tooAzure DNS 위임 후, 사용자 지정 도메인에 대 한 다음 레코드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-114">After creating a zone and delegating it tooAzure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="ccc9b-115">1. 사용자 지정 도메인에 대한 A 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="ccc9b-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="ccc9b-116">A 레코드에 사용 되는 toomap 이름 tooits IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-116">An A record is used toomap a name tooits IP address.</span></span> <span data-ttu-id="ccc9b-117">다음 예제는 hello에 A 레코드 tooan IPv4 주소와 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-117">In hello following example we will assign @ as an A record tooan IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="ccc9b-118">1단계</span><span class="sxs-lookup"><span data-stu-id="ccc9b-118">Step 1</span></span>

<span data-ttu-id="ccc9b-119">A 레코드를 만들고 변수 $rs tooa 할당</span><span class="sxs-lookup"><span data-stu-id="ccc9b-119">Create an A record and assign tooa variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="ccc9b-120">2단계</span><span class="sxs-lookup"><span data-stu-id="ccc9b-120">Step 2</span></span>

<span data-ttu-id="ccc9b-121">Hello IPv4 값 이전에 만든 toohello 레코드 집합을 추가 합니다. "@" hello $rs 변수 할당을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-121">Add hello IPv4 value toohello previously created record set "@" using hello $rs variable assigned.</span></span> <span data-ttu-id="ccc9b-122">할당 된 IPv4 값 hello 웹 앱에 대 한 IP 주소 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-122">hello IPv4 value assigned will be hello IP address for your web app.</span></span>

<span data-ttu-id="ccc9b-123">웹 앱에 대 한 toofind hello IP 주소에서 다음과 같이 hello [Azure 앱 서비스에서 사용자 지정 도메인 이름을 구성](../app-service-web/app-service-web-tutorial-custom-domain.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-123">toofind hello IP address for a web app, follow hello steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="ccc9b-124">3단계</span><span class="sxs-lookup"><span data-stu-id="ccc9b-124">Step 3</span></span>

<span data-ttu-id="ccc9b-125">Hello 변경 toohello 레코드 집합을 커밋하십시오.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-125">Commit hello changes toohello record set.</span></span> <span data-ttu-id="ccc9b-126">사용 하 여 `Set-AzureRMDnsRecordSet` tooupload hello toohello 레코드 집합 tooAzure DNS를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-126">Use `Set-AzureRMDnsRecordSet` tooupload hello changes toohello record set tooAzure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="ccc9b-127">2. 사용자 지정 도메인에 대한 CNAME 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="ccc9b-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="ccc9b-128">도메인이 Azure DNS에서 이미 관리 되는 경우 (참조 [DNS 도메인 위임](dns-domain-delegation.md), hello 예제 toocreate contoso.azurewebsites.net에 대 한 CNAME 레코드를 따라 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use hello following hello example toocreate a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="ccc9b-129">1단계</span><span class="sxs-lookup"><span data-stu-id="ccc9b-129">Step 1</span></span>

<span data-ttu-id="ccc9b-130">PowerShell를 열고 새 CNAME 레코드 집합을 만든 tooa 변수 $rs 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-130">Open PowerShell and create a new CNAME record set and assign tooa variable $rs.</span></span> <span data-ttu-id="ccc9b-131">이 예제에서는 "시간의 toolive" 600 초 DNS 영역에 "contoso.com" 이라는 CNAME 레코드 집합 형식을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-131">This example will create a record set type CNAME with a "time toolive" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="ccc9b-132">다음 예제는 hello hello 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-132">hello following example is hello response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="ccc9b-133">2단계</span><span class="sxs-lookup"><span data-stu-id="ccc9b-133">Step 2</span></span>

<span data-ttu-id="ccc9b-134">Hello CNAME 레코드 집합을 만든 후 toocreate toohello 웹 앱에 가리키는 별칭 값 필요.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-134">Once hello CNAME record set is created, you need toocreate an alias value which will point toohello web app.</span></span>

<span data-ttu-id="ccc9b-135">이전에 "$rs" 변수를 할당 하는 hello를 사용 하 여 웹 응용 프로그램 contoso.azurewebsites.net hello에 대 한 toocreate hello 별칭 아래 hello PowerShell 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-135">Using hello previously assigned variable "$rs" you can use hello PowerShell command below toocreate hello alias for hello web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="ccc9b-136">다음 예제는 hello hello 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-136">hello following example is hello response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="ccc9b-137">3단계</span><span class="sxs-lookup"><span data-stu-id="ccc9b-137">Step 3</span></span>

<span data-ttu-id="ccc9b-138">Hello를 사용 하 여 hello 변경 내용 커밋 `Set-AzureRMDnsRecordSet` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ccc9b-138">Commit hello changes using hello `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="ccc9b-139">유효성을 검사할 수 hello 레코드가 올바르게 아래와 같이 hello "www.contoso.com" nslookup을 사용 하 여 쿼리를 통해 만들어진:</span><span class="sxs-lookup"><span data-stu-id="ccc9b-139">You can validate hello record was created correctly by querying hello "www.contoso.com" using nslookup, as shown below:</span></span>

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

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="ccc9b-140">웹앱에 대한 "awverify" 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="ccc9b-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="ccc9b-141">웹 앱에 대 한 toouse A 레코드를 결정 한 경우 있습니다 거쳐야 확인 프로세스 tooensure 있습니다 hello 고유의 사용자 지정 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-141">If you decide toouse an A record for your web app, you must go through a verification process tooensure you own hello custom domain.</span></span> <span data-ttu-id="ccc9b-142">이 검증 단계는 "awverify"라는 특수 CNAME 레코드를 만들어 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="ccc9b-143">이 섹션에는 tooA 레코드에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-143">This section applies tooA records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="ccc9b-144">1단계</span><span class="sxs-lookup"><span data-stu-id="ccc9b-144">Step 1</span></span>

<span data-ttu-id="ccc9b-145">Hello "awverify" 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-145">Create hello "awverify" record.</span></span> <span data-ttu-id="ccc9b-146">Hello 아래의 예제에서는 사용자 지정 도메인 hello에 대 한 contoso.com tooverify 소유권에 대 한 hello "aweverify" 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-146">In hello example below, we will create hello "aweverify" record for contoso.com tooverify ownership for hello custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="ccc9b-147">다음 예제는 hello hello 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-147">hello following example is hello response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="ccc9b-148">2단계</span><span class="sxs-lookup"><span data-stu-id="ccc9b-148">Step 2</span></span>

<span data-ttu-id="ccc9b-149">"Awverify" hello 레코드 집합을 만든 후 별칭 설정 hello CNAME 레코드를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-149">Once hello record set "awverify" is created, assign hello CNAME record set alias.</span></span> <span data-ttu-id="ccc9b-150">Hello 아래 예제에서는 우리는 hello CNAMe 레코드 집합 별칭 tooawverify.contoso.azurewebsites.net을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-150">In hello example below, we will assign hello CNAMe record set alias tooawverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="ccc9b-151">다음 예제는 hello hello 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-151">hello following example is hello response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="ccc9b-152">3단계</span><span class="sxs-lookup"><span data-stu-id="ccc9b-152">Step 3</span></span>

<span data-ttu-id="ccc9b-153">Hello를 사용 하 여 hello 변경 내용 커밋 `Set-AzureRMDnsRecordSet cmdlet`hello 명령 아래에 표시 된 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-153">Commit hello changes using hello `Set-AzureRMDnsRecordSet cmdlet`, as shown in hello command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="ccc9b-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ccc9b-154">Next steps</span></span>

<span data-ttu-id="ccc9b-155">Hello 단계에 따라 [응용 프로그램 서비스에 대 한 사용자 지정 도메인 이름 구성](../app-service-web/web-sites-custom-domain-name.md) tooconfigure 웹 앱 toouse 사용자 지정 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="ccc9b-155">Follow hello steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure your web app toouse a custom domain.</span></span>
