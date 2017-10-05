---
title: "Azure Data Factory를 사용하여 FTP 서버에서 데이터 이동 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 FTP 서버에서 데이터를 이동하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: f8f31f3a2ee02c964737dd32145499f3dcfd0624
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="d3485-103">Azure Data Factory를 사용하여 FTP 서버에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="d3485-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="d3485-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 FTP 서버에서 데이터를 이동하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-104">This article explains how to use the copy activity in Azure Data Factory to move data from an FTP server.</span></span> <span data-ttu-id="d3485-105">이 문서는 복사 작업을 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="d3485-106">FTP 서버에서 지원되는 모든 싱크 데이터 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-106">You can copy data from an FTP server to any supported sink data store.</span></span> <span data-ttu-id="d3485-107">복사 작업의 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-107">For a list of data stores supported as sinks by the copy activity, see the [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="d3485-108">현재 데이터 팩터리는 FTP 서버에서 다른 데이터 저장소로의 데이터 이동만 지원하며, 다른 데이터 저장소에서 FTP 서버로의 데이터 이동은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-108">Data Factory currently supports only moving data from an FTP server to other data stores, but not moving data from other data stores to an FTP server.</span></span> <span data-ttu-id="d3485-109">온-프레미스 및 클라우드 FTP 서버를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="d3485-110">복사 작업 시 원본 파일이 대상에 성공적으로 복사된 후 원본 파일이 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-110">The copy activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="d3485-111">성공적 복사 후 원본 파일을 삭제해야 할 경우 파일을 삭제하는 사용자 지정 작업을 만들고 파이프라인에서 해당 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-111">If you need to delete the source file after a successful copy, create a custom activity to delete the file, and use the activity in the pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="d3485-112">연결 설정</span><span class="sxs-lookup"><span data-stu-id="d3485-112">Enable connectivity</span></span>
<span data-ttu-id="d3485-113">**온-프레미스** FTP 서버의 데이터를 클라우드 데이터 저장소(예: Azure Blob Storage)로 이동하는 경우 데이터 관리 게이트웨이를 설치하여 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-113">If you are moving data from an **on-premises** FTP server to a cloud data store (for example, to Azure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="d3485-114">데이터 관리 게이트웨이는 온-프레미스 컴퓨터에 설치되는 클라이언트 에이전트로, 클라우드 서비스가 온-프레미스 리소스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-114">The Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services to connect to an on-premises resource.</span></span> <span data-ttu-id="d3485-115">자세한 내용은 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="d3485-116">게이트웨이 설정 및 사용에 대한 단계별 지침은 [온-프레미스 위치 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-116">For step-by-step instructions on setting up the gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="d3485-117">서버가 Azure IaaS(Infrastructure as a Service) 가상 컴퓨터(VM)인 경우에도 게이트웨이를 사용하여 FTP 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-117">You use the gateway to connect to an FTP server, even if the server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="d3485-118">FTP 서버로 동일한 온-프레미스 컴퓨터 또는 IaaS VM에 게이트웨이를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-118">It is possible to install the gateway on the same on-premises machine or IaaS VM as the FTP server.</span></span> <span data-ttu-id="d3485-119">그러나 리소스 경합을 방지하고 성능 향상을 꾀하려면 게이트웨이를 별도 컴퓨터 또는 IaaS VM에 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-119">However, we recommend that you install the gateway on a separate machine or IaaS VM to avoid resource contention, and for better performance.</span></span> <span data-ttu-id="d3485-120">별도 컴퓨터에 게이트웨이를 설치하는 경우 컴퓨터가 FTP 서버에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-120">When you install the gateway on a separate machine, the machine should be able to access the FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="d3485-121">시작</span><span class="sxs-lookup"><span data-stu-id="d3485-121">Get started</span></span>
<span data-ttu-id="d3485-122">다른 도구 또는 API를 사용하여 FTP 원본의 데이터를 이동하는 복사 작업이 포함된 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="d3485-123">파이프라인을 만드는 가장 쉬운 방법은 **데이터 팩터리 복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-123">The easiest way to create a pipeline is to use the **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="d3485-124">빠른 연습을 위해서는 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="d3485-125">또한 **Azure Portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API** 도구를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d3485-126">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="d3485-127">도구를 사용하거나 API를 사용하는 경우에도 다음 단계에 따라 원본 데이터 저장소에서 싱크 데이터 저장소로 데이터를 이동하는 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-127">Whether you use the tools or APIs, perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="d3485-128">입력 및 출력 데이터 저장소를 데이터 팩터리에 연결하는 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="d3485-129">복사 작업의 입력 및 출력 데이터를 나타내는 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-129">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="d3485-130">입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="d3485-131">마법사를 사용하는 경우 이러한 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)에 대한 JSON 정의가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="d3485-132">도구 또는 API(.NET API 제외)를 사용하는 경우 JSON 형식을 사용하여 이러한 데이터 팩터리 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="d3485-133">FTP 데이터 저장소의 데이터를 복사하는 데 사용되는 데이터 팩터리 엔터티의 JSON 정의에 대한 샘플은 이 문서의 [JSON의 예: FTP 서버에서 Azure Blob으로 데이터 복사](#json-example-copy-data-from-ftp-server-to-azure-blob) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an FTP data store, see the [JSON example: Copy data from FTP server to Azure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="d3485-134">지원되는 파일 및 사용할 압축 파일에 대한 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-134">For details about supported file and compression formats to use, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="d3485-135">다음 섹션에서는 FTP에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 JSON 속성에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to FTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d3485-136">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="d3485-136">Linked service properties</span></span>
<span data-ttu-id="d3485-137">다음 테이블은 FTP 연결 서비스에만 해당하는 JSON 요소에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-137">The following table describes JSON elements specific to an FTP linked service.</span></span>

| <span data-ttu-id="d3485-138">속성</span><span class="sxs-lookup"><span data-stu-id="d3485-138">Property</span></span> | <span data-ttu-id="d3485-139">설명</span><span class="sxs-lookup"><span data-stu-id="d3485-139">Description</span></span> | <span data-ttu-id="d3485-140">필수</span><span class="sxs-lookup"><span data-stu-id="d3485-140">Required</span></span> | <span data-ttu-id="d3485-141">기본값</span><span class="sxs-lookup"><span data-stu-id="d3485-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d3485-142">type</span><span class="sxs-lookup"><span data-stu-id="d3485-142">type</span></span> |<span data-ttu-id="d3485-143">FtpServer로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-143">Set this to FtpServer.</span></span> |<span data-ttu-id="d3485-144">예</span><span class="sxs-lookup"><span data-stu-id="d3485-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="d3485-145">host</span><span class="sxs-lookup"><span data-stu-id="d3485-145">host</span></span> |<span data-ttu-id="d3485-146">FTP 서버의 이름 또는 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-146">Specify the name or IP address of the FTP server.</span></span> |<span data-ttu-id="d3485-147">예</span><span class="sxs-lookup"><span data-stu-id="d3485-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="d3485-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="d3485-148">authenticationType</span></span> |<span data-ttu-id="d3485-149">인증 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-149">Specify the authentication type.</span></span> |<span data-ttu-id="d3485-150">예</span><span class="sxs-lookup"><span data-stu-id="d3485-150">Yes</span></span> |<span data-ttu-id="d3485-151">기본, 익명</span><span class="sxs-lookup"><span data-stu-id="d3485-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="d3485-152">username</span><span class="sxs-lookup"><span data-stu-id="d3485-152">username</span></span> |<span data-ttu-id="d3485-153">FTP 서버에 액세스하는 사용자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-153">Specify the user who has access to the FTP server.</span></span> |<span data-ttu-id="d3485-154">아니요</span><span class="sxs-lookup"><span data-stu-id="d3485-154">No</span></span> |&nbsp; |
| <span data-ttu-id="d3485-155">password</span><span class="sxs-lookup"><span data-stu-id="d3485-155">password</span></span> |<span data-ttu-id="d3485-156">사용자(사용자 이름)의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-156">Specify the password for the user (username).</span></span> |<span data-ttu-id="d3485-157">아니요</span><span class="sxs-lookup"><span data-stu-id="d3485-157">No</span></span> |&nbsp; |
| <span data-ttu-id="d3485-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d3485-158">encryptedCredential</span></span> |<span data-ttu-id="d3485-159">FTP 서버 액세스를 위한 암호화된 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-159">Specify the encrypted credential to access the FTP server.</span></span> |<span data-ttu-id="d3485-160">아니요</span><span class="sxs-lookup"><span data-stu-id="d3485-160">No</span></span> |&nbsp; |
| <span data-ttu-id="d3485-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d3485-161">gatewayName</span></span> |<span data-ttu-id="d3485-162">온-프레미스 FTP 서버에 연결하기 위한 데이터 관리 게이트웨이의 게이트웨이 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-162">Specify the name of the gateway in Data Management Gateway to connect to an on-premises FTP server.</span></span> |<span data-ttu-id="d3485-163">아니요</span><span class="sxs-lookup"><span data-stu-id="d3485-163">No</span></span> |&nbsp; |
| <span data-ttu-id="d3485-164">포트</span><span class="sxs-lookup"><span data-stu-id="d3485-164">port</span></span> |<span data-ttu-id="d3485-165">FTP 서버가 수신 대기하는 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-165">Specify the port on which the FTP server is listening.</span></span> |<span data-ttu-id="d3485-166">아니요</span><span class="sxs-lookup"><span data-stu-id="d3485-166">No</span></span> |<span data-ttu-id="d3485-167">21</span><span class="sxs-lookup"><span data-stu-id="d3485-167">21</span></span> |
| <span data-ttu-id="d3485-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="d3485-168">enableSsl</span></span> |<span data-ttu-id="d3485-169">SSL/TLS 채널을 통해 FTP를 사용할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-169">Specify whether to use FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="d3485-170">아니요</span><span class="sxs-lookup"><span data-stu-id="d3485-170">No</span></span> |<span data-ttu-id="d3485-171">true</span><span class="sxs-lookup"><span data-stu-id="d3485-171">true</span></span> |
| <span data-ttu-id="d3485-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="d3485-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="d3485-173">SSL/TLS 채널을 통해 FTP를 사용할 때 서버 SSL 인증서 유효성 검사를 사용할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-173">Specify whether to enable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="d3485-174">아니요</span><span class="sxs-lookup"><span data-stu-id="d3485-174">No</span></span> |<span data-ttu-id="d3485-175">true</span><span class="sxs-lookup"><span data-stu-id="d3485-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="d3485-176">익명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="d3485-176">Use Anonymous authentication</span></span>

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

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="d3485-177">일반 텍스트에 사용자 이름 및 암호를 기본 인증에 사용</span><span class="sxs-lookup"><span data-stu-id="d3485-177">Use username and password in plain text for basic authentication</span></span>

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

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="d3485-178">포트, enableSsl, enableServerCertificateValidation 사용</span><span class="sxs-lookup"><span data-stu-id="d3485-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

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

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="d3485-179">인증 및 게이트웨이에 encryptedCredential 사용</span><span class="sxs-lookup"><span data-stu-id="d3485-179">Use encryptedCredential for authentication and gateway</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="d3485-180">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="d3485-180">Dataset properties</span></span>
<span data-ttu-id="d3485-181">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="d3485-182">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="d3485-183">**typeProperties** 섹션은 데이터 집합의 각 형식마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-183">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="d3485-184">데이터 집합 형식에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-184">It provides information that is specific to the dataset type.</span></span> <span data-ttu-id="d3485-185">**FileShare** 형식의 데이터 집합에 대한 **typeProperties** 섹션에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-185">The **typeProperties** section for a dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="d3485-186">속성</span><span class="sxs-lookup"><span data-stu-id="d3485-186">Property</span></span> | <span data-ttu-id="d3485-187">설명</span><span class="sxs-lookup"><span data-stu-id="d3485-187">Description</span></span> | <span data-ttu-id="d3485-188">필수</span><span class="sxs-lookup"><span data-stu-id="d3485-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d3485-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="d3485-189">folderPath</span></span> |<span data-ttu-id="d3485-190">폴더의 하위 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-190">Subpath to the folder.</span></span> <span data-ttu-id="d3485-191">문자열의 특수 문자에 이스케이프 문자 '\'를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-191">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="d3485-192">예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="d3485-193">이 속성을 **partitionBy**와 결합하여 조각 시작 및 종료 날짜-시간을 기준으로 폴더 경로를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-193">You can combine this property with **partitionBy** to have folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="d3485-194">예</span><span class="sxs-lookup"><span data-stu-id="d3485-194">Yes</span></span> |
| <span data-ttu-id="d3485-195">fileName</span><span class="sxs-lookup"><span data-stu-id="d3485-195">fileName</span></span> |<span data-ttu-id="d3485-196">폴더에서 특정 파일을 참조하기 위해 테이블을 사용하려는 경우 **folderPath** 에 있는 파일의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-196">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="d3485-197">이 속성에 값을 지정하지 않으면 테이블은 폴더에 있는 모든 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-197">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="d3485-198">출력 데이터 집합에 대한 **fileName**이 지정되지 않은 경우 생성되는 파일의 이름 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-198">When **fileName** is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="d3485-199">Data.<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="d3485-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="d3485-200">아니요</span><span class="sxs-lookup"><span data-stu-id="d3485-200">No</span></span> |
| <span data-ttu-id="d3485-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="d3485-201">fileFilter</span></span> |<span data-ttu-id="d3485-202">모든 파일이 아닌 **folderPath**의 파일 하위 집합을 선택하는데 사용할 필터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-202">Specify a filter to be used to select a subset of files in the **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="d3485-203">허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="d3485-204">예 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="d3485-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="d3485-205">예 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="d3485-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="d3485-206">**fileFilter**는 FileShare 입력 데이터 집합에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="d3485-207">이 속성은 HDFS(Hadoop Distributed File System)에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="d3485-208">아니요</span><span class="sxs-lookup"><span data-stu-id="d3485-208">No</span></span> |
| <span data-ttu-id="d3485-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="d3485-209">partitionedBy</span></span> |<span data-ttu-id="d3485-210">동적 **folderPath** 및 시계열 데이터에 대한 **filename**을 지정하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-210">Used to specify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="d3485-211">예를 들어 매 시간 데이터에 대해 매개 변수가 있는 **folderPath**를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="d3485-212">아니요</span><span class="sxs-lookup"><span data-stu-id="d3485-212">No</span></span> |
| <span data-ttu-id="d3485-213">format</span><span class="sxs-lookup"><span data-stu-id="d3485-213">format</span></span> | <span data-ttu-id="d3485-214">**TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**과 같은 서식 유형이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-214">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="d3485-215">이 값 중 하나로 서식에서 **type** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-215">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="d3485-216">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-216">For more information, see the [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="d3485-217">파일 기반 저장소(이진 복사) 간에 파일을 있는 그대로 복사하려는 경우 입력 및 출력 데이터 집합 정의에서 형식 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-217">If you want to copy files as they are between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="d3485-218">아니요</span><span class="sxs-lookup"><span data-stu-id="d3485-218">No</span></span> |
| <span data-ttu-id="d3485-219">압축</span><span class="sxs-lookup"><span data-stu-id="d3485-219">compression</span></span> | <span data-ttu-id="d3485-220">데이터에 대한 압축 유형 및 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-220">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="d3485-221">지원되는 형식은 **GZip**, **Deflate**, **BZip2**, **ZipDeflate**이고 지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="d3485-222">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="d3485-223">아니요</span><span class="sxs-lookup"><span data-stu-id="d3485-223">No</span></span> |
| <span data-ttu-id="d3485-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="d3485-224">useBinaryTransfer</span></span> |<span data-ttu-id="d3485-225">이진 전송 모드를 사용할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-225">Specify whether to use the binary transfer mode.</span></span> <span data-ttu-id="d3485-226">값은 이진 모드(기본값)에서만 true이며 ASCII에서는 false입니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-226">The values are true for binary mode (this is the default value), and false for ASCII.</span></span> <span data-ttu-id="d3485-227">이 속성은 연결된 서비스 유형이 FtpServer인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-227">This property can only be used when the associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="d3485-228">아니요</span><span class="sxs-lookup"><span data-stu-id="d3485-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="d3485-229">**filename** 및 **fileFilter**는 동시에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-the-partionedby-property"></a><span data-ttu-id="d3485-230">partionedBy 속성 사용</span><span class="sxs-lookup"><span data-stu-id="d3485-230">Use the partionedBy property</span></span>
<span data-ttu-id="d3485-231">이전 섹션에서 설명한 대로 **partitionedBy** 속성을 사용하여 시계열 데이터의 동적 **folderPath**와 **fileName**을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-231">As mentioned in the previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with the **partitionedBy** property.</span></span>

<span data-ttu-id="d3485-232">시계열 데이터 집합, 예약 및 조각에 대한 자세한 내용은 [데이터 집합 만들기](data-factory-create-datasets.md), [일정 예약 및 실행](data-factory-scheduling-and-execution.md) 및 [파이프라인 만들기](data-factory-create-pipelines.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-232">To learn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="d3485-233">샘플 1</span><span class="sxs-lookup"><span data-stu-id="d3485-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="d3485-234">이 예제에서 {Slice}는 지정된 형식(YYYYMMDDHH)의 데이터 팩터리 시스템 변수 SliceStart 값으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-234">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart, in the format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="d3485-235">SliceStart는 조각의 시작 시간을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-235">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="d3485-236">폴더 경로는 각 조각에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-236">The folder path is different for each slice.</span></span> <span data-ttu-id="d3485-237">(예를 들어 wikidatagateway/wikisampledataout/2014100103 또는 wikidatagateway/wikisampledataout/2014100104입니다.)</span><span class="sxs-lookup"><span data-stu-id="d3485-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="d3485-238">샘플 2</span><span class="sxs-lookup"><span data-stu-id="d3485-238">Sample 2</span></span>

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
<span data-ttu-id="d3485-239">이 예제에서 SliceStart의 연도, 월, 일 및 시간은 **folderPath** 및 **fileName** 속성에서 사용하는 별도 변수로 추출됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-239">In this example, the year, month, day, and time of SliceStart are extracted into separate variables that are used by the **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="d3485-240">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="d3485-240">Copy activity properties</span></span>
<span data-ttu-id="d3485-241">작업 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="d3485-242">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="d3485-243">반면 작업의 **typeProperties** 섹션에서 사용할 수 있는 속성은 각 작업 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-243">Properties available in the **typeProperties** section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="d3485-244">복사 작업의 경우 유형 속성은 원본 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-244">For the copy activity, the type properties vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="d3485-245">원본이 **FileSystemSource** 형식인 복사 작업의 경우 **typeProperties** 섹션에서 다음과 같은 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-245">In copy activity, when the source is of type **FileSystemSource**, the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="d3485-246">속성</span><span class="sxs-lookup"><span data-stu-id="d3485-246">Property</span></span> | <span data-ttu-id="d3485-247">설명</span><span class="sxs-lookup"><span data-stu-id="d3485-247">Description</span></span> | <span data-ttu-id="d3485-248">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="d3485-248">Allowed values</span></span> | <span data-ttu-id="d3485-249">필수</span><span class="sxs-lookup"><span data-stu-id="d3485-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d3485-250">recursive</span><span class="sxs-lookup"><span data-stu-id="d3485-250">recursive</span></span> |<span data-ttu-id="d3485-251">하위 폴더 또는 지정된 폴더에서만 데이터를 재귀적으로 읽을지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-251">Indicates whether the data is read recursively from the subfolders, or only from the specified folder.</span></span> |<span data-ttu-id="d3485-252">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="d3485-252">True, False (default)</span></span> |<span data-ttu-id="d3485-253">아니요</span><span class="sxs-lookup"><span data-stu-id="d3485-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-to-azure-blob"></a><span data-ttu-id="d3485-254">JSON 예: FTP 서버에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="d3485-254">JSON example: Copy data from FTP server to Azure Blob</span></span>
<span data-ttu-id="d3485-255">이 샘플은 FTP 서버에서 Azure Blob Storage로 데이터를 복사하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-255">This sample shows how to copy data from an FTP server to Azure Blob storage.</span></span> <span data-ttu-id="d3485-256">하지만 데이터 팩터리의 복사 작업을 사용하여 [지원되는 데이터 저장소 및 형식](data-factory-data-movement-activities.md#supported-data-stores-and-formats)에 지정된 싱크로 데이터를 직접 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-256">However, data can be copied directly to any of the sinks stated in the [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using the copy activity in Data Factory.</span></span>  

<span data-ttu-id="d3485-257">다음 예에서는 [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-257">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="d3485-258">[FtpServer](#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="d3485-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="d3485-259">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="d3485-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="d3485-260">[FileShare](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="d3485-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="d3485-261">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="d3485-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="d3485-262">[FileSystemSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="d3485-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="d3485-263">샘플은 1시간마다 FTP 서버의 데이터를 Azure Blob으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-263">The sample copies data from an FTP server to an Azure blob every hour.</span></span> <span data-ttu-id="d3485-264">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-264">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="d3485-265">FTP 연결 서비스</span><span class="sxs-lookup"><span data-stu-id="d3485-265">FTP linked service</span></span>

<span data-ttu-id="d3485-266">이 예에서는 일반 텍스트의 사용자 이름과 암호를 기본 인증으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-266">This example uses basic authentication, with the user name and password in plain text.</span></span> <span data-ttu-id="d3485-267">다음 방법 중 하나를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-267">You can also use one of the following ways:</span></span>

* <span data-ttu-id="d3485-268">익명 인증 </span><span class="sxs-lookup"><span data-stu-id="d3485-268">Anonymous authentication</span></span>
* <span data-ttu-id="d3485-269">암호화된 자격 증명으로 기본 인증 </span><span class="sxs-lookup"><span data-stu-id="d3485-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="d3485-270">SSL/TLS 경우 FTP(FTPS)</span><span class="sxs-lookup"><span data-stu-id="d3485-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="d3485-271">사용할 수 있는 다른 유형의 인증은 [FTP 연결 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-271">See the [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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
### <a name="azure-storage-linked-service"></a><span data-ttu-id="d3485-272">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="d3485-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="d3485-273">FTP 입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="d3485-273">FTP input dataset</span></span>

<span data-ttu-id="d3485-274">이 데이터 집합은 FTP 폴더 `mysharedfolder`와 `test.csv` 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-274">This dataset refers to the FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="d3485-275">파이프라인은 파일을 대상에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-275">The pipeline copies the file to the destination.</span></span>

<span data-ttu-id="d3485-276">**external**을 **true**로 설정하면 데이터 집합이 데이터 팩터리의 외부에 있으며 데이터 팩터리의 활동에 의해 생성되지 않는다는 사실이 Data Factory 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-276">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory, and is not produced by an activity in the data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="d3485-277">Azure Blob 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="d3485-277">Azure Blob output dataset</span></span>

<span data-ttu-id="d3485-278">데이터는 매시간 새 blob에 기록됩니다.(빈도: 1시간, 간격:1회)</span><span class="sxs-lookup"><span data-stu-id="d3485-278">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d3485-279">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-279">The folder path for the blob is dynamically evaluated, based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="d3485-280">폴더 경로는 시작 시간의 년, 월, 일 및 시 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-280">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="d3485-281">파일 시스템 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업</span><span class="sxs-lookup"><span data-stu-id="d3485-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="d3485-282">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-282">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="d3485-283">파이프라인 JSON 정의에서 **source** 형식은 **FileSystemSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3485-283">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and the **sink** type is set to **BlobSink**.</span></span>

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
> <span data-ttu-id="d3485-284">원본 데이터 집합의 열을 싱크 데이터 집합의 열로 매핑하려면 [Azure Data Factory의 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-284">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3485-285">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d3485-285">Next steps</span></span>
<span data-ttu-id="d3485-286">다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-286">See the following articles:</span></span>

* <span data-ttu-id="d3485-287">Data Factory에서 데이터 이동(복사 작업) 성능에 영향을 미치는 주요 요소 및 다양한 최적화 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-287">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="d3485-288">복사 작업이 포함된 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3485-288">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
