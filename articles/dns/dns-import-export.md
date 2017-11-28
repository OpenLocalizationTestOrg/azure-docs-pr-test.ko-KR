---
title: "파일 tooAzure Azure CLI 1.0을 사용 하 여 DNS aaaImport와 내보내기 도메인 영역 | Microsoft Docs"
description: "어떻게 tooimport 및 내보내기는 DNS 영역 파일 tooAzure DNS Azure CLI 1.0을 사용 하 여 알아봅니다"
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
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a><span data-ttu-id="203c2-103">Hello Azure CLI 1.0을 사용 하 여 DNS 영역 파일 가져오기 및 내보내기</span><span class="sxs-lookup"><span data-stu-id="203c2-103">Import and export a DNS zone file using hello Azure CLI 1.0</span></span> 

<span data-ttu-id="203c2-104">이 문서 tooimport 및 내보내기 DNS 영역 파일을 Azure DNS를 사용 하 여 Azure CLI 1.0 hello 하는 방법을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-104">This article walks you through how tooimport and export DNS zone files for Azure DNS using hello Azure CLI 1.0.</span></span>

## <a name="introduction-toodns-zone-migration"></a><span data-ttu-id="203c2-105">소개 tooDNS 영역 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="203c2-105">Introduction tooDNS zone migration</span></span>

<span data-ttu-id="203c2-106">DNS 영역 파일은 hello 영역의 모든 이름을 DNS (도메인) 레코드의 세부 정보가 포함 된 텍스트 파일.</span><span class="sxs-lookup"><span data-stu-id="203c2-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in hello zone.</span></span> <span data-ttu-id="203c2-107">표준 형식을 따르며 이는 DNS 시스템 간에 DNS 레코드를 전송하는 데 적합하도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="203c2-108">영역 파일을 사용 하 여 며 빠른, 신뢰할 수 있는 편리한 방법 tootransfer DNS 영역 내부 또는 외부로 Azure DNS 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-108">Using a zone file is a quick, reliable, and convenient way tootransfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="203c2-109">Azure DNS 파일 가져오기 및 내보내기 영역 hello Azure CLI (명령줄 인터페이스)를 사용 하 여 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-109">Azure DNS supports importing and exporting zone files by using hello Azure command-line interface (CLI).</span></span> <span data-ttu-id="203c2-110">영역 파일 가져오기는 **하지** hello Azure 포털 또는 Azure PowerShell을 통해 현재 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-110">Zone file import is **not** currently supported via Azure PowerShell or hello Azure portal.</span></span>

<span data-ttu-id="203c2-111">hello Azure CLI 1.0은 Azure 서비스 관리에 사용 되는 플랫폼 간 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-111">hello Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="203c2-112">Hello에서 hello Windows, Mac 및 Linux 플랫폼에 사용할 수 [Azure 다운로드 페이지](https://azure.microsoft.com/downloads/)합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-112">It is available for hello Windows, Mac, and Linux platforms from hello [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="203c2-113">가져오기 및 영역 파일을 내보내는 hello 가장 일반적인 이름 서버 소프트웨어에 대 한 플랫폼 간 지원 반드시 [바인딩할](https://www.isc.org/downloads/bind/), 일반적으로 Linux에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-113">Cross-platform support is important for importing and exporting zone files, because hello most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="203c2-114">현재 hello Azure CLI의 버전은 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-114">There are currently two versions of hello Azure CLI.</span></span> <span data-ttu-id="203c2-115">CLI1.0은 Node.js를 기반으로 하며 "azure"로 시작하는 명령이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="203c2-116">CLI2.0은 Python을 기반으로 하며 "az"로 시작하는 명령이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="203c2-117">영역 파일 가져오기는 두 버전에서에서 지원 되지만, 권장 hello CLI1.0 명령을 사용 하 여이 페이지에 설명 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-117">While zone file import is supported in both versions, we recommend using hello CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="203c2-118">기존 DNS 영역 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="203c2-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="203c2-119">Azure DNS로 DNS 영역 파일을 가져오기 전에 tooobtain hello 영역 파일의 복사본을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-119">Before you import a DNS zone file into Azure DNS, you need tooobtain a copy of hello zone file.</span></span> <span data-ttu-id="203c2-120">이 파일의 원본을 hello hello DNS 영역이 현재 호스트 된 위치에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-120">hello source of this file depends on where hello DNS zone is currently hosted.</span></span>

* <span data-ttu-id="203c2-121">DNS 영역에는 파트너 서비스 (예: 도메인 등록자, 전용된 DNS 호스팅 공급자 또는 다른 클라우드 공급자)에서 호스트 될 경우 해당 서비스 hello 기능 toodownload hello DNS 영역 파일을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide hello ability toodownload hello DNS zone file.</span></span>
* <span data-ttu-id="203c2-122">Hello 영역 파일에 대 한 hello 기본 폴더는 DNS 영역이 Windows DNS에 호스트 될 경우 **%systemroot%\system32\dns**합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-122">If your DNS zone is hosted on Windows DNS, hello default folder for hello zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="203c2-123">hello 전체 경로 tooeach 영역 파일 hello에도 표시 **일반** hello DNS 콘솔의 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-123">hello full path tooeach zone file also shows on hello **General** tab of hello DNS console.</span></span>
* <span data-ttu-id="203c2-124">각 영역에 대 한 hello 영역 파일의 hello 위치 hello 바인딩 구성 파일에 지정 된 DNS 영역이 BIND를 사용 하 여 호스팅되 경우 **named.conf**합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-124">If your DNS zone is hosted by using BIND, hello location of hello zone file for each zone is specified in hello BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="203c2-125">GoDaddy에서 다운로드한 영역 파일은 약간 비표준 형식을 가지고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="203c2-126">필요한 toocorrect이 Azure DNS로 이러한 영역 파일을 가져오기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-126">You need toocorrect this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="203c2-127">각 DNS 레코드의 RDATA hello에 대 한 DNS 이름을 정규화 된 이름으로 지정 되어 있지만 종료 없는 경우 "." 즉, 이 이름은 다른 DNS 시스템에서 상대 이름으로 해석됩니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-127">DNS names in hello RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="203c2-128">Tooedit hello 영역 파일 tooappend hello 종료 해야 "." tootheir Azure DNS로 가져오기 전에 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-128">You need tooedit hello zone file tooappend hello terminating "." tootheir names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="203c2-129">CNAME 레코드 "www 3600 CNAME contoso.com에서" hello 너무 하 여 변경 해야 예를 들어 "www 3600 IN CNAME contoso.com"</span><span class="sxs-lookup"><span data-stu-id="203c2-129">For example, hello CNAME record "www 3600 IN CNAME contoso.com" should be changed too"www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="203c2-130">(끝에 "."가 있어야 함).</span><span class="sxs-lookup"><span data-stu-id="203c2-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="203c2-131">Azure DNS에 DNS 영역 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="203c2-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="203c2-132">영역이 아직 없는 경우 영역 파일을 가져오면 Azure DNS에서 새 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="203c2-133">Hello 영역에 이미 있으면 hello 레코드 집합 hello 영역 파일에 병합 해야 hello 기존 레코드 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-133">If hello zone already exists, hello record sets in hello zone file must be merged with hello existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="203c2-134">병합 동작</span><span class="sxs-lookup"><span data-stu-id="203c2-134">Merge behavior</span></span>

* <span data-ttu-id="203c2-135">기존 및 새 레코드 집합은 기본적으로 병합됩니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="203c2-136">병합된 레코드 집합 내의 동일한 레코드는 중복을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="203c2-137">Hello를 지정 하 여 또는 `--force` 옵션, 가져오기 프로세스 대신 새 레코드 집합으로 설정 하는 기존 레코드 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-137">Alternatively, by specifying hello `--force` option, hello import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="203c2-138">해당 레코드가 hello 가져온된 영역 파일에 설정 하지 않은 기존 레코드 집합 제거 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-138">Existing record sets that do not have a corresponding record set in hello imported zone file are not be removed.</span></span>
* <span data-ttu-id="203c2-139">레코드 집합을 병합 될 때는 hello toolive TTL (time)의 기존 레코드 집합 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-139">When record sets are merged, hello time toolive (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="203c2-140">때 `--force` 는 사용 하는 hello hello 새 레코드 집합의 TTL 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-140">When `--force` is used, hello TTL of hello new record set is used.</span></span>
* <span data-ttu-id="203c2-141">SOA () 매개 변수는 시작 (제외 하 고 `host`) hello 가져온된 영역 파일에 있는 여부에 관계 없이 항상 취해집니다 `--force` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-141">Start of Authority (SOA) parameters (except `host`) are always taken from hello imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="203c2-142">마찬가지로, hello 이름 서버 레코드 hello 영역 루트에서 설정에 대 한 hello TTL은 항상 파일에서 가져온 hello 가져온된 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-142">Similarly, for hello name server record set at hello zone apex, hello TTL is always taken from hello imported zone file.</span></span>
* <span data-ttu-id="203c2-143">기존 CNAME 가져온된 CNAME 레코드를 대체 하지 않습니다 hello 하지 않는 한 이름과 같은 이름을 hello를 사용 하 여 기록 `--force` 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-143">An imported CNAME record does not replace an existing CNAME record with hello same name unless hello `--force` parameter is specified.</span></span>
* <span data-ttu-id="203c2-144">CNAME 레코드가 다른 레코드 사이 충돌이 발생 하는 경우 hello 다르지만 이름과 같은 이름을 입력 (하는 기존에 관계 없이 또는 새), hello 기존 레코드 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-144">When a conflict arises between a CNAME record and another record of hello same name but different type (regardless of which is existing or new), hello existing record is retained.</span></span> <span data-ttu-id="203c2-145">이 별개의 hello 사용 `--force`합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-145">This is independent of hello use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="203c2-146">가져오기에 대한 추가 정보</span><span class="sxs-lookup"><span data-stu-id="203c2-146">Additional information about importing</span></span>

<span data-ttu-id="203c2-147">hello 다음 참고 사항에서는 hello 영역에 대 한 추가 기술 세부 정보 가져오기 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-147">hello following notes provide additional technical details about hello zone import process.</span></span>

* <span data-ttu-id="203c2-148">hello `$TTL` 지시문은 선택적 이며 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-148">hello `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="203c2-149">No `$TTL` 지시문이 주어진 경우 명시적 TTL 없는 레코드를 가져오는 tooa 기본 TTL 3600 (초)을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-149">When no `$TTL` directive is given, records without an explicit TTL are imported set tooa default TTL of 3600 seconds.</span></span> <span data-ttu-id="203c2-150">에 두 개를 기록 하는 경우 hello 동일한 레코드 집합이 지정 다른 TTLs, hello 더 낮은 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-150">When two records in hello same record set specify different TTLs, hello lower value is used.</span></span>
* <span data-ttu-id="203c2-151">hello `$ORIGIN` 지시문은 선택적 이며 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-151">hello `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="203c2-152">No `$ORIGIN` 설정 되 면 hello 기본 사용 되는 값은 hello 명령줄에 지정 된 대로 hello 영역 이름 (hello 종료 및 ".").</span><span class="sxs-lookup"><span data-stu-id="203c2-152">When no `$ORIGIN` is set, hello default value used is hello zone name as specified on hello command line (plus hello terminating ".").</span></span>
* <span data-ttu-id="203c2-153">hello `$INCLUDE` 및 `$GENERATE` 지시문이 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-153">hello `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="203c2-154">A, AAAA, CNAME, MX, NS, SOA, SRV, TXT 등의 레코드 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="203c2-155">hello SOA 레코드는 영역을 만들면 Azure DNS에서 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-155">hello SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="203c2-156">모든 SOA 매개 변수는 hello 영역 파일에서 가져온 영역 파일을 가져올 때 *제외 하 고* hello `host` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-156">When you import a zone file, all SOA parameters are taken from hello zone file *except* hello `host` parameter.</span></span> <span data-ttu-id="203c2-157">이 매개 변수는 Azure DNS에서 제공 하는 hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-157">This parameter uses hello value provided by Azure DNS.</span></span> <span data-ttu-id="203c2-158">즉,이 매개 변수는 toohello 기본 이름 서버가 Azure DNS를 제공한 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-158">This is because this parameter must refer toohello primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="203c2-159">hello 영역 루트에서 설정 하는 hello 이름 서버 레코드가 만들어집니다 자동으로 Azure DNS에서 hello 영역을 만들 때.</span><span class="sxs-lookup"><span data-stu-id="203c2-159">hello name server record set at hello zone apex is also created automatically by Azure DNS when hello zone is created.</span></span> <span data-ttu-id="203c2-160">만 hello TTL이 레코드 집합을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-160">Only hello TTL of this record set is imported.</span></span> <span data-ttu-id="203c2-161">이러한 레코드에는 Azure DNS에서 제공 하는 hello 이름 서버 이름이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-161">These records contain hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="203c2-162">데이터를 기록 하는 hello hello 가져온된 영역 파일에 포함 된 hello 값으로 덮어쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-162">hello record data is not overwritten by hello values contained in hello imported zone file.</span></span>
* <span data-ttu-id="203c2-163">공개 미리 보기 중에 Azure DNS는 단일 문자 TXT 레코드만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="203c2-164">다중 문자열 TXT 레코드는 연결 및 잘린 too255 자가 하 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-164">Multistring TXT records are be concatenated and truncated too255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="203c2-165">CLI 형식 및 값</span><span class="sxs-lookup"><span data-stu-id="203c2-165">CLI format and values</span></span>

<span data-ttu-id="203c2-166">hello hello Azure CLI 명령 tooimport DNS 영역의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-166">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="203c2-167">값</span><span class="sxs-lookup"><span data-stu-id="203c2-167">Values:</span></span>

* <span data-ttu-id="203c2-168">`<resource group>`hello Azure dns에서 영역 hello에 대 한 hello 리소스 그룹 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-168">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="203c2-169">`<zone name>`hello hello 영역 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-169">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="203c2-170">`<zone file name>`가져온 hello 영역 파일 toobe hello 경로/이름입니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-170">`<zone file name>` is hello path/name of hello zone file toobe imported.</span></span>

<span data-ttu-id="203c2-171">이 이름 사용 하 여 영역 hello 리소스 그룹에 없는 경우 사용자에 대 한 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-171">If a zone with this name does not exist in hello resource group, it is created for you.</span></span> <span data-ttu-id="203c2-172">Hello 영역에 이미 있으면 hello 가져온된 레코드 집합이 병합 됩니다 기존 레코드 집합.</span><span class="sxs-lookup"><span data-stu-id="203c2-172">If hello zone already exists, hello imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="203c2-173">toooverwrite hello 기존 레코드 집합을 사용 하 여 hello `--force` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-173">toooverwrite hello existing record sets, use hello `--force` option.</span></span>

<span data-ttu-id="203c2-174">실제로 가져오지 않고을 사용 하 여 hello 영역 파일의 tooverify hello 형식을 `--parse-only` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-174">tooverify hello format of a zone file without actually importing it, use hello `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="203c2-175">1단계.</span><span class="sxs-lookup"><span data-stu-id="203c2-175">Step 1.</span></span> <span data-ttu-id="203c2-176">영역 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="203c2-176">Import a zone file</span></span>

<span data-ttu-id="203c2-177">tooimport hello 영역에 대 한 영역 파일 **contoso.com**합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-177">tooimport a zone file for hello zone **contoso.com**.</span></span>

1. <span data-ttu-id="203c2-178">Hello Azure CLI 1.0을 사용 하 여 Azure 구독 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-178">Sign in tooyour Azure subscription by using hello Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="203c2-179">저장할 toocreate 새 DNS 영역이 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-179">Select hello subscription where you want toocreate your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="203c2-180">Azure DNS는 Azure 리소스 관리자 전용 서비스 이므로 hello Azure CLI tooResource 전환 된 관리자 모드 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-180">Azure DNS is an Azure Resource Manager-only service, so hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="203c2-181">Hello Azure DNS 서비스를 사용 하기 전에 구독 toouse hello Microsoft.Network 리소스 공급자를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-181">Before you use hello Azure DNS service, you must register your subscription toouse hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="203c2-182">(이 작업은 각 구독에 대해 한 번만 수행하면 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="203c2-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="203c2-183">없는 경우 하나 이미, toocreate 리소스 관리자 리소스 그룹이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-183">If you don't have one already, you also need toocreate a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="203c2-184">tooimport hello 영역 **contoso.com** hello 파일에서 **contoso.com.txt** hello 리소스 그룹에 새 DNS 영역으로 **myresourcegroup**, hello 명령을 실행`azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="203c2-184">tooimport hello zone **contoso.com** from hello file **contoso.com.txt** into a new DNS zone in hello resource group **myresourcegroup**, run hello command `azure network dns zone import`.</span></span><BR><span data-ttu-id="203c2-185">이 명령은 hello 영역 파일을 로드 하 고 구문 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-185">This command loads hello zone file and parse it.</span></span> <span data-ttu-id="203c2-186">hello 명령 hello Azure DNS 서비스 toocreate hello 영역에는 일련의 명령 실행 하 고 hello 영역에서 모든 hello 레코드 집합 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-186">hello command executes a series of commands on hello Azure DNS service toocreate hello zone and all hello record sets in hello zone.</span></span> <span data-ttu-id="203c2-187">hello 명령 오류 또는 경고와 함께 hello 콘솔 창에서 진행률을 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-187">hello command reports progress in hello console window, along with any errors or warnings.</span></span> <span data-ttu-id="203c2-188">레코드 집합 계열에서 만들어지므로 큰 영역 파일을 몇 분 tooimport 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-188">Because record sets are created in series, it may take a few minutes tooimport a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a><span data-ttu-id="203c2-189">2단계.</span><span class="sxs-lookup"><span data-stu-id="203c2-189">Step 2.</span></span> <span data-ttu-id="203c2-190">Hello 영역 확인</span><span class="sxs-lookup"><span data-stu-id="203c2-190">Verify hello zone</span></span>

<span data-ttu-id="203c2-191">tooverify hello DNS 영역 hello 파일을 가져온 후 hello 메서드를 다음 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-191">tooverify hello DNS zone after you import hello file, you can use any one of hello following methods:</span></span>

* <span data-ttu-id="203c2-192">다음 Azure CLI 명령을 hello를 사용 하 여 hello 레코드를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-192">You can list hello records by using hello following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="203c2-193">Hello PowerShell cmdlet을 사용 하 여 hello 레코드를 나열할 수 있습니다 `Get-AzureRmDnsRecordSet`합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-193">You can list hello records by using hello PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="203c2-194">사용할 수 있습니다 `nslookup` hello 레코드에 대 한 tooverify 이름 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-194">You can use `nslookup` tooverify name resolution for hello records.</span></span> <span data-ttu-id="203c2-195">Hello 영역을 아직 위임 되지 않습니다, 때문에 toospecify hello 올바른 Azure DNS 이름 서버에 명시적으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-195">Because hello zone isn't delegated yet, you need toospecify hello correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="203c2-196">hello 다음 샘플에서는 tooretrieve hello 이름 서버 이름이 toohello 영역을 할당 하는 방식</span><span class="sxs-lookup"><span data-stu-id="203c2-196">hello following sample shows how tooretrieve hello name server names assigned toohello zone.</span></span> <span data-ttu-id="203c2-197">IT tooquery hello "www"를 사용 하 여 기록 하는 방법을 보여 줍니다 `nslookup`합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-197">IT also shows how tooquery hello "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
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

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="203c2-198">3단계.</span><span class="sxs-lookup"><span data-stu-id="203c2-198">Step 3.</span></span> <span data-ttu-id="203c2-199">DNS 위임 업데이트</span><span class="sxs-lookup"><span data-stu-id="203c2-199">Update DNS delegation</span></span>

<span data-ttu-id="203c2-200">Hello 영역 올바로 가져왔는지, tooupdate hello DNS 위임 toopoint toohello 필요한 확인 한 후 Azure DNS 서버 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-200">After you have verified that hello zone has been imported correctly, you need tooupdate hello DNS delegation toopoint toohello Azure DNS name servers.</span></span> <span data-ttu-id="203c2-201">자세한 내용은 hello 문서 참조 [hello DNS 위임 업데이트](dns-domain-delegation.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-201">For more information, see hello article [Update hello DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="203c2-202">Azure DNS에서 DNS 영역 파일 내보내기</span><span class="sxs-lookup"><span data-stu-id="203c2-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="203c2-203">hello hello Azure CLI 명령 tooimport DNS 영역의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-203">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="203c2-204">값</span><span class="sxs-lookup"><span data-stu-id="203c2-204">Values:</span></span>

* <span data-ttu-id="203c2-205">`<resource group>`hello Azure dns에서 영역 hello에 대 한 hello 리소스 그룹 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-205">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="203c2-206">`<zone name>`hello hello 영역 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-206">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="203c2-207">`<zone file name>`내보낸 hello 영역 파일 toobe hello 경로/이름입니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-207">`<zone file name>` is hello path/name of hello zone file toobe exported.</span></span>

<span data-ttu-id="203c2-208">Hello 영역 가져오기를 사용 하 여 먼저 toosign에 필요한, 구독을 선택 하 고 hello Azure CLI toouse Resource Manager 모드를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-208">As with hello zone import, you first need toosign in, choose your subscription, and configure hello Azure CLI toouse Resource Manager mode.</span></span>

### <a name="tooexport-a-zone-file"></a><span data-ttu-id="203c2-209">tooexport 영역 파일</span><span class="sxs-lookup"><span data-stu-id="203c2-209">tooexport a zone file</span></span>

1. <span data-ttu-id="203c2-210">Hello Azure CLI를 사용 하 여 Azure 구독 tooyour에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-210">Sign in tooyour Azure subscription by using hello Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="203c2-211">Hello 구독 저장할 toocreate DNS 영역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-211">Select hello subscription where you want toocreate your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="203c2-212">Azure DNS는 Azure 리소스 관리자 전용 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="203c2-213">hello Azure CLI tooResource 전환 된 관리자 모드 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-213">hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="203c2-214">tooexport hello 기존 Azure DNS 영역 **contoso.com** 리소스 그룹에 **myresourcegroup** toohello 파일 **contoso.com.txt** (hello 현재 폴더)을 실행 `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="203c2-214">tooexport hello existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** toohello file **contoso.com.txt** (in hello current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="203c2-215">호출 hello Azure DNS 서비스 tooenumerate이이 명령은 hello 영역에서 레코드 집합 및 hello 결과 tooa 바인딩 호환 영역 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="203c2-215">This command  calls hello Azure DNS service tooenumerate record sets in hello zone and export hello results tooa BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
