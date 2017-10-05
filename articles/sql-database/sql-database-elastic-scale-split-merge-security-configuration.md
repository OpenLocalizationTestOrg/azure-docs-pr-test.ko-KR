---
title: "분할-병합 보안 구성 | Microsoft Docs"
description: "암호화에 대한 409 인증서를 설정"
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 7e6ccf51a4b75eef16a7df5c1a1018954af8e5dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="9cb61-103">분할-병합 보안 구성</span><span class="sxs-lookup"><span data-stu-id="9cb61-103">Split-merge security configuration</span></span>
<span data-ttu-id="9cb61-104">분할/병합 서비스를 사용하려면 보안을 올바르게 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-104">To use the Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="9cb61-105">서비스는 Microsoft Azure SQL 데이터베이스의 탄력적인 확장 기능에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-105">The service is part of the Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="9cb61-106">자세한 내용은 [탄력적인 확장 분할 및 병합 서비스 자습서](sql-database-elastic-scale-configure-deploy-split-and-merge.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cb61-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="9cb61-107">인증서 구성</span><span class="sxs-lookup"><span data-stu-id="9cb61-107">Configuring certificates</span></span>
<span data-ttu-id="9cb61-108">인증서는 두 가지 방법으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="9cb61-109">SSL 인증서를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="9cb61-109">To Configure the SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="9cb61-110">클라이언트 인증서를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="9cb61-110">To Configure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="to-obtain-certificates"></a><span data-ttu-id="9cb61-111">인증서를 얻으려면</span><span class="sxs-lookup"><span data-stu-id="9cb61-111">To obtain certificates</span></span>
<span data-ttu-id="9cb61-112">공용 CA(인증 기관) 또는 [Windows 인증서 서비스](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx)에서 인증서를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-112">Certificates can be obtained from public Certificate Authorities (CAs) or from the [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="9cb61-113">인증서를 가져올 때 이러한 방법이 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-113">These are the preferred methods to obtain certificates.</span></span>

<span data-ttu-id="9cb61-114">이러한 옵션을 사용할 수 없는 경우 **자체 서명된 인증서**를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-to-generate-certificates"></a><span data-ttu-id="9cb61-115">인증서를 생성하는 도구</span><span class="sxs-lookup"><span data-stu-id="9cb61-115">Tools to generate certificates</span></span>
* [<span data-ttu-id="9cb61-116">makecert.exe</span><span class="sxs-lookup"><span data-stu-id="9cb61-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="9cb61-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="9cb61-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="to-run-the-tools"></a><span data-ttu-id="9cb61-118">도구를 실행하려면</span><span class="sxs-lookup"><span data-stu-id="9cb61-118">To run the tools</span></span>
* <span data-ttu-id="9cb61-119">Visual Studio용 개발자 명령 프롬프트에서 [Visual Studio 명령 프롬프트를 참조하세요](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="9cb61-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="9cb61-120">설치되어 있는 경우 다음으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="9cb61-121">WDK 가져오기 [Windows 8.1: 키트 및 도구 다운로드](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="9cb61-121">Get the WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="to-configure-the-ssl-certificate"></a><span data-ttu-id="9cb61-122">SSL 인증서를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="9cb61-122">To configure the SSL certificate</span></span>
<span data-ttu-id="9cb61-123">통신을 암호화하고 서버를 인증하려면 SSL 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-123">A SSL certificate is required to encrypt the communication and authenticate the server.</span></span> <span data-ttu-id="9cb61-124">아래 세 가지 시나리오 중 가장 적합한 시나리오를 선택하고 모든 단계를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-124">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="9cb61-125">자체 서명된 새로운 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="9cb61-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="9cb61-126">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="9cb61-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="9cb61-127">자체 서명된 SSL 인증서용 PFX 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="9cb61-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="9cb61-128">클라우드 서비스에 SSL 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="9cb61-128">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="9cb61-129">서비스 구성 파일에서 SSL 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="9cb61-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="9cb61-130">SSL 인증 기관 가져오기</span><span class="sxs-lookup"><span data-stu-id="9cb61-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="to-use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="9cb61-131">인증서 저장소에서 기존 인증서를 사용하려면</span><span class="sxs-lookup"><span data-stu-id="9cb61-131">To use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="9cb61-132">인증서 저장소에서 SSL 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="9cb61-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="9cb61-133">클라우드 서비스에 SSL 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="9cb61-133">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="9cb61-134">서비스 구성 파일에서 SSL 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="9cb61-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="to-use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="9cb61-135">PFX 파일에서 기존 인증서를 사용하려면</span><span class="sxs-lookup"><span data-stu-id="9cb61-135">To use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="9cb61-136">클라우드 서비스에 SSL 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="9cb61-136">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="9cb61-137">서비스 구성 파일에서 SSL 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="9cb61-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="to-configure-client-certificates"></a><span data-ttu-id="9cb61-138">클라이언트 인증서를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="9cb61-138">To configure client certificates</span></span>
<span data-ttu-id="9cb61-139">클라이언트 인증서는 서비스에 요청을 인증하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-139">Client certificates are required in order to authenticate requests to the service.</span></span> <span data-ttu-id="9cb61-140">아래 세 가지 시나리오 중 가장 적합한 시나리오를 선택하고 모든 단계를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-140">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="9cb61-141">클라이언트 인증서 해제</span><span class="sxs-lookup"><span data-stu-id="9cb61-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="9cb61-142">클라이언트 인증서 기반 인증 해제</span><span class="sxs-lookup"><span data-stu-id="9cb61-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="9cb61-143">자체 서명된 새로운 클라이언트 인증서 발급</span><span class="sxs-lookup"><span data-stu-id="9cb61-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="9cb61-144">자체 서명된 인증 기관 만들기</span><span class="sxs-lookup"><span data-stu-id="9cb61-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="9cb61-145">클라우드 서비스에 CA 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="9cb61-145">Upload CA Certificate to Cloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="9cb61-146">서비스 구성 파일의 CA 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="9cb61-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="9cb61-147">클라이언트 인증서 발급</span><span class="sxs-lookup"><span data-stu-id="9cb61-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="9cb61-148">클라이언트 인증서용 PFX 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="9cb61-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="9cb61-149">클라이언트 인증서 가져오기</span><span class="sxs-lookup"><span data-stu-id="9cb61-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="9cb61-150">클라이언트 인증서 지문 복사</span><span class="sxs-lookup"><span data-stu-id="9cb61-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="9cb61-151">서비스 구성 파일에서 허용된 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="9cb61-151">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="9cb61-152">기존 클라이언트 인증서 사용</span><span class="sxs-lookup"><span data-stu-id="9cb61-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="9cb61-153">Find CA Public Key</span><span class="sxs-lookup"><span data-stu-id="9cb61-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="9cb61-154">클라우드 서비스에 CA 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="9cb61-154">Upload CA Certificate to Cloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="9cb61-155">서비스 구성 파일의 CA 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="9cb61-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="9cb61-156">클라이언트 인증서 지문 복사</span><span class="sxs-lookup"><span data-stu-id="9cb61-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="9cb61-157">서비스 구성 파일에서 허용된 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="9cb61-157">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="9cb61-158">클라이언트 인증서 해지 확인 구성</span><span class="sxs-lookup"><span data-stu-id="9cb61-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="9cb61-159">허용된 IP 주소</span><span class="sxs-lookup"><span data-stu-id="9cb61-159">Allowed IP addresses</span></span>
<span data-ttu-id="9cb61-160">특정 범위의 IP 주소에서만 서비스 끝점에 액세스하도록 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-160">Access to the service endpoints can be restricted to specific ranges of IP addresses.</span></span>

## <a name="to-configure-encryption-for-the-store"></a><span data-ttu-id="9cb61-161">저장소에 대한 암호화를 구성하려면</span><span class="sxs-lookup"><span data-stu-id="9cb61-161">To configure encryption for the store</span></span>
<span data-ttu-id="9cb61-162">메타데이터 저장소에 저장된 자격 증명을 암호화하려면 인증서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-162">A certificate is required to encrypt the credentials that are stored in the metadata store.</span></span> <span data-ttu-id="9cb61-163">아래 세 가지 시나리오 중 가장 적합한 시나리오를 선택하고 모든 단계를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-163">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="9cb61-164">자체 서명된 새로운 인증서 사용</span><span class="sxs-lookup"><span data-stu-id="9cb61-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="9cb61-165">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="9cb61-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="9cb61-166">자체 서명된 암호화 인증서용 PFX 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="9cb61-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="9cb61-167">클라우드 서비스에 암호화 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="9cb61-167">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="9cb61-168">서비스 구성 파일에서 암호화 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="9cb61-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="9cb61-169">인증서 저장소에서 기존 인증서 사용</span><span class="sxs-lookup"><span data-stu-id="9cb61-169">Use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="9cb61-170">인증서 저장소에서 암호화 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="9cb61-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="9cb61-171">클라우드 서비스에 암호화 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="9cb61-171">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="9cb61-172">서비스 구성 파일에서 암호화 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="9cb61-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="9cb61-173">PFX 파일에서 기존 인증서 사용</span><span class="sxs-lookup"><span data-stu-id="9cb61-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="9cb61-174">클라우드 서비스에 암호화 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="9cb61-174">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="9cb61-175">서비스 구성 파일에서 암호화 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="9cb61-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="the-default-configuration"></a><span data-ttu-id="9cb61-176">기본 구성</span><span class="sxs-lookup"><span data-stu-id="9cb61-176">The default configuration</span></span>
<span data-ttu-id="9cb61-177">기본 구성에서는 HTTP 끝점에 대한 모든 액세스를 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-177">The default configuration denies all access to the HTTP endpoint.</span></span> <span data-ttu-id="9cb61-178">이러한 끝점에 대한 요청에서는 데이터베이스 자격 증명과 같은 중요한 정보가 전송될 수 있으므로 이 설정을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-178">This is the recommended setting, since the requests to these endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="9cb61-179">기본 구성에서는 HTTPS 끝점에 대한 모든 액세스가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-179">The default configuration allows all access to the HTTPS endpoint.</span></span> <span data-ttu-id="9cb61-180">이 설정을 추가로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-180">This setting may be restricted further.</span></span>

### <a name="changing-the-configuration"></a><span data-ttu-id="9cb61-181">구성 변경</span><span class="sxs-lookup"><span data-stu-id="9cb61-181">Changing the Configuration</span></span>
<span data-ttu-id="9cb61-182">**서비스 구성 파일**의 **<EndpointAcls>** 섹션에서 끝점에 적용되는 액세스 제어 규칙 그룹을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-182">The group of access control rules that apply to and endpoint are configured in the **<EndpointAcls>** section in the **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="9cb61-183">액세스 제어 그룹의 규칙은 서비스 구성 파일의 <AccessControl name=""> 섹션에서 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-183">The rules in an access control group are configured in a <AccessControl name=""> section of the service configuration file.</span></span> 

<span data-ttu-id="9cb61-184">해당 형식에 대한 설명은 네트워크 액세스 제어 목록 설명서에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-184">The format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="9cb61-185">예를 들어 100.100.0.0~100.100.255.255 범위의 IP만 HTTPS 끝점에 액세스하도록 허용하려는 경우의 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-185">For example, to allow only IPs in the range 100.100.0.0 to 100.100.255.255 to access the HTTPS endpoint, the rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="9cb61-186">서비스 거부 방지</span><span class="sxs-lookup"><span data-stu-id="9cb61-186">Denial of service prevention</span></span>
<span data-ttu-id="9cb61-187">서비스 거부 공격을 검색 및 방지할 수 있도록 지원하는 메커니즘이 두 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-187">There are two different mechanisms supported to detect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="9cb61-188">원격 호스트당 동시 요청 수 제한(기본적으로 해제됨)</span><span class="sxs-lookup"><span data-stu-id="9cb61-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="9cb61-189">원격 호스트당 액세스 속도 제한(기본적으로 설정됨)</span><span class="sxs-lookup"><span data-stu-id="9cb61-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="9cb61-190">이러한 메커니즘은 IIS의 동적 IP 보안에 자세히 설명되어 있는 기능을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-190">These are based on the features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="9cb61-191">이 구성을 변경할 때 다음과 같은 요인에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="9cb61-191">When changing this configuration beware of the following factors:</span></span>

* <span data-ttu-id="9cb61-192">프록시 및 원격 호스트 정보를 통한 Network Address Translation 장치의 동작</span><span class="sxs-lookup"><span data-stu-id="9cb61-192">The behavior of proxies and Network Address Translation devices over the remote host information</span></span>
* <span data-ttu-id="9cb61-193">웹 역할의 모든 리소스에 대한 각 요청(예: 스크립트, 이미지 등 로드) 이 고려됨</span><span class="sxs-lookup"><span data-stu-id="9cb61-193">Each request to any resource in the web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="9cb61-194">동시 액세스 수 제한</span><span class="sxs-lookup"><span data-stu-id="9cb61-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="9cb61-195">이 동작을 구성하는 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-195">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="9cb61-196">이 보호를 사용하도록 설정하려면 DynamicIpRestrictionDenyByConcurrentRequests를 true로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-196">Change DynamicIpRestrictionDenyByConcurrentRequests to true to enable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="9cb61-197">액세스 속도 제한</span><span class="sxs-lookup"><span data-stu-id="9cb61-197">Restricting rate of access</span></span>
<span data-ttu-id="9cb61-198">이 동작을 구성하는 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-198">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-the-response-to-a-denied-request"></a><span data-ttu-id="9cb61-199">거부된 요청에 대한 응답 구성</span><span class="sxs-lookup"><span data-stu-id="9cb61-199">Configuring the response to a denied request</span></span>
<span data-ttu-id="9cb61-200">다음 설정은 거부된 요청에 대한 응답을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-200">The following setting configures the response to a denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="9cb61-201">기타 지원되는 값에 대해서는 IIS의 동적 IP 보안에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cb61-201">Refer to the documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="9cb61-202">서비스 인증서 구성 작업</span><span class="sxs-lookup"><span data-stu-id="9cb61-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="9cb61-203">이 항목은 참조용일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-203">This topic is for reference only.</span></span> <span data-ttu-id="9cb61-204">아래 항목에 나와 있는 구성 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="9cb61-204">Please follow the configuration steps outlined in:</span></span>

* <span data-ttu-id="9cb61-205">SSL 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="9cb61-205">Configure the SSL certificate</span></span>
* <span data-ttu-id="9cb61-206">클라이언트 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="9cb61-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="9cb61-207">자체 서명된 인증서 만들기</span><span class="sxs-lookup"><span data-stu-id="9cb61-207">Create a self-signed certificate</span></span>
<span data-ttu-id="9cb61-208">다음 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="9cb61-209">사용자 지정하려면:</span><span class="sxs-lookup"><span data-stu-id="9cb61-209">To customize:</span></span>

* <span data-ttu-id="9cb61-210">-n을 서비스 URL로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-210">-n with the service URL.</span></span> <span data-ttu-id="9cb61-211">와일드카드("CN=*.cloudapp.net") 및 대체 이름("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net")이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="9cb61-212">-e 및 인증서 만료 날짜                 강력한 암호를 만들고 메시지가 표시되면 해당 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-212">-e with the certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="9cb61-213">자체 서명된 SSL 인증서용 PFX 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="9cb61-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="9cb61-214">다음 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="9cb61-215">암호를 입력하고 다음 옵션을 사용하여 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="9cb61-216">예, 개인 키를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-216">Yes, export the private key</span></span>
* <span data-ttu-id="9cb61-217">확장된 속성 모두 내보내기</span><span class="sxs-lookup"><span data-stu-id="9cb61-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="9cb61-218">인증서 저장소에서 SSL 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="9cb61-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="9cb61-219">인증서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-219">Find certificate</span></span>
* <span data-ttu-id="9cb61-220">작업-> 모든 작업 -> 내보내기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="9cb61-221">다음 옵션을 사용하여 .PFX 파일로 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="9cb61-222">예, 개인 키를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-222">Yes, export the private key</span></span>
  * <span data-ttu-id="9cb61-223">가능하면 인증 경로에 있는 인증서 모두 포함 *확장된 속성 모두 내보내기</span><span class="sxs-lookup"><span data-stu-id="9cb61-223">Include all certificates in the certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-to-cloud-service"></a><span data-ttu-id="9cb61-224">클라우드 서비스에 SSL 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="9cb61-224">Upload SSL certificate to cloud service</span></span>
<span data-ttu-id="9cb61-225">SSL 키 쌍이 포함된 기존 또는 생성된 .PFX 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-225">Upload certificate with the existing or generated .PFX file with the SSL key pair:</span></span>

* <span data-ttu-id="9cb61-226">개인 키 정보를 보호하는 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-226">Enter the password protecting the private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="9cb61-227">서비스 구성 파일에서 SSL 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="9cb61-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="9cb61-228">클라우드 서비스에 업로드된 인증서의 지문으로 서비스 구성 파일의 다음 설정에 대한 지문 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-228">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="9cb61-229">SSL 인증 기관 가져오기</span><span class="sxs-lookup"><span data-stu-id="9cb61-229">Import SSL certification authority</span></span>
<span data-ttu-id="9cb61-230">서비스와 통신 하는 모든 계정/컴퓨터에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-230">Follow these steps in all account/machine that will communicate with the service:</span></span>

* <span data-ttu-id="9cb61-231">Windows 탐색기에서 CER 파일을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-231">Double-click the .CER file in Windows Explorer</span></span>
* <span data-ttu-id="9cb61-232">인증서 대화 상자에서 인증서 설치를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-232">In the Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="9cb61-233">신뢰할 수 있는 루트 인증 기관 저장소로 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-233">Import certificate into the Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="9cb61-234">클라이언트 인증서 기반 인증 해제</span><span class="sxs-lookup"><span data-stu-id="9cb61-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="9cb61-235">클라이언트 인증서 기반 인증만 지원되며, 이를 사용하지 않으면 다른 메커니즘(예: Microsoft Azure 가상 네트워크)이 없는 한 서비스 끝점에 대한 공용 액세스가 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-235">Only client certificate-based authentication is supported and disabling it will allow for public access to the service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="9cb61-236">서비스 구성 파일에서 이러한 설정을 false로 변경하여 기능을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-236">Change these settings to false in the service configuration file to turn the feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="9cb61-237">그런 다음 CA 인증서 설정의 SSL 인증서와 동일한 지문을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-237">Then, copy the same thumbprint as the SSL certificate in the CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="9cb61-238">자체 서명된 인증 기관 만들기</span><span class="sxs-lookup"><span data-stu-id="9cb61-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="9cb61-239">다음 단계를 실행하여 인증 기관 역할을 할 자체 서명된 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-239">Execute the following steps to create a self-signed certificate to act as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="9cb61-240">이를 사용자 지정하려면</span><span class="sxs-lookup"><span data-stu-id="9cb61-240">To customize it</span></span>

* <span data-ttu-id="9cb61-241">-e 및 인증 만료 날짜</span><span class="sxs-lookup"><span data-stu-id="9cb61-241">-e with the certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="9cb61-242">CA 공개 키 찾기</span><span class="sxs-lookup"><span data-stu-id="9cb61-242">Find CA public key</span></span>
<span data-ttu-id="9cb61-243">모든 클라이언트 인증서는 서비스에서 신뢰하는 인증 기관에서 발급해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-243">All client certificates must have been issued by a Certification Authority trusted by the service.</span></span> <span data-ttu-id="9cb61-244">클라우드 서비스에 업로드할 수 있도록 인증에 사용할 클라이언트 인증서를 발급한 인증 기관의 공용 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-244">Find the public key to the Certification Authority that issued the client certificates that are going to be used for authentication in order to upload it to the cloud service.</span></span>

<span data-ttu-id="9cb61-245">공용 키가 포함된 파일을 사용할 수 없는 경우 인증서 저장소에서 이 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-245">If the file with the public key is not available, export it from the certificate store:</span></span>

* <span data-ttu-id="9cb61-246">인증서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-246">Find certificate</span></span>
  * <span data-ttu-id="9cb61-247">동일한 인증 기관에서 발급한 클라이언트 인증서를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-247">Search for a client certificate issued by the same Certification Authority</span></span>
* <span data-ttu-id="9cb61-248">인증서를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-248">Double-click the certificate.</span></span>
* <span data-ttu-id="9cb61-249">인증서 대화 상자에서 인증 경로 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-249">Select the Certification Path tab in the Certificate dialog.</span></span>
* <span data-ttu-id="9cb61-250">경로의 CA 항목을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-250">Double-click the CA entry in the path.</span></span>
* <span data-ttu-id="9cb61-251">인증서 속성을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-251">Take notes of the certificate properties.</span></span>
* <span data-ttu-id="9cb61-252">**인증서** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-252">Close the **Certificate** dialog.</span></span>
* <span data-ttu-id="9cb61-253">인증서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-253">Find certificate</span></span>
  * <span data-ttu-id="9cb61-254">위에서 기록한 CA를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-254">Search for the CA noted above.</span></span>
* <span data-ttu-id="9cb61-255">작업-> 모든 작업 -> 내보내기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="9cb61-256">다음 옵션을 사용하여 .CER 파일로 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="9cb61-257">**아니요, 개인 키를 내보내지 않습니다.**</span><span class="sxs-lookup"><span data-stu-id="9cb61-257">**No, do not export the private key**</span></span>
  * <span data-ttu-id="9cb61-258">가능하면 인증 경로에 있는 인증서 모두 포함</span><span class="sxs-lookup"><span data-stu-id="9cb61-258">Include all certificates in the certification path if possible.</span></span>
  * <span data-ttu-id="9cb61-259">확장된 속성 모두 내보내기</span><span class="sxs-lookup"><span data-stu-id="9cb61-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-to-cloud-service"></a><span data-ttu-id="9cb61-260">클라우드 서비스에 CA 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="9cb61-260">Upload CA certificate to cloud service</span></span>
<span data-ttu-id="9cb61-261">CA 공개 키가 포함된 기존 또는 생성된 .CER 파일과 함께 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-261">Upload certificate with the existing or generated .CER file with the CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="9cb61-262">서비스 구성 파일의 CA 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="9cb61-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="9cb61-263">클라우드 서비스에 업로드된 인증서의 지문으로 서비스 구성 파일의 다음 설정에 대한 지문 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-263">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="9cb61-264">동일한 지문으로 다음 설정의 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-264">Update the value of the following setting with the same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="9cb61-265">클라이언트 인증서 발급</span><span class="sxs-lookup"><span data-stu-id="9cb61-265">Issue client certificates</span></span>
<span data-ttu-id="9cb61-266">서비스에 액세스할 수 있는 권한이 부여된 각 개인은 단독 사용을 위해 클라이언트 인증서를 발급해야 하며 해당 개인 키를 보호 하기 위한 강력한 암호를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-266">Each individual authorized to access the service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password to protect its private key.</span></span> 

<span data-ttu-id="9cb61-267">다음 단계는 자체 서명된 CA 인증서를 생성하고 저장한 동일한 컴퓨터에서 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-267">The following steps must be executed in the same machine where the self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="9cb61-268">사용자 지정:</span><span class="sxs-lookup"><span data-stu-id="9cb61-268">Customizing:</span></span>

* <span data-ttu-id="9cb61-269">-n 및 이 인증서로 인증할 클라이언트의 ID</span><span class="sxs-lookup"><span data-stu-id="9cb61-269">-n with an ID for to the client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="9cb61-270">-e 및 인증서 만료 날짜</span><span class="sxs-lookup"><span data-stu-id="9cb61-270">-e with the certificate expiration date</span></span>
* <span data-ttu-id="9cb61-271">MyID.pvk 및 MyID.cer과 이 클라이언트 인증서의 고유한 파일 이름</span><span class="sxs-lookup"><span data-stu-id="9cb61-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="9cb61-272">이 명령은 암호를 만들어 한 번 사용하라는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-272">This command will prompt for a password to be created and then used once.</span></span> <span data-ttu-id="9cb61-273">강력한 암호를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="9cb61-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="9cb61-274">클라이언트 인증서용 PFX 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="9cb61-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="9cb61-275">생성된 각 클라이언트 인증서에 대해 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="9cb61-276">사용자 지정:</span><span class="sxs-lookup"><span data-stu-id="9cb61-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the client certificate

<span data-ttu-id="9cb61-277">암호를 입력하고 다음 옵션을 사용하여 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="9cb61-278">예, 개인 키를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-278">Yes, export the private key</span></span>
* <span data-ttu-id="9cb61-279">확장된 속성 모두 내보내기</span><span class="sxs-lookup"><span data-stu-id="9cb61-279">Export all extended properties</span></span>
* <span data-ttu-id="9cb61-280">이 인증서를 발급하는 개인이 내보내기 암호를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-280">The individual to whom this certificate is being issued should choose the export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="9cb61-281">클라이언트 인증서 가져오기</span><span class="sxs-lookup"><span data-stu-id="9cb61-281">Import client certificate</span></span>
<span data-ttu-id="9cb61-282">클라이언트 인증서를 발급받은 개별 사용자는 서비스와 통신하는 데 사용할 컴퓨터의 키 쌍을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-282">Each individual for whom a client certificate has been issued should import the key pair in the machines he/she will use to communicate with the service:</span></span>

* <span data-ttu-id="9cb61-283">Windows 탐색기에서 .PFX 파일을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-283">Double-click the .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="9cb61-284">적어도 다음 옵션을 사용하여 개인 저장소에 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-284">Import certificate into the Personal store with at least this option:</span></span>
  * <span data-ttu-id="9cb61-285">확장된 속성 모두 포함 옵션 선택</span><span class="sxs-lookup"><span data-stu-id="9cb61-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="9cb61-286">클라이언트 인증서 지문 복사</span><span class="sxs-lookup"><span data-stu-id="9cb61-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="9cb61-287">클라이언트 인증서를 발급한 각 개인이 서비스 구성 파일에 추가할 인증서의 지문을 가져오려면 다음 단계를 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-287">Each individual for whom a client certificate has been issued must follow these steps in order to obtain the thumbprint of his/hers certificate which will be added to the service configuration file:</span></span>

* <span data-ttu-id="9cb61-288">Certmgr.exe 실행</span><span class="sxs-lookup"><span data-stu-id="9cb61-288">Run certmgr.exe</span></span>
* <span data-ttu-id="9cb61-289">개인 탭 선택</span><span class="sxs-lookup"><span data-stu-id="9cb61-289">Select the Personal tab</span></span>
* <span data-ttu-id="9cb61-290">인증에 사용할 클라이언트 인증서를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-290">Double-click the client certificate to be used for authentication</span></span>
* <span data-ttu-id="9cb61-291">표시되는 인증서 대화 상자에서 세부 정보 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-291">In the Certificate dialog that opens, select the Details tab</span></span>
* <span data-ttu-id="9cb61-292">표시가 모두를 나타내는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="9cb61-293">목록에서 지문이라는 필드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-293">Select the field named Thumbprint in the list</span></span>
* <span data-ttu-id="9cb61-294">지문 값을 복사합니다. ** 첫 번째 숫자 앞에 표시되지 않는 유니코드 문자를 삭제합니다.** 모든 공백을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-294">Copy the value of the thumbprint ** Delete non-visible Unicode characters in front of the first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-the-service-configuration-file"></a><span data-ttu-id="9cb61-295">서비스 구성 파일에서 허용된 클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="9cb61-295">Configure Allowed clients in the service configuration file</span></span>
<span data-ttu-id="9cb61-296">서비스 구성 파일에서 다음 설정의 값을 서비스에 대한 액세스가 허용된 클라이언트 인증서의 지문 목록(쉼표로 구분)으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-296">Update the value of the following setting in the service configuration file with a comma-separated list of the thumbprints of the client certificates allowed access to the service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="9cb61-297">클라이언트 인증서 해지 확인 구성</span><span class="sxs-lookup"><span data-stu-id="9cb61-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="9cb61-298">기본 설정은 인증 기관으로 클라이언트 인증서 해지 상태를 확인하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-298">The default setting does not check with the Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="9cb61-299">확인을 설정하려면 클라이언트 인증서를 발급한 인증 기관에서 이러한 확인을 지원하는 경우 X509RevocationMode 열거에 정의된 값 중 하나로 다음 설정을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-299">To turn on the checks, if the Certification Authority which issued the client certificates supports such checks, change the following setting with one of the values defined in the X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="9cb61-300">자체 서명된 암호화 인증서용 PFX 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="9cb61-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="9cb61-301">암호화 인증서에 대해 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="9cb61-302">사용자 지정:</span><span class="sxs-lookup"><span data-stu-id="9cb61-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the encryption certificate

<span data-ttu-id="9cb61-303">암호를 입력하고 다음 옵션을 사용하여 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="9cb61-304">예, 개인 키를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-304">Yes, export the private key</span></span>
* <span data-ttu-id="9cb61-305">확장된 속성 모두 내보내기</span><span class="sxs-lookup"><span data-stu-id="9cb61-305">Export all extended properties</span></span>
* <span data-ttu-id="9cb61-306">클라우드 서비스에 인증서를 업로드할 때 암호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-306">You will need the password when uploading the certificate to the cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="9cb61-307">인증서 저장소에서 암호화 인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="9cb61-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="9cb61-308">인증서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-308">Find certificate</span></span>
* <span data-ttu-id="9cb61-309">작업-> 모든 작업 -> 내보내기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="9cb61-310">다음 옵션을 사용하여 .PFX 파일로 인증서를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="9cb61-311">예, 개인 키를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-311">Yes, export the private key</span></span>
  * <span data-ttu-id="9cb61-312">가능하면 인증 경로에 있는 인증서 모두 포함</span><span class="sxs-lookup"><span data-stu-id="9cb61-312">Include all certificates in the certification path if possible</span></span> 
* <span data-ttu-id="9cb61-313">확장된 속성 모두 내보내기</span><span class="sxs-lookup"><span data-stu-id="9cb61-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-to-cloud-service"></a><span data-ttu-id="9cb61-314">클라우드 서비스에 암호화 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="9cb61-314">Upload encryption certificate to cloud service</span></span>
<span data-ttu-id="9cb61-315">암호화 키 쌍이 포함된 기존 또는 생성된 .PFX 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-315">Upload certificate with the existing or generated .PFX file with the encryption key pair:</span></span>

* <span data-ttu-id="9cb61-316">개인 키 정보를 보호하는 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-316">Enter the password protecting the private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="9cb61-317">서비스 구성 파일에서 암호화 인증서 업데이트</span><span class="sxs-lookup"><span data-stu-id="9cb61-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="9cb61-318">클라우드 서비스에 업로드된 인증서의 지문으로 서비스 구성 파일의 다음 설정에 대한 지문 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-318">Update the thumbprint value of the following settings in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="9cb61-319">일반 인증서 작업</span><span class="sxs-lookup"><span data-stu-id="9cb61-319">Common certificate operations</span></span>
* <span data-ttu-id="9cb61-320">SSL 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="9cb61-320">Configure the SSL certificate</span></span>
* <span data-ttu-id="9cb61-321">클라이언트 인증서 구성</span><span class="sxs-lookup"><span data-stu-id="9cb61-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="9cb61-322">인증서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-322">Find certificate</span></span>
<span data-ttu-id="9cb61-323">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="9cb61-323">Follow these steps:</span></span>

1. <span data-ttu-id="9cb61-324">Mmc.exe를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="9cb61-325">파일-> 스냅인 추가/제거로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="9cb61-326">**인증서**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="9cb61-327">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-327">Click **Add**.</span></span>
5. <span data-ttu-id="9cb61-328">인증서 저장소 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-328">Choose the certificate store location.</span></span>
6. <span data-ttu-id="9cb61-329">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-329">Click **Finish**.</span></span>
7. <span data-ttu-id="9cb61-330">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-330">Click **OK**.</span></span>
8. <span data-ttu-id="9cb61-331">**인증서**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="9cb61-332">인증서 저장소 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-332">Expand the certificate store node.</span></span>
10. <span data-ttu-id="9cb61-333">인증서 하위 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-333">Expand the Certificate child node.</span></span>
11. <span data-ttu-id="9cb61-334">목록에서 인증서를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-334">Select a certificate in the list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="9cb61-335">인증서 내보내기</span><span class="sxs-lookup"><span data-stu-id="9cb61-335">Export certificate</span></span>
<span data-ttu-id="9cb61-336">**인증서 내보내기 마법사**에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-336">In the **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="9cb61-337">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-337">Click **Next**.</span></span>
2. <span data-ttu-id="9cb61-338">**예**, **개인 키 내보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-338">Select **Yes**, then **Export the private key**.</span></span>
3. <span data-ttu-id="9cb61-339">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-339">Click **Next**.</span></span>
4. <span data-ttu-id="9cb61-340">원하는 출력 파일 형식을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-340">Select the desired output file format.</span></span>
5. <span data-ttu-id="9cb61-341">원하는 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-341">Check the desired options.</span></span>
6. <span data-ttu-id="9cb61-342">**암호**를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-342">Check **Password**.</span></span>
7. <span data-ttu-id="9cb61-343">강력한 암호를 입력하고 이를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="9cb61-344">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-344">Click **Next**.</span></span>
9. <span data-ttu-id="9cb61-345">인증서를 저장할 파일 이름을 입력하거나 찾습니다(.PFX 확장명을 사용하여).</span><span class="sxs-lookup"><span data-stu-id="9cb61-345">Type or browse a filename where to store the certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="9cb61-346">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-346">Click **Next**.</span></span>
11. <span data-ttu-id="9cb61-347">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-347">Click **Finish**.</span></span>
12. <span data-ttu-id="9cb61-348">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="9cb61-349">인증서 가져오기</span><span class="sxs-lookup"><span data-stu-id="9cb61-349">Import certificate</span></span>
<span data-ttu-id="9cb61-350">인증서 가져오기 마법사에서:</span><span class="sxs-lookup"><span data-stu-id="9cb61-350">In the Certificate Import Wizard:</span></span>

1. <span data-ttu-id="9cb61-351">저장소 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-351">Select the store location.</span></span>
   
   * <span data-ttu-id="9cb61-352">현재 사용자 계정으로 실행되는 프로세스만 서비스에 액세스하는 경우 **현재 사용자** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-352">Select **Current User** if only processes running under current user will access the service</span></span>
   * <span data-ttu-id="9cb61-353">컴퓨터의 다른 프로세스에서 서비스에 액세스하는 경우 **로컬 컴퓨터** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-353">Select **Local Machine** if other processes in this computer will access the service</span></span>
2. <span data-ttu-id="9cb61-354">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-354">Click **Next**.</span></span>
3. <span data-ttu-id="9cb61-355">파일에서 가져오는 경우 파일 경로를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-355">If importing from a file, confirm the file path.</span></span>
4. <span data-ttu-id="9cb61-356">.PFX 파일을 가져오는 경우:</span><span class="sxs-lookup"><span data-stu-id="9cb61-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="9cb61-357">개인 키를 보호하는 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-357">Enter the password protecting the private key</span></span>
   2. <span data-ttu-id="9cb61-358">가져오기 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-358">Select import options</span></span>
5. <span data-ttu-id="9cb61-359">다음 저장소에 인증서 저장을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-359">Select "Place" certificates in the following store</span></span>
6. <span data-ttu-id="9cb61-360">**찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-360">Click **Browse**.</span></span>
7. <span data-ttu-id="9cb61-361">원하는 저장소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-361">Select the desired store.</span></span>
8. <span data-ttu-id="9cb61-362">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="9cb61-363">신뢰할 수 있는 루트 인증 기관 저장소를 선택한 경우 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-363">If the Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="9cb61-364">모든 대화 상자 창에서 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="9cb61-365">인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="9cb61-365">Upload certificate</span></span>
<span data-ttu-id="9cb61-366">[Azure 포털](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="9cb61-366">In the [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="9cb61-367">**클라우드 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="9cb61-368">클라우드 서비스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-368">Select the cloud service.</span></span>
3. <span data-ttu-id="9cb61-369">최상위 메뉴에서 **인증서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-369">On the top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="9cb61-370">아래쪽 메뉴 모음에서 **업로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-370">On the bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="9cb61-371">인증서 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-371">Select the certificate file.</span></span>
6. <span data-ttu-id="9cb61-372">.PFX 파일인 경우 개인 키에 대한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-372">If it is a .PFX file, enter the password for the private key.</span></span>
7. <span data-ttu-id="9cb61-373">완료되면 목록의 새 항목에서 인증서 지문을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-373">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="9cb61-374">기타 보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="9cb61-374">Other security considerations</span></span>
<span data-ttu-id="9cb61-375">이 문서에 설명된 SSL 설정은 HTTPS 끝점을 사용하는 경우 해당 클라이언트와 서비스 간의 통신을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-375">The SSL settings described in this document encrypt communication between the service and its clients when the HTTPS endpoint is used.</span></span> <span data-ttu-id="9cb61-376">데이터베이스 액세스에 대한 자격 증명 및 기타 잠재적으로 중요한 정보가 통신에 포함되므로 이러한 암호화가 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-376">This is important since credentials for database access and potentially other sensitive information are contained in the communication.</span></span> <span data-ttu-id="9cb61-377">단, 서비스에서 Microsoft Azure 구독의 메타데이터 저장소에 대해 제공한 Microsoft Azure SQL 데이터베이스의 내부 테이블에 있는 자격 증명을 비롯하여 내부 상태를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-377">Note, however, that the service persists internal status, including credentials, in its internal tables in the Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="9cb61-378">해당 데이터베이스는 서비스 구성 파일(.CSCFG 파일)에서 다음 설정의 일부로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-378">That database was defined as part of the following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="9cb61-379">이 데이터베이스에 저장된 자격 증명은 암호화됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="9cb61-380">그러나 서비스 배포의 웹 역할과 작업자 역할 모두 최신 상태를 유지하고 저장된 자격 증명의 암호화 및 암호 해독에 사용되는 인증서와 메타데이터 데이터베이스에 액세스할 때 보안을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cb61-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up to date and secure as they both have access to the metadata database and the certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

