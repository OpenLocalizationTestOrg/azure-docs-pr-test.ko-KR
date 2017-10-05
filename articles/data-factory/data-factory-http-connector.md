---
title: "HTTP 소스에서 데이터 이동 - Azure | Microsoft Docs"
description: "Azure Data Factory를 사용하여 온-프레미스 또는 클라우드 HTTP 소스에서 데이터를 이동하는 방법을 알아봅니다."
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
ms.openlocfilehash: 3cc1bd293868b0bb093f617ac12e16c26780fc89
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="fbc59-103">Azure Data Factory를 사용하여 HTTP 소스에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="fbc59-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="fbc59-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 온-프레미스/클라우드 HTTP 끝점의 데이터를 지원되는 싱크 데이터 저장소로 이동하는 방법에 대해 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from an on-premises/cloud HTTP endpoint to a supported sink data store.</span></span> <span data-ttu-id="fbc59-105">이 문서는 복사 작업 및 지원되는 데이터 저장소를 원본/싱크로 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 활동](data-factory-data-movement-activities.md) 문서를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="fbc59-106">현재 Data Factory는 HTTP 소스에서 다른 데이터 저장소로 데이터 이동이 아닌 다른 데이터 저장소에서 HTTP 대상으로 데이터 이동만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-106">Data factory currently supports only moving data from an HTTP source to other data stores, but not moving data from other data stores to an HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="fbc59-107">지원되는 시나리오 및 인증 형식</span><span class="sxs-lookup"><span data-stu-id="fbc59-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="fbc59-108">이 HTTP 커넥터에서 HTTP **GET** 또는 **POST** 메서드를 사용하여 **클라우드 및 온-프레미스 HTTP/s 끝점**에서 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-108">You can use this HTTP connector to retrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="fbc59-109">다음 인증 형식이 지원됩니다. **Anonymous**, **Basic**, **Digest**, **Windows** 및 **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="fbc59-109">The following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="fbc59-110">이 커넥터와 [웹 테이블 커넥터](data-factory-web-table-connector.md) 간이 차이는 후자는 웹 HTML 페이지에서 테이블 콘텐츠를 추출하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-110">Note the difference between this connector and the [Web table connector](data-factory-web-table-connector.md) is: the latter is used to extract table content from web HTML page.</span></span>

<span data-ttu-id="fbc59-111">온-프레미스 HTTP 끝점에서 데이터를 복사할 때 온-프레미스 환경/Azure VM에서 데이터 관리 게이트웨이를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in the on-premises environment/Azure VM.</span></span> <span data-ttu-id="fbc59-112">데이터 관리 게이트웨이 및 게이트웨이 설정에 대한 단계별 지침을 알아보려면 [온-프레미스 위치 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fbc59-113">시작</span><span class="sxs-lookup"><span data-stu-id="fbc59-113">Getting started</span></span>
<span data-ttu-id="fbc59-114">다른 도구/API를 사용하여 HTTP 원본의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="fbc59-115">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-115">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="fbc59-116">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

- <span data-ttu-id="fbc59-117">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-117">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="fbc59-118">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> <span data-ttu-id="fbc59-119">HTTP 소스에서 Azure Blob Storage로 데이터를 복사하는 JSON 샘플은 이 문서의 [JSON 예제](#json-examples) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-119">For JSON samples to copy data from HTTP source to Azure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="fbc59-120">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="fbc59-120">Linked service properties</span></span>
<span data-ttu-id="fbc59-121">다음 표는 HTTP 연결 서비스에 특정한 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-121">The following table provides description for JSON elements specific to HTTP linked service.</span></span>

| <span data-ttu-id="fbc59-122">속성</span><span class="sxs-lookup"><span data-stu-id="fbc59-122">Property</span></span> | <span data-ttu-id="fbc59-123">설명</span><span class="sxs-lookup"><span data-stu-id="fbc59-123">Description</span></span> | <span data-ttu-id="fbc59-124">필수</span><span class="sxs-lookup"><span data-stu-id="fbc59-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fbc59-125">type</span><span class="sxs-lookup"><span data-stu-id="fbc59-125">type</span></span> | <span data-ttu-id="fbc59-126">type 속성을 `Http`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-126">The type property must be set to: `Http`.</span></span> | <span data-ttu-id="fbc59-127">예</span><span class="sxs-lookup"><span data-stu-id="fbc59-127">Yes</span></span> |
| <span data-ttu-id="fbc59-128">url</span><span class="sxs-lookup"><span data-stu-id="fbc59-128">url</span></span> | <span data-ttu-id="fbc59-129">웹 서버에 대한 기본 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-129">Base URL to the Web Server</span></span> | <span data-ttu-id="fbc59-130">예</span><span class="sxs-lookup"><span data-stu-id="fbc59-130">Yes</span></span> |
| <span data-ttu-id="fbc59-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="fbc59-131">authenticationType</span></span> | <span data-ttu-id="fbc59-132">인증 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-132">Specifies the authentication type.</span></span> <span data-ttu-id="fbc59-133">허용되는 값: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="fbc59-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="fbc59-134">각 인증 형식에 대한 더 많은 속성 및 JSON 샘플은 표 아래 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-134">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="fbc59-135">예</span><span class="sxs-lookup"><span data-stu-id="fbc59-135">Yes</span></span> |
| <span data-ttu-id="fbc59-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="fbc59-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="fbc59-137">소스가 HTTPS 웹 서버인 경우 서버 SSL 인증서 유효성 검사를 사용할지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-137">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="fbc59-138">아니요. 기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-138">No, default is true</span></span> |
| <span data-ttu-id="fbc59-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="fbc59-139">gatewayName</span></span> | <span data-ttu-id="fbc59-140">온-프레미스 HTTP 소스에 연결하기 위한 데이터 관리 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-140">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="fbc59-141">온-프레미스 HTTP 소스에서 데이터를 복사하는 경우에는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="fbc59-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="fbc59-142">encryptedCredential</span></span> | <span data-ttu-id="fbc59-143">HTTP 끝점 액세스를 위한 암호화된 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-143">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="fbc59-144">복사 마법사 또는 ClickOnce 팝업 대화 상자에서 인증 정보를 구성할 때 자동 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-144">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="fbc59-145">아니요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-145">No.</span></span> <span data-ttu-id="fbc59-146">온-프레미스 HTTP 서버에서 데이터를 복사하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="fbc59-147">온-프레미스 HTTP 커넥터 데이터 원본의 자격 증명을 설정하는 방법에 대한 자세한 내용은 [데이터 관리 게이트웨이를 사용하여 온-프레미스 원본과 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-147">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="fbc59-148">Basic, Digest 또는 Windows 인증 사용</span><span class="sxs-lookup"><span data-stu-id="fbc59-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="fbc59-149">`authenticationType`을 `Basic`, `Digest` 또는 `Windows`로 설정하고, 위에서 소개한 HTTP 커넥터 일반 속성 외에 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="fbc59-150">속성</span><span class="sxs-lookup"><span data-stu-id="fbc59-150">Property</span></span> | <span data-ttu-id="fbc59-151">설명</span><span class="sxs-lookup"><span data-stu-id="fbc59-151">Description</span></span> | <span data-ttu-id="fbc59-152">필수</span><span class="sxs-lookup"><span data-stu-id="fbc59-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fbc59-153">username</span><span class="sxs-lookup"><span data-stu-id="fbc59-153">username</span></span> | <span data-ttu-id="fbc59-154">HTTP 끝점 액세스를 위한 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-154">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="fbc59-155">예</span><span class="sxs-lookup"><span data-stu-id="fbc59-155">Yes</span></span> |
| <span data-ttu-id="fbc59-156">password</span><span class="sxs-lookup"><span data-stu-id="fbc59-156">password</span></span> | <span data-ttu-id="fbc59-157">사용자(사용자 이름) 암호.</span><span class="sxs-lookup"><span data-stu-id="fbc59-157">Password for the user (username).</span></span> | <span data-ttu-id="fbc59-158">예</span><span class="sxs-lookup"><span data-stu-id="fbc59-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="fbc59-159">예: Basic, Digest 또는 Windows 인증</span><span class="sxs-lookup"><span data-stu-id="fbc59-159">Example: using Basic, Digest, or Windows authentication</span></span>

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

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="fbc59-160">ClientCertificate 인증 사용</span><span class="sxs-lookup"><span data-stu-id="fbc59-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="fbc59-161">기본 인증을 사용하려면 `authenticationType`을 `ClientCertificate`로 설정하고, 위에서 소개한 HTTP 커넥터 일반 속성 외에 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-161">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="fbc59-162">속성</span><span class="sxs-lookup"><span data-stu-id="fbc59-162">Property</span></span> | <span data-ttu-id="fbc59-163">설명</span><span class="sxs-lookup"><span data-stu-id="fbc59-163">Description</span></span> | <span data-ttu-id="fbc59-164">필수</span><span class="sxs-lookup"><span data-stu-id="fbc59-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fbc59-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="fbc59-165">embeddedCertData</span></span> | <span data-ttu-id="fbc59-166">PFX(개인 정보 교환) 파일의 이진 데이터에 대해 Base64로 인코딩된 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="fbc59-166">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="fbc59-167">`embeddedCertData` 또는 `certThumbprint`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-167">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="fbc59-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="fbc59-168">certThumbprint</span></span> | <span data-ttu-id="fbc59-169">게이트웨이 컴퓨터의 인증서 저장소에 설치된 인증서의 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-169">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="fbc59-170">온-프레미스 HTTP 소스에서 데이터를 복사하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="fbc59-171">`embeddedCertData` 또는 `certThumbprint`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-171">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="fbc59-172">password</span><span class="sxs-lookup"><span data-stu-id="fbc59-172">password</span></span> | <span data-ttu-id="fbc59-173">인증서와 연결된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-173">Password associated with the certificate.</span></span> | <span data-ttu-id="fbc59-174">아니요</span><span class="sxs-lookup"><span data-stu-id="fbc59-174">No</span></span> |

<span data-ttu-id="fbc59-175">인증에 `certThumbprint`를 사용하고 인증서가 로컬 컴퓨터의 개인 저장소에 설치된 경우 게이트웨이 서비스에 읽기 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-175">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="fbc59-176">MMC(Microsoft Management Console)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="fbc59-177">**로컬 컴퓨터**를 대상으로 하는 **인증서** 스냅인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-177">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="fbc59-178">**인증서**, **개인**을 확장하고 **인증서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="fbc59-179">개인 저장소에서 인증서를 마우스 오른쪽 단추로 클릭하고 **모든 작업**->**개인 키 관리...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-179">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="fbc59-180">**보안** 탭에서 인증서에 대한 읽기 권한으로 데이터 관리 게이트웨이 호스트 서비스를 실행 중인 사용자 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-180">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="fbc59-181">예제: 클라이언트 인증서 사용</span><span class="sxs-lookup"><span data-stu-id="fbc59-181">Example: using client certificate</span></span>
<span data-ttu-id="fbc59-182">이 연결된 서비스는 데이터 팩터리를 온-프레미스 HTTP 웹 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-182">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="fbc59-183">데이터 관리 게이트웨이가 설치된 컴퓨터에 설치된 클라이언트 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-183">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="fbc59-184">예제: 파일로 클라이언트 인증서 사용</span><span class="sxs-lookup"><span data-stu-id="fbc59-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="fbc59-185">이 연결된 서비스는 데이터 팩터리를 온-프레미스 HTTP 웹 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-185">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="fbc59-186">데이터 관리 게이트웨이가 설치된 컴퓨터에서 클라이언트 인증서 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-186">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="fbc59-187">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="fbc59-187">Dataset properties</span></span>
<span data-ttu-id="fbc59-188">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-188">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="fbc59-189">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).</span><span class="sxs-lookup"><span data-stu-id="fbc59-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="fbc59-190">**typeProperties** 섹션은 데이터 집합의 각 형식에 따라 다르며 데이터 저장소에 있는 데이터의 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-190">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="fbc59-191">**Http** 형식의 데이터 집합에 대한 typeProperties 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-191">The typeProperties section for dataset of type **Http** has the following properties</span></span>

| <span data-ttu-id="fbc59-192">속성</span><span class="sxs-lookup"><span data-stu-id="fbc59-192">Property</span></span> | <span data-ttu-id="fbc59-193">설명</span><span class="sxs-lookup"><span data-stu-id="fbc59-193">Description</span></span> | <span data-ttu-id="fbc59-194">필수</span><span class="sxs-lookup"><span data-stu-id="fbc59-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="fbc59-195">type</span><span class="sxs-lookup"><span data-stu-id="fbc59-195">type</span></span> | <span data-ttu-id="fbc59-196">데이터 집합의 형식을 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-196">Specified the type of the dataset.</span></span> <span data-ttu-id="fbc59-197">`Http`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-197">must be set to `Http`.</span></span> | <span data-ttu-id="fbc59-198">예</span><span class="sxs-lookup"><span data-stu-id="fbc59-198">Yes</span></span> |
| <span data-ttu-id="fbc59-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="fbc59-199">relativeUrl</span></span> | <span data-ttu-id="fbc59-200">데이터를 포함하는 리소스에 대한 상대 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-200">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="fbc59-201">경로를 지정하지 않으면 연결된 서비스 정의에 지정된 URL만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-201">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="fbc59-202">동적 URL을 생성하려면 [데이터 팩터리 함수 및 시스템 변수](data-factory-functions-variables.md)를 사용할 수 있습니다(예: "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)").</span><span class="sxs-lookup"><span data-stu-id="fbc59-202">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="fbc59-203">아니요</span><span class="sxs-lookup"><span data-stu-id="fbc59-203">No</span></span> |
| <span data-ttu-id="fbc59-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="fbc59-204">requestMethod</span></span> | <span data-ttu-id="fbc59-205">HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-205">Http method.</span></span> <span data-ttu-id="fbc59-206">허용되는 값은 **GET** 또는 **POST**입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="fbc59-207">아니요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-207">No.</span></span> <span data-ttu-id="fbc59-208">기본값은 `GET`입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-208">Default is `GET`.</span></span> |
| <span data-ttu-id="fbc59-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="fbc59-209">additionalHeaders</span></span> | <span data-ttu-id="fbc59-210">추가 HTTP 요청 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="fbc59-211">아니요</span><span class="sxs-lookup"><span data-stu-id="fbc59-211">No</span></span> |
| <span data-ttu-id="fbc59-212">requestBody</span><span class="sxs-lookup"><span data-stu-id="fbc59-212">requestBody</span></span> | <span data-ttu-id="fbc59-213">HTTP 요청의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-213">Body for HTTP request.</span></span> | <span data-ttu-id="fbc59-214">아니요</span><span class="sxs-lookup"><span data-stu-id="fbc59-214">No</span></span> |
| <span data-ttu-id="fbc59-215">format</span><span class="sxs-lookup"><span data-stu-id="fbc59-215">format</span></span> | <span data-ttu-id="fbc59-216">데이터를 구문 분석하지 않고 **HTTP 끝점에서 데이터를 그대로 검색**하려면 이 서식 설정을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-216">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="fbc59-217">복사 중에 HTTP 응답 내용을 구문 분석하려면 **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**과 같은 서식 유형이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-217">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="fbc59-218">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="fbc59-219">아니요</span><span class="sxs-lookup"><span data-stu-id="fbc59-219">No</span></span> |
| <span data-ttu-id="fbc59-220">압축</span><span class="sxs-lookup"><span data-stu-id="fbc59-220">compression</span></span> | <span data-ttu-id="fbc59-221">데이터에 대한 압축 유형 및 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-221">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="fbc59-222">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="fbc59-223">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="fbc59-224">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="fbc59-225">아니요</span><span class="sxs-lookup"><span data-stu-id="fbc59-225">No</span></span> |

### <a name="example-using-the-get-default-method"></a><span data-ttu-id="fbc59-226">예제: GET(기본) 메서드 사용</span><span class="sxs-lookup"><span data-stu-id="fbc59-226">Example: using the GET (default) method</span></span>

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

### <a name="example-using-the-post-method"></a><span data-ttu-id="fbc59-227">예제: POST 메서드 사용</span><span class="sxs-lookup"><span data-stu-id="fbc59-227">Example: using the POST method</span></span>

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

## <a name="copy-activity-properties"></a><span data-ttu-id="fbc59-228">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="fbc59-228">Copy activity properties</span></span>
<span data-ttu-id="fbc59-229">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-229">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fbc59-230">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="fbc59-231">반면 활동의 **typeProperties** 섹션에서 사용할 수 있는 속성은 각 활동 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-231">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="fbc59-232">복사 활동의 경우 이러한 속성은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-232">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="fbc59-233">현재 복사 작업의 원본이 **HttpSource** 형식인 경우 다음 속성이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-233">Currently, when the source in copy activity is of type **HttpSource**, the following properties are supported.</span></span>

| <span data-ttu-id="fbc59-234">속성</span><span class="sxs-lookup"><span data-stu-id="fbc59-234">Property</span></span> | <span data-ttu-id="fbc59-235">설명</span><span class="sxs-lookup"><span data-stu-id="fbc59-235">Description</span></span> | <span data-ttu-id="fbc59-236">필수</span><span class="sxs-lookup"><span data-stu-id="fbc59-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="fbc59-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="fbc59-237">httpRequestTimeout</span></span> | <span data-ttu-id="fbc59-238">HTTP 요청이 응답을 받을 시간 제한(TimeSpan)입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-238">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="fbc59-239">응답 데이터를 읽는 시간 제한이 아니라, 응답을 받을 시간 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-239">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="fbc59-240">아니요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-240">No.</span></span> <span data-ttu-id="fbc59-241">기본값: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="fbc59-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="fbc59-242">지원되는 파일 및 압축 형식</span><span class="sxs-lookup"><span data-stu-id="fbc59-242">Supported file and compression formats</span></span>
<span data-ttu-id="fbc59-243">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="fbc59-244">JSON 예</span><span class="sxs-lookup"><span data-stu-id="fbc59-244">JSON examples</span></span>
<span data-ttu-id="fbc59-245">다음 예제에서는 [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-245">The following example provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="fbc59-246">HTTP 원본에서 Azure Blob Storage로 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-246">They show how to copy data from HTTP source to Azure Blob Storage.</span></span> <span data-ttu-id="fbc59-247">그러나 Azure 데이터 팩터리의 복사 작업을 사용하여 임의의 원본에서 **여기**에 설명한 싱크로 [직접](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-247">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-to-azure-blob-storage"></a><span data-ttu-id="fbc59-248">예제: HTTP 원본에서 Azure Blob Storage로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="fbc59-248">Example: Copy data from HTTP source to Azure Blob Storage</span></span>
<span data-ttu-id="fbc59-249">이 샘플에 대한 Data Factory 솔루션은 다음 Data Factory 엔터티를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-249">The Data Factory solution for this sample contains the following Data Factory entities:</span></span>

1. <span data-ttu-id="fbc59-250">[HTTP](#linked-service-properties) 형식의 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="fbc59-251">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="fbc59-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fbc59-252">[Http](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="fbc59-253">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="fbc59-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="fbc59-254">[HttpSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="fbc59-255">샘플은 1시간마다 HTTP 소스의 데이터를 Azure Blob으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-255">The sample copies data from an HTTP source to an Azure blob every hour.</span></span> <span data-ttu-id="fbc59-256">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-256">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="fbc59-257">HTTP 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="fbc59-257">HTTP linked service</span></span>
<span data-ttu-id="fbc59-258">이 예제에서는 익명 인증으로 HTTP 연결된 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-258">This example uses the HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="fbc59-259">사용할 수 있는 다른 유형의 인증은 [HTTP 연결 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="fbc59-260">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="fbc59-260">Azure Storage linked service</span></span>

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

### <a name="http-input-dataset"></a><span data-ttu-id="fbc59-261">HTTP 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="fbc59-261">HTTP input dataset</span></span>
<span data-ttu-id="fbc59-262">**external**을 **true**로 설정하면 데이터 집합이 Data Factory의 외부에 있고 Data Factory의 활동으로 생성되지 않는다고 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-262">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="fbc59-263">Azure Blob 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="fbc59-263">Azure Blob output dataset</span></span>

<span data-ttu-id="fbc59-264">데이터는 매시간 새 blob에 기록됩니다.(빈도: 1시간, 간격:1회)</span><span class="sxs-lookup"><span data-stu-id="fbc59-264">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

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

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="fbc59-265">복사 작업을 포함하는 파이프라인</span><span class="sxs-lookup"><span data-stu-id="fbc59-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="fbc59-266">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-266">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="fbc59-267">파이프라인 JSON 정의에서 **source** 형식은 **HttpSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbc59-267">In the pipeline JSON definition, the **source** type is set to **HttpSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="fbc59-268">HttpSource에서 지원하는 속성 목록은 [HttpSource](#copy-activity-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-268">See [HttpSource](#copy-activity-properties) for the list of properties supported by the HttpSource.</span></span>

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
        "description": "Copy from an HTTP source to an Azure blob",
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
> <span data-ttu-id="fbc59-269">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하려면 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-269">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="fbc59-270">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="fbc59-270">Performance and Tuning</span></span>
<span data-ttu-id="fbc59-271">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc59-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
