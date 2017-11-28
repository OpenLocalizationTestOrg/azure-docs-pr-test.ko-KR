---
title: "Azure DNS를 사용 하 여 DNS 레코드 aaaManage hello Azure CLI 1.0 | Microsoft Docs"
description: "Azure DNS에서 도메인을 호스트하는 경우 Azure DNS에서 DNS 레코드 집합 및 레코드를 관리합니다. 레코드 집합 및 레코드 작업에 대한 모든 CLI 1.0 명령입니다."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2016
ms.author: jonatul
ms.openlocfilehash: 1f01450b0839f712cb1d96be318766bac581fea1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-in-azure-dns-using-hello-azure-cli-10"></a><span data-ttu-id="08f06-104">Azure dns hello Azure CLI 1.0을 사용 하 여 DNS 레코드 관리</span><span class="sxs-lookup"><span data-stu-id="08f06-104">Manage DNS records in Azure DNS using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="08f06-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="08f06-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="08f06-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="08f06-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="08f06-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="08f06-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="08f06-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08f06-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="08f06-109">이 문서를 사용 하 여 DNS 영역에 대 한 DNS 레코드 toomanage Azure CLI (명령줄 인터페이스), Windows, Mac 및 Linux에 사용할 수 있는 플랫폼 간 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-109">This article shows you how toomanage DNS records for your DNS zone by using hello cross-platform Azure command-line interface (CLI), which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="08f06-110">사용 하 여 DNS 레코드를 관리할 수도 있습니다 [Azure PowerShell](dns-operations-recordsets.md) 또는 hello [Azure 포털](dns-operations-recordsets-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="08f06-111">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="08f06-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="08f06-112">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="08f06-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) -hello 클래식 및 리소스 관리 배포 모델에 대 한 우리의 CLI 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="08f06-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="08f06-115">이 문서의 예제 hello 이미 있다고 가정 [hello 로그인 되어 Azure CLI 1.0을 설치 하 고 DNS 영역을 만든](dns-operations-dnszones-cli-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-115">hello examples in this article assume you have already [installed hello Azure CLI 1.0, signed in, and created a DNS zone](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="08f06-116">소개</span><span class="sxs-lookup"><span data-stu-id="08f06-116">Introduction</span></span>

<span data-ttu-id="08f06-117">Azure DNS에 DNS 레코드를 만들기 전에 먼저 toounderstand Azure DNS DNS 레코드 집합으로 DNS 레코드를 구성 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-117">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="08f06-118">Azure DNS의 DNS 레코드에 대한 자세한 내용은 [DNS 영역 및 레코드](dns-zones-records.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08f06-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="08f06-119">DNS 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="08f06-119">Create a DNS record</span></span>

<span data-ttu-id="08f06-120">toocreate DNS 레코드를 사용 하 여 hello `azure network dns record-set add-record` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-120">toocreate a DNS record, use hello `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="08f06-121">도움말을 보려면 `azure network dns record-set add-record -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08f06-121">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="08f06-122">레코드를 만들 때 필요한 toospecify hello 리소스 그룹 이름, 영역 이름, 레코드 이름, hello 레코드 종류 및 만들려는 hello 레코드의 hello 세부 정보를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-122">When creating a record, you need toospecify hello resource group name, zone name, record set name, hello record type, and hello details of hello record being created.</span></span> <span data-ttu-id="08f06-123">hello 지정 된 레코드 집합 이름 이어야 합니다는 *상대* 이름, 즉 hello 영역 이름을 제외 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-123">hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span>

<span data-ttu-id="08f06-124">레코드 집합 hello가 아직 없는 경우이 명령은을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-124">If hello record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="08f06-125">Hello 레코드 집합이 이미 있는 경우이 명령은 adda hello 레코드 toohello 기존 레코드 집합을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-125">If hello record set already exists, this command adda hello record you specify toohello existing record set.</span></span>

<span data-ttu-id="08f06-126">새 레코드 집합이 만들어지면 3600의 기본 TTL(Time to Live)이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="08f06-127">다른 TTLs 참조 하는 toouse 방법에 대 한 지침은 [DNS 레코드 집합 만들기](#create-a-dns-record-set)합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-127">For instructions on how toouse different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="08f06-128">hello 다음 예제에서는 호출 A 레코드 *www* hello 영역에 *contoso.com* hello 리소스 그룹에 *MyResourceGroup*합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-128">hello following example creates an A record called *www* in hello zone *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="08f06-129">IP 주소 레코드는 hello hello *1.2.3.4*합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-129">hello IP address of hello A record is *1.2.3.4*.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="08f06-130">toocreate hello hello 영역 루트에서 레코드 (이 경우 "contoso.com"), hello 레코드 이름을 사용 하 여 "@", hello 인용 부호를 포함 하 여:</span><span class="sxs-lookup"><span data-stu-id="08f06-130">toocreate a record in hello apex of hello zone (in this case, "contoso.com"), use hello record name "@", including hello quotation marks:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="08f06-131">DNS 레코드 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="08f06-131">Create a DNS record set</span></span>

<span data-ttu-id="08f06-132">위의 예제는 hello에서 hello DNS 레코드 기존 레코드 집합 중 하나가 추가 tooan 되었거나 hello 레코드 집합 만들어진 *암시적으로*합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-132">In hello above examples, hello DNS record was either added tooan existing record set, or hello record set was created *implicitly*.</span></span> <span data-ttu-id="08f06-133">Hello 레코드 집합을 만들 수도 있습니다 *명시적으로* 전에 tooit 레코드 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-133">You can also create hello record set *explicitly* before adding records tooit.</span></span> <span data-ttu-id="08f06-134">Azure DNS 역할을 할 수는 자리 표시자 tooreserve DNS 이름 DNS 레코드를 만들기 전에 '빈' 레코드 집합을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-134">Azure DNS supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="08f06-135">빈 레코드 집합 hello Azure DNS 평면을 제어 있지만 hello Azure DNS 이름 서버에 표시 되지 않는에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-135">Empty record sets are visible in hello Azure DNS control plane, but do not appear on hello Azure DNS name servers.</span></span>

<span data-ttu-id="08f06-136">레코드 집합 hello를 사용 하 여 만들어집니다. `azure network dns record-set create` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-136">Record sets are created using hello `azure network dns record-set create` command.</span></span> <span data-ttu-id="08f06-137">도움말을 보려면 `azure network dns record-set create -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08f06-137">For help, see `azure network dns record-set create -h`.</span></span>

<span data-ttu-id="08f06-138">Hello 같은 toospecify 레코드 집합 속성을 통해 명시적으로 설정 하는 hello 레코드를 만드는 [Time To Live (TTL)](dns-zones-records.md#time-to-live) 및 메타 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-138">Creating hello record set explicitly allows you toospecify record set properties such as hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="08f06-139">[메타 데이터를 설정 하는 레코드](dns-zones-records.md#tags-and-metadata) 키-값 쌍으로 각 레코드 집합을 사용 하 여 사용 되는 tooassociate 응용 프로그램별 데이터 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="08f06-140">hello 다음 예제에서는 hello를 사용 하 여 60 초 TTL로 설정 하는 빈 레코드 `--ttl` 매개 변수 (약식 `-l`):</span><span class="sxs-lookup"><span data-stu-id="08f06-140">hello following example creates an empty record set with a 60-second TTL, by using hello `--ttl` parameter (short form `-l`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

<span data-ttu-id="08f06-141">hello 다음 예제에서는 두 개의 메타 데이터 항목을 사용 하 여 설정 하는 레코드 "dept finance =" 및 "환경 프로덕션 =", hello를 사용 하 여 `--metadata` 매개 변수 (약식 `-m`):</span><span class="sxs-lookup"><span data-stu-id="08f06-141">hello following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter (short form `-m`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

<span data-ttu-id="08f06-142">비어 있는 레코드 집합을 만들었으므로 [DNS 레코드 만들기](#create-a-dns-record)에 설명된 대로 `azure network dns record-set add-record`를 사용하여 레코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-142">Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="08f06-143">다른 형식의 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="08f06-143">Create records of other types</span></span>

<span data-ttu-id="08f06-144">것에 표시할 세부 toocreate 'A' 레코드 방법, hello toocreate 레코드가 다른 레코드 종류의 지원 되는 방식 예제 보여 Azure DNS에서 다음.</span><span class="sxs-lookup"><span data-stu-id="08f06-144">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="08f06-145">hello 매개 변수 사용 toospecify hello 레코드 데이터 hello 레코드의 hello 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-145">hello parameters used toospecify hello record data vary depending on hello type of hello record.</span></span> <span data-ttu-id="08f06-146">예를 들어 "A" 형식의 레코드에 대 한 있습니다 hello IPv4 주소 지정 hello 매개 변수와 함께 `-a <IPv4 address>`합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-146">For example, for a record of type "A", you specify hello IPv4 address with hello parameter `-a <IPv4 address>`.</span></span> <span data-ttu-id="08f06-147">매개 변수를 사용 하 여 각 레코드 종류를 나열할 수 있습니다에 대 한 hello `azure network dns record-set add-record -h`합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-147">hello parameters for each record type can be listed using `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="08f06-148">각 경우에서는 보여줍니다 어떻게 toocreate 단일 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-148">In each case, we show how toocreate a single record.</span></span> <span data-ttu-id="08f06-149">hello 레코드는 레코드 집합을 기존 추가 toohello 또는 레코드 집합을 암시적으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-149">hello record is added toohello existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="08f06-150">레코드 집합 생성 및 레코드 집합 매개 변수를 명시적으로 정의하는 방법은 [DNS 레코드 집합 만들](#create-a-dns-record-set)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08f06-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="08f06-151">에서는 제공 하지 않으므로 예제 toocreate SOA 레코드 집합 Soa 만들어지므로 및 각 DNS 영역 있을 경우 삭제 하 고 만들거나 수 개별적으로 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-151">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="08f06-152">그러나 [SOA를 수정할 수는 뒷부분에 나오는 예제와 같이 hello](#to-modify-an-SOA-record)합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-152">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="08f06-153">AAAA 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="08f06-153">Create an AAAA record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="08f06-154">CNAME 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="08f06-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="08f06-155">hello DNS 표준 hello 영역 루트에서 CNAME 레코드를 허용 하지 않습니다 (`-Name "@"`), 또는 둘 이상의 레코드를 포함 하는 레코드 집합 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-155">hello DNS standards do not permit CNAME records at hello apex of a zone (`-Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="08f06-156">자세한 내용은 [CNAME 레코드](dns-zones-records.md#cname-records)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08f06-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="08f06-157">MX 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="08f06-157">Create an MX record</span></span>

<span data-ttu-id="08f06-158">이 예제에서 사용 하 여 hello 레코드 집합 이름은 "@" toocreate hello hello 영역 루트에서 MX 레코드 (이 경우 "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="08f06-158">In this example, we use hello record set name "@" toocreate hello MX record at hello zone apex (in this case, "contoso.com").</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="08f06-159">NS 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="08f06-159">Create an NS record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="08f06-160">PTR 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="08f06-160">Create a PTR record</span></span>

<span data-ttu-id="08f06-161">이 경우 ' 내-arpa-zone.com' 나타냅니다 hello ARPA 영역이 IP 범위를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-161">In this case, 'my-arpa-zone.com' represents hello ARPA zone representing your IP range.</span></span> <span data-ttu-id="08f06-162">이 IP 범위에 속하는 tooan IP 주소를 해당 하는 각 PTR 레코드를이 영역 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-162">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span>  <span data-ttu-id="08f06-163">hello 레코드 이름은 '10' hello 마지막 8 진수 단위 값이이 레코드를 나타내는이 IP 범위에 속하는 hello IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-163">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a><span data-ttu-id="08f06-164">SRV 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="08f06-164">Create an SRV record</span></span>

<span data-ttu-id="08f06-165">만들 때는 [SRV 레코드 집합](dns-zones-records.md#srv-records), hello 지정  *\_서비스* 및  *\_프로토콜* hello 레코드 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="08f06-166">없는 필요 tooinclude는 "@" hello 레코드 집합 hello 영역 루트에서 설정 SRV 레코드를 만들 때.</span><span class="sxs-lookup"><span data-stu-id="08f06-166">There is no need tooinclude "@" in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a><span data-ttu-id="08f06-167">TXT 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="08f06-167">Create a TXT record</span></span>

<span data-ttu-id="08f06-168">hello 다음 예제에서는 한 TXT toocreate 기록 하는 방법을</span><span class="sxs-lookup"><span data-stu-id="08f06-168">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="08f06-169">TXT 레코드에서 지원 되는 hello 최대 문자열 길이 대 한 자세한 내용은 참조 [TXT 레코드](dns-zones-records.md#txt-records)합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-169">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="08f06-170">레코드 집합 가져오기</span><span class="sxs-lookup"><span data-stu-id="08f06-170">Get a record set</span></span>

<span data-ttu-id="08f06-171">tooretrieve 기존 레코드 집합을 사용 하 여 `azure network dns record-set show`합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-171">tooretrieve an existing record set, use `azure network dns record-set show`.</span></span> <span data-ttu-id="08f06-172">도움말을 보려면 `azure network dns record-set show -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08f06-172">For help, see `azure network dns record-set show -h`.</span></span>

<span data-ttu-id="08f06-173">Hello 레코드 집합이 지정 된 이름 레코드 또는 레코드 집합을 만들 때 처럼 이어야 합니다는 *상대* 이름, 즉 hello 영역 이름을 제외 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-173">As when creating a record or record set, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="08f06-174">또한 toospecify hello 레코드 종류를 해야, hello 레코드를 포함 하는 hello 영역을 설정 하 고 hello hello 영역을 포함 하는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-174">You also need toospecify hello record type, hello zone containing hello record set, and hello resource group containing hello zone.</span></span>

<span data-ttu-id="08f06-175">hello 다음 예제에서는 검색 hello 레코드 *www* 영역에서 a 형식의 *contoso.com* 리소스 그룹에 *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="08f06-175">hello following example retrieves hello record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a><span data-ttu-id="08f06-176">레코드 집합 나열</span><span class="sxs-lookup"><span data-stu-id="08f06-176">List record sets</span></span>

<span data-ttu-id="08f06-177">Hello를 사용 하 여 DNS 영역에 있는 모든 레코드를 나열할 수 있습니다 `azure network dns record-set list` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-177">You can list all records in a DNS zone by using hello `azure network dns record-set list` command.</span></span> <span data-ttu-id="08f06-178">도움말을 보려면 `azure network dns record-set list -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08f06-178">For help, see `azure network dns record-set list -h`.</span></span>

<span data-ttu-id="08f06-179">이 예에서는 hello 영역의 모든 레코드 집합을 반환 *contoso.com*, 리소스 그룹에 *MyResourceGroup*, 이름 또는 레코드 종류에 관계 없이:</span><span class="sxs-lookup"><span data-stu-id="08f06-179">This example returns all record sets in hello zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

<span data-ttu-id="08f06-180">이 예에서는 (이 경우 'A' 레코드)의 레코드 종류를 지정 하는 hello와 일치 하는 모든 레코드 집합을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-180">This example returns all record sets that match hello given record type (in this case, 'A' records):</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="08f06-181">레코드 집합을 기존 레코드 tooan 추가</span><span class="sxs-lookup"><span data-stu-id="08f06-181">Add a record tooan existing record set</span></span>

<span data-ttu-id="08f06-182">사용할 수 있습니다 `azure network dns record-set add-record` 모두 toocreate 새 레코드의 레코드 집합 또는 tooadd 레코드 tooan 기존 레코드 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-182">You can use `azure network dns record-set add-record` both toocreate a record in a new record set, or tooadd a record tooan existing record set.</span></span>

<span data-ttu-id="08f06-183">자세한 내용은 위의 [DNS 레코드 만들기](#create-a-dns-record) 및 [다른 형식의 레코드 만들기](#create-records-of-other-types)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08f06-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="08f06-184">기존 레코드 집합에서 레코드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="08f06-185">tooremove DNS 레코드에서 기존 레코드 집합을 사용 하 여 `azure network dns record-set delete-record`합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-185">tooremove a DNS record from an existing record set, use `azure network dns record-set delete-record`.</span></span> <span data-ttu-id="08f06-186">도움말을 보려면 `azure network dns record-set delete-record -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08f06-186">For help, see `azure network dns record-set delete-record -h`.</span></span>

<span data-ttu-id="08f06-187">이 명령은 레코드 집합에서 DNS 레코드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="08f06-188">자체적으로 설정 하는 hello 레코드는 레코드 집합의 hello 마지막 레코드를 삭제 한 경우 **하지** 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-188">If hello last record in a record set is deleted, hello record set itself is **not** deleted.</span></span> <span data-ttu-id="08f06-189">대신, 비어 있는 레코드 집합이 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-189">Instead, an empty record set is left.</span></span> <span data-ttu-id="08f06-190">대신, 설정 toodelete hello 레코드 참조 [레코드 집합 삭제](#delete-a-record-set)합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-190">toodelete hello record set instead, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="08f06-191">Toospecify 필요한 hello 레코드 toobe 삭제 및 삭제 하 여 메모리를 사용 하 여 hello 영역 hello 동일한 매개 변수를 사용 하는 레코드를 만들 때 `azure network dns record-set add-record`합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-191">You need toospecify hello record toobe deleted and hello zone it should be deleted from, using hello same parameters as when creating a record using `azure network dns record-set add-record`.</span></span> <span data-ttu-id="08f06-192">이러한 매개 변수는 위의 [DNS 레코드 만들기](#create-a-dns-record) 및 [다른 형식의 레코드 만들기](#create-records-of-other-types)에 설명됩니다</span><span class="sxs-lookup"><span data-stu-id="08f06-192">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="08f06-193">이 명령은 확인 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-193">This command prompts for confirmation.</span></span> <span data-ttu-id="08f06-194">Hello를 사용 하 여이 프롬프트를 보류 될 수 있습니다 `--quiet` 스위치 (약식 `-q`).</span><span class="sxs-lookup"><span data-stu-id="08f06-194">This prompt can be suppressed using hello `--quiet` switch (short form `-q`).</span></span>

<span data-ttu-id="08f06-195">다음 예에서는 삭제 하는 hello hello '1.2.3.4' hello 레코드에서 명명 된 설정 값이 있는 레코드 *www* hello 영역에 *contoso.com*, hello 리소스 그룹에 *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="08f06-195">hello following example deletes hello A record with value '1.2.3.4' from hello record set named *www* in hello zone *contoso.com*, in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="08f06-196">hello 확인 메시지가 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-196">hello confirmation prompt is suppressed.</span></span>

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="08f06-197">기존 레코드 집합 수정</span><span class="sxs-lookup"><span data-stu-id="08f06-197">Modify an existing record set</span></span>

<span data-ttu-id="08f06-198">각 레코드 집합에는 [TTL(Time to Live)](dns-zones-records.md#time-to-live), [메타데이터](dns-zones-records.md#tags-and-metadata) 및 DNS 레코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-198">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="08f06-199">hello 다음 섹션에서는 어떻게 각 toomodify 이러한 속성 중입니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-199">hello following sections explain how toomodify each of these properties.</span></span>

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="08f06-200">toomodify A, AAAA, MX, NS, PTR, SRV, 또는 TXT 레코드</span><span class="sxs-lookup"><span data-stu-id="08f06-200">toomodify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="08f06-201">기존 레코드 유형 A, AAAA, MX, NS, PTR, SRV, 또는 TXT toomodify 새 레코드와 다음 삭제 hello 기존 레코드 추가 먼저 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-201">toomodify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete hello existing record.</span></span> <span data-ttu-id="08f06-202">방법에 대 한 자세한 내용은 toodelete 레코드 추가, 참조 및이 문서의 이전 섹션 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-202">For detailed instructions on how toodelete and add records, see hello earlier sections of this article.</span></span>

<span data-ttu-id="08f06-203">다음 예제는 hello 5.6.7.8 toomodify IP 주소 1.2.3.4 tooIP에서 'A' 레코드를 해결 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-203">hello following example shows how toomodify an 'A' record, from IP address 1.2.3.4 tooIP address 5.6.7.8:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="toomodify-a-cname-record"></a><span data-ttu-id="08f06-204">toomodify CNAME 레코드</span><span class="sxs-lookup"><span data-stu-id="08f06-204">toomodify a CNAME record</span></span>

<span data-ttu-id="08f06-205">toomodify CNAME 레코드를 사용 하 여 `azure network dns record-set add-record` tooadd hello 새 레코드 값입니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-205">toomodify a CNAME record, use `azure network dns record-set add-record` tooadd hello new record value.</span></span> <span data-ttu-id="08f06-206">다른 레코드 형식과 달리 CNAME 레코드 집합은 단일 레코드만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-206">Unlike other record types, a CNAME record set can only contain a single record.</span></span> <span data-ttu-id="08f06-207">따라서 hello 기존 레코드는 *대체* hello 새 레코드가 추가 되 고 별도로 삭제 toobe 필요 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="08f06-207">Therefore, hello existing record is *replaced* when hello new record is added, and does not need toobe deleted separately.</span></span>  <span data-ttu-id="08f06-208">하면이 대체재로이 증명된 tooaccept 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-208">You will be prompted tooaccept this replacement.</span></span>

<span data-ttu-id="08f06-209">hello 수정 하는 예제 hello CNAME 레코드 집합 *www* hello 영역에 *contoso.com*, 리소스 그룹에 *MyResourceGroup*, toopoint 너무 'www.fabrikam.net' 대신 해당 기존 값:</span><span class="sxs-lookup"><span data-stu-id="08f06-209">hello example modifies hello CNAME record set *www* in hello zone *contoso.com*, in resource group *MyResourceGroup*, toopoint too'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="08f06-210">toomodify SOA 레코드</span><span class="sxs-lookup"><span data-stu-id="08f06-210">toomodify an SOA record</span></span>

<span data-ttu-id="08f06-211">사용 하 여 `azure network dns record-set set-soa-record` toomodify hello SOA 주어진된 DNS 영역에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-211">Use `azure network dns record-set set-soa-record` toomodify hello SOA for a given DNS zone.</span></span> <span data-ttu-id="08f06-212">도움말을 보려면 `azure network dns record-set set-soa-record -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08f06-212">For help, see `azure network dns record-set set-soa-record -h`.</span></span>

<span data-ttu-id="08f06-213">hello 다음 예제에서는 hello 영역에 대 한 hello SOA의 tooset hello 'email' 속성을 기록 하는 방법을 *contoso.com* hello 리소스 그룹에 *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="08f06-213">hello following example shows how tooset hello 'email' property of hello SOA record for hello zone *contoso.com* in hello resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="08f06-214">hello 영역 루트에 있는 toomodify NS 레코드</span><span class="sxs-lookup"><span data-stu-id="08f06-214">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="08f06-215">hello 영역 루트에서 설정 하는 hello NS 레코드는 각 DNS 영역과 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-215">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="08f06-216">Hello Azure DNS 이름 서버 할당된 toohello 영역의 hello 이름이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-216">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="08f06-217">추가 이름 서버 toothis NS 레코드 집합을 공동 도메인 DNS 공급자를 둘 이상의 호스팅 toosupport를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-217">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="08f06-218">또한 TTL hello 및이 레코드 집합에 대 한 메타 데이터를 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-218">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="08f06-219">그러나 제거 하거나 hello 미리 채워진된 Azure DNS 이름 서버를 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-219">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="08f06-220">Note이 적용 hello 영역 루트에서 레코드 집합 toohello NS만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-220">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="08f06-221">제약 조건 없이 (사용 되는 toodelegate 하위 영역)으로 시간대에서 다른 NS 레코드 집합을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-221">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="08f06-222">다음 예제는 hello 설정 방법을 보여 주는 tooadd 추가 이름 서버 toohello NS 레코드가 hello 영역 루트에서:</span><span class="sxs-lookup"><span data-stu-id="08f06-222">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a><span data-ttu-id="08f06-223">기존 레코드의 TTL toomodify hello 설정</span><span class="sxs-lookup"><span data-stu-id="08f06-223">toomodify hello TTL of an existing record set</span></span>

<span data-ttu-id="08f06-224">기존 레코드의 TTL toomodify hello 설정, 사용 하 여 `azure network dns record-set set`합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-224">toomodify hello TTL of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="08f06-225">도움말을 보려면 `azure network dns record-set set -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08f06-225">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="08f06-226">다음 예제는 hello toomodify 레코드 집합 TTL이 too60 초 경우 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-226">hello following example shows how toomodify a record set TTL, in this case too60 seconds:</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a><span data-ttu-id="08f06-227">기존 레코드의 toomodify hello 메타 데이터 설정</span><span class="sxs-lookup"><span data-stu-id="08f06-227">toomodify hello metadata of an existing record set</span></span>

<span data-ttu-id="08f06-228">[메타 데이터를 설정 하는 레코드](dns-zones-records.md#tags-and-metadata) 키-값 쌍으로 각 레코드 집합을 사용 하 여 사용 되는 tooassociate 응용 프로그램별 데이터 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="08f06-229">기존 레코드의 toomodify hello 메타 데이터 설정, 사용 하 여 `azure network dns record-set set`합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-229">toomodify hello metadata of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="08f06-230">도움말을 보려면 `azure network dns record-set set -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08f06-230">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="08f06-231">hello 다음 예제에서는 설정 방법을 보여 줍니다 toomodify 레코드 두 개 메타 데이터 항목이 있는 "dept finance =" 및 "환경 프로덕션 =", hello를 사용 하 여 `--metadata` 매개 변수 (약식 `-m`).</span><span class="sxs-lookup"><span data-stu-id="08f06-231">hello following example shows how toomodify a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter (short form `-m`).</span></span> <span data-ttu-id="08f06-232">기존 메타 데이터는 *대체* 여 hello 값이 지정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-232">Note that any existing metadata is *replaced* by hello values given.</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a><span data-ttu-id="08f06-233">레코드 집합 삭제</span><span class="sxs-lookup"><span data-stu-id="08f06-233">Delete a record set</span></span>

<span data-ttu-id="08f06-234">Hello를 사용 하 여 레코드 집합을 삭제할 수 있습니다 `azure network dns record-set delete` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-234">Record sets can be deleted by using hello `azure network dns record-set delete` command.</span></span> <span data-ttu-id="08f06-235">도움말을 보려면 `azure network dns record-set delete -h`을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="08f06-235">For help, see `azure network dns record-set delete -h`.</span></span> <span data-ttu-id="08f06-236">레코드 집합을 삭제 하면 hello 레코드 집합 내의 모든 레코드가 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-236">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="08f06-237">Hello NS 및 SOA 레코드 집합 hello 영역 루트에서 삭제할 수 없습니다 (`-Name "@"`).</span><span class="sxs-lookup"><span data-stu-id="08f06-237">You cannot delete hello SOA and NS record sets at hello zone apex (`-Name "@"`).</span></span>  <span data-ttu-id="08f06-238">Hello 영역을 만든 시간 및 hello 영역 삭제 될 때 자동으로 삭제 됩니다 때 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-238">These are created automatically when hello zone was created, and are deleted automatically when hello zone is deleted.</span></span>

<span data-ttu-id="08f06-239">hello 다음 예에서는 삭제 hello 레코드 명명 된 집합 *www* hello 영역에서 a 형식의 *contoso.com* 리소스 그룹에 *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="08f06-239">hello following example deletes hello record set named *www* of type A from hello zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

<span data-ttu-id="08f06-240">입력 정보 요청된 tooconfirm hello 삭제 작업이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-240">You are prompted tooconfirm hello delete operation.</span></span> <span data-ttu-id="08f06-241">toosuppress이 프롬프트를 사용 하 여 hello `--quiet` 스위치 (약식 `-q`).</span><span class="sxs-lookup"><span data-stu-id="08f06-241">toosuppress this prompt, use hello `--quiet` switch (short form `-q`).</span></span>

## <a name="next-steps"></a><span data-ttu-id="08f06-242">다음 단계</span><span class="sxs-lookup"><span data-stu-id="08f06-242">Next steps</span></span>

<span data-ttu-id="08f06-243">[Azure DNS의 영역 및 레코드](dns-zones-records.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="08f06-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="08f06-244">너무 방법에 대해 알아봅니다[영역 및 레코드 보호](dns-protect-zones-recordsets.md) Azure DNS를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="08f06-244">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
