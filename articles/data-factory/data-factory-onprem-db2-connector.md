---
title: "Azure 데이터 팩터리를 사용 하 여 d b 2에서 aaaMove 데이터 | Microsoft Docs"
description: "Azure 데이터 팩터리 복사 작업을 사용 하 여 toomove 데이터를 온-프레미스 DB2 데이터베이스 하는 방법에 대해 알아봅니다"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="b4c12-103">Azure Data Factory 복사 활동을 사용하여 DB2에서 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="b4c12-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="b4c12-104">이 문서에서는 온-프레미스 DB2 데이터베이스 tooa 데이터 저장소에서 Azure Data Factory toocopy 데이터에서 복사 작업을 사용 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-104">This article describes how you can use Copy Activity in Azure Data Factory toocopy data from an on-premises DB2 database tooa data store.</span></span> <span data-ttu-id="b4c12-105">Hello에 지원 되는 싱크로 나열 되어 있는 데이터 tooany 저장소를 복사할 수는 있지만 [Data Factory 데이터 이동 작업](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 문서.</span><span class="sxs-lookup"><span data-stu-id="b4c12-105">You can copy data tooany store that is listed as a supported sink in hello [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="b4c12-106">이 항목 복사 작업을 사용 하 여 데이터 이동의 개요를 제공 하 고 hello 지원 데이터 저장소 조합을 나열 하는 hello Data Factory 문서 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-106">This topic builds on hello Data Factory article, which presents an overview of data movement by using Copy Activity and lists hello supported data store combinations.</span></span> 

<span data-ttu-id="b4c12-107">Data Factory에는 현재 DB2 데이터베이스 tooa 동안의 데이터만 이동 지원 [싱크를 지원 되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-107">Data Factory currently supports only moving data from a DB2 database tooa [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="b4c12-108">다른 데이터에서 데이터를 이동 저장 tooa DB2 데이터베이스에 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-108">Moving data from other data stores tooa DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4c12-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b4c12-109">Prerequisites</span></span>
<span data-ttu-id="b4c12-110">데이터 팩터리 hello를 사용 하 여 연결 tooan 온-프레미스 DB2 데이터베이스를 지원 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-110">Data Factory supports connecting tooan on-premises DB2 database by using hello [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="b4c12-111">단계별 지침은 tooset hello 게이트웨이 데이터를 데이터 toomove 파이프라인을 참조 하십시오 hello [toocloud 온-프레미스에서에서 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="b4c12-111">For step-by-step instructions tooset up hello gateway data pipeline toomove your data, see hello [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="b4c12-112">게이트웨이 hello d b 2에서 호스팅되는 Azure IaaS VM 하는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-112">A gateway is required even if hello DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="b4c12-113">Hello에 hello 게이트웨이 설치할 수 있습니다 hello 데이터 저장소로 동일한 IaaS VM입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-113">You can install hello gateway on hello same IaaS VM as hello data store.</span></span> <span data-ttu-id="b4c12-114">Hello 게이트웨이 toohello 데이터베이스를 연결할 수 경우 다른 VM에 hello 게이트웨이 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-114">If hello gateway can connect toohello database, you can install hello gateway on a different VM.</span></span>

<span data-ttu-id="b4c12-115">하지 않으면 하므로 필요 toomanually 설치 드라이버 toocopy 데이터 d b 2에서, hello 데이터 관리 게이트웨이 기본 제공 DB2 드라이버를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-115">hello data management gateway provides a built-in DB2 driver, so you don't need toomanually install a driver toocopy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="b4c12-116">연결 및 게이트웨이 문제를 해결 하는 정보에 대 한 참조 hello [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 문서.</span><span class="sxs-lookup"><span data-stu-id="b4c12-116">For tips on troubleshooting connection and gateway issues, see hello [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="b4c12-117">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="b4c12-117">Supported versions</span></span>
<span data-ttu-id="b4c12-118">데이터 팩터리 DB2 hello 커넥터 IBM DB2 플랫폼 및 버전 9, 10 및 11 DRDA 분산 관계형 데이터베이스 아키텍처 () SQL 액세스 관리자 버전에 따라 hello를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-118">hello Data Factory DB2 connector supports hello following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="b4c12-119">z/OS용 IBM DB2 버전 11.1</span><span class="sxs-lookup"><span data-stu-id="b4c12-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="b4c12-120">z/OS용 IBM DB2 버전 10.1</span><span class="sxs-lookup"><span data-stu-id="b4c12-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="b4c12-121">i(AS400)용 IBM DB2 버전 7.2</span><span class="sxs-lookup"><span data-stu-id="b4c12-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="b4c12-122">i(AS400)용 IBM DB2 버전 7.1</span><span class="sxs-lookup"><span data-stu-id="b4c12-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="b4c12-123">LUW(Linux, UNIX, and Windows)용 IBM DB2 버전 11</span><span class="sxs-lookup"><span data-stu-id="b4c12-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="b4c12-124">LUW용 IBM DB2 버전 10.5</span><span class="sxs-lookup"><span data-stu-id="b4c12-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="b4c12-125">LUW용 IBM DB2 버전 10.1</span><span class="sxs-lookup"><span data-stu-id="b4c12-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="b4c12-126">"Hello 패키지 해당 tooan SQL 문 실행 요청을 찾을 수 없습니다 hello 오류 메시지가 표시 되 면.</span><span class="sxs-lookup"><span data-stu-id="b4c12-126">If you receive hello error message "hello package corresponding tooan SQL statement execution request was not found.</span></span> <span data-ttu-id="b4c12-127">SQLSTATE 805-51002 SQLCODE =, = "hello 이유는 hello 일반 사용자 hello 운영 체제에 대 한 필수 패키지 만들어지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-127">SQLSTATE=51002 SQLCODE=-805," hello reason is a necessary package is not created for hello normal user on hello OS.</span></span> <span data-ttu-id="b4c12-128">tooresolve이 문제를 DB2 서버 유형에 대 한 다음이 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-128">tooresolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="b4c12-129">용 DB2 (AS400) i: 전원 사용자 hello 일반 사용자에 대 한 복사 작업을 실행 하기 전에 hello 컬렉션을 만들 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-129">DB2 for i (AS400): Let a power user create hello collection for hello normal user before running Copy Activity.</span></span> <span data-ttu-id="b4c12-130">명령 사용 하 여 hello toocreate hello 컬렉션:`create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="b4c12-130">toocreate hello collection, use hello command: `create collection <username>`</span></span>
> - <span data-ttu-id="b4c12-131">Z/OS 또는 LUW 용 d b 2: 권한이 높은 계정-고급 사용자 또는 관리자가 패키지 기관과 BINDADD, 바인딩, 사용 권한을 EXECUTE tooPUBLIC-toorun hello를 한 번만 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE tooPUBLIC permissions--toorun hello copy once.</span></span> <span data-ttu-id="b4c12-132">필수 패키지 hello hello 복사 중 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-132">hello necessary package is automatically created during hello copy.</span></span> <span data-ttu-id="b4c12-133">나중에 후속 복사 실행에 대 한 백 toohello 일반 사용자를 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-133">Afterward, you can switch back toohello normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b4c12-134">시작</span><span class="sxs-lookup"><span data-stu-id="b4c12-134">Getting started</span></span>
<span data-ttu-id="b4c12-135">온-프레미스 DB2 데이터 저장소에서 복사 활동 toomove 데이터와 함께 다른 도구와 Api를 사용 하 여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-135">You can create a pipeline with a copy activity toomove data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="b4c12-136">hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello Azure 데이터 팩터리 복사 마법사입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-136">hello easiest way toocreate a pipeline is toouse hello Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="b4c12-137">Hello 복사 마법사를 사용 하 여 파이프라인을 만드는 방법에 간략 한 설명이, 참조 hello [자습서: hello 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-137">For a quick walkthrough on creating a pipeline by using hello Copy Wizard, see hello [Tutorial: Create a pipeline by using hello Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="b4c12-138">도구 toocreate hello Azure 포털, Visual Studio, Azure PowerShell는 Azure 리소스 관리자 템플릿, hello.NET API 및 hello를 포함 하 여 파이프라인을 사용할 수도 있습니다 REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-138">You can also use tools toocreate a pipeline, including hello Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, hello .NET API, and hello REST API.</span></span> <span data-ttu-id="b4c12-139">단계별 지침은 toocreate 복사 작업으로 파이프라인에 대 한 참조 hello [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-139">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="b4c12-140">Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-140">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="b4c12-141">연결 된 서비스 toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-141">Create linked services toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="b4c12-142">Toorepresent 입력 데이터 집합을 만들고 hello 복사 작업에 대 한 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-142">Create datasets toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="b4c12-143">입력과 출력으로 각각의 데이터 집합을 사용하는 복사 활동이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="b4c12-144">Hello hello Data Factory 연결 서비스에 대 한 JSON 정의 복사 마법사를 사용 하는 경우 데이터 집합 및 파이프라인 엔터티는 자동으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-144">When you use hello Copy Wizard, JSON definitions for hello Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="b4c12-145">도구 또는 Api를 사용 하 여 hello.NET API) (제외 hello JSON 형식을 사용 하 여 hello Data Factory 엔터티를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-145">When you use tools or APIs (except hello .NET API), you define hello Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="b4c12-146">hello [JSON의 예: DB2 tooAzure Blob 저장소에서에서 데이터를 복사](#json-example-copy-data-from-db2-to-azure-blob) 온-프레미스 DB2 데이터 저장소에서 사용 되는 toocopy 데이터 엔터티를 Data Factory hello에 대 한 hello JSON 정의 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-146">hello [JSON example: Copy data from DB2 tooAzure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows hello JSON definitions for hello Data Factory entities that are used toocopy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="b4c12-147">다음 섹션 hello JSON 속성을 사용 하는 toodefine hello Data Factory 된 엔터티를 특정 tooa DB2 데이터 저장소 hello에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-147">hello following sections provide details about hello JSON properties that are used toodefine hello Data Factory entities that are specific tooa DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="b4c12-148">DB2 연결된 서비스 속성</span><span class="sxs-lookup"><span data-stu-id="b4c12-148">DB2 linked service properties</span></span>
<span data-ttu-id="b4c12-149">다음 표에서 hello 특정 tooa DB2 연결 서비스는 hello JSON 속성을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-149">hello following table lists hello JSON properties that are specific tooa DB2 linked service.</span></span>

| <span data-ttu-id="b4c12-150">속성</span><span class="sxs-lookup"><span data-stu-id="b4c12-150">Property</span></span> | <span data-ttu-id="b4c12-151">설명</span><span class="sxs-lookup"><span data-stu-id="b4c12-151">Description</span></span> | <span data-ttu-id="b4c12-152">필수</span><span class="sxs-lookup"><span data-stu-id="b4c12-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4c12-153">**type**</span><span class="sxs-lookup"><span data-stu-id="b4c12-153">**type**</span></span> |<span data-ttu-id="b4c12-154">이 속성을 너무 설정 해야**OnPremisesDB2**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-154">This property must be set too**OnPremisesDB2**.</span></span> |<span data-ttu-id="b4c12-155">예</span><span class="sxs-lookup"><span data-stu-id="b4c12-155">Yes</span></span> |
| <span data-ttu-id="b4c12-156">**server**</span><span class="sxs-lookup"><span data-stu-id="b4c12-156">**server**</span></span> |<span data-ttu-id="b4c12-157">hello DB2 서버 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-157">hello name of hello DB2 server.</span></span> |<span data-ttu-id="b4c12-158">예</span><span class="sxs-lookup"><span data-stu-id="b4c12-158">Yes</span></span> |
| <span data-ttu-id="b4c12-159">**database**</span><span class="sxs-lookup"><span data-stu-id="b4c12-159">**database**</span></span> |<span data-ttu-id="b4c12-160">hello DB2 데이터베이스의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-160">hello name of hello DB2 database.</span></span> |<span data-ttu-id="b4c12-161">예</span><span class="sxs-lookup"><span data-stu-id="b4c12-161">Yes</span></span> |
| <span data-ttu-id="b4c12-162">**schema**</span><span class="sxs-lookup"><span data-stu-id="b4c12-162">**schema**</span></span> |<span data-ttu-id="b4c12-163">hello DB2 데이터베이스에 대 한 hello 스키마의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-163">hello name of hello schema in hello DB2 database.</span></span> <span data-ttu-id="b4c12-164">대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-164">This property is case-sensitive.</span></span> |<span data-ttu-id="b4c12-165">아니요</span><span class="sxs-lookup"><span data-stu-id="b4c12-165">No</span></span> |
| <span data-ttu-id="b4c12-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="b4c12-166">**authenticationType**</span></span> |<span data-ttu-id="b4c12-167">인증 시 사용 되는 tooconnect toohello DB2 데이터베이스의 hello 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-167">hello type of authentication that is used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="b4c12-168">hello 가능한 값은: 익명, 기본 및 Windows.</span><span class="sxs-lookup"><span data-stu-id="b4c12-168">hello possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="b4c12-169">예</span><span class="sxs-lookup"><span data-stu-id="b4c12-169">Yes</span></span> |
| <span data-ttu-id="b4c12-170">**사용자 이름**</span><span class="sxs-lookup"><span data-stu-id="b4c12-170">**username**</span></span> |<span data-ttu-id="b4c12-171">기본 인증 또는 Windows 인증을 사용 하는 경우 hello 사용자 계정에 대 한 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-171">hello name for hello user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="b4c12-172">아니요</span><span class="sxs-lookup"><span data-stu-id="b4c12-172">No</span></span> |
| <span data-ttu-id="b4c12-173">**암호**</span><span class="sxs-lookup"><span data-stu-id="b4c12-173">**password**</span></span> |<span data-ttu-id="b4c12-174">hello hello 사용자 계정의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-174">hello password for hello user account.</span></span> |<span data-ttu-id="b4c12-175">아니요</span><span class="sxs-lookup"><span data-stu-id="b4c12-175">No</span></span> |
| <span data-ttu-id="b4c12-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="b4c12-176">**gatewayName**</span></span> |<span data-ttu-id="b4c12-177">데이터 팩터리 서비스 hello hello 게이트웨이의 hello 이름 tooconnect toohello 온-프레미스 DB2 데이터베이스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-177">hello name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="b4c12-178">예</span><span class="sxs-lookup"><span data-stu-id="b4c12-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="b4c12-179">데이터 집합 속성</span><span class="sxs-lookup"><span data-stu-id="b4c12-179">Dataset properties</span></span>
<span data-ttu-id="b4c12-180">Hello 섹션 및 데이터 집합 정의에 사용할 수 있는 속성 목록에 대 한 참조 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="b4c12-180">For a list of hello sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b4c12-181">와 같은 섹션 **구조**, **가용성**, 및 hello **정책** JSON는 데이터 집합에 대 한 권장 사항과 비슷합니다 (Azure SQL, Azure Blob 저장소, Azure 테이블에 모든 데이터 집합 형식에 대 한 저장소 및 등)입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-181">Sections, such as **structure**, **availability**, and hello **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="b4c12-182">hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-182">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="b4c12-183">hello **typeProperties** 형식의 데이터 집합에 대 한 섹션 **RelationalTable**, hello DB2 데이터 집합에 포함 되어 있는, hello 속성 뒤에:</span><span class="sxs-lookup"><span data-stu-id="b4c12-183">hello **typeProperties** section for a dataset of type **RelationalTable**, which includes hello DB2 dataset, has hello following property:</span></span>

| <span data-ttu-id="b4c12-184">속성</span><span class="sxs-lookup"><span data-stu-id="b4c12-184">Property</span></span> | <span data-ttu-id="b4c12-185">설명</span><span class="sxs-lookup"><span data-stu-id="b4c12-185">Description</span></span> | <span data-ttu-id="b4c12-186">필수</span><span class="sxs-lookup"><span data-stu-id="b4c12-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4c12-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="b4c12-187">**tableName**</span></span> |<span data-ttu-id="b4c12-188">hello 연결 된 서비스는 hello DB2 데이터베이스 인스턴스의 hello 테이블의 hello 이름을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-188">hello name of hello table in hello DB2 database instance that hello linked service refers to.</span></span> <span data-ttu-id="b4c12-189">대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-189">This property is case-sensitive.</span></span> |<span data-ttu-id="b4c12-190">더 (경우 hello **쿼리** 형식의 복사 작업의 속성 **RelationalSource** 지정)</span><span class="sxs-lookup"><span data-stu-id="b4c12-190">No (if hello **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="b4c12-191">복사 활동 속성</span><span class="sxs-lookup"><span data-stu-id="b4c12-191">Copy Activity properties</span></span>
<span data-ttu-id="b4c12-192">Hello 섹션 및 복사 활동 정의에 사용할 수 있는 속성 목록에 대 한 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="b4c12-192">For a list of hello sections and properties that are available for defining copy activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b4c12-193">**name**, **description**, **inputs** 테이블, **outputs** 테이블 및 **policy**와 같은 복사 활동 속성은 모든 유형의 활동에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="b4c12-194">hello에서 사용할 수 있는 속성 hello **typeProperties** 각 활동 유형에 대 한 hello 활동의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-194">hello properties that are available in hello **typeProperties** section of hello activity for each activity type.</span></span> <span data-ttu-id="b4c12-195">복사 작업에 대 한 hello 속성의 데이터 원본 및 싱크 hello 유형에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-195">For Copy Activity, hello properties vary depending on hello types of data sources and sinks.</span></span>

<span data-ttu-id="b4c12-196">Hello 원본 유형인 경우 복사 작업에 대 한 **RelationalSource** (DB2 포함), 다음과 같은 속성 hello hello에서 사용할 수 있는 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="b4c12-196">For Copy Activity, when hello source is of type **RelationalSource** (which includes DB2), hello following properties are available in hello **typeProperties** section:</span></span>

| <span data-ttu-id="b4c12-197">속성</span><span class="sxs-lookup"><span data-stu-id="b4c12-197">Property</span></span> | <span data-ttu-id="b4c12-198">설명</span><span class="sxs-lookup"><span data-stu-id="b4c12-198">Description</span></span> | <span data-ttu-id="b4c12-199">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="b4c12-199">Allowed values</span></span> | <span data-ttu-id="b4c12-200">필수</span><span class="sxs-lookup"><span data-stu-id="b4c12-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b4c12-201">**query**</span><span class="sxs-lookup"><span data-stu-id="b4c12-201">**query**</span></span> |<span data-ttu-id="b4c12-202">Hello tooread hello 데이터 사용자 지정 쿼리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-202">Use hello custom query tooread hello data.</span></span> |<span data-ttu-id="b4c12-203">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="b4c12-203">SQL query string.</span></span> <span data-ttu-id="b4c12-204">예: `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="b4c12-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="b4c12-205">더 (경우 hello **tableName** 속성이 데이터 집합의 지정 된)</span><span class="sxs-lookup"><span data-stu-id="b4c12-205">No (if hello **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="b4c12-206">스키마 및 테이블 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="b4c12-207">Hello 쿼리문을에서 속성 이름을 사용 하 여 묶습니다 "" (큰따옴표).</span><span class="sxs-lookup"><span data-stu-id="b4c12-207">In hello query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="b4c12-208">예:</span><span class="sxs-lookup"><span data-stu-id="b4c12-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a><span data-ttu-id="b4c12-209">JSON의 예: DB2 tooAzure Blob 저장소에서에서 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="b4c12-209">JSON example: Copy data from DB2 tooAzure Blob storage</span></span>
<span data-ttu-id="b4c12-210">이 예제에서는 샘플 JSON 정의 제공 hello를 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-210">This example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b4c12-211">hello 예제 toocopy 데이터는 d b 2에서 데이터베이스 tooBlob 저장소 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-211">hello example shows you how toocopy data from a DB2 database tooBlob storage.</span></span> <span data-ttu-id="b4c12-212">하지만 데이터를 너무 복사할 수 있습니다[모든 지원 되는 데이터 저장 싱크 유형이](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure 데이터 팩터리 복사 작업을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-212">However, data can be copied too[any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="b4c12-213">hello 샘플 Data Factory 엔터티에 따라 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-213">hello sample has hello following Data Factory entities:</span></span>

- <span data-ttu-id="b4c12-214">[OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties) 형식의 DB2 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="b4c12-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="b4c12-215">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 Azure Blob 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="b4c12-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="b4c12-216">[RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="b4c12-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="b4c12-217">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="b4c12-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="b4c12-218">A [파이프라인](data-factory-create-pipelines.md) hello를 사용 하 여 복사 활동으로 [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 속성</span><span class="sxs-lookup"><span data-stu-id="b4c12-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="b4c12-219">hello 샘플에 1 시간 마다 DB2 데이터베이스 tooan Azure blob에서에서 쿼리 결과에서 데이터 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-219">hello sample copies data from a query result in a DB2 database tooan Azure blob hourly.</span></span> <span data-ttu-id="b4c12-220">hello 샘플에 사용 되는 hello JSON 속성 hello 엔터티 정의 다음에 나오는 hello 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-220">hello JSON properties that are used in hello sample are described in hello sections that follow hello entity definitions.</span></span>

<span data-ttu-id="b4c12-221">첫 번째 단계로 데이터 관리 게이트웨이를 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="b4c12-222">지침은 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="b4c12-222">Instructions are in hello [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="b4c12-223">**DB2 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="b4c12-223">**DB2 linked service**</span></span>

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="b4c12-224">**Azure Blob 저장소 연결된 서비스**</span><span class="sxs-lookup"><span data-stu-id="b4c12-224">**Azure Blob storage linked service**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="b4c12-225">**DB2 입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="b4c12-225">**DB2 input dataset**</span></span>

<span data-ttu-id="b4c12-226">hello 샘플 hello 시계열 데이터에 대 한 "timestamp" 레이블이 지정 된 열이 있는 "MyTable" 이라는 DB2 테이블 만들었다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-226">hello sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for hello time series data.</span></span>

<span data-ttu-id="b4c12-227">hello **외부** 속성 너무 "true로 설정 되어 있습니다."</span><span class="sxs-lookup"><span data-stu-id="b4c12-227">hello **external** property is set too"true."</span></span> <span data-ttu-id="b4c12-228">이 설정은이 데이터 집합 데이터 팩터리 외부 toohello 이며 hello data factory에는 활동에 의해 생성 되지 않을 hello 데이터 팩터리 서비스에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-228">This setting informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="b4c12-229">해당 hello 확인 **형식** 너무 속성이**RelationalTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-229">Notice that hello **type** property is set too**RelationalTable**.</span></span>


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="b4c12-230">**Azure Blob 출력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="b4c12-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="b4c12-231">데이터에서 작성 되었습니다. 새 blob tooa 1 시간 마다 hello 설정 **주파수** 속성 너무 "시간" 및 hello **간격** 속성 too1 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-231">Data is written tooa new blob every hour by setting hello **frequency** property too"Hour" and hello **interval** property too1.</span></span> <span data-ttu-id="b4c12-232">hello **folderPath** 처리 중인 hello 조각의 hello 시작 시간에 따라 hello blob 동적으로 평가 대 한 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-232">hello **folderPath** property for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="b4c12-233">hello 폴더 경로 hello 시작 시간의 hello 연도, 월, 일 및 시간 부분을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-233">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="b4c12-234">**Hello 복사 작업에 대 한 파이프라인**</span><span class="sxs-lookup"><span data-stu-id="b4c12-234">**Pipeline for hello copy activity**</span></span>

<span data-ttu-id="b4c12-235">구성 된 복사 작업을 포함 하는 hello 파이프라인 toouse 입력 및 출력 데이터 집합을 지정 하 고 예약 된 toorun를 1 시간 마다가입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-235">hello pipeline contains a copy activity that is configured toouse specified input and output datasets and which is scheduled toorun every hour.</span></span> <span data-ttu-id="b4c12-236">Hello hello 파이프라인에 대 한 JSON 정의에서 hello **소스** 형식이 너무 설정**RelationalSource** 및 hello **싱크** 형식이 너무 설정**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="b4c12-236">In hello JSON definition for hello pipeline, hello **source** type is set too**RelationalSource** and hello **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="b4c12-237">hello에 대 한 지정 된 hello SQL 쿼리 **쿼리** 속성 hello "Orders" 테이블에서 hello 데이터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-237">hello SQL query specified for hello **query** property selects hello data from hello "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a><span data-ttu-id="b4c12-238">DB2에 대한 형식 매핑</span><span class="sxs-lookup"><span data-stu-id="b4c12-238">Type mapping for DB2</span></span>
<span data-ttu-id="b4c12-239">Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서, 복사 작업 2 단계 방식을 따릅니다 hello를 사용 하 여 소스 형식 toosink 형식을 자동 형식 변환을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-239">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type toosink type by using hello following two-step approach:</span></span>

1. <span data-ttu-id="b4c12-240">가 네이티브 소스 형식 tooa.NET 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="b4c12-240">Convert from a native source type tooa .NET type</span></span>
2. <span data-ttu-id="b4c12-241">.NET 형식 tooa 네이티브 싱크 형식에서 변환</span><span class="sxs-lookup"><span data-stu-id="b4c12-241">Convert from a .NET type tooa native sink type</span></span>

<span data-ttu-id="b4c12-242">hello 다음 매핑은 사용 하는 복사 작업 DB2 형식 tooa.NET 유형에 서 hello 데이터를 변환 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="b4c12-242">hello following mappings are used when Copy Activity converts hello data from a DB2 type tooa .NET type:</span></span>

| <span data-ttu-id="b4c12-243">DB2 데이터베이스 형식</span><span class="sxs-lookup"><span data-stu-id="b4c12-243">DB2 database type</span></span> | <span data-ttu-id="b4c12-244">.NET Framework 형식</span><span class="sxs-lookup"><span data-stu-id="b4c12-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="b4c12-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="b4c12-245">SmallInt</span></span> |<span data-ttu-id="b4c12-246">Int16</span><span class="sxs-lookup"><span data-stu-id="b4c12-246">Int16</span></span> |
| <span data-ttu-id="b4c12-247">Integer</span><span class="sxs-lookup"><span data-stu-id="b4c12-247">Integer</span></span> |<span data-ttu-id="b4c12-248">Int32</span><span class="sxs-lookup"><span data-stu-id="b4c12-248">Int32</span></span> |
| <span data-ttu-id="b4c12-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="b4c12-249">BigInt</span></span> |<span data-ttu-id="b4c12-250">Int64</span><span class="sxs-lookup"><span data-stu-id="b4c12-250">Int64</span></span> |
| <span data-ttu-id="b4c12-251">Real</span><span class="sxs-lookup"><span data-stu-id="b4c12-251">Real</span></span> |<span data-ttu-id="b4c12-252">단일</span><span class="sxs-lookup"><span data-stu-id="b4c12-252">Single</span></span> |
| <span data-ttu-id="b4c12-253">Double</span><span class="sxs-lookup"><span data-stu-id="b4c12-253">Double</span></span> |<span data-ttu-id="b4c12-254">Double</span><span class="sxs-lookup"><span data-stu-id="b4c12-254">Double</span></span> |
| <span data-ttu-id="b4c12-255">Float</span><span class="sxs-lookup"><span data-stu-id="b4c12-255">Float</span></span> |<span data-ttu-id="b4c12-256">Double</span><span class="sxs-lookup"><span data-stu-id="b4c12-256">Double</span></span> |
| <span data-ttu-id="b4c12-257">10진수</span><span class="sxs-lookup"><span data-stu-id="b4c12-257">Decimal</span></span> |<span data-ttu-id="b4c12-258">10진수</span><span class="sxs-lookup"><span data-stu-id="b4c12-258">Decimal</span></span> |
| <span data-ttu-id="b4c12-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="b4c12-259">DecimalFloat</span></span> |<span data-ttu-id="b4c12-260">10진수</span><span class="sxs-lookup"><span data-stu-id="b4c12-260">Decimal</span></span> |
| <span data-ttu-id="b4c12-261">숫자</span><span class="sxs-lookup"><span data-stu-id="b4c12-261">Numeric</span></span> |<span data-ttu-id="b4c12-262">10진수</span><span class="sxs-lookup"><span data-stu-id="b4c12-262">Decimal</span></span> |
| <span data-ttu-id="b4c12-263">Date</span><span class="sxs-lookup"><span data-stu-id="b4c12-263">Date</span></span> |<span data-ttu-id="b4c12-264">DateTime</span><span class="sxs-lookup"><span data-stu-id="b4c12-264">DateTime</span></span> |
| <span data-ttu-id="b4c12-265">Time</span><span class="sxs-lookup"><span data-stu-id="b4c12-265">Time</span></span> |<span data-ttu-id="b4c12-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b4c12-266">TimeSpan</span></span> |
| <span data-ttu-id="b4c12-267">Timestamp</span><span class="sxs-lookup"><span data-stu-id="b4c12-267">Timestamp</span></span> |<span data-ttu-id="b4c12-268">Datetime</span><span class="sxs-lookup"><span data-stu-id="b4c12-268">DateTime</span></span> |
| <span data-ttu-id="b4c12-269">xml</span><span class="sxs-lookup"><span data-stu-id="b4c12-269">Xml</span></span> |<span data-ttu-id="b4c12-270">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b4c12-270">Byte[]</span></span> |
| <span data-ttu-id="b4c12-271">Char</span><span class="sxs-lookup"><span data-stu-id="b4c12-271">Char</span></span> |<span data-ttu-id="b4c12-272">문자열</span><span class="sxs-lookup"><span data-stu-id="b4c12-272">String</span></span> |
| <span data-ttu-id="b4c12-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="b4c12-273">VarChar</span></span> |<span data-ttu-id="b4c12-274">문자열</span><span class="sxs-lookup"><span data-stu-id="b4c12-274">String</span></span> |
| <span data-ttu-id="b4c12-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="b4c12-275">LongVarChar</span></span> |<span data-ttu-id="b4c12-276">문자열</span><span class="sxs-lookup"><span data-stu-id="b4c12-276">String</span></span> |
| <span data-ttu-id="b4c12-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="b4c12-277">DB2DynArray</span></span> |<span data-ttu-id="b4c12-278">문자열</span><span class="sxs-lookup"><span data-stu-id="b4c12-278">String</span></span> |
| <span data-ttu-id="b4c12-279">이진</span><span class="sxs-lookup"><span data-stu-id="b4c12-279">Binary</span></span> |<span data-ttu-id="b4c12-280">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b4c12-280">Byte[]</span></span> |
| <span data-ttu-id="b4c12-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="b4c12-281">VarBinary</span></span> |<span data-ttu-id="b4c12-282">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b4c12-282">Byte[]</span></span> |
| <span data-ttu-id="b4c12-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="b4c12-283">LongVarBinary</span></span> |<span data-ttu-id="b4c12-284">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b4c12-284">Byte[]</span></span> |
| <span data-ttu-id="b4c12-285">Graphic</span><span class="sxs-lookup"><span data-stu-id="b4c12-285">Graphic</span></span> |<span data-ttu-id="b4c12-286">문자열</span><span class="sxs-lookup"><span data-stu-id="b4c12-286">String</span></span> |
| <span data-ttu-id="b4c12-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="b4c12-287">VarGraphic</span></span> |<span data-ttu-id="b4c12-288">문자열</span><span class="sxs-lookup"><span data-stu-id="b4c12-288">String</span></span> |
| <span data-ttu-id="b4c12-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="b4c12-289">LongVarGraphic</span></span> |<span data-ttu-id="b4c12-290">문자열</span><span class="sxs-lookup"><span data-stu-id="b4c12-290">String</span></span> |
| <span data-ttu-id="b4c12-291">Clob</span><span class="sxs-lookup"><span data-stu-id="b4c12-291">Clob</span></span> |<span data-ttu-id="b4c12-292">문자열</span><span class="sxs-lookup"><span data-stu-id="b4c12-292">String</span></span> |
| <span data-ttu-id="b4c12-293">Blob</span><span class="sxs-lookup"><span data-stu-id="b4c12-293">Blob</span></span> |<span data-ttu-id="b4c12-294">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b4c12-294">Byte[]</span></span> |
| <span data-ttu-id="b4c12-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="b4c12-295">DbClob</span></span> |<span data-ttu-id="b4c12-296">문자열</span><span class="sxs-lookup"><span data-stu-id="b4c12-296">String</span></span> |
| <span data-ttu-id="b4c12-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="b4c12-297">SmallInt</span></span> |<span data-ttu-id="b4c12-298">Int16</span><span class="sxs-lookup"><span data-stu-id="b4c12-298">Int16</span></span> |
| <span data-ttu-id="b4c12-299">Integer</span><span class="sxs-lookup"><span data-stu-id="b4c12-299">Integer</span></span> |<span data-ttu-id="b4c12-300">Int32</span><span class="sxs-lookup"><span data-stu-id="b4c12-300">Int32</span></span> |
| <span data-ttu-id="b4c12-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="b4c12-301">BigInt</span></span> |<span data-ttu-id="b4c12-302">Int64</span><span class="sxs-lookup"><span data-stu-id="b4c12-302">Int64</span></span> |
| <span data-ttu-id="b4c12-303">Real</span><span class="sxs-lookup"><span data-stu-id="b4c12-303">Real</span></span> |<span data-ttu-id="b4c12-304">단일</span><span class="sxs-lookup"><span data-stu-id="b4c12-304">Single</span></span> |
| <span data-ttu-id="b4c12-305">Double</span><span class="sxs-lookup"><span data-stu-id="b4c12-305">Double</span></span> |<span data-ttu-id="b4c12-306">Double</span><span class="sxs-lookup"><span data-stu-id="b4c12-306">Double</span></span> |
| <span data-ttu-id="b4c12-307">Float</span><span class="sxs-lookup"><span data-stu-id="b4c12-307">Float</span></span> |<span data-ttu-id="b4c12-308">Double</span><span class="sxs-lookup"><span data-stu-id="b4c12-308">Double</span></span> |
| <span data-ttu-id="b4c12-309">10진수</span><span class="sxs-lookup"><span data-stu-id="b4c12-309">Decimal</span></span> |<span data-ttu-id="b4c12-310">10진수</span><span class="sxs-lookup"><span data-stu-id="b4c12-310">Decimal</span></span> |
| <span data-ttu-id="b4c12-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="b4c12-311">DecimalFloat</span></span> |<span data-ttu-id="b4c12-312">10진수</span><span class="sxs-lookup"><span data-stu-id="b4c12-312">Decimal</span></span> |
| <span data-ttu-id="b4c12-313">숫자</span><span class="sxs-lookup"><span data-stu-id="b4c12-313">Numeric</span></span> |<span data-ttu-id="b4c12-314">10진수</span><span class="sxs-lookup"><span data-stu-id="b4c12-314">Decimal</span></span> |
| <span data-ttu-id="b4c12-315">Date</span><span class="sxs-lookup"><span data-stu-id="b4c12-315">Date</span></span> |<span data-ttu-id="b4c12-316">DateTime</span><span class="sxs-lookup"><span data-stu-id="b4c12-316">DateTime</span></span> |
| <span data-ttu-id="b4c12-317">Time</span><span class="sxs-lookup"><span data-stu-id="b4c12-317">Time</span></span> |<span data-ttu-id="b4c12-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b4c12-318">TimeSpan</span></span> |
| <span data-ttu-id="b4c12-319">Timestamp</span><span class="sxs-lookup"><span data-stu-id="b4c12-319">Timestamp</span></span> |<span data-ttu-id="b4c12-320">Datetime</span><span class="sxs-lookup"><span data-stu-id="b4c12-320">DateTime</span></span> |
| <span data-ttu-id="b4c12-321">xml</span><span class="sxs-lookup"><span data-stu-id="b4c12-321">Xml</span></span> |<span data-ttu-id="b4c12-322">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b4c12-322">Byte[]</span></span> |
| <span data-ttu-id="b4c12-323">Char</span><span class="sxs-lookup"><span data-stu-id="b4c12-323">Char</span></span> |<span data-ttu-id="b4c12-324">문자열</span><span class="sxs-lookup"><span data-stu-id="b4c12-324">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="b4c12-325">원본 toosink 열 매핑</span><span class="sxs-lookup"><span data-stu-id="b4c12-325">Map source toosink columns</span></span>
<span data-ttu-id="b4c12-326">hello 싱크 데이터 집합의 원본 데이터 집합 toocolumns hello의에서 toomap 열 참조 toolearn [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-326">toolearn how toomap columns in hello source dataset toocolumns in hello sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="b4c12-327">관계형 원본에서 반복 가능한 읽기</span><span class="sxs-lookup"><span data-stu-id="b4c12-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="b4c12-328">관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에 반복성을 유지 의도 하지 않은 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-328">When you copy data from a relational data store, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="b4c12-329">Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="b4c12-330">Hello 재시도 구성할 수도 있습니다 **정책** dataset toorerun 오류 발생 시 분할 영역에 대 한 속성.</span><span class="sxs-lookup"><span data-stu-id="b4c12-330">You can also configure hello retry **policy** property for a dataset toorerun a slice when a failure occurs.</span></span> <span data-ttu-id="b4c12-331">동일한 데이터 방법에 관계 없이 읽는 hello 하 고 있는지 확인을 다시 실행 하 고 hello 조각을 다시 실행 방법에 관계 없이 여러 번 hello 조각이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-331">Make sure that hello same data is read no matter how many times hello slice is rerun, and regardless of how you rerun hello slice.</span></span> <span data-ttu-id="b4c12-332">자세한 내용은 [관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4c12-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b4c12-333">성능 및 튜닝</span><span class="sxs-lookup"><span data-stu-id="b4c12-333">Performance and tuning</span></span>
<span data-ttu-id="b4c12-334">복사 활동와 같은 방법으로 toooptimize 성능을 hello에 hello 성능에 영향을 주는 주요 요인에 대 한 자세한 내용은 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4c12-334">Learn about key factors that affect hello performance of Copy Activity and ways toooptimize performance in hello [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
