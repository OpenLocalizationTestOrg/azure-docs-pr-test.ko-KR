---
title: "Azure 데이터 팩터리를 사용 하 여 FTP 서버에서 데이터 aaaMove | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 Azure 데이터 팩터리를 사용 하 여 FTP 서버에서 toomove 데이터입니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="ad299-103">Azure Data Factory를 사용하여 FTP 서버에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="ad299-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="ad299-104">이 문서에서는 어떻게 toouse hello 복사 작업이 Azure Data Factory toomove 데이터에는 FTP 서버에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from an FTP server.</span></span> <span data-ttu-id="ad299-105">Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="ad299-106">FTP 서버 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-106">You can copy data from an FTP server tooany supported sink data store.</span></span> <span data-ttu-id="ad299-107">데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-107">For a list of data stores supported as sinks by hello copy activity, see hello [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="ad299-108">Data Factory에는 현재 FTP 서버 tooother 데이터에서 데이터 이동을 저장 하지만 tooan FTP 서버를 다른 데이터에서 데이터를 이동 하지 저장만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-108">Data Factory currently supports only moving data from an FTP server tooother data stores, but not moving data from other data stores tooan FTP server.</span></span> <span data-ttu-id="ad299-109">온-프레미스 및 클라우드 FTP 서버를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="ad299-110">hello 복사 작업으로 복사한 toohello 대상 않아 hello 소스 파일을 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-110">hello copy activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="ad299-111">성공적인 복사 후 toodelete hello 소스 파일을 필요한 경우 사용자 지정 활동 toodelete hello 파일을 만들고 hello 파이프라인에서 hello 활동을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-111">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file, and use hello activity in hello pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="ad299-112">연결 설정</span><span class="sxs-lookup"><span data-stu-id="ad299-112">Enable connectivity</span></span>
<span data-ttu-id="ad299-113">데이터를 이동 하는 경우는 **온-프레미스** FTP 서버 tooa 클라우드 데이터 저장소 (예를 들어 tooAzure Blob 저장소)를 설치 하 고 데이터 관리 게이트웨이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-113">If you are moving data from an **on-premises** FTP server tooa cloud data store (for example, tooAzure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="ad299-114">hello 데이터 관리 게이트웨이 온-프레미스 컴퓨터에 설치 된 클라이언트 에이전트로, 및 클라우드 서비스 tooconnect tooan 온-프레미스 리소스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-114">hello Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services tooconnect tooan on-premises resource.</span></span> <span data-ttu-id="ad299-115">자세한 내용은 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad299-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="ad299-116">Hello 게이트웨이를 설정 하 고 사용에 대 한 단계별 지침에 대 한 참조 [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-116">For step-by-step instructions on setting up hello gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="ad299-117">경우에 hello 서버는 Azure 인프라 서비스 (IaaS) 가상 컴퓨터 (VM)으로 hello 게이트웨이 tooconnect tooan FTP 서버를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-117">You use hello gateway tooconnect tooan FTP server, even if hello server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="ad299-118">가능한 tooinstall hello 수단 hello에 동일한 온-프레미스 컴퓨터 또는 IaaS VM FTP 서버 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-118">It is possible tooinstall hello gateway on hello same on-premises machine or IaaS VM as hello FTP server.</span></span> <span data-ttu-id="ad299-119">그러나 별도 컴퓨터 또는 IaaS VM tooavoid 리소스 경합 및 성능 향상을 위해 hello 게이트웨이 설치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-119">However, we recommend that you install hello gateway on a separate machine or IaaS VM tooavoid resource contention, and for better performance.</span></span> <span data-ttu-id="ad299-120">별도 컴퓨터에 hello 게이트웨이 설치할 때 hello 컴퓨터 수 tooaccess hello FTP 서버가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-120">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="ad299-121">시작</span><span class="sxs-lookup"><span data-stu-id="ad299-121">Get started</span></span>
<span data-ttu-id="ad299-122">다른 도구 또는 API를 사용하여 FTP 원본의 데이터를 이동하는 복사 작업이 포함된 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="ad299-123">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **데이터 팩터리 복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-123">hello easiest way toocreate a pipeline is toouse hello **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="ad299-124">빠른 연습을 위해서는 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad299-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="ad299-125">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **PowerShell**, **Azure리소스관리자템플릿**, **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ad299-126">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="ad299-127">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-127">Whether you use hello tools or APIs, perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="ad299-128">만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="ad299-129">만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="ad299-130">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="ad299-131">Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="ad299-132">도구 또는 Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="ad299-133">Data Factory 된 엔터티를 FTP 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 hello [JSON의 예: FTP 서버 tooAzure blob에서 데이터를 복사](#json-example-copy-data-from-ftp-server-to-azure-blob) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="ad299-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an FTP data store, see hello [JSON example: Copy data from FTP server tooAzure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="ad299-134">지원 되는 파일 및 압축 형식 toouse에 대 한 세부 정보를 참조 하십시오. [Azure Data Factory에서 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-134">For details about supported file and compression formats toouse, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="ad299-135">다음 섹션 hello 사용 되는 toodefine Data Factory 엔터티에 특정 tooFTP는 JSON 속성에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooFTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="ad299-136">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="ad299-136">Linked service properties</span></span>
<span data-ttu-id="ad299-137">다음 표에서 hello JSON 요소 특정 tooan 연결 하는 FTP 서비스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-137">hello following table describes JSON elements specific tooan FTP linked service.</span></span>

| <span data-ttu-id="ad299-138">속성</span><span class="sxs-lookup"><span data-stu-id="ad299-138">Property</span></span> | <span data-ttu-id="ad299-139">설명</span><span class="sxs-lookup"><span data-stu-id="ad299-139">Description</span></span> | <span data-ttu-id="ad299-140">필수</span><span class="sxs-lookup"><span data-stu-id="ad299-140">Required</span></span> | <span data-ttu-id="ad299-141">기본값</span><span class="sxs-lookup"><span data-stu-id="ad299-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ad299-142">type</span><span class="sxs-lookup"><span data-stu-id="ad299-142">type</span></span> |<span data-ttu-id="ad299-143">이 tooFtpServer를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-143">Set this tooFtpServer.</span></span> |<span data-ttu-id="ad299-144">예</span><span class="sxs-lookup"><span data-stu-id="ad299-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="ad299-145">host</span><span class="sxs-lookup"><span data-stu-id="ad299-145">host</span></span> |<span data-ttu-id="ad299-146">Hello 이름 또는 hello FTP 서버의 IP 주소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-146">Specify hello name or IP address of hello FTP server.</span></span> |<span data-ttu-id="ad299-147">예</span><span class="sxs-lookup"><span data-stu-id="ad299-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="ad299-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ad299-148">authenticationType</span></span> |<span data-ttu-id="ad299-149">Hello 인증 유형을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-149">Specify hello authentication type.</span></span> |<span data-ttu-id="ad299-150">예</span><span class="sxs-lookup"><span data-stu-id="ad299-150">Yes</span></span> |<span data-ttu-id="ad299-151">기본, 익명</span><span class="sxs-lookup"><span data-stu-id="ad299-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="ad299-152">username</span><span class="sxs-lookup"><span data-stu-id="ad299-152">username</span></span> |<span data-ttu-id="ad299-153">Hello 있는 사용자에 게 액세스 toohello FTP 서버를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-153">Specify hello user who has access toohello FTP server.</span></span> |<span data-ttu-id="ad299-154">아니요</span><span class="sxs-lookup"><span data-stu-id="ad299-154">No</span></span> |&nbsp; |
| <span data-ttu-id="ad299-155">암호</span><span class="sxs-lookup"><span data-stu-id="ad299-155">password</span></span> |<span data-ttu-id="ad299-156">Hello 사용자 (사용자 이름)에 대 한 hello 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-156">Specify hello password for hello user (username).</span></span> |<span data-ttu-id="ad299-157">아니요</span><span class="sxs-lookup"><span data-stu-id="ad299-157">No</span></span> |&nbsp; |
| <span data-ttu-id="ad299-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="ad299-158">encryptedCredential</span></span> |<span data-ttu-id="ad299-159">Hello 암호화 된 자격 증명 tooaccess hello FTP 서버를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-159">Specify hello encrypted credential tooaccess hello FTP server.</span></span> |<span data-ttu-id="ad299-160">아니요</span><span class="sxs-lookup"><span data-stu-id="ad299-160">No</span></span> |&nbsp; |
| <span data-ttu-id="ad299-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ad299-161">gatewayName</span></span> |<span data-ttu-id="ad299-162">데이터 관리 게이트웨이 tooconnect tooan 온-프레미스 FTP 서버에 hello 게이트웨이의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-162">Specify hello name of hello gateway in Data Management Gateway tooconnect tooan on-premises FTP server.</span></span> |<span data-ttu-id="ad299-163">아니요</span><span class="sxs-lookup"><span data-stu-id="ad299-163">No</span></span> |&nbsp; |
| <span data-ttu-id="ad299-164">포트</span><span class="sxs-lookup"><span data-stu-id="ad299-164">port</span></span> |<span data-ttu-id="ad299-165">Hello 수신 포트를 어떤 hello FTP 서버를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-165">Specify hello port on which hello FTP server is listening.</span></span> |<span data-ttu-id="ad299-166">아니요</span><span class="sxs-lookup"><span data-stu-id="ad299-166">No</span></span> |<span data-ttu-id="ad299-167">21</span><span class="sxs-lookup"><span data-stu-id="ad299-167">21</span></span> |
| <span data-ttu-id="ad299-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="ad299-168">enableSsl</span></span> |<span data-ttu-id="ad299-169">Toouse SSL/TLS 채널을 통해 FTP 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-169">Specify whether toouse FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="ad299-170">아니요</span><span class="sxs-lookup"><span data-stu-id="ad299-170">No</span></span> |<span data-ttu-id="ad299-171">true</span><span class="sxs-lookup"><span data-stu-id="ad299-171">true</span></span> |
| <span data-ttu-id="ad299-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="ad299-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="ad299-173">SSL/TLS 채널을 통해 FTP를 사용 하는 경우 tooenable 서버 SSL 인증서 유효성 검사 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-173">Specify whether tooenable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="ad299-174">아니요</span><span class="sxs-lookup"><span data-stu-id="ad299-174">No</span></span> |<span data-ttu-id="ad299-175">true</span><span class="sxs-lookup"><span data-stu-id="ad299-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="ad299-176">익명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="ad299-176">Use Anonymous authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="ad299-177">일반 텍스트에 사용자 이름 및 암호를 기본 인증에 사용</span><span class="sxs-lookup"><span data-stu-id="ad299-177">Use username and password in plain text for basic authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="ad299-178">포트, enableSsl, enableServerCertificateValidation 사용</span><span class="sxs-lookup"><span data-stu-id="ad299-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="ad299-179">인증 및 게이트웨이에 encryptedCredential 사용</span><span class="sxs-lookup"><span data-stu-id="ad299-179">Use encryptedCredential for authentication and gateway</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="ad299-180">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="ad299-180">Dataset properties</span></span>
<span data-ttu-id="ad299-181">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad299-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="ad299-182">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="ad299-183">hello **typeProperties** 섹션은 데이터 집합의 각 형식 마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-183">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="ad299-184">가 특정 toohello 데이터 집합 형식 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-184">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="ad299-185">hello **typeProperties** 형식의 데이터 집합에 대 한 섹션 **FileShare** hello 다음과 같은 속성에:</span><span class="sxs-lookup"><span data-stu-id="ad299-185">hello **typeProperties** section for a dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="ad299-186">속성</span><span class="sxs-lookup"><span data-stu-id="ad299-186">Property</span></span> | <span data-ttu-id="ad299-187">설명</span><span class="sxs-lookup"><span data-stu-id="ad299-187">Description</span></span> | <span data-ttu-id="ad299-188">필수</span><span class="sxs-lookup"><span data-stu-id="ad299-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad299-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="ad299-189">folderPath</span></span> |<span data-ttu-id="ad299-190">하위 경로 toohello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-190">Subpath toohello folder.</span></span> <span data-ttu-id="ad299-191">이스케이프 문자를 사용 하 여 ' \ ' hello 문자열의 특수 문자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-191">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="ad299-192">예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad299-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="ad299-193">이 속성을 결합할 수 **partitionBy** toohave 폴더 경로 분할 영역에 따라 시작 및 종료 날짜 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-193">You can combine this property with **partitionBy** toohave folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="ad299-194">예</span><span class="sxs-lookup"><span data-stu-id="ad299-194">Yes</span></span> |
| <span data-ttu-id="ad299-195">fileName</span><span class="sxs-lookup"><span data-stu-id="ad299-195">fileName</span></span> |<span data-ttu-id="ad299-196">Hello에 hello hello 파일 이름을 지정 **folderPath** hello 테이블 toorefer tooa 특정 파일 hello 폴더에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-196">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="ad299-197">이 속성에 대 한 모든 값을 지정 하지 않는 경우 hello 테이블 hello 폴더의 tooall 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-197">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="ad299-198">때 **fileName** hello hello 생성 된 파일의 이름이 형식에 따라 hello에 출력 데이터 집합의 경우 지정 하지 않으면:</span><span class="sxs-lookup"><span data-stu-id="ad299-198">When **fileName** is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="ad299-199">Data.<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="ad299-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="ad299-200">아니요</span><span class="sxs-lookup"><span data-stu-id="ad299-200">No</span></span> |
| <span data-ttu-id="ad299-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="ad299-201">fileFilter</span></span> |<span data-ttu-id="ad299-202">Hello에 필터 사용 toobe tooselect 파일의 하위 집합을 지정 **folderPath**, 모든 파일이 아닌 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-202">Specify a filter toobe used tooselect a subset of files in hello **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="ad299-203">허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="ad299-204">예 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="ad299-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="ad299-205">예 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="ad299-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="ad299-206">**fileFilter**는 FileShare 입력 데이터 집합에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="ad299-207">이 속성은 HDFS(Hadoop Distributed File System)에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="ad299-208">아니요</span><span class="sxs-lookup"><span data-stu-id="ad299-208">No</span></span> |
| <span data-ttu-id="ad299-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="ad299-209">partitionedBy</span></span> |<span data-ttu-id="ad299-210">사용 하는 동적 toospecify **folderPath** 및 **fileName** 시계열 데이터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-210">Used toospecify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="ad299-211">예를 들어 매 시간 데이터에 대해 매개 변수가 있는 **folderPath**를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="ad299-212">아니요</span><span class="sxs-lookup"><span data-stu-id="ad299-212">No</span></span> |
| <span data-ttu-id="ad299-213">format</span><span class="sxs-lookup"><span data-stu-id="ad299-213">format</span></span> | <span data-ttu-id="ad299-214">hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-214">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="ad299-215">집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-215">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="ad299-216">자세한 내용은 참조 hello [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format), 및 [Parquet 형식 ](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션.</span><span class="sxs-lookup"><span data-stu-id="ad299-216">For more information, see hello [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="ad299-217">파일 기반 저장소 (이진 복사) 사이 있는 대로 toocopy 파일을 만들려는 경우 두 입력 및 출력 데이터 집합 정의에 hello 형식 섹션을 건너뛰십시오.</span><span class="sxs-lookup"><span data-stu-id="ad299-217">If you want toocopy files as they are between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="ad299-218">아니요</span><span class="sxs-lookup"><span data-stu-id="ad299-218">No</span></span> |
| <span data-ttu-id="ad299-219">압축</span><span class="sxs-lookup"><span data-stu-id="ad299-219">compression</span></span> | <span data-ttu-id="ad299-220">Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-220">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="ad299-221">지원되는 형식은 **GZip**, **Deflate**, **BZip2**, **ZipDeflate**이고 지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="ad299-222">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad299-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="ad299-223">아니요</span><span class="sxs-lookup"><span data-stu-id="ad299-223">No</span></span> |
| <span data-ttu-id="ad299-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="ad299-224">useBinaryTransfer</span></span> |<span data-ttu-id="ad299-225">전송 모드를 toouse hello 이진 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-225">Specify whether toouse hello binary transfer mode.</span></span> <span data-ttu-id="ad299-226">hello 값은 이진 모드 (이것이 hello 기본값)에 대 한 true이 고 ASCII false입니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-226">hello values are true for binary mode (this is hello default value), and false for ASCII.</span></span> <span data-ttu-id="ad299-227">이 속성 hello 관련된 연결 된 서비스 유형의 유형인 경우에 사용할 수 있습니다: ftp 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-227">This property can only be used when hello associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="ad299-228">아니요</span><span class="sxs-lookup"><span data-stu-id="ad299-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="ad299-229">**filename** 및 **fileFilter**는 동시에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-hello-partionedby-property"></a><span data-ttu-id="ad299-230">Hello partionedBy 속성 사용</span><span class="sxs-lookup"><span data-stu-id="ad299-230">Use hello partionedBy property</span></span>
<span data-ttu-id="ad299-231">Hello 이전 섹션에서 설명 했 듯이 동적을 지정할 수 있습니다 **folderPath** 및 **fileName** hello로 시계열 데이터에 대 한 **partitionedBy** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-231">As mentioned in hello previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with hello **partitionedBy** property.</span></span>

<span data-ttu-id="ad299-232">toolearn 시간 시계열 데이터 집합, 일정 및 분할 하는 방법에 대 한 참조 [데이터 집합을 만드는](data-factory-create-datasets.md), [일정 예약 및 실행](data-factory-scheduling-and-execution.md), 및 [파이프라인 만들기](data-factory-create-pipelines.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-232">toolearn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="ad299-233">샘플 1</span><span class="sxs-lookup"><span data-stu-id="ad299-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="ad299-234">이 예제에서 {Slice}는 데이터 팩터리 시스템 변수 SliceStart의 hello 값으로 대체 됩니다, 그리고 hello에 지정 된 (yyyymmddhh).</span><span class="sxs-lookup"><span data-stu-id="ad299-234">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart, in hello format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="ad299-235">hello SliceStart hello 조각의 toostart 시간을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-235">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="ad299-236">hello 폴더 경로 각 조각에 대 한 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-236">hello folder path is different for each slice.</span></span> <span data-ttu-id="ad299-237">(예를 들어 wikidatagateway/wikisampledataout/2014100103 또는 wikidatagateway/wikisampledataout/2014100104입니다.)</span><span class="sxs-lookup"><span data-stu-id="ad299-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="ad299-238">샘플 2</span><span class="sxs-lookup"><span data-stu-id="ad299-238">Sample 2</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="ad299-239">Hello에서 사용 되는 개별 변수로 hello 연도, 월, 일 및 시간 SliceStart의이 예제에서는 추출 **folderPath** 및 **fileName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-239">In this example, hello year, month, day, and time of SliceStart are extracted into separate variables that are used by hello **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="ad299-240">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="ad299-240">Copy activity properties</span></span>
<span data-ttu-id="ad299-241">작업 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad299-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="ad299-242">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="ad299-243">Hello에 사용할 수 있는 속성 **typeProperties** 섹션 hello hello에 활동 반면, 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-243">Properties available in hello **typeProperties** section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="ad299-244">Hello 복사 작업에 대 한 hello 형식 속성의 원본 및 싱크 hello 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-244">For hello copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="ad299-245">Hello 원본 유형인 경우 복사 활동에서 **FileSystemSource**, hello 다음 속성은 영어로 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="ad299-245">In copy activity, when hello source is of type **FileSystemSource**, hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="ad299-246">속성</span><span class="sxs-lookup"><span data-stu-id="ad299-246">Property</span></span> | <span data-ttu-id="ad299-247">설명</span><span class="sxs-lookup"><span data-stu-id="ad299-247">Description</span></span> | <span data-ttu-id="ad299-248">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="ad299-248">Allowed values</span></span> | <span data-ttu-id="ad299-249">필수</span><span class="sxs-lookup"><span data-stu-id="ad299-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ad299-250">recursive</span><span class="sxs-lookup"><span data-stu-id="ad299-250">recursive</span></span> |<span data-ttu-id="ad299-251">Hello 데이터 읽는지 재귀적으로 hello 지정 된 폴더 또는 hello 하위 폴더에서 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-251">Indicates whether hello data is read recursively from hello subfolders, or only from hello specified folder.</span></span> |<span data-ttu-id="ad299-252">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="ad299-252">True, False (default)</span></span> |<span data-ttu-id="ad299-253">아니요</span><span class="sxs-lookup"><span data-stu-id="ad299-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a><span data-ttu-id="ad299-254">JSON의 예: FTP 서버 tooAzure Blob에서에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="ad299-254">JSON example: Copy data from FTP server tooAzure Blob</span></span>
<span data-ttu-id="ad299-255">이 샘플은 어떻게 FTP 서버 tooAzure Blob 저장소에서에서 toocopy 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-255">This sample shows how toocopy data from an FTP server tooAzure Blob storage.</span></span> <span data-ttu-id="ad299-256">하지만 hello tooany 싱크에 언급 된 hello 직접 데이터 복사할 수 있습니다 [지원 되는 데이터 저장소 및 형식](data-factory-data-movement-activities.md#supported-data-stores-and-formats), Data Factory에 hello 복사 작업을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-256">However, data can be copied directly tooany of hello sinks stated in hello [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using hello copy activity in Data Factory.</span></span>  

<span data-ttu-id="ad299-257">hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), 또는 [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="ad299-257">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="ad299-258">[FtpServer](#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="ad299-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="ad299-259">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="ad299-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="ad299-260">[FileShare](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="ad299-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="ad299-261">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="ad299-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="ad299-262">[FileSystemSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="ad299-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="ad299-263">hello 샘플 데이터 복사 FTP 서버 tooan Azure blob에서에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-263">hello sample copies data from an FTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="ad299-264">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-264">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="ad299-265">FTP 연결 서비스</span><span class="sxs-lookup"><span data-stu-id="ad299-265">FTP linked service</span></span>

<span data-ttu-id="ad299-266">이 예제에서는 hello 사용자 이름과 암호가 일반 텍스트로 기본 인증을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-266">This example uses basic authentication, with hello user name and password in plain text.</span></span> <span data-ttu-id="ad299-267">또한 hello 같은 방법으로 다음 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-267">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="ad299-268">익명 인증 </span><span class="sxs-lookup"><span data-stu-id="ad299-268">Anonymous authentication</span></span>
* <span data-ttu-id="ad299-269">암호화된 자격 증명으로 기본 인증 </span><span class="sxs-lookup"><span data-stu-id="ad299-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="ad299-270">SSL/TLS 경우 FTP(FTPS)</span><span class="sxs-lookup"><span data-stu-id="ad299-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="ad299-271">Hello 참조 [FTP 연결 된 서비스](#linked-service-properties) 섹션에 대 한 다양 한 유형의 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-271">See hello [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a><span data-ttu-id="ad299-272">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="ad299-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="ad299-273">FTP 입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="ad299-273">FTP input dataset</span></span>

<span data-ttu-id="ad299-274">이 데이터 집합 참조 toohello FTP 폴더 `mysharedfolder` 파일과 `test.csv`합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-274">This dataset refers toohello FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="ad299-275">hello 파이프라인 hello 파일 toohello 대상에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-275">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="ad299-276">설정 **외부** 너무**true** 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-276">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory, and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="ad299-277">Azure Blob 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="ad299-277">Azure Blob output dataset</span></span>

<span data-ttu-id="ad299-278">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="ad299-278">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ad299-279">hello 폴더 경로 hello blob에 대 한 동적으로 평가 처리 중인 hello 조각의 hello 시작 시간에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-279">hello folder path for hello blob is dynamically evaluated, based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="ad299-280">hello 폴더 경로 hello 시작 시간의 hello 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-280">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="ad299-281">파일 시스템 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업</span><span class="sxs-lookup"><span data-stu-id="ad299-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="ad299-282">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-282">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="ad299-283">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**FileSystemSource**, 및 hello **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-283">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and hello **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="ad299-284">원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 toomap 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-284">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad299-285">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ad299-285">Next steps</span></span>
<span data-ttu-id="ad299-286">Hello 다음 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="ad299-286">See hello following articles:</span></span>

* <span data-ttu-id="ad299-287">키에 대 한 toolearn Data Factory에서 데이터 이동을 (복사 작업) 및 다양 한 방법으로 toooptimize의 성능에 영향을 해당 요소를 hello 참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-287">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="ad299-288">복사 작업을 사용 하 여 파이프라인 만들기에 대 한 단계별 지침은 참조 hello [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ad299-288">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
