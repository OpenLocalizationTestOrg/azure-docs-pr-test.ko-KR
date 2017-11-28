---
title: "Azure 데이터 팩터리를 사용 하 여 SFTP 서버에서 데이터 aaaMove | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 온-프레미스 또는 Azure 데이터 팩터리를 사용 하 여 클라우드 SFTP 서버에서 toomove 데이터입니다."
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
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a><span data-ttu-id="eee62-103">Azure Data Factory를 사용하여 SFTP 서버에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="eee62-103">Move data from an SFTP server using Azure Data Factory</span></span>
<span data-ttu-id="eee62-104">이 문서에서는 toouse hello 복사 작업에서-프레미스/클라우드 SFTP 서버 tooa에서 Azure Data Factory toomove 데이터에서 싱크 데이터 저장소를 지원 되는 방식에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud SFTP server tooa supported sink data store.</span></span> <span data-ttu-id="eee62-105">Hello를 기반으로 한이 문서 [데이터 이동 작업](data-factory-data-movement-activities.md) 원본/싱크의로 지원 되는 데이터 저장소의 복사 작업 및 hello 목록 사용 하 여 데이터 이동의 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="eee62-106">데이터 팩터리의 현재만 지 원하는 SFTP 서버 tooother 데이터에서 데이터 저장소, 아니면 이동 tooan SFTP 서버 저장소를 다른 데이터와 데이터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-106">Data factory currently supports only moving data from an SFTP server tooother data stores, but not for moving data from other data stores tooan SFTP server.</span></span> <span data-ttu-id="eee62-107">온-프레미스 및 클라우드 SFTP 서버를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-107">It supports both on-premises and cloud SFTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="eee62-108">복사 작업으로 복사한 toohello 대상 않아 hello 소스 파일을 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-108">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="eee62-109">성공적인 복사 후 toodelete hello 소스 파일을 필요한 경우 사용자 지정 활동 toodelete hello 파일 만들고 hello 파이프라인에서 hello 활동을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-109">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="eee62-110">지원되는 시나리오 및 인증 형식</span><span class="sxs-lookup"><span data-stu-id="eee62-110">Supported scenarios and authentication types</span></span>
<span data-ttu-id="eee62-111">이 SFTP 커넥터 toocopy 데이터를 사용할 수 **SFTP 서버와 온-프레미스 SFTP 서버 클라우드 둘 다**합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-111">You can use this SFTP connector toocopy data from **both cloud SFTP servers and on-premises SFTP servers**.</span></span> <span data-ttu-id="eee62-112">**기본** 및 **SshPublicKey** toohello SFTP 서버에 연결 하는 경우에 인증 형식이 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-112">**Basic** and **SshPublicKey** authentication types are supported when connecting toohello SFTP server.</span></span>

<span data-ttu-id="eee62-113">온-프레미스 SFTP 서버에서 데이터를 복사할 때 hello 온-프레미스 환경/Azure VM에서에서 데이터 관리 게이트웨이 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-113">When copying data from an on-premises SFTP server, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="eee62-114">참조 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) hello 게이트웨이에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-114">See [Data Management Gateway](data-factory-data-management-gateway.md) for details on hello gateway.</span></span> <span data-ttu-id="eee62-115">참조 [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 대 한 단계별 지침은 hello 게이트웨이를 설정 하 고 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway and using it.</span></span>

## <a name="getting-started"></a><span data-ttu-id="eee62-116">시작</span><span class="sxs-lookup"><span data-stu-id="eee62-116">Getting started</span></span>
<span data-ttu-id="eee62-117">다른 도구/API를 사용하여 SFTP 원본의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-117">You can create a pipeline with a copy activity that moves data from an SFTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="eee62-118">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="eee62-119">참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="eee62-120">다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="eee62-121">참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="eee62-122">SFTP 서버 tooAzure Blob 저장소에서에서 toocopy 데이터를 샘플링 하는 JSON, 참조 [JSON의 예: SFTP 서버 tooAzure blob에서 데이터를 복사](#json-example-copy-data-from-sftp-server-to-azure-blob) 이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="eee62-122">For JSON samples toocopy data from SFTP server tooAzure Blob Storage, see [JSON Example: Copy data from SFTP server tooAzure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) section of this article.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="eee62-123">연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="eee62-123">Linked service properties</span></span>
<span data-ttu-id="eee62-124">다음 표에서 hello JSON 요소 특정 tooFTP 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-124">hello following table provides description for JSON elements specific tooFTP linked service.</span></span>

| <span data-ttu-id="eee62-125">속성</span><span class="sxs-lookup"><span data-stu-id="eee62-125">Property</span></span> | <span data-ttu-id="eee62-126">설명</span><span class="sxs-lookup"><span data-stu-id="eee62-126">Description</span></span> | <span data-ttu-id="eee62-127">필수</span><span class="sxs-lookup"><span data-stu-id="eee62-127">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eee62-128">type</span><span class="sxs-lookup"><span data-stu-id="eee62-128">type</span></span> | <span data-ttu-id="eee62-129">너무 hello 유형 속성을 설정 해야`Sftp`합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-129">hello type property must be set too`Sftp`.</span></span> |<span data-ttu-id="eee62-130">예</span><span class="sxs-lookup"><span data-stu-id="eee62-130">Yes</span></span> |
| <span data-ttu-id="eee62-131">host</span><span class="sxs-lookup"><span data-stu-id="eee62-131">host</span></span> | <span data-ttu-id="eee62-132">Hello SFTP 서버의 이름 또는 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-132">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="eee62-133">예</span><span class="sxs-lookup"><span data-stu-id="eee62-133">Yes</span></span> |
| <span data-ttu-id="eee62-134">포트</span><span class="sxs-lookup"><span data-stu-id="eee62-134">port</span></span> |<span data-ttu-id="eee62-135">어떤 hello SFTP 서버 수신 대기 중인 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-135">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="eee62-136">hello 기본값은: 21</span><span class="sxs-lookup"><span data-stu-id="eee62-136">hello default value is: 21</span></span> |<span data-ttu-id="eee62-137">아니요</span><span class="sxs-lookup"><span data-stu-id="eee62-137">No</span></span> |
| <span data-ttu-id="eee62-138">authenticationType</span><span class="sxs-lookup"><span data-stu-id="eee62-138">authenticationType</span></span> |<span data-ttu-id="eee62-139">인증 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-139">Specify authentication type.</span></span> <span data-ttu-id="eee62-140">허용되는 값은 **기본** 및 **SshPublicKey**입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-140">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="eee62-141">너무 참조[기본 인증을 사용 하 여](#using-basic-authentication) 및 [를 사용 하 여 SSH 공개 키 인증](#using-ssh-public-key-authentication) 더 많은 속성 및 JSON 샘플에서 각각 섹션.</span><span class="sxs-lookup"><span data-stu-id="eee62-141">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="eee62-142">예</span><span class="sxs-lookup"><span data-stu-id="eee62-142">Yes</span></span> |
| <span data-ttu-id="eee62-143">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="eee62-143">skipHostKeyValidation</span></span> | <span data-ttu-id="eee62-144">Tooskip 호스트 키 유효성 검사 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-144">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="eee62-145">아니요.</span><span class="sxs-lookup"><span data-stu-id="eee62-145">No.</span></span> <span data-ttu-id="eee62-146">hello 기본값: false</span><span class="sxs-lookup"><span data-stu-id="eee62-146">hello default value: false</span></span> |
| <span data-ttu-id="eee62-147">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="eee62-147">hostKeyFingerprint</span></span> | <span data-ttu-id="eee62-148">Hello 호스트 키의 지문 안녕하세요를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-148">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="eee62-149">예 경우 hello `skipHostKeyValidation` toofalse 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-149">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="eee62-150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="eee62-150">gatewayName</span></span> |<span data-ttu-id="eee62-151">데이터 관리 게이트웨이 tooconnect tooan hello의 이름 온-프레미스 SFTP 서버.</span><span class="sxs-lookup"><span data-stu-id="eee62-151">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="eee62-152">온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-152">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="eee62-153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="eee62-153">encryptedCredential</span></span> | <span data-ttu-id="eee62-154">암호화 된 자격 증명 tooaccess hello SFTP 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-154">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="eee62-155">자동 생성 된 복사 마법사 또는 hello ClickOnce 팝업 대화 상자에서 기본 인증 (사용자 이름 + 암호) 또는 SshPublicKey 인증 (사용자 이름 + 개인 키의 경로 또는 콘텐츠)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-155">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="eee62-156">아니요.</span><span class="sxs-lookup"><span data-stu-id="eee62-156">No.</span></span> <span data-ttu-id="eee62-157">온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-157">Apply only when copying data from an on-premises SFTP server.</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="eee62-158">기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="eee62-158">Using basic authentication</span></span>

<span data-ttu-id="eee62-159">toouse 기본 인증 설정 `authenticationType` 으로 `Basic`, hello SFTP 커넥터 hello 마지막 섹션에 도입 된 일반 자원을 hello 외에 다음과 같은 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-159">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="eee62-160">속성</span><span class="sxs-lookup"><span data-stu-id="eee62-160">Property</span></span> | <span data-ttu-id="eee62-161">설명</span><span class="sxs-lookup"><span data-stu-id="eee62-161">Description</span></span> | <span data-ttu-id="eee62-162">필수</span><span class="sxs-lookup"><span data-stu-id="eee62-162">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eee62-163">username</span><span class="sxs-lookup"><span data-stu-id="eee62-163">username</span></span> | <span data-ttu-id="eee62-164">사용자가 액세스 toohello SFTP 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-164">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="eee62-165">예</span><span class="sxs-lookup"><span data-stu-id="eee62-165">Yes</span></span> |
| <span data-ttu-id="eee62-166">암호</span><span class="sxs-lookup"><span data-stu-id="eee62-166">password</span></span> | <span data-ttu-id="eee62-167">Hello 사용자 (사용자 이름)에 대 한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-167">Password for hello user (username).</span></span> | <span data-ttu-id="eee62-168">예</span><span class="sxs-lookup"><span data-stu-id="eee62-168">Yes</span></span> |

#### <a name="example-basic-authentication"></a><span data-ttu-id="eee62-169">예: 기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="eee62-169">Example: Basic authentication</span></span>
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

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="eee62-170">예: 암호화된 자격 증명으로 기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="eee62-170">Example: Basic authentication with encrypted credential</span></span>

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

### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="eee62-171">SSH 공개 키 인증 사용</span><span class="sxs-lookup"><span data-stu-id="eee62-171">Using SSH public key authentication</span></span>

<span data-ttu-id="eee62-172">toouse SSH 공용 키 인증, 설정 `authenticationType` 으로 `SshPublicKey`, hello SFTP 커넥터 hello 마지막 섹션에 도입 된 일반 자원을 hello 외에 다음과 같은 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-172">toouse SSH public key authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="eee62-173">속성</span><span class="sxs-lookup"><span data-stu-id="eee62-173">Property</span></span> | <span data-ttu-id="eee62-174">설명</span><span class="sxs-lookup"><span data-stu-id="eee62-174">Description</span></span> | <span data-ttu-id="eee62-175">필수</span><span class="sxs-lookup"><span data-stu-id="eee62-175">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="eee62-176">username</span><span class="sxs-lookup"><span data-stu-id="eee62-176">username</span></span> |<span data-ttu-id="eee62-177">액세스 toohello SFTP 서버에 있는 사용자</span><span class="sxs-lookup"><span data-stu-id="eee62-177">User who has access toohello SFTP server</span></span> |<span data-ttu-id="eee62-178">예</span><span class="sxs-lookup"><span data-stu-id="eee62-178">Yes</span></span> |
| <span data-ttu-id="eee62-179">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="eee62-179">privateKeyPath</span></span> | <span data-ttu-id="eee62-180">절대 경로 toohello 지정 개인 키 파일 해당 게이트웨이에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-180">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="eee62-181">어느 hello 지정 `privateKeyPath` 또는 `privateKeyContent`합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-181">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="eee62-182">온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-182">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="eee62-183">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="eee62-183">privateKeyContent</span></span> | <span data-ttu-id="eee62-184">Hello 개인 키 콘텐츠는 serialize 된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-184">A serialized string of hello private key content.</span></span> <span data-ttu-id="eee62-185">hello 복사 마법사 hello 개인 키 파일 읽고 hello 개인 키 콘텐츠를 자동으로 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-185">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="eee62-186">모든 다른 도구/SDK를 사용 하는 경우 hello privateKeyPath 속성을 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-186">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="eee62-187">어느 hello 지정 `privateKeyPath` 또는 `privateKeyContent`합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-187">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="eee62-188">passPhrase</span><span class="sxs-lookup"><span data-stu-id="eee62-188">passPhrase</span></span> | <span data-ttu-id="eee62-189">암호 구문을 통해 hello 키 파일을 보호 하는 경우에 hello 전달 구를/암호 toodecrypt hello 개인 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-189">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="eee62-190">Yes 전달 구에 의해 hello 개인 키 파일 보호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-190">Yes if hello private key file is protected by a pass phrase.</span></span> |

> [!NOTE]
> <span data-ttu-id="eee62-191">SFTP 커넥터는 OpenSSH 키만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-191">SFTP connector only support OpenSSH key.</span></span> <span data-ttu-id="eee62-192">키 파일 hello 적절 한 형식에서 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-192">Make sure your key file is in hello proper format.</span></span> <span data-ttu-id="eee62-193">Putty 도구 tooconvert tooOpenSSH 형식.ppk에서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-193">You can use Putty tool tooconvert from .ppk tooOpenSSH format.</span></span>

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a><span data-ttu-id="eee62-194">예: 개인 키 파일 경로를 사용하여 SshPublicKey 인증</span><span class="sxs-lookup"><span data-stu-id="eee62-194">Example: SshPublicKey authentication using private key filePath</span></span>

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

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="eee62-195">예: 개인 키 콘텐츠를 사용하여 SshPublicKey 인증</span><span class="sxs-lookup"><span data-stu-id="eee62-195">Example: SshPublicKey authentication using private key content</span></span>

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
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="eee62-196">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="eee62-196">Dataset properties</span></span>
<span data-ttu-id="eee62-197">섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="eee62-197">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="eee62-198">구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-198">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="eee62-199">hello **typeProperties** 섹션은 데이터 집합의 각 형식 마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-199">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="eee62-200">가 특정 toohello 데이터 집합 형식 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-200">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="eee62-201">형식의 데이터 집합에 대 한 hello typeProperties 섹션 **FileShare** 데이터 집합에 다음과 같은 속성 hello:</span><span class="sxs-lookup"><span data-stu-id="eee62-201">hello typeProperties section for a dataset of type **FileShare** dataset has hello following properties:</span></span>

| <span data-ttu-id="eee62-202">속성</span><span class="sxs-lookup"><span data-stu-id="eee62-202">Property</span></span> | <span data-ttu-id="eee62-203">설명</span><span class="sxs-lookup"><span data-stu-id="eee62-203">Description</span></span> | <span data-ttu-id="eee62-204">필수</span><span class="sxs-lookup"><span data-stu-id="eee62-204">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eee62-205">folderPath</span><span class="sxs-lookup"><span data-stu-id="eee62-205">folderPath</span></span> |<span data-ttu-id="eee62-206">하위 경로 toohello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-206">Sub path toohello folder.</span></span> <span data-ttu-id="eee62-207">이스케이프 문자를 사용 하 여 ' \ ' hello 문자열의 특수 문자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-207">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="eee62-208">예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eee62-208">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="eee62-209">이 속성을 결합할 수 **partitionBy** toohave 폴더 경로 분할 영역에 따라 시작/종료 날짜와 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-209">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="eee62-210">예</span><span class="sxs-lookup"><span data-stu-id="eee62-210">Yes</span></span> |
| <span data-ttu-id="eee62-211">fileName</span><span class="sxs-lookup"><span data-stu-id="eee62-211">fileName</span></span> |<span data-ttu-id="eee62-212">Hello에 hello hello 파일 이름을 지정 **folderPath** hello 테이블 toorefer tooa 특정 파일 hello 폴더에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-212">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="eee62-213">이 속성에 대 한 모든 값을 지정 하지 않는 경우 hello 테이블 hello 폴더의 tooall 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-213">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="eee62-214">출력 데이터 집합에 대 한 파일 이름을 지정 하지 않으면,이 형식에 따라 hello에 hello 생성 된 파일의 hello 이름이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-214">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="eee62-215">Data.<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="eee62-215">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="eee62-216">아니요</span><span class="sxs-lookup"><span data-stu-id="eee62-216">No</span></span> |
| <span data-ttu-id="eee62-217">fileFilter</span><span class="sxs-lookup"><span data-stu-id="eee62-217">fileFilter</span></span> |<span data-ttu-id="eee62-218">필터 toobe tooselect 사용 되는 모든 파일이 아니라 hello folderPath에 있는 파일의 하위 집합을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-218">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="eee62-219">허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-219">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="eee62-220">예 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="eee62-220">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="eee62-221">예 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="eee62-221">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="eee62-222">fileFilter는 FileShare 입력 데이터 집합에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-222">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="eee62-223">이 속성은 HDFS에는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-223">This property is not supported with HDFS.</span></span> |<span data-ttu-id="eee62-224">아니요</span><span class="sxs-lookup"><span data-stu-id="eee62-224">No</span></span> |
| <span data-ttu-id="eee62-225">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="eee62-225">partitionedBy</span></span> |<span data-ttu-id="eee62-226">partitionedBy 사용된 toospecify 동적 folderPath 시계열 데이터에 대 한 파일 이름이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-226">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="eee62-227">예를 들어 매시간 데이터에 대한 매개 변수가 있는 folderPath입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-227">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="eee62-228">아니요</span><span class="sxs-lookup"><span data-stu-id="eee62-228">No</span></span> |
| <span data-ttu-id="eee62-229">format</span><span class="sxs-lookup"><span data-stu-id="eee62-229">format</span></span> | <span data-ttu-id="eee62-230">hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-230">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="eee62-231">집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-231">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="eee62-232">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eee62-232">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="eee62-233">너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오.</span><span class="sxs-lookup"><span data-stu-id="eee62-233">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="eee62-234">아니요</span><span class="sxs-lookup"><span data-stu-id="eee62-234">No</span></span> |
| <span data-ttu-id="eee62-235">압축</span><span class="sxs-lookup"><span data-stu-id="eee62-235">compression</span></span> | <span data-ttu-id="eee62-236">Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-236">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="eee62-237">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-237">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="eee62-238">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-238">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="eee62-239">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eee62-239">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="eee62-240">아니요</span><span class="sxs-lookup"><span data-stu-id="eee62-240">No</span></span> |
| <span data-ttu-id="eee62-241">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="eee62-241">useBinaryTransfer</span></span> |<span data-ttu-id="eee62-242">이전 전송 모드를 사용할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-242">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="eee62-243">이진 모드인 경우 true이고 ASCII인 경우 false입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-243">True for binary mode and false ASCII.</span></span> <span data-ttu-id="eee62-244">기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-244">Default value: True.</span></span> <span data-ttu-id="eee62-245">이 속성은 연결된 서비스 유형이 FtpServer인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-245">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="eee62-246">아니요</span><span class="sxs-lookup"><span data-stu-id="eee62-246">No</span></span> |

> [!NOTE]
> <span data-ttu-id="eee62-247">filename 및 fileFilter는 동시에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-247">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="eee62-248">partionedBy 속성 사용</span><span class="sxs-lookup"><span data-stu-id="eee62-248">Using partionedBy property</span></span>
<span data-ttu-id="eee62-249">Hello 이전 섹션에서 설명 했 듯이 동적 folderPath에 partitionedBy 된 시계열 데이터에 대 한 파일 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-249">As mentioned in hello previous section, you can specify a dynamic folderPath, filename for time series data with partitionedBy.</span></span> <span data-ttu-id="eee62-250">Hello Data Factory 매크로와 SliceEnd hello 지정 된 데이터 조각에 대 한 논리적 기간을 나타내는 hello 시스템 변수 SliceStart, 그렇게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-250">You can do so with hello Data Factory macros and hello system variable SliceStart, SliceEnd that indicate hello logical time period for a given data slice.</span></span>

<span data-ttu-id="eee62-251">toolearn 시간 시계열 데이터 집합, 일정 및 분할 하는 방법에 대 한 참조 [데이터 집합 만들기](data-factory-create-datasets.md), [일정 예약 및 실행](data-factory-scheduling-and-execution.md), 및 [파이프라인 만들기](data-factory-create-pipelines.md) 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-251">toolearn about time series datasets, scheduling, and slices, See [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="eee62-252">샘플 1:</span><span class="sxs-lookup"><span data-stu-id="eee62-252">Sample 1:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="eee62-253">이 예제에서 {Slice}는 지정 된 hello (yyyymmddhh)에서 데이터 팩터리 시스템 변수 SliceStart의 hello 값으로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-253">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="eee62-254">hello SliceStart hello 조각의 toostart 시간을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-254">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="eee62-255">hello folderPath 각 조각에 대 한 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-255">hello folderPath is different for each slice.</span></span> <span data-ttu-id="eee62-256">예를 들어 wikidatagateway/wikisampledataout/2014100103 또는 wikidatagateway/wikisampledataout/2014100104입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-256">Example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="eee62-257">샘플 2:</span><span class="sxs-lookup"><span data-stu-id="eee62-257">Sample 2:</span></span>

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
<span data-ttu-id="eee62-258">이 예제에서 SliceStart의 연도, 월, 일 및 시간은 folderPath 및 fileName 속성에서 사용하는 별도 변수로 추출됩니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-258">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="eee62-259">복사 작업 속성</span><span class="sxs-lookup"><span data-stu-id="eee62-259">Copy activity properties</span></span>
<span data-ttu-id="eee62-260">섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="eee62-260">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="eee62-261">이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-261">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="eee62-262">반면 hello hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-262">Whereas, hello properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="eee62-263">복사 작업에 대 한 hello 형식 속성의 원본 및 싱크 hello 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-263">For Copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="eee62-264">지원되는 파일 및 압축 형식</span><span class="sxs-lookup"><span data-stu-id="eee62-264">Supported file and compression formats</span></span>
<span data-ttu-id="eee62-265">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eee62-265">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a><span data-ttu-id="eee62-266">SFTP 서버 tooAzure blob에서 데이터를 복사 하는 JSON의 예:</span><span class="sxs-lookup"><span data-stu-id="eee62-266">JSON Example: Copy data from SFTP server tooAzure blob</span></span>
<span data-ttu-id="eee62-267">hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-267">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="eee62-268">SFTP에서 toocopy 데이터 tooAzure Blob 저장소를 원본 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-268">They show how toocopy data from SFTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="eee62-269">그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 소스 tooany 중 어디에서 든 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-269">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eee62-270">이 샘플은 JSON 코드 조각을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-270">This sample provides JSON snippets.</span></span> <span data-ttu-id="eee62-271">Hello 데이터 팩터리를 만들기 위한 단계별 지침을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-271">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="eee62-272">단계별 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eee62-272">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="eee62-273">hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-273">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="eee62-274">[sftp](#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="eee62-274">A linked service of type [sftp](#linked-service-properties).</span></span>
* <span data-ttu-id="eee62-275">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="eee62-275">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="eee62-276">[FileShare](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="eee62-276">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="eee62-277">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="eee62-277">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="eee62-278">[FileSystemSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-278">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="eee62-279">hello 샘플 데이터 복사 SFTP 서버 tooan Azure blob에서에서 1 시간 마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-279">hello sample copies data from an SFTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="eee62-280">이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-280">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="eee62-281">**SFTP 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="eee62-281">**SFTP linked service**</span></span>

<span data-ttu-id="eee62-282">이 예제에서는 사용자 이름과 암호가 일반 텍스트로 hello 기본 인증을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-282">This example uses hello basic authentication with user name and password in plain text.</span></span> <span data-ttu-id="eee62-283">또한 hello 같은 방법으로 다음 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-283">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="eee62-284">암호화된 자격 증명으로 기본 인증 </span><span class="sxs-lookup"><span data-stu-id="eee62-284">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="eee62-285">SSH 공개 키 인증</span><span class="sxs-lookup"><span data-stu-id="eee62-285">SSH public key authentication</span></span>

<span data-ttu-id="eee62-286">사용할 수 있는 다른 유형의 인증은 [FTP 연결 서비스](#linked-service-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eee62-286">See [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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
<span data-ttu-id="eee62-287">**Azure 저장소 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="eee62-287">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="eee62-288">**SFTP 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="eee62-288">**SFTP input dataset**</span></span>

<span data-ttu-id="eee62-289">이 데이터 집합 참조 toohello SFTP 폴더 `mysharedfolder` 파일과 `test.csv`합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-289">This dataset refers toohello SFTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="eee62-290">hello 파이프라인 hello 파일 toohello 대상에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-290">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="eee62-291">설정 "외부": "true" 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-291">Setting "external": "true" informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="eee62-292">**Azure Blob 출력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="eee62-292">**Azure Blob output dataset**</span></span>

<span data-ttu-id="eee62-293">데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="eee62-293">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="eee62-294">hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-294">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="eee62-295">hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-295">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="eee62-296">**복사 작업을 포함하는 파이프라인**</span><span class="sxs-lookup"><span data-stu-id="eee62-296">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="eee62-297">hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-297">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="eee62-298">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**FileSystemSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-298">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span>

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

## <a name="performance-and-tuning"></a><span data-ttu-id="eee62-299">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="eee62-299">Performance and Tuning</span></span>
<span data-ttu-id="eee62-300">참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eee62-300">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eee62-301">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eee62-301">Next Steps</span></span>
<span data-ttu-id="eee62-302">Hello 다음 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="eee62-302">See hello following articles:</span></span>

* <span data-ttu-id="eee62-303">[복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .</span><span class="sxs-lookup"><span data-stu-id="eee62-303">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
