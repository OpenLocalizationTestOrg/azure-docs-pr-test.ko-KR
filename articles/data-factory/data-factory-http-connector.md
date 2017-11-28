---
title: "HTTP 소스-Azure에서에서 aaaMove 데이터 | Microsoft Docs"
description: "온-프레미스 또는 클라우드에서 HTTP toomove 데이터 원본 Azure 데이터 팩터리를 사용 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="c3652-103">Azure Data Factory를 사용하여 HTTP 소스에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="c3652-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="c3652-104">이 문서에서는 toouse hello 복사 작업에서-프레미스/클라우드 HTTP 끝점 tooa에서 Azure Data Factory toomove 데이터에서 싱크 데이터 저장소를 지원 되는 방식에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud HTTP endpoint tooa supported sink data store.</span></span> <span data-ttu-id="c3652-105">Hello를 기반으로 한이 문서 [데이터 이동 작업](data-factory-data-movement-activities.md) 원본/싱크의로 지원 되는 데이터 저장소의 복사 작업 및 hello 목록 사용 하 여 데이터 이동의 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="c3652-106">데이터 팩터리의 현재만 HTTP에서 데이터를 이동할 원본 tooother 데이터 저장소, 하지만 HTTP tooan 대상 저장 다른 데이터에서 데이터를 이동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-106">Data factory currently supports only moving data from an HTTP source tooother data stores, but not moving data from other data stores tooan HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="c3652-107">지원되는 시나리오 및 인증 형식</span><span class="sxs-lookup"><span data-stu-id="c3652-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="c3652-108">이 HTTP 커넥터 tooretrieve 데이터를 사용할 수 **클라우드와 온-프레미스 둘 다 HTTP/s 끝점** HTTP를 사용 하 여 **가져오기** 또는 **POST** 메서드.</span><span class="sxs-lookup"><span data-stu-id="c3652-108">You can use this HTTP connector tooretrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="c3652-109">hello 인증 유형만 지원 됩니다: **익명**, **기본**, **다이제스트**, **Windows**, 및  **ClientCertificate**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-109">hello following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="c3652-110">이 커넥터 및 hello hello 차이점에 주의 해야 [웹 테이블 커넥터](data-factory-web-table-connector.md) 은: hello 후자는 HTML 웹 페이지에서 콘텐츠 tooextract 사용 되는 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-110">Note hello difference between this connector and hello [Web table connector](data-factory-web-table-connector.md) is: hello latter is used tooextract table content from web HTML page.</span></span>

<span data-ttu-id="c3652-111">온-프레미스 HTTP 끝점에서 데이터를 복사할 때 hello 온-프레미스 환경/Azure VM에서에서 데이터 관리 게이트웨이 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="c3652-112">참조 [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 데이터 관리 게이트웨이 및 hello 게이트웨이 설정에 대 한 단계별 지침에 대 한 문서 toolearn 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c3652-113">시작</span><span class="sxs-lookup"><span data-stu-id="c3652-113">Getting started</span></span>
<span data-ttu-id="c3652-114">다른 도구/API를 사용하여 HTTP 원본의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="c3652-115">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-115">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="c3652-116">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="c3652-117">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-117">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c3652-118">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="c3652-119">HTTP 소스 tooAzure Blob 저장소에서에서 toocopy 데이터를 샘플링 하는 JSON, 참조 [JSON 예제](#json-examples) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="c3652-119">For JSON samples toocopy data from HTTP source tooAzure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c3652-120">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="c3652-120">Linked service properties</span></span>
<span data-ttu-id="c3652-121">다음 표에서 hello JSON 요소 특정 tooHTTP 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-121">hello following table provides description for JSON elements specific tooHTTP linked service.</span></span>

| <span data-ttu-id="c3652-122">속성</span><span class="sxs-lookup"><span data-stu-id="c3652-122">Property</span></span> | <span data-ttu-id="c3652-123">설명</span><span class="sxs-lookup"><span data-stu-id="c3652-123">Description</span></span> | <span data-ttu-id="c3652-124">필수</span><span class="sxs-lookup"><span data-stu-id="c3652-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3652-125">type</span><span class="sxs-lookup"><span data-stu-id="c3652-125">type</span></span> | <span data-ttu-id="c3652-126">hello type 속성 설정 해야 합니다: `Http`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-126">hello type property must be set to: `Http`.</span></span> | <span data-ttu-id="c3652-127">예</span><span class="sxs-lookup"><span data-stu-id="c3652-127">Yes</span></span> |
| <span data-ttu-id="c3652-128">url</span><span class="sxs-lookup"><span data-stu-id="c3652-128">url</span></span> | <span data-ttu-id="c3652-129">기본 URL toohello 웹 서버</span><span class="sxs-lookup"><span data-stu-id="c3652-129">Base URL toohello Web Server</span></span> | <span data-ttu-id="c3652-130">예</span><span class="sxs-lookup"><span data-stu-id="c3652-130">Yes</span></span> |
| <span data-ttu-id="c3652-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="c3652-131">authenticationType</span></span> | <span data-ttu-id="c3652-132">Hello 인증 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-132">Specifies hello authentication type.</span></span> <span data-ttu-id="c3652-133">허용되는 값: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="c3652-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="c3652-134">이 표 아래에 더 많은 속성 및 JSON 샘플 toosections 해당 인증 형식에 각각 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-134">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="c3652-135">예</span><span class="sxs-lookup"><span data-stu-id="c3652-135">Yes</span></span> |
| <span data-ttu-id="c3652-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="c3652-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="c3652-137">소스 HTTPS 웹 서버인 경우 tooenable 서버 SSL 인증서 유효성 검사 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-137">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="c3652-138">아니요. 기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-138">No, default is true</span></span> |
| <span data-ttu-id="c3652-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="c3652-139">gatewayName</span></span> | <span data-ttu-id="c3652-140">데이터 관리 게이트웨이 tooconnect tooan hello의 이름 온-프레미스 HTTP 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-140">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="c3652-141">온-프레미스 HTTP 소스에서 데이터를 복사하는 경우에는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="c3652-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="c3652-142">encryptedCredential</span></span> | <span data-ttu-id="c3652-143">암호화 된 자격 증명 tooaccess hello HTTP 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-143">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="c3652-144">자동 생성 된 복사 마법사 또는 hello ClickOnce 팝업 대화 상자에 hello 인증 정보를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-144">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="c3652-145">아니요.</span><span class="sxs-lookup"><span data-stu-id="c3652-145">No.</span></span> <span data-ttu-id="c3652-146">온-프레미스 HTTP 서버에서 데이터를 복사하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="c3652-147">참조 [온-프레미스 원본 및 데이터 관리 게이트웨이 사용 하는 hello 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 온-프레미스 HTTP 커넥터 데이터 원본에 대 한 자격 증명을 설정 하는 방법에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-147">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="c3652-148">Basic, Digest 또는 Windows 인증 사용</span><span class="sxs-lookup"><span data-stu-id="c3652-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="c3652-149">설정 `authenticationType` 으로 `Basic`, `Digest`, 또는 `Windows`, hello hello HTTP 커넥터 제네릭 위에서 소개 하는 것 외에 다음과 같은 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="c3652-150">속성</span><span class="sxs-lookup"><span data-stu-id="c3652-150">Property</span></span> | <span data-ttu-id="c3652-151">설명</span><span class="sxs-lookup"><span data-stu-id="c3652-151">Description</span></span> | <span data-ttu-id="c3652-152">필수</span><span class="sxs-lookup"><span data-stu-id="c3652-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3652-153">username</span><span class="sxs-lookup"><span data-stu-id="c3652-153">username</span></span> | <span data-ttu-id="c3652-154">사용자 이름 tooaccess hello HTTP 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-154">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="c3652-155">예</span><span class="sxs-lookup"><span data-stu-id="c3652-155">Yes</span></span> |
| <span data-ttu-id="c3652-156">암호</span><span class="sxs-lookup"><span data-stu-id="c3652-156">password</span></span> | <span data-ttu-id="c3652-157">Hello 사용자 (사용자 이름)에 대 한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-157">Password for hello user (username).</span></span> | <span data-ttu-id="c3652-158">예</span><span class="sxs-lookup"><span data-stu-id="c3652-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="c3652-159">예: Basic, Digest 또는 Windows 인증</span><span class="sxs-lookup"><span data-stu-id="c3652-159">Example: using Basic, Digest, or Windows authentication</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="c3652-160">ClientCertificate 인증 사용</span><span class="sxs-lookup"><span data-stu-id="c3652-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="c3652-161">toouse 기본 인증 설정 `authenticationType` 으로 `ClientCertificate`, hello hello HTTP 커넥터 제네릭 위에서 소개 하는 것 외에 다음과 같은 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-161">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="c3652-162">속성</span><span class="sxs-lookup"><span data-stu-id="c3652-162">Property</span></span> | <span data-ttu-id="c3652-163">설명</span><span class="sxs-lookup"><span data-stu-id="c3652-163">Description</span></span> | <span data-ttu-id="c3652-164">필수</span><span class="sxs-lookup"><span data-stu-id="c3652-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3652-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="c3652-165">embeddedCertData</span></span> | <span data-ttu-id="c3652-166">hello 개인 정보 교환 (PFX) 파일의 이진 데이터의 Base64 인코딩 내용 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-166">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="c3652-167">어느 hello 지정 `embeddedCertData` 또는 `certThumbprint`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-167">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="c3652-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="c3652-168">certThumbprint</span></span> | <span data-ttu-id="c3652-169">게이트웨이 컴퓨터의 인증서 저장소에 설치 된 hello 인증서의 지문을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-169">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="c3652-170">온-프레미스 HTTP 소스에서 데이터를 복사하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="c3652-171">어느 hello 지정 `embeddedCertData` 또는 `certThumbprint`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-171">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="c3652-172">암호</span><span class="sxs-lookup"><span data-stu-id="c3652-172">password</span></span> | <span data-ttu-id="c3652-173">Hello 인증서와 연결 된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-173">Password associated with hello certificate.</span></span> | <span data-ttu-id="c3652-174">아니요</span><span class="sxs-lookup"><span data-stu-id="c3652-174">No</span></span> |

<span data-ttu-id="c3652-175">사용 하는 경우 `certThumbprint` toogrant hello 읽기 권한은 toohello 게이트웨이 서비스가 필요한 경우 인증 및 hello 인증서 hello hello 로컬 컴퓨터의 개인 저장소에 설치 하면:</span><span class="sxs-lookup"><span data-stu-id="c3652-175">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="c3652-176">MMC(Microsoft Management Console)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="c3652-177">Hello 추가 **인증서** 스냅인 해당 대상 hello **로컬 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-177">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="c3652-178">**인증서**, **개인**을 확장하고 **인증서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="c3652-179">Hello 개인 저장소에서 hello 인증서를 마우스 오른쪽 단추로 클릭 하 고 선택 **모든 작업**->**개인 키 관리...**</span><span class="sxs-lookup"><span data-stu-id="c3652-179">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="c3652-180">Hello에 **보안** 탭에서 데이터 관리 게이트웨이 호스트 서비스가 실행 되 고 있는 hello 읽기 액세스 toohello 인증서로 hello 사용자 계정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-180">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="c3652-181">예제: 클라이언트 인증서 사용</span><span class="sxs-lookup"><span data-stu-id="c3652-181">Example: using client certificate</span></span>
<span data-ttu-id="c3652-182">서비스 링크 데이터 팩터리 tooan 온-프레미스 HTTP 웹 서버를 연결 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-182">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="c3652-183">데이터 관리 게이트웨이가 설치 된 hello 컴퓨터에 설치 된 클라이언트 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-183">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="c3652-184">예제: 파일로 클라이언트 인증서 사용</span><span class="sxs-lookup"><span data-stu-id="c3652-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="c3652-185">서비스 링크 데이터 팩터리 tooan 온-프레미스 HTTP 웹 서버를 연결 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-185">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="c3652-186">데이터 관리 게이트웨이가 설치 된 hello 컴퓨터에 클라이언트 인증서 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-186">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="c3652-187">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="c3652-187">Dataset properties</span></span>
<span data-ttu-id="c3652-188">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="c3652-188">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c3652-189">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="c3652-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="c3652-190">hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-190">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="c3652-191">형식의 데이터 집합에 대 한 hello typeProperties 섹션 **Http** hello 다음과 같은 속성에</span><span class="sxs-lookup"><span data-stu-id="c3652-191">hello typeProperties section for dataset of type **Http** has hello following properties</span></span>

| <span data-ttu-id="c3652-192">속성</span><span class="sxs-lookup"><span data-stu-id="c3652-192">Property</span></span> | <span data-ttu-id="c3652-193">설명</span><span class="sxs-lookup"><span data-stu-id="c3652-193">Description</span></span> | <span data-ttu-id="c3652-194">필수</span><span class="sxs-lookup"><span data-stu-id="c3652-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c3652-195">type</span><span class="sxs-lookup"><span data-stu-id="c3652-195">type</span></span> | <span data-ttu-id="c3652-196">Hello 유형의 hello 데이터 집합을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-196">Specified hello type of hello dataset.</span></span> <span data-ttu-id="c3652-197">너무 설정 되어 있어야`Http`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-197">must be set too`Http`.</span></span> | <span data-ttu-id="c3652-198">예</span><span class="sxs-lookup"><span data-stu-id="c3652-198">Yes</span></span> |
| <span data-ttu-id="c3652-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="c3652-199">relativeUrl</span></span> | <span data-ttu-id="c3652-200">상대 URL toohello 리소스 hello 데이터가 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-200">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="c3652-201">경로 지정 하지 않으면 hello 연결 된 서비스 정의에 지정 된 유일한 hello URL 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-201">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="c3652-202">사용할 수 있습니다 tooconstruct 동적 URL [데이터 팩터리 함수 및 시스템 변수](data-factory-functions-variables.md), 예: "relativeUrl": "$$Text.Format ('/ my/보고서? 월 = {0:yyyy}-{0:MM} & fmt csv =', SliceStart)"입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-202">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="c3652-203">아니요</span><span class="sxs-lookup"><span data-stu-id="c3652-203">No</span></span> |
| <span data-ttu-id="c3652-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="c3652-204">requestMethod</span></span> | <span data-ttu-id="c3652-205">HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-205">Http method.</span></span> <span data-ttu-id="c3652-206">허용되는 값은 **GET** 또는 **POST**입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="c3652-207">아니요.</span><span class="sxs-lookup"><span data-stu-id="c3652-207">No.</span></span> <span data-ttu-id="c3652-208">기본값은 `GET`입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-208">Default is `GET`.</span></span> |
| <span data-ttu-id="c3652-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="c3652-209">additionalHeaders</span></span> | <span data-ttu-id="c3652-210">추가 HTTP 요청 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="c3652-211">아니요</span><span class="sxs-lookup"><span data-stu-id="c3652-211">No</span></span> |
| <span data-ttu-id="c3652-212">requestBody</span><span class="sxs-lookup"><span data-stu-id="c3652-212">requestBody</span></span> | <span data-ttu-id="c3652-213">HTTP 요청의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-213">Body for HTTP request.</span></span> | <span data-ttu-id="c3652-214">아니요</span><span class="sxs-lookup"><span data-stu-id="c3652-214">No</span></span> |
| <span data-ttu-id="c3652-215">format</span><span class="sxs-lookup"><span data-stu-id="c3652-215">format</span></span> | <span data-ttu-id="c3652-216">Toosimply 하려는 경우 **으로 HTTP 끝점에서 hello 데이터를 검색-은** 것, 구문 분석 하지 않고 형식 설정에이 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-216">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="c3652-217">복사 중 tooparse hello HTTP 응답을 콘텐츠에 삭제 하는 경우에 hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-217">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="c3652-218">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3652-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="c3652-219">아니요</span><span class="sxs-lookup"><span data-stu-id="c3652-219">No</span></span> |
| <span data-ttu-id="c3652-220">압축</span><span class="sxs-lookup"><span data-stu-id="c3652-220">compression</span></span> | <span data-ttu-id="c3652-221">Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-221">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="c3652-222">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="c3652-223">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="c3652-224">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3652-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="c3652-225">아니요</span><span class="sxs-lookup"><span data-stu-id="c3652-225">No</span></span> |

### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="c3652-226">예: hello GET (기본값) 메서드 사용</span><span class="sxs-lookup"><span data-stu-id="c3652-226">Example: using hello GET (default) method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-hello-post-method"></a><span data-ttu-id="c3652-227">예: hello POST 메서드를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c3652-227">Example: using hello POST method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="c3652-228">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="c3652-228">Copy activity properties</span></span>
<span data-ttu-id="c3652-229">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="c3652-229">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c3652-230">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="c3652-231">Hello에 사용할 수 있는 속성 **typeProperties** 섹션 hello에 hello 활동의 다른 손 활동 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-231">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="c3652-232">복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-232">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="c3652-233">현재 복사 작업에서 hello 소스 경우 형식의 **HttpSource**, 다음과 같은 속성 hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-233">Currently, when hello source in copy activity is of type **HttpSource**, hello following properties are supported.</span></span>

| <span data-ttu-id="c3652-234">속성</span><span class="sxs-lookup"><span data-stu-id="c3652-234">Property</span></span> | <span data-ttu-id="c3652-235">설명</span><span class="sxs-lookup"><span data-stu-id="c3652-235">Description</span></span> | <span data-ttu-id="c3652-236">필수</span><span class="sxs-lookup"><span data-stu-id="c3652-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="c3652-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="c3652-237">httpRequestTimeout</span></span> | <span data-ttu-id="c3652-238">안녕 hello HTTP 요청 tooget 응답 하기 위한 시간 제한 (TimeSpan).</span><span class="sxs-lookup"><span data-stu-id="c3652-238">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="c3652-239">Hello timeout tooget 응답으로 hello timeout tooread 응답 데이터가 아닌 경우</span><span class="sxs-lookup"><span data-stu-id="c3652-239">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="c3652-240">아니요.</span><span class="sxs-lookup"><span data-stu-id="c3652-240">No.</span></span> <span data-ttu-id="c3652-241">기본값: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="c3652-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="c3652-242">지원되는 파일 및 압축 형식</span><span class="sxs-lookup"><span data-stu-id="c3652-242">Supported file and compression formats</span></span>
<span data-ttu-id="c3652-243">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3652-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="c3652-244">JSON 예</span><span class="sxs-lookup"><span data-stu-id="c3652-244">JSON examples</span></span>
<span data-ttu-id="c3652-245">샘플 JSON 정의 제공 하는 다음 예제는 hello를 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-245">hello following example provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c3652-246">HTTP에서 toocopy 데이터 tooAzure Blob 저장소를 원본 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-246">They show how toocopy data from HTTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="c3652-247">그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 소스 tooany 중 어디에서 든 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-247">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a><span data-ttu-id="c3652-248">예: HTTP 소스 tooAzure Blob 저장소에서에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-248">Example: Copy data from HTTP source tooAzure Blob Storage</span></span>
<span data-ttu-id="c3652-249">이 샘플에 대 한 데이터 팩터리의 솔루션 hello를 Data Factory 엔터티에 따라 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-249">hello Data Factory solution for this sample contains hello following Data Factory entities:</span></span>

1. <span data-ttu-id="c3652-250">[HTTP](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="c3652-251">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="c3652-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c3652-252">[Http](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="c3652-253">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="c3652-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c3652-254">[HttpSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c3652-255">hello 샘플 데이터 복사 HTTP 소스 tooan Azure blob에서에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-255">hello sample copies data from an HTTP source tooan Azure blob every hour.</span></span> <span data-ttu-id="c3652-256">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-256">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="c3652-257">HTTP 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="c3652-257">HTTP linked service</span></span>
<span data-ttu-id="c3652-258">이 예제를 사용 하 여 hello HTTP 익명 인증을 사용 하는 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-258">This example uses hello HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="c3652-259">사용할 수 있는 다른 유형의 인증은 [HTTP 연결 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3652-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="c3652-260">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="c3652-260">Azure Storage linked service</span></span>

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

### <a name="http-input-dataset"></a><span data-ttu-id="c3652-261">HTTP 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="c3652-261">HTTP input dataset</span></span>
<span data-ttu-id="c3652-262">설정 **외부** 너무**true** 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-262">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="c3652-263">Azure Blob 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="c3652-263">Azure Blob output dataset</span></span>

<span data-ttu-id="c3652-264">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="c3652-264">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="c3652-265">복사 작업을 포함하는 파이프라인</span><span class="sxs-lookup"><span data-stu-id="c3652-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="c3652-266">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-266">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="c3652-267">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**HttpSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-267">In hello pipeline JSON definition, hello **source** type is set too**HttpSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="c3652-268">참조 [HttpSource](#copy-activity-properties) hello 목록이 hello HttpSource에서 지 원하는 속성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-268">See [HttpSource](#copy-activity-properties) for hello list of properties supported by hello HttpSource.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

> [!NOTE]
> <span data-ttu-id="c3652-269">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 toomap 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-269">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c3652-270">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="c3652-270">Performance and Tuning</span></span>
<span data-ttu-id="c3652-271">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3652-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
