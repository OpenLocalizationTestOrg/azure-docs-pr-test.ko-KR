---
title: "Azure CLI 1.0을 사용하여 도메인 영역 파일을 Azure DNS에 가져오기 및 내보내기 | Microsoft Docs"
description: "Azure CLI 1.0을 사용하여 Azure DNS에 DNS 영역 파일을 가져오고 내보내는 방법을 알아봅니다"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: d6d3fa7aa0e8b2462b3a6b4b66d3d87ab5535314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="import-and-export-a-dns-zone-file-using-the-azure-cli-10"></a><span data-ttu-id="fabce-103">Azure CLI 1.0을 사용하여 DNS 영역 파일 가져오기 및 내보내기</span><span class="sxs-lookup"><span data-stu-id="fabce-103">Import and export a DNS zone file using the Azure CLI 1.0</span></span> 

<span data-ttu-id="fabce-104">이 문서는 Azure CLI 1.0을 사용하여 Azure DNS에 대한 DNS 영역 파일 가져오고 내보내는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-104">This article walks you through how to import and export DNS zone files for Azure DNS using the Azure CLI 1.0.</span></span>

## <a name="introduction-to-dns-zone-migration"></a><span data-ttu-id="fabce-105">DNS 영역 마이그레이션 소개</span><span class="sxs-lookup"><span data-stu-id="fabce-105">Introduction to DNS zone migration</span></span>

<span data-ttu-id="fabce-106">DNS 영역 파일은 영역의 모든 DNS(도메인 이름 시스템) 레코드의 세부 정보를 포함하는 텍스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in the zone.</span></span> <span data-ttu-id="fabce-107">표준 형식을 따르며 이는 DNS 시스템 간에 DNS 레코드를 전송하는 데 적합하도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="fabce-108">영역 파일을 사용하는 작업은 DNS 영역을 Azure DNS으로 전송할 수 있는 신뢰할 수 있는 빠르고 편리한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-108">Using a zone file is a quick, reliable, and convenient way to transfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="fabce-109">Azure DNS는 Azure CLI(명령줄 인터페이스I)를 사용하여 영역 파일 가져오기 및 내보내기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-109">Azure DNS supports importing and exporting zone files by using the Azure command-line interface (CLI).</span></span> <span data-ttu-id="fabce-110">영역 파일 가져오기는 현재 Azure PowerShell 또는 Azure Portal을 통해 지원되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="fabce-110">Zone file import is **not** currently supported via Azure PowerShell or the Azure portal.</span></span>

<span data-ttu-id="fabce-111">Azure CLI 1.0은 Azure 서비스를 관리하는 데 사용하는 플랫폼 간 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-111">The Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="fabce-112">[Azure 다운로드 페이지](https://azure.microsoft.com/downloads/)에서 다운로드하여 Windows, Mac 및 Linux 플랫폼에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-112">It is available for the Windows, Mac, and Linux platforms from the [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="fabce-113">가장 일반적인 이름 서버 소프트웨어인 [BIND](https://www.isc.org/downloads/bind/)는 일반적으로 Linux에서 실행하기 때문에 플랫폼 간 지원은 영역 파일 가져오기 및 내보내기에 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-113">Cross-platform support is important for importing and exporting zone files, because the most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="fabce-114">현재 두 가지 버전의 Azure CLI가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-114">There are currently two versions of the Azure CLI.</span></span> <span data-ttu-id="fabce-115">CLI1.0은 Node.js를 기반으로 하며 "azure"로 시작하는 명령이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="fabce-116">CLI2.0은 Python을 기반으로 하며 "az"로 시작하는 명령이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="fabce-117">두 버전에서 영역 파일 가져오기가 지원되지만 이 페이지에서 설명하는 대로 CLI1.0 명령을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-117">While zone file import is supported in both versions, we recommend using the CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="fabce-118">기존 DNS 영역 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="fabce-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="fabce-119">Azure DNS에 DNS 영역 파일을 가져오기 전에 영역 파일의 복사본을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-119">Before you import a DNS zone file into Azure DNS, you need to obtain a copy of the zone file.</span></span> <span data-ttu-id="fabce-120">이 파일의 원본은 DNS 영역이 현재 호스팅되는 위치에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-120">The source of this file depends on where the DNS zone is currently hosted.</span></span>

* <span data-ttu-id="fabce-121">DNS 영역이 파트너 서비스에서 호스팅되는 경우(예: 도메인 등록자, 전용 DNS 호스팅 공급자 또는 다른 클라우드 공급자) 해당 서비스는 DNS 영역 파일을 다운로드하는 기능을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide the ability to download the DNS zone file.</span></span>
* <span data-ttu-id="fabce-122">사용자의 DNS 영역이 Windows DNS에서 호스팅되는 경우 영역 파일의 기본 폴더는 **%systemroot%\system32\dns**입니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-122">If your DNS zone is hosted on Windows DNS, the default folder for the zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="fabce-123">또한 각 영역 파일의 전체 경로는 DNS 콘솔의 **일반** 탭에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-123">The full path to each zone file also shows on the **General** tab of the DNS console.</span></span>
* <span data-ttu-id="fabce-124">DNS 영역이 BIND를 사용하여 호스팅되는 경우 각 영역에 대한 영역 파일의 위치는 바인딩 구성 파일 **'named.conf'**에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-124">If your DNS zone is hosted by using BIND, the location of the zone file for each zone is specified in the BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="fabce-125">GoDaddy에서 다운로드한 영역 파일은 약간 비표준 형식을 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="fabce-126">이러한 영역 파일을 Azure DNS로 가져오기 전에 이 오류를 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-126">You need to correct this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="fabce-127">각 DNS 레코드의 RDATA에서 DNS 이름은 정규화된 이름으로 지정되지만 끝에 “.”가 없습니다. 즉, 이 이름은 다른 DNS 시스템에서 상대 이름으로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-127">DNS names in the RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="fabce-128">Azure DNS로 가져오기 전에 영역 파일을 편집하여 이러한 이름에 종료하는 “.”를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-128">You need to edit the zone file to append the terminating "." to their names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="fabce-129">예를 들어 CNAME 레코드 "www 3600 IN CNAME contoso.com"을 "www 3600 IN CNAME contoso.com"으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-129">For example, the CNAME record "www 3600 IN CNAME contoso.com" should be changed to "www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="fabce-130">(끝에 "."가 있어야 함).</span><span class="sxs-lookup"><span data-stu-id="fabce-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="fabce-131">Azure DNS에 DNS 영역 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="fabce-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="fabce-132">영역이 아직 없는 경우 영역 파일을 가져오면 Azure DNS에서 새 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="fabce-133">영역이 이미 있는 경우 영역 파일의 레코드 집합은 기존 레코드 집합으로 병합되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-133">If the zone already exists, the record sets in the zone file must be merged with the existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="fabce-134">병합 동작</span><span class="sxs-lookup"><span data-stu-id="fabce-134">Merge behavior</span></span>

* <span data-ttu-id="fabce-135">기존 및 새 레코드 집합은 기본적으로 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="fabce-136">병합된 레코드 집합 내의 동일한 레코드는 중복을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="fabce-137">또는 `--force` 옵션을 지정하여 가져오기 프로세스가 기존 레코드 집합을 새 레코드 집합으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-137">Alternatively, by specifying the `--force` option, the import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="fabce-138">가져온 영역 파일에 해당 레코드 집합이 없는 기존 레코드 집합은 제거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-138">Existing record sets that do not have a corresponding record set in the imported zone file are not be removed.</span></span>
* <span data-ttu-id="fabce-139">레코드 집합을 병합하는 경우 기존 레코드 집합의 TTL(time to live)이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-139">When record sets are merged, the time to live (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="fabce-140">`--force`을(를) 사용하는 경우 새 레코드 집합의 TTL가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-140">When `--force` is used, the TTL of the new record set is used.</span></span>
* <span data-ttu-id="fabce-141">SOA(Start of Authority) 매개 변수(`host` 제외)는 `--force`의 사용에 관계 없이 항상 가져온 영역 파일에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-141">Start of Authority (SOA) parameters (except `host`) are always taken from the imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="fabce-142">마찬가지로 영역 광선의 이름 서버 레코드 집합의 경우 TTL은 항상 가져온 영역 파일에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-142">Similarly, for the name server record set at the zone apex, the TTL is always taken from the imported zone file.</span></span>
* <span data-ttu-id="fabce-143">`--force` 매개 변수를 지정하지 않는 한 가져온 CNAME 레코드는 기존 CNAME 레코드를 동일한 이름으로 바꾸지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-143">An imported CNAME record does not replace an existing CNAME record with the same name unless the `--force` parameter is specified.</span></span>
* <span data-ttu-id="fabce-144">CNAME 레코드와 이름은 같지만 형식이 다른 레코드 간에 충돌이 발생할 경우(기존 또는 새로 만든 것에 관계 없이) 기존 레코드가 보존됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-144">When a conflict arises between a CNAME record and another record of the same name but different type (regardless of which is existing or new), the existing record is retained.</span></span> <span data-ttu-id="fabce-145">`--force`의 사용과 별개입니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-145">This is independent of the use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="fabce-146">가져오기에 대한 추가 정보</span><span class="sxs-lookup"><span data-stu-id="fabce-146">Additional information about importing</span></span>

<span data-ttu-id="fabce-147">다음 정보는 영역 가져오기 프로세스에 대한 추가 기술 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-147">The following notes provide additional technical details about the zone import process.</span></span>

* <span data-ttu-id="fabce-148">`$TTL` 지시어는 선택적이며 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-148">The `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="fabce-149">`$TTL` 지시어를 지정하지 않는 경우 기본 TTL 3600초로 설정하고 명시적 TTL이 없는 레코드를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-149">When no `$TTL` directive is given, records without an explicit TTL are imported set to a default TTL of 3600 seconds.</span></span> <span data-ttu-id="fabce-150">동일한 레코드 집합의 두 레코드가 다른 TTL을 지정하는 경우 낮은 값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-150">When two records in the same record set specify different TTLs, the lower value is used.</span></span>
* <span data-ttu-id="fabce-151">`$ORIGIN` 지시어는 선택적이며 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-151">The `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="fabce-152">`$ORIGIN` 을(를) 설정하지 않는 경우 사용된 기본 값은 명령줄에 지정된 영역 이름입니다(그리고 종료하는 ".").</span><span class="sxs-lookup"><span data-stu-id="fabce-152">When no `$ORIGIN` is set, the default value used is the zone name as specified on the command line (plus the terminating ".").</span></span>
* <span data-ttu-id="fabce-153">`$INCLUDE` 및 `$GENERATE` 지시어는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-153">The `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="fabce-154">A, AAAA, CNAME, MX, NS, SOA, SRV, TXT 등의 레코드 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="fabce-155">SOA 레코드는 영역이 만들어질 때 Azure DNS에서 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-155">The SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="fabce-156">영역 파일을 가져오는 경우 `host` 매개 변수를 *제외한* 모든 SOA 매개 변수는 영역 파일에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-156">When you import a zone file, all SOA parameters are taken from the zone file *except* the `host` parameter.</span></span> <span data-ttu-id="fabce-157">이 매개 변수는 Azure DNS에서 제공 되는 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-157">This parameter uses the value provided by Azure DNS.</span></span> <span data-ttu-id="fabce-158">이 매개 변수가 Azure DNS에서 제공하는 기본 이름 서버를 참조해야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-158">This is because this parameter must refer to the primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="fabce-159">또한 영역을 만들 때 역영 광선의 이름 서버 레코드 집합은 Azure DNS에서 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-159">The name server record set at the zone apex is also created automatically by Azure DNS when the zone is created.</span></span> <span data-ttu-id="fabce-160">이 레코드 집합의 TTL만을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-160">Only the TTL of this record set is imported.</span></span> <span data-ttu-id="fabce-161">이러한 레코드는 Azure DNS에서 제공하는 이름 서버 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-161">These records contain the name server names provided by Azure DNS.</span></span> <span data-ttu-id="fabce-162">레코드 데이터를 가져온 영역 파일에 포함된 값으로 덮어쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-162">The record data is not overwritten by the values contained in the imported zone file.</span></span>
* <span data-ttu-id="fabce-163">공개 미리 보기 중에 Azure DNS는 단일 문자 TXT 레코드만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="fabce-164">다중 문자열 TXT 레코드는 연결되어 255자로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-164">Multistring TXT records are be concatenated and truncated to 255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="fabce-165">CLI 형식 및 값</span><span class="sxs-lookup"><span data-stu-id="fabce-165">CLI format and values</span></span>

<span data-ttu-id="fabce-166">DNS 영역을 가져오는 Azure CLI 명령 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-166">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="fabce-167">값</span><span class="sxs-lookup"><span data-stu-id="fabce-167">Values:</span></span>

* <span data-ttu-id="fabce-168">`<resource group>` 은(는) Azure DNS의 영역에 대한 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-168">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="fabce-169">`<zone name>` 은(는) 영역의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-169">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="fabce-170">`<zone file name>` 은(는) 가져올 영역 파일의 경로/이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-170">`<zone file name>` is the path/name of the zone file to be imported.</span></span>

<span data-ttu-id="fabce-171">이 이름이 있는 영역이 리소스 그룹에 없는 경우 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-171">If a zone with this name does not exist in the resource group, it is created for you.</span></span> <span data-ttu-id="fabce-172">영역이 이미 있는 경우 가져온 레코드 집합은 기존 레코드 집합으로 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-172">If the zone already exists, the imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="fabce-173">기존 레코드 집합을 덮어쓰려면 `--force` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-173">To overwrite the existing record sets, use the `--force` option.</span></span>

<span data-ttu-id="fabce-174">영역 파일을 실제로 가져오지 않고 영역 파일의 유효성을 검사하려면 `--parse-only` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-174">To verify the format of a zone file without actually importing it, use the `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="fabce-175">1단계.</span><span class="sxs-lookup"><span data-stu-id="fabce-175">Step 1.</span></span> <span data-ttu-id="fabce-176">영역 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="fabce-176">Import a zone file</span></span>

<span data-ttu-id="fabce-177">**contoso.com**영역에 대한 영역 파일을 가져오려면</span><span class="sxs-lookup"><span data-stu-id="fabce-177">To import a zone file for the zone **contoso.com**.</span></span>

1. <span data-ttu-id="fabce-178">Azure CLI 1.0을 사용하여 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-178">Sign in to your Azure subscription by using the Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="fabce-179">새 DNS 영역을 만들려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-179">Select the subscription where you want to create your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="fabce-180">Azure DNS는 Azure 리소스 관리자 전용 서비스입니다. Azure CLI는 리소스 관리자 모드로 전환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-180">Azure DNS is an Azure Resource Manager-only service, so the Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="fabce-181">Azure DNS 서비스를 사용하기 전에 구독을 등록하여 Microsoft.Network 리소스 공급자를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-181">Before you use the Azure DNS service, you must register your subscription to use the Microsoft.Network resource provider.</span></span> <span data-ttu-id="fabce-182">(이 작업은 각 구독에 대해 한 번만 수행하면 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="fabce-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="fabce-183">또한 Resource Manager 리소스 그룹이 없는 경우 해당 리소스 그룹을 만들어야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-183">If you don't have one already, you also need to create a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="fabce-184">**contoso.com.txt** 파일에서 **myresourcegroup** 리소스 그룹의 새 DNS 영역으로 **contoso.com** 영역을 가져오려면 `azure network dns zone import` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-184">To import the zone **contoso.com** from the file **contoso.com.txt** into a new DNS zone in the resource group **myresourcegroup**, run the command `azure network dns zone import`.</span></span><BR><span data-ttu-id="fabce-185">이 명령은 영역 파일을 로드하여 구문을 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-185">This command loads the zone file and parse it.</span></span> <span data-ttu-id="fabce-186">이 명령은 Azure DNS 서비스에서 일련의 명령을 실행하여 영역 및 영역의 모든 레코드 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-186">The command executes a series of commands on the Azure DNS service to create the zone and all the record sets in the zone.</span></span> <span data-ttu-id="fabce-187">이 명령은 모든 오류 또는 경고뿐만 아니라 콘솔 창에 진행률도 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-187">The command reports progress in the console window, along with any errors or warnings.</span></span> <span data-ttu-id="fabce-188">레코드 집합이 계열에 만들어지기 때문에 큰 영역 파일을 가져오는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-188">Because record sets are created in series, it may take a few minutes to import a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-the-zone"></a><span data-ttu-id="fabce-189">2단계.</span><span class="sxs-lookup"><span data-stu-id="fabce-189">Step 2.</span></span> <span data-ttu-id="fabce-190">영역 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="fabce-190">Verify the zone</span></span>

<span data-ttu-id="fabce-191">파일을 가져온 후에 DNS 영역의 유효성을 검사하기 위해서, 다음 방법 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-191">To verify the DNS zone after you import the file, you can use any one of the following methods:</span></span>

* <span data-ttu-id="fabce-192">다음 Azure CLI 명령을 사용하여 레코드를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-192">You can list the records by using the following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="fabce-193">PowerShell cmdlet `Get-AzureRmDnsRecordSet`를 사용하여 레코드를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-193">You can list the records by using the PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="fabce-194">`nslookup` 을 사용하여 레코드에 대한 이름 확인의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-194">You can use `nslookup` to verify name resolution for the records.</span></span> <span data-ttu-id="fabce-195">영역이 아직 위임되지 않았기 때문에 올바른 Azure DNS 이름 서버를 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-195">Because the zone isn't delegated yet, you need to specify the correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="fabce-196">다음 샘플은 영역에 할당된 이름 서버 이름을 검색하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-196">The following sample shows how to retrieve the name server names assigned to the zone.</span></span> <span data-ttu-id="fabce-197">또한 IT는 `nslookup`을(를) 사용하여 "www" 레코드를 쿼리 하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-197">IT also shows how to query the "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up the DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="fabce-198">3단계.</span><span class="sxs-lookup"><span data-stu-id="fabce-198">Step 3.</span></span> <span data-ttu-id="fabce-199">DNS 위임 업데이트</span><span class="sxs-lookup"><span data-stu-id="fabce-199">Update DNS delegation</span></span>

<span data-ttu-id="fabce-200">영역을 올바르게 가져왔는지 확인한 후 Azure DNS 이름 서버를 가리키도록 DNS 위임을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-200">After you have verified that the zone has been imported correctly, you need to update the DNS delegation to point to the Azure DNS name servers.</span></span> <span data-ttu-id="fabce-201">자세한 내용은 [DNS 위임 업데이트](dns-domain-delegation.md)문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fabce-201">For more information, see the article [Update the DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="fabce-202">Azure DNS에서 DNS 영역 파일 내보내기</span><span class="sxs-lookup"><span data-stu-id="fabce-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="fabce-203">DNS 영역을 가져오는 Azure CLI 명령 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-203">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="fabce-204">값</span><span class="sxs-lookup"><span data-stu-id="fabce-204">Values:</span></span>

* <span data-ttu-id="fabce-205">`<resource group>` 은(는) Azure DNS의 영역에 대한 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-205">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="fabce-206">`<zone name>` 은(는) 영역의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-206">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="fabce-207">`<zone file name>` 은(는) 내보낼 영역 파일의 경로/이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-207">`<zone file name>` is the path/name of the zone file to be exported.</span></span>

<span data-ttu-id="fabce-208">영역 가져오기와 마찬가지로 먼저 로그인하고 구독을 선택한 다음 리소스 관리자 모드를 사용하도록 Azure CLI를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-208">As with the zone import, you first need to sign in, choose your subscription, and configure the Azure CLI to use Resource Manager mode.</span></span>

### <a name="to-export-a-zone-file"></a><span data-ttu-id="fabce-209">영역 파일을 내보내려면</span><span class="sxs-lookup"><span data-stu-id="fabce-209">To export a zone file</span></span>

1. <span data-ttu-id="fabce-210">Azure CLI를 사용하여 Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-210">Sign in to your Azure subscription by using the Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="fabce-211">DNS 영역을 만들려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-211">Select the subscription where you want to create your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="fabce-212">Azure DNS는 Azure 리소스 관리자 전용 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="fabce-213">Azure CLI는 리소스 관리자 모드로 전환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-213">The Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="fabce-214">**myresourcegroup** 리소스 그룹의 기존 **contoso.com** Azure DNS 영역을 현재 폴더의 **contoso.com.txt** 파일로 내보내려면 `azure network dns zone export` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-214">To export the existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** to the file **contoso.com.txt** (in the current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="fabce-215">이 명령은 Azure DNS 서비스를 호출하여 영역에서 레코드 집합을 열거하고 BIND와 호환 가능한 영역 파일에 결과를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fabce-215">This command  calls the Azure DNS service to enumerate record sets in the zone and export the results to a BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
