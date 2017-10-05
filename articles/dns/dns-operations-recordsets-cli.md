---
title: "Azure CLI 2.0을 사용하여 Azure DNS에서 DNS 레코드 관리 | Microsoft Docs"
description: "Azure DNS에서 도메인을 호스트하는 경우 Azure DNS에서 DNS 레코드 집합 및 레코드를 관리합니다. 레코드 집합 및 레코드 작업에 대한 모든 CLI 2.0 명령입니다."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: jonatul
ms.openlocfilehash: 9543759d7ba88c7c5068021cebbeec6b8d63633e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-the-azure-cli-20"></a><span data-ttu-id="0f72e-104">Azure CLI 2.0을 사용하여 Azure DNS에서 DNS 레코드 및 레코드 집합 관리</span><span class="sxs-lookup"><span data-stu-id="0f72e-104">Manage DNS records and recordsets in Azure DNS using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0f72e-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="0f72e-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="0f72e-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0f72e-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="0f72e-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0f72e-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="0f72e-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f72e-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="0f72e-109">이 문서는 Windows, Mac 및 Linux용으로 제공되는 플랫폼 간 Azure CLI(명령줄 인터페이스) 2.0을 사용하여 DNS 영역에 대한 DNS 레코드를 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-109">This article shows you how to manage DNS records for your DNS zone by using the cross-platform Azure command-line interface (CLI) 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="0f72e-110">[Azure PowerShell](dns-operations-recordsets.md) 또는 [Azure Portal](dns-operations-recordsets-portal.md)을 사용하여 DNS 레코드를 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="0f72e-111">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="0f72e-111">CLI versions to complete the task</span></span>

<span data-ttu-id="0f72e-112">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="0f72e-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - 클래식 및 리소스 관리 배포 모델용 CLI.</span><span class="sxs-lookup"><span data-stu-id="0f72e-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="0f72e-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="0f72e-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="0f72e-115">이 문서의 예제에서는 이미 [Azure CLI 2.0을 설치했고, 로그인했고, DNS 영역을 만들었다](dns-operations-dnszones-cli.md)고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-115">The examples in this article assume you have already [installed the Azure CLI 2.0, signed in, and created a DNS zone](dns-operations-dnszones-cli.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="0f72e-116">소개</span><span class="sxs-lookup"><span data-stu-id="0f72e-116">Introduction</span></span>

<span data-ttu-id="0f72e-117">Azure DNS에 DNS 레코드를 만들기 전에 먼저 Azure DNS에서 DNS 레코드를 DNS 레코드 집합으로 구성하는 방법을 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-117">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="0f72e-118">Azure DNS의 DNS 레코드에 대한 자세한 내용은 [DNS 영역 및 레코드](dns-zones-records.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="0f72e-119">DNS 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="0f72e-119">Create a DNS record</span></span>

<span data-ttu-id="0f72e-120">DNS 레코드를 만들려면 `az network dns record-set <record-type> set-record` 명령을 사용합니다(여기서 `<record-type>`은</span><span class="sxs-lookup"><span data-stu-id="0f72e-120">To create a DNS record, use the `az network dns record-set <record-type> set-record` command (where `<record-type>` is the type of record, i.e</span></span> <span data-ttu-id="0f72e-121">a, srv, txt 등의 레코드 형식임). 도움말을 보려면 `az network dns record-set --help`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-121">a, srv, txt, etc.) For help, see `az network dns record-set --help`.</span></span>

<span data-ttu-id="0f72e-122">레코드를 만드는 경우 리소스 그룹 이름, 영역 이름, 레코드 집합 이름, 레코드 유형 및 만드는 레코드의 세부 정보를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-122">When creating a record, you need to specify the resource group name, zone name, record set name, the record type, and the details of the record being created.</span></span> <span data-ttu-id="0f72e-123">레코드 집합 이름은 *상대* 이름이어야 합니다. 즉, 영역 이름을 제외해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-123">The record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span>

<span data-ttu-id="0f72e-124">레코드 집합이 아직 없는 경우 이 명령은 자동으로 레코드 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-124">If the record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="0f72e-125">레코드 집합이 이미 있는 경우 이 명령은 지정한 레코드를 기존 레코드 집합에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-125">If the record set already exists, this command adds the record you specify to the existing record set.</span></span>

<span data-ttu-id="0f72e-126">새 레코드 집합이 만들어지면 3600의 기본 TTL(Time to Live)이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="0f72e-127">다른 TTL을 사용하는 방법에 대한 지침은 [DNS 레코드 집합 만들기](#create-a-dns-record-set)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-127">For instructions on how to use different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="0f72e-128">다음 예제에서는 *MyResourceGroup* 리소스 그룹의 *contoso.com* 영역에 *www*라는 A 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-128">The following example creates an A record called *www* in the zone *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="0f72e-129">A 레코드의 IP 주소는 *1.2.3.4*입니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-129">The IP address of the A record is *1.2.3.4*.</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="0f72e-130">영역의 구로에서 레코드 집합을 만들려면(이 경우 "contoso.com"), 따옴표를 포함한 레코드 이름 "@"를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-130">To create a record set in the apex of the zone (in this case, "contoso.com"), use the record name "@", including the quotation marks:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --ipv4-address 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="0f72e-131">DNS 레코드 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="0f72e-131">Create a DNS record set</span></span>

<span data-ttu-id="0f72e-132">위의 예제에서는 DNS 레코드가 기존 레코드 집합에 추가되거나 레코드 집합이 *명시적*으로 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-132">In the above examples, the DNS record was either added to an existing record set, or the record set was created *implicitly*.</span></span> <span data-ttu-id="0f72e-133">레코드를 추가하기 전에 레코드 집합을 *명시적*으로 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-133">You can also create the record set *explicitly* before adding records to it.</span></span> <span data-ttu-id="0f72e-134">Azure DNS는 DNS 레코드를 만들기 전에 DNS 이름을 예약하는 자리 표시자 역할을 수행할 수 있는 '빈' 레코드 집합도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-134">Azure DNS supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="0f72e-135">빈 레코드 집합은 Azure DNS 제어 평면에 표시되어 있지만 Azure DNS 이름 서버에 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-135">Empty record sets are visible in the Azure DNS control plane, but do not appear on the Azure DNS name servers.</span></span>

<span data-ttu-id="0f72e-136">`az network dns record-set <record-type> create` 명령을 사용하여 레코드 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-136">Record sets are created using the `az network dns record-set <record-type> create` command.</span></span> <span data-ttu-id="0f72e-137">도움말을 보려면 `az network dns record-set <record-type> create --help`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-137">For help, see `az network dns record-set <record-type> create --help`.</span></span>

<span data-ttu-id="0f72e-138">레코드 집합을 명시적으로 만들면 [TTL(Time to Live)](dns-zones-records.md#time-to-live) 및 메타데이터와 같은 레코드 집합 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-138">Creating the record set explicitly allows you to specify record set properties such as the [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="0f72e-139">[레코드 집합 메타데이터](dns-zones-records.md#tags-and-metadata)는 키-값 쌍의 형태로 각 레코드 집합과 응용 프로그램 특정 데이터를 연결하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="0f72e-140">다음 예제에서는 `--ttl` 매개 변수(약식 `-l`)를 사용하여 60초 TTL이 있는 비어 있는 'A' 형식의 레코드 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-140">The following example creates an empty record set of type 'A' with a 60-second TTL, by using the `--ttl` parameter (short form `-l`):</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --ttl 60
```

<span data-ttu-id="0f72e-141">다음 예제에서는 `--metadata` 매개 변수를 사용하여 "dept=finance" 및 "environment=production"라는 두 개의 메타데이터 항목을 가진 레코드 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-141">The following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter :</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --metadata "dept=finance" "environment=production"
```

<span data-ttu-id="0f72e-142">비어 있는 레코드 집합을 만들었으므로 [DNS 레코드 만들기](#create-a-dns-record)에 설명된 대로 `azure network dns record-set <record-type> set-record`를 사용하여 레코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-142">Having created an empty record set, records can be added using `azure network dns record-set <record-type> set-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="0f72e-143">다른 형식의 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="0f72e-143">Create records of other types</span></span>

<span data-ttu-id="0f72e-144">지금까지 'A' 레코드를 만드는 방법에 대해 자세히 살펴보았으며, 다음 예제에서는 Azure DNS에서 지원하는 다른 레코드 형식의 레코드를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-144">Having seen in detail how to create 'A' records, the following examples show how to create record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="0f72e-145">레코드 데이터를 지정하는 데 사용되는 매개 변수는 레코드 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-145">The parameters used to specify the record data vary depending on the type of the record.</span></span> <span data-ttu-id="0f72e-146">예를 들어 "A" 유형의 레코드의 경우 `--ipv4-address <IPv4 address>` 매개 변수로 IPv4 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-146">For example, for a record of type "A", you specify the IPv4 address with the parameter `--ipv4-address <IPv4 address>`.</span></span> <span data-ttu-id="0f72e-147">각 레코드 형식에 대한 매개 변수는 `az network dns record-set <record-type> set-record --help`를 사용하여 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-147">The parameters for each record type can be listed using `az network dns record-set <record-type> set-record --help`.</span></span>

<span data-ttu-id="0f72e-148">각각의 경우에 단일 레코드를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-148">In each case, we show how to create a single record.</span></span> <span data-ttu-id="0f72e-149">레코드는 기존 레코드 집합 또는 암시적으로 생성된 레코드 집합에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-149">The record is added to the existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="0f72e-150">레코드 집합 생성 및 레코드 집합 매개 변수를 명시적으로 정의하는 방법은 [DNS 레코드 집합 만들](#create-a-dns-record-set)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="0f72e-151">SOA가 각 DNS 영역과 함께 만들어지고 삭제되며 별도로 만들어지거나 삭제될 수 없기 때문에 SOA 레코드 집합을 만드는 예제를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-151">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="0f72e-152">그러나 [뒷부분의 예제에 표시된 대로 SOA를 수정할 수 있습니다](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="0f72e-152">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="0f72e-153">AAAA 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="0f72e-153">Create an AAAA record</span></span>

```azurecli
az network dns record-set aaaa set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-aaaa --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="0f72e-154">CNAME 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="0f72e-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="0f72e-155">DNS 표준은 영역의 apex(`--Name "@"`)에서 CNAME 레코드를 허용하거나 둘 이상의 레코드를 포함하는 레코드 집합을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-155">The DNS standards do not permit CNAME records at the apex of a zone (`--Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="0f72e-156">자세한 내용은 [CNAME 레코드](dns-zones-records.md#cname-records)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="0f72e-157">MX 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="0f72e-157">Create an MX record</span></span>

<span data-ttu-id="0f72e-158">이 예제에서는 레코드 집합 이름을 "@"로 사용하여 영역 구로에 MX 레코드를 만듭니다(이 경우 "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="0f72e-158">In this example, we use the record set name "@" to create the MX record at the zone apex (in this case, "contoso.com").</span></span>

```azurecli
az network dns record-set mx set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="0f72e-159">NS 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="0f72e-159">Create an NS record</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-ns --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="0f72e-160">PTR 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="0f72e-160">Create a PTR record</span></span>

<span data-ttu-id="0f72e-161">이 경우에 'my-arpa-zone.com'은 IP 범위를 나타내는 ARPA 영역을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-161">In this case, 'my-arpa-zone.com' represents the ARPA zone representing your IP range.</span></span> <span data-ttu-id="0f72e-162">이 영역의 각 PTR 레코드 집합은 IP 범위 내의 IP 주소에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-162">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span>  <span data-ttu-id="0f72e-163">레코드 이름 '10'은 이 레코드에서 나타내는 이 IP 범위 내에서 IP 주소의 마지막 옥텟입니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-163">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```azurecli
az network dns record-set ptr set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name my-arpa.zone.com --ptrdname myservice.contoso.com
```

### <a name="create-an-srv-record"></a><span data-ttu-id="0f72e-164">SRV 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="0f72e-164">Create an SRV record</span></span>

<span data-ttu-id="0f72e-165">[SRV 레코드 집합](dns-zones-records.md#srv-records)을 만들 경우 레코드 집합 이름에 *\_서비스* 및 *\_프로토콜*을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="0f72e-166">영역 apex에 SRV 레코드 집합을 만드는 경우 레코드 집합 이름에서 "@"을 포함할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-166">There is no need to include "@" in the record set name when creating an SRV record set at the zone apex.</span></span>

```azurecli
az network dns record-set srv set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name _sip._tls --priority 10 --weight 5 --port 8080 --target sip.contoso.com
```

### <a name="create-a-txt-record"></a><span data-ttu-id="0f72e-167">TXT 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="0f72e-167">Create a TXT record</span></span>

<span data-ttu-id="0f72e-168">다음 예제에서는 TXT 레코드를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-168">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="0f72e-169">TXT 레코드에서 지원되는 최대 문자열 길이에 대한 자세한 내용은 [TXT 레코드](dns-zones-records.md#txt-records)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-169">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
az network dns record-set txt set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-txt --value "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="0f72e-170">레코드 집합 가져오기</span><span class="sxs-lookup"><span data-stu-id="0f72e-170">Get a record set</span></span>

<span data-ttu-id="0f72e-171">기존 레코드 집합을 가져오려면, `az network dns record-set <record-type> show`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-171">To retrieve an existing record set, use `az network dns record-set <record-type> show`.</span></span> <span data-ttu-id="0f72e-172">도움말을 보려면 `az network dns record-set <record-type> show --help`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-172">For help, see `az network dns record-set <record-type> show --help`.</span></span>

<span data-ttu-id="0f72e-173">레코드 또는 레코드 집합을 만들 때와 마찬가지로, 레코드 집합 이름은 *상대* 이름이어야 합니다. 즉, 영역 이름을 제외해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-173">As when creating a record or record set, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="0f72e-174">레코드 형식, 레코드 집합을 포함하는 영역 및 영역을 포함하는 리소스 그룹을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-174">You also need to specify the record type, the zone containing the record set, and the resource group containing the zone.</span></span>

<span data-ttu-id="0f72e-175">다음 예제에서는 *MyResourceGroup* 리소스 그룹의 *contoso.com* 영역에서 *www*라는 A 형식의 레코드를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-175">The following example retrieves the record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a show --resource-group myresourcegroup --zone-name contoso.com --name www
```

## <a name="list-record-sets"></a><span data-ttu-id="0f72e-176">레코드 집합 나열</span><span class="sxs-lookup"><span data-stu-id="0f72e-176">List record sets</span></span>

<span data-ttu-id="0f72e-177">`az network dns record-set list` 명령을 사용하여 DNS 영역에 있는 모든 레코드를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-177">You can list all records in a DNS zone by using the `az network dns record-set list` command.</span></span> <span data-ttu-id="0f72e-178">도움말을 보려면 `az network dns record-set list --help`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-178">For help, see `az network dns record-set list --help`.</span></span>

<span data-ttu-id="0f72e-179">이 예제는 이름이나 레코드 형식에 관계없이 *MyResourceGroup* 리소스 그룹의 *contoso.com* 영역에 모든 레코드 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-179">This example returns all record sets in the zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
az network dns record-set list --resource-group myresourcegroup --zone-name contoso.com
```

<span data-ttu-id="0f72e-180">이 예제는 지정된 레코드 형식(이 경우 'A' 레코드)과 일치하는 모든 레코드 집합을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-180">This example returns all record sets that match the given record type (in this case, 'A' records):</span></span>

```azurecli
az network dns record-set a list --resource-group myresourcegroup --zone-name contoso.com 
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="0f72e-181">기존 레코드 집합에 레코드 추가</span><span class="sxs-lookup"><span data-stu-id="0f72e-181">Add a record to an existing record set</span></span>

<span data-ttu-id="0f72e-182">`az network dns record-set <record-type> set-record`를 사용하여 새 레코드 집합에 레코드를 만들거나 기존 레코드 집합에 레코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-182">You can use `az network dns record-set <record-type> set-record` both to create a record in a new record set, or to add a record to an existing record set.</span></span>

<span data-ttu-id="0f72e-183">자세한 내용은 위의 [DNS 레코드 만들기](#create-a-dns-record) 및 [다른 형식의 레코드 만들기](#create-records-of-other-types)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="0f72e-184">기존 레코드 집합에서 레코드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="0f72e-185">기존 레코드 집합에서 DNS 레코드를 제거하려면 `az network dns record-set <record-type> remove-record`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-185">To remove a DNS record from an existing record set, use `az network dns record-set <record-type> remove-record`.</span></span> <span data-ttu-id="0f72e-186">도움말을 보려면 `az network dns record-set <record-type> remove-record -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-186">For help, see `az network dns record-set <record-type> remove-record -h`.</span></span>

<span data-ttu-id="0f72e-187">이 명령은 레코드 집합에서 DNS 레코드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="0f72e-188">레코드 집합에서 마지막 레코드가 삭제되면 레코드 집합 자체도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-188">If the last record in a record set is deleted, the record set itself is also deleted.</span></span> <span data-ttu-id="0f72e-189">대신, 빈 레코드 집합을 유지하려면 `--keep-empty-record-set` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-189">To keep the empty record set instead, use the `--keep-empty-record-set` option.</span></span>

<span data-ttu-id="0f72e-190">`az network dns record-set <record-type> set-record`를 사용하여 레코드를 만들 때와 동일한 매개 변수를 사용하여 삭제할 레코드와 레코드를 삭제할 영역을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-190">You need to specify the record to be deleted and the zone it should be deleted from, using the same parameters as when creating a record using `az network dns record-set <record-type> set-record`.</span></span> <span data-ttu-id="0f72e-191">이러한 매개 변수는 위의 [DNS 레코드 만들기](#create-a-dns-record) 및 [다른 형식의 레코드 만들기](#create-records-of-other-types)에 설명됩니다</span><span class="sxs-lookup"><span data-stu-id="0f72e-191">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="0f72e-192">다음 예제에서는 *MyResourceGroup* 리소스 그룹의 *contoso.com* 영역에 *www*라는 레코드 집합에서 값이 '1.2.3.4'인 A 레코드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-192">The following example deletes the A record with value '1.2.3.4' from the record set named *www* in the zone *contoso.com*, in the resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="0f72e-193">기존 레코드 집합 수정</span><span class="sxs-lookup"><span data-stu-id="0f72e-193">Modify an existing record set</span></span>

<span data-ttu-id="0f72e-194">각 레코드 집합에는 [TTL(Time to Live)](dns-zones-records.md#time-to-live), [메타데이터](dns-zones-records.md#tags-and-metadata) 및 DNS 레코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-194">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="0f72e-195">다음 섹션에서는 이러한 각 속성을 수정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-195">The following sections explain how to modify each of these properties.</span></span>

### <a name="to-modify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="0f72e-196">A, AAAA, MX, NS, PTR, SRV 또는 TXT 레코드를 수정하려면</span><span class="sxs-lookup"><span data-stu-id="0f72e-196">To modify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="0f72e-197">A, AAAA, MX, NS, PTR, SRV 또는 TXT 형식의 기존 레코드를 수정하려면 먼저 새 레코드를 추가한 후 기존 레코드를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-197">To modify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete the existing record.</span></span> <span data-ttu-id="0f72e-198">레코드를 삭제 및 추가하는 방법에 대한 자세한 내용은 이 문서의 이전 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-198">For detailed instructions on how to delete and add records, see the earlier sections of this article.</span></span>

<span data-ttu-id="0f72e-199">다음 예제에서는 IP 주소 1.2.3.4~IP 주소 5.6.7.8 범위에서 'A' 레코드를 수정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-199">The following example shows how to modify an 'A' record, from IP address 1.2.3.4 to IP address 5.6.7.8:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 5.6.7.8
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="0f72e-200">영역 루트(인용 부호를 포함하는 `--Name "@"`)에 자동으로 생성된 NS 레코드 집합에서 레코드를 추가, 제거 또는 수정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-200">You cannot add, remove, or modify the records in the automatically created NS record set at the zone apex (`--Name "@"`, including quote marks).</span></span> <span data-ttu-id="0f72e-201">이 레코드 집합의 경우 레코드 집합 TTL 및 메타데이터를 수정하는 변경 작업만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-201">For this record set, the only changes permitted are to modify the record set TTL and metadata.</span></span>

### <a name="to-modify-a-cname-record"></a><span data-ttu-id="0f72e-202">CNAME 레코드를 수정하려면</span><span class="sxs-lookup"><span data-stu-id="0f72e-202">To modify a CNAME record</span></span>

<span data-ttu-id="0f72e-203">대부분의 다른 레코드 형식과 달리 CNAME 레코드 집합은 단일 레코드만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-203">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="0f72e-204">따라서 다른 레코드 형식의 경우과 달리, 새 레코드를 추가하고 기존 레코드를 제거하여 현재 값을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-204">Therefore, you cannot replace the current value by adding a new record and removing the existing record, as for other record types.</span></span>

<span data-ttu-id="0f72e-205">대신 CNAME 레코드를 수정하려면 `az network dns record-set cname set-record`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-205">Instead, to modify a CNAME record, use `az network dns record-set cname set-record`.</span></span> <span data-ttu-id="0f72e-206">도움말을 보려면 `az network dns record-set cname set-record --help`를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-206">For help, see `az network dns record-set cname set-record --help`</span></span>

<span data-ttu-id="0f72e-207">이 예에서는 기존 값 대신 'www.fabrikam.net'을 가리키도록 *MyResourceGroup* 리소스 그룹의 *contoso.com* 영역에서 *www*라는 CNAME 레코드 집합을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-207">The example modifies the CNAME record set *www* in the zone *contoso.com*, in resource group *MyResourceGroup*, to point to 'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.fabrikam.net
``` 

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="0f72e-208">SOA 레코드를 수정하려면</span><span class="sxs-lookup"><span data-stu-id="0f72e-208">To modify an SOA record</span></span>

<span data-ttu-id="0f72e-209">대부분의 다른 레코드 형식과 달리 CNAME 레코드 집합은 단일 레코드만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-209">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="0f72e-210">따라서 다른 레코드 형식의 경우과 달리, 새 레코드를 추가하고 기존 레코드를 제거하여 현재 값을 바꿀 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-210">Therefore, you cannot replace the current value by adding a new record and removing the existing record, as for other record types.</span></span>

<span data-ttu-id="0f72e-211">대신 SOA 레코드를 수정하려면 `az network dns record-set soa update`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-211">Instead, to modify the SOA record, use `az network dns record-set soa update`.</span></span> <span data-ttu-id="0f72e-212">도움말을 보려면 `az network dns record-set soa update --help`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-212">For help, see `az network dns record-set soa update --help`.</span></span>

<span data-ttu-id="0f72e-213">다음 예제에서는 *MyResourceGroup* 리소스 그룹의 *contoso.com* 영역에 SOA 레코드의 'email' 속성을 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-213">The following example shows how to set the 'email' property of the SOA record for the zone *contoso.com* in the resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set soa update --resource-group myresourcegroup --zone-name contoso.com --email admin.contoso.com
```

### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="0f72e-214">영역 루트의 NS 레코드를 수정하려면</span><span class="sxs-lookup"><span data-stu-id="0f72e-214">To modify NS records at the zone apex</span></span>

<span data-ttu-id="0f72e-215">각 DNS 영역에 영역 루트의 NS 레코드 집합이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-215">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="0f72e-216">여기에는 영역에 할당된 Azure DNS 이름 서버의 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-216">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="0f72e-217">이 NS 레코드 집합에 추가 이름 서버를 추가하여 DNS 공급자가 2개 이상 있는 공동 호스팅 도메인을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-217">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="0f72e-218">또한 이 레코드 집합의 TTL 및 메타데이터를 수정할 수 있습니다.또한 이 레코드 집합의 TTL 및 메타데이터를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-218">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="0f72e-219">그러나 미리 채워진 Azure DNS 이름 서버를 제거 또는 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-219">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="0f72e-220">이는 영역 루트에 있는 NS 레코드 집합에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-220">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="0f72e-221">영역의 다른 NS 레코드 집합은 제약 없이 수정할 수 있습니다(자식 영역을 위임하는 데 사용되므로).</span><span class="sxs-lookup"><span data-stu-id="0f72e-221">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="0f72e-222">다음 예제에서는 영역 루트의 NS 레코드 집합에 추가 이름 서버를 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-222">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="to-modify-the-ttl-of-an-existing-record-set"></a><span data-ttu-id="0f72e-223">기존 레코드 집합의 TTL을 수정하려면</span><span class="sxs-lookup"><span data-stu-id="0f72e-223">To modify the TTL of an existing record set</span></span>

<span data-ttu-id="0f72e-224">기존 레코드 집합의 TTL을 수정하려면 `azure network dns record-set <record-type> update`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-224">To modify the TTL of an existing record set, use `azure network dns record-set <record-type> update`.</span></span> <span data-ttu-id="0f72e-225">도움말을 보려면 `azure network dns record-set <record-type> update --help`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-225">For help, see `azure network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="0f72e-226">다음 예제에서는 레코드 집합 TTL(이 경우 60초)을 수정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-226">The following example shows how to modify a record set TTL, in this case to 60 seconds:</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set ttl=60
```

### <a name="to-modify-the-metadata-of-an-existing-record-set"></a><span data-ttu-id="0f72e-227">기존 레코드 집합의 메타데이터를 수정하려면</span><span class="sxs-lookup"><span data-stu-id="0f72e-227">To modify the metadata of an existing record set</span></span>

<span data-ttu-id="0f72e-228">[레코드 집합 메타데이터](dns-zones-records.md#tags-and-metadata)는 키-값 쌍의 형태로 각 레코드 집합과 응용 프로그램 특정 데이터를 연결하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="0f72e-229">기존 레코드 집합의 메타데이터를 수정하려면 `az network dns record-set <record-type> update`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-229">To modify the metadata of an existing record set, use `az network dns record-set <record-type> update`.</span></span> <span data-ttu-id="0f72e-230">도움말을 보려면 `az network dns record-set <record-type> update --help`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-230">For help, see `az network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="0f72e-231">다음 예제에서는 "dept=finance" 및 "environment=production"라는 두 개의 메타데이터 항목을 가진 레코드 집합을 수정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-231">The following example shows how to modify a record set with two metadata entries, "dept=finance" and "environment=production".</span></span> <span data-ttu-id="0f72e-232">기존 메타데이터는 지정된 값으로 *대체*됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-232">Note that any existing metadata is *replaced* by the values given.</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set metadata.dept=finance metadata.environment=production
```

## <a name="delete-a-record-set"></a><span data-ttu-id="0f72e-233">레코드 집합 삭제</span><span class="sxs-lookup"><span data-stu-id="0f72e-233">Delete a record set</span></span>

<span data-ttu-id="0f72e-234">`az network dns record-set <record-type> delete` 명령을 사용하여 레코드 집합을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-234">Record sets can be deleted by using the `az network dns record-set <record-type> delete` command.</span></span> <span data-ttu-id="0f72e-235">도움말을 보려면 `azure network dns record-set <record-type> delete --help`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f72e-235">For help, see `azure network dns record-set <record-type> delete --help`.</span></span> <span data-ttu-id="0f72e-236">레코드 집합을 삭제하면 레코드 집합 내에서 모든 레코드가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-236">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="0f72e-237">영역 apex(`--name "@"`)에서 SOA 및 NS 레코드 집합을 삭제할 수 없습니다 .</span><span class="sxs-lookup"><span data-stu-id="0f72e-237">You cannot delete the SOA and NS record sets at the zone apex (`--name "@"`).</span></span>  <span data-ttu-id="0f72e-238">이러한 항목은 영역을 만들 때 자동으로 만들어지고 영역을 삭제할 때 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-238">These are created automatically when the zone was created, and are deleted automatically when the zone is deleted.</span></span>

<span data-ttu-id="0f72e-239">다음 예제에서는 *MyResourceGroup* 리소스 그룹의 *contoso.com* 영역에서 *www*라는 A 형식의 레코드 집합을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-239">The following example deletes the record set named *www* of type A from the zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a delete --resource-group myresourcegroup --zone-name contoso.com --name www
```

<span data-ttu-id="0f72e-240">삭제 작업을 확인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-240">You are prompted to confirm the delete operation.</span></span> <span data-ttu-id="0f72e-241">이 프롬프트를 표시하지 않으려면 `--yes` 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-241">To suppress this prompt, use the `--yes` switch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f72e-242">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f72e-242">Next steps</span></span>

<span data-ttu-id="0f72e-243">[Azure DNS의 영역 및 레코드](dns-zones-records.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="0f72e-244">Azure DNS를 사용하는 경우 [영역 및 레코드를 보호](dns-protect-zones-recordsets.md)하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0f72e-244">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
