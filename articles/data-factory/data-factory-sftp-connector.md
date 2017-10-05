---
title: "Azure Data Factory를 사용하여 SFTP 서버에서 데이터 이동 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 온-프레미스 또는 클라우드 SFTP 서버에서 데이터를 이동하는 방법을 알아봅니다."
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
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: 3a73311342489af031ed2ea1489e56292ebf2e09
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a><span data-ttu-id="89612-103">Azure Data Factory를 사용하여 SFTP 서버에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="89612-103">Move data from an SFTP server using Azure Data Factory</span></span>
<span data-ttu-id="89612-104">이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 온-프레미스/클라우드 SFTP 서버의 데이터를 지원되는 싱크 데이터 저장소로 이동하는 방법에 대해 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from an on-premises/cloud SFTP server to a supported sink data store.</span></span> <span data-ttu-id="89612-105">이 문서는 복사 작업 및 지원되는 데이터 저장소를 원본/싱크로 사용한 데이터 이동의 일반적인 개요를 보여주는 [데이터 이동 활동](data-factory-data-movement-activities.md) 문서를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="89612-106">현재 데이터 팩터리는 SFTP 서버에서 다른 데이터 저장소로의 데이터 이동만 지원하며, 다른 데이터 저장소에서 SFTP 서버로의 데이터 이동은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-106">Data factory currently supports only moving data from an SFTP server to other data stores, but not for moving data from other data stores to an SFTP server.</span></span> <span data-ttu-id="89612-107">온-프레미스 및 클라우드 SFTP 서버를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-107">It supports both on-premises and cloud SFTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="89612-108">복사 작업 시 원본 파일이 대상에 성공적으로 복사된 후 원본 파일이 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-108">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="89612-109">성공적 복사 후 원본 파일을 삭제해야 할 경우 파일을 삭제하는 사용자 지정 작업을 만들고 파이프라인에서 해당 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-109">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="89612-110">지원되는 시나리오 및 인증 형식</span><span class="sxs-lookup"><span data-stu-id="89612-110">Supported scenarios and authentication types</span></span>
<span data-ttu-id="89612-111">이 SFTP 커넥터를 사용하여 **클라우드 SFTP 서버와 온-프레미스 SFTP 서버**의 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-111">You can use this SFTP connector to copy data from **both cloud SFTP servers and on-premises SFTP servers**.</span></span> <span data-ttu-id="89612-112">SFTP 서버에 연결할 때 **기본** 및 **SshPublicKey** 인증 유형이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-112">**Basic** and **SshPublicKey** authentication types are supported when connecting to the SFTP server.</span></span>

<span data-ttu-id="89612-113">온-프레미스 SFTP 서버에서 데이터를 복사할 때 온-프레미스 환경/Azure VM에서 데이터 관리 게이트웨이를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-113">When copying data from an on-premises SFTP server, you need install a Data Management Gateway in the on-premises environment/Azure VM.</span></span> <span data-ttu-id="89612-114">게이트웨이에 대한 자세한 내용은 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-114">See [Data Management Gateway](data-factory-data-management-gateway.md) for details on the gateway.</span></span> <span data-ttu-id="89612-115">게이트웨이 설정 및 사용에 대한 단계별 지침은 [온-프레미스 위치 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway and using it.</span></span>

## <a name="getting-started"></a><span data-ttu-id="89612-116">시작</span><span class="sxs-lookup"><span data-stu-id="89612-116">Getting started</span></span>
<span data-ttu-id="89612-117">다른 도구/API를 사용하여 SFTP 원본의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-117">You can create a pipeline with a copy activity that moves data from an SFTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="89612-118">파이프라인을 만드는 가장 쉬운 방법은 **복사 마법사**를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="89612-119">데이터 복사 마법사를 사용하여 파이프라인을 만드는 방법에 대한 빠른 연습은 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

- <span data-ttu-id="89612-120">또한 **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager 템플릿**, **.NET API** 및 **REST API**를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="89612-121">복사 작업을 사용하여 파이프라인을 만드는 단계별 지침은 [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> <span data-ttu-id="89612-122">SFTP 서버에서 Azure Blob Storage로 데이터를 복사하는 JSON 샘플은 이 문서의 [JSON 예제: SFTP 서버에서 Azure blob으로 데이터 복사](#json-example-copy-data-from-sftp-server-to-azure-blob) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-122">For JSON samples to copy data from SFTP server to Azure Blob Storage, see [JSON Example: Copy data from SFTP server to Azure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) section of this article.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="89612-123">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="89612-123">Linked service properties</span></span>
<span data-ttu-id="89612-124">다음 테이블은 FTP 연결 서비스에 특정한 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-124">The following table provides description for JSON elements specific to FTP linked service.</span></span>

| <span data-ttu-id="89612-125">속성</span><span class="sxs-lookup"><span data-stu-id="89612-125">Property</span></span> | <span data-ttu-id="89612-126">설명</span><span class="sxs-lookup"><span data-stu-id="89612-126">Description</span></span> | <span data-ttu-id="89612-127">필수</span><span class="sxs-lookup"><span data-stu-id="89612-127">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="89612-128">type</span><span class="sxs-lookup"><span data-stu-id="89612-128">type</span></span> | <span data-ttu-id="89612-129">type 속성을 `Sftp`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-129">The type property must be set to `Sftp`.</span></span> |<span data-ttu-id="89612-130">예</span><span class="sxs-lookup"><span data-stu-id="89612-130">Yes</span></span> |
| <span data-ttu-id="89612-131">host</span><span class="sxs-lookup"><span data-stu-id="89612-131">host</span></span> | <span data-ttu-id="89612-132">SFTP 서버의 이름 또는 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-132">Name or IP address of the SFTP server.</span></span> |<span data-ttu-id="89612-133">예</span><span class="sxs-lookup"><span data-stu-id="89612-133">Yes</span></span> |
| <span data-ttu-id="89612-134">포트</span><span class="sxs-lookup"><span data-stu-id="89612-134">port</span></span> |<span data-ttu-id="89612-135">SFTP 서버가 수신하는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-135">Port on which the SFTP server is listening.</span></span> <span data-ttu-id="89612-136">기본값은 21입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-136">The default value is: 21</span></span> |<span data-ttu-id="89612-137">아니요</span><span class="sxs-lookup"><span data-stu-id="89612-137">No</span></span> |
| <span data-ttu-id="89612-138">authenticationType</span><span class="sxs-lookup"><span data-stu-id="89612-138">authenticationType</span></span> |<span data-ttu-id="89612-139">인증 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-139">Specify authentication type.</span></span> <span data-ttu-id="89612-140">허용되는 값은 **기본** 및 **SshPublicKey**입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-140">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="89612-141">더 많은 속성 및 각 속성의 JSON 샘플은 [기본 인증 사용](#using-basic-authentication) 및 [SSH 공개 키 인증 사용](#using-ssh-public-key-authentication) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-141">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="89612-142">예</span><span class="sxs-lookup"><span data-stu-id="89612-142">Yes</span></span> |
| <span data-ttu-id="89612-143">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="89612-143">skipHostKeyValidation</span></span> | <span data-ttu-id="89612-144">호스트 키 유효성 검사를 건너뛸지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-144">Specify whether to skip host key validation.</span></span> | <span data-ttu-id="89612-145">아니요.</span><span class="sxs-lookup"><span data-stu-id="89612-145">No.</span></span> <span data-ttu-id="89612-146">기본값: false</span><span class="sxs-lookup"><span data-stu-id="89612-146">The default value: false</span></span> |
| <span data-ttu-id="89612-147">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="89612-147">hostKeyFingerprint</span></span> | <span data-ttu-id="89612-148">호스트 키의 지문을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-148">Specify the finger print of the host key.</span></span> | <span data-ttu-id="89612-149">`skipHostKeyValidation`이 false로 지정되면 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-149">Yes if the `skipHostKeyValidation` is set to false.</span></span>  |
| <span data-ttu-id="89612-150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="89612-150">gatewayName</span></span> |<span data-ttu-id="89612-151">온-프레미스 SFTP 서버에 연결하기 위한 데이터 관리 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-151">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span></span> | <span data-ttu-id="89612-152">온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-152">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="89612-153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="89612-153">encryptedCredential</span></span> | <span data-ttu-id="89612-154">SFTP 서버 액세스를 위한 암호화된 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-154">Encrypted credential to access the SFTP server.</span></span> <span data-ttu-id="89612-155">복사 마법사 또는 ClickOnce 팝업 대화 상자에서 기본 인증(사용자 이름 + 암호) 또는 SshPublicKey 인증(사용자 이름 + 개인 키 경로 또는 콘텐츠)를 지정할 때 자정으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-155">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="89612-156">아니요.</span><span class="sxs-lookup"><span data-stu-id="89612-156">No.</span></span> <span data-ttu-id="89612-157">온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-157">Apply only when copying data from an on-premises SFTP server.</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="89612-158">기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="89612-158">Using basic authentication</span></span>

<span data-ttu-id="89612-159">기본 인증을 사용하려면 `authenticationType`을 `Basic`으로 설정하고, 마지막 섹션에서 소개한 SFTP 커넥터 일반 속성 외에 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-159">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="89612-160">속성</span><span class="sxs-lookup"><span data-stu-id="89612-160">Property</span></span> | <span data-ttu-id="89612-161">설명</span><span class="sxs-lookup"><span data-stu-id="89612-161">Description</span></span> | <span data-ttu-id="89612-162">필수</span><span class="sxs-lookup"><span data-stu-id="89612-162">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="89612-163">username</span><span class="sxs-lookup"><span data-stu-id="89612-163">username</span></span> | <span data-ttu-id="89612-164">SFTP 서버에 액세스하는 사용자.</span><span class="sxs-lookup"><span data-stu-id="89612-164">User who has access to the SFTP server.</span></span> |<span data-ttu-id="89612-165">예</span><span class="sxs-lookup"><span data-stu-id="89612-165">Yes</span></span> |
| <span data-ttu-id="89612-166">password</span><span class="sxs-lookup"><span data-stu-id="89612-166">password</span></span> | <span data-ttu-id="89612-167">사용자(사용자 이름) 암호.</span><span class="sxs-lookup"><span data-stu-id="89612-167">Password for the user (username).</span></span> | <span data-ttu-id="89612-168">예</span><span class="sxs-lookup"><span data-stu-id="89612-168">Yes</span></span> |

#### <a name="example-basic-authentication"></a><span data-ttu-id="89612-169">예: 기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="89612-169">Example: Basic authentication</span></span>
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="89612-170">예: 암호화된 자격 증명으로 기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="89612-170">Example: Basic authentication with encrypted credential</span></span>

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="89612-171">SSH 공개 키 인증 사용</span><span class="sxs-lookup"><span data-stu-id="89612-171">Using SSH public key authentication</span></span>

<span data-ttu-id="89612-172">SSH 공개 키 인증을 사용하려면 `authenticationType`을 `SshPublicKey`으로 설정하고, 마지막 섹션에서 소개한 SFTP 커넥터 일반 속성 외에 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-172">To use SSH public key authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="89612-173">속성</span><span class="sxs-lookup"><span data-stu-id="89612-173">Property</span></span> | <span data-ttu-id="89612-174">설명</span><span class="sxs-lookup"><span data-stu-id="89612-174">Description</span></span> | <span data-ttu-id="89612-175">필수</span><span class="sxs-lookup"><span data-stu-id="89612-175">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="89612-176">username</span><span class="sxs-lookup"><span data-stu-id="89612-176">username</span></span> |<span data-ttu-id="89612-177">SFTP 서버에 액세스하는 사용자</span><span class="sxs-lookup"><span data-stu-id="89612-177">User who has access to the SFTP server</span></span> |<span data-ttu-id="89612-178">예</span><span class="sxs-lookup"><span data-stu-id="89612-178">Yes</span></span> |
| <span data-ttu-id="89612-179">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="89612-179">privateKeyPath</span></span> | <span data-ttu-id="89612-180">게이트웨이에서 액세스할 수 있는 개인 키 파일의 절대 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-180">Specify absolute path to the private key file that gateway can access.</span></span> | <span data-ttu-id="89612-181">`privateKeyPath` 또는 `privateKeyContent`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-181">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="89612-182">온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-182">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="89612-183">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="89612-183">privateKeyContent</span></span> | <span data-ttu-id="89612-184">개인 키 콘텐츠의 직렬화된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-184">A serialized string of the private key content.</span></span> <span data-ttu-id="89612-185">복사 마법사는 개인 키 파일을 읽고 개인 키 콘텐츠를 자동으로 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-185">The Copy Wizard can read the private key file and extract the private key content automatically.</span></span> <span data-ttu-id="89612-186">다른 도구/SDK를 사용하는 경우 privateKeyPath 속성을 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-186">If you are using any other tool/SDK, use the privateKeyPath property instead.</span></span> | <span data-ttu-id="89612-187">`privateKeyPath` 또는 `privateKeyContent`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-187">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="89612-188">passPhrase</span><span class="sxs-lookup"><span data-stu-id="89612-188">passPhrase</span></span> | <span data-ttu-id="89612-189">키 파일이 암호문으로 보호되는 경우 개인 키를 해독하는 암호문/암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-189">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span></span> | <span data-ttu-id="89612-190">개인 키 파일이 암호문으로 보호되는 경우에는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-190">Yes if the private key file is protected by a pass phrase.</span></span> |

> [!NOTE]
> <span data-ttu-id="89612-191">SFTP 커넥터는 OpenSSH 키만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-191">SFTP connector only support OpenSSH key.</span></span> <span data-ttu-id="89612-192">키 파일이 적절한 형식인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-192">Make sure your key file is in the proper format.</span></span> <span data-ttu-id="89612-193">Putty 도구를 사용하여 .ppk에서 OpenSSH 형식으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-193">You can use Putty tool to convert from .ppk to OpenSSH format.</span></span>

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a><span data-ttu-id="89612-194">예: 개인 키 파일 경로를 사용하여 SshPublicKey 인증</span><span class="sxs-lookup"><span data-stu-id="89612-194">Example: SshPublicKey authentication using private key filePath</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="89612-195">예: 개인 키 콘텐츠를 사용하여 SshPublicKey 인증</span><span class="sxs-lookup"><span data-stu-id="89612-195">Example: SshPublicKey authentication using private key content</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of the private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="89612-196">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="89612-196">Dataset properties</span></span>
<span data-ttu-id="89612-197">데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-197">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="89612-198">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-198">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="89612-199">**typeProperties** 섹션은 데이터 집합의 각 형식마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="89612-199">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="89612-200">데이터 집합 형식에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-200">It provides information that is specific to the dataset type.</span></span> <span data-ttu-id="89612-201">**FileShare** 데이터 집합 형식의 데이터 집합에 대한 typeProperties 섹션에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-201">The typeProperties section for a dataset of type **FileShare** dataset has the following properties:</span></span>

| <span data-ttu-id="89612-202">속성</span><span class="sxs-lookup"><span data-stu-id="89612-202">Property</span></span> | <span data-ttu-id="89612-203">설명</span><span class="sxs-lookup"><span data-stu-id="89612-203">Description</span></span> | <span data-ttu-id="89612-204">필수</span><span class="sxs-lookup"><span data-stu-id="89612-204">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="89612-205">folderPath</span><span class="sxs-lookup"><span data-stu-id="89612-205">folderPath</span></span> |<span data-ttu-id="89612-206">폴더에 대한 하위 경로.</span><span class="sxs-lookup"><span data-stu-id="89612-206">Sub path to the folder.</span></span> <span data-ttu-id="89612-207">문자열의 특수 문자에 이스케이프 문자 '\'를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-207">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="89612-208">예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-208">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="89612-209">이 속성을 **partitionBy** 와 결합하여 조각 시작/종료 날짜/시간을 기준으로 폴더 경로를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-209">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="89612-210">예</span><span class="sxs-lookup"><span data-stu-id="89612-210">Yes</span></span> |
| <span data-ttu-id="89612-211">fileName</span><span class="sxs-lookup"><span data-stu-id="89612-211">fileName</span></span> |<span data-ttu-id="89612-212">폴더에서 특정 파일을 참조하기 위해 테이블을 사용하려는 경우 **folderPath** 에 있는 파일의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-212">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="89612-213">이 속성에 값을 지정하지 않으면 테이블은 폴더에 있는 모든 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="89612-213">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="89612-214">출력 데이터 집합에 대한 fileName이 지정되는 경우 생성되는 파일의 이름 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-214">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="89612-215">Data.<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="89612-215">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="89612-216">아니요</span><span class="sxs-lookup"><span data-stu-id="89612-216">No</span></span> |
| <span data-ttu-id="89612-217">fileFilter</span><span class="sxs-lookup"><span data-stu-id="89612-217">fileFilter</span></span> |<span data-ttu-id="89612-218">모든 파일이 아닌 folderPath의 파일 하위 집합을 선택하는데 사용할 필터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-218">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="89612-219">허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-219">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="89612-220">예 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="89612-220">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="89612-221">예 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="89612-221">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="89612-222">fileFilter는 FileShare 입력 데이터 집합에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-222">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="89612-223">이 속성은 HDFS에는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-223">This property is not supported with HDFS.</span></span> |<span data-ttu-id="89612-224">아니요</span><span class="sxs-lookup"><span data-stu-id="89612-224">No</span></span> |
| <span data-ttu-id="89612-225">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="89612-225">partitionedBy</span></span> |<span data-ttu-id="89612-226">동적 folderPath, 시계열 데이터에 대한 filename을 지정하는 데 partitionedBy를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-226">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="89612-227">예를 들어 매시간 데이터에 대한 매개 변수가 있는 folderPath입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-227">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="89612-228">아니요</span><span class="sxs-lookup"><span data-stu-id="89612-228">No</span></span> |
| <span data-ttu-id="89612-229">format</span><span class="sxs-lookup"><span data-stu-id="89612-229">format</span></span> | <span data-ttu-id="89612-230">**TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**과 같은 서식 유형이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-230">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="89612-231">이 값 중 하나로 서식에서 **type** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-231">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="89612-232">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-232">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="89612-233">파일 기반 저장소(이진 복사) 간에 **파일을 있는 그대로 복사**하려는 경우 입력 및 출력 데이터 집합 정의 둘 다에서 형식 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="89612-233">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="89612-234">아니요</span><span class="sxs-lookup"><span data-stu-id="89612-234">No</span></span> |
| <span data-ttu-id="89612-235">압축</span><span class="sxs-lookup"><span data-stu-id="89612-235">compression</span></span> | <span data-ttu-id="89612-236">데이터에 대한 압축 유형 및 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-236">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="89612-237">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-237">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="89612-238">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-238">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="89612-239">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-239">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="89612-240">아니요</span><span class="sxs-lookup"><span data-stu-id="89612-240">No</span></span> |
| <span data-ttu-id="89612-241">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="89612-241">useBinaryTransfer</span></span> |<span data-ttu-id="89612-242">이전 전송 모드를 사용할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-242">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="89612-243">이진 모드인 경우 true이고 ASCII인 경우 false입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-243">True for binary mode and false ASCII.</span></span> <span data-ttu-id="89612-244">기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-244">Default value: True.</span></span> <span data-ttu-id="89612-245">이 속성은 연결된 서비스 유형이 FtpServer인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-245">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="89612-246">아니요</span><span class="sxs-lookup"><span data-stu-id="89612-246">No</span></span> |

> [!NOTE]
> <span data-ttu-id="89612-247">filename 및 fileFilter는 동시에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-247">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="89612-248">partionedBy 속성 사용</span><span class="sxs-lookup"><span data-stu-id="89612-248">Using partionedBy property</span></span>
<span data-ttu-id="89612-249">이전 섹션에서 설명했듯이 동적 folderPath, partitionedBy된 시계열 데이터에 대한 filename을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-249">As mentioned in the previous section, you can specify a dynamic folderPath, filename for time series data with partitionedBy.</span></span> <span data-ttu-id="89612-250">지정된 데이터 조각에 대한 논리적 기간을 나타내는 데이터 팩터리 매크로 및 시스템 변수 SliceStart, SliceEnd를 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-250">You can do so with the Data Factory macros and the system variable SliceStart, SliceEnd that indicate the logical time period for a given data slice.</span></span>

<span data-ttu-id="89612-251">시계열 데이터 집합, 예약 및 조각에 대한 자세한 내용은 [데이터 집합 만들기](data-factory-create-datasets.md), [일정 예약 및 실행](data-factory-scheduling-and-execution.md) 및 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-251">To learn about time series datasets, scheduling, and slices, See [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="89612-252">샘플 1:</span><span class="sxs-lookup"><span data-stu-id="89612-252">Sample 1:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="89612-253">이 예제에서 {Slice}는 지정된 형식(YYYYMMDDHH)의 Data Factory 시스템 변수 SliceStart 값으로 대체됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-253">In this example {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="89612-254">SliceStart는 조각의 시작 시간을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="89612-254">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="89612-255">folderPath는 각 조각에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="89612-255">The folderPath is different for each slice.</span></span> <span data-ttu-id="89612-256">예를 들어 wikidatagateway/wikisampledataout/2014100103 또는 wikidatagateway/wikisampledataout/2014100104입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-256">Example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="89612-257">샘플 2:</span><span class="sxs-lookup"><span data-stu-id="89612-257">Sample 2:</span></span>

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
<span data-ttu-id="89612-258">이 예제에서 SliceStart의 연도, 월, 일 및 시간은 folderPath 및 fileName 속성에서 사용하는 별도 변수로 추출됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-258">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="89612-259">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="89612-259">Copy activity properties</span></span>
<span data-ttu-id="89612-260">활동 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-260">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="89612-261">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-261">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="89612-262">반면 활동의 typeProperties 섹션에서 사용할 수 있는 속성은 각 활동 유형에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="89612-262">Whereas, the properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="89612-263">복사 활동의 경우 유형은 소스 및 싱크의 형식에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="89612-263">For Copy activity, the type properties vary depending on the types of sources and sinks.</span></span>

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="89612-264">지원되는 파일 및 압축 형식</span><span class="sxs-lookup"><span data-stu-id="89612-264">Supported file and compression formats</span></span>
<span data-ttu-id="89612-265">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-265">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-sftp-server-to-azure-blob"></a><span data-ttu-id="89612-266">JSON 예: SFTP 서버에서 Azure Blob으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="89612-266">JSON Example: Copy data from SFTP server to Azure blob</span></span>
<span data-ttu-id="89612-267">다음 예제에서는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)을 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-267">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="89612-268">SFTP 원본에서 Azure Blob Storage로 데이터를 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89612-268">They show how to copy data from SFTP source to Azure Blob Storage.</span></span> <span data-ttu-id="89612-269">그러나 Azure 데이터 팩터리의 복사 작업을 사용하여 임의의 원본에서 **여기**에 설명한 싱크로 [직접](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-269">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89612-270">이 샘플은 JSON 코드 조각을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-270">This sample provides JSON snippets.</span></span> <span data-ttu-id="89612-271">데이터 팩터리를 만들기 위한 단계별 지침은 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-271">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="89612-272">단계별 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-272">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="89612-273">이 샘플에는 다음 데이터 팩터리 엔터티가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-273">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="89612-274">[sftp](#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="89612-274">A linked service of type [sftp](#linked-service-properties).</span></span>
* <span data-ttu-id="89612-275">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="89612-275">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="89612-276">[FileShare](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="89612-276">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="89612-277">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="89612-277">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="89612-278">[FileSystemSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="89612-278">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="89612-279">샘플은 1시간마다 SFTP 서버의 데이터를 Azure Blob으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-279">The sample copies data from an SFTP server to an Azure blob every hour.</span></span> <span data-ttu-id="89612-280">이 샘플에 사용된 JSON 속성은 샘플 다음에 나오는 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-280">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="89612-281">**SFTP 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="89612-281">**SFTP linked service**</span></span>

<span data-ttu-id="89612-282">이 예에서는 일반 텍스트의 사용자 이름과 암호를 기본 인증으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-282">This example uses the basic authentication with user name and password in plain text.</span></span> <span data-ttu-id="89612-283">다음 방법 중 하나를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89612-283">You can also use one of the following ways:</span></span>

* <span data-ttu-id="89612-284">암호화된 자격 증명으로 기본 인증 </span><span class="sxs-lookup"><span data-stu-id="89612-284">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="89612-285">SSH 공개 키 인증</span><span class="sxs-lookup"><span data-stu-id="89612-285">SSH public key authentication</span></span>

<span data-ttu-id="89612-286">사용할 수 있는 다른 유형의 인증은 [FTP 연결 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-286">See [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
<span data-ttu-id="89612-287">**Azure 저장소 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="89612-287">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="89612-288">**SFTP 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="89612-288">**SFTP input dataset**</span></span>

<span data-ttu-id="89612-289">이 데이터 집합은 SFTP 폴더 `mysharedfolder`와 `test.csv` 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-289">This dataset refers to the SFTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="89612-290">파이프라인은 파일을 대상에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-290">The pipeline copies the file to the destination.</span></span>

<span data-ttu-id="89612-291">"external": "true" 설정은 데이터 집합이 Data Factory의 외부에 있으며 Data Factory의 활동에 의해 생성되지 않는다는 사실을 Data Factory 서비스에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-291">Setting "external": "true" informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="89612-292">**Azure Blob 출력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="89612-292">**Azure Blob output dataset**</span></span>

<span data-ttu-id="89612-293">데이터는 매시간 새 blob에 기록됩니다(frequency: hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="89612-293">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="89612-294">Blob에 대한 폴더 경로는 처리 중인 조각의 시작 시간에 기반하여 동적으로 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-294">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="89612-295">폴더 경로는 시작 시간에서 연도, 월, 일 및 시간 부분을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89612-295">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="89612-296">**복사 작업을 포함하는 파이프라인**</span><span class="sxs-lookup"><span data-stu-id="89612-296">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="89612-297">파이프라인은 입력 및 출력 데이터 집합을 사용하도록 구성된 복사 작업을 포함하고 매시간 실행하도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-297">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="89612-298">파이프라인 JSON 정의에서 **source** 형식은 **FileSystemSource**로 설정되고 **sink** 형식은 **BlobSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="89612-298">In the pipeline JSON definition, the **source** type is set to **FileSystemSource** and **sink** type is set to **BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
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
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a><span data-ttu-id="89612-299">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="89612-299">Performance and Tuning</span></span>
<span data-ttu-id="89612-300">Azure Data Factory의 데이터 이동(복사 작업) 성능에 영향을 주는 주요 요소 및 최적화하는 다양한 방법에 대해 알아보려면 [복사 작업 성능 및 조정 가이드](data-factory-copy-activity-performance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-300">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89612-301">다음 단계</span><span class="sxs-lookup"><span data-stu-id="89612-301">Next Steps</span></span>
<span data-ttu-id="89612-302">다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89612-302">See the following articles:</span></span>

* <span data-ttu-id="89612-303">[복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .</span><span class="sxs-lookup"><span data-stu-id="89612-303">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
