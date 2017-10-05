---
title: "Azure PowerShell을 사용하여 Azure DNS의 DNS 레코드 관리 | Microsoft Docs"
description: "Azure DNS에서 도메인을 호스트하는 경우 Azure DNS에서 DNS 레코드 집합 및 레코드를 관리합니다. 레코드 집합 및 레코드 작업에 대한 모든 PowerShell 명령입니다."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: 2962e30e5d9c60b8e786e2ba79647cabfc5925cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="bdfb9-104">Azure PowerShell을 사용하여 Azure DNS에서 DNS 레코드 및 레코드 집합 관리</span><span class="sxs-lookup"><span data-stu-id="bdfb9-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bdfb9-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="bdfb9-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="bdfb9-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bdfb9-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="bdfb9-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bdfb9-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="bdfb9-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bdfb9-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="bdfb9-109">이 문서는 Azure PowerShell을 사용하여 DNS 영역에 대한 DNS 레코드를 관리하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-109">This article shows you how to manage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="bdfb9-110">크로스 플랫폼인 [Azure CLI](dns-operations-recordsets-cli.md) 또는 [Azure Portal](dns-operations-recordsets-portal.md)을 사용하여 DNS 레코드를 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-110">DNS records can also be managed by using the cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="bdfb9-111">이 문서의 예제에서는 이미 [Azure PowerShell을 설치했고, 로그인했고, DNS 영역을 만들었다](dns-operations-dnszones.md)고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-111">The examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="bdfb9-112">소개</span><span class="sxs-lookup"><span data-stu-id="bdfb9-112">Introduction</span></span>

<span data-ttu-id="bdfb9-113">Azure DNS에 DNS 레코드를 만들기 전에 먼저 Azure DNS에서 DNS 레코드를 DNS 레코드 집합으로 구성하는 방법을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-113">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="bdfb9-114">Azure DNS의 DNS 레코드에 대한 자세한 내용은 [DNS 영역 및 레코드](dns-zones-records.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="bdfb9-115">새 DNS 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="bdfb9-115">Create a new DNS record</span></span>

<span data-ttu-id="bdfb9-116">새 레코드가 기존 레코드와 이름 및 형식이 똑같은 경우 [기존 레코드 집합에 추가](#add-a-record-to-an-existing-record-set)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-116">If your new record has the same name and type as an existing record, you need to [add it to the existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="bdfb9-117">새 레코드가 기존 레코드와 이름 및 형식이 다른 경우 새 레코드 집합을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-117">If your new record has a different name and type to all existing records, you need to create a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="bdfb9-118">새 레코드 집합에서 ‘A’ 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="bdfb9-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="bdfb9-119">`New-AzureRmDnsRecordSet` cmdlet을 사용하여 레코드 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-119">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="bdfb9-120">레코드 집합을 만들 때, 레코드 집합 이름, 영역, TTL(Time-to-Live), 레코드 형식 및 만들 레코드를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-120">When creating a record set, you need to specify the record set name, the zone, the time to live (TTL), the record type, and the records to be created.</span></span>

<span data-ttu-id="bdfb9-121">레코드 집합에 레코드를 추가하기 위한 매개 변수는 레코드 집합 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-121">The parameters for adding records to a record set vary depending on the type of the record set.</span></span> <span data-ttu-id="bdfb9-122">예를 들어 'A' 형식의 레코드 집합을 사용하는 경우 `-IPv4Address` 매개 변수를 사용하여 IP 주소를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-122">For example, when using a record set of type 'A', you need to specify the IP address using the parameter `-IPv4Address`.</span></span> <span data-ttu-id="bdfb9-123">다른 레코드 형식에 다른 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="bdfb9-124">자세한 내용은 [추가 레코드 형식 예제](#additional-record-type-examples)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="bdfb9-125">다음 예제에서는 DNS 영역 'contoso.com'에 상대적 이름 'www'가 포함된 레코드 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-125">The following example creates a record set with the relative name 'www' in the DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="bdfb9-126">레코드의 정규화된 이름은 'www.contoso.com'입니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-126">The fully-qualified name of the record set is 'www.contoso.com'.</span></span> <span data-ttu-id="bdfb9-127">레코드 형식은 'A'이고 TTL은 3600초입니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-127">The record type is 'A', and the TTL is 3600 seconds.</span></span> <span data-ttu-id="bdfb9-128">레코드 집합은 '1.2.3.4' IP 주소를 가진 단일 레코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-128">The record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="bdfb9-129">영역의 'apex'에서 레코드 집합을 만들려면(이 경우 'contoso.com'), 따옴표를 포함한 레코드 집합 이름 '@'를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-129">To create a record set at the 'apex' of a zone (in this case, 'contoso.com'), use the record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="bdfb9-130">둘 이상의 레코드를 포함하는 레코드 집합을 만들어야 하는 경우 먼저 로컬 배열을 만들고 레코드를 추가한 후에 다음과 같이 `New-AzureRmDnsRecordSet`에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-130">If you need to create a record set containing more than one record, first create a local array and add the records, then pass the array to `New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="bdfb9-131">[레코드 집합 메타데이터](dns-zones-records.md#tags-and-metadata)는 키-값 쌍의 형태로 각 레코드 집합과 응용 프로그램 특정 데이터를 연결하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="bdfb9-132">다음 예제에서는 "dept=finance" 및 "environment=production"라는 두 개의 메타데이터 항목을 가진 레코드 집합을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-132">The following example shows how to create a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="bdfb9-133">Azure DNS는 DNS 레코드를 만들기 전에 DNS 이름을 예약하는 자리 표시자 역할을 수행할 수 있는 '빈' 레코드 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="bdfb9-134">빈 레코드 집합은 Azure DNS 제어 평면에 표시되어 있지만 Azure DNS 이름 서버에도 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-134">Empty record sets are visible in the Azure DNS control plane, but do appear on the Azure DNS name servers.</span></span> <span data-ttu-id="bdfb9-135">아래 예제에서는 빈 레코드 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-135">The following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="bdfb9-136">다른 형식의 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="bdfb9-136">Create records of other types</span></span>

<span data-ttu-id="bdfb9-137">지금까지 'A' 레코드를 만드는 방법에 대해 자세히 살펴보았으며, 다음 예제에서는 Azure DNS에서 지원하는 다른 레코드 형식의 레코드를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-137">Having seen in detail how to create 'A' records, the following examples show how to create records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="bdfb9-138">각각의 경우에 단일 레코드를 포함하는 레코드 집합을 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-138">In each case, we show how to create a record set containing a single record.</span></span> <span data-ttu-id="bdfb9-139">'A' 레코드에 대한 이전 예제는 메타데이터와 여러 레코드를 포함하는 다른 형식의 레코드 집합을 만들거나 빈 레코드 집합을 만드는 데 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-139">The earlier examples for 'A' records can be adapted to create record sets of other types containing multiple records, with metadata, or to create empty record sets.</span></span>

<span data-ttu-id="bdfb9-140">SOA가 각 DNS 영역과 함께 만들어지고 삭제되며 별도로 만들어지거나 삭제될 수 없기 때문에 SOA 레코드 집합을 만드는 예제를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-140">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="bdfb9-141">그러나 [뒷부분의 예제에 표시된 대로 SOA를 수정할 수 있습니다](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="bdfb9-141">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="bdfb9-142">단일 레코드가 포함된 AAAA 레코드 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="bdfb9-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="bdfb9-143">단일 레코드가 포함된 CNAME 레코드 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="bdfb9-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="bdfb9-144">DNS 표준은 영역의 apex(`-Name '@'`)에서 CNAME 레코드를 허용하거나 둘 이상의 레코드를 포함하는 레코드 집합을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-144">The DNS standards do not permit CNAME records at the apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="bdfb9-145">자세한 내용은 [CNAME 레코드](dns-zones-records.md#cname-records)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="bdfb9-146">단일 레코드가 포함된 MX 레코드 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="bdfb9-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="bdfb9-147">이 예제에서는 레코드 집합 이름을 '@'로 사용하여 영역 구로에 MX 레코드를 만듭니다(이 경우 'contoso.com').</span><span class="sxs-lookup"><span data-stu-id="bdfb9-147">In this example, we use the record set name '@' to create an MX record at the zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="bdfb9-148">단일 레코드가 포함된 NS 레코드 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="bdfb9-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="bdfb9-149">단일 레코드가 포함된 PTR 레코드 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="bdfb9-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="bdfb9-150">이 경우에 'my-arpa-zone.com'은 IP 범위를 나타내는 ARPA 역방향 조회 영역을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-150">In this case, 'my-arpa-zone.com' represents the ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="bdfb9-151">이 영역의 각 PTR 레코드 집합은 IP 범위 내의 IP 주소에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-151">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span> <span data-ttu-id="bdfb9-152">레코드 이름 '10'은 이 레코드에서 나타내는 이 IP 범위 내에서 IP 주소의 마지막 옥텟입니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-152">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="bdfb9-153">단일 레코드가 포함된 SRV 레코드 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="bdfb9-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="bdfb9-154">[SRV 레코드 집합](dns-zones-records.md#srv-records)을 만들 경우 레코드 집합 이름에 *\_서비스* 및 *\_프로토콜*을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="bdfb9-155">영역 apex에 SRV 레코드 집합을 만드는 경우 레코드 집합 이름에서 '@'를 포함할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-155">There is no need to include '@' in the record set name when creating an SRV record set at the zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="bdfb9-156">단일 레코드가 포함된 TXT 레코드 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="bdfb9-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="bdfb9-157">다음 예제에서는 TXT 레코드를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-157">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="bdfb9-158">TXT 레코드에서 지원되는 최대 문자열 길이에 대한 자세한 내용은 [TXT 레코드](dns-zones-records.md#txt-records)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-158">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="bdfb9-159">레코드 집합 가져오기</span><span class="sxs-lookup"><span data-stu-id="bdfb9-159">Get a record set</span></span>

<span data-ttu-id="bdfb9-160">기존 레코드 집합을 가져오려면, `Get-AzureRmDnsRecordSet`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-160">To retrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="bdfb9-161">이 cmdlet은 Azure DNS에서 레코드 집합을 나타내는 로컬 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-161">This cmdlet returns a local object that represents the record set in Azure DNS.</span></span>

<span data-ttu-id="bdfb9-162">`New-AzureRmDnsRecordSet`와 마찬가지로, 레코드 집합 이름은 *상대* 이름이어야 합니다. 즉, 영역 이름을 제외해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-162">As with `New-AzureRmDnsRecordSet`, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="bdfb9-163">레코드 형식 및 레코드 집합을 포함하는 영역을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-163">You also need to specify the record type, and the zone containing the record set.</span></span>

<span data-ttu-id="bdfb9-164">다음 예제에서는 레코드 집합을 검색하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-164">The following example shows how to retrieve a record set.</span></span> <span data-ttu-id="bdfb9-165">이 예제에서는 `-ZoneName` 및 `-ResourceGroupName` 매개 변수를 사용하여 영역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-165">In this example, the zone is specified using the `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="bdfb9-166">또는 `-Zone` 매개 변수를 사용하여 전달된 영역 개체를 사용하는 영역도 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-166">Alternatively, you can also specify the zone using a zone object, passed using the `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="bdfb9-167">레코드 집합 나열</span><span class="sxs-lookup"><span data-stu-id="bdfb9-167">List record sets</span></span>

<span data-ttu-id="bdfb9-168">`-Name` 및/또는 `-RecordType` 매개 변수를 생략하여 영역에 있는 레코드 집합을 나열하도록 `Get-AzureRmDnsZone`을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-168">You can also use `Get-AzureRmDnsZone` to list record sets in a zone, by omitting the `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="bdfb9-169">다음 예제에서는 영역에 있는 모든 레코드 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-169">The following example returns all record sets in the zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="bdfb9-170">다음 예제에서는 레코드 집합 이름을 생략하는 동시에 레코드 형식을 지정하여 모든 지정된 형식의 레코드 집합을 검색할 수 있는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-170">The following example shows how all record sets of a given type can be retrieved by specifying the record type while omitting the record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="bdfb9-171">레코드 형식에서 지정된 이름의 모든 레코드 집합을 검색하려면 모든 레코드 집합을 검색한 다음 결과를 필터링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-171">To retrieve all record sets with a given name, across record types, you need to retrieve all record sets and then filter the results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="bdfb9-172">위의 모든 예제에서 영역은 `-ZoneName` 및 `-ResourceGroupName` 매개 변수를 사용하거나 영역 개체를 지정하여 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-172">In all the above examples, the zone can be specified either by using the `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="bdfb9-173">기존 레코드 집합에 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="bdfb9-173">Add a record to an existing record set</span></span>

<span data-ttu-id="bdfb9-174">기존 레코드 집합에 레코드를 추가하려면 다음 세 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-174">To add a record to an existing record set, follow the following three steps:</span></span>

1. <span data-ttu-id="bdfb9-175">기존 레코드 집합 가져오기</span><span class="sxs-lookup"><span data-stu-id="bdfb9-175">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="bdfb9-176">로컬 레코드 집합에 새 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="bdfb9-176">Add the new record to the local record set.</span></span> <span data-ttu-id="bdfb9-177">이 작업은 오프라인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="bdfb9-178">Azure DNS 서비스에 변경 내용 커밋</span><span class="sxs-lookup"><span data-stu-id="bdfb9-178">Commit the change back to the Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="bdfb9-179">`Set-AzureRmDnsRecordSet`을 사용하여 Azure DNS의 기존 레코드 집합 및 포함된 모든 레코드를 지정된 레코드 집합으로 *바꿉니다*.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-179">Using `Set-AzureRmDnsRecordSet` *replaces* the existing record set in Azure DNS (and all records it contains) with the record set specified.</span></span> <span data-ttu-id="bdfb9-180">[Etag 검사](dns-zones-records.md#etags)를 사용하여 동시 변경 내용을 덮어쓰지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-180">[Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="bdfb9-181">선택적 `-Overwrite` 스위치를 사용하여 이러한 검사를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-181">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="bdfb9-182">이 작업 시퀀스를 *파이프*할 수도 있습니다. 즉, 레코드 집합 개체를 매개 변수로 전달하는 대신 파이프를 통해 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-182">This sequence of operations can also be *piped*, meaning you pass the record set object by using the pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="bdfb9-183">위의 예제에서는 'A' 형식의 기존 레코드 집합에 'A' 레코드를 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-183">The examples above show how to add an 'A' record to an existing record set of type 'A'.</span></span> <span data-ttu-id="bdfb9-184">비슷한 작업 시퀀스를 사용하여 다른 형식의 레코드 집합에 레코드를 추가하면 `Add-AzureRmDnsRecordConfig`의 `-Ipv4Address` 매개 변수를 각 레코드 형식에 특정된 다른 매개 변수로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-184">A similar sequence of operations is used to add records to record sets of other types, substituting the `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific to each record type.</span></span> <span data-ttu-id="bdfb9-185">각 레코드 형식의 매개 변수는 위의 [추가 레코드 형식 예제](#additional-record-type-examples)에 표시된 대로 `New-AzureRmDnsRecordConfig` cmdlet의 경우와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-185">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="bdfb9-186">'CNAME' 또는 'SOA' 형식의 레코드 집합은 둘 이상의 레코드를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="bdfb9-187">이 제약 조건은 DNS 표준에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-187">This constraint arises from the DNS standards.</span></span> <span data-ttu-id="bdfb9-188">Azure DNS의 제한 사항이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="bdfb9-189">기존 레코드 집합에서 레코드 제거</span><span class="sxs-lookup"><span data-stu-id="bdfb9-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="bdfb9-190">레코드 집합에서 레코드를 제거하는 프로세스는 기존 레코드 집합에 레코드를 추가하는 프로세스와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-190">The process to remove a record from a record set is similar to the process to add a record to an existing record set:</span></span>

1. <span data-ttu-id="bdfb9-191">기존 레코드 집합 가져오기</span><span class="sxs-lookup"><span data-stu-id="bdfb9-191">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="bdfb9-192">로컬 레코드 집합 개체에서 레코드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-192">Remove the record from the local record set object.</span></span> <span data-ttu-id="bdfb9-193">이 작업은 오프라인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-193">This is an off-line operation.</span></span> <span data-ttu-id="bdfb9-194">제거되는 레코드는 모든 매개 변수가 기존 레코드와 정확히 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-194">The record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="bdfb9-195">Azure DNS 서비스에 변경 내용 커밋</span><span class="sxs-lookup"><span data-stu-id="bdfb9-195">Commit the change back to the Azure DNS service.</span></span> <span data-ttu-id="bdfb9-196">선택적 `-Overwrite` 스위치를 사용하여 동시 변경에 대한 [Etag 검사](dns-zones-records.md#etags)를 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-196">Use the optional `-Overwrite` switch to suppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="bdfb9-197">레코드 집합에서 마지막 레코드를 제거하는 위의 시퀀스를 사용하여 레코드 집합을 삭제하지 않습니다. 오히려 빈 레코드 집합을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-197">Using the above sequence to remove the last record from a record set does not delete the record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="bdfb9-198">레코드 집합을 완전히 제거하려면 [레코드 집합 삭제](#delete-a-record-set)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-198">To remove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="bdfb9-199">마찬가지로 레코드 집합에 레코드를 추가하려면 레코드 집합을 제거하는 작업 시퀀스는 파이핑될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-199">Similarly to adding records to a record set, the sequence of operations to remove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="bdfb9-200">적절한 형식 특정 매개 변수를 `Remove-AzureRmDnsRecordSet`에 전달하여 다른 레코드 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-200">Different record types are supported by passing the appropriate type-specific parameters to `Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="bdfb9-201">각 레코드 형식의 매개 변수는 위의 [추가 레코드 형식 예제](#additional-record-type-examples)에 표시된 대로 `New-AzureRmDnsRecordConfig` cmdlet의 경우와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-201">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="bdfb9-202">기존 레코드 집합 수정</span><span class="sxs-lookup"><span data-stu-id="bdfb9-202">Modify an existing record set</span></span>

<span data-ttu-id="bdfb9-203">기존 레코드 집합을 수정하기 위한 단계는 레코드 집합에서 레코드를 추가하거나 제거할 때 수행하는 단계와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-203">The steps for modifying an existing record set are similar to the steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="bdfb9-204">`Get-AzureRmDnsRecordSet`을 사용하여 기존 레코드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-204">Retrieve the existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="bdfb9-205">다음을 통해 로컬 레코드 집합 개체를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-205">Modify the local record set object by:</span></span>
    * <span data-ttu-id="bdfb9-206">레코드 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="bdfb9-206">Adding or removing records</span></span>
    * <span data-ttu-id="bdfb9-207">기존 레코드의 매개 변수 변경</span><span class="sxs-lookup"><span data-stu-id="bdfb9-207">Changing the parameters of existing records</span></span>
    * <span data-ttu-id="bdfb9-208">레코드 집합 메타데이터 및 TTL(Time To Live) 변경</span><span class="sxs-lookup"><span data-stu-id="bdfb9-208">Changing the record set metadata and time to live (TTL)</span></span>
3. <span data-ttu-id="bdfb9-209">`Set-AzureRmDnsRecordSet` cmdlet을 사용하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-209">Commit your changes by using the `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="bdfb9-210">그러면 Azure DNS의 기존 레코드 집합이 지정된 레코드 집합으로 *바뀝니다*.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-210">This *replaces* the existing record set in Azure DNS with the record set specified.</span></span>

<span data-ttu-id="bdfb9-211">`Set-AzureRmDnsRecordSet`을 사용하는 경우 [Etag 검사](dns-zones-records.md#etags)를 사용하여 동시 변경 내용을 덮어쓰지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="bdfb9-212">선택적 `-Overwrite` 스위치를 사용하여 이러한 검사를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-212">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

### <a name="to-update-a-record-in-an-existing-record-set"></a><span data-ttu-id="bdfb9-213">기존 레코드 집합의 레코드를 업데이트하려면</span><span class="sxs-lookup"><span data-stu-id="bdfb9-213">To update a record in an existing record set</span></span>

<span data-ttu-id="bdfb9-214">이 예제에서는 기존 'A' 레코드의 IP 주소를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-214">In this example, we change the IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="bdfb9-215">SOA 레코드를 수정하려면</span><span class="sxs-lookup"><span data-stu-id="bdfb9-215">To modify an SOA record</span></span>

<span data-ttu-id="bdfb9-216">영역 루트(인용 부호를 포함한 `-Name "@"`)에 설정된 자동으로 생성된 SOA 레코드 집합에서 레코드를 추가 또는 제거할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-216">You cannot add or remove records from the automatically created SOA record set at the zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="bdfb9-217">그러나 SOA 레코드 내의 매개 변수("Host" 제외) 및 레코드 집합 TTL을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-217">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

<span data-ttu-id="bdfb9-218">다음 예제에서는 SOA 레코드의 *Email* 속성을 변경하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-218">The following example shows how to change the *Email* property of the SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="bdfb9-219">영역 루트의 NS 레코드를 수정하려면</span><span class="sxs-lookup"><span data-stu-id="bdfb9-219">To modify NS records at the zone apex</span></span>

<span data-ttu-id="bdfb9-220">각 DNS 영역에 영역 루트의 NS 레코드 집합이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-220">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="bdfb9-221">여기에는 영역에 할당된 Azure DNS 이름 서버의 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-221">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="bdfb9-222">이 NS 레코드 집합에 추가 이름 서버를 추가하여 DNS 공급자가 2개 이상 있는 공동 호스팅 도메인을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-222">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="bdfb9-223">또한 이 레코드 집합의 TTL 및 메타데이터를 수정할 수 있습니다.또한 이 레코드 집합의 TTL 및 메타데이터를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-223">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="bdfb9-224">그러나 미리 채워진 Azure DNS 이름 서버를 제거 또는 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-224">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="bdfb9-225">이는 영역 루트에 있는 NS 레코드 집합에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-225">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="bdfb9-226">영역의 다른 NS 레코드 집합은 제약 없이 수정할 수 있습니다(자식 영역을 위임하는 데 사용되므로).</span><span class="sxs-lookup"><span data-stu-id="bdfb9-226">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="bdfb9-227">다음 예제에서는 영역 루트의 NS 레코드 집합에 추가 이름 서버를 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-227">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-record-set-metadata"></a><span data-ttu-id="bdfb9-228">레코드 집합 메타데이터를 수정하려면</span><span class="sxs-lookup"><span data-stu-id="bdfb9-228">To modify record set metadata</span></span>

<span data-ttu-id="bdfb9-229">[레코드 집합 메타데이터](dns-zones-records.md#tags-and-metadata)는 키-값 쌍의 형태로 각 레코드 집합과 응용 프로그램 특정 데이터를 연결하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="bdfb9-230">다음 예제에서는 기존 레코드 집합의 메타데이터를 수정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-230">The following example shows how to modify the metadata of an existing record set:</span></span>

```powershell
# Get the record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="bdfb9-231">레코드 집합 삭제</span><span class="sxs-lookup"><span data-stu-id="bdfb9-231">Delete a record set</span></span>

<span data-ttu-id="bdfb9-232">`Remove-AzureRmDnsRecordSet` cmdlet을 사용하여 레코드 집합을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-232">Record sets can be deleted by using the `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="bdfb9-233">레코드 집합을 삭제하면 레코드 집합 내에서 모든 레코드가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-233">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="bdfb9-234">영역 apex(`-Name '@'`)에서 SOA 및 NS 레코드 집합을 삭제할 수 없습니다 .</span><span class="sxs-lookup"><span data-stu-id="bdfb9-234">You cannot delete the SOA and NS record sets at the zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="bdfb9-235">Azure DNS는 영역을 만들 때 자동으로 만들어지고 영역을 삭제할 때 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-235">Azure DNS created these automatically when the zone was created, and deletes them automatically when the zone is deleted.</span></span>

<span data-ttu-id="bdfb9-236">다음 예제에서는 레코드 집합을 삭제하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-236">The following example shows how to delete a record set.</span></span> <span data-ttu-id="bdfb9-237">이 예제에서는 레코드 집합 이름, 레코드 집합 형식, 영역 이름 및 리소스 그룹을 각각 명시적으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-237">In this example, the record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="bdfb9-238">또는 개체를 사용하여 지정된 이름과 형식 및 영역으로 레코드 집합을 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-238">Alternatively, the record set can be specified by name and type, and the zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="bdfb9-239">세 번째 옵션으로 레코드 집합 자체를 레코드 집합 개체를 사용하여 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-239">As a third option, the record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="bdfb9-240">레코드 집합 개체를 사용하여 레코드 집합을 삭제하도록 지정하는 경우 동시 변경 내용이 삭제되지 않도록 [Etag 검사](dns-zones-records.md#etags)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-240">When you specify the record set to be deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="bdfb9-241">선택적 `-Overwrite` 스위치를 사용하여 이러한 검사를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-241">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="bdfb9-242">레코드 집합 개체를 매개 변수로 전달하는 대신 파이프할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-242">The record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="bdfb9-243">확인 메시지 표시</span><span class="sxs-lookup"><span data-stu-id="bdfb9-243">Confirmation prompts</span></span>

<span data-ttu-id="bdfb9-244">`New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet` 및 `Remove-AzureRmDnsRecordSet` cmdlet은 모두 확인 메시지를 표시하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-244">The `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="bdfb9-245">`$ConfirmPreference` PowerShell 기본 설정 변수 값에 `Medium` 이하의 값이 있는 경우 각 cmdlet은 확인 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-245">Each cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="bdfb9-246">`$ConfirmPreference`의 기본 값이 `High`이기 때문에 기본 PowerShell 설정을 사용하는 경우 이러한 프롬프트가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-246">Since the default value for `$ConfirmPreference` is `High`, these prompts are not given when using the default PowerShell settings.</span></span>

<span data-ttu-id="bdfb9-247">`-Confirm` 매개 변수를 사용하여 현재 `$ConfirmPreference` 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-247">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="bdfb9-248">`-Confirm` 또는 `-Confirm:$True`를 지정하는 경우 cmdlet은 실행하기 전에 확인을 위한 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-248">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="bdfb9-249">`-Confirm:$False`을 지정하는 경우 cmdlet은 확인을 위한 메시지를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-249">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="bdfb9-250">`-Confirm` 및 `$ConfirmPreference`에 대한 자세한 내용은 [기본 설정 변수 정보](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdfb9-251">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bdfb9-251">Next steps</span></span>

<span data-ttu-id="bdfb9-252">[Azure DNS의 영역 및 레코드](dns-zones-records.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="bdfb9-253">Azure DNS를 사용하는 경우 [영역 및 레코드를 보호](dns-protect-zones-recordsets.md)하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-253">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="bdfb9-254">[Azure DNS PowerShell 참조 설명서](/powershell/module/azurerm.dns)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="bdfb9-254">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>
