---
title: "데이터 관리 게이트웨이에 대 한 aaaRelease 노트 | Microsoft Docs"
description: "데이터 관리 게이트웨이 릴리스 정보"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="f1e36-103">데이터 관리 게이트웨이에 대한 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="f1e36-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="f1e36-104">최신 데이터 통합에 대 한 hello 과제 중 하나에서 온-프레미스 toocloud toomove 데이터 tooand입니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-104">One of hello challenges for modern data integration is toomove data tooand from on-premises toocloud.</span></span> <span data-ttu-id="f1e36-105">데이터 팩터리 하면 데이터 관리 게이트웨이 온-프레미스 tooenable 하이브리드 데이터 이동의 설치할 수 있도록 하는 에이전트와의이 통합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-105">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises tooenable hybrid data movement.</span></span>

<span data-ttu-id="f1e36-106">Hello 문서 데이터 관리 게이트웨이 대 한 자세한 내용은 다음 참조와 방법을 toouse 하기:</span><span class="sxs-lookup"><span data-stu-id="f1e36-106">See hello following articles for detailed information about Data Management Gateway and how toouse it:</span></span>

*  [<span data-ttu-id="f1e36-107">데이터 관리 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="f1e36-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="f1e36-108">Azure 데이터 팩터리를 사용하여 온-프레미스 및 클라우드 간 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="f1e36-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a><span data-ttu-id="f1e36-109">현재 버전(2.10.6347.7)</span><span class="sxs-lookup"><span data-stu-id="f1e36-109">CURRENT VERSION (2.10.6347.7)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="f1e36-110">향상된 기능</span><span class="sxs-lookup"><span data-stu-id="f1e36-110">Enhancements-</span></span>
- <span data-ttu-id="f1e36-111">추가할 수 있습니다 허용 목록이 하지 않고 DNS 항목이 toowhitelist 서비스 버스 Azure IP 주소의 모든 방화벽에서 (필요한 경우).</span><span class="sxs-lookup"><span data-stu-id="f1e36-111">You can add DNS entries toowhitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="f1e36-112">Azure Portal에서 각각의 DNS 항목을 찾을 수 있습니다(Data Factory -> '작성자 및 배포' -> '게이트웨이' -> JSON의 “serviceUrls”).</span><span class="sxs-lookup"><span data-stu-id="f1e36-112">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="f1e36-113">이제 HDFS 커넥터는 SSL 유효성 검사를 건너뛸 수 있도록 하여 자체 서명된 공용 인증서를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-113">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="f1e36-114">업데이트 (기한 tooclock 오차) 하는 동안 오프 라인으로 게이트웨이 통해 문제를 수정된:</span><span class="sxs-lookup"><span data-stu-id="f1e36-114">Fixed: Issue with gateway offline during update (due tooclock skew)</span></span>



## <a name="earlier-versions"></a><span data-ttu-id="f1e36-115">이전 버전</span><span class="sxs-lookup"><span data-stu-id="f1e36-115">Earlier versions</span></span>

## <a name="2963132"></a><span data-ttu-id="f1e36-116">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="f1e36-116">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="f1e36-117">향상된 기능</span><span class="sxs-lookup"><span data-stu-id="f1e36-117">Enhancements-</span></span>
-   <span data-ttu-id="f1e36-118">추가할 수 있습니다 허용 목록이 하지 않고 DNS 항목이 toowhitelist 서비스 버스 Azure IP 주소의 모든 방화벽에서 (필요한 경우).</span><span class="sxs-lookup"><span data-stu-id="f1e36-118">You can add DNS entries toowhitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="f1e36-119">자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1e36-119">More details here.</span></span>
-   <span data-ttu-id="f1e36-120">이제 too4.75 TB는 블록 blob의 hello 최대 지원 크기를 단일 블록 blob에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-120">You can now copy data to/from a single block blob up too4.75 TB, which is hello max supported size of block blob.</span></span> <span data-ttu-id="f1e36-121">이전에는 195GB까지로 제한되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-121">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="f1e36-122">복사 작업 중 작은 파일 여러 개의 압축을 푸는 동안 발생하는 메모리 부족 문제가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-122">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="f1e36-123">고정된: 인덱스가 문서 DB tooan에서 복사 하는 동안 문제 범위를 벗어났습니다. 온-프레미스 SQL Server 멱 기능.</span><span class="sxs-lookup"><span data-stu-id="f1e36-123">Fixed: Index out of range issue while copying from Document DB tooan on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="f1e36-124">SQL 정리 스크립트가 복사 마법사에서 온-프레미스 SQL Server와 작동하지 않는 문제가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-124">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="f1e36-125">고정: hello 끝에 공간이 있는 열 이름에서에서 작동 하지 않습니다 복사 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-125">Fixed: Column name with space at hello end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="f1e36-126">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="f1e36-126">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="f1e36-127">향상된 기능</span><span class="sxs-lookup"><span data-stu-id="f1e36-127">Enhancements-</span></span>
- <span data-ttu-id="f1e36-128">게이트웨이 컴퓨터를 다시 부팅할 때 자격 증명이 누락되는 문제가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-128">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="f1e36-129">백업 파일을 사용하여 게이트웨이를 복원하는 중에 발생하는 등록 문제가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-129">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="f1e36-130">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-130">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="f1e36-131">향상된 기능</span><span class="sxs-lookup"><span data-stu-id="f1e36-131">Enhancements-</span></span>
- <span data-ttu-id="f1e36-132">Oracle에서 10진수 null 값을 원본으로 잘못 읽는 문제가 수정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-132">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="f1e36-133">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="f1e36-133">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="f1e36-134">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="f1e36-134">What’s new</span></span>
- <span data-ttu-id="f1e36-135">고객이 게이트웨이 등록 경험에 대한 피드백을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-135">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="f1e36-136">새 압축 형식 지원: ZIP (Deflate)</span><span class="sxs-lookup"><span data-stu-id="f1e36-136">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="f1e36-137">향상된 기능</span><span class="sxs-lookup"><span data-stu-id="f1e36-137">Enhancements-</span></span>
- <span data-ttu-id="f1e36-138">Oracle Sink, HDFS 원본에 대한 성능 개선</span><span class="sxs-lookup"><span data-stu-id="f1e36-138">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="f1e36-139">게이트웨이 자동 업데이트, 게이트웨이 병렬 처리 용량에 대한 버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-139">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="f1e36-140">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-140">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="f1e36-141">향상된 기능</span><span class="sxs-lookup"><span data-stu-id="f1e36-141">Enhancements</span></span>
- <span data-ttu-id="f1e36-142">보다 강력 하 고 향상 된 게이트웨이 등록 경험-이제 응답성 hello 등록 경험을 낮추는 hello 게이트웨이 등록 프로세스 중 진행 상태를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-142">Improved and more robust Gateway registration experience- Now you can track progress status during hello Gateway registration process, which makes hello registration experience more responsive.</span></span>
- <span data-ttu-id="f1e36-143">이 업데이트 된 hello 게이트웨이 백업 파일이 없는 경우에 게이트웨이 복원 프로세스-있습니다 향상 게이트웨이 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-143">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have hello gateway backup file with this update.</span></span> <span data-ttu-id="f1e36-144">이 포털에서 tooreset 연결 된 서비스 자격 증명을 요구 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-144">This would require you tooreset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="f1e36-145">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-145">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="f1e36-146">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-146">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="f1e36-147">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="f1e36-147">What’s new</span></span>

- <span data-ttu-id="f1e36-148">이제 데이터 원본 자격 증명을 로컬로 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-148">You can now store data source credentials locally.</span></span> <span data-ttu-id="f1e36-149">hello 자격 증명은 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-149">hello credentials are encrypted.</span></span> <span data-ttu-id="f1e36-150">hello 데이터 원본 자격 증명 복구할 수 있습니다 및 기존의 모든 온-프레미스 게이트웨이 hello에서 내보낼 수 있는 hello 백업 파일을 사용 하 여 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-150">hello data source credentials can be recovered and restored using hello backup file that can be exported from hello existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="f1e36-151">향상된 기능</span><span class="sxs-lookup"><span data-stu-id="f1e36-151">Enhancements-</span></span>

- <span data-ttu-id="f1e36-152">더 강력하게 향상된 게이트웨이 등록 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-152">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="f1e36-153">복사 마법사를 텍스트 형식에 대 한 QuoteChar 구성의 자동 검색을 지원 하 고 hello 개선 전체 검색 정확도 서식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-153">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve hello overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="f1e36-154">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="f1e36-154">2.3.6100.2</span></span>

- <span data-ttu-id="f1e36-155">온-프레미스 파일 시스템 및 HDFS의 텍스트 파일에 대해 복사 마법사의 firstRowAsHeader 및 SkipLineCount 자동 검색을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-155">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="f1e36-156">서비스 버스와 게이트웨이 간의 네트워크 연결의 hello 안정성 향상</span><span class="sxs-lookup"><span data-stu-id="f1e36-156">Enhance hello stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="f1e36-157">몇 가지 버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-157">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="f1e36-158">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-158">2.2.6072.1</span></span>

*  <span data-ttu-id="f1e36-159">Hello 게이트웨이 구성 관리자를 사용 하 여 hello 게이트웨이에 대 한 HTTP 프록시를 설정할 수 있도록 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-159">Supports setting HTTP proxy for hello gateway using hello Gateway Configuration Manager.</span></span> <span data-ttu-id="f1e36-160">Azure Blob, Azure 테이블, Azure Data Lake 및 DocumentDB가 구성되어 있는 경우 HTTP 프록시를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-160">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="f1e36-161">데이터를 복사 하는 경우 TextFormat에 대 한 처리는 지원 헤더 tooAzure Blob, Azure 데이터 레이크 저장소 온-프레미스 파일 시스템 및 온-프레미스 HDFS /입니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-161">Supports header handling for TextFormat when copying data from/tooAzure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="f1e36-162">블록 Blob는 지원 데이터 복사 추가 Blob 및 페이지 Blob에서 hello와 함께 이미 하도록 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-162">Supports copying data from Append Blob and Page Blob along with hello already supported Block Blob.</span></span>
*  <span data-ttu-id="f1e36-163">새 게이트웨이 상태를 소개 **온라인 (제한 됨)**, 복사 마법사에 대 한 hello 대화형 작업 지원을 제외 하 고 작동 하는 hello 게이트웨이의 해당 hello 주요 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-163">Introduces a new gateway status **Online (Limited)**, which indicates that hello main functionality of hello gateway works except hello interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="f1e36-164">등록 키를 사용 하 여 게이트웨이 등록의 hello 견고성을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-164">Enhances hello robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="f1e36-165">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="f1e36-165">2.1.6040.</span></span>

*  <span data-ttu-id="f1e36-166">DB2 드라이버가 지금 hello 게이트웨이 설치 패키지에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-166">DB2 driver is included in hello gateway installation package now.</span></span> <span data-ttu-id="f1e36-167">Tooinstall 필요가 없습니다 것 별도로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-167">You do not need tooinstall it separately.</span></span>
*  <span data-ttu-id="f1e36-168">Z/OS 용 DB2 및 DB2 driver에서는 이제 i (AS / 400) hello 이미 지원 되는 플랫폼 (Linux, Unix 및 Windows)와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-168">DB2 driver now supports z/OS and DB2 for i (AS/400) along with hello platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="f1e36-169">온-프레미스 데이터 저장소에 대한 Azure Cosmos DB를 원본 또는 대상으로 사용하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-169">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="f1e36-170">범용 저장소 계정을 지원 하는 hello와 함께 데이터에서 / toocold/핫 blob 저장소에 이미 복사 하도록 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-170">Supports copying data from/toocold/hot blob storage along with hello already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="f1e36-171">Tooconnect tooon 온-프레미스 사용 하면 원격 로그인 권한 사용 하 여 게이트웨이 통해 SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f1e36-171">Allows you tooconnect tooon-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="f1e36-172">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-172">2.0.6013.1</span></span>

*  <span data-ttu-id="f1e36-173">수동 설치 하는 동안 한 게이트웨이에서 사용 되는 hello 언어/문화권 toobe를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-173">You can select hello language/culture toobe used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="f1e36-174">게이트웨이가 예상 대로 작동 하지 않으면 마지막 7 일 tooMicrosoft toofacilitate 문제 해결의 hello 문제의 toosend 게이트웨이 로그 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-174">When gateway does not work as expected, you can choose toosend gateway logs of last seven days tooMicrosoft toofacilitate troubleshooting of hello issue.</span></span> <span data-ttu-id="f1e36-175">게이트웨이 사용할 경우 연결 된 toohello 클라우드 서비스 게이트웨이 로그를 보관 한 toosave 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-175">If gateway is not connected toohello cloud service, you can choose toosave and archive gateway logs.</span></span>  

*  <span data-ttu-id="f1e36-176">게이트웨이 구성 관리자에 대한 사용자 인터페이스 개선 사항:</span><span class="sxs-lookup"><span data-stu-id="f1e36-176">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="f1e36-177">Hello 홈 탭에 더 많은 보이는 게이트웨이 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-177">Make gateway status more visible on hello Home tab.</span></span>

    *  <span data-ttu-id="f1e36-178">재구성되고 간소화된 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-178">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="f1e36-179">Hello를 사용 하 여 저장소에서 데이터를 복사할 수 [복사 코드 필요 없는 미리 보기 도구](data-factory-copy-data-wizard-tutorial.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-179">You can copy data from a storage using hello [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="f1e36-180">이 기능에 대한 전반적인 세부 정보는 [준비된 복사](data-factory-copy-activity-performance.md#staged-copy) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1e36-180">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="f1e36-181">Azure 기계 학습에는 온-프레미스 SQL Server 데이터베이스에서 직접 데이터 관리 게이트웨이 tooingress 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-181">You can use Data Management Gateway tooingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="f1e36-182">성능 개선</span><span class="sxs-lookup"><span data-stu-id="f1e36-182">Performance improvements</span></span>

    * <span data-ttu-id="f1e36-183">코드가 없는 미리 보기 도구의 SQL Server에 대해 스키마/미리 보기 보기의 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-183">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="f1e36-184">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-184">1.12.5953.1</span></span>

*  <span data-ttu-id="f1e36-185">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-185">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="f1e36-186">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-186">1.11.5918.1</span></span>

*  <span data-ttu-id="f1e36-187">Hello 게이트웨이 이벤트 로그의 최대 크기를 MB too40 1MB에서 증가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-187">Maximum size of hello gateway event log has been increased from 1 MB too40 MB.</span></span>

*  <span data-ttu-id="f1e36-188">게이트웨이를 자동 업데이트하는 동안 다시 시작이 필요하면 경고 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-188">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="f1e36-189">나중에 또는 다음 toorestart 오른쪽을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-189">You can choose toorestart right then or later.</span></span>

*  <span data-ttu-id="f1e36-190">자동 업데이트가 실패하면 게이트웨이 설치 관리자는 자동 업데이트를 최대 3회까지 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-190">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="f1e36-191">성능 개선</span><span class="sxs-lookup"><span data-stu-id="f1e36-191">Performance improvements</span></span>

    * <span data-ttu-id="f1e36-192">코드가 없는 복사 시나리오를 통해 온-프레미스 서버의 큰 테이블을 로드하는 성능을 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-192">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="f1e36-193">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-193">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="f1e36-194">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-194">1.10.5892.1</span></span>

*  <span data-ttu-id="f1e36-195">성능 개선</span><span class="sxs-lookup"><span data-stu-id="f1e36-195">Performance improvements</span></span>

*  <span data-ttu-id="f1e36-196">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-196">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="f1e36-197">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="f1e36-197">1.9.5865.2</span></span>

*  <span data-ttu-id="f1e36-198">0 터치 자동 업데이트 기능</span><span class="sxs-lookup"><span data-stu-id="f1e36-198">Zero touch auto update capability</span></span>
*  <span data-ttu-id="f1e36-199">게이트웨이 상태 표시기 포함 새 트레이 아이콘</span><span class="sxs-lookup"><span data-stu-id="f1e36-199">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="f1e36-200">기능 너무 "지금 업데이트" hello 클라이언트에서</span><span class="sxs-lookup"><span data-stu-id="f1e36-200">Ability too“Update now” from hello client</span></span>
*  <span data-ttu-id="f1e36-201">기능 tooset 업데이트 일정 시간</span><span class="sxs-lookup"><span data-stu-id="f1e36-201">Ability tooset update schedule time</span></span>
*  <span data-ttu-id="f1e36-202">자동 업데이트를 설정/해제하기 위한 PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="f1e36-202">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="f1e36-203">JSON 형식 파일 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-203">Support for JSON format</span></span>  
*  <span data-ttu-id="f1e36-204">성능 개선</span><span class="sxs-lookup"><span data-stu-id="f1e36-204">Performance improvements</span></span>
*  <span data-ttu-id="f1e36-205">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-205">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="f1e36-206">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-206">1.8.5822.1</span></span>

*  <span data-ttu-id="f1e36-207">문제 해결 환경 개선</span><span class="sxs-lookup"><span data-stu-id="f1e36-207">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="f1e36-208">성능 개선</span><span class="sxs-lookup"><span data-stu-id="f1e36-208">Performance improvements</span></span>
*  <span data-ttu-id="f1e36-209">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-209">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="f1e36-210">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-210">1.7.5795.1</span></span>

*  <span data-ttu-id="f1e36-211">성능 개선</span><span class="sxs-lookup"><span data-stu-id="f1e36-211">Performance improvements</span></span>
*  <span data-ttu-id="f1e36-212">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-212">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="f1e36-213">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-213">1.7.5764.1</span></span>

*  <span data-ttu-id="f1e36-214">성능 개선</span><span class="sxs-lookup"><span data-stu-id="f1e36-214">Performance improvements</span></span>
*  <span data-ttu-id="f1e36-215">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-215">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="f1e36-216">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-216">1.6.5735.1</span></span>

*  <span data-ttu-id="f1e36-217">온-프레미스 HDFS 원본/싱크 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-217">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="f1e36-218">성능 개선</span><span class="sxs-lookup"><span data-stu-id="f1e36-218">Performance improvements</span></span>
*  <span data-ttu-id="f1e36-219">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-219">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="f1e36-220">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-220">1.6.5696.1</span></span>

*  <span data-ttu-id="f1e36-221">성능 개선</span><span class="sxs-lookup"><span data-stu-id="f1e36-221">Performance improvements</span></span>
*  <span data-ttu-id="f1e36-222">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-222">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="f1e36-223">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-223">1.6.5676.1</span></span>

*  <span data-ttu-id="f1e36-224">구성 관리자에서 진단 도구 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-224">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="f1e36-225">Azure 데이터 팩터리에 대 한 테이블 데이터 원본의 테이블 열 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-225">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="f1e36-226">Azure 데이터 팩터리에 대 한 SQL DW 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-226">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="f1e36-227">Azure 데이터 팩터리에 대한 BlobSource 및 FileSource의 단독 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-227">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="f1e36-228">CopyBehavior 지원 – Azure Data Factory의 이진 복사 기능을 통해 BlobSink 및 FileSink에서 MergeFiles, PreserveHierarchy, FlattenHierarchy 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-228">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="f1e36-229">Azure 데이터 팩터리의 진행률을 보고하는 복사 작업 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-229">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="f1e36-230">Azure 데이터 팩터리에 대한 데이터 원본 연결 유효성 검사 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-230">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="f1e36-231">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-231">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="f1e36-232">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-232">1.6.5672.1</span></span>

*  <span data-ttu-id="f1e36-233">Azure 데이터 팩터리에 대 한 ODBC 데이터 원본의 테이블 이름 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-233">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="f1e36-234">성능 개선</span><span class="sxs-lookup"><span data-stu-id="f1e36-234">Performance improvements</span></span>
*  <span data-ttu-id="f1e36-235">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-235">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="f1e36-236">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-236">1.6.5658.1</span></span>

*  <span data-ttu-id="f1e36-237">Azure 데이터 팩터리에 대 한 파일 싱크 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-237">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="f1e36-238">Azure 데이터 팩터리에 대 한 이진 복사본에서 계층 구조 유지 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-238">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="f1e36-239">Azure 데이터 팩터리에 대한 복사 작업 멱등성 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-239">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="f1e36-240">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-240">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="f1e36-241">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-241">1.6.5640.1</span></span>

*  <span data-ttu-id="f1e36-242">Azure 데이터 팩터리(ODBC, OData, HDFS)에 대 한 3개 더 많은 데이터 원본 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-242">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="f1e36-243">Azure 데이터 팩터리에 대 한 csv 파서에서 따옴표 문자 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-243">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="f1e36-244">압축 지원(BZip2)</span><span class="sxs-lookup"><span data-stu-id="f1e36-244">Compression support (BZip2)</span></span>
*  <span data-ttu-id="f1e36-245">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-245">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="f1e36-246">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-246">1.5.5612.1</span></span>

*  <span data-ttu-id="f1e36-247">Azure Data Factory에 대해 관계형 데이터베이스 5개(MySQL, PostgreSQL, DB2, Teradata, Sybase) 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-247">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="f1e36-248">압축 지원(Gzip 및 Deflate)</span><span class="sxs-lookup"><span data-stu-id="f1e36-248">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="f1e36-249">성능 개선</span><span class="sxs-lookup"><span data-stu-id="f1e36-249">Performance improvements</span></span>
*  <span data-ttu-id="f1e36-250">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-250">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="f1e36-251">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-251">1.4.5549.1</span></span>

*  <span data-ttu-id="f1e36-252">Azure 데이터 팩터리에 대 한 Oracle 데이터 원본 지원 추가</span><span class="sxs-lookup"><span data-stu-id="f1e36-252">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="f1e36-253">성능 개선</span><span class="sxs-lookup"><span data-stu-id="f1e36-253">Performance improvements</span></span>
*  <span data-ttu-id="f1e36-254">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f1e36-254">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="f1e36-255">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-255">1.4.5492.1</span></span>

*  <span data-ttu-id="f1e36-256">Microsoft Azure 데이터 팩터리 및 Office 365 Power BI 서비스를 지원하는 통합 된 이진 파일</span><span class="sxs-lookup"><span data-stu-id="f1e36-256">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="f1e36-257">Hello 구성 UI 및 등록 프로세스를 구체화합니다</span><span class="sxs-lookup"><span data-stu-id="f1e36-257">Refine hello Configuration UI and registration process</span></span>
*  <span data-ttu-id="f1e36-258">Azure 데이터 팩터리 - SQL Server 데이터 원본에 대한 Azure 수신 및 송신 지원</span><span class="sxs-lookup"><span data-stu-id="f1e36-258">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="f1e36-259">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="f1e36-259">1.2.5303.1</span></span>

*  <span data-ttu-id="f1e36-260">시간 초과 문제 toosupport 보다 시간이 많이 걸리는 데이터 원본 연결을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-260">Fix timeout issue toosupport more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="f1e36-261">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="f1e36-261">1.1.5526.8</span></span>

*  <span data-ttu-id="f1e36-262">설치하는 동안 필수 요소로 .NET Framework 4.5.1이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-262">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="f1e36-263">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="f1e36-263">1.0.5144.2</span></span>

*  <span data-ttu-id="f1e36-264">Azure 데이터 팩터리 시나리오에 영향을 주는 변경은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1e36-264">No changes that affect Azure Data Factory scenarios.</span></span>
